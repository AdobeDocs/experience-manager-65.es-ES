---
title: Configuración de la configuración del tipo de archivo
seo-title: Configuring file type settings
description: Obtenga información sobre cómo configurar opciones de tipo de archivo.
seo-description: Learn how to configure file type settings.
uuid: ab037659-c6ff-4de9-9417-f5a6fc8122cb
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ab19b248-8931-4cf6-b6a5-fb7b067c4a49
feature: PDF Generator
exl-id: 1a6640cc-22ef-41d5-a0c6-7a2c2dabcef1
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '6158'
ht-degree: 2%

---

# Configuración de la configuración del tipo de archivo {#configuring-file-type-settings}

En Generador de PDF, puede configurar la configuración de la aplicación para los tipos de archivo admitidos. En Windows, puede configurar la configuración de la aplicación para cada tipo de archivo admitido. En UNIX y Linux, puede configurar la configuración de la aplicación para HTML a PDF y OpenOffice.

En la página Configuración de tipo de archivo , puede realizar las siguientes tareas:

* [Crear o editar una configuración de Tipo de archivo](#create-or-edit-file-type-settings)
* Especifique qué configuración de tipo de archivo utilizar de forma predeterminada (consulte [Importación y exportación de archivos de configuración de PDF Generator](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md))
* [Cambiar la configuración predeterminada](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings)
* [Habilitar compatibilidad con PDF/A](/help/forms/using/admin-help/enable-pdf-a-support.md)
* [Eliminar una configuración de Tipo de archivo](/help/forms/using/admin-help/enable-pdf-a-support.md)

>[!NOTE]
>
>La configuración del tipo de archivo no está disponible para los convertidores de reserva, como Acrobat para conversión de HTML a PDF, Microsoft PowerPoint, Microsoft Word y Microsoft Excel.

## Crear o editar la configuración de Tipo de archivo {#create-or-edit-file-type-settings}

Cree o edite una configuración de tipo de archivo para especificar cómo gestiona la aplicación la conversión de tipos de archivo admitidos. En Windows, puede configurar la configuración de la aplicación para cada tipo de archivo admitido. En UNIX y Linux, puede configurar la configuración de la aplicación para HTML a PDF y OpenOffice.

1. En la consola de administración, haga clic en **[!UICONTROL Servicios]** > **[!UICONTROL Generador de PDF]** > **[!UICONTROL Configuración de tipo de archivo]**.
1. Haga clic en Nuevo o en el nombre de una configuración.
1. En el cuadro Extensiones de nombre de archivo , escriba las extensiones de nombre de archivo, separadas por comas, para los tipos de archivo que se aceptan en esta aplicación. No incluya el punto antes o un espacio entre las extensiones. El valor predeterminado es `bmp,gif,jpeg,jpg,tif,tiff,png`.
1. (Opcional) Para utilizar el reconocimiento óptico de código (OCR) del texto en gráficos o imágenes, seleccione Usar OCR y defina las siguientes opciones:

**Idioma principal de OCR:** El idioma que debe utilizar el motor OCR para identificar los caracteres. El valor predeterminado es inglés (EE. UU.).

**Estilo de salida del PDF:** Seleccione Imagen que se puede buscar para tener una imagen de mapa de bits de las páginas en primer plano y el texto escaneado en una capa invisible debajo. El aspecto de la página no cambia, pero el texto se puede seleccionar y leer. Seleccione Texto y gráficos con formato para reconstruir la página original utilizando texto, fuentes, imágenes y otros elementos gráficos reconocidos. El valor predeterminado es Imagen buscable (exacta).

**Descargar imágenes:** Reduce el número de píxeles en imágenes en color, escala de grises y monocromas. El muestreo de imágenes escaneadas se realiza una vez finalizado el OCR. El valor predeterminado es el más bajo (600 ppp). Esta opción no está disponible si establece el estilo de salida del PDF en Imagen buscable (Exacta).

1. Complete la información requerida en estas secciones:

[Importación y exportación de archivos de configuración de PDF Generator](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md)

[Configuración de exportación de Adobe PDF (solo Windows)](#adobe-pdf-export-settings-windows-only)

[Configuración de HTML a PDF](#html-to-pdf-settings)

[Flash de vídeos a la configuración de PDF](#flash-videos-to-pdf-settings)

[Configuración de XPS a PDF](#xps-to-pdf-settings)

[Configuración del optimizador de PDF](/help/forms/using/admin-help/configuring-file-type-settings.md)

[Configuración de Microsoft Excel (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-excel-settings-windows-only)

[Configuración de Microsoft PowerPoint (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-powerpoint-settings-windows-only)

[Configuración del proyecto de Microsoft (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-project-settings-windows-only)

[Configuración de Microsoft Word (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-word-settings-windows-only)

[Configuración de Microsoft Visio (solo Windows)](#visio)

[Configuración de Microsoft Publisher (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-publisher-settings-windows-only)

[Configuración de AutoCAD (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#autocad-settings-windows-only)

[Configuración de OpenOffice](/help/forms/using/admin-help/configuring-file-type-settings.md#openoffice-settings)

[Configuración de otras aplicaciones (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#other-applications-settings-windows-only)

   Para ir a otra sección, haga clic en su vínculo en la página web o utilice el **[!UICONTROL Siguiente]** o **[!UICONTROL Anterior]** botones.

1. Después de completar todas las secciones, haga clic en **[!UICONTROL Guardar]** o **[!UICONTROL Guardar como]** y proporcione un nombre para la configuración.

Se puede personalizar la compatibilidad con varios tipos de archivos. (Consulte [Añadir compatibilidad con formatos de archivo nativos adicionales](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)&quot; [Programación con formularios AEM](https://www.adobe.com/go/learn_lc_programming_11).)

## Cambiar la configuración predeterminada {#change-the-default-settings}

Puede cambiar el valor predeterminado de la configuración de Adobe PDF, la configuración de seguridad y la configuración de tipo de archivo que se aplica a los orígenes recién creados. El cambio de los valores predeterminados no afecta a la configuración de los orígenes existentes.

1. En la Consola de administración, haga clic en **[!UICONTROL Servicios > Generador de PDF]**.
1. En el **[!UICONTROL Configuración de Adobe PDF]**, **[!UICONTROL Configuración de tipo de archivo]** o **[!UICONTROL Configuración de seguridad]** página, haga clic en **[!UICONTROL Definir configuración predeterminada]**.
1. Seleccione la configuración predeterminada que prefiera. Una o más de las siguientes opciones de configuración están disponibles en la página Establecer configuración predeterminada :

   **[!UICONTROL Configuración de Adobe PDF]**: El valor predeterminado original es Estándar (Acrobat 6).

   **[!UICONTROL Configuración de seguridad]**: El valor predeterminado original es Sin seguridad (Acrobat 5).

   **[!UICONTROL Configuración de tipo de archivo]**: El valor predeterminado original es Estándar.

1. Haga clic en **[!UICONTROL Guardar]**.

## Eliminar una configuración de Tipo de archivo {#delete-a-file-type-setting}

Puede eliminar una configuración de tipo de archivo que ya no se utilice.

1. En la consola de administración, haga clic en **[!UICONTROL Servicios > Generador de PDF > Configuración de tipo de archivo]**.
1. Seleccione la casilla de verificación situada junto a la configuración que desea eliminar. Puede seleccionar varias fuentes. Los ajustes que no tengan una casilla de verificación junto a ellos siempre se incluyen en el Generador de PDF y no se pueden eliminar.
1. Haga clic en **[!UICONTROL Eliminar]** y, en la página Confirmación de eliminación , haga clic en **[!UICONTROL Eliminar]**.

## Configuración de imagen a PDF {#image-to-pdf-settings}

Las siguientes opciones determinan cómo se convierten los archivos de imagen en PDF. Para obtener instrucciones sobre el acceso a esta configuración, consulte [Crear o editar la configuración del tipo de archivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Extensiones de nombre de archivo:** Lista separada por comas de las extensiones de nombre de archivo que se pueden convertir.

**Pruebe el convertidor de reserva:** El Generador de PDF puede utilizar Java™ o Acrobat para convertir archivos de imagen a PDF. Cuando se selecciona esta opción y una conversión falla o alcanza el límite de tiempo de espera especificado, el Generador de PDF intenta la conversión utilizando el método alternativo. Si el método alternativo falla o alcanza el límite de tiempo de espera especificado, se escribe una excepción en el archivo de registro.

>[!NOTE]
>
>Los archivos JPEG 2000 solo se pueden convertir con Acrobat.

**Usar OCR:** Especifica si se aplica OCR (reconocimiento óptico de caracteres) al PDF. El software OCR permite buscar, corregir y copiar el texto en el PDF.

***nota **: La función PDF de OCR (PDF en el que se pueden realizar búsquedas) solo es compatible con Microsoft Windows.*

**Idioma principal de OCR:** Especifica el idioma que debe utilizar el motor OCR para identificar los caracteres.

**Estilo de salida del PDF:** Determina el tipo de PDF que se va a producir. Todos los formatos aplican OCR y reconocimiento de fuentes y páginas a las imágenes de texto y las convierten a texto normal.

**Imagen que se puede buscar:** Garantiza que el texto se pueda buscar y seleccionar. Esta opción mantiene la imagen original, la visualiza según sea necesario y coloca sobre ella una capa de texto invisible. La opción Imágenes de muestra determina si la imagen se reduce y en qué medida.

**Imagen que se puede buscar (exacta):** Garantiza que el texto se pueda buscar y seleccionar. Esta opción mantiene la imagen original y coloca sobre ella una capa de texto invisible. Recomendado para casos que requieran la máxima fidelidad a la imagen original.

**ClearScan:** Sintetiza una nueva fuente de Tipo 3 que se aproxima al original y conserva el fondo de la página mediante una copia de baja resolución.

**Descargar imágenes:** Reduce el número de píxeles en imágenes en color, escala de grises y monocromas una vez completado el OCR. Elija el grado de disminución de resolución que desee aplicar. Las opciones con mayor número reducen el muestreo, lo que produce PDF de mayor resolución.

## Configuración de exportación de Adobe PDF (solo Windows) {#adobe-pdf-export-settings-windows-only}

La configuración Tipo de archivo de exportación de la sección Configuración de exportación de Adobe PDF se utiliza para convertir un archivo de PDF a otro formato. El valor predeterminado es HTML 4.01 con hojas de estilo en cascada (CSS) 1.0 (*.htm, *.html).

Para obtener instrucciones sobre el acceso a esta configuración, consulte [Crear o editar la configuración del tipo de archivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

## Configuración de HTML a PDF {#html-to-pdf-settings}

Las siguientes opciones determinan cómo se convierten los archivos HTML en PDF. Para obtener instrucciones sobre el acceso a estas opciones, consulte [Crear o editar la configuración del tipo de archivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Pruebe el convertidor de reserva:** El Generador de PDF puede utilizar Java™ o Acrobat para convertir archivos HTML a PDF. Cuando se selecciona esta opción y una conversión falla o alcanza el límite de tiempo de espera especificado, el Generador de PDF intenta la conversión utilizando el método alternativo. Si el método alternativo falla o alcanza el límite de tiempo de espera especificado, se escribe una excepción en el archivo de registro.

**Codificación predeterminada:** Define la codificación de entrada del texto del archivo desde un menú de sistemas operativos y alfabetos. Utiliza la selección mostrada en la opción Codificación predeterminada solo si el archivo de origen del HTML no especifica un tipo de codificación.

**Forzar codificación seleccionada:** Omite cualquier codificación especificada en el archivo de origen del HTML y utiliza la selección mostrada en la opción Codificación predeterminada.

### Configuración de arañas {#spidering-settings}

*Araña* busca vínculos a otras páginas web en las páginas web. Cuando se encuentra un vínculo a otra página web, la página de destino se busca y se incluye en el documento de PDF que se genera. Active estas opciones para establecer el número de niveles que desea recuperar y convertir en PDF:

**Obtener solo niveles X:** Las arañas de Web y convierten las páginas hasta una profundidad del nivel especificado en la dirección URL de la página base. Un valor de 1 convierte solo la dirección URL suministrada.

**Obtener todo el sitio:** Convierte todo el sitio, empezando por la dirección URL proporcionada.

**Manténgase En El Mismo Camino:** Los vínculos que dirigen a páginas que no están en la misma ruta relativa que la dirección URL base no se convierten durante la araña.

**Permanezca En El Mismo Servidor:** Los vínculos que dirigen a páginas en diferentes servidores no se convierten durante la araña. Solo se convierten los vínculos que apuntan al mismo servidor que la dirección URL especificada.

### Configuración de conversión de página {#page-conversion-settings}

Active estas opciones para especificar cómo se convierten las páginas del HTML. En función del tamaño de la página, los valores de ancho, alto y margen se ajustan en consecuencia.

**Tamaño de página:** Elija personalizada y especifique la anchura y la altura, o bien seleccione dimensiones predefinidas.

**Orientación:** Seleccione vertical u horizontal para el documento PDF convertido.

**Márgenes:** Especifica los márgenes (Superior, Inferior, Izquierda y Derecha) en el documento de PDF generado.

**Agregar Marcadores Al PDF:** Agrega marcadores al documento del PDF.

**Habilitar PDF etiquetado:** Incrusta etiquetas en el documento de PDF.

**Definir la configuración de vista inicial:** Permite configurar opciones de documento, opciones de ventana y opciones de interfaz de usuario. Esta configuración determina cómo se muestra inicialmente el contenido.

### Opciones de documento {#document-options}

Active estas opciones para especificar cómo mostrar contenido, cómo mostrar páginas en el documento del PDF y cómo especificar el nivel de ampliación:

**Mostrar:** Seleccione los paneles que desea abrir en Acrobat cuando se abra el documento del PDF.

**Diseño de página:** Seleccione el tipo de presentación de página para el documento del PDF.

**Ampliación:** Elija la ampliación preestablecida para la vista inicial del documento del PDF o seleccione un valor personalizado. Si elige una configuración predeterminada, se usará la ampliación predeterminada de Acrobat.

**Abrir a número de página:** Especifique el número de página al que se abre el PDF.

### Opciones de ventana {#window-options}

Active estas opciones para especificar el tamaño y la visualización de la ventana.

**Cambiar El Tamaño De La Ventana A La Página Inicial:** Cambia el tamaño de la ventana de Acrobat al tamaño de la página inicial.

**Ventana central en pantalla:** Abre la ventana en el centro de la pantalla.

**Abrir En Modo De Pantalla Completa:** Abre la ventana en modo de pantalla completa.

**Mostrar:** Muestra el título o el nombre de archivo del documento en la ventana.

### Opciones de interfaz de usuario {#user-interface-options}

Active estas opciones para especificar el aspecto de la ventana:

**Ocultar barra de menús:** Oculta la barra de menús del documento del PDF.

**Ocultar barras de herramientas:** Oculta las barras de herramientas del documento PDF.

**Ocultar controles de ventana:** Oculta los controles de ventana del documento del PDF.

## Flash de vídeos a la configuración de PDF {#flash-videos-to-pdf-settings}

El Generador de PDF admite la capacidad de enviar un vídeo para el Flash de Adobe (SWF o archivo FLV) y crear un archivo PDF con un vídeo para el Flash de Adobe incrustado en él. Esta conversión no requiere que el Flash Player de Adobe esté instalado en el servidor de formularios. Para obtener instrucciones sobre el acceso a esta opción, consulte [Crear o editar la configuración del tipo de archivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Extensiones de nombre de archivo:** Lista separada por comas de las extensiones de nombre de archivo que se pueden convertir.

## Configuración de XPS a PDF {#xps-to-pdf-settings}

La especificación de papel XML (XPS) se utiliza en la máquina de impresión de Windows. Este es un formato de Microsoft y se puede crear desde cualquier aplicación de Microsoft Office. AEM formularios permite convertir el PDF de archivos XPS.

**Extensiones de nombre de archivo:** Lista separada por comas de todas las extensiones de nombre de archivo XPS que se pueden convertir. Actualmente hay un formato: .xps.

## Configuración del optimizador de PDF {#pdf-optimizer-settings}

El Generador de PDF admite la capacidad de reducir el tamaño de los archivos PDF. Tanto si utiliza todos estos ajustes como si solo unos pocos dependen de cómo pretenda utilizar los archivos y de las propiedades esenciales que debe tener un archivo. En la mayoría de los casos, la configuración predeterminada es adecuada para lograr la máxima eficacia: ahorra espacio al eliminar fuentes incrustadas, comprimir imágenes y eliminar elementos de los archivos que ya no son necesarios.

>[!NOTE]
>
>Al optimizar un documento firmado digitalmente, se eliminan e invalidan las firmas digitales.

Para obtener instrucciones sobre el acceso a esta configuración, consulte [Crear o editar la configuración del tipo de archivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Versión del PDF de Target:** Especifica la versión de Acrobat con la que es compatible el PDF.

### Fuentes {#fonts}

1. Select **Fuentes.**
1. Seleccione una de las siguientes opciones:

   **Desincrustar todas las fuentes:** Desincrusta todas las fuentes incrustadas.

   **No desincruste ninguna fuente:** No desincrusta ninguna fuente.

   **Desincruste algunas fuentes:** Desincrusta solo las fuentes especificadas. Siga estos pasos para especificar las fuentes que desea desincrustar:

   * Si es necesario, seleccione un directorio de fuentes diferente del **Fuente** menú desplegable. Este menú desplegable enumera los directorios de fuentes especificados en **Inicio > Configuración > Sistema principal > Configuraciones principales**.
   * Seleccione una o varias fuentes de la lista **Fuentes disponibles** haga clic en **Agregar**. Estas fuentes se añaden al **Fuentes que se van a desincrustar** lista.
   * Si desea desincrustar algunas fuentes que no existen en el servidor de formularios, introduzca los nombres de esas fuentes en la **Añadir fuentes a desincrustar** en la ventana Haga clic en **Agregar**.

   >[!NOTE]
   >
   >*Si desea desincrustar algunas fuentes cuyos subconjuntos están incrustados en el documento, anteponga el nombre de la fuente con el signo +. Por ejemplo, &quot;+Helvetica&quot;.*

1. Si desea incrustar solo los subconjuntos en uso de las fuentes incrustadas, seleccione **Subconjunto de todas las fuentes incrustadas**.

   >[!NOTE]
   >
   >*Si utiliza esta opción en combinación con **Desincrustar algunas fuentes**, fuentes en la **Añadir fuentes a desincrustar**la lista sigue sin estar incrustada.*

   >[!NOTE]
   >
   >*El subconjunto de fuentes es la técnica de incrustar solo una parte de una fuente. Un subconjunto de fuentes contiene solo los caracteres utilizados en el documento.*

### Transparencia {#transparency}

Si el documento del PDF incluye ilustraciones que contienen transparencia, puede utilizar la configuración de PDF Optimizer para aplanar la transparencia y reducir el tamaño del archivo.

>[!NOTE]
>
>Si se selecciona Acrobat 4.0 y versiones posteriores como versión del PDF de Target, se acoplan todos los objetos transparentes. Para otras versiones de PDF de Target, se admite la transparencia y se puede configurar la transparencia.

Select **Transparencia** para configurar los ajustes de transparencia al optimizar los documentos de PDF.

**Nivel de transparencia** Especifica la cantidad de información vectorial que se va a conservar. Los ajustes más altos conservan más objetos vectoriales, mientras que los más bajos rasterizan más objetos vectoriales; la configuración intermedia conserva las áreas simples en forma vectorial y rasteriza las complejas. Seleccione la configuración más baja para rasterizar todas las ilustraciones.

>[!NOTE]
>
>La cantidad de rasterización que se produce depende de la complejidad de la página y de los tipos de objetos superpuestos.

**Arte de líneas y texto** Resolución a la que se rasterizan todos los objetos, incluidas las imágenes, las ilustraciones vectoriales, el texto y los degradados. Los valores admitidos son de 1 píxeles por pulgada (ppi) a 9600 ppi.

>[!NOTE]
>
>La resolución de Arte de Línea y Texto debe establecerse generalmente en 600-1200 ppi para proporcionar rasterización de alta calidad, especialmente en serif o de pequeño tamaño de punto.

**Degradación y mallas** Resolución a la que se rasterizan el degradado y las redes. Los valores admitidos son de 1 ppi a 1200 ppi.

>[!NOTE]
>
>La resolución de degradado y de malla debería establecerse generalmente en 150-300 ppi porque la calidad de los degradados, las sombras y las plumas no mejora con resoluciones más altas, pero el tiempo de impresión y el tamaño del archivo aumentan.

**Convertir todo el texto en contornos** Convierte todos los objetos de tipo (tipo de punto, tipo de área y tipo de ruta) en contornos y descarta toda la información de glifo de tipo en páginas que contienen transparencia. Esta opción garantiza que la anchura del texto sea constante durante el acoplamiento. Tenga en cuenta que si se habilita esta opción, las fuentes pequeñas aparecerán ligeramente más gruesas cuando se vean en Acrobat o se impriman en impresoras de escritorio de baja resolución. No afecta a la calidad del tipo impreso en impresoras de alta resolución o en impresoras de imágenes.

**Convertir todos los trazos en contornos** Convierte todos los trazos en rutas rellenas simples en páginas que contengan transparencia. Esta opción garantiza que la anchura de los trazos sea constante durante el aplanamiento. Tenga en cuenta que, al habilitar esta opción, los trazos finos aparecen un poco más gruesos y pueden degradar el rendimiento del acoplamiento.

**Recortar regiones complejas** Garantiza que los límites entre la ilustración vectorial y la ilustración rasterizada se encuentren a lo largo de las rutas de los objetos. Esta opción reduce los artefactos de vinculación que se producen cuando forma parte de un registro

<!--
NOTE to WRITER: Unfinished sentence above.
-->

>[!NOTE]
>
>Algunos controladores de impresión procesan el arte de trama y vectorial de forma diferente, lo que a veces resulta en la unión de colores. Es posible que pueda minimizar los problemas de unión desactivando algunos ajustes específicos de gestión de color del controlador de impresión. Estos ajustes varían con cada impresora, por lo que consulte la documentación que viene con ella para obtener más información.

Mantener sobreimpresión: Combina el color de la ilustración transparente con el color de fondo para crear un efecto de sobreimpresión.

La siguiente tabla muestra los tipos comunes de impresoras y su resolución medida en ppp, su regla de pantalla predeterminada medida en líneas por pulgada (lpi) y una resolución de remuestreo para imágenes medidas en píxeles por pulgada (ppi). Por ejemplo, si imprimiera en una impresora láser de 600 ppp, introduciría 170 para la resolución en la que se remuestrearán las imágenes.

**Imágenes** Seleccione Imágenes para especificar opciones de compresión y remuestreo para imágenes en color, escala de grises y monocromas. Es posible que desee experimentar con estas opciones para encontrar un equilibrio adecuado entre el tamaño del archivo y la calidad de la imagen. La configuración de resolución para imágenes en color y escala de grises debe ser de 1,5 a 2 veces la pantalla de línea en la que se imprimirá el archivo. La resolución de las imágenes monocromas debe ser la misma que la del dispositivo de salida, pero tenga en cuenta que al guardar una imagen monocromática con una resolución superior a 1500 ppp, se aumenta el tamaño del archivo sin mejorar notablemente la calidad de la imagen. Las imágenes que se amplificarán, como los mapas, pueden requerir resoluciones más altas.

>[!NOTE]
>
>El remuestreo de imágenes monocromas puede tener resultados de visualización inesperados, como que no se muestre ninguna imagen. Si esto sucede, desactive el remuestreo y vuelva a convertir el archivo. Es muy probable que este problema ocurra con el submuestreo, y menos probable con la disminución de resolución bicúbica.

<table>
 <tbody>
  <tr>
   <th><p><strong>Resolución de la impresora</strong></p> </th>
   <th><p><strong>Pantalla de línea predeterminada</strong></p> </th>
   <th><p><strong>Resolución de imágenes</strong></p> </th>
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

#### Descartar objetos {#discard-objects}

* Select **Descartar objetos** para especificar los objetos que se van a quitar del PDF y para optimizar las líneas curvas en dibujos CAD.
* **Descartar Todas Las Acciones De Envío, Importación Y Restablecimiento De Formularios**: Desactiva todas las acciones relacionadas con el envío o importación de datos de formulario y restablece los campos de formulario. Esta opción conserva los objetos de formulario a los que están vinculadas las acciones.
* **Descartar todas las acciones de JavaScript**: Quita del PDF cualquier acción que utilice JavaScript.
* **Descartar miniaturas de página incrustadas**: Quita las miniaturas de página incrustadas. Esta opción es útil para documentos grandes, que pueden tardar mucho tiempo en dibujar miniaturas de página después de hacer clic en el botón Páginas .
* **Convertir líneas suaves en curvas**: Reduce el número de puntos de control utilizados para crear curvas en dibujos CAD, lo que da como resultado archivos de PDF más pequeños y un procesamiento en pantalla más rápido.
* **Descartar configuración de impresión incrustada**: Quita la configuración de impresión incrustada, como el escalado de página y el modo dúplex, del documento.
* **Descartar marcadores**: Quita todos los marcadores del documento.
* **Acoplar campos de formulario**: Hace que los campos de formulario no se puedan utilizar sin ningún cambio en su aspecto. Los datos del formulario se combinan con la página para convertirse en contenido de página.
* **Descartar todas las imágenes alternativas**: Elimina todas las versiones de una imagen, excepto la versión destinada a la visualización en pantalla. Algunos PDF incluyen varias versiones de la misma imagen para diferentes propósitos, como la visualización en pantalla de baja resolución y la impresión de alta resolución.
* **Descartar etiquetas de documento**: Quita las etiquetas del documento, que también elimina la accesibilidad y las capacidades de reflujo del texto.
* **Detectar Y Combinar Fragmentos De Imagen**: Busca imágenes o máscaras fragmentadas en sectores finos y trata de fusionar los sectores en una sola imagen o máscara.
* **Descartar índice de búsqueda incrustado**: Elimina los índices de búsqueda incrustados, lo que reduce el tamaño del archivo.

#### Descartar datos de usuario {#discard-user-data}

Select **Descartar datos de usuario** para eliminar cualquier información personal que no desee distribuir o compartir con otros usuarios.

* **Descartar Todos Los Comentarios, Forms Y Multimedia**: Quita todos los comentarios, formularios, campos de formulario y contenido multimedia del PDF.
* **Descartar todos los datos de objeto**: Quita todos los objetos del PDF.
* **Descartar referencias cruzadas externas**: Quita los vínculos a otros documentos. Los vínculos que conducen a otras ubicaciones dentro del PDF no se eliminan.
* **Descartar contenido de capa oculto y acoplar capas visibles**: Reduce el tamaño del archivo. El documento optimizado se parece al PDF original, pero no contiene información de capa.
* **Descartar información y metadatos del documento**: Quita la información del diccionario de información del documento y todos los flujos de metadatos. (Utilice el comando Guardar como para restaurar los flujos de metadatos a una copia del PDF).
* **Descartar archivos adjuntos**: Quita todos los archivos adjuntos, incluidos los archivos adjuntos agregados al PDF como comentarios. (PDF Optimizer no optimiza los archivos adjuntos).
* **Descartar Datos Privados De Otras Aplicaciones**: Quita información de un documento de PDF que solo sea útil para la aplicación que creó el documento. Esta configuración no afecta a la funcionalidad del PDF, pero disminuye el tamaño del archivo.

### Limpiar {#clean-up}

Select **Limpiar** para eliminar elementos innecesarios del documento.
Estos artículos incluyen elementos que están obsoletos o son innecesarios para el uso previsto del documento. La eliminación de ciertos elementos puede afectar gravemente a la funcionalidad del PDF. De forma predeterminada, solo se seleccionan los elementos que no afectan a la funcionalidad. Si no está seguro de las implicaciones de eliminar otras opciones, utilice las selecciones predeterminadas.

**Compresión**

Seleccione una de las siguientes opciones de compresión Flate en el menú desplegable:

* Comprimir todo el archivo
* Comprimir la estructura del documento
* Eliminar compresión
* Dejar sin tocar la compresión

**Utilice Flate Para Codificar Flujos Que No Estén Codificados**: Aplica compresión Flate a todas las secuencias que no están codificadas.

**Descartar marcadores no válidos**: Elimina los marcadores que apuntan a páginas del documento que se eliminan.

**Descartar destinos con nombre sin referencia**: Elimina los destinos con nombre a los que no se hace referencia internamente desde el documento del PDF. Esta opción no comprueba los vínculos de otros archivos PDF o sitios web.

**Optimizar El PDF Para Una Vista Web Rápida**: Reestructura un documento de PDF para la descarga de página en tiempo (servicio de bytes) desde servidores web.

**En Transmisiones Que Utilizan Codificación LZW, Utilice Flate En Su Lugar**: Aplica compresión Flate a todas las emisiones de contenido e imágenes que utilizan codificación LZW.

**Descartar vínculos no válidos**: Quita los vínculos que conducen a destinos no válidos.

**Optimizar el contenido de la página**: Convierte todos los caracteres de fin de línea en caracteres de espacio, lo que mejora la compresión Flate.

## Configuración de Microsoft Excel (solo Windows) {#microsoft-excel-settings-windows-only}

Estas opciones determinan cómo se convierten los archivos de Excel de Microsoft. Para obtener instrucciones sobre el acceso a estas opciones, consulte [Crear o editar la configuración del tipo de archivo](#create-or-edit-file-type-settings).

**Pruebe OpenOffice As Fallback Converter**: Cuando se selecciona esta opción y una conversión con Microsoft Excel falla o alcanza el límite de tiempo de espera especificado, el Generador de PDF intenta la conversión utilizando OpenOffice. Si la conversión mediante OpenOffice falla o alcanza el límite de tiempo de espera especificado, se escribe una excepción en el archivo de registro.

**Extensiones de nombre de archivo**: Especifica las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan para esta aplicación. El valor predeterminado es `xls,xlsx`. No incluya un punto antes o un espacio entre las extensiones.

**Crear archivo compatible con PDF/A-1a**: Fuerza el uso de la configuración de Adobe PDF del RGB PDF/A-1b:2005.

**Agregar Marcadores A Adobe PDF**: Convierte los nombres de las hojas de cálculo de Excel en marcadores. Esta opción está seleccionada de forma predeterminada.

**Ajustar hoja de cálculo a una sola página**: Reduce el tamaño del texto para que quepa en la hoja de cálculo de una sola página.

**Convertir todo el libro**: Convierte todas las hojas de cálculo del archivo de Excel. Si no se selecciona esta opción, solo se convierte la página actual.

**Ejecutar macros automáticamente**: Ejecuta cualquier macro del documento de Excel (como una macro que inserta la hora actual) antes de convertir el documento.

**Convertir información de documento**: Agrega propiedades del documento PDF basadas en la información del documento en el archivo de origen. Esto incluye información como título del documento, autor, asunto y palabras clave.

**Añadir Vínculos A Adobe PDF**: Convierte los hipervínculos del archivo de origen en hipervínculos del documento de PDF.

**Adjuntar archivo de origen a Adobe PDF**: Cuando se selecciona esta opción, la hoja de cálculo original de Excel se inserta como archivo adjunto dentro del documento de PDF generado.

**Habilitar Accesibilidad Y Reflow Con Adobe PDF Etiquetado**: Incrusta etiquetas dentro del documento del PDF para habilitar la accesibilidad y el reflujo.

**Lista De Los Anuncios De Excel Que Se Van A Cargar**: De forma predeterminada (por motivos de seguridad), no se ejecutan complementos de Excel cuando un archivo de Excel se convierte en PDF. Para permitir que ciertos complementos de Excel se ejecuten durante la conversión, proporcione una lista separada por comas de los nombres de los complementos.

**Lista De Hojas De Cálculo Que Convertir**: Cuando este cuadro está vacío, todas las hojas de cálculo de Excel se incluyen en el PDF generado. Para convertir selectivamente un subconjunto de hojas de cálculo, proporcione una lista de nombres de hojas de cálculo separados por coma.

## Configuración de Microsoft PowerPoint (solo Windows) {#microsoft-powerpoint-settings-windows-only}

Estas opciones determinan cómo se convierten los archivos de Microsoft PowerPoint. Para obtener instrucciones sobre el acceso a estas opciones, consulte [Crear o editar la configuración del tipo de archivo](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**[!UICONTROL Pruebe OpenOffice As Fallback Converter]**: Cuando se selecciona esta opción y una conversión que utiliza Microsoft PowerPoint falla o alcanza el límite de tiempo de espera especificado, PDF Generator intenta la conversión utilizando OpenOffice. Si la conversión mediante OpenOffice falla o alcanza el límite de tiempo de espera especificado, se escribe una excepción en el archivo de registro.

**[!UICONTROL Extensiones de nombre de archivo]**: Especifica las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan para esta aplicación. El valor predeterminado es ppt,pptx. No incluya un punto antes o un espacio entre las extensiones.

**[!UICONTROL Convertir información de documento]**: Agrega información del documento desde el cuadro de diálogo Propiedades del archivo de origen, incluido título, asunto, autor, palabras clave, administrador, empresa, categoría y comentarios. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Agregar Marcadores A Adobe PDF]**: Convierte los títulos de PowerPoint en marcadores. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Adjuntar archivo de origen a Adobe PDF]**: Agrega el archivo de origen al archivo de PDF como archivo adjunto. Esta opción está desactivada de forma predeterminada.

**[!UICONTROL Habilitar Accesibilidad Y Reflow Con Adobe PDF Etiquetado]**: Incrusta etiquetas en el archivo PDF. Esta opción está desactivada de forma predeterminada.

**[!UICONTROL Convertir Multimedia En Multimedia PDF]**: Convierte el contenido multimedia en PDF multimedia, siempre que sea posible. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Convertir notas del altavoz]**: Convierte las notas del orador en PDF.

**[!UICONTROL Ejecutar macros automáticamente]**: Ejecuta cualquier macro del documento de PowerPoint (como una macro que inserta la hora actual) antes de convertir el documento.

**[!UICONTROL Diseño del PDF basado en la configuración de la impresora de PowerPoint]**: Utiliza la configuración de la impresora de PowerPoint para presentar el documento del PDF.

**[!UICONTROL Añadir Vínculos A Adobe PDF]**: Conserva los vínculos existentes cuando se convierte el archivo. Por lo general, el aspecto de los vínculos no cambia. Los vínculos solo se pueden crear si la opción Enable Accessibility también está seleccionada. Esta opción está desactivada de forma predeterminada.

**[!UICONTROL Guardar Transiciones De Diapositivas En Adobe PDF]**: Convierte las transiciones de diapositivas. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Guardar Animaciones En Adobe PDF]**: Guarda las animaciones convertidas en el archivo PDF.

**[!UICONTROL Convertir diapositivas ocultas en páginas PDF]**: Convierte las diapositivas ocultas.

**[!UICONTROL Crear archivo compatible con PDF/A-1a]**: Fuerza el uso de la configuración de Adobe PDF del RGB PDF/A-1b:2005. Algunas funciones de PowerPoint no se convierten cuando se produce un archivo PDF. Si una transición de PowerPoint no tiene una transición equivalente en Acrobat, se sustituye una transición similar. Si hay varios efectos de animación en la misma diapositiva, se utiliza un solo efecto. Se convierten las transiciones de página y los volantes de viñetas.

## Configuración del proyecto de Microsoft (solo Windows) {#microsoft-project-settings-windows-only}

Estas opciones determinan cómo se convierten los archivos de proyecto de Microsoft. Para obtener instrucciones sobre el acceso a estas opciones, consulte [Crear o editar la configuración del tipo de archivo](#create-or-edit-file-type-settings).

1. **[!UICONTROL Extensiones de nombre de archivo:]** Especifica las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan para esta aplicación. El valor predeterminado es `mpp`. No incluya un punto antes o un espacio entre las extensiones.

1. **[!UICONTROL Convertir información de documento]**: Agrega información del documento desde el cuadro de diálogo Propiedades del archivo de origen, incluido título, asunto, autor, palabras clave, administrador, empresa, categoría y comentarios. Esta opción está seleccionada de forma predeterminada.
1. **[!UICONTROL Adjuntar archivo de origen a Adobe PDF]**: Agrega el archivo de origen al archivo de PDF como archivo adjunto.
1. **[!UICONTROL Crear archivo compatible con PDF/A-1a]**: Fuerza el uso de la configuración de Adobe PDF del RGB PDF/A-1b:2005.
1. **[!UICONTROL Ejecutar macros automáticamente]**: Ejecuta las macros del documento Proyecto de Microsoft (como una macro que inserta la hora actual) antes de convertir el documento.

## Configuración de Microsoft Word (solo Windows) {#microsoft-word-settings-windows-only}

Estas opciones determinan cómo se convierten los archivos de Microsoft Word. Para obtener instrucciones sobre el acceso a estas opciones, consulte [Crear o editar la configuración del tipo de archivo](#create-or-edit-file-type-settings).

**[!UICONTROL Pruebe OpenOffice As Fallback Converter]**: Cuando se selecciona esta opción y una conversión con Microsoft Word falla o alcanza el límite de tiempo de espera especificado, el Generador de PDF intenta la conversión utilizando OpenOffice. Si la conversión mediante OpenOffice falla o alcanza el límite de tiempo de espera especificado, se escribe una excepción en el archivo de registro.

**[!UICONTROL Extensiones de nombre de archivo]**: Especifica las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan para esta aplicación. El valor predeterminado es `doc,docx,rtf,txt`. No incluya un punto antes o un espacio entre las extensiones.

**[!UICONTROL Convertir información de documento]**: Agrega información del documento desde el cuadro de diálogo Propiedades del archivo de origen, incluido título, asunto, autor, palabras clave, administrador, empresa, categoría y comentarios. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Agregar Marcadores A Adobe PDF]**: Convierte los encabezados en marcadores. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Adjuntar archivo de origen a Adobe PDF]**: Agrega el archivo de origen al archivo de PDF como archivo adjunto.

**[!UICONTROL Convertir Referencias Cruzadas Y Tabla De Contenido En Vínculos]**: Convierte todas las referencias cruzadas y entradas de tabla de contenido en vínculos. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Habilitar Accesibilidad Y Reflow Con Adobe PDF Etiquetado]**: Incrusta etiquetas en el archivo PDF. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Crear archivo compatible con PDF/A-1a]**: Si se selecciona, fuerza el uso de la configuración de Adobe PDF del RGB PDF/A-1b:2005.

**[!UICONTROL Ejecutar macros automáticamente]**: Ejecuta cualquier macro del documento de Word (como una macro que inserta la hora actual) antes de convertir el documento.

**[!UICONTROL Conservar El Marcado De Documentos En Adobe PDF]**: Convierte el marcado del documento de Word en anotaciones del archivo PDF.

**[!UICONTROL Añadir Vínculos A Adobe PDF]**: Convierte los hipervínculos del archivo de origen en hipervínculos del documento de PDF.

**[!UICONTROL Convertir vínculos de notas al pie y notas al final]**: Crea vínculos desde las citas de notas al pie y notas al final a notas en el documento del PDF.

**[!UICONTROL Convertir los comentarios mostrados en notas en Adobe PDF]**: Convierte los comentarios del documento de Word en notas de texto del documento del PDF.

**[!UICONTROL Habilitar etiquetado avanzado]**: Añade etiquetas avanzadas para mejorar la accesibilidad.

**[!UICONTROL Convertir todos los estilos en marcadores]**: Convierte todos los estilos del documento de Word en marcadores en el documento PDF.

**[!UICONTROL Convertir estilos especificados en marcadores]**: Convierte los estilos que define en la variable **[!UICONTROL Estilos con niveles]** a marcadores en el documento PDF.

**[!UICONTROL Estilos con niveles]**: Especifica qué estilos del documento de Word se convierten en marcadores en el documento de PDF. También especifica el nivel de los marcadores. Para utilizar esta función, anule la selección de la opción **[!UICONTROL Convertir todos los estilos en marcadores]** y especifique los nombres de estilo en el siguiente formato:

**styleName1=level1[,styleName2=level2...]**

Si un nombre de estilo de Microsoft Word incluye una coma (,) o un signo igual (=), preceda los caracteres especiales con el carácter de escape (&quot;\_). Por ejemplo, especifique un estilo denominado &quot;Encabezado, 1&quot; como Encabezado\, 1.

**Codificación de Acrobat PDFMaker:** Especifica el tipo de codificación de los archivos de texto sin formato de entrada al PDFMaker de Acrobat. Por ejemplo, si está utilizando un archivo codificado UTF-8, seleccione UTF-8 para obtener los mejores resultados.

## Configuración de Microsoft Visio (solo Windows) {#visio}

**Convertir información de documento**: Agrega información del documento desde el cuadro de diálogo Propiedades del archivo de origen, incluido título, asunto, autor, palabras clave, administrador, empresa, categoría y comentarios. Esta opción está seleccionada de forma predeterminada. Esta opción está activada de forma predeterminada.

**Añadir Vínculos A Adobe PDF**: Conserva todos los vínculos. Esta opción está seleccionada de forma predeterminada.

**Agregar Marcadores A Adobe PDF**: Convierte los encabezados en marcadores. Esta opción está seleccionada de forma predeterminada.

**Adjuntar archivo de origen a Adobe PDF**: Agrega el archivo de origen al archivo de PDF como archivo adjunto.

**Acoplar Siempre Las Capas En Adobe PDF**: Acopla todas las capas de Visio.

**Convertir todas las páginas**: Convierte todas las páginas del archivo de Visio.

**Abrir El Panel Capas Cuando Se Ve En Adobe Acrobat**: Si las capas de Visio no están acopladas, abre una ventana en la que puede especificar las capas que se conservan en el archivo PDF al abrirlas con Acrobat. Esta opción está seleccionada de forma predeterminada.

**Crear archivo PDF/compatible con A-1b**: Fuerza el uso del PDF de configuración de Adobe PDF/A-1b:2005 (RGB).

**Convertir comentarios en comentarios de Adobe PDF**: Convierte las notas de Visio en comentarios de PDF.

## Configuración de Microsoft Publisher (solo Windows) {#microsoft-publisher-settings-windows-only}

Estas opciones determinan cómo se convierten los archivos de Microsoft Publisher. Para obtener instrucciones sobre el acceso a estas opciones, consulte [Crear o editar la configuración del tipo de archivo](#create-or-edit-file-type-settings).

**[!UICONTROL Extensiones de nombre de archivo]**: Especifica las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan para esta aplicación. El valor predeterminado es `pub`. No incluya un punto antes o un espacio entre las extensiones.

## Configuración de AutoCAD (solo Windows) {#autocad-settings-windows-only}

Estas opciones determinan cómo se convierten los archivos de AutoCAD. Para obtener instrucciones sobre el acceso a estas opciones, consulte [Crear o editar la configuración del tipo de archivo](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**[!UICONTROL Extensiones de nombre de archivo]**: Especifica las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan para esta aplicación. El valor predeterminado es `dwg`. No incluya un punto antes o un espacio entre las extensiones.

**[!UICONTROL Convertir información de documento]**: Agrega información del documento desde el cuadro de diálogo Propiedades del archivo de origen, incluido título, asunto, autor, palabras clave, administrador, empresa, categoría y comentarios. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Agregar Marcadores A Adobe PDF]**: Convierte los encabezados en marcadores.

**[!UICONTROL Acoplar Siempre Las Capas En Adobe PDF]**: Aplana todas las capas de AutoCAD.

**[!UICONTROL Abrir El Panel Capas Cuando Se Ve En Adobe Acrobat]**: Muestra la estructura de las capas cuando se abre el PDF en Acrobat.

**[!UICONTROL Convertir todas las presentaciones]**: Incluye todos los diseños del PDF.

**[!UICONTROL Convertir espacio de modelo a 3D]**: Cuando se selecciona, el diseño de espacio del modelo se convierte en una anotación 3D en el PDF.

**[!UICONTROL Añadir Vínculos A Adobe PDF]**: Si se selecciona, conserva todos los vínculos.

**[!UICONTROL Adjuntar archivo de origen a Adobe PDF]**: Agrega el archivo de origen al archivo de PDF como archivo adjunto.

**[!UICONTROL Crear archivo PDF/compatible con A-1b]**: Fuerza el uso de la configuración de Adobe PDF PDF/A-1b.

**[!UICONTROL Convertir todas las capas]**: De forma predeterminada, Generador de PDF convierte sólo la capa predeterminada de los archivos de AutoCAD a PDF en lugar de todas las capas dentro del archivo. Seleccione esta opción para convertir todas las capas del archivo.

**[!UICONTROL Incrustar información de escala]**: Conserva la información de la escala de dibujo.

**[!UICONTROL Convertir diseño actual]**: Solo incluye el diseño actual en el PDF.

**[!UICONTROL Lista De Diseños De AutoCAD Que Convertir]**: Un dibujo de AutoCAD puede tener varios diseños. Cuando este cuadro está vacío, todos los diseños del dibujo de AutoCAD se incluyen en el documento de PDF generado. Para convertir selectivamente un subconjunto de los diseños, proporcione una lista de nombres de diseño separados por coma.

## Configuración de OpenOffice {#openoffice-settings}

Estas opciones determinan cómo se convierten los archivos de OpenOffice. Para obtener instrucciones sobre el acceso a estas opciones, consulte [Crear o editar la configuración del tipo de archivo](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Pruebe PDFMaker As Fallback Converter**: Cuando se selecciona esta opción y una conversión mediante OpenOffice falla o alcanza el límite de tiempo de espera especificado, el Generador de PDF intenta la conversión utilizando PDFMaker. Si la conversión mediante PDFMaker falla o alcanza el límite de tiempo de espera especificado, se escribe una excepción en el archivo de registro.

**Extensiones de nombre de archivo**: Especifique las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan para esta aplicación. El valor predeterminado es `odt,odp,ods,odg,odf,sxw,sxi,sxd`. No incluya un punto antes o un espacio entre las extensiones.

**Rango**: Convierta todas las páginas o especifique determinadas páginas o un intervalo de páginas. Si no se define un intervalo de páginas, se convierten todas las páginas. Para exportar un rango de páginas, utilice el formato 3-6. Para exportar páginas individuales, utilice el formato 7;9;11. Puede exportar una combinación de intervalos de páginas y páginas únicas utilizando un formato como 3-6;8;10;12.

**Orientación de la página**: Para archivos de texto sin formato solamente, seleccione vertical u horizontal para el documento PDF convertido.

**Imágenes**: Configure cómo se convierten las imágenes. Las imágenes de EPS con vistas previas incrustadas se exportan únicamente como vistas previas. Las imágenes de EPS sin vistas previas incrustadas se exportan como marcadores de posición vacíos. Con la compresión sin pérdidas de imágenes, se conservan todos los píxeles. Con la compresión JPEG de las imágenes y un nivel de alta calidad, se conservan casi todos los píxeles. Con un nivel de baja calidad, se pierden algunos píxeles y se introducen artefactos, pero se reduce el tamaño de los archivos.

**General**: Active las opciones para convertir un PDF etiquetado o para exportar notas de documento de Writer y FormCalc, efectos de transición de Impresión de diapositivas o páginas en blanco al PDF. Cuando se exportan etiquetas, el tamaño del archivo puede aumentar en grandes cantidades. Algunas etiquetas que se exportan son tablas de contenido, hipervínculos y controles.

También puede especificar cómo se envían los formularios. Las opciones son XML, FDF, PDF o HTML. Esta configuración anula la propiedad URL del control que haya establecido en el documento. Solo se puede seleccionar una configuración común para el documento PDF:

* PDF (envía todo el documento)
* FDF (envía el contenido del control)
* HTML
* XML

**PDF etiquetado**: Permite la creación de un PDF etiquetado a partir de documentos de OpenOffice. El PDF etiquetado contiene información sobre la estructura del contenido del documento. Esto puede resultar útil al mostrar el documento en dispositivos con pantallas diferentes y al utilizar software de lector de pantalla. También ayuda al software de accesibilidad a realizar diversas operaciones útiles con el documento del PDF, como leer en voz alta el contenido del documento del PDF.

**Exportar notas**: Convierte las notas de los documentos de OpenOffice en notas del documento de PDF generado.

**Usar efectos de transición**: Convierte los efectos de transición de diapositivas en presentaciones de OpenOffice a los correspondientes efectos de transición de PDF.

**Enviar Forms en formato**: Crea un formulario de PDF que el usuario puede rellenar e imprimir en el documento de PDF.

**Exportar páginas en blanco insertadas automáticamente**: Cuando se selecciona esta opción, las páginas en blanco insertadas automáticamente se incluyen en el documento del PDF generado. Esto resulta útil si va a imprimir un documento PDF a doble cara. Por ejemplo, se puede configurar un libro para que la primera página del capítulo siempre comience en una página impar. Si el capítulo anterior termina en una página impar, OpenOffice inserta una página par en blanco. Esta opción controla si se incluye esa página par en el PDF generado.

## Otra configuración de aplicación (solo Windows) {#other-applications-settings-windows-only}

No puede cambiar la configuración de otras aplicaciones a través de la consola de administración; muestran las extensiones de nombre de archivo para los tipos de archivo compatibles. Para obtener instrucciones sobre el acceso a esta configuración, consulte [Crear o editar la configuración del tipo de archivo](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html).

* Corel WordPerfect: `wpd`
* PageMaker de Adobe: `pmd, pm6, p65, pm`
* Adobe FrameMaker: `fm`
* Adobe Photoshop: `psd`

Puede que sea necesario personalizar la compatibilidad con estos tipos de archivos. Para obtener más información, consulte &quot;Añadir compatibilidad con formatos de archivo nativos adicionales&quot; en [Programación con formularios AEM](https://www.adobe.com/go/learn_aemforms_programming_62).

Para obtener ayuda sobre la configuración de una impresora de red PDFG, consulte [Configuración de una impresora de red PDFG (solo Windows)](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md).
