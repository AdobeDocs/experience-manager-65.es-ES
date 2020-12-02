---
title: Cambiar el conjunto de caracteres
seo-title: Cambiar el conjunto de caracteres
description: Puede especificar el conjunto de caracteres utilizado para codificar el flujo de salida. Descubra cómo puede cambiar el conjunto de caracteres.
seo-description: Puede especificar el conjunto de caracteres utilizado para codificar el flujo de salida. Descubra cómo puede cambiar el conjunto de caracteres.
uuid: ecb0c3ff-368c-4553-80e4-aa35fc15af62
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 811b31f8-5465-4fb2-b1f9-513936041771
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 1%

---


# Cambiar el conjunto de caracteres {#change-the-character-set}

Puede especificar el conjunto de caracteres utilizado para codificar el flujo de salida.

1. En la consola de administración, haga clic en **[!UICONTROL Servicios > salida]**.
1. En Internacionalización, en la lista Conjunto de caracteres, seleccione un conjunto de caracteres. Esta configuración depende de los valores `TransformationFormat` y `PrintFormat` especificados a través de la API. Para especificar un conjunto de caracteres distinto de los enumerados, seleccione Personalizado y especifique un valor de codificación en el cuadro que se muestra.

   Si `TransformationFormat` es PDF y PDF/A o `PrintFormat` es PCL, PostScript, etiqueta Zebra, IPL, DPL, TPCL, GenericColorPCL o GenericPSLevel3, solo se admiten conjuntos de caracteres específicos.

   El conjunto de caracteres debe ser un nombre canónico válido. El valor predeterminado es ISO-8859-1.

1. Haga clic en **[!UICONTROL Guardar]**.

