---
title: Estrategia de Backup para Usuarios de Connector para Documentum de EMC
seo-title: Backup strategy for Connector for EMC Documentum users
description: Consulte cómo crear una estrategia de backup para los usuarios de Documentum de EMC en Connector.
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
ht-degree: 0%

---

# Estrategia de Backup para Usuarios de Connector para Documentum de EMC {#backup-strategy-for-connector-for-emc-documentum-users}

Si tiene instalado Connector para Documentum de EMC, además de las instrucciones de este capítulo, su estrategia de backup y recuperación debe incluir backup (o recuperación) del equipo en el que está instalado el sistema ECM correspondiente. (Consulte la documentación de Documentum de ECM).

Haga una copia de seguridad de su entorno de formularios AEM utilizando el repositorio ECM y realizando las siguientes tareas:

* Haga una copia de seguridad de AEM formularios siguiendo las instrucciones descritas en este documento.
* Haga una copia de seguridad de su sistema Documentum de ECM siguiendo las instrucciones de [Haga backup de Documentum Content Server de EMC](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server).

Restaure AEM entorno de formularios utilizando el repositorio ECM y realizando las siguientes tareas:

* Restaure su sistema ECM correspondiente siguiendo las instrucciones indicadas en [Restauración de Content Server de Documentum de EMC](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server).
* Restaure AEM formularios siguiendo las instrucciones descritas en este documento.
