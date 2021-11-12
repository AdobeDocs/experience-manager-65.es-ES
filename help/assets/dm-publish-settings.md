---
title: Configuración de Dynamic Media Publish
description: Obtenga información sobre cómo configurar la publicación en Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
hide: true
hidefromtoc: true
exl-id: null
source-git-commit: 1985058faa2a85a4544b35f2a6925670207df9e1
workflow-type: tm+mt
source-wordcount: '3114'
ht-degree: 2%

---


# Configuración de Dynamic Media Publish

>[!IMPORTANT]
>
>La configuración de Dynamic Media Publish solo está disponible si:
>
>* Está ejecutando Dynamic Media en modo Scene7.
>* Tiene un *existente* **[!UICONTROL Configuración de Dynamic Media]** (en **[!UICONTROL Cloud Services]**) en Adobe Experience Manager 6.5 o en Experience Manager as a Cloud Service.
>* Es administrador del sistema del Experience Manager con privilegios de administrador.


La configuración de la página Configuración de publicación de Dynamic Media determina cómo se envían los recursos de forma predeterminada desde los servidores Dynamic Media de Adobe a los sitios web o las aplicaciones. Si no se especifica ninguna configuración, el servidor Dynamic Media de Adobe envía un recurso de acuerdo con la configuración predeterminada de una página de configuración de publicación. Por ejemplo, una solicitud para enviar una imagen que no incluya un atributo de resolución genera una imagen con la configuración Resolución de objeto predeterminada en la página Servidor de imágenes.

Los administradores pueden cambiar la configuración predeterminada de las páginas Servidor de imágenes, Procesador de imágenes y viñeta para establecer la configuración predeterminada para enviar recursos desde servidores.

>[!NOTE]
>
>La configuración de publicación de Dynamic Media está diseñada para que la utilicen desarrolladores y programadores experimentados de sitios web. Adobe Dynamic Media supone que los usuarios que cambian cualquiera de estos ajustes de publicación predeterminados están familiarizados con Dynamic Media de Adobe, las normas y convenciones de protocolo HTTP y la tecnología básica de creación de imágenes.

**Para configurar la configuración de publicación de Dynamic Media:**

