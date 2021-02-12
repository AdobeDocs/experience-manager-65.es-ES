---
title: ¿Cómo crear un Forms adaptable mediante el Esquema JSON?
description: Aprenda a crear formularios adaptables con el esquema JSON como modelo de formulario. Puede utilizar esquemas JSON existentes para crear formularios adaptables. Profundice con una muestra de un esquema JSON, preconfigure los campos en la definición de esquema JSON, limite los valores aceptables para un componente de formulario adaptable y aprenda construcciones no compatibles.
feature: Adaptive Forms
role: Business Practitioner, Developers
level: Beginner, Imtermediate
translation-type: tm+mt
source-git-commit: 37ab98c9c78af452887c32101287b6d7f18d9d91
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 6%

---


# Creación de formularios adaptables mediante el Esquema JSON {#creating-adaptive-forms-using-json-schema}

## Requisitos previos {#prerequisites}

La creación de un formulario adaptable con un Esquema JSON como modelo de formulario requiere una comprensión básica del Esquema JSON. Se recomienda leer el siguiente contenido antes de este artículo.

* [Creación de un formulario adaptable](creating-adaptive-form.md)
* [Esquema JSON](https://json-schema.org/)

## Uso de un Esquema JSON como modelo de formulario {#using-a-json-schema-as-form-model}

[!DNL Adobe Experience Manager Forms] admite la creación de un formulario adaptable utilizando un Esquema JSON existente como modelo de formulario. Este Esquema JSON representa la estructura en la que el sistema back-end de su organización produce o consume datos. El Esquema JSON que utilice debe cumplir con [especificaciones v4](https://json-schema.org/draft-04/schema).

Las características clave del uso de un Esquema JSON son:

* La estructura del JSON se muestra como un árbol en la ficha Buscador de contenido en el modo de creación de un formulario adaptable. Puede arrastrar y agregar elementos de la jerarquía JSON al formulario adaptable.
* Puede rellenar previamente el formulario con JSON compatible con el esquema asociado.
* Al enviarlos, los datos introducidos por el usuario se envían como JSON que coinciden con el esquema asociado.

Un Esquema JSON consta de tipos de elementos simples y complejos. Los elementos tienen atributos que agregan reglas al elemento. Cuando estos elementos y atributos se arrastran a un formulario adaptable, se asignan automáticamente al componente de formulario adaptable correspondiente.

Esta asignación de elementos JSON con componentes de formulario adaptables es la siguiente:

```json
"birthDate": {
              "type": "string",
              "format": "date",
              "pattern": "date{DD MMMM, YYYY}",
              "aem:affKeyword": [
                "DOB",
                "Date of Birth"
              ],
              "description": "Date of birth in DD MMMM, YYYY",
              "aem:afProperties": {
                "displayPictureClause": "date{DD MMMM, YYYY}",
                "displayPatternType": "date{DD MMMM, YYYY}",
                "validationPatternType": "date{DD MMMM, YYYY}",
                "validatePictureClause": "date{DD MMMM, YYYY}",
                "validatePictureClauseMessage": "Date must be in DD MMMM, YYYY format."
              }
```

<table>
 <tbody>
  <tr>
   <th><strong>Elemento, propiedades o atributos JSON</strong></th>
   <th><strong>Componente de formulario adaptable</strong></th>
  </tr>
  <tr>
   <td><p>Propiedades de cadena con restricción enum y enumNames.</p> <p>Sintaxis,</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>Componente desplegable:</p>
    <ul>
     <li>Los valores enumerados en enumNames se muestran en el cuadro desplegable.</li>
     <li>Los valores enumerados en la enumeración se utilizan para el cálculo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Propiedad de cadena con restricción de formato. Por ejemplo, correo electrónico y fecha.</p> <p>Sintaxis,</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>El componente Correo electrónico se asigna cuando el tipo es cadena y el formato es correo electrónico.</li>
     <li>El componente de cuadro de texto con validación se asigna cuando el tipo es cadena y el formato es nombre de host.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>}</code></p> </td>
   <td><br /> <br /> Campo de texto<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>number, propiedad<br /> </td>
   <td>Campo numérico con subtipo definido como flotante<br /> </td>
  </tr>
  <tr>
   <td>integer, propiedad<br /> </td>
   <td>Campo numérico con subtipo definido como entero<br /> </td>
  </tr>
  <tr>
   <td>propiedad booleana<br /> </td>
   <td>Cambiar<br /> </td>
  </tr>
  <tr>
   <td>propiedad object<br /> </td>
   <td>Panel<br /> </td>
  </tr>
  <tr>
   <td>array, propiedad</td>
   <td>Panel repetible con mínimo y máximo igual a minItems y maxItems respectivamente. Solo se admiten matrices homogéneas. Por lo tanto, la restricción items debe ser un objeto y no una matriz.<br /> </td>
  </tr>
 </tbody>
</table>

### Propiedades de esquema comunes {#common-schema-properties}

El formulario adaptable utiliza la información disponible en el Esquema JSON para asignar cada campo generado. En particular:

* La propiedad `title` sirve como etiqueta para los componentes del formulario adaptable.
* La propiedad `description` se establece como descripción larga para un componente de formulario adaptable.
* La propiedad `default` sirve como valor inicial de un campo de formulario adaptable.
* La propiedad `maxLength` se establece como atributo `maxlength` del componente de campo de texto.
* Las propiedades `minimum`, `maximum`, `exclusiveMinimum` y `exclusiveMaximum` se utilizan para el componente de cuadro numérico.
* Para admitir el intervalo para `DatePicker component` propiedades de Esquema JSON adicionales `minDate` y `maxDate` se proporcionan.
* Las propiedades `minItems` y `maxItems` se utilizan para restringir el número de elementos/campos que se pueden agregar o quitar de un componente de panel.
* La propiedad `readOnly` establece el atributo `readonly` de un componente de formulario adaptable.
* La propiedad `required` marca el campo de formulario adaptable como obligatorio, mientras que en panel (donde type es object), los datos JSON enviados por última vez tienen campos con un valor vacío correspondiente a ese objeto.
* La propiedad `pattern` se establece como patrón de validación (expresión regular) en formato adaptable.
* La extensión del archivo Esquema JSON debe conservarse como .esquema.json. Por ejemplo, &lt;filename>.esquema.json.

## Esquema JSON de muestra {#sample-json-schema}

Este es un ejemplo de un Esquema JSON.

```json
{
 "$schema": "https://json-schema.org/draft-04/schema#",
 "definitions": {
  "employee": {
   "type": "object",
   "properties": {
    "userName": {
     "type": "string"
    },
    "dateOfBirth": {
     "type": "string",
     "format": "date"
    },
    "email": {
     "type": "string",
     "format": "email"
    },
    "language": {
     "type": "string"
    },
    "personalDetails": {
     "$ref": "#/definitions/personalDetails"
    },
    "projectDetails": {
     "$ref": "#/definitions/projectDetails"
    }
   },
   "required": [
    "userName",
    "dateOfBirth",
    "language"
   ]
  },
  "personalDetails": {
   "type": "object",
   "properties": {
    "GeneralDetails": {
     "$ref": "#/definitions/GeneralDetails"
    },
    "Family": {
     "$ref": "#/definitions/Family"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "projectDetails": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projects": {
      "$ref": "#/definitions/projects"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projects": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projectsAdditional": {
      "$ref": "#/definitions/projectsAdditional"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projectsAdditional": {
   "type": "array",
   "items": {
    "properties": {
     "Additional_name": {
      "type": "string"
     },
     "Additional_areacode": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "GeneralDetails": {
   "type": "object",
   "properties": {
    "age": {
     "type": "number"
    },
    "married": {
     "type": "boolean"
    },
    "phone": {
     "type": "number",
     "aem:afProperties": {
      "sling:resourceType": "/libs/fd/af/components/guidetelephone",
      "guideNodeClass": "guideTelephone"
     }
    },
    "address": {
     "type": "string"
    }
   }
  },
  "Family": {
   "type": "object",
   "properties": {
    "spouse": {
     "$ref": "#/definitions/spouse"
    },
    "kids": {
     "$ref": "#/definitions/kids"
    }
   }
  },
  "Income": {
   "type": "object",
   "properties": {
    "monthly": {
     "type": "number"
    },
    "yearly": {
     "type": "number"
    }
   }
  },
  "spouse": {
   "type": "object",
   "properties": {
    "name": {
     "type": "string"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "kids": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  }
 },
 "type": "object",
 "properties": {
  "employee": {
   "$ref": "#/definitions/employee"
  }
 }
}
```

### Definiciones de esquema reutilizables {#reusable-schema-definitions}

Las claves de definición se utilizan para identificar esquemas reutilizables. Las definiciones de esquema reutilizables se utilizan para crear fragmentos. Es similar a identificar tipos complejos en XSD. A continuación se muestra un Esquema JSON de muestra con definiciones:

```json
{
  "$schema": "https://json-schema.org/draft-04/schema#",

  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street_address": { "type": "string" },
        "city":           { "type": "string" },
        "state":          { "type": "string" }
      },
      "required": ["street_address", "city", "state"]
    }
  },

  "type": "object",

  "properties": {
    "billing_address": { "$ref": "#/definitions/address" },
    "shipping_address": { "$ref": "#/definitions/address" }
  }
}
```

El ejemplo anterior define un registro de cliente, donde cada cliente tiene una dirección de envío y una dirección de facturación. La estructura de ambas direcciones es la misma: las direcciones tienen una dirección, ciudad y estado— así que es una buena idea no duplicado las direcciones. También facilita la adición y eliminación de campos para cualquier cambio futuro.

## Preconfiguración de campos en Definición de Esquema JSON {#pre-configuring-fields-in-json-schema-definition}

Puede utilizar la propiedad **aem:afProperties** para preconfigurar el campo de Esquema JSON para asignarlo a un componente de formulario adaptable personalizado. A continuación se muestra un ejemplo:

```json
{
    "properties": {
        "sizeInMB": {
            "type": "integer",
            "minimum": 16,
            "maximum": 512,
            "aem:afProperties" : {
                 "sling:resourceType" : "/apps/fd/af/components/guideTextBox",
                 "guideNodeClass" : "guideTextBox"
             }
        }
    },
    "required": [ "sizeInMB" ],
    "additionalProperties": false
}
```

## Configurar secuencias de comandos o expresiones para objetos de formulario {#configure-scripts-or-expressions-for-form-objects}

JavaScript es el lenguaje de expresión de los formularios adaptables. Todas las expresiones son expresiones JavaScript válidas y utilizan API de modelos de secuencias de comandos de formularios adaptables. Puede preconfigurar objetos de formulario para [evaluar una expresión](adaptive-form-expressions.md) en un evento de formulario.

Utilice la propiedad aem:afproperties para preconfigurar expresiones de formularios adaptables o secuencias de comandos para componentes de formularios adaptables. Por ejemplo, cuando se activa el evento initialize, el código siguiente establece el valor del campo telefónico e imprime un valor en el registro:

```json
"telephone": {
  "type": "string",
  "pattern": "/\\d{10}/",
  "aem:affKeyword": ["phone", "telephone","mobile phone", "work phone", "home phone", "telephone number", "telephone no", "phone number"],
  "description": "Telephone Number",
  "aem:afProperties" : {
    "sling:resourceType" : "fd/af/components/guidetelephone",
    "guideNodeClass" : "guideTelephone",
    "events": {
      "Initialize" : "this.value = \"1234567890\"; console.log(\"ef:gh\") "
    }
  }
}
```

Debe ser miembro del grupo [form-power-user](forms-groups-privileges-tasks.md) para configurar secuencias de comandos o expresiones para objetos de formulario. La tabla siguiente lista todos los eventos de secuencia de comandos admitidos para un componente de formulario adaptable.

<table>
 <tbody>
  <tr>
   <th><strong></strong>Componente \ Evento</th>
   <th>initialize <br /> </th>
   <td>Calcular</td>
   <td>Visibilidad</td>
   <td>Validar</td>
   <td>Activado</td>
   <td>Implementación de valor</td>
   <td>Haga clic </td>
   <td>Opciones</td>
  </tr>
  <tr>
   <td>Campo de texto</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Campo numérico</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Stepper numérico</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Botón de opción</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Teléfono</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Cambiar</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Botón</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>Casilla de verificación</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Lista desplegable</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Opción de imagen</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Campo de introducción de fecha</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Selector de fecha</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Correo electrónico</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Archivo adjunto</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Imagen</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Draw</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Panel</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

Algunos ejemplos de uso de eventos en un JSON están ocultando un campo en el evento de inicialización y configurando el valor de otro campo en el evento de confirmación de valor. Para obtener información detallada sobre la creación de expresiones para los eventos de secuencias de comandos, consulte [Expresiones de formularios adaptables](adaptive-form-expressions.md).

Este es el código JSON de muestra para los ejemplos mencionados anteriormente.

### Ocultar un campo en el evento de inicialización {#hiding-a-field-on-initialize-event}

```json
"name": {
    "type": "string",
    "aem:afProperties": {
        "events" : {
            "Initialize" : "this.visible = false;"
        }
    }
}
```

#### Configurar el valor de otro campo en el evento de confirmación de valor {#configure-value-of-another-field-on-value-commit-event}

```json
"Income": {
    "type": "object",
    "properties": {
        "monthly": {
            "type": "number",
            "aem:afProperties": {
                "events" : {
                    "Value Commit" : "IncomeYearly.value = this.value * 12;"
                }
            }
        },
        "yearly": {
            "type": "number",
            "aem:afProperties": {
                "name": "IncomeYearly"
            }
        }
    }
}
```

## Límite de valores aceptables para un componente de formulario adaptable {#limit-acceptable-values-for-an-adaptive-form-component}

Puede agregar las siguientes restricciones a los elementos de Esquema JSON para limitar los valores aceptables para un componente de formulario adaptable:

<table>
 <tbody>
  <tr>
   <td><p><strong> Esquema, propiedad</strong></p> </td>
   <td><p><strong>Tipo de datos</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
   <td><p><strong>Componente</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>Cadena</p> </td>
   <td><p>Especifica el límite superior de los valores numéricos y las fechas. De forma predeterminada, se incluye el valor máximo.</p> </td>
   <td>
    <ul>
     <li>Cuadro numérico</li>
     <li>Stepper numérico<br /> </li>
     <li>Selector de fecha</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>Cadena</p> </td>
   <td><p>Especifica el límite inferior de los valores numéricos y las fechas. De forma predeterminada, se incluye el valor mínimo.</p> </td>
   <td>
    <ul>
     <li>Cuadro numérico</li>
     <li>Stepper numérico</li>
     <li>Selector de fecha</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Si es true, el valor numérico o la fecha especificados en el componente del formulario deben ser menores que el valor numérico o la fecha especificados para la propiedad máxima.</p> <p>Si es false, el valor numérico o la fecha especificados en el componente del formulario debe ser menor o igual que el valor numérico o la fecha especificados para la propiedad máxima.</p> </td>
   <td>
    <ul>
     <li>Cuadro numérico</li>
     <li>Stepper numérico</li>
     <li>Selector de fecha</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Si es true, el valor numérico o la fecha especificados en el componente del formulario deben ser buenos que el valor numérico o la fecha especificados para la propiedad mínima.</p> <p>Si es false, el valor numérico o la fecha especificados en el componente del formulario deben ser buenos o iguales al valor numérico o la fecha especificados para la propiedad mínima.</p> </td>
   <td>
    <ul>
     <li>Cuadro numérico</li>
     <li>Stepper numérico</li>
     <li>Selector de fecha</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>Cadena</p> </td>
   <td><p>Especifica el número mínimo de caracteres permitidos en un componente. La longitud mínima debe ser igual o buena a cero.</p> </td>
   <td>
    <ul>
     <li>Cuadro de texto</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxLength</code></td>
   <td>Cadena</td>
   <td>Especifica el número máximo de caracteres permitidos en un componente. La longitud máxima debe ser igual o buena a cero.</td>
   <td>
    <ul>
     <li>Cuadro de texto</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>Cadena</p> </td>
   <td><p>Especifica la secuencia de los caracteres. Un componente acepta los caracteres si éstos se ajustan al patrón especificado.</p> <p>La propiedad pattern se asigna al patrón de validación del componente de formulario adaptable correspondiente.</p> </td>
   <td>
    <ul>
     <li>Todos los componentes de formularios adaptables asignados a un esquema XSD </li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxItems</code></td>
   <td>Cadena</td>
   <td>Especifica el número máximo de elementos de una matriz. Los elementos máximos deben ser iguales o buenos a cero.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>minItems</code></td>
   <td>Cadena</td>
   <td>Especifica el número mínimo de elementos de una matriz. Los elementos mínimos deben ser iguales o buenos a cero.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Construcciones no admitidas {#non-supported-constructs}

Los formularios adaptables no admiten las siguientes construcciones de Esquema JSON:

* Tipo nulo
* tipos de unión como cualquiera, y
* OneOf, AnyOf, AllOf y NOT
* Solo se admiten matrices homogéneas. Por lo tanto, la restricción items debe ser un objeto y no una matriz.

## Preguntas frecuentes {#frequently-asked-questions}

**¿Por qué no se pueden arrastrar elementos individuales de un subformulario (estructura generada a partir de cualquier tipo complejo) para subformularios repetibles (los valores minOccours o maxoccur son buenos a partir de 1)?**

En un subformulario repetible, debe utilizar el subformulario completo. Si solo desea campos selectivos, utilice toda la estructura y elimine los no deseados.

**Tengo una estructura larga y compleja en Content Finder. ¿Cómo puedo encontrar un elemento específico?**

Tiene dos opciones:

* Desplácese por la estructura de árbol
* Utilice el cuadro Buscar para encontrar un elemento

**¿Cuál debería ser la extensión del archivo esquema JSON?**

La extensión del archivo Esquema JSON debe ser .esquema.json. Por ejemplo, &lt;filename>.esquema.json.
