---
title: Inicio de Flujos de trabajo
seo-title: Inicio de Flujos de trabajo
description: Aprenda a inicio de Flujos de trabajo en AEM.
seo-description: Aprenda a inicio de Flujos de trabajo en AEM.
uuid: 0648d335-ecce-459d-95fd-3d4d76181b32
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: e9ab4796-a050-40de-b073-af7d33cff009
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 5%

---


# Inicio de Flujos de trabajo{#starting-workflows}

Al administrar flujos de trabajo, puede darles inicio mediante diversos métodos:

* Manualmente:

   * Desde un [Modelo de flujo de trabajo](#workflow-models).
   * Uso de un paquete de workflow para [procesamiento por lotes](#workflow-packages-for-batch-processing).

* Automáticamente:

   * En respuesta a los cambios de nodo; [usando un iniciador](#workflows-launchers).

>[!NOTE]
>
>También hay otros métodos disponibles para los autores; para obtener más información, consulte:
>
>* [Aplicación de flujos de trabajo a las páginas](/help/sites-authoring/workflows-applying.md)
>* [Cómo aplicar flujos de trabajo a recursos DAM](/help/assets/assets-workflow.md)
>* [AEM Forms](https://helpx.adobe.com/aem-forms/6-2/aem-workflows-submit-process-form.html)
>* [Proyectos de traducción](/help/sites-administering/tc-manage.md)

>



## Modelos de flujo de trabajo {#workflow-models}

Puede inicio de un flujo de trabajo [basado en uno de los modelos](/help/sites-administering/workflows.md#workflow-models-and-instances) enumerados en la consola Modelos de flujo de trabajo. La única información obligatoria es la carga útil, aunque también se puede añadir un título y/o comentario.

## Lanzadores de flujos de trabajo {#workflows-launchers}

Workflow Launcher supervisa los cambios en el repositorio de contenido para iniciar flujos de trabajo en función de la ubicación y el tipo de recurso del nodo modificado.

Con el **iniciador** puede:

* Consulte los flujos de trabajo ya iniciados para nodos específicos.
* Seleccione un flujo de trabajo para iniciar cuando se haya creado/modificado/eliminado un determinado nodo/tipo de nodo.
* Elimine una relación existente de flujo de trabajo a nodo.

Se puede crear un iniciador para cualquier nodo. Sin embargo, los cambios realizados en determinados nodos no inician flujos de trabajo. Los cambios en los nodos situados debajo de las rutas siguientes no provocan que se inicien flujos de trabajo:

* `/var/workflow/instances`
* Cualquier nodo de bandeja de entrada de workflow ubicado en cualquier parte de la rama `/home/users`
* `/tmp`
* `/var/audit`
* `/var/classes`
* `/var/eventing`
* `/var/linkchecker`
* `/var/mobile`
* `/var/statistics`

   * Excepción: Los cambios en los nodos por debajo de `/var/statistics/tracking` *do* hacen que se inicien flujos de trabajo.

La instalación estándar incluye varias definiciones. Se utilizan para la administración de recursos digitales y tareas de colaboración social:

![wf-100](assets/wf-100.png)

## Paquetes de flujo de trabajo para procesamiento por lotes {#workflow-packages-for-batch-processing}

Los paquetes de flujo de trabajo son paquetes que se pueden pasar a un flujo de trabajo como carga útil para el procesamiento, lo que permite procesar varios recursos.

Un paquete de workflow:

* contiene vínculos a un conjunto de recursos (como páginas, recursos).
* contiene información del paquete, como la fecha de creación, el usuario que creó el paquete y una breve descripción.
* se define mediante una plantilla de página especializada; estas páginas permiten al usuario especificar los recursos del paquete.
* puede utilizarse varias veces.
* puede cambiarla el usuario (agregar o quitar recursos) mientras se esté ejecutando la instancia de flujo de trabajo.

## Inicio de un flujo de trabajo desde la consola Modelos {#starting-a-workflow-from-the-models-console}

1. Vaya a la consola **Modelos** utilizando **Herramientas**, **Flujo de trabajo** y, a continuación, **Modelos**.
1. Seleccione el flujo de trabajo (según la vista de la consola); también puede utilizar Buscar (parte superior izquierda) si es necesario:

   ![wf-103](assets/wf-103.png)

   >[!NOTE]
   >
   >El indicador **[Transient](/help/sites-developing/workflows.md#transient-workflows)** muestra flujos de trabajo para los que no se persistirá el historial de flujo de trabajo.

1. Seleccione **Flujo de trabajo de Inicio** en la barra de herramientas.
1. Se abrirá el cuadro de diálogo Ejecutar flujo de trabajo, que le permite especificar:

   * **Carga útil**

      Puede ser una página, un nodo, un recurso, un paquete, entre otros recursos.

   * **Título**

      Un título opcional para ayudar a identificar esta instancia.

   * **Comentario**

      Un comentario opcional para ayudar a indicar los detalles de esta instancia.
   ![wf-104](assets/wf-104.png)

## Creación de una configuración de iniciador {#creating-a-launcher-configuration}

1. Vaya a la consola **Workflow Launchers** utilizando **Tools**, **Workflow** y, a continuación, **Launchers**.
1. Seleccione **Crear** y luego **Añadir iniciador** para abrir el cuadro de diálogo:

   ![wf-105](assets/wf-105.png)

   * **Tipo de evento**

      El tipo de evento que iniciará el flujo de trabajo:

      * Creado
      * Modificado
      * Eliminado
   * **Notetype**

      El tipo de nodo al que se aplica el iniciador del flujo de trabajo.

   * **Ruta**

      Ruta a la que se aplica el iniciador del flujo de trabajo.

   * **Modo(s) de ejecución**

      El tipo de servidor al que se aplica el iniciador del flujo de trabajo. Seleccione **Autor**, **Publicar** o **Autor y publicar**.

   * **Condiciones**

      Lista de condiciones para valores de nodo que, al evaluarse, determinan si se inicia el flujo de trabajo. Por ejemplo, la siguiente condición hace que el flujo de trabajo se inicie cuando el nodo tenga un nombre de propiedad con el valor Usuario:

      name==User

   * **Características**

      Lista de características que se van a habilitar. Seleccione las funciones necesarias con el selector desplegable.

   * **Funciones desactivadas**

   Lista de funciones que se van a deshabilitar. Seleccione las funciones necesarias con el selector desplegable.

   * **Modelo de flujo de trabajo**

      Flujo de trabajo que se iniciará cuando se produzca el Tipo de evento en el tipo de nodo o en la ruta de acceso en la condición definida.

   * **Descripción**

      Su propio texto para describir e identificar la configuración del iniciador.

   * **Activar**

      Controla si el iniciador del flujo de trabajo está activado:

      * Seleccione **Habilitar** para iniciar flujos de trabajo cuando se cumplan las propiedades de configuración.
      * Seleccione **Deshabilitar** cuando el flujo de trabajo no se deba ejecutar (ni siquiera cuando se cumplan las propiedades de configuración).
   * **Lista de exclusiones**

      Esto especifica los eventos JCR que se excluirán (es decir, se omitirán) al determinar si se debe activar un flujo de trabajo.

      Esta propiedad del iniciador es una lista de elementos separados por comas: &quot;

      * `property-name` ignore cualquier  `jcr` evento que se active en el nombre de propiedad especificado. &quot;
      * `event-user-data:<*someValue*>` ignora cualquier evento que contenga el  `*<someValue*`>  `user-data` establecido mediante la  [ `ObservationManager` API](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/observation/ObservationManager.html#setUserData(java.lang.String).

      Por ejemplo:

      `jcr:lastModified,dc:modified,dc:format,jcr:lastModifiedBy,imageMap,event-user-data:changedByWorkflowProcess`

      Esta función se puede utilizar para ignorar cualquier cambio que se desencadene en otro proceso de flujo de trabajo mediante la adición del elemento de exclusión:

      `event-user-data:changedByWorkflowProcess`





1. Seleccione **Crear** para crear el iniciador y volver a la consola.

   Una vez que se produce el evento adecuado, se activa el iniciador y se inicia el flujo de trabajo.

## Administración de la configuración del iniciador {#managing-a-launcher-configuration}

Después de crear la configuración del iniciador, puede utilizar la misma consola para seleccionar la instancia y, a continuación, **Propiedades de Vista** (y editarlas) o **Eliminar**.
