---
title: Cómo hacer un lanzamiento con su aplicación sin encabezado
description: AEM En esta parte del Recorrido para desarrolladores sin encabezado de, aprenda a implementar una aplicación sin encabezado en directo.
exl-id: ec3356ef-9e60-4151-984d-3ebdab593b96
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1903'
ht-degree: 54%

---

# Cómo hacer un lanzamiento con su aplicación sin encabezado {#go-live}

En esta parte del [AEM Recorrido de desarrollador sin encabezado](overview.md), aprenda a implementar una aplicación sin encabezado en directo.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de AEM sin encabezado, [Cómo actualizar su contenido a través de las API de AEM Asset](update-your-content.md) ha aprendido a actualizar el contenido sin encabezado existente en AEM mediante la API y ahora debería:

* Comprender la API HTTP de AEM Asset.

Este artículo se basa en estos fundamentos para que entienda cómo preparar su propio proyecto de AEM sin encabezado para su lanzamiento.

## Objetivo {#objective}

AEM Este documento le ayuda a comprender la canalización de publicaciones sin encabezado y las consideraciones de rendimiento que debe tener en cuenta antes de publicar en su aplicación.

* AEM Obtenga información acerca del SDK de la y las herramientas de desarrollo necesarias
* Configure un tiempo de ejecución de desarrollo local para simular el contenido antes de publicarlo
* AEM Comprender los conceptos básicos de almacenamiento en caché y replicación de contenido
* Asegurar y escalar su aplicación antes del lanzamiento
* Monitorizar los problemas de rendimiento y depuración

## El SDK de AEM {#the-aem-sdk}

El SDK de AEM se utiliza para crear e implementar código personalizado. Es la principal herramienta que necesita para desarrollar y probar su aplicación sin encabezado antes de lanzarla. Contiene los siguientes artefactos:

* Jar de inicio rápido: un archivo Jar ejecutable que se puede utilizar para configurar una instancia de autor y de publicación
* Herramientas de Dispatcher: el módulo de Dispatcher y sus dependencias para sistemas basados en Windows y UNIX
* AEM Jar de API de Java: la dependencia de Jar de Java/Maven que expone todas las API de Java permitidas que se pueden utilizar para desarrollar contra el uso de la
* Javadoc jar: Javadocs para el jar de la API de Java

## Herramientas de desarrollo adicionales {#additional-development-tools}

AEM Además del SDK de la, necesitará herramientas adicionales que faciliten el desarrollo y la prueba del código y el contenido de forma local:

* Java
* Git
* Apache Maven
* La biblioteca Node.js
* El IDE de su elección

AEM AEM Dado que es una aplicación Java, debe instalar Java y el SDK de Java para admitir el desarrollo de la aplicación as a Cloud Service de.

Git es lo que utilizará para administrar el control de código fuente, así como para proteger los cambios en Cloud Manager e implementarlos en una instancia de producción.

AEM AEM Utiliza Apache Maven para crear proyectos generados a partir del tipo de archivo del proyecto de Maven de la. Todos los IDE principales proporcionan compatibilidad con la integración de Maven.

Node.js es un entorno de tiempo de ejecución de JavaScript que se utiliza para trabajar con los recursos front-end de un subproyecto `ui.frontend` del proyecto de AEM. Node.js se distribuye con npm, que es el administrador de paquetes de facto de Node.js, que se utiliza para administrar las dependencias de JavaScript.

## Generalidades de los componentes del sistema AEM {#components-of-an-aem-system-at-a-glance}

AEM A continuación, echemos un vistazo a las partes constitutivas de un entorno de la.

Un entorno de AEM completo está formado por un Autor, una Publicación y un Dispatcher. Estos mismos componentes estarán disponibles en el tiempo de ejecución de desarrollo local para que sea más fácil obtener una vista previa del código y el contenido antes de publicarlos.

* **El servicio de creación** es donde los usuarios internos crean, administran y previsualizan contenido.

* **El servicio de publicación** se considera el entorno “activo” y suele ser con el que interactúan los usuarios finales. El contenido, después de editarse y aprobarse en el servicio de creación, se distribuye (replica) al de publicación. El patrón de implementación más común con las aplicaciones sin encabezado de AEM es tener la versión de producción de la aplicación conectada a un servicio de publicación de AEM.

* **Dispatcher** es un servidor web estático ampliado con el módulo Dispatcher de AEM. Almacena en la caché las páginas web producidas por la instancia de publicación para mejorar el rendimiento.

## Flujo de trabajo de desarrollo local {#the-local-development-workflow}

El proyecto de desarrollo local se basa en Apache Maven y utiliza Git para el control de código fuente. Para actualizar el proyecto, los desarrolladores pueden utilizar su entorno de desarrollo integrado preferido, como Eclipse, Visual Studio Code o IntelliJ, entre otros.

AEM AEM Para probar las actualizaciones de código o contenido que la aplicación sin encabezado va a introducir, debe implementar las actualizaciones en el tiempo de ejecución de la aplicación local, que incluye instancias locales de los servicios de autor y publicación de la.

