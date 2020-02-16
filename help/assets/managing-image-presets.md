---
title: Administración de ajustes preestablecidos de imagen de Dynamic Media
description: Obtenga información sobre los ajustes preestablecidos de imagen de Dynamic Media y aprenda a crear, modificar y administrar ajustes preestablecidos de imagen
uuid: 3e9a7af6-bf49-4cff-b516-0a3ee9765391
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: cc1111c4-6e24-4570-9ac7-97c25cf24ede
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/image-presets
translation-type: tm+mt
source-git-commit: 1d38c2bf5f4a00bfa5a12ddaefcab1898f81a6aa

---


# Administración de ajustes preestablecidos de imagen de Dynamic Media{#managing-image-presets}

Los ajustes preestablecidos de imagen permiten que Recursos AEM distribuya de forma dinámica imágenes de diferentes tamaños, formatos diferentes o con otras propiedades de imagen que se generan de forma dinámica. Cada ajuste preestablecido de imagen representa una colección predefinida de comandos de tamaño y diseño para mostrar las imágenes. Al crear un ajuste preestablecido de imagen, se elige un tamaño para la publicación de imágenes. También puede elegir comandos de formato para que el aspecto de la imagen se optimice cuando se distribuya para su visualización.

Los administradores pueden crear ajustes preestablecidos para exportar recursos. Los usuarios pueden elegir un ajuste preestablecido cuando exportan imágenes, lo que también cambia el formato de las imágenes según las especificaciones del administrador.

También puede crear ajustes preestablecidos de imagen adaptables. Si se aplica un ajuste preestablecido de imagen interactivo a los recursos, éstos cambian según el dispositivo o el tamaño de pantalla en el que se vean. Puede configurar los ajustes preestablecidos de imagen para que utilicen CMYK en el espacio de color además de RGB o Gris.

En esta sección se describe cómo crear, modificar y administrar, en general, los ajustes preestablecidos de imagen. Puede aplicar un ajuste preestablecido de imagen a una imagen cada vez que la previsualice. See [Applying Image Presets](/help/assets/image-presets.md).

>[!NOTE]
>
>Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes y utilizan la inteligencia en el último milisegundo de la publicación para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión de red o del navegador. Consulte Imágenes [inteligentes](/help/assets/imaging-faq.md) para obtener más información.

## Explicación de los ajustes preestablecidos de imagen de Dynamic Media {#understanding-image-presets}

Al igual que una macro, un ajuste preestablecido de imagen es una colección predefinida de comandos de tamaño y formato guardados con un nombre. Para comprender cómo funcionan los ajustes preestablecidos de imagen, supongamos que el sitio web requiere que cada imagen de producto aparezca en diferentes tamaños, formatos diferentes y tasas de compresión para la distribución móvil y de escritorio.

Puede crear dos ajustes preestablecidos de imagen: uno con 500 x 500 píxeles para la versión de escritorio y 150 x 150 píxeles para la versión móvil. Puede crear dos ajustes preestablecidos de imagen, uno llamado `Enlarge` para mostrar imágenes de 500 x 500 píxeles y otro llamado `Thumbnail` para mostrar imágenes de 150 x 150 píxeles. Para distribuir imágenes con el `Enlarge` mismo tamaño y `Thumbnail` tamaño, AEM busca la definición del ajuste preestablecido de imagen Ampliación y el ajuste preestablecido de imagen en miniatura. A continuación, AEM genera dinámicamente una imagen con las especificaciones de tamaño y formato de cada ajuste preestablecido de imagen.

Las imágenes con un tamaño reducido al distribuirse dinámicamente pueden perder nitidez y detalle. Por este motivo, cada ajuste preestablecido de imagen contiene controles de formato para optimizar una imagen cuando se distribuye con un tamaño concreto. Estos controles garantizan que las imágenes sean nítidas y claras cuando se envían al sitio web o a la aplicación.

Los administradores pueden crear ajustes preestablecidos de imagen. Para crear un ajuste preestablecido de imagen, puede empezar desde cero o desde uno existente y guardarlo con un nombre nuevo.

## Administración de ajustes preestablecidos de imagen de Dynamic Media {#managing-image-presets-1}

Para administrar los ajustes preestablecidos de imagen en AEM, toque o haga clic en el logotipo de AEM para acceder a la consola de navegación global y, a continuación, toque o haga clic en el icono Herramientas y vaya a **[!UICONTROL Recursos > Ajustes preestablecidos]** de imagen.

![6_5_tools-assets-imagepresets](assets/6_5_tools-assets-imagepresets.png)

