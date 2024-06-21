---
title: Configurar las opciones de internacionalización
description: Obtenga información sobre cómo especificar la configuración regional utilizada para procesar formularios y cómo especificar el conjunto de caracteres utilizado para codificar el flujo de salida.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6cf82c2b-29f0-49d5-a138-99d7801d5a28
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 4%

---

# Configurar las opciones de internacionalización{#setting-internationalization-options}

## Especifique la configuración regional utilizada para procesar formularios {#specify-the-locale-used-to-render-forms}

Puede especificar la configuración regional utilizada al procesar un formulario de PDF. Los campos de un formulario de PDF utilizan la configuración regional especificada para mostrar datos. Por ejemplo, si la configuración regional está establecida en alemán, el formulario utiliza separadores decimales alemanes para los valores numéricos. La configuración regional también se utiliza para enviar mensajes de validación a dispositivos cliente, como exploradores web, como parte de las transformaciones de HTML.

1. En la consola de administración, haga clic en Servicios > Forms.
1. En Internacionalización, en la lista Idioma, seleccione la configuración regional utilizada para procesar un formulario. El valor predeterminado es Inglés (Estados Unidos).
1. Haga clic en Guardar.

## Especifique el conjunto de caracteres utilizado para codificar el flujo de salida {#specify-the-character-set-used-to-encode-the-output-stream}

1. En Internacionalización, en la lista Conjunto de caracteres, seleccione un conjunto de caracteres. Esta configuración depende de la API utilizada, renderHTMLForm o renderPDFForm. Para especificar un conjunto de caracteres distinto de los enumerados, seleccione Personalizado y especifique un valor de codificación en el cuadro que se muestra.

   Para las transformaciones de HTML AEM, los formularios de datos de la aplicación admiten valores de codificación de caracteres definidos por el `java.nio.charset` paquete. Si sFormPreference es PDFForm, solo se admiten conjuntos de caracteres específicos. El conjunto de caracteres debe ser un nombre canónico válido. El valor predeterminado es ISO-8859-1.

1. Haga clic en Guardar.
