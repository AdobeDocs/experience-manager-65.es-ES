---
title: Configuración de mensajes de validación
seo-title: Configuring validation messages
description: Aprenda a especificar cómo se muestran los mensajes de validación y su ubicación en relación con el formulario devuelto en el explorador web.
seo-description: Learn how to specify how validation messages are displayed and their location relative to the form returned in the web browser.
uuid: f6bff4fa-f90f-4135-ae40-7ab3d3613122
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f2f8129-e45e-4f3f-ae30-c09330d0e152
exl-id: 14314383-5228-4904-98c1-586f48a1142c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 2%

---

# Configuración de mensajes de validación {#configuring-validation-messages}

En el caso de los formularios procesados como HTML, los errores de validación de formularios que se producen se muestran al usuario. Puede personalizar el modo en que se muestran los mensajes de validación. Dependiendo de dónde se muestren los mensajes de validación, también puede controlar la ubicación del mensaje en el formulario y el tamaño del borde del marco.

## Especificar cómo se muestran los mensajes de validación {#specify-how-validation-messages-are-displayed}

1. En la consola de administración, haga clic en Servicios > formularios.
1. En Salida de validación, en la lista Informes, seleccione una de las siguientes opciones:

   **Cuadro de mensaje:** Para mostrar los mensajes de validación en un cuadro de diálogo independiente.

   **Marco:** Para mostrar los mensajes de validación dentro de un marco de la misma ventana.

   **Sin fotograma:** Para mostrar los mensajes de validación en la misma ventana. Este valor es el predeterminado.

   **A través de la API (con datos):** Para devolver los mensajes de validación a través de la API (con datos). Los mensajes de validación no se muestran en la pantalla.

   **Mediante API (con formulario):** Para devolver los mensajes de validación a través de la API (con el formulario). Los mensajes de validación no se muestran en la pantalla.

   **Ninguno:** Para no mostrar mensajes de validación.

1. Haga clic en Guardar.

## Especificar la ubicación de los mensajes de validación en relación con el formulario devuelto en el explorador web {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

Cuando el sistema de informes está establecido en Marco o Sin fotograma, puede especificar la ubicación de los mensajes de validación.

1. En Salida de validación, en la lista Posición, seleccione una de las siguientes opciones:

   **Izquierda:** Para mostrar mensajes de validación en la parte izquierda del explorador web.

   **Derecha:** Para mostrar mensajes de validación en el lado derecho del explorador web.

   **Superior**: Para mostrar mensajes de validación en la parte superior del explorador web. Este valor es el predeterminado.

   **Inferior**: Para mostrar los mensajes de validación en la parte inferior del explorador web.

1. Haga clic en Guardar.

## Especificar el tamaño del borde del marco {#specify-the-frame-border-size}

Cuando el Sistema de informes está establecido en Marco, puede especificar el tamaño del borde del marco.

1. En Salida de validación, en el cuadro Tamaño del borde, escriba el tamaño del borde del marco, en píxeles.

   El tamaño del borde debe ser igual o bueno a 0. El valor predeterminado es 1.

1. Haga clic en Guardar.
