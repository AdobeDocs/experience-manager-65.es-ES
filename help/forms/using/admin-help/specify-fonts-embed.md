---
title: Especificar fuentes para incrustar
seo-title: Especificar fuentes para incrustar
description: Obtenga información sobre cómo especificar fuentes para incrustar.
seo-description: Obtenga información sobre cómo especificar fuentes para incrustar.
uuid: 02da5c00-0467-4633-a076-c36725cbfbad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 180f0448-d507-4b6d-bb8a-d12a434e1250
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Especificar fuentes para incrustar{#specify-fonts-to-embed}

Puede especificar las fuentes que siempre se incrustan o que nunca se incrustan en los formularios utilizados por Output. La incrustación de fuentes aumenta el tamaño de archivo de los formularios. Incruste fuentes inusuales que los usuarios probablemente no tengan en sus sistemas y no incruste fuentes comunes que habrán instalado.

>[!NOTE]
>
>Si ha especificado un archivo XCI personalizado para Output, la opción de incrustar fuente en el archivo XCI anula esta configuración. (Consulte [Especificación de ubicaciones de archivos para Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)

1. En la consola de administración, haga clic en Servicios > salida.
1. En Configuración de incrustación de fuentes, en el cuadro Incrustar siempre fuentes, escriba los nombres de las fuentes que desee incrustar con los formularios, separados por comas. Las fuentes que especifique solo se incrustarán en el formulario generado si se utilizan en el formulario. Esta configuración se ignora si la opción de incrustar fuente se ha activado en el archivo XCI que se pasa al servicio. En ese caso, todas las fuentes utilizadas en el PDF siempre se incrustan.
1. En el cuadro No incrustar nunca fuentes, escriba los nombres de las fuentes que no se van a incrustar en los formularios, separados por comas. Las fuentes que especifique no se incrustarán en el PDF, aunque se utilicen en el PDF generado. Esta configuración se omite si la opción de incrustar fuente se ha desactivado en el archivo XCI que se pasa al servicio. En ese caso, ninguna de las fuentes utilizadas en el PDF está incrustada.
1. Haga clic en Guardar.