1. En el modo Autor del Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global.
1. En el carril izquierdo, seleccione el icono Herramientas y, a continuación, vaya a **[!UICONTROL Recursos]** > **[!UICONTROL Configuración de Dynamic Media Publish]**.
1. En la página Servidor de imágenes , establezca el contexto de publicación de Image Server y, a continuación, utilice las cinco pestañas para configurar los ajustes de publicación predeterminados.

   * [Servidor de imágenes](#image-server)
   * [Seguridad](#security-tab) ficha
   * [Administración de catálogos](#catalog-management-tab) ficha
   * [Atributos de solicitud](#request-attributes-tab) ficha
   * [Atributos de miniatura comunes](#common-thumbnail-attributes-tab) ficha
   * [Atributos de gestión de color](#color-management-attributes-tab) ficha

   ![Página Configuración de publicación de Dynamic Media](/help/assets/assets-dm/dm-publish-setup.png)
   *Configuración de publicación de Dynamic Media , con la variable **[!UICONTROL Atributos de solicitud]**seleccionada.*<br><br>

1. Cuando haya terminado, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]**.

## Servidor de imágenes {#image-server}

La página Servidor de imágenes establece la configuración predeterminada para enviar imágenes desde los servidores de imágenes. La configuración está disponible en cinco categorías

| Contexto de publicación | Descripción |
| --- | --- |
| Servicio de imágenes | Especifica el contexto para la configuración de publicación. |
| Probar servicio de imágenes | Especifica el contexto para probar la configuración de publicación.<br>Consulte [Probar recursos antes de hacerlos públicos](#test-assets-before-making-public). |

### Ficha Seguridad {#security-tab}

**[!UICONTROL Dirección del cliente]** - Permite especificar una o más direcciones IP o intervalos de direcciones IP. Cuando se especifica, se rechazan las solicitudes a este catálogo de imágenes que se originan en un cliente con una dirección IP no incluida en la lista. Esta regla se aplica tanto a la entrega de imágenes como a las imágenes procesadas.

### Ficha Administración del catálogo {#catalog-management-tab}

**[!UICONTROL Ruta del archivo de definición del conjunto de reglas]** - Especifica el archivo que contiene las definiciones del conjunto de reglas para el catálogo de imágenes.

Consulte también [RuleSetFile](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) en la Guía de referencia de visores de Dynamic Media.

### Ficha Atributos de solicitud {#request-attributes-tab}

Estos ajustes pertenecen al aspecto predeterminado de las imágenes.

| Configuración | Descripción |
| --- | --- |
| **[!UICONTROL Límite de tamaño de la imagen de respuesta]** | Requerido.<br>Especifica el ancho y el alto máximo de la imagen de respuesta que se devuelve al cliente. El servidor devuelve un error si una solicitud produce una imagen de respuesta cuya anchura, altura o ambas dimensiones sean superiores a esta configuración.<br>Consulte también [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Modo de ofuscación de solicitud]** | Habilitar si desea aplicar codificación base64 a solicitudes válidas.<br>Consulte también [RequestObfuscation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Modo de bloqueo de solicitud]** | Habilitar si desea un simple bloqueo hash incluido en las solicitudes.<br>Consulte también [RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Atributos de solicitud predeterminados]** |  |
| **[!UICONTROL Sufijo de archivo de imagen predeterminado]** | Requerido.<br>Extensión de archivo de datos predeterminada que se anexa a los valores de campo Ruta del catálogo y RutaDeMáscara si la ruta no incluye un sufijo de archivo.<br>Consulte también [DefaultExt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Nombre de fuente predeterminada]** | Especifica qué fuente se utiliza si una solicitud de capa de texto no proporciona ninguna fuente. Si se especifica, debe ser un valor de nombre de fuente válido en el mapa de fuentes de este catálogo de imágenes o en el mapa de fuentes del catálogo predeterminado.<br>Consulte también [DefaultFont](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Imagen predeterminada]** | Proporciona una imagen predeterminada para devolver en respuesta a una solicitud en la que no se encuentra la imagen solicitada.<br>Consulte también [DefaultImage](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Modo de imagen predeterminado]** | Cuando el cuadro deslizante está activado (control deslizante a la derecha), la variable **[!UICONTROL Imagen predeterminada]** reemplaza cada capa que falta en la imagen de origen por la imagen predeterminada y devuelve el compuesto como de costumbre. Cuando el cuadro deslizante está desactivado (deslizador a la izquierda), la imagen predeterminada reemplaza a la imagen compuesta completa, aunque la imagen que falta sea una de varias capas.<br>Consulte también [DefaultImageMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Tamaño de vista predeterminado]** | Requerido.<br>El servidor restringe el tamaño de las imágenes de respuesta para que no supere esta anchura y altura si la solicitud no especifica el tamaño de vista de forma explícita mediante `wid=`, `hei=`o `scl=`.<br>Consulte también [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Tamaño de miniatura predeterminado]** | Requerido.<br>Se utiliza en lugar del atributo **[!UICONTROL Tamaño de vista predeterminado]** para solicitudes de miniaturas (`req=tmb`). El servidor restringe el tamaño de las imágenes de respuesta para que no superen esta anchura y altura, si se solicita una miniatura (`req=tmb`) no especifica el tamaño utilizando `wid=`, `hei=`o `scl=`.<br>Consulte también [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Color de fondo predeterminado]** | Especifica el valor del RGB utilizado para rellenar cualquier área de una imagen de respuesta que no contenga datos de imagen reales.<br>Consulte también [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Atributos de codificación JPEG]** |  |
| **[!UICONTROL Calidad]** | Especifica los atributos predeterminados para las imágenes de respuesta del JPEG. La variable **[!UICONTROL Calidad]** se define en el rango de 1 a 100.<br>Consulte también [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Disminución de resolución de cromaticidad]** | Activar o desactivar el muestreo descendente cromático empleado por los codificadores JPEG. |
| **[!UICONTROL Modo de remuestreo predeterminado]** | Especifica los atributos de remuestreo e interpolación predeterminados que se utilizarán para escalar datos de imagen. Usar cuando `resMode` no se ha especificado en una solicitud.<br>Consulte también [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) en la Guía de referencia de visores de Dynamic Media. |

### Ficha Atributos de miniatura comunes {#common-thumbnail-attributes-tab}

Estos ajustes pertenecen al aspecto y la alineación predeterminados de las imágenes en miniatura.

| Configuración | Descripción |
| --- | --- |
| **[!UICONTROL Color de fondo predeterminado para miniatura]** | Especifica el valor del RGB utilizado para rellenar el área de una imagen en miniatura de salida que no contiene datos de imagen reales. Solo se usa para solicitudes de miniaturas (`req=tmb`) y cuándo **[!UICONTROL Tipo de miniatura predeterminado]** está configurada en **[!UICONTROL Ajustar]** o **[!UICONTROL Textura]**.<br>Consulte también [ThumbBkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Alineación horizontal]** | Especifica la alineación horizontal de la imagen en miniatura en el rectángulo de imagen de respuesta especificado por `wid=` y `hei=` valores.<br>Solo se usa para solicitudes de miniaturas (`req=tmb`) y cuándo **[!UICONTROL Tipo de miniatura predeterminado]** está configurada en **[!UICONTROL Ajustar]**.<br>Hay tres alineaciones horizontales entre las que elegir: **[!UICONTROL Alineación central]**, **[!UICONTROL Alineación izquierda]** y **[!UICONTROL Alineación derecha]**.<br>Consulte también [ThumbHorizAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Alineación vertical]** | Especifica la alineación vertical de la imagen en miniatura en el rectángulo de imagen de respuesta especificado por `wid=` y `hei=` valores. Solo se usa para solicitudes de miniaturas (`req=tmb`) y cuándo **[!UICONTROL Tipo de miniatura predeterminado]** está configurada en **[!UICONTROL Ajustar]**.<br>Hay tres alineaciones verticales para elegir: **[!UICONTROL Alineación superior]**, **[!UICONTROL Alineación central]** y **[!UICONTROL Alineación inferior]**.<br>Consulte también [ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Duración predeterminada de la caché]** | Proporciona un intervalo de caducidad predeterminado en horas en caso de que un registro de catálogo en particular no contenga un valor de caducidad de catálogo válido. Establecer como `-1` para marcar como nunca caduca. <br>Consulte también [Caducidad](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Tipo de miniatura predeterminado]** | Proporciona un valor predeterminado para el tipo de miniatura en caso de que un registro de catálogo en particular no contenga un valor de catálogo ThumbType válido. Solo se usa para solicitudes de miniaturas (`req=tmb`).<br>Hay tres tipos de miniaturas entre los que elegir: **[!UICONTROL Recortar]**, **[!UICONTROL Ajustar]** y **[!UICONTROL Textura]**.<br>Consulte también [ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Resolución de miniatura predeterminada]** | Proporciona un valor predeterminado para la resolución del objeto de miniatura en caso de que un registro de catálogo concreto no contenga un valor de catálogo ThumbRes válido. Solo se usa para solicitudes de miniaturas (`req=tmb`) y cuando la variable **[!UICONTROL Tipo de miniatura predeterminado]** está configurada en **[!UICONTROL Textura]**.<br>Consulte también [ThumbRes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) en la Guía de referencia de visores de Dynamic Media. |

### Ficha Atributos de administración de color {#color-management-attributes-tab}

Estos ajustes determinan qué perfiles de color ICC se utilizan para las imágenes.

**Interpretación de la conversión de color**
Una interpretación de conversión de color permite anular la interpretación predeterminada de los perfiles de trabajo para determinar cómo se ajustan los colores de origen. Se usa cuando:

1. Uno de los perfiles ICC predeterminados es el espacio de color de destino de una conversión de color.
1. Un dispositivo de salida (impresora o monitor) se caracteriza por este perfil.
1. Además, la interpretación especificada es válida para este perfil.

Las distintas intenciones de renderización utilizan reglas diferentes para determinar cómo se ajustan los colores de origen.

Consulte también [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) en la Guía de referencia de visores de Dynamic Media.

>[!NOTE]
>
>En general, es mejor utilizar la interpretación predeterminada para la configuración de color seleccionada, que ha sido probada por Adobe para cumplir los estándares del sector. Por ejemplo, si elige una configuración de color para Norteamérica o Europa, la interpretación de conversión de color predeterminada es **[!UICONTROL Colormétrica relativa]**. Si elige una configuración de color para Japón, la interpretación de conversión de color predeterminada es **[!UICONTROL Percepción]**.

| Configuración | Características |
| --- | --- |
| **[!UICONTROL Espacio de color predeterminado CMYK]** | Especifica el nombre del perfil de color ICC que se utilizará como perfil de trabajo para los datos CMYK. If **[!UICONTROL Ninguno especificado]** se elige, la gestión de color se desactiva para este catálogo de imágenes cuando están involucradas las imágenes de origen CMYK. Todos los espacios de trabajo CMYK dependen del dispositivo, lo que significa que se basan en combinaciones reales de tinta y papel. Los materiales de Adobe para espacios de trabajo CMYK se basan en condiciones estándar de impresión comercial.<br> Consulte también [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Espacio de color predeterminado de escala de grises]** | Especifica el nombre del perfil de color ICC que se utilizará como perfil de trabajo para los datos de escala de grises. If **[!UICONTROL Ninguno especificado]** se elige, la gestión de color se desactiva para este catálogo de imágenes cuando están implicadas imágenes de origen en escala de grises.<br>Consulte también [IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Espacio de color predeterminado del RGB]** | Especifica el nombre del perfil de color ICC que se utilizará como perfil de trabajo para los datos del RGB. If **[!UICONTROL Ninguno especificado]** se elige, la gestión de color se desactiva para este catálogo de imágenes cuando están involucradas las imágenes de fuentes RGB. En general, es mejor elegir **[!UICONTROL Adobe RGB]** o **[!UICONTROL sRGB]**, en lugar del perfil de un dispositivo específico (como un perfil de monitor). **[!UICONTROL sRGB]** se recomienda cuando prepare imágenes para la web o dispositivos móviles, ya que define el espacio de color del monitor estándar utilizado para ver imágenes en la web. **[!UICONTROL sRGB]** también es una buena opción cuando se trabaja con imágenes de cámaras digitales de consumo, ya que la mayoría de estas cámaras utilizan sRGB como espacio de color predeterminado.<br>Consulte también [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Interpretación de la conversión de color]** | **[!UICONTROL Percepción]** - Su objetivo es preservar la relación visual entre los colores para que se perciba como natural para el ojo humano, aunque los valores de color en sí mismos puedan cambiar. Esta intención es adecuada para imágenes fotográficas con muchos colores fuera de gama. Este ajuste es la interpretación estándar para la industria de impresión japonesa. |
|  | **[!UICONTROL Colorimétrico relativo]** - Compara el resaltado extremo del espacio de color de origen con el del espacio de color de destino y cambia todos los colores según corresponda. Los colores fuera de gama se desplazan al color reproducible más cercano en el espacio de color de destino. Colorimétrico relativo conserva más de los colores originales en una imagen que Perceptual. Este ajuste es la interpretación estándar para impresión en Norteamérica y Europa. |
|  | **[!UICONTROL Saturación]** - Trata de producir colores vivos en una imagen a expensas de la precisión del color. Esta interpretación es adecuada para gráficos empresariales, como gráficos o gráficos, en los que los colores saturados brillantes son más importantes que la relación exacta entre los colores. |
|  | **[!UICONTROL Colorimétrico absoluto]** - Deja sin cambios los colores que entran dentro de la gama de destino. Los colores fuera de gama se recortan. No se aplica ninguna escala de colores a los puntos blancos de destino. Esta intención es mantener la precisión del color a expensas de preservar las relaciones entre los colores y es adecuada para pruebas para simular la salida de un dispositivo en particular. Esta intención es útil para previsualizar cómo el color del papel afecta a los colores impresos. |

## Probar recursos antes de hacerlos públicos {#test-assets-before-making-public}

Secure Testing le ayuda a definir un entorno de prueba seguro y a crear una solución empresarial a empresa sólida, basada en un conjunto configurable de direcciones IP e intervalos. Esta funcionalidad le permite hacer coincidir las implementaciones de Dynamic Media de Adobe con la arquitectura de su sistema empresarial y de administración de contenido.

Con Secure Testing, puede obtener una vista previa de la versión de ensayo del sitio web con contenido no publicado.

Si lo desea, cree un entorno de ensayo en lugar de publicar los recursos por los siguientes motivos:

* Previsualizar sitios web antes del lanzamiento público (sitio web de ensayo).
* Proporcione recursos que requieran acceso restringido, como catálogos electrónicos que muestren precios en una aplicación web B2B.
* Utilice los recursos detrás de un cortafuegos como parte del sistema de administración de la información del producto, la aplicación de servicio al cliente, el sitio de formación, etc.

>[!NOTE]
>
>Secure Testing no afecta al acceso a Adobe Dynamic Media Classic. La seguridad de Adobe Dynamic Media Classic sigue siendo coherente y requiere las credenciales habituales para acceder a Adobe Dynamic Media Classic y a los servicios web relacionados.

### Funcionamiento de Secure Testing {#how-test-assets-works}

La mayoría de las corporaciones ejecutan Internet detrás de un cortafuegos. El acceso a Internet es posible a través de ciertas rutas y, por lo general, a través de una gama limitada de direcciones IP públicas.

Desde su red corporativa, puede averiguar su dirección IP pública utilizando sitios web como [https://www.whatismyip.com](https://www.whatismyip.com/) o solicite esta información a su organización de TI corporativa.

Con Secure Testing, Adobe Dynamic Media crea un servidor de imágenes dedicado para entornos de ensayo o aplicaciones internas. Cualquier solicitud a este servidor comprueba la dirección IP de origen. Si la solicitud entrante no está dentro de la lista aprobada de direcciones IP, se devuelve una respuesta de error. El administrador de la empresa de Dynamic Media de Adobe configura la lista aprobada de direcciones IP para el entorno Secure Testing de su empresa.

Como se debe confirmar la ubicación de la solicitud original, el tráfico del servicio Secure Testing no se enruta a través de una red de distribución de contenido como el tráfico público del servidor de imágenes de Dynamic Media. Las solicitudes al servicio Secure Testing tienen una latencia ligeramente mayor que los servidores públicos de imágenes de Dynamic Media.

Los recursos no publicados están disponibles inmediatamente desde los servicios Secure Testing, sin necesidad de publicarlos. De este modo, puede ejecutar una vista previa antes de publicar los recursos en su servidor de imágenes público.

>[!NOTE]
>
>Los servicios de Secure Testing utilizan el servidor de catálogo configurado con un contexto de publicación interno. Por lo tanto, si su empresa está configurada para publicar en Secure Testing, cualquier recurso cargado en Adobe Dynamic Media estará disponible inmediatamente en los servicios de Secure Testing. Esta funcionalidad es verdadera independientemente de si los recursos están marcados para publicarse en la carga.

Los servicios de Secure Testing admiten actualmente los siguientes tipos de activos y funcionalidades:

* Imágenes.
* Viñetas (Procesar solicitudes del servidor).
* Procesar solicitudes de servidor (admitidas, pero el cliente debe solicitarlas explícitamente).
* Conjuntos, incluidos conjuntos de imágenes, catálogos electrónicos, conjuntos de representación y conjuntos de medios.
* Visores de medios enriquecidos de Dynamic Media de Adobe estándar.
* Adobe de páginas JSP de Dynamic Media OnDemand.
* Contenido estático, como archivos PDF y vídeos servidos de forma progresiva.
* Flujo continuo de vídeo HTTP.
* Flujo continuo de vídeo progresivo.

Actualmente no se admiten los siguientes tipos de recursos y funcionalidades:

* Búsqueda de información o catálogo electrónico de Adobe Dynamic Media Classic
* Flujo de vídeo RTMP
* Impresión virtual
* Servicios UGC (contenido generado por el usuario)

>[!IMPORTANT]
>
>La compatibilidad con recursos de imagen vectoriales UGC nuevos o existentes en Adobe Dynamic Media finalizó el 30 de septiembre de 2021.

### Probar el servicio Secure Testing {#test-secure-testing-service}

Para asegurarse de que el servicio Secure Testing funciona según lo esperado, haga lo siguiente:

#### Preparar su cuenta

1. Póngase en contacto con el Servicio de atención al cliente de Adobe y solicite que habiliten Secure Testing en su cuenta.
1. En Adobe Experience Manager, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Configuración de Dynamic Media Publish]**.
1. En la página Servidor de imágenes , en la sección **[!UICONTROL Publicar contexto]** lista desplegable, seleccione **[!UICONTROL Probar servicio de imágenes]**.
1. Seleccione el **[!UICONTROL Seguridad]** pestaña .
1. Para la variable **[!UICONTROL Dirección del cliente]** filtrar, seleccionar **[!UICONTROL Agregar]**.
1. En el **[!UICONTROL Dirección IP]** , escriba una dirección IP.
1. En el **[!UICONTROL Máscara]** , escriba una máscara de red.

   >[!NOTE]
   >
   >Si agrega más de una dirección IP y una máscara de red, se permite *all* Direcciones IP para realizar llamadas de recursos y todas se muestran.

1. Realice una de las acciones siguientes:

   * Para agregar más direcciones IP, repita los tres pasos anteriores.
   * Continúe con el paso siguiente.

1. En la esquina superior derecha de la página Servidor de imágenes , seleccione **[!UICONTROL Guardar]**.
1. Cargue las imágenes que desee en su cuenta de Dynamic Media de Adobe.

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. Asegúrese de que algunas imágenes estén marcadas para publicación y otras no estén marcadas y, a continuación, envíe el trabajo de publicación.

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. Determine el nombre de su servicio Secure Testing. Para ello, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Configuración general de Dynamic Media]**.
1. En el **[!UICONTROL Servidor]** , busque el nombre del servidor a la derecha de **[!UICONTROL Nombre del servidor publicado]**.

Póngase en contacto con el servicio de atención al Adobe si falta el nombre del servidor o si la URL del servidor no funciona.

#### Preparación de las variaciones del sitio web

Necesita dos variaciones de un sitio web que vincule los recursos publicados y no publicados:

* Versión pública : vincule recursos con su sintaxis de URL tradicional de Dynamic Media de Adobe.
* Versión de ensayo : vincule los recursos con la misma sintaxis pero con el nombre del sitio Secure Testing.

#### Ejecute las pruebas

Realice las siguientes pruebas:

1. Compruebe si los recursos son visibles desde la red corporativa.

   Desde la red corporativa identificada por el intervalo de direcciones IP definido anteriormente, la versión de ensayo del sitio web muestra todas las imágenes, estén o no marcadas para publicación. De este modo, puede realizar pruebas sin tener que poner las imágenes a disposición por error antes de la aprobación de la vista previa o el inicio del producto.

   Confirme que la versión pública del sitio muestra los recursos publicados tal y como se experimentaron anteriormente con Adobe Dynamic Media.

1. Desde fuera de la red corporativa, compruebe que los activos no publicados (es decir, sin marcar para publicación) estén protegidos contra el acceso de terceros.

   Acceda a su red desde el exterior (por ejemplo, desde su equipo doméstico o a través de una conexión 4G/5G) y, a continuación, verifique que la versión pública del sitio muestre todos los recursos publicados, excepto ninguno del contenido no publicado.

   Confirme que la versión de ensayo no muestra ningún recurso porque está accediendo al servicio Secure Testing desde una dirección IP no aprobada.



