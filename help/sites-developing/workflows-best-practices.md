---
title: Prácticas recomendadas del flujo de trabajo
seo-title: Prácticas recomendadas del flujo de trabajo
description: Prácticas recomendadas del flujo de trabajo
seo-description: nulo
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1924'
ht-degree: 1%

---


# Prácticas recomendadas del flujo de trabajo{#workflow-best-practices}

Los flujos de trabajo permiten automatizar las actividades de Adobe Experience Manager (AEM).

A menudo representan una gran cantidad del procesamiento que se produce en un entorno de AEM, por lo que cuando los pasos de flujo de trabajo personalizados no se escriben según las prácticas recomendadas o los flujos de trabajo listos para usar no están configurados para ejecutarse de la manera más eficiente posible, el sistema puede verse afectado como resultado.

Por lo tanto, se recomienda planificar cuidadosamente las implementaciones de los flujos de trabajo.

## Configuración {#configuration}

Al configurar los procesos de flujo de trabajo (personalizados o predeterminados), hay que tener en cuenta algunas cosas.

### Flujos de trabajo transitorios {#transient-workflows}

Para optimizar las cargas de ingesta alta, puede definir un flujo de trabajo [como transitorio](/help/sites-developing/workflows.md#transient-workflows).

Cuando un flujo de trabajo es transitorio, los datos de tiempo de ejecución relacionados con los pasos de trabajo intermedios no se mantienen en el JCR cuando se ejecutan (las representaciones de salida se mantienen, por supuesto).

Las ventajas pueden incluir:

* Reducción del tiempo de procesamiento del flujo de trabajo; de hasta el 10 %.
* Reduzca considerablemente el crecimiento del repositorio.
* No se necesitan más flujos de trabajo CRUD para purgar.
* Además, reduce el número de archivos TAR a compactos.

>[!CAUTION]
>
>Si su empresa dicta que persiste o archiva los datos de tiempo de ejecución del flujo de trabajo para fines de auditoría, no habilite esta función.

### Ajuste de los flujos de trabajo de DAM {#tuning-dam-workflows}

Para ver las directrices de ajuste del rendimiento para los flujos de trabajo DAM, consulte la [Guía de ajuste del rendimiento de AEM Assets](/help/assets/performance-tuning-guidelines.md).

### Configurar el número máximo de flujos de trabajo simultáneos {#configure-the-maximum-number-of-concurrent-workflows}

AEM permitir que varios subprocesos de flujo de trabajo se ejecuten simultáneamente. De forma predeterminada, el número de subprocesos está configurado para ser la mitad del número de núcleos de procesador en el sistema.

En los casos en los que los flujos de trabajo que se ejecutan exigen recursos del sistema, esto puede significar que queda poco para que AEM utilice para otras tareas, como renderizar la interfaz de usuario de creación. Como resultado, el sistema puede ser lento durante actividades como la carga masiva de imágenes.

Para solucionar este problema, Adobe recomienda configurar el número de **Trabajos paralelos máximos** para que esté entre la mitad y las tres cuartas partes del número de núcleos de procesador en el sistema. Esto debería permitir suficiente capacidad para que el sistema siga respondiendo al procesar estos flujos de trabajo.

Para configurar **Máximo de trabajos paralelos**, puede:

* Configure la **[Configuración de OSGi](/help/sites-deploying/configuring-osgi.md)** desde la consola web AEM; para **Cola: Cola de flujo de trabajo de Granite** (una **Configuración de cola de trabajos de Apache Sling**).

* Configure la cola puede desde la opción **Sling Jobs** de la consola web AEM; para **Configuración de cola de trabajo: Cola de flujo de trabajo de Granite**, en `http://localhost:4502/system/console/slingevent`.

Además, existe una configuración independiente para la **cola de trabajos de proceso externo de Granite Workflow**. Se utiliza para procesos de flujo de trabajo que inician binarios externos, como **InDesign Server** o **Image Magick**.

### Configurar colas de trabajos individuales {#configure-individual-job-queues}

En algunos casos, es útil configurar colas de trabajos individuales para controlar los subprocesos simultáneos u otras opciones de cola, de forma individual. Puede añadir y configurar una cola individual desde la consola web a través de la fábrica **Apache Sling Job Queue Configuration**. Para encontrar el tema adecuado a la lista, ejecute el modelo del flujo de trabajo y búsquelo en la consola **Sling Jobs**; por ejemplo, en `http://localhost:4502/system/console/slingevent`.

También se pueden agregar colas de trabajos individuales para flujos de trabajo transitorios.

### Configurar la purga del flujo de trabajo {#configure-workflow-purging}

En una instalación estándar AEM proporciona una consola de mantenimiento en la que se pueden programar y configurar las actividades de mantenimiento diarias y semanales; por ejemplo, en:

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

De forma predeterminada, la **Ventana de mantenimiento semanal** tiene una tarea **Depuración del flujo de trabajo**, pero esto debe configurarse antes de que se ejecute. Para configurar las purgas del flujo de trabajo, se debe agregar una nueva **Configuración de purga del flujo de trabajo de Granite de Adobe** en la consola web.

Para obtener más información sobre las tareas de mantenimiento en AEM, consulte [Operations Dashboard](/help/sites-administering/operations-dashboard.md).

## Personalización {#customization}

Al escribir procesos de flujo de trabajo personalizados, hay que tener en cuenta algunas cosas.

### Ubicaciones {#locations}

Las definiciones de modelos de flujo de trabajo, lanzadores, secuencias de comandos y notificaciones se mantienen en el repositorio según el tipo; es decir, preestablecido, personalizado, entre otros.

>[!NOTE]
>
>Consulte también [Reestructuración del repositorio en AEM 6.5](/help/sites-deploying/repository-restructuring.md).

#### Ubicaciones: modelos de flujo de trabajo {#locations-workflow-models}

Los modelos de flujo de trabajo se almacenan en el repositorio según el tipo:

* Los diseños de flujo de trabajo listos para usar se mantienen en la siguiente ruta:

   `/libs/settings/workflow/models/`

   >[!CAUTION]
   >
   >No:
   >
   >* coloque cualquiera de los modelos de flujo de trabajo personalizados en esta carpeta
   >* editar cualquier cosa en `/libs`

   >
   >Como cualquier cambio se puede sobrescribir en la actualización o al instalar correcciones, paquetes fijos acumulativos o paquetes de servicio.

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
   >Si estos diseños se editan *mediante la IU AEM*, los detalles se copiarán en las nuevas ubicaciones.

#### Ubicaciones: iniciadores de flujo de trabajo {#locations-workflow-launchers}

Las definiciones del iniciador de flujo de trabajo también se almacenan en el repositorio según el tipo:

* Los lanzadores de flujo de trabajo listos para usar se mantienen en la siguiente ruta:

   `/libs/settings/workflow/launcher/`

   >[!CAUTION]
   >
   >No:
   >
   >* coloque cualquiera de los iniciadores de flujo de trabajo personalizados en esta carpeta
   >* editar cualquier cosa en `/libs`

   >
   >Como cualquier cambio se puede sobrescribir en la actualización o al instalar correcciones, paquetes fijos acumulativos o paquetes de servicio.

* Los iniciadores de flujo de trabajo personalizados se incluyen en:

   ```
   /conf/global/settings/workflow/launcher/...
   ```

* Los iniciadores de flujo de trabajo heredados se mantienen en la siguiente ruta:

   `/etc/workflow/launcher/`

   >[!NOTE]
   >
   >Si estas definiciones se editan *utilizando la IU AEM*, los detalles se copiarán en las nuevas ubicaciones.

#### Ubicaciones - Scripts de flujo de trabajo {#locations-workflow-scripts}

Los scripts de flujo de trabajo también se almacenan en el repositorio según el tipo:

* Los scripts de flujo de trabajo listos para usar se mantienen en la siguiente ruta:

   `/libs/workflow/scripts/`

   >[!CAUTION]
   >
   >No:
   >
   >* coloque cualquiera de las secuencias de comandos de flujo de trabajo personalizadas en esta carpeta
   >* editar cualquier cosa en `/libs`

   >
   >Como cualquier cambio se puede sobrescribir en la actualización o al instalar correcciones, paquetes fijos acumulativos o paquetes de servicio.

* Los scripts de flujo de trabajo personalizados se mantienen en:

   ```
   /apps/workflow/scripts/...
   ```

* Los scripts de flujo de trabajo heredados se mantienen en la siguiente ruta:

   `/etc/workflow/scripts/`

#### Ubicaciones: Notificaciones de flujo de trabajo {#locations-workflow-notifications}

Las notificaciones de flujo de trabajo también se almacenan en el repositorio según el tipo:

* Las definiciones de notificaciones de flujo de trabajo integradas se mantienen en la siguiente ruta:

   `/libs/settings/workflow/notification/`

   >[!CAUTION]
   >
   >No:
   >
   >* Coloque cualquiera de las definiciones de notificación de flujo de trabajo personalizadas en esta carpeta
   >* editar cualquier cosa en `/libs`

   >
   >Como cualquier cambio se puede sobrescribir en la actualización o al instalar correcciones, paquetes fijos acumulativos o paquetes de servicio.

* Las definiciones de notificaciones de flujo de trabajo personalizadas se incluyen en:

   ```
   /conf/global/settings/workflow/notification/...
   ```

   >[!NOTE]
   >
   >Si desea anular un texto de notificación de flujo de trabajo, cree una ruta superpuesta en:
   >
   >
   >`/conf/global/settings/workflow/notification/<path-under-libs>`

* Las definiciones de notificaciones de flujo de trabajo heredadas se mantienen en la siguiente ruta:

   `/etc/workflow/notification/`

### Sesiones de proceso {#process-sessions}

Como en cualquier desarrollo personalizado, siempre se recomienda utilizar la sesión de un usuario cuando sea posible:

* para el mejor cumplimiento de las directrices de seguridad
* para permitir que el sistema administre la apertura y cierre de la sesión

Al implementar un proceso de flujo de trabajo:

* Se proporcionará una sesión de flujo de trabajo que debe utilizarse a menos que haya una razón convincente para no hacerlo.
* Las nuevas sesiones no deben crearse a partir de pasos de flujo de trabajo, ya que esto causa incoherencias en los estados junto con posibles problemas de concurrencia en el motor del flujo de trabajo.
* No debe adquirir una nueva sesión JCR desde dentro de un paso de proceso en un flujo de trabajo; debe adaptar la sesión de flujo de trabajo proporcionada por la API de paso de proceso a una sesión jcr. Por ejemplo:

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

Guardar una sesión:

* Dentro de un proceso de flujo de trabajo, si el `WorkflowSession` se está utilizando para modificar el repositorio, no guarde explícitamente la sesión: el flujo de trabajo guarda la sesión cuando se completa.
* `Session.Save` no debe llamarse desde un paso de flujo de trabajo:

   * se recomienda adaptar la sesión jcr del flujo de trabajo; luego `save` no es necesario, ya que el motor de flujo de trabajo guarda la sesión automáticamente una vez que el flujo de trabajo ha terminado de ejecutarse.
   * no se recomienda para un paso de proceso crear su propia sesión jcr.

* Al eliminar los ahorros innecesarios, puede reducir la sobrecarga y, por lo tanto, hacer que los flujos de trabajo sean más eficientes.

>[!CAUTION]
>
>Si, a pesar de las recomendaciones aquí, usted crea su propia sesión jcr, entonces tendrá que ser guardada.

### Minimizar el número/alcance de lanzadores {#minimize-the-number-scope-of-launchers}

Hay un oyente que es responsable de todos los [iniciadores de flujo de trabajo](/help/sites-administering/workflows-starting.md#workflows-launchers) registrados:

* Detectará cambios en todas las rutas especificadas en las propiedades de globalización de los otros lanzadores.
* Cuando se envía un evento, el motor de flujo de trabajo evalúa cada lanzador para determinar si debe ejecutarse.

La creación de demasiados lanzadores hará que el proceso de evaluación se ejecute más lentamente.

La creación de una ruta de globalización en la raíz del repositorio en un único lanzador haría que el motor de flujo de trabajo escuchara y evaluara eventos create/modify en cada nodo del repositorio. Por este motivo, se recomienda crear únicamente lanzadores que sean necesarios y hacer que la ruta de globalización sea lo más específica posible.

Debido al impacto de estos lanzadores en el comportamiento del flujo de trabajo, también puede resultar útil deshabilitar cualquier lanzador listo para usar que no esté en uso.

### Mejoras de configuración para lanzadores {#configuration-enhancements-for-launchers}

La configuración personalizada del [iniciador](/help/sites-administering/workflows-starting.md#workflows-launchers) se ha mejorado para admitir lo siguiente:

* Tener múltiples condiciones &quot;AND&quot; terminadas juntas.
* Tener condiciones OR dentro de una sola condición.
* Desactivar/habilitar lanzadores en función de si un indicador de característica está habilitado o deshabilitado.
* Admita regex en condiciones de lanzador.

### No iniciar flujos de trabajo de otros flujos de trabajo {#do-not-start-workflows-from-other-workflows}

Los flujos de trabajo pueden conllevar una gran sobrecarga, tanto en términos de objetos creados en memoria como de nodos rastreados en el repositorio. Por este motivo, es mejor hacer que un flujo de trabajo realice su procesamiento en sí mismo en lugar de iniciar flujos de trabajo adicionales.

Un ejemplo de esto sería un flujo de trabajo que implementa un proceso empresarial en un conjunto de contenido y luego activa ese contenido. Es mejor crear un proceso de flujo de trabajo personalizado que active cada uno de estos nodos, en lugar de iniciar un modelo **Activate Content** para cada uno de los nodos de contenido que debe publicarse. Este método requerirá trabajo de desarrollo adicional, pero es más eficaz cuando se ejecuta que iniciar una instancia de flujo de trabajo independiente para cada activación.

Otro ejemplo sería un flujo de trabajo que procesa varios nodos, crea un paquete de flujo de trabajo y, a continuación, activa dicho paquete. En lugar de crear el paquete y luego iniciar un flujo de trabajo independiente con el paquete como carga útil, puede cambiar la carga útil del flujo de trabajo en el paso que crea el paquete y, a continuación, llamar al paso para activar el paquete dentro del mismo modelo de flujo de trabajo.

### Avance de controlador {#handler-advance}

Al diseñar un modelo de flujo de trabajo, tiene la opción de habilitar el avance del controlador en los pasos del flujo de trabajo. Como alternativa, puede agregar código al paso del flujo de trabajo para determinar qué paso se debe ejecutar a continuación y luego ejecutarlo.

Se recomienda utilizar el avance del controlador, ya que ofrece un mejor rendimiento.

### Etapas de flujo de trabajo {#workflow-stages}

Puede definir [fases del flujo de trabajo](/help/sites-developing/workflows.md#workflow-stages) y luego asignar tareas/pasos a una fase específica del flujo de trabajo.

Esta información se utiliza para mostrar el progreso de un flujo de trabajo al hacer clic en la pestaña [**Workflow Info** de un elemento de trabajo de la **Bandeja de entrada**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions). Los modelos de flujo de trabajo existentes se pueden editar para añadir etapas.

### Activar el paso del proceso de página {#activate-page-process-step}

El paso **Activar proceso de página** activará las páginas por usted, pero no encontrará automáticamente ningún recurso DAM al que se haga referencia y activarlos también.

Esto es algo que se debe tener en cuenta si planea utilizar este paso como parte de un modelo de flujo de trabajo.

### Consideraciones de actualización {#upgrade-considerations}

Al actualizar su instancia:

* asegúrese de que todos los modelos de flujo de trabajo personalizados estén respaldados antes de actualizar una instancia.
* confirme que ninguno de los flujos de trabajo personalizados se almacena en [location](#locations):

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>Consulte también [Reestructuración del repositorio en AEM 6.5](/help/sites-deploying/repository-restructuring.md).

## Herramientas del sistema {#system-tools}

Hay muchas herramientas del sistema disponibles para ayudar con la monitorización, el mantenimiento y la resolución de problemas de los flujos de trabajo. Todas las direcciones URL de ejemplo siguientes utilizan `localhost:4502`, pero deben estar disponibles en cualquier instancia de autor ( `<hostname>:<port>`).

### Consola de administración de trabajos de Sling {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

La consola de Gestión de trabajos de Sling mostrará:

* Estadísticas sobre el estado de los trabajos en el sistema desde el último reinicio.
* También muestra las configuraciones de todas las colas de trabajos y proporciona un método abreviado para editarlas en el administrador de configuración.

### Herramienta Informe de flujo de trabajo {#workflow-report-tool}

La herramienta de informes de flujo de trabajo se está eliminando en la versión 6.3 para evitar la degradación del rendimiento.

### Operaciones de mantenimiento del flujo de trabajo MBean {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

El MBean de mantenimiento del flujo de trabajo expone varias rutinas de mantenimiento útiles, como purgar los flujos de trabajo completados y recuperar las estadísticas del flujo de trabajo.

## Información adicional {#further-information}

Para obtener más información, consulte:

* [Uso de flujos de trabajo](/help/sites-authoring/workflows.md)
* [Administración de flujos de trabajo](/help/sites-administering/workflows.md)
* [Desarrollo y ampliación de flujos de trabajo](/help/sites-developing/workflows.md)
* [Optimización del rendimiento](/help/sites-deploying/configuring-performance.md)