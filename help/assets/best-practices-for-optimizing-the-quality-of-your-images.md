---
title: Práctica recomendada para optimizar la calidad de las imágenes
description: Conozca las prácticas recomendadas para optimizar la calidad de imagen en Dynamic Media
uuid: b73f0918-c723-4a0d-a63f-4242223c2d47
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 12baf001-dfc9-410a-9821-a3bae1324392
feature: Administración de activos
role: Profesional empresarial, administrador
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 5%

---


# Práctica recomendada para optimizar la calidad de las imágenes {#best-practices-for-optimizing-the-quality-of-your-images}

La optimización de la calidad de la imagen puede ser un proceso largo, ya que muchos factores contribuyen a que se obtengan resultados aceptables. El resultado es en parte subjetivo porque las personas perciben la calidad de la imagen de manera diferente. La experimentación estructurada es clave.

AEM incluye más de 100 comandos de envío de imágenes de Dynamic Media para ajustar y optimizar imágenes y procesar resultados. Las siguientes directrices pueden ayudarle a agilizar el proceso y a obtener buenos resultados rápidamente mediante algunos comandos esenciales y prácticas recomendadas.

## Prácticas recomendadas para el formato de imagen (`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG o PNG son las mejores opciones para ofrecer imágenes de buena calidad y con un tamaño y peso manejables.
* Si no se proporciona ningún comando de formato en la URL, Dynamic Media Image Delivery toma como valor predeterminado JPG para su envío.
* JPG comprime a una proporción de 10:1 y normalmente produce tamaños de archivo de imagen más pequeños. PNG se comprime a una proporción de aproximadamente 2:1, excepto en algunos casos, como cuando las imágenes contienen un fondo blanco. Por lo general, los tamaños de archivo PNG son más grandes que los archivos JPG.
* JPG utiliza compresión con pérdidas, lo que significa que los elementos de imagen (píxeles) se pierden durante la compresión. Por otro lado, PNG utiliza compresión sin pérdidas.
* JPG a menudo comprime las imágenes fotográficas con mejor fidelidad que las imágenes sintéticas con bordes nítidos y contraste.
* Si sus imágenes contienen transparencia, utilice PNG porque JPG no admite transparencia.

Como práctica recomendada para el formato de imagen, comience con la configuración más común `&fmt=JPG`.

## Prácticas recomendadas para el tamaño de imagen {#best-practices-for-image-size}

La reducción dinámica del tamaño de la imagen es una de las tareas más comunes. Requiere especificar el tamaño y, opcionalmente, qué modo de disminución de resolución se utiliza para reducir la escala de la imagen.

* Para el tamaño de la imagen, el enfoque mejor y más directo es utilizar `&wid=<value>` y `&hei=<value>,`o solo `&hei=<value>`. Estos parámetros establecen automáticamente la anchura de la imagen según la proporción de aspecto.
* `&resMode=<value>`controla el algoritmo utilizado para la disminución de resolución. Comience con `&resMode=sharp2`. Este valor proporciona la mejor calidad de imagen. Mientras que el uso de la disminución de resolución `value =bilin` es más rápido, a menudo resulta en el alias de artefactos.

Como práctica recomendada para el tamaño de la imagen, utilice `&wid=<value>&hei=<value>&resMode=sharp2` o `&hei=<value>&resMode=sharp2`

## Prácticas recomendadas para enfocar la imagen {#best-practices-for-image-sharpening}

El enfoque de imágenes es el aspecto más complejo de controlar las imágenes en su sitio web, y donde se cometen muchos errores. Tómese el tiempo para obtener más información sobre cómo funciona la máscara de enfoque y enfoque en AEM, refiriéndose a los siguientes recursos útiles:

El documento técnico de prácticas recomendadas [Enfoque de imágenes en Adobe Dynamic Media Classic](/help/assets/assets/sharpening_images.pdf) también se aplica a AEM.

