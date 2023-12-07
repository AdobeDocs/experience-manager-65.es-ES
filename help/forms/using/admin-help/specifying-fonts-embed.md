---
title: Especificar fuentes para incrustar
description: Obtenga información sobre cómo especificar fuentes para incrustarlas en un formulario adaptable. Puede especificar qué fuentes están incrustadas o nunca están incrustadas con los formularios que genera el servicio Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b2cbf5f3-ee13-47bf-bf7f-f6a1884cee66
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 3%

---

# Especificar fuentes para incrustar {#specifying-fonts-to-embed}

Puede especificar qué fuentes están siempre incrustadas o nunca incrustadas con los formularios que genera el servicio Forms. La incrustación de fuentes aumenta el tamaño de archivo de los formularios. Incruste fuentes inusuales que los usuarios rara vez tienen en sus sistemas. No incruste fuentes comunes que normalmente tienen instaladas.

>[!NOTE]
>
>Si ha especificado un archivo XCI personalizado para Forms, la opción de fuente incrustada en el archivo XCI anula esta configuración. (Consulte [Configuración de ubicaciones para Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).)

1. En la consola de administración, haga clic en **[!UICONTROL Servicios > Forms]**.
1. En **[!UICONTROL Configuración de incrustación de fuentes]**, en el **[!UICONTROL Incrustar siempre fuentes]** , escriba los nombres de las fuentes que desea incrustar con los formularios, separados por comas. Las fuentes especificadas solo están incrustadas en el formulario generado si se utilizan en el formulario. Esta configuración se ignora si la opción de fuente incrustada se ha activado en el archivo XCI enviado al servicio porque, en ese caso, todas las fuentes utilizadas en el PDF siempre están incrustadas.
1. En el **[!UICONTROL No incrustar nunca fuentes]** , escriba los nombres de las fuentes que no desea incrustar con los formularios, separados por comas. Las fuentes especificadas no están incrustadas en el PDF, aunque se utilicen en el PDF generado. Esta configuración se ignora si la opción de fuente incrustada se ha desactivado en el archivo XCI enviado al servicio porque, en ese caso, ninguna de las fuentes utilizadas en el PDF está incrustada.
1. Haga clic en **[!UICONTROL Guardar]**.
