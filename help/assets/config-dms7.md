---
title: 'Configuración de Dynamic Media: modo Scene7'
description: Información sobre cómo configurar el modo Dynamic Media - Scene7.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 996780c3fac85f0ce0deeddd5ff4e74e01df436e
workflow-type: tm+mt
source-wordcount: '6083'
ht-degree: 5%

---


# Configuración de Dynamic Media - modo Scene7{#configuring-dynamic-media-scene-mode}

Si utiliza la configuración de Adobe Experience Manager para diferentes entornos, como desarrollo, ensayo y producción, configure Cloud Services de Dynamic Media para cada uno de esos entornos.

## Diagrama de arquitectura de Dynamic Media: modo Scene7 {#architecture-diagram-of-dynamic-media-scene-mode}

El siguiente diagrama de arquitectura describe el funcionamiento del modo Dynamic Media - Scene7.

Con la nueva arquitectura, Experience Manager es responsable de los recursos de origen principales y de las sincronizaciones con Dynamic Media para el procesamiento y la publicación de recursos:

1. Cuando el recurso de origen principal se carga en Experience Manager, se replica en Dynamic Media. En ese momento, Dynamic Media gestiona todo el procesamiento de recursos y la generación de representaciones, como la codificación de vídeo y las variantes dinámicas de una imagen. <!-- (In Dynamic Media - Scene7 mode, be aware that you can only upload assets whose file sizes are 2 GB or less.) Jira ticket CQ-4286561 fixed this issue. DM-S7 NOW SUPPORTS THE UPLOAD OF ASSETS LARGER THAN 2 GB. -->
1. Una vez generadas las representaciones, el Experience Manager puede acceder a las representaciones remotas de Dynamic Media y realizar la previsualización de forma segura (no se envían los binarios a la instancia del Experience Manager).
1. Una vez que el contenido está listo para publicarse y aprobarse, déclencheur al servicio Dynamic Media para insertar el contenido en los servidores de envío y almacenar el contenido en caché en la CDN (Red de Envío de contenido).

![chlimage_1-550](assets/chlimage_1-550.png)

>[!NOTE]
>
>La siguiente lista de funciones requiere el uso de la CDN lista para usar que se incluye con Adobe Experience Manager - Dynamic Media. Ninguna otra CDN personalizada es compatible con estas funciones.
>
>* [Imágenes inteligentes](/help/assets/imaging-faq.md)
>* [Invalidez de caché](/help/assets/invalidate-cdn-cache-dynamic-media.md)
>* [Protección de Hotlink](/help/assets/hotlink-protection.md)
>* [ENVÍO HTTP/2 del contenido](/help/assets/http2.md)
>* [Integración de visores de Dynamic Media con Adobe Analytics y Experience Platform Launch](/help/assets/launch.md)
>* Redirección de URL a nivel de CDN
>* Akamai ChinaCDN (para un envío óptimo en China)


## Activación de Dynamic Media en modo Scene7 {#enabling-dynamic-media-in-scene-mode}

[Dynamic Media está desactivado de forma predeterminada. ](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html) Para aprovechar las funciones de Dynamic Media, debe habilitarlas.

>[!NOTE]
>
>Dynamic Media - El modo Scene7 es solo para la instancia de Experience Manager Author. Como tal, debe configurar `runmode=dynamicmedia_scene7` en la instancia de Experience Manager Author, *no* la instancia de Experience Manager Publish.

Para habilitar Dynamic Media, debe realizar el inicio del Experience Manager mediante el modo de ejecución `dynamicmedia_scene7` desde la línea de comandos introduciendo lo siguiente en una ventana de terminal (el puerto de ejemplo utilizado es 4502):

