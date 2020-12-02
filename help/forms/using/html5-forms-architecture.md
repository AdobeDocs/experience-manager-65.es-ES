---
title: Arquitectura de formularios HTML5
seo-title: Arquitectura de formularios HTML5
description: Los formularios HTML5 se implementan como un paquete dentro de la instancia de AEM incrustada y exponen la funcionalidad como punto final REST sobre HTTP/S mediante la arquitectura RESTful Apache Sling.
seo-description: Los formularios HTML5 se implementan como un paquete dentro de la instancia de AEM incrustada y exponen la funcionalidad como punto final REST sobre HTTP/S mediante la arquitectura RESTful Apache Sling.
uuid: 7f515cea-1447-4fc7-82ba-17f2e3f9f80c
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a644978e-5736-4771-918a-dfefe350a4a1
docset: aem65
translation-type: tm+mt
source-git-commit: 84dd0d551431169239f63cff62a015e15f998e7d
workflow-type: tm+mt
source-wordcount: '2043'
ht-degree: 0%

---


# Arquitectura de formularios HTML5{#architecture-of-html-forms}

## Arquitectura {#architecture}

La funcionalidad de formularios HTML5 se implementa como un paquete dentro de la instancia de AEM incrustada y se expone como un punto final REST sobre HTTP/S mediante RESTful [Apache Sling Architecture](https://sling.apache.org/).

![02-aem-forms-Architecture_large](assets/02-aem-forms-architecture_large.jpg)

### Uso de Sling Framework {#using-sling-framework}

[Apache ](https://sling.apache.org/) Slingis se centra en los recursos. Utiliza una URL de solicitud para resolver primero el recurso. Cada recurso tiene una propiedad **sling:resourceType** (o **sling:resourceSuperType**). En función de esta propiedad, el método de solicitud y las propiedades de la dirección URL de la solicitud, se selecciona una secuencia de comandos sling para gestionar la solicitud. Este script sling puede ser un JSP o un servlet. En los formularios HTML5, los nodos **Perfil** actúan como recursos de sling y **Perfil Renderer** actúa como la secuencia de comandos sling que gestiona la solicitud para procesar el formulario móvil con un perfil determinado. Un **procesador de Perfil** es un JSP que lee parámetros de una solicitud y llama al servicio OSGi de Forms.

Para obtener más información sobre el extremo REST y los parámetros de solicitud admitidos, consulte [Representación de plantilla de formulario](/help/forms/using/rendering-form-template.md).

Cuando un usuario realiza una solicitud desde un dispositivo cliente, como un navegador iOS o Android, Sling resuelve primero el nodo de Perfil en función de la dirección URL de la solicitud. Desde este nodo de Perfil, lee **sling:resourceSuperType** y **sling:resourceType** para determinar todas las secuencias de comandos disponibles que pueden gestionar esta solicitud de procesamiento de formulario. A continuación, utiliza selectores de solicitud Sling junto con el método de solicitud para identificar la secuencia de comandos más adecuada para gestionar esta solicitud. Una vez que la solicitud llega a un JSP de procesador de Perfil, el JSP llama al servicio OSGi de Forms.

Para obtener más información sobre la resolución de secuencias de comandos sling, consulte [AEM hoja de consejos Sling](https://docs.adobe.com/content/docs/en/cq/current/developing/sling_cheatsheet.html) o [descomposición de direcciones URL Sling de Apache](https://sling.apache.org/site/url-decomposition.html).

#### Flujo de llamada de procesamiento de formularios típico {#typical-form-processing-call-flow}

Los formularios HTML5 almacenan en caché todos los objetos intermedios necesarios para procesar (representación o envío) un formulario en la primera solicitud. No almacena en caché los objetos que dependen de los datos, ya que es probable que estos objetos cambien.

Formulario móvil mantiene dos niveles diferentes de caché: caché de preprocesamiento y caché de procesamiento. La caché preRender contiene todos los fragmentos e imágenes de una plantilla resuelta y la caché de procesamiento contiene contenido procesado como HTML.

![Flujo de trabajo de formularios HTML5](assets/cacheworkflow.png)

Flujo de trabajo de formularios HTML5

Los formularios HTML5 no almacenan en caché plantillas que no tienen referencias de fragmentos e imágenes. Si los formularios HTML5 tardan más de lo normal, compruebe en los registros del servidor si faltan referencias y advertencias. Asegúrese también de que no se alcance el tamaño máximo del objeto.

El servicio OSGi de Forms procesa una solicitud en dos pasos:

* **Presentación y generación** de estado de formulario inicial: El servicio de procesamiento OSGi de Forms llama al componente Caché de Forms para determinar si el formulario ya se ha almacenado en caché y no se ha invalidado. Si el formulario está en caché y es válido, proporciona el HTML generado a partir de la caché. Si el formulario está invalidado, el servicio de procesamiento OSGi de Forms genera Presentación de formulario inicial y Estado de formulario en formato XML. El servicio OSGi de Forms transforma este XML en formato HTML y estado de formulario JSON inicial en formato HTML y, a continuación, lo almacena en caché para solicitudes posteriores.
* **Forms** prerellenado: Durante la representación, si un usuario solicita formularios con datos previamente rellenados, el servicio de procesamiento OSGi de Forms llama al contenedor de servicio de Forms y genera un nuevo estado de formulario con datos combinados. Sin embargo, como el diseño ya se ha generado en el paso anterior, esta llamada es más rápida que la primera llamada. Esta llamada solo realiza la combinación de datos y ejecuta las secuencias de comandos en los datos.

Si hay alguna actualización en el formulario o alguno de los recursos utilizados dentro del formulario, el componente de la caché del formulario la detecta y la caché de ese formulario en particular se invalida. Una vez que el servicio OSGi de Forms finaliza el procesamiento, el jsp del procesador de Perfil agrega referencias de biblioteca de JavaScript y estilo a este formulario y devuelve la respuesta al cliente. Aquí se puede utilizar un servidor web típico como [Apache](https://httpd.apache.org/) con compresión HTML activada. Un servidor web reduciría el tamaño de respuesta, el tráfico de red y el tiempo necesario para transmitir los datos entre el servidor y el equipo cliente de forma significativa.

Cuando un usuario envía el formulario, el explorador envía el estado del formulario en formato JSON al [proxy de servicio de envío](../../forms/using/service-proxy.md); a continuación, el proxy de servicio de envío genera un XML de datos con datos JSON y envía ese XML de datos para enviar el extremo.

## Componentes {#components}

Se requiere el paquete de complementos de AEM Forms para activar los formularios HTML5. Para obtener información sobre la instalación del paquete de complementos de AEM Forms, consulte [Instalación y configuración de AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

### Componentes OSGi (adobe-lc-forms-core.jar) {#osgi-components-adobe-lc-forms-core-jar}

**Adobe XFA Forms Renderer (com.adobe.livecycle.adobe-lc-forms-core)** es el nombre para mostrar del paquete OSGi de formularios HTML5 cuando se visualiza desde la Vista Bundle de la consola de administración Felix (https://[host]:[port]/system/console/buncles).

Este componente contiene componentes OSGi para la configuración de procesamiento, administración de caché y configuración.

#### Servicio OSGi de Forms {#forms-osgi-service}

Este servicio OSGi contiene la lógica para procesar un XDP como HTML y gestiona el envío de un formulario para generar datos XML. Este servicio utiliza el contenedor de servicio de Forms. El contenedor de servicio de Forms llama internamente al componente nativo `XMLFormService.exe` que realiza el procesamiento.

Si se recibe una solicitud de procesamiento, este componente llama al contenedor de servicios de Forms para generar información de presentación y estado que se procesa más adelante para generar estados DOM de formularios HTML y JSON.

Este componente también es responsable de generar datos XML a partir del estado de formulario enviado JSON.

#### Componente de caché {#cache-component}

Los formularios HTML5 utilizan el almacenamiento en caché para optimizar el rendimiento y el tiempo de respuesta. Puede configurar el nivel del servicio de caché para ajustar el equilibrio entre el rendimiento y la utilización del espacio.

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
   <td>Caché Contenido HTML procesado<br /> Almacene en caché todos los artefactos almacenados en caché en el nivel conservador.<br /> <strong>Nota</strong>: Esta estrategia resulta en un mejor rendimiento, pero consume más memoria para almacenar los artefactos almacenados en caché.</td>
  </tr>
 </tbody>
</table>

Los formularios HTML5 se guardan en la memoria caché mediante la estrategia LRU. Si la estrategia de caché se establece en la caché Ninguno, no se creará la caché y los datos de caché existentes, si los hay, se borrarán. Además de la estrategia de almacenamiento en caché, también puede configurar el tamaño total de caché en memoria, lo que puede ayudar a tener el límite máximo en el tamaño de caché y si va más allá, utilizará el modo LRU para liberar recursos de caché.

>[!NOTE]
>
>La caché en memoria no se comparte entre los nodos del clúster.

#### Servicio de configuración {#configuration-service}

El servicio de configuración permite ajustar los parámetros de configuración y la configuración de caché para formularios HTML5.

Para actualizar esta configuración, vaya al Admin Console CQ Felix (disponible en https://&lt;&#39;[server]:[port]&#39;/system/console/configMgr), busque y seleccione Configuración de Mobile Forms.

Puede configurar el tamaño de caché o deshabilitar la caché mediante el servicio de configuración. También puede habilitar la depuración mediante el parámetro Opciones de depuración. Encontrará más información sobre la depuración de formularios en [Depuración de formularios HTML5](/help/forms/using/debug.md).

### Componentes de tiempo de ejecución (adobe-lc-forms-Runtime-pkg.zip) {#runtime-components-adobe-lc-forms-runtime-pkg-zip}

El paquete de tiempo de ejecución contiene las bibliotecas del lado del cliente utilizadas para procesar formularios HTML.

**Componentes importantes disponibles como parte del paquete Runtime:**

#### Motor de secuencias de comandos {#scripting-engine}

La implementación XFA de Adobe admite dos tipos de lenguajes de secuencias de comandos para habilitar la ejecución lógica definida por el usuario en formularios: JavaScript y FormCalc.

El motor de secuencias de comandos de HTML Forms se escribe en JavaScript para admitir la API de secuencias de comandos XFA en ambos idiomas.

En el momento de la representación, la secuencia de comandos de FormCalc se traduce (y se almacena en caché) en JavaScript en el servidor transparente para el usuario o diseñador.

Este motor de secuencias de comandos utiliza algunas de las funciones de ECMAScript5 como Object.defineProperty. El motor/biblioteca se entrega como CQ Client Lib con el nombre de categoría **xfaforms.perfil**. También proporciona **API de FormBridge** para permitir que portales o aplicaciones externas interactúen con el formulario. Con FormBridge, una aplicación externa puede ocultar mediante programación determinados elementos, obtener o establecer sus valores o cambiar sus atributos.

Para obtener más información, consulte el artículo [Puente de formulario](/help/forms/using/form-bridge-apis.md).

#### Motor de diseño {#layout-engine}

La presentación y el aspecto visual de los formularios HTML5 se basan en las funciones SVG 1.1, jQuery, BackBone y CSS3. El aspecto inicial de un formulario se genera y se almacena en caché en el servidor. La modificación de esa presentación inicial y cualquier otro cambio incremental en la presentación del formulario se administran en el cliente. Para conseguirlo, el paquete Runtime contiene un motor de diseño escrito en JavaScript y basado en jQuery/Backbone. Este motor gestiona todo el comportamiento dinámico, como Añadir/Eliminar instancias repetibles o Diseño de objetos acumulables. Este motor de presentación procesa un formulario de una página a la vez. Inicialmente, un usuario solo vista una página y la barra de desplazamiento horizontal solo cuenta para la primera página. Sin embargo, cuando un usuario se desplaza hacia abajo, la página siguiente inicio el procesamiento. Esta representación página por página reduce la cantidad de tiempo necesario para procesar la primera página en un explorador y mejora el rendimiento percibido del formulario. Este motor/biblioteca forma parte de CQ Client Lib con el nombre de categoría **xfaforms.perfil**.

El motor de presentación también contiene un conjunto de utilidades utilizadas para capturar el valor de los campos de formulario de un usuario. Estos widgets están modelados como [utilidades de la interfaz de usuario de jQuery](https://api.jqueryui.com/jQuery.widget/) que implementan un contrato adicional para trabajar sin problemas con el motor de diseño.

Para obtener más información sobre las utilidades y los contratos correspondientes, consulte [Utilidades personalizadas para formularios HTML5](/help/forms/using/introduction-widgets.md).

#### Estilo {#styling}

El estilo asociado con los elementos HTML se agrega en línea o en función de un bloque CSS incrustado. Algunos estilos comunes que no dependen del formulario forman parte de CQ Client Lib con el nombre de categoría xfaforms.perfil.

Además de las propiedades de estilo predeterminadas, cada elemento de formulario también contiene ciertas clases CSS basadas en el tipo de elemento, el nombre y otras propiedades. Con estas clases, se pueden volver a aplicar estilo a los elementos especificando su propia CSS.

Para obtener más información sobre el estilo y las clases predeterminados, consulte [Introducción a los estilos](/help/forms/using/css-styles.md).

#### Script del lado del servidor y servicios Web {#server-side-script-and-web-services}

Todas las secuencias de comandos marcadas para ejecutarse en el servidor o marcadas para llamar a un servicio Web (independientemente de dónde esté marcado para ejecutarse) siempre se ejecutan en el servidor.

Motor de secuencias de comandos de cliente:

1. Realiza una llamada sincrónica al servidor que pasa el estado de formulario actual en forma de JSON
1. Ejecuta la secuencia de comandos o el servicio Web en el servidor
1. Genera un nuevo estado JSON
1. Combina el nuevo estado JSON en el cliente cuando se devuelve la respuesta.

#### Paquetes de recursos de localización {#localization-resource-bundles}

Los formularios HTML5 admiten italiano (it), español (es), portugués brasileño (pt_BR), chino simplificado (zh_CN), chino tradicional (solo compatibilidad limitada) (zh_TW), coreano (ko_KR), inglés (en_US), francés (fr_FR), alemán (de_DE) y japonés (ja). Según la configuración regional recibida en el encabezado de la solicitud, se envía al cliente el paquete de recursos correspondiente. Este paquete de recursos se agrega a Perfil JSP como una biblioteca de cliente de CQ con el nombre de categoría **xfaforms.I18N**. Puede anular la lógica de selección del paquete de configuración regional en el perfil.

### Sling Components (adobe-lc-forms-content-pkg.zip) {#sling-components-adobe-lc-forms-content-pkg-zip}

El paquete Sling contiene contenido relacionado con Perfiles y procesador de Perfil.

#### Perfiles {#profiles}

Los perfiles son los nodos de recursos en sling que representan un formulario o familia de Forms. A nivel de CQ, estos perfiles son nodos JCR. Los nodos residen en la carpeta **/content** del repositorio JCR y pueden estar dentro de cualquier subcarpeta de la carpeta **/content**.

#### Procesadores de perfil {#profile-renderers}

El nodo Perfil tiene una propiedad **sling:resourceSuperType** con el valor **xfaforms/perfil**. Esta propiedad envía internamente solicitudes a la secuencia de comandos sling para nodos Perfil ubicados en la carpeta **/libs/xfaforms/perfil**. Estas secuencias de comandos son páginas JSP, que son contenedores para agrupar los formularios HTML y los artefactos JS/CSS requeridos. Las páginas incluyen referencias a:

* **xfaforms.I18N.&lt;locale>**:: Esta biblioteca contiene datos localizados.
* **xfaforms.perfil**: Esta biblioteca contiene la implementación para el motor XFA Scripting y Layout.

Estas bibliotecas están modeladas como bibliotecas de cliente de CQ que aprovecha las ventajas de la concatenación automática, la minimización y las capacidades de compresión de las bibliotecas JavaScript del marco de CQ.
Para obtener más información sobre las bibliotecas de cliente de CQ, consulte [Documentación de CQ Clientlib](https://docs.adobe.com/docs/en/cq/current/developing/components/clientlibs.html).

Como se ha descrito anteriormente, el JSP del procesador de perfil llama al servicio Forms a través de un inclusión de sling. Este JSP también establece varias opciones de depuración en función de la configuración de administración o los parámetros de solicitud.

Los formularios HTML5 permiten a los desarrolladores crear un procesador de Perfil y Perfil para personalizar el aspecto de los formularios. Por ejemplo, los formularios HTML permiten a los desarrolladores integrar formularios en un panel o en la sección &lt;div> de un portal HTML existente.
Para obtener más información sobre la creación de perfiles personalizados, consulte [Creación de un Perfil personalizado](/help/forms/using/custom-profile.md).
