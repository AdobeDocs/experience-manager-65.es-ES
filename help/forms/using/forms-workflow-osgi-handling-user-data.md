---
title: flujos de trabajo centrados en formularios en OSGi| Gestión de datos de usuario
seo-title: flujos de trabajo centrados en formularios en OSGi| Gestión de datos de usuario
description: nulo
seo-description: nulo
uuid: 6eefbe84-6496-4bf8-b065-212aa50cd074
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f400560-8152-4d07-a946-e514e9b9cedf
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# flujos de trabajo centrados en formularios en OSGi| Gestión de datos de usuario {#forms-centric-workflows-on-osgi-handling-user-data}

Los flujos de trabajo de AEM centrados en los formularios le permiten automatizar procesos empresariales reales centrados en los formularios. Los Flujos de trabajo constan de una serie de pasos que se ejecutan en un orden especificado en el modelo de flujo de trabajo asociado. Cada paso realiza una acción específica, como asignar una tarea a un usuario o enviar un mensaje de correo electrónico. Los Flujos de trabajo pueden interactuar con los recursos del repositorio, las cuentas de usuario y los servicios. Por lo tanto, los flujos de trabajo pueden coordinar actividades complicadas que involucran cualquier aspecto de Experience Manager.

Se puede activar o iniciar un flujo de trabajo centrado en formularios mediante cualquiera de los siguientes métodos:

* Envío de una aplicación desde la bandeja de entrada de AEM
* Envío de una aplicación desde la aplicación de AEM Forms
* Envío de un formulario adaptable
* Uso de una carpeta vigilada
* Envío de una comunicación interactiva o una carta

Para obtener más información sobre las funciones y flujos de trabajo de AEM centrados en formularios, consulte Flujo de trabajo centrado en [formularios en OSGi](/help/forms/using/aem-forms-workflow.md).

## Almacenes de datos y datos de usuarios {#user-data-and-data-stores}

Cuando se activa un flujo de trabajo, se genera automáticamente una carga útil para la instancia de flujo de trabajo. A cada instancia de flujo de trabajo se le asigna un ID de instancia único y un ID de carga útil asociado. La carga útil contiene las ubicaciones del repositorio para los datos de usuario y formulario asociados a una instancia de flujo de trabajo. Además, los borradores y los datos históricos de una instancia de flujo de trabajo también se almacenan en el repositorio de AEM.

Las ubicaciones de repositorio predeterminadas donde residen la carga útil, los borradores y el historial de una instancia de flujo de trabajo son las siguientes:

>[!NOTE]
>
>Puede configurar diferentes ubicaciones para almacenar datos de carga útil, borrador e historial al crear un flujo de trabajo o una aplicación. Para identificar las ubicaciones en las que un flujo de trabajo o una aplicación almacenaron datos, revise el flujo de trabajo.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td>AEM 6.4 Forms</td>
   <td>AEM 6.3 Forms</td>
  </tr>
  <tr>
   <td><strong>Instancia <br /> de flujo de trabajo</strong></td>
   <td>/var/workflow/instance/[server_id]/&lt;fecha&gt;/[workflow-instance]/</td>
   <td>/etc/workflow/instance/[server_id]/[date]/[workflow-instance]/</td>
  </tr>
  <tr>
   <td><strong>Carga útil</strong></td>
   <td>/var/fd/panel/payload/[server_id]/[date]/<br /> [payload-id]/</td>
   <td>/etc/fd/panel/payload/[server_id]/[date]/<br /> [payload-id]/</td>
  </tr>
  <tr>
   <td><strong>Borradores</strong></td>
   <td>/var/fd/panel/instance/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td>
   <td>/etc/fd/panel/instance/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td>
  </tr>
  <tr>
   <td><strong>Historia</strong></td>
   <td>/var/fd/panel/instance/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
   <td>/etc/fd/panel/instance/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
  </tr>
 </tbody>
</table>

## Acceso y eliminación de datos de usuario {#access-and-delete-user-data}

Puede acceder a los datos de usuario y eliminarlos de una instancia de flujo de trabajo del repositorio. Para conseguirlo, debe conocer el ID de instancia de la instancia de flujo de trabajo asociada al usuario. Puede encontrar el ID de instancia de una instancia de flujo de trabajo utilizando el nombre de usuario del usuario que inició la instancia de flujo de trabajo o que es el usuario asignado actual de la instancia de flujo de trabajo.

Sin embargo, no puede identificar o los resultados pueden ser ambiguos al identificar flujos de trabajo asociados con un iniciador en los siguientes escenarios:

* **Flujo de trabajo desencadenado mediante una carpeta** vigilada: No se puede identificar una instancia de flujo de trabajo con su iniciador si el flujo de trabajo se activa mediante una carpeta vigilada. En este caso, la información del usuario se codifica en los datos almacenados.
* **Flujo de trabajo iniciado desde la instancia** de AEM de publicación: Todas las instancias de flujo de trabajo se crean mediante un usuario de servicio cuando se envían formularios adaptables, comunicaciones interactivas o cartas desde una instancia de publicación de AEM. En estos casos, el nombre de usuario del usuario que ha iniciado sesión no se captura en los datos de instancia del flujo de trabajo.

