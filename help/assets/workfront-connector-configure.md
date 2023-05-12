---
title: Configuración de [!DNL Workfront for Experience Manager enhanced connector]
description: Configuración de [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2660de7c-0281-4884-98d9-e78f20cf571c
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1737'
ht-degree: 1%

---

# Configuración de [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-configure.html?lang=en) |
| AEM 6.5 | Este artículo |

Un usuario con acceso de administrador en [!DNL Adobe Experience Manager] configura el conector mejorado después de instalarlo. Para obtener instrucciones sobre la instalación, consulte [Instalación del conector](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
>* El Adobe requiere la implementación y la configuración del [!DNL Adobe Workfront for Experience Manager enhanced connector] solo a través de socios certificados o [!DNL Adobe Professional Services]. Si se implementa y se configura sin un socio certificado o [!DNL Adobe Professional Services], no es compatible con Adobe.
>
>* Adobe puede publicar actualizaciones en [!DNL Adobe Workfront] y [!DNL Adobe Experience Manager] que hacen que este conector sea redundante; si esto ocurre, es posible que se requiera a los clientes que pasen del uso de este conector.
>
>* Adobe admite las versiones 1.7.4 y posteriores del conector mejorado. No se admiten versiones anteriores y personalizadas. Para comprobar la versión del conector mejorado, vaya a la `digital.hoodoo` grupo disponible en el panel izquierdo de [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es).
>
>* Consulte [Examen de certificación de socios para conector mejorado de Workfront para Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obtener información acerca del examen, consulte [Guía de examen](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


## Configurar suscripciones de eventos {#event-subscriptions}

Las suscripciones de eventos se utilizan para notificar a AEM los eventos que se producen en [!DNL Adobe Workfront]. Hay tres [!DNL Workfront for Experience Manager enhanced connector] funciones que necesitan suscripciones de eventos para funcionar, son las siguientes:

* Creación automática de carpetas vinculadas a proyectos.
* Sincronización de los cambios en Workfront documenta valores de formulario personalizados a metadatos de AEM recurso.
* Publicación automática de recursos en Brand Portal tras la finalización del proyecto.

Para utilizar estas funciones, habilite suscripciones de eventos.

* Editar [!UICONTROL Herramientas de Workfront] La configuración de Cloud Services que ha creado en el paso 5 y seleccione la [!UICONTROL Suscripciones de eventos] pestaña .
* Seleccione el [!UICONTROL Integración personalizada de Workfront] creado en la sección 6.
* Haga clic en [!UICONTROL Habilitar suscripciones de eventos de Workfront].

   ![Suscripción al evento](/help/assets/assets/event-subs.png)

## Configuración de carpetas vinculadas {#linked-folders}

Para suscribirse a los eventos, siga estos pasos:

1. Vaya a la **[!UICONTROL Suscripciones de eventos]** en los servicios de nube.
1. Seleccione la integración personalizada creada en [!DNL Workfront].
1. Haga clic en **[!UICONTROL Habilitar suscripciones de eventos de Workfront]**.

### Configuración de estructura de carpetas vinculadas {#linked-folder-structure}

1. Vaya a la pestaña Carpetas vinculadas al proyecto en los servicios de nube.
1. Ruta principal de la carpeta vinculada: Seleccione una carpeta en DAM donde desee crear las carpetas vinculadas. Si se deja vacío, pasará de forma predeterminada a /content/dam. Asegúrese de que el esquema de metadatos de las herramientas de Workfront y el esquema de metadatos de la carpeta vinculada de Workfront se hayan aplicado a la carpeta seleccionada.
1. Estructura de carpetas vinculadas: Introduzca valores separados por comas. Cada valor debe `DE:<some-project-custom-form-field>`, Portfolio, Programa, Año, Nombre o &quot;Valor de cadena literal&quot; (este último con comillas). Actualmente está establecido en Portfolio,Programa,Año,DE:Tipo de proyecto,Nombre.
1. La casilla de verificación Generar título de carpeta vinculada en Workfront utilizando los nombres de estructura de carpetas debe activarse si el título de la carpeta en Workfront debe incluir todas las carpetas de la estructura. De lo contrario, será el título de la última carpeta.
1. Sub-folders multifield permite especificar una lista de carpetas que deben crearse como una carpeta secundaria de la carpeta vinculada.
1. Estado del proyecto: Seleccione el estado en el que debe configurarse el proyecto para crear la carpeta vinculada.
1. Cree una carpeta vinculada en proyectos con portafolio: Lista de Portfolio a los que debe pertenecer el proyecto para crear la carpeta vinculada. Deje esta lista vacía para crear la carpeta vinculada para todo el portafolio de proyectos.
1. Cree una carpeta vinculada en proyectos con un campo de formulario personalizado: Campo de formulario personalizado y su valor correspondiente que el proyecto debe tener para crear la carpeta vinculada. Esta configuración se ignorará si se deja vacía. Select `CUSTOM FORMS: Create DAM Linked Folder` para el campo y la entrada `Yes` para el valor.
1. Haga clic en Habilitar la creación automática de carpetas vinculadas. Si vuelve a la pestaña Suscripciones de eventos , verá que ahora hay un evento de creación.

![configuración de carpeta vinculada](/help/assets/assets/wf-linked-folder-config.png)

## Asignación de esquemas de metadatos {#metadata-schema-mapping}

### Configuración de la asignación de metadatos de carpetas {#folder-metadata-mapping}

La asignación de metadatos entre proyectos de Workfront y carpetas de AEM se define en AEM esquemas de metadatos de carpeta. Los esquemas de metadatos de carpeta deben crearse y configurarse de la forma habitual en AEM. Herramientas de Workfront agrega un menú desplegable de autocompletado a la ficha Configuración de cada campo de formulario de esquema de metadatos de carpeta. Este menú desplegable de autocompletar le permite especificar a qué campo de Workfront se debe asignar cada propiedad de carpeta de AEM.

Para configurar las asignaciones, siga estos pasos:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Esquemas de metadatos de carpeta]**.
1. Seleccione el formulario de esquema de metadatos de carpeta que desea editar y haga clic en Editar.
1. Seleccione el campo de formulario de esquema de metadatos de carpeta que desea editar y seleccione la pestaña Configuración en el panel derecho.
1. En [!UICONTROL Asignado desde el campo Workfront] , seleccione el nombre del campo Workfront que desea asignar a la propiedad carpeta de AEM seleccionada. Las opciones disponibles son:

   * Campos de formulario personalizados del proyecto
   * Campos Información general del proyecto (ID, nombre, descripción, número de referencia, fecha de finalización planeada, propietario del proyecto, patrocinador del proyecto, Portfolio o programa)

![configuración de asignación de metadatos](/help/assets/assets/wf-metadata-mapping-config2.png)

### Configuración de la asignación de metadatos de recursos {#asset-metadata-mapping}

La asignación de metadatos entre documentos y recursos de Adobe Workfront se define dentro de AEM esquemas de metadatos. Los esquemas de metadatos deben crearse y configurarse de la forma habitual en AEM. Las herramientas de Workfront añaden opciones de configuración a la ficha Configuración de cada campo de formulario de esquema de metadatos. Estas opciones le permiten especificar a qué campo de Workfront se debe asignar cada propiedad de AEM.

Para configurar las asignaciones, siga estos pasos:

1. Vaya a **Herramientas** > **Recursos** > **Esquemas de metadatos**.
1. Seleccione el formulario de esquema de metadatos que desea editar y haga clic en **Editar** o crear un nuevo esquema de metadatos desde cero.
1. Seleccione el campo del formulario de esquema de metadatos que desea editar y seleccione **Configuración** en el panel derecho.
1. En [!DNL Workfront] Campo de formulario personalizado seleccione el nombre del [!DNL Workfront] campo que desea asignar a la propiedad AEM seleccionada. Las opciones disponibles son:

   * Documentar campos de formulario personalizados
   * Campos de formulario personalizados del proyecto
   * Problemas con campos de formulario personalizados
   * Campos de formulario personalizados de tarea
   * Campos Información general del proyecto (ID, nombre, descripción o número de referencia)

1. En el caso de que la variable [!DNL Workfront] campo seleccionado en [!UICONTROL Campo de formulario personalizado de Workfront] es un campo de avance de tipo Usuario de Workfront , será necesario especificar qué campo Usuario de Workfront desea asignar. Para ello, marque Get value from Workfront referenced object field y luego especifique el nombre del [!UICONTROL Campo de formulario personalizado del usuario de Workfront] desde el cual recuperar el valor que se va a asignar.

   ![configuración de asignación de metadatos](/help/assets/assets/wf-metadata-mapping-config1.png)

## Asignar, propiedad {#map-property}

Este paso del flujo de trabajo permite al usuario asignar una propiedad a un [!DNL Workfront] formulario personalizado en un proyecto, tarea, problema o documento. La variable [!DNL Workfront] artefacto al que afecta este paso se busca utilizando una ruta relativa de la carga útil. Las propiedades que se van a asignar se controlan desde la configuración del cuadro de diálogo pasos.

**Tipo**: Este campo permite seleccionar el tipo de objeto Workfront al que se deben asignar las propiedades.

**Propiedad ID**: Este campo permite especificar la ruta al ID del objeto Workfront al que se deben asignar las propiedades. La ruta especificada en este campo debe ser relativa a la carga útil del flujo de trabajo.

**Asignaciones de propiedades**: Este campo múltiple permite especificar las asignaciones entre AEM propiedades y los campos de Workfront. Cada elemento del campo múltiple especificará una asignación. Cada asignación debe tener el formato `<workfront-field>=<aem-mapped-property>`.

* La variable `workfront-field` can

   * Un campo de formulario personalizado identificado por el prefijo `DE:`.
   * Campo editable identificado por su nombre. Los nombres de campo se encuentran en [[!DNL Workfront] Explorador de API](https://experience.workfront.com/s/api-explorer).

* La variable `aem-mapped-property` puede ser:

   * Un valor literal. Deben estar entre comillas.
   * Una propiedad AEM. Esta referencia debe ser relativa a la carga útil del flujo de trabajo.
   * Un valor con nombre. Deben estar entre corchetes.
   * Una concatenación de los 3 elementos anteriores. Especifique el mediante `{+}`.
   * Una alteración de los 3 elementos anteriores rodeando el valor con `{replace(<value>,"old-char","new-char")}`.

* Algunos ejemplos son:

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![Configuración para asignar la propiedad](/help/assets/assets/wf-map-property-config.png)

## Establecer estado {#set-status}

En el editor de flujo de trabajo, edite las propiedades de **[!UICONTROL Workfront: Establecer estado]** en el **[!UICONTROL Argumentos]** pestaña .

![Editar flujo de trabajo para establecer el estado](/help/assets/assets/wf-set-status.png)

## Sincronización de comentarios {#comments-sync}

1. En [!DNL Experience Manager], acceso **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de herramientas de Workfront]**, seleccione la configuración y, **[!UICONTROL Propiedades]**.

   ![sincronización de comentarios](/help/assets/assets/comments-sync1.png)

1. Select **[!UICONTROL Suscripciones de eventos]** , haga clic en **[!UICONTROL Habilitar sincronización de comentarios]** en **[!UICONTROL Enviar comentarios realizados en Workfront a AEM]** .

   ![La sincronización está habilitada](/help/assets/assets/wf-comment-sync-enabled.png)

Para probar la sincronización de comentarios de Workfront a AEM, siga estos pasos:

1. Vaya a un documento vinculado en Workfront y añada un comentario en la pestaña Actualizaciones .

   ![dejar comentario en Workfront](/help/assets/assets/comments-sync2.png)

1. Vaya al mismo documento vinculado en AEM, seleccione el documento y abra el [!UICONTROL Cronología] en el panel de navegación izquierdo y seleccione [!UICONTROL Comentarios]. La barra lateral izquierda muestra los comentarios sincronizados desde [!DNL Workfront].

## Versiones de recursos {#asset-versions}

Para mantener el historial de versiones de los recursos en AEM, configure las versiones de los recursos en AEM.

1. En el Experience Manager, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de herramientas de Workfront]** y abra el **[!UICONTROL Avanzadas]** pestaña .

1. Opción Select **[!UICONTROL Almacenar recursos con el mismo nombre que las versiones del recurso existente]**. Cuando está activada, esta opción permite almacenar los recursos cargados con el mismo nombre y en la misma ubicación que la versión del recurso existente. Si se deja sin marcar, se creará un nuevo recurso con un nombre diferente (por ejemplo, `asset-name.pdf` y `asset-name-1.pdf`).

1. Opción Select **[!UICONTROL Actualizar metadatos de recursos al crear una nueva versión]**. Cuando está activada, esta opción actualiza los metadatos del recurso cada vez que se crea una nueva versión del recurso. Si no está activada, el recurso conserva los metadatos que tenía antes de crear la nueva versión.

![configurar versiones de recursos](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>El control de versiones no se admite en carpetas vinculadas. Al crear un [!DNL Workfront] con un documento dentro de una carpeta vinculada, los comentarios y anotaciones de la versión anterior del recurso se eliminan.

## Adjuntar formularios personalizados {#attach-custom-forms}

Este paso del flujo de trabajo permite a los usuarios adjuntar un formulario personalizado a una [!DNL Workfront] artefacto. Este paso del flujo de trabajo se puede añadir a cualquier modelo de flujo de trabajo. La variable [!DNL Workfront] artefacto al que afecta este paso se buscará usando una ruta relativa de la carga útil.

En el editor de flujo de trabajo en Experience Manager, edite las propiedades de la variable [!UICONTROL Workfront: adjuntar formulario personalizado] paso del flujo de trabajo.

![formularios personalizados](/help/assets/assets/wf-custom-forms.png).

## Publicación automática de recursos {#auto-publish-assets}

1. En el Experience Manager, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de herramientas de Workfront]** y abra el **[!UICONTROL Avanzadas]** pestaña .

1. Select **[!UICONTROL Publicar recursos automáticamente al enviarlos desde Workfront]**. Esta opción permite la publicación automática de los recursos cuando se envían de Workfront a AEM. Esta función se puede habilitar condicionalmente especificando un campo de formulario personalizado de Workfront y el valor que debe establecerse. Cada vez que se envía un documento a AEM, si cumple la condición, el recurso se publicará automáticamente.

1. Select **[!UICONTROL Publicar todos los recursos del proyecto en Brand Portal al finalizar el proyecto]**. Esta opción permite la publicación automática de recursos en [!DNL Brand Portal] cuando el estado del proyecto de Workfront al que pertenecen cambia a `Complete`.

![configurar la publicación automática](/help/assets/assets/wf-auto-publish-config.png)

## Actualizaciones de formularios personalizados de Workfront document {#subscribe-workfront-doc-custom-form-updates}

Para suscribirse a los cambios en [!DNL Workfront] documentar formularios personalizados, seleccione la opción correspondiente en la **[!UICONTROL Avanzadas]** pestaña . Al suscribirse a estas actualizaciones, se actualiza la asignación de [!DNL Experience Manager] campos de metadatos cuando el campo correspondiente de [!DNL Workfront] el formulario personalizado del documento ha cambiado.

![Configuración de actualizaciones de formulario personalizadas de Workfront document en [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
