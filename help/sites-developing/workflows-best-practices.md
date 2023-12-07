---
title: Prácticas recomendadas de flujo de trabajo
description: Conozca las prácticas recomendadas para trabajar con flujos de trabajo en Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 14775476-6fe5-4583-8ab5-b55fef892174
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1925'
ht-degree: 1%

---

# Prácticas recomendadas de flujo de trabajo{#workflow-best-practices}

Los flujos de trabajo permiten automatizar las actividades de Adobe Experience Manager AEM ().

AEM A menudo representan una gran cantidad del procesamiento que se produce en un entorno de trabajo de la, por lo que cuando los pasos personalizados del flujo de trabajo no se escriben según las prácticas recomendadas o los flujos de trabajo listos para usar no están configurados para ejecutarse de la manera más eficiente posible, el sistema puede sufrir las consecuencias.

Por lo tanto, es muy recomendable planificar cuidadosamente las implementaciones de los flujos de trabajo.

## Configuración {#configuration}

Al configurar los procesos de flujo de trabajo (personalizados o predeterminados), hay algunas cosas que deben tenerse en cuenta.

### Flujos de trabajo transitorios {#transient-workflows}

Para optimizar las cargas de ingesta altas, puede definir una [flujo de trabajo como transitorio](/help/sites-developing/workflows.md#transient-workflows).

Cuando un flujo de trabajo es transitorio, los datos de tiempo de ejecución relacionados con los pasos de trabajo intermedios no persisten en el JCR cuando se ejecutan (las representaciones de salida se mantienen).

Las ventajas pueden incluir:

* Reducción en el tiempo de procesamiento del flujo de trabajo de hasta el 10 %.
* Reduzca considerablemente el crecimiento del repositorio.
* No se requieren más flujos de trabajo CRUD para purgar.
* Además, reduce el número de archivos TAR que se van a compactar.

>[!CAUTION]
>
>Si su empresa dicta que los datos de tiempo de ejecución del flujo de trabajo se conservan o archivan con fines de auditoría, no habilite esta función.

### Ajuste de flujos de trabajo DAM {#tuning-dam-workflows}

Para ver las directrices de ajuste del rendimiento para flujos de trabajo de DAM, consulte la [Guía de ajuste de rendimiento de AEM Assets](/help/assets/performance-tuning-guidelines.md).

### Configuración del número máximo de flujos de trabajo simultáneos {#configure-the-maximum-number-of-concurrent-workflows}

AEM Puede permitir que varios subprocesos de flujo de trabajo se ejecuten de forma simultánea. De forma predeterminada, el número de subprocesos está configurado para ser la mitad del número de núcleos de procesador del sistema.

AEM En los casos en los que los flujos de trabajo que se ejecutan requieren recursos del sistema, esto puede significar poco para que se lo utilice en otras tareas, como procesar la interfaz de usuario de creación. Como resultado, el sistema puede resultar lento durante actividades como la carga masiva de imágenes.

Para solucionar este problema, el Adobe recomienda configurar el número de **Máximo de trabajos paralelos** que se sitúe entre la mitad y las tres cuartas partes del número de núcleos de procesador del sistema. Esto debería permitir suficiente capacidad para que el sistema mantenga su capacidad de respuesta al procesar estos flujos de trabajo.

Para configurar **Máximo de trabajos paralelos**, puede hacer lo siguiente:

* Configure las variables **[Configuración de OSGi](/help/sites-deploying/configuring-osgi.md)** AEM desde la consola web de; para **Cola: Cola de flujo de trabajo de Granite** (an) **Configuración de cola de trabajos de Apache Sling**).

* Configure la cola desde el **Trabajos de Sling** AEM opción de la consola web de; para **Configuración de cola de trabajos: cola de flujo de trabajo de Granite**, en `http://localhost:4502/system/console/slingevent`.

Además, hay una configuración independiente para **Cola de trabajos de proceso externo de Granite Workflow**. Se utiliza para procesos de flujo de trabajo que inician binarios externos como **InDesign Server** o **Imagen Magick**.

### Configurar colas de trabajos individuales {#configure-individual-job-queues}

En algunos casos, resulta útil configurar colas de trabajos individuales para controlar los subprocesos simultáneos u otras opciones de cola de forma individual. Puede agregar y configurar una cola individual desde la consola web a través de **Configuración de cola de trabajos de Apache Sling** de fábrica. Para encontrar el tema adecuado que enumerar, ejecute el modelo del flujo de trabajo y búsquelo en la **Trabajos de Sling** consola; por ejemplo, en `http://localhost:4502/system/console/slingevent`.

