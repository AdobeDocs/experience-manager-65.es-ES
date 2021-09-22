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
source-git-commit: cd0ff8f3f595e4c97668abc8c296b2f15f9d4810
workflow-type: tm+mt
source-wordcount: '2618'
ht-degree: 1%

---


# Imágenes inteligentes {#smart-imaging}

## ¿Qué es &quot;Imágenes inteligentes&quot;? {#what-is-smart-imaging}

La tecnología de imágenes inteligentes aplica las capacidades de Adobe Sensei AI y funciona con los &quot;ajustes preestablecidos de imagen&quot; existentes para mejorar el rendimiento de la entrega de imágenes optimizando automáticamente el formato, el tamaño y la calidad de la imagen en función de las capacidades del navegador del cliente.

>[!NOTE]
>
>Esta función requiere que utilice la CDN (red de distribución de contenido) predeterminada que se incluye con Adobe Experience Manager Dynamic Media. Esta función no admite ninguna otra CDN personalizada.

Las imágenes inteligentes también se benefician del aumento de rendimiento añadido de la integración total con el servicio CDN premium de Adobe. Este servicio encuentra la ruta óptima de Internet entre servidores, redes y puntos de interrelación. Encuentra una ruta que tiene la latencia más baja y la menor tasa de pérdida de paquetes en lugar de usar la ruta predeterminada en Internet.

Los siguientes ejemplos de recursos de imagen ilustran la optimización de imágenes inteligentes añadida:

