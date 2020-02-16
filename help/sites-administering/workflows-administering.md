---
title: Administración de instancias de flujo de trabajo
seo-title: Administración de instancias de flujo de trabajo
description: Obtenga información sobre cómo administrar instancias de flujo de trabajo.
seo-description: Obtenga información sobre cómo administrar instancias de flujo de trabajo.
uuid: 81e53ef5-fe62-4ed4-b2d4-132aa986d5aa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d9c96e7f-9416-48e1-a6af-47384f7bee92
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Administración de instancias de flujo de trabajo{#administering-workflow-instances}

La consola de flujo de trabajo proporciona varias herramientas para administrar instancias de flujo de trabajo a fin de asegurarse de que se ejecutan según lo esperado.

>[!NOTE]
>
>La consola [](/help/sites-administering/jmx-console.md#workflow-maintenance) JMX proporciona operaciones de mantenimiento de flujo de trabajo adicionales.

Hay una serie de consolas disponibles para administrar los flujos de trabajo. Utilice la navegación [](/help/sites-authoring/basic-handling.md#global-navigation) global para abrir el panel **Herramientas** y, a continuación, seleccione **Flujo de trabajo**:

* **Modelos**: Administrar definiciones de flujo de trabajo
* **Instancias**: Visualización y administración de instancias de flujo de trabajo en ejecución
* **Lanzadores**: Administrar cómo se deben iniciar los flujos de trabajo
* **Archivo**: Ver el historial de flujos de trabajo que se completaron correctamente
* **Errores**: Ver el historial de flujos de trabajo que se completaron con errores

## Monitoreo del estado de las instancias de flujo de trabajo {#monitoring-the-status-of-workflow-instances}

1. Con Navegación, seleccione **Herramientas** y, a continuación, **Flujo de trabajo**.
1. Seleccione **Instancias** para mostrar la lista de instancias de flujo de trabajo en curso.

   ![wf-96](assets/wf-96.png)

1. Seleccione un elemento específico y, a continuación, **Abrir historial** para ver más detalles:

   ![wf-97](assets/wf-97.png)

## Suspensión, reanudación y finalización de una instancia de flujo de trabajo {#suspending-resuming-and-terminating-a-workflow-instance}

1. Con Navegación, seleccione **Herramientas** y, a continuación, **Flujo de trabajo**.
1. Seleccione **Instancias** para mostrar la lista de instancias de flujo de trabajo en curso.

   ![wf-96-1](assets/wf-96-1.png)

1. Seleccione un elemento específico y, a continuación, utilice **Terminar**, **Suspender** o **Reanudar**, según corresponda; se requiere confirmación y/o más detalles:

   ![wf-97-1](assets/wf-97-1.png)

## Visualización de flujos de trabajo archivados {#viewing-archived-workflows}

1. Con Navegación, seleccione **Herramientas** y, a continuación, **Flujo de trabajo**.
1. Seleccione **Archivar** para mostrar la lista de instancias de flujo de trabajo que se completaron correctamente.

   ![wf-98](assets/wf-98.png)

   >[!NOTE]
   >
   >El estado de anulación se considera una finalización exitosa, ya que se produce como resultado de la acción del usuario; por ejemplo:
   >
   >* uso de la acción **Terminar**
   >* cuando se elimina (forzosamente) una página que está sujeta a un flujo de trabajo, se cierra el flujo de trabajo


1. Seleccione un elemento específico y, a continuación, **Abrir historial** para ver más detalles:

   ![wf-99](assets/wf-99.png)

## Corrección de errores de instancia de flujo de trabajo {#fixing-workflow-instance-failures}

Cuando un flujo de trabajo falla, AEM proporciona la consola **Errores** para permitirle investigar y realizar las acciones oportunas una vez que se haya gestionado la causa original:

* **Detalles** de errorAbre una ventana para mostrar el mensaje **de** error, el **paso** y la pila **de** errores.

* **Abrir historial** Muestra detalles del historial de flujo de trabajo.

* **Paso** de reintento Ejecuta de nuevo la instancia del componente Paso de secuencia de comandos. Utilice el comando Reintentar etapa después de haber corregido la causa del error original. Por ejemplo, vuelva a intentar el paso después de corregir un error en el script que ejecuta el paso de proceso.
* **Finalizar** Finalice el flujo de trabajo si el error ha provocado una situación irreconsiderable para el flujo de trabajo. Por ejemplo, el flujo de trabajo puede basarse en condiciones ambientales como la información del repositorio que ya no son válidas para la instancia de flujo de trabajo.
* **Terminar y reintentar** De forma similar a **Finalizar** , con la diferencia de que una nueva instancia de flujo de trabajo se inicia con la carga útil, el título y la descripción originales.

Para investigar los errores y, a continuación, reanudar o finalizar el flujo de trabajo posteriormente, siga estos pasos:

1. Con Navegación, seleccione **Herramientas** y, a continuación, **Flujo de trabajo**.
1. Seleccione **Errores** para mostrar la lista de instancias de flujo de trabajo que no se completaron correctamente.
1. Seleccione un elemento específico y, a continuación, la acción adecuada:

   ![wf-47](assets/wf-47.png)

## Depuración regular de instancias de flujo de trabajo {#regular-purging-of-workflow-instances}

Al minimizar el número de instancias de flujo de trabajo, aumenta el rendimiento del motor de flujo de trabajo, de modo que puede depurar regularmente instancias de flujo de trabajo completadas o en ejecución del repositorio.

Configure **Adobe Granite Workflow Purge Configuration** para purgar instancias de flujo de trabajo según su edad y estado. También puede depurar instancias de flujo de trabajo de todos los modelos o de un modelo específico.

También puede crear varias configuraciones del servicio para depurar instancias de flujo de trabajo que cumplan diferentes criterios. Por ejemplo, cree una configuración que purgue las instancias de un modelo de flujo de trabajo concreto cuando se estén ejecutando durante mucho más tiempo del esperado. Cree otra configuración que purgue todos los flujos de trabajo completados después de un determinado número de días para minimizar el tamaño del repositorio.

Para configurar el servicio, puede utilizar la consola [](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) web o [agregar una configuración OSGi al repositorio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository). En la tabla siguiente se describen las propiedades necesarias para cada método.

>[!NOTE]
>
>Para agregar la configuración al repositorio, el PID de servicio es:
>
>`com.adobe.granite.workflow.purge.Scheduler`
>
>Dado que el servicio es un servicio de fábrica, el nombre del `sling:OsgiConfig` nodo requiere un sufijo de identificador, por ejemplo:
>
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>Nombre de propiedad (consola web)</th>
   <th>Nombre de propiedad OSGi</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>Nombre del trabajo</td>
   <td>schedule purge.name</td>
   <td>Un nombre descriptivo para la depuración programada.</td>
  </tr>
  <tr>
   <td>Estado de flujo de trabajo</td>
   <td>schedule purge.workflowStatus</td>
   <td><p>Estado de las instancias de flujo de trabajo que se van a purgar. Los siguientes valores son válidos:</p>
    <ul>
     <li>COMPLETADO: Las instancias de flujo de trabajo completadas se purgan.</li>
     <li>EJECUTANDO: Se purgan las instancias de flujo de trabajo en ejecución.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modelos que purgar</td>
   <td>schedule purge.modelIds</td>
   <td><p>ID de los modelos de flujo de trabajo que se van a purgar. <br /> El ID es la ruta al nodo del modelo, por ejemplo: /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br /> No especifique ningún valor para depurar instancias de todos los modelos de flujo de trabajo.</p> <p>Para especificar varios modelos, haga clic en el botón + en la consola web. </p> </td>
  </tr>
  <tr>
   <td>Edad del flujo de trabajo</td>
   <td>purga programada.daysell</td>
   <td>La antigüedad de las instancias de flujo de trabajo que se van a purgar, en días.</td>
  </tr>
 </tbody>
</table>

## Configuración del tamaño máximo de la bandeja de entrada {#setting-the-maximum-size-of-the-inbox}

Puede configurar el tamaño máximo de la bandeja de entrada configurando el servicio **de flujo de trabajo de** Adobe Granite, utilizando la consola [](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) Web o [agregando una configuración OSGi al repositorio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository). En la tabla siguiente se describe la propiedad que se configura para cualquier método.

>[!NOTE]
>
>Para agregar la configuración al repositorio, el PID de servicio es:
>
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| Nombre de propiedad (consola web) | Nombre de propiedad OSGi |
|---|---|
| Tamaño máximo de consulta de la bandeja de entrada | granite.workflow.inboxQuerySize |

