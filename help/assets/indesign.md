---
title: Integrar [!DNL Assets] con [!DNL InDesign Server]
description: Aprenda a integrar [!DNL Adobe Experience Manager Assets] con [!DNL Adobe InDesign Server].
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
source-git-commit: 67e145e250bbe386168ab2c0f8967f91aa9d8a36
workflow-type: tm+mt
source-wordcount: '1591'
ht-degree: 4%

---

# Integrar [!DNL Adobe Experience Manager Assets] con [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] utilice:

* Un proxy para distribuir la carga de ciertas tareas de procesamiento. Un proxy es una instancia [!DNL Experience Manager] que se comunica con un trabajador proxy para realizar una tarea específica y otras instancias [!DNL Experience Manager] para ofrecer los resultados.
* Trabajador de proxy para definir y administrar una tarea específica.
Pueden abarcar una amplia variedad de tareas; por ejemplo, usar un [!DNL InDesign Server] para procesar archivos.

Para cargar archivos completamente en [!DNL Experience Manager Assets] que ha creado con [!DNL Adobe InDesign] se utiliza un proxy. Esto utiliza un trabajador proxy para comunicarse con [!DNL Adobe InDesign Server], donde se ejecutan [scripts](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) para extraer metadatos y generar varias representaciones para [!DNL Experience Manager Assets]. El trabajador del proxy habilita la comunicación bidireccional entre las instancias [!DNL InDesign Server] y [!DNL Experience Manager] en una configuración de nube.

