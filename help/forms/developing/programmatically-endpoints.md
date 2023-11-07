---
title: Administración programática de puntos de conexión
seo-title: Programmatically Managing Endpoints
description: Utilice el servicio Registro de extremos para agregar extremos de EJB, agregar extremos de SOAP, agregar extremos de carpetas inspeccionadas, agregar extremos de correo electrónico, agregar extremos de Remoting, agregar extremos de Task Manager, modificar extremos, quitar extremos y recuperar información del conector de extremo.
seo-description: Use the Endpoint Registry service to add EJB endpoints, add SOAP endpoint, add Watched Folder endpoints, add Email endpoints, add  Remoting endpoints, add Task Manager endpoints, modify endpoints, remove endpoints, and retrieve endpoint connector information.
uuid: 5dc50946-3323-4c5d-a43b-31c1c980bd04
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 076889a7-9c9f-4b6f-a45b-67a9b3923c36
role: Developer
exl-id: b94dcca2-136b-4b7d-b5ce-544804575876
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '10790'
ht-degree: 2%

---

# Administración programática de puntos de conexión {#programmatically-managing-endpoints}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

**Acerca del servicio Registro de extremos**

El servicio Registro de extremos proporciona la capacidad de administrar los extremos mediante programación. Por ejemplo, puede agregar los siguientes tipos de extremos a un servicio:

* EJB
* SOAP
* Carpeta inspeccionada
* Correo electrónico
* AEM (Obsoleto para formularios en formato de) Remoting
* Administrador de tareas

>[!NOTE]
>
>AEM Los puntos de conexión remotos SOAP, EJB y (obsoletos para formularios de en JEE) se crean automáticamente para cada servicio activado. Los extremos SOAP y EJB habilitan SOAP y EJB para todas las operaciones de servicio.

Un extremo remoto permite a los clientes de Flex invocar operaciones en el servicio AEM Forms al que se agrega el extremo. Se crea un destino de Flex con el mismo nombre que el extremo y los clientes de Flex pueden crear objetos remotos que apunten a este destino para invocar operaciones en el servicio correspondiente.

Los extremos de Correo electrónico, Administrador de tareas y Carpeta inspeccionada solo exponen una operación específica del servicio. Para agregar estos extremos, es necesario realizar un segundo paso de configuración para seleccionar un método para invocar, establecer parámetros de configuración y especificar asignaciones de parámetros de entrada y salida.

Puede organizar los extremos de TaskManager en grupos llamados *categorías*. Estas categorías se exponen a Workspace a través de TaskManager, y los usuarios finales ven los puntos finales de TaskManager a medida que se clasifican. En Workspace, los usuarios finales ven estas categorías en el panel de navegación. Los puntos finales de cada categoría se muestran como tarjetas de proceso en la página Iniciar procesos de Workspace.

Puede realizar estas tareas mediante el servicio Registro de extremos:

