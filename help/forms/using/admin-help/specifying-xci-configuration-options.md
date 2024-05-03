---
title: Especificar las opciones de configuración XCI
description: Obtenga información sobre cómo especificar las opciones de configuración de XCI. Puede especificar valores de archivo XCI personalizados para el formulario adaptable, de modo que se pueda utilizar durante el procesamiento del formulario.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 6%

---

# Especificar las opciones de configuración XCI {#specifying-xci-configuration-options}

Forms permite especificar un archivo XCI personalizado que puede utilizar para el procesamiento. (Consulte [Configuración de ubicaciones para Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).) De forma predeterminada, Forms anula algunas de las opciones especificadas en el archivo XCI, incluidas las siguientes:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Puede seleccionar opciones que cancelen la anulación de las opciones enumeradas anteriormente, en cuyo caso Forms utilizará los valores especificados en el archivo XCI personalizado.

1. En la consola de administración, haga clic en **Servicios** > **Forms**.
1. Seleccione o anule la selección de la casilla de verificación Usar opciones XCI predeterminadas del sistema. Cuando se selecciona esta opción, Forms utiliza sus valores predeterminados para los valores de paquetes, creador, productor y compressObjectStream. Cuando esta opción no está seleccionada, Forms utiliza los valores especificados en el archivo XCI personalizado.
1. Haga clic en **Guardar**.
