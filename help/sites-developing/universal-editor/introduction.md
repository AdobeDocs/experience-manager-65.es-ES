---
title: El editor universal
description: AEM Obtenga información acerca de la flexibilidad del editor universal y cómo puede ayudarle a potenciar sus experiencias sin encabezado mediante el uso de la versión 6.5 de.
feature: Developing
role: Developer
source-git-commit: a088fcb3069fae7e63c7238710534d817a308eff
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 1%

---


# El editor universal {#universal-editor}

AEM Obtenga información acerca de la flexibilidad del editor universal y cómo puede ayudarle a potenciar sus experiencias sin encabezado mediante el uso de la versión 6.5 de.

## Información general {#overview}

El editor universal es un editor visual versátil que forma parte de Adobe Experience Manager Sites. Permite a los autores editar lo que se ve es lo que se obtiene (WYSIWYG) de cualquier experiencia sin encabezado.

* AEM Los autores se benefician de la flexibilidad del editor universal, ya que es compatible con la misma edición visual coherente para todas las formas de contenido sin encabezado de la.
* Los desarrolladores se benefician de la versatilidad del editor universal, ya que también admite el desacoplamiento real de la implementación. Permite a los desarrolladores utilizar prácticamente cualquier marco o arquitectura de su elección, sin imponer restricciones de SDK o tecnología.

Consulte la [documentación de AEM as a Cloud Service en el editor universal](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) para obtener más información.

## Arquitectura {#architecture}

AEM El editor universal es un servicio que funciona en conjunto con la creación de contenido sin encabezado, lo que lo convierte en una herramienta de creación de contenido sin encabezado.

* AEM El editor universal está alojado en `https://experience.adobe.com/#/aem/editor/canvas` y puede editar las páginas procesadas por la versión 6.5 de la versión de.
* AEM AEM El editor universal lee la página de la a través de Dispatcher desde la instancia de autor.
* El servicio de editor universal, que se ejecuta en el mismo host que Dispatcher AEM, vuelve a escribir los cambios en la instancia de autor de la.

![Flujo de autor mediante el editor universal](assets/author-flow.png)

## Configuración {#setup}

Para probar el editor universal, deberá hacer lo siguiente:

