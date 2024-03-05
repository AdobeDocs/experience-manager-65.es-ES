---
title: ¿Cómo se utiliza el servicio de ejecución de scripts en AEM Forms en JEE Workbench para generar datos XML?
description: Usar el servicio de ejecución de scripts en AEM Forms en JEE Workbench para generar datos XML
exl-id: 2ec57cd4-f41b-4e5c-849d-88ca3d2cfe19
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 3%

---

# Usar el servicio de ejecución de scripts en AEM Forms en JEE Workbench para generar datos XML {#using-execute-script-service-forms-jee-workbench}

Hay mucho XML relacionado con los flujos de trabajo de AEM Forms en JEE Process Management, por ejemplo: la información XML se puede crear en un proceso y enviarse a una aplicación de Flex en AEM Forms en JEE Workspace, utilizarse para la configuración de sistemas o pasar información hacia y desde formularios. Hay muchos casos en los que un desarrollador de AEM Forms en JEE necesita administrar XML y muchas veces esto requiere que el XML se administre a través de un proceso de AEM Forms en JEE.

Cuando se trata de una configuración XML simple, se puede utilizar la variable `Set Value` , que es un servicio predeterminado de AEM Forms en JEE. Este servicio establece el valor de uno o más elementos de datos en el modelo de datos de proceso. Para una lógica condicional simple, los escenarios &quot;si es esto, entonces es lo&quot;, este servicio puede adaptarse al propósito.

Sin embargo, en situaciones más complejas, el servicio Establecer valor no es tan eficaz. En estas situaciones, se debe confiar en un conjunto más robusto de comandos de programación, como los que proporciona un lenguaje de programación como Java™. El uso de Java™ para generar XML complejo puede ser mucho más fácil y claro que la creación de un documento XML a partir de texto simple dentro del servicio Establecer valor. Además, es más fácil incluir la programación condicional en Java™ que dentro de un servicio Set Value.

## Uso del servicio Ejecutar script en un proceso {#using-execute-script-service-in-process}

Dentro del conjunto de servicios estándar de AEM Forms en JEE disponibles en AEM Forms en JEE Workbench, se encuentra el `Execute Script` servicio. Este servicio permite ejecutar scripts en procesos y proporciona el `executeScript` operación para hacerlo.

### Crear una aplicación y un proceso con el servicio &quot;Ejecutar script&quot; definido como actividad {#create-an-application}

La creación general de aplicaciones y procesos está fuera del ámbito de este tutorial, pero para esta instrucción, se ha creado una aplicación denominada DemoApplication02. Suponiendo que ya se ha creado una aplicación, debe crear un proceso en esta aplicación para llamar al servicio executeScript. Para agregar un proceso a la aplicación que incluye `Execute Script` servicio:

1. Haga clic con el botón derecho en la aplicación y seleccione **[!UICONTROL Nuevo]**. Entrada **[!UICONTROL Nuevo]** menú deslizable, seleccionar **[!UICONTROL Proceso]**. Asigne un nombre al proceso, añada una descripción, si es necesario, y seleccione el icono que desea que represente este proceso. Para los fines de este tutorial, hemos creado un proceso y lo hemos denominado  `executeScriptDemoProcess`.
1. Defina sus puntos de inicio o simplemente opte por añadir sus puntos de inicio más adelante.
1. El proceso se creará y se abrirá automáticamente en [!UICONTROL Diseño de procesos] ventana. En esta ventana, haga clic en el icono Selector de actividad en la parte superior de la ventana Diseño del proceso y arrastre la nueva actividad a la pista de natación. En este punto, la variable [!UICONTROL Ventana Definición de Actividad] (consulte la figura siguiente).
   ![Definir actividad](assets/define-activity.jpg)
1. El servicio executeScript se encuentra en `Foundation` conjunto de servicios. El nombre Servicios enumera el objeto como `Execute Script – 1.0` con el nombre de la operación `executeScript`. Haga clic para seleccionar este elemento.
1. Este proceso debe crearse y, de forma predeterminada, la variable [!UICONTROL Propiedades del proceso] La ventana de debe aparecer en el panel de la izquierda.

#### Añadir un script al proceso con el servicio &quot;Ejecutar script&quot; {#add-script-to-process-with-execute-script}

Una vez creado el proceso con la actividad del servicio &quot;Ejecutar script&quot; definida, se puede añadir una secuencia de comandos a este proceso. Para agregar una secuencia de comandos a este proceso:

