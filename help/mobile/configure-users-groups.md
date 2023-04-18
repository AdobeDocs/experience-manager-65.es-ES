---
title: Configuración de usuarios y grupos de usuarios
description: Siga esta página para comprender las funciones de usuario y cómo configurar los usuarios y grupos para que admitan la creación y administración de sus aplicaciones móviles.
uuid: 55cea2b3-d7e6-4174-92b3-ee97e46b59c4
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 167f3bd9-7dbc-4e6b-9868-3ee53935641b
exl-id: 9f814204-8cd4-4ba9-9e25-3ff1b25c1955
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# Configurar usuarios y grupos de usuarios {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

En este capítulo se describen las funciones de usuario y cómo configurar los usuarios y grupos para que admitan la creación y administración de sus aplicaciones móviles.

## Usuarios de aplicaciones de AEM Mobile y administración de grupos {#aem-mobile-application-users-and-group-administration}

Para ayudar a organizar y administrar el modelo de permisos para AEM aplicaciones, están disponibles los dos grupos siguientes:

* administradores de aplicaciones para administradores de aplicaciones
* autores de aplicaciones para autores de aplicaciones

### Autores de contenido de aplicaciones de AEM Mobile (grupo de autores de aplicaciones) {#aem-mobile-application-content-authors-app-author-group}

Los miembros del grupo de creación de aplicaciones son responsables de la creación AEM contenido de aplicaciones móviles, incluidas páginas, texto, imágenes y vídeos.

#### Configuración de grupo: app-authors {#group-configuration-app-authors}

1. Cree un nuevo grupo de usuarios llamado &quot;app-authors&quot;:

   Vaya al Admin Console de usuario: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   Desde la consola de grupos de usuarios, seleccione el botón &quot;+&quot; para crear un grupo.

   Establezca el ID de este grupo en &quot;autores de aplicaciones&quot; para indicar que es un tipo específico de grupo de usuarios de autor específico para la creación de aplicaciones móviles en AEM.

1. Agregar miembro al grupo: Autores

   ![chlimage_1-18](assets/chlimage_1-18.png)

   Agregar autores de aplicaciones al grupo Autores

1. Ahora que ha creado el grupo de usuarios de autores de aplicaciones, puede agregar miembros individuales del equipo a este nuevo grupo a través del [Consola de administración de usuarios](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-19](assets/chlimage_1-19.png)

   Editar grupos de usuarios

1. Vaya a la [Consola de permisos](http://localhost:4502/useradmin) y agregar permisos para administrar cloudservices

   * (Leído) en /etc/cloudservices
   >[!NOTE]
   >
   >Autores de aplicaciones amplía el grupo predeterminado de autores de contenido (autores) de AEM heredando así la capacidad de crear contenido en /content/phonegap

### Grupo de administradores de aplicaciones de AEM Mobile (grupo de administradores de aplicaciones) {#aem-mobile-application-administrators-group-app-admins-group}

Los miembros del grupo de administradores de aplicaciones pueden crear contenido de aplicación con los mismos permisos incluidos con los autores de aplicaciones **Y** además son responsables de:

* Configuración de los servicios en la nube de PhoneGap Build y Adobe Mobile Services en AEM
* Ensayo, publicación y limpieza de las actualizaciones de OTA de sincronización de contenido de la aplicación

>[!NOTE]
>
>Los permisos determinan la disponibilidad de algunas acciones del usuario en el Centro de comandos de la aplicación AEM.
>
>Verá que algunas opciones no están disponibles para los autores de aplicaciones que están disponibles para los administradores de aplicaciones.

#### Configuración de grupo: administradores de aplicaciones {#group-configuration-app-admins}

1. Cree un nuevo grupo llamado administradores de aplicaciones.
1. Agregue los siguientes grupos a su nuevo grupo de administradores de aplicaciones:

   * content-authors
   * workflow-users

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. Vaya a la [Consola de permisos](http://localhost:4502/useradmin) y agregar permisos para administrar cloudservices

   * (Leer, Modificar, Crear, Eliminar, Replicar) en /etc/cloudservices/mobileservices
   * (Leer, Modificar, Crear, Eliminar, Replicar) en /etc/cloudservices/phonegap-build

1. En la misma consola de permisos, agregue permisos a las actualizaciones de contenido de la aplicación de ensayo, publicación y borrado.

   * (Leer, Modificar, Crear, Eliminar, Replicar) en /etc/packages/mobileapp
   * (Leído) en /var/contentsync

   >[!NOTE]
   >
   >La duplicación de paquetes se utiliza para publicar actualizaciones de aplicaciones de la instancia de autor para publicar instancias

   >[!CAUTION]
   >
   >El acceso a /var/contentsync está denegado a OOTB.
   >
   >Omitir el permiso READ puede resultar en la creación y replicación de paquetes de actualización vacíos.

1. Agregue miembros a este grupo según sea necesario

## Permisos del mosaico del panel {#dashboard-tile-permissions}

Los mosaicos de tablero pueden exponer diferentes acciones en función de los permisos que tenga el usuario. A continuación se describen las acciones disponibles para cada mosaico.

Además de estos permisos, también se puede mostrar u ocultar una acción en función de cómo esté configurada la aplicación actual. Por ejemplo, no tiene sentido exponer la acción &quot;Compilación remota&quot; si no se ha asignado una configuración de nube de PhoneGap a la aplicación. Se enumerarán a continuación en &#39;**Condición de configuración**&#39;.

### Administrar mosaico de aplicación {#manage-app-tile}

El mosaico no tiene actualmente ninguna acción que requiera permisos. Sin embargo, la página de detalles de la aplicación tiene las siguientes acciones:

* *Editar* para app-author y app-admin (Déclencheur de IU - jcr:write - en /content/phonegap/{suffix})
* *Descargar* para app-author y app-admin (Déclencheur de IU en /content/phonegap/{suffix})

La imagen siguiente muestra las opciones de descarga y edición de una aplicación:

![imagen_1-21](assets/chlimage_1-21.png)
