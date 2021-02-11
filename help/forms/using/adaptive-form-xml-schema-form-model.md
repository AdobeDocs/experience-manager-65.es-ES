---
title: ¿Cómo crear un Forms adaptable mediante el Esquema XML?
description: Aprenda a utilizar el esquema XML como modelo de formulario en un formulario adaptable. Puede aplicar plantillas XSD existentes para crear formularios adaptables y arrastrar y soltar elementos de esquema desde XSD en el formulario adaptable. Profundice con un ejemplo de esquema XML, agregue propiedades especiales a los campos mediante el esquema XML y limite los valores aceptables para un componente de formulario adaptable.
feature: Adaptive Forms
role: Business Practitioner, Developers
level: Beginner, Imtermediate
translation-type: tm+mt
source-git-commit: ec8a4c3941b5434f10ad0727be02fcf296cd4da7
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 5%

---


# Creación de formularios adaptables mediante el Esquema XML {#creating-adaptive-forms-using-xml-schema}

## Requisitos previos {#prerequisites}

La creación de un formulario adaptable con un esquema XML como modelo de formulario requiere una comprensión básica de los esquemas XML. Además, se recomienda leer el siguiente contenido antes de este artículo.

* [Creación de un formulario adaptable](creating-adaptive-form.md)
* [ESQUEMA XML](https://www.w3.org/TR/xmlschema-2/)

## Uso de un esquema XML como modelo de formulario {#using-an-xml-schema-as-form-model}

[!DNL Experience Manager Forms] admite la creación de un formulario adaptable utilizando un esquema XML existente como modelo de formulario. Este esquema XML representa la estructura en la que el sistema back-end de la organización produce o consume datos.

Las características clave del uso de un esquema XML son:

* La estructura del XSD se muestra como un árbol en la ficha Buscador de contenido en el modo de creación de un formulario adaptable. Puede arrastrar y agregar elementos de la jerarquía XSD al formulario adaptable.
* Puede rellenar previamente el formulario utilizando XML que sea compatible con el esquema asociado.
* Al enviar, los datos introducidos por el usuario se envían como XML que se alinea con el esquema asociado.

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

## Esquema XML de muestra {#sample-xml-schema}

Este es un ejemplo de un esquema XML.

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
>Asegúrese de que el esquema XML solo tenga un elemento raíz. No se admite un esquema XML con más de un elemento raíz.

## Añadir propiedades especiales a campos mediante el esquema XML {#adding-special-properties-to-fields-using-xml-schema}

Puede agregar los atributos siguientes a los elementos de Esquema XML para agregar propiedades especiales a los campos del formulario adaptable asociado.

<table>
 <tbody>
  <tr>
   <th><strong>Esquema, propiedad</strong></th>
   <th><strong>Uso en formularios adaptables</strong></th>
   <th><strong>Compatible con </strong></th>
  </tr>
  <tr>
   <td><code>use=required </code></td>
   <td>Marca un campo obligatorio<br /> </td>
   <td>Atributo</td>
  </tr>
  <tr>
   <td><code>default="default value"</code></td>
   <td>Añade un valor predeterminado</td>
   <td>Elemento y atributo</td>
  </tr>
  <tr>
   <td><code>minOccurs="3"</code></td>
   <td><p>Especifica las incidencias mínimas</p> <p>(Para subformularios repetibles (tipos complejos))</p> </td>
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
>* Inserción de espacio en blanco en los límites de mayúsculas y minúsculas.

>
>
Por ejemplo, si agrega el elemento de esquema `userFirstName`, el rótulo generado en el formulario adaptable será `User First Name`.

## Límite de valores aceptables para un componente de formulario adaptable {#limit-acceptable-values-for-an-adaptive-form-component}

Puede agregar las siguientes restricciones a los elementos de esquema XML para limitar los valores aceptables para un componente de formulario adaptable:

<table>
 <tbody>
  <tr>
   <td><p><strong> Esquema, propiedad</strong></p> </td>
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
   <td><p>Especifica el número exacto de caracteres permitidos en un componente. La longitud debe ser igual o buena a cero.</p> </td>
   <td>
    <ul>
     <li>Cuadro de texto</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>fractionDigits</code></p> </td>
   <td><p>Cadena</p> </td>
   <td><p>Especifica el número máximo de decimales permitido en un componente. La fracciónDigits debe ser igual o buena a cero.</p> </td>
   <td>
    <ul>
     <li> Cuadro numérico con tipo de datos flotante o decimal</li>
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
 </tbody>
</table>

## Preguntas frecuentes {#frequently-asked-questions}

**¿Cómo sé qué elemento del árbol está asociado con qué elemento XML?**

Al hacer clic con el botón doble en un elemento del Buscador de contenido, una ventana emergente muestra un nombre de campo y una propiedad llamada `bindRef`. Esta propiedad asigna el elemento de árbol al elemento o atributo del esquema.

![Campo bindref de un elemento de esquema XML](assets/dblclick.png)

El campo bindRef</code> muestra la asociación entre un elemento de árbol y un elemento o atributo de un esquema.

>[!NOTE]
>
>Los atributos tienen un símbolo `@` en su valor `bindRef`para distinguirlos de los elementos. Por ejemplo, `/config/projectDetails/@duration`.

**¿Por qué no se pueden arrastrar elementos individuales de un subformulario (estructura generada a partir de cualquier tipo complejo) para subformularios repetibles (los valores minOccours o maxoccur son buenos a partir de 1)?**

En un subformulario repetible, debe utilizar el subformulario Completar. Si solo desea campos selectivos, utilice toda la estructura y elimine los no deseados.

**Tengo una estructura larga y compleja en Content Finder. ¿Cómo puedo encontrar un elemento específico?**

Tiene dos opciones:

* Desplácese por la estructura de árbol
* Utilice el cuadro Buscar para encontrar un elemento

**¿Qué es bindRef?**

Un `bindRef` es la conexión entre un componente de formulario adaptable y un elemento o atributo de esquema. Indica el `XPath` donde el valor capturado de este componente o campo está disponible en el XML de salida. También se utiliza un `bindRef`cuando se rellena previamente un valor de campo a partir de un XML prerelleno (prerellenado).
