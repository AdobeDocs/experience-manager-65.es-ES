---
title: Compatibilidad con XFA en formularios adaptables basados en XDP
seo-title: Compatibilidad con XFA en formularios adaptables basados en XDP
description: Las listas admiten eventos XFA, propiedades, secuencias de comandos y validación en formularios adaptables.
seo-description: Las listas admiten eventos XFA, propiedades, secuencias de comandos y validación en formularios adaptables.
uuid: 75d3c292-cfed-438f-afdb-4071d95a08b7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 05303b29-9058-4723-b134-4ba605fe40c7
docset: aem65
feature: Formularios adaptables
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 7%

---


# Compatibilidad con XFA en formularios adaptables basados en XDP{#xfa-support-in-xdp-based-adaptive-forms}

## Introducción {#introduction}

Los formularios adaptables son compatibles con varios eventos, propiedades, secuencias de comandos y validaciones XFA definidos en un archivo XDP, incluidos:

* Ejecución de secuencias de comandos definidas en los eventos del archivo XDP.
* Captura de los valores predeterminados y las propiedades de comportamiento para los campos del archivo XDP.
* Ejecución de secuencias de comandos de validación definidas en el archivo XDP.

Cuando se crea un formulario adaptable basado en un archivo XDP, las propiedades, los eventos y las validaciones se rellenan automáticamente en la IU de creación de formularios. Sin embargo, los autores de formularios pueden anular algunos de estos elementos para crear una experiencia alternativa.

Este artículo enumera los eventos XFA admitidos, las propiedades y las validaciones aceptadas en los formularios adaptables y explica cómo sustituirlos en los formularios adaptables.

## Elementos XFA compatibles y su asignación en formularios adaptables {#supported-xfa-elements-and-their-mapping-in-adaptive-forms-br}

### Fields {#fields}

Cuando se crea un formulario adaptable utilizando un archivo XDP, se puede arrastrar y soltar un campo XFA en el formulario adaptable. La tabla siguiente muestra cómo se asignan los campos XFA a los campos de formulario adaptables.

<table>
 <tbody>
  <tr>
   <td><p><strong>Campo o contenedor XFA</strong></p> </td>
   <td><p><strong>Componente de formulario adaptable correspondiente</strong></p> </td>
  </tr>
  <tr>
   <td><p>Botón </p> </td>
   <td><p>Botón</p> </td>
  </tr>
  <tr>
   <td><p>Casilla de verificación </p> </td>
   <td><p>Casilla de verificación</p> </td>
  </tr>
  <tr>
   <td><p>Cuadro de lista </p> </td>
   <td><p>Lista desplegable</p> </td>
  </tr>
  <tr>
   <td><p>Campo de fecha y hora </p> </td>
   <td><p>Selector de fecha</p> </td>
  </tr>
  <tr>
   <td><p>Scribble de firma</p> </td>
   <td><p>Firma a mano alzada</p> </td>
  </tr>
  <tr>
   <td><p>Campo numérico </p> </td>
   <td><p>Cuadro numérico</p> </td>
  </tr>
  <tr>
   <td><p>Campo decimal</p> </td>
   <td><p>Cuadro numérico</p> </td>
  </tr>
  <tr>
   <td><p>Campo de texto </p> </td>
   <td><p>Cuadro de texto</p> </td>
  </tr>
  <tr>
   <td><p>Campo de contraseña </p> </td>
   <td><p>Cuadro de contraseña</p> </td>
  </tr>
  <tr>
   <td><p>Imagen</p> </td>
   <td><p>Imagen</p> </td>
  </tr>
  <tr>
   <td><p>Texto</p> </td>
   <td><p>Texto</p> </td>
  </tr>
  <tr>
   <td><p>Subformulario </p> </td>
   <td><p>Panel</p> </td>
  </tr>
  <tr>
   <td><p>Área (grupo)</p> </td>
   <td><p>Panel</p> </td>
  </tr>
  <tr>
   <td><p>Conjunto de subformularios </p> </td>
   <td><p>Panel</p> </td>
  </tr>
 </tbody>
</table>

### Propiedades {#properties}

La siguiente tabla captura cómo se comportan los distintos scripts XFA definidos en los archivos XDP en los formularios adaptables.

