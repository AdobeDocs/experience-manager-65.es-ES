---
title: Especificación de las opciones de configuración XCI
seo-title: Especificación de las opciones de configuración XCI
description: Aprenda a especificar las opciones de configuración XCI.
seo-description: Aprenda a especificar las opciones de configuración XCI.
uuid: 5d3c10c1-4a93-4336-b311-20faaf835b9f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 162c9fda-f4d4-4ad5-a9ab-7554828e821c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Especificación de las opciones de configuración XCI {#specifying-xci-configuration-options}

Forms le permite especificar un archivo XCI personalizado que utilizará para el procesamiento. (Consulte [Configuración de ubicaciones para Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).) De forma predeterminada, Forms anula algunas de las opciones especificadas en el archivo XCI, incluidas las siguientes:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Puede seleccionar opciones que cancelen la anulación de las opciones enumeradas anteriormente, en cuyo caso Forms utilizará los valores especificados en el archivo XCI personalizado.

1. En la consola de administración, haga clic en Servicios > Formularios.
1. Active o desactive la casilla de verificación Usar opciones XCI predeterminadas del sistema. Cuando se selecciona esta opción, Forms utiliza sus valores predeterminados para los ajustes de paquetes, creador, productor y compressObjectStream. Cuando se anula la selección de esta opción, Forms utiliza los valores especificados en el archivo XCI personalizado.
1. Haga clic en Guardar.

