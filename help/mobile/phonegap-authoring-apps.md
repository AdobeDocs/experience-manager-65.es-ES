---
title: Creación de aplicaciones móviles
seo-title: Authoring Mobile Applications
description: El tablero de AEM Mobile le permite crear, crear e implementar su aplicación móvil, así como crear, eliminar y editar metadatos de aplicación. Siga esta página para obtener más información.
seo-description: he AEM Mobile Dashboard allows you to create, build and deploy your mobile application, create, delete and edit application metadata. Follow this page to learn more.
uuid: 293b5d29-df7e-42dd-ae64-8c677317e7a5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: abfeea65-102d-4800-abeb-304d61afcc13
exl-id: 073daff7-0c1d-4715-bfd4-3e2336e4cb88
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 0%

---

# Creación de aplicaciones móviles{#authoring-mobile-applications}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

El tablero de AEM Mobile le permite crear, crear e implementar su aplicación móvil, así como crear, eliminar y editar metadatos de aplicación. Una vez que la aplicación esté activa, puede analizar los análisis de la aplicación, incluidas las métricas de ciclo de vida y uso, para mejorar la conversión del cliente y la lealtad de la marca.

Para crear la aplicación para AEM Mobile, consulte la [Creación de aplicaciones móviles](/help/mobile/building-app-mobile-phonegap.md) página.

Para configurar su entorno y empezar, consulte [AEM AEM Administración de la para utilizar PhoneGap Enterprise de la red de](/help/mobile/administer-phonegap.md).

## El catálogo de aplicaciones de AEM Mobile {#the-aem-mobile-apps-catalog}

