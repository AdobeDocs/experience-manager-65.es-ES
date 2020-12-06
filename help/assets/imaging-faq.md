---
title: Imágenes inteligentes
description: Las imágenes inteligentes aprovechan las características de visualización únicas de cada usuario para ofrecer automáticamente las imágenes correctas optimizadas para su experiencia, lo que mejora el rendimiento y la participación.
uuid: c11e52ba-8d64-4dc5-b30a-fc10c2b704e5
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
translation-type: tm+mt
source-git-commit: 10dae6e9f49e93d2f4923cee754c1d23d9d4b25e
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 2%

---


# Imágenes inteligentes {#smart-imaging}

## ¿Qué es &quot;Imágenes inteligentes&quot;? {#what-is-smart-imaging}

La tecnología Smart Imaging aprovecha las capacidades de Adobe Sensei AI y funciona con los &quot;ajustes preestablecidos de imagen&quot; existentes para mejorar el rendimiento del envío de imágenes optimizando automáticamente el formato, el tamaño y la calidad de las imágenes en función de las capacidades del navegador del cliente.

Smart Imaging también se beneficia del aumento de rendimiento añadido de la integración total con el servicio CDN de primera calidad de Adobe. Este servicio encuentra la ruta de Internet óptima entre servidores, redes y puntos de interrelación que tiene la latencia y/o la tasa de pérdida de paquetes más baja que la ruta predeterminada en Internet.

Los siguientes ejemplos de recursos de imagen muestran la optimización de imágenes inteligentes añadida:

