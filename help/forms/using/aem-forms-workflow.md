---
title: Flujo de trabajo centrado en formularios en OSGi
seo-title: Cree rápidamente procesos basados en formularios adaptables, automatice las operaciones de servicios de documentos y utilice Adobe Sign con flujos de trabajo de AEM
description: Utilice el flujo de trabajo de AEM Forms para automatizar y generar rápidamente revisiones y aprobaciones para iniciar document services
seo-description: Utilice AEM Forms Workflow para automatizar y generar rápidamente revisiones y aprobaciones, para iniciar document services (por ejemplo, para convertir un documento PDF a otro formato), integrar con el flujo de trabajo de firma de Adobe Sign, etc.
uuid: 797ba0f7-a378-45ac-9f82-fa9a952027be
topic-tags: document_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 73e63493-e821-443f-b50d-10797360f5d1
docset: aem65
translation-type: tm+mt
source-git-commit: 3eaace94bc0499aaebfcd389d4dc97b97c7d9160

---


# Flujo de trabajo centrado en formularios en OSGi{#forms-centric-workflow-on-osgi}

![](do-not-localize/header.png)

Las empresas recopilan datos de cientos y miles de formularios, diversos sistemas de back-end y fuentes de datos en línea o sin conexión. También tienen un conjunto dinámico de usuarios para tomar decisiones sobre los datos, lo que implica procesos de revisión y aprobación iterativos.

Junto con los flujos de trabajo de revisión y aprobación para audiencias internas y externas, las grandes organizaciones y empresas tienen tareas repetitivas. Por ejemplo, convertir un documento PDF a otro formato. Cuando se realizan manualmente, estas tareas requieren mucho tiempo y recursos. Las empresas también tienen requisitos legales para firmar digitalmente un documento y archivar datos de formulario para su uso posterior en formatos predefinidos.

## Introducción al flujo de trabajo centrado en formularios en OSGi {#introduction-to-forms-centric-workflow-on-osgi}

Puede utilizar flujos de trabajo de AEM para crear rápidamente flujos de trabajo adaptables basados en formularios. Estos flujos de trabajo pueden utilizarse para revisiones y aprobaciones, flujos de procesos comerciales, para iniciar servicios de documentos, integrarse con el flujo de trabajo de firma de Adobe Sign y operaciones similares. Por ejemplo, el procesamiento de la aplicación de tarjeta de crédito, los empleados dejan los flujos de trabajo de aprobación y guardan un formulario como documento PDF. Además, estos flujos de trabajo se pueden utilizar dentro de una organización o a través de un servidor de seguridad de red.

Con el flujo de trabajo centrado en Forms en OSGi, puede generar e implementar rápidamente flujos de trabajo para diversas tareas en la pila OSGi, sin tener que instalar la capacidad de administración de procesos completa en la pila JEE. El desarrollo y la gestión de flujos de trabajo utilizan las funciones conocidas de Flujo de trabajo de AEM y Bandeja de entrada de AEM. Los flujos de trabajo forman la base para automatizar los procesos comerciales del mundo real que abarcan múltiples sistemas de software, redes, departamentos e incluso organizaciones.

Una vez configurados, estos flujos de trabajo se pueden activar manualmente para completar un proceso definido o ejecutarse mediante programación cuando los usuarios envían un formulario o una carta de administración [de](/help/forms/using/cm-overview.md) correspondencia. Gracias a estas funciones mejoradas de flujo de trabajo de AEM, AEM Forms ofrece dos funciones distintas pero similares. Como parte de su estrategia de implementación, debe decidir cuál es la que mejor le conviene. Consulte una [comparación](../../forms/using/capabilities-osgi-jee-workflows.md) de los flujos de trabajo de AEM centrados en formularios en OSGi y Process Management en JEE. Además, para la topología de implementación, consulte [Arquitectura y topologías de implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

El flujo de trabajo centrado en formularios en OSGi amplía la bandeja de entrada [de](/help/sites-authoring/inbox.md) AEM y proporciona componentes adicionales (pasos) para que el editor de flujo de trabajo de AEM añada compatibilidad con flujos de trabajo centrados en AEM Forms. La bandeja de entrada de AEM ampliada tiene funciones similares a [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md). Junto con la administración de flujos de trabajo centrados en el ser humano (aprobación, revisión, etc.), puede utilizar los flujos de trabajo de AEM para automatizar las operaciones relacionadas con servicios de [documentos](/help/sites-developing/workflows-step-ref.md)(por ejemplo, Generar PDF) y la firma electrónica de documentos (Adobe Sign).

Todos los pasos del flujo de trabajo de AEM Forms admiten el uso de variables. Las variables permiten que los pasos del flujo de trabajo retengan y pasen metadatos en varios pasos durante la ejecución. Puede crear diferentes tipos de variables para almacenar diferentes tipos de datos. También puede crear colecciones de variables (matriz) para almacenar varias instancias de datos relacionados con el mismo tipo. Normalmente, se utiliza una variable o una colección de variables cuando se necesita tomar una decisión en función del valor que contiene o para almacenar la información que se necesita más adelante en un proceso. Para obtener más información sobre el uso de variables en estos componentes de flujo de trabajo centrados en formularios (pasos), consulte Flujo de trabajo centrado en [formularios en OSGi - Referencia](../../forms/using/aem-forms-workflow-step-reference.md)de pasos. Para obtener información sobre la creación y administración de variables, consulte [Variables en flujos de trabajo](../../forms/using/variable-in-aem-workflows.md)de AEM.

En el diagrama siguiente se muestra un procedimiento completo para crear, ejecutar y supervisar un flujo de trabajo centrado en formularios en OSGi.

![introducción a aem-forms-workflow](assets/introduction-to-aem-forms-workflow.jpg)

## Antes de comenzar {#before-you-start}

* Un flujo de trabajo es una representación de un proceso empresarial real. Mantenga preparado su proceso comercial real y la lista de participantes del proceso empresarial. Además, mantenga la garantía (formularios adaptables, documentos PDF, etc.) lista antes de empezar a crear un flujo de trabajo.
*  Un flujo de trabajo puede tener varias etapas. Estas etapas se muestran en la Bandeja de entrada de AEM y ayudan a informar sobre el progreso del flujo de trabajo. Divida el proceso comercial en etapas lógicas.
* Puede configurar el paso de tareas de asignación de flujos de trabajo de AEM para enviar notificaciones por correo electrónico a los usuarios o a los usuarios asignados. Por lo tanto, [habilite las notificaciones](#configure-email-service)por correo electrónico.
* Un flujo de trabajo también puede utilizar la firma de Adobe para firmas digitales. Si planea utilizar Adobe Sign en un flujo de trabajo, [configure Adobe Sign para AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) antes de utilizarlo en un flujo de trabajo.

## Create a workflow model {#create-a-workflow-model}

Un modelo de flujo de trabajo consiste en la lógica y el flujo de un proceso comercial. Se compone de una serie de pasos. Estos pasos son componentes de AEM. Puede ampliar los pasos del flujo de trabajo con parámetros y secuencias de comandos para proporcionar más funcionalidad y control, según sea necesario. AEM Forms proporciona algunos pasos además de los pasos de AEM disponibles de forma predeterminada. Para obtener una lista detallada de los pasos de AEM y AEM Forms, consulte Referencia [de los pasos de flujo de trabajo de](/help/sites-developing/workflows-step-ref.md) AEM y Flujo de trabajo centrado en [formularios en OSGi: Referencia](../../forms/using/aem-forms-workflow.md)de pasos.

AEM proporciona una interfaz de usuario intuitiva para crear un modelo de flujo de trabajo mediante los pasos de flujo de trabajo proporcionados. Para obtener instrucciones paso a paso para crear un modelo de flujo de trabajo, consulte [Creación de modelos](/help/sites-developing/workflows-models.md)de flujo de trabajo. El ejemplo siguiente proporciona instrucciones paso a paso para crear un modelo de flujo de trabajo para un flujo de trabajo de aprobación y revisión:

>[!NOTE]
>
>Debe ser miembro del grupo de editor de flujo de trabajo para crear o editar un modelo de flujo de trabajo.

### Creación de un modelo para un flujo de trabajo de aprobación y revisión {#create-a-model-for-an-approval-and-review-workflow}

El flujo de trabajo de aprobación y revisión corresponde a las tareas que requieren la intervención humana para tomar decisiones. En el siguiente ejemplo se crea un modelo de flujo de trabajo para una solicitud de préstamo hipotecario que debe rellenar un agente bancario de la oficina central. Una vez completada la solicitud, se envía para su aprobación. Más adelante, la solicitud aprobada se envía al solicitante para que presente firmas electrónicas mediante Adobe Sign.

El ejemplo está disponible como paquete adjunto a continuación. Importe e instale el ejemplo con el administrador de paquetes. También puede realizar los siguientes pasos para crear manualmente el modelo de flujo de trabajo para la aplicación:

En el ejemplo se crea un modelo de flujo de trabajo con una aplicación de hipoteca que debe rellenar un agente bancario de recepción. Una vez completada, la solicitud se envía para su aprobación. Posteriormente, la aplicación aprobada se envía al cliente para que la firme electrónicamente con Adobe Sign. Puede importar e instalar el ejemplo con el administrador de paquetes.

[Obtener archivo](assets/example-mortgage-loan-application.zip)

1. Abra la consola Modelos de flujo de trabajo. La dirección URL predeterminada es https://[Server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models
1. Select **Create**, then **Create Model**. Aparecerá el cuadro de diálogo Agregar modelo de flujo de trabajo.
1. Introduzca el **Título** y el **Nombre** (opcional). Por ejemplo, una solicitud de hipoteca. Puntee **Listo**.
1. Seleccione el modelo de flujo de trabajo recién creado y toque **Editar**. Ahora puede agregar pasos de flujo de trabajo para generar lógica empresarial. Cuando se crea un modelo de flujo de trabajo por primera vez, contiene:

   * Los pasos: Inicio de flujo y Fin de flujo. Estos pasos representan el comienzo y el final del flujo de trabajo. Estos pasos son obligatorios y no se pueden editar ni eliminar.
   * Ejemplo de paso de participante denominado Paso 1. Este paso está configurado para asignar un elemento de trabajo al usuario administrador. Elimine este paso.

1. Habilite las notificaciones por correo electrónico. Puede configurar el flujo de trabajo centrado en formularios en OSGi para enviar notificaciones por correo electrónico a los usuarios o a los usuarios asignados. Realice las siguientes configuraciones para habilitar las notificaciones por correo electrónico:

   1. Vaya al administrador de configuración de AEM en https://[server]:[port]/system/console/configMgr.
   1. Abra la configuración **[!UICONTROL Día del servicio]** de correo de CQ. Especifique un valor para los campos de nombre **[!UICONTROL de host del servidor]** SMTP, **[!UICONTROL puerto del servidor]** SMTP y dirección **** &quot;De&quot;. Haga clic en **[!UICONTROL Guardar]**.
   1. Abra la configuración **[!UICONTROL Day CQ Link Externalizer]** . En el campo **[!UICONTROL Dominios]** , especifique el nombre de host/dirección IP real y el número de puerto para las instancias locales, de autor y de publicación. Haga clic en **[!UICONTROL Guardar]**.

1. Cree etapas de flujo de trabajo.  Un flujo de trabajo puede tener varias etapas. Estas etapas se muestran en la Bandeja de entrada de AEM y en el flujo de trabajo se informa del progreso del mismo.

   Para definir un escenario, toque el icono del ![círculo](assets/info-circle.png) de información para abrir las propiedades del modelo de flujo de trabajo, abra la ficha **Etapas** , agregue etapas para el modelo de flujo de trabajo y toque **Guardar y cerrar**. Para la aplicación hipoteca de ejemplo, cree las etapas: solicitud de préstamo, estado de solicitud de préstamo, documentos firmados y documento de préstamo firmado.

1. Arrastre y suelte el navegador de pasos **Asignar tarea** al modelo de flujo de trabajo. Hacerlo el primer paso del modelo.

   El componente de asignación de tareas asigna la tarea, creada por el flujo de trabajo, a un usuario o grupo. Junto con la asignación de la tarea, puede utilizar el componente para especificar un formulario adaptable o un PDF no interactivo para la tarea. El formulario adaptable es necesario para aceptar datos introducidos por los usuarios y se utiliza un PDF no interactivo o un formulario adaptable de sólo lectura para los flujos de trabajo de solo revisión.

   También puede utilizar el paso para controlar el comportamiento de la tarea. Por ejemplo, al crear un documento de registro automático, asigne la tarea a un usuario o grupo específico, la ruta de los datos enviados, la ruta de los datos que se van a rellenar previamente y las acciones predeterminadas. Para obtener información detallada sobre las opciones del paso de tareas de asignación, consulte Flujo de trabajo centrado en [formularios en el documento OSGi - Referencia](../../forms/using/aem-forms-workflow.md) de pasos.

   ![workflow-editor](assets/workflow-editor.png)

   Para el ejemplo de la aplicación hipoteca, configure el paso de tarea de asignación para utilizar un formulario adaptable de sólo lectura y mostrar el documento PDF una vez finalizada la tarea. Además, seleccione un grupo de usuarios autorizado para aprobar la solicitud de préstamo. En la ficha **Acciones** , desactive la opción **Enviar** . Cree una **variable actionTaken** del tipo de datos String y especifique la variable como la variable **Route**. Por ejemplo, actionTaken. Además, agregue las rutas Aprobar y Rechazar. Las rutas se muestran como acciones independientes (botones) en la Bandeja de entrada de AEM. El flujo de trabajo selecciona una rama en función de la acción (botón) que toca un usuario.

   Puede importar el paquete de ejemplo, disponible para descargar al principio de la sección, para el conjunto completo de valores de todos los campos del paso de tarea de asignación configurado, por ejemplo, la aplicación de hipoteca.

1. Arrastre y suelte el componente O dividido desde el navegador de pasos hasta el modelo de flujo de trabajo. La división O crea una división en el flujo de trabajo, tras la cual solo una rama está activa. Este paso le permite introducir rutas de procesamiento condicionales en el flujo de trabajo. Puede agregar pasos de flujo de trabajo a cada rama según sea necesario.

   Puede definir la expresión de enrutamiento para una rama mediante una definición de regla, una secuencia de comandos ECMA o una secuencia de comandos externa.

   Utilice el editor de expresiones para crear expresiones de enrutamiento para las ramas 1 y 2. Estas expresiones de enrutamiento ayudan a elegir una rama en función de la acción del usuario en la Bandeja de entrada de AEM.

   **Expresión de enrutamiento para la rama 2**

   Cuando un usuario toca **Aprobar** en la bandeja de entrada de AEM, se activa la rama 1.

   ![Ejemplo de división OR](assets/orsplit_branch1_active_new.png)

   **Expresión de enrutamiento para la rama 2**

   Cuando un usuario toca **Rechazar** en la bandeja de entrada de AEM, se activa la rama 2.

   ![Ejemplo de división OR](assets/orsplit_branch2_active_new.png)

   Para obtener información sobre la creación de expresiones de enrutamiento mediante variables, consulte [Variables en flujos de trabajo](../../forms/using/variable-in-aem-workflows.md)de AEM Forms.

1. Agregue otros pasos del flujo de trabajo para crear la lógica empresarial.

   Para el ejemplo de hipoteca, agregue un documento de generación de registros, dos pasos de tareas de asignación y un paso de documento de firma a la Rama 1 del modelo, como se muestra en la siguiente imagen. Un paso de tarea de asignación es mostrar y enviar **a los candidatos** documentos de préstamo firmados y otro componente de tarea de asignación es **mostrar documentos** firmados. Además, agregue un componente de tarea de asignación a la ramificación 2. Se activa cuando un usuario toca Rechazar en la bandeja de entrada de AEM.

   Para el conjunto completo de valores de todos los campos de los pasos de tarea de asignación, el paso del documento de registro y el paso del documento de firma configurados, por ejemplo, la aplicación de hipoteca, importe el paquete de ejemplo, disponible para su descarga al comienzo de esta sección.

   El modelo de flujo de trabajo está listo. Puede iniciar el flujo de trabajo mediante varios métodos. Para obtener más información, consulte [Iniciar un flujo de trabajo centrado en formularios en OSGi](../../forms/using/aem-forms-workflow.md#main-pars-header).

   ![workflow-editor-hipoteca](assets/workflow-editor-mortgage.png)

## Creación de una aplicación de flujo de trabajo centrada en formularios {#create-a-forms-centric-workflow-application}

La aplicación es el formulario adaptable asociado al flujo de trabajo. Cuando una aplicación se envía a través de la Bandeja de entrada, inicia el flujo de trabajo asociado. Para que un flujo de trabajo de formularios esté disponible como aplicación en AEM Inbox y AEM Forms App, haga lo siguiente para crear una aplicación de flujo de trabajo:

>[!NOTE]
>
>Debe ser miembro del grupo fd-admin para poder crear y administrar aplicaciones de flujo de trabajo.

1. En la instancia de autor de AEM, vaya a ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]**> **[!UICONTROL Manage Workflow Application]** y toque **[!UICONTROL Create]**.
1. En la ventana Crear aplicación de flujo de trabajo, proporcione entradas para los campos siguientes y toque **Crear**. Se crea una nueva aplicación y se muestra en la pantalla Aplicaciones de flujo de trabajo.

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Descripción</td>
  </tr>
  <tr>
   <td>Título</td>
   <td>El título está visible en la Bandeja de entrada de AEM y ayuda a los usuarios a elegir una aplicación. Manténgalo descriptivo. Por ejemplo, Guardar la aplicación de apertura de cuenta.<br /> </td>
  </tr>
  <tr>
   <td>Nombre </td>
   <td>Especifique el nombre de la aplicación. Todos los caracteres que no sean alfabetos, números, guiones y subrayados se sustituyen por guiones. </td>
  </tr>
  <tr>
   <td>Descripción</td>
   <td>La descripción está visible en la Bandeja de entrada de AEM. Proporcione información detallada sobre la aplicación en los campos de descripción. Por ejemplo, el propósito de la aplicación.<br /> </td>
  </tr>
  <tr>
   <td>Formulario adaptable</td>
   <td><p>Especifique la ruta de un formulario adaptable. Cuando un usuario inicia una aplicación, se muestra el formulario adaptable especificado.</p> <p><strong>Nota</strong>: Las aplicaciones de flujo de trabajo no admiten formularios ni documentos PDF que tengan más de una página o que requieran desplazamiento en el iPad de Apple. Cuando se abre una aplicación en Apple iPad y el formulario adaptable o el documento PDF es más largo que una página, se pierden los campos y el contenido del formulario de la segunda página.</p> </td>
  </tr>
  <tr>
   <td>Grupo de acceso</td>
   <td><p>Seleccione un grupo. La aplicación solo está visible en la Bandeja de entrada de AEM para los miembros del grupo seleccionado. La opción de grupo de acceso permite seleccionar todos los grupos del grupo de usuarios del flujo de trabajo. </p> <br /> </td>
  </tr>
  <tr>
   <td>Servicio de prerrellenar</td>
   <td>Seleccione un servicio <a href="../../forms/using/prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">de</a> cumplimentación previa para el formulario adaptable.<br /> </td>
  </tr>
  <tr>
   <td>Modelo de flujo de trabajo</td>
   <td>Seleccione un modelo <a href="../../forms/using/aem-forms-workflow.md#create-a-workflow-model">de</a> flujo de trabajo para la aplicación. Un modelo de flujo de trabajo consiste en la lógica y el flujo del proceso comercial. </td>
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
   <td>Especifique la ruta del archivo Documento de registro en crx-repositorio. La ruta es relativa a la ubicación de carga útil del formulario adaptable. Incluya siempre el nombre completo del archivo, incluida la extensión, si corresponde. Por ejemplo, [carga útil]/DOR/creditcard.pdf.</td>
  </tr>
 </tbody>
</table>

## Iniciar un flujo de trabajo centrado en formularios en OSGi {#launch}

Puede iniciar o activar un flujo de trabajo centrado en Forms mediante:

* [Envío de una aplicación desde la bandeja de entrada de AEM](#inbox)
* [Envío de una aplicación desde la aplicación de AEM Forms](#afa)

* [Envío de un formulario adaptable](#af)
* [Uso de la carpeta vigilada](#watched)

* [Envío de una comunicación interactiva o una carta](#letter)

### Envío de una aplicación desde la bandeja de entrada de AEM {#inbox}

La aplicación de flujo de trabajo que ha creado está disponible como una aplicación en la Bandeja de entrada. Los usuarios que son miembros del grupo de usuarios del flujo de trabajo pueden rellenar y enviar la aplicación que activa el flujo de trabajo asociado. Para obtener información sobre el uso de la Bandeja de entrada de AEM para enviar aplicaciones y administrar tareas, consulte [Gestión de aplicaciones y tareas de formularios en la Bandeja de entrada](../../forms/using/manage-applications-inbox.md)de AEM.

### Envío de una aplicación desde la aplicación de AEM Forms {#afa}

La aplicación de AEM Forms se sincroniza con un servidor de AEM Forms y le permite realizar cambios en los datos de formulario, las tareas, las aplicaciones de flujo de trabajo y la información guardada (borradores/plantillas) en su cuenta. Para obtener más información, consulte Aplicación [de formularios](/help/forms/using/aem-forms-app.md) AEM y artículos relacionados.

### Envío de un formulario adaptable {#af}

Puede configurar las acciones de envío de un formulario adaptable para iniciar un flujo de trabajo al enviar el formulario adaptable. Los formularios adaptables proporcionan la **acción de envío Invocar un flujo de trabajo** de AEM para iniciar un flujo de trabajo al enviar un formulario adaptable. Para obtener información detallada sobre la acción de envío, consulte [Configuración de la acción](../../forms/using/configuring-submit-actions.md)Enviar. Para enviar un formulario adaptable a través de la aplicación de AEM Forms, habilite Sincronizar con la aplicación de AEM Forms en las propiedades del formulario adaptable.

Puede configurar un formulario adaptable para sincronizar, enviar y activar un flujo de trabajo desde la aplicación de AEM Forms. Para obtener más información, consulte [Uso de un formulario](/help/forms/using/working-with-form.md).

### Uso de una carpeta vigilada {#watched}

Un administrador (un miembro del grupo de administradores de fd) puede configurar una carpeta de red para ejecutar un flujo de trabajo preconfigurado cuando un usuario coloca un archivo (como un archivo PDF) en la carpeta. Una vez completado el flujo de trabajo, puede guardar el archivo de resultados en una carpeta de salida especificada. Dicha carpeta se conoce como [Carpeta](../../forms/using/watched-folder-in-aem-forms.md)vigilada. Realice el siguiente procedimiento para configurar una carpeta vigilada para iniciar un flujo de trabajo:

1. En la instancia de autor de AEM, vaya a ![tools-1](assets/tools-1.png) **>**[!UICONTROL Forms]**> Configure Watched Folder.** Se muestra una lista de carpetas ya configuradas vigiladas.
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
   <td>Especifique la ubicación física de la carpeta vigilada. En un entorno agrupado, utilice una carpeta de red compartida a la que se pueda acceder desde el nodo de clúster de AEM.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Procesar archivos mediante</code></td>
   <td>Seleccione la <span class="uicontrol">opción </code>Flujo de trabajo. </code></td>
  </tr>
  <tr>
   <td><span class="uicontrol">Modelo de flujo de trabajo</code></td>
   <td>Select a workflow model.<br /> </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Patrón de archivo de salida</code></td>
   <td>Especifique la estructura de directorios para los archivos de salida y los directorios. También puede especificar un <a href="/help/forms/using/admin-help/configuring-watched-folder-endpoints.md" target="_blank">patrón para archivos de salida y directorios</a>.</td>
  </tr>
 </tbody>
</table>

1. Toque **Avanzado**. Especifique un valor para el campo siguiente y toque **Crear**. La carpeta vigilada está configurada para iniciar un flujo de trabajo. Ahora, cada vez que se coloca un archivo en el directorio de entrada de la carpeta vigilada, se activa el flujo de trabajo especificado.

   | Campo | Descripción |
   |---|---|
   | Filtro de asignador de cargas útiles | Cuando se crea una carpeta vigilada, se crea una estructura de carpetas en el repositorio crx. La estructura de carpetas puede servir como carga útil para el flujo de trabajo. Puede escribir una secuencia de comandos para asignar un flujo de trabajo de AEM y aceptar entradas de la estructura de carpetas observada. Hay una implementación lista para usar disponible que se muestra en el filtro del asignador de carga útil. Si no tiene una implementación personalizada, seleccione la implementación predeterminada. |

   La ficha Avanzado contiene más campos. La mayoría de estos campos contienen un valor predeterminado. Para obtener más información sobre todos los campos, consulte el artículo [Crear o configurar una carpeta](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md) vigilada.

### Envío de una comunicación interactiva o una carta {#letter}

Puede asociar y ejecutar un flujo de trabajo centrado en formularios en OSGi al enviar una comunicación interactiva o una carta. En los flujos de trabajo de gestión de correspondencia se utilizan para las comunicaciones y cartas interactivas posteriores al procesamiento. Por ejemplo, enviar por correo electrónico, imprimir, enviar por fax o archivar letras finales. Para ver los pasos detallados, consulte [Postprocesamiento de comunicaciones interactivas y cartas](../../forms/using/submit-letter-topostprocess.md).

## Configuraciones adicionales {#additional-configurations}

### Configurar servicio de correo electrónico {#configure-email-service}

Puede utilizar los pasos Asignar tarea y Enviar correo electrónico de los flujos de trabajo de AEM para enviar un correo electrónico. Realice los siguientes pasos para especificar los servidores de correo electrónico y otras configuraciones necesarias para enviar correo electrónico:

1. Vaya al administrador de configuración de AEM en https://[server]:[port]/system/console/configMgr.
1. Abra la configuración **[!UICONTROL Día del servicio]** de correo de CQ. Especifique un valor para los campos de nombre **[!UICONTROL de host del servidor]** SMTP, **[!UICONTROL puerto del servidor]** SMTP y dirección **** &quot;De&quot;. Haga clic en **[!UICONTROL Guardar]**.
1. Abra la configuración **[!UICONTROL Day CQ Link Externalizer]** . En el campo **[!UICONTROL Dominios]** , especifique el nombre de host/dirección IP real y el número de puerto para las instancias locales, de autor y de publicación. Haga clic en **[!UICONTROL Guardar]**.

### Purgar instancias de flujo de trabajo {#purge-workflow-instances}

Al minimizar el número de instancias de flujo de trabajo, aumenta el rendimiento del motor de flujo de trabajo, de modo que puede depurar regularmente instancias de flujo de trabajo completadas o en ejecución del repositorio. Para obtener información detallada, consulte Depuración [regular de instancias]de flujo de trabajo (/help/sites-administering/workflows-administering.md#normal purgar instancias de flujo de trabajo).
