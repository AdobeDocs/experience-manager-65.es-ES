---
title: Texto de marcador de posición en AEM Forms
seo-title: Placeholder text in AEM Forms
description: El texto de marcador de posición está diseñado para ayudar al usuario con la introducción de datos cuando el control no tiene valor. Puede ser un valor de muestra o una breve descripción del formato esperado.
seo-description: Placeholder text is intended to aid the user with data entry when the control has no value. It could be a sample value or a brief description of the expected format.
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
feature: Adaptive Forms
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '215'
ht-degree: 100%

---

# Texto de marcador de posición en AEM Forms {#placeholder-text-in-aem-forms}

El texto de marcador de posición representa una palabra o una frase corta. Está diseñado para ayudar al usuario a introducir los datos cuando el control no tiene valor. Un texto de marcador de posición puede ser un valor de muestra o una breve descripción del formato esperado. El texto de marcador de posición se muestra antes de que el usuario introduzca un valor, y se quita cuando el usuario introduce o selecciona un valor.

>[!NOTE]
>
>Si se especifica, el texto del marcador de posición debe tener un valor que no contenga caracteres de nueva línea.

![Componente de fecha con y sin texto de marcador de posición](assets/dat-picker-place-holder-text.png)

**A.** Componente de fecha con texto de marcador de posición **B.** Componente de fecha sin texto de marcador de posición

AEM Forms admite texto de marcador de posición en los campos Cuadro de contraseña, Selector de fecha, Cuadro numérico y Cuadro de texto.\
Los textos de los marcadores de posición no son compatibles con el widget de fecha HTML5 nativo. Para especificar un texto de marcador de posición:

1. Haga clic con el botón derecho en un componente que admita texto de marcador de posición y haga clic en **Editar**. Aparecerá el cuadro de diálogo Editar componente.

1. Abra la pestaña **Título y texto**.
1. Especifique una palabra o una frase corta en el **Cuadro de texto de marcador de posición**. Haga clic en **Aceptar**.

>[!NOTE]
>
>El texto del marcador de posición no es compatible con Microsoft Internet Explorer 9.
