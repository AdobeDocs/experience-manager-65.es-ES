---
title: Configuración del programador de sincronización
seo-title: Configuración del programador de sincronización
description: Obtenga información sobre cómo migrar y sincronizar recursos, configurar el programador de sincronización y utilizar carpetas para organizar los recursos.
seo-description: Obtenga información sobre cómo migrar y sincronizar recursos, configurar el programador de sincronización y utilizar carpetas para organizar los recursos.
uuid: b2c89feb-2947-418a-b343-4c01e453602b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8c8b1998-eab4-4230-b24f-5e96883ba599
docset: aem65
role: Admin
exl-id: 34db1f76-ee40-4612-85da-22041e7560fb
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Configuración del programador de sincronización {#configuring-the-synchronization-scheduler}

De forma predeterminada, el programador de sincronización se ejecuta cada 3 minutos para sincronizar todos los recursos modificados y actualizados en el repositorio mediante LiveCycle Workbench 11. Las aplicaciones que contienen formularios y recursos son visibles en la interfaz de usuario de AEM Forms una vez finalizado el proceso de sincronización.

## Cambiar el intervalo del programador de sincronización {#change-interval-of-the-synchronization-scheduler}

Realice los siguientes pasos para cambiar el intervalo del programador de sincronización:

1. Inicie sesión en AEM Administrador de configuración. La dirección URL de Configuration Manager es `https://'[server]:[port]'/lc/system/console/configMgr`

1. Busque y abra el paquete **FormsManagerConfiguration**.

1. Especifique un nuevo valor para la opción **Frecuencia del planificador de sincronización**.

   La unidad de la frecuencia es minutos. Por ejemplo, para configurar el planificador para que se ejecute después de cada 60 minutos, especifique 60.

## Sincronización de recursos {#synchronizing-assets}

Puede utilizar la opción **Sincronizar recursos del repositorio** para sincronizar manualmente los recursos. Realice los siguientes pasos para sincronizar manualmente los recursos:

1. Inicie sesión en AEM Forms. La dirección URL predeterminada es `https://'[server]:[port]'/lc/aem/forms/`.

   ![Interfaz de usuario de AEM Forms](assets/aem_forms_ui.png)

   **Figura: Interfaz de usuario de** *AEM Forms*

1. Haga clic en el icono ![aem6forms_sync](assets/aem6forms_sync.png) de la barra de herramientas. Si no tiene ningún recurso en la última ruta configurada, seleccione el cuadro de diálogo como se muestra a continuación. Haga clic en **Start** para iniciar la sincronización.

   ![Cuadro de diálogo Sincronización](assets/migrate-and-syncronize.png)

   **Figura: Cuadro de diálogo** *Sincronización*

## Solución de problemas de sincronización {#troubleshooting-synchronization-error}

Puede crear nuevas aplicaciones en el diseñador de flujos de trabajo (Área de trabajo de LiveCycle).

Si la aplicación recién creada y una carpeta en /content/dam/formsanddocuments tienen un nombre idéntico, aparece el error &quot;*Un recurso con el mismo nombre que esta aplicación ya existe en el nivel raíz.*&quot; está registrado.

Para resolver el conflicto, cambie el nombre de la aplicación y sincronice manualmente los recursos.

![Conflictos en el cuadro de diálogo de sincronización de recursos](assets/sync-conflict.png)

**Figura:** *Conflictos en el cuadro de diálogo de sincronización de recursos*
