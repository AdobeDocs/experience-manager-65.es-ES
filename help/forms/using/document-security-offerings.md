---
title: Ofertas de seguridad de los documentos
seo-title: Document security offerings
description: Obtenga información sobre las distintas herramientas y características de la seguridad de los documentos de AEM
seo-description: Learn about various tools and features of AEM Document Security
uuid: 24e3275c-cd44-47c0-a6a0-e4cfb1bced8a
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 91e85e86-2361-4d1d-aa73-c3cce46ab1f1
docset: aem65
feature: Document Security
exl-id: d00ae232-b018-44e5-b04b-376d4cd9c6eb
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 99%

---

# Ofertas de seguridad de los documentos{#document-security-offerings}

Adobe Experience Manager Forms Document Security garantiza que solo los usuarios autorizados puedan utilizar sus documentos. Con Document Security, puede distribuir de forma segura cualquier tipo de información guardada en un formato compatible. Los formatos de archivo admitidos son Adobe Portable Document Format (PDF) y Microsoft Word, Excel y PowerPoint.

Puede proteger los documentos mediante políticas. La configuración especificada en una política determina cómo puede el destinatario utilizar un documento al que se aplica la política. Por ejemplo, puede especificar si los destinatarios pueden imprimir o copiar texto, editarlo o agregar firmas y comentarios a documentos protegidos.

Las políticas se almacenan en el servidor de Document Security y se aplican a los documentos a través de la aplicación cliente. Cuando aplica una política a un documento, la configuración de confidencialidad especificada en la política protege la información que contiene el documento. Puede distribuir los documentos protegidos por una política a los destinatarios autorizados por esta.

En el siguiente diagrama se muestra la arquitectura típica de la seguridad de los documentos de AEM Forms:

![Seguridad de documentos: arquitectura recomendada](do-not-localize/document_security_architecture.png)

## Clientes de la seguridad de los documentos {#document-security-clients}

La seguridad de los documentos proporciona varios clientes para proteger, ver y editar documentos protegidos e indexadores para habilitar la búsqueda de texto completo en documentos protegidos. Puede elegir un cliente en función de sus necesidades y las capacidades del cliente.

El servidor de seguridad de los documentos es el componente central mediante el cual la seguridad de los documentos realiza transacciones como la autenticación de usuarios, la administración en tiempo real de directivas y la aplicación de la confidencialidad. El servidor también proporciona un repositorio central para directivas, registros de auditoría y otra información relacionada.

El servidor de seguridad de los documentos proporciona una interfaz basada en Web (página Web) para crear directivas, administrar documentos protegidos por directivas y supervisar eventos asociados a documentos protegidos por directivas. Los administradores también pueden configurar opciones globales como autenticación de usuarios, auditoría y mensajería para usuarios invitados y administrar cuentas de usuario invitadas.

