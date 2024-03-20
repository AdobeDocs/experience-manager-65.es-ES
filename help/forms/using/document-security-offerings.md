---
title: Ofertas de seguridad de los documentos
description: AEM Obtenga información acerca de las distintas herramientas y características de Seguridad de documentos de.
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Document Security
exl-id: d00ae232-b018-44e5-b04b-376d4cd9c6eb
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 39%

---

# Ofertas de seguridad de los documentos{#document-security-offerings}

Adobe Experience Manager Forms Document Security garantiza que solo los usuarios autorizados puedan utilizar sus documentos. Con Document Security, puede distribuir de forma segura cualquier tipo de información guardada en un formato compatible. Los formatos de archivo admitidos son Adobe Portable Document Format (PDF) y Microsoft® Word, Excel y PowerPoint.

Puede proteger los documentos mediante políticas. La configuración de confidencialidad especificada en una política determina cómo puede un destinatario utilizar un documento al que se aplica la política. Por ejemplo, puede especificar si los destinatarios pueden imprimir o copiar texto, editarlo o agregar firmas y comentarios a documentos protegidos.

Las directivas se almacenan en el servidor de Document Security y se aplican a los documentos a través de la aplicación cliente. Cuando aplica una política a un documento, la configuración de confidencialidad especificada en la política protege la información que contiene el documento. Puede distribuir los documentos protegidos por una política a los destinatarios autorizados por esta.

En el siguiente diagrama se muestra la arquitectura típica de la seguridad de los documentos de AEM Forms:

![Seguridad de documentos: arquitectura recomendada](do-not-localize/document_security_architecture.png)

## Clientes de la seguridad de los documentos {#document-security-clients}

La seguridad de los documentos proporciona varios clientes para proteger, ver y editar documentos protegidos e indexadores para habilitar la búsqueda de texto completo en documentos protegidos. Puede elegir un cliente en función de sus necesidades y las capacidades del cliente.

El servidor de seguridad de los documentos es el componente central mediante el cual la seguridad de los documentos realiza transacciones como la autenticación de usuarios, la administración en tiempo real de directivas y la aplicación de la confidencialidad. El servidor también proporciona un repositorio central para directivas, registros de auditoría y otra información relacionada.

El servidor de seguridad de los documentos proporciona una interfaz basada en Web (página Web) para crear directivas, administrar documentos protegidos por directivas y supervisar eventos asociados a documentos protegidos por directivas. Los administradores también pueden configurar opciones globales como autenticación de usuarios, auditoría y mensajería para usuarios invitados y administrar cuentas de usuario invitadas.

