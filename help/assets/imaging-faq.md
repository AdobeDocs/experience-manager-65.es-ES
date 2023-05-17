---
title: Imágenes inteligentes
description: Las imágenes inteligentes aplican las características de visualización únicas de cada usuario para ofrecer automáticamente las imágenes adecuadas optimizadas para su experiencia, lo que mejora el rendimiento y la participación.
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
feature: Asset Management,Renditions
role: User, Admin
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
source-git-commit: 164b3745c5bddf6ec77f9ac2ada19cfa10c6d266
workflow-type: tm+mt
source-wordcount: '3624'
ht-degree: 1%

---

# Imágenes inteligentes {#smart-imaging}

## ¿Qué es &quot;Imágenes inteligentes&quot;? {#what-is-smart-imaging}

La tecnología de imágenes inteligentes aplica las capacidades de Adobe Sensei AI y funciona con los &quot;ajustes preestablecidos de imagen&quot; existentes. Funciona para mejorar el rendimiento de la entrega de imágenes optimizando automáticamente el formato, el tamaño y la calidad de la imagen en función de las capacidades del explorador del cliente.

Y ahora, obtenga una mejor puntuación de Google Core Web Vital para LCP (Pintado de mayor contenido) con imágenes inteligentes mejoradas que ahora viene con compatibilidad con AVIF y WebP.

>[!IMPORTANT]
>
>Las imágenes inteligentes requieren que utilice la CDN (red de distribución de contenido) predeterminada que se incluye con Adobe Experience Manager - Dynamic Media. Esta función no admite ninguna otra CDN personalizada.

