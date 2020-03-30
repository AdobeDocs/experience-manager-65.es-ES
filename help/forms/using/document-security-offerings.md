---
title: Ofertas de seguridad de Documento
seo-title: Ofertas de seguridad de Documento
description: Obtenga información sobre las distintas herramientas y funciones de AEM Documento Security
seo-description: Obtenga información sobre las distintas herramientas y funciones de AEM Documento Security
uuid: 24e3275c-cd44-47c0-a6a0-e4cfb1bced8a
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 91e85e86-2361-4d1d-aa73-c3cce46ab1f1
docset: aem65
translation-type: tm+mt
source-git-commit: e45e335d433f17a48ba1bf27a93c5b1003369512

---


# Ofertas de seguridad de Documento{#document-security-offerings}

La seguridad de Adobe Experience Manager Forms documento garantiza que solo los usuarios autorizados puedan utilizar sus documentos. Con la seguridad de documento, puede distribuir con seguridad cualquier información que haya guardado en un formato compatible. Los formatos de archivo admitidos son Adobe Portable Documento Format (PDF) y Microsoft Word, Excel y PowerPoint.

Puede proteger documentos mediante políticas. La configuración de confidencialidad que especifique en una política determinará cómo puede un destinatario utilizar un documento al que aplique la política. Por ejemplo, puede especificar si los destinatarios pueden imprimir o copiar texto, editar texto o agregar firmas y comentarios a documentos protegidos.

Las directivas se almacenan en el servidor de seguridad de Documento; las políticas se aplican a los documentos a través de la aplicación cliente. Cuando se aplica una política a un documento, la configuración de confidencialidad especificada en la política protege la información que contiene el documento. Puede distribuir el documento protegido por una política a destinatarios autorizados por la política.

En el diagrama siguiente se muestra la arquitectura típica de AEM Forms Documento Security:

![Seguridad de Documento: arquitectura recomendada](do-not-localize/document_security_architecture.png)

## Clientes de Documento Security {#document-security-clients}

Documento Security proporciona varios clientes para proteger documentos, vista y edición de documentos protegidos e indexadores para permitir la búsqueda de texto completo en documentos protegidos. Puede elegir un cliente según sus necesidades y las capacidades del cliente.

Documento Security Server es el componente central mediante el cual Documento Security realiza transacciones como la autenticación de usuarios, la administración en tiempo real de políticas y la aplicación de la confidencialidad. El servidor también proporciona un repositorio central para directivas, registros de auditoría y otra información relacionada.

El servidor de seguridad de Documento proporciona una interfaz basada en web (página web) para crear políticas, administrar documentos protegidos por políticas y supervisar eventos asociados con documentos protegidos por políticas. Los administradores también pueden configurar opciones globales como autenticación de usuarios, auditoría y mensajería para los usuarios invitados, y administrar las cuentas de usuario invitadas.

