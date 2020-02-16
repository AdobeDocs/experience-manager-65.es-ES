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
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Imágenes inteligentes {#smart-imaging}

## ¿Qué son las imágenes inteligentes? {#what-is-smart-imaging}

Las imágenes inteligentes aprovechan las características de visualización únicas de cada usuario para ofrecer automáticamente las imágenes correctas optimizadas para su experiencia, lo que mejora el rendimiento y la participación. Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes y utilizan la inteligencia en el último milisegundo de la publicación para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión de red o del navegador.

Las imágenes inteligentes se benefician del aumento de rendimiento añadido de la integración total con el mejor servicio CDN de primera categoría. Este servicio encuentra la ruta de Internet óptima entre servidores, redes y puntos de interrelación que tiene la latencia y/o la tasa de pérdida de paquetes más baja que la ruta predeterminada en Internet.

## ¿Cuáles son los beneficios clave de las imágenes inteligentes? {#what-are-the-key-benefits-of-smart-imaging}

Las imágenes inteligentes ofrecen un mejor rendimiento de entrega de imágenes al optimizar automáticamente el tamaño de archivo de imagen en función de las características del usuario. Dado que las imágenes constituyen la mayor parte del tiempo de carga de una página, la mejora del rendimiento puede tener un impacto profundo en los KPI comerciales, como una mayor conversión, tiempo invertido en el sitio, una menor tasa de salida hacia otro sitio, etc. Adobe comparó el rendimiento de la entrega de imágenes predeterminada con las imágenes inteligentes en diferentes formatos de archivo, navegadores y ajustes de calidad (QLT). En general, puede esperar una mejora del rendimiento del 22 al 47 % en función de los ajustes preestablecidos de imagen existentes y de las características específicas del usuario final.

![image2017-11-14_133226](assets/image2017-11-14_133226.png)

## ¿Hay algún costo de licencia asociado con las imágenes inteligentes? {#are-there-any-licensing-costs-associated-with-smart-imaging}

No. Las imágenes inteligentes se incluyen con la licencia existente de Dynamic Media Classic (Scene7) o Dynamic Media. No hay costos adicionales que aprovechar esta nueva función.

## ¿Cómo funcionan las imágenes inteligentes? {#how-does-smart-imaging-work}

Cuando un consumidor solicita una imagen por primera vez, comprobamos las características del usuario y la convertimos al formato de imagen adecuado según el navegador. Además, creamos simultáneamente todas las conversiones de formato que luego se almacenan en caché en la CDN. Cuando los consumidores de distintos navegadores solicitan posteriormente esa imagen, el formato de imagen adecuado se entrega automáticamente directamente desde la caché de CDN. Estas conversiones de formato se realizan sin pérdidas, lo que no degrada la fidelidad visual. Las imágenes inteligentes convierten automáticamente las imágenes en diferentes formatos según la capacidad del navegador:

* Convierta automáticamente a WebP sin pérdida para navegadores que admitan formato WebP, como Chrome, Android y Opera.
* Convertir automáticamente a JPEGXR sin pérdida para navegadores que admitan formato JPEGXR, como Internet Explorer 9+.
* Convierta automáticamente a JPEG2000 sin pérdida para navegadores que admitan formato JPEG2000, como Safari.
* Para los exploradores que no admiten estos formatos, se proporciona el formato de imagen solicitado originalmente.

## ¿Qué formatos de imagen se admiten? {#what-image-formats-are-supported}

Para las imágenes inteligentes se admiten los siguientes formatos de imagen:

* RGB JPEG
* PNG RGB
* TIFF RGB
* JPEG CMYK
* TIFF CMYK

## ¿Cómo funcionan las imágenes inteligentes con los ajustes preestablecidos de imagen que ya se están utilizando? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes y observan prácticamente todos los ajustes de imagen, como el tamaño, la calidad, el enfoque, etc. Lo que cambiará es el formato de imagen o, en caso de velocidad de conexión de red lenta, el ajuste de calidad. Para la conversión de formato, mantenemos la fidelidad visual total definida por la configuración de ajustes preestablecidos de imagen, pero con un tamaño de archivo más pequeño.

Por ejemplo, supongamos que se define un ajuste preestablecido de imagen con formato JPEG, tamaño 500 x 500, calidad = 85 y máscara de enfoque = 0,1,1,5. Cuando detectamos que un usuario está en el navegador Chrome, la imagen se convierte al formato WebP sin pérdida, con un tamaño de 500 x 500, calidad = 85 y máscara de enfoque = 0,1,1,5.

## ¿Tendré que cambiar direcciones URL, ajustes preestablecidos de imagen o implementar código nuevo en mi sitio para imágenes inteligentes? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

No. Las imágenes inteligentes funcionan perfectamente con las direcciones URL y los ajustes preestablecidos de imagen existentes. Además, las imágenes inteligentes no requieren que agregue código en el sitio web para detectar diferentes características de usuario (explorador, ancho de banda, dispositivo, etc.). Adobe gestiona todo esto automáticamente.

El único cambio que puede ser necesario es actualizar el ajuste **[!UICONTROL Tiempo de vida]** (TTL). Esta configuración define la duración de la caché de los recursos por parte de la CDN. Para maximizar las mejoras de rendimiento de las imágenes inteligentes, Adobe recomienda establecer el TTL en 24 horas o más. Para cambiar esta configuración:

* Si utiliza Dynamic Media Classic, toque **[!UICONTROL Ajustes > Ajustes de aplicación > Ajustes de publicación > Servidor]** de imágenes. Establezca el valor **[!UICONTROL Predeterminado de Tiempo de espera de cliente en Activo]** en 24 o más.

* Si utiliza Dynamic Media, siga las instrucciones para [configurar](config-dynamic.md) la imagen de Dynamic Media. Establezca el valor de **[!UICONTROL caducidad]** en 24 horas o más.

>[!NOTE]
>
>Si establece TTL &lt;= 1 hora, las imágenes inteligentes no funcionan.

## ¿Funcionan las imágenes inteligentes con HTTPS? ¿Qué tal HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

Las imágenes inteligentes funcionan con imágenes enviadas a través de HTTP o HTTPS. Además, también funciona a través de HTTP/2.

## ¿Puedo usar imágenes inteligentes? {#am-i-eligible-to-use-smart-imaging}

Para utilizar imágenes inteligentes, la cuenta de AEM de Dynamic Media Classic o Dynamic Media de su empresa debe cumplir los siguientes requisitos:

* Utilice la CDN (Red de entrega de contenido) incluida en Adobe como parte de su licencia.
* Utilice un dominio dedicado (es decir, `images.company.com` o `mycompany.scene7.com`), no un dominio genérico (es decir, `s7d1.scene7.com`, `s7d2.scene7.com`o `s7d13.scene7.com`).

   Para encontrar los dominios, inicie sesión en la cuenta o cuentas de la empresa.

   Toque **[!UICONTROL Ajustes > Ajustes de aplicación > Configuración]** general. Busque el campo con la etiqueta Nombre **[!UICONTROL del servidor]** publicado. Si actualmente está utilizando un dominio genérico, puede solicitar el traslado a su propio dominio personalizado como parte de esta transición.

* No solicite imágenes JPEG CMYK. Como parte de su procesamiento, las imágenes inteligentes convierten imágenes JPEG CMYK en RGB. Si necesita obtener imágenes JPEG CMYK, no puede utilizar imágenes inteligentes.

## ¿Cuál es el proceso para habilitar las imágenes inteligentes en mi cuenta? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Debe iniciar la solicitud para utilizar imágenes inteligentes; no se habilita automáticamente.

1. Iniciar una solicitud de asistencia técnica (correo electrónico: s7support@adobe.com).
1. Proporcione la siguiente información en su solicitud de asistencia:

   1. Nombre de contacto principal, correo electrónico, teléfono.
   1. Todos los dominios que se van a habilitar para las imágenes inteligentes (es decir, imágenes.empresa.com o miempresa.escena7.com).

      Para encontrar los dominios, inicie sesión en la cuenta o cuentas de la empresa.

      Haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Configuración]** general.

      Busque el campo con la etiqueta Nombre **[!UICONTROL del servidor]** publicado.
   1. Compruebe que está utilizando la CDN a través de Adobe y que no se administra con una relación directa.
   1. Compruebe que está utilizando un dominio dedicado como `images.company.com` o `mycompany.scene7.com`, y no un dominio genérico, como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Para encontrar los dominios, inicie sesión en la cuenta o cuentas de la empresa.

      Haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Configuración]** general.

      Busque el campo con la etiqueta Nombre **[!UICONTROL del servidor]** publicado. Si actualmente está utilizando un dominio genérico de Dynamic Media Classic, puede solicitar el traslado a su propio dominio personalizado como parte de esta transición.
   1. Indique si también necesita que esto funcione con HTTP/2

