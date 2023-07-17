---
title: Crear un formulario adaptable
seo-title: Learn how to create a Core Components based Adaptive Form on AEM 6.5 Forms.
description: Obtenga información sobre cómo crear un formulario adaptable mediante  [!DNL Experience Manager Forms]. Los formularios adaptables son formularios HTML5 interactivos que agilizan la recopilación y el procesamiento de la información. Descubra más información sobre cómo crear un formulario adaptable basado en un modelo de datos de formulario y un esquema XML o JSON.
seo-description: Learn how to create an Adaptive Form using [!DNL Experience Manager Forms]. Adaptive Forms are responsive HTML5 forms that streamline information gathering and processing. Dig deeper on how to create an Adaptive Form based on a Form Data Model and XML or JSON schema.
Keywords: create adaptive form core component, create core component based adaptive form, creare adaptive form
products: SG_EXPERIENCEMANAGER/6.5/FORMS
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
source-git-commit: 85f423b98ff680d7ed7cdbdde65e2dec1cfe4c03
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 54%

---


# Crear componentes principales basados en formularios adaptables {#creating-an-adaptive-form-core-components}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | Este artículo |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=es) |

Los formularios adaptables le permiten crear formularios atractivos, interactivos, dinámicos y adaptables. AEM Forms proporciona una interfaz de usuario fácil de usar para las empresas que crea rápidamente Forms adaptable. La IU de ofrece una navegación rápida por las pestañas para seleccionar fácilmente plantillas, estilos, campos y opciones de envío preconfiguradas para crear un formulario adaptable.

Antes de empezar, obtenga información sobre el tipo de componentes de Forms disponibles para usted:

* [Componentes principales de formularios adaptables](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es): son componentes estandarizados de captura de datos. Estos componentes proporcionan funcionalidades de personalización, un tiempo de desarrollo reducido y costes de mantenimiento más bajos para sus experiencias de inscripción digital. Un desarrollador puede personalizar y aplicar estilo fácilmente a estos componentes. Adobe recomienda aprovechar estos componentes modernos y ampliables para desarrollar formularios adaptables.

* [Componentes de base de formularios adaptables](creating-adaptive-form.md): estos son componentes clásicos (antiguos) de captura de datos. Puede seguir utilizándolos para editar su Formulario adaptable basado en componentes de base existentes. Si está creando formularios, Adobe recomienda utilizar  [Componentes principales de Forms adaptable](creating-adaptive-form-core-components.md) para crear un Forms adaptable.

## Requisitos previos

Para crear un formulario adaptable, es necesario lo siguiente:

* **Habilitar los componentes principales de Forms adaptables para su entorno** AEM : Se requiere la versión 41 o posterior del proyecto de tipo de archivo para lo siguiente: [Habilitar los componentes principales para su entorno](/help/forms/using/installing-core-components.md). Al habilitar los componentes principales para su entorno, la variable **Forms adaptable (componente principal)** La plantilla y la temática Lienzo se añaden al entorno.

* **Una plantilla de formulario adaptable**: Una plantilla ofrece una estructura básica y define el aspecto (diseños y estilos) de un formulario adaptable. Tiene componentes con formato previo que contienen determinadas propiedades y estructura de contenido. También ofrece opciones para definir una temática y una acción de envío. La temática define la apariencia, y la acción de envío define la acción que debe realizarse al enviar un Formulario adaptable. Por ejemplo, enviar los datos recopilados a una fuente de datos. La plantilla denominada `blank` es compatible con OOTB:

   * El `blank` La plantilla de se incluye con cada entorno local y de AMS de AEM Forms nuevo.
   * Puede instalar el paquete de referencia mediante el Administrador de paquetes para agregar `blank` a su entorno local de AEM Forms y a su entorno de AMS.
   * También puede [crear una nueva plantilla de formularios adaptables (componentes principales)](template-editor.md) desde cero.

  >[!NOTE]
  >
  > Si no tiene la plantilla de **Formularios adaptables (componente principal)** en su entorno, [Habilite los componentes principales de formularios adaptables para su entorno](/help/forms/using/installing-core-components.md). Al habilitar los componentes principales para su entorno, la plantilla de **Formularios adaptables (componente principal)** se agrega al entorno.

