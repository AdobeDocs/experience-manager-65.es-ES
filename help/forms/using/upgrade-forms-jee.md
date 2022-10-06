---
title: Actualizar a AEM 6.5 Forms
seo-title: Upgrade to AEM 6.5 Forms
description: Puede realizar una actualización directa de AEM 6.1 Forms, AEM 6.2 Forms y LiveCycle ES4 SP1 a AEM 6.3 Forms.
seo-description: You can perform a direct upgrade from AEM 6.1 Forms, AEM 6.2 Forms, and LiveCycle ES4 SP1 to AEM 6.3 Forms.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: 722e75a0-bcb3-465e-bb74-ea94a3b99fd3
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 6%

---

# Actualización a AEM 6.5 Forms en JEE {#upgrade-to-aem-forms-jee}

AEM 6.5.12.0 Forms en JEE proporciona dos tipos de instaladores: Instalador completo y instalador de parches.

**Instalador completo**: Puede usar la variable [AEM 6.5.12.0 en el instalador completo de JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) para configurar nuevas instancias de AEM Forms o realizar actualizaciones de AEM 6.3 Forms en JEE, AEM 6.4 en JEE y la actualización fuera de lugar de AEM 6.5.x.x Forms en JEE a AEM 6.5.12.0 Forms en JEE.

**Instalador de parches**: [AEM 6.5.12.0 en el instalador de parches de JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) es para clientes que ya utilizan AEM versión 6.5.x.x. Puede utilizar el instalador de parches para actualizar a la versión más reciente de AEM Forms.

La siguiente tabla muestra los escenarios para utilizar el instalador completo y el instalador de parches.

![](assets/full-and-patch-installer.png)

Realice el siguiente procedimiento para utilizar el instalador completo para actualizar el Forms existente AEM 6.3 en JEE o AEM 6.4 Forms en JEE a AEM 6.5.12.0 Forms en JEE:

1. Descargue el instalador AEM 6.5 de Forms en JEE desde el [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html). Necesita un contrato de mantenimiento y soporte válido para utilizar el instalador.
1. Consulte [Planificación y lista de comprobación de la actualización](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65) para obtener más información sobre las comprobaciones que se deben realizar para garantizar una actualización correcta.
1. Consulte [Preparación para actualizar a AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65) para aprender y realizar las tareas que garantizan que la actualización se ejecute correctamente con un tiempo de inactividad mínimo en el servidor.
1. Según el entorno y el servidor de aplicaciones existentes, elija uno de los siguientes documentos y siga las instrucciones.

   * [Actualización de AEM 6.3 o AEM 6.4 Forms a AEM 6.5 Forms para JBoss](https://www.adobe.com/go/learn_aemforms_upgradeJBoss_65)
   * [Actualización de AEM 6.3 o AEM 6.4 Forms a AEM 6.5 Forms para WebSphere](https://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65)
   * [Actualización de AEM 6.3 o AEM 6.4 Forms a AEM 6.5 Forms para JBoss Turnkey](https://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65)

La actualización directa desde LiveCycle ES2, LiveCycle ES3, AEM 6.0 Forms, AEM 6.1 Forms, AEM 6.2 Forms a AEM 6.5 Forms no está disponible. Puede realizar una actualización intermedia a una o más versiones de LiveCycle o AEM Forms y, a continuación, actualizar a AEM 6.5 Forms. Para obtener la lista de versiones intermedias y las instrucciones de actualización correspondientes, consulte [Elija una ruta de actualización](upgrade.md).
