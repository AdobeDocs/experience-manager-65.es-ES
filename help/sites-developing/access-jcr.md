---
title: Cómo acceder mediante programación al JCR AEM
seo-title: Cómo acceder mediante programación al JCR AEM
description: Puede modificar mediante programación nodos y propiedades ubicados en el repositorio de AEM, que forma parte del Adobe Marketing Cloud
seo-description: Puede modificar mediante programación nodos y propiedades ubicados en el repositorio de AEM, que forma parte del Adobe Marketing Cloud
uuid: 2051d03f-430a-4cae-8f6d-e5bc727d733f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 69f62a38-7991-4009-8db7-ee8fd35dc535
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---


# Cómo acceder mediante programación al JCR{#how-to-programmatically-access-the-aem-jcr} de AEM

Puede modificar mediante programación nodos y propiedades ubicados dentro del repositorio de Adobe CQ, que forma parte del Adobe Marketing Cloud. Para acceder al repositorio de CQ, utilice la API de Java Content Repository (JCR). Puede utilizar la API de JCR de Java para realizar operaciones de creación, sustitución, actualización y eliminación (CRUD) en contenido ubicado en el repositorio de Adobe CQ. Para obtener más información sobre la API de JCR de Java, consulte [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Este artículo de desarrollo modifica el JCR de Adobe CQ desde una aplicación Java externa. Por el contrario, puede modificar el JCR desde un paquete OSGi mediante la API de JCR. Para obtener más información, consulte [Datos CQ persistentes en el repositorio de contenido de Java](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html).

>[!NOTE]
>
>Para utilizar la API de JCR, agregue el archivo `jackrabbit-standalone-2.4.0.jar` a la ruta de clases de la aplicación Java. Puede obtener este archivo JAR desde la página Web de la API de Java JCR en [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Para obtener información sobre cómo realizar la consulta del JCR de Adobe CQ mediante la API de Consulta JCR, consulte [Consulta de datos de Adobe Experience Manager mediante la API de JCR](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Crear una instancia de repositorio {#create-a-repository-instance}

Aunque hay diferentes maneras de conectarse a un repositorio y establecer una conexión, este artículo de desarrollo utiliza un método estático que pertenece a la clase `org.apache.jackrabbit.commons.JcrUtils`. El nombre del método es `getRepository`. Este método toma un parámetro de cadena que representa la dirección URL del servidor de Adobe CQ. Por ejemplo `http://localhost:4503/crx/server`.

El método `getRepository`devuelve una instancia `Repository`, como se muestra en el siguiente ejemplo de código.

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## Crear una instancia de sesión {#create-a-session-instance}

La instancia `Repository`representa el repositorio de CRX. La instancia `Repository`se utiliza para establecer una sesión con el repositorio. Para crear una sesión, invoque el método `Repository`de la instancia `login`y pase un objeto `javax.jcr.SimpleCredentials`. El método `login`devuelve una instancia `javax.jcr.Session`.

Para crear un objeto `SimpleCredentials`se utiliza su constructor y se pasan los siguientes valores de cadena:

* El nombre de usuario;
* La contraseña correspondiente

Al pasar el segundo parámetro, llame al método `toCharArray`del objeto String. El siguiente código muestra cómo llamar al método `login`que devuelve un `javax.jcr.Sessioninstance`.

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## Crear una instancia de nodo {#create-a-node-instance}

Utilice una instancia `Session`para crear una instancia `javax.jcr.Node`. Una instancia `Node`permite realizar operaciones de nodo. Por ejemplo, puede crear un nuevo nodo. Para crear un nodo que represente el nodo raíz, invoque el método `Session`de la instancia `getRootNode`, como se muestra en la siguiente línea de código.

```java
//Create a Node
Node root = session.getRootNode();
```

Una vez creada una instancia `Node`, puede realizar tareas como crear otro nodo y agregarle un valor. Por ejemplo, el código siguiente crea dos nodos y agrega un valor al segundo nodo.

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## Recuperar valores de nodo {#retrieve-node-values}

Para recuperar un nodo y su valor, invoque el método `Node`de la instancia `getNode`y pase un valor de cadena que represente la ruta completa al nodo. Considere la estructura de nodos creada en el ejemplo de código anterior. Para recuperar el nodo day, especifique adobe/day, como se muestra en el código siguiente:

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## Crear nodos en el repositorio de Adobe CQ {#create-nodes-in-the-adobe-cq-repository}

El siguiente ejemplo de código Java representa una clase Java que se conecta a Adobe CQ, crea una instancia `Session`y agrega nuevos nodos. A un nodo se le asigna un valor de datos y, a continuación, el valor del nodo y su ruta se escriben en la consola. Cuando termine con la sesión, asegúrese de cerrar la sesión.

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

Después de ejecutar el ejemplo de código completo y crear los nodos, puede realizar la vista de los nuevos nodos en el **[!UICONTROL CRXDE Lite]**, como se muestra en la siguiente ilustración.

![chlimage_1-68](assets/chlimage_1-68a.png)

