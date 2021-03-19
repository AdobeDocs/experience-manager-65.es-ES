---
title: Biblioteca de transcodificación de imágenes
description: Aprenda a configurar y utilizar la biblioteca de transcodificación de imágenes de Adobe, una solución de procesamiento de imágenes que puede realizar funciones básicas de gestión de imágenes, como codificación, transcodificación, remuestreo de imágenes y cambio de tamaño de imágenes.
contentOwner: AG
role: Administrador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 0%

---


# Biblioteca de transcodificación de imágenes {#imaging-transcoding-library}

La biblioteca de transcodificación de imágenes de Adobe es una solución de procesamiento de imágenes propietaria que puede realizar funciones básicas de gestión de imágenes, entre las que se incluyen:

* Codificación
* Transcodificación (conversión de formatos admitidos)
* Remuestreo de imágenes mediante algoritmos PS e Intel IPP
* Profundidad de bits y conservación de perfiles de color
* Compresión de calidad JPEG
* Cambio de tamaño de la imagen

La biblioteca de transcodificación de imágenes proporciona compatibilidad con CMYK y compatibilidad con alfa completa, excepto CMYK -Alpha.

Además de admitir una amplia gama de formatos y perfiles de archivo, la biblioteca de transcodificación de imágenes tiene ventajas significativas con respecto a otras soluciones de terceros en lo que respecta al rendimiento, la escalabilidad y la calidad. Estas son algunas de las ventajas clave del uso de la biblioteca de transcodificación de imágenes:

* **Escalas con un tamaño o una resolución** de archivo crecientes: El escalado se logra principalmente gracias a la capacidad patentada de la biblioteca de transcodificación de imágenes para cambiar el tamaño al descodificar archivos. Esta capacidad garantiza que el uso de la memoria en tiempo de ejecución siempre sea óptimo y no sea una función cuadrática de aumento del tamaño del archivo o de resolución de megapíxeles. La biblioteca de transcodificación de imágenes puede procesar archivos de mayor tamaño y alta resolución (con megapíxeles más altos). Las herramientas de terceros, como ImageMagick, no pueden gestionar archivos grandes ni bloqueos mientras se procesan dichos archivos.
* **Algoritmos** de compresión y cambio de tamaño de la calidad de Photoshop: Coherencia con el estándar del sector en términos de calidad de muestreo descendente (bíbico liso, nítido y automático) y calidad de compresión. La biblioteca de transcodificación de imágenes evalúa aún más el factor de calidad de la imagen de entrada y utiliza de forma inteligente tablas y ajustes de calidad óptimos para la imagen de salida. Esta capacidad produce archivos de tamaño óptimo sin comprometer la calidad visual.
* **Alto rendimiento:** el tiempo de respuesta es menor y el rendimiento es siempre mayor que ImageMagick. Por lo tanto, la biblioteca de transcodificación de imágenes debería reducir el tiempo de espera de los usuarios y el coste del alojamiento.
* **Escale mejor con carga simultánea:** la biblioteca de transcodificación de imágenes funciona de forma óptima en condiciones de carga concurrentes. Proporciona un alto rendimiento con rendimiento óptimo de la CPU, uso de memoria y tiempo de respuesta bajo, lo que ayuda a reducir el costo del alojamiento.

## Plataformas compatibles {#supported-platforms}

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

Puede configurar las siguientes opciones para el parámetro `-resize` :

* `X`: Funciona de forma similar a  [!DNL Experience Manager]. Por ejemplo: cambie el tamaño a 319.
* `WxH`: La relación de aspecto no se mantiene, por ejemplo  `-resize 319x319`.
* `Wx`: Corrige la anchura y calcula la altura manteniendo la relación de aspecto. Por ejemplo `-resize 319x`.
* `xH`: Corrige la altura y calcula la anchura manteniendo la relación de aspecto. Por ejemplo `-resize x319`.

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## Configurar la biblioteca de transcodificación de imágenes {#configuring-imaging-transcoding-library}

Para configurar el procesamiento de ITL, cree un archivo de configuración y actualice el flujo de trabajo para ejecutarlo.

### Crear archivo de configuración para el paquete extraído {#create-conf-file}

Para configurar la biblioteca, cree un archivo CONF para indicar las bibliotecas siguiendo los pasos siguientes. Necesita permisos de administrador o raíz.

1. Descargue el paquete [Imaging Transcoding Library desde Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) e instálelo mediante el Administrador de paquetes. El paquete es compatible con [!DNL Experience Manager] 6.5.

