---
title: Creación de aplicaciones móviles
description: El panel de AEM Mobile le permite crear, crear e implementar su aplicación móvil, así como crear, eliminar y editar metadatos de aplicación. Siga esta página para obtener más información.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 073daff7-0c1d-4715-bfd4-3e2336e4cb88
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 0%

---

# Creación de aplicaciones móviles{#authoring-mobile-applications}

{{ue-over-mobile}}

El panel de AEM Mobile le permite crear, crear e implementar su aplicación móvil, así como crear, eliminar y editar metadatos de aplicación. Una vez que la aplicación esté activa, puede analizar los análisis de la aplicación, incluidas las métricas de ciclo de vida y uso, para mejorar la conversión del cliente y la lealtad de la marca.

Para crear su aplicación de AEM Mobile, consulte la página [Crear aplicaciones móviles](/help/mobile/building-app-mobile-phonegap.md).

AEM AEM Para configurar su entorno y comenzar, consulte [Administración de la para usar PhoneGap Enterprise](/help/mobile/administer-phonegap.md).

## El catálogo de aplicaciones de AEM Mobile {#the-aem-mobile-apps-catalog}

El [catálogo de aplicaciones de AEM Mobile AEM](http://localhost:4502/aem/apps.html/content/phonegap) muestra toda la aplicación móvil administrada en la aplicación de forma que se pueda administrar de forma independiente.

Piense en este catálogo como en la &quot;página de aterrizaje&quot; de AEM Mobile, donde los administradores pueden iniciar una nueva aplicación de AEM Mobile creando a partir de una plantilla o cargando una aplicación existente ya iniciada por un desarrollador móvil.

Siga estos pasos para llegar a la página de aterrizaje del catálogo de aplicaciones:

1. Vaya a **Navegación** y, a continuación, elija **Móvil**.

1. Elija **Aplicaciones** para abrir el catálogo de aplicaciones.

![Catálogo de aplicaciones de AEM Mobile](assets/chlimage_1-135.png)

## El tablero de aplicaciones de AEM Mobile {#the-aem-mobile-app-dashboard}

Al seleccionar una aplicación de AEM Mobile en el catálogo, se muestra su panel. Aquí puede administrar la aplicación, ver estadísticas, crear, implementar y administrar el contenido de la aplicación móvil.

Puede expandirse a cada mosaico del panel de AEM Mobile para ver o editar detalles haciendo clic en &quot;...&quot; en la esquina inferior derecha.

![Centro de comandos de aplicaciones AEM Mobile](assets/chlimage_1-136.png)

### El mosaico Administrar aplicación {#the-manage-app-tile}

El mosaico Administrar aplicación muestra el icono de su aplicación, el nombre, la descripción, las plataformas admitidas, la dirección URL de inicio de la llamada para obtener actualizaciones e información de la versión. Puede explorar en profundidad este mosaico para editar y mantener la Configuración de la aplicación PhoneGap (config.xml) y preparar la aplicación para enviarla a las distintas tiendas de aplicaciones para su distribución.

Haga clic [aquí](/help/mobile/phonegap-app-details-tile.md) para obtener detalles.

![chlimage_1-137](assets/chlimage_1-137.png)

### El mosaico Administrar contenido de la página {#the-manage-page-content-tile}

El contenido se puede crear, actualizar y eliminar en AEM Mobile de la misma manera que se hace en AEM Sites. El **mosaico Administrar contenido de página** muestra el número de páginas de contenido administrado y modificadas por última vez. Puede explorar el contenido para crear, copiar, mover, eliminar y actualizar páginas haciendo clic en cada registro del mosaico. Una vez que se haya actualizado el contenido, puede enviar una actualización de contenido a sus clientes a través del **mosaico Administrar paquetes de contenido.**

![Mosaico de contenido](assets/chlimage_1-138.png)

### El Mosaico Administrar Paquetes De Contenido {#the-manage-content-packages-tile}

Una vez que haya añadido o modificado el contenido a través del mosaico Administrar contenido de la página, puede insertar esos cambios en los clientes con una actualización de la versión de contenido.

AEM AEM El paquete de contenido permite al autor de la aplicación de administrar el contenido de la página en los entornos de y, hacer que el equipo de desarrollo cambie la aplicación PhoneGap Shell (es decir, el marco de la aplicación o la infraestructura) y luego enviar esos cambios a los clientes de forma rápida y sin necesidad de inscribir a un desarrollador para que vuelva a enviarlos a las distintas tiendas para su distribución.

El paquete de contenido crea un archivo ZIP, considerado un paquete de liberación de contenido, para cada actualización. Estos paquetes contienen recursos html y páginas html que se generan al procesar la aplicación y son lo suficientemente inteligentes como para empaquetar solo aquellos archivos que se han modificado desde la última actualización.

La columna **Tipo** del mosaico Administrar paquete de contenido muestra &quot;Aplicación&quot; para indicar contenido de Application Shell, por ejemplo, el marco de trabajo o la infraestructura de la aplicación administrada por un desarrollador, o bien, &quot;Contenido&quot;, que representa el contenido de la página administrado por el autor del contenido.

El contenido puede representarse como un idioma o como una parte concreta de la aplicación en la que la aplicación consume varios paquetes de Content Release. La elección de cómo empaquetar el contenido es flexible y depende totalmente de cómo desee administrar el contenido de la aplicación.

La columna **Modificado** indica cuándo se modificaron las páginas más recientemente.

La columna **Ensayado** muestra cuándo se creó la última actualización de contenido. Para crear una actualización de contenido y almacenar en zona intermedia los cambios, abra cualquier registro del mosaico y cree una actualización.

La columna **Publicado** muestra cuándo se publicó la última actualización de contenido y cuándo sus clientes la pusieron a disposición para su consumo. Para publicar contenido, primero debe almacenarlo en el escenario y luego publicar la actualización explorando en este mosaico y publicando desde la consola Detalles de la versión de contenido.

![Título de la versión del contenido](assets/chlimage_1-139.png) ![Paquete ContentSync para el shell de la aplicación](do-not-localize/chlimage_1-5.png)

Este icono representa un paquete de versión de contenido para el shell de la aplicación

![Icono de paquete de publicación de contenido indicado por dos símbolos de paquete cuadrados superpuestos.](do-not-localize/chlimage_1-6.png)

Estos iconos representan un paquete de publicación de contenido para el contenido de la aplicación

### El mosaico del PhoneGap Build {#the-phonegap-build-tile}

El **Mosaico de PhoneGap Build** se conecta con `https://build.phonegap.com` para generar y alojar compilaciones remotas. Una vez creada, la compilación está disponible como descarga o directamente en el dispositivo mediante un código QR.

También puede descargar el origen del dispositivo para compilarlo localmente mediante la CLI de PhoneGap (`https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html`).

![Mosaico de PhoneGap Build](assets/chlimage_1-140.png)

### El mosaico Métricas {#the-metrics-tile}

>[!CAUTION]
>
>El mosaico Métricas solo se muestra después de configurar el servicio en la nube.
>
>Consulte [Configuración del Cloud Service de Adobe Mobile Services](/help/mobile/configure-adobe-mobile-cloud-service.md) para obtener más información.

AEM Mobile se integra con Adobe Analytics mediante [Adobe Mobile Services SDK](https://experienceleague.adobe.com/docs/mobile.html?lang=es) (AMS).

El mosaico **Métricas** del Centro de control muestra análisis de resumen extraídos de AMS para su aplicación. Puede explorar en profundidad el panel de análisis haciendo clic en &#39;...&#39; en la parte inferior derecha.

![Mosaico de métricas](assets/chlimage_1-141.png)

### El mosaico Administrar contenido de la entidad {#the-manage-entity-content-tile}

El mosaico Administrar contenido de la entidad le permite añadir y administrar definiciones de aplicaciones. Las definiciones de aplicación son una forma de identificar qué espacios (y otras configuraciones) son adecuados para la aplicación. De este modo, se puede añadir un nuevo espacio sin tener que volver a compilar la aplicación. La definición de la aplicación se actualiza y eso incluye la información de cualquier espacio nuevo.

Haga clic [aquí](/help/mobile/phonegap-app-definitions.md) para crear y administrar las definiciones de su aplicación.

Puede explorar en profundidad el panel de contenido de la entidad administrada haciendo clic en &quot;...&quot; en la parte inferior derecha.

![chlimage_1-142](assets/chlimage_1-142.png)

#### Recursos adicionales {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y un desarrollador, consulte los recursos siguientes:

* [Desarrollo para Adobe PhoneGap AEM Enterprise con](/help/mobile/developing-in-phonegap.md)
* [Administración de contenido para Adobe PhoneGap AEM Enterprise con el servicio de administración de](/help/mobile/administer-phonegap.md)
