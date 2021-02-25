---
title: Administración de extremos mediante programación
seo-title: Administración de extremos mediante programación
description: Utilice el servicio de Registro de Extremos para agregar extremos de EJB, agregar puntos finales de SOAP, agregar puntos finales de carpetas vigiladas, agregar puntos finales de correo electrónico, agregar puntos finales de Remoting, agregar puntos finales de Administrador de Tareas, modificar puntos finales, eliminar puntos finales y recuperar información del conector del extremo.
seo-description: Utilice el servicio de Registro de Extremos para agregar extremos de EJB, agregar puntos finales de SOAP, agregar puntos finales de carpetas vigiladas, agregar puntos finales de correo electrónico, agregar puntos finales de Remoting, agregar puntos finales de Administrador de Tareas, modificar puntos finales, eliminar puntos finales y recuperar información del conector del extremo.
uuid: 5dc50946-3323-4c5d-a43b-31c1c980bd04
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 076889a7-9c9f-4b6f-a45b-67a9b3923c36
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '10863'
ht-degree: 1%

---


# Administración programada de extremos {#programmatically-managing-endpoints}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en el entorno JEE.**

**Acerca del Servicio de Registro de Extremos**

El servicio de registro de extremos permite administrar los extremos mediante programación. Por ejemplo, puede agregar los siguientes tipos de extremos a un servicio:

* EJB
* SOAP
* Carpeta vigilada
* Correo electrónico
* (obsoleto para formularios AEM) Remoting
* Administrador de tareas

>[!NOTE]
>
>SOAP, EJB y (obsoleto para formularios AEM en JEE) Los extremos de reubicación se crean automáticamente para cada servicio activado. Los extremos SOAP y EJB habilitan SOAP y EJB para todas las operaciones de servicio.

Un extremo Remoting permite a los clientes de Flex invocar operaciones en el servicio AEM Forms al que se agrega el extremo. Se crea un destino de Flex con el mismo nombre que el extremo y los clientes de Flex pueden crear objetos remotos que apunten a este destino para invocar operaciones en el servicio relevante.

Los extremos Correo electrónico, Administrador de Tareas y Carpeta vigilada exponen solo una operación específica del servicio. Para añadir estos extremos se requiere un segundo paso de configuración para seleccionar un método que se invocará, definir parámetros de configuración y especificar asignaciones de parámetros de entrada y salida.

Puede organizar los extremos de TaskManager en grupos llamados *categorías*. A continuación, estas categorías se exponen a Workspace a través de TaskManager. Los usuarios finales ven los extremos de TaskManager a medida que se clasifican. En Workspace, los usuarios finales ven estas categorías en el panel de navegación. Los extremos de cada categoría se muestran como tarjetas de proceso en la página Procesos de Inicio de Workspace.

Puede realizar estas tareas mediante el servicio Endpoint Registry:

