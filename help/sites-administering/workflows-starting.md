---
title: Inicio de flujos de trabajo
seo-title: Starting Workflows
description: AEM Obtenga información sobre cómo iniciar flujos de trabajo de en la.
seo-description: Learn how to start Workflows in AEM.
uuid: 0648d335-ecce-459d-95fd-3d4d76181b32
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: e9ab4796-a050-40de-b073-af7d33cff009
exl-id: 84a1964c-4121-4763-b946-9eee6093747d
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 6%

---

# Inicio de flujos de trabajo{#starting-workflows}

Al administrar flujos de trabajo, puede iniciarlos mediante diversos métodos:

* Manualmente:

   * Desde una [Modelo de flujo de trabajo](#workflow-models).
   * Uso de un paquete de flujo de trabajo para [procesamiento por lotes](#workflow-packages-for-batch-processing).

* Automáticamente:

   * En respuesta a cambios de nodo; [Uso de un lanzador](#workflows-launchers).

>[!NOTE]
>
>Otros métodos también están disponibles para los autores; para obtener más información, consulte:
>
>* [Aplicación de flujos de trabajo a páginas](/help/sites-authoring/workflows-applying.md)
>* [Cómo aplicar flujos de trabajo a recursos DAM](/help/assets/assets-workflow.md)
>* [AEM Forms](https://helpx.adobe.com/aem-forms/6-2/aem-workflows-submit-process-form.html)
>* [Proyectos de traducción](/help/sites-administering/tc-manage.md)
>


## Modelos de flujo de trabajo {#workflow-models}

Puede iniciar un flujo de trabajo [basado en uno de los modelos](/help/sites-administering/workflows.md#workflow-models-and-instances) en la consola Modelos de flujo de trabajo. La única información obligatoria es la carga útil, aunque también se puede añadir un título o un comentario.

## Iniciadores de flujos de trabajo {#workflows-launchers}

El iniciador del flujo de trabajo supervisa los cambios en el repositorio de contenido para iniciar flujos de trabajo que dependen de la ubicación y el tipo de recurso del nodo modificado.

Uso del **Lanzador** puede:

* Consulte los flujos de trabajo ya iniciados para nodos específicos.
* Seleccione un flujo de trabajo que iniciar cuando se haya creado, modificado o eliminado un determinado tipo de nodo o nodo.
* Elimine una relación existente entre flujo de trabajo y nodo.

Se puede crear un lanzador para cualquier nodo. Sin embargo, los cambios en ciertos nodos no inician flujos de trabajo. Los cambios en los nodos de las siguientes rutas no hacen que se inicien los flujos de trabajo:

* `/var/workflow/instances`
* Cualquier nodo de bandeja de entrada de flujo de trabajo ubicado en cualquier parte del `/home/users` ramificación
* `/tmp`
* `/var/audit`
* `/var/classes`
* `/var/eventing`
* `/var/linkchecker`
* `/var/mobile`
* `/var/statistics`

   * Excepción: cambios en los nodos siguientes `/var/statistics/tracking` *hacer* iniciar flujos de trabajo.

La instalación estándar incluye varias definiciones. Se utilizan para tareas de colaboración social y administración de activos digitales:

![wf-100](assets/wf-100.png)

## Paquetes de flujo de trabajo para procesamiento por lotes {#workflow-packages-for-batch-processing}

Los paquetes de flujo de trabajo son paquetes que se pueden pasar a un flujo de trabajo como carga útil para su procesamiento, lo que permite procesar varios recursos.

Un paquete de flujo de trabajo:

* contiene vínculos a un conjunto de recursos (como páginas o recursos).
* contiene información del paquete, como la fecha de creación, el usuario que lo creó y una breve descripción.
* se define mediante una plantilla de página especializada; estas páginas permiten al usuario especificar los recursos del paquete.
* se puede utilizar varias veces.
* el usuario puede cambiarlo (añadir o quitar recursos) mientras la instancia de flujo de trabajo se está ejecutando.

## Inicio de un flujo de trabajo desde la consola Modelos {#starting-a-workflow-from-the-models-console}

1. Vaya a **Modelos** consola con **Herramientas**, **Flujo de trabajo**, entonces **Modelos**.
1. Seleccione el flujo de trabajo (según la vista de la consola); también puede utilizar Buscar (parte superior izquierda) si es necesario:

   ![wf-103](assets/wf-103.png)

   >[!NOTE]
   >
   >El **[Transitorio](/help/sites-developing/workflows.md#transient-workflows)** El indicador muestra los flujos de trabajo para los que no se mantendrá el historial del flujo de trabajo.

1. Seleccionar **Iniciar flujo de trabajo** en la barra de herramientas.
1. Se abrirá el cuadro de diálogo Ejecutar flujo de trabajo, que le permitirá especificar lo siguiente:

   * **Carga útil**

      Puede ser una página, un nodo, un recurso o un paquete, entre otros recursos.

   * **Título**

      Un título opcional para ayudar a identificar esta instancia.

   * **Comentar**

      Un comentario opcional para indicar los detalles de esta instancia.
   ![wf-104](assets/wf-104.png)

## Creación de una configuración de lanzador {#creating-a-launcher-configuration}

1. Vaya a **Iniciadores de flujo de trabajo** consola con **Herramientas**, **Flujo de trabajo**, entonces **Lanzadores**.
1. Seleccionar **Crear**, entonces **Añadir lanzador** para abrir el cuadro de diálogo:

   ![wf-105](assets/wf-105.png)

   * **Tipo de evento**

      El tipo de evento que iniciará el flujo de trabajo:

      * Creado
      * Modificado
      * Eliminado
   * **Tipo de nodo**

      El tipo de nodo al que se aplica el iniciador del flujo de trabajo.

   * **Ruta**

      Ruta de acceso a la que se aplica el iniciador del flujo de trabajo.

   * **Modo(s) de ejecución**

      El tipo de servidor al que se aplica el iniciador del flujo de trabajo. Seleccionar **Autor**, **Publish**, o **Crear y publicar**.

   * **Condiciones**

      Una lista de condiciones para valores de nodo que, al evaluarse, determinan si se inicia el flujo de trabajo. Por ejemplo, la siguiente condición hace que el flujo de trabajo se inicie cuando el nodo tenga un nombre de propiedad con el valor Usuario:

      name==User

   * **Características**

      Lista de funciones que se van a habilitar. Seleccione las funciones necesarias mediante el selector desplegable.

   * **Funciones desactivadas**

   Lista de funciones que se van a deshabilitar. Seleccione las funciones necesarias mediante el selector desplegable.

   * **Modelo de flujo de trabajo**

      Flujo de trabajo que se inicia cuando se produce el tipo de evento en el tipo de nodo o la ruta de acceso bajo la condición definida.

   * **Descripción**

      Su propio texto para describir e identificar la configuración del lanzador.

   * **Activar**

      Controla si el lanzador del flujo de trabajo está activado:

      * Seleccionar **Activar** para iniciar flujos de trabajo cuando se cumplan las propiedades de configuración.
      * Seleccionar **Deshabilitar** cuando el flujo de trabajo no debe ejecutarse (ni siquiera cuando se cumplan las propiedades de configuración).
   * **Lista de exclusiones**

      Esto especifica los eventos JCR que se deben excluir (es decir, ignorar) al determinar si se debe activar un flujo de trabajo.

      Esta propiedad del lanzador es una lista de elementos separados por comas:&quot;

      * `property-name` ignorar cualquiera `jcr` evento que se activó en el nombre de propiedad especificado. &quot;
      * `event-user-data:<*someValue*>` pasa por alto cualquier evento que contenga `*<someValue*`> `user-data` configurar a través de [ `ObservationManager` API](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/observation/ObservationManager.html#setUserData(java.lang.String.

      Por ejemplo:

      `jcr:lastModified,dc:modified,dc:format,jcr:lastModifiedBy,imageMap,event-user-data:changedByWorkflowProcess`

      Esta función se puede utilizar para ignorar cualquier cambio activado por otro proceso de flujo de trabajo añadiendo el elemento de exclusión:

      `event-user-data:changedByWorkflowProcess`





1. Seleccionar **Crear**, para crear el lanzador y volver a la consola.

   Una vez que se produzca el evento correspondiente, el iniciador se activará y se iniciará el flujo de trabajo.

## Administración de una configuración de lanzador {#managing-a-launcher-configuration}

Una vez creada la configuración del iniciador, puede utilizar la misma consola para seleccionar la instancia y, a continuación, **Ver propiedades** (y editarlos) o **Eliminar**.
