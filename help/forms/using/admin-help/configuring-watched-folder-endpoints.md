---
title: Configuración de los extremos de carpetas vigiladas
seo-title: Configuración de los extremos de carpetas vigiladas
description: Obtenga información sobre cómo configurar los extremos de las carpetas vigiladas.
seo-description: Obtenga información sobre cómo configurar los extremos de las carpetas vigiladas.
uuid: 01fb5ff8-2071-44bd-9241-7d5d41a5b26e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 761e7909-43ba-4642-bcfc-8d76f139b9a3
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '7174'
ht-degree: 0%

---


# Configuración de los extremos de carpeta observados {#configuring-watched-folder-endpoints}

Un administrador puede configurar una carpeta de red, conocida como *carpeta vigilada*, para que cuando un usuario coloque un archivo (como un archivo PDF) en la carpeta vigilada, se invoque una operación de servicio configurada y se manipule el archivo. Una vez que el servicio realiza la operación especificada, guarda el archivo modificado en una carpeta de salida especificada.

## Configuración del servicio de carpetas vigiladas {#configuring-the-watched-folder-service}

Antes de configurar un extremo de carpeta vigilada, configure el servicio Carpeta vigilada. Los parámetros de configuración del servicio Carpeta vigilada tienen dos propósitos:

* Para configurar atributos que son comunes para todos los extremos de carpeta observados
* Proporcionar valores predeterminados para todos los extremos de carpeta observados

Después de configurar el servicio de carpetas vigiladas, agregue un extremo de carpetas vigiladas para el servicio de destinatario. Al agregar el extremo, se configuran valores, como el nombre del servicio y el nombre de la operación, para que se invoquen cuando se coloquen archivos o carpetas en la carpeta de entrada del servicio de carpetas vigiladas configurado. Para obtener más información sobre la configuración del servicio Carpeta vigilada, consulte [Configuración del servicio Carpeta vigilada](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings).

## Creación de una carpeta vigilada {#creating-a-watched-folder}

Puede crear una carpeta vigilada de las dos formas siguientes:

* Al configurar la configuración de un extremo de carpeta vigilada, escriba la ruta completa al directorio principal en el cuadro Ruta y anexe el nombre de la carpeta vigilada que se va a crear, como se muestra en este ejemplo:
   `  C:\MyPDFs\MyWatchedFolder`Como la carpeta MyWatchedFolder no existe, AEM formularios intentan crearla en esa ubicación.

* Cree una carpeta en el sistema de archivos antes de configurar un extremo de carpeta vigilado y, a continuación, escriba la ruta completa en el cuadro Ruta.

En un entorno agrupado, la carpeta que se utilizará como carpeta vigilada debe ser accesible, grabable y compartida en el sistema de archivos o la red. En este escenario, cada instancia de servidor de aplicaciones del clúster debe tener acceso a la misma carpeta compartida.

En Windows, si el servidor de aplicaciones se está ejecutando como un servicio, debe iniciarse con el acceso adecuado a la carpeta compartida de una de las siguientes maneras:

* Configure el parámetro **a1/> del servicio del servidor de aplicaciones para que se inicio como un usuario específico con acceso adecuado a la carpeta vigilada compartida.**
* Configure el Inicio del servicio del servidor de aplicaciones como sistema local para permitir que el servicio interactúe con el escritorio. Esta opción requiere que todos tengan acceso a la carpeta vigilada compartida y que se pueda escribir en ella.

## Encadenado de carpetas vigiladas {#chaining-together-watched-folders}

Las carpetas vigiladas se pueden encadenar juntas para que el documento resultante de una carpeta vigilada sea el documento de entrada de la siguiente carpeta vigilada. Cada carpeta vigilada puede invocar un servicio diferente. Al configurar las carpetas vigiladas de esta manera, se pueden invocar varios servicios. Por ejemplo, una carpeta vigilada podría convertir archivos PDF a Adobe PostScript® y otra carpeta vigilada podría convertir los archivos PostScript a formato PDF/A. Para ello, simplemente configure la carpeta *result* de la carpeta vigilada definida por el primer punto final para que señale a la carpeta *input* de la carpeta vigilada definida por el segundo punto final.

El resultado de la primera conversión iría a \path\result. La entrada para la segunda conversión sería \path\result y el resultado de la segunda conversión iría a \path\result\result  (o el directorio que defina en el cuadro Carpeta de resultados para la segunda conversión).

## Cómo interactúan los usuarios con las carpetas vigiladas {#how-users-interact-with-watched-folders}

Para un extremo de carpeta vigilada, los usuarios pueden invocar copiando o arrastrando archivos de entrada o carpetas de sus escritorios a una carpeta vigilada. Los archivos se procesarán en el orden en que lleguen.

Para los extremos de carpeta vigilados, si el trabajo solo requiere un archivo de entrada, el usuario puede copiar ese archivo en la raíz de la carpeta vigilada.

Si el trabajo contiene más de un archivo de entrada, el usuario debe crear una carpeta fuera de la jerarquía de carpetas vigiladas que contenga todos los archivos necesarios. Esta nueva carpeta debe incluir los archivos de entrada (y opcionalmente un archivo DDX si el proceso lo requiere). Una vez construida la carpeta de trabajo, el usuario la copia en la carpeta de entrada de la carpeta controlada.

>[!NOTE]
>
>Asegúrese de que el servidor de aplicaciones ha eliminado el acceso a los archivos de la carpeta vigilada. Si AEM formularios no pueden eliminar los archivos de la carpeta de entrada después de analizarlos, el proceso asociado se invocará indefinidamente.

## Salida de carpeta observada {#watched-folder-output}

Cuando la entrada es una carpeta y el resultado consta de varios archivos, AEM formularios crea una carpeta de salida con el mismo nombre que la carpeta de entrada y copia los archivos de salida en dicha carpeta. Cuando el resultado consiste en un mapa de documento que contiene un par clave-valor, como el resultado de un proceso Output, la clave se utilizará como nombre de archivo de salida.

Los nombres de archivo de salida que resultan de un proceso de extremo no pueden contener caracteres que no sean letras, números y un punto (.) antes de la extensión del archivo. AEM formularios convierte otros caracteres a sus valores hexadecimales.

Las aplicaciones cliente recogen los documentos resultantes de la carpeta de resultados de la carpeta controlada. Los errores de proceso se registran en la carpeta de errores de la carpeta controlada.

## Cómo funciona la carpeta vigilada {#how-watched-folder-works}

El módulo Carpeta vigilada contiene estos servicios:

