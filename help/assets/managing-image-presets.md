---
title: Administración de ajustes preestablecidos de imagen de Dynamic Media
description: Comprenda los ajustes preestablecidos de imagen de Dynamic Media y aprenda a crear, modificar y administrar ajustes preestablecidos de imagen.
uuid: 3e9a7af6-bf49-4cff-b516-0a3ee9765391
mini-toc-levels: 3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: cc1111c4-6e24-4570-9ac7-97c25cf24ede
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/image-presets
feature: Image Presets
role: User, Admin
exl-id: 556b99fe-91c3-441f-ba81-22cb8c10ef7f
source-git-commit: 0d3bcdaa10d16c292aa0dd60254302d30fd700d6
workflow-type: tm+mt
source-wordcount: '3839'
ht-degree: 8%

---

# Administración de ajustes preestablecidos de imagen de Dynamic Media{#managing-image-presets}

Los ajustes preestablecidos de imagen permiten a Adobe Experience Manager Assets entregar de forma dinámica imágenes con tamaños diferentes, en formatos diferentes o con otras propiedades de imagen generadas de forma dinámica. Cada ajuste preestablecido de imagen representa una colección predefinida de comandos de tamaño y diseño para mostrar las imágenes. Al crear un ajuste preestablecido de imagen, se elige un tamaño para la entrega de imágenes. También puede elegir los comandos de formato para que el aspecto de la imagen se optimice cuando la imagen se entregue para su visualización.

Los administradores pueden crear ajustes preestablecidos para exportar recursos. Los usuarios pueden elegir un ajuste preestablecido cuando exportan imágenes, lo que también permite cambiar el formato de las imágenes según las especificaciones del administrador.

También puede crear ajustes preestablecidos de imagen que sean interactivos. Si aplica un ajuste preestablecido de imagen adaptable a sus recursos, estos cambian según el dispositivo o el tamaño de pantalla en el que se visualicen. Puede configurar ajustes preestablecidos de imagen para que utilicen CMYK en el espacio de color, además de RGB o gris.

En esta sección se describe cómo crear, modificar y administrar los ajustes preestablecidos de imagen en general. Puede aplicar un ajuste preestablecido de imagen a una imagen cada vez que la previsualice. Consulte [Aplicación de ajustes preestablecidos de imagen](/help/assets/image-presets.md).

>[!NOTE]
>
>Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes y utilizan la inteligencia en el último milisegundo de envío para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión de red o del explorador. Consulte [Imágenes inteligentes](/help/assets/imaging-faq.md) para obtener más información.

## Explicación de los ajustes preestablecidos de imagen de Dynamic Media {#understanding-image-presets}

Al igual que una macro, un ajuste preestablecido de imagen es una colección predefinida de comandos de tamaño y formato guardados con un nombre. Para comprender cómo funcionan los ajustes preestablecidos de imagen, supongamos que el sitio web requiere que cada imagen de producto aparezca en diferentes tamaños, formatos diferentes y tasas de compresión para la entrega por equipos de escritorio y dispositivos móviles.

>[!NOTE]
>
>En el modo Dynamic Media - Scene7, los ajustes preestablecidos de imagen solo son compatibles con los recursos de imagen.

Puede crear dos ajustes preestablecidos de imagen: uno con 500 x 500 píxeles para la versión de escritorio y 150 x 150 píxeles para la versión móvil. Se crean dos ajustes preestablecidos de imagen, uno llamado `Enlarge` para mostrar imágenes a 500 x 500 píxeles y una llamada `Thumbnail` para mostrar las imágenes a 150 x 150 píxeles. Para enviar imágenes en la variable `Enlarge` y `Thumbnail` tamaño, el Experience Manager busca la definición del ajuste preestablecido de ampliación de imagen y el ajuste preestablecido de imagen en miniatura. A continuación, el Experience Manager genera dinámicamente una imagen con las especificaciones de tamaño y formato de cada ajuste preestablecido de imagen.

Las imágenes con un tamaño reducido cuando se entregan de forma dinámica pueden perder nitidez y detalle. Por este motivo, cada ajuste preestablecido de imagen contiene controles de formato para optimizar una imagen cuando se entrega a un tamaño concreto. Estos controles garantizan que las imágenes sean nítidas y claras cuando se envían al sitio web o a la aplicación.

Los administradores pueden crear ajustes preestablecidos de imagen. Para crear un ajuste preestablecido de imagen, puede empezar desde cero o desde uno existente y guardarlo con un nuevo nombre.

## Administración de ajustes preestablecidos de imagen de Dynamic Media {#managing-image-presets-1}

Para administrar los ajustes preestablecidos de imagen en Experience Manager, toque o haga clic en el logotipo del Experience Manager para acceder a la consola de navegación global y, a continuación, toque o haga clic en el icono Herramientas y navegue hasta **[!UICONTROL Assets > Ajustes preestablecidos de imagen]**.

![6_5_tools-assets-imagepresets](assets/6_5_tools-assets-imagepresets.png)

