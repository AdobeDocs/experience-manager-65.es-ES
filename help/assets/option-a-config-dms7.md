---
title: 'OPCIÓN A: Configurar Dynamic Media: modo Scene7'
description: Obtenga información sobre cómo configurar Dynamic Media en modo Scene7.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
mini-toc-levels: 3
hide: true
hidefromtoc: true
feature: Configuration,Scene7 Mode
exl-id: null
source-git-commit: b6000516b88342d6abf8072623cfece43e2ba19d
workflow-type: tm+mt
source-wordcount: '11571'
ht-degree: 3%

---

# OPCIÓN A: Configurar Dynamic Media: modo Scene7{#configuring-dynamic-media-scene-mode}

>[!NOTE]
>
>OPCIÓN A: SE ELIMINAN LOS DOS TEMAS NUEVOS QUE ESCRIBÍ. PERO ANTES DE ELIMINAR LOS TEMAS, TODO SU CONTENIDO SE TRASLADÓ A ESTE TEMA, A LAS RESPECTIVAS ÁREAS EN LAS QUE YA HABLO DE CONFIGURACIÓN GENERAL Y CONFIGURACIÓN DE PUBLICACIÓN.

Si utiliza la configuración de Adobe Experience Manager para diferentes entornos, como desarrollo, ensayo y producción, configure los Cloud Services de Dynamic Media para cada uno de esos entornos.

## Diagrama de arquitectura de Dynamic Media: modo Scene7 {#architecture-diagram-of-dynamic-media-scene-mode}

**RIESGO: CONSERVAR TAL CUAL**

En el diagrama de arquitectura siguiente se describe cómo funciona el modo Dynamic Media - Scene7.

Con la nueva arquitectura, Experience Manager es responsable de los recursos de origen principales y de las sincronizaciones con Dynamic Media para el procesamiento y la publicación de recursos:

