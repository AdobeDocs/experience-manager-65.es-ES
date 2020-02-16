---
title: Configuración de las opciones de internacionalización
seo-title: Configuración de las opciones de internacionalización
description: Obtenga información sobre cómo especificar la configuración regional utilizada para procesar formularios y cómo especificar el conjunto de caracteres utilizado para codificar el flujo de salida.
seo-description: Obtenga información sobre cómo especificar la configuración regional utilizada para procesar formularios y cómo especificar el conjunto de caracteres utilizado para codificar el flujo de salida.
uuid: bb77f5f3-634f-4285-9b10-c4dd40085e69
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e845d13f-bef2-442d-af9a-4f92d7616a46
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración de las opciones de internacionalización{#setting-internationalization-options}

## Especificar la configuración regional utilizada para procesar formularios {#specify-the-locale-used-to-render-forms}

Puede especificar la configuración regional que se utilizará al procesar un formulario PDF. Los campos de un formulario PDF utilizan la configuración regional especificada para mostrar los datos. Por ejemplo, si la configuración regional se establece en alemán, el formulario utiliza separadores decimales alemanes para los valores numéricos. La configuración regional también se utiliza para enviar mensajes de validación a dispositivos cliente, como exploradores web, como parte de transformaciones HTML.

1. En la consola de administración, haga clic en Servicios > Formularios.
1. En Internacionalización, en la lista Idioma, seleccione la configuración regional utilizada para procesar un formulario. El valor predeterminado es inglés (Estados Unidos).
1. Haga clic en Guardar.

## Especifique el conjunto de caracteres utilizado para codificar el flujo de salida {#specify-the-character-set-used-to-encode-the-output-stream}

1. En Internacionalización, en la lista Conjunto de caracteres, seleccione un conjunto de caracteres. Esta configuración depende de la API utilizada, ya sea reneHTMLForm o renePDFForm. Para especificar un conjunto de caracteres distinto de los enumerados, seleccione Personalizado y especifique un valor de codificación en el cuadro que se muestra.

   Para las transformaciones HTML, los formularios AEM admiten valores de codificación de caracteres definidos por el `java.nio.charset` paquete. Si sFormPreference es PDFForm, solo se admiten conjuntos de caracteres específicos. El conjunto de caracteres debe ser un nombre canónico válido. El valor predeterminado es ISO-8859-1.

1. Haga clic en Guardar.

