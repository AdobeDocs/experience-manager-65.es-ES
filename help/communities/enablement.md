---
title: Configuración de funciones de habilitación
seo-title: Configuring Enablement Features
description: Configurar funciones de habilitación en Communities
seo-description: Configure enablement features in Communities
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
source-wordcount: '439'
ht-degree: 3%

---

# Configuración de funciones de habilitación {#configuring-enablement-features}

## Información general {#overview}

Las funciones de habilitación permiten crear lo siguiente [comunidades de habilitación](overview.md#enablement-community).

* Esta función requiere licencias adicionales para su uso en entornos de producción.

El uso de las funciones de habilitación requiere lo siguiente:

Instalación de:

* **SCORM**

   El Modelo de referencia de objetos de contenido compartido (SCORM) es un conjunto de estándares y especificaciones para el aprendizaje electrónico. SCORM también define cómo se puede empaquetar el contenido en un archivo ZIP transferible.

* **MySQL**

   MySQL es una base de datos relacional que se utiliza principalmente para el seguimiento de SCORM y los datos de informes para la habilitación, así como tablas para el seguimiento del progreso de vídeo. El paquete de funciones SCORM para habilitación requiere el controlador JDBC MySQL.

* **FFmpeg**

   FFmpeg es una solución para la conversión y transmisión de audio y vídeo y, cuando está instalado, se utiliza para la transcodificación adecuada de [Recursos de vídeo](../../help/sites-authoring/default-components-foundation.md#video). Para las comunidades de habilitación, se utiliza en el entorno de creación para obtener metadatos para los recursos cargados, así como para generar una miniatura que se mostrará al enumerar el recurso.

Configuración de:

* **Administradores de la comunidad**

   Para comunidades de habilitación, solo los miembros de `Community Enablement Managers` grupo de usuarios puede tener asignada la función de `Community Site Enablement Manager`, cuyos permisos pueden incluir la creación de contenido, asignaciones y administración de miembros en el entorno de publicación.

Configuración opcional de:

* **Adobe Analytics**

   La integración con Adobe Analytics añade completas funciones de creación de informes y admite la adición de Video Heartbeat a Analytics.

* **Dispatcher**

## Pasos de configuración {#configuration-steps}

A continuación se indican los pasos necesarios para las comunidades de habilitación.

Cada paso vincula a una documentación que proporciona los detalles necesarios.

**En todas las instancias de autor/publicación:**

1. **[Instalar el controlador JDBC para MySQL](deploy-communities.md#jdbc-driver-for-mysql)**

   Usar la consola web (paquetes): *http://localhost:4502/system/console/bundles*

   Instalar *antes* instalar el paquete SCORM

1. **[Instalación del paquete SCORM](deploy-communities.md#scorm-package)**


   Usar Administrador de paquetes: *http://localhost:4502/crx/packmgr/*

**En cualquier servidor:**

1. **[Instalar MySQL, MySQL Workbench](mysql.md)**

1. **[Instalación de bases de datos MySQL](mysql.md#database-setup)**

   Ejecutar scripts SQL descargados de la instancia de autor

   Uso de MySQL Workbench

**En el mismo servidor que aloja la instancia de autor:**

1. **[Instalar FFmpeg](ffmpeg.md)**

**En todas las instancias de autor/publicación:**

1. **[Configurar el grupo de conexiones JDBC](mysql.md#configure-jdbc-connections)**

   Usar la consola web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Configuración del servicio del motor SCORM](mysql.md#aem-communities-scormengine-service)**

   Usar la consola web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Configuración de filtros CSRF](mysql.md#adobe-granite-csrf-filter)**

   Usar la consola web (configMgr): *http://localhost:4502/system/console/configMgr*

**En la instancia de autor:**

1. (*Opcional*) **[Configurar el servicio de Analytics](analytics.md)**

   Uso de herramientas, implementación, consola de Cloud Services: *http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[Configurar FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   Usar flujo de trabajo/consola de modelos

1. **[Habilitar servicio de túnel](deploy-communities.md#tunnel-service-on-author)**

   Usar la consola web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Crear administradores de la comunidad](users.md#creating-community-members)**

   Para el entorno de autor, utilice la consola de seguridad de la IU clásica: *http://localhost:4502/useradmin*

   Crear usuario(s) con ruta = /home/users/community

   * Agregar miembros a los siguientes grupos:

      * Administradores de habilitación de comunidades
      * Administradores de Communities

## Dispatcher {#dispatcher}

Cuando la implementación incluye [AEM Dispatcher](https://helpx.adobe.com/es/experience-manager/dispatcher/using/dispatcher.html), para que las funciones de habilitación funcionen correctamente, la variable `clientheader` y `filter` las secciones deben modificarse. Consulte [Configurar Dispatcher para comunidades](dispatcher.md#enablement).
