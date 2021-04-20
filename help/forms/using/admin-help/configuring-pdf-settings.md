---
title: Configuración de Adobe PDF
seo-title: Configuración de Adobe PDF
description: Obtenga información sobre cómo configurar Adobe PDF.
seo-description: Obtenga información sobre cómo configurar Adobe PDF.
uuid: 980c9d6a-f75e-4e7d-b050-d2d07a10ef33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab018b6d-0233-4439-bb75-58c5421d769a
feature: PDF Generator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '7278'
ht-degree: 0%

---


# Configuración de Adobe PDF{#configuring-adobe-pdf-settings}

La página Configuración de Adobe PDF muestra la configuración de conversión que puede especificar para las fuentes. Puede usar cualquiera de los ajustes de PDF predefinidos o crear los suyos propios. La configuración de PDF determina con precisión cómo se convierten los archivos y su estructura y características de PDF resultantes. La configuración de Adobe PDF se conocía anteriormente como parámetros de Distiller® u opciones de trabajo.

En la página Configuración de Adobe PDF, puede realizar las siguientes tareas:

* Ver la configuración de PDF predefinida. (Consulte [Acerca de la configuración de PDF predefinida](configuring-pdf-settings.md#about-the-predefined-pdf-settings)).
* Cree una configuración de PDF o edite una que haya creado anteriormente. (Consulte [Agregar o editar la configuración de PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings)).
* Especifique la configuración predeterminada de PDF. (Consulte [Cambiar la configuración predeterminada](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings))
* Cargue un archivo de configuración de PDF en el servidor. (Consulte [Cargar configuración de PDF](configuring-pdf-settings.md#upload-pdf-settings)).
* Eliminar la configuración de PDF personalizada. (Consulte [Eliminar configuración de PDF](configuring-pdf-settings.md#delete-pdf-settings)).
* Cargue y descargue archivos de prólogo y epílogo. (Consulte [Carga y descarga de archivos de prólogo y epílogo](configuring-pdf-settings.md#uploading-and-downloading-prologue-and-epilogue-files)).

La configuración de Adobe PDF solo se aplica a las conversiones basadas en PDFMaker. Estas incluyen las siguientes conversiones:

* Documento de Microsoft Word (DOC, DOCX, RTF, TXT)
* Documento de Microsoft Excel (XLS, XLSX)
* Documento de Microsoft PowerPoint (PPT, PPTX)
* Documento de Microsoft Project (MPP)
* Documento de Microsoft Visio (VSD)

>[!NOTE]
>
>Al utilizar OpenOffice para convertir los formatos anteriores, no se aplica la configuración de Adobe PDF.

## Acerca de la configuración de PDF predefinida {#about-the-predefined-pdf-settings}

PDF Generator proporciona varias configuraciones de PDF predefinidas para su uso. No puede modificar esta configuración predefinida; sin embargo, puede crear una configuración basada en una existente editando la configuración y guardarla con un nombre nuevo.

**Impresión de alta calidad:** crea archivos PDF para obtener una salida de alta calidad. Esta configuración:

* baja resolución de imágenes en color y escala de grises a 300 ppp
* baja imágenes monocromas a 1200 ppp
* imprime en una resolución de imagen más alta
* utiliza otros ajustes para conservar la cantidad máxima de información sobre el documento original.

Estos archivos PDF se pueden abrir en Adobe Acrobat 5 y Adobe Acrobat Reader® 5 o posterior.

**Páginas de gran tamaño:** crea documentos PDF adecuados para una visualización e impresión fiables de dibujos de ingeniería de más de 200 x 200 pulgadas. Los documentos PDF creados se pueden abrir en Adobe Acrobat Professional y Acrobat Standard, en la versión 7 o posterior, y en Adobe Reader 7 o posterior.

**PDF/A-1B 2005 CMYK / PDF/A-1B 2005 RGB:** comprueba los trabajos entrantes para cumplir con la norma ISO para la conservación (archivo) a largo plazo de documentos electrónicos y crea archivos PDF/A únicamente si se cumplen las normas. Estos archivos se utilizan principalmente para el archivado. Los archivos compatibles solo pueden contener texto, imágenes rasterizadas y objetos vectoriales; no pueden contener codificación ni secuencias de comandos. Además, todas las fuentes deben incrustarse para que los documentos puedan abrirse y verse como se crearon. PDF/A-1b utiliza PDF 1.4 y convierte todos los colores a CMYK o RGB, según el estándar que elija. Los archivos PDF creados con este archivo de configuración se pueden abrir en Acrobat 5 y Acrobat Reader 5 y posteriores. Para obtener más información sobre PDF/A, consulte Adobe y estándares del sector.

**PDF/X-1a 2001:** comprueba los trabajos entrantes para comprobar si son compatibles con PDF/X-1a y crea archivos PDF únicamente si son compatibles. PDF/X-1a es un estándar ISO para el intercambio de contenido gráfico. PDF/X-1a requiere que todas las fuentes estén incrustadas, que se especifiquen los cuadros PDF adecuados y que el color aparezca como CMYK o manchas de color. Los archivos PDF que cumplen los requisitos de PDF/X-1a están dirigidos a una condición de salida específica, como la impresión de desplazamiento web según las Publicaciones de Desplazamiento web de Especificaciones. Para obtener más información sobre PDF/X, consulte Adobe y estándares del sector.

**PDF/X-3 2002:** comprueba los trabajos entrantes para comprobar si son compatibles con PDF/X-3 y crea archivos PDF únicamente si son compatibles. Al igual que PDF/X-1a, PDF/X-3 es un estándar ISO para el intercambio de contenido gráfico. La diferencia principal es que PDF/X-3 admite color independiente del dispositivo.

**Calidad de prensa:** crea archivos PDF para una producción de impresión de alta calidad (por ejemplo, en un selector de imágenes o un platesetter). En este caso, el tamaño del archivo no es una consideración. El objetivo es mantener toda la información en un archivo PDF que una impresora comercial o un proveedor de servicios de preimpresión necesitan para imprimir el documento correctamente. Este conjunto de opciones:

* baja resolución de imágenes en color y escala de grises a 300 ppp
* baja imágenes monocromas a 1200 ppp
* incrusta subconjuntos de todas las fuentes utilizadas en el documento
* impresiones a una resolución de imagen más alta,
* no rota automáticamente las páginas en función de la orientación de los comentarios de las convenciones de estructuración de texto o documentos (DSC)
* utiliza otros ajustes para conservar la cantidad máxima de información sobre el documento original.

Los trabajos de impresión fallan si tienen fuentes que no se pueden incrustar. Estos archivos PDF se pueden abrir en Acrobat 5 y Acrobat Reader 5 y posteriores.

>[!NOTE]
>
>Antes de crear un archivo PDF para enviarlo a una impresora comercial o a un proveedor de servicios de preimpresión, determine la resolución de salida y otros ajustes, o solicite un archivo .joboptions con los ajustes recomendados. Es posible que tenga que personalizar la configuración de Adobe PDF de un proveedor en particular y, a continuación, proporcionar su propio archivo .joboptions .

**Tamaño de archivo más pequeño:** crea archivos PDF para mostrarlos en la web o en una intranet, o para distribuirlos a través de un sistema de correo electrónico para visualizarlos en pantalla. Este conjunto de opciones utiliza compresión, disminución de resolución y una resolución de imagen relativamente baja. Convierte todos los colores a sRGB y no incrusta fuentes a menos que sea necesario. También optimiza los archivos para el servicio de bytes. Estos archivos PDF se pueden abrir en Acrobat 5 y Acrobat Reader 5.0 y posteriores.

**Estándar:** crea archivos PDF para imprimirlos en impresoras de escritorio o fotocopiadoras digitales, publicarlos en un CD o enviarlos a un cliente como prueba de publicación. Este conjunto de opciones utiliza compresión y disminución de resolución para reducir el tamaño del archivo. También incrusta subconjuntos de todas las fuentes que se utilizan en el archivo, convierte todos los colores a sRGB e imprime a una resolución media para crear una representación razonablemente precisa del documento original. Tenga en cuenta que los subconjuntos de fuentes de Microsoft Windows no están incrustados de forma predeterminada. Estos archivos PDF se pueden abrir en Acrobat 5 y Acrobat Reader 5.0 y posteriores.

## Agregar o editar la configuración de PDF {#add-or-edit-pdf-settings}

La configuración de PDF determina con precisión cómo se convierten los archivos y su estructura y características de PDF resultantes. Defina una nueva configuración de PDF o edite una que haya creado anteriormente. No puede modificar la configuración predefinida, pero puede crear una configuración basada en una existente editando la configuración y guardarla con un nombre nuevo.

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Configuración de Adobe PDF.
1. Haga clic en Nuevo o en el nombre de una configuración existente.
1. En la página Nueva/Editar configuración de Adobe PDF , complete la información requerida en estas secciones:

   [Opciones generales](configuring-pdf-settings.md#general-options)

   [Opciones de imágenes](configuring-pdf-settings.md#images-options)

   [Opciones de fuentes](configuring-pdf-settings.md#fonts-options)

   [Opciones de color](configuring-pdf-settings.md#color-options)

   [Opciones avanzadas](configuring-pdf-settings.md#advanced-options)

   [Opciones de informes y cumplimiento de normas](configuring-pdf-settings.md#standards-reporting-and-compliance-options)

   [Opciones de vista inicial](configuring-pdf-settings.md#initial-view-options)

   Para ir a otra sección, haga clic en su vínculo en la página web o utilice los botones Next y Previous .

1. Después de completar la información en todas las secciones, haga clic en Guardar o Guardar como y proporcione un nombre para la configuración.

## Cargar configuración de PDF {#upload-pdf-settings}

Puede tener la configuración de PDF disponible en el servidor de PDF Generator cargándolos desde un equipo local o una ubicación de red.

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Configuración de Adobe PDF y, a continuación, haga clic en Cargar.
1. En la página Cargar configuración de Adobe PDF , haga clic en Examinar, busque el archivo de configuración de PDF y haga clic en Abrir.
1. Haga clic en Aceptar y, a continuación, en Aceptar de nuevo.

## Eliminar configuración de PDF {#delete-pdf-settings}

Puede eliminar permanentemente la configuración de PDF si ya no es necesaria.

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Configuración de Adobe PDF.
1. Seleccione la casilla de verificación situada junto a la configuración que desea eliminar. Puede seleccionar varias opciones de configuración.
1. Haga clic en Eliminar y, en la página Confirmación de eliminación, haga clic de nuevo en Eliminar.

## Opciones generales {#general-options}

Utilice las opciones generales para especificar la versión de Acrobat que se utilizará para la compatibilidad de archivos y otras opciones de archivos y dispositivos. Para obtener instrucciones sobre el acceso a las opciones generales, consulte [Agregar o editar la configuración de PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

### Opciones de archivo {#file-options}

**Compatibilidad:** el nivel de compatibilidad del archivo PDF. Para documentos que se distribuirán ampliamente, considere la posibilidad de seleccionar Acrobat 4 (PDF 1.3) o Acrobat 5 (PDF 1.4) para garantizar que todos los usuarios puedan ver e imprimir el documento. Si crea archivos con compatibilidad con Acrobat 5 o versiones posteriores, es posible que no sean compatibles con versiones anteriores de Acrobat. Las siguientes subsecciones muestran algunas de las diferencias entre los archivos PDF que se crean con distintos niveles de compatibilidad con Acrobat.

<table>
 <tbody>
  <tr>
   <th><p>Acrobat 4 (PDF 1.3)</p> </th>
   <th><p>Acrobat 5 (PDF 1.4)</p> </th>
   <th><p>Acrobat 6 (PDF 1.5)</p> </th>
   <th><p>Acrobat 7 (PDF 1.6) y Acrobat 8 (PDF 1.7)</p> </th>
  </tr>
  <tr>
   <td><p>Se puede abrir con Acrobat 3.0 y Acrobat Reader 3.0 y posteriores.</p> </td>
   <td><p>Se puede abrir con Acrobat 3.0 y Acrobat Reader 3.0 y posteriores. Las funciones específicas de versiones posteriores pueden perderse o no verse.</p> </td>
   <td><p>La mayoría se puede abrir con Acrobat 4 y Acrobat Reader 4.0 y posteriores. Las funciones específicas de versiones posteriores pueden perderse o no verse.</p> </td>
   <td><p>La mayoría se puede abrir con Acrobat 4 y Acrobat Reader 4.0 y posteriores. Las funciones específicas de versiones posteriores pueden perderse o no verse.</p> </td>
  </tr>
  <tr>
   <td><p>No puede contener ilustraciones que utilicen efectos de transparencia en directo. Cualquier transparencia debe aplanarse antes de convertirse a PDF 1.3.</p> </td>
   <td><p>Admite el uso de transparencia en vivo en ilustraciones. (La función de Acrobat Distiller aplana la transparencia).</p> </td>
   <td><p>Admite el uso de transparencia en vivo en ilustraciones. (La función de Acrobat Distiller aplana la transparencia).</p> </td>
   <td><p>Admite el uso de transparencia en vivo en ilustraciones. (La función de Acrobat Distiller aplana la transparencia).</p> </td>
  </tr>
  <tr>
   <td><p>Las capas no son compatibles.</p> </td>
   <td><p>Las capas no son compatibles.</p> </td>
   <td><p>Conserva las capas cuando crea archivos PDF a partir de aplicaciones que admiten la generación de documentos PDF en capas, como Adobe Illustrator® CS o Adobe InDesign® CS y posteriores.</p> </td>
   <td><p>Conserva las capas al crear archivos PDF a partir de aplicaciones que admiten la generación de documentos PDF en capas, como Illustrator CS o InDesign CS y posteriores.</p> </td>
  </tr>
  <tr>
   <td><p>Se admite el espacio de color DeviceN con 8 colorantes.</p> </td>
   <td><p>Se admite el espacio de color DeviceN con 8 colorantes.</p> </td>
   <td><p>Se admite el espacio de color DeviceN con hasta 31 colorantes.</p> </td>
   <td><p>Se admite el espacio de color DeviceN con hasta 31 colorantes.</p> </td>
  </tr>
  <tr>
   <td><p>Se pueden incrustar fuentes multibyte. (Distiller convierte las fuentes al incrustar.)</p> </td>
   <td><p>Se pueden incrustar fuentes multibyte.</p> </td>
   <td><p>Se pueden incrustar fuentes multibyte.</p> </td>
   <td><p>Se pueden incrustar fuentes multibyte.</p> </td>
  </tr>
  <tr>
   <td><p>Se admite la seguridad RC4 de 40 bits.</p> </td>
   <td><p>Se admite la seguridad RC4 de 128 bits.</p> </td>
   <td><p>Se admite la seguridad RC4 de 128 bits.</p> </td>
   <td><p>Se admite la seguridad RC4 de 128 bits y AES (Estándar de codificación avanzada) de 128 bits.</p> </td>
  </tr>
 </tbody>
</table>

**Compresión de nivel de objeto:** consolida objetos pequeños (cada uno de los cuales no se puede comprimir por sí mismo) en flujos que luego se pueden comprimir de forma eficaz.

**Desactivado:** no comprime ninguna información estructural del documento PDF. Seleccione esta opción si desea que los usuarios vean, naveguen e interactúen con marcadores y otra información estructural usando Acrobat 5 y posterior.

**Solo etiquetas:** comprime la información estructural del documento PDF. El uso de esta opción da como resultado un archivo PDF que se puede abrir e imprimir con Acrobat 5. Los usuarios no pueden ver ninguna información de accesibilidad, estructura o PDF etiquetado en Acrobat 5 o Acrobat Reader 5.0, pero sí pueden ver esta información en Acrobat 6 y Adobe Reader 6.0.

**Rotar páginas automáticamente:** establece la rotación automática de las páginas en función de la orientación del texto o de los comentarios del DSC. Por ejemplo, algunas páginas (como las páginas que contienen tablas) pueden requerir que el usuario las ponga de lado para leerlas. Seleccione Individualmente para rotar cada página en función de la dirección del texto de esa página. Seleccione Colectivamente Por archivo para girar todas las páginas del documento en función de la orientación de la mayoría del texto.

>[!NOTE]
>
>Si está seleccionado Procesar comentarios de DSC en la Configuración avanzada y si se incluyen los comentarios %%Visualización de orientación , estos comentarios tienen prioridad a la hora de determinar la orientación de la página.

**Enlace:** especifica si se mostrará un archivo PDF con un enlace del lado izquierdo o derecho. Esta configuración afecta a la visualización de las páginas en la página principal: diseño continuo y visualización de miniaturas una al lado de la otra.

**Resolución:** establece la emulación de la resolución de una impresora para los archivos de entrada que ajustan su comportamiento según la resolución de la impresora a la que imprimen. Para la mayoría de los archivos de entrada, una configuración de mayor resolución da como resultado archivos PDF más grandes pero de mayor calidad, y una configuración más baja da como resultado archivos PDF más pequeños pero de menor calidad. Normalmente, la resolución determina el número de pasos de un degradado o una mezcla. Puede introducir un valor entre 72 y 4000. Mantenga esta configuración como predeterminada a menos que planifique imprimir el archivo PDF en una impresora específica y desee emular la resolución definida en el archivo de entrada original.

>[!NOTE]
>
>Al aumentar la configuración de resolución, aumenta el tamaño del archivo y puede aumentar ligeramente el tiempo necesario para procesar algunos archivos.

**Todas las páginas o páginas de:** especifica qué páginas convertir. Deje vacío el cuadro Para para crear un rango desde el número de página que escriba en el cuadro Desde al final del archivo.

**Optimizar para vista rápida en Web:** Reestructura el archivo para la descarga de página a página (servicio de bytes) desde servidores Web. Esta opción comprime el texto y el arte lineal, independientemente de lo que haya seleccionado como configuración de compresión en la ficha Imágenes . La compresión hace que el acceso y la visualización sean más rápidos al descargar el archivo desde la web o una red. De forma predeterminada, esta opción no está activada.

### Tamaño de página predeterminado {#default-page-size}

Las opciones Tamaño de página predeterminado especifican el tamaño de página que se debe usar cuando no se especifica ninguno en el archivo original. Normalmente, los archivos Adobe PostScript incluyen esta información, excepto los archivos PostScript encapsulados (EPS), que proporcionan un tamaño de cuadro delimitador pero no un tamaño de página. El tamaño máximo de página permitido es de 31 800 000 cm (15 000 000 pulgadas) en cualquier dirección. Estas opciones configuran el tamaño predeterminado de la página:

**Anchura:** Anchura de la página

**Altura:** altura de la página

**Unidades:** unidades que se deben usar para la configuración de anchura y altura

## Opciones de imágenes {#images-options}

Las opciones de Imágenes especifican la compresión y el remuestreo de las imágenes. Puede experimentar con estas opciones para encontrar un equilibrio adecuado entre el tamaño del archivo y la calidad de la imagen. Para obtener instrucciones sobre el acceso a la configuración de imágenes, consulte [Agregar o editar la configuración de PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Estas opciones configuran imágenes en color, escala de grises y monocromo:

**Descargar muestra:** establezca un valor para cada tipo de imagen. Para reducir la muestra de imágenes en color, escala de grises o monocromas, PDF Generator combina píxeles en un área de muestra para aumentar el tamaño de un píxel. Proporcione la resolución de su dispositivo de salida en puntos por pulgada (dpi) e introduzca una resolución en dpi en el cuadro Para imágenes arriba. Para imágenes con una resolución por encima de este umbral, PDF Generator combina píxeles, según sea necesario, para reducir la resolución de la imagen (píxeles por pulgada) a la configuración de ppp especificada. Para desactivar la disminución de resolución, seleccione Desactivado. Estas son las opciones:

**Media de disminución de resolución a:** obtiene el promedio de píxeles en un área de muestra y reemplaza toda el área con el color promedio de píxeles en la resolución especificada.

**Bicúbico a:** utiliza una media ponderada para determinar el color de los píxeles y normalmente produce mejores resultados que el simple método de promedio de disminución de resolución. Bicúbico es el método más lento pero más preciso y resulta en las gradaciones tonales más suaves.

**Submuestreo a:** selecciona un píxel en el centro del área de muestra y reemplaza todo el área con ese píxel en la resolución especificada. El submuestreo reduce significativamente el tiempo de conversión en comparación con la disminución de resolución, pero resulta en imágenes menos suaves y continuas.

La configuración de resolución para color y escala de grises debe ser de 1,5 a 2 veces la configuración de la pantalla de línea en la que se imprimirá el archivo. (Siempre que no se sitúe por debajo de esta configuración de resolución recomendada, las imágenes que no contengan líneas rectas o patrones geométricos o repetitivos no se verán afectadas por una resolución inferior). La resolución de las imágenes monocromas debe ser la misma que la del dispositivo de salida. Sin embargo, tenga en cuenta que al guardar una imagen monocromática con una resolución superior a 1500 ppp, se aumenta el tamaño del archivo sin mejorar considerablemente la calidad de la imagen.

También considere si los usuarios necesitan ampliar una página. Por ejemplo, si está creando un documento PDF de un mapa, considere la posibilidad de usar una resolución de imagen más alta para que los usuarios puedan acercar el mapa.

>[!NOTE]
>
>El remuestreo de imágenes monocromas puede tener resultados de visualización inesperados, como que no se muestre ninguna imagen. Si se produce este problema, desactive el remuestreo y vuelva a convertir el archivo. Es muy probable que este problema ocurra con el submuestreo y que el menor número de casos se produzca con la disminución de la resolución de la bibliografía.

Esta tabla muestra los tipos de impresoras y su resolución medida en dpi, su regla de pantalla predeterminada medida en líneas por pulgada (lpi) y una resolución de remuestreo para imágenes que se miden en píxeles por pulgada (ppi). Por ejemplo, para imprimir en una impresora láser de 600 ppp, escriba 170 para que la resolución vuelva a muestrear las imágenes en.

<table>
 <tbody>
  <tr>
   <th><p>Resolución de la impresora</p> </th>
   <th><p>Pantalla de línea predeterminada</p> </th>
   <th><p>Resolución de imágenes</p> </th>
  </tr>
  <tr>
   <td><p>300 ppp (impresora láser)</p> </td>
   <td><p>60 lpi</p> </td>
   <td><p>120 ppp</p> </td>
  </tr>
  <tr>
   <td><p>600 ppp (impresora láser)</p> </td>
   <td><p>85 lpi</p> </td>
   <td><p>170 ppp</p> </td>
  </tr>
  <tr>
   <td><p>1200 ppp (imagen)</p> </td>
   <td><p>120 lpi</p> </td>
   <td><p>240 ppp</p> </td>
  </tr>
  <tr>
   <td><p>2400 ppp (imagen)</p> </td>
   <td><p>150 lpi</p> </td>
   <td><p>300 ppp</p> </td>
  </tr>
 </tbody>
</table>

**Compresión:** establezca un valor para aplicarlo a imágenes en color, escala de grises y monocromas. Para las imágenes en color y escala de grises, también establezca la calidad de la imagen:

* Para imágenes en color o escala de grises, seleccione ZIP para aplicar compresión que funcione bien en imágenes que tengan grandes áreas de colores únicos o patrones repetitivos. Algunos ejemplos son las capturas de pantalla, las imágenes simples creadas con programas de pintura y las imágenes monocromas que contienen patrones repetitivos. Seleccione JPEG, calidad mínima hasta el máximo, para aplicar compresión adecuada para imágenes en escala de grises o en color, como fotografías en tono continuo que contengan más detalle del que se puede reproducir en la pantalla o en la impresión. Seleccione Automático (JPEG) para determinar automáticamente la mejor calidad para las imágenes en color y escala de grises.
* Para las imágenes monocromas, seleccione compresión CCITT Grupo 4, CCITT Grupo 3, ZIP, JPEG200, Automático (JPEG2000) o Ejecutar longitud.

Asegúrese de que las imágenes monocromas se escanean como monocromas y no como escala de grises. El texto digitalizado a veces se guarda como imágenes en escala de grises de forma predeterminada. El texto en escala de grises comprimido con el método de compresión JPEG no es claro y puede ser ilegible.

**Calidad de imagen:** configura la calidad de imagen para las imágenes en color y en escala de grises. Las opciones son mínimo, bajo, medio, alto y máximo.

**Suavizado A gris:** suaviza los bordes dentados en imágenes monocromas. Seleccione 2 bits, 4 bits u 8 bits para especificar 4, 16 o 256 niveles de gris. (El suavizado puede desenfocar líneas pequeñas o delgadas.)

>[!NOTE]
>
>La compresión de texto y arte lineal siempre está activada.

**Política de imagen:** defina una política para imágenes en color, escala de grises y monocromas. Si la resolución de la imagen es inferior a la resolución especificada, puede seleccionar continuar (Ignorar), proporcionar un mensaje de advertencia o cancelar el trabajo.

## Opciones de fuentes {#fonts-options}

Las opciones de fuentes especifican qué fuentes se van a incrustar en un archivo PDF y si se va a incrustar un subconjunto de caracteres que se utilizan en el archivo PDF. Para obtener instrucciones sobre el acceso a las opciones de fuentes, consulte [Agregar o editar la configuración de PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

>[!NOTE]
>
>Cuando se combinan archivos PDF con el mismo subconjunto de fuentes, PDF Generator intenta combinar los subconjuntos de fuentes.

**Incrustar todas las fuentes:** incrusta todas las fuentes que se utilicen en el archivo. La incrustación de fuentes es necesaria para la compatibilidad con PDF/X.

**Subconjunto de fuentes incrustadas cuando el porcentaje de caracteres utilizados es menor que:** si selecciona esta opción, especifique un porcentaje de umbral para incrustar solo un subconjunto de las fuentes. Por ejemplo, si el umbral es 35 y se utilizan menos del 35 % de los caracteres, PDF Generator incrusta solo esos caracteres. Solo se incrustan las fuentes con bits de permiso adecuados.

**Al incrustar errores:** especifica cómo responde PDF Generator si no encuentra una fuente que incrustar al procesar un archivo. Puede hacer que PDF Generator ignore la solicitud y sustituya la fuente, avise y sustituya la fuente, o cancele el procesamiento del trabajo actual.

**Fuente:** la ubicación de las fuentes que utiliza PDF Generator.

### Especificar qué fuentes incrustar {#specify-which-fonts-to-embed}

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Configuración de Adobe PDF.
1. Haga clic en Nuevo o en el nombre de una configuración.
1. Haga clic en Fuentes y anule la selección de Incrustar todas las fuentes.
1. En la lista Fuente, seleccione una fuente de fuente y haga clic en Ir para actualizar la lista de fuentes en el cuadro de la izquierda.
1. Haga clic en una fuente en el cuadro de la izquierda. A continuación, haga clic en Agregar , al lado del cuadro correspondiente, para moverlo a la lista Incrustar siempre o Nunca incrustar. Repita el proceso para cada fuente. Utilice la tecla Ctrl y haga clic para seleccionar varias fuentes que desee mover.
1. Para eliminar una fuente de la lista Incrustar siempre o No incrustar nunca, selecciónela y haga clic en Quitar, al lado del cuadro correspondiente. Esta acción no elimina la fuente del sistema; solo elimina la referencia a él en la lista.
1. Si la fuente que desea especificar no aparece, escriba su nombre en el cuadro Agregar fuente y, a continuación, haga clic en Incrustar siempre o No incrustar nunca. Los nombres de fuentes no pueden contener caracteres alfanuméricos.

>[!NOTE]
>
>Una fuente TrueType puede contener un ajuste que agregó el diseñador de fuentes que impide que la fuente se incruste en archivos PDF.

>[!NOTE]
>
>Las fuentes se seleccionan de la caché de fuentes del sistema de Windows y es necesario reiniciar el sistema para actualizar la caché. Después de especificar el directorio de fuentes del cliente, asegúrese de reiniciar el sistema en el que está instalado AEM formulario.

## Opciones de color {#color-options}

Las opciones de color definen toda la información de gestión de color para PDF Generator. Para obtener instrucciones sobre el acceso a las opciones de color, consulte [Agregar o editar la configuración de PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

### Configuración de Adobe Color {#adobe-color-settings}

**Archivo de configuración:** esta lista contiene una lista de configuraciones de color que también se utilizan en las principales aplicaciones gráficas, como Adobe Photoshop y Adobe Illustrator. La configuración de color que seleccione determina los demás ajustes de color del Adobe de esta página. Por ejemplo, si selecciona una configuración que no sea Ninguno, todas las opciones que no sean las de Datos dependientes del dispositivo estarán predefinidas y atenuadas. Solo puede editar la configuración de Políticas de administración de color y Espacios de trabajo si selecciona Ninguno en Archivo de configuración.

### Políticas de administración de color {#color-management-policies}

Si seleccionó Ninguno en el Archivo de configuración, el área Políticas de administración de color especifica cómo el Generador de PDF convierte el color no administrado en un archivo PostScript.

**Dejar color sin cambiar:** mantiene los colores dependientes del dispositivo sin modificar y conserva los colores independientes del dispositivo como el equivalente más cercano posible en PDF. Esta opción es útil para imprimir tiendas que han calibrado todos sus dispositivos, utilizado esa información para especificar el color del archivo y mostrar sólo a esos dispositivos.

**Etiquete todo para la gestión de color:** incrusta un perfil de International Color Consortium al dividir archivos y calibrar el color en las imágenes, lo que hace que los colores de los archivos PDF resultantes sean independientes del dispositivo si ha seleccionado la compatibilidad con Acrobat 4 (PDF 1.3) o posterior. Sin embargo, los espacios de color dependientes del dispositivo en los archivos (RGB, escala de grises y CMYK) se convierten en espacios de color independientes del dispositivo (CalRGB, CalGray y LAB).

**Etiquetar solo imágenes para la gestión de color:** incrusta perfiles ICC solo en imágenes, no en texto ni en gráficos, al dividir archivos si ha seleccionado la compatibilidad con Acrobat 4 (PDF 1.3). Esta opción evita que el texto negro experimente cualquier cambio de color. Sin embargo, los espacios de color dependientes del dispositivo en las imágenes (RGB, escala de grises y CMYK) se convierten en espacios de color independientes del dispositivo (CalRGB, CalGray y LAB). El texto y los gráficos no se convierten.

**Convertir todos los colores a sRGB o Convertir todos los colores a CMYK:** califica el color en el archivo, haciendo que el color sea independiente del dispositivo, similar a Etiquetar todo para la gestión del color. Si ha seleccionado la compatibilidad con Acrobat 4 (PDF 1.3) o versiones posteriores y ha convertido a sRGB, las imágenes CMYK y RGB se convierten a sRGB.

Independientemente de la opción de compatibilidad seleccionada, las imágenes en escala de grises no cambian. Esto generalmente reduce el tamaño y aumenta la velocidad de visualización de los archivos PDF porque se necesita menos información para describir imágenes RGB que para describir imágenes CMYK. Como RGB es el espacio de color nativo que se utiliza en los monitores, no es necesario realizar ninguna conversión de color durante la visualización, lo que contribuye a una visualización en línea más rápida. Esta opción se recomienda si el archivo PDF se utiliza en línea o con impresoras de baja resolución.

**Interpretación de documentos:** Método para asignar colores entre espacios de color. El resultado de cualquier método en particular depende de los perfiles de los espacios de color. Por ejemplo, algunos perfiles producen resultados idénticos con métodos diferentes. Las opciones disponibles son:

>[!NOTE]
>
>En todos los casos, las operaciones de gestión de color que se producen tras la creación del archivo PDF pueden ignorar o anular las intenciones.

**Conservar:** significa que la intención se especifica en el dispositivo de salida en lugar de en el archivo PDF. En muchos dispositivos de salida, la opción Colorimétrica relativa es la intención predeterminada.

**Perceptual:** mantiene los valores de color relativos entre los píxeles originales a medida que se asignan a la gama de destino. Este método conserva la relación visual entre los colores, aunque los valores de color pueden cambiar.

**Saturación:** mantiene los valores de saturación relativos de los píxeles originales. Este método es adecuado para gráficos empresariales, donde la relación exacta entre colores no es tan importante como tener colores saturados brillantes.

**Métrica de color relativa:** reasigna el punto blanco del espacio de origen al punto blanco del espacio de destino.

**Colorimétrico absoluto:** deshabilita la coincidencia de puntos blancos y negros al convertir colores. Este método no se recomienda a menos que deba conservar los colores de firma, como los utilizados en marcas comerciales o logotipos.

### Espacios de trabajo {#working-spaces}

Para todos los valores de la lista en Políticas de administración de color, que no sean Dejar color sin cambiar, seleccione entre las listas del área Espacio de trabajo para especificar qué perfiles ICC se utilizan para definir y calibrar los espacios de color de escala de grises, RGB y CMYK en archivos PDF destilados. Las opciones disponibles son:

**Gris:** define el espacio de color de todas las imágenes en escala de grises de los archivos. Esta opción solo está disponible si elige Etiquetar todo para la administración de color o Etiquetar solo imágenes para la administración de color. El perfil ICC predeterminado para imágenes grises es Gray Gamma 2.2. También puede seleccionar Ninguno para evitar que las imágenes en escala de grises se conviertan.

**RGB:** define el espacio de color de todas las imágenes RGB de los archivos. El valor predeterminado, sRGB IEC61966-2.1, es generalmente una buena opción porque se está convirtiendo en un estándar del sector y muchos dispositivos de salida lo reconocen. También puede seleccionar Ninguno para evitar que las imágenes RGB se conviertan.

**CMYK:** define el espacio de color de todas las imágenes CMYK de los archivos. El valor predeterminado es U.S. Web Coated (SWOP) v2. También puede seleccionar Ninguno para evitar que las imágenes CMYK se conviertan.

>[!NOTE]
>
>Seleccionar Ninguno para los tres espacios de trabajo tiene el mismo efecto que seleccionar Dejar color sin cambiar.

**Preservar valores CMYK para espacios de color CMYK calibrados:** cuando se selecciona, los valores CMYK independientes del dispositivo se tratan como valores dependientes del dispositivo (DeviceCMYK), los espacios de color independientes del dispositivo se descartan y los archivos PDF/X-1a utilizan el valor Convertir todos los colores a CMYK. Cuando se anula la selección, los espacios de color independientes del dispositivo se convierten a CMYK si la política de gestión de color está establecida en Convertir todos los colores a CMYK.

### Datos dependientes del dispositivo {#device-dependent-data}

Estas opciones se aplican si trabaja con documentos creados con aplicaciones gráficas y de documentación de high-end, como Adobe Illustrator y Adobe InDesign. Para obtener más información, consulte la documentación que acompaña a la aplicación.

Las funciones de transferencia se utilizan para efectos artísticos y para ajustar las especificaciones de un dispositivo de salida específico. Por ejemplo, un archivo que se va a generar en una imagen concreta puede contener funciones de transferencia que compensen la ganancia de puntos inherente a esa impresora.

**Mantener en Eliminación de color y Generación de negro:** conserva esta configuración si existe en el archivo PostScript. La generación de negro calcula la cantidad de negro que se utilizará al intentar reproducir un color determinado. La eliminación de color inferior (UCR) reduce la cantidad de componentes cian, magenta y amarillo para compensar la cantidad de negro que agregó la generación negra. Debido a que utiliza menos tinta, el UCR se utiliza generalmente para papel de periódico y material sin estucar.

**Cuando se encuentran funciones de transferencia:**  determina qué hacer cuando se encuentran funciones de transferencia:

**Preservar:** conserva las funciones de transferencia que se utilizan tradicionalmente para compensar la ganancia de puntos o la pérdida de puntos que pueden producirse cuando se transfiere una imagen a una película. La ganancia de puntos se produce cuando los puntos de tinta que componen una imagen impresa son más grandes (por ejemplo, debido a la propagación en papel) que en la pantalla de semitonos; la pérdida de puntos se produce cuando los puntos se imprimen más pequeños. Con esta opción, las funciones de transferencia se mantienen como parte del archivo y se aplican al archivo cuando se genera el archivo.

**Aplicar:** no conserva la función de transferencia, pero la aplica al archivo, que cambia los colores del archivo. Esta opción resulta útil para crear efectos de color en un archivo. De forma predeterminada, esta opción está seleccionada para las nuevas configuraciones.

**Eliminar:** quita todas las funciones de transferencia aplicadas. Elimine las funciones de transferencia aplicadas a menos que el archivo PDF se envíe al mismo dispositivo para el que se creó el archivo PostScript de origen.

**Conservar información de semitonos:** conserva toda la información de semitonos de los archivos. La información de semitonos consiste en puntos que controlan cuánto depositan los dispositivos de semitonos de tinta en una ubicación específica del papel. Modificar el tamaño y la densidad del punto crea la ilusión de variaciones de color gris o continuo. Para una imagen CMYK, se utilizan cuatro pantallas de semitonos, una para cada tinta que se utiliza en el proceso de impresión.

En la producción de impresión tradicional, se produce un semitono colocando una pantalla de semitonos entre una pieza de película y la imagen, y luego exponiendo la película. Los equivalentes electrónicos, como en Adobe Photoshop, permiten a los usuarios especificar los atributos de pantalla de semitonos antes de producir la película o el papel. La información de semitonos está pensada para su uso con un dispositivo de salida específico.

## Opciones avanzadas {#advanced-options}

Las opciones avanzadas especifican qué convenciones de estructura de documentos (DSC) se deben mantener en el archivo PDF y cómo se establecen otras opciones que afectan a la conversión desde PostScript. En un archivo PostScript, los comentarios de DSC contienen información sobre el archivo (como la aplicación original, la fecha de creación y la orientación de la página). También proporcionan estructura para las descripciones de página en el archivo (como las instrucciones de inicio y finalización para una sección de prólogo). Los comentarios de DSC pueden ser útiles cuando el documento se va a imprimir o presionar. Para obtener instrucciones sobre el acceso a las opciones avanzadas, consulte [Agregar o editar la configuración de PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Al trabajar con las opciones avanzadas, resulta útil tener una comprensión del lenguaje PostScript y de cómo se traduce a PDF. (Consulte [Adobe PostScript 3](https://www.adobe.com/products/postscript/main.html)).

**Permitir que el archivo PostScript anule la configuración de Adobe PDF:** utiliza la configuración almacenada en un archivo PostScript en lugar del archivo de configuración actual de Adobe PDF. Antes de procesar un archivo PostScript, puede colocar parámetros en el archivo para controlar los siguientes aspectos:

* compresión de texto y gráficos
* disminución de resolución y codificación de imágenes muestreadas
* incrustación de fuentes Tipo 1 e instancias de fuentes Tipo 1 Múltiples fuentes Maestras

**Permitir XObjects PostScript:** los XObjects PostScript almacenan información que aparece en muchas páginas del mismo archivo, como una imagen de fondo o información de encabezado y pie de página. El uso de XObjects PostScript puede dar como resultado una impresión más rápida, pero requiere más memoria de impresora. Para evitar que se creen XObjects PostScript, anule la selección de esta opción si crea archivos PDF con compatibilidad con Acrobat 5 (PDF 1.4) o posterior.

**Convertir degradados en sombras suaves:** convierte mezclas en sombras suaves para Acrobat 4 y versiones posteriores, reduciendo los archivos PDF y mejorando potencialmente la calidad de la salida final. PDF Generator convierte los degradados de Adobe Illustrator, Adobe InDesign, Adobe FreeHand MX, CorelDraw, Quark Xpress y Microsoft PowerPoint.

**Convertir líneas suavizadas en curvas:**  reduce la cantidad de puntos de control utilizados para crear curvas en dibujos CAD, lo que da como resultado PDF más pequeños y un procesamiento en pantalla más rápido.

**Conservar semántica de copypage de nivel 2:** utiliza el operador de copypage definido en PostScript de nivel de idioma 2 en lugar de en PostScript de nivel de idioma 3. Si tiene un archivo PostScript y selecciona esta opción, un operador de copypage copia la página. Si no se selecciona esta opción, se ejecuta el equivalente de una operación showpage, pero el estado gráfico no se reinicia.

**Conservar configuración de sobreimpresión:** conserva cualquier configuración de sobreimpresión en archivos que se están convirtiendo a PDF. Los colores sobreimpresos son dos o más tintas impresas sobre las otras. Por ejemplo, cuando una tinta cian se imprime sobre una tinta amarilla, la sobreimpresión resultante es de color verde. Sin sobreimpresión, el amarillo subyacente no se imprime, lo que da como resultado un color cian.

**La sobreimpresión predeterminada es distinta de la sobreimpresión:**  evita que los objetos sobreimpresos con valores CMYK nulos caigan en los objetos CMYK que están debajo de ellos. Este efecto se logra insertando el parámetro de estado de gráficos OPM 1 en el archivo PDF donde esté presente el operador Setoverprint .

**Guardar configuración de Adobe PDF dentro del archivo PDF:** incrusta el archivo de configuración utilizado para crear el archivo PDF. Puede abrir y ver el archivo de configuración (que tiene la extensión de nombre de archivo .joboptions) en el cuadro de diálogo Archivos adjuntos de Acrobat. El archivo de configuración de Adobe PDF se convierte en un elemento del árbol EmbeddedFiles dentro del archivo PDF.

**Guardar imágenes JPEG originales en PDF Si es posible:** procesa las imágenes JPEG comprimidas (imágenes que ya se han comprimido con codificación DCT) sin volver a comprimirlas. Si se selecciona esta opción, PDF Generator descomprime las imágenes JPEG para asegurarse de que no estén dañadas. Sin embargo, no vuelve a comprimir imágenes válidas, por lo que el procesamiento de la imagen original no se ha tocado. Con esta opción seleccionada, el rendimiento mejora porque solo se produce la descompresión (no la recompresión) y se conservan los datos y los metadatos de la imagen.

**Guardar ticket de trabajo portátil dentro del archivo PDF:** conserva un ticket de trabajo de PostScript en un archivo PDF. El ticket de trabajo contiene información sobre el archivo PostScript, como el tamaño de la página, la resolución y la información de reventado, en lugar de información sobre el contenido. Esta información se puede utilizar más adelante en un flujo de trabajo o para imprimir el PDF.

**Use Prolog.ps y Epilog.ps:** envía un archivo de prólogo y epilog con cada trabajo. Estos archivos tienen muchos propósitos. Por ejemplo, se pueden editar los archivos de perfil para especificar las portadas. Los archivos Epilog se pueden editar para resolver una serie de procedimientos en un archivo PostScript. Puede cargar o descargar los archivos. (Consulte Carga y descarga de archivos de prólogo y epílog).

**Procesar comentarios de DSC:** mantiene la información de DSC de un archivo PostScript. Estas subopciones están disponibles:

**Registrar advertencias de DSC:** muestra mensajes de advertencia sobre comentarios problemáticos de DSC durante el procesamiento y los agrega a un archivo de registro.

**Conservar información EPS de DSC:** conserva información, como la fecha de creación y la aplicación de origen de un archivo EPS. Si se anula la selección de esta opción, el tamaño y el centro de la página dependen de la esquina superior izquierda del objeto superior izquierdo y de la esquina inferior derecha del objeto inferior derecho de la página.

**Conservar comentarios de OPI:** conserva la información necesaria para reemplazar una imagen o comentario de Solo para ubicación (FPO) por la imagen de alta resolución ubicada en servidores que admiten las versiones 1.3 y 2.0 de Open Prepress Interface (OPI).

**Conservar información del documento desde DSC:** conserva información como el título, la fecha de creación y la hora. Cuando abra un archivo PDF en Acrobat, esta información aparecerá en el panel Descripción de las propiedades del documento.

**Cambiar el tamaño de las ilustraciones de página y centro para archivos EPS:** centra una imagen EPS y cambia el tamaño de la página para que se ajuste estrechamente a la imagen. Esta opción solo se aplica a los trabajos que constan de un solo archivo EPS.

## Opciones de informes y cumplimiento de normas {#standards-reporting-and-compliance-options}

PDF Generator puede comprobar el contenido del documento en un archivo PostScript para asegurarse de que cumple los criterios estándar PDF/X-1a, PDF/X-3 o PDF/A antes de crear el archivo PDF. Para archivos compatibles con PDF/X, también puede requerir que el archivo PostScript cumpla con los criterios adicionales seleccionando otras opciones en &quot;Informes de estándares y cumplimiento&quot;. La disponibilidad de las opciones depende del estándar seleccionado.

Los archivos compatibles con PDF/X se utilizan principalmente como formato estandarizado para el intercambio de archivos PDF destinados a la producción de impresión de alta resolución. A menos que esté creando un documento PDF para la producción de impresión, puede ignorar los estándares de cumplimiento de PDF/X.

Los archivos compatibles con PDF/A se utilizan principalmente para el archivado. Como la preservación a largo plazo es el objetivo, el documento debe contener sólo lo necesario para abrirlo y verlo durante toda la vida prevista del documento. Por ejemplo, los archivos compatibles con PDF/A solo pueden contener texto, imágenes rasterizadas y objetos vectoriales; no pueden contener codificación ni secuencias de comandos. Además, todas las fuentes deben incrustarse para que los documentos puedan abrirse y verse como se crearon. En otras palabras, los documentos compatibles con PDF/A son *más delgados* que sus homólogos de PDF/X, que están destinados a la producción de high-end.

>[!NOTE]
>
>Si configura una carpeta vigilada para crear archivos compatibles con PDF/A, asegúrese de no agregar seguridad a la carpeta; el estándar PDF/A no permite el cifrado.

Para obtener instrucciones sobre el acceso a las opciones de informes y cumplimiento de normas, consulte [Agregar o editar la configuración de PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

**Estándar de cumplimiento:** seleccione un estándar para generar un informe que indique si el archivo cumple los requisitos y, si no, qué problemas se han encontrado. Cuando la Compatibilidad en la página Configuración general está configurada en Acrobat 4.0, las siguientes opciones están habilitadas. Cuando la Compatibilidad se establece en Acrobat 5.0, solo las opciones de Acrobat 5.0 están disponibles para su selección. Cuando Compatibilidad se establece en una opción alternativa, las siguientes opciones aparecen atenuadas:

* PDF/X-1a (compatible con Acrobat 4.0)
* PDF/X-3 (compatible con Acrobat 4.0)
* PDF/X-1a (compatible con Acrobat 5.0)
* PDF/X-3 (compatible con Acrobat 5.0)
* PDF/A-1b (compatible con Acrobat 5.0)

### Opciones para estándares PDF/X {#options-for-pdf-x-standards}

**Cuando no es compatible:** especifica si se creará el archivo PDF si el archivo PostScript no cumple los requisitos de PDF/X. Esta opción está disponible cuando Compliance Standard en la página de informes y cumplimiento de normas está configurada en una opción distinta de None.

**Continuar:** crea un archivo PDF.

**Cancelar trabajo:** crea un archivo PDF solo si el archivo PostScript cumple los requisitos PDF/X de las opciones de informe seleccionadas y, en caso contrario, es válido. Si se seleccionan ambas opciones de informes PDF/X y el archivo PostScript solo cumple un conjunto de criterios PDF/X (por ejemplo, PDF/X-3), PDF Generator crea el archivo compatible.

**Si no se especifican ni TrimBox ni ArtBox:**  disponible cuando Compliance Standard en la página Informes y conformidad de normas está configurada en una opción distinta de None.

**Informar como error:** marca el archivo PostScript como no compatible si se selecciona una de las opciones de informes y falta un cuadro de recorte o un cuadro de arte en cualquier página.

**Establecer TrimBox en MediaBox con desplazamientos:** calcula los valores en puntos para el cuadro de recorte en función de los desplazamientos para el cuadro de medios de las páginas respectivas si no se especifica ni el cuadro de recorte ni el cuadro de arte. La caja de recorte siempre es tan pequeña o más pequeña que la caja de medios que la rodea.

**Si no se especifica BleedBox:** disponible cuando Compliance Standard en la página Informes y cumplimiento de normas está configurada en una opción distinta de None.

**Establecer BleedBox como MediaBox:** utiliza los valores de cuadro de medios para el cuadro de sangrado si no se especifica el cuadro de sangrado.

**Establezca BleedBox en TrimBox con desplazamientos:** calcula los valores en puntos del cuadro de sangrado en función de los desplazamientos del cuadro de recorte de las páginas respectivas si no se especifica el cuadro de sangrado. El cuadro de sangrado siempre es tan grande o más grande que el cuadro de guarnecido adjunto.

**Valores predeterminados si no se especifica en el documento:**  esta opción está disponible cuando Compliance Standard en la página Informes y conformidad de normas está establecida en una opción distinta de None.

**Nombre del perfil de intención de salida:** indica la condición de impresión caracterizada para la que está preparado el documento. Si un documento no especifica un nombre de OutputIntent, PDF Generator utiliza el valor seleccionado en este menú. Puede seleccionar uno de los nombres suministrados o introducir un nombre en el espacio proporcionado. Si el flujo de trabajo requiere que el documento especifique la intención de salida, seleccione Ninguno. Cualquier documento que no cumpla los requisitos falla en la comprobación de conformidad.

**Identificador de condición de salida:** indica el nombre de referencia especificado por el registro del nombre del perfil de intención de salida.

**Condición de salida:** describe la condición de impresión deseada. Esta entrada puede ser útil para el receptor deseado del documento PDF.

**Nombre del Registro (URL):** indica la dirección web para obtener más información sobre el Registro. La dirección URL se introduce automáticamente para los nombres de registro ICC.

**Reventado:** indica el estado de reventado en el documento. El cumplimiento con PDF/X requiere un valor de True o False. Si el documento no especifica el estado retenido, se utiliza el valor proporcionado aquí. Si el flujo de trabajo requiere que el documento especifique el estado retenido, seleccione Dejar sin definir. Cualquier documento que no cumpla los requisitos falla en la comprobación de conformidad.

### Opciones para PDF/A estándar {#options-for-pdf-a-standard}

Estas opciones se activan cuando Compatibilidad (en el área General) está configurada en Acrobat 4 (PDF 1.3) o Acrobat 5 (PDF 1.4).

**Cuando no es compatible:** especifica si se creará el archivo PDF si el archivo PostScript no cumple los requisitos de PDF/A.

**Continuar:** crea un archivo PDF aunque el archivo PostScript no cumpla los requisitos del estándar.

**Cancelar trabajo:** crea un archivo PDF solo si el archivo PostScript cumple los requisitos de PDF/A y por lo demás es válido.

**Nombre del perfil de calidad de salida:** indica la condición de impresión caracterizada para la que se ha preparado el documento y es necesaria para el cumplimiento de PDF/A. Si el flujo de trabajo requiere que el documento especifique la información de intento de salida, seleccione &quot;Ninguno&quot;. Si no se proporciona esta información, el documento no se verificará correctamente.

**Condición de salida:** describe la condición de impresión deseada. Esta entrada no es obligatoria, pero puede utilizarse para proporcionar información útil al destinatario deseado del documento PDF.

## Opciones de vista inicial {#initial-view-options}

Estas opciones están organizadas en tres áreas: Opciones de documento, Opciones de ventana y Opciones de interfaz de usuario. Para obtener instrucciones sobre el acceso a las opciones de la vista inicial, consulte [Agregar o editar la configuración de PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Para usar cualquier opción, seleccione Establecer configuración de vista inicial.

### Opciones de documento {#document-options}

Las opciones del documento controlan el aspecto del documento dentro de la ventana del documento, como el nivel de ampliación y cómo se desplaza.

**Mostrar:** determina qué paneles y pestañas se muestran en la ventana de la aplicación de forma predeterminada. Panel de marcadores y Página abre el panel del documento y muestra la ficha Marcadores .

**Diseño de página:** determina si el documento se ve en modo de una sola página, de cara a página, de página continua o de página opuesta continua.

**Ampliación:** establece el nivel de zoom utilizado para mostrar el documento al abrirlo. El valor predeterminado utiliza el valor de ampliación configurado por el usuario en las preferencias de Acrobat o Adobe Reader.

**Abrir a número de página:** establece la página en la que se abre el documento, que suele ser la página 1.

>[!NOTE]
>
>La configuración predeterminada para las opciones de ampliación y diseño de página utiliza la configuración de usuario individual en las preferencias de visualización de página de Acrobat o Adobe Reader.

### Opciones de ventana {#window-options}

Las opciones de la ventana determinan cómo se ajusta la ventana en el área de pantalla cuando un usuario abre el documento. Sin embargo, las opciones no tienen ningún efecto cuando un documento PDF se visualiza dentro de un explorador web.

**Cambiar el tamaño de la ventana a la página inicial:** ajusta la ventana del documento para que se ajuste perfectamente a la página de apertura, según las opciones que haya seleccionado en Opciones del documento.

**Ventana central en pantalla:** coloca la ventana en el centro del área de la pantalla.

**Abrir en modo pantalla completa:** maximiza la ventana del documento y muestra el documento sin la barra de menús, la barra de herramientas o los controles de ventana.

**Mostrar:** Nombre de archivo muestra el nombre de archivo en la barra de título de la ventana. El título del documento muestra el título del documento en la barra de título de la ventana.

### Opciones de la interfaz de usuario {#user-interface-options}

Las opciones de la interfaz de usuario determinan qué controles se muestran u ocultan cuando el usuario abre el documento.

**Ocultar barra de menús:** si está seleccionada, oculta la barra de menús

**Ocultar barras de herramientas:** si se selecciona, oculta las barras de herramientas

**Ocultar controles de ventana:** si está seleccionado, oculta los controles de ventana

>[!NOTE]
>
>Si oculta la barra de menús y la barra de herramientas, los usuarios no pueden aplicar comandos ni seleccionar herramientas a menos que conozcan los métodos abreviados de teclado cuando abren el archivo en Acrobat.

## Carga y descarga de archivos de prólogo y epilog {#uploading-and-downloading-prologue-and-epilogue-files}

Los archivos de perfiles se utilizan para agregar código PostScript personalizado que se ejecuta al principio de cada trabajo de PostScript que se destile. Los archivos de registro electrónico se utilizan para agregar código PostScript personalizado que se ejecuta al final de cada trabajo de PostScript. Puede descargar archivos de registro y epílogo del servidor para guardarlos localmente. Puede que desee descargar los archivos para configurarlos de forma independiente o cargarlos en otra ubicación o en otro equipo.

Estos archivos tienen muchos propósitos. Por ejemplo, se pueden editar los archivos de perfiles para especificar las portadas; los archivos epilog se pueden editar para resolver una serie de procedimientos en un archivo PostScript. También puede seleccionar y cargar los archivos de prólogo y epílogo para enviarlos con cada trabajo.

### Descargar un archivo de prólog o epilog {#download-a-prologue-or-epilogue-file}

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Configuración de Adobe PDF.
1. Haga clic en Nuevo o en el nombre de una configuración.
1. Haga clic en Avanzadas y, después, junto a la opción Use Prolog.ps y Epilog.ps , haga clic en Descargar.
1. En la página Descargar archivos de registro y registro electrónico, haga clic en Prolog.ps o Epilog.ps y haga clic en Guardar.

### Cargar un archivo de prólogo o epilog {#upload-a-prologue-or-epilogue-file}

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Configuración de Adobe PDF.
1. Haga clic en Nuevo o en el nombre de una configuración.
1. Haga clic en Avanzadas y, después, junto a la opción Use Prolog.ps And Epilog.ps , haga clic en Cargar.
1. En la página Cargar archivos de registro y registro electrónico , haga clic en Examinar para seleccionar un perfil o un archivo de registro electrónico.
1. Busque el archivo y haga clic en Abrir.
1. Para utilizar el archivo, asegúrese de que la opción Use Prolog.ps And Epilog.ps está seleccionada en el área Avanzado de la página Nueva/Editar configuración de Adobe PDF .
1. Haga clic en Guardar

>[!NOTE]
>
>PDF Generator admite archivos de prólogo y epílogo sólo para la conversión de archivos PostScript y Encapsulated PostScript a PDF.

