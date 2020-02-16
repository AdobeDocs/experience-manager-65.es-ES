---
title: Biblioteca de transcodificación de imágenes
description: Descubra cómo configurar y utilizar la biblioteca de transcodificación de imágenes de Adobe, una solución de procesamiento de imágenes que puede realizar funciones básicas de gestión de imágenes, como codificación, transcodificación, remuestreo de imágenes y cambio de tamaño de imágenes.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Biblioteca de transcodificación de imágenes {#imaging-transcoding-library}

La biblioteca de transcodificación de imágenes de Adobe es una solución de procesamiento de imágenes propiedad que puede realizar funciones básicas de gestión de imágenes, entre las que se incluyen:

* Codificación
* Transcodificación (conversión de formatos admitidos)
* Remuestreo de imágenes mediante algoritmos PS e Intel IPP
* Profundidad de bits y conservación del perfil de color
* Compresión de calidad JPEG
* Cambio de tamaño de imagen

La biblioteca de transcodificación de imágenes ofrece compatibilidad con CMYK y alfa completa, excepto CMYK -Alpha.

Además de admitir una amplia gama de perfiles y formatos de archivo, la biblioteca de transcodificación de imágenes tiene ventajas significativas con respecto a otras soluciones de terceros en cuanto a rendimiento, escalabilidad y calidad. Estas son algunas de las ventajas clave del uso de la biblioteca de transcodificación de imágenes:

* **Escala con un tamaño de archivo o una resolución** crecientes: El escalado se logra principalmente gracias a la capacidad patentada de la biblioteca de transcodificación de imágenes para cambiar el tamaño al descodificar archivos. Esta capacidad garantiza que el uso de la memoria en tiempo de ejecución siempre es óptimo y no es una función cuadrática de aumento del tamaño del archivo o de resolución de megapíxeles. La biblioteca de transcodificación de imágenes puede procesar archivos de mayor tamaño y alta resolución (con megapíxeles más altos). Las herramientas de terceros, como ImageMagick, no pueden gestionar archivos grandes ni bloqueos mientras procesan dichos archivos.
* **Algoritmos** de compresión y cambio de tamaño de la calidad de Photoshop: Coherencia con el estándar de la industria en términos de calidad del muestreo de bajada (suave, nítida y automática bicúbica) y calidad de compresión. La biblioteca de transcodificación de imágenes evalúa aún más el factor de calidad de la imagen de entrada y utiliza de forma inteligente tablas y ajustes de calidad óptimos para la imagen de salida. Esta capacidad produce archivos de tamaño óptimo sin comprometer la calidad visual.
* **** Alto rendimiento: El tiempo de respuesta es menor y el rendimiento es siempre mayor que ImageMagick. Por lo tanto, la biblioteca de transcodificación de imágenes debería reducir el tiempo de espera de los usuarios y el coste del alojamiento.
* **** Escalar mejor con carga simultánea: La biblioteca de transcodificación de imágenes funciona de forma óptima en condiciones de carga simultánea. Proporciona un alto rendimiento con rendimiento óptimo de la CPU, uso de memoria y tiempo de respuesta bajo, lo que ayuda a reducir el costo del alojamiento.

## Supported platforms {#supported-platforms}

La biblioteca de transcodificación de imágenes solo está disponible para las distribuciones RHEL 7 y CentOS 7.

>[!NOTE]
>
>Mac OS y otras distribuciones *nix (por ejemplo, Debian y Ubuntu) no son compatibles.

## Uso {#usage}

Los argumentos de la línea de comandos para la biblioteca de transcodificación de imágenes pueden incluir lo siguiente:

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth ‘4’ is automatically converted to ‘8’
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

Puede configurar las siguientes opciones para el `-resize` parámetro:

* `X`: `Works similar to AEM. For example -resize 319.`
* `WxH`: `Aspect Ratio will not be maintained, For example -resize 319X319.`
* `Wx`: `Fixes the width and calculates the height maintaining the aspect ratio. For example -resize 319x.`
* `xH`: `Fixes the height and calculates the width maintaining the aspect ratio. For example -resize x319.`

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## Configurar la biblioteca de transcodificación de imágenes {#configuring-imaging-transcoding-library}

Para configurar el procesamiento del DIT, cree un archivo de configuración y actualice el flujo de trabajo para ejecutarlo.

### Crear archivo de configuración para el paquete extraído {#create-conf-file}

Para configurar la biblioteca, cree un archivo .conf para indicar las bibliotecas siguiendo los pasos siguientes. Necesita permisos de administrador o raíz.

1. Descargue el paquete [Biblioteca de transcodificación de](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) imágenes e instálelo mediante el Administrador de paquetes. El paquete es compatible con AEM 6.5.

1. Para conocer un ID de paquete para `com.day.cq.dam.cq-dam-switchengine`, inicie sesión en la consola web y toque **[!UICONTROL OSGi > Paquetes]**. Como alternativa, para abrir la consola de paquetes, acceda a la `https://[aem_server:[port]/system/console/bundles/` URL. Busque `com.day.cq.dam.cq-dam-switchengine` el paquete y su ID.

1. Asegúrese de que se extraen todas las bibliotecas necesarias marcando la carpeta con el comando `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`, donde el nombre de la carpeta se construye con el ID del paquete. Por ejemplo, el comando es `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` si el ID del paquete es `588`.

1. Cree un `SWitchEngineLibs.conf` archivo para vincularlo a la biblioteca.

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. Agregue `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` path al archivo conf usando el `cat SWitchEngineLibs.conf` comando .

1. Ejecutar `ldconfig` para crear los vínculos y la caché necesarios.

1. En la cuenta que se utiliza para iniciar AEM, edite el `.bash_profile` archivo. Agregue `LD_LIBRARY_PATH` lo siguiente:

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. Para asegurarse de que el valor de la ruta está establecido en `.`, utilice `echo $LD_LIBRARY_PATH` command. El resultado debería ser `.`. Si el valor no está establecido en `.`, reinicie la sesión.

### Configurar el flujo de trabajo de recursos de actualización DAM {#configure-dam-asset-update-workflow}

Actualice el flujo de trabajo de recursos [!UICONTROL de actualización de] DAM para utilizar la biblioteca para procesar imágenes.

1. Toque o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Herramientas > Flujo de trabajo > Modelos]**.