También se pueden agregar colas de trabajos individuales para flujos de trabajo transitorios.

### Configurar depuración de flujo de trabajo {#configure-workflow-purging}

AEM En una instalación estándar, proporciona una consola de mantenimiento en la que se pueden programar y configurar actividades de mantenimiento diarias y semanales; por ejemplo, en:

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

De forma predeterminada, la variable **Ventana de mantenimiento semanal** tiene un **Depuración de flujo de trabajo** , pero esto debe configurarse antes de que se ejecute. Para configurar las depuraciones del flujo de trabajo, cree un nuevo **Configuración de depuración del flujo de trabajo de Adobe Granite** debe añadirse en la consola web.

AEM Para obtener más información sobre las tareas de mantenimiento en la, consulte la [Tablero de operaciones](/help/sites-administering/operations-dashboard.md).

## Personalización {#customization}

Al escribir procesos de flujo de trabajo personalizados, hay algunas cosas que deben tenerse en cuenta.

### Ubicaciones {#locations}

Las definiciones de modelos de flujo de trabajo, iniciadores, scripts y notificaciones se mantienen en el repositorio según el tipo; es decir, listas para usar, personalizadas, entre otros.

>[!NOTE]
>
>Consulte también [AEM Reestructuración de repositorios en 6.5](/help/sites-deploying/repository-restructuring.md).

#### Ubicaciones - Modelos de flujo de trabajo {#locations-workflow-models}

Los modelos de flujo de trabajo se almacenan en el repositorio según el tipo:

* Los diseños de flujo de trabajo listos para usar se mantienen en la siguiente ruta:

  `/libs/settings/workflow/models/`

  >[!CAUTION]
  >
  >No haga lo siguiente:
  >
  >* coloque cualquiera de los modelos de flujo de trabajo personalizados en esta carpeta
  >* editar cualquier elemento en `/libs`
  >
  >Como cualquier cambio puede sobrescribirse durante la actualización o al instalar correcciones rápidas, paquetes de correcciones acumulativos o paquetes de servicio.

* Los diseños de flujo de trabajo personalizados se encuentran en:

  ```
  /conf/global/settings/workflow/models/...
  ```

* Los diseños de flujo de trabajo de tiempo de ejecución (tanto predeterminados como personalizados) se mantienen en la siguiente ruta:

  `/var/workflow/models/`

* Los diseños de flujo de trabajo heredados (tanto en tiempo de diseño como en tiempo de ejecución) se mantienen en la siguiente ruta:

  `/etc/workflow/models/`

  >[!NOTE]
  >
  >Si estos diseños se editan *AEM uso de la IU de*, los detalles se copiarán en las nuevas ubicaciones.

#### Ubicaciones - Iniciadores de flujo de trabajo {#locations-workflow-launchers}

Las definiciones del lanzador de flujos de trabajo también se almacenan en el repositorio según el tipo:

* Los iniciadores de flujo de trabajo listos para usar se mantienen en la siguiente ruta:

  `/libs/settings/workflow/launcher/`

  >[!CAUTION]
  >
  >No haga lo siguiente:
  >
  >* coloque cualquiera de los iniciadores de flujo de trabajo personalizados en esta carpeta
  >* editar cualquier elemento en `/libs`
  >
  >Como cualquier cambio puede sobrescribirse durante la actualización o al instalar correcciones rápidas, paquetes de correcciones acumulativos o paquetes de servicio.

* Los iniciadores de flujo de trabajo personalizados se encuentran en:

  ```
  /conf/global/settings/workflow/launcher/...
  ```

* Los iniciadores de flujos de trabajo heredados se mantienen en la siguiente ruta:

  `/etc/workflow/launcher/`

  >[!NOTE]
  >
  >Si se editan estas definiciones *AEM uso de la IU de*, los detalles se copiarán en las nuevas ubicaciones.

#### Ubicaciones - Scripts de flujo de trabajo {#locations-workflow-scripts}

Los scripts de flujo de trabajo también se almacenan en el repositorio según el tipo:

* Los scripts de flujo de trabajo listos para usar se mantienen en la siguiente ruta:

  `/libs/workflow/scripts/`

  >[!CAUTION]
  >
  >No haga lo siguiente:
  >
  >* coloque cualquiera de los scripts de flujo de trabajo personalizados en esta carpeta
  >* editar cualquier elemento en `/libs`
  >
  >Como cualquier cambio puede sobrescribirse durante la actualización o al instalar correcciones rápidas, paquetes de correcciones acumulativos o paquetes de servicio.

