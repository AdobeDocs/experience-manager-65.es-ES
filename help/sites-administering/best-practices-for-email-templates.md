---
title: Prácticas recomendadas para plantillas de correo electrónico
seo-title: Prácticas recomendadas para plantillas de correo electrónico
description: Encuentre optimizaciones para crear plantillas de correo electrónico en AEM.
seo-description: Encuentre optimizaciones para crear plantillas de correo electrónico en AEM.
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
translation-type: tm+mt
source-git-commit: 4333cfde433d00ddc4cb013b31fe52956791da46
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 1%

---


# Prácticas recomendadas para plantillas de correo electrónico {#best-practices-for-email-templates}

>[!CAUTION]
>
>Los componentes de correo electrónico AEM han quedado obsoletos. Debido a la naturaleza del correo electrónico, que combina contenido y estilo, los componentes de correo electrónico proporcionados de forma predeterminada por AEM se vuelven de uso limitado para los clientes debido a la necesidad de implementar estilos personalizados en los componentes que sean necesarios para los proyectos.
>
>Los componentes de correo electrónico se pueden implementar a nivel de proyecto y los componentes de correo electrónico AEM obsoletos ilustran cómo se puede lograr. Sin embargo, estos componentes desaprobados no deben usarse en proyectos.

Este documento describe algunas de las prácticas recomendadas en torno al diseño del correo electrónico, lo que resulta en una plantilla de campaña de correo electrónico bien desarrollada.

La campaña de demostración disponible en AEM sigue todas estas prácticas recomendadas. La forma en que se implementan las prácticas recomendadas en la campaña de demostración se describe para cada práctica recomendada.

Siga estas prácticas recomendadas para crear su propia newsletter.

>[!NOTE]
>
>Todo el contenido de campaña debe crearse en una `master` página de tipo `cq/personalization/components/ambitpage`.
>
>Por ejemplo, si la estructura de campaña planificada es algo similar a
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>Debe asegurarse de que reside en una página `master`
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>Al crear una plantilla de correo para Adobe Campaign, debe incluir la propiedad **acMapping** con el valor **mapRecipient** en el nodo **jcr:content** de la plantilla, o no podrá seleccionar la plantilla Adobe Campaign en **Propiedades de la página** de AEM (el campo está deshabilitado).

## Plantilla/componente de página {#template-page-component}

***/libs/mcm/campaña/components/campaña_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>Práctica recomendada</strong></td>
   <td><strong>Implementación</strong></td>
  </tr>
  <tr>
   <td><p>Especifique el tipo de documento para garantizar una representación coherente.</p> <p>Añadir DOCTYPE al principio (HTML o XHTML)</p> </td>
   <td><p>Se puede configurar mediante el diseño cambiando la propiedad <i>cq:doctype</i> en<i>"/etc/designs/default/jcr:content/campaña_newsletterpage"</i></p> <p>El valor predeterminado es "XHTML":</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>Se puede cambiar a "HTML_5":</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Especifique la definición de caracteres para garantizar la representación correcta de caracteres especiales.</p> <p>Añadir la declaración CHARSET (p. ej. iso-8859-15, UTF-8) en &lt;head&gt;</p> </td>
   <td><p>Se establece en UTF-8.</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Codifique toda la estructura mediante el elemento &lt;table&gt;. Para diseños más complicados, debe anidar tablas para crear estructuras complejas.</p> <p>El correo electrónico debería verse bien incluso sin css.</p> </td>
   <td><p>Las tablas se utilizan en toda la plantilla para estructurar el contenido. Actualmente se está utilizando un máximo de cuatro tablas anidadas (1 tabla base + máx.). 3 niveles de anidación)</p> <p>&lt;div&gt; las etiquetas solo se utilizan en el modo de autor para garantizar una adecuada edición de componentes.</p> </td>
  </tr>
  <tr>
   <td>Utilice atributos de elemento (como relleno de celdas, validación y ancho) para definir las dimensiones de la tabla. Esto fuerza una estructura de modelo de caja.</td>
   <td><p>Todas las tablas contienen atributos necesarios como <i>borde</i>, <i>relleno de celdas</i>, <i>espaciado entre celdas</i> y <i>ancho</i>.</p> <p>Para armonizar la posición del elemento dentro de las tablas, todas las celdas de la tabla tienen el atributo <i>valign="top"</i> establecido.</p> </td>
  </tr>
  <tr>
   <td><p>Si es posible, tenga en cuenta la facilidad de uso de los dispositivos móviles. Utilice consultas de medios para aumentar el tamaño del texto en pantallas pequeñas y proporcione áreas de visita del tamaño de la miniatura para los vínculos.</p> <p>Haga que un correo electrónico responda si el diseño lo permite.</p> </td>
   <td>En cuanto a los estilos CSS que se utilizan para ilustrar el diseño de demostración, se utilizan consultas de medios para realizar la oferta de una versión móvil compatible.</td>
  </tr>
  <tr>
   <td>La CSS en línea es mejor que colocar toda la CSS al principio.</td>
   <td><p>Para demostrar mejor la estructura HTML subyacente y facilitar la posibilidad de personalizar la estructura de la newsletter, solo se han subrayado algunas definiciones de CSS.</p> <p>Los estilos base y las variaciones de plantilla se han extraído a un bloque de estilo en el &lt;encabezado&gt; de la página. En el envío final de la newsletter, estas definiciones de CSS deben insertarse en el HTML. Está previsto un mecanismo automático de inlineado, pero actualmente no está disponible.</p> </td>
  </tr>
  <tr>
   <td>Mantenga la CSS sencilla. Evite declaraciones de estilo compuestas, código abreviado, propiedades de diseño CSS, selectores complejos y pseudoelementos.</td>
   <td>En cuanto a los estilos CSS que se utilizan para ilustrar el diseño de demostración, se siguen las recomendaciones CSS.</td>
  </tr>
  <tr>
   <td>Los mensajes de correo electrónico deben tener una anchura máxima de 600-800 píxeles. Esto hará que se comporten mejor dentro del tamaño del panel de previsualización proporcionado por muchos clientes.</td>
   <td>La <i>anchura</i> de la tabla de contenido está limitada a 600 px en el diseño de demostración.</td>
  </tr>
 </tbody>
