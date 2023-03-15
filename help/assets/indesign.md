---
title: Integrar  [!DNL Assets]  con  [!DNL InDesign Server]
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

* Un proxy para distribuir la carga de ciertas tareas de procesamiento. Un proxy es un [!DNL Experience Manager] instancia que se comunica con un trabajador proxy para realizar una tarea específica y otras [!DNL Experience Manager] instancias para entregar los resultados.
* Un trabajador proxy para definir y administrar una tarea específica.
Pueden cubrir una amplia variedad de tareas; por ejemplo, el uso de una [!DNL InDesign Server] para procesar archivos.

Para cargar archivos completamente en [!DNL Experience Manager Assets] que ha creado con [!DNL Adobe InDesign] se utiliza un proxy. Utiliza un trabajador proxy para comunicarse con el [!DNL Adobe InDesign Server], donde [scripts](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) se ejecutan para extraer metadatos y generar varias representaciones para [!DNL Experience Manager Assets]. El trabajador proxy habilita la comunicación bidireccional entre los [!DNL InDesign Server] y el [!DNL Experience Manager] instancias en una configuración de nube.

>[!NOTE]
>
>[!DNL Adobe InDesign] se ofrece como dos ofertas independientes. [Adobe InDesign](https://www.adobe.com/products/indesign.html) aplicación de escritorio que se utiliza para diseñar diseños de página para la impresión y distribución digital. [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html) le permite crear documentos automatizados mediante programación en función de lo que haya creado con [!DNL InDesign]. Funciona como un servicio que ofrece una interfaz a su [ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) engine.Los scripts se escriben en [!DNL ExtendScript], que es similar a [!DNL JavaScript]. Para obtener información acerca de [!DNL InDesign] secuencias de comandos consulte [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## Funcionamiento de la extracción {#how-the-extraction-works}

El [!DNL Adobe InDesign Server] se puede integrar con [!DNL Experience Manager Assets] para que los archivos INDD creados con [!DNL InDesign] se pueden cargar, generar representaciones, extraer todos los medios (por ejemplo, vídeo) y almacenar como recursos:

>[!NOTE]
>
>Versiones anteriores de [!DNL Experience Manager] XMP fueron capaces de extraer la vista en miniatura y la vista en miniatura, ahora se pueden extraer todos los medios.

1. Cargue su archivo INDD en [!DNL Experience Manager Assets].
1. Un marco de trabajo envía scripts de comando a [!DNL InDesign Server] mediante SOAP (Simple Object Access Protocol).
Esta secuencia de comandos:

   * Recupere el archivo INDD.
   * Ejecutar [!DNL InDesign Server] comandos:

      * Se extraerán la estructura, el texto y los archivos multimedia.
      * Se generan las representaciones de PDF y JPG.
      * Se generan las representaciones HTML e IDML.
   * Volver a publicar los archivos resultantes en [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML es un formato basado en XML que procesa todo el contenido del [!DNL InDesign] archivo. Se almacena como un paquete comprimido utilizando [ZIP](https://www.techterms.com/definition/zip) compresión. Para obtener más información, consulte [Formatos de intercambio de InDesign INX e IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >Si la variable [!DNL InDesign Server] no está instalado o no está configurado, a continuación, aún puede cargar un archivo INDD en [!DNL Experience Manager]. Sin embargo, las representaciones generadas se limitarán a PNG y JPEG. No podrá generar representaciones de HTML, .idml ni de página.

1. Después de la generación de la extracción y la representación:

   * La estructura se duplica en un `cq:Page` (tipo de representación).
   * El texto y los archivos extraídos se almacenan en [!DNL Experience Manager Assets].
   * Todas las representaciones se almacenan en [!DNL Experience Manager Assets], en el propio recurso.

## Integración de [!DNL InDesign Server] con Experience Manager {#integrating-the-indesign-server-with-aem}

Para integrar [!DNL InDesign Server] para su uso con [!DNL Experience Manager Assets] y después de configurar el proxy, debe:

1. [Instalación del InDesign Server](#installing-the-indesign-server).
1. Si es necesario, [Configuración del flujo de trabajo de Experience Manager Assets](#configuring-the-aem-assets-workflow).
Esto solo es necesario si los valores predeterminados no son adecuados para su instancia.
1. Configurar un [trabajador proxy para el InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Instale el [!DNL InDesign Server] {#installing-the-indesign-server}

Para instalar e iniciar el [!DNL InDesign Server] para su uso con [!DNL Experience Manager]:

1. Descargue e instale [!DNL InDesign Server].

1. Si es necesario, puede personalizar la configuración de su [!DNL InDesign Server] ejemplo.

1. Desde la línea de comandos, inicie el servidor:

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Esto inicia el servidor con el complemento SOAP escuchando en el puerto 8080. Todos los mensajes de registro y los resultados se escriben directamente en la ventana de comandos.

   >[!NOTE]
   >
   >Si desea guardar los mensajes de salida en un archivo, utilice la redirección; por ejemplo, en Windows:
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configure las variables [!DNL Experience Manager Assets] workflow {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] tiene un flujo de trabajo preconfigurado **[!UICONTROL Recurso de actualización DAM]**, que tiene varios pasos de proceso específicos para [!DNL InDesign]:

* [Extracción de medios](#media-extraction)
* [Extracción de páginas](#page-extraction)

Este flujo de trabajo se configura con valores predeterminados que se pueden adaptar a la configuración en las distintas instancias de autor (se trata de un flujo de trabajo estándar), por lo que encontrará más información en [Edición de un flujo de trabajo](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Si utiliza los valores predeterminados (incluido el puerto SOAP), no es necesaria ninguna configuración.

Después de la configuración, al cargar [!DNL InDesign] archivos en [!DNL Experience Manager Assets] (mediante cualquiera de los métodos habituales) déclencheur el flujo de trabajo para procesar el recurso y preparar las distintas representaciones. Pruebe la configuración cargando un archivo INDD en [!DNL Experience Manager Assets] para confirmar que ve las diferentes representaciones creadas por IDS en `<*your_asset*>.indd/Renditions`

#### Extracción de medios {#media-extraction}

Este paso controla la extracción de medios del archivo INDD.

Para personalizar, puede editar la pestaña **[!UICONTROL Argumentos]** del paso **[!UICONTROL Extracción de medios]**.

![Argumentos de extracción de medios y rutas de scripts](assets/media_extraction_arguments_scripts.png)

Argumentos de extracción de medios y rutas de scripts

* **Biblioteca de ExtendScript**: es una biblioteca de métodos simple http get/post, requerida por los demás scripts.

* **Ampliar scripts**: aquí puede especificar diferentes combinaciones de scripts. Si desea que sus propios scripts se ejecuten en [!DNL InDesign Server], guarde los scripts en `/apps/settings/dam/indesign/scripts`.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>No cambie la biblioteca ExtendScript. Esta biblioteca proporciona la funcionalidad HTTP necesaria para comunicarse con Sling. Esta configuración especifica la biblioteca que se enviará a [!DNL InDesign Server] para su uso allí.

El `ThumbnailExport.jsx` La secuencia de comandos ejecutada por el paso de flujo de trabajo Extracción de medios genera una representación de miniaturas en formato de JPG. El paso del flujo de trabajo Procesar miniaturas utiliza esta representación para generar las representaciones estáticas requeridas por [!DNL Experience Manager].

Puede configurar el paso del flujo de trabajo Procesar miniaturas para generar representaciones estáticas en diferentes tamaños. Asegúrese de no eliminar los valores predeterminados, ya que son necesarios para el [!DNL Experience Manager Assets] interfaz. Por último, el paso de flujo de trabajo Eliminar representación de previsualización de imagen elimina la representación de miniaturas del JPG, ya que ya no es necesaria.

#### Extracción de página {#page-extraction}

Esto crea un [!DNL Experience Manager] de los elementos extraídos. Se utiliza un controlador de extracción para extraer datos de una representación (actualmente HTML o IDML). Estos datos se utilizan para crear una página con PageBuilder.

Para personalizar, puede editar la pestaña **[!UICONTROL Argumentos]** del paso **[!UICONTROL Extracción de página]**.

![chlimage_1-96](assets/chlimage_1-289.png)

* **Controlador de extracción de página**: En la lista emergente, seleccione el controlador que desee utilizar. Un controlador de extracción funciona en una representación específica, elegida por un elemento relacionado `RenditionPicker` (consulte la API `ExtractionHandler`).
En un estándar [!DNL Experience Manager] instalación está disponible lo siguiente:
   * IDML Export Extraction Handle: Funciona en `IDML` Representación generada en el paso MediaExtract.

* **Nombre de página**: especifique el nombre que desea tener asignado a la página resultante. Si se deja en blanco, el nombre es &quot;página&quot; (o un derivado si &quot;página&quot; ya existe).

* **Título de página**: especifique el título que desea tener asignado a la página resultante.

* **Ruta raíz de página**: Ruta a la ubicación raíz de la página resultante. Si se deja en blanco, se utilizará el nodo que contiene las representaciones del recurso.

* **Plantilla de página**: Plantilla que se utiliza al generar la página resultante.

* **Diseño de página**: El diseño de página que se utilizará al generar la página resultante.

### Configuración del trabajador proxy para [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>El trabajador reside en la instancia de proxy.

1. En la consola Herramientas, expanda **[!UICONTROL Configuraciones de Cloud Services]** en el panel izquierdo. A continuación, expanda **[!UICONTROL Configuración de proxy de nube]**.

1. Haga doble clic en el programa de **[!UICONTROL IDS de trabajo]** para abrirlo y configurarlo.

1. Clic **[!UICONTROL Editar]** para abrir el cuadro de diálogo de configuración y definir la configuración necesaria:

   ![proxy_disworkerconfig](assets/proxy_idsworkerconfig.png)

   * **Grupo IDS**
Los extremos SOAP que se utilizarán para comunicarse con el [!DNL InDesign Server]. Puede añadir, quitar y ordenar los elementos que sean necesarios.

1. Haga clic en Aceptar para guardar.

### Configurar el externalizador de vínculos CQ de día {#configuring-day-cq-link-externalizer}

Si la variable [!DNL InDesign Server] y [!DNL Experience Manager] están en hosts diferentes o una o ambas aplicaciones no funcionan en los puertos predeterminados y, a continuación, configure [!UICONTROL Externalizador de vínculos CQ de día] para establecer el nombre de host, el puerto y la ruta de contenido para [!DNL InDesign Server].

1. Acceda a la consola web en `https://[aem_server]:[port]/system/console/configMgr`.
1. Busque la configuración **[!UICONTROL Externalizador de vínculos CQ de día]**. Clic **[!UICONTROL Editar]** para abrir.
1. La configuración del externalizador de vínculos ayuda a crear direcciones URL absolutas para [!DNL Experience Manager] implementación y para [!DNL InDesign Server]. Uso **[!UICONTROL Domains]** para especificar el nombre de host de [!DNL Adobe InDesign Server]. Haga clic en **Guardar**.

   En direcciones URL absolutas, utilice `localhost` como el nombre de host de la instancia local (autor) y el nombre de host o la dirección IP de la instancia de publicación, como se muestra en la siguiente ilustración.

   ![Configuración del externalizador de vínculos](assets/link-externalizer-config.png)

### Habilitar el procesamiento de trabajos en paralelo para [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

Ahora puede habilitar el procesamiento de trabajos en paralelo para los ID. Determinar el número máximo de trabajos paralelos (`x`) an [!DNL InDesign Server] puede procesar:

* En un solo equipo multiprocesador, el número máximo de trabajos paralelos (`x`) que un [!DNL InDesign Server] puede procesar un número menor que el número de procesadores que ejecutan IDS.
* Cuando ejecuta IDS en varios equipos, necesita contar el número total de procesadores disponibles (es decir, en todos los equipos) y luego restar el número total de equipos.

Para configurar el número de trabajos de IDS paralelos:

1. Abra el **[!UICONTROL Configuraciones]** de la Consola Felix; por ejemplo: `https://[aem_server]:[port]/system/console/configMgr`.

1. Seleccione la cola de procesamiento de IDS en `Apache Sling Job Queue Configuration`.

1. Configurar:

   * **Tipo** - `Parallel`
   * **Máximo de trabajos paralelos** - `<*x*>` (según el cálculo anterior)

1. Guarde estos cambios.
1. Para habilitar la compatibilidad con varias sesiones para Adobe CS6 y versiones posteriores, marque `enable.multisession.name` casilla de verificación, en `com.day.cq.dam.ids.impl.IDSJobProcessor.name` configuración.
1. Crear un [grupo de `x` Trabajadores IDS agregando puntos finales SOAP a la configuración de IDS Worker](#configuring-the-proxy-worker-for-indesign-server).

   Si hay varios equipos en ejecución [!DNL InDesign Server], agregue puntos finales SOAP (número de procesadores por equipo -1) para cada equipo.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>Al trabajar con grupos de empleados, puede habilitar la lista de bloqueados de los empleados de IDS.
>
>Para ello, habilite la variable **[!UICONTROL enable.retry.name]** casilla de verificación, en `com.day.cq.dam.ids.impl.IDSJobProcessor.name` , que activa los reintentos de trabajos IDS.
>
>Además, en la `com.day.cq.dam.ids.impl.IDSPoolImpl.name` , defina un valor positivo para `max.errors.to.blacklist` parámetro que determina el número de reintentos de trabajos antes de excluir un ID de la lista de controladores de trabajos.
>
>De forma predeterminada, después de la variable configurable (`retry.interval.to.whitelist.name`) vez que se vuelve a validar el trabajador IDS de trabajo en minutos. Si el trabajador se encuentra en línea, se elimina de la lista de bloqueados.

## Habilitar compatibilidad con [!DNL InDesign Server] 10.0 o posterior {#enabling-support-for-indesign-server-or-later}

Para [!DNL InDesign Server] 10.0 o superior, realice los siguientes pasos para habilitar la compatibilidad con varias sesiones.

1. Abra el Administrador de configuración desde su [!DNL Experience Manager Assets] instancia `https://[aem_server]:[port]/system/console/configMgr`.
1. Editar la configuración `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Seleccione el **[!UICONTROL ids.cc.enable]** y haga clic en **[!UICONTROL Guardar]**.

>[!NOTE]
>
>Para [!DNL InDesign Server] integración con [!DNL Experience Manager Assets], utilice un procesador de núcleo múltiple porque la función de compatibilidad de sesión necesaria para la integración no es compatible con los sistemas de núcleo único.

## Configurar [!DNL Experience Manager] credenciales {#configure-aem-credentials}

Puede cambiar las credenciales de administrador predeterminadas (nombre de usuario y contraseña) para acceder a [!DNL InDesign Server] de su [!DNL Experience Manager] implementación sin romper la integración con [!DNL InDesign Server].

1. Vaya a `/etc/cloudservices/proxy.html`.
1. En el cuadro de diálogo, especifique el nuevo nombre de usuario y contraseña.
1. Guarde las credenciales.

>[!MORELIKETHIS]
>
>* [Acerca de Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

