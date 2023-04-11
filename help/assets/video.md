---
title: Vídeo en Dynamic Media
description: Aprenda a trabajar con vídeo en Dynamic Media, como prácticas recomendadas para codificar vídeos, publicar vídeos en YouTube y ver informes de vídeo. Aprenda también a añadir subtítulos o marcadores de capítulo a los vídeos.
mini-toc-levels: 3
uuid: 97f311a3-a227-479a-91bf-fb54ecd1a55d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 1103b849-0042-4e11-b170-38ee81dd0157
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 28cf9e39-cab4-4278-b6c9-e84cc31964db
source-git-commit: 3430897fc98aecbcf6cc7bf6bdc9b3df24e92366
workflow-type: tm+mt
source-wordcount: '8098'
ht-degree: 3%

---

# Vídeo en Dynamic Media {#video}

En esta sección se describe cómo trabajar con vídeo en Dynamic Media.

## Inicio rápido: Vídeos {#quick-start-videos}

La siguiente descripción paso a paso del flujo de trabajo está diseñada para ayudarle a poner en marcha rápidamente los conjuntos de vídeos adaptables en Dynamic Media. Después de cada paso, hay referencias cruzadas a encabezados de temas donde puede encontrar más información.

>[!IMPORTANT]
>
>Antes de trabajar con vídeo en Dynamic Media, asegúrese de que su administrador de Adobe Experience Manager ya haya habilitado y configurado los Cloud Services de Dynamic Media en Dynamic Media - modo Scene7 o Dynamic Media - modo híbrido.
>
>* Consulte [Configuración de Cloud Services de Dynamic Media](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) en Configuración de Dynamic Media: modo Scene7 y [Resolución de problemas de Dynamic Media: modo Scene7](/help/assets/troubleshoot-dms7.md).
>
>* Consulte [Configuración de Cloud Services de Dynamic Media](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services) en Configuración de Dynamic Media: modo híbrido.
>
>Problema de reproducción de vídeo conocido actualmente en Dynamic Media *solo en el Experience Manager 6.5.9.0*:
>
>* Si se actualiza un vídeo publicado, debe volver a publicarse para reflejar los cambios en la entrega.
>