Asegúrese de tomar nota de las distinciones entre cada componente en el tiempo de ejecución de AEM local, ya que es vital probar las actualizaciones allí donde sean más importantes. Por ejemplo, pruebe las actualizaciones de contenido en la instancia de autor o pruebe el nuevo código en la instancia de publicación.

AEM En un sistema de producción, un Dispatcher y un servidor HTTP Apache siempre se sientan delante de una instancia de publicación de la. AEM Proporcionan servicios de almacenamiento en caché y seguridad para el sistema de, por lo que es fundamental probar también las actualizaciones de código y contenido con Dispatcher.

## Vista previa del código y el contenido localmente con el entorno de desarrollo local {#previewing-your-code-and-content-locally-with-the-local-development-environment}

AEM Para preparar el proyecto sin encabezado de la para su lanzamiento, debe asegurarse de que todas las partes constitutivas del proyecto funcionen correctamente.

Para ello, debe reunir todo: código, contenido y configuración y probarlos en un entorno de desarrollo local para la preparación para el lanzamiento.

El entorno de desarrollo local consta de tres esferas principales:

1. AEM AEM El proyecto de: contendrá todo el código, la configuración y el contenido personalizados en los que trabajarán los desarrolladores de la
1. AEM AEM AEM Tiempo de ejecución de la local: versiones locales de los servicios de autor y publicación de la aplicación que se utilizarán para implementar código desde el proyecto de la
1. Tiempo de ejecución de Dispatcher local: una versión local del HTTPD del servidor web Apache que incluye el módulo de Dispatcher.

Una vez configurado el entorno de desarrollo local, puede simular el contenido que sirve en la aplicación React mediante la implementación local de un servidor de nodo estático.

Para obtener una vista más detallada de la configuración de un entorno de desarrollo local y de todas las dependencias necesarias para la vista previa del contenido, consulte [Documentación de implementación de producción](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites).

## AEM Preparación de la aplicación sin encabezado de la aplicación para el lanzamiento {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

AEM Ahora es el momento de preparar su aplicación sin encabezado para el lanzamiento, siguiendo las prácticas recomendadas que se describen a continuación.

### Proteja su aplicación sin encabezado antes del lanzamiento {#secure-and-scale-before-launch}

1. Preparar [Autenticación](/help/assets/content-fragments/graphql-authentication-content-fragments.md) para sus solicitudes de GraphQL

### Estructura del modelo frente al output de GraphQL {#structure-vs-output}

* Evite crear consultas que produzcan más de 15 kb de JSON (gzip comprimido). Los archivos JSON largos consumen muchos recursos para que la aplicación cliente los analice.
* Evite más de cinco niveles anidados de jerarquías de fragmento. Los niveles adicionales hacen que a los autores de contenido les resulte difícil considerar el impacto de sus cambios.
* Utilice consultas de varios objetos en lugar de modelar consultas con jerarquías de dependencia dentro de los modelos. Esto permite una mayor flexibilidad a largo plazo para reestructurar el output de JSON sin tener que hacer muchos cambios de contenido.

### Maximizar la proporción de visitas en caché de CDN {#maximize-cdn}

* No utilice consultas directas de GraphQL, a menos que solicite contenido activo desde la superficie.
   * Utilice consultas persistentes siempre que sea posible.
   * Proporcione el tiempo de duración (TTL) de la red de distribución de contenido (CDN) por encima de 600 segundos para que la CDN los almacene en la caché.
   * AEM calcula el impacto de un cambio de modelo en las consultas existentes.
* Divida los archivos JSON o consultas GraphQL entre tasas de cambio de contenido bajas y altas para reducir el tráfico de clientes a la CDN y asignar un TTL más alto. Esto minimiza la CDN que vuelve a validar el JSON con el servidor de origen.
* Para invalidar activamente el contenido de la CDN, utilice la depuración leve. Esto permite a la CDN volver a descargar el contenido sin provocar una pérdida de caché.