>[!NOTE]
>
>Los ajustes preestablecidos de imagen que cree también estarán disponibles como representaciones dinámicas al obtener una vista previa o distribuir recursos.
>
>En el modo *Medios* dinámicos - Scene7, *no es necesario* publicar ajustes preestablecidos de imagen cuando los ajustes preestablecidos de imagen se publican automáticamente.
>
>En el modo *Medios* dinámicos: híbrido, es necesario publicar manualmente los ajustes preestablecidos de imagen.
>
>See [Publishing Image Presets.](#publishing-image-presets)

>[!NOTE]
>
>El sistema muestra una serie de representaciones al seleccionar **[!UICONTROL Representaciones]** en la vista de detalles de un recurso. Puede aumentar o disminuir el número de ajustes preestablecidos de imagen que se muestran. Consulte [Aumento del número de ajustes preestablecidos de imagen que se muestran](#increasingthenumberofimagepresetsthatdisplay).

### Formatos de archivo de Adobe Illustrator (AI), Postscript (EPS) y PDF {#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats}

Si desea admitir la ingestión de archivos AI, EPS y PDF para poder generar representaciones dinámicas de estos formatos de archivo, puede que desee revisar la siguiente información antes de crear ajustes preestablecidos de imagen.

El formato de archivo de Adobe Illustrator es una variante de PDF. Las principales diferencias, en el contexto de Recursos AEM, son las siguientes:

* Los documentos de Adobe Illustrator constan de una sola página con varias capas. Cada capa se extrae como un subrecurso PNG en el recurso principal de Illustrator.
* Los documentos PDF constan de una o varias páginas. Cada página se extrae como un subrecurso PDF de una sola página en el documento PDF principal de varias páginas.

Los subrecursos los crea el `Create Sub Asset process` componente dentro del flujo de trabajo general `DAM Update Asset` . Para ver este componente de proceso dentro del flujo de trabajo, toque **[!UICONTROL Herramientas > Flujo de trabajo > Modelos > Recurso de actualización de DAM > Editar]**.

Consulte también [Visualización de páginas de un archivo](/help/assets/managing-linked-subassets.md#view-pages-of-a-multi-page-file)de varias páginas.

Puede ver los subrecursos o las páginas al abrir el recurso, tocar el menú Contenido y seleccionar **[!UICONTROL Subrecursos]** o **[!UICONTROL Páginas]**. Los subactivos son activos reales. Es decir, las páginas PDF se extraen mediante el componente de `Create Sub Asset` flujo de trabajo. Después se almacenan como `page1.pdf`, `page2.pdf`, etc., debajo del recurso principal. Una vez almacenados, el `DAM Update Asset` flujo de trabajo los procesa.

Para utilizar Dynamic Media para obtener una vista previa y generar representaciones dinámicas para archivos AI, EPS o PDF, se requieren los siguientes pasos de procesamiento:

1. En el flujo de trabajo, el componente de `DAM Update Asset` proceso rasteriza la primera página del recurso original (con la resolución configurada) en una `Rasterize PDF/AI Image Preview Rendition` `cqdam.preview.png` representación.

1. A continuación, el componente de proceso del flujo de trabajo optimiza la `cqdam.preview.png` representación en un PTIFF mediante el componente de `Dynamic Media Process Image Assets` proceso.

>[!NOTE]
>
>En el flujo de trabajo de recursos de actualización de DAM, el paso de miniaturas **[!UICONTROL de]** EPS genera miniaturas para los archivos EPS.

#### Propiedades de metadatos de recursos PDF/AI/EPS {#pdf-ai-eps-asset-metadata-properties}

| **Propiedad Metadata** | **Descripción** |
|---|---|
| dam:Physicalwidthinpulgadas | Ancho del documento en pulgadas. |
| dam:Physicalheightinpulgadas | Altura del documento en pulgadas. |

Puede acceder a las opciones `Rasterize PDF/AI Image Preview Rendition` de componentes del proceso a través del `DAM Update Asset` flujo de trabajo.

Toque Adobe Experience Manager en la esquina superior izquierda y vaya a **[!UICONTROL Herramientas > Flujo de trabajo > Modelos]**. En la página Modelos de flujo de trabajo, seleccione **[!UICONTROL DAM Update Asset]** y, a continuación, en la barra de herramientas, toque **[!UICONTROL Editar]**. En la página de flujo de trabajo de recursos de actualización de DAM, toque dos veces el componente de `Rasterize PDF/AI Image Preview Rendition` proceso para abrir el cuadro de diálogo Propiedades de la etapa.

#### Rasterize PDF/AI Image Preview Rendition options {#rasterize-pdf-ai-image-preview-rendition-options}

![Argumentos para rasterizar el flujo de trabajo de archivos PDF o AI](assets/rasterize_pdf_ai_image_preview.png)

Argumentos para rasterizar el flujo de trabajo de archivos PDF o AI

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
   <td>Lista de los tipos MIME del documento que se consideran documentos PDF o de Illustrator.<br /> </td>
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
   <td>Resolución para rasterizar la primera página, en ppp (píxeles por pulgada).</td>
  </tr>
 </tbody>
</table>

Con los argumentos de proceso predeterminados, la primera página de un documento PDF/AI se rasteriza a 72 ppp y la imagen de vista previa generada tiene un tamaño de 2048 x 2048 píxeles. Para una implementación típica, puede aumentar la resolución a un mínimo de 150 ppp o más. Por ejemplo, un documento de tamaño de letra de EE. UU. a 300 ppp requiere una anchura y una altura máximas de 2550 x 3300 píxeles, respectivamente.

La anchura máxima y la altura máxima limitan la resolución en la que se rasterizará. Por ejemplo, si los máximos no cambian y la resolución se establece en 300 ppp, un documento de carta de EE. UU. se rasteriza a 186 ppp. Es decir, el documento tiene 1581 x 2046 píxeles.

El componente de `Rasterize PDF/AI Image Preview Rendition` proceso tiene un máximo definido para garantizar que no cree imágenes demasiado grandes en la memoria. Estas imágenes de gran tamaño pueden desbordar la memoria proporcionada a la JVM (Máquina virtual Java). Se debe tener cuidado de proporcionar al JVM suficiente memoria para administrar el número configurado de flujos de trabajo paralelos, y cada uno de ellos tiene la posibilidad de crear una imagen con el tamaño máximo configurado.

### Formato de archivo de InDesign (INDD) {#indesign-indd-file-format}

Si desea admitir la ingestión de archivos INDD para poder generar una representación dinámica de este formato de archivo, es posible que desee revisar la siguiente información antes de crear ajustes preestablecidos de imagen.

En el caso de los archivos de InDesign, los subrecursos solo se extraen si el servidor de Adobe InDesign está integrado con AEM. Los recursos a los que se hace referencia están vinculados según sus metadatos. InDesign Server no es necesario para la vinculación. Sin embargo, los recursos a los que se hace referencia deben estar presentes en AEM antes de que se procesen los archivos de InDesign para poder crear los vínculos entre los archivos de InDesign y los recursos a los que se hace referencia.

See [Integrating AEM Assets with InDesign Server](/help/assets/indesign.md).

El componente de proceso Extracción de medios del `DAM Update Asset` flujo de trabajo ejecuta varios scripts extend preconfigurados para procesar archivos de InDesign.

![Las rutas de ExtendScript en los argumentos del proceso de extracción de medios](assets/6_5_mediaextractionprocess.png)

Las rutas de ExtendScript en los argumentos del componente de proceso de extracción de medios en el flujo de trabajo de recursos de actualización de DAM.

La integración de Dynamic Media utiliza las siguientes secuencias de comandos:

<table>
 <tbody>
  <tr>
   <td><strong>Ampliar nombre de secuencia de comandos</strong></td>
   <td><strong>Predeterminado</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>ThumbnailExport.jsx</td>
   <td>Sí</td>
   <td>Genera una representación de 300 ppp <code>thumbnail.jpg</code> que se optimiza y se convierte en una representación PTIFF por componente <code>Dynamic Media Process Image Assets</code> de proceso.<br /> </td>
  </tr>
  <tr>
   <td>JPEGPagesExport.jsx</td>
   <td>Sí</td>
   <td>Genera un subrecurso JPEG de 300 ppp para cada página. El subrecurso JPEG es un recurso real almacenado en el recurso de InDesign. El flujo de trabajo también lo optimiza y lo convierte en un PTIFF <code>DAM Update Asset</code> .<br /> </td>
  </tr>
  <tr>
   <td>PDFPagesExport.jsx</td>
   <td>No</td>
   <td>Genera un subrecurso PDF para cada página. El subrecurso PDF se procesa como se ha descrito anteriormente. Dado que el PDF solo contiene una página, no se generan subrecursos.<br /> </td>
  </tr>
 </tbody>
</table>

## Configuración del tamaño de miniatura de la imagen {#configuring-image-thumbnail-size}

Puede configurar el tamaño de las miniaturas configurando dicha configuración en el flujo de trabajo de recursos **[!UICONTROL de actualización de]** DAM. Hay dos pasos en el flujo de trabajo donde puede configurar el tamaño de las miniaturas de los recursos de imagen. Aunque se utiliza uno (Recursos **[!UICONTROL de imagen de proceso de medios]** dinámicos) para recursos de imagen dinámicos y el otro (Miniaturas de **[!UICONTROL proceso]**) para la generación de miniaturas estáticas o cuando todos los demás procesos no pueden generar miniaturas, *ambos* deben tener la misma configuración.

Con el paso Recursos **[!UICONTROL de imagen de proceso de]** Dynamic Media, el servidor de imágenes genera miniaturas y esta configuración es independiente de la configuración aplicada al paso **[!UICONTROL Procesar miniaturas]** . La generación de miniaturas a través del paso Miniaturas **[!UICONTROL de]** proceso es la forma más lenta y con mayor consumo de memoria de crear miniaturas.

El tamaño de las miniaturas se define en el siguiente formato: **[!UICONTROL width:height:center]**, por ejemplo, *80:80:false*. La anchura y la altura determinan el tamaño en píxeles de la miniatura; el valor central es false o true y, si se define como true, indica que la imagen en miniatura tiene exactamente el tamaño indicado en la configuración. Si la imagen redimensionada es más pequeña, se centrará dentro de la miniatura.

>[!NOTE]
>
>* El tamaño de las miniaturas de los archivos EPS se configura en el paso de miniaturas **** EPS, en la ficha **[!UICONTROL Argumentos]** , en Miniaturas.
   >
   >
* El tamaño de las miniaturas de los vídeos se configura en el paso **[!UICONTROL Miniaturas]** FFmpeg, en la ficha **[!UICONTROL Proceso]** , en **[!UICONTROL Argumentos]**.
>



**Para configurar el tamaño** de miniatura de la imagen:

1. Toque **[!UICONTROL Herramientas > Flujo de trabajo > Modelos > Recurso de actualización de DAM > Editar]**.
1. Toque el paso Recursos **[!UICONTROL de imagen de proceso de medios]** dinámicos y toque o haga clic en la ficha **[!UICONTROL Miniaturas]** . Cambie el tamaño de la miniatura, según sea necesario, y toque **[!UICONTROL Aceptar]**.

   ![6_5_dynamicmediaprocessimageassets-thumbnailstab](assets/6_5_dynamicmediaprocessimageassets-thumbnailstab.png)

1. Toque el paso **[!UICONTROL Procesar miniaturas]** y, a continuación, toque la ficha **[!UICONTROL Miniaturas]** . Cambie el tamaño de la miniatura, según sea necesario, y toque **[!UICONTROL Aceptar]**.

   >[!NOTE]
   >
   >Los valores del argumento de miniaturas del paso Miniaturas **[!UICONTROL de]** proceso deben coincidir con el argumento de miniaturas del paso Recursos **[!UICONTROL de imagen de proceso de]** Dynamic Media.

1. Toque **[!UICONTROL Guardar]** para guardar los cambios en el flujo de trabajo.

### Aumento o disminución del número de ajustes preestablecidos de imagen de Dynamic Media que se muestran {#increasing-or-decreasing-the-number-of-image-presets-that-display}

Los ajustes preestablecidos de imagen que cree estarán disponibles como representaciones dinámicas al obtener una vista previa de los recursos. AEM muestra una gran variedad de representaciones dinámicas al visualizar recursos desde la vista de **[!UICONTROL detalles > Representaciones]**. Puede aumentar o reducir el límite de representaciones que se muestran.

**Para aumentar o reducir el número de ajustes preestablecidos de imagen de Dynamic Media que se muestran**:

1. Vaya a CRXDE Lite ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Vaya al nodo de lista de ajustes preestablecidos de imagen en `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist`

   ![Increase_decreasethenumberofimagepresetsthatdisplay](assets/increase_decreasethenumberofimagepresetsthatdisplay.png)

1. En la propiedad **[!UICONTROL limit]** , cambie el **[!UICONTROL valor]**, que se establece en 15 de forma predeterminada, por el número deseado.
1. Vaya al origen de datos de ajustes preestablecidos de imagen en `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist/datasource`

   ![chlimage_1-495](assets/chlimage_1-495.png)

1. En la propiedad limit, cambie el número al número deseado, por ejemplo `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. Toque **[!UICONTROL Guardar todo]**.

## Creación de un ajuste preestablecido de imagen de Dynamic Media {#creating-image-presets}

La creación de un ajuste preestablecido de imagen de Dynamic Media le permite aplicar estos ajustes a cualquier imagen al realizar una vista previa o publicar.

>[!NOTE]
>
>Si utiliza Internet Explorer 9, la creación de un ajuste preestablecido no aparece en la lista de ajustes preestablecidos inmediatamente después de guardarlo. Para solucionar este problema, deshabilite la caché para IE9.

Si desea admitir la ingestión de archivos AI, PDF y EPS para poder generar una representación dinámica de estos formatos de archivo, es posible que desee revisar la siguiente información antes de crear ajustes preestablecidos de imagen.
Consulte [Adobe Illustrator (AI), Postscript (EPS) y formatos](#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)de archivo PDF.

Si desea admitir la ingestión de archivos INDD para poder generar una representación dinámica de este formato de archivo, es posible que desee revisar la siguiente información antes de crear ajustes preestablecidos de imagen.
Consulte Formato [de archivo de InDesign (INDD)](#indesign-indd-file-format).

>[!NOTE]
>
>Para crear ajustes preestablecidos de imagen de Dynamic Media, debe tener privilegios de administrador como administrador de AEM o administrador de la Consola de administración.

**Para crear un ajuste preestablecido** de imagen de Dynamic Media:

1. En AEM, toque el logotipo de AEM para acceder a la consola de navegación global y, a continuación, toque **[!UICONTROL Herramientas > Recursos > Ajustes preestablecidos]** de imagen.
1. Haga clic en **[!UICONTROL Crear]**. Se abre la ventana **[!UICONTROL Editar ajuste preestablecido]** de imagen.

   ![chlimage_1-496](assets/chlimage_1-496.png)

   >[!NOTE]
   >
   >Para que este ajuste preestablecido de imagen sea interactivo, borre los valores de los campos de **[!UICONTROL anchura]** y **[!UICONTROL altura]** y déjelos en blanco.

1. Introduzca valores en las fichas **[!UICONTROL Básico]** y **[!UICONTROL Avanzado]** según corresponda, incluido un nombre. Las opciones se describen en Opciones [de ajustes preestablecidos](#image-preset-options)de imagen. Los ajustes preestablecidos aparecen en el panel izquierdo y se pueden utilizar sobre la marcha con otros recursos.

   ![6_5_imagepreset-edit](assets/6_5_imagepreset-edit.png)

1. Haga clic en **[!UICONTROL Guardar**.

## Creación de un ajuste preestablecido de imagen interactivo {#creating-a-responsive-image-preset}

Para crear un ajuste preestablecido de imagen interactivo, siga los pasos que se indican en [Creación de ajustes preestablecidos](#creating-image-presets)de imagen. Al introducir la altura y la anchura en la ventana **[!UICONTROL Editar ajuste preestablecido]** de imagen, borre los valores y déjelos en blanco.

Dejarlos en blanco indica a AEM que este ajuste preestablecido de imagen responde. Puede ajustar los demás valores según corresponda.



>[!NOTE]
>
>Para ver los botones **[!UICONTROL URL]** y **[!UICONTROL RESS]** al aplicar un ajuste preestablecido de imagen a un recurso, este debe publicarse.
>
>![chlimage_1-79](assets/chlimage_1-498.png)
>
>En el modo Dynamic Media - Scene7, los ajustes preestablecidos de imagen y los recursos de imagen se publican automáticamente.
>
>En el modo Dynamic Media: híbrido, debe publicar manualmente ajustes preestablecidos de imagen y recursos de imagen.

### Opciones de ajustes preestablecidos de imagen {#image-preset-options}

Al crear o editar ajustes preestablecidos de imagen, tiene las opciones descritas en esta sección. Además, Adobe recomienda estas opciones de &quot;prácticas recomendadas&quot; para comenzar:

* **[!Formato** UICONTROL (ficha **[!UICONTROL Básico]** ): seleccione **[!UICONTROL JPEG]** u otro formato que satisfaga sus necesidades. Todos los navegadores web admiten el formato de imagen JPEG; ofrece un buen equilibrio entre los tamaños de archivos pequeños y la calidad de imagen. Sin embargo, las imágenes en formato JPEG utilizan un esquema de compresión con pérdida que puede introducir artefactos de imagen no deseados si el ajuste de compresión es demasiado bajo. Por este motivo, Adobe recomienda establecer la calidad de compresión en 75. Este ajuste ofrece un buen equilibrio entre la calidad de imagen y el tamaño de archivo pequeño.

* **[!UICONTROL Activar enfoque]** simple: no seleccione **[!UICONTROL Activar enfoque]** simple (este filtro de enfoque ofrece menos control que la configuración de máscara de enfoque).

* **[!UICONTROL Enfoque: Modo]** de remuestreo: seleccione **[!UICONTROL Bicúbico]**.

#### Opciones de ficha básicas {#basic-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>Campo</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td><strong>Nombre</strong></td>
   <td>Introduzca un nombre descriptivo sin espacios en blanco. Incluya la especificación de tamaño de imagen en el nombre para ayudar a los usuarios a identificar este ajuste preestablecido de imagen.</td>
  </tr>
  <tr>
   <td><strong>Anchura y altura</strong></td>
   <td>Introduzca en píxeles el tamaño con el que se distribuye la imagen. La anchura y la altura deben ser mayores que 0 píxeles. Si alguno de los valores es 0, no se crea ningún ajuste preestablecido. Si ambos valores están en blanco, se crea un ajuste preestablecido de imagen interactivo.</td>
  </tr>
  <tr>
   <td><strong>Formato</strong></td>
   <td><p>Elija un formato en el menú.</p> <p>Al elegir <strong>JPEG</strong> se ofrecen las siguientes opciones adicionales:</p>
    <ul>
     <li><strong>Calidad</strong> : controla el nivel de compresión JPEG. Esta configuración afecta tanto al tamaño del archivo como a la calidad de la imagen. La escala de calidad JPEG es de 1 a 100. La escala está visible al arrastrar el control deslizante.</li>
     <li><strong>Activar disminución de resolución</strong> de crominancia JPG: como el ojo es menos sensible a la información de color de alta frecuencia que la luminancia de alta frecuencia, las imágenes JPEG dividen la información de la imagen en componentes de color y luminancia. Cuando se comprime una imagen JPEG, el componente de luminancia se deja con una resolución completa, mientras que los componentes de color se reducen al calcular el promedio de grupos de píxeles. La disminución de resolución reduce el volumen de datos en una mitad o en un tercio, sin afectar prácticamente a la calidad percibida. La disminución de resolución no se aplica a imágenes en escala de grises. Esta técnica reduce la cantidad de compresión útil para imágenes con alto contraste (por ejemplo, imágenes con texto superpuesto).</li>
    </ul>
    <div>
      Al elegir <strong>GIF</strong> o <strong>GIF con alfa</strong> se proporcionan las siguientes opciones adicionales de Cuantificación <strong>de color</strong> GIF:
    </div>
    <ul>
     <li><strong>Tipo </strong>- Seleccione <strong>Adaptable</strong> (opción predeterminada), <strong>Web</strong>o <strong>Macintosh</strong>. If you select <strong>GIF with Alpha</strong>, the Macintosh option is not available.</li>
     <li><strong>Tramado</strong> : seleccione <strong>Difusión</strong> o <strong>Desactivado</strong>.</li>
     <li><strong>Número de colores </strong>- Introduzca un número entre 2 y 256.</li>
     <li><strong>Lista</strong> de colores: introduzca una lista separada por comas. Por ejemplo, para blanco, gris y negro, introduzca 000000,888888,ffffff.</li>
    </ul>
    <div>
      La selección de <strong>PDF</strong>, <strong>TIFF</strong>o <strong>TIFF con alfa</strong> proporciona esta opción adicional:
    </div>
    <ul>
     <li><strong>Compresión</strong> : seleccione un algoritmo de compresión. Las opciones de algoritmo para PDF son <strong>None</strong>, <strong>Zip</strong>y <strong>Jpeg</strong>; TIFF son <strong>None</strong>, <strong>LZW</strong>, <strong>Jpeg</strong>y <strong>Zip</strong>; y para TIFF con Alpha son <strong>None</strong>, <strong>LZW</strong>y <strong>Zip</strong>.</li>
    </ul> <p>Al elegir <strong>PNG</strong>, <strong>PNG con alfa,</strong> o <strong>EPS</strong> no se proporcionan opciones adicionales.</p> </td>
  </tr>
  <tr>
   <td><strong>Enfoque</strong></td>
   <td>Select the <strong>Enable Simple Sharpening</strong> option to apply a basic sharpening filter to the image after all scaling takes place. Sharpening can help compensate for blurriness that can result when you display an image at a different size. </td>
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
   <td>Seleccione <strong>RGB,</strong> CMYK o <strong>Escala de grises</strong> para el espacio de color.</td>
  </tr>
  <tr>
   <td><strong>Perfil de color</strong></td>
   <td>Seleccione el perfil de espacio de color de salida al que se debe convertir el recurso si es diferente del perfil de trabajo.</td>
  </tr>
  <tr>
   <td><strong>Procesar intención</strong></td>
   <td>Puede anular la interpretación predeterminada. Las interpretaciones determinan lo que sucede con los colores que no se pueden reproducir en el perfil de color de destino (fuera de gama). La calidad de representación se omite si no es compatible con el perfil ICC.
    <ul>
     <li>Seleccione <strong>Perceptual</strong> para comprimir la gama total de un espacio de color en otro espacio de color cuando uno o varios colores de la imagen original se encuentren fuera de la gama del espacio de color de destino.</li>
     <li>Seleccione <strong>Relativa colorimétrica</strong> cuando un color del espacio de color actual esté fuera de gama en el espacio de color de destino y desee asignarlo al color más cercano posible dentro de la gama del espacio de color de destino sin afectar a ningún otro color. </li>
     <li>Seleccione <strong>Saturación</strong> para reproducir la saturación de color de la imagen original al convertirla en el espacio de color de destino. </li>
     <li>Seleccione Colorimétrica <strong>absoluta</strong> para que los colores coincidan exactamente sin ningún ajuste para puntos blancos o negros que pueda alterar el brillo de la imagen.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Compensación de punto negro</strong></td>
   <td>Seleccione esta opción si el perfil de salida admite esta función. La compensación de punto negro se ignora si no es compatible con el perfil ICC especificado.</td>
  </tr>
  <tr>
   <td><strong>Distorsión</strong></td>
   <td>Seleccione esta opción para evitar o reducir posibles defectos de bandas de color. </td>
  </tr>
  <tr>
   <td><strong>Tipo de enfoque</strong></td>
   <td><p>Seleccione <strong>Ninguno</strong>, <strong>Enfocar</strong>o Máscara de <strong>enfoque</strong>. </p>
    <ul>
     <li>Seleccione <strong>Ninguno</strong> para desactivar el enfoque.</li>
     <li>Seleccione <strong>Enfocar </strong>para aplicar un filtro de enfoque básico a la imagen después de que se haya realizado todo el escalado. El enfoque puede ayudar a compensar el desenfoque que puede producirse al mostrar una imagen con un tamaño diferente. </li>
     <li>Seleccione<strong> Máscara</strong> de enfoque para ajustar con precisión un efecto de filtro de enfoque en la imagen final con disminución de resolución. Puede controlar la intensidad del efecto, el radio del efecto (medido en píxeles) y un umbral de contraste que se omitirá. Este efecto utiliza las mismas opciones que el filtro "Máscara de enfoque" de Photoshop.</li>
    </ul> <p>En Máscara de <strong>enfoque</strong>, tiene las siguientes opciones:</p>
    <ul>
     <li><strong>Cantidad</strong> : controla la cantidad de contraste aplicado a los píxeles del borde. El valor de número real predeterminado es 1,0. Para imágenes de alta resolución, puede aumentarlas hasta 5,0. Considere la cantidad como una medida de la intensidad del filtro.</li>
     <li><strong>Radio</strong> : determina el número de píxeles que rodean los píxeles del borde que afectan al enfoque. Para las imágenes de alta resolución, introduzca un número real entre 1 y 2. Un valor bajo enfoca solo los píxeles del borde; un valor alto enfoca una banda más ancha de píxeles. El valor correcto depende del tamaño de la imagen.</li>
     <li><strong>Umbral</strong> : determina el rango de contraste que se debe ignorar al aplicar el filtro de máscara de enfoque. En otras palabras, esta opción determina la diferencia entre los píxeles enfocados y el área que los rodea antes de que se consideren píxeles de borde y se enfoquen. Para evitar introducir ruido, experimente con valores enteros entre 2 y 20. </li>
     <li><strong>Aplicar a: determina si el enfoque se aplica a cada color o brillo.</strong></li>
    </ul>
    <div>
      El enfoque se describe en <a href="https://docs.adobe.com/content/help/en/dynamic-media-classic/using/assets/s7_sharpening_images.pdf">Enfoque de imágenes</a>.
    </div> </td>
  </tr>
  <tr>
   <td><strong>Modo de remuestreo</strong></td>
   <td>Seleccione una opción <strong>Modo</strong> de remuestreo. Estas opciones enfocan la imagen cuando se reduce su resolución:
    <ul>
     <li><strong>Bi-Lineal</strong> : el método de remuestreo más rápido. Algunos artefactos de solapamiento son evidentes.</li>
     <li><strong>Bicúbico</strong> : aumenta el uso de CPU pero genera imágenes más nítidas con artefactos de solapamiento menos evidentes.</li>
     <li><strong>Sharp2</strong> : Puede producir resultados ligeramente más enfocados que los bicúbicos, pero a un costo de CPU aún mayor.</li>
     <li><strong>Bi-Sharp</strong> : selecciona el reampliador predeterminado de Photoshop para reducir el tamaño de la imagen, que en Adobe Photoshop se denomina <strong>bibicúbico más nítido</strong> .</li>
     <li><strong>Cada color</strong> y <strong>brillo</strong> : cada método puede basarse en el color o el brillo. De forma predeterminada, <strong>se selecciona Cada color</strong> .</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Resolución de impresión</strong></td>
   <td>Seleccione una resolución para imprimir esta imagen; 72 píxeles es el valor predeterminado.</td>
  </tr>
  <tr>
   <td><strong>Modificador de imagen</strong></td>
   <td><p>Más allá de la configuración de imagen común disponible en la interfaz de usuario, Dynamic Media admite numerosas modificaciones de imagen avanzadas que se pueden especificar en el campo Modificadores <strong>de</strong> imagen. Estos parámetros se definen en la referencia <a href="https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/http_ref/c_command_reference.html">del comando del protocolo</a>de servidor de imágenes.</p> <p>Importante: No se admite la siguiente funcionalidad enumerada en la API:</p>
    <ul>
     <li>Comandos básicos de creación de plantillas y procesamiento de texto: <code>text= textAngle= textAttr= textFlowPath= textFlowXPath= textPath=</code> y <code>textPs=</code></li>
     <li>Comandos de localización: <code>locale=</code> y <code>req=xlate</code></li>
     <li><code>req=set</code> no está disponible para uso general.</li>
     <li><code>req=mbrset</code></li>
     <li><code>req=saveToFile</code></li>
     <li><code>req=targets</code></li>
     <li><code>template=</code></li>
     <li>Servicios de Dynamic Media no principales: SVG, procesamiento de imágenes y impresión virtual</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Definición de opciones de ajustes preestablecidos de imagen con modificadores de imagen {#defining-image-preset-options-with-image-modifiers}

Además de las opciones disponibles en las fichas Básico y Avanzado, puede definir modificadores de imagen para proporcionar más opciones al definir ajustes preestablecidos de imagen. El procesamiento de imágenes se basa en la API de procesamiento de imágenes de Scene7 y se define en detalle en la Referencia [del protocolo](https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/http_ref/c_http_protocol_reference.html)HTTP.

A continuación se proporcionan algunos ejemplos básicos de lo que se puede hacer con los modificadores de imagen.

>[!NOTE]
>
>Algunos modificadores de imagen [no se pueden usar en AEM](#advanced-tab-options).

* [op_invert](https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/http_ref/r_op_invert.html) : invierte cada componente de color para obtener un efecto de imagen negativo.

   ```xml
   &op_invert=1
   ```

   ![6_5_imagepreset-edit-invert](assets/6_5_imagepreset-edit-invert.png)

* [op_blur](https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/http_ref/r_op_blur.html) : aplica un filtro de desenfoque a la imagen.

   ```xml
   &op_blur=7
   ```

   ![6_5_imagepreset-edit-blur](assets/6_5_imagepreset-edit-blur.png)

* Comandos combinados: op_blur y op-invert

   ```xml
   &op_invert=1&op_blur=7
   ```

   ![chlimage_1-80](assets/chlimage_1-501.png)

* [op_bright](https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/http_ref/r_op_brightness.html) : reduce o aumenta el brillo.

   ```xml
   &op_brightness=58
   ```

   ![6_5_imagepreset-edit-bright](assets/6_5_imagepreset-edit-brightness.png)

* [opac](https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/http_ref/r_opac.html) : ajusta la opacidad de la imagen. Permite reducir la opacidad en primer plano.

   ```xml
   opac=29
   ```

   ![6_5_imagepreset-edit-opacity](assets/6_5_imagepreset-edit-opacity.png)

## Edición de ajustes preestablecidos de imagen {#modifying-image-presets}

1. En AEM, toque el logotipo de AEM para acceder a la consola de navegación global y, a continuación, toque **[!UICONTROL Herramientas > Recursos > Ajustes preestablecidos]** de imagen.

   ![6_5_imagepreset-editpreset](assets/6_5_imagepreset-editpreset.png)

1. Seleccione un ajuste preestablecido y, a continuación, haga clic en **[!UICONTROL Editar]**. Se abre la ventana **[!UICONTROL Editar ajuste preestablecido]** de imagen.
1. Realice cambios y haga clic en **[!UICONTROL Guardar]** para guardar los cambios o en **[!UICONTROL Cancelar]** para cancelarlos.

## Publicación de ajustes preestablecidos de imagen de Dynamic Media {#publishing-image-presets}

Si está ejecutando el modo Dynamic Media: híbrido, debe publicar manualmente los ajustes preestablecidos de imagen.

(Si está ejecutando el modo Dynamic Media - Scene7, los ajustes preestablecidos de imagen se publican automáticamente; no necesita completar estos pasos).

**Para publicar ajustes preestablecidos de imagen en Dynamic Media: modo** híbrido:

1. En AEM, toque o haga clic en el logotipo de AEM para acceder a la consola de navegación global y toque o haga clic en el icono Herramientas y vaya a **[!UICONTROL Recursos > Ajustes preestablecidos]** de imagen.
1. Seleccione el ajuste preestablecido de imagen o varios ajustes preestablecidos de imagen en la lista de ajustes preestablecidos de imagen y toque o haga clic en **[!UICONTROL Publicar]**.
1. Después de publicar el ajuste preestablecido de imagen, el estado cambia de no publicado a publicado.

   ![chlimage_1-81](assets/chlimage_1-505.png)

## Eliminación de ajustes preestablecidos de imagen de Dynamic Media {#deleting-image-presets}

1. En AEM, toque o haga clic en el logotipo de AEM para acceder a la consola de navegación global.
1. Toque el icono **[!UICONTROL Herramientas]** y, a continuación, vaya a **[!UICONTROL Recursos > Ajustes preestablecidos]** de imagen.
1. Seleccione un ajuste preestablecido y, a continuación, haga clic en **[!UICONTROL Eliminar**. Dynamic Media confirma que desea eliminarlo. Toque **[!UICONTROL Eliminar]** para eliminar o **[!UICONTROL Cancelar]** para cancelar.

