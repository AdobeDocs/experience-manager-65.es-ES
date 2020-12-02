---
title: Especificar opciones de configuración XCI
seo-title: Especificar opciones de configuración XCI
description: Aprenda a especificar las opciones de configuración XCI.
seo-description: Aprenda a especificar las opciones de configuración XCI.
uuid: cf9e544d-63cd-4fad-8f89-bdb46eeef409
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f38ebd69-8d1c-49b6-824f-4bf0ec8a8953
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 1%

---


# Especifique las opciones de configuración XCI {#specify-xci-configuration-options}

Output permite especificar un archivo XCI personalizado que se utiliza para el procesamiento. (Consulte [Especificar ubicaciones de archivos para Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).) De forma predeterminada, Output anula algunas de las opciones especificadas en el archivo XCI, incluidas las siguientes:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Puede seleccionar opciones que cancelen la anulación de las opciones enumeradas anteriormente, en cuyo caso Output utiliza los valores especificados en el archivo XCI personalizado.

1. En la consola de administración, haga clic en Servicios > salida.
1. Active o desactive la casilla de verificación Usar opciones XCI predeterminadas del sistema. Cuando se selecciona esta opción, Output utiliza sus valores predeterminados para los ajustes de paquetes, creador, productor y compressObjectStream. Cuando se anula la selección de esta opción, Output utiliza los valores especificados en el archivo XCI personalizado.
1. Haga clic en Guardar.

