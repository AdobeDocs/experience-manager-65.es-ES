---
title: Flujo de trabajo centrado en Forms en OSGi
seo-title: Cree rápidamente procesos adaptables basados en formularios, automatice las operaciones de servicios de documento y utilice Adobe Sign con flujos de trabajo AEM
description: Utilice AEM Forms Workflow para automatizar y generar rápidamente revisiones y aprobaciones en los servicios de documento de inicio
seo-description: Utilice AEM Forms Workflow para automatizar y generar rápidamente revisiones y aprobaciones, para los servicios de documento de inicio (por ejemplo, para convertir un documento PDF a otro formato), integrar con el flujo de trabajo de firma de Adobe Sign, etc.
uuid: 797ba0f7-a378-45ac-9f82-fa9a952027be
topic-tags: publish, document_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 73e63493-e821-443f-b50d-10797360f5d1
docset: aem65
translation-type: tm+mt
source-git-commit: 149e505eb4dac0d9a56c53036ce1c6b8d16ad0f1
workflow-type: tm+mt
source-wordcount: '3065'
ht-degree: 1%

---


# Flujo de trabajo centrado en Forms en OSGi{#forms-centric-workflow-on-osgi}

![](do-not-localize/header.png)

Las empresas recopilan datos de cientos y miles de formularios, diversos sistemas de back-end y fuentes de datos en línea o sin conexión. También tienen un conjunto dinámico de usuarios para tomar decisiones sobre los datos, lo que implica procesos de revisión y aprobación iterativos.

Junto con los flujos de trabajo de revisión y aprobación para audiencias internas y externas, las grandes organizaciones y empresas tienen tareas repetitivas. Por ejemplo, convertir un documento PDF a otro formato. Cuando se realizan manualmente, estas tareas requieren mucho tiempo y recursos. Las empresas también tienen requisitos legales para firmar digitalmente un documento y archivar datos de formulario para su uso posterior en formatos predefinidos.

## Introducción al flujo de trabajo centrado en Forms en OSGi {#introduction-to-forms-centric-workflow-on-osgi}

Puede utilizar Flujos de trabajo de AEM para crear rápidamente flujos de trabajo basados en formularios adaptables. Estos flujos de trabajo pueden utilizarse para revisiones y aprobaciones, flujos de procesos comerciales, servicios de documento de inicio, integración con el flujo de trabajo de firma de Adobe Sign y operaciones similares. Por ejemplo, el procesamiento de la aplicación de tarjeta de crédito, el empleado deja flujos de trabajo de aprobación y guarda un formulario como documento PDF. Además, estos flujos de trabajo se pueden usar dentro de una organización o a través de un servidor de seguridad de red.

Con el flujo de trabajo centrado en Forms en OSGi, puede crear e implementar rápidamente flujos de trabajo para diversas tareas en la pila OSGi, sin tener que instalar la capacidad de administración de procesos completa en la pila JEE. El desarrollo y la administración de flujos de trabajo utilizan las funciones conocidas de Flujo de trabajo de AEM y Bandeja de entrada de AEM. Los flujos de trabajo constituyen la base para automatizar los procesos comerciales del mundo real que abarcan múltiples sistemas de software, redes, departamentos e incluso organizaciones.

