---
title: Configuración para aplicaciones AEM
seo-title: Configuring for AEM Apps
description: Obtenga información sobre cómo configurar AEM aplicaciones.
seo-description: Learn how to configure AEM Apps.
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Configuración para aplicaciones AEM{#configuring-for-aem-apps}

Adobe Experience Manager Apps proporciona la capacidad de actualizar el contenido de su aplicación por aire (OTA). El contenido actualizado se almacena en la instancia de publicación. Para permitir que la aplicación del dispositivo se conecte a la instancia de publicación y compruebe si hay actualizaciones, la instancia de publicación debe configurarse para permitir un encabezado de referente vacío.

## Configuración del encabezado de referente vacío {#configuring-empty-referrer-header}

Para configurar el servicio de filtro de referente:

* Abra la consola Apache Felix (**Configuraciones**) en:
* https://&lt;server>:&lt;port_number>/system/console/configMgr
* Inicie sesión como administrador.
* En el **Configuraciones** seleccione: *Filtro de referente de Apache Sling*
* Marque el campo Permitir vacío para permitir encabezados de referente vacíos o que faltan.
* Haga clic en **Guardar** para guardar los cambios.

![chlimage_1-58](assets/chlimage_1-58a.png)

Consulte la [Configuración de OSGI](/help/sites-deploying/osgi-configuration-settings.md) y [Lista de comprobación de seguridad: problemas con la falsificación de solicitudes entre sitios](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) para obtener más información.
