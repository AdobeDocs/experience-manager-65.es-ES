---
title: ¿Cómo se crea Forms adaptable utilizando el esquema XML?
description: Aprenda a utilizar el esquema XML como modelo de formulario en un formulario adaptable. Puede aplicar plantillas XSD existentes para crear formularios adaptables y arrastrar y soltar elementos de esquema de XSD en el formulario adaptable. Profundizar con una muestra de un esquema XML, añadir propiedades especiales a los campos utilizando el esquema XML y limitar los valores aceptables para un componente de formulario adaptable.
feature: Formularios adaptables
role: Business Practitioner, Developer
level: Beginner, Intermediate
exl-id: 35d5859f-54c4-4d14-9c64-0d9291ef9029
translation-type: tm+mt
source-git-commit: ad67634278088f8f953fde61a3543acdd70537dd
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 6%

---

# Creación de formularios adaptables mediante el esquema XML {#creating-adaptive-forms-using-xml-schema}

## Requisitos previos {#prerequisites}

La creación de un formulario adaptable utilizando un esquema XML como modelo de formulario requiere una comprensión básica de los esquemas XML. Además, se recomienda leer el siguiente contenido antes de este artículo.

* [Creación de un formulario adaptable](creating-adaptive-form.md)
* [Esquema XML](https://www.w3.org/TR/xmlschema-2/)

## Uso de un esquema XML como modelo de formulario {#using-an-xml-schema-as-form-model}

[!DNL Experience Manager Forms] admite la creación de un formulario adaptable utilizando un esquema XML existente como modelo de formulario. Este esquema XML representa la estructura en la que el sistema back-end de su organización produce o consume datos.

Las características clave del uso de un esquema XML son:

* La estructura del XSD se muestra como un árbol en la pestaña Buscador de contenido en el modo de creación de un formulario adaptable. Puede arrastrar y agregar un elemento de la jerarquía XSD al formulario adaptable.
* Puede rellenar previamente el formulario utilizando XML que cumpla con el esquema asociado.
* Al realizar el envío, los datos introducidos por el usuario se envían como XML que se ajusta al esquema asociado.

Un esquema XML consta de tipos de elementos simples y complejos. Los elementos tienen atributos que agregan reglas al elemento. Cuando estos elementos y atributos se arrastran a un formulario adaptable, se asignan automáticamente al componente de formulario adaptable correspondiente.

Esta asignación de elementos XML con componentes de formulario adaptables es la siguiente:

<table>
 <tbody>
  <tr>
   <th><strong>Elemento o atributo XML </strong></th>
   <th><strong>Componente de formulario adaptable</strong></th>
  </tr>
  <tr>
   <td><code>xs:string</code></td>
   <td>Cuadro de texto</td>
  </tr>
  <tr>
   <td><code>xs:boolean</code></td>
   <td>Casilla de verificación</td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><code>xs:unsignedInt</code></li>
     <li><code>xs:xs:int</code></li>
     <li><code class="code">xs:decimal
        </code></li>
     <li>Todos los tipos de valores numéricos</li>
    </ul> </td>
   <td>Cuadro numérico</td>
  </tr>
  <tr>
   <td><code>xs:date</code></td>
   <td>Selector de fecha</td>
  </tr>
  <tr>
   <td><code class="code">xs:enumeration
      </code></td>
   <td>Desplegable</td>
  </tr>
  <tr>
   <td>Cualquier elemento de tipo complejo</td>
   <td>Panel</td>
  </tr>
 </tbody>
</table>

## Esquema XML de ejemplo {#sample-xml-schema}

Este es un ejemplo de esquema XML.

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartBirth" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```

>[!NOTE]
>
>Asegúrese de que el esquema XML tenga solo un elemento raíz. No se admite un esquema XML con más de un elemento raíz.

## Adición de propiedades especiales a campos mediante el esquema XML {#adding-special-properties-to-fields-using-xml-schema}

Puede añadir los siguientes atributos a los elementos del esquema XML para añadir propiedades especiales a los campos del formulario adaptable asociado.

<table>
 <tbody>
  <tr>
   <th><strong>Propiedad Schema</strong></th>
   <th><strong>Uso en forma adaptable</strong></th>
   <th><strong>Admitido en </strong></th>
  </tr>
  <tr>
   <td><code>use=required </code></td>
   <td>Marca un campo obligatorio<br /> </td>
   <td>Atributo</td>
  </tr>
  <tr>
   <td><code>default="default value"</code></td>
   <td>Agrega un valor predeterminado</td>
   <td>Elemento y atributo</td>
  </tr>
  <tr>
   <td><code>minOccurs="3"</code></td>
   <td><p>Especifica ocurrencias mínimas</p> <p>(Para subformularios repetibles (tipos complejos))</p> </td>
   <td>Elemento (tipo complejo)</td>
  </tr>
  <tr>
   <td><code class="code">maxOccurs="10"
      </code></td>
   <td><p>Especifica el número máximo de incidencias</p> <p>(Para subformularios repetibles (tipos complejos))</p> </td>
   <td>Elemento (tipo complejo)</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Al arrastrar un elemento de esquema a un formulario adaptable, se genera un rótulo predeterminado mediante:
>
>* Poner en mayúscula el primer carácter del nombre del elemento
>* Inserción de espacio en blanco en los límites del Camel Case.

>
>
Por ejemplo, si agrega el elemento de esquema `userFirstName` , el rótulo generado en el formulario adaptable es `User First Name`.

## Límite de valores aceptables para un componente de formulario adaptable {#limit-acceptable-values-for-an-adaptive-form-component}

Puede añadir las siguientes restricciones a los elementos de esquema XML para limitar los valores aceptables para un componente de formulario adaptable:

<table>
 <tbody>
  <tr>
   <td><p><strong> Propiedad Schema</strong></p> </td>
   <td><p><strong>Tipo de datos</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
   <td><p><strong>Componente</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>totalDigits</code></p> </td>
   <td><p>Cadena</p> </td>
   <td><p>Especifica el número máximo de dígitos permitidos en un componente. El número de dígitos especificado debe ser bueno a cero.</p> </td>
   <td>
    <ul>
     <li>Cuadro numérico</li>
     <li>Stepper numérico</li>
    </ul> </td>
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
   <td><p>Especifica el límite inferior de valores numéricos y fechas. De forma predeterminada, se incluye el valor mínimo.</p> </td>
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
   <td><p>Si es true, el valor numérico o la fecha especificados en el componente del formulario deben ser menores que el valor numérico o la fecha especificados para la propiedad máxima.</p> <p>Si es false, el valor numérico o la fecha especificados en el componente del formulario deben ser menores o iguales que el valor numérico o la fecha especificados para la propiedad maximum.</p> </td>
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
   <td><p>Si es true, el valor numérico o la fecha especificados en el componente del formulario deben ser buenos que el valor numérico o la fecha especificados para la propiedad Minimum.</p> <p>Si es false, el valor numérico o la fecha especificados en el componente del formulario deben ser buenos o iguales al valor numérico o la fecha especificados para la propiedad Minimum.</p> </td>
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
   <td><p>Especifica el número mínimo de caracteres permitidos en un componente. La longitud mínima debe ser igual o buena que cero.</p> </td>
   <td>
    <ul>
     <li>Cuadro de texto</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maxLength</code></p> </td>
   <td><p>Cadena</p> </td>
   <td><p>Especifica el número máximo de caracteres permitidos en un componente. La longitud máxima debe ser buena a cero.</p> </td>
   <td>
    <ul>
     <li>Cuadro de texto</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>length</code></p> </td>
   <td><p>Cadena</p> </td>
   <td><p>Especifica el número exacto de caracteres permitidos en un componente. La longitud debe ser igual o buena que cero.</p> </td>
   <td>
    <ul>
     <li>Cuadro de texto</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>fractionDigits</code></p> </td>
   <td><p>Cadena</p> </td>
   <td><p>Especifica el número máximo de decimales permitido en un componente. fractionDigits debe ser igual o bueno que cero.</p> </td>
   <td>
    <ul>
     <li> Cuadro numérico con tipo de datos flotante o decimal</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>Cadena</p> </td>
   <td><p>Especifica la secuencia de los caracteres. Un componente acepta los caracteres si se ajustan al patrón especificado.</p> <p>La propiedad pattern se asigna al patrón de validación del componente de formulario adaptable correspondiente.</p> </td>
   <td>
    <ul>
     <li>Todos los componentes de formularios adaptables asignados a un esquema XSD </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Preguntas frecuentes {#frequently-asked-questions}

**¿Cómo sé qué elemento del árbol está asociado con qué elemento XML?**

Al hacer doble clic en un elemento del Buscador de contenido, una ventana emergente muestra un nombre de campo y una propiedad denominada `bindRef`. Esta propiedad asigna el elemento de árbol al elemento o atributo del esquema.

![Campo bindref de un elemento de esquema XML](assets/dblclick.png)

El campo bindRef</code> muestra la asociación entre un elemento de árbol y un elemento o atributo de un esquema.

>[!NOTE]
>
>Los atributos tienen un símbolo `@` en su valor `bindRef`para distinguirlos de los elementos. Por ejemplo, `/config/projectDetails/@duration`.

**¿Por qué no puedo arrastrar elementos individuales de un subformulario (estructura generada a partir de cualquier tipo complejo) para subformularios repetibles (los valores minOccours o maxOccurs son buenos a 1)?**

En un subformulario repetible, debe utilizar el subformulario Complete . Si solo desea campos selectivos, utilice toda la estructura y elimine los no deseados.

**Tengo una estructura compleja y larga en el Buscador de Contenido. ¿Cómo puedo encontrar un elemento específico?**

Tiene dos opciones:

* Desplácese por la estructura de árbol
* Utilice el cuadro Buscar para buscar un elemento

**¿Qué es bindRef?**

Una `bindRef` es la conexión entre un componente de formulario adaptable y un elemento o atributo de esquema. Indica el `XPath` donde el valor capturado de este componente o campo está disponible en el XML de salida. También se utiliza un `bindRef`cuando se rellena previamente un valor de campo del XML prerellenado (prerellenado).
