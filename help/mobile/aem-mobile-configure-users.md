---
title: Configuración de usuarios y grupos de usuarios
description: Siga esta página para comprender las funciones de usuario y cómo configurar los usuarios y grupos para que admitan la creación y administración de la aplicación de Mobile On-Demand Services.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
exl-id: 58b7d1b9-a851-442a-9d02-212cad8abbed
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Configuración de usuarios y grupos de usuarios {#configure-your-users-and-user-groups}

{{ue-over-mobile}}

En este capítulo se describen las funciones de usuario y cómo configurar los usuarios y grupos para que admitan la creación y administración de sus aplicaciones móviles.

## Administración de grupos y usuarios de aplicaciones AEM Mobile {#aem-mobile-application-users-and-group-administration}

### Autores de contenido de aplicaciones de AEM Mobile (grupo de autores de aplicaciones) {#aem-mobile-application-content-authors-app-author-group}

AEM Los miembros del grupo de creación de aplicaciones son responsables de la creación de contenido de aplicaciones móviles, incluido contenido de aplicaciones móviles, páginas, texto, imágenes y vídeos.

#### Configuración de grupo: app-authors {#group-configuration-app-authors}

1. Cree un grupo de usuarios llamado &quot;autores de aplicaciones&quot;:

   Vaya al Admin Console de usuario: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   En la consola de grupos de usuarios, seleccione el botón &quot;+&quot; para crear un grupo.

   AEM Establezca el ID de este grupo en &quot;autores de aplicaciones&quot; para indicar que es un tipo específico de grupo de usuarios de autores específico para la creación de aplicaciones móviles dentro de los dispositivos de creación de usuarios de la aplicación de creación de aplicaciones de la aplicación de la aplicación de la aplicación de creación de usuarios de la aplicación de la aplicación de.

1. Añadir miembro al grupo: Autores

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Ahora que ha creado el grupo de usuarios de autores de aplicaciones, puede agregar integrantes individuales del equipo a este nuevo grupo a través de [Admin Console de usuarios](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. AEM A continuación, se permite agregar al grupo Autores de contenido de:

   (Lectura) el

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### Grupo de administradores de aplicaciones de AEM Mobile (grupo de administradores de aplicaciones) {#aem-mobile-application-administrators-group-app-admins-group}

Los miembros del grupo de administradores de aplicaciones pueden crear contenido de aplicación con los mismos permisos incluidos con los autores de aplicaciones **Y**. Además, también son responsables de lo siguiente:

* Actualizaciones OTA de ContentSync de ensayo, publicación y borrado de la aplicación

>[!NOTE]
>
>AEM Los permisos determinan la disponibilidad de algunas acciones del usuario en el Centro de comandos de la aplicación de.
>
>Tenga en cuenta que algunas opciones no están disponibles para los autores de aplicaciones que están disponibles para los administradores de aplicaciones.

### Configuración de grupo: administradores de aplicaciones {#group-configuration-app-admins}

1. Cree un grupo llamado administradores de aplicaciones.
1. Añada los siguientes grupos al nuevo grupo de administradores de aplicaciones:

   * content-authors
   * workflow-users

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >los usuarios del flujo de trabajo deben realizar la compilación remota con el servicio de PhoneGap Build

1. Vaya a la consola [Permisos](http://localhost:4502/useradmin) y agregue permisos para administrar cloudservices

   * (Leer, Modificar, Crear, Eliminar, Replicar) en /etc/cloudservices/mobileservices

1. En la misma consola Permisos, agregue permisos para almacenar en zona intermedia, publicar y borrar actualizaciones de contenido de la aplicación.

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
1. Para exportar contenido o cargar

   * (Lectura) en /etc/contentsync para acceder a las plantillas de exportación
   * (Lectura) en /var a recorrido de ruta en lecturas
   * (Leer, Escribir, Modificar, Eliminar) en /var/contentsync para escribir, leer y limpiar contenido de exportación en caché de ContentSync

### Recursos adicionales {#additional-resources}

Para obtener más información sobre las otras dos funciones y responsabilidades a la hora de crear una aplicación de AEM Mobile On-demand Services, consulte los siguientes recursos:

* [AEM Desarrollo de contenido para AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [AEM Creación de contenido de la aplicación de para AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)
