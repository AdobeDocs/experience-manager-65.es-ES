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
source-git-commit: d690bcc80052f356425cd85c498aa48b1caf44bc

---


# Imágenes inteligentes {#smart-imaging}

## ¿Qué es &quot;Imágenes inteligentes&quot;? {#what-is-smart-imaging}

La tecnología de imágenes inteligentes aprovecha las capacidades de Adobe Sensei AI y funciona con los &quot;ajustes preestablecidos de imagen&quot; existentes para mejorar el rendimiento del envío de imágenes optimizando automáticamente el formato, el tamaño y la calidad de las imágenes en función de las capacidades del navegador del cliente.

Smart Imaging también se beneficia del aumento de rendimiento añadido de la integración total con el servicio CDN Premium de Adobe. Este servicio encuentra la ruta de Internet óptima entre servidores, redes y puntos de interrelación que tiene la latencia y/o la tasa de pérdida de paquetes más baja que la ruta predeterminada en Internet.

Los siguientes ejemplos de recursos de imagen muestran la optimización de imágenes inteligentes añadida:

| Image<br>(URL) | Miniatura   | Tamaño<br> (JPEG) | Tamaño (WebP)<br> (con imágenes ***inteligentes***) | % de reducción |
|---|:---:|:---:|:---:|:---:|:---:|
| [Imagen 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&fmt=jpg&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38% |
| [Imagen 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&fmt=jpg&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63% |
| [Imagen 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&fmt=jpg&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59% |
| [Imagen 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44% |
|  |  |  |  | Promedio = 51% |

De manera similar a lo anterior, Adobe también ejecutó una prueba con 7009 URL de sitios de clientes activos, y logró una optimización del tamaño de archivo en JPEG de un 38% en promedio y una optimización del tamaño de archivo en un 31% adicional para PNG con formato WebP, debido a la capacidad de las imágenes inteligentes.

## ¿Cuáles son las ventajas clave de las últimas imágenes inteligentes? {#what-are-the-key-benefits-of-smart-imaging}

Dado que las imágenes constituyen la mayor parte del tiempo de carga de una página, la mejora del rendimiento puede tener un impacto profundo en los KPI comerciales, como una mayor conversión, tiempo invertido en el sitio y una menor tasa de devoluciones del sitio.

Mejoras en la versión más reciente de Imágenes inteligentes:

* Proporciona contenido optimizado inmediatamente (en tiempo de ejecución).
* Utiliza la tecnología Adobe Sensei para convertir según la calidad (qlt) especificada en la solicitud de imagen.
* Las imágenes inteligentes se pueden desactivar con el parámetro de URL &quot;bfc&quot;.
* TTL (Tiempo de vivir) independiente. Anteriormente, era obligatorio un TTL mínimo de 12 horas para que funcionara la imagen inteligente.
* Anteriormente, tanto las imágenes originales como las derivadas se almacenaban en caché y era un proceso de dos pasos para invalidar la caché. En las últimas imágenes inteligentes, solo los derivados se almacenan en caché, lo que permite un proceso de invalidación de caché de un solo paso.
* Los clientes que utilicen encabezados personalizados en su conjunto de reglas (por ejemplo, &quot;Origen de permitir temporización&quot; o &quot;Robot X&quot;, como se sugiere al [Añadir un valor de encabezado personalizado en las respuestas de imágenes|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)) se beneficiarán de la última imagen inteligente, ya que estos encabezados no están bloqueados, a diferencia de la versión anterior de la imagen inteligente.

## ¿Hay algún costo de licencia asociado con las imágenes inteligentes? {#are-there-any-licensing-costs-associated-with-smart-imaging}

No. Las imágenes inteligentes se incluyen en la licencia existente de Dynamic Media Classic (Scene7) o AEM Dynamic Media (On Prem, AMS y AEM como servicio de nube).

>[!NOTE]
>
>Las imágenes inteligentes no están disponibles para los clientes de Dynamic Media - híbrido.


## ¿Cómo funcionan las imágenes inteligentes? {#how-does-smart-imaging-work}

Smart Imaging utiliza Adobe Sensei para convertir automáticamente imágenes al formato, tamaño y calidad más óptimos, según la capacidad del navegador:

* Convertir automáticamente a WebP para exploradores como Chrome, Firefox, Microsoft Edge, Android y Opera.
* Convertir automáticamente a JPEG2000 para navegadores como Safari.
* Convertir automáticamente a JPEG para exploradores como Internet Explorer 9+.
* Para los exploradores que no admiten estos formatos, se proporciona el formato de imagen solicitado originalmente.

Si el tamaño de la imagen original es menor que el de la imagen inteligente, se muestra la imagen original.

## ¿Qué formatos de imagen se admiten? {#what-image-formats-are-supported}

Los siguientes formatos de imagen son compatibles con las imágenes inteligentes:
* JPEG
* PNG

Para cualquier otro formato mencionado en una URL, debe desactivar explícitamente las imágenes inteligentes.  Añada un modificador `bfc=off` a la URL para los formatos de archivo distintos de JPEG y PNG. Esto se puede lograr mediante uno de los siguientes métodos:

* Utilice un conjunto de reglas si se menciona el `fmt` modificador en la dirección URL.
* Añada el campo modificadores de URL de los ajustes preestablecidos correspondientes.

Adobe está trabajando en una corrección permanente que no requiere que anexe `bfc=off` para `fmt !=JPEG` o `fmt !=PNG`. Este tema se actualizará después de que se envíe la corrección.


## ¿Cómo funciona la imagen inteligente con los ajustes preestablecidos de imagen que ya se están utilizando? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

La imagen inteligente funciona con los &quot;ajustes preestablecidos de imagen&quot; existentes y observa todos los ajustes de imagen, excepto la calidad (qlt) y el formato (fmt) si el formato de archivo solicitado es JPEG o PNG. Para la conversión de formato, mantenemos la fidelidad visual total definida por la configuración de ajustes preestablecidos de imagen, pero con un tamaño de archivo más pequeño. Si el tamaño de la imagen original es menor que el que produce la imagen inteligente, se muestra la imagen original.

Además, si los ajustes preestablecidos de imagen se utilizan para devolver `fmt !=JPEG` o `fmt !=PNG`, asegúrese de anexar `bfc=off` el campo modificador de ajustes preestablecidos para devolver el formato de archivo solicitado.

## ¿Tendré que cambiar direcciones URL, ajustes preestablecidos de imagen o implementar código nuevo en mi sitio para las imágenes inteligentes? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

Las imágenes inteligentes funcionan perfectamente con las URL de imágenes y los ajustes preestablecidos de imagen existentes. Además, las imágenes inteligentes no requieren que agregue ningún código en el sitio web para detectar el explorador de un usuario. Todo esto se gestiona automáticamente.

Como se mencionó anteriormente, Smart Imaging solo admite formatos de imagen JPEG y PNG. Para otros formatos, debe anexar el `bfc=off` modificador a la dirección URL como se ha descrito anteriormente.

Además, consulte [¿Cumplo los requisitos para utilizar imágenes inteligentes?](#am-i-eligible-to-use-smart-imaging) para comprender los requisitos previos para las imágenes inteligentes.

## ¿Funciona la función de Smart Mmaging con HTTPS? ¿Qué tal HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

Las imágenes inteligentes funcionan con imágenes enviadas a través de HTTP o HTTPS. Además, también funciona a través de HTTP/2.

## ¿Puedo usar imágenes inteligentes? {#am-i-eligible-to-use-smart-imaging}

Para utilizar las imágenes inteligentes, la cuenta de AEM de Dynamic Media Classic o Dynamic Media de su compañía debe cumplir los siguientes requisitos:

* Use la CDN (Red de Envío de contenido) incluida en Adobe como parte de su licencia.
* Utilice un dominio dedicado (por ejemplo, `images.company.com` o `mycompany.scene7.com`), no un dominio genérico (por ejemplo, `s7d1.scene7.com`, `s7d2.scene7.com`o `s7d13.scene7.com`).

Para encontrar los dominios, inicie sesión en la cuenta o cuentas de compañía.

Tap **[!UICONTROL Setup > Application Setup > General Settings]**. Busque el campo con la etiqueta Nombre **[!UICONTROL del servidor]** publicado. Si actualmente está utilizando un dominio genérico, puede solicitar el traslado a su propio dominio personalizado como parte de esta transición cuando envíe un ticket de asistencia técnica.

El primer dominio personalizado no tiene costo adicional con una licencia de Dynamic Media.

## ¿Cuál es el proceso para activar las imágenes inteligentes en mi cuenta? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Debe iniciar la solicitud para utilizar imágenes inteligentes; no se habilita automáticamente.

1. Iniciar una solicitud de asistencia técnica (correo electrónico: s7support@adobe.com).
1. Proporcione la siguiente información en su solicitud de asistencia:

   1. Nombre de contacto principal, correo electrónico, teléfono.
   1. Todos los dominios que se van a habilitar para las imágenes inteligentes (es decir, imágenes.compañía.com o miempresa.escena7.com).

      Para encontrar los dominios, inicie sesión en la cuenta o cuentas de compañía.

      Haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Configuracióngeneral]**.

      Busque el campo con la etiqueta Nombre **[!UICONTROL del servidor]** publicado.
   1. Compruebe que está utilizando la CDN a través de Adobe y que no se administra con una relación directa.
   1. Compruebe que está utilizando un dominio dedicado como `images.company.com` o `mycompany.scene7.com`, y no un dominio genérico, como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Para encontrar los dominios, inicie sesión en la cuenta o cuentas de compañía.

      Haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Configuracióngeneral]**.

      Busque el campo con la etiqueta Nombre **[!UICONTROL del servidor]** publicado. Si actualmente está utilizando un dominio genérico de Dynamic Media Classic, puede solicitar el traslado a su propio dominio personalizado como parte de esta transición.
   1. Indique si también necesita que esto funcione con HTTP/2.

1. La asistencia técnica le agregará a la Lista de espera del cliente de Smart Imaging en función del orden en que se enviaron las solicitudes.
1. Cuando Adobe esté preparado para gestionar su solicitud, el servicio de asistencia técnica se pondrá en contacto con usted para coordinar y establecer una fecha de destinatario.
1. **Opcional**: Tiene la opción de probar las imágenes inteligentes en Ensayo antes de que Adobe implemente la nueva función en producción.
1. Se le notifica después de completarlo mediante soporte técnico.
1. Para maximizar las mejoras de rendimiento de las imágenes inteligentes, Adobe recomienda establecer el Tiempo de vida (TTL) en 24 horas o más. El TTL define cuánto tiempo los recursos se almacenan en caché en la CDN. Para cambiar esta configuración:

   1. Si utiliza Dynamic Media Classic, haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Ajustes de publicación > Servidor]** de imágenes. Establezca el valor **[!UICONTROL Predeterminado de Tiempo de espera de cliente en Activo]** en 24 o más.
   1. Si utiliza Dynamic Media, siga [estas instrucciones](config-dynamic.md). Establezca el valor **[!UICONTROL Caducidad]** en 24 horas o más.

## ¿Cuándo puedo esperar que mi cuenta esté habilitada con Imágenes inteligentes? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

Las solicitudes se procesan en el orden en que son recibidas por la asistencia técnica, según la Lista de espera.

>[!NOTE]
Puede haber un largo tiempo de espera, ya que la activación de las imágenes inteligentes implica que Adobe borre la caché. Por lo tanto, sólo se pueden gestionar unas pocas transiciones de clientes en un momento dado.

## ¿Cuáles son los riesgos de pasar a utilizar las imágenes inteligentes? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

No hay riesgo para una página web del cliente. Sin embargo, debe tener en cuenta que la transición a Imágenes inteligentes borra la caché en CDN porque implica pasar a una nueva configuración de Dynamic Media Classic o Dynamic Media en AEM.

Durante la transición inicial, las imágenes no almacenadas en caché llegan directamente a los servidores de origen de Adobe hasta que se vuelve a crear la caché. Debido a esto, Adobe planea gestionar algunas transiciones de clientes a la vez, de modo que se mantenga un rendimiento aceptable al extraer solicitudes de nuestro origen. Para la mayoría de los clientes, la caché se vuelve a crear completamente en la CDN en ~1 a 2 días.

## ¿Cómo puedo verificar si las imágenes inteligentes funcionan correctamente?  {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Una vez configurada la cuenta con imágenes inteligentes, cargue una URL de imagen de Dynamic Media Classic (Scene7)/Dynamic Media en el navegador.
1. Abra el panel del desarrollador de Chrome haciendo clic en **[!UICONTROL Vista > Desarrollador > Herramientas]** para desarrolladores en el navegador. O bien, elija la herramienta de desarrollo de navegador que desee.

1. Asegúrese de que la caché está deshabilitada cuando las herramientas de desarrollo están abiertas.

   * En Windows: vaya a la configuración del panel de herramientas del desarrollador y, a continuación, seleccione la casilla de verificación **[!UICONTROL Deshabilitar caché (mientras devtools está abierto)]** .
   * On Mac – in the developer pane, under the **[!UICONTROL Network]** tab, select **[!UICONTROL disable cache]** .

1. Observe que el tipo de contenido se transforma al formato adecuado. La siguiente captura de pantalla muestra una imagen PNG que se está convirtiendo dinámicamente a WebP en Chrome.
1. Repita esta prueba en diferentes exploradores y condiciones de usuario.

>[!NOTE]
No se convierten todas las imágenes. La imagen inteligente decide si la conversión es necesaria para mejorar el rendimiento. En algunos casos, cuando no hay una ganancia de rendimiento esperada o el formato no es JPEG o PNG, la imagen no se convierte.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## ¿Se puede desactivar Smart Imaging para cualquier solicitud? {#turning-off-smart-imaging}

Sí. Puede desactivar las imágenes inteligentes agregando el modificador `bfc=off` a la URL.

## ¿Qué &quot;ajuste&quot; está disponible? ¿Hay alguna configuración o comportamiento que se pueda definir? (#tuning-settings)

Actualmente, puede activar o desactivar las imágenes inteligentes de forma opcional. No hay ningún otro ajuste disponible.

## Si Imágenes inteligentes gestiona la configuración de calidad, ¿hay mínimos y máximos que podamos configurar? Por ejemplo, ¿es posible establecer &quot;no menos de 60&quot; y &quot;no más de 80 calidad buena&quot;? (#Minimum-Maximum)

No existe esta capacidad de aprovisionamiento en las imágenes inteligentes actuales.

## En algunos casos, se devuelve una imagen JPEG a Chrome en lugar de una imagen WebP. ¿Por qué pasa eso? (#jpeg-webp)

Las imágenes inteligentes determinan si la conversión es beneficiosa o no. Solo devuelve la nueva imagen si la conversión da como resultado un tamaño de archivo más pequeño con una calidad comparable.
