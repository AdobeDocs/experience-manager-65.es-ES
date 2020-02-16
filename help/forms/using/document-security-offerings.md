---
title: Ofertas de seguridad de documentos
seo-title: Ofertas de seguridad de documentos
description: Obtenga información sobre las distintas herramientas y funciones de AEM Document Security
seo-description: Obtenga información sobre las distintas herramientas y funciones de AEM Document Security
uuid: 24e3275c-cd44-47c0-a6a0-e4cfb1bced8a
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 91e85e86-2361-4d1d-aa73-c3cce46ab1f1
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# Ofertas de seguridad de documentos{#document-security-offerings}

La seguridad de documentos de Adobe Experience Manager Forms garantiza que solo los usuarios autorizados puedan utilizar sus documentos. Con la seguridad de los documentos, puede distribuir con seguridad cualquier información que haya guardado en un formato compatible. Los formatos de archivo admitidos son Adobe Portable Document Format (PDF) y Microsoft Word, Excel y PowerPoint.

Puede proteger documentos mediante políticas. La configuración de confidencialidad que especifique en una política determinará cómo puede un destinatario utilizar un documento al que aplique la política. Por ejemplo, puede especificar si los destinatarios pueden imprimir o copiar texto, editar texto o agregar firmas y comentarios a documentos protegidos.

Las directivas se almacenan en el servidor de Document Security; las políticas se aplican a los documentos a través de la aplicación cliente. Cuando se aplica una política a un documento, la configuración de confidencialidad especificada en la política protege la información que contiene el documento. Puede distribuir el documento protegido por una política a los destinatarios autorizados por la política.

En el diagrama siguiente se muestra la arquitectura típica de AEM Forms Document Security:

![Document Security: arquitectura recomendada](do-not-localize/document_security_architecture.png)

## Clientes de Document Security {#document-security-clients}

Document Security proporciona varios clientes para proteger documentos, ver y editar documentos protegidos e indexadores para permitir la búsqueda de texto completo en documentos protegidos. Puede elegir un cliente según sus necesidades y las capacidades del cliente.

Document Security Server es el componente central mediante el cual Document Security realiza transacciones como autenticación de usuarios, administración en tiempo real de políticas y aplicación de la confidencialidad. El servidor también proporciona un repositorio central para directivas, registros de auditoría y otra información relacionada.

El servidor de Document Security proporciona una interfaz basada en Web (página Web) para crear políticas, administrar documentos protegidos por políticas y supervisar eventos asociados a documentos protegidos por políticas. Los administradores también pueden configurar opciones globales como autenticación de usuarios, auditoría y mensajería para los usuarios invitados, y administrar las cuentas de usuario invitadas.

