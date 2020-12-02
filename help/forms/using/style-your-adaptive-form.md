---
title: 'Estilo del formulario adaptable '
seo-title: 'Estilo del formulario adaptable '
description: 'Aprenda a crear un tema personalizado, a diseñar componentes individuales y a utilizar fuentes web en un tema '
seo-description: 'Aprenda a crear un tema personalizado, a diseñar componentes individuales y a utilizar fuentes web en un tema '
page-status-flag: de-activated
uuid: ffb2cc22-baaf-4525-a2e3-29f39271c670
topic-tags: introduction
discoiquuid: 655303a4-99bb-4ba3-9d50-a178f5edcf85
translation-type: tm+mt
source-git-commit: 263a25b70fe4a3e7de65b47f07932d2e5f3d0197
workflow-type: tm+mt
source-wordcount: '2057'
ht-degree: 8%

---


# Defina el estilo del formulario adaptable {#do-not-publish-style-your-adaptive-form}

Aprenda a crear un tema personalizado, a diseñar componentes individuales y a utilizar fuentes web en un tema

![](do-not-localize/08-style_your_adaptiveformmain.png)

Este tutorial es un paso en la serie [Crear su primer formulario adaptable](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). Se recomienda seguir la serie en secuencia cronológica para comprender, realizar y demostrar el caso de uso completo del tutorial.

## Acerca del tutorial {#about-the-tutorial}

Puede utilizar temáticas para proporcionar un aspecto y un estilo únicos a un formulario adaptable. Puede aplicar temáticas predeterminadas con el editor de formularios adaptables o crear temáticas personalizadas propias. AEM [!DNL Forms] proporciona un [editor de temas](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html) para crear temáticas personalizadas. Un solo tema puede proporcionar un aspecto diferente al mismo formulario adaptable que se abre en un dispositivo móvil, tablet o escritorio. No es necesario tener conocimientos previos de CSS o LESS para utilizar el editor de temas, pero se desea.

Al final del tutorial, aprenderá a:

* Aplicar un tema predefinido a un formulario adaptable
* Creación de un tema para un formulario adaptable mediante el editor de temas
* Estilo de componentes individuales
* Sección de primas: Uso de fuentes web en un tema personalizado

El formulario tendrá un aspecto similar al siguiente una vez que complete el tutorial:

![Formulario con un tema personalizado](assets/styled-adaptive-form.png)

## Antes de comenzar {#before-you-start}

Descargue las imágenes de estilo de encabezado y logotipo que se muestran a continuación en el equipo local. El encabezado del formulario adaptable `shipping-address-add-update-form` utiliza el estilo de encabezado y las imágenes de logotipo. La imagen de estilo de encabezado aparece en la parte derecha del encabezado.

[Obtener archivo](assets/header-style.png)

[Obtener archivo](assets/logo-1.png)

## Paso 1: Aplicar un tema al formulario adaptable {#step-apply-a-theme-to-your-adaptive-form}

El editor de formularios adaptables proporciona varias temáticas listas para usar. Si tiene previsto no utilizar un estilo personalizado en el formulario adaptable, también puede publicar los formularios adaptables con un tema incorporado. Las temáticas son independientes de los formularios adaptables. Puede aplicar el mismo tema a varios formularios adaptables. Para aplicar un tema a un formulario adaptable:

1. Abra el formulario adaptable para editarlo.

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. Abrir propiedades de **[!UICONTROL contenedor de formulario adaptable]**. En el navegador de propiedades, vaya a **[!UICONTROL Basic]** > **[!UICONTROL Tema del formulario adaptable]**. El campo **[!UICONTROL Tema del formulario adaptable]** lista todas las temáticas predeterminadas y personalizadas. De forma predeterminada, se aplica el tema Lienzo.
1. Seleccione un tema en el campo **[!UICONTROL Tema del formulario adaptable]**. Por ejemplo, **tema de Encuesta**. Toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para aplicar el tema seleccionado.

   ![Formulario adaptable con el tema predeterminado](assets/default-adaptive-form.png)

   **Figura:Formulario** *adaptable con el tema predeterminado*

   ![Formulario adaptable con el tema de Encuesta](assets/adaptive-form-with-survey-theme.png)

   **Figura:Formulario** *adaptable con el tema de Encuesta*

## Paso 2: Actualice el formulario adaptable {#step-update-your-adaptive-form}

El diseño que se muestra arriba requiere cambios en el texto del marcador de posición y en el logotipo del formulario adaptable existente. Realice los siguientes pasos para realizar los cambios necesarios:

