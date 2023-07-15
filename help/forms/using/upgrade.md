---
title: Actualizar a AEM 6.5 Forms
seo-title: Upgrade to AEM 6.5 Forms
description: Puede realizar una actualización directa de AEM 6.3 Forms y AEM 6.4 Forms a AEM 6.5 Forms.
seo-description: You can perform a direct upgrade from AEM 6.3 Forms and AEM 6.4 Forms to AEM 6.5 Forms.
uuid: 7a38cd72-2d01-4af7-b6a3-00dc34c4f02b
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f89921ef-c638-4a07-88d5-3dd8614c5166
docset: aem65
role: Admin
exl-id: 2fc8abec-8ba6-40b7-bbb1-4288eeea7c86
source-git-commit: 762e918a2c65898fc518f131d44421fb82ce4d6f
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 97%

---

# Actualizar a AEM 6.5 Forms{#upgrade-to-aem-forms}

AEM 6.5 Forms incluye varias funciones y mejoras nuevas que optimizan la creación, administración y experiencia del usuario con formularios y correspondencia. Para obtener más información sobre las nuevas funciones y mejoras de AEM 6.5 Forms, consulte [Documento de resumen de las nuevas funciones](../../forms/using/whats-new.md).

Puede actualizar su LiveCycle existente o la instalación de AEM Forms para obtener nuevas funciones y mejoras que se ofrecen en AEM 6.5 Forms, mientras mantiene intactos los datos, procesos y recursos existentes. En la actualización, también se conservan los metadatos y el estado de los procesos. Puede elegir una ruta de actualización para empezar con la actualización.

El diagrama siguiente muestra las rutas de actualización disponibles para AEM Forms en OSGi:

![Flujo de actualización de OSGi](do-not-localize/osgi-upgrade-path.png)

Puede realizar una actualización directa desde:

* AEM 6.3 Forms en OSGi
* AEM 6.4 Forms en OSGi

También puede realizar una actualización multisalto desde

* AEM 6.0 Forms en OSGi
* AEM 6.1 Forms en OSGi
* AEM 6.2 Forms en OSGi

El diagrama siguiente muestra las rutas de actualización disponibles para AEM Forms en JEE:

![Actualización de JEE 6.5](do-not-localize/jee-upgrade-6-5.png)

Puede realizar una actualización directa desde:

* AEM 6.3 Forms en JEE
* AEM 6.4 Forms en JEE
* AEM 6.5.x.x Forms en JEE

También puede realizar una actualización multisalto desde

* LiveCycle ES2
* LiveCycle ES3
* LiveCycle ES4 SP1
* AEM 6.0 Forms en JEE
* AEM 6.1 Forms en JEE
* AEM 6.2 Forms en JEE

AEM 6.5.12.0 Forms en JEE proporciona dos tipos de instaladores: [Programa de instalación completo](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) y [Programa de instalación de parches](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).

**Programa de instalación completo**: Puede utilizar el programa de instalación completo para configurar nuevas instancias de AEM Forms o realizar actualizaciones de AEM 6.3 Forms en JEE, AEM 6.4 en JEE y la actualización remota de AEM 6.5.x.x Forms en JEE a AEM 6.5.12.0 Forms en JEE.

**Programa de instalación de parches**: El programa de instalación de parches es para clientes que ya utilizan versiones de AEM 6.5.x.x. Puede utilizar el programa de instalación de parches para actualizar a la versión más reciente de AEM Forms.

La siguiente imagen muestra los escenarios para utilizar el programa de instalación completo y de parches.

![Programa de instalación completo y parche](/help/forms/using/assets/full-and-patch-installer.png)

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

      The migration utility makes the adaptive forms and correspondence management assets of earlier versions compatible with AEM 6.3 forms. You can download the utility from AEM Software Distribution. For step-by-step information to configure and use the migration utility, see [migration utility](../../forms/using/migration-utility.md) documentation.

    * **Reconfigure Adobe Sign**

      If you had Adobe Sign configured in the previous version of AEM Forms, then reconfigure Adobe Sign from AEM Cloud services. For more details, see [Integrate Adobe Sign with AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

      Moreover, AEM 6.3 Forms release has introduced many new Adobe Sign features. For step-by-step information to use Adobe Sign, see [Using Adobe Sign in an adaptive form](../../forms/using/working-with-adobe-sign.md).

    * **Reconfigure analytics and reports**

      In AEM 6.3 Forms, traffic variable for source and success event for impression are not available. So, when you upgrade to AEM 6.3 Forms, AEM Forms stops sending data to Adobe Analytics server and analytics reports for adaptive forms are not available. Moreover, AEM 6.3 Forms introduces traffic variable for the version of form analytics and success event for the amount of time spent on a field. So, reconfigure analytics and reports for your AEM Forms environment. For detailed steps, see [Configuring analytics and reports](../../forms/using/configure-analytics-forms-documents.md).

      Methods to calculate average fill time for forms and average read time for have changed. So, when you upgrade to AEM 6.3 forms, older data (data from previous AEM Forms release) for these metrics is available only in Adobe Analytics. It is not visible in AEM Forms analytics reports. For these metrics, AEM Forms analytics reports display data which is captured after performing the upgrade.
      
      -->