* Los scripts de flujo de trabajo personalizados se encuentran en:

  ```
  /apps/workflow/scripts/...
  ```

* Los scripts de flujo de trabajo heredados se mantienen en la siguiente ruta:

  `/etc/workflow/scripts/`

#### Ubicaciones - Notificaciones de flujo de trabajo {#locations-workflow-notifications}

Las notificaciones de flujo de trabajo también se almacenan en el repositorio según el tipo:

* Las definiciones de notificaciones de flujo de trabajo listas para usar se mantienen en la siguiente ruta:

  `/libs/settings/workflow/notification/`

  >[!CAUTION]
  >
  >No haga lo siguiente:
  >
  >* coloque cualquiera de las definiciones de notificación de flujo de trabajo personalizadas en esta carpeta
  >* editar cualquier elemento en `/libs`
  >
  >Como cualquier cambio puede sobrescribirse durante la actualización o al instalar correcciones rápidas, paquetes de correcciones acumulativos o paquetes de servicio.

* Las definiciones de notificaciones de flujo de trabajo personalizadas se encuentran en:

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

Como en cualquier desarrollo personalizado, siempre se recomienda utilizar una sesión del usuario cuando sea posible:

* para un mejor cumplimiento de las directrices de seguridad
* para permitir que el sistema administre la apertura y el cierre de la sesión

Al implementar un proceso de flujo de trabajo:

* Se proporcionará una sesión de flujo de trabajo que se debe utilizar a menos que haya una razón de peso para no hacerlo.
* No se deben crear nuevas sesiones a partir de los pasos del flujo de trabajo, ya que esto provoca incoherencias en los estados junto con posibles problemas de concurrencia en el motor de flujos de trabajo.
* No debe adquirir una nueva sesión JCR desde un paso de proceso en un flujo de trabajo; debe adaptar la sesión de flujo de trabajo proporcionada por la API de paso de proceso a una sesión JCR. Por ejemplo:

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

Guardar una sesión:

* Dentro de un proceso de flujo de trabajo, si la variable `WorkflowSession` se está utilizando para modificar el repositorio y, a continuación, no guarde la sesión explícitamente: el flujo de trabajo guardará la sesión cuando se complete.
* `Session.Save` no se debe llamar desde un paso del flujo de trabajo:

   * se recomienda adaptar la sesión jcr del flujo de trabajo; a continuación, `save` no es necesario, ya que el motor de flujos de trabajo guarda la sesión automáticamente una vez que el flujo de trabajo ha terminado de ejecutarse.
   * no se recomienda que un paso de proceso cree su propia sesión jcr.

* Al eliminar los ahorros innecesarios, puede reducir la sobrecarga y, por lo tanto, hacer que los flujos de trabajo sean más eficientes.

>[!CAUTION]
>
>Si, a pesar de las recomendaciones aquí, crea su propia sesión jcr, se debe guardar.

### Minimizar el número/ámbito de los lanzadores {#minimize-the-number-scope-of-launchers}

