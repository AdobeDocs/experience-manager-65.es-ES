---
title: Actualizar a AEM 6.5 Forms en JEE
description: Puede realizar una actualización directa de AEM 6.1 Forms, AEM 6.2 Forms y LiveCycle ES4 SP1 a AEM 6.3 Forms.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: 722e75a0-bcb3-465e-bb74-ea94a3b99fd3
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 99%

---

# Actualizar a AEM 6.5 Forms en JEE {#upgrade-to-aem-forms-jee}

AEM 6.5.12.0 Forms en JEE proporciona dos tipos de instaladores: Programa de instalación completo y Programa de instalación de parches.

**Programa de instalación completo**: Puede utilizar el [programa de instalación completo de AEM 6.5.12.0 en JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) para configurar nuevas instancias de AEM Forms o realizar actualizaciones de AEM 6.3 Forms en JEE, AEM 6.4 en JEE y la actualización remota de AEM 6.5.x.x Forms en JEE a AEM 6.5.12.0 Forms en JEE.

**Programa de instalación de parches**: [El programa de instalación de parches AEM 6.5.12.0 en JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) es para clientes que ya utilizan versiones de AEM 6.5.x.x. Puede utilizar el programa de instalación de parches para actualizar a la versión más reciente de AEM Forms.

La siguiente tabla muestra los escenarios para utilizar el programa de instalación completo y de parches.

![](assets/full-and-patch-installer.png)

Realice el siguiente procedimiento para utilizar el programa de instalación completo para actualizar el AEM 6.3 Forms existente en JEE o AEM 6.4 Forms en JEE a AEM 6.5.12.0 Forms en JEE:

1. Descargue el programa de instalación AEM 6.5 Forms en JEE desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html). Necesita un contrato de mantenimiento y soporte válido para utilizar el programa de instalación.
1. Consulte [Planificación y lista de comprobación de la actualización](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65_es) para obtener más información sobre las comprobaciones que se deben realizar para garantizar una actualización correcta.
1. Consulte [Prepararse para actualizar a AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65_es) para aprender y realizar las tareas que garantizan que la actualización se ejecute correctamente con un tiempo de inactividad mínimo en el servidor.
1. Según el entorno y el servidor de aplicaciones existentes, elija uno de los siguientes documentos y siga las instrucciones.

   * [Actualizar de AEM 6.3 o AEM 6.4 Forms a AEM 6.5 Forms para JBoss](https://www.adobe.com/go/learn_aemforms_upgradeJBoss_65_es)
   * [Actualizar de AEM 6.3 o AEM 6.4 Forms a AEM 6.5 Forms para WebSphere](https://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65_es)
   * [Actualizar de AEM 6.3 o AEM 6.4 Forms a AEM 6.5 Forms para JBoss Turnkey](https://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65_es)

La actualización directa desde LiveCycle ES2, LiveCycle ES3, AEM 6.0 Forms, AEM 6.1 Forms, AEM 6.2 Forms a AEM 6.5 Forms no está disponible. Puede realizar una actualización intermedia a una o más versiones de LiveCycle o AEM Forms y, a continuación, actualizar a AEM 6.5 Forms. Para obtener la lista de versiones intermedias y las instrucciones de actualización correspondientes, consulte [Elegir una ruta de actualización](upgrade.md).