| Imagen<br>(URL) | Miniatura    | Tamaño<br> (JPEG) | Tamaño (WebP)<br> (con imágenes inteligentes) | % de reducción |
|---|---|---|---|---|
| [Imagen 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38 % |
| [Imagen 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63 % |
| [Imagen 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59 % |
| [Imagen 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44 % |
|  |  |  |  | Media = 51% |

De forma similar a lo anterior, Adobe también realizó una prueba con 7009 URL de sitios de clientes activos. Pudieron lograr una optimización promedio de un 38% más del tamaño de archivo para JPEG. Para PNG con formato WebP, fueron capaces de lograr un promedio de un 31% más de optimización del tamaño de archivo. Este tipo de optimización es posible debido a la capacidad de las imágenes inteligentes.

En la web móvil, los desafíos se ven agravados por dos factores:

* Gran variedad de dispositivos con diferentes factores de forma y pantallas de alta resolución.
* Ancho de banda de red limitado.

En términos de imágenes, el objetivo es servir las imágenes de mejor calidad de la manera más eficiente posible.

### Acerca de la optimización de la proporción de píxeles del dispositivo {#dpr}

La proporción de píxeles del dispositivo (DPR), también conocida como proporción de píxeles de CSS, es la relación entre los píxeles físicos de un dispositivo y los píxeles lógicos. Especialmente con la llegada de las pantallas de retina, la resolución de píxeles de los dispositivos móviles modernos está creciendo a una velocidad rápida.

Al habilitar la optimización de la proporción de píxeles del dispositivo, la imagen se muestra en la resolución nativa de la pantalla, lo que la hace parecer nítida.

Activar la configuración del RGPD de imágenes inteligentes ajusta automáticamente la imagen solicitada en función de la densidad de píxeles de la pantalla desde la que se presenta la solicitud. Actualmente, la densidad de píxeles de la visualización proviene de los valores de encabezado de CDN de Akamai.

| Valores permitidos en la dirección URL de una imagen | Descripción |
|---|---|
| `dpr=off` | Desactive la optimización del RGPD en un nivel de URL de imagen individual. |
| `dpr=on,dprValue` | Sobrescriba el valor de RGPD detectado por las imágenes inteligentes, con un valor personalizado (tal y como lo detecte cualquier lógica del lado del cliente u otro medio). El valor permitido para `dprValue` es cualquier número bueno que 0. Los valores especificados de 1.5, 2 o 3 son típicos. |

>[!NOTE]
>
>* Puede utilizar `dpr=on,dprValue` incluso si la configuración del RGPD a nivel de empresa está desactivada.
>* Debido a la optimización del RGPD, cuando la imagen resultante es buena que la configuración de Dynamic Media MaxPix, el ancho de MaxPix siempre se reconoce manteniendo la relación de aspecto de la imagen.


| Tamaño de la imagen solicitado | Valor de RGPD | Tamaño de la imagen entregada |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632x1000 |

Consulte también [Al trabajar con imágenes](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images) y [Al trabajar con Recorte inteligente](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

### Acerca de la optimización del ancho de banda de la red {#network-bandwidth-optimization}

Activar el ancho de banda de red ajusta automáticamente la calidad de imagen ofrecida en función del ancho de banda de red real. Para un ancho de banda de red deficiente, la optimización del RGPD se desactiva automáticamente, incluso si ya está activada.

Si lo desea, su empresa puede excluir la optimización del ancho de banda de la red a nivel de imagen individual añadiendo `network=off` a la dirección URL de la imagen.

| Valor permitido en la dirección URL de una imagen | Descripción |
|---|---|
| `network=off` | Desactiva la optimización de red a nivel de URL de imagen individual. |

>[!NOTE]
>
>Los valores de RGPD y ancho de banda de red se basan en los valores detectados del lado del cliente de la CDN agrupada. Estos valores a veces son inexactos. Por ejemplo, iPhone5 con DPR=2 e iPhone12 con DPR=3, ambos muestran DPR=2. Sin embargo, para los dispositivos de alta resolución, el envío del RGPD=2 es mejor que el envío del RGPD=1. Próximamente: Adobe está trabajando en código del lado del cliente para determinar con precisión el RGPD de un usuario final.

## ¿Cuáles son las ventajas clave de las últimas imágenes inteligentes? {#what-are-the-key-benefits-of-smart-imaging}

Como las imágenes constituyen la mayor parte del tiempo de carga de una página, la mejora del rendimiento puede tener un impacto profundo en un negocio, como una mayor conversión, el tiempo invertido en el sitio y una menor tasa de devoluciones del sitio.

Mejoras en la última versión de imágenes inteligentes:

* Se ha mejorado la clasificación SEO de Google para páginas web que utilizan la última imagen inteligente.
* Proporciona contenido optimizado inmediatamente (en tiempo de ejecución).
* Utiliza la tecnología de Adobe Sensei para realizar la conversión según la calidad (qlt) especificada en la solicitud de imagen.
* Las imágenes inteligentes se pueden desactivar utilizando el parámetro de URL &quot;bfc&quot;.
* TTL (Tiempo de vida) independiente. Anteriormente, para que funcionara la imagen inteligente era obligatorio un TTL mínimo de 12 horas.
* Anteriormente, las imágenes originales y las imágenes derivadas se almacenaban en caché y era un proceso de 2 pasos para invalidar la caché. En las últimas imágenes inteligentes, solo se almacenan en caché los derivados, lo que permite un proceso de invalidación de caché de un solo paso.
* Los clientes que utilizan encabezados personalizados en su conjunto de reglas se benefician de las últimas imágenes inteligentes, ya que estos encabezados no están bloqueados, a diferencia de la versión anterior de imágenes inteligentes. Por ejemplo, &quot;Origen de permiso de temporización&quot;, &quot;Robot X&quot;, como se sugiere en [Agregue un valor de encabezado personalizado a las respuestas de imagen|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## ¿Hay algún costo de licencia asociado con las imágenes inteligentes? {#are-there-any-licensing-costs-associated-with-smart-imaging}

No. Las imágenes inteligentes se incluyen en su licencia existente de Dynamic Media Classic o Adobe Experience Manager - Dynamic Media (On-Premim, AMS y Adobe Experience Manager como Cloud Service).

>[!NOTE]
>
>Las imágenes inteligentes no están disponibles para los clientes de Dynamic Media: híbrido.

## ¿Cómo funcionan las imágenes inteligentes? {#how-does-smart-imaging-work}

Cuando un consumidor solicita una imagen, la función Imágenes inteligentes comprueba las características del usuario y la convierte al formato de imagen adecuado en función del explorador en uso. Estas conversiones de formato se realizan de manera que no degrada la fidelidad visual. Las imágenes inteligentes convierten automáticamente las imágenes en diferentes formatos según la capacidad del navegador de la siguiente manera.

<!--   * Safari 14.0 +
    * Safari 14 only with iOS 14.0 and above and macOS BigSur and above -->

* Convertir automáticamente a WebP para los siguientes navegadores:
   * Chrome
   * Firefox
   * Microsoft® Edge
   * Safari (en iOS, macOS, iPadOS), compatible con WebP con el explorador y la versión del sistema operativo
   * Android™
   * Opera
* Compatibilidad con navegadores anteriores para lo siguiente:

   | Explorador | Versión del navegador/sistema operativo | Formato |
   | --- | --- | --- |
   | Safari | Anterior a iOS/iPad 14.0 o macOS BigSur | JPEG2000 |
   | Edge | Anteriores a 18 | JPEGXR |
   | Internet Explorer | 9+ | JPEGXR |
* Para los navegadores que no admiten estos formatos, se proporciona el formato de imagen solicitado originalmente.

Si el tamaño de la imagen original es menor que el que produce la imagen inteligente, se suministra la imagen original.

## ¿Qué formatos de imagen se admiten? {#what-image-formats-are-supported}

Los siguientes formatos de imagen son compatibles con las imágenes inteligentes:

* JPEG
* PNG

<!-- CQDOC-15846 For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## ¿Cómo funciona la imagen inteligente con mis ajustes preestablecidos de imagen que ya están en uso? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

La imagen inteligente funciona con los &quot;ajustes preestablecidos de imagen&quot; existentes y observa todos los ajustes de imagen, excepto la calidad (`qlt`) y el formato (`fmt`) si el formato de archivo solicitado es JPEG o PNG. Para la conversión de formato, las imágenes inteligentes mantienen la fidelidad visual total definida por la configuración preestablecida de la imagen, pero con un tamaño de archivo más pequeño. Si el tamaño de la imagen original es menor que el que produce la imagen inteligente, se suministra la imagen original.

<!-- CQDOC-15846 In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## ¿Tengo que cambiar direcciones URL, ajustes preestablecidos de imagen o implementar código nuevo en mi sitio para imágenes inteligentes? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

Las imágenes inteligentes funcionan perfectamente con las URL de imágenes y los ajustes preestablecidos de imagen existentes si configura las imágenes inteligentes en su dominio personalizado existente. Además, las imágenes inteligentes no requieren que añada código en el sitio web para detectar el explorador de un usuario. Todo se gestiona automáticamente.

Si debe configurar un nuevo dominio personalizado para utilizar imágenes inteligentes, las direcciones URL deben actualizarse para reflejar este dominio personalizado.

Para comprender los requisitos previos para las imágenes inteligentes, consulte [¿Puedo utilizar imágenes inteligentes?](#am-i-eligible-to-use-smart-imaging)

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## ¿Las imágenes inteligentes funcionan con HTTPS? ¿Qué sucede con HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

Las imágenes inteligentes funcionan con imágenes entregadas mediante HTTP o HTTPS. Además, también funciona a través de HTTP/2.

## ¿Puedo utilizar imágenes inteligentes? {#am-i-eligible-to-use-smart-imaging}

Para utilizar imágenes inteligentes, la cuenta de Experience Manager de Dynamic Media Classic o Dynamic Media de su empresa debe cumplir los siguientes requisitos:

* Utilice la CDN (red de distribución de contenido) incluida en la Adobe como parte de su licencia.
* Utilice un dominio dedicado (por ejemplo, `images.company.com` o `mycompany.scene7.com`), no un dominio genérico (por ejemplo, `s7d1.scene7.com`, `s7d2.scene7.com` o `s7d13.scene7.com`).

Para encontrar sus dominios, abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) y luego inicie sesión en la cuenta o cuentas de su empresa.

Vaya a **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL General Settings]** Busque el campo etiquetado **[!UICONTROL Published Server Name]**. Si está utilizando un dominio genérico, puede solicitar pasar a su propio dominio personalizado como parte de esta transición cuando envíe un ticket de asistencia técnica.

El primer dominio personalizado no tiene coste adicional con una licencia de Dynamic Media.

## ¿Cuál es el proceso para habilitar las imágenes inteligentes para mi cuenta? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Se inicia la solicitud para utilizar imágenes inteligentes; no se activa automáticamente.

De forma predeterminada, el RGPD de imágenes inteligentes y la optimización de la red están deshabilitados (desactivados) para una cuenta de empresa de Dynamic Media. Si desea habilitar (activar) una o ambas mejoras integradas, cree un caso de asistencia como se describe a continuación.

<!-- NOW AVAILABLE IN ALL THREE REGIONS AS OF AUGUST 2. 2021. SEE CQDOC- 17915 The release schedule for Smart Imaging DPR and network optimization is as follows:

| Region | Target date |
|---|---|
| North America | Live |
| Europe, Middle East, Africa | 13 Aug 2021 |
| Asia-Pacific | 22 Jul 2021 | -->

1. [Utilice el Admin Console para crear un caso](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) de asistencia.
1. Proporcione la siguiente información en su caso de asistencia:

   1. Nombre de contacto principal, correo electrónico, teléfono.
   1. Todos los dominios que se activarán para la creación de imágenes inteligentes (es decir, `images.company.com` o `mycompany.scene7.com`).

      Para encontrar sus dominios, abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) y luego inicie sesión en la cuenta o cuentas de su empresa.

      Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**.

      Busque el campo denominado **[!UICONTROL Published Server Name]**.
   1. Compruebe que está utilizando la CDN a través de la Adobe y que no se administra con una relación directa.
   1. Compruebe que está utilizando un dominio dedicado como `images.company.com` o `mycompany.scene7.com` y no un dominio genérico, como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Para encontrar sus dominios, abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) y luego inicie sesión en la cuenta o cuentas de su empresa.

      Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**.

      Busque el campo denominado **[!UICONTROL Published Server Name]**. Si está utilizando un dominio genérico de Dynamic Media Classic, puede solicitar pasar a su propio dominio personalizado como parte de esta transición.
   1. Indique si también necesita que las imágenes inteligentes funcionen con HTTP/2.

1. El Servicio de atención al cliente de Adobe le agrega a la lista de espera de cliente de imágenes inteligentes en función del orden en que se enviaron las solicitudes.
1. Cuando el Adobe esté listo para gestionar su solicitud, el servicio de asistencia técnica contactará con usted para coordinar y establecer una fecha objetivo.
1. **Opcional** : opcionalmente, puede probar imágenes inteligentes en Ensayo antes de que el Adobe implemente la producción de la nueva función.
1. El Servicio de atención al cliente le notifica una vez que la haya completado.
1. Para maximizar las mejoras de rendimiento de las imágenes inteligentes, Adobe recomienda establecer el tiempo de vida (TTL) en 24 horas o más. El TTL define cuánto tiempo la CDN almacena en caché los recursos. Para cambiar esta configuración:

   1. Si utiliza Dynamic Media Classic, vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Publicar configuración]** > **[!UICONTROL Servidor de imágenes]**. Establezca el valor **[!UICONTROL Tiempo de caché de cliente predeterminado en activo]** en 24 o más.
   1. Si usa Dynamic Media, siga [estas instrucciones](config-dynamic.md). Establezca el valor **[!UICONTROL Expiration]** 24 horas o más.

## ¿Cuándo puedo esperar que mi cuenta esté habilitada con imágenes inteligentes? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

Las solicitudes se procesan en el orden en que se reciben en el Servicio de atención al cliente, según la lista de espera.

>[!NOTE]
>
>Puede haber un largo tiempo de espera, ya que la activación de imágenes inteligentes implica la eliminación de Adobes en la caché. Por lo tanto, solo se pueden gestionar algunas transiciones de cliente en un momento dado.

## ¿Cuáles son los riesgos de cambiar para utilizar imágenes inteligentes? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

No existe riesgo para una página web del cliente. Sin embargo, la transición a imágenes inteligentes borra la caché en la CDN porque implica pasar a una nueva configuración de Dynamic Media Classic o Dynamic Media en el Experience Manager.

Durante la transición inicial, las imágenes no almacenadas en caché llegan directamente a los servidores de origen del Adobe hasta que se vuelve a crear la caché. Como resultado, Adobe planea gestionar algunas transiciones de cliente a la vez, de modo que se mantenga un rendimiento aceptable al extraer solicitudes del origen. Para la mayoría de los clientes, la caché se vuelve a crear completamente en la CDN en ~1 - 2 días.

## ¿Cómo puedo verificar si las imágenes inteligentes funcionan según lo esperado?{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Una vez configurada la cuenta con imágenes inteligentes, cargue una URL de imagen de Dynamic Media Classic o Adobe Experience Manager - Dynamic Media en el explorador.
1. Abra el panel del desarrollador de Chrome navegando hasta **[!UICONTROL View]** > **[!UICONTROL Developer]** > **[!UICONTROL Developer Tools]** en el explorador. O bien, elija cualquier herramienta para desarrolladores de navegador que desee.

1. Asegúrese de que la caché esté deshabilitada cuando las herramientas para desarrolladores estén abiertas.

   * En Windows®, vaya a la configuración del panel de herramientas para desarrolladores y, a continuación, active la casilla **[!UICONTROL Deshabilitar caché (mientras devtools está abierta)]**.
   * En macOS, en el panel del desarrollador, en la pestaña **[!UICONTROL Network]**, seleccione **[!UICONTROL disable cache]**.

1. Observe que el tipo de contenido se transforma al formato adecuado. La siguiente captura de pantalla muestra una imagen PNG que se está convirtiendo dinámicamente a WebP en Chrome.
1. Repita esta prueba en distintos navegadores y condiciones de usuario.

>[!NOTE]
>
>No todas las imágenes se convierten. Imágenes inteligentes decide si la conversión puede mejorar el rendimiento. A veces, cuando no hay una ganancia de rendimiento esperada o el formato no es JPEG o PNG, la imagen no se convierte.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## ¿Se puede desactivar la imagen inteligente para cualquier solicitud? {#turning-off-smart-imaging}

Sí. Puede desactivar las imágenes inteligentes añadiendo el modificador `bfc=off` a la dirección URL.

## ¿Puedo solicitar que la optimización del RGPD y de la red se desactive a nivel de empresa? {#dpr-companylevel-turnoff}

Sí. Para desactivar la optimización de la red y el RGPD en su empresa, cree un caso de asistencia como se describió anteriormente en este tema.

## ¿Qué &quot;ajuste&quot; está disponible? ¿Hay alguna configuración o comportamiento que se pueda definir? (#tuning-settings)

Actualmente, puede activar o desactivar las imágenes inteligentes. No hay ningún otro ajuste disponible.

## Si Imágenes inteligentes administra la configuración de calidad, ¿hay mínimos y máximos que configurar? Por ejemplo, ¿es posible configurar &quot;no menos de 60&quot; y &quot;no buena que 80 calidad&quot;? (#Minimum-maximum)

No existe esta capacidad de aprovisionamiento en la imagen inteligente actual.

## A veces, se devuelve una imagen JPEG a Chrome en lugar de una imagen WebP. ¿Por qué ocurre ese cambio? (#jpeg-webp)

Las imágenes inteligentes determinan si la conversión es beneficiosa o no. Devuelve la nueva imagen solo si la conversión resulta en un tamaño de archivo más pequeño con una calidad comparable.

## ¿Cómo funciona la optimización del RGPD de imágenes inteligentes con los componentes de Adobe Experience Manager Sites y los visores de Dynamic Media?

* Los componentes principales de Experience Manager Sites están configurados de forma predeterminada para la optimización del RGPD. Para evitar imágenes sobredimensionadas debido a la optimización del RGPD de imágenes inteligentes en el lado del servidor, `dpr=off` siempre se agrega a las imágenes de Dynamic Media de los componentes principales de los sitios del Experience Manager.
* Dado que el componente base de Dynamic Media está configurado de forma predeterminada para la optimización del RGPD, para evitar imágenes de tamaño excesivo debido a la optimización del RGPD de imágenes inteligentes en el servidor, `dpr=off` siempre se añade a las imágenes de los componentes de Dynamic Media Foundation. Aunque el cliente anule la selección de la optimización de RGPD en el componente de base de DM, el RGPD de imágenes inteligentes del lado del servidor no se inicia. En resumen, en el componente de base de DM, la optimización del RGPD entra en vigor solo en función de la configuración del nivel de componente de base de DM .
* Cualquier optimización del RGPD del lado del visor funciona junto con la optimización del RGPD de imágenes inteligentes del lado del servidor y no genera imágenes de tamaño excesivo. En otras palabras, independientemente de dónde gestione el visor el RGPD, como la vista principal solo en un visor con zoom habilitado, no se activan los valores del RGPD de imágenes inteligentes del lado del servidor. Del mismo modo, siempre que los elementos del visualizador, como muestras y miniaturas, no tengan gestión de RGPD, se activa el valor RGPD de imágenes inteligentes del lado del servidor.

Consulte también [Al trabajar con imágenes](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images) y [Al trabajar con Recorte inteligente](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

>[!MORELIKETHIS]
>
>* [Optimización de imágenes con los formatos de imagen de próxima generación WebP y AVIF.](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)
>

