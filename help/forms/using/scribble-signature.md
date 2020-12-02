---
title: Uso de la firma manuscrita en formularios HTML5
seo-title: Uso de la firma manuscrita en formularios HTML5
description: Los formularios HTML5 se utilizan cada vez más en dispositivos táctiles y un requisito común es admitir firmas. La firma de documentos en dispositivos móviles se está convirtiendo en una forma aceptada de firmar formularios en dispositivos móviles.
seo-description: Los formularios HTML5 se utilizan cada vez más en dispositivos táctiles y un requisito común es admitir firmas. La firma de documentos en dispositivos móviles se está convirtiendo en una forma aceptada de firmar formularios en dispositivos móviles.
uuid: 163dd55a-971a-4dd4-93a7-a14e80184d9b
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
discoiquuid: ecd7f538-9c24-48e7-8450-596851e99cff
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---


# Uso de la firma manuscrita en formularios HTML5{#using-scribble-signature-in-html-forms}

Los formularios HTML5 se utilizan cada vez más en dispositivos táctiles y un requisito común es admitir firmas. La creación de secuencias de comandos (escritura con un lápiz o un dedo) se está convirtiendo en una forma aceptada de firmar formularios en dispositivos móviles. Los formularios HTML5 y Forms Designer ahora habilitan la opción de tener un campo de firma de garabatos en el formulario. Cuando el formulario se procesa en el navegador, se puede iniciar sesión en estos campos con un puntero, un ratón o un toque.

## Cómo diseñar un formulario utilizando el campo Firma de garabatos {#how-to-design-a-form-using-scribble-signature-field}

1. Abra un formulario en Forms Designer.
1. Arrastre y suelte el campo Creación de firma en la página.

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >Los Dimension del campo seleccionado en Forms Designer se reflejan cuando se procesa el campo. Sin embargo, la dimensión del cuadro de firma procesado se calcula en función de la proporción de aspecto del campo y no de la dimensión especificada en Forms Designer.

1. Configure el campo Creación de firma.

   De forma predeterminada, el campo Creación de firma marca la información de geolocalización como obligatoria durante el proceso de firma en el iPad (y es opcional para otros dispositivos). Este comportamiento predeterminado se puede anular cambiando el valor de la propiedad `geoLocMandatoryOnIpad`. Esta propiedad está expuesta como extras en el campo Creación de firma. Los pasos para modificarla son:

   1. En el formulario, seleccione el campo Creación de firma.
   1. Seleccione la ficha **Código fuente XML**.

      >[!NOTE]
      >
      >Para abrir la ficha Código fuente XML, haga clic en **Vista** > **Código fuente XML**.

   1. Busque la etiqueta `<ui>` en la etiqueta `<field>` y modifique el código fuente para que tenga el siguiente aspecto:

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. Seleccione la ficha **Vista de diseño**. En el cuadro de confirmación, haga clic en **Sí**.
   1. Guarde el formulario.

1. Representar el formulario en un navegador de escritorio o dispositivo compatible.

## Interrelación con las firmas de garabatos {#interfacing-with-the-scribble-signatures}

### Firma {#signing}

Una vez agregado el campo Creación de firma al formulario y procesado, al tocar o hacer clic en el campo se abre un cuadro de diálogo. El usuario puede garabatear una firma en el área de dibujo designada por un rectángulo de puntos, utilizando un ratón, un dedo o un lápiz.

![geolocalización](assets/geolocation.png)

**A.** Brush  **B.** Eraser  **C.** Geolocation  **D.** Geolocation

### Etiquetado geográfico {#geo-tagging}

Al hacer clic en el icono de geolocalización mientras se crea el garabato, la ubicación geográfica y la información de tiempo se incrustan en el campo.

>[!NOTE]
De forma predeterminada, en el iPad es obligatorio incrustar información de geolocalización.

En el iPad, el icono de geolocalización no se muestra de forma predeterminada y la información de geolocalización se incrusta automáticamente al hacer clic en **Aceptar**.

Para los iPad, esta configuración se puede modificar modificando el valor del parámetro `geoLocManadatoryOnIpad` a `0` en los parámetros init del campo.

* Cuando la información de geolocalización es obligatoria, se presenta al usuario un área de dibujo reducida. El texto de geolocalización se agrega cuando el usuario hace clic en el icono **Aceptar** en el área restante.
* En otros casos, se presenta al usuario un área total que se puede utilizar. Si el usuario decide incrustar información de geolocalización, esta área cambia de tamaño para dar cabida al texto de geolocalización.

### Borrado de una firma {#clearing-a-signature}

Mientras utiliza esta función, un usuario puede hacer clic en el icono **Borrador** para borrar el campo y pasar el inicio. Si se agregó información de geolocalización, también se borra.

### Guardando una firma {#saving-a-signature}

Al hacer clic en el icono **Aceptar** se guarda el garabato como una imagen en el campo. La imagen y los valores se pueden enviar al servidor para un procesamiento posterior. Una vez que un usuario ha hecho clic en **Aceptar**, el campo de garabatos se bloquea. La firma no se puede volver a editar con el widget de garabatos.

Al tocar o hacer clic en el campo Garabatos, se abre el cuadro de diálogo en modo de solo lectura.

![3](assets/3.png)

### Selección del tamaño de la pluma {#selecting-pen-size}

Haga clic en el icono **Pinceles** para mostrar una lista de los tamaños de pluma disponibles. Toque o haga clic en un tamaño de pluma para utilizar la pluma correspondiente.

### Eliminar firmas del formulario {#delete-signatures-from-the-form}

Para eliminar las firmas del formulario:

* (Dispositivos móviles) Presione el campo de firma y, en el cuadro de diálogo de confirmación, toque **Sí**.
* (Escritorio) Pase el ratón sobre el campo de firma, haga clic en el icono **Cancelar** y, en el cuadro de diálogo de confirmación, haga clic en **Sí**.