1. Para conocer un id de paquete para `com.day.cq.dam.cq-dam-switchengine`, inicie sesión en la consola web y haga clic en **[!UICONTROL OSGi]** > **[!UICONTROL Paquetes]**. Como alternativa, para abrir la consola de paquetes, acceda a la dirección URL `https://[aem_server:[port]/system/console/bundles/`. Busque el paquete `com.day.cq.dam.cq-dam-switchengine` y su ID.

1. Asegúrese de que se extraen todas las bibliotecas necesarias comprobando la carpeta con el comando `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`, donde el nombre de la carpeta se construye con el ID del paquete. Por ejemplo, el comando es `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` si el id de paquete es `588`.

1. Cree un archivo `SWitchEngineLibs.conf` para vincular a la biblioteca.

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. Añada la ruta `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` al archivo conf utilizando el comando `cat SWitchEngineLibs.conf`.

1. Ejecute el comando `ldconfig` para crear los vínculos y la caché necesarios.

1. En la cuenta utilizada para iniciar [!DNL Experience Manager], edite el archivo `.bash_profile`. Agregue `LD_LIBRARY_PATH` agregando lo siguiente.

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. Para asegurarse de que el valor de la ruta está establecido en `.`, utilice el comando `echo $LD_LIBRARY_PATH`. El resultado debe ser `.`. Si el valor no está establecido en `.`, reinicie la sesión.

### Configurar [!UICONTROL Activo de actualización de DAM] flujo de trabajo {#configure-dam-asset-update-workflow}

Actualice el flujo de trabajo [!UICONTROL DAM Update Asset] para utilizar la biblioteca para procesar imágenes.

1. En la interfaz de usuario [!DNL Experience Manager], seleccione **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.

1. En la página **[!UICONTROL Workflow Models]**, abra el modelo de flujo de trabajo **[!UICONTROL DAM Update Asset]** en modo de edición.

1. Abra el paso del proceso de flujo de trabajo **[!UICONTROL Procesar miniaturas]**. En la pestaña **[!UICONTROL Miniaturas]**, añada los tipos MIME para los que desea omitir el proceso de generación de miniaturas predeterminado en la lista **[!UICONTROL Omitir tipos de MIME]**.
Por ejemplo, si desea crear miniaturas para una imagen TIFF mediante la Biblioteca de transcodificación de imágenes, especifique `image/tiff` en el campo **[!UICONTROL Omitir tipos de imágenes]**.

1. En la pestaña **[!UICONTROL Web Enabled Image]**, añada los tipos MIME para los que desea omitir el proceso predeterminado de generación de representación web en **[!UICONTROL Skip List]**. Por ejemplo, si ha omitido el tipo MIME `image/tiff` en el paso anterior, añada `image/tiff` a la lista de omisión.

1. Abra las **[!UICONTROL miniaturas EPS (con tecnología ImageMagick)]** paso , vaya a la pestaña **[!UICONTROL Argumentos]** . En la lista **[!UICONTROL Tipos de MIME]**, añada los tipos de MIME que desea que procese la biblioteca de transcodificación de imágenes. Por ejemplo, si ha omitido el tipo MIME `image/tiff` en el paso anterior, añada `image/jpeg` a la lista **[!UICONTROL Tipos de MIME]**.

1. Elimine los comandos predeterminados si existen.

1. Cambie el panel lateral y, en la lista de pasos, añada **[!UICONTROL SWitchEngine Handler]**.

1. Agregue comandos al [!UICONTROL SwitchEngine Handler] según sus necesidades personalizadas. Ajuste los parámetros de los comandos que especifique para satisfacer sus necesidades. Por ejemplo, si desea conservar el perfil de color de la imagen JPEG, agregue los siguientes comandos a la lista **[!UICONTROL Commands]**:

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![imagen](assets/chlimage_1-199.png)

1. (Opcional) Genere miniaturas a partir de una representación intermedia utilizando un solo comando. La representación intermedia actúa como fuente para generar representaciones estáticas y web. Este método es más rápido que el método anterior. Sin embargo, no puede aplicar parámetros personalizados a miniaturas mediante este método.

   ![imagen](assets/chlimage_1-200.png)

1. Para generar representaciones web, configure parámetros en la pestaña **[!UICONTROL Web-Enabled Image]**.

1. Sincronice el modelo de flujo de trabajo [!UICONTROL Activo de actualización de DAM] actualizado. Guarde el flujo de trabajo.

El verifica la configuración, carga una imagen TIFF y supervisa el archivo error.log. Verá `INFO` mensajes con menciones de `SwitchEngineHandlingProcess execute: executing command line`. Los registros mencionan las representaciones generadas. Una vez completado el flujo de trabajo, puede ver las nuevas representaciones en [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Artículo de tipos MIME admitidos](assets-formats.md#supported-image-transcoding-library)

