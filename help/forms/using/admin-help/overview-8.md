---
title: Descripción general del servicio de salida
seo-title: Overview of output service
description: La salida permite combinar los datos de formulario XML con un diseño de formulario creado en Designer para crear una secuencia de salida de documento en varios formatos.
seo-description: Output lets you merge XML form data with a form design created in Designer to create a document output stream in various formats.
uuid: 7890b0a6-bae5-4ad5-ae41-503b988ba3da
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5a96f5ea-6fe3-44b1-b314-14097b9e9c01
exl-id: e99b72d0-fbd5-4150-a225-1a91ad4c5867
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 7%

---

# Descripción general del servicio de salida {#overview-of-output-service}

La salida permite combinar los datos de formulario XML con un diseño de formulario creado en Designer para crear una secuencia de salida de documento en varios formatos. La secuencia de salida se puede enviar a una impresora de red, a una impresora local o a un archivo de disco

Puede utilizar la página Salida en la consola de administración para administrar el servicio Salida. AEM La configuración que configure se utiliza en tiempo de ejecución cuando la configuración equivalente no se especificó a través de la API de formularios en la que se utiliza el formulario de la. AEM La configuración realizada a través del SDK de formularios en la aplicación de la anula la configuración establecida mediante la consola de administración.

Para obtener más información sobre el servicio Output, consulte [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_61).

En las páginas Salida de la consola de administración, puede realizar varias tareas:

* Especifique conjuntos de caracteres para la internacionalización. (Consulte [Cambiar el conjunto de caracteres](/help/forms/using/admin-help/change-character-set.md#change-the-character-set).)
* Especifique rutas absolutas y relativas para direcciones URL, URI, XCI y ubicaciones de archivos. (Consulte [Especificar ubicaciones de archivos para la salida](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)
* Configure los tamaños y las políticas de la caché. (Consulte [Especificación del modo de caché](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) y [Configuración de caché](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings).)
* Hacer que las fuentes estén disponibles en el servidor de aplicaciones. (Consulte [Hacer que las fuentes estén disponibles](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available).)
* Especificar fuentes para incrustar. (Consulte [Especificar fuentes para incrustar](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed).)
* Especificar las opciones de configuración XCI. (Consulte [Especificar las opciones de configuración XCI](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options).)
* Especificar la configuración de seguridad. (Consulte [Especificar la configuración de seguridad](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings).)

Después de cambiar la configuración, haga clic en Save para aplicarla a Output. No es necesario reiniciar el servidor para que los cambios surtan efecto, pero es posible que tenga que reiniciar el Servicio de salida al configurar la caché.
