---
title: Crear modelo de datos de formulario
seo-title: Crear modelo de datos de formulario
description: Aprenda a crear modelos de datos de formulario con o sin fuentes de datos configuradas.
seo-description: Aprenda a crear modelos de datos de formulario con o sin fuentes de datos configuradas.
uuid: 5a94f733-0c08-41bb-983f-e7d34816d8fb
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: 7c392909-ff84-4411-b44f-16f99dffac54
docset: aem65
feature: Form Data Model
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---


# Crear modelo de datos de formulario{#create-form-data-model}

![](do-not-localize/data-integeration.png)

La integración de datos de AEM Forms proporciona una interfaz de usuario intuitiva para crear y trabajar con modelos de datos de formulario. Un modelo de datos de formulario se basa en fuentes de datos para el intercambio de datos; sin embargo, puede crear un modelo de datos de formulario con o sin un origen de datos. Existen dos métodos para crear un desde el modelo de datos en función de si ha configurado fuentes de datos:

* **Uso de fuentes** de datos preconfiguradas: Si ha configurado los orígenes de datos como se describe en  [Configuración de orígenes de datos](../../forms/using/configure-data-sources.md), puede seleccionarlos al crear un modelo de datos de formulario. Incorpora todos los objetos, propiedades y servicios del modelo de datos de los orígenes de datos seleccionados que se pueden utilizar en el modelo de datos de formulario.

* **Sin fuentes** de datos: Si no ha configurado orígenes de datos para el modelo de datos de formulario, puede crearlos sin orígenes de datos. Puede utilizar el modelo de datos de formulario para crear formularios adaptables y comunicaciones interactivas y probarlos con datos de ejemplo. Cuando hay orígenes de datos disponibles, se puede enlazar el modelo de datos de formulario con orígenes de datos, que se reflejarán automáticamente en los formularios adaptables y las comunicaciones interactivas asociados.

>[!NOTE]
>
>Debe ser miembro de los grupos **fdm-author** y **forms-user** para poder crear y trabajar con el modelo de datos de formulario. Póngase en contacto con el administrador de AEM para convertirse en miembro de los grupos.

## Crear modelo de datos de formulario {#data-sources}

Asegúrese de haber configurado los orígenes de datos que desea utilizar en el modelo de datos de formulario como se describe en [Configurar orígenes de datos](../../forms/using/configure-data-sources.md). Para crear un modelo de datos de formulario basado en orígenes de datos configurados:

1. En AEM instancia de autor, vaya a **[!UICONTROL Forms > Integraciones de datos]**.
1. Pulse **[!UICONTROL Crear > Modelo de datos de formulario]**.
1. En el cuadro de diálogo Crear modelo de datos de formulario:

   * Especifique un nombre para el modelo de datos del formulario.
   * (**Opcional**) Especifique el título, la descripción y las etiquetas del modelo de datos del formulario.
   * (**Opcional y aplicable solo si las fuentes de datos están configuradas**) Pulse el icono de visto situado junto al campo **[!UICONTROL Configuración de fuente de datos]** y seleccione el nodo de configuración donde residen los servicios en la nube para las fuentes de datos que desea utilizar. Restringe la lista de fuentes de datos disponibles para su selección en la página siguiente a las disponibles en el nodo de configuración seleccionado. Sin embargo, cualquier base de datos JDBC y fuentes de datos de perfil de usuario AEM se muestran de forma predeterminada. Si no selecciona un nodo de configuración, se enumeran las fuentes de datos de todos los nodos de configuración.

   Toque **[!UICONTROL Siguiente]**.

1. (**Aplicable solo si las fuentes de datos están configuradas**) La pantalla **[!UICONTROL Seleccionar origen de datos]** enumera las fuentes de datos disponibles, si las hay. Seleccione los orígenes de datos que desee utilizar en el modelo de datos de formulario.
1. Pulse **[!UICONTROL Crear]** y, en el cuadro de diálogo de confirmación, pulse **[!UICONTROL Abrir]** para abrir el editor del modelo de datos de formulario.

