---
title: Configuración del programa de instalación de Dynamic Media Publish para el servidor de imágenes
description: Obtenga información sobre cómo configurar el programa de instalación de publicación de Dynamic Media para el servidor de imágenes para poder publicar recursos. También puede probar los recursos antes de hacerlos públicos.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: c86e79c4-e887-4ee3-bb54-eeffb34a33c2
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3351'
ht-degree: 0%

---

# Configuración del programa de instalación de Dynamic Media Publish para el servidor de imágenes

La configuración de Dynamic Media Publish solo está disponible si:

* Está ejecutando Dynamic Media en modo Scene7. Consulte [Habilitar Dynamic Media en modo Scene7](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* Tiene un *existente* **[!UICONTROL Configuración de Dynamic Media]** (en **[!UICONTROL Cloud Service]**) en Adobe Experience Manager 6.5.11 o superior. Consulte [Creación de una configuración de Dynamic Media en Cloud Service](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
* Es administrador del sistema Experience Manager con privilegios de administrador.

El programa de instalación de publicación de Dynamic Media está diseñado para que lo utilicen programadores y desarrolladores de sitios web experimentados. Adobe Dynamic Media recomienda que los usuarios que cambien esta configuración de publicación estén familiarizados con el Dynamic Media de Adobe, las normas y convenciones del protocolo HTTP y la tecnología básica de creación de imágenes.

La página Configuración de publicación de Dynamic Media establece la configuración predeterminada que determina cómo se envían los recursos desde los servidores de Dynamic Media de Adobe a los sitios web o las aplicaciones. Si no se especifica ninguna configuración, el servidor de Dynamic Media de Adobe envía un recurso según una configuración predeterminada que se configuró en la página Configuración de publicación de Dynamic Media.

Consulte también [Opcional: configuración de Dynamic Media: configuración del modo Scene7](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) para tareas de configuración más opcionales.

>[!NOTE]
>
>¿Desea actualizar de Dynamic Media Classic a Dynamic Media en Adobe Experience Manager? El [Configuración general](/help/assets/dm-general-settings.md) y la página Ajustes de publicación de Dynamic Media se rellenan previamente con los valores tomados de la cuenta de Dynamic Media Classic. Las excepciones son todos los valores enumerados en la variable **[!UICONTROL Opciones de carga predeterminadas]** de la página Configuración general. Estos valores ya están en Experience Manager. Como tal, cualquier cambio que realice en **[!UICONTROL Opciones de carga predeterminadas]**, en cualquiera de las cinco pestañas, a través de la interfaz de usuario del Experience Manager, se reflejan en Dynamic Media, no en Dynamic Media Classic. El resto de configuraciones y valores de la variable [Configuración general](/help/assets/dm-general-settings.md) y la página Ajustes de publicación se mantienen entre Dynamic Media Classic y Dynamic Media en Experience Manager.

**Para configurar el servidor de imágenes del programa de instalación de Dynamic Media Publish:**

1. En el modo Autor del Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global.
1. En el carril izquierdo, seleccione el icono Herramientas y vaya a **[!UICONTROL Assets]** > **[!UICONTROL Ajustes de publicación de Dynamic Media]**.
1. En la página Servidor de imágenes, establezca el contexto Servidor de imágenes: publicar y, a continuación, utilice las cinco pestañas para establecer la configuración de publicación predeterminada.

   * [Servidor de imágenes](#image-server)
   * [Seguridad](#security-tab) pestaña
   * [Administración de catálogos](#catalog-management-tab) pestaña
   * [Atributos de solicitud](#request-attributes-tab) pestaña
   * [Atributos de miniatura comunes](#common-thumbnail-attributes-tab) pestaña
   * [Atributos de gestión de color](#color-management-attributes-tab) pestaña

   ![Página Configuración de publicación de Dynamic Media](/help/assets/assets-dm/dm-publish-setup.png)
   *página Configuración de publicación de Dynamic Media, con la variable **[!UICONTROL Atributos de solicitud]**pestaña seleccionada.*<br><br>

1. Cuando haya terminado, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]**.

## Servidor de imágenes {#image-server}

La página Servidor de imágenes establece la configuración predeterminada para enviar imágenes desde servidores de imágenes. La configuración está disponible en cinco categorías

| Contexto de publicación | Descripción |
| --- | --- |
| Servicio de imágenes | Especifica el contexto para la configuración de publicación. |
| Probar servicio de imágenes | Especifica el contexto para probar la configuración de publicación.<br>Solo para las nuevas cuentas de Dynamic Media, la opción predeterminada **[!UICONTROL Dirección del cliente]** el campo está configurado como `127.0.0.1` automáticamente.<br>Consulte [Pruebe los recursos antes de hacerlos públicos](#test-assets-before-making-public). |

### Pestaña Seguridad {#security-tab}

**[!UICONTROL Dirección del cliente]** : Permite especificar una o varias direcciones IP o intervalos de direcciones IP. Cuando se especifica, se rechazan las solicitudes a este catálogo de imágenes que se originan desde un cliente con una dirección IP no incluida. Esta regla se aplica tanto a la entrega de imágenes como a las imágenes procesadas.

![Pestaña Seguridad ](/help/assets/assets-dm/dm-ipallowlist.png)<br>*Pestaña Seguridad que muestra el campo &quot;Permitir&quot; de IP.*

### Pestaña Administración de catálogos {#catalog-management-tab}

**[!UICONTROL Ruta del archivo de definición del conjunto de reglas]** - Especifica el archivo que contiene las definiciones del conjunto de reglas para el catálogo de imágenes.

Consulte también [RuleSetFile](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) en la Guía de referencia de visores de Dynamic Media.

>[!NOTE]
>
>Si su cuenta de Dynamic Media Classic ya tiene un **[!UICONTROL Ruta del archivo de definición del conjunto de reglas]** seleccionado (como se establece en **[!UICONTROL Configurar]** > **[!UICONTROL Aplicación]** > **[!UICONTROL Configuración de publicación]**, en **[!UICONTROL Administración de catálogos]** grupo), su cuenta de Dynamic Media en el Experience Manager recupera el archivo de Dynamic Media Classic. A continuación, el archivo se almacena y se pone a disposición en este campo al abrir **[!UICONTROL Ajustes de publicación de Dynamic Media]** por primera vez.

### Pestaña Atributos de solicitud {#request-attributes-tab}

Estos ajustes pertenecen al aspecto predeterminado de las imágenes.

| Configuración | Descripción |
| --- | --- |
| **[!UICONTROL Límite de tamaño de imagen de respuesta]** | Requerido.<br>Solo para las cuentas nuevas de Dynamic Media, el límite de tamaño predeterminado se establece automáticamente en Anchura: `3000` y Altura: `3000` para ambos **[!UICONTROL Servicio de imágenes]** y **[!UICONTROL Probar servicio de imágenes]**.<br>Especifica la anchura y altura máximas para la imagen de respuesta que se devuelve al cliente. El servidor devuelve un error si una solicitud genera una imagen de respuesta con una anchura, altura o ambas superiores a esta configuración.<br>Consulte también [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Modo de ofuscación de solicitud]** | Habilite esta opción si desea aplicar la codificación base64 a solicitudes válidas.<br>Consulte también [RequestObfuscation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Modo de bloqueo de solicitud]** | Habilite esta opción si desea que las solicitudes incluyan un bloqueo hash simple.<br>Consulte también [RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Atributos de solicitud predeterminados]** | |
| **[!UICONTROL Sufijo de archivo de imagen predeterminado]** | Requerido.<br>Extensión de archivo de datos predeterminada que se anexa a los valores de campo de la ruta de máscara y la ruta de catálogo si la ruta no incluye un sufijo de archivo.<br>Consulte también [DefaultExt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Nombre de fuente predeterminada]** | Especifica la fuente que se utilizará en caso de que la solicitud de capa de texto no proporcione ninguna. Si se especifica, debe ser un valor de nombre de fuente válido en el mapa de fuentes de este catálogo de imágenes o en el mapa de fuentes del catálogo predeterminado.<br>Consulte también [DefaultFont](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Imagen predeterminada]** | Proporciona una imagen predeterminada en respuesta a una solicitud donde la imagen solicitada no se encuentra.<br>Consulte también [DefaultImage](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) en la Guía de referencia de visores de Dynamic Media.<br>**NOTA**: Si su cuenta de Dynamic Media Classic ya tiene un **[!UICONTROL Imagen predeterminada]** seleccionado (como se establece en **[!UICONTROL Configurar]** > **[!UICONTROL Aplicación]** > **[!UICONTROL Configuración de publicación]**, en **[!UICONTROL Atributos de solicitud predeterminados]** grupo), su cuenta de Dynamic Media en el Experience Manager recupera el archivo de Dynamic Media Classic. A continuación, el archivo se almacena y se pone a disposición en este campo al abrir **[!UICONTROL Ajustes de publicación de Dynamic Media]** por primera vez. |
| **[!UICONTROL Modo de imagen predeterminado]** | Cuando la casilla deslizante está activada (deslizador a la derecha), la **[!UICONTROL Imagen predeterminada]** reemplaza cada capa que falta en la imagen de origen con la imagen predeterminada y devuelve el compuesto de la forma habitual. Cuando el cuadro deslizante está desactivado (deslizador a la izquierda), la imagen predeterminada reemplaza toda la imagen compuesta, incluso si la imagen que falta es solo una de varias capas.<br>Consulte también [DefaultImageMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Tamaño de vista predeterminado]** | Requerido.<br>Solo para las cuentas nuevas de Dynamic Media, el tamaño de vista predeterminado se establece automáticamente en Anchura: `1280` y Altura: `1280` para ambos **[!UICONTROL Servicio de imágenes]** y **[!UICONTROL Probar servicio de imágenes]**.<br>El servidor limita el tamaño de las imágenes de respuesta a esta altura y anchura máximas, a no ser que la solicitud especifique el tamaño de vista explícitamente con `wid=`, `hei=`, o `scl=`.<br>Consulte también [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Tamaño de miniatura predeterminado]** | Requerido.<br>Se utiliza en lugar del atributo **[!UICONTROL Tamaño de vista predeterminado]** para solicitudes de miniatura (`req=tmb`). El servidor limita el tamaño de las imágenes de respuesta a esta altura y anchura máximas, a no ser que se produzca una solicitud de miniatura (`req=tmb`) no especifica el tamaño explícitamente usando `wid=`, `hei=`, o `scl=`.<br>Consulte también [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Color de fondo predeterminado]** | Especifica el valor del RGB utilizado para rellenar cualquier área de una imagen de respuesta que no contenga datos de imagen reales.<br>Consulte también [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Atributos de codificación del JPEG]** |  |
| **[!UICONTROL Calidad]** | <br>Especifica los atributos predeterminados para las imágenes de respuesta del JPEG.<br>Solo para las nuevas cuentas de Dynamic Media, la variable **[!UICONTROL Calidad]** el valor predeterminado se establece automáticamente como `80` para ambos **[!UICONTROL Servicio de imágenes]** y **[!UICONTROL Probar servicio de imágenes]**.<br>Este campo se define en el intervalo de 1 a 100.<br>Consulte también [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Disminución cromática de resolución]** | Habilite o deshabilite la disminución de resolución cromática que emplean los codificadores JPEG. |
| **[!UICONTROL Modo de remuestreo predeterminado]** | Especifica los atributos predeterminados de remuestreo e interpolación que se utilizarán para escalar los datos de imagen. Usar cuando `resMode` no se ha especificado en una solicitud.<br>Solo para las cuentas nuevas de Dynamic Media, el modo de remuestreo predeterminado se establece automáticamente en `Sharp2` para ambos **[!UICONTROL Servicio de imágenes]** y **[!UICONTROL Probar servicio de imágenes]**.<br>Consulte también [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) en la Guía de referencia de visores de Dynamic Media. |

### Pestaña Atributos de miniatura comunes {#common-thumbnail-attributes-tab}

Estos ajustes se refieren al aspecto y la alineación predeterminados de las imágenes en miniatura.

| Configuración | Descripción |
| --- | --- |
| **[!UICONTROL Color de fondo predeterminado para la miniatura]** | Especifica el valor del RGB que se utiliza para rellenar el área de una imagen en miniatura de salida que no contiene datos de imagen reales. Solo se usa para solicitudes de miniaturas (`req=tmb`) y cuándo **[!UICONTROL Tipo de miniatura predeterminado]** se establece en **[!UICONTROL Ajuste]** o **[!UICONTROL Textura]**.<br>Consulte también [ThumbBkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Alineación horizontal]** | Especifica la alineación horizontal de la imagen en miniatura en el rectángulo de imagen de respuesta especificado por `wid=` y `hei=` valores.<br>Solo se usa para solicitudes de miniaturas (`req=tmb`) y cuándo **[!UICONTROL Tipo de miniatura predeterminado]** se establece en **[!UICONTROL Ajuste]**.<br>Hay tres alineaciones horizontales entre las que elegir: **[!UICONTROL Alineación al centro]**, **[!UICONTROL Alineación izquierda]**, y **[!UICONTROL Alineación derecha]**.<br>Consulte también [ThumbHorizAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Alineación vertical]** | Especifica la alineación vertical de la imagen en miniatura en el rectángulo de imagen de respuesta especificado por `wid=` y `hei=` valores. Solo se usa para solicitudes de miniaturas (`req=tmb`) y cuándo **[!UICONTROL Tipo de miniatura predeterminado]** se establece en **[!UICONTROL Ajuste]**.<br>Hay tres alineaciones verticales entre las que elegir: **[!UICONTROL Alineación superior]**, **[!UICONTROL Alineación al centro]**, y **[!UICONTROL Alineación inferior]**.<br>Consulte también [ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Duración predeterminada de la caché]** | Proporciona un intervalo de caducidad predeterminado en horas en el caso de que el valor de catálogo Expiration no sea válido en un registro de catálogo determinado. Configure como. `-1` para marcar como nunca caduca. <br>Consulte también [Caducidad](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Tipo de miniatura predeterminado]** | Proporciona un tipo de miniatura predeterminado en el caso de que el valor de catálogo ThumbType no sea válido en un registro de catálogo determinado. Solo se usa para solicitudes de miniaturas (`req=tmb`).<br>Hay tres tipos de miniaturas para elegir: **[!UICONTROL Recorte]**, **[!UICONTROL Ajuste]**, y **[!UICONTROL Textura]**.<br>Consulte también [ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Resolución de miniatura predeterminada]** | Proporciona una resolución de miniatura predeterminada en el caso de que el valor de catálogo ThumbRes no sea válido en un registro de catálogo determinado. Solo se usa para solicitudes de miniaturas (`req=tmb`) y cuando el **[!UICONTROL Tipo de miniatura predeterminado]** se establece en **[!UICONTROL Textura]**.<br>Consulte también [ThumbRes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) en la Guía de referencia de visores de Dynamic Media. |

### Pestaña Atributos de gestión de color {#color-management-attributes-tab}

Esta configuración determina qué perfiles de color ICC se utilizan para las imágenes.

**Interpretación de conversión de color**
Una interpretación de conversión de color permite anular la interpretación predeterminada de los perfiles de trabajo para determinar cómo se ajustan los colores de origen. Se utiliza cuando:

1. Uno de los perfiles ICC predeterminados es el espacio de color de destino de una conversión de color.
1. Un dispositivo de salida (impresora o monitor) se caracteriza por este perfil.
1. Y la interpretación especificada es válida para este perfil.

Las distintas intenciones de renderización utilizan reglas diferentes para determinar cómo se ajustan los colores de origen.

Consulte también [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) en la Guía de referencia de visores de Dynamic Media.

>[!NOTE]
>
>En general, es mejor utilizar la interpretación predeterminada para el ajuste de color seleccionado, que ha sido probado por Adobe para cumplir con los estándares del sector. Por ejemplo, si elige una configuración de color para Norteamérica o Europa, la interpretación de la conversión de color por defecto es **[!UICONTROL Colorimétrico relativo]**. Si elige una configuración de color para Japón, la interpretación de la conversión de color por defecto es **[!UICONTROL Perceptual]**.

| Configuración | Características |
| --- | --- |
| **[!UICONTROL Espacio de color predeterminado CMYK]** | Especifica el nombre del perfil de color ICC que se utilizará como perfil de trabajo para los datos CMYK. If **[!UICONTROL Ninguno especificado]** se elige, la administración de color se desactiva para este catálogo de imágenes cuando hay imágenes de origen CMYK involucradas. Todos los espacios de trabajo CMYK dependen del dispositivo, lo que significa que se basan en combinaciones reales de tinta y papel. Los suministros de Adobe para espacios de trabajo CMYK se basan en las condiciones de impresión comercial estándar.<br> Consulte también [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Espacio de color predeterminado de escala de grises]** | Especifica el nombre del perfil de color ICC que se utilizará como perfil de trabajo para los datos de escala de grises. If **[!UICONTROL Ninguno especificado]** se elige, la administración de color se desactiva para este catálogo de imágenes cuando hay imágenes con origen de escala de grises involucradas.<br>Consulte también [IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Espacio de color predeterminado del RGB]** | Especifica el nombre del perfil de color ICC que se utilizará como perfil de trabajo para los datos del RGB. If **[!UICONTROL Ninguno especificado]** se elige, la administración de color se desactiva para este catálogo de imágenes cuando hay imágenes de fuentes de RGB implicadas. En general, es mejor elegir **[!UICONTROL Adobe RGB]** o **[!UICONTROL sRGB]**, en lugar del perfil de un dispositivo específico (como un perfil de monitor). **[!UICONTROL sRGB]** se recomienda cuando se preparan imágenes para la web o dispositivos móviles, ya que define el espacio de color del monitor estándar utilizado para ver imágenes en la web. **[!UICONTROL sRGB]** también es una buena opción cuando se trabaja con imágenes de cámaras digitales de consumo, ya que la mayoría de estas cámaras utilizan sRGB como su espacio de color predeterminado.<br>Consulte también [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Interpretación de conversión de color]** | **[!UICONTROL Perceptual]** - Pretende preservar la relación visual entre los colores para que se perciba como natural para el ojo humano, aunque los valores de color en sí mismos puedan cambiar. Esta intención es adecuada para imágenes fotográficas con muchos colores fuera de gama. Esta configuración es la interpretación estándar para la industria de impresión japonesa. |
|  | **[!UICONTROL Colorimétrico relativo]** : compara el resaltado extremo del espacio de color de origen con el del espacio de color de destino y cambia todos los colores en consecuencia. Los colores fuera de gama se desplazan al color reproducible más cercano en el espacio de color de destino. Colorimétrico relativo conserva más de los colores originales en una imagen que Perceptual. Esta configuración es la interpretación estándar de la impresión en Norteamérica y Europa. |
|  | **[!UICONTROL Saturación]** - Intenta producir colores vivos en una imagen a expensas de la precisión del color. Esta interpretación es adecuada para gráficos empresariales como gráficos o gráficos, donde los colores saturados brillantes son más importantes que la relación exacta entre los colores. |
|  | **[!UICONTROL Colorimétrico absoluto]** - Deja los colores que caen dentro de la gama de destino sin cambios. Los colores fuera de gama se recortan. No se aplica ninguna escala de colores al punto blanco de destino. Esta intención tiene como objetivo mantener la precisión del color a expensas de preservar las relaciones entre los colores y es adecuada para la prueba para simular la salida de un dispositivo en particular. Esta intención es útil para obtener una vista previa del modo en que el color del papel afecta a los colores impresos. |

## Pruebe los recursos antes de hacerlos públicos {#test-assets-before-making-public}

Las pruebas seguras le ayudan a definir un entorno de prueba seguro y a crear una solución sólida de empresa a empresa, basada en un conjunto configurable de direcciones IP e intervalos. Esta funcionalidad le permite hacer coincidir las implementaciones de Dynamic Media de Adobe con la arquitectura del sistema empresarial y de administración de contenido.

Con Pruebas seguras, puede obtener una vista previa de la versión de ensayo del sitio web con contenido sin publicar.

Si lo desea, cree un entorno de ensayo en lugar de publicar los recursos por los siguientes motivos:

* Previsualizar sitios web antes del lanzamiento público (sitio web de ensayo).
* Proporcione recursos que requieran acceso restringido, como catálogos electrónicos que muestran precios en una aplicación web B2B.
* Utilice recursos detrás de un cortafuegos como parte de un sistema de administración de la información del producto, una aplicación de servicio al cliente, un sitio de formación, etc.

>[!NOTE]
>
>Prueba segura no afecta al acceso a Adobe Dynamic Media Classic. La seguridad de Adobe Dynamic Media Classic sigue siendo coherente y requiere las credenciales habituales para acceder a Adobe Dynamic Media Classic y a los servicios web relacionados.

### Funcionamiento de las pruebas de seguridad {#how-test-assets-works}

La mayoría de las corporaciones manejan su Internet detrás de un cortafuegos. El acceso a Internet es posible a través de determinadas rutas y, por lo general, a través de un rango limitado de direcciones IP públicas.

Desde la red corporativa, puede averiguar su dirección IP pública mediante sitios web como [https://www.whatismyip.com](https://www.whatismyip.com/) o solicite esta información a su organización de TI corporativa.

Con las pruebas seguras, Adobe Dynamic Media crea un servidor de imágenes específico para entornos de ensayo o aplicaciones internas. Cualquier solicitud a este servidor comprueba la dirección IP de origen. Si la solicitud entrante no se encuentra dentro de la lista aprobada de direcciones IP, se devuelve una respuesta de error. El administrador de la empresa de Adobe Dynamic Media configura la lista aprobada de direcciones IP para el entorno de prueba segura de su empresa.

Dado que la ubicación de la solicitud original debe confirmarse, el tráfico del servicio Prueba segura no se enruta a través de una red de distribución de contenido como el tráfico público de Dynamic Media Image Server. Las solicitudes al servicio Secure Testing tienen una latencia ligeramente superior en comparación con los servidores de imágenes de Dynamic Media públicos.

Los recursos sin publicar están disponibles inmediatamente en los servicios de prueba segura, sin necesidad de publicarlos. De este modo, puede ejecutar una previsualización antes de que los recursos se publiquen en su servidor de imágenes público.

>[!NOTE]
>
>Los servicios de prueba segura utilizan el servidor de catálogos configurado con un contexto de publicación interno. Por lo tanto, si su empresa está configurada para publicar en pruebas seguras, cualquier recurso cargado en Adobe Dynamic Media estará disponible inmediatamente en los servicios de pruebas seguras. Esta funcionalidad se cumple independientemente de si los recursos se marcan para su publicación durante la carga.

Actualmente, los servicios de prueba segura admiten los siguientes tipos de recursos y funcionalidades:

* Imágenes.
* Viñetas (solicitudes del servidor de procesamiento).
* Solicitudes del servidor de procesamiento (admitidas, pero solicitadas explícitamente por el cliente).
* Conjuntos, incluidos conjuntos de imágenes, catálogos electrónicos, conjuntos de procesamiento y conjuntos de medios.
* Visores de medios enriquecidos estándar de Adobe Dynamic Media.
* Adobe de páginas JSP de Dynamic Media OnDemand.
* Contenido estático, como archivos de PDF y vídeos servidos progresivamente.
* Streaming de vídeo HTTP.
* Flujo de vídeo progresivo.

Actualmente no se admiten los siguientes tipos de recursos y funcionalidades:

* Búsqueda en catálogo electrónico o información de Adobe Dynamic Media Classic
* Flujo de vídeo RTMP
* Web-to-print
* Servicios de UGC (contenido generado por el usuario)

  >[!IMPORTANT]
  >
  >A partir del 1 de mayo de 2023, los recursos UGC de Dynamic Media estarán disponibles para su uso hasta 60 días después de la fecha de carga. Después de 60 días, los recursos se eliminan.

  >[!NOTE]
  >
  >La compatibilidad con recursos de imagen vectorial UGC nuevos o existentes en Adobe Dynamic Media finalizó el 30 de septiembre de 2021.

### Prueba del servicio Secure Testing {#test-secure-testing-service}

Para asegurarse de que el servicio Prueba segura funciona según lo esperado, haga lo siguiente:

#### Prepare su cuenta

1. Póngase en contacto con el Servicio de atención al cliente de Adobe y solicite que habiliten Prueba segura en su cuenta.
1. En Adobe Experience Manager, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Ajustes de publicación de Dynamic Media]**.
1. En la página Servidor de imágenes, en **[!UICONTROL Contexto de publicación]** , seleccione la opción **[!UICONTROL Probar servicio de imágenes]**.
1. Seleccione el **[!UICONTROL Seguridad]** pestaña.
1. Para el **[!UICONTROL Dirección del cliente]** filtrar, seleccionar **[!UICONTROL Añadir]**.
1. En el **[!UICONTROL Dirección IP]** , escriba una dirección IP.
1. En el **[!UICONTROL Máscara]** , escriba una máscara de red.

   >[!NOTE]
   >
   >Si agrega más de una dirección IP y máscara de red, lo permite *todo* Direcciones IP para realizar llamadas a recursos y todas aparecerán.

1. Realice una de las siguientes acciones:

   * Para agregar más direcciones IP, repita los tres pasos anteriores.
   * Continúe con el paso siguiente.

1. En la esquina superior derecha de la página Servidor de imágenes, seleccione **[!UICONTROL Guardar]**.
1. Cargue las imágenes que desee en su cuenta de Dynamic Media de Adobe.

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. Asegúrese de que algunas imágenes estén marcadas para publicación y otras no, y luego envíe el trabajo de publicación.

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. Determine el nombre del servicio Secure Testing yendo a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Configuración general de Dynamic Media]**.
1. En el **[!UICONTROL Servidor]** , busque el nombre del servidor a la derecha de **[!UICONTROL Servidor de publicación]**.

Póngase en contacto con el Servicio de atención al Adobe si falta el nombre del servidor o si la dirección URL del servidor no funciona.

#### Preparar variaciones de sitios web

Necesita dos variaciones de un sitio web que vincule los recursos publicados y no publicados:

* Versión pública: vincule recursos con la sintaxis tradicional de la URL de Dynamic Media de Adobe.
* Versión de ensayo: vincule los recursos con la misma sintaxis pero con el nombre del sitio de prueba segura.

#### Ejecutar las pruebas

Realice las siguientes pruebas:

1. Compruebe si los recursos son visibles desde la red corporativa.

   Desde la red corporativa identificada por el intervalo de direcciones IP previamente definido, la versión de ensayo del sitio web muestra todas las imágenes, estén marcadas para publicación o no. Como tal, puede realizar pruebas sin poner accidentalmente las imágenes a disposición antes de la aprobación de la vista previa o el lanzamiento del producto.

   Confirme que la versión pública del sitio muestra los recursos publicados tal y como se experimentó anteriormente con Adobe Dynamic Media.

1. Desde fuera de la red corporativa, compruebe que los recursos no publicados (es decir, sin marcar para publicación) estén protegidos frente al acceso de terceros.

   Acceda a su red desde el exterior (por ejemplo, desde su equipo doméstico o a través de una conexión 4G/5G) y, a continuación, compruebe que la versión pública del sitio muestre todos los recursos publicados, pero ninguno del contenido no publicado.

   Confirme que la versión de ensayo no muestra ningún recurso porque está accediendo al servicio de prueba segura desde una dirección IP no aprobada.
