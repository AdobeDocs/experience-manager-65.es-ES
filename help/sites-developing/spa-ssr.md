---
title: SPA Procesamiento del lado del servidor y de
seo-title: SPA and Server-Side Rendering
description: SPA "Procesamiento del lado del servidor y de la"
seo-description: null
uuid: 27e26e3f-65d4-4069-b570-58b8b9e2a1ae
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 844e5c96-2a18-4869-b4c8-2fb9efe0332a
docset: aem65
exl-id: a80bc883-e0f6-4714-bd28-108262f96d77
source-git-commit: 1ee82589ca9284a8ad5ecf3ca156fe10f314846a
workflow-type: tm+mt
source-wordcount: '1754'
ht-degree: 2%

---

# SPA Procesamiento del lado del servidor y de{#spa-and-server-side-rendering}

>[!NOTE]
>
>SPA SPA El editor de segmentos es la solución recomendada para los proyectos que requieren un procesamiento basado en el marco de trabajo del cliente basado en el marco de trabajo de la aplicación (por ejemplo, React o Angular).

>[!NOTE]
>
>AEM SPA Se requiere la versión 6.5.1.0 o posterior para utilizar las funciones de renderización del lado del servidor de como se describe en este documento.

## Información general {#overview}

SPA Las aplicaciones de una sola página () pueden ofrecer al usuario una experiencia enriquecida y dinámica que reacciona y se comporta de formas familiares, a menudo igual que una aplicación nativa. [Esto se logra confiando en que el cliente cargue el contenido por adelantado y luego haga el trabajo pesado de manejar la interacción del usuario](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) y, por lo tanto, minimiza la cantidad de comunicación necesaria entre el cliente y el servidor, lo que hace que la aplicación sea más reactiva.

SPA Sin embargo, esto puede conllevar tiempos de carga inicial más largos, especialmente si el contenido del es grande y rico. Para optimizar los tiempos de carga, parte del contenido se puede procesar en el servidor. El uso del procesamiento del lado del servidor (SSR) puede acelerar la carga inicial de la página y, a continuación, pasar más procesamiento al cliente.

## Cuándo usar SSR {#when-to-use-ssr}

No se requiere SSR en todos los proyectos. AEM SPA Aunque admite totalmente la SR de JS para la, Adobe no recomienda implementarla sistemáticamente en todos los proyectos.

Al decidir implementar SSR primero debe estimar qué complejidad adicional, esfuerzo y costo adicional representa SSR de manera realista para el proyecto, incluido el mantenimiento a largo plazo. Sólo debe elegirse una arquitectura SSR cuando el valor añadido supere claramente los costes estimados.

SSR generalmente proporciona algún valor cuando hay un claro &quot;sí&quot; a cualquiera de las siguientes preguntas:

* **SEO:** ¿Se sigue necesitando SSR para que los motores de búsqueda que generan tráfico indexen correctamente su sitio? Tenga en cuenta que los rastreadores del motor de búsqueda principal ahora evalúan JS.
* **Velocidad de página:** ¿Proporciona la SSR una mejora de velocidad mensurable en entornos de la vida real y aumenta la experiencia general del usuario?

Solo cuando al menos una de estas dos preguntas se responda con un claro &quot;sí&quot; para su proyecto, el Adobe recomienda implementar SSR. En las secciones siguientes se describe cómo hacerlo con Adobe I/O Runtime.

## Adobe I/O Runtime {#adobe-i-o-runtime}

Si usted [está seguro de que su proyecto requiere la implementación de la SSR](/help/sites-developing/spa-ssr.md#when-to-use-ssr), la solución recomendada por Adobe es utilizar Adobe I/O Runtime.

Para obtener más información sobre Adobe I/O Runtime, consulte

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) - para obtener una descripción general del servicio
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) - para obtener documentación detallada sobre la plataforma

Las siguientes secciones detallan cómo se puede utilizar Adobe I/O Runtime SPA para implementar SSR para su en dos modelos diferentes:

