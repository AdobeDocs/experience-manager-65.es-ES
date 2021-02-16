---
title: Carpeta vigilada en AEM Forms
seo-title: Carpeta vigilada en AEM Forms
description: Un administrador puede poner una carpeta a la vista y inicio de una operación de flujo de trabajo, servicio o secuencia de comandos cuando se coloca un archivo en la carpeta que se está viendo.
seo-description: Un administrador puede poner una carpeta a la vista y inicio de una operación de flujo de trabajo, servicio o secuencia de comandos cuando se coloca un archivo en la carpeta que se está viendo.
uuid: 39eac0fd-8212-46ff-b75d-8b4320d448a9
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: db38972c-be3f-49fd-8cc1-45b16ed244af
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '7153'
ht-degree: 0%

---


# Carpeta vigilada en AEM Forms{#watched-folder-in-aem-forms}

Un administrador puede configurar una carpeta de red, conocida como carpeta vigilada, de modo que cuando un usuario coloque un archivo (como un archivo PDF) en la carpeta vigilada, se inicie una operación de flujo de trabajo, servicio o secuencia de comandos preconfigurada para procesar el archivo agregado. Una vez que el servicio realiza la operación especificada, guarda el archivo de resultados en una carpeta de salida especificada. Para obtener más información sobre el flujo de trabajo, el servicio y la secuencia de comandos, consulte [Varios métodos para procesar archivos](#variousmethodsforprocessingfiles).

## Crear una carpeta vigilada {#create-a-watched-folder}

Puede utilizar uno de los siguientes métodos para crear una carpeta vigilada en el sistema de archivos:

* Mientras configura las propiedades de un nodo de configuración Carpeta vigilada, escriba la ruta completa del directorio principal en la propiedad folderPath y anexe el nombre de la Carpeta vigilada que se creará, como se muestra en el siguiente ejemplo: `C:/MyPDFs/MyWatchedFolder`
El 
`MyWatchedFolder`no existe, AEM Forms intenta crear la carpeta en la ruta especificada.

* Cree una carpeta en el sistema de archivos antes de configurar un extremo de Carpeta vigilada y, a continuación, proporcione la ruta completa en la propiedad folderPath. Para obtener información detallada sobre la propiedad folderPath, consulte [Propiedades de la carpeta vigilada](#watchedfolderproperties).

>[!NOTE]
>
>En un entorno agrupado, la carpeta utilizada como carpeta vigilada debe ser accesible, grabable y compartida en el sistema de archivos o la red. Cada instancia de servidor de aplicaciones del clúster debe tener acceso a la misma carpeta compartida. En Windows, cree una unidad de red asignada en todos los servidores y especifique la ruta de la unidad de red asignada en la propiedad folderPath.

## Crear nodo de configuración de carpeta vigilada {#create-watched-folder-configuration-node}

Para configurar una carpeta vigilada, cree un nodo de configuración Carpeta vigilada. Realice los siguientes pasos para crear el nodo de configuración:

1. Inicie sesión en la lista CRX-DE como administrador y vaya a la carpeta /etc/fd/watchfolder/config.

1. Cree un nodo de tipo `nt:unstructured`. Por ejemplo, watchedfolder

   >[!NOTE]
   >
   >El nombre del nodo Carpeta vigilada no puede incluir espacios ni caracteres especiales.

1. Añada las siguientes propiedades en el nodo:

   * `folderPath`
   * `inputProcessorType`
   * `inputProcessorId`
   * `outputFilePattern`

   Para obtener una lista completa de las propiedades admitidas, consulte [Propiedades de la carpeta vigilada](#watchedfolderproperties).

1. Haga clic en **Guardar todo**. Después de crear el nodo y guardar las propiedades. Las carpetas `input`, `result`, `failure`, `preserve` y `stage`se crean en la ruta especificada en la propiedad `folderPath`.

   Los inicios de trabajo de análisis que analizan la carpeta vigilada en un intervalo de tiempo definido.

## Propiedades de la carpeta vigilada {#watchedfolderproperties}

Puede configurar las siguientes propiedades para una carpeta vigilada.

* **folderPath (String)**: Ruta de la carpeta que se va a analizar en intervalos de tiempo definidos. Para un entorno en clúster, la carpeta debe estar en una ubicación compartida con todos los servidores que tengan acceso completo al servidor. Es una propiedad obligatoria.
* **inputProcessorType (String)**: Tipo de proceso que se va a inicio. Puede especificar el flujo de trabajo, la secuencia de comandos o el servicio. Es una propiedad obligatoria.
* **inputProcessorId (String)**: El comportamiento de la propiedad inputProcessorId se basa en el valor especificado para la propiedad inputProcessorType. Es una propiedad obligatoria. La siguiente lista detalla todos los valores posibles de la propiedad inputProcessorType y los requisitos correspondientes para la propiedad inputProcessorType:

   * Para el flujo de trabajo, especifique el modelo de flujo de trabajo que se va a ejecutar. Por ejemplo, /etc/workflow/models/&lt;nombre_de_workflow>/jcr:content/model
   * Para la secuencia de comandos, especifique la ruta de JCR de la secuencia de comandos que se va a ejecutar. Por ejemplo, /etc/fd/watchfolder/test/testScript.ecma
   * Para el servicio, especifique el filtro utilizado para localizar un servicio OSGi. El servicio está registrado como una implementación de la interfaz com.adobe.aemfd.watchfolder.service.api.ContentProcessor.

* **runModes (String)**: Lista separada por comas de los modos de ejecución permitidos para la ejecución del flujo de trabajo. Algunos ejemplos son:

   * author

   * instancias de publicación

   * creación, publicación

   * publicar, autor

>[!NOTE]
>
>Si el servidor que aloja la carpeta vigilada no tiene ninguno de los modos de ejecución especificados, la carpeta vigilada siempre se activa independientemente de los modos de ejecución del servidor.

* **outputFilePattern (String)**: Patrón del archivo de salida. Puede especificar una carpeta o un patrón de archivos. Si se especifica un patrón de carpetas, los archivos de salida tienen nombres como se describe en flujos de trabajo. Si se especifica un patrón de archivos, los archivos de salida tienen nombres como se describe en el patrón de archivos. [El ](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) patrón de archivos y carpetas también puede especificar una estructura de directorio para los archivos de salida. Es una propiedad obligatoria.

* **stageFileExpirationDuration (Long, predeterminado -1)**: El número de segundos que hay que esperar antes de que un archivo o carpeta de entrada que ya se ha seleccionado para el procesamiento se considere como si se hubiera agotado el tiempo de espera y se hubiera marcado como un error. Este mecanismo de caducidad solo se activa cuando el valor de esta propiedad es un número positivo.

>[!NOTE]
>
>Incluso cuando una entrada se marca como si se hubiera agotado el tiempo de espera con este mecanismo, puede que se esté procesando en segundo plano pero tardando más tiempo del esperado. Si el contenido de entrada se consumió antes de que se iniciara el mecanismo de tiempo de espera, el procesamiento podría incluso completarse más tarde y la salida se volcaría a la carpeta de resultados. Si el contenido no se consumió antes de que se agotara el tiempo de espera, es muy probable que se produzca un error en el procesamiento al intentar consumir el contenido, y este error también se registrará en la carpeta de errores para la misma entrada. Por otra parte, si el procesamiento de la entrada nunca se activó debido a un error intermitente en el trabajo o el flujo de trabajo (que es el escenario que el mecanismo de caducidad pretende abordar), entonces, por supuesto, no se producirá ninguna de estas dos eventualidades. Por lo tanto, para todas las entradas de la carpeta de errores que se marcaron como errores debido a un tiempo de espera (busque los mensajes del formulario &quot;Archivo no procesado después de un tiempo significativo, marcando como error!&quot; en el registro de errores), es aconsejable analizar la carpeta de resultados (y también la propia carpeta de errores para buscar otra entrada para la misma entrada) a fin de comprobar si se ha producido alguna de las eventualidades descritas anteriormente.

* **deleteExpiredStageFileOnlyWhenThrottled (Boolean, valor predeterminado true):** Si el mecanismo de caducidad solo debe activarse cuando se reduce la carpeta de inspección. El mecanismo es más relevante para las carpetas de inspección con limitación, ya que un pequeño número de archivos que permanecen en un estado no procesado (debido a errores intermitentes en el trabajo o el flujo de trabajo) pueden dificultar el procesamiento de todo el lote cuando se habilita la limitación. Si esta propiedad se mantiene como true (valor predeterminado), el mecanismo de caducidad no se activará para las carpetas de inspección que no estén restringidas. Si la propiedad se mantiene como false, el mecanismo siempre se activará siempre que la propiedad stageFileExpirationDuration sea un número positivo.

* **pollInterval (Long)**: Intervalo en segundos para analizar la información de la carpeta vigilada. A menos que se habilite la configuración de aceleración, el intervalo de encuesta debe ser mayor que el tiempo para procesar un trabajo promedio; de lo contrario, el sistema podría estar sobrecargado. El valor predeterminado es 5. Consulte la descripción del tamaño del lote para obtener más información. El valor del intervalo de encuesta debe ser bueno o igual a uno.
* **excludeFilePattern (String)**: Una lista delimitada por punto y coma (;) de patrones que utiliza una carpeta vigilada para determinar qué archivos y carpetas se deben analizar y recoger. Ningún archivo o carpeta con este patrón se analiza para su procesamiento. Esta opción resulta útil cuando la entrada es una carpeta con varios archivos. El contenido de la carpeta se puede copiar en una carpeta con un nombre que la carpeta vigilada recoge. Esto evita que la carpeta vigilada recoja una carpeta para procesarla antes de que la carpeta se copie completamente en la carpeta de entrada. El valor predeterminado es null.
Puede utilizar [patrones de archivo](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) para excluir:

   * Archivos con extensiones de nombre de archivo específicas; por ejemplo, *.dat, *.xml, .pdf, *.*
   * Archivos con nombres específicos; por ejemplo, data* excluiría archivos y carpetas con el nombre data1, data2, etc.
   * Archivos con expresiones compuestas en el nombre y la extensión, como en estos ejemplos:

      * Data[0-9][0-9][0-9].[dD][aA]&#39;puerto&#39;
      * *.[dD][Aa]&#39;puerto&#39;
      * *.[Xx][Mm][Ll]

Para obtener más información sobre los patrones de archivo, consulte [Acerca de los patrones de archivo](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

* **includeFilePattern (String)**: Una lista delimitada por punto y coma (;) de patrones que utiliza la carpeta vigilada para determinar qué carpetas y archivos se deben analizar y recoger. Por ejemplo, si IncludeFilePattern es input*, se recogen todos los archivos y carpetas que coinciden con input*. Esto incluye archivos y carpetas denominados input1, input2, etc. El valor predeterminado es * e indica todos los archivos y carpetas. Puede utilizar patrones de archivo para incluir:

   * Archivos con extensiones de nombre de archivo específicas; por ejemplo, *.dat, *.xml, .pdf, *.*
   * Archivos con nombres específicos; por ejemplo, datos.* incluiría archivos y carpetas denominados data1, data2, etc.

* Archivos con expresiones compuestas en el nombre y la extensión, como en estos ejemplos:

   * Data[0-9][0-9][0-9].[dD][aA]&#39;puerto&#39;

      * *.[dD][Aa]&#39;puerto&#39;
      * *.[Xx][Mm][Ll]

Para obtener más información sobre los patrones de archivos, consulte [Acerca de los patrones de archivos](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)

* **waitTime (Long)**: Tiempo, en milisegundos, que debe esperarse antes de analizar una carpeta o archivo después de crearlo. Por ejemplo, si el tiempo de espera es de 3.600.000 milisegundos (una hora) y el archivo se creó hace un minuto, este archivo se recuperará después de que hayan transcurrido 59 minutos o más. El valor predeterminado es 0. Esta configuración es útil para asegurarse de que un archivo o carpeta se copia completamente en la carpeta de entrada. Por ejemplo, si tiene un archivo grande que procesar y el archivo tarda diez minutos en descargarse, establezca el tiempo de espera en 10*60 *1000 milisegundos. Esto evita que la carpeta vigilada analice el archivo si no tiene diez minutos de antigüedad.
* **purgeDuration (Long)**: Los archivos y carpetas de la carpeta de resultados se purgan cuando son anteriores a este valor. Este valor se mide en días. Esta configuración es útil para garantizar que la carpeta de resultados no se llena. Un valor de -1 días indica que nunca se elimina la carpeta de resultados. El valor predeterminado es -1.
* **resultFolderName (String)**: Carpeta donde se almacenan los resultados guardados. Si los resultados no aparecen en esta carpeta, compruebe la carpeta de errores. Los archivos de sólo lectura no se procesan y se guardan en la carpeta de errores. Este valor puede ser una ruta absoluta o relativa con los siguientes patrones de archivo:

   * %F = prefijo de nombre de archivo
   * %E = extensión de nombre de archivo
   * %Y = año (completo)
   * %y = año (dos últimos dígitos)
   * %M = mes
   * %D = día del mes
   * %d = día del año
   * %H = hora (reloj de 24 horas)
   * %h = hora (reloj de 12 horas)
   * %m = minuto
   * %s = segundo
   * %l = milisegundo
   * %R = número aleatorio (entre 0 y 9)
   * %P = id. de proceso o trabajo

   Por ejemplo, si es a las 8 pm del 17 de julio de 2009 y especifica C:/Test/WF0/fail/%Y/%M/%D/%H/, la carpeta de resultados es C:/Test/WF0/fail/2009/07/17/20

   Si la ruta no es absoluta sino relativa, la carpeta se crea dentro de la carpeta vigilada. El valor predeterminado es result/%Y/%M/%D/, que es la carpeta Result dentro de la carpeta Watched. Para obtener más información sobre los patrones de archivo, consulte [Acerca de los patrones de archivo](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

>[!NOTE]
>
>Cuanto menor sea el tamaño de las carpetas resultantes, mejor será el rendimiento de la carpeta vigilada. Por ejemplo, si la carga estimada para la carpeta vigilada es de 1000 archivos por hora, pruebe un patrón como result/%Y%M%D%H para que se cree una nueva subcarpeta cada hora. Si la carga es más pequeña (por ejemplo, 1000 archivos por día), puede usar un patrón como result/%Y%M%D.

* **failFolderName (String)**: Carpeta donde se guardan los archivos de error. Esta ubicación siempre es relativa a la carpeta vigilada. Puede utilizar patrones de archivo, como se describe en Carpeta de resultados. Los archivos de sólo lectura no se procesan y se guardan en la carpeta de errores. El valor predeterminado es error/%Y/%M/%D/.
* **preserveFolderName (String):** la ubicación en la que se almacenan los archivos tras procesarlos correctamente. La ruta puede ser absoluta, relativa o nula. Puede utilizar patrones de archivo, como se describe en Carpeta de resultados. El valor predeterminado es preserve/%Y/%M/%D/.
* **batchSize (Long)**: Número de archivos o carpetas que se van a buscar por análisis. Utilícelo para evitar una sobrecarga en el sistema; el análisis de demasiados archivos al mismo tiempo puede provocar un bloqueo. El valor predeterminado es 2.

   La configuración Intervalo de encuesta y Tamaño de lote determina cuántos archivos se han visto en cada análisis. Watched Folder utiliza un grupo de subprocesos de Quartz para analizar la carpeta de entrada. El grupo de subprocesos se comparte con otros servicios. Si el intervalo de exploración es pequeño, los subprocesos analizan la carpeta de entrada con frecuencia. Si los archivos se sueltan con frecuencia en la carpeta vigilada, debe reducir el intervalo de exploración. Si los archivos se retiran con poca frecuencia, utilice un intervalo de exploración mayor para que los demás servicios puedan utilizar los subprocesos.

   Si se está extrayendo un gran volumen de archivos, haga que el tamaño del lote sea grande. Por ejemplo, si el servicio iniciado por el extremo de la carpeta vigilada puede procesar 700 archivos por minuto y los usuarios colocan los archivos en la carpeta de entrada a la misma velocidad, al establecer el tamaño del lote en 350 y el intervalo de encuesta en 30 segundos se ayuda a observar el rendimiento de la carpeta sin incurrir en el costo de analizar la carpeta vigilada con demasiada frecuencia.

   Cuando los archivos se colocan en la carpeta vigilada, se lista la entrada de los archivos, lo que puede reducir el rendimiento si se realiza el análisis cada segundo. El aumento del intervalo de exploración puede mejorar el rendimiento. Si el volumen de archivos que se van a soltar es pequeño, ajuste el tamaño del lote y el intervalo de encuesta en consecuencia. Por ejemplo, si se pierden 10 archivos cada segundo, intente establecer el intervalo de encuesta en 1 segundo y el tamaño del lote en 10

* **throttleOn (Boolean)**: Cuando esta opción está seleccionada, limita el número de trabajos de carpetas vigiladas que AEM Forms procesa en un momento dado. El número máximo de trabajos viene determinado por el valor Tamaño de lote. El valor predeterminado es true. (Consulte [Acerca de la limitación](../../forms/using/watched-folder-in-aem-forms.md#p-about-throttling-p).)

* **overwriteDuplicateFilename (Boolean)**: Cuando se establece en True, se sobrescriben los archivos de la carpeta de resultados y la carpeta de preservación. Cuando se establece en False, se utilizan para el nombre archivos y carpetas con un sufijo de índice numérico. El valor predeterminado es False.
* **preserveOnFailure (Boolean)**: Preservar archivos de entrada en caso de error al ejecutar la operación en un servicio. El valor predeterminado es true.
* **inputFilePattern (String)**: Especifica el patrón de los archivos de entrada para una carpeta vigilada. Crea una lista de permitidos de los archivos.
* **asynch (booleano)**: Identifica el tipo de invocación como asíncrono o sincrónico. El valor predeterminado es true (asincrónico). El procesamiento de archivos es una tarea que consume recursos, mantenga el valor del indicador asincrónico en true para evitar que se ahogue el subproceso principal del trabajo de digitalización. En un entorno agrupado, es fundamental mantener el indicador verdadero para habilitar el equilibrio de carga para los archivos que se procesan en los servidores disponibles. Si el indicador es false, el trabajo de análisis intenta realizar el procesamiento de cada archivo o carpeta de nivel superior secuencialmente dentro de su propio subproceso. No establezca el indicador en false sin un motivo específico, como el procesamiento basado en flujos de trabajo en una configuración de un solo servidor.

>[!NOTE]
>
>Por diseño, los flujos de trabajo son asincrónicos. Incluso si establece el valor en false, los flujos de trabajo se inician en el modo asincrónico.

* **enabled (Boolean)**: Desactiva y activa la búsqueda de una carpeta vigilada. Establezca enabled en true para que el inicio analice la carpeta vigilada. El valor predeterminado es true.
* **payloadMapperFilter:** cuando una carpeta se configura como carpeta vigilada, se crea una estructura de carpetas dentro de la carpeta vigilada. La estructura tiene carpetas para proporcionar entradas, recibir resultados, guardar datos para fallos, conservar datos para procesos de larga duración y guardar datos para diversas etapas. La estructura de carpetas de una carpeta vigilada puede servir como carga útil de flujos de trabajo centrados en Forms. Un asignador de carga útil permite definir la estructura de una carga útil que utiliza una carpeta vigilada para entrada, salida y procesamiento. Por ejemplo, si utiliza el asignador predeterminado, asigna el contenido de la carpeta vigilada con [carga útil]\input y [carga útil]\output. Hay dos implementaciones de mapeador de carga útil integradas disponibles. Si no tiene [una implementación personalizada](../../forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter), utilice una implementación lista para usar:

   * **Asignador predeterminado:** utilice el asignador de carga útil predeterminado para mantener el contenido de entrada y salida de las carpetas vigiladas en carpetas de entrada y salida independientes en la carga útil. Además, en la ruta de carga útil de un flujo de trabajo, utilice [carga útil]/input/ y [carga útil]/rutas de salida para recuperar y guardar contenido.

   * **Asignador de carga útil simple basado en archivos:** utilice el asignador de carga útil simple basado en archivos para mantener el contenido de entrada y salida directamente en la carpeta de carga útil. No crea ninguna jerarquía adicional, como el asignador predeterminado.

### Parámetros de configuración personalizados {#custom-configuration-parameters}

Junto con las propiedades de configuración de la carpeta vigilada que se muestran más arriba, también puede especificar parámetros de configuración personalizados. Los parámetros personalizados se pasan al código de procesamiento de archivos. Permite que el código cambie su comportamiento en función del valor del parámetro. Para especificar un parámetro:

1. Inicie sesión en CRXDE-Lite y vaya al nodo de configuración Carpeta vigilada.
1. Añada un parámetro de propiedad.&lt;property_name> al nodo de configuración Carpeta vigilada. El tipo de propiedad solo puede ser Boolean, Date, Decimal, Doble, Long y String. Puede especificar propiedades de uno o varios valores.

>[!NOTE]
>
>Si el tipo de datos de la propiedad es Doble, especifique un punto decimal en el valor de dichas propiedades. Para todas las propiedades, donde el tipo de datos es Doble y no se especifica ninguna coma decimal en el valor, el tipo se convierte a Long.

Estas propiedades se pasan como un mapa inmutable de tipo Map&lt;String, Object> al código de procesamiento. El código de procesamiento puede ser un ECMAScript, un flujo de trabajo o un servicio. Los valores proporcionados para las propiedades están disponibles como pares clave-valor en el mapa. Key es el nombre de la propiedad y value es el valor de la propiedad. Para obtener más información sobre los parámetros de configuración personalizados, consulte la siguiente imagen:

![Un nodo de configuración de carpeta de inspección de muestra con propiedades obligatorias, algunas propiedades opcionales, algunos parámetros de configuración](assets/custom-configuration-parameters.png)

Un nodo de configuración de carpeta de inspección de muestra con propiedades obligatorias, unas pocas propiedades opcionales, unos pocos parámetros de configuración.

#### Variables mutables para flujos de trabajo {#mutable-variables-for-workflows}

Puede crear variables múltiples para métodos de procesamiento de archivos basados en flujos de trabajo. Estas variables sirven como contenedores para los datos que fluyen entre los pasos de un flujo de trabajo. Para crear dichas variables:

1. Inicie sesión en CRXDE-Lite y vaya al nodo de configuración Carpeta vigilada.

1. Añada una propiedad workflow.var.&lt;variable_name> al nodo de configuración Carpeta vigilada.

   El tipo de propiedad solo puede ser Boolean, Date, Decimal, Doble, Long y String. También se admiten propiedades de varios valores. Para propiedades de varios valores, el valor disponible para el paso de flujo de trabajo es una matriz de un tipo especificado.

   >[!NOTE]
   >
   >Si el tipo de datos de la propiedad es Doble, especifique un punto decimal en el valor de dichas propiedades. Para todas las propiedades, donde el tipo de datos es Doble y no se especifica ninguna coma decimal en el valor, el tipo se convierte a Long.

>[!NOTE]
>
>La especificación JCR establece un valor predeterminado para las propiedades. Los valores predeterminados están disponibles para los pasos de un flujo de trabajo para su procesamiento. Por lo tanto, especifique los valores predeterminados adecuados.

![custom-configuration-parameters2](assets/custom-configuration-parameters2.png)

## Varios métodos para procesar archivos {#variousmethodsforprocessingfiles}

Puede inicio de un flujo de trabajo, un servicio o una secuencia de comandos para procesar los documentos colocados en una carpeta de inspección.

### Uso de un servicio para procesar archivos de una carpeta vigilada   {#using-a-service-to-process-files-of-a-watched-folder-nbsp}

Un servicio es una implementación personalizada de la interfaz `com.adobe.aemfd.watchfolder.service.api.ContentProcessor`. Está registrado con OSGi junto con algunas propiedades personalizadas. Las propiedades personalizadas de la implementación la hacen única y ayudan a identificar la implementación.

#### Implementación personalizada de la interfaz ContentProcessor {#custom-implementation-of-the-contentprocessor-interface}

La implementación personalizada acepta un contexto de procesamiento (un objeto de tipo com.adobe.aemfd.watchfolder.service.api.ProcessorContext), lee documentos de entrada y parámetros de configuración desde el contexto, procesa las entradas y agrega el resultado nuevamente al
contexto. ProcessorContext tiene las siguientes API:

* **getWatchFolderId**: Devuelve el ID de la carpeta vigilada.
* **getInputMap**: Devuelve un mapa de tipo Map. Las claves del mapa son el nombre del archivo de entrada y un objeto documento que contiene el contenido del archivo. Utilice la API getinputMap para leer los archivos de entrada.
* **getConfigParameters**: Devuelve un mapa inmutable de tipo Map. El mapa contiene
los parámetros de configuración de una carpeta vigilada.

* **setResult**: La implementación ContentProcessor utiliza la API para escribir el documento de salida en la carpeta de resultados. Puede proporcionar un nombre para el archivo de salida a la API setResult. La API puede elegir usar o ignorar el archivo proporcionado según el patrón de carpeta o archivo de salida especificado. Si se especifica un patrón de carpetas, los archivos de salida tienen nombres como se describe en flujos de trabajo. Si se especifica un patrón de archivos, los archivos de salida tienen nombres como se describe en el patrón de archivos.

Por ejemplo, el siguiente código es una implementación personalizada de la interfaz ContentProcessor con una propiedad foo=bar personalizada.

```java
@Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
@Service(value = {OutputWriter.class, ContentProcessor.class})
@Property(name = "foo", value = "bar")
public class OutputWriter implements ContentProcessor {
```

Mientras [configura una carpeta vigilada](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p), si especifica la propiedad inputProcessorId como (foo=bar) y la propiedad inputProcessorType como Servicio, se utilizará el servicio mencionado anteriormente (implementación personalizada) para procesar los archivos de entrada de la carpeta vigilada.

El siguiente ejemplo es también una implementación personalizada de la interfaz ContentProcessor. En el ejemplo, el servicio acepta archivos de entrada, los copia en una ubicación temporal y devuelve un objeto documento con el contenido del archivo. El contenido del objeto documento se guarda en la carpeta de resultados. La ruta física de la carpeta de resultados se configura en el nodo de configuración [Carpeta vigilada](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

```java
@Component(immediate = true)
@Service(value = ContentProcessor.class)
@Property(name = "serviceSelector", value = "testProcessor1")
public class TestContentProcessor1 implements ContentProcessor {
    @Override
    public void processInputs(ProcessorContext context) throws Exception {
        Map.Entry<String, Document> e = context.getInputMap().entrySet().iterator().next();
        File f = new File((String) context.getConfigParameters().get("tempDir"),
                context.getConfigParameters().get("outPrefix") + e.getKey());
        e.getValue().copyToFile(f);
        context.setResult(f.getName(), new Document(f, true));
    }
}
```

### Uso de scripts para procesar archivos de una carpeta vigilada {#using-scripts-to-process-files-of-a-watched-folder}

Las secuencias de comandos son el código personalizado de reclamación de ECMAScript que se escribe para procesar documentos colocados en la carpeta vigilada. Una secuencia de comandos se representa como un nodo JCR. Aparte de las variables ECMAScript estándar (log, sling y más), el Script tiene una variable processorContext. La variable es del tipo ProcessorContext. ProcessorContext tiene las siguientes API:

* **getWatchFolderId**: Devuelve el ID de la carpeta vigilada.
* **getInputMap**: Devuelve un mapa de tipo Map. Las claves del mapa son el nombre del archivo de entrada y un objeto documento que contiene el contenido del archivo. Utilice la API getinputMap para leer los archivos de entrada.
* **getConfigParameters**: Devuelve un mapa inmutable de tipo Map. El mapa contiene los parámetros de configuración de una carpeta vigilada.
* **setResult**: La implementación ContentProcessor utiliza la API para escribir el documento de salida en la carpeta de resultados. Puede proporcionar un nombre para el archivo de salida a la API setResult. La API puede elegir usar o ignorar el archivo proporcionado según el patrón de carpeta o archivo de salida especificado. Si se especifica un patrón de carpetas, los archivos de salida tienen nombres como se describe en flujos de trabajo. Si se especifica un patrón de archivos, los archivos de salida tienen nombres como se describe en el patrón de archivos.

El siguiente código es un ejemplo de ECMAScript. Acepta archivos de entrada, copia los archivos en una ubicación temporal y devuelve un objeto documento con el contenido del archivo. El contenido del objeto documento se guarda en la carpeta de resultados. La ruta física de la carpeta de resultados se configura en el nodo de configuración [Carpeta vigilada](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

>[!NOTE]
>
>La carpeta de salida y el prefijo de nombre de archivo se deciden según los parámetros de configuración de la carpeta vigilada.

```java
var inputMap = processorContext.getInputMap();
var params = processorContext.getConfigParameters();
var entry = inputMap.entrySet().iterator().next();
var tempFile = new Packages.java.io.File(params.get("tempDir"), params.get("outPrefix") + entry.getKey());
entry.getValue().copyToFile(tempFile);
processorContext.setResult(tempFile.getName(), new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true));
```

#### Ubicación de scripts y consideraciones de seguridad {#location-of-scripts-and-security-considerations}

De forma predeterminada, se proporciona una carpeta de contenedor (/etc/fd/watchfolder/scripts) en la que los clientes pueden colocar sus scripts, y el usuario de servicios predeterminado que utiliza el módulo de carpetas de inspección tiene los permisos necesarios para leer scripts de esta ubicación.

Si planea colocar las secuencias de comandos en una ubicación personalizada, es probable que el usuario de servicios predeterminado no tenga permisos de lectura sobre la ubicación personalizada. Para este escenario, realice los siguientes pasos para proporcionar los permisos necesarios a la ubicación personalizada:

1. Cree un usuario del sistema mediante programación o mediante la consola https://&#39;[server]:[port]&#39;/crx/explorer. También puede utilizar un usuario del sistema existente. Es importante trabajar con los usuarios del sistema aquí en lugar de con los usuarios normales.
1. Proporcione permisos de lectura al usuario del sistema recién creado o existente en la ubicación personalizada donde se almacenan las secuencias de comandos. Puede tener varias ubicaciones personalizadas. Proporcione al menos permisos de lectura a todas las ubicaciones personalizadas.
1. En la consola de configuración Félix (/system/console/configMgr), busque la asignación de usuarios de servicios para las carpetas de inspección. Esta asignación se parece a &#39;Asignación: adobe-aemds-core-watch-folder=...&#39;.
1. Haga clic en la asignación. Para la entrada &#39;adobe-aemds-core-watch-folder:scripts=fd-service&#39;, cambie fd-service por el ID del usuario del sistema personalizado. Haga clic en Guardar.

Ahora puede utilizar la ubicación personalizada configurada para guardar las secuencias de comandos.

### Uso de un flujo de trabajo para procesar archivos de una carpeta vigilada {#using-a-workflow-to-process-files-of-a-watched-folder}

Los flujos de trabajo le permiten automatizar actividades de Experience Manager. Los flujos de trabajo constan de una serie de pasos que se ejecutan en un orden específico. Cada paso realiza una actividad distinta, como activar una página o enviar un mensaje de correo electrónico. Los flujos de trabajo pueden interactuar con los recursos del repositorio, las cuentas de usuario y los servicios de Experience Manager. Por lo tanto, los flujos de trabajo pueden coordinarse de forma complicada.

* Antes de crear un flujo de trabajo, tenga en cuenta los siguientes puntos:
* El resultado de un paso debe estar disponible para todos los pasos subsiguientes.
Los pasos deben poder actualizar (o incluso eliminar) los productos existentes generados por los pasos anteriores.
* Las variables múltiples se utilizan para el flujo de datos dinámicos personalizados entre los pasos.

Realice los siguientes pasos para procesar archivos mediante flujos de trabajo:

1. Cree una implementación de la interfaz `com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextProcessor`. Es similar a la implementación creada para un servicio.

   >[!NOTE]
   >
   >Puede crear la implementación completa completamente en ECMAScript.

1. En un paso de Flujo de trabajo, busque el servicio OSGi de tipo com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService y llame al método execute() del servicio con los siguientes argumentos.

   * Su implementación personalizada de la interfaz WorkflowContextProcessor
   * workItem
   * workflowSession
   * metadata

Si utiliza el lenguaje de programación Java para implementar el flujo de trabajo, el motor de flujos de trabajo AEM proporciona valor para variables workItem, workflowSession y metadata. Estas variables se pasan como argumentos al método execute() de la implementación de WorkflowProcess personalizada.

Si utiliza ECMAScript para implementar el flujo de trabajo, el motor de flujos de trabajo AEM proporciona valor para las variables graniteWorkItem, graniteWorkflowSession y metadata. Estas variables se pasan como argumentos al método WorkflowContextService.execute().

El argumento de processWorkflowContext() es un objeto de tipo com.adobe.aemfd.watchfolder.workflow.api.WorkflowContext. La interfaz WorkflowContext tiene las siguientes API para facilitar las consideraciones específicas del flujo de trabajo mencionadas anteriormente:

* getWorkItem: Devuelve el valor de la variable WorkItem. Las variables se pasan al método WorkflowContextService.execute().
* getWorkflowSession: Devuelve el valor de la variable WorkflowSession. Las variables se pasan al método WorkflowContextService.execute().
* getMetadata: Devuelve el valor de la variable de metadatos. Las variables se pasan al método WorkflowContextService.execute().
* getCommitVariables: Devuelve un mapa de objetos de sólo lectura que representa las variables establecidas por pasos anteriores. Si una variable no se modifica en ninguno de los pasos anteriores, se devuelve el valor predeterminado especificado durante la configuración de la carpeta vigilada.
* getCommitResults: Devuelve un mapa de Documento de sólo lectura. El mapa representa los archivos de salida generados por los pasos anteriores.
* setVariable: La implementación WorkflowContextProcessor utiliza la variable para manipular las variables que representan los datos dinámicos personalizados que fluyen entre los pasos. El nombre y el tipo de las variables es idéntico al nombre de las variables especificadas durante la configuración de la carpeta vigilada](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p). [ Para cambiar el valor de una variable, llame a la API setVariable con un valor que no sea nulo. Para eliminar una variable, llame a setVariable() con un valor nulo.

También están disponibles las siguientes API de ProcessorContext:

* getWatchFolderId: Devuelve el ID de la carpeta vigilada.
* getInputMap: Devuelve un mapa de tipo Map&lt;String, Documento>. Las claves del mapa son el nombre del archivo de entrada y un objeto documento que contiene el contenido del archivo. Utilice la API getinputMap para leer los archivos de entrada.
* getConfigParameters: Devuelve un mapa inmutable de tipo Map&lt;String, Object>. El mapa contiene los parámetros de configuración de una carpeta vigilada.
* setResult: La implementación ContentProcessor utiliza la API para escribir el documento de salida en la carpeta de resultados. Puede proporcionar un nombre para el archivo de salida a la API setResult. La API puede elegir usar o ignorar el archivo proporcionado según el patrón de carpeta o archivo de salida especificado. Si se especifica un patrón de carpetas, los archivos de salida tienen nombres como se describe en flujos de trabajo. Si se especifica un patrón de archivos, los archivos de salida tienen nombres como se describe en el patrón de archivos

Consideración de la API setResult cuando se utiliza en flujos de trabajo:

* Para agregar un nuevo documento de salida que contribuya a la salida general del flujo de trabajo, llame a la API setResult con un nombre de archivo que no se haya utilizado como nombre de archivo de salida en ningún paso anterior.
* Para actualizar un resultado generado por un paso anterior, llame a la API setResult con un nombre de archivo ya utilizado por un paso anterior.
* Para eliminar un resultado generado por un paso anterior, llame a setResult con un nombre de archivo ya utilizado por un paso anterior y nulo como contenido.

>[!NOTE]
>
>Si se llama a la API setResult con contenido nulo en cualquier otro escenario, se producirá un error.

El siguiente ejemplo se implementa como un paso del flujo de trabajo. En el ejemplo, ECMAscript utiliza una variable stepCount para rastrear el número de veces que se llama a un paso en la instancia de flujo de trabajo actual.
El nombre de la carpeta de salida es una combinación del número de paso actual, el nombre del archivo original y el prefijo especificado en el parámetro outPrefix.

ECMAScript obtiene una referencia del servicio de contexto de flujo de trabajo y crea una implementación de la interfaz WorkflowContextProcessor. La implementación WorkflowContextProcessor acepta archivos de entrada, los copia en una ubicación temporal y devuelve un documento que representa el archivo copiado. En función del valor de la variable booleana purgePrevious, el paso actual elimina el resultado generado por última vez en el mismo paso cuando se inició el paso en la instancia de flujo de trabajo actual. Al final, se invoca el método wfSvc.execute para ejecutar la implementación WorkflowContextProcessor. El contenido del documento de salida se guarda en la carpeta de resultados en la ruta de acceso física mencionada en el nodo de configuración Carpeta vigilada.

```javascript
log.error("Watch-folder workflow script called for step: " + graniteWorkItem.getNode().getTitle());
var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
// Custom WorkflowContextProcessor implementation which defines the processWorkflowContext() method purely in JS
var impl = { processWorkflowContext: function (wfContext) {
    var wfId = wfContext.getWatchFolderId();
    var inputMap = wfContext.getInputMap();
    var paramMap = wfContext.getConfigParameters();
    var preResults = wfContext.getCommittedResults();
    var preVars = wfContext.getCommittedVariables();
    log.info("WF ID: " + wfId); // workflowId of type String
    log.info("Inputs: " + inputMap); // Input map of type Map<String, Document>
    log.info("Params: " + paramMap); // Config params of type Map<String, Object>
    log.info("Old results: " + preResults);
    log.info("Old variables: " + preVars);
    var currStepNumber = new Packages.java.lang.Long(new Packages.java.lang.Long(preVars.get("stepCount")).longValue() + 1);
    log.info("Current step number: " + currStepNumber);
    wfContext.setVariable("stepCount", currStepNumber);
    var entry = inputMap.entrySet().iterator().next();
    var tempFile = new Packages.java.io.File(paramMap.get("tempDir"), paramMap.get("outPrefix") + "STEP-" + currStepNumber + "-" + entry.getKey());
    entry.getValue().copyToFile(tempFile);
    var fName = tempFile.getName();
    var outDoc = new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true);
    wfContext.setResult(tempFile.getName(), outDoc);
    var prevStepOutName = paramMap.get("outPrefix") + "STEP-" + (currStepNumber - 1) + "-" + entry.getKey();
    if (preResults.containsKey(prevStepOutName) && paramMap.get("purgePrevious").booleanValue()) {
        log.info("Purging previous step output " + prevStepOutName);
        wfContext.setResult(prevStepOutName, null);
    }
} }
wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
log.info("Exiting workflow script!")
```

### Crear un filtro de asignador de carga útil para asignar la estructura de una carpeta vigilada a la carga útil de un flujo de trabajo {#create-payload-mapper-filter-to-map-structure-of-a-watched-folder-to-the-payload-of-a-workflow}

Cuando se crea una carpeta vigilada, se crea una estructura de carpetas dentro de la carpeta que se está viendo. La estructura de carpetas tiene carpetas de etapa, resultado, conservación, entrada y error. La estructura de carpetas puede servir como carga útil de entrada para el flujo de trabajo y aceptar resultados de un flujo de trabajo. También puede lista puntos de error, si los hay.

Si la estructura de una carga útil es diferente a la de la carpeta vigilada, puede escribir secuencias de comandos personalizadas para asignar la estructura de la carpeta vigilada a la carga útil. Esta secuencia de comandos se denomina filtro de mapeador de carga útil. De forma predeterminada, AEM Forms proporciona un filtro de mapeador de carga útil para asignar la estructura de la carpeta vigilada a una carga útil.

#### Creación de un filtro personalizado de asignador de carga útil {#creating-a-custom-payload-mapper-filter}

1. Descargue [SDK de cliente de Adobe](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aemfd/aemfd-client-sdk/6.3.0/aemfd-client-sdk-6.3.0.jar).
1. Configure el SDK de cliente en la ruta de compilación del proyecto basado en lotes. Para comenzar, puede descargar y abrir el siguiente proyecto basado en lotes en el IDE que desee.
1. Edite el código de filtro del asignador de carga útil disponible en el paquete de muestra para adaptarlo a sus necesidades.
1. Utilice maven para crear un paquete del filtro personalizado del asignador de carga útil.
1. Utilice [AEM consola de paquetes](https://localhost:4502/system/console/bundles) para instalar el paquete.

   Ahora, el filtro personalizado del asignador de carga útil aparece en AEM interfaz de usuario de la carpeta vigilada. Puede utilizarla con su flujo de trabajo.

   El siguiente código de ejemplo implementa un asignador simple basado en archivos para los archivos guardados en relación con una carga útil. Puede usarlo para empezar.

   ```java
   package com.adobe.aemfd.watchfolder.workflow;
   import com.adobe.aemfd.docmanager.Document;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.PayloadMapper;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowExecutionContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowInitializationContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowVariable;
   import com.adobe.granite.workflow.exec.Workflow;
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.ResourceResolver;
   import javax.jcr.Binary;
   import javax.jcr.Node;
   import java.util.Collection;
   import java.util.HashMap;
   import java.util.Map;
   @Component(immediate = true)
   @Service(value = PayloadMapper.class)
   public class SimpleFileBasedPayloadMapper implements PayloadMapper {
   @Override
   public Node createPayload(WorkflowInitializationContext wfInitCtxt, Node stagingFolder, String uniquePayloadName,
   Map<String, Binary> inputs, Collection<WorkflowVariable> variableDefs) throws Exception {
   Node dirNode = stagingFolder.addNode(uniquePayloadName, "sling:Folder");
   for (Map.Entry<String, Binary> bins: inputs.entrySet()) {
   Node fileNode = dirNode.addNode(bins.getKey(), "nt:file");
   Node resNode = fileNode.addNode ("jcr:content", "nt:resource");
   resNode.setProperty("jcr:data", bins.getValue());
   }
   return dirNode;
   }
   @Override
   public Map<String, Document> getInputs(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload, ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public void setOutput(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   String fileName, Binary contents, int outputMode) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getIntermediateOutputs(WorkflowInitializationContext wfInitCtxt,
   WorkflowExecutionContext wfExecCtxt, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getFinalOutputs(WorkflowInitializationContext wfInitCtxt, Workflow workflow, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   Map<String, Object> params = wfInitCtxt.getConfigParameters();
   Map<String, Document> result = new HashMap<String, Document>();
   for (Map.Entry<String, Object> me: params.entrySet()) {
   String key = me.getKey();
   if (key.startsWith("pm.outfile.")) {
   String fName = (String) me.getValue();
   Document d = new Document(payload.getPath() + "/" + fName, resourceResolver);
   result.put(fName, d);
   }
   }
   return result;
   }
   @Override
   public void setVariable(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   WorkflowVariable variable) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Object> getVariables(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   }
   ```

## Cómo interactúan los usuarios con una carpeta vigilada {#how-users-interact-with-a-watched-folder}

Para un extremo de carpeta vigilada, los usuarios pueden realizar inicios en las operaciones de procesamiento de archivos copiando o arrastrando archivos de entrada o carpetas de sus escritorios a una carpeta vigilada. Los archivos se procesan en el orden de llegada.

Para los extremos de carpetas vigiladas, si un trabajo solo requiere un archivo de entrada, el usuario puede copiar ese archivo en la raíz de la carpeta vigilada.

Si el trabajo contiene más de un archivo de entrada, el usuario debe crear una carpeta fuera de la jerarquía de carpetas vigiladas que contenga todos los archivos necesarios. Esta nueva carpeta debe incluir los archivos de entrada (y opcionalmente un archivo DDX si el proceso lo requiere). Una vez construida la carpeta de trabajo, el usuario la copia en la carpeta de entrada de la carpeta Watched.

>[!NOTE]
>
>Asegúrese de que el servidor de aplicaciones ha eliminado el acceso a los archivos en la carpeta vigilada. Si AEM Forms no puede eliminar los archivos de la carpeta de entrada después de analizarlos, el proceso asociado se iniciará indefinidamente.

## Información adicional sobre las carpetas vigiladas {#additional-information-about-the-watched-folders}

### Acerca de la limitación {#about-throttling}

Cuando la limitación está habilitada para un extremo de carpeta de inspección, limita el número de trabajos de carpeta de inspección que se procesan en un momento dado. El número máximo de trabajos está determinado por el valor Tamaño de lote, también configurable en el extremo Carpeta vigilada. Cuando se alcanza el límite de limitación, los documentos entrantes en el directorio de entrada de la carpeta vigilada no se sondea. El documento también permanece en el directorio de entrada hasta que se completen otros trabajos de carpetas vigiladas y se realice otro intento de encuesta. Para el procesamiento sincrónico, todos los trabajos procesados en una sola encuesta se cuentan hacia el límite de limitación, aunque los trabajos se procesen consecutivamente en un solo subproceso.

>[!NOTE]
>
>La limitación no se escala con un clúster. Cuando se habilita la limitación, el clúster en su conjunto no procesará más trabajos que el número especificado en Tamaño de lote en un momento dado. Este límite es para todo el clúster y no es específico para cada nodo del clúster. Por ejemplo, con un tamaño de lote de 2, se puede alcanzar el límite de regulación con un solo nodo que procese dos trabajos y ningún otro nodo sondeará el directorio de entrada hasta que se complete uno de los trabajos.

#### Cómo funciona la limitación {#how-throttling-works}

Watched Folder analiza la carpeta de entrada en cada intervalo de encuesta, toma el número de archivos especificado en Tamaño de lote e invoca el servicio de destinatario para cada uno de estos archivos. Por ejemplo, si el tamaño del lote es cuatro, en cada análisis, la carpeta vigilada recoge cuatro archivos, crea cuatro solicitudes de invocación e invoca el servicio de destinatario. Antes de que se completen estas solicitudes, si se invoca la carpeta vigilada, vuelve a inicio cuatro trabajos, independientemente de si se han completado o no los cuatro trabajos anteriores.

La limitación evita que la carpeta vigilada invoque nuevos trabajos cuando los trabajos anteriores no se han completado. La carpeta vigilada detecta los trabajos en curso y procesa los nuevos trabajos en función del tamaño del lote menos los trabajos en curso. Por ejemplo, en la segunda invocación, si el número de trabajos completados es solo tres y un trabajo sigue en curso, Watched Folder solo invoca tres trabajos más.

* La carpeta vigilada depende del número de archivos presentes en la carpeta del escenario para averiguar cuántos trabajos están en curso. Si los archivos siguen sin procesarse en la carpeta del escenario, la carpeta vigilada no invocará más trabajos. Por ejemplo, si el tamaño del lote es cuatro y se han detenido tres trabajos, la carpeta vigilada solo invocará un trabajo en las invocaciones posteriores. Existen varios escenarios que pueden hacer que los archivos permanezcan sin procesar en la carpeta de escenario. Cuando los trabajos están paralizados, el administrador puede finalizar el proceso en la página de administración de Process Management para que Watched Folder mueva los archivos fuera de la carpeta del escenario.
* Si el servidor de AEM Forms deja de funcionar antes de que la carpeta vigilada invoque los trabajos, el administrador puede mover los archivos fuera de la carpeta del escenario. Para obtener más información, consulte [Puntos de error y recuperación](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).
* Si el servidor de AEM Forms se está ejecutando pero la carpeta vigilada no se está ejecutando cuando el servicio Administrador de trabajos vuelve a llamar, lo que ocurre cuando los servicios no inicio en la secuencia ordenada, el administrador puede mover los archivos fuera de la carpeta del escenario. Para obtener más información, consulte [Puntos de error y recuperación](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).

### Puntos de error y recuperación Puntos de error y recuperación {#failure-points-and-recoveryfailure-points-and-recovery}

En cada evento de la encuesta, la carpeta vigilada bloquea la carpeta de entrada, mueve los archivos que coinciden con el patrón de inclusión de archivos a la carpeta del escenario y, a continuación, desbloquea la carpeta de entrada. El bloqueo es necesario para que dos subprocesos no tomen el mismo conjunto de archivos y los procesen dos veces. Las posibilidades de que esto ocurra aumentan con un pequeño intervalo de encuesta y un gran tamaño de lote. Después de mover los archivos a la carpeta de escenario, la carpeta de entrada se desbloquea para que otros subprocesos puedan examinar la carpeta. Este paso ayuda a proporcionar un alto rendimiento, ya que otros subprocesos pueden analizarse mientras un subproceso está procesando los archivos.

Una vez que los archivos se mueven a la carpeta stage, se crean solicitudes de invocación para cada archivo y se invoca el servicio de destinatario. Es posible que haya casos en los que la carpeta vigilada no pueda recuperar los archivos de la carpeta del escenario:

* Si el servidor deja de funcionar antes de que la carpeta vigilada pueda crear la solicitud de invocación, los archivos de la carpeta del escenario permanecen en la carpeta del escenario y no se recuperan.

* Si la carpeta vigilada ha creado correctamente la solicitud de invocación para cada uno de los archivos de la carpeta de escenario y el servidor se bloquea, hay dos comportamientos basados en el tipo de invocación:

   * **Sincrónico**: Si la carpeta vigilada está configurada para invocar el servicio sincrónicamente, todos los archivos de la carpeta de escenario permanecen sin procesar en la carpeta de escenario.
   * **Asincrónico**: En este caso, la carpeta vigilada depende del servicio Administrador de trabajos. Si el servicio de administrador de trabajos devuelve la llamada a la carpeta vigilada, los archivos de la carpeta de etapa se mueven a la carpeta de conservación o error en función de los resultados de la invocación. Si el servicio Administrador de trabajos no devuelve la llamada a la carpeta vigilada, los archivos permanecerán sin procesar en la carpeta del escenario. Esta situación se produce cuando la carpeta vigilada no se está ejecutando cuando el Administrador de trabajos vuelve a llamar.

#### Recuperar archivos de origen no procesados en la carpeta de etapa {#recover-unprocessed-source-files-in-the-stage-folder}

Cuando la carpeta de inspección no puede procesar los archivos de origen en la carpeta de etapa, puede recuperar los archivos sin procesar.

1. Reinicie el servidor de aplicaciones o el nodo.

1. Detenga la carpeta vigilada para que no procese nuevos archivos de entrada. Si omite este paso, será mucho más difícil determinar qué archivos no se procesan en la carpeta de escenario. Para evitar que la carpeta vigilada procese nuevos archivos de entrada, realice una de las siguientes tareas:

   * Cambie la propiedad includeFilePattern de la carpeta vigilada a algo que no coincida con ninguno de los nuevos archivos de entrada (por ejemplo, introduzca NOMATCH).
   * Suspenda el proceso de creación de nuevos archivos de entrada.

   Espere hasta que AEM Forms recupere y procese todos los archivos. La mayoría de los archivos deben recuperarse y los nuevos archivos de entrada deben procesarse correctamente. El tiempo que espera a que la carpeta vigilada se recupere y procese los archivos dependerá de la duración de la operación que se invoque y del número de archivos que se recuperarán.

1. Determinar qué archivos no se pueden procesar. Si ha esperado una cantidad de tiempo adecuada y ha completado el paso anterior, y aún quedan archivos sin procesar en la carpeta de escenario, vaya al paso siguiente.

   >[!NOTE]
   >
   >Puede consultar la marca de fecha y hora de los archivos en el directorio de etapas. En función del número de archivos y del tiempo de procesamiento normal, puede determinar qué archivos son lo suficientemente antiguos como para que se los considere atascados.

1. Copie los archivos sin procesar del directorio de etapa al directorio de entrada.

1. Si ha impedido que la carpeta vigilada procese nuevos archivos de entrada en el paso 2, cambie el Patrón de archivos de inclusión a su valor anterior o vuelva a habilitar el proceso que deshabilitó.

### Carpetas vigiladas por cadena {#chain-watched-folders-together}

Las carpetas vigiladas se pueden encadenar juntas para que el documento resultante de una carpeta vigilada sea el documento de entrada de la siguiente carpeta vigilada. Cada carpeta vigilada puede invocar un servicio diferente. Al configurar las carpetas vigiladas de esta manera, se pueden invocar varios servicios. Por ejemplo, una carpeta vigilada podría convertir archivos PDF a Adobe PostScript® y una segunda carpeta vigilada podría convertir los archivos PostScript a formato PDF/A. Para ello, simplemente configure la carpeta de resultados de la carpeta Watched definida por el primer punto final para que apunte a la carpeta de entrada de la carpeta Watched definida por el segundo punto final.

El resultado de la primera conversión iría a \path\result. La entrada para la segunda conversión sería \path\result y el resultado de la segunda conversión iría a \path\result\result  (o el directorio que defina en el cuadro Carpeta de resultados para la segunda conversión).

### Patrones de archivos y carpetas {#file-and-folder-patterns}

Los administradores pueden especificar el tipo de archivo que puede invocar un servicio. Se pueden establecer varios patrones de archivo para cada carpeta vigilada. Un patrón de archivo puede ser una de las siguientes propiedades de archivo:

* Archivos con extensiones de nombre de archivo específicas; por ejemplo, *.dat, *.xml, .pdf, *.*
* Archivos con nombres específicos; por ejemplo, datos.*
* Archivos con expresiones compuestas en el nombre y la extensión, como en estos ejemplos:

   * Data[0-9][0-9][0-9].[dD][aA]&#39;puerto&#39;
   * *.[dD][Aa]&#39;puerto&#39;
   * *.[Xx][Mm][Ll]

* El administrador puede definir el patrón de archivo de la carpeta de salida en la que desea almacenar los resultados. Para las carpetas de salida (resultado, conservación y error), el administrador puede especificar cualquiera de estos patrones de archivo:
* %Y = año (completo)
* %y = año (dos últimos dígitos)
* %M = mes,
* %D = día del mes,
* %d = día del año,
* %h = hora,
* %m = minuto,
* %s = segundo,
* %R = número aleatorio entre 0 y 9
* %J = Nombre del trabajo

Por ejemplo, la ruta de la carpeta de resultados puede ser C:\Adobe\Adobe LiveCycle ES4\BarcodedForms\%y\%m\%d.

Las asignaciones de parámetros de salida también pueden especificar patrones adicionales, como estos:

* %F = Nombre de archivo de origen
* %E = Extensión de nombre de archivo de origen

Si el patrón de asignación de parámetros de salida termina con &quot;File.separator&quot; (que es el separador de rutas), se crea una carpeta y el contenido se copia en esa carpeta. Si el patrón no termina con &quot;File.separator&quot;, el contenido (archivo de resultados o carpeta) se crea con ese nombre.

## Uso de PDF Generator con una carpeta vigilada {#using-pdf-generator-with-a-watched-folder}

Puede configurar una carpeta vigilada para iniciar un flujo de trabajo, un servicio o una secuencia de comandos para procesar los archivos de entrada. En la siguiente sección, configuraremos una carpeta vigilada para iniciar un ECMAScript. ECMAScript utilizaría el generador de PDF para convertir documentos de Microsoft Word (.docx) en documentos PDF.

Realice los siguientes pasos para configurar una carpeta vigilada con el generador de PDF:

1. [Creación de un ECMAScript](../../forms/using/watched-folder-in-aem-forms.md#p-create-an-ecmascript-p)
1. [Crear un flujo de trabajo](../../forms/using/watched-folder-in-aem-forms.md#p-create-a-workflow-p)
1. [Configurar la carpeta vigilada](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p)

### Crear un ECMAScript {#create-an-ecmascript}

ECMAScript utilizaría la API createPDF del generador de PDF para convertir documentos de Microsoft Word (.docx) en documentos PDF. Realice los siguientes pasos para crear la secuencia de comandos:

1. Abra la lista CRXDE en una ventana del explorador. La dirección URL es https://&#39;[server]:[port]&#39;/crx/de.

1. Vaya a /etc/workflow/scripts y cree una carpeta denominada PDFG.

1. En la carpeta PDFG, cree un archivo denominado pdfg-openOffice-sample.ecma y agregue el siguiente código al archivo:

   ```javascript
   var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
   // Custom ContentProcessor implementation which defines the processInputs() method purely in JS
   var impl = { processWorkflowContext: function (wrkfContext) {
   
     //  var logger = Packages.org.slf4j.LoggerFactory.getLogger("cmb-mergeandprint-sample.ecma");
                   var inputMap=wrkfContext.getInputMap();
   
                   var distiller = sling.getService(com.adobe.pdfg.service.api.DistillerService);
                   var generatePDF = sling.getService(com.adobe.pdfg.service.api.GeneratePDFService);
                   var pdfgConfig = sling.getService(com.adobe.pdfg.service.api.PDFGConfigService);
       var result = new Packages.java.util.HashMap();
       var entry = inputMap.entrySet().iterator().next();
       var pdfgOut = generatePDF.createPDF(entry.getValue(), ".docx", "Standard OpenOffice", "Standard", "No Security", null, null);
                   var convertedDoc = pdfgOut.get("ConvertedDoc");
   //   logger.info("SuccessFully saved the document to Ouput Node");
       wrkfContext.setResult(entry.getKey().substring(0, entry.getKey().lastIndexOf('.'))+".pdf",convertedDoc); // Ownership flag set to true for auto temp-file deletion.
   
   } }
   
   wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
   ```

1. Guarde y cierre el archivo.

### Crear un flujo de trabajo {#create-a-workflow}

1. Abra AEM interfaz de usuario de workflow en una ventana del explorador.
https://[nombre_servidor]:&#39;puerto&#39;/flujo de trabajo

1. En la vista Modelos, haga clic en **Nuevo**. En el cuadro de diálogo Nuevo flujo de trabajo, especifique **Título** y haga clic en **Aceptar**.

   ![create-a-workflow-pdf](assets/create-a-workflow-pdf.png)

1. Seleccione el flujo de trabajo recién creado y haga clic en **Editar**. El flujo de trabajo se abre en una ventana nueva.

1. Elimine el paso predeterminado del flujo de trabajo. Arrastre y suelte el paso de proceso desde la barra de tareas hasta el flujo de trabajo.

   ![create-a-workflow-pdf2](assets/create-a-workflow-pdf2.png)

1. Haga clic con el botón derecho en el paso de proceso y seleccione **Editar**. Aparece la ventana Propiedades del paso.

1. En la ficha Proceso, seleccione ECMAScript. Por ejemplo, la secuencia de comandos pdfg-openOffice-sample.ecma creada en [Crear un ECMAScript](#p-create-an-ecmascript-p). Habilite la opción **Avance del controlador** y haga clic en **Aceptar**.

   ![create-a-workflow3-pdf](assets/create-a-workflow3-pdf.png)

### Configurar la carpeta vigilada {#configure-the-watched-folder}

1. Abra la lista CRXDE en una ventana del explorador. https://&#39;[servidor]:[puerto]&#39;/crx/de/

1. Vaya a la carpeta /etc/fd/watchfolder/config/ y cree un nodo de tipo nt:unestructure.

   ![configure-the-watch-folder-pdf](assets/configure-the-watched-folder-pdf.png)

1. Añada las siguientes propiedades en el nodo:

   * folderPath (String): Ruta de la carpeta que se va a analizar en intervalos de tiempo definidos. La carpeta debe estar en una ubicación compartida con todos los servidores con acceso completo al servidor.
inputProcessorType (String): Tipo de proceso que se va a inicio. En este tutorial, especifique el flujo de trabajo.

   * inputProcessorId (String): El comportamiento de la propiedad inputProcessorId se basa en el valor especificado para la propiedad inputProcessorType. En este ejemplo, el valor de la propiedad inputProcessorType es workflow. Por lo tanto, para la propiedad inputProcessorId, especifique la siguiente ruta del flujo de trabajo del PDFG: /etc/workflow/models/pdfg/jcr:content/model

   * outputFilePattern (String): Patrón del archivo de salida. Puede especificar una carpeta o un patrón de archivos. Si se especifica un patrón de carpetas, los archivos de salida tienen nombres como se describe en flujos de trabajo. Si se especifica un patrón de archivos, los archivos de salida tienen nombres como se describe en el patrón de archivos.
   Aparte de las propiedades obligatorias mencionadas anteriormente, las carpetas vigiladas también admiten algunas propiedades opcionales. Para obtener una lista y una descripción completas de las propiedades opcionales, consulte [Propiedades de la carpeta vigilada](#watchedfolderproperties).

