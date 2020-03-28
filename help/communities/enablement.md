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
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Configuración de las funciones de habilitación {#configuring-enablement-features}

## Información general {#overview}

Las funciones de habilitación permiten crear comunidades [de](overview.md#enablement-community)habilitación.

* Esta función requiere licencias adicionales para su uso en un entorno de producción.

El uso de las funciones de habilitación requiere lo siguiente:

Instalación de:

* **SCORM**

   El Modelo de referencia de objetos de contenido compartido (SCORM) es una colección de estándares y especificaciones para el aprendizaje electrónico. SCORM también define cómo se puede empaquetar el contenido en un archivo ZIP transferible.

* **MySQL**

   MySQL es una base de datos relacional que se utiliza principalmente para el seguimiento de SCORM y los datos de sistema de informes para Habilitación, así como tablas para el seguimiento del progreso del video. El paquete de funciones SCORM para habilitación requiere el controlador JDBC MySQL.

* **FFmpeg**

   FFmpeg es una solución para convertir y transmitir audio y vídeo y, cuando se instala, se utiliza para una transcodificación adecuada de los recursos [de vídeo](../../help/sites-authoring/default-components-foundation.md#video). Para las comunidades de habilitación, se utiliza en el entorno del autor para obtener metadatos de los recursos cargados y generar una miniatura para mostrarla al enumerar el recurso.

Configuración de:

* **Administradores de la comunidad**

   Para las comunidades de habilitación, solo se puede asignar la función de miembros del grupo de `Community Enablement Managers` usuarios `Community Site Enablement Manager`, cuyos permisos pueden incluir la creación de contenido, las asignaciones y la administración de miembros en el entorno de publicación.

Configuración opcional de:

* **Adobe Analytics**

   La integración con Adobe Analytics agrega funciones de sistema de informes completas y admite la adición de Video Heartbeat a Analytics.

* **Dispatcher**

## Pasos de configuración {#configuration-steps}

A continuación se indican los pasos necesarios para habilitar a las comunidades.

Cada paso enlaza a la documentación que proporciona los detalles necesarios.

**En todas las instancias de autor/publicación:**

1. **[Instalación del controlador JDBC para MySQL](deploy-communities.md#jdbc-driver-for-mysql)**

   Utilizar consola web (paquetes): *http://localhost:4502/system/console/bundles* Instalar *antes* de instalar el paquete SCORM

1. **[Instalación del paquete](deploy-communities.md#scorm-package)**SCORM Uso del administrador de paquetes:*http://localhost:4502/crx/packmgr/*

**En cualquier servidor:**

1. **[Instalar MySQL, MySQL Workbench](mysql.md)**

1. **[Instalación de bases de datos MySQL](mysql.md#database-setup)**

   Ejecutar secuencias de comandos SQL descargadas de la instancia de autorUsar MySQL Workbench

**En la misma instancia de autor de alojamiento de servidor:**

1. **[Instalar FFmpeg](ffmpeg.md)**

**En todas las instancias de autor/publicación:**

1. **[Configurar el grupo de conexiones JDBC](mysql.md#configure-jdbc-connections)**

   Utilizar consola web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Configuración del servicio de motor SCORM](mysql.md#aem-communities-scormengine-service)**

   Utilizar consola web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Configurar filtros CSRF](mysql.md#adobe-granite-csrf-filter)**

   Utilizar consola web (configMgr): *http://localhost:4502/system/console/configMgr*

**En la instancia de autor:**

1. (*Opcional*) **[Configurar el servicio Analytics](analytics.md)**

   Utilice la consola Herramientas, Implementación y Servicios de nube: *http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[Configurar FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   Utilizar consola de flujo de trabajo/modelos

1. **[Habilitar servicio de túnel](deploy-communities.md#tunnel-service-on-author)**

   Utilizar consola web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Crear administradores de comunidad](users.md#creating-community-members)**

   Para crear entorno, utilice la consola de seguridad clásica-UI: *http://localhost:4502/useradmin* crear usuarios con ruta = /home/users/community

   * Añadir miembros a los siguientes grupos:

      * Administradores de habilitación de la comunidad
      * Administradores de comunidades

## Dispatcher {#dispatcher}

Cuando la implementación incluye Dispatcher [de](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)AEM, para que las funciones de habilitación funcionen correctamente, es necesario modificar las secciones `clientheader` y `filter` . Consulte [Configuración de Dispatcher para Comunidades](dispatcher.md#enablement).