| Imagen<br>(URL) | Miniatura    | Tamaño<br> (JPEG) | Tamaño (WebP)<br> (con imágenes inteligentes) | % de reducción |
|---|---|---|---|---|
| [Imagen 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38 % |
| [Imagen 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63 % |
| [Imagen 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59 % |
| [Imagen 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44 % |
|  |  |  |  | Promedio = 51% |

De manera similar a lo anterior, Adobe también ejecutó una prueba con 7009 direcciones URL de sitios de clientes activos, y logró una optimización del tamaño de archivo JPEG de un 38% más y una optimización del tamaño de archivo de un 31% más para PNG con formato WebP, debido a la capacidad de las imágenes inteligentes.

## ¿Cuáles son las ventajas clave de las últimas imágenes inteligentes? {#what-are-the-key-benefits-of-smart-imaging}

Dado que las imágenes constituyen la mayor parte del tiempo de carga de una página, la mejora del rendimiento puede tener un impacto profundo en los KPI comerciales, como una mayor conversión, tiempo invertido en el sitio y una menor tasa de devoluciones del sitio.

Mejoras en la versión más reciente de Imágenes inteligentes:

* Proporciona contenido optimizado inmediatamente (en tiempo de ejecución).
* Utiliza la tecnología de Adobe Sensei para convertir según la calidad (qlt) especificada en la solicitud de imagen.
* Las imágenes inteligentes se pueden desactivar con el parámetro de URL &quot;bfc&quot;.
* TTL (Tiempo de vivir) independiente. Anteriormente, era obligatorio un TTL mínimo de 12 horas para que funcionara la imagen inteligente.
* Anteriormente, tanto las imágenes originales como las derivadas se almacenaban en caché y era un proceso de dos pasos para invalidar la caché. En las últimas imágenes inteligentes, solo los derivados se almacenan en caché, lo que permite un proceso de invalidación de caché de un solo paso.
* Los clientes que utilicen encabezados personalizados en su conjunto de reglas (por ejemplo, &quot;Origen de permitir temporización&quot;, &quot;Robot X&quot;, como se sugiere en [Añadir un valor de encabezado personalizado en respuestas de imagen|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)) se beneficiarán de la última imagen inteligente, ya que estos encabezados no están bloqueados, a diferencia de la versión anterior de Imágenes inteligentes.

## ¿Hay algún costo de licencia asociado con las imágenes inteligentes? {#are-there-any-licensing-costs-associated-with-smart-imaging}

No. Las imágenes inteligentes se incluyen en la licencia existente de Dynamic Media Classic o Adobe Experience Manager - Dynamic Media (On Prem, AMS y AEM como Cloud Service).

>[!NOTE]
>
>Las imágenes inteligentes no están disponibles para los clientes de Dynamic Media - híbrido.


## ¿Cómo funcionan las imágenes inteligentes? {#how-does-smart-imaging-work}

Cuando un consumidor solicita una imagen, comprobamos las características del usuario y la convertimos al formato de imagen adecuado según el navegador en uso. Estas conversiones de formato se realizan de manera que no disminuya la fidelidad visual. Las imágenes inteligentes convierten automáticamente las imágenes en diferentes formatos según la capacidad del navegador de la siguiente manera.

* Convertir automáticamente a WebP para los siguientes exploradores:
   * Chrome
   * Firefox
   * Microsoft Edge
   * Safari 14.0 +
      * Safari 14 solo con iOS 14.0 y posterior y macOS BigSur y posterior
   * Android
   * Opera
* Compatibilidad con exploradores heredados para lo siguiente:

   | Explorador | Versión de explorador/SO | Formato |
   | --- | --- | --- |
   | Safari | iOS 14.0 o anterior | JPEG2000 |
   | Edge | 18 o anterior | JPEGXR |
   | Internet Explorer | 9+ | JPEGXR |
* Para los exploradores que no admiten estos formatos, se proporciona el formato de imagen solicitado originalmente.

Si el tamaño de la imagen original es menor que el de la imagen inteligente, se muestra la imagen original.

## ¿Qué formatos de imagen se admiten? {#what-image-formats-are-supported}

Los siguientes formatos de imagen son compatibles con las imágenes inteligentes:
* JPEG
* PNG

<!-- For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## ¿Cómo funciona la imagen inteligente con los ajustes preestablecidos de imagen que ya se están utilizando? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

La imagen inteligente funciona con los &quot;ajustes preestablecidos de imagen&quot; existentes y observa todos los ajustes de imagen, excepto la calidad (qlt) y el formato (fmt) si el formato de archivo solicitado es JPEG o PNG. Para la conversión de formato, mantenemos la fidelidad visual total definida por la configuración de ajustes preestablecidos de imagen, pero con un tamaño de archivo más pequeño. Si el tamaño de la imagen original es menor que el que produce la imagen inteligente, se muestra la imagen original.

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## ¿Tendré que cambiar direcciones URL, ajustes preestablecidos de imagen o implementar código nuevo en mi sitio para las imágenes inteligentes? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

Las imágenes inteligentes funcionan perfectamente con las URL de imágenes y los ajustes preestablecidos de imagen existentes si se configura las imágenes inteligentes en el dominio personalizado existente. Además, las imágenes inteligentes no requieren que agregue ningún código en el sitio web para detectar el explorador de un usuario. Todo esto se gestiona automáticamente.

En caso de que necesite configurar un nuevo dominio personalizado para utilizar las imágenes inteligentes, las direcciones URL deberán actualizarse para reflejar este dominio personalizado.

Además, consulte [¿Cumplo los requisitos para utilizar imágenes inteligentes?](#am-i-eligible-to-use-smart-imaging) para comprender los requisitos previos para las imágenes inteligentes.

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## ¿Las imágenes inteligentes funcionan con HTTPS? ¿Qué tal HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

Las imágenes inteligentes funcionan con imágenes enviadas a través de HTTP o HTTPS. Además, también funciona a través de HTTP/2.

## ¿Puedo usar imágenes inteligentes? {#am-i-eligible-to-use-smart-imaging}

Para utilizar las imágenes inteligentes, los medios dinámicos de su compañía (Dynamic Media Classic o Dynamic Media) en AEM cuenta deben cumplir los siguientes requisitos:

* Use la CDN (Red de Envío de contenido) incluida en el Adobe como parte de su licencia.
* Utilice un dominio dedicado (por ejemplo, `images.company.com` o `mycompany.scene7.com`), no un dominio genérico (por ejemplo, `s7d1.scene7.com`, `s7d2.scene7.com` o `s7d13.scene7.com`).

Para encontrar los dominios, inicie sesión en la cuenta o cuentas de compañía.

Puntee **[!UICONTROL Ajustes > Ajustes de aplicación > Configuración general.]** Busque el campo denominado Nombre del servidor  **[!UICONTROL publicado.]** Si actualmente está utilizando un dominio genérico, puede solicitar el traslado a su propio dominio personalizado como parte de esta transición cuando envíe un ticket de asistencia técnica.

El primer dominio personalizado no tiene costo adicional con una licencia de Dynamic Media.

## ¿Cuál es el proceso para activar las imágenes inteligentes en mi cuenta? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Debe iniciar la solicitud para utilizar imágenes inteligentes; no se habilita automáticamente.

1. [Utilice el Admin Console para crear un caso de soporte técnico.](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)
1. Proporcione la siguiente información en su caso de asistencia:

   1. Nombre de contacto principal, correo electrónico, teléfono.
   1. Todos los dominios que se habilitarán para la creación de imágenes inteligentes (es decir, `images.company.com` o `mycompany.scene7.com`).

      Para encontrar los dominios, inicie sesión en la cuenta o cuentas de compañía.

      Haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Configuracióngeneral.]**

      Busque el campo etiquetado **[!UICONTROL Nombre del servidor publicado.]**
   1. Compruebe que está utilizando la CDN mediante Adobe y que no se administra con una relación directa.
   1. Compruebe que está utilizando un dominio dedicado como `images.company.com` o `mycompany.scene7.com`, y no un dominio genérico, como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Para encontrar los dominios, inicie sesión en la cuenta o cuentas de compañía.

      Haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Configuracióngeneral.]**

      Busque el campo etiquetado **[!UICONTROL Nombre del servidor publicado.]** Si actualmente está utilizando un dominio genérico de Dynamic Media Classic, puede solicitar el traslado a su propio dominio personalizado como parte de esta transición.
   1. Indique si también necesita que esto funcione con HTTP/2.

1. La asistencia técnica le agregará a la Lista de espera del cliente de Smart Imaging en función del orden en que se enviaron las solicitudes.
1. Cuando Adobe esté listo para gestionar su solicitud, el servicio de soporte técnico se pondrá en contacto con usted para coordinar y establecer una fecha de destinatario.
1. **Opcional**: Tiene la opción de probar las imágenes inteligentes en Ensayo antes de que el Adobe impulse la nueva función a la producción.
1. Se le notifica después de completarlo mediante soporte técnico.
1. Para maximizar las mejoras de rendimiento de las imágenes inteligentes, Adobe recomienda establecer el Tiempo de vida (TTL) en 24 horas o más. El TTL define cuánto tiempo los recursos se almacenan en caché en la CDN. Para cambiar esta configuración:

   1. Si utiliza Dynamic Media Classic, haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Ajustes de publicación > Servidor de imágenes.]** Establezca el tiempo  **[!UICONTROL predeterminado de caché de cliente en]** Livevalue en 24 o más.
   1. Si utiliza Dynamic Media, siga [estas instrucciones](config-dynamic.md). Establezca el valor **[!UICONTROL Caducidad]** 24 horas o más.

## ¿Cuándo puedo esperar que mi cuenta esté habilitada con Imágenes inteligentes? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

Las solicitudes se procesan en el orden en que son recibidas por la asistencia técnica, según la Lista de espera.

>[!NOTE]
Puede que haya un largo tiempo de espera, ya que la activación de las imágenes inteligentes implica que el Adobe borre la caché. Por lo tanto, sólo se pueden gestionar unas pocas transiciones de clientes en un momento dado.

## ¿Cuáles son los riesgos de pasar a utilizar las imágenes inteligentes? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

No hay riesgo para una página web del cliente. Sin embargo, debe tener en cuenta que la transición a Imágenes inteligentes borra la caché en CDN porque implica pasar a una nueva configuración de Dynamic Media Classic o Dynamic Media en AEM.

Durante la transición inicial, las imágenes no almacenadas en caché llegan directamente a los servidores de origen de Adobe hasta que se vuelve a crear la caché. Debido a esto, Adobe planea manejar algunas transiciones de clientes a la vez para mantener un rendimiento aceptable al extraer solicitudes de nuestro origen. Para la mayoría de los clientes, la caché se vuelve a crear completamente en la CDN en ~1 a 2 días.

## ¿Cómo puedo verificar si las imágenes inteligentes funcionan correctamente?  {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Una vez configurada la cuenta con imágenes inteligentes, cargue una URL de imagen de Dynamic Media Classic o Adobe Experience Manager - Dynamic Media en el navegador.
1. Abra el panel del desarrollador de Chrome haciendo clic en **[!UICONTROL Vista > Desarrollador > Herramientas para desarrolladores]** en el explorador. O bien, elija la herramienta de desarrollo de navegador que desee.

1. Asegúrese de que la caché está deshabilitada cuando las herramientas de desarrollo están abiertas.

   * En Windows: vaya a la configuración del panel de herramientas del desarrollador y seleccione la casilla **[!UICONTROL Deshabilitar caché (mientras devtools está abierto)]**.
   * En Mac: en el panel del desarrollador, en la ficha **[!UICONTROL Red]**, seleccione **[!UICONTROL deshabilitar caché]**.

1. Observe que el tipo de contenido se transforma al formato adecuado. La siguiente captura de pantalla muestra una imagen PNG que se está convirtiendo dinámicamente a WebP en Chrome.
1. Repita esta prueba en diferentes exploradores y condiciones de usuario.

>[!NOTE]
No se convierten todas las imágenes. La imagen inteligente decide si la conversión es necesaria para mejorar el rendimiento. En algunos casos, cuando no hay una ganancia de rendimiento esperada o el formato no es JPEG o PNG, la imagen no se convierte.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## ¿Se puede desactivar Smart Imaging para cualquier solicitud? {#turning-off-smart-imaging}

Sí. Puede desactivar las imágenes inteligentes agregando el modificador `bfc=off` a la dirección URL.

## ¿Qué &quot;ajuste&quot; está disponible? ¿Hay alguna configuración o comportamiento que se pueda definir? (#tuning-settings)

Actualmente, puede activar o desactivar las imágenes inteligentes de forma opcional. No hay ningún otro ajuste disponible.

## Si Imágenes inteligentes gestiona la configuración de calidad, ¿hay mínimos y máximos que podamos configurar? Por ejemplo, ¿es posible establecer &quot;no menos de 60&quot; y &quot;no más de 80 calidad buena&quot;? (#Minimum-Maximum)

No existe esta capacidad de aprovisionamiento en las imágenes inteligentes actuales.

## En algunos casos, se devuelve una imagen JPEG a Chrome en lugar de una imagen WebP. ¿Por qué pasa eso? (#jpeg-webp)

Las imágenes inteligentes determinan si la conversión es beneficiosa o no. Solo devuelve la nueva imagen si la conversión da como resultado un tamaño de archivo más pequeño con una calidad comparable.
