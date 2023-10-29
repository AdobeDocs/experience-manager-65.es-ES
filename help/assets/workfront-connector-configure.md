---
title: Configuración de [!DNL Workfront for Experience Manager enhanced connector]
description: Configuración de [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2660de7c-0281-4884-98d9-e78f20cf571c
hide: true
source-git-commit: a07765f95f01f05a30dce14138f75e7edbe94ae2
workflow-type: tm+mt
source-wordcount: '1740'
ht-degree: 1%

---

# Configuración de [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-configure.html?lang=en) |
| AEM 6.5 | Este artículo |

Un usuario con acceso de administrador en [!DNL Adobe Experience Manager] configura el conector mejorado después de instalarlo. Para obtener instrucciones de instalación, consulte [Instale el conector](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
>* El Adobe requiere la implementación y la configuración de [!DNL Adobe Workfront for Experience Manager enhanced connector] solo a través de socios certificados o [!DNL Adobe Professional Services]. Si se implementa y configura sin un socio certificado o [!DNL Adobe Professional Services], no es compatible con el Adobe.
>
>* El Adobe puede publicar actualizaciones en [!DNL Adobe Workfront] y [!DNL Adobe Experience Manager] que hacen que este conector sea redundante; si esto sucede, es posible que los clientes deban realizar la transición desde el uso de este conector.
>
>* El Adobe admite las versiones de conector mejoradas 1.7.4 y posteriores. No se admiten versiones preliminares ni versiones personalizadas anteriores. Para comprobar la versión mejorada del conector, vaya a `digital.hoodoo` grupo disponible en el panel izquierdo de [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es).
>
>* Consulte [Examen de certificación de socio para el conector mejorado de Workfront para Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obtener más información sobre el examen, consulte [Guía del examen](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## Configuración de suscripciones a eventos {#event-subscriptions}

AEM Las suscripciones a eventos se utilizan para notificar a los usuarios de eventos que tienen lugar en el [!DNL Adobe Workfront]. Hay tres [!DNL Workfront for Experience Manager enhanced connector] Las funciones que necesitan suscripciones de evento para funcionar son las siguientes:

* Creación automática de carpetas vinculadas a proyectos.
* Sincronización de cambios en los valores del formulario personalizado de documentos de Workfront AEM para crear metadatos de recursos de la aplicación
* Publicación automática de recursos en Brand Portal al finalizar el proyecto.

Para utilizar estas funciones, habilite las suscripciones a eventos.

* Editar [!UICONTROL Herramientas de Workfront] Configuración de Cloud Service creada en el paso 5 y seleccione. [!UICONTROL Suscripciones de eventos] pestaña.
* Seleccione el [!UICONTROL Integración personalizada de Workfront] ha creado en la sección 6.
* Clic [!UICONTROL Habilitar suscripciones a eventos de Workfront].

  ![Suscripción de evento](/help/assets/assets/event-subs.png)

## Configuración de carpetas vinculadas {#linked-folders}

Para suscribirse a los eventos, siga estos pasos:

1. Vaya a **[!UICONTROL Suscripciones de eventos]** en cloud services.
1. Seleccione la integración personalizada creada en [!DNL Workfront].
1. Clic **[!UICONTROL Habilitar suscripciones a eventos de Workfront]**.

### Configuración de estructura de carpetas vinculadas {#linked-folder-structure}

1. Vaya a la pestaña Carpetas vinculadas del proyecto en los servicios en la nube.
1. Ruta principal de la carpeta vinculada: seleccione una carpeta en DAM en la que desee crear las carpetas vinculadas. Si se deja vacío, el valor predeterminado será /content/dam. Asegúrese de que el esquema de metadatos de Workfront Tools y el esquema de metadatos de la carpeta de carpetas vinculadas de Workfront se hayan aplicado a la carpeta seleccionada.
1. Estructura de carpetas vinculadas: introduzca valores separados por comas. Cada valor debe ser `DE:<some-project-custom-form-field>`, Portfolio, Programa, Año, Nombre o algún &quot;Valor de cadena literal&quot; (este último con comillas). Actualmente está establecido en Portfolio, Programa, Año, DE: Tipo de proyecto, Nombre.
1. La casilla de verificación Generar título de carpeta vinculado en Workfront mediante los nombres de estructura de carpetas debe activarse si el título de la carpeta en Workfront debe incluir todas las carpetas de la estructura. De lo contrario, será el título de la última carpeta.
1. Subcarpetas multicampo permite especificar una lista de carpetas que deben crearse como una carpeta secundaria de la carpeta vinculada.
1. Estado del proyecto: seleccione el estado en el que debe configurarse el proyecto para crear la carpeta vinculada.
1. Crear una carpeta vinculada en proyectos con portafolio: lista de Portfolio a los que debe pertenecer el proyecto para crear la carpeta vinculada. Deje esta lista vacía para crear la carpeta vinculada para todo el portafolio de proyectos.
1. Crear una carpeta vinculada en proyectos con un campo de formulario personalizado: Campo de formulario personalizado y su valor correspondiente que el proyecto debe tener para crear la carpeta vinculada. Esta configuración se ignorará si se deja vacía. Seleccionar `CUSTOM FORMS: Create DAM Linked Folder` para campo y entrada `Yes` para el valor.
1. Haga clic en Habilitar la creación automática de carpetas vinculadas. Si vuelve a la pestaña Suscripciones de eventos, verá que ahora hay un evento de creación.

![configuración de carpeta vinculada](/help/assets/assets/wf-linked-folder-config.png)

## Asignación de esquema de metadatos {#metadata-schema-mapping}

### Configurar asignación de metadatos de carpeta {#folder-metadata-mapping}

La asignación de metadatos entre proyectos de Workfront AEM AEM y carpetas de recursos se define dentro de los esquemas de metadatos de carpeta de. AEM Los esquemas de metadatos de carpeta deben crearse y configurarse de la forma habitual en las carpetas de trabajo de los recursos Workfront Tools agrega un menú desplegable de autocompletar a la pestaña Configuración de configuración de cada campo del formulario de esquema de metadatos de carpeta. Este menú desplegable de autocompletar le permite especificar a qué campo de Workfront AEM debe asignarse cada propiedad de carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de destino.

Para configurar las asignaciones, siga estos pasos:

1. Añadir `jcr:read` permisos para `/conf/global/settings/dam/adminui-extension/foldermetadataschema` para `wf-workfront-users` grupo.
1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos de carpeta]**.
1. Seleccione el formulario de esquema de metadatos de carpeta que desee editar y haga clic en Editar.
1. Seleccione el campo del formulario del esquema de metadatos de la carpeta que desea editar y seleccione la pestaña Configuración en el panel derecho.
1. Entrada [!UICONTROL Asignado desde el campo de Workfront] , seleccione el nombre del campo de Workfront AEM que desea asignar a la propiedad de carpeta de la carpeta seleccionada. Las opciones disponibles son:

   * Campos de formulario personalizados del proyecto
   * Campos de Información general del proyecto (ID, nombre, descripción, número de referencia, fecha planificada de finalización, propietario del proyecto, patrocinador del proyecto, Portfolio o programa)

![configuración de asignación de metadatos](/help/assets/assets/wf-metadata-mapping-config2.png)

### Configuración de la asignación de metadatos de recursos {#asset-metadata-mapping}

La asignación de metadatos entre documentos y recursos de Adobe Workfront AEM se define dentro de los esquemas de metadatos de la. AEM Los esquemas de metadatos deben crearse y configurarse de la forma habitual en los archivos de datos de la interfaz de usuario de. Workfront Tools agrega opciones de configuración a la pestaña Configuración de cada campo del formulario de esquema de metadatos. Estas opciones le permiten especificar a qué campo de Workfront AEM debe asignarse cada propiedad de.

Para configurar las asignaciones, siga estos pasos:

1. Vaya a **Herramientas** > **Assets** > **Esquemas de metadatos**.
1. Seleccione el formulario de esquema de metadatos que desee editar y haga clic en **Editar** o cree un nuevo esquema de metadatos desde cero.
1. Seleccione el campo del formulario de esquema de metadatos que desea editar y seleccione **Configuración** en el panel derecho.
1. Entrada [!DNL Workfront] Campo de formulario personalizado, seleccione el nombre del [!DNL Workfront] AEM que desee asignar a la propiedad seleccionada de la. Las opciones disponibles son:

   * Documentar campos de formulario personalizados
   * Campos de formulario personalizados del proyecto
   * Emitir campos de formulario personalizados
   * Campos de formulario personalizados de tarea
   * Campos Información general del proyecto (ID, Nombre, Descripción o Número de referencia)

1. En caso de que la variable [!DNL Workfront] campo seleccionado en [!UICONTROL Campo de formulario personalizado de Workfront] es un campo de escritura anticipada de usuario de Workfront, será necesario especificar qué campo de usuario de Workfront desea asignar. Para ello, marque Obtener valor del campo de objeto al que se hace referencia en Workfront y luego especifique el nombre del [!UICONTROL Campo de formulario personalizado de usuario de Workfront] desde el que se recupera el valor que se va a asignar.

   ![configuración de asignación de metadatos](/help/assets/assets/wf-metadata-mapping-config1.png)

## Asignar propiedad {#map-property}

Este paso del flujo de trabajo permite que un usuario asigne una propiedad a una [!DNL Workfront] formulario personalizado en un proyecto, tarea, problema o documento. El [!DNL Workfront] artefacto que este paso afecta se busca usando una ruta relativa desde la carga útil. Las propiedades que se van a asignar se controlan desde la configuración del cuadro de diálogo de pasos.

**Tipo**: Este campo permite seleccionar el tipo de objeto de Workfront al que se deben asignar las propiedades.

**Propiedad de ID**: Este campo permite especificar la ruta al ID del objeto de Workfront al que se deben asignar las propiedades. La ruta especificada en este campo debe ser relativa a la carga útil del flujo de trabajo.

**Asignaciones de propiedades** AEM : Este multicampo permite especificar las asignaciones entre las propiedades y los campos de Workfront de la. Cada elemento del campo múltiple especificará una asignación. Cada asignación debe tener el formato `<workfront-field>=<aem-mapped-property>`.

* El `workfront-field` puede ser

   * Campo de formulario personalizado identificado por el prefijo `DE:`.
   * Campo editable identificado por su nombre. Los nombres de campo se encuentran en [[!DNL Workfront] Explorador de API](https://experience.workfront.com/s/api-explorer).

* El `aem-mapped-property` puede ser:

   * Un valor literal. Deben ir entre comillas.
   * AEM Una propiedad de. Esta referencia debe ser relativa a la carga útil del flujo de trabajo.
   * Un valor con nombre. Estos deben ir entre corchetes.
   * Una concatenación de los tres elementos anteriores. Especifíquelo mediante `{+}`.
   * Una modificación de los 3 elementos anteriores al rodear el valor con `{replace(<value>,"old-char","new-char")}`.

* Algunos ejemplos son:

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![Configuración para asignar la propiedad](/help/assets/assets/wf-map-property-config.png)

## Definir estado {#set-status}

En el editor de flujo de trabajo, edite las propiedades de **[!UICONTROL Workfront - Definir estado]** en el **[!UICONTROL Argumentos]** pestaña.

![Editar flujo de trabajo para establecer el estado](/help/assets/assets/wf-set-status.png)

## Sincronización de comentarios {#comments-sync}

1. Entrada [!DNL Experience Manager], acceso **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configuración de herramientas de Workfront]**, seleccione la configuración y seleccione **[!UICONTROL Propiedades]**.

   ![sincronización de comentarios](/help/assets/assets/comments-sync1.png)

1. Seleccionar **[!UICONTROL Suscripciones de eventos]** pestaña, haga clic en **[!UICONTROL Habilitar sincronización de comentarios]** el **[!UICONTROL Envíe los comentarios realizados en Workfront AEM a la dirección de correo electrónico]** opción.

   ![La sincronización está habilitada](/help/assets/assets/wf-comment-sync-enabled.png)

Para probar la sincronización de los comentarios de Workfront AEM a la, siga estos pasos:

1. Vaya a un documento vinculado en Workfront y añada un comentario en la pestaña Actualizaciones.

   ![dejar comentario en Workfront](/help/assets/assets/comments-sync2.png)

1. AEM Navegue hasta el mismo documento vinculado en la sección, seleccione el documento y abra la pestaña [!UICONTROL Cronología] en el panel de navegación izquierdo y seleccione [!UICONTROL Comentarios]. La barra lateral izquierda muestra los comentarios sincronizados desde [!DNL Workfront].

## Versiones de recursos {#asset-versions}

AEM AEM Para mantener el historial de versiones de los recursos en la, configure el control de versiones de los recursos en la.

1. En Experience Manager, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configuración de herramientas de Workfront]** y abra el **[!UICONTROL Avanzadas]** pestaña.

1. Seleccionar opción **[!UICONTROL Almacenar recursos con el mismo nombre que las versiones del recurso existente]**. Cuando se selecciona, esta opción permite almacenar recursos cargados con el mismo nombre y en la misma ubicación que la versión del recurso existente. Si no se selecciona, se creará un nuevo recurso con un nombre diferente (por ejemplo, `asset-name.pdf` y `asset-name-1.pdf`).

1. Seleccionar opción **[!UICONTROL Actualizar los metadatos del recurso al crear una nueva versión]**. Cuando se selecciona, esta opción actualiza los metadatos del recurso cada vez que se crea una nueva versión del recurso. Si no se selecciona, el recurso conservará los metadatos que tenía antes de crear la nueva versión.

![configurar versiones de recursos](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>Las versiones no son compatibles con las carpetas vinculadas. Al crear un [!DNL Workfront] prueba con un documento dentro de una carpeta vinculada, se eliminan los comentarios y anotaciones de la versión anterior del recurso.

## Adjuntar formularios personalizados {#attach-custom-forms}

Este paso del flujo de trabajo permite a los usuarios adjuntar un formulario personalizado a una [!DNL Workfront] artefacto. Este paso del flujo de trabajo se puede agregar a cualquier modelo de flujo de trabajo. El [!DNL Workfront] artefacto que este paso afecta se buscará utilizando una ruta relativa desde la carga útil.

En el editor de flujo de trabajo de Experience Manager, edite las propiedades del [!UICONTROL Workfront: adjuntar formulario personalizado] paso de flujo de trabajo.

![formularios personalizados](/help/assets/assets/wf-custom-forms.png).

## Publicar recursos automáticamente {#auto-publish-assets}

1. En Experience Manager, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configuración de herramientas de Workfront]** y abra el **[!UICONTROL Avanzadas]** pestaña.

1. Seleccionar **[!UICONTROL Publicar recursos automáticamente cuando se envíen desde Workfront]**. Esta opción habilita la publicación automática de recursos cuando se envían de Workfront AEM a los recursos de la aplicación de la. Esta función se puede habilitar de forma condicional especificando un campo de formulario personalizado de Workfront y el valor en el que debe establecerse. AEM Siempre que se envíe un documento a la publicación, si cumple la condición, el recurso se publicará automáticamente.

1. Seleccionar **[!UICONTROL Publicar todos los recursos del proyecto en Brand Portal al finalizar el proyecto]**. Esta opción permite la publicación automática de recursos en [!DNL Brand Portal] cuando se cambie el estado del proyecto de Workfront al que pertenecen a `Complete`.

![configurar la publicación automática](/help/assets/assets/wf-auto-publish-config.png)

## Actualizaciones de formularios personalizados de documentos de Workfront {#subscribe-workfront-doc-custom-form-updates}

Para suscribirse a los cambios en [!DNL Workfront] para documentar los formularios personalizados, seleccione la opción correspondiente en la **[!UICONTROL Avanzadas]** pestaña. Al suscribirse a estas actualizaciones, se actualiza el asignado [!DNL Experience Manager] campos de metadatos cuando el campo correspondiente en [!DNL Workfront] se ha cambiado el formulario personalizado del documento.

![El documento de Workfront actualiza la configuración de formulario personalizado en [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