El [Catálogo de aplicaciones de AEM Mobile](http://localhost:4502/aem/apps.html/content/phonegap) AEM muestra toda la aplicación móvil gestionada en el servicio de asistencia de la aplicación de.

Piense en este catálogo como en la &quot;página de aterrizaje&quot; de AEM Mobile, donde los administradores pueden iniciar una nueva aplicación de AEM Mobile creando a partir de una plantilla o cargando una aplicación existente ya iniciada por un desarrollador móvil.

Siga estos pasos para llegar a la página de aterrizaje del catálogo de aplicaciones:

1. Navegar a **Navegación** y luego elija **Móvil**.

1. Elegir **Aplicaciones** para abrir el catálogo de aplicaciones.

![Catálogo de aplicaciones de AEM Mobile](assets/chlimage_1-135.png)

## El tablero de aplicaciones de AEM Mobile {#the-aem-mobile-app-dashboard}

Al seleccionar una aplicación de AEM Mobile en el catálogo, se muestra su panel. Aquí puede administrar la aplicación, ver estadísticas, crear, implementar y administrar el contenido de la aplicación móvil.

Puede expandirse a cada mosaico del panel de AEM Mobile para ver o editar detalles haciendo clic en &quot;...&quot; en la esquina inferior derecha.

![Centro de comandos de aplicaciones AEM Mobile](assets/chlimage_1-136.png)

### El mosaico Administrar aplicación {#the-manage-app-tile}

El mosaico Administrar aplicación muestra el icono de su aplicación, el nombre, la descripción, las plataformas admitidas, la dirección URL de inicio de la llamada para obtener actualizaciones e información de la versión. Puede explorar en profundidad este mosaico para editar y mantener la Configuración de la aplicación PhoneGap (config.xml) y preparar la aplicación para enviarla a las distintas tiendas de aplicaciones para su distribución.

Clic [aquí](/help/mobile/phonegap-app-details-tile.md) para obtener más información.

![chlimage_1-137](assets/chlimage_1-137.png)

### El mosaico Administrar contenido de la página {#the-manage-page-content-tile}

El contenido se puede crear, actualizar y eliminar en AEM Mobile de la misma manera que se hace en AEM Sites. El **Administrar mosaico de contenido de página** muestra el número de páginas de contenido administrado y modificadas por última vez. Puede explorar el contenido para crear, copiar, mover, eliminar y actualizar páginas haciendo clic en cada registro del mosaico. Una vez actualizado el contenido, puede enviar una actualización de contenido a sus clientes a través del **Mosaico Administrar paquetes de contenido.**

![Mosaico de contenido](assets/chlimage_1-138.png)

### El Mosaico Administrar Paquetes De Contenido {#the-manage-content-packages-tile}

Una vez que haya añadido o modificado el contenido a través del mosaico Administrar contenido de la página, puede insertar esos cambios en los clientes con una actualización de la versión de contenido.

AEM AEM El paquete de contenido permite al autor de la aplicación de administrar el contenido de la página en y, así como hacer que el equipo de desarrollo realice cambios en la aplicación de shell de PhoneGap (es decir, el marco de la aplicación o la infraestructura) y luego enviar esos cambios a los clientes de forma rápida y sin necesidad de inscribir a un desarrollador para que los vuelva a enviar a las distintas tiendas para su distribución.

El paquete de contenido crea un archivo ZIP, considerado un paquete de liberación de contenido, para cada actualización. Estos paquetes contienen recursos html y páginas html que se generan al procesar la aplicación y son lo suficientemente inteligentes como para empaquetar solo aquellos archivos que se han modificado desde la última actualización.

El mosaico Administrar paquete de contenido **Tipo** La columna muestra &quot;Aplicación&quot; para indicar contenido de Application Shell como, por ejemplo, el marco de trabajo o la infraestructura de la aplicación gestionada por un desarrollador, o bien &quot;Contenido&quot;, que representa el contenido de la página gestionado por el autor del contenido.

El contenido puede representarse como un idioma o como una parte concreta de la aplicación en la que la aplicación consume varios paquetes de Content Release. La elección de cómo empaquetar el contenido es flexible y depende totalmente de cómo desee administrar el contenido de la aplicación.

El **Modificado** indica cuándo se modificaron las páginas más recientemente.

El **Ensayado** La columna muestra cuándo se creó la última actualización de contenido. Para crear una actualización de contenido y almacenar en zona intermedia los cambios, abra cualquier registro del mosaico y cree una actualización.

El **Publicado** Esta columna muestra cuándo se publicó la última actualización de contenido y cuándo sus clientes la pusieron a disposición para su consumo. Para publicar contenido, primero debe almacenarlo en el escenario y luego publicar la actualización explorando en este mosaico y publicando desde la consola Detalles de la versión de contenido.

![Mosaico de publicación de contenido](assets/chlimage_1-139.png) ![Paquete ContentSync para el shell de la aplicación](do-not-localize/chlimage_1-5.png)

Este icono representa un paquete de versión de contenido para el shell de la aplicación

![](do-not-localize/chlimage_1-6.png)

Estos iconos representan un paquete de publicación de contenido para el contenido de la aplicación

### El mosaico del PhoneGap Build {#the-phonegap-build-tile}

El **Mosaico de PhoneGap Build** conecta con [https://build.phonegap.com](https://build.phonegap.com) para generar y alojar compilaciones remotas. Una vez creada, la compilación está disponible como descarga o directamente en el dispositivo mediante un código QR.

También puede descargar el origen del dispositivo para compilarlo localmente mediante el [CLI de PhoneGap](https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html).

![Mosaico de PhoneGap Build](assets/chlimage_1-140.png)

### El mosaico Métricas {#the-metrics-tile}

>[!CAUTION]
>
>El mosaico Métricas solo se muestra después de configurar el servicio en la nube.
>
>Consulte [Configuración del Cloud Service de Adobe Mobile Services](/help/mobile/configure-adobe-mobile-cloud-service.md) para obtener más información.

AEM Mobile se integra con Adobe Analytics mediante [SDK de Adobe Mobile Services](https://experienceleague.adobe.com/docs/mobile.html?lang=en) (AMS).

El Centro de control **Mosaico de métricas** muestra análisis de resumen extraídos de AMS para su aplicación. Puede explorar en profundidad el panel de análisis haciendo clic en &#39;...&#39; en la parte inferior derecha.

![Mosaico de métricas](assets/chlimage_1-141.png)

### El mosaico Administrar contenido de la entidad {#the-manage-entity-content-tile}

El mosaico Administrar contenido de la entidad le permite añadir y administrar definiciones de aplicaciones. Las definiciones de aplicación son una forma de identificar qué espacios (y otras configuraciones) son adecuados para la aplicación. De este modo, se puede añadir un nuevo espacio sin tener que volver a compilar la aplicación. La definición de la aplicación se actualiza y eso incluye la información de cualquier espacio nuevo.

Clic [aquí](/help/mobile/phonegap-app-definitions.md) para crear y administrar las definiciones de aplicaciones.

Puede explorar en profundidad el panel de contenido de la entidad administrada haciendo clic en &quot;...&quot; en la parte inferior derecha.

![chlimage_1-142](assets/chlimage_1-142.png)

#### Recursos adicionales {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y un desarrollador, consulte los recursos siguientes:

* [Desarrollo para Adobe PhoneGap AEM Enterprise con](/help/mobile/developing-in-phonegap.md)
* [Administración de contenido para Adobe PhoneGap AEM Enterprise con el servicio de administración de](/help/mobile/administer-phonegap.md)
