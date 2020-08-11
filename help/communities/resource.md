---
title: Crear y asignar recursos de habilitación
seo-title: Crear y asignar recursos de habilitación
description: Añadir recursos de habilitación
seo-description: Añadir recursos de habilitación
uuid: da940242-0c9b-4ad8-8880-61fd41461c3b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8fe97181-600e-42ac-af25-d5d4db248740
translation-type: tm+mt
source-git-commit: e84c9a99ce9ec0447a5fb3e0ca5ba76b41c888cd
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 7%

---


# Crear y asignar recursos de habilitación {#create-and-assign-enablement-resources}

## Añadir un recurso de habilitación {#add-an-enablement-resource}

Para agregar un recurso de habilitación al nuevo sitio de comunidad:

* Inicie sesión como administrador del sistema en la instancia de creación:
   * Por ejemplo, [http://localhost:4502/](http://localhost:4503/)
* En la navegación global, seleccione **[!UICONTROL Comunidades]** > **[!UICONTROL Recursos]**

   ![medios](assets/resources.png)

   ![habilitación-recurso](assets/enablement-resource.png)
* Seleccione el sitio de la comunidad al que se agregan los recursos de habilitación:
   * Seleccione Tutorial **[!UICONTROL de habilitación]**.
* En el menú, seleccione **[!UICONTROL Crear]**.
* Seleccione **[!UICONTROL Recurso]**.

![create-resource](assets/create-enablement-resource.png)

### Información básica {#basic-info}

Rellene la información básica del recurso:

* **[!UICONTROL Nombre del sitio]**

   Establezca el nombre del sitio de comunidad seleccionado: Tutorial de habilitación

* **[!UICONTROL Nombre&amp;amp de recurso;ast;]**

   Lección de esquí 1

* **[!UICONTROL Etiquetas]**

   Tutorial: Deportes / Esquí

* **[!UICONTROL Mostrar en el catálogo]**

   Configúrelo en **Activado**.

* **[!UICONTROL Descripción]**

   Deslizar la nieve para principiantes.

* **[!UICONTROL Agregar imagen]**

   Añada una imagen para representar el recurso al miembro en su vista Asignaciones.

   ![basic-info](assets/basic-info.png)

* Seleccione **[!UICONTROL Siguiente]**

### Añadir contenido {#add-content}

Aunque parece que se pueden seleccionar varios recursos, solo se permite uno.

Seleccione el `'+' icon`, en la esquina superior derecha, para comenzar el proceso de selección del recurso identificando el origen.

![add-content](assets/add-content.png)

![upload-resource](assets/upload-resource.png)

Cargar un recurso. Si se trata de un recurso de vídeo, cargue una imagen personalizada para que se muestre antes de que se reproduzca el vídeo o permita que se genere una miniatura a partir del vídeo (puede tardar unos minutos; no es necesario esperar).

![upload-video](assets/upload-video.png)

* Seleccione **[!UICONTROL Siguiente]**.

### Configuración {#settings}

* **[!UICONTROL Entornos sociales]**

   Deje la configuración predeterminada para que los alumnos comenten y valoren los recursos de habilitación.

* **[!UICONTROL Fecha de vencimiento]**

   *(Opcional)* Se puede seleccionar una fecha para completar la asignación.

* **[!UICONTROL Autor del medio]**

   *(Opcional)* Deje en blanco.

* **[!UICONTROL Resource Contact&amp;ast;]**

   *(Requerido)* Utilice el menú desplegable para seleccionar un miembro `Quinn Harper`.

* **[!UICONTROL Experto de medios]**

   *(Opcional)* Deje en blanco.

   **Nota**: Si los usuarios o grupos no están visibles, compruebe que se han agregado al `Community Enable Members` grupo y que se han *guardado* en la instancia de publicación.

   ![habiliement-settings](assets/enablement-settings.png)

* Seleccione **[!UICONTROL Siguiente]**

### Asignaciones {#assignments}

* **[!UICONTROL Añadir usuarios asignados]**

   Deje sin configurar, ya que este recurso de habilitación se agregará a una ruta de aprendizaje. Si se asigna un alumno al recurso de habilitación individual, así como a una ruta de aprendizaje que contiene el recurso de habilitación, el alumno se asignará dos veces al recurso de habilitación.

   ![adiciones](assets/add-assignments.png)

* Seleccione **[!UICONTROL Crear]**

   ![create-resource](assets/create-resource.png)

La creación del recurso se realiza correctamente en la consola Recursos con el recurso recién creado seleccionado. Desde esta consola, es posible publicar, añadir alumnos y cambiar otros ajustes.

Para cargar una nueva versión del recurso de habilitación, se recomienda crear un nuevo recurso y, a continuación, anular la inscripción de los miembros de la versión anterior y matricularlos en la nueva versión.

### Publicar el recurso {#publish-the-resource}

Antes de que los alumnos matriculados puedan ver el recurso asignado, debe publicarse:

* Seleccione el icono mundial `Publish`

La activación se confirma con un mensaje de éxito:

![publish-resource](assets/publish-resource.png)

## Añadir un segundo recurso de habilitación {#add-a-second-enablement-resource}

Repita los pasos anteriores para crear y publicar un segundo recurso de habilitación relacionado desde el que se creará una ruta de aprendizaje.

![add-resource](assets/add-resource.png)

**Publique** el segundo recurso.

Vuelva a la lista de tutoriales de habilitación de sus recursos.

*Sugerencia: Si ambos recursos no están visibles, actualice la página.*

![refresh-resource](assets/refresh-resource.png)

## Añadir una ruta de aprendizaje {#add-a-learning-path}

Una ruta de aprendizaje es una agrupación lógica de recursos de habilitación que forman un curso.

* En la consola Recursos, seleccione `+ Create`
* Seleccionar ruta **[!UICONTROL de aprendizaje]**

![add-learning-path](assets/add-learning-path.png)

Añada la información **[!UICONTROL básica]**:

* **[!UICONTROL Nombre de la ruta de aprendizaje]**

   Clases de esquí

* **[!UICONTROL Etiquetas]**

   Tutorial: Esquí

* **[!UICONTROL Mostrar en el catálogo]**

   No marcar

* **[!UICONTROL Cargar una imagen]**

   Para representar la ruta de aprendizaje en la consola Recursos.

   ![learningPath-basic](assets/learningpath-basic.png)

* Seleccione **[!UICONTROL Siguiente]**.

Omita el panel siguiente, ya que no hay rutas de aprendizaje previas que agregar.

* Seleccione **[!UICONTROL Siguiente]**

En el panel Añadir recursos:

* Seleccione `+ Add Resources` para seleccionar los 2 recursos de lecturas de esquí que desea agregar a la ruta de aprendizaje.

   Nota: Solo se podrán seleccionar los recursos **publicados** .

>[!NOTE]
>
>Solo puede seleccionar los recursos disponibles en el mismo nivel que la ruta de aprendizaje. Por ejemplo, para una ruta de aprendizaje creada en un grupo, solo están disponibles los recursos de nivel de grupo; para una ruta de aprendizaje creada en un sitio de comunidad, los recursos de ese sitio están disponibles para agregarlos a la ruta de aprendizaje.


* Seleccione **[!UICONTROL Enviar]**.

   ![learningPath](assets/learningpath-add.png)

   ![create-learningPath](assets/create-learningpath.png)

* Seleccione **[!UICONTROL Siguiente]**

   ![learnPath-settings](assets/learningpath-settings.png)

* **[!UICONTROL Añadir usuarios asignados]**

   Utilice el menú desplegable para seleccionar el `Community Ski Class` grupo, que debe incluir miembros `Riley Taylor` y `Sidney Croft.`

* **[!UICONTROL Ruta de acceso de aprendizaje: Contact&amp;ast;]**

   *(Requerido)* Utilice el menú desplegable para seleccionar un miembro `Quinn Harper`.

* Seleccione **[!UICONTROL Crear]**.

   ![learnPath-info](assets/learningpath-info.png)

La creación correcta de la ruta de aprendizaje regresa a la consola Recursos con la ruta de aprendizaje recién creada seleccionada. Desde esta consola, es posible publicar, añadir alumnos y cambiar otros ajustes.

**Publique** la ruta de aprendizaje.

