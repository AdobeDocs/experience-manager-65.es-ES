---
title: Administración de ajustes preestablecidos de imagen de Dynamic Media
description: Conozca los ajustes preestablecidos de imagen de Dynamic Media y aprenda a crear, modificar y gestionar ajustes preestablecidos de imagen
uuid: 3e9a7af6-bf49-4cff-b516-0a3ee9765391
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: cc1111c4-6e24-4570-9ac7-97c25cf24ede
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/image-presets
translation-type: tm+mt
source-git-commit: ae3e6b1c2d3dfa63b9ea5763ebedaa57f5c7bc85
workflow-type: tm+mt
source-wordcount: '3866'
ht-degree: 10%

---


# Administración de ajustes preestablecidos de imagen de Dynamic Media{#managing-image-presets}

Los ajustes preestablecidos de imagen permiten a AEM Assets distribuir dinámicamente imágenes de diferentes tamaños, formatos diferentes o con otras propiedades de imagen que se generan dinámicamente. Cada ajuste preestablecido de imagen representa una colección predefinida de comandos de tamaño y diseño para mostrar las imágenes. Al crear un ajuste preestablecido de imagen, se elige un tamaño para el envío de la imagen. También puede elegir comandos de formato para que el aspecto de la imagen se optimice cuando se distribuya para su visualización.

Los administradores pueden crear ajustes preestablecidos para exportar recursos. Los usuarios pueden elegir un ajuste preestablecido cuando exportan imágenes, lo que también cambia el formato de las imágenes según las especificaciones del administrador.

También puede crear ajustes preestablecidos de imagen adaptables. Si se aplica un ajuste preestablecido de imagen interactivo a los recursos, éstos cambian según el dispositivo o el tamaño de pantalla en el que se vean. Puede configurar los ajustes preestablecidos de imagen para que utilicen CMYK en el espacio de color además de RGB o Gris.

En esta sección se describe cómo crear, modificar y administrar, en general, los ajustes preestablecidos de imagen. Puede aplicar un ajuste preestablecido de imagen a una imagen cada vez que la previsualización. Consulte [Aplicación de ajustes preestablecidos de imagen](/help/assets/image-presets.md).

>[!NOTE]
>
>Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes y utilizan la inteligencia en el último milisegundo de envío para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión de red o del navegador. Consulte [Imágenes inteligentes](/help/assets/imaging-faq.md) para obtener más información.

## Explicación de los ajustes preestablecidos de imagen de Dynamic Media {#understanding-image-presets}

Al igual que una macro, un ajuste preestablecido de imagen es una colección predefinida de comandos de tamaño y formato guardados con un nombre. Para comprender cómo funcionan los ajustes preestablecidos de imagen, supongamos que el sitio web requiere que cada imagen de producto aparezca en diferentes tamaños, formatos diferentes y tasas de compresión para el envío de escritorio y móvil.

>[!NOTE]
>
>En el modo Dynamic Media - Scene7, los ajustes preestablecidos de imagen solo son compatibles con los recursos de imagen.

Puede crear dos ajustes preestablecidos de imagen: uno con 500 x 500 píxeles para la versión de escritorio y 150 x 150 píxeles para la versión móvil. Puede crear dos ajustes preestablecidos de imagen, uno denominado `Enlarge` para mostrar imágenes de 500 x 500 píxeles y otro denominado `Thumbnail` para mostrar imágenes de 150 x 150 píxeles. Para distribuir imágenes con los tamaños `Enlarge` y `Thumbnail`, AEM busca la definición del ajuste preestablecido de imagen Ampliar y el ajuste preestablecido de imagen en miniatura. A continuación, AEM genera dinámicamente una imagen con las especificaciones de tamaño y formato de cada ajuste preestablecido de imagen.

Las imágenes con un tamaño reducido al distribuirse dinámicamente pueden perder nitidez y detalle. Por este motivo, cada ajuste preestablecido de imagen contiene controles de formato para optimizar una imagen cuando se distribuye con un tamaño concreto. Estos controles garantizan que las imágenes sean nítidas y claras cuando se envían al sitio web o a la aplicación.

Los administradores pueden crear ajustes preestablecidos de imagen. Para crear un ajuste preestablecido de imagen, puede realizar inicios desde cero o puede realizar inicios desde uno existente y guardarlo con un nombre nuevo.

## Administración de ajustes preestablecidos de imagen de Dynamic Media {#managing-image-presets-1}