>[!TIP]
>
>Pruebe y descubra las ventajas de los modificadores de imágenes de Dynamic Media y de la Imágenes inteligentes con Dynamic Media [_Instantánea_](https://snapshot.scene7.com/).
>
> La instantánea es una herramienta visual de demostración diseñada para ilustrar el poder de Dynamic Media para la entrega de imágenes optimizada y dinámica. Experimente con imágenes de prueba o URL de Dynamic Media para observar visualmente el resultado de varios modificadores de imagen de Dynamic Media y optimizaciones de imágenes inteligentes para lo siguiente:
>* Tamaño del archivo (con entrega de WebP y AVIF)
>* Ancho de banda de la red
>* DPR (proporción de píxeles del dispositivo)
>
>Para aprender lo fácil que es utilizar la instantánea, reproduzca el [Vídeo de formación de instantáneas](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=en) (3 minutos y 17 segundos).

Las imágenes inteligentes se benefician del aumento de rendimiento añadido de la integración total con el servicio CDN (Red de Entrega de Contenido) premium de Adobe. Este servicio encuentra la ruta óptima de Internet entre servidores, redes y puntos de interrelación. Encuentra una ruta que tiene la latencia más baja y la menor tasa de pérdida de paquetes en lugar de usar la ruta predeterminada en Internet.

Los siguientes ejemplos de recursos de imagen ilustran la optimización de imágenes inteligentes añadida:

| Imagen (URL) | Miniatura    | Tamaño (JPEG) | Tamaño (WebP) con imágenes inteligentes | Tamaño (AVIF) con imágenes inteligentes | Reducción de % con WebP | Reducción del porcentaje con AVIF |
|---|---|---|---|---|---|---|
| [Imagen 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 145 KB | 106 KB | 90.2 KB | 26.89% | 37.79% |
| [Imagen 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 412 KB | 346 KB | 113 KB | 16.01% | 72.57% |
| [Imagen 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 221 KB | 189 KB | 87.1 KB | 14.47% | 60.58% |
| [Imagen 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 594 KB | 545 KB | 286 KB | 8.25% | 51.85% |

De forma similar a lo anterior, Adobe también realizó una prueba con un conjunto de muestras más grande. El formato AVIF proporcionó un 20% de reducción de tamaño adicional con respecto a WebP, lo que proporcionó una reducción del 27% con respecto al JPEG. Todo con la misma calidad visual. En total, el AVIF proporciona hasta un 41% de reducción de tamaño promedio en comparación con el JPEG.

Compare WebP y AVIF con PNG, puede ver una reducción del tamaño del 84% con WebP y del 87% con AVIF. Y, como tanto los formatos WebP como AVIF admiten transparencia y múltiples animaciones de imagen, es un buen reemplazo para archivos PNG y GIF transparentes.

Consulte también [Optimización de imágenes con formatos de imagen de próxima generación (WebP y AVIF)](https://blog.developer.adobe.com/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

## ¿Cuáles son las ventajas clave de las últimas imágenes inteligentes? {#what-are-the-key-benefits-of-smart-imaging}

Las imágenes inteligentes proporcionan un mejor rendimiento de entrega de imágenes al optimizar automáticamente el tamaño del archivo de imagen en función del explorador del cliente en uso, la visualización del dispositivo y las condiciones de red. Dado que las imágenes constituyen la mayor parte del tiempo de carga de una página, cualquier mejora del rendimiento puede tener un impacto profundo en los KPI comerciales, como tasas de conversión más altas, tiempo invertido en un sitio y tasas de devoluciones del sitio más bajas.

Entre las ventajas clave más recientes de la última imagen inteligente se incluyen las siguientes:

* Ahora es compatible con el formato AVIF de próxima generación.
* PNG a WebP y AVIF ahora admite la conversión con pérdidas. Debido a que PNG es un formato sin pérdidas, los WebP y AVIF anteriores que se entregaban no tenían pérdidas.
* Conversión de formato del explorador (`bfc`)
* Proporción de píxeles del dispositivo (`dpr`)
* Ancho de banda de la red (`network`)

### Acerca de la conversión de formato del explorador (bfc) {#bfc}

Activar la conversión de formato del explorador anexando `bfc=on` a la URL de imagen convierte automáticamente JPEG y PNG a AVIF con pérdidas, WebP con pérdidas, JPEGXR con pérdidas, JPEG con pérdidas2000 para diferentes navegadores. En los navegadores que no admiten estos formatos, las imágenes inteligentes siguen siendo útiles para el JPEG o PNG. Junto con el formato, la calidad del nuevo formato se vuelve a calcular mediante imágenes inteligentes.

Las imágenes inteligentes también se pueden desactivar añadiendo `bfc=off` a la URL de la imagen.

Consulte también [bfc](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc.html?lang=en) en la API de servicio y renderización de imágenes de Dynamic Media.

### Acerca de la optimización de la proporción de píxeles de dispositivo (dpr) {#dpr}

La proporción de píxeles del dispositivo (DPR), también conocida como proporción de píxeles de CSS, es la relación entre los píxeles físicos de un dispositivo y los píxeles lógicos. Especialmente con la llegada de las pantallas de retina, la resolución de píxeles de los dispositivos móviles modernos está creciendo a una velocidad rápida.

Al habilitar la optimización de la proporción de píxeles del dispositivo, la imagen se muestra en la resolución nativa de la pantalla, lo que la hace nítida.

Actualmente, la densidad de píxeles de la visualización proviene de los valores de encabezado de CDN de Akamai.

| Valores permitidos en la dirección URL de una imagen | Descripción |
|---|---|
| `dpr=off` | Desactive la optimización del RGPD en un nivel de URL de imagen individual. |
| `dpr=on,dprValue` | Sobrescriba el valor de RGPD detectado por las imágenes inteligentes, con un valor personalizado (tal y como lo detecte cualquier lógica del lado del cliente u otro medio). Valor permitido para `dprValue` es cualquier número bueno que 0. |

>[!NOTE]
>
>* Puede usar `dpr=on,dprValue` incluso si el ajuste del RGPD a nivel de empresa está desactivado.
>* Debido a la optimización del RGPD, cuando la imagen resultante es buena que la configuración de Dynamic Media MaxPix, el ancho de MaxPix siempre se reconoce manteniendo la relación de aspecto de la imagen.


| Tamaño de imagen solicitado | Valor de la proporción de píxeles del dispositivo (dpr) | Tamaño de la imagen entregada |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

Consulte también [Uso de imágenes](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images) y [Trabajar con Recorte inteligente](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

### Acerca de la optimización del ancho de banda de red {#network}

Activar el ancho de banda de red ajusta automáticamente la calidad de imagen ofrecida en función del ancho de banda de red real. Para un ancho de banda de red deficiente, la optimización del RGPD (Proporción de píxeles de dispositivo) se desactiva automáticamente, aunque ya esté activada.

Si lo desea, su empresa puede excluir la optimización del ancho de banda de la red a nivel de imagen individual añadiendo `network=off` a la URL de la imagen.

| Valor permitido en la dirección URL de una imagen | Descripción |
|---|---|
| `network=off` | Desactiva la optimización de red a nivel de URL de imagen individual. |

Los valores de RGPD y ancho de banda de red se basan en los valores detectados del lado del cliente de la CDN agrupada. Estos valores a veces son inexactos. Por ejemplo, iPhone5 con DPR=2 y iPhone12 con `dpr=3`, ambos programas `dpr=2`. Sin embargo, para dispositivos de alta resolución, enviar `dpr=2` es mejor que enviar `dpr=1`. Sin embargo, la mejor manera de superar esta inexactitud es usar el RGPD del lado del cliente para ofrecerle valores 100% precisos. Y funciona para cualquier dispositivo, ya sea Apple o cualquier otro dispositivo que se haya iniciado. Consulte [Uso de imágenes inteligentes con relación de píxeles de dispositivo del lado del cliente](/help/assets/client-side-dpr.md).

### Ventajas clave adicionales de las imágenes inteligentes

* Se ha mejorado la clasificación SEO de Google para las páginas web que utilizan las últimas imágenes inteligentes.
* Proporciona contenido optimizado inmediatamente (durante la ejecución).
* Utiliza la tecnología Adobe Sensei para convertir según la calidad (`qlt`) especificado en la solicitud de imagen.
* TTL (Tiempo de vida) independiente. Anteriormente, para que funcionara la imagen inteligente era obligatorio un TTL mínimo de 12 horas.
* Anteriormente, las imágenes originales y las imágenes derivadas se almacenaban en caché y era un proceso de 2 pasos para invalidar la caché. En las últimas imágenes inteligentes, solo se almacenan en caché los derivados, lo que permite un proceso de invalidación de caché de un solo paso.
* Los clientes que utilizan encabezados personalizados en su conjunto de reglas se benefician de las últimas imágenes inteligentes, ya que estos encabezados no están bloqueados, a diferencia de la versión anterior de imágenes inteligentes. Por ejemplo, &quot;Origen de permiso de temporización&quot;, &quot;Robot X&quot;, tal como se sugiere en [Añadir un valor de encabezado personalizado a las respuestas de imagen|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## ¿Hay algún costo de licencia asociado con las imágenes inteligentes? {#are-there-any-licensing-costs-associated-with-smart-imaging}

No. Las imágenes inteligentes se incluyen en la licencia existente. Esta regla es verdadera para Dynamic Media Classic o Experience Manager: Dynamic Media (local, AMS y as a Cloud Service por Experience Manager).

>[!NOTE]
>
>Las imágenes inteligentes no están disponibles para los clientes de Dynamic Media: híbrido.

## ¿Cómo funciona la imagen inteligente? {#how-does-smart-imaging-work}

Cuando un consumidor solicita una imagen, la función Imágenes inteligentes comprueba las características del usuario y las convierte al formato de imagen adecuado en función del explorador en uso. Estas conversiones de formato se realizan de manera que no degrada la fidelidad visual. Las imágenes inteligentes convierten automáticamente las imágenes en diferentes formatos según la capacidad del navegador de la siguiente manera.

* Convertir automáticamente a AVIF si el explorador admite el formato
* Convertir automáticamente a WebP si la conversión de AVIF no fue beneficiosa o el explorador no admite AVIF
* Convertir automáticamente a JPEG2000 si Safari no es compatible con WebP
* Convertir automáticamente a JPEGXR para IE 9+ o si Edge no es compatible con WebP\
   | Formato de imagen | Navegadores admitidos | |—|—| | AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) | | WebP | [https://caniuse.com/webp](https://caniuse.com/webp) | | JPEG 2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) | | JPEGXR | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |
* Para los navegadores que no admiten estos formatos, se proporciona el formato de imagen solicitado originalmente.

Si el tamaño de la imagen original es menor que el que produce la imagen inteligente, se suministra la imagen original.

## ¿Qué formatos de imagen se admiten? {#what-image-formats-are-supported}

Los siguientes formatos de imagen son compatibles con las imágenes inteligentes:

* JPEG
* PNG

Para el formato de archivo de imagen del JPEG, las imágenes inteligentes vuelven a calcular la calidad del nuevo formato.

Para formatos de archivo de imagen compatibles con la transparencia como PNG, puede configurar imágenes inteligentes para ofrecer AVIF y WebP con pérdidas. Para la conversión de formatos con pérdidas, Imágenes inteligentes utiliza la calidad mencionada en la URL de la imagen o la calidad configurada en la cuenta de empresa de Dynamic Media.

## ¿Cómo funciona la imagen inteligente con mis ajustes preestablecidos de imagen que ya están en uso? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

La imagen inteligente funciona con los ajustes preestablecidos de imagen existentes y observa todos los ajustes de imagen. Lo que cambia es el formato de la imagen, el ajuste de calidad o ambos. Para la conversión de formato, las imágenes inteligentes mantienen la fidelidad visual total definida por la configuración preestablecida de la imagen, pero con un tamaño de archivo más pequeño.

Por ejemplo, supongamos que un ajuste preestablecido de imagen está definido con formato de JPEG, tamaño 500 x 500, calidad=85 y máscara de enfoque 0,1,1,5. Cuando Imágenes inteligentes detecta que un usuario está en un navegador Chrome, la imagen se convierte al formato WebP, con un tamaño de 500 x 500. Y, la máscara de enfoque=0.1,1,5 se encuentra en una calidad WebP que coincide con una calidad de JPEG de 85 lo más cerca posible. La huella de esa conversión WebP se compara con el JPEG y se devuelve la menor de las dos.

## ¿Tengo que cambiar direcciones URL, ajustes preestablecidos de imagen o implementar código nuevo en mi sitio para imágenes inteligentes? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

No. Las imágenes inteligentes funcionan perfectamente con las URL de imágenes y los ajustes preestablecidos de imagen existentes. Además, las imágenes inteligentes no requieren que agregue código al sitio web para detectar el explorador de un usuario. Toda esta funcionalidad se gestiona automáticamente.

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## ¿Las imágenes inteligentes funcionan con HTTPS? ¿Qué sucede con HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

Las imágenes inteligentes funcionan con imágenes entregadas mediante HTTP o HTTPS. Además, también funciona a través de HTTP/2.

## ¿Puedo utilizar imágenes inteligentes? {#am-i-eligible-to-use-smart-imaging}

Para utilizar imágenes inteligentes, la cuenta de Experience Manager de Dynamic Media Classic o Dynamic Media de su empresa debe cumplir los siguientes requisitos:

* Utilice la CDN (red de distribución de contenido) incluida en la Adobe como parte de su licencia.
* Usar un dominio dedicado (por ejemplo, `images.company.com` o `mycompany.scene7.com`), no un dominio genérico (por ejemplo, `s7d1.scene7.com`, `s7d2.scene7.com`o `s7d13.scene7.com`).

Para encontrar los dominios, abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), luego inicie sesión en la cuenta o cuentas de su empresa.

Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**. Busque el campo etiquetado **[!UICONTROL Nombre del servidor publicado]**. Si actualmente utiliza un dominio genérico, puede solicitar el cambio a su propio dominio personalizado. Realice esta solicitud de transición cuando envíe un caso de asistencia.

El primer dominio personalizado no tiene coste adicional con una licencia de Dynamic Media.

## ¿Cuál es el proceso para habilitar las imágenes inteligentes para mi cuenta? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Se inicia una solicitud para utilizar imágenes inteligentes; no se activa automáticamente.

Cree un caso de asistencia como se describe a continuación. En su caso de asistencia, asegúrese de mencionar cuál de las siguientes capacidades de imágenes inteligentes (una o más) desea habilitar en su cuenta:

* WebP
* AVIF
* Optimización de RGPD y ancho de banda de red
* PNG a AVIF con pérdida o WebP con pérdida

Si ya ha habilitado las imágenes inteligentes con WebP, pero desea otras funciones nuevas como se ha indicado anteriormente, debe crear un caso de compatibilidad.

**Para crear un caso de compatibilidad para habilitar las imágenes inteligentes en su cuenta:**

1. [Utilice el Admin Console para iniciar la creación de un nuevo caso de asistencia](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html).
1. Proporcione la siguiente información en su caso de asistencia:

   * Nombre de contacto principal, correo electrónico, teléfono.

   * Enumere cuál de las siguientes capacidades de imágenes inteligentes (una o más) desea habilitar en su cuenta:
      * WebP
      * AVIF
      * Optimización de RGPD y ancho de banda de red
      * PNG a AVIF con pérdida o WebP con pérdida
   * Todos los dominios que se activarán para las imágenes inteligentes (es decir, `images.company.com` o `mycompany.scene7.com`).

      Para encontrar los dominios, abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), luego inicie sesión en la cuenta o cuentas de su empresa.

      Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**.

      Busque el campo etiquetado **[!UICONTROL Nombre del servidor publicado]**.

   * Compruebe que está utilizando la CDN a través de la Adobe y que no se administra con una relación directa.

   * Compruebe que está utilizando un dominio dedicado como `images.company.com` o `mycompany.scene7.com`y no un dominio genérico, como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Para encontrar los dominios, abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), luego inicie sesión en la cuenta o cuentas de su empresa.

      Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**.

      Busque el campo etiquetado **[!UICONTROL Nombre del servidor publicado]**. Si está utilizando un dominio genérico de Dynamic Media Classic, puede solicitar pasar a su propio dominio personalizado como parte de esta transición.

   * Indique si desea que funcione a través de HTTP/2.


1. El servicio de asistencia al cliente de Adobe le agrega a la lista de espera de cliente de imágenes inteligentes en función del orden en que se envíen las solicitudes.
1. Cuando el Adobe está listo para gestionar su solicitud, el Servicio de atención al cliente se pone en contacto con usted para coordinar y establecer una fecha objetivo.
1. **Opcional**: Si lo desea, puede probar las imágenes inteligentes en Ensayo antes de que el Adobe implemente la producción de la nueva función.
1. El Servicio de atención al cliente le notifica cuando haya terminado.
1. Para maximizar las mejoras de rendimiento de las imágenes inteligentes, Adobe recomienda establecer el tiempo de vida (TTL) en 24 horas o más. El TTL define cuánto tiempo la CDN almacena en caché los recursos. Para cambiar esta configuración:

   1. Si utiliza Dynamic Media Classic, vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración de publicación]** > **[!UICONTROL Servidor de imágenes]**. Configure las variables **[!UICONTROL Tiempo de vida predeterminado de la caché del cliente]** a 24 o más.
   1. Si usa Dynamic Media, siga [estas instrucciones](/help/assets/dm-publish-settings.md#common-thumbnail-attributes-tab). Configure las variables **[!UICONTROL Caducidad]** 24 horas o más.

## ¿Cuándo puedo esperar que mi cuenta esté habilitada con imágenes inteligentes? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

Las solicitudes se procesan en el orden en que son recibidas por el Servicio de atención al cliente, según la lista de espera.

>[!NOTE]
>
>Puede haber un largo tiempo de espera, ya que la activación de imágenes inteligentes implica la eliminación de Adobes en la caché. Por lo tanto, solo se pueden gestionar algunas transiciones de cliente en un momento dado.

## ¿Cuáles son los riesgos de cambiar para utilizar imágenes inteligentes? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

No existe riesgo para una página web del cliente. Sin embargo, la transición a imágenes inteligentes elimina la caché de CDN. Esta operación implica pasar a una nueva configuración de Dynamic Media Classic o Dynamic Media en el Experience Manager.

Durante la transición inicial, las imágenes no almacenadas en caché llegan directamente a los servidores de origen del Adobe hasta que se vuelve a crear la caché. De este modo, Adobe planea gestionar algunas transiciones de cliente a la vez, de modo que se mantenga un rendimiento aceptable al extraer solicitudes del origen. Para la mayoría de los clientes, la caché se vuelve a crear completamente en la CDN en ~1 - 2 días.

## ¿Cómo puedo verificar si las imágenes inteligentes funcionan correctamente?{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Una vez configurada la cuenta con imágenes inteligentes, cargue una URL de imagen de Dynamic Media Classic o Adobe Experience Manager - Dynamic Media en el explorador.
1. Abra el panel para desarrolladores de Chrome en **[!UICONTROL Ver]** > **[!UICONTROL Desarrollador]** > **[!UICONTROL Herramientas para desarrolladores]** en el navegador. O bien, elija cualquier herramienta para desarrolladores de navegador que desee.

1. Asegúrese de que la caché esté deshabilitada cuando las herramientas para desarrolladores estén abiertas.

   * En Windows®, vaya a la configuración del panel de herramientas para desarrolladores y, a continuación, seleccione **[!UICONTROL Deshabilitar la caché (mientras devtools está abierta)]** en el Navegador.
   * En macOS, en el panel del desarrollador, debajo de la sección **[!UICONTROL Red]** , seleccione **[!UICONTROL deshabilitar caché]**.

1. Observe que el tipo de contenido se transforma al formato adecuado. La siguiente captura de pantalla muestra una imagen PNG que se está convirtiendo dinámicamente a WebP en Chrome. Si su dominio tiene AVIF habilitado, también puede esperar ver AVIF en el Tipo de contenido.
1. Repita esta prueba en distintos navegadores y condiciones de usuario.

>[!NOTE]
>
>No todas las imágenes se convierten. Imágenes inteligentes decide si la conversión puede mejorar el rendimiento. A veces, cuando no hay una ganancia de rendimiento esperada o el formato no es JPEG o PNG, la imagen no se convierte.

![image2017-11-14_15398](/help/assets/assets/image2017-11-14_15398.png)

## ¿Cómo sé la ganancia de rendimiento? ¿Existe alguna forma de conocer los beneficios de las imágenes inteligentes? {#benefits}

El encabezado Imágenes inteligentes determina las ventajas de las imágenes inteligentes. Cuando la imagen inteligente está activada, después de solicitar una imagen, en la sección **[!UICONTROL Encabezados de respuesta]** encabezado, puede ver `-X-Adobe-Smart-Imaging` como se ve en el siguiente ejemplo resaltado:

![Encabezado de imagen inteligente](/help/assets/assets-dm/smart-imaging-header2.png)

Este encabezado le indica lo siguiente:

* Las imágenes inteligentes funcionan para la empresa.
* Un valor positivo significa que la conversión se ha realizado correctamente. En este caso, se devuelve una nueva imagen WebP.
* Un valor negativo significa que la conversión no se ha realizado correctamente. En tal caso, se devuelve la imagen solicitada original (JPEG de forma predeterminada, si no se especifica).
* Un valor positivo muestra la diferencia en bytes entre la imagen solicitada y la nueva imagen. En el ejemplo anterior, los bytes guardados son `75048` o aproximadamente 75 KB para una imagen.
* Un valor negativo significa que la imagen solicitada es más pequeña que la nueva imagen. Se muestra la diferencia de tamaño negativa, pero la imagen servida es solo la imagen solicitada original.

>[!NOTE]
>
>**X-Adobe-Smart-Imaging = -1 con WebP entregado**
>
>Si el valor de `X-Adobe-Smart-Imaging` es -1 y WebP sigue siendo entregado, lo que significa que imágenes inteligentes funciona, pero los beneficios de tamaño no se calcularon debido a la caché antigua. Puede usar `cache=update` (solo una vez) en la URL de la imagen para solucionar este problema.
>Ejemplo de uso del modificador:
>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>Para invalidar toda la caché, debe crear un caso de compatibilidad.

## ¿Cómo puedo desactivar la optimización de AVIF en imágenes inteligentes?{#disable-avif}

Si desea volver a servir WebP de forma predeterminada, cree un caso de soporte para el mismo. Como de costumbre, puede desactivar las imágenes inteligentes añadiendo el parámetro `bfc=off` a la URL de la imagen. Sin embargo, no puede seleccionar WebP o AVIF en el modificador de URL para imágenes inteligentes. Esta capacidad se mantiene en el nivel de cuenta de la empresa.

## ¿Se puede desactivar la imagen inteligente para cualquier solicitud?{#turning-off-smart-imaging}

Sí. Puede desactivar las imágenes inteligentes añadiendo cualquiera de los siguientes modificadores:

* `bfc=off` para desactivar la conversión de formato del explorador. Consulte también [Conversión de formato del explorador](#bfc).
* `dpr=off` para desactivar la proporción de píxeles del dispositivo. Consulte también [Proporción de píxeles del dispositivo](#dpr).
* `network=off` para desactivar el ancho de banda de la red. Consulte también [Ancho de banda de red](#network).

## ¿Qué &quot;ajuste&quot; está disponible? ¿Hay alguna configuración o comportamiento que se pueda definir? {#tuning-settings}

Las imágenes inteligentes tienen tres opciones que se pueden activar o desactivar.

* [Conversión de formato del explorador](#bfc)
* [Proporción de píxeles del dispositivo](#dpr)
* [Ancho de banda de red](#network)

## Tengo una URL con fmt=tif en el navegador web de Chrome. Pero mi solicitud falla con un error de ImageServer. ¿Por qué? {#fmt-tif}

Este error no se produce si las imágenes inteligentes no están habilitadas en la cuenta. Las imágenes inteligentes solo funcionan con los formatos JPEG o PNG.

Para evitar este error, puede:

* Especifique el JPEG o PNG, o
* No use el `fmt` modificador en absoluto, o
* Utilice un formato preferido por el navegador definido por las imágenes inteligentes. Por ejemplo, puede utilizar WebP para el explorador web Chrome.

## Quiero descargar una imagen de TIFF de la URL de una imagen. ¿Cómo lo hago? {#download-tif}

Agregar `fmt=tif` y `bfc=off` a la ruta URL de la imagen.

## ¿Las imágenes inteligentes solo administran el formato de imagen o también administran la configuración de calidad de imagen para obtener los mejores resultados?

Las imágenes inteligentes utilizan formato y calidad. El resto de los parámetros siguen siendo los mismos, si se solicitan en la dirección URL de la imagen.

## Si Imágenes inteligentes administra la configuración de calidad, ¿hay mínimos y máximos que pueda establecer? En otras palabras, ¿una calidad no inferior a 60 y no buena a 80? {#quality-setting}

Actualmente no hay tal aprovisionamiento.

## ¿Las imágenes inteligentes ajustan automáticamente la configuración de salida de la calidad porcentual o es una configuración que se ajusta manualmente y se aplica a todas las imágenes? ¿Dentro de qué rango? {#percent-quality}

Imágenes inteligentes ajusta automáticamente el porcentaje de calidad. Este porcentaje de calidad se determina usando un algoritmo de aprendizaje automático desarrollado por el Adobe. Este porcentaje no es específico del rango.

## Con las imágenes inteligentes, ¿qué comandos de servicio de imágenes se admiten o se ignoran? {#support-ignore}

Los únicos comandos que se ignoran son `fmt` y `qlt`. Se admiten todos los comandos restantes.

## ¿Solo se reemplazan las imágenes JPEG por imágenes inteligentes? ¿Qué sucede si solicito un WebP, PNG o algo más? {#replace-request}

Esta funcionalidad solo funciona para JPEG y PNG.

## ¿Por qué a veces se devuelve una imagen JPEG a Chrome en lugar de a WebP? {#jpeg-returned}

Las imágenes inteligentes determinan si la conversión es beneficiosa o no. Devuelve la nueva imagen solo si la conversión es beneficiosa.

## ¿Por qué la funcionalidad de la proporción de píxeles del dispositivo (dpr) no funciona como se espera con las imágenes compuestas? {#composite-images}

Si una imagen compuesta implica demasiadas capas, la funcionalidad del dpr puede verse afectada al utilizar un modificador de posición. Este problema se conoce y se solucionará en futuras versiones de Imágenes inteligentes. Si otras funciones de imágenes inteligentes no funcionan como se espera, puede crear un caso de compatibilidad para informar del problema.

## ¿Por qué el PNG de imágenes inteligentes sigue convirtiéndose en WebP/AVIF sin pérdidas? {#convert-to-lossless}

Debido a que PNG es un formato sin pérdidas, los WebP y AVIF anteriores que se entregaban no tenían pérdidas, por lo que su tamaño es superior al esperado. Las imágenes inteligentes ahora admiten la conversión con pérdidas. Puede utilizar el modificador `cache=update` (solo una vez) en una solicitud de imagen para solucionar este problema. Ejemplo de uso de este modificador:

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

Para invalidar toda la caché, debe crear un caso de asistencia que solicite este esfuerzo.

## ¿Cómo puedo seguir utilizando PNG para la conversión sin pérdidas en imágenes inteligentes? {#continue-using}

Las imágenes inteligentes ahora admiten la conversión con pérdidas en función del nivel de calidad. Para seguir utilizando la conversión sin pérdidas, puede utilizar la calidad 100 que se establece mediante la configuración de su empresa o a través de la URL de la imagen mediante `qlt=100` en la ruta.