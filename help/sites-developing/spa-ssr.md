---
title: SPA y procesamiento del lado del servidor
seo-title: SPA y procesamiento del lado del servidor
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
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPA y procesamiento del lado del servidor{#spa-and-server-side-rendering}

>[!NOTE]
>
>El Editor de SPA es la solución recomendada para proyectos que requieren procesamiento del cliente basado en el marco de SPA (por ejemplo, React o Angular).

>[!NOTE]
>
>Se requiere AEM 6.5.1.0 o posterior para utilizar las funciones de representación del lado del servidor SPA tal como se describe en este documento.

## Información general {#overview}

Las aplicaciones de una sola página (SPA) pueden ofrecer al usuario una experiencia dinámica y enriquecida que reacciona y se comporta de formas conocidas, a menudo como una aplicación nativa. [Esto se consigue confiando en que el cliente cargue el contenido por adelantado y, a continuación, lleve a cabo el trabajo pesado de gestionar la interacción](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) del usuario y, de este modo, se minimiza la cantidad de comunicación necesaria entre el cliente y el servidor, lo que hace que la aplicación sea más reactiva.

Sin embargo, esto puede llevar a tiempos de carga iniciales más largos, especialmente si el SPA es grande y rico en su contenido. Para optimizar los tiempos de carga, parte del contenido se puede representar en el servidor. El uso del procesamiento en el lado del servidor (SSR) puede acelerar la carga inicial de la página y, a continuación, pasar el procesamiento al cliente.

## Cuándo utilizar SSR {#when-to-use-ssr}

No es necesaria la reforma del sector de la seguridad en todos los proyectos. Aunque AEM es totalmente compatible con JS SSR para SPA, Adobe no recomienda implementarlo sistemáticamente en todos los proyectos.

Al decidir implementar SSR, primero debe calcular qué complejidad adicional, esfuerzo y costo de adición de SSR representa de manera realista para el proyecto, incluido el mantenimiento a largo plazo. La arquitectura de SSR sólo debe elegirse cuando el valor añadido exceda claramente los costes estimados.

SSR suele proporcionar algún valor cuando hay un claro &quot;sí&quot; a cualquiera de las siguientes preguntas:

* **** SEO: ¿Es aún necesario realizar la SSR para que los motores de búsqueda que traen tráfico indiquen correctamente el sitio? Tenga en cuenta que los rastreadores de motores de búsqueda principales ahora evalúan JS.
* **** Velocidad de página: ¿Proporciona la SSR una mejora de velocidad medible en los entornos de la vida real y contribuye a la experiencia general del usuario?

Solo cuando al menos una de estas dos preguntas se conteste con un claro &quot;sí&quot; para su proyecto, Adobe recomienda implementar SSR. Las siguientes secciones describen cómo hacerlo con Adobe I/O Runtime.

## Adobe I/O Runtime {#adobe-i-o-runtime}

Si [está seguro de que su proyecto requiere la implementación de SSR](/help/sites-developing/spa-ssr.md#when-to-use-ssr), la solución recomendada de Adobe es utilizar Adobe I/O Runtime.

Para obtener más información sobre Adobe I/O Runtime, consulte

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) : para obtener una descripción general del servicio
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) : para obtener documentación detallada sobre la plataforma

Las siguientes secciones detallan cómo se puede utilizar Adobe I/O Runtime para implementar SSR para su SPA en dos modelos diferentes:

