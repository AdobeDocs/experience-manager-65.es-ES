---
title: Especificar fuentes para incrustar
description: Obtenga información sobre cómo especificar fuentes para incrustarlas en un formulario adaptable. Puede especificar qué fuentes están incrustadas o nunca están incrustadas con los formularios que genera el servicio Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 3%

---

# Especificar fuentes para incrustar{#specify-fonts-to-embed}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Puede especificar qué fuentes están siempre incrustadas o nunca incrustadas con los formularios que utiliza Output. La incrustación de fuentes aumenta el tamaño de archivo de los formularios. Incruste fuentes inusuales que probablemente los usuarios no tengan en sus sistemas y no incruste fuentes comunes que habrán instalado.

>[!NOTE]
>
>Si ha especificado un archivo XCI personalizado para Salida, la opción de fuente incrustada en el archivo XCI anula esta configuración. (Consulte [Especificar ubicaciones de archivos para la salida](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)

1. En la consola de administración, haga clic en Servicios > Resultados.
1. En Configuración de incrustación de fuentes, en el cuadro Incrustar siempre fuentes, escriba los nombres de las fuentes que desea incrustar con los formularios, separados por comas. Las fuentes especificadas solo están incrustadas en el formulario generado si se utilizan en el formulario. Esta configuración se ignora si la opción de fuente incrustada se ha activado en el archivo XCI enviado al servicio. En ese caso, todas las fuentes utilizadas en el PDF siempre están incrustadas.
1. En el cuadro No incrustar nunca fuentes, escriba los nombres de las fuentes que no desea incrustar con los formularios, separados por comas. Las fuentes especificadas no están incrustadas en el PDF, aunque se utilicen en el PDF generado. Esta configuración se ignora si la opción de fuente incrustada se ha desactivado en el archivo XCI enviado al servicio. En ese caso, ninguna de las fuentes utilizadas en el PDF está incrustada.
1. Haga clic en Guardar.
