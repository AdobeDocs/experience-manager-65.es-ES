---
title: Creative Project e integración PIM
seo-title: Creative Project e integración PIM
description: Proyecto creativo agiliza el flujo de trabajo completo de la sesión fotográfica que incluye generar una solicitud de sesión fotográfica, cargar una sesión fotográfica, colaborar en una sesión fotográfica y empaquetar recursos aprobados
seo-description: Proyecto creativo agiliza el flujo de trabajo completo de la sesión fotográfica que incluye generar una solicitud de sesión fotográfica, cargar una sesión fotográfica, colaborar en una sesión fotográfica y empaquetar recursos aprobados
uuid: 09f27d36-e725-45cb-88d1-27383aedceed
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 0e5d0a45-c663-4d91-b793-03d39119d103
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '3013'
ht-degree: 68%

---


# Creative Project e integración PIM{#creative-project-and-pim-integration}

Si es un especialista en marketing o un profesional creativo, puede utilizar las herramientas de Creative Project en Adobe Experience Manager (AEM) para administrar la fotografía de productos relacionada con el comercio electrónico y los procesos creativos asociados dentro de su organización.

En concreto, puede utilizar Proyecto creativo para agilizar las tareas siguientes en el flujo de trabajo de la sesión fotográfica:

* Creación de una solicitud de sesión fotográfica
* Carga de una sesión fotográfica
* Colaborar en una sesión fotográfica
* Recursos aprobados para el empaquetado