1. **Cargar vídeos de Dynamic Media** haciendo lo siguiente:

   * Cree su propio perfil de codificación de vídeo. O bien, simplemente puede utilizar el _Codificación de vídeo adaptable_ perfil que viene con Dynamic Media.

      * [Creación de un perfil de codificación de vídeo](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * Más información sobre [Prácticas recomendadas para la codificación de vídeo](#best-practices-for-encoding-videos).
   * Asocie el perfil de procesamiento de vídeo a una o varias carpetas en las que va a cargar los vídeos de origen principales.

      * [Aplicación de un perfil de vídeo a carpetas](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).
      * Más información sobre [Prácticas recomendadas para organizar los recursos digitales con el fin de utilizar perfiles de procesamiento](/help/assets/organize-assets.md).
      * Más información sobre [Organizar recursos digitales](/help/assets/organize-assets.md).
   * Cargue los vídeos de origen principales en las carpetas. Al agregar vídeos a la carpeta, estos se codifican según el perfil de procesamiento de vídeo que asignó a la carpeta.

      * Dynamic Media admite principalmente vídeos de formato corto con una longitud máxima de 30 minutos y una resolución mínima buena de 25 x 25.
      * Puede cargar archivos de vídeo de hasta 15 GB cada uno.
      * [Cargar vídeos](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).
      * Más información sobre [Formatos de archivo de entrada compatibles](/help/assets/assets-formats.md#supported-multimedia-formats).
   * Monitorizar cómo [la codificación de vídeo está progresando](#monitoring-video-encoding-and-youtube-publishing-progress) bien desde la vista de recursos o flujo de trabajo.




1. **Administrar los vídeos de Dynamic Media** realizando cualquiera de las siguientes acciones:

   * Organizar, examinar y buscar recursos de vídeo

      * [Organizar recursos digitales](/help/assets/organize-assets.md)
Más información sobre [Prácticas recomendadas para organizar los recursos digitales con el fin de utilizar perfiles de procesamiento](organize-assets.md)

      * [Buscar recursos de vídeo](search-assets.md#custompredicates) o [Buscar recursos](/help/assets/search-assets.md)
   * Vista previa y publicación de recursos de vídeo

      * Vea el vídeo de origen y las representaciones codificadas del vídeo junto con sus miniaturas asociadas:
         [Vista previa de vídeos](managing-video-assets.md#upload-and-preview-video-assets) o [Vista previa de recursos](previewing-assets.md)
         [Ver representaciones de vídeo](video-renditions.md)
         [Administrar representaciones de vídeo](manage-assets.md#managing-renditions)

      * [Administrar ajustes preestablecidos de visor](managing-viewer-presets.md)
      * [Publicar recursos](publishing-dynamicmedia-assets.md)
   * Trabajo con metadatos de vídeo

      * Vea las propiedades de una representación de vídeo codificada, como la velocidad de fotogramas, la velocidad de bits de audio y vídeo y el códec:
         [Ver propiedades de representación de vídeo](video-renditions.md)

      * Edite las propiedades del vídeo, como el título, la descripción y las etiquetas, campos de metadatos personalizados:
         [Editar propiedades de vídeo](manage-assets.md#editing-properties)

      * [Administrar metadatos de recursos digitales](metadata.md)
      * [Esquemas de metadatos](metadata-schemas.md)
   * Revisar, aprobar y anotar vídeos y mantener el control de versiones completo

      * [Anotar vídeos](managing-video-assets.md#annotate-video-assets) o [Anotar recursos](manage-assets.md#annotating)

      * [Crear una versión](manage-assets.md#asset-versioning)
      * [Aplicación de flujos de trabajo a recursos](assets-workflow.md) o consulte [Inicio de un flujo de trabajo en un recurso](manage-assets.md#starting-a-workflow-on-an-asset)

      * [Revisar recursos de carpetas](bulk-approval.md)
      * [Proyectos](../sites-authoring/projects.md)




1. **Publicación de vídeos de Dynamic Media** realizando una de las siguientes acciones:

   * Si usa Adobe Experience Manager como sistema de administración de contenido web, puede agregar vídeos directamente a las páginas web.

      * [Agregar vídeos a las páginas web](adding-dynamic-media-assets-to-pages.md).
   * Si utiliza un sistema de administración de contenido web de terceros, puede vincular o incrustar vídeos a sus páginas web.

      * Integrar vídeo con URL:
         [Vinculación de URL en la aplicación web](linking-urls-to-yourwebapplication.md).

      * Integración de vídeo mediante el código incrustado en la página web:
         [Incrustar el visor de vídeo en una página web](embed-code.md).
   * [Publicar vídeos en YouTube](#publishing-videos-to-youtube).
   * [Generar informes de vídeo](#viewing-video-reports).

   * [Agregar subtítulos a vídeo](#adding-captions-to-video).



## Trabajo con vídeo en Dynamic Media {#working-with-video-in-dynamic-media}

Video in Dynamic Media es una solución integral que facilita la publicación de vídeos adaptables de alta calidad para su transmisión en varias pantallas, incluidos equipos de escritorio, iOS, Android™, BlackBerry® y dispositivos móviles Windows. Un conjunto de vídeos adaptables agrupa versiones del mismo vídeo codificadas a diferentes velocidades de bits y formatos, como 400 kbps, 800 kbps y 1000 kbps. El equipo de escritorio o dispositivo móvil detecta el ancho de banda disponible.

Por ejemplo, en un dispositivo móvil iOS, detecta un ancho de banda como 3G, 4G o Wi-Fi. A continuación, selecciona automáticamente el vídeo codificado correcto entre las distintas tasas de bits de vídeo del conjunto de vídeos adaptables. El vídeo se transmite a escritorios, dispositivos móviles o tabletas.

Además, la calidad del vídeo se cambia automáticamente si las condiciones de red cambian en el escritorio o en el dispositivo móvil. Además, si un cliente entra en el modo de pantalla completa en un escritorio, el conjunto de vídeos adaptables responde mediante una mejor resolución, lo que mejora la experiencia de visualización del cliente. El uso de conjuntos de vídeos adaptables le ofrece la mejor reproducción posible para los clientes que reproduzcan vídeo de Dynamic Media en varias pantallas y dispositivos.

La lógica que utiliza un reproductor de vídeo para determinar qué vídeo codificado reproducir o seleccionar durante la reproducción se basa en el siguiente algoritmo:

1. El reproductor de vídeo carga el fragmento de vídeo inicial en función de la velocidad de bits más cercana al valor establecido para la &quot;velocidad de bits inicial&quot; en el propio reproductor.
1. El reproductor de vídeo cambia en función de los cambios en la velocidad de ancho de banda mediante los siguientes criterios:

   1. El reproductor elige el flujo de ancho de banda más alto por debajo o igual al ancho de banda estimado.
   1. El reproductor considera sólo el 80% del ancho de banda disponible. Sin embargo, si está subiendo, es más conservador, con solo el 70%, evitar sobreestimar y volver a empezar de inmediato.

Para obtener información técnica detallada sobre el algoritmo, consulte [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

Para administrar conjuntos de vídeos adaptables y de vídeo único, se admite lo siguiente:

* Carga de vídeo desde varios formatos de vídeo y formatos de audio compatibles y codificación de vídeo al formato MP4 H.264 para su reproducción en varias pantallas. Puede utilizar ajustes preestablecidos de vídeo adaptable predefinidos, ajustes preestablecidos de codificación de vídeo único o personalizar su propia codificación para controlar la calidad y el tamaño del vídeo.

   * Cuando se genera un conjunto de vídeos adaptables, incluye vídeos MP4.
   * **Nota**: Los vídeos principales/de origen no se agregan a un conjunto de vídeos adaptables.

* Subtítulos de vídeo en todos los visualizadores de vídeo de HTML5.
* Organice, examine y busque vídeos con compatibilidad para metadatos completa para una administración eficiente de los recursos de vídeo.
* Entregue conjuntos de vídeos adaptables a la Web y a los equipos de escritorio, así como a los dispositivos móviles, incluidos iPhone, iPad, Android™, BlackBerry® y Windows Phone.

La transmisión de vídeo adaptable es compatible con varias plataformas de iOS. Consulte [Guía de referencia de visores de Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html#video).

Dynamic Media admite la reproducción de vídeo móvil para vídeo MP4 H.264. Puede encontrar los dispositivos BlackBerry® compatibles con este formato de vídeo en el siguiente enlace: [Formatos de vídeo compatibles con BlackBerry®](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

Puede encontrar los dispositivos de Windows compatibles con este formato de vídeo en el siguiente enlace: [Códecs multimedia compatibles con Windows Phone 8](https://learn.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs)



* Reproduzca el vídeo con los ajustes preestablecidos del visualizador de vídeo de Dynamic Media, que incluyen lo siguiente:

   * Visores de vídeo únicos.
   * Visores de medios mixtos que combinan contenido de vídeo y de imagen.

* Configure reproductores de vídeo para satisfacer sus necesidades de promoción de la marca.
* Integre vídeo en su sitio web, sitio móvil o aplicación móvil con una URL simple o un código incrustado.

<!-- See [Dynamic video playback](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480) sample. -->

Consulte también [Visualizadores para Experience Manager Assets y Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) y [Visualizadores solo para recursos de Experience Manager](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only).

## Práctica recomendada: Uso del visor de vídeo de HTML5 {#best-practice-using-the-html-video-viewer}

Los ajustes preestablecidos del visor de vídeo de Dynamic Media HTML5 son reproductores de vídeo sólidos. Puede utilizarlos para evitar muchos problemas comunes asociados con la reproducción de vídeo de HTML5. Además, los problemas asociados con dispositivos móviles como la falta de transmisión de velocidad de bits adaptable y el limitado alcance del navegador de escritorio.

En el lado de diseño del reproductor, puede diseñar la funcionalidad del reproductor de vídeo mediante herramientas de desarrollo web estándar. Por ejemplo, puede diseñar los botones, los controles y el fondo personalizado de la imagen de póster utilizando HTML5 y CSS para ayudarle a llegar a sus clientes con un aspecto personalizado.

En el lado de reproducción del visor, detecta automáticamente la capacidad de vídeo del explorador. A continuación, sirve el vídeo utilizando HLS (HTTP Live Streaming) o DASH (Dynamic Adaptive Streaming over HTTP) , también conocido como flujo de velocidad de bits adaptable. O, si esos métodos de envío no están presentes, se utiliza HTML5 progresiva en su lugar.

Combinando en un solo reproductor lo siguiente:

* La capacidad de diseñar los componentes de reproducción mediante HTML5 y CSS
* Tener reproducción incrustada
* Utilizar flujo adaptable y progresivo según la capacidad del explorador

Amplía el alcance del contenido multimedia enriquecido tanto a los usuarios de escritorio como a los móviles y garantiza una experiencia de vídeo optimizada.

Consulte también [Acerca de los visores de HTML5](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only).

### Reproducción de vídeo en equipos de escritorio y dispositivos móviles mediante el visor de vídeo de HTML5 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

Para el streaming de vídeo adaptable móvil y de escritorio, los vídeos utilizados para el cambio de velocidad de bits se basan en todos los vídeos MP4 del conjunto de vídeos adaptables.

La reproducción de vídeo se produce mediante DASH o HLS, o mediante descarga progresiva de vídeo. En versiones anteriores de Experience Manager, como 6.0, 6.1 y 6.2, los vídeos se transmitían por HTTP.

En el Experience Manager 6.3 y en adelante, los vídeos ahora se transmiten a través de HTTPS (es decir, DASH o HLS) porque la URL del servicio de puerta de enlace DM también utiliza HTTPS. Este comportamiento predeterminado no afecta al cliente. Es decir, el flujo de vídeo siempre se produce a través de HTTPS a menos que el explorador no lo admita. (véase la tabla siguiente). Por lo tanto,

* Si tiene un sitio web HTTPS con flujo de vídeo HTTPS, la transmisión está bien.
* Si tiene un sitio web HTTP con flujo de vídeo HTTPS, la transmisión está bien y no hay problemas de contenido mixto en el navegador web.

DASH es el estándar internacional y HLS es un estándar de Apple. Ambos se utilizan para el flujo de vídeo adaptable. Además, ambas tecnologías ajustan automáticamente la reproducción en función de la capacidad de ancho de banda de la red. También permite al cliente &quot;buscar&quot; en cualquier punto del vídeo sin necesidad de esperar a que se descargue el resto del vídeo.

El vídeo progresivo se entrega descargando y almacenando el vídeo localmente en el sistema de escritorio o dispositivo móvil del usuario.

En la tabla siguiente se describe el dispositivo, el navegador y el método de reproducción de los vídeos en equipos de escritorio y dispositivos móviles que utilizan el visor de vídeo de Dynamic Media.

<table>
 <tbody>
  <tr>
   <td><strong>Dispositivo</strong></td>
   <td><strong>Explorador</strong></td>
   <td><strong>Modo de reproducción de vídeo</strong></td>
  </tr>
  <tr>
   <td>Escritorio</td>
   <td>Internet Explorer 9 y 10</td>
   <td>Descarga progresiva.</td>
  </tr>
  <tr>
   <td>Escritorio</td>
   <td>Internet Explorer 11+</td>
   <td>En Windows 8 y Windows 10: forzar el uso de HTTPS siempre que se solicite DASH* o HLS. Limitación conocida: HTTP en DASH* o HLS no funciona en esta combinación de navegador/sistema operativo<br /> <br /> En Windows 7: descarga progresiva. Utiliza lógica estándar para seleccionar protocolo HTTP o HTTPS.</td>
  </tr>
  <tr>
   <td>Escritorio</td>
   <td>Firefox 23-44</td>
   <td>Descarga progresiva.</td>
  </tr>
  <tr>
   <td>Escritorio</td>
   <td>Firefox 45 o posterior</td>
   <td>Flujo continuo de velocidad de bits adaptable DASH* o HLS.</td>
  </tr>
  <tr>
   <td>Escritorio</td>
   <td>Chrome</td>
   <td>Flujo continuo de velocidad de bits adaptable DASH* o HLS.</td>
  </tr>
  <tr>
   <td>Escritorio</td>
   <td>Safari (Mac)</td>
   <td>Flujo continuo de velocidad de bits adaptable HLS.</td>
  </tr>
  <tr>
   <td>Móvil</td>
   <td>Chrome (Android™ 6 o anterior)</td>
   <td>Descarga progresiva.</td>
  </tr>
  <tr>
   <td>Móvil</td>
   <td>Chrome (Android™ 7 o posterior)</td>
   <td>Flujo continuo de velocidad de bits adaptable DASH* o HLS.</td>
  </tr>
  <tr>
   <td>Móvil</td>
   <td>Android™ (navegador predeterminado)</td>
   <td>Descarga progresiva.</td>
  </tr>
  <tr>
   <td>Móvil</td>
   <td>Safari (iOS)</td>
   <td>Flujo continuo de velocidad de bits adaptable HLS.</td>
  </tr>
  <tr>
   <td>Móvil</td>
   <td>Chrome (iOS)</td>
   <td>Flujo continuo de velocidad de bits adaptable HLS.</td>
  </tr>
  <tr>
   <td>Móvil</td>
   <td>BlackBerry®</td>
   <td>Flujo continuo de velocidad de bits adaptable DASH* o HLS./td&gt;
  </tr>
 </tbody>
</table>

>[!IMPORTANT]
>
>*Para usar DASH en tus vídeos, primero debe ser habilitado por el servicio de asistencia técnica de Adobe en tu cuenta. Consulte [Habilitar DASH en su cuenta](#enable-dash).

## Arquitectura de la solución de vídeo de Dynamic Media {#architecture-of-dynamic-media-video-solution}

El siguiente gráfico muestra el flujo de trabajo general de creación de vídeos que se cargan y codifican mediante DMGgateway (en modo híbrido de Dynamic Media) y que están disponibles para el consumo público.

![chlimage_1-427](assets/chlimage_1-427.png)

## Arquitectura de publicación híbrida para vídeos {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## Prácticas recomendadas para la codificación de vídeos {#best-practices-for-encoding-videos}

La variable **Codificar vídeo de Dynamic Media** flujo de trabajo codifica el vídeo si ha activado Dynamic Media y ha configurado los servicios de nube de vídeo. Este flujo de trabajo captura el historial de procesos de flujo de trabajo y la información de errores. Consulte [Monitorización de la codificación de vídeo y progreso de publicación de YouTube](#monitoring-video-encoding-and-youtube-publishing-progress). Si ha habilitado Dynamic Media y ha configurado los servicios de nube de vídeo, la variable **[!UICONTROL Codificar vídeo de Dynamic Media]** El flujo de trabajo de se aplica automáticamente al cargar un vídeo. (Si no utiliza Dynamic Media, la variable **[!UICONTROL Recurso de actualización DAM]** tiene efecto).

<!-- DEAD The following are best-practice tips for encoding source video files.

For advice about video encoding, see [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en).

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en). -->

### Archivos de vídeo de origen {#source-video-files}

Cuando codifique un archivo de vídeo, utilice un archivo de vídeo de origen de la máxima calidad posible. Evite utilizar archivos de vídeo codificados anteriormente porque estos archivos ya están comprimidos y una codificación adicional crea un vídeo de calidad inferior.

* Dynamic Media admite principalmente vídeos de formato corto con una longitud máxima de 30 minutos y una resolución mínima buena de 25 x 25.
* Puede cargar archivos de vídeo de origen primarios de hasta 15 GB cada uno.

En la tabla siguiente se describe el tamaño recomendado, la proporción de aspecto y la velocidad de bits mínima que deben tener los archivos de vídeo de origen antes de codificarlos:

| Tamaño | Proporción de aspecto | Tasa de bits mínima |
|--- |--- |--- |
| 1024 X 768 | 4:3 | 4500 kbps para la mayoría de los vídeos. |
| 1280 X 720 | 16:9 | 3000 - 6000 kbps, dependiendo de la cantidad de movimiento en el vídeo. |
| 1920 X 1080 | 16:9 | 6000 - 8000 kbps, dependiendo de la cantidad de movimiento en el vídeo. |

### Obtener los metadatos de un archivo {#obtaining-a-file-s-metadata}

Puede obtener los metadatos de un archivo consultando sus metadatos con una herramienta de edición de vídeo o utilizando una aplicación diseñada para obtener metadatos. A continuación se indican las instrucciones para utilizar MediaInfo, una aplicación de terceros, para obtener los metadatos de un archivo de vídeo:

1. Vaya a [Descarga de MediaInfo](https://mediaarea.net/en/MediaInfo/Download).
1. Seleccione y descargue el instalador para la versión GUI, y siga las instrucciones de instalación.
1. Después de la instalación, haga clic con el botón derecho en el archivo de vídeo (solo Windows) y seleccione MediaInfo, o abra MediaInfo y arrastre el archivo de vídeo a la aplicación. Verá todos los metadatos asociados con el archivo de vídeo, incluida su anchura, altura y fps.

### Proporción de aspecto {#aspect-ratio}

Cuando elija o cree un ajuste preestablecido de codificación de vídeo para el archivo de vídeo de origen principal, asegúrese de que el ajuste preestablecido tenga la misma proporción de aspecto que el archivo de vídeo de origen principal. La relación de aspecto es la relación entre la anchura y la altura del vídeo.

Para determinar la relación de aspecto de un archivo de vídeo, obtenga los metadatos del archivo y tenga en cuenta la anchura y la altura del archivo (consulte Obtener los metadatos de un archivo más arriba). A continuación, utilice esta fórmula para determinar la relación de aspecto:

anchura/altura = relación de aspecto

En la tabla siguiente se describe cómo los resultados de la fórmula se traducen en opciones de relación de aspecto comunes:

| Resultado de la fórmula | Proporción de aspecto |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

Por ejemplo, un vídeo con una anchura de 1440 x una altura de 1080 tiene una relación de aspecto de 1440/1080 o 1,33. En este caso, se elige un ajuste preestablecido de codificación de vídeo con una relación de aspecto de 4:3 para codificar el archivo de vídeo.

### Velocidad de bits {#bitrate}

La velocidad de bits es la cantidad de datos que se codifican para formar un solo segundo de reproducción de vídeo. La velocidad de bits se mide en kilobits por segundo (Kbps).

>[!NOTE]
>
>Dado que todos los códecs utilizan compresión con pérdida, la velocidad de bits es el factor más importante en la calidad del vídeo. Con la compresión con pérdidas, cuanto más comprima un archivo de vídeo, más degradará la calidad. Por este motivo, si todas las demás características son iguales (resolución, velocidad de fotogramas y códec), menor es la velocidad de bits, menor es la calidad del archivo comprimido.

Al seleccionar una codificación de velocidad de bits, hay dos tipos que puede elegir:

* **[!UICONTROL Codificación de velocidad de bits constante]** (CBR): Durante la codificación CBR, la velocidad de bits o el número de bits por segundo se mantiene igual durante todo el proceso de codificación. La codificación CBR mantiene la velocidad de datos definida en su configuración en todo el vídeo. Además, la codificación CBR no optimiza los archivos multimedia para garantizar la calidad, pero sí ahorra espacio de almacenamiento.
Utilice CBR si el vídeo contiene un nivel de movimiento similar en todo el vídeo. CBR se utiliza generalmente para transmitir contenido de vídeo. Consulte también [Usar parámetros de codificación de vídeo personalizados](/help/assets/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL Codificación de velocidad de bits variable]** (VBR): La codificación VBR ajusta la velocidad de datos hacia abajo y hasta el límite superior establecido, según los datos requeridos por el compresor. Esta funcionalidad significa que durante un proceso de codificación VBR, la velocidad de bits del archivo multimedia aumenta o disminuye dinámicamente según las necesidades de velocidad de bits de los archivos multimedia.
El VBR tarda más en codificarse, pero produce los resultados más favorables; la calidad del archivo multimedia es superior. VBR se utiliza generalmente para el envío progresivo http de contenido de vídeo.

¿Cuándo utiliza VBR frente a CRB?
Al seleccionar VBR en comparación con CBR, casi siempre se recomienda usar VBR para los archivos multimedia. VBR proporciona archivos de mayor calidad a velocidades de bits competitivas. Cuando utilice VBR, asegúrese de utilizar con codificación de dos pasos y establezca que la velocidad de bits máxima sea 1,5 veces la velocidad de bits de vídeo de destino.

Cuando elija un ajuste preestablecido de codificación de vídeo, recuerde la velocidad de conexión del usuario final objetivo. Elija un ajuste preestablecido con una velocidad de datos del 80 % de esa velocidad. Por ejemplo, si la velocidad de conexión del usuario final objetivo es de 1000 Kbps, el mejor ajuste preestablecido es uno con una velocidad de datos de vídeo de 800 Kbps.

En esta tabla se describe la velocidad de datos de las velocidades de conexión típicas.

| Velocidad (Kbps) | Tipo de conexión |
|--- |--- |
| 256 | Conexión de acceso telefónico. |
| 800 | Conexión móvil típica. Para esta conexión, establezca como objetivo una velocidad de datos del rango de 400 a un máximo de 800 para las experiencias 3G. |
| 2000 | Conexión de escritorio de banda ancha típica. Para esta conexión, establezca como objetivo una velocidad de datos en el rango de 800 a 2000 Kbps, con la mayoría de objetivos que promedien entre 1200 y 1500 Kbps. |
| 5000 | Conexión de banda ancha típica. No se recomienda codificar en este rango superior porque la entrega de vídeo a esta velocidad no está disponible para la mayoría de los consumidores. |

### Resolución {#resolution}

**Resolución** describe la altura y anchura de un archivo de vídeo en píxeles. La mayoría de los vídeos de origen se almacenan a alta resolución (por ejemplo, 1920 x 1080). Para fines de transmisión, el vídeo de origen se comprime a una resolución más pequeña (640 x 480 o más pequeña).

La resolución y la velocidad de datos son dos factores integrados que determinan la calidad del vídeo. Para mantener la misma calidad de vídeo, cuanto mayor sea el número de píxeles en un archivo de vídeo (mayor es la resolución), mayor será la velocidad de datos. Por ejemplo, considere el número de píxeles por fotograma en una resolución de 320 x 240 y un archivo de vídeo de resolución de 640 x 480:

| Resolución | Píxeles por fotograma |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

El archivo de 640 x 480 tiene cuatro veces más píxeles por fotograma. Para lograr la misma velocidad de datos para estas dos resoluciones de ejemplo, se aplica cuatro veces la compresión al archivo de 640 x 480, lo que puede reducir la calidad del vídeo. Por lo tanto, una velocidad de datos de vídeo de 250 Kbps produce una visualización de alta calidad a una resolución de 320 x 240, pero no a una resolución de 640 x 480.

En general, cuanto mayor sea la velocidad de datos que utilice, mejor será el aspecto del vídeo y, cuanto mayor sea la resolución que utilice, mayor será la velocidad de datos que debe mantener la calidad de visualización (en comparación con resoluciones más bajas).

Como la resolución y la velocidad de datos están vinculadas, existen dos opciones al codificar vídeo:

* Elija una velocidad de datos y, a continuación, codifique con la resolución más alta que se muestre bien a la velocidad de datos elegida.
* Elija una resolución y, a continuación, codifique a la velocidad de datos necesaria para lograr vídeo de alta calidad en la resolución que elija.

Al elegir (o crear) un ajuste preestablecido de codificación de vídeo para el archivo de vídeo de origen principal, utilice esta tabla para dirigirse a la resolución correcta:

| Resolución | Altura (píxeles) | Tamaño de la pantalla |
|--- |--- |--- |
| 240p | 240 | Pantalla pequeña |
| 300p | 300 | Pantalla pequeña normalmente para dispositivos móviles |
| 360p | 360 | Pantalla pequeña |
| 480p | 480 | Pantalla media |
| 720p | 720 | Pantalla grande |
| 1080p | 1080 | Pantalla grande de alta definición |

### Fps (fotogramas por segundo) {#fps-frames-per-second}

En los Estados Unidos y Japón, la mayoría de los vídeos se graban a 29,97 fotogramas por segundo (fps); en Europa, la mayor parte del vídeo se toma a 25 fps. La película es filmada a 24 fps.

Elija un ajuste preestablecido de codificación de vídeo que coincida con la velocidad de fps del archivo de vídeo de origen principal. Por ejemplo, si el vídeo de origen principal es de 25 fps, elija un ajuste preestablecido de codificación con 25 fps. De forma predeterminada, toda la codificación personalizada utiliza el fps del archivo de vídeo de origen principal. Por este motivo, no es necesario especificar explícitamente la configuración de fps al crear un ajuste preestablecido de codificación de vídeo.

### Dimensiones de codificación de vídeo {#video-encoding-dimensions}

Para obtener resultados óptimos, seleccione dimensiones de codificación de modo que el vídeo de origen sea un múltiplo completo de todos los vídeos codificados.

Para calcular esta proporción, se divide el ancho de origen por el ancho codificado para obtener la relación de ancho. A continuación, se divide la altura de origen por la altura codificada para obtener la relación de altura.

Si la proporción resultante es un número entero, significa que el vídeo se escala de forma óptima. Si la proporción resultante no es un número entero, afecta a la calidad del vídeo dejando artefactos de píxeles sobrantes en la pantalla. Este efecto es más visible cuando el vídeo tiene texto.

Por ejemplo, suponga que el vídeo de origen es de 1920 x 1080. En la tabla siguiente, los tres vídeos codificados proporcionan la configuración de codificación óptima para su uso.

| Tipo de vídeo | Anchura x Altura | Proporción de anchura | Proporción de altura |
|--- |--- |--- |--- |
| Origen | 1920x1080 | 1 | 1 |
| Codificado | 960 x 540 | 2 | 2 |
| Codificado | 640 x 360 | 3 | 3 |
| Codificado | 480 x 270 | 4 | 4 |

### Formato de archivo de vídeo codificado {#encoded-video-file-format}

Dynamic Media recomienda utilizar ajustes preestablecidos de codificación de vídeo MP4 H.264. Dado que los archivos MP4 utilizan el códec de vídeo H.264, proporcionan vídeo de alta calidad pero en un tamaño de archivo comprimido.

### Habilitar DASH en su cuenta {#enable-dash}

DASH (Digital Adaptive Streaming over HTTP) es el estándar internacional para la transmisión de vídeo y se adopta ampliamente en los distintos visores de vídeo. Cuando DASH está habilitado en su cuenta, tiene la opción de elegir entre DASH o HLS para flujo de vídeo adaptable. O bien, puede optar por ambas con el cambio automático entre reproductores cuando **[!UICONTROL auto]** se selecciona como el tipo de reproducción en el ajuste preestablecido de visualizador.

Algunas de las ventajas clave de habilitar DASH en su cuenta son:

* Empaquete el vídeo de flujo DASH para el flujo de velocidad de bits adaptable. Este método conduce a una mayor eficacia de la entrega. El flujo adaptable garantiza la mejor experiencia de visualización para sus clientes.
* La transmisión optimizada para navegadores con reproductores Dynamic Media cambia entre el flujo HLS y el DASH para garantizar la mejor calidad del servicio. El reproductor de vídeo cambia automáticamente a HLS cuando se utiliza un explorador Safari.
* Puede configurar su método de flujo preferido (HLS o DASH) editando el ajuste preestablecido del visor de vídeo.
* La codificación de vídeo optimizada garantiza que no se utilice ningún almacenamiento adicional mientras se habilita la capacidad DASH. Se crea un único conjunto de codificaciones de vídeo para HLS y DASH a fin de optimizar los costes de almacenamiento de vídeo.
* Ayuda a que el envío de vídeo sea más accesible para sus clientes.
* Obtenga también la URL de flujo continuo mediante API.

   >[!IMPORTANT]
   >
   >Actualmente, habilitar DASH en su cuenta solo está disponible en Asia-Pacífico y Norteamérica; próximamente en Europa, Oriente Medio y África.

La activación de DASH en su cuenta requiere dos pasos:

* Configuración de Dynamic Media para utilizar DASH que puede hacer fácilmente.
* Configuración de Experience Manager 6.5 para utilizar DASH que se realiza mediante un caso de asistencia al cliente de Adobe que crea y envía.

**Para habilitar DASH en su cuenta:**

1. **Configuración de Dynamic Media** - En Dynamic Media en Experience Manager 6.5, vaya a [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Buscar **Transmisión avanzada de vídeo de AEM Assets Dynamic Media** indicador de función.
1. Seleccione la casilla de verificación para activar DASH.
1. Seleccione **[!UICONTROL Guardar]**.
1. **Configuración de Experience Manager 6.5** - [Utilice el Admin Console para iniciar la creación de un nuevo caso de asistencia](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html).
1. Siga las instrucciones para crear un caso de asistencia y, a la vez, proporcione la siguiente información:

   * Nombre de contacto principal, correo electrónico, teléfono.
   * Nombre de la cuenta de Dynamic Media.
   * Especifique que desea habilitar DASH en el Experience Manager 6.5.

1. El servicio de asistencia al cliente de Adobe le agrega a la lista de espera de clientes de DASH en función del orden en que se envían las solicitudes.
1. Cuando el Adobe está listo para gestionar su solicitud, el Servicio de atención al cliente se pone en contacto con usted para coordinar y establecer una fecha objetivo para la habilitación de DASH.
1. El Servicio de atención al cliente le notifica cuando haya terminado.
1. Cree su [ajuste preestablecido del visor de vídeo](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) como de costumbre.

## Ver informes de vídeo {#viewing-video-reports}

>[!NOTE]
>
>Los informes de vídeo solo están disponibles cuando se ejecuta Dynamic Media en modo híbrido.

Los informes de vídeo muestran varias métricas agregadas a lo largo de un tiempo específico para ayudarle a supervisar que *publicado* los vídeos individuales y agregados están teniendo el rendimiento que se esperaba. Los siguientes datos de métricas principales se agregan para todos los vídeos publicados en todo el sitio web:

* Inicios de vídeo
* Tasa de finalización
* Promedio de tiempo en vídeo
* Tiempo total en vídeo
* Vídeos por visita

Una tabla de todas *publicado* Los vídeos también se muestran para que pueda rastrear los vídeos más vistos del sitio web en función del número total de inicios de vídeo.

Al tocar un nombre de vídeo en la lista, se muestra el informe de retención de audiencia (desplegable) del vídeo en forma de gráfico de líneas. El gráfico muestra el número de vistas durante un momento determinado de la reproducción del vídeo. Cuando reproduce el vídeo, la barra vertical realiza el seguimiento en sincronización con el indicador de tiempo del reproductor. Las pérdidas en los datos del gráfico de líneas indican de dónde sale la audiencia del desinterés.

Si el vídeo se ha codificado fuera de Adobe Experience Manager Dynamic Media, el gráfico de retención de audiencia (desplegable) y los datos de Porcentaje de reproducción de la tabla no están disponibles.

Consulte también [Configuración de Cloud Services de Dynamic Media](/help/assets/config-dynamic.md).

>[!NOTE]
>
>El seguimiento y los informes de datos se basan exclusivamente en el uso del propio reproductor de vídeo de Dynamic Media y el ajuste preestablecido de reproductor de vídeo asociado. Como tal, no puede rastrear vídeos que se reproducen mediante otros reproductores de vídeo ni crear informes de ellos.

De forma predeterminada, la primera vez que se introduce Informes de vídeo, el informe muestra datos de vídeo a partir del primer mes del mes actual y termina con la fecha del mes actual. Sin embargo, puede anular el intervalo de fechas predeterminado especificando su propio intervalo de fechas. La próxima vez que introduzca Informes de vídeo, se utilizará el intervalo de fechas especificado.

Para que los informes de vídeo funcionen correctamente, se crea automáticamente un ID de grupo de informes cuando se configuran los Cloud Services de Dynamic Media. Al mismo tiempo, la ID del grupo de informes se envía al servidor de publicación, de modo que esté disponible para la función Copiar URL cuando se previsualizan los recursos. Sin embargo, esta funcionalidad requiere que el servidor de publicación ya esté configurado. Si el servidor de publicación no está configurado, aún puede publicar para ver el informe de vídeo. Sin embargo, debe volver a la Configuración de Dynamic Media Cloud y pulsar **[!UICONTROL OK]**.

**Para ver informes de vídeo:**

1. En la esquina superior izquierda del Experience Manager, pulse el logotipo del Experience Manager y, a continuación, en el carril izquierdo, pulse **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Recursos]** > **[!UICONTROL Informes de vídeo]**.
1. En la página Informes de vídeo , realice una de las acciones siguientes:

   * Cerca de la esquina superior derecha, toque la **Actualizar informe de vídeo** icono.
Utilice Actualizar solo si la fecha de finalización del informe es el día actual. Al hacerlo, se asegura de que vea el seguimiento de vídeo que se ha producido desde la última vez que ejecutó el informe.

   * Cerca de la esquina superior derecha, toque la **Selector de fechas** icono.
Especifique el intervalo de fechas de inicio y finalización para el que desee usar datos de vídeo y, a continuación, pulse **[!UICONTROL Ejecutar informe]**.

   El cuadro de grupo Métricas principales identifica varias medidas agregadas para todas las *publicado* vídeos en todo el sitio.

1. En la tabla que enumera los vídeos más publicados, pulse un nombre de vídeo para reproducir el vídeo y también consulte el informe de retención de audiencia (desplegable) del vídeo.

### Ver informes de vídeo basados en un visor de vídeo creado con el SDK de visor de Dynamic Media HTML5 {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

Si utiliza un visualizador de vídeo incorporado proporcionado por Dynamic Media o si ha creado un ajuste preestablecido de visualizador personalizado basado en un visualizador de vídeo incorporado, no se requiere ningún paso adicional para ver los informes de vídeo. Sin embargo, si ha creado su propio visor de vídeo basado en la API del SDK del visor de HTML5, siga los siguientes pasos para asegurarse de que el visor de vídeo envía eventos de seguimiento a los informes de vídeo de Dynamic Media.

Utilice la variable [Guía de referencia de visores de Dynamic Media de Adobe](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html) y [API del SDK del visor HTML5](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html) para crear sus propios visualizadores de vídeo.

**Para ver informes de vídeo basados en un visor de vídeo creado con el SDK de visor de Dynamic Media HTML5:**

1. Vaya a cualquier recurso de vídeo publicado.
1. Junto a la esquina superior izquierda de la página del recurso, en la lista desplegable, seleccione **[!UICONTROL Visualizadores]**.
1. Seleccione cualquier ajuste preestablecido de visualizador de vídeo y copie el código incrustado.
1. En el código incrustado, busque la línea con lo siguiente:

   `videoViewer.setParam("config2", "<value>");`

   La variable `config2` habilita el seguimiento en los visualizadores de HTML5. También es un ajuste preestablecido específico de la empresa que contiene la información de configuración para los informes de vídeo y para las configuraciones de Adobe Analytics específicas del cliente.

   El valor correcto del parámetro config2 se encuentra tanto en el **[!UICONTROL código incrustado]** como en la función de copia de **[!UICONTROL URL]**. En la URL del comando copiar **[!UICONTROL URL]**, el parámetro que se busca es `&config2=<value>`. El valor es casi siempre `companypreset`, pero en algunos casos también puede ser `companypreset-1`, `companypreset-2`, etc.

1. En el código personalizado del visor de vídeo, agregue AppMeasurementBridge .jsp a la página del visor haciendo lo siguiente:

   * En primer lugar, determine si necesita la variable `&preset` parámetro.

      Si la variable `config2` el parámetro es `companypreset`, usted *not* need `&preset=parameter`.

      If `config2` es cualquier otra cosa, establezca el parámetro preestablecido igual que la variable `config2` parámetro. Por ejemplo, si `config2=companypreset-2`, agregue `&param2=companypreset-2` a la URL de AppMeasumentBridge.jsp.

   * A continuación, agregue el script AppMeasurementBridge.jsp:

      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. Cree el componente TrackingManager haciendo lo siguiente:

   * Después de llamar a `s7sdk.Util.init();`, cree una instancia de TrackingManager para rastrear eventos agregando lo siguiente:

      `var trackingManager = new s7sdk.TrackingManager();`

   * Conecte componentes a TrackingManager haciendo lo siguiente:

      En el `s7sdk.Event.SDK_READY` controlador de eventos, adjunte el componente que desee rastrear al TrackingManager.

      Por ejemplo, si el componente es `videoPlayer`, agregue

      `trackingManager.attach(videoPlayer);`

      para adjuntar el componente al trackingManager. Para rastrear varios visualizadores en una página, utilice varios componentes del administrador de seguimiento.

   * Cree el objeto AppMeasurementBridge agregando lo siguiente:

      ```
      var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
      ```

   * Añada la función de seguimiento agregando lo siguiente:

      ```
      trackingManager.setCallback(appMeasurementBridge.track, 
       appMeasurementBridge);
      ```
   El objeto appMeasurementBridge tiene una función de seguimiento integrada. Sin embargo, puede proporcionar su propia compatibilidad con varios sistemas de seguimiento u otra funcionalidad.

<!--    For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

## Agregar subtítulos o subtítulos cerrados a un vídeo {#adding-captions-to-video}

Puede ampliar el alcance de sus vídeos a mercados globales añadiendo subtítulos a vídeos individuales o a conjuntos de vídeos adaptables. Al agregar subtítulos cerrados, evita la necesidad de doblar el audio, o la necesidad de usar hablantes nativos para volver a grabar el audio para cada idioma diferente. El vídeo se reproduce en el idioma en que se grabó. Aparecen subtítulos en idiomas extranjeros para que personas de diferentes idiomas puedan entender la parte de audio.

Los subtítulos también permiten una buena accesibilidad para las personas sordas o con dificultades auditivas.

>[!NOTE]
>
>El reproductor de vídeo que utilice debe admitir la visualización de subtítulos.

Consulte también [Accesibilidad en Dynamic Media](/help/assets/accessibility-dm.md).

Dynamic Media convierte los archivos de rótulos al formato JSON (JavaScript Object Notation). Esta conversión significa que puede incrustar el texto JSON en una página web como una transcripción oculta pero completa del vídeo. Los motores de búsqueda pueden rastrear e indexar el contenido para que los vídeos se puedan descubrir más fácilmente y proporcionar a los clientes detalles adicionales sobre el contenido del vídeo.

Consulte [Proporcionar contenido estático (no de imagen)](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html#image-serving-api) en el *Ayuda de la API de servicio y renderización de imágenes de Dynamic Media* para obtener más información sobre el uso de la función JSON en una URL.

**Para agregar subtítulos o subtítulos a un vídeo:**

1. Utilice una aplicación o servicio de terceros para crear el archivo de subtítulos o subtítulos de vídeo.

   Asegúrese de que el archivo que crea sigue el estándar WebVTT (Web Video Text Tracks). La extensión del nombre de archivo del rótulo es .vtt. Puede obtener más información sobre el estándar de subtítulos WebVTT.

   Consulte [WebVTT: Formato de seguimiento de texto de vídeo web](https://w3c.github.io/webvtt/).

   Existen herramientas y servicios gratuitos y premium que puede utilizar para crear archivos de subtítulos o subtítulos fuera de Dynamic Media. Por ejemplo, para crear un archivo de subtítulos de vídeo sencillo sin estilo, puede utilizar la siguiente herramienta gratuita de edición y creación de subtítulos en línea:

   [Creador de subtítulos WebVTT](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   Para obtener los mejores resultados, utilice la herramienta en Internet Explorer 9 o posterior, Google Chrome o Safari.

   En la herramienta, en la **[!UICONTROL Introducir URL del archivo de vídeo]** , pegue la dirección URL copiada del archivo de vídeo y, a continuación, haga clic en **[!UICONTROL Cargar]**. Consulte [Obtener una URL para un recurso](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) para obtener la URL del propio archivo de vídeo, que puede pegar en el **[!UICONTROL Introducir URL del campo de archivo de vídeo]**. Internet Explorer, Chrome o Safari pueden reproducir el vídeo de forma predeterminada.

   Ahora siga las instrucciones en pantalla del sitio para crear y guardar el archivo WebVTT. Cuando haya terminado, copie el contenido del archivo de rótulo y péguelo en un editor de texto sin formato y guárdelo con un `.vtt` extensión de nombre de archivo.

   >[!NOTE]
   >
   >Para la compatibilidad global con subtítulos de vídeo en varios idiomas, el estándar WebVTT requiere que cree archivos .vtt y llamadas independientes para cada idioma que desee admitir.

   Normalmente, le interesa asignar al archivo VTT de rótulo el mismo nombre que el archivo de vídeo y añadirlo a la configuración regional del idioma, como -EN, -FR o -DE. Al hacerlo, puede ayudarle a automatizar la generación de las URL de vídeo con su sistema de administración de contenido web existente.

1. En Experience Manager, cargue el archivo de subtítulos WebVTT en DAM.
1. Vaya a la *publicado* recurso de vídeo que desea asociar al archivo de rótulo que ha cargado.

   Recuerde que las direcciones URL solo están disponibles para copiarse *después* de *publicar* los recursos por primera vez.

   Consulte [Publicar recursos](/help/assets/publishing-dynamicmedia-assets.md).

1. Realice una de las siguientes acciones:

   * Para obtener una experiencia del visor de vídeo emergente, pulse **[!UICONTROL URL]**. En el cuadro de diálogo URL, seleccione y copie la dirección URL en el portapapeles y, a continuación, pase la dirección URL a un editor de texto sencillo. Añada la URL copiada del vídeo con la siguiente sintaxis:

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      Tenga en cuenta que `,1` al final de la ruta del rótulo. Inmediatamente después de la `.vtt` extensión de nombre de archivo en la ruta, si lo desea, puede activar o desactivar el botón de subtítulos en la barra del reproductor de vídeo configurándolo en `,1` o `,0`, respectivamente.

   * Para una experiencia de visor de vídeo incrustado, pulse **[!UICONTROL Código incrustado]**. En el cuadro de diálogo Código incrustado , seleccione y copie el código incrustado en el portapapeles y, a continuación, pegue el código en un editor de texto sencillo. Añada el código incrustado copiado con la siguiente sintaxis:

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      Tenga en cuenta que `,1` al final de la ruta del rótulo. Inmediatamente después de la `.vtt` extensión de nombre de archivo en la ruta, si lo desea, puede activar o desactivar el botón de subtítulos en la barra del reproductor de vídeo configurándolo en `,1` o `,0`, respectivamente.

## Agregar marcadores de capítulo a vídeo {#adding-chapter-markers-to-video}

Puede hacer que los vídeos de formulario largos sean más fáciles de ver y navegar añadiendo marcadores de capítulo a vídeos individuales o a conjuntos de vídeos adaptables. Cuando un usuario reproduce el vídeo, puede hacer clic en los marcadores de capítulo en la cronología del vídeo (también conocida como depurador de vídeo) para desplazarse fácilmente a su punto de interés. O bien, pueden ir de inmediato a contenido, demostraciones y tutoriales nuevos.

>[!NOTE]
>
>El reproductor de vídeo que se utilice debe admitir el uso de marcadores de capítulo. Los reproductores de vídeo de Dynamic Media admiten marcadores de capítulo, pero es posible que no utilicen reproductores de vídeo de terceros.

Si lo desea, puede crear y personalizar su propio visor de vídeo con capítulos en lugar de usar un ajuste preestablecido de visualizador de vídeo. Para obtener instrucciones sobre la creación de su propio visor de HTML5 con navegación por capítulos, en la API del SDK de visor de Adobe HTML5, consulte el encabezado &quot;Personalización del comportamiento mediante modificadores&quot; en las clases `s7sdk.video.VideoPlayer` y `s7sdk.video.VideoScrubber`. Consulte la [API del SDK del visor HTML5](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html) documentación.

<!-- If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

Puede crear una lista de capítulos para el vídeo de la misma manera que crea subtítulos. Es decir, se crea un archivo WebVTT. No obstante, tenga en cuenta que este archivo debe estar separado de cualquier archivo de subtítulos WebVTT que esté utilizando; no se pueden combinar subtítulos y capítulos en un archivo WebVTT.

Puede utilizar el siguiente ejemplo como ejemplo del formato que utiliza para crear un archivo WebVTT con navegación por capítulos:

### Archivo WebVTT con navegación por capítulos de vídeo {#webvtt-file-with-video-chapter-navigation}

```xml
WEBVTT
Chapter 1
00:00.000 --> 01:04.364
The bicycle store behind it all.
Chapter 2
01:04.364 --> 02:00.944
Creative Cloud.
Chapter 3
02:00.944 --> 03:02.937
Ease of management for a working solution.
Chapter 4
03:02.937 --> 03:35.000
Cost-efficient access to rapidly evolving technology.
```

En el ejemplo anterior, `Chapter 1` es el identificador de referencia y es opcional. El tiempo de referencia de `00:00:000 --> 01:04:364` especifica la hora de inicio y la hora de finalización del capítulo, en `00:00:000` formato. Los tres últimos dígitos son milisegundos y se pueden dejar como `000`, si se prefiere. El título del capítulo de `The bicycle store behind it all` es la descripción real del contenido del capítulo. El identificador de referencia, el tiempo de referencia de inicio y el título del capítulo aparecen en una ventana emergente del reproductor de vídeo cuando un usuario pasa el puntero del ratón sobre un punto de referencia visual en la cronología del vídeo.

Como está utilizando un visor de vídeo de HTML5, asegúrese de que el archivo de capítulo que cree sigue el estándar WebVTT (Web Video Text Tracks). La extensión del nombre del archivo del capítulo es `.vtt`. Puede obtener más información sobre el estándar de subtítulos WebVTT.

Consulte [WebVTT: Formato de seguimiento de texto de vídeo web](https://w3c.github.io/webvtt/)

**Para agregar navegación por capítulos de vídeo:**

1. Guarde el `.vtt` en la codificación UTF8 para evitar problemas con la representación de caracteres en el texto del título del capítulo.

   Normalmente, le interesa asignar al archivo VTT de capítulo el mismo nombre que el archivo de vídeo y anexarlo con capítulos. Al hacerlo, puede ayudarle a automatizar la generación de las URL de vídeo con su sistema de administración de contenido web existente.
1. En Experience Manager, cargue el archivo de capítulo WebVTT.

   Consulte [Carga de recursos](/help/assets/manage-assets.md#uploading-assets).

1. Realice una de las siguientes acciones:

   <table>
     <tbody>
      <tr>
       <td>Para una experiencia de visor de vídeo emergente</td>
       <td>
       <ol>
       <li>Vaya a la <i>publicado </i>recurso de vídeo que desea asociar al archivo de capítulo que ha cargado. Recuerde que las direcciones URL solo están disponibles para copiarse <i>después</i> de <i>publicar</i> los recursos por primera vez. Consulte <a href="/help/assets/publishing-dynamicmedia-assets.md">Publicación de recursos.</a></li>
       <li>En el menú desplegable, toque o haga clic en <strong>Visualizadores</strong>.</li>
       <li>En el carril izquierdo, toque o haga clic en el nombre del ajuste preestablecido del visualizador de vídeo. Se abre una vista previa del vídeo en una página independiente.</li>
       <li>En el carril izquierdo, en la parte inferior, haga clic en <strong>URL</strong>.</li>
       <li>En el cuadro de diálogo URL, seleccione y copie la dirección URL en el portapapeles y, a continuación, pase la dirección URL a un editor de texto sencillo.</li>
       <li>Añada la URL copiada del vídeo con la siguiente sintaxis para poder asociarla con la URL copiada al archivo de capítulo:<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>Para una experiencia de visor de vídeo incrustado<br /> </td>
       <td>
       <ol>
       <li>Vaya a la <i>publicado </i>recurso de vídeo que desea asociar al archivo de capítulo que ha cargado. Recuerde que las direcciones URL solo están disponibles para copiarse <i>después</i> de <i>publicar</i> los recursos por primera vez. Consulte <a href="/help/assets/publishing-dynamicmedia-assets.md">Publicación de recursos.</a></li>
       <li>En el menú desplegable, toque o haga clic en <strong>Visualizadores</strong>.</li>
       <li>En el carril izquierdo, toque o haga clic en el nombre del ajuste preestablecido del visualizador de vídeo. Se abre una vista previa del vídeo en una página independiente.</li>
       <li>En el carril izquierdo, en la parte inferior, haga clic en <strong>Incrustar</strong>.</li>
       <li>En el cuadro de diálogo Código incrustado, seleccione y copie todo el código en el Portapapeles y, a continuación, péguelo en un editor de texto sencillo.</li>
       <li>Añada el código incrustado del vídeo con la siguiente sintaxis para poder asociarlo a la URL copiada al archivo de capítulo:<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt&gt;"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

## Acerca de las miniaturas de vídeo en Dynamic Media: modo Scene7 {#about-video-thumbnails-in-dynamic-media-scene-mode}

Una miniatura de vídeo es una versión reducida de un fotograma de vídeo o un recurso de imagen que representa el vídeo al cliente. La miniatura sirve para animar a un cliente a hacer clic en el vídeo.

Todos los vídeos del Experience Manager deben tener una miniatura asociada; no puede eliminar una miniatura sin reemplazarla. De forma predeterminada, cuando se carga un vídeo en el Experience Manager, el primer fotograma se utiliza como miniatura. Sin embargo, puede personalizar la miniatura con fines de promoción de la marca o búsqueda visual, por ejemplo. Al personalizar una miniatura de vídeo, puede reproducir el vídeo y pausar el fotograma que desee utilizar. O bien, puede seleccionar un recurso de imagen que ya haya cargado y *publicado* en el administrador de recursos digitales.

Una imagen en miniatura de vídeo personalizada que seleccione en un vídeo no se extrae ni se guarda en DAM como un recurso independiente y distinto. Sin embargo, la miniatura de vídeo personalizada que seleccione en un recurso de imagen existente se guarda en el JCR. La ruta del recurso seleccionado se almacena en el nodo del recurso de vídeo como en la siguiente ruta de acceso de ejemplo:

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

La capacidad de personalizar una miniatura de vídeo solo está disponible después de haber aplicado un perfil de vídeo a la carpeta en la que se encuentra el vídeo.

Consulte también [Acerca de las miniaturas de vídeo en Dynamic Media: modo híbrido](#about-video-thumbnails-in-dynamic-media-hybrid-mode).

### Añadir una miniatura de vídeo personalizada {#adding-a-custom-video-thumbnail}

Estos pasos se aplican únicamente a Dynamic Media que se ejecuta en modo &quot;Dynamic Media_Scene7&quot;.

**Para agregar una miniatura de vídeo personalizada:**

1. Asegúrese de que ya ha hecho lo siguiente:

   * Se ha creado una carpeta para los recursos de vídeo.
   * [Aplicar un perfil de vídeo a la carpeta](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

   * [Se han cargado los vídeos en la carpeta](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

1. Vaya a un recurso de vídeo cargado cuya imagen en miniatura desee cambiar.
1. En el modo de selección de recursos, desde **[!UICONTROL Vista de lista]** o **[!UICONTROL Vista de tarjeta]**, pulse el recurso de vídeo.
1. En la barra de herramientas, pulse el botón **[!UICONTROL Propiedades]** (un círculo con una &quot;i&quot;).
1. En la página Propiedades del vídeo, pulse **[!UICONTROL Cambiar miniatura]**.
1. En la página Cambiar miniatura, realice una de las siguientes acciones:

   * Para utilizar un fotograma del vídeo como la nueva miniatura:

      * En la barra de herramientas, pulse **[!UICONTROL Seleccionar fotograma del vídeo]**.
      * Pulse el botón Reproducir y, a continuación, pulse el botón Pausa del fotograma que desee capturar como la nueva miniatura del vídeo.
   * Para utilizar un recurso de imagen como la nueva miniatura:

      * En la barra de herramientas, pulse **[!UICONTROL Seleccionar miniatura de recursos]**.
      * Toque **[!UICONTROL Seleccionar miniatura]**.
      * Vaya a un recurso de imagen previamente cargado y publicado que desee utilizar. El recurso se cambia de tamaño automáticamente para que sirva como imagen en miniatura para el vídeo.
      * Seleccione el recurso de imagen y, a continuación, pulse **[!UICONTROL Select]**.


1. En la página Cambiar miniatura , pulse **[!UICONTROL Guardar cambio]**.
1. En la página Propiedades del vídeo, en la esquina superior derecha, pulse **[!UICONTROL Guardar y cerrar]**.

## Acerca de las miniaturas de vídeo en Dynamic Media: modo híbrido {#about-video-thumbnails-in-dynamic-media-hybrid-mode}

Puede elegir entre una de las diez imágenes en miniatura generadas automáticamente por Dynamic Media para añadirlas al vídeo. El reproductor de vídeo muestra la miniatura seleccionada cuando se utiliza un recurso de vídeo con el componente Dynamic Media en el entorno de creación de Experience Manager Sites, Experience Manager Mobile o Experience Manager Screens. La miniatura sirve como imagen estática que representa mejor el contenido de todo el vídeo y además anima a los usuarios a hacer clic en el botón Reproducir .

En función del tiempo total del vídeo, Dynamic Media captura diez imágenes en miniatura (predeterminadas). Las imágenes se capturan al 1 %, 11 %, 21 %, 31 %, 41 %, 51 %, 61 %, 71 %, 81 % y 91 % en el vídeo. Las diez miniaturas persisten, lo que significa que si decide elegir una miniatura diferente más adelante, no es necesario volver a generar la serie. Obtenga una vista previa de las diez imágenes en miniatura y, a continuación, seleccione la que desee utilizar con el vídeo. Si desea cambiar al valor predeterminado, puede utilizar CRXDE Lite para configurar el intervalo de tiempo en el que se generan las imágenes en miniatura. Por ejemplo, si solo desea generar una serie de cuatro imágenes en miniatura con espaciado uniforme a partir del vídeo, puede configurar el tiempo de intervalo en 24 %, 49 %, 74 % y 99 %.

Lo ideal es agregar una miniatura de vídeo en cualquier momento después de cargar el vídeo, pero antes de publicar el vídeo en su sitio web.

Si lo prefiere, puede elegir cargar una miniatura personalizada para representar el vídeo en lugar de usar una miniatura generada por Dynamic Media. Por ejemplo, puede crear una imagen en miniatura personalizada que tenga el título del vídeo, una imagen de apertura llamativa o una imagen específica capturada del vídeo. La imagen en miniatura del vídeo personalizado que cargue debe tener una resolución máxima de 1280 x 720 píxeles (anchura mínima de 640 píxeles) y no debe superar los 2 MB.

Consulte también [Acerca de las miniaturas de vídeo en Dynamic Media: modo Scene7](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

### Adición de una miniatura de vídeo {#adding-a-video-thumbnail}

Estos pasos se aplican únicamente a Dynamic Media que se ejecuta en modo híbrido.

**Para agregar una miniatura de vídeo:**

1. Vaya a un recurso de vídeo cargado que quiera agregar una miniatura de vídeo.
1. En el modo de selección de recursos, ya sea en la vista de lista o en la vista de tarjeta, pulse el recurso de vídeo.
1. En la barra de herramientas, pulse el botón **[!UICONTROL Ver propiedades]** (un círculo con una &quot;i&quot;).
1. En la página Propiedades del vídeo, pulse **[!UICONTROL Cambiar miniatura]**.
1. En la página Cambiar miniatura, en la barra de herramientas, pulse **[!UICONTROL Seleccionar marco]**.

   Dynamic Media genera una serie de imágenes en miniatura a partir del vídeo, en función del intervalo de tiempo o intervalo de tiempo predeterminado que haya personalizado.

1. Previsualice las imágenes en miniatura generadas y, a continuación, seleccione la que desee agregar al vídeo.
1. Toque **[!UICONTROL Guardar cambio]**.

   La imagen en miniatura del vídeo se actualiza para usar la miniatura seleccionada. Si posteriormente decide cambiar la imagen en miniatura, puede volver a la **[!UICONTROL Cambiar miniatura]** y seleccione una nueva.

   Si ha configurado nuevos intervalos de tiempo predeterminados o ha cargado un nuevo vídeo para reemplazar el vídeo existente, haga que Dynamic Media vuelva a generar las miniaturas.

   Consulte [Configure el intervalo de tiempo predeterminado en el que se generan las miniaturas de vídeo](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

#### Configure el intervalo de tiempo predeterminado en el que se generan las miniaturas de vídeo {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

Cuando configura y guarda el nuevo intervalo de tiempo predeterminado, el cambio se aplica automáticamente solo a los vídeos que cargue en el futuro. No aplica automáticamente el nuevo valor predeterminado a los vídeos que ha cargado anteriormente. Para los vídeos existentes, debe volver a generar las miniaturas.

Consulte [Adición de una miniatura de vídeo](#adding-a-video-thumbnail).

**Para configurar el intervalo de tiempo predeterminado en el que se generan las miniaturas de vídeo:**

1. En el Experience Manager, pulse **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.

1. En la página CRXDE Lite, en el panel de directorio de la izquierda, vaya a `o etc/dam/imageserver/configuration/jcr:content/settings.`

   si el panel de directorio no está visible, pulse el icono >> a la izquierda de la pestaña Inicio .

1. En el panel inferior derecho, en la ficha Propiedades, pulse dos veces `thumbnailtime`.
1. En el **[!UICONTROL Editar tiempo de miniaturas]** , utilice los campos de texto para introducir valores de intervalo como porcentajes.

   * Pulse el icono de signo más (+) si desea añadir uno o varios campos de valor de intervalo. Si es necesario, desplácese hasta la parte inferior del cuadro de diálogo para ver el icono.
   * Pulse el icono de signo menos (-) a la derecha de un campo de valor de intervalo si desea eliminarlo de la lista.
   * Pulse el icono de flecha hacia arriba y el icono de flecha hacia abajo si desea reordenar los valores de intervalo.

1. Toque **[!UICONTROL OK]** y vuelva a la ficha Propiedades .
1. Cerca de la esquina superior izquierda de la página CRXDE Lite, pulse **[!UICONTROL Guardar todo]** y, a continuación, pulse el icono Volver a la página de inicio en la esquina superior izquierda para volver al Experience Manager.

   Consulte [Adición de una miniatura de vídeo](#adding-a-video-thumbnail).

### Añadir una miniatura de vídeo personalizada {#adding-a-custom-video-thumbnail-1}

Estos pasos se aplican únicamente a Dynamic Media que se ejecuta en modo híbrido.

**Para agregar una miniatura de vídeo personalizada:**

1. Vaya a un recurso de vídeo cargado que quiera agregar una miniatura de vídeo personalizada.
1. En el modo de selección de recursos, ya sea en la vista de lista o en la vista de tarjeta, pulse el recurso de vídeo.
1. En la barra de herramientas, pulse el botón **[!UICONTROL Ver propiedades]** (un círculo con una &quot;i&quot;).
1. En la página Propiedades del vídeo, pulse **[!UICONTROL Cambiar miniatura]**.
1. En la página Cambiar miniatura, en la barra de herramientas, pulse **[!UICONTROL Cargar nueva miniatura]**.
1. Vaya a la imagen en miniatura que desee usar, selecciónela y, a continuación, pulse **[!UICONTROL Apertura]** para empezar a cargar la imagen en el Experience Manager. Después de la carga, asegúrese de publicar la imagen.
1. Una vez que haya cargado y publicado correctamente la imagen, en la página Cambiar miniatura, pulse **[!UICONTROL Guardar cambios]**.

   La miniatura personalizada se añade al vídeo.

## Cambiar la URL de Dynamic Media para los recursos de Dynamic Media {#manifest-urls}

Los vídeos procesados en Dynamic Media se pueden utilizar mediante visores integrados, así como accediendo directamente a las direcciones URL de manifiesto y reproduciéndolos a través de sus propios visores personalizados. La siguiente es la API para recuperar direcciones URL de manifiesto para un vídeo.

### Acerca de la API getVideoManifestURI

La variable `getVideoManifestURI`La API se expone a través de c`q-scene7-api:com.day.cq.dam.scene7.api` y se pueden usar para generar las siguientes direcciones URL de manifiesto:

```java
/**   
* Returns the manifest url for videos 
* @param resource video resource 
* @param manifestType type of video streaming manifest being requested 
* @param onlyIfPublished return a manifest only if the video is published 
* @return the manifest url for videos 
* 
* @throws Exception 
*/
@Nullable 
String getVideoManifestURI(Resource resource, ManifestType manifestType, boolean onlyIfPublished) throws Exception;
```

#### Parámetros de API getVideoManifestURI

Esta API incorpora los tres parámetros siguientes:

| Parámetro | Descripción |
| --- | --- |
| `resource` | El recurso correspondiente al vídeo que Dynamic Media ha introducido. |
| `manifestType` | Puede: `ManifestType.DASH` o `ManifestType.HLS` |
| `onlyIfPublished` | Se establece en true en caso de que el uri de manifiesto se genere solo si se publica y está disponible en el nivel de entrega. |

Para recuperar las direcciones URL de manifiesto para vídeos con el método anterior, agregue una [perfil de codificación de vídeo](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) a una carpeta &quot;cargar vídeos&quot;. Dynamic Media procesa estos vídeos en función de las codificaciones que se encuentran en el archivo de codificación de vídeo asignado a la carpeta . Ahora puede invocar la API anterior para recuperar las URL de manifiesto de los vídeos cargados.

### Situaciones de error

La API devuelve nulo si hay errores. Las excepciones se registran en los registros de errores del Experience Manager. Todos estos errores registrados empiezan con `Could not generate Video Manifest URI`. Los siguientes escenarios pueden provocar estos errores:

* Un `IllegalArgumentException` se registra para cualquiera de los siguientes elementos:

   * La variable `resource` el parámetro pasado es nulo.
   * La variable `resource` parámetro pasado no es un vídeo.
   * La variable `manifestType` el parámetro pasado es nulo.
   * La variable `onlyIfPublished` se pasa como true, pero el vídeo no se publica.
   * El vídeo no se incorporó mediante un conjunto de vídeos adaptables de Dynamic Media.

* `IOException` se registra cuando hay un problema de conexión a Dynamic Media.
* `UnsupportedOperationException` se registra cuando una `manifestType` parámetro pasado es `ManifestType.DASH`, mientras que el vídeo no se ha procesado con formato DASH.

El siguiente es un ejemplo de la API anterior que utiliza servlets escritos en *Tablero blanco de TPWite* especificación. Seleccione cada pestaña para la sintaxis del código.

>[!BEGINTABS]

>[!TAB Añadir dependencia en pom.xml]

+++**Añadir dependencia en pom.xml**

```java
dependency> 
     <groupId>com.day.cq.dam</groupId> 
     <artifactId>cq-scene7-api</artifactId> 
     <version>5.12.64</version> 
     <scope>provided</scope> 
</dependency> 
```

+++

>[!TAB Servlet de ejemplo]

+++**Servlet de ejemplo**

```java
@Component
        service = Servlet.class 
) 
@HttpWhiteboardServletPattern(value = ManifestServlet.SERVLET_PATTERN) 
@HttpWhiteboardContextSelect(value = Constants.SERVLET_CONTEXT_SELECTOR) 
public class ManifestServlet extends HttpServlet { 

   private static final Logger LOGGER = LoggerFactory.getLogger(ManifestServlet.class); 

   private final ObjectMapper objectMapper; 

    @Reference 
    private Scene7Service scene7Service; 

   public static final String SERVLET_PATTERN = Constants.VIDEO_API_PREFIX + "/manifestUrl"; 

   public ManifestServlet() {
         this.objectMapper = new ObjectMapper(); 
         objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL); 
   }

   @Override 

   protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        final ResourceResolver resolver = getResourceResolver(request); 
        String assetPath = request.getParameter("assetPath"); 
        String manifest = request.getParameter("manifestType"); 
        String onlyIfPublished = request.getParameter("onlyIfPublished"); 
        Resource resource = resolver.getResource(assetPath); 
        response.setCharacterEncoding(StandardCharsets.UTF_8.toString()); 
        response.setContentType("application/json"); 
        if(resource == null) { 
            LOGGER.info("could not retrieve the resource from JCR"); 
            error("could not retrieve the resource from JCR", response); 
            return; 
        }

        String manifestUri = null; 

        try{ 
            ManifestType manifestType =  ManifestType.DASH; 
            if(manifest != null) { 
                manifestType = ManifestType.valueOf(manifest); 
            } 
            manifestUri = scene7Service.getVideoManifestURI(resource, manifestType, onlyIfPublished != null); 
            objectMapper.writeValue(response.getWriter(), new ManifestUrl(manifestUri)); 
            response.setContentType("application/json"); 
        } catch (Exception e) { 
            LOGGER.error(e.getMessage(), e); 
            error(String.format("Unable to get the manifest url for %s. %s", assetPath, e.getMessage()), response); 
        } 
    } 

    private ResourceResolver getResourceResolver(HttpServletRequest request) { 
        Object rr = request.getAttribute(AuthenticationSupport.REQUEST_ATTRIBUTE_RESOLVER); 
        if (!(rr instanceof ResourceResolver)) { 
            throw new IllegalStateException( 
                    "The request does not seem to have been created via Apache Sling's authentication mechanism."); 
        } else { 
            return (ResourceResolver) rr; 
        } 
    } 

    private void error(String errorMessage, HttpServletResponse response) throws IOException { 
        ManifestUrl errorManifest = new ManifestUrl(null); 
        errorManifest.setErrorMessage(errorMessage); 
        response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR); 
        objectMapper.writeValue(response.getWriter(), errorManifest); 
    } 
} 
```

+++

>[!TAB Clase de respuesta para servlet]

+++**Clase de respuesta para servlet**

```java
public class ManifestUrl extends VideoResponse { 
     String manifestUrl; 
     public ManifestUrl(String manifestUrl) { 
         this.manifestUrl = manifestUrl; 
     } 
     public String getManifestUrl() { 
         return manifestUrl; 
     } 
} 

public abstract class VideoResponse { 
     String errorString; 

     public String getErrorString() { 
         return errorString; 
     } 

     public void setErrorMessage(String errorString) { 
         this.errorString = errorString; 
     } 
} 
```

+++

>[!TAB Archivo de constantes al que se hace referencia en el servlet]

+++**Archivo de constantes al que se hace referencia en el servlet**

```java
public final class Constants { 

     private Constants() { 
     } 

     public static final String VIDEO_API_PREFIX = "/dynamicmedia/video"; 
     public static final String SERVLET_CONTEXT_SELECTOR = "(" + HttpWhiteboardConstants.HTTP_WHITEBOARD_CONTEXT_NAME + "=" + 
             DMSampleApiHttpContext.CONTEXT_NAME + ")"; 

 } 
```

+++

>[!TAB ServletContext]

+++**ServletContext**

Monte el servlet anterior utilizando un `servletContext`. El siguiente es un ejemplo de `servletContext`.

```java
public class DMSampleApiHttpContext extends ServletContextHelper { 

 public static final String CONTEXT_NAME = "com.adobe.dmSample"; 
 public static final String CONTEXT_PATH = "/dmSample"; 

 private final MimeTypeService mimeTypeService; 

 private final AuthenticationSupport authenticationSupport; 

 /** 
  * Constructs a new context that will use the given dependencies. 
  * 
  * @param mimeTypeService Used when providing mime type of requests. 
  * @param authenticationSupport Used to authenticate requests with sling. 
  */ 
 @Activate 
 public DMSampleApiHttpContext(@Reference final MimeTypeService mimeTypeService, 
                               @Reference final AuthenticationSupport authenticationSupport) { 
     this.mimeTypeService = mimeTypeService; 
     this.authenticationSupport = authenticationSupport; 
 } 

 // ---------- HttpContext interface ---------------------------------------- 
 /** 
  * Returns the MIME type as resolved by the <code>MimeTypeService</code> or 
  * <code>null</code> if the service is not available. 
  */ 
 @Override 
 public String getMimeType(String name) { 
     MimeTypeService mtservice = mimeTypeService; 
     if (mtservice != null) { 
         return mtservice.getMimeType(name); 
     } 
     return null; 
 } 

 /** 
  * Returns the real context path that is used to mount this context. 
  * @param req servlet request 
  * @return the context path 
  */ 
 public static String getRealContextPath(HttpServletRequest req) { 
     final String path = req.getContextPath(); 
     if (path.equals(CONTEXT_PATH)) { 
         return ""; 
     } 
     return path.substring(CONTEXT_PATH.length()); 
 } 

 /** 
  * Returns a request wrapper that transforms the context path back to the original one 
  * @param req request 
  * @return the request wrapper 
  */ 
 public static HttpServletRequest createContextPathAdapterRequest(HttpServletRequest req) { 
     return new HttpServletRequestWrapper(req) { 

         @Override 
         public String getContextPath() { 
             return getRealContextPath((HttpServletRequest) getRequest()); 
         } 

     }; 

 } 

 /** 
  * Always returns <code>null</code> because resources are all provided 
  * through individual endpoint implementations. 
  */ 
 @Override 
 public URL getResource(String name) { 
     return null; 
 } 

 /** 
  * Tries to authenticate the request using the 
  * <code>SlingAuthenticator</code>. If the authenticator or the Repository 
  * is missing this method returns <code>false</code> and sends a 503/SERVICE 
  * UNAVAILABLE status back to the client. 
  */ 
 @Override 
 public boolean handleSecurity(HttpServletRequest request, 
                               HttpServletResponse response) throws IOException { 

     final AuthenticationSupport authenticator = this.authenticationSupport; 
     if (authenticator != null) { 
         return authenticator.handleSecurity(createContextPathAdapterRequest(request), response); 
     } 

     // send 503/SERVICE UNAVAILABLE, flush to ensure delivery 
     response.sendError(HttpServletResponse.SC_SERVICE_UNAVAILABLE, 
             "AuthenticationSupport service missing. Cannot authenticate request."); 
     response.flushBuffer(); 

     // terminate this request now 
     return false; 
 } 
}
```

+++

>[!ENDTABS]

### Uso del servlet de ejemplo

Para invocar el servlet, realice una `GET` operación en `/dmSample/dynamicmedia/video/manifestUrl`. Se pasan los siguientes parámetros de consulta:

| Parámetro de consulta | Descripción |
| --- | --- |
| `assetPath` | Obligatorio. La ruta al vídeo para la que `manifestUrl` se genera. |
| `manifestType` | Opcional. El parámetro puede ser DASH o HLS. Si no se pasa, el valor predeterminado es DASH. |
| `onlyIfPublished` | Opcional. Si se pasa, la variable `manifestUrl` solo se devuelve si se publica el vídeo. |

En este ejemplo, supongamos la siguiente configuración:

* La empresa es `samplecompany`.
* La instancia de creación es `http://sample-aem-author.com`.
* La carpeta `/content/dam/video-example` tiene un perfil de codificación de vídeo aplicado.
* El vídeo `scenery.mp4` se carga en la carpeta `/content/dam/video-example`.

Puede invocar el servlet de las siguientes maneras:

| Tipo | Descripción |
| :--- | --- |
| HLS | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=HLS&assetPath=/content/dam/video-example/scenery.mp4`<br><br>En caso de que el envío DASH esté habilitado:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8?packagedStreaming=true"}`<br><br>En caso de que el envío DASH esté desactivado:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8"}` |
| DASH | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scenery.mp4`<br><br>En caso de que el envío DASH esté habilitado:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.mpd"}`<br><br>En caso de que el envío DASH esté desactivado:<br>`{}` |
| Error: la ruta de acceso del recurso es incorrecta | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scennnnnnery.mp4`<br><br>`{"errorString":"could not retrieve the resource from JCR"}` |


