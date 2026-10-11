---
title: Paquete de compatibilidad
description: La instalación del paquete de compatibilidad en AEM Forms 6.5 le permite utilizar los recursos de Administración de correspondencia de AEM Forms 6.4 y versiones anteriores, así como las plantillas y páginas de formularios adaptables obsoletos
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin,User
exl-id: bb16017c-a1bf-40d8-a78d-827c05b7ee2e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 77%
---
# Paquete de compatibilidad{#compatibility-package}

## Información general {#overview}

Interactive Communications es la forma predeterminada y recomendada de crear comunicaciones con los clientes en AEM Forms 6.5. Para seguir usando cartas en AEM Forms 6.5, debes instalar el [paquete de compatibilidad de AEMFD](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html) más reciente.

El paquete de compatibilidad de AEMFD también le permite [usar los siguientes recursos de AEM Forms 6.4, 6.3 y 6.2 en AEM Forms 6.5:](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* Fragmentos de documento
* Cartas
* Diccionarios de datos
* Plantillas y páginas obsoletas de formularios adaptables

Para obtener más información, consulte [Recursos compatibles con AEM Forms 6.5 mediante la instalación del paquete Compatibilidad](../../forms/using/compatibility-package.md#assetsmadecompatible).

## Agregue compatibilidad para los recursos de AEM Forms 6.4, 6.3 y 6.2 en AEM Forms 6.5 {#add-support-for-aem-forms-and-assets-in-aem-forms}

Después de realizar una actualización, haga lo siguiente para instalar el paquete de compatibilidad de AEMFD y hacer que sus recursos sean compatibles con la versión 6.5:

Asegúrese de que tiene preinstalado el [paquete de compatibilidad de AEM](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html).

1. Instale la última versión 6.5 del [paquete de compatibilidad](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html).

   Para obtener más información sobre cómo cargar e instalar el paquete, consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md).

1. Una vez estabilizados los registros, reinicie el servidor.
1. Utilice la utilidad de migración para hacer que los recursos sean compatibles con la versión 6.5.

   >[!NOTE]
   >
   > Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.

   Para obtener más información, consulte [utilidad de migración](../../forms/using/migration-utility.md).

## Recursos compatibles con AEM Forms 6.5 mediante la instalación del paquete Compatibilidad {#assetsmadecompatible}

Al instalar el paquete Compatibilidad, puede hacer que los siguientes recursos y plantillas sean compatibles con AEM Forms 6.5:

* Recursos de Administración de correspondencia de AEM 6.4 y anteriores:

  * [Cartas](../../forms/using/create-letter.md)
  * [Diccionarios de datos](/help/forms/using/data-dictionary.md)
  * Fragmentos de documento

* Plantillas de formularios adaptables obsoletas:

  * /libs/fd/af/templates/blankTemplate2
  * /libs/fd/af/templates/simpleEnrollmentTemplate
  * /libs/fd/af/templates/simpleEnrollmentTemplate2
  * /libs/fd/af/templates/surveyTemplate
  * /libs/fd/af/templates/surveyTemplate2
  * /libs/fd/af/templates/tabbedEnrollmentTemplate
  * /libs/fd/af/templates/tabbedEnrollmentTemplate2
  * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
  * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* Páginas obsoletas de formularios adaptables:

  * /libs/fd/af/components/page/survey
  * /libs/fd/af/components/page/tabbedenrollment
  * /libs/fd/afaddon/components/page/advancedenrollment
