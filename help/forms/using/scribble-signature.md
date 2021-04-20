---
title: Uso de la firma manuscrita en formularios HTML5
seo-title: Uso de la firma manuscrita en formularios HTML5
description: Los formularios HTML5 se utilizan cada vez más en dispositivos táctiles y uno de los requisitos comunes es admitir firmas. La firma de documentos en dispositivos móviles se está convirtiendo en una forma aceptada de firmar formularios en dispositivos móviles.
seo-description: Los formularios HTML5 se utilizan cada vez más en dispositivos táctiles y uno de los requisitos comunes es admitir firmas. La firma de documentos en dispositivos móviles se está convirtiendo en una forma aceptada de firmar formularios en dispositivos móviles.
uuid: 163dd55a-971a-4dd4-93a7-a14e80184d9b
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
discoiquuid: ecd7f538-9c24-48e7-8450-596851e99cff
docset: aem65
feature: Designer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---


# Uso de la firma manuscrita en formularios HTML5{#using-scribble-signature-in-html-forms}

Los formularios HTML5 se utilizan cada vez más en dispositivos táctiles y uno de los requisitos comunes es admitir firmas. La creación de secuencias de comandos (escritura con un lápiz o un dedo) se está convirtiendo en una forma aceptada de firmar formularios en dispositivos móviles. Los formularios HTML5 y Forms Designer ahora habilitan la opción de tener un campo de firma de anotaciones en el formulario. Cuando el formulario se procesa en el explorador, se puede iniciar sesión en estos campos con un lápiz, ratón o contacto.

## Cómo diseñar un formulario utilizando Scribble Signature field {#how-to-design-a-form-using-scribble-signature-field}

1. Abra un formulario en Forms Designer.
1. Arrastre y suelte el campo Scribble de firma en la página.

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >Los Dimension del campo seleccionado en Forms Designer se reflejan cuando se procesa el campo. Sin embargo, la dimensión del cuadro de firma procesada se calcula en función de la relación de aspecto del campo y no de la dimensión especificada en Forms Designer.

1. Configure el campo Scribble de firma .

   El campo Scribble de firma, de forma predeterminada, marca la información de geolocalización como obligatoria durante el proceso de firma en iPad (y es opcional para otros dispositivos). Este comportamiento predeterminado se puede anular cambiando el valor de la propiedad `geoLocMandatoryOnIpad` . Esta propiedad se expone como extras en el campo Scribble de firma . Los pasos para modificarla son:

   1. En el formulario, seleccione el campo Scribble de firma .
   1. Seleccione la pestaña **XML Source**.

      >[!NOTE]
      >
      >Para abrir la ficha Código fuente XML, haga clic en **Ver** > **Código fuente XML**.

   1. Busque la etiqueta `<ui>` en la etiqueta `<field>` y modifique el código fuente para que tenga el aspecto siguiente:

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. Seleccione la pestaña **Vista diseño**. En el cuadro de confirmación, haga clic en **Yes**.
   1. Guarde el formulario.

1. Representar el formulario en un explorador de escritorio o dispositivo compatible.

## Interrelación con las firmas manuscritas {#interfacing-with-the-scribble-signatures}

### Firmando {#signing}

Una vez que se ha agregado un campo de Scribble de firma al formulario y se ha procesado, al pulsar o hacer clic en el campo se abre un cuadro de diálogo. El usuario puede garabatear una firma en el área de dibujo designada por un rectángulo de puntos, utilizando un ratón, un dedo o un lápiz.

![geolocalización](assets/geolocation.png)

**A.** Brush  **B.** Eraser  **C.** Geolocation  **D.** Información de geolocalización

### Etiquetado geográfico {#geo-tagging}

Al hacer clic en el icono de geolocalización mientras se crea la secuencia de comandos, la ubicación geográfica y la información horaria se incrustan en el campo.

>[!NOTE]
De forma predeterminada, en el iPad, la incrustación de información de geolocalización es obligatoria.

En el iPad, el icono de geolocalización no se muestra de forma predeterminada y la información de geolocalización se incrusta automáticamente al hacer clic en **OK**.

Para los iPads, esta configuración se puede modificar modificando el valor del parámetro `geoLocManadatoryOnIpad` a `0` en los parámetros init del campo .

* Cuando la información de geolocalización es obligatoria, al usuario se le presenta un área de dibujo reducida. El texto de geolocalización se agrega cuando el usuario hace clic en el icono **OK** del área restante.
* En otros casos, el usuario se presenta con un área de cajón completa. Si el usuario decide incrustar la información de geolocalización, esta área cambia de tamaño para ajustarse al texto de geolocalización.

### Borrar una firma {#clearing-a-signature}

Al utilizar esta función, un usuario puede hacer clic en el icono **Borrador** para borrar el campo y volver a empezar. Si se agregó información de geolocalización, también se borra.

### Guardar una firma {#saving-a-signature}

Al hacer clic en el icono **OK** se guarda el garabato como una imagen en el campo. La imagen y los valores se pueden enviar al servidor para un procesamiento posterior. Una vez que un usuario ha hecho clic en **OK**, el campo de anotaciones está bloqueado. La firma no se puede volver a editar con el widget de anotaciones.

Al pulsar o hacer clic en el campo Scribble se abre el cuadro de diálogo en modo de solo lectura.

![3](assets/3.png)

### Selección del tamaño de la pluma {#selecting-pen-size}

Haga clic en el icono **Brushes** para mostrar una lista de los tamaños de pluma disponibles. Toque o haga clic en un tamaño de pluma para usar la pluma correspondiente.

### Eliminar firmas del formulario {#delete-signatures-from-the-form}

Para eliminar las firmas del formulario:

* (Dispositivos móviles) Pulse durante mucho tiempo el campo de firma y, en el cuadro de diálogo de confirmación, pulse **Yes**.
* (Escritorio) Pase el ratón sobre el campo de firma, haga clic en el icono **Cancelar** y, en el cuadro de diálogo de confirmación, haga clic en **Sí**.
