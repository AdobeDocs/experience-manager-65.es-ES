---
title: Creación de aplicaciones móviles
seo-title: Creación de aplicaciones móviles
description: El panel de AEM Mobile le permite crear, crear e implementar la aplicación móvil, crear, eliminar y editar los metadatos de la aplicación. Siga esta página para obtener más información.
seo-description: El panel de AEM Mobile le permite crear, crear e implementar la aplicación móvil, crear, eliminar y editar los metadatos de la aplicación. Siga esta página para obtener más información.
uuid: 293b5d29-df7e-42dd-ae64-8c677317e7a5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: abfeea65-102d-4800-abeb-304d61afcc13
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Creación de aplicaciones móviles{#authoring-mobile-applications}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

El panel de AEM Mobile le permite crear, crear e implementar la aplicación móvil, crear, eliminar y editar los metadatos de la aplicación. Una vez que la aplicación esté activa, puede analizar los análisis de las aplicaciones, incluidas las métricas de ciclo de vida y uso, para mejorar la conversión del cliente y la lealtad de la marca.

Para crear la aplicación de AEM Mobile, consulte la página [Creación de aplicaciones](/help/mobile/building-app-mobile-phonegap.md) móviles.

Para configurar su entorno y empezar, consulte [Administración de AEM para utilizar AEM PhoneGap Enterprise](/help/mobile/administer-phonegap.md).

## Catálogo de aplicaciones de AEM Mobile {#the-aem-mobile-apps-catalog}

El catálogo [de aplicaciones de](http://localhost:4502/aem/apps.html/content/phonegap) AEM Mobile muestra toda la aplicación móvil gestionada en AEM.

Considere este catálogo como la &quot;página de aterrizaje&quot; para AEM Mobile, donde los administradores pueden iniciar una nueva aplicación de AEM Mobile creando una aplicación basada en una plantilla o cargando una aplicación existente ya iniciada por un desarrollador móvil.

Siga estos pasos para acceder a la página de destino del catálogo de aplicaciones:

1. Vaya a **Navegación** y, a continuación, elija **Móvil**.

1. Elija **Aplicaciones** para abrir el catálogo de aplicaciones.

![Catálogo de aplicaciones de AEM Mobile](assets/chlimage_1-135.png)

## Panel de aplicaciones de AEM Mobile {#the-aem-mobile-app-dashboard}

Al seleccionar una aplicación de AEM Mobile del catálogo, se mostrará su panel. Aquí puede administrar la aplicación, ver las estadísticas, crear, implementar y administrar el contenido de la aplicación móvil.

Puede expandirse a cada mosaico en el panel de AEM Mobile para ver o editar los detalles haciendo clic en el botón &#39;..&#39; en la esquina inferior derecha.

![Centro de comandos de aplicaciones de AEM Mobile](assets/chlimage_1-136.png)

### El icono Administrar aplicación {#the-manage-app-tile}

El icono Administrar mosaico de aplicaciones muestra el icono de la aplicación, el nombre, la descripción, las plataformas admitidas y la llamada a casa para obtener información sobre la versión y la URL de las actualizaciones. Puede profundizar en este mosaico para editar y mantener la Configuración de la aplicación PhoneGap (config.xml) y preparar la aplicación para su envío a los distintos almacenes de aplicaciones para su distribución.

Haga clic [aquí](/help/mobile/phonegap-app-details-tile.md) para obtener más detalles.

![chlimage_1-137](assets/chlimage_1-137.png)

### Mosaico Administrar contenido de página {#the-manage-page-content-tile}

El contenido se puede crear, actualizar y eliminar en AEM Mobile del mismo modo que en los sitios de AEM. El icono **Administrar contenido de página** muestra el número de páginas de contenido administrado y modificadas por última vez. Puede profundizar en el contenido para crear, copiar, mover, eliminar y actualizar páginas haciendo clic en cada registro del mosaico. Una vez que el contenido se haya actualizado, puede insertar una actualización de contenido para sus clientes a través del icono **Administrar paquetes de contenido.**

![Mosaico de contenido](assets/chlimage_1-138.png)

### Mosaico Administrar paquetes de contenido {#the-manage-content-packages-tile}

Una vez que haya agregado o modificado el contenido a través del icono Administrar contenido de página, podrá insertar estos cambios en los clientes con una actualización de la versión de contenido.

Content Package permite que AEM App Author administre el contenido de la página en AEM y que su equipo de desarrollo realice cambios en la aplicación de shell de PhoneGap (es decir, el marco de aplicaciones o la infraestructura) y, a continuación, envíe esos cambios a sus clientes rápidamente y sin necesidad de solicitar a un desarrollador que vuelva a enviarlos a las distintas tiendas para su distribución.

Content Package crea un archivo ZIP, considerado un paquete de revisión de contenido, para cada actualización. Estos paquetes contienen recursos HTML y páginas HTML que se generan al procesar la aplicación y son lo suficientemente inteligentes como para empaquetar solo los archivos que se han modificado desde la última actualización.

La columna Administrar el **tipo** del mosaico del paquete de contenido mostrará &quot;Aplicación&quot; para indicar el contenido del shell de la aplicación, por ejemplo, el marco o la infraestructura de la aplicación administrada por un desarrollador o, &quot;Contenido&quot;, que representa el contenido de la página administrado por el autor del contenido.

El contenido se puede representar como un idioma o como una parte concreta de la aplicación en la que la aplicación consume varios paquetes de la versión de contenido. La elección de cómo empaqueta el contenido está diseñada para ser flexible y para adaptarse a la forma en que desee administrar el contenido de su aplicación.

La columna **Modificado** indica cuándo se modificaron las páginas más recientemente.

La columna **Ensayo** muestra cuándo se creó la última actualización de contenido. Para crear una nueva actualización de contenido y realizar los cambios, abra cualquier registro del mosaico y cree una nueva actualización.

La columna **Publicado** muestra cuándo se publicó la última actualización de contenido y cuándo los clientes la pusieron a disposición para su consumo. Para publicar contenido, primero debe realizar la fase de ese contenido y, a continuación, publicar la actualización mediante la exploración en profundidad en este mosaico y la publicación desde la consola de detalles de la publicación de contenido.

![Paquete Content Release Tile](assets/chlimage_1-139.png) ![ContentSync para el shell de la aplicación](do-not-localize/chlimage_1-5.png)

Este icono representa un paquete de la versión de contenido para el shell de la aplicación

![](do-not-localize/chlimage_1-6.png)

Estos iconos representan un paquete de la versión de contenido para el contenido de la aplicación

### Mosaico de PhoneGap Build {#the-phonegap-build-tile}

El icono **de** PhoneGap Build se conecta con [https://build.phonegap.com](https://build.phonegap.com) para crear y alojar buids remotos. Una vez compilada, la compilación está disponible como descarga o directamente en el dispositivo a través de un código QR.

También puede descargar la fuente del dispositivo para compilar localmente a través de la CLI [de](https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html)PhoneGap.

![Mosaico de compilación de PhoneGap](assets/chlimage_1-140.png)

### Mosaico de métricas {#the-metrics-tile}

>[!CAUTION]
>
>El mosaico Métricas se muestra únicamente después de configurar el servicio en la nube.
>
>Consulte [Configuración del servicio](/help/mobile/configure-adobe-mobile-cloud-service.md) de nube de Adobe Mobile Services para obtener más información.

AEM Mobile se integra con Adobe Analytics a través del SDK [de](https://www.adobe.com/ca/solutions/digital-marketing/mobile-services/app-sdk.html) Adobe Mobile Services (AMS).

El mosaico **de** métricas del centro de control muestra un resumen de los análisis extraídos de AMS para la aplicación. Puede profundizar en el tablero de análisis haciendo clic en el botón &#39;...&#39; en la parte inferior derecha.

![Mosaico de métricas](assets/chlimage_1-141.png)

### Mosaico de contenido de la entidad de gestión {#the-manage-entity-content-tile}

El icono Administrar contenido de entidad le permite agregar y administrar definiciones de aplicación. Las definiciones de aplicación permiten identificar qué espacios (y otras configuraciones) son adecuados para la aplicación. De este modo, se puede añadir un nuevo espacio, sin tener que volver a compilar la aplicación. La definición de la aplicación se actualiza y eso incluirá la información de los nuevos espacios.

Haga clic [aquí](/help/mobile/phonegap-app-definitions.md) para crear y administrar las definiciones de la aplicación.

Puede explorar en profundidad el tablero de contenido de la entidad de administración haciendo clic en el botón &#39;...&#39; en la parte inferior derecha.

![chlimage_1-142](assets/chlimage_1-142.png)

#### Additional Resources {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y un desarrollador, consulte los siguientes recursos:

* [Desarrollo para Adobe PhoneGap Enterprise con AEM](/help/mobile/developing-in-phonegap.md)
* [Administración de contenido para Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)