```shell
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## (Opcional) Migración de ajustes preestablecidos y configuraciones de Dynamic Media de 6.3 a 6.5 Zero Downtime {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

La actualización de Dynamic Media Experience Manager de 6.3 a 6.4 o 6.5 ahora incluye la capacidad de realizar implementaciones sin downtime. Para migrar todos los ajustes preestablecidos y configuraciones de `/etc` a `/conf` en CRXDE Lite, asegúrese de ejecutar el siguiente comando curl.

>[!NOTE]
>
>Si ejecuta la instancia de Experience Manager en modo de compatibilidad (es decir, tiene la compatibilidad empaquetada instalada), no necesita ejecutar estos comandos.

Para todas las actualizaciones, ya sea con o sin el paquete de compatibilidad, puede copiar los ajustes preestablecidos de visor predeterminados y listos para usar que originalmente se incluyeron con Dynamic Media ejecutando el siguiente comando de control de Linux:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

Para migrar cualquier ajuste preestablecido de visor personalizado y configuración que haya creado de `/etc` a `/conf`, ejecute el siguiente comando de control de Linux:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## Instalación del paquete de funciones 18912 para migración masiva de recursos {#installing-feature-pack-for-bulk-asset-migration}

La instalación del paquete de funciones 18912 es *opcional*.

El paquete de funciones 18912 le permite realizar ingestas masivas de recursos mediante FTP o migrar recursos desde el modo Dynamic Media - híbrido o Dynamic Media Classic a Dynamic Media - modo Scene7 en Experience Manager. Está disponible en [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

Consulte [Instalación del paquete de funciones 18912 para la migración masiva de recursos](/help/assets/bulk-ingest-migrate.md) para obtener más información.

## Creación de una configuración de Dynamic Media en Cloud Services {#configuring-dynamic-media-cloud-services}

**Antes de configurar Dynamic Media** : después de recibir el correo electrónico de aprovisionamiento con las credenciales de Dynamic Media, debe abrir la aplicación [ de escritorio de ](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)Dynamic Media Classic e iniciar sesión en la cuenta para cambiar la contraseña. La contraseña que se proporciona en el correo electrónico de aprovisionamiento es generada por el sistema y está pensada para ser una contraseña temporal solamente. Es importante que actualice la contraseña para que Dynamic Media Cloud Service esté configurado con las credenciales correctas.

![dynamicmediaconfiguration2update](assets/dynamicmediaconfiguration2updated.png)

**Para crear una configuración de Dynamic Media en Cloud Services**

1. En Experience Manager, toque el logotipo del Experience Manager para acceder a la consola de navegación global y toque el icono Herramientas y, a continuación, toque **[!UICONTROL Cloud Services > Configuración de Dynamic Media.]**
1. En la página Explorador de configuración de Dynamic Media, en el panel izquierdo, pulse **[!UICONTROL global]** (no pulse ni seleccione el icono de carpeta a la izquierda de **[!UICONTROL global]**) y, a continuación, pulse **[!UICONTROL Crear.]**
1. En la página **[!UICONTROL Crear configuración de Dynamic Media]**, escriba un título, la dirección de correo electrónico de la cuenta de Dynamic Media, la contraseña y, a continuación, seleccione su región. Esta información se le proporciona por Adobe en el correo electrónico de aprovisionamiento. Póngase en contacto con el Servicio de atención al cliente de Adobe si no ha recibido el correo electrónico.

   Toque **[!UICONTROL Conectar a Dynamic Media.]**

   >[!NOTE]
   Después de recibir el correo electrónico de aprovisionamiento con las credenciales de Dynamic Media, abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e inicie sesión en su cuenta para cambiar la contraseña. La contraseña que se proporciona en el correo electrónico de aprovisionamiento es generada por el sistema y está pensada para ser una contraseña temporal solamente. Es importante que actualice la contraseña para que el Cloud Service de Dynamic Media esté configurado con las credenciales correctas.

1. Cuando la conexión se realice correctamente, establezca lo siguiente. Los encabezados con un asterisco (*) son obligatorios:

   * **[!UICONTROL Compañía]** : el nombre de la cuenta de Dynamic Media. Tiene varias cuentas de Dynamic Media. Por ejemplo, puede tener diferentes submarcas, divisiones, entornos de ensayo o producción.

   * **[!UICONTROL Ruta de carpeta raíz de la empresa]**

   * **[!UICONTROL Publicación de recursos]** : puede elegir entre las tres opciones siguientes:
      * **** Inmediatamente significa que cuando se cargan recursos, el sistema los ingesta y proporciona la URL o incrustación al instante. No es necesaria la intervención del usuario para publicar recursos.
      * **[!UICONTROL Tras la]** activación, significa que primero debe publicar explícitamente el recurso antes de proporcionar un vínculo URL/Incrustar.
      * **[!UICONTROL Publicación selectivaEsta opción le permite controlar qué carpetas se publican en Dynamic Media.]** Permite utilizar funciones como recorte inteligente o representaciones dinámicas, o determinar qué carpetas se publican exclusivamente en Experience Manager para la vista previa. Esos mismos recursos *no* se publican en Dynamic Media para su envío en el dominio público.<br>Puede definir esta opción aquí en  **[!UICONTROL Dynamic Media Cloud]** Configurationo, si lo prefiere, puede elegir establecer esta opción en el nivel de carpeta, en  **[!UICONTROL Propiedades]** de una carpeta.<br>Consulte  [Uso de la publicación selectiva en Dynamic Media.](/help/assets/selective-publishing.md)<br>Si posteriormente cambia esta configuración o posteriormente la cambia a nivel de carpeta, esos cambios solo afectarán a los nuevos recursos que cargue a partir de ese momento. El estado de publicación de los recursos existentes en la carpeta permanece tal cual hasta que los cambie manualmente desde **[!UICONTROL Publicación rápida]** o el cuadro de diálogo **[!UICONTROL Administrar publicación]**.
   * **[!UICONTROL Servidor]**  de Previsualización segura: permite especificar la ruta de URL al servidor de previsualización de representaciones seguras. Es decir, una vez generadas las representaciones, el Experience Manager puede acceder a las representaciones remotas de Dynamic Media y realizar la previsualización de forma segura (no se envían archivos binarios a la instancia de Experience Manager).
A menos que tenga una disposición especial para utilizar el servidor de su propia compañía o un servidor especial, Adobe recomienda que deje esta configuración como se especificó.

   * **[!UICONTROL Sincronizar todo el contenido]** :  <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->seleccionado de forma predeterminada. Anule la selección de esta opción si desea incluir o excluir recursos de la sincronización con Dynamic Media de forma selectiva. Si anula la selección de esta opción, podrá elegir entre los dos modos de sincronización de Dynamic Media siguientes:

   * **[!UICONTROL Modo de sincronización de Dynamic Media]**
      * **[!UICONTROL Habilitado de forma predeterminada]** : la configuración se aplica a todas las carpetas de forma predeterminada, a menos que se marque una carpeta específicamente para la exclusión.  <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL Deshabilitada de forma predeterminada]** : la configuración no se aplica a ninguna carpeta hasta que se marque explícitamente una carpeta seleccionada para sincronizarla con Dynamic Media.
Para marcar una carpeta seleccionada para sincronizar con Dynamic Media, seleccione una carpeta de recursos y, en la barra de herramientas, toque **[!UICONTROL Propiedades]**. En la ficha **[!UICONTROL Detalles]**, en la lista desplegable **[!UICONTROL modo de sincronización de Dynamic Media]**, elija una de las tres opciones siguientes. Cuando haya terminado, toque **[!UICONTROL Guardar.]** *Recuerde: estas tres opciones no están disponibles si seleccionó&#x200B;**Sincronizar todo el**contenido anteriormente.* Consulte también  [Uso de Publicación selectiva en el nivel de carpeta de Dynamic Media.](/help/assets/selective-publishing.md)
         * **[!UICONTROL Heredado]** : no hay ningún valor de sincronización explícita en la carpeta; en su lugar, la carpeta hereda el valor de sincronización de una de sus carpetas antecesoras o del modo predeterminado en la configuración de nube. El estado detallado de heredado se muestra mediante una información del objeto.
         * **[!UICONTROL Habilitar para subcarpetas]** : Incluya todo en este subárbol para sincronizar con Dynamic Media. La configuración específica de la carpeta anula el modo predeterminado en la configuración de la nube.
         * **[!UICONTROL Deshabilitado para subcarpetas]** : excluya todo lo que se encuentra en este subárbol de la sincronización con Dynamic Media.

   >[!NOTE]
   No se admite el control de versiones en DMS7. Además, la activación retrasada solo se aplica si **[!UICONTROL Publicar recursos]** en la página Editar configuración de Dynamic Media está configurada en **[!UICONTROL Al activarse]** y, a continuación, solo hasta la primera vez que se activa el recurso.
   Una vez activado un recurso, cualquier actualización se publica inmediatamente en directo en el Envío S7.

1. Toque **[!UICONTROL Guardar.]**
1. Para realizar una previsualización segura del contenido de Dynamic Media antes de que se publique, debe &quot;lista de permitidos&quot; de la instancia de creación del Experience Manager para conectarse a Dynamic Media:

   * Abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e inicie sesión en su cuenta. Adobe proporcionó las credenciales y los detalles de inicio de sesión en el momento del aprovisionamiento. Si no dispone de esta información, póngase en contacto con el servicio de asistencia técnica.

   * En la barra de navegación situada cerca de la parte superior derecha de la página, toque **[!UICONTROL Ajustes > Ajustes de aplicación > Ajustes de publicación > Servidor de imágenes]**.

   * En la lista desplegable Contexto de publicación de la página Servidor de imágenes, seleccione **[!UICONTROL Probar servicio de imágenes.]**
   * Para el filtro de direcciones de cliente, toque **[!UICONTROL Añadir.]**
   * Para habilitar (activar) la dirección, seleccione la casilla de verificación. Introduzca la dirección IP de la instancia de Experience Manager Author (no la IP de Dispatcher).
   * Toque **[!UICONTROL Guardar.]**

Ha finalizado con la configuración básica; está listo para usar Dynamic Media - modo Scene7.

Si desea personalizar aún más la configuración, puede completar opcionalmente cualquiera de las tareas en [(Opcional) Configuración avanzada en Dynamic Media - modo Scene7](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

## (Opcional) Configuración avanzada en Dynamic Media: modo Scene7 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Si desea personalizar aún más la configuración y la configuración del modo Dynamic Media - Scene7 o optimizar su rendimiento, puede completar una o más de las siguientes *tareas opcionales*:

* [(Opcional) Configuración y configuración de Dynamic Media - Configuración del modo Scene7](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)

* [(Opcional) Ajuste del rendimiento de Dynamic Media: modo Scene7](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [(Opcional) Filtrado de recursos para replicación](#optional-filtering-assets-for-replication)

### (Opcional) Configuración y configuración de Dynamic Media - Configuración del modo Scene7 {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

Cuando esté en modo de ejecución `dynamicmedia_scene7`, utilice la interfaz de usuario de Dynamic Media Classic para cambiar la configuración de Dynamic Media.

Algunas de las tareas anteriores requieren que abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) y luego inicie sesión en su cuenta.

Las tareas de configuración y configuración incluyen lo siguiente:

* [Configuración de publicación para Image Server](#publishing-setup-for-image-server)
* [Configuración de la configuración general de la aplicación](#configuring-application-general-settings)
* [Configuración de la administración de color](#configuring-color-management)
* [Edición de tipos MIME para formatos admitidos](#editing-mime-types-for-supported-formats)
* [Añadir tipos MIME para formatos no admitidos](#adding-mime-types-for-unsupported-formats)
* [Creación de ajustes preestablecidos de conjunto de lotes para generar automáticamente conjuntos de imágenes y conjuntos de giros](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)

#### Configuración de publicación para el servidor de imágenes {#publishing-setup-for-image-server}

La configuración de Ajuste de publicación determina cómo se envían los recursos de forma predeterminada desde Dynamic Media. Si no se especifica ninguna configuración, Dynamic Media envía un recurso según la configuración predeterminada definida en Ajuste de publicación. Por ejemplo, una solicitud de envío de una imagen que no incluye un atributo resolution genera una imagen con la configuración de Resolución de objeto predeterminada.

Para configurar Ajuste de publicación: en Dynamic Media Classic, toque **[!UICONTROL Ajustes > Ajustes de aplicación > Ajustes de publicación > Servidor de imágenes]**.

La pantalla Servidor de imágenes establece la configuración predeterminada para la entrega de imágenes. Consulte la pantalla de la interfaz de usuario para ver la descripción de cada configuración.

* **[!UICONTROL Atributos]**  de solicitud: esta configuración impone límites a las imágenes que se pueden enviar desde el servidor.
* **[!UICONTROL Atributos]**  de solicitud predeterminados: esta configuración se refiere al aspecto predeterminado de las imágenes.
* **[!UICONTROL Atributos]**  de miniatura comunes: esta configuración se refiere al aspecto predeterminado de las imágenes en miniatura.
* **[!UICONTROL Valores predeterminados para los campos]** del catálogo: esta configuración se refiere a la resolución y al tipo de miniatura predeterminada de las imágenes.
* **[!UICONTROL Atributos]**  de administración de color: esta configuración determina qué perfiles de color ICC se utilizan.
* **[!UICONTROL Atributos]**  de compatibilidad: Esta configuración permite que los párrafos al inicio y al final de las capas de texto se traten como en la versión 3.6 para lograr compatibilidad con versiones anteriores.
* **[!UICONTROL Compatibilidad]**  con localizaciones: Esta configuración le permite administrar varios atributos de configuración regional. También le permite especificar una cadena de asignación de configuración regional para que pueda definir qué idiomas desea admitir para las distintas sugerencias de herramientas en los visores. Para obtener más información sobre la configuración de **[Soporte para Localizaciones]**, consulte [Consideraciones al configurar la localización de recursos](https://help.adobe.com/en_US/scene7/using/WS997f1dc4cb0179f034e07dc31412799d19a-8000.html).

#### Configuración de la configuración general de la aplicación {#configuring-application-general-settings}

Para abrir la página Configuración general de la aplicación, en la barra de navegación global de Dynamic Media Classic, toque **[!UICONTROL Ajustes > Ajustes de aplicación > Configuración general.]**

**Servidores - **Al aprovisionar la cuenta, Dynamic Media proporciona automáticamente los servidores asignados para la compañía. Estos servidores se utilizan para construir cadenas URL para el sitio Web y las aplicaciones. Estas llamadas mediante URL son específicas de su cuenta. No cambie ninguno de los nombres de los servidores a menos que se indique expresamente que lo haga el Servicio de atención al cliente de Adobe.

**[!UICONTROL Sobrescribir imágenes]** : Dynamic Media no permite que dos archivos tengan el mismo nombre. El ID de URL de cada elemento (el nombre de archivo menos la extensión) debe ser único. Estas opciones especifican cómo se cargan los recursos de reemplazo: ya sea que reemplacen el original o se conviertan en duplicados. Se cambia el nombre de los recursos de duplicado por &quot;-1&quot; (por ejemplo, silla.tif se denomina silla-1.tif). Estas opciones afectan a los recursos cargados en una carpeta diferente a la original o a los recursos con una extensión de nombre de archivo diferente a la original (como JPG, TIF o PNG).

* **[!UICONTROL Sobrescribir en la carpeta actual, el mismo nombre de imagen base/extensión]** : esta opción es la regla más estricta para reemplazar. Requiere que la imagen de sustitución se cargue en la misma carpeta que la imagen original y que la imagen de sustitución tenga la misma extensión de nombre de archivo que la imagen original. Si no se cumplen estos requisitos, se crea un duplicado.

>[!NOTE]
Para mantener la coherencia con el Experience Manager, seleccione siempre esta configuración: **Sobrescribir en la carpeta actual, el mismo nombre/extensión de imagen base**

* **[!UICONTROL Sobrescribir en cualquier carpeta, el mismo nombre de recurso base/extensión]** : requiere que la imagen de sustitución tenga la misma extensión de nombre de archivo que la imagen original (por ejemplo, silla.jpg debe reemplazar a silla.jpg, no silla.tif). Sin embargo, puede cargar la imagen de reemplazo en una carpeta distinta a la original. La imagen actualizada reside en la nueva carpeta; el archivo ya no se puede encontrar en su ubicación original
* **[!UICONTROL Sobrescribir en cualquier carpeta, el mismo nombre de recurso base independientemente de la extensión]** : esta opción es la regla de reemplazo más inclusiva. Puede cargar una imagen de sustitución en una carpeta distinta a la original, cargar un archivo con una extensión de nombre de archivo diferente y reemplazar el archivo original. Si el archivo original se encuentra en una carpeta diferente, la imagen de reemplazo reside en la nueva carpeta en la que se cargó.

**[!UICONTROL Perfiles]**  de color predeterminados: consulte  [Configuración de la ](#configuring-color-management) administración de color para obtener más información.

>[!NOTE]
De forma predeterminada, el sistema muestra 15 representaciones al seleccionar **[!UICONTROL Representaciones]** y 15 ajustes preestablecidos de visualizador al seleccionar **[!UICONTROL Visualizadores]** en la vista de detalles del recurso. Puede aumentar este límite. Consulte [Aumento del número de ajustes preestablecidos de imagen que muestran](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) o [Aumento del número de ajustes preestablecidos de visor que muestran](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).


#### Configuración de la administración de color {#configuring-color-management}

La administración dinámica de color de los medios le permite colorear los recursos correctos. Con la corrección de color, los recursos ingestados conservan su espacio de color (RGB, CMYK, Gris) y su perfil de color incrustado. Cuando se solicita una representación dinámica, el color de la imagen se corrige en el espacio de color del destinatario mediante la salida CMYK, RGB o gris. Consulte [Configuración de ajustes preestablecidos de imagen](/help/assets/managing-image-presets.md).

Para configurar las propiedades de color predeterminadas de modo que la corrección de color esté habilitada cuando se soliciten imágenes:

1. Abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e inicie sesión en su cuenta con las credenciales proporcionadas durante el aprovisionamiento.
1. Vaya a **[!UICONTROL Ajustes > Ajustes de aplicación.]**
1. Expanda el área **[!UICONTROL Ajustes de publicación]** y seleccione **[!UICONTROL Servidor de imágenes.]** Configure **[!UICONTROL Publicar contexto]** en **[!UICONTROL Servicio de imágenes]** cuando establezca los valores predeterminados para las instancias de publicación.
1. Desplácese a la propiedad que desee cambiar. Por ejemplo, una propiedad del área **[!UICONTROL Atributos de administración de color]**.

   Puede establecer las siguientes propiedades de corrección de color:

   * **[!UICONTROL Espacio]**  de color predeterminado CMYK: nombre del perfil de color CMYK predeterminado
   * **[!UICONTROL Espacio]**  de color predeterminado de escala de grises: nombre del perfil de color gris predeterminado
   * **[!UICONTROL Espacio]**  de color predeterminado RGB: nombre del perfil de color RGB predeterminado
   * **[!UICONTROL Calidad]**  de representación de conversión de color: especifica la interpretación. Los valores aceptables son: **[!UICONTROL percepción]**, **[!UICONTROL colométrica relativa]**, **[!UICONTROL saturación]**, **[!UICONTROL colométrica absoluta.]** Adobe recomienda  **** relativamente como valor predeterminado.

1. Toque **[!UICONTROL Guardar.]**

Por ejemplo, puede establecer el **[!UICONTROL espacio de color predeterminado RGB]** en *sRGB* y el **[!UICONTROL espacio de color predeterminado CMYK]** en *WebCoated*.

Al hacerlo, se haría lo siguiente:

* Permite la corrección de color para imágenes RGB y CMYK.
* Se supone que las imágenes RGB que no tienen un perfil de color están en el espacio de color *sRGB*.
* Se supone que las imágenes CMYK que no tienen un perfil de color están en *espacio de color WebCoated*.
* Las representaciones dinámicas que devuelven salida RGB la devuelven en el espacio de color *sRGB*.
* Representaciones dinámicas que devuelven una salida CMYK, la devuelven en el espacio de color *WebCoated*.

#### Edición de tipos MIME para formatos admitidos {#editing-mime-types-for-supported-formats}

Puede definir qué tipos de recursos procesa Dynamic Media y personalizar los parámetros avanzados de procesamiento de recursos. Por ejemplo, puede especificar parámetros de procesamiento de recursos para realizar lo siguiente:

* Convertir un Adobe PDF en un recurso de catálogo electrónico.
* Convertir un Documento de Adobe Photoshop (.PSD) en un recurso de plantilla de letrero para su personalización.
* Rasterizar un archivo de Adobe Illustrator (.AI) o un archivo de PostScript® encapsulado de Adobe Photoshop (.EPS).
* [Los ](/help/assets/video-profiles.md) perfiles de vídeo y  [los ](/help/assets/image-profiles.md) perfiles de imagen se pueden utilizar para definir el procesamiento de vídeos e imágenes, respectivamente.

Consulte [Carga de recursos](/help/assets/manage-assets.md#uploading-assets).

**Para editar tipos MIME para formatos admitidos**

1. En Experience Manager, toque el logotipo del Experience Manager para acceder a la consola de navegación global y, a continuación, toque **[!UICONTROL Herramientas > General > CRXDE Lite.]**
1. En el carril izquierdo, vaya a lo siguiente:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![Tipos MIME](assets/mimetypes.png)

1. En la carpeta mimeTypes, seleccione un tipo de MIME.
1. A la derecha de la página CRXDE Lite, en la parte inferior:

   * Haga clic con el doble en el campo **[!UICONTROL enabled]**. De forma predeterminada, todos los tipos de MIME de recursos están habilitados (definidos como **[!UICONTROL true]**), lo que significa que los recursos se sincronizan con Dynamic Media para su procesamiento. Si desea excluir este tipo de MIME de recurso para que no se procese, cambie esta configuración a **[!UICONTROL false.]**

   * doble toque **[!UICONTROL jobParam]** para abrir el campo de texto asociado. Consulte [Tipos de MIME admitidos](/help/assets/assets-formats.md#supported-mime-types) para obtener una lista de los valores de parámetro de procesamiento permitidos que puede utilizar para un tipo de MIME determinado.

1. Realice una de las acciones siguientes:

   * Repita los pasos del 3 al 4 para editar más tipos MIME.
   * En la barra de menús de la página CRXDE Lite, toque **[!UICONTROL Guardar todo.]**

1. En la esquina superior izquierda de la página, toque **[!UICONTROL CRXDE Lite]** para volver al Experience Manager.

#### Añadir tipos MIME para formatos no admitidos {#adding-mime-types-for-unsupported-formats}

Puede agregar tipos MIME personalizados para formatos no admitidos en Recursos Experience Manager. Asegúrese de que el Experience Manager no elimine ningún nodo nuevo que agregue al CRXDE Lite moviendo el tipo MIME antes de `image_`. Además, asegúrese de que su valor habilitado esté establecido en **[!UICONTROL false.]**

**Para agregar tipos MIME a formatos no admitidos**

1. En el Experience Manager, toque **[!UICONTROL Herramientas > Operaciones > Consola web.]**

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Se abre una nueva ficha de explorador en la página **[!UICONTROL Configuración de la consola web de Adobe Experience Manager]**.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. En la página, desplácese hacia abajo hasta el nombre *Servicio MIME de tipo de recurso de Adobe CQ Scene7* como se muestra en la siguiente captura de pantalla. A la derecha del nombre, pulse la opción **[!UICONTROL Editar los valores de configuración]** (icono de lápiz).

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. En la página **Servicio de tipo MIME de Scene7 Asset de Adobe CQ**, toque el icono de signo más &lt;+>. La ubicación en la tabla donde se toca el signo más para agregar el nuevo tipo de MIME es trivial.

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. Escriba `DWG=image/vnd.dwg` en el campo de texto vacío que acaba de agregar.

   El ejemplo `DWG=image/vnd.dwg` se muestra únicamente con fines ilustrativos. El tipo MIME que agregue aquí puede ser cualquier otro formato no admitido.

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. En la esquina inferior derecha de la página, toque **[!UICONTROL Guardar.]**

   En este punto, puede cerrar la ficha del explorador que tiene la página de configuración de la consola web de Adobe Experience Manager abierta.

1. Vuelva a la ficha del explorador que tiene la consola Experience Manager abierta.
1. En el Experience Manager, toque **[!UICONTROL Herramientas > General > CRXDE Lite.]**

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. En el carril izquierdo, vaya a lo siguiente:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Arrastre el tipo de MIME `image_vnd.dwg` y colóquelo directamente sobre `image_` en el árbol como se muestra en la siguiente captura de pantalla.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. Con el tipo MIME `image_vnd.dwg` aún seleccionado, en la ficha **[!UICONTROL Propiedades]**, en la fila **[!UICONTROL habilitada]**, bajo el encabezado de columna **[!UICONTROL Valor]**, toque con el doble el valor para abrir la lista desplegable **[!UICONTROL Valor]**.
1. Escriba `false` en el campo (o seleccione **[!UICONTROL false]** en la lista desplegable).

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. Cerca de la esquina superior izquierda de la página CRXDE Lite, toque **[!UICONTROL Guardar todo.]**

#### Creación de ajustes preestablecidos de conjunto de lotes para generar automáticamente conjuntos de imágenes y conjuntos de giros {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

Utilice los ajustes preestablecidos de conjunto de lotes para automatizar la creación de conjuntos de imágenes o conjuntos de giros mientras los recursos se cargan en Dynamic Media.

En primer lugar, defina la convención de nombre para el modo en que los recursos se agrupan en un conjunto. A continuación, cree un ajuste preestablecido de conjunto de lotes con un nombre único y un conjunto de instrucciones independiente. Debe definir cómo construir el conjunto con imágenes que coincidan con las convenciones de nombres definidas en la fórmula preestablecida.

Al cargar archivos, Dynamic Media crea automáticamente un conjunto con todos los archivos que coinciden con la convención de nombre definida en los ajustes preestablecidos activos.

**Configuración de la nomenclatura predeterminada**

Cree una convención de nombre predeterminada que se utilice en cualquier fórmula de ajuste preestablecido de conjunto de lotes. Es probable que la convención de nombre predeterminada seleccionada en la definición del ajuste preestablecido de conjunto de lotes sea todo lo que necesita la compañía para generar conjuntos por lotes. Se crea un ajuste preestablecido de conjunto de lotes para utilizar la convención de nombre predeterminada que defina. Puede crear tantos ajustes preestablecidos de conjunto de lotes como desee con convenciones de nombre personalizadas alternativas necesarias para un conjunto concreto de contenido en casos en los que exista una excepción a la nomenclatura predeterminada definida por la compañía.

Aunque no es necesario configurar una convención de nombre predeterminada para utilizar la funcionalidad de ajuste preestablecido de conjunto de lotes, se recomienda utilizar la convención de nombre predeterminada. Permite definir tantos elementos de la convención de nombres como desee agrupar en un conjunto para agilizar la creación de conjuntos de lotes.

Como alternativa, puede utilizar **[!UICONTROL Código de Vista]** sin campos de formulario disponibles. En esta vista, las definiciones de convención de nombres se crean utilizando expresiones normales.

Hay dos elementos disponibles para la definición: Coincidencia y Nombre base. Estos campos permiten definir todos los elementos de una convención de nombres e identificar la parte de la convención utilizada para asignar un nombre al conjunto en el que están contenidos. La convención de nombre individual de una compañía suele utilizar una o varias líneas de definición para cada uno de estos elementos. Puede utilizar tantas líneas como desee para su definición única y agruparlas en elementos distintos, como imagen principal, elemento de color, elemento de Vista alternativa y elemento de muestra.

**Para configurar la nomenclatura predeterminada**

1. Abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e inicie sesión en su cuenta.

   Adobe proporcionó las credenciales y los detalles de inicio de sesión en el momento del aprovisionamiento. Si no dispone de esta información, póngase en contacto con el servicio de asistencia técnica.

1. En la barra de navegación cerca de la parte superior de la página, toque **[!UICONTROL Ajustes > Ajustes de aplicación > Valores preestablecidos de conjunto por lotes > Nombre predeterminado.]**
1. Seleccione **[!UICONTROL Ver formulario]** o **[!UICONTROL Ver código]** para especificar cómo desea ver e introducir información sobre cada elemento.

   Puede seleccionar la casilla de verificación **[!UICONTROL Código de Vista]** para realizar una vista de la creación del valor de expresión normal junto con las selecciones de formulario. Puede introducir o modificar estos valores para ayudar a definir los elementos de la convención de nombres, si la vista del formulario le limita por cualquier motivo. Si los valores no se pueden analizar en la vista del formulario, los campos del formulario se desactivan.

   >[!NOTE]
   Los campos de formulario desactivados no validan que las expresiones normales sean correctas. Verá los resultados de la expresión normal que está generando para cada elemento después de la línea de resultados. La expresión regular completa está visible en la parte inferior de la página.

1. Expanda cada elemento según sea necesario e introduzca las convenciones de nombres que desee utilizar.
1. Si es necesario, realice una de las siguientes acciones:

   * Toque **[!UICONTROL Añadir]** para agregar otra convención de nombre para un elemento.
   * Toque **[!UICONTROL Eliminar]** para eliminar una convención de nombre para un elemento.

1. Realice una de las acciones siguientes:

   * Toque **[!UICONTROL Guardar como]** y escriba un nombre para el ajuste preestablecido.
   * Toque **[!UICONTROL Guardar]** si está editando un ajuste preestablecido existente.

**Creación de un ajuste preestablecido de conjunto de lotes**

Dynamic Media utiliza ajustes preestablecidos de conjunto de lotes para organizar los recursos en conjuntos de imágenes (imágenes alternativas, opciones de color, giro de 360) para su visualización en los visores. Los ajustes preestablecidos de conjunto de lotes se ejecutan automáticamente junto con los procesos de carga de recursos en Dynamic Media.

Puede crear, editar y administrar los ajustes preestablecidos de conjunto de lotes. Existen dos formas de definiciones de ajustes preestablecidos de conjunto de lotes: una para una convención de nombre predeterminada que puede configurar y otra para convenciones de nombre personalizadas que cree sobre la marcha.

Puede utilizar el método de campo de formulario para definir un ajuste preestablecido de conjunto de lotes o el método de código, que le permite utilizar expresiones regulares. Como en Nombre predeterminado, puede elegir Código de Vista al mismo tiempo que define en la Vista Formulario y utilizar expresiones regulares para crear sus definiciones. También puede desactivar la vista para usar una u otra exclusivamente.

**Creación de un ajuste preestablecido de conjunto por lotes**

1. Abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e inicie sesión en su cuenta.

   Adobe proporcionó las credenciales y los detalles de inicio de sesión en el momento del aprovisionamiento. Si no dispone de esta información, póngase en contacto con el servicio de asistencia técnica.

1. En la barra de navegación cerca de la parte superior de la página, toque **[!UICONTROL Ajustes > Ajustes de aplicación > Valores preestablecidos de conjunto por lotes > Valor preestablecido de conjunto por lotes.]**

   **[!UICONTROL Formulario]** de vista, tal como se define en la esquina superior derecha de la página Detalles, es la vista predeterminada.

1. En el panel Lista de ajustes preestablecidos, toque **[!UICONTROL Añadir]** para activar los campos de definición en el panel Detalles del lado derecho de la pantalla.
1. En el panel Detalles, en el campo Nombre de ajuste preestablecido, escriba un nombre para el ajuste preestablecido.
1. En el menú desplegable Tipo de conjunto de lotes, seleccione un tipo de ajuste preestablecido.
1. Realice una de las acciones siguientes:

   * Si está utilizando una convención de nombres predeterminada que configuró anteriormente en **[!UICONTROL Ajustes de aplicación > Valores preestablecidos de conjuntos de lotes > Nombres predeterminados]**, expanda **[!UICONTROL Convenciones de nombres de recursos]** y, a continuación, en la lista desplegable Nombre de archivo, toque **[!UICONTROL Predeterminado.]**

   * Para definir una nueva convención de nombres al configurar el ajuste preestablecido, expanda **[!UICONTROL Convenciones de nombres de recursos]** y, a continuación, en la lista desplegable Nombres de archivos, toque **[!UICONTROL Personalizado.]**

1. Para el orden de secuencia, defina el orden en que se muestran las imágenes después de que el conjunto se agrupe en Dynamic Media.

   De forma predeterminada, los recursos se ordenan de forma alfanumérica. Sin embargo, puede utilizar una lista separada por comas de expresiones regulares para definir el orden.

1. Para la convención de creación y nombre de conjunto, especifique el sufijo o el prefijo del nombre base definido en la convención de nombres de recursos. Además, defina dónde se crea el conjunto dentro de la estructura de carpetas de Dynamic Media.

   Si define un gran número de conjuntos, mantenga los conjuntos separados de las carpetas que contienen los propios recursos. Por ejemplo, cree una carpeta de conjuntos de imágenes y coloque aquí los conjuntos generados.

1. En el panel Detalles, toque **[!UICONTROL Guardar.]**
1. Toque **[!UICONTROL Activo]** junto al nuevo nombre de ajuste preestablecido.

   Al activar el ajuste preestablecido, se garantiza que al cargar recursos en Dynamic Media, el ajuste preestablecido de conjunto de lotes se aplica para generar el conjunto.

**Creación de un ajuste preestablecido de conjunto de lotes para la generación automática de un conjunto de giros 2D**

Puede utilizar el tipo de conjunto de lotes **[!UICONTROL Conjunto de giros con varios ejes]** para crear una fórmula que automatice la generación de conjuntos de giros 2D. La agrupación de imágenes utiliza expresiones regulares de fila y columna para que los recursos de imagen estén correctamente alineados en la ubicación correspondiente de la matriz multidimensional. No hay un número mínimo o máximo de filas o columnas que debe tener en un conjunto de giros de varios ejes.

Por ejemplo, supongamos que desea crear un conjunto de giros de varios ejes denominado `spin-2dspin`. Tiene un conjunto de imágenes de conjunto de giros que contienen tres filas, con 12 imágenes por fila. Las imágenes reciben el siguiente nombre:

```
spin-01-01
 spin-01-02
 …
 spin-01-12
 spin-02-01
 …
 spin-03-12
