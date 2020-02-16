---
title: Configuración de las funciones de habilitación
seo-title: Configuración de las funciones de habilitación
description: Configurar funciones de habilitación en Comunidades
seo-description: Configurar funciones de habilitación en Comunidades
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración de las funciones de habilitación {#configuring-enablement-features}

## Información general {#overview}

Las funciones de habilitación permiten crear comunidades [de](overview.md#enablement-community)habilitación.

* Esta función requiere licencias adicionales para su uso en un entorno de producción.

El uso de las funciones de habilitación requiere lo siguiente:

Instalación de:

* **SCORM** Sharable Content Object Reference Model (SCORM) es un conjunto de estándares y especificaciones para el aprendizaje electrónico. SCORM también define cómo se puede empaquetar el contenido en un archivo ZIP transferible.

* **MySQL** MySQL es una base de datos relacional que se utiliza principalmente para el seguimiento de SCORM y los datos de informes para Habilitación, así como tablas para el seguimiento del progreso del video. El paquete de funciones SCORM para habilitación requiere el controlador JDBC MySQL.

* **FFmpeg** FFmpeg es una solución para convertir y transmitir audio y vídeo y, cuando se instala, se utiliza para una transcodificación adecuada de los recursos [de](../../help/sites-authoring/default-components-foundation.md#video)vídeo. Para las comunidades de habilitación, se utiliza en el entorno de creación para obtener metadatos de los recursos cargados, así como para generar una miniatura que se mostrará al enumerar el recurso.

Configuración de:

* **Administradores** de comunidad Para comunidades de habilitación, solo se puede asignar la función de `Community Enablement Managers` a los miembros del grupo de `*Community Site* Enablement Manager`usuarios, cuyos permisos pueden incluir la creación de contenido, las asignaciones y la administración de miembros en el entorno de publicación.

Configuración opcional de:

* **La integración de Adobe Analytics** con Adobe Analytics agrega funciones de creación de informes completas y admite la adición de Video Heartbeat a Analytics.

* **Dispatcher**

## Pasos de configuración {#configuration-steps}

A continuación se indican los pasos necesarios para habilitar a las comunidades.

Cada paso enlaza a la documentación que proporciona los detalles necesarios.

**En todas las instancias de autor/publicación:**

1. **[instalar controlador JDBC para MySQL](deploy-communities.md#jdbc-driver-for-mysql)**Usar consola web (paquetes):*http://localhost:4502/system/console/bundles*Instalar *antes*de instalar el paquete SCORM

1. **[instalar paquete](deploy-communities.md#scorm-package)**SCORM Usar administrador de paquetes:*http://localhost:4502/crx/packmgr/*

**En cualquier servidor:**

1. **[instalar MySQL, MySQL Workbench](mysql.md)**

1. **[instalar bases de datos](mysql.md#database-setup)**MySQL Ejecutar secuencias de comandos SQL descargadas de la instancia de autorUsar MySQL Workbench

**En la misma instancia de autor de alojamiento de servidor:**

1. **[instalar FFmpeg](ffmpeg.md)**

**En todas las instancias de autor/publicación:**

1. **[configurar el grupo](mysql.md#configure-jdbc-connections)**Conexiones JDBCusar la consola Web (configMgr):*http://localhost:4502/system/console/configMgr*

1. **[configurar el servicio](mysql.md#aem-communities-scormengine-service)**de motor SCORM Usar consola web (configMgr):*http://localhost:4502/system/console/configMgr*

1. **[configurar filtros](mysql.md#adobe-granite-csrf-filter)**CSRF Usar consola web (configMgr):*http://localhost:4502/system/console/configMgr*

**En la instancia de autor:**

1. (*opcional*) **[configure el servicio](analytics.md)**de AnalyticsUtilice las herramientas, la implementación y la consola de servicios de nube:*http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[configurar la consola Fumpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**Usar flujo de trabajo/modelos

1. **[habilitar servicio](deploy-communities.md#tunnel-service-on-author)**de túnel Usar consola web (configMgr):*http://localhost:4502/system/console/configMgr*

1. **[crear administradores](users.md#creating-community-members)**de comunidad Para entorno de creación, utilice la consola de seguridad clásica-UI:*http://localhost:4502/useradmin*crear usuarios con ruta = /home/users/community

   * Agregue miembros a los siguientes grupos:

      * Administradores de habilitación de la comunidad
      * Administradores de comunidades

## Dispatcher {#dispatcher}

Cuando la implementación incluye Dispatcher [de](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)AEM, para que las funciones de habilitación funcionen correctamente, es necesario modificar las `clientheader`secciones `filter`y . Consulte [Configuración de Dispatcher para Comunidades](dispatcher.md#enablement).