1. Cuando el recurso de origen principal se carga en Experience Manager, se replica en Dynamic Media. En este punto, Dynamic Media gestiona todo el procesamiento de recursos y la generación de representaciones, como la codificación de vídeo y las variantes dinámicas de una imagen.
(En el modo Dynamic Media - Scene7, el tamaño predeterminado del archivo de carga es de 2 GB o menos. Para habilitar el tamaño de los archivos de carga de 2 GB hasta 15 GB, consulte [(Opcional) Configuración de Dynamic Media: modo Scene7 para cargar recursos de más de 2 GB](#optional-config-dms7-assets-larger-than-2gb).)
1. Una vez generadas las representaciones, el Experience Manager puede acceder de forma segura a las representaciones de Dynamic Media remotas y obtener una vista previa de ellas (no se devuelven binarios a la instancia de Experience Manager).
1. Una vez que el contenido está listo para publicarse y aprobarse, se déclencheur al servicio Dynamic Media para enviar el contenido a los servidores de entrega y almacenar el contenido en caché en la CDN (Red de entrega de contenido).

![chlimage_1-550](assets/chlimage_1-550.png)

>[!IMPORTANT]
>
>La siguiente lista de funciones requiere que utilice la CDN predeterminada incluida con Adobe Experience Manager - Dynamic Media. Ninguna otra CDN personalizada es compatible con estas funciones.
>
>* [Imágenes inteligentes](/help/assets/imaging-faq.md)
>* [Invalidación de caché](/help/assets/invalidate-cdn-cache-dynamic-media.md)
>* [Protección de Hotlink](/help/assets/hotlink-protection.md)
>* [Entrega de contenido HTTP/2](/help/assets/http2.md)
>* Redireccionamiento de URL a nivel de CDN
>* Akamai ChinaCDN (para una entrega óptima en China)


## Habilitar Dynamic Media en modo Scene7 {#enabling-dynamic-media-in-scene-mode}

**RIESGO: CONSERVAR TAL CUAL**

[Dynamic Media está desactivado de forma predeterminada. ](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) Para aprovechar las funciones de Dynamic Media, debe activarlas.

>[!WARNING]
>
>Dynamic Media: el modo Scene7 es para la variable *Solo instancia de autor Experience Manager*. Como tal, debe configurar `runmode=dynamicmedia_scene7` en la instancia de autor del Experience Manager, *not* la instancia de publicación de Experience Manager.

Para habilitar Dynamic Media, debe iniciar el Experience Manager utilizando la variable `dynamicmedia_scene7` ejecute el modo desde la línea de comandos introduciendo lo siguiente en una ventana de terminal (por ejemplo, el puerto utilizado es 4502):

```shell
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## (Opcional) Migre los ajustes preestablecidos y configuraciones de Dynamic Media de la versión 6.3 a la versión 6.5 de cero tiempo de inactividad {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

**RIESGO: CONSERVAR TAL CUAL**

La actualización de Experience Manager Dynamic Media de 6.3 a 6.4 o 6.5 ahora incluye la capacidad de no realizar implementaciones de downtime. Para migrar todos los ajustes preestablecidos y configuraciones desde `/etc` a `/conf` en CRXDE Lite, asegúrese de ejecutar el siguiente comando curl.

>[!NOTE]
>
>Si ejecuta la instancia de Experience Manager en modo de compatibilidad (es decir, tiene instalada la compatibilidad empaquetada), no es necesario ejecutar estos comandos.

Para todas las actualizaciones, ya sea con o sin el paquete de compatibilidad, puede copiar los ajustes preestablecidos de visor predeterminados y listos para usar que se incluyeron originalmente con Dynamic Media ejecutando el siguiente comando Linux® curl:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

Para migrar cualquier ajuste preestablecido de visualizador personalizado y configuración que haya creado a partir de `/etc` a `/conf`, ejecute el siguiente comando curl de Linux®:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## Instalación del paquete de características 18912 para la migración masiva de recursos {#installing-feature-pack-for-bulk-asset-migration}

**RIESGO: CONSERVAR TAL CUAL**

La instalación del paquete de características 18912 es *opcional*.

El paquete de funciones 18912 le permite ingerir recursos de forma masiva mediante FTP o migrar recursos desde Dynamic Media (modo híbrido) o Dynamic Media Classic a Dynamic Media (modo Scene7 en Experience Manager). Está disponible en [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

Consulte [Instalación del paquete de características 18912 para la migración masiva de recursos](/help/assets/bulk-ingest-migrate.md) para obtener más información.

## Crear una configuración de Dynamic Media en Cloud Services {#configuring-dynamic-media-cloud-services}

**RIESGO: CONSERVAR TAL CUAL**

**Antes de configurar Dynamic Media** - Después de recibir el correo electrónico de aprovisionamiento con las credenciales de Dynamic Media, debe abrir el [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), luego inicie sesión en su cuenta para cambiar su contraseña. La contraseña proporcionada en el correo electrónico de aprovisionamiento se genera en el sistema y se pretende que sea solo una contraseña temporal. Es importante que actualice la contraseña para que el Cloud Service de Dynamic Media esté configurado con las credenciales correctas.

![dynamic mediaconfiguration2update](assets/dynamicmediaconfiguration2updated.png)

**Para crear una configuración de Dynamic Media en Cloud Services:**

1. En el modo Autor de Experience Manager, seleccione el logotipo de Experience Manager para acceder a la consola de navegación global, seleccione el icono Herramientas y, a continuación, vaya a **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de Dynamic Media]**.
1. En la página Explorador de configuración de Dynamic Media, en el panel izquierdo, seleccione **[!UICONTROL global]** (no seleccione el icono de carpeta a la izquierda de **[!UICONTROL global]**) y, a continuación, seleccione **[!UICONTROL Crear]**.
1. En el **[!UICONTROL Crear configuración de Dynamic Media]** , introduzca un título, la dirección de correo electrónico de la cuenta de Dynamic Media, la contraseña y, a continuación, seleccione su región. Esta información se proporciona por Adobe en el correo electrónico de aprovisionamiento. Póngase en contacto con el servicio de atención al cliente de Adobe si no recibió el correo electrónico.

   Select **[!UICONTROL Conectarse a Dynamic Media]**.

   >[!NOTE]
   **RIESGO: ¿MANTÉNGASE ASÍ?** Cuando reciba el correo electrónico de aprovisionamiento con credenciales de Dynamic Media, abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), luego inicie sesión en su cuenta para cambiar su contraseña. La contraseña proporcionada en el correo electrónico de aprovisionamiento se genera en el sistema y se pretende que sea solo una contraseña temporal. Es importante que actualice la contraseña para que el Cloud Service de Dynamic Media esté configurado con las credenciales correctas.

1. Cuando la conexión se realice correctamente, establezca lo siguiente. Los encabezados con un asterisco (*) son obligatorios:

   * **[!UICONTROL Empresa]** - el nombre de la cuenta de Dynamic Media. Tiene varias cuentas de Dynamic Media. Por ejemplo, puede tener diferentes submarcas, divisiones, entornos de ensayo o producción.

   * **[!UICONTROL Ruta de carpeta raíz de la empresa]**

   * **[!UICONTROL Publicación de recursos]** - Puede elegir entre las tres opciones siguientes:
      * **[!UICONTROL Inmediatamente]** significa que, cuando se cargan los recursos, el sistema los incorpora y proporciona la URL o la Incrustar al instante. No es necesario que el usuario intervenga para publicar recursos.
      * **[!UICONTROL Tras la activación]** significa que debe publicar explícitamente el recurso primero antes de proporcionar un vínculo de URL/incrustación.<br><!-- CQDOC-17478, Added March 9, 2021-->A partir de Experience Manager 6.5.8, la instancia de publicación de Experience Manager refleja valores de metadatos Dynamic Media precisos, como `dam:scene7Domain` y `dam:scene7FileStatus` en **[!UICONTROL Tras la activación]** solo en modo de publicación. Para habilitar esta funcionalidad, instale Service Pack 8 y, a continuación, reinicie el Experience Manager. Vaya al Administrador de configuración de Sling. Busque la configuración para `Scene7ActivationJobConsumer Component` o crear uno nuevo). Seleccione la casilla de verificación **[!UICONTROL Replicar metadatos después de la publicación de Dynamic Media]** y, a continuación, seleccione **[!UICONTROL Guardar]**.

         ![Duplicación de metadatos después de la casilla de verificación de publicación de Dynamic Media](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL Publicación selectiva]** Esta opción le permite controlar qué carpetas se publican en Dynamic Media. Permite utilizar funciones como Recorte inteligente o representaciones dinámicas, o determinar qué carpetas se publican exclusivamente en Experience Manager para la vista previa. Los mismos activos son *not* publicado en Dynamic Media para su entrega en el dominio público.<br>Puede establecer esta opción aquí en la **[!UICONTROL Configuración de Dynamic Media Cloud]** o, si lo prefiere, puede elegir establecer esta opción en el nivel de carpeta, en el **[!UICONTROL Propiedades]**.<br>Consulte [Trabajar con publicación selectiva en Dynamic Media](/help/assets/selective-publishing.md).<br>Si más adelante cambia esta configuración o la cambia posteriormente a nivel de carpeta, esos cambios solo afectarán a los nuevos recursos que cargue a partir de ese momento. El estado de publicación de los recursos existentes en la carpeta permanece tal cual hasta que los cambie manualmente de **[!UICONTROL Publicación rápida]** o **[!UICONTROL Administrar publicación]** para abrir el Navegador.
   * **[!UICONTROL Servidor de vista previa seguro]** - permite especificar la ruta URL del servidor de vista previa de representaciones seguras. Es decir, una vez generadas las representaciones, el Experience Manager puede acceder y previsualizar de forma segura las representaciones de Dynamic Media remotas (no se devuelven binarios a la instancia de Experience Manager).
A menos que tenga una disposición especial para utilizar el servidor de su propia empresa o un servidor especial, Adobe recomienda que deje esta configuración como se ha especificado.

   * **[!UICONTROL Sincronizar todo el contenido]** - <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->Seleccionado de forma predeterminada. Anule la selección de esta opción si desea incluir o excluir selectivamente recursos de la sincronización con Dynamic Media. Al anular la selección de esta opción, puede elegir entre los dos modos de sincronización de Dynamic Media siguientes:

   * **[!UICONTROL Modo de sincronización de Dynamic Media]**
      * **[!UICONTROL Habilitado de forma predeterminada]** - La configuración se aplica a todas las carpetas de forma predeterminada, a menos que marque una carpeta específicamente para la exclusión. <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL Deshabilitado de forma predeterminada]** - La configuración no se aplica a ninguna carpeta hasta que marque explícitamente una carpeta seleccionada para sincronizar con Dynamic Media.
Para marcar una carpeta seleccionada para sincronizar con Dynamic Media, seleccione una carpeta de recursos y, en la barra de herramientas, seleccione **[!UICONTROL Propiedades]**. En el **[!UICONTROL Detalles]** en la **[!UICONTROL Modo de sincronización de Dynamic Media]** , elija entre las tres opciones siguientes. Cuando haya terminado, seleccione **[!UICONTROL Guardar]**. *Recuerde: estas tres opciones no están disponibles si ha seleccionado **[!UICONTROL Sincronizar todo el contenido]**más temprano.* Consulte también [Trabajar con publicación selectiva en el nivel de carpeta en Dynamic Media](/help/assets/selective-publishing.md).
         * **[!UICONTROL Heredado]** - No hay ningún valor de sincronización explícito en la carpeta; en su lugar, la carpeta hereda el valor de sincronización de una de sus carpetas antecesoras o el modo predeterminado en la configuración de nube. El estado detallado de heredado se muestra mediante una información del objeto.
         * **[!UICONTROL Habilitar para subcarpetas]** - Incluya todo en este subárbol para sincronizar con Dynamic Media. La configuración específica de la carpeta anula el modo predeterminado en la configuración de la nube.
         * **[!UICONTROL Deshabilitado para subcarpetas]** - Excluya todo lo que se encuentra en este subárbol de la sincronización con Dynamic Media.

   >[!NOTE]
   No se admite el control de versiones en DMS7. Además, la activación retrasada solo se aplica si **[!UICONTROL Publicar recursos]** en la página Editar configuración de Dynamic Media está configurada en **[!UICONTROL Al activarse]** y, a continuación, solo hasta la primera vez que se activa el recurso.
   Una vez activado un recurso, las actualizaciones se publican inmediatamente en S7 Delivery.

1. Seleccione **[!UICONTROL Guardar]**.
1. Para previsualizar de forma segura el contenido de Dynamic Media antes de publicarlo, debe &quot;lista de permitidos&quot; la instancia de autor del Experience Manager para conectarse a Dynamic Media:

   * **RIESGO: VÍNCULO AL NUEVO TEMA DE CONFIGURACIÓN DE PUBLICACIÓN** Abra el [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), luego inicie sesión en su cuenta. Adobe proporcionó las credenciales y los detalles de inicio de sesión en el momento del aprovisionamiento. Si no tiene esta información, póngase en contacto con el servicio de atención al cliente de Adobe.

   * En la barra de navegación cerca de la parte superior derecha de la página, vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración de publicación]** > **[!UICONTROL Servidor de imágenes]**.

   * En la página Publicación del servidor de imágenes , en la lista desplegable Contexto de publicación , seleccione **[!UICONTROL Probar servicio de imágenes]**.
   * Para el filtro de direcciones de cliente, seleccione **[!UICONTROL Agregar]**.
   * Para activar la dirección, seleccione la casilla de verificación. Introduzca la dirección IP de la instancia de Autor del Experience Manager (no la IP de Dispatcher).
   * Seleccione **[!UICONTROL Guardar]**.

Ya ha finalizado con la configuración básica; está listo para usar el modo Dynamic Media - Scene7 .

Si desea personalizar aún más la configuración, puede completar opcionalmente cualquiera de las tareas de [(Opcional) Configuración avanzada en Dynamic Media: modo Scene7](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

## (Opcional) Configuración avanzada en Dynamic Media: modo Scene7 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

**RIESGO: CONSERVAR TAL CUAL**

Si desea personalizar aún más la configuración y la configuración del modo Dynamic Media - Scene7 o optimizar su rendimiento, puede realizar una o más de las siguientes acciones: *opcional* tareas:

* [(Opcional) Configuración de Dynamic Media: modo Scene7 para cargar recursos de más de 2 GB](#optional-config-dms7-assets-larger-than-2gb)
* [(Opcional) Configuración de Dynamic Media Publish](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)
   * [(Opcional) Pruebe los recursos antes de hacerlos públicos](#test-assets-before-making-public)
* [(Opcional) Configuración general de Dynamic Media](#configuring-application-general-settings)
* [(Opcional) Tareas de configuración adicionales](#additional-configuration-tasks)
* [(Opcional) Ajuste el rendimiento del modo Dynamic Media - Scene7](#optional-tuning-the-performance-of-dynamic-media-scene-mode)
* [(Opcional) Filtrar recursos para la replicación](#optional-filtering-assets-for-replication)

### (Opcional) Configuración de Dynamic Media: modo Scene7 para cargar recursos de más de 2 GB {#optional-config-dms7-assets-larger-than-2gb}

**RIESGO: CONSERVAR TAL CUAL**

En el modo Dynamic Media - Scene7, el tamaño predeterminado del archivo de carga de recursos es de 2 GB o menos. Sin embargo, si lo desea, puede configurar la carga de recursos de más de 2 GB y hasta 15 GB.

Si tiene intención de utilizar esta función, tenga en cuenta los siguientes requisitos previos y puntos:

* Debe ejecutar Experience Manager 6.5 con Service Pack 6.5.4.0 o posterior en el modo Dynamic Media - Scene7.
* Esta función de carga grande solo es compatible con [*Managed Services*](https://business.adobe.com/products/experience-manager/managed-services.html) clientes.
* Asegúrese de que la instancia de Experience Manager esté configurada con Amazon S3 o el almacenamiento del blob de Microsoft® Azure.

   >[!NOTE]
   Configure el almacenamiento del blob de Azure con una clave de acceso y una clave secreta porque esta función de carga grande no es compatible con AzureSas en la configuración de almacenamiento del blob.

* Oak&#39;s [Descarga de Direct Binary Access](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html) está habilitado (Oak&#39;s *Carga de acceso binario directo* no es obligatorio).

   Para habilitar la descarga de Direct Binary Access, establezca la propiedad `presignedHttpDownloadURIExpirySeconds > 0` en la configuración del almacén de datos. El valor debe ser lo suficientemente largo como para descargar binarios más grandes y, posiblemente, volver a intentarlo.

* Los activos mayores de 15 GB no se cargan. (El límite de tamaño se establece en el paso 8 siguiente.)
* Cuando la variable **[!UICONTROL Reprocesamiento de Dynamic Media]** el flujo de trabajo de recursos se activa en una carpeta, vuelve a procesar los recursos grandes que ya estén sincronizados con la empresa de Dynamic Media. Sin embargo, si algún recurso grande aún no se ha sincronizado en la carpeta, no se carga el recurso. Por lo tanto, para sincronizar recursos grandes existentes en Dynamic Media, puede ejecutar **[!UICONTROL Reprocesamiento de Dynamic Media]** flujo de trabajo de recursos en recursos individuales.

**Para configurar el modo Dynamic Media - Scene7 para la carga de recursos de más de 2 GB:**

1. En el Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.

1. En la ventana del CRXDE Lite, realice una de las acciones siguientes:

   * En el carril izquierdo, vaya a la siguiente ruta:

      `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * Copie y pegue la ruta de acceso superior en el campo de ruta del CRXDE Lite debajo de la barra de herramientas y, a continuación, pulse `Enter`.

1. En el carril izquierdo, haga clic con el botón derecho en `fileupload`y, en el menú emergente, seleccione **[!UICONTROL Nodo de superposición]**.

   ![Opción Nodo de superposición](/help/assets/assets-dm/uploadassets15gb_a.png)

1. En el cuadro de diálogo Nodo de superposición, seleccione la opción **[!UICONTROL Coincidir tipos de nodo]** para activar la opción y, a continuación, seleccione **[!UICONTROL OK]**.

   ![Cuadro de diálogo Nodo de superposición](/help/assets/assets-dm/uploadassets15gb_b.png)

1. Desde la ventana del CRXDE Lite, realice una de las siguientes acciones:

   * En el carril izquierdo, vaya a la siguiente ruta de nodo de superposición:

      `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * Copie y pegue la ruta de acceso superior en el campo de ruta del CRXDE Lite debajo de la barra de herramientas y, a continuación, pulse `Enter`.

1. En el **[!UICONTROL Propiedades]** en la **[!UICONTROL Nombre]** columna, localizar `sizeLimit`.
1. A la derecha del `sizeLimit` nombre, en el **[!UICONTROL Valor]** , haga doble clic en el campo de valor.
1. Introduzca el valor adecuado en bytes para poder aumentar el límite de tamaño hasta el tamaño de carga máximo deseado. Por ejemplo, para aumentar el límite de tamaño del recurso de carga a 10 GB, introduzca `10737418240` en el campo value .
Puede introducir un valor de hasta 15 GB (`2013265920` bytes). En este caso, los recursos cargados que tengan más de 15 GB no se cargan.


   ![Valor límite de tamaño](/help/assets/assets-dm/uploadassets15gb_c.png)

1. Cerca de la esquina superior izquierda de la ventana del CRXDE Lite, seleccione **[!UICONTROL Guardar todo]**.

   *Ahora establezca el tiempo de espera para el controlador de trabajo de proceso externo de Adobe Granite Workflow haciendo lo siguiente:*

1. En el Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global.
1. Realice una de las siguientes acciones:

   * Vaya a la siguiente ruta de URL:

      `localhost:4502/system/console/configMgr/com.adobe.granite.workflow.core.job.ExternalProcessJobHandler`

   * Copie y pegue la ruta anterior en el campo URL del explorador. Asegúrese de reemplazar `localhost:4502` con su propia instancia de Experience Manager.

1. En el **[!UICONTROL Controlador de trabajos de proceso externo de flujo de trabajo de Granite de Adobe]** en el **[!UICONTROL Tiempo de espera máximo]** , establezca el valor en `18000` minutos (cinco horas). El valor predeterminado es 10 800 minutos (tres horas).

   ![Valor máximo de tiempo de espera](/help/assets/assets-dm/uploadassets15gb_d.png)

1. En la esquina inferior derecha del cuadro de diálogo, seleccione **[!UICONTROL Guardar]**.

   *Ahora, establezca el tiempo de espera para el proceso de carga binaria directa de Scene7 siguiendo estos pasos:*

1. En el Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global.
1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página Modelos de flujo de trabajo , seleccione **[!UICONTROL Codificar vídeo de Dynamic Media]**.
1. En la barra de herramientas, seleccione **[!UICONTROL Editar]**.
1. En la página de flujo de trabajo, haga doble clic en el botón **[!UICONTROL Carga binaria directa de Scene7]** paso del proceso.
1. En el **[!UICONTROL Propiedades de los pasos]** en el **[!UICONTROL Frecuentes]** en la **[!UICONTROL Configuración avanzada]** en el **[!UICONTROL Tiempo de espera]** , introduzca un valor de `18000` minutos (cinco horas). El valor predeterminado es `3600` minutos (una hora).
1. Select **[!UICONTROL OK]**.
1. Select **[!UICONTROL Sincronización]**.
1. Repita los pasos 14-21 para el **[!UICONTROL Recurso de actualización DAM]** modelo de flujo de trabajo y **[!UICONTROL Reprocesamiento de Dynamic Media]** modelo de flujo de trabajo.

### (Opcional) Configuración de Dynamic Media Publish {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

**RIESGO: TODO EL CONTENIDO DEL NUEVO TEMA DE CONFIGURACIÓN DE PUBLICACIÓN AÑADIDO AQUÍ**

>[!IMPORTANT]
La configuración de Dynamic Media Publish solo está disponible si:
* Está ejecutando Dynamic Media en modo Scene7.
* Tiene un *existente* **[!UICONTROL Configuración de Dynamic Media]** (en **[!UICONTROL Cloud Services]**) en Adobe Experience Manager 6.5 o en Experience Manager as a Cloud Service.
* Es administrador del sistema del Experience Manager con privilegios de administrador.


La configuración de la página Configuración de publicación de Dynamic Media determina cómo se envían los recursos de forma predeterminada desde los servidores Dynamic Media de Adobe a los sitios web o las aplicaciones. Si no se especifica ninguna configuración, el servidor Dynamic Media de Adobe envía un recurso de acuerdo con la configuración predeterminada de una página de configuración de publicación. Por ejemplo, una solicitud para enviar una imagen que no incluya un atributo de resolución genera una imagen con la configuración Resolución de objeto predeterminada en la página Servidor de imágenes.

Los administradores pueden cambiar la configuración predeterminada de las páginas Servidor de imágenes, Procesador de imágenes y viñeta para establecer la configuración predeterminada para enviar recursos desde servidores.

>[!NOTE]
La configuración de publicación de Dynamic Media está diseñada para que la utilicen desarrolladores y programadores experimentados de sitios web. Adobe recomienda que los usuarios que cambian cualquiera de estas configuraciones de publicación predeterminadas estén familiarizados con Dynamic Media de Adobe, las normas y convenciones de protocolo HTTP y la tecnología básica de creación de imágenes.

**Para configurar la configuración de publicación de Dynamic Media:**

1. En el modo Autor del Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global.
1. En el carril izquierdo, seleccione el icono Herramientas y, a continuación, vaya a **[!UICONTROL Recursos]** > **[!UICONTROL Configuración de Dynamic Media Publish]**.
1. En la página Servidor de imágenes , establezca el contexto de publicación de Image Server y, a continuación, utilice las cinco pestañas para configurar los ajustes de publicación predeterminados.

   * [Servidor de imágenes](#image-server)
   * [Seguridad](#security-tab) ficha
   * [Administración de catálogos](#catalog-management-tab) ficha
   * [Atributos de solicitud](#request-attributes-tab) ficha
   * [Atributos de miniatura comunes](#common-thumbnail-attributes-tab) ficha
   * [Atributos de gestión de color](#color-management-attributes-tab) ficha

   ![Página Configuración de publicación de Dynamic Media](/help/assets/assets-dm/dm-publish-setup.png)
   *Configuración de publicación de Dynamic Media , con la variable **[!UICONTROL Atributos de solicitud]**seleccionada.*<br><br>

1. Cuando haya terminado, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]**.

#### Servidor de imágenes {#image-server}

La página Servidor de imágenes establece la configuración predeterminada para enviar imágenes desde los servidores de imágenes. La configuración está disponible en cinco categorías

| Contexto de publicación | Descripción |
| --- | --- |
| Servicio de imágenes | Especifica el contexto para la configuración de publicación. |
| Probar servicio de imágenes | Especifica el contexto para probar la configuración de publicación.<br>Consulte [Probar recursos antes de hacerlos públicos](#test-assets-before-making-public). |

#### Ficha Seguridad {#security-tab}

**[!UICONTROL Dirección del cliente]** - Permite especificar una o más direcciones IP o intervalos de direcciones IP. Cuando se especifica, se rechazan las solicitudes a este catálogo de imágenes que se originan en un cliente con una dirección IP no incluida en la lista. Esta regla se aplica tanto a la entrega de imágenes como a las imágenes procesadas.

#### Ficha Administración del catálogo {#catalog-management-tab}

**[!UICONTROL Ruta del archivo de definición del conjunto de reglas]** - Especifica el archivo que contiene las definiciones del conjunto de reglas para el catálogo de imágenes.

Consulte también [RuleSetFile](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) en la Guía de referencia de visores de Dynamic Media.

#### Ficha Atributos de solicitud {#request-attributes-tab}

Estos ajustes pertenecen al aspecto predeterminado de las imágenes.

| Configuración | Descripción |
| --- | --- |
| **[!UICONTROL Límite de tamaño de la imagen de respuesta]** | Requerido.<br>Especifica el ancho y el alto máximo de la imagen de respuesta que se devuelve al cliente. El servidor devuelve un error si una solicitud produce una imagen de respuesta cuya anchura, altura o ambas dimensiones sean superiores a esta configuración.<br>Consulte también [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Modo de ofuscación de solicitud]** | Habilitar si desea aplicar codificación base64 a solicitudes válidas.<br>Consulte también [RequestObfuscation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Modo de bloqueo de solicitud]** | Habilitar si desea un simple bloqueo hash incluido en las solicitudes.<br>Consulte también [RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Atributos de solicitud predeterminados]** |  |
| **[!UICONTROL Sufijo de archivo de imagen predeterminado]** | Requerido.<br>Extensión de archivo de datos predeterminada que se anexa a los valores de campo Ruta del catálogo y RutaDeMáscara si la ruta no incluye un sufijo de archivo.<br>Consulte también [DefaultExt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Nombre de fuente predeterminada]** | Especifica qué fuente se utiliza si una solicitud de capa de texto no proporciona ninguna fuente. Si se especifica, debe ser un valor de nombre de fuente válido en el mapa de fuentes de este catálogo de imágenes o en el mapa de fuentes del catálogo predeterminado.<br>Consulte también [DefaultFont](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Imagen predeterminada]** | Proporciona una imagen predeterminada para devolver en respuesta a una solicitud en la que no se encuentra la imagen solicitada.<br>Consulte también [DefaultImage](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Modo de imagen predeterminado]** | Cuando el cuadro deslizante está activado (control deslizante a la derecha), la variable **[!UICONTROL Imagen predeterminada]** reemplaza cada capa que falta en la imagen de origen por la imagen predeterminada y devuelve el compuesto como de costumbre. Cuando el cuadro deslizante está desactivado (deslizador a la izquierda), la imagen predeterminada reemplaza a la imagen compuesta completa, aunque la imagen que falta sea una de varias capas.<br>Consulte también [DefaultImageMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Tamaño de vista predeterminado]** | Requerido.<br>El servidor restringe el tamaño de las imágenes de respuesta para que no supere esta anchura y altura si la solicitud no especifica el tamaño de vista de forma explícita mediante `wid=`, `hei=`o `scl=`.<br>Consulte también [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Tamaño de miniatura predeterminado]** | Requerido.<br>Se utiliza en lugar del atributo **[!UICONTROL Tamaño de vista predeterminado]** para solicitudes de miniaturas (`req=tmb`). El servidor restringe el tamaño de las imágenes de respuesta para que no superen esta anchura y altura, si se solicita una miniatura (`req=tmb`) no especifica el tamaño utilizando `wid=`, `hei=`o `scl=`.<br>Consulte también [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Color de fondo predeterminado]** | Especifica el valor del RGB utilizado para rellenar cualquier área de una imagen de respuesta que no contenga datos de imagen reales.<br>Consulte también [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Atributos de codificación JPEG]** |  |
| **[!UICONTROL Calidad]** | Especifica los atributos predeterminados para las imágenes de respuesta del JPEG. La variable **[!UICONTROL Calidad]** se define en el rango de 1 a 100.<br>Consulte también [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Disminución de resolución de cromaticidad]** | Activar o desactivar el muestreo descendente cromático empleado por los codificadores JPEG. |
| **[!UICONTROL Modo de remuestreo predeterminado]** | Especifica los atributos de remuestreo e interpolación predeterminados que se utilizarán para escalar datos de imagen. Usar cuando `resMode` no se ha especificado en una solicitud.<br>Consulte también [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) en la Guía de referencia de visores de Dynamic Media. |

#### Ficha Atributos de miniatura comunes {#common-thumbnail-attributes-tab}

Estos ajustes pertenecen al aspecto y la alineación predeterminados de las imágenes en miniatura.

| Configuración | Descripción |
| --- | --- |
| **[!UICONTROL Color de fondo predeterminado para miniatura]** | Especifica el valor del RGB utilizado para rellenar el área de una imagen en miniatura de salida que no contiene datos de imagen reales. Solo se usa para solicitudes de miniaturas (`req=tmb`) y cuándo **[!UICONTROL Tipo de miniatura predeterminado]** está configurada en **[!UICONTROL Ajustar]** o **[!UICONTROL Textura]**.<br>Consulte también [ThumbBkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Alineación horizontal]** | Especifica la alineación horizontal de la imagen en miniatura en el rectángulo de imagen de respuesta especificado por `wid=` y `hei=` valores.<br>Solo se usa para solicitudes de miniaturas (`req=tmb`) y cuándo **[!UICONTROL Tipo de miniatura predeterminado]** está configurada en **[!UICONTROL Ajustar]**.<br>Hay tres alineaciones horizontales entre las que elegir: **[!UICONTROL Alineación central]**, **[!UICONTROL Alineación izquierda]** y **[!UICONTROL Alineación derecha]**.<br>Consulte también [ThumbHorizAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Alineación vertical]** | Especifica la alineación vertical de la imagen en miniatura en el rectángulo de imagen de respuesta especificado por `wid=` y `hei=` valores. Solo se usa para solicitudes de miniaturas (`req=tmb`) y cuándo **[!UICONTROL Tipo de miniatura predeterminado]** está configurada en **[!UICONTROL Ajustar]**.<br>Hay tres alineaciones verticales para elegir: **[!UICONTROL Alineación superior]**, **[!UICONTROL Alineación central]** y **[!UICONTROL Alineación inferior]**.<br>Consulte también [ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Duración predeterminada de la caché]** | Proporciona un intervalo de caducidad predeterminado en horas en caso de que un registro de catálogo en particular no contenga un valor de caducidad de catálogo válido. Establecer como `-1` para marcar como nunca caduca. <br>Consulte también [Caducidad](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Tipo de miniatura predeterminado]** | Proporciona un valor predeterminado para el tipo de miniatura en caso de que un registro de catálogo en particular no contenga un valor de catálogo ThumbType válido. Solo se usa para solicitudes de miniaturas (`req=tmb`).<br>Hay tres tipos de miniaturas entre los que elegir: **[!UICONTROL Recortar]**, **[!UICONTROL Ajustar]** y **[!UICONTROL Textura]**.<br>Consulte también [ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Resolución de miniatura predeterminada]** | Proporciona un valor predeterminado para la resolución del objeto de miniatura en caso de que un registro de catálogo concreto no contenga un valor de catálogo ThumbRes válido. Solo se usa para solicitudes de miniaturas (`req=tmb`) y cuando la variable **[!UICONTROL Tipo de miniatura predeterminado]** está configurada en **[!UICONTROL Textura]**.<br>Consulte también [ThumbRes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) en la Guía de referencia de visores de Dynamic Media. |

#### Ficha Atributos de administración de color {#color-management-attributes-tab}

Estos ajustes determinan qué perfiles de color ICC se utilizan para las imágenes.

**Interpretación de la conversión de color**
Una interpretación de conversión de color permite anular la interpretación predeterminada de los perfiles de trabajo para determinar cómo se ajustan los colores de origen. Se usa cuando:

1. Uno de los perfiles ICC predeterminados es el espacio de color de destino de una conversión de color.
1. Un dispositivo de salida (impresora o monitor) se caracteriza por este perfil.
1. Además, la interpretación especificada es válida para este perfil.

Las distintas intenciones de renderización utilizan reglas diferentes para determinar cómo se ajustan los colores de origen.

Por ejemplo, puede configurar la variable **[!UICONTROL Espacio de color predeterminado del RGB]** a **[!UICONTROL sRGB]** y **[!UICONTROL Espacio de color predeterminado CMYK]** a **[!UICONTROL WebCoated]**.

Al hacerlo, se haría lo siguiente:

* Habilita la corrección de color para imágenes RGB y CMYK.
* Se supone que las imágenes de RGB que no tienen un perfil de color están en la variable *sRGB* espacio de color.
* Se supone que las imágenes CMYK que no tienen un perfil de color están en *WebCoated* espacio de color.
* Representaciones dinámicas que devuelven la salida del RGB, las devuelven en la variable *sRGB* espacio de color.
* Representaciones dinámicas que devuelven la salida CMYK y la devuelven en la variable *WebCoated* espacio de color.

Consulte también [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) en la Guía de referencia de visores de Dynamic Media.

>[!NOTE]
En general, es mejor utilizar la interpretación predeterminada para la configuración de color seleccionada, que ha sido probada por Adobe para cumplir los estándares del sector. Por ejemplo, si elige una configuración de color para Norteamérica o Europa, la interpretación de conversión de color predeterminada es **[!UICONTROL Colormétrica relativa]**. Si elige una configuración de color para Japón, la interpretación de conversión de color predeterminada es **[!UICONTROL Percepción]**.

| Configuración | Características |
| --- | --- |
| **[!UICONTROL Espacio de color predeterminado CMYK]** | Especifica el nombre del perfil de color ICC que se utilizará como perfil de trabajo para los datos CMYK. If **[!UICONTROL Ninguno especificado]** se elige, la gestión de color se desactiva para este catálogo de imágenes cuando están involucradas las imágenes de origen CMYK. Todos los espacios de trabajo CMYK dependen del dispositivo, lo que significa que se basan en combinaciones reales de tinta y papel. Los materiales de Adobe para espacios de trabajo CMYK se basan en condiciones estándar de impresión comercial.<br> Consulte también [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Espacio de color predeterminado de escala de grises]** | Especifica el nombre del perfil de color ICC que se utilizará como perfil de trabajo para los datos de escala de grises. If **[!UICONTROL Ninguno especificado]** se elige, la gestión de color se desactiva para este catálogo de imágenes cuando están implicadas imágenes de origen en escala de grises.<br>Consulte también [IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Espacio de color predeterminado del RGB]** | Especifica el nombre del perfil de color ICC que se utilizará como perfil de trabajo para los datos del RGB. If **[!UICONTROL Ninguno especificado]** se elige, la gestión de color se desactiva para este catálogo de imágenes cuando están involucradas las imágenes de fuentes RGB. En general, es mejor elegir **[!UICONTROL Adobe RGB]** o **[!UICONTROL sRGB]**, en lugar del perfil de un dispositivo específico (como un perfil de monitor). **[!UICONTROL sRGB]** se recomienda cuando prepare imágenes para la web o dispositivos móviles, ya que define el espacio de color del monitor estándar utilizado para ver imágenes en la web. **[!UICONTROL sRGB]** también es una buena opción cuando se trabaja con imágenes de cámaras digitales de consumo, ya que la mayoría de estas cámaras utilizan sRGB como espacio de color predeterminado.<br>Consulte también [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Interpretación de la conversión de color]** | **[!UICONTROL Percepción]** - Su objetivo es preservar la relación visual entre los colores para que se perciba como natural para el ojo humano, aunque los valores de color en sí mismos puedan cambiar. Esta intención es adecuada para imágenes fotográficas con muchos colores fuera de gama. Este ajuste es la interpretación estándar para la industria de impresión japonesa. |
|  | **[!UICONTROL Colorimétrico relativo]** - Compara el resaltado extremo del espacio de color de origen con el del espacio de color de destino y cambia todos los colores según corresponda. Los colores fuera de gama se desplazan al color reproducible más cercano en el espacio de color de destino. Colorimétrico relativo conserva más de los colores originales en una imagen que Perceptual. Este ajuste es la interpretación estándar para impresión en Norteamérica y Europa. |
|  | **[!UICONTROL Saturación]** - Trata de producir colores vivos en una imagen a expensas de la precisión del color. Esta interpretación es adecuada para gráficos empresariales, como gráficos o gráficos, en los que los colores saturados brillantes son más importantes que la relación exacta entre los colores. |
|  | **[!UICONTROL Colorimétrico absoluto]** - Deja sin cambios los colores que entran dentro de la gama de destino. Los colores fuera de gama se recortan. No se aplica ninguna escala de colores a los puntos blancos de destino. Esta intención es mantener la precisión del color a expensas de preservar las relaciones entre los colores y es adecuada para pruebas para simular la salida de un dispositivo en particular. Esta intención es útil para previsualizar cómo el color del papel afecta a los colores impresos. |

### Probar recursos antes de hacerlos públicos {#test-assets-before-making-public}

Secure Testing le ayuda a definir un entorno de prueba seguro y a crear una solución empresarial a empresa sólida, basada en un conjunto configurable de direcciones IP e intervalos. Esta funcionalidad le permite hacer coincidir las implementaciones de Dynamic Media de Adobe con la arquitectura de su sistema empresarial y de administración de contenido.

Con Secure Testing, puede obtener una vista previa de la versión de ensayo del sitio web con contenido no publicado.

Si lo desea, cree un entorno de ensayo en lugar de publicar los recursos por los siguientes motivos:

* Previsualizar sitios web antes del lanzamiento público (sitio web de ensayo).
* Proporcione recursos que requieran acceso restringido, como catálogos electrónicos que muestren precios en una aplicación web B2B.
* Utilice los recursos detrás de un cortafuegos como parte del sistema de administración de la información del producto, la aplicación de servicio al cliente, el sitio de formación, etc.

>[!NOTE]
Secure Testing no afecta al acceso a Adobe Dynamic Media Classic. La seguridad de Adobe Dynamic Media Classic sigue siendo coherente y requiere las credenciales habituales para acceder a Adobe Dynamic Media Classic y a los servicios web relacionados.

#### Funcionamiento de Secure Testing {#how-test-assets-works}

La mayoría de las corporaciones ejecutan Internet detrás de un cortafuegos. El acceso a Internet es posible a través de ciertas rutas y, por lo general, a través de una gama limitada de direcciones IP públicas.

Desde su red corporativa, puede averiguar su dirección IP pública utilizando sitios web como [https://www.whatismyip.com](https://www.whatismyip.com/) o solicite esta información a su organización de TI corporativa.

Con Secure Testing, Adobe Dynamic Media crea un servidor de imágenes dedicado para entornos de ensayo o aplicaciones internas. Cualquier solicitud a este servidor comprueba la dirección IP de origen. Si la solicitud entrante no está dentro de la lista aprobada de direcciones IP, se devuelve una respuesta de error. El administrador de la empresa de Dynamic Media de Adobe configura la lista aprobada de direcciones IP para el entorno Secure Testing de su empresa.

Como se debe confirmar la ubicación de la solicitud original, el tráfico del servicio Secure Testing no se enruta a través de una red de distribución de contenido como el tráfico público del servidor de imágenes de Dynamic Media. Las solicitudes al servicio Secure Testing tienen una latencia ligeramente mayor que los servidores públicos de imágenes de Dynamic Media.

Los recursos no publicados están disponibles inmediatamente desde los servicios Secure Testing, sin necesidad de publicarlos. De este modo, puede ejecutar una vista previa antes de publicar los recursos en su servidor de imágenes público.

>[!NOTE]
Los servicios de Secure Testing utilizan el servidor de catálogo configurado con un contexto de publicación interno. Por lo tanto, si su empresa está configurada para publicar en Secure Testing, cualquier recurso cargado en Adobe Dynamic Media estará disponible inmediatamente en los servicios de Secure Testing. Esta funcionalidad es verdadera independientemente de si los recursos están marcados para publicarse en la carga.

Los servicios de Secure Testing admiten actualmente los siguientes tipos de activos y funcionalidades:

* Imágenes.
* Viñetas (Procesar solicitudes del servidor).
* Procesar solicitudes de servidor (admitidas, pero el cliente debe solicitarlas explícitamente).
* Conjuntos, incluidos conjuntos de imágenes, catálogos electrónicos, conjuntos de representación y conjuntos de medios.
* Visores de medios enriquecidos de Dynamic Media de Adobe estándar.
* Adobe de páginas JSP de Dynamic Media OnDemand.
* Contenido estático, como archivos PDF y vídeos servidos de forma progresiva.
* Flujo continuo de vídeo HTTP.
* Flujo continuo de vídeo progresivo.

Actualmente no se admiten los siguientes tipos de recursos y funcionalidades:

* Búsqueda de información o catálogo electrónico de Adobe Dynamic Media Classic
* Flujo de vídeo RTMP
* Impresión virtual
* Servicios UGC (contenido generado por el usuario)

>[!IMPORTANT]
La compatibilidad con recursos de imagen vectoriales UGC nuevos o existentes en Adobe Dynamic Media finalizó el 30 de septiembre de 2021.

#### Probar el servicio Secure Testing {#test-secure-testing-service}

Para asegurarse de que el servicio Secure Testing funciona según lo esperado, haga lo siguiente:

##### Preparar su cuenta

1. Póngase en contacto con el Servicio de atención al cliente de Adobe y solicite que habiliten Secure Testing en su cuenta.
1. En Adobe Experience Manager, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Configuración de Dynamic Media Publish]**.
1. En la página Servidor de imágenes , en la sección **[!UICONTROL Publicar contexto]** lista desplegable, seleccione **[!UICONTROL Probar servicio de imágenes]**.
1. Seleccione el **[!UICONTROL Seguridad]** pestaña .
1. Para la variable **[!UICONTROL Dirección del cliente]** filtrar, seleccionar **[!UICONTROL Agregar]**.
1. En el **[!UICONTROL Dirección IP]** , escriba una dirección IP.
1. En el **[!UICONTROL Máscara]** , escriba una máscara de red.

   >[!NOTE]
   Si agrega más de una dirección IP y una máscara de red, se permite *all* Direcciones IP para realizar llamadas de recursos y todas se muestran.

1. Realice una de las acciones siguientes:

   * Para agregar más direcciones IP, repita los tres pasos anteriores.
   * Continúe con el paso siguiente.

1. En la esquina superior derecha de la página Servidor de imágenes , seleccione **[!UICONTROL Guardar]**.
1. Cargue las imágenes que desee en su cuenta de Dynamic Media de Adobe.

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. Asegúrese de que algunas imágenes estén marcadas para publicación y otras no estén marcadas y, a continuación, envíe el trabajo de publicación.

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. Determine el nombre de su servicio Secure Testing. Para ello, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Configuración general de Dynamic Media]**.
1. En el **[!UICONTROL Servidor]** , busque el nombre del servidor a la derecha de **[!UICONTROL Nombre del servidor publicado]**.

Póngase en contacto con el servicio de atención al Adobe si falta el nombre del servidor o si la URL del servidor no funciona.

##### Preparación de las variaciones del sitio web

Necesita dos variaciones de un sitio web que vincule los recursos publicados y no publicados:

* Versión pública : vincule recursos con su sintaxis de URL tradicional de Dynamic Media de Adobe.
* Versión de ensayo : vincule los recursos con la misma sintaxis pero con el nombre del sitio Secure Testing.

##### Ejecute las pruebas

Realice las siguientes pruebas:

1. Compruebe si los recursos son visibles desde la red corporativa.

   Desde la red corporativa identificada por el intervalo de direcciones IP definido anteriormente, la versión de ensayo del sitio web muestra todas las imágenes, estén o no marcadas para publicación. De este modo, puede realizar pruebas sin tener que poner las imágenes a disposición por error antes de la aprobación de la vista previa o el inicio del producto.

   Confirme que la versión pública del sitio muestra los recursos publicados tal y como se experimentaron anteriormente con Adobe Dynamic Media.

1. Desde fuera de la red corporativa, compruebe que los activos no publicados (es decir, sin marcar para publicación) estén protegidos contra el acceso de terceros.

   Acceda a su red desde el exterior (por ejemplo, desde su equipo doméstico o a través de una conexión 4G/5G) y, a continuación, verifique que la versión pública del sitio muestre todos los recursos publicados, excepto ninguno del contenido no publicado.

   Confirme que la versión de ensayo no muestra ningún recurso porque está accediendo al servicio Secure Testing desde una dirección IP no aprobada.

### Configuración general de Dynamic Media {#configuring-application-general-settings}

>[!IMPORTANT]
La configuración general de Dynamic Media solo está disponible si:
* Está ejecutando Dynamic Media en modo Scene7.
* Tiene un *existente* **[!UICONTROL Configuración de Dynamic Media]** (en **[!UICONTROL Cloud Services]**) en Adobe Experience Manager 6.5 o en Experience Manager as a Cloud Service.
* Es administrador del sistema del Experience Manager con privilegios de administrador.


Al crear la cuenta, Adobe Dynamic Media proporciona automáticamente los servidores asignados a su empresa. Estos servidores se utilizan para construir cadenas de URL para el sitio web y las aplicaciones. Estas llamadas a URL son específicas de su cuenta.

Consulte también [Probar el servicio Secure Testing](/help/assets/dm-publish-settings.md#test-assets-before-making-public).

**Para configurar la configuración general de Dynamic Media:**

1. En el modo Autor del Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global.
1. En el carril izquierdo, seleccione el icono Herramientas y, a continuación, vaya a **[!UICONTROL Recursos]** > **[!UICONTROL Configuración general de Dynamic Media]**.
1. En la página Servidor , configure **[!UICONTROL Nombre del servidor publicado]** y **[!UICONTROL Nombre del servidor de origen]** y, a continuación, utilice las cinco pestañas para configurar las opciones de publicación predeterminadas.

   * [Servidor](#server-general-setting)
   * [Cargar a la aplicación](#upload-to-application)
   * [Edición de imágenes](#image-editing-tab) ficha
   * [PostScript](#postscript-tab) ficha
   * [Photoshop](#photoshop-tab) ficha
   * [PDF](#pdf-tab) ficha
   * [Illustrator](#illustrator-tab) ficha

   ![Página Configuración general de Dynamic Media](/help/assets/assets-dm/dm-general-settings.png)
   *Configuración general de Dynamic Media , con la variable **[!UICONTROL Edición de imágenes]**seleccionada.*<br><br>

1. Cuando haya terminado, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]**.

#### Servidor {#server-general-setting}

Al crear la cuenta, Adobe Dynamic Media proporciona automáticamente los servidores asignados a su empresa. Estos servidores se utilizan para construir cadenas de URL para el sitio web y las aplicaciones. Estas llamadas a URL son específicas de su cuenta.

| Opción | Descripción |
| --- | --- |
| **[!UICONTROL Servidor de publicación]** | Requerido.<br>Este servidor es el servidor CDN (red de entrega de contenido) activo que se utiliza en todas las llamadas URL generadas por el sistema que son específicas de su cuenta. No cambie este nombre de servidor a menos que se le indique que lo haga por Adobe Technical Support. El nombre debe utilizar `https://` en la ruta. |
| **[!UICONTROL Servidor de origen]** | Requerido.<br>Este servidor solo se utiliza para pruebas de control de calidad. No cambie este nombre de servidor a menos que se le indique que lo haga el servicio de asistencia técnica de Adobe. |

#### Cargar a la aplicación {#upload-to-application}

* **[!UICONTROL Sobrescribir imágenes]**

   Adobe Dynamic Media no permite que dos archivos tengan el mismo nombre. El ID de Dynamic Media de Adobe de cada elemento (el nombre de imagen menos la extensión de nombre de archivo) debe ser único. Debido a esta regla, **[!UICONTROL Cargar a la aplicación]** tiene sobrescritura. El efecto exacto de esta opción depende de la opción Sobrescribir imágenes que haya elegido. Estas opciones especifican cómo se cargan las imágenes de reemplazo: si reemplazan las imágenes originales o se convierten en imágenes duplicadas. Se cambia el nombre de las imágenes duplicadas por una `-1`. Por ejemplo, `chair.tif` se cambia el nombre `chair-1.tif`. Estas opciones afectan a las imágenes cargadas en una carpeta diferente a la original o a las imágenes con una extensión de nombre de archivo diferente a la original, como JPG, TIF o PNG.

   | Opción Sobrescribir imágenes | Descripción |
   | --- | --- |
   | **[!UICONTROL Sobrescribir en la carpeta actual, mismo nombre/extensión de base]** | Predeterminado.<br>Esta opción es la regla más estricta para la sustitución. Requiere que cargue la imagen de reemplazo en la misma carpeta que la original y que la imagen de reemplazo tenga la misma extensión de nombre de archivo que la original. Si no se cumplen estos requisitos, se crea un duplicado. |
   | **[!UICONTROL Sobrescribir en la carpeta actual, mismo nombre de base independientemente de la extensión]** | Requiere que cargue la imagen de reemplazo en la misma carpeta que el original, aunque la extensión del nombre de archivo puede ser diferente de la original. Por ejemplo, chair.tif reemplaza a chair.jpg. |
   | **[!UICONTROL Sobrescribir en cualquier carpeta con mismo nombre y ext. de recurso base]** | Requiere que la imagen de reemplazo tenga la misma extensión de nombre de archivo que la imagen original (por ejemplo, chair.jpg debe reemplazar a chair.jpg, no chair.tif). Sin embargo, puede cargar la imagen de reemplazo en una carpeta diferente a la original. La imagen actualizada reside en la nueva carpeta; el archivo ya no se puede encontrar en su ubicación original. |
   | **[!UICONTROL Sobrescribir en cualquier carpeta, mismo nombre de base independientemente de la extensión]** | Esta opción es la regla de reemplazo más inclusiva. Puede cargar una imagen de reemplazo en una carpeta distinta a la original, cargar un archivo con una extensión de nombre de archivo diferente y reemplazar el archivo original. Si el archivo original se encuentra en una carpeta diferente, la imagen de reemplazo reside en la nueva carpeta a la que se cargó. |

* **[!UICONTROL Conservar recorte]**

   Controla la preservación de cualquier definición de recorte manual existente.

   Consulte también `preserveCrop` en [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) y [ReprocessAssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html), ambas en la Guía de referencia de visores de Dynamic Media.

#### Opciones de carga predeterminadas {#default-upload-options}

##### Ficha Edición de imágenes {#image-editing-tab}

Este filtro permite ajustar un efecto de filtro de enfoque en la imagen final con disminución de resolución. Ayuda a controlar la intensidad del efecto, el radio del efecto (medido en píxeles) y un umbral de contraste que se ignora.

El efecto Máscara de enfoque utiliza las mismas opciones que el filtro Máscara de enfoque de Photoshop. Contrariamente a lo que sugiere el nombre, Máscara de enfoque es un filtro de enfoque.

| Opciones de máscara de enfoque | Descripción |
| --- | --- |
| **[!UICONTROL Cantidad]** | Requerido.<br>Controla la cantidad de contraste que se aplica a los píxeles de borde.<br>Piensen en ello como la intensidad del efecto. La principal diferencia entre los valores de cantidad de Máscara de enfoque en Adobe Dynamic Media y los valores de cantidad en Adobe Photoshop es que Photoshop tiene un rango de cantidad del 1% al 500%. Mientras que en Adobe Dynamic Media, el intervalo de valores es `0.0` a `5.0`. Un valor de 5,0 en Adobe Dynamic Media es el equivalente aproximado del 500 % en Photoshop; un valor de 0,9 es el equivalente a 90 %, etc. |
| **[!UICONTROL Radio]** | Requerido.<br>Controla el radio del efecto.<br>El intervalo de valores es `0` a `250`. El efecto se ejecuta en todos los píxeles de una imagen y se irradia desde todos los píxeles en todas las direcciones. El radio se mide en píxeles. Por ejemplo, para obtener un efecto de nitidez similar para una imagen de 2000 x 2000 píxeles y una imagen de 500 x 500 píxeles, establecería un radio de dos píxeles en la imagen de 2000 x 2000 píxeles. Luego establezca un valor de radio de un píxel en la imagen de 500 x 500 píxeles. Se utiliza un valor mayor para una imagen que tiene más píxeles. |
| **[!UICONTROL Umbral]** | Requerido.<br>El umbral es un intervalo de contraste que se ignora cuando se aplica el filtro Máscara de enfoque. Este efecto es importante para que no se introduzca ningún &quot;ruido&quot; en una imagen cuando se utilice este filtro. El intervalo de valores es `0` - `255`, que es el número de pasos de brillo de una imagen en escala de grises. `0`=negro, `128`=50% gris y `255`=blanco.<br>Un valor de umbral de `12` ignora las ligeras variaciones en el brillo del tono de la piel para evitar agregar ruido, pero agrega contraste al borde de áreas contrastadas como donde las pestañas tocan la piel.<br>Si tienes una foto de la cara de alguien, la máscara de enfoque afecta a las partes contrastadas de la imagen. Por ejemplo, donde las pestañas y la piel se encuentran para crear un área obvia de contraste, y la piel suave en sí. Incluso la piel más suave presenta cambios sutiles en los valores de brillo. Si no utiliza un valor de umbral, el filtro acentúa estos cambios sutiles en los píxeles de la piel. A su vez, se crea una reacción ruidosa e indeseable mientras que aumenta el contraste en las pestañas, mejorando la nitidez.<br>Para evitar este problema, se introduce un valor de umbral que indica al filtro que ignore los píxeles que no cambian el contraste de forma drástica, como la piel suave.<br>En el gráfico de cierre mostrado anteriormente, observe la textura junto a los tapones. El ruido de la imagen se muestra porque los valores de umbral eran demasiado bajos para suprimir el ruido. |
| **[!UICONTROL Monocromo]** | Seleccione para aplicar máscara de enfoque al brillo (intensidad) de la imagen.<br>Anule la selección para desenmascarar cada componente de color por separado. |

Consulte también [Enfoque de imágenes en Adobe Dynamic Media y en Image Server](/help/assets/assets/sharpening_images.pdf).

##### Ficha PostScript {#postscript-tab}

Puede rasterizar archivos Adobe PostScript®, mantener fondos transparentes, elegir una resolución y elegir un espacio de color.

Puede utilizar archivos Adobe PostScript® (EPS) en Adobe Dynamic Media. Adobe Dynamic Media ofrece comandos para configurar estos archivos a medida que los carga.

Al cargar archivos de imagen PostScript (EPS), puede aplicarles formato de varias formas. Puede rasterizar los archivos, mantener el fondo transparente, elegir una resolución y elegir un espacio de color.

| Opción PostScript | Descripción |
| --- | --- |
| **[!UICONTROL Procesando]** | Seleccione Rasterizar para convertir los gráficos vectoriales del archivo al formato de mapa de bits. |
| **[!UICONTROL Mantener el fondo transparente en las imágenes procesadas]** | Conserva la transparencia en segundo plano del archivo. |
| **[!UICONTROL Resolución (píxel/pulgada)]** | Determina la configuración de resolución. Esta configuración determina cuántos píxeles se muestran por pulgada en el archivo. |
| **[!UICONTROL Espacio de color]** | ・ **[!UICONTROL Detectar automáticamente]** - Conserva el espacio de color del archivo.<br>・ **[!UICONTROL Forzar como RGB]** - Convierte al espacio de color del RGB.<br>・ **[!UICONTROL Forzar como CMYK]** - Convierte al espacio de color CMYK.<br>・ **[!UICONTROL Forzar como escala de grises]** - Convierte al espacio de color Escala de grises . |

##### Ficha Photoshop {#photoshop-tab}

Puede crear plantillas a partir de archivos Photoshop® de Adobe®, mantener las capas, especificar el nombre de las capas, extraer texto y especificar cómo se anclan las imágenes en las plantillas.

| Opción Photoshop | Descripción |
| --- | --- |
| **[!UICONTROL Mantener capas]** | Extrae las capas del PSD, si las hay, en recursos individuales. Las capas de recursos permanecen asociadas al PSD. Para verlas, abra el archivo PSD en la Vista de detalles y seleccione el panel de capas. Consulte Visualización y edición de capas en un archivo de PSD. |
| **[!UICONTROL Crear plantilla]** | Crea una plantilla a partir de las capas del archivo PSD. |
| **[!UICONTROL Extraer texto]** | Extrae el texto para que los usuarios puedan buscar texto en un visualizador. |
| **[!UICONTROL Extender las capas al tamaño del fondo]** | Amplía el tamaño de las capas de imagen recortadas al tamaño de la capa de fondo. |
| **[!UICONTROL Nombres de capas]** | Amplía el tamaño de las capas de imagen recortadas al tamaño de la capa de fondo.<br>・ **[!UICONTROL Nombre de la capa]** - Nombra las imágenes después de sus nombres de capa en el archivo PSD. Por ejemplo, una capa denominada Etiqueta de precio en el archivo PSD original se convierte en una imagen denominada Etiqueta de precio. Sin embargo, si los nombres de capa del archivo PSD son nombres de capa predeterminados de Photoshop (Fondo, Capa 1, Capa 2, etc.), las imágenes reciben el nombre de sus números de capa en el archivo PSD. <br>・ **[!UICONTROL Photoshop y número de capa]** - Nombra las imágenes después de sus números de capa en el archivo PSD, ignorando los nombres de capa originales. Las imágenes reciben el nombre del archivo Photoshop y un número de capa anexado. Por ejemplo, la segunda capa de un archivo llamado `Spring Ad.psd` se llama `Spring Ad_2` incluso si tenía un nombre no predeterminado en Photoshop.<br>・ **[!UICONTROL Photoshop y nombre de capa]** - Nombra las imágenes después del archivo de PSD seguido del nombre o número de capa. El número de capa se utiliza si los nombres de capa del archivo PSD son nombres de capa predeterminados de Photoshop. Por ejemplo, una capa denominada `Price Tag` en un archivo PSD denominado `SpringAd` se llama `Spring Ad_Price Tag`. Una capa con el nombre predeterminado Capa 2 se llama `Spring Ad_2`. |
| **[!UICONTROL Ancla]** | Especifique cómo se anclan las imágenes en plantillas generadas a partir de la composición en capas producida a partir del archivo PSD. De forma predeterminada, el anclaje es el centro. Un anclaje central permite que las imágenes de reemplazo ocupen el mismo espacio, independientemente de la proporción de aspecto de la imagen de reemplazo. Las imágenes con un aspecto diferente que reemplazan a esta imagen, al hacer referencia a la plantilla y utilizar la sustitución de parámetros, ocupan efectivamente el mismo espacio. Cambie a una configuración diferente si la aplicación requiere que las imágenes de reemplazo rellenen el espacio asignado en la plantilla. |

##### ficha PDF {#pdf-tab}

Puede elegir rasterizar los archivos, extraer palabras de búsqueda y vínculos, definir la resolución y elegir un espacio de color.

| opción PDF | Descripción |
| --- | --- |
| **[!UICONTROL Procesando]** | ・ **[!UICONTROL Ninguna]** - No se procesa el PDF.<br>・ **[!UICONTROL Miniatura]** - Extrae cada página del archivo PDF y la convierte en una imagen en miniatura.<br> ・ **[!UICONTROL Rasterizar]** : quita las páginas del archivo PDF y convierte los gráficos vectoriales en imágenes de mapa de bits. Para crear un catálogo electrónico, seleccione esta opción. |
| **[!UICONTROL Extraer]** | ・ **[!UICONTROL Ninguna]** - No se extraen palabras de búsqueda ni vínculos del PDF.<br>・ **[!UICONTROL Palabras de búsqueda]** - Extrae palabras de búsqueda del archivo PDF para que el archivo se pueda buscar por palabra clave en un visor de catálogos electrónicos.<br>・ **[!UICONTROL Vínculos]** - Extrae enlaces de los archivos PDF y los convierte en mapas de imágenes que se usan en un visor de catálogos electrónicos.<br>・ **[!UICONTROL Buscar palabras y vínculos]** - Extrae palabras de búsqueda y vínculos para usarlos en un visor de catálogos electrónicos. |
| **[!UICONTROL Resolución (píxel/pulgada)]** | Determina la configuración de resolución. Esta configuración determina cuántos píxeles se muestran por pulgada en el archivo PDF. El valor predeterminado es 150. |
| **[!UICONTROL Espacio de color]** | ・ **[!UICONTROL Detectar automáticamente]** : mantiene el espacio de color del archivo PDF.<br>・ **[!UICONTROL Forzar como RGB]** - Convierte al espacio de color del RGB.<br>・ **[!UICONTROL Forzar como CMYK]** - Convierte al espacio de color CMYK.<br>・ **[!UICONTROL Forzar como escala de grises]** - Convierte al espacio de color Escala de grises . |

##### Ficha Illustrator {#illustrator-tab}

Puede rasterizar archivos Adobe Illustrator®, mantener fondos transparentes, elegir una resolución y elegir un espacio de color.

Puede utilizar archivos Adobe® Illustrator® (AI) en Adobe Dynamic Media. Adobe Dynamic Media ofrece comandos para configurar estos archivos a medida que los carga.

Al cargar archivos de imagen de Illustrator (AI), puede aplicarles formato de varias formas. Puede rasterizar los archivos, mantener el fondo transparente, elegir una resolución y elegir un espacio de color. Las opciones para dar formato a archivos PostScript y Illustrator están disponibles en la pantalla Cargar, en Opciones de PostScript y Opciones de Illustrator, en el cuadro Opciones de carga de trabajo .


| Opción Illustrator | Descripción |
| --- | --- |
| **[!UICONTROL Procesando]** | Seleccione Rasterizar para convertir los gráficos vectoriales del archivo al formato de mapa de bits. |
| **[!UICONTROL Mantener el fondo transparente en las imágenes procesadas]** | Conserva la transparencia en segundo plano del archivo. |
| **[!UICONTROL Resolución (píxel/pulgada)]** | Determina la configuración de resolución. Esta configuración determina cuántos píxeles se muestran por pulgada en el archivo. |
| **[!UICONTROL Espacio de color]** | ・ **[!UICONTROL Detectar automáticamente]** - Conserva el espacio de color del archivo.<br>・ **[!UICONTROL Forzar como RGB]** - Convierte al espacio de color del RGB.<br>・ **[!UICONTROL Forzar como CMYK]** - Convierte al espacio de color CMYK.<br>・ **[!UICONTROL Forzar como escala de grises]** - Convierte al espacio de color Escala de grises . |


**[!UICONTROL Perfiles de color predeterminados]** - Consulte [Configurar la administración de color](#configuring-color-management) para obtener más información.

>[!NOTE]
De forma predeterminada, el sistema muestra 15 representaciones al seleccionar **[!UICONTROL Representaciones]** y 15 ajustes preestablecidos de visualizador al seleccionar **[!UICONTROL Visualizadores]** en la vista de detalles del recurso. Puede aumentar este límite. Consulte [Aumente el número de ajustes preestablecidos de imagen que se muestran](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) o [Aumente el número de ajustes preestablecidos de visor que se muestran](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

### (Opcional) Tareas de configuración adicionales {#additional-configuration-tasks}

Las tareas opcionales de configuración y configuración incluyen lo siguiente:

* [Editar tipos MIME para formatos admitidos](#editing-mime-types-for-supported-formats) **RIESGO: ¿CONTINÚA?**
* [Añadir tipos MIME para formatos no compatibles](#adding-mime-types-for-unsupported-formats) **RIESGO: ¿CONTINÚA?**
* [Crear ajustes preestablecidos de conjuntos de lotes para generar automáticamente conjuntos de imágenes y conjuntos de giros](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) **RIESGO: ¿CONTINÚA?**

* **[!UICONTROL Atributos de compatibilidad]** - **RIESGO: ¿SIGUE SIENDO NECESARIO? ESTABA EN CLASSIC** Este ajuste permite que los párrafos iniciales y finales de las capas de texto se traten como lo eran en la versión 3.6 para la compatibilidad con versiones anteriores.
* **[!UICONTROL Compatibilidad con localización]** - **RIESGO: ¿SIGUE SIENDO NECESARIO? ESTABA EN CLASSIC** Esta configuración le permite administrar varios atributos de configuración regional. También le permite especificar una cadena de asignación de configuración regional para que pueda definir qué idiomas desea admitir para las distintas informaciones de objeto en Visualizadores. Para obtener más información sobre la configuración **[Compatibilidad con localización]**, consulte [Consideraciones al configurar la localización de recursos](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html#considerations-when-setting-up-localization-of-assets).

#### Editar tipos MIME para formatos admitidos {#editing-mime-types-for-supported-formats}

**RIESGO: ¿MANTÉNGASE ASÍ?**

Puede definir qué tipos de recursos procesa Dynamic Media y personalizar los parámetros avanzados de procesamiento de recursos. Por ejemplo, puede especificar parámetros de procesamiento de recursos para hacer lo siguiente:

* Convierta una Adobe PDF en un recurso de catálogo electrónico.
* Convierta un documento de Adobe Photoshop (.PSD) en un recurso de plantilla de banner para su personalización.
* Rasterizar un archivo Adobe Illustrator (.AI) o un archivo de PostScript® Encapsulado de Adobe Photoshop (.EPS).
* [Perfiles de vídeo](/help/assets/video-profiles.md) y [Perfiles de imagen](/help/assets/image-profiles.md) se puede utilizar para definir el procesamiento de vídeos e imágenes, respectivamente.

Consulte [Carga de recursos](/help/assets/manage-assets.md#uploading-assets).

**Para editar tipos MIME para formatos compatibles:**

1. En el Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. En el carril izquierdo, vaya a lo siguiente:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![Tipos MIME](assets/mimetypes.png)

1. En la carpeta mimeTypes , seleccione un tipo de mime.
1. En el lado derecho de la página CRXDE Lite, en la parte inferior:

   * Haga doble clic en el botón **[!UICONTROL enabled]** campo . De forma predeterminada, todos los tipos de MIME de recursos están habilitados (se establece en **[!UICONTROL true]**), lo que significa que los recursos se sincronizan con Dynamic Media para su procesamiento. Si desea excluir el procesamiento de este tipo de MIME de recurso, cambie esta configuración a **[!UICONTROL false]**.

   * Pulsar dos veces **[!UICONTROL jobParam]** para abrir el campo de texto asociado. Consulte [Tipos Mime Admitidos](/help/assets/assets-formats.md#supported-mime-types) para obtener una lista de los valores de parámetro de procesamiento permitidos, puede utilizar para un tipo mime determinado.

1. Realice una de las acciones siguientes:

   * Repita los pasos del 3 al 4 para editar más tipos MIME.
   * En la barra de menús de la página CRXDE Lite, seleccione **[!UICONTROL Guardar todo]**.

1. En la esquina superior izquierda de la página, seleccione **[!UICONTROL CRXDE Lite]** para volver al Experience Manager.

#### Adición de tipos MIME para formatos no admitidos {#adding-mime-types-for-unsupported-formats}

**RIESGO: ¿MANTÉNGASE ASÍ?**

Puede añadir tipos MIME personalizados para formatos no compatibles en Experience Manager Assets. Asegúrese de que el Experience Manager no elimina ningún nodo nuevo que agregue al CRXDE Lite moviendo el tipo MIME antes de `image_`. Además, asegúrese de que su valor habilitado esté establecido en **[!UICONTROL false]**.

**Para añadir tipos MIME para formatos no compatibles:**

1. En el Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Una nueva pestaña del navegador se abre para **[!UICONTROL Configuración de la consola web de Adobe Experience Manager]** página.

   ![29-08-2019](assets/2019-08-02_16-17-29.png)

1. En la página, desplácese hacia abajo hasta el nombre *Servicio MIME de tipo de recurso de Adobe CQ Scene7* como se muestra en la siguiente captura de pantalla. A la derecha del nombre, seleccione la opción **[!UICONTROL Editar los valores de configuración]** (icono de lápiz).

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. En el **Servicio de tipo MIME de Adobe CQ Scene7 Asset** seleccione cualquier icono de signo más &lt;+>. La ubicación en la tabla donde se selecciona el signo más para añadir el nuevo tipo de mime es trivial.

   ![27-27-02-08-2019](assets/2019-08-02_16-27-27.png)

1. Tipo `DWG=image/vnd.dwg` en el campo de texto vacío que acaba de añadir.

   El ejemplo `DWG=image/vnd.dwg` es solo con fines de demostración. El tipo MIME que agregue aquí puede ser cualquier otro formato no admitido.

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. En la esquina inferior derecha de la página, seleccione **[!UICONTROL Guardar]**.

   En este punto, puede cerrar la ficha del explorador que tiene la página de configuración de la consola web de Adobe Experience Manager abierta.

1. Vuelva a la ficha del explorador que tiene la consola de Experience Manager abierta.
1. En el Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. En el carril izquierdo, vaya a lo siguiente:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Arrastre el tipo mime `image_vnd.dwg` y suéltelo directamente encima `image_` en el árbol como se ve en la siguiente captura de pantalla.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. Con el tipo mime `image_vnd.dwg` aún seleccionado, en la **[!UICONTROL Propiedades]** en la **[!UICONTROL enabled]** dentro de **[!UICONTROL Valor]** , toque dos veces el valor para abrir el **[!UICONTROL Valor]** lista desplegable.
1. Tipo `false` en el campo (o seleccione **[!UICONTROL false]** en la lista desplegable).

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. Cerca de la esquina superior izquierda de la página CRXDE Lite, seleccione **[!UICONTROL Guardar todo]**.

#### Crear ajustes preestablecidos de conjuntos de lotes para generar automáticamente conjuntos de imágenes y conjuntos de giros {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

**RIESGO: ¿MANTÉNGASE ASÍ?**

Utilice los ajustes preestablecidos de conjuntos de lotes para automatizar la creación de conjuntos de imágenes o conjuntos de giros mientras los recursos se cargan en Dynamic Media.

En primer lugar, defina la convención de nomenclatura para ver cómo se agrupan los recursos en un conjunto. A continuación, cree un ajuste preestablecido de conjunto de lotes que sea un conjunto de instrucciones con nombre único e independiente. Debe definir cómo construir el conjunto utilizando imágenes que coincidan con las convenciones de nomenclatura definidas en la fórmula preestablecida.

Al cargar archivos, Dynamic Media crea automáticamente un conjunto con todos los archivos que coinciden con la convención de nombres definida en los ajustes preestablecidos activos.

##### Configurar la asignación de nombres predeterminada

Cree una convención de nombres predeterminada que se utilice en cualquier fórmula preestablecida de conjunto de lotes. Es probable que la convención de nombres predeterminada seleccionada en la definición del ajuste preestablecido de conjunto de lotes sea todo lo que necesita su empresa para generar conjuntos por lotes. Se crea un ajuste preestablecido de conjunto de lotes para utilizar la convención de nombres predeterminada que defina. Puede crear tantos ajustes preestablecidos de conjunto de lotes como desee con convenciones de nomenclatura personalizadas alternativas necesarias para un conjunto de contenido determinado en casos en los que exista una excepción a la nomenclatura predeterminada definida por la empresa.

Aunque no es necesario configurar una convención de nombres predeterminada para utilizar la funcionalidad preestablecida de conjuntos de lotes, se recomienda utilizar la convención de nombres predeterminada. Permite definir tantos elementos de la convención de nombres como desee agrupar en un conjunto para optimizar la creación de conjuntos de lotes.

Como alternativa, puede usar **[!UICONTROL Ver código]** sin campos de formulario disponibles. En esta vista, se crean las definiciones de convención de nombres utilizando expresiones regulares.

Hay dos elementos disponibles para la definición: Coincidencia y Nombre base. Estos campos permiten definir todos los elementos de una convención de nombres e identificar la parte de la convención utilizada para asignar un nombre al conjunto en el que están contenidos. La convención de nombres individual de una empresa suele utilizar una o más líneas de definición para cada uno de estos elementos. Puede utilizar tantas líneas para su definición única y agruparlas en elementos distintos, como Imagen principal, Elemento de color, Elemento de vista alternativa y Elemento de muestra.

**Para configurar la nomenclatura predeterminada:**

**RIESGO: ¿MANTÉNGASE ASÍ?**

1. Abra el [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), luego inicie sesión en su cuenta.

   Adobe proporcionó las credenciales y los detalles de inicio de sesión en el momento del aprovisionamiento. Si no tiene esta información, póngase en contacto con el servicio de atención al cliente de Adobe.

1. En la barra de navegación cerca de la parte superior de la página, vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]** > **[!UICONTROL Nombre predeterminado]**.
1. Seleccione **[!UICONTROL Ver formulario]** o **[!UICONTROL Ver código]** para especificar cómo desea ver e introducir información sobre cada elemento.

   Puede seleccionar el **[!UICONTROL Ver código]** para ver la generación del valor de expresión regular junto con las selecciones de formulario. Puede introducir o modificar estos valores para ayudar a definir los elementos de la convención de nomenclatura, si la vista del formulario lo limita por cualquier motivo. Si los valores no se pueden analizar en la vista de formulario, los campos del formulario se desactivan.

   >[!NOTE]
   Los campos de formulario desactivados no realizan ninguna validación de que las expresiones regulares son correctas. Los resultados de la expresión regular que está creando para cada elemento se muestran después de la línea de resultados. La expresión regular completa se puede ver en la parte inferior de la página.

1. Expanda cada elemento según sea necesario e introduzca las convenciones de nomenclatura que desee utilizar.
1. Si es necesario, realice una de las acciones siguientes:

   * Select **[!UICONTROL Agregar]** para agregar otra convención de nombres para un elemento.
   * Select **[!UICONTROL Eliminar]** para eliminar una convención de nombres para un elemento.

1. Realice una de las acciones siguientes:

   * Select **[!UICONTROL Guardar como]** y escriba un nombre para el ajuste preestablecido.
   * Select **[!UICONTROL Guardar]** si está editando un ajuste preestablecido existente.

##### Crear un ajuste preestablecido de conjunto de lotes

Dynamic Media utiliza ajustes preestablecidos de conjuntos de lotes para organizar los recursos en conjuntos de imágenes (imágenes alternativas, opciones de color y giro de 360) para mostrarlos en los visualizadores. Los ajustes preestablecidos de conjuntos de lotes se ejecutan automáticamente junto con los procesos de carga de recursos en Dynamic Media.

Puede crear, editar y administrar los ajustes preestablecidos de conjuntos de lotes. Existen dos formas de definiciones de ajustes preestablecidos de conjuntos de lotes: una para una convención de nombres predeterminada que puede configurar y otra para convenciones de nombres personalizadas que cree sobre la marcha.

Se puede utilizar el método de campo de formulario para definir un ajuste preestablecido de conjunto de lotes o el método de código, que permite utilizar expresiones regulares. Al igual que en Nombre predeterminado, puede elegir Ver código al mismo tiempo que define en la Vista de formulario y utilizar expresiones regulares para crear las definiciones. Como alternativa, puede desmarcar cualquiera de las vistas para utilizar una o las otras exclusivamente.

**Para crear un ajuste preestablecido de conjunto de lotes:**

**RIESGO: ¿MANTÉNGASE ASÍ?**

1. Abra el [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), luego inicie sesión en su cuenta.

   Adobe proporcionó las credenciales y los detalles de inicio de sesión en el momento del aprovisionamiento. Si no tiene esta información, póngase en contacto con el servicio de atención al cliente de Adobe.

1. En la barra de navegación cerca de la parte superior de la página, vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]** > **[!UICONTROL Ajuste preestablecido de conjunto de lotes]**.

   **[!UICONTROL Ver formulario]**, tal y como se establece en la esquina superior derecha de la página Detalles, es la vista predeterminada.

1. En el panel Lista de ajustes preestablecidos, seleccione **[!UICONTROL Agregar]** para activar los campos de definición en el panel Detalles del lado derecho de la pantalla.
1. En el panel Detalles, en el campo Nombre de ajuste preestablecido , escriba un nombre para el ajuste preestablecido.
1. En el menú desplegable Tipo de conjunto de lotes , seleccione un tipo de ajuste preestablecido.
1. Realice una de las acciones siguientes:

   * Si está utilizando una convención de nombres predeterminada que configuró anteriormente en **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]** > **[!UICONTROL Nombre predeterminado]**, expandir **[!UICONTROL Convenciones de nomenclatura de recursos]** y, a continuación, en la lista desplegable Nombres de archivo , seleccione **[!UICONTROL Predeterminado]**.

   * Para definir una nueva convención de nombres al configurar el ajuste preestablecido, expanda **[!UICONTROL Convenciones de nomenclatura de recursos]** y, a continuación, en la lista desplegable Nombres de archivo , seleccione **[!UICONTROL Personalizado]**.

1. En Orden de secuencia, defina el orden en que se muestran las imágenes después de agrupar el conjunto en Dynamic Media.

   De forma predeterminada, los recursos se ordenan alfanuméricamente. Sin embargo, puede utilizar una lista de expresiones regulares separadas por coma para definir el orden.

1. Para Set Naming and Creation Convention , especifique el sufijo o prefijo del nombre base definido en la Convención de nombres de recursos. Además, defina dónde se creará el conjunto dentro de la estructura de carpetas de Dynamic Media.

   Si define un gran número de conjuntos, mantenga los conjuntos separados de las carpetas que contienen los propios recursos. Por ejemplo, cree una carpeta Conjuntos de imágenes y coloque los conjuntos generados aquí.

1. En el panel Detalles, seleccione **[!UICONTROL Guardar]**.
1. Select **[!UICONTROL Activo]** junto al nuevo nombre del ajuste preestablecido.

   Al activar el ajuste preestablecido, se garantiza que, al cargar recursos en Dynamic Media, el ajuste preestablecido de conjunto de lotes se aplique para generar el conjunto.

##### Crear un ajuste preestablecido de conjunto de lotes para la generación automática de un conjunto de giros 2D

Puede utilizar el tipo de conjunto de lotes **[!UICONTROL Conjunto de giros de varios ejes]** para crear una fórmula que automatiza la generación de conjuntos de giros 2D. La agrupación de imágenes utiliza expresiones regulares de fila y columna para que los recursos de imagen se alineen correctamente en la ubicación correspondiente de la matriz multidimensional. No hay un número mínimo o máximo de filas o columnas que deba tener en un conjunto de giros de varios ejes.

Por ejemplo, supongamos que desea crear un conjunto de giros de varios ejes denominado `spin-2dspin`. Tiene un conjunto de imágenes de conjuntos de giros que contienen tres filas, con 12 imágenes por fila. Las imágenes reciben el nombre siguiente:

```
spin-01-01
 spin-01-02
 …
 spin-01-12
 spin-02-01
 …
 spin-03-12
```

Con esta información, la fórmula Tipo de conjunto de lotes se puede crear de la siguiente manera:

![chlimage_1-560](assets/chlimage_1-560.png)

La agrupación de la parte del nombre de recurso compartido del conjunto de giros se agrega al **[!UICONTROL Coincidencia]** (como resaltado). La parte variable del nombre del recurso que contiene la fila y la columna se agrega a los campos **[!UICONTROL Fila]** y **[!UICONTROL Columna]**, respectivamente.

Cuando se carga y publica el conjunto de giros, se activa el nombre de la fórmula de conjunto de giros 2D que aparece en **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]** en el cuadro de diálogo **[!UICONTROL Opciones de carga de trabajo]**.

**Para crear un ajuste preestablecido de conjunto de lotes para la generación automática de un conjunto de giros 2D:**

**RIESGO: ¿MANTÉNGASE ASÍ?**

1. Abra el [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), luego inicie sesión en su cuenta.

   Adobe proporcionó las credenciales y los detalles de inicio de sesión en el momento del aprovisionamiento. Si no tiene esta información, póngase en contacto con el servicio de atención al cliente de Adobe.

1. En la barra de navegación cerca de la parte superior de la página, vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]** > **[!UICONTROL Ajuste preestablecido de conjunto de lotes]**.

   **[!UICONTROL Ver formulario]**, tal y como se establece en la esquina superior derecha de la página Detalles, es la vista predeterminada.

1. En el panel Lista de ajustes preestablecidos, seleccione **[!UICONTROL Agregar]** para activar los campos de definición en el panel Detalles del lado derecho de la pantalla.
1. En el panel Detalles, en el campo Nombre de ajuste preestablecido , escriba un nombre para el ajuste preestablecido.
1. En el menú desplegable Tipo de conjunto de lotes, seleccione **[!UICONTROL Conjunto de recursos]**.
1. En la lista desplegable Subtipo , seleccione **[!UICONTROL Conjunto de giros de varios ejes]**.
1. Expandir **[!UICONTROL Convenciones de nomenclatura de recursos]** y, a continuación, en la lista desplegable Nombres de archivo , seleccione **[!UICONTROL Personalizado]**.
1. Utilice los atributos **[!UICONTROL Coincidencia]** y, opcionalmente, **[!UICONTROL Nombre base]** para establecer una expresión regular para la asignación de nombres a los recursos de imagen que conforman la agrupación.

   Por ejemplo, el literal Match regular puede tener el siguiente aspecto:

   `(w+)-w+-w+`

1. Expandir **[!UICONTROL Posición de columna de fila]** y, a continuación, defina el formato de nombre para la posición del recurso de imagen en la matriz de conjunto de giros 2D.

   Utilice el paréntesis para adoptar la posición de fila o columna en el nombre del archivo.

   Por ejemplo, para la expresión regular de fila, puede tener el siguiente aspecto:

   `\w+-R([0-9]+)-\w+`

   o

   `\w+-(\d+)-\w+`

   Para la expresión regular de su columna, puede tener el siguiente aspecto:

   `\w+-\w+-C([0-9]+)`

   o

   `\w+-\w+-C(\d+)`

   Los ejemplos anteriores son únicamente para fines de demostración. Puede crear la expresión regular según sus necesidades.

   >[!NOTE]
   Si la combinación de expresiones regulares de fila y columna no puede determinar la posición del recurso dentro de la matriz de conjuntos de giros multidimensionales, el recurso no se agrega al conjunto. También se registra un error.

1. Para Set Naming and Creation Convention , especifique el sufijo o prefijo del nombre base definido en la Convención de nombres de recursos.

   Además, defina dónde se crea el conjunto de giros dentro de la estructura de carpetas de Dynamic Media Classic.

   Si define un gran número de conjuntos, mantenga los conjuntos separados de las carpetas que contienen los propios recursos. Por ejemplo, cree una carpeta Conjuntos de giros para colocar los conjuntos generados aquí.

1. En el panel Detalles, seleccione **[!UICONTROL Guardar]**.
1. Select **[!UICONTROL Activo]** junto al nuevo nombre del ajuste preestablecido.

   Al activar el ajuste preestablecido, se garantiza que, al cargar recursos en Dynamic Media, el ajuste preestablecido de conjunto de lotes se aplique para generar el conjunto.

### (Opcional) Ajuste el rendimiento del modo Dynamic Media - Scene7 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

**RIESGO: ¿MANTÉNGASE ASÍ?**

Para mantener Dynamic Media en modo Scene7 funcionando sin problemas, Adobe recomienda los siguientes consejos de ajuste del rendimiento/escalabilidad de la sincronización:

* Actualización de los parámetros de trabajo predefinidos para el procesamiento de diferentes formatos de archivo.
* Actualización de los subprocesos de trabajo de la cola de Granite (recursos de vídeo) predefinidos.
* Actualización de los subprocesos de trabajo de la cola de Granite transient predefinidos (imágenes y recursos que no sean de vídeo).
* Actualización de las conexiones de carga máximas al servidor de Dynamic Media Classic.

#### Actualizar los parámetros de trabajo predefinidos para el procesamiento de diferentes formatos de archivo

**RIESGO: ¿MANTÉNGASE ASÍ?**

Puede ajustar los parámetros de trabajo para un procesamiento más rápido al cargar archivos. Por ejemplo, si carga archivos de PSD, pero no desea procesarlos como plantillas, puede establecer la extracción de capas en false (desactivado). En tal caso, el parámetro de trabajo ajustado aparece de la siguiente manera: `process=None&createTemplate=false`.

Si desea activar la creación de plantillas, utilice los siguientes parámetros: `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe recomienda utilizar los siguientes parámetros de trabajo &quot;ajustados&quot; para archivos de PDF, PostScript® y PSD:

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| Tipo de archivo | Parámetros de trabajo recomendados |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

Para actualizar cualquiera de estos parámetros, siga los pasos indicados en [Habilitación de la compatibilidad con los parámetros de trabajo de carga de recursos/Dynamic Media Classic basados en tipos MIME](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).

#### Actualizar la cola de flujo de trabajo transitorio de Granite {#updating-the-granite-transient-workflow-queue}

**RIESGO: ¿MANTÉNGASE ASÍ?**

La cola Flujo de trabajo de tránsito de Granite se utiliza para la variable **[!UICONTROL Recurso de actualización DAM]** flujo de trabajo. En Dynamic Media, se utiliza para la ingesta y el procesamiento de imágenes.

**Para actualizar la cola de flujo de trabajo transitorio de Granite:**

1. Vaya a [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) y busque **Cola: Cola de flujo de trabajo transitorio de Granite**.

   >[!NOTE]
   Es necesario buscar texto en lugar de una dirección URL directa porque el OSGi PID se genera dinámicamente.

1. En el **[!UICONTROL Trabajos paralelos máximos]** , cambie el número al valor deseado.

   Puede aumentar **[!UICONTROL Trabajos paralelos máximos]** para admitir correctamente la carga pesada de archivos en Dynamic Media. El valor exacto depende de la capacidad del hardware. En ciertos casos (es decir, una migración inicial o una carga masiva única), puede utilizar un valor grande. No obstante, tenga en cuenta que el uso de un valor grande (por ejemplo, dos veces el número de núcleos) puede tener efectos negativos en otras actividades simultáneas. Como tal, pruebe y ajuste el valor en función de su caso de uso particular.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![imagen_1](assets/chlimage_1.jpeg)

1. Seleccione **[!UICONTROL Guardar]**.

#### Actualizar la cola de flujo de trabajo de Granite {#updating-the-granite-workflow-queue}

**RIESGO: ¿MANTÉNGASE ASÍ?**

La cola Granite Workflow se utiliza para flujos de trabajo no transitorios. En Dynamic Media, se utilizaba para procesar vídeos con la variable **[!UICONTROL Codificar vídeo de Dynamic Media]** flujo de trabajo.

**Para actualizar la cola de flujo de trabajo de Granite:**

1. Vaya a `https://<server>/system/console/configMgr` y busque **Cola: Cola de flujo de trabajo de Granite**.

   >[!NOTE]
   Es necesario buscar texto en lugar de una dirección URL directa porque el OSGi PID se genera dinámicamente.

1. En el **[!UICONTROL Trabajos paralelos máximos]** , cambie el número al valor deseado.

   Puede aumentar el número máximo de trabajos paralelos para admitir correctamente la carga pesada de archivos en Dynamic Media. El valor exacto depende de la capacidad del hardware. En ciertos casos (es decir, una migración inicial o una carga masiva única), puede utilizar un valor grande. No obstante, tenga en cuenta que el uso de un valor grande (por ejemplo, dos veces el número de núcleos) puede tener efectos negativos en otras actividades simultáneas. Como tal, pruebe y ajuste el valor en función de su caso de uso particular.

   ![Chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Seleccione **[!UICONTROL Guardar]**.

#### Actualizar la conexión de carga de Dynamic Media Classic {#updating-the-scene-upload-connection}

**RIESGO: ¿MANTÉNGASE ASÍ?**

La configuración de conexión de carga de Scene7 sincroniza los recursos de Experience Manager con los servidores de Dynamic Media Classic.

**Para actualizar la conexión de carga de Dynamic Media Classic:**

1. Vaya a `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. En el **[!UICONTROL Número de conexiones]** o **[!UICONTROL Tiempo de espera de trabajo activo]** , cambie el número como desee.

   La variable **[!UICONTROL Número de conexiones]** el ajuste controla el número máximo de conexiones HTTP permitidas para el Experience Manager de carga de Dynamic Media; normalmente, el valor predefinido de diez conexiones es suficiente.

   La variable **[!UICONTROL Tiempo de espera de trabajo activo]** determina el tiempo de espera para que los recursos de Dynamic Media cargados se publiquen en el servidor de entrega. Este valor es de 2100 segundos o 35 minutos de forma predeterminada.

   Para la mayoría de los casos de uso, el ajuste de 2100 es suficiente.

   ![Chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Seleccione **[!UICONTROL Guardar]**.

### (Opcional) Filtrar recursos para la replicación {#optional-filtering-assets-for-replication}

**RIESGO: CONSERVAR TAL CUAL**

En implementaciones que no son de Dynamic Media, se replican *all* recursos (imágenes y vídeo) desde el entorno de creación de Experience Manager al nodo de publicación de Experience Manager. Este flujo de trabajo es necesario porque los servidores de publicación de Experience Manager también entregan los recursos.

Sin embargo, en las implementaciones de Dynamic Media, dado que los recursos se entregan mediante el Cloud Service, no es necesario replicar esos mismos recursos en los nodos de publicación de Experience Manager. Este flujo de trabajo de &quot;publicación híbrida&quot; evita costos de almacenamiento adicionales y tiempos de procesamiento más largos para replicar recursos. Otros contenidos, como las páginas del sitio, se siguen sirviendo desde los nodos de publicación del Experience Manager.

Los filtros proporcionan una forma de *excluir* los recursos se replican en el nodo de publicación de Experience Manager.

#### Usar filtros de recursos predeterminados para la replicación {#using-default-asset-filters-for-replication}

**RIESGO: CONSERVAR TAL CUAL**

Si usa Dynamic Media para imágenes, vídeos o ambos, puede usar los filtros predeterminados que Adobe proporciona tal cual. Los siguientes filtros están activos de forma predeterminada:

|  | Filtro | Tipo de máquina | Representaciones |
| --- | --- | --- | --- |
| Entrega de imágenes de Dynamic Media | filter-image<br>filter-sets | Comienza con **image/**<br> Contiene **aplicaciones/** y termine con **set**. | Las &quot;imágenes de filtro&quot; integradas (se aplican a recursos de imágenes únicas, incluidas imágenes interactivas) y &quot;conjuntos de filtros&quot; (se aplica a conjuntos de giros, conjuntos de imágenes, conjuntos de medios mixtos y conjuntos de carrusel):<br>・ Excluir de la replicación la imagen original y las representaciones de imágenes estáticas. |
| Entrega de vídeo de Dynamic Media | filter-video | Comienza con **video/** | El &quot;vídeo de filtro&quot; listo para usar:<br>・ Excluir de la replicación el vídeo original y las representaciones en miniatura estáticas. |

>[!NOTE]
Los filtros se aplican a tipos MIME y no pueden ser específicos de la ruta.

#### Personalización de filtros de recursos para replicación {#customizing-asset-filters-for-replication}

**RIESGO: CONSERVAR TAL CUAL**

1. En el Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. En el árbol de carpetas de la izquierda, vaya a `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` para revisar los filtros.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. Para definir el tipo de hora para el filtro, puede localizar el tipo de hora de la siguiente manera:

   En el carril izquierdo, expanda `content > dam > <locate_your_asset> > jcr:content > metadata`y, a continuación, en la tabla, busque `dc:format`.

   El siguiente gráfico es un ejemplo de la ruta de un recurso a `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Observe que la variable `dc:format` para el recurso `Fiji Red.jpg` es `image/jpeg`.

   Para que este filtro se aplique a todas las imágenes, independientemente de su formato, establezca el valor en `image/*` donde `*` es una expresión regular que se aplica a todas las imágenes de cualquier formato.

   Para que el filtro se aplique solo a las imágenes del tipo JPEG, introduzca un valor de `image/jpeg`.

1. Defina qué representaciones desea incluir o excluir de la replicación.

   Los caracteres que se pueden usar para filtrar para la replicación son los siguientes:

   | Carácter que se va a usar | Cómo se filtran los recursos para la replicación |
   | --- | --- |
   | * | Carácter comodín |
   | + | Incluye recursos para replicación |
   | - | Excluye los activos de la replicación |

   Vaya a `content/dam/<locate your asset>/jcr:content/renditions`.

   El siguiente gráfico es un ejemplo de las representaciones de un recurso.

   ![Chlimage_1-4](assets/chlimage_1-4.png)

   Si sólo desea replicar el original, entonces ingresaría `+original`.