Para administrar los ajustes preestablecidos de imagen en AEM, toque o haga clic en el logotipo de AEM para acceder a la consola de navegación global y, a continuación, toque o haga clic en el icono Herramientas y vaya a **[!UICONTROL Recursos > Ajustes preestablecidos de imagen.]**

![6_5_tools-assets-imagepresets](assets/6_5_tools-assets-imagepresets.png)

>[!NOTE]
>
>Los ajustes preestablecidos de imagen que cree también estarán disponibles como representaciones dinámicas cuando realice la previsualización o entrega de recursos.
>
>En *Dynamic Media - modo Scene7*, *no* necesita publicar ajustes preestablecidos de imagen cuando los ajustes preestablecidos de imagen se publican automáticamente.
>
>En *Dynamic Media - Modo híbrido*, debe publicar manualmente los ajustes preestablecidos de imagen.
>
>Consulte [Publicación de ajustes preestablecidos de imagen.](#publishing-image-presets)

>[!NOTE]
>
>El sistema muestra una variedad de representaciones al seleccionar **[!UICONTROL Representaciones]** en la Vista de detalles de un recurso. Puede aumentar o disminuir el número de ajustes preestablecidos de imagen que se muestran. Consulte [Aumento del número de ajustes preestablecidos de imagen que se muestran](#increasing-or-decreasing-the-number-of-image-presets-that-display).

### Cultivos inteligentes, Adobe Illustrator (AI), Postscript (EPS) y formatos de archivo PDF {#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats}

>[!NOTE]
>
>Este tema solo se aplica a Dynamic Media: modo híbrido.

Si desea admitir la ingestión de archivos AI, EPS y PDF para poder generar representaciones dinámicas de estos formatos de archivo, puede que desee revisar la siguiente información antes de crear ajustes preestablecidos de imagen.

El formato de archivo de Adobe Illustrator es una variante de PDF. Las principales diferencias, en el contexto de AEM Assets, son las siguientes:

* Los documentos de Adobe Illustrator constan de una sola página con varias capas. Cada capa se extrae como un subrecurso PNG en el recurso principal de Illustrator.
* Los documentos PDF constan de una o varias páginas. Cada página se extrae como un subrecurso PDF de una sola página en el documento PDF principal de varias páginas.

Los subrecursos son creados por el componente `Create Sub Asset process` dentro del flujo de trabajo general `DAM Update Asset`. Para ver este componente de proceso dentro del flujo de trabajo, toque **[!UICONTROL Herramientas > Flujo de trabajo > Modelos > Recurso de actualización de DAM > Editar.]**

Consulte también [Visualización de páginas de un archivo de varias páginas](/help/assets/managing-linked-subassets.md#view-pages-of-a-multi-page-file).

Puede vista de los subrecursos o las páginas al abrir el recurso, tocar el menú Contenido y seleccionar **[!UICONTROL Subrecursos]** o **[!UICONTROL Páginas.]** Los subactivos son activos reales. Es decir, las páginas PDF se extraen mediante el componente de flujo de trabajo `Create Sub Asset`. Luego se almacenan como `page1.pdf`, `page2.pdf`, etc., debajo del recurso principal. Una vez almacenados, el flujo de trabajo `DAM Update Asset` los procesa.

Para utilizar Dynamic Media para la previsualización y generación de representaciones dinámicas para archivos AI, EPS o PDF, se requieren los siguientes pasos de procesamiento:

1. En el flujo de trabajo `DAM Update Asset`, el componente de proceso `Rasterize PDF/AI Image Preview Rendition` rasteriza la primera página del recurso original (utilizando la resolución configurada) en una representación `cqdam.preview.png`.

1. A continuación, la representación `cqdam.preview.png` se optimiza en un PTIFF mediante el componente de proceso `Dynamic Media Process Image Assets` dentro del flujo de trabajo.

>[!NOTE]
>
>En el flujo de trabajo [!UICONTROL Recurso de actualización de DAM], el paso **[!UICONTROL Miniaturas de EPS]** genera miniaturas para los archivos EPS.

#### Propiedades de metadatos de recursos PDF/AI/EPS {#pdf-ai-eps-asset-metadata-properties}

| **Propiedad Metadata** | **Descripción** |
|---|---|
| dam:Physicalwidthinpulgadas | Ancho del documento en pulgadas. |
| dam:Physicalheightinpulgadas | Altura del documento en pulgadas. |

Puede acceder a las opciones de los componentes de proceso `Rasterize PDF/AI Image Preview Rendition` mediante el flujo de trabajo `DAM Update Asset`.

Toque en Adobe Experience Manager en la esquina superior izquierda y vaya a **[!UICONTROL Herramientas > Flujo de trabajo > Modelos.]** En la página Modelos de flujo de trabajo, seleccione Actualizar recurso **** DAM y, a continuación, en la barra de herramientas, toque  **[!UICONTROL Editar.]** En la página  [!UICONTROL DAM Update ] Assetworkflow, toque con el doble el componente de  `Rasterize PDF/AI Image Preview Rendition` proceso para abrir el cuadro de diálogo Propiedades de paso.

#### Rasterizar opciones de representación de Previsualización de imágenes PDF/AI {#rasterize-pdf-ai-image-preview-rendition-options}

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
   <td>Lista de tipos MIME de documento que se consideran documentos PDF o Illustrator.<br /> </td>
  </tr>
  <tr>
   <td>Ancho máximo</td>
   <td>2048</td>
   <td>Ancho máximo de la representación de previsualización generada, en píxeles.<br /> </td>
  </tr>
  <tr>
   <td>Alto máximo</td>
   <td>2048</td>
   <td>Altura máxima de la representación de previsualización generada, en píxeles.<br /> </td>
  </tr>
  <tr>
   <td>Resolución</td>
   <td>72</td>
   <td>Resolución para rasterizar la primera página, en ppp (píxeles por pulgada).</td>
  </tr>
 </tbody>
</table>

Con los argumentos de proceso predeterminados, la primera página de un documento PDF/AI se rasteriza a 72 ppp y la imagen de previsualización generada tiene un tamaño de 2048 x 2048 píxeles. Para una implementación típica, puede aumentar la resolución a un mínimo de 150 ppp o más. Por ejemplo, un documento de tamaño de letra de EE. UU. a 300 ppp requiere una anchura y una altura máximas de 2550 x 3300 píxeles, respectivamente.

La anchura máxima y la altura máxima limitan la resolución en la que se rasterizará. Por ejemplo, si los máximos no cambian y la resolución se establece en 300 ppp, un documento de carta de EE. UU. se rasteriza a 186 ppp. Es decir, el documento es de 1581 x 2046 píxeles.

El componente de proceso `Rasterize PDF/AI Image Preview Rendition` tiene un máximo definido para garantizar que no cree imágenes demasiado grandes en la memoria. Estas imágenes de gran tamaño pueden desbordar la memoria proporcionada a la JVM (Máquina virtual Java). Se debe tener cuidado de proporcionar al JVM suficiente memoria para administrar el número configurado de flujos de trabajo paralelos, y cada uno de ellos tiene la posibilidad de crear una imagen con el tamaño máximo configurado.

### Formato de archivo InDesign (INDD) {#indesign-indd-file-format}

Si desea admitir la ingestión de archivos INDD para poder generar una representación dinámica de este formato de archivo, es posible que desee revisar la siguiente información antes de crear ajustes preestablecidos de imagen.

Para los archivos InDesign, los subrecursos se extraen solo si el servidor Adobe InDesign está integrado con AEM. Los recursos a los que se hace referencia están vinculados según sus metadatos. No se requiere InDesign Server para la vinculación. Sin embargo, los recursos a los que se hace referencia deben estar presentes en AEM antes de que se procesen los archivos de InDesign para que se creen los vínculos entre los archivos de InDesign y los recursos a los que se hace referencia.

Consulte [Integración de AEM Assets con InDesign Server](/help/assets/indesign.md).

El componente de proceso de Extracción de medios del flujo de trabajo `DAM Update Asset` ejecuta varios scripts extend preconfigurados para procesar archivos InDesign.

![Rutas de ExtendScript en los argumentos del proceso de Extracción de medios](assets/6_5_mediaextractionprocess.png)

Las rutas de ExtendScript en los argumentos del componente de proceso de Extracción de medios en el flujo de trabajo [!UICONTROL Recurso de actualización de DAM].

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
   <td>Genera una representación de 300 ppp <code>thumbnail.jpg</code> que se optimiza y se convierte en una representación PTIFF mediante <code>Dynamic Media Process Image Assets</code> componente de proceso.<br /> </td>
  </tr>
  <tr>
   <td>JPEGPagesExport.jsx</td>
   <td>Sí</td>
   <td>Genera un subrecurso JPEG de 300 ppp para cada página. El subrecurso JPEG es un recurso real almacenado bajo el recurso InDesign. También se optimiza y se convierte en un PTIFF mediante el flujo de trabajo <code>DAM Update Asset</code>.<br /> </td>
  </tr>
  <tr>
   <td>PDFPagesExport.jsx</td>
   <td>No</td>
   <td>Genera un subrecurso PDF para cada página. El subrecurso PDF se procesa como se ha descrito anteriormente. Dado que el PDF solo contiene una página, no se generan subrecursos.<br /> </td>
  </tr>
 </tbody>
</table>

## Configuración del tamaño de miniatura de la imagen {#configuring-image-thumbnail-size}

Puede configurar el tamaño de las miniaturas configurando dicha configuración en el flujo de trabajo **[!UICONTROL Recurso de actualización de DAM]**. Hay dos pasos en el flujo de trabajo donde puede configurar el tamaño de las miniaturas de los recursos de imagen. Aunque se utiliza uno (**[!UICONTROL Recursos de imagen de proceso de Dynamic Media]**) para recursos de imagen dinámica y el otro (**[!UICONTROL Miniaturas de proceso]**) para la generación de miniaturas estáticas o cuando todos los demás procesos no pueden generar miniaturas, *ambos* deben tener la misma configuración.

Con el paso **[!UICONTROL Recursos de imagen de proceso de Dynamic Media]**, el servidor de imágenes genera miniaturas y esta configuración es independiente de la configuración aplicada al paso **[!UICONTROL Procesar miniaturas]**. La generación de miniaturas a través del paso **[!UICONTROL Miniaturas de proceso]** es la forma más lenta y con mayor consumo de memoria para crear miniaturas.

El tamaño de las miniaturas se define en el siguiente formato: **[!UICONTROL width:height:center]**, por ejemplo *80:80:false*. La anchura y la altura determinan el tamaño en píxeles de la miniatura; el valor central es false o true y, si se define como true, indica que la imagen en miniatura tiene exactamente el tamaño indicado en la configuración. Si la imagen redimensionada es más pequeña, se centrará dentro de la miniatura.

>[!NOTE]
>
>* El tamaño de las miniaturas de los archivos EPS se configura en el paso de **[!UICONTROL miniaturas EPS]**, en la pestaña **[!UICONTROL Argumentos]**, en Miniaturas.
   >
   >
* El tamaño de las miniaturas de los vídeos se configura en el paso **[!UICONTROL Miniaturas FFmpeg]**, en la pestaña **[!UICONTROL Proceso]**, en **[!UICONTROL Argumentos.]**

>



**Para configurar el tamaño** de miniatura de la imagen:

1. Toque **[!UICONTROL Herramientas > Flujo de trabajo > Modelos > Recurso de actualización de DAM > Editar.]**
1. Toque el paso **[!UICONTROL Recursos de imagen de proceso de Dynamic Media]** y toque o haga clic en la ficha **[!UICONTROL Miniaturas]**. Cambie el tamaño de la miniatura, según sea necesario, y pulse **[!UICONTROL Aceptar.]**

   ![6_5_dynamicmediaprocessimageassets-thumbnailstab](assets/6_5_dynamicmediaprocessimageassets-thumbnailstab.png)

1. Pulse el paso **[!UICONTROL Procesar miniaturas]** y, a continuación, pulse la pestaña **[!UICONTROL Miniaturas]**. Cambie el tamaño de la miniatura, según sea necesario, y pulse **[!UICONTROL Aceptar.]**

   >[!NOTE]
   >
   >Los valores del argumento de miniaturas del paso **[!UICONTROL Miniaturas de proceso]** deben coincidir con el argumento de miniaturas del paso **[!UICONTROL Recursos de imagen de proceso de Dynamic Media]**.

1. Toque **[!UICONTROL Guardar]** para guardar los cambios en el flujo de trabajo.

### Aumento o disminución del número de ajustes preestablecidos de imagen de Dynamic Media que muestran {#increasing-or-decreasing-the-number-of-image-presets-that-display}

Los ajustes preestablecidos de imagen que cree estarán disponibles como representaciones dinámicas al realizar la previsualización de recursos. AEM muestra una variedad de representaciones dinámicas al visualizar recursos desde **[!UICONTROL Vista de detalles > Representaciones.]** Puede aumentar o reducir el límite de representaciones que se muestran.

**Para aumentar o reducir el número de ajustes preestablecidos de imagen de Dynamic Media que se muestran**:

1. Vaya a CRXDE Lite ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Vaya al nodo de lista de ajustes preestablecidos de imagen en `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist`

   ![Increase_decreasethenumberofimagepresetsthatdisplay](assets/increase_decreasethenumberofimagepresetsthatdisplay.png)

1. En la propiedad **[!UICONTROL limit]**, cambie el **[!UICONTROL valor]**, que se establece en 15 de forma predeterminada, por el número deseado.
1. Vaya al origen de datos de ajustes preestablecidos de imagen en `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist/datasource`

   ![chlimage_1-495](assets/chlimage_1-495.png)

1. En la propiedad limit, cambie el número al número deseado, por ejemplo `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. Toque **[!UICONTROL Guardar todo.]**

## Creación de un ajuste preestablecido de imagen para Dynamic Media {#creating-image-presets}

La creación de un ajuste preestablecido de imagen de Dynamic Media le permite aplicar estos ajustes a cualquier imagen al obtener una vista previa o al publicar.

>[!NOTE]
>
>Si utiliza Internet Explorer 9, la creación de un ajuste preestablecido no aparece en la lista preestablecida inmediatamente después de guardarlo. Para solucionar este problema, deshabilite la caché para IE9.

Si desea admitir la ingestión de archivos AI, PDF y EPS para poder generar una representación dinámica de estos formatos de archivo, es posible que desee revisar la siguiente información antes de crear ajustes preestablecidos de imagen.
Consulte [Formatos de archivo Adobe Illustrator (AI), Postscript (EPS) y PDF](#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats).

Si desea admitir la ingestión de archivos INDD para poder generar una representación dinámica de este formato de archivo, es posible que desee revisar la siguiente información antes de crear ajustes preestablecidos de imagen.
Consulte [Formato de archivo InDesign (INDD)](#indesign-indd-file-format).

>[!NOTE]
>
>Para crear ajustes preestablecidos de imagen de Dynamic Media, debe tener privilegios de administrador como administrador AEM o administrador de Admin Console.

**Para crear un ajuste preestablecido** de imagen de Dynamic Media:

1. En AEM, toque el logotipo de AEM para acceder a la consola de navegación global y, a continuación, toque **[!UICONTROL Herramientas > Recursos > Ajustes preestablecidos de imagen.]**
1. Haga clic en **[!UICONTROL Crear.]** Se abre la ventana  **[!UICONTROL Editar]** ajuste preestablecido de imagen.

   ![chlimage_1-496](assets/chlimage_1-496.png)

   >[!NOTE]
   >
   >Para que este ajuste preestablecido de imagen sea interactivo, borre los valores de los campos de **[!UICONTROL anchura]** y **[!UICONTROL altura]** y déjelos en blanco.

1. Introduzca valores en las pestañas **[!UICONTROL Básico]** y **[!UICONTROL Avanzadas]** según corresponda, incluido un nombre. Las opciones se describen en [Opciones de ajustes preestablecidos de imagen](#image-preset-options). Los ajustes preestablecidos aparecen en el panel izquierdo y se pueden utilizar sobre la marcha con otros recursos.

   ![6_5_imagepreset-edit](assets/6_5_imagepreset-edit.png)

1. Haga clic en **[!UICONTROL Guardar]**.

## Creación de un ajuste preestablecido de imagen interactivo {#creating-a-responsive-image-preset}

Para crear un ajuste preestablecido de imagen interactivo, siga los pasos que se describen en [Creación de ajustes preestablecidos de imagen](#creating-image-presets). Al introducir la altura y la anchura en la ventana **[!UICONTROL Editar ajuste preestablecido de imagen]**, borre los valores y déjelos en blanco.

Si se dejan en blanco, AEM que este ajuste preestablecido de imagen responde. Puede ajustar los demás valores según corresponda.



>[!NOTE]
>
>Para ver los botones **[!UICONTROL URL]** y **[!UICONTROL RESS]** al aplicar un ajuste preestablecido de imagen a un recurso, el recurso debe publicarse.
>
>![chlimage_1-79](assets/chlimage_1-498.png)
>
>En el modo Dynamic Media - Scene7, los ajustes preestablecidos de imagen y los recursos de imagen se publican automáticamente.
>
>En Dynamic Media: modo híbrido, debe publicar manualmente ajustes preestablecidos de imagen y recursos de imagen.

### Opciones de ajustes preestablecidos de imagen {#image-preset-options}

Al crear o editar ajustes preestablecidos de imagen, tiene las opciones descritas en esta sección. Además, Adobe recomienda estas opciones de &quot;prácticas recomendadas&quot; para el inicio:

* **[!UICONTROL Formato]** (pestaña **[!UICONTROL Básico]**): Seleccione **[!UICONTROL JPEG]** u otro formato que cumpla sus necesidades. Todos los navegadores web admiten el formato de imagen JPEG; ofrece un buen equilibrio entre los tamaños de archivos pequeños y la calidad de imagen. Sin embargo, las imágenes en formato JPEG utilizan un esquema de compresión con pérdidas que puede introducir artefactos de imagen no deseados si el ajuste de compresión es demasiado bajo. Por este motivo, Adobe recomienda establecer la calidad de compresión en 75. Este ajuste ofrece un buen equilibrio entre la calidad de imagen y el tamaño de archivo pequeño.

* **[!UICONTROL Activar enfoque simple]**: No seleccione **[!UICONTROL Activar enfoque simple]** (este filtro de enfoque ofrece menos control que la configuración de máscara de enfoque).

* **[!UICONTROL Enfoque: Modo]**  de remuestreo: seleccione  **[!UICONTROL Bicúbico.]**

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
   <td><p>Elija un formato en el menú.</p> <p>Al elegir <strong>JPEG</strong> se ofertas las siguientes opciones adicionales:</p>
    <ul>
     <li><strong>Calidad</strong> : controla el nivel de compresión JPEG. Esta configuración afecta tanto al tamaño del archivo como a la calidad de la imagen. La escala de calidad JPEG es de 1 a 100. La escala está visible al arrastrar el control deslizante.</li>
     <li><strong>Activar disminución de resolución</strong>  de crominancia JPG: como el ojo es menos sensible a la información de color de alta frecuencia que la luminancia de alta frecuencia, las imágenes JPEG dividen la información de la imagen en componentes de color y luminancia. Cuando se comprime una imagen JPEG, el componente de luminancia se deja con una resolución completa, mientras que los componentes de color se reducen al calcular el promedio de grupos de píxeles. La disminución de resolución reduce el volumen de datos en una mitad o en un tercio, sin afectar prácticamente a la calidad percibida. La disminución de resolución no se aplica a imágenes en escala de grises. Esta técnica reduce la cantidad de compresión útil para imágenes con alto contraste (por ejemplo, imágenes con texto superpuesto).</li>
    </ul>
    <div>
      Elección
     <strong>GIF</strong> o
     <strong>GIF con alpha</strong> proporciona estas
     <strong>Opciones de Cuantificación de color GIF</strong>:
    </div>
    <ul>
     <li><strong>Tipo  </strong>- Seleccione  <strong>Adaptable</strong>  (opción predeterminada),  <strong>Web</strong> o  <strong>Macintosh</strong>. Si selecciona <strong>GIF con Alpha</strong>, la opción Macintosh no está disponible.</li>
     <li><strong>Tramado</strong> : seleccione  <strong></strong> Difusor o  <strong>Desactivado</strong>.</li>
     <li><strong>Número de colores  </strong>- Introduzca un número entre 2 y 256.</li>
     <li><strong>Lista</strong>  de color: introduzca una lista separada por comas. Por ejemplo, para blanco, gris y negro, introduzca 000000,888888,ffffff.</li>
    </ul>
    <div>
      Elección
     <strong>PDF</strong>,
     <strong>TIFF</strong>, o
     <strong>TIFF con alpha</strong> proporciona esta opción adicional:
    </div>
    <ul>
     <li><strong>Compresión</strong> : seleccione un algoritmo de compresión. Las opciones de algoritmo para PDF son <strong>None</strong>, <strong>Zip</strong> y <strong>Jpeg</strong>; para TIFF son <strong>None</strong>, <strong>LZW</strong>, <strong>Jpeg</strong> y <strong>Zip</strong>; y para TIFF con alfa son <strong>Ninguno</strong>, <strong>LZW</strong> y <strong>Zip</strong>.</li>
    </ul> <p>Al elegir <strong>PNG</strong>, <strong>PNG con alfa,</strong> o <strong>EPS</strong> no se proporcionan opciones adicionales.</p> </td>
  </tr>
  <tr>
   <td><strong>Enfoque</strong></td>
   <td>Seleccione la opción <strong>Activar enfoque simple</strong> para aplicar un filtro de enfoque básico a la imagen después de que se realice todo el escalado. El enfoque puede ayudar a compensar el desenfoque que puede producirse al mostrar una imagen con un tamaño diferente. </td>
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
   <td>Seleccione <strong>RGB, CMYK,</strong> o <strong>Escala de grises</strong> para el espacio de color.</td>
  </tr>
  <tr>
   <td><strong>Perfil de color</strong></td>
   <td>Seleccione el perfil de espacio de color de salida al que se debe convertir el recurso si es distinto del perfil de trabajo.</td>
  </tr>
  <tr>
   <td><strong>Procesar intención</strong></td>
   <td>Puede anular la interpretación predeterminada. Las interpretaciones determinan lo que sucede con los colores que no se pueden reproducir en el perfil de color del destinatario (fuera de gama). La calidad de representación se omite si no es compatible con el perfil ICC.
    <ul>
     <li>Seleccione <strong>Perceptual</strong> para comprimir la gama total de un espacio de color en otro espacio de color cuando uno o varios colores de la imagen original están fuera de la gama del espacio de color de destino.</li>
     <li>Seleccione <strong>Colorimétrica relativa</strong> cuando un color del espacio de color actual esté fuera de gama en el espacio de color de destinatario y desee asignarlo al color más cercano posible dentro de la gama del espacio de color de destinatario sin afectar a ningún otro color. </li>
     <li>Seleccione <strong>Saturación</strong> para reproducir la saturación de color de la imagen original al convertirla en el espacio de color del destinatario. </li>
     <li>Seleccione <strong>Colorimétrica absoluta</strong> para que coincida exactamente con los colores sin ningún ajuste para el punto blanco o el punto negro que pueda alterar el brillo de la imagen.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Compensación de punto negro</strong></td>
   <td>Seleccione esta opción si el perfil de salida admite esta función. La compensación de Blackpoint se ignora si no es compatible con el perfil ICC especificado.</td>
  </tr>
  <tr>
   <td><strong>Distorsión</strong></td>
   <td>Seleccione esta opción para evitar o reducir posibles defectos de bandas de color. </td>
  </tr>
  <tr>
   <td><strong>Tipo de enfoque</strong></td>
   <td><p>Seleccione <strong>Ninguno</strong>, <strong>Enfocar</strong> o <strong>Máscara de enfoque</strong>. </p>
    <ul>
     <li>Seleccione <strong>Ninguno</strong> para desactivar el enfoque.</li>
     <li>Seleccione <strong>Enfocar </strong>para aplicar un filtro de enfoque básico a la imagen después de que se realice todo el escalado. El enfoque puede ayudar a compensar el desenfoque que puede producirse al mostrar una imagen con un tamaño diferente. </li>
     <li>Seleccione<strong> Máscara de enfoque</strong> para ajustar un efecto de filtro de enfoque en la imagen final con disminución de resolución. Puede controlar la intensidad del efecto, el radio del efecto (medido en píxeles) y un umbral de contraste que se omitirá. Este efecto utiliza las mismas opciones que el filtro “Máscara de enfoque” de Photoshop.</li>
    </ul> <p>En <strong>Máscara de enfoque</strong>, tiene las siguientes opciones:</p>
    <ul>
     <li><strong>Cantidad</strong> : controla la cantidad de contraste aplicado a los píxeles del borde. El valor de número real predeterminado es 1,0. Para imágenes de alta resolución, puede aumentarlas hasta 5,0. Considere la cantidad como una medida de la intensidad del filtro.</li>
     <li><strong>Radio</strong> : determina el número de píxeles que rodean los píxeles del borde que afectan al enfoque. Para las imágenes de alta resolución, introduzca un número real entre 1 y 2. Un valor bajo enfoca solo los píxeles del borde; un valor alto enfoca una banda más ancha de píxeles. El valor correcto depende del tamaño de la imagen.</li>
     <li><strong>Umbral</strong> : determina el rango de contraste que se debe ignorar al aplicar el filtro de máscara de enfoque. En otras palabras, esta opción determina la diferencia entre los píxeles enfocados y el área que los rodea antes de que se consideren píxeles de borde y se enfoquen. Para evitar introducir ruido, experimente con valores enteros entre 2 y 20. </li>
     <li><strong>Aplicar a: determina si el enfoque se aplica a cada color o brillo. </strong> </li>
    </ul>
    <div>
      El enfoque se describe en
     <a href="https://docs.adobe.com/content/help/en/dynamic-media-classic/using/assets/sharpening_images.pdf">Enfoque de imágenes</a>.
    </div> </td>
  </tr>
  <tr>
   <td><strong>Modo de remuestreo</strong></td>
   <td>Seleccione una opción <strong>Modo de remuestreo</strong>. Estas opciones enfocan la imagen cuando se reduce su resolución:
    <ul>
     <li><strong>Bilineal</strong> : el método de remuestreo más rápido. Algunos artefactos de solapamiento son evidentes.</li>
     <li><strong>Bicúbico</strong> : aumenta el uso de CPU pero genera imágenes más nítidas con artefactos de solapamiento menos evidentes.</li>
     <li><strong>Sharp2</strong> - Puede producir resultados ligeramente más nítidos que Bicúbicos, pero a un costo de CPU aún mayor.</li>
     <li><strong>Bi-Sharp</strong> : selecciona el reampliador predeterminado de Photoshop para reducir el tamaño de la imagen, que se denomina  <strong>bibicúbico </strong> enfoque en Adobe Photoshop.</li>
     <li><strong>Cada </strong> color y  <strong>brillo</strong> : cada método puede basarse en el color o el brillo. De forma predeterminada <strong>Cada color</strong> está seleccionado.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Resolución de impresión</strong></td>
   <td>Seleccione una resolución para imprimir esta imagen; 72 píxeles es el valor predeterminado.</td>
  </tr>
  <tr>
   <td><strong>Modificador de imagen</strong></td>
   <td><p>Más allá de la configuración de imagen común disponible en la interfaz de usuario, Dynamic Media admite numerosas modificaciones de imagen avanzadas que se pueden especificar en el campo <strong>Modificadores de imagen</strong>. Estos parámetros se definen en la referencia del comando <a href="https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html">Protocolo del servidor de imágenes</a>.</p> <p>Importante: No se admite la siguiente funcionalidad enumerada en la API:</p>
    <ul>
     <li>Comandos básicos de creación de plantillas y procesamiento de texto: <code>text= textAngle= textAttr= textFlowPath= textFlowXPath= textPath=</code> y <code>textPs=</code></li>
     <li>Comandos de localización: <code>locale=</code> y <code>req=xlate</code></li>
     <li><code>req=set</code> no está disponible para uso general.</li>
     <li><code>req=mbrset</code></li>
     <li><code>req=saveToFile</code></li>
     <li><code>req=targets</code></li>
     <li><code>template=</code></li>
     <li>Servicios no principales de Dynamic Media: SVG, procesamiento de imágenes y impresión virtual</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Definición de opciones de ajustes preestablecidos de imagen con modificadores de imagen {#defining-image-preset-options-with-image-modifiers}

Además de las opciones disponibles en las fichas Básico y Avanzado, puede definir modificadores de imagen para proporcionar más opciones al definir ajustes preestablecidos de imagen. El procesamiento de imágenes se basa en la API de procesamiento de imágenes de Scene7 y se define en detalle en la [Referencia del protocolo HTTP](https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/http_ref/c_http_protocol_reference.html).

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

1. En AEM, toque el logotipo de AEM para acceder a la consola de navegación global y, a continuación, toque **[!UICONTROL Herramientas > Recursos > Ajustes preestablecidos de imagen.]**

   ![6_5_imagepreset-editpreset](assets/6_5_imagepreset-editpreset.png)

1. Seleccione un ajuste preestablecido y haga clic en **[!UICONTROL Editar.]** Se abre la ventana  **[!UICONTROL Editar]** ajuste preestablecido de imagen.
1. Realice cambios y haga clic en **[!UICONTROL Guardar]** para guardar los cambios o **[!UICONTROL Cancelar]** para cancelar los cambios.

## Publicación de ajustes preestablecidos de imagen de Dynamic Media {#publishing-image-presets}

Si está ejecutando Dynamic Media en modo híbrido, debe publicar manualmente los ajustes preestablecidos de imagen.

(Si está ejecutando el modo Dynamic Media - Scene7, los ajustes preestablecidos de imagen se publican automáticamente; no necesita completar estos pasos).

**Para publicar ajustes preestablecidos de imagen en Dynamic Media: modo** híbrido:

1. En AEM, toque o haga clic en el logotipo de AEM para acceder a la consola de navegación global y toque o haga clic en el icono Herramientas y vaya a **[!UICONTROL Recursos > Ajustes preestablecidos de imagen.]**
1. Seleccione el ajuste preestablecido de imagen o varios ajustes preestablecidos de imagen en la lista de ajustes preestablecidos de imagen y toque o haga clic en **[!UICONTROL Publicar.]**
1. Después de publicar el ajuste preestablecido de imagen, el estado cambia de no publicado a publicado.

   ![chlimage_1-81](assets/chlimage_1-505.png)

## Eliminación de ajustes preestablecidos de imagen de Dynamic Media {#deleting-image-presets}

1. En AEM, toque o haga clic en el logotipo de AEM para acceder a la consola de navegación global.
1. Toque el icono **[!UICONTROL Herramientas]** y luego navegue a **[!UICONTROL Recursos > Ajustes preestablecidos de imagen.]**
1. Seleccione un ajuste preestablecido y haga clic en **[!UICONTROL Eliminar]**. Dynamic Media confirma que desea eliminarlo. Toque **[!UICONTROL Eliminar]** para eliminar o toque **[!UICONTROL Cancelar]** para cancelar.

