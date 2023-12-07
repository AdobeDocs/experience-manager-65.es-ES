---
title: Cambiar el conjunto de caracteres
description: Puede especificar el conjunto de caracteres utilizado para codificar la secuencia de salida. Aprenda a cambiar el conjunto de caracteres.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9ff75d98-54ad-425d-912f-d5a7501bf564
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 7%

---

# Cambiar el conjunto de caracteres {#change-the-character-set}

Puede especificar el conjunto de caracteres utilizado para codificar la secuencia de salida.

1. En la consola de administración, haga clic en **[!UICONTROL Servicios > salida]**.
1. En Internacionalización, en la lista Conjunto de caracteres, seleccione un conjunto de caracteres. Esta configuración depende de la variable `TransformationFormat` y `PrintFormat` se especifica mediante la API. Para especificar un conjunto de caracteres distinto de los enumerados, seleccione Personalizado y especifique un valor de codificación en el cuadro que se muestra.

   If `TransformationFormat` es PDF y PDF/A o `PrintFormat` es PCL, PostScript, etiqueta Zebra, IPL, DPL, TPCL, GenericColorPCL o GenericPSLevel3, solo se admiten conjuntos de caracteres específicos.

   El conjunto de caracteres debe ser un nombre canónico válido. El valor predeterminado es ISO-8859-1.

1. Haga clic en **[!UICONTROL Guardar]**.
