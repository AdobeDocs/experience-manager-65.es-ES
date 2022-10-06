---
title: Paquete de compatibilidad
seo-title: Compatibility Package
description: La instalación del paquete de compatibilidad en AEM Forms 6.5 le permite utilizar los recursos de gestión de correspondencia de AEM Forms 6.4 y versiones anteriores, así como las plantillas y páginas de formularios adaptables obsoletos
seo-description: Installing the Compatibility package on AEM Forms 6.4 allows you to use the Correspondence Management assets from AEM Forms 6.4 and deprecated adaptive forms templates and pages
uuid: b49633d6-2cb3-422c-a314-25f3b8a37b7f
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 73e8ccc6-f857-493e-b6e3-878f93e2a356
docset: aem65
role: Admin
exl-id: bb16017c-a1bf-40d8-a78d-827c05b7ee2e
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 6%

---

# Paquete de compatibilidad{#compatibility-package}

## Información general {#overview}

La comunicación interactiva es el método predeterminado y recomendado para crear comunicaciones con los clientes en AEM Forms 6.5. Para seguir utilizando letras en AEM Forms 6.5, debe instalar la última [Paquete de compatibilidad de AEMFD](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html).

El paquete de compatibilidad con AEMFD también le permite: [utilice los siguientes recursos de AEM Forms 6.4, 6.3 y 6.2 en AEM Forms 6.5:](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* Fragmentos de documento
* Cartas
* Diccionarios de datos
* Plantillas y páginas obsoletas de formularios adaptables

Para obtener más información, consulte [Recursos compatibles con AEM Forms 6.5 mediante la instalación del paquete Compatibilidad](../../forms/using/compatibility-package.md#assetsmadecompatible).

## Añada compatibilidad con los recursos de AEM Forms 6.4, 6.3 y 6.2 en AEM Forms 6.5 {#add-support-for-aem-forms-and-assets-in-aem-forms}

Después de realizar una actualización, haga lo siguiente para instalar el paquete de compatibilidad con AEMFD y hacer que sus recursos sean compatibles con la versión 6.5:

Asegúrese de que [AEM Paquete de compatibilidad](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) preinstalado.

1. Instale la última versión 6.5 [Paquete de compatibilidad](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html).

   Para obtener más información sobre cómo cargar e instalar el paquete, consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md).

1. Una vez estabilizados los registros, reinicie el servidor.
1. Utilice la utilidad de migración para hacer que los recursos sean compatibles con la versión 6.5.

   Para obtener más información, consulte [utilidad de migración](../../forms/using/migration-utility.md).

## Recursos compatibles con AEM Forms 6.5 mediante la instalación del paquete Compatibilidad {#assetsmadecompatible}

Al instalar el paquete Compatibilidad, puede hacer que los siguientes recursos y plantillas sean compatibles con AEM Forms 6.5:

* Activos de gestión de correspondencia de AEM 6.4 y anteriores:

   * [Cartas](../../forms/using/create-letter.md)
   * [Diccionarios de datos](/help/forms/using/data-dictionary.md)
   * Fragmentos de documento

* Plantillas de formularios adaptables en desuso:

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnscriptionsTemplate
   * /libs/fd/af/templates/simpleEnscriptionsTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnscriptionsTemplate
   * /libs/fd/af/templates/tabbedEnscriptionsTemplate2
   * /libs/fd/afaddon/templates/advancedEnsubscriptionTemplate
   * /libs/fd/afaddon/templates/advancedEnSubscriptionTemplate2

* Páginas en desuso de formularios adaptables:

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedensubscription
   * /libs/fd/afaddon/components/page/Advancedensubscription
