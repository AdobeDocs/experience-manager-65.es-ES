---
title: AEM Configuración de para aplicaciones de
description: Aprenda a utilizar las aplicaciones de Adobe Experience Manager para actualizar el contenido de su aplicación OTA (por el aire).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# AEM Configuración de para aplicaciones de{#configuring-for-aem-apps}

Adobe Experience Manager Apps permite actualizar el contenido de la OTA de la aplicación (por el aire). El contenido actualizado se almacena en la instancia de publicación. Para permitir que la aplicación de su dispositivo se conecte a la instancia de publicación y compruebe las actualizaciones, la instancia de publicación debe configurarse para permitir un encabezado de referente vacío.

## Configuración de un encabezado de referente vacío {#configuring-empty-referrer-header}

Para configurar el servicio del filtro de referente:

* Abra la consola Apache Felix (**Configuraciones**) en:
* https://&lt;server>:&lt;port_number>/system/console/configMgr
* Inicie sesión como administrador.
* En el menú **Configuraciones**, seleccione: *Filtro de referente de Apache Sling*
* Marque el campo Permitir vacío para poder permitir encabezados de referente vacíos o que falten.
* Haga clic en **Guardar** para guardar los cambios.

![chlimage_1-58](assets/chlimage_1-58a.png)

Consulte las [Opciones de configuración de OSGI](/help/sites-deploying/osgi-configuration-settings.md) y la [Lista de comprobación de seguridad - Problemas con la falsificación de solicitudes entre sitios](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) para obtener más información.
