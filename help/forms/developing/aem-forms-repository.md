---
title: Trabajar con el repositorio de AEM Forms
description: Administre el repositorio de AEM Forms para crear carpetas, escribir, enumerar, leer, actualizar y buscar recursos mediante la API de Java y la API de servicio web. Además, aprenda a crear relaciones de recursos, bloquear y eliminar recursos.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: a07e51ca-fea0-4719-8071-1b7e805de2ae
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '9036'
ht-degree: 1%

---

# Trabajar con el repositorio de AEM Forms {#working-with-aem-forms-repository}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

**Acerca del servicio de repositorio**

El servicio Repositorio proporciona servicios de gestión y almacenamiento de recursos a AEM Forms. Cuando los desarrolladores crean un *AEM Forms* pueden implementar los recursos en el repositorio en lugar del sistema de archivos. Los recursos pueden incluir cualquier tipo de material colateral, incluidos formularios XML, PDF forms (incluidos formularios Acrobat), fragmentos de formulario, imágenes, perfiles, directivas, archivos de SWF, archivos DDX, esquemas XML, archivos WSDL y datos de prueba.

Por ejemplo, considere la siguiente aplicación de Forms denominada *Aplicaciones/FormsApplication*:

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

Observe que hay un archivo denominado Loan.xdp en la carpeta FormsFolder. Para acceder a este diseño de formulario, debe especificar la ruta completa (incluida la versión): `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>Para obtener información sobre la creación de una aplicación de Forms mediante Workbench, consulte [Ayuda de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

La ruta a un recurso en el repositorio de AEM Forms es:

`Applications/Application-name/Application-version/Folder.../Filename`

Los siguientes valores muestran algunos ejemplos de valores de URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>Puede examinar el repositorio de AEM Forms utilizando un explorador web. Para examinar el repositorio, introduzca la siguiente URL en un explorador web `https://[server name]:[server port]/repository`. Puede comprobar los resultados de inicio rápido asociados a la sección Uso del repositorio de AEM Forms mediante un explorador web. Por ejemplo, si agrega contenido al repositorio de AEM Forms, puede verlo en un explorador web. (Consulte [SOAP Inicio rápido (modo de): Escritura de un recurso mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api).)

La API del repositorio proporciona varias operaciones que puede utilizar para almacenar y recuperar información del repositorio. Por ejemplo, puede obtener una lista de recursos o recuperar recursos específicos almacenados en el repositorio cuando se necesite un recurso como parte del procesamiento de una aplicación.

>[!NOTE]
>
>La API del repositorio no se puede usar para interactuar con Content Services (obsoleto). Para interactuar con Content Services (obsoleto), utiliza la API de Administración de documentos.

Mediante la API del servicio de repositorio, puede realizar las siguientes tareas:

* Cree carpetas. Consulte [Creación de carpetas](aem-forms-repository.md#creating-folders).
* Recursos de escritura y sus propiedades. Consulte [Recursos de escritura](aem-forms-repository.md#writing-resources).
* Enumerar recursos de una colección determinada o relacionados con otros recursos. Consulte [Listando recursos](aem-forms-repository.md#listing-resources).
* Recursos de lectura y sus propiedades. Consulte [Leyendo recursos](aem-forms-repository.md#reading-resources).
* Actualizar recursos y sus propiedades. Consulte [Actualización de recursos](aem-forms-repository.md#updating-resources).
* Busque recursos, incluido su historial, recursos relacionados y propiedades. Consulte [Búsqueda de recursos](aem-forms-repository.md#searching-for-resources).
* Especifique las relaciones entre los recursos. Consulte [Creación de relaciones de recursos](aem-forms-repository.md#creating-resource-relationships).
* Administrar el control de acceso a recursos, incluidos el bloqueo y desbloqueo de recursos y la lectura y escritura de listas de control de acceso (ACL). Consulte [Bloqueo de recursos](aem-forms-repository.md#locking-resources).
* Eliminar recursos y sus propiedades. Consulte [Eliminación de recursos](aem-forms-repository.md#deleting-resources).

>[!NOTE]
>
>Con la API del repositorio, no puede administrar el control de acceso a recursos, buscar recursos ni especificar relaciones de recursos mediante un repositorio de ECM.

>[!NOTE]
>
>Cuando se escribe un PDF cifrado en el repositorio, no se puede utilizar la función de extracción automatizada de relaciones. De lo contrario, se puede almacenar un PDF cifrado en el repositorio y recuperarlo más tarde. El recuperador puede optar por descifrar el PDF después de recuperarlo del repositorio.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Creación de carpetas {#creating-folders}

Las carpetas (colecciones de recursos) se utilizan para almacenar objetos (archivos o recursos) en agrupaciones organizadas. Las carpetas pueden contener recursos y otras carpetas, también conocidas como subcarpetas. Los recursos solo se pueden almacenar en una carpeta a la vez.

Los archivos heredan las listas de control de acceso (ACL) de las carpetas y las subcarpetas heredan las ACL de sus carpetas principales. Por lo tanto, las carpetas principales deben existir antes de poder crear carpetas secundarias. El IDE permite interactuar únicamente carpeta por carpeta, no archivo por archivo. No puede crear versiones de carpetas y no es necesario; una carpeta no contiene datos en sí. En su lugar, solo es un contenedor para recursos que contienen datos. La ACL predeterminada es el permiso del sistema, lo que significa que los usuarios deben tener permisos del sistema (leer, escribir, recorrer y administrar ACL) hasta que alguien les conceda permisos para una carpeta en particular. Las ACL solo funcionan en el IDE.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para crear una carpeta, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree el cliente de servicios.
1. Cree la carpeta.
1. Escriba la carpeta en el repositorio.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Creación del cliente de servicios**

Para poder crear mediante programación una colección de recursos, debe establecer una conexión y proporcionar credenciales. Esto se logra creando un cliente de servicio.

**Cree la carpeta**

Invoque el método del servicio de repositorio para crear la colección de recursos y rellenarla con información de identificación, incluido su UUID, nombre de carpeta y descripción.

**Escribir la carpeta en el repositorio**

Invoque el método del servicio de repositorio para escribir la colección de recursos, especificando el URI de la carpeta de destino.

**Consulte también**

[Creación de carpetas con la API de Java](aem-forms-repository.md#create-folders-using-the-java-api)

[Creación de carpetas mediante la API de servicio web](aem-forms-repository.md#create-folders-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de repositorio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Creación de carpetas con la API de Java {#create-folders-using-the-java-api}

Cree una carpeta mediante la API de servicio de repositorio (Java):

1. Incluir archivos de proyecto

   Incluya archivos de proyecto en la ruta de clase de su proyecto Java.

1. Creación del cliente de servicios

   Crear un `ResourceRepositoryClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. Cree la carpeta

   Para crear una colección de recursos, primero debe crear una `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` objeto.

   Invoque el `repositoryInfomodelFactoryBean` del objeto `newResourceCollection` y pase los siguientes parámetros:

   * A `com.adobe.repository.infomodel.Id` Identificador UUID que se va a asignar al recurso.
   * A `com.adobe.repository.infomodel.Lid` Identificador UUID que se va a asignar al recurso.
   * A `java.lang.String` que contiene el nombre de la colección de recursos. Por ejemplo, `FormsFolder`.

   El método devuelve un valor `com.adobe.repository.infomodel.bean.ResourceCollection` que representa la nueva carpeta.

   Defina la descripción de la carpeta utilizando `setDescription` y pase el siguiente parámetro:

   * A `String` que describe la colección de recursos. En este ejemplo, `"test Folder"` se utiliza `.`

1. Escribir la carpeta en el repositorio

   Invoque el `ResourceRepositoryClient` del objeto `writeResource` y pase el URI de la carpeta y el `ResourceCollection` objeto. Por ejemplo, el URI de la carpeta puede ser el siguiente valor `/Applications/FormsApplication/1.0/`.

   El método devuelve una instancia del recién creado `com.adobe.repository.infomodel.bean.Resource` objeto. Por ejemplo, puede recuperar el valor del identificador del nuevo recurso invocando el método `com.adobe.repository.infomodel.bean.Resource` del objeto `getId` método.

**Consulte también**

[Creación de carpetas](aem-forms-repository.md#creating-folders)

[SOAP Inicio rápido (modo de): Creación de una carpeta mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creación de carpetas mediante la API de servicio web {#create-folders-using-the-web-service-api}

Cree una carpeta mediante la API del servicio de repositorio (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL del repositorio utilizando base64.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Creación del cliente de servicios

   Mediante el ensamblado de cliente de Microsoft .NET, cree un `RepositoryServiceService` invocando su constructor predeterminado. Establezca su `Credentials` propiedad con un `System.Net.NetworkCredential` que contiene el nombre de usuario y la contraseña.

1. Cree la carpeta

   Cree la carpeta utilizando el constructor predeterminado para `ResourceCollection` y pasar los siguientes parámetros:

   * Un `Id` , que se crea invocando el constructor predeterminado para el objeto `Id` y se asigna a la `Resource` del objeto `id` field.
   * Un `Lid` , que se crea invocando el constructor predeterminado para el objeto `Lid` y se asigna a la `Resource` del objeto `lid` field.
   * Cadena que contiene el nombre de la colección de recursos, que se asigna a la variable `Resource` del objeto `name` field. El nombre utilizado en este ejemplo es `"testfolder"`.
   * Cadena que contiene la descripción de la colección de recursos, que se asigna a la variable `Resource` del objeto `description` field. La descripción utilizada en este ejemplo es `"test folder"`.

1. Escribir la carpeta en el repositorio

   Invoque el `RepositoryServiceService` del objeto `writeResource` y pasar los siguientes parámetros:

   * Ruta de acceso donde se creará la carpeta.
   * El `ResourceCollection` que representa la carpeta.
   * Aprobado `null` para los otros dos parámetros.

**Consulte también**

[Creación de carpetas](aem-forms-repository.md#creating-folders)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Recursos de escritura {#writing-resources}

Puede crear recursos en una ubicación determinada del repositorio. El tamaño natural del archivo está sujeto a las limitaciones de la base de datos y al tiempo de espera de la sesión. Para la configuración predeterminada, los archivos están limitados a 25 MB. Para aumentar o reducir el tamaño máximo de archivo, debe cambiar la configuración de la base de datos.

Escribir recursos equivale a almacenar datos en el repositorio. Una vez que escriba un recurso en el repositorio, todos los clientes del ecosistema del repositorio podrán acceder a él. Al escribir recursos, como esquemas XML, archivos XDP y archivos XSD, en el repositorio, el contenido se analiza en función del tipo MIME. Si se admite el tipo MIME, el analizador determina si hay una relación implícita con otro contenido. Por ejemplo, si una hoja de estilos en cascada (CSS) tiene una dirección URL relativa que hace referencia a un CSS común, se espera que también envíe el CSS común al repositorio. La relación entre los dos recursos se almacena como una relación pendiente durante un periodo no ajustable de 30 días. Cuando envía el CSS común al repositorio en el periodo de 30 días, se forma la relación.

Al crear un recurso, la lista de control de acceso (ACL) se hereda de la carpeta principal. La carpeta raíz tiene permisos de nivel del sistema hasta que se crea un recurso o una carpeta inicial, momento en el que el recurso o la carpeta recibe los permisos ACL predeterminados.

Puede escribir recursos mediante programación utilizando la API de Java del servicio de repositorio o la API del servicio web.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para escribir un recurso, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de Repositorio.
1. Especifique el URI del recurso que se va a leer.
1. Lea el recurso.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Creación del cliente de servicios**

Para poder leer un recurso mediante programación, debe establecer una conexión y proporcionar credenciales. Esto se logra creando un cliente de servicio.

**Especifique el URI de la carpeta de destino del recurso**

Cree una cadena que contenga el URI del recurso que se va a leer. La sintaxis incluye barras diagonales, como en este ejemplo: &quot;/*ruta*/*carpeta*&quot;.

**Creación del recurso**

Invoque el método del servicio del repositorio para crear el recurso y rellénelo con información de identificación, incluido su UUID, el nombre del recurso y la descripción.

**Especificar el contenido del recurso**

Invoque el método del servicio Repositorio para crear contenido de recursos y almacenarlo en el recurso.

**Escribir el recurso en la carpeta de destino**

Invoque el método del servicio del repositorio para escribir el recurso, especificando el URI de la carpeta de destino.

**Consulte también**

[Escribir recursos mediante la API de Java](aem-forms-repository.md#write-resources-using-the-java-api)

[Escribir recursos mediante la API de servicio web](aem-forms-repository.md#write-resources-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de repositorio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Escribir recursos mediante la API de Java {#write-resources-using-the-java-api}

Escriba un recurso mediante la API de servicio de repositorio (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clase del proyecto Java.

1. Creación del cliente de servicios

   Crear un `ResourceRepositoryClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. Especifique el URI de la carpeta de destino del recurso

   Especifique el URI de la carpeta de destino del recurso. En este caso, debido a que el recurso denominado `testResource` se almacenarán en la carpeta denominada `testFolder`, el URI de la carpeta es `"/testFolder"`. El URI se almacena como `java.lang.String` objeto.

1. Creación del recurso

   Para crear un recurso, primero debe crear un `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` objeto.

   Invoque el `RepositoryInfomodelFactoryBean` del objeto `newResource` , que crea un `com.adobe.repository.infomodel.bean.Resource` objeto. En este ejemplo, se proporcionan los siguientes parámetros:

   * A `com.adobe.repository.infomodel.Id` , que se crea invocando el constructor predeterminado para el objeto `Id` clase.
   * A `com.adobe.repository.infomodel.Lid` , que se crea invocando el constructor predeterminado para el objeto `Lid` clase.
   * A `java.lang.String` que contiene el nombre de archivo del recurso.

   Para especificar la descripción del recurso, invoque el `Resource` del objeto `setDescription` y pase una cadena que contenga la descripción. En este ejemplo, la descripción es `"test resource"`.

1. Especificar el contenido del recurso

   Para crear contenido para el recurso, invoque el `RepositoryInfomodelFactoryBean` del objeto `newResourceContent` método, que devuelve un valor `com.adobe.repository.infomodel.bean.ResourceContent` objeto. Añadir contenido a `ResourceContent` objeto. En este ejemplo, esto se logra haciendo las siguientes tareas:

   * Invocando el `ResourceContent` del objeto `setDataDocument` método y pasar un `com.adobe.idp.Document` objeto
   * Invocando el `ResourceContent` del objeto `setSize` y pasando el tamaño en bytes del método `Document` objeto

   Añada el contenido al recurso invocando el `Resource` del objeto `setContent` método y pasando el `ResourceContent` objeto. Para obtener más información, consulte [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Escribir el recurso en la carpeta de destino

   Invoque el `ResourceRepositoryClient` del objeto `writeResource` y pasan el URI de la carpeta, y el `Resource` objeto.

**Consulte también**

[Recursos de escritura](aem-forms-repository.md#writing-resources)

[SOAP Inicio rápido (modo de): Escritura de un recurso mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Escribir recursos mediante la API de servicio web {#write-resources-using-the-web-service-api}

Escribir un recurso mediante la API del servicio de repositorio (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL del repositorio utilizando base64.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Creación del cliente de servicios

   Mediante el ensamblado de cliente de Microsoft .NET, cree un `RepositoryServiceService` invocando su constructor predeterminado. Establezca su `Credentials` propiedad con un `System.Net.NetworkCredential` que contiene el nombre de usuario y la contraseña.

1. Especifique el URI de la carpeta de destino del recurso

   Especifique el URI de la carpeta de destino del recurso. En este caso, debido a que el recurso denominado `testResource` se almacenarán en la carpeta denominada `testFolder`, el URI de la carpeta es `"/testFolder"`. Cuando utilice un lenguaje compatible con Microsoft .NET Framework (por ejemplo, C#), almacene el URI en una `System.String` objeto.

1. Creación del recurso

   Para crear un recurso, invoque el constructor predeterminado para `Resource` clase. En este ejemplo, la siguiente información se almacena en el `Resource` objeto:

   * A `com.adobe.repository.infomodel.Id` , que se crea invocando el constructor predeterminado para el objeto `Id` y se asigna a la `Resource` del objeto `id` field.
   * A `com.adobe.repository.infomodel.Lid` , que se crea invocando el constructor predeterminado para el objeto `Lid` y se asigna a la `Resource` del objeto `lid` field.
   * Cadena que contiene el nombre de archivo del recurso, que se asigna al `Resource` del objeto `name` field. El nombre utilizado en este ejemplo es `"testResource"`.
   * Cadena que contiene la descripción del recurso, que se asigna al `Resource` del objeto `description` field. La descripción utilizada en este ejemplo es `"test resource"`.

1. Especificar el contenido del recurso

   Para crear contenido para el recurso, invoque el constructor predeterminado para `ResourceContent` clase. A continuación, añada contenido a `ResourceContent` objeto. En este ejemplo, esto se logra haciendo las siguientes tareas:

   * Asignación de un `BLOB` objeto que contiene un documento para `ResourceContent` del objeto `dataDocument` field.
   * Asignación del tamaño en bytes del `BLOB` objeto a `ResourceContent` del objeto `size` field.

   Añada el contenido al recurso asignando el `ResourceContent` objeto a `Resource` del objeto `content` field.

1. Escribir el recurso en la carpeta de destino

   Invoque el `RepositoryServiceService` del objeto `writeResource` y pasan el URI de la carpeta, y el `Resource` objeto. Aprobado `null` para los otros dos parámetros.

**Consulte también**

[Recursos de escritura](aem-forms-repository.md#writing-resources)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Listando recursos {#listing-resources}

Puede descubrir recursos enumerando los recursos. Se realiza una consulta en el repositorio para buscar todos los recursos relacionados con una colección de recursos determinada.

Una vez organizados los recursos, puede inspeccionar la estructura creada viendo una rama concreta de la estructura, como lo haría en un sistema operativo.

La lista de recursos funciona por relación: los recursos son miembros de carpetas. La pertenencia se representa mediante una relación de tipo &quot;miembro de&quot;. Cuando se enumeran recursos en una carpeta determinada, se están consultando recursos relacionados con una carpeta determinada mediante la relación &quot;miembro de&quot;. Las relaciones son direccionales: un miembro de una relación tiene un origen que es miembro del destino. El origen es el recurso, el destino es la carpeta principal.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para enumerar los recursos, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree el cliente de servicios.
1. Especifique la ruta de la carpeta.
1. Recupere la lista de recursos.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Creación del cliente de servicios**

Para poder crear mediante programación una colección de recursos, debe establecer una conexión y proporcionar credenciales. Esto se logra creando un cliente de servicio.

**Especificar la ruta de la carpeta**

Cree una cadena que contenga la ruta de la carpeta que contiene los recursos. La sintaxis incluye barras diagonales, como en este ejemplo: &quot;/*ruta*/*carpeta*&quot;.

**Recuperación de la lista de recursos**

Invoque el método del servicio Repositorio para recuperar la lista de recursos, especificando la ruta de la carpeta de destino.

**Consulte también**

[Enumeración de recursos mediante la API de Java](aem-forms-repository.md#list-resources-using-the-java-api)

[Enumerar recursos mediante la API de servicio web](aem-forms-repository.md#list-resources-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de repositorio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Enumeración de recursos mediante la API de Java {#list-resources-using-the-java-api}

Enumerar recursos mediante la API de servicio de repositorio (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clase del proyecto Java.

1. Creación del cliente de servicios

   Crear un `ResourceRepositoryClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. Especificar la ruta de la carpeta

   Especifique el URI de la colección de recursos que desea consultar. En este caso, su URI es `"/testFolder"`. El URI se almacena como `java.lang.String` objeto.

1. Recuperación de la lista de recursos

   Invoque el `ResourceRepositoryClient` del objeto `listMembers` y pase el URI de la carpeta.

   El método devuelve un valor `java.util.List` de `com.adobe.repository.infomodel.bean.Resource` objetos que son el origen de un objeto `com.adobe.repository.infomodel.bean.Relation` de tipo `Relation.TYPE_MEMBER_OF` y tienen como destino el URI de la colección de recursos. Puede iterar a través de esto `List` para recuperar cada uno de los recursos. En este ejemplo, se muestra el nombre y la descripción de cada recurso.

**Consulte también**

[Listando recursos](aem-forms-repository.md#listing-resources).

[SOAP Inicio rápido (modo de): Enumeración de recursos mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Enumerar recursos mediante la API de servicio web {#list-resources-using-the-web-service-api}

Enumerar recursos mediante la API del servicio de repositorio (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL del repositorio.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Creación del cliente de servicios

   Mediante el ensamblado de cliente de Microsoft .NET, cree un `RepositoryServiceService` invocando su constructor predeterminado. Establezca su `Credentials` propiedad con un `System.Net.NetworkCredential` que contiene el nombre de usuario y la contraseña.

1. Especificar la ruta de la carpeta

   Especifique una cadena que contenga el URI de la carpeta que se va a consultar. En este caso, su URI es `"/testFolder"`. Cuando utilice un lenguaje compatible con Microsoft .NET Framework (por ejemplo, C#), almacene el URI en una `System.String` objeto.

1. Recuperación de la lista de recursos

   Invoque el `RepositoryServiceService` del objeto `listMembers` y pase el URI de la carpeta como primer parámetro. Aprobado `null` para los otros dos parámetros.

   El método devuelve una matriz de objetos a los que se puede convertir `Resource` objetos. Puede iterar a través de la matriz de objetos para recuperar cada uno de los recursos relacionados. En este ejemplo, se muestra el nombre y la descripción de cada recurso.

**Consulte también**

[Listando recursos](aem-forms-repository.md#listing-resources).

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Leyendo recursos {#reading-resources}

Puede recuperar recursos de una ubicación determinada del repositorio para leer su contenido y metadatos. El flujo de trabajo está front-end mediante un formulario de inicialización. El proceso tiene todos los permisos necesarios para leer el formulario. El sistema recupera el formulario de datos y lee el contenido del repositorio. El repositorio concede acceso al contenido y a los metadatos (la capacidad de saber si existe el recurso).

El repositorio tiene los siguientes cuatro tipos de permisos:

* **recorrer**: permite enumerar recursos; es decir, leer metadatos de recursos, pero no contenido de recursos
* **leer**: permite leer el contenido del recurso
* **escribir**: permite escribir contenido de recursos
* **administración de listas de control de acceso (ACL)**: permite manipular las ACL en los recursos

Los usuarios solo pueden ejecutar procesos cuando tienen permiso para ejecutar el proceso. Los usuarios del IDE necesitan permisos de recorrido y lectura para sincronizarse con el repositorio. Las ACL se aplican solo en tiempo de diseño porque el tiempo de ejecución se produce dentro del contexto del sistema.

Puede leer recursos mediante programación utilizando la API de Java del servicio de repositorio o la API del servicio web.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-3}

Para leer un recurso, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de Repositorio.
1. Especifique el URI del recurso que se va a leer.
1. Lea el recurso.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Creación del cliente de servicios**

Para poder leer un recurso mediante programación, debe establecer una conexión y proporcionar credenciales. Esto se logra creando un cliente de servicio.

**Especifique el URI del recurso que desea leer**

Cree una cadena que contenga el URI del recurso que se va a leer. La sintaxis incluye barras diagonales, como en este ejemplo: &quot;/*ruta*/*resource*&quot;.

**Leer el recurso**

Invoque el método del servicio del repositorio para leer el recurso y especificar el URI.

**Consulte también**

[Leer recursos mediante la API de Java](aem-forms-repository.md#read-resources-using-the-java-api)

[Lectura de recursos mediante la API de servicio web](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de repositorio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Leer recursos mediante la API de Java {#read-resources-using-the-java-api}

Leer un recurso mediante la API de servicio de repositorio (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clase del proyecto Java.

1. Creación del cliente de servicios

   Crear un `ResourceRepositoryClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. Especifique el URI del recurso que desea leer

   Especifique un valor de cadena que represente el URI del recurso que se va a recuperar. Por ejemplo, suponiendo que el recurso se llame *testResource* que se encuentra en una carpeta denominada *testFolder*, especifique `/testFolder/testResource`.

1. Leer el recurso

   Invoque el `ResourceRepositoryClient` del objeto `readResource` y pase el URI del recurso como parámetro. Este método devuelve un `Resource` instancia que representa el recurso.

**Consulte también**

[Leyendo recursos](aem-forms-repository.md#reading-resources)

[SOAP Inicio rápido (modo de): Lectura de un recurso mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Lectura de recursos mediante la API de servicio web {#reading-resources-using-the-web-service-api}

Leer un recurso mediante la API del servicio de repositorio (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL del repositorio. (Consulte [Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)
   * Hacer referencia al ensamblado de cliente de Microsoft .NET. (Consulte [Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Creación del cliente de servicios

   Mediante el ensamblado de cliente de Microsoft .NET, cree un `RepositoryServiceService` invocando su constructor predeterminado. Establezca su `Credentials` propiedad con un `System.Net.NetworkCredential` que contiene el nombre de usuario y la contraseña.

1. Especifique el URI del recurso que desea leer

   Especifique una cadena que contenga el URI del recurso que se va a recuperar. En este caso, debido a que el recurso denominado `testResource` se encuentra en la carpeta denominada `testFolder`, su URI es `"/testFolder/testResource"`. Cuando utilice un lenguaje compatible con Microsoft .NET Framework (por ejemplo, C#), almacene el URI en una `System.String` objeto.

1. Leer el recurso

   Invoque el `RepositoryServiceService` del objeto `readResource` y pase el URI del recurso como el primer parámetro. Aprobado `null` para los otros dos parámetros.

**Consulte también**

[Leyendo recursos](aem-forms-repository.md#reading-resources)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Actualización de recursos {#updating-resources}

Puede recuperar y actualizar el contenido de los recursos del repositorio. Al actualizar los recursos, el control de acceso a esos recursos permanece sin cambios entre las versiones. Al realizar una actualización, tiene la opción de incrementar la versión principal. Si no incrementa la versión principal, la versión secundaria se actualiza automáticamente.

Al actualizar un recurso, se crea la nueva versión en función de los atributos de recurso especificados. Al actualizar un recurso, se especifican dos parámetros importantes: el URI de destino y una instancia de recurso que contiene todos los metadatos actualizados. Es importante tener en cuenta que si no está cambiando un atributo determinado (por ejemplo, el nombre), el atributo sigue siendo necesario en la instancia que transfiere. Las relaciones que se crean al analizar el contenido se añaden a la versión específica y no se reenvían a menos que se especifique lo contrario.

Por ejemplo, si actualiza un archivo XDP y contiene referencias a otros recursos, también se registrarán esas referencias adicionales. Supongamos que form.xdp versión 1.0 tiene dos referencias externas: un logotipo y una hoja de estilo y, a continuación, actualice form.xdp para que ahora tenga tres referencias: un logotipo, una hoja de estilo y un archivo de esquema. Durante la actualización, el repositorio añadirá la tercera relación (al archivo de esquema) a su tabla de relaciones pendiente. Una vez que el archivo de esquema esté presente en el repositorio, la relación se formará automáticamente. Sin embargo, si la versión 2.0 de form.xdp ya no utiliza el logotipo, la versión 2.0 de form.xdp no tendrá relación con él.

Todas las operaciones de actualización son atómicas y transaccionales. Por ejemplo, si dos usuarios leen el mismo recurso y ambos deciden actualizar la versión 1.0 a la 2.0, uno de ellos se realizará correctamente y uno de ellos fallará, la integridad del repositorio se mantendrá y ambos recibirán un mensaje que confirme el éxito o el error. Si la transacción no se confirma, se revertirá si se produce un error en la base de datos y se agotará el tiempo de espera o se revertirá según el servidor de aplicaciones.

Puede actualizar los recursos mediante programación utilizando la API de Java del servicio de repositorio o la API del servicio web.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-4}

Para actualizar un recurso, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de Repositorio.
1. Recupere el recurso que desea actualizar.
1. Actualice el recurso.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Creación del cliente de servicios**

Para poder leer un recurso mediante programación, debe establecer una conexión y proporcionar credenciales. Esto se logra creando un cliente de servicio.

**Recupere el recurso que desea actualizar**

Lea el recurso. Para obtener más información, consulte [Leyendo recursos](aem-forms-repository.md#reading-resources).

**Actualizar el recurso**

Establezca la nueva información en el recurso e invoque el método del servicio del repositorio para actualizar el recurso, especificando el URI, el recurso actualizado y cómo se debe actualizar la información de la versión.

**Consulte también**

[Actualización de recursos mediante la API de Java](aem-forms-repository.md#update-resources-using-the-java-api)

[Actualización de recursos mediante la API de servicio web](aem-forms-repository.md#update-resources-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de repositorio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Actualización de recursos mediante la API de Java {#update-resources-using-the-java-api}

Actualizar un recurso mediante la API de servicio de repositorio (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clase del proyecto Java.

1. Creación del cliente de servicios

   Crear un `ResourceRepositoryClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. Recupere el recurso que desea actualizar

   Especifique el URI del recurso para recuperar y leer el recurso. En este ejemplo, el URI del recurso es `"/testFolder/testResource"`.

1. Actualizar el recurso

   Actualice el `Resource` información del objeto. En este ejemplo, para actualizar la descripción, invoque el `Resource` del objeto `setDescription` y pasar la nueva cadena de descripción como parámetro.

   A continuación, invoque el `ServiceClientFactory` del objeto `updateResource` y pase los siguientes parámetros:

   * A `java.lang.String` que contiene el URI del recurso.
   * El `Resource` que contiene la información actualizada del recurso.
   * A `boolean` valor que indica si se actualiza la versión principal o secundaria. En este ejemplo, un valor de `true` se pasa para indicar que la versión principal se va a incrementar.

**Consulte también**

[Actualización de recursos](aem-forms-repository.md#updating-resources)

[SOAP Inicio rápido (modo de): Actualización de un recurso mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Actualización de recursos mediante la API de servicio web {#update-resources-using-the-web-service-api}

Actualizar un recurso mediante la API del repositorio (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL del repositorio.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Creación del cliente de servicios

   Mediante el ensamblado de cliente de Microsoft .NET, cree un `RepositoryServiceService` invocando su constructor predeterminado. Establezca su `Credentials` propiedad con un `System.Net.NetworkCredential` que contiene el nombre de usuario y la contraseña.

1. Recupere el recurso que desea actualizar

   Especifique el URI del recurso que se va a recuperar y lea el recurso. En este ejemplo, el URI del recurso es `"/testFolder/testResource"`. Para obtener más información, consulte [Leyendo recursos](aem-forms-repository.md#reading-resources).

1. Actualizar el recurso

   Actualice el `Resource` información del objeto. En este ejemplo, para actualizar la descripción, asigne un nuevo valor al `Resource` del objeto `description` field.

1. Invoque el `RepositoryServiceService` del objeto `updateResource` y pase los siguientes parámetros:

   * A `System.String` que contiene el URI del recurso.
   * El `Resource` que contiene la información actualizada del recurso.
   * A `boolean` valor que indica si se actualiza la versión principal o secundaria. En este ejemplo, un valor de `true` se pasa para indicar que la versión principal se va a incrementar.
   * Aprobado `null` para los dos parámetros restantes.

**Consulte también**

[Actualización de recursos](aem-forms-repository.md#updating-resources)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Búsqueda de recursos {#searching-for-resources}

Puede construir consultas utilizadas para buscar recursos en el repositorio, incluido el historial, los recursos relacionados y las propiedades.

Puede recuperar recursos relacionados para determinar las dependencias entre un formulario y sus fragmentos. Por ejemplo, si tiene un formulario, puede determinar qué fragmentos o recursos externos utiliza. Si tiene una imagen, también puede averiguar qué formularios utilizan la imagen. También puede buscar recursos relacionados utilizando el filtrado basado en propiedades. Por ejemplo, puede buscar todos los formularios que utilizan una imagen con un nombre especificado o cualquier imagen utilizada por un formulario con un nombre especificado. También puede buscar utilizando las propiedades del recurso. Por ejemplo, puede realizar una consulta para buscar todos los formularios o recursos cuyo nombre comience por una cadena determinada que puede incluir caracteres comodín &quot;%&quot; y &quot;_&quot;. Recuerde que las búsquedas basadas en propiedades no se basan en relaciones; dichas búsquedas se basan en la suposición de que tiene conocimientos específicos sobre un recurso determinado.

**Instrucciones de consulta**

A *query* contiene una o más instrucciones unidas lógicamente con condiciones. A *declaración* consta de un operando izquierdo, un operador y un operando derecho. Además, puede especificar el criterio de ordenación que se utilizará para los resultados de búsqueda. El *criterio de ordenación* contiene información equivalente a un SQL `ORDER BY` y se compone de elementos que contienen los atributos en los que se basó la búsqueda y un valor que indica si se va a utilizar en orden ascendente o descendente.

Puede buscar recursos mediante programación utilizando la API de Java del servicio de repositorio. En este momento, no es posible utilizar la API del servicio web para buscar recursos.

**Comportamiento de ordenación**

No se respeta el orden al invocar el `ResourceRepositoryClient` del objeto `searchProperties` y especificando un criterio de ordenación. Por ejemplo, suponga que crea un recurso con tres propiedades personalizadas, donde los nombres de atributo son `name`, `secondName`, y `asecondName`. A continuación, cree un elemento de criterio de ordenación en el nombre de atributo y establezca el `ascending` valor hasta `true`.

A continuación, invoque la variable `ResourceRepositoryClient` del objeto `searchProperties` y pasar el criterio de ordenación. La búsqueda devuelve el recurso correcto, con las tres propiedades. Sin embargo, las propiedades no se ordenan por nombre de atributo. Se devuelven en el orden en que se agregaron: `name`, `secondName`, y `asecondName`.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-5}

Para buscar recursos, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de Repositorio.
1. Especifique la carpeta de destino para la búsqueda.
1. Especifique los atributos utilizados en la búsqueda.
1. Cree la consulta utilizada en la búsqueda.
1. Cree el criterio de ordenación para los resultados de búsqueda.
1. Busque los recursos.
1. Recupere los recursos del resultado de la búsqueda.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Creación del cliente de servicios**

Para poder leer un recurso mediante programación, debe establecer una conexión y proporcionar credenciales. Esto se logra creando un cliente de servicio.

**Especifique la carpeta de destino para la búsqueda**

Cree una cadena que contenga la ruta base desde la que realizar la búsqueda. La sintaxis incluye barras diagonales, como en este ejemplo: &quot;/*ruta*/*carpeta*&quot;.

**Especifique los atributos utilizados en la búsqueda**

Puede basar la búsqueda en los atributos contenidos en los recursos. Especifique los valores de los atributos en los que desea realizar la búsqueda.

**Cree la consulta utilizada en la búsqueda**

Construya una consulta utilizando instrucciones y condiciones. Cada instrucción especifica el atributo en el que se basará la búsqueda, la condición que se utilizará y el valor del atributo que se utilizará en la búsqueda.

**Crear el criterio de ordenación para los resultados de búsqueda**

El criterio de ordenación consta de elementos, cada uno de los cuales contiene uno de los atributos utilizados en la búsqueda y un valor que indica si se va a utilizar en orden ascendente o descendente.

**Búsqueda de los recursos**

Busque los recursos mediante la carpeta, la consulta y el criterio de ordenación. Además, indique la profundidad de la búsqueda y un límite superior en el número de resultados que se van a devolver.

**Recuperación de los recursos del resultado de la búsqueda**

Itere por la lista devuelta de recursos y extraiga la información para un procesamiento posterior.

**Consulte también**

[Búsqueda de recursos mediante la API de Java](aem-forms-repository.md#search-for-resources-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de repositorio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Búsqueda de recursos mediante la API de Java {#search-for-resources-using-the-java-api}

Busque un recurso mediante la API de servicio de repositorio (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clase del proyecto Java.

1. Creación del cliente de servicios

   Crear un `ResourceRepositoryClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. Especifique la carpeta de destino para la búsqueda

   Especifique el URI de la ruta base desde la que se ejecutará la búsqueda. En este ejemplo, el URI del recurso es `/testFolder`.

1. Especifique los atributos utilizados en la búsqueda

   Especifique los valores de los atributos en los que desea realizar la búsqueda. Los atributos existen dentro de un `com.adobe.repository.infomodel.bean.Resource` objeto. En este ejemplo, la búsqueda se realizará en el atributo name; por lo tanto, un `java.lang.String` que contiene el `Resource` se utiliza el nombre del objeto, que es `testResource` en este caso.

1. Cree la consulta utilizada en la búsqueda

   Para crear una consulta, cree un `com.adobe.repository.query.Query` invocando el constructor predeterminado para el objeto `Query` y agregue instrucciones a la consulta.

   Para crear una instrucción, invoque el constructor de la instrucción `com.adobe.repository.query.Query.Statement` y pasar los siguientes parámetros:

   * Operando izquierdo que contiene la constante de atributo de recurso. En este ejemplo, como el nombre del recurso se utiliza como base para la búsqueda, el valor estático `Resource.ATTRIBUTE_NAME` se utiliza.
   * Operador que contiene la condición utilizada en la búsqueda del atributo. El operador debe ser una de las constantes estáticas de `Query.Statement` clase. En este ejemplo, el valor estático `Query.Statement.OPERATOR_BEGINS_WITH` se utiliza.
   * Operando derecho que contiene el valor del atributo en el que se va a realizar la búsqueda. En este ejemplo, el atributo name, un `String` que contiene el valor `"testResource"`, se utiliza.

   Especifique el área de nombres del operando izquierdo invocando el `Query.Statement` del objeto `setNamespace` y pasando uno de los valores estáticos contenidos en la variable `com.adobe.repository.infomodel.bean.ResourceProperty` clase. En este ejemplo, se utiliza `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY`.

   Agregue cada instrucción a la consulta invocando el método `Query` del objeto `addStatement` método y pasando el `Query.Statement` objeto.

1. Crear el criterio de ordenación para los resultados de búsqueda

   Para especificar el criterio de ordenación utilizado en los resultados de búsqueda, cree un `com.adobe.repository.query.sort.SortOrder` invocando el constructor predeterminado para el objeto `SortOrder` y agregue elementos al criterio de ordenación.

   Para crear un elemento para el criterio de ordenación, invoque uno de los constructores para `com.adobe.repository.query.sort.SortOrder.Element` clase. En este ejemplo, como el nombre del recurso se utiliza como base para la búsqueda, el valor estático `Resource.ATTRIBUTE_NAME` se utiliza como primer parámetro y en orden ascendente (a) `boolean` valor de `true`) se especifica como segundo parámetro.

   Agregue cada elemento al criterio de ordenación invocando la variable `SortOrder` del objeto `addSortElement` método y pasando el `SortOrder.Element` objeto.

1. Búsqueda de los recursos

   Para buscar `resources` en función de las propiedades del atributo, invoque el `ResourceRepositoryClient` del objeto `searchProperties` y pasar los siguientes parámetros:

   * A `String` que contiene la ruta base desde la que ejecutar la búsqueda. En este caso, `"/testFolder"` se utiliza.
   * La consulta utilizada en la búsqueda.
   * Profundidad de la búsqueda. En este caso, `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` se utiliza para indicar que se van a utilizar la ruta base y todas sus carpetas.
   * Un `int` valor que indica la primera fila desde la que se selecciona el conjunto de resultados no paginado. En este ejemplo, `0` se ha especificado.
   * Un `int` valor que indica el número máximo de resultados que se van a devolver. En este ejemplo, `10` se ha especificado.
   * Orden utilizado en la búsqueda.

   El método devuelve un valor `java.util.List` de `Resource` en el orden especificado.

1. Recuperación de los recursos del resultado de la búsqueda

   Para recuperar los recursos contenidos en el resultado de búsqueda, itere a través de la variable `List` y convierta cada objeto en una `Resource` para extraer su información. En este ejemplo, se muestra el nombre de cada recurso.

**Consulte también**

[Búsqueda de recursos](aem-forms-repository.md#searching-for-resources)

[SOAP Inicio rápido (modo de): Búsqueda de recursos mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Creación de relaciones de recursos {#creating-resource-relationships}

Puede especificar relaciones entre recursos en el repositorio. Existen tres tipos de relaciones:

* **Dependencia**: una relación en la que un recurso depende de otros recursos, lo que significa que todos los recursos relacionados son necesarios en el repositorio.
* **Suscripción (sistema de archivos)**: una relación en la que un recurso se encuentra dentro de una carpeta determinada.
* **Personalizado**: una relación que especifique entre los recursos. Por ejemplo, si un recurso ha quedado obsoleto y otro introducido en el repositorio, puede especificar su propia relación de sustitución.

Puede crear sus propias relaciones personalizadas. Por ejemplo, si almacena un archivo de HTML en el repositorio y utiliza una imagen, puede especificar una relación personalizada para relacionar el archivo de HTML con la imagen (ya que normalmente solo los archivos XML están asociados a imágenes mediante una relación de dependencia definida en el repositorio). Otro ejemplo de relación personalizada sería si desea crear una vista diferente del repositorio con una estructura de gráficos cíclica en lugar de una estructura de árbol. Puede definir un gráfico circular junto con un visor para recorrer esas relaciones. Por último, puede indicar que un recurso reemplaza a otro aunque los dos recursos sean completamente diferentes. En ese caso, puede definir un tipo de relación fuera del intervalo reservado y crear una relación entre esos dos recursos. Su aplicación sería el único cliente que podría detectar y procesar la relación y se podría utilizar para realizar búsquedas sobre esa relación.

Puede especificar mediante programación relaciones entre recursos mediante la API de Java del servicio de repositorio o la API del servicio web.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-6}

Para especificar una relación entre dos recursos, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de Repositorio.
1. Especifique los URI de los recursos que se van a relacionar.
1. Cree la relación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Creación del cliente de servicios**

Para poder leer un recurso mediante programación, debe establecer una conexión y proporcionar credenciales. Esto se logra creando un cliente de servicio.

**Especifique los URI de los recursos que se van a relacionar**

Cree cadenas que contengan los URI del recurso que desea relacionar. La sintaxis incluye barras diagonales, como en este ejemplo: &quot;/*ruta*/*resource*&quot;.

**Creación de la relación**

Invoque el método de servicio Repositorio para crear y especificar el tipo de relación.

**Consulte también**

[Creación de recursos de relación mediante la API de Java](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[Creación de recursos de relación mediante la API de servicio web](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de repositorio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Creación de recursos de relación mediante la API de Java {#create-relationship-resources-using-the-java-api}

Cree recursos de relación mediante la API de Java del servicio de repositorio y realice las siguientes tareas:

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clase del proyecto Java.

1. Creación del cliente de servicios

   Crear un `ResourceRepositoryClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. Especifique los URI de los recursos que se van a relacionar

   Especifique los URI de los recursos que se van a relacionar. En este caso, debido a que los recursos se denominan `testResource1` y `testResource2` y se encuentran en la carpeta denominada `testFolder`, sus URI son `"/testFolder/testResource1"` y `"/testFolder/testResource2"`. Los URI se almacenan como `java.lang.String` objetos. En este ejemplo, los recursos se escriben primero en el repositorio y se recuperan sus URI. Para obtener más información sobre cómo escribir un recurso, consulte [Recursos de escritura](aem-forms-repository.md#writing-resources).

1. Creación de la relación

   Invoque el `ResourceRepositoryClient` del objeto `createRelationship` y pasar los siguientes parámetros:

   * URI del recurso de origen.
   * URI del recurso de destino.
   * El tipo de relación, que es una de las constantes estáticas de `com.adobe.repository.infomodel.bean.Relation` clase. En este ejemplo, se establece una relación de dependencia especificando el valor `Relation.TYPE_DEPENDANT_OF`.
   * A `boolean` valor que indica si el recurso de destino se actualiza automáticamente al `com.adobe.repository.infomodel.Id`Identificador basado en del nuevo recurso de encabezado. En este ejemplo, debido a la relación de dependencia, el valor `true` se ha especificado.

   También puede recuperar una lista de recursos relacionados para un recurso determinado invocando el método `ResourceRepositoryClient` del objeto `getRelated` y pasando los siguientes parámetros:

   * URI del recurso para el que se recuperan los recursos relacionados. En este ejemplo, el recurso de origen ( `"/testFolder/testResource1"`) se ha especificado.
   * A `boolean` valor que indica si el recurso especificado es el recurso de origen en la relación. En este ejemplo, el valor `true` se especifica porque este es el caso.
   * El tipo de relación, que es una de las constantes estáticas de `Relation` clase. En este ejemplo, se especifica una relación de dependencia utilizando el mismo valor utilizado anteriormente: `Relation.TYPE_DEPENDANT_OF`.

   El `getRelated` El método devuelve un valor `java.util.List` de `Resource` objetos a través de los cuales se puede iterar para recuperar cada uno de los recursos relacionados, convirtiendo los objetos contenidos en el `List` hasta `Resource` mientras lo hace. En este ejemplo, `testResource2` se espera que esté en la lista de recursos devueltos.

**Consulte también**

[Creación de relaciones de recursos](aem-forms-repository.md#creating-resource-relationships)

[SOAP Inicio rápido (modo de): Creación de relaciones entre recursos mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creación de recursos de relación mediante la API de servicio web {#create-relationship-resources-using-the-web-service-api}

Cree recursos de relación mediante la API del repositorio (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL del repositorio.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Creación del cliente de servicios

   Mediante el ensamblado de cliente de Microsoft .NET, cree un `RepositoryServiceService` invocando su constructor predeterminado. Establezca su `Credentials` propiedad con un `System.Net.NetworkCredential` que contiene el nombre de usuario y la contraseña.

1. Especifique los URI de los recursos que se van a relacionar

   Especifique los URI de los recursos que se van a relacionar. En este caso, debido a que los recursos se denominan `testResource1` y `testResource2` y se encuentran en la carpeta denominada `testFolder`, sus URI son `"/testFolder/testResource1"` y `"/testFolder/testResource2"`. Cuando se utiliza un lenguaje compatible con Microsoft .NET Framework (por ejemplo, C#), los URI se almacenan como `System.String` objetos. En este ejemplo, los recursos se escriben primero en el repositorio y se recuperan sus URI. Para obtener más información sobre cómo escribir un recurso, consulte [Recursos de escritura](aem-forms-repository.md#writing-resources).

1. Creación de la relación

   Invoque el `RepositoryServiceService` del objeto `createRelationship` y pasar los siguientes parámetros:

   * URI del recurso de origen.
   * URI del recurso de destino.
   * El tipo de relación. En este ejemplo, se establece una relación de dependencia especificando el valor `3`.
   * A `boolean` valor que indica si se especificó el tipo de relación. En este ejemplo, el valor `true` se ha especificado.
   * A `boolean` valor que indica si el recurso de destino se actualiza automáticamente al `Id`Identificador basado en del nuevo recurso de encabezado. En este ejemplo, debido a la relación de dependencia, el valor `true` se ha especificado.
   * A `boolean` valor que indica si se especificó el encabezado de destinatario. En este ejemplo, el valor `true` se ha especificado.
   * Aprobado `null` para el último parámetro.

   También puede recuperar una lista de recursos relacionados para un recurso determinado invocando el método `RepositoryServiceService` del objeto `getRelated` y pasando los siguientes parámetros:

   * URI del recurso para el que se recuperan los recursos relacionados. En este ejemplo, el recurso de origen ( `"/testFolder/testResource1"`) se ha especificado.
   * A `boolean` valor que indica si el recurso especificado es el recurso de origen en la relación. En este ejemplo, el valor `true` se especifica porque este es el caso.
   * A `boolean` valor que indica si se especificó el recurso de origen. En este ejemplo, el valor `true` se proporciona.
   * Matriz de enteros que contiene los tipos de relación. En este ejemplo, se especifica una relación de dependencia utilizando el mismo valor en la matriz que se utilizó anteriormente: `3`.
   * Aprobado `null` para los dos parámetros restantes.

   El `getRelated` método devuelve una matriz de objetos a los que se puede convertir `Resource` objetos a través de los cuales se puede iterar para recuperar cada uno de los recursos relacionados. En este ejemplo, `testResource2` se espera que esté en la lista de recursos devueltos.

**Consulte también**

[Creación de relaciones de recursos](aem-forms-repository.md#creating-resource-relationships)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Bloqueo de recursos {#locking-resources}

Puede bloquear un recurso o un conjunto de recursos para su uso exclusivo por parte de un usuario en particular o para su uso compartido entre más de un usuario. Un bloqueo compartido es una indicación de que algo sucederá con el recurso, pero no impide que otra persona realice acciones con ese recurso. Un bloqueo compartido debe considerarse un mecanismo de señalización. Un bloqueo exclusivo significa que el usuario que bloqueó el recurso va a cambiar el recurso y el bloqueo garantiza que nadie más pueda hacerlo hasta que el usuario ya no necesite acceso al recurso y haya liberado el bloqueo. Si un administrador del repositorio desbloquea un recurso, todos los bloqueos exclusivos y compartidos de ese recurso se eliminarán automáticamente. Este tipo de acción está diseñado para situaciones en las que un usuario ya no está disponible y no ha desbloqueado el recurso.

Cuando un recurso está bloqueado, aparece un icono de bloqueo al ver la pestaña Recursos en Workbench, como se muestra en la siguiente ilustración.

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

Puede controlar mediante programación el acceso a los recursos mediante la API de Java del servicio de repositorio o la API del servicio web.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-7}

Para bloquear y desbloquear recursos, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de Repositorio.
1. Especifique el URI del recurso que se va a bloquear.
1. Bloquee el recurso.
1. Recupere los bloqueos del recurso.
1. Desbloquear el recurso

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Creación del cliente de servicios**

Para poder leer un recurso mediante programación, debe establecer una conexión y proporcionar credenciales. Esto se logra creando un cliente de servicio.

**Especifique el URI del recurso que desea bloquear**

Cree una cadena que contenga el URI del recurso que se va a bloquear. La sintaxis incluye barras diagonales, como en este ejemplo: &quot;/*ruta*/*resource*&quot;.

**Bloquear el recurso**

Invoque el método del servicio de repositorio para bloquear el recurso, especificando el URI, el tipo de bloqueo y la profundidad de bloqueo.

**Recuperar los bloqueos del recurso**

Invoque el método del Servicio de repositorio para recuperar los bloqueos del recurso y especificar el URI.

**Desbloquear el recurso**

Invoque el método del Servicio de repositorio para desbloquear el recurso y especificar el URI.

**Consulte también**

[Bloqueo de recursos mediante la API de Java](aem-forms-repository.md#lock-resources-using-the-java-api)

[Bloqueo de recursos mediante la API de servicio web](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de repositorio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Bloqueo de recursos mediante la API de Java {#lock-resources-using-the-java-api}

Bloqueo de recursos mediante la API de servicio de repositorio (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clase del proyecto Java.

1. Creación del cliente de servicios

   Crear un `ResourceRepositoryClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. Especifique el URI del recurso que desea bloquear

   Especifique el URI del recurso que se va a bloquear. En este caso, debido a que el recurso denominado `testResource` se encuentra en la carpeta denominada `testFolder`, su URI es `"/testFolder/testResource"`. El URI se almacena como `java.lang.String` objeto.

1. Bloquear el recurso

   Invoque el `ResourceRepositoryClient` del objeto `lockResource` y pasar los siguientes parámetros:

   * URI del recurso.
   * El ámbito de bloqueo. En este ejemplo, como el recurso estará bloqueado para uso exclusivo, el ámbito de bloqueo se especifica como `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`.
   * La profundidad del bloqueo. En este ejemplo, debido a que el bloqueo se aplicará sólo al recurso concreto y a ninguno de sus miembros o hijos, la profundidad de bloqueo se especifica como `Lock.DEPTH_ZERO`.

   >[!NOTE]
   >
   >La versión sobrecargada del `lockResource` que requiere cuatro parámetros y genera una excepción. Asegúrese de utilizar el `lockResource` que requiere tres parámetros, como se muestra en este tutorial.

1. Recuperar los bloqueos del recurso

   Invoque el `ResourceRepositoryClient` del objeto `getLocks` y pase el URI del recurso como parámetro. El método devuelve un objeto List of Lock a través del cual se puede iterar. En este ejemplo, el propietario, la profundidad y el ámbito del bloqueo se imprimen para cada objeto invocando el de cada objeto Lock `getOwnerUserId`, `getDepth`, y `getType` métodos, respectivamente.

1. Desbloquear el recurso

   Invoque el `ResourceRepositoryClient` del objeto `unlockResource` y pase el URI del recurso como parámetro. Para obtener más información, consulte la [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Consulte también**

[Bloqueo de recursos](aem-forms-repository.md#locking-resources)

[SOAP Inicio rápido (modo de): Bloqueo de un recurso mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Bloqueo de recursos mediante la API de servicio web {#lock-resources-using-the-web-service-api}

Bloqueo de recursos mediante la API del servicio de repositorio (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL del repositorio utilizando Base64.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Creación del cliente de servicios

   Mediante el ensamblado de cliente de Microsoft .NET, cree un `RepositoryServiceService` invocando su constructor predeterminado. Establezca su `Credentials` propiedad con un `System.Net.NetworkCredential` que contiene el nombre de usuario y la contraseña.

1. Especifique el URI del recurso que desea bloquear

   Especifique una cadena que contenga el URI del recurso que se va a bloquear. En este caso, debido a que el recurso denominado `testResource` está en la carpeta `testFolder`, su URI es `"/testFolder/testResource"`. Cuando utilice un lenguaje compatible con Microsoft .NET Framework (por ejemplo, C#), almacene el URI en una `System.String` objeto.

1. Bloquear el recurso

   Invoque el `RepositoryServiceService` del objeto `lockResource` y pasar los siguientes parámetros:

   * URI del recurso.
   * El ámbito de bloqueo. En este ejemplo, como el recurso estará bloqueado para uso exclusivo, el ámbito de bloqueo se especifica como `11`.
   * La profundidad del bloqueo. En este ejemplo, debido a que el bloqueo se aplicará sólo al recurso concreto y a ninguno de sus miembros o hijos, la profundidad de bloqueo se especifica como `2`.
   * Un `int` valor que indica el número de segundos hasta que caduca el bloqueo. En este ejemplo, el valor de `1000` se utiliza.
   * Aprobado `null` para el último parámetro.

1. Recuperar los bloqueos del recurso

   Invoque el `RepositoryServiceService` del objeto `getLocks` y pasan el URI del recurso como primer parámetro y `null` para el segundo parámetro. El método devuelve un valor `object` matriz que contiene `Lock` objetos a través de los cuales se puede iterar. En este ejemplo, el propietario del bloqueo, la profundidad y el ámbito se imprimen para cada objeto accediendo a cada uno `Lock` del objeto `ownerUserId`, `depth`, y `type` Campos, respectivamente.

1. Desbloquear el recurso

   Invoque el `RepositoryServiceService` del objeto `unlockResource` y pasan el URI del recurso como primer parámetro y `null` para el segundo parámetro.

**Consulte también**

[Bloqueo de recursos](aem-forms-repository.md#locking-resources)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Eliminación de recursos {#deleting-resources}

SOAP Puede eliminar recursos mediante programación de una ubicación determinada del repositorio mediante la API de Java del servicio de repositorio (API) de Java. ()

Cuando se elimina un recurso, la eliminación suele ser permanente, aunque en algunos casos los repositorios de ECM pueden almacenar las versiones del recurso según sus mecanismos de historial. Por lo tanto, al eliminar un recurso, es importante asegurarse de que nunca más necesitará ese recurso. Los motivos comunes para eliminar un recurso incluyen la necesidad de aumentar el espacio disponible en la base de datos. Puede eliminar una versión de un recurso, pero si lo hace debe especificar el identificador del recurso y no su identificador lógico (LID) o ruta de acceso. Si elimina una carpeta, se eliminará automáticamente todo el contenido de la misma, incluidas las subcarpetas y los recursos.

Los recursos relacionados no se eliminan. Por ejemplo, si tiene un formulario que utiliza el archivo logo.gif y elimina logo.gif, se almacenará una relación en la tabla de relaciones pendientes. Como alternativa, para la obsolescencia de la versión, establezca el estado de objeto de la última versión como obsoleto.

Una operación de eliminación no es segura para transacciones en sistemas ECM. Por ejemplo, si intenta eliminar 100 recursos y la operación falla en el recurso número 50, las primeras 49 instancias se eliminarán, pero el resto no. De lo contrario, el comportamiento predeterminado es rollback (sin compromiso).

>[!NOTE]
>
>Al usar el `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` método con el repositorio de ECM (EMC Documentum Content Server y IBM FileNet P8 Content Manager), la transacción no se revertirá si la eliminación falla en uno de los recursos especificados, lo que significa que los archivos que se han eliminado no se pueden deshacer.

>[!NOTE]
>
>Para obtener más información sobre el servicio Repositorio, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-8}

Para eliminar un recurso, siga estos pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de Repositorio.
1. Especifique el URI del recurso que se va a eliminar.
1. Elimine el recurso.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Creación del cliente de servicios**

Para poder leer un recurso mediante programación, debe establecer una conexión y proporcionar credenciales. Esto se logra creando un cliente de servicio.

**Especifique el URI del recurso que desea eliminar**

Cree una cadena que contenga el URI del recurso que se va a eliminar. La sintaxis incluye barras diagonales, como en este ejemplo: &quot;/*ruta*/*resource*&quot;. Si el recurso que se va a eliminar es una carpeta, la eliminación será recursiva.

**Eliminar el recurso**

Invoque el método del servicio del repositorio para eliminar el recurso y especifique el URI.

**Consulte también**

[Eliminación de recursos mediante la API de Java](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[Eliminación de recursos mediante la API de servicio web](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de repositorio](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### SOAP Eliminación de recursos mediante la API de Java (API) {#delete-resources-using-the-java-api-soap}

Elimine un recurso mediante la API del repositorio (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clase del proyecto Java.

1. Creación del cliente de servicios

   Crear un `ResourceRepositoryClient` mediante su constructor y pasando un objeto `ServiceClientFactory` que contiene las propiedades de conexión.

1. Especifique el URI del recurso que desea eliminar

   Especifique el URI del recurso que se va a recuperar. En este caso, como el recurso denominado testResourceToBeDeleted se encuentra en la carpeta denominada testFolder, su URI es `/testFolder/testResourceToBeDeleted`. El URI se almacena como `java.lang.String` objeto. En este ejemplo, el recurso se escribe primero en el repositorio y se recupera su URI. Para obtener más información sobre cómo escribir un recurso, consulte [Recursos de escritura](aem-forms-repository.md#writing-resources).

1. Eliminar el recurso

   Invoque el `ResourceRepositoryClient` del objeto `deleteResource` y pase el URI del recurso como parámetro.

**Consulte también**

[Eliminación de recursos](aem-forms-repository.md#deleting-resources)

[SOAP Inicio rápido (modo de): Búsqueda de recursos mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminación de recursos mediante la API de servicio web {#delete-resources-using-the-web-service-api}

Eliminar un recurso mediante la API del repositorio (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL del repositorio utilizando Base64.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Creación del cliente de servicios

   Mediante el ensamblado de cliente de Microsoft .NET, cree un `RepositoryServiceService` invocando su constructor predeterminado. Establezca su `Credentials` propiedad con un `System.Net.NetworkCredential` que contiene el nombre de usuario y la contraseña.

1. Especifique el URI del recurso que desea eliminar

   Especifique el URI del recurso que se va a recuperar. En este caso, debido a que el recurso denominado `testResourceToBeDeleted` se encuentra en la carpeta denominada `testFolder`, su URI es `"/testFolder/testResourceToBeDeleted"`. En este ejemplo, el recurso se escribe primero en el repositorio y se recupera su URI. Para obtener más información sobre cómo escribir un recurso, consulte [Recursos de escritura](aem-forms-repository.md#writing-resources).

1. Eliminar el recurso

   Invoque el `RepositoryServiceService` del objeto `deleteResources` método y pase un `System.String` matriz que contiene el URI del recurso como primer parámetro. Aprobado `null` para el segundo parámetro.

**Consulte también**

[Eliminación de recursos](aem-forms-repository.md#deleting-resources)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