>[!NOTE]
>
>Consulte [Funciones de usuario del proyecto](/help/sites-authoring/projects.md#user-roles-in-a-project) para obtener información sobre la asignación de funciones de usuario y flujos de trabajo a ciertos tipos de usuarios.

## Explorar los flujos de trabajo de la sesión fotográfica del producto  {#exploring-product-photo-shoot-workflows}

Creative Project ofrece varias plantillas de proyecto para cumplir los distintos requisitos del proyecto. La plantilla **Proyecto de sesión fotográfica del producto** está disponible y lista para usar. Esta plantilla incluye los flujos de trabajo de la sesión fotográfica que le permiten iniciar y administrar las solicitudes de sesión fotográfica del producto. También incluye una serie de tareas que le permiten obtener las imágenes digitales para los productos a través de procesos de revisión y aprobación apropiados.

La plantilla incluye los siguientes flujos de trabajo:

* **Flujo de trabajo de la sesión fotográfica del producto (integración del comercio)**: este flujo de trabajo aprovecha la integración del comercio en el sistema de administración de la información del producto (PIM) para generar automáticamente una lista de tomas para los productos seleccionados (jerarquía). Puede ver los datos del producto como parte de los metadatos de recursos una vez completado el flujo de trabajo.
* **Flujo de trabajo de la sesión fotográfica del producto**: este flujo de trabajo le permite proporcionar una lista de tomas en lugar de depender de la integración del comercio. Asigna las imágenes cargadas en un archivo CSV de la carpeta de recursos del proyecto.

>[!NOTE]
>
>El archivo CSV que se carga en la tarea Cargar lista de tomas del flujo de trabajo de sesión fotográfica del producto debe tener el nombre de archivo shotlist.csv.

## Crear un proyecto de sesión fotográfica del producto {#create-a-product-photo-shoot-project}

1. En la consola **Proyectos**, toque o haga clic en **Crear** y, a continuación, elija **Crear proyecto** en la lista.

   ![chlimage_1-132](assets/chlimage_1-132a.png)

1. En la página **Crear proyecto**, seleccione la plantilla de proyecto de sesión fotográfica y toque o haga clic en **Siguiente**.

   ![chlimage_1-133](assets/chlimage_1-133a.png)

1. Introduzca los detalles del proyecto, incluido el título, la descripción y la fecha de caducidad. Añada usuarios y asígneles diversas funciones. También puede añadir una miniatura para el proyecto.

   ![chlimage_1-134](assets/chlimage_1-134a.png)

1. Toque o haga clic en **Crear**. Un mensaje de confirmación notifica que el proyecto se ha creado.
1. Toque o haga clic **Listo** para volver a la consola **Proyectos**. O bien, toque o haga clic en **Abrir** para vista de los recursos dentro del proyecto de sesión fotográfica.

## Comenzar a trabajar en un proyecto de sesión fotográfica del producto {#starting-work-in-a-product-photo-shoot-project}

Para iniciar una solicitud de sesión fotográfica, toque o haga clic en un proyecto y, a continuación, toque o haga clic en **Añadir trabajo** en la página de detalles del proyecto para iniciar un flujo de trabajo.

![chlimage_1-133](assets/chlimage_1-135a.png)

Un proyecto de sesión fotográfica del producto incluye los siguientes flujos de trabajo listos para usarse:

* Flujo de trabajo de la sesión fotográfica del producto (integración del comercio)
* Flujo de trabajo de la sesión fotográfica del producto

Utilice el flujo de trabajo de la sesión fotográfica del producto (integración del comercio) para asignar los recursos de imagen a los productos de AEM. Este flujo de trabajo aprovecha la integración del comercio para vincular las imágenes aprobadas a los datos del producto existentes en la ubicación */etc/commerce*.

El flujo de trabajo de sesión fotográfica de producto (Integración comercial) incluye las siguientes tareas:

* Crear lista de tomas
* Cargar sesión fotográfica
* Retocar sesión fotográfica
* Revisar y aprobar
* Mover a la tarea de producción

Si la información del producto no está disponible en AEM, utilice el flujo de trabajo de la sesión fotográfica del productopara asignar los recursos de imagen a los productos de acuerdo con los datos que haya cargado en un archivo CSV. El archivo CSV debe contener información del producto básica, como el identificador, la categoría y una descripción del producto. El flujo de trabajo obtiene recursos aprobados para los productos.

Este flujo de trabajo incluye las tareas siguientes:

* Cargar lista de tomas
* Cargar sesión fotográfica
* Retocar sesión fotográfica
* Revisar y aprobar
* Mover a la tarea de producción

Puede personalizar este flujo de trabajo mediante la opción de configuración de flujo de trabajo.

Ambos flujos de trabajo incluyen pasos para vincular productos a los recursos aprobados. Cada flujo de trabajo incluye los pasos siguientes:

* Configuración de flujo de trabajo: describe las opciones para personalizar el flujo de trabajo.
* Iniciar un flujo de trabajo del proyecto: explica cómo iniciar una sesión fotográfica del producto.
* Información sobre las tareas de flujo de trabajo: proporciona información sobre las tareas disponibles en el flujo de trabajo.

## Seguimiento del progreso del proyecto  {#tracking-project-progress}

Para realizar un seguimiento del progreso de un proyecto, puede controlar las tareas activas/terminadas de un proyecto.

Utilice la información siguiente para controlar el progreso de un proyecto:

* **Tarjeta de la tarea**

* **Lista de tareas**

La tarjeta de Tarea muestra el progreso general del proyecto. Aparece en la página Detalles del proyecto solo si el proyecto tiene alguna tarea relacionada. La tarjeta de la tarea muestra el estado de finalización del proyecto actual de acuerdo con el número de tareas completadas. No incluye las tareas futuras.

La tarjeta de la tarea proporciona la información siguiente:

* Porcentaje de tareas activas
* Porcentaje de tareas completadas

![chlimage_1-136](assets/chlimage_1-136a.png)

La lista de tareas proporciona información detallada sobre la tarea para el proyecto que actualmente tiene un flujo de trabajo activo. Para mostrar la lista, toque o haga clic en la tarjeta de la tarea. La lista de tareas también muestra metadatos como, por ejemplo, fecha de inicio, fecha de caducidad, usuario asignado, prioridad y estado de la tarea.

![chlimage_1-137](assets/chlimage_1-137a.png)

## Configuración de flujo de trabajo {#workflow-configuration}

Esta tarea consiste en asignar pasos del flujo de trabajo a los usuarios según sus funciones.

Para configurar el flujo de trabajo de la **sesión fotográfica del producto**:

1. Vaya a **Herramientas** > **Flujos de trabajo** y, a continuación, toque el mosaico **Modelos** para abrir la página **Modelos de flujo de trabajo**.
1. Seleccione el flujo de trabajo **Captura de fotos del producto** y toque el icono **Editar** en la barra de herramientas para abrirlo en modo de edición.

   ![chlimage_1-138](assets/chlimage_1-138a.png)

1. En la página **Flujo de trabajo de sesión fotográfica del producto**, abra una tarea del proyecto. Por ejemplo, abra la tarea **Cargar lista de tomas**.

   ![chlimage_1-139](assets/chlimage_1-139a.png)

1. Haga clic en la pestaña **Tarea** para configurar las opciones siguientes:

   * Nombre de la tarea.
   * Usuario predeterminado (función) que recibe la tarea.
   * Prioridad predeterminada de la tarea, que se muestra en la lista de tareas del usuario.
   * Descripción de una tarea que se mostrará cuando el usuario asignado abra la tarea.
   * Fecha de caducidad de una tarea, que se calcula en función del momento en que la tarea comenzó.

1. Haga clic en **OK** para guardar las opciones de configuración.

   De manera similar, puede configurar las tareas siguientes para el flujo de trabajo de la **sesión fotográfica del producto**:

   * Cargar sesión fotográfica
   * Retocar la sesión fotográfica del producto
   * Revisión de sesión fotográfica
   * Mover a producción

   Realice un procedimiento similar para configurar las tareas en el flujo de trabajo **Product Photo Shoot (Commerce Integration)**.

En esta sección se describe cómo integrar la administración de la información del producto en su proyecto creativo.

## Iniciar un flujo de trabajo del proyecto  {#starting-a-project-workflow}

1. Vaya a un proyecto de sesión fotográfica de producto y toque o haga clic en el icono **Añadir trabajo** de la tarjeta **Flujos de trabajo**.
1. Seleccione la tarjeta del flujo de trabajo de la **sesión fotográfica del producto (integración del comercio)** para iniciar el flujo de trabajo de la sesión fotográfica del producto (integración del comercio). Si la información del producto no está disponible en /etc/commerce, seleccione el flujo de trabajo **Captura de fotos del producto** y inicio el flujo de trabajo de sesión fotográfica del producto.

   ![chlimage_1-140](assets/chlimage_1-140a.png)

1. Toque o haga clic en **Siguiente** para iniciar el flujo de trabajo en el proyecto.
1. Introduzca la información del flujo de trabajo en la página siguiente.

   ![chlimage_1-141](assets/chlimage_1-141a.png)

   Haga clic en **Enviar** para iniciar el flujo de trabajo de la sesión fotográfica. Se muestra la página de información del proyecto para el proyecto de sesión fotográfica.

   ![chlimage_1-142](assets/chlimage_1-142a.png)

### Información de las tareas de flujo de trabajo {#workflow-tasks-details}

El flujo de trabajo de la sesión fotográfica incluye varias tareas. Cada una de ellas se asigna a un grupo de usuarios en función de la configuración definida para la tarea.

#### Tarea Crear lista de tomas  {#create-shot-list-task}

La tarea **Crear lista de tomas** permite al propietario del proyecto seleccionar los productos para los que se requieren imágenes. De acuerdo con la opción seleccionada por el usuario, se genera un archivo CSV que contiene la información del producto básica.

1. En la carpeta del proyecto, toque o haga clic en las elipses de la [Tarjeta de Tareas](#tracking-project-progress) para vista del elemento de tarea en el flujo de trabajo.

   ![chlimage_1-143](assets/chlimage_1-143a.png)

1. Seleccione la tarea **Crear Lista de toma** y, a continuación, toque o haga clic en el icono **Abrir** de la barra de herramientas.

   ![chlimage_1-144](assets/chlimage_1-144a.png)

1. Revise la información de la tarea y, a continuación, toque o haga clic en el botón **Crear lista de tomas**.

   ![chlimage_1-145](assets/chlimage_1-145a.png)

1. Seleccione los productos para los que existen datos del producto sin imágenes asociadas.

   ![chlimage_1-146](assets/chlimage_1-146a.png)

1. Toque o haga clic en el icono **Añadir a lista de tomas** para crear un archivo CSV que contenga una lista de todos esos productos. Un mensaje confirma que se ha creado la lista de tomas para los productos seleccionados. Haga clic en **Cerrar** para completar el flujo de trabajo.
1. Después de crear una lista de tomas, se muestra el vínculo **Ver lista de tomas**. Para agregar más productos a la lista de toma, toque/haga clic **Añadir a la Lista de toma**. En este caso, los datos se añaden a la lista de tomas creada inicialmente.

   ![chlimage_1-147](assets/chlimage_1-147a.png)

1. Toque o haga clic en **Ver lista de tomas** para ver la nueva lista de tomas.

   ![chlimage_1-148](assets/chlimage_1-148a.png)

   Para editar los datos existentes o añadir datos nuevos, toque o haga clic en **Editar** en la barra de herramientas. Solo se pueden editar los campos **Product **and **Description**.

   ![chlimage_1-149](assets/chlimage_1-149a.png)

   Después de actualizar el archivo, toque o haga clic en **Guardar** en la barra de herramientas para guardar el archivo.

1. Después de agregar los productos, toque o haga clic en el icono **Completar** en la página **Crear Lista de toma **Detalles de tarea para marcar la tarea como completada. Puede añadir un comentario opcional.

   La finalización de la tarea presenta los siguientes cambios en el proyecto:

   * Los recursos correspondientes a la jerarquía del producto se crean en una carpeta con el mismo nombre que el título del flujo de trabajo.
   * Los metadatos para los recursos se convierten en editables mediante la consola Recursos, incluso antes de que el fotógrafo proporcione las imágenes.
   * Se crea una carpeta de la sesión fotográfica en que se almacenan las imágenes que el fotógrafo proporciona. La carpeta de la sesión fotográfica contiene las subcarpetas para cada entrada del producto en la lista de tomas.

   Cargar lista de tomas es la primera tarea del flujo de trabajo de la sesión fotográfica del producto (sin integración del comercio). Toque o haga clic en **Cargar lista de tomas** para cargar un archivo **shotlist.csv**. El archivo CSV debe contener el identificador del producto. Los demás campos son opcionales. Puede utilizarlos para asignar recursos a los productos.

### Tarea Cargar lista de tomas  {#upload-shot-list-task}

Esta tarea forma parte del flujo de trabajo de la sesión fotográfica del producto. Esta tarea se realiza si la información del producto no está disponible en AEM. En este caso, se carga una lista de productos en un archivo CSV para el que se necesitan recursos de imagen. En función de los detalles del archivo CSV, los recursos de imagen se asignan a los productos.

Utilice el vínculo **Ver lista de tomas** en la tarjeta del proyecto del procedimiento anterior para descargar un archivo CSV de muestra. Revise el archivo de muestra para saber cuál es el contenido habitual de un archivo CSV.

La lista de productos o el archivo CSV pueden contener campos, tales como **Categoría, Identificador del producto, Descripción** y **Ruta de acceso**. El campo **Identificador** es obligatorio y contiene el identificador del producto. Los demás campos son opcionales.

Un producto puede pertenecer a una categoría determinada. La categoría del producto puede aparecer en el CSV debajo de la columna **Categoría**. El campo **Producto** contiene el nombre del producto. En el campo **Descripción**, introduzca la descripción del producto o las instrucciones para el fotógrafo.

>[!NOTE]
>
>El nombre de las imágenes que se van a cargar debe tener el inicio &quot;**&lt;ProductId>_&quot;** donde se hace referencia al ID de producto desde el campo **Id** del archivo *shotlist.csv*. Por ejemplo, para un producto de la lista de toma con **Id. 397122**, puede cargar archivos con nombres **397122_high-Contraste.jpg**, **397122_lowlight.png**, etc.

1. En la carpeta del proyecto, toque o haga clic en las elipses de la [Tarjeta de Tareas](#tracking-project-progress) para vista de la lista de tareas en el flujo de trabajo.
1. Seleccione la tarea **Cargar Lista de toma** y, a continuación, toque o haga clic en el icono **Abrir** de la barra de herramientas.

   ![chlimage_1-150](assets/chlimage_1-150a.png)

1. Revise los detalles de la tarea y, a continuación, toque o haga clic en el botón **Cargar Lista de toma**.

   ![chlimage_1-151](assets/chlimage_1-151a.png)

1. Toque o haga clic en el botón **Cargar Lista de toma** para cargar el archivo CSV con el nombre de archivo shotlist.csv. El flujo de trabajo reconoce este archivo como origen que se utilizará para extraer los datos del producto para la tarea siguiente.
1. Cargue un archivo CSV que contenga la información del producto en el formato adecuado. El vínculo **Vista de recursos cargados** aparece debajo de la tarjeta después de cargar el archivo CSV.

   ![chlimage_1-152](assets/chlimage_1-152a.png)

   Haga clic en el icono **Completar** para completar la tarea.

1. Toque o haga clic en el icono **Completar** para completar la tarea.

### Tarea Cargar sesión fotográfica {#upload-photo-shoot-task}

Si es un editor, puede cargar las tomas de los productos enumerados en el archivo **shotlist.csv** que se crea o carga en la tarea anterior.

El nombre de las imágenes que se van a cargar debe comenzar por **&quot;&lt;productId>_&quot;** donde se hace referencia al ID de producto desde el campo **Id** del archivo **shotlist.csv**. Por ejemplo, para un producto con un **identificador 397122** en la lista de tomas, puede cargar archivos con nombres **397122_highcontrast.jpg**, **397122_lowlight.png**, etcétera.

Puede cargar las imágenes directamente o cargar un archivo ZIP que contenga las imágenes. De acuerdo con sus nombres, las imágenes se encuentran en carpetas de productos respectivas dentro de la carpeta **Sesión fotográfica**.

1. En la carpeta del proyecto, toque o haga clic en las elipses de la [tarjeta de Tarea](#tracking-project-progress) para vista del elemento de tarea en el flujo de trabajo.
1. Seleccione la tarea **Cargar sesión fotográfica** y, a continuación, toque o haga clic en el icono **Abrir** de la barra de herramientas.

   ![chlimage_1-153](assets/chlimage_1-153a.png)

1. Toque o haga clic **Cargar sesión fotográfica** y cargue las imágenes de la sesión fotográfica.
1. Toque o haga clic en el icono **Completar** de la barra de herramientas para completar la tarea.

### Tarea Retocar sesión fotográfica  {#retouch-photo-shoot-task}

Si tiene derechos de edición, realice la tarea Retocar sesión fotográfica para editar las imágenes cargadas en la carpeta de la sesión fotográfica.

1. En la carpeta del proyecto, toque o haga clic en las elipses de la [tarjeta de Tarea](#tracking-project-progress) para vista del elemento de tarea en el flujo de trabajo.
1. Seleccione la tarea **Retocar sesión fotográfica** y, a continuación, toque o haga clic en el icono **Abrir** de la barra de herramientas.

   ![chlimage_1-154](assets/chlimage_1-154a.png)

1. Toque o haga clic en el vínculo **Vista de recursos cargados** en la página **Retocar sesión fotográfica** para examinar las imágenes cargadas.

   ![chlimage_1-155](assets/chlimage_1-155a.png)

   Si es necesario, edite las imágenes mediante una aplicación de Adobe Creative Cloud.

   ![chlimage_1-156](assets/chlimage_1-156a.png)

1. Toque o haga clic en el icono **Completar** de la barra de herramientas para completar la tarea.

### Revisar y aprobar la tarea {#review-and-approve-task}

En esta tarea, las imágenes de la sesión fotográfica cargadas por un fotógrafo se revisan y se marcan como aprobadas para usarse.

1. En la carpeta del proyecto, toque o haga clic en las elipses de la [tarjeta de Tarea](#tracking-project-progress) para vista del elemento de tarea en el flujo de trabajo.
1. Seleccione la tarea **Revisar y aprobar** y, a continuación, toque o haga clic en el icono **Abrir** de la barra de herramientas.

   ![chlimage_1-157](assets/chlimage_1-157a.png)

1. En la página **Revisar y aprobar**, asigne la tarea de revisión a la función, por ejemplo los revisores, y luego toque o haga clic en **Revisar **al inicio para revisar las imágenes del producto cargadas.

   ![chlimage_1-158](assets/chlimage_1-158a.png)

1. Seleccione una imagen del producto y toque o haga clic en el icono Aprobar de la barra de herramientas para marcarla como aprobada.

   ![chlimage_1-159](assets/chlimage_1-159a.png)

   Una vez aprobada una imagen, se muestra sobre ella un letrero aprobado.

   >[!NOTE]
   Puede dejar algunos productos sin ninguna imagen. Más adelante, puede volver a visitar la tarea y marcarla como completada cuando haya terminado.

1. Toque o haga clic en **Completar**. Las imágenes aprobadas están vinculados a los recursos vacíos que se han creado.

Puede navegar a los recursos del proyecto a través de la IU de Recursos y verificar las imágenes aprobadas.

Toque o haga clic en el nivel siguiente para ver los productos de acuerdo con su jerarquía de datos del producto.

Creative Project asocia los recursos aprobados al producto utilizado como referencia. Los metadatos de recursos se actualizan con la referencia del producto y la información básica en la pestaña **Datos del producto**; en las propiedades de recursos, aparecen en la sección Metadatos de recursos de AEM.

>[!NOTE]
En el flujo de trabajo de la sesión fotográfica del producto (sin integración del comercio), las imágenes aprobadas no están asociadas a los productos.

### Mover a la tarea de producción  {#move-to-production-task}

Esta tarea mueve los recursos aprobados a la carpeta lista para la producción para que estén disponibles para usarse.

1. En la carpeta del proyecto, toque o haga clic en las elipses de la [tarjeta de Tarea](#tracking-project-progress) para vista del elemento de tarea en el flujo de trabajo.
1. Seleccione la tarea **Mover a producción** y, a continuación, toque o haga clic en el icono **Abrir** de la barra de herramientas.

   ![chlimage_1-160](assets/chlimage_1-160a.png)

1. Para ver los recursos aprobados de la sesión fotográfica antes de moverlos a la carpeta lista para la producción, haga clic en el vínculo **Ver recursos aprobados** debajo de la miniatura del proyecto en la página de la tarea **Mover a producción**.

   ![chlimage_1-161](assets/chlimage_1-161a.png)

1. Introduzca la ruta de la carpeta lista para producción en el campo **Mover a**.

   ![chlimage_1-162](assets/chlimage_1-162a.png)

   Toque o haga clic en **Mover a producción**. Cierre el mensaje de confirmación. Los recursos se desplazan a la ruta de acceso mencionada y se crea automáticamente un conjunto de giros para los recursos aprobados para cada producto de acuerdo con la jerarquía de carpetas.

1. Toque o haga clic en el icono **Completar** de la barra de herramientas. El flujo de trabajo termina cuando el último paso se marca como completado.

## Visualización de los metadatos de recursos DAM  {#viewing-dam-asset-metadata}

Una vez los apruebe, los recursos se vinculan a los productos correspondientes. La [página de propiedades](/help/assets/manage-assets.md#editing-properties) de los recursos aprobados ahora tiene una pestaña **Datos de producción (información del producto vinculada)** adicional. En esta pestaña se muestra la información del producto, el número de SKU y otros datos relacionados con el producto que vinculan el recurso. Toque o haga clic en el icono **Editar** para actualizar las propiedades de un recurso. La información relacionada con el producto es de solo lectura.

Toque o haga clic en el vínculo que aparece para desplazarse a la página correspondiente de información del producto en la consola de productos a la que el recurso está asociado.

## Personalizar los flujos de trabajo de la sesión fotográfica del proyecto  {#customizing-the-project-photo-shoot-workflows}

Puede personalizar los flujos de trabajo de la sesión fotográfica del proyecto en función de los requisitos. Esta es una tarea opcional, basada en las funciones, que se lleva a cabo para establecer el valor de una variable dentro del proyecto. Posteriormente, se puede utilizar el valor configurado para tomar una decisión.

1. Toque o haga clic en el logotipo de AEM y, a continuación, vaya a **Herramientas** > **Flujo de trabajo** > **Modelos** para abrir la página Modelos de flujo de trabajo.
1. Seleccione el flujo de trabajo de la **sesión fotográfica del producto (integración del comercio)** o el flujo de trabajo de la **sesión fotográfica del producto** y toque o haga clic en **Editar** en la barra de herramientas para abrir el flujo de trabajo en modo de edición.
1. Abra las tareas **Proyectos** en la barra de tareas y arrastre el paso **Crear tarea de proyecto basada en funciones** al flujo de trabajo.

   ![chlimage_1-163](assets/chlimage_1-163a.png)

1. Abra el paso **Tarea basada en roles**.
1. En la pestaña **Tarea**, especifique un nombrepara la tarea que se mostrará en la lista **Tarea**. También puede asignar la tarea a una función, establecer la prioridad predeterminada, proporcionar una descripción y especificar una hora en la que vence la tarea.

   ![chlimage_1-164](assets/chlimage_1-164a.png)

1. En la pestaña **Enrutamiento**, especifique las acciones para la tarea. Para agregar varias acciones, toque o haga clic en el vínculo **Añadir elemento **link.

   ![chlimage_1-165](assets/chlimage_1-165a.png)

1. Después de agregar las opciones, haga clic en **Aceptar** para agregar los cambios al paso.

   >[!NOTE]
   Al tocar o hacer clic **Aceptar** no se guardan los cambios en el flujo de trabajo. Para guardar los cambios en el flujo de trabajo, toque o haga clic en **Guardar**.

1. Abra las tareas **Workflow** desde la barra lateral y agregue una tarea **Goto**.
1. Abra la tarea **Ir a** y toque o haga clic en la pestaña **Proceso**.
1. Especifique el código siguiente en el cuadro **Script**:

```
   function check() {

   if (workflowData.getMetaDataMap().get("lastTaskAction","") == "Reject All") {

   return true

   }

   // set copywriter user in metadata

   var previousId = workflowData.getMetaDataMap().get("lastTaskCompletedBy", "");

   workflowData.getMetaDataMap().put("copywriter", previousId);

   return false;

   }
```

>[!NOTE]
Para obtener más información sobre las secuencias de comandos en los pasos del flujo de trabajo, consulte [Definición de una regla para una división OR](/help/sites-developing/workflows-models.md).

![chlimage_1-166](assets/chlimage_1-166a.png)

1. Toque o haga clic **Aceptar**.

1. Toque o haga clic en **Guardar** para guardar el flujo de trabajo.

   ![chlimage_1-167](assets/chlimage_1-167a.png)

1. Una nueva tarea de aceptación del propietario del proyecto ahora aparece después de que [Mover a la tarea de producción](#move-to-production-task) se complete y se asigne al propietario.

   El usuario con la función de propietario puede completar la tarea y seleccionar una acción (de la lista de acciones añadidas a las opciones de configuración del paso del flujo de trabajo) en la lista de la ventana emergente de comentarios.

   ![chlimage_1-168](assets/chlimage_1-168a.png)

   Seleccione la opción adecuada y haga clic en **Completar** para ejecutar el **paso Ir a** en el flujo de trabajo.

>[!NOTE]
Cuando se inicio un servidor, el servlet de lista de tarea del proyecto almacena en caché las asignaciones entre tipos de tarea y direcciones URL definidas en `/libs/cq/core/content/projects/tasktypes`. A continuación, puede realizar la superposición habitual y agregar tipos de tarea personalizados colocándolos en `/apps/cq/core/content/projects/tasktypes`.