1. En la página Modelos **[!UICONTROL de]** flujo de trabajo, abra el modelo de flujo de trabajo de recursos **[!UICONTROL de actualización de]** DAM en modo de edición.

1. Abra el paso **[!UICONTROL del proceso de flujo de trabajo Miniaturas]** de proceso. En la ficha **[!UICONTROL Miniaturas]** , agregue los tipos MIME para los que desea omitir el proceso de generación de miniaturas predeterminado en la lista **[!UICONTROL Omitir tipos]** de MIME.
Por ejemplo, si desea crear miniaturas para una imagen TIFF con la biblioteca de transcodificación de imágenes, especifique `image/tiff` en el campo **[!UICONTROL Omitir tipos]** de MIME.

1. En la ficha Imagen **[!UICONTROL habilitada para]** Web, agregue los tipos MIME para los que desea omitir el proceso predeterminado de generación de representaciones Web en **[!UICONTROL Omitir lista]**. Por ejemplo, si ha omitido el tipo MIME `image/tiff` en el paso anterior, agregue `image/tiff` a la lista de omisiones.

1. Abra el paso de las miniaturas **[!UICONTROL EPS (con tecnología ImageMagick)]** y vaya a la ficha **[!UICONTROL Argumentos]** . En la lista Tipos **[!UICONTROL de]** MIME, agregue los tipos MIME que desea que la biblioteca de transcodificación de imágenes procese. Por ejemplo, si ha omitido el tipo MIME `image/tiff` en el paso anterior, agregue `image/jpeg` a la lista Tipos **[!UICONTROL de]** MIME.

1. Elimine los comandos predeterminados si los hay.

1. Alterne el panel lateral y, en la lista de pasos, agregue **[!UICONTROL SWitchEngine Handler]**.

1. Agregue comandos al controlador [!UICONTROL SwitchEngine] en función de los requisitos personalizados. Ajuste los parámetros de los comandos que especifique para satisfacer sus necesidades. Por ejemplo, si desea conservar el perfil de color de la imagen JPEG, agregue los siguientes comandos a la lista **[!UICONTROL Comandos]** :

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`
   ![chlimage](assets/chlimage_1-199.png)

1. (Opcional) Genere miniaturas a partir de una representación intermedia mediante un único comando. La representación intermedia actúa como fuente para generar representaciones estáticas y web. Este método es más rápido que el método anterior. Sin embargo, no se pueden aplicar parámetros personalizados a las miniaturas mediante este método.

   ![chlimage](assets/chlimage_1-200.png)

1. Para generar representaciones web, configure los parámetros en la ficha Imagen **[!UICONTROL habilitada para]** Web.

1. Sincronice el modelo de flujo de trabajo de recursos [!UICONTROL de actualización de] DAM actualizado. Guarde el flujo de trabajo.

El usuario verifica la configuración, carga una imagen TIFF y supervisa el archivo error.log. Observará `INFO` mensajes con menciones de `SwitchEngineHandlingProcess execute: executing command line`. Los registros mencionan las representaciones generadas. Una vez completado el flujo de trabajo, puede ver las nuevas representaciones en AEM.

>[!MORELIKETHIS]
>
>* [Artículo de tipos MIME admitidos](assets-formats.md#supported-image-transcoding-library)