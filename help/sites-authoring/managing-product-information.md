---
title: Integración de Creative Project y PIM
description: Creative Project optimiza todo el flujo de trabajo de la sesión fotográfica, incluido la generación de una solicitud de sesión fotográfica, la carga de una sesión fotográfica, la colaboración en una sesión fotográfica y el empaquetado de recursos aprobados
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
exl-id: c4eff50e-0d55-4a61-98fd-cc42138656cb
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '2888'
ht-degree: 2%

---


# Integración de Creative Project y PIM {#creative-project-and-pim-integration}

Si es un experto en marketing o un profesional creativo, puede utilizar las herramientas de Creative Project en Adobe Experience Manager AEM () para administrar la fotografía de productos relacionada con el comercio electrónico y los procesos creativos asociados dentro de su organización.

Puede utilizar Creative Project para racionalizar las siguientes tareas en el flujo de trabajo de la sesión fotográfica:

* Generación de una solicitud de sesión fotográfica
* Carga de una sesión fotográfica
* Colaboración en una sesión fotográfica
* Empaquetando recursos aprobados

>[!NOTE]
>
>Consulte [Funciones de usuario del proyecto para obtener información](/help/sites-authoring/projects.md#user-roles-in-a-project) sobre la asignación de funciones de usuario y flujos de trabajo a determinados tipos de usuarios.

## Flujos de trabajo de sesión fotográfica del producto  {#exploring-product-photo-shoot-workflows}

Creative Project proporciona varias plantillas de proyecto para satisfacer los distintos requisitos del proyecto. El **Proyecto de sesión fotográfica del producto** La plantilla de está disponible de forma predeterminada. Esta plantilla incluye flujos de trabajo de sesión fotográfica que le permiten iniciar y administrar solicitudes de sesión fotográfica de productos. También incluye una serie de tareas que le permiten obtener imágenes digitales para los productos a través de procesos de revisión y aprobación adecuados.

## Crear un proyecto de sesión fotográfica de producto {#create-a-product-photo-shoot-project}

1. En el **Proyectos** consola, haga clic en **Crear** y luego elija **Crear proyecto** de la lista.

   ![Botón Crear proyecto](assets/chlimage_1-132a.png)

1. En el **Crear proyecto** , seleccione la **Proyecto de sesión fotográfica del producto** y haga clic en **Siguiente**.

   ![Asistente del proyecto](assets/chlimage_1-133a.png)

1. Escriba los detalles del proyecto, incluido el título, la descripción y la fecha de vencimiento. Agregue usuarios y asígneles diversas funciones. También puede agregar una miniatura para el proyecto.

   ![Detalles del proyecto](assets/chlimage_1-134a.png)

1. Haga clic en **Crear**. Un mensaje de confirmación notifica que se ha creado el proyecto.
1. Clic **Listo** para volver a la **Proyectos** consola. También puede hacer clic en **Abrir** para ver los recursos del proyecto.

## Iniciar el trabajo en un proyecto de sesión fotográfica de producto {#starting-work-in-a-product-photo-shoot-project}

Para iniciar una solicitud de sesión fotográfica, haga clic en un proyecto y luego en **Añadir trabajo** en la página de detalles del proyecto para iniciar un flujo de trabajo.

![Añadir trabajo](assets/chlimage_1-135a.png)

A **Proyecto de sesión fotográfica del producto** incluye los siguientes flujos de trabajo predeterminados:

* **Flujo de trabajo de la sesión fotográfica del producto (integración comercial)**: Este flujo de trabajo utiliza la integración comercial con el sistema de gestión de la información del producto (PIM) para generar automáticamente una lista de tomas para los productos seleccionados (jerarquía). Una vez completado el flujo de trabajo, puede ver los datos del producto como parte de los metadatos del recurso.
* **Flujo de trabajo de sesión fotográfica del producto**: Este flujo de trabajo permite proporcionar una lista de tomas en lugar de depender de la integración comercial. Asigna las imágenes cargadas a un archivo CSV en la carpeta de recursos del proyecto.

Utilice el **Sesión fotográfica del producto (integración comercial)** AEM flujo de trabajo para asignar recursos de imagen con los productos en la. Este flujo de trabajo utiliza la integración comercial para vincular las imágenes aprobadas a los datos de producto existentes en la ubicación `/etc/commerce`.

El **Sesión fotográfica del producto (integración comercial)** El flujo de trabajo de incluye las siguientes tareas:

* Crear lista de tomas
* Cargar sesión fotográfica
* Retocar la sesión fotográfica
* Revisar y aprobar
* Mover a la tarea de producción

AEM Si la información del producto no está disponible en la documentación de la aplicación, utilice la variable de configuración de la aplicación **Sesión fotográfica del producto** flujo de trabajo para asignar recursos de imagen a los productos en función de los detalles que cargue en un archivo CSV. El archivo CSV debe contener información básica del producto, como el ID del producto, la categoría y la descripción. El flujo de trabajo recupera los recursos aprobados para los productos.

Este flujo de trabajo incluye las siguientes tareas:

* Cargar lista de tomas
* Cargar sesión fotográfica
* Retocar la sesión fotográfica
* Revisar y aprobar
* Mover a la tarea de producción

Puede personalizar este flujo de trabajo mediante la opción de configuraciones del flujo de trabajo.

Ambos flujos de trabajo incluyen pasos para vincular productos con sus recursos aprobados. Cada flujo de trabajo incluye los siguientes pasos:

* Configuración del flujo de trabajo: describe las opciones para personalizar el flujo de trabajo
* Inicio de un flujo de trabajo de proyecto: explica cómo iniciar una sesión fotográfica del producto
* Detalles de tareas de flujo de trabajo: proporciona detalles de las tareas disponibles en el flujo de trabajo

## Seguimiento del progreso del proyecto {#tracking-project-progress}

Puede realizar un seguimiento del progreso de un proyecto controlando las tareas activas o completadas dentro de un proyecto.

Utilice lo siguiente para monitorizar el progreso de un proyecto:

* Tarjeta de tarea
* Lista de tareas

La tarjeta de tareas muestra el progreso general del proyecto. Aparece en la página de detalles del proyecto sólo si el proyecto tiene tareas relacionadas. La tarjeta de tareas muestra el estado de finalización actual del proyecto en función del número de tareas completadas. No incluye tareas futuras.

La tarjeta de tareas proporciona los siguientes detalles:

* Porcentaje de tareas activas
* Porcentaje de tareas completadas

![Tarjeta de tareas](assets/chlimage_1-136a.png)

La lista de tareas proporciona información detallada sobre la tarea de flujo de trabajo activa actualmente para el proyecto. Para mostrar la lista, haga clic en la tarjeta de tareas. La lista de tareas también muestra metadatos como la fecha de inicio, la fecha de vencimiento, el usuario asignado, la prioridad y el estado de la tarea.

![Lista de tareas](assets/chlimage_1-137a.png)

## Configuración del flujo de trabajo {#workflow-configuration}

Esta tarea implica asignar pasos del flujo de trabajo a los usuarios según sus funciones.

Para configurar la variable **Sesión fotográfica del producto** flujo de trabajo:

1. Vaya a **Herramientas** > **Flujos de trabajo** y, a continuación, seleccione **Modelos** mosaico para abrir **Modelos de flujo de trabajo** página.
1. Seleccione el **Sesión fotográfica del producto** y, a continuación, seleccione la variable **Editar** en la barra de herramientas para abrirlo en modo de edición.

   ![Modelo de sesión fotográfica del producto](assets/chlimage_1-138a.png)

1. En el **Flujo de trabajo de sesión fotográfica del producto** , abra una tarea de proyecto. Por ejemplo, abra el **Cargar lista de tomas** tarea.

   ![Editar modelo](assets/project-photo-shoot-workflow-model.png)

1. Haga clic en **Tarea** para configurar lo siguiente:

   * Nombre de la tarea
   * Usuario (función) predeterminado que recibe la tarea
   * Prioridad predeterminada de la tarea, que se muestra en la lista de tareas del usuario
   * Descripción de tarea que se mostrará cuando el usuario asignado abra la tarea
   * Fecha de vencimiento para una tarea, que se calcula según la hora en que se inició la tarea

1. Clic **OK** para guardar los ajustes de configuración.

Puede configurar las tareas adicionales para el **Sesión fotográfica del producto** flujo de trabajo de forma similar.

Siga los mismos pasos para configurar las tareas de la **Flujo de trabajo de la sesión fotográfica del producto (integración comercial)**.

## Iniciar un flujo de trabajo de proyecto {#starting-a-project-workflow}

En esta sección se describe cómo integrar la administración de la información del producto con el proyecto creativo.

1. Vaya al proyecto de sesión fotográfica de un producto y haga clic en **Añadir trabajo** en el menú **Flujos de trabajo** Tarjeta de.
1. Seleccione el **Sesión fotográfica del producto (integración comercial)** tarjeta de flujo de trabajo para iniciar **Sesión fotográfica del producto (integración comercial)** flujo de trabajo. Si la información del producto no está disponible en `/etc/commerce`, seleccione la **Sesión fotográfica del producto** flujo de trabajo e inicio del **Sesión fotográfica del producto** flujo de trabajo.

   ![Asistente de flujo de trabajo](assets/chlimage_1-140a.png)

1. Clic **Siguiente** para iniciar el flujo de trabajo en el proyecto.
1. Introduzca los detalles del flujo de trabajo en la página siguiente.

   ![Detalles del flujo de trabajo](assets/chlimage_1-141a.png)

1. Clic **Enviar** para iniciar el flujo de trabajo de la sesión fotográfica. Se muestra la página de detalles del proyecto para el proyecto de la sesión fotográfica.

   ![Página de proyecto con nuevo flujo de trabajo](assets/chlimage_1-142a.png)

### Detalles de tareas de flujo de trabajo {#workflow-tasks-details}

El flujo de trabajo de la sesión fotográfica incluye varias tareas. Cada tarea se asigna a un grupo de usuarios en función de la configuración definida para la tarea.

#### Crear tarea de lista de tomas {#create-shot-list-task}

El **Crear lista de tomas** Esta tarea permite al propietario del proyecto seleccionar productos para los que se requieren imágenes. En función de la opción seleccionada por el usuario, se genera un archivo CSV que contiene información básica del producto.

1. En la carpeta del proyecto, haga clic en el botón de puntos suspensivos en la parte inferior derecha de la [Tarjeta de tareas](#tracking-project-progress) para ver el elemento de tarea en el flujo de trabajo.

   ![Tarjeta de tareas](assets/chlimage_1-143a.png)

1. Seleccione el **Crear lista de tomas** y haga clic en el botón **Abrir** de la barra de herramientas.

   ![Abrir tarea de lista de tomas](assets/chlimage_1-144a.png)

1. Revise los detalles de la tarea y haga clic en **Crear lista de tomas** botón.

   ![Detalles de tarea de lista de tomas](assets/chlimage_1-145a.png)

1. Seleccione productos para los que existen datos de productos sin imágenes asociadas.

   ![Selección de productos](assets/chlimage_1-146a.png)

1. Haga clic en **Añadir a la lista de tomas** para crear un archivo CSV que contenga una lista de todos estos productos. Un mensaje confirma que la lista de tomas se ha creado para los productos seleccionados. Clic **Cerrar** para completar el flujo de trabajo.

1. Después de crear una lista de tomas, **Ver lista de tomas** aparece el vínculo. Para añadir más productos a la lista de tomas, haga clic en **Añadir a la lista de tomas**. En este caso, los datos se anexan a la lista de tomas creada inicialmente.

   ![Añadir a la lista de tomas](assets/chlimage_1-147a.png)

1. Clic **Ver lista de tomas** para ver la nueva lista de tomas.

   ![Ver lista de tomas](assets/chlimage_1-148a.png)

   Para editar los datos existentes o añadir nuevos datos, haga clic en **Editar** en la barra de herramientas. Solo el **Producto **y **Descripción** Los campos de son editables.

   ![Editar lista de tomas](assets/chlimage_1-149a.png)

   Después de actualizar el archivo, haga clic en **Guardar** en la barra de herramientas para guardar el archivo.

1. Después de añadir los productos, haga clic en **Completar** en el menú **Crear lista de tomas** página de detalles de la tarea para marcar la tarea como completada. Puede agregar un comentario opcional.

La finalización de la tarea introduce los siguientes cambios dentro del proyecto:

* Los recursos correspondientes a la jerarquía de productos se crean en una carpeta con el mismo nombre que el título del flujo de trabajo.
* Los metadatos de los recursos se pueden editar mediante la consola Recursos, incluso antes de que el fotógrafo proporcione las imágenes.
* Se crea una carpeta de sesión fotográfica que almacena las imágenes que proporciona el fotógrafo. La carpeta de la sesión fotográfica contiene subcarpetas para cada entrada de producto de la lista de tomas.

### Cargar tarea de lista de tomas {#upload-shot-list-task}

Esta tarea forma parte del flujo de trabajo Sesión fotográfica del producto. AEM Esta tarea se realiza si la información del producto no está disponible en el mercado de trabajo de la. En este caso, se carga una lista de productos en un archivo CSV para los que se requieren recursos de imagen. Según los detalles del archivo CSV, los recursos de imagen se asignan a los productos. El archivo debe ser un archivo CSV denominado `shotlist.csv`.

Utilice el **Ver lista de tomas** vínculo debajo de la tarjeta de proyecto en el procedimiento anterior para descargar un archivo CSV de ejemplo. Revise el archivo de muestra para conocer el contenido habitual de un archivo CSV.

La lista de productos o el archivo CSV pueden contener campos como **Categoría, Producto, Id, Descripción**, y **Ruta**. El **Id** El campo es obligatorio y contiene el ID de producto. Los demás campos son opcionales.

Un producto puede pertenecer a una categoría en particular. La categoría del producto se puede enumerar en el archivo CSV debajo de **Categoría** columna. El **Product** contiene el nombre del producto. En el **Descripción** , introduzca la descripción del producto o las instrucciones para el fotógrafo.

1. En la carpeta del proyecto, haga clic en el botón de puntos suspensivos en la parte inferior derecha de la [Tarjeta de tareas](#tracking-project-progress) para ver la lista de tareas del flujo de trabajo.
1. Seleccione el **Cargar lista de tomas** y haga clic en el botón **Abrir** de la barra de herramientas.

   ![Cargar lista de tomas](assets/chlimage_1-150a.png)

1. Revise los detalles de la tarea y haga clic en **Cargar lista de tomas** botón.

   ![Cargando lista de tomas](assets/chlimage_1-151a.png)

1. Haga clic en **Cargar lista de tomas** para cargar el archivo CSV. El flujo de trabajo reconoce este archivo como un origen que se utilizará para extraer los datos del producto para la siguiente tarea.
1. Cargue un archivo CSV que contenga información del producto en el formato adecuado. El **Ver recursos cargados** El vínculo aparece en la tarjeta de después de cargar el archivo CSV.

   ![Cargar información del producto](assets/chlimage_1-152a.png)

   Haga clic en **Completar** para completar la tarea.

1. Haga clic en **Completar** para completar la tarea.

### Cargar tarea de sesión fotográfica {#upload-photo-shoot-task}

Si es editor, puede cargar capturas de los productos enumerados en la **shotlist.csv** que se crea o se carga en la tarea anterior.

El nombre de las imágenes que se van a cargar debe comenzar por `<ProductId_>` donde `ProductId` se hace referencia a desde el **Id** en el campo `shotlist.csv` archivo. Por ejemplo, para un producto de la lista de tomas con **Id** `397122`, cargaría archivos con nombres `397122_highcontrast.jpg`, `397122_lowlight.png`, etc.

Puede cargar las imágenes directamente o cargar un archivo ZIP que contenga las imágenes. En función de sus nombres, las imágenes se colocan dentro de las respectivas carpetas de producto dentro de la carpeta de la sesión fotográfica.

1. En la carpeta del proyecto, haga clic en el botón de puntos suspensivos en la parte inferior derecha de la [Tarjeta de tarea](#tracking-project-progress) para ver el elemento de tarea en el flujo de trabajo.
1. Seleccione el **Cargar sesión fotográfica** y haga clic en el botón **Abrir** de la barra de herramientas.

   ![Cargar sesión fotográfica](assets/chlimage_1-153a.png)

1. Clic **Cargar sesión fotográfica** y cargue las imágenes de la sesión fotográfica.
1. Haga clic en **Completar** de la barra de herramientas para completar la tarea.

### Retocar tarea de sesión fotográfica {#retouch-photo-shoot-task}

Si tiene derechos de edición, realice la **Retocar la sesión fotográfica** para editar las imágenes cargadas en la carpeta de la sesión fotográfica.

1. En la carpeta del proyecto, haga clic en el botón de puntos suspensivos en la parte inferior derecha de la [Tarjeta de tarea](#tracking-project-progress) para ver el elemento de tarea en el flujo de trabajo.
1. Seleccione el **Retocar la sesión fotográfica** y haga clic en el botón **Abrir** de la barra de herramientas.

   ![Retocar sesión fotográfica](assets/chlimage_1-154a.png)

1. Haga clic en **Ver recursos cargados** vínculo en el **Retocar la sesión fotográfica** para examinar las imágenes cargadas.

   ![Ver recursos cargados](assets/chlimage_1-155a.png)

   Si es necesario, edite las imágenes mediante una aplicación de Adobe Creative Cloud.

   ![Editar recurso](assets/chlimage_1-156a.png)

1. Haga clic en **Completar** de la barra de herramientas para completar la tarea.

### Revisar y aprobar la tarea {#review-and-approve-task}

En esta tarea, se revisan las imágenes de la sesión fotográfica cargadas por un fotógrafo y se marcan las imágenes como aprobadas para su uso.

1. En la carpeta del proyecto, haga clic en el botón de puntos suspensivos en la parte inferior derecha de la [Tarjeta de tarea](#tracking-project-progress) para ver el elemento de tarea en el flujo de trabajo.
1. Seleccione el **Revisar y aprobar** y haga clic en el botón **Abrir** de la barra de herramientas.

   ![Revisar y aprobar](assets/chlimage_1-157a.png)

1. En el **Revisar y aprobar** , asigne la tarea de revisión a un rol y haga clic en **Revisar** para empezar a revisar las imágenes de producto cargadas.

   ![Empezar a revisar recursos](assets/chlimage_1-158a.png)

1. Seleccione una imagen de producto y haga clic en **Aprobar** en la barra de herramientas para marcarlo como aprobado. Una vez aprobada una imagen, aparece un banner aprobado sobre ella.

   ![Aprobación de una imagen](assets/chlimage_1-159a.png)

1. Clic **Completar**. Las imágenes aprobadas se vinculan con los recursos vacíos creados.

Puede omitir algunos productos sin ninguna imagen. Más adelante, puede volver a visitar la tarea y marcarla como completada una vez completada.

Puede navegar a los recursos del proyecto mediante la interfaz de usuario de Assets y comprobar las imágenes aprobadas.

Haga clic en el nivel siguiente para ver los productos según la jerarquía de datos del producto.

Creative Project asocia los recursos aprobados con el producto de referencia. Los metadatos del recurso se actualizan con la referencia del producto y la información básica en la **Datos del producto** AEM en las propiedades del recurso, aparecen en la sección Metadatos del recurso de la.

>[!NOTE]
>
>En el **Flujo de trabajo de sesión fotográfica del producto** (sin integración comercial), las imágenes aprobadas no tienen ninguna asociación con los productos.

### Mover a la tarea de producción {#move-to-production-task}

Esta tarea mueve los recursos aprobados a la carpeta lista para la producción para que estén disponibles para su uso.

1. En la carpeta del proyecto, haga clic en el botón de puntos suspensivos en la parte inferior derecha de la [Tarjeta de tarea](#tracking-project-progress) para ver el elemento de tarea en el flujo de trabajo.
1. Seleccione el **Mover a producción** y haga clic en el botón **Abrir** de la barra de herramientas.

   ![Mover a producción](assets/chlimage_1-160a.png)

1. Para ver los recursos aprobados para la sesión fotográfica antes de moverlos a la carpeta production ready, haga clic en **Ver recursos aprobados** vínculo debajo de la miniatura del proyecto en la **Mover a producción** página de tareas.

   ![Mover a la página de tareas de producción](assets/chlimage_1-161a.png)

1. Introduzca la ruta de la carpeta lista para la producción en la **Mover a** field.

   ![Mover a ruta](assets/chlimage_1-162a.png)

1. Clic **Mover a producción**. Cierre el mensaje de confirmación. Los recursos se mueven a la ruta mencionada y se crea automáticamente un conjunto de giros para los recursos aprobados para cada producto en función de la jerarquía de carpetas.

1. Haga clic en **Completar** de la barra de herramientas. El flujo de trabajo se completa cuando el último paso se marca como completado.

## Visualización de metadatos de recursos DAM {#viewing-dam-asset-metadata}

Después de la aprobación, los recursos se vinculan a los productos correspondientes. El [Página Propiedades](/help/assets/manage-assets.md#editing-properties) de los recursos aprobados ahora tiene un **Datos del producto** pestaña (información de producto vinculada). Esta pestaña muestra los detalles del producto, el número de SKU y otros detalles relacionados con el producto que vinculan el recurso. Haga clic en **Editar** para actualizar una propiedad de recurso. La información relacionada con el producto sigue siendo de solo lectura.

Haga clic en el vínculo que aparece para desplazarse a la página de detalles del producto correspondiente en la consola de producto con la que está asociado el recurso.

## Personalizar los flujos de trabajo de sesión fotográfica del proyecto {#customizing-the-project-photo-shoot-workflows}

Puede personalizar la variable **Sesión fotográfica del proyecto** flujos de trabajo basados en sus necesidades. Es una tarea opcional basada en funciones que se realiza para establecer el valor de una variable dentro del proyecto. Posteriormente, puede utilizar el valor configurado para llegar a una decisión.

1. AEM Haga clic en el logotipo de la y, a continuación, vaya a **Herramientas** > **Flujo de trabajo** > **Modelos** para abrir **Modelos de flujo de trabajo** página.
1. Seleccione el **Sesión fotográfica del producto (integración comercial)** flujo de trabajo para **Sesión fotográfica del producto** flujo de trabajo y clic **Editar** en la barra de herramientas para abrir el flujo de trabajo en modo de edición.
1. Abra el panel lateral y busque **Crear tarea de proyecto basada en roles** y arrástrelo al flujo de trabajo.

   ![Crear tarea de proyecto basada en roles](assets/project-model-role-based.png)

1. Abra el **Tarea basada en roles** paso.
1. En el **Tarea** pestaña, proporcione un nombre para la tarea que se mostrará en la lista de tareas. También puede asignar la tarea a un rol, establecer la prioridad predeterminada, proporcionar una descripción y especificar una hora en la que vence la tarea.

   ![Configuración del paso de flujo de trabajo](assets/project-task-step.png)

1. En el **Enrutamiento** , especifique las acciones de la tarea. Para añadir varias acciones, haga clic en el **Agregar elemento** vínculo.

   ![Ficha Routing](assets/project-task-step-routing.png)

1. Después de añadir las opciones, haga clic en **OK** para agregar los cambios al paso.

1. De nuevo en **Modelo de flujo de trabajo** clic de ventana **Sincronización** para guardar los cambios de todo el flujo de trabajo. Toque o haga clic **OK** para el paso no guarda los cambios en el flujo de trabajo. Para guardar los cambios en el flujo de trabajo, haga clic en **Sincronización**.

1. Abra el panel lateral y busque **Paso Ir a** y arrástrelo al flujo de trabajo.

1. Abra el **Ir a** y haga clic en **Proceso** pestaña.

1. Seleccione el **Paso de destino** para ir a y especificar que la variable **Expresión de enrutamiento** es un script ECMA. A continuación, proporcione el siguiente código en **Script** campo:

   ```javascript
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

   >[!TIP]
   >
   >Para obtener más información sobre los scripts en los pasos del flujo de trabajo, consulte [Definición de una regla para una división O](/help/sites-developing/workflows-models.md).

   ![Ir a script](assets/project-workflow-goto.png)

1. Haz clic en **OK**.

1. Clic **Sincronización** para guardar el flujo de trabajo.

Ahora aparece una nueva tarea después de [Mover a la tarea de producción](#move-to-production-task) se completa y se asigna al propietario.

El usuario en la **Propietario** Esta función puede completar la tarea y seleccionar una acción (de la lista de acciones añadidas en las configuraciones de paso del flujo de trabajo) en la lista de la ventana emergente de comentarios.

>[!NOTE]
>
>Cuando se inicia un servidor, el servlet de lista de tareas de Project almacena en caché las asignaciones entre tipos de tareas y direcciones URL definidas en `/libs/cq/core/content/projects/tasktypes`. A continuación, puede realizar la superposición habitual y agregar tipos de tareas personalizadas colocándolos debajo de `/apps/cq/core/content/projects/tasktypes`.
