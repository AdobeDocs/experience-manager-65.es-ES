---
title: Configurar la salida del formulario
description: Obtenga información sobre cómo configurar la salida del formulario. Para configurar la salida del formulario y habilitar la función, utilice secuencias de comandos personalizadas antes del envío del formulario.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 8%

---

# Configurar la salida del formulario{#configuring-form-output}

## Especifique el tipo de salida del HTML devuelta al explorador web {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. En la consola de administración, haga clic en Servicios > Formularios.
1. En Salida de formulario, en la lista Tipo de salida, seleccione una de las siguientes opciones:

   **HTML completo:** Para procesar el formulario con las HTML completas (una página completa del HTML). Este valor es el predeterminado.

   **Cuerpo del formulario:** Para procesar el formulario en `<BODY>` etiquetas (no es una página de HTML completa).

1. Haga clic en Guardar.

## Especifique la ubicación donde se procesa el contenido del PDF {#specify-the-location-where-pdf-content-is-rendered}

1. En Salida de formulario, en la lista Procesar en, seleccione una de las siguientes opciones:

   **Cliente:** Para procesar PDF forms en Adobe Acrobat o Adobe Reader. AEM El procesamiento del lado del cliente mejora el rendimiento de los formularios de la y se aplica solo a la transformación del formulario PDF.

   **Servidor:** Para procesar PDF forms en el servidor de aplicaciones.

   **Automático:** Para procesar el formulario de PDF en la ubicación especificada por la variable `dynamicRender` valor de configuración del archivo XDP. Este valor es el predeterminado.

1. Haga clic en Guardar.

## Configurar la invocación de scripts personalizados antes del envío del formulario {#configuring-invocation-of-custom-scripts-before-form-submit}

Siga los siguientes pasos para habilitar la función:

1. Inicie sesión en la consola de administración.
1. Ir a **Servicios** > **formularios**.
1. Especifique el Tipo de salida como Cuerpo del formulario.
1. Guarde la configuración.
1. Declare una variable JavaScript, __CUSTOM_SCRIPTS_VERSION, en la sección head del código de HTML y establezca su valor en 1.

   >[!NOTE]
   >
   >*Para deshabilitar esta función, puede quitar la variable JavaScript o establecer su valor en 0.*
