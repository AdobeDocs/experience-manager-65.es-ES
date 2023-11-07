---
title: Biblioteca de transcodificación de imágenes
description: Aprenda a configurar y utilizar la biblioteca de transcodificación de imágenes de Adobe, una solución de procesamiento de imágenes que puede realizar funciones principales de administración de imágenes, como codificación, transcodificación, remuestreo de imágenes y cambio de tamaño de imágenes.
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools,Asset Processing
exl-id: b67465f9-177c-49c4-b4eb-a1d6e09ac9a2
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# Biblioteca de transcodificación de imágenes {#imaging-transcoding-library}

La biblioteca de transcodificación de imágenes de Adobe es una solución de procesamiento de imágenes propietaria que puede realizar funciones principales de administración de imágenes, entre ellas:

* Codificación
* Transcodificación (conversión de formatos compatibles)
* Remuestreo de imágenes, con algoritmos de PS e Intel IPP
* Profundidad de bits y preservación del perfil de color
* Compresión de calidad JPEG
* Cambio de tamaño de imagen

La biblioteca de transcodificación de imágenes es compatible con CMYK y con alfa completo, excepto con el Alpha CMYK.

Además de admitir una amplia gama de formatos y perfiles de archivo, la biblioteca de transcodificación de imágenes tiene ventajas significativas respecto a otras soluciones de terceros en cuanto a rendimiento, escalabilidad y calidad. Estas son algunas de las ventajas clave de utilizar la biblioteca de transcodificación de imágenes:

* **Escalas con aumento del tamaño o la resolución del archivo**: La escala se logra principalmente mediante la capacidad patentada de la biblioteca de transcodificación de imágenes para cambiar el tamaño al descodificar archivos. Esta capacidad garantiza que el uso de la memoria en tiempo de ejecución siempre sea óptimo y no sea una función cuadrática de aumento del tamaño del archivo o de megapíxeles de resolución. La biblioteca de transcodificación de imágenes puede procesar archivos más grandes y de alta resolución (que contienen megapíxeles más altos). Las herramientas de terceros, como ImageMagick, no pueden gestionar archivos grandes ni bloqueos durante el procesamiento de dichos archivos.
* **Algoritmos de compresión y cambio de tamaño de calidad Photoshop**: Coherencia con el estándar de la industria en términos de calidad del muestreo hacia abajo (bicúbico liso, agudo y automático) y calidad de compresión. La biblioteca de transcodificación de imágenes evalúa aún más el factor de calidad de la imagen de entrada y utiliza de forma inteligente tablas y ajustes de calidad óptimos para la imagen de salida. Esta capacidad produce archivos de tamaño óptimo sin poner en riesgo la calidad visual.
* **Alto rendimiento:** El tiempo de respuesta es menor y el rendimiento es consistentemente mayor que ImageMagick. Por lo tanto, la biblioteca de transcodificación de imágenes debe reducir el tiempo de espera de los usuarios y el coste del alojamiento.
* **Escalar mejor con carga simultánea:** La biblioteca de transcodificación de imágenes funciona de forma óptima en condiciones de carga simultánea. Proporciona un alto rendimiento con un rendimiento óptimo de la CPU, uso de la memoria y bajo tiempo de respuesta, lo que ayuda a reducir el coste del alojamiento.

## Plataformas compatibles {#supported-platforms}

La biblioteca de transcodificación de imágenes solo está disponible para distribuciones RHEL 7 y CentOS 7.

>[!NOTE]
>
>Mac OS y otras distribuciones *nix (por ejemplo, Debian y Ubuntu) no son compatibles.

## Uso {#usage}

Los argumentos de la línea de comandos para la biblioteca de transcodificación de imágenes pueden incluir los siguientes:

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth '4' is automatically converted to '8'
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

Puede configurar las siguientes opciones para `-resize` parámetro:

* `X`: funciona de forma similar a [!DNL Experience Manager]. Por ejemplo, -resize 319.
* `WxH`: La proporción de aspecto no se mantiene, por ejemplo, `-resize 319x319`.
* `Wx`: corrige la anchura y calcula la altura manteniendo la relación de aspecto. Por ejemplo, `-resize 319x`.
* `xH`: corrige la altura y calcula la anchura manteniendo la relación de aspecto. Por ejemplo, `-resize x319`.

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## Configurar biblioteca de transcodificación de imágenes {#configuring-imaging-transcoding-library}

Para configurar el procesamiento de ITL, cree un archivo de configuración y actualice el flujo de trabajo para ejecutarlo.

### Crear archivo de configuración para el paquete extraído {#create-conf-file}

Para configurar la biblioteca, cree un archivo CONF para indicar las bibliotecas siguiendo los pasos siguientes. Necesita permisos de administrador o de raíz.

1. Descargue la [Paquete de biblioteca de transcodificación de imágenes desde distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) e instálelo mediante el Administrador de paquetes. El paquete es compatible con [!DNL Experience Manager] 6.5.

