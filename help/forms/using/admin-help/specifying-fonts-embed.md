---
title: Especificación de fuentes para incrustar
seo-title: Specifying fonts to embed
description: Aprenda a especificar fuentes para incrustar.
seo-description: Learn how to specify fonts to embed.
uuid: 97de6f98-ed3b-4a93-854a-193a967b4672
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4c83694c-b00f-40be-9ac4-f5785cd60741
exl-id: b2cbf5f3-ee13-47bf-bf7f-f6a1884cee66
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Especificación de fuentes para incrustar {#specifying-fonts-to-embed}

Puede especificar qué fuentes se incrustan siempre o nunca se incrustan en los formularios que genera el servicio de Forms. La incrustación de fuentes aumenta el tamaño de archivo de los formularios. Incruste fuentes inusuales que los usuarios rara vez tienen en sus sistemas. No incruste fuentes comunes que normalmente tienen instaladas.

>[!NOTE]
>
>Si ha especificado un archivo XCI personalizado para Forms, la opción de incrustar fuente en el archivo XCI anula esta configuración. (Consulte [Configuración de ubicaciones para Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).)

1. En la consola de administración, haga clic en **[!UICONTROL Servicios > Forms]**.
1. En **[!UICONTROL Configuración de incrustación de fuentes]**, en el **[!UICONTROL Incrustar siempre fuentes]** , escriba los nombres de las fuentes que desea incrustar con los formularios separados por comas. Las fuentes que especifique solo se incrustarán en el formulario generado si se utilizan en el formulario. Esta configuración se ignora si la opción incrustar fuente se ha activado en el archivo XCI pasado al servicio porque, en ese caso, todas las fuentes utilizadas en el PDF siempre están incrustadas.
1. En el **[!UICONTROL No incrustar nunca fuentes]** , escriba los nombres de las fuentes que no se van a incrustar en los formularios separados por comas. Las fuentes que especifique no están incrustadas en el PDF, aunque se utilicen en el PDF generado. Esta configuración se ignora si la opción incrustar fuente se ha desactivado en el archivo XCI pasado al servicio porque, en ese caso, ninguna de las fuentes utilizadas en el PDF está incrustada.
1. Haga clic en **[!UICONTROL Guardar]**.
