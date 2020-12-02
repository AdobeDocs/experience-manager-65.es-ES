---
title: Visión general del servicio de salida
seo-title: Visión general del servicio de salida
description: Output permite combinar datos de formulario XML con un diseño de formulario creado en Designer para crear una secuencia de salida de documento en varios formatos.
seo-description: Output permite combinar datos de formulario XML con un diseño de formulario creado en Designer para crear una secuencia de salida de documento en varios formatos.
uuid: 7890b0a6-bae5-4ad5-ae41-503b988ba3da
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5a96f5ea-6fe3-44b1-b314-14097b9e9c01
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Visión general del servicio de salida {#overview-of-output-service}

Output permite combinar datos de formulario XML con un diseño de formulario creado en Designer para crear una secuencia de salida de documento en varios formatos. El flujo de salida se puede enviar a una impresora de red, una impresora local o un archivo de disco

Puede utilizar la página Salida en la consola de administración para administrar el servicio Output. La configuración que configure se utiliza en tiempo de ejecución cuando la configuración equivalente no se especificó mediante la API de formularios AEM. La configuración que se realiza mediante el SDK de formularios AEM anula la configuración establecida mediante la consola de administración.

Para obtener información adicional sobre el servicio Output, consulte [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_61).

En las páginas Salida de la consola de administración, puede realizar varias tareas:

* Especifique conjuntos de caracteres para la internacionalización. (Consulte [Cambio del conjunto de caracteres](/help/forms/using/admin-help/change-character-set.md#change-the-character-set).)
* Especifique rutas absolutas y relativas para direcciones URL, URI, XCI y ubicaciones de archivos. (Consulte [Especificar ubicaciones de archivos para Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)
* Configurar tamaños y directivas de caché. (Consulte [Especificación del modo de caché](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) y [Configuración de la configuración de caché](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings).)
* Publique fuentes en el servidor de aplicaciones. (Consulte [Disponibilidad de fuentes](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available)).
* Especifique las fuentes que desea incrustar. (Consulte [Especificar fuentes para incrustar](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed).)
* Especifique las opciones de configuración XCI. (Consulte [Especificación de opciones de configuración XCI](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options)).
* Especifique la configuración de seguridad. (Consulte [Especificar configuración de seguridad](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings).)

Después de cambiar la configuración, haga clic en Guardar para aplicarla a Output. No es necesario reiniciar el servidor para que los cambios surtan efecto, pero es posible que tenga que reiniciar el servicio Output al configurar la configuración de la caché.