* **Una temática de formulario adaptable**: Una temática contiene detalles de estilo para los componentes y paneles. Los estilos incluyen propiedades como colores de fondo, colores de estado, transparencia, alineación y tamaño. Al aplicar una temática, el estilo especificado se refleja en los componentes correspondientes.  El `Canvas` La temática se añade de forma predeterminada al habilitar los componentes principales para su entorno. También puede [descargar y personalizar las temáticas de referencia](create-or-customize-themes-for-adaptive-forms-core-components.md).

* **Permisos**: añada sus usuarios al grupo [!DNL forms-users]. Los miembros del grupo [!DNL forms-users] tienen permisos para crear un formulario adaptable. Para obtener una lista detallada de los grupos de usuarios específicos de los formularios, consulte [Grupos y permisos](forms-groups-privileges-tasks.md).

## Crear un formulario adaptable {#create-an-adaptive-form}

1. Inicie sesión en su [AEM instancia de autor](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=en#author-and-publish-installs).

1. Introduzca sus credenciales en la página de inicio de sesión de Experience Manager. Cuando haya iniciado sesión, en la esquina superior izquierda, pulse **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.

1. Tocar **[!UICONTROL Crear]**  > **[!UICONTROL Crear Forms adaptable]**.

1. Seleccione una plantilla de componentes principales de Forms adaptable y haga clic en **[!UICONTROL Siguiente]**.

1. El **[!UICONTROL Añadir propiedades]** aparece. Especifique los valores para los siguientes campos de propiedad. Los campos Título y Nombre son obligatorios:

   * **[!UICONTROL Título:]** Especifica el nombre para mostrar del formulario. El título le ayuda a identificar el formulario en la interfaz de usuario de [!DNL Experience Manager Forms].
   * **[!UICONTROL Nombre:]** Especifica el nombre del formulario. Se crea un nodo con el nombre especificado en el repositorio. A medida que empieza a escribir un título, el valor del campo de nombre se genera automáticamente. Puede cambiar el valor sugerido. El campo de nombre solo puede incluir caracteres alfanuméricos, guiones y guiones bajos.
   * **[!UICONTROL Descripción:]** especifica la información detallada sobre el formulario.
   * **[!UICONTROL Biblioteca de cliente de temas]:** Especifica la temática de un formulario adaptable. De forma predeterminada, la variable `adaptiveform.theme.canvas3` tema está seleccionado. También puede elegir una temática diferente de la **[!UICONTROL Biblioteca de cliente de temas]** menú desplegable.
   * **[!UICONTROL Contenedor de configuración:]**  Define una ubicación en la que se almacenan los archivos de configuración de Forms adaptable. Estos archivos de configuración contienen ajustes y propiedades relacionados con el comportamiento y el aspecto de Adaptive Forms.
   * **[!UICONTROL Etiquetas:]** Especifica etiquetas para identificar de forma exclusiva el formulario adaptable. Las etiquetas ayudan a buscar en el formulario. Para crear etiquetas, escriba nuevos nombres de etiqueta en el cuadro **[!UICONTROL Etiquetas]**.
1. Pulse **[!UICONTROL Crear]**. Se creará un formulario adaptable y aparecerá un cuadro de diálogo para abrir el formulario y editarlo.


1. Tocar **[!UICONTROL Editar]** para abrir el formulario recién creado en una pestaña nueva. El formulario se abrirá para editarlo y mostrará el contenido disponible en la plantilla. También muestra la barra lateral para personalizar el formulario recién creado.


## Utilice los componentes principales de Forms adaptable para crear el formulario

Después de abrir el formulario para editarlo, puede utilizar los componentes principales adaptables de Forms disponibles para agregar campos de formulario al formulario. Puede arrastrar y soltar o utilizar el signo + [insertar componente] para agregar estos componentes a un formulario. AEM Consulte la documentación de componentes principales para obtener más información sobre los componentes disponibles [Componentes principales de Forms adaptable](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en#components). También puede visitar [https://aemcomponents.dev/](https://aemcomponents.dev/) para ver los componentes principales disponibles en acción.

## Configurar la acción de envío para un formulario adaptable {#configure-submit-action-for-form}

Una acción de envío permite elegir el destino de los datos capturados mediante un formulario adaptable. Se activa una acción de envío cuando un usuario hace clic en el botón Enviar en un formulario adaptable. Los formularios adaptables incluyen algunas acciones de envío listas para usar. También puede ampliar las acciones de envío predeterminadas para crear su propia acción de envío personalizada. Para configurar una acción de envío para el formulario:

1. Abra el Explorador de contenido y seleccione **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en las propiedades del contenedor de guía ![Propiedades de guía](/help/forms/using/assets/configure-icon.svg) icono. Se abrirá el cuadro de diálogo Contenedor de formulario adaptable.

1. Haga clic en  **[!UICONTROL Envío]** pestaña.

   ![Haga clic en el icono Llave inglesa para abrir el cuadro de diálogo Contenedor de formulario adaptable y configurar una acción de envío](/help/forms/using/assets/adaptive-forms-submit-message.png)

1. Seleccione y configure un **[!UICONTROL Acción de envío]**, según sus necesidades. Para obtener información detallada sobre las acciones de envío, consulte [Acción de envío del formulario adaptable](/help/forms/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## Redirigir al usuario a una página o mostrar un mensaje de agradecimiento al enviar el formulario

Al enviar un formulario, puede redirigir al usuario a otra página web o a un mensaje. Para redirigir al usuario o configurar el mensaje de agradecimiento:

1. Abra el Explorador de contenido y seleccione **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en las propiedades del contenedor de guía ![Propiedades de guía](/help/forms/using/assets/configure-icon.svg) icono. Se abrirá el cuadro de diálogo Contenedor de formulario adaptable.
1. Abra la pestaña **[!UICONTROL Envío]**.

   ![Haga clic en el icono Llave inglesa para abrir el cuadro de diálogo Contenedor de formulario adaptable y configurar una página de redireccionamiento o un mensaje de agradecimiento](/help/forms/using/assets/adaptive-forms-submit-message.png)

   * Para configurar una URL de redireccionamiento, por ejemplo, en la opción Enviar, seleccione **[!UICONTROL Redirigir a URL]** y examine y seleccione una página de AEM Sites, o proporcione la URL de una página externa.

   * Para configurar un mensaje personalizado o de agradecimiento, para en la opción Enviar, seleccione **[!UICONTROL Mostrar mensaje]** y proporcione un mensaje en la **[!UICONTROL Contenido del mensaje]** cuadro. Es un cuadro de texto enriquecido, puede utilizar la opción de pantalla completa para ver todos los elementos de texto enriquecido disponibles.

## Configurar un esquema o un modelo de datos de formulario para un formulario adaptable {#configure-schema-or-data-model-for-form}

Puede utilizar el modelo de datos del formulario para conectar un formulario a una fuente de datos para enviar y recibir datos en función de las acciones del usuario. También puede conectar un formulario a un esquema JSON para recibir los datos enviados en un formato predefinido. En función del requisito, conecte el formulario a un esquema JSON o a un modelo de datos de formulario:

* [Crear un esquema JSON y cargarlo en su entorno](/help/forms/adaptive-form-json-schema-form-model.md)
* [Crear modelo de datos de formulario](/help/forms/create-form-data-models.md)

### Configurar un esquema JSON o un modelo de datos de formulario para el formulario

Para configurar un esquema JSON o un modelo de datos de formulario para su formulario:

1. Abra el Explorador de contenido y seleccione **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en las propiedades del contenedor de guía ![Propiedades de guía](/help/forms/using/assets/configure-icon.svg) icono. Se abrirá el cuadro de diálogo Contenedor de formulario adaptable.
1. Abra el **[!UICONTROL Modelo de datos]** pestaña.

   ![Haga clic en el icono Llave inglesa para abrir el cuadro de diálogo Contenedor de formulario adaptable y configurar un esquema JSON o un modelo de datos de formulario](/help/forms/using/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. Seleccione y configure un esquema JSON o un modelo de datos de formulario según sus necesidades:

   * Al seleccionar la variable **[!UICONTROL Modelo de formulario]**, utilice la opción **[!UICONTROL Seleccionar modelo de datos de formulario]** para seleccionar un modelo de datos de formulario preconfigurado.
   * Al seleccionar la opción **[!UICONTROL Esquema]**, utilice la opción **[!UICONTROL Esquema]** para seleccionar un esquema JSON para el formulario.

1. Haga clic en **[!UICONTROL Listo]**.

## Configurar un servicio de rellenado previo  {#configure-prefill-service-for-form}

Puede utilizar el servicio de cumplimentación previa para rellenar automáticamente los campos de un formulario adaptable utilizando los datos existentes. Cuando un usuario abre un formulario, los valores de esos campos ya han sido rellenados. Puede hacer lo siguiente:

* [Crear un servicio de rellenado previo personalizado](/help/forms/prepopulate-adaptive-form-fields.md)
* [Servicio de rellenado previo de modelo de datos de formulario](#fdm-prefill-service)

### Utilice el servicio de prerrellenado del modelo de datos de formulario para rellenar previamente los campos de un formulario adaptable {#fdm-prefill-service}

Puede utilizar el servicio de prerrellenado del modelo de datos de formulario para rellenar previamente los campos de un formulario adaptable mediante un modelo de datos de formulario o un servicio de prerrellenado personalizado. El servicio de rellenado previo del modelo de datos de formulario utiliza el [Obtener servicio del modelo de datos de formulario configurado](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) para recuperar datos. Para utilizar el servicio de rellenado previo del modelo de datos de formulario de un formulario adaptable, haga lo siguiente:

1. Abra el Explorador de contenido y seleccione **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en las propiedades del contenedor de guía ![Propiedades de guía](/help/forms/using/assets/configure-icon.svg) icono. Se abrirá el cuadro de diálogo Contenedor de formulario adaptable.
1. Haga clic en el icono de las ![Propiedades del contenedor del formulario adaptable](/help/forms/using/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable para configurar modelos de datos.
   ![Haga clic en el icono Llave inglesa para abrir el cuadro de diálogo Contenedor de formulario adaptable y configurar una página de redireccionamiento o un mensaje de agradecimiento](/help/forms/using/assets/adaptive-forms-container-prefill-service.png)
1. Seleccionar modelo de datos de formulario. Abra la pestaña **[!UICONTROL Básico]**. En el servicio de relleno previo, seleccione **[!UICONTROL Servicio de prerrellenado del modelo de datos de formulario]**.
1. Haga clic en **[!UICONTROL Listo]**. El formulario adaptable ahora está configurado para utilizar el prerrellenado del modelo de datos de formulario. Ahora puede usar la variable [editor de reglas](rule-editor.md) para crear reglas para rellenar previamente los campos del formulario.

## Edición de las propiedades del modelo de formulario de un formulario adaptable {#edit-form-model}

1. Seleccione el formulario adaptable y pulse ![Información de página](/help/forms/using/assets/configure-icon.svg) > **[!UICONTROL Abrir propiedades]**. Se abre la página Propiedades del formulario.

1. Vaya a la pestaña **[!UICONTROL Modelo de formulario]** y elija un modelo de formulario. Si el formulario adaptable no cuenta con un modelo de formulario, tiene la posibilidad de elegir un esquema JSON o un modelo de datos de formulario. Por otro lado, si el formulario adaptable ya se basa en un modelo de formulario, tiene la opción de cambiar a otro modelo de formulario del mismo tipo. Por ejemplo, si el formulario utiliza un esquema JSON, puede cambiar fácilmente a otro esquema JSON y, del mismo modo, si el formulario utiliza un modelo de datos de formulario, puede cambiar a otro modelo de datos de formulario.

1. Pulse **[!UICONTROL Guardar]** para guardar las propiedades.

## Siguientes pasos

* [Utilice el editor de reglas para agregar un comportamiento dinámico al formulario](rule-editor.md)
* [Crear o personalizar temáticas para componentes principales basados en Forms adaptable](create-or-customize-themes-for-adaptive-forms-core-components.md)
* Crear una plantilla para componentes principales basados en Forms adaptable

## Consulte también

* [Crear un formulario adaptable basado en componentes principales](/help/forms/using/create-an-adaptive-form-core-components.md)
* [Crear o agregar un formulario adaptable a una página de AEM Sites o a un fragmento de experiencia](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)

