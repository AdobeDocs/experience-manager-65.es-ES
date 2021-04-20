---
title: Estilo en línea de los componentes de formulario adaptables
seo-title: Propiedades CSS en línea para componentes de formulario adaptables
description: Aunque puede aplicar estilos personalizados en un formulario adaptable, también puede aplicar propiedades CSS en línea en componentes individuales de un formulario adaptable.
seo-description: Aunque puede aplicar estilos personalizados en un formulario adaptable, también puede aplicar propiedades CSS en línea en componentes individuales de un formulario adaptable.
uuid: e863780e-2250-4bea-9569-22be5638d54e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 21dec713-c76d-408b-baea-fc585377b429
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 3%

---


# Estilo en línea de los componentes de formulario adaptables {#inline-styling-of-adaptive-form-components}

Puede definir el aspecto y el estilo generales de un formulario adaptable especificando los estilos mediante [editor de temas](../../forms/using/themes.md). Además, puede aplicar estilos CSS en línea a componentes de formulario adaptables individuales y previsualizar los cambios sobre la marcha. Los estilos en línea anulan el estilo proporcionado en el tema.

## Aplicar propiedades CSS en línea {#apply-inline-css-properties}

Para añadir estilos en línea a un componente:

1. Abra el formulario en el editor de formularios y cambie el modo a modo de estilo. Para cambiar el modo al modo de estilo, en la barra de herramientas de la página, pulse ![lienzo-desplegable](assets/canvas-drop-down.png) > **Estilo**.
1. Seleccione un componente en la página y pulse el botón de edición ![editar-button](assets/edit-button.png). Propiedades de estilo abiertas en la barra lateral.

   También puede seleccionar componentes del árbol de jerarquía de formularios en la barra lateral. El árbol de jerarquía de formularios está disponible como Objetos de formulario en la barra lateral.

   También puede seleccionar un componente de la barra lateral. En el modo Estilo, puede ver los componentes enumerados en Objetos de formulario. Sin embargo, la lista Objetos de formulario de la barra lateral enumera componentes como campos y paneles. Los campos y los paneles son componentes genéricos que pueden contener componentes como, por ejemplo, cuadros de texto y botones de opción.

   Al seleccionar un componente de la barra lateral, se ven todos los subcomponentes enumerados y las propiedades del componente seleccionado. Puede seleccionar un subcomponente específico y aplicarle un estilo.

1. Haga clic en una ficha de la barra lateral para especificar las propiedades CSS. Puede especificar propiedades como:

   * Dimension y posición (visualización, relleno, altura, anchura, margen, posición, z-index, flotante, transparente, desbordamiento)
   * Texto (familia de fuentes, peso, color, tamaño, altura de línea y alineación)
   * Fondo (imagen y degradado, color de fondo)
   * Borde (ancho, estilo, color, radio)
   * Efectos (Sombra, Opacidad)
   * Avanzado (permite escribir CSS personalizada para el componente)

1. Del mismo modo, puede aplicar estilos a otras partes de un componente, como Widget, Rótulo y Ayuda.
1. Toque **Listo** para confirmar los cambios o **Cancelar** para descartar los cambios.

## Ejemplo: estilos en línea para un componente de campo {#example-inline-styles-for-a-field-component}

Las siguientes imágenes muestran un campo de texto antes y después de que se le apliquen estilos en línea.

![Componente de cuadro de texto antes de aplicar estilo en línea](assets/no-style.png)

Componente de cuadro de texto antes de aplicar propiedades de estilo en línea

Observe el cambio en el estilo del cuadro de texto como se muestra en la siguiente imagen después de aplicar las siguientes propiedades CSS.

<table>
 <tbody>
  <tr>
   <td><p>Selector</p> </td>
   <td><p>CSS, propiedad</p> </td>
   <td><p>Value</p> </td>
   <td><p>Efecto</p> </td>
  </tr>
  <tr>
   <td><p>Campo</p> </td>
   <td><p>border</p> </td>
   <td><p>Ancho del borde = 2 px</p> <p>Estilo de borde=Sólido</p> <p>Color del borde=#1111</p> </td>
   <td><p>Crea un borde ancho negro de 2 píxeles alrededor del campo</p> </td>
  </tr>
  <tr>
   <td><p>Cuadro de texto</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>Cambia el color de fondo a CornflowerBlue (#6495ED)</p> <p>Nota: Puede especificar un nombre de color o su código hexadecimal en el campo de valor.</p> </td>
  </tr>
  <tr>
   <td><p>Etiqueta</p> </td>
   <td><p>Dimensiones y posición &gt; anchura</p> </td>
   <td><p>100px</p> </td>
   <td><p>Corrige la anchura de 100 píxeles para la etiqueta</p> </td>
  </tr>
  <tr>
   <td>Icono de ayuda de campo</td>
   <td>Texto &gt; Color de fuente</td>
   <td>#2ECC40</td>
   <td>Cambia el color de la cara del icono de ayuda.</td>
  </tr>
  <tr>
   <td><p>Descripción larga</p> </td>
   <td><p>text-align</p> </td>
   <td><p>center</p> </td>
   <td><p>Alinea la descripción larga para que la ayuda se centre</p> </td>
  </tr>
 </tbody>
</table>

![Estilo de cuadro de texto después de aplicar estilo en línea](assets/applied-style.png)

Componente de cuadro de texto después de aplicar propiedades de estilo en línea

Siguiendo los pasos anteriores, puede seleccionar y aplicar estilo a otros componentes, como paneles, botones de envío y botones de radio.

>[!NOTE]
>
>Las propiedades de estilo varían en función del componente que seleccione.

