---
title: proxy del servicio de formularios HTML5
seo-title: proxy del servicio de formularios HTML5
description: El proxy de servicio de formularios HTML5 es una configuración para registrar un proxy para el servicio de envío. Para configurar el proxy de servicio, especifique la URL del servicio de envío mediante el parámetro de solicitud submitServiceProxy.
seo-description: El proxy de servicio de formularios HTML5 es una configuración para registrar un proxy para el servicio de envío. Para configurar el proxy de servicio, especifique la URL del servicio de envío mediante el parámetro de solicitud submitServiceProxy.
uuid: 42d6c1da-3945-469d-b429-c33e563ed70c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 081f7c17-4e5d-4c7e-a5c3-5541a29b9d55
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 1%

---


# proxy de servicio de formularios HTML5{#html-forms-service-proxy}

El proxy de servicio de formularios HTML5 es una configuración para registrar un proxy para el servicio de envío. Para configurar el proxy de servicio, especifique la URL del servicio de envío mediante el parámetro de solicitud *submitServiceProxy*.

## Ventajas del proxy de servicio {#benefits-of-service-proxy-br}

El proxy de servicio elimina lo siguiente:

* El flujo de trabajo de formularios HTML5 requiere la apertura del servicio de envío &quot;/content/xfaforms/submit/default&quot; para los usuarios de formularios HTML5. Expone AEM servidores a una audiencia no deseada más amplia.
* La URL del servicio está incrustada en el modelo de tiempo de ejecución del formulario. No es posible cambiar la ruta de la URL del servicio.
* El envío es un proceso de dos pasos. Para enviar los datos del formulario, el envío requiere al menos dos recorridos para el servidor. Por lo tanto, aumenta la carga en el servidor.
* Los formularios HTML5 envían datos en la solicitud del POST en lugar de en la solicitud PDF. Para los flujos de trabajo que implican formularios PDF y HTML5, se requieren dos métodos diferentes de procesamiento de los envíos.

### Topologías {#topologies-br}

Los formularios HTML5 pueden utilizar las siguientes topologías para conectarse a los servidores de AEM.

* Topología en la que los formularios AEM Server o HTML5 envían datos mediante POST al servidor.
* Topología en la que el servidor proxy envía datos de POST al servidor.

![topologías de proxy del servicio de formularios HTML5](assets/topology.png)

topologías de proxy del servicio de formularios HTML5

Los formularios HTML5 se conectan a los servidores de AEM para ejecutar secuencias de comandos, servicios web y envíos del lado del servidor. El tiempo de ejecución XFA de los formularios HTML5 utiliza llamadas Ajax en el punto final &quot;/bin/xfaforms/submitaction&quot; con varios parámetros para conectarse a los servidores AEM. Los formularios HTML5 se conectan AEM servidores para realizar las siguientes operaciones:

#### Ejecutar scripts y servicios web del lado del servidor {#execute-server-sided-scripts-and-web-services}

Las secuencias de comandos marcadas para ejecutarse en el servidor se conocen como secuencias de comandos del lado del servidor. En la tabla siguiente se enumeran todos los parámetros utilizados en secuencias de comandos del lado del servidor y Web Services.

<table>
 <tbody>
  <tr>
   <td><p><strong>Parámetro</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p>activity</p> </td>
   <td><p>Activity contiene los eventos que configuran el déclencheur de la solicitud. Como clic, salida o cambio</p> </td>
  </tr>
  <tr>
   <td><p>contextSom</p> </td>
   <td><p>contextSom contiene la expresión SOM del objeto donde se ejecutan los eventos.</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>Plantilla contiene la plantilla utilizada para procesar el formulario.</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>contentRoot contiene el directorio raíz de la plantilla utilizado para procesar el formulario.</p> </td>
  </tr>
  <tr>
   <td><p>Datos</p> </td>
   <td><p>Los datos contienen bytes de datos utilizados para procesar el formulario.</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>formDom contiene DOM del formulario HTML5 en formato JSON.</p> </td>
  </tr>
  <tr>
   <td><p>packet</p> </td>
   <td><p>se especifica como formulario.</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>debugDir contiene el directorio de depuración utilizado para procesar el formulario.</p> </td>
  </tr>
 </tbody>
</table>

#### Enviar datos {#submit-data}

Al hacer clic en el botón de envío, los formularios HTML5 envían datos al servidor. En la tabla siguiente se enumeran todos los parámetros que los formularios HTML5 envían al servidor.

<table>
 <tbody>
  <tr>
   <td><p><strong>Parámetro</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>Plantilla utilizada para procesar el formulario.</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>directorio raíz de plantilla que se utiliza para procesar el formulario.</p> </td>
  </tr>
  <tr>
   <td><p>Datos</p> </td>
   <td><p>bytes de datos utilizados para procesar el formulario.</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>DOM del formulario HTML5 en formato JSON.</p> </td>
  </tr>
  <tr>
   <td><p>submiturl</p> </td>
   <td><p>Dirección URL donde se publican los datos XML.</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>El directorio de depuración utilizado para procesar el formulario.</p> </td>
  </tr>
 </tbody>
</table>

#### ¿Cómo funciona el proxy de envío? {#how-nbsp-the-nbsp-submit-proxy-works}

El proxy del servicio de envío actúa como un paso a través si el envío no está presente en el parámetro de solicitud. Actúa como una transmisión. Envía la solicitud al punto final /bin/xfaforms/submitaction y envía la respuesta al tiempo de ejecución de XFA.

El proxy del servicio de envío selecciona una topología si el envío está presente en el parámetro de solicitud.

* Si AEM servidores publican los datos, el servicio proxy actúa como un paso a través. Envía la solicitud al punto final /bin/xfaforms/submitaction y envía la respuesta al tiempo de ejecución de XFA.
* Si el proxy publica los datos, el servicio proxy pasa todos los parámetros excepto submitUrl al punto final */bin/xfaforms/submitaction* y recibe bytes xml en el flujo de respuesta. A continuación, el servicio proxy envía los bytes xml de datos a submitUrl para su procesamiento.

* Antes de enviar datos (solicitud del POST) a un servidor, los formularios HTML5 comprueban la conectividad y disponibilidad del servidor. Para verificar la conectividad y disponibilidad, los formularios HTML envían una solicitud de encabezado vacía al servidor. Si el servidor está disponible, el formulario HTML5 envía datos (solicitud del POST) al servidor. Si el servidor no está disponible, aparece un mensaje de error *No se pudo conectar con el servidor,*. La detección avanzada evita que los usuarios tengan que rellenar el formulario. El servlet proxy gestiona la solicitud del encabezado y no emite una excepción.