1. La asistencia técnica le agregará a la lista de espera de cliente de imágenes inteligentes en función del orden en que se enviaron las solicitudes.
1. Cuando Adobe esté preparado para gestionar su solicitud, el servicio de asistencia técnica se pondrá en contacto con usted para coordinar y establecer una fecha objetivo.
1. Opcional: Tiene la opción de probar las imágenes inteligentes en Ensayo antes de que Adobe implemente la nueva función en producción.
1. Se le notifica después de completarlo mediante soporte técnico.
1. Para maximizar las mejoras de rendimiento de las imágenes inteligentes, Adobe recomienda establecer el Tiempo de vida (TTL) en 24 horas o más. El TTL define cuánto tiempo los recursos se almacenan en caché en la CDN. Para cambiar esta configuración:

   1. Si utiliza Dynamic Media Classic, haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Ajustes de publicación > Servidor]** de imágenes. Establezca el valor **[!UICONTROL Predeterminado de Tiempo de espera de cliente en Activo]** en 24 o más.
   1. Si utiliza Dynamic Media, siga [estas instrucciones](config-dynamic.md). Establezca el valor **[!UICONTROL Caducidad]** en 24 horas o más.

## ¿Cuándo puedo esperar que mi cuenta esté habilitada con imágenes inteligentes? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

