---
title: Renderización de Forms
seo-title: Renderización de Forms
description: Utilice el servicio Forms para crear aplicaciones cliente de captura de datos interactivas que validen, procesan, transforman y entregan formularios creados normalmente en Designer. Los creadores de formularios pueden desarrollar un único diseño de formulario que el servicio de Forms procesa en PDF, SWF o HTML en varios entornos de explorador.
seo-description: Utilice el servicio Forms para crear aplicaciones cliente de captura de datos interactivas que validen, procesan, transforman y entregan formularios creados normalmente en Designer. Los creadores de formularios pueden desarrollar un único diseño de formulario que el servicio de Forms procesa en PDF, SWF o HTML en varios entornos de explorador.
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---


# Renderización de Forms {#rendering-forms}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

**Acerca del servicio Forms**

El servicio Forms permite crear aplicaciones cliente de captura de datos interactivas que validan, procesan, transforman y entregan formularios creados normalmente en Designer. Los creadores de formularios pueden desarrollar un único diseño de formulario que el servicio de Forms procesa en PDF, SWF o HTML en varios entornos de explorador.

Cuando un usuario final solicita un formulario, una aplicación cliente envía la solicitud al servicio Forms, que devuelve el formulario en un formato adecuado. Tan pronto como el servicio de Forms recibe una solicitud, combina los datos con un diseño de formulario y, a continuación, envía el formulario en el formato deseado. El resultado del servicio de formulario es un formulario interactivo, normalmente un documento PDF. Un formulario interactivo permite a los usuarios rellenar campos ubicados en el formulario.

Según el tipo de aplicación cliente, puede escribir el formulario en un explorador web cliente o guardarlo como archivo PDF. Una aplicación basada en Web puede escribir el formulario en un explorador Web. Una aplicación de escritorio puede guardar el formulario como un archivo PDF. Para demostrar cómo escribir en un explorador web y en un archivo PDF, los inicios rápidos ubicados en la sección *Rendering Forms* se organizan de la siguiente manera:

* Los ejemplos de Java API con establecimiento inflexible de tipos (modo SOAP) son un servlet Java.
* Los ejemplos del servicio web (Java Base64) son un servlet Java.
* Los ejemplos del servicio web (MTOM) son una aplicación de consola (no todos los inicios rápidos tienen un ejemplo MTOM).

>[!NOTE]
>
>Para obtener información sobre la creación de una aplicación web que utilice servlets de java para invocar el servicio Forms, consulte [Creación de aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

Puede pasar un diseño de formulario (un archivo XDP) o un documento PDF al servicio de Forms mediante una de las dos formas siguientes:

* Puede hacer referencia al diseño de formulario mediante un valor de URL. Este método implica el uso de un objeto `URLSpec`. La raíz del contenido se pasa al servicio de Forms mediante el método `URLSpec` del objeto `setContentRootURI`. El nombre del diseño de formulario ( `formQuery`) se pasa como un parámetro independiente. Los dos valores se concatenan para obtener la referencia absoluta al diseño de formulario. (La mayoría de los inicios rápidos ubicados en la sección *Rendering Forms* utilizan este método).
* Puede pasar un `com.adobe.idp.Document` que contenga el diseño de formulario al servicio de Forms. Dos nuevos métodos llamados `renderPDFForm2` y `renderHTMLForm2` aceptan un objeto `com.adobe.idp.Document` que contiene un diseño de formulario. (Consulte [Pasar documentos al servicio de Forms](/help/forms/developing/passing-documents-forms-service.md)

Puede realizar estas tareas mediante el servicio Forms:

* Procesar PDF forms interactivos. (Consulte [Representación de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)).
* Procesar formularios en el cliente. (Consulte [Renderización de Forms en Client](/help/forms/developing/rendering-forms-client.md)).
* Procesar formularios basados en fragmentos. (Consulte [Procesamiento de Forms basado en fragmentos](/help/forms/developing/rendering-forms-based-fragments.md)).
* Representar formularios habilitados para derechos. (Consulte [Rendering Rights-Enabled Forms](/help/forms/developing/rendering-rights-enabled-forms.md)).
* Representar formularios como HTML. (Consulte [Representación de Forms como HTML](/help/forms/developing/rendering-forms-html.md)).
* Renderización de HTML Forms mediante archivos CSS personalizados ([Renderización de HTML Forms mediante archivos CSS personalizados](/help/forms/developing/rendering-html-forms-using-custom.md))
* Gestionar formularios enviados. (Consulte [Gestión de Forms enviado](/help/forms/developing/handling-submitted-forms.md)).
* Creación de documentos PDF con datos XML enviados. (Consulte [Creación de documentos PDF con datos XML enviados](/help/forms/developing/creating-pdf-documents-submitted-xml.md)).
* Rellenar formularios de antemano. (Consulte [Rellenado previo de Forms con diseños de posición variable](/help/forms/developing/prepopulating-forms-flowable-layouts.md)).
* Pasar documentos. (Consulte [Pasar documentos al servicio de Forms](/help/forms/developing/passing-documents-forms-service.md)
* Calcular datos de formulario. (Consulte [Cálculo de datos del formulario](/help/forms/developing/calculating-form-data.md)).
* Optimizar una aplicación. (Consulte [Optimización del rendimiento del servicio de Forms](/help/forms/developing/optimizing-performance-forms-service.md)).

   ***Sugerencia **: El sitio web del Desarrollador de Adobes contiene el siguiente artículo que explica cómo crear una aplicación ASP.NET que invoque el servicio de Forms y procese formularios. Consulte [Creación de formularios que procesen aplicaciones ASP.NET](https://www.adobe.com/devnet/livecycle/articles/asp_net.html).*

