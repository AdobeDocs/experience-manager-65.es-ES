---
title: Configuración de usuarios y grupos de usuarios
description: Siga esta página para comprender las funciones de usuario y cómo configurar los usuarios y grupos para que admitan la creación y administración de sus aplicaciones móviles.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 9f814204-8cd4-4ba9-9e25-3ff1b25c1955
source-git-commit: 0aa929021aa724e4ec18d49fea26f8c0b0538bdc
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Configuración de usuarios y grupos de usuarios {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

En este capítulo se describen las funciones de usuario y cómo configurar los usuarios y grupos para que admitan la creación y administración de sus aplicaciones móviles.

## Administración de grupos y usuarios de aplicaciones AEM Mobile {#aem-mobile-application-users-and-group-administration}

AEM Para ayudar a organizar y administrar el modelo de permisos para las aplicaciones de, existen los dos grupos siguientes:

* administradores de aplicaciones para administradores de aplicaciones
* App-authors para autores de aplicaciones

### Autores de contenido de aplicaciones de AEM Mobile (grupo de autores de aplicaciones) {#aem-mobile-application-content-authors-app-author-group}

AEM Los miembros del grupo de creación de aplicaciones son responsables de la creación de contenido de aplicaciones móviles, incluido contenido de aplicaciones móviles, páginas, texto, imágenes y vídeos.

#### Configuración de grupo: app-authors {#group-configuration-app-authors}

1. Cree un grupo de usuarios llamado &quot;autores de aplicaciones&quot;:

   Vaya al Admin Console de usuario: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   En la consola de grupos de usuarios, seleccione el botón &quot;+&quot; para crear un grupo.

   AEM Establezca el ID de este grupo en &quot;autores de aplicaciones&quot; para indicar que es un tipo específico de grupo de usuarios de autores específico para la creación de aplicaciones móviles dentro de los dispositivos de creación de usuarios de la aplicación de creación de aplicaciones de la aplicación de la aplicación de la aplicación de creación de usuarios de la aplicación de la aplicación de.

1. Añadir miembro al grupo: Autores

   ![chlimage_1-18](assets/chlimage_1-18.png)

   Añadir autores de la aplicación al grupo Autores

1. Ahora que ha creado el grupo de usuarios Autores de la aplicación, puede añadir miembros individuales del equipo a este nuevo grupo a través del [Admin Console de usuario](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-19](assets/chlimage_1-19.png)

   Editar grupos de usuarios

1. Vaya a [Consola Permisos](http://localhost:4502/useradmin) y agregue permisos para administrar cloudservices

   * (Lectura) en /etc/cloudservices

   >[!NOTE]
   >
   >AEM Los autores de aplicaciones extienden el grupo predeterminado content-authors (Authors) de los recursos, de modo que heredan la capacidad de crear contenido en /content/phonegap

### Grupo de administradores de aplicaciones de AEM Mobile (grupo de administradores de aplicaciones) {#aem-mobile-application-administrators-group-app-admins-group}

Los miembros del grupo de administradores de aplicaciones pueden crear contenido de la aplicación con los mismos permisos incluidos con los autores de aplicaciones **Y** además, son responsables de:

* Configuración de los servicios en la nube de PhoneGap Build y Adobe AEM de Mobile Services en la
* Ensayo, publicación y borrado de actualizaciones de OTA de sincronización de contenido de la aplicación

>[!NOTE]
>
>AEM Los permisos determinan la disponibilidad de algunas acciones del usuario en el Centro de comandos de la aplicación de.
>
>Tenga en cuenta que algunas opciones no están disponibles para los autores de aplicaciones que están disponibles para los administradores de aplicaciones.

#### Configuración de grupo: administradores de aplicaciones {#group-configuration-app-admins}

1. Cree un grupo llamado administradores de aplicaciones.
1. Añada los siguientes grupos al nuevo grupo de administradores de aplicaciones:

   * content-authors
   * workflow-users

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. Vaya a [Consola Permisos](http://localhost:4502/useradmin) y agregue permisos para administrar cloudservices

   * (Leer, Modificar, Crear, Eliminar, Replicar) en /etc/cloudservices/mobileservices
   * (Leer, Modificar, Crear, Eliminar, Replicar) en /etc/cloudservices/phonegap-build

1. En la misma consola Permisos, agregue permisos para ensayo, publicar y borrar actualizaciones de contenido de la aplicación

   * (Leer, Modificar, Crear, Eliminar, Replicar) en /etc/packages/mobileapp
   * (Lectura) en /var/contentsync

   >[!NOTE]
   >
   >La replicación de paquetes se utiliza para publicar actualizaciones de la aplicación de la instancia de autor a la instancia de publicación

   >[!CAUTION]
   >
   >El acceso a /var/contentsync se deniega de forma predeterminada.
   >
   >Si se omite el permiso READ, los paquetes de actualización vacíos se pueden crear y replicar.

1. Agregar miembros a este grupo según sea necesario

## Permisos del mosaico del panel {#dashboard-tile-permissions}

Los mosaicos del panel pueden exponer diferentes acciones en función de los permisos que tenga el usuario. A continuación se describen qué acciones están disponibles para cada mosaico.

Además de estos permisos, también se puede mostrar u ocultar una acción en función de cómo esté configurada la aplicación actual. Por ejemplo, no tiene sentido exponer la acción &quot;Compilación remota&quot; si no se ha asignado una configuración de nube de PhoneGap a la aplicación. Se enumeran a continuación en &quot;**Condición de configuración**&#39; secciones.

### Administrar mosaico de aplicación {#manage-app-tile}

Actualmente, el mosaico no tiene acciones que requieran permisos. Sin embargo, la página de detalles de la aplicación tiene las siguientes acciones:

* *Editar* para app-author y app-admin (Déclencheur de interfaz de usuario - jcr:write - en /content/phonegap/{suffix})
* *Descargar* para app-author y app-admin (Déclencheur de la interfaz de usuario: en /content/phonegap/{suffix})

La siguiente imagen muestra las opciones de descarga y edición de una aplicación:

![chlimage_1-21](assets/chlimage_1-21.png)
