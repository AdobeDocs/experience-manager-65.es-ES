---
title: Prácticas recomendadas para plantillas de correo electrónico
seo-title: Best Practices for Email Templates
description: Encuentre prácticas recomendadas sobre la creación de plantillas de correo electrónico en AEM.
seo-description: Find best practices on creating email templates in AEM.
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
exl-id: 6666eddc-dc17-4bd4-9d55-e6522f40a680
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 1%

---

# Prácticas recomendadas para plantillas de correo electrónico {#best-practices-for-email-templates}

>[!CAUTION]
>
>Los componentes de correo electrónico AEM han quedado obsoletos. Debido a la naturaleza del correo electrónico, que combina contenido y estilo, los componentes de correo electrónico proporcionados de forma predeterminada por AEM se vuelven de reutilización limitada para los clientes debido a la necesidad de implementar estilos personalizados en los componentes necesarios para los proyectos.
>
>Los componentes de correo electrónico se pueden implementar en el nivel de proyecto y los componentes de correo electrónico AEM obsoletos ilustran cómo se puede lograr. Sin embargo, estos componentes obsoletos no deben utilizarse en proyectos.

En este documento se describen algunas de las prácticas recomendadas relacionadas con el diseño de correo electrónico, lo que resulta en una plantilla de campaña de correo electrónico bien desarrollada.

La campaña de demostración disponible en AEM sigue todas estas prácticas recomendadas. Para cada práctica recomendada se describe cómo se implementan las prácticas recomendadas en la campaña de demostración.

Siga estas prácticas recomendadas al crear su propio boletín informativo.

>[!NOTE]
>
>Todo el contenido de la campaña debe crearse en una `master` página de tipo `cq/personalization/components/ambitpage`.
>
>Por ejemplo, si la estructura de la campaña planificada es algo así
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>Debe asegurarse de que reside en un `master` página
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>Al crear una plantilla de correo para Adobe Campaign, debe incluir la propiedad **acMapping** con el valor **mapRecipient** en el **jcr:content** de la plantilla, o no podrá seleccionar la plantilla Adobe Campaign en **Propiedades de página** de AEM (el campo está deshabilitado).

## Componente de plantilla/página {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>Práctica recomendada</strong></td>
   <td><strong>Implementación</strong></td>
  </tr>
  <tr>
   <td><p>Especifique el tipo de documento para garantizar una representación coherente.</p> <p>Agregar DOCTYPE al principio (HTML o XHTML)</p> </td>
   <td><p>Se puede configurar cambiando el diseño de <i>cq:doctype</i> propiedad en<i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i></p> <p>El valor predeterminado es "XHTML":</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>Se puede cambiar a "HTML_5":</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Especifique la definición del carácter para garantizar la representación correcta de los caracteres especiales.</p> <p>Agregar la declaración CHARSET (por ejemplo, iso-8859-15, UTF-8) a &lt;head&gt;</p> </td>
   <td><p>Se establece en UTF-8.</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Codifique todas las estructuras utilizando la variable &lt;table&gt;elemento. Para diseños más complicados, debe anidar tablas para crear estructuras complejas.</p> <p>El correo electrónico debería tener un aspecto adecuado incluso sin css.</p> </td>
   <td><p>Las tablas se utilizan en toda la plantilla para estructurar el contenido. Actualmente se está utilizando un máximo de cuatro tablas anidadas (1 tabla base + máx.). 3 niveles de anidación)</p> <p>&lt;div&gt; las etiquetas solo se utilizan en el modo de autor para garantizar la correcta edición de los componentes.</p> </td>
  </tr>
  <tr>
   <td>Utilice atributos de elemento (como el relleno de celdas, la validación y la anchura) para establecer las dimensiones de la tabla. Esto fuerza una estructura de modelo de caja.</td>
   <td><p>Todas las tablas contienen atributos necesarios como <i>borde</i>, <i>cellpadding</i>, <i>espaciado de celdas</i> y <i>width</i>.</p> <p>Para armonizar la colocación de elementos dentro de las tablas, todas las celdas de la tabla tienen el atributo <i>valign="top"</i> que se está configurando.</p> </td>
  </tr>
  <tr>
   <td><p>Tenga en cuenta la facilidad de uso del móvil, si es posible. Utilice consultas de medios para aumentar el tamaño del texto en pantallas pequeñas y proporcione áreas de visita del tamaño de la miniatura para los vínculos.</p> <p>Haga que un correo electrónico responda si el diseño lo permite.</p> </td>
   <td>En la medida en que se utilizan estilos CSS para ilustrar el diseño de demostración, las consultas de medios se utilizan para ofrecer una versión compatible con dispositivos móviles.</td>
  </tr>
  <tr>
   <td>CSS en línea es mejor que poner toda la CSS al principio.</td>
   <td><p>Para demostrar mejor la estructura del HTML subyacente y facilitar la posibilidad de personalizar la estructura del boletín, solo se han resaltado algunas definiciones de CSS.</p> <p>Los estilos base y las variaciones de plantilla se han extraído a un bloque de estilos en la variable &lt;head&gt; de la página. En el envío final del boletín, estas definiciones de CSS deben incluirse en el HTML. Está previsto un mecanismo automático de inlineado, pero actualmente no está disponible.</p> </td>
  </tr>
  <tr>
   <td>Mantenga su CSS simple. Evite declaraciones de estilo compuestas, código abreviado, propiedades de diseño CSS, selectores complejos y pseudoelementos.</td>
   <td>En cuanto a los estilos CSS que se utilizan para ilustrar el diseño de demostración, se siguen las recomendaciones CSS.</td>
  </tr>
  <tr>
   <td>Los correos electrónicos deben tener una anchura máxima de 600-800 píxeles. Esto les hará comportarse mejor dentro del tamaño del panel de vista previa proporcionado por muchos clientes.</td>
   <td>La variable <i>width</i> de la tabla de contenido está limitada a 600 px en el diseño de demostración.</td>
  </tr>
 </tbody>