* Servicio de carpetas vigiladas
* provider.file_scan_service
* provider.file_write_results_service

Además de los servicios mencionados anteriormente, Watched Folder también depende de otros servicios, incluido el servicio de Planificador para programar los trabajos y el servicio de Job Manager para admitir la invocación asincrónica de servicios de destinatario.

### Proceso de la carpeta vigilada de una solicitud de invocación {#how-watched-folder-processes-an-invocation-request}

El servicio Carpeta vigilada gestiona la creación, actualización y eliminación de los extremos. Una vez que el administrador haya creado los extremos, el servicio de Planificador programará su activación según el intervalo de repetición o la expresión de cron especificados.

Este diagrama ilustra cómo la carpeta vigilada procesa una solicitud de invocación.

![en_watchedfolder](assets/en_watchedfolder.png)

El proceso de invocación de un servicio mediante carpetas vigiladas es el siguiente:

1. Una aplicación cliente coloca archivos o carpetas en la carpeta de entrada de la carpeta controlada.
1. Cuando se produce el intervalo de exploración del trabajo, el servicio Planificador invoca provider.file_scan_service para procesar los archivos o las carpetas de la carpeta de entrada.
1. provider.file_scan_service realiza las siguientes tareas:


   * Examina la carpeta de entrada en busca de archivos o carpetas que coincidan con el patrón de inclusión de archivos y excluye los archivos o carpetas del patrón de exclusión de archivos especificado. Los archivos o carpetas más antiguos se recogen primero. También se recogen los archivos y las carpetas que tengan una antigüedad superior al tiempo de espera. En un análisis, el número de archivos o carpetas procesados se basa en el tamaño del lote. Para obtener más información sobre los patrones de archivo, consulte [Acerca de los patrones de archivo](configuring-watched-folder-endpoints.md#about-file-patterns). Para obtener información sobre cómo configurar el tamaño del lote, consulte [Configuración del servicio de carpetas vigiladas](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings).
   * Recopila los archivos o carpetas para su procesamiento. Si los archivos o carpetas no se descargan completamente, se recogen en el siguiente análisis. Para asegurarse de que las carpetas se descargan completamente, los administradores deben crear una carpeta con un nombre utilizando el patrón de exclusión de archivos. Una vez que la carpeta tiene todos los archivos, debe cambiarse su nombre por el patrón especificado en el patrón de archivos de inclusión. Este paso garantiza que la carpeta tiene todos los archivos necesarios para invocar el servicio. Para obtener más información sobre cómo garantizar que las carpetas se descarguen por completo, consulte [Sugerencias y trucos para carpetas controladas](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).
   * Mueve los archivos o carpetas a la carpeta del escenario después de seleccionarlos para su procesamiento.
   * Convierte los archivos o carpetas de la carpeta de escenario a la entrada adecuada según las asignaciones de parámetros de entrada de extremo. Para obtener ejemplos de asignaciones de parámetros de entrada, consulte [Sugerencias y trucos para carpetas controladas](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).


1. El servicio de destinatario configurado para el extremo se invoca de forma sincrónica o asincrónica. El servicio de destinatario se invoca utilizando el nombre de usuario y la contraseña configurados para el extremo.

   * La invocación sincrónica llama al servicio de destinatario directamente y gestiona inmediatamente la respuesta.
   * Para la invocación asincrónica, se llama al servicio de destinatario a través del servicio de Job Manager, que coloca la solicitud en una cola. El servicio de Job Manager, a su vez, llama al proveedor.file_write_results_service para controlar los resultados.

1. El provider.file_write_results_service gestiona la respuesta o el error de la invocación del servicio de destinatario. Cuando se realiza correctamente, el resultado se guarda en la carpeta de resultados según la configuración del extremo. El provider.file_write_results_service también conserva el origen si el extremo está configurado para conservar los resultados una vez finalizados correctamente.

   Cuando la invocación del servicio de destinatario resulta en un error, provider.file_write_results_service registra el motivo del error en un archivo fail.log y coloca ese archivo en la carpeta de errores. La carpeta de errores se crea en función de los parámetros de configuración especificados para el extremo. Cuando el administrador establece la opción Mantener si hay un error para la configuración del extremo, provider.file_write_results_service también copia los archivos de origen en la carpeta de error. Para obtener información sobre la recuperación de archivos desde la carpeta de errores, consulte [Puntos de error y recuperación](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Configuración del extremo de la carpeta observada {#watched-folder-endpoint-settings}

Utilice la siguiente configuración para configurar un extremo de carpeta vigilado.

**Nombre:**  (obligatorio) Identifica el extremo. No incluya un carácter &lt; porque truncará el nombre mostrado en Workspace. Si está introduciendo una dirección URL como nombre del extremo, asegúrese de que cumple las reglas de sintaxis especificadas en RFC1738.

**Descripción:** Descripción del extremo. No incluya un carácter &lt; porque truncará la descripción que se muestra en Workspace.

**Ruta:** (obligatoria) Especifica la ubicación de la carpeta vigilada. En un entorno agrupado, esta configuración debe apuntar a una carpeta de red compartida a la que se pueda acceder desde todos los equipos del clúster.

**Asincrónico:** identifica el tipo de invocación como asíncrono o sincrónico. El valor predeterminado es asincrónico. Se recomienda la asincrónica para procesos de larga duración, mientras que la sincrónica se recomienda para procesos transitorios o de corta duración.

**Expresión Cron:** Introduzca una expresión cron si la carpeta controlada debe programarse mediante una expresión cron. Cuando se configura esta opción, se ignora el intervalo de repetición.

**Intervalo de repetición:** el intervalo en segundos para analizar la carpeta vigilada para la introducción de datos. A menos que la configuración de aceleración esté habilitada, el intervalo de repetición debe ser mayor que el tiempo para procesar un trabajo promedio; de lo contrario, el sistema podría estar sobrecargado. El valor predeterminado es 5. Consulte la descripción del tamaño del lote para obtener más información.

**Recuento de repeticiones:** Número de veces que la carpeta vigilada explora la carpeta o el directorio. Un valor de -1 indica la digitalización indefinida. El valor predeterminado es -1.

**Aceleración:** cuando se selecciona esta opción, se limita el número de trabajos de carpeta observados que se procesan AEM formularios en un momento dado. El número máximo de trabajos viene determinado por el valor Tamaño de lote. (Consulte Acerca de la limitación).

**Nombre de usuario:**  (obligatorio) el nombre de usuario que se utiliza al invocar un servicio de destinatario desde la carpeta controlada. El valor predeterminado es SuperAdmin.

**Nombre de dominio:**  (obligatorio) El dominio del usuario. El valor predeterminado es DefaultDom.

**Tamaño de lote:** el número de archivos o carpetas que se van a buscar por análisis. Utilícelo para evitar una sobrecarga en el sistema; el análisis de demasiados archivos al mismo tiempo puede provocar un bloqueo. El valor predeterminado es 2.

La configuración de Repetir intervalo y Tamaño de lote determina cuántos archivos ha visto la carpeta se recogen en cada análisis. Watched Folder utiliza un grupo de subprocesos de Quartz para analizar la carpeta de entrada. El grupo de subprocesos se comparte con otros servicios. Si el intervalo de exploración es pequeño, los subprocesos analizarán la carpeta de entrada con frecuencia. Si los archivos se sueltan con frecuencia en la carpeta vigilada, debe reducir el intervalo de exploración. Si los archivos se retiran con poca frecuencia, utilice un intervalo de exploración mayor para que los demás servicios puedan utilizar los subprocesos.

Si se está extrayendo un gran volumen de archivos, haga que el tamaño del lote sea grande. Por ejemplo, si el servicio invocado por el extremo de la carpeta vigilada puede procesar 700 archivos por minuto y los usuarios sueltan los archivos en la carpeta de entrada a la misma velocidad, si se establece el tamaño del lote en 350 y el intervalo de repetición en 30 segundos, se ayudará a observar el rendimiento de la carpeta sin incurrir en el coste de digitalizar la carpeta vigilada con demasiada frecuencia.

Cuando los archivos se colocan en la carpeta vigilada, se lista la entrada de los archivos, lo que puede reducir el rendimiento si se realiza el análisis cada segundo. El aumento del intervalo de exploración puede mejorar el rendimiento. Si el volumen de archivos que se van a soltar es pequeño, ajuste el tamaño del lote y el intervalo de repetición en consecuencia. Por ejemplo, si se pierden 10 archivos cada segundo, intente establecer el intervalo de repetición en 1 segundo y el tamaño del lote en 10.

**Tiempo de espera:** El tiempo, en milisegundos, que debe esperarse antes de analizar una carpeta o archivo después de crearlo. Por ejemplo, si el tiempo de espera es de 3.600.000 milisegundos (una hora) y el archivo se creó hace un minuto, este archivo se recuperará después de que hayan transcurrido 59 minutos o más. El valor predeterminado es 0.

Esta configuración es útil para asegurarse de que un archivo o carpeta se copia completamente en la carpeta de entrada. Por ejemplo, si tiene un archivo grande para procesar y el archivo tarda diez minutos en descargarse, establezca el tiempo de espera en 10&amp;ast;60 &amp;ast;1000 milisegundos. Esto evita que la carpeta vigilada analice el archivo si no tiene diez minutos de antigüedad.

**Patrón de exclusión de archivos:** punto y coma  **;lista** delimitada de patrones que utiliza una carpeta vigilada para determinar qué archivos y carpetas se deben analizar y recoger. No se analizará ningún archivo o carpeta con este patrón para su procesamiento.

Esta opción resulta útil cuando la entrada es una carpeta con varios archivos. El contenido de la carpeta se puede copiar en una carpeta con un nombre que la carpeta vigilada recogerá. Esto evita que la carpeta vigilada recoja una carpeta para procesarla antes de que la carpeta se copie completamente en la carpeta de entrada.

Puede utilizar patrones de archivo para excluir:

* Archivos con extensiones de nombre de archivo específicas; por ejemplo, &amp;ast;.dat, &amp;ast;.xml, &amp;ast;.pdf.
* Archivos con nombres específicos; por ejemplo, datos.&amp;ast; excluiría archivos y carpetas con nombres *data1*, *data2*, etc.
* Archivos con expresiones compuestas en el nombre y la extensión, como en estos ejemplos:

   * Data[0-9][0-9][0-9].[dD][aA]&#39;puerto&#39;
   * &amp;ast;..[dD][Aa]&#39;puerto&#39;
   * &amp;ast;..[Xx][Mm][Ll]

Para obtener más información sobre los patrones de archivo, consulte [Acerca de los patrones de archivo](configuring-watched-folder-endpoints.md#about-file-patterns).

**Patrón de archivos de inclusión:**  (obligatorio) punto y coma  **;lista** delimitada de patrones que utiliza la carpeta vigilada para determinar qué carpetas y archivos se deben analizar y recoger. Por ejemplo, si el Patrón de archivos de inclusión es input&amp;ast;, todos los archivos y carpetas que coincidan con input&amp;ast; son recogidos. Esto incluye archivos y carpetas denominados input1, input2, etc.

El valor predeterminado es &amp;ast; e indica todos los archivos y carpetas.

Puede utilizar patrones de archivo para incluir:

* Archivos con extensiones de nombre de archivo específicas; por ejemplo, &amp;ast;.dat, &amp;ast;.xml, &amp;ast;.pdf.
* Archivos con nombres específicos; por ejemplo, datos.&amp;ast; incluiría archivos y carpetas con el nombre *data1*, *data2*, etc.
* Archivos con expresiones compuestas en el nombre y la extensión, como en estos ejemplos:

   * Data[0-9][0-9][0-9].[dD][aA]&#39;puerto&#39;
   * &amp;ast;..[dD][Aa]&#39;puerto&#39;
   * &amp;ast;..[Xx][Mm][Ll]

Para obtener más información sobre los patrones de archivo, consulte [Acerca de los patrones de archivo](configuring-watched-folder-endpoints.md#about-file-patterns).


**Carpeta de resultados:** la carpeta en la que se almacenan los resultados guardados. Si los resultados no aparecen en esta carpeta, compruebe la carpeta de errores. Los archivos de sólo lectura no se procesan y se guardarán en la carpeta de errores. Este valor puede ser una ruta absoluta o relativa con los siguientes patrones de archivo:

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

Por ejemplo, si es a las 8 pm del 17 de julio de 2009 y especifica `C:/Test/WF0/failure/%Y/%M/%D/%H/`, la carpeta de resultados es `C:/Test/WF0/failure/2009/07/17/20`.

Si la ruta no es absoluta sino relativa, la carpeta se creará dentro de la carpeta controlada. El valor predeterminado es result/%Y/%M/%D/, que es la carpeta Result dentro de la carpeta observada. Para obtener más información sobre los patrones de archivo, consulte [Acerca de los patrones de archivo](configuring-watched-folder-endpoints.md#about-file-patterns).

>[!NOTE]
>
>Cuanto menor sea el tamaño de las carpetas resultantes, mejor será el rendimiento de la carpeta vigilada. Por ejemplo, si la carga estimada para la carpeta vigilada es de 1000 archivos por hora, pruebe un patrón como `result/%Y%M%D%H` para que se cree una nueva subcarpeta cada hora. Si la carga es más pequeña (por ejemplo, 1000 archivos por día), puede usar un patrón como `result/%Y%M%D`.

**Conservar carpeta:** la ubicación en la que se almacenan los archivos tras realizar correctamente el análisis y la recogida. La ruta puede ser absoluta, relativa o nula. Puede utilizar patrones de archivo, como se describe en Carpeta de resultados. El valor predeterminado es preserve/%Y/%M/%D/.

**Carpeta de errores:** la carpeta en la que se guardan los archivos de error. Esta ubicación siempre es relativa a la carpeta vigilada. Puede utilizar patrones de archivo, como se describe en Carpeta de resultados.

Los archivos de sólo lectura no se procesan y se guardarán en la carpeta de errores.

El valor predeterminado es error/%Y/%M/%D/.

**Preservar si falla:** Preservar archivos de entrada en caso de error al ejecutar la operación en un servicio. El valor predeterminado es true.

**Sobrescribir nombres de archivo de Duplicado:** cuando se establece en True, se sobrescriben los archivos de la carpeta de resultados y la carpeta de preservación. Cuando se establece en False, se utilizan para el nombre archivos y carpetas con un sufijo de índice numérico. El valor predeterminado es False.

**Duración de purga:**  (obligatorio) Los archivos y carpetas de la carpeta de resultados se purgan cuando son anteriores a este valor. Este valor se mide en días. Esta configuración es útil para garantizar que la carpeta de resultados no se llena.

Un valor de -1 días indica que nunca se elimina la carpeta de resultados. El valor predeterminado es -1.

**Nombre de la operación:**  (obligatorio) una lista de operaciones que se pueden asignar al extremo de la carpeta controlada.

**Asignaciones de parámetros de entrada:** se utiliza para configurar la entrada necesaria para procesar el servicio y la operación. La configuración disponible depende del servicio que utilice el extremo de la carpeta vigilada. Estos son los dos tipos de entradas:

**Literal:** la carpeta controlada utiliza el valor introducido en el campo al mostrarse. Se admiten todos los tipos de Java básicos. Por ejemplo, si una API utiliza entradas como String, long, int y Boolean, la cadena se convierte al tipo adecuado y se invoca el servicio.

**Variable:** El valor introducido es un patrón de archivo que utiliza la carpeta vigilada para elegir la entrada. Por ejemplo, en el caso del servicio de cifrado de contraseñas, donde el documento de entrada debe ser un archivo PDF, el usuario puede utilizar &amp;ast;.pdf como patrón de archivo. La carpeta observada recogerá todos los archivos de la carpeta vigilada que coincidan con este patrón e invocará el servicio para cada archivo. Cuando se utiliza una variable, todos los archivos de entrada se convierten en documentos. Solo se admiten las API que utilizan Documento como tipo de entrada.

**Asignaciones de parámetros de salida:** se utiliza para configurar las salidas del servicio y la operación. La configuración disponible depende del servicio que utilice el extremo de la carpeta vigilada.

El resultado de la carpeta vigilada puede ser un solo documento, una lista de documentos o un mapa de documentos. Estos documentos de salida se guardan en la carpeta de resultados, utilizando el patrón especificado en Asignación de parámetros de salida.

>[!NOTE]
>
>La especificación de nombres que resulten en nombres de archivo de salida únicos mejora el rendimiento. Por ejemplo, piense en el caso en que el servicio devuelve un documento de salida y la Asignación de parámetros de salida lo asigna a `%F.%E` (el nombre de archivo y la extensión del archivo de entrada). En este caso, si los usuarios sueltan archivos con el mismo nombre cada minuto y la carpeta resultante se configura en `result/%Y/%M/%D` y la opción Sobrescribir nombre de archivo Duplicado está desactivada, la carpeta vigilada intentará resolver los nombres de archivo duplicado. El proceso de resolución de nombres de archivos duplicado puede afectar al rendimiento. En este caso, cambiar la asignación de parámetros de salida a `%F_%h_%m_%s_%l` para agregar horas, minutos, segundos y milisegundos al nombre, o garantizar que los archivos eliminados tengan nombres únicos, puede mejorar el rendimiento.

## Acerca de los patrones de archivo {#about-file-patterns}

Los administradores pueden especificar el tipo de archivo que puede invocar un servicio. Se pueden establecer varios patrones de archivo para cada carpeta vigilada. Un patrón de archivo puede ser una de las siguientes propiedades de archivo:

* Archivos con extensiones de nombre de archivo específicas; por ejemplo, &amp;ast;.dat, &amp;ast;.xml, &amp;ast;.pdf,;;
* Archivos con nombres específicos; por ejemplo, datos.&amp;ast;
* Archivos con expresiones compuestas en el nombre y la extensión, como en estos ejemplos:

   * Data[0-9][0-9][0-9].[dD][aA]&#39;puerto&#39;
   * &amp;ast;..[dD][Aa]&#39;puerto&#39;
   * &amp;ast;..[Xx][Mm][Ll]

El administrador puede definir el patrón de archivo de la carpeta de salida en la que desea almacenar los resultados. Para las carpetas de salida (resultado, conservación y error), el administrador puede especificar cualquiera de estos patrones de archivo:

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

Por ejemplo, la ruta a la carpeta de resultados puede ser `C:\Adobe\Adobe_Experience_Manager_forms\BarcodedForms\%y\%m\%d`.

Las asignaciones de parámetros de salida también pueden especificar patrones adicionales, como estos:

* %F = Nombre de archivo de origen
* %E = Extensión de nombre de archivo de origen

Si el patrón de asignación de parámetros de salida termina con &quot;File.separator&quot; (que es el separador de rutas), se crea una carpeta y el contenido se copia en esa carpeta. Si el patrón no termina con &quot;File.separator&quot;, el contenido (archivo de resultados o carpeta) se crea con ese nombre. Para obtener más información sobre las asignaciones de parámetros de salida, consulte [Sugerencias y trucos para carpetas controladas](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).

## Acerca de la limitación {#about-throttling}

Cuando la limitación está habilitada para un extremo de carpeta de inspección, limita el número de trabajos de carpeta observados que se pueden procesar en un momento dado. El número máximo de trabajos está determinado por el valor Tamaño de lote, también configurable en el extremo Carpeta vigilada. Los documentos entrantes del directorio de entrada de la carpeta controlada no se sondearán cuando se alcance el límite de limitación. Los documentos también permanecerán en el directorio de entrada hasta que se hayan completado otros trabajos de carpeta vigilados y se haya realizado otro intento de encuesta. En el caso del procesamiento sincrónico, todos los trabajos procesados en una sola encuesta se contarán hacia el límite de limitación, aunque los trabajos se procesen consecutivamente en un solo subproceso.

>[!NOTE]
>
>La limitación no se escala con un clúster. Cuando se habilita la limitación, el clúster en su conjunto no procesará más trabajos que el número especificado en Tamaño de lote en un momento dado. Este límite es para todo el clúster y no es específico para cada nodo del clúster. Por ejemplo, con un tamaño de lote de 2, se puede alcanzar el límite de regulación con un solo nodo que procese dos trabajos y ningún otro nodo sondeará el directorio de entrada hasta que se complete uno de los trabajos.

### Cómo funciona la limitación {#how-throttling-works}

La carpeta observada analiza la carpeta de entrada en cada intervalo de repetición, toma el número de archivos especificado en Tamaño de lote e invoca el servicio de destinatario para cada uno de estos archivos. Por ejemplo, si el tamaño del lote es cuatro, en cada análisis, la carpeta vigilada recogerá cuatro archivos, creará cuatro solicitudes de invocación e invocará el servicio de destinatario. Antes de completar estas solicitudes, si se invoca la carpeta vigilada, se volverán a inicio cuatro trabajos, independientemente de si se han completado los cuatro trabajos anteriores.

La limitación evita que la carpeta vigilada invoque nuevos trabajos cuando los trabajos anteriores no se han completado. La carpeta vigilada detectará los trabajos en curso y procesará los nuevos trabajos en función del tamaño del lote menos los trabajos en curso. Por ejemplo, en la segunda invocación, si el número de trabajos completados es solo tres y un trabajo sigue en curso, Watched Folder solo invoca tres trabajos más.

* La carpeta vigilada depende del número de archivos presentes en la carpeta del escenario para averiguar cuántos trabajos están en curso. Si los archivos siguen sin procesarse en la carpeta del escenario, la carpeta vigilada no invocará más trabajos. Por ejemplo, si el tamaño del lote es cuatro y se han detenido tres trabajos, la carpeta vigilada solo invocará un trabajo en las invocaciones posteriores. Existen varios escenarios que pueden hacer que los archivos permanezcan sin procesar en la carpeta de escenario. Cuando los trabajos están paralizados, el administrador puede finalizar el proceso en la página de administración del flujo de trabajo de formularios para que la carpeta de inspección mueva los archivos fuera de la carpeta del escenario.
* Si el servidor de formularios deja de funcionar antes de que la carpeta vigilada pueda invocar los trabajos, el administrador puede mover los archivos fuera de la carpeta del escenario. Para obtener más información, consulte [Puntos de error y recuperación](configuring-watched-folder-endpoints.md#failure-points-and-recovery).
* Si el servidor de formularios se está ejecutando pero la carpeta vigilada no se está ejecutando cuando el servicio Administrador de trabajos vuelve a llamar, lo que ocurre cuando los servicios no inicio en la secuencia ordenada, el administrador puede mover los archivos fuera de la carpeta del escenario. Para obtener más información, consulte [Puntos de error y recuperación](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Performance y escalabilidad {#performance-and-scalability}

La carpeta vigilada puede servir 100 carpetas en total en un solo nodo. El rendimiento de la carpeta vigilada depende del rendimiento del servidor de formularios. Para la invocación asincrónica, el rendimiento depende más de la carga del sistema y de los trabajos que se encuentran en la cola de Job Manager.

El rendimiento de la carpeta vigilada se puede mejorar agregando nodos al clúster. Los trabajos de carpetas vigiladas se distribuyen a través de los nodos del clúster en virtud del Planificador de Cuartz y, en el caso de solicitudes asincrónicas, por el servicio Administrador de trabajos. Todos los trabajos se mantienen en la base de datos.

La carpeta vigilada depende del servicio de Planificador para programar, desprogramar y reprogramar los trabajos. Hay otros servicios disponibles, como el servicio de administración de Eventos, el servicio de administración de usuarios y el servicio de proveedor de correo electrónico, que comparten el grupo de subprocesos del servicio de Planificador. Esto puede afectar al rendimiento de la carpeta vigilada. El ajuste del grupo de subprocesos del servicio Planificador será necesario cuando todos los inicios de servicios lo utilicen.

## Carpetas observadas en un clúster {#watched-folders-in-a-cluster}

En un clúster, la carpeta vigilada depende del Planificador de Quartz y del servicio Administrador de trabajos para el equilibrio de carga y la conmutación por error. Para obtener más información sobre el comportamiento del clúster de Quartz, consulte [Documentación de Quartz](https://www.quartz-scheduler.org/documentation).

La carpeta vigilada realiza estas tres tareas principales en cada encuesta:

* Analizar la carpeta
* Invocar el servicio de destinatario
* Administrar los resultados

El equilibrio de carga y el comportamiento de conmutación por error cambian dependiendo de si la carpeta vigilada está configurada para la invocación sincrónica o asincrónica.

### Carpeta observada sincrónica en un clúster {#synchronous-watched-folder-in-a-cluster}

Para las invocaciones sincrónicas, el equilibrador de carga de Quartz decide qué nodo recibirá el evento de sondeo. El nodo que obtiene el evento de sondeo realizará todas las tareas: escanee la carpeta, invoque el servicio de destinatario y gestione los resultados.

![en_synchwatchedfoldercluster](assets/en_synchwatchedfoldercluster.png)

Para las invocaciones sincrónicas, cuando un nodo falla, el Planificador Quartz envía nuevos eventos de sondeo a otros nodos. Se perderán las invocaciones que se iniciaron en el nodo con error. Para obtener más información sobre cómo recuperar los archivos asociados con el trabajo fallido, consulte [Puntos de error y recuperación](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


### Carpeta vigilada asincrónica en un clúster {#asynchronous-watched-folder-in-a-cluster}

Para las invocaciones asincrónicas, el equilibrador de carga de Quartz decide qué nodo recibirá el evento de sondeo. El nodo que obtiene el evento de sondeo analizará la carpeta de entrada e invocará el servicio de destinatario colocando la solicitud en la cola de servicio de Job Manager. El equilibrador de carga del servicio de Job Manager, a su vez, es responsable de decidir qué nodo procesará la solicitud de invocación. Es posible que, aunque el nodo A haya creado la solicitud de invocación, el nodo B termine procesando la solicitud. O bien, el nodo que inició la solicitud de invocación también puede terminar procesando la solicitud.

![en_asynchwatchedfoldercluster](assets/en_asynchwatchedfoldercluster.png)

Para las invocaciones asincrónicas, cuando un nodo falla, el Planificador Quartz envía nuevos eventos de sondeo a otros nodos. Las solicitudes de invocación que se crearon en el nodo con error estarán en la cola de servicio de Job Manager y se enviarán a otros nodos para su procesamiento. Los archivos para los que no se han creado solicitudes de invocación permanecerán en la carpeta stage. Para obtener más información sobre cómo recuperar los archivos asociados con el trabajo fallido, consulte [Puntos de error y recuperación](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Puntos de falla y recuperación {#failure-points-and-recovery}

En cada evento de la encuesta, la carpeta vigilada bloquea la carpeta de entrada, mueve los archivos que coinciden con el patrón de inclusión de archivos a la carpeta del escenario y, a continuación, desbloquea la carpeta de entrada. El bloqueo es necesario para que dos subprocesos no tomen el mismo conjunto de archivos y los procesen dos veces. Las posibilidades de que esto ocurra aumentan con un pequeño intervalo de repetición y un gran tamaño de lote. Después de mover los archivos a la carpeta de escenario, la carpeta de entrada se desbloquea para que otros subprocesos puedan examinar la carpeta. Este paso ayuda a proporcionar un alto rendimiento, ya que otros subprocesos pueden analizarse mientras un subproceso está procesando los archivos.

Una vez que los archivos se mueven a la carpeta stage, se crean solicitudes de invocación para cada archivo y se invoca el servicio de destinatario. Es posible que haya casos en los que la carpeta vigilada no pueda recuperar los archivos de la carpeta del escenario:

* Si el servidor deja de funcionar antes de que la carpeta vigilada pueda crear la solicitud de invocación, los archivos de la carpeta del escenario permanecen en la carpeta del escenario y no se recuperan.
* Si la carpeta vigilada ha creado correctamente la solicitud de invocación para cada uno de los archivos de la carpeta de escenario y el servidor se bloquea, hay dos comportamientos basados en el tipo de invocación:

**Sincrónico:** si la carpeta vigilada está configurada para invocar el servicio sincrónicamente, todos los archivos de la carpeta de escenario permanecen sin procesar en la carpeta de escenario.

**Asincrónico:** en este caso, la carpeta vigilada depende del servicio Administrador de trabajos. Si el servicio de administrador de trabajos devuelve la llamada a la carpeta vigilada, los archivos de la carpeta de etapa se mueven a la carpeta de conservación o error en función de los resultados de la invocación. Si el servicio Administrador de trabajos no devuelve la llamada a la carpeta vigilada, los archivos permanecerán sin procesar en la carpeta del escenario. Esta situación se produce cuando la carpeta vigilada no se está ejecutando cuando el Administrador de trabajos vuelve a llamar.

### Recuperación de archivos de origen no procesados en la carpeta del escenario {#recovering-unprocessed-source-files-in-the-stage-folder}

Cuando la carpeta de inspección no puede procesar los archivos de origen en la carpeta de etapa, puede recuperar los archivos sin procesar.

1. Reinicie el servidor de aplicaciones o el nodo.
1. (Opcional) Impida que la carpeta vigilada procese nuevos archivos de entrada. Si omite este paso, será mucho más difícil determinar qué archivos no se procesan en la carpeta de escenario. Para evitar que la carpeta vigilada procese nuevos archivos de entrada, realice una de las siguientes tareas:

   * En Aplicaciones y servicios, cambie el parámetro Incluir patrón de archivo para el extremo de la carpeta vigilada a algo que no coincida con ninguno de los nuevos archivos de entrada (por ejemplo, escriba `NOMATCH`).
   * Suspenda el proceso de creación de nuevos archivos de entrada.

   Espere hasta que AEM formularios recupere y procese todos los archivos. La mayoría de los archivos deben recuperarse y los nuevos archivos de entrada deben procesarse correctamente. El tiempo que espera a que la carpeta vigilada se recupere y procese los archivos dependerá de la duración de la operación que se invoque y del número de archivos que se recuperarán.

1. Determinar qué archivos no se pueden procesar. Si ha esperado una cantidad de tiempo adecuada y ha completado el paso anterior, y aún quedan archivos sin procesar en la carpeta de escenario, vaya al paso siguiente.

   >[!NOTE]
   >
   >Puede consultar la marca de fecha y hora de los archivos en el directorio de etapas. En función del número de archivos y del tiempo de procesamiento normal, puede determinar qué archivos son lo suficientemente antiguos como para que se los considere atascados.

1. Copie los archivos sin procesar del directorio de etapa al directorio de entrada.
1. Si ha impedido que la carpeta vigilada procese nuevos archivos de entrada en el paso 2, cambie el Patrón de archivos de inclusión a su valor anterior o vuelva a habilitar el proceso que deshabilitó.

## Consideraciones de seguridad para carpetas controladas {#security-considerations-for-watched-folders}

Cada carpeta vigilada se configura con un nombre de usuario y una contraseña. Estas credenciales se utilizan al invocar los servicios. La carpeta vigilada depende del hecho de que la carpeta compartida está protegida con el sistema de archivos de seguridad subyacente, de modo que solo el propietario de la carpeta vigilada puede acceder a la carpeta compartida.

## Sugerencias y trucos para carpetas controladas {#tips-and-tricks-for-watched-folders}

Estos son algunos consejos y trucos al configurar el punto final de la carpeta vigilada:

* Si tiene una carpeta vigilada en Windows que esté procesando archivos de imagen, especifique los valores de la opción Incluir patrón de archivos o Excluir patrón de archivos para evitar que la carpeta vigilada sondee el archivo Thumbs.db generado automáticamente por Windows.
* Si se especifica una expresión cron, se ignora el intervalo de repetición. El uso de la expresión cron se basa en el sistema de programación de trabajos de código abierto Quartz, versión 1.4.0.
* El tamaño del lote es el número de archivos o carpetas que se recogerán en cada análisis de la carpeta vigilada. Si el tamaño del lote se establece en dos y diez archivos o carpetas se sueltan en la carpeta de entrada de la carpeta controlada, solo se recogerán dos en cada análisis. En la siguiente exploración, que se realizará después del tiempo especificado en el intervalo de repetición, se recogerán los dos archivos siguientes.
* En el caso de los patrones de archivo, los administradores pueden especificar expresiones regulares con compatibilidad añadida para los patrones de comodines a fin de especificar los patrones de archivo. La carpeta vigilada modifica la expresión normal para admitir patrones de comodines como &amp;ast;.&amp;ast; o &amp;ast;.pdf. Estos patrones comodín no son compatibles con las expresiones normales.
* Watched Folder busca la entrada en la carpeta de entrada y no sabe si el archivo o la carpeta de origen se han copiado completamente en la carpeta de entrada antes de que inicio el procesamiento del archivo o la carpeta. Para asegurarse de que el archivo o la carpeta de origen se copian completamente en la carpeta de entrada de la carpeta controlada antes de que se recoja el archivo o la carpeta, lleve a cabo las siguientes tareas:

   * Utilice el tiempo de espera, que es el tiempo en milisegundos que la carpeta observada espera desde la última vez que se modificó. Utilice esta función si tiene archivos grandes para procesar. Por ejemplo, si un archivo tarda 10 minutos en descargarse, especifique el tiempo de espera como 10&amp;ast;60 &amp;ast;1000 milisegundos. Esto impedirá que la carpeta vigilada recoja el archivo si no es tan antiguo como 10 minutos.
   * Utilice el patrón de exclusión de archivos e incluya el patrón de archivos. Por ejemplo, si el patrón de archivos de exclusión es `ex*` y el patrón de archivos de inclusión es `in*`, la carpeta vigilada recogerá los archivos que inicio con &quot;in&quot; y no recogerá los archivos que inicio con &quot;ex&quot;. Para copiar archivos o carpetas de gran tamaño, primero cambie el nombre del archivo o de la carpeta para que el nombre inicio con &quot;ex&quot;. Una vez que el archivo o carpeta denominado &quot;ex&quot; se haya copiado completamente en la carpeta vigilada, cámbiele el nombre a &quot;in&amp;ast;&quot;.

* Utilice la duración de purga para mantener limpia la carpeta de resultados. La carpeta vigilada limpia todos los archivos anteriores a la duración mencionada en la duración de la purga. La duración es en días.
* Al agregar un extremo de carpeta vigilada, después de seleccionar el nombre de la operación, se rellena la asignación de parámetros de entrada. Para cada entrada de la operación, se genera un campo de asignación de parámetros de entrada. Estos son ejemplos de asignaciones de parámetros de entrada:

   * Para `com.adobe.idp.Document` entrada: Si la operación de servicio tiene una entrada de tipo `Document`, el administrador puede especificar el tipo de asignación como `Variable`. La carpeta vigilada recogerá la entrada de la carpeta de entrada de la carpeta vigilada según el patrón de archivo especificado para el parámetro de entrada. Si el administrador especifica `*.pdf` como parámetro, cada archivo que tenga una extensión de .pdf se recogerá, se convertirá a `com.adobe.idp.Document` y se invocará el servicio.
   * Para `java.util.Map` entrada: Si la operación de servicio tiene una entrada de tipo `Map`, el administrador puede especificar el tipo de asignación como `Variable` e introducir un valor de asignación con un patrón como `*.pdf`. Por ejemplo, un servicio necesita un mapa de dos objetos `com.adobe.idp.Document` que representan dos archivos en la carpeta de entrada, como 1.pdf y 2.pdf. La carpeta vigilada creará un mapa con la clave como nombre de archivo y el valor como `com.adobe.idp.Document`.
   * Para `java.util.List` entrada: Si la operación de servicio tiene una entrada de tipo Lista, el administrador puede especificar el tipo de asignación como `Variable` e introducir un valor de asignación con un patrón como `*.pdf`. Cuando se quitan los archivos PDF en la carpeta de entrada, Watched Folder creará una lista de los objetos `com.adobe.idp.Document` que representan estos archivos e invocará el servicio destinatario.
   * Para `java.lang.String`: El administrador tiene dos opciones. En primer lugar, el administrador puede especificar el tipo de asignación como `Literal` e introducir un valor de asignación como una cadena, como `hello.` Watched Folder invocará el servicio con la cadena `hello`. En segundo lugar, el administrador puede especificar el tipo de asignación como `Variable` e introducir un valor de asignación con un patrón como `*.txt`. En este último caso, los archivos con la extensión .txt se leerán como un documento forzado como una cadena para invocar el servicio.
   * Tipo primitivo Java: El administrador puede especificar el tipo de asignación como `Literal` y proporcionar el valor. La carpeta vigilada invocará el servicio con el valor especificado.

* La carpeta vigilada está pensada para funcionar con documentos. Los resultados admitidos son `com.adobe.idp.Document`, `org.w3c.Document`, `org.w3c.Node`, así como una lista y un mapa de estos tipos. Cualquier otro tipo dará como resultado un error en la carpeta de error.
* Si los resultados no están en la carpeta de resultados, compruebe la carpeta de errores para ver si se ha producido un error.
* Carpeta vigilada funciona mejor si se utiliza en modo asincrónico. En este modo, la carpeta vigilada coloca la solicitud de invocación en la cola y devuelve las llamadas. A continuación, la cola se procesa asincrónicamente. Cuando no se establece la opción Asincrónico, la carpeta vigilada invoca el servicio de destinatario sincrónicamente y el motor de proceso espera hasta que el servicio se realiza con la solicitud y se producen los resultados. Si el servicio de destinatario tarda mucho en procesar la solicitud, es posible que la carpeta vigilada obtenga errores de tiempo de espera.
* La creación de carpetas vigiladas para operaciones de importación y exportación no permite la abstracción de la extensión del nombre de archivo. Al invocar el servicio de integración de datos de formulario mediante carpetas vigiladas, es posible que el tipo de extensión de nombre de archivo del archivo de salida no coincida con el formato de salida deseado para el tipo de objeto de documento. Por ejemplo, si el archivo de entrada de una carpeta vigilada que invoca la operación de exportación es un formulario XFA que contiene datos, el resultado debe ser un archivo de datos XDP. Para obtener un archivo de salida con la extensión de nombre de archivo correcta, puede especificarlo en la asignación de parámetros de salida. En este ejemplo, puede utilizar %F.xdp para la asignación de parámetros de salida.
* La carpeta vigilada puede procesar los archivos de entrada antes de que se copien completamente en la carpeta. El bloqueo de archivos no es obligatorio en UNIX, como en Windows. Por este motivo, cuando se copia un archivo en una carpeta vigilada, esta puede mover el archivo a la etapa sin esperar a que se complete la copia del archivo. Este comportamiento hace que solo se procese una parte del archivo de entrada. Actualmente hay dos soluciones alternativas:

   * Solución alternativa 1

      1. Especifique un patrón para Excluir patrón de archivo, como temp&amp;ast;.ps.
      1. Copie los archivos que comienzan por temp (por ejemplo, temp1.ps) en la carpeta controlada.
      1. Una vez que el archivo se haya copiado completamente en la carpeta vigilada, cambie el nombre del archivo para que se corresponda con el patrón especificado para Incluir patrón de archivos. Carpeta vigilada luego mueve el archivo completado a la etapa.
   * Solución alternativa 2

      Si sabe cuánto tiempo tardará en copiarse los archivos en una carpeta vigilada, especifique el tiempo en segundos para el tiempo de espera. Carpeta vigilada espera el tiempo especificado antes de mover el archivo a la etapa.

      No se trata de un problema con los archivos de Windows porque Windows bloquea un archivo cuando se escribe un subproceso. Sin embargo, este es un problema para las carpetas de Windows. Para las carpetas, debe seguir los pasos de Solución 1.


* Si el atributo de extremo Conservar nombre de carpeta para la carpeta vigilada está establecido en una ruta de directorio nula, el directorio de ensayo no se elimina como debería estar. El directorio aún contiene el archivo procesado y la carpeta temporal.

## Recomendaciones específicas del servicio para carpetas controladas {#service-specific-recommendations-for-watched-folders}

Para todos los servicios, debe ajustar el tamaño del lote y el intervalo de repetición de la carpeta vigilada para que la velocidad a la que la carpeta vigilada recoge nuevos archivos y carpetas para su procesamiento no supere la velocidad de los trabajos que puede procesar el servidor de formularios AEM. Los parámetros reales que se deben utilizar pueden variar en función de la cantidad de carpetas vigiladas que se hayan configurado, los servicios que utilizan carpetas vigiladas y la intensidad de los trabajos en el procesador.

### Generar recomendaciones de servicio PDF {#generate-pdf-service-recommendations}

* El servicio Generar PDF puede convertir sólo un archivo a la vez para estos tipos de archivo: Microsoft Word, Microsoft Excel, Microsoft PowerPoint, Microsoft Project, AutoCAD, Adobe Photoshop®, Adobe FrameMaker® y Adobe PageMaker®. Se trata de trabajos de larga data; por lo tanto, asegúrese de mantener el tamaño del lote en un valor bajo. También aumente el intervalo de repetición si hay más nodos en el clúster.
* Para los tipos de archivo PostScript (PS), PostScript encapsulado (EPS) y de imagen, el servicio Generar PDF puede procesar varios archivos en paralelo. Debe ajustar cuidadosamente el tamaño del grupo de granos de sesión (que rige el número de conversiones que se realizarán en paralelo) en función de la capacidad del servidor y del número de nodos del clúster. A continuación, aumente el tamaño del lote a un número que sea igual al tamaño del conjunto de granos de sesión para los tipos de archivo que intenta convertir. La frecuencia de sondeo debe estar determinada por el número de nodos del clúster; sin embargo, como el servicio Generar PDF procesa estos tipos de trabajos con bastante rapidez, puede configurar el intervalo de repetición a un valor bajo como 5 o 10.
* Aunque el servicio Generar PDF sólo puede convertir un archivo de OpenOffice a la vez, la conversión es bastante rápida. La lógica anterior para las conversiones de imágenes, PS y EPS también se aplica a las conversiones de OpenOffice.
* Para habilitar una distribución uniforme de la carga en el clúster, mantenga el tamaño del lote bajo y aumente el intervalo de repetición.

### recomendaciones de servicio de formularios con códigos de barras {#barcoded-forms-service-recommendations}

* Para obtener el mejor rendimiento al procesar formularios con códigos de barras (archivos pequeños), introduzca `10` para Tamaño de lote y `2` para Intervalo de repetición.
* Cuando se colocan muchos archivos en la carpeta de entrada, pueden producirse errores con archivos ocultos llamados *thumbs.db*. Por lo tanto, se recomienda configurar el Patrón de archivos de inclusión para los archivos de inclusión con el mismo valor especificado para la variable de entrada (por ejemplo, `*.tiff`). Esto evita que la carpeta vigilada procese los archivos de base de datos.
* Un valor de Tamaño de lote de `5` e Intervalo de repetición de `2` es normalmente suficiente porque el servicio de Forms con códigos de barras normalmente tarda unos 0,5 segundos en procesar un código de barras.
* La carpeta vigilada no espera a que el motor de proceso finalice el trabajo antes de que recopile nuevos archivos o carpetas. Sigue analizando la carpeta vigilada e invocando el servicio de destinatario. Este comportamiento puede sobrecargar el motor, causando problemas de recursos y tiempos de espera. Asegúrese de utilizar el intervalo de repetición y el tamaño del lote para reducir la entrada de la carpeta vigilada. Puede aumentar el intervalo de repetición y reducir el tamaño del lote si existen más carpetas vigiladas o habilitar la limitación en el extremo. Para obtener información sobre la limitación, consulte [Acerca de la limitación](configuring-watched-folder-endpoints.md#about-throttling).
* La carpeta vigilada suplantará al usuario especificado en el nombre de usuario y el nombre de dominio. La carpeta vigilada invoca el servicio como este usuario si se invoca directamente o si el proceso es de corta duración. Para un proceso de larga duración, el proceso se invoca con el contexto del sistema. Los administradores pueden establecer directivas del sistema operativo para la carpeta vigilada a fin de determinar a qué usuario permitir o denegar el acceso.
* Utilice patrones de archivo para organizar los resultados, las fallas y la conservación de carpetas. (Consulte [Acerca de los patrones de archivo](configuring-watched-folder-endpoints.md#about-file-patterns).)

* La carpeta vigilada depende del Planificador Quartz para examinar las carpetas vigiladas. El Planificador Quartz tiene un pool de subprocesos para escanearlos. Si el intervalo de repetición de la carpeta vigilada es muy bajo (&lt; 5 segundos) y el tamaño del lote es alto (> 2), puede producirse una condición de carrera. Cuando se produce esta condición, dos subprocesos de Quartz recogen un archivo:

   * Uno de los subprocesos encuentra correctamente el archivo e invoca el servicio de destinatario con el archivo.
   * El segundo subproceso ve el archivo pero falla cuando intenta averiguar si es válido (archivo de lectura o escritura), lo que provoca errores falsos que indican que el archivo no se puede procesar porque es de sólo lectura. Esto sucede solamente con un intervalo de repetición bajo y un tamaño de lote elevado.

