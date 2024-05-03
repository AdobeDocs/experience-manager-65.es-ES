---
title: Configurar mensajes de validación
description: Obtenga información sobre cómo especificar cómo se muestran los mensajes de validación y su ubicación en relación con el formulario devuelto en el explorador web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 14314383-5228-4904-98c1-586f48a1142c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 4%

---

# Configurar mensajes de validación {#configuring-validation-messages}

En el caso de los formularios que se representan como HTML, se muestran los errores de validación de formularios que se producen para el usuario. Puede personalizar cómo se muestran los mensajes de validación. Dependiendo de dónde se muestren los mensajes de validación, también puede controlar la ubicación del mensaje en el formulario y el tamaño del borde del marco.

## Especificar cómo se muestran los mensajes de validación {#specify-how-validation-messages-are-displayed}

1. En la consola de administración, haga clic en Servicios > Formularios.
1. En Salida de validación, en la lista Informes, seleccione una de las siguientes opciones:

   **Cuadro de mensaje:** Para mostrar los mensajes de validación en un cuadro de diálogo independiente.

   **Marco:** Para mostrar mensajes de validación dentro de un marco de la misma ventana.

   **Sin marco:** Para mostrar mensajes de validación en la misma ventana. Este valor es el predeterminado.

   **Mediante API (con datos):** Para devolver los mensajes de validación a través de la API (con datos). Los mensajes de validación no se muestran en la pantalla.

   **Mediante API (con formulario):** Para devolver los mensajes de validación mediante la API (con el formulario). Los mensajes de validación no se muestran en la pantalla.

   **Ninguno:** Para no mostrar mensajes de validación.

1. Haga clic en Guardar.

## Especifique la ubicación de los mensajes de validación en relación con el formulario devuelto en el explorador web {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

Cuando Informes se establece en Marco o Sin marco, puede especificar la ubicación de los mensajes de validación.

1. En Salida de validación, en la lista Posición, seleccione una de las siguientes opciones:

   **Izquierda:** Para mostrar mensajes de validación en el lado izquierdo del explorador web.

   **Derecha:** Para mostrar mensajes de validación en el lado derecho del explorador web.

   **Superior**: para mostrar los mensajes de validación en la parte superior del explorador web. Este valor es el predeterminado.

   **Inferior**: para mostrar los mensajes de validación en la parte inferior del explorador web.

1. Haga clic en Guardar.

## Especificar el tamaño del borde del marco {#specify-the-frame-border-size}

Cuando Informes se establece en Marco, puede especificar el tamaño del borde del marco.

1. En Salida de validación, en el cuadro Tamaño del borde, escriba el tamaño del borde del marco, en píxeles.

   El tamaño del borde debe ser igual o mayor que 0. El valor predeterminado es 1.

1. Haga clic en Guardar.