* [Flujo de comunicación dirigido por AEM](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Flujo de comunicación impulsado por el tiempo de ejecución de Adobe I/O](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe recomienda una instancia de Adobe I/O Runtime independiente para cada entorno de AEM (autor, publicación, etapa, etc.).

## Flujo de comunicación dirigido por AEM {#aem-driven-communication-flow}

Al utilizar SSR, el flujo de trabajo [de interacción de](/help/sites-developing/spa-overview.md#workflow) componentes de SPA en AEM incluye una fase en la que el contenido inicial de la aplicación se genera en Adobe I/O Runtime.

1. El navegador solicita el contenido de SSR a AEM.

1. AEM publica el modelo en Adobe I/O Runtime.

1. Adobe I/O Runtime devuelve el contenido generado.

1. AEM proporciona el HTML devuelto por Adobe I/O Runtime a través de la plantilla HTL del componente de página de back-end.

![server-side-renderizacióncms-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Flujo de comunicación impulsado por el tiempo de ejecución de Adobe I/O {#adobe-i-o-runtime-driven-communication-flow}

En la sección anterior se describe la implementación estándar y recomendada del procesamiento del lado del servidor con respecto a los SPA en AEM, donde AEM realiza el arranque y el servicio del contenido.

De forma alternativa, SSR se puede implementar para que Adobe I/O Runtime sea responsable del arranque, con lo que se invierte de forma efectiva el flujo de comunicación.

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
     <li>Solo es necesario mantener los recursos en AEM<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Posiblemente no sea familiar para el desarrollador de SPA<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>mediante Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>Más familiarizado con los desarrolladores de SPA<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Los recursos de la biblioteca de clientes requeridos por la aplicación, como CSS y JavaScript, deberán estar disponibles para el desarrollador de AEM mediante la <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> propiedad<br /> </li>
     <li>Los recursos deben sincronizarse entre AEM y Adobe I/O Runtime<br /> </li>
     <li>Para habilitar la creación de SPA, puede ser necesario un servidor proxy para Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Planificación de SSR {#planning-for-ssr}

Generalmente, solo una parte de una aplicación debe representarse en el servidor. El ejemplo común es que el contenido que se mostrará encima del pliegue en la carga inicial de la página se procesará en el servidor. Esto ahorra tiempo al enviar al cliente contenido ya procesado. A medida que el usuario interactúa con el SPA, el cliente procesa el contenido adicional.

A medida que considere implementar el procesamiento del lado del servidor para su SPA, debe revisar qué partes de la aplicación serán necesarias.

## Desarrollo de un SPA mediante SSR {#developing-an-spa-using-ssr}

Los componentes de SPA pueden ser procesados por el cliente (en el navegador) o por el servidor. Cuando se procesa en el servidor, las propiedades del navegador, como el tamaño y la ubicación de la ventana, no están presentes. Por lo tanto, los componentes de la SPA deben ser isomórficos, sin suponer dónde se representarán.

Para aprovechar SSR, deberá implementar su código en AEM, así como en Adobe I/O Runtime, que es responsable del procesamiento en el servidor. La mayoría del código será el mismo, pero las tareas específicas del servidor diferirán.

## SSR para SPA en AEM {#ssr-for-spas-in-aem}

El SSR para SPA en AEM requiere Adobe I/O Runtime, que se llama para la representación del servidor de contenido de la aplicación. En el HTML de la aplicación, se llama a un recurso en tiempo de ejecución de Adobe I/O para procesar el contenido.

Al igual que AEM admite los marcos de SPA angulares y de reacción predeterminados, el procesamiento en el servidor también es compatible con las aplicaciones Angular y React. Consulte la documentación de NPM para conocer ambos marcos para obtener más detalles.

* Reaccionar: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Angular: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

Para ver un ejemplo simplista, consulte la aplicación [](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)We.Retail Journal. Procesa todo el lado del servidor de aplicaciones. Aunque este no es un ejemplo real, ilustra lo que se necesita para implementar la reforma del sector de la seguridad.

>[!CAUTION]
>
>La aplicación [](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) We.Retail Journal solo sirve para fines de demostración y, por tanto, utiliza Node.js como un ejemplo sencillo en lugar del tiempo de ejecución de Adobe I/O recomendado. Este ejemplo no debe utilizarse para ningún trabajo de proyecto.

>[!NOTE]
>
>Todos los proyectos de SPA en AEM deben basarse en el [arquetipo Maven para el kit](https://github.com/adobe/aem-spa-project-archetype)de inicio de SPA.

## Uso de Node.js {#using-node-js}

Adobe I/O Runtime es la solución recomendada para implementar SSR para SPA en AEM.

En el caso de instancias de AEM in situ, también es posible implementar SSR mediante una instancia de Node.js personalizada de la misma manera que se describe anteriormente. Aunque Adobe lo admite, no se recomienda.

>[!NOTE]
>
>Node.js no es compatible con las instancias de AEM alojadas en Adobe.

>[!NOTE]
>
>Si SSR debe implementarse mediante Node.js, Adobe recomienda una instancia de Node.js independiente para cada entorno de AEM (autor, publicación, etapa, etc.).
