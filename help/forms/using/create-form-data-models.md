---
title: Crear modelo de datos de formulario
seo-title: Crear modelo de datos de formulario
description: Obtenga información sobre cómo crear modelos de datos de formulario con o sin fuentes de datos configuradas.
seo-description: Obtenga información sobre cómo crear modelos de datos de formulario con o sin fuentes de datos configuradas.
uuid: 5a94f733-0c08-41bb-983f-e7d34816d8fb
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: 7c392909-ff84-4411-b44f-16f99dffac54
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# Create form data model{#create-form-data-model}

![](do-not-localize/data-integeration.png)

La integración de datos de AEM Forms proporciona una interfaz de usuario intuitiva para crear y trabajar con modelos de datos de formulario. Un modelo de datos de formulario se basa en fuentes de datos para el intercambio de datos; sin embargo, puede crear un modelo de datos de formulario con o sin un origen de datos. Existen dos métodos para crear un modelo de datos a partir de datos, según si ha configurado fuentes de datos:

* **Uso de fuentes** de datos preconfiguradas: Si ha configurado orígenes de datos como se describe en [Configurar orígenes](../../forms/using/configure-data-sources.md)de datos, puede seleccionarlos al crear un modelo de datos de formulario. Proporciona todos los objetos, propiedades y servicios del modelo de datos de los orígenes de datos seleccionados disponibles para su uso en el modelo de datos de formulario.

* **Sin fuentes** de datos: Si no ha configurado orígenes de datos para el modelo de datos de formulario, puede crearlos sin orígenes de datos. Puede utilizar el modelo de datos de formulario para crear formularios adaptables y comunicaciones interactivas y probarlos con datos de ejemplo. Cuando los orígenes de datos están disponibles, puede enlazar el modelo de datos de formulario con los orígenes de datos, que se reflejarán automáticamente en los formularios adaptables y las comunicaciones interactivas asociados.

>[!NOTE]
>
>Debe ser miembro de los grupos **fdm-author** y **form-user** para poder crear y trabajar con el modelo de datos de formulario. Póngase en contacto con el administrador de AEM para convertirse en miembro de los grupos.

## Create form data model {#data-sources}

Asegúrese de haber configurado los orígenes de datos que desea utilizar en el modelo de datos de formulario como se describe en [Configurar orígenes](../../forms/using/configure-data-sources.md)de datos. Para crear un modelo de datos de formulario basado en orígenes de datos configurados, haga lo siguiente:

1. En la instancia de creación de AEM, vaya a **[!UICONTROL Formularios > Integraciones]** de datos.
1. Tap **[!UICONTROL Create > Form Data Model]**.
1. En el cuadro de diálogo Crear modelo de datos de formulario:

   * Especifique un nombre para el modelo de datos de formulario.
   * (**Opcional**) Especifique el título, la descripción y las etiquetas del modelo de datos de formulario.
   * (**Opcional y aplicable sólo si se configuran** las fuentes de datos) Toque el icono de marca de verificación situado junto al campo Configuración **[!UICONTROL de fuentes de]** datos y seleccione el nodo de configuración en el que residen los servicios en la nube para las fuentes de datos que desee utilizar. Restringe la lista de fuentes de datos disponibles para la selección en la página siguiente a las disponibles en el nodo de configuración seleccionado. Sin embargo, las fuentes de datos de perfil de usuario de AEM y la base de datos JDBC se muestran de forma predeterminada. Si no selecciona un nodo de configuración, se muestran las fuentes de datos de todos los nodos de configuración.
   Puntee **[!UICONTROL Siguiente]**.

1. (**Aplicable sólo si se configuran** las fuentes de datos) La pantalla **[!UICONTROL Seleccionar origen]** de datos muestra las fuentes de datos disponibles, si las hay. Seleccione los orígenes de datos que desee utilizar en el modelo de datos de formulario.
1. Toque **[!UICONTROL Crear]** y, en el cuadro de diálogo de confirmación, toque **[!UICONTROL Abrir]** para abrir el editor del modelo de datos de formulario.

