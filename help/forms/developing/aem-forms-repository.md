---
title: Uso del repositorio de AEM Forms
seo-title: Uso del repositorio de AEM Forms
description: Administre el repositorio de AEM Forms para crear carpetas, escribir, lista, leer, actualizar y buscar recursos mediante la API de Java y la API de servicio web. Además, aprenda a crear relaciones con los recursos, bloquearlos y eliminarlos.
seo-description: Administre el repositorio de AEM Forms para crear carpetas, escribir, lista, leer, actualizar recursos y buscar recursos mediante la API de Java y la API de servicio web. Además, aprenda a crear relaciones con los recursos, bloquearlos y eliminarlos.
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '9157'
ht-degree: 0%

---


# Uso del repositorio de AEM Forms {#working-with-aem-forms-repository}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en el entorno JEE.**

**Acerca del servicio de repositorio**

El servicio Repositorio proporciona almacenamiento de recursos y servicios de administración a AEM Forms. Cuando los desarrolladores crean una aplicación *AEM Forms*, pueden implementar los recursos en el repositorio en lugar del sistema de archivos. Los recursos pueden incluir cualquier tipo de material colateral, incluidos formularios XML, PDF forms (incluidos formularios Acrobat), fragmentos de formulario, imágenes, perfiles, políticas, archivos SWF, archivos DDX, esquemas XML, archivos WSDL y datos de prueba.

Por ejemplo, considere la siguiente aplicación de Forms con el nombre *Aplicaciones/FormsApplication*:

![ww_ww_formrepositorio](assets/ww_ww_formrepository.png)

Observe que hay un archivo llamado Loan.xdp ubicado en FormsFolder. Para acceder a este diseño de formulario, debe especificar la ruta completa (incluida la versión): `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>Para obtener información sobre la creación de una aplicación de Forms mediante Workbench, consulte la [Ayuda de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

La ruta a un recurso ubicado en el repositorio de AEM Forms es:

`Applications/Application-name/Application-version/Folder.../Filename`

Los siguientes valores muestran algunos ejemplos de valores URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>Puede examinar el repositorio de AEM Forms mediante un navegador web. Para examinar el repositorio, introduzca la siguiente dirección URL en un explorador Web `https://[server name]:[server port]/repository`. Puede comprobar los resultados de inicio rápido asociados a la sección Uso del repositorio de AEM Forms mediante un navegador web. Por ejemplo, si agrega contenido al Repositorio de AEM Forms, puede ver el contenido en un explorador Web. (Consulte [Inicio rápido (modo SOAP): Escritura de un recurso mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api).)

La API de repositorio proporciona una serie de operaciones que puede utilizar para almacenar y recuperar información del repositorio. Por ejemplo, puede obtener una lista de recursos o recuperar recursos específicos almacenados en el repositorio cuando se necesita un recurso como parte del procesamiento de una aplicación.

>[!NOTE]
>
>La API del repositorio no se puede utilizar para interactuar con los servicios de contenido (obsoleto). Para interactuar con Content Services (obsoleto), utilice la API de administración de Documento.

Mediante la API de servicio Repositorio, puede realizar las siguientes tareas:

