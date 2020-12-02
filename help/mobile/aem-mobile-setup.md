---
title: AEM Mobile SetUp
seo-title: AEM Mobile SetUp
description: Siga esta página para configurar AEM Mobile y permitir así al usuario crear y administrar el contenido dentro de AEM. Esta página proporciona información sobre la integración de la instancia de AEM con la cuenta y los proyectos de AEM Mobile On-demand Services basados en la nube.
seo-description: Siga esta página para configurar AEM Mobile y permitir así al usuario crear y administrar el contenido dentro de AEM. Esta página proporciona información sobre la integración de la instancia de AEM con la cuenta y los proyectos de AEM Mobile On-demand Services basados en la nube.
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 1%

---


# AEM Mobile SetUp{#aem-mobile-setup}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>Los clientes existentes de aplicaciones de AEM Mobile que migran de AEM 6.2 o 6.3 a AEM 6.5 pueden seguir utilizando aplicaciones de AEM Mobile descargando un [paquete de PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/compatpack/aem-mobile-package). Sin embargo, las nuevas instalaciones de AEM 6.5 no admitirán la funcionalidad de las aplicaciones de AEM Mobile.

Para utilizar AEM para producir contenido para las aplicaciones de AEM Mobile, debe integrar la instancia de AEM con la cuenta y los proyectos de AEM Mobile On-demand Services basados en la nube.

Siga estos pasos para configurar AEM Mobile y permitir así al usuario crear y administrar el contenido dentro de AEM.

## Aprovisionamiento de AEM Mobile {#aem-mobile-provisioning}

Para comenzar con la configuración de AEM Mobile, debe:

