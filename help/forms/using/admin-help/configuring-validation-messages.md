---
title: Configuración de los mensajes de validación
seo-title: Configuración de los mensajes de validación
description: Descubra cómo se muestran los mensajes de validación y su ubicación en relación con el formulario devuelto en el navegador web.
seo-description: Descubra cómo se muestran los mensajes de validación y su ubicación en relación con el formulario devuelto en el navegador web.
uuid: f6bff4fa-f90f-4135-ae40-7ab3d3613122
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f2f8129-e45e-4f3f-ae30-c09330d0e152
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración de los mensajes de validación {#configuring-validation-messages}

En el caso de los formularios procesados como HTML, los errores de validación que se producen se muestran al usuario. Puede personalizar el modo en que se muestran los mensajes de validación. En función de dónde se muestren los mensajes de validación, también puede controlar la ubicación del mensaje en el formulario y el tamaño del borde del marco.

## Especificar cómo se muestran los mensajes de validación {#specify-how-validation-messages-are-displayed}

1. En la consola de administración, haga clic en Servicios > formularios.
1. En Resultados de validación, en la lista Informes, seleccione una de las siguientes opciones:

   **** Cuadro de mensaje: Para mostrar mensajes de validación en un cuadro de diálogo independiente.

   **** Marco: Para mostrar mensajes de validación dentro de un marco de la misma ventana.

   **** Sin marco: Para mostrar mensajes de validación en la misma ventana. Este valor es el predeterminado.

   **** Mediante API (con datos): Para devolver los mensajes de validación a través de la API (con datos). Los mensajes de validación no se muestran en la pantalla.

   **** Mediante API (con formulario): Para devolver los mensajes de validación a través de la API (con el formulario). Los mensajes de validación no se muestran en la pantalla.

   **** Ninguno: Para no mostrar mensajes de validación.

1. Haga clic en Guardar.

## Especificar la ubicación de los mensajes de validación en relación con el formulario devuelto en el explorador Web {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

Cuando Informes se establece en Marco o Sin marco, puede especificar la ubicación de los mensajes de validación.

1. En Resultados de validación, en la lista Posición, seleccione una de las siguientes opciones:

   **** Izquierda: Para mostrar mensajes de validación en el lado izquierdo del explorador web.

   **** Derecha: Para mostrar mensajes de validación en el lado derecho del explorador web.

   **Superior**: Para mostrar mensajes de validación en la parte superior del explorador Web. Este valor es el predeterminado.

   **Inferior**: Para mostrar mensajes de validación en la parte inferior del explorador Web.

1. Haga clic en Guardar.

## Especificar el tamaño del borde del marco {#specify-the-frame-border-size}

Cuando Informes se establece en Marco, puede especificar el tamaño del borde del marco.

1. En Salida de validación, en el cuadro Tamaño del borde, escriba el tamaño del borde del marco, en píxeles.

   El tamaño del borde debe ser igual o mayor que 0. El valor predeterminado es 1.

1. Haga clic en Guardar.

