---
title: Editor universal
description: Obtenga información acerca de la flexibilidad del editor universal y cómo puede ayudarle a potenciar sus experiencias headless con AEM 6.5.
feature: Developing
role: Developer
exl-id: 7bdf1fcc-02b9-40bc-8605-e6508a84d249
source-git-commit: 9f91063e51aa599ef48967f832aa359ecf100fc2
workflow-type: ht
source-wordcount: '1183'
ht-degree: 100%

---


# Editor universal {#universal-editor}

Obtenga información acerca de la flexibilidad del editor universal y cómo puede ayudarle a potenciar sus experiencias headless con AEM 6.5.

## Información general {#overview}

El editor universal es un editor visual versátil que forma parte de Adobe Experience Manager Sites. Permite a los autores realizar una edición WYSIWYG (lo que ve es lo que obtiene) de cualquier experiencia headless.

* Los autores se benefician de la flexibilidad del editor universal, ya que admite la misma edición visual coherente para todas las formas de contenido sin encabezado de AEM.
* Los desarrolladores se benefician de la versatilidad del editor universal, ya que también admite el desacoplamiento verdadero de la implementación. Permite a los desarrolladores utilizar prácticamente cualquier estructura o arquitectura de su elección, sin imponer restricciones de SDK o tecnológicas.

Consulte la [documentación de AEM as a Cloud Service sobre el editor universal](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) para obtener más información.

## Arquitectura {#architecture}

El editor universal es un servicio que funciona junto con AEM para crear contenido headless.

* El editor universal está alojado en `https://experience.adobe.com/#/aem/editor/canvas` y puede editar páginas procesadas por AEM 6.5.
* El editor universal lee la página de AEM a través de Dispatcher desde la instancia de autor de AEM.
* El servicio de editor universal, que se ejecuta en el mismo host que Dispatcher, vuelve a escribir los cambios en la instancia de autor de AEM.

![Flujo de autor mediante el editor universal](assets/author-flow.png)

## Requisitos {#requirements}

El editor universal es compatible con lo siguiente:

* AEM 6.5
   * Se admiten tanto el alojamiento local como el alojamiento AMS.
