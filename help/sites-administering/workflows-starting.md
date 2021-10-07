---
title: Inicio de flujos de trabajo
seo-title: Starting Workflows
description: Aprenda a iniciar Flujos de trabajo en AEM.
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

   * Desde un [Modelo de flujo de trabajo](#workflow-models).
   * Uso de un paquete de flujo de trabajo para [procesamiento por lotes](#workflow-packages-for-batch-processing).

* Automáticamente:

   * En respuesta a los cambios de nodo; [usando un Iniciador](#workflows-launchers).

>[!NOTE]
>
>También hay otros métodos disponibles para los autores; para obtener más información, consulte:
>
>* [Aplicación de flujos de trabajo a páginas](/help/sites-authoring/workflows-applying.md)
>* [Cómo aplicar flujos de trabajo a recursos DAM](/help/assets/assets-workflow.md)
>* [AEM Forms](https://helpx.adobe.com/aem-forms/6-2/aem-workflows-submit-process-form.html)
>* [Proyectos de traducción](/help/sites-administering/tc-manage.md)

>


## Modelos de flujo de trabajo {#workflow-models}

Puede iniciar un flujo de trabajo [basado en uno de los modelos](/help/sites-administering/workflows.md#workflow-models-and-instances) enumerados en la consola Modelos de flujo de trabajo. La única información obligatoria es la carga útil, aunque también se puede añadir un título o comentario.

## Iniciadores de flujos de trabajo {#workflows-launchers}

Workflow Launcher supervisa los cambios en el repositorio de contenido para iniciar los flujos de trabajo según la ubicación y el tipo de recurso del nodo modificado.

Con **Launcher** puede:

* Consulte los flujos de trabajo ya iniciados para nodos específicos.
* Seleccione un flujo de trabajo que iniciar cuando se haya creado, modificado o eliminado un determinado tipo de nodo/nodo.
* Elimine una relación flujo a nodo existente.

Se puede crear un lanzador para cualquier nodo. Sin embargo, los cambios en ciertos nodos no inician flujos de trabajo. Los cambios en los nodos situados debajo de las rutas siguientes no hacen que se inicien los flujos de trabajo:

* `/var/workflow/instances`
* Cualquier nodo de bandeja de entrada de flujo de trabajo ubicado en cualquier lugar de la rama `/home/users`
* `/tmp`
* `/var/audit`
* `/var/classes`
* `/var/eventing`
* `/var/linkchecker`
* `/var/mobile`
* `/var/statistics`

   * Excepción: Los cambios en los nodos situados debajo de `/var/statistics/tracking` *do* hacen que se inicien los flujos de trabajo.

Con la instalación estándar se incluyen varias definiciones. Se utilizan para tareas de administración de recursos digitales y colaboración social:

![wf-100](assets/wf-100.png)

## Paquetes de flujo de trabajo para procesamiento por lotes {#workflow-packages-for-batch-processing}

Los paquetes de flujo de trabajo son paquetes que se pueden pasar a un flujo de trabajo como carga útil para el procesamiento, lo que permite procesar varios recursos.

Un paquete de flujo de trabajo:

* contiene vínculos a un conjunto de recursos (como páginas o recursos).
* contiene información del paquete, como la fecha de creación, el usuario que creó el paquete y una breve descripción.
* se define mediante una plantilla de página especializada; estas páginas permiten al usuario especificar los recursos del paquete.
* se puede usar varias veces.
* el usuario puede cambiarlo (añadir o eliminar recursos) mientras se esté ejecutando realmente la instancia de flujo de trabajo.

## Inicio de un flujo de trabajo desde la consola Modelos {#starting-a-workflow-from-the-models-console}

1. Vaya a la consola **Modelos** utilizando **Herramientas**, **Flujo de trabajo** y, a continuación, **Modelos**.
1. Seleccione el flujo de trabajo (según la vista de la consola); también puede utilizar Buscar (parte superior izquierda) si es necesario:

   ![wf-103](assets/wf-103.png)

   >[!NOTE]
   >
   >El indicador **[Transient](/help/sites-developing/workflows.md#transient-workflows)** muestra los flujos de trabajo para los que no se persistirá el historial del flujo de trabajo.

1. Seleccione **Iniciar flujo de trabajo** en la barra de herramientas.
1. Se abrirá el cuadro de diálogo Ejecutar flujo de trabajo , que le permite especificar:

   * **Carga útil**

      Puede ser una página, nodo, recurso, paquete, entre otros recursos.

   * **Título**

      Un título opcional para ayudar a identificar esta instancia.

   * **Comentario**

      Un comentario opcional para ayudar a indicar los detalles de esta instancia.
   ![wf-104](assets/wf-104.png)

## Creación de una configuración de lanzador {#creating-a-launcher-configuration}

1. Vaya a la consola **Workflow Launchers** utilizando **Tools**, **Workflow** y, a continuación, **Launchers**.
1. Seleccione **Crear** y luego **Agregar lanzador** para abrir el cuadro de diálogo:

   ![wf-105](assets/wf-105.png)

   * **Tipo de evento**

      El tipo de evento que iniciará el flujo de trabajo:

      * Creado
      * Modificado
      * Eliminado
   * **Tipo de nodo**

      Tipo de nodo al que se aplica el iniciador del flujo de trabajo.

   * **Ruta**

      Ruta a la que se aplica el iniciador del flujo de trabajo.

   * **Modo(s) de ejecución**

      Tipo de servidor al que se aplica el iniciador del flujo de trabajo. Seleccione **Autor**, **Publicar** o **Autor y publicación**.

   * **Condiciones**

      Una lista de condiciones para valores de nodo que, cuando se evalúan, determinan si se inicia el flujo de trabajo. Por ejemplo, la siguiente condición hace que el flujo de trabajo se inicie cuando el nodo tenga un nombre de propiedad con el valor Usuario:

      name==User

   * **Características**

      Lista de funciones que se activarán. Seleccione las funciones necesarias con el selector desplegable.

   * **Funciones desactivadas**

   Lista de funciones que se van a deshabilitar. Seleccione las funciones necesarias con el selector desplegable.

   * **Modelo de flujo de trabajo**

      Flujo de trabajo que se inicia cuando el tipo de evento se produce en el tipo de nodo o en la ruta bajo la condición definida.

   * **Descripción**

      Su propio texto para describir e identificar la configuración del iniciador.

   * **Activar**

      Controla si el iniciador del flujo de trabajo está activado:

      * Seleccione **Enable** para iniciar flujos de trabajo cuando se cumplan las propiedades de configuración.
      * Seleccione **Disable** cuando el flujo de trabajo no debe ejecutarse (ni siquiera cuando se cumplen las propiedades de configuración).
   * **Lista de exclusiones**

      Esto especifica cualquier evento JCR que se excluya (es decir, que se ignore) al determinar si se debe activar un flujo de trabajo.

      Esta propiedad de lanzador es una lista de elementos separados por comas: &quot;

      * `property-name` ignore cualquier  `jcr` evento que se active con el nombre de propiedad especificado. &quot;
      * `event-user-data:<*someValue*>` ignora cualquier evento que contenga el  `*<someValue*`>  `user-data` establecido a través de la  [ `ObservationManager` API] (https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/observation/ObservationManager.html#setUserData(java.lang.String).

      Por ejemplo:

      `jcr:lastModified,dc:modified,dc:format,jcr:lastModifiedBy,imageMap,event-user-data:changedByWorkflowProcess`

      Esta función se puede utilizar para ignorar cualquier cambio activado por otro proceso de flujo de trabajo añadiendo el elemento de exclusión:

      `event-user-data:changedByWorkflowProcess`





1. Seleccione **Crear** para crear el lanzador y volver a la consola.

   Una vez que se produce el evento apropiado, se activa el lanzador y se inicia el flujo de trabajo.

## Administración de la configuración de un iniciador {#managing-a-launcher-configuration}

Después de crear la configuración del iniciador, puede utilizar la misma consola para seleccionar la instancia y, a continuación, **Ver propiedades** (y editarlas) o **Eliminar**.
