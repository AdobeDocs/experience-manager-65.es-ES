---
title: Estrategia de copia de seguridad para usuarios de Connector para Documentum&reg; de EMC
description: Consulte cómo crear una estrategia de copia de seguridad para los usuarios de Connector for EMC Documentum&reg;.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b759b936-5907-4311-a5cc-60f321476368
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Estrategia de copia de seguridad para usuarios de Connector para Documentum® de EMC {#backup-strategy-for-connector-for-emc-documentum-users}

Si tiene instalado Connector para EMC Documentum®, además de las instrucciones de este capítulo, la estrategia de copia de seguridad y recuperación debe incluir la copia de seguridad (o recuperación) del equipo en el que está instalado el sistema ECM. (Consulte la documentación de ECM Documentum®).

AEM Haga una copia de seguridad del entorno de formularios de la utilizando el repositorio de ECM y realizando las siguientes tareas:

* AEM Realice una copia de seguridad de los formularios de la aplicación siguiendo las instrucciones descritas en este documento.
* Realice una copia de seguridad del sistema ECM Documentum® siguiendo las instrucciones indicadas en [Copia de seguridad de EMC Documentum® Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server).

AEM Restaurar el entorno de formularios utilizando el repositorio de ECM y realizando las siguientes tareas:

* Restaure su sistema ECM respectivo siguiendo las instrucciones de [Restaurar EMC Documentum® Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server).
* AEM Restaure formularios siguiendo las instrucciones descritas en este documento.
