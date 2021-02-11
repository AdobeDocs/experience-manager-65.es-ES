---
title: Cómo crear un formulario adaptable
description: 'Obtenga información sobre cómo crear un formulario adaptable con [!DNL Experience Manager Forms]. Los formularios adaptables son formularios HTML5 interactivos que facilitan la recopilación y el procesamiento de información. Descubra cómo crear un formulario adaptable basado en un modelo de datos de formulario, una plantilla de formulario XFA y un esquema XML o JSON. '
feature: Adaptive Forms
role: Business Practitioner, Developers
level: Beginner
translation-type: tm+mt
source-git-commit: 52fedc234b3edf581393bb42325902d2da3ab46e
workflow-type: tm+mt
source-wordcount: '1856'
ht-degree: 0%

---


# Creación de un formulario adaptable {#creating-an-adaptive-form}

## <strong>Creación de un formulario adaptable</strong> {#strong-create-an-adaptive-form-strong}

Siga estos pasos para crear un formulario adaptable.

1. Acceder a [!DNL Experience Manager Forms] instancia de autor en `https://'[server]:[port]'/<custom-context-if-any>.`

1. Introduzca sus credenciales en la página de inicio de sesión del Experience Manager.

   Después de iniciar sesión, en la esquina superior izquierda, toque **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms y Documentos]**.

   >[!NOTE]
   >
   >Para una instalación predeterminada, el inicio de sesión es `admin` y la contraseña es `admin`.