>[!NOTE]
>
>Consulte [Recursos adicionales](#additional-resources) para obtener más información sobre CDN y almacenamiento en caché.

### Mejora del tiempo para descargar contenido sin encabezado {#improve-download-time}

* Asegúrese de que los clientes HTTP utilicen HTTP/2.
* Asegúrese de que los clientes HTTP acepten la solicitud de encabezados para gzip.
* Minimice el número de dominios utilizados para alojar el formato JSON y los artefactos de referencia.
* Utilice `Last-modified-since` para actualizar los recursos.
* Use la salida `_reference` en el archivo JSON para iniciar la descarga de los recursos sin tener que analizar los archivos JSON completos.

<!-- End of CDN Review -->

## Implementación de la producción {#deploy-to-production}

La implementación en producción puede depender de si tiene un *tradicional* AEM Instancia de que se implementa mediante Maven o que se encuentra en Adobe Managed Services (AMS) y, por lo tanto, utiliza Cloud Manager.

## Implementación en producción mediante Maven {#deploy-to-production-maven}

Para un *tradicional* implementación (que no es AMS) con Maven puede ver las [Tutorial de WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=en#build) para obtener una descripción general.

## Implementar en producción mediante Cloud Manager {#deploy-to-production-cloud-manager}

Si es cliente de AMS que utiliza Cloud Manager, una vez que se haya asegurado de que todo se ha probado y funciona correctamente, estará listo para insertar las actualizaciones de código en un [repositorio Git centralizado en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=es).

Una vez cargadas las actualizaciones en Cloud Manager, se pueden implementar en AEM mediante la [canalización CI/CD de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=es).

<!-- Can't find a parallel link -->
<!--
You can start deploying your code by leveraging the Cloud Manager CI/CD pipeline, which is covered extensively [here](/help/implementing/deploying/overview.md).
-->

## Monitorización del rendimiento {#performance-monitoring}

AEM Para que los usuarios tengan la mejor experiencia posible al utilizar la aplicación sin encabezado de, es importante que supervise las métricas de rendimiento clave, como se detalla a continuación:

* Valide las versiones de producción y previsualización de la aplicación.
* Verifique las páginas de estado de AEM para el estado actual de disponibilidad del servicio.
* Acceda a los informes de rendimiento.
   * Rendimiento de entrega
      * Servidores de origen: número de llamadas, tasas de error, cargas de CPU, tráfico de carga útil
   * Rendimiento del autor
      * Comprobar el número de usuarios, solicitudes y cargas
* Acceso a informes de rendimiento específicos de la aplicación y el espacio
   * Una vez que el servidor esté activo, compruebe si las métricas generales son verdes, naranjas o rojas y, a continuación, identifique los problemas específicos de la aplicación.
   * Abra los mismos informes filtrados anteriormente en la aplicación o el espacio (por ejemplo, escritorio de Photoshop, muro de pago).
   * Utilice las API de registro de Splunk para acceder al rendimiento del servicio y de la aplicación.
   * Póngase en contacto con asistencia al cliente en caso de que surjan otros problemas.

## Solución de problemas {#troubleshooting}

### Depuración {#debugging}

Siga estas prácticas recomendadas como enfoque general de la depuración:

* Valide la funcionalidad y el rendimiento con la versión previa de la aplicación.
* Valide la funcionalidad y el rendimiento con la versión de producción de la aplicación.
* Valide con la vista previa JSON del Editor de fragmentos de contenido.
* Examine el JSON en la aplicación cliente para comprobar si existen problemas en la aplicación cliente o en la entrega.
* Examine el JSON mediante GraphQL para comprobar si existen problemas relacionados con el contenido en caché o AEM.

### Registro de un error con asistencia {#logging-a-bug-with-support}

Para registrar de forma eficaz un error con el servicio de asistencia en caso de que necesite más ayuda, siga estos pasos:

* Tome capturas de pantalla del problema, si es necesario.
* Documente una manera de reproducir el problema.
* Documente el contenido con el que se reproduce el problema.
* Registre un problema a través del portal de asistencia de AEM con la prioridad adecuada.

## El recorrido ha terminado, ¿o no? {#journey-ends}

Felicitaciones. Ha completado el recorrido para desarrolladores de AEM sin encabezado. Ahora debe comprender lo siguiente:

* La diferencia entre la entrega de contenido sin encabezado y con encabezado.
* Las características sin encabezado de AEM.
* Cómo organizar un proyecto sin encabezado en AEM.
* Cómo crear contenido sin encabezado en AEM.
* Cómo recuperar y actualizar contenido sin encabezado en AEM.
* Cómo poner en marcha un proyecto de AEM sin encabezado.
* Qué hacer después del lanzamiento.

Ya ha iniciado su primer proyecto de AEM sin encabezado o ahora tiene los conocimientos necesarios para hacerlo. Buen trabajo.

### Explorar aplicaciones de una sola página {#explore-spa}

Sin embargo, las tiendas sin encabezado de AEM no tienen que detenerse aquí. Quizás recuerde en el [Introducción como parte del recorrido](getting-started.md#integration-levels) AEM hemos discutido brevemente cómo el sistema no solo admite la entrega sin encabezado y los modelos tradicionales full-stack, sino que también puede admitir modelos híbridos que combinen las ventajas de ambos.

Si este es el tipo de flexibilidad que necesita para su proyecto, continúe con la parte opcional adicional del recorrido, [Cómo crear aplicaciones de una sola página (SPA) con AEM.](create-spa.md)

## Recursos adicionales {#additional-resources}

* [AEM Guía de desarrollo de](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/the-basics.html?lang=en)

* [Tutorial de WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)

* [AEM Cloud Manager para](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=en)

* Caché de CDN

   * [Control de una caché de CDN](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#controlling-a-cdn-cache)

   * Configuración de la [Reescritura CDN](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html) (*buscar reescritura de CDN*)