Veamos los diferentes componentes de la interfaz de usuario del editor de modelos de datos de formulario.

![Un modelo de datos de formulario con tres orígenes de datos: un servicio RESTful, un perfil de usuario de AEM y un RDBMS](assets/fdm-ui.png)

**A. Fuentes** de datos Muestra las fuentes de datos en un modelo de datos de formulario. Expanda un origen de datos para ver los objetos y servicios del modelo de datos.

**B. Actualizar definiciones** de fuentes de datos Obtiene cualquier cambio en las definiciones de fuentes de datos de orígenes de datos configurados y los actualiza en la ficha Fuentes de datos del editor del modelo de datos de formulario.

**C. Área de contenido del modelo** en la que aparecen los objetos del modelo de datos agregados.

**D. Área de contenido de servicios** donde aparecen operaciones o servicios de fuentes de datos agregados.

**E. Herramientas de la barra de herramientas** para trabajar con el modelo de datos de formulario. La barra de herramientas muestra más opciones en función del objeto seleccionado en el modelo de datos de formulario.

**F. Agregar selección** Agrega objetos y servicios del modelo de datos seleccionado al modelo de datos de formulario.

Para obtener más información sobre el editor del modelo de datos de formulario y cómo puede trabajar con él para editar y configurar el modelo de datos de formulario, consulte [Trabajo con el modelo](../../forms/using/work-with-form-data-model.md)de datos de formulario.

## Actualizar fuentes de datos {#update}

Para agregar o actualizar orígenes de datos a un modelo de datos de formulario existente, haga lo siguiente.

1. Vaya a **[!UICONTROL Formularios > Integraciones]** de datos, seleccione el modelo de datos de formulario en el que desea agregar o actualizar orígenes de datos y toque **[!UICONTROL Propiedades]**.
1. En las propiedades del modelo de datos de formulario, vaya a la ficha **[!UICONTROL Actualizar origen]** .

   En la ficha Actualizar origen:

   * Puntee en el icono Examinar del campo Configuración **[!UICONTROL según el]** contexto y seleccione un nodo de configuración en el que resida la configuración de nube para el origen de datos que desee agregar. Si no selecciona ningún nodo, las configuraciones de nube que residen únicamente en el `global` nodo se muestran al tocar **[!UICONTROL Agregar fuentes]**.

   * Para agregar un nuevo origen de datos, toque **[!UICONTROL Agregar orígenes]** y seleccione los orígenes de datos que desee agregar al modelo de datos de formulario. Se muestran todos los orígenes de datos configurados en `global` y el nodo de configuración seleccionado, si los hay.

   * Para reemplazar una fuente de datos existente por otra fuente de datos del mismo tipo, toque el icono **[!UICONTROL Editar]** para la fuente de datos y seleccione una de la lista de fuentes de datos disponibles.
   * Para eliminar un origen de datos existente, toque el icono **[!UICONTROL Eliminar]** del origen de datos. El icono Eliminar se desactiva si se agrega un objeto de modelo de datos en el origen de datos en el modelo de datos de formulario.
   ![fdm-properties](assets/fdm-properties.png)

1. Toque **[!UICONTROL Guardar y cerrar]** para guardar las actualizaciones.

>[!NOTE]
>
>Una vez agregados los orígenes de datos nuevos o actualizados los orígenes de datos existentes en un modelo de datos de formulario, asegúrese de actualizar las referencias de enlace, según corresponda, en formularios adaptables y comunicaciones interactivas que utilicen el modelo de datos de formulario actualizado.

## Pasos siguientes {#next-steps}

Ahora tiene un modelo de datos de formulario con orígenes de datos agregados. A continuación, puede editar el modelo de datos de formulario para agregar y configurar objetos y servicios del modelo de datos, agregar asociaciones entre objetos del modelo de datos, editar propiedades, agregar objetos y propiedades del modelo de datos personalizados, generar datos de ejemplo, etc.

Para obtener más información, consulte [Trabajo con el modelo](../../forms/using/work-with-form-data-model.md)de datos de formulario.
