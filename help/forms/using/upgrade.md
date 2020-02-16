---
title: Actualización a AEM 6.5 Forms
seo-title: Actualización a AEM 6.5 Forms
description: Puede realizar una actualización directa de AEM 6.3 Forms y AEM 6.4 Forms a AEM 6.5 Forms.
seo-description: Puede realizar una actualización directa de AEM 6.3 Forms y AEM 6.4 Forms a AEM 6.5 Forms.
uuid: 7a38cd72-2d01-4af7-b6a3-00dc34c4f02b
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f89921ef-c638-4a07-88d5-3dd8614c5166
docset: aem65
translation-type: tm+mt
source-git-commit: 43fe9540a3a29ae86f48756c77001c0a4b8ea3e4

---


# Actualización a AEM 6.5 Forms{#upgrade-to-aem-forms}

AEM 6.5 Forms incluye varias funciones y mejoras nuevas que optimizan la creación, la gestión y la experiencia del usuario con los formularios y las correspondencias. Para obtener más información sobre las nuevas funciones y mejoras de AEM 6.5 Forms, consulte el documento [de resumen de](../../forms/using/whats-new.md)nuevas funciones.

Puede actualizar la instalación existente de LiveCycle o AEM Forms para obtener nuevas funciones y mejoras ofrecidas en AEM 6.5 Forms, manteniendo intactos los datos, procesos y recursos existentes. Al actualizar, también se conservan los metadatos y el estado de los procesos. Puede elegir una ruta de actualización para comenzar con la actualización.

En el diagrama siguiente se muestran las rutas de actualización disponibles para AEM Forms en OSGi:

![](do-not-localize/osgi-upgrade-path.png)

Puede realizar una actualización directa desde:

* AEM 6.3 Forms en OSGi
* AEM 6.4 Forms en OSGi

También puede realizar una actualización de varios saltos desde

* AEM 6.0 Forms en OSGi
* AEM 6.1 Forms en OSGi
* AEM 6.2 Forms en OSGi

En el diagrama siguiente se muestran las rutas de actualización disponibles para AEM Forms en JEE:

![](do-not-localize/jee-upgrade-6-5.png)

Puede realizar una actualización directa desde:

* AEM 6.3 Forms en JEE
* AEM 6.3 Forms en JEE

También puede realizar una actualización de varios saltos desde

* LiveCycle ES2
* LiveCycle ES3
* LiveCycle ES4 SP1
* AEM 6.0 Forms en JEE
* AEM 6.1 Forms en JEE
* AEM 6.2 Forms en JEE

<!--
[Work in Progress]

Migration involves moving only assets (PDF, XDP, images, adaptive forms, correspondence management assets) from one server to another - processes (LCA), settings, configurations, and a few other pieces of metadata are not migrated. Perform the following steps to migrate to AEM 6.3 Forms:

1. Set up a fresh environment of [AEM 6.3 Forms](https://adobe.com/go/learn_aemforms_documentation_63).
1. Move XDP or other compatible assets to the freshly set instance. For detailed instructions, see [Importing and exporting assets to AEM Forms](../../forms/using/import-export-forms-templates.md). [
   ](../../forms/using/import-export-forms-templates.md)
1. Build the required services, if any.

   For example, if you are using AEM Forms on JEE Document Services, changes are required in the code to use document services available in AEM Forms on OSGi.

1. Perform post-installation activities:

    * **Run Migration Utility**

      The migration utility makes the adaptive forms and correspondence management assets of earlier versions compatible with AEM 6.3 forms. You can download the utility from AEM package share. For step-by-step information to configure and use the migration utility, see [migration utility](../../forms/using/migration-utility.md) documentation.

    * **Reconfigure Adobe Sign**

      If you had Adobe Sign configured in the previous version of AEM Forms, then reconfigure Adobe Sign from AEM Cloud services. For more details, see [Integrate Adobe Sign with AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

      Moreover, AEM 6.3 Forms release has introduced many new Adobe Sign features. For step-by-step information to use Adobe Sign, see [Using Adobe Sign in an adaptive form](../../forms/using/working-with-adobe-sign.md).

    * **Reconfigure analytics and reports**

      In AEM 6.3 Forms, traffic variable for source and success event for impression are not available. So, when you upgrade to AEM 6.3 Forms, AEM Forms stops sending data to Adobe Analytics server and analytics reports for adaptive forms are not available. Moreover, AEM 6.3 Forms introduces traffic variable for the version of form analytics and success event for the amount of time spent on a field. So, reconfigure analytics and reports for your AEM Forms environment. For detailed steps, see [Configuring analytics and reports](../../forms/using/configure-analytics-forms-documents.md).

      Methods to calculate average fill time for forms and average read time for have changed. So, when you upgrade to AEM 6.3 forms, older data (data from previous AEM Forms release) for these metrics is available only in Adobe Analytics. It is not visible in AEM Forms analytics reports. For these metrics, AEM Forms analytics reports display data which is captured after performing the upgrade.
      
      -->
