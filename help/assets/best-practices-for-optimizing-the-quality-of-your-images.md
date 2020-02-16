---
title: Prácticas recomendadas para optimizar la calidad de las imágenes
description: Conozca las prácticas recomendadas para optimizar la calidad de imagen en Dynamic Media
uuid: b73f0918-c723-4a0d-a63f-4242223c2d47
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 12baf001-dfc9-410a-9821-a3bae1324392
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Prácticas recomendadas para optimizar la calidad de las imágenes {#best-practices-for-optimizing-the-quality-of-your-images}

La optimización de la calidad de la imagen puede ser un proceso lento, ya que muchos factores contribuyen a obtener resultados aceptables. El resultado es en parte subjetivo porque las personas perciben la calidad de imagen de manera diferente. La clave es la experimentación estructurada.

AEM incluye más de 100 comandos de distribución de imágenes de Dynamic Media para ajustar y optimizar imágenes y procesar resultados. Las siguientes directrices pueden ayudarle a agilizar el proceso y a obtener buenos resultados rápidamente mediante algunos comandos esenciales y prácticas recomendadas.

## Prácticas recomendadas para el formato de imagen (`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG o PNG son las mejores opciones para ofrecer imágenes de buena calidad y con un tamaño y peso manejables.
* Si no se proporciona ningún comando de formato en la URL, la entrega de imágenes de Dynamic Media tiene el valor predeterminado JPG para la entrega.
* JPG comprime a una proporción de 10:1 y normalmente produce archivos de imagen más pequeños. PNG se comprime a una proporción de aproximadamente 2:1, excepto en algunos casos, como cuando las imágenes contienen un fondo blanco. Normalmente, los tamaños de archivo PNG son mayores que los archivos JPG.
* JPG utiliza compresión con pérdida, lo que significa que los elementos de imagen (píxeles) se pierden durante la compresión. Por otro lado, PNG utiliza compresión sin pérdida.
* JPG a menudo comprime imágenes fotográficas con mejor fidelidad que las imágenes sintéticas con bordes nítidos y contraste.
* Si las imágenes contienen transparencia, utilice PNG porque JPG no admite transparencia.

Como práctica recomendada para el formato de imagen, comience con la configuración más común `&fmt=JPG`.

## Prácticas recomendadas para el tamaño de imagen {#best-practices-for-image-size}

La reducción dinámica del tamaño de la imagen es una de las tareas más comunes. Implica especificar el tamaño y, opcionalmente, qué modo de disminución de resolución se utiliza para reducir la escala de la imagen.

* Para cambiar el tamaño de la imagen, el mejor método y el más sencillo es usar `&wid=<value>` y `&hei=<value>,`o simplemente `&hei=<value>`. Estos parámetros establecen automáticamente la anchura de la imagen según la proporción de aspecto.
* `&resMode=<value>`controla el algoritmo utilizado para la disminución de resolución. Empiece por `&resMode=sharp2`. Este valor proporciona la mejor calidad de imagen. Aunque el uso de la disminución de resolución `value =bilin` es más rápido, a menudo resulta en el solapamiento de artefactos.

Como práctica recomendada para cambiar el tamaño, el uso `&wid=<value>&hei=<value>&resMode=sharp2` o `&hei=<value>&resMode=sharp2`

## Prácticas recomendadas para el enfoque de imágenes {#best-practices-for-image-sharpening}

El enfoque de imágenes es el aspecto más complejo del control de imágenes en el sitio web y en el que se cometen muchos errores. Tómese el tiempo para conocer mejor cómo funciona el enfoque y la máscara de enfoque en AEM, haciendo referencia a los siguientes recursos útiles:

Documento técnico de prácticas recomendadas [Enfoque de imágenes en Adobe Scene7 Publishing System y en el servidor](/help/assets/assets/s7_sharpening_images.pdf) de imágenes también se aplica a AEM.

Consulte también [Enfoque de imágenes con máscara](https://helpx.adobe.com/photoshop/atv/cs6-tutorials/sharpening-an-image-with-unsharp-mask.html)de enfoque.

Con AEM, puede enfocar imágenes durante la ingesta, la entrega o ambos. En la mayoría de los casos, sin embargo, debe enfocar las imágenes utilizando solo un método o el otro, pero no ambos. El enfoque de imágenes durante la entrega, en una dirección URL, normalmente proporciona los mejores resultados.

Existen dos métodos de enfoque de imagen que puede utilizar:

* Enfoque simple ( `&op_sharpen`): similar al filtro de enfoque utilizado en Photoshop, el enfoque simple aplica enfoque básico a la vista final de la imagen tras el cambio de tamaño dinámico. Sin embargo, este método no es configurable por el usuario. La práctica recomendada es no utilizar &amp;op_sharpen a menos que sea necesario.
* Máscara de enfoque ( `&op_USM`): la máscara de enfoque es un filtro de enfoque estándar del sector. Lo mejor es enfocar imágenes con máscaras de enfoque siguiendo las directrices que se describen a continuación. La máscara de enfoque permite controlar los tres parámetros siguientes:

   * `&op_sharpen=`cantidad,radio,umbral

      * **[!UICONTROL cantidad]** (0-5, intensidad del efecto).
      * **[!UICONTROL radio]** (0-250, anchura de las &quot;líneas de enfoque&quot; dibujadas alrededor del objeto enfocado, medida en píxeles).

         Tenga en cuenta que el radio y la cantidad de parámetros funcionan entre sí. La reducción del radio se puede compensar aumentando la cantidad. Radio permite un control más preciso, ya que un valor inferior enfoca solo los píxeles del borde, mientras que un valor superior enfoca una banda más ancha de píxeles.

      * **[!UICONTROL umbral]** (0-255, sensibilidad del efecto).

         Este parámetro determina la diferencia entre los píxeles enfocados y el área circundante antes de que se consideren píxeles de borde y el filtro los enfoque. El parámetro de **[!UICONTROL umbral]** ayuda a evitar áreas de enfoque excesivo con colores similares, como los tonos de piel. Por ejemplo, un valor de umbral de 12 ignora las ligeras variaciones en el brillo del tono de la piel para evitar agregar &quot;ruido&quot;, mientras que al mismo tiempo agrega contraste al borde de las áreas de alto contraste, como cuando las pestañas tocan la piel.
      Para obtener más información sobre cómo se configuran estos tres parámetros, incluidas las prácticas recomendadas para usar con el filtro, consulte los siguientes recursos:

      Tema de ayuda de AEM sobre cómo enfocar una imagen.

      Documento técnico de prácticas recomendadas [Enfoque de imágenes en Adobe Scene7 Publishing System y en el servidor](/help/assets/assets/s7_sharpening_images.pdf)de imágenes.

   * AEM también le permite controlar un cuarto parámetro: monocromo (0,1). Este parámetro determina si la máscara de enfoque se aplica a cada componente de color por separado utilizando el valor 0 o al brillo/intensidad de la imagen con el valor 1.


La práctica recomendada es comenzar con el parámetro de radio de máscara de enfoque. Los ajustes de radio con los que puede comenzar son los siguientes:

* **[!UICONTROL Sitio web]**: 0,2-0,3 píxeles
* **[!UICONTROL Impresión fotográfica (250-300 ppp)]**: 0,3-0,5 píxeles
* **[!UICONTROL Impresión offset (266-300 ppp)]**: 0,7-1,0 píxeles
* **[!UICONTROL Impresión de lienzo (150 ppp)]**: 1,5-2,0 píxeles

Aumentar gradualmente la cantidad de 1,75 a 4. Si el enfoque sigue sin ser el deseado, aumente el radio en un punto decimal y vuelva a ejecutar la cantidad de 1,75 a 4. Repita el procedimiento según sea necesario.

Deje la configuración del parámetro monocromo en 0.

### Prácticas recomendadas para la compresión JPEG (`&qlt=`) {#best-practices-for-jpeg-compression-qlt}

* Este parámetro controla la calidad de codificación JPG. Un valor mayor significa una imagen de mayor calidad pero un tamaño de archivo grande; de forma alternativa, un valor más bajo significa una imagen de menor calidad pero un tamaño de archivo más pequeño. El intervalo para este parámetro es 0-100.
* Para optimizar la calidad, no establezca el valor del parámetro en 100. La diferencia entre un ajuste de 90 ó 95 y 100 es casi imperceptible, pero 100 aumenta innecesariamente el tamaño del archivo de imagen. Por lo tanto, para optimizar la calidad pero evitar que los archivos de imagen sean demasiado grandes, establezca el valor `qlt= value` en 90 o 95.
* Para optimizar un tamaño de archivo de imagen pequeño pero mantener la calidad de imagen en un nivel aceptable, defina el valor `qlt= value` en 80. Los valores por debajo de 70 a 75 degradan significativamente la calidad de imagen.
* Como práctica recomendada, para quedarse en el medio, `qlt= value` a 85 para quedarse en el medio.
* Uso del indicador de croma en `qlt=`

   * El `qlt=` parámetro tiene un segundo ajuste que le permite activar la disminución de resolución de cromaticidad RGB utilizando el valor `,1` o desactivando mediante el valor `,0`.
   * Para que sea sencillo, comience con la disminución de resolución de cromaticidad RGB desactivada (`,0`). Este ajuste suele dar como resultado una mejor calidad de imagen, especialmente para imágenes sintéticas con muchos bordes nítidos y contraste.

Como práctica recomendada para el uso de compresión JPG `&qlt=85,0`.

## Prácticas recomendadas para el tamaño JPEG (`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

jpegSize es un parámetro útil si desea garantizar que una imagen no supere un tamaño determinado para la entrega a dispositivos con memoria limitada.

* Este parámetro se establece en kilobytes (`jpegSize=&lt;size_in_kilobytes&gt;`). Define el tamaño máximo permitido para la entrega de imágenes.
* `&jpegSize=` interactúa con el parámetro de compresión JPG `&qlt=`. Si la respuesta JPG con el parámetro de compresión JPG especificado (`&qlt=`) no supera el valor jpegSize, la imagen se devuelve con la `&qlt=` definición definida. De lo contrario, `&qlt=` se reduce gradualmente hasta que la imagen se ajuste al tamaño máximo permitido o hasta que el sistema determine que no cabe y devuelva un error.

Como práctica recomendada, establezca `&jpegSize=` y agregue el parámetro `&qlt=` si va a enviar imágenes JPG a dispositivos con memoria limitada.

## Resumen de prácticas recomendadas {#best-practices-summary}

Como práctica recomendada, para lograr una alta calidad de imagen y un tamaño de archivo pequeño, comience con la siguiente combinación de parámetros:

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

Esta combinación de configuraciones produce excelentes resultados en la mayoría de las circunstancias.

Si la imagen requiere optimización adicional, ajuste gradualmente los parámetros de enfoque (máscara de enfoque) comenzando con un radio definido en 0,2 o 0,3. A continuación, aumente gradualmente la cantidad de 1,75 a un máximo de 4 (equivalente al 400 % en Photoshop). Compruebe que se ha logrado el resultado deseado.

Si los resultados de enfoque siguen siendo insatisfactorios, aumente el radio en incrementos decimales. Para cada incremento decimal, reinicie la cantidad a 1,75 y aumente gradualmente a 4. Repita este proceso hasta que alcance el resultado deseado. Aunque los valores anteriores son un enfoque que los estudios creativos han validado, recuerde que puede empezar con otros valores y seguir otras estrategias. Si los resultados son satisfactorios para usted o no es un asunto subjetivo, por lo tanto la experimentación estructurada es clave.

A medida que experimenta, también puede encontrar las siguientes sugerencias generales útiles para optimizar el flujo de trabajo:

* Pruebe distintos parámetros en tiempo real, ya sea directamente en una URL o mediante la función de ajuste de imagen de Scene7 Publishing System, que proporciona vistas previas en tiempo real para las operaciones de ajuste.
* Como práctica recomendada, recuerde que puede agrupar comandos de servicio de imágenes de Dynamic Media en un ajuste preestablecido de imagen. Un ajuste preestablecido de imagen es básicamente macros de comandos de URL con nombres de ajustes preestablecidos personalizados como `$thumb_low$` y `&product_high$`. El nombre de ajuste preestablecido personalizado en una ruta de URL hace una llamada a estos ajustes preestablecidos. Esta funcionalidad le ayuda a administrar los comandos y la configuración de calidad para los distintos patrones de uso de imágenes en el sitio web y acorta la longitud total de las direcciones URL.
* AEM también ofrece métodos más avanzados para ajustar la calidad de imagen, como la aplicación de imágenes de enfoque durante la ingesta. En los casos de uso avanzado en los que esta opción puede mejorar y optimizar los resultados del procesamiento, [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html) puede ayudarle con las prácticas recomendadas y la perspectiva personalizada.

