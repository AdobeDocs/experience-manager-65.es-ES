---
title: Compatibilidad con cláusula de imagen para formularios HTML5
seo-title: Compatibilidad con cláusula de imagen para formularios HTML5
description: Los formularios HTML5 son compatibles con la cláusula de imagen XFA para mostrar valor y valor formateado para símbolos numéricos, de texto y de fecha.
seo-description: Los formularios HTML5 son compatibles con la cláusula de imagen XFA para mostrar valor y valor formateado para símbolos numéricos, de texto y de fecha.
uuid: ca5074ce-8219-4f27-a37c-b1f0dca4ce03
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 5%

---


# Compatibilidad con cláusula de imagen para formularios HTML5 {#picture-clause-support-for-html-forms}

Los formularios HTML5 son compatibles con la cláusula de imagen XFA para mostrar valor y valor formateado para símbolos numéricos, de texto y de fecha. Se admiten las expresiones de cláusula de imagen siguientes:

* category(locale){picture-subscription} | category(locale){picture-subscription} | category(locale){picture-subscription}
* category.subcategory{}

>[!NOTE]
>
>Actualmente, Mobile Forms no admite la cláusula Editar imagen. Además, no se admiten los símbolos de las cláusulas DateTime y Time Picture.

## Símbolos de campo de fecha admitidos {#supported-date-field-symbols}

Expresión admitida para la cláusula Date Picture:

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* date{date Picture Clause símbolos}

>[!NOTE]
>
>El patrón predeterminado de la cláusula de imagen es el patrón {MMM D, AAAA}. Si no se aplica ningún patrón, se utiliza el patrón predeterminado.

<table>
 <tbody>
  <tr>
   <th><strong>Símbolo</strong></th>
   <th>Interpretación</th>
  </tr>
  <tr>
   <td>D</td>
   <td>Día del mes expresado con 1 o 2 dígitos (1-31).</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>Día del mes expresado con 2 dígitos (se rellena con ceros en el caso de los días 1 a 31).<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>Mes del año expresado con 1 o 2 dígitos (1-12).<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>Mes del año expresado con 2 dígitos (se rellena con ceros en el caso de los meses 1 a 12).<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>Nombre abreviado del mes de la configuración regional actual<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>Nombre completo del mes de la configuración regional actual<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>Nombre abreviado del día de la semana de la configuración regional actual<br /> </td>
  </tr>
  <tr>
   <td>EEEE</td>
   <td>Nombre completo del día de la semana de la configuración regional actual<br /> </td>
  </tr>
  <tr>
   <td>YY</td>
   <td>año de 2 dígitos, donde 00 = 2000, 29 = 2029, 30 = 1930 y 99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>YYYY</td>
   <td>Año de 4 dígitos<br /> </td>
  </tr>
 </tbody>
</table>

## Cláusula de imagen numérica {#numeric-picture-clause}

Los formularios HTML5 admiten símbolos de imagen numérica. Sin embargo, existe una diferencia en la compatibilidad entre los PDF forms y HTML Forms.

En **PDF forms**, se da formato a un número independientemente del número de símbolos que tenga la cláusula Picture

En **HTML Forms**, un número tiene formato únicamente si el número tiene dígitos inferiores al número de símbolos de la cláusula Picture.

**Ejemplo**: Considere una cláusula Picture: num{zzz,zzz,zz9}.

El número **10000** tiene el formato **10.000** tanto en HTML como en PDF forms.

El número 1000000 tiene un formato de 1 000 000 PDF forms. Sin embargo, en HTML Forms el número permanece sin formato como 100000.

Las expresiones admitidas para la cláusula de Imagen numérica en **HTML Forms** son:

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{Numeric Picture Clause Symbols}

<table>
 <tbody>
  <tr>
   <th><strong>Símbolo</strong></th>
   <th><strong>Interpretación</strong></th>
   <th>Análisis de entrada</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>Formato</strong> de salida: un solo dígito. O para el dígito cero si los datos de entrada están vacíos o si hay un espacio en la posición correspondiente.<br /> </td>
   <td>Dígito sencillo</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>Formato</strong> de salida: un solo dígito. O para un espacio si los datos de entrada están vacíos, un espacio o el dígito cero en la posición correspondiente.<br /> </td>
   <td>Un solo dígito o espacio</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>Formato</strong> de salida: un solo dígito. O para nada si los datos de entrada están vacíos, un espacio o el dígito cero en la posición correspondiente.<br /> </td>
   <td>Un solo dígito o nada</td>
  </tr>
  <tr>
   <td>E</td>
   <td><strong>Formato</strong> de salida: la parte exponencial de un número de coma flotante que consta del símbolo exponencial (E). Seguido de un signo más o menos opcional. Seguido por el valor exponencial.<br /> </td>
   <td>Igual que para el formato de salida</td>
  </tr>
  <tr>
   <td>CR o cr<br /> </td>
   <td>Símbolo de crédito (CR) si el número es negativo. No más.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S o s<br /> </td>
   <td>Formato de salida: un signo menos si el número es negativo. Espacio restante.<br /> </td>
   <td>Signo menos si el número es negativo. Signo más si el número es positivo</td>
  </tr>
  <tr>
   <td>V</td>
   <td>Base decimal de la configuración regional predominante. Permiso para que la base decimal sea implícita al analizar la entrada.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>Base decimal de la configuración regional predominante. Permiso para que la base decimal sea implícita al analizar la entrada y al dar formato de salida.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>.</td>
   <td>Base decimal de la configuración regional predominante.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>, (U+FF0C)</td>
   <td>Separador de agrupación de la configuración regional prevaleciente</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>$ (U+FF04)</td>
   <td>Símbolo de moneda de la configuración regional predominante.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>% (U+FF05)</td>
   <td>Símbolo porcentual de la configuración regional prevaleciente.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>(U+FF08)</td>
   <td>Paréntesis izquierdo si el número es negativo. Más espacio.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>) (U+FF09)</td>
   <td>Paréntesis derecho si el número es negativo. Más espacio.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>t</td>
   <td>Carácter de tabulación</td>
   <td><br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## Cláusula de imagen de texto {#text-picture-clause}

Los formularios HTML5 admiten las siguientes expresiones de cláusula de imagen de texto:

* text{text Picture, símbolos de cláusula de imagen}

| **Símbolo** | **Interpretación** |
|---|---|
| A | Carácter alfabético sencillo. |
| X | Carácter sencillo. |
| O | Carácter alfanumérico sencillo. |
| 0 (cero) | Carácter alfanumérico sencillo. |
| 9 | Dígito sencillo. |
