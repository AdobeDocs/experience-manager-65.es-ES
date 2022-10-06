---
title: 'Desarrollo de AEM: directrices y prácticas recomendadas'
seo-title: AEM Development - Guidelines and Best Practices
description: Directrices y prácticas recomendadas para el desarrollo en AEM
seo-description: Guidelines and best practices for developing on AEM
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
exl-id: 8eef7e4d-a6f2-4b87-a995-0761447283c6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 0%

---

# Desarrollo de AEM: directrices y prácticas recomendadas{#aem-development-guidelines-and-best-practices}

## Directrices para el uso de plantillas y componentes {#guidelines-for-using-templates-and-components}

AEM componentes y plantillas forman un conjunto de herramientas muy potente. Los desarrolladores pueden utilizarlos para proporcionar a los usuarios comerciales, editores y administradores del sitio web la funcionalidad de adaptar sus sitios web a las cambiantes necesidades comerciales (agilidad del contenido), al tiempo que mantienen el diseño uniforme de los sitios (protección de la marca).

Un desafío típico para una persona responsable de un sitio web o conjunto de sitios web (por ejemplo, en una sucursal de una empresa global), es introducir un nuevo tipo de presentación de contenido en sus sitios web.

Supongamos que es necesario agregar una página de lista de noticias a los sitios web, que enumera extractos de otros artículos ya publicados. La página debe tener el mismo diseño y estructura que el resto del sitio web.

La manera recomendada de abordar ese problema sería:

* Vuelva a utilizar una plantilla existente para crear un nuevo tipo de página. La plantilla define aproximadamente la estructura de la página (elementos de navegación, paneles, etc.), que se ajusta aún más con su diseño (CSS, gráficos).
* Utilice el sistema de párrafos (parsys/iparsys) en las nuevas páginas.
* Defina el derecho de acceso al modo Diseño de los sistemas de párrafos, de modo que solo las personas autorizadas (normalmente el administrador) puedan cambiarlos.
* Defina los componentes permitidos en el sistema de párrafos dado para que los editores puedan colocar los componentes necesarios en la página. En nuestro caso, podría ser un componente de lista, que puede recorrer un subárbol de páginas y extraer la información según reglas predefinidas.
* Los editores añaden y configuran los componentes permitidos, en las páginas de las que son responsables, para entregar la funcionalidad solicitada (información) a la empresa.

Esto ilustra cómo este enfoque permite a los usuarios y administradores contribuyentes del sitio web responder rápidamente a las necesidades comerciales, sin requerir la participación de equipos de desarrollo. Los métodos alternativos, como la creación de una nueva plantilla, suelen ser un ejercicio costoso que requiere un proceso de gestión del cambio y la participación del equipo de desarrollo. Esto hace que todo el proceso sea mucho más largo y costoso.

Por lo tanto, los desarrolladores de sistemas basados en AEM deben utilizar:

* plantillas y control de acceso al diseño del sistema de párrafos para la uniformidad y la protección de la marca
* sistema de párrafos, incluidas sus opciones de configuración para la flexibilidad.

Las siguientes reglas generales para desarrolladores tienen sentido en la mayoría de los proyectos habituales:

* Mantenga bajo el número de plantillas, tan bajo como el número de estructuras de página fundamentalmente diferentes en los sitios web.
* Proporcione la flexibilidad y las capacidades de configuración necesarias a sus componentes personalizados.
* Maximice el uso de la potencia y la flexibilidad de AEM sistema de párrafos: los componentes parsys y iparsys.

### Personalización de componentes y otros elementos {#customizing-components-and-other-elements}

Al crear sus propios componentes o personalizar un componente existente, a menudo es más fácil (y seguro) reutilizar las definiciones existentes. Los mismos principios también se aplican a otros elementos dentro de AEM, por ejemplo el controlador de errores.

Esto se puede hacer copiando y superponiendo la definición existente. En otras palabras, copiar la definición de `/libs` a `/apps/<your-project>`. Esta nueva definición, en `/apps`, se puede actualizar según sus necesidades.

>[!NOTE]
>
>Consulte [Uso de superposiciones](/help/sites-developing/overlays.md) para obtener más información.

Por ejemplo:

* [Personalización de un componente](/help/sites-developing/components.md)

   Esto implicaba superponer una definición de componente:

   * Cree una nueva carpeta de componentes en `/apps/<website-name>/components/<MyComponent>` copiando un componente existente:

      * Por ejemplo, para personalizar la copia del componente Texto :

         * de `/libs/foundation/components/text`
         * hasta `/apps/myProject/components/text`

