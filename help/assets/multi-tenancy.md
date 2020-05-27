---
title: Varias tenencias para colecciones, fragmentos y plantillas de fragmentos
description: Descubra cómo la función de varios alquileres le permite segregar contenido en el repositorio de CRX según la organización del cliente para evitar el acceso no autorizado.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---


# Varias tenencias para colecciones, fragmentos y plantillas de fragmentos {#multi-tenancy-for-collections-snippets-and-snippet-templates}

La función de varios alquileres le permite segregar contenido en CRX según el prefijo de organización y el ID de organización para proteger el contenido del acceso no autorizado por parte de usuarios de otras organizaciones.

Recursos Adobe Experience Manager almacena datos para cada organización en una ruta diferente. Cada ruta específica de la organización se identifica mediante el prefijo de la organización y el identificador de organización que se incluyen en la ubicación tradicional donde se almacenan distintos tipos de recursos en CRX.

Por ejemplo, si crea una carpeta con el nombre `Demo`, los recursos de Experience Manager generalmente almacenan la carpeta en la `../content/dam/Demo`. Con la opción de varios alquileres activada, ahora puede almacenar los datos en `../content/dam/<organization prefix>/<organization id>Demo`

Por ejemplo, si para [!DNL Adobe Marketing Cloud] los usuarios de Recursos (On Demand) asignados a la `aodpremium` organización, puede utilizar la función de varios alquileres para configurar la `../content/dam/<mac>/<aodpremium>Demo` ruta y segregar su contenido. En este ejemplo, `mac` es el prefijo de organización y `aodpremium` es el identificador de organización.

En función de la organización y el ID del usuario, esta ruta de acceso cualificada se muestra en la interfaz de Recursos y en varios asistentes, incluidos los asistentes para la creación de movimiento y de fragmentos para aplicar la segregación.

La función de varios alquileres permite separar los siguientes tipos de recursos y componentes:

* Colecciones
* Colecciones públicas
* Catálogos (incluido el asistente para Añadir/seleccionar página)
* Plantillas
* Plantillas de fragmento
* Lightbox
