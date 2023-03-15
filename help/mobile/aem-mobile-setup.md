---
title: Configuración de AEM Mobile
seo-title: AEM Mobile SetUp
description: Siga esta página para configurar AEM Mobile y permitir así al usuario crear y administrar el contenido dentro de AEM. Esta página proporciona información sobre la integración de la instancia de AEM con la cuenta de AEM Mobile On-demand Services basada en la nube y los proyectos.
seo-description: Follow this page for setting up AEM Mobile and thus allowing the user to create and manage the content within AEM. This page provides information on integrating the AEM instance with the cloud-based AEM Mobile On-Demand Services account and project(s).
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 2%

---

# Configuración de AEM Mobile{#aem-mobile-setup}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>Los clientes existentes de aplicaciones de AEM Mobile que migran de AEM 6.2 o 6.3 a AEM 6.5 pueden seguir utilizando aplicaciones de AEM Mobile descargando un [paquete de PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/compatpack/aem-mobile-package). Sin embargo, las nuevas instalaciones de AEM 6.5 no admitirán la funcionalidad Aplicaciones de AEM Mobile.

Para utilizar AEM para producir contenido para aplicaciones de AEM Mobile, debe integrar la instancia de AEM con la cuenta y los proyectos de AEM Mobile On-demand Services basados en la nube.

Siga estos pasos para configurar AEM Mobile y permitir al usuario crear y administrar el contenido dentro de AEM.

## Aprovisionamiento de AEM Mobile {#aem-mobile-provisioning}

Para empezar a utilizar la configuración de AEM Mobile, debe:

