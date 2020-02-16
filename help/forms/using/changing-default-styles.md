---
title: Cambio de los estilos predeterminados de los formularios HTML5
seo-title: Cambio de los estilos predeterminados de los formularios HTML5
description: El estilo de los formularios HTML5 se basa en CSS. Puede cambiar los estilos predeterminados del formulario.
seo-description: El estilo de los formularios HTML5 se basa en CSS. Puede cambiar los estilos predeterminados del formulario.
uuid: 5e23237d-42d8-4d29-b79e-4dc276ef65ff
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 582b0fe8-a92b-4a1d-b859-57f13f53d0d8
docset: aem65
translation-type: tm+mt
source-git-commit: 19299fb5fc764d0e71c0ea3a5ec2286183dd6861

---


# Cambio de los estilos predeterminados de los formularios HTML5{#changing-default-styles-of-html-forms}

Los formularios HTML5 se procesan con funciones HTML5 y el estilo del formulario procesado se realiza con CSS. El aspecto predeterminado de los formularios HTML5 es similar al de su representación en PDF. Los desarrolladores pueden utilizar CSS personalizada para cambiar el aspecto predeterminado de los formularios HTML5.

Este artículo proporciona información paso a paso para cambiar el estilo de un formulario HTML5 y el artículo [Introducción a los estilos](/help/forms/using/css-styles.md) contiene información detallada sobre diversos aspectos del estilo de los formularios HTML5. Asegúrese de leer Introducción a los artículos de estilos antes de realizar los pasos mencionados en este artículo.

Las dos imágenes siguientes muestran la diferencia entre los estilos predeterminados y personalizados.

![images-002-small](assets/pictures-002-small.png)

## Estilo de los formularios {#style-your-forms}

1. **Elija un perfil para agregar estilos personalizados**

   Acceda a la interfaz CRX DE en la URL: **https://&lt;server>:&lt;port>/crx/de** y cree un perfil o elija un perfil existente. Para obtener información sobre cómo crear un perfil, consulte [Creación de un perfil nuevo](/help/forms/using/custom-profile.md)

1. **Creación de una hoja de estilo CSS para aplicar estilo a los formularios HTML5**

   Vaya a la carpeta en la que ha creado el procesador de perfiles y cree un archivo de hoja de estilo CSS. Los pasos a seguir son

   1. Haga clic con el botón derecho en la carpeta y seleccione **crear** > **crear archivo** en el menú

   1. En el cuadro de diálogo Crear archivo, introduzca el nombre de la hoja de estilo. Asegúrese de utilizar la extensión .css (por ejemplo, stylesheet.css)
   1. En el panel de navegación, abra el archivo CSS que ha creado.
   1. Defina las clases CSS de los componentes a los que desea aplicar estilo y agregue estilos en dichas clases.
   Para saber qué clases CSS crear para un componente concreto en los formularios HTML5, consulte [Introducción a los estilos](/help/forms/using/css-styles.md).

1. **Incluir la hoja de estilo en el procesador de perfiles**

   Abra la página Procesador de perfiles (archivo jsp) en CRX DE e incluya el archivo CSS en la página que hay justo debajo de la biblioteca de cliente XFA. Siga estos pasos para incluir el archivo CSS en el perfil.

   1. Busque la línea siguiente en la página del procesador:

      &lt;cq:includeClientLib categories=&quot;xfaforms.profile&quot; />

   1. Inserte lo siguiente debajo de la línea anterior para incluir la hoja de estilo:

      &lt;link href=&quot;/path/to/stylesheet&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot;/>

   1. Guarde el archivo.

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
