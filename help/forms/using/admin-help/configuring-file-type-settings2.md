---
title: Configuración de la configuración del tipo de archivo
seo-title: Configuración de la configuración del tipo de archivo
description: Obtenga información sobre cómo configurar opciones de tipo de archivo.
seo-description: Obtenga información sobre cómo configurar opciones de tipo de archivo.
uuid: d01f430b-9637-4a5f-b3a7-d5ef3e5ecbc5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: adbe8416-c8d7-4581-940b-df62eadf0e26
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '6178'
ht-degree: 2%

---


# Configuración de la configuración del tipo de archivo {#configuring-file-type-settings}

En PDF Generator, puede configurar la configuración de la aplicación para los tipos de archivo admitidos. En Windows, puede configurar la configuración de la aplicación para cada tipo de archivo admitido. En UNIX y Linux, puede configurar la configuración de la aplicación para HTML a PDF y OpenOffice.

En la página Configuración del tipo de archivo, puede realizar las siguientes tareas:

* [Crear o editar una configuración de tipo de archivo](#create-or-edit-file-type-settings)
* Especifique la configuración de tipo de archivo que se usará de forma predeterminada (consulte [Importación y exportación de archivos de configuración del generador de PDF](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html))
* [Cambiar la configuración predeterminada](/help/forms/using/admin-help/configuring-file-type-settings2.md#change-the-default-settings)
* [Habilitar compatibilidad con PDF/A](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)
* [Opción Eliminar tipo de archivo](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)

>[!NOTE]
>
>La configuración del tipo de archivo no está disponible para los convertidores de reserva como Acrobat para conversión de HTML a PDF, Microsoft PowerPoint, Microsoft Word y Microsoft Excel.

## Crear o editar la configuración del tipo de archivo {#create-or-edit-file-type-settings}

Cree o edite una configuración de tipo de archivo para especificar cómo gestiona la aplicación la conversión de tipos de archivo admitidos. En Windows, puede configurar la configuración de la aplicación para cada tipo de archivo admitido. En UNIX y Linux, puede configurar la configuración de la aplicación para HTML a PDF y OpenOffice.

1. En la consola de administración, haga clic en **[!UICONTROL Servicios]** > **[!UICONTROL Generador de PDF]** > **[!UICONTROL Configuración del tipo de archivo]**.
1. Haga clic en Nuevo o en el nombre de una configuración.
1. En el cuadro Extensiones de nombre de archivo, escriba las extensiones de nombre de archivo, separadas por comas, para los tipos de archivo que se aceptan en esta aplicación. No incluya el punto anterior o un espacio entre las extensiones. El valor predeterminado es `bmp,gif,jpeg,jpg,tif,tiff,png`.
1. (Opcional) Para utilizar el reconocimiento de código óptico (OCR) del texto en gráficos o imágenes, seleccione Usar OCR y defina las siguientes opciones:

**Idioma OCR principal:** el idioma que usará el motor OCR para identificar los caracteres. El valor predeterminado es inglés (EE. UU.).

**Estilo de salida PDF:** seleccione Imagen que se puede buscar para que haya una imagen de mapa de bits de las páginas en primer plano y el texto digitalizado en una capa invisible debajo. El aspecto de la página no cambia, pero el texto se puede seleccionar y leer. Seleccione Texto y gráficos con formato para reconstruir la página original utilizando texto reconocido, fuentes, imágenes y otros elementos gráficos. El valor predeterminado es Imagen que se puede buscar (exacta).

**Disminuir resolución de imágenes:** reduce el número de píxeles en imágenes en color, escala de grises y monocromas. La disminución de resolución de imágenes escaneadas se realiza una vez finalizado el OCR. El valor predeterminado es Más bajo (600 ppp). Esta opción no está disponible si establece el estilo de salida PDF en Imagen que se puede buscar (exacta).

1. Complete la información requerida en estas secciones:

   [Importación y exportación de archivos de configuración de PDF Generator](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html)

   [Configuración de exportación de Adobe PDF (solo Windows)](#adobe-pdf-export-settings-windows-only)

   [Configuración de HTML a PDF](#html-to-pdf-settings)

   [Ajustes de Flash de vídeos a PDF](#flash-videos-to-pdf-settings)

   [Configuración de XPS a PDF](#xps-to-pdf-settings)

   [Configuración del optimizador de PDF](#pdf-optimizer-settings)

   [Configuración de Microsoft Excel (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-excel-settings-windows-only)

   [Configuración de Microsoft PowerPoint (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-powerpoint-settings-windows-only)

   [Configuración de Microsoft Project (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-project-settings-windows-only)

   [Configuración de Microsoft Word (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-word-settings-windows-only)

   [Configuración de Microsoft Visio (solo Windows)](#visio)

   [Configuración de Microsoft Publisher (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-publisher-settings-windows-only)

   [Configuración de AutoCAD (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings2.md#autocad-settings-windows-only)

   [Configuración de OpenOffice](/help/forms/using/admin-help/configuring-file-type-settings2.md#openoffice-settings)

   [Configuración de otras aplicaciones (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings2.md#other-applications-settings-windows-only)

   Para ir a otra sección, haga clic en su vínculo en la página web o utilice los botones **[!UICONTROL Siguiente]**o **[!UICONTROL Anterior]**.

1. Después de completar todas las secciones, haga clic en **[!UICONTROL Guardar]** o **[!UICONTROL Guardar como]** y proporcione un nombre para la configuración.

Se puede personalizar la compatibilidad con varios tipos de archivo. (Consulte &quot; [Añadir compatibilidad con formatos de archivo nativos adicionales](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)&quot; en [Programación con formularios AEM](https://www.adobe.com/go/learn_lc_programming_11).)

## Cambiar la configuración predeterminada {#change-the-default-settings}

Puede cambiar el valor predeterminado de la configuración de Adobe PDF, la configuración de seguridad y la configuración de tipo de archivo que se aplican a los orígenes recién creados. El cambio de los valores predeterminados no afecta a la configuración de los orígenes existentes.

1. En la Consola de administración, haga clic en **[!UICONTROL Servicios > Generador de PDF]**.
1. En la página **[!UICONTROL Configuración de Adobe PDF]**, **[!UICONTROL Configuración del tipo de archivo]** o **[!UICONTROL Configuración de seguridad]**, haga clic en **[!UICONTROL Definir configuración predeterminada]**.
1. Seleccione la configuración predeterminada que prefiera. Una o más de las siguientes opciones de configuración están disponibles en la página Definir configuración predeterminada:

   **[!UICONTROL Configuración]** de Adobe PDF: El valor predeterminado original es Estándar (Acrobat 6).

   **[!UICONTROL Configuración]** de seguridad: El valor predeterminado original es Sin seguridad (Acrobat 5).

   **[!UICONTROL Configuración]** del tipo de archivo: El valor predeterminado original es Estándar.

1. Haga clic en **[!UICONTROL Guardar]**.

## Eliminar un ajuste de Tipo de archivo {#delete-a-file-type-setting}

Puede eliminar una configuración de tipo de archivo que ya no se utilice.

1. En la consola de administración, haga clic en **[!UICONTROL Servicios > Generador de PDF> Configuración de tipo de archivo]**.
1. Seleccione la casilla de verificación situada junto a la configuración que desee eliminar. Puede seleccionar varias fuentes. La configuración que no tiene una casilla de verificación junto a ellos siempre se incluye con el generador de PDF y no se puede eliminar.
1. Haga clic en **[!UICONTROL Eliminar]** y, en la página de confirmación de eliminación, haga clic en **[!UICONTROL Eliminar]**.

## Configuración de imagen a PDF {#image-to-pdf-settings}

Las siguientes opciones determinan cómo se convierten los archivos de imagen a PDF. Para obtener instrucciones sobre cómo acceder a esta configuración, consulte [Creación o edición de la configuración del tipo de archivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Extensiones de nombre de archivo:lista separada por** comas de las extensiones de nombre de archivo que se pueden convertir.

**Pruebe el conversor de reserva:** PDF Generator puede utilizar Java™ o Acrobat para convertir archivos de imagen a PDF. Cuando se selecciona esta opción y una conversión falla o alcanza el límite de tiempo de espera especificado, PDF Generator intenta la conversión mediante el método alternativo. Si el método alternativo falla o alcanza el límite de tiempo de espera especificado, se escribe una excepción en el archivo de registro.

>[!NOTE]
>
>Los archivos JPEG 2000 solo se pueden convertir con Acrobat.

**Usar OCR:** especifica si se aplica OCR (reconocimiento óptico de caracteres) al PDF. El software OCR le permite buscar, corregir y copiar el texto en el PDF.

***nota **: La función OCR PDF (PDF en el que se pueden realizar búsquedas) solo es compatible con Microsoft Windows.*

**Idioma OCR principal:** especifica el idioma que usará el motor OCR para identificar los caracteres.

**Estilo de salida PDF:** determina el tipo de PDF que se va a producir. Todos los formatos aplican OCR y reconocimiento de fuentes y páginas a las imágenes de texto y las convierten en texto normal.

**Imagen con capacidad de búsqueda:** garantiza que el texto se pueda buscar y seleccionar. Esta opción mantiene la imagen original, la muestra según sea necesario y coloca una capa de texto invisible sobre ella. La opción Disminuir resolución de imágenes determina si se disminuye la resolución de la imagen y en qué medida.

**Imagen con capacidad de búsqueda (exacta):** garantiza que el texto se pueda buscar y seleccionar. Esta opción mantiene la imagen original y coloca una capa de texto invisible sobre ella. Recomendado para los casos que requieren la máxima fidelidad a la imagen original.

**ClearScan:** sintetiza una nueva fuente Type 3 que se aproxima al original y conserva el fondo de la página mediante una copia de baja resolución.

**Disminuir resolución de imágenes:** reduce el número de píxeles en imágenes en color, escala de grises y monocromas una vez completado el OCR. Elija el grado de disminución de resolución que desee aplicar. Las opciones con mayor número reducen la resolución, lo que produce archivos PDF de mayor resolución.

## Configuración de exportación de Adobe PDF (solo Windows) {#adobe-pdf-export-settings-windows-only}

La opción Exportar tipo de archivo de la sección de configuración de exportación de Adobe PDF se utiliza para convertir un archivo PDF a otro formato. El valor predeterminado es HTML 4.01 con hojas de estilo en cascada (CSS) 1.0 (*.htm, *.html).

Para obtener instrucciones sobre cómo acceder a esta configuración, consulte [Creación o edición de la configuración del tipo de archivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

## Configuración de HTML a PDF {#html-to-pdf-settings}

Las siguientes opciones determinan cómo se convierten los archivos HTML a PDF. Para obtener instrucciones sobre cómo acceder a estas opciones, consulte [Crear o editar la configuración del tipo de archivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Try Fallback Converter:** PDF Generator puede utilizar Java™ o Acrobat para convertir archivos HTML a PDF. Cuando se selecciona esta opción y una conversión falla o alcanza el límite de tiempo de espera especificado, PDF Generator intenta la conversión mediante el método alternativo. Si el método alternativo falla o alcanza el límite de tiempo de espera especificado, se escribe una excepción en el archivo de registro.

**Codificación predeterminada:** establece la codificación de entrada del texto del archivo desde un menú de sistemas operativos y alfabetos. Utiliza la selección mostrada en la opción Codificación predeterminada solo si el archivo de origen HTML no especifica un tipo de codificación.

**Forzar codificación seleccionada:** omite cualquier codificación especificada en el archivo de origen HTML y utiliza la selección mostrada en la opción Codificación predeterminada.

### Configuración de arañas {#spidering-settings}

** Spideringescanea páginas web para buscar vínculos a otras páginas web. Cuando se encuentra un vínculo a otra página web, se busca la página de destino y se incluye en el documento PDF que se genera. Active estas opciones para establecer el número de niveles que se van a recuperar y convertir a PDF:

**Obtener solo niveles X:** arañas de Web y convierte las páginas hasta una profundidad del nivel especificado desde la dirección URL de la página base. Un valor de 1 convierte sólo la dirección URL proporcionada.

**Obtener sitio completo:** convierte todo el sitio, empezando por la dirección URL proporcionada.

**Permanecer en la misma ruta:** los vínculos que apuntan a páginas que no están en la misma ruta relativa que la dirección URL base no se convierten durante la araña.

**Permanecer en el mismo servidor:** los vínculos que apuntan a páginas en diferentes servidores no se convierten durante la araña. Solo se convierten los vínculos que apuntan al mismo servidor que la dirección URL especificada.

### Configuración de conversión de página {#page-conversion-settings}

Active estas opciones para especificar cómo se convierten las páginas HTML. En función del tamaño de la página, los valores de anchura, altura y margen se ajustan en consecuencia.

**Tamaño de página:** elija personalizada y especifique la anchura y la altura, o seleccione dimensiones predefinidas.

**Orientación:** seleccione vertical u horizontal para el documento PDF convertido.

**Márgenes:** especifica los márgenes (Superior, Inferior, Izquierda y Derecha) en el documento PDF generado.

**Añadir marcadores a PDF:** Añade marcadores al documento PDF.

**Habilitar PDF etiquetado:** Incrusta etiquetas en el documento PDF.

**Configuración inicial de Vista:** permite configurar las opciones de Documento, las opciones de ventana y las opciones de interfaz de usuario. Esta configuración determina cómo se muestra inicialmente el contenido.

### Opciones de documento {#document-options}

Habilite estas opciones para especificar cómo mostrar contenido, cómo mostrar páginas en el documento PDF y cómo especificar el nivel de ampliación:

**Mostrar:** seleccione los paneles que se abrirán en Acrobat cuando se abra el documento PDF.

**Diseño de página:** seleccione el tipo de presentación de página para el documento PDF.

**Ampliación:** elija la ampliación preestablecida para la vista inicial del documento PDF o seleccione un valor personalizado. Si elige una configuración predeterminada, se utilizará la ampliación predeterminada de Acrobat.

**Abrir a número de página:** especifique el número de página al que se abre el PDF.

### Opciones de ventana {#window-options}

Active estas opciones para especificar el tamaño y la visualización de la ventana.

**Cambiar el tamaño de la ventana a la página inicial:** cambia el tamaño de la ventana de Acrobat al tamaño de la página inicial.

**Centrar ventana en pantalla:** abre la ventana en el centro de la pantalla.

**Abrir en modo de pantalla completa:** abre la ventana en modo de pantalla completa.

**Mostrar:** muestra el título o el nombre de archivo del documento en la ventana.

### Opciones de interfaz de usuario {#user-interface-options}

Active estas opciones para especificar el aspecto de la ventana:

**Ocultar barra de menús:** oculta la barra de menús en el documento PDF.

**Ocultar barras de herramientas:** oculta las barras de herramientas en el documento PDF.

**Ocultar controles de ventana:** oculta los controles de ventana en el documento PDF.

## Ajustes de Flash de vídeos a PDF {#flash-videos-to-pdf-settings}

PDF Generator admite la capacidad de enviar un vídeo para Adobe Flash (archivo SWF o FLV) y crear un archivo PDF con un vídeo para Adobe Flash incrustado en él. Esta conversión no requiere que el Flash Player de Adobe esté instalado en el servidor de formularios. Para obtener instrucciones sobre cómo acceder a esta opción, consulte [Creación o edición de la configuración del tipo de archivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Extensiones de nombre de archivo:lista separada por** comas de las extensiones de nombre de archivo que se pueden convertir.

## Configuración de XPS a PDF {#xps-to-pdf-settings}

La Especificación de papel XML (XPS) se utiliza en la máquina de impresión de Windows. Es un formato de Microsoft y se puede crear desde cualquier aplicación de Microsoft Office. AEM formularios permite convertir archivos XPS PDF.

**Extensiones de nombre de archivo:** una lista separada por comas de todas las extensiones de nombre de archivo XPS que se pueden convertir. Actualmente hay un formato: .xps.

## Configuración del optimizador de PDF {#pdf-optimizer-settings}

PDF Generator permite reducir el tamaño de los archivos PDF. Tanto si utiliza todos estos ajustes como algunos dependerán de cómo pretenda utilizar los archivos y de las propiedades esenciales que debe tener un archivo. En la mayoría de los casos, la configuración predeterminada es adecuada para lograr la máxima eficacia: ahorra espacio eliminando fuentes incrustadas, comprimiendo imágenes y eliminando elementos de los archivos que ya no son necesarios.

>[!NOTE]
>
>Al optimizar un documento firmado digitalmente, se eliminan e invalidan las firmas digitales.

Para obtener instrucciones sobre cómo acceder a esta configuración, consulte [Creación o edición de la configuración del tipo de archivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Versión de destinatario PDF:** especifica la versión de Acrobat con la que es compatible el PDF.

### Fuentes {#fonts}

1. Seleccione **Fuentes.**
1. Seleccione una de las siguientes opciones:

   **Desincrustar todas las fuentes:** Desincrusta todas las fuentes incrustadas.

   **No desincruste ninguna fuente:** No desincrusta ninguna fuente.

   **Desincrustar algunas fuentes:** Desincrusta solo las fuentes especificadas. Siga estos pasos para especificar las fuentes que desea desincrustar:

   * Si es necesario, seleccione un directorio de fuentes diferente en el menú desplegable **Fuente**. Este menú desplegable lista las fuentes de los directorios especificados en **Inicio > Configuración > Sistema principal > Configuraciones principales**.
   * Seleccione una o varias fuentes de la lista **Fuentes disponibles** y haga clic en **Añadir**. Estas fuentes se agregan a la lista **Fuentes para desincrustar**.
   * Si desea desincrustar algunas fuentes que no existen en el servidor de formularios, introduzca los nombres de dichas fuentes en el cuadro **Añadir fuentes a desincrustar**. Haga clic en **Agregar**.

   >[!NOTE]
   >
   >*Si desea desincrustar algunas fuentes cuyos subconjuntos están incrustados en el documento, anteponga el nombre de la fuente con el signo +. Por ejemplo, &quot;+Helvetica&quot;.*

1. Si desea incrustar solo los subconjuntos en uso de las fuentes incrustadas, seleccione **Subconjunto de todas las fuentes incrustadas**.

   >[!NOTE]
   >
   >*Si está utilizando esta opción en combinación con **Desincrustar algunas fuentes**, las fuentes de la lista de fuentes **Añadir a**desincrustadas aún quedan completamente desincrustadas.*

   >[!NOTE]
   >
   >*El subconjunto de fuentes es la técnica de incrustar sólo una parte de una fuente. Un subconjunto de fuentes solo contiene los caracteres utilizados en el documento.*

### Transparencia {#transparency}

Si el documento PDF incluye ilustraciones con transparencia, puede utilizar la configuración del Optimizador de PDF para acoplar la transparencia y reducir el tamaño del archivo.

>[!NOTE]
>
>Si se selecciona Acrobat 4.0 y posterior como la versión de Destinatario PDF, todos los objetos transparentes se acoplan. Para otras versiones de Destinatario PDF, se admite la transparencia y se puede configurar la transparencia.

Seleccione **Transparencia** para configurar la configuración de transparencia mientras se optimizan los documentos PDF.

**Nivel de** transparenciaEspecifica la cantidad de información de vector que se conservará. Los valores más altos conservan más objetos vectoriales, mientras que los valores más bajos rasterizan más objetos vectoriales; los ajustes intermedios conservan áreas simples en forma vectorial y rasterizan áreas complejas. Seleccione la configuración más baja para rasterizar toda la ilustración.

>[!NOTE]
>
>La cantidad de rasterización que se produce depende de la complejidad de la página y de los tipos de objetos superpuestos.

**Arte de líneas y** TextoResolución a la que se rasterizan todos los objetos, incluidas las imágenes, las ilustraciones vectoriales, el texto y los degradados. Los valores admitidos son de 1 píxeles por pulgada (ppp) a 9600 ppp.

>[!NOTE]
>
>La resolución de texto y arte de línea debe establecerse generalmente en 600-1200 ppp para proporcionar rasterización de alta calidad, especialmente en el serif o en el tipo de punto pequeño.

**Degradado y** mallasResolución en la que se rasterizan el degradado y las mallas. Los valores admitidos son de 1 ppp a 1200 ppp.

>[!NOTE]
>
>La resolución de malla y degradado debe establecerse generalmente en 150-300 ppp, ya que la calidad de los degradados, las sombras paralelas y las plumas no mejora con resoluciones más altas, pero el tiempo de impresión y el tamaño del archivo aumentan.

**Convertir todo el texto en** contornosConvierte todos los objetos de tipo (tipo de punto, tipo de área y tipo de ruta) en contornos y descarta toda la información de tipo de glifo en páginas con transparencia. Esta opción garantiza que la anchura del texto sea la misma durante el acoplamiento. Tenga en cuenta que al habilitar esta opción, las fuentes pequeñas aparecerán ligeramente más gruesas cuando se vean en Acrobat o se impriman en impresoras de escritorio de baja resolución. No afecta a la calidad del tipo impreso en impresoras o fotocomponedoras de alta resolución.

**Convertir todos los trazos en** contornosConvierte todos los trazos en trazados rellenos simples en páginas con transparencia. Esta opción garantiza que la anchura de los trazos sea la misma durante el acoplamiento. Tenga en cuenta que, al habilitar esta opción, los trazos finos aparecen ligeramente más gruesos y pueden degradar el rendimiento de acoplamiento.

**Recortar** regiones complejasGarantiza que los límites entre las ilustraciones vectoriales y las rasterizadas se sitúen a lo largo de los trazados de objetos. Esta opción reduce los artefactos de unión que se producen cuando parte de un registro

<!--
NOTE to WRITER: Unfinished sentence above.
-->

>[!NOTE]
>
>Algunos controladores de impresión procesan las ilustraciones rasterizadas y vectoriales de forma diferente, lo que a veces da como resultado la unión de colores. Es posible que pueda minimizar los problemas de costura desactivando algunos ajustes de gestión de color específicos del controlador de impresión. Esta configuración varía según la impresora, así que consulte la documentación que viene con la impresora para obtener más información.

Mantener sobreimpresión: Combina el color de la ilustración transparente con el color de fondo para crear un efecto de sobreimpresión.

La siguiente tabla muestra los tipos comunes de impresoras y su resolución medida en ppp, su regla de pantalla predeterminada medida en líneas por pulgada (lpi) y una resolución de remuestreo para imágenes medidas en píxeles por pulgada (ppp). Por ejemplo, si se imprimiera en una impresora láser de 600 ppp, se introduciría 170 para la resolución en la que se remuestrearían las imágenes.

**** ImágenesSeleccione Imágenes para especificar opciones de compresión y remuestreo para imágenes en color, escala de grises y monocromas. Es posible que desee experimentar con estas opciones para encontrar un equilibrio adecuado entre el tamaño del archivo y la calidad de la imagen.La configuración de resolución de las imágenes en color y escala de grises debe ser de 1,5 a 2 veces la configuración de la pantalla de línea en la que se imprimirá el archivo. La resolución de las imágenes monocromas debe ser la misma que la del dispositivo de salida, pero tenga en cuenta que al guardar una imagen monocroma con una resolución superior a 1500 ppp, se aumenta el tamaño del archivo sin mejorar notablemente la calidad de la imagen. Las imágenes que se van a ampliar, como los mapas, pueden requerir resoluciones más altas.

>[!NOTE]
>
>El remuestreo de imágenes monocromas puede tener resultados de visualización inesperados, como la ausencia de visualización de imágenes. Si esto sucede, desactive el remuestreo y vuelva a convertir el archivo. Es muy probable que este problema ocurra con el submuestreo y menos probable con la disminución de resolución bicúbica.

<table>
 <tbody>
  <tr>
   <th><p><strong>Resolución de impresora</strong></p> </th>
   <th><p><strong>Pantalla de línea predeterminada</strong></p> </th>
   <th><p><strong>Resolución de imágenes</strong></p> </th>
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
   <td><p>1200 ppp (fotocomponedor)</p> </td>
   <td><p>120 lpp</p> </td>
   <td><p>240 ppp</p> </td>
  </tr>
  <tr>
   <td><p>2400 ppp (fotocomponedor)</p> </td>
   <td><p>150 lpp</p> </td>
   <td><p>300 ppp</p> </td>
  </tr>
 </tbody>
</table>

#### Descartar objetos {#discard-objects}

* Seleccione **Descartar objetos** para especificar los objetos que desea quitar del PDF y optimizar las líneas curvas en los dibujos CAD.
* **Descartar Todas Las Acciones** De Envío, Importación Y Restauración De Formularios: Deshabilita todas las acciones relacionadas con el envío o la importación de datos de formulario y restablece los campos de formulario. Esta opción conserva los objetos de formulario a los que están vinculadas las acciones.
* **Descartar todas las acciones** de JavaScript: Quita del PDF cualquier acción que utilice JavaScript.
* **Descartar miniaturas** de página incrustadas: Quita las miniaturas de página incrustadas. Esta opción es útil para documentos grandes, que pueden tardar mucho tiempo en dibujar miniaturas de página después de hacer clic en el botón Páginas.
* **Convertir líneas suaves en curvas**: Reduce el número de puntos de control utilizados para crear curvas en dibujos CAD, lo que da como resultado archivos PDF más pequeños y una representación en pantalla más rápida.
* **Descartar configuración** de impresión incrustada: Quita del documento la configuración de impresión incrustada, como el escalado de página y el modo dúplex.
* **Descartar marcadores**: Quita todos los marcadores del documento.
* **Acoplar campos** de formulario: Impide que los campos de formulario se puedan utilizar sin modificar su aspecto. Los datos del formulario se combinan con la página para convertirse en contenido de la página.
* **Descartar todas las imágenes** alternativas: Elimina todas las versiones de una imagen, excepto la versión destinada a la visualización en pantalla. Algunos archivos PDF incluyen varias versiones de la misma imagen para distintos fines, como la visualización en pantalla de baja resolución y la impresión de alta resolución.
* **Descartar etiquetas** de Documento: Quita las etiquetas del documento, lo que también elimina las funciones de accesibilidad y reflujo del texto.
* **Detectar Y Combinar Fragmentos** De Imagen: Busca imágenes o máscaras fragmentadas en sectores finos e intenta combinar los sectores en una sola imagen o máscara.
* **Descartar índice** de búsqueda integrada: Elimina los índices de búsqueda incrustados, lo que reduce el tamaño del archivo.

#### Descartar datos de usuario {#discard-user-data}

Seleccione **Descartar datos de usuario** para eliminar cualquier información personal que no desee distribuir o compartir con otros usuarios.

* **Descartar Todos Los Comentarios, Forms Y Multimedia**: Quita todos los comentarios, formularios, campos de formulario y elementos multimedia del PDF.
* **Descartar todos los datos** del objeto: Quita todos los objetos del PDF.
* **Descartar referencias** cruzadas externas: Quita los vínculos a otros documentos. Los vínculos que dirigen a otras ubicaciones dentro del PDF no se eliminan.
* **Descartar Contenido De Capa Oculto Y Acoplar Capas** Visibles: Reduce el tamaño del archivo. El documento optimizado se parece al PDF original, pero no contiene información de capa.
* **Descartar Información Y Metadatos** De Documento: Elimina la información del diccionario de información de documento y todos los flujos de metadatos. (Utilice el comando Guardar como para restaurar flujos de metadatos a una copia del PDF).
* **Descartar archivos adjuntos**: Quita todos los archivos adjuntos, incluidos los archivos adjuntos agregados al PDF como comentarios. (PDF Optimizer no optimiza los archivos adjuntos).
* **Descartar Datos Privados De Otras Aplicaciones**: Elimina información de un documento PDF que solo resulta útil para la aplicación que creó el documento. Esta configuración no afecta a la funcionalidad del PDF, pero sí reduce el tamaño del archivo.

### Limpiar {#clean-up}

Seleccione **Limpiar** para eliminar elementos innecesarios del documento.
Estos elementos incluyen elementos que son obsoletos o innecesarios para el uso previsto del documento. La eliminación de ciertos elementos puede afectar gravemente a la funcionalidad del PDF. De forma predeterminada, solo se seleccionan los elementos que no afectan a la funcionalidad. Si no está seguro de las implicaciones de eliminar otras opciones, utilice las selecciones predeterminadas.

**Compresión**

Seleccione una de las siguientes opciones de compresión Flate en el menú desplegable:

* Comprimir todo el archivo
* Comprimir la estructura del documento
* Eliminar compresión
* Dejar intacta la compresión

**Utilice Flate Para Codificar Flujos Que No Estén Codificados**: Aplica compresión Flate a todos los flujos que no están codificados.

**Descartar marcadores** no válidos: Elimina los marcadores que apuntan a páginas del documento que se eliminan.

**Descartar destinos** con nombre sin referencia: Quita los destinos con nombre a los que no se hace referencia internamente desde el documento PDF. Esta opción no comprueba los vínculos de otros archivos PDF o sitios web.

**Optimizar el PDF para una Vista** Web rápida: Reestructura un documento PDF para la descarga página a página (servicio de bytes) desde servidores Web.

**En Flujos Que Utilizan Codificación LZW, Utilice Flate En Su Lugar**: Aplica compresión Flate a todos los flujos de contenido e imágenes que utilizan la codificación LZW.

**Descartar vínculos** no válidos: Quita los vínculos que dirigen a destinos no válidos.

**Optimizar el contenido** de la página: Convierte todos los caracteres de fin de línea en caracteres de espacio, lo que mejora la compresión Flate.

## Configuración de Microsoft Excel (solo Windows) {#microsoft-excel-settings-windows-only}

Estas opciones determinan cómo se convierten los archivos de Microsoft Excel. Para obtener instrucciones sobre cómo acceder a estas opciones, consulte [Crear o editar la configuración del tipo de archivo](#create-or-edit-file-type-settings).

**Pruebe OpenOffice As Fallback Converter**: Cuando esta opción está seleccionada y una conversión que utiliza Microsoft Excel falla o alcanza el límite de tiempo de espera especificado, PDF Generator intenta la conversión mediante OpenOffice. Si la conversión mediante OpenOffice falla o alcanza el límite de tiempo de espera especificado, se escribe una excepción en el archivo de registro.

**Extensiones** de nombre de archivo: Especifica las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan para esta aplicación. El valor predeterminado es `xls,xlsx`. No incluya un punto antes o un espacio entre las extensiones.

**Crear archivo** compatible con PDF/A-1a: Fuerza el uso de la configuración de Adobe PDF RGB PDF/A-1b:2005.

**Añadir marcadores a Adobe PDF**: Convierte los nombres de las hojas de cálculo de Excel en marcadores. Esta opción está seleccionada de forma predeterminada.

**Ajustar hoja de cálculo a una sola página**: Reduce el tamaño del texto para que se ajuste a la hoja de cálculo en una sola página.

**Convertir todo el libro**: Convierte todas las hojas de cálculo del archivo de Excel. Si esta opción no está seleccionada, solo se convierte la página actual.

**Ejecutar macros automáticamente**: Ejecuta las macros del documento de Excel (como una macro que inserta la hora actual) antes de convertir el documento.

**Convertir información** de Documento: Añade las propiedades del documento PDF en función de la información de documento del archivo de origen. Esto incluye información como título de documento, autor, asunto y palabras clave.

**Añadir vínculos a Adobe PDF**: Convierte los hipervínculos del archivo de origen en hipervínculos del documento PDF.

**Adjuntar archivo de origen a Adobe PDF**: Cuando se selecciona esta opción, la hoja de cálculo original de Excel se inserta como un archivo adjunto dentro del documento PDF generado.

**Habilite Accesibilidad Y Reflow Con Adobe PDF** Etiquetado: Incrusta las etiquetas dentro del documento PDF para permitir la accesibilidad y el reflujo.

**Lista De Los Agregados De Excel Para Cargar**: De forma predeterminada (por motivos de seguridad), no se ejecuta ningún complemento de Excel cuando se convierte un archivo de Excel a PDF. Para permitir que ciertos complementos de Excel se ejecuten durante la conversión, proporcione una lista separada por comas de los nombres de los complementos.

**Lista De Hojas De Cálculo Para Convertir**: Cuando este cuadro está vacío, todas las hojas de cálculo de la hoja de cálculo de Excel se incluyen en el PDF generado. Para convertir selectivamente un subconjunto de las hojas de cálculo, proporcione una lista separada por comas de los nombres de las hojas de cálculo.

## Configuración de Microsoft PowerPoint (solo Windows) {#microsoft-powerpoint-settings-windows-only}

Estas opciones determinan cómo se convierten los archivos de Microsoft PowerPoint. Para obtener instrucciones sobre cómo acceder a estas opciones, consulte [Crear o editar la configuración del tipo de archivo](/help/forms/using/admin-help/configuring-file-type-settings2.md#create-or-edit-file-type-settings).

**[!UICONTROL Pruebe OpenOffice As Fallback Converter]**: Cuando esta opción está seleccionada y una conversión que utiliza Microsoft PowerPoint falla o alcanza el límite de tiempo de espera especificado, PDF Generator intenta la conversión mediante OpenOffice. Si la conversión mediante OpenOffice falla o alcanza el límite de tiempo de espera especificado, se escribe una excepción en el archivo de registro.

**[!UICONTROL Extensiones]** de nombre de archivo: Especifica las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan para esta aplicación. El valor predeterminado es ppt,pptx. No incluya un punto antes o un espacio entre las extensiones.

**[!UICONTROL Convertir información]** de Documento: Añade información de documento desde el cuadro de diálogo Propiedades del archivo de origen, incluso título, asunto, autor, palabras clave, administrador, compañía, categoría y comentarios. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Añadir marcadores a Adobe PDF]**: Convierte títulos de PowerPoint en marcadores. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Adjuntar archivo de origen a Adobe PDF]**: Añade el archivo de origen en el archivo PDF como un archivo adjunto. Esta opción está desactivada de forma predeterminada.

**[!UICONTROL Habilite Accesibilidad Y Reflow Con Adobe PDF]** Etiquetado: Incrusta etiquetas en el archivo PDF. Esta opción está desactivada de forma predeterminada.

**[!UICONTROL Convertir multimedia a PDF multimedia]**: Convierte multimedia a PDF multimedia, siempre que sea posible. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Convertir notas]** del ponente: Convierte las notas del ponente a PDF.

**[!UICONTROL Ejecutar macros automáticamente]**: Ejecuta las macros del documento de PowerPoint (como una macro que inserta la hora actual) antes de convertir el documento.

**[!UICONTROL Diseño PDF basado en la configuración]** de impresora de PowerPoint: Utiliza la configuración de la impresora PowerPoint para diseñar el documento PDF.

**[!UICONTROL Añadir vínculos a Adobe PDF]**: Conserva los vínculos existentes cuando se convierte el archivo. El aspecto de los vínculos generalmente no cambia. Los vínculos solo se pueden crear si también está seleccionada la opción Activar accesibilidad. Esta opción está desactivada de forma predeterminada.

**[!UICONTROL Guardar Transiciones De Diapositivas En Adobe PDF]**: Convierte transiciones de diapositivas. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Guardar Animaciones En Adobe PDF]**: Guarda las animaciones convertidas en el archivo PDF.

**[!UICONTROL Convertir diapositivas ocultas en páginas]** PDF: Convierte diapositivas ocultas.

**[!UICONTROL Crear archivo]** compatible con PDF/A-1a: Fuerza el uso de la configuración de Adobe PDF RGB PDF/A-1b:2005. Algunas funciones de PowerPoint no se convierten cuando se produce un archivo PDF. Si una transición de PowerPoint no tiene una transición equivalente en Acrobat, se sustituye una transición similar. Si hay varios efectos de animación en la misma diapositiva, se utiliza un solo efecto. Se convierten las transiciones de página y las viñetas.

## Configuración de Microsoft Project (solo Windows) {#microsoft-project-settings-windows-only}

Estas opciones determinan cómo se convierten los archivos de Microsoft Project. Para obtener instrucciones sobre cómo acceder a estas opciones, consulte [Crear o editar la configuración del tipo de archivo](#create-or-edit-file-type-settings).

1. **[!UICONTROL Extensiones de nombre de archivo:]** especifica las extensiones de nombre de archivo para tipos de archivo, separadas por comas, que se aceptan para esta aplicación. El valor predeterminado es `mpp`. No incluya un punto antes o un espacio entre las extensiones.

1. **[!UICONTROL Convertir información]** de Documento: Añade información de documento desde el cuadro de diálogo Propiedades del archivo de origen, incluso título, asunto, autor, palabras clave, administrador, compañía, categoría y comentarios. Esta opción está seleccionada de forma predeterminada.
1. **[!UICONTROL Adjuntar archivo de origen a Adobe PDF]**: Añade el archivo de origen en el archivo PDF como un archivo adjunto.
1. **[!UICONTROL Crear archivo]** compatible con PDF/A-1a: Fuerza el uso de la configuración de Adobe PDF RGB PDF/A-1b:2005.
1. **[!UICONTROL Ejecutar macros automáticamente]**: Ejecuta las macros del documento de Microsoft Project (como una macro que inserta la hora actual) antes de convertir el documento.

## Configuración de Microsoft Word (solo Windows) {#microsoft-word-settings-windows-only}

Estas opciones determinan cómo se convierten los archivos de Microsoft Word. Para obtener instrucciones sobre cómo acceder a estas opciones, consulte [Crear o editar la configuración del tipo de archivo](#create-or-edit-file-type-settings).

**[!UICONTROL Pruebe OpenOffice As Fallback Converter]**: Cuando esta opción está seleccionada y una conversión que utiliza Microsoft Word falla o alcanza el límite de tiempo de espera especificado, PDF Generator intenta la conversión mediante OpenOffice. Si la conversión mediante OpenOffice falla o alcanza el límite de tiempo de espera especificado, se escribe una excepción en el archivo de registro.

**[!UICONTROL Extensiones]** de nombre de archivo: Especifica las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan para esta aplicación. El valor predeterminado es `doc,docx,rtf,txt`. No incluya un punto antes o un espacio entre las extensiones.

**[!UICONTROL Convertir información]** de Documento: Añade información de documento desde el cuadro de diálogo Propiedades del archivo de origen, incluso título, asunto, autor, palabras clave, administrador, compañía, categoría y comentarios. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Añadir marcadores a Adobe PDF]**: Convierte los encabezados en marcadores. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Adjuntar archivo de origen a Adobe PDF]**: Añade el archivo de origen en el archivo PDF como un archivo adjunto.

**[!UICONTROL Convertir Referencias Cruzadas Y Tabla De Contenido En Vínculos]**: Convierte todas las referencias cruzadas y las entradas de la tabla de contenido en vínculos. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Habilite Accesibilidad Y Reflow Con Adobe PDF]** Etiquetado: Incrusta etiquetas en el archivo PDF. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Crear archivo]** compatible con PDF/A-1a: Si se selecciona, fuerza el uso de la configuración de Adobe PDF RGB PDF/A-1b:2005.

**[!UICONTROL Ejecutar macros automáticamente]**: Ejecuta las macros del documento de Word (como una macro que inserta la hora actual) antes de convertir el documento.

**[!UICONTROL Conservar el marcado de Documento en Adobe PDF]**: Convierte las marcas del documento de Word en anotaciones del archivo PDF.

**[!UICONTROL Añadir vínculos a Adobe PDF]**: Convierte los hipervínculos del archivo de origen en hipervínculos del documento PDF.

**[!UICONTROL Convertir Vínculos]** De Notas Al Pie Y Notas Al Final: Crea vínculos desde las citas de notas al pie y notas al final a notas en el documento PDF.

**[!UICONTROL Convertir comentarios mostrados a notas en Adobe PDF]**: Convierte los comentarios del documento de Word en notas de texto del documento PDF.

**[!UICONTROL Habilitar etiquetado]** avanzado: Añade las etiquetas avanzadas para mejorar la accesibilidad.

**[!UICONTROL Convertir todos los estilos en marcadores]**: Convierte todos los estilos del documento de Word en marcadores en el documento PDF.

**[!UICONTROL Estilos con niveles]**: Especifica qué estilos del documento de Word se convierten en marcadores en el documento PDF. También especifica el nivel de los marcadores. Para utilizar esta función, anule la selección de la opción **[!UICONTROL Convertir todos los estilos en marcadores]** y especifique los nombres de estilo en el siguiente formato:

styleName1=level1[,styleName2=level2...]

Si un nombre de estilo de Microsoft Word incluye una coma (,) o un signo igual (=), preceda los caracteres especiales con el carácter de escape (&quot;\_). Por ejemplo, especifique un estilo denominado &quot;Encabezado, 1&quot; como Encabezado\, 1.

## Configuración de Microsoft Visio (solo Windows) {#visio}

**Convertir información** de Documento: Añade información de documento desde el cuadro de diálogo Propiedades del archivo de origen, incluso título, asunto, autor, palabras clave, administrador, compañía, categoría y comentarios. Esta opción está seleccionada de forma predeterminada. Esta opción está activada de forma predeterminada.

**Añadir vínculos a Adobe PDF**: Conserva todos los vínculos. Esta opción está seleccionada de forma predeterminada.

**Añadir marcadores a Adobe PDF**: Convierte los encabezados en marcadores. Esta opción está seleccionada de forma predeterminada.

**Adjuntar archivo de origen a Adobe PDF**: Añade el archivo de origen en el archivo PDF como un archivo adjunto.

**Acoplar siempre capas en Adobe PDF**: Acopla todas las capas de Visio.

**Convertir todas las páginas**: Convierte todas las páginas del archivo de Visio.

**Abra El Panel Capas Cuando Lo Vea En Adobe Acrobat**: Si las capas de Visio no están acopladas, abre una ventana en la que puede especificar las capas que se conservan en el archivo PDF al abrirlas con Acrobat. Esta opción está seleccionada de forma predeterminada.

**Crear archivo** compatible con PDF/A-1b: Fuerza el uso de la configuración de Adobe PDF PDF/A-1b:2005 (RGB).

**Convertir comentarios en comentarios** de Adobe PDF: Convierte las notas de Visio en comentarios PDF.

## Configuración de Microsoft Publisher (solo Windows) {#microsoft-publisher-settings-windows-only}

Estas opciones determinan cómo se convierten los archivos de Microsoft Publisher. Para obtener instrucciones sobre cómo acceder a estas opciones, consulte [Crear o editar la configuración del tipo de archivo](#create-or-edit-file-type-settings).

**[!UICONTROL Extensiones]** de nombre de archivo: Especifica las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan para esta aplicación. El valor predeterminado es `pub`. No incluya un punto antes o un espacio entre las extensiones.

## Configuración de AutoCAD (solo Windows) {#autocad-settings-windows-only}

Estas opciones determinan cómo se convierten los archivos de AutoCAD. Para obtener instrucciones sobre cómo acceder a estas opciones, consulte [Crear o editar la configuración del tipo de archivo](/help/forms/using/admin-help/configuring-file-type-settings2.md#create-or-edit-file-type-settings).

**[!UICONTROL Extensiones]** de nombre de archivo: Especifica las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan para esta aplicación. El valor predeterminado es `dwg`. No incluya un punto antes o un espacio entre las extensiones.

**[!UICONTROL Convertir información]** de Documento: Añade información de documento desde el cuadro de diálogo Propiedades del archivo de origen, incluso título, asunto, autor, palabras clave, administrador, compañía, categoría y comentarios. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Añadir marcadores a Adobe PDF]**: Convierte los encabezados en marcadores.

**[!UICONTROL Acoplar siempre capas en Adobe PDF]**: Acopla todas las capas de AutoCAD.

**[!UICONTROL Abra El Panel Capas Cuando Se Vea En Adobe Acrobat]**: Muestra la estructura de capas al abrir el PDF en Acrobat.

**[!UICONTROL Crear archivo]** compatible con PDF/E-1: Crea un archivo compatible con PDF/E-1. PDF/E es una norma ISO para el intercambio de documentación técnica e ingeniería. Para obtener más información sobre PDF/E-1, consulte [estándares de Adobe y del sector](https://www.adobe.com/enterprise/standards/index.html).

**[!UICONTROL Convertir todos los diseños]**: Incluye todos los diseños del PDF.

**[!UICONTROL Convertir espacio de modelo a 3D]**: Cuando se selecciona, la presentación del espacio del modelo se convierte en una anotación 3D en el PDF.

**[!UICONTROL Añadir vínculos a Adobe PDF]**: Si se selecciona, se conservan todos los vínculos.

**[!UICONTROL Adjuntar archivo de origen a Adobe PDF]**: Añade el archivo de origen en el archivo PDF como un archivo adjunto.

**[!UICONTROL Crear archivo]** compatible con PDF/A-1b: Fuerza el uso de la configuración de Adobe PDF PDF/A-1b.

**[!UICONTROL Convertir todas las capas]**: De forma predeterminada, PDF Generator convierte sólo la capa predeterminada de los archivos de AutoCAD a PDF en lugar de todas las capas del archivo. Seleccione esta opción para convertir todas las capas del archivo.

**[!UICONTROL Incrustar información]** de escala: Conserva la información de escala de dibujo.

**[!UICONTROL Convertir diseño]** actual: Solo incluye la presentación actual en el PDF.

**[!UICONTROL Lista De Diseños De AutoCAD Para Convertir]**: Un dibujo de AutoCAD puede tener varias maquetaciones. Cuando este cuadro está vacío, todos los diseños del dibujo de AutoCAD se incluyen en el documento PDF generado. Para convertir selectivamente un subconjunto de los diseños, proporcione una lista de nombres de diseño separados por comas.

## Configuración de OpenOffice {#openoffice-settings}

Estas opciones determinan cómo se convierten los archivos de OpenOffice. Para obtener instrucciones sobre cómo acceder a estas opciones, consulte [Crear o editar la configuración del tipo de archivo](/help/forms/using/admin-help/configuring-file-type-settings2.md#create-or-edit-file-type-settings).

**Pruebe PDFMaker As Fallback Converter**: Cuando esta opción está seleccionada y una conversión que utiliza OpenOffice falla o alcanza el límite de tiempo de espera especificado, PDF Generator intenta la conversión mediante PDFMaker. Si la conversión mediante PDFMaker falla o alcanza el límite de tiempo de espera especificado, se escribe una excepción en el archivo de registro.

**Extensiones** de nombre de archivo: Especifique las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan para esta aplicación. El valor predeterminado es `odt,odp,ods,odg,odf,sxw,sxi,sxd`. No incluya un punto antes o un espacio entre las extensiones.

**Intervalo**: Convierta todas las páginas o especifique páginas específicas o un intervalo de páginas. Si no se define un intervalo de páginas, se convierten todas las páginas. Para exportar un rango de páginas, utilice el formato 3-6. Para exportar páginas individuales, utilice el formato 7;9;11. Puede exportar una combinación de intervalos de páginas y páginas individuales utilizando un formato como 3-6;8;10;12.

**Orientación** de página: Solo para archivos de texto sin formato, seleccione vertical u horizontal para el documento PDF convertido.

**Imágenes**: Configure cómo se convierten las imágenes. Las imágenes EPS con previsualizaciones incrustadas solo se exportan como previsualizaciones. Las imágenes EPS sin previsualizaciones incrustadas se exportan como marcadores de posición vacíos. Con la compresión sin pérdida de imágenes, se conservan todos los píxeles. Con la compresión JPEG de imágenes y un nivel de alta calidad, se conservan casi todos los píxeles. Con un nivel de baja calidad, se pierden algunos píxeles y se introducen artefactos, pero se reducen los tamaños de archivo.

**General**: Active las opciones para convertir un PDF con etiquetas o para exportar notas de documento de Writer y FormCalc, efectos de transición de diapositivas de Impresión o páginas en blanco al PDF. Cuando se exportan etiquetas, el tamaño del archivo puede aumentar en grandes cantidades. Algunas etiquetas que se exportan son tablas de contenido, hipervínculos y controles.

También puede especificar cómo se envían los formularios. Las opciones son XML, FDF, PDF o HTML. Esta configuración anula la propiedad URL del control que se establece en el documento. Solo se puede seleccionar una configuración común para el documento PDF:

* PDF (envía el documento completo)
* FDF (envía el contenido del control)
* HTML
* XML

**PDF** con etiquetas: Permite la creación de archivos PDF con etiquetas desde documentos de OpenOffice. El PDF etiquetado contiene información sobre la estructura del contenido del documento. Esto puede ayudar a mostrar el documento en dispositivos con pantallas diferentes y al utilizar software de lector de pantalla. También ayuda al software de accesibilidad a realizar varias operaciones útiles con el documento PDF, como leer en voz alta el contenido del documento PDF.

**Notas** de exportación: Convierte las notas de los documentos de OpenOffice en notas del documento PDF generado.

**Usar efectos** de Transición: Convierte los efectos de transición de diapositivas en presentaciones de OpenOffice a los efectos de transición de PDF correspondientes.

**Enviar Forms en formato**: Crea un formulario PDF que el usuario del documento PDF puede rellenar e imprimir.

**Exportar páginas** en blanco insertadas automáticamente: Cuando se selecciona esta opción, las páginas en blanco insertadas automáticamente se incluyen en el documento PDF generado. Esto resulta útil si va a imprimir un doble de documento PDF a una cara. Por ejemplo, se puede configurar un libro para que la primera página del capítulo siempre tenga inicios en una página impar. Si el capítulo anterior termina en una página impar, OpenOffice inserta una página par en blanco. Esta opción controla si se incluye esa página par en el PDF generado.

## Otros ajustes de la aplicación (solo Windows) {#other-applications-settings-windows-only}

No puede cambiar la configuración de otras aplicaciones a través de la consola de administración; muestran las extensiones de nombre de archivo para los tipos de archivo admitidos. Para obtener instrucciones sobre cómo acceder a esta configuración, consulte [Creación o edición de la configuración del tipo de archivo](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html).

* Corel WordPerfect: `wpd`
* PageMaker de Adobe: `pmd, pm6, p65, pm`
* Adobe FrameMaker: `fm`
* Adobe Photoshop: `psd`

Es posible que sea necesario personalizar la compatibilidad con estos tipos de archivos. Para obtener más información, consulte &quot;Añadir compatibilidad con formatos de archivo nativos adicionales&quot; en [Programación con formularios AEM](https://www.adobe.com/go/learn_aemforms_programming_62).

Para obtener ayuda sobre la configuración de una impresora de red PDFG, consulte [Configuración de una impresora de red PDFG (solo Windows)](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md).
