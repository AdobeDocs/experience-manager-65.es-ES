---
title: Cómo crear un formulario adaptable
description: Aprenda a crear un formulario adaptable utilizando [!DNL Experience Manager Forms]. Los formularios adaptables son formularios HTML5 interactivos que agilizan la recopilación y el procesamiento de la información. Descubra más información sobre cómo crear un formulario adaptable basado en un modelo de datos de formulario, una plantilla de formulario XFA y un esquema XML o JSON.
feature: Adaptive Forms
role: User, Developer
level: Beginner
exl-id: 2c25a8b7-73f7-40fb-a303-9446a708c8eb
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1856'
ht-degree: 10%

---

# Creación de un formulario adaptable {#creating-an-adaptive-form}

## <strong>Creación de un formulario adaptable</strong> {#strong-create-an-adaptive-form-strong}

Siga estos pasos para crear un formulario adaptable.

1. Acceso [!DNL Experience Manager Forms] Instancia de autor en `https://'[server]:[port]'/<custom-context-if-any>.`

1. Introduzca sus credenciales en la página de inicio de sesión de Experience Manager.

   Cuando haya iniciado sesión, en la esquina superior izquierda, pulse **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.

   >[!NOTE]
   >
   >Para una instalación predeterminada, el inicio de sesión es `admin` y la contraseña es `admin`.

