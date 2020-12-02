---
title: Configuración del resultado del formulario
seo-title: Configuración del resultado del formulario
description: Obtenga información sobre cómo configurar la salida del formulario.
seo-description: Obtenga información sobre cómo configurar la salida del formulario.
uuid: 70aad14e-c845-4ef3-a751-ad8860d5d505
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 17c9b69a-3c6f-47e3-a828-841bb90eba8b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---


# Configuración del resultado del formulario{#configuring-form-output}

## Especifique el tipo de salida HTML devuelta al explorador Web {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. En la consola de administración, haga clic en Servicios > formularios.
1. En Salida de formulario, en la lista Tipo de salida, seleccione una de las siguientes opciones:

   **HTML completo:** para procesar el formulario con etiquetas HTML completas (una página HTML completa). Este valor es el predeterminado.

   **Cuerpo del formulario:** Para procesar el formulario con  `<BODY>` etiquetas (no una página HTML completa).

1. Haga clic en Guardar.

## Especifique la ubicación en la que se procesa el contenido PDF {#specify-the-location-where-pdf-content-is-rendered}

1. En Salida de formulario, en Procesar en la lista, seleccione una de las siguientes opciones:

   **Cliente:** Para procesar PDF forms en Adobe Acrobat o Adobe Reader. El procesamiento en el lado del cliente mejora el rendimiento de AEM formularios y se aplica solo a la transformación PDFForm.

   **Servidor:** Para procesar PDF forms en el servidor de aplicaciones.

   **Automático:** Para procesar el formulario PDF en la ubicación especificada por el valor de  `dynamicRender` configuración del archivo XDP. Este valor es el predeterminado.

1. Haga clic en Guardar.

## Configuración de la invocación de secuencias de comandos personalizadas antes del envío de formularios {#configuring-invocation-of-custom-scripts-before-form-submit}

Realice los siguientes pasos para habilitar la función:

1. Inicie sesión en la consola de administración.
1. Vaya a **Servicios** > **formularios**.
1. Especifique el tipo Salida como Cuerpo del formulario.
1. Guarde la configuración.
1. Declare una variable de JavaScript, __CUSTOM_SCRIPTS_VERSION, en la sección del encabezado del código HTML y defina su valor en 1.

   >[!NOTE]
   >
   >*Para deshabilitar la función, puede eliminar la variable JavaScript o establecer su valor en 0.*

