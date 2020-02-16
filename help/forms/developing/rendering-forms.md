---
title: Representación de formularios
seo-title: Representación de formularios
description: nulo
seo-description: nulo
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
translation-type: tm+mt
source-git-commit: 687cdacc2868de16a4df968dddedd330ce3317bb

---


# Rendering Forms {#rendering-forms}

**Acerca del servicio Forms**

El servicio Forms permite crear aplicaciones cliente de captura de datos interactivas que validan, procesan, transforman y entregan formularios creados normalmente en Designer. Los autores de formularios pueden desarrollar un único diseño de formulario que el servicio Forms procesa en PDF, SWF o HTML en diversos entornos de explorador.

Cuando un usuario final solicita un formulario, una aplicación cliente envía la solicitud al servicio Forms, que devuelve el formulario en un formato adecuado. Tan pronto como el servicio Forms recibe una solicitud, combina los datos con un diseño de formulario y, a continuación, envía el formulario en el formato deseado. El resultado del servicio de formulario es un formulario interactivo, normalmente un documento PDF. Un formulario interactivo permite a los usuarios rellenar los campos ubicados en el formulario.

Según el tipo de aplicación cliente, puede escribir el formulario en un navegador web cliente o guardarlo como archivo PDF. Una aplicación basada en Web puede escribir el formulario en un explorador Web. Una aplicación de escritorio puede guardar el formulario como un archivo PDF. Para mostrar cómo escribir en un explorador Web y en un archivo PDF, los inicios rápidos que se encuentran en la sección *Representar formularios* se organizan de la siguiente manera:

* Los ejemplos de Java API con establecimiento inflexible de tipos (modo SOAP) son un servlet de Java.
* Los ejemplos del servicio Web (Java Base64) son un servlet Java.
* Los ejemplos de servicio Web (MTOM) son una aplicación de consola (no todos los inicios rápidos tienen un ejemplo MTOM).

***Nota **: Para obtener información sobre la creación de una aplicación web que utilice servlets de Java para invocar el servicio Forms, consulte[Creación de aplicaciones web que procesen formularios](/help/forms/developing/creating-web-applications-renders-forms.md).*


Puede pasar un diseño de formulario (un archivo XDP) o un documento PDF al servicio Forms de una de las dos formas siguientes:

* Puede hacer referencia al diseño de formulario utilizando un valor de URL. Este método implica el uso de un `URLSpec` objeto. La raíz del contenido se pasa al servicio Forms mediante el `URLSpec` método `setContentRootURI` del objeto. El nombre del diseño de formulario ( `formQuery`) se pasa como un parámetro independiente. Los dos valores se concatenan para obtener la referencia absoluta al diseño de formulario. (La mayoría de los inicios rápidos ubicados en la sección *Representar formularios* utilizan este método).
* Puede pasar un `com.adobe.idp.Document` formulario que contenga el diseño de formulario al servicio Forms. Dos nuevos métodos con nombre `renderPDFForm2` y `renderHTMLForm2` aceptar un `com.adobe.idp.Document` objeto que contiene un diseño de formulario. (Consulte [Pasar documentos al servicio Forms)](/help/forms/developing/passing-documents-forms-service.md)

Puede realizar estas tareas mediante el servicio Forms:

* Representar formularios PDF interactivos. (Consulte [Representación de formularios](/help/forms/developing/rendering-interactive-pdf-forms.md)PDF interactivos).
* Procesar formularios en el cliente. (Consulte [Representación de formularios en el cliente](/help/forms/developing/rendering-forms-client.md)).
* Procesar formularios basados en fragmentos. (Consulte [Representación de formularios basados en fragmentos](/help/forms/developing/rendering-forms-based-fragments.md)).
* Representar formularios habilitados para derechos. (Consulte [Representación de formularios](/help/forms/developing/rendering-rights-enabled-forms.md)habilitados para derechos).
* Procesar formularios como HTML. (Consulte [Representación de formularios como HTML](/help/forms/developing/rendering-forms-html.md)).
* Representación de formularios HTML con archivos CSS personalizados ([procesamiento de formularios HTML con archivos](/help/forms/developing/rendering-html-forms-using-custom.md)CSS personalizados).
* Administrar formularios enviados. (Consulte [Gestión de formularios](/help/forms/developing/handling-submitted-forms.md)enviados).
* Creación de documentos PDF con datos XML enviados. (Consulte [Creación de documentos PDF con datos](/help/forms/developing/creating-pdf-documents-submitted-xml.md)XML enviados).
* Rellenar formularios de antemano. (Consulte [Rellenado previo de formularios con diseños](/help/forms/developing/prepopulating-forms-flowable-layouts.md)de posición variable).
* Pasar documentos. (Consulte [Pasar documentos al servicio Forms)](/help/forms/developing/passing-documents-forms-service.md)
* Calcular datos de formulario. (Consulte [Cálculo de datos](/help/forms/developing/calculating-form-data.md)de formulario.)
* Optimizar una aplicación. (Consulte [Optimización del rendimiento del servicio](/help/forms/developing/optimizing-performance-forms-service.md)Forms).

   ***Sugerencia **: El sitio web de desarrolladores de Adobe contiene el siguiente artículo que explica cómo crear una aplicación ASP.NET que invoque el servicio Forms y procese formularios. Consulte[Creación de aplicaciones](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)ASP.NET de procesamiento de formularios.*