### Acceso a los datos de usuario {#access}

Para identificar y acceder a los datos de usuario almacenados para una instancia de flujo de trabajo, lleve a cabo los siguientes pasos:

1. En la instancia de creación de AEM, vaya a `https://'[server]:[port]'/crx/de` Herramientas > **[!UICONTROL Consulta]** y vaya a.

   Seleccione **[!UICONTROL SQL2]** en la lista desplegable **[!UICONTROL Tipo]** .

1. Según la información disponible, ejecute una de las siguientes consultas:

   * Ejecute lo siguiente si se conoce el iniciador del flujo de trabajo:
   `SELECT &ast; FROM [cq:Workflow] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[initiator]='*initiator-ID*'`

   * Ejecute lo siguiente si el usuario cuyos datos está encontrando es el usuario asignado del flujo de trabajo actual:
   `SELECT &ast; FROM [cq:WorkItem] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[assignee]='*assignee-id*'`

   La consulta devuelve la ubicación de todas las instancias de flujo de trabajo para el iniciador de flujo de trabajo especificado o el usuario asignado del flujo de trabajo actual.

   Por ejemplo, la siguiente consulta devuelve dos rutas de acceso de instancias de flujo de trabajo desde el `/var/workflow/instances` nodo cuyo iniciador de flujo de trabajo es `srose`.

   ![workflow-instance](assets/workflow-instance.png)

1. Vaya a una ruta de instancia de flujo de trabajo devuelta por la consulta. La propiedad status muestra el estado actual de la instancia de workflow.

   ![estado](assets/status.png)

1. En el nodo de instancia de flujo de trabajo, vaya a `data/payload/`. La `path` propiedad almacena la ruta de la carga útil de la instancia de flujo de trabajo. Puede desplazarse a la ruta para acceder a los datos almacenados en la carga útil.

   ![payload-path](assets/payload-path.png)

1. Vaya a las ubicaciones de borradores e historial de la instancia de flujo de trabajo.

   Por ejemplo:

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/draft/`

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/history/`

1. Repita los pasos 3 a 5 para todas las instancias de flujo de trabajo devueltas por la consulta en el paso 2.

>[!NOTE]
>
>La aplicación AEM Forms también almacena datos en modo sin conexión. Es posible que los datos de una instancia de flujo de trabajo se almacenen localmente en dispositivos individuales y se envíen al servidor de Forms cuando la aplicación se sincroniza con el servidor.

### Eliminar datos de usuario {#delete-user-data}

Debe ser administrador de AEM para eliminar los datos de usuario de las instancias de flujo de trabajo siguiendo estos pasos:

1. Siga las instrucciones de [Access user data](/help/forms/using/forms-workflow-osgi-handling-user-data.md#access) y tenga en cuenta lo siguiente:

   * Rutas a instancias de flujo de trabajo asociadas con el usuario
   * Estado de las instancias de flujo de trabajo
   * Rutas a las cargas útiles para las instancias de flujo de trabajo
   * Rutas a borradores e historial para las instancias de flujo de trabajo

1. Siga este paso para las instancias de flujo de trabajo en **EJECUCIÓN**, **SUSPENDIDO** o **ESTADO** :

   1. Vaya a `https://'[server]:[port]'/aem/start.html` e inicie sesión con las credenciales del administrador.
   1. Vaya a **[!UICONTROL Herramientas > Flujo de trabajo > Instancias]**.
   1. Seleccione las instancias de flujo de trabajo relevantes para el usuario y toque **[!UICONTROL Finalizar]** para finalizar las instancias en ejecución.
   Para obtener más información sobre cómo trabajar con instancias de flujo de trabajo, consulte [Administración de instancias](/help/sites-administering/workflows-administering.md)de flujo de trabajo.

1. Vaya a la consola de CRXDE Lite, vaya a la ruta de carga útil de una instancia de flujo de trabajo y elimine el `payload` nodo.
1. Vaya a la ruta de borradores de una instancia de flujo de trabajo y elimine el `draft` nodo.
1. Vaya a la ruta de historial de una instancia de flujo de trabajo y elimine el `history` nodo.
1. Vaya a la ruta de la instancia de flujo de trabajo de una instancia de flujo de trabajo y elimine el `[workflow-instance-ID]` nodo del flujo de trabajo.

   >[!NOTE]
   >
   >Al eliminar el nodo de instancia de flujo de trabajo, se eliminará la instancia de flujo de trabajo para todos los participantes del flujo de trabajo.

1. Repita los pasos 2 a 6 para todas las instancias de flujo de trabajo identificadas para un usuario.
1. Identifique y elimine los datos de borrador y envío sin conexión de la bandeja de salida de la aplicación de AEM Forms de los participantes del flujo de trabajo para evitar el envío al servidor.

También puede utilizar API para acceder a nodos y propiedades y eliminarlos. Consulte los siguientes documentos para obtener más información.

* [Cómo acceder mediante programación al JCR de AEM](/help/sites-developing/access-jcr.md)
* [Eliminación de nodos y propiedades](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.9%20Removing%20Nodes%20and%20Properties)
* [Referencia de API](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/overview-summary.html)

