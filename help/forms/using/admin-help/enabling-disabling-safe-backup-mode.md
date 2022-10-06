---
title: Activación y desactivación del modo de copia de seguridad segura
seo-title: Enabling and disabling safe backup mode
description: En la página Configuración de copia de seguridad, puede utilizar AEM formularios en modo de copia de seguridad segura, de modo que pueda realizar una copia de seguridad fiable de la base de datos y del directorio Global Document Storage (GDS) (GDS). Aprenda a habilitar y deshabilitar el modo de copia de seguridad segura.
seo-description: On the Backup Settings page, you can operate AEM forms in safe backup mode so that you can reliably back up your database and Global Document Storage (GDS) (GDS) directory. Learn how to enable and disable safe backup mode.
uuid: 2fdeaeaf-e969-40a4-8aee-1f2b627d3942
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fda71e4-78a1-4581-9d02-bf06a75c3bcb
exl-id: f0ab712f-ecd9-4be8-a7a5-fd1a7a8c9a0b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Activación y desactivación del modo de copia de seguridad segura {#enabling-and-disabling-safe-backup-mode}

En la página Configuración de copia de seguridad, puede utilizar AEM formularios en modo de copia de seguridad segura, de modo que pueda realizar una copia de seguridad fiable de la base de datos y del directorio Global Document Storage (GDS) (GDS).

Aunque AEM formularios se encuentra en modo de copia de seguridad segura, funciona normalmente, excepto que no elimina de forma activa los archivos del directorio GDS.

>[!NOTE]
>
>Configurar esta opción no hace una copia de seguridad del sistema; prepara el sistema para realizar copias de seguridad.

## Habilitar el modo de copia de seguridad segura {#enable-safe-backup-mode}

1. En la consola de administración, haga clic en Configuración > Configuración de sistemas principales > Configuración de copia de seguridad.
1. En la página Configuración de copia de seguridad, seleccione Operar en modo de copia de seguridad segura y haga clic en Aceptar.

>[!NOTE]
>
>Si el sistema ya se está ejecutando en modo de copia de seguridad segura, no se creará una reserva nueva al hacer clic en Aceptar.

## Deshabilitar el modo de copia de seguridad segura {#disable-safe-backup-mode}

1. En la consola de administración, haga clic en Configuración > Configuración de sistemas principales > Configuración de copia de seguridad.
1. En la página Configuración de copia de seguridad, anule la selección de Operar en modo de copia de seguridad segura y haga clic en Aceptar.