* [AEM Flujo de comunicación impulsado por el](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Flujo de comunicación impulsado por Adobe I/O Runtime](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe recomienda un espacio de trabajo de Adobe I/O Runtime independiente por entorno (ensayo, producción, prueba, etc.). Esto permite patrones típicos del ciclo de vida de desarrollo de sistemas (SDLC) con diferentes versiones de una sola aplicación implementada en diferentes entornos. Ver el documento [CI/CD para el proyecto Firefly Applications](https://www.adobe.io/apis/experienceplatform/project-firefly/docs.html#!AdobeDocs/project-firefly/master/guides/ci_cd_for_firefly_apps.md) para obtener más información.
>
>No se necesita un espacio de trabajo independiente por instancia (autor, publicación) a menos que haya diferencias en la implementación de tiempo de ejecución por tipo de instancia.

## Configuración del procesador remoto {#remote-renderer-configuration}

AEM Debe saber dónde se puede recuperar el contenido procesado de forma remota. Independientemente de [qué modelo decide implementar para SSR,](#adobe-i-o-runtime) AEM deberá especificar cómo acceder a este servicio de procesamiento remoto para obtener acceso a los datos de la aplicación.

Esto se realiza mediante la variable **RemoteContentRenderer: servicio OSGi de fábrica de configuración**. Busque la cadena &quot;RemoteContentRenderer&quot; en la consola de configuración de la consola web en `http://<host>:<port>/system/console/configMgr`.

![Configuración del procesador](assets/rendererconfig.png)

Los campos siguientes están disponibles para la configuración:

* **Patrón de ruta de contenido** - Expresión regular para que coincida con una parte del contenido, si es necesario
* **URL de extremo remoto** : URL del punto de conexión responsable de la generación del contenido
   * Utilice el protocolo HTTPS protegido si no está en la red local.
* **Encabezados de solicitud adicionales** - Encabezados adicionales que se añadirán a la solicitud enviada al extremo remoto
   * Patrón: `key=value`
* **Tiempo de espera de solicitud** - Tiempo de espera de solicitud de host remoto en milisegundos

>[!NOTE]
>
>Independientemente de si decide implementar el [AEM Flujo de comunicación impulsado por el](#aem-driven-communication-flow) o el [Flujo impulsado por Adobe I/O Runtime,](#adobe-i-o-runtime-driven-communication-flow) debe definir una configuración de procesador de contenido remoto.
>
>Esta configuración también debe definirse si elige [utilice un servidor Node.js personalizado.](#using-node-js)

>[!NOTE]
>
>Esta configuración aprovecha las [Procesador de contenido remoto,](#remote-content-renderer) que tiene opciones de extensión y personalización adicionales disponibles.

## AEM Flujo de comunicación impulsado por el {#aem-driven-communication-flow}

Cuando se utiliza SSR, la variable [flujo de trabajo de interacción](/help/sites-developing/spa-overview.md#workflow) SPA AEM de la en la que se incluye una fase en la que el contenido inicial de la aplicación se genera en Adobe I/O Runtime.

1. AEM El explorador solicita el contenido SSR a los usuarios de la interfaz de usuario de.

1. AEM Publica el modelo en Adobe I/O Runtime.

1. Adobe I/O Runtime devuelve el contenido generado.

1. AEM sirve al HTML devuelto por Adobe I/O Runtime a través de la plantilla HTL del componente de página back-end.

![server-side-rendering-cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Flujo de comunicación impulsado por Adobe I/O Runtime {#adobe-i-o-runtime-driven-communication-flow}

SPA AEM AEM En la sección anterior se describe la implementación estándar y recomendada del procesamiento en el servidor con respecto a la en la que el usuario realiza el arranque y la entrega de contenido en el lado del servidor, en el que el usuario realiza el procesamiento de manera predeterminada y de manera predeterminada, en el lado del servidor, en lo que respecta a la en la que se realiza el procesamiento y la entrega de contenido.

Como alternativa, SSR se puede implementar de modo que Adobe I/O Runtime sea responsable del arranque, lo que invierte de forma eficaz el flujo de comunicación.

AEM Ambos modelos son válidos y compatibles con el servicio de asistencia de la aplicación de la. Sin embargo, se deben considerar las ventajas y desventajas de cada uno antes de implementar un modelo en particular.

<table>
 <tbody>
  <tr>
   <th><strong>Bootstrapping</strong></th>
   <th><strong>Ventajas</strong></th>
   <th><strong>Desventajas</strong></th>
  </tr>
  <tr>
   <th><strong>AEM vía de la</strong><br /> </th>
   <td>
    <ul>
     <li>AEM administra la inyección de bibliotecas donde sea necesario</li>
     <li>AEM Solo es necesario mantener los recursos en el área de la<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>SPA Posiblemente desconocido para el desarrollador de<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>mediante Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>SPA Más familiar para los desarrolladores de<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>AEM Los recursos de Clientlib requeridos por la aplicación, como CSS y JavaScript, los deberá poner a disposición el desarrollador de la aplicación a través de la interfaz de usuario de la biblioteca de cliente de la aplicación de desarrollador de. <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> propiedad<br /> </li>
     <li>AEM Los recursos deben sincronizarse entre la aplicación y la aplicación de Adobe I/O Runtime<br /> </li>
     <li>SPA Para habilitar la creación de la, puede ser necesario un servidor proxy para Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Planificación de la SSR {#planning-for-ssr}

Por lo general, solo parte de una aplicación debe procesarse en el servidor. El ejemplo común es el contenido que se muestra encima del pliegue en la carga inicial de la página y que se procesa en el servidor. Esto ahorra tiempo al enviar al cliente contenido ya procesado. SPA A medida que el usuario interactúa con el usuario, el cliente procesa el contenido adicional.

SPA A medida que considere la posibilidad de implementar el procesamiento en el servidor para su, deberá revisar qué partes de la aplicación serán necesarias.

## SPA Desarrollo de una mediante SSR {#developing-an-spa-using-ssr}

SPA El cliente (en el explorador) o el servidor pueden procesar los componentes de la. Cuando se representan en el servidor, las propiedades del explorador como el tamaño y la ubicación de la ventana no están presentes. SPA Por lo tanto, los componentes de la deben ser isomórficos, sin dar por hecho dónde se procesarán.

AEM Para aprovechar la SSR, deberá implementar su código tanto en el servidor como en el Adobe I/O Runtime, que es responsable del procesamiento del lado del servidor. La mayoría del código será el mismo, aunque las tareas específicas del servidor diferirán.

## SPA AEM SSR para la en el {#ssr-for-spas-in-aem}

SPA AEM SSR para la en la práctica requiere Adobe I/O Runtime, que es necesario para el procesamiento del lado del servidor de contenido de la aplicación. Dentro del HTL de la aplicación, se llama a un recurso en Adobe I/O Runtime para procesar el contenido.

AEM Del mismo modo que admite los módulos Angular SPA y React de forma predeterminada, el procesamiento en el servidor también es compatible con las aplicaciones de Angular y React. Consulte la documentación de NPM para ambos marcos para obtener más información.

* Reaccionar: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Angular: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

Para ver un ejemplo simplista, consulte la [Aplicación de diario We.Retail](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal). Procesa todo el servidor de aplicaciones. Aunque este no es un ejemplo real, ilustra lo que se necesita para implementar la SSR.

>[!CAUTION]
>
>El [Aplicación de diario We.Retail](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) es solo para fines de demostración y, por lo tanto, utiliza Node.js como un ejemplo sencillo en lugar del Adobe I/O Runtime recomendado. Este ejemplo no debe utilizarse para ningún trabajo de proyecto.

>[!NOTE]
>
>Cualquier proyecto AEM debería aprovechar el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es), que admite proyectos de SPA que utilizan React o Angular y aprovecha el SDK de SPA.

## Uso de Node.js {#using-node-js}

Adobe I/O Runtime SPA AEM es la solución recomendada para implementar SSR para el uso de la en los entornos de trabajo de la.

AEM En el caso de instancias de locales, también es posible implementar SSR mediante una instancia personalizada de Node.js del mismo modo que se ha descrito anteriormente. Aunque esto es compatible con el Adobe, no se recomienda.

>[!NOTE]
>
>Node.js no es compatible con instancias de alojadas en el Adobe AEM.

>[!NOTE]
>
>Si el SSR debe implementarse mediante Node.js, Adobe AEM recomienda una instancia de Node.js independiente para cada entorno de (autor, publicación, fase, etc.).

## Procesador de contenido remoto {#remote-content-renderer}

El [Configuración del procesador de contenido remoto](#remote-content-renderer-configuration) SPA AEM que es necesario para utilizar SSR con sus en la práctica, utiliza un servicio de renderización más generalizado que se puede ampliar y personalizar para satisfacer sus necesidades.

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` es un servicio OSGi para recuperar contenido procesado en un servidor remoto, como desde el Adobe I/O. El contenido enviado al servidor remoto se basa en el parámetro de solicitud pasado.

`RemoteContentRenderingService` se puede insertar mediante la inversión de dependencia en un modelo Sling personalizado o servlet cuando se requiere una manipulación de contenido adicional.

Este servicio lo utiliza internamente el [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

El `RemoteContentRendererRequestHandlerServlet` se puede utilizar para establecer mediante programación la configuración de la solicitud. `DefaultRemoteContentRendererRequestHandlerImpl`, la implementación del controlador de solicitudes predeterminada proporcionada, le permite crear varias configuraciones de OSGi para asignar una ubicación en la estructura de contenido a un extremo remoto.

Para agregar un controlador de solicitud personalizado, implemente la variable `RemoteContentRendererRequestHandler` interfaz. Asegúrese de configurar el `Constants.SERVICE_RANKING` propiedad de componente a un entero superior a 100, que es la clasificación del `DefaultRemoteContentRendererRequestHandlerImpl`.

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### Configurar la configuración OSGi del controlador predeterminado {#configure-default-handler}

La configuración del controlador predeterminado debe configurarse como se describe en la sección [Configuración del procesador de contenido remoto](#remote-content-renderer-configuration).

### Uso del procesador de contenido remoto {#usage}

Para que un servlet recupere y devuelva contenido que se pueda insertar en la página:

1. Asegúrese de que el servidor remoto sea accesible.
1. AEM Agregue uno de los siguientes fragmentos de código a la plantilla HTL de un componente de la.
1. Opcionalmente, puede crear o modificar las configuraciones de OSGi.
1. Explorar el contenido del sitio

Normalmente, la plantilla HTL de un componente de página es el destinatario principal de una función de este tipo.

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Requisitos  {#requirements}

Los servlets aprovechan el exportador de modelos Sling para serializar los datos del componente. De forma predeterminada, tanto la variable `com.adobe.cq.export.json.ContainerExporter` y `com.adobe.cq.export.json.ComponentExporter` se admiten como adaptadores del modelo Sling. Si es necesario, puede agregar clases a las que se debe adaptar la solicitud utilizando `RemoteContentRendererServlet` y la implementación de `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. Las clases adicionales deben ampliar el `ComponentExporter`.
