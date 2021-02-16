---
title: Crear o configurar una carpeta vigilada
seo-title: Crear o configurar una carpeta vigilada
description: Obtenga información sobre cómo crear o eliminar una carpeta vigilada o modificar las propiedades de una carpeta vigilada existente.
seo-description: Obtenga información sobre cómo crear o eliminar una carpeta vigilada o modificar las propiedades de una carpeta vigilada existente.
uuid: 659d4d8c-99b8-40dd-b884-bfee4d476fe1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 0ce7b338-6686-49b3-b58b-e7ab6b670708
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e
workflow-type: tm+mt
source-wordcount: '1844'
ht-degree: 0%

---


# Crear o configurar una carpeta controlada {#create-or-configure-a-watched-folder}

Un administrador puede configurar una carpeta de red, conocida como *carpeta vigilada*, para que cuando un usuario coloque un archivo (como un archivo PDF) en la carpeta vigilada, se inicie una operación preconfigurada y se manipule el archivo. Una vez realizada la operación especificada, la operación guarda el archivo modificado en una carpeta de salida especificada. Para obtener información detallada sobre la administración de una carpeta vigilada, consulte [Ayuda de administración](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md).

Puede utilizar la interfaz de usuario de la carpeta controlada para:

* Creación de una carpeta vigilada
* Modificar propiedades de una carpeta vigilada existente
* Eliminar una carpeta vigilada

## Crear una carpeta vigilada {#create-a-watched-folder}

Antes de configurar una carpeta vigilada, asegúrese de lo siguiente:

