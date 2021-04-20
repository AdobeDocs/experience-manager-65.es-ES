---
title: 'Texto de marcador de posición en AEM Forms '
seo-title: 'Texto de marcador de posición en AEM Forms '
description: El texto del marcador de posición está diseñado para ayudar al usuario con la introducción de datos cuando el control no tiene valor. Podría ser un valor de muestra o una breve descripción del formato esperado.
seo-description: El texto del marcador de posición está diseñado para ayudar al usuario con la introducción de datos cuando el control no tiene valor. Podría ser un valor de muestra o una breve descripción del formato esperado.
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---


# Texto del marcador de posición en AEM Forms {#placeholder-text-in-aem-forms}

El texto del marcador de posición representa una palabra o una frase corta. Su objetivo es ayudar al usuario a introducir los datos cuando el control no tiene valor. Un texto de marcador de posición podría ser un valor de muestra o una breve descripción del formato esperado. El texto del marcador de posición se muestra antes de que el usuario introduzca un valor; se elimina cuando el usuario introduce o selecciona un valor.

>[!NOTE]
>
>Si se especifica, el texto del marcador de posición debe tener un valor que no contenga caracteres de línea nuevos.

![Componente de fecha con y sin texto de marcador de posición](assets/dat-picker-place-holder-text.png)

**A.** Componente de fecha con texto de marcador de posición  **B.** Componente de fecha sin texto de marcador de posición

AEM Forms admite el texto de marcador de posición para los campos Cuadro de contraseña, Selector de fecha, Cuadro numérico y Cuadro de texto.\
Los textos de los marcadores de posición no son compatibles con el widget de fechas HTML5 nativo. Para especificar un texto de marcador de posición:

1. Haga clic con el botón derecho en un componente que admita Texto del marcador de posición y haga clic en **Editar**. Aparecerá el cuadro de diálogo Editar componente.

1. Abra la pestaña **Title and text**.
1. Especifique una palabra o una frase corta en el cuadro de texto **Marcador de posición**. Haga clic en **Aceptar**.

>[!NOTE]
>
>El texto del marcador de posición no es compatible con Microsoft Internet Explorer 9.

