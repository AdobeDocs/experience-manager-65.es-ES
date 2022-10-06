---
title: Varios alquileres para colecciones, fragmentos y plantillas de fragmento
description: Descubra cómo la función de inquilinos múltiples le permite segregar contenido en el repositorio CRX en función de la organización del cliente para evitar el acceso no autorizado.
contentOwner: AG
role: Architect, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

---

# Varios alquileres para colecciones, fragmentos y plantillas de fragmento {#multi-tenancy-for-collections-snippets-and-snippet-templates}

La función de inquilinos múltiples le permite segregar contenido en CRX en función del prefijo de organización y el ID de organización para proteger el contenido de acceso no autorizado por parte de usuarios de otras organizaciones.

[!DNL Adobe Experience Manager Assets] almacena datos para cada organización en una ruta diferente. Cada ruta específica de la organización se identifica mediante el prefijo de organización y el ID de organización que se incluyen en la ubicación tradicional donde se almacenan distintos tipos de activos en CRX.

Por ejemplo, si crea una carpeta con el nombre `Demo`, [!DNL Experience Manager] assets generalmente almacena la carpeta en `../content/dam/Demo`. Con la opción de inquilino múltiple habilitada, ahora puede almacenar los datos en `../content/dam/<organization prefix>/<organization id>Demo`

Por ejemplo, si [!DNL Adobe Marketing Cloud] usuarios de [!DNL Assets] (On Demand) que se asignan al `aodpremium` organización, puede utilizar la función de varios alquileres para configurar `../content/dam/<mac>/<aodpremium>Demo` ruta para segregar su contenido. En este ejemplo, `mac` es el prefijo de la organización y `aodpremium` es el ID de organización.

En función de la organización y el ID del usuario, esta ruta cualificada se muestra en la variable [!DNL Assets] y varios asistentes, incluidos los asistentes de creación Mover y Fragmento para aplicar la segregación.

La función de inquilino múltiple permite separar los siguientes tipos de activos y componentes:

* Colecciones
* Colecciones públicas
* Catálogos (incluido el asistente Agregar/Seleccionar página )
* Plantillas
* Plantillas de recorte
* Lightbox
