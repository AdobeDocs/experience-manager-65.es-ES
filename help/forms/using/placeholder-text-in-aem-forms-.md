---
title: 'Texto de marcador de posición en AEM Forms '
seo-title: 'Texto de marcador de posición en AEM Forms '
description: El texto del marcador de posición está diseñado para ayudar al usuario a introducir datos cuando el control no tiene ningún valor. Podría ser un valor de muestra o una breve descripción del formato esperado.
seo-description: El texto del marcador de posición está diseñado para ayudar al usuario a introducir datos cuando el control no tiene ningún valor. Podría ser un valor de muestra o una breve descripción del formato esperado.
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# Texto de marcador de posición en AEM Forms {#placeholder-text-in-aem-forms}

El texto del marcador de posición representa una palabra o una frase corta. Está diseñado para ayudar al usuario a introducir datos cuando el control no tiene ningún valor. Un texto de marcador de posición puede ser un valor de muestra o una breve descripción del formato esperado. El texto del marcador de posición se muestra antes de que el usuario introduzca un valor; se elimina cuando el usuario introduce o selecciona un valor.

>[!NOTE]
>
>El texto del marcador de posición, si se especifica, debe tener un valor que no contenga caracteres de línea nuevos.

![Componente de fecha con y sin texto de marcador de posición](assets/dat-picker-place-holder-text.png)

******A. Componente de fecha con texto de marcador de posición** B. Componente de fecha sin texto de marcador de posición

Los formularios AEM admiten texto de marcador de posición para los campos Cuadro de contraseña, Selector de fecha, Cuadro numérico y Cuadro de texto.\
Los textos de los marcadores de posición no son compatibles con la utilidad de fecha HTML5 nativa. Para especificar un texto de marcador de posición:

1. Haga clic con el botón secundario en un componente que admita Texto de marcador de posición y haga clic en **Editar**. Aparecerá el cuadro de diálogo Editar componente.

1. Abra la ficha **Título y texto** .
1. Especifique una palabra o una frase corta en el cuadro **de texto Marcador de** posición. Haga clic en **Aceptar**.

>[!NOTE]
>
>El texto del marcador de posición no es compatible con Microsoft Internet Explorer 9.