Hay un oyente que es responsable de todas las [iniciadores de flujo de trabajo](/help/sites-administering/workflows-starting.md#workflows-launchers) que están registrados:

* Escuchará los cambios en todas las rutas especificadas en las propiedades de globalización de los otros lanzadores.
* Cuando se envía un evento, el motor de flujo de trabajo evalúa cada iniciador para determinar si debe ejecutarse.

Si crea demasiados iniciadores, el proceso de evaluación se ejecutará más lentamente.

La creación de una ruta globbing en la raíz del repositorio en un único lanzador haría que el motor de flujos de trabajo escuchara y evaluara los eventos create/modify en cada nodo del repositorio. Por este motivo, se recomienda crear únicamente iniciadores necesarios y hacer que la ruta de globalización sea lo más específica posible.

Debido al impacto de estos iniciadores en el comportamiento del flujo de trabajo, también puede resultar útil deshabilitar cualquier lanzador predeterminado que no esté en uso.

### Mejoras en la configuración de los lanzadores {#configuration-enhancements-for-launchers}

El personalizado [configuración del lanzador](/help/sites-administering/workflows-starting.md#workflows-launchers) se ha mejorado para admitir lo siguiente:

* Tienen múltiples condiciones &quot;Y&quot; juntas.
* Tener condiciones O dentro de una sola condición.
* Deshabilitar/habilitar iniciadores en función de si un indicador de funcionalidad está habilitado o deshabilitado.
* Compatibilidad con regex en condiciones de lanzador.

### No iniciar flujos de trabajo desde otros flujos de trabajo {#do-not-start-workflows-from-other-workflows}

Los flujos de trabajo pueden conllevar una cantidad significativa de sobrecarga, tanto en términos de objetos creados en memoria como de nodos rastreados en el repositorio. Por este motivo, es mejor que un flujo de trabajo realice su procesamiento dentro de sí mismo en lugar de iniciar flujos de trabajo adicionales.

Un ejemplo de esto sería un flujo de trabajo que implementa un proceso empresarial en un conjunto de contenido y luego activa ese contenido. Es mejor crear un proceso de flujo de trabajo personalizado que active cada uno de estos nodos, en lugar de iniciar un **Activar contenido** modelo para cada uno de los nodos de contenido que deben publicarse. Este método requerirá un trabajo de desarrollo adicional, pero es más eficaz cuando se ejecuta que iniciar una instancia de flujo de trabajo independiente para cada activación.

Otro ejemplo sería un flujo de trabajo que procese varios nodos, cree un paquete de flujo de trabajo y active dicho paquete. En lugar de crear el paquete y luego iniciar un flujo de trabajo independiente con el paquete como carga útil, puede cambiar la carga útil del flujo de trabajo en el paso que crea el paquete y luego llamar al paso para activar el paquete dentro del mismo modelo de flujo de trabajo.

### Avance de controlador {#handler-advance}

Al diseñar un modelo del flujo de trabajo, tiene la opción de habilitar el avance del controlador en los pasos del flujo de trabajo. Como alternativa, puede agregar código al paso del flujo de trabajo para determinar qué paso se debe ejecutar a continuación y, a continuación, ejecutarlo.

Se recomienda utilizar el avance del controlador, ya que ofrece un mejor rendimiento.

### Fases del flujo de trabajo {#workflow-stages}

Puede definir [fases del flujo de trabajo](/help/sites-developing/workflows.md#workflow-stages), luego asigne tareas/pasos a una fase específica del flujo de trabajo.

Esta información se utiliza para mostrar el progreso de un flujo de trabajo al hacer clic en [**Información de flujo de trabajo** de un elemento de trabajo de la **Bandeja de entrada**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions). Los modelos de flujo de trabajo existentes se pueden editar para añadir fases.

### Activar etapa de proceso de página {#activate-page-process-step}

El **Activar proceso de página** Este paso activará las páginas por usted, pero no encontrará automáticamente ningún recurso DAM al que se haga referencia ni los activará también.

Es algo que debe tener en cuenta si planea utilizar este paso como parte de un modelo del flujo de trabajo.

### Consideraciones de actualización {#upgrade-considerations}

Al actualizar la instancia:

* asegúrese de que se realiza una copia de seguridad de todos los modelos de flujo de trabajo personalizados antes de actualizar una instancia.
* confirme que ninguno de los flujos de trabajo personalizados se almacena en la variable [ubicación](#locations):

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>Consulte también [AEM Reestructuración de repositorios en 6.5](/help/sites-deploying/repository-restructuring.md).

## Herramientas del sistema {#system-tools}

Hay muchas herramientas del sistema disponibles para ayudar con la monitorización, el mantenimiento y la resolución de problemas de los flujos de trabajo. Todas las URL de ejemplo siguientes utilizan `localhost:4502`, pero debería estar disponible en cualquier instancia de autor ( `<hostname>:<port>`).

### Consola de administración de trabajos Sling {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

La consola de administración de trabajos de Sling mostrará lo siguiente:

* Estadísticas sobre el estado de los trabajos en el sistema desde el último reinicio.
* También mostrará las configuraciones de todas las colas de trabajos y proporcionará un acceso directo para editarlas en el administrador de configuración.

### Herramienta Informe de flujo de trabajo {#workflow-report-tool}

La herramienta de creación de informes de flujo de trabajo se ha eliminado en la versión 6.3 para evitar una degradación del rendimiento.

### MBean de operaciones de mantenimiento de flujo de trabajo {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

El MBean de mantenimiento del flujo de trabajo expone varias rutinas de mantenimiento útiles, como la depuración de flujos de trabajo completados y la recuperación de estadísticas de flujo de trabajo.

## Información adicional {#further-information}

Para obtener más información, consulte lo siguiente:

* [Uso de flujos de trabajo](/help/sites-authoring/workflows.md)
* [Administración de flujos de trabajo](/help/sites-administering/workflows.md)
* [Desarrollo y ampliación de flujos de trabajo](/help/sites-developing/workflows.md)
* [Optimización del rendimiento](/help/sites-deploying/configuring-performance.md)
