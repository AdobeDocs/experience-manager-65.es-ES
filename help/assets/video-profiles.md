---
title: Perfiles de vídeo
description: Dynamic Media ya viene con un perfil de codificación de vídeo adaptable predefinido. Los ajustes de este perfil listos para usar están optimizados para ofrecer a sus clientes la mejor experiencia de visualización posible. También puede agregar un recorte inteligente a los vídeos.
uuid: 26a20984-db63-41e9-b16c-6e164b7596a0
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 3b8791c8-2c97-42b7-b4a9-e1157ac9ea02
docset: aem65
feature: Perfiles de vídeo
role: Business Practitioner, Administrator
exl-id: b290fac2-7259-45d7-b733-70419d632b07
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '3704'
ht-degree: 18%

---

# Perfiles de vídeo {#video-profiles}

Dynamic Media ya viene con un perfil de codificación de vídeo adaptable predefinido. Los ajustes de este perfil listos para usar están optimizados para ofrecer a sus clientes la mejor experiencia de visualización posible. Al codificar los vídeos de origen principales mediante el perfil de codificación de vídeo adaptable, durante la reproducción el reproductor de vídeo ajusta automáticamente la calidad del flujo de vídeo en función de la velocidad de conexión a Internet de sus clientes. Esto se conoce como flujo adaptable.

A continuación se indican otros factores que determinan la calidad de los vídeos:

* **Resolución del vídeo de origen principal cargado**

   Si el vídeo MP4 se grabó a una resolución inferior, como 240p o 360p, no se puede transmitir en alta definición.

* **Tamaño del reproductor de vídeo**

   De forma predeterminada, el valor &quot;Anchura&quot; del perfil de codificación de vídeo adaptable está establecido en &quot;Automático&quot;. De nuevo, durante la reproducción se utiliza la mejor calidad en función del tamaño del reproductor.

