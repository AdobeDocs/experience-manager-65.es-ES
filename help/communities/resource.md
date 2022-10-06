---
title: Crear y asignar recursos de habilitación
seo-title: Create and Assign Enablement Resources
description: Añadir recursos de habilitación
seo-description: Add enablement resources
uuid: da940242-0c9b-4ad8-8880-61fd41461c3b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8fe97181-600e-42ac-af25-d5d4db248740
exl-id: 78908a9c-a260-44ff-ad1e-baa6d78ae399
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 7%

---

# Crear y asignar recursos de habilitación {#create-and-assign-enablement-resources}

## Agregar un recurso de habilitación {#add-an-enablement-resource}

Para agregar un recurso de habilitación al nuevo sitio de la comunidad:

* Inicie sesión como administrador del sistema en la instancia de autor:
   * Por ejemplo, [http://localhost:4502/](http://localhost:4503/)
* En la navegación global, seleccione **[!UICONTROL Comunidades]** > **[!UICONTROL Recursos]**

   ![medios](assets/resources.png)

   ![enablement-resource](assets/enablement-resource.png)
* Seleccione el sitio de la comunidad al que se agregarán los recursos de habilitación:
   * Select **[!UICONTROL Tutorial de habilitación]**.
* En el menú , seleccione **[!UICONTROL Crear]**.
* Select **[!UICONTROL Recurso]**.

![create-resource](assets/create-enablement-resource.png)

### Información básica {#basic-info}

Complete la información básica del recurso:

* **[!UICONTROL Nombre del sitio]**

   Configúrelo en el nombre del sitio de comunidad seleccionado: Tutorial de habilitación

* **[!UICONTROL Nombre&amp;ast de recurso;]**

   Lección de esquí 1

* **[!UICONTROL Etiquetas]**

   Tutorial: Deportes / esquí

* **[!UICONTROL Mostrar en el catálogo]**

   Configúrelo en **Activado**.

* **[!UICONTROL Descripción]**

   Corriendo nieve para principiantes.

* **[!UICONTROL Agregar imagen]**

   Agregue una imagen para representar el recurso al miembro en la vista Asignaciones.

   ![basic-info](assets/basic-info.png)

* Seleccione **[!UICONTROL Siguiente]**

### Añadir contenido {#add-content}

Aunque aparece como si se pudieran seleccionar varios recursos, solo se permite uno.

Seleccione el `'+' icon`, en la esquina superior derecha, para comenzar el proceso de selección del recurso identificando el origen.

![add-content](assets/add-content.png)

![upload-resource](assets/upload-resource.png)

Cargar un recurso. Si se usa un recurso de vídeo, cargue una imagen personalizada para que se muestre antes de que se inicie la reproducción del vídeo o permita que se genere una miniatura a partir del vídeo (puede tardar unos minutos, no es necesario esperar).

![upload-video](assets/upload-video.png)

* Seleccione **[!UICONTROL Siguiente]**.

### Configuración {#settings}

* **[!UICONTROL Entornos sociales]**

   Deje la configuración predeterminada para experimentar comentarios y clasificaciones de los recursos de habilitación por parte de los alumnos.

* **[!UICONTROL Fecha de vencimiento]**

   *(Opcional)* Se puede seleccionar una fecha en la que se debe completar la asignación.

* **[!UICONTROL Autor del medio]**

   *(Opcional)* Deje en blanco.

* **[!UICONTROL Contacto&amp;ast de recursos;]**

   *(Obligatorio)* Utilice el menú desplegable para seleccionar un miembro `Quinn Harper`.

* **[!UICONTROL Experto de medios]**

   *(Opcional)* Deje en blanco.

   **Nota**: Si los usuarios o grupos no están visibles, compruebe que se añadieron al informe `Community Enable Members` grupo y *Guardado* en la instancia de publicación.

   ![enablement-settings](assets/enablement-settings.png)

* Seleccione **[!UICONTROL Siguiente]**

### Asignaciones {#assignments}

* **[!UICONTROL Añadir usuarios asignados]**

   Deje sin configurar, ya que este recurso de habilitación se agregará a una ruta de aprendizaje. Si se asigna un alumno al recurso de habilitación individual, así como a una ruta de aprendizaje que contenga el recurso de habilitación, el alumno se asignará dos veces al recurso de habilitación.

   ![asignaciones adicionales](assets/add-assignments.png)

* Seleccione **[!UICONTROL Crear]**

   ![create-resource](assets/create-resource.png)

La creación correcta del recurso vuelve a la consola Recursos con el recurso recién creado seleccionado. Desde esta consola, es posible publicar, añadir estudiantes y cambiar otras configuraciones.

Para cargar una nueva versión del recurso de habilitación, se recomienda crear un nuevo recurso y, a continuación, anular la inscripción de miembros de la versión antigua e inscribirlos en la nueva versión.

### Publicar el recurso {#publish-the-resource}

Antes de que los alumnos puedan ver el recurso asignado, debe publicarse:

* Seleccionar el mundo `Publish` icono

La activación se confirma con un mensaje de éxito:

![publish-resource](assets/publish-resource.png)

## Agregar un segundo recurso de habilitación {#add-a-second-enablement-resource}

Repita los pasos anteriores para crear y publicar un segundo recurso de habilitación relacionado desde el que se creará una ruta de aprendizaje.

![add-resource](assets/add-resource.png)

**Publicación** el segundo recurso.

Vuelva a la lista de tutoriales de habilitación de sus recursos.

*Sugerencia: Si ambos recursos no están visibles, actualice la página.*

![actualizar-recurso](assets/refresh-resource.png)

## Agregar una ruta de aprendizaje {#add-a-learning-path}

Una ruta de aprendizaje es una agrupación lógica de recursos de habilitación que forman un curso.

* En la consola Recursos, seleccione `+ Create`
* Select **[!UICONTROL Ruta de aprendizaje]**

![add-learning-path](assets/add-learning-path.png)

Agregue la variable **[!UICONTROL Información básica]**:

* **[!UICONTROL Nombre de la ruta de aprendizaje]**

   Lecciones de esquí

* **[!UICONTROL Etiquetas]**

   Tutorial: Esquí

* **[!UICONTROL Mostrar en el catálogo]**

   Dejar sin marcar

* **[!UICONTROL Cargar una imagen]**

   Para representar la ruta de aprendizaje en la consola Recursos.

   ![learningPath-basic](assets/learningpath-basic.png)

* Seleccione **[!UICONTROL Siguiente]**.

Omita el panel siguiente, ya que no hay rutas de aprendizaje previas que añadir.

* Seleccione **[!UICONTROL Siguiente]**

En el panel Agregar recursos:

* Select `+ Add Resources` para seleccionar los recursos de las 2 lecciones de esquí que se agregarán a la ruta de aprendizaje.

   Nota: Solo **publicado** Los recursos se pueden seleccionar.

>[!NOTE]
>
>Solo puede seleccionar los recursos disponibles en el mismo nivel que la ruta de aprendizaje. Por ejemplo, para una ruta de aprendizaje creada en un grupo solo están disponibles los recursos de nivel de grupo; para una ruta de aprendizaje creada en un sitio de comunidad, los recursos de ese sitio están disponibles para añadirlos a la ruta de aprendizaje.

* Seleccione **[!UICONTROL Enviar]**.

   ![ruta de aprendizaje](assets/learningpath-add.png)

   ![create-learningPath](assets/create-learningpath.png)

* Seleccione **[!UICONTROL Siguiente]**

   ![aprendizaje de la configuración de ruta](assets/learningpath-settings.png)

* **[!UICONTROL Añadir usuarios asignados]**

   Utilice el menú desplegable para seleccionar la variable `Community Ski Class` grupo, que debería incluir miembros `Riley Taylor` y `Sidney Croft.`

* **[!UICONTROL Ruta de aprendizaje Contacto&amp;ast;]**

   *(Obligatorio)* Utilice el menú desplegable para seleccionar un miembro `Quinn Harper`.

* Seleccione **[!UICONTROL Crear]**.

   ![aprendizaje de la ruta-información](assets/learningpath-info.png)

La creación correcta de la ruta de aprendizaje vuelve a la consola Recursos con la ruta de aprendizaje recién creada seleccionada. Desde esta consola, es posible publicar, añadir estudiantes y cambiar otras configuraciones.

**Publicación** la ruta de aprendizaje.