>[!NOTE]
>
>Los ajustes preestablecidos de imagen que cree también estarán disponibles como representaciones dinámicas cuando realice la vista previa o el envío de recursos.
>
>En *Dynamic Media: modo Scene7*, usted *not* es necesario publicar ajustes preestablecidos de imagen, ya que los ajustes preestablecidos de imagen se publican automáticamente.
>
>En *Dynamic Media: modo híbrido*, debe publicar manualmente los ajustes preestablecidos de imagen.
>
>Consulte [Publicar ajustes preestablecidos de imagen](#publishing-image-presets).

>[!NOTE]
>
>El sistema muestra varias representaciones al seleccionar **[!UICONTROL Representaciones]** en la Vista de detalles de un recurso. Puede aumentar o disminuir el número de ajustes preestablecidos de imagen que se muestran. Consulte [Aumento del número de ajustes preestablecidos de imagen que se muestran](#increasing-or-decreasing-the-number-of-image-presets-that-display).

### Formatos de archivo de SmartCultivos, Adobe Illustrator (AI), Postscript (EPS) y PDF {#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats}

>[!NOTE]
>
>Este tema solo se aplica a Dynamic Media - Modo híbrido.

Si tiene intención de admitir la ingesta de archivos AI, EPS y PDF para poder generar representaciones dinámicas de estos formatos de archivo, revise la siguiente información antes de crear ajustes preestablecidos de imagen.

El formato de archivo de Adobe Illustrator es una variante de PDF. Las principales diferencias, en el contexto de Experience Manager Assets, son las siguientes:

* Los documentos de Adobe Illustrator constan de una sola página con varias capas. Cada capa se extrae como un subrecurso PNG bajo el recurso principal de Illustrator.
* Los documentos del PDF constan de una o más páginas. Cada página se extrae como un subrecurso de PDF de página única en el documento principal de PDF de varias páginas.

Los subrecursos los crea el `Create Sub Asset process` dentro del `DAM Update Asset` flujo de trabajo. Para ver este componente de proceso en el flujo de trabajo, pulse **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]** > **[!UICONTROL Recurso de actualización DAM]** > **[!UICONTROL Editar]**.

Consulte también [Visualización de páginas de un archivo de varias páginas](/help/assets/managing-linked-subassets.md#view-pages-of-a-multi-page-file).

Puede ver los subrecursos o las páginas al abrir el recurso, pulsar el menú Contenido y seleccionar **[!UICONTROL Subrecursos]** o **[!UICONTROL Páginas]**. Los subactivos son activos reales. Es decir, las páginas del PDF se extraen mediante la variable `Create Sub Asset` componente de flujo de trabajo. A continuación, se almacenan como `page1.pdf`, `page2.pdf`, etc., debajo del recurso principal. Una vez almacenados, la variable `DAM Update Asset` flujo de trabajo los procesa.

Para utilizar Dynamic Media para obtener una vista previa y generar representaciones dinámicas para archivos AI, EPS o PDF, se requieren los siguientes pasos de procesamiento:

1. En el `DAM Update Asset` flujo de trabajo, la variable `Rasterize PDF/AI Image Preview Rendition` el componente de proceso rasteriza la primera página del recurso original (con la resolución configurada) en un `cqdam.preview.png` representación.

1. La variable `cqdam.preview.png` a continuación, la representación se optimiza en un PTIFF mediante la función `Dynamic Media Process Image Assets` componente de proceso dentro del flujo de trabajo.

>[!NOTE]
>
>En el [!UICONTROL Recurso de actualización DAM] flujo de trabajo, la variable **[!UICONTROL Miniaturas de EPS]** genera miniaturas para los archivos EPS.

#### Propiedades de metadatos de recursos de PDF/IA/EPS {#pdf-ai-eps-asset-metadata-properties}

| **Propiedad Metadata** | **Descripción** |
|---|---|
| `dam:Physicalwidthininches` | Ancho del documento en pulgadas. |
| `dam:Physicalheightininches` | Altura del documento en pulgadas. |

Puede acceder a `Rasterize PDF/AI Image Preview Rendition` opciones de componentes de proceso mediante `DAM Update Asset` flujo de trabajo.

Toque en Adobe Experience Manager, en la esquina superior izquierda, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**. En la página Modelos de flujo de trabajo , seleccione **[!UICONTROL Recurso de actualización DAM]** y, a continuación, en la barra de herramientas, pulse **[!UICONTROL Editar]**. En el [!UICONTROL Recurso de actualización DAM] página de flujo de trabajo, toque dos veces el botón `Rasterize PDF/AI Image Preview Rendition` procesar componente para abrir su cuadro de diálogo Propiedades del paso.

#### Rasterizar PDF/opciones de representación de vista previa de imágenes de IA {#rasterize-pdf-ai-image-preview-rendition-options}

![Argumentos para rasterizar el PDF o el flujo de trabajo de IA](assets/rasterize_pdf_ai_image_preview.png)

Argumentos para rasterizar el PDF o el flujo de trabajo de IA

<table>
 <tbody>
  <tr>
   <td><strong>Argumento de proceso</strong></td>
   <td><strong>Configuración predeterminada</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Tipos MIME</td>
   <td><p>application/pdf</p> <p>application/postscript</p> <p>aplicación/ilustrador<br /> </p> </td>
   <td>Lista de tipos de mime de documento que se consideran documentos PDF o Illustrator.<br /> </td>
  </tr>
  <tr>
   <td>Ancho máximo</td>
   <td>2048</td>
   <td>Ancho máximo de la representación de vista previa generada, en píxeles.<br /> </td>
  </tr>
  <tr>
   <td>Alto máximo</td>
   <td>2048</td>
   <td>Altura máxima de la representación de vista previa generada, en píxeles.<br /> </td>
  </tr>
  <tr>
   <td>Resolución</td>
   <td>72</td>
   <td>Resolución para rasterizar la primera página, en ppi (píxeles por pulgada).</td>
  </tr>
 </tbody>
</table>

Con los argumentos de proceso predeterminados, la primera página de un documento PDF/AI se rasteriza a 72 ppi y la imagen de vista previa generada tiene un tamaño de 2048 x 2048 píxeles. Para una implementación típica, es posible que desee aumentar la resolución a un mínimo de 150 ppi o más. Por ejemplo, un documento de tamaño de letra de EE. UU. a 300 ppi requiere una anchura y una altura máximas de 2550 x 3300 píxeles, respectivamente.

La anchura máxima y la altura máxima limitan la resolución a la que se debe rasterizar. Por ejemplo, si los máximos no cambian y la resolución se establece en 300 ppi, se rasteriza un documento de carta de EE. UU. a 186 ppi. Es decir, el documento es de 1581 x 2046 píxeles.

La variable `Rasterize PDF/AI Image Preview Rendition` el componente de proceso tiene un máximo definido para garantizar que no cree imágenes demasiado grandes en la memoria. Estas imágenes grandes pueden desbordarse la memoria proporcionada a la JVM (máquina virtual Java™). Se debe tener cuidado de proporcionar a la JVM suficiente memoria para administrar el número configurado de flujos de trabajo paralelos, con cada uno con el potencial de crear una imagen al tamaño máximo configurado.

### Formato del archivo InDesign (INDD) {#indesign-indd-file-format}

Si tiene intención de admitir la ingesta de archivos INDD para poder generar una representación dinámica de este formato de archivo, es posible que desee revisar la siguiente información antes de crear ajustes preestablecidos de imagen.

Para los archivos de InDesign, los subrecursos se extraen solo si Adobe InDesign Server está integrado con Experience Manager. Los recursos a los que se hace referencia están vinculados según sus metadatos. No se requiere InDesign Server para la vinculación. Sin embargo, los recursos a los que se hace referencia deben estar presentes en Experience Manager antes de que se procesen los archivos de InDesign para que se creen los vínculos entre los archivos de InDesign y los recursos a los que se hace referencia.

Consulte [Integración de Experience Manager Assets con InDesign Server](/help/assets/indesign.md).

El componente de proceso Extracción de medios en la variable `DAM Update Asset` El flujo de trabajo ejecuta varios scripts extend preconfigurados para procesar archivos de InDesign.

![Las rutas de ExtendScript en los argumentos del proceso de Extracción de medios](assets/6_5_mediaextractionprocess.png)

Las rutas de ExtendScript en los argumentos del componente de proceso Extracción de medios en la [!UICONTROL Recurso de actualización DAM] flujo de trabajo.

La integración de Dynamic Media utiliza las siguientes secuencias de comandos:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre de ExtendScript</strong></td>
   <td><strong>Predeterminado</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>ThumbnailExport.jsx</td>
   <td>Sí</td>
   <td>Genera 300 ppp <code>thumbnail.jpg</code> representación optimizada y convertida en una representación PTIFF por <code>Dynamic Media Process Image Assets</code> componente de proceso.<br /> </td>
  </tr>
  <tr>
   <td>JPEGPagesExport.jsx</td>
   <td>Sí</td>
   <td>Genera un subrecurso de JPEG de 300 PPI para cada página. El subrecurso de JPEG es un recurso real almacenado en el recurso de InDesign. También está optimizado y se convierte en un PTIFF mediante la función <code>DAM Update Asset</code> flujo de trabajo.<br /> </td>
  </tr>
  <tr>
   <td>PDFPagesExport.jsx</td>
   <td>No</td>
   <td>Genera un subrecurso de PDF para cada página. El subrecurso del PDF se procesa como se describió anteriormente. Como el PDF solo contiene una página, no se generan subrecursos.<br /> </td>
  </tr>
 </tbody>
</table>

## Configuración del tamaño de la miniatura de la imagen {#configuring-image-thumbnail-size}

Puede configurar el tamaño de las miniaturas configurando esos ajustes en la variable **[!UICONTROL Recurso de actualización DAM]** flujo de trabajo. Hay dos pasos en el flujo de trabajo donde puede configurar el tamaño de las miniaturas de los recursos de imagen. Aunque (**[!UICONTROL Recursos de imagen de proceso de Dynamic Media]**) se utiliza para los recursos de imagen dinámica y (**[!UICONTROL Miniaturas de proceso]**) es para la generación de miniaturas estáticas o cuando todos los demás procesos no pueden generar miniaturas, *both* debe tener la misma configuración.

Con el paso **[!UICONTROL Recursos de imagen de proceso de Dynamic Media]**, el servidor de imágenes genera miniaturas y esta configuración es independiente de la configuración aplicada al paso **[!UICONTROL Procesar miniaturas]**. La generación de miniaturas a través del paso **[!UICONTROL Miniaturas de proceso]** es la forma más lenta y con mayor consumo de memoria para crear miniaturas.

El tamaño de las miniaturas se define en el siguiente formato: **[!UICONTROL width:height:center]**, por ejemplo `80:80:false`. La anchura y la altura determinan el tamaño en píxeles de la miniatura. El valor central es false o true y, si se establece en true, indica que la imagen en miniatura tiene exactamente el tamaño indicado en la configuración. Si la imagen cambiada de tamaño es más pequeña, se centra dentro de la miniatura.

>[!NOTE]
>
>* Los tamaños de miniatura para archivos EPS se configuran en la variable **[!UICONTROL Miniaturas de EPS]** en la **[!UICONTROL Argumentos]** en Miniaturas.
>
>* Los tamaños de miniatura para vídeos se configuran en la variable **[!UICONTROL Miniaturas de FFmpeg]** en la **[!UICONTROL Proceso]** ficha **[!UICONTROL Argumentos]**.
>


**Para configurar el tamaño de las miniaturas de la imagen:**

1. Toque **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]** > **[!UICONTROL Recurso de actualización DAM]** > **[!UICONTROL Editar]**.
1. Toque . **[!UICONTROL Recursos de imagen de proceso de Dynamic Media]** y pulse o haga clic en **[!UICONTROL Miniaturas]** pestaña . Cambie el tamaño de la miniatura, según sea necesario, y pulse **[!UICONTROL Aceptar]**.

   ![6_5_dynamicmediaprocessimageassets-thumbnailstab](assets/6_5_dynamicmediaprocessimageassets-thumbnailstab.png)

1. Pulse el paso **[!UICONTROL Procesar miniaturas]** y, a continuación, pulse la pestaña **[!UICONTROL Miniaturas]**. Cambie el tamaño de la miniatura, según sea necesario, y pulse **[!UICONTROL Aceptar]**.

   >[!NOTE]
   >
   >Los valores del argumento de miniaturas del paso **[!UICONTROL Miniaturas de proceso]** deben coincidir con el argumento de miniaturas del paso **[!UICONTROL Recursos de imagen de proceso de Dynamic Media]**.

1. Toque **[!UICONTROL Guardar]** para guardar los cambios en el flujo de trabajo.

### Aumento o disminución del número de ajustes preestablecidos de imagen de Dynamic Media que se muestran {#increasing-or-decreasing-the-number-of-image-presets-that-display}

Los ajustes preestablecidos de imagen que cree estarán disponibles como representaciones dinámicas cuando se previsualizan los recursos. El Experience Manager muestra varias representaciones dinámicas al ver un recurso desde **[!UICONTROL Vista de detalles > Representaciones]**. Puede aumentar o reducir el límite de representaciones que se muestran.

**Aumente o disminuya el número de ajustes preestablecidos de imagen de Dynamic Media que se muestran:**

1. Vaya al CRXDE Lite ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Vaya al nodo de lista de ajustes preestablecidos de imagen en `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist`

   ![Increase_decreasethenumberofimagepresetsthatdisplay](assets/increase_decreasethenumberofimagepresetsthatdisplay.png)

1. En la propiedad **[!UICONTROL limit]**, cambie el **[!UICONTROL valor]**, que se establece en 15 de forma predeterminada, por el número deseado.
1. Vaya a la fuente de datos del ajuste preestablecido de imagen en `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist/datasource`

   ![chlimage_1-495](assets/chlimage_1-495.png)

1. En la propiedad limit , cambie el número por el número deseado, por ejemplo `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. Toque **[!UICONTROL Guardar todo]**.

## Creación de un ajuste preestablecido de imagen de Dynamic Media {#creating-image-presets}

La creación de un ajuste preestablecido de imagen de Dynamic Media permite aplicar esta configuración a cualquier imagen al obtener una vista previa o publicar.

>[!NOTE]
>
>Si utiliza Internet Explorer 9, la creación de un ajuste preestablecido no aparece en la lista de ajustes preestablecidos inmediatamente después de guardarlo. Para solucionar este problema, deshabilite la caché para IE9.

Si tiene intención de admitir la ingesta de archivos AI, PDF y EPS para poder generar una representación dinámica de estos formatos de archivo, revise la siguiente información antes de crear ajustes preestablecidos de imagen.
Consulte [Formatos de archivo Adobe Illustrator (AI), Postscript (EPS) y PDF](#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats).

Si tiene intención de admitir la ingesta de archivos INDD para poder generar una representación dinámica de este formato de archivo, es posible que desee revisar la siguiente información antes de crear ajustes preestablecidos de imagen.
Consulte [Formato del archivo InDesign (INDD)](#indesign-indd-file-format).

>[!NOTE]
>
>Para crear ajustes preestablecidos de imagen de Dynamic Media, debe tener privilegios de administrador como administrador del Experience Manager o administrador del Admin Console.

**Para crear un ajuste preestablecido de imagen de Dynamic Media:**

1. En el Experience Manager, pulse el logotipo del Experience Manager para acceder a la consola de navegación global y, a continuación, pulse **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Ajustes preestablecidos de imagen]**.
1. Haga clic en **[!UICONTROL Crear]**. La variable **[!UICONTROL Editar ajuste preestablecido de imagen]** se abre.

   ![chlimage_1-496](assets/chlimage_1-496.png)

   >[!NOTE]
   >
   >Para que este ajuste preestablecido de imagen sea interactivo, borre los valores de los campos de **[!UICONTROL anchura]** y **[!UICONTROL altura]** y déjelos en blanco.

1. Introduzca valores en las pestañas **[!UICONTROL Básico]** y **[!UICONTROL Avanzadas]** según corresponda, incluido un nombre. Las opciones se describen en [Opciones de ajustes preestablecidos de imagen](#image-preset-options). Los ajustes preestablecidos aparecen en el panel izquierdo y se pueden utilizar sobre la marcha con otros recursos.

   ![6_5_imagepreset-edit](assets/6_5_imagepreset-edit.png)

1. Haga clic en **[!UICONTROL Guardar]**.

## Creación de un ajuste preestablecido de imagen interactivo {#creating-a-responsive-image-preset}

Para crear un ajuste preestablecido de imagen interactivo, realice los pasos indicados en [Creación de ajustes preestablecidos de imagen](#creating-image-presets). Al introducir la altura y la anchura en la variable **[!UICONTROL Editar ajuste preestablecido de imagen]** , borre los valores y déjelos en blanco.

Dejarlos en blanco indica al Experience Manager que este ajuste preestablecido de imagen es interactivo. Puede ajustar los demás valores según corresponda.



>[!NOTE]
>
>Para ver la **[!UICONTROL URL]** y **[!UICONTROL RESS]** al aplicar un ajuste preestablecido de imagen a un recurso, este debe publicarse.
>
>![chlimage_1-79](assets/chlimage_1-498.png)
>
>En el modo Dynamic Media - Scene7, los ajustes preestablecidos de imagen y los recursos de imagen se publican automáticamente.
>
>En Dynamic Media: modo híbrido, debe publicar manualmente ajustes preestablecidos de imagen y recursos de imagen.

### Opciones de ajustes preestablecidos de imagen {#image-preset-options}

Cuando crea o edita ajustes preestablecidos de imagen, tiene las opciones descritas en esta sección. Además, Adobe recomienda estas opciones de &quot;prácticas recomendadas&quot; para comenzar:

* **[!UICONTROL Formato]** (pestaña **[!UICONTROL Básico]**): Seleccione **[!UICONTROL JPEG]** u otro formato que cumpla sus necesidades. Todos los navegadores web admiten el formato de imagen JPEG; ofrece un buen equilibrio entre los tamaños de archivos pequeños y la calidad de imagen. Sin embargo, las imágenes en formato JPEG utilizan un esquema de compresión con pérdidas que puede introducir artefactos de imagen no deseados si el ajuste de compresión es demasiado bajo. Por este motivo, Adobe recomienda establecer la calidad de compresión en 75. Este ajuste ofrece un buen equilibrio entre la calidad de imagen y el tamaño de archivo pequeño.

* **[!UICONTROL Activar enfoque simple]**: No seleccione **[!UICONTROL Activar enfoque simple]** (este filtro de enfoque ofrece menos control que la configuración de máscara de enfoque).

* **[!UICONTROL Enfoque: Modo de remuestreo]** - Seleccionar **[!UICONTROL Sharp2]**.

#### Opciones de ficha básicas {#basic-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>Campo</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td><strong>Nombre</strong></td>
   <td>Escriba un nombre descriptivo sin espacios en blanco. Incluya la especificación de tamaño de imagen en el nombre para que los usuarios puedan identificar este ajuste preestablecido de imagen.</td>
  </tr>
  <tr>
   <td><strong>Anchura y altura</strong></td>
   <td>Introduzca en píxeles el tamaño con el que se entrega la imagen. La anchura y la altura deben ser superiores a 0 píxeles. Si alguno de los valores es 0, no se crea ningún ajuste preestablecido. Si ambos valores están en blanco, se crea un ajuste preestablecido de imagen interactivo.</td>
  </tr>
  <tr>
   <td><strong>Formato</strong></td>
   <td><p>Elija un formato en el menú .</p> <p>Elección <strong>JPEG</strong> ofrece las siguientes opciones adicionales:</p>
    <ul>
     <li><strong>Calidad</strong> - Controla el nivel de compresión del JPEG. Esta configuración afecta tanto al tamaño del archivo como a la calidad de la imagen. La escala de calidad del JPEG es de 1 a 100. La escala está visible al arrastrar el control deslizante.</li>
     <li><strong>Habilitar disminución de resolución de crominancia del JPG</strong> - Como el ojo es menos sensible a la información de color de alta frecuencia que la luminancia de alta frecuencia, las imágenes JPEG dividen la información de la imagen en componentes de luminancia y color. Cuando se comprime una imagen de JPEG, el componente de luminancia se deja a resolución completa, mientras que los componentes de color se reducen al obtener una media de los grupos de píxeles. La disminución de la resolución de muestreo reduce el volumen de datos en una mitad o un tercio, sin afectar casi a la calidad percibida. La disminución de resolución no es aplicable a las imágenes en escala de grises. Esta técnica reduce la cantidad de compresión útil para imágenes con alto contraste (por ejemplo, imágenes con texto superpuesto).</li>
    </ul>
    <div>
      Elección
     <strong>GIF</strong> o
     <strong>GIF con alfa</strong> proporciona estos
     <strong>Cuantificación de color del GIF</strong> opciones:
    </div>
    <ul>
     <li><strong>Tipo </strong>- Seleccionar <strong>Adaptable</strong> (predeterminado), <strong>Web</strong>o <strong>Macintosh</strong>. Si selecciona <strong>GIF con alfa</strong>, la opción Macintosh no está disponible.</li>
     <li><strong>Diámetro</strong> - Seleccionar <strong>Difusión</strong> o <strong>Off</strong>.</li>
     <li><strong>Número de colores </strong>- Escriba un número del 2 al 256.</li>
     <li><strong>Lista de colores</strong> - Introduzca una lista separada por comas. Por ejemplo, para blanco, gris y negro, escriba <code>000000,888888,ffffff</code>.</li>
    </ul>
    <div>
      Elección
     <strong>PDF</strong>,
     <strong>TIFF</strong>o
     <strong>TIFF con alfa</strong> proporciona esta opción adicional:
    </div>
    <ul>
     <li><strong>Compresión</strong> - Seleccione un algoritmo de compresión. Las opciones de algoritmo para el PDF son <strong>Ninguna</strong>, <strong>Zip</strong>y <strong>Jpeg</strong>; para TIFF, las opciones son <strong>Ninguna</strong>, <strong>LZW</strong>, <strong>Jpeg</strong>y <strong>Zip</strong>; y para el TIFF con Alpha son <strong>Ninguna</strong>, <strong>LZW</strong>y <strong>Zip</strong>.</li>
    </ul> <p>Elección <strong>PNG</strong>, <strong>PNG con Alpha,</strong> o <strong>EPS</strong> no proporciona opciones adicionales.</p> </td>
  </tr>
  <tr>
   <td><strong>Enfoque</strong></td>
   <td>Seleccione el <strong>Activar enfoque simple</strong> para aplicar un filtro de enfoque básico a la imagen después de que se haya realizado todo el escalado. El enfoque puede ayudar a compensar el desenfoque que puede producirse al mostrar una imagen con un tamaño diferente. </td>
  </tr>
 </tbody>
</table>

#### Opciones de ficha avanzadas {#advanced-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>Campo</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td><strong>Espacio de color</strong></td>
   <td>Select <strong>RGB, CMYK,</strong> o <strong>Escala de grises</strong> para el espacio de color.</td>
  </tr>
  <tr>
   <td><strong>Perfil de color</strong></td>
   <td>Seleccione el perfil de espacio de color de salida al que debe convertirse el recurso si es diferente del perfil de trabajo.</td>
  </tr>
  <tr>
   <td><strong>Procesar intención</strong></td>
   <td>Puede anular la interpretación predeterminada. Las intenciones de renderización determinan lo que sucede con los colores que no se pueden reproducir en el perfil de color de destino (fuera de gama). Se ignora la interpretación de intenciones si no es compatible con el perfil ICC.
    <ul>
     <li>Select <strong>Percepción</strong> para comprimir la gama total de un espacio de color en otro espacio de color cuando uno o más colores de la imagen original están fuera de la gama del espacio de color de destino.</li>
     <li>Select <strong>Colorimétrico relativo</strong> cuando un color del espacio de color actual está fuera de la gama en el espacio de color de destino. Y, desea asignarlo al color más cercano posible dentro de la gama del espacio de color de destino sin afectar a ningún otro color. </li>
     <li>Select <strong>Saturación</strong> si desea reproducir la saturación de color de la imagen original al convertirla en el espacio de color de destino. </li>
     <li>Select <strong>Colorimétrico absoluto</strong> para hacer coincidir colores exactamente sin ajuste de punto blanco o punto negro que pueda alterar el brillo de la imagen.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Compensación de punto negro</strong></td>
   <td>Seleccione esta opción si el perfil de salida es compatible con esta función. La compensación de puntos negros se ignora si no es compatible con el perfil ICC especificado.</td>
  </tr>
  <tr>
   <td><strong>Distorsión</strong></td>
   <td>Seleccione esta opción para evitar o reducir los artefactos de bandas de color. </td>
  </tr>
  <tr>
   <td><strong>Tipo de perfeccionamiento</strong></td>
   <td><p>Select <strong>Ninguna</strong>, <strong>Enfoque</strong>o <strong>Máscara de enfoque</strong>. </p>
    <ul>
     <li>Select <strong>Ninguna</strong> si desea desactivar el enfoque.</li>
     <li>Select <strong>Enfoque</strong> si desea aplicar un filtro de enfoque básico a la imagen después de que se haya realizado todo el escalado. El enfoque puede ayudar a compensar el desenfoque que puede producirse al mostrar una imagen con un tamaño diferente. </li>
     <li>Select<strong> Máscara de enfoque</strong> si desea ajustar un efecto de filtro de enfoque en la imagen final con disminución de resolución. Puede controlar la intensidad del efecto, el radio del efecto (medido en píxeles) y un umbral de contraste que se ignora. Este efecto utiliza las mismas opciones que el filtro “Máscara de enfoque” de Photoshop.</li>
    </ul> <p>En <strong>Máscara de enfoque</strong>, tiene las siguientes opciones:</p>
    <ul>
     <li><strong>Importe</strong> - Controla la cantidad de contraste aplicada a los píxeles de borde. El valor de número real predeterminado es 1,0. Para imágenes de alta resolución, puede aumentarlo hasta 5,0. Piense en Cantidad como una medida de la intensidad del filtro.</li>
     <li><strong>Radio</strong> - Determina el número de píxeles que rodean los píxeles de borde que afectan al enfoque. Para imágenes de alta resolución, introduzca un número real de 1 a 2. Un valor bajo afilará solo los píxeles de borde; un valor alto afila una banda más amplia de píxeles. El valor correcto depende del tamaño de la imagen.</li>
     <li><strong>Umbral</strong> - Determina el rango de contraste que se debe ignorar cuando se aplica el filtro de máscara de enfoque. En otras palabras, esta opción determina la diferencia entre los píxeles enfocados y el área circundante antes de que se consideren píxeles de borde y se agranden. Para evitar introducir ruido, experimente con valores enteros entre 2 y 20. </li>
     <li><strong>Aplicar a</strong> - Determina si el desenfoque se aplica a cada color o brillo.</li>
    </ul>
    <div>
      El enfoque se describe en
     <a href="https://experienceleague.adobe.com/docs/experience-manager-65/assets/sharpening_images.pdf">Enfoque de imágenes</a>.
    </div> </td>
  </tr>
  <tr>
   <td><strong>Modo de remuestreo</strong></td>
   <td>Seleccione un <strong>Modo de remuestreo</strong> . Estas opciones afinan la imagen cuando se reduce su resolución:
    <ul>
     <li><strong>Bi-Lineal</strong> - El método de remuestreo más rápido. Se pueden apreciar algunos artefactos de aliasing.</li>
     <li><strong>Bi-cúbico</strong> - Aumenta el uso de la CPU pero produce imágenes más nítidas con artefactos de alias menos visibles.</li>
     <li><strong>Sharp2</strong> - Puede producir resultados ligeramente más nítidos que el Bi-Cubic, pero a un costo de CPU aún mayor.</li>
     <li><strong>Bi-Sharp</strong> - Selecciona el reampliador predeterminado de Photoshop para reducir el tamaño de la imagen, que se denomina <strong>parachoques bicúbicos</strong> en Adobe Photoshop.</li>
     <li><strong>Cada color</strong> y <strong>Brillo</strong> - cada método puede basarse en el color o el brillo. De forma predeterminada <strong>Cada color</strong> está seleccionado.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Resolución de impresión</strong></td>
   <td>Seleccione una resolución para imprimir esta imagen; El valor predeterminado es 72 píxeles.</td>
  </tr>
  <tr>
   <td><strong>Modificador de imagen</strong></td>
   <td><p>Más allá de la configuración de imagen común disponible en la interfaz de usuario, Dynamic Media admite numerosas modificaciones de imagen avanzadas que se pueden especificar en la <strong>Modificadores de imagen</strong> campo . Estos parámetros se definen en la variable <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html#image-serving-api">Referencia de comandos del protocolo de servidor de imágenes</a>.</p> <p>Importante: No se admite la siguiente funcionalidad enumerada en la API:</p>
    <ul>
     <li>Plantillas básicas y comandos de renderización de texto: <code>text= textAngle= textAttr= textFlowPath= textFlowXPath= textPath=</code> y <code>textPs=</code></li>
     <li>Comandos de localización: <code>locale=</code> y <code>req=xlate</code></li>
     <li><code>req=set</code> no está disponible para uso general.</li>
     <li><code>req=mbrset</code></li>
     <li><code>req=saveToFile</code></li>
     <li><code>req=targets</code></li>
     <li><code>template=</code></li>
     <li>Servicios Dynamic Media no principales: SVG, procesamiento de imágenes e impresión virtual</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Definición de opciones de ajustes preestablecidos de imagen con modificadores de imagen {#defining-image-preset-options-with-image-modifiers}

Además de las opciones disponibles en las pestañas Básico y Avanzado , puede definir modificadores de imagen para ofrecerle más opciones al definir ajustes preestablecidos de imagen. El procesamiento de imágenes se basa en la API de renderización de imágenes que se define en detalle en la variable [Referencia de protocolo HTTP](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html#image-serving-api).

A continuación se presentan algunos ejemplos básicos de lo que puede hacer con los modificadores de imagen.

>[!NOTE]
>
>Algunos modificadores de imagen [no se puede usar en Experience Manager](#advanced-tab-options).

* [op_invert](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-invert.html#image-serving-api) - Invierte cada componente de color para un efecto de imagen negativo.

   ```xml
   &op_invert=1
   ```

   ![6_5_imagepreset-edit-invert](assets/6_5_imagepreset-edit-invert.png)

* [op_blur](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-blur.html#image-serving-api) - Aplica un filtro de desenfoque a la imagen.

   ```xml
   &op_blur=7
   ```

   ![6_5_imagepreset-edit-blur](assets/6_5_imagepreset-edit-blur.png)

* Comandos combinados: op_blur y op-invert

   ```xml
   &op_invert=1&op_blur=7
   ```

   ![chlimage_1-80](assets/chlimage_1-501.png)

* [op_bright](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-brightness.html#image-serving-api) - Reduce o aumenta el brillo.

   ```xml
   &op_brightness=58
   ```

   ![6_5_imagepreset-edit-bright](assets/6_5_imagepreset-edit-brightness.png)

* [opac](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-opac.html#image-serving-api) - Ajusta la opacidad de la imagen. Permite reducir la opacidad en primer plano.

   ```xml
   opac=29
   ```

   ![6_5_imagepreset-edit-opacity](assets/6_5_imagepreset-edit-opacity.png)

## Edición de ajustes preestablecidos de imagen {#modifying-image-presets}

1. En el Experience Manager, pulse el logotipo del Experience Manager para acceder a la consola de navegación global y, a continuación, pulse **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Ajustes preestablecidos de imagen]**.

   ![6_5_imagepreset-editpreset](assets/6_5_imagepreset-editpreset.png)

1. Seleccione un ajuste preestablecido y haga clic en **[!UICONTROL Editar]**. La variable **[!UICONTROL Editar ajuste preestablecido de imagen]** se abre.
1. Realice cambios y haga clic en **[!UICONTROL Guardar]** para guardar los cambios o **[!UICONTROL Cancelar]** para cancelar los cambios.

## Publicación de ajustes preestablecidos de imagen de Dynamic Media {#publishing-image-presets}

Si está ejecutando Dynamic Media en modo híbrido, debe publicar manualmente los ajustes preestablecidos de imagen.

(Si está ejecutando Dynamic Media en modo Scene7, los ajustes preestablecidos de imagen se publican automáticamente; no es necesario que complete estos pasos).

**Para publicar ajustes preestablecidos de imagen en Dynamic Media: modo híbrido:**

1. En el Experience Manager, pulse o haga clic en el logotipo del Experience Manager para acceder a la consola de navegación global, pulse o haga clic en el icono Herramientas y vaya a **[!UICONTROL Recursos]** > **[!UICONTROL Ajustes preestablecidos de imagen]**.
1. Seleccione el ajuste preestablecido de imagen o varios ajustes preestablecidos de imagen de la lista de ajustes preestablecidos de imagen y toque o haga clic en **[!UICONTROL Publicación]**.
1. Una vez publicado el ajuste preestablecido de imagen, el estado cambia de no publicado a publicado.

   ![chlimage_1-81](assets/chlimage_1-505.png)

## Eliminación de ajustes preestablecidos de imagen de Dynamic Media {#deleting-image-presets}

1. En el Experience Manager, toque o haga clic en el logotipo del Experience Manager para acceder a la consola de navegación global.
1. Toque . **[!UICONTROL Herramientas]** y, a continuación, vaya a **[!UICONTROL Recursos]** > **[!UICONTROL Ajustes preestablecidos de imagen]**.
1. Seleccione un ajuste preestablecido y, a continuación, haga clic en **[!UICONTROL Eliminar]**. Dynamic Media confirma que desea eliminarlo. Toque **[!UICONTROL Eliminar]** para eliminar o tocar **[!UICONTROL Cancelar]** para cancelar.