El servidor está incluido en la oferta de complementos de seguridad de los documentos de AEM Forms. Puede ponerse en contacto con el [equipo de ventas](https://business.adobe.com/request-consultation/experience-cloud.html?s_osc=70114000002JNwKAAW&amp;s_iid=70114000002JHs3AAG) de AEM Forms para adquirir el complemento Seguridad de los documentos.

### Proteger documentos {#protect-documents}

La seguridad de los documentos de AEM Forms proporciona varias herramientas para aplicar directivas de seguridad. Puede elegir una herramienta según sus necesidades y especificaciones.

![document-security-offerings](assets/document-security-offerings.png)

Puede utilizar el SDK de seguridad de documentos, Adobe Acrobat, la extensión de seguridad de documentos para Microsoft® Office o la biblioteca de protección portátil para aplicar y rastrear las directivas de seguridad:

* **SDK de seguridad de documentos:** el SDK es un cliente con numerosas características. Puede utilizar el SDK de seguridad de los documentos para acceder a la funcionalidad del servidor de documentos, abrir documentos protegidos por directivas y desarrollar extensiones, complementos o aplicaciones personalizados. Por ejemplo, puede desarrollar extensiones para proteger formatos de archivo personalizados o integrar el SDK con soluciones de Prevención de pérdida de datos (DLP). Las extensiones, aplicaciones y complementos desarrollados con el SDK de seguridad de los documentos para enviar documentos al servidor de AEM Forms designado y las directivas se aplican en el servidor. El SDK del cliente de seguridad de los documentos (CSDK) de AEM Forms no puede desproteger los documentos protegidos mediante la biblioteca de protección portátil (PPL) y a la inversa.

  El SDK de seguridad de los documentos está disponible para Java™ y C++. El SDK de Java™ se incluye en la oferta de seguridad de los documentos de AEM Forms AEM y se instala en la implementación de formularios en JEE de la aplicación de la seguridad de los documentos de la plataforma de datos de la plataforma de JEE. Contacto [AEM Atención al cliente](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home&amp;lang=es#support) para adquirir el SDK de C++. El SDK de C++ se puede compilar con Microsoft® Visual Studio 2013. Visite la [Documentación de API de Document Security](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html) sitio donde puede aprender y utilizar funciones del SDK.

* **Adobe Acrobat:** Puede utilizar Adobe Acrobat para aplicar directivas de seguridad a documentos de PDF creados con aplicaciones de  populares, como Microsoft® Office, exploradores Web o cualquier aplicación que admita la impresión en formato de PDF.

  Puede adquirir y descargar Adobe Acrobat desde el [Sitio web de Adobe](https://www.adobe.com/acrobat/free-trial-download.html). El artículo de Adobe Acrobat [Configuración de directivas de seguridad para PDF](https://helpx.adobe.com/es/acrobat/using/setting-security-policies-pdfs.html) proporciona información detallada sobre la creación y aplicación de directivas en Adobe Acrobat.

* **Extensión de seguridad de los documentos para Microsoft® Office**: puede utilizar la extensión de Document Security para Microsoft® Office para aplicar directivas predefinidas a los archivos de Microsoft® Office desde los programas de Microsoft® Office. La extensión garantiza que solo las personas autorizadas puedan utilizar archivos de Microsoft® Word, Excel y PowerPoint protegidos por directivas. Solo los usuarios autorizados que tengan el complemento instalado pueden utilizar los archivos protegidos por directivas.

  La extensión de Document Security está disponible como complemento de Microsoft® Office. Contacto [AEM Atención al cliente](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html) para obtener la extensión. Más adelante, puede visitar [Extensión de seguridad de los documentos para Microsoft® Office](https://experienceleague.adobe.com/docs/experience-manager-document-security/using/download-installer.html?lang=es) ayuda para obtener más información sobre la instalación, configuración y uso de la extensión de.

* **Biblioteca de protección portátil:** La PPL protege un documento localmente, sin enviarlo al servidor de AEM Forms. Solo las credenciales de seguridad y los detalles de las directivas viajan por la red. La PPL también le permite limitar el acceso a la recuperación de directivas solo a los usuarios que iniciaron sesión. Puede recuperar directivas con el contexto del usuario que haya iniciado sesión en AEM usuario.

  Junto con lo anterior, la PPL tiene todas las características del SDK de seguridad de los documentos. Puede utilizar el SDK de seguridad de los documentos para acceder a la funcionalidad del servidor de documentos, abrir documentos protegidos por directivas y desarrollar extensiones, complementos o aplicaciones personalizados. La PPL no puede desproteger los documentos protegidos mediante el SDK del cliente de seguridad de los documentos (CSDK) de AEM Forms y a la inversa.

  La PPL está disponible para los idiomas Java™ y C++ en versiones de 32 y 64 bits. También está disponible como un paquete OSGi para AEM Forms en OSGi. La PPL de C++ se puede compilar con Microsoft® Visual Studio 2013. Si tiene licencia del complemento de seguridad de los documentos de AEM Forms, puede ponerse en contacto con el [AEM Forms Document Security](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home&amp;lang=es#support) equipo de apoyo para obtener la PPL. Más adelante, puede utilizar la Ayuda de PPL (incluida en la biblioteca) para configurar y utilizar la PPL.

### Ver o editar documentos protegidos {#view-or-edit-protected-documents}

* Para **documentos PDF**, puede utilizar Adobe Acrobat DC, Acrobat Reader y Acrobat Reader Mobile para ver documentos PDF protegidos. La mayoría de los usuarios ya tienen Acrobat Reader instalado en sus dispositivos, por lo que no necesitan obtener o aprender software adicional para ver documentos protegidos. También puede descargar Acrobat Reader desde el [Sitio web de descarga de Acrobat Reader](https://get.adobe.com/es/reader/).

* Para **Documentos de Microsoft® Office**, necesita la extensión de Microsoft® Office y AEM Forms Document Security para Microsoft® Office. La extensión de Document Security está disponible como complemento de Microsoft® Office. Puede descargar la extensión desde el sitio web del Adobe.

### Documentos protegidos por índices {#index-protected-documents}

Los motores de búsqueda de texto completo de Microsoft® Windows (servidor de índice de SharePoint) y Adobe Experience Manager AEM () pueden realizar búsquedas de texto completo en formatos de documento usados con más frecuencia, como archivos de texto sin formato, documentos de Microsoft® Office y documentos de PDF. Puede utilizar los indexadores de seguridad de los documentos para habilitar los motores de búsqueda de texto completo para buscar documentos de PDF protegidos:

* **Indexador iFilter:** Puede utilizar el indexador iFilter para indexar documentos de PDF protegidos y habilitar los motores de búsqueda de texto completo de Microsoft® Windows (servicio de indexación de escritorio y servidor de índice de SharePoint) para buscar documentos de PDF protegidos. Para obtener información detallada, consulte [AEM IFilter de SharePoint para documentos protegidos](assets/sharepoint-ifilter-doc-security.pdf).

* **Indexador de seguridad de los documentos de AEM Forms:** puede utilizar el indexador de seguridad de los documentos de AEM Forms para indexar documentos PDF protegidos y permitir que Adobe Experience Manager busque documentos PDF protegidos. Los indexadores forman parte de la oferta de AEM Forms Document Security. Estos se incluyen en AEM Forms en instaladores JEE.
