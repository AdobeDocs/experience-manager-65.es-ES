---
title: Configurar Adobe PDF
seo-title: Configuring Adobe PDF settings
description: Obtenga información sobre cómo establecer la configuración de Adobe PDF.
seo-description: Learn how to configure Adobe PDF settings.
uuid: 980c9d6a-f75e-4e7d-b050-d2d07a10ef33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab018b6d-0233-4439-bb75-58c5421d769a
feature: PDF Generator
exl-id: 1bcb8429-c06e-4bd3-b422-4c512084dd09
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '7265'
ht-degree: 0%

---

# Configurar Adobe PDF{#configuring-adobe-pdf-settings}

La página Configuración de Adobe PDF muestra la configuración de conversión que puede especificar para que la utilicen sus orígenes. Puede utilizar cualquiera de los ajustes predefinidos del PDF o crear los suyos propios. La configuración del PDF determina con precisión cómo se convierten los archivos y la estructura y características del PDF resultantes. La configuración de Adobe PDF se conocía anteriormente como parámetros de Distiller® u opciones de trabajo.

En la página Configuración de Adobe PDF, puede realizar las siguientes tareas:

* Vea la configuración predefinida del PDF. (Consulte [Acerca de la configuración predefinida del PDF](configuring-pdf-settings.md#about-the-predefined-pdf-settings).)
* Cree una configuración de PDF o edite una que haya creado anteriormente. (Consulte [Agregar o editar la configuración del PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).)
* Especifique la configuración predeterminada del PDF. (Consulte [Cambiar la configuración predeterminada](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings))
* Cargue un archivo de configuración del PDF en el servidor. (Consulte [Cargar configuración del PDF](configuring-pdf-settings.md#upload-pdf-settings).)
* Eliminar configuración de PDF personalizada. (Consulte [Eliminar configuración del PDF](configuring-pdf-settings.md#delete-pdf-settings).)
* Cargar y descargar archivos de prólogo y epílogo. (Consulte [Carga y descarga de archivos de prólogo y epílogo](configuring-pdf-settings.md#uploading-and-downloading-prologue-and-epilogue-files).)

La configuración de Adobe PDF solo se aplica a las conversiones basadas en PDFMaker. Estas incluyen las siguientes conversiones:

* Documento de Microsoft Word (DOC, DOCX, RTF, TXT)
* Documento de Microsoft Excel (XLS, XLSX)
* Documento de Microsoft PowerPoint (PPT, PPTX)
* Documento de proyecto de Microsoft (MPP)
* Documento de Microsoft Visio (VSD)

>[!NOTE]
>
>Al utilizar OpenOffice para convertir formatos anteriores, no se aplica la configuración de Adobe PDF.

## Acerca de la configuración predefinida del PDF {#about-the-predefined-pdf-settings}

PDF Generator proporciona varias configuraciones de PDF predefinidas para su uso. No puede modificar esta configuración predefinida; sin embargo, puede crear una configuración basada en una existente editándola y guardándola con un nuevo nombre.

**Impresión de alta calidad:** Crea archivos de PDF para resultados de alta calidad. Esta configuración:

* disminución de resolución de imágenes en color y escala de grises a 300 ppp
* reduce las muestras de imágenes monocromas a 1200 ppp
* imprime con mayor resolución de imagen
* utiliza otras opciones para conservar la máxima cantidad de información sobre el documento original.

Estos archivos de PDF se pueden abrir en Adobe Acrobat 5 y Adobe Acrobat Reader® 5 o versiones posteriores.

**Páginas de gran tamaño:** Crea documentos de PDF adecuados para la visualización e impresión fiables de planos de ingeniería de más de 200 x 200 pulgadas. Los documentos de PDF creados se pueden abrir en Adobe Acrobat Professional y Acrobat Standard, versión 7 o posterior, y Adobe Reader 7 o posterior.

**PDF/A-1B 2005 CMYK/PDF/A-1B 2005 RGB:** Comprueba la conformidad de los trabajos entrantes con la norma ISO para la conservación a largo plazo (archivo) de documentos electrónicos y crea archivos PDF/A solo si cumplen con la normativa. Estos archivos se utilizan principalmente para el archivado. Los archivos compatibles solo pueden contener texto, imágenes rasterizadas y objetos vectoriales; no pueden contener codificación ni secuencias de comandos. Además, todas las fuentes deben estar incrustadas para que los documentos puedan abrirse y verse como creados. PDF/A-1b utiliza el PDF 1.4 y convierte todos los colores a CMYK o RGB, dependiendo del estándar que elija. Los archivos de PDF creados con este archivo de configuración se pueden abrir en Acrobat 5 y Acrobat Reader 5 y versiones posteriores. Para obtener más información sobre PDF/A, consulte Adobe y estándares del sector.

**PDF/X-1a 2001:** Comprueba la compatibilidad de los trabajos entrantes con PDF/X-1a y crea archivos de PDF solo si son compatibles. PDF/X-1a es un estándar ISO para el intercambio de contenido gráfico. PDF/X-1a requiere que todas las fuentes estén incrustadas, que se especifiquen los cuadros de PDF adecuados y que el color aparezca como CMYK o manchas de color. Los archivos de PDF que cumplen los requisitos de PDF/X-1a se dirigen a una condición de salida específica, como la impresión en offset de la web de acuerdo con las Especificaciones Publicaciones en offset de la web. Para obtener más información sobre PDF/X, consulte Adobe y estándares del sector.

**PDF/X-3 2002:** Comprueba la compatibilidad de los trabajos entrantes con PDF/X-3 y crea archivos de PDF solo si cumplen los requisitos. Al igual que PDF/X-1a, PDF/X-3 es un estándar ISO para el intercambio de contenido gráfico. La principal diferencia es que el PDF/X-3 admite colores independientes del dispositivo.

**Calidad de prensa:** Crea archivos de PDF para la producción de impresión de alta calidad (por ejemplo, en una filmadora o una filmadora). En este caso, el tamaño del archivo no es una consideración. El objetivo es mantener toda la información en un archivo de PDF que un impresor comercial o proveedor de servicios de preimpresión necesita para imprimir el documento correctamente. Este conjunto de opciones:

* disminución de resolución de imágenes en color y escala de grises a 300 ppp
* reduce las muestras de imágenes monocromas a 1200 ppp
* incrusta los subconjuntos de todas las fuentes utilizadas en el documento
* imprime con mayor resolución de imagen,
* no gira automáticamente las páginas según la orientación del texto o los comentarios de las convenciones de estructuración de documentos (DSC)
* utiliza otras opciones para conservar la máxima cantidad de información sobre el documento original.

Los trabajos de impresión fallan si tienen fuentes que no se pueden incrustar. Estos archivos de PDF se pueden abrir en Acrobat 5 y Acrobat Reader 5 y versiones posteriores.

>[!NOTE]
>
>Antes de crear un archivo de PDF para enviarlo a una imprenta comercial o a un proveedor de servicios de preimpresión, determine la resolución de salida y otras opciones de configuración, o solicite un archivo .joboptions con la configuración recomendada. Es posible que tenga que personalizar la configuración de Adobe PDF para un proveedor en particular y luego proporcionar un archivo .joboptions propio.

**Tamaño de archivo más pequeño:** Crea archivos de PDF para mostrarlos en la web o en una intranet, o para distribuirlos a través de un sistema de correo electrónico y visualizarlos en pantalla. Este conjunto de opciones utiliza compresión, disminución de resolución y una resolución de imagen relativamente baja. Convierte todos los colores a sRGB y no incrusta las fuentes a menos que sea necesario. También optimiza los archivos para el servicio de bytes. Estos archivos de PDF se pueden abrir en Acrobat 5 y Acrobat Reader 5.0 y versiones posteriores.

**Estándar:** Crea archivos de PDF para imprimirlos en impresoras de escritorio o fotocopiadoras digitales, publicarlos en un CD o enviarlos a un cliente como prueba de publicación. Este conjunto de opciones utiliza la compresión y la disminución de resolución para reducir el tamaño del archivo. También incrusta subconjuntos de todas las fuentes utilizadas en el archivo, convierte todos los colores en sRGB e imprime a una resolución media para crear una representación razonablemente precisa del documento original. Observe que los subconjuntos de fuentes de Microsoft Windows no están incrustados de forma predeterminada. Estos archivos de PDF se pueden abrir en Acrobat 5 y Acrobat Reader 5.0 y versiones posteriores.

## Agregar o editar la configuración del PDF {#add-or-edit-pdf-settings}

La configuración del PDF determina con precisión cómo se convierten los archivos y la estructura y características del PDF resultantes. Defina una nueva configuración de PDF o edite una que haya creado anteriormente. No puede modificar la configuración predefinida, pero puede crear una configuración basada en una existente editándola y guardándola con un nuevo nombre.

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Configuración de Adobe PDF.
1. Haga clic en Nuevo o haga clic en el nombre de una configuración existente.
1. En la página Nueva/Editar configuración de Adobe PDF, complete la información necesaria en estas secciones:

[Opciones generales](configuring-pdf-settings.md#general-options)

[Opciones de imágenes](configuring-pdf-settings.md#images-options)

[Opciones de fuentes](configuring-pdf-settings.md#fonts-options)

[Opciones de color](configuring-pdf-settings.md#color-options)

[Opciones avanzadas](configuring-pdf-settings.md#advanced-options)

[Información sobre normas y opciones de conformidad](configuring-pdf-settings.md#standards-reporting-and-compliance-options)

[Opciones de vista inicial](configuring-pdf-settings.md#initial-view-options)

   Para ir a otra sección, haga clic en su vínculo en la página web o utilice los botones Next y Previous.

1. Una vez completada la información en todas las secciones, haga clic en Guardar o Guardar como y proporcione un nombre para la configuración.

## Cargar configuración del PDF {#upload-pdf-settings}

Puede disponer de la configuración de PDF en el servidor de PDF Generator cargándola desde un equipo local o una ubicación de red.

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Configuración de Adobe PDF y, a continuación, haga clic en Cargar.
1. En la página Cargar configuración de Adobe PDF, haga clic en Examinar, busque el archivo de configuración del PDF y haga clic en Abrir.
1. Haga clic en Aceptar y vuelva a hacer clic en Aceptar.

## Eliminar configuración del PDF {#delete-pdf-settings}

Puede eliminar de forma permanente la configuración del PDF si ya no es necesaria.

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Configuración de Adobe PDF.
1. Seleccione la casilla de verificación situada junto a la configuración que desea eliminar. Puede seleccionar varias configuraciones.
1. Haga clic en Eliminar y, en la página Confirmación de eliminación, vuelva a hacer clic en Eliminar.

## Opciones generales {#general-options}

Utilice las opciones generales para especificar la versión de Acrobat que se utilizará para la compatibilidad de archivos y otras opciones de archivos y dispositivos. Para obtener instrucciones sobre el acceso a las opciones generales, consulte [Agregar o editar la configuración del PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

### Opciones de archivo {#file-options}

**Compatibilidad:** Nivel de compatibilidad del archivo de PDF. Para los documentos que se distribuirán ampliamente, considere la posibilidad de seleccionar Acrobat 4 (PDF 1.3) o Acrobat 5 (PDF 1.4) para garantizar que todos los usuarios puedan ver e imprimir el documento. Si crea archivos mediante la compatibilidad con Acrobat 5 o versiones posteriores, es posible que no sean compatibles con versiones anteriores de Acrobat. Las siguientes subsecciones muestran algunas de las diferencias entre los archivos de PDF que se crean con diferentes niveles de compatibilidad con Acrobat.

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
   <td><p>Se puede abrir con Acrobat 3.0 y Acrobat Reader 3.0 y posteriores. Las funciones específicas de versiones posteriores se pueden perder o no verse.</p> </td>
   <td><p>La mayoría se pueden abrir con Acrobat 4 y Acrobat Reader 4.0 y versiones posteriores. Las funciones específicas de versiones posteriores se pueden perder o no verse.</p> </td>
   <td><p>La mayoría se pueden abrir con Acrobat 4 y Acrobat Reader 4.0 y versiones posteriores. Las funciones específicas de versiones posteriores se pueden perder o no verse.</p> </td>
  </tr>
  <tr>
   <td><p>No puede contener ilustraciones que utilicen efectos de transparencia activos. Cualquier transparencia debe aplanarse antes de convertirla en PDF 1.3.</p> </td>
   <td><p>Apoya el uso de la transparencia en vivo en las ilustraciones. (La función de Acrobat Distiller aplana la transparencia.)</p> </td>
   <td><p>Apoya el uso de la transparencia en vivo en las ilustraciones. (La función de Acrobat Distiller aplana la transparencia.)</p> </td>
   <td><p>Apoya el uso de la transparencia en vivo en las ilustraciones. (La función de Acrobat Distiller aplana la transparencia.)</p> </td>
  </tr>
  <tr>
   <td><p>No se admiten capas.</p> </td>
   <td><p>No se admiten capas.</p> </td>
   <td><p>Conserva las capas al crear archivos de PDF a partir de aplicaciones que admiten la generación de documentos de PDF por capas, como Adobe Illustrator® CS o Adobe InDesign® CS y posteriores.</p> </td>
   <td><p>Conserva las capas al crear archivos de PDF a partir de aplicaciones que admiten la generación de documentos de PDF por capas, como Illustrator CS o InDesign CS y posterior.</p> </td>
  </tr>
  <tr>
   <td><p>Se admite el espacio de color DeviceN con 8 colorantes.</p> </td>
   <td><p>Se admite el espacio de color DeviceN con 8 colorantes.</p> </td>
   <td><p>Se admite el espacio de color DeviceN con hasta 31 colorantes.</p> </td>
   <td><p>Se admite el espacio de color DeviceN con hasta 31 colorantes.</p> </td>
  </tr>
  <tr>
   <td><p>Las fuentes multibyte se pueden incrustar. (Distiller convierte las fuentes al incrustarlas).</p> </td>
   <td><p>Las fuentes multibyte se pueden incrustar.</p> </td>
   <td><p>Las fuentes multibyte se pueden incrustar.</p> </td>
   <td><p>Las fuentes multibyte se pueden incrustar.</p> </td>
  </tr>
  <tr>
   <td><p>Se admite la seguridad RC4 de 40 bits.</p> </td>
   <td><p>Se admite la seguridad RC4 de 128 bits.</p> </td>
   <td><p>Se admite la seguridad RC4 de 128 bits.</p> </td>
   <td><p>Compatible con la seguridad RC4 de 128 bits y AES (Advanced Encryption Standard) de 128 bits.</p> </td>
  </tr>
 </tbody>
</table>

**Compresión de nivel de objeto:** Consolida objetos pequeños (cada uno de los cuales no se puede comprimir por sí mismo) en flujos que luego se pueden comprimir de manera eficiente.

**Desactivado:** No comprime ninguna información estructural en el documento de PDF. Seleccione esta opción si desea que los usuarios vean, naveguen e interactúen con marcadores y otra información estructural mediante Acrobat 5 y posterior.

**Solo etiquetas:** Comprime la información estructural en el documento del PDF. El uso de esta opción da como resultado un archivo de PDF que se puede abrir e imprimir mediante Acrobat 5. Los usuarios no pueden ver información de accesibilidad, estructura o PDF etiquetado en Acrobat 5 o Acrobat Reader 5.0, pero pueden ver esta información en Acrobat 6 y Adobe Reader 6.0.

**Rotar páginas automáticamente:** Establece el giro automático de las páginas en función de la orientación del texto o de los comentarios DSC. Por ejemplo, algunas páginas (como las que contienen tablas) pueden requerir que el usuario las gire de lado para leerlas. Seleccione Individualmente para rotar cada página según la dirección del texto de esa página. Seleccione Colectivamente por archivo para rotar todas las páginas del documento en función de la orientación de la mayor parte del texto.

>[!NOTE]
>
>Si se selecciona Procesar comentarios DSC en la configuración Avanzada y se incluyen los comentarios %%Orientación de visualización, estos comentarios tienen prioridad a la hora de determinar la orientación de la página.

**Enlace:** Especifica si se muestra un archivo de PDF con enlaces del lado izquierdo o derecho. Esta configuración afecta a la visualización de páginas en el diseño Página de enfrente: Continua y a la visualización de miniaturas en paralelo.

**Resolución:** Establece la emulación para la resolución de una impresora para archivos de entrada que ajustan su comportamiento según la resolución de la impresora en la que se va a imprimir. Para la mayoría de los archivos de entrada, una configuración de mayor resolución resulta en archivos de PDF más grandes pero de mayor calidad, y una configuración más baja resulta en archivos de PDF más pequeños pero de menor calidad. Normalmente, la resolución determina el número de pasos de un degradado o mezcla. Puede introducir un valor de 72 a 4000. Mantenga esta configuración como predeterminada a menos que tenga pensado imprimir el archivo del PDF en una impresora específica y desee emular la resolución definida en el archivo de entrada original.

>[!NOTE]
>
>Al aumentar la configuración de resolución, aumenta el tamaño del archivo y puede aumentar ligeramente el tiempo necesario para procesar algunos archivos.

**Todas las páginas o páginas de:** Especifica qué páginas convertir. Deje el cuadro Para vacío para crear un intervalo desde el número de página especificado en el cuadro Desde hasta el final del archivo.

**Optimizar Para Vista Web Rápida:** Reestructura el archivo para la descarga página a página (servidor de bytes) desde servidores web. Esta opción comprime el texto y el arte lineal, independientemente de lo que haya seleccionado como configuración de compresión en la ficha Imágenes. La compresión resulta en un acceso y una visualización más rápidos al descargar el archivo desde la web o una red. Esta opción no está habilitada de forma predeterminada.

### Tamaño de página predeterminado {#default-page-size}

Las opciones de Tamaño de página predeterminado especifican el tamaño de página que se utilizará cuando no se especifique uno en el archivo original. Normalmente, los archivos Adobe PostScript incluyen esta información, excepto los archivos PostScript encapsulado (EPS), que dan un tamaño de cuadro delimitador pero no un tamaño de página. El tamaño máximo de página permitido es de 31 800 000 cm (15 000 000 pulgadas) en cualquier dirección. Estas opciones configuran el tamaño de página predeterminado:

**Anchura:** Anchura de la página

**Altura:** Altura de la página

**Unidades:** Unidades que se utilizarán en la configuración de anchura y altura

## Opciones de imágenes {#images-options}

Las opciones de imágenes especifican la compresión y el remuestreo de las imágenes. Puede experimentar con estas opciones para encontrar un equilibrio adecuado entre el tamaño del archivo y la calidad de la imagen. Para obtener instrucciones sobre cómo acceder a la configuración de imágenes, consulte [Agregar o editar la configuración del PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Estas opciones configuran el color, la escala de grises y las imágenes monocromas:

**Disminuir resolución:** Establezca un valor para cada tipo de imagen. Para reducir la resolución de imágenes en color, escala de grises o monocromas, PDF Generator combina píxeles en un área de muestra para aumentar el tamaño de un píxel. Proporcione la resolución del dispositivo de salida en puntos por pulgada (ppp) e introduzca una resolución en ppp en el cuadro Para imágenes anterior. En el caso de las imágenes con una resolución superior a este umbral, PDF Generator combina píxeles, según sea necesario, para reducir la resolución de la imagen (píxeles por pulgada) al valor de ppp especificado. Para desactivar la disminución de resolución, seleccione Desactivado. Estas son las opciones:

**Promedio de disminución de resolución a:** Obtiene el promedio de los píxeles de un área de muestra y reemplaza toda el área por el color de píxel promedio con la resolución especificada.

**Disminución de resolución bicúbica a:** Utiliza un promedio ponderado para determinar el color de los píxeles y, por lo general, ofrece mejores resultados que el método de promedio simple de disminución de resolución. Bicúbico es el método más lento pero más preciso y da lugar a las gradaciones tonales más suaves.

**Submuestreo a:** Selecciona un píxel en el centro del área de muestra y reemplaza todo el área por ese píxel con la resolución especificada. El submuestreo reduce significativamente el tiempo de conversión en comparación con la disminución de resolución, pero da como resultado imágenes menos fluidas y continuas.

La configuración de resolución para el color y la escala de grises debe ser de 1,5 a 2 veces la pantalla de líneas que indica que el archivo se imprimirá en. (Siempre que no descienda por debajo de esta configuración de resolución recomendada, las imágenes que no contengan líneas rectas o patrones geométricos o repetitivos no se verán afectadas por una resolución más baja.) La resolución de las imágenes monocromas debe ser la misma que la del dispositivo de salida. Sin embargo, tenga en cuenta que si guarda una imagen monocroma con una resolución superior a 1500 ppp, el tamaño del archivo aumenta sin que la calidad de la imagen mejore de forma notable.

Considere también si los usuarios necesitan ampliar una página. Por ejemplo, si está creando un documento PDF de un mapa, considere la posibilidad de utilizar una resolución de imagen más alta para que los usuarios puedan ampliar el mapa.

>[!NOTE]
>
>El remuestreo de imágenes monocromas puede dar lugar a resultados de visualización inesperados, como la ausencia de visualización de imágenes. Si se produce este problema, desactive el remuestreo y vuelva a convertir el archivo. Es muy probable que este problema se produzca con el submuestreo y es menos probable que se produzca con la disminución de resolución bicúbica.

En esta tabla se muestran los tipos de impresoras y su resolución medida en ppp, su resolución de pantalla predeterminada medida en líneas por pulgada (lpp) y una resolución de remuestreo para imágenes que se miden en píxeles por pulgada (ppi). Por ejemplo, para imprimir en una impresora láser de 600 ppp, escriba 170 para que la resolución remuestre las imágenes en.

<table>
 <tbody>
  <tr>
   <th><p>Resolución de impresora</p> </th>
   <th><p>Pantalla de línea predeterminada</p> </th>
   <th><p>Resolución de imagen</p> </th>
  </tr>
  <tr>
   <td><p>300 ppp (impresora láser)</p> </td>
   <td><p>60 lpp</p> </td>
   <td><p>120 ppp</p> </td>
  </tr>
  <tr>
   <td><p>600 ppp (impresora láser)</p> </td>
   <td><p>85 lpp</p> </td>
   <td><p>170 ppp</p> </td>
  </tr>
  <tr>
   <td><p>1200 ppp (filmadora)</p> </td>
   <td><p>120 lpp</p> </td>
   <td><p>240 ppp</p> </td>
  </tr>
  <tr>
   <td><p>2.400 ppp (filmadora)</p> </td>
   <td><p>150 lpp</p> </td>
   <td><p>300 ppp</p> </td>
  </tr>
 </tbody>
</table>

**Compresión:** Establezca un valor para aplicarlo al color, la escala de grises y las imágenes monocromas. Para imágenes en color y escala de grises, establezca también la calidad de la imagen:

* En el caso de las imágenes en color o en escala de grises, seleccione ZIP para aplicar una compresión que funcione bien en imágenes con grandes áreas de colores únicos o patrones repetidos. Algunos ejemplos son capturas de pantalla, imágenes sencillas creadas con programas de pintura e imágenes monocromas que contienen patrones repetidos. Seleccione JPEG, de calidad mínima a máxima, para aplicar una compresión adecuada para imágenes en escala de grises o en color, como fotografías de tonos continuos que contienen más detalles de los que se pueden reproducir en la pantalla o en la impresión. Seleccione JPEG para determinar automáticamente la mejor calidad para las imágenes en color y en escala de grises.
* Para imágenes monocromas, seleccione la compresión CCITT Group 4, CCITT Group 3, ZIP, JPEG 200, Automatic (JPEG 2000) o Run Length.

Asegúrese de que las imágenes monocromas se digitalicen como monocromas y no como en escala de grises. El texto digitalizado a veces se guarda como imágenes en escala de grises de forma predeterminada. El texto en escala de grises comprimido con el método de compresión JPEG no es claro y puede ser ilegible.

**Calidad de imagen:** Configura la calidad de imagen para imágenes en color y escala de grises. Las opciones son mínima, baja, media, alta y máxima.

**Suavizar a gris:** Suaviza los bordes irregulares en imágenes monocromas. Seleccione 2, 4 u 8 bits para especificar 4, 16 o 256 niveles de gris. (El suavizado puede desenfocar las líneas pequeñas o delgadas.)

>[!NOTE]
>
>La compresión de texto y arte lineal siempre está activada.

**Política de imagen:** Establezca una directiva para las imágenes en color, en escala de grises y monocromas. Si la resolución de la imagen está por debajo de la resolución especificada, puede seleccionar continuar (Ignorar), enviar un mensaje de advertencia o cancelar el trabajo.

## Opciones de fuentes {#fonts-options}

Las opciones de Fuentes especifican qué fuentes se incrustarán en un archivo de PDF y si se incrustará un subconjunto de caracteres que se utilizan en el archivo de PDF. Para obtener instrucciones sobre cómo acceder a las opciones de Fuentes, consulte [Agregar o editar la configuración del PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

>[!NOTE]
>
>Cuando se combinan archivos de PDF con el mismo subconjunto de fuentes, PDF Generator intenta combinar los subconjuntos de fuentes.

**Insertar todas las fuentes:** Incrusta todas las fuentes utilizadas en el archivo. Se requiere la incrustación de fuentes para la compatibilidad con PDF/X.

**Subconjunto De Fuentes Incrustadas Cuando El Porcentaje De Caracteres Utilizados Es Inferior A:** Si selecciona esta opción, especifique un porcentaje de umbral para incrustar solo un subconjunto de las fuentes. Por ejemplo, si el umbral es 35 y se utiliza menos del 35 % de los caracteres, PDF Generator incrusta solo esos caracteres. Solo se incrustan las fuentes con los bits de permiso adecuados.

**Cuando La Incrustación Falla:** Especifica cómo responde PDF Generator si no encuentra una fuente que incrustar al procesar un archivo. Puede hacer que PDF Generator ignore la solicitud y sustituya la fuente, le advierta y sustituya la fuente o cancele el procesamiento del trabajo actual.

**Fuente de fuente:** Ubicación de las fuentes que utiliza PDF Generator.

### Especificar las fuentes que se van a incrustar {#specify-which-fonts-to-embed}

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Configuración de Adobe PDF.
1. Haga clic en Nuevo o haga clic en el nombre de una configuración.
1. Haga clic en Fuentes y desmarque Incrustar todas las fuentes.
1. En la lista Fuente, seleccione una fuente y haga clic en Ir para actualizar la lista de fuentes en el cuadro de la izquierda.
1. Haga clic en una fuente en el cuadro de la izquierda. A continuación, haga clic en Agregar junto al cuadro correspondiente para moverlo a la lista Incrustar siempre o Nunca. Repita el proceso para cada fuente. Utilice Ctrl mientras hace clic para seleccionar varias fuentes que desee mover.
1. Para quitar una fuente de la lista Incrustar siempre o No incrustar nunca, selecciónela y haga clic en Quitar junto al cuadro correspondiente. Esta acción no elimina la fuente del sistema; simplemente elimina la referencia a ella en la lista.
1. Si la fuente que desea especificar no aparece, escriba su nombre en el cuadro Agregar fuente y, a continuación, haga clic en Incrustar siempre o No incrustar nunca. Los nombres de fuente no pueden contener caracteres alfanuméricos.

>[!NOTE]
>
>Una fuente TrueType puede contener un valor agregado por el diseñador de fuentes que impida que la fuente se incruste en los archivos de PDF.

>[!NOTE]
>
>Las fuentes se seleccionan de la caché de fuentes del sistema de Windows y es necesario reiniciar el sistema para actualizar la caché. AEM Después de especificar el directorio de fuentes del cliente, asegúrese de reiniciar el sistema en el que está instalado el formulario de la aplicación de la versión de la aplicación de datos de la aplicación de la aplicación de datos de usuario.

## Opciones de color {#color-options}

Las opciones de color definen toda la información de gestión de color para PDF Generator. Para obtener instrucciones sobre cómo acceder a las opciones de Color, consulte [Agregar o editar la configuración del PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

### Configuración de Adobe Color {#adobe-color-settings}

**Archivo de configuración:** Esta lista contiene una lista de configuraciones de color que también se utilizan en las principales aplicaciones gráficas, como Adobe Photoshop y Adobe Illustrator. La configuración de color que seleccione determina las demás configuraciones de color del Adobe en esta página. Por ejemplo, si selecciona una configuración que no sea Ninguno, todas las opciones que no sean las de Datos dependientes del dispositivo estarán predefinidas y atenuadas. Sólo puede editar la configuración de las directivas de gestión de color y los espacios de trabajo si selecciona Ninguno en Archivo de configuración.

### Políticas de gestión de color {#color-management-policies}

Si ha seleccionado Ninguno en el archivo de configuración, el área Directivas de gestión de color especifica cómo PDF Generator convierte el color no administrado en un archivo PostScript.

**Dejar el color sin cambiar:** Deja sin cambios los colores dependientes del dispositivo y conserva los colores independientes del dispositivo como el equivalente más cercano posible en PDF. Esta opción es útil para imprimir tiendas que han calibrado todos sus dispositivos, utilizado esa información para especificar el color del archivo y enviado sólo a esos dispositivos.

**Etiquetar todo para la gestión de color:** Incrusta un perfil de International Color Consortium al destilar archivos y calibra el color de las imágenes, lo que hace que los colores de los archivos de PDF resultantes sean independientes del dispositivo si ha seleccionado la compatibilidad con Acrobat 4 (PDF 1.3) o versiones posteriores. Sin embargo, los espacios de color dependientes del dispositivo en los archivos (RGB, Escala de grises y CMYK) se convierten en espacios de color independientes del dispositivo (CalRGB, CalGray y LAB).

**Etiquetar solo imágenes para la gestión de color:** Incrusta perfiles ICC únicamente en imágenes, no en texto ni en gráficos, al destilar archivos si ha seleccionado la compatibilidad con Acrobat 4 (PDF 1.3). Esta opción evita que el texto negro sufra ningún cambio de color. Sin embargo, los espacios de color dependientes del dispositivo en las imágenes (RGB, Escala de grises y CMYK) se convierten en espacios de color independientes del dispositivo (CalRGB, CalGray y LAB). El texto y los gráficos no se convierten.

**Convertir todos los colores a sRGB o Convertir todos los colores a CMYK:** Calibra el color del archivo, haciendo que el dispositivo de color sea independiente, de forma similar a Etiquetar todo para la administración de color. Si ha seleccionado la compatibilidad con Acrobat 4 (PDF 1.3) o versiones posteriores y la convierte a sRGB, las imágenes CMYK y RGB se convierten a sRGB.

Independientemente de la opción de compatibilidad que seleccione, las imágenes en escala de grises no se modifican. Esto generalmente reduce el tamaño y aumenta la velocidad de visualización de los archivos de PDF porque se necesita menos información para describir imágenes de RGB que para describir imágenes CMYK. Dado que RGB es el espacio de color nativo que se utiliza en los monitores, no es necesaria ninguna conversión de color durante la visualización, lo que contribuye a una visualización en línea más rápida. Esta opción se recomienda si el archivo de PDF se utiliza en línea o con impresoras de baja resolución.

**Interpretación de documentos:** Método para asignar colores entre espacios de color. El resultado de cualquier método en particular depende de los perfiles de los espacios de color. Por ejemplo, algunos perfiles producen resultados idénticos con métodos diferentes. Estas opciones están disponibles:

>[!NOTE]
>
>En todos los casos, las operaciones de gestión de colores que se producen después de crear el archivo PDF pueden ignorar o anular las intenciones.

**Conservar:** Significa que la intención se especifica en el dispositivo de salida en lugar de en el archivo del PDF. En muchos dispositivos de salida, la calidad predeterminada es Colorimétrica relativa.

**Perceptual:** Mantiene los valores de color relativo entre los píxeles originales a medida que se asignan a la gama de destino. Este método conserva la relación visual entre los colores, aunque los valores de color en sí mismos pueden cambiar.

**Saturación:** Mantiene los valores de saturación relativa de los píxeles originales. Este método es adecuado para gráficos empresariales, donde la relación exacta entre colores no es tan importante como tener colores saturados brillantes.

**Colorimétrico relativo:** Reasigna el punto blanco del espacio de origen al punto blanco del espacio de destino.

**Colorimétrico absoluto:** Deshabilita la coincidencia de puntos blancos y negros al convertir colores. Este método no se recomienda a menos que deba conservar los colores de la firma, como los utilizados en marcas comerciales o logotipos.

### Espacios de trabajo {#working-spaces}

Para todos los valores de la lista en Políticas de gestión de color, excepto Dejar el color sin cambiar, seleccione en las listas del área de Espacio de trabajo para especificar qué perfiles ICC se utilizan para definir y calibrar los espacios de color de escala de grises, RGB y CMYK en los archivos de PDF destilados. Estas opciones están disponibles:

**Gris:** Define el espacio de color de todas las imágenes en escala de grises de los archivos. Esta opción sólo está disponible si ha elegido Etiquetar todo para la administración de color o Etiquetar sólo imágenes para la administración de color. El perfil ICC predeterminado para imágenes grises es Gray Gamma 2.2. También puede seleccionar Ninguno para evitar que las imágenes en escala de grises se conviertan.

**RGB:** Define el espacio de color de todas las imágenes de RGB de los archivos. El predeterminado, sRGB IEC61966-2.1, es generalmente una buena opción porque se está convirtiendo en un estándar en la industria y muchos dispositivos de salida lo reconocen. También puede seleccionar Ninguno para evitar que las imágenes del RGB se conviertan.

**CMYK:** Define el espacio de color de todas las imágenes CMYK de los archivos. El valor predeterminado es U.S. Web Coated (SWOP) v2. También puede seleccionar Ninguno para evitar que las imágenes CMYK se conviertan.

>[!NOTE]
>
>La selección de Ninguno para los tres espacios de trabajo tiene el mismo efecto que la selección de Dejar el color sin cambiar.

**Conservar valores CMYK para espacios de color CMYK calibrados:** Si se selecciona, los valores CMYK independientes del dispositivo se tratan como valores dependientes del dispositivo (DeviceCMYK), se descartan los espacios de color independientes del dispositivo y los archivos PDF/X-1a utilizan el valor Convertir todos los colores a CMYK. Si no se selecciona, los espacios de color independientes del dispositivo se convierten a CMYK si la directiva de administración de color está establecida en Convertir todos los colores a CMYK.

### Datos dependientes del dispositivo {#device-dependent-data}

Estas opciones se aplican si trabaja con documentos creados con documentación de gama alta y aplicaciones gráficas, como Adobe Illustrator y Adobe InDesign. Para obtener más información, consulte la documentación suministrada con la aplicación.

Las funciones de transferencia se utilizan para efectos artísticos y para ajustar las especificaciones de un dispositivo de salida específico. Por ejemplo, un archivo destinado a la salida en una filmadora determinada puede contener funciones de transferencia que compensen la ganancia de puntos inherente a esa impresora.

**Conservar Bajo Eliminación De Color Y Generación De Negro:** Conserva esta configuración si existe en el archivo PostScript. La generación de negro calcula la cantidad de negro que se va a utilizar cuando se intenta reproducir un color concreto. La eliminación de subcolor (UCR) reduce la cantidad de componentes cian, magenta y amarillo para compensar la cantidad de negro que agregó la generación de negro. Debido a que utiliza menos tinta, UCR se utiliza generalmente para papel prensa y material sin revestimiento.

**Cuando Se Encuentran Funciones De Transferencia:** Determina qué hacer cuando se encuentran funciones de transferencia:

**Conservar:** Conserva las funciones de transferencia que se utilizan tradicionalmente para compensar la ganancia o pérdida de puntos que puede producirse cuando una imagen se transfiere a una película. La ganancia de puntos se produce cuando los puntos de tinta que componen una imagen impresa son más grandes (por ejemplo, debido a la propagación en papel) que en la pantalla de semitonos; la pérdida de puntos se produce cuando los puntos se imprimen más pequeños. Con esta opción, las funciones de transferencia se mantienen como parte del archivo y se aplican al archivo cuando se genera la salida del archivo.

**Aplicar:** No mantiene la función de transferencia, pero la aplica al archivo, que cambia los colores del archivo. Esta opción es útil para crear efectos de color en un archivo. De forma predeterminada, esta opción está seleccionada para las nuevas configuraciones.

**Eliminar:** Elimina las funciones de transferencia aplicadas. Elimine las funciones de transferencia aplicadas a menos que el archivo de PDF se envíe al mismo dispositivo para el que se creó el archivo PostScript de origen.

**Conservar información de semitonos:** Conserva la información de semitonos de los archivos. La información de semitonos consiste en puntos que controlan la cantidad de tinta que depositan los dispositivos de semitonos en una ubicación específica del papel. Al variar el tamaño y la densidad del punto, se crea la ilusión de variaciones de gris o de color continuo. Para una imagen CMYK, se utilizan cuatro tramas de semitonos, una para cada tinta que se utiliza en el proceso de impresión.

En la producción de impresión tradicional, se produce un semitono colocando una pantalla de semitono entre una película y la imagen, y luego exponiendo la película. Los equivalentes electrónicos, como en Adobe Photoshop, permiten a los usuarios especificar los atributos de la pantalla de semitonos antes de producir la salida de película o papel. La información de semitonos está destinada a utilizarse con un dispositivo de salida concreto.

## Opciones avanzadas {#advanced-options}

Las opciones avanzadas especifican qué comentarios de las convenciones de estructuración de documentos (DSC) se guardarán en el archivo de PDF y cómo se establecerán otras opciones que afectan a la conversión desde PostScript. En un archivo PostScript, los comentarios de DSC contienen información sobre el archivo (como la aplicación de origen, la fecha de creación y la orientación de la página). También proporcionan una estructura para las descripciones de páginas en el archivo (como las instrucciones de inicio y finalización de una sección de prólogo). Los comentarios de DSC pueden ser útiles cuando el documento se va a imprimir o imprimir. Para obtener instrucciones sobre el acceso a las opciones avanzadas, consulte [Agregar o editar la configuración del PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Al trabajar con las opciones Avanzadas, resulta útil conocer el lenguaje PostScript y cómo se traduce al PDF. (Consulte [ADOBE POSTSCRIPT 3](https://www.adobe.com/products/postscript/main.html).)

**Permitir que el archivo PostScript anule la configuración de Adobe PDF:** Utiliza la configuración almacenada en un archivo PostScript en lugar del archivo de configuración actual de Adobe PDF. Antes de procesar un archivo PostScript, puede colocar parámetros en el archivo para controlar los siguientes aspectos:

* compresión de texto y gráficos
* disminución de resolución y codificación de imágenes muestreadas
* incrustación de fuentes Type 1 e instancias de fuentes Type 1 Multiple Master

**Permitir XObjects de PostScript:** Los objetos XObject de PostScript almacenan información que aparece en muchas páginas del mismo archivo, como una imagen de fondo o información del encabezado y pie de página. El uso de objetos XObject de PostScript puede acelerar la impresión, pero requiere más memoria de impresora. Para evitar que se creen objetos XObject de PostScript, anule la selección de esta opción si crea archivos de PDF con compatibilidad con Acrobat 5 (PDF 1.4) o posterior.

**Convertir degradados en tonos suaves:** Convierte mezclas en tonos suaves para Acrobat 4 y posterior, lo que hace que los archivos PDF sean más pequeños y pueda mejorar la calidad de la salida final. PDF Generator convierte los degradados de Adobe Illustrator, Adobe InDesign, Adobe FreeHand MX, CorelDraw, Quark Xpress y Microsoft PowerPoint.

**Convertir líneas suaves en curvas:** Reduce la cantidad de puntos de control utilizados para crear curvas en los planos CAD, lo que da como resultado PDF más pequeños y una representación en pantalla más rápida.

**Conservar semántica de copia de nivel 2:** Utiliza el operador copypage definido en el PostScript de nivel de lenguaje 2 en lugar de en el PostScript de nivel de lenguaje 3. Si tiene un archivo PostScript y selecciona esta opción, un operador de copypage copia la página. Si no se selecciona esta opción, se ejecuta el equivalente de una operación showpage, pero no se reinicia el estado gráfico.

**Conservar configuración de sobreimpresión:** Conserva la configuración de sobreimpresión de los archivos que se van a convertir en PDF. Los colores sobreimpresos son dos o más tintas impresas una encima de la otra. Por ejemplo, cuando se imprime una tinta cian sobre una tinta amarilla, la sobreimpresión resultante es de color verde. Sin sobreimpresión, el amarillo subyacente no se imprimiría, lo que daría como resultado un color cian.

**El Valor Predeterminado De Sobreimpresión Es Sobreimpresión Distinta De Cero:** Evita que los objetos sobreimpresos con valores CMYK cero eliminen los objetos CMYK que se encuentran debajo de ellos. Este efecto se consigue insertando el parámetro de estado gráfico OPM 1 en el fichero PDF siempre que el operador Setoverprint esté presente.

**Guardar la configuración de Adobe PDF en el archivo de PDF:** Incrusta el archivo de configuración que se utiliza para crear el archivo de PDF. Puede abrir y ver el archivo de configuración (que tiene la extensión de nombre de archivo .joboptions) en el cuadro de diálogo Archivos adjuntos de Acrobat. El archivo de configuración de Adobe PDF se convierte en un elemento del árbol EmbeddedFiles dentro del archivo de PDF.

**Guardar Imágenes Del JPEG Original En El PDF Si Es Posible:** Procesa cualquier imagen comprimida del JPEG (imágenes que ya están comprimidas con codificación DCT) sin volver a comprimirlas. Si se selecciona esta opción, PDF Generator descomprime las imágenes del JPEG para asegurarse de que no estén dañadas. Sin embargo, no recomprime imágenes válidas, por lo que procesa la imagen original intacta. Con esta opción seleccionada, el rendimiento mejora porque sólo se produce la descompresión (no la recompresión) y se conservan los datos de imagen y los metadatos.

**Guardar vale de trabajo portátil dentro del archivo del PDF:** Conserva un ticket de trabajo PostScript en un archivo de PDF. El ticket de trabajo contiene información sobre el archivo PostScript, como el tamaño de página, la resolución y la información de reventado, en lugar de información sobre el contenido. Esta información se puede utilizar más adelante en un flujo de trabajo o para imprimir el PDF.

**Utilice Prolog.ps y Epilog.ps:** Envía un archivo de prólogo y epílogo con cada trabajo. Estos archivos tienen muchos propósitos. Por ejemplo, los archivos de prólogo se pueden editar para especificar portadas. Los archivos Epilog se pueden editar para resolver una serie de procedimientos en un archivo PostScript. Puede cargar o descargar los archivos. (Consulte Carga y descarga de archivos de prólogo y epílogo).

**Procesar comentarios de DSC:** Mantiene información de DSC de un archivo PostScript. Estas subopciones están disponibles:

**Registrar advertencias de DSC:** Muestra mensajes de advertencia sobre comentarios problemáticos de DSC durante el procesamiento y los agrega a un archivo de registro.

**Conservar información de EPS de DSC:** Conserva información, como la aplicación de origen y la fecha de creación de un archivo EPS. Si no se selecciona esta opción, el tamaño y el centro de la página se asignan en función de la esquina superior izquierda del objeto superior izquierdo y la esquina inferior derecha del objeto inferior derecho de la página.

**Conservar comentarios de OPI:** Conserva la información necesaria para reemplazar una imagen o comentario de Sólo para ubicación (FPO) por la imagen de alta resolución ubicada en servidores compatibles con las versiones 1.3 y 2.0 de la Interfaz de preimpresión abierta (OPI).

**Conservar información del documento de DSC:** Conserva información como el título, la fecha de creación y la hora. Cuando se abre un archivo de PDF en Acrobat, esta información aparece en el panel Descripción de las propiedades del documento.

**Cambiar el tamaño de la página y centrar ilustraciones para archivos EPS:** Centra una imagen de EPS y cambia el tamaño de la página para ajustarla a la imagen. Esta opción solo se aplica a los trabajos que constan de un solo archivo EPS.

## Información sobre normas y opciones de conformidad {#standards-reporting-and-compliance-options}

PDF Generator puede comprobar el contenido de los documentos en un archivo PostScript para asegurarse de que cumplen los criterios estándar de PDF/X-1a, PDF/X-3 o PDF/A antes de crear el archivo PDF. Para los archivos compatibles con PDF/X, también puede requerir que el archivo PostScript cumpla criterios adicionales seleccionando otras opciones en &quot;Informes y conformidad de normas&quot;. La disponibilidad de las opciones depende del estándar seleccionado.

Los archivos compatibles con PDF/X se utilizan principalmente como formato estandarizado para el intercambio de archivos de PDF destinados a la producción de impresión de alta resolución. A menos que esté creando un documento de PDF para la producción de impresión, puede ignorar los estándares de conformidad de PDF/X.

Los archivos compatibles con el PDF/A se utilizan principalmente para el archivado. Dado que la preservación a largo plazo es el objetivo, el documento debe contener solo lo necesario para abrirlo y verlo durante toda la vida útil prevista del documento. Por ejemplo, los archivos compatibles con PDF/A sólo pueden contener texto, imágenes rasterizadas y objetos vectoriales; no pueden contener cifrado y secuencias de comandos. Además, todas las fuentes deben estar incrustadas para que los documentos puedan abrirse y verse como creados. En otras palabras, los documentos compatibles con PDF/A son *más delgado* que sus homólogos PDF/X, destinados a la producción de gama alta.

>[!NOTE]
>
>Si configura una carpeta inspeccionada para crear archivos compatibles con el estándar PDF/A, asegúrese de no agregar seguridad a la carpeta; el estándar PDF/A no permite el cifrado.

Para obtener instrucciones sobre el acceso a las opciones de informes y conformidad con las normas, consulte [Agregar o editar la configuración del PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

**Estándar de cumplimiento:** Seleccione un estándar para generar un informe que indique si el archivo cumple los requisitos y, si no es así, qué problemas se han producido. Cuando la compatibilidad en la página Configuración general está establecida en Acrobat 4.0, se activan las siguientes opciones. Cuando Compatibilidad se establece en Acrobat 5.0, solo están disponibles las opciones de Acrobat 5.0. Cuando Compatibilidad se establece en una opción alternativa, las siguientes opciones aparecen atenuadas:

* PDF/X-1a (compatible con Acrobat 4.0)
* PDF/X-3 (compatible con Acrobat 4.0)
* PDF/X-1a (compatible con Acrobat 5.0)
* PDF/X-3 (compatible con Acrobat 5.0)
* PDF/A-1b (compatible con Acrobat 5.0)

### Opciones para los estándares PDF/X {#options-for-pdf-x-standards}

**Cuando no es compatible:** Especifica si se crea el archivo PDF si el archivo PostScript no cumple los requisitos de PDF/X. Esta opción está disponible cuando Estándar de conformidad en la página Informes y conformidad estándar está establecida en una opción distinta de Ninguno.

**Continuar:** Crea un archivo de PDF.

**Cancelar trabajo:** Crea un archivo de PDF sólo si el archivo PostScript cumple los requisitos de PDF/X de las opciones de informe seleccionadas y por lo demás es válido. Si se seleccionan ambas opciones de informe PDF/X y el archivo PostScript cumple únicamente un conjunto de criterios PDF/X (por ejemplo, PDF/X-3), PDF Generator crea el archivo compatible.

**Si no se especifica TrimBox ni ArtBox:** Esta opción está disponible cuando Estándar de conformidad en la página Informes y conformidad estándar está establecida en una opción distinta de Ninguno.

**Informar como error:** Marca el archivo PostScript como no compatible si una de las opciones de creación de informes está seleccionada y falta un cuadro de recorte o un cuadro de arte en cualquier página.

**Establezca TrimBox en MediaBox with Offsets:** Calcula los valores en puntos del cuadro de recorte basándose en los desplazamientos del cuadro de medios de las páginas respectivas si no se ha especificado ni el cuadro de recorte ni el cuadro de arte. El cuadro de recorte siempre es tan pequeño o más pequeño que el cuadro de medios envolvente.

**Si BleedBox no se especifica:** Esta opción está disponible cuando Estándar de conformidad en la página Informes y conformidad estándar está establecida en una opción distinta de Ninguno.

**Establezca BleedBox en MediaBox:** Utiliza los valores de los cuadros de medios para el cuadro de sangrado si no se ha especificado este.

**Definir BleedBox en TrimBox con desplazamientos:** Calcula los valores en puntos del cuadro de sangrado en función de los desplazamientos del cuadro de recorte de las páginas respectivas si no se especifica el cuadro de sangrado. El cuadro de purga siempre es tan grande o más grande que el cuadro de recorte adjunto.

**Valores Predeterminados Si No Se Especifican En El Documento:** Esta opción está disponible cuando Estándar de conformidad en la página Informes y conformidad estándar está establecida en una opción distinta de Ninguno.

**Nombre del perfil de calidad de salida:** Indica la condición de impresión caracterizada para la que está preparado el documento. Si un documento no especifica un nombre de OutputIntent, PDF Generator utiliza el valor seleccionado en este menú. Puede seleccionar uno de los nombres proporcionados o escribir un nombre en el espacio proporcionado. Si el flujo de trabajo requiere que el documento especifique la calidad de salida, seleccione Ninguno. Cualquier documento que no cumpla los requisitos no supera la comprobación de cumplimiento.

**Identificador de condición de salida:** Indica el nombre de referencia especificado por el Registro del nombre del perfil de calidad de salida.

**Condición de salida:** Describe la condición de impresión deseada. Esta entrada puede resultar útil para el destinatario deseado del documento del PDF.

**Nombre del Registro (URL):** Indica la dirección Web para obtener más información acerca del Registro. La dirección URL se introduce automáticamente para los nombres de registro ICC.

**Reventado:** Indica el estado del reventado en el documento. La compatibilidad con PDF/X requiere un valor de True o False. Si el documento no especifica el estado reventado, se utiliza el valor proporcionado aquí. Si el flujo de trabajo requiere que el documento especifique el estado de reventado, seleccione Dejar sin definir. Cualquier documento que no cumpla los requisitos no supera la comprobación de cumplimiento.

### Opciones para el estándar PDF/A {#options-for-pdf-a-standard}

Estas opciones se activan cuando Compatibilidad (en el área General) está configurada en Acrobat 4 (PDF 1.3) o Acrobat 5 (PDF 1.4).

**Cuando no es compatible:** Especifica si se crea el archivo PDF si el archivo PostScript no cumple los requisitos de PDF/A.

**Continuar:** Crea un archivo de PDF incluso si el archivo PostScript no cumple los requisitos del estándar.

**Cancelar trabajo:** Crea un archivo de PDF solo si el archivo PostScript cumple los requisitos de PDF/A y es válido en caso contrario.

**Nombre del perfil de calidad de salida:** Indica la condición de impresión caracterizada para la que se ha preparado el documento y es necesaria para el cumplimiento de las normas PDF/A. Si el flujo de trabajo requiere que el documento especifique la información de calidad de salida, seleccione &quot;Ninguno&quot;. El documento no podrá comprobar el cumplimiento si no se proporciona esta información.

**Condición de salida:** Describe la condición de impresión deseada. Esta entrada no es obligatoria, pero puede utilizarse para proporcionar información útil al destinatario previsto del documento de PDF.

## Opciones de vista inicial {#initial-view-options}

Estas opciones están organizadas en tres áreas: Opciones de documento, Opciones de ventana y Opciones de interfaz de usuario. Para obtener instrucciones sobre el acceso a las opciones de la Vista inicial, consulte [Agregar o editar la configuración del PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Para utilizar cualquier opción, seleccione Definir configuración de vista inicial.

### Opciones de documento {#document-options}

Las opciones del documento controlan el aspecto del documento dentro de la ventana del documento, como el nivel de ampliación y cómo se desplaza.

**Mostrar:** Determina qué paneles y pestañas se muestran en la ventana de la aplicación de forma predeterminada. Panel de marcadores y Página abre el panel del documento y muestra la ficha Marcadores.

**Diseño de página:** Determina si el documento se visualiza en modo de una sola página, página enfrentada, página continua o página enfrentada continua.

**Aumentar:** Define el nivel de zoom utilizado para mostrar el documento al abrirlo. El valor predeterminado utiliza el valor de ampliación configurado por el usuario en las preferencias de Acrobat o Adobe Reader.

**Abrir en Número de página:** Establece la página en la que se abre el documento, que suele ser la página 1.

>[!NOTE]
>
>Al establecer Predeterminado para las opciones de ampliación y diseño de página, se utiliza la configuración de usuario individual en las preferencias de Visualización de página en Acrobat o Adobe Reader.

### Opciones de ventana {#window-options}

Las opciones de ventana determinan cómo se ajusta la ventana en el área de pantalla cuando un usuario abre el documento. Sin embargo, las opciones no tienen ningún efecto cuando se visualiza un documento de PDF dentro de un explorador web.

**Cambiar tamaño de ventana a página inicial:** Ajusta la ventana del documento para que se ajuste perfectamente alrededor de la página de apertura, según las opciones seleccionadas en Opciones de documento.

**Centrar ventana en pantalla:** Sitúa la luna en el centro del área de la pantalla.

**Abrir En Modo De Pantalla Completa:** Maximiza la ventana del documento y muestra el documento sin la barra de menús, la barra de herramientas o los controles de ventana.

**Mostrar:** Nombre de archivo muestra el nombre de archivo en la barra de título de la ventana. El título del documento se muestra en la barra de título de la ventana.

### Opciones de interfaz de usuario {#user-interface-options}

Las opciones de la interfaz de usuario determinan qué controles se muestran u ocultan cuando el usuario abre el documento.

**Ocultar barra de menús:** Si está seleccionada, oculta la barra de menús

**Ocultar barras de herramientas:** Si está seleccionada, oculta las barras de herramientas

**Ocultar controles de ventana:** Si está seleccionada, oculta los controles de la ventana

>[!NOTE]
>
>Si oculta la barra de menús y la barra de herramientas, los usuarios no podrán aplicar comandos ni seleccionar herramientas a menos que conozcan los métodos abreviados de teclado cuando abran el archivo en Acrobat.

## Carga y descarga de archivos de prólogo y epílogo {#uploading-and-downloading-prologue-and-epilogue-files}

Los archivos de prólogo se utilizan para agregar código PostScript personalizado que se ejecuta al principio de cada trabajo PostScript que se destila. Los archivos Epilog se utilizan para añadir código PostScript personalizado que se ejecuta al final de cada trabajo PostScript. Puede descargar archivos de prólogo y epílogo del servidor para guardarlos localmente. Es posible que desee descargar los archivos para configurarlos de forma independiente o para cargarlos en otra ubicación o en otro equipo.

Estos archivos tienen muchos propósitos. Por ejemplo, los archivos de prólogo se pueden editar para especificar portadas; los archivos de epílogo se pueden editar para resolver una serie de procedimientos en un archivo PostScript. También puede seleccionar y cargar los archivos de prólogo y epílogo que desea enviar con cada trabajo.

### Descargar un archivo de prólogo o epílogo {#download-a-prologue-or-epilogue-file}

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Configuración de Adobe PDF.
1. Haga clic en Nuevo o haga clic en el nombre de una configuración.
1. Haga clic en Avanzadas y, a continuación, junto a la opción Usar Prolog.ps y Epilog.ps, haga clic en Descargar.
1. En la página Descargar Prolog y archivos de Epilog, haga clic en Prolog.ps o Epilog.ps y, a continuación, en Guardar.

### Carga de un archivo de prólogo o epílogo {#upload-a-prologue-or-epilogue-file}

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Configuración de Adobe PDF.
1. Haga clic en Nuevo o haga clic en el nombre de una configuración.
1. Haga clic en Avanzadas y, a continuación, junto a la opción Usar Prolog.ps y Epilog.ps, haga clic en Cargar.
1. En la página Cargar archivos de prólogo y epílogo, haga clic en Examinar para seleccionar un prólogo o un archivo epílogo.
1. Busque el archivo y haga clic en Abrir.
1. Para utilizar el archivo, asegúrese de que la opción Usar Prolog.ps y Epilog.ps está seleccionada en el área Avanzadas de la página Nuevo/Editar configuración de Adobe PDF.
1. Haga clic en Guardar

>[!NOTE]
>
>PDF Generator sólo admite archivos de prólogo y epílogo para la conversión de archivos PostScript y PostScript encapsulado a PDF.
