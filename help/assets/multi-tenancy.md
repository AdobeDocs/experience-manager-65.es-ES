---
title: Varios alquileres para colecciones, fragmentos y plantillas de fragmento
description: Descubra cómo la función de inquilinos múltiples le permite segregar contenido en el repositorio CRX en función de la organización del cliente para evitar el acceso no autorizado.
contentOwner: AG
role: Arquitecto, Administrador, Líder
feature: Colecciones
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 1%

---


# Varios alquileres para colecciones, fragmentos y plantillas de fragmentos {#multi-tenancy-for-collections-snippets-and-snippet-templates}

La función de inquilinos múltiples le permite segregar contenido en CRX en función del prefijo de organización y el ID de organización para proteger el contenido de acceso no autorizado por parte de usuarios de otras organizaciones.

[!DNL Adobe Experience Manager Assets] almacena datos para cada organización en una ruta diferente. Cada ruta específica de la organización se identifica mediante el prefijo de organización y el ID de organización
que se incluye en la ubicación tradicional donde se almacenan distintos tipos de activos en CRX.

Por ejemplo, si crea una carpeta denominada `Demo`, los recursos [!DNL Experience Manager] generalmente almacenan la carpeta en `../content/dam/Demo`. Con la opción de inquilino múltiple habilitada, ahora puede almacenar los datos en `../content/dam/<organization prefix>/<organization id>Demo`

Por ejemplo, si para [!DNL Adobe Marketing Cloud] usuarios de [!DNL Assets] (On Demand) que están asignados a la organización `aodpremium`, puede utilizar la función de varios inquilinos para configurar la ruta `../content/dam/<mac>/<aodpremium>Demo` y segregar su contenido. En este ejemplo, `mac` es el prefijo de organización y `aodpremium` es el ID de organización.

En función de la organización y el ID del usuario, esta ruta de acceso cualificada se muestra en la interfaz [!DNL Assets] y en varios asistentes, incluidos los asistentes de creación Mover y Fragmentar para aplicar la segregación.

La función de inquilino múltiple permite separar los siguientes tipos de activos y componentes:

* Colecciones
* Colecciones públicas
* Catálogos (incluido el asistente Agregar/Seleccionar página )
* Plantillas
* Plantillas de recorte
* Lightbox
