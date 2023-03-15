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

## Añadir un medio de habilitación {#add-an-enablement-resource}

Para agregar un recurso de habilitación al nuevo sitio de la comunidad:

* Inicie sesión como administrador del sistema en la instancia de autor:
   * Por ejemplo, [http://localhost:4502/](http://localhost:4503/)
* En la navegación global, seleccione **[!UICONTROL Communities]** > **[!UICONTROL Recursos]**

   ![medios](assets/resources.png)

   ![enablement-resource](assets/enablement-resource.png)
* Seleccione el sitio de la comunidad al que se agregan los recursos de habilitación:
   * Seleccionar **[!UICONTROL Tutorial de habilitación]**.
* En el menú, seleccione **[!UICONTROL Crear]**.
* Seleccionar **[!UICONTROL Recurso]**.

![create-resource](assets/create-enablement-resource.png)

### Información básica {#basic-info}

Rellene la información básica del recurso:

* **[!UICONTROL Nombre del sitio]**

   Establezca con el nombre del sitio de comunidad seleccionado: Tutorial de habilitación

* **[!UICONTROL Nombre del recurso&amp;ast;]**

   Lección de esquí 1

* **[!UICONTROL Etiquetas]**

   Tutorial: Deportes / Esquí

* **[!UICONTROL Mostrar en el catálogo]**

   Configúrelo en. **Activado**.

* **[!UICONTROL Descripción]**

   Deslizamiento en la nieve para los principiantes.

* **[!UICONTROL Agregar imagen]**

   Agregue una imagen para representar el recurso ante el miembro en su vista Asignaciones.

   ![basic-info](assets/basic-info.png)

* Seleccione **[!UICONTROL Siguiente]**

### Añadir contenido {#add-content}

Aunque parezca que se pueden seleccionar varios recursos, solo se permite uno.

Seleccione el `'+' icon`, en la esquina superior derecha, para comenzar el proceso de selección del recurso identificando el origen.

![add-content](assets/add-content.png)

![upload-resource](assets/upload-resource.png)

Cargar un medio. Si se trata de un recurso de vídeo, cargue una imagen personalizada para mostrarla antes de que comience a reproducirse o permita que se genere una miniatura a partir del vídeo (puede tardar unos minutos; no es necesario esperar).

![upload-video](assets/upload-video.png)

* Seleccione **[!UICONTROL Siguiente]**.

### Configuración {#settings}

* **[!UICONTROL Entornos sociales]**

   Deje la configuración predeterminada para que los alumnos experimenten los comentarios y la clasificación de los recursos de habilitación.

* **[!UICONTROL Fecha de vencimiento]**

   *(Opcional)* Se puede seleccionar una fecha límite para finalizar la asignación.

* **[!UICONTROL Autor del medio]**

   *(Opcional)* Déjelo en blanco.

* **[!UICONTROL Contacto de medios&amp;ast;]**

   *(Obligatorio)* Utilice el menú desplegable para seleccionar un miembro `Quinn Harper`.

* **[!UICONTROL Experto de medios]**

   *(Opcional)* Déjelo en blanco.

   **Nota**: Si los usuarios o grupos no son visibles, compruebe que se agregaron al `Community Enable Members` grupo y *Guardado* en la instancia de publicación.

   ![enablement-settings](assets/enablement-settings.png)

* Seleccione **[!UICONTROL Siguiente]**

### Asignaciones {#assignments}

* **[!UICONTROL Añadir usuarios asignados]**

   Deje sin configurar, ya que este recurso de habilitación se agregará a una ruta de aprendizaje. Si se asigna un alumno al recurso de habilitación individual, así como una ruta de aprendizaje que contenga el recurso de habilitación, el alumno se asignará dos veces al recurso de habilitación.

   ![add-assignments](assets/add-assignments.png)

* Seleccione **[!UICONTROL Crear]**

   ![create-resource](assets/create-resource.png)

La creación correcta del recurso vuelve a la consola Recursos con el recurso recién creado seleccionado. Desde esta consola, es posible publicar, añadir alumnos y cambiar otras configuraciones.

Para cargar una nueva versión del recurso de habilitación, se recomienda crear un nuevo Recurso y luego dar de baja a los miembros de la versión antigua e inscribirlos en la nueva versión.

### Publicar el medio {#publish-the-resource}

Antes de que los inscritos puedan ver el recurso asignado, debe publicarse:

* Selecciona el mundo `Publish` icono

La activación se confirma con un mensaje de éxito:

![publish-resource](assets/publish-resource.png)

## Añadir un segundo recurso de habilitación {#add-a-second-enablement-resource}

Repita los pasos anteriores para crear y publicar un segundo recurso de habilitación relacionado desde el que se creará una ruta de aprendizaje.

![add-resource](assets/add-resource.png)

**Publish** el segundo recurso.

Vuelva a la lista del tutorial de habilitación de sus recursos.

*Sugerencia: Si ambos recursos no están visibles, actualice la página.*

![refresh-resource](assets/refresh-resource.png)

## Añadir una ruta de aprendizaje {#add-a-learning-path}

Una ruta de aprendizaje es una agrupación lógica de recursos de habilitación que forman un curso.

* En la consola Recursos, seleccione `+ Create`
* Seleccionar **[!UICONTROL Ruta de aprendizaje]**

![add-learning-path](assets/add-learning-path.png)

Añada el **[!UICONTROL Información básica]**:

* **[!UICONTROL Nombre de la ruta de aprendizaje]**

   Clases de esquí

* **[!UICONTROL Etiquetas]**

   Tutorial: Esquí

* **[!UICONTROL Mostrar en el catálogo]**

   Dejar sin marcar

* **[!UICONTROL Cargar una imagen]**

   Para representar la ruta de aprendizaje en la consola Recursos.

   ![learningpath-basic](assets/learningpath-basic.png)

* Seleccione **[!UICONTROL Siguiente]**.

Omita el siguiente panel, ya que no hay rutas de aprendizaje de requisitos previos que añadir.

* Seleccione **[!UICONTROL Siguiente]**

En el panel Añadir recursos:

* Seleccionar `+ Add Resources` para seleccionar los 2 recursos de sesiones de esquí que se añadirán a la ruta de aprendizaje.

   Nota: Solo **publicado** Se podrán seleccionar los recursos.

>[!NOTE]
>
>Solo puede seleccionar los recursos disponibles en el mismo nivel que la ruta de aprendizaje. Por ejemplo, para una ruta de aprendizaje creada en un grupo solo están disponibles los recursos de nivel de grupo; para una ruta de aprendizaje creada en un sitio de comunidad, los recursos de ese sitio están disponibles para añadirlos a la ruta de aprendizaje.

* Seleccione **[!UICONTROL Enviar]**.

   ![ruta de aprendizaje](assets/learningpath-add.png)

   ![create-learningpath](assets/create-learningpath.png)

* Seleccione **[!UICONTROL Siguiente]**

   ![learningpath-settings](assets/learningpath-settings.png)

* **[!UICONTROL Añadir usuarios asignados]**

   Utilice el menú desplegable para seleccionar `Community Ski Class` grupo, que debe incluir miembros `Riley Taylor` y `Sidney Croft.`

* **[!UICONTROL Contacto de ruta de aprendizaje&amp;ast;]**

   *(Obligatorio)* Utilice el menú desplegable para seleccionar un miembro `Quinn Harper`.

* Seleccione **[!UICONTROL Crear]**.

   ![learningpath-info](assets/learningpath-info.png)

La creación correcta de la ruta de aprendizaje vuelve a la consola Recursos con la ruta de aprendizaje recién creada seleccionada. Desde esta consola, es posible publicar, añadir alumnos y cambiar otras configuraciones.

**Publish** la ruta de aprendizaje.
