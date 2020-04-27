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
source-git-commit: 62f2a11491e427a13cecae75c225ed41a44783cd

---


# Crear y asignar recursos de habilitación {#create-and-assign-enablement-resources}

## Añadir un recurso de habilitación {#add-an-enablement-resource}

Para agregar un recurso de habilitación al nuevo sitio de comunidad:

* Inicie sesión como administrador del sistema en la instancia de creación:
   * Por ejemplo, [http://localhost:4502/](http://localhost:4503/)
* En la navegación global, seleccione **[!UICONTROL Comunidades]** > **[!UICONTROL Recursos]**

   ![chlimage_1-199](assets/chlimage_1-199.png)

   ![chlimage_1-200](assets/chlimage_1-200.png)
* Seleccione el sitio de la comunidad al que se agregan los recursos de habilitación:
   * Seleccione Tutorial **[!UICONTROL de habilitación]**.
* En el menú, seleccione **[!UICONTROL Crear]**.
* Seleccione **[!UICONTROL Recurso]**.

![chlimage_1-201](assets/chlimage_1-201.png)

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

   ![chlimage_1-202](assets/chlimage_1-202.png)

* Seleccione **[!UICONTROL Siguiente]**

### Añadir contenido {#add-content}

Aunque parece que se pueden seleccionar varios recursos, solo se permite uno.

Seleccione el `'+' icon`, en la esquina superior derecha, para comenzar el proceso de selección del recurso identificando el origen.

![chlimage_1-203](assets/chlimage_1-203.png) ![chlimage_1-204](assets/chlimage_1-204.png)

Cargar un recurso. Si se trata de un recurso de vídeo, cargue una imagen personalizada para que se muestre antes de que se reproduzca el vídeo o permita que se genere una miniatura a partir del vídeo (puede tardar unos minutos; no es necesario esperar).

![chlimage_1-206](assets/chlimage_1-205.png)

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

   ![chlimage_1-205](assets/chlimage_1-206.png)

* Seleccione **[!UICONTROL Siguiente]**

### Asignaciones {#assignments}

* **[!UICONTROL Añadir usuarios asignados]**

   Deje sin configurar, ya que este recurso de habilitación se agregará a una ruta de aprendizaje. Si se asigna un alumno al recurso de habilitación individual, así como a una ruta de aprendizaje que contiene el recurso de habilitación, el alumno se asignará dos veces al recurso de habilitación.

   ![chlimage_1-207](assets/chlimage_1-207.png)

* Seleccione **[!UICONTROL Crear]**

   ![chlimage_1-208](assets/chlimage_1-208.png)

La creación del recurso se realiza correctamente en la consola Recursos con el recurso recién creado seleccionado. Desde esta consola, es posible publicar, añadir alumnos y cambiar otros ajustes.

Para cargar una nueva versión del recurso de habilitación, se recomienda crear un nuevo recurso y, a continuación, anular la inscripción de los miembros de la versión anterior y matricularlos en la nueva versión.

### Publicar el recurso {#publish-the-resource}

Antes de que los alumnos matriculados puedan ver el recurso asignado, debe publicarse:

* Seleccione el icono mundial `Publish`

La Activación se confirma con un mensaje de éxito:

![chlimage_1-209](assets/chlimage_1-209.png)

## Añadir un segundo recurso de habilitación {#add-a-second-enablement-resource}

Repita los pasos anteriores para crear y publicar un segundo recurso de habilitación relacionado desde el que se creará una ruta de aprendizaje.

![chlimage_1-210](assets/chlimage_1-210.png)

**Publique** el segundo recurso.

Vuelva a la lista de tutoriales de habilitación de sus recursos.

*Sugerencia: Si ambos recursos no están visibles, actualice la página.*

![chlimage_1-211](assets/chlimage_1-211.png)

## Añadir una ruta de aprendizaje {#add-a-learning-path}

Una ruta de aprendizaje es una agrupación lógica de recursos de habilitación que forman un curso.

* En la consola Recursos, seleccione `+ Create`
* Seleccionar ruta **[!UICONTROL de aprendizaje]**

![chlimage_1-212](assets/chlimage_1-212.png)

Añada la información **[!UICONTROL básica]**:

* **[!UICONTROL Nombre de la ruta de aprendizaje]**

   Clases de esquí

* **[!UICONTROL Etiquetas]**

   Tutorial: Esquí

* **[!UICONTROL Mostrar en el catálogo]**

   No marcar

* **[!UICONTROL Cargar una imagen]**

   Para representar la ruta de aprendizaje en la consola Recursos.

   ![chlimage_1-213](assets/chlimage_1-213.png)

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

   ![chlimage_1-214](assets/chlimage_1-214.png)

   ![chlimage_1-215](assets/chlimage_1-215.png)

* Seleccione **[!UICONTROL Siguiente]**

   ![chlimage_1-216](assets/chlimage_1-216.png)

* **[!UICONTROL Añadir usuarios asignados]**

   Utilice el menú desplegable para seleccionar el `Community Ski Class` grupo, que debe incluir miembros `Riley Taylor` y `Sidney Croft.`

* **[!UICONTROL Ruta de acceso de aprendizaje: Contact&amp;ast;]**

   *(Requerido)* Utilice el menú desplegable para seleccionar un miembro `Quinn Harper`.

* Seleccione **[!UICONTROL Crear]**.

   ![chlimage_1-217](assets/chlimage_1-217.png)

La creación correcta de la ruta de aprendizaje regresa a la consola Recursos con la ruta de aprendizaje recién creada seleccionada. Desde esta consola, es posible publicar, añadir alumnos y cambiar otros ajustes.

**Publique** la ruta de aprendizaje.

