---
title: Marco de aspecto para formularios adaptables y HTML5
seo-title: Appearance framework for adaptive and HTML5 forms
description: Las plantillas de formulario de Forms móvil se representan como formularios de HTML5. Estos formularios utilizan archivos jQuery, Backbone.js y Underscore.js para el aspecto y para habilitar las secuencias de comandos.
seo-description: Mobile Forms render Form Templates as HTML5 forms. These forms use jQuery, Backbone.js and Underscore.js files for the appearance and to enable scripting.
uuid: 183b8d71-44fc-47bf-8cb2-1cf920ffd23a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 3c2a44a7-24e7-49ee-bf18-eab0e44efa42
exl-id: 3458471a-9815-463e-8044-68631073863c
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 3%

---

# Marco de aspecto para formularios adaptables y HTML5 {#appearance-framework-for-adaptive-and-html-forms}

Forms (formularios adaptables y formularios HTML5) utiliza [jQuery](https://jquery.com/), [Backbone.js](https://backbonejs.org/) y [Guión bajo.js](https://underscorejs.org/) bibliotecas para apariencia y secuencias de comandos. Los formularios también utilizan la variable [Interfaz de usuario de jQuery](https://jqueryui.com/) **Widgets** para todos los elementos interactivos (como campos y botones) del formulario. Esta arquitectura permite al desarrollador de formularios utilizar un completo conjunto de utilidades y complementos jQuery disponibles en Forms. También puede implementar lógica específica del formulario al capturar datos de usuarios como restricciones de leadDigits/trackDigits o la implementación de cláusulas de imagen. Los desarrolladores de formularios pueden crear y utilizar funciones personalizadas para mejorar la experiencia de captura de datos y hacerla más fácil de usar.

Este artículo es para desarrolladores con suficiente conocimiento de las utilidades jQuery y jQuery. Proporciona una perspectiva del marco de trabajo de aspecto visual y permite a los desarrolladores crear un aspecto alternativo para un campo de formulario.

El marco de trabajo de aspecto visual se basa en diversas opciones, eventos (déclencheur) y funciones para capturar las interacciones del usuario con el formulario, y responde a los cambios del modelo para informar al usuario final. Además:

* La estructura proporciona un conjunto de opciones para el aspecto de un campo. Estas opciones son pares de clave-valor y se dividen en dos categorías: opciones comunes y opciones específicas de tipo de campo.
* El aspecto, como parte del contrato, déclencheur un conjunto de eventos como entrar y salir.
* El aspecto es necesario para implementar un conjunto de funciones. Algunas de las funciones son comunes, mientras que otras son específicas de las funciones de tipo de campo.

## Opciones comunes {#common-options}

A continuación se muestran las opciones globales definidas. Estas opciones están disponibles para cada campo.

<table>
 <tbody>
  <tr>
   <th>Propiedad </th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>name</td>
   <td>Identificador utilizado para especificar este objeto o suceso en expresiones de secuencia de comandos. Por ejemplo, esta propiedad especifica el nombre de la aplicación host.</td>
  </tr>
  <tr>
   <td>value</td>
   <td>Valor real del campo. </td>
  </tr>
  <tr>
   <td>displayValue</td>
   <td>Se muestra este valor del campo. </td>
  </tr>
  <tr>
   <td>screenReaderText</td>
   <td>Los Reader de pantalla utilizan este valor para narrar información sobre el campo. El formulario proporciona el valor y puede anularlo.<br /> </td>
  </tr>
  <tr>
   <td>tabIndex</td>
   <td>Posición del campo en la secuencia de tabulación del formulario. Anule el tabIndex solo si desea cambiar el orden de tabulación predeterminado del formulario.</td>
  </tr>
  <tr>
   <td>role</td>
   <td>Función del elemento, por ejemplo, Encabezado o Tabla.</td>
  </tr>
  <tr>
   <td>height</td>
   <td>Altura del widget. Se especifica en píxeles. </td>
  </tr>
  <tr>
   <td>width</td>
   <td>Ancho del widget. Se especifica en píxeles.</td>
  </tr>
  <tr>
   <td>access</td>
   <td>Controles utilizados para acceder al contenido de un objeto contenedor, como un subformulario.</td>
  </tr>
  <tr>
   <td>paraStyles</td>
   <td>Propiedad para de un elemento XFA del widget.</td>
  </tr>
  <tr>
   <td>dir</td>
   <td>Dirección del texto. Los valores posibles son ltr (de izquierda a derecha) y rtl (de derecha a izquierda).</td>
  </tr>
 </tbody>
</table>

Aparte de estas opciones, el marco proporciona otras opciones que varían según el tipo de campo. A continuación se enumeran los detalles de las opciones específicas de los campos.

### Interacción con el marco de formularios {#interaction-with-forms-framework}

Para interactuar con la estructura de formularios, una utilidad déclencheur algunos sucesos para permitir que funcione la secuencia de comandos de formulario. Si la utilidad no desencadena estos sucesos, algunas de las secuencias de comandos escritas en el formulario para ese campo no funcionan.

#### Eventos activados por la utilidad {#events-triggered-by-widget}

<table>
 <tbody>
  <tr>
   <th>Evento </th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>XFA_ENTER_EVENT</td>
   <td>Este evento se activa cada vez que el campo está seleccionado. Permite que la secuencia de comandos "enter" se ejecute en el campo. La sintaxis para activar el evento es<br /> (utilidad)._déclencheur(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_EVENT</td>
   <td>Este evento se activa cada vez que el usuario abandona el campo. Permite que el motor establezca el valor del campo y ejecute su secuencia de comandos "exit". La sintaxis para activar el evento es<br /> (utilidad)._déclencheur(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENT</td>
   <td>Este suceso se activa para permitir que el motor ejecute la secuencia de comandos "change" escrita en el campo. La sintaxis para activar el evento es<br /> (utilidad)._déclencheur(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_EVENT</td>
   <td>Este evento se activa cada vez que se hace clic en el campo. permite al motor ejecutar la secuencia de comandos "click" escrita en el campo. La sintaxis para activar el evento es<br /> (utilidad)._déclencheur(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENT)<br /> </td>
  </tr>
 </tbody>
</table>

#### API implementadas por widget {#apis-implemented-by-widget}

El marco de apariencia llama a algunas funciones del widget que se implementan en los widgets personalizados. La utilidad debe implementar las siguientes funciones:

<table>
 <tbody>
  <tr>
   <th>Función</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>enfoque: function()</td>
   <td>Centra la atención en el campo.</td>
  </tr>
  <tr>
   <td>haga clic en: function()</td>
   <td>Centra la atención en el campo y llama a XFA_CLICK_EVENT.</td>
  </tr>
  <tr>
   <td><p>markError:function(errorMessage, errorType)<br /> <br /> <em>erorrMessage: string </em>representación del error<br /> <em>errorType: string ("warning"/"error")</em></p> <p><strong>Nota</strong>: Aplicable solo para formularios HTML5.</p> </td>
   <td>Envía un mensaje de error y un tipo de error al widget. La utilidad muestra el error.</td>
  </tr>
  <tr>
   <td><p>clearError: function()</p> <p><strong>Nota</strong>: Aplicable solo para formularios HTML5.</p> </td>
   <td>Se llama a si se corrigen los errores en el campo. La utilidad oculta el error.</td>
  </tr>
 </tbody>
</table>

## Opciones específicas del tipo de campo {#options-specific-to-type-of-field}

Todos los widgets personalizados deben cumplir las especificaciones anteriores. Para utilizar las funciones de diferentes campos, la utilidad debe ajustarse a las directrices de ese campo en particular.

### TextEdit: Campo de texto {#textedit-text-field}

<table>
 <tbody>
  <tr>
   <th>Opción</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>multiline</td>
   <td>True si el campo admite la introducción de un carácter de nueva línea, si no es false.</td>
  </tr>
  <tr>
   <td>maxChars</td>
   <td>Número máximo de caracteres que se pueden introducir en el campo .</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>Nota</strong>: Aplicable únicamente a los formularios HTML5</p> </td>
   <td>Especifica el comportamiento del campo de texto cuando el ancho del texto supera el ancho del widget.</td>
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
   <td>value<br /> </td>
   <td>Matriz de valores seleccionados.<br /> </td>
  </tr>
  <tr>
   <td>items<br /> </td>
   <td>Matriz de objetos que se van a mostrar como opciones. Cada objeto contiene dos propiedades:<br /> guardar: valor que desea guardar, mostrar: para mostrar.<br /> <br /> </td>
  </tr>
  <tr>
   <td><p>editable</p> <p><strong>Nota</strong>: Aplicable solo para formularios HTML5.<br /> </p> </td>
   <td>Si el valor es true, la entrada de texto personalizado está habilitada en el widget.<br /> </td>
  </tr>
  <tr>
   <td>displayValue<br /> </td>
   <td>Matriz de valores que se van a mostrar.<br /> </td>
  </tr>
  <tr>
   <td>selección múltiple<br /> </td>
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
   <td><p>addItem:<em> function(itemValues)<br /> itemValues: objeto que contiene el valor de visualización y guardado <br /> {sDisplayVal: &lt;displayvalue&gt;, sSaveVal: &lt;save value=""&gt;}</em></p> </td>
   <td>Agrega un elemento a la lista.</td>
  </tr>
  <tr>
   <td>deleteItem<em>: function(nIndex)<br /> nÍndice: índice del elemento que se va a eliminar de la lista<br /> </em><br /> <br /> </td>
   <td>Elimina una opción de la lista.</td>
  </tr>
  <tr>
   <td>clearItems:<code> function()</code></td>
   <td>Borra todas las opciones de la lista.</td>
  </tr>
 </tbody>
</table>

### NumericEdit: Campo numérico, Campo decimal {#numericedit-numericfield-decimalfield}

| Opciones | Descripción |
|---|---|
| dataType | Cadena que representa el tipo de datos del campo (entero/decimal). |
| leadDigits | Máximo de dígitos al principio permitidos en el número decimal. |
| fracDigits | Dígitos de fracción máxima permitidos en el número decimal. |
| zero | Representación de cadena cero en la configuración regional del campo. |
| decimal | Representación de cadena del decimal en la configuración regional del campo. |

### CheckButton: RadioButton, CheckBox {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>Opciones</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>values</td>
   <td><p>Matriz de valores (encendido/apagado/neutro).</p> <p>Es una matriz de valores para los diferentes estados de checkButton. values[0] es el valor cuando el estado está activado, values[1] es el valor cuando el estado está desactivado,<br /> values[2] es el valor cuando el estado es NEUTRAL. La longitud de la matriz de valores es igual a la opción valor de estado .<br /> </p> </td>
  </tr>
  <tr>
   <td>state</td>
   <td><p>Número de estados permitidos. </p> <p>Dos para formularios adaptables (Activado, Desactivado) y tres para formularios HTML5 (Activado, Desactivado, Neutro).</p> </td>
  </tr>
  <tr>
   <td>estado</td>
   <td><p>Estado actual del elemento.</p> <p>Dos para formularios adaptables (Activado, Desactivado) y tres para formularios HTML5 (Activado, Desactivado, Neutro).</p> </td>
  </tr>
 </tbody>
</table>

### DateTimeEdit: (CampoFecha) {#datetimeedit-datefield}

| Opción | Descripción |
|---|---|
| días | Nombre localizado de días para ese campo. |
| meses | Nombres de mes localizados para ese campo. |
| zero | Texto localizado para el número 0. |
| clearText | Texto localizado para el botón de borrado. |