1. Toque **[!UICONTROL Crear]** y seleccione **[!UICONTROL Formulario adaptable]**.
1. Aparece una opción para seleccionar una plantilla. Para obtener más información acerca de las plantillas, consulte [Plantillas de formulario adaptables](creating-adaptive-form.md#p-adaptive-form-templates-p). Toque una plantilla para seleccionarla y toque Siguiente.
1. Aparece una opción para &#39;Añadir propiedades&#39;. Especifique los valores de los siguientes campos de propiedad. Los campos Título y Nombre son obligatorios:

   * **[!UICONTROL Título:]** especifica el nombre para mostrar del formulario. El título le ayuda a identificar el formulario en la interfaz de usuario [!DNL Experience Manager Forms].
   * **[!UICONTROL Nombre:]** especifica el nombre del formulario. En el repositorio se crea un nodo con el nombre especificado. Al escribir un título con inicio, se genera automáticamente el valor del campo de nombre. Puede cambiar el valor sugerido. El campo de nombre solo puede incluir caracteres alfanuméricos, guiones y guiones bajos. Todas las entradas no válidas se reemplazan con un guión.
   * **[!UICONTROL Descripción:]** especifica la información detallada sobre el formulario.
   * **[!UICONTROL Etiquetas:]** especifica etiquetas para identificar exclusivamente el formulario adaptable. Las etiquetas ayudan a buscar en el formulario. Para crear etiquetas, escriba nuevos nombres de etiquetas en el cuadro **[!UICONTROL Etiquetas]**.

1. Puede crear un formulario adaptable basado en uno de los siguientes modelos de formulario:

   * [Modelo de datos de formulario](#fdm)
   * [Plantilla de formulario XFA](#create-an-adaptive-form-based-on-an-xfa-form-template)
   * [ESQUEMA XML o JSON](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * Ninguno o sin ningún modelo de formulario

   Puede configurarlas desde la ficha **[!UICONTROL Modelo de formulario]** en la página **[!UICONTROL Añadir propiedades]**. De forma predeterminada, el modelo de formulario seleccionado es **[!UICONTROL Ninguno]**.

1. Toque **[!UICONTROL Crear]**. Se crea un formulario adaptable y aparece un cuadro de diálogo para abrir el formulario y editarlo.

   Una vez que haya terminado de especificar todas las propiedades, haga clic en **[!UICONTROL Crear]**. Se crea un formulario adaptable y aparece un cuadro de diálogo para abrir el formulario y editarlo.

   Una vez que haya terminado de especificar todas las propiedades, haga clic en **[!UICONTROL Crear]**. Se crea un formulario adaptable y aparece un cuadro de diálogo para abrir el formulario y editarlo.

1. Toque **[!UICONTROL Abrir]** para abrir el formulario recién creado en una nueva ficha. El formulario se abre para su edición y muestra el contenido disponible en la plantilla. También muestra la barra lateral para personalizar el formulario recién creado según las necesidades.

   En función del tipo de formulario adaptable, los elementos de formulario presentes en la plantilla de formulario XFA, el esquema XML o el esquema JSON asociados se muestran en la ficha **[!UICONTROL Objetos del modelo de datos]** del **[!UICONTROL Explorador de contenido]** de la barra lateral. También puede arrastrar y soltar estos elementos para crear el formulario adaptable.

   Para obtener información sobre la interfaz de creación de formularios adaptables y los componentes disponibles, consulte [Introducción a la creación de formularios adaptables](introduction-forms-authoring.md).

   >[!NOTE]
   >
   >Permite que las ventanas emergentes del navegador abran el formulario recién creado en una nueva ficha.

## Crear un formulario adaptable basado en un modelo de datos de formulario {#fdm}

[[!DNL Experience Manager Forms] la ](data-integration.md) integración de datos permite integrar varios orígenes de datos y unir sus entidades y servicios para crear un modelo de datos de formulario. Es una extensión del esquema JSON. Puede utilizar un modelo de datos de formulario para crear un formulario adaptable. Las entidades u objetos del modelo de datos configurados en un modelo de datos de formulario están disponibles como objetos del modelo de datos para la creación de formularios. Se enlazan a las fuentes de datos respectivas y se utilizan para rellenar previamente un formulario y escribir los datos enviados de vuelta a las fuentes de datos respectivas. También puede llamar a servicios configurados en un modelo de datos de formulario mediante reglas de formulario adaptables.

Para utilizar un modelo de datos de formulario para crear un formulario adaptable:

1. En la ficha Modelo de formulario de la pantalla Añadir propiedades, seleccione **[!UICONTROL Modelo de datos de formulario]** en la lista desplegable **[!UICONTROL Seleccionar desde]**.

   ![create-af-1-1](assets/create-af-1-1.png)

1. Toque para expandir **[!UICONTROL Seleccionar modelo de datos de formulario]**. Se muestran todos los modelos de datos de formulario disponibles.

   Seleccione un modelo de datos de.

   ![create-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>También puede cambiar el modelo de datos de formulario para un formulario adaptable. Para ver los pasos detallados, consulte [Editar propiedades del modelo de formulario de un formulario adaptable](#edit-form-model).

## Crear un formulario adaptable basado en una plantilla de formulario XFA {#create-an-adaptive-form-based-on-an-xfa-form-template}

Puede reutilizar las plantillas de formulario XFA para crear formularios adaptables. Para reutilizar, cargue y asocie una plantilla de formulario XFA con un formulario adaptable. Los elementos de la plantilla de formulario (formulario XFA) están disponibles para su uso en el buscador de contenido en el momento de la creación de formularios adaptables. Desde Content Finder, puede arrastrar y soltar los elementos de la plantilla de formulario en el formulario.

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

## Crear un formulario adaptable basado en el esquema XML o JSON {#create-an-adaptive-form-based-on-xml-or-json-schema}

Los esquemas XML y JSON representan la estructura en la que el sistema back-end de la organización produce o consume los datos. Puede asociar un esquema a un formulario adaptable y utilizar sus elementos para agregar contenido dinámico al formulario adaptable. Los elementos del esquema están disponibles en la ficha Objeto del modelo de datos del navegador de contenido para la creación de formularios adaptables. Puede arrastrar y soltar los elementos de esquema para crear el formulario.

Consulte los siguientes documentos para comprender cómo diseñar el esquema XML o JSON para la creación de formularios adaptables.

* [Creación de formularios adaptables mediante esquema XML](adaptive-form-xml-schema-form-model.md)
* [Creación de formularios adaptables con esquema JSON](adaptive-form-json-schema-form-model.md)

Para utilizar el esquema XML o JSON como modelo de formulario para un formulario adaptable, haga lo siguiente:

1. En el paso **[!UICONTROL Añadir propiedades]** de la página de creación de formularios adaptables, toque la ficha **[!UICONTROL Modelo de formulario]**.
1. En la ficha Modelo de formulario, seleccione **[!UICONTROL Esquema]** en el campo desplegable **[!UICONTROL Seleccionar de]**.

1. Toque **[!UICONTROL Seleccionar Esquema]** y realice una de las siguientes acciones:

   * **[!UICONTROL Cargar desde el disco]** : seleccione esta opción y toque Cargar definición de Esquema para buscar y cargar un esquema XML o un esquema JSON desde el sistema de archivos. El archivo de esquema cargado reside en el formulario y no es accesible para otros formularios adaptables.
   * **[!UICONTROL Buscar en el repositorio]** : seleccione esta opción para seleccionar entre la lista de archivos de definición de esquema disponibles en el repositorio. Seleccione el archivo de esquema XML o JSON como modelo de formulario. El esquema seleccionado está asociado al formulario por referencia y es accesible para su uso en otros formularios adaptables.

   >[!CAUTION]
   >
   >Asegúrese de que el nombre de archivo del esquema JSON termine con **.esquema.json**. Por ejemplo: mySchema.esquema.json

   ![Selección de esquema XML o JSON](assets/upload-schema.png)
   **Figura:** *Selección del esquema XML o JSON*

1. (Solo para esquema XML) Después de seleccionar o cargar un Esquema XML, especifique un elemento raíz del archivo XSD seleccionado para asignarlo al formulario adaptable.

   ![Selección del elemento raíz XSD](assets/xsd-root-element.png)
   **Figura:** *Selección del elemento raíz XSD*

>[!NOTE]
>
>También puede cambiar el esquema de un formulario adaptable. Para ver los pasos detallados, consulte [Editar propiedades del modelo de formulario de un formulario adaptable](#edit-form-model).

## Plantillas de formulario adaptables {#adaptive-form-templates}

Una plantilla proporciona una estructura básica y define el aspecto (diseños y estilos) de un formulario adaptable. Tiene componentes con formato previo que contienen determinadas propiedades y estructura de contenido. <!-- Out of the box, AEM Forms provides some adaptive form templates. To get the complete template package including advanced templates, you need to install the AEM Forms add-on package. For more information, see [Installing AEM Forms add-on package](installing-configuring-aem-forms-osgi.md).-->

Además, puede utilizar el editor de plantillas para crear sus propias plantillas. Para obtener más información sobre cómo trabajar con plantillas, consulte [Plantillas de formulario adaptables](template-editor.md).

>[!NOTE]
>
>Cuando se abre un formulario adaptable creado con la plantilla avanzada para edición, aparece un mensaje de error. La plantilla avanzada tiene un componente Paso de firma y Adobe Sign está habilitado para ella de forma predeterminada. Cree y seleccione una [configuración de nube de Adobe Sign](adobe-sign-integration-adaptive-forms.md) y [configure un firmante](working-with-adobe-sign.md#addsignerstoanadaptiveform) para resolver el error.

## Editar propiedades del modelo de formulario de un formulario adaptable {#edit-form-model}

Los formularios adaptables se crean sin un modelo de formulario (con la opción Ninguno para el modelo de formulario) o con un modelo de formulario como una plantilla de formulario, un esquema XML o un esquema JSON o un modelo de datos de formulario. Puede cambiar el modelo de formulario para un formulario adaptable de Ninguno a otro modelo de formulario. Para los formularios adaptables basados en un modelo de formulario, puede elegir otra plantilla de formulario, esquema XML, esquema JSON o modelo de datos de formulario para el mismo modelo de formulario. Sin embargo, no puede cambiar de un modelo de formulario a otro.

1. Seleccione el formulario adaptable y toque el icono **Propiedades**.
1. Abra la ficha **[!UICONTROL Modelo de formulario]** y realice una de las acciones siguientes.

   * Si el formulario adaptable no tiene un modelo de formulario, puede elegir otro modelo de formulario y, en consecuencia, seleccionar una plantilla de formulario, un esquema XML o JSON o un modelo de datos de formulario.
   * Si el formulario adaptable se basa en un modelo de formulario, puede elegir otra plantilla de formulario, esquema XML o JSON, o modelo de datos de formulario para el mismo modelo de formulario.

1. Toque **[!UICONTROL Guardar]** para guardar las propiedades.

## Guardar automáticamente un formulario adaptable {#auto-save-an-adaptive-form}

De forma predeterminada, el contenido de un formulario adaptable se guarda en una acción del usuario, como al pulsar el botón Guardar. También puede configurar un formulario adaptable para que guarde automáticamente el contenido en inicio según un evento o un intervalo de tiempo. La opción de guardado automático es útil en:

* Guardar automáticamente el contenido para usuarios anónimos e iniciados en sesión
* Guardado del contenido de un formulario sin la intervención mínima del usuario
* Inicio para guardar el contenido de un formulario basado en un evento de usuario
* Guardar el contenido de un formulario repetidamente después de un intervalo de tiempo especificado

### Habilitar guardado automático para un formulario adaptable {#enable-auto-save-for-an-adaptive-form}

De forma predeterminada, la opción de guardado automático no está activada. Puede activar la opción de guardado automático desde la ficha Guardar automáticamente de un formulario adaptable. La ficha Guardado automático también proporciona otras opciones de configuración. Realice los siguientes pasos para habilitar y configurar la opción de guardado automático para un formulario adaptable:

1. Para acceder a la sección de guardado automático de las propiedades, seleccione un componente, toque ![campo-nivel](assets/field-level.png) > **[!UICONTROL Contenedor de formulario adaptable]** y luego toque ![cmppr](assets/cmppr.png).
1. En la sección **[!UICONTROL Guardado automático]**, **[!UICONTROL Habilite]** la opción de guardado automático.
1. En el cuadro **[!UICONTROL Evento de formulario adaptable]**, especifique 1 o TRUE para guardar automáticamente el formulario cuando se cargue en el explorador en inicio para guardarlo. También puede especificar una expresión condicional para un evento, que cuando se activa y devuelve verdadero, inicios que guardan el contenido del formulario.
1. Especifique el Déclencheur. El guardado automático se activa según la configuración. Sus opciones son:

   * **[!UICONTROL Basado en el tiempo:]** seleccione la opción para guardar en inicio el contenido en función de un intervalo de tiempo específico.
   * **[!UICONTROL Basado en evento:]** seleccione la opción para guardar en inicio el contenido en función de cuándo se activa un evento.

   Al seleccionar un déclencheur, se activa el cuadro de configuración de estrategia. El cuadro Configuración de estrategia permite:

   * Especifique un intervalo de tiempo si selecciona el déclencheur **[!UICONTROL basado en tiempo]**.
   * Especifique un nombre de evento si selecciona el déclencheur **[!UICONTROL basado en Evento]**.

   <!-- You can also create and add your own custom strategy to the list. For details, see [Implement a custom strategy to autosave the forms](auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p). -->

1. (Solo guardado automático basado en el tiempo) Realice los siguientes pasos para configurar las opciones de guardado automático basado en el tiempo.

   1. En el cuadro **[!UICONTROL Guardar automáticamente en este intervalo]**, especifique el intervalo de tiempo en segundos. El formulario se guarda repetidamente después de que transcurra el número de segundos especificado en el cuadro de intervalo.

1. (Solo guardado automático basado en Eventos) Realice los siguientes pasos para configurar las opciones de guardado automático basado en Eventos.

   1. En el cuadro **[!UICONTROL Guardar automáticamente después de este evento]**, especifique un evento [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html). El formulario se guarda cada vez que la expresión se evalúa como VERDADERA.

1. (Opcional) Para guardar automáticamente el contenido para usuarios anónimos, seleccione la opción **[!UICONTROL Habilitar guardado automático para usuarios anónimos]** y haga clic en **[!UICONTROL Aceptar]**.

   >[!NOTE]
   >
   >Para que la opción de guardado automático funcione para usuarios anónimos, asegúrese de configurar el servicio de configuración común de Forms para permitir que todos los usuarios realicen previsualizaciones, verifiquen y firmen formularios.
   >
   >Para configurar el servicio, vaya a la configuración de Adobe Experience Manager Web Console en `https://'[server]:[port]'system/console/configMgr` y edite el **[!UICONTROL Servicio de configuración común de Forms]** para elegir la opción **[!UICONTROL Todos los usuarios]** en el campo **[!UICONTROL Permitir]** y guarde la configuración.