Consulte [Prácticas recomendadas para la codificación de vídeo](/help/assets/video.md#best-practices-for-encoding-videos).

Consulte también [Prácticas recomendadas para organizar los recursos digitales para utilizar perfiles de procesamiento](/help/assets/organize-assets.md).

>[!NOTE]
>
>Para generar los metadatos de un vídeo y las miniaturas de imágenes de vídeo asociadas, el propio vídeo debe pasar por el proceso de codificación en Dynamic Media. En AEM, el flujo de trabajo **[!UICONTROL Dynamic Media Encode Video]** codifica el vídeo si ha habilitado Dynamic Media y ha configurado los servicios de nube de vídeo. Este flujo de trabajo captura el historial de procesos de flujo de trabajo y la información de errores. Consulte [Supervisión de la codificación de vídeo y progreso de publicación en YouTube](/help/assets/video.md#monitoring-video-encoding-and-youtube-publishing-progress). Si ha habilitado Dynamic Media y ha configurado los servicios de nube de vídeo, el flujo de trabajo **[!UICONTROL Dynamic Media Encode Video]** surte efecto automáticamente al cargar un vídeo. (Si no utiliza Dynamic Media, el flujo de trabajo **[!UICONTROL DAM Update Asset]** tiene efecto).
>
>Los metadatos son útiles cuando se buscan recursos. Las miniaturas son imágenes de vídeo estáticas que se generan durante la codificación. El sistema AEM los necesita y se utilizan en la interfaz de usuario para ayudarle a identificar visualmente los vídeos en la vista Tarjetas, la vista Resultados de la búsqueda y la vista Lista de recursos. Puede ver las miniaturas generadas al pulsar el icono Representaciones (paleta de un pintor) de un vídeo codificado.

Cuando haya terminado de crear el perfil de vídeo, debe aplicarlo a una carpeta o varias carpetas. Consulte [Aplicación de un perfil de vídeo a carpetas.](#applying-a-video-profile-to-folders)

Para definir parámetros de procesamiento avanzados para otros tipos de recursos, consulte [Configuración del procesamiento de recursos](/help/assets/config-dms7.md#configuring-asset-processing).

Consulte también [Perfiles para procesar metadatos, imágenes y vídeos](processing-profiles.md).

## Ajustes preestablecidos de codificación de vídeo adaptable {#adaptive-video-encoding-presets}

En la tabla siguiente se identifican los perfiles de codificación de prácticas recomendadas para la transmisión de vídeo adaptable a dispositivos móviles, tabletas y equipos de escritorio. Puede utilizar estos ajustes preestablecidos para cualquier vídeo de relación de aspecto.

<table>
 <tbody>
  <tr>
   <td><strong>Códec de formato de vídeo</strong></td>
   <td><strong>Tamaño de vídeo: ancho (px)</strong></td>
   <td><strong>Tamaño del vídeo: altura (px)</strong></td>
   <td><strong>Mantener proporción de aspecto?</strong></td>
   <td><strong>Velocidad de bits de vídeo (Kbps)</strong></td>
   <td><strong>Velocidad De Fotogramas De Vídeo (Fps)</strong></td>
   <td><strong>Códec de audio</strong></td>
   <td><strong>Velocidad de bits de audio (Kbps)</strong></td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>360</td>
   <td>Sí</td>
   <td>730</td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>540</td>
   <td>Sí</td>
   <td>2000<br /> </td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>720<br /> </td>
   <td>Sí</td>
   <td>3000<br /> </td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
 </tbody>
</table>

## Acerca del uso del recorte inteligente en perfiles de vídeo {#about-smart-crop-video}

El recorte inteligente para vídeo (una función opcional disponible en Perfiles de vídeo) es una herramienta que utiliza el poder de la inteligencia artificial en Adobe Sensei para detectar y recortar automáticamente el punto focal en cualquier vídeo adaptable o vídeo progresivo que haya cargado, independientemente del tamaño.

Los formatos de vídeo compatibles con el recorte inteligente son MP4, MKV, MOV, AVI, FLV y WMV.

El tamaño máximo del archivo de vídeo admitido para el recorte inteligente es el siguiente criterio:

* Duración de cinco minutos.
* 30 fotogramas por segundo (FPS).
* Tamaño de archivo de 300 MB.

Tenga en cuenta que Adobe Sensei está actualmente limitado a 9000 fotogramas. Es decir, cinco minutos a 30 FPS. Si el vídeo tiene un FPS más alto, la duración máxima del vídeo compatible disminuye. Por ejemplo, un vídeo de 60 FPS debe durar dos minutos y medio para que sea compatible con Adobe Sensai y con el recorte inteligente.

![Recorte inteligente para vídeo](assets/smart-crop-video.png)

>[!IMPORTANT]
>
>Para que funcione el recorte inteligente de vídeo, debe incluir uno o varios ajustes preestablecidos de codificación de vídeo en el perfil de vídeo.

Para utilizar el recorte inteligente para el vídeo, se crea un perfil de codificación de vídeo adaptable o progresivo. Como parte de su perfil, utilice la herramienta **[!UICONTROL Smart Crop Ratio]** para seleccionar relaciones de aspecto predefinidas. Por ejemplo, después de definir los ajustes preestablecidos de codificación de vídeo, puede añadir una definición de &quot;Horizontal móvil&quot; con una relación de aspecto de 16x9 y una definición de &quot;Vertical móvil&quot; con una relación de aspecto de 9x16. Otros aspectos o relaciones de recorte desde los que puede elegir incluyen 1x1, 4x3 y 4x5.

![Edición de perfiles de codificación de vídeo con recorte inteligente](assets/edit-smart-crop-video2.png)

Tenga en cuenta que puede activar o desactivar el recorte inteligente de vídeo en el perfil de vídeo mediante el control deslizante situado a la derecha de la **[!UICONTROL proporción de recorte inteligente]** en la interfaz de usuario.

Después de crear y guardar el perfil de vídeo, puede aplicarlo a las carpetas que desee.

Consulte [Aplicación de perfiles de vídeo a carpetas específicas](#applying-video-profiles-to-specific-folders) o [Aplicación de un perfil de vídeo globalmente](#applying-a-video-profile-globally).

Consulte también [Recorte inteligente para imágenes](image-profiles.md).

## Creación de un perfil de vídeo para flujo adaptable {#creating-a-video-encoding-profile-for-adaptive-streaming}

Dynamic Media ya viene con un perfil predefinido de codificación de vídeo adaptable (un grupo de ajustes de carga de vídeo para MP4 H.264) optimizado para la mejor experiencia de visualización. Puede utilizar este perfil al cargar los vídeos.

Sin embargo, si este perfil predefinido no satisface sus necesidades, puede elegir crear su propio perfil de codificación de vídeo adaptable. Al utilizar la configuración **[!UICONTROL Codificar para flujo adaptable]** como práctica recomendada, todos los ajustes preestablecidos de codificación que agregue al perfil se validan para garantizar que todos los vídeos tengan la misma proporción de aspecto. Además, los vídeos codificados se tratan como un conjunto de varias velocidades de bits para la transmisión.

Al crear el perfil de codificación de vídeo, verá que la mayoría de las opciones de codificación se rellenan previamente con ajustes predeterminados recomendados para ayudarle. Sin embargo, si selecciona un valor que no sea el predeterminado recomendado, tenga en cuenta que puede provocar una mala calidad de vídeo durante la reproducción y otros problemas de rendimiento.

Por lo tanto, para todos los ajustes preestablecidos de codificación de vídeo MP4 H.264 del perfil, se validan los siguientes valores para garantizar que sean los mismos en todos los ajustes preestablecidos de codificación individuales del perfil, lo que permite la transmisión adaptativa:

* Códec de formato de vídeo: MP4 H.264 (.mp4)
* Códec de audio
* Velocidad de bits de audio
* Mantener proporción de aspecto
* Codificación de dos pasos
* Velocidad de bits constante
* Perfil H264
* Velocidad de muestreo de audio

Si los valores no son los mismos, puede seguir creando el perfil tal cual. Sin embargo, tenga en cuenta que la transmisión adaptativa no será posible. En su lugar, los usuarios verán la transmisión de una sola velocidad de bits. Se recomienda editar la configuración de codificación para utilizar los mismos valores en ajustes preestablecidos de codificación individuales en el perfil. (Tenga en cuenta que el editor de perfiles/ajustes preestablecidos de vídeo debe aplicar la paridad de los ajustes de codificación de vídeo adaptable si &quot;Codificar para flujo adaptable&quot; está habilitado).

Consulte también [Creación de un perfil de codificación de vídeo para flujo progresivo](#creating-a-video-encoding-profile-for-progressive-streaming).

Consulte también [Prácticas recomendadas para la codificación de vídeo](/help/assets/video.md#best-practices-for-encoding-videos).

Para definir parámetros de procesamiento avanzados para otros tipos de recursos, consulte [Configuración del procesamiento de recursos](/help/assets/config-dms7.md#configuring-asset-processing).

**Para crear un perfil de vídeo para flujo adaptable**,

1. Pulse el logotipo de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de vídeo]**.
1. Toque o haga clic en **[!UICONTROL Crear]** para agregar un nuevo perfil de vídeo.

1. Introduzca un nombre y una descripción para el perfil.
1. En la página Crear/Editar ajustes preestablecidos de codificación de vídeo , pulse **[!UICONTROL Agregar ajuste preestablecido de codificación de vídeo]**.
1. En la pestaña **[!UICONTROL Básico]**, configure las opciones de vídeo y audio.
Pulse el icono de información situado junto a cada opción para obtener descripciones adicionales o ajustes recomendados basados en el códec de formato de vídeo seleccionado.
1. Bajo el encabezado Tamaño del vídeo, asegúrese de que **[!UICONTROL Mantener relación de aspecto]** está marcada.
1. Establezca la resolución del tamaño del fotograma de vídeo en píxeles. Utilice el valor **[!UICONTROL Auto]** para escalar automáticamente para que coincida con la proporción de aspecto del origen (relación ancho-alto). Por ejemplo, Automático x 480 o 640 x Automático.

1. Realice una de las acciones siguientes:

   * En el campo **[!UICONTROL Width]**, introduzca **[!UICONTROL auto]**. En el campo **[!UICONTROL Height]**, introduzca un valor en píxeles.

   * Para ayudarle a visualizar el tamaño del vídeo, pulse el icono Información (i) a la derecha de **[!UICONTROL Altura]** para abrir la página Calculadora de tamaño. Utilice **[!UICONTROL Calculadora de tamaño]** para establecer las dimensiones de vídeo (representadas por el cuadro azul) que desee. Toque **[!UICONTROL X]** en la esquina superior derecha cuando haya terminado.

1. (Opcional) Pulse la pestaña **[!UICONTROL Avanzado]** y asegúrese de que la casilla **[!UICONTROL Usar valores predeterminados]** está seleccionada (recomendada). También puede modificar la configuración avanzada de vídeo y audio.
1. En la esquina superior derecha de la página, pulse **[!UICONTROL Guardar]** para guardar el ajuste preestablecido.
1. Realice una de las acciones siguientes:
   * Repita los pasos 4-10 para crear ajustes preestablecidos de codificación adicionales. (El flujo de vídeo adaptable requiere más de un ajuste preestablecido de vídeo).
   * Continúe con el paso siguiente.

1. (Opcional) Para agregar un recorte inteligente de vídeo a los vídeos a los que se aplicará este perfil, haga lo siguiente:
   * En la página Editar perfil de vídeo , a la derecha del encabezado Proporción de recorte inteligente , pulse **[!UICONTROL Agregar nuevo]**.
   * En el campo Nombre, escriba un nombre para la proporción de recorte que le ayudará a identificarla fácilmente.
   * En la lista desplegable **[!UICONTROL Crop Ratio]**, seleccione la proporción que desee utilizar.

1. Realice una de las acciones siguientes:

   * Siga agregando nuevas relaciones de recorte según sea necesario.
   * Continúe con el paso siguiente.

1. En la esquina superior derecha de la página, pulse **[!UICONTROL Guardar]** de nuevo para guardar el perfil.

Ahora puede aplicar el perfil a las carpetas que contienen vídeos. Consulte [Aplicación de un perfil de vídeo a carpetas](#applying-a-video-profile-to-folders) o [Aplicación de un perfil de vídeo globalmente](#applying-a-video-profile-globally).

## Creación de un perfil de vídeo para flujo progresivo {#creating-a-video-encoding-profile-for-progressive-streaming}

Si decide no utilizar la opción **[!UICONTROL Codificar para flujo adaptable]**, tenga en cuenta que todos los ajustes preestablecidos de codificación que agregue al perfil se tratan como representaciones de vídeo individuales para flujo de una sola velocidad de bits o entrega de vídeo progresivo. Además, no hay ninguna validación para garantizar que todas las representaciones de vídeo tengan la misma proporción de aspecto.

Dependiendo del modo que esté ejecutando, los códecs de formato de vídeo compatibles son los siguientes:

* Modo Dynamic Media-Scene7: H.264 (.mp4)
* Modo híbrido de Dynamic Media: H.264 (.mp4), WebM

Consulte también [Creación de un perfil de codificación de vídeo para flujo adaptable](#creating-a-video-encoding-profile-for-adaptive-streaming).

Consulte también [Prácticas recomendadas para la codificación de vídeo](/help/assets/video.md#best-practices-for-encoding-videos).

Para definir parámetros de procesamiento avanzados para otros tipos de recursos, consulte [Configuración del procesamiento de recursos](/help/assets/config-dms7.md#configuring-asset-processing).

**Para crear un perfil de vídeo para flujo progresivo:**

1. Pulse el logotipo de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de vídeo]**.
1. Toque **[!UICONTROL Crear]** para agregar un nuevo perfil de vídeo.
1. Introduzca un nombre y una descripción para el perfil.
1. En la página Crear/Editar ajustes preestablecidos de codificación de vídeo , pulse **[!UICONTROL Agregar ajuste preestablecido de codificación de vídeo]**.
1. En la pestaña **[!UICONTROL Básico]**, configure las opciones de vídeo y audio.
Pulse el icono de información situado junto a cada opción para obtener descripciones adicionales o ajustes recomendados basados en el códec de formato de vídeo seleccionado.
1. (Opcional) En el encabezado Tamaño del vídeo, desmarque **[!UICONTROL Mantener relación de aspecto]**.
1. Haga lo siguiente:
   * En el campo **[!UICONTROL Width]**, introduzca **[!UICONTROL auto]**.
   * En el campo **[!UICONTROL Height]**, introduzca un valor en píxeles.
Para ayudarle a visualizar el tamaño del vídeo, pulse el icono de información Altura para abrir la página **[!UICONTROL Calculadora de tamaño]**. Utilice la página **[!UICONTROL Calculadora de tamaño]** para definir la dimensión de vídeo (cuadro azul) como desee. Cuando haya terminado, en la esquina superior derecha del cuadro de diálogo, pulse **[!UICONTROL X]**.
1. (Opcional) Realice una de las siguientes acciones:

   * Pulse la pestaña **[!UICONTROL Advanced]** y asegúrese de que la casilla **[!UICONTROL Use Default Values]** está seleccionada (recomendado).

   * Desactive la casilla de verificación **[!UICONTROL Usar valores predeterminados]** y especifique la configuración de vídeo y audio que desee.
Pulse el icono de información situado junto a cada opción para obtener descripciones adicionales o ajustes recomendados basados en el códec de formato de vídeo seleccionado.

1. En la esquina superior derecha de la página, pulse **[!UICONTROL Guardar]** para guardar el ajuste preestablecido.
1. Realice una de las acciones siguientes:

   * Repita los pasos 4-9 para crear ajustes preestablecidos de codificación adicionales.
   * Continúe con el paso siguiente.

1. (Opcional) Para agregar un recorte inteligente de vídeo a los vídeos a los que se aplicará este perfil, haga lo siguiente:

   * En la página Editar perfil de vídeo , a la derecha del encabezado Proporción de recorte inteligente , pulse **[!UICONTROL Agregar nuevo]**.
   * En el campo Nombre, escriba un nombre para la proporción de recorte que le ayudará a identificarla fácilmente.
   * En la lista desplegable **[!UICONTROL Crop Ratio]**, seleccione la proporción que desee utilizar.

1. Realice una de las acciones siguientes:

   * Siga agregando nuevas relaciones de recorte según sea necesario.
   * Continúe con el paso siguiente.

1. En la esquina superior derecha de la página, pulse **[!UICONTROL Guardar]** para almacenar el perfil.

Ahora puede aplicar el perfil a las carpetas que contienen vídeos. Consulte [Aplicación de un perfil de vídeo a carpetas](#applying-a-video-profile-to-folders) o [Aplicación de un perfil de vídeo globalmente](#applying-a-video-profile-globally).

## Uso de parámetros de codificación de vídeo personalizados {#using-custom-added-video-encoding-parameters}

Puede editar un perfil de codificación de vídeo existente para aprovechar los parámetros avanzados de codificación de vídeo que no se encuentran en la interfaz de usuario al crear o editar un perfil de vídeo en AEM. Los parámetros personalizados (como minBitrate y maxBitrate) se agregan al perfil existente.

**Para utilizar parámetros** de codificación de vídeo personalizados:

1. Pulse el logotipo de AEM y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. En la página CRXDE Lite, en el panel Explorador de la izquierda, vaya a lo siguiente:

   `/conf/global/settings/dam/dm/presets/video/*name_of_video_encoding_profile_to_edit`

1. En el panel situado en la parte inferior derecha de la página, en la pestaña Propiedades, especifique el **[!UICONTROL nombre]**, el **[!UICONTROL tipo]** y el **[!UICONTROL valor]** del parámetro que desea utilizar.

   Los siguientes parámetros avanzados están disponibles para su uso:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre</strong></td>
   <td><strong>Descripción</strong><br /> </td>
   <td><strong>Tipo</strong><br /> </td>
   <td><strong>Value</strong></td>
  </tr>
  <tr>
   <td><code>h264Level</code></td>
   <td>Nivel H.264 que se utilizará para la codificación. Normalmente, esto se determina automáticamente según la configuración de codificación que utilice.</td>
   <td><code>String</code></td>
   <td><p>10 * nivel h264</p> <p>Por ejemplo, 3,0 = 30, 1,3 = 13)</p> <p>No hay ningún valor predeterminado.</p> </td>
  </tr>
  <tr>
   <td><code>keyframe</code></td>
   <td>El número de fotogramas de destino entre fotogramas clave. Calcule este valor para generar un fotograma clave cada 2-10 segundos. Por ejemplo, a 30 fotogramas por segundo, el intervalo de fotogramas clave debe ser de 60 a 300.<br /> <br /> Los intervalos más bajos de los fotogramas clave mejoran la búsqueda de flujo y el comportamiento de conmutación de flujo para las codificaciones de vídeo adaptables, y también pueden mejorar la calidad de los vídeos que tienen mucho movimiento. Sin embargo, debido a que los fotogramas clave aumentan el tamaño de un archivo, un intervalo de fotogramas clave inferior generalmente da como resultado una menor calidad de vídeo general a una velocidad de bits determinada.</td>
   <td><code>String</code></td>
   <td><p>Número positivo.</p> <p>El valor predeterminado es 300.</p> <p>El valor recomendado para HLS (HTTP Live Streaming) es 60-90.</p> </td>
  </tr>
  <tr>
   <td><code>minBitrate</code></td>
   <td><p>Velocidad de bits mínima para permitir codificaciones de velocidad de bits variable, en Kbps (kilobits por segundo).</p> <p>Este parámetro solo se aplica cuando<strong> Utilizar velocidad de bits constante</strong> no está seleccionado en la ficha Avanzado cuando se crea o edita un perfil de codificación de vídeo.</p> <p>Consulte también <a href="/help/assets/video.md#bitrate">Velocidad de bits</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>Número positivo, en Kbps.</p> <p>No hay ningún valor predeterminado.</p> </td>
  </tr>
  <tr>
   <td><code>maxBitrate</code></td>
   <td><p>Velocidad de bits máxima para permitir codificaciones de velocidad de bits variables, en Kbps.</p> <p>Este parámetro solo se aplica cuando<strong> Utilizar velocidad de bits constante</strong> no está seleccionado en la ficha Avanzado cuando se crea o edita un perfil de codificación de vídeo.</p> <p>Consulte también <a href="/help/assets/video.md#bitrate">Velocidad de bits</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>Número positivo, en Kbps.</p> <p>No hay ningún valor predeterminado. Sin embargo, el valor recomendado es hasta dos veces superior a la velocidad de bits de la codificación.</p> </td>
  </tr>
  <tr>
   <td><code>audioBitrateCustom</code></td>
   <td>Establezca el valor en <code>true</code> para forzar una velocidad de bits constante para el flujo de audio, si es compatible con el códec de audio.</td>
   <td><code>String</code></td>
   <td><p><code>true</code>/<code>false</code></p> <p>El valor predeterminado es <code>false</code>.</p> <p>El valor recomendado para HLS (HTTP Live Streaming) es <code>false</code>.</p> <p> </p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-516](assets/chlimage_1-516.png)

1. Cerca de la esquina inferior derecha de la página, pulse **[!UICONTROL Agregar]**.
1. Realice una de las acciones siguientes:

   * Repita los pasos 3 y 4 para agregar otro parámetro al perfil de codificación de vídeo.
   * Cerca de la esquina superior izquierda de la página, pulse **[!UICONTROL Guardar todo]**.

1. En la esquina superior izquierda de la página CRXDE Lite, pulse el icono **[!UICONTROL Back Home]** para volver a AEM.

### Edición de un perfil de vídeo {#editing-a-video-encoding-profile}

Puede editar cualquier perfil de vídeo que haya creado para agregar, editar o eliminar ajustes preestablecidos de vídeo dentro de ese perfil.

De forma predeterminada, no puede editar el perfil predefinido **[!UICONTROL Adaptive Video Encoding]** que viene con Dynamic Media. En su lugar, puede copiar fácilmente el perfil y guardarlo con un nuevo nombre. A continuación, puede editar los ajustes preestablecidos que desee en el perfil copiado.

Consulte también [Prácticas recomendadas para la codificación de vídeo](/help/assets/video.md#best-practices-for-encoding-videos).

Para definir parámetros de procesamiento avanzados para otros tipos de recursos, consulte [Configuración del procesamiento de recursos](/help/assets/config-dms7.md#configuring-asset-processing).

**Para editar un perfil** de vídeo:

1. Pulse el logotipo de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de vídeo]**.
1. En la página Perfiles de vídeo , marque un nombre de perfil de vídeo.
1. En la barra de herramientas, pulse **[!UICONTROL Editar]**.
1. En la página Perfil de codificación de vídeo , edite el nombre y la descripción como desee.
1. Como práctica recomendada, compruebe que la casilla de verificación **[!UICONTROL Codificar para flujo adaptable]** está activada.
Pulse el icono de información para ver una descripción del flujo adaptable. (Si está editando un perfil de vídeo progresivo, no active esta casilla de verificación).
1. En el encabezado Ajustes preestablecidos de codificación de vídeo , agregue, edite o elimine los ajustes preestablecidos de codificación de vídeo que conforman el perfil.

   Pulse el icono de información que hay junto a cada opción en las pestañas **[!UICONTROL Básico]** y **[!UICONTROL Avanzado]** para obtener descripciones adicionales o ajustes recomendados basados en el códec de formato de vídeo seleccionado.

1. En la esquina superior derecha de la página, pulse **[!UICONTROL Guardar]**.

### Copia de un perfil de vídeo {#copying-a-video-encoding-profile}

1. Pulse el logotipo de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de vídeo]**.
1. En la página Perfiles de vídeo , marque un nombre de perfil de vídeo.
1. En la barra de herramientas, pulse **[!UICONTROL Copiar]**.
1. En la página Perfil de codificación de vídeo , introduzca un nuevo nombre para el perfil.
1. Como práctica recomendada, compruebe que la casilla de verificación **[!UICONTROL Codificar para flujo adaptable]** está activada. Pulse el icono de información para ver una descripción del flujo adaptable. (Si está copiando un perfil de vídeo progresivo, no active la casilla de verificación).

   En Dynamic Media: modo híbrido, si un ajuste preestablecido de vídeo WebM forma parte del perfil de vídeo, no es posible **[!UICONTROL Codificar para flujo adaptable]** porque todos los ajustes preestablecidos deben ser MP4.
1. En el encabezado Ajustes preestablecidos de codificación de vídeo , agregue, edite o elimine los ajustes preestablecidos de codificación de vídeo que conforman el perfil.

   Pulse el icono de información situado junto a cada opción en las pestañas Básico y Avanzado para ver la configuración y las descripciones recomendadas.

1. En la esquina superior derecha de la página, pulse **[!UICONTROL Guardar]**.

### Eliminación de un perfil de vídeo {#deleting-a-video-encoding-profile}

1. Pulse el logotipo de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de vídeo]**.
1. En la página Perfiles de vídeo , compruebe uno o varios nombres de perfil de vídeo.
1. En la barra de herramientas, pulse **[!UICONTROL Eliminar]**.
1. Pulse **[!UICONTROL Aceptar]**.

## Aplicación de un perfil de vídeo a carpetas {#applying-a-video-profile-to-folders}

Al asignar un perfil de vídeo a una carpeta, las subcarpetas heredan automáticamente el perfil de su carpeta principal. Esto significa que solo puede asignar un perfil de vídeo a una carpeta. Como tal, considere detenidamente la estructura de carpetas en la que carga, almacena, utiliza y archiva recursos.

Si ha asignado un perfil de vídeo diferente a una carpeta, el nuevo perfil anula el perfil anterior. Los recursos de carpeta existentes no cambian. El nuevo perfil se aplica a los recursos que se agregan a la carpeta más adelante.

Las carpetas que tienen un perfil asignado se indican en la interfaz de usuario por el nombre del perfil que aparece en el nombre de la tarjeta.

![chlimage_1-517](assets/chlimage_1-517.png)

Puede aplicar perfiles de vídeo a carpetas específicas o globalmente a todos los recursos.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de vídeo existente que haya cambiado posteriormente. Consulte el artículo [Reprocesamiento de recursos en una carpeta después de editar su perfil de procesamiento](processing-profiles.md#reprocessing-assets).

### Aplicación de un perfil de vídeo a carpetas específicas {#applying-video-profiles-to-specific-folders}

Puede aplicar un perfil de vídeo a una carpeta desde el menú **[!UICONTROL Herramientas]** o, si se encuentra en la carpeta, desde **[!UICONTROL Propiedades]**. En esta sección se describe cómo aplicar perfiles de vídeo a las carpetas de ambos modos.

Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

Consulte también [Reprocesamiento de recursos en una carpeta después de editar su perfil de procesamiento](processing-profiles.md#reprocessing-assets).

#### Aplicación de un perfil de vídeo a carpetas mediante la interfaz de usuario Perfiles {#applying-video-profiles-to-folders-by-way-of-the-profiles-user-interface}

1. Pulse el logotipo de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de vídeo]**.
1. Seleccione el perfil de vídeo que desea aplicar a una o varias carpetas.
1. Pulse **[!UICONTROL Aplicar perfil a las carpetas]** y seleccione la carpeta o carpetas que desee utilizar para recibir los recursos cargados recientemente y pulse **[!UICONTROL Aplicar]**. Las carpetas que ya tienen un perfil asignado se indican mostrando el nombre del perfil directamente debajo del nombre de la carpeta en el modo **[!UICONTROL Vista de tarjeta]**.
Puede [monitorizar el progreso de un trabajo de procesamiento de perfiles de vídeo](#monitoring-the-progress-of-an-encoding-job).

#### Aplicación de un perfil de vídeo a carpetas desde Propiedades {#applying-video-profiles-to-folders-from-properties}

1. Toque o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Assets]** y, a continuación, a la carpeta a la que desee aplicar un perfil de vídeo.
1. En la carpeta, pulse la marca de verificación para seleccionarla y, a continuación, pulse **[!UICONTROL Propiedades]**.
1. Seleccione la pestaña **[!UICONTROL Perfiles de vídeo]**, seleccione el perfil en el menú desplegable y haga clic en **[!UICONTROL Guardar y cerrar]**. Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

   ![chlimage_1-518](assets/chlimage_1-518.png)
Puede  [monitorizar el progreso de un trabajo](#monitoring-the-progress-of-an-encoding-job) de procesamiento de perfiles de vídeo.

### Aplicación global de un perfil de vídeo {#applying-a-video-profile-globally}

Además de aplicar un perfil a una carpeta, también puede aplicarlo de forma global para que cualquier contenido cargado en AEM recursos de cualquier carpeta tenga aplicado el perfil seleccionado.

Consulte también [Reprocesamiento de recursos en una carpeta después de editar su perfil de procesamiento](processing-profiles.md#reprocessing-assets).

**Para aplicar un perfil de vídeo globalmente:**

* Vaya al CRXDE Lite al nodo siguiente: `/content/dam/jcr:content`. Agregue la propiedad `videoProfile:/libs/settings/dam/video/dynamicmedia/<name of video encoding profile>` y pulse **[!UICONTROL Guardar todo]**.

   ![chlimage_1-519](assets/chlimage_1-519.png)
* Puede [monitorizar el progreso de un trabajo de procesamiento de perfiles de vídeo](#monitoring-the-progress-of-an-encoding-job).

## Monitorización del progreso de un trabajo de procesamiento de perfiles de vídeo {#monitoring-the-progress-of-an-encoding-job}

Se muestra un indicador de procesamiento (o barra de progreso) para que pueda supervisar visualmente el progreso de un trabajo de procesamiento de perfiles de vídeo.

También puede ver el archivo `error.log` para supervisar el progreso de un trabajo de codificación, para ver si la codificación ha finalizado o si se han producido errores en el trabajo. El `error.log` se encuentra en la carpeta `logs` donde está instalada la instancia de AEM.

## Eliminación de un perfil de vídeo de las carpetas {#removing-a-video-profile-from-folders}

Al quitar un perfil de vídeo de una carpeta, las subcarpetas heredan automáticamente la eliminación del perfil de su carpeta principal. Sin embargo, cualquier procesamiento de archivos que se haya producido dentro de las carpetas permanece intacto.

Puede quitar un perfil de vídeo de una carpeta desde el menú **[!UICONTROL Herramientas]** o, si se encuentra en la carpeta, desde **[!UICONTROL Configuración de carpeta]**. En esta sección se describe cómo quitar perfiles de vídeo de las carpetas de ambos modos.

### Eliminación de un perfil de vídeo de carpetas mediante la interfaz de usuario Perfiles {#removing-video-profiles-from-folders-by-way-of-the-profiles-user-interface}

1. Pulse el logotipo de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de vídeo]**.
1. Seleccione el perfil de vídeo que desea eliminar de una carpeta o varias carpetas.
1. Pulse **[!UICONTROL Eliminar perfil de las carpetas]** y seleccione la carpeta o carpetas que desee utilizar para quitar el perfil. A continuación, pulse **[!UICONTROL Quitar]**.

   Puede confirmar que el perfil de vídeo ya no se aplica a una carpeta porque el nombre ya no aparece debajo del nombre de la carpeta.

### Eliminación de un perfil de vídeo de carpetas mediante Propiedades {#removing-video-profiles-from-folders-by-way-of-properties}

1. Toque o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Assets]** y, a continuación, a la carpeta desde la que desea eliminar un perfil de vídeo.
1. En la carpeta, pulse la marca de verificación para seleccionarla y, a continuación, pulse **[!UICONTROL Propiedades]**.
1. Seleccione la pestaña **[!UICONTROL Perfiles de vídeo]** y seleccione **[!UICONTROL Ninguno]** en el menú desplegable y haga clic en **[!UICONTROL Guardar y cerrar]**. Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.
