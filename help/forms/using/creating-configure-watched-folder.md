---
title: Crear o configurar una carpeta vigilada
seo-title: Create or Configure a watched folder
description: Obtenga información sobre cómo crear o eliminar una carpeta vigilada, o modificar las propiedades de una carpeta observada existente.
seo-description: Learn how to create or delete a watched folder, or modify the properties of an existing watched folder.
uuid: 659d4d8c-99b8-40dd-b884-bfee4d476fe1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 0ce7b338-6686-49b3-b58b-e7ab6b670708
exl-id: b15d8d3b-5e47-4c33-95fe-440fcf96be83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 0%

---

# Crear o configurar una carpeta vigilada {#create-or-configure-a-watched-folder}

Un administrador puede configurar una carpeta de red, conocida como *carpeta vigilada*, de modo que cuando un usuario coloca un archivo (como un archivo PDF) en la carpeta vigilada, se inicia una operación preconfigurada y se manipula el archivo. Una vez realizada la operación especificada, la operación guarda el archivo modificado en una carpeta de salida especificada. Para obtener información detallada sobre la administración de una carpeta vigilada, consulte [Ayuda de administración](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md).

Puede utilizar la interfaz de usuario de la carpeta observada para:

* Crear una carpeta vigilada
* Modificar propiedades de una carpeta vigilada existente
* Eliminar una carpeta vigilada

## Crear una carpeta vigilada {#create-a-watched-folder}

Antes de configurar una carpeta vigilada, asegúrese de lo siguiente:

