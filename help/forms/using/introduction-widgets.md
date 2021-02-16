---
title: Marco de apariencia para formularios adaptables y HTML5
seo-title: Marco de apariencia para formularios adaptables y HTML5
description: Forms móvil procesa las plantillas de formulario como formularios HTML5. Estos formularios utilizan archivos jQuery, Backbone.js y Underscore.js para la apariencia y para activar las secuencias de comandos.
seo-description: Forms móvil procesa las plantillas de formulario como formularios HTML5. Estos formularios utilizan archivos jQuery, Backbone.js y Underscore.js para la apariencia y para activar las secuencias de comandos.
uuid: 183b8d71-44fc-47bf-8cb2-1cf920ffd23a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 3c2a44a7-24e7-49ee-bf18-eab0e44efa42
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 3%

---


# Marco de aspecto para formularios adaptables y HTML5 {#appearance-framework-for-adaptive-and-html-forms}

Forms (formularios adaptables y formularios HTML5) utiliza bibliotecas [jQuery](https://jquery.com/), [Backbone.js](https://backbonejs.org/) y [Underscore.js](https://underscorejs.org/) para apariencia y secuencias de comandos. Los formularios también utilizan la arquitectura [jQuery UI](https://jqueryui.com/) **Widgets** para todos los elementos interactivos (como campos y botones) del formulario. Esta arquitectura permite al desarrollador de formularios utilizar un completo conjunto de utilidades y complementos jQuery disponibles en Forms. También puede implementar lógica específica del formulario al capturar datos de usuarios como las restricciones de leadDigits/trackDigits o la implementación de cláusulas de imagen. Los desarrolladores de formularios pueden crear y utilizar apariencias personalizadas para mejorar la experiencia de captura de datos y hacerla más sencilla.

Este artículo está dirigido a los desarrolladores con suficiente conocimiento de las utilidades jQuery y jQuery. Proporciona una visión detallada del marco de trabajo de apariencia y permite a los desarrolladores crear un aspecto alternativo para un campo de formulario.

La estructura de aspecto se basa en diversas opciones, eventos (déclencheur) y funciones para capturar las interacciones del usuario con el formulario, y responde a los cambios del modelo para informar al usuario final. Además:

* La estructura proporciona un conjunto de opciones para el aspecto de un campo. Estas opciones son pares de clave-valor y se dividen en dos categorías: opciones comunes y opciones específicas de tipo de campo.
* El aspecto, como parte del contrato, déclencheur un conjunto de eventos como entrar y salir.
* El aspecto es necesario para implementar un conjunto de funciones. Algunas de las funciones son comunes, mientras que otras son específicas de las funciones de tipo de campo.

## Opciones comunes {#common-options}

Las siguientes son las opciones globales definidas. Estas opciones están disponibles para cada campo.

<table>
 <tbody>
  <tr>
   <th>Propiedad </th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>name</td>
   <td>Identificador utilizado para especificar este objeto o evento en expresiones de secuencias de comandos. Por ejemplo, esta propiedad especifica el nombre de la aplicación host.</td>
  </tr>
  <tr>
   <td>seleccionado</td>
   <td>Valor real del campo. </td>
  </tr>
  <tr>
   <td>displayValue</td>
   <td>Se muestra este valor del campo. </td>
  </tr>
  <tr>
   <td>screenReaderText</td>
   <td>Los Reader de pantalla utilizan este valor para contar información sobre el campo. El formulario proporciona el valor y puede sobrescribirlo.<br /> </td>
  </tr>
  <tr>
   <td>tabIndex</td>
   <td>Posición del campo en la secuencia de tabulación del formulario. Sobrescriba el tabIndex sólo si desea cambiar el orden de tabulación predeterminado del formulario.</td>
  </tr>
  <tr>
   <td>role</td>
   <td>Función del elemento, por ejemplo, Encabezado o Tabla.</td>
  </tr>
  <tr>
   <td>altura</td>
   <td>Altura del widget. Se especifica en píxeles. </td>
  </tr>
  <tr>
   <td>Anchura</td>
   <td>Ancho del widget. Se especifica en píxeles.</td>
  </tr>
  <tr>
   <td>access</td>
   <td>Controles utilizados para acceder al contenido de un objeto de contenedor, como un subformulario.</td>
  </tr>
  <tr>
   <td>paraStyles</td>
   <td>Propiedad para de un elemento XFA en la utilidad.</td>
  </tr>
  <tr>
   <td>dir</td>
   <td>Dirección del texto. Los valores posibles son ltr (de izquierda a derecha) y rtl (de derecha a izquierda).</td>
  </tr>
 </tbody>
</table>

Aparte de estas opciones, la estructura ofrece otras opciones que varían según el tipo de campo. A continuación se detallan las opciones específicas de los campos.

### Interacción con el marco de formularios {#interaction-with-forms-framework}

Para interactuar con la estructura de formularios, una utilidad déclencheur algunos eventos para permitir que funcione la secuencia de comandos del formulario. Si la utilidad no emite estos eventos, algunas de las secuencias de comandos escritas en el formulario para ese campo no funcionan.

#### Eventos activados por la utilidad {#events-triggered-by-widget}

<table>
 <tbody>
  <tr>
   <th>Evento </th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>XFA_ENTER_EVENTO</td>
   <td>Este evento se activa cada vez que el campo está activo. Permite que la secuencia de comandos "enter" se ejecute en el campo. La sintaxis para activar el evento es<br /> (utilidad)._déclencheur(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENTO)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_EVENTO</td>
   <td>Este evento se activa cada vez que el usuario abandona el campo. Permite que el motor establezca el valor del campo y ejecute su secuencia de comandos "exit". La sintaxis para activar el evento es<br /> (utilidad)._déclencheur(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENTO)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENTO</td>
   <td>Este evento se activa para permitir que el motor ejecute la secuencia de comandos de "cambio" escrita en el campo. La sintaxis para activar el evento es<br /> (utilidad)._déclencheur(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENTO)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_EVENTO</td>
   <td>Este evento se activa cada vez que se hace clic en el campo. permite al motor ejecutar la secuencia de comandos de "clic" escrita en el campo. La sintaxis para activar el evento es<br /> (utilidad)._déclencheur(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENTO)<br /> </td>
  </tr>
 </tbody>
</table>

#### API implementadas por la utilidad {#apis-implemented-by-widget}

La estructura de apariencia llama a algunas funciones de la utilidad que se implementan en las utilidades personalizadas. La utilidad debe implementar las siguientes funciones:

<table>
 <tbody>
  <tr>
   <th>Función</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>focus: function()</td>
   <td>Centra la atención en el campo.</td>
  </tr>
  <tr>
   <td>haga clic en: function()</td>
   <td>Centra la atención en el campo y llama a XFA_CLICK_EVENTO.</td>
  </tr>
  <tr>
   <td><p>markError:function(errorMessage, errorType)<br /> <br /> <em>errorMessage: cadena </em>que representa el error<br /> <em>errorType: string ("warning"/"error")</em></p> <p><strong>Nota</strong>: Aplicable solo para formularios HTML5.</p> </td>
   <td>Envía un mensaje de error y un tipo de error a la utilidad. La utilidad muestra el error.</td>
  </tr>
  <tr>
   <td><p>clearError: function()</p> <p><strong>Nota</strong>: Aplicable solo para formularios HTML5.</p> </td>
   <td>Se llama si se corrigen los errores en el campo. La utilidad oculta el error.</td>
  </tr>
 </tbody>
</table>

## Opciones específicas del tipo de campo {#options-specific-to-type-of-field}

Todos los widgets personalizados deben cumplir las especificaciones anteriores. Para utilizar las funciones de distintos campos, la utilidad debe cumplir las directrices de ese campo concreto.

### TextEdit: Campo de texto {#textedit-text-field}

<table>
 <tbody>
  <tr>
   <th>Opción</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>multiline</td>
   <td>True si el campo admite la introducción de un carácter de nueva línea; en caso contrario, false.</td>
  </tr>
  <tr>
   <td>maxChars</td>
   <td>Número máximo de caracteres que se pueden introducir en el campo.</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>Nota</strong>: Aplicable solo para formularios HTML5</p> </td>
   <td>Especifica el comportamiento del campo de texto cuando la anchura del texto supera la anchura del widget.</td>
  </tr>
 </tbody>
</table>

### ChoiceList: DropDownList, ListBox {#choicelist-dropdownlist-listbox}

<table>
 <tbody>
  <tr>
   <th>Opción</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>seleccionado<br /> </td>
   <td>Matriz de valores seleccionados.<br /> </td>
  </tr>
  <tr>
   <td>items<br /> </td>
   <td>Matriz de objetos que se mostrarán como opciones. Cada objeto contiene dos propiedades:<br /> save: valor para guardar, mostrar: valor para mostrar.<br /> <br /> </td>
  </tr>
  <tr>
   <td><p>editable</p> <p><strong>Nota</strong>: Aplicable solo para formularios HTML5.<br /> </p> </td>
   <td>Si el valor es true, la entrada de texto personalizada está habilitada en la utilidad.<br /> </td>
  </tr>
  <tr>
   <td>displayValue<br /> </td>
   <td>Matriz de valores para mostrar.<br /> </td>
  </tr>
  <tr>
   <td>multiselect<br /> </td>
   <td>True si se permiten varias selecciones, de lo contrario false.<br /> </td>
  </tr>
 </tbody>
</table>

#### API {#api}

<table>
 <tbody>
  <tr>
   <th>Función</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><p>addItem:<em> function(itemValues)<br /> itemValues: objeto que contiene el valor de visualización y guardado <br /> {sDisplayVal: &lt;displayValue&gt;, sSaveVal: &lt;save Value&gt;}</em></p> </td>
   <td>Añade un elemento a la lista.</td>
  </tr>
  <tr>
   <td>deleteItem<em>: function(nIndex)<br /> nIndex: índice del elemento que se va a quitar de la lista<br /> </em><br /> <br /> </td>
   <td>Elimina una opción de la lista.</td>
  </tr>
  <tr>
   <td>clearItems:<code> function()</code></td>
   <td>Borra todas las opciones de la lista.</td>
  </tr>
 </tbody>
</table>

### NumericEdit: NumericField, DecimalField {#numericedit-numericfield-decimalfield}

| Opciones | Descripción |
|---|---|
| dataType | Cadena que representa el tipo de datos del campo (entero/decimal). |
| leadDigits | Número máximo de dígitos al principio permitidos en el número decimal. |
| fracDigits | Dígitos de fracción máximos permitidos en el número decimal. |
| zero | Representación de cadena de cero en la configuración regional del campo. |
| decimal | Representación de cadena de decimales en la configuración regional del campo. |

### CheckButton: RadioButton, CheckBox {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>Opciones</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>values</td>
   <td><p>Matriz de valores (activado/desactivado/neutro).</p> <p>Es una matriz de valores para los diferentes estados de checkButton. values[0] es el valor cuando el estado está activado, values[1] es el valor cuando el estado está desactivado,<br /> valores[2] es el valor cuando el estado es NEUTRAL. La longitud de la matriz de valores es igual al valor de la opción de estado.<br /> </p> </td>
  </tr>
  <tr>
   <td>estados</td>
   <td><p>Número de estados permitidos. </p> <p>Dos para formularios adaptables (activado, desactivado) y tres para formularios HTML5 (activado, desactivado, neutro).</p> </td>
  </tr>
  <tr>
   <td>estado</td>
   <td><p>Estado actual del elemento.</p> <p>Dos para formularios adaptables (activado, desactivado) y tres para formularios HTML5 (activado, desactivado, neutro).</p> </td>
  </tr>
 </tbody>
</table>

### DateTimeEdit: (DateField) {#datetimeedit-datefield}

| Opción | Descripción |
|---|---|
| días | Nombre localizado de días para ese campo. |
| meses | Nombres de mes localizados para ese campo. |
| zero | Texto localizado para el número 0. |
| clearText | Texto localizado para el botón borrar. |