* [AEM 6.5 LTS](https://experienceleague.adobe.com/es/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction)
   * Se admiten tanto el alojamiento local como el alojamiento AMS.
* [AEM as a Cloud Service](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)

Este documento se centra en la compatibilidad con AEM 6.5 del editor universal. Para utilizar el editor universal con AEM 6.5, necesitará lo siguiente:

* AEM 6.5 con el Service Pack 23 o superior
   * Los Service Packs 21 y 22 también son compatibles con [un Feature Pack.](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-6.5.21-universal-editor-1.0.0.zip).
* Dispatcher correctamente configurado

## Configuración {#setup}

Para probar el editor universal, deberá hacer lo siguiente:

1. [Configure un servicio de editor universal local.](#set-up-ue)
1. [Ajuste su Dispatcher para permitir el servicio de editor universal.](#update-dispatcher)

Una vez completada la configuración, puede [instrumentar sus aplicaciones para que utilicen el editor universal.](#instrumentation)

### Configuración de servicios {#configure-services}

El editor universal aprovecha varios paquetes para los que se necesita configuración adicional.

#### Establezca el atributo SameSite para la cookie `login-token`. {#samesite-attribute}

1. Abra el Administrador de configuración. 
   * `http://<host>:<port>/system/console/configMgr`
1. Busque **Controlador de autenticación de token de Adobe Granite** en la lista y haga clic en **Cambiar los valores de configuración**.
1. En el cuadro de diálogo, cambie el atributo **SameSite para el valor de la cookie del token de inicio de sesión** (`token.samesite.cookie.attr`) a `Partitioned`.
1. Haga clic en **Guardar**.

#### Quitar la opción X-Frame de encabezados `SAMEORIGIN`. {#sameorigin}

1. Abra el Administrador de configuración. 
   * `http://<host>:<port>/system/console/configMgr`
1. Busque **Servlet principal de Apache Sling** en la lista y haga clic en **Editar los valores de configuración**.
1. Elimine el valor `X-Frame-Options=SAMEORIGIN` del atributo **Encabezados de respuesta adicionales** (`sling.additional.response.headers`) si existe.
1. Haga clic en **Guardar**.

#### Configure el Controlador de autenticación del parámetro de consulta de Adobe Granite. {#query-parameter}

1. Abra el Administrador de configuración. 
   * `http://<host>:<port>/system/console/configMgr`
1. Busque **Controlador de autenticación del parámetro de consulta de Adobe Granite** en la lista y haga clic en **Editar los valores de configuración**.
1. En el campo **Ruta** (`path`), añada `/` para habilitarlo.
   * Un valor vacío deshabilita el controlador de autenticación.
1. Haga clic en **Guardar**.

#### Defina para qué rutas de contenido o `sling:resourceTypes` se abrirá el editor universal. {#paths}

1. Abra el Administrador de configuración. 
   * `http://<host>:<port>/system/console/configMgr`
1. Busque **Servicio de URL del editor universal** en la lista y haga clic en **Editar los valores de configuración**.
1. Defina para qué rutas de contenido o `sling:resourceTypes` se abrirá el editor universal.
   * En el campo **Asignación de apertura del editor universal**, proporcione las rutas para las que se abre el editor universal.
   * En el campo **Sling:resourceTypes que abrirá el editor universal**, proporcione una lista de recursos que el editor universal abrirá directamente.
1. Haga clic en **Guardar**.
1. Compruebe la [configuración de su externalizador](/help/sites-developing/externalizer.md) y asegúrese de que dispone al menos de los entornos local, de autor y de publicación establecidos como en el ejemplo siguiente.

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

Una vez completados estos pasos de configuración, AEM abrirá el editor universal para páginas en el siguiente orden.

1. AEM comprobará las asignaciones de `Universal Editor Opening Mapping` y, si el contenido se encuentra en alguna de las rutas definidas, se abrirá el editor universal para él.
1. Para el contenido que no se encuentra en las rutas definidas en `Universal Editor Opening Mapping`, AEM comprueba si el `resourceType` del contenido coincide con los definidos en **Sling:resourceTypes, que abrirá el editor universal**. Si el contenido coincide con uno de esos tipos, el editor universal se abre para él en `${author}${path}.html`.
1. De lo contrario, AEM abre el editor de páginas.

Las siguientes variables están disponibles para definir las asignaciones en `Universal Editor Opening Mapping`.

* `path`: ruta de contenido del recurso que se abre
* `localhost`: entrada del externalizador para `localhost` sin esquema, p. ej., `localhost:4502`
* `author`: entrada del externalizador para el autor sin esquema, p. ej., `localhost:4502`
* `publish`: entrada del externalizador para publicación sin esquema, p. ej., `localhost:4503`
* `preview`: entrada del externalizador para vista previa sin esquema, p. ej., `localhost:4504`
* `env`: `prod`, `stage`, `dev` según los modos de ejecución de Sling definidos
* `token`: token de consulta necesario para `QueryTokenAuthenticationHandler`

Asignaciones de ejemplo:

* Abra todas las páginas de `/content/foo` en AEM Author:
   * `/content/foo:${author}${path}.html?login-token=${token}`
   * Esto resulta en abrir `https://localhost:4502/content/foo/x.html?login-token=<token>`
* Abra todas las páginas de `/content/bar` en un servidor NextJS remoto y proporcione todas las variables como información
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * Esto resulta en abrir `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

### Configuración del servicio de editor universal {#set-up-ue}

Con AEM actualizado y configurado, puede configurar un servicio de editor universal local para sus procesos de desarrollo y pruebas locales.

1. Instale la versión de Node.js >=20.
1. Descargue y desempaquete el servicio de editor universal más reciente de [Distribución de software](https://experienceleague.adobe.com/es/docs/experience-cloud/software-distribution/home)
1. Configure el servicio del editor universal mediante variables de entorno o el archivo `.env`.
   * [Consulte la documentación del editor universal de AEM as a Cloud Service para obtener más información.](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
   * Tenga en cuenta que es posible que necesite utilizar la opción `UES_MAPPING` si se requiere una reescritura de IP interna.
1. Ejecute `universal-editor-service.cjs`

### Actualice Dispatcher {#update-dispatcher}

Con AEM configurado y un servicio de editor universal local en ejecución, deberá permitir un proxy inverso para el nuevo servicio [en Dispatcher.](https://experienceleague.adobe.com/es/docs/experience-manager-dispatcher/using/dispatcher)

1. Ajuste el archivo vhost de la instancia de autor para incluir un proxy inverso.

   ```html
   <IfModule mod_proxy.c>
    ProxyPass "/universal-editor" "http://localhost:8080"
    ProxyPassReverse "/universal-editor" "http://localhost:8080"
   </IfModule>
   ```

   >[!NOTE]
   >
   >8080 es el puerto predeterminado. Si ha cambiado esto usando el parámetro `UES_PORT` en [su archivo `.env`,](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service) debe ajustar el valor del puerto aquí en consecuencia.

1. Reinicie Apache.

## Instrumentalización de la aplicación {#instrumentation}

Con AEM actualizado y un servicio de editor universal local en ejecución, puede comenzar a editar contenido headless mediante el editor universal.

Sin embargo, la aplicación debe estar instrumentada para aprovechar las ventajas del editor universal. Esto implica incluir metaetiquetas para instruir al editor sobre cómo y dónde conservar el contenido. Los detalles de esta instrumentación están disponibles en la [documentación del editor universal para AEM as a Cloud Service.](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page)

Tenga en cuenta que, cuando se sigue la documentación del editor universal con AEM as a Cloud Service, se aplican los siguientes cambios al utilizarlo con AEM 6.5.

* El protocolo de la metaetiqueta debe ser `aem65`, en lugar de `aem`.

  ```html
  <meta name="urn:adobe:aue:system:aemconnection" content={`aem65:${getAuthorHost()}`}/>
  ```

* El punto final del servicio del editor universal debe anunciarse mediante una metaetiqueta.

  ```html
  <meta name="urn:adobe:aue:config:service" content={`${getAuthorHost()}/universal-editor`}/>
  ```

* En la sección `plugins` de la definición de componentes, se debe usar `aem65`, en lugar de `aem`.

>[!TIP]
>
>Para obtener una guía completa para los desarrolladores que empiezan con el editor universal, consulte el documento [Información general del editor universal para desarrolladores de AEM](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/developer-overview) en la documentación de AEM as a Cloud Service. Tenga en cuenta los cambios necesarios para la compatibilidad con AEM 6.5, tal como se menciona en esta sección.

## Diferencias entre AEM 6.5 y AEM as a Cloud Service {#differences}

En líneas generales, el editor universal en AEM 6.5 funciona igual que en AEM as a Cloud Service, incluida la IU y gran parte de la configuración. Sin embargo, hay diferencias que deben señalarse.

* El editor universal de 6.5 solo admite el caso de uso headless.
* La configuración del editor universal varía ligeramente para 6.5 ([como se describe](#setup) en el documento actual).
* El editor universal de 6.5 usa un selector de recursos y un selector de fragmentos de contenido diferentes a los de AEM as a Cloud Service.
