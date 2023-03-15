---
title: Creación de modelos de flujo de trabajo
seo-title: Creating Workflow Models
description: Puede crear un modelo del flujo de trabajo para definir la serie de pasos que se ejecutan cuando un usuario inicia el flujo de trabajo.
seo-description: You create a workflow model to define the series of steps executed when a user starts the workflow.
uuid: 31071d3a-d6d5-4476-9ac0-7b335de406d9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c097b60f-bcdf-45de-babe-b4c2e2b746a1
docset: aem65
exl-id: 6790202f-0542-4779-b3ce-d394cdba77b4
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '2464'
ht-degree: 4%

---

# Creación de modelos de flujo de trabajo{#creating-workflow-models}

>[!CAUTION]
>
>Para utilizar la IU clásica, consulte la [AEM Documentación de.3](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/workflows-models.html) como referencia.

Usted crea un [modelo de flujo de trabajo](/help/sites-developing/workflows.md#model) para definir la serie de pasos que se ejecutan cuando un usuario inicia el flujo de trabajo. También puede definir propiedades del modelo, como si el flujo de trabajo es transitorio o utiliza varios recursos.

Cuando un usuario inicia un flujo de trabajo, se inicia una instancia; este es el modelo de tiempo de ejecución correspondiente, creado al [Sincronización](#sync-your-workflow-generate-a-runtime-model) sus cambios.

## Creación de un nuevo flujo de trabajo {#creating-a-new-workflow}

La primera vez que cree un nuevo modelo de flujo de trabajo, contendrá lo siguiente:

* Los pasos, **Inicio de flujo** y **Fin de flujo**.
Representan el principio y el final del flujo de trabajo. Estos pasos son obligatorios y no se pueden editar ni eliminar.
* Un ejemplo **Participante** paso denominado **Paso 1**.
Este paso está configurado para asignar un elemento de trabajo al iniciador del flujo de trabajo. Edite o elimine este paso y agregue los pasos necesarios.

Para crear un nuevo flujo de trabajo con el editor:

1. Abra el **Modelos de flujo de trabajo** consola; mediante **Herramientas**, **Flujo de trabajo**, **Modelos** o, por ejemplo: [https://localhost:4502/aem/workflow](https://localhost:4502/aem/workflow)
1. Seleccione **Crear** y, a continuación, **Crear modelo**.
1. El **Agregar modelo de flujo de trabajo** aparece el cuadro de diálogo. Introduzca el **Título** y **Nombre** (opcional) antes de seleccionar **Listo**.
1. El nuevo modelo aparece en la lista **Modelos de flujo de trabajo** consola.
1. Seleccione el nuevo flujo de trabajo y utilice [**Editar** para abrirlo y configurarlo](#editinganexistingworkflow):
   ![wf-01](assets/wf-01.png)

>[!NOTE]
>
>Si crea modelos mediante programación (mediante un paquete crx), también puede crear una subcarpeta dentro de:
>
>`/var/workflow/models`
>
>Por ejemplo, `/var/workflow/models/prototypes`. 
>
>Esta carpeta se puede utilizar para lo siguiente [administrar el acceso a los modelos de esa carpeta](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that).

## Edición de un flujo de trabajo {#editing-a-workflow}

Puede editar cualquier modelo de flujo de trabajo existente para:

* [definir pasos](#addingasteptoamodel-) y sus [parámetros](#configuring-a-workflow-step)
* configurar las propiedades del flujo de trabajo, incluyendo [etapas](#configuring-workflow-stages-that-show-workflow-progress), [si el flujo de trabajo es transitorio](#creatingatransientworkflow-) y/o [utiliza varios recursos](#configuring-a-workflow-for-multi-resource-support)

Edición de un [**Predeterminado o heredado** Flujo de trabajo (predeterminado)](#editing-a-default-or-legacy-workflow-for-the-first-time) tiene un paso adicional, para garantizar que una [copia segura](/help/sites-developing/workflows-best-practices.md#locations-workflow-models) se realiza antes de que se realicen los cambios.

Cuando haya completado las actualizaciones del flujo de trabajo, debe utilizar **Sincronización** hasta **Generar un modelo de tiempo de ejecución**. Consulte [Sincronizar el flujo de trabajo](#sync-your-workflow-generate-a-runtime-model) para obtener más información.

### Sincronizar el flujo de trabajo: generar un modelo de tiempo de ejecución {#sync-your-workflow-generate-a-runtime-model}

**Sincronización** (justo en la barra de herramientas del editor) genera un [modelo de tiempo de ejecución](/help/sites-developing/workflows.md#runtime-model). El modelo de tiempo de ejecución es el modelo que se utiliza realmente cuando un usuario inicia un flujo de trabajo. Si no lo hace **Sincronización** Cuando realice los cambios, estos no estarán disponibles durante la ejecución.

Cuando usted (o cualquier otro usuario) realice cambios en el flujo de trabajo, deberá utilizar **Sincronización** para generar un modelo de tiempo de ejecución: incluso cuando los cuadros de diálogo individuales (por ejemplo, para pasos) han tenido sus propias opciones de guardado.

Cuando los cambios se sincronizan con el modelo de tiempo de ejecución (guardado), **Sincronizado** en su lugar.

Algunos pasos tienen campos obligatorios o validación integrada. Cuando no se cumplen estas condiciones, se muestra un error al intentar **Sincronización** el modelo. Por ejemplo, cuando no se ha definido ningún participante para una **Participante** paso:

![wf-21](assets/wf-21.png)

### Edición de un flujo de trabajo predeterminado o heredado por primera vez {#editing-a-default-or-legacy-workflow-for-the-first-time}

Al abrir un [Modelo predeterminado o heredado](/help/sites-developing/workflows.md#workflow-types) para editar:

* El navegador de pasos no está disponible (lado izquierdo).
* Hay un **Editar** acción disponible en la barra de herramientas (lado derecho).
* Inicialmente, el modelo y sus propiedades se presentan en modo de solo lectura como:
   * Los flujos de trabajo predeterminados se encuentran en `/libs`
   * Los flujos de trabajo heredados se encuentran en `/etc`
Seleccionar 
**Editar** hará:
* realice una copia del flujo de trabajo en `/conf`
* Hacer que el explorador de Pasos esté disponible
* permite realizar cambios

>[!NOTE]
>
>Consulte [Ubicaciones de modelos de flujo de trabajo](/help/sites-developing/workflows-best-practices.md#locations-workflow-models) para obtener más información.

![wf-22](assets/wf-22.png)

### Adición de un paso a un modelo {#adding-a-step-to-a-model}

Deberá agregar pasos al modelo para representar la actividad que se va a realizar: cada paso realiza una actividad específica. AEM Hay una selección de componentes de paso disponibles en una instancia de estándar.

Cuando se edita un modelo, los pasos disponibles aparecen en los distintos grupos del **Explorador de pasos**. Por ejemplo:

![wf-10](assets/wf-10.png)

>[!NOTE]
>
>AEM Para obtener información sobre los componentes de paso principales que se instalan con, consulte la sección sobre componentes de paso de la interfaz de usuario de, que se encuentra en la sección [Referencia de pasos del flujo de trabajo](/help/sites-developing/workflows-step-ref.md).

Para agregar pasos al modelo de flujo de trabajo:

1. Abra un modelo de flujo de trabajo existente para editarlo. Desde el **Modelo de flujos de trabajo** consola, seleccione el modelo requerido y, a continuación, **Editar**.
1. Abra el explorador de Pasos; usando **Alternar panel lateral**, en el extremo izquierdo de la barra de herramientas superior. Aquí puede hacer lo siguiente:

   * **Filtrar** para pasos específicos.
   * Utilice el selector desplegable para limitar la selección a un grupo específico de pasos.
   * Seleccione el icono Mostrar descripción ![wf-stepinfo-icon](assets/wf-stepinfo-icon.png) para mostrar más detalles sobre el paso correspondiente.

   ![wf-02](assets/wf-02.png)

1. Arrastre los pasos adecuados a la ubicación requerida en el modelo.

   Por ejemplo, una **Etapa de participante**.

   Una vez añadido al flujo, puede hacer lo siguiente [configuración del paso](#configuring-a-workflow-step).

   ![wf-03](assets/wf-03.png)

1. Añada tantos pasos u otras actualizaciones como sea necesario.

   En tiempo de ejecución, los pasos se ejecutan en el orden en que aparecen en el modelo. Después de añadir componentes de paso, puede arrastrarlos a una ubicación diferente en el modelo.

   También puede copiar, cortar, pegar, agrupar o eliminar pasos existentes, como con el [editor de páginas.](/help/sites-authoring/editing-content.md)

   Los pasos de división también se pueden contraer o expandir mediante la opción de la barra de herramientas: ![wf-collapseexpand-toolbar-icon](assets/wf-collapseexpand-toolbar-icon.png)

1. Confirme los cambios con **Sincronización** (barra de herramientas del editor) para generar el modelo de tiempo de ejecución.

   Consulte [Sincronizar el flujo de trabajo](#sync-your-workflow-generate-a-runtime-model) para obtener más información.

### Configuración de un paso de flujo de trabajo {#configuring-a-workflow-step}

Puede **Configurar** y personalizar el comportamiento de un paso del flujo de trabajo mediante la variable **Propiedades del paso** diálogos.

1. Para abrir **Propiedades del paso** para ver un paso:

   * Pulse o haga clic en el paso * * del modelo de flujo de trabajo y seleccione **Configurar** en la barra de herramientas de componentes.

   * Haga doble clic en el paso.
   >[!NOTE]
   >
   >AEM Para obtener información sobre los componentes de paso principales que se instalan con, consulte la sección sobre componentes de paso de la interfaz de usuario de, que se encuentra en la sección [Referencia de pasos del flujo de trabajo](/help/sites-developing/workflows-step-ref.md).

1. Configure las variables **Propiedades del paso** según sea necesario; las propiedades disponibles dependen del tipo de paso; también puede haber varias pestañas disponibles. Por ejemplo, la opción predeterminada **Etapa de participante**, presentes en un nuevo flujo de trabajo como `Step 1`:

   ![wf-11](assets/wf-11.png)

1. Confirme las actualizaciones con la marca de verificación.
1. Confirme los cambios con **Sincronización** (barra de herramientas del editor) para generar el modelo de tiempo de ejecución.

   Consulte [Sincronizar el flujo de trabajo](#sync-your-workflow-generate-a-runtime-model) para obtener más información.

### Creación de un flujo de trabajo transitorio {#creating-a-transient-workflow}

Puede crear un [Transitorio](/help/sites-developing/workflows.md#transient-workflows) modelo de flujo de trabajo al crear un nuevo modelo o al editar uno existente:

1. Abra el modelo de flujo de trabajo para [edición](#editinganexistingworkflow).
1. Seleccionar **Propiedades del modelo de flujo de trabajo** en la barra de herramientas.
1. En el cuadro de diálogo activar **Flujo de trabajo transitorio** (o desactívela si es necesario):

   ![wf-07](assets/wf-07.png)

1. Confirme el cambio con **Guardar y cerrar**; seguido de **Sincronización** (barra de herramientas del editor) para generar el modelo de tiempo de ejecución.

   Consulte [Sincronizar el flujo de trabajo](#sync-your-workflow-generate-a-runtime-model) para obtener más información.

>[!NOTE]
>
>Cuando se ejecuta un flujo de trabajo en [efímero](/help/sites-developing/workflows.md#transient-workflows) AEM El modo no almacena ningún historial de flujo de trabajo. Por lo tanto, [Cronología](/help/sites-authoring/basic-handling.md#timeline) no muestra ninguna información relacionada con ese flujo de trabajo.

## Hacer que los modelos de flujo de trabajo estén disponibles en la IU táctil {#classic2touchui}

Si un modelo de flujo de trabajo está presente en la IU clásica, pero no aparece en el menú emergente de selección de la **[!UICONTROL Cronología]** de la IU táctil y, a continuación, siga la configuración para que esté disponible. Los siguientes pasos ilustran el uso del modelo de flujo de trabajo denominado **[!UICONTROL Solicitud de activación]**.

1. Confirme que el modelo no esté disponible en la IU táctil. Acceso a un recurso mediante `/assets.html/content/dam` ruta. Seleccione un recurso. Abrir **[!UICONTROL Cronología]** en el carril izquierdo. Clic **[!UICONTROL Iniciar flujo de trabajo]** y confirme que la variable **[!UICONTROL Solicitud de activación]** El modelo de no está presente en la lista emergente.

1. Navegar por **[!UICONTROL Herramientas > General > Etiquetado]**. Seleccionar **[!UICONTROL Flujo de trabajo]**.

1. Seleccionar **[!UICONTROL Crear > Crear etiqueta]**. Establecer **[!UICONTROL Título]** as `DAM` y **[!UICONTROL Nombre]** as `dam`. Seleccione **[!UICONTROL Enviar]**.
   ![Crear etiqueta en el modelo de flujo de trabajo](assets/workflow_create_tag.png)

1. Navegue hasta **[!UICONTROL Herramientas > Flujo de trabajo > Modelos]**. Seleccionar **[!UICONTROL Solicitud de activación]**, luego seleccione **[!UICONTROL Editar]**.

1. Seleccionar **[!UICONTROL Editar]**, abra el **[!UICONTROL Información de página]** y, desde allí, seleccione **[!UICONTROL Abrir propiedades]** y vaya a la **[!UICONTROL Básico]** pestaña (si no está abierta).

1. Añadir `Workflow : DAM` hasta **[!UICONTROL Etiquetas]** field. Confirme la selección con la marca de verificación.

1. Confirme la adición de la etiqueta con **[!UICONTROL Guardar y cerrar]**.
   ![Editar propiedades de página del modelo](assets/workflow_model_edit_activation1.png)

1. Complete el proceso con **[!UICONTROL Sincronización]**. El flujo de trabajo ahora está disponible en la interfaz de usuario táctil.

### Configuración de un flujo de trabajo para la compatibilidad con varios recursos {#configuring-a-workflow-for-multi-resource-support}

Puede configurar un modelo del flujo de trabajo para [Compatibilidad con varios recursos](/help/sites-developing/workflows.md#multi-resource-support) al crear un nuevo modelo o al editar uno existente:

1. Abra el modelo de flujo de trabajo para [edición](#editinganexistingworkflow).
1. Seleccionar **Propiedades del modelo de flujo de trabajo** en la barra de herramientas.

1. En el cuadro de diálogo activar **Compatibilidad con varios recursos** (o desactívela si es necesario):

   ![wf-08](assets/wf-08.png)

1. Confirme el cambio con **Guardar y cerrar**; seguido de **Sincronización** (barra de herramientas del editor) para generar el modelo de tiempo de ejecución.

   Consulte [Sincronizar el flujo de trabajo](#sync-your-workflow-generate-a-runtime-model) para obtener más información.

### Configuración de fases del flujo de trabajo (que muestran el progreso del flujo de trabajo) {#configuring-workflow-stages-that-show-workflow-progress}

[Fases del flujo de trabajo](/help/sites-developing/workflows.md#workflow-stages) Ayudar a visualizar el progreso de un flujo de trabajo al gestionar tareas.

>[!CAUTION]
>
>Si las fases del flujo de trabajo se definen en **Propiedades de página**, pero no se utiliza para ninguno de los pasos del flujo de trabajo, la barra de progreso no mostrará ningún progreso (independientemente del paso del flujo de trabajo actual).

Las fases que van a estar disponibles se definen en los modelos de flujo de trabajo; los modelos de flujo de trabajo existentes se pueden actualizar para incluir definiciones de fases. Puede definir cualquier número de fases para el modelo de flujo de trabajo.

Para definir **Fases** para el flujo de trabajo:

1. Abra el modelo de flujo de trabajo para editarlo.
1. Seleccionar **Propiedades del modelo de flujo de trabajo** en la barra de herramientas. A continuación, abra **Fases** pestaña.
1. Añada (y coloque) su **Fases**. Puede definir cualquier número de fases para el modelo de flujo de trabajo.

   Por ejemplo:

   ![wf-08-1](assets/wf-08-1.png)

1. Clic **Guardar y cerrar** para guardar las propiedades.
1. Asigne una fase a cada uno de los pasos del modelo de flujo de trabajo. Por ejemplo:

   ![wf-09](assets/wf-09.png)

   Se puede asignar una fase a más de un paso. Por ejemplo:

   | **Paso** | **Escenario** |
   |---|---|
   | Etapa 1 | Crear |
   | Etapa 2 | Crear |
   | Etapa 3 | Revisión |
   | Etapa 4 | Aprobar |
   | Etapa 5 | Aprobar |
   | Etapa 6 | Completar |

1. Confirme los cambios con **Sincronización** (barra de herramientas del editor) para generar el modelo de tiempo de ejecución.

   Consulte [Sincronizar el flujo de trabajo](#sync-your-workflow-generate-a-runtime-model) para obtener más información.

## Exportación de un modelo de flujo de trabajo en un paquete {#exporting-a-workflow-model-in-a-package}

Para exportar un modelo de flujo de trabajo en un paquete:

1. Cree un nuevo paquete con la variable [Administrador de paquetes](/help/sites-administering/package-manager.md#package-manager):

   1. Vaya al Administrador de paquetes mediante **Herramientas**, **Implementación**, **Paquetes**.

   1. Haga clic en **Crear paquete**.
   1. Especifique el **Nombre del paquete** y cualquier otra información según sea necesario.
   1. Haga clic en **Aceptar**.

1. Clic **Editar** en la barra de herramientas del nuevo paquete.

1. Abra el **Filtros** pestaña.

1. Seleccionar **Añadir filtro** y especifique la ruta del modelo de flujo de trabajo *diseño*:

   `/conf/global/settings/workflow/models/<*your-model-name*>`

   Haga clic en **Listo**.

1. Seleccionar **Añadir filtro** y especifique la ruta de su *runtime* modelo de flujo de trabajo:

   `/var/workflow/models/<*your-model-name*>`

   Haga clic en **Listo**.

1. Añada filtros adicionales para cualquier script personalizado que utilice el modelo.
1. Clic **Guardar** para confirmar las definiciones del filtro.
1. Seleccionar **Generar** en la barra de herramientas de la definición del paquete.
1. Seleccionar **Descargar** en la barra de herramientas del paquete.

## Usar flujos de trabajo para procesar envíos de formularios {#using-workflows-to-process-form-submissions}

Puede configurar un formulario para que el flujo de trabajo seleccionado lo procese. Cuando los usuarios envían el formulario, se crea una nueva instancia de flujo de trabajo con los datos del envío del formulario como carga útil.

Para configurar el flujo de trabajo que se utilizará con el formulario:

1. Cree una nueva página y ábrala para editarla.
1. Añadir un **Form** a la página.
1. **Configurar** el **Inicio de formulario** componente que apareció en la página.
1. Uso **Iniciar flujo de trabajo** para seleccionar el flujo de trabajo deseado de entre los disponibles:

   ![wf-12](assets/wf-12.png)

1. Confirme la nueva configuración del formulario con la marca de verificación.

## Prueba de flujos de trabajo {#testing-workflows}

Se recomienda probar un flujo de trabajo para utilizar una variedad de tipos de carga útil, incluidos tipos que son diferentes al tipo para el que se ha desarrollado. Por ejemplo, si desea que el flujo de trabajo gestione los recursos, pruébelo configurando una página como carga útil y asegúrese de que no genere errores.

Por ejemplo, pruebe el nuevo flujo de trabajo de la siguiente manera:

1. [Inicie el modelo de flujo de trabajo](/help/sites-administering/workflows-starting.md) desde la consola.
1. Defina el **Carga útil** y confirme.

1. Realice las acciones necesarias para que el flujo de trabajo continúe.
1. Supervise los archivos de registro mientras se ejecuta el flujo de trabajo.

AEM También puede configurar la visualización de la **DEPURAR** mensajes en los archivos de registro. Consulte [Registro](/help/sites-deploying/configure-logging.md) para obtener más información y una vez finalizado el desarrollo, configure el **Nivel de registro** volver a **Información**.

## Ejemplos {#examples}

### Ejemplo: Creación de un flujo de trabajo (simple) para aceptar o rechazar una solicitud de publicación {#example-creating-a-simple-workflow-to-accept-or-reject-a-request-for-publication}

Para ilustrar algunas de las posibilidades de creación de un flujo de trabajo, en el siguiente ejemplo se crea una variación del `Publish Example` flujo de trabajo.

1. [Crear un nuevo modelo de flujo de trabajo](#creating-a-new-workflow).

   El nuevo flujo de trabajo contendrá:

   * **Inicio de flujo**
   * `Step 1`
   * **Fin de flujo**

1. Eliminar `Step 1` (ya que es el tipo de paso incorrecto para este ejemplo):

   * Haga clic en el paso y seleccione **Eliminar** en la barra de herramientas de componentes. Confirme la acción.

1. Desde el **Flujo de trabajo** Selección del explorador de pasos, arrastre un **Etapa de participante** en el flujo de trabajo y colóquelo entre **Inicio de flujo** y **Fin de flujo**.
1. Para abrir el cuadro de diálogo de propiedades:

   * Haga clic en el paso del participante y seleccione **Configurar** en la barra de herramientas de componentes.
   * Haga doble clic en el paso de participante.

1. En el **Común** tab enter `Validate Content` para ambos, el **Título** y **Descripción**.
1. Abra el **Usuario/grupo** pestaña:

   * Activar **Notificar al usuario por correo electrónico**.
   * Seleccionar `Administrator` ( `admin`) para el **Usuario/grupo** field.

   >[!NOTE]
   >
   >Para enviar correos electrónicos, [es necesario configurar los detalles del servicio de correo y de la cuenta de usuario](/help/sites-administering/notification.md).

1. Confirme las actualizaciones con la marca.

   Volverá a la descripción general del modelo de flujo de trabajo, donde el paso del participante se habrá cambiado a `Validate Content`.

1. Arrastrar un **División O** en el flujo de trabajo y colóquelo entre `Validate Content` y **Fin de flujo**.
1. Abra el **División O** para la configuración.
1. Configuración de:

   * **Común**: especifique el nombre de la división.
   * **Rama 1**: seleccione **Ruta predeterminada**.

   * **Rama 2**: garantizar **Ruta predeterminada** no está seleccionado.

1. Confirme las actualizaciones de **División O**.
1. Arrastre una **Etapa de participante** en la rama izquierda, abra las propiedades, especifique los siguientes valores y confirme los cambios:

   * **Título**: `Reject Publish Request`

   * **Usuario/grupo**: por ejemplo, `projects-administrators`

   * **Notificar al usuario por correo electrónico**: active esta opción para que se notifique al usuario por correo electrónico.

1. Arrastre una **Etapa del proceso** en la rama derecha, abra las propiedades, especifique los siguientes valores y confirme los cambios:

   * **Título**: `Publish Page as Requested`

   * **Proceso**: seleccione `Activate Page`. Este proceso publica la página seleccionada en las instancias de editor.

1. Clic **Sincronización** (barra de herramientas del editor) para generar el modelo de tiempo de ejecución.

   Consulte [Sincronizar el flujo de trabajo](#sync-your-workflow-generate-a-runtime-model) para obtener más información.

   El nuevo modelo de flujo de trabajo tendrá este aspecto:

   ![wf-13](assets/wf-13.png)

1. Aplique este flujo de trabajo a su página, de modo que cuando el usuario se desplace a **Completar** el **Validar contenido** , pueden seleccionar si lo desean. **Publicar página como solicitada**, o **Rechazar solicitud de publicación**.

   ![chlimage_1-72](assets/chlimage_1-72.png)

### Ejemplo: Definición de una regla para una división O mediante un script ECMA {#defineruleecmascript}

**División O** Los pasos le permiten introducir rutas de procesamiento condicionales en el flujo de trabajo.

Para definir una regla OR, siga este procedimiento:

1. Cree dos scripts y guárdelos en el repositorio, por ejemplo, en:

   `/apps/myapp/workflow/scripts`

   >[!NOTE]
   >
   >Los scripts deben tener un [función `check()`](#function-check) que devuelve un valor booleano.

1. Edite el flujo de trabajo y añada **División O** al modelo.
1. Editar las propiedades de **Rama 1** de la **División O**:

   * Defina esto como el **Ruta predeterminada** mediante la configuración de **Valor** hasta `true`.

   * Como **Regla**, establezca la ruta en el script. Por ejemplo:
      `/apps/myapp/workflow/scripts/myscript1.ecma`
   >[!NOTE]
   >
   >Si es necesario, puede cambiar el orden de las sucursales.

1. Edite las propiedades del **Rama 2** de la **División O**.

   * Como **Regla**, establezca la ruta al otro script. Por ejemplo:
      `/apps/myapp/workflow/scripts/myscript2.ecma`

1. Establezca las propiedades de los pasos individuales en cada rama. Asegúrese de que la **Usuario/grupo** está configurado.
1. Clic **Sincronización** (barra de herramientas del editor) para mantener los cambios en el modelo de tiempo de ejecución.

   Consulte [Sincronizar el flujo de trabajo](#sync-your-workflow-generate-a-runtime-model) para obtener más información.

#### Comprobación de funciones () {#function-check}

>[!NOTE]
>
>Consulte [Uso de ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).

El siguiente script de ejemplo devuelve `true` si el nodo es un `JCR_PATH` situado debajo de `/content/we-retail/us/en`:

```
function check() {
    if (workflowData.getPayloadType() == "JCR_PATH") {
      var path = workflowData.getPayload().toString();
      var node = jcrSession.getItem(path);

      if (node.getPath().indexOf("/content/we-retail/us/en") >= 0) {
       return true;
      } else {
       return false;
      }
     } else {
      return false;
     }
}
```

### Ejemplo: Solicitud de activación personalizada {#example-customized-request-for-activation}

Puede personalizar cualquiera de los flujos de trabajo predeterminados. Para tener un comportamiento personalizado, debe superponer los detalles del flujo de trabajo adecuado.

Por ejemplo, **Solicitud de activación**. Este flujo de trabajo se utiliza para publicar páginas en **Sites** y se activa automáticamente cuando un autor de contenido no tiene los derechos de replicación adecuados. Consulte [Personalización de la creación de páginas: Personalización del flujo de trabajo de solicitud de activación](/help/sites-developing/customizing-page-authoring-touch.md#customizing-the-request-for-activation-workflow) para obtener más información.