<table>
 <tbody>
  <tr>
   <td><p><strong>Propiedades de componentes XFA</strong></p> </td>
   <td><p><strong>Comportamiento correspondiente en formularios adaptables</strong></p> </td>
  </tr>
  <tr>
   <td><p>somExpression </p> </td>
   <td><p>Asignado a la propiedad Bind reference (bindRef) en forma adaptativa.</p> </td>
  </tr>
  <tr>
   <td><p>presence </p> </td>
   <td><p>Asignado a la propiedad visible en forma adaptable. Puede anularlo utilizando la expresión Visibilidad .</p> </td>
  </tr>
  <tr>
   <td><p>access </p> </td>
   <td><p>Asignado a la propiedad enabled en forma adaptable. Puede anularlo utilizando la expresión Access .</p> </td>
  </tr>
  <tr>
   <td><p>Accesibilidad: función </p> </td>
   <td><p>Asignado a la propiedad role en forma adaptable.</p> </td>
  </tr>
  <tr>
   <td><p>Accesibilidad: speakPriority </p> </td>
   <td><p>Asignado a la propiedad speakPriority en forma adaptativa.</p> </td>
  </tr>
  <tr>
   <td><p>Accesibilidad: speakText</p> </td>
   <td><p>Asignado al texto de accesibilidad personalizado en forma adaptable.</p> </td>
  </tr>
  <tr>
   <td><p>Accesibilidad: toolTip </p> </td>
   <td><p>Asignado a la propiedad short description en forma adaptable.</p> </td>
  </tr>
  <tr>
   <td><p>caption<em> (todos los tipos de campo)</em></p> </td>
   <td><p>Asignado a la propiedad Título en forma adaptable.</p> </td>
  </tr>
  <tr>
   <td><p>displayFormat<em> (todos los tipos de campo)</em></p> </td>
   <td><p>Asignado al patrón de visualización en forma adaptable.</p> </td>
  </tr>
  <tr>
   <td><p>rawValue<em> (todos los tipos de campo)</em></p> </td>
   <td><p>Asignado a la propiedad value en el formulario adaptable.</p> </td>
  </tr>
  <tr>
   <td><p>items<em> (cuadro de lista, casilla de verificación)</em></p> </td>
   <td><p>Asignado a la propiedad options en forma adaptable. Puede anularlo utilizando la expresión Options .</p> </td>
  </tr>
  <tr>
   <td><p>maxChar<em> (Campo de texto)</em></p> </td>
   <td><p>Asignado a la propiedad Maximum character allowed en un formulario adaptable.</p> </td>
  </tr>
  <tr>
   <td><p>multilínea<em> (campo de texto)</em></p> </td>
   <td><p>Asignado a la propiedad Permitir líneas múltiples en forma adaptable.</p> </td>
  </tr>
  <tr>
   <td><p>fracDigit<em> (Campo numérico, Campo decimal)</em></p> </td>
   <td><p>Asignado a la propiedad Frac digit en forma adaptable.</p> </td>
  </tr>
  <tr>
   <td><p>leadDigit<em> (Campo numérico, Campo decimal)</em></p> </td>
   <td><p>Asignado a la propiedad Dígitos de posible cliente en forma adaptativa.</p> </td>
  </tr>
  <tr>
   <td><p>multiSelect<em> (cuadro de lista)</em></p> </td>
   <td><p>Asignado a la propiedad Permite selección múltiple en forma adaptable.</p> </td>
  </tr>
 </tbody>
</table>

### Secuencias de comandos {#scripts}

La siguiente tabla captura cómo se comportan los distintos scripts XFA definidos en el archivo XDP en formularios adaptables.

<table>
 <tbody>
  <tr>
   <td><p><strong>Eventos de script XFA</strong></p> </td>
   <td><p><strong>Comportamiento correspondiente en formularios adaptables</strong></p> </td>
  </tr>
  <tr>
   <td><p>initialize </p> </td>
   <td><p>Esta secuencia de comandos se ejecuta durante la ejecución y no se puede anular en forma adaptativa.</p> </td>
  </tr>
  <tr>
   <td><p>calculate</p> </td>
   <td><p>Asignado a la expresión Calculate en forma adaptable.</p> </td>
  </tr>
  <tr>
   <td><p>validate </p> </td>
   <td><p>Asignado a la expresión Validación en forma adaptable.</p> </td>
  </tr>
  <tr>
   <td><p>validationState </p> </td>
   <td><p>Esta secuencia de comandos se ejecuta en tiempo de ejecución y no se puede anular en forma adaptable.<br /> </p> </td>
  </tr>
  <tr>
   <td><p>exit </p> </td>
   <td><p>Esta secuencia de comandos se ejecuta durante la ejecución y no se puede anular en forma adaptativa.</p> </td>
  </tr>
  <tr>
   <td><p>click (campos de botón)</p> </td>
   <td><p>Asignado a la expresión Click del botón.</p> </td>
  </tr>
  <tr>
   <td><p>Compatibilidad con scripts del lado del servidor</p> </td>
   <td><p>Esta secuencia de comandos se ejecuta durante la ejecución y no se puede anular en forma adaptativa.</p> </td>
  </tr>
  <tr>
   <td><p>Compatibilidad con servicios web</p> </td>
   <td><p>Esta secuencia de comandos se ejecuta durante la ejecución y no se puede anular en forma adaptativa.</p> </td>
  </tr>
  <tr>
   <td><p>Cambio (campo de anotaciones, botón de opción, casilla de verificación)</p> </td>
   <td><p>Esta secuencia de comandos se ejecuta durante la ejecución y no se puede anular en forma adaptativa.</p> </td>
  </tr>
 </tbody>
</table>

### Validaciones {#validations}

La siguiente tabla captura cómo se asignan las validaciones XFA a las validaciones en formularios adaptables.

<table>
 <tbody>
  <tr>
   <td><p><strong>Validación XFA</strong></p> </td>
   <td><p><strong>Validación correspondiente en forma adaptable</strong></p> </td>
  </tr>
  <tr>
   <td><p>Patrón de validación (formatTest)</p> </td>
   <td><p>validatePictureClause</p> </td>
  </tr>
  <tr>
   <td><p>Mensaje del patrón de validación (formatTestMessage)</p> </td>
   <td><p>validatePictureMessage</p> </td>
  </tr>
  <tr>
   <td><p>Requerido (nullTest )</p> </td>
   <td><p>obligatorio </p> </td>
  </tr>
  <tr>
   <td><p>Mensaje vacío (nullTestMessage) </p> </td>
   <td><p>mandatoryMessage</p> </td>
  </tr>
  <tr>
   <td><p>Validar secuencia de comandos (scriptTest)</p> </td>
   <td><p>validateExp</p> </td>
  </tr>
  <tr>
   <td><p>Mensaje de la secuencia de comandos de validación (scriptTestMessage)</p> </td>
   <td><p>validateMessage</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>No se puede anular la propiedad obligatoria del botón de opción de formulario adaptable y del grupo de casillas de verificación enlazados a los botones de verificación XFA.