* Agregar extremos de EJB. (Consulte [Agregar extremos de EJB](programmatically-endpoints.md#adding-ejb-endpoints).)
* Agregar extremos SOAP. (Consulte [Adición de extremos SOAP](programmatically-endpoints.md#adding-soap-endpoints).)
* Agregar extremos de carpeta inspeccionada (consulte ) [Adición de extremos de carpeta inspeccionada](programmatically-endpoints.md#adding-watched-folder-endpoints).)
* Agregar extremos de correo electrónico. (Consulte [Añadir extremos de correo electrónico](programmatically-endpoints.md#adding-email-endpoints).)
* Agregar extremos remotos. (Consulte [Agregar extremos remotos](programmatically-endpoints.md#adding-remoting-endpoints).)
* Agregar extremos de TaskManager (consulte [Agregar extremos de TaskManager](programmatically-endpoints.md#adding-taskmanager-endpoints).)
* Modificar extremos (consulte [Modificación de puntos finales](programmatically-endpoints.md#modifying-endpoints).)
* Eliminar extremos (consulte [Eliminación de extremos](programmatically-endpoints.md#removing-endpoints).)
* Recuperar información del conector del extremo (consulte [Recuperando información del conector de extremo](programmatically-endpoints.md#retrieving-endpoint-connector-information).)

## Agregar extremos de EJB {#adding-ejb-endpoints}

Puede agregar mediante programación un extremo de EJB a un servicio mediante la API de Java de AEM Forms. Al agregar un extremo de EJB a un servicio, está habilitando una aplicación cliente para que invoque el servicio mediante el modo EJB. Es decir, al establecer las propiedades de conexión necesarias para invocar AEM Forms, puede seleccionar el modo EJB. (Consulte [Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>No puede agregar un extremo de EJB mediante servicios web.

>[!NOTE]
>
>Normalmente, se agrega un extremo EJB a un servicio de forma predeterminada. Sin embargo, se puede agregar un extremo EJB a un proceso implementado mediante programación o cuando se quita un extremo EJB y debe agregarse de nuevo.

### Resumen de los pasos {#summary-of-steps}

Para agregar un extremo de EJB a un servicio, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Crear un `EndpointRegistry Client` objeto.
1. Establecer atributos de extremo de EJB.
1. Cree un extremo de EJB.
1. Habilite el extremo.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un objeto EndpointRegistry Client**

Para poder agregar mediante programación un extremo EJB, debe crear un `EndpointRegistryClient` objeto.

**Establecer atributos de extremo de EJB**

Para crear un extremo de EJB para un servicio, especifique los siguientes valores:

* **Identificador del conector**: especifica el tipo de extremo que se va a crear. Para crear un extremo de EJB, especifique `EJB`.
* **Descripción**: especifica la descripción del extremo.
* **Nombre**: especifica el nombre del extremo.
* **Identificador de servicio**: especifica el servicio al que pertenece el extremo.
* **Nombre de operación**: especifica el nombre de la operación que se invoca mediante el extremo. Al crear un extremo de EJB, especifique un carácter comodín ( `*`). Sin embargo, si desea especificar una operación específica en lugar de invocar todas las operaciones de servicio, especifique el nombre de la operación en lugar de utilizar el carácter comodín ( `*`).

**Crear un extremo EJB**

Después de establecer los atributos de extremo de EJB, puede crear un extremo de EJB para un servicio.

**Habilitar el extremo**

Después de crear un extremo, debe habilitarlo. Después de habilitar el punto de conexión, se puede utilizar para invocar el servicio. Después de habilitar el punto de conexión, puede verlo en la consola de administración.

**Consulte también**

[Agregar un extremo EJB mediante la API de Java](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Agregar un extremo EJB mediante la API de Java {#adding-an-ejb-endpoint-using-the-java-api}

Agregar un extremo de EJB mediante la API de Java:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clase del proyecto Java. (

1. Cree un objeto EndpointRegistry Client.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `EndpointRegistryClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Establecer atributos de extremo de EJB.

   * Crear un `CreateEndpointInfo` mediante su constructor.
   * Especifique el valor del identificador del conector invocando el `CreateEndpointInfo` del objeto `setConnectorId` método y pasar el valor de cadena `EJB`.
   * Especifique la descripción del extremo invocando el `CreateEndpointInfo` del objeto `setDescription` y pasando un valor de cadena que describe el extremo.
   * Especifique el nombre del extremo invocando el `CreateEndpointInfo` del objeto `setName` y pasando un valor de cadena que especifica el nombre.
   * Especifique el servicio al que pertenece el extremo invocando el `CreateEndpointInfo` del objeto `setServiceId` y pasando un valor de cadena que especifica el nombre del servicio.
   * Especifique la operación que se invoca invocando el `CreateEndpointInfo` del objeto `setOperationName` y pasar un valor de cadena que especifique el nombre de la operación. Para los extremos SOAP y EJB, especifique un carácter comodín ( `*`), que implica todas las operaciones.

1. Cree un extremo de EJB.

   Cree el extremo invocando el `EndpointRegistryClient` del objeto `createEndpoint` y pasando el `CreateEndpointInfo` objeto. Este método devuelve un `Endpoint` que representa el nuevo extremo de EJB.

1. Habilite el extremo.

   Habilite el punto de conexión invocando `EndpointRegistryClient` método enable del objeto y pasar el `Endpoint` objeto que ha devuelto el `createEndpoint` método.

**Consulte también**

[Resumen de los pasos](programmatically-endpoints.md#summary-of-steps)

[Inicio rápido: Agregar un extremo EJB mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Adición de extremos SOAP {#adding-soap-endpoints}

Puede agregar mediante programación un extremo SOAP a un servicio mediante la API de Java de AEM Forms. Al agregar un extremo SOAP, habilita una aplicación cliente para invocar el servicio mediante el modo SOAP. Es decir, al establecer las propiedades de conexión necesarias para invocar AEM Forms, puede seleccionar el modo SOAP.

>[!NOTE]
>
>No puede agregar un extremo SOAP mediante servicios web.

>[!NOTE]
>
>Normalmente, se agrega un extremo SOAP a un servicio de forma predeterminada. Sin embargo, se puede agregar un extremo SOAP a un proceso que se implementa mediante programación o cuando se quita un extremo SOAP y debe agregarse de nuevo.

### Resumen de los pasos {#summary_of_steps-1}

Para agregar un extremo SOAP a un servicio, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Crear un `EndpointRegistryClient` objeto.
1. Establezca atributos de extremo SOAP.
1. Cree un extremo SOAP.
1. Habilite el extremo.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

Estos archivos JAR son necesarios para crear un extremo SOAP. Sin embargo, necesita archivos JAR adicionales si utiliza el extremo SOAP para invocar el servicio. Para obtener información sobre los archivos JAR de AEM Forms, consulte [Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un objeto EndpointRegistry Client**

Para agregar mediante programación un extremo SOAP a un servicio, debe crear un `EndpointRegistryClient` objeto.

**Establecer atributos de extremo SOAP**

Para agregar un extremo SOAP a un servicio, especifique los siguientes valores:

* **Valor del identificador del conector**: especifica el tipo de extremo que se va a crear. Para crear un extremo SOAP, especifique `SOAP`.
* **Descripción**: especifica la descripción del extremo.
* **Nombre**: especifica el nombre del extremo.
* **Valor del identificador del servicio**: especifica el servicio al que pertenece el extremo.
* **Nombre de operación**: especifica el nombre de la operación que se invoca mediante el extremo. Al crear un extremo SOAP, especifique un carácter comodín ( `*`). Sin embargo, si desea especificar una operación específica en lugar de invocar todas las operaciones de servicio, especifique el nombre de la operación en lugar de utilizar el carácter comodín ( `*`).

**Crear un extremo SOAP**

Después de establecer los atributos de extremo SOAP, puede crear un extremo SOAP.

**Habilitar el extremo**

Después de crear un extremo, debe habilitarlo. Cuando el punto de conexión está habilitado, se puede utilizar para invocar el servicio. Después de habilitar el punto de conexión, puede verlo en la consola de administración.

**Consulte también**

[Añadir un extremo SOAP mediante la API de Java](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Añadir un extremo SOAP mediante la API de Java {#add-a-soap-endpoint-using-the-java-api}

Agregar un extremo SOAP a un servicio mediante la API de Java:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto EndpointRegistry Client.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `EndpointRegistryClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Establezca atributos de extremo SOAP.

   * Crear un `CreateEndpointInfo` mediante su constructor.
   * Especifique el valor del identificador del conector invocando el `CreateEndpointInfo` del objeto `setConnectorId` método y pasar el valor de cadena `SOAP`.
   * Especifique la descripción del extremo invocando el `CreateEndpointInfo` del objeto `setDescription` y pasando un valor de cadena que describe el extremo.
   * Especifique el nombre del extremo invocando el `CreateEndpointInfo` del objeto `setName` y pasando un valor de cadena que especifica el nombre.
   * Especifique el servicio al que pertenece el extremo invocando el `CreateEndpointInfo` del objeto `setServiceId` y pasando un valor de cadena que especifica el nombre del servicio.
   * Especifique la operación que se invoca invocando el `CreateEndpointInfo` del objeto `setOperationName` y pasando un valor de cadena que especifica el nombre de la operación. Para los extremos SOAP y EJB, especifique un carácter comodín ( `*`), que implica todas las operaciones.

1. Cree un extremo SOAP.

   Cree el extremo invocando el `EndpointRegistryClient` del objeto `createEndpoint` y pasando el `CreateEndpointInfo` objeto. Este método devuelve un `Endpoint` que representa el nuevo extremo SOAP.

1. Habilite el extremo.

   Habilite el punto de conexión invocando `EndpointRegistryClient` método enable del objeto y pase el `Endpoint` objeto que ha devuelto el `createEndpoint` método.

**Consulte también**

[Resumen de los pasos](programmatically-endpoints.md#summary-of-steps)

[Inicio rápido: Añadir un punto final SOAP mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Adición de extremos de carpeta inspeccionada {#adding-watched-folder-endpoints}

Puede agregar mediante programación un punto final de carpeta inspeccionada a un servicio mediante la API de Java de AEM Forms. Al agregar un punto final de carpeta inspeccionada, permite a los usuarios colocar un archivo (como un archivo de PDF) en una carpeta. Cuando el archivo se coloca en la carpeta, el servicio configurado se invoca y manipula el archivo. Una vez que el servicio realiza la operación especificada, guarda el archivo modificado en una carpeta de salida especificada. Una carpeta vigilada está configurada para analizarse a un intervalo de tasa fija o con una programación cron, como todos los lunes, miércoles y viernes al mediodía.

Para agregar mediante programación un extremo de carpeta inspeccionada a un servicio, considere el siguiente proceso de corta duración denominado *EncryptDocument*. (Consulte [Explicación de los procesos AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

Este proceso acepta un documento de PDF no protegido como valor de entrada y, a continuación, pasa el documento de PDF no protegido al servicio Encryption `EncryptPDFUsingPassword` operación. El documento de PDF se cifra con una contraseña y el documento de PDF cifrado con contraseña es el valor de salida de este proceso. El nombre del valor de entrada (el documento de PDF no protegido) es `InDoc` y el tipo de datos es `com.adobe.idp.Document`. El nombre del valor de salida (el documento de PDF cifrado con contraseña) es `SecuredDoc` y el tipo de datos es `com.adobe.idp.Document`.

>[!NOTE]
>
>No puede agregar un punto final de carpeta inspeccionada mediante los servicios web.

### Resumen de los pasos {#summary_of_steps-2}

Para agregar un punto final de carpeta inspeccionada a un servicio, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Crear un `EndpointRegistryClient` objeto.
1. Establezca los atributos del punto final de la carpeta inspeccionada.
1. Especifique los valores de configuración.
1. Defina los valores de parámetros de entrada.
1. Defina un valor de parámetro de salida.
1. Cree un punto final de carpeta inspeccionada.
1. Habilite el extremo.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un objeto EndpointRegistry Client**

Para agregar mediante programación un punto final de carpeta inspeccionada, debe crear un `EndpointRegistryClient` objeto.

**Establecer atributos de extremo de carpeta inspeccionada**

Para crear un punto final de carpeta inspeccionada para un servicio, especifique los siguientes valores:

* **Identificador del conector**: especifica el tipo de extremo que se crea. Para crear un punto final de carpeta inspeccionada, especifique `WatchedFolder`.
* **Descripción**: especifica la descripción del extremo.
* **Nombre**: especifica el nombre del extremo.
* **Identificador de servicio**: especifica el servicio al que pertenece el extremo. Por ejemplo, para agregar un punto final de carpeta inspeccionada al proceso introducido en esta sección (un proceso se convierte en servicio cuando se activa mediante Workbench), especifique `EncryptDocument`.
* **Nombre de operación**: especifica el nombre de la operación que se invoca mediante el extremo. Normalmente, cuando se crea un punto final de carpeta inspeccionada para un servicio que se originó a partir de un proceso creado en Workbench, el nombre de la operación es `invoke`.

**Especificar valores de configuración**

Especifique valores de configuración para un punto final de carpeta inspeccionada al agregar mediante programación un punto final de carpeta inspeccionada a un servicio. Un administrador especifica estos valores de configuración si se agrega un punto final de carpeta inspeccionada mediante la consola de administración.

La siguiente lista especifica los valores de configuración que se establecen al agregar mediante programación un punto final de carpeta inspeccionada a un servicio:

* **url**: especifica la ubicación de la carpeta vigilada. En un entorno agrupado, este valor debe apuntar a una carpeta de red compartida a la que se pueda acceder desde todos los equipos del clúster.
* **asíncrono**: Identifica el tipo de invocación como asincrónico o sincrónico. Los procesos transitorios y sincrónicos solo se pueden invocar sincrónicamente. El valor predeterminado es True. Se recomienda asincrónico.
* **cronExpression**: lo utiliza el cuarzo para programar el sondeo del directorio de entrada.
* **purgeDuration**: Este es un atributo obligatorio. Los archivos y carpetas de la carpeta de resultados se depuran cuando son anteriores a este valor. Este valor se mide en días. Este atributo es útil para garantizar que la carpeta de resultados no se llene. El valor de -1 días indica que nunca se eliminará la carpeta de resultados. El valor predeterminado es -1.
* **repeatInterval**: Intervalo, en segundos, para analizar la carpeta inspeccionada para obtener información. A menos que la restricción esté habilitada, este valor debe ser mayor que el tiempo para procesar un trabajo promedio; de lo contrario, el sistema puede sobrecargarse. El valor predeterminado es 5.
* **repeatCount**: el número de veces que una carpeta inspeccionada analiza la carpeta o el directorio. El valor -1 indica un escaneo indefinido. El valor predeterminado es -1.
* **throttleOn**: Limita el número de trabajos de la carpeta inspeccionada que se pueden procesar en un momento determinado. El número máximo de trabajos está determinado por el valor batchSize.
* **userName**: nombre de usuario utilizado al invocar un servicio de destino desde la carpeta inspeccionada. Este valor es obligatorio. El valor predeterminado es SuperAdmin.
* **domainName**: dominio del usuario. Este valor es obligatorio. El valor predeterminado es DefaultDom.
* **batchSize**: el número de archivos o carpetas que se recogerán por análisis. Utilice este valor para evitar sobrecargas en el sistema; el análisis de demasiados archivos al mismo tiempo puede provocar un bloqueo. El valor predeterminado es 2.
* **waitTime**: Tiempo, en milisegundos, que debe esperarse antes de analizar una carpeta o archivo después de su creación. Por ejemplo, si el tiempo de espera es de 36 000 000 milisegundos (una hora) y el archivo se creó hace un minuto, el archivo se recopilará después de que hayan transcurrido 59 minutos o más. Este atributo es útil para asegurarse de que un archivo o carpeta se copia completamente en la carpeta de entrada. Por ejemplo, si tiene un archivo grande para procesar y tarda diez minutos en descargarse, establezca el tiempo de espera en 10&amp;ast;60 &amp;ast;1000 milisegundos. Esta configuración evita que la carpeta vigilada analice el archivo si no ha estado esperando durante diez minutos. El valor predeterminado es 0.
* **excludeFilePattern**: Patrón que utiliza una carpeta vigilada para determinar qué archivos y carpetas analizar y recoger. Ningún archivo o carpeta que tenga este patrón se analizará para su procesamiento. Esta configuración es útil cuando la entrada es una carpeta que contiene varios archivos. El contenido de la carpeta se puede copiar en una carpeta que tenga un nombre que recogerá la carpeta vigilada. Este paso evita que la carpeta inspeccionada recoja una carpeta para procesarla antes de que la carpeta se copie completamente en la carpeta de entrada. Por ejemplo, si el valor excludeFilePattern es `data*`, todos los archivos y carpetas que coincidan `data*` no se recogen. Esto incluye archivos y carpetas llamados `data1`, `data2`, etc. Además, el patrón se puede complementar con patrones de comodines para especificar patrones de archivo. La carpeta inspeccionada modifica la expresión regular para admitir patrones de comodines como `*.*` y `*.pdf`. Estas expresiones regulares no admiten estos patrones comodín.
* **includeFilePattern**: Patrón que utiliza la carpeta vigilada para determinar qué carpetas y archivos analizar y recoger. Por ejemplo, si este valor es `*`, todos los archivos y carpetas que coincidan `input*` son recogidos. Esto incluye archivos y carpetas llamados `input1`, `input2`, etc. El valor predeterminado es `*`. Este valor indica todos los archivos y carpetas. Además, el patrón se puede complementar con patrones de comodines para especificar patrones de archivo. La carpeta inspeccionada modifica la expresión regular para admitir patrones de comodines como `*.*` y `*.pdf`. Estas expresiones regulares no admiten estos patrones comodín. Este valor es obligatorio.
* **resultFolderName**: Carpeta en la que se almacenan los resultados guardados. Esta ubicación puede ser una ruta de acceso de directorio absoluta o relativa. Si los resultados no aparecen en esta carpeta, compruebe la carpeta de errores. Los archivos de solo lectura no se procesan y se guardan en la carpeta de errores. El valor predeterminado es `result/%Y/%M/%D/`. Esta es la carpeta de resultados dentro de la carpeta vigilada.
* **preserveFolderName**: Ubicación en la que se almacenan los archivos después de analizarlos y recogerlos correctamente. Esta ubicación puede ser una ruta de directorio absoluta, relativa o nula. El valor predeterminado es `preserve/%Y/%M/%D/`.
* **failureFolderName**: Carpeta en la que se guardan los archivos de error. Esta ubicación siempre es relativa a la carpeta vigilada. Los archivos de solo lectura no se procesan y se guardan en la carpeta de errores. El valor predeterminado es `failure/%Y/%M/%D/`.
* **preserveOnFailure**: Conservar archivos de entrada en caso de que no se ejecute la operación en un servicio. El valor predeterminado es True.
* **overwriteDuplicateFilename**: cuando se establece en true, los archivos de la carpeta de resultados y de la carpeta de conservación se sobrescriben. Cuando se establece en false, los archivos y carpetas que tienen un sufijo de índice numérico se utilizan para el nombre. El valor predeterminado es False.

**Definir valores de parámetros de entrada**

Al crear un punto final de carpeta inspeccionada, debe definir los valores de parámetro de entrada. Es decir, debe describir los valores de entrada que se pasan a la operación que invoca la carpeta vigilada. Por ejemplo, considere el proceso introducido en este tema. Tiene un valor de entrada denominado `InDoc` y su tipo de datos es `com.adobe.idp.Document`. Al crear un punto final de carpeta inspeccionada para este proceso (una vez activado un proceso, se convierte en un servicio), debe definir el valor del parámetro de entrada.

Para definir los valores de parámetro de entrada necesarios para un punto final de carpeta inspeccionada, especifique los siguientes valores:

**Nombre del parámetro de entrada**: nombre del parámetro de entrada. El nombre de un valor de entrada se especifica en Workbench para un proceso. Si el valor de entrada pertenece a una operación de servicio (un servicio que no es un proceso creado en Workbench), el nombre de entrada se especifica en el archivo component.xml. Por ejemplo, el nombre del parámetro de entrada para el proceso introducido en esta sección es `InDoc`.

**Tipo de asignación**: se utiliza para configurar los valores de entrada necesarios para invocar la operación de servicio. Existen dos tipos de asignación:

* `Literal`: el punto final de la carpeta inspeccionada utiliza el valor introducido en el campo a medida que se muestra. Se admiten todos los tipos básicos de Java. Por ejemplo, si una API utiliza entradas como String, long, int y Boolean, la cadena se convierte en el tipo adecuado y se invoca el servicio.
* `Variable`: el valor introducido es un patrón de archivo que la carpeta vigilada utiliza para elegir la entrada. Por ejemplo, si selecciona Variable para el tipo de asignación y el documento de entrada debe ser un archivo de PDF, puede especificar `*.pdf`como valor de asignación.

**Valor de asignación**: especifica el valor del tipo de asignación. Por ejemplo, si selecciona una `Variable` tipo de asignación, puede especificar `*.pdf` como el patrón de archivo.

**Tipo de datos**: especifica el tipo de datos de los valores de entrada. Por ejemplo, el tipo de datos del valor de entrada del proceso introducido en esta sección es `com.adobe.idp.Document`.

**Definir un valor de parámetro de salida**

Al crear un punto final de carpeta inspeccionada, debe definir un valor de parámetro de salida. Es decir, debe describir el valor de salida que devuelve el servicio que invoca el punto final de la carpeta inspeccionada. Por ejemplo, considere el proceso introducido en este tema. Tiene un valor de salida denominado `SecuredDoc` y su tipo de datos es `com.adobe.idp.Document`. Al crear un punto final de carpeta inspeccionada para este proceso (una vez activado un proceso, se convierte en un servicio), debe definir el valor del parámetro de salida.

Para definir un valor de parámetro de salida necesario para un punto final de carpeta inspeccionada, especifique los siguientes valores:

**Nombre del parámetro de salida**: Nombre del parámetro de salida. El nombre de un valor de salida de proceso se especifica en Workbench. Si el valor de salida pertenece a una operación de servicio (un servicio que no es un proceso creado en Workbench), el nombre de salida se especifica en el archivo component.xml. Por ejemplo, el nombre del parámetro de salida para el proceso introducido en esta sección es `SecuredDoc`.

**Tipo de asignación**: se utiliza para configurar la salida del servicio y la operación. Las opciones disponibles son las siguientes:

* Si el servicio devuelve un solo objeto (un solo documento), el patrón es `%F.pdf` y el destino de origen es sourcefilename.pdf. Por ejemplo, el proceso introducido en esta sección devuelve un solo documento. Como resultado, el tipo de asignación puede definirse como `%F.pdf` ( `%F` significa utilizar el nombre de archivo dado). El patrón `%E` especifica la extensión del documento de entrada.
* Si el servicio devuelve una lista, el patrón es `Result\%F\`y el destino de origen es Result\sourcefilename\source1 (salida 1) y Result\sourcefilename\source2 (salida 2).
* Si el servicio devuelve un mapa, el patrón es `Result\%F\`y el destino de origen es Result\sourcefilename\file1 y Result\sourcefilename\file2. Si el mapa tiene más de un objeto, el patrón es `Result\%F.pdf` y el destino de origen es Result\sourcefilename1.pdf (salida 1), Result\sourcefilenam2.pdf (salida 2), etc.

**Tipo de datos**: especifica el tipo de datos del valor devuelto. Por ejemplo, el tipo de datos del valor devuelto del proceso introducido en esta sección es `com.adobe.idp.Document`.

**Crear un punto final de carpeta inspeccionada**

Después de establecer los atributos del punto de conexión, los valores de configuración y definir los valores de parámetros de entrada y salida, debe crear el punto de conexión de la carpeta inspeccionada.

**Habilitar el extremo**

Después de crear un punto final de carpeta inspeccionada, debe habilitarlo. Cuando el punto de conexión está habilitado, se puede utilizar para invocar el servicio. Después de habilitar el punto de conexión, puede verlo en la consola de administración.

**Consulte también**

[Añadir un punto final de carpeta inspeccionada mediante la API de Java](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Añadir un punto final de carpeta inspeccionada mediante la API de Java {#add-a-watched-folder-endpoint-using-the-java-api}

Añada un punto final de carpeta inspeccionada mediante la API de Java de AEM Forms:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto EndpointRegistry Client.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `EndpointRegistryClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Establezca los atributos del punto final de la carpeta inspeccionada.

   * Crear un `CreateEndpointInfo` mediante su constructor.
   * Especifique el valor del identificador del conector invocando el `CreateEndpointInfo` del objeto `setConnectorId` método y pasar el valor de cadena `WatchedFolder`.
   * Especifique la descripción del extremo invocando el `CreateEndpointInfo` del objeto `setDescription` y pasando un valor de cadena que describe el extremo.
   * Especifique el nombre del extremo invocando el `CreateEndpointInfo` del objeto `setName` y pasando un valor de cadena que especifica el nombre.
   * Especifique el servicio al que pertenece el extremo invocando el `CreateEndpointInfo` del objeto `setServiceId` y pasando un valor de cadena que especifica el nombre del servicio.
   * Especifique la operación que se invoca invocando el `CreateEndpointInfo` del objeto `setOperationName` y pasando un valor de cadena que especifica el nombre de la operación. Normalmente, al crear un punto final de carpeta inspeccionada para un servicio que se originó a partir de un proceso creado en Workbench, se invoca el nombre de la operación.

1. Especifique los valores de configuración.

   Para que cada valor de configuración se establezca para el punto final de la carpeta inspeccionada, debe invocar el `CreateEndpointInfo` del objeto `setConfigParameterAsText` método. Por ejemplo, para establecer la variable `url` valor de configuración, invoque el `CreateEndpointInfo` del objeto `setConfigParameterAsText` y pasar los siguientes valores de cadena:

   * Un valor de cadena que especifica el nombre del valor de configuración. Al configurar el `url` valor de configuración, especifique `url`.
   * Un valor de cadena que especifica el valor del valor de configuración. Al configurar el `url` valor de configuración, especifique la ubicación de la carpeta vigilada.

   >[!NOTE]
   >
   >Para ver todos los valores de configuración establecidos para el servicio EncryptDocument, consulte el ejemplo de código Java ubicado en [Inicio rápido: Agregar un punto final de carpeta inspeccionada mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api).

1. Defina los valores de parámetros de entrada.

   Defina un valor de parámetro de entrada invocando la variable `CreateEndpointInfo` del objeto `setInputParameterMapping` y pasar los siguientes valores:

   * Valor de cadena que especifica el nombre del parámetro de entrada. Por ejemplo, el nombre del parámetro de entrada para el servicio EncryptDocument es `InDoc`.
   * Valor de cadena que especifica el tipo de datos del parámetro de entrada. Por ejemplo, el tipo de datos del `InDoc` el parámetro de entrada es `com.adobe.idp.Document`.
   * Valor de cadena que especifica el tipo de asignación. Por ejemplo, puede especificar `variable`.
   * Valor de cadena que especifica el valor del tipo de asignación. Por ejemplo, puede especificar &amp;ast;.pdf como patrón de archivo.

   >[!NOTE]
   >
   >Invoque el `setInputParameterMapping` método para cada valor de parámetro de entrada que se va a definir. Dado que el proceso EncryptDocument sólo tiene un parámetro de entrada, es necesario invocar este método una vez.

1. Defina un valor de parámetro de salida.

   Defina un valor de parámetro de salida invocando el `CreateEndpointInfo` del objeto `setOutputParameterMapping` y pasar los siguientes valores:

   * Valor de cadena que especifica el nombre del parámetro de salida. Por ejemplo, el nombre del parámetro de salida para el servicio EncryptDocument es `SecuredDoc`.
   * Valor de cadena que especifica el tipo de datos del parámetro de salida. Por ejemplo, el tipo de datos del `SecuredDoc` el parámetro de salida es `com.adobe.idp.Document`.
   * Valor de cadena que especifica el tipo de asignación. Por ejemplo, puede especificar `%F.pdf`.

1. Cree un punto final de carpeta inspeccionada.

   Cree el extremo invocando el `EndpointRegistryClient` del objeto `createEndpoint` y pasando el `CreateEndpointInfo` objeto. Este método devuelve un `Endpoint` que representa el extremo de la carpeta inspeccionada.

1. Habilite el extremo.

   Habilite el punto de conexión invocando `EndpointRegistryClient` del objeto `enable` y pasando el `Endpoint` objeto que ha devuelto el `createEndpoint` método.

**Consulte también**

[Resumen de los pasos](programmatically-endpoints.md#summary-of-steps)

[Inicio rápido: Agregar un punto final de carpeta inspeccionada mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Archivo constante de valores de configuración de carpeta inspeccionada {#watched-folder-configuration-values-constant-file}

El [Inicio rápido: Agregar un punto final de carpeta inspeccionada mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) utiliza un archivo constante que debe formar parte del proyecto Java para compilar el inicio rápido. Este archivo constante representa los valores de configuración que deben establecerse al agregar un punto final de carpeta inspeccionada. El siguiente código Java representa el archivo constante.

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

Puede agregar mediante programación un extremo de correo electrónico a un servicio mediante la API de Java de AEM Forms. Al agregar un punto final de correo electrónico, permite a los usuarios enviar un mensaje de correo electrónico con uno o más archivos adjuntos a una cuenta de correo electrónico especificada. A continuación, se invoca la operación de configuración del servicio y se manipulan los archivos. Una vez que el servicio realiza la operación especificada, envía un mensaje de correo electrónico al remitente con los archivos modificados como archivos adjuntos.

Para agregar mediante programación un extremo de correo electrónico a un servicio, considere el siguiente proceso de corta duración denominado *MyApplication\EncryptDocument*. Para obtener información sobre los procesos de corta duración, consulte [Explicación de los procesos AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

Este proceso acepta un documento de PDF no protegido como valor de entrada y, a continuación, pasa el documento de PDF no protegido al servicio Encryption `EncryptPDFUsingPassword` operación. Este proceso cifra el documento de PDF con una contraseña y devuelve el documento de PDF cifrado con contraseña como valor de salida. El nombre del valor de entrada (el documento de PDF no protegido) es `InDoc` y el tipo de datos es `com.adobe.idp.Document`. El nombre del valor de salida (el documento de PDF cifrado con contraseña) es `SecuredDoc` y el tipo de datos es `com.adobe.idp.Document`.

>[!NOTE]
>
>No puede agregar un extremo de correo electrónico mediante los servicios web.

### Resumen de los pasos {#summary_of_steps-3}

Para agregar un extremo de correo electrónico a un servicio, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Crear un `EndpointRegistryClient` objeto.
1. Definir atributos de extremo de correo electrónico.
1. Especifique los valores de configuración.
1. Defina los valores de parámetros de entrada.
1. Defina un valor de parámetro de salida.
1. Cree el extremo de correo electrónico.
1. Habilite el extremo.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un objeto EndpointRegistry Client**

Antes de poder agregar un extremo de correo electrónico mediante programación, debe crear un `EndpointRegistryClient` objeto.

**Definir atributos de extremo de correo electrónico**

Para crear un extremo de correo electrónico para un servicio, especifique los siguientes valores:

* **Valor del identificador del conector**: especifica el tipo de extremo que se crea. Para crear un extremo de correo electrónico, especifique `Email`.
* **Descripción**: especifica una descripción para el extremo.
* **Nombre**: especifica el nombre del extremo.
* **Valor del identificador del servicio**: especifica el servicio al que pertenece el extremo. Por ejemplo, para agregar un extremo de correo electrónico al proceso introducido en esta sección (un proceso se convierte en servicio cuando se activa mediante Workbench), especifique `EncryptDocument`.
* **Nombre de operación**: especifica el nombre de la operación que se invoca mediante el extremo. Normalmente, al crear un extremo de correo electrónico para un servicio originado a partir de un proceso creado en Workbench, el nombre de la operación es `invoke`.

**Especificar valores de configuración**

Especifique valores de configuración para un extremo de correo electrónico al agregar mediante programación un extremo de correo electrónico a un servicio. Estos valores de configuración los especifica un administrador si se agrega un extremo de correo electrónico mediante la consola de administración.

>[!NOTE]
>
>La cuenta de correo electrónico monitorizada es una cuenta especial que solo se utiliza para el punto final de correo electrónico. Esta cuenta no es una cuenta de correo electrónico de un usuario normal. La cuenta de correo electrónico de un usuario normal no debe configurarse como la cuenta que utiliza el proveedor de correo electrónico, ya que este elimina los mensajes de correo electrónico de la bandeja de entrada una vez que ha finalizado con ellos.

Los siguientes valores de configuración se establecen al agregar mediante programación un extremo de correo electrónico a un servicio:

* **cronExpression**: Una expresión cron si el correo electrónico debe programarse mediante una expresión cron.
* **repeatCount**: Número de veces que el extremo de correo electrónico analiza la carpeta o el directorio. El valor -1 indica un escaneo indefinido. El valor predeterminado es -1.
* **repeatInterval**: Velocidad de análisis en segundos que utiliza el receptor para comprobar el correo entrante. El valor predeterminado es 10.
* **startDelay**: Tiempo de espera para analizar después de iniciar el planificador. La hora predeterminada es 0.
* **batchSize**: El número de mensajes de correo electrónico que el receptor procesa por análisis para obtener un rendimiento óptimo. El valor -1 indica todos los correos electrónicos. El valor predeterminado es 2.
* **userName**: Nombre de usuario utilizado al invocar un servicio de destinatario desde el correo electrónico. El valor predeterminado es `SuperAdmin`.
* **domainName**: Un valor de configuración obligatorio. El valor predeterminado es `DefaultDom`.
* **domainPattern**: especifica los patrones de dominio del correo electrónico entrante que acepta el proveedor. Por ejemplo, si `adobe.com` se utiliza, solo se procesa el correo electrónico de adobe.com y se ignora el correo electrónico de otros dominios.
* **filePattern**: especifica los patrones de archivos adjuntos entrantes que acepta el proveedor. Esto incluye archivos que tienen extensiones de nombre de archivo específicas (&amp;ast;.dat, &amp;ast;.xml), archivos que tienen nombres específicos (data) y archivos que tienen expresiones compuestas en el nombre y la extensión (&amp;ast;).[dD][aA]&#39;port&#39;). El valor predeterminado es `*`.
* **recipientSuccessfulJob**: Dirección de correo electrónico a la que se envían mensajes para indicar que los trabajos se han realizado correctamente. De forma predeterminada, siempre se envía un mensaje de trabajo correcto al remitente. Si escribe `sender`, los resultados del correo electrónico se envían al remitente. Se admiten hasta 100 destinatarios. Especifique destinatarios adicionales con direcciones de correo electrónico, cada uno separado por una coma. Para desactivar esta opción, deje este valor en blanco. En algunos casos, es posible que desee almacenar en déclencheur un proceso y no desee recibir una notificación del resultado por correo electrónico. El valor predeterminado es `sender`.
* **recipientFailedJob**: Dirección de correo electrónico a la que se envían mensajes para indicar trabajos fallidos. De forma predeterminada, siempre se envía un mensaje de trabajo con errores al remitente. Si escribe `sender`, los resultados del correo electrónico se envían al remitente. Se admiten hasta 100 destinatarios. Especifique destinatarios adicionales con direcciones de correo electrónico, cada uno separado por una coma. Para desactivar esta opción, deje este valor en blanco. El valor predeterminado es `sender`.
* **inboxHost**: El nombre de host de la bandeja de entrada o la dirección IP del proveedor de correo electrónico que se va a analizar.
* **inboxPort**: el puerto que utiliza el servidor de correo electrónico. El valor predeterminado de POP3 es 110 y el de IMAP es 143. Si SSL está habilitado, el valor predeterminado para POP3 es 995 y para IMAP es 993.
* **inboxProtocol**: Protocolo de correo electrónico para el extremo de correo electrónico que se utilizará para analizar la bandeja de entrada. Las opciones son `IMAP` o `POP3`. El servidor de correo host de bandeja de entrada debe admitir estos protocolos.
* **inboxTimeOut**: Tiempo de espera en segundos para que el proveedor de correo electrónico espere respuestas de la bandeja de entrada. El valor predeterminado es 60.
* **inboxUser**: nombre de usuario necesario para iniciar sesión en la cuenta de correo electrónico. Según el servidor de correo electrónico y la configuración, puede que solo sea la parte del nombre de usuario del correo electrónico o puede ser la dirección de correo electrónico completa.
* **inboxPassword**: contraseña para el usuario de la bandeja de entrada.
* **inboxSSLEnabled**: configure este valor para obligar al proveedor de correo electrónico a utilizar SSL al enviar mensajes de notificación de resultados o errores. Asegúrese de que el host IMAP o POP3 admita SSL.
* **smtpHost**: Nombre del host del servidor de correo al que el proveedor de correo electrónico envía los resultados y los mensajes de error.
* **smtpPort**: el valor predeterminado del puerto SMTP es 25.
* **smtpUser**: Cuenta de usuario que utiliza el proveedor de correo electrónico cuando envía notificaciones por correo electrónico de resultados y errores.
* **smtpPassword**: la contraseña de la cuenta SMTP. Algunos servidores de correo no requieren una contraseña SMTP.
* **charSet**: El conjunto de caracteres utilizado por el proveedor de correo electrónico. El valor predeterminado es `UTF-8`.
* **smtpSSLEnabled**: configure este valor para obligar al proveedor de correo electrónico a utilizar SSL al enviar mensajes de notificación de resultados o errores. Asegúrese de que el host SMTP admita SSL.
* **failedJobFolder**: especifica un directorio en el que almacenar los resultados cuando el servidor de correo SMTP no está operativo.
* **asíncrono**: cuando se establece en sincrónico, se procesan todos los documentos de entrada y se devuelve una sola respuesta. Cuando se establece en asíncrono, se envía una respuesta para cada documento de entrada que se procesa. Por ejemplo, se crea un extremo de correo electrónico para el proceso que se describe en este tema y se envía un mensaje de correo electrónico a la bandeja de entrada del extremo que contiene varios documentos de PDF no protegidos. Cuando todos los documentos del PDF se cifran con una contraseña y el punto de conexión se configura como sincrónico, se envía un único mensaje de correo electrónico de respuesta con todos los documentos del PDF protegidos adjuntos. Si el extremo está configurado como asincrónico, se envía un mensaje de correo electrónico de respuesta independiente para cada documento de PDF protegido. Cada mensaje de correo electrónico contiene un solo documento de PDF como datos adjuntos. El valor predeterminado es asíncrono.

**Definir valores de parámetros de entrada**

Al crear un extremo de correo electrónico, debe definir los valores de parámetros de entrada. Es decir, debe describir los valores de entrada que se pasan a la operación que invoca el extremo de correo electrónico. Por ejemplo, considere el proceso introducido en este tema. Tiene un valor de entrada denominado `InDoc` y su tipo de datos es `com.adobe.idp.Document`. Al crear un extremo de correo electrónico para este proceso (una vez activado un proceso, se convierte en un servicio), debe definir el valor del parámetro de entrada.

Para definir los valores de parámetro de entrada necesarios para un extremo de correo electrónico, especifique los siguientes valores:

**Nombre del parámetro de entrada**: nombre del parámetro de entrada. El nombre de un valor de entrada se especifica en Workbench para un proceso. Si el valor de entrada pertenece a una operación de servicio (un servicio de Forms que no es un proceso creado en Workbench), el nombre de entrada se especifica en el archivo component.xml. Por ejemplo, el nombre del parámetro de entrada para el proceso introducido en esta sección es `InDoc`.

**Tipo de asignación**: se utiliza para configurar los valores de entrada necesarios para invocar la operación de servicio. A continuación se indican dos tipos de asignación:

* `Literal`: el extremo de correo electrónico utiliza el valor introducido en el campo a medida que se muestra. Se admiten todos los tipos básicos de Java. Por ejemplo, si una API utiliza entradas como String, long, int y Boolean, la cadena se convierte al tipo adecuado y se invoca el servicio.
* `Variable`: el valor introducido es un patrón de archivo que el extremo de correo electrónico utiliza para elegir la entrada. Por ejemplo, si selecciona Variable para el tipo de asignación y el documento de entrada debe ser un archivo de PDF, puede especificar `*.pdf` como valor de asignación.

**Valor de asignación**: especifica el valor del tipo de asignación. Por ejemplo, si selecciona un tipo de asignación Variable, puede especificar `*.pdf` como el patrón de archivo.

**Tipo de datos**: especifica el tipo de datos de los valores de entrada. Por ejemplo, el tipo de datos del valor de entrada del proceso introducido en esta sección es com.adobe.idp.Document.

**Definir un valor de parámetro de salida**

Al crear un extremo de correo electrónico, debe definir un valor de parámetro de salida. Es decir, debe describir el valor de salida que devuelve el servicio que invoca el extremo de correo electrónico. Por ejemplo, considere el proceso introducido en este tema. Tiene un valor de salida denominado `SecuredDoc` y su tipo de datos es `com.adobe.idp.Document`. Al crear un extremo de correo electrónico para este proceso (una vez activado un proceso, se convierte en un servicio), debe definir el valor del parámetro de salida.

Para definir un valor de parámetro de salida necesario para un extremo de correo electrónico, especifique los siguientes valores:

**Nombre del parámetro de salida**: Nombre del parámetro de salida. El nombre de un valor de salida de proceso se especifica en Workbench. Si el valor de salida pertenece a una operación de servicio (un servicio que no es un proceso creado en Workbench), el nombre de salida se especifica en el archivo component.xml. Por ejemplo, el nombre del parámetro de salida para el proceso introducido en esta sección es `SecuredDoc`.

**Tipo de asignación**: se utiliza para configurar la salida del servicio y la operación. Las opciones disponibles son las siguientes:

* Si el servicio devuelve un solo objeto (un solo documento), el patrón es `%F.pdf` y el destino de origen es sourcefilename.pdf. Por ejemplo, el proceso introducido en esta sección devuelve un solo documento. Como resultado, el tipo de asignación puede definirse como `%F.pdf` ( `%F` significa utilizar el nombre de archivo dado). El patrón `%E` especifica la extensión del documento de entrada.
* Si el servicio devuelve una lista, el patrón es `Result\%F\`y el destino de origen es Result\sourcefilename\source1 (salida 1) y Result\sourcefilename\source2 (salida 2).
* Si el servicio devuelve un mapa, el patrón es `Result\%F\`y el destino de origen es Result\sourcefilename\file1 y Result\sourcefilename\file2. Si el mapa tiene más de un objeto, el patrón es `Result\%F.pdf` y el destino de origen es Result\sourcefilename1.pdf (salida 1), Result\sourcefilenam2.pdf (salida 2), etc.

**Tipo de datos**: especifica el tipo de datos del valor devuelto. Por ejemplo, el tipo de datos del valor devuelto del proceso introducido en esta sección es `com.adobe.idp.Document`.

**Crear el extremo de correo electrónico**

Después de establecer los atributos de punto de conexión de correo electrónico y los valores de configuración, y definir los valores de parámetros de entrada y salida, debe crear el punto de conexión de correo electrónico.

**Habilitar el extremo**

Después de crear un extremo de correo electrónico, debe habilitarlo. Cuando el punto de conexión está habilitado, se puede utilizar para invocar el servicio. Después de habilitar el punto de conexión, puede verlo en la consola de administración.

**Consulte también**

[Añadir un extremo de correo electrónico mediante la API de Java](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Añadir un extremo de correo electrónico mediante la API de Java {#add-an-email-endpoint-using-the-java-api}

Añadir un extremo de correo electrónico mediante la API de Java:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto EndpointRegistry Client.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `EndpointRegistryClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Definir atributos de extremo de correo electrónico.

   * Crear un `CreateEndpointInfo` mediante su constructor.
   * Especifique el valor del identificador del conector invocando el `CreateEndpointInfo` del objeto `setConnectorId` método y pasar el valor de cadena `Email`.
   * Especifique la descripción del extremo invocando el `CreateEndpointInfo` del objeto `setDescription` y pasando un valor de cadena que describe el extremo.
   * Especifique el nombre del extremo invocando el `CreateEndpointInfo` del objeto `setName` y pasando un valor de cadena que especifica el nombre.
   * Especifique el servicio al que pertenece el extremo invocando el `CreateEndpointInfo` del objeto `setServiceId` y pasando un valor de cadena que especifica el nombre del servicio.
   * Especifique la operación que se invoca invocando el `CreateEndpointInfo` del objeto `setOperationName` y pasando un valor de cadena que especifica el nombre de la operación. Normalmente, al crear un extremo de correo electrónico para un servicio originado a partir de un proceso creado en Workbench, se invoca el nombre de la operación.

1. Especifique los valores de configuración.

   Para cada valor de configuración que se establezca para el punto de conexión de correo electrónico, debe invocar el `CreateEndpointInfo` del objeto `setConfigParameterAsText` método. Por ejemplo, para establecer la variable `smtpHost` valor de configuración, invoque el `CreateEndpointInfo` del objeto `setConfigParameterAsText` y pasar los siguientes valores:

   * Un valor de cadena que especifica el nombre del valor de configuración. Al configurar el `smtpHost` valor de configuración, especifique `smtpHost`.
   * Un valor de cadena que especifica el valor del valor de configuración. Al configurar el `smtpHost` valor de configuración, especifique un valor de cadena que especifique el nombre del servidor SMTP.

   >[!NOTE]
   >
   >Para ver todos los valores de configuración establecidos para el servicio EncryptDocument introducidos en esta sección, consulte el ejemplo de código Java ubicado en [Inicio rápido: Añadir un punto final de correo electrónico mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api).

1. Defina los valores de parámetros de entrada.

   Defina un valor de parámetro de entrada invocando la variable `CreateEndpointInfo` del objeto `setInputParameterMapping` y pasar los siguientes valores:

   * Valor de cadena que especifica el nombre del parámetro de entrada. Por ejemplo, el nombre del parámetro de entrada para el servicio EncryptDocument es `InDoc`.
   * Valor de cadena que especifica el tipo de datos del parámetro de entrada. Por ejemplo, el tipo de datos del `InDoc` el parámetro de entrada es `com.adobe.idp.Document`.
   * Valor de cadena que especifica el tipo de asignación. Por ejemplo, puede especificar `variable`.
   * Valor de cadena que especifica el valor del tipo de asignación. Por ejemplo, puede especificar &amp;ast;.pdf como patrón de archivo.

   >[!NOTE]
   >
   >Invoque el `setInputParameterMapping` método para cada valor de parámetro de entrada que se va a definir. Dado que el proceso EncryptDocument sólo tiene un parámetro de entrada, es necesario invocar este método una vez.

1. Defina un valor de parámetro de salida.

   Defina un valor de parámetro de salida invocando el `CreateEndpointInfo` del objeto `setOutputParameterMapping` y pasando los siguientes valores:

   * Valor de cadena que especifica el nombre del parámetro de salida. Por ejemplo, el nombre del parámetro de salida para el servicio EncryptDocument es `SecuredDoc`.
   * Valor de cadena que especifica el tipo de datos del parámetro de salida. Por ejemplo, el tipo de datos del `SecuredDoc` el parámetro de salida es `com.adobe.idp.Document`.
   * Valor de cadena que especifica el tipo de asignación. Por ejemplo, puede especificar `%F.pdf`.

1. Cree el extremo de correo electrónico.

   Cree el extremo invocando el `EndpointRegistryClient` del objeto `createEndpoint` y pasando el `CreateEndpointInfo` objeto. Este método devuelve un `Endpoint` que representa el extremo de correo electrónico.

1. Habilite el extremo.

   Habilite el punto de conexión invocando `EndpointRegistryClient` del objeto `enable` y pasando el `Endpoint` objeto que ha devuelto el `createEndpoint` método.

**Consulte también**

[Resumen de los pasos](programmatically-endpoints.md#summary-of-steps)

[Inicio rápido: Agregar un punto final de carpeta inspeccionada mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Archivo constante de valores de configuración de correo electrónico {#email-configuration-values-constant-file}

El [Inicio rápido: Añadir un punto final de correo electrónico mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) utiliza un archivo constante que debe formar parte del proyecto Java para compilar el inicio rápido. Este archivo constante representa los valores de configuración que deben establecerse al agregar un extremo de correo electrónico. El siguiente código Java representa el archivo constante.

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

## Agregar extremos remotos {#adding-remoting-endpoints}

>[!NOTE]
>
>Las API de LiveCycle Remoting AEM están en desuso para los formularios de en JEE.

Puede agregar mediante programación un extremo de Remoting a un servicio mediante la API de Java de AEM Forms. Al agregar un extremo de Remoting, habilita una aplicación de Flex para invocar el servicio mediante Remoting. (Consulte [Invocar AEM Forms AEM mediante (obsoleto para formularios) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

Para agregar mediante programación un extremo de Remoting a un servicio, considere el siguiente proceso de corta duración denominado *EncryptDocument*.

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

Este proceso acepta un documento de PDF no protegido como valor de entrada y, a continuación, pasa el documento de PDF no protegido al servicio Encryption `EncryptPDFUsingPassword` operación. El documento de PDF se cifra con una contraseña y el documento de PDF cifrado con contraseña es el valor de salida de este proceso. El nombre del valor de entrada (el documento de PDF no protegido) es `InDoc` y el tipo de datos es `com.adobe.idp.Document`. El nombre del valor de salida (el documento de PDF cifrado con contraseña) es `SecuredDoc` y el tipo de datos es `com.adobe.idp.Document`.

Para mostrar cómo agregar un extremo de Remoting a un servicio, esta sección agrega un extremo de Remoting a un servicio denominado EncryptDocument.

>[!NOTE]
>
>No se puede agregar un extremo de Remoting mediante los servicios Web.

### Resumen de los pasos {#summary_of_steps-4}

Para quitar un extremo de un servicio, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Crear un `EndpointRegistryClient` objeto.
1. Establecer atributos de extremo remoto.
1. Cree un extremo remoto.
1. Habilite el extremo.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un objeto EndpointRegistry Client**

Para agregar mediante programación un extremo de Remoting, debe crear un `EndpointRegistryClient` objeto.

**Establecer atributos de extremo remoto**

Para crear un extremo remoto para un servicio, especifique los siguientes valores:

* **Valor del identificador del conector**: especifica el tipo de extremo que se crea. Para crear un extremo Remoting, especifique `Remoting`.
* **Descripción**: especifica la descripción del extremo.
* **Nombre**: especifica el nombre del extremo.
* **Valor del identificador del servicio**: especifica el servicio al que pertenece el extremo. Por ejemplo, para agregar un extremo de Remoting al proceso introducido en esta sección (un proceso se convierte en un servicio cuando se activa en Workbench), especifique `EncryptDocument`.
* **Nombre de operación**: especifica el nombre de la operación que se invoca mediante el extremo. Al crear un extremo de Remoting, especifique un carácter comodín (&amp;ast;).

**Crear un extremo remoto**

Después de establecer los atributos de extremo remoto, puede crear un extremo remoto para un servicio.

**Habilitar el extremo**

Después de crear un extremo, debe habilitarlo. Cuando se habilita un extremo de Remoting, permite a un cliente de Flex invocar el servicio.

**Consulte también**

[Agregar un extremo remoto mediante la API de Java](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Agregar un extremo remoto mediante la API de Java {#add-a-remoting-endpoint-using-the-java-api}

Agregar un extremo remoto mediante la API de Java:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto EndpointRegistry Client.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `EndpointRegistryClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Establecer atributos de extremo remoto.

   * Crear un `CreateEndpointInfo` mediante su constructor.
   * Especifique el valor del identificador del conector invocando el `CreateEndpointInfo` del objeto `setConnectorId` método y pasar el valor de cadena `Remoting`.
   * Especifique la descripción del extremo invocando el `CreateEndpointInfo` del objeto `setDescription` y pasando un valor de cadena que describe el extremo.
   * Especifique el nombre del extremo invocando el `CreateEndpointInfo` del objeto `setName` y pasando un valor de cadena que especifica el nombre.
   * Especifique el servicio al que pertenece el extremo invocando el `CreateEndpointInfo` del objeto `setServiceId` y pasando un valor de cadena que especifica el nombre del servicio.
   * Especifique la operación que invoca el `CreateEndpointInfo` del objeto `setOperationName` y pasando un valor de cadena que especifica el nombre de la operación. Para un punto final remoto, especifique un carácter comodín (&amp;ast;).

1. Cree un extremo remoto.

   Cree el extremo invocando el `EndpointRegistryClient` del objeto `createEndpoint` y pasando el `CreateEndpointInfo` objeto. Este método devuelve un `Endpoint` que representa el nuevo extremo de Remoting.

1. Habilite el extremo.

   Habilite el punto de conexión invocando `EndpointRegistryClient` del objeto `enable` y pasando el `Endpoint` objeto que ha devuelto el `createEndpoint` método.

**Consulte también**

[Resumen de los pasos](programmatically-endpoints.md#summary-of-steps)

[Inicio rápido: Agregar un extremo remoto mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Agregar extremos de TaskManager {#adding-taskmanager-endpoints}

Puede agregar mediante programación un extremo de TaskManager a un servicio mediante la API de Java de AEM Forms. Al agregar un extremo de TaskManager a un servicio, permite que un usuario de Workspace invoque el servicio. Es decir, un usuario que trabaje en Workspace puede invocar un proceso que tenga un punto final de TaskManager correspondiente.

>[!NOTE]
>
>No se puede agregar un extremo de TaskManager mediante los servicios web.

### Resumen de los pasos {#summary_of_steps-5}

Para agregar un extremo de TaskManager a un servicio, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Crear un `EndpointRegistryClient` objeto.
1. Cree una categoría para el extremo.
1. Establecer atributos de extremo de TaskManager.
1. Cree un extremo de TaskManager.
1. Habilite el extremo.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un objeto EndpointRegistry Client**

Para poder agregar mediante programación un extremo de TaskManager, debe crear un `EndpointRegistryClient` objeto.

**Crear una categoría para el extremo**

Las categorías se utilizan para organizar los servicios en Workspace. Es decir, un usuario de Workspace puede invocar un servicio que tiene un punto de conexión de TaskManager seleccionando una categoría en Workspace. Al crear un extremo de TaskManager, puede hacer referencia a una categoría existente o crear una categoría mediante programación.

>[!NOTE]
>
>Esta sección crea una nueva categoría como parte de la adición de un extremo de TaskManager a un servicio.

**Establecer atributos de extremo de TaskManager**

Para crear un extremo de TaskManager para un servicio, especifique los siguientes valores:

* **Identificador del conector**: especifica el tipo de extremo que se crea. Para crear un extremo de TaskManager, especifique `TaskManagerConnector`.
* **Descripción**: especifica la descripción del extremo.
* **Nombre**: especifica el nombre del extremo.
* **Identificador de servicio**: especifica el servicio al que pertenece el extremo.
* **Categoría**: especifica un valor de identificador de categoría asociado al extremo de TaskManager.
* **Nombre de operación**: Normalmente, cuando se crea un extremo de TaskManager para un servicio que se originó a partir de un proceso creado en Workbench, el nombre de la operación es `invoke`.

**Crear un extremo de TaskManager**

Después de establecer los atributos de extremo de TaskManager, puede crear un extremo de TaskManager para un servicio.

**Habilitar el extremo**

Después de crear un extremo, debe habilitarlo. Cuando el punto de conexión está habilitado, se puede utilizar para invocar el servicio desde Workspace. Después de habilitar el punto de conexión, puede verlo en la consola de administración.

**Consulte también**

[Agregar un extremo de TaskManager mediante la API de Java](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Agregar un extremo de TaskManager mediante la API de Java {#add-a-taskmanager-endpoint-using-the-java-api}

Agregar un extremo de TaskManager mediante la API de Java:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto EndpointRegistry Client.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `EndpointRegistryClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Cree una categoría para el extremo.

   * Crear un `CreateEndpointCategoryInfo` mediante su constructor y pasando los siguientes valores:

      * Un valor de cadena que especifica el valor de identificador de la categoría
      * Valor de cadena que especifica la descripción de la categoría

   * Cree la categoría invocando el `EndpointRegistryClient` del objeto `createEndpointCategory` y pasando el `CreateEndpointCategoryInfo` objeto. Este método devuelve un `EndpointCategory` que representa la nueva categoría.

1. Establecer atributos de extremo de TaskManager.

   * Crear un `CreateEndpointInfo` mediante su constructor.
   * Especifique el valor del identificador del conector invocando el `CreateEndpointInfo` del objeto `setConnectorId` método y pasar el valor de cadena `TaskManagerConnector`.
   * Especifique la descripción del extremo invocando el `CreateEndpointInfo` del objeto `setDescription` y pasando un valor de cadena que describe el extremo.
   * Especifique el nombre del extremo invocando el `CreateEndpointInfo` del objeto `setName` y pasando un valor de cadena que especifica el nombre.
   * Especifique el servicio al que pertenece el extremo invocando el `CreateEndpointInfo` del objeto `setServiceId` y pasando un valor de cadena que especifica el nombre del servicio.
   * Especifique la categoría a la que pertenece el extremo invocando el `CreateEndpointInfo` del objeto `setCategoryId` y pasando un valor de cadena que especifica el valor del identificador de categoría. Puede invocar el `EndpointCategory` del objeto `getId` para obtener el valor identificador de esta categoría.
   * Especifique la operación que se invoca invocando el `CreateEndpointInfo` del objeto `setOperationName` y pasando un valor de cadena que especifica el nombre de la operación. Normalmente, al crear una `TaskManager` punto final de un servicio que se originó desde un proceso creado en Workbench, el nombre de la operación es `invoke`.

1. Cree un extremo de TaskManager.

   Cree el extremo invocando el `EndpointRegistryClient` del objeto `createEndpoint` y pasando el `CreateEndpointInfo` objeto. Este método devuelve un `Endpoint` que representa el nuevo extremo de TaskManager.

1. Habilite el extremo.

   Habilite el punto de conexión invocando `EndpointRegistryClient` del objeto `enable` y pasando el `Endpoint` objeto que ha devuelto el `createEndpoint` método.

**Consulte también**

[Resumen de los pasos](programmatically-endpoints.md#summary-of-steps)

[Inicio rápido: Agregar un punto final de TaskManager mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Modificación de puntos finales {#modifying-endpoints}

Puede modificar mediante programación un extremo existente mediante la API de Java de AEM Forms. Al modificar un extremo, puede cambiar el comportamiento del extremo. Considere, por ejemplo, un punto final de carpeta inspeccionada que especifique una carpeta que se utilice como carpeta inspeccionada. Puede modificar mediante programación los valores de configuración que pertenecen al punto final de la carpeta inspeccionada, lo que da como resultado que otra carpeta funcione como carpeta inspeccionada. Para obtener información sobre los valores de configuración que pertenecen a un punto final de carpeta inspeccionada, consulte [Adición de extremos de carpeta inspeccionada](programmatically-endpoints.md#adding-watched-folder-endpoints).

Para mostrar cómo modificar un extremo, esta sección modifica un extremo de carpeta inspeccionada al cambiar la carpeta que se comporta como la carpeta inspeccionada.

>[!NOTE]
>
>No se puede modificar un extremo mediante los servicios web.

### Resumen de los pasos {#summary_of_steps-6}

Para modificar un extremo, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Crear un `EndpointRegistryClient` objeto.
1. Recupere el punto final.
1. Especifique nuevos valores de configuración.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un objeto EndpointRegistry Client**

Para modificar un extremo mediante programación, debe crear un `EndpointRegistryClient` objeto.

**Recupere el extremo que desea modificar**

Para poder modificar un extremo, debe recuperarlo. Para recuperar un extremo, debe conectarse como un usuario que puede acceder a un extremo. Se recomienda que se conecte como administrador. (Consulte [Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

Puede recuperar un extremo recuperando una lista de extremos. A continuación, puede iterar por la lista buscando el extremo específico que desea quitar. Por ejemplo, puede localizar un extremo determinando el servicio que corresponde al extremo y el tipo de extremo. Cuando encuentre el punto de conexión, podrá modificarlo.

**Especificar nuevos valores de configuración**

Al modificar un punto de conexión, especifique nuevos valores de configuración. Por ejemplo, para modificar un punto final de carpeta inspeccionada, restablezca todos los valores de configuración de punto final de carpeta inspeccionada, no solo los que desee modificar. Para obtener información sobre los valores de configuración que pertenecen a un punto final de carpeta inspeccionada, consulte [Adición de extremos de carpeta inspeccionada](programmatically-endpoints.md#adding-watched-folder-endpoints).

>[!NOTE]
>
>Para obtener información sobre los valores de configuración que pertenecen a un extremo de correo electrónico, consulte [Añadir extremos de correo electrónico](programmatically-endpoints.md#adding-email-endpoints).

>[!NOTE]
>
>No puede modificar el servicio que invoca el extremo. Si intenta modificar el servicio, se generará una excepción. Para modificar el servicio asociado a un extremo determinado, elimine el extremo y cree uno. (Consulte [Eliminación de extremos](programmatically-endpoints.md#removing-endpoints).)

**Consulte también**

[Modificación de un extremo mediante la API de Java](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Modificación de un extremo mediante la API de Java {#modifying-an-endpoint-using-the-java-api}

Modifique un extremo mediante la API de Java:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto EndpointRegistry Client.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `EndpointRegistryClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Recupere el extremo que desea modificar.

   * Recupere una lista de todos los extremos a los que puede acceder el usuario actual (especificado en las propiedades de conexión) invocando el `EndpointRegistryClient` del objeto `getEndpoints` método y pasar un `PagingFilter` que actúa como filtro. Puede pasar un `(PagingFilter)null` para devolver todos los extremos. Este método devuelve un `java.util.List` objeto donde cada elemento es un `Endpoint` objeto. Para obtener información acerca de `PagingFilter` objeto, consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Itere a través de `java.util.List` para determinar si tiene puntos finales. Si existen puntos finales, cada elemento es un `EndPoint` ejemplo.
   * Determine el servicio que corresponde a un extremo invocando el `EndPoint` del objeto `getServiceId` método. Este método devuelve un valor de cadena que especifica el nombre del servicio.
   * Determine el tipo de punto de conexión invocando el `EndPoint` del objeto `getConnectorId` método. Este método devuelve un valor de cadena que especifica el tipo de extremo. Por ejemplo, si el punto final es un punto final de carpeta inspeccionada, este método devuelve `WatchedFolder`.

1. Especifique nuevos valores de configuración.

   * Crear un `ModifyEndpointInfo` invocando su constructor.
   * Para cada valor de configuración que se va a establecer, invoque el `ModifyEndpointInfo` del objeto `setConfigParameterAsText` método. Por ejemplo, para establecer el valor de configuración de la URL, invoque el `ModifyEndpointInfo` del objeto `setConfigParameterAsText` y pasar los siguientes valores:

      * Un valor de cadena que especifica el nombre del valor de configuración. Por ejemplo, para establecer la variable `url` valor de configuración, especifique `url`.
      * Un valor de cadena que especifica el valor del valor de configuración. Para definir un valor para `url` valor de configuración, especifique la ubicación de la carpeta vigilada.

   * Invoque el `EndpointRegistryClient` del objeto `modifyEndpoint` y pase el `ModifyEndpointInfo` objeto.

**Consulte también**

[Resumen de los pasos](programmatically-endpoints.md#summary-of-steps)

[Inicio rápido: Modificación de un punto final mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eliminación de extremos {#removing-endpoints}

Puede quitar un extremo de un servicio mediante programación utilizando la API de Java de AEM Forms. Después de quitar un extremo, el servicio no se puede invocar mediante el método de invocación que habilita el extremo. Por ejemplo, si quita un extremo SOAP de un servicio, no puede invocar el servicio mediante el modo SOAP.

Para mostrar cómo quitar un extremo de un servicio, esta sección quita un extremo EJB de un servicio denominado *EncryptDocument*.

>[!NOTE]
>
>No se puede quitar un extremo mediante los servicios web.

### Resumen de los pasos {#summary_of_steps-7}

Para quitar un extremo de un servicio, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Crear un `EndpointRegistryClient` objeto.
1. Recupere el punto final.
1. Elimine el punto final.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un objeto EndpointRegistry Client**

Para quitar un extremo mediante programación, debe crear un `EndpointRegistryClient` objeto.

**Recupere el extremo que desea eliminar**

Para poder quitar un extremo, debe recuperarlo. Para recuperar un extremo, debe conectarse como un usuario que puede acceder a un extremo. Se recomienda que se conecte como administrador. (Consulte [Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

Puede recuperar un extremo recuperando una lista de extremos. A continuación, puede iterar por la lista buscando el extremo específico que desea quitar. Por ejemplo, puede localizar un extremo determinando el servicio que corresponde al extremo y el tipo de extremo. Cuando encuentre el punto de conexión, podrá eliminarlo.

**Quitar el punto final**

Después de crear un extremo, debe habilitarlo. Cuando el punto de conexión está habilitado, se puede utilizar para invocar el servicio. Después de habilitar el punto de conexión, puede verlo en la consola de administración.

**Consulte también**

[Eliminación de un extremo mediante la API de Java](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminación de un extremo mediante la API de Java {#removing-an-endpoint-using-the-java-api}

Elimine un extremo mediante la API de Java:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto EndpointRegistry Client.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `EndpointRegistryClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Recupere el extremo que desea eliminar.

   * Recupere una lista de todos los extremos a los que tiene acceso el usuario actual (especificado en las propiedades de conexión) invocando el método `EndpointRegistryClient` del objeto `getEndpoints` método y pasar un `PagingFilter` que actúa como filtro. Puedes pasar `(PagingFilter)null` para devolver todos los extremos. Este método devuelve un `java.util.List` objeto donde cada elemento es un `Endpoint` objeto.
   * Itere a través de `java.util.List` para determinar si tiene puntos finales. Si existen puntos finales, cada elemento es un `EndPoint` ejemplo.
   * Determine el servicio que corresponde a un extremo invocando el `EndPoint` del objeto `getServiceId` método. Este método devuelve un valor de cadena que especifica el nombre del servicio.
   * Determine el tipo de punto de conexión invocando el `EndPoint` del objeto `getConnectorId` método. Este método devuelve un valor de cadena que especifica el tipo de extremo. Por ejemplo, si el extremo es un extremo EJB, este método devuelve `EJB`.

1. Elimine el punto final.

   Elimine el extremo invocando el `EndpointRegistryClient` del objeto `remove` y pasando el `EndPoint` que representa el extremo que se va a quitar.

**Consulte también**

[Resumen de los pasos](programmatically-endpoints.md#summary-of-steps)

[Inicio rápido: Eliminación de un extremo mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Recuperando información del conector de extremo {#retrieving-endpoint-connector-information}

Puede recuperar información mediante programación sobre los conectores de extremos mediante la API de AEM Forms. Un conector permite que un extremo invoque un servicio mediante varios métodos de invocación. Por ejemplo, un conector de carpeta inspeccionada permite que un extremo invoque un servicio mediante carpetas inspeccionadas. Mediante la recuperación mediante programación de información acerca de los conectores de extremo, puede recuperar los valores de configuración asociados a un conector, como los valores de configuración necesarios y los opcionales.

Para demostrar cómo recuperar información sobre los conectores de extremo, esta sección recupera información sobre un conector de carpeta inspeccionada. (Consulte [Adición de extremos de carpeta inspeccionada](programmatically-endpoints.md#adding-watched-folder-endpoints).)

>[!NOTE]
>
>No se puede recuperar información sobre los extremos mediante los servicios web.

>[!NOTE]
>
>Este tema utiliza el `ConnectorRegistryClient` API para recuperar información sobre conectores de extremos. (Consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

### Resumen de los pasos {#summary_of_steps-8}

Para recuperar la información del conector de extremo, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Crear un `ConnectorRegistryClient` objeto.
1. Especifique el tipo de conector.
1. Recupere los valores de configuración.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

Si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, sustituya adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que AEM Forms está implementado. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un objeto ConnectorRegistry Client**

Para recuperar mediante programación la información del conector de extremo, cree un `ConnectorRegistryClient` objeto.

**Especificar el tipo de conector**

Especifique el tipo de conector desde el que desea recuperar la información. Existen los siguientes tipos de conectores:

* **EJB**: permite que una aplicación cliente invoque un servicio mediante el modo EJB.
* **JABÓN**: permite que una aplicación cliente invoque un servicio mediante el modo SOAP.
* **Carpeta inspeccionada**: permite que las carpetas inspeccionadas invoquen un servicio.
* **Correo electrónico**: permite que los mensajes de correo electrónico invoquen un servicio.
* **Remoting**: permite que una aplicación cliente de Flex invoque un servicio.
* **TaskManagerConnector**: permite que un usuario de Workspace invoque un servicio desde Workspace.

**Recuperar valores de configuración**

Una vez especificado el tipo de conector, se puede recuperar información sobre el conector, como el valor de configuración admitido. Por ejemplo, para cualquier conector, puede determinar qué valores de configuración son necesarios y cuáles son opcionales.

**Consulte también**

[Recuperar información del conector de extremo mediante la API de Java](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar información del conector de extremo mediante la API de Java {#retrieve-endpoint-connector-information-using-the-java-api}

Recupere información del conector de extremo mediante la API de Java:

1. Incluir archivos de proyecto. .

   Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto ConnectorRegistry Client.

   * Crear un `ServiceClientFactory` que contiene las propiedades de conexión.
   * Crear un `ConnectorRegistryClient` usando su constructor y pasando el objeto `ServiceClientFactory` objeto.

1. Especifique el tipo de conector.

   Especifique el tipo de conector invocando el `ConnectorRegistryClient` del objeto `getEndpointDefinition` y pasando un valor de cadena que especifica el tipo de conector. Por ejemplo, para especificar el tipo de conector de la carpeta inspeccionada, pase el valor de cadena `WatchedFolder`. Este método devuelve un `Endpoint` que corresponde al tipo de conector.

1. Recupere los valores de configuración.

   * Recupere los valores de configuración asociados dentro de este punto de conexión invocando el `Endpoint` del objeto `getConfigParameters` método. Este método devuelve una matriz de `ConfigParameter` objetos.
   * Recupere información sobre cada valor de configuración recuperando cada elemento dentro de la matriz. Cada elemento es un `ConfigParameter` objeto. Por ejemplo, puede determinar si el valor de configuración es obligatorio u opcional invocando la variable `ConfigParameter` del objeto `isRequired` método. Si el valor de configuración es obligatorio, este método devuelve `true`.

**Consulte también**

[Resumen de los pasos](programmatically-endpoints.md#summary-of-steps)

[Inicio rápido: Recuperación de información del conector de extremo mediante la API de Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
