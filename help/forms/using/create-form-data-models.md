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
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---


# Crear modelo de datos de formulario{#create-form-data-model}

![](do-not-localize/data-integeration.png)

La integración de datos de AEM Forms proporciona una interfaz de usuario intuitiva para crear y trabajar con modelos de datos de formulario. Un modelo de datos de formulario depende de las fuentes de datos para el intercambio de datos; sin embargo, puede crear un modelo de datos de formulario con o sin un origen de datos. Existen dos métodos para crear un modelo de datos a partir de datos, según si ha configurado fuentes de datos:

* **Uso de fuentes** de datos preconfiguradas: Si ha configurado orígenes de datos como se describe en  [Configurar orígenes](../../forms/using/configure-data-sources.md) de datos, puede seleccionarlos al crear un modelo de datos de formulario. Proporciona todos los objetos, propiedades y servicios del modelo de datos de los orígenes de datos seleccionados disponibles para su uso en el modelo de datos de formulario.

* **Sin fuentes** de datos: Si no ha configurado orígenes de datos para el modelo de datos de formulario, puede crearlos sin orígenes de datos. Puede utilizar el modelo de datos de formulario para crear formularios adaptables y comunicaciones interactivas y probarlos con datos de ejemplo. Cuando los orígenes de datos están disponibles, puede enlazar el modelo de datos de formulario con los orígenes de datos, que se reflejarán automáticamente en los formularios adaptables y las comunicaciones interactivas asociados.

>[!NOTE]
>
>Debe ser miembro de los grupos **fdm-author** y **form-user** para poder crear y trabajar con el modelo de datos de formulario. Póngase en contacto con el administrador de AEM para convertirse en miembro de los grupos.

## Crear modelo de datos de formulario {#data-sources}

Asegúrese de haber configurado los orígenes de datos que desea utilizar en el modelo de datos de formulario como se describe en [Configurar orígenes de datos](../../forms/using/configure-data-sources.md). Para crear un modelo de datos de formulario basado en orígenes de datos configurados, haga lo siguiente:

1. En AEM instancia de autor, vaya a **[!UICONTROL Forms > Integraciones de datos]**.
1. Puntee **[!UICONTROL Crear > Modelo de datos de formulario]**.
1. En el cuadro de diálogo Crear modelo de datos de formulario:

   * Especifique un nombre para el modelo de datos de formulario.
   * (**Opcional**) Especifique el título, la descripción y las etiquetas del modelo de datos de formulario.
   * (**Opcional y aplicable solamente si las fuentes de datos están configuradas**) Toque el icono de visto situado junto al campo **[!UICONTROL Configuración de fuente de datos]** y seleccione el nodo de configuración donde residen los servicios en la nube para las fuentes de datos que desee utilizar. Restringe la lista de fuentes de datos disponibles para selección en la página siguiente a las disponibles en el nodo de configuración seleccionado. Sin embargo, todas las bases de datos JDBC y AEM fuentes de datos de perfil de usuarios se muestran de forma predeterminada. Si no selecciona un nodo de configuración, se muestran las fuentes de datos de todos los nodos de configuración.

   Toque **[!UICONTROL Siguiente]**.

1. (**Aplicable sólo si las fuentes de datos están configuradas**) La pantalla **[!UICONTROL Seleccionar origen de datos]** lista las fuentes de datos disponibles, si las hay. Seleccione los orígenes de datos que desee utilizar en el modelo de datos de formulario.
1. Toque **[!UICONTROL Crear]** y, en el cuadro de diálogo de confirmación, toque **[!UICONTROL Abrir]** para abrir el editor del modelo de datos de formulario.

Veamos los diferentes componentes de la interfaz de usuario del editor de modelos de datos de formulario.

![Un modelo de datos de formulario con tres orígenes de datos: un servicio RESTful, AEM perfil de usuario y un RDBMS](assets/fdm-ui.png)

**A. Fuentes** de datosEnumera los orígenes de datos de un modelo de datos de formulario. Expanda un origen de datos para vista de los objetos y servicios del modelo de datos.

**B. Actualizar** definiciones de fuentes de datosObtiene cualquier cambio en las definiciones de fuentes de datos de fuentes de datos configuradas y las actualiza en la ficha Fuentes de datos del editor del modelo de datos de formulario.

**C. Área** ModelContent donde aparecen los objetos del modelo de datos agregados.

**D.** ServiciosÁrea de contenido en la que aparecen operaciones o servicios de fuentes de datos agregados.

**E.** Barra de herramientasHerramientas para trabajar con el modelo de datos de formulario. La barra de herramientas muestra más opciones en función del objeto seleccionado en el modelo de datos de formulario.

**F. Añadir** seleccionadosAgrega objetos y servicios del modelo de datos seleccionado al modelo de datos de formulario.

Para obtener más información sobre el editor del modelo de datos de formulario y cómo puede trabajar con él para editar y configurar el modelo de datos de formulario, consulte [Trabajo con el modelo de datos de formulario](../../forms/using/work-with-form-data-model.md).

## Actualizar fuentes de datos {#update}

Para agregar o actualizar orígenes de datos a un modelo de datos de formulario existente, haga lo siguiente.

1. Vaya a **[!UICONTROL Forms > Integraciones de datos]**, seleccione el modelo de datos de formulario en el que desee agregar o actualizar orígenes de datos y toque **[!UICONTROL Propiedades]**.
1. En las propiedades del modelo de datos de formulario, vaya a la ficha **[!UICONTROL Actualizar origen]**.

   En la ficha Actualizar origen:

   * Toque el icono Examinar en el campo **[!UICONTROL Configuración según el contexto]** y seleccione un nodo de configuración en el que resida la configuración de nube para el origen de datos que desea agregar. Si no selecciona ningún nodo, las configuraciones de nube que residen únicamente en el nodo `global` se muestran al tocar **[!UICONTROL Añadir fuentes]**.

   * Para agregar un nuevo origen de datos, toque **[!UICONTROL Añadir orígenes]** y seleccione los orígenes de datos que desee agregar al modelo de datos de formulario. Se muestran todas las fuentes de datos configuradas en `global` y el nodo de configuración seleccionado, si existe.

   * Para reemplazar una fuente de datos existente por otra fuente de datos del mismo tipo, toque el icono **[!UICONTROL Editar]** para la fuente de datos y seleccione entre la lista de fuentes de datos disponibles.
   * Para eliminar un origen de datos existente, toque el icono **[!UICONTROL Eliminar]** del origen de datos. El icono Eliminar se desactiva si se agrega un objeto de modelo de datos en el origen de datos en el modelo de datos de formulario.

   ![fdm-properties](assets/fdm-properties.png)

1. Toque **[!UICONTROL Guardar y cerrar]** para guardar las actualizaciones.

>[!NOTE]
>
>Una vez agregados los orígenes de datos nuevos o actualizados los orígenes de datos existentes en un modelo de datos de formulario, asegúrese de actualizar las referencias de enlace, según corresponda, en formularios adaptables y comunicaciones interactivas que utilicen el modelo de datos de formulario actualizado.

## Próximos pasos {#next-steps}

Ahora tiene un modelo de datos de formulario con orígenes de datos agregados. A continuación, puede editar el modelo de datos de formulario para agregar y configurar objetos y servicios del modelo de datos, agregar asociaciones entre objetos del modelo de datos, editar propiedades, agregar objetos y propiedades del modelo de datos personalizados, generar datos de ejemplo, etc.

Para obtener más información, consulte [Trabajo con el modelo de datos de formulario](../../forms/using/work-with-form-data-model.md).
