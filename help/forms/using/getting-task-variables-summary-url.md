---
title: Obtención de variables de tarea en la dirección URL de resumen
seo-title: Obtención de variables de tarea en la dirección URL de resumen
description: Cómo reutilizar la información sobre una tarea y generar una URL de resumen para resumir o describir una tarea.
seo-description: Cómo reutilizar la información sobre una tarea y generar una URL de resumen para resumir o describir una tarea.
uuid: 9eab3a6a-a99a-40ae-b483-33ec7d21c5b6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6dc31bec-b02d-47db-a4f4-be8c14c5619e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Obtención de variables de tarea en la dirección URL de resumen {#getting-task-variables-in-summary-url}

La página de resumen muestra información relacionada con las tareas. Este artículo describe cómo puede reutilizar la información relacionada con las tareas en la página de resumen.

En esta orquestación de ejemplo, un empleado envía un formulario de solicitud de baja. A continuación, el formulario de solicitud se envía al administrador del empleado para su aprobación.

1. Cree un procesador HTML de muestra (html.esp) para resourcesType **Employees/PtoApplication**.

   El procesador asume las siguientes propiedades que se van a establecer en el nodo:

   * name
   * empid
   * reason
   * duration
   **Nota**: Este procesador es la plantilla de página de resumen.

   El siguiente código de muestra para este procesador se encuentra en:

   `apps/Employees/PtoApplication/html.esp`

   ```
   <html>
     <body>
       <table>
       <tbody>
       <tr>
           <td>
               <h3>Employee Name: <%= currentNode.ename %></h3>
               <h3>Employee ID: <%= currentNode.eid %></h3>
               <h3>Leave duration: <%= currentNode.duration %> days</h3>
               <h3>Reason: <%= currentNode.reason %></h3>
           </td>
       </tr>
       </tbody>
       </table>
     </body>
   </html>
   ```

1. Modifique la orquestación para extraer las cuatro propiedades de los datos del formulario enviado. Después de esto, cree un nodo en CRX de tipo **Empleados/PtoApplication**, con las propiedades rellenadas.

   1. Cree un proceso **cree un resumen** de PTO y utilícelo como un subproceso antes de la operación **Asignar tarea** en la orquestación.
   1. Defina **usernameName**, **workerID**, **ptoReason**, **totalDays** y **nodeName** como variables de entrada en el nuevo proceso. Estas variables se pasarán como datos de formulario enviados.

      También defina una variable de salida **ptoNodePath **que se utilizará al configurar la dirección URL de resumen.

   1. En el proceso de **creación de resumen** de PTO, utilice el componente de valor **** establecido para establecer los detalles de entrada en un mapa **nodeProperty **(**nodeProps**).

      Las claves de este mapa deben ser las mismas que las definidas en el procesador HTML en el paso anterior.

      Además, agregue una clave **sling:resourceType** con el valor **Employees/PtoApplication** en el mapa.

   1. Utilice el subproceso **storeContent** del servicio **ContentRepositoryConnector** en el proceso de **creación de resumen** de PTO. Este subproceso crea un nodo CRX.

      Se necesitan tres variables de entrada:

      * **Ruta** de carpeta: Ruta de acceso donde se crea el nuevo nodo CRX. Configure la ruta como **/contenido**.
      * **Nombre** del nodo: Asigne la variable de entrada nodeName a este campo. Es una cadena de nombre de nodo única.
      * **Tipo** de nodo: Defina el tipo como **no:no estructurado**. El resultado de este proceso es nodePath. nodePath es la ruta CRX del nodo recién creado. El resultado final del proceso de **creación de resumen de PTO** sería ndoePath.
   1. Pasar los datos del formulario enviados (**username**, **workerID**, **ptoReason** y **totalDays**) como entrada para el nuevo proceso **crear un resumen** de PTO. Tome la salida como **ptoSummaryNodePath**.


1. Defina la URL de resumen como una expresión XPath que contiene los detalles del servidor junto con **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

En el espacio de trabajo de AEM Forms, cuando se abre una tarea, la URL de resumen accede al nodo CRX y el procesador HTML muestra el resumen.

El diseño de resumen se puede cambiar sin modificar el proceso. El procesador HTML muestra el resumen correctamente.

**[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)**