Una vez configurados, estos flujos de trabajo se pueden activar manualmente para completar un proceso definido o ejecutarse programáticamente cuando los usuarios envían un formulario o [carta de administración de correspondencia](/help/forms/using/cm-overview.md). Con estas funciones AEM de flujo de trabajo mejoradas, AEM Forms oferta dos funciones distintas pero similares. Como parte de su estrategia de implementación, debe decidir cuál es la que mejor le conviene. Consulte una [comparación](capabilities-osgi-jee-workflows.md) de los Flujos de trabajo de AEM centrados en Forms en OSGi y Process Management en JEE. Además, para la topología de implementación, consulte [Topologías de arquitectura e implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

El flujo de trabajo centrado en Forms en OSGi amplía [AEM Bandeja de entrada](/help/sites-authoring/inbox.md) y proporciona componentes adicionales (pasos) para AEM editor de flujo de trabajo a fin de agregar compatibilidad con flujos de trabajo centrados en AEM Forms. La bandeja de entrada de AEM ampliada tiene funciones similares a [AEM Forms Workspace](introduction-html-workspace.md). Junto con la administración de flujos de trabajo centrados en el ser humano (aprobación, revisión, etc.), puede utilizar flujos de trabajo de AEM para automatizar las operaciones relacionadas con [servicios de documento](/help/sites-developing/workflows-step-ref.md) (por ejemplo, Generar PDF) y los documentos de firma electrónica (Adobe Sign).

Todos los pasos del flujo de trabajo de AEM Forms admiten el uso de variables. Las variables permiten que los pasos del flujo de trabajo retengan y pasen metadatos en varios pasos durante la ejecución. Puede crear diferentes tipos de variables para almacenar diferentes tipos de datos. También puede crear colecciones de variables (matriz) para almacenar varias instancias de datos relacionados con el mismo tipo. Normalmente, se utiliza una variable o una colección de variables cuando se necesita tomar una decisión en función del valor que contiene o para almacenar la información que se necesita más adelante en un proceso. Para obtener más información sobre el uso de variables en estos componentes de flujo de trabajo centrados en Forms (pasos), consulte [Flujo de trabajo centrado en Forms en OSGi - Referencia de pasos](../../forms/using/aem-forms-workflow-step-reference.md). Para obtener información sobre cómo crear y administrar variables, consulte [Variables en flujos de trabajo de AEM](../../forms/using/variable-in-aem-workflows.md).

En el diagrama siguiente se muestra un procedimiento completo para crear, ejecutar y supervisar un flujo de trabajo centrado en Forms en OSGi.

![introducción a aem-forms-workflow](assets/introduction-to-aem-forms-workflow.jpg)

## Antes de comenzar {#before-you-start}

* Un flujo de trabajo es una representación de un proceso empresarial real. Mantenga preparado su proceso comercial real y la lista de los participantes en el proceso de negocios. Además, mantenga la garantía (formularios adaptables, Documentos PDF, etc.) lista antes de crear un flujo de trabajo con inicio.
* Un flujo de trabajo puede tener varias etapas. Estas etapas se muestran en la Bandeja de entrada AEM y ayudan a informar sobre el progreso del flujo de trabajo. Divida el proceso comercial en etapas lógicas.
* Puede configurar el paso de asignación de tareas de AEM Flujos de trabajo para enviar notificaciones por correo electrónico a los usuarios o a los usuarios asignados. Por lo tanto, [habilite las notificaciones por correo electrónico](#configure-email-service).
* Un flujo de trabajo también puede utilizar la firma de Adobe para las firmas digitales. Si planea utilizar Adobe Sign en un flujo de trabajo, [configure Adobe Sign para AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) antes de utilizarlo en un flujo de trabajo.

## Crear un modelo de flujo de trabajo {#create-a-workflow-model}

Un modelo de flujo de trabajo consiste en la lógica y el flujo de un proceso comercial. Se compone de una serie de pasos. Estos pasos son componentes AEM. Puede ampliar los pasos del flujo de trabajo con parámetros y secuencias de comandos para proporcionar más funcionalidad y control, según sea necesario. AEM Forms proporciona algunos pasos además de AEM pasos disponibles de forma predeterminada. Para obtener una lista detallada de los pasos de AEM y AEM Forms, consulte [AEM Referencia de pasos del flujo de trabajo](/help/sites-developing/workflows-step-ref.md) y [Flujo de trabajo centrado en Forms en OSGi - Referencia de pasos](../../forms/using/aem-forms-workflow.md).

AEM proporciona una interfaz de usuario intuitiva para crear un modelo de flujo de trabajo mediante los pasos de flujo de trabajo proporcionados. Para obtener instrucciones paso a paso para crear un modelo de flujo de trabajo, consulte [Creación de modelos de flujo de trabajo](/help/sites-developing/workflows-models.md). El ejemplo siguiente proporciona instrucciones paso a paso para crear un modelo de flujo de trabajo para un flujo de trabajo de aprobación y revisión:

>[!NOTE]
>
>Debe ser miembro del grupo de editor de flujo de trabajo para crear o editar un modelo de flujo de trabajo.

### Crear un modelo para un flujo de trabajo de aprobación y revisión {#create-a-model-for-an-approval-and-review-workflow}

El flujo de trabajo de aprobación y revisión corresponde a las tareas que requieren la intervención humana para tomar decisiones. En el siguiente ejemplo se crea un modelo de flujo de trabajo para una solicitud de préstamo hipotecario que debe rellenar un agente bancario de la oficina central. Una vez completada la solicitud, se envía para su aprobación. Posteriormente, la solicitud aprobada se envía al solicitante para que presente firmas electrónicas utilizando Adobe Sign.

El ejemplo está disponible como paquete adjunto a continuación. Importe e instale el ejemplo con el administrador de paquetes. También puede realizar los siguientes pasos para crear manualmente el modelo de flujo de trabajo para la aplicación:

En el ejemplo se crea un modelo de flujo de trabajo con una aplicación de hipoteca que debe rellenar un agente bancario de recepción. Una vez completada, la solicitud se envía para su aprobación. Más adelante, la solicitud aprobada se envía al cliente para que la firme electrónicamente con Adobe Sign. Puede importar e instalar el ejemplo con el administrador de paquetes.

[Obtener archivo](assets/example-mortgage-loan-application.zip)

1. Abra la consola Modelos de flujo de trabajo. La dirección URL predeterminada es `https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. Seleccione **Crear** y luego **Crear modelo**. Aparecerá el cuadro de diálogo Añadir modelo de flujo de trabajo.
1. Introduzca **Title** y **Name** (opcional). Por ejemplo, una solicitud de hipoteca. Puntee **Listo**.
1. Seleccione el modelo de flujo de trabajo recién creado y toque **Editar**. Ahora puede agregar pasos de flujo de trabajo para generar lógica empresarial. Cuando se crea un modelo de flujo de trabajo por primera vez, contiene:

   * Los pasos: Inicio de flujo y Fin de flujo. Estos pasos representan el comienzo y el final del flujo de trabajo. Estos pasos son obligatorios y no se pueden editar ni eliminar.
   * Ejemplo de paso de participante denominado Paso 1. Este paso está configurado para asignar un elemento de trabajo al usuario administrador. Elimine este paso.

1. Habilite las notificaciones por correo electrónico. Puede configurar el flujo de trabajo centrado en Forms en OSGi para enviar notificaciones por correo electrónico a los usuarios o a los usuarios asignados. Realice las siguientes configuraciones para habilitar las notificaciones por correo electrónico:

   1. Vaya a AEM administrador de configuración en `https://[server]:[port]/system/console/configMgr`.
   1. Abra la configuración **[!UICONTROL Day CQ Mail Service]**. Especifique un valor para los campos **[!UICONTROL nombre del host del servidor SMTP]**, **[!UICONTROL puerto del servidor SMTP,]** y **[!UICONTROL dirección &quot;De&quot;]**. Haga clic en **[!UICONTROL Guardar]**.
   1. Abra la configuración de **[!UICONTROL Day CQ Link Externalizer]**. En el campo **[!UICONTROL Dominios]**, especifique el nombre de host/dirección IP real y el número de puerto para las instancias locales, de autor y de publicación. Haga clic en **[!UICONTROL Guardar]**.

1. Cree etapas de flujo de trabajo. Un flujo de trabajo puede tener varias etapas. Estas etapas se muestran en la Bandeja de entrada de AEM y en el progreso del flujo de trabajo de los informes.

   Para definir un escenario, toque el icono ![info-círculo](assets/info-circle.png) para abrir las propiedades del modelo de workflow, abra la ficha **Etapas**, agregue etapas para el modelo de workflow y toque **Guardar y cerrar**. Para la aplicación hipoteca de ejemplo, cree las etapas: solicitud de préstamo, estado de solicitud de préstamo, documentos firmados y documento de préstamo firmado.

1. Arrastre y suelte el navegador de pasos **Asignar Tarea** al modelo de flujo de trabajo. Hacerlo el primer paso del modelo.

   El componente de asignación de tarea asigna la tarea, creada por el flujo de trabajo, a un usuario o grupo. Junto con la asignación de la tarea, puede utilizar el componente para especificar un formulario adaptable o un PDF no interactivo para la tarea. El formulario adaptable es necesario para aceptar datos introducidos por los usuarios y se utiliza un PDF no interactivo o un formulario adaptable de sólo lectura para flujos de trabajo solo de revisión.

   También puede utilizar el paso para controlar el comportamiento de la tarea. Por ejemplo, al crear un documento de registro automático, asigne la tarea a un usuario o grupo específico, la ruta de los datos enviados, la ruta de los datos que se van a rellenar previamente y las acciones predeterminadas. Para obtener información detallada sobre las opciones del paso de asignación de tarea, consulte [Flujo de trabajo centrado en Forms en OSGi - Referencia de pasos](../../forms/using/aem-forms-workflow.md) documento.

   ![workflow-editor](assets/workflow-editor.png)

   Para el ejemplo de la aplicación hipoteca, configure el paso de asignación de tarea para utilizar un formulario adaptable de sólo lectura y mostrar el Documento PDF una vez que se complete la tarea. Además, seleccione un grupo de usuarios autorizado para aprobar la solicitud de préstamo. En la ficha **Acciones**, deshabilite la opción **Enviar**. Cree una variable **actionTaken** del tipo de datos String y especifique la variable como la **Variable Route**. Por ejemplo, actionTaken. Además, agregue las rutas Aprobar y Rechazar. Las rutas se muestran como acciones independientes (botones) en AEM Bandeja de entrada. El flujo de trabajo selecciona una rama en función de la acción (botón) que toca un usuario.

   Puede importar el paquete de ejemplo, disponible para descargar al principio de la sección, para el conjunto completo de valores de todos los campos del paso de asignación de tarea configurado, por ejemplo, la aplicación de hipoteca.

1. Arrastre y suelte el componente O dividido desde el navegador de pasos hasta el modelo de flujo de trabajo. La división O crea una división en el flujo de trabajo, tras la cual solo una rama está activa. Este paso le permite introducir rutas de procesamiento condicionales en el flujo de trabajo. Puede agregar pasos de flujo de trabajo a cada rama según sea necesario.

   Puede definir la expresión de enrutamiento para una rama mediante una definición de regla, una secuencia de comandos ECMA o una secuencia de comandos externa.

   Utilice el editor de expresiones para crear expresiones de enrutamiento para las ramas 1 y 2. Estas expresiones de enrutamiento ayudan a elegir una rama en función de la acción del usuario en AEM Bandeja de entrada.

   **Expresión de enrutamiento para la ramificación 1**

   Cuando un usuario toca **Aprobar** en AEM Bandeja de entrada, se activa la Ramificación 1.

   ![Ejemplo de división OR](assets/orsplit_branch1_active_new.png)

   **Expresión de enrutamiento para la ramificación 2**

   Cuando un usuario toca **Rechazar** en AEM Bandeja de entrada, se activa la Ramificación 2.

   ![Ejemplo de división OR](assets/orsplit_branch2_active_new.png)

   Para obtener información sobre la creación de expresiones de enrutamiento mediante variables, consulte [Variables en flujos de trabajo de AEM Forms](../../forms/using/variable-in-aem-workflows.md).

1. Añada otros pasos del flujo de trabajo para crear la lógica empresarial.

   Para el ejemplo de hipoteca, agregue un documento de registro de generación, dos pasos de asignación de tarea y un paso de documento de firma a la Rama 1 del modelo, como se muestra en la imagen siguiente. Un paso de tarea de asignación es mostrar y enviar **documentos de préstamo firmados al solicitante** y otro componente de tarea de asignación es **para mostrar documentos firmados**. Además, agregue un componente de asignación de tarea a la rama 2. Se activa cuando un usuario toca Rechazar en AEM Bandeja de entrada.

   Para el conjunto completo de valores de todos los campos de los pasos de tarea de asignación, el documento del paso de registro y el paso de documento de firma configurados, por ejemplo, la aplicación de hipoteca, importe el paquete de ejemplo, disponible para su descarga al comienzo de esta sección.

   El modelo de flujo de trabajo está listo. Puede iniciar el flujo de trabajo mediante varios métodos. Para obtener más información, consulte [Iniciar un flujo de trabajo centrado en Forms en OSGi](#launch).

   ![workflow-editor-hipoteca](assets/workflow-editor-mortgage.png)

## Crear una aplicación de flujo de trabajo centrada en Forms {#create-a-forms-centric-workflow-application}

La aplicación es el formulario adaptable asociado al flujo de trabajo. Cuando una aplicación se envía a través de la Bandeja de entrada, inicia el flujo de trabajo asociado. Para que un flujo de trabajo de Forms esté disponible como aplicación en AEM Bandeja de entrada y en la aplicación de AEM Forms, haga lo siguiente para crear una aplicación de flujo de trabajo:

>[!NOTE]
>
>Debe ser miembro del grupo fd-admin para poder crear y administrar aplicaciones de flujo de trabajo.

1. En la instancia de autor de AEM, vaya a ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Administrar aplicación de flujo de trabajo]** y toque **[!UICONTROL Crear]**.
1. En la ventana Crear aplicación de flujo de trabajo, proporcione entradas para los campos siguientes y toque **Crear**. Se crea una nueva aplicación y se muestra en la pantalla Aplicaciones de flujo de trabajo.

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Descripción</td>
  </tr>
  <tr>
   <td>Título</td>
   <td>El título está visible en AEM Bandeja de entrada y ayuda a los usuarios a elegir una aplicación. Manténgalo descriptivo. Por ejemplo: Guarda la aplicación de apertura de cuenta.<br /> </td>
  </tr>
  <tr>
   <td>Nombre </td>
   <td>Especifique el nombre de la aplicación. Todos los caracteres que no sean alfabetos, números, guiones y subrayados se sustituyen por guiones. </td>
  </tr>
  <tr>
   <td>Descripción</td>
   <td>La descripción está visible en AEM Bandeja de entrada. Proporcione información detallada sobre la aplicación en los campos de descripción. Por ejemplo, Propósito de la aplicación.<br /> </td>
  </tr>
  <tr>
   <td>Formulario adaptable</td>
   <td><p>Especifique la ruta de un formulario adaptable. Cuando un usuario inicio una aplicación, se muestra el formulario adaptable especificado.</p> <p><strong>Nota</strong>: Las aplicaciones de flujo de trabajo no admiten formularios ni documentos PDF que tengan más de una página o que requieran desplazamiento en el iPad de Apple. Cuando se abre una aplicación en Apple iPad y el formulario adaptable o el documento PDF es más largo que una página, se pierden los campos de formulario y el contenido de la segunda página.</p> </td>
  </tr>
  <tr>
   <td>Grupo de acceso</td>
   <td><p>Seleccione un grupo. La aplicación solo está visible en AEM Bandeja de entrada para los miembros del grupo seleccionado. La opción de grupo de acceso permite seleccionar todos los grupos del grupo de usuarios del flujo de trabajo. </p> <br /> </td>
  </tr>
  <tr>
   <td>Servicio de prerrellenar</td>
   <td>Seleccione un <a href="../../forms/using/prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">servicio de relleno previo</a> para el formulario adaptable.<br /> </td>
  </tr>
  <tr>
   <td>Modelo de flujo de trabajo</td>
   <td>Seleccione un <a href="../../forms/using/aem-forms-workflow.md#create-a-workflow-model">modelo de flujo de trabajo</a> para la aplicación. Un modelo de flujo de trabajo consiste en la lógica y el flujo del proceso comercial. </td>
  </tr>
  <tr>
   <td>Ruta del archivo de datos</td>
   <td>Especifique la ruta del archivo de datos en el repositorio de crx. La ruta es relativa a la carga útil del formulario adaptable y contiene el nombre del archivo de datos. Incluya siempre el nombre completo del archivo, incluida la extensión, si corresponde. Por ejemplo, [carga útil]/data.xml. </td>
  </tr>
  <tr>
   <td>Ruta de archivos adjuntos</td>
   <td>Especifique la ruta de la carpeta de archivos adjuntos en el repositorio crx. La ruta de acceso de datos adjuntos es relativa a la ubicación de la carga útil. Por ejemplo, [carga útil]/data.xml. </td>
  </tr>
  <tr>
   <td>Documento de ruta de registro</td>
   <td>Especifique la ruta de Documento del archivo Record en crx-repository. La ruta es relativa a la ubicación de carga útil del formulario adaptable. Incluya siempre el nombre completo del archivo, incluida la extensión, si corresponde. Por ejemplo, [carga útil]/DOR/creditcard.pdf.</td>
  </tr>
 </tbody>
</table>

## Iniciar un flujo de trabajo centrado en Forms en OSGi {#launch}

Puede iniciar o déclencheur un flujo de trabajo centrado en Forms mediante:

* [Envío de una aplicación desde AEM Bandeja de entrada](#inbox)
* [Envío de una aplicación desde la aplicación AEM Forms](#afa)

* [Envío de un formulario adaptable](#af)
* [Uso de la carpeta vigilada](#watched)

* [Envío de una comunicación interactiva o una carta](#letter)

### Envío de una aplicación desde AEM Bandeja de entrada {#inbox}

La aplicación de flujo de trabajo que ha creado está disponible como una aplicación en la Bandeja de entrada. Los usuarios que son miembros del grupo de usuarios del flujo de trabajo pueden rellenar y enviar la aplicación que déclencheur el flujo de trabajo asociado. Para obtener información sobre el uso de AEM Bandeja de entrada para enviar aplicaciones y administrar tareas, consulte [Administrar aplicaciones y tareas de Forms en AEM Bandeja de entrada](../../forms/using/manage-applications-inbox.md).

### Envío de una aplicación desde la aplicación de AEM Forms {#afa}

La aplicación de AEM Forms se sincroniza con un servidor de AEM Forms y le permite realizar cambios en los datos del formulario, las tareas, las aplicaciones de flujo de trabajo y la información guardada (borradores/plantillas) en su cuenta. Para obtener más información, consulte [Aplicación de AEM Forms](/help/forms/using/aem-forms-app.md) y artículos relacionados.

### Envío de un formulario adaptable {#af}

Puede configurar las acciones de envío de un formulario adaptable para que el inicio de un flujo de trabajo se realice al enviar el formulario adaptable. Los formularios adaptables proporcionan la **acción de envío Invocar un flujo de trabajo de AEM** para inicio de un flujo de trabajo al enviar un formulario adaptable. Para obtener información detallada sobre la acción de envío, consulte [Configuración de la acción de envío](../../forms/using/configuring-submit-actions.md). Para enviar un formulario adaptable a través de la aplicación de AEM Forms, habilite Sincronizar con la aplicación de AEM Forms en las propiedades del formulario adaptable.

Puede configurar un formulario adaptable para sincronizar, enviar y déclencheur un flujo de trabajo desde la aplicación de AEM Forms. Para obtener más información, consulte [trabajo con un formulario](/help/forms/using/working-with-form.md).

### Uso de una carpeta controlada {#watched}

Un administrador (un miembro del grupo de administradores de fd) puede configurar una carpeta de red para ejecutar un flujo de trabajo preconfigurado cuando un usuario coloca un archivo (como un archivo PDF) en la carpeta. Una vez completado el flujo de trabajo, puede guardar el archivo de resultados en una carpeta de salida especificada. Dicha carpeta se conoce como [Carpeta vigilada](../../forms/using/watched-folder-in-aem-forms.md). Realice el siguiente procedimiento para configurar una carpeta vigilada para iniciar un flujo de trabajo:

1. En la instancia de autor de AEM, vaya a ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Configurar carpeta vigilada]**. Se muestra una lista de las carpetas ya configuradas controladas.
1. Toque **[!UICONTROL Nuevo]**. Se muestra una lista de campos. Especifique un valor para los siguientes campos para configurar una carpeta vigilada para un flujo de trabajo:

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Descripción</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Nombre</code></td>
   <td>Especifique el nombre de la carpeta vigilada. Este campo solo admite alfanuméricos.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Ruta</code></td>
   <td>Especifique la ubicación física de la carpeta vigilada. En un entorno agrupado, utilice una carpeta de red compartida a la que se pueda acceder desde AEM nodo de clúster.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Procesar archivos mediante</code></td>
   <td>Seleccione la opción <span class="uicontrol">Flujo de trabajo </code>. </code></td>
  </tr>
  <tr>
   <td><span class="uicontrol">Modelo de flujo de trabajo</code></td>
   <td>Seleccione un modelo de flujo de trabajo.<br /> </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Patrón de archivo de salida</code></td>
   <td>Especifique la estructura de directorios para los archivos de salida y los directorios. También puede especificar un patrón <a href="/help/forms/using/admin-help/configuring-watched-folder-endpoints.md" target="_blank">para archivos de salida y directorios</a>.</td>
  </tr>
 </tbody>
</table>

1. Toque **Avanzado**. Especifique un valor para el campo siguiente y toque **Crear**. La carpeta vigilada está configurada para iniciar un flujo de trabajo. Ahora, cada vez que se coloca un archivo en el directorio de entrada de la carpeta vigilada, se activa el flujo de trabajo especificado.

   | Campo | Descripción |
   |---|---|
   | Filtro de asignador de cargas útiles | Cuando se crea una carpeta vigilada, se crea una estructura de carpetas en el repositorio crx. La estructura de carpetas puede servir como carga útil para el flujo de trabajo. Puede escribir una secuencia de comandos para asignar un flujo de trabajo de AEM para aceptar entradas de la estructura de carpetas vigiladas. Hay una implementación lista para usar disponible que se muestra en el filtro del asignador de carga útil. Si no tiene una implementación personalizada, seleccione la implementación predeterminada. |

   La ficha Avanzado contiene más campos. La mayoría de estos campos contienen un valor predeterminado. Para obtener más información sobre todos los campos, consulte el artículo [Crear o configurar una carpeta controlada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md).

### Envío de una comunicación interactiva o una carta {#letter}

Puede asociar y ejecutar un flujo de trabajo centrado en Forms en OSGi al enviar una comunicación interactiva o una carta. En la gestión de la correspondencia se utilizan flujos de trabajo para las comunicaciones y cartas interactivas posteriores al procesamiento. Por ejemplo, enviar por correo electrónico, imprimir, enviar por fax o archivar letras finales. Para obtener más información, consulte [Post-procesamiento de comunicaciones interactivas y letras](../../forms/using/submit-letter-topostprocess.md).

## Configuraciones adicionales {#additional-configurations}

### Configurar el servicio de correo electrónico {#configure-email-service}

Puede utilizar los pasos Asignar Tarea y Enviar correo electrónico de AEM Flujos de trabajo para enviar un correo electrónico. Realice los siguientes pasos para especificar los servidores de correo electrónico y otras configuraciones necesarias para enviar correo electrónico:

1. Vaya a AEM administrador de configuración en `https://[server]:[port]/system/console/configMgr`.
1. Abra la configuración **[!UICONTROL Day CQ Mail Service]**. Especifique un valor para los campos **[!UICONTROL nombre del host del servidor SMTP]**, **[!UICONTROL puerto del servidor SMTP,]** y **[!UICONTROL dirección &quot;De&quot;]**. Haga clic en **[!UICONTROL Guardar]**.
1. Abra la configuración de **[!UICONTROL Day CQ Link Externalizer]**. En el campo **[!UICONTROL Dominios]**, especifique el nombre de host/dirección IP real y el número de puerto para las instancias locales, de autor y de publicación. Haga clic en **[!UICONTROL Guardar]**.

### Purgar instancias de flujo de trabajo {#purge-workflow-instances}

Al minimizar el número de instancias de flujo de trabajo, aumenta el rendimiento del motor de flujos de trabajo, de modo que puede depurar regularmente instancias de flujo de trabajo completadas o en ejecución desde el repositorio. Para obtener información detallada, consulte [Depuración regular de instancias de flujo de trabajo](/help/sites-administering/workflows-administering.md#regular) puración de instancias de flujo de trabajo