El servidor se incluye en la oferta del complemento AEM Forms Documento Security. Puede ponerse en contacto con el equipo [de](https://www.adobe.com/products/request-consultation/marketing-cloud.html?s_osc=70114000002JNwKAAW&s_iid=70114000002JHs3AAG) ventas de AEM Forms para adquirir el complemento Documento Security.

### Proteger documentos {#protect-documents}

AEM Forms Documento Security proporciona varias herramientas para aplicar políticas de seguridad. Puede elegir una herramienta según sus necesidades y especificaciones.

![documento-seguridad-ofertas](assets/document-security-offerings.png)

Puede utilizar el SDK de seguridad de Documento, Adobe Acrobat, Documento Security Extension for Microsoft Office o la biblioteca de protección portátil para aplicar y realizar el seguimiento de las políticas de seguridad:

* **SDK de seguridad de Documento:** El SDK es un cliente con muchas funciones. Puede utilizar el SDK de seguridad de Documento para acceder a la funcionalidad del servidor de documento, abrir documentos protegidos por políticas y desarrollar extensiones, complementos o aplicaciones personalizados. Por ejemplo, puede desarrollar extensiones para proteger formatos de archivo personalizados o integrar SDK con soluciones de prevención de pérdida de datos (DLP). Las extensiones, aplicaciones y complementos desarrollados con el SDK de Document Security envían documentos al servidor de AEM Forms designado y las políticas se aplican en el servidor. Tenga en cuenta también que el SDK de cliente de seguridad de AEM Forms documento (CSDK) no puede desproteger los documentos protegidos mediante la biblioteca de protección portátil (PPL) y viceversa.

   El SDK de seguridad de Documento está disponible para Java y C++. El SDK de Java se incluye en la oferta de seguridad de Documento de AEM Forms y se instala en la implementación de formularios AEM en JEE. Puede ponerse en contacto con el equipo [de asistencia de](https://helpx.adobe.com/marketing-cloud/contact-support.html) AEM para adquirir el SDK de C++. El SDK de C++ se puede compilar con Microsoft Visual Studio 2013. Puede visitar el sitio de documentación [de la API de seguridad de](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html) Documento para conocer y utilizar las funciones del SDK.

* **Adobe Acrobat:** Puede utilizar Adobe Acrobat para aplicar políticas de seguridad a documentos PDF creados con aplicaciones de escritorio conocidas, como Microsoft Office, navegadores web o cualquier aplicación que admita la impresión en formato PDF.

   Puede comprar y descargar Adobe Acrobat desde el sitio web de [Adobe](https://acrobat.adobe.com/us/en/free-trial-download.html). El artículo [Configuración de políticas de seguridad de Adobe Acrobat para archivos PDF](https://helpx.adobe.com/acrobat/using/setting-security-policies-pdfs.html) proporciona información detallada sobre la creación y aplicación de políticas en Adobe Acrobat.

* **Documento Security Extension for Microsoft Office**: Puede utilizar Documento Security Extension for Microsoft Office para aplicar políticas predefinidas a sus archivos de Microsoft Office desde los programas de Microsoft Office. La extensión garantiza que solo las personas autorizadas puedan utilizar archivos de Microsoft Word, Excel y PowerPoint protegidos por políticas. Solo los usuarios autorizados que tengan instalado el complemento pueden utilizar los archivos protegidos por políticas.

   La extensión Seguridad de Documento está disponible como complemento de Microsoft Office. Puede ponerse en contacto con el equipo [de asistencia de](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html) AEM para obtener la extensión. Más adelante, puede visitar la ayuda de [Documento Security Extension for Microsoft Office](https://helpx.adobe.com/aem-forms/aem-document-security/download-installer.html) para obtener información sobre la instalación, la configuración y el uso de la extensión.

* **Biblioteca de protección portátil:** La biblioteca de protección portátil (PPL) protege un documento localmente sin enviar el documento al servidor de AEM Forms. Sólo las credenciales de seguridad y los detalles de las políticas se desplazan por la red. PPL también le permite limitar el acceso a la recuperación de directivas solo a los usuarios que iniciaron sesión. Puede recuperar directivas con el contexto del usuario que ha iniciado sesión en AEM.

   Junto con lo anterior, la biblioteca de protección predecible tiene todas las características del SDK de seguridad de Documento. Puede utilizar el SDK de seguridad de Documento para acceder a la funcionalidad del servidor de documento, abrir documentos protegidos por políticas y desarrollar extensiones, complementos o aplicaciones personalizados. Tenga en cuenta también que la biblioteca de protección portátil (PPL) no puede desproteger los documentos protegidos mediante el SDK de cliente de seguridad de AEM Forms documento (CSDK) y viceversa.

   La biblioteca de protección portátil está disponible para los idiomas Java y C++ en las versiones de 32 y 64 bits. También está disponible como paquete OSGi para AEM Forms en OSGi. La PPL de C++ se puede compilar con Microsoft Visual Studio 2013. Si tiene licencia del complemento AEM Forms Documento Security, puede ponerse en contacto con el equipo de asistencia de seguridad [de Documento de](https://helpx.adobe.com/marketing-cloud/contact-support.html) AEM Forms para adquirir la biblioteca de protección portátil. Más adelante, puede utilizar la Ayuda de la biblioteca de protección portátil (incluida en la biblioteca) para configurar y utilizar la biblioteca de protección portátil.

### Vista o edición de documentos protegidos {#view-or-edit-protected-documents}

* Para documentos **** PDF, puede utilizar Adobe Acrobat DC, Acrobat Reader y Acrobat Reader Mobile para crear vistas de documentos PDF protegidos. La mayoría de los usuarios ya tienen Acrobat Reader instalado en sus dispositivos, por lo que no necesitan obtener o aprender software adicional para vista de documentos protegidos. También puede descargar Acrobat Reader desde el sitio [web de descargas de](https://get.adobe.com/reader/)Acrobat Reader.

* Para documentos **de** Microsoft Office, necesita Microsoft Office y la extensión de seguridad de Documento de AEM Forms para Microsoft Office. La extensión Seguridad de Documento está disponible como complemento de Microsoft Office. Puede descargar la extensión desde el sitio web de Adobe.

### documentos protegidos por índices {#index-protected-documents}

Los motores de búsqueda de texto completo de Microsoft Windows (servidor de índice de SharePoint) y Adobe Experience Manager (AEM) pueden realizar búsquedas de texto completo en formatos de documento más utilizados, como archivos de texto sin formato, documentos de Microsoft Office y documentos PDF. Puede utilizar los indexadores de seguridad de Documento para habilitar los motores de búsqueda de texto completo para buscar documentos PDF protegidos:

* **Indizador de iFilter:** Puede utilizar el indizador de iFilter para indexar documentos PDF protegidos y activar los motores de búsqueda de texto completo de Microsoft Windows (Desktop Indexing Service y SharePoint Indexserver) para buscar documentos PDF protegidos. Para obtener información detallada, consulte [AEM SharePoint IFilter para Documentos](assets/sharepoint-ifilter-doc-security.pdf)protegidos.

* **AEM Forms Documento Security Indexer:** Puede utilizar el indizador de seguridad de Documento de AEM Forms para indexar documentos PDF protegidos y activar Adobe Experience Manager para buscar documentos PDF protegidos. Los indexadores forman parte de la oferta AEM Forms Documento Security. Estos se incluyen en AEM Forms en instaladores JEE.