* Añadir extremos de EJB. (Consulte [Añadir extremos de EJB](programmatically-endpoints.md#adding-ejb-endpoints).)
* Añada los extremos de SOAP. (Consulte [Añadir extremos de SOAP](programmatically-endpoints.md#adding-soap-endpoints).)
* Añadir extremos de carpetas vigiladas (consulte [Añadir extremos de carpetas vigiladas](programmatically-endpoints.md#adding-watched-folder-endpoints)).
* Añadir los extremos de correo electrónico. (Consulte [Añadir extremos de correo electrónico](programmatically-endpoints.md#adding-email-endpoints).)
* Añadir los extremos de Remoting. (Consulte [Añadir extremos remotos](programmatically-endpoints.md#adding-remoting-endpoints)).
* Añadir extremos de TaskManager (consulte [Añadir extremos de TaskManager](programmatically-endpoints.md#adding-taskmanager-endpoints)).
* Modifique los extremos (consulte [Modificación de extremos](programmatically-endpoints.md#modifying-endpoints)).
* Eliminar extremos (consulte [Eliminación de extremos](programmatically-endpoints.md#removing-endpoints)).
* Recuperar información del conector del extremo (Consulte [Recuperación de información del conector del extremo](programmatically-endpoints.md#retrieving-endpoint-connector-information)).

## Añadir extremos de EJB {#adding-ejb-endpoints}

Puede agregar mediante programación un extremo EJB a un servicio mediante la API de Java de AEM Forms. Al agregar un punto final de EJB a un servicio, está habilitando una aplicación cliente para que invoque el servicio mediante el modo EJB. Es decir, al establecer las propiedades de conexión necesarias para invocar AEM Forms, puede seleccionar el modo EJB. (Consulte [Configuración de propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>No se puede agregar un extremo EJB mediante servicios Web.

>[!NOTE]
>
>Normalmente, se agrega un extremo EJB a un servicio de forma predeterminada. Sin embargo, se puede agregar un extremo EJB a un proceso implementado mediante programación o cuando se ha eliminado un extremo EJB y se debe volver a agregar.

### Resumen de los pasos {#summary-of-steps}

Para agregar un extremo EJB a un servicio, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto `EndpointRegistry Client`.
1. Defina los atributos de extremo de EJB.
1. Cree un punto final de EJB.
1. Habilite el punto final.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss Application Server)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creación de un objeto EndpointRegistry Client**

Para poder agregar mediante programación un punto final de EJB, debe crear un objeto `EndpointRegistryClient`.

**Definir atributos de extremo de EJB**

Para crear un punto final de EJB para un servicio, especifique los siguientes valores:

* **Identificador** del conector: Especifica el tipo de extremo que se va a crear. Para crear un punto final de EJB, especifique `EJB`.
* **Descripción**: Especifica la descripción del extremo.
* **Nombre**: Especifica el nombre del extremo.
* **Identificador** de servicio: Especifica el servicio al que pertenece el extremo.
* **Nombre** de la operación: Especifica el nombre de la operación que se invoca mediante el extremo. Al crear un punto final de EJB, especifique un carácter comodín ( `*`). Sin embargo, si desea especificar una operación específica en lugar de invocar todas las operaciones de servicio, especifique el nombre de la operación en lugar de utilizar el carácter comodín ( `*`).

**Crear un punto final de EJB**

Después de definir los atributos de extremo de EJB, puede crear un extremo de EJB para un servicio.

**Habilitar el extremo**

Después de crear un nuevo extremo, debe habilitarlo. Después de habilitar el extremo, se puede utilizar para invocar el servicio. Después de habilitar el punto final, puede vista dentro de la consola de administración.

**Consulte también**

[Añadir un extremo EJB mediante la API de Java](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Añadir un extremo EJB mediante la API de Java {#adding-an-ejb-endpoint-using-the-java-api}

Añada un punto final de EJB mediante la API de Java:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clases del proyecto Java. (

1. Cree un objeto EndpointRegistry Client.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EndpointRegistryClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Defina los atributos de extremo de EJB.

   * Cree un objeto `CreateEndpointInfo` utilizando su constructor.
   * Especifique el valor del identificador del conector invocando el método `CreateEndpointInfo` del objeto `setConnectorId` y pasando el valor de cadena `EJB`.
   * Especifique la descripción del punto final invocando el método `CreateEndpointInfo` del objeto `setDescription` y pasando un valor de cadena que describe el punto final.
   * Especifique el nombre del extremo invocando el método `CreateEndpointInfo` del objeto `setName` y pasando un valor de cadena que especifica el nombre.
   * Especifique el servicio al que pertenece el extremo invocando el método `CreateEndpointInfo` del objeto `setServiceId` y pasando un valor de cadena que especifica el nombre del servicio.
   * Especifique la operación que se invoca invocando el método `CreateEndpointInfo` del objeto `setOperationName` y pase un valor de cadena que especifique el nombre de la operación. Para los extremos SOAP y EJB, especifique un carácter comodín ( `*`), lo que implica todas las operaciones.

1. Cree un punto final de EJB.

   Cree el punto final invocando el método `EndpointRegistryClient` del objeto `createEndpoint` y pasando el objeto `CreateEndpointInfo`. Este método devuelve un objeto `Endpoint` que representa el nuevo extremo de EJB.

1. Habilite el punto final.

   Habilite el punto final invocando el método enable del objeto `EndpointRegistryClient` y pasando el objeto `Endpoint` devuelto por el método `createEndpoint`.

**Consulte también**

[Resumen de los pasos](programmatically-endpoints.md#summary-of-steps)

[Inicio rápido: Añadir un extremo EJB mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Añadir extremos de SOAP {#adding-soap-endpoints}

Puede agregar mediante programación un extremo SOAP a un servicio mediante la API de Java de AEM Forms. Al agregar un extremo SOAP, se habilita una aplicación cliente para invocar el servicio mediante el modo SOAP. Es decir, al establecer las propiedades de conexión necesarias para invocar AEM Forms, puede seleccionar el modo SOAP.

>[!NOTE]
>
>No se puede agregar un extremo SOAP mediante servicios Web.

>[!NOTE]
>
>Normalmente, se agrega un extremo SOAP a un servicio de forma predeterminada. Sin embargo, se puede agregar un extremo SOAP a un proceso implementado mediante programación o cuando se quitó un extremo SOAP y se debe agregar de nuevo.

### Resumen de los pasos {#summary_of_steps-1}

Para agregar un extremo SOAP a un servicio, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto `EndpointRegistryClient`.
1. Defina los atributos del extremo SOAP.
1. Cree un extremo SOAP.
1. Habilite el punto final.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss Application Server)

Estos archivos JAR son necesarios para crear un extremo SOAP. Sin embargo, se requieren archivos JAR adicionales si se utiliza el extremo SOAP para invocar el servicio. Para obtener información sobre los archivos JAR de AEM Forms, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creación de un objeto EndpointRegistry Client**

Para agregar mediante programación un extremo SOAP a un servicio, debe crear un objeto `EndpointRegistryClient`.

**Definir atributos de extremo SOAP**

Para agregar un extremo SOAP a un servicio, especifique los siguientes valores:

* **Valor** del identificador del conector: Especifica el tipo de extremo que se va a crear. Para crear un extremo SOAP, especifique `SOAP`.
* **Descripción**: Especifica la descripción del extremo.
* **Nombre**: Especifica el nombre del extremo.
* **Valor** del identificador de servicio: Especifica el servicio al que pertenece el extremo.
* **Nombre** de la operación: Especifica el nombre de la operación que se invoca mediante el extremo. Al crear un extremo SOAP, especifique un carácter comodín ( `*`). Sin embargo, si desea especificar una operación específica en lugar de invocar todas las operaciones de servicio, especifique el nombre de la operación en lugar de utilizar el carácter comodín ( `*`).

**Creación de un extremo SOAP**

Después de definir atributos de extremo SOAP, puede crear un extremo SOAP.

**Habilitar el extremo**

Después de crear un nuevo extremo, debe habilitarlo. Cuando el extremo está habilitado, se puede utilizar para invocar el servicio. Después de habilitar el punto final, puede ver la vista dentro de la consola de administración.

**Consulte también**

[Añadir un extremo SOAP mediante la API de Java](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Añadir un extremo SOAP mediante la API de Java {#add-a-soap-endpoint-using-the-java-api}

Añada un extremo SOAP a un servicio mediante la API de Java:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto EndpointRegistry Client.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EndpointRegistryClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Defina los atributos del extremo SOAP.

   * Cree un objeto `CreateEndpointInfo` utilizando su constructor.
   * Especifique el valor del identificador del conector invocando el método `CreateEndpointInfo` del objeto `setConnectorId` y pasando el valor de cadena `SOAP`.
   * Especifique la descripción del punto final invocando el método `CreateEndpointInfo` del objeto `setDescription` y pasando un valor de cadena que describe el punto final.
   * Especifique el nombre del extremo invocando el método `CreateEndpointInfo` del objeto `setName` y pasando un valor de cadena que especifica el nombre.
   * Especifique el servicio al que pertenece el extremo invocando el método `CreateEndpointInfo` del objeto `setServiceId` y pasando un valor de cadena que especifica el nombre del servicio.
   * Especifique la operación que se invoca invocando el método `CreateEndpointInfo` del objeto `setOperationName` y pasando un valor de cadena que especifica el nombre de la operación. Para los extremos SOAP y EJB, especifique un carácter comodín ( `*`), lo que implica todas las operaciones.

1. Cree un extremo SOAP.

   Cree el punto final invocando el método `EndpointRegistryClient` del objeto `createEndpoint` y pasando el objeto `CreateEndpointInfo`. Este método devuelve un objeto `Endpoint` que representa el nuevo extremo SOAP.

1. Habilite el punto final.

   Habilite el punto final invocando el método enable del objeto `EndpointRegistryClient` y pase el objeto `Endpoint` devuelto por el método `createEndpoint`.

**Consulte también**

[Resumen de los pasos](programmatically-endpoints.md#summary-of-steps)

[Inicio rápido: Añadir un extremo SOAP mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Añadir extremos de carpeta observados {#adding-watched-folder-endpoints}

Puede agregar mediante programación un extremo de carpeta vigilada a un servicio mediante la API de Java de AEM Forms. Al agregar un punto final Carpeta vigilada, se permite a los usuarios colocar un archivo (como un archivo PDF) en una carpeta. Cuando el archivo se coloca en la carpeta, se invoca el servicio configurado y se manipula el archivo. Una vez que el servicio realiza la operación especificada, guarda el archivo modificado en una carpeta de salida especificada. Una carpeta vigilada está configurada para analizarse con un intervalo de velocidad fijo o con un cronograma crónico, como todos los lunes, miércoles y viernes al mediodía.

Para agregar mediante programación un extremo de carpeta vigilada a un servicio, considere el siguiente proceso breve denominado *EncryptDocument*. (Consulte [Explicación de los procesos de AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)).

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

Este proceso acepta un documento PDF no seguro como valor de entrada y, a continuación, pasa el documento PDF no seguro a la operación `EncryptPDFUsingPassword` del servicio de cifrado. El documento PDF se cifra con una contraseña y el documento PDF con contraseña cifrada es el valor de salida de este proceso. El nombre del valor de entrada (el documento PDF no seguro) es `InDoc` y el tipo de datos es `com.adobe.idp.Document`. El nombre del valor de salida (el documento PDF cifrado con contraseña) es `SecuredDoc` y el tipo de datos es `com.adobe.idp.Document`.

>[!NOTE]
>
>No se puede agregar un extremo de carpeta vigilada mediante servicios Web.

### Resumen de los pasos {#summary_of_steps-2}

Para agregar un extremo de carpeta vigilada a un servicio, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto `EndpointRegistryClient`.
1. Definir atributos de extremo de carpeta vigilada.
1. Especifique los valores de configuración.
1. Defina los valores de parámetro de entrada.
1. Defina un valor de parámetro de salida.
1. Crear un punto final de carpeta vigilada.
1. Habilite el punto final.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss Application Server)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creación de un objeto EndpointRegistry Client**

Para agregar mediante programación un extremo de carpeta vigilada, debe crear un objeto `EndpointRegistryClient`.

**Definir atributos de extremo de carpeta vigilada**

Para crear un extremo de carpeta vigilada para un servicio, especifique los siguientes valores:

* **Identificador** del conector: Especifica el tipo de extremo que se crea. Para crear un extremo de carpeta vigilada, especifique `WatchedFolder`.
* **Descripción**: Especifica la descripción del extremo.
* **Nombre**: Especifica el nombre del extremo.
* **Identificador** de servicio: Especifica el servicio al que pertenece el extremo. Por ejemplo, para agregar un extremo de carpeta vigilada al proceso que se introduce en esta sección (un proceso se convierte en un servicio cuando se activa mediante Workbench), especifique `EncryptDocument`.
* **Nombre** de la operación: Especifica el nombre de la operación que se invoca mediante el extremo. Normalmente, al crear un extremo de carpeta vigilada para un servicio que se originó a partir de un proceso creado en Workbench, el nombre de la operación es `invoke`.

**Especificar valores de configuración**

Debe especificar valores de configuración para un extremo de carpeta vigilada al agregar mediante programación un extremo de carpeta vigilada a un servicio. Estos valores de configuración los especifica un administrador si se agrega un extremo de carpeta vigilada mediante la consola de administración.

La siguiente lista especifica los valores de configuración que se establecen al agregar mediante programación un extremo de carpeta vigilada a un servicio:

* **url**: Especifica la ubicación de la carpeta vigilada. En un entorno agrupado, este valor debe apuntar a una carpeta de red compartida a la que se pueda acceder desde todos los equipos del clúster.
* **asincrónico**: Identifica el tipo de invocación como asíncrono o sincrónico. Los procesos transitorios y sincrónicos sólo se pueden invocar sincrónicamente. El valor predeterminado es true. Se recomienda asincrónico.
* **cronExpression**: Utilizado por cuarzo para programar el sondeo del directorio de entrada. Para obtener más información sobre la configuración de la expresión cron, consulte [https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html](https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html).
* **purgeDuration**: Se trata de un atributo obligatorio. Los archivos y carpetas de la carpeta de resultados se purgan cuando son anteriores a este valor. Este valor se mide en días. Este atributo es útil para garantizar que la carpeta de resultados no esté llena. Un valor de -1 días indica que nunca se elimina la carpeta de resultados. El valor predeterminado es -1.
* **repeatInterval**: Intervalo, en segundos, para analizar la carpeta vigilada para obtener información. A menos que la limitación esté habilitada, este valor debe ser mayor que el tiempo para procesar un trabajo promedio; de lo contrario, el sistema podría estar sobrecargado. El valor predeterminado es 5.
* **repeatCount**: Número de veces que una carpeta vigilada explora la carpeta o el directorio. Un valor de -1 indica la digitalización indefinida. El valor predeterminado es -1.
* **throttleOn**: Limita el número de trabajos de carpetas vigiladas que se pueden procesar en un momento dado. El número máximo de trabajos viene determinado por el valor batchSize.
* **userName**: El nombre de usuario utilizado al invocar un servicio de destinatario desde la carpeta vigilada. Este valor es obligatorio. El valor predeterminado es SuperAdmin.
* **domainName**: Dominio del usuario. Este valor es obligatorio. El valor predeterminado es DefaultDom.
* **batchSize**: Número de archivos o carpetas que se van a buscar por análisis. Utilice este valor para evitar una sobrecarga en el sistema; si se analizan demasiados archivos al mismo tiempo, se puede producir un bloqueo. El valor predeterminado es 2.
* **waitTime**: Tiempo, en milisegundos, que se debe esperar antes de analizar una carpeta o archivo después de la creación. Por ejemplo, si el tiempo de espera es de 36.000.000 milisegundos (una hora) y el archivo se creó hace un minuto, este archivo se recoge después de que hayan transcurrido 59 minutos o más. Este atributo es útil para asegurarse de que un archivo o carpeta se copia completamente en la carpeta de entrada. Por ejemplo, si tiene un archivo grande para procesar y el archivo tarda diez minutos en descargarse, establezca el tiempo de espera en 10&amp;ast;60 &amp;ast;1000 milisegundos. Esta configuración evita que la carpeta vigilada analice el archivo si no ha estado esperando durante diez minutos. El valor predeterminado es 0.
* **excludeFilePattern**: Patrón que utiliza una carpeta vigilada para determinar qué archivos y carpetas deben analizarse y captarse. No se analizará el procesamiento de ningún archivo o carpeta que tenga este patrón. Esta configuración resulta útil cuando la entrada es una carpeta que contiene varios archivos. El contenido de la carpeta se puede copiar en una carpeta con un nombre que la carpeta vigilada recogerá. Este paso evita que la carpeta vigilada recoja una carpeta para procesarla antes de que la carpeta se copie completamente en la carpeta de entrada. Por ejemplo, si el valor excludeFilePattern es `data*`, no se recogen todos los archivos y carpetas que coinciden con `data*`. Esto incluye archivos y carpetas con los nombres `data1`, `data2`, etc. Además, el patrón se puede complementar con patrones comodín para especificar patrones de archivo. La carpeta observada modifica la expresión normal para admitir patrones comodín como `*.*` y `*.pdf`. Estos patrones comodín no son compatibles con expresiones regulares.
* **includeFilePattern**: Patrón que utiliza la carpeta vigilada para determinar qué carpetas y archivos se deben analizar y recoger. Por ejemplo, si este valor es `*`, se recogen todos los archivos y carpetas que coinciden con `input*`. Esto incluye archivos y carpetas con los nombres `input1`, `input2`, etc. El valor predeterminado es `*`. Este valor indica todos los archivos y carpetas. Además, el patrón se puede complementar con patrones comodín para especificar patrones de archivo. La carpeta observada modifica la expresión normal para admitir patrones comodín como `*.*` y `*.pdf`. Estos patrones comodín no son compatibles con expresiones regulares. Este valor es obligatorio.
* **resultFolderName**: Carpeta donde se almacenan los resultados guardados. Esta ubicación puede ser una ruta de directorio absoluta o relativa. Si los resultados no aparecen en esta carpeta, compruebe la carpeta de errores. Los archivos de sólo lectura no se procesan y se guardarán en la carpeta de errores. El valor predeterminado es `result/%Y/%M/%D/`. Esta es la carpeta de resultados dentro de la carpeta vigilada.
* **preserveFolderName**: Ubicación en la que se almacenan los archivos después de realizar correctamente el análisis y la recogida. Esta ubicación puede ser absoluta, relativa o nula. El valor predeterminado es `preserve/%Y/%M/%D/`.
* **failFolderName**: Carpeta donde se guardan los archivos de error. Esta ubicación siempre es relativa a la carpeta vigilada. Los archivos de sólo lectura no se procesan y se guardarán en la carpeta de errores. El valor predeterminado es `failure/%Y/%M/%D/`.
* **preserveOnFailure**: Preservar archivos de entrada en caso de error al ejecutar la operación en un servicio. El valor predeterminado es true.
* **overwriteDuplicateFilename**: Cuando se establece en true, se sobrescriben los archivos de la carpeta de resultados y la carpeta de conservación. Cuando se establece en false, los archivos y las carpetas que tienen un sufijo de índice numérico se utilizan para el nombre. El valor predeterminado es false.

**Definir valores de parámetro de entrada**

Al crear un extremo de carpeta vigilada, debe definir los valores de parámetro de entrada. Es decir, debe describir los valores de entrada que se pasan a la operación que invoca la carpeta controlada. Por ejemplo, considere el proceso introducido en este tema. Tiene un valor de entrada denominado `InDoc` y su tipo de datos es `com.adobe.idp.Document`. Al crear un extremo de carpeta vigilada para este proceso (después de activar un proceso, se convierte en un servicio), debe definir el valor del parámetro de entrada.

Para definir los valores de parámetro de entrada necesarios para un extremo de carpeta vigilada, especifique los siguientes valores:

**Nombre** del parámetro de entrada: Nombre del parámetro de entrada. El nombre de un valor de entrada se especifica en Workbench para un proceso. Si el valor de entrada pertenece a una operación de servicio (un servicio que no es un proceso creado en Workbench), el nombre de entrada se especifica en el archivo component.xml. Por ejemplo, el nombre del parámetro de entrada para el proceso introducido en esta sección es `InDoc`.

**Tipo** de asignación: Se utiliza para configurar los valores de entrada necesarios para invocar la operación de servicio. Existen dos tipos de asignación:

* `Literal`:: El punto final Carpeta vigilada utiliza el valor introducido en el campo a medida que se muestra. Se admiten todos los tipos de Java básicos. Por ejemplo, si una API utiliza entradas como String, long, int y Boolean, la cadena se convierte al tipo adecuado y se invoca el servicio.
* `Variable`:: El valor introducido es un patrón de archivo que la carpeta vigilada utiliza para seleccionar la entrada. Por ejemplo, si selecciona Variable para el tipo de asignación y el documento de entrada debe ser un archivo PDF, puede especificar `*.pdf`como valor de asignación.

**Valor** de asignación: Especifica el valor del tipo de asignación. Por ejemplo, si selecciona un tipo de asignación `Variable`, puede especificar `*.pdf` como patrón de archivo.

**Tipo** de datos: Especifica el tipo de datos de los valores de entrada. Por ejemplo, el tipo de datos del valor de entrada del proceso introducido en esta sección es `com.adobe.idp.Document`.

**Definir un valor de parámetro de salida**

Al crear un extremo de carpeta vigilada, debe definir un valor de parámetro de salida. Es decir, debe describir el valor de salida que devuelve el servicio que invoca el extremo de la carpeta vigilada. Por ejemplo, considere el proceso introducido en este tema. Tiene un valor de salida denominado `SecuredDoc` y su tipo de datos es `com.adobe.idp.Document`. Al crear un extremo de carpeta vigilada para este proceso (después de activar un proceso, se convierte en un servicio), debe definir el valor del parámetro de salida.

Para definir un valor de parámetro de salida requerido para un extremo de carpeta vigilada, especifique los siguientes valores:

**Nombre** del parámetro de salida: Nombre del parámetro de salida. El nombre de un valor de salida de proceso se especifica en Workbench. Si el valor de salida pertenece a una operación de servicio (un servicio que no es un proceso creado en Workbench), el nombre de salida se especifica en el archivo component.xml. Por ejemplo, el nombre del parámetro de salida para el proceso introducido en esta sección es `SecuredDoc`.

**Tipo** de asignación: Se utiliza para configurar la salida del servicio y la operación. Las opciones disponibles son las siguientes:

* Si el servicio devuelve un solo objeto (un solo documento), el patrón es `%F.pdf` y el destino de origen es source cefilename.pdf. Por ejemplo, el proceso introducido en esta sección devuelve un solo documento. Como resultado, el tipo de asignación se puede definir como `%F.pdf` ( `%F` significa utilizar el nombre de archivo dado). El patrón `%E` especifica la extensión del documento de entrada.
* Si el servicio devuelve una lista, el patrón es `Result\%F\` y el destino de origen es Result\sourcefilename\source1 (salida 1) y Result\sourcefilename\source2 (salida 2).
* Si el servicio devuelve un mapa, el patrón es `Result\%F\` y el destino de origen es Result\sourcefilename\file1 and Result\sourcefilename\file2. Si el mapa tiene más de un objeto, el patrón es `Result\%F.pdf` y el destino de origen es Result\sourcefilename1.pdf (salida 1), Result\sourcefilenam2.pdf (salida 2), etc.

**Tipo** de datos: Especifica el tipo de datos del valor devuelto. Por ejemplo, el tipo de datos del valor devuelto del proceso introducido en esta sección es `com.adobe.idp.Document`.

**Creación de un extremo de carpeta vigilada**

Después de definir los atributos, los valores de configuración y los valores de los parámetros de entrada y salida del extremo, debe crear el extremo Carpeta vigilada.

**Habilitar el extremo**

Después de crear un extremo de carpeta vigilada, debe habilitarlo. Cuando el extremo está habilitado, se puede utilizar para invocar el servicio. Después de habilitar el punto final, puede vista dentro de la consola de administración.

**Consulte también**

[Añadir un extremo de carpeta vigilada mediante la API de Java](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Añadir un extremo de carpeta vigilada mediante la API de Java {#add-a-watched-folder-endpoint-using-the-java-api}

Añada un extremo de carpeta vigilada mediante la API de Java de AEM Forms:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto EndpointRegistry Client.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EndpointRegistryClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Definir atributos de extremo de carpeta vigilada.

   * Cree un objeto `CreateEndpointInfo` utilizando su constructor.
   * Especifique el valor del identificador del conector invocando el método `CreateEndpointInfo` del objeto `setConnectorId` y pasando el valor de cadena `WatchedFolder`.
   * Especifique la descripción del punto final invocando el método `CreateEndpointInfo` del objeto `setDescription` y pasando un valor de cadena que describe el punto final.
   * Especifique el nombre del extremo invocando el método `CreateEndpointInfo` del objeto `setName` y pasando un valor de cadena que especifica el nombre.
   * Especifique el servicio al que pertenece el extremo invocando el método `CreateEndpointInfo` del objeto `setServiceId` y pasando un valor de cadena que especifica el nombre del servicio.
   * Especifique la operación que se invoca invocando el método `CreateEndpointInfo` del objeto `setOperationName` y pasando un valor de cadena que especifica el nombre de la operación. Normalmente, al crear un extremo de carpeta vigilada para un servicio que se originó a partir de un proceso creado en Workbench, se invoca el nombre de la operación.

1. Especifique los valores de configuración.

   Para cada valor de configuración que se va a establecer para el extremo Carpeta vigilada, debe invocar el método `CreateEndpointInfo` del objeto `setConfigParameterAsText`. Por ejemplo, para establecer el valor de configuración `url`, invoque el método `CreateEndpointInfo` del objeto `setConfigParameterAsText` y pase los siguientes valores de cadena:

   * Un valor de cadena que especifica el nombre del valor de configuración. Al configurar el valor de configuración `url`, especifique `url`.
   * Un valor de cadena que especifica el valor del valor de configuración. Al establecer el valor de configuración `url`, especifique la ubicación de la carpeta controlada.

   >[!NOTE]
   >
   >Para ver todos los valores de configuración establecidos para el servicio EncryptDocument, consulte el ejemplo de código Java ubicado en [QuickStart: Añadir un extremo de carpeta vigilada mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api).

1. Defina los valores de parámetro de entrada.

   Defina un valor de parámetro de entrada invocando el método `CreateEndpointInfo` del objeto `setInputParameterMapping` y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del parámetro de entrada. Por ejemplo, el nombre del parámetro de entrada para el servicio EncryptDocument es `InDoc`.
   * Un valor de cadena que especifica el tipo de datos del parámetro de entrada. Por ejemplo, el tipo de datos del parámetro de entrada `InDoc` es `com.adobe.idp.Document`.
   * Un valor de cadena que especifica el tipo de asignación. Por ejemplo, puede especificar `variable`.
   * Un valor de cadena que especifica el valor del tipo de asignación. Por ejemplo, puede especificar &amp;ast;.pdf como patrón de archivo.

   >[!NOTE]
   >
   >Invoque el método `setInputParameterMapping` para cada valor del parámetro de entrada que se va a definir. Dado que el proceso EncryptDocument tiene sólo un parámetro de entrada, debe invocar este método una vez.

1. Defina un valor de parámetro de salida.

   Defina un valor de parámetro de salida invocando el método `CreateEndpointInfo` del objeto `setOutputParameterMapping` y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del parámetro de salida. Por ejemplo, el nombre del parámetro de salida para el servicio EncryptDocument es `SecuredDoc`.
   * Un valor de cadena que especifica el tipo de datos del parámetro de salida. Por ejemplo, el tipo de datos del parámetro de salida `SecuredDoc` es `com.adobe.idp.Document`.
   * Un valor de cadena que especifica el tipo de asignación. Por ejemplo, puede especificar `%F.pdf`.

1. Crear un punto final de carpeta vigilada.

   Cree el punto final invocando el método `EndpointRegistryClient` del objeto `createEndpoint` y pasando el objeto `CreateEndpointInfo`. Este método devuelve un objeto `Endpoint` que representa el punto final Carpeta vigilada.

1. Habilite el punto final.

   Habilite el punto final invocando el método `EndpointRegistryClient` del objeto `enable` y pasando el objeto `Endpoint` devuelto por el método `createEndpoint`.

**Consulte también**

[Resumen de los pasos](programmatically-endpoints.md#summary-of-steps)

[Inicio rápido: Añadir un extremo de carpeta vigilada mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Archivo constante {#watched-folder-configuration-values-constant-file} de valores de configuración de carpeta observados

El [inicio rápido: Añadir un extremo de carpeta vigilada mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) utiliza un archivo constante que debe formar parte del proyecto de Java para compilar el inicio rápido. Este archivo constante representa los valores de configuración que deben establecerse al agregar un extremo de carpeta vigilada. El siguiente código Java representa el archivo constante.

```java
 /**
     * This class contains constants that can be used when setting Watched Folder
     * configuration values
     */

 public final class WatchedFolderEndpointConfigConstants {

         public static final String PROPERTY_FILEPROVIDER_URL = "url";
         public static final String PROPERTY_PROPERTY_ASYNCHRONOUS = "asynchronous";
         public static final String PROPERTY_CRON_EXPRESSION = "cronExpression";
         public static final String PROPERTY_PURGE_DURATION = "purgeDuration";
         public static final String PROPERTY_REPEAT_INTERVAL = "repeatInterval";
         public static final String PROPERTY_REPEAT_COUNT = "repeatCount";
         public static final String PROPERTY_THROTTLE = "throttleOn";
         public static final String PROPERTY_USERNAMER = "userName";
         public static final String PROPERTY_DOMAINNAME = "domainName";
         public static final String PROPERTY_FILEPROVIDER_BATCH_SIZE = "batchSize";
         public static final String PROPERTY_FILEPROVIDER_WAIT_TIME = "waitTime";
         public static final String PROPERTY_EXCLUDE_FILE_PATTERN = "excludeFilePattern";
         public static final String PROPERTY_INCLUDE_FILE_PATTERN = "excludeFilePattern";
         public static final String PROPERTY_FILEPROVIDER_RESULT_FOLDER_NAME =  "resultFolderName";
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_FOLDER_NAME = "preserveFolderName";
         public static final String PROPERTY_FILEPROVIDER_FAILURE_FOLDER_NAME = "failureFolderName";
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_ON_FAILURE = "preserveOnFailure";
         public static final String PROPERTY_FILEPROVIDER_OVERWRITE_DUPLICATE_FILENAME = "overwriteDuplicateFilename";
        }
```

## Añadir extremos de correo electrónico {#adding-email-endpoints}

Puede agregar mediante programación un extremo de correo electrónico a un servicio mediante la API de AEM Forms Java. Al agregar un extremo de correo electrónico, se permite a los usuarios enviar un mensaje de correo electrónico con uno o varios archivos adjuntos a una cuenta de correo electrónico específica. A continuación, se invoca la operación del servicio de configuración y se manipulan los archivos. Una vez que el servicio realiza la operación especificada, envía un mensaje de correo electrónico al remitente con los archivos modificados como archivos adjuntos.

Para agregar mediante programación un extremo de correo electrónico a un servicio, considere el siguiente proceso breve denominado *MyApplication\EncryptDocument*. Para obtener información sobre los procesos de corta duración, consulte [Explicación de los procesos de AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

Este proceso acepta un documento PDF no seguro como valor de entrada y, a continuación, pasa el documento PDF no seguro a la operación `EncryptPDFUsingPassword` del servicio de cifrado. Este proceso codifica el documento PDF con una contraseña y devuelve el documento PDF cifrado con contraseña como valor de salida. El nombre del valor de entrada (el documento PDF no seguro) es `InDoc` y el tipo de datos es `com.adobe.idp.Document`. El nombre del valor de salida (el documento PDF cifrado con contraseña) es `SecuredDoc` y el tipo de datos es `com.adobe.idp.Document`.

>[!NOTE]
>
>No puede agregar un extremo de correo electrónico mediante servicios Web.

### Resumen de los pasos {#summary_of_steps-3}

Para agregar un extremo de correo electrónico a un servicio, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto `EndpointRegistryClient`.
1. Definir atributos de extremo de correo electrónico.
1. Especifique los valores de configuración.
1. Defina los valores de parámetro de entrada.
1. Defina un valor de parámetro de salida.
1. Cree el extremo de correo electrónico.
1. Habilite el punto final.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss Application Server)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creación de un objeto EndpointRegistry Client**

Para poder agregar mediante programación un extremo de correo electrónico, debe crear un objeto `EndpointRegistryClient`.

**Definir atributos de extremo de correo electrónico**

Para crear un extremo de correo electrónico para un servicio, especifique los siguientes valores:

* **Valor** del identificador del conector: Especifica el tipo de extremo que se crea. Para crear un extremo de correo electrónico, especifique `Email`.
* **Descripción**: Especifica una descripción para el extremo.
* **Nombre**: Especifica el nombre del extremo.
* **Valor** del identificador de servicio: Especifica el servicio al que pertenece el extremo. Por ejemplo, para agregar un extremo de correo electrónico al proceso que se introduce en esta sección (un proceso se convierte en un servicio cuando se activa mediante Workbench), especifique `EncryptDocument`.
* **Nombre** de la operación: Especifica el nombre de la operación que se invoca mediante el extremo. Normalmente, al crear un extremo de correo electrónico para un servicio que se originó a partir de un proceso creado en Workbench, el nombre de la operación es `invoke`.

**Especificar valores de configuración**

Debe especificar los valores de configuración para un extremo de correo electrónico al agregar mediante programación un extremo de correo electrónico a un servicio. Estos valores de configuración los especifica un administrador si se agrega un extremo de correo electrónico mediante la consola de administración.

>[!NOTE]
>
>La cuenta de correo electrónico que se monitorea es una cuenta especial que se utiliza solamente para el extremo de correo electrónico. Esta cuenta no es una cuenta de correo electrónico de un usuario normal. La cuenta de correo electrónico de un usuario normal no debe configurarse como la cuenta que utiliza el proveedor de correo electrónico porque este elimina los mensajes de correo electrónico de la bandeja de entrada después de que hayan finalizado con los mensajes.

Los siguientes valores de configuración se establecen al agregar mediante programación un extremo de correo electrónico a un servicio:

* **cronExpression**: Una expresión cron si el correo electrónico debe programarse mediante una expresión cron.
* **repeatCount**: Número de veces que el extremo de correo electrónico explora la carpeta o el directorio. Un valor de -1 indica la digitalización indefinida. El valor predeterminado es -1.
* **repeatInterval**: Frecuencia de análisis en segundos que utiliza el receptor para comprobar si hay correo entrante. El valor predeterminado es 10.
* **startDelay**: Tiempo de espera para analizar después de los inicios del Planificador. La hora predeterminada es 0.
* **batchSize**: Número de mensajes de correo electrónico que procesa el receptor por escaneo para obtener un rendimiento óptimo. Un valor de -1 indica todos los correos electrónicos. El valor predeterminado es 2.
* **userName**: El nombre de usuario que se utiliza al invocar un servicio de destinatario desde el correo electrónico. El valor predeterminado es `SuperAdmin`.
* **domainName**: Un valor de configuración obligatorio. El valor predeterminado es `DefaultDom`.
* **domainPattern**: Especifica los patrones de dominio del correo electrónico entrante que acepta el proveedor. Por ejemplo: si se utiliza `adobe.com`, solo se procesa el correo electrónico de adobe.com, se ignora el correo electrónico de otros dominios.
* **filePattern**: Especifica los patrones de archivos adjuntos entrantes que acepta el proveedor. Esto incluye archivos con extensiones de nombre de archivo específicas (&amp;ast;.dat, &amp;ast;.xml), archivos con nombres (datos) específicos y archivos con expresiones compuestas en el nombre y la extensión (&amp;ast;..[dD][aA]&#39;puerto&#39;). El valor predeterminado es `*`.
* **destinationSuccessfulJob**: Dirección de correo electrónico a la que se envían mensajes para indicar los trabajos que se han realizado correctamente. De forma predeterminada, siempre se envía un mensaje de trabajo correcto al remitente. Si escribe `sender`, los resultados del correo electrónico se envían al remitente. Se admiten hasta 100 destinatarios. Especifique destinatarios adicionales con direcciones de correo electrónico, cada uno separado por una coma. Para desactivar esta opción, deje este valor en blanco. En algunos casos, es posible que desee realizar un déclencheur en un proceso y no desee recibir una notificación por correo electrónico del resultado. El valor predeterminado es `sender`.
* **destinationFailedJob**: Dirección de correo electrónico a la que se envían mensajes para indicar que se han producido errores en los trabajos. De forma predeterminada, siempre se envía un mensaje de trabajo fallido al remitente. Si escribe `sender`, los resultados del correo electrónico se envían al remitente. Se admiten hasta 100 destinatarios. Especifique destinatarios adicionales con direcciones de correo electrónico, cada uno separado por una coma. Para desactivar esta opción, deje este valor en blanco. El valor predeterminado es `sender`.
* **inboxHost**: El nombre de host o la dirección IP de la bandeja de entrada que debe analizar el proveedor de correo electrónico.
* **inboxPort**: El puerto que utiliza el servidor de correo electrónico. El valor predeterminado para POP3 es 110 y el valor predeterminado para IMAP es 143. Si SSL está habilitado, el valor predeterminado para POP3 es 995 y el valor predeterminado para IMAP es 993.
* **inboxProtocol**: El protocolo de correo electrónico del extremo de correo electrónico que se va a usar para analizar la bandeja de entrada. Las opciones son `IMAP` o `POP3`. El servidor de correo de host de bandeja de entrada debe admitir estos protocolos.
* **inboxTimeOut**: Tiempo de espera en segundos para que el proveedor de correo electrónico espere las respuestas de la bandeja de entrada. El valor predeterminado es 60.
* **inboxUser**: El nombre de usuario necesario para iniciar sesión en la cuenta de correo electrónico. Según el servidor de correo electrónico y la configuración, esto puede ser solamente la parte del nombre de usuario del correo electrónico o puede ser la dirección de correo electrónico completa.
* **inboxPassword**: La contraseña del usuario de la bandeja de entrada.
* **inboxSSLEnabled**: Establezca este valor para obligar al proveedor de correo electrónico a utilizar SSL al enviar mensajes de notificación de resultados o errores. Asegúrese de que el host IMAP o POP3 admita SSL.
* **smtpHost**: El nombre de host del servidor de correo al que el proveedor de correo electrónico envía resultados y mensajes de error.
* **smtpPort**: El valor predeterminado para el puerto SMTP es 25.
* **smtpUser**: Cuenta de usuario del proveedor de correo electrónico que se utilizará cuando envíe notificaciones por correo electrónico de resultados y errores.
* **smtpPassword**: La contraseña de la cuenta SMTP. Algunos servidores de correo no requieren una contraseña SMTP.
* **charSet**: Conjunto de caracteres utilizado por el proveedor de correo electrónico. El valor predeterminado es `UTF-8`.
* **smtpSSLEnabled**: Establezca este valor para obligar al proveedor de correo electrónico a utilizar SSL al enviar mensajes de notificación de resultados o errores. Asegúrese de que el host SMTP admita SSL.
* **failedJobFolder**: Especifica un directorio en el que almacenar los resultados cuando el servidor de correo SMTP no está operativo.
* **asincrónico**: Cuando se establece en sincrónico, se procesan todos los documentos de entrada y se devuelve una sola respuesta. Cuando se establece en asincrónico, se envía una respuesta por cada documento de entrada que se procesa. Por ejemplo, se crea un extremo de correo electrónico para el proceso introducido en este tema y se envía un mensaje de correo electrónico a la bandeja de entrada del extremo que contiene varios documentos PDF no seguros. Cuando todos los documentos PDF se cifran con una contraseña y si el extremo se configura como sincrónico, se envía un único mensaje de correo electrónico de respuesta con todos los documentos PDF protegidos adjuntos. Si el extremo está configurado como asincrónico, se envía un mensaje de correo electrónico de respuesta independiente para cada documento PDF protegido. Cada mensaje de correo electrónico contiene un único documento PDF como archivo adjunto. El valor predeterminado es asincrónico.

**Definir valores de parámetro de entrada**

Al crear un extremo de correo electrónico, debe definir los valores de parámetro de entrada. Es decir, debe describir los valores de entrada que se pasan a la operación que invoca el extremo de correo electrónico. Por ejemplo, considere el proceso introducido en este tema. Tiene un valor de entrada denominado `InDoc` y su tipo de datos es `com.adobe.idp.Document`. Al crear un extremo de correo electrónico para este proceso (después de activar un proceso, se convierte en un servicio), debe definir el valor del parámetro de entrada.

Para definir los valores de parámetro de entrada necesarios para un extremo de correo electrónico, especifique los siguientes valores:

**Nombre** del parámetro de entrada: Nombre del parámetro de entrada. El nombre de un valor de entrada se especifica en Workbench para un proceso. Si el valor de entrada pertenece a una operación de servicio (un servicio de Forms que no es un proceso creado en Workbench), el nombre de entrada se especifica en el archivo component.xml. Por ejemplo, el nombre del parámetro de entrada para el proceso introducido en esta sección es `InDoc`.

**Tipo** de asignación: Se utiliza para configurar los valores de entrada necesarios para invocar la operación de servicio. Dos tipos de asignación son los siguientes:

* `Literal`:: El extremo Correo electrónico utiliza el valor introducido en el campo tal como se muestra. Se admiten todos los tipos de Java básicos. Por ejemplo, si una API utiliza entradas como String, long, int y Boolean, la cadena se convierte al tipo adecuado y se invoca el servicio.
* `Variable`:: El valor introducido es un patrón de archivo que utiliza el extremo de correo electrónico para elegir la entrada. Por ejemplo, si selecciona Variable para el tipo de asignación y el documento de entrada debe ser un archivo PDF, puede especificar `*.pdf` como valor de asignación.

**Valor** de asignación: Especifica el valor del tipo de asignación. Por ejemplo, si selecciona un tipo de asignación Variable, puede especificar `*.pdf` como patrón de archivo.

**Tipo** de datos: Especifica el tipo de datos de los valores de entrada. Por ejemplo, el tipo de datos del valor de entrada del proceso introducido en esta sección es com.adobe.idp.Documento.

**Definir un valor de parámetro de salida**

Al crear un extremo de correo electrónico, debe definir un valor de parámetro de salida. Es decir, debe describir el valor de salida que devuelve el servicio que invoca el extremo de correo electrónico. Por ejemplo, considere el proceso introducido en este tema. Tiene un valor de salida denominado `SecuredDoc` y su tipo de datos es `com.adobe.idp.Document`. Al crear un extremo de correo electrónico para este proceso (después de activar un proceso, se convierte en un servicio), debe definir el valor del parámetro de salida.

Para definir un valor de parámetro de salida requerido para un extremo de correo electrónico, especifique los siguientes valores:

**Nombre** del parámetro de salida: Nombre del parámetro de salida. El nombre de un valor de salida de proceso se especifica en Workbench. Si el valor de salida pertenece a una operación de servicio (un servicio que no es un proceso creado en Workbench), el nombre de salida se especifica en el archivo component.xml. Por ejemplo, el nombre del parámetro de salida para el proceso introducido en esta sección es `SecuredDoc`.

**Tipo** de asignación: Se utiliza para configurar la salida del servicio y la operación. Las opciones disponibles son las siguientes:

* Si el servicio devuelve un solo objeto (un solo documento), el patrón es `%F.pdf` y el destino de origen es source cefilename.pdf. Por ejemplo, el proceso introducido en esta sección devuelve un solo documento. Como resultado, el tipo de asignación se puede definir como `%F.pdf` ( `%F` significa utilizar el nombre de archivo dado). El patrón `%E` especifica la extensión del documento de entrada.
* Si el servicio devuelve una lista, el patrón es `Result\%F\` y el destino de origen es Result\sourcefilename\source1 (salida 1) y Result\sourcefilename\source2 (salida 2).
* Si el servicio devuelve un mapa, el patrón es `Result\%F\` y el destino de origen es Result\sourcefilename\file1 and Result\sourcefilename\file2. Si el mapa tiene más de un objeto, el patrón es `Result\%F.pdf` y el destino de origen es Result\sourcefilename1.pdf (salida 1), Result\sourcefilenam2.pdf (salida 2), etc.

**Tipo** de datos: Especifica el tipo de datos del valor devuelto. Por ejemplo, el tipo de datos del valor devuelto del proceso introducido en esta sección es `com.adobe.idp.Document`.

**Crear el extremo de correo electrónico**

Después de definir los atributos de extremo de correo electrónico y los valores de configuración, así como los valores de parámetro de entrada y salida, debe crear el extremo de correo electrónico.

**Habilitar el extremo**

Después de crear un extremo de correo electrónico, debe habilitarlo. Cuando el extremo está habilitado, se puede utilizar para invocar el servicio. Después de habilitar el punto final, puede vista dentro de la consola de administración.

**Consulte también**

[Añadir un extremo de correo electrónico mediante la API de Java](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Añadir un extremo de correo electrónico mediante la API de Java {#add-an-email-endpoint-using-the-java-api}

Añada un extremo de correo electrónico mediante la API de Java:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto EndpointRegistry Client.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EndpointRegistryClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Definir atributos de extremo de correo electrónico.

   * Cree un objeto `CreateEndpointInfo` utilizando su constructor.
   * Especifique el valor del identificador del conector invocando el método `CreateEndpointInfo` del objeto `setConnectorId` y pasando el valor de cadena `Email`.
   * Especifique la descripción del punto final invocando el método `CreateEndpointInfo` del objeto `setDescription` y pasando un valor de cadena que describe el punto final.
   * Especifique el nombre del extremo invocando el método `CreateEndpointInfo` del objeto `setName` y pasando un valor de cadena que especifica el nombre.
   * Especifique el servicio al que pertenece el extremo invocando el método `CreateEndpointInfo` del objeto `setServiceId` y pasando un valor de cadena que especifica el nombre del servicio.
   * Especifique la operación que se invoca invocando el método `CreateEndpointInfo` del objeto `setOperationName` y pasando un valor de cadena que especifica el nombre de la operación. Normalmente, al crear un extremo de correo electrónico para un servicio que se originó a partir de un proceso creado en Workbench, se invoca el nombre de la operación.

1. Especifique los valores de configuración.

   Para cada valor de configuración que se establezca para el extremo de correo electrónico, debe invocar el método `CreateEndpointInfo` del objeto `setConfigParameterAsText`. Por ejemplo, para establecer el valor de configuración `smtpHost`, invoque el método `CreateEndpointInfo` del objeto `setConfigParameterAsText` y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del valor de configuración. Al configurar el valor de configuración `smtpHost`, especifique `smtpHost`.
   * Un valor de cadena que especifica el valor del valor de configuración. Al establecer el valor de configuración `smtpHost`, especifique un valor de cadena que especifique el nombre del servidor SMTP.

   >[!NOTE]
   >
   >Para ver todos los valores de configuración establecidos para el servicio EncryptDocument introducido en esta sección, consulte el ejemplo de código Java ubicado en [QuickStart: Añadir un extremo de correo electrónico usando la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api).

1. Defina los valores de parámetro de entrada.

   Defina un valor de parámetro de entrada invocando el método `CreateEndpointInfo` del objeto `setInputParameterMapping` y pase los valores siguientes:

   * Un valor de cadena que especifica el nombre del parámetro de entrada. Por ejemplo, el nombre del parámetro de entrada para el servicio EncryptDocument es `InDoc`.
   * Un valor de cadena que especifica el tipo de datos del parámetro de entrada. Por ejemplo, el tipo de datos del parámetro de entrada `InDoc` es `com.adobe.idp.Document`.
   * Un valor de cadena que especifica el tipo de asignación. Por ejemplo, puede especificar `variable`.
   * Un valor de cadena que especifica el valor del tipo de asignación. Por ejemplo, puede especificar &amp;ast;.pdf como patrón de archivo.

   >[!NOTE]
   >
   >Invoque el método `setInputParameterMapping` para cada valor del parámetro de entrada que se va a definir. Dado que el proceso EncryptDocument tiene sólo un parámetro de entrada, debe invocar este método una vez.

1. Defina un valor de parámetro de salida.

   Defina un valor de parámetro de salida invocando el método `CreateEndpointInfo` del objeto `setOutputParameterMapping` y pasando los siguientes valores:

   * Un valor de cadena que especifica el nombre del parámetro de salida. Por ejemplo, el nombre del parámetro de salida para el servicio EncryptDocument es `SecuredDoc`.
   * Un valor de cadena que especifica el tipo de datos del parámetro de salida. Por ejemplo, el tipo de datos del parámetro de salida `SecuredDoc` es `com.adobe.idp.Document`.
   * Un valor de cadena que especifica el tipo de asignación. Por ejemplo, puede especificar `%F.pdf`.

1. Cree el extremo de correo electrónico.

   Cree el punto final invocando el método `EndpointRegistryClient` del objeto `createEndpoint` y pasando el objeto `CreateEndpointInfo`. Este método devuelve un objeto `Endpoint` que representa el extremo de correo electrónico.

1. Habilite el punto final.

   Habilite el punto final invocando el método `EndpointRegistryClient` del objeto `enable` y pasando el objeto `Endpoint` devuelto por el método `createEndpoint`.

**Consulte también**

[Resumen de los pasos](programmatically-endpoints.md#summary-of-steps)

[Inicio rápido: Añadir un extremo de carpeta vigilada mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Archivo constante de valores de configuración de correo electrónico {#email-configuration-values-constant-file}

El [inicio rápido: Añadir un extremo de correo electrónico usando la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) usa un archivo constante que debe formar parte del proyecto de Java para compilar el inicio rápido. Este archivo constante representa los valores de configuración que deben establecerse al agregar un extremo de correo electrónico. El siguiente código Java representa el archivo constante.

```java
 /**
     * This class contains constants that can be used when setting email endpoint
     * configuration values
     */
 public class EmailEndpointConfigConstants {

     public static final String PROPERTY_EMAILPROVIDER_CRON_EXPRESSION = "cronExpression";
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_COUNT = "repeatCount";
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_INTERVAL = "repeatInterval";
     public static final String PROPERTY_EMAILPROVIDER_START_DELAY = "startDelay";
     public static final String PROPERTY_EMAILPROVIDER_BATCH_SIZE = "batchSize";
     public static final String PROPERTY_EMAILPROVIDER_USERNAME = "userName";
     public static final String PROPERTY_EMAILPROVIDER_DOMAINNAME = "domainName";
     public static final String PROPERTY_EMAILPROVIDER_DOMAINPATTERN = "domainPattern";
     public static final String PROPERTY_EMAILPROVIDER_FILEPATTERN = "filePattern";
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_SUCCESSFUL_JOB = "recipientSuccessfulJob";
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_FAILED_JOB = "recipientFailedJob";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_HOST = "inboxHost";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PORT = "inboxPort";
     public static final String PROPERTY_EMAILPROVIDER_PROTOCOL = "inboxProtocol";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_TIMEOUT = "inboxTimeOut";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_USER = "inboxUser";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PASSWORD = "inboxPassword";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_SSL = "inboxSSLEnabled";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_HOST = "smtpHost";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PORT = "smtpPort";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_USER = "smtpUser";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PASSWORD = "smtpPassword";
     public static final String PROPERTY_EMAILPROVIDER_CHARSET = "charSet";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_SSL = "smtpSSLEnabled";
     public static final String PROPERTY_EMAILPROVIDER_FAILED_FOLDER = "failedJobFolder";
     public static final String PROPERTY_EMAILPROVIDER_ASYNCHRONOUS = "asynchronous";
 }
```

## Añadir extremos remotos {#adding-remoting-endpoints}

>[!NOTE]
>
>Las API de LiveCycle Remoting están en desuso para AEM formularios en JEE.

Puede agregar mediante programación un extremo Remoting a un servicio mediante la API de Java de AEM Forms. Al agregar un extremo Remoting, se habilita una aplicación de Flex para invocar el servicio mediante remoting. (Consulte [Invocación de AEM Forms mediante (obsoleto para formularios AEM) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

Para agregar mediante programación un extremo Remoting a un servicio, considere el siguiente proceso de corta duración denominado *EncryptDocument*.

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

Este proceso acepta un documento PDF no seguro como valor de entrada y, a continuación, pasa el documento PDF no seguro a la operación `EncryptPDFUsingPassword` del servicio de cifrado. El documento PDF se cifra con una contraseña y el documento PDF con contraseña cifrada es el valor de salida de este proceso. El nombre del valor de entrada (el documento PDF no seguro) es `InDoc` y el tipo de datos es `com.adobe.idp.Document`. El nombre del valor de salida (el documento PDF cifrado con contraseña) es `SecuredDoc` y el tipo de datos es `com.adobe.idp.Document`.

Para mostrar cómo agregar un extremo Remoting a un servicio, en esta sección se agrega un extremo Remoting a un servicio llamado EncryptDocument.

>[!NOTE]
>
>No se puede agregar un extremo Remoting mediante servicios Web.

### Resumen de los pasos {#summary_of_steps-4}

Para eliminar un extremo de un servicio, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto `EndpointRegistryClient`.
1. Establecer atributos de extremo de Remoting.
1. Cree un extremo remoto.
1. Habilite el punto final.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss Application Server)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creación de un objeto EndpointRegistry Client**

Para agregar un extremo Remoting mediante programación, debe crear un objeto `EndpointRegistryClient`.

**Establecer atributos de extremo de Remoting**

Para crear un extremo Remoting para un servicio, especifique los siguientes valores:

* **Valor** del identificador del conector: Especifica el tipo de extremo que se crea. Para crear un extremo Remoting, especifique `Remoting`.
* **Descripción**: Especifica la descripción del extremo.
* **Nombre**: Especifica el nombre del extremo.
* **Valor** del identificador de servicio: Especifica el servicio al que pertenece el extremo. Por ejemplo, para agregar un extremo Remoting al proceso que se introduce en esta sección (un proceso se convierte en un servicio cuando se activa en Workbench), especifique `EncryptDocument`.
* **Nombre** de la operación: Especifica el nombre de la operación que se invoca mediante el extremo. Al crear un extremo remoto, especifique un carácter comodín (&amp;ast;).

**Crear un extremo remoto**

Después de definir atributos de extremo de Remoting, puede crear un extremo de Remoting para un servicio.

**Habilitar el extremo**

Después de crear un nuevo extremo, debe habilitarlo. Cuando se habilita un extremo Remoting, habilita un cliente de Flex para invocar el servicio.

**Consulte también**

[Añadir un extremo remoto mediante la API de Java](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Añadir un extremo remoto mediante la API de Java {#add-a-remoting-endpoint-using-the-java-api}

Añada un extremo Remoting mediante la API de Java:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto EndpointRegistry Client.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EndpointRegistryClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Establecer atributos de extremo de Remoting.

   * Cree un objeto `CreateEndpointInfo` utilizando su constructor.
   * Especifique el valor del identificador del conector invocando el método `CreateEndpointInfo` del objeto `setConnectorId` y pasando el valor de cadena `Remoting`.
   * Especifique la descripción del punto final invocando el método `CreateEndpointInfo` del objeto `setDescription` y pasando un valor de cadena que describe el punto final.
   * Especifique el nombre del extremo invocando el método `CreateEndpointInfo` del objeto `setName` y pasando un valor de cadena que especifica el nombre.
   * Especifique el servicio al que pertenece el extremo invocando el método `CreateEndpointInfo` del objeto `setServiceId` y pasando un valor de cadena que especifica el nombre del servicio.
   * Especifique la operación que invoca el método `CreateEndpointInfo` del objeto `setOperationName` y pase un valor de cadena que especifique el nombre de la operación. Para un extremo Remoting, especifique un carácter comodín (&amp;ast;).

1. Cree un extremo remoto.

   Cree el punto final invocando el método `EndpointRegistryClient` del objeto `createEndpoint` y pasando el objeto `CreateEndpointInfo`. Este método devuelve un objeto `Endpoint` que representa el nuevo extremo Remoting.

1. Habilite el punto final.

   Habilite el punto final invocando el método `EndpointRegistryClient` del objeto `enable` y pasando el objeto `Endpoint` devuelto por el método `createEndpoint`.

**Consulte también**

[Resumen de los pasos](programmatically-endpoints.md#summary-of-steps)

[Inicio rápido: Añadir un extremo remoto mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Añadir extremos de TaskManager {#adding-taskmanager-endpoints}

Puede agregar mediante programación un extremo de TaskManager a un servicio mediante la API de Java de AEM Forms. Al agregar un extremo de TaskManager a un servicio, se habilita a un usuario de Workspace para que invoque el servicio. Es decir, un usuario que trabaja en Workspace puede invocar un proceso que tiene un extremo de TaskManager correspondiente.

>[!NOTE]
>
>No se puede agregar un extremo de TaskManager mediante servicios Web.

### Resumen de los pasos {#summary_of_steps-5}

Para agregar un extremo de TaskManager a un servicio, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto `EndpointRegistryClient`.
1. Cree una categoría para el extremo.
1. Definir atributos de extremo de TaskManager.
1. Cree un extremo de TaskManager.
1. Habilite el punto final.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss Application Server)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creación de un objeto EndpointRegistry Client**

Para poder agregar mediante programación un extremo de TaskManager, debe crear un objeto `EndpointRegistryClient`.

**Crear una categoría para el extremo**

Las categorías se utilizan para organizar servicios dentro de Workspace. Es decir, un usuario de Workspace puede invocar un servicio que tiene un extremo de TaskManager seleccionando una categoría dentro de Workspace. Al crear un extremo de TaskManager, puede hacer referencia a una categoría existente o crear una categoría nueva mediante programación.

>[!NOTE]
>
>Esta sección crea una nueva categoría como parte de la adición de un extremo de TaskManager a un servicio.

**Establecer atributos de extremo de TaskManager**

Para crear un extremo de TaskManager para un servicio, especifique los siguientes valores:

* **Identificador** del conector: Especifica el tipo de extremo que se crea. Para crear un extremo de TaskManager, especifique `TaskManagerConnector`.
* **Descripción**: Especifica la descripción del extremo.
* **Nombre**: Especifica el nombre del extremo.
* **Identificador** de servicio: Especifica el servicio al que pertenece el extremo.
* **Categoría**: Especifica un valor de identificador de categoría asociado al extremo de TaskManager.
* **Nombre** de la operación: Normalmente, al crear un extremo de TaskManager para un servicio que se originó a partir de un proceso creado en Workbench, se asigna el nombre de la operación  `invoke`.

**Crear un extremo de TaskManager**

Después de establecer los atributos de extremo de TaskManager, puede crear un extremo de TaskManager para un servicio.

**Habilitar el extremo**

Después de crear un nuevo extremo, debe habilitarlo. Cuando el extremo está habilitado, se puede utilizar para invocar el servicio desde Workspace. Después de habilitar el punto final, puede vista dentro de la consola de administración.

**Consulte también**

[Añadir un extremo de TaskManager mediante la API de Java](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Añadir un extremo de TaskManager mediante la API de Java {#add-a-taskmanager-endpoint-using-the-java-api}

Añada un extremo de TaskManager mediante la API de Java:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto EndpointRegistry Client.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EndpointRegistryClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Cree una categoría para el extremo.

   * Cree un objeto `CreateEndpointCategoryInfo` utilizando su constructor y pasando los siguientes valores:

      * Un valor de cadena que especifica el valor de identificador de la categoría
      * Un valor de cadena que especifica la descripción de la categoría
   * Cree la categoría invocando el método `EndpointRegistryClient` del objeto `createEndpointCategory` y pasando el objeto `CreateEndpointCategoryInfo`. Este método devuelve un objeto `EndpointCategory` que representa la nueva categoría.


1. Definir atributos de extremo de TaskManager.

   * Cree un objeto `CreateEndpointInfo` utilizando su constructor.
   * Especifique el valor del identificador del conector invocando el método `CreateEndpointInfo` del objeto `setConnectorId` y pasando el valor de cadena `TaskManagerConnector`.
   * Especifique la descripción del punto final invocando el método `CreateEndpointInfo` del objeto `setDescription` y pasando un valor de cadena que describe el punto final.
   * Especifique el nombre del extremo invocando el método `CreateEndpointInfo` del objeto `setName` y pasando un valor de cadena que especifica el nombre.
   * Especifique el servicio al que pertenece el extremo invocando el método `CreateEndpointInfo` del objeto `setServiceId` y pasando un valor de cadena que especifica el nombre del servicio.
   * Especifique la categoría a la que pertenece el extremo invocando el método `CreateEndpointInfo` del objeto `setCategoryId` y pasando un valor de cadena que especifica el valor del identificador de categoría. Puede invocar el método `EndpointCategory` del objeto `getId` para obtener el valor de identificador de esta categoría.
   * Especifique la operación que se invoca invocando el método `CreateEndpointInfo` del objeto `setOperationName` y pasando un valor de cadena que especifica el nombre de la operación. Normalmente, al crear un extremo `TaskManager` para un servicio que se originó a partir de un proceso creado en Workbench, el nombre de la operación es `invoke`.

1. Cree un extremo de TaskManager.

   Cree el punto final invocando el método `EndpointRegistryClient` del objeto `createEndpoint` y pasando el objeto `CreateEndpointInfo`. Este método devuelve un objeto `Endpoint` que representa el nuevo extremo de TaskManager.

1. Habilite el punto final.

   Habilite el punto final invocando el método `EndpointRegistryClient` del objeto `enable` y pasando el objeto `Endpoint` devuelto por el método `createEndpoint`.

**Consulte también**

[Resumen de los pasos](programmatically-endpoints.md#summary-of-steps)

[Inicio rápido: Añadir un extremo de TaskManager mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Modificación de los extremos {#modifying-endpoints}

Puede modificar mediante programación un punto final existente mediante la API Java de AEM Forms. Al modificar un punto final, puede cambiar el comportamiento del punto final. Considere, por ejemplo, un punto final Carpeta vigilada que especifica una carpeta que se utiliza como carpeta vigilada. Puede modificar mediante programación los valores de configuración que pertenecen al punto final Carpeta vigilada, lo que resulta en que otra carpeta funcione como la carpeta vigilada. Para obtener información sobre los valores de configuración que pertenecen a un extremo de carpeta vigilada, consulte [Añadir extremos de carpeta vigilada](programmatically-endpoints.md#adding-watched-folder-endpoints).

Para mostrar cómo modificar un extremo, esta sección modifica un extremo de carpeta vigilada cambiando la carpeta que se comporta como la carpeta vigilada.

>[!NOTE]
>
>No se puede modificar un punto final mediante servicios Web.

### Resumen de los pasos {#summary_of_steps-6}

Para modificar un extremo, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto `EndpointRegistryClient`.
1. Recupere el punto final.
1. Especifique nuevos valores de configuración.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss Application Server)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creación de un objeto EndpointRegistry Client**

Para modificar un extremo mediante programación, debe crear un objeto `EndpointRegistryClient`.

**Recuperar el punto final para modificar**

Para poder modificar un punto final, debe recuperarlo. Para recuperar un punto final, debe conectarse como usuario que puede acceder a un punto final. Se recomienda que se conecte como administrador. (Consulte [Configuración de propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

Puede recuperar un punto final recuperando una lista de puntos finales. A continuación, puede iterar a través de la lista, buscando el punto final específico que desea eliminar. Por ejemplo, puede ubicar un extremo determinando el servicio que corresponde al extremo y el tipo de extremo. Cuando localice el punto final, puede modificarlo.

**Especificar nuevos valores de configuración**

Al modificar un extremo, especifique nuevos valores de configuración. Por ejemplo, para modificar un extremo de carpeta vigilada, restablezca todos los valores de configuración del extremo de carpeta vigilada, no solo los que desea modificar. Para obtener información sobre los valores de configuración que pertenecen a un extremo de carpeta vigilada, consulte [Añadir extremos de carpeta vigilada](programmatically-endpoints.md#adding-watched-folder-endpoints).

>[!NOTE]
>
>Para obtener información sobre los valores de configuración que pertenecen a un extremo de correo electrónico, consulte [Añadir extremos de correo electrónico](programmatically-endpoints.md#adding-email-endpoints).

>[!NOTE]
>
>No se puede modificar el servicio que invoca el extremo. Si intenta modificar el servicio, se genera una excepción. Para modificar el servicio asociado a un punto final determinado, elimine el extremo y cree uno nuevo. (Consulte [Eliminación de extremos](programmatically-endpoints.md#removing-endpoints).)

**Consulte también**

[Modificación de un extremo mediante la API de Java](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Modificación de un extremo mediante la API de Java {#modifying-an-endpoint-using-the-java-api}

Modifique un punto final mediante la API de Java:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto EndpointRegistry Client.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EndpointRegistryClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recupere el punto final que desea modificar.

   * Recupere una lista de todos los extremos a los que puede acceder el usuario actual (especificada en las propiedades de conexión) invocando el método `EndpointRegistryClient` del objeto `getEndpoints` y pasando un objeto `PagingFilter` que actúa como filtro. Puede pasar un valor `(PagingFilter)null` para devolver todos los extremos. Este método devuelve un objeto `java.util.List` donde cada elemento es un objeto `Endpoint`. Para obtener información sobre un objeto `PagingFilter`, consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Repita el objeto `java.util.List` para determinar si tiene extremos. Si existen extremos, cada elemento es una instancia `EndPoint`.
   * Determine el servicio que corresponde a un extremo invocando el método `EndPoint` del objeto `getServiceId`. Este método devuelve un valor de cadena que especifica el nombre del servicio.
   * Determine el tipo de extremo invocando el método `EndPoint` del objeto `getConnectorId`. Este método devuelve un valor de cadena que especifica el tipo de extremo. Por ejemplo, si el punto final es una carpeta vigilada, este método devuelve `WatchedFolder`.

1. Especifique nuevos valores de configuración.

   * Cree un objeto `ModifyEndpointInfo` invocando su constructor.
   * Para cada valor de configuración que se va a establecer, invoque el método `ModifyEndpointInfo` del objeto `setConfigParameterAsText`. Por ejemplo, para establecer el valor de configuración de URL, invoque el método `ModifyEndpointInfo` del objeto `setConfigParameterAsText` y pase los valores siguientes:

      * Un valor de cadena que especifica el nombre del valor de configuración. Por ejemplo, para establecer el valor de configuración `url`, especifique `url`.
      * Un valor de cadena que especifica el valor del valor de configuración. Para definir un valor para el valor de configuración `url`, especifique la ubicación de la carpeta controlada.
   * Invoque el método `EndpointRegistryClient` del objeto `modifyEndpoint` y pase el objeto `ModifyEndpointInfo`.


**Consulte también**

[Resumen de los pasos](programmatically-endpoints.md#summary-of-steps)

[Inicio rápido: Modificación de un extremo mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eliminando extremos {#removing-endpoints}

Puede eliminar mediante programación un extremo de un servicio mediante la API de AEM Forms Java. Después de quitar un punto final, no se puede invocar el servicio mediante el método de invocación que habilitó el punto final. Por ejemplo, si elimina un extremo SOAP de un servicio, no podrá invocar el servicio mediante el modo SOAP.

Para demostrar cómo eliminar un punto final de un servicio, esta sección elimina un punto final de EJB de un servicio llamado *EncryptDocument*.

>[!NOTE]
>
>No se puede quitar un punto final mediante servicios Web.

### Resumen de los pasos {#summary_of_steps-7}

Para eliminar un extremo de un servicio, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto `EndpointRegistryClient`.
1. Recupere el punto final.
1. Elimine el punto final.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss Application Server)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creación de un objeto EndpointRegistry Client**

Para eliminar un extremo mediante programación, debe crear un objeto `EndpointRegistryClient`.

**Recuperar el punto final que eliminar**

Antes de eliminar un punto final, debe recuperarlo. Para recuperar un punto final, debe conectarse como usuario que puede acceder a un punto final. Se recomienda que se conecte como administrador. (Consulte [Configuración de propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

Puede recuperar un punto final recuperando una lista de puntos finales. A continuación, puede iterar a través de la lista, buscando el punto final específico que desea eliminar. Por ejemplo, puede ubicar un extremo determinando el servicio que corresponde al extremo y el tipo de extremo. Cuando encuentre el punto final, puede eliminarlo.

**Eliminar el punto final**

Después de crear un nuevo extremo, debe habilitarlo. Cuando el extremo está habilitado, se puede utilizar para invocar el servicio. Después de habilitar el punto final, puede vista dentro de la consola de administración.

**Consulte también**

[Eliminación de un extremo mediante la API de Java](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminación de un extremo mediante la API de Java {#removing-an-endpoint-using-the-java-api}

Elimine un punto final mediante la API de Java:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto EndpointRegistry Client.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EndpointRegistryClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recupere el punto final que desea eliminar.

   * Recupere una lista de todos los extremos a los que tiene acceso el usuario actual (especificada en las propiedades de conexión) invocando el método `EndpointRegistryClient` del objeto `getEndpoints` y pasando un objeto `PagingFilter` que actúa como filtro. Puede pasar `(PagingFilter)null` para devolver todos los extremos. Este método devuelve un objeto `java.util.List` donde cada elemento es un objeto `Endpoint`.
   * Repita el objeto `java.util.List` para determinar si tiene extremos. Si existen extremos, cada elemento es una instancia `EndPoint`.
   * Determine el servicio que corresponde a un extremo invocando el método `EndPoint` del objeto `getServiceId`. Este método devuelve un valor de cadena que especifica el nombre del servicio.
   * Determine el tipo de extremo invocando el método `EndPoint` del objeto `getConnectorId`. Este método devuelve un valor de cadena que especifica el tipo de extremo. Por ejemplo, si el punto final es un punto final de EJB, este método devuelve `EJB`.

1. Elimine el punto final.

   Elimine el punto final invocando el método `EndpointRegistryClient` del objeto `remove` y pasando el objeto `EndPoint` que representa el punto final que se va a quitar.

**Consulte también**

[Resumen de los pasos](programmatically-endpoints.md#summary-of-steps)

[Inicio rápido: Eliminación de un extremo mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Recuperando información del conector de extremo {#retrieving-endpoint-connector-information}

Puede recuperar mediante programación información sobre los conectores de extremo mediante la API de AEM Forms. Un conector permite que un punto final invoque un servicio mediante varios métodos de invocación. Por ejemplo, un conector de carpeta vigilada permite que un extremo invoque un servicio mediante carpetas vigiladas. Al recuperar mediante programación la información sobre los conectores de punto final, puede recuperar los valores de configuración asociados con un conector, como los valores de configuración necesarios y los opcionales.

Para mostrar cómo recuperar información sobre los conectores de punto final, esta sección recupera información sobre un conector de carpeta vigilada. (Consulte [Añadir extremos de carpeta vigilados](programmatically-endpoints.md#adding-watched-folder-endpoints)).

>[!NOTE]
>
>No puede recuperar información sobre los extremos mediante servicios Web.

>[!NOTE]
>
>En este tema se utiliza la API `ConnectorRegistryClient` para recuperar información sobre los conectores de extremo. (Consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

### Resumen de los pasos {#summary_of_steps-8}

Para recuperar la información del conector del punto final, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto `ConnectorRegistryClient`.
1. Especifique el tipo de conector.
1. Recuperar valores de configuración.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

Se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms se implementa en JBoss Application Server)

Si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no es JBoss, sustituya adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que se implementa AEM Forms. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creación de un objeto ConnectorRegistry Client**

Para recuperar mediante programación la información del conector del punto final, cree un objeto `ConnectorRegistryClient`.

**Especifique el tipo de conector**

Especifique el tipo de conector desde el que desea recuperar la información. Existen los siguientes tipos de conectores:

* **EJB**: Permite que una aplicación cliente invoque un servicio mediante el modo EJB.
* **SOAP**: Permite que una aplicación cliente invoque un servicio mediante el modo SOAP.
* **Carpeta** vigilada: Permite que las carpetas vigiladas invoquen un servicio.
* **Correo electrónico**: Permite que los mensajes de correo electrónico invoquen un servicio.
* **Remoting**: Permite que una aplicación cliente de Flex invoque un servicio.
* **TaskManagerConnector**: Permite que un usuario de Workspace invoque un servicio desde Workspace.

**Recuperar valores de configuración**

Después de especificar el tipo de conector, puede recuperar información sobre el conector, como el valor de configuración admitido. Por ejemplo, para cualquier conector, puede determinar qué valores de configuración son obligatorios y cuáles son opcionales.

**Consulte también**

[Recuperar información del conector del extremo mediante la API de Java](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar información del conector del extremo mediante la API de Java {#retrieve-endpoint-connector-information-using-the-java-api}

Recupere la información del conector del extremo mediante la API de Java:

1. Incluir archivos de proyecto. .

   Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clases del proyecto Java.

1. Cree un objeto ConnectorRegistry Client.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `ConnectorRegistryClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Especifique el tipo de conector.

   Especifique el tipo de conector invocando el método `ConnectorRegistryClient` del objeto `getEndpointDefinition` y pasando un valor de cadena que especifica el tipo de conector. Por ejemplo, para especificar el tipo de conector Carpeta vigilada, pase el valor de cadena `WatchedFolder`. Este método devuelve un objeto `Endpoint` que corresponde al tipo de conector.

1. Recuperar valores de configuración.

   * Recupere los valores de configuración asociados dentro de este extremo invocando el método `Endpoint` del objeto `getConfigParameters`. Este método devuelve una matriz de objetos `ConfigParameter`.
   * Recupere información sobre cada valor de configuración recuperando cada elemento dentro de la matriz. Cada elemento es un objeto `ConfigParameter`. Por ejemplo, puede determinar si el valor de configuración es obligatorio u opcional invocando el método `ConfigParameter` del objeto `isRequired`. Si se requiere el valor de configuración, este método devuelve `true`.

**Consulte también**

[Resumen de los pasos](programmatically-endpoints.md#summary-of-steps)

[Inicio rápido: Recuperación de información del conector del extremo mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
