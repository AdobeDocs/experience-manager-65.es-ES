---
title: Creación de estilos CSS para formularios HTML5
seo-title: Creación de estilos CSS para formularios HTML5
description: Aprenda a cambiar el aspecto de los formularios HTML5 modificando la clase CSS asociada al elemento de formulario HTML.
seo-description: Aprenda a cambiar el aspecto de los formularios HTML5 modificando la clase CSS asociada al elemento de formulario HTML.
uuid: 43c689b4-243c-43de-a8be-1eef10d75295
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a8d986ab-2a4c-488b-957e-4606f7391bd3
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 4%

---


# Creación de estilos CSS para formularios HTML5 {#creating-css-styles-for-html-forms}

La representación HTML5 de una plantilla de formulario basada en XFA consta de varios elementos HTML. Estos elementos se organizan en un orden. Cada elemento tiene clases CSS bien definidas. Puede utilizar estas clases CSS para seleccionar y cambiar el aspecto de un elemento.

>[!NOTE]
>
>En las clases CSS, no cambie el valor de los atributos width, height, border-thickness, top, left, right, bottom, padding, margin y other position and size . Cualquier cambio en los atributos de posición y tamaño produce cambios en la presentación del formulario.

## Clases CSS  para elementos  {#css-classes-nbsp-for-elements-nbsp}

Cada elemento contiene clases CSS bien definidas. Puede modificar estas clases para cambiar el aspecto de un elemento. Todos los elementos, excepto los elementos de campo y dibujo, tienen dos clases CSS: clase Type y clase Name.

* La clase **Type** representa el tipo del campo XFA. Puede anular la clase `type` para modificar los estilos de todos los elementos de un tipo concreto.

* La **Name class** corresponde al nombre del campo XFA. Puede anular la clase `name` para modificar y aplicar estilo personalizado a un elemento.

>[!NOTE]
>
>Algunos elementos XFA no tienen nombre. Para cambiar los estilos de dichos componentes, modifique todos los componentes de ese tipo concreto.

Para las páginas no nombradas en el Diseñador de AEM Forms, las páginas de un formulario HTML5 reciben un nombre en el orden creciente de su número. Por ejemplo, para un formulario HTML5 con dos páginas, las páginas se denominan Página1, Página2.

## Elemento de campo {#field-element}

El elemento de campo contiene dos elementos anidados: widget y rótulo.

**Elemento Widget**

El elemento widget contiene el elemento de interfaz de usuario para la interacción con los usuarios. Tiene tres clases CSS:

* **Utilidad**: Cada utilidad tiene esta clase.
* **nombre**: Todos los widgets enviados con AEM contienen la clase de nombre del widget. Para las utilidades personalizadas, el desarrollador de utilidades proporciona la clase Widget name .
* **tipo**: Cada utilidad tiene un elemento de interfaz de usuario. Esta clase define el tipo del elemento de interfaz de usuario.

```xml
<!--field with caption-->
<div class="field numericfield NumericField3 ">
     <div class="caption">
        caption content
     </div>
     <div class="widget numericfieldwidget numericInput">
       widget content
     </div>
</div>

<!--field without caption-->
<div class="widget numericfieldwidget numericInput">
   widget content
</div>
```

Además de la clase type y name , el componente de campo también contiene una clase CSS adicional denominada **subtype**. Un subtipo identifica qué tipo de campo es, por ejemplo, NumericField, DateField, TextField. Puede anular la clase subtype para modificar el estilo de todos los campos de tipo subtype.

## Clases CSS para diferentes componentes {#css-classes-for-different-components}

<table>
 <tbody>
  <tr>
   <td><strong>Componente</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Nombre</strong></td>
  </tr>
  <tr>
   <td>Página</td>
   <td>page</td>
   <td>Nombre definido por el usuario<br /> o<br /> Página&lt;pageNumber&gt; (predeterminado)</td>
  </tr>
  <tr>
   <td>Área de contenido</td>
   <td>contentarea</td>
   <td>Nombre definido por el usuario</td>
  </tr>
  <tr>
   <td>Subformulario</td>
   <td>subform</td>
   <td>Nombre definido por el usuario</td>
  </tr>
  <tr>
   <td>Grupo de exclusión</td>
   <td>exclgroup</td>
   <td>Nombre definido por el usuario</td>
  </tr>
  <tr>
   <td>Draw</td>
   <td>draw</td>
   <td>Nombre definido por el usuario</td>
  </tr>
  <tr>
   <td>Campo</td>
   <td>field</td>
   <td>Nombre definido por el usuario</td>
  </tr>
  <tr>
   <td>Pie de ilustración</td>
   <td>caption</td>
   <td>ND</td>
  </tr>
  <tr>
   <td>Widget</td>
   <td>widget</td>
   <td>El desarrollador de utilidades lo define (para widgets definidos por el usuario, consulte la tabla en la siguiente sección)</td>
  </tr>
 </tbody>