* **Solicitar una clave de API**: Para acceder a la API de servicios bajo demanda, debe solicitar una clave de API. Para solicitar la clave de API, complete la [formulario de PDF](https://helpx.adobe.com/digital-publishing-solution/help/integrating-dps.html). Envíe el formulario completado al equipo de asistencia de Adobe Developer: [wwds@adobe.com](mailto:wwds@adobe.com)

* **Generar el ID del dispositivo y el token del dispositivo**: Una vez que haya recibido la clave de API, puede generar el ID del dispositivo y el token del dispositivo. Vaya a [https://aex.aemmobile.adobe.com](https://aex.aemmobile.adobe.com/) y haga lo siguiente:

   * Proporcione la clave de API
   * Inicie sesión con un Adobe ID que haya agregado a un proyecto de AEM Mobile con los siguientes permisos (consulte los pasos a continuación para crear el proyecto)

      * Administración > Administrar proyectos y usuarios
      * Contenido > Agregar y editar contenido, eliminar contenido, ver contenido, publicar contenido

Si se cumplen todas las condiciones, se generarán un ID de dispositivo y un token de dispositivo.

>[!NOTE]
>
>Se debe conceder acceso a Adobe ID necesario en un proyecto de AEM Mobile. Consulte [Administración de cuentas para AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) en la Ayuda en línea.

## Creación de proyectos para AEM Mobile {#creating-projects-for-aem-mobile}

Al crear un proyecto, se especifica la configuración de cualquier plataforma a la que se dirija: Visor web de iOS, Android, Windows y escritorio. Muchas de las opciones del proyecto que especifique afectarán al comportamiento de la aplicación.

Para crear un proyecto es necesario iniciar sesión en el portal de servicios bajo demanda con un Adobe ID que tenga una función de administrador maestro. La edición de un proyecto requiere un rol de administrador maestro o un rol de usuario con un **Administrar proyectos y usuarios** permiso.

>[!NOTE]
>
>Para obtener más información sobre la creación de proyectos en AEM Mobile, haga clic en [here](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## Configuración de un conector de AEM Mobile {#configuring-an-aem-mobile-connector}

AEM configuración implica los siguientes pasos para la configuración del conector. Una vez completada la configuración del conector de AEM Mobile, el usuario puede configurar grupos de usuarios y permisos.

El conector AEM Mobile On-Demand se utiliza para enlazar contenido administrado por AEM Mobile con los servicios On-Demand de Adobe Experience Manager Mobile. Esto permite a los autores de contenido crear y administrar material para aplicaciones móviles mediante las herramientas de AEM mientras utilizan los servicios On-Demand de AEM Mobile para una distribución sencilla del contenido móvil.

>[!NOTE]
>
>Este es un paso único para configurar la instancia de AEM.

### Configuración del cliente de AEM Mobile On-demand Services {#configuring-aem-mobile-on-demand-services-client}

Debe completar los pasos de configuración para que las integraciones de AEM Mobile funcionen correctamente.

1. Vaya a la configuración del servicio OSGI

   1. AEM > Herramientas > Operaciones > Consola web
   1. Desplácese o busque ***Experience Manager Mobile On Demand Services Client (era cliente de Adobe Digital Publishing Solution)***

1. Editar ***Experience Manager Mobile On Demand Services Client***

   1. **(Obligatorio)** Introduzca los campos obligatorios:

      1. ID del cliente.
      1. Secreto de cliente.
   1. **(Opcional)** Edite los valores existentes.


1. Guarde los cambios.
1. A continuación se muestra un ejemplo de configuración:

![imagen_1-53](assets/chlimage_1-53.png)

### Configuración de AEM Mobile On-demand Services Cloud Service {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Ir a Cloud Services

   1. AEM > Herramientas > Implementación > [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). Desplácese o busque ***Servicios bajo demanda de Adobe Experience Manager Mobile***

1. Select ***Configurar ahora*** o ***Mostrar configuraciones*** y seleccione el icono agregar nueva configuración

1. Crear una nueva configuración

   1. Introduzca un título y un nombre
   1. Introducir ID de dispositivo
   1. Introducir token de dispositivo
   1. Select ***Probar la configuración del dispositivo*** para validar los valores introducidos
   1. Seleccione Aceptar

## Adición de funciones de usuario de AEM Mobile y asignación de permisos {#adding-aem-mobile-user-roles-and-assigning-permissions}

Después de crear un proyecto, debe crear funciones y conceder acceso a los usuarios. Solo los administradores principales pueden crear y editar funciones. Al crear una función, se habilitan capacidades (o permisos) para los usuarios a los que se asignen dichos permisos. Por ejemplo, puede crear una función que incluya permisos para la creación de aplicaciones y otra que incluya permisos para la creación y publicación de contenido.

En el desarrollo de aplicaciones de AEM Mobile, existen tres funciones diferentes:

* Administrador
* Desarrollador
* Autor

Para obtener más información sobre la creación de funciones con diferentes permisos, como para la creación de aplicaciones o para la creación y publicación de contenido, haga clic en [Creación de funciones de usuario y concesión de acceso](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) en la Ayuda de AEM Mobile.

>[!NOTE]
>
>La gestión del contenido de la aplicación requiere el esfuerzo colectivo de los desarrolladores, los autores de contenido y los administradores. Los autores manipulan las páginas, que a su vez se basan en plantillas y componentes generados por los desarrolladores de aplicaciones. Por último, los administradores publican estratégicamente el contenido actualizado de la aplicación. La configuración de AEM Grupos y permisos define sus funciones en el panel de la aplicación o en el centro de control.
>
>Para obtener más información sobre el panel de AEM Mobile, haga clic en [here](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

Una vez que haya terminado de crear funciones con diferentes permisos, como para la creación de aplicaciones o para crear y publicar contenido, consulte [**Configurar los grupos de usuarios y usuarios**](/help/mobile/aem-mobile-configure-users.md) para configurar los usuarios y grupos de modo que admitan la creación y administración de sus aplicaciones móviles.

### Recursos adicionales {#additional-resources}

Para obtener más información sobre las otras dos funciones y responsabilidades para crear una aplicación de AEM Mobile On-demand Services, consulte los siguientes recursos:

* [Desarrollo de contenido de AEM para AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Creación de contenido AEM para aplicaciones de AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>Para obtener una vista previa del contenido de la aplicación, incluidas las páginas de navegación y los artículos, consulte [Vista previa con comprobación preliminar](/help/mobile/aem-mobile-manage-ondemand-services.md).
