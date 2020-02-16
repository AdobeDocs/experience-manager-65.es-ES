---
title: Estrategia de Backup para Usuarios de Connector para Documentum de EMC
seo-title: Estrategia de Backup para Usuarios de Connector para Documentum de EMC
description: Compruebe cómo crear una estrategia de backup para los usuarios de Documentum de EMC para Connector.
seo-description: Compruebe cómo crear una estrategia de backup para los usuarios de Documentum de EMC para Connector.
uuid: 5d8a0476-5231-4e1d-96c4-ae3df68e09f0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e83b1a59-a730-4d22-9d58-1c9c38e5d534
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Estrategia de Backup para Usuarios de Connector para Documentum de EMC {#backup-strategy-for-connector-for-emc-documentum-users}

Si tiene instalado Connector para Documentum de EMC, además de las instrucciones de este capítulo, su estrategia de backup y recuperación debe incluir backup (o recuperación) del equipo en el que está instalado el sistema ECM correspondiente. (Consulte la documentación de Documentum de ECM).

Realice una copia de seguridad del entorno de formularios AEM mediante el repositorio de ECM y las siguientes tareas:

* Realice una copia de seguridad de los formularios AEM siguiendo las instrucciones descritas en este documento.
* Haga backup de su sistema Documentum de ECM siguiendo las instrucciones de [Backup de Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server)de Documentum de EMC.

Restaure el entorno de formularios AEM utilizando el repositorio de ECM y realizando las siguientes tareas:

* Restaure su sistema ECM correspondiente siguiendo las instrucciones de [Restore de Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server)de Documentum de EMC.
* Restaure los formularios de AEM siguiendo las instrucciones descritas en este documento.