Las solicitudes se procesan en el orden en que son recibidas por la asistencia técnica, según la lista de espera.

>[!NOTE]
Puede haber un largo tiempo de espera, ya que la activación de imágenes inteligentes implica la eliminación de la caché. Por lo tanto, solo se pueden gestionar algunas transiciones de cliente en un momento dado.

## ¿Cuáles son los riesgos de cambiar para utilizar imágenes inteligentes? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

La transición a imágenes inteligentes borra la caché en CDN porque implica pasar a una nueva configuración de Dynamic Media Classic o Dynamic Media en AEM.

Durante la transición inicial, las imágenes no almacenadas en caché llegan directamente a los servidores de origen de Adobe hasta que se vuelve a crear la caché. Debido a esto, Adobe tiene previsto gestionar algunas transiciones de clientes a la vez, de modo que se mantenga un rendimiento aceptable al extraer solicitudes de nuestro origen. Para la mayoría de los clientes, la caché se vuelve a crear completamente en la CDN en ~1 a 2 días.

## ¿Cómo puedo verificar si las imágenes inteligentes funcionan correctamente?  {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Una vez configurada la cuenta con imágenes inteligentes, cargue una URL de imagen de Dynamic Media Classic(S7)/Dynamic Media en el explorador.
1. Abra el panel del desarrollador de Chrome haciendo clic en **[!UICONTROL Ver > Desarrollador > Herramientas]** para desarrolladores en el navegador. O elija la herramienta de desarrollo de navegador que desee.

1. Asegúrese de que la caché está deshabilitada cuando las herramientas de desarrollo están abiertas.

   1. En Windows, vaya a la configuración del panel de herramientas del desarrollador y, a continuación, seleccione la casilla de verificación **[!UICONTROL Deshabilitar caché (mientras devtools está abierto)]** .
   1. En Mac, en el panel del desarrollador, en la ficha **[!UICONTROL Red]** , seleccione **[!UICONTROL deshabilitar la caché]** .

1. En la solicitud inicial, la imagen no se optimizará. Normalmente, se tardan unos 15 minutos en devolver la imagen optimizada si no está en la caché de CDN.
1. Observe que el tipo de contenido se transforma al formato adecuado. La siguiente captura de pantalla muestra la imagen PNG que se está convirtiendo dinámicamente a WebP en Chrome.
1. Repita esta prueba en diferentes exploradores y condiciones de usuario.

>[!NOTE]
No se convierten todas las imágenes. Las imágenes inteligentes deciden si se necesita la conversión para mejorar el rendimiento. En algunos casos, cuando no hay una ganancia de rendimiento esperada, la imagen no se convierte.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