Vamos a revisar los diferentes componentes de la interfaz de usuario del editor del modelo de datos de formulario.

![Modelo de datos de formulario con tres fuentes de datos: un servicio RESTful, AEM perfil de usuario y un RDBMS](assets/fdm-ui.png)

**A.** Fuentes de datosEnumera los orígenes de datos de un modelo de datos de formulario. Expanda un origen de datos para ver los objetos y servicios del modelo de datos.

**B. Actualizar** definiciones de fuentes de datosRecupera cualquier cambio en las definiciones de fuentes de datos de orígenes de datos configurados y las actualiza en la ficha Fuentes de datos del editor del modelo de datos de formulario.

**C. Área** ModelContent donde aparecen los objetos del modelo de datos añadidos.

**D. Área** ServiciosContenido donde aparecen operaciones o servicios de fuentes de datos añadidos.

**E.** Herramientas de barra de herramientas para trabajar con el modelo de datos de formulario. La barra de herramientas muestra más opciones en función del objeto seleccionado en el modelo de datos de formulario.

**F. Agregar** seleccionadosAñade objetos y servicios del modelo de datos seleccionado al modelo de datos del formulario.

Para obtener más información sobre el editor del modelo de datos de formulario y cómo puede trabajar con él para editar y configurar el modelo de datos de formulario, consulte [Trabajo con el modelo de datos de formulario](../../forms/using/work-with-form-data-model.md).

## Actualizar fuentes de datos {#update}

Haga lo siguiente para agregar o actualizar orígenes de datos a un modelo de datos de formulario existente.

1. Vaya a **[!UICONTROL Forms > Integraciones de datos]**, seleccione el modelo de datos de formulario en el que desea agregar o actualizar orígenes de datos y pulse **[!UICONTROL Propiedades]**.
1. En las propiedades del modelo de datos de formulario, vaya a la pestaña **[!UICONTROL Actualizar origen]**.

   En la pestaña Actualizar origen :

   * Pulse el icono Examinar en el campo **[!UICONTROL Configuración según el contexto]** y seleccione un nodo de configuración en el que reside la configuración de nube para el origen de datos que desea añadir. Si no selecciona ningún nodo, las configuraciones de nube que residen únicamente en el nodo `global` se enumeran al pulsar **[!UICONTROL Agregar fuentes]**.

   * Para agregar un nuevo origen de datos, pulse **[!UICONTROL Agregar orígenes]** y seleccione los orígenes de datos que desea agregar al modelo de datos del formulario. Se muestran todas las fuentes de datos configuradas en `global` y el nodo de configuración seleccionado, si existe.

   * Para reemplazar una fuente de datos existente por otra fuente de datos del mismo tipo, pulse el icono **[!UICONTROL Editar]** de la fuente de datos y seleccione en la lista de fuentes de datos disponibles.
   * Para eliminar una fuente de datos existente, pulse el icono **[!UICONTROL Eliminar]** de la fuente de datos. El icono Eliminar está desactivado si se agrega un objeto de modelo de datos en el origen de datos en el modelo de datos del formulario.

   ![fdm-properties](assets/fdm-properties.png)

1. Toque **[!UICONTROL Guardar y cerrar]** para guardar las actualizaciones.

>[!NOTE]
>
>Una vez que agregue nuevos orígenes de datos o actualice los orígenes de datos existentes en un modelo de datos de formulario, asegúrese de actualizar las referencias de enlace, según corresponda, en formularios adaptables y comunicaciones interactivas que utilicen el modelo de datos de formulario actualizado.

## Pasos siguientes {#next-steps}

Ahora tiene un modelo de datos de formulario con orígenes de datos agregados. A continuación, puede editar el modelo de datos de formulario para agregar y configurar objetos y servicios del modelo de datos, agregar asociaciones entre objetos del modelo de datos, editar propiedades, agregar objetos y propiedades del modelo de datos personalizado, generar datos de ejemplo, etc.

Para obtener más información, consulte [Trabajo con el modelo de datos de formulario](../../forms/using/work-with-form-data-model.md).
