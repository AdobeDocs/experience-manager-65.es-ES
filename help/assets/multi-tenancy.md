---
title: Varias tenencias para colecciones, fragmentos y plantillas de fragmentos
description: Descubra cómo la función de varios alquileres le permite segregar contenido en el repositorio de CRX según la organización del cliente para evitar el acceso no autorizado.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Varias tenencias para colecciones, fragmentos y plantillas de fragmentos {#multi-tenancy-for-collections-snippets-and-snippet-templates}

La función de varios alquileres le permite segregar contenido en CRX según el prefijo de organización y el ID de organización para proteger el contenido del acceso no autorizado por parte de usuarios de otras organizaciones.

Recursos Adobe Experience Manager (AEM) almacena datos para cada organización en una ruta diferente. Cada ruta específica de la organización se identifica mediante el prefijo de la organización y el identificador de organización que se incluyen en la ubicación tradicional donde se almacenan distintos tipos de recursos en CRX.

Por ejemplo, si crea una carpeta con el nombre `Demo`, los recursos de AEM suelen almacenar la carpeta en la `../content/dam/Demo`. Con la opción de varios alquileres activada, ahora puede almacenar los datos en `../content/dam/<organization prefix>/<organization id>Demo`

Por ejemplo, si para [!DNL Adobe Marketing Cloud] usuarios de Recursos AEM (On Demand) asignados a la `aodpremium` organización, puede utilizar la función de varios alquileres para configurar la `../content/dam/<mac>/<aodpremium>Demo` ruta y segregar su contenido. En este ejemplo, `mac` es el prefijo de organización y `aodpremium` es el identificador de organización.

En función de la organización y el ID del usuario, esta ruta de acceso cualificada se muestra en la interfaz de Recursos AEM y en varios asistentes, incluidos los asistentes para la creación de movimientos y fragmentos de código, con el fin de aplicar la segregación.

La función de varios alquileres permite separar los siguientes tipos de recursos y componentes:

* Colecciones
* Colecciones públicas
* Catálogos (incluido el asistente Agregar o seleccionar página)
* Plantillas
* Plantillas de fragmento
* Lightbox