El servidor se incluye en la oferta del complemento AEM Forms Document Security. Puede ponerse en contacto con el equipo [de](https://www.adobe.com/products/request-consultation/marketing-cloud.html?s_osc=70114000002JNwKAAW&s_iid=70114000002JHs3AAG) ventas de AEM Forms para adquirir el complemento Document Security.

### Proteger documentos {#protect-documents}

AEM Forms Document Security proporciona varias herramientas para aplicar políticas de seguridad. Puede elegir una herramienta según sus necesidades y especificaciones.

![document-security-options](assets/document-security-offerings.png)

Puede utilizar Document Security SDK, Adobe Acrobat, Document Security Extension for Microsoft Office o Portable Protection Library para aplicar y realizar el seguimiento de las políticas de seguridad:

* **** SDK de Document Security: El SDK es un cliente con muchas funciones. Puede utilizar el SDK de Document Security para acceder a la funcionalidad del servidor de documentos, abrir documentos protegidos por políticas y desarrollar extensiones, complementos o aplicaciones personalizados. Por ejemplo, puede desarrollar extensiones para proteger formatos de archivo personalizados o integrar SDK con soluciones de prevención de pérdida de datos (DLP). Las extensiones, aplicaciones y complementos desarrollados con el SDK de Document Security envían documentos al servidor designado de AEM Forms y las políticas se aplican en el servidor. Tenga en cuenta también que el SDK de cliente de seguridad de documentos (CSDK) de AEM Forms no puede desproteger los documentos protegidos con la biblioteca de protección portátil (PPL) y viceversa.

   El SDK de Document Security está disponible para Java y C++. El SDK de Java se incluye en la oferta de AEM Forms Document Security y se instala al implementar formularios AEM en JEE. Puede ponerse en contacto con el equipo [de asistencia de](https://helpx.adobe.com/marketing-cloud/contact-support.html) AEM para adquirir el SDK de C++. El SDK de C++ se puede compilar con Microsoft Visual Studio 2013. Puede visitar el sitio de documentación [de la API de](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html) Document Security para conocer y utilizar las funciones del SDK.

* **** Adobe Acrobat: Puede utilizar Adobe Acrobat para aplicar políticas de seguridad a documentos PDF creados con aplicaciones de escritorio conocidas, como Microsoft Office, navegadores web o cualquier aplicación que admita la impresión en formato PDF.

   Puede comprar y descargar Adobe Acrobat desde el sitio web de [Adobe](https://acrobat.adobe.com/us/en/free-trial-download.html). El artículo [Configuración de políticas de seguridad de Adobe Acrobat para archivos PDF](https://helpx.adobe.com/acrobat/using/setting-security-policies-pdfs.html) proporciona información detallada sobre la creación y aplicación de políticas en Adobe Acrobat.

* **Document Security Extension for Microsoft Office**: Puede utilizar Document Security Extension for Microsoft Office para aplicar políticas predefinidas a sus archivos de Microsoft Office desde los programas de Microsoft Office. La extensión garantiza que solo las personas autorizadas puedan utilizar archivos de Microsoft Word, Excel y PowerPoint protegidos por políticas. Solo los usuarios autorizados que tengan instalado el complemento pueden utilizar los archivos protegidos por políticas.

   La extensión de Document Security está disponible como complemento de Microsoft Office. Puede ponerse en contacto con el equipo [de asistencia de](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html) AEM para obtener la extensión. Posteriormente, puede visitar la ayuda de [Document Security Extension for Microsoft Office](https://helpx.adobe.com/aem-forms/aem-document-security/aem-document-security-extension-help.html) para obtener información sobre la instalación, configuración y uso de la extensión.

* **** Biblioteca de protección portátil: La biblioteca de protección portátil (PPL) protege un documento localmente sin enviarlo al servidor de AEM Forms. Sólo las credenciales de seguridad y los detalles de las políticas se desplazan por la red. PPL también le permite limitar el acceso a la recuperación de directivas solo a los usuarios que iniciaron sesión. Puede recuperar directivas con el contexto del usuario que ha iniciado sesión en AEM.

   Junto con lo anterior, la biblioteca de protección adecuada tiene todas las funciones del SDK de Document Security. Puede utilizar el SDK de Document Security para acceder a la funcionalidad del servidor de documentos, abrir documentos protegidos por políticas y desarrollar extensiones, complementos o aplicaciones personalizados. Tenga en cuenta también que la biblioteca de protección portátil (PPL) no puede desproteger los documentos protegidos con el SDK de cliente de seguridad de documentos (CSDK) de AEM Forms y viceversa.

   La biblioteca de protección portátil está disponible para los idiomas Java y C++ en las versiones de 32 y 64 bits. También está disponible como paquete OSGi para AEM Forms en OSGi. La PPL de C++ se puede compilar con Microsoft Visual Studio 2013. Si tiene licencia del complemento AEM Forms Document Security, puede ponerse en contacto con el equipo de asistencia de [AEM Forms Document Security](https://helpx.adobe.com/marketing-cloud/contact-support.html) para adquirir la biblioteca de protección portátil. Más adelante, puede utilizar la Ayuda de la biblioteca de protección portátil (incluida en la biblioteca) para configurar y utilizar la biblioteca de protección portátil.

### Visualización o edición de documentos protegidos {#view-or-edit-protected-documents}

* Para documentos **** PDF, puede utilizar Adobe Acrobat DC, Acrobat Reader y Acrobat Reader Mobile para ver documentos PDF protegidos. La mayoría de los usuarios ya tienen Acrobat Reader instalado en sus dispositivos, por lo que no necesitan obtener o aprender software adicional para ver documentos protegidos. También puede descargar Acrobat Reader desde el sitio [web de descargas de](https://get.adobe.com/reader/)Acrobat Reader.

* Para documentos **de** Microsoft Office, necesita Microsoft Office y la extensión de AEM Forms Document Security para Microsoft Office. La extensión de Document Security está disponible como complemento de Microsoft Office. Puede descargar la extensión desde el sitio web de Adobe.

### Documentos protegidos por índices {#index-protected-documents}

Los motores de búsqueda de texto completo de Microsoft Windows (servidor de índice de SharePoint) y Adobe Experience Manager (AEM) pueden realizar búsquedas de texto completo en formatos de documento de uso común, como archivos de texto sin formato, documentos de Microsoft Office y documentos PDF. Puede utilizar los indexadores de Document Security para habilitar los motores de búsqueda de texto completo para buscar documentos PDF protegidos:

* **** Indizador de iFilter: Puede utilizar el indizador de iFilter para indexar documentos PDF protegidos y activar los motores de búsqueda de texto completo de Microsoft Windows (Desktop Indexing Service y SharePoint Indexserver) para buscar documentos PDF protegidos. Para obtener información detallada, consulte [AEM SharePoint IFilter para documentos](assets/sharepoint-ifilter-doc-security.pdf)protegidos.

* **** AEM Forms Document Security Indexer: Puede utilizar el indizador de AEM Forms Document Security para indexar documentos PDF protegidos y activar Adobe Experience Manager para buscar documentos PDF protegidos. Los indexadores forman parte de la oferta de AEM Forms Document Security. Estos se incluyen en AEM Forms en instaladores JEE.

