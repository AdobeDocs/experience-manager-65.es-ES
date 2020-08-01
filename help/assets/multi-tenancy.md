---
title: Varias tenencias para colecciones, fragmentos y plantillas de fragmentos
description: Descubra cómo la función de varios alquileres le permite segregar contenido en el repositorio de CRX según la organización del cliente para evitar el acceso no autorizado.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

---


# Varias tenencias para colecciones, fragmentos y plantillas de fragmentos {#multi-tenancy-for-collections-snippets-and-snippet-templates}

La función de varios alquileres le permite segregar contenido en CRX según el prefijo de organización y el ID de organización para proteger el contenido del acceso no autorizado por parte de usuarios de otras organizaciones.

[!DNL Adobe Experience Manager Assets] almacena datos para cada organización en una ruta diferente. Cada ruta específica de la organización se identifica mediante el prefijo de la organización y el identificador de organización que se incluyen en la ubicación tradicional donde se almacenan distintos tipos de recursos en CRX.

Por ejemplo, si crea una carpeta con el nombre `Demo`, [!DNL Experience Manager] assets almacena tradicionalmente la carpeta en `../content/dam/Demo`. Con la opción de varios alquileres activada, ahora puede almacenar los datos en `../content/dam/<organization prefix>/<organization id>Demo`

Por ejemplo, si para [!DNL Adobe Marketing Cloud] usuarios de [!DNL Assets] (On Demand) asignados a la `aodpremium` organización, puede utilizar la función de varios alquileres para configurar la `../content/dam/<mac>/<aodpremium>Demo` ruta y segregar su contenido. En este ejemplo, `mac` es el prefijo de organización y `aodpremium` es el identificador de organización.

En función de la organización y el ID del usuario, esta ruta de acceso cualificada se muestra en la interfaz y en varios asistentes, incluidos los asistentes de creación Mover y Fragmentar para aplicar la segregación. [!DNL Assets]

La función de varios alquileres permite separar los siguientes tipos de recursos y componentes:

* Colecciones
* Colecciones públicas
* Catálogos (incluido el asistente para Añadir/seleccionar página)
* Plantillas
* Plantillas de fragmento
* Lightbox