>[!NOTE]
>
>[!DNL Adobe InDesign] se ofrece en dos ofertas independientes. [Adobe ](https://www.adobe.com/products/indesign.html) en la aplicación de escritorio de Designer que se utiliza para diseñar diseños de página para impresión y distribución digital. [Adobe InDesign ](https://www.adobe.com/products/indesignserver.html) Server le permite crear mediante programación documentos automatizados basados en lo que haya creado con  [!DNL InDesign]. Funciona como un servicio que ofrece una interfaz con su motor [ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting). Los scripts se escriben en [!DNL ExtendScript], que es similar a [!DNL JavaScript]. Para obtener información sobre los scripts [!DNL InDesign], consulte [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## Funcionamiento de la extracción {#how-the-extraction-works}

El [!DNL Adobe InDesign Server] se puede integrar con [!DNL Experience Manager Assets] para que los archivos INDD creados con [!DNL InDesign] se puedan cargar, generar representaciones, extraer todos los medios (por ejemplo, vídeo) y almacenarse como recursos:

>[!NOTE]
>
>Las versiones anteriores de [!DNL Experience Manager] podían extraer XMP y la miniatura, ahora se pueden extraer todos los medios.

1. Cargue su archivo INDD a [!DNL Experience Manager Assets].
1. Un marco envía secuencias de comandos de comandos a [!DNL InDesign Server] mediante SOAP (Simple Object Access Protocol).
Este script de comando:

   * Recupere el archivo INDD.
   * Ejecutar comandos [!DNL InDesign Server]:

      * Se extraen la estructura, el texto y los archivos multimedia.
      * Se generan representaciones de PDF y JPG.
      * Se generan representaciones HTML e IDML.
   * Vuelva a publicar los archivos resultantes en [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML es un formato basado en XML que procesa todo el contenido del archivo [!DNL InDesign]. Se almacena como un paquete comprimido usando la compresión [ZIP](https://www.techterms.com/definition/zip). Para obtener más información, consulte [Formatos de intercambio de InDesign INX e IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >Si el [!DNL InDesign Server] no está instalado o no está configurado, puede seguir cargando un archivo INDD en [!DNL Experience Manager]. Sin embargo, las representaciones generadas se limitarán a PNG y JPEG. No podrá generar HTML, .idml ni las representaciones de página.

1. Después de la generación de extracción y representación:

   * La estructura se replica en `cq:Page` (tipo de representación).
   * El texto extraído y los archivos se almacenan en [!DNL Experience Manager Assets].
   * Todas las representaciones se almacenan en [!DNL Experience Manager Assets], en el propio recurso.

## Integración del [!DNL InDesign Server] con el Experience Manager {#integrating-the-indesign-server-with-aem}

Para integrar el [!DNL InDesign Server] para utilizarlo con [!DNL Experience Manager Assets] y después de configurar el proxy, debe:

1. [Instale el InDesign Server](#installing-the-indesign-server).
1. Si es necesario, [configure el flujo de trabajo de recursos de Experience Manager](#configuring-the-aem-assets-workflow).
Esto solo es necesario si los valores predeterminados no son adecuados para su instancia.
1. Configure un [trabajador proxy para el InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Instale el [!DNL InDesign Server] {#installing-the-indesign-server}

Para instalar e iniciar el [!DNL InDesign Server] para usar con [!DNL Experience Manager]:

1. Descargue e instale el [!DNL InDesign Server].

1. Si es necesario, puede personalizar la configuración de la instancia [!DNL InDesign Server].

1. Desde la línea de comandos, inicie el servidor:

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Esto iniciará el servidor con el complemento SOAP escuchando en el puerto 8080. Todos los mensajes de registro y los resultados se escriben directamente en la ventana de comandos.

   >[!NOTE]
   >
   >Si desea guardar los mensajes de salida en un archivo, utilice la redirección; por ejemplo, en Windows:
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configuración del flujo de trabajo [!DNL Experience Manager Assets] {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] tiene un flujo de trabajo preconfigurado  **[!UICONTROL DAM Update Asset]**, que tiene varios pasos de proceso específicos para  [!DNL InDesign]:

* [Extracción de medios](#media-extraction)
* [Extracción de páginas](#page-extraction)

Este flujo de trabajo está configurado con valores predeterminados que se pueden adaptar para su configuración en las distintas instancias de autor (se trata de un flujo de trabajo estándar, por lo que hay más información disponible en [Edición de un flujo de trabajo](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Si está utilizando los valores predeterminados (incluido el puerto SOAP), no se necesita ninguna configuración.

Después de la configuración, la carga de archivos [!DNL InDesign] en [!DNL Experience Manager Assets] (por cualquiera de los métodos habituales) déclencheur el flujo de trabajo para procesar el recurso y preparar las distintas representaciones. Pruebe la configuración cargando un archivo INDD en [!DNL Experience Manager Assets] para confirmar que ve las diferentes representaciones creadas por ID en `<*your_asset*>.indd/Renditions`

#### Extracción de medios {#media-extraction}

Este paso controla la extracción de medios del archivo INDD.

Para personalizar, puede editar la pestaña **[!UICONTROL Argumentos]** del paso **[!UICONTROL Extracción de medios]**.

![Argumentos de extracción de medios y rutas de secuencias de comandos](assets/media_extraction_arguments_scripts.png)

Argumentos de extracción de medios y rutas de secuencias de comandos

* **Biblioteca** de ExtendScript: Esta es una sencilla biblioteca de métodos http get/post , requerida por las otras secuencias de comandos.

* **Ampliar secuencias de comandos**: Aquí puede especificar diferentes combinaciones de scripts. Si desea que sus propios scripts se ejecuten en [!DNL InDesign Server], guarde los scripts en `/apps/settings/dam/indesign/scripts`.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>No cambie la biblioteca ExtendScript. Esta biblioteca proporciona la funcionalidad HTTP necesaria para comunicarse con Sling. Esta configuración especifica la biblioteca que se enviará al [!DNL InDesign Server] para su uso allí.

El script `ThumbnailExport.jsx` ejecutado por el paso del flujo de trabajo de extracción de medios genera una representación en miniatura en formato JPG. Esta representación la utiliza el paso del flujo de trabajo Procesar miniaturas para generar las representaciones estáticas requeridas por [!DNL Experience Manager].

Puede configurar el paso del flujo de trabajo Procesar miniaturas para generar representaciones estáticas de diferentes tamaños. Asegúrese de no eliminar los valores predeterminados, ya que son necesarios para la interfaz [!DNL Experience Manager Assets]. Por último, el paso Eliminar representación de vista previa de imagen del flujo de trabajo elimina la representación de miniaturas JPG, ya que ya no es necesaria.

#### Extracción de páginas {#page-extraction}

Esto crea una página [!DNL Experience Manager] a partir de los elementos extraídos. Un controlador de extracción se utiliza para extraer datos de una representación (actualmente HTML o IDML). Estos datos se utilizan para crear una página con PageBuilder.

Para personalizar, puede editar la pestaña **[!UICONTROL Argumentos]** del paso **[!UICONTROL Extracción de página]**.

![imagen_1-96](assets/chlimage_1-289.png)

* **Controlador de extracción de página**: En la lista emergente, seleccione el controlador que desee utilizar. Un controlador de extracción funciona en una representación específica, elegida por un elemento relacionado `RenditionPicker` (consulte la API `ExtractionHandler`).
En una instalación estándar [!DNL Experience Manager] está disponible lo siguiente:
   * Controlador de extracción de exportación IDML: Funciona en la representación `IDML` generada en el paso MediaExtract.

* **Nombre** de página: Especifique el nombre que desea asignar a la página resultante. Si se deja en blanco, el nombre es &quot;página&quot; (o una derivada si ya existe &quot;página&quot;).

* **Título** de página: Especifique el título que desea asignar a la página resultante.

* **Ruta** raíz de página: Ruta a la ubicación raíz de la página resultante. Si se deja en blanco, se utilizará el nodo que contiene las representaciones del recurso.

* **Plantilla** de página: La plantilla que se utilizará al generar la página resultante.

* **Diseño** de página: El diseño de página que se utilizará al generar la página resultante.

### Configurar el trabajador del proxy para [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>El trabajador reside en la instancia de proxy.

1. En la consola Herramientas, expanda **[!UICONTROL Configuraciones de Cloud Services]** en el panel izquierdo. A continuación, expanda **[!UICONTROL Cloud Proxy Configuration]**.

1. Haga doble clic en el programa de **[!UICONTROL IDS de trabajo]** para abrirlo y configurarlo.

1. Haga clic en **[!UICONTROL Editar]** para abrir el cuadro de diálogo de configuración y definir la configuración necesaria:

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **Grupo**
de IDLos puntos de conexión SOAP que se utilizarán para la comunicación con  [!DNL InDesign Server]. Puede agregar, quitar y ordenar los elementos que sean necesarios.

1. Haga clic en Aceptar para guardar.

### Configurar el externalizador de vínculos de CQ de día {#configuring-day-cq-link-externalizer}

Si [!DNL InDesign Server] y [!DNL Experience Manager] están en hosts diferentes o si una o ambas aplicaciones no están funcionando en puertos predeterminados, configure [!UICONTROL Day CQ Link Externalizer] para establecer el nombre de host, el puerto y la ruta de contenido para [!DNL InDesign Server].

1. Acceda a la consola web en `https://[aem_server]:[port]/system/console/configMgr`.
1. Busque la configuración **[!UICONTROL Day CQ Link Externalizer]**. Haga clic en **[!UICONTROL Editar]** para abrirlo.
1. La configuración del externalizador de vínculos ayuda a crear direcciones URL absolutas para la implementación [!DNL Experience Manager] y para [!DNL InDesign Server]. Utilice el campo **[!UICONTROL Domains]** para especificar el nombre de host de [!DNL Adobe InDesign Server]. Haga clic en **Guardar**.

   En las direcciones URL absolutas, utilice `localhost` como nombre de host para la instancia local (de autor) y nombre de host o dirección IP para la instancia de publicación, como se muestra en la siguiente ilustración.

   ![Configuración del externalizador de vínculos](assets/link-externalizer-config.png)

### Habilitar el procesamiento de trabajos paralelo para [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

Ahora puede habilitar el procesamiento paralelo de trabajos para IDS. Determine el número máximo de trabajos paralelos (`x`) que un [!DNL InDesign Server] puede procesar:

* En un solo equipo multiprocesador, el número máximo de trabajos paralelos (`x`) que un [!DNL InDesign Server] puede procesar es uno menor que el número de procesadores que ejecutan IDS.
* Cuando ejecute IDS en varios equipos, deberá contar el número total de procesadores disponibles (es decir, en todos los equipos) y restar el número total de equipos.

Para configurar el número de trabajos de ID paralelos:

1. Abra la pestaña **[!UICONTROL Configurations]** de la Consola Felix; por ejemplo: `https://[aem_server]:[port]/system/console/configMgr`.

1. Seleccione la cola de procesamiento de IDS en `Apache Sling Job Queue Configuration`.

1. Configurar:

   * **Tipo** - `Parallel`
   * **Máximo de trabajos paralelos** :  `<*x*>` (según se ha calculado anteriormente)

1. Guarde estos cambios.
1. Para habilitar la compatibilidad con varias sesiones para Adobe CS6 y posteriores, marque la casilla `enable.multisession.name` en la configuración `com.day.cq.dam.ids.impl.IDSJobProcessor.name` .
1. Cree un [grupo de `x` trabajadores de IDS añadiendo extremos SOAP a la configuración de IDS Worker](#configuring-the-proxy-worker-for-indesign-server).

   Si hay varios equipos que ejecutan [!DNL InDesign Server], añada extremos SOAP (número de procesadores por máquina -1) para cada equipo.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>Al trabajar con un grupo de trabajadores, puede habilitar la lista de bloqueados de los trabajadores de IDS.
>
>Para ello, active la casilla **[!UICONTROL enable.retry.name]**, en la configuración `com.day.cq.dam.ids.impl.IDSJobProcessor.name`, que habilita las recuperaciones de trabajos de IDS.
>
>Además, en la configuración `com.day.cq.dam.ids.impl.IDSPoolImpl.name`, establezca un valor positivo para el parámetro `max.errors.to.blacklist` que determina el número de recuperaciones de trabajos antes de prohibir un ID en la lista de controladores de trabajos.
>
>De forma predeterminada, después del tiempo configurable (`retry.interval.to.whitelist.name`) en minutos, el programa de trabajo de IDS se vuelve a validar. Si el trabajador se encuentra en línea, se elimina de la lista de bloqueados.

## Habilite la compatibilidad con [!DNL InDesign Server] 10.0 o posterior {#enabling-support-for-indesign-server-or-later}

Para [!DNL InDesign Server] 10.0 o superior, realice los siguientes pasos para habilitar el soporte de varias sesiones.

1. Abra el Administrador de configuración desde la instancia [!DNL Experience Manager Assets] `https://[aem_server]:[port]/system/console/configMgr`.
1. Edite la configuración `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Seleccione la opción **[!UICONTROL ids.cc.enable]** y haga clic en **[!UICONTROL Guardar]**.

>[!NOTE]
>
>Para la integración [!DNL InDesign Server] con [!DNL Experience Manager Assets], utilice un procesador de varios núcleos porque la función de soporte de sesión necesaria para la integración no es compatible con sistemas de un solo núcleo.

## Configurar las credenciales [!DNL Experience Manager] {#configure-aem-credentials}

Puede cambiar las credenciales de administrador predeterminadas (nombre de usuario y contraseña) para acceder a [!DNL InDesign Server] desde su implementación [!DNL Experience Manager] sin romper la integración con [!DNL InDesign Server].

1. Ir a `/etc/cloudservices/proxy.html`.
1. En el cuadro de diálogo, especifique el nuevo nombre de usuario y contraseña.
1. Guarde las credenciales.

>[!MORELIKETHIS]
>
>* [Acerca de Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