* Las carpetas vigiladas son una característica avanzada de AEM formularios. Requiere que funcione AEM paquete de complementos de formularios. Asegúrese de que el paquete adicional de AEM Forms adecuado está instalado y configurado.
* Puede crear la carpeta vigilada en un almacenamiento compartido o local. Asegúrese de que AEM usuario de formularios configurado para ejecutar la carpeta vigilada tiene permisos de lectura y escritura en la carpeta vigilada.
* Puede utilizar un servicio, un flujo de trabajo o una secuencia de comandos para automatizar una operación con una carpeta vigilada. Asegúrese de que el servicio, el flujo de trabajo o una secuencia de comandos correspondientes están creados y listos para ejecutarse. Para obtener información sobre la creación de un servicio, un flujo de trabajo y una secuencia de comandos, consulte [Diversos métodos de procesamiento de archivos](/help/forms/using/watched-folder-in-aem-forms.md#various-methods-for-processing-files).
* Una carpeta vigilada tiene varias propiedades, consulte [Propiedades de la carpeta vigilada](watched-folder-in-aem-forms.md#watchedfolderproperties).

Realice los siguientes pasos para crear una carpeta vigilada:

1. Toque **Adobe Experience Manager** en la esquina superior izquierda de la pantalla.
1. Toque **Herramientas** > **Forms** > **Configurar carpeta vigilada.** Se muestra una lista de las carpetas ya configuradas controladas.
1. Toque **Nuevo**. Se muestra una lista de los campos necesarios para crear la carpeta controlada:

   * **Nombre**: Identifica la carpeta vigilada. Utilice sólo caracteres alfanuméricos para el nombre.
   * **Ruta**: Especifica la ubicación de la carpeta vigilada. En un entorno agrupado, esta configuración debe apuntar a una carpeta de red compartida a la que puedan acceder todos los usuarios que ejecuten AEM en diferentes nodos de un clúster.
   * **Procesar archivos usando**: Tipo de proceso que se va a inicio. Puede especificar el flujo de trabajo, la secuencia de comandos o el servicio.
   * **Nombre del servicio/Ruta de script/Ruta** del flujo de trabajo: El comportamiento del campo se basa en el valor especificado para el campo  **Procesar archivos** usando. Puede especificar los siguientes valores:

      * Para Flujo de trabajo, especifique el modelo de flujo de trabajo que se va a ejecutar. Por ejemplo, /etc/workflow/models/&lt;nombre_de_workflow>/jcr:content/model
      * Para Script, especifique la ruta de JCR de la secuencia de comandos que se va a ejecutar. Por ejemplo, /etc/watchfolder/test/testScript.ecma
      * En Servicio, especifique el filtro utilizado para localizar un servicio OSGi. El servicio está registrado como una implementación de la interfaz com.adobe.aemfd.watchfolder.service.api.ContentProcessor. Por ejemplo, el siguiente código es una implementación personalizada de la interfaz ContentProcessor con una propiedad personalizada (foo=bar).

   >[!NOTE]
   >
   >Si ha seleccionado **Servicio** para el campo **Procesar archivos usando**, el valor del campo Nombre del servicio (inputProcessorType) se debe incluir entre paréntesis. Por ejemplo, (foo=bar).

   ```java
   @Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
   @Service(value = {OutputWriter.class, ContentProcessor.class})
   @Property(name = "foo", value = "bar")
   public class OutputWriter implements ContentProcessor {
   ```

   * **Patrón** de archivo de salida: Especifique una lista delimitada por punto y coma (;) de los patrones que utiliza una carpeta vigilada para determinar el nombre y la ubicación de los archivos y carpetas de salida. Para obtener más información sobre los patrones de archivo, consulte [Acerca de los patrones de archivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).


1. Toque **Avanzado**. La ficha avanzada contiene más campos. La mayoría de estos campos contienen un valor predeterminado.

   * **Filtro de asignador de carga útil:** cuando se crea una carpeta vigilada, se crea una estructura de carpetas dentro de la carpeta que se está viendo. La estructura de carpetas tiene carpetas de etapa, resultado, conservación, entrada y error. La estructura de carpetas puede servir como carga útil de entrada para el flujo de trabajo y aceptar resultados de un flujo de trabajo. También puede lista puntos de error, si los hay. La estructura de una carga útil es diferente de la de una carpeta vigilada. Puede escribir secuencias de comandos personalizadas para asignar la estructura de una carpeta vigilada a la carga útil. Esta secuencia de comandos se denomina filtro de mapeador de carga útil. Hay dos implementaciones de mapeador de carga útil integradas disponibles. Si no tiene [una implementación personalizada](/help/forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter), utilice una implementación lista para usar:

      * **Asignador predeterminado:** utilice el asignador de carga útil predeterminado para mantener el contenido de entrada y salida de las carpetas vigiladas en carpetas de entrada y salida independientes en la carga útil.
      * **Asignador de carga útil simple basado en archivos:** utilice el asignador de carga útil simple basado en archivos para mantener el contenido de entrada y salida directamente en la carpeta de carga útil. No crea ninguna jerarquía adicional, como el asignador predeterminado.
   * **Modo** de ejecución: Especifique la lista separada por comas de los modos de ejecución permitidos para la ejecución del flujo de trabajo.
   * **Tiempo de espera de archivos escalonados después** de: Especifique el número de segundos de espera antes de que un archivo o carpeta de entrada que ya se ha seleccionado para el procesamiento se trate como si se hubiera agotado el tiempo de espera y se hubiera marcado como un error. El mecanismo de tiempo de espera solo se activa cuando el valor de esta propiedad es un número positivo.
   * **Eliminar los archivos escalonados con tiempo de espera agotado al activarlos**: Si está activado, el mecanismo  **Tiempo de espera de archivos escalonados** Aftermecanismo solo se activa cuando se activa la limitación de la carpeta vigilada.
   * **Analizar la carpeta de entrada después de cada:** especifique el intervalo de tiempo, en segundos, para buscar entradas en la carpeta vigilada. A menos que se habilite la configuración de aceleración, el intervalo de encuesta debe ser mayor que el tiempo para procesar un trabajo promedio; de lo contrario, el sistema podría sobrecargarse. El valor del intervalo debe ser bueno o igual a uno.
   * **Patrón** de exclusión de archivos: Especifique una lista delimitada por punto y coma (;) de los patrones que utiliza una carpeta vigilada para determinar qué archivos y carpetas se deben analizar y recoger. No se analiza para su procesamiento ningún archivo o carpeta con el patrón especificado. Para obtener más información sobre los patrones de archivo, consulte [Acerca de los patrones de archivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Incluir patrón** de archivos: Especifique una lista delimitada por punto y coma (;) de los patrones que utiliza la carpeta vigilada para determinar qué carpetas y archivos se deben analizar y recoger. Por ejemplo, si el Patrón de archivos de inclusión es input&amp;ast;, todos los archivos y carpetas que coincidan con input&amp;ast; son recogidos. El valor predeterminado es &amp;ast; e indica todos los archivos y carpetas. Para obtener más información sobre los patrones de archivo, consulte [Acerca de los patrones de archivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Tiempo de espera:** especifique el tiempo, en milisegundos, que debe esperar antes de analizar una carpeta o archivo después de crearlo. Por ejemplo, si el tiempo de espera es de 3.600.000 milisegundos (una hora) y el archivo se creó hace un minuto, este archivo se recuperará después de que hayan transcurrido 59 minutos o más. El valor predeterminado es 0.

      Esta opción resulta útil para asegurarse de que todo el contenido del archivo o la carpeta se copia en la carpeta de entrada. Por ejemplo, si tiene un archivo grande para procesar y el archivo tarda diez minutos en descargarse, establezca el tiempo de espera en 10&amp;ast;60 &amp;ast;1000 milisegundos. Este intervalo evita que la carpeta vigilada analice el archivo si no tiene diez minutos de antigüedad.

   * **Eliminar resultados anteriores a:** especifique el tiempo, en número de días, que se debe esperar antes de eliminar los archivos y carpetas anteriores al valor especificado. Esta configuración es útil para garantizar que la carpeta de resultados no se llena. Un valor de -1 días indica que nunca se elimina la carpeta de resultados. El valor predeterminado es -1.
   * **Nombre de la carpeta de resultados:** especifique el nombre de la carpeta en la que desea almacenar los resultados. Si los resultados no aparecen en esta carpeta, compruebe la carpeta de errores. Los archivos de sólo lectura no se procesan y se guardan en la carpeta de errores. Puede utilizar una ruta absoluta o relativa con los siguientes patrones de archivo:

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
      * Por ejemplo, si es a las 8 pm del 17 de julio de 2009 y especifica C:/Test/WF0/fail/%Y/%M/%D/%H/, la carpeta de resultados es C:/Test/WF0/fail/2009/07/17/20.
      * Si la ruta no es absoluta sino relativa, la carpeta se crea dentro de la carpeta controlada. El valor predeterminado es result/%Y/%M/%D/, que es la carpeta Result dentro de la carpeta observada. Para obtener más información sobre los patrones de archivo, consulte [Acerca de los patrones de archivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Nombre de la carpeta de errores:** especifique la carpeta en la que se guardarán los archivos con errores. Esta ubicación siempre es relativa a la carpeta vigilada. Puede utilizar patrones de archivo, como se describe en Carpeta de resultados.
   * **Conservar nombre de la carpeta:** especifique la carpeta en la que se almacenan los archivos tras realizar correctamente la digitalización y la recogida. La ruta puede ser absoluta, relativa o nula. Puede utilizar patrones de archivo, como se describe en Carpeta de resultados. El valor predeterminado es preserve/%Y/%M/%D/.
   * **Tamaño de lote:** especifique el número de archivos o carpetas que se van a buscar por análisis. Evita una sobrecarga en el sistema; el análisis de demasiados archivos al mismo tiempo puede provocar un bloqueo. El valor predeterminado es 2.

      Si el intervalo de exploración es pequeño, los subprocesos analizan la carpeta de entrada con frecuencia. Si los archivos se sueltan con frecuencia en la carpeta vigilada, debe reducir el intervalo de exploración. Si los archivos se retiran con poca frecuencia, utilice un intervalo de exploración mayor para que los demás servicios puedan utilizar los subprocesos.

   * **Activación del acelerador:** cuando esta opción está activada, limita el número de trabajos de carpeta observados que se procesan en los formularios en un momento dado. El valor Tamaño de lote determina el número máximo de trabajos. Para obtener más información, consulte [limitación](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-throttling)
   * **Sobrescribir archivos existentes con un nombre** similar: Cuando se establece en True, se sobrescriben los archivos de la carpeta de resultados y la carpeta de preservación. Cuando se establece en False, se utilizan para el nombre archivos y carpetas con un sufijo de índice numérico. El valor predeterminado es False.
   * **Conservar archivos si se produce un error:** cuando se establece en True, los archivos de entrada se conservan en caso de error. El valor predeterminado es true.
   * **Incluir archivos con patrón:** especifique una lista delimitada por punto y coma (;) de los patrones que utiliza la carpeta vigilada para determinar qué carpetas y archivos se deben analizar y recoger. Por ejemplo, si se introduce el Patrón de archivos de inclusión, se recogen todos los archivos y carpetas que coinciden con los datos introducidos. Para obtener más información, consulte [Ayuda de administración](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)
   * **Invocar carpeta vigilada asincrónicamente:** identifica el tipo de invocación como asíncrono o sincrónico. El valor predeterminado es asincrónico. Se recomienda la asincrónica para procesos de larga duración, mientras que la sincrónica se recomienda para procesos transitorios o de corta duración.
   * **Activar carpeta vigilada:** cuando esta opción está activada, la carpeta de inspección está activada. El valor predeterminado es True.



## Modificar propiedades de una carpeta observada existente {#modify-properties-of-an-existing-watched-folder}

Además de cambiar el nombre de la carpeta vigilada, puede modificar todas las propiedades de una carpeta observada existente. Realice los siguientes pasos para modificar las propiedades de una carpeta vigilada existente:

1. Toque el icono **Adobe Experience Manager** en la esquina superior izquierda de la pantalla.
1. Toque **Herramientas** > **Forms** > **Configurar carpeta vigilada.** Se muestra una lista de las carpetas ya configuradas controladas.
1. En la parte izquierda de la pantalla Carpeta vigilada, seleccione la carpeta de inspección y toque **Editar.** Se muestra una lista de los campos necesarios para crear la carpeta vigilada. Los campos enumerados en la ficha **Básico** son obligatorios. La ficha avanzada contiene más campos. La mayoría de estos campos contienen un valor predeterminado. Puede modificar estas propiedades según sus necesidades.
1. Después de modificar las propiedades, toque **Actualizar**. Las propiedades modificadas se guardan.

