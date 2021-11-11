---
title: Configuración general de Dynamic Media
description: Obtenga información sobre cómo administrar la configuración general en Dynamic Media. Aquí puede establecer el nombre del servidor de publicación y el nombre del servidor de origen y establecer una opción de sobrescritura de imagen. También hay opciones predeterminadas para la carga de imágenes máscaras de enfoque y opciones de carga para procesar archivos PostScript, Adobe Photoshop, PDF y Adobe Illustrator.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
hide: true
hidefromtoc: true
exl-id: null
source-git-commit: bbced918e67c64c0bf2f5a3de8cbcb9063fff669
workflow-type: tm+mt
source-wordcount: '2200'
ht-degree: 5%

---


# Configuración general de Dynamic Media

>[!IMPORTANT]
>
>La configuración general de Dynamic Media solo está disponible si:
>
>* Está ejecutando Dynamic Media en modo Scene7.
>* Tiene un *existente* **[!UICONTROL Configuración de Dynamic Media]** (en **[!UICONTROL Cloud Services]**) en Adobe Experience Manager 6.5 o en Experience Manager as a Cloud Service.
>* Es administrador del sistema del Experience Manager con privilegios de administrador.


Al crear la cuenta, Adobe Dynamic Media proporciona automáticamente los servidores asignados a su empresa. Estos servidores se utilizan para construir cadenas de URL para el sitio web y las aplicaciones. Estas llamadas a URL son específicas de su cuenta.

Consulte también [Probar el servicio Secure Testing](/help/assets/dm-publish-settings.md#test-assets-before-making-public).

**Para configurar la configuración general de Dynamic Media:**

1. En el modo Autor del Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global.
1. En el carril izquierdo, seleccione el icono Herramientas y, a continuación, vaya a **[!UICONTROL Recursos]** > **[!UICONTROL Configuración general de Dynamic Media]**.
1. En la página Servidor , configure **[!UICONTROL Nombre del servidor publicado]** y **[!UICONTROL Nombre del servidor de origen]** y, a continuación, utilice las cinco pestañas para configurar las opciones de publicación predeterminadas.

   * [Servidor](#server-general-setting)
   * [Cargar a la aplicación](#upload-to-application)
   * [Edición de imágenes](#image-editing-tab) ficha
   * [PostScript](#postscript-tab) ficha
   * [Photoshop](#photoshop-tab) ficha
   * [PDF](#pdf-tab) ficha
   * [Illustrator](#illustrator-tab) ficha

1. Cuando haya terminado, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]**.

## Servidor {#server-general-setting}

Al crear la cuenta, Adobe Dynamic Media proporciona automáticamente los servidores asignados a su empresa. Estos servidores se utilizan para construir cadenas de URL para el sitio web y las aplicaciones. Estas llamadas a URL son específicas de su cuenta.

| Opción | Descripción |
| --- | --- |
| **[!UICONTROL Servidor de publicación]** | Requerido.<br>Este servidor es el servidor CDN (red de entrega de contenido) activo que se utiliza en todas las llamadas URL generadas por el sistema que son específicas de su cuenta. No cambie este nombre de servidor a menos que se le indique que lo haga por Adobe Technical Support. El nombre debe utilizar `https://` en la ruta. |
| **[!UICONTROL Servidor de origen]** | Requerido.<br>Este servidor solo se utiliza para pruebas de control de calidad. No cambie este nombre de servidor a menos que se le indique que lo haga el servicio de asistencia técnica de Adobe. |

## Cargar a la aplicación {#upload-to-application}

* **[!UICONTROL Sobrescribir imágenes]**

   Adobe Dynamic Media no permite que dos archivos tengan el mismo nombre. El ID de Dynamic Media de Adobe de cada elemento (el nombre de imagen menos la extensión de nombre de archivo) debe ser único. Debido a esta regla, **[!UICONTROL Cargar a la aplicación]** tiene sobrescritura. El efecto exacto de esta opción depende de la opción Sobrescribir imágenes que haya elegido. Estas opciones especifican cómo se cargan las imágenes de reemplazo: si reemplazan las imágenes originales o se convierten en imágenes duplicadas. Se cambia el nombre de las imágenes duplicadas por una `-1`. Por ejemplo, `chair.tif` se cambia el nombre `chair-1.tif`. Estas opciones afectan a las imágenes cargadas en una carpeta diferente a la original o a las imágenes con una extensión de nombre de archivo diferente a la original, como JPG, TIF o PNG.

   | Opción Sobrescribir imágenes | Descripción |
   | --- | --- |
   | **[!UICONTROL Sobrescribir en la carpeta actual, mismo nombre/extensión de base]** | Predeterminado.<br>Esta opción es la regla más estricta para la sustitución. Requiere que cargue la imagen de reemplazo en la misma carpeta que la original y que la imagen de reemplazo tenga la misma extensión de nombre de archivo que la original. Si no se cumplen estos requisitos, se crea un duplicado. |
   | **[!UICONTROL Sobrescribir en la carpeta actual, mismo nombre de base independientemente de la extensión]** | Requiere que cargue la imagen de reemplazo en la misma carpeta que el original, aunque la extensión del nombre de archivo puede ser diferente de la original. Por ejemplo, chair.tif reemplaza a chair.jpg. |
   | **[!UICONTROL Sobrescribir en cualquier carpeta con mismo nombre y ext. de recurso base]** | Requiere que la imagen de reemplazo tenga la misma extensión de nombre de archivo que la imagen original (por ejemplo, chair.jpg debe reemplazar a chair.jpg, no chair.tif). Sin embargo, puede cargar la imagen de reemplazo en una carpeta diferente a la original. La imagen actualizada reside en la nueva carpeta; el archivo ya no se puede encontrar en su ubicación original. |
   | **[!UICONTROL Sobrescribir en cualquier carpeta, mismo nombre de base independientemente de la extensión]** | Esta opción es la regla de reemplazo más inclusiva. Puede cargar una imagen de reemplazo en una carpeta distinta a la original, cargar un archivo con una extensión de nombre de archivo diferente y reemplazar el archivo original. Si el archivo original se encuentra en una carpeta diferente, la imagen de reemplazo reside en la nueva carpeta a la que se cargó. |

* **[!UICONTROL Conservar recorte]**

   Controla la preservación de cualquier definición de recorte manual existente.

   Consulte también `preserveCrop` en [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) y [ReprocessAssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html), ambas en la Guía de referencia de visores de Dynamic Media.

## Opciones de carga predeterminadas {#default-upload-options}

### Ficha Edición de imágenes {#image-editing-tab}

Este filtro permite ajustar un efecto de filtro de enfoque en la imagen final con disminución de resolución. Ayuda a controlar la intensidad del efecto, el radio del efecto (medido en píxeles) y un umbral de contraste que se ignora.

El efecto Máscara de enfoque utiliza las mismas opciones que el filtro Máscara de enfoque de Photoshop. Contrariamente a lo que sugiere el nombre, Máscara de enfoque es un filtro de enfoque.

| Opciones de máscara de enfoque | Descripción |
| --- | --- |
| **[!UICONTROL Cantidad]** | Requerido.<br>Controla la cantidad de contraste que se aplica a los píxeles de borde.<br>Piensen en ello como la intensidad del efecto. La principal diferencia entre los valores de cantidad de Máscara de enfoque en Adobe Dynamic Media y los valores de cantidad en Adobe Photoshop es que Photoshop tiene un rango de cantidad del 1% al 500%. Mientras que en Adobe Dynamic Media, el intervalo de valores es `0.0` a `5.0`. Un valor de 5,0 en Adobe Dynamic Media es el equivalente aproximado del 500 % en Photoshop; un valor de 0,9 es el equivalente a 90 %, etc. |
| **[!UICONTROL Radio]** | Requerido.<br>Controla el radio del efecto.<br>El intervalo de valores es `0` a `250`. El efecto se ejecuta en todos los píxeles de una imagen y se irradia desde todos los píxeles en todas las direcciones. El radio se mide en píxeles. Por ejemplo, para obtener un efecto de nitidez similar para una imagen de 2000 x 2000 píxeles y una imagen de 500 x 500 píxeles, establecería un radio de dos píxeles en la imagen de 2000 x 2000 píxeles. Luego establezca un valor de radio de un píxel en la imagen de 500 x 500 píxeles. Se utiliza un valor mayor para una imagen que tiene más píxeles. |
| **[!UICONTROL Umbral]** | Requerido.<br>El umbral es un intervalo de contraste que se ignora cuando se aplica el filtro Máscara de enfoque. Este efecto es importante para que no se introduzca ningún &quot;ruido&quot; en una imagen cuando se utilice este filtro. El intervalo de valores es `0` - `255`, que es el número de pasos de brillo de una imagen en escala de grises. `0`=negro, `128`=50% gris y `255`=blanco.<br>Un valor de umbral de `12` ignora las ligeras variaciones en el brillo del tono de la piel para evitar agregar ruido, pero agrega contraste al borde de áreas contrastadas como donde las pestañas tocan la piel.<br>Si tienes una foto de la cara de alguien, la máscara de enfoque afecta a las partes contrastadas de la imagen. Por ejemplo, donde las pestañas y la piel se encuentran para crear un área obvia de contraste, y la piel suave en sí. Incluso la piel más suave presenta cambios sutiles en los valores de brillo. Si no utiliza un valor de umbral, el filtro acentúa estos cambios sutiles en los píxeles de la piel. A su vez, se crea una reacción ruidosa e indeseable mientras que aumenta el contraste en las pestañas, mejorando la nitidez.<br>Para evitar este problema, se introduce un valor de umbral que indica al filtro que ignore los píxeles que no cambian el contraste de forma drástica, como la piel suave.<br>En el gráfico de cierre mostrado anteriormente, observe la textura junto a los tapones. El ruido de la imagen se muestra porque los valores de umbral eran demasiado bajos para suprimir el ruido. |
| **[!UICONTROL Monocromo]** | Seleccione para aplicar máscara de enfoque al brillo (intensidad) de la imagen.<br>Anule la selección para desenmascarar cada componente de color por separado. |

Consulte también [Enfoque de imágenes en Adobe Dynamic Media y en Image Server](/help/assets/assets/sharpening_images.pdf).

### Ficha PostScript {#postscript-tab}

Puede rasterizar archivos Adobe PostScript®, mantener fondos transparentes, elegir una resolución y elegir un espacio de color.

Puede utilizar archivos Adobe PostScript® (EPS) en Adobe Dynamic Media. Adobe Dynamic Media ofrece comandos para configurar estos archivos a medida que los carga.

Al cargar archivos de imagen PostScript (EPS), puede aplicarles formato de varias formas. Puede rasterizar los archivos, mantener el fondo transparente, elegir una resolución y elegir un espacio de color.

| Opción PostScript | Descripción |
| --- | --- |
| **[!UICONTROL Procesando]** | Seleccione Rasterizar para convertir los gráficos vectoriales del archivo al formato de mapa de bits. |
| **[!UICONTROL Mantener el fondo transparente en las imágenes procesadas]** | Conserva la transparencia en segundo plano del archivo. |
| **[!UICONTROL Resolución (píxel/pulgada)]** | Determina la configuración de resolución. Esta configuración determina cuántos píxeles se muestran por pulgada en el archivo. |
| **[!UICONTROL Espacio de color]** | ・ **[!UICONTROL Detectar automáticamente]** - Conserva el espacio de color del archivo.<br>・ **[!UICONTROL Forzar como RGB]** - Convierte al espacio de color del RGB.<br>・ **[!UICONTROL Forzar como CMYK]** - Convierte al espacio de color CMYK.<br>・ **[!UICONTROL Forzar como escala de grises]** - Convierte al espacio de color Escala de grises . |

### Ficha Photoshop {#photoshop-tab}

Puede crear plantillas a partir de archivos Photoshop® de Adobe®, mantener las capas, especificar el nombre de las capas, extraer texto y especificar cómo se anclan las imágenes en las plantillas.

| Opción Photoshop | Descripción |
| --- | --- |
| **[!UICONTROL Mantener capas]** | Extrae las capas del PSD, si las hay, en recursos individuales. Las capas de recursos permanecen asociadas al PSD. Para verlas, abra el archivo PSD en la Vista de detalles y seleccione el panel de capas. Consulte Visualización y edición de capas en un archivo de PSD. |
| **[!UICONTROL Crear plantilla]** | Crea una plantilla a partir de las capas del archivo PSD. |
| **[!UICONTROL Extraer texto]** | Extrae el texto para que los usuarios puedan buscar texto en un visualizador. |
| **[!UICONTROL Extender las capas al tamaño del fondo]** | Amplía el tamaño de las capas de imagen recortadas al tamaño de la capa de fondo. |
| **[!UICONTROL Nombres de capas]** | Amplía el tamaño de las capas de imagen recortadas al tamaño de la capa de fondo.<br>・ **[!UICONTROL Nombre de la capa]** - Nombra las imágenes después de sus nombres de capa en el archivo PSD. Por ejemplo, una capa denominada Etiqueta de precio en el archivo PSD original se convierte en una imagen denominada Etiqueta de precio. Sin embargo, si los nombres de capa del archivo PSD son nombres de capa predeterminados de Photoshop (Fondo, Capa 1, Capa 2, etc.), las imágenes reciben el nombre de sus números de capa en el archivo PSD. <br>・ **[!UICONTROL Photoshop y número de capa]** - Nombra las imágenes después de sus números de capa en el archivo PSD, ignorando los nombres de capa originales. Las imágenes reciben el nombre del archivo Photoshop y un número de capa anexado. Por ejemplo, la segunda capa de un archivo llamado `Spring Ad.psd` se llama `Spring Ad_2` incluso si tenía un nombre no predeterminado en Photoshop.<br>・ **[!UICONTROL Photoshop y nombre de capa]** - Nombra las imágenes después del archivo de PSD seguido del nombre o número de capa. El número de capa se utiliza si los nombres de capa del archivo PSD son nombres de capa predeterminados de Photoshop. Por ejemplo, una capa denominada `Price Tag` en un archivo PSD denominado `SpringAd` se llama `Spring Ad_Price Tag`. Una capa con el nombre predeterminado Capa 2 se llama `Spring Ad_2`. |
| **[!UICONTROL Ancla]** | Especifique cómo se anclan las imágenes en plantillas generadas a partir de la composición en capas producida a partir del archivo PSD. De forma predeterminada, el anclaje es el centro. Un anclaje central permite que las imágenes de reemplazo ocupen el mismo espacio, independientemente de la proporción de aspecto de la imagen de reemplazo. Las imágenes con un aspecto diferente que reemplazan a esta imagen, al hacer referencia a la plantilla y utilizar la sustitución de parámetros, ocupan efectivamente el mismo espacio. Cambie a una configuración diferente si la aplicación requiere que las imágenes de reemplazo rellenen el espacio asignado en la plantilla. |

### ficha PDF {#pdf-tab}

Puede elegir rasterizar los archivos, extraer palabras de búsqueda y vínculos, definir la resolución y elegir un espacio de color.

| opción PDF | Descripción |
| --- | --- |
| **[!UICONTROL Procesando]** | ・ **[!UICONTROL Ninguna]** - No se procesa el PDF.<br>・ **[!UICONTROL Miniatura]** - Extrae cada página del archivo PDF y la convierte en una imagen en miniatura.<br> ・ **[!UICONTROL Rasterizar]** : quita las páginas del archivo PDF y convierte los gráficos vectoriales en imágenes de mapa de bits. Para crear un catálogo electrónico, seleccione esta opción. |
| **[!UICONTROL Extraer]** | ・ **[!UICONTROL Ninguna]** - No se extraen palabras de búsqueda ni vínculos del PDF.<br>・ **[!UICONTROL Palabras de búsqueda]** - Extrae palabras de búsqueda del archivo PDF para que el archivo se pueda buscar por palabra clave en un visor de catálogos electrónicos.<br>・ **[!UICONTROL Vínculos]** - Extrae enlaces de los archivos PDF y los convierte en mapas de imágenes que se usan en un visor de catálogos electrónicos.<br>・ **[!UICONTROL Buscar palabras y vínculos]** - Extrae palabras de búsqueda y vínculos para usarlos en un visor de catálogos electrónicos. |
| **[!UICONTROL Resolución (píxel/pulgada)]** | Determina la configuración de resolución. Esta configuración determina cuántos píxeles se muestran por pulgada en el archivo PDF. El valor predeterminado es 150. |
| **[!UICONTROL Espacio de color]** | ・ **[!UICONTROL Detectar automáticamente]** : mantiene el espacio de color del archivo PDF.<br>・ **[!UICONTROL Forzar como RGB]** - Convierte al espacio de color del RGB.<br>・ **[!UICONTROL Forzar como CMYK]** - Convierte al espacio de color CMYK.<br>・ **[!UICONTROL Forzar como escala de grises]** - Convierte al espacio de color Escala de grises . |

### Ficha Illustrator {#illustrator-tab}

Puede rasterizar archivos Adobe Illustrator®, mantener fondos transparentes, elegir una resolución y elegir un espacio de color.

Puede utilizar archivos Adobe® Illustrator® (AI) en Adobe Dynamic Media. Adobe Dynamic Media ofrece comandos para configurar estos archivos a medida que los carga.

Al cargar archivos de imagen de Illustrator (AI), puede aplicarles formato de varias formas. Puede rasterizar los archivos, mantener el fondo transparente, elegir una resolución y elegir un espacio de color. Las opciones para dar formato a archivos PostScript y Illustrator están disponibles en la pantalla Cargar, en Opciones de PostScript y Opciones de Illustrator, en el cuadro Opciones de carga de trabajo .


| Opción Illustrator | Descripción |
| --- | --- |
| **[!UICONTROL Procesando]** | Seleccione Rasterizar para convertir los gráficos vectoriales del archivo al formato de mapa de bits. |
| **[!UICONTROL Mantener el fondo transparente en las imágenes procesadas]** | Conserva la transparencia en segundo plano del archivo. |
| **[!UICONTROL Resolución (píxel/pulgada)]** | Determina la configuración de resolución. Esta configuración determina cuántos píxeles se muestran por pulgada en el archivo. |
| **[!UICONTROL Espacio de color]** | ・ **[!UICONTROL Detectar automáticamente]** - Conserva el espacio de color del archivo.<br>・ **[!UICONTROL Forzar como RGB]** - Convierte al espacio de color del RGB.<br>・ **[!UICONTROL Forzar como CMYK]** - Convierte al espacio de color CMYK.<br>・ **[!UICONTROL Forzar como escala de grises]** - Convierte al espacio de color Escala de grises . |