* [Personalización de las páginas que muestra el Controlador de errores](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   Este caso implica superponer un servlet:

   * En el repositorio, copie los scripts predeterminados:

      * de `/libs/sling/servlet/errorhandler/`
      * hasta `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>You **no debe** cambie cualquier cosa en la variable `/libs` ruta.
>
>Esto se debe a que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y puede sobrescribirse al aplicar una corrección o un paquete de funciones).
>
>Para cambios de configuración y otros cambios:
>
>1. copiar el elemento en `/libs` a `/apps`
>1. realice cualquier cambio dentro de `/apps`


## Cuándo usar consultas JCR y cuándo no utilizarlas {#when-to-use-jcr-queries-and-when-not-to-use-them}

Las consultas JCR son una potente herramienta cuando se utilizan correctamente. Son adecuadas para:

* consultas reales del usuario final, como búsquedas de texto completo en el contenido.
* ocasiones en las que el contenido estructurado debe encontrarse en todo el repositorio.

   En estos casos, asegúrese de que las consultas solo se ejecutan cuando es absolutamente necesario, por ejemplo, en la activación de componentes o la invalidación de caché (a diferencia de, por ejemplo, los pasos de flujos de trabajo, los controladores de eventos que generan déclencheur en las modificaciones de contenido, los filtros, etc.).

Las consultas JCR nunca deben utilizarse para solicitudes de procesamiento puras. Por ejemplo, las consultas JCR no son adecuadas para

* navegación de renderización
* creación de una descripción general de los &quot;primeros 10 artículos de noticias más recientes&quot;
* visualización de recuentos de elementos de contenido

Para procesar contenido, utilice el acceso de navegación al árbol de contenido en lugar de realizar una consulta JCR.

>[!NOTE]
>
>Si usa la variable [Generador de consultas](/help/sites-developing/querybuilder-api.md), se utilizan consultas JCR, ya que el Generador de consultas genera consultas JCR debajo del capó.

## Consideraciones de seguridad {#security-considerations}

>[!NOTE]
>
>También vale la pena hacer referencia al [lista de comprobación de seguridad](/help/sites-administering/security-checklist.md).

### Sesiones de JCR (repositorio) {#jcr-repository-sessions}

Debe utilizar la sesión del usuario, no la sesión administrativa. Esto significa que debe utilizar:

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protect contra scripts en sitios múltiples (XSS) {#protect-against-cross-site-scripting-xss}

La ejecución de scripts en sitios múltiples (XSS) permite a los atacantes insertar código en páginas web vistas por otros usuarios. Esta vulnerabilidad de seguridad puede ser explotada por usuarios web malintencionados para evitar los controles de acceso.

AEM aplica el principio de filtrado de todo el contenido proporcionado por el usuario en la salida. La prevención de XSS tiene la prioridad más alta durante el desarrollo y las pruebas.

Además, un cortafuegos de la aplicación web, como [mod_security para Apache](https://modsecurity.org), puede proporcionar un control central fiable sobre la seguridad del entorno de implementación y protegerse contra ataques de scripts entre sitios no detectados anteriormente.

>[!CAUTION]
>
>El código de ejemplo proporcionado con AEM puede no protegerse de estos ataques y generalmente se basa en el filtrado de solicitudes por parte de un cortafuegos de aplicaciones web.

La hoja de referencia de la API XSS contiene información que debe conocer para utilizar la API XSS y hacer que una aplicación AEM sea más segura. Puede descargarlo aquí:

La hoja de referencia de XSSAPI.

[Obtener archivo](assets/xss_cheat_sheet_2016.pdf)

### Protección de la comunicación para la información confidencial {#securing-communication-for-confidential-information}

En cuanto a cualquier aplicación de Internet, asegúrese de que al transportar información confidencial

* el tráfico está protegido mediante SSL
* Se utiliza el POST HTTP si corresponde

Esto se aplica a la información que es confidencial para el sistema (como la configuración o el acceso administrativo) así como a la información confidencial para sus usuarios (como sus datos personales)

## Tareas de desarrollo distintas {#distinct-development-tasks}

### Personalización de páginas de error {#customizing-error-pages}

Las páginas de error se pueden personalizar para AEM. Esto es aconsejable para que la instancia no muestre los seguimientos de Sling en los errores internos del servidor.

Consulte [Personalización de páginas de error que muestra el Controlador de errores](/help/sites-developing/customizing-errorhandler-pages.md) para obtener más información.

### Abrir archivos en el proceso Java {#open-files-in-the-java-process}

Como AEM puede acceder a un gran número de archivos, se recomienda que el número de [abrir archivos para un proceso Java](/help/sites-deploying/configuring.md#open-files-in-the-java-process) se debe configurar explícitamente para AEM.

Para minimizar este problema, el desarrollo debe garantizar que cualquier archivo abierto se cierre correctamente lo antes posible (de forma significativa).
