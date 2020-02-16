---
title: Especificación de fuentes para incrustar
seo-title: Especificación de fuentes para incrustar
description: Obtenga información sobre cómo especificar fuentes para incrustar.
seo-description: Obtenga información sobre cómo especificar fuentes para incrustar.
uuid: 97de6f98-ed3b-4a93-854a-193a967b4672
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4c83694c-b00f-40be-9ac4-f5785cd60741
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Especificación de fuentes para incrustar {#specifying-fonts-to-embed}

Puede especificar qué fuentes se incrustan siempre o nunca se incrustan en los formularios que genera el servicio Forms. La incrustación de fuentes aumenta el tamaño de archivo de los formularios. Incruste fuentes inusuales que los usuarios rara vez tienen en sus sistemas. No incruste las fuentes comunes que suelen tener instaladas.

>[!NOTE]
>
>Si ha especificado un archivo XCI personalizado para Forms, la opción de incrustación de fuente en el archivo XCI anula esta configuración. (Consulte [Configuración de ubicaciones para Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).)

1. En la consola de administración, haga clic en **[!UICONTROL Servicios > Formularios]**.
1. En Configuración **[!UICONTROL de incrustación de]** fuentes, en el cuadro **[!UICONTROL Incrustar siempre fuentes]** , escriba los nombres de las fuentes que desee incrustar con los formularios, separados por comas. Las fuentes que especifique solo se incrustarán en el formulario generado si se utilizan en el formulario. Esta configuración se ignora si la opción de incrustar fuente se ha activado en el archivo XCI que se pasa al servicio porque, en ese caso, todas las fuentes utilizadas en el PDF siempre están incrustadas.
1. En el cuadro **[!UICONTROL No incrustar nunca fuentes]** , escriba los nombres de las fuentes que no se van a incrustar en los formularios, separados por comas. Las fuentes que especifique no se incrustarán en el PDF, aunque se utilicen en el PDF generado. Esta configuración se omite si la opción de incrustar fuente se ha desactivado en el archivo XCI que se pasa al servicio porque, en ese caso, no se incrusta ninguna de las fuentes utilizadas en el PDF.
1. Haga clic en **[!UICONTROL Guardar]**.

