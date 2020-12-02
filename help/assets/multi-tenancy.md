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

[!DNL Adobe Experience Manager Assets] almacena datos para cada organización en una ruta diferente. Cada ruta específica de la organización se identifica mediante el prefijo de la organización y el identificador de la organización
que se incluye en la ubicación tradicional en la que se almacenan distintos tipos de activos en CRX.

Por ejemplo, si se crea una carpeta con el nombre `Demo`, [!DNL Experience Manager] recursos generalmente almacena la carpeta en `../content/dam/Demo`. Con la opción de varios alquileres habilitada, ahora puede almacenar los datos en `../content/dam/<organization prefix>/<organization id>Demo`

Por ejemplo: si para [!DNL Adobe Marketing Cloud] usuarios de [!DNL Assets] (según demanda) asignados a la organización `aodpremium`, puede utilizar la función de varios tenedores para configurar la ruta `../content/dam/<mac>/<aodpremium>Demo` para segregar su contenido. En este ejemplo, `mac` es el prefijo de organización y `aodpremium` es el identificador de organización.

En función de la organización y el ID del usuario, esta ruta de acceso completa se muestra en la interfaz [!DNL Assets] y en varios asistentes, incluidos los asistentes para la creación de movimiento y de fragmentos para aplicar la segregación.

La función de varios alquileres permite separar los siguientes tipos de recursos y componentes:

* Colecciones
* Colecciones públicas
* Catálogos (incluido el asistente para Añadir/seleccionar página)
* Plantillas
* Plantillas de fragmento
* Lightbox
