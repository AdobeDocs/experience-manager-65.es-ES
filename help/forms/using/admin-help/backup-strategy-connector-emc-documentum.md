---
title: Estrategia de copia de seguridad para usuarios de Connector para Documentum de EMC
seo-title: Backup strategy for Connector for EMC Documentum users
description: Consulte cómo crear una estrategia de copia de seguridad para usuarios de Connector para Documentum de EMC.
seo-description: Check how to create a backup strategy for Connector for EMC Documentum users.
uuid: 5d8a0476-5231-4e1d-96c4-ae3df68e09f0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e83b1a59-a730-4d22-9d58-1c9c38e5d534
exl-id: b759b936-5907-4311-a5cc-60f321476368
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 10%

---

# Estrategia de copia de seguridad para usuarios de Connector para Documentum de EMC {#backup-strategy-for-connector-for-emc-documentum-users}

Si tiene instalado Connector para Documentum de EMC, además de las instrucciones de este capítulo, la estrategia de copia de seguridad y recuperación debe incluir la copia de seguridad (o recuperación) del equipo en el que está instalado el sistema ECM correspondiente. (Consulte la documentación de Documentum de ECM).

AEM Haga una copia de seguridad del entorno de formularios de la utilizando el repositorio de ECM y realizando las siguientes tareas:

* AEM Realice una copia de seguridad de los formularios de la aplicación siguiendo las instrucciones descritas en este documento.
* Realice una copia de seguridad del sistema Documentum de ECM siguiendo las instrucciones indicadas en [Copia de seguridad de EMC Documentum Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server).

AEM Restaurar el entorno de formularios utilizando el repositorio de ECM y realizando las siguientes tareas:

* Restaure su sistema ECM respectivo siguiendo las instrucciones de [Restaurar EMC Documentum Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server).
* AEM Restaure formularios siguiendo las instrucciones descritas en este documento.