1. Vaya a [!UICONTROL Propiedades del proceso] paleta. Dentro de esta paleta, expanda el [!UICONTROL Entrada] y haga clic en el icono &quot;...&quot;.

1. En el cuadro de texto que aparece, escriba el script. Una vez escrito el script, presione Aceptar (consulte la figura siguiente).
   ![Ejecutar script](assets/execute-script.jpg)

## Crear XML mediante el servicio Ejecutar script {#create-xml-execute-script-service}

Una vez creado un proceso con el servicio Ejecutar script incluido, se puede utilizar este script para crear XML. Se escribirían los scripts que se describen a continuación en el cuadro de texto descrito en Agregar un script al proceso con `Execute Script` Sección de servicio anterior.

**Acerca de la tecnología del servicio Ejecutar script**

Para saber cuáles son las capacidades y limitaciones del servicio Ejecutar Script, es necesario conocer los fundamentos tecnológicos del servicio. AEM Forms en JEE utiliza el analizador del modelo de objetos de documento (DOM) de Apache Xerces para crear y almacenar variables XML en procesos. Xerces es una implementación Java™ de la especificación del Modelo de objetos de documento de W3C; definici ó n [aquí](https://dom.spec.whatwg.org/). La especificación DOM es una forma estándar de manipular XML que existe desde 1998. La implementación Java™ de Xerces, Xerces-J, es compatible con la versión 1.0 del nivel 2 del DOM.

Las clases Java™ utilizadas para almacenar variables XML son:

* org.apache.xerces.dom.NodeImpl y

* org.apache.xerces.dom.DocumentImpl

DocumentImpl es una subclase de NodeImpl, por lo que se puede suponer que cualquier variable de proceso XML es una derivación de NodeImpl. Puede encontrar la documentación de NodeImpl [aquí](https://xerces.apache.org/xerces-j/apiDocs/org/apache/xerces/dom/NodeImpl.html).

**Creación de XML de ejemplo mediante el servicio Ejecutar script**

Este es un ejemplo de creación de XML, dentro de un servicio Ejecutar script. El proceso tiene un nodo de variable que es de tipo XML. El resultado de esta actividad es un documento XML. Lo que hace ese documento, o cómo se aplica al proceso general, está fuera de ámbito para este tutorial; en última instancia, se reduce a lo que el XML debe hacer en la aplicación general. Como se mencionó en la introducción, el XML se puede utilizar para muchos fines en AEM Forms en formularios y procesos JEE; esta es simplemente una explicación de cómo codificar la actividad Ejecutar script para generar un documento XML simple.

Un JavaScript simple para generar XML tendría este aspecto:

```xml
import org.apache.xerces.dom.DocumentImpl;

import org.w3c.dom.Document;

import org.w3c.dom.Element;



Document document = new DocumentImpl();

Element topLevelResources = document.createElement("resources");

Element resource = document.createElement("resource");

resource.setAttribute("id", "first item id");

resource.setAttribute("value", "first item value");

topLevelResources.appendChild(resource);

document.appendChild(topLevelResources);

patExecContext.setProcessDataValue("/process_data/node", document);
```

>[!NOTE]
>
>Los objetos DOM mencionados anteriormente deben importarse en la secuencia de comandos.

El resultado de este script simple es un nuevo documento XML con un nodo de variable establecido en:

```xml
<resources>

<resource id="first item id" value="first item value"/>

</resources>
```

**Uso de un bucle iterativo para agregar nodos al XML**

Los nodos también se pueden agregar a una variable XML existente dentro del proceso. La variable, node, contiene el objeto XML creado.

```xml
Document document = patExecContext.getProcessDataValue("/process_data/node");

NodeList childNodes = document.getChildNodes();

int numChildren = childNodes.getLength();

for (int i = 0; i < numChildren; i++)

{

Node currentChild = childNodes.item(i);

if (currentChild.getNodeType() == Node.ELEMENT_NODE)

{

// found the top-level node

Element newResource = document.createElement("resource");

newResource.setAttribute("id", "second item id");

newResource.setAttribute("value", "second item value");

currentChild.appendChild(newResource);

break;

}

}

patExecContext.setProcessDataValue("/process_data/node", document);
The variable node in the XML is now set to:

<resources> 

<resource id="first item id" value="first item value"/> 

<resource id="second item id" value="second item value"/> 

</resources>
```