</table>

## Clases CSS para diferentes campos {#css-classes-for-different-fields}

AEM Forms Designer admite distintos tipos de campos en un formulario, como NumericField, DecimalField y Date Field. Todos estos campos en HTML contienen las clases CSS mencionadas anteriormente. También contienen algunas clases adicionales según el tipo de campo.

Cada campo tiene un widget asociado que representa el elemento UI. A continuación se enumeran las clases de cada campo y las utilidades asociadas a cada campo.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de campo</strong></td>
   <td><strong>Subtipo</strong></td>
   <td><strong>Nombre de la utilidad</strong></td>
   <td><strong>Tipo de utilidad</strong></td>
   <td><strong>Etiqueta de IU HTML</strong></td>
  </tr>
  <tr>
   <td>Botón<br type="_moz" /> </td>
   <td>ND</td>
   <td>xfaButton<br type="_moz" /> </td>
   <td>widget<br type="_moz" /> </td>
   <td>input type=button<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CheckButton<br type="_moz" /> </td>
   <td>checkboxfield<br /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>checkboxfieldwidget<br type="_moz" /> </td>
   <td>input type=check<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateField<br type="_moz" /> </td>
   <td>datefield<br type="_moz" /> </td>
   <td>dateField<br type="_moz" /> </td>
   <td>datefieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateTimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget</td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>Campo decimal<br type="_moz" /> </td>
   <td>Numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DropDown<br type="_moz" /> </td>
   <td>lista de opciones<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>select</td>
  </tr>
  <tr>
   <td>ListBox<br type="_moz" /> </td>
   <td>lista de opciones<br type="_moz" /> </td>
   <td>listBoxWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>ol</td>
  </tr>
  <tr>
   <td>NumericField<br type="_moz" /> </td>
   <td>Numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>Campo de contraseña<br type="_moz" /> </td>
   <td>campo de contraseña<br type="_moz" /> </td>
   <td>defaultWidget<br type="_moz" /> </td>
   <td>passwordfieldwidget<br type="_moz" /> </td>
   <td>input type=password<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>RadioButton<br type="_moz" /> </td>
   <td>radiocampo<br type="_moz" /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>utilidad de radiocampo<br type="_moz" /> </td>
   <td>input type=radio<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TextField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## Clases CSS para diferentes elementos de dibujo {#css-classes-for-different-draw-elements}

Con AEM Forms Designer, se pueden insertar elementos estáticos de dibujo como texto e imágenes. Para cada elemento de dibujo, se asocia una clase CSS independiente a ese elemento. A continuación se muestra la lista de clases CSS para elementos de dibujo. Cada elemento de dibujo tiene una clase de dibujo asociada a él.

| **Dibujar tipo** | **Clase de CSS** |
|---|---|
| Texto | text |
| Imagen | image |
| Rectángulo | rectangle |
| Línea | line |

## Estilo de otras partes del formulario {#styling-other-parts-of-the-form}

Además del aspecto de los componentes de la interfaz de usuario en el formulario HTML, puede cambiar el estilo de elementos como Errores en línea, Advertencias en línea y campos con errores de validación.

`Styling Inline Errors`

Cuando la validación de un campo genera un error, se muestra un error en línea cuando el campo está activo. Para cambiar el estilo de los errores en línea, anule el ID de CSS **error-msg**.

`Styling Inline Warnings`

Cuando la validación de un campo genera una advertencia, se muestra una advertencia en línea cuando el campo está activo. Para cambiar el estilo de estas advertencias en línea, anule el identificador CSS **warning-msg**.

`Styling Fields with Validation Errors`

Cuando falla la validación de un campo, cambia el estilo del widget. Este cambio de estilo se realiza aplicando una clase CSS **widgetError** en el componente widget. Para modificar el estilo predeterminado, anule la clase **widgetError**.