1. Cambie el logotipo y el texto existentes del encabezado. Para eliminar el logotipo:

   1. Abra el formulario en el editor de formularios.

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. Toque la imagen del logotipo en el componente [!UICONTROL header] y toque ![cmppr](assets/cmppr.png) **[!UICONTROL properties]**. En la propiedad [!UICONTROL image], toque X para eliminar la imagen del logotipo existente.
   1. Toque **[!UICONTROL upload]**, seleccione el archivo logo.png y toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para guardar los cambios. La imagen se descargó en la sección [Antes de inicio](/help/forms/using/style-your-adaptive-form.md#before-you-start).
   1. Toque texto de encabezado, `We.Retail` y toque ![aem_6_3_edit](assets/aem_6_3_edit.png) **[!UICONTROL edit]**. Cambie el texto del encabezado a `we retail`. Aplicar formato de negrita solo a `we`en `we retail`.

      ![we-Retail-logo-text](assets/we-retail-logo-text.png)

1. Elimine el título y añada texto de marcador de posición:

   1. Toque el campo ID de cliente y toque ![cmppr](assets/cmppr.png) propiedades.
   1. Copie el contenido del campo **[!UICONTROL Título]** en el campo **[!UICONTROL Texto del marcador de posición]**.
   1. Elimine el contenido del campo **[!UICONTROL Título]** y toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
   1. Repita los tres pasos anteriores para todos los cuadros de texto, cuadros numéricos y campos de correo electrónico del formulario.

      ![update-adaptive-form](assets/updated-adaptive-form.png)

## Paso 3: Crear un tema personalizado para el formulario adaptable {#step-create-a-custom-theme-for-your-adaptive-form}

Puede utilizar [editor de temas](/help/forms/using/themes.md) para crear temáticas personalizadas. El editor de temas es un poderoso editor WYSIWYG. Es un método visual para aplicar CSS a varios componentes de un formulario adaptable. Proporciona controles más precisos para aplicar estilo a los componentes y paneles de un formulario adaptable.

Un tema es una entidad independiente como los formularios adaptables. Contiene estilos (CSS) para los componentes y paneles de un formulario adaptable. Los estilos incluyen propiedades CSS como colores de fondo, colores de estado, transparencia, alineación y tamaño. Al aplicar un tema, el estilo especificado se aplica a los componentes correspondientes de un formulario adaptable.

En este tutorial, aplicará estilo al encabezado y al pie de página, a los componentes numéricos y de texto, al componente de datos adjuntos y a los botones. Inicios con la creación de un tema:

### Crear un tema {#create-a-theme}

1. Inicie sesión en la instancia de creación de AEM y vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Temáticas]**. La dirección URL predeterminada es [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes).
1. Toque **[!UICONTROL Crear]** y seleccione **[!UICONTROL Tema]**. Aparece la página [!UICONTROL Crear tema] con los campos necesarios para crear un tema. Los campos **[!UICONTROL Título]** y **[!UICONTROL Nombre]** son obligatorios:

   * **Título:** especifique un título del tema. Por ejemplo, **Tema global.** El título le ayuda a identificar el tema a partir de la lista de temáticas.
   * **Nombre:** especifique el nombre del tema. Por ejemplo, **Tema global.** En el repositorio se crea un nodo con el nombre especificado. Al escribir un título con inicio, se genera automáticamente el valor del campo de nombre. Puede cambiar el valor sugerido. El campo de nombre solo puede incluir caracteres alfanuméricos, guiones y guiones bajos. Todas las entradas no válidas se reemplazan con un guión.

1. Toque **[!UICONTROL Crear]**. Se crea un tema y un cuadro de diálogo para abrir el formulario y editarlo. Toque **[!UICONTROL Abrir]** para abrir el tema recién creado en una pestaña nueva. El tema se abre en el editor de temas. Para aplicar estilo, el editor de temas utiliza un formulario adaptable incorporado que se incluye con AEM [!DNL Forms].

   Para obtener información sobre el uso de la IU del editor de temas, consulte [Acerca del editor de temas](/help/forms/using/themes.md#aboutthethemeeditor).

1. Toque **[!UICONTROL Opciones de tema]** ![opciones de tema](assets/theme-options.png) > **[!UICONTROL Configurar]**. En el campo **[!UICONTROL Formulario de Previsualización]**, seleccione el formulario adaptable **Shipping-address-add-update-form**, toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) y toque **[!UICONTROL Guardar]**. Ahora, el editor de temas está configurado para utilizar su propio formulario adaptable en lugar del formulario adaptable predeterminado. Toque **[!UICONTROL Cancelar]** para volver al editor de temas.

   ![custom-topic](assets/custom-theme.png)

   **Figura:Editor de** *temas con el formulario adaptable Shipping-address-add-update-form*

   ![create-a-topic](assets/create-a-theme.png)

   **Figura:Formulario** *adaptable con el formulario predeterminado*

