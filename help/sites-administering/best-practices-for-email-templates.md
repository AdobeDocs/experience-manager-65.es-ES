---
title: Prácticas recomendadas para plantillas de correo electrónico
description: AEM Encuentre prácticas recomendadas sobre la creación de plantillas de correo electrónico en la.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
docset: aem65
exl-id: 6666eddc-dc17-4bd4-9d55-e6522f40a680
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 0%

---


# Prácticas recomendadas para plantillas de correo electrónico {#best-practices-for-email-templates}

>[!CAUTION]
>
>AEM Este artículo se aplica a los componentes de base obsoletos basados en componentes de correo electrónico de la.
>
>Se recomienda a los usuarios que utilicen el [Componentes principales Componentes de correo electrónico.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html)

Este documento describe algunas de las prácticas recomendadas en cuanto al diseño de correos electrónicos, lo que da como resultado una plantilla de campaña de correo electrónico bien desarrollada.

AEM La campaña de demostración disponible en la sección de la documentación de sigue todas estas prácticas recomendadas de administración de segmentos de mercado. Se describe cómo se implementan las prácticas recomendadas en la campaña de demostración para cada práctica recomendada.

Siga estas prácticas recomendadas al crear su propia newsletter.

>[!NOTE]
>
>Todo el contenido de la campaña debe crearse en una `master` página de tipo `cq/personalization/components/ambitpage`.
>
>Por ejemplo, si la estructura de la campaña planificada es similar a
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>Asegúrese de que se encuentra debajo de `master` página
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>Al crear una plantilla de correo electrónico para Adobe Campaign, debe incluir la propiedad **acMapping** con el valor **mapRecipient** en el **jcr:contenido** nodo de la plantilla. Si no lo hace, no puede seleccionar la plantilla Adobe Campaign en **Propiedades de página** del Experience Manager (el campo está desactivado).

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
   <td><p>Es configurable por el diseño cambiando el <i>cq:doctype</i> propiedad en<i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i></p> <p>El valor predeterminado es "XHTML":</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional/EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>Se puede cambiar a "HTML_5":</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Especifique la definición de caracteres para garantizar la correcta representación de los caracteres especiales.</p> <p>Agregue la declaración CHARSET (por ejemplo, iso-8859-15, UTF-8) a &lt;head&gt;</p> </td>
   <td><p>Se establece en UTF-8.</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Codifique toda la estructura utilizando &lt;table&gt;Elemento. Para diseños más complicados, debe anidar tablas para crear estructuras complejas.</p> <p>El correo electrónico debería verse bien incluso sin css.</p> </td>
   <td><p>Las tablas se utilizan en toda la plantilla para estructurar el contenido. Actualmente se utiliza un máximo de cuatro tablas anidadas (1 tabla base + máx. 3 niveles de anidación)</p> <p>&lt;div&gt; las etiquetas solo se utilizan en el modo de autor para garantizar la edición adecuada de los componentes.</p> </td>
  </tr>
  <tr>
   <td>Utilice atributos de elemento (como relleno de celda, validación y anchura) para establecer las dimensiones de la tabla. Este método fuerza una estructura de modelo de cuadro.</td>
   <td><p>Todas las tablas contienen atributos necesarios como <i>borde</i>, <i>cellpadding</i>, <i>espaciado de celdas</i>, y <i>anchura</i>.</p> <p>Para armonizar la colocación de los elementos dentro de las tablas, todas las celdas de la tabla tienen el atributo <i>valign="top"</i> que se está configurando.</p> </td>
  </tr>
  <tr>
   <td><p>Tenga en cuenta la compatibilidad con dispositivos móviles, si es posible. Utilice consultas de medios para aumentar el tamaño del texto en pantallas pequeñas y proporcione áreas de visita en miniatura para los vínculos.</p> <p>Hacer que un correo electrónico sea adaptable si el diseño lo permite.</p> </td>
   <td>En la medida en que los estilos CSS se utilizan para ilustrar el diseño de demostración, las consultas de medios se utilizan para ofrecer una versión compatible con dispositivos móviles.</td>
  </tr>
  <tr>
   <td>CSS en línea es mejor que colocar todo el CSS al principio.</td>
   <td><p>Para mostrar mejor la estructura del HTML subyacente y facilitar la personalización de la estructura del boletín informativo, solo se han insertado algunas definiciones de CSS.</p> <p>Los estilos base y las variaciones de plantilla se han extraído a un bloque de estilo en la &lt;head&gt; de la página. Al enviar la newsletter final, estas definiciones de CSS se insertan en el HTML. Se ha planificado un mecanismo de inline automático, pero actualmente no está disponible.</p> </td>
  </tr>
  <tr>
   <td>Simplifique el código CSS. Evite las declaraciones de estilos compuestos, el código abreviado, las propiedades de diseño CSS, los selectores complejos y los pseudoelementos.</td>
   <td>En cuanto a los estilos CSS que se utilizan para ilustrar el diseño de demostración, se siguen las recomendaciones CSS.</td>
  </tr>
  <tr>
   <td>Los correos electrónicos deben tener una anchura máxima de 600-800 píxeles. Este tamaño hace que se comporten mejor dentro del tamaño del panel de vista previa proporcionado por muchos clientes.</td>
   <td>El <i>anchura</i> El tamaño de la tabla de contenido está limitado a 600 píxeles en el diseño de demostración.</td>
  </tr>
 </tbody>