1. [AEM Actualice y configure la instancia de creación de la.](#update-configure-aem)
1. [Configure un servicio de editor universal local.](#set-up-ue)
1. [Ajuste su Dispatcher para permitir el servicio de editor universal.](#update-dispatcher)

Una vez completada la configuración, puede [instrumentar sus aplicaciones para que utilicen el editor universal.](#instrumentation)

### AEM Actualización de {#update-aem}

AEM AEM Se requieren el Service Pack 21 y un paquete de funciones para la para poder utilizar el editor universal con 6.5.

#### Aplicar el paquete de servicio más reciente {#latest}

AEM Asegúrese de que está ejecutando al menos el Service Pack 21 para la versión 6.5 de la versión de la aplicación de. Puede descargar el Service Pack más reciente desde [Distribución de software.](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=es)

#### Instalación del paquete de funciones del editor universal {#feature-pack}

AEM Instale el paquete de funciones del editor universal **para la versión 6.5** [disponible en la distribución de software.](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-6.5.21-universal-editor-1.0.0.zip)

Si ya está ejecutando el Service Pack 23 o superior, este paso no es necesario.

### Configurar servicios {#configure-services}

El paquete de funciones instala una serie de paquetes nuevos para los que se necesita una configuración adicional.

#### Establezca el atributo SameSite para la cookie `login-token`. {#samesite-attribute}

1. Abra el Administrador de configuración.
   * `http://<host>:<port>/system/console/configMgr`
1. Busque **Controlador de autenticación de token de Granite de Adobe** en la lista y haga clic en **Cambiar los valores de configuración**.
1. En el cuadro de diálogo, cambie el atributo **SameSite para el valor de la cookie del token de inicio de sesión** (`token.samesite.cookie.attr`) a `Partitioned`.
1. Haga clic en **Guardar**.

#### Quitar la opción X-Frame de encabezados `SAMEORIGIN`. {#sameorigin}

1. Abra el Administrador de configuración.
   * `http://<host>:<port>/system/console/configMgr`
1. Busque **Apache Sling Main Servlet** en la lista y haga clic en **Editar los valores de configuración**.
1. Elimine el valor `X-Frame-Options=SAMEORIGIN` del atributo **Encabezados de respuesta adicionales** (`sling.additional.response.headers`) si existe.
1. Haga clic en **Guardar**.

#### Configure el Controlador de autenticación del parámetro de consulta de Adobe Granite. {#query-parameter}

1. Abra el Administrador de configuración.
   * `http://<host>:<port>/system/console/configMgr`
1. Busque **Controlador de autenticación de parámetro de Adobe Granite Query** en la lista y haga clic en **Editar los valores de configuración**.
1. En el campo **Ruta** (`path`), agregue `/` para habilitar.
   * Un valor vacío deshabilita el controlador de autenticación.
1. Haga clic en **Guardar**.

#### Defina para qué rutas de contenido o `sling:resourceTypes` se abrirá el editor universal. {#paths}

1. Abra el Administrador de configuración.
   * `http://<host>:<port>/system/console/configMgr`
1. Busque **Servicio de URL del editor universal** en la lista y haga clic en **Editar los valores de configuración**.
1. Defina para qué rutas de contenido o `sling:resourceTypes` se abrirá el editor universal.
   * En el campo **Asignación de apertura de editor universal**, proporcione las rutas para las que se abre el editor universal.
   * En el campo **Sling:resourceTypes que abrirá el editor universal**, proporcione una lista de los recursos que el editor universal abrirá directamente.
1. Haga clic en **Guardar**.

AEM Se abrirá el Editor universal para las páginas basadas en esta configuración.

1. AEM Se comprobarán las asignaciones en `Universal Editor Opening Mapping` y, si el contenido se encuentra en alguna de las rutas definidas, se abrirá el Editor universal para él.
1. AEM Para el contenido que no se encuentra en las rutas definidas en `Universal Editor Opening Mapping`, comprueba si el `resourceType` del contenido coincide con los definidos en **Sling:resourceTypes, que abrirá el editor universal**. Si el contenido coincide con uno de esos tipos, el editor universal se abrirá para él en `${author}${path}.html`.
1. AEM De lo contrario, abre el Editor de páginas.

Las siguientes variables están disponibles para definir las asignaciones en `Universal Editor Opening Mapping`.

* `path`: ruta de contenido del recurso a abrir
* `localhost`: entrada del externalizador para `localhost` sin esquema, p. ej. `localhost:4502`
* `author`: entrada de externalizador para el autor sin esquema, p. ej. `localhost:4502`
* `publish`: entrada de externalizador para publicación sin esquema, p. ej. `localhost:4503`
* `preview`: entrada del externalizador para vista previa sin esquema, p. ej. `localhost:4504`
* `env`: `prod`, `stage`, `dev` según los modos de ejecución de Sling definidos
* `token`: token de consulta necesario para `QueryTokenAuthenticationHandler`

Asignaciones de ejemplo:

* AEM Abra todas las páginas por debajo de `/content/foo` en el Autor de la:
   * `/content/foo:${author}${path}.html?login-token=${token}`
   * Esto resulta en abrir `https://localhost:4502/content/foo/x.html?login-token=<token>`
* Abra todas las páginas por debajo de `/content/bar` en un servidor NextJS remoto y proporcione todas las variables como información
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * Esto resulta en abrir `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

### Configuración del servicio de editor universal {#set-up-ue}

AEM Con la actualización y la configuración de la aplicación, puede configurar un servicio de editor universal local para su propio desarrollo y pruebas locales.

1. Instale la versión de Node.js >=20.
1. Descargue y desempaquete el servicio de editor universal más reciente de [Distribución de software](https://experienceleague.adobe.com/en/docs/experience-cloud/software-distribution/home)
1. Configure el servicio de editor universal mediante variables de entorno o el archivo `.env`.
   * [Consulte la documentación del Editor universal de AEM as a Cloud Service para obtener más información.](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
   * Tenga en cuenta que es posible que necesite utilizar la opción `UES_MAPPING` si se requiere una reescritura de IP interna.
1. Ejecutar `universal-editor-service.cjs`

### Actualización de Dispatcher {#update-dispatcher}

AEM Con el servicio de editor universal local configurado y en ejecución, tendrá que permitir un proxy inverso para el nuevo servicio [en Dispatcher.](https://experienceleague.adobe.com/es/docs/experience-manager-dispatcher/using/dispatcher)

1. Ajuste el archivo vhost de la instancia de autor para incluir un proxy inverso.

   ```html
   <IfModule mod_proxy.c>
    ProxyPass "/universal-editor" "http://localhost:8080"
    ProxyPassReverse "/universal-editor" "http://localhost:8080"
   </IfModule>
   ```

   >[!NOTE]
   >
   >8080 es el puerto predeterminado. Si ha cambiado esto usando el parámetro `UES_PORT` en [su archivo `.env`,](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service) debe ajustar el valor del puerto aquí en consecuencia.

1. Reinicie Apache.

## Instrumentar su aplicación {#instrumentation}

AEM Con el servicio de editor universal local actualizado y en ejecución, puede empezar a editar contenido sin encabezado con el editor universal.

Sin embargo, la aplicación debe estar instrumentada para aprovechar las ventajas del editor universal. Esto implica incluir metaetiquetas para instruir al editor sobre cómo y dónde conservar el contenido. Los detalles de esta instrumentación están disponibles en la [documentación del editor universal para AEM as a Cloud Service.](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page)

Tenga en cuenta que cuando se sigue la documentación del Editor universal con AEM as a Cloud Service AEM, se aplican los siguientes cambios al utilizarlo con.5.

* El protocolo de la metaetiqueta debe ser `aem65` en lugar de `aem`.

  ```html
  <meta name="urn:adobe:aue:system:aemconnection" content={`aem65:${getAuthorHost()}`}/>
  ```

* El punto final del servicio de editor universal debe anunciarse mediante una etiqueta meta.

  ```html
  <meta name="urn:adobe:aue:config:service" content={`${getAuthorHost()}/universal-editor`}/>
  ```

* En la sección `plugins` de la definición de componentes, se debe usar `aem65` en lugar de `aem`.

>[!TIP]
>
>AEM Para obtener una guía completa para desarrolladores que empiecen a usar el Editor universal, consulte el documento [Información general del Editor universal para desarrolladores](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/developer-overview) en la documentación de AEM as a Cloud Service AEM, teniendo en cuenta los cambios necesarios para la compatibilidad con la versión 6.5 de, tal como se menciona en esta sección.
