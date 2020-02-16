---
title: Configuración para aplicaciones AEM
seo-title: Configuración para aplicaciones AEM
description: Obtenga información sobre cómo configurar aplicaciones AEM.
seo-description: Obtenga información sobre cómo configurar aplicaciones AEM.
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# Configuración para aplicaciones AEM{#configuring-for-aem-apps}

Las aplicaciones de Adobe Experience Manager permiten actualizar el contenido de la aplicación por aire (OTA). El contenido actualizado se almacena en la instancia de publicación. Para permitir que la aplicación del dispositivo se conecte a la instancia de publicación y buscar actualizaciones, la instancia de publicación debe configurarse para permitir un encabezado de referente vacío.

## Configuración del encabezado de referente vacío {#configuring-empty-referrer-header}

Para configurar el servicio de filtros de referente:

* Abra la consola Apache Felix (**Configuraciones**) en:
* https://&lt;server>:&lt;número_puerto>/system/console/configMgr
* Inicie sesión como administrador.
* En el menú **Configuraciones** , seleccione: Filtro de referente *Apache Sling*
* Marque el campo Permitir vacío para permitir encabezados de referente vacíos o ausentes.
* Click **Save** to save your changes.

![chlimage_1-58](assets/chlimage_1-58a.png)

Consulte Configuración de [OSGI](/help/sites-deploying/osgi-configuration-settings.md) y Lista de comprobación de [seguridad - Problemas con falsificación](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) de solicitudes entre sitios para obtener más información.
