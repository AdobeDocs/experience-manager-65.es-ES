---
title: Arquitectura de formularios HTML5
seo-title: Arquitectura de formularios HTML5
description: Los formularios HTML5 se implementan como un paquete en la instancia de AEM incrustada y expone la funcionalidad como punto final de REST en HTTP/S mediante la arquitectura de Sling Apache RESTful.
seo-description: Los formularios HTML5 se implementan como un paquete en la instancia de AEM incrustada y expone la funcionalidad como punto final de REST en HTTP/S mediante la arquitectura de Sling Apache RESTful.
uuid: 7f515cea-1447-4fc7-82ba-17f2e3f9f80c
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a644978e-5736-4771-918a-dfefe350a4a1
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2045'
ht-degree: 0%

---


# Arquitectura de formularios HTML5{#architecture-of-html-forms}

## Arquitectura {#architecture}

La funcionalidad de formularios HTML5 se implementa como un paquete en la instancia de AEM incrustada y se expone como un punto final de REST a través de HTTP/S usando RESTful [Apache Sling Architecture](https://sling.apache.org/).

![02-aem-forms-Architecture_large](assets/02-aem-forms-architecture_large.jpg)

### Uso de Sling Framework {#using-sling-framework}

[Apache ](https://sling.apache.org/) Slingis está centrado en los recursos. Utiliza una dirección URL de solicitud para resolver primero el recurso. Cada recurso tiene una propiedad **sling:resourceType** (o **sling:resourceSuperType**). En función de esta propiedad, el método de solicitud y las propiedades de la URL de solicitud, se selecciona un script sling para gestionar la solicitud. Este script de sling puede ser un JSP o un servlet. En los formularios HTML5, los nodos **Profile** actúan como recursos de sling y **Profile Renderer** actúa como la secuencia de comandos de sling que gestiona la solicitud para procesar el formulario móvil con un perfil determinado. Un **Procesador de perfiles** es un JSP que lee parámetros de una solicitud y llama al servicio OSGi de Forms.

Para obtener más información sobre el extremo REST y los parámetros de solicitud admitidos, consulte [Representación de plantilla de formulario](/help/forms/using/rendering-form-template.md).

Cuando un usuario realiza una solicitud desde un dispositivo cliente, como un explorador iOS o Android, Sling resuelve primero el nodo de perfil en función de la dirección URL de la solicitud. Desde este nodo de perfil, lee **sling:resourceSuperType** y **sling:resourceType** para determinar todas las secuencias de comandos disponibles que pueden gestionar esta solicitud de procesamiento de formulario. A continuación, utiliza selectores de solicitud de Sling junto con el método de solicitud para identificar la secuencia de comandos más adecuada para gestionar esta solicitud. Una vez que la solicitud llega a un JSP del procesador de perfiles, el JSP llama al servicio OSGi de Forms.

Para obtener más información sobre la resolución de secuencias de comandos de sling, consulte [AEM hoja de referencia de Sling](https://docs.adobe.com/content/docs/en/cq/current/developing/sling_cheatsheet.html) o [descomposición de direcciones URL de Apache Sling](https://sling.apache.org/site/url-decomposition.html).

#### Flujo de llamada de procesamiento de formulario típico {#typical-form-processing-call-flow}

Los formularios HTML5 almacenan en caché todos los objetos intermedios necesarios para procesar (procesar o enviar) un formulario en la primera solicitud. No almacena en caché los objetos que dependen de los datos, ya que es probable que estos objetos cambien.

Formulario móvil mantiene dos niveles diferentes de caché, caché de procesamiento previo y caché de procesamiento. La caché preRender contiene todos los fragmentos e imágenes de una plantilla resuelta y la caché Render contiene contenido procesado como HTML.

![Flujo de trabajo de formularios HTML5](assets/cacheworkflow.png)

Flujo de trabajo de formularios HTML5

Los formularios HTML5 no almacenan en caché plantillas a las que les faltan referencias de fragmentos e imágenes. Si los formularios HTML5 tardan más de lo normal en completarse, compruebe en los registros del servidor si faltan referencias y advertencias. Asegúrese también de que no se alcance el tamaño máximo del objeto.

El servicio OSGi de Forms procesa una solicitud en dos pasos:

* **Presentación y generación del estado del formulario inicial**: El servicio de renderización OSGi de Forms llama al componente Caché de Forms para determinar si el formulario ya se ha almacenado en caché y no se ha invalidado. Si el formulario está en la caché y es válido, proporciona el HTML generado a partir de la caché. Si el formulario se invalida, el servicio de renderización OSGi de Forms genera Diseño de formulario inicial y Estado de formulario en formato XML. Este XML se transforma en HTML layout y Initial JSON Form State mediante el servicio OSGi de Forms y, a continuación, se almacena en caché para solicitudes posteriores.
* **Forms** prerrellenado: Durante la representación, si un usuario solicita formularios con datos previamente rellenados, el servicio de renderización OSGi de Forms llama al contenedor de servicio de Forms y genera un nuevo estado de formulario con datos combinados. Sin embargo, como el diseño ya se ha generado en el paso anterior, esta llamada es más rápida que la primera llamada de . Esta llamada solo realiza la combinación de datos y ejecuta las secuencias de comandos en los datos.

Si hay alguna actualización en el formulario o cualquiera de los recursos utilizados dentro del formulario, el componente de caché del formulario lo detecta y la caché de ese formulario en particular se invalida. Una vez que el servicio OSGi de Forms termina de procesarse, el jsp del procesador de perfiles agrega referencias de biblioteca JavaScript y estilo a este formulario y devuelve la respuesta al cliente. Aquí se puede usar un servidor web típico como [Apache](https://httpd.apache.org/) con compresión HTML activada. Un servidor web reduciría significativamente el tamaño de respuesta, el tráfico de red y el tiempo necesario para transmitir los datos entre el servidor y el equipo cliente.

Cuando un usuario envía el formulario, el explorador envía el estado del formulario en formato JSON al [proxy del servicio de envío](../../forms/using/service-proxy.md); a continuación, el proxy del servicio de envío genera un XML de datos utilizando datos JSON y envía ese XML de datos para enviar el extremo.

## Componentes {#components}

Se necesita el paquete de complementos de AEM Forms para habilitar los formularios HTML5. Para obtener información sobre la instalación del paquete de complementos de AEM Forms, consulte [Instalación y configuración de AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

### Componentes OSGi (adobe-lc-forms-core.jar) {#osgi-components-adobe-lc-forms-core-jar}

**Adobe XFA Forms Renderer (com.adobe.livecycle.adobe-lc-forms-core)**  es el nombre para mostrar del paquete OSGi de formularios HTML5 cuando se visualiza desde la vista de paquete de la consola de administración Felix (https://[host]:[port]/system/console/bundles).

Este componente contiene componentes OSGi para la configuración de procesamiento, administración de caché y configuración.

#### Servicio OSGi de Forms {#forms-osgi-service}

Este servicio OSGi contiene la lógica para procesar un XDP como HTML y gestiona el envío de un formulario para generar datos XML. Este servicio utiliza el contenedor de servicio de Forms. El contenedor de servicio de Forms llama internamente al componente nativo `XMLFormService.exe` que realiza el procesamiento.

Si se recibe una solicitud de procesamiento, este componente llama al contenedor de servicio de Forms para generar información de estado y diseño que se procesa más adelante para generar estados DOM de formulario HTML y JSON.

Este componente también es responsable de la generación de datos XML desde el estado de formulario enviado JSON.

#### Componente de caché {#cache-component}

Los formularios HTML5 utilizan el almacenamiento en caché para optimizar el rendimiento y el tiempo de respuesta. Puede configurar el nivel del servicio de caché para ajustar el equilibrio entre rendimiento y utilización del espacio.

<table>
 <tbody>
  <tr>
   <th>Estrategia de caché</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>Ninguna</td>
   <td>No almacenar en caché artefactos<br /> </td>
  </tr>
  <tr>
   <td>Conservador</td>
   <td>Almacenar en caché solo los artefactos intermedios que se generan antes del procesamiento del formulario, como la plantilla que contiene fragmentos e imágenes en línea</td>
  </tr>
  <tr>
   <td>Agresivo</td>
   <td>Caché Contenido HTML procesado<br /> Almacene en caché todos los artefactos almacenados en caché a nivel conservador.<br /> <strong>Nota</strong>: Esta estrategia ofrece el mejor rendimiento, pero consume más memoria para almacenar los artefactos en caché.</td>
  </tr>
 </tbody>
</table>

Los formularios HTML5 se almacenan en caché en la memoria mediante la estrategia LRU. Si la estrategia de caché se establece en None cache , no se creará y los datos de caché existentes, si los hay, se borrarán. Además de la estrategia de almacenamiento en caché, también puede configurar el tamaño total de la caché en memoria, lo que puede ayudar a tener el límite máximo en el tamaño de la caché y si va más allá, utilizará el modo LRU para liberar recursos de caché.

>[!NOTE]
>
>La caché en memoria no se comparte entre nodos del clúster.

#### Servicio de configuración {#configuration-service}

El servicio de configuración permite ajustar los parámetros de configuración y la configuración de caché para los formularios HTML5.

Para actualizar esta configuración, vaya al Admin Console CQ Felix (disponible en https://&lt;&#39;[server]:[port]&#39;/system/console/configMgr), busque y seleccione Configuración móvil de Forms.

Puede configurar el tamaño de la caché o deshabilitar la caché mediante el servicio de configuración. También puede habilitar la depuración con el parámetro Opciones de depuración . Encontrará más información sobre la depuración de formularios en [Depuración de formularios HTML5](/help/forms/using/debug.md).

### Componentes de tiempo de ejecución (adobe-lc-forms-runtime-pkg.zip) {#runtime-components-adobe-lc-forms-runtime-pkg-zip}

El paquete en tiempo de ejecución contiene las bibliotecas del lado del cliente que se utilizan para procesar formularios HTML.

**Componentes importantes disponibles como parte del paquete Runtime:**

#### Motor de secuencias de comandos {#scripting-engine}

La implementación de Adobe XFA admite dos tipos de lenguajes de secuencias de comandos para permitir la ejecución de lógica definida por el usuario en formularios: JavaScript y FormCalc.

El motor de secuencias de comandos de HTML Forms se escribe en JavaScript para admitir la API de secuencias de comandos XFA en ambos idiomas.

En el momento de la representación, la secuencia de comandos de FormCalc se traduce (y se almacena en caché) en JavaScript del servidor de forma transparente para el usuario o el diseñador.

Este motor de secuencias de comandos utiliza algunas de las funciones de ECMAScript5 como Object.defineProperty. El motor/biblioteca se entrega como CQ Client Lib con el nombre de categoría **xfaforms.profile**. También proporciona **API de FormBridge** para permitir que portales o aplicaciones externos interactúen con el formulario. Con FormBridge, una aplicación externa puede ocultar mediante programación ciertos elementos, obtener o establecer sus valores o cambiar sus atributos.

Para obtener más información, consulte el artículo [Puente de formulario](/help/forms/using/form-bridge-apis.md).

#### Motor de diseño {#layout-engine}

La presentación y el aspecto visual de los formularios HTML5 se basan en las funciones SVG 1.1, jQuery, BackBone y CSS3. El aspecto inicial de un formulario se genera y se almacena en caché en el servidor. El ajuste de esa presentación inicial y cualquier cambio adicional en la presentación del formulario se administran en el cliente. Para conseguirlo, el paquete Runtime contiene un motor de diseño escrito en JavaScript y basado en jQuery/Backbone. Este motor gestiona todo el comportamiento dinámico, como Añadir/Eliminar instancias repetibles o el diseño de objeto acumulable. Este motor de presentación procesa un formulario de una página a la vez. Inicialmente, un usuario solo ve una página y la barra de desplazamiento horizontal solo cuenta para la primera página. Sin embargo, cuando un usuario se desplaza hacia abajo, la siguiente página comienza a procesarse. Esta representación página por página reduce el tiempo necesario para procesar la primera página en un explorador y mejora el rendimiento percibido del formulario. Este motor/biblioteca es parte de CQ Client Lib con el nombre de categoría **xfaforms.profile**.

El motor de diseño también contiene un conjunto de widgets utilizados para capturar el valor de los campos de formulario de un usuario. Estos widgets están modelados como [jQuery UI Widgets](https://api.jqueryui.com/jQuery.widget/) que implementan cierto contrato adicional para funcionar sin problemas con el motor de diseño.

Para obtener más información sobre las utilidades y los contratos correspondientes, consulte [Widgets personalizados para formularios HTML5](/help/forms/using/introduction-widgets.md).

#### Estilo {#styling}

El estilo asociado con los elementos HTML se añade en línea o en función del bloque CSS incrustado. Algunos estilos comunes que no dependen del formulario forman parte de CQ Client Lib con el nombre de categoría xfaforms.profile.

Además de las propiedades de estilo predeterminadas, cada elemento de formulario también contiene ciertas clases CSS basadas en el tipo de elemento, el nombre y otras propiedades. Con estas clases, se pueden restaurar los elementos especificando su propia CSS.

Para obtener más información sobre el estilo y las clases predeterminados, consulte [Introducción a los estilos](/help/forms/using/css-styles.md).

#### Script del lado del servidor y servicios web {#server-side-script-and-web-services}

Cualquier script que esté marcado para ejecutarse en el servidor o marcado para llamar a un servicio web (independientemente de dónde esté marcado para ejecutarse) siempre se ejecuta en el servidor.

El motor de secuencias de comandos del cliente:

1. Realiza una llamada sincrónica al servidor que pasa el estado actual del formulario en forma de JSON
1. Ejecuta la secuencia de comandos o el servicio Web en el servidor
1. Genera un nuevo estado JSON
1. Combina el nuevo estado JSON en el cliente cuando se devuelve la respuesta.

#### Paquetes de recursos de localización {#localization-resource-bundles}

Los formularios HTML5 admiten italiano (it), español (es), portugués de Brasil (pt_BR), chino simplificado (zh_CN), chino tradicional (solo compatibilidad limitada) (zh_TW), coreano (ko_KR), inglés (en_US), francés (fr_FR), alemán (de_DE) y japonés (ja). Según la configuración regional recibida en el encabezado de la solicitud, se envía el paquete de recursos correspondiente al cliente. Este paquete de recursos se agrega al JSP de perfil como una biblioteca de cliente de CQ con el nombre de categoría **xfaforms.I18N**. Puede anular la lógica de selección del paquete de configuración regional en el perfil.

### Componentes de Sling (adobe-lc-forms-content-pkg.zip) {#sling-components-adobe-lc-forms-content-pkg-zip}

El paquete Sling contiene contenido relacionado con Perfiles y Procesador de perfiles.

#### Perfiles {#profiles}

Los perfiles son los nodos de recursos de sling que representan un formulario o una familia de Forms. En el nivel CQ, estos perfiles son nodos JCR. Los nodos residen en la carpeta **/content** del repositorio JCR y pueden estar dentro de cualquier subcarpeta de la carpeta **/content**.

#### Representadores de perfil {#profile-renderers}

El nodo Perfil tiene una propiedad **sling:resourceSuperType** con valor **xfaforms/profile**. Esta propiedad envía internamente solicitudes al script sling para los nodos de perfil ubicados en la carpeta **/libs/xfaforms/profile**. Estas secuencias de comandos son páginas JSP, que son contenedores para reunir los formularios HTML y los artefactos JS/CSS necesarios. Las páginas incluyen referencias a:

* **xfaforms.I18N.&lt;locale>**: Esta biblioteca contiene datos localizados.
* **xfaforms.profile**: Esta biblioteca contiene la implementación para el motor de diseño y secuencias de comandos XFA.

Estas bibliotecas están modeladas como CQ Client Libraries que aprovecha las capacidades de concatenación, minificación y compresión automáticas de las bibliotecas JavaScript del marco de CQ.
Para obtener más información sobre las bibliotecas de cliente de CQ, consulte [Documentación de CQ Clientlib](https://docs.adobe.com/docs/en/cq/current/developing/components/clientlibs.html).

Como se ha descrito anteriormente, el procesador de perfiles JSP llama a Forms Service a través de un sling include. Este JSP también establece varias opciones de depuración en función de la configuración de administración o los parámetros de solicitud.

Los formularios HTML5 permiten a los desarrolladores crear un perfil y un procesador de perfiles para personalizar el aspecto de los formularios. Por ejemplo, los formularios HTML permiten a los desarrolladores integrar formularios en un panel o en la sección &lt;div> de un portal HTML existente.
Para obtener más información sobre la creación de perfiles personalizados, consulte [Creación de un perfil personalizado](/help/forms/using/custom-profile.md).