```

Con esta información, la fórmula de tipo de conjunto de lotes se puede crear de la siguiente manera:

![chlimage_1-560](assets/chlimage_1-560.png)

La agrupación de la parte del nombre de recurso compartido del conjunto de giros se agrega al campo **Coincidencia** (como resaltado). La parte variable del nombre del recurso que contiene la fila y la columna se agrega a los campos **Fila** y **Columna**, respectivamente.

Cuando se carga y publica el conjunto de giros, se activa el nombre de la fórmula de conjunto de giros 2D que aparece en **Ajustes preestablecidos de conjunto de lotes** en el cuadro de diálogo **Opciones de carga de trabajo**.

**Creación de un ajuste preestablecido de conjunto de lotes para la generación automática de un conjunto de giros 2D**

1. Abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e inicie sesión en su cuenta.

   Adobe proporcionó las credenciales y los detalles de inicio de sesión en el momento del aprovisionamiento. Si no dispone de esta información, póngase en contacto con el servicio de asistencia técnica.

1. En la barra de navegación cerca de la parte superior de la página, toque **[!UICONTROL Configuración] > [!UICONTROL Ajustes de aplicación] > [!UICONTROL Valores preestablecidos de conjunto por lotes] > [!UICONTROL Valor preestablecido de conjunto por lotes]**.

   **[!UICONTROL Formulario]** de vista, tal como se define en la esquina superior derecha de la página Detalles, es la vista predeterminada.

1. En el panel Lista de ajustes preestablecidos, toque **[!UICONTROL Añadir]** para activar los campos de definición en el panel Detalles del lado derecho de la pantalla.
1. En el panel Detalles, en el campo Nombre de ajuste preestablecido, escriba un nombre para el ajuste preestablecido.
1. En el menú desplegable Tipo de conjunto de lotes, seleccione **[!UICONTROL Conjunto de recursos.]**
1. En la lista desplegable Subtipo, seleccione **[!UICONTROL Conjunto de giros con varios ejes.]**
1. Expanda **[!UICONTROL Convenciones de nombres de recursos]** y, a continuación, en la lista desplegable Nombres de archivos, toque **[!UICONTROL Personalizado.]**
1. Utilice los atributos **[!UICONTROL Coincidencia]** y, opcionalmente, **[!UICONTROL Nombre base]** para establecer una expresión regular para la asignación de nombres a los recursos de imagen que conforman la agrupación.

   Por ejemplo, la expresión regular de coincidencia literal puede tener el siguiente aspecto:

   `(w+)-w+-w+`

1. Expanda **[!UICONTROL Posición de columna de fila]** y, a continuación, defina el formato de nombre para la posición del recurso de imagen dentro de la matriz Conjunto de giros 2D.

   Utilice el paréntesis para abarcar la posición de fila o columna en el nombre del archivo.

   Por ejemplo, para la expresión regular de fila, puede tener el siguiente aspecto:

   `\w+-R([0-9]+)-\w+`

   o

   `\w+-(\d+)-\w+`

   Para la expresión regular de columna, puede tener el siguiente aspecto:

   `\w+-\w+-C([0-9]+)`

   o

   `\w+-\w+-C(\d+)`

   Los ejemplos anteriores son únicamente ilustrativos. Puede crear la expresión normal según sus necesidades.

   >[!NOTE]
   Si la combinación de expresiones regulares de filas y columnas no puede determinar la posición del recurso dentro de la matriz de conjuntos de giros multidimensionales, el recurso no se agrega al conjunto. También se registra un error.

1. Para la convención de creación y nombre de conjunto, especifique el sufijo o el prefijo del nombre base definido en la convención de nombres de recursos.

   Además, defina dónde se creará el conjunto de giros en la estructura de carpetas de Dynamic Media Classic.

   Si define un gran número de conjuntos, mantenga los conjuntos separados de las carpetas que contienen los propios recursos. Por ejemplo, cree una carpeta Conjuntos de giros para colocar los conjuntos generados aquí.

1. En el panel Detalles, toque **[!UICONTROL Guardar.]**
1. Toque **[!UICONTROL Activo]** junto al nuevo nombre de ajuste preestablecido.

   Al activar el ajuste preestablecido, se garantiza que al cargar recursos en Dynamic Media, el ajuste preestablecido de conjunto de lotes se aplica para generar el conjunto.

### (Opcional) Ajuste del rendimiento de Dynamic Media: modo Scene7 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Para mantener el modo Dynamic Media - Scene7 funcionando sin problemas, Adobe recomienda los siguientes consejos de ajuste de escalabilidad/rendimiento de sincronización:

* Actualización de los parámetros de trabajo predefinidos para el procesamiento de diferentes formatos de archivo.
* Actualización de los subprocesos de trabajo de la cola de Granite (recursos de vídeo) predefinidos.
* Actualizando los subprocesos de trabajo en cola predefinidos de flujo de trabajo transitorio de Granite (imágenes y recursos que no son de vídeo).
* Actualización de las conexiones de carga máximas al servidor de Dynamic Media Classic.

#### Actualización de los parámetros de trabajo predefinidos para el procesamiento de diferentes formatos de archivo

Puede ajustar los parámetros de trabajo para un procesamiento más rápido al cargar archivos. Por ejemplo, si está cargando archivos PSD pero no desea procesarlos como plantillas, puede establecer la extracción de capas en false (desactivado). En ese caso, el parámetro de trabajo ajustado aparecerá como `process=None&createTemplate=false`.

Adobe recomienda utilizar los siguientes parámetros de trabajo &quot;optimizados&quot; para archivos PDF, PostScript® y PSD:

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| Tipo de archivo | Parámetros de trabajo recomendados |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=Layername&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

Para actualizar cualquiera de estos parámetros, siga los pasos de [Activación de la compatibilidad con parámetros de trabajo de carga MIME basados en tipos/Dynamic Media Classic](#enabling-mime-type-based-assets-scene-upload-job-parameter-support).

#### Actualizando la cola de flujo de trabajo transitorio de Granite {#updating-the-granite-transient-workflow-queue}

La cola de flujo de trabajo de tránsito de granito se utiliza para el flujo de trabajo **[!UICONTROL recurso de actualización de DAM]**. En Dynamic Media, se utiliza para la ingestión y el procesamiento de imágenes.

**Para actualizar la cola de flujo de trabajo transitorio de Granite**

1. Vaya a [https://&lt;server>/system/console/configMgr](https://localhost:4502/system/console/configMgr) y busque **Queue: Granite Transient Workflow Queue**.

   >[!NOTE]
   Se necesita una búsqueda de texto en lugar de una dirección URL directa porque el OSGi PID se genera de forma dinámica.

1. En el campo **[!UICONTROL Número máximo de trabajos paralelos]**, cambie el número al valor deseado.

   Puede aumentar **[!UICONTROL Número máximo de trabajos paralelos]** para admitir adecuadamente la carga pesada de archivos a Dynamic Media. El valor exacto depende de la capacidad del hardware. En determinados escenarios (es decir, una migración inicial o una carga masiva única) puede utilizar un valor grande. Sin embargo, tenga en cuenta que el uso de un valor grande (por ejemplo, dos veces el número de núcleos) puede tener efectos negativos en otras actividades simultáneas. Como tal, pruebe y ajuste el valor en función de su caso de uso particular.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Toque **[!UICONTROL Guardar.]**

#### Actualizando la cola de flujo de trabajo de Granite {#updating-the-granite-workflow-queue}

La cola Granite Workflow se utiliza para flujos de trabajo no transitorios. En Dynamic Media, solía procesar vídeo con el flujo de trabajo **[!UICONTROL Dynamic Media Encode Video]**.

**Para actualizar la cola de flujo de trabajo de Granite**

1. Vaya a `https://<server>/system/console/configMgr` y busque **Cola: Cola de flujo de trabajo de granito**.

   >[!NOTE]
   Se necesita una búsqueda de texto en lugar de una dirección URL directa porque el OSGi PID se genera de forma dinámica.