### Encabezado y pie de página de estilo {#style-header-and-footer}

El encabezado y el pie de página proporcionan un aspecto coherente y distintivo a un formulario adaptable. Generalmente, el encabezado contiene el logotipo y el nombre de la organización, el pie de página contiene información de copyright y estas permanecen idénticas en varias formas de una organización. Para aplicar estilo al encabezado y al pie de página del formulario adaptable Shipping-address-add-update-form:

1. Vaya a la opción **[!UICONTROL Encabezado]** > **[!UICONTROL Texto]** en el panel Selectores. El panel Selectores se encuentra a la izquierda del editor de temas. Si el panel no está visible, toque ![alternar panel lateral](assets/toggle-side-panel.png) Alternar panel lateral.

1. Defina las siguientes propiedades en el acordeón **[!UICONTROL Texto]** y toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propiedad | Value |
   |---|---|
   | Familia de fuentes | Arial |
   | Color de fuente | FFFFFF |
   | Tamaño de fuente | 54 px |

1. Toque la utilidad [!UICONTROL encabezado] y toque **[!UICONTROL Encabezado]**. Las opciones para aplicar estilo al widget de encabezado aparecen a la izquierda. Expanda el acordeón **[!UICONTROL Dimension y posición]**, establezca la **[!UICONTROL altura]** en `120px` y toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. Expanda el acordeón **[!UICONTROL Fondo]** del widget de encabezado, establezca el **[!UICONTROL Color de fondo]** en `F6921E.`

   Pase el ratón sobre **[!UICONTROL Imagen y degradado]** > **[!UICONTROL + Añadir]**, toque **[!UICONTROL Imagen]**. Defina las siguientes propiedades y toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propiedad | Valor |
   |---|---|
   | image | Cargue header-style.png. La imagen se descargó en la sección [Antes de inicio](/help/forms/using/style-your-adaptive-form.md#before-you-start). |
   | Posición | Inferior Derecha |
   | Mosaico | No repetir |

1. En el editor de temas, toque el logotipo en el encabezado y toque **[!UICONTROL Logotipo de encabezado]**. Expanda el acordeón Dimension y posición, defina las siguientes propiedades y toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>imagen</b></td> 
      <td><b>Valor</b></td> 
     </tr> 
     <tr> 
      <td>imagen</td> 
      <td> 
       <ul> 
        <li>Superior: 1,5 rem</li> 
        <li>Inferior: -35 px</li> 
        <li>Izquierda: 1rem<strong><br /> </strong></li> 
       </ul> <p><strong>Sugerencia:</strong> Toque el icono del  <img src="assets/link.png"> vínculo para proporcionar un valor diferente a cada campo.<br /> </p> </td> 
     </tr> 
     <tr> 
      <td>Altura</td> 
      <td>4,75 rem</td> 
     </tr> 
    </tbody> 
   </table>

1. Toque el widget de pie de página y toque **[!UICONTROL Pie de página]**. Expanda el acordeón **[!UICONTROL Fondo]**, establezca el **[!UICONTROL Color de fondo]** en `F6921E` y toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

### Aplique estilo al componente de captura de datos y aplique un fondo al formulario adaptable {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

Puede utilizar varios componentes en un formulario adaptable para capturar datos. Por ejemplo, cuadro de texto y cuadro numérico. Puede proporcionar un estilo idéntico a todos los componentes de captura de datos o a un estilo independiente para cada componente. En este tutorial, se aplica un estilo idéntico a los cuadros numéricos (ID del cliente, código postal) y los cuadros de texto (ID del cliente, nombre, dirección de envío, estado, correo electrónico). Para aplicar estilo a los componentes de captura de datos:

1. Toque el campo **[!UICONTROL ID del cliente]** y toque la opción **[!UICONTROL Utilidad del campo]**. Defina las siguientes propiedades y toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Acordeón</b></td> 
      <td><b>Propiedad</b></td> 
      <td><b>Valor</b></td> 
     </tr> 
     <tr> 
      <td>Borde</td> 
      <td>Color del borde</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>Borde</td> 
      <td>Radio de borde </td> 
      <td> 
       <ul> 
        <li>Superior: 7px<br /> </li> 
        <li>Derecha: 7px<br /> </li> 
        <li>Inferior: 7px<br /> </li> 
        <li>Izquierda: 7px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Texto</td> 
      <td>Familia de fuentes</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>Texto</td> 
      <td>Color de fuente</td> 
      <td>939598<br /> </td> 
     </tr> 
     <tr> 
      <td>Texto</td> 
      <td>Tamaño de fuente</td> 
      <td>18 px</td> 
     </tr> 
     <tr> 
      <td>Dimension y posición</td> 
      <td>Anchura</td> 
      <td>60%</td> 
     </tr> 
     <tr> 
      <td>Dimension y posición</td> 
      <td>imagen</td> 
      <td> 
       <ul> 
        <li>Izquierda: 10 rem</li> 
       </ul> </td> 
     </tr> 
    </tbody> 
    </table>

1. Toque en el área vacía encima del campo **[!UICONTROL ID del cliente]** y toque **[!UICONTROL Contenedor del panel interactivo]**. Establezca el **[!UICONTROL Fondo]** > **[!UICONTROL Color de fondo]** en F1F2F2. Toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   ![](do-not-localize/responsive-panel-container.png)

### Estilo de los botones {#style-the-buttons}

Puede utilizar un tema personalizado para aplicar un estilo idéntico a todos los botones del formulario adaptable y [estilo en línea](/help/forms/using/inline-style-adaptive-forms.md) para aplicar un estilo a un botón específico. Para aplicar estilo a los botones:

1. Toque el botón **[!UICONTROL Enviar]** y toque la opción **[!UICONTROL Botón]**. Defina las siguientes propiedades y toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Acordeón</b></td> 
      <td><b>Propiedad</b></td> 
      <td><b>Valor</b></td> 
     </tr> 
     <tr> 
      <td>Fondo</td> 
      <td>Color de fondo</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>Borde<br /> </td> 
      <td>Color del borde</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>Borde</td> 
      <td>Radio de borde </td> 
      <td> 
       <ul> 
        <li>Superior: 7px<br /> </li> 
        <li>Derecha: 7px<br /> </li> 
        <li>Inferior: 7px<br /> </li> 
        <li>Izquierda: 7 px</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Texto<br /> </td> 
      <td>Familia de fuentes</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>Texto</td> 
      <td>Color de fuente</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>Texto</td> 
      <td>Tamaño de fuente</td> 
      <td>18 px</td> 
     </tr> 
    </tbody> 
   </table>

1. [Aplique el tema](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form) personalizado, Tema global, al formulario adaptable. Si el estilo no se refleja en el formulario adaptable, limpie la caché del explorador e inténtelo de nuevo.

   ![style-data-capture-components](assets/style-data-capture-components.png)

## Paso 4: Estilo de componentes individuales {#step-style-individual-components}

Algunos estilos solo se aplican a un componente específico. Estos componentes están diseñados en el editor de formularios adaptables.

1. Abra el formulario adaptable para editarlo. [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. En la barra superior, seleccione la opción **[!UICONTROL Estilo]**.

   ![style-option](assets/style-option.png)

1. Toque el botón **[!UICONTROL Adjuntar]** y toque el icono ![aem_6_3_edit](assets/aem_6_3_edit.png). Defina las siguientes propiedades en el acordeón **[!UICONTROL Dimension y posición]**:

   | Propiedad | Valor |
   |---|---|
   | Flotante | Izquierda |
   | Anchura | 10% |

1. Toque la opción **[!UICONTROL prueba de dirección aprobada por el gobierno]** y toque el icono ![aem_6_3_edit](assets/aem_6_3_edit.png). Establezca las siguientes propiedades:

   <table> 
    <tbody> 
     <tr> 
      <td><b>Acordeón</b></td> 
      <td><b>Propiedad</b></td> 
      <td><b>Valor</b></td> 
     </tr> 
     <tr> 
      <td>Dimensiones y posición</td> 
      <td>Flotante</td> 
      <td>Izquierda</td> 
     </tr> 
     <tr> 
      <td>Dimensiones y posición</td> 
      <td>Anchura</td> 
      <td>73 %</td> 
     </tr> 
     <tr> 
      <td>Dimensiones y posición</td> 
      <td>Espacio</td> 
      <td> 
       <ul> 
        <li>Izquierda: 10 px</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Dimensiones y posición</td> 
      <td>Altura</td> 
      <td>40 px</td> 
     </tr> 
     <tr> 
      <td>Dimensiones y posición<br /> </td> 
      <td>imagen</td> 
      <td><br /> 
       <ul> 
        <li>Derecha: 2 rem</li> 
        <li>Izquierda: 10 rem </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Fondo</td> 
      <td>Color de fondo</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>Borde</td> 
      <td>Anchura de borde</td> 
      <td>1 px</td> 
     </tr> 
     <tr> 
      <td>Borde</td> 
      <td>Estilo de borde</td> 
      <td>Sólido</td> 
     </tr> 
     <tr> 
      <td>Borde</td> 
      <td>Color del borde</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>Borde</td> 
      <td>Radio de borde</td> 
      <td>7 px</td> 
     </tr> 
     <tr> 
      <td>Texto</td> 
      <td>Familia de fuentes</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>Texto</td> 
      <td>Color de fuente</td> 
      <td>BCBEC0</td> 
     </tr> 
     <tr> 
      <td>Texto</td> 
      <td>Tamaño de fuente</td> 
      <td>18 px</td> 
     </tr> 
     <tr> 
      <td>Texto</td> 
      <td>Altura de la línea</td> 
      <td>2</td> 
     </tr> 
     </tr> 
    </tbody> 
   </table>

1. Toque el botón **[!UICONTROL Enviar]** y toque el icono ![aem_6_3_edit](assets/aem_6_3_edit.png). Establezca las siguientes propiedades:

   <table> 
    <tbody> 
     <tr> 
      <td><b>Acordeón</b></td> 
      <td><b>Propiedad</b></td> 
      <td><b>Valor</b></td> 
     </tr> 
     <tr> 
      <td>Dimension y posición</td> 
      <td>Flotante</td> 
      <td>Derecha</td> 
     </tr> 
     <tr> 
      <td>Dimension y posición</td> 
      <td>imagen</td> 
      <td> 
       <ul> 
        <li>Superior: 5 rem</li> 
        <li>Derecha: 14 rem</li> 
        <li>Inferior: 20 px</li> 
        <li>Izquierda: 20 px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Fondo</td> 
      <td>Color de fondo</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>Borde</td> 
      <td>Color del borde</td> 
      <td>F6921E</td> 
     </tr> 
    </tbody> 
   </table>

   ![styled-adaptive-form-1](assets/styled-adaptive-form-1.png)

## Paso 5: Sección de primas: Uso de fuentes web en un tema personalizado {#step-bonus-section-using-web-fonts-in-a-custom-theme}

Puede utilizar varias fuentes para diseñar un formulario adaptable. Es posible que todos los dispositivos en los que se visualiza el formulario adaptable no tengan las fuentes utilizadas para diseñar el formulario adaptable. Puede utilizar un servicio de fuentes web para proporcionar las fuentes necesarias al dispositivo destinatario.

[!DNL Adobe Fonts] es un servicio de fuentes web. Puede configurar y utilizar el servicio con formularios adaptables. Para utilizar [!DNL Adobe Fonts] en un formulario adaptable:

>[!NOTE]
>
>![typekit-to-adobe-](assets/typekit-to-adobe-fonts.png) [!DNL Typekit] fontsis ahora se denomina Adobe Fonts y se incluye con Creative Cloud y otras suscripciones. [Más información](https://fonts.adobe.com/).

1. Cree una cuenta [Adobe Fonts](https://typekit.com/), cree un kit, agregue la fuente Myriad Pro al kit, publique el kit y obtenga el ID del kit. Es necesario utilizar [!DNL Adobe Fonts] (fuentes Web) en un formulario adaptable.
1. En el servidor AEM [!DNL Forms], navegue a ![adobeexperience emanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Herramientas]** ![martillo](assets/hammer.png) > **[!UICONTROL Adobe Fonts]**. Ahora, abra una carpeta de configuración. Si ya hay una configuración disponible, haga clic en el botón **[!UICONTROL Crear]** para crear una nueva instancia.

   En el cuadro de diálogo Crear configuración, especifique un **Título** para la configuración y haga clic en **[!UICONTROL Crear]**. Se le redirige a la página de configuración. En el cuadro de diálogo [!UICONTROL Editar componente] que aparece, proporcione el **ID del kit** y haga clic en **[!UICONTROL Aceptar]**.

1. Configure el tema para utilizar la configuración [!DNL Adobe Fonts]. En la instancia de autor, abra **[!UICONTROL Tema global]** en el editor de temas. En el editor de temas, vaya a **[!UICONTROL Opciones de tema]** ![opciones de tema](assets/theme-options.png) > **[!UICONTROL Configurar]**. En el campo **[!UICONTROL Configuración de Adobe Fonts]**, seleccione el kit y haga clic en **[!UICONTROL Guardar]**.

   Las fuentes agregadas a **[!UICONTROL Adobe Fonts]** están disponibles para su selección en el acordeón **[!UICONTROL Texto]** de todos los componentes.

