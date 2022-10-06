---
title: Renderización de Forms
seo-title: Rendering Forms
description: Utilice el servicio Forms para crear aplicaciones cliente de captura de datos interactivas que validen, procesan, transforman y entregan formularios creados normalmente en Designer. Los creadores de formularios pueden desarrollar un único diseño de formulario que el servicio de Forms procesa en PDF, SWF o HTML en varios entornos de explorador.
seo-description: Use the Forms service to create interactive data capture client applications that validate, process, transform, and deliver forms typically created in Designer. Form authors can develop a single form design that the Forms service renders in PDF, SWF, or HTML in various browser environments.
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
role: Developer
exl-id: ec9ccf04-7cec-493a-91ab-0e399a905338
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Renderización de Forms {#rendering-forms}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

**Acerca del servicio Forms**

El servicio Forms permite crear aplicaciones cliente de captura de datos interactivas que validan, procesan, transforman y entregan formularios creados normalmente en Designer. Los creadores de formularios pueden desarrollar un único diseño de formulario que el servicio de Forms procesa en PDF, SWF o HTML en varios entornos de explorador.

Cuando un usuario final solicita un formulario, una aplicación cliente envía la solicitud al servicio Forms, que devuelve el formulario en un formato adecuado. Tan pronto como el servicio de Forms recibe una solicitud, combina los datos con un diseño de formulario y, a continuación, envía el formulario en el formato deseado. La salida del servicio de formulario es un formulario interactivo, normalmente un documento PDF. Un formulario interactivo permite a los usuarios rellenar campos ubicados en el formulario.

Según el tipo de aplicación cliente, puede escribir el formulario en un explorador web cliente o guardarlo como archivo PDF. Una aplicación basada en Web puede escribir el formulario en un explorador Web. Una aplicación de escritorio puede guardar el formulario como un archivo PDF. Para demostrar cómo escribir en un explorador web y en un archivo PDF, el inicio rápido se encuentra en la variable *Renderización de Forms* se organizan de la siguiente manera:

* Los ejemplos de Java API con establecimiento inflexible de tipos (modo SOAP) son un servlet Java.
* Los ejemplos del servicio web (Java Base64) son un servlet Java.
* Los ejemplos del servicio web (MTOM) son una aplicación de consola (no todos los inicios rápidos tienen un ejemplo MTOM).

>[!NOTE]
>
>Para obtener información sobre la creación de una aplicación web que utilice servlets de java para invocar el servicio de Forms, consulte [Creación de aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

Puede pasar un diseño de formulario (un archivo XDP) o un documento de PDF al servicio de Forms de una de las dos maneras siguientes:

* Puede hacer referencia al diseño de formulario mediante un valor de URL. Este método implica usar una `URLSpec` objeto. La raíz del contenido se pasa al servicio de Forms mediante la variable `URLSpec` del objeto `setContentRootURI` método. El nombre del diseño de formulario ( `formQuery`) se pasa como un parámetro independiente. Los dos valores se concatenan para obtener la referencia absoluta al diseño de formulario. (La mayoría de los inicios rápidos se encuentran en la variable *Renderización de Forms* utilice este método).
* Puede pasar un `com.adobe.idp.Document` que contiene el diseño de formulario para el servicio de Forms. Dos métodos nuevos denominados `renderPDFForm2` y `renderHTMLForm2` aceptar `com.adobe.idp.Document` objeto que contiene un diseño de formulario. (Consulte [Pasar documentos al servicio de Forms](/help/forms/developing/passing-documents-forms-service.md)

Puede realizar estas tareas mediante el servicio Forms:

* Procesar PDF forms interactivos. (Consulte [Renderización de PDF forms interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md).)
* Procesar formularios en el cliente. (Consulte [Representación de Forms en el cliente](/help/forms/developing/rendering-forms-client.md).)
* Procesar formularios basados en fragmentos. (Consulte [Representación de Forms basada en fragmentos](/help/forms/developing/rendering-forms-based-fragments.md).)
* Representar formularios habilitados para derechos. (Consulte [Renderización de Forms con derechos activados](/help/forms/developing/rendering-rights-enabled-forms.md).)
* Procesar formularios como HTML. (Consulte [Representación de Forms como HTML](/help/forms/developing/rendering-forms-html.md).)
* Renderización de Forms HTML mediante archivos CSS personalizados ([Representación de Forms de HTML mediante archivos CSS personalizados](/help/forms/developing/rendering-html-forms-using-custom.md).)
* Gestionar formularios enviados. (Consulte [Gestión de Forms enviado](/help/forms/developing/handling-submitted-forms.md).)
* Creación de documentos de PDF con datos XML enviados. (Consulte [Creación de documentos de PDF con datos XML enviados](/help/forms/developing/creating-pdf-documents-submitted-xml.md).)
* Rellenar formularios de antemano. (Consulte [Rellenado previo de Forms con diseños flexibles](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
* Pasar documentos. (Consulte [Pasar documentos al servicio de Forms](/help/forms/developing/passing-documents-forms-service.md)
* Calcular datos de formulario. (Consulte [Cálculo de datos de formulario](/help/forms/developing/calculating-form-data.md).)
* Optimizar una aplicación. (Consulte [Optimización del rendimiento del servicio Forms](/help/forms/developing/optimizing-performance-forms-service.md).)