1. En el campo **[!UICONTROL Número máximo de trabajos paralelos]**, cambie el número al valor deseado.

   Puede aumentar el número máximo de trabajos paralelos para admitir correctamente la carga pesada de archivos en Dynamic Media. El valor exacto depende de la capacidad del hardware. En determinados escenarios (es decir, una migración inicial o una carga masiva única) puede utilizar un valor grande. Sin embargo, tenga en cuenta que el uso de un valor grande (por ejemplo, dos veces el número de núcleos) puede tener efectos negativos en otras actividades simultáneas. Como tal, pruebe y ajuste el valor en función de su caso de uso particular.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Toque **[!UICONTROL Guardar.]**

#### Actualización de la conexión de carga de Dynamic Media Classic {#updating-the-scene-upload-connection}

La configuración de la conexión de carga de Scene7 sincroniza los recursos de Experience Manager con los servidores de Dynamic Media Classic.

**Para actualizar la conexión de carga de Dynamic Media Classic**

1. Ir a `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. En el campo **[!UICONTROL Número de conexiones]** y/o el campo **[!UICONTROL Tiempo de espera de trabajo activo]**, cambie el número como desee.

   La configuración **[!UICONTROL Número de conexiones]** controla el número máximo de conexiones HTTP permitidas para la carga de Experience Manager a Dynamic Media; normalmente, el valor predefinido de diez conexiones es suficiente.

   La configuración **[!UICONTROL Tiempo de espera de trabajo activo]** determina el tiempo de espera para que los recursos de Dynamic Media cargados se publiquen en el servidor de envío. Este valor es 2100 segundos o 35 minutos de forma predeterminada.

   Para la mayoría de los casos de uso, el ajuste de 2100 es suficiente.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Toque **[!UICONTROL Guardar.]**

### (Opcional) Filtrado de recursos para replicación {#optional-filtering-assets-for-replication}

En implementaciones que no son de Dynamic Media, se replican *todos* recursos (tanto imágenes como vídeo) desde el entorno de creación de Experience Manager al nodo de publicación de Experience Manager. Este flujo de trabajo es necesario porque los servidores de publicación Experience Manager también envían los recursos.

Sin embargo, en las implementaciones de Dynamic Media, como los recursos se entregan mediante el Cloud Service, no es necesario replicarlos en nodos de publicación de Experience Manager. Este flujo de trabajo de &quot;publicación híbrida&quot; evita costes de almacenamiento adicionales y tiempos de procesamiento más largos para replicar recursos. Otros contenidos, como las páginas del sitio, se siguen ofreciendo desde los nodos de publicación del Experience Manager.

Los filtros proporcionan una manera de *excluir* recursos de la replicación en el nodo de publicación de Experience Manager.

#### Uso de filtros de recursos predeterminados para replicación {#using-default-asset-filters-for-replication}

Si utiliza Dynamic Media para imágenes, vídeos o ambos, puede utilizar los filtros predeterminados que Adobe proporciona tal cual. Los siguientes filtros están activos de forma predeterminada:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Filtro</strong></td>
   <td><strong>Tipo MIME</strong></td>
   <td><strong>Representaciones</strong></td>
  </tr>
  <tr>
   <td>Dynamic Media Image Envío</td>
   <td><p>filter-images</p> <p>filter-sets</p> <p> </p> </td>
   <td><p>Inicios con <strong>imagen/</strong></p> <p>Contiene <strong>application/</strong> y termina con <strong>set</strong>.</p> </td>
   <td>Las "imágenes de filtro" integradas (se aplican a recursos de imágenes únicas, incluidas imágenes interactivas) y "conjuntos de filtros" (se aplican a conjuntos de giros, conjuntos de imágenes, conjuntos de medios mixtos y conjuntos de carrusel):
    <ul>
     <li>Excluya de la replicación la imagen original y las representaciones de imágenes estáticas.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media Video Envío</td>
   <td>filter-video</td>
   <td>Inicios con <strong>video/</strong></td>
   <td>El "video-filtro" incorporado:
    <ul>
     <li>Excluya de la replicación el vídeo original y las representaciones de miniaturas estáticas.<br /> <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
Los filtros se aplican a tipos MIME y no pueden ser específicos de la ruta.

#### Personalización de filtros de recursos para replicación {#customizing-asset-filters-for-replication}

1. En Experience Manager, toque el logotipo del Experience Manager para acceder a la consola de navegación global y toque el CRXDE Lite **[!UICONTROL Herramientas > General >]**.
1. En el árbol de carpetas de la izquierda, vaya a `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` para revisar los filtros.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. Para definir el tipo de MIME para el filtro, puede localizar el tipo de MIME de la siguiente manera:

   En el carril izquierdo, expanda `content > dam > <locate_your_asset> > jcr:content > metadata` y, a continuación, en la tabla, localice `dc:format`.

   El siguiente gráfico es un ejemplo de la ruta de un recurso a `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Observe que `dc:format` para el recurso `Fiji Red.jpg` es `image/jpeg`.

   Para que este filtro se aplique a todas las imágenes, independientemente de su formato, establezca el valor en `image/*` donde `*` es una expresión normal que se aplica a todas las imágenes de cualquier formato.

   Para que el filtro solo se aplique a imágenes del tipo JPEG, introduzca un valor de `image/jpeg`.

1. Defina qué representaciones desea incluir o excluir de la replicación.

   Los caracteres que se pueden usar para filtrar para la replicación son los siguientes:

<table>
 <tbody>
  <tr>
   <td><strong>Carácter que utilizar</strong></td>
   <td><strong>Filtros de recursos para replicación</strong></td>
  </tr>
  <tr>
   <td>*</td>
   <td>Carácter comodín<br /> </td>
  </tr>
  <tr>
   <td>+</td>
   <td>Incluye recursos para replicación.</td>
  </tr>
  <tr>
   <td>-</td>
   <td>Excluye los recursos de la replicación.</td>
  </tr>
 </tbody>
</table>

Ir a `content/dam/<locate your asset>/jcr:content/renditions`.

El siguiente gráfico es un ejemplo de las representaciones de un recurso.

![climage_1-4](assets/chlimage_1-4.png)

Si sólo desea replicar el original, debe ingresar `+original`.

