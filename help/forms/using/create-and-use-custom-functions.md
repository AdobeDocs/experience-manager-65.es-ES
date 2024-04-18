---
title: Crear y agregar funciones personalizadas en un formulario adaptable
description: AEM Forms admite funciones personalizadas que permiten a los usuarios crear y utilizar sus propias funciones dentro del editor de reglas.
keywords: Agregar una función personalizada, utilizar una función personalizada, crear una función personalizada, utilizar una función personalizada en el editor de reglas.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: a328b4a8-e8dd-42a0-b73b-94e76c7692a8
source-git-commit: 91ab786cd7e0dd75b9ad15058a125605245ec5bb
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 38%

---


# Funciones personalizadas en Forms adaptable (componentes principales)

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/create-and-use-custom-functions) |
| AEM 6.5 | Este artículo |

## Introducción

AEM Forms 6.5 ha introducido la capacidad de definir las funciones de JavaScript que se pueden utilizar para definir reglas comerciales complejas mediante el editor de reglas. AEM Forms proporciona varias de estas funciones personalizadas de forma predeterminada, pero tendrá que definir sus propias funciones personalizadas y utilizarlas en varios formularios.

Las funciones personalizadas amplían las capacidades de los formularios al facilitar la manipulación y el procesamiento de los datos introducidos para satisfacer requisitos específicos. También permiten la modificación dinámica del comportamiento del formulario en función de criterios predefinidos.
En Forms adaptable, puede utilizar funciones personalizadas dentro de [Editor de reglas de un formulario adaptable](/help/forms/using/rule-editor.md) para crear reglas de validación específicas para los campos de formulario.

Comprendamos el uso de la función personalizada en la que los usuarios escriben la dirección de correo electrónico y desea asegurarse de que la dirección de correo electrónico introducida sigue un formato específico (contiene un símbolo &quot;@&quot; y un nombre de dominio). Cree una función personalizada como &quot;ValidateEmail&quot; que tome la dirección de correo electrónico como entrada y devuelva el valor &quot;True&quot; si es válido y el valor &quot;False&quot; en caso contrario.

```javascript
function ValidateEmail(inputText)
{
    var email = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
    if(inputText.value.match(email))
        {
            alert("Valid email address!");
            return true;
        }
    else
    {
        alert("Invalid email address!");
        return false;
    }
}
```

En el ejemplo anterior, cuando el usuario intenta enviar el formulario, se invoca la función personalizada &quot;ValidateEmail&quot; para comprobar si la dirección de correo electrónico introducida es válida.

## Usos de las funciones personalizadas {#uses-of-custom-function}

Las ventajas de utilizar funciones personalizadas en Forms adaptable son:

* **Manipulación de datos**: Las funciones personalizadas manipulan y procesan los datos introducidos en los campos de formulario.
* **Validación de datos**: las funciones personalizadas permiten realizar comprobaciones personalizadas en las entradas del formulario y proporcionar mensajes de error especificados.
* **Comportamiento dinámico**: las funciones personalizadas le permiten controlar el comportamiento dinámico de los formularios en función de condiciones específicas. Por ejemplo, puede mostrar u ocultar campos, modificar valores de campos o ajustar la lógica del formulario de forma dinámica.
* **Integración**: Puede utilizar funciones personalizadas para integrarse con API o servicios externos. Ayuda a recuperar datos de fuentes externas, enviar datos a extremos REST externos o realizar acciones personalizadas basadas en eventos externos.

## Anotaciones JS admitidas

