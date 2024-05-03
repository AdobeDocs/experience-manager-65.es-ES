---
title: Habilitar y deshabilitar el modo de copia de seguridad
description: AEM En la página Configuración de copia de seguridad, puede utilizar formularios en modo de copia de seguridad segura para realizar copias de seguridad fiables de la base de datos y del directorio de almacenamiento global de documentos (GDS) (GDS). Obtenga información sobre cómo habilitar y deshabilitar el modo de copia de seguridad segura.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f0ab712f-ecd9-4be8-a7a5-fd1a7a8c9a0b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 6%

---

# Habilitar y deshabilitar el modo de copia de seguridad {#enabling-and-disabling-safe-backup-mode}

AEM En la página Configuración de copia de seguridad, puede utilizar formularios en modo de copia de seguridad segura para realizar copias de seguridad fiables de la base de datos y del directorio de almacenamiento global de documentos (GDS) (GDS).

AEM Mientras que los formularios de datos se encuentran en modo de copia de seguridad seguro, funcionan normalmente, excepto que no eliminan activamente los archivos del directorio GDS.

>[!NOTE]
>
>La configuración de esta opción no realiza una copia de seguridad del sistema, sino que lo prepara para realizar una copia de seguridad.

## Habilitar modo de copia de seguridad {#enable-safe-backup-mode}

1. En la consola de administración, haga clic en Configuración > Configuración de sistemas principales > Configuración de copia de seguridad.
1. En la página Configuración de copia de seguridad, seleccione Operar en modo de copia de seguridad segura y haga clic en Aceptar.

>[!NOTE]
>
>Si el sistema ya se está ejecutando en modo de copia de seguridad, no se creará una nueva reserva al hacer clic en Aceptar.

## Desactivar el modo de copia de seguridad {#disable-safe-backup-mode}

1. En la consola de administración, haga clic en Configuración > Configuración de sistemas principales > Configuración de copia de seguridad.
1. En la página Configuración de copia de seguridad, anule la selección de Operar en modo de copia de seguridad segura y haga clic en Aceptar.