</table>

### Imágenes {#images}

/libs/mcm/campaign/components/image

| **Práctica recomendada** | **Implementación** |
|---|---|
| Añadir *alt* atributos a imágenes | El *alt* El atributo se ha definido como obligatorio para el componente de imagen. |
| Uso *jpg* en lugar de *png* formato para imágenes | El componente de imagen siempre sirve como JPG a las imágenes. |
| Uso `<img>` en lugar de imágenes de fondo en una tabla. | No se utilizan datos de imagen de fondo en las plantillas. |
| Añadir el atributo style=&quot;display block&quot; en las imágenes. Al hacerlo, se muestran bien en Gmail. | Todas las imágenes contienen de forma predeterminada el *style=&quot;bloque de visualización&quot;* atributo. |

### Texto y vínculos {#text-and-links}

/libs/mcm/campaign/components/heading, /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>Práctica recomendada</strong></td>
   <td><strong>Implementación</strong></td>
  </tr>
  <tr>
   <td>Utilice html en lugar de estilo en CSS (familia de fuentes)</td>
   <td>RichTextEditor (por ejemplo, en el componente textimage) ahora admite la selección y aplicación de familias de fuentes y tamaños de fuente a textos seleccionados. Se representan como etiquetas.</td>
  </tr>
  <tr>
   <td>Utilice fuentes básicas entre plataformas, como <i>Arial®, Verdana, Georgia</i>, y <i>Times New Roman®</i>.</td>
   <td><p>Depende del diseño de la newsletter.</p> <p>Para el diseño de demostración, se utiliza la fuente "Helvetica®", pero vuelve a una fuente sans-serif genérica, si no está presente.</p> </td>
  </tr>
 </tbody>
</table>

### Genérica {#generic}

| **Práctica recomendada** | **Implementación** |
|---|---|
| Utilice el validador W3C para corregir el código del HTML. Asegúrese de que todas las etiquetas abiertas estén correctamente cerradas. | Se ha validado el código. Solo para el tipo de documento XHTML transitorio, falta el atributo xmlns para el `<html>` falta el elemento. |
| Evite utilizar JavaScript o Flash: estas tecnologías suelen ser incompatibles con los clientes de correo electrónico. | JavaScript o Flash no se utilizan en la plantilla del boletín informativo. |
| Añada una versión de texto sin formato para el envío de varias partes. | Se ha incorporado un nuevo widget en las propiedades de la página para extraer fácilmente una versión de texto sin formato del contenido de la página. Puede utilizarlo como punto de partida para la versión final de texto sin formato. |

## Plantillas y ejemplos de newsletter de Campaign {#campaign-newsletter-templates-and-examples}

AEM viene con varias plantillas y componentes listos para usar para que cree boletines de campaña. Puede utilizar estas plantillas y componentes para crear sus boletines personalizados.

### Plantillas {#templates}

Para ofrecer una base sólida y ampliar la variedad de posibilidades de flujo de contenido, hay tres tipos de plantillas ligeramente diferentes disponibles de forma predeterminada. Puede utilizar fácilmente estos tres tipos para crear un boletín informativo personalizado.

Todos tienen un **encabezado**, a **pie de página**, y a **cuerpo** sección. Debajo de la sección del cuerpo, cada plantilla difiere en **diseño de columna** (una, dos o tres columnas).

![Variantes de posibles boletines](assets/chlimage_1-69.png)

### Componentes {#components}

Actualmente hay [siete componentes disponibles para usar en plantillas de campaña](/help/sites-authoring/adobe-campaign-components.md). Todos estos componentes se basan en el lenguaje de marcado de Adobe **HTL**.

| **Nombre del componente** | **Ruta del componente** |
|---|---|
| Encabezado | /libs/mcm/campaign/components/heading |
| Imagen | /libs/mcm/campaign/components/image |
| Texto y personalización | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| Vínculo | /libs/mcm/campaign/components/reference |
| Plantilla de imagen de Dynamic Media Classic (anteriormente Scene7) | /libs/mcm/campaign/s7image |
| Referencia de destino | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>Estos componentes están optimizados para el contenido del correo; es decir, se adhieren a las prácticas recomendadas descritas en este documento. El uso de otros componentes listos para usar generalmente infringe estas reglas.

Estos componentes se describen en detalle en [Componentes de Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md).
