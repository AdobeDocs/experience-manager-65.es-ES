---
title: Creación de una nueva aplicación de AEM Mobile mediante el asistente para crear
seo-title: Creación de una nueva aplicación de AEM Mobile mediante el asistente para crear
description: Las aplicaciones de AEM Mobile se basan en un modelo que define una estructura de página y propiedades. Siga esta página para obtener información sobre cómo crear una aplicación nueva basada en una plantilla de aplicación.
seo-description: Las aplicaciones de AEM Mobile se basan en un modelo que define una estructura de página y propiedades. Siga esta página para obtener información sobre cómo crear una aplicación nueva basada en una plantilla de aplicación.
uuid: c2bd63a5-3dff-4a72-b1fb-0c776e0afa33
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 27605eb7-59b2-42d4-8cc5-02cfa52b4491
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Creación de una nueva aplicación de AEM Mobile mediante el asistente para crear{#creating-a-new-aem-mobile-app-using-create-wizard}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Las aplicaciones de AEM Mobile se basan en un modelo que define una estructura de página y propiedades. Puede configurar las siguientes propiedades de la aplicación:

* **** Título: El título de la aplicación.
* **** Ruta de destino: Ubicación en el repositorio donde se almacena la aplicación. Deje el valor predeterminado para crear una ruta basada en el nombre de la aplicación.

* **** Nombre: El valor predeterminado es el valor de la propiedad Title con caracteres de espacio eliminados. El nombre se utiliza en AEM para hacer referencia a la aplicación, por ejemplo, para el nodo de repositorio que representa la aplicación.
* **** Descripción: Descripción de la aplicación.
* **** URL del servidor: La URL que proporciona actualizaciones de contenido de Over-the-Air (OTA) a la aplicación. El valor predeterminado es la URL del servidor de publicación de la instancia que se utiliza para crear una aplicación (tomada del servicio de externalización). Tenga en cuenta que debe ser una instancia de servidor de publicación en lugar de un autor, lo que requiere autenticación.

También puede proporcionar un archivo de imagen para utilizarlo como miniatura de la aplicación, seleccionar la configuración de PhoneGap Build que se va a utilizar y seleccionar la configuración de análisis de aplicaciones móviles que se va a usar. Esta imagen solo se utiliza como miniatura para representar la aplicación móvil en la consola de aplicaciones móviles de Experience Manager.

Existen fichas adicionales (y opcionales) para crear el servicio en la nube e integrar el complemento SDK de Adobe Mobile Services en la aplicación.

* Generar: Haga clic en Administrar configuraciones y configure el servicio de compilación build.phonegap.com aquí. A continuación, desde la lista desplegable podrá seleccionar el servicio en la nube PhoneGap recién creado.
* Analytics: Haga clic en administrar configuraciones y configure el servicio en la nube del SDK [de](https://marketing.adobe.com/developer/en_US/get-started/mobile/c-measuring-mobile-applications) Adobe Mobile Services. A continuación, desde la lista desplegable, podrá seleccionar el servicio móvil recién creado para integrarlo en su aplicación móvil.

## Uso de plantillas de aplicación {#using-app-templates}

Las plantillas de aplicación proporcionan una manera sencilla de aprovechar los diseños existentes creados por los desarrolladores, que se utilizan para crear nuevas aplicaciones en AEM.

¿Qué es una plantilla de aplicación? Considérela como una colección de plantillas de página y componentes que representan una línea de base o una base de una aplicación.
Al crear una aplicación nueva basada en la plantilla de otra aplicación, obtendrá una aplicación que tenga un punto de partida representativo de la aplicación desde la que se creó.

Debe tener una plantilla de aplicación móvil existente (o una aplicación instalada que tenga una plantilla de aplicación) para utilizar esta función.

El último paquete de ejemplos de aplicaciones AEM incluye una versión actualizada de la aplicación Geometrixx con una plantilla de aplicación. También puede instalar [StarterKit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) , que también proporciona una plantilla.

Pasos para crear una aplicación nueva basada en una plantilla de aplicación:

1. Vaya al catálogo de aplicaciones de AEM Mobile: &lt;*server-url*>aem/apps.html/content/mobileapps
1. Seleccione **Crear** y, a continuación, elija **Aplicación** como se muestra a continuación

![chlimage_1-158](assets/chlimage_1-158.png)

Seleccione una plantilla de aplicación que haya puesto a su disposición un desarrollador de AEM. Consulte [Estructura de una aplicación](/help/mobile/phonegap-structure-an-app.md) de AEM Mobile para obtener ayuda para desarrolladores.

![chlimage_1-159](assets/chlimage_1-159.png)

Complete los detalles de la nueva aplicación según sea necesario, incluido el cambio opcional de la imagen en miniatura. Estos valores se pueden editar posteriormente desde el mosaico **Administrar aplicación** .

![chlimage_1-160](assets/chlimage_1-160.png)

## Pasos siguientes {#the-next-steps}

Consulte los siguientes recursos para obtener más información sobre otras funciones de creación:

* [El icono Administrar aplicación](/help/mobile/phonegap-app-details-tile.md)
* [Edición de metadatos de la aplicación](/help/mobile/phonegap-editmetadata.md)
* [Definiciones de aplicaciones](/help/mobile/phonegap-app-definitions.md)
* [Importar una aplicación híbrida existente](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

## Additional Resources {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y un desarrollador, consulte los siguientes recursos:

* [Desarrollo para Adobe PhoneGap Enterprise con AEM](/help/mobile/developing-in-phonegap.md)
* [Administración de contenido para Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)
