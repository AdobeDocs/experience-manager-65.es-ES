---
title: Cómo acceder mediante programación al JCR de AEM
seo-title: How to programmatically access the AEM JCR
description: Puede modificar mediante programación nodos y propiedades ubicados dentro del repositorio de AEM, que forma parte de Adobe Marketing Cloud
seo-description: You can programmatically modify nodes and properties located within the AEM repository, which is part of the Adobe Marketing Cloud
uuid: 2051d03f-430a-4cae-8f6d-e5bc727d733f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 69f62a38-7991-4009-8db7-ee8fd35dc535
exl-id: fe946b9a-b29e-4aa5-b973-e2a652417a55
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---

# Cómo acceder mediante programación al JCR de AEM{#how-to-programmatically-access-the-aem-jcr}

Puede modificar mediante programación nodos y propiedades ubicados dentro del repositorio de Adobe CQ, que forma parte de Adobe Marketing Cloud. Para acceder al repositorio de CQ, utiliza la API del repositorio de contenido Java (JCR). Puede utilizar la API JCR de Java para realizar operaciones de creación, sustitución, actualización y eliminación (CRUD) en contenido ubicado dentro del repositorio de Adobe CQ. Para obtener más información sobre la API de JCR de Java, consulte [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Este artículo de desarrollo modifica el JCR de Adobe CQ de una aplicación Java externa. Por el contrario, puede modificar el JCR desde un paquete OSGi mediante la API JCR. Para obtener más información, consulte [Persistencia de datos de CQ en el repositorio de contenido Java](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html).

>[!NOTE]
>
>Para utilizar la API de JCR, agregue la variable `jackrabbit-standalone-2.4.0.jar` a la ruta de clase de su aplicación Java. Puede obtener este archivo JAR desde la página web de la API de Java JCR en [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Para obtener información sobre cómo consultar el JCR de Adobe CQ mediante la API de consulta JCR, consulte [Consulta de datos de Adobe Experience Manager mediante la API de JCR](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Crear una instancia de repositorio {#create-a-repository-instance}

Aunque hay diferentes formas de conectarse a un repositorio y establecer una conexión, este artículo de desarrollo utiliza un método estático que pertenece al `org.apache.jackrabbit.commons.JcrUtils` Clase . El nombre del método es `getRepository`. Este método emplea un parámetro de cadena que representa la dirección URL del servidor de Adobe CQ. Por ejemplo `http://localhost:4503/crx/server`.

La variable `getRepository`el método devuelve un `Repository`como se muestra en el siguiente ejemplo de código.

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## Crear una instancia de sesión {#create-a-session-instance}

La variable `Repository`representa el repositorio CRX. Utilice la variable `Repository`para establecer una sesión con el repositorio. Para crear una sesión, invoque la función `Repository`del `login`método y pasar una `javax.jcr.SimpleCredentials` objeto. La variable `login`el método devuelve un `javax.jcr.Session` instancia.

Puede crear un `SimpleCredentials`usando su constructor y pasando los siguientes valores de cadena:

* El nombre de usuario;
* La contraseña correspondiente

Al pasar el segundo parámetro, llame al objeto String `toCharArray`método. El siguiente código muestra cómo llamar a la función `login`método que devuelve un `javax.jcr.Sessioninstance`.

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## Crear una instancia de nodo {#create-a-node-instance}

Utilice un `Session`para crear una `javax.jcr.Node` instancia. A `Node`instance permite realizar operaciones de nodos. Por ejemplo, puede crear un nuevo nodo. Para crear un nodo que represente el nodo raíz, invoque la variable `Session`instance&#39;s `getRootNode` como se muestra en la siguiente línea de código.

```java
//Create a Node
Node root = session.getRootNode();
```

Una vez que haya creado una `Node`, puede realizar tareas como crear otro nodo y añadir un valor a él. Por ejemplo, el siguiente código crea dos nodos y añade un valor al segundo nodo.

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## Recuperar valores de nodo {#retrieve-node-values}

Para recuperar un nodo y su valor, invoque la variable `Node`del `getNode`y pase un valor de cadena que represente la ruta completa al nodo. Tenga en cuenta la estructura de nodos creada en el ejemplo de código anterior. Para recuperar el nodo del día, especifique adobe/day, como se muestra en el siguiente código:

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## Creación de nodos en el repositorio de Adobe CQ {#create-nodes-in-the-adobe-cq-repository}

El siguiente ejemplo de código Java representa una clase Java que se conecta a Adobe CQ y crea una `Session`y añade nuevos nodos. A un nodo se le asigna un valor de datos y, a continuación, el valor del nodo y su ruta se escriben en la consola. Cuando haya terminado con la sesión, asegúrese de cerrar la sesión.

```java
/*
 * This Java Quick Start uses the jackrabbit-standalone-2.4.0.jar
 * file. See the previous section for the location of this JAR file
 */

import javax.jcr.Repository;
import javax.jcr.Session;
import javax.jcr.SimpleCredentials;
import javax.jcr.Node;

import org.apache.jackrabbit.commons.JcrUtils;
import org.apache.jackrabbit.core.TransientRepository;

public class GetRepository {

public static void main(String[] args) throws Exception {

try {

    //Create a connection to the CQ repository running on local host
    Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");

   //Create a Session
   javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));

  //Create a node that represents the root node
  Node root = session.getRootNode();

  // Store content
  Node adobe = root.addNode("adobe");
  Node day = adobe.addNode("day");
  day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");

  // Retrieve content
  Node node = root.getNode("adobe/day");
  System.out.println(node.getPath());
  System.out.println(node.getProperty("message").getString());

  // Save the session changes and log out
  session.save();
  session.logout();
  }
 catch(Exception e){
  e.printStackTrace();
  }
 }
}
```

Después de ejecutar el ejemplo de código completo y crear los nodos, puede ver los nuevos nodos en la variable **[!UICONTROL CRXDE Lite]**, como se muestra en la siguiente ilustración.

![chlimage_1-68](assets/chlimage_1-68a.png)
