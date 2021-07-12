---
title: Configuración de funciones de habilitación
seo-title: Configuración de funciones de habilitación
description: Configurar las funciones de habilitación en Communities
seo-description: Configurar las funciones de habilitación en Communities
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
role: Admin
exl-id: b635e2ed-4637-4b2f-a746-ec8dc7541bab
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Configuración de funciones de habilitación {#configuring-enablement-features}

## Información general {#overview}

Las funciones de habilitación permiten crear [comunidades de habilitación](overview.md#enablement-community).

* Esta función requiere licencias adicionales para su uso en un entorno de producción.

El uso de las funciones de habilitación requiere lo siguiente:

Instalación de:

* **SCORM**

   El Modelo de referencia de objetos de contenido compartible (SCORM) es una colección de estándares y especificaciones para el aprendizaje electrónico. SCORM también define cómo el contenido puede empaquetarse en un archivo ZIP transferible.

* **MySQL**

   MySQL es una base de datos relacional que se utiliza principalmente para el seguimiento de SCORM y los datos de informes para la habilitación, así como tablas para el seguimiento del progreso del vídeo. El SCORM para el paquete de características de habilitación requiere el controlador JDBC de MySQL.

* **FFmpeg**

   FFmpeg es una solución para convertir y transmitir audio y vídeo y, cuando se instala, se utiliza para la transcodificación adecuada de [Video Assets](../../help/sites-authoring/default-components-foundation.md#video). Para las comunidades de habilitación, se utiliza en el entorno de creación para obtener metadatos de los recursos cargados, así como para generar una miniatura que se mostrará al enumerar el recurso.

Configuración de:

* **Administradores de la comunidad**

   Para las comunidades de habilitación, solo se puede asignar a los miembros del grupo de usuarios `Community Enablement Managers` la función de `Community Site Enablement Manager`, cuyos permisos pueden incluir la creación de contenido, asignaciones y administración de miembros en el entorno de publicación.

Configuración opcional de:

* **Adobe Analytics**

   La integración con Adobe Analytics agrega funciones de informes completas y admite la adición de Video Heartbeat a Analytics.

* **Dispatcher**

## Pasos de configuración {#configuration-steps}

A continuación se indican los pasos necesarios para habilitar a las comunidades.

Cada paso vincula a la documentación que proporciona los detalles necesarios.

**En todas las instancias de autor/publicación:**

1. **[Instalación del controlador JDBC para MySQL](deploy-communities.md#jdbc-driver-for-mysql)**

   Utilizar la consola web (paquetes): *http://localhost:4502/system/console/bundles*

   Instale *antes* de instalar el paquete SCORM

1. **[Instalación del paquete SCORM](deploy-communities.md#scorm-package)**


   Utilice el Administrador de paquetes: *http://localhost:4502/crx/packmgr/*

**En cualquier servidor:**

1. **[Instalar MySQL, MySQL Workbench](mysql.md)**

1. **[Instalar bases de datos MySQL](mysql.md#database-setup)**

   Ejecución de scripts SQL descargados de la instancia de autor

   Usar MySQL Workbench

**En la misma instancia de autor de alojamiento de servidor:**

1. **[Instalar FFmpeg](ffmpeg.md)**

**En todas las instancias de autor/publicación:**

1. **[Configurar el grupo de conexiones JDBC](mysql.md#configure-jdbc-connections)**

   Usar la consola web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Configurar el servicio de motor SCORM](mysql.md#aem-communities-scormengine-service)**

   Usar la consola web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Configuración de filtros CSRF](mysql.md#adobe-granite-csrf-filter)**

   Usar la consola web (configMgr): *http://localhost:4502/system/console/configMgr*

**En la instancia de autor:**

1. (*Opcional*) **[Configurar el servicio de Analytics](analytics.md)**

   Utilice Herramientas, Implementación, consola Cloud Services: *http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[Configurar FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   Uso de la consola Flujo de trabajo/Modelos

1. **[Habilitar el servicio de túnel](deploy-communities.md#tunnel-service-on-author)**

   Usar la consola web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Crear administradores de la comunidad](users.md#creating-community-members)**

   Para el entorno de creación, utilice la consola de seguridad clásica-UI: *http://localhost:4502/useradmin*

   Crear usuarios con la ruta = /home/users/community

   * Agregue miembros a los siguientes grupos:

      * Administradores de habilitación de la comunidad
      * Administradores de comunidades

## Dispatcher {#dispatcher}

Cuando la implementación incluye [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html), para que las funciones de habilitación funcionen correctamente, es necesario modificar las secciones `clientheader` y `filter`. Consulte [Configuración de Dispatcher para Communities](dispatcher.md#enablement).
