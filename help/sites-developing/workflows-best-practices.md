---
title: Prácticas recomendadas del flujo de trabajo
seo-title: Prácticas recomendadas del flujo de trabajo
description: nulo
seo-description: nulo
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Prácticas recomendadas del flujo de trabajo{#workflow-best-practices}

Los flujos de trabajo le permiten automatizar las actividades de Adobe Experience Manager (AEM).

A menudo representan una gran cantidad del procesamiento que se produce en un entorno de AEM, por lo que cuando los pasos del flujo de trabajo personalizado no se escriben según las prácticas recomendadas, o cuando los flujos de trabajo predeterminados no se configuran para ejecutarse de la manera más eficiente posible, el sistema puede sufrir las consecuencias.

Por lo tanto, es muy recomendable planificar cuidadosamente las implementaciones de flujos de trabajo.

## Configuración {#configuration}

Al configurar procesos de flujo de trabajo (personalizados y/o predeterminados), hay algunas cosas que deben tenerse en cuenta.

### Flujos de trabajo transitorios {#transient-workflows}

Para optimizar las cargas de ingestión alta, puede definir un [flujo de trabajo como transitorio](/help/sites-developing/workflows.md#transient-workflows).

Cuando un flujo de trabajo es transitorio, los datos del tiempo de ejecución relacionados con los pasos de trabajo intermedios no persisten en el JCR cuando se ejecutan (las representaciones de salida se mantienen, por supuesto).

Las ventajas pueden incluir:

* Reducción del tiempo de procesamiento del flujo de trabajo; de hasta el 10 %.
* Reduzca significativamente el crecimiento del repositorio.
* No se necesitan más flujos de trabajo de CRUD para depurar.
* Además, reduce el número de archivos TAR para compactar.

>[!CAUTION]
>
>Si su empresa dicta que los datos de tiempo de ejecución del flujo de trabajo de mantenimiento y archivado se conservan con fines de auditoría, no active esta función.

### Ajuste de flujos de trabajo DAM {#tuning-dam-workflows}

Para obtener directrices de ajuste del rendimiento para flujos de trabajo de DAM, consulte la Guía [de ajuste del rendimiento de](/help/assets/performance-tuning-guidelines.md)AEM Assets.

### Configurar el número máximo de flujos de trabajo simultáneos {#configure-the-maximum-number-of-concurrent-workflows}

AEM puede permitir que se ejecuten varios subprocesos de flujo de trabajo al mismo tiempo. De forma predeterminada, el número de subprocesos está configurado para ser la mitad del número de núcleos de procesador del sistema.

En los casos en que los flujos de trabajo que se ejecutan exijan recursos del sistema, esto puede significar que AEM no puede utilizarse para otras tareas, como procesar la IU de creación. Como resultado, el sistema puede ser lento durante actividades como la carga masiva de imágenes.

Para solucionar este problema, Adobe recomienda configurar el número de trabajos **paralelos** máximos de entre la mitad y las tres cuartas partes del número de núcleos de procesador del sistema. Esto debería permitir que el sistema tenga suficiente capacidad para responder al procesar estos flujos de trabajo.

Para configurar los trabajos **paralelos** máximos, puede:

* Configuración de **[OSGi](/help/sites-deploying/configuring-osgi.md)**desde la consola web de AEM; para **cola: Granite Workflow Queue**(una configuración **de cola de trabajos Sling de**Apache).

* Configure la cola desde la opción Trabajos **de** Sling de la consola web de AEM; para la configuración de la cola de **trabajos: Cola** de flujo de trabajo de granito, en `http://localhost:4502/system/console/slingevent`.

Además, existe una configuración independiente para la cola **de trabajos de proceso externo de** Granite Workflow. Se utiliza para procesos de flujo de trabajo que inician binarios externos, como **InDesign Server** o **Image Magick**.

### Configurar colas de trabajos individuales {#configure-individual-job-queues}

En algunos casos, es útil configurar colas de trabajos individuales para controlar los subprocesos simultáneos u otras opciones de cola, en un trabajo individual. Puede agregar y configurar una cola individual desde la consola web a través de la fábrica de configuración **de cola de trabajos Sling de** Apache. Para encontrar el tema apropiado para enumerar, ejecute el modelo del flujo de trabajo y búsquelo en la consola Trabajos **** de Sling; por ejemplo, en `http://localhost:4502/system/console/slingevent`.

También se pueden agregar colas de trabajos individuales para flujos de trabajo transitorios.

### Configurar depuración de flujo de trabajo {#configure-workflow-purging}

En una instalación estándar, AEM proporciona una consola de mantenimiento en la que se pueden programar y configurar las actividades de mantenimiento diarias y semanales; por ejemplo, en:

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

De forma predeterminada, la ventana **de mantenimiento** semanal tiene una tarea **Depuración** de flujo de trabajo, pero debe configurarse antes de que se ejecute. Para configurar las purgas de flujo de trabajo, se debe agregar una nueva configuración **de depuración de flujo de trabajo de** Adobe Granite en la consola web.

Para obtener más información sobre las tareas de mantenimiento en AEM, consulte el panel de [operaciones](/help/sites-administering/operations-dashboard.md).

## Personalización {#customization}

Al escribir procesos de flujo de trabajo personalizados, hay algunas cosas que deben tenerse en cuenta.

### Ubicaciones {#locations}

Las definiciones de modelos de flujo de trabajo, lanzadores, secuencias de comandos y notificaciones se guardan en el repositorio según el tipo; es decir, lista para usar, personalizada, entre otros.

>[!NOTE]
>
>Consulte también Reestructuración [del repositorio en AEM 6.5](/help/sites-deploying/repository-restructuring.md).

#### Ubicaciones: modelos de flujo de trabajo {#locations-workflow-models}

Los modelos de flujo de trabajo se almacenan en el repositorio según el tipo:

* Los diseños de flujo de trabajo predeterminados se mantienen en la siguiente ruta:

   `/libs/settings/workflow/models/`

   >[!CAUTION]
   >
   >No:
   >
   >* coloque cualquiera de los modelos de flujo de trabajo personalizados en esta carpeta
   >* editar cualquier elemento de `/libs`
   >
   >Como cualquier cambio se puede sobrescribir al actualizar o al instalar correcciones urgentes, paquetes de correcciones acumulativas o Service Packs.

* Los diseños de flujo de trabajo personalizados se incluyen en:

   ```
   /conf/global/settings/workflow/models/...
   ```

* Los diseños de flujo de trabajo en tiempo de ejecución (tanto predeterminados como personalizados) se mantienen en la siguiente ruta:

   `/var/workflow/models/`

* Los diseños de flujo de trabajo heredados (tanto en tiempo de diseño como en tiempo de ejecución) se mantienen en la siguiente ruta:

   `/etc/workflow/models/`

   >[!NOTE]
   >
   >Si estos diseños se editan *mediante la interfaz de usuario* de AEM, los detalles se copiarán en las nuevas ubicaciones.

#### Ubicaciones - Iniciadores de flujo de trabajo {#locations-workflow-launchers}

Las definiciones del iniciador de flujo de trabajo también se almacenan en el repositorio según el tipo:

* Los lanzadores de flujo de trabajo listos para usar se encuentran en la siguiente ruta:

   `/libs/settings/workflow/launcher/`

   >[!CAUTION]
   >
   >No:
   >
   >* colocar cualquiera de los iniciadores de flujo de trabajo personalizados en esta carpeta
   >* editar cualquier elemento de `/libs`
   >
   >Como cualquier cambio se puede sobrescribir al actualizar o al instalar correcciones urgentes, paquetes de correcciones acumulativas o Service Packs.

* Los lanzadores de flujo de trabajo personalizados se encuentran en:

   ```
   /conf/global/settings/workflow/launcher/...
   ```

* Los iniciadores de flujo de trabajo heredados se mantienen en la siguiente ruta:

   `/etc/workflow/launcher/`

   >[!NOTE]
   >
   >Si estas definiciones se editan *mediante la interfaz de usuario* de AEM, los detalles se copiarán en las nuevas ubicaciones.

#### Ubicaciones: secuencias de comandos de flujo de trabajo {#locations-workflow-scripts}

Las secuencias de comandos de flujo de trabajo también se almacenan en el repositorio según el tipo:

* Las secuencias de comandos de flujo de trabajo integradas se mantienen en la siguiente ruta:

   `/libs/workflow/scripts/`

   >[!CAUTION]
   >
   >No:
   >
   >* coloque cualquiera de las secuencias de comandos de flujo de trabajo personalizadas en esta carpeta
   >* editar cualquier elemento de `/libs`
   >
   >Como cualquier cambio se puede sobrescribir al actualizar o al instalar correcciones urgentes, paquetes de correcciones acumulativas o Service Packs.

* Las secuencias de comandos de flujo de trabajo personalizadas se incluyen en:

   ```
   /apps/workflow/scripts/...
   ```

* Las secuencias de comandos de flujo de trabajo heredadas se mantienen en la siguiente ruta:

   `/etc/workflow/scripts/`

#### Ubicaciones: notificaciones de flujo de trabajo {#locations-workflow-notifications}

Las notificaciones de flujo de trabajo también se almacenan en el repositorio según el tipo:

* Las definiciones de notificación de flujo de trabajo integradas se mantienen en la siguiente ruta:

   `/libs/settings/workflow/notification/`

   >[!CAUTION]
   >
   >No:
   >
   >* coloque cualquiera de las definiciones de notificación de flujo de trabajo personalizadas en esta carpeta
   >* editar cualquier elemento de `/libs`
   >
   >Como cualquier cambio se puede sobrescribir al actualizar o al instalar correcciones urgentes, paquetes de correcciones acumulativas o Service Packs.

* Las definiciones de notificación de flujo de trabajo personalizado se encuentran en:

   ```
   /conf/global/settings/workflow/notification/...
   ```

   >[!NOTE]
   >
   >Si desea anular un texto de notificación de flujo de trabajo, cree una ruta superpuesta en:
   >
   >
   >`/conf/global/settings/workflow/notification/<path-under-libs>`

* Las definiciones de notificación de flujo de trabajo heredadas se mantienen en la siguiente ruta:

   `/etc/workflow/notification/`

### Sesiones de proceso {#process-sessions}

Como en cualquier desarrollo personalizado, siempre se recomienda utilizar una sesión de usuario cuando sea posible:

* para la mejor conformidad con las directrices de seguridad
* permitir que el sistema gestione la apertura y cierre de la sesión

Al implementar un proceso de flujo de trabajo:

* Se proporcionará una sesión de flujo de trabajo que debe utilizarse a menos que haya una razón de peso para no hacerlo.
* Las sesiones nuevas no deben crearse a partir de pasos de flujo de trabajo, ya que esto provoca incoherencias en los estados junto con posibles problemas de concurrencia en el motor de flujo de trabajo.
* No debe adquirir una nueva sesión de JCR desde un paso de proceso en un flujo de trabajo; debe adaptar la sesión de flujo de trabajo proporcionada por la API de paso de proceso a una sesión jcr. Por ejemplo:

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

Guardar una sesión:

* Dentro de un proceso de flujo de trabajo, si `WorkflowSession` se utiliza para modificar el repositorio, no guarde explícitamente la sesión; el flujo de trabajo guardará la sesión cuando se complete.
* `Session.Save` no se debe llamar desde dentro de un paso de flujo de trabajo:

   * se recomienda adaptar la sesión jcr del flujo de trabajo; no `save` es necesario, ya que el motor de flujo de trabajo guarda la sesión automáticamente una vez que el flujo de trabajo ha terminado de ejecutarse.
   * no se recomienda para un paso de proceso crear su propia sesión de jcr.

* Al eliminar los ahorros innecesarios, puede reducir la sobrecarga y, por lo tanto, aumentar la eficacia de los flujos de trabajo.

>[!CAUTION]
>
>Si, a pesar de las recomendaciones aquí, crea su propia sesión de jcr, deberá guardarla.

### Minimizar el número y el alcance de los lanzadores {#minimize-the-number-scope-of-launchers}

Hay un detector responsable de todos los lanzadores [de](/help/sites-administering/workflows-starting.md#workflows-launchers) flujo de trabajo registrados:

* Escuchará los cambios en todas las rutas especificadas en las propiedades de globalización de los otros lanzadores.
* Cuando se envía un evento, el motor de flujo de trabajo evaluará cada iniciador para determinar si debe ejecutarse.

La creación de demasiados lanzadores hará que el proceso de evaluación se ejecute más lentamente.

La creación de una ruta de acceso de globalización en la raíz del repositorio en un único iniciador haría que el motor de flujo de trabajo escuchara y evaluara eventos de creación/modificación en cada nodo del repositorio. Por este motivo, se recomienda crear únicamente lanzadores que sean necesarios y hacer que la ruta de globalización sea lo más específica posible.

Debido al impacto de estos lanzadores en el comportamiento del flujo de trabajo, también puede resultar útil desactivar cualquier iniciador incorporado que no esté en uso.

### Mejoras de configuración para lanzadores {#configuration-enhancements-for-launchers}

La configuración [del](/help/sites-administering/workflows-starting.md#workflows-launchers) iniciador personalizado se ha mejorado para admitir lo siguiente:

* Tener múltiples condiciones &quot;AND&quot; juntas.
* Tener condiciones OR en una sola condición.
* Desactive o active los lanzadores en función de si un indicador de función está habilitado o deshabilitado.
* Admite regex en condiciones de lanzador.

### No iniciar flujos de trabajo de otros flujos de trabajo {#do-not-start-workflows-from-other-workflows}

Los flujos de trabajo pueden soportar una considerable cantidad de sobrecarga, tanto en términos de objetos creados en memoria como de nodos rastreados en el repositorio. Por este motivo, es mejor que un flujo de trabajo realice su procesamiento en sí mismo en lugar de iniciar flujos de trabajo adicionales.

Un ejemplo de esto sería un flujo de trabajo que implementa un proceso comercial en un conjunto de contenido y luego activa dicho contenido. Es mejor crear un proceso de flujo de trabajo personalizado que active cada uno de estos nodos, en lugar de iniciar un modelo de **activación de contenido** para cada uno de los nodos de contenido que necesita publicarse. Este método requerirá trabajo de desarrollo adicional, pero es más eficaz cuando se ejecuta que cuando se inicia una instancia de flujo de trabajo independiente para cada activación.

Otro ejemplo sería un flujo de trabajo que procesa varios nodos, crea un paquete de workflow y, a continuación, activa dicho paquete. En lugar de crear el paquete y luego iniciar un flujo de trabajo independiente con el paquete como carga útil, puede cambiar la carga útil del flujo de trabajo en el paso que crea el paquete y, a continuación, llamar al paso para activar el paquete dentro del mismo modelo de flujo de trabajo.

### Avance de controlador {#handler-advance}

Al diseñar un modelo de flujo de trabajo, tiene la opción de habilitar el avance del controlador en los pasos del flujo de trabajo. También puede agregar código al paso del flujo de trabajo para determinar qué paso debe ejecutarse a continuación y luego ejecutarlo.

Se recomienda utilizar el avance de los controladores para ofrecer un mejor rendimiento.

### Etapas del flujo de trabajo {#workflow-stages}

Puede definir las etapas [del](/help/sites-developing/workflows.md#workflow-stages)flujo de trabajo y, a continuación, asignar tareas/pasos a una fase específica del flujo de trabajo.

Esta información se utiliza para mostrar el progreso de un flujo de trabajo al hacer clic en la ficha Información [**del **flujo de trabajo de un elemento de trabajo desde la** Bandeja de entrada **](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions). Los modelos de flujo de trabajo existentes se pueden editar para agregar etapas.

### Activar paso del proceso de página {#activate-page-process-step}

El paso **Activar proceso** de página activará las páginas por usted, pero no buscará automáticamente ningún recurso DAM referenciado ni tampoco los activará.

Esto es algo que hay que tener en cuenta si piensa utilizar este paso como parte de un modelo de flujo de trabajo.

### Consideraciones de actualización {#upgrade-considerations}

Al actualizar la instancia:

* asegúrese de que se realiza una copia de seguridad de los modelos de flujo de trabajo personalizados antes de actualizar una instancia.
* confirme que ninguno de los flujos de trabajo personalizados se almacena en la [ubicación](#locations):

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>Consulte también Reestructuración [del repositorio en AEM 6.5](/help/sites-deploying/repository-restructuring.md).

## Herramientas del sistema {#system-tools}

Existen muchas herramientas del sistema disponibles para ayudar con la supervisión, el mantenimiento y la solución de problemas de los flujos de trabajo. Todas las direcciones URL de ejemplo siguientes utilizan `localhost:4502`pero deben estar disponibles en cualquier instancia de autor ( `<hostname>:<port>`).

### Sling Job Handling Console {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

La consola de Sling Job Handling mostrará:

* Estadísticas sobre el estado de los trabajos en el sistema desde el último reinicio.
* También mostrará las configuraciones de todas las colas de trabajos y proporcionará un método abreviado para editarlas en el administrador de configuración.

### Herramienta de informes de flujo de trabajo {#workflow-report-tool}

La herramienta de generación de informes de flujo de trabajo se está eliminando en la versión 6.3 para evitar la degradación del rendimiento.

### MBean de operaciones de mantenimiento de flujo de trabajo {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

El MBean de mantenimiento del flujo de trabajo expone varias rutinas de mantenimiento útiles, como purgar flujos de trabajo completados y recuperar estadísticas del flujo de trabajo.

## Información adicional {#further-information}

Para obtener más información, consulte:

* [Uso de flujos de trabajo](/help/sites-authoring/workflows.md)
* [Administración de flujos de trabajo](/help/sites-administering/workflows.md)
* [Desarrollo y ampliación de flujos de trabajo](/help/sites-developing/workflows.md)
* [Optimización del rendimiento](/help/sites-deploying/configuring-performance.md)