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

* Un proxy para distribuir la carga de ciertas tareas de procesamiento. Un proxy es un [!DNL Experience Manager] instancia que se comunica con un trabajador proxy para realizar una tarea específica, y [!DNL Experience Manager] instancias para entregar los resultados.
* Trabajador de proxy para definir y administrar una tarea específica.
Pueden abarcar una amplia variedad de tareas; por ejemplo, si se usa un [!DNL InDesign Server] para procesar archivos.

Para cargar archivos por completo en [!DNL Experience Manager Assets] que ha creado con [!DNL Adobe InDesign] se utiliza un proxy. Utiliza un trabajador proxy para comunicarse con el [!DNL Adobe InDesign Server], donde [scripts](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) se ejecutan para extraer metadatos y generar varias representaciones para [!DNL Experience Manager Assets]. El trabajador proxy permite la comunicación bidireccional entre las variables [!DNL InDesign Server] y [!DNL Experience Manager] instancias en una configuración de nube.

>[!NOTE]
>
>[!DNL Adobe InDesign] se ofrece en dos ofertas independientes. [Adobe InDesign](https://www.adobe.com/products/indesign.html) aplicación de escritorio que se utiliza para diseñar diseños de página para impresión y distribución digital. [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html) le permite crear mediante programación documentos automatizados basados en lo que ha creado con [!DNL InDesign]. Funciona como un servicio que ofrece una interfaz con su [ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) motor.Las secuencias de comandos se escriben en [!DNL ExtendScript], que es similar a [!DNL JavaScript]. Para obtener información sobre [!DNL InDesign] secuencias de comandos ver [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## Funcionamiento de la extracción {#how-the-extraction-works}

La variable [!DNL Adobe InDesign Server] se puede integrar con [!DNL Experience Manager Assets] para que los archivos INDD creados con [!DNL InDesign] se pueden cargar, generar representaciones, extraer todos los medios (por ejemplo, vídeo) y almacenar como recursos:

>[!NOTE]
>
>Versiones anteriores de [!DNL Experience Manager] fueron capaces de extraer XMP y la miniatura, ahora se pueden extraer todos los medios.

1. Cargue su archivo INDD a [!DNL Experience Manager Assets].
1. Un marco envía secuencias de comandos de comando a la [!DNL InDesign Server] mediante SOAP (Protocolo simple de acceso a objetos).
Este script de comando:

   * Recupere el archivo INDD.
   * Ejecutar [!DNL InDesign Server] comandos:

      * Se extraen la estructura, el texto y los archivos multimedia.
      * Se generan representaciones de PDF y JPG.
      * Se generan representaciones de HTML e IDML.
   * Volver a anunciar los archivos resultantes en [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML es un formato basado en XML que procesa todo el contenido de la variable [!DNL InDesign] archivo. Se almacena como un paquete comprimido mediante [ZIP](https://www.techterms.com/definition/zip) compresión. Para obtener más información, consulte [Formatos de intercambio de InDesign INX e IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >Si la variable [!DNL InDesign Server] no está instalado o no está configurado, puede seguir cargando un archivo INDD en [!DNL Experience Manager]. Sin embargo, las representaciones generadas se limitarán a PNG y JPEG. No podrá generar representaciones de HTML, .idml ni de página.

1. Después de la generación de extracción y representación:

   * La estructura se duplica en un `cq:Page` (tipo de representación).
   * El texto extraído y los archivos se almacenan en [!DNL Experience Manager Assets].
   * Todas las representaciones se almacenan en [!DNL Experience Manager Assets], en el propio recurso.

## Integrar el [!DNL InDesign Server] con Experience Manager {#integrating-the-indesign-server-with-aem}

Para integrar la variable [!DNL InDesign Server] para usar con [!DNL Experience Manager Assets] y después de configurar el proxy, debe:

1. [Instalación del InDesign Server](#installing-the-indesign-server).
1. Si es necesario, [configuración del flujo de trabajo de Experience Manager Assets](#configuring-the-aem-assets-workflow).
Esto solo es necesario si los valores predeterminados no son adecuados para su instancia.
1. Configure un [trabajador proxy para el InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Instale el [!DNL InDesign Server] {#installing-the-indesign-server}

Para instalar e iniciar el [!DNL InDesign Server] para usar con [!DNL Experience Manager]:

1. Descargue e instale el [!DNL InDesign Server].

1. Si es necesario, puede personalizar la configuración de su [!DNL InDesign Server] instancia.

1. Desde la línea de comandos, inicie el servidor:

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Esto iniciará el servidor con el complemento SOAP escuchando en el puerto 8080. Todos los mensajes de registro y los resultados se escriben directamente en la ventana de comandos.

   >[!NOTE]
   >
   >Si desea guardar los mensajes de salida en un archivo, utilice la redirección; por ejemplo, en Windows:
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configure las variables [!DNL Experience Manager Assets] flujo de trabajo {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] tiene un flujo de trabajo preconfigurado **[!UICONTROL Recurso de actualización DAM]**, que tiene varios pasos de proceso específicos para [!DNL InDesign]:

* [Extracción de medios](#media-extraction)
* [Extracción de páginas](#page-extraction)

Este flujo de trabajo está configurado con valores predeterminados que pueden adaptarse para su configuración en las distintas instancias de creación (se trata de un flujo de trabajo estándar, por lo que puede obtener más información en [Edición de un flujo de trabajo](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Si está utilizando los valores predeterminados (incluido el puerto SOAP), no se necesita ninguna configuración.

Después de la configuración, cargue [!DNL InDesign] archivos en [!DNL Experience Manager Assets] (por cualquiera de los métodos habituales) déclencheur el flujo de trabajo para procesar el recurso y preparar las distintas representaciones. Pruebe la configuración cargando un archivo INDD en [!DNL Experience Manager Assets] para confirmar que ve las diferentes representaciones creadas por ID en `<*your_asset*>.indd/Renditions`

#### Extracción de medios {#media-extraction}

Este paso controla la extracción de medios del archivo INDD.

Para personalizar, puede editar la pestaña **[!UICONTROL Argumentos]** del paso **[!UICONTROL Extracción de medios]**.

![Argumentos de extracción de medios y rutas de secuencias de comandos](assets/media_extraction_arguments_scripts.png)

Argumentos de extracción de medios y rutas de secuencias de comandos

* **Biblioteca ExtendScript**: Esta es una sencilla biblioteca de métodos http get/post , requerida por las otras secuencias de comandos.

* **Ampliar secuencias de comandos**: Aquí puede especificar diferentes combinaciones de scripts. Si desea que sus propios scripts se ejecuten en la variable [!DNL InDesign Server], guarde las secuencias de comandos en `/apps/settings/dam/indesign/scripts`.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>No cambie la biblioteca ExtendScript. Esta biblioteca proporciona la funcionalidad HTTP necesaria para comunicarse con Sling. Esta configuración especifica la biblioteca que se enviará al [!DNL InDesign Server] para usar allí.

La variable `ThumbnailExport.jsx` la secuencia de comandos ejecutada por el paso del flujo de trabajo Extracción de medios genera una representación en miniatura en formato de JPG. Esta representación la utiliza el paso del flujo de trabajo Procesar miniaturas para generar las representaciones estáticas requeridas por [!DNL Experience Manager].

Puede configurar el paso del flujo de trabajo Procesar miniaturas para generar representaciones estáticas de diferentes tamaños. Asegúrese de que no elimina los valores predeterminados, ya que los necesita el [!DNL Experience Manager Assets] interfaz. Por último, el paso Eliminar representación de vista previa de imagen del flujo de trabajo elimina la representación de JPG en miniatura, ya que ya no es necesaria.

#### Extracción de páginas {#page-extraction}

Esto crea un [!DNL Experience Manager] de los elementos extraídos. Un controlador de extracción se utiliza para extraer datos de una representación (actualmente HTML o IDML). Estos datos se utilizan para crear una página con PageBuilder.

Para personalizar, puede editar la pestaña **[!UICONTROL Argumentos]** del paso **[!UICONTROL Extracción de página]**.

![imagen_1-96](assets/chlimage_1-289.png)

* **Controlador de extracción de página**: En la lista emergente, seleccione el controlador que desee utilizar. Un controlador de extracción funciona en una representación específica, elegida por un elemento relacionado `RenditionPicker` (consulte la API `ExtractionHandler`).
En un [!DNL Experience Manager] instalación: está disponible lo siguiente:
   * Controlador de extracción de exportación IDML: Funciona en la variable `IDML` representación generada en el paso MediaExtract .

* **Nombre de la página**: Especifique el nombre que desea asignar a la página resultante. Si se deja en blanco, el nombre es &quot;página&quot; (o una derivada si ya existe &quot;página&quot;).

* **Título de página**: Especifique el título que desea asignar a la página resultante.

* **Ruta raíz de página**: Ruta a la ubicación raíz de la página resultante. Si se deja en blanco, se utilizará el nodo que contiene las representaciones del recurso.

* **Plantilla de página**: La plantilla que se utilizará al generar la página resultante.

* **Diseño de página**: El diseño de página que se utilizará al generar la página resultante.

### Configurar el trabajador proxy para [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>El trabajador reside en la instancia de proxy.

1. En la consola Herramientas , expanda **[!UICONTROL Configuraciones de Cloud Services]** en el panel izquierdo. A continuación, expanda **[!UICONTROL Configuración de proxy en la nube]**.

1. Haga doble clic en el programa de **[!UICONTROL IDS de trabajo]** para abrirlo y configurarlo.

1. Haga clic en **[!UICONTROL Editar]** para abrir el cuadro de diálogo de configuración y definir los ajustes necesarios:

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **Grupo de ID**
Los puntos de conexión SOAP que se utilizarán para la comunicación con el [!DNL InDesign Server]. Puede agregar, quitar y ordenar los elementos que sean necesarios.

1. Haga clic en Aceptar para guardar.

### Configurar el externalizador de vínculos de CQ de día {#configuring-day-cq-link-externalizer}

Si la variable [!DNL InDesign Server] y [!DNL Experience Manager] están en diferentes hosts o una o ambas aplicaciones no funcionan en puertos predeterminados y, a continuación, configure [!UICONTROL Externalizador de vínculos de CQ de día] para establecer el nombre de host, el puerto y la ruta de contenido para la variable [!DNL InDesign Server].

1. Acceda a la consola web en `https://[aem_server]:[port]/system/console/configMgr`.
1. Localizar la configuración **[!UICONTROL Externalizador de vínculos de CQ de día]**. Haga clic en **[!UICONTROL Editar]** para abrir.
1. La configuración del externalizador de vínculos ayuda a crear direcciones URL absolutas para [!DNL Experience Manager] implementación y para [!DNL InDesign Server]. Uso **[!UICONTROL Dominios]** para especificar el nombre de host de la variable [!DNL Adobe InDesign Server]. Haga clic en **Guardar**.

   En direcciones URL absolutas, utilice `localhost` como nombre de host para la instancia local (de autor) y nombre de host o dirección IP para la instancia de publicación, como se muestra en la siguiente ilustración.

   ![Configuración del externalizador de vínculos](assets/link-externalizer-config.png)

### Habilitar procesamiento de trabajos paralelo para [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

Ahora puede habilitar el procesamiento paralelo de trabajos para IDS. Determinar el número máximo de trabajos paralelos (`x`) y [!DNL InDesign Server] puede procesar:

* En una sola máquina multiprocesador, el número máximo de trabajos paralelos (`x`) que [!DNL InDesign Server] puede procesar es uno menos que el número de procesadores que ejecutan IDS.
* Cuando ejecute IDS en varios equipos, deberá contar el número total de procesadores disponibles (es decir, en todos los equipos) y restar el número total de equipos.

Para configurar el número de trabajos de ID paralelos:

1. Abra el **[!UICONTROL Configuraciones]** ficha de la Consola Felix; por ejemplo: `https://[aem_server]:[port]/system/console/configMgr`.

1. Seleccione la cola de procesamiento de IDS en `Apache Sling Job Queue Configuration`.

1. Configurar:

   * **Tipo** - `Parallel`
   * **Trabajos paralelos máximos** - `<*x*>` (tal como se ha calculado anteriormente)

1. Guarde estos cambios.
1. Para habilitar la compatibilidad con varias sesiones para Adobe CS6 y posteriores, marque `enable.multisession.name` casilla de verificación, en `com.day.cq.dam.ids.impl.IDSJobProcessor.name` configuración.
1. Cree un [grupo de `x` Trabajadores de IDS añadiendo extremos SOAP a la configuración de IDS Worker](#configuring-the-proxy-worker-for-indesign-server).

   Si hay varios equipos en ejecución [!DNL InDesign Server], añada extremos SOAP (número de procesadores por máquina -1) para cada máquina.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>Al trabajar con un grupo de trabajadores, puede habilitar la lista de bloqueados de los trabajadores de IDS.
>
>Para ello, habilite el **[!UICONTROL enable.retry.name]** en la `com.day.cq.dam.ids.impl.IDSJobProcessor.name` , que habilita las recuperaciones de trabajos de IDS.
>
>Además, en la sección `com.day.cq.dam.ids.impl.IDSPoolImpl.name` configuración, establezca un valor positivo para `max.errors.to.blacklist` que determina el número de recuperaciones de trabajos antes de prohibir un ID en la lista de controladores de trabajos.
>
>De forma predeterminada, después de la etiqueta configurable (`retry.interval.to.whitelist.name`) tiempo en minutos en que se vuelve a validar el programa de trabajo de IDS. Si el trabajador se encuentra en línea, se elimina de la lista de bloqueados.

## Habilite la compatibilidad con [!DNL InDesign Server] 10.0 o posterior {#enabling-support-for-indesign-server-or-later}

Para [!DNL InDesign Server] 10.0 o superior, realice los siguientes pasos para habilitar la compatibilidad con varias sesiones.

1. Abra el Administrador de configuración desde su [!DNL Experience Manager Assets] instancia `https://[aem_server]:[port]/system/console/configMgr`.
1. Editar la configuración `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Seleccione el **[!UICONTROL ids.cc.enable]** y haga clic en **[!UICONTROL Guardar]**.

>[!NOTE]
>
>Para [!DNL InDesign Server] integración con [!DNL Experience Manager Assets], utilice un procesador multi-core porque la función de soporte de sesión necesaria para la integración no es compatible con sistemas de un solo núcleo.

## Configurar [!DNL Experience Manager] credenciales {#configure-aem-credentials}

Puede cambiar las credenciales de administrador predeterminadas (nombre de usuario y contraseña) para acceder al [!DNL InDesign Server] de su [!DNL Experience Manager] implementación sin romper la integración con [!DNL InDesign Server].

1. Vaya a `/etc/cloudservices/proxy.html`.
1. En el cuadro de diálogo, especifique el nuevo nombre de usuario y contraseña.
1. Guarde las credenciales.

>[!MORELIKETHIS]
>
>* [Acerca de Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