* **Solicitar una clave** de API: Para acceder a la On-Demand Services API, debe solicitar una clave de API. Para solicitar la clave de API, complete el [formulario PDF](https://helpx.adobe.com/digital-publishing-solution/help/integrating-dps.html). Envíe el formulario completado a la asistencia para desarrolladores de Adobe: [wwds@adobe.com](mailto:wwds@adobe.com)

* **Genere el ID del dispositivo y el autentificador** del dispositivo: Una vez que haya recibido la clave de API, puede generar el ID del dispositivo y el autentificador del dispositivo. Vaya a [https://aex.aemmobile.adobe.com](https://aex.aemmobile.adobe.com/) y haga lo siguiente:

   * Proporcione la clave de API
   * Inicie sesión con un Adobe ID que haya agregado a un proyecto de AEM Mobile con los permisos siguientes (consulte los pasos a continuación para crear un proyecto)

      * Administración > Administrar proyectos y usuarios
      * Contenido > Añadir y editar contenido, eliminar contenido, Vista de contenido, publicar contenido

Si se cumplen todas las condiciones, se generarán un ID de dispositivo y un autentificador de dispositivo.

>[!NOTE]
>
>Se debe conceder acceso al Adobe ID necesario en un proyecto de AEM Mobile. Consulte [Administración de cuentas para AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) en la Ayuda en línea.

## Creación de proyectos para AEM Mobile {#creating-projects-for-aem-mobile}

Al crear un proyecto, debe especificar la configuración de cualquier plataforma que esté estableciendo como objetivo: Visor web de iOS, Android, Windows y escritorio. Muchos de los ajustes del proyecto que especifique afectan al comportamiento de la aplicación.

La creación de un proyecto requiere que inicie sesión en el portal de servicios bajo demanda con un Adobe ID que tenga una función de administrador maestro. La edición de un proyecto requiere una función de administrador maestro o una función de usuario con un permiso **Administrar proyectos y usuarios**.

>[!NOTE]
>
>Para obtener más información sobre la creación de proyectos en AEM Mobile, haga clic [aquí](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## Configuración de un conector de AEM Mobile {#configuring-an-aem-mobile-connector}

AEM configuración implica los siguientes pasos para la configuración del conector. Una vez completada la configuración del conector de AEM Mobile, el usuario puede configurar grupos de usuarios y permisos.

El conector On-Demand de AEM Mobile se utiliza para enlazar contenido administrado por AEM Mobile con los servicios On-Demand Services de Adobe Experience Manager Mobile. Esto permite a los autores de contenido crear y administrar material para aplicaciones móviles mediante las herramientas de AEM, mientras que utilizan los servicios On-Demand Services de AEM Mobile para una distribución sencilla del contenido móvil.

>[!NOTE]
>
>Éste es un paso único para configurar la instancia de AEM.

### Configuración del cliente de AEM Mobile On-demand Services {#configuring-aem-mobile-on-demand-services-client}

Debe completar los pasos de configuración para que las integraciones de AEM Mobile funcionen correctamente.

1. Ir a la configuración del servicio OSGI

   1. AEM > Herramientas > Operaciones > Consola web
   1. Desplácese o busque ***Experience Manager Mobile On-demand Services Client (era Adobe Digital Publishing Solution Client)***

1. Editar ***Experience Manager Mobile On-demand Services Client***

   1. **(Obligatorio)** Introduzca los campos obligatorios:

      1. ID del cliente.
      1. Secreto del cliente.
   1. **(Opcional)** Edite los valores existentes.


1. Guarde los cambios.
1. A continuación se muestra un ejemplo de configuración:

![chlimage_1-53](assets/chlimage_1-53.png)

### Configuración de AEM Mobile On-demand Services CloudService {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Ir a Cloud Services

   1. AEM > Herramientas > Implementación> [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). Desplácese o busque ***Adobe Experience Manager Mobile On-demand Services***

1. Seleccione ***Configurar ahora*** o ***Mostrar configuraciones*** y seleccione el icono Agregar nueva configuración

1. Crear una nueva configuración

   1. Escriba un título y un nombre
   1. Especifique el ID del dispositivo
   1. Especifique el autentificador del dispositivo
   1. Seleccione ***Probar configuración del dispositivo*** para validar los valores introducidos
   1. Seleccionar Aceptar

## Añadir las funciones de usuario de AEM Mobile y asignar permisos {#adding-aem-mobile-user-roles-and-assigning-permissions}

Después de crear un proyecto, debe crear funciones y conceder acceso a los usuarios. Solo los administradores principales pueden crear y editar funciones. Al crear una función, se habilitan las capacidades (o permisos) para los usuarios a los que se asignen dichos permisos. Por ejemplo, puede crear una función que incluya permisos para la creación de aplicaciones y otra que incluya permisos para crear y publicar contenido.

En el desarrollo de aplicaciones de AEM Mobile, existen tres funciones diferentes:

* Administrador
* Desarrollador
* Autor

Para obtener más información sobre la creación de funciones con diferentes permisos, como para la creación de aplicaciones o para crear y publicar contenido, haga clic en [Creación de funciones de usuario y concesión de acceso](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) en la Ayuda de AEM Mobile.

>[!NOTE]
>
>La administración del contenido de la aplicación requiere un esfuerzo colectivo de los desarrolladores, autores de contenido y administradores. Los autores manipulan las páginas, que a su vez se basan en plantillas y componentes generados por los desarrolladores de la aplicación. Por último, los administradores publican estratégicamente el contenido actualizado de la aplicación. La configuración de AEM Grupos y permisos define sus funciones en el Panel de la aplicación o en el Centro de control.
>
>Para obtener más información sobre AEM Mobile Panel, haga clic [aquí](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

Una vez que haya terminado de crear funciones con diferentes permisos, como para la creación de aplicaciones o para crear y publicar contenido, consulte [**Configurar los grupos de usuarios y usuarios**](/help/mobile/aem-mobile-configure-users.md) para configurar los usuarios y grupos de modo que admitan la creación y la gestión de las aplicaciones móviles.

### Recursos adicionales {#additional-resources}

Para obtener más información sobre las otras dos funciones y responsabilidades para crear una aplicación de AEM Mobile On-demand Services, consulte los siguientes recursos:

* [Desarrollo de contenido AEM para AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Creación de contenido AEM para la aplicación AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>Para realizar la previsualización del contenido de la aplicación, incluidas las páginas de búsqueda y los artículos, consulte [Vista previa con verificación previa](/help/mobile/aem-mobile-manage-ondemand-services.md).