</table>

### Imágenes {#images}

/libs/mcm/campaña/components/image

| **Práctica recomendada** | **Implementación** |
|---|---|
| Añadir atributos *alt* en imágenes | El atributo *alt* se ha definido como obligatorio para el componente de imagen. |
| Utilice el formato *jpg* en lugar del formato *png* para las imágenes | El componente de imagen siempre servirá como JPG las imágenes. |
| Utilice el elemento `<img>` en lugar de imágenes de fondo en una tabla. | No se utilizan datos de imagen de fondo en las plantillas. |
| Añada attribute style=&quot;display block&quot; en imágenes. Permite mostrar bien en Gmail. | Todas las imágenes contienen de forma predeterminada el atributo *style=&quot;display block&quot;*. |

### Texto y vínculos {#text-and-links}

/libs/mcm/campaña/components/heading, /libs/mcm/campaña/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>Práctica recomendada</strong></td>
   <td><strong>Implementación</strong></td>
  </tr>
  <tr>
   <td>Utilice html &lt;font&gt; en lugar de estilo en CSS (font-family)</td>
   <td>RichTextEditor (por ejemplo, en el componente textimage) ahora admite la selección y aplicación de familias de fuentes y tamaños de fuente a los textos seleccionados. Se representarán como etiquetas &lt;font&gt;.</td>
  </tr>
  <tr>
   <td>Utilice fuentes básicas y multiplataforma como <i>Arial, Verdana, Georgia</i> y <i>Times New Roman</i>.</td>
   <td><p>Depende del diseño de la newsletter.</p> <p>Para el diseño de demostración, se utiliza la fuente "Helvetica", pero regresará a la fuente sans-serif genérica, si no está presente.</p> </td>
  </tr>
 </tbody>
</table>

### Genérico {#generic}

| **Práctica recomendada** | **Implementación** |
|---|---|
| Use el validador de W3C para corregir el código HTML. Asegúrese de que todas las etiquetas abiertas estén correctamente cerradas. | Se validó el código. Para XHTML transicional Doctype, solo falta el atributo xmlns que falta para el elemento `<html>`. |
| No se preocupe por JavaScript o Flash: los clientes de correo electrónico no admiten estas tecnologías. | No se utiliza JavaScript ni Flash en la plantilla de newsletter. |
| Añada una versión de texto sin formato para el envío de varias partes. | Se ha incorporado una nueva utilidad en las propiedades de la página para extraer fácilmente una versión de texto sin formato del contenido de la página. Se puede utilizar como punto de partida para la versión final de texto sin formato. |

## Ejemplos y plantillas de newsletter de campaña {#campaign-newsletter-templates-and-examples}

AEM incluye varias plantillas y componentes listos para usar para crear newsletters de campaña. Puede utilizar estas plantillas y componentes para crear boletines informativos personalizados.

### Plantillas {#templates}

Para oferta de una base sólida y ampliar la variedad de posibilidades de flujo de contenido, hay tres tipos de plantilla ligeramente diferentes disponibles de forma predeterminada. Puede utilizarlos fácilmente para crear una newsletter personalizada.

Todos tienen una sección **header**, un **pie de página** y una sección **body**. Debajo de la sección body, cada plantilla difiere en **diseño de columna** (1, 2 o 3 columnas).

![](assets/chlimage_1-69.png)

### Componentes {#components}

Actualmente hay [siete componentes disponibles para su uso dentro de plantillas de campaña](/help/sites-authoring/adobe-campaign-components.md). Todos estos componentes se basan en el lenguaje de marcado de Adobe **HTL**.

| **Nombre del componente** | **Ruta del componente** |
|---|---|
| Encabezado | /libs/mcm/campaña/components/heading |
| Imagen | /libs/mcm/campaña/components/image |
| Texto y personalización | /libs/mcm/campaña/components/personalization |
| Textimage | /libs/mcm/campaña/components/textimage |
| Vínculo | /libs/mcm/campaña/components/reference |
| Plantilla de imagen de Dynamic Media Classic (anteriormente Scene7) | /libs/mcm/campaña/s7image |
| Referencia de objetivo | /libs/mcm/campaña/components/reference |

>[!NOTE]
>
>Estos componentes están optimizados para el contenido del correo; es decir, se adhieren a las mejores prácticas descritas en este documento. El uso de otros componentes listos para usar generalmente infringe estas reglas.

Estos componentes se describen en detalle en [componentes de Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md).