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
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Configuración para aplicaciones AEM{#configuring-for-aem-apps}

Las aplicaciones de Adobe Experience Manager permiten actualizar el contenido de la aplicación a través del aire (OTA). El contenido actualizado se almacena en la instancia de publicación. Para permitir que la aplicación del dispositivo se conecte a la instancia de publicación y buscar actualizaciones, la instancia de publicación debe configurarse para permitir un encabezado de remitente del reenvío vacío.

## Configuración del encabezado de Remitente del reenvío vacío {#configuring-empty-referrer-header}

Para configurar el servicio de filtros de remitente del reenvío:

* Abra la consola Apache Felix (**Configuraciones**) en:
* https://&lt;server>:&lt;número_puerto>/system/console/configMgr
* Inicie sesión como administrador.
* En el menú **Configuraciones**, seleccione: *Filtro de Remitente del reenvío Sling de Apache*
* Marque el campo Permitir vacío para permitir encabezados de remitente del reenvío vacíos o que faltan.
* Haga clic en **Guardar** para guardar los cambios.

![chlimage_1-58](assets/chlimage_1-58a.png)

Consulte la [Configuración de OSGI](/help/sites-deploying/osgi-configuration-settings.md) y [Lista de comprobación de seguridad: problemas con falsificación de solicitudes entre sitios](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) para obtener más información.
