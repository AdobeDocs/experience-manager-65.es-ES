---
title: Inquilinos múltiples para colecciones, fragmentos y plantillas de fragmentos
description: Descubra cómo la función de varios alquileres le permite separar el contenido en el repositorio CRX en función de la organización del cliente para evitar el acceso no autorizado.
contentOwner: AG
role: Architect, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

---

# Inquilinos múltiples para colecciones, fragmentos y plantillas de fragmentos {#multi-tenancy-for-collections-snippets-and-snippet-templates}

La función de varios alquileres le permite separar el contenido en CRX en función del prefijo de la organización y el ID de la organización para proteger el contenido del acceso no autorizado de usuarios de otras organizaciones.

[!DNL Adobe Experience Manager Assets] almacena los datos de cada organización en una ruta diferente. Cada ruta específica de la organización se identifica mediante el prefijo de organización y el ID de organización que se incluye en la ubicación tradicional donde se almacenan diferentes tipos de recursos en CRX.

Por ejemplo, si crea una carpeta denominada `Demo`, [!DNL Experience Manager] recursos almacena tradicionalmente la carpeta en `../content/dam/Demo`. Con el alquiler múltiple habilitado, ahora puede almacenar los datos en `../content/dam/<organization prefix>/<organization id>Demo`

Por ejemplo, si para [!DNL Adobe Marketing Cloud] usuarios de [!DNL Assets] (bajo demanda) que se asignan al `aodpremium` organización, puede utilizar la función de varios alquileres para configurar `../content/dam/<mac>/<aodpremium>Demo` ruta para separar su contenido. En este ejemplo, `mac` es el prefijo de organización y `aodpremium` es el ID de organización de.

En función de la organización y el ID del usuario, esta ruta cualificada se muestra en la variable [!DNL Assets] y varios asistentes, incluidos los asistentes para mover y crear fragmentos de código para aplicar la segregación.

La función de inquilinos múltiples le permite separar los siguientes tipos de activos y componentes:

* Colecciones
* Colecciones públicas
* Catálogos (incluido el asistente Agregar/Seleccionar página)
* Plantillas
* Plantillas de fragmento
* Lightbox
