---
title: Creación de una aplicación de AEM Mobile mediante el asistente de creación
description: Las aplicaciones de AEM Mobile se basan en un modelo que define una estructura y propiedades de página. Siga esta página para obtener más información sobre cómo crear una aplicación basada en una plantilla de aplicación.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: be093025-b19f-4499-a7b5-aae5ab74f966
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 1%

---

# Creación de una aplicación de AEM Mobile mediante el asistente de creación{#creating-a-new-aem-mobile-app-using-create-wizard}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Las aplicaciones de AEM Mobile se basan en un modelo que define una estructura y propiedades de página. Puede configurar las siguientes propiedades de la aplicación:

* **Título:** El título de la aplicación.
* **Ruta de destino:** La ubicación en el repositorio donde se almacena la aplicación. Deje el valor predeterminado para crear una ruta basada en el nombre de la aplicación.

* **Nombre:** El valor predeterminado es el valor de la propiedad Title sin los caracteres de espacio. AEM El nombre se utiliza dentro de la aplicación para hacer referencia a la aplicación, por ejemplo, para el nodo del repositorio que representa la aplicación.
* **Descripción:** Una descripción de la aplicación.
* **URL del servidor:** La dirección URL que proporciona actualizaciones de contenido OTA (Over-the-Air) en la aplicación. El valor predeterminado es la URL del servidor de publicación de la instancia que se utiliza para crear una aplicación (tomada del servicio externalizador). Tenga en cuenta que debe ser una instancia del servidor de publicación en lugar de un autor, lo que requiere autenticación.

También puede proporcionar un archivo de imagen para utilizarlo como miniatura de la aplicación, seleccionar la configuración de PhoneGap Build que desea utilizar y seleccionar la configuración de análisis de aplicaciones móviles que desea utilizar. Esta imagen solo se utiliza como miniatura para representar la aplicación móvil dentro de la consola de aplicaciones móviles en Experience Manager.

Existen pestañas adicionales (y opcionales) para crear un servicio en la nube e integrar el complemento SDK de Adobe Mobile Services en su aplicación.

* Generar: Haga clic en Administrar configuraciones y configure el servicio de compilación de build.phonegap.com aquí. A continuación, en la lista desplegable, podrá seleccionar el servicio en la nube de PhoneGap Build recién creado.
* Analytics: Haga clic en Administrar configuraciones y configure los [SDK de Adobe Mobile Services](https://experienceleague.adobe.com/docs/mobile-services/using/home.html) servicio en la nube. A continuación, en la lista desplegable, podrá seleccionar el Mobile Service recién creado para integrarlo en su aplicación móvil.

## Uso de plantillas de aplicación {#using-app-templates}

AEM Las plantillas de aplicación ofrecen una forma sencilla de utilizar los diseños existentes creados por desarrolladores y utilizados para la creación de nuevas aplicaciones dentro de los programas de desarrollo de aplicaciones de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación.

¿Qué es una plantilla de aplicación? Considérelo como una colección de plantillas de página y componentes que representan una línea de base o una base de una aplicación.
Al crear una aplicación basada en la plantilla de otra aplicación, obtiene una aplicación con un punto de partida representativo de la aplicación en la que se creó.

Debe tener una plantilla de aplicación móvil existente (o una aplicación instalada que tenga una plantilla de aplicación) para utilizar esta función.

AEM El último paquete de ejemplos de aplicaciones de la aplicación de la aplicación de la aplicación de la aplicación incluye una versión actualizada de la Geometrixx con una plantilla de aplicación. También puede instalar el [StarterKit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) que también proporciona una plantilla.

Pasos para crear una aplicación basada en una plantilla de aplicación:

1. Vaya al catálogo de aplicaciones de AEM Mobile: &lt;*server-url*>aem/apps.html/content/mobileapps
1. Seleccionar **Crear** y luego elija **Aplicación** como se muestra a continuación

![chlimage_1-158](assets/chlimage_1-158.png)

AEM Seleccione una plantilla de aplicación que un desarrollador de aplicaciones haya puesto a su disposición para que la ejecute. Consulte [Estructura de una aplicación de AEM Mobile](/help/mobile/phonegap-structure-an-app.md) para obtener ayuda del desarrollador.

![chlimage_1-159](assets/chlimage_1-159.png)

Complete los detalles de la nueva aplicación según sea necesario, incluido el cambio opcional de la imagen en miniatura. Estos valores se pueden editar más adelante desde el **Administrar aplicación** mosaico.

![chlimage_1-160](assets/chlimage_1-160.png)

## Pasos siguientes {#the-next-steps}

Consulte los siguientes recursos para obtener más información sobre otras funciones de creación:

* [El mosaico Administrar aplicación](/help/mobile/phonegap-app-details-tile.md)
* [Edición de metadatos de aplicación](/help/mobile/phonegap-editmetadata.md)
* [Definiciones de aplicación](/help/mobile/phonegap-app-definitions.md)
* [Importar una aplicación híbrida existente](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

## Recursos adicionales {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y un desarrollador, consulte los recursos siguientes:

* [Desarrollo para Adobe PhoneGap AEM Enterprise con](/help/mobile/developing-in-phonegap.md)
* [Administración de contenido para Adobe PhoneGap AEM Enterprise con el servicio de administración de](/help/mobile/administer-phonegap.md)