1. Para conocer un ID de paquete para `com.day.cq.dam.cq-dam-switchengine`, inicie sesión en la consola web y haga clic en **[!UICONTROL OSGi]** > **[!UICONTROL Paquetes]**. También puede acceder a para abrir la consola de paquetes `https://[aem_server:[port]/system/console/bundles/` URL. Localizar `com.day.cq.dam.cq-dam-switchengine` paquete y su ID.

1. Asegúrese de que todas las bibliotecas requeridas se extraen comprobando la carpeta con el comando `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`, donde el nombre de la carpeta se construye con el ID del paquete. Por ejemplo, el comando es `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` si el id del paquete es `588`.

1. Crear `SWitchEngineLibs.conf` para vincular a la biblioteca.

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. Añadir `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` ruta al archivo conf mediante `cat SWitchEngineLibs.conf` comando.

1. Ejecutar `ldconfig` para crear los vínculos y la caché necesarios.

1. En la cuenta que se usa para iniciar [!DNL Experience Manager], editar `.bash_profile` archivo. Añadir `LD_LIBRARY_PATH` mediante la adición de lo siguiente.

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. Para asegurarse de que el valor de la ruta está establecido en `.`, use `echo $LD_LIBRARY_PATH` comando. La salida debería ser `.`. Si el valor no está establecido en `.`, reinicie la sesión.

### Configurar [!UICONTROL Recurso de actualización DAM] workflow {#configure-dam-asset-update-workflow}

Actualice el [!UICONTROL Recurso de actualización DAM] flujo de trabajo para utilizar la biblioteca para procesar imágenes.

1. Entrada [!DNL Experience Manager] interfaz de usuario, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.

1. Desde el **[!UICONTROL Modelos de flujo de trabajo]** , abra la página **[!UICONTROL Recurso de actualización DAM]** modelo de flujo de trabajo en modo de edición.

1. Abra el **[!UICONTROL Procesar miniaturas]** paso del proceso de flujo de trabajo. En el **[!UICONTROL Miniaturas]** , añada los tipos MIME para los que desea omitir el proceso de generación de miniaturas predeterminado en la **[!UICONTROL Tipos MIME omitidos]** lista.
Por ejemplo, si desea crear miniaturas para una imagen de TIFF mediante la Biblioteca de transcodificación de imágenes, especifique `image/tiff` en el **[!UICONTROL Tipos MIME omitidos]** field.

1. En el **[!UICONTROL Imagen Web]** , añada los tipos MIME para los que desea omitir el proceso de generación de representación web predeterminado en **[!UICONTROL Lista para omitir]**. Por ejemplo, si ha omitido el tipo MIME `image/tiff` en el paso anterior, agregue `image/tiff` a la lista de omisión.

1. Abra el **[!UICONTROL Miniaturas de EPS (con ImageMagick)]** paso, vaya a **[!UICONTROL Argumentos]** pestaña. En el **[!UICONTROL Tipos MIME]** , agregue los tipos MIME que desea que procese la biblioteca de transcodificación de imágenes. Por ejemplo, si omitió el tipo MIME `image/tiff` en el paso anterior, agregue `image/jpeg` a la **[!UICONTROL Tipos MIME]** lista.

1. Quite los comandos predeterminados, si los hay.

1. Alternar panel lateral y añadir en la lista de pasos **[!UICONTROL Controlador SWitchEngine]**.

1. Agregar comandos al [!UICONTROL Controlador SwitchEngine] en función de sus necesidades personalizadas. Ajuste los parámetros de los comandos que especifique para satisfacer sus necesidades. Por ejemplo, si desea conservar el perfil de color de la imagen del JPEG, agregue los siguientes comandos al **[!UICONTROL Comandos]** lista:

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![chlimage](assets/chlimage_1-199.png)

1. (Opcional) Genere miniaturas de una representación intermedia con un solo comando. La representación intermedia actúa como fuente para generar representaciones estáticas y web. Este método es más rápido que el anterior. Sin embargo, no puede aplicar parámetros personalizados a las miniaturas mediante este método.

   ![chlimage](assets/chlimage_1-200.png)

1. Para generar representaciones web, configure parámetros en la variable **[!UICONTROL Imagen habilitada para web]** pestaña.

1. Sincronizar el actualizado [!UICONTROL Recurso de actualización DAM] modelo de flujo de trabajo. Guarde el flujo de trabajo.

Para comprobar la configuración, cargue una imagen de TIFF y supervise el archivo error.log. Lo notará `INFO` mensajes con menciones de `SwitchEngineHandlingProcess execute: executing command line`. Los registros mencionan las representaciones generadas. Una vez completado el flujo de trabajo, puede ver las nuevas representaciones en [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Artículo de tipos MIME admitidos](assets-formats.md#supported-image-transcoding-library)