Asegúrese de que la función personalizada que escriba esté acompañada de la variable `jsdoc` encima, en caso de que necesite configuración y descripción personalizadas. Existen varias formas de declarar una función en `JavaScript,` Los comentarios y permiten realizar un seguimiento de las funciones. Para obtener más información, consulte [usejsdoc.org](https://jsdoc.app/).

Etiquetas `jsdoc` compatibles:

* **Sintaxis**
privada: `@private`
una función privada no se incluye como función personalizada.

* **Sintaxis**
de nombre: `@name funcName <Function Name>`
O bien, `,` puede usar: `@function funcName <Function Name>` **o** `@func` `funcName <Function Name>`.
  `funcName` es el nombre de la función (no se permiten espacios).
  `<Function Name>` es el nombre para mostrar de la función.

* **Sintaxis**
de abonado: `@memberof namespace`
adjunta un área de nombres a la función.

* **Sintaxis**
de parámetro: `@param {type} name <Parameter Description>`
O bien, puede usar: `@argument` `{type} name <Parameter Description>` **o** `@arg` `{type}` `name <Parameter Description>`.
Muestra los parámetros utilizados por la función. Una función puede tener varias etiquetas de parámetro, una etiqueta para cada parámetro en el orden de ocurrencia.
  `{type}` representa el tipo de parámetro. Los tipos de parámetros permitidos son:

   1. cadena
   2. número
   3. booleano
   4. ámbito

  El ámbito se utiliza para hacer referencia a los campos de un formulario adaptable. Cuando un formulario utiliza la carga diferida, puede utilizar `scope` para acceder a sus campos. Puede acceder a los campos cuando se cargan o si están marcados como globales.

  Todos los demás tipos de parámetro se clasifican en una de las categorías anteriores. Ninguno no es compatible. Asegúrese de seleccionar uno de los tipos anteriores. Los tipos no distinguen entre mayúsculas y minúsculas. No se permiten espacios en el parámetro `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **Sintaxis**
de tipo de retorno: `@return {type}`
O bien, puede usar `@returns {type}`.
Agrega información sobre la función, como su objetivo. 
{type} representa el tipo de valor devuelto de la función. Los tipos de valor devuelto permitidos son:

   1. cadena
   1. número
   1. booleano

  Todos los demás tipos de valor devuelto se clasifican en una de las categorías anteriores. Ninguno no es compatible. Asegúrese de seleccionar uno de los tipos anteriores. Los tipos de devolución no distinguen entre mayúsculas y minúsculas.

* **Esta**
sintaxis: `@this currentComponent`

  Utilice @this para hacer referencia al componente de formulario adaptable en el que se escribe la regla.

  El siguiente ejemplo se basa en el valor de campo. En el ejemplo siguiente, la regla oculta un campo del formulario. La porción `this` de `this.value` hace referencia al componente de formulario adaptable subyacente, en el que se escribe la regla.

  ```
     /**
     * @function myTestFunction
     * @this currentComponent
     * @param {scope} scope in which code inside function will be executed.
     */
     myTestFunction = function (scope) {
        if(this.value == "O"){
              scope.age.visible = true;
        } else {
           scope.age.visible = false;
        }
     }
  ```

  >[!NOTE]
  >
  >Los comentarios antes de la función personalizada se utilizan como resumen. El resumen puede extenderse a varias líneas hasta que se encuentre una etiqueta. Limite el tamaño a un único para ver una descripción concisa en el generador de reglas.

## Tipos admitidos para la declaración de funciones {#function-declaration-supported-types}

**Instrucción de función**

```javascript
function area(len) {
    return len*len;
}
```

Esta función se incluye sin comentarios `jsdoc`.

**Expresión de función**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Instrucción y expresión de función**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Declaración de función como variable**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limitación: la función personalizada selecciona solo la primera declaración de función de la lista de variables, si están juntas. Puede utilizar la expresión de función para cada función declarada.

**Declaración de función como objeto**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```

## Crear función personalizada {#create-custom-function}

Para crear una función personalizada, realice los siguientes pasos:

1. Iniciar sesión en `http://server:port/crx/de/index.jsp#`.
1. Cree una carpeta dentro de la carpeta `/apps`. Por ejemplo, cree una carpeta denominada como `experience-league`.
1. Guarde los cambios.
1. Vaya a la carpeta creada y cree un nodo de tipo `cq:ClientLibraryFolder` as `clientlibs`.
1. Vaya al recién creado `clientlibs` y añada la `allowProxy` y `categories` propiedades:

   ![Propiedades del nodo de biblioteca personalizado](/help/forms/using/assets/customlibrary-catproperties.png)

   >[!NOTE]
   >
   > Puede proporcionar cualquier nombre en lugar de `customfunctionsdemo`.

1. Guarde los cambios.

1. Cree una carpeta llamada `js` en el `clientlibs` carpeta.
1. Cree un archivo JavaScript llamado `functions.js` en el `js` carpeta
1. Cree un archivo llamado `js.txt` en el `clientlibs` carpeta.
1. Guarde los cambios.
La estructura de carpetas creada tiene este aspecto:

   ![Estructura de carpetas de la biblioteca de cliente creada](/help/forms/using/assets/clientlibrary_folderstructure.png)
1. Haga doble clic en `functions.js` para abrir el editor. El archivo contiene el código de la función personalizada.
Añadamos el siguiente código al archivo JavaScript para calcular la edad en función de la fecha de nacimiento (AAAA-MM-DD).

   ```javascript
       /**
            * Calculates Age
            * @name calculateAge 
            * @return {string} 
       */
   
       function calculateAge(dateOfBirthString) {
       var dob = new Date(dateOfBirthString);
       var now = new Date();
   
       var age = now.getFullYear() - dob.getFullYear();
       var monthDiff = now.getMonth() - dob.getMonth();
   
       if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
       age--;
       }
   
       return age;
       }
   ```

1. Guardar `function.js`.
1. Vaya a `js.txt` y agregue el siguiente código:

   ```javascript
       #base=js
       functions.js
   ```

1. Guarde el archivo `js.txt`.

Puede hacer referencia a lo siguiente [función personalizada](/help/forms/using/assets/customfunction.zip) carpeta. AEM Descargue e instale esta carpeta en su instancia de.

Ahora puede utilizar la función personalizada en el formulario adaptable agregando la biblioteca de cliente.

## Agregar una biblioteca de cliente en un formulario adaptable{#use-custom-function}

Una vez que haya implementado la biblioteca de cliente en el entorno de Forms CS, utilice sus funcionalidades en el formulario adaptable. Para agregar la biblioteca de cliente en el formulario adaptable

1. Abra el formulario en modo de edición. Para abrir un formulario en modo de edición, seleccione un formulario y seleccione **[!UICONTROL Editar]**.
1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía. Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Abra el **[!UICONTROL Básico]** y seleccione el nombre de la **[!UICONTROL categoría de biblioteca de cliente]** en la lista desplegable (en este caso, seleccione `customfunctionscategory`).

   ![Agregar la biblioteca de cliente de funciones personalizada](/help/forms/using//assets/custom-function-category-name-core-component.png)

1. Clic **[!UICONTROL Listo]** .

Ahora puede crear una regla para utilizar funciones personalizadas en el editor de reglas:

![Agregar la biblioteca de cliente de funciones personalizada](/help/forms/using//assets/calculateage-customfunction.png)

Ahora, vamos a comprender cómo configurar y utilizar una función personalizada mediante [Servicio Invocar del editor de reglas en AEM Forms](/help//forms/using/rule-editor.md).