<!-- To be reviewed and updated: Broken link.
See also [Sharpening an image with unsharp mask](https://helpx.adobe.com/photoshop/atv/cs6-tutorials/sharpening-an-image-with-unsharp-mask.html). -->

Con AEM, puede enfocar las imágenes sobre la ingesta, el envío o ambos. Sin embargo, en la mayoría de los casos, las imágenes se deben enfocar utilizando solo un método o el otro, pero no ambos. Por lo general, el enfoque de imágenes en la entrega, en una dirección URL, le proporciona los mejores resultados.

Hay dos métodos de perfeccionamiento de imagen que puede utilizar:

* Perfeccionamiento simple ( `&op_sharpen`): similar al filtro de enfoque utilizado en Photoshop, el enfoque simple aplica un enfoque básico a la vista final de la imagen después del cambio de tamaño dinámico. Sin embargo, este método no es configurable por el usuario. La práctica recomendada es no utilizar &amp;op_sharpen a menos que sea necesario.
* Enmascaramiento de enfoque ( `&op_USM`): el enmascaramiento de enfoque es un filtro de enfoque estándar del sector. Se recomienda enfocar las imágenes con máscaras de enfoque siguiendo las directrices que se indican a continuación. La máscara de enfoque permite controlar los tres parámetros siguientes:

   * `&op_sharpen=`amount,radius,threshold

      * **[!UICONTROL cantidad]**  (0-5, fuerza del efecto).
      * **[!UICONTROL radius]**  (0-250, ancho de las &quot;líneas de enfoque&quot; dibujadas alrededor del objeto enfocado, medido en píxeles).

         Tenga en cuenta que los parámetros radius e amount funcionan entre sí. La reducción del radio se puede compensar aumentando la cantidad. El radio permite un control más preciso, ya que un valor inferior afila sólo los píxeles de borde, mientras que un valor más alto afila una banda más amplia de píxeles.

      * **[!UICONTROL umbral]**  (0-255, sensibilidad del efecto).

         Este parámetro determina la diferencia entre los píxeles enfocados y el área circundante antes de que se consideren píxeles de borde y el filtro los enfoque. El parámetro **[!UICONTROL threshold]** ayuda a evitar áreas de enfoque excesivo con colores similares, como los tonos de piel. Por ejemplo, un valor de umbral de 12 ignora las ligeras variaciones en el brillo del tono de la piel para evitar agregar “ruido”, mientras que al mismo tiempo agrega contraste al borde de las áreas de alto contraste, como cuando las pestañas tocan la piel.
      Para obtener más información sobre cómo configurar estos tres parámetros, incluidas las prácticas recomendadas para usar con el filtro, consulte los siguientes recursos:

      AEM tema de ayuda sobre cómo enfocar una imagen.

      Documento técnico de prácticas recomendadas [Enfoque de imágenes en Adobe Dynamic Media Classic](/help/assets/assets/sharpening_images.pdf).

   * AEM también permite controlar un cuarto parámetro: monocromo (0,1). Este parámetro determina si la máscara de enfoque se aplica a cada componente de color por separado utilizando el valor 0 o al brillo/intensidad de la imagen utilizando el valor 1.


Se recomienda comenzar con el parámetro de radio de máscara de enfoque. La configuración de radio con la que puede empezar es la siguiente:

* **[!UICONTROL Sitio web]**: 0,2-0,3 píxeles
* **[!UICONTROL Impresión fotográfica (250-300 ppi)]**: 0,3-0,5 píxeles
* **[!UICONTROL Impresión offset (266-300 ppp)]**: 0,7-1,0 píxeles
* **[!UICONTROL Impresión de lienzo (150 ppi)]**: 1,5-2,0 píxeles

Aumentar gradualmente la cantidad de 1,75 a 4. Si el enfoque sigue sin ser el que desea, aumente el radio en un punto decimal y ejecute de nuevo la cantidad de 1,75 a 4. Repita el proceso según sea necesario.

Deje el parámetro monocromo configurado en 0.

### Prácticas recomendadas para la compresión JPEG (`&qlt=`) {#best-practices-for-jpeg-compression-qlt}

* Este parámetro controla la calidad de codificación JPG. Un valor superior significa una imagen de mayor calidad pero un tamaño de archivo grande; también, un valor inferior significa una imagen de menor calidad pero un tamaño de archivo más pequeño. El rango para este parámetro es 0-100.
* Para optimizar la calidad, no establezca el valor del parámetro en 100. La diferencia entre un ajuste de 90 o 95 y 100 es casi imperceptible, pero 100 aumenta innecesariamente el tamaño del archivo de imagen. Por lo tanto, para optimizar la calidad pero evitar que los archivos de imagen sean demasiado grandes, establezca el `qlt= value` en 90 o 95.
* Para optimizar un tamaño de archivo de imagen pequeño pero mantener la calidad de imagen en un nivel aceptable, establezca el `qlt= value` en 80. Los valores por debajo de 70 a 75 producen una degradación significativa de la calidad de imagen.
* Como práctica recomendada, para permanecer en el medio, establezca el `qlt= value` en 85 para permanecer en el medio.
* Uso del indicador de croma en `qlt=`

   * El parámetro `qlt=` tiene un segundo ajuste que le permite activar la disminución de resolución de cromaticidad RGB utilizando el valor `,1` o desactivado utilizando el valor `,0`.
   * Para que sea sencillo, empiece con la disminución de resolución de cromaticidad RGB desactivada (`,0`). Este ajuste suele dar como resultado una mejor calidad de imagen, especialmente para imágenes sintéticas con muchos bordes nítidos y contraste.

Como práctica recomendada para la compresión JPG, utilice `&qlt=85,0`.

## Prácticas recomendadas para el tamaño de JPEG (`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

jpegSize es un parámetro útil si desea garantizar que una imagen no supere un tamaño determinado para su entrega a dispositivos que tengan memoria limitada.

* Este parámetro se establece en kilobytes (`jpegSize=&lt;size_in_kilobytes&gt;`). Define el tamaño máximo permitido para la entrega de imágenes.
* `&jpegSize=` interactúa con el parámetro de compresión JPG  `&qlt=`. Si la respuesta JPG con el parámetro de compresión JPG especificado (`&qlt=`) no supera el valor jpegSize, la imagen se devuelve con `&qlt=` como se ha definido. De lo contrario, `&qlt=` se reduce gradualmente hasta que la imagen se ajusta al tamaño máximo permitido, o hasta que el sistema determine que no se puede ajustar y devuelva un error.

Como práctica recomendada, establezca `&jpegSize=` y añada el parámetro `&qlt=` si está entregando imágenes JPG a dispositivos con memoria limitada.

## Resumen de prácticas recomendadas {#best-practices-summary}

Como práctica recomendada, para lograr una alta calidad de imagen y un tamaño de archivo pequeño, comience con la siguiente combinación de parámetros:

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

Esta combinación de configuraciones de productos excelentes resultados en la mayoría de las circunstancias.

Si la imagen requiere mayor optimización, ajuste gradualmente los parámetros de nitidez (máscara de enfoque) empezando por un radio definido en 0,2 o 0,3. A continuación, aumente gradualmente la cantidad de 1,75 a un máximo de 4 (equivalente al 400 % en Photoshop). Compruebe que se logra el resultado deseado.

Si los resultados de nitidez siguen siendo insatisfactorios, aumente el radio en incrementos decimales. Para cada incremento decimal, reinicie la cantidad a 1,75 y aumente gradualmente a 4. Repita este proceso hasta obtener el resultado deseado. Aunque los valores anteriores son un enfoque que los estudios creativos han validado, recuerde que puede empezar con otros valores y seguir otras estrategias. Si los resultados son satisfactorios para usted o no es un asunto subjetivo, por lo tanto la experimentación estructurada es clave.

A medida que experimenta, también puede encontrar útiles las siguientes sugerencias generales para optimizar el flujo de trabajo:

* Pruebe diferentes parámetros en tiempo real, directamente en una dirección URL.
* Como práctica recomendada, recuerde que puede agrupar los comandos de Dynamic Media Image Serving en un ajuste preestablecido de imagen. Un ajuste preestablecido de imagen es básicamente macros de comandos de URL con nombres preestablecidos personalizados como `$thumb_low$` y `&product_high$`. El nombre de ajuste preestablecido personalizado en una ruta URL hace una llamada a estos ajustes preestablecidos. Esta funcionalidad le ayuda a administrar los comandos y la configuración de calidad para diferentes patrones de uso de imágenes en su sitio web y acorta la longitud total de las direcciones URL.
* AEM también proporciona métodos más avanzados para ajustar la calidad de imagen, como la aplicación de imágenes de nitidez durante la ingesta. En los casos de uso avanzado en los que esta opción pueda ajustar y optimizar los resultados de procesamiento, [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html) puede ayudarle con las prácticas recomendadas y la perspectiva personalizada.

