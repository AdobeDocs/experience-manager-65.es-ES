---
title: Configurar usuarios y grupos de usuarios
seo-title: Configurar usuarios y grupos de usuarios
description: Siga esta página para conocer las funciones de usuario y cómo configurar los usuarios y grupos para que admitan la creación y la administración de la aplicación de servicios bajo demanda móvil.
seo-description: Siga esta página para conocer las funciones de usuario y cómo configurar los usuarios y grupos para que admitan la creación y la administración de la aplicación de servicios bajo demanda móvil.
uuid: 461e1725-41dd-4883-92b9-a7e175660401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: c3c73e67-7f85-4308-b4cd-1b42d4f3f2d9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---


# Configurar usuarios y grupos de usuarios {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

En este capítulo se describen las funciones de usuario y cómo configurar los usuarios y grupos para que admitan la creación y la gestión de las aplicaciones móviles.

## Usuarios de aplicaciones y administración de grupos de AEM Mobile {#aem-mobile-application-users-and-group-administration}

### Autores de contenido de aplicaciones de AEM Mobile (grupo de creación de aplicaciones) {#aem-mobile-application-content-authors-app-author-group}

Los miembros del grupo de creación de aplicaciones son responsables de la creación AEM contenido de aplicaciones móviles, incluidas páginas, texto, imágenes y vídeos.

#### Configuración de grupo: app-author {#group-configuration-app-authors}

1. Cree un nuevo grupo de usuarios llamado &#39;app-author&#39;:

   Vaya al Admin Console de usuarios: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   Desde la consola de grupo de usuarios, seleccione el botón &#39;+&#39; para crear un grupo.

   Establezca el ID de este grupo en &#39;app-author&#39; para indicar que es un tipo específico de grupo de usuarios autores específico para la creación de aplicaciones móviles dentro de AEM.

1. Añadir miembro en grupo: Autores

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Ahora que ha creado el grupo de usuarios autores de aplicaciones, puede agregar miembros individuales del equipo a este nuevo grupo a través de la [Consola de administración de usuarios](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Lo siguiente le permite agregar a AEM grupo Autores de contenido:

   (Leído) el

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### Grupo de administradores de aplicaciones de AEM Mobile (grupo de administradores de aplicaciones) {#aem-mobile-application-administrators-group-app-admins-group}

Los miembros del grupo app-admins pueden crear contenido de aplicación con los mismos permisos incluidos con los autores de aplicaciones **AND**, además de ser responsables de:

* Ensayo, publicación y borrado de la aplicación ContentSync Actualizaciones OTA

>[!NOTE]
>
>Los permisos determinan la disponibilidad de algunas acciones de usuario en el Centro de comandos de la aplicación de AEM.
>
>Observará que algunas opciones no están disponibles para los creadores de aplicaciones que están disponibles para los administradores de aplicaciones.

### Configuración de grupo: administradores de aplicaciones {#group-configuration-app-admins}

1. Cree un nuevo grupo llamado administradores de aplicaciones.
1. Añada los siguientes grupos en su nuevo grupo de administradores de aplicaciones:

   * content-author
   * flujos de trabajo-usuarios

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >los usuarios del flujo de trabajo deben realizar la compilación remota con el servicio de PhoneGap Build

1. Vaya a la [consola de permisos](http://localhost:4502/useradmin) y agregue permisos para administrar cloudservices

   * (Leer, Modificar, Crear, Eliminar, Replicar) en /etc/cloudservices/mobileservices

1. En la misma consola Permisos, agregue permisos para realizar las actualizaciones de contenido de la aplicación en el escenario, publicarlas y borrarlas;

   * (Leer, Modificar, Crear, Eliminar, Replicar) en /etc/packages/mobileapp
   * (Leer) en /var/contentsync

   >[!NOTE]
   >
   >La replicación de paquetes se utiliza para publicar actualizaciones de aplicaciones desde la instancia de autor para publicar la instancia

   >[!CAUTION]
   >
   >Se denegó el acceso a /var/contentsync a OOTB.
   >
   >Si se omite el permiso READ, los paquetes de actualización vacíos se pueden crear y replicar.

1. Añadir miembros a este grupo según sea necesario
1. Para exportar contenido o cargar

   * (Leer) en /etc/contentsync para acceder a las plantillas de exportación
   * (Leer) en /var to para ver la ruta transversal en lecturas
   * (Leer, escribir, modificar, eliminar) en /var/contentsync para escribir, leer y limpiar contenidoSincronizar contenido de exportación en caché

### Recursos adicionales {#additional-resources}

Para obtener más información sobre las otras dos funciones y responsabilidades para crear una aplicación de AEM Mobile On-demand Services, consulte los siguientes recursos:

* [Desarrollo de contenido AEM para AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Creación de contenido AEM para la aplicación AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)