El servidor está incluido en la oferta de complementos de la seguridad de los documentos de AEM Forms Puede ponerse en contacto con el [equipo de ventas](https://www.adobe.com/products/request-consultation/marketing-cloud.html?s_osc=70114000002JNwKAAW&amp;s_iid=70114000002JHs3AAG) de AEM Forms para adquirir el complemento Seguridad de los documentos.

### Proteger documentos {#protect-documents}

La seguridad de los documentos de AEM Forms proporciona varias herramientas para aplicar directivas de seguridad. Puede elegir una herramienta según sus necesidades y especificaciones.

![document-security-offerings](assets/document-security-offerings.png)

Puede utilizar el SDK de seguridad de documentos, Adobe Acrobat, la extensión de seguridad de documentos para Microsoft Office o la biblioteca de protección portátil para aplicar y rastrear las directivas de seguridad:

* **SDK de seguridad de documentos:** el SDK es un cliente con numerosas características. Puede utilizar el SDK de seguridad de los documentos para acceder a la funcionalidad del servidor de documentos, abrir documentos protegidos por directivas y desarrollar extensiones, complementos o aplicaciones personalizados. Por ejemplo, puede desarrollar extensiones para proteger formatos de archivo personalizados o integrar SDK con soluciones de Prevención de pérdida de datos (DLP). Las extensiones, aplicaciones y complementos desarrollados con el SDK de seguridad de los documentos envían documentos al servidor de AEM Forms designado y las directivas se aplican en el servidor. Tenga en cuenta también que el cliente SDK de la seguridad de los documentos (CSDK) de AEM Forms no puede desproteger los documentos protegidos mediante la biblioteca de protección portátil (PPL) y viceversa.

  El SDK de seguridad de los documentos está disponible tanto para Java como para C++. El SDK de Java se incluye en la oferta de seguridad de los documentos de AEM Forms y se instala en la implementación de AEM Forms en JEE. Puede ponerse en contacto con el [equipo de soporte de AEM](https://helpx.adobe.com/es/marketing-cloud/contact-support.html) para obtener el SDK de C++. El SDK de C++ se puede compilar con Microsoft Visual Studio 2013. Puede visitar el sitio [Documentación de la API de seguridad de los documentos](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html) para aprender y utilizar funciones de SDK.

* **Adobe Acrobat:** puede utilizar Adobe Acrobat para aplicar directivas de seguridad a documentos PDF creados con aplicaciones de escritorio populares, como Microsoft Office, exploradores Web o cualquier aplicación que admita la impresión en formato PDF.

  Puede adquirir y descargar Adobe Acrobat desde el [Sitio web de Adobe](https://acrobat.adobe.com/es/es/free-trial-download.html). El artículo de Adobe Acrobat [Configuración de directivas de seguridad para PDF](https://helpx.adobe.com/es/acrobat/using/setting-security-policies-pdfs.html) proporciona información detallada sobre la creación y aplicación de directivas en Adobe Acrobat.

* **Extensión de seguridad de los documentos para Microsoft Office**: puede utilizar la extensión de seguridad de los documentos para Microsoft Office para aplicar directivas predefinidas a los archivos de Microsoft Office desde los programas de Microsoft Office. La extensión garantiza que solo las personas autorizadas puedan utilizar archivos de Microsoft Word, Excel y PowerPoint protegidos por directivas. Solo los usuarios autorizados que tengan el complemento instalado pueden utilizar los archivos protegidos por directivas.

  La extensión de seguridad de los documentos está disponible como complemento de Microsoft Office. Puede ponerse en contacto con el [equipo de soporte de AEM](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html) para obtener la extensión. Más adelante, podrá visitar la ayuda de [Extensión de seguridad de los documentos para Microsoft Office](https://helpx.adobe.com/es/aem-forms/aem-document-security/download-installer.html) para obtener más información sobre la instalación, configuración y uso de la extensión.

* **Biblioteca de protección portátil:** la biblioteca de protección portátil (PPL) protege un documento localmente, sin enviarlo al servidor de AEM Forms. Solo las credenciales de seguridad y los detalles de las directivas viajan por la red. La PPL también le permite limitar el acceso a la recuperación de directivas solo a los usuarios que iniciaron sesión. Puede recuperar directivas con el contexto del usuario que haya iniciado sesión en AEM usuario.

  Junto con lo anterior, la biblioteca de protección adecuada tiene todas las características del SDK de seguridad de los documentos. Puede utilizar el SDK de seguridad de los documentos para acceder a la funcionalidad del servidor de documentos, abrir documentos protegidos por directivas y desarrollar extensiones, complementos o aplicaciones personalizados. Tenga en cuenta también que la biblioteca de protección portátil (PPL) no puede desproteger los documentos protegidos mediante el SDK del cliente de seguridad de los documentos (CSDK) de AEM Forms y viceversa.

  La biblioteca de protección portátil está disponible para los idiomas Java y C++ en versiones de 32 y 64 bits. También está disponible como un paquete OSGi para AEM Forms en OSGi. La PPL de C++ se puede compilar con Microsoft Visual Studio 2013. Si tiene una licencia para el complemento de seguridad de los documentos de AEM Forms, puede ponerse en contacto con el equipo de soporte de [Seguridad de los documentos de AEM Forms](https://helpx.adobe.com/es/marketing-cloud/contact-support.html) para adquirir la biblioteca de protección portátil. Más adelante, puede utilizar la Ayuda de la biblioteca de protección portátil (incluida en la biblioteca) para configurar y utilizar la biblioteca de protección portátil.

### Ver o editar documentos protegidos {#view-or-edit-protected-documents}

* Para **documentos PDF**, puede utilizar Adobe Acrobat DC, Acrobat Reader y Acrobat Reader Mobile para ver documentos PDF protegidos. La mayoría de los usuarios ya tienen Acrobat Reader instalado en sus dispositivos, por lo que no necesitan obtener o aprender software adicional para ver documentos protegidos. También puede descargar Acrobat Reader desde el [Sitio web de descarga de Acrobat Reader](https://get.adobe.com/es/reader/).

* Para **Documentos de Microsoft Office**, necesita la extensión Microsoft Office y seguridad de los documentos de AEM Forms para Microsoft Office. La extensión de seguridad de los documentos está disponible como complemento de Microsoft Office. Puede descargar la extensión desde el sitio web de Adobe.

### Documentos protegidos por índices {#index-protected-documents}

Los motores de búsqueda de texto completo de Microsoft Windows (servidor de índice de SharePoint) y Adobe Experience Manager (AEM) pueden realizar búsquedas de texto completo en formatos de documento usados con más frecuencia, como archivos de texto sin formato, documentos de Microsoft Office y documentos PDF. Puede utilizar los indexadores de seguridad de los documentos para habilitar los motores de búsqueda de texto completo para buscar documentos de PDF protegidos:

* **Indexador iFilter:** puede utilizar el indexador iFilter para indexar documentos PDF protegidos y habilitar los motores de búsqueda de texto completo de Microsoft Windows (servicio de indexación de escritorio y SharePoint Indexserver) para buscar documentos de PDF protegidos. Para obtener información detallada, consulte [IFilter de AEM SharePoint para documentos protegidos](assets/sharepoint-ifilter-doc-security.pdf).

* **Indexador de seguridad de los documentos de AEM Forms:** puede utilizar el indexador de seguridad de los documentos de AEM Forms para indexar documentos PDF protegidos y permitir que Adobe Experience Manager busque documentos PDF protegidos. Los indexadores forman parte de la oferta de seguridad de los documentos de AEM Forms. Estos se incluyen en AEM Forms en instaladores JEE.