</table>

### Imágenes {#images}

/libs/mcm/campaign/components/image

| **Práctica recomendada** | **Implementación** |
|---|---|
| Agregar *alt* atributos a imágenes | La variable *alt* se ha definido como obligatorio para el componente de imagen. |
| Uso *jpg* en lugar de *png* formato para imágenes | El componente de imagen siempre servirá como JPG las imágenes. |
| Uso `<img>` en lugar de imágenes de fondo en una tabla. | En las plantillas no se utilizan datos de imagen de fondo. |
| Añada attribute style=&quot;display block&quot; en imágenes. Permite mostrar bien en Gmail. | Todas las imágenes contienen de forma predeterminada la variable *style=&quot;display block&quot;* atributo. |

### Texto y vínculos {#text-and-links}

/libs/mcm/campaign/components/header, /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>Práctica recomendada</strong></td>
   <td><strong>Implementación</strong></td>
  </tr>
  <tr>
   <td>Utilizar html en lugar de estilo en CSS (font-family)</td>
   <td>RichTextEditor (por ejemplo, en el componente textimage) ahora admite la selección y aplicación de familias de fuentes y tamaños de fuente a textos seleccionados. Se procesarán como etiquetas.</td>
  </tr>
  <tr>
   <td>Utilice fuentes básicas entre plataformas como <i>Arial, Verdana, Georgia</i> y <i>Times New Roman</i>.</td>
   <td><p>Depende del diseño de la newsletter.</p> <p>Para el diseño de demostración se utiliza la fuente "Helvetica", pero regresará a la fuente genérica sans-serif, si no está presente.</p> </td>
  </tr>
 </tbody>
</table>

### Genérico {#generic}

| **Práctica recomendada** | **Implementación** |
|---|---|
| Utilice el validador W3C para corregir el código del HTML. Asegúrese de que todas las etiquetas abiertas estén correctamente cerradas. | Se validó el código. Para el tipo de documento de transición XHTML solo falta el atributo xmlns para la variable `<html>` falta el elemento . |
| No se preocupe por JavaScript o Flash: estos métodos no son compatibles con los clientes de correo electrónico. | Ni JavaScript ni el Flash se usan en la plantilla del boletín informativo. |
| Añada una versión de texto sin formato para el envío de varias partes. | Se ha incorporado un nuevo widget en las propiedades de página para extraer fácilmente una versión de texto sin formato del contenido de la página. Esto puede utilizarse como punto de partida para la versión final de texto sin formato. |

## Plantillas y ejemplos de boletines informativos de Campaign {#campaign-newsletter-templates-and-examples}

AEM viene con varias plantillas y componentes listos para usar para crear boletines de campaña. Puede utilizar estas plantillas y componentes para crear boletines informativos personalizados.

### Plantillas {#templates}

Para ofrecer una base sólida y ampliar la variedad de posibilidades de flujo de contenido, hay tres tipos de plantilla disponibles de forma predeterminada. Puede utilizarlos fácilmente para crear un boletín personalizado.

Todos tienen un **header**, **pie de página** y **body** para obtener más información. Debajo de la sección del cuerpo, cada plantilla difiere en **diseño de columna** (1, 2 o 3 columnas).

![](assets/chlimage_1-69.png)

### Componentes {#components}

Actualmente hay [siete componentes disponibles para su uso en plantillas de campaña](/help/sites-authoring/adobe-campaign-components.md). Todos estos componentes se basan en el lenguaje de marcado de Adobe **HTL**.

| **Nombre del componente** | **Ruta del componente** |
|---|---|
| Encabezado | /libs/mcm/campaign/components/header |
| Imagen | /libs/mcm/campaign/components/image |
| Texto y personalización | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| Vincular | /libs/mcm/campaign/components/reference |
| Plantilla de imagen de Dynamic Media Classic (anteriormente Scene7) | /libs/mcm/campaign/s7image |
| Referencia de destino | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>Estos componentes están optimizados para el contenido del correo; es decir, se adhieren a las prácticas recomendadas descritas en este documento. El uso de otros componentes listos para usar normalmente infringirá estas reglas.

Estos componentes se describen detalladamente en [Componentes de Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md).