1. Pulse **[!UICONTROL Crear]** y seleccione **[!UICONTROL Formulario adaptable]**.
1. Aparece una opción para seleccionar una plantilla. Para obtener más información sobre las plantillas, consulte [Plantillas de formulario adaptables](creating-adaptive-form.md#p-adaptive-form-templates-p). Pulse una plantilla para seleccionarla y pulse Siguiente.
1. Aparece la opción &quot;Agregar propiedades&quot;. Especifique los valores para los siguientes campos de propiedad. Los campos Título y Nombre son obligatorios:

   * **[!UICONTROL Título:]** Especifica el nombre para mostrar del formulario. El título le ayuda a identificar el formulario en la interfaz de usuario de [!DNL Experience Manager Forms].
   * **[!UICONTROL Nombre:]** Especifica el nombre del formulario. Se crea un nodo con el nombre especificado en el repositorio. A medida que empieza a escribir un título, el valor del campo de nombre se genera automáticamente. Puede cambiar el valor sugerido. El campo de nombre solo puede incluir caracteres alfanuméricos, guiones y guiones bajos. Todas las entradas no válidas se sustituyen por guiones.
   * **[!UICONTROL Descripción:]** Especifica la información detallada sobre el formulario.
   * **[!UICONTROL Etiquetas:]** Especifica etiquetas para identificar de forma exclusiva el formulario adaptable. Las etiquetas ayudan a buscar en el formulario. Para crear etiquetas, escriba nuevos nombres de etiqueta en la **[!UICONTROL Etiquetas]** en la ventana

1. Puede crear un formulario adaptable basado en uno de los siguientes modelos de formulario:

   * [Modelo de datos de formulario](#fdm)
   * [Plantilla de formulario XFA](#create-an-adaptive-form-based-on-an-xfa-form-template)
   * [Esquema XML o JSON](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * Ninguno o sin modelo de formulario

   Puede configurarlos desde el **[!UICONTROL Modelo de formulario]** en la ficha **[!UICONTROL Agregar propiedades]** página. De forma predeterminada, el modelo de formulario seleccionado es **[!UICONTROL Ninguna]**.

1. Pulse **[!UICONTROL Crear]**. Se crea un formulario adaptable y aparece un cuadro de diálogo para abrir el formulario y editarlo.

   Una vez que haya terminado de especificar todas las propiedades, haga clic en **[!UICONTROL Crear]**. Se crea un formulario adaptable y aparece un cuadro de diálogo para abrir el formulario y editarlo.

   Una vez que haya terminado de especificar todas las propiedades, haga clic en **[!UICONTROL Crear]**. Se crea un formulario adaptable y aparece un cuadro de diálogo para abrir el formulario y editarlo.

1. Toque **[!UICONTROL Apertura]** para abrir el formulario recién creado en una pestaña nueva. El formulario se abre para su edición y muestra el contenido disponible en la plantilla. También muestra la barra lateral para personalizar el formulario recién creado según las necesidades.

   En función del tipo de formulario adaptable, los elementos de formulario presentes en la plantilla de formulario XFA asociada, el esquema XML o el esquema JSON se muestran en la variable **[!UICONTROL Objetos del modelo de datos]** de la pestaña **[!UICONTROL Navegador de contenido]** en la barra lateral. También puede arrastrar y soltar estos elementos para crear su formulario adaptable.

   Para obtener información sobre la interfaz de creación de formularios adaptables y los componentes disponibles, consulte [Introducción a la creación de formularios adaptables](introduction-forms-authoring.md).

   >[!NOTE]
   >
   >Permita que las ventanas emergentes del explorador abran el formulario recién creado en una nueva ficha.

## Creación de un formulario adaptable basado en un modelo de datos de formulario {#fdm}

[[!DNL Experience Manager Forms] integración de datos](data-integration.md) permite integrar varios orígenes de datos y unir sus entidades y servicios para crear un modelo de datos de formulario. Es una extensión del esquema JSON. Puede utilizar un modelo de datos de formulario para crear un formulario adaptable. Las entidades u objetos del modelo de datos configurados en un modelo de datos de formulario están disponibles como objetos del modelo de datos para la creación de formularios. Están enlazados a los respectivos orígenes de datos y se utilizan para rellenar previamente un formulario y escribir los datos enviados en los respectivos orígenes de datos. También puede llamar a servicios configurados en un modelo de datos de formulario mediante reglas de formulario adaptables.

Para utilizar un modelo de datos de formulario para crear un formulario adaptable:

1. En la pestaña modelo de formulario de la pantalla Agregar propiedades, seleccione **[!UICONTROL Modelo de datos de formulario]** en la lista desplegable **[!UICONTROL Seleccionar desde]**.

   ![crear-af-1-1](assets/create-af-1-1.png)

1. Pulse para expandir **[!UICONTROL Seleccionar modelo de datos de formulario]**. Se muestran todos los modelos de datos de formulario disponibles.

   Seleccione un modelo de datos de formulario.

   ![crear-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>También puede cambiar el modelo de datos de formulario para un formulario adaptable. Para ver los pasos detallados, consulte [Edición de las propiedades del modelo de formulario de un formulario adaptable](#edit-form-model).

## Crear un formulario adaptable basado en una plantilla de formulario XFA {#create-an-adaptive-form-based-on-an-xfa-form-template}

Puede reutilizar las plantillas de formulario XFA para crear formularios adaptables. Para cambiar el propósito, cargue y asocie una plantilla de formulario XFA con un formulario adaptable. Los elementos de la plantilla de formulario (formulario XFA) están disponibles para su uso en el buscador de contenido en el momento de la creación de formularios adaptables. Desde el buscador de contenido, puede arrastrar y soltar los elementos de plantilla de formulario en el formulario.

<!-- >>[!NOTE]
>
>[Upload the XFA Form Template](get-xdp-pdf-documents-aem.md) to AEM Forms before you start creating an adaptive form based on the form template.

Do the following to use an XFA form template as form model for your adaptive form:

1. On the **[!UICONTROL Add Properties]** page, open the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, from the drop-down list, select **[!UICONTROL Form Templates]**. All the form templates that are uploaded to the repository via AEM Forms UI are listed for selection. Select a template from the list.

   ![Associate XFA Form Template with an Adaptive Form](assets/form_model_xfa_associate.png)
**Figure:** *Selecting a form template*

   >[!NOTE]
   >
   >You can also change the form template for an adaptive form. For detailed steps, see [Edit Form Model properties of an adaptive form](#edit-form-model). -->

## Creación de un formulario adaptable basado en un esquema XML o JSON {#create-an-adaptive-form-based-on-xml-or-json-schema}

Los esquemas XML y JSON representan la estructura en la que el sistema back-end de su organización produce o consume los datos. Puede asociar un esquema a un formulario adaptable y utilizar sus elementos para agregar contenido dinámico al formulario adaptable. Los elementos del esquema están disponibles en la ficha Objeto del modelo de datos del navegador de contenido para la creación de formularios adaptables. Puede arrastrar y soltar los elementos de esquema para crear el formulario.

Consulte los siguientes documentos para comprender cómo diseñar esquemas XML o JSON para crear formularios adaptables.

* [Creación de formularios adaptables con esquema XML](adaptive-form-xml-schema-form-model.md)
* [Creación de formularios adaptables mediante el esquema JSON](adaptive-form-json-schema-form-model.md)

Haga lo siguiente para utilizar el esquema XML o JSON como modelo de formulario para un formulario adaptable:

1. En el **[!UICONTROL Agregar propiedades]** paso de la página de creación de formularios adaptables, toque en el **[!UICONTROL Modelo de formulario]** pestaña .
1. En la ficha Modelo de formulario, seleccione **[!UICONTROL Esquema]** de la variable **[!UICONTROL Seleccionar de]** campo desplegable.

1. Toque **[!UICONTROL Seleccionar esquema]** y realice una de las siguientes acciones:

   * **[!UICONTROL Cargar desde disco]** : seleccione esta opción y pulse Cargar definición de esquema para buscar y cargar un esquema XML o JSON desde el sistema de archivos. El archivo de esquema cargado reside con el formulario y no es accesible para otros formularios adaptables.
   * **[!UICONTROL Buscar en el repositorio]** - Seleccione esta opción para seleccionar de la lista de archivos de definición de esquema disponibles en el repositorio. Seleccione el archivo de esquema XML o JSON como modelo de formulario. El esquema seleccionado está asociado al formulario por referencia y es accesible para su uso en otros formularios adaptables.

   >[!CAUTION]
   >
   >Asegúrese de que el nombre de archivo del esquema JSON termina con **.schema.json**. Por ejemplo: mySchema.schema.json

   ![Selección del esquema XML o JSON](assets/upload-schema.png)
   **Figura:** *Selección del esquema XML o JSON*

1. (Solo para esquema XML) Después de seleccionar o cargar un esquema XML, especifique un elemento raíz del archivo XSD seleccionado para asignarlo al formulario adaptable.

   ![Selección del elemento raíz XSD](assets/xsd-root-element.png)
   **Figura:** *Selección del elemento raíz XSD*

>[!NOTE]
>
>También puede cambiar el esquema de un formulario adaptable. Para ver los pasos detallados, consulte [Edición de las propiedades del modelo de formulario de un formulario adaptable](#edit-form-model).

## Plantillas de formulario adaptables {#adaptive-form-templates}

Una plantilla proporciona una estructura básica y define el aspecto (diseños y estilos) de un formulario adaptable. Tiene componentes con formato previo que contienen determinadas propiedades y estructura de contenido. <!-- Out of the box, AEM Forms provides some adaptive form templates. To get the complete template package including advanced templates, you need to install the AEM Forms add-on package. For more information, see [Installing AEM Forms add-on package](installing-configuring-aem-forms-osgi.md).-->

Además, puede utilizar el editor de plantillas para crear sus propias plantillas. Para obtener más información sobre cómo trabajar con plantillas, consulte [Plantillas de formulario adaptables](template-editor.md).

>[!NOTE]
>
>Cuando se abre un formulario adaptable creado con la plantilla avanzada para su edición, aparece un mensaje de error. La plantilla avanzada tiene un componente Paso de firma y Adobe Sign está habilitado para él de forma predeterminada. Cree y seleccione un [Configuración de nube de Adobe Sign](adobe-sign-integration-adaptive-forms.md) y [configurar un firmante](working-with-adobe-sign.md#addsignerstoanadaptiveform) para resolver el error.

## Edición de las propiedades del modelo de formulario de un formulario adaptable {#edit-form-model}

Los formularios adaptables se crean sin un modelo de formulario (con la opción Ninguno del modelo de formulario) o utilizando un modelo de formulario como una plantilla de formulario, un esquema XML o JSON o un modelo de datos de formulario. Puede cambiar el modelo de formulario para un formulario adaptable de Ninguno a otro modelo de formulario. Para los formularios adaptables basados en un modelo de formulario, puede elegir otra plantilla de formulario, un esquema XML, un esquema JSON o un modelo de datos de formulario para el mismo modelo de formulario. Sin embargo, no se puede cambiar de un modelo de formulario a otro.

1. Seleccione el formulario adaptable y pulse el botón **Propiedades** icono.
1. Abra la pestaña **[!UICONTROL Modelo de formulario]** y haga una de las siguientes acciones.

   * Si el formulario adaptable no tiene un modelo de formulario, puede elegir otro modelo de formulario y, en consecuencia, seleccionar una plantilla de formulario, un esquema XML o JSON o un modelo de datos de formulario.
   * Si el formulario adaptable se basa en un modelo de formulario, puede elegir otra plantilla de formulario, un esquema XML o JSON o un modelo de datos de formulario para el mismo modelo de formulario.

1. Pulse **[!UICONTROL Guardar]** para guardar las propiedades.

## Guardar automáticamente un formulario adaptable {#auto-save-an-adaptive-form}

De forma predeterminada, el contenido de un formulario adaptable se guarda en una acción del usuario, como al pulsar el botón guardar. También puede configurar un formulario adaptable para que empiece a guardar automáticamente el contenido en función de un evento o intervalo de tiempo. La opción de guardado automático es útil en:

* Guardar automáticamente el contenido para usuarios anónimos y con sesión iniciada
* Guardado del contenido de un formulario sin la intervención mínima del usuario
* Empezar a guardar contenido de un formulario basado en un suceso de usuario
* Guardar el contenido de un formulario repetidamente después de un intervalo de tiempo especificado

### Habilitar el guardado automático para un formulario adaptable {#enable-auto-save-for-an-adaptive-form}

De forma predeterminada, la opción de guardado automático no está activada. Puede activar la opción de guardado automático desde la ficha Guardar automáticamente de un formulario adaptable. La ficha Guardar automáticamente también proporciona otras opciones de configuración. Realice los siguientes pasos para habilitar y configurar la opción de guardado automático para un formulario adaptable:

1. Para acceder a la sección de guardado automático de las propiedades, seleccione un componente y pulse ![nivel de campo](assets/field-level.png) > **[!UICONTROL Contenedor de formulario adaptable]** y, a continuación, toque ![cmppr](assets/cmppr.png).
1. En el **[!UICONTROL Guardar automáticamente]** sección, **[!UICONTROL Habilitar]** la opción guardar automáticamente.
1. En el **[!UICONTROL Evento de formulario adaptable]** especifique 1 o TRUE para comenzar a guardar automáticamente el formulario cuando se carga en el explorador. También se puede especificar una expresión condicional para un suceso, que cuando se activa y devuelve el valor &quot;True&quot;, comienza a guardar el contenido del formulario.
1. Especifique el Déclencheur. El guardado automático se activa según la configuración. Las opciones son las siguientes:

   * **[!UICONTROL Basado en el tiempo:]** Seleccione la opción para comenzar a guardar el contenido en función de un intervalo de tiempo específico.
   * **[!UICONTROL Basado en eventos:]** Seleccione la opción para comenzar a guardar el contenido en función de cuándo se activa un evento.

   Cuando selecciona un déclencheur, se activa el cuadro Configuración de estrategia . El cuadro Configuración de estrategia le permite:

   * Especifique un intervalo de tiempo si selecciona **[!UICONTROL Basado en el tiempo]** déclencheur.
   * Especifique un nombre de evento si selecciona **[!UICONTROL Basado en eventos]** déclencheur.

   <!-- You can also create and add your own custom strategy to the list. For details, see [Implement a custom strategy to autosave the forms](auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p). -->

1. (Solo guardado automático basado en el tiempo) Realice los siguientes pasos para configurar las opciones de guardado automático basado en el tiempo.

   1. En el **[!UICONTROL Guardar automáticamente en este intervalo]** especifique el intervalo de tiempo en segundos. El formulario se guarda repetidamente después de que transcurra el número de segundos especificado en el cuadro de intervalo.

1. (Solo guardado automático basado en eventos) Realice los siguientes pasos para configurar las opciones de guardado automático basado en eventos.

   1. En el **[!UICONTROL Guardar automáticamente después de este evento]** , especifique un [GuideBridge](https://helpx.adobe.com/es/aem-forms/6/javascript-api/GuideBridge.html) evento. El formulario se guarda cada vez que la expresión se evalúa como TRUE.

1. (Opcional) Para guardar automáticamente el contenido para usuarios anónimos, seleccione la opción **[!UICONTROL Habilitar el guardado automático para usuarios anónimos]** y haga clic en **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Para que la opción de guardado automático funcione para usuarios anónimos, asegúrese de configurar el servicio de configuración común de Forms para permitir que todos los usuarios puedan obtener una vista previa, verificar y firmar formularios.
   >
   >Para configurar el servicio, vaya a la configuración de Adobe Experience Manager Web Console en `https://'[server]:[port]'system/console/configMgr` y edite el **[!UICONTROL Servicio de configuración común de Forms]** para elegir **[!UICONTROL Todos los usuarios]** en la **[!UICONTROL Permitir]** y guarde la configuración.