* Crear carpetas. Consulte [Creación de carpetas](aem-forms-repository.md#creating-folders).
* Escriba los recursos y sus propiedades. Consulte [Escritura de recursos](aem-forms-repository.md#writing-resources).
* Lista de recursos en una colección determinada o relacionados con otros recursos. Consulte [Recursos de listado](aem-forms-repository.md#listing-resources).
* Lea los recursos y sus propiedades. Consulte [Lectura de recursos](aem-forms-repository.md#reading-resources).
* Actualice los recursos y sus propiedades. Consulte [Actualización de recursos](aem-forms-repository.md#updating-resources).
* Busque recursos, incluidos su historial, recursos relacionados y propiedades. Consulte [Búsqueda de recursos](aem-forms-repository.md#searching-for-resources).
* Especifique las relaciones entre los recursos. Consulte [Creación de relaciones de recursos](aem-forms-repository.md#creating-resource-relationships).
* Administre el control de acceso de recursos, incluido el bloqueo y desbloqueo de recursos, y lea y escriba listas de control de acceso (ACL). Consulte [Bloqueo de recursos](aem-forms-repository.md#locking-resources).
* Elimine los recursos y sus propiedades. Consulte [Eliminación de recursos](aem-forms-repository.md#deleting-resources).

>[!NOTE]
>
>Con la API de repositorio, no puede administrar el control de acceso de recursos, buscar recursos ni especificar relaciones de recursos mediante un repositorio de ECM.

>[!NOTE]
>
>Cuando se escribe un PDF cifrado en el repositorio, no se puede utilizar la función de extracción de relaciones automatizada. De lo contrario, un archivo PDF cifrado se puede almacenar en el repositorio y recuperarse posteriormente. El recuperador puede elegir descifrar el PDF después de recuperarlo del repositorio.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Creación de carpetas {#creating-folders}

Las carpetas (colecciones de recursos) se utilizan para almacenar objetos (archivos o recursos) en grupos organizados. Las carpetas pueden contener recursos y otras carpetas, también conocidas como subcarpetas. Los recursos solo se pueden almacenar en una carpeta a la vez.

Los archivos heredan listas de control de acceso (ACL) de las carpetas y las subcarpetas heredan las ACL de las carpetas principales. Por lo tanto, las carpetas principales deben existir para poder crear carpetas secundarias. El IDE le permite interactuar sólo carpeta por carpeta, no archivo por archivo. No puede crear versiones de carpetas y no es necesario; una carpeta no contiene datos en sí misma. Más bien, es sólo un contenedor para los recursos que contienen datos. La ACL predeterminada es un permiso de nivel de sistema, lo que significa que los usuarios deben tener permisos de nivel de sistema (leer, escribir, recorrer, administrar ACL) hasta que alguien les conceda permisos para una carpeta en particular. Las ACL solo funcionan en el IDE.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para crear una carpeta, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree el cliente de servicio.
1. Cree la carpeta.
1. Escriba la carpeta en el repositorio.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

**Crear el cliente de servicios**

Para poder crear una colección de recursos mediante programación, debe establecer una conexión y proporcionar credenciales. Esto se logra creando un cliente de servicio.

**Crear la carpeta**

Invoque el método de servicio Repositorio para crear la colección de recursos y rellenar la colección de recursos con información de identificación, incluyendo su UUID, nombre de carpeta y descripción.

**Escribir la carpeta en el repositorio**

Invoque el método de servicio Repositorio para escribir la colección de recursos, especificando el URI de la carpeta de destinatario.

**Consulte también**

[Creación de carpetas mediante la API de Java](aem-forms-repository.md#create-folders-using-the-java-api)

[Creación de carpetas mediante la API de servicio Web](aem-forms-repository.md#create-folders-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API de servicio de repositorio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Crear carpetas con la API de Java {#create-folders-using-the-java-api}

Cree una carpeta mediante la API del servicio Repositorio (Java):

1. Incluir archivos de proyecto

   Incluya archivos de proyecto en la ruta de clases del proyecto Java.

1. Crear el cliente de servicios

   Cree un objeto `ResourceRepositoryClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Crear la carpeta

   Para crear una colección de recursos, primero debe crear un objeto `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`.

   Invoque el método `repositoryInfomodelFactoryBean` del objeto `newResourceCollection` y pase los parámetros siguientes:

   * Un identificador UUID `com.adobe.repository.infomodel.Id` que se asignará al recurso.
   * Un identificador UUID `com.adobe.repository.infomodel.Lid` que se asignará al recurso.
   * Un `java.lang.String` que contiene el nombre de la colección de recursos. Por ejemplo, `FormsFolder`.

   El método devuelve un objeto `com.adobe.repository.infomodel.bean.ResourceCollection` que representa la nueva carpeta.

   Defina la descripción de la carpeta con el método `setDescription` y pase el siguiente parámetro:

   * Un `String` que describe la colección de recursos. En este ejemplo, se utiliza `"test Folder"` `.`


1. Escribir la carpeta en el repositorio

   Invoque el método `ResourceRepositoryClient` del objeto `writeResource` y pase el URI de la carpeta y el objeto `ResourceCollection`. Por ejemplo, el URI de la carpeta puede ser el siguiente valor `/Applications/FormsApplication/1.0/`.

   El método devuelve una instancia del objeto `com.adobe.repository.infomodel.bean.Resource` recién creado. Por ejemplo, puede recuperar el valor de identificador del nuevo recurso invocando el método `com.adobe.repository.infomodel.bean.Resource` del objeto `getId`.

**Consulte también**

[Creación de carpetas](aem-forms-repository.md#creating-folders)

[Inicio rápido (modo SOAP): Creación de una carpeta mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Crear carpetas mediante la API de servicio Web {#create-folders-using-the-web-service-api}

Cree una carpeta mediante la API del servicio Repositorio (servicio Web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el WSDL de repositorio mediante base64.
   * Haga referencia al ensamblado de cliente de Microsoft .NET.

1. Crear el cliente de servicios

   Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `RepositoryServiceService` invocando su constructor predeterminado. Establezca su propiedad `Credentials` mediante un objeto `System.Net.NetworkCredential` que contenga el nombre de usuario y la contraseña.

1. Crear la carpeta

   Cree la carpeta utilizando el constructor predeterminado para la clase `ResourceCollection` y pase los parámetros siguientes:

   * Un objeto `Id`, que se crea invocando el constructor predeterminado para la clase `Id` y se asigna al campo `Resource` del objeto `id`.
   * Un objeto `Lid`, que se crea invocando el constructor predeterminado para la clase `Lid` y se asigna al campo `Resource` del objeto `lid`.
   * Una cadena que contiene el nombre de la colección de recursos, que se asigna al campo `Resource` del objeto `name`. El nombre utilizado en este ejemplo es `"testfolder"`.
   * Una cadena que contiene la descripción de la colección de recursos, que se asigna al campo `Resource` del objeto `description`. La descripción utilizada en este ejemplo es `"test folder"`.

1. Escribir la carpeta en el repositorio

   Invoque el método `RepositoryServiceService` del objeto `writeResource` y pase los parámetros siguientes:

   * Ruta de acceso donde se creará la carpeta.
   * El objeto `ResourceCollection` que representa la carpeta.
   * Pase `null` para los otros dos parámetros.

**Consulte también**

[Creación de carpetas](aem-forms-repository.md#creating-folders)

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Escritura de recursos {#writing-resources}

Puede crear recursos en una ubicación determinada del repositorio. El tamaño natural del archivo está sujeto a las limitaciones de la base de datos y al tiempo de espera de sesión. Para la configuración predeterminada, los archivos están limitados a 25 MB. Para aumentar o reducir el tamaño máximo del archivo, debe cambiar la configuración de la base de datos.

Escribir recursos equivale a almacenar datos en el repositorio. Una vez que se escribe un recurso en el repositorio, se convierte en accesible para todos los clientes del ecosistema del repositorio. Al escribir recursos en el repositorio, como esquemas XML, archivos XDP y archivos XSD, el contenido se analiza en función del tipo MIME. Si se admite el tipo MIME, el analizador determina si existe una relación implícita con otro contenido. Por ejemplo, si una hoja de estilo en cascada (CSS) tiene una URL relativa que hace referencia a una CSS común, se espera que también envíe la CSS común al repositorio. La relación entre los dos recursos se almacena como una relación pendiente durante un período no ajustable de 30 días. Cuando envía la CSS común al repositorio dentro del período de 30 días, se forma la relación.

Al crear un recurso, la lista de control de acceso (ACL) se hereda de la carpeta principal. La carpeta raíz tiene permisos de nivel de sistema hasta que se crea un recurso o una carpeta inicial, momento en el cual se otorgan permisos de ACL predeterminados al recurso o la carpeta.

Puede escribir recursos mediante programación mediante la API de Java del servicio Repositorio o la API de servicio Web.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para escribir un recurso, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio Repositorio.
1. Especifique el URI del recurso que se va a leer.
1. Lea el recurso.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

**Crear el cliente de servicios**

Para poder leer un recurso mediante programación, debe establecer una conexión y proporcionar credenciales. Esto se logra creando un cliente de servicio.

**Especifique el URI de la carpeta de destinatario del recurso**

Cree una cadena que contenga el URI del recurso que se va a leer. La sintaxis incluye barras diagonales, como en este ejemplo: &quot;/*path*/*folder*&quot;.

**Crear el recurso**

Invoque el método de servicio Repositorio para crear el recurso y rellene el recurso con información de identificación, incluido su UUID, nombre del recurso y descripción.

**Especificar el contenido del recurso**

Invoque el método de servicio Repositorio para crear contenido de recursos y almacenarlo en el recurso.

**Escribir el recurso en la carpeta destinatario**

Invoque el método de servicio Repositorio para escribir el recurso, especificando el URI de la carpeta destinatario.

**Consulte también**

[Escribir recursos mediante la API de Java](aem-forms-repository.md#write-resources-using-the-java-api)

[Escribir recursos mediante la API de servicio web](aem-forms-repository.md#write-resources-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API de servicio de repositorio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Escribir recursos mediante la API de Java {#write-resources-using-the-java-api}

Escriba un recurso mediante la API de servicio de repositorio (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clases del proyecto Java.

1. Crear el cliente de servicios

   Cree un objeto `ResourceRepositoryClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Especifique el URI de la carpeta de destinatario del recurso

   Especifique el URI de la carpeta de destinatario del recurso. En este caso, como el recurso denominado `testResource` se almacenará en la carpeta `testFolder`, el URI de la carpeta es `"/testFolder"`. El URI se almacena como un objeto `java.lang.String`.

1. Crear el recurso

   Para crear un recurso, primero debe crear un objeto `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`.

   Invocar el método `RepositoryInfomodelFactoryBean` del objeto `newResource`, que crea un objeto `com.adobe.repository.infomodel.bean.Resource`. En este ejemplo, se proporcionan los siguientes parámetros:

   * Un objeto `com.adobe.repository.infomodel.Id`, que se crea invocando el constructor predeterminado para la clase `Id`.
   * Un objeto `com.adobe.repository.infomodel.Lid`, que se crea invocando el constructor predeterminado para la clase `Lid`.
   * `java.lang.String` que contiene el nombre de archivo del recurso.

   Para especificar la descripción del recurso, invoque el método `Resource` del objeto `setDescription` y pase una cadena que contenga la descripción. En este ejemplo, la descripción es `"test resource"`.

1. Especificar el contenido del recurso

   Para crear contenido para el recurso, invoque el método `RepositoryInfomodelFactoryBean` del objeto `newResourceContent`, que devuelve un objeto `com.adobe.repository.infomodel.bean.ResourceContent`. Añada contenido al objeto `ResourceContent`. En este ejemplo, esto se logra realizando las siguientes tareas:

   * Invocar el método `ResourceContent` del objeto `setDataDocument` y pasar un objeto `com.adobe.idp.Document`
   * Invocar el método `ResourceContent` del objeto `setSize` y pasar el tamaño en bytes del objeto `Document`

   Añada el contenido al recurso invocando el método `Resource` del objeto `setContent` y pasando el objeto `ResourceContent`. Para obtener más información, consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Escribir el recurso en la carpeta destinatario

   Invoque el método `ResourceRepositoryClient` del objeto `writeResource` y pase el URI de la carpeta, así como el objeto `Resource`.

**Consulte también**

[Escritura de recursos](aem-forms-repository.md#writing-resources)

[Inicio rápido (modo SOAP): Escritura de un recurso mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Escribir recursos mediante la API de servicio Web {#write-resources-using-the-web-service-api}

Escriba un recurso mediante la API de servicio de repositorio (servicio Web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el WSDL de repositorio mediante base64.
   * Haga referencia al ensamblado de cliente de Microsoft .NET.

1. Crear el cliente de servicios

   Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `RepositoryServiceService` invocando su constructor predeterminado. Establezca su propiedad `Credentials` mediante un objeto `System.Net.NetworkCredential` que contenga el nombre de usuario y la contraseña.

1. Especifique el URI de la carpeta de destinatario del recurso

   Especifique el URI de la carpeta de destinatario del recurso. En este caso, como el recurso denominado `testResource` se almacenará en la carpeta `testFolder`, el URI de la carpeta es `"/testFolder"`. Cuando utilice un idioma compatible con Microsoft .NET Framework (por ejemplo, C#), almacene el URI en un objeto `System.String`.

1. Crear el recurso

   Para crear un recurso, invoque el constructor predeterminado para la clase `Resource`. En este ejemplo, la siguiente información se almacena en el objeto `Resource`:

   * Un objeto `com.adobe.repository.infomodel.Id`, que se crea invocando el constructor predeterminado para la clase `Id` y se asigna al campo `Resource` del objeto `id`.
   * Un objeto `com.adobe.repository.infomodel.Lid`, que se crea invocando el constructor predeterminado para la clase `Lid` y se asigna al campo `Resource` del objeto `lid`.
   * Una cadena que contiene el nombre de archivo del recurso, que se asigna al campo `Resource` del objeto `name`. El nombre utilizado en este ejemplo es `"testResource"`.
   * Una cadena que contiene la descripción del recurso, que se asigna al campo `Resource` del objeto `description`. La descripción utilizada en este ejemplo es `"test resource"`.

1. Especificar el contenido del recurso

   Para crear contenido para el recurso, invoque el constructor predeterminado para la clase `ResourceContent`. A continuación, agregue contenido al objeto `ResourceContent`. En este ejemplo, esto se logra realizando las siguientes tareas:

   * Asignación de un objeto `BLOB` que contenga un documento al campo `ResourceContent` del objeto `dataDocument`.
   * Asignación del tamaño en bytes del objeto `BLOB` al campo `ResourceContent` del objeto `size`.

   Añada el contenido al recurso asignando el objeto `ResourceContent` al campo `Resource` del objeto `content`.

1. Escribir el recurso en la carpeta destinatario

   Invoque el método `RepositoryServiceService` del objeto `writeResource` y pase el URI de la carpeta, así como el objeto `Resource`. Pase `null` para los otros dos parámetros.

**Consulte también**

[Escritura de recursos](aem-forms-repository.md#writing-resources)

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Recursos de listado {#listing-resources}

Puede descubrir recursos enumerando los recursos. Se realiza una consulta en el repositorio para encontrar todos los recursos relacionados con una colección de recursos determinada.

Una vez que haya organizado los recursos, podrá inspeccionar la estructura que ha creado al ver una rama concreta de la estructura, como lo haría en un sistema operativo.

Los recursos de listado funcionan según la relación: los recursos son miembros de carpetas. La afiliación está representada por una relación de tipo &quot;miembro de&quot;. Al lista de recursos en una carpeta determinada, se realiza una consulta de recursos relacionados con una carpeta determinada por el &quot;miembro de&quot; de la relación. Las relaciones son direccionales: un miembro de una relación tiene una fuente que es miembro del destinatario. La fuente es el recurso; el destinatario es la carpeta principal.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para lista de recursos, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree el cliente de servicio.
1. Especifique la ruta de la carpeta.
1. Recuperar la lista de recursos.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

**Crear el cliente de servicios**

Para poder crear una colección de recursos mediante programación, debe establecer una conexión y proporcionar credenciales. Esto se logra creando un cliente de servicio.

**Especificar la ruta de la carpeta**

Cree una cadena que contenga la ruta de la carpeta que contenga los recursos. La sintaxis incluye barras diagonales, como en este ejemplo: &quot;/*path*/*folder*&quot;.

**Recuperar la lista de recursos**

Invocar el método de servicio Repositorio para recuperar la lista de recursos, especificando la ruta de la carpeta destinatario.

**Consulte también**

[Recursos de lista mediante la API de Java](aem-forms-repository.md#list-resources-using-the-java-api)

[Recursos de lista mediante la API de servicio web](aem-forms-repository.md#list-resources-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API de servicio de repositorio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Recursos de lista mediante la API de Java {#list-resources-using-the-java-api}

Recursos de lista mediante la API del servicio Repositorio (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clases del proyecto Java.

1. Crear el cliente de servicios

   Cree un objeto `ResourceRepositoryClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Especificar la ruta de la carpeta

   Especifique el URI de la colección de recursos que se va a consultar. En este caso, su URI es `"/testFolder"`. El URI se almacena como un objeto `java.lang.String`.

1. Recuperar la lista de recursos

   Invoque el método `ResourceRepositoryClient` del objeto `listMembers` y pase el URI de la carpeta.

   El método devuelve un `java.util.List` de `com.adobe.repository.infomodel.bean.Resource` objetos que son el origen de un `com.adobe.repository.infomodel.bean.Relation` de tipo `Relation.TYPE_MEMBER_OF` y tienen el URI de recopilación de recursos como destinatario. Puede iterar por este `List` para recuperar cada uno de los recursos. En este ejemplo, se muestra el nombre y la descripción de cada recurso.

**Consulte también**

[Recursos](aem-forms-repository.md#listing-resources) de listado.

[Inicio rápido (modo SOAP): Lista de recursos mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recursos de lista mediante la API de servicio Web {#list-resources-using-the-web-service-api}

Recursos de lista mediante la API del servicio Repositorio (servicio Web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el WSDL de repositorio.
   * Haga referencia al ensamblado de cliente de Microsoft .NET.

1. Crear el cliente de servicios

   Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `RepositoryServiceService` invocando su constructor predeterminado. Establezca su propiedad `Credentials` mediante un objeto `System.Net.NetworkCredential` que contenga el nombre de usuario y la contraseña.

1. Especificar la ruta de la carpeta

   Especifique una cadena que contenga el URI de la carpeta que se va a consultar. En este caso, su URI es `"/testFolder"`. Cuando utilice un idioma compatible con Microsoft .NET Framework (por ejemplo, C#), almacene el URI en un objeto `System.String`.

1. Recuperar la lista de recursos

   Invoque el método `RepositoryServiceService` del objeto `listMembers` y pase el URI de la carpeta como el primer parámetro. Pase `null` para los otros dos parámetros.

   El método devuelve una matriz de objetos que se pueden convertir en objetos `Resource`. Puede iterar por la matriz de objetos para recuperar cada uno de los recursos relacionados. En este ejemplo, se muestra el nombre y la descripción de cada recurso.

**Consulte también**

[Recursos](aem-forms-repository.md#listing-resources) de listado.

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Leyendo recursos {#reading-resources}

Puede recuperar recursos de una ubicación determinada del repositorio para leer su contenido y metadatos. El flujo de trabajo es un formulario de inicialización. El proceso tiene todos los permisos necesarios para leer el formulario. El sistema recupera el formulario de datos y lee el contenido del repositorio. El repositorio otorga acceso al contenido y a los metadatos (la capacidad de saber si el recurso existe).

El repositorio tiene los cuatro tipos de permisos siguientes:

* **traverse**: permite la lista de recursos; es decir, para leer metadatos de recursos, pero no contenido de recursos
* **lea**: le permite leer contenido de recursos
* **escribir**: le permite escribir contenido de recursos
* **administración de listas de control de acceso (ACL)**: le permite manipular las ACL en los recursos

Los usuarios solo pueden ejecutar procesos cuando tienen permiso para ejecutar el proceso. Los usuarios de IDE necesitan permisos de lectura y travesía para sincronizar con el repositorio. Las ACL solo se aplican en tiempo de diseño porque el tiempo de ejecución se produce en el contexto del sistema.

Puede leer recursos mediante programación mediante la API de Java del servicio Repositorio o la API de servicio Web.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-3}

Para leer un recurso, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio Repositorio.
1. Especifique el URI del recurso que se va a leer.
1. Lea el recurso.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

**Crear el cliente de servicios**

Para poder leer un recurso mediante programación, debe establecer una conexión y proporcionar credenciales. Esto se logra creando un cliente de servicio.

**Especifique el URI del recurso que se va a leer**

Cree una cadena que contenga el URI del recurso que se va a leer. La sintaxis incluye barras diagonales, como en este ejemplo: &quot;/*path*/*resource*&quot;.

**Leer el recurso**

Invoque el método del servicio Repositorio para leer el recurso, especificando el URI.

**Consulte también**

[Leer recursos mediante la API de Java](aem-forms-repository.md#read-resources-using-the-java-api)

[Lectura de recursos mediante la API de servicio web](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API de servicio de repositorio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Leer recursos usando la API de Java {#read-resources-using-the-java-api}

Lea un recurso mediante la API de servicio de repositorio (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clases del proyecto Java.

1. Crear el cliente de servicios

   Cree un objeto `ResourceRepositoryClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Especifique el URI del recurso que se va a leer

   Especifique un valor de cadena que represente el URI del recurso que se va a recuperar. Por ejemplo, suponiendo que el recurso se llame *testResource*, que se encuentra en una carpeta denominada *testFolder*, especifique `/testFolder/testResource`.

1. Leer el recurso

   Invoque el método `ResourceRepositoryClient` del objeto `readResource` y pase el URI del recurso como parámetro. Este método devuelve una instancia `Resource` que representa el recurso.

**Consulte también**

[Lectura de recursos](aem-forms-repository.md#reading-resources)

[Inicio rápido (modo SOAP): Lectura de un recurso mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Lectura de recursos mediante la API de servicio Web {#reading-resources-using-the-web-service-api}

Lea un recurso mediante la API de servicio Repositorio (servicio Web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el WSDL de repositorio. (Consulte [Creación de un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)
   * Haga referencia al ensamblado de cliente de Microsoft .NET. (Consulte [Creación de un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Crear el cliente de servicios

   Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `RepositoryServiceService` invocando su constructor predeterminado. Establezca su propiedad `Credentials` mediante un objeto `System.Net.NetworkCredential` que contenga el nombre de usuario y la contraseña.

1. Especifique el URI del recurso que se va a leer

   Especifique una cadena que contenga el URI del recurso que se va a recuperar. En este caso, como el recurso denominado `testResource` está en la carpeta `testFolder`, su URI es `"/testFolder/testResource"`. Cuando utilice un idioma compatible con Microsoft .NET Framework (por ejemplo, C#), almacene el URI en un objeto `System.String`.

1. Leer el recurso

   Invoque el método `RepositoryServiceService` del objeto `readResource` y pase el URI del recurso como el primer parámetro. Pase `null` para los otros dos parámetros.

**Consulte también**

[Lectura de recursos](aem-forms-repository.md#reading-resources)

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Actualizando recursos {#updating-resources}

Puede recuperar y actualizar el contenido de los recursos en el repositorio. Al actualizar los recursos, el control de acceso a esos recursos permanece sin cambios entre las versiones. Al realizar una actualización, tiene la opción de incrementar la versión principal. Si no decide incrementar la versión principal, la versión secundaria se actualiza automáticamente.

Al actualizar un recurso, la nueva versión se crea en función de los atributos de recurso especificados. Al actualizar un recurso, se especifican dos parámetros importantes: el URI de destinatario y una instancia de recurso que contiene todos los metadatos actualizados. Es importante tener en cuenta que si no cambia un atributo determinado (por ejemplo, el nombre), el atributo seguirá siendo necesario en la instancia que pase. Las relaciones que se crean al analizar el contenido se agregan a la versión específica y no se presentan a menos que se especifique.

Por ejemplo, si actualiza un archivo XDP y contiene referencias a otros recursos, también se registrarán esas referencias adicionales. Supongamos que form.xdp versión 1.0 tiene dos referencias externas: un logotipo y una hoja de estilo, y posteriormente se actualiza form.xdp para que ahora tenga tres referencias: un logotipo, una hoja de estilo y un archivo esquema. Durante la actualización, el repositorio agregará la tercera relación (al archivo esquema) a su tabla de relación pendiente. Una vez que el archivo esquema esté presente en el repositorio, la relación se formará automáticamente. Sin embargo, si form.xdp versión 2.0 ya no utiliza el logotipo, la versión 2.0 de form.xdp no tendrá relación con el logotipo.

Todas las operaciones de actualización son atómicas y transaccionales. Por ejemplo, si dos usuarios leen el mismo recurso y ambos deciden actualizar la versión 1.0 a la versión 2.0, uno de ellos se realizará correctamente y uno de ellos fallará, se mantendrá la integridad del repositorio y ambos obtendrán un mensaje que confirme el éxito o el error. Si la transacción no se confirma, se reenviará en caso de error en la base de datos y se agotará el tiempo de espera o se revirtirá en función del servidor de aplicaciones.

Puede actualizar los recursos mediante programación mediante la API de Java del servicio Repositorio o la API de servicio Web.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-4}

Para actualizar un recurso, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio Repositorio.
1. Recupere el recurso que se va a actualizar.
1. Actualice el recurso.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

**Crear el cliente de servicios**

Para poder leer un recurso mediante programación, debe establecer una conexión y proporcionar credenciales. Esto se logra creando un cliente de servicio.

**Recuperar el recurso que se va a actualizar**

Lea el recurso. Para obtener más información, consulte [Lectura de recursos](aem-forms-repository.md#reading-resources).

**Actualizar el recurso**

Configure la nueva información en el recurso e invoque el método de servicio Repositorio para actualizar el recurso, especificando el URI, el recurso actualizado y cómo se debe actualizar la información de la versión.

**Consulte también**

[Actualización de recursos mediante la API de Java](aem-forms-repository.md#update-resources-using-the-java-api)

[Actualización de recursos mediante la API de servicio web](aem-forms-repository.md#update-resources-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API de servicio de repositorio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Actualizar recursos mediante la API de Java {#update-resources-using-the-java-api}

Actualice un recurso mediante la API del servicio Repositorio (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clases del proyecto Java.

1. Crear el cliente de servicios

   Cree un objeto `ResourceRepositoryClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Recuperar el recurso que se va a actualizar

   Especifique el URI del recurso para recuperarlo y leerlo. En este ejemplo, el URI del recurso es `"/testFolder/testResource"`.

1. Actualizar el recurso

   Actualice la información del objeto `Resource`. En este ejemplo, para actualizar la descripción, invoque el método `Resource` del objeto `setDescription` y pase la nueva cadena de descripción como parámetro.

   A continuación, invoque el método `ServiceClientFactory` del objeto `updateResource` y pase los parámetros siguientes:

   * Un objeto `java.lang.String` que contiene el URI del recurso.
   * El objeto `Resource` que contiene la información de recursos actualizada.
   * Un valor `boolean` que indica si se debe actualizar la versión principal o la secundaria. En este ejemplo, se pasa un valor de `true` para indicar que se va a incrementar la versión principal.

**Consulte también**

[Actualización de recursos](aem-forms-repository.md#updating-resources)

[Inicio rápido (modo SOAP): Actualización de un recurso mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Actualizar recursos mediante la API de servicio Web {#update-resources-using-the-web-service-api}

Actualice un recurso mediante la API de repositorio (servicio Web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el WSDL de repositorio.
   * Haga referencia al ensamblado de cliente de Microsoft .NET.

1. Crear el cliente de servicios

   Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `RepositoryServiceService` invocando su constructor predeterminado. Establezca su propiedad `Credentials` mediante un objeto `System.Net.NetworkCredential` que contenga el nombre de usuario y la contraseña.

1. Recuperar el recurso que se va a actualizar

   Especifique el URI del recurso que se va a recuperar y lea el recurso. En este ejemplo, el URI del recurso es `"/testFolder/testResource"`. Para obtener más información, consulte [Lectura de recursos](aem-forms-repository.md#reading-resources).

1. Actualizar el recurso

   Actualice la información del objeto `Resource`. En este ejemplo, para actualizar la descripción, asigne un nuevo valor al campo `Resource` del objeto `description`.

1. Invoque el método `RepositoryServiceService` del objeto `updateResource` y pase los parámetros siguientes:

   * Un objeto `System.String` que contiene el URI del recurso.
   * El objeto `Resource` que contiene la información de recursos actualizada.
   * Un valor `boolean` que indica si se debe actualizar la versión principal o la secundaria. En este ejemplo, se pasa un valor de `true` para indicar que se va a incrementar la versión principal.
   * Pase `null` para los dos parámetros restantes.

**Consulte también**

[Actualización de recursos](aem-forms-repository.md#updating-resources)

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Buscando recursos {#searching-for-resources}

Puede construir consultas que se utilizan para buscar recursos en el repositorio, incluidos el historial, los recursos relacionados y las propiedades.

Puede recuperar recursos relacionados para determinar las dependencias entre un formulario y sus fragmentos. Por ejemplo, si tiene un formulario, puede determinar qué fragmentos o recursos externos utiliza. Si tiene una imagen, también puede averiguar qué formularios utilizan la imagen. También puede buscar recursos relacionados mediante el filtrado basado en propiedades. Por ejemplo, puede buscar todos los formularios que utilicen una imagen con un nombre especificado o buscar cualquier imagen utilizada por un formulario con un nombre especificado. También puede realizar búsquedas con propiedades de recurso. Por ejemplo, puede llevar a cabo una consulta para buscar todos los formularios o recursos cuyos inicios de nombre tengan una cadena determinada que pueda incluir caracteres comodín ’%’ y ’_’. Recuerde que las búsquedas basadas en propiedades no se basan en relaciones; estas búsquedas se basan en la suposición de que tiene conocimientos específicos sobre un recurso determinado.

**Declaraciones de consulta**

Una *consulta* contiene una o más afirmaciones que se unen lógicamente con condiciones. Una *instrucción* consta de un operando izquierdo, un operador y un operando derecho. Además, puede especificar el orden que se usará para los resultados de búsqueda. El *criterio de ordenación* contiene información equivalente a una cláusula SQL `ORDER BY` y consta de elementos que contienen los atributos en los que se basó la búsqueda, así como un valor que indica si se va a utilizar el orden ascendente o descendente.

Puede buscar recursos mediante programación mediante la API de Java del servicio Repositorio. En este momento, no es posible utilizar la API de servicio Web para buscar recursos.

**Comportamiento de ordenación**

El orden no se respeta cuando se invoca el método `ResourceRepositoryClient` del objeto `searchProperties` y se especifica un criterio de ordenación. Por ejemplo, supongamos que crea un recurso con tres propiedades personalizadas, donde los nombres de atributo son `name`, `secondName` y `asecondName`. A continuación, se crea un elemento de orden de clasificación en el nombre del atributo y se establece el valor `ascending` en `true`.

A continuación, invoque el método `ResourceRepositoryClient` del objeto `searchProperties` y pase el orden. La búsqueda devuelve el recurso correcto, con las tres propiedades. Sin embargo, las propiedades no se ordenan por nombre de atributo. Se devuelven en el orden en que se añadieron: `name`, `secondName` y `asecondName`.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-5}

Para buscar recursos, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio Repositorio.
1. Especifique la carpeta de destinatario para la búsqueda.
1. Especifique los atributos utilizados en la búsqueda.
1. Cree la consulta utilizada en la búsqueda.
1. Cree el orden para los resultados de la búsqueda.
1. Busque los recursos.
1. Recupere los recursos del resultado de búsqueda.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

**Crear el cliente de servicios**

Para poder leer un recurso mediante programación, debe establecer una conexión y proporcionar credenciales. Esto se logra creando un cliente de servicio.

**Especifique la carpeta de destinatario para la búsqueda**

Cree una cadena que contenga la ruta de acceso base desde la cual realizar la búsqueda. La sintaxis incluye barras diagonales, como en este ejemplo: &quot;/*path*/*folder*&quot;.

**Especifique los atributos utilizados en la búsqueda**

Puede basar la búsqueda en los atributos contenidos dentro de los recursos. Especifique los valores de los atributos en los que se realizará la búsqueda.

**Crear la consulta utilizada en la búsqueda**

Construya una consulta mediante instrucciones y condiciones. Cada instrucción especificará el atributo en el que se basará la búsqueda, la condición que se utilizará y el valor de atributo que se utilizará en la búsqueda.

**Crear el orden para los resultados de búsqueda**

El orden de clasificación consta de elementos, cada uno de los cuales contiene uno de los atributos utilizados en la búsqueda y un valor que indica si se va a utilizar el orden ascendente o descendente.

**Buscar recursos**

Busque los recursos con la carpeta, la consulta y el orden. Además, indique la profundidad de la búsqueda y un límite superior en el número de resultados que se van a devolver.

**Recuperar los recursos del resultado de búsqueda**

Repetir mediante la lista devuelta de recursos y extraer la información para su posterior procesamiento.

**Consulte también**

[Buscar recursos con la API de Java](aem-forms-repository.md#search-for-resources-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API de servicio de repositorio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Buscar recursos con la API de Java {#search-for-resources-using-the-java-api}

Busque un recurso mediante la API de servicio Repositorio (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clases del proyecto Java.

1. Crear el cliente de servicios

   Cree un objeto `ResourceRepositoryClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Especifique la carpeta de destinatario para la búsqueda

   Especifique el URI de la ruta de acceso base desde la que se ejecutará la búsqueda. En este ejemplo, el URI del recurso es `/testFolder`.

1. Especifique los atributos utilizados en la búsqueda

   Especifique los valores de los atributos en los que se realizará la búsqueda. Los atributos existen dentro de un objeto `com.adobe.repository.infomodel.bean.Resource`. En este ejemplo, la búsqueda se realizará en el atributo name; por lo tanto, se utiliza un `java.lang.String` que contiene el nombre del objeto `Resource`, que en este caso es `testResource`.

1. Crear la consulta utilizada en la búsqueda

   Para crear una consulta, cree un objeto `com.adobe.repository.query.Query` invocando el constructor predeterminado para la clase `Query` y agregue sentencias a la consulta.

   Para crear una sentencia, invoque el constructor para la clase `com.adobe.repository.query.Query.Statement` y pase los siguientes parámetros:

   * Operando izquierdo que contiene la constante de atributo de recurso. En este ejemplo, como el nombre del recurso se utiliza como base para la búsqueda, se utiliza el valor estático `Resource.ATTRIBUTE_NAME`.
   * Operador que contiene la condición utilizada en la búsqueda del atributo. El operador debe ser una de las constantes estáticas de la clase `Query.Statement`. En este ejemplo, se utiliza el valor estático `Query.Statement.OPERATOR_BEGINS_WITH`.
   * Operando derecho que contiene el valor de atributo en el que se realizará la búsqueda. En este ejemplo, se utiliza el atributo name, un `String` que contiene el valor `"testResource"`.

   Especifique la Área de nombres del operando izquierdo invocando el método `Query.Statement` del objeto `setNamespace` y pasando uno de los valores estáticos contenidos en la clase `com.adobe.repository.infomodel.bean.ResourceProperty`. En este ejemplo, se utiliza `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY`.

   Añada cada instrucción en la consulta invocando el método `Query` del objeto `addStatement` y pasando el objeto `Query.Statement`.

1. Crear el orden para los resultados de búsqueda

   Para especificar el criterio de ordenación utilizado en los resultados de búsqueda, cree un objeto `com.adobe.repository.query.sort.SortOrder` invocando el constructor predeterminado para la clase `SortOrder` y agregue elementos al criterio de ordenación.

   Para crear un elemento para el orden de clasificación, invoque uno de los constructores para la clase `com.adobe.repository.query.sort.SortOrder.Element`. En este ejemplo, como el nombre del recurso se utiliza como base para la búsqueda, se utiliza el valor estático `Resource.ATTRIBUTE_NAME` como primer parámetro y el orden ascendente (un valor `boolean` de `true`) se especifica como segundo parámetro.

   Añada cada elemento al orden invocando el método `SortOrder` del objeto `addSortElement` y pasando el objeto `SortOrder.Element`.

1. Buscar recursos

   Para buscar `resources` según las propiedades de atributo, invoque el método `ResourceRepositoryClient` del objeto `searchProperties` y pase los parámetros siguientes:

   * Un `String` que contiene la ruta base desde la cual ejecutar la búsqueda. En este caso, se utiliza `"/testFolder"`.
   * Consulta utilizada en la búsqueda.
   * Profundidad de la búsqueda. En este caso, `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` se utiliza para indicar que se utilizarán la ruta de acceso base y todas sus carpetas.
   * Un valor `int` que indica la primera fila desde la que se selecciona el conjunto de resultados sin paginar. En este ejemplo, se especifica `0`.
   * Un valor `int` que indica el número máximo de resultados que se van a devolver. En este ejemplo, se especifica `10`.
   * Orden utilizado en la búsqueda.

   El método devuelve un `java.util.List` de `Resource` objetos en el orden de clasificación especificado.

1. Recuperar los recursos del resultado de búsqueda

   Para recuperar los recursos contenidos en el resultado de la búsqueda, repita el `List` y convierta cada objeto en `Resource` para extraer su información. En este ejemplo, se muestra el nombre de cada recurso.

**Consulte también**

[Búsqueda de recursos](aem-forms-repository.md#searching-for-resources)

[Inicio rápido (modo SOAP): Búsqueda de recursos mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Creación de relaciones de recursos {#creating-resource-relationships}

Puede especificar relaciones entre los recursos del repositorio. Existen tres tipos de relaciones:

* **Dependencia**: una relación en la que un recurso depende de otros recursos, lo que significa que todos los recursos relacionados son necesarios en el repositorio.
* **Membresía (sistema de archivos)**: una relación en la que un recurso se encuentra dentro de una carpeta determinada.
* **Personalizado**: una relación que se especifica entre los recursos. Por ejemplo, si un recurso se ha desaprobado y otro se ha introducido en el repositorio, puede especificar su propia relación de reemplazo.

Puede crear sus propias relaciones personalizadas. Por ejemplo, si almacena un archivo HTML en el repositorio y utiliza una imagen, puede especificar una relación personalizada para relacionar el archivo HTML con la imagen (ya que normalmente solo los archivos XML se asocian con imágenes mediante una relación de dependencia definida por el repositorio). Otro ejemplo de relación personalizada sería si desea crear una vista diferente del repositorio con una estructura de gráficos cíclica en lugar de una estructura de árbol. Puede definir un gráfico circular junto con un visor para recorrer esas relaciones. Por último, puede indicar que un recurso reemplaza a otro aunque los dos recursos sean completamente diferentes. En ese caso, puede definir un tipo de relación fuera del rango reservado y crear una relación entre esos dos recursos. Su aplicación sería el único cliente que podría detectar y procesar la relación, y podría utilizarse para realizar búsquedas en esa relación.

Puede especificar mediante programación las relaciones entre los recursos mediante la API de Java del servicio Repositorio o la API de servicio Web.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-6}

Para especificar una relación entre dos recursos, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio Repositorio.
1. Especifique los URI de los recursos que se van a relacionar.
1. Cree la relación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

**Crear el cliente de servicios**

Para poder leer un recurso mediante programación, debe establecer una conexión y proporcionar credenciales. Esto se logra creando un cliente de servicio.

**Especifique los URI de los recursos que se van a relacionar**

Cree cadenas que contengan los URI del recurso que se va a relacionar. La sintaxis incluye barras diagonales, como en este ejemplo: &quot;/*path*/*resource*&quot;.

**Crear la relación**

Invoque el método de servicio Repositorio para crear y especificar el tipo de relación.

**Consulte también**

[Creación de recursos de relación mediante la API de Java](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[Creación de recursos de relación mediante la API de servicio web](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API de servicio de repositorio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Crear recursos de relación mediante la API de Java {#create-relationship-resources-using-the-java-api}

Cree recursos de relación mediante la API de Java del servicio Repositorio, lleve a cabo las siguientes tareas:

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clases del proyecto Java.

1. Crear el cliente de servicios

   Cree un objeto `ResourceRepositoryClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Especifique los URI de los recursos que se van a relacionar

   Especifique los URI de los recursos que se van a relacionar. En este caso, como los recursos se denominan `testResource1` y `testResource2` y se encuentran en la carpeta `testFolder`, sus URI son `"/testFolder/testResource1"` y `"/testFolder/testResource2"`. Los URI se almacenan como objetos `java.lang.String`. En este ejemplo, los recursos se escriben primero en el repositorio y se recuperan sus URI. Para obtener más información sobre cómo escribir un recurso, consulte [Escritura de recursos](aem-forms-repository.md#writing-resources).

1. Crear la relación

   Invoque el método `ResourceRepositoryClient` del objeto `createRelationship` y pase los parámetros siguientes:

   * URI del recurso de origen.
   * URI del recurso de destinatario.
   * El tipo de relación, que es una de las constantes estáticas de la clase `com.adobe.repository.infomodel.bean.Relation`. En este ejemplo, se establece una relación de dependencia especificando el valor `Relation.TYPE_DEPENDANT_OF`.
   * Un valor `boolean` que indica si el recurso de destinatario se actualiza automáticamente al identificador basado en `com.adobe.repository.infomodel.Id` del nuevo recurso principal. En este ejemplo, debido a la relación de dependencia, se especifica el valor `true`.

   También puede recuperar una lista de recursos relacionados para un recurso determinado invocando el método `ResourceRepositoryClient` del objeto `getRelated` y pasando los parámetros siguientes:

   * URI del recurso para el que se recuperan los recursos relacionados. En este ejemplo, se especifica el recurso de origen ( `"/testFolder/testResource1"`).
   * Un valor `boolean` que indica si el recurso especificado es el recurso de origen en la relación. En este ejemplo, se especifica el valor `true` porque éste es el caso.
   * El tipo de relación, que es una de las constantes estáticas de la clase `Relation`. En este ejemplo, se especifica una relación de dependencia utilizando el mismo valor utilizado anteriormente: `Relation.TYPE_DEPENDANT_OF`.

   El método `getRelated` devuelve un `java.util.List` de `Resource` objetos a través de los cuales puede iterar para recuperar cada uno de los recursos relacionados, convirtiendo los objetos contenidos en el `List` en `Resource` a medida que lo hace. En este ejemplo, se espera que `testResource2` esté en la lista de los recursos devueltos.

**Consulte también**

[Creación de relaciones de recursos](aem-forms-repository.md#creating-resource-relationships)

[Inicio rápido (modo SOAP): Creación de relaciones entre recursos mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Crear recursos de relación mediante la API de servicio Web {#create-relationship-resources-using-the-web-service-api}

Cree recursos de relación mediante la API de repositorio (servicio Web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el WSDL de repositorio.
   * Haga referencia al ensamblado de cliente de Microsoft .NET.

1. Crear el cliente de servicios

   Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `RepositoryServiceService` invocando su constructor predeterminado. Establezca su propiedad `Credentials` mediante un objeto `System.Net.NetworkCredential` que contenga el nombre de usuario y la contraseña.

1. Especifique los URI de los recursos que se van a relacionar

   Especifique los URI de los recursos que se van a relacionar. En este caso, como los recursos se denominan `testResource1` y `testResource2` y se encuentran en la carpeta `testFolder`, sus URI son `"/testFolder/testResource1"` y `"/testFolder/testResource2"`. Cuando se utiliza un idioma compatible con Microsoft .NET Framework (por ejemplo, C#), los URI se almacenan como objetos `System.String`. En este ejemplo, los recursos se escriben primero en el repositorio y se recuperan sus URI. Para obtener más información sobre cómo escribir un recurso, consulte [Escritura de recursos](aem-forms-repository.md#writing-resources).

1. Crear la relación

   Invoque el método `RepositoryServiceService` del objeto `createRelationship` y pase los parámetros siguientes:

   * URI del recurso de origen.
   * URI del recurso de destinatario.
   * Tipo de relación. En este ejemplo, se establece una relación de dependencia especificando el valor `3`.
   * Un valor `boolean` que indica si se especificó el tipo de relación. En este ejemplo, se especifica el valor `true`.
   * Un valor `boolean` que indica si el recurso de destinatario se actualiza automáticamente al identificador basado en `Id` del nuevo recurso principal. En este ejemplo, debido a la relación de dependencia, se especifica el valor `true`.
   * Un valor `boolean` que indica si se especificó el encabezado del destinatario. En este ejemplo, se especifica el valor `true`.
   * Pase `null` para el último parámetro.

   También puede recuperar una lista de recursos relacionados para un recurso determinado invocando el método `RepositoryServiceService` del objeto `getRelated` y pasando los parámetros siguientes:

   * URI del recurso para el que se recuperan los recursos relacionados. En este ejemplo, se especifica el recurso de origen ( `"/testFolder/testResource1"`).
   * Un valor `boolean` que indica si el recurso especificado es el recurso de origen en la relación. En este ejemplo, se especifica el valor `true` porque éste es el caso.
   * Un valor `boolean` que indica si se especificó el recurso de origen. En este ejemplo, se proporciona el valor `true`.
   * Matriz de enteros que contiene los tipos de relación. En este ejemplo, se especifica una relación de dependencia utilizando el mismo valor en la matriz que se utilizó anteriormente: `3`.
   * Pase `null` para los dos parámetros restantes.

   El método `getRelated` devuelve una matriz de objetos que se pueden convertir en `Resource` objetos a través de los cuales se puede iterar para recuperar cada uno de los recursos relacionados. En este ejemplo, se espera que `testResource2` esté en la lista de los recursos devueltos.

**Consulte también**

[Creación de relaciones de recursos](aem-forms-repository.md#creating-resource-relationships)

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Bloqueo de recursos {#locking-resources}

Puede bloquear un recurso o conjunto de recursos para su uso exclusivo por un usuario en particular o para uso compartido entre más de un usuario. Un bloqueo compartido indica que algo va a suceder con el recurso, pero no impide que nadie más actúe con ese recurso. Un bloqueo compartido debe considerarse un mecanismo de señalización. Un bloqueo exclusivo significa que el usuario que bloqueó el recurso va a cambiar el recurso y el bloqueo garantiza que nadie más pueda hacerlo hasta que el usuario ya no necesite acceder al recurso y haya liberado el bloqueo. Si un administrador de repositorio desbloquea un recurso, se eliminarán automáticamente todos los bloqueos exclusivos y compartidos de ese recurso. Este tipo de acción está pensado para situaciones en las que un usuario ya no está disponible y no ha desbloqueado el recurso.

Cuando un recurso está bloqueado, aparece un icono de candado cuando se vista la ficha Recursos ubicada en Workbench, como se muestra en la siguiente ilustración.

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

Puede controlar mediante programación el acceso a los recursos mediante la API de Java del servicio Repositorio o la API de servicio Web.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-7}

Para bloquear y desbloquear recursos, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio Repositorio.
1. Especifique el URI del recurso que se va a bloquear.
1. Bloquear el recurso.
1. Recupere los bloqueos del recurso.
1. Desbloquear el recurso

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

**Crear el cliente de servicios**

Para poder leer un recurso mediante programación, debe establecer una conexión y proporcionar credenciales. Esto se logra creando un cliente de servicio.

**Especifique el URI del recurso que se va a bloquear**

Cree una cadena que contenga el URI del recurso que se va a bloquear. La sintaxis incluye barras diagonales, como en este ejemplo: &quot;/*path*/*resource*&quot;.

**Bloquear el recurso**

Invoque el método de servicio Repositorio para bloquear el recurso, especificando el URI, el tipo de bloqueo y la profundidad de bloqueo.

**Recuperar los bloqueos del recurso**

Invoque el método de servicio Repositorio para recuperar los bloqueos del recurso, especificando el URI.

**Desbloquear el recurso**

Invocar el método del servicio Repositorio para desbloquear el recurso, especificando el URI.

**Consulte también**

[Bloquear recursos con la API de Java](aem-forms-repository.md#lock-resources-using-the-java-api)

[Bloquear recursos mediante la API de servicio web](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API de servicio de repositorio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Bloquear recursos con la API de Java {#lock-resources-using-the-java-api}

Bloquear recursos mediante la API del servicio Repositorio (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clases del proyecto Java.

1. Crear el cliente de servicios

   Cree un objeto `ResourceRepositoryClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Especifique el URI del recurso que se va a bloquear

   Especifique el URI del recurso que se va a bloquear. En este caso, como el recurso denominado `testResource` está en la carpeta `testFolder`, su URI es `"/testFolder/testResource"`. El URI se almacena como un objeto `java.lang.String`.

1. Bloquear el recurso

   Invoque el método `ResourceRepositoryClient` del objeto `lockResource` y pase los parámetros siguientes:

   * URI del recurso.
   * Ámbito de bloqueo. En este ejemplo, como el recurso se bloqueará para uso exclusivo, el ámbito de bloqueo se especifica como `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`.
   * Profundidad de bloqueo. En este ejemplo, como el bloqueo se aplicará únicamente al recurso en particular y a ninguno de sus miembros o elementos secundarios, la profundidad de bloqueo se especifica como `Lock.DEPTH_ZERO`.

   >[!NOTE]
   >
   >La versión sobrecargada del método `lockResource` que requiere cuatro parámetros emite una excepción. Asegúrese de utilizar el método `lockResource` que requiere tres parámetros, como se muestra en este tutorial.

1. Recuperar los bloqueos del recurso

   Invoque el método `ResourceRepositoryClient` del objeto `getLocks` y pase el URI del recurso como parámetro. El método devuelve una Lista de objetos Lock a través de la cual se puede iterar. En este ejemplo, el propietario del bloqueo, la profundidad y el ámbito se imprimen para cada objeto invocando los métodos `getOwnerUserId`, `getDepth` y `getType` de cada objeto Lock, respectivamente.

1. Desbloquear el recurso

   Invoque el método `ResourceRepositoryClient` del objeto `unlockResource` y pase el URI del recurso como parámetro. Para obtener más información, consulte la [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Consulte también**

[Bloqueo de recursos](aem-forms-repository.md#locking-resources)

[Inicio rápido (modo SOAP): Bloqueo de un recurso mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Bloquear recursos con la API de servicio Web {#lock-resources-using-the-web-service-api}

Bloquear recursos mediante la API de servicio Repositorio (servicio Web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el WSDL de repositorio mediante Base64.
   * Haga referencia al ensamblado de cliente de Microsoft .NET.

1. Crear el cliente de servicios

   Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `RepositoryServiceService` invocando su constructor predeterminado. Establezca su propiedad `Credentials` mediante un objeto `System.Net.NetworkCredential` que contenga el nombre de usuario y la contraseña.

1. Especifique el URI del recurso que se va a bloquear

   Especifique una cadena que contenga el URI del recurso que se va a bloquear. En este caso, como el recurso denominado `testResource` está en la carpeta `testFolder`, su URI es `"/testFolder/testResource"`. Cuando utilice un idioma compatible con Microsoft .NET Framework (por ejemplo, C#), almacene el URI en un objeto `System.String`.

1. Bloquear el recurso

   Invoque el método `RepositoryServiceService` del objeto `lockResource` y pase los parámetros siguientes:

   * URI del recurso.
   * Ámbito de bloqueo. En este ejemplo, como el recurso se bloqueará para uso exclusivo, el ámbito de bloqueo se especifica como `11`.
   * Profundidad de bloqueo. En este ejemplo, como el bloqueo se aplicará únicamente al recurso en particular y a ninguno de sus miembros o elementos secundarios, la profundidad de bloqueo se especifica como `2`.
   * Un valor `int` que indica el número de segundos hasta que caduca el bloqueo. En este ejemplo, se utiliza el valor de `1000`.
   * Pase `null` para el último parámetro.

1. Recuperar los bloqueos del recurso

   Invoque el método `RepositoryServiceService` del objeto `getLocks` y pase el URI del recurso como el primer parámetro y `null` para el segundo parámetro. El método devuelve una matriz `object` que contiene objetos `Lock` a través de los cuales puede iterar. En este ejemplo, el propietario del bloqueo, la profundidad y el ámbito se imprimen para cada objeto accediendo a los campos `Lock` `ownerUserId`, `depth` y `type` de cada objeto, respectivamente.

1. Desbloquear el recurso

   Invoque el método `RepositoryServiceService` del objeto `unlockResource` y pase el URI del recurso como el primer parámetro y `null` para el segundo parámetro.

**Consulte también**

[Bloqueo de recursos](aem-forms-repository.md#locking-resources)

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Eliminación de recursos {#deleting-resources}

Puede eliminar recursos mediante programación desde una ubicación determinada del repositorio mediante la API de Java (SOAP) del servicio Repositorio.

Cuando elimina un recurso, la eliminación es normalmente permanente, aunque en algunos casos los repositorios de ECM pueden almacenar las versiones del recurso según sus mecanismos de historial. Por lo tanto, al eliminar un recurso, es importante asegurarse de que nunca más necesitará ese recurso. Los motivos comunes para eliminar un recurso incluyen la necesidad de aumentar el espacio disponible en la base de datos. Puede eliminar una versión de un recurso, pero si lo hace, debe especificar el identificador de recurso y no su identificador lógico (LID) o ruta. Si elimina una carpeta, todo lo que contenga, incluidas las subcarpetas y los recursos, se eliminará automáticamente.

Los recursos relacionados no se eliminan. Por ejemplo, si tiene un formulario que utiliza el archivo logo.gif y elimina logo.gif, se almacenará una relación en la tabla de relación pendiente. Como alternativa, para la desaprobación de versiones, establezca el estado del objeto de la última versión en desaprobado.

Una operación de eliminación no es segura para las transacciones en los sistemas ECM. Por ejemplo, si intenta eliminar 100 recursos y la operación falla en el recurso número 50, se eliminarán las primeras 49 instancias pero el resto no. De lo contrario, el comportamiento predeterminado es rollback (no compromiso).

>[!NOTE]
>
>Al utilizar el método `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` con el repositorio de ECM (Content Server de Documentum de EMC y FileNet P8 Content Manager de IBM), la transacción no se revertirá si falla la eliminación de uno de los recursos especificados, lo que significa que los archivos que se han eliminado no se pueden eliminar.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-8}

Para eliminar un recurso, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio Repositorio.
1. Especifique el URI del recurso que se va a eliminar.
1. Elimine el recurso.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, incluya los archivos proxy.

**Crear el cliente de servicios**

Para poder leer un recurso mediante programación, debe establecer una conexión y proporcionar credenciales. Esto se logra creando un cliente de servicio.

**Especifique el URI del recurso que se va a eliminar**

Cree una cadena que contenga el URI del recurso que se va a eliminar. La sintaxis incluye barras diagonales, como en este ejemplo: &quot;/*path*/*resource*&quot;. Si el recurso que se va a eliminar es una carpeta, la eliminación será recursiva.

**Eliminar el recurso**

Invoque el método del servicio Repositorio para eliminar el recurso, especificando el URI.

**Consulte también**

[Eliminar recursos mediante la API de Java](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[Eliminar recursos mediante la API de servicio Web](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API de servicio de repositorio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Eliminar recursos mediante la API de Java (SOAP) {#delete-resources-using-the-java-api-soap}

Elimine un recurso mediante la API de repositorio (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clases del proyecto Java.

1. Crear el cliente de servicios

   Cree un objeto `ResourceRepositoryClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Especifique el URI del recurso que se va a eliminar

   Especifique el URI del recurso que se va a recuperar. En este caso, como el recurso llamado testResourceToBeDeleted está en la carpeta denominada testFolder, su URI es `/testFolder/testResourceToBeDeleted`. El URI se almacena como un objeto `java.lang.String`. En este ejemplo, el recurso se escribe primero en el repositorio y se recupera su URI. Para obtener más información sobre cómo escribir un recurso, consulte [Escritura de recursos](aem-forms-repository.md#writing-resources).

1. Eliminar el recurso

   Invoque el método `ResourceRepositoryClient` del objeto `deleteResource` y pase el URI del recurso como parámetro.

**Consulte también**

[Eliminación de recursos](aem-forms-repository.md#deleting-resources)

[Inicio rápido (modo SOAP): Búsqueda de recursos mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminar recursos mediante la API de servicio Web {#delete-resources-using-the-web-service-api}

Elimine un recurso mediante la API de repositorio (servicio Web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el WSDL de repositorio mediante Base64.
   * Haga referencia al ensamblado de cliente de Microsoft .NET.

1. Crear el cliente de servicios

   Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `RepositoryServiceService` invocando su constructor predeterminado. Establezca su propiedad `Credentials` mediante un objeto `System.Net.NetworkCredential` que contenga el nombre de usuario y la contraseña.

1. Especifique el URI del recurso que se va a eliminar

   Especifique el URI del recurso que se va a recuperar. En este caso, como el recurso denominado `testResourceToBeDeleted` está en la carpeta `testFolder`, su URI es `"/testFolder/testResourceToBeDeleted"`. En este ejemplo, el recurso se escribe primero en el repositorio y se recupera su URI. Para obtener más información sobre cómo escribir un recurso, consulte [Escritura de recursos](aem-forms-repository.md#writing-resources).

1. Eliminar el recurso

   Invoque el método `RepositoryServiceService` del objeto `deleteResources` y pase una matriz `System.String` que contenga el URI del recurso como el primer parámetro. Pase `null` para el segundo parámetro.

**Consulte también**

[Eliminación de recursos](aem-forms-repository.md#deleting-resources)

[Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