* Las carpetas vigiladas son una característica avanzada de los formularios AEM. Requiere AEM paquete de complementos de formularios para funcionar. Asegúrese de que el paquete de complementos de AEM Forms adecuado esté instalado y configurado.
* Puede crear la carpeta vigilada en un almacenamiento compartido o local. Asegúrese de que AEM usuario de formularios configurado para ejecutar la carpeta vigilada tenga permisos de lectura y escritura en la carpeta vigilada.
* Puede utilizar un servicio, un flujo de trabajo o un script para automatizar una operación con una carpeta vigilada. Asegúrese de que el servicio, el flujo de trabajo o un script correspondiente estén creados y listos para ejecutarse. Para obtener información sobre la creación de un servicio, un flujo de trabajo y una secuencia de comandos, consulte [Varios métodos de procesamiento de archivos](/help/forms/using/watched-folder-in-aem-forms.md#various-methods-for-processing-files).
* Una carpeta vigilada tiene varias propiedades, consulte [Propiedades de carpeta vigilada](watched-folder-in-aem-forms.md#watchedfolderproperties).

Realice los siguientes pasos para crear una carpeta vigilada:

1. Toque **Adobe Experience Manager** en la esquina superior izquierda de la pantalla.
1. Toque **Herramientas** > **Forms** > **Configurar la carpeta vigilada.** Se muestra una lista de las carpetas ya configuradas.
1. Toque **Nuevo**. Se muestra una lista de los campos necesarios para crear la carpeta vigilada:

   * **Nombre**: Identifica la carpeta vigilada. Utilice solo caracteres alfanuméricos para el nombre.
   * **Ruta**: Especifica la ubicación de la carpeta vigilada. En un entorno agrupado, esta configuración debe apuntar a una carpeta de red compartida a la que puedan acceder todos los usuarios que ejecuten AEM en diferentes nodos de un clúster.
   * **Procesar archivos usando**: Tipo de proceso que se va a iniciar. Puede especificar el flujo de trabajo, la secuencia de comandos o el servicio.
   * **Nombre de servicio/Ruta de script/Ruta de flujo de trabajo**: El comportamiento del campo se basa en el valor especificado para la variable **Procesar archivos usando** campo . Puede especificar los siguientes valores:

      * Para Workflow, especifique el modelo de flujo de trabajo que se va a ejecutar. Por ejemplo, /etc/workflow/models/&lt;workflow_name>/jcr:content/model
      * Para Script, especifique la ruta JCR del script que se va a ejecutar. Por ejemplo, /etc/watchfolder/test/testScript.ecma
      * En Servicio, especifique el filtro utilizado para localizar un servicio OSGi. El servicio está registrado como una implementación de la interfaz com.adobe.aemfd.watchfolder.service.api.ContentProcessor . Por ejemplo, el siguiente código es una implementación personalizada de la interfaz ContentProcessor con una propiedad personalizada (foo=bar).

   >[!NOTE]
   >
   >Si ha seleccionado **Servicio** para el **Procesar archivos usando** , el valor del campo Service Name(inputProcessorType) debe incluirse entre paréntesis. Por ejemplo, (foo=bar).

   ```java
   @Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
   @Service(value = {OutputWriter.class, ContentProcessor.class})
   @Property(name = "foo", value = "bar")
   public class OutputWriter implements ContentProcessor {
   ```

   * **Patrón de archivo de salida**: Especifique una lista delimitada por punto y coma (;) de patrones que usa una carpeta vigilada para determinar el nombre y la ubicación de los archivos y carpetas de salida. Para obtener más información sobre los patrones de archivo, consulte [Acerca de los patrones de archivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).


1. Toque **Avanzadas**. La pestaña advanced contiene más campos. La mayoría de estos campos contienen un valor predeterminado.

   * **Filtro de asignador de carga útil:** Cuando se crea una carpeta vigilada, se crea una estructura de carpetas dentro de la carpeta que se está viendo. La estructura de carpetas tiene carpetas de etapa, resultado, conservación, entrada y error. La estructura de carpetas puede servir como carga útil de entrada al flujo de trabajo y aceptar la salida de un flujo de trabajo. También puede enumerar los puntos de error, si los hay. La estructura de una carga útil es diferente de la de una carpeta vigilada. Puede escribir secuencias de comandos personalizadas para asignar la estructura de una carpeta vigilada a la carga útil. Este script se denomina filtro de mapeo de carga útil. Hay dos implementaciones de mapeo de carga útil listas para usar disponibles. Si no tiene [una implementación personalizada](/help/forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter), utilice una implementación predeterminada:

      * **Asignador predeterminado:** Utilice el asignador de carga útil predeterminado para mantener el contenido de entrada y salida de las carpetas vigiladas en carpetas de entrada y salida independientes en la carga útil.
      * **Asignador de carga útil basado en archivos simple:** Utilice el asignador de carga útil basado en archivos simples para mantener el contenido de entrada y salida directamente en la carpeta de carga útil. No crea ninguna jerarquía adicional, como el asignador predeterminado.
   * **Ejecutar modo**: Especifique la lista separada por comas de modos de ejecución permitidos para la ejecución del flujo de trabajo.
   * **Tiempo de espera agotado: archivos clasificados después de**: Especifique el número de segundos que hay que esperar antes de que un archivo o carpeta de entrada que ya se haya seleccionado para el procesamiento se trate como si se hubiera agotado el tiempo de espera y se haya marcado como un error. El mecanismo de tiempo de espera solo se activa cuando el valor de esta propiedad es un número positivo.
   * **Eliminar archivos clasificados con tiempo de espera agotado al activarlos**: Si está activado, la variable **Tiempo de espera agotado: archivos clasificados después de** El mecanismo de solo se activa cuando se activa la restricción para la carpeta vigilada.
   * **Analizar carpeta de entrada después de cada:** Especifique el intervalo de tiempo, en segundos, para buscar entradas en la carpeta vigilada. A menos que el ajuste Aceleración esté habilitado, el intervalo de sondeo debe ser mayor que el tiempo para procesar un trabajo promedio; de lo contrario, el sistema podría sobrecargarse. El valor del intervalo debe ser bueno o igual a uno.
   * **Patrón de exclusión de archivo**: Especifique una lista delimitada por punto y coma (;) de patrones que usa una carpeta vigilada para determinar qué archivos y carpetas analizar y recoger. Ningún archivo o carpeta con el patrón especificado se analiza para su procesamiento. Para obtener más información sobre los patrones de archivo, consulte [Acerca de los patrones de archivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Patrón de archivo de inclusión**: Especifique una lista delimitada por punto y coma (;) de patrones que la carpeta vigilada usa para determinar qué carpetas y archivos analizar y recoger. Por ejemplo, si el Patrón de archivo de inclusión es input&amp;ast;, todos los archivos y carpetas que coincidan con input&amp;ast; son recogidos. El valor predeterminado es &amp;ast; e indica todos los archivos y carpetas. Para obtener más información sobre los patrones de archivo, consulte [Acerca de los patrones de archivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Tiempo de espera:** Especifique el tiempo, en milisegundos, de espera antes de analizar una carpeta o archivo después de crearlo. Por ejemplo, si el tiempo de espera es de 3 600 000 milisegundos (una hora) y el archivo se creó hace un minuto, el archivo se recopilará después de que hayan transcurrido 59 minutos o más. El valor predeterminado es 0.

      Esta configuración es útil para asegurarse de que todo el contenido del archivo o la carpeta se copia en la carpeta de entrada. Por ejemplo, si tiene un archivo grande para procesar y el archivo tarda diez minutos en descargarse, establezca el tiempo de espera en 10&amp;ast;60 &amp;ast;1000 milisegundos. Este intervalo evita que la carpeta vigilada analice el archivo si no tiene diez minutos de antigüedad.

   * **Eliminar resultados anteriores a:** Especifique el tiempo, en número de días, de espera antes de eliminar los archivos y carpetas anteriores al valor especificado. Esta configuración es útil para garantizar que la carpeta de resultados no esté llena. El valor de -1 días indica que nunca se eliminará la carpeta de resultados. El valor predeterminado es -1.
   * **Nombre de la carpeta de resultados:** Especifique el nombre de la carpeta para almacenar los resultados. Si los resultados no aparecen en esta carpeta, compruebe la carpeta de errores. Los archivos de solo lectura no se procesan y se guardan en la carpeta de errores. Puede utilizar una ruta absoluta o relativa con los siguientes patrones de archivo:

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
      * Por ejemplo, si es 8 PM el 17 de julio de 2009 y especifica C:/Test/WF0/failure/%Y/%M/%D/%H/, la carpeta de resultados es C:/Test/WF0/failure/2009/07/17/20.
      * Si la ruta no es absoluta sino relativa, la carpeta se crea dentro de la carpeta vigilada. El valor predeterminado es result/%Y/%M/%D/, que es la carpeta Result dentro de la carpeta observada. Para obtener más información sobre los patrones de archivo, consulte [Acerca de los patrones de archivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Nombre de la carpeta de errores:** Especifique la carpeta en la que se guardan los archivos con errores. Esta ubicación siempre es relativa a la carpeta vigilada. Puede utilizar patrones de archivo, tal como se describe para la carpeta de resultados.
   * **Conservar nombre de carpeta:** Especifique la carpeta en la que se almacenan los archivos después de realizar el análisis y la recogida con éxito. La ruta puede ser un directorio absoluto, relativo o nulo. Puede utilizar patrones de archivo, tal como se describe para la carpeta de resultados. El valor predeterminado es preserve/%Y/%M/%D/.
   * **Tamaño del lote:** Especifique el número de archivos o carpetas que se recogerán por análisis. Evita una sobrecarga en el sistema; el análisis de demasiados archivos al mismo tiempo puede provocar un bloqueo. El valor predeterminado es 2.

      Si el intervalo de análisis es pequeño, los subprocesos analizan la carpeta de entrada con frecuencia. Si los archivos se sueltan con frecuencia en la carpeta vigilada, debe reducir el intervalo de análisis. Si los archivos se pierden con poca frecuencia, utilice un intervalo de exploración mayor para que los demás servicios puedan utilizar los subprocesos.

   * **Acelerador activado:** Cuando esta opción está habilitada, limita el número de trabajos de carpeta observados que AEM los procesos de formularios en un momento dado. El valor Tamaño de lote determina el número máximo de trabajos. Para obtener más información, consulte [restricción](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-throttling)
   * **Sobrescribir archivos existentes con un nombre similar**: Cuando se establece en True, los archivos de la carpeta de resultados y de la carpeta de preservación se sobrescriben. Cuando se establece en False, se utilizan archivos y carpetas con un sufijo de índice numérico para el nombre. El valor predeterminado es False.
   * **Conservar archivos en caso de error:** Cuando se establece en True, los archivos de entrada se conservan en caso de error. El valor predeterminado es true.
   * **Incluir archivos con patrón:** Especifique una lista delimitada por punto y coma (;) de patrones que la carpeta vigilada usa para determinar qué carpetas y archivos analizar y recoger. Por ejemplo, si se introduce el Patrón de archivo de inclusión, se recogen todos los archivos y carpetas que coincidan con la entrada. Para obtener más información, consulte [Ayuda de administración](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)
   * **Invocar la carpeta vigilada asincrónicamente:** Identifica el tipo de invocación como asíncrono o sincrónico. El valor predeterminado es asíncrono. Se recomienda asincrónico para procesos de larga duración, mientras que sincrónico para procesos transitorios o de corta duración.
   * **Habilitar carpeta vigilada:** Cuando esta opción está activada, la carpeta del reloj está activada. El valor predeterminado es True.



## Modificar propiedades de una carpeta vigilada existente {#modify-properties-of-an-existing-watched-folder}

Además de cambiar el nombre de la carpeta vigilada, puede modificar todas las propiedades de una carpeta observada existente. Realice los siguientes pasos para modificar las propiedades de una carpeta vista existente:

1. Toque . **Adobe Experience Manager** en la esquina superior izquierda de la pantalla.
1. Toque **Herramientas** > **Forms** > **Configurar la carpeta vigilada.** Se muestra una lista de las carpetas ya configuradas.
1. En la parte izquierda de la pantalla Carpeta vigilada, seleccione la carpeta de inspección y pulse **Editar.** Se muestra una lista de los campos necesarios para crear la carpeta vigilada. Los campos enumerados en la **Básico** Las pestañas son obligatorias. La pestaña advanced contiene más campos. La mayoría de estos campos contienen un valor predeterminado. Puede modificar estas propiedades según sus necesidades.
1. Después de modificar las propiedades, pulse **Actualizar**. Las propiedades modificadas se guardan.
