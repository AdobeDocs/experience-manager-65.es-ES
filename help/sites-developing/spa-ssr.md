---
title: Procesamiento en el lado de SPA y servidor
seo-title: Procesamiento en el lado de SPA y servidor
description: nulo
seo-description: nulo
uuid: 27e26e3f-65d4-4069-b570-58b8b9e2a1ae
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 844e5c96-2a18-4869-b4c8-2fb9efe0332a
docset: aem65
translation-type: tm+mt
source-git-commit: 590dc4464182d4baf8293e7bb0774ce92971c0af
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 1%

---


# Representación en SPA y en el servidor{#spa-and-server-side-rendering}

>[!NOTE]
>
>El Editor de SPA es la solución recomendada para proyectos que requieren SPA procesamiento del lado del cliente basado en el marco de trabajo (por ejemplo, React o Angular).

>[!NOTE]
>
>Se necesita AEM 6.5.1.0 o posterior para utilizar las funciones de procesamiento del lado del servidor SPA, tal como se describe en este documento.

## Información general {#overview}

Las aplicaciones de una sola página (SPA) pueden oferta al usuario de una experiencia dinámica y enriquecida que reacciona y se comporta de maneras conocidas, a menudo como una aplicación nativa. [Esto se consigue confiando en que el cliente cargue el contenido por adelantado y, a continuación, realice el trabajo pesado de gestionar la ](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) interacción del usuario y, de este modo, se minimiza la cantidad de comunicación necesaria entre el cliente y el servidor, lo que hace que la aplicación sea más reactiva.

Sin embargo, esto puede llevar a tiempos de carga iniciales más largos, especialmente si el SPA es grande y rico en su contenido. Para optimizar los tiempos de carga, parte del contenido se puede representar en el servidor. El uso del procesamiento en el lado del servidor (SSR) puede acelerar la carga inicial de la página y, a continuación, pasar el procesamiento al cliente.

## Cuándo utilizar SSR {#when-to-use-ssr}

No es necesaria la reforma del sector de la seguridad en todos los proyectos. Si bien AEM apoyar plenamente la SSR de JS para SPA, Adobe no recomienda implementarla sistemáticamente en todos los proyectos.

Al decidir implementar SSR, primero debe calcular qué complejidad adicional, esfuerzo y costo de adición de SSR representa de manera realista para el proyecto, incluido el mantenimiento a largo plazo. La arquitectura de SSR sólo debe elegirse cuando el valor añadido exceda claramente los costes estimados.

SSR suele proporcionar algún valor cuando hay un claro &quot;sí&quot; a cualquiera de las siguientes preguntas:

* **SEO:** ¿Es aún necesario realizar la SSR para que el sitio esté indexado correctamente por los motores de búsqueda que traen tráfico? Tenga en cuenta que los rastreadores de motores de búsqueda principales ahora evalúan JS.
* **Velocidad de la página:** ¿Proporciona la SSR una mejora de velocidad medible en los entornos de la vida real y contribuye a la experiencia del usuario en general?

Sólo cuando al menos una de estas dos preguntas se conteste con un claro &quot;sí&quot; para su proyecto, Adobe recomienda la implementación de SSR. Las siguientes secciones describen cómo hacerlo con Adobe I/O Runtime.

## Adobe I/O Runtime {#adobe-i-o-runtime}

Si [está seguro de que su proyecto requiere la implementación de SSR](/help/sites-developing/spa-ssr.md#when-to-use-ssr), la solución recomendada de Adobe es utilizar Adobe I/O Runtime.

Para obtener más información sobre Adobe I/O Runtime, consulte

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) : para obtener una descripción general del servicio
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) : para obtener documentación detallada sobre la plataforma

Las siguientes secciones detallan cómo se puede utilizar Adobe I/O Runtime para implementar SSR para su SPA en dos modelos diferentes:

* [Flujo de comunicación AEM](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Flujo de comunicación impulsado por Adobe I/O Runtime](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe recomienda una instancia de Adobe I/O Runtime independiente para cada entorno de AEM (autor, publicación, etapa, etc.).

## Configuración del procesador remoto {#remote-renderer-configuration}

AEM saber dónde se puede recuperar el contenido procesado de forma remota. Independientemente del [modelo que elija implementar para SSR,](#adobe-i-o-runtime) deberá especificar para AEM cómo acceder a este servicio de procesamiento remoto.

Esto se realiza mediante el **servicio OSGi de RemoteContentRenderer - Configuration Factory**. Busque la cadena &quot;RemoteContentRenderer&quot; en la consola de configuración de la consola web en `http://<host>:<port>/system/console/configMgr`.

![Configuración del procesador](assets/rendererconfig.png)

Los siguientes campos están disponibles para la configuración:

* **Patrón**  de ruta de contenido: expresión regular para que coincida con una parte del contenido, si es necesario
* **Dirección URL**  del extremo remoto: dirección URL del extremo responsable de la generación del contenido
   * Utilice el protocolo HTTPS seguro si no está en la red local.
* **Encabezados**  de solicitud adicionales: Encabezados adicionales que se agregarán a la solicitud enviada al extremo remoto
   * Patrón: `key=value`
* **Tiempo de espera**  de solicitud: tiempo de espera de solicitud de host remoto en milisegundos

>[!NOTE]
>
>Independientemente de si decide implementar el flujo de comunicación [AEM](#aem-driven-communication-flow) o el flujo [gobernado por Adobe I/O Runtime,](#adobe-i-o-runtime-driven-communication-flow) debe definir una configuración del procesador de contenido remoto.
>
>Esta configuración también debe definirse si elige [utilizar un servidor Node.js personalizado.](#using-node-js)

>[!NOTE]
>
>Esta configuración aprovecha el [procesador de contenido remoto,](#remote-content-renderer), que tiene opciones de personalización y extensión adicionales disponibles.

## Flujo de comunicación impulsado por AEM {#aem-driven-communication-flow}

Al utilizar SSR, el [flujo de trabajo de interacción de componentes](/help/sites-developing/spa-overview.md#workflow) de SPA en AEM incluye una fase en la que el contenido inicial de la aplicación se genera en Adobe I/O Runtime.

1. El explorador solicita el contenido de SSR a AEM.

1. AEM publica el modelo en Adobe I/O Runtime.

1. Adobe I/O Runtime devuelve el contenido generado.

1. AEM proporciona el HTML devuelto por Adobe I/O Runtime a través de la plantilla HTL del componente de página de back-end.

![server-side-procesing-cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Flujo de comunicación impulsado por Adobe I/O Runtime {#adobe-i-o-runtime-driven-communication-flow}

En la sección anterior se describe la implementación estándar y recomendada de la representación del lado del servidor con respecto a la SPA en AEM, donde AEM realiza la inicialización y el servicio del contenido.

Como alternativa, SSR puede implementarse para que Adobe I/O Runtime sea responsable del arranque, revirtiendo efectivamente el flujo de comunicación.

Ambos modelos son válidos y son compatibles con AEM. Sin embargo, hay que tener en cuenta las ventajas y desventajas de cada uno de ellos antes de aplicar un modelo determinado.

<table>
 <tbody>
  <tr>
   <th><strong>Bootstrap</strong></th>
   <th><strong>Ventajas</strong></th>
   <th><strong>Desventajas</strong></th>
  </tr>
  <tr>
   <th><strong>mediante AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM administra las bibliotecas de inyección donde sea necesario</li>
     <li>Sólo es necesario mantener los recursos en AEM<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Quizás no sea familiar para SPA programador<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>a través de Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>Más familiarizado con SPA desarrolladores<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Los recursos de la biblioteca de clientes requeridos por la aplicación, como CSS y JavaScript, deberán estar disponibles para el desarrollador de AEM mediante la propiedad <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code><br /> </li>
     <li>Los recursos deben sincronizarse entre AEM y Adobe I/O Runtime<br /> </li>
     <li>Para habilitar la creación de la SPA, puede ser necesario un servidor proxy para Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Planificación de SSR {#planning-for-ssr}

Generalmente, solo una parte de una aplicación debe representarse en el servidor. El ejemplo común es que el contenido que se mostrará encima del pliegue en la carga inicial de la página se procesará en el servidor. Esto ahorra tiempo al enviar al cliente contenido ya procesado. A medida que el usuario interactúa con el SPA, el cliente procesa el contenido adicional.

A medida que considere la implementación del procesamiento del lado del servidor para su SPA, debe revisar qué partes de la aplicación serán necesarias.

## Desarrollo de un SPA con SSR {#developing-an-spa-using-ssr}

SPA componentes pueden ser procesados por el cliente (en el navegador) o por el servidor. Cuando se procesa en el servidor, las propiedades del navegador, como el tamaño y la ubicación de la ventana, no están presentes. Por lo tanto, SPA componentes deben ser isomórficos, sin dar por sentado dónde se representarán.

Para aprovechar SSR, deberá implementar el código en AEM y en Adobe I/O Runtime, que es responsable del procesamiento en el servidor. La mayoría del código será el mismo, aunque las tareas específicas del servidor diferirán.

## SSR para SPA en AEM {#ssr-for-spas-in-aem}

El SSR para SPA en AEM requiere Adobe I/O Runtime, que se llama para la representación del servidor de contenido de la aplicación. En el HTML de la aplicación, se llama a un recurso de Adobe I/O Runtime para procesar el contenido.

De la misma manera que AEM admite los marcos SPA Angular y Reaccionar de forma predeterminada, el procesamiento del lado del servidor también es compatible con las aplicaciones Angular y Reaccionar. Consulte la documentación de NPM para conocer ambos marcos para obtener más detalles.

* Reaccionar: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Angular: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

Para ver un ejemplo simplista, consulte la aplicación de Historial [We.Retail](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal). Procesa todo el lado del servidor de aplicaciones. Aunque este no es un ejemplo real, ilustra lo que se necesita para implementar la reforma del sector de la seguridad.

>[!CAUTION]
>
>La [aplicación de Historial We.Retail](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) se utiliza únicamente con fines de demostración y, por lo tanto, Node.js es un ejemplo sencillo en lugar del Adobe I/O Runtime recomendado. Este ejemplo no debe utilizarse para ningún trabajo de proyecto.

>[!NOTE]
>
>Cualquier proyecto AEM debe aprovechar el [AEM Arquetipo de proyecto](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype/overview.html), que admite SPA proyectos usando React o Angular y aprovecha el SDK SPA.

## Uso de Node.js {#using-node-js}

Adobe I/O Runtime es la solución recomendada para implementar SSR para SPA en AEM.

En el caso de instancias de AEM in situ, también es posible implementar SSR mediante una instancia de Node.js personalizada de la misma manera que se describe anteriormente. Aunque Adobe lo admite, no se recomienda.

>[!NOTE]
>
>Node.js no es compatible con instancias de AEM alojadas en Adobe.

>[!NOTE]
>
>Si SSR debe implementarse mediante Node.js, Adobe recomienda una instancia de Node.js independiente para cada entorno de AEM (autor, publicación, etapa, etc.).

## Procesador de contenido remoto {#remote-content-renderer}

La [Configuración del procesador de contenido remoto](#remote-content-renderer-configuration) que se requiere para utilizar SSR con su SPA en AEM toca en un servicio de procesamiento más generalizado que se puede ampliar y personalizar para satisfacer sus necesidades.

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` es un servicio OSGi para recuperar contenido procesado en un servidor remoto, como por ejemplo, de Adobe I/O. El contenido enviado al servidor remoto se basa en el parámetro de solicitud pasado.

`RemoteContentRenderingService` se puede insertar mediante la inversión de dependencias en un modelo Sling personalizado o en un servlet cuando se requiera una manipulación de contenido adicional.

Este servicio lo utiliza internamente [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

El `RemoteContentRendererRequestHandlerServlet` se puede utilizar para configurar la solicitud mediante programación. `DefaultRemoteContentRendererRequestHandlerImpl`, la implementación predeterminada del controlador de solicitudes proporcionada, le permite crear varias configuraciones OSGi para asignar una ubicación en la estructura de contenido a un punto final remoto.

Para agregar un controlador de solicitud personalizado, implemente la interfaz `RemoteContentRendererRequestHandler`. Asegúrese de establecer la propiedad del componente `Constants.SERVICE_RANKING` en un entero mayor que 100, que es la clasificación de `DefaultRemoteContentRendererRequestHandlerImpl`.

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

Para que un servlet recupere y devuelva contenido que se puede insertar en la página:

1. Asegúrese de que el servidor remoto sea accesible.
1. Añada uno de los siguientes fragmentos en la plantilla HTL de un componente AEM.
1. Opcionalmente, cree o modifique las configuraciones de OSGi.
1. Explorar el contenido del sitio

Normalmente, la plantilla HTL de un componente de página es el destinatario principal de dicha función.

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Requisitos {#requirements}

Los servlets aprovechan el Sling Model Exporter para serializar los datos del componente. De forma predeterminada, tanto `com.adobe.cq.export.json.ContainerExporter` como `com.adobe.cq.export.json.ComponentExporter` son compatibles como adaptadores del modelo Sling. Si es necesario, puede agregar clases que la solicitud debe adaptarse para utilizar `RemoteContentRendererServlet` e implementar el `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. Las clases adicionales deben ampliar el `ComponentExporter`.
