---
title: AEM Configuración de para aplicaciones de
seo-title: Configuring for AEM Apps
description: AEM Obtenga información sobre cómo configurar aplicaciones de.
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

# AEM Configuración de para aplicaciones de{#configuring-for-aem-apps}

Las aplicaciones de Adobe Experience Manager permiten actualizar el contenido de la aplicación por el aire (OTA). El contenido actualizado se almacena en la instancia de publicación. Para permitir que la aplicación de su dispositivo se conecte a la instancia de publicación y compruebe las actualizaciones, la instancia de publicación debe configurarse para permitir un encabezado de referente vacío.

## Configuración de un encabezado de referente vacío {#configuring-empty-referrer-header}

Para configurar el servicio del filtro de referente:

* Abra la consola Apache Felix (**Configuraciones**) a las:
* https://&lt;server>:&lt;port_number>/system/console/configMgr
* Inicie sesión como administrador.
* En el **Configuraciones** menú, seleccione: *Filtro de referente de Apache Sling*
* Marque el campo Permitir vacío para permitir encabezados de referente vacíos o que falten.
* Clic **Guardar** para guardar los cambios.

![chlimage_1-58](assets/chlimage_1-58a.png)

Consulte la [Ajustes de configuración de OSGI](/help/sites-deploying/osgi-configuration-settings.md) y [Lista de comprobación de seguridad - Problemas con la falsificación de solicitudes entre sitios](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) para obtener más información.
