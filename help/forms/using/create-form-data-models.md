---
title: Crear un modelo de datos de formulario
seo-title: Create form data model
description: Aprenda a crear modelos de datos de formulario con o sin fuentes de datos configuradas.
seo-description: Learn how to create form data models with or without configured data sources.
uuid: 5a94f733-0c08-41bb-983f-e7d34816d8fb
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: 7c392909-ff84-4411-b44f-16f99dffac54
docset: aem65
feature: Form Data Model
exl-id: 7f5978c3-6c9f-4ce4-b0fb-660ac1d49244
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 100%

---

# Crear un modelo de datos de formulario{#create-form-data-model}

![](do-not-localize/data-integeration.png)

La integración de datos de AEM Forms ofrece una interfaz de usuario intuitiva para crear y trabajar con modelos de datos de formulario. Un modelo de datos de formulario se basa en fuentes de datos para el intercambio de datos; sin embargo, puede crear un modelo de datos de formulario con o sin una fuente de datos. Existen dos métodos para crear un modelo de datos de formulario en función de si ha configurado fuentes de datos:

* **Utilizando fuentes de datos preconfiguradas**: Si ha configurado las fuentes de datos tal como se describe en [Configurar fuentes de datos](../../forms/using/configure-data-sources.md), puede seleccionarlas al crear un modelo de datos de formulario. Incorpora todos los objetos, propiedades y servicios del modelo de datos de las fuentes de datos seleccionados que se pueden utilizar en el modelo de datos de formulario.

* **Sin fuentes de datos**: Si no ha configurado fuentes de datos para su modelo de datos de formulario, puede crearlos sin fuentes de datos. Puede utilizar el modelo de datos de formulario para crear formularios adaptables y comunicaciones interactivas y probarlos con datos de ejemplo. Cuando haya fuentes de datos disponibles, puede vincular el modelo de datos de formulario con fuentes de datos, lo que se reflejará automáticamente en los formularios adaptables asociados y en las comunicaciones interactivas.

>[!NOTE]
>
>Debe ser miembro de los grupos **fdm-author** y **forms-user** para poder crear y trabajar con el modelo de datos de formulario. Póngase en contacto con su administrador de AEM para convertirse en miembro de los grupos.

## Crear un modelo de datos de formulario {#data-sources}

Asegúrese de haber configurado las fuentes de datos que desea utilizar en el modelo de datos de formulario como se describe en [Configurar fuentes de datos](../../forms/using/configure-data-sources.md). Para crear un modelo de datos de formulario basado en fuentes de datos configuradas, haga lo siguiente:

1. En la instancia de autor de AEM, navegue hasta **[!UICONTROL Formularios > Integraciones de datos]**.
1. Pulse **[!UICONTROL Crear > Modelo de datos de formulario.]**
1. En el cuadro de diálogo Crear un modelo de datos de formulario:

   * Especifique un nombre para el modelo de datos del formulario.
   * (**Opcional**) Especifique el título, la descripción y las etiquetas del modelo de datos del formulario.
   * (**Opcional y aplicable solo si se configuran fuentes de datos**) Pulse el icono de verificación situado junto al campo **[!UICONTROL Configuración de la fuente de datos]** y seleccione el nodo de configuración donde residen los servicios en la nube para las fuentes de datos que desea utilizar. Restringe la lista de fuentes de datos disponibles para su selección en la página siguiente a las disponibles en el nodo de configuración seleccionado. Sin embargo, cualquier base de datos JDBC y fuentes de datos de perfil de usuario de AEM se muestran de forma predeterminada. Si no selecciona un nodo de configuración, se enumeran las fuentes de datos de todos los nodos de configuración.

   Pulse **[!UICONTROL Siguiente]**.

1. (**Aplicable únicamente si se han configurado fuentes de datos**). La pantalla **[!UICONTROL Seleccionar fuente de datos]** enumera las fuentes de datos disponibles, si las hay. Seleccione las fuentes de datos que desee utilizar en el modelo de datos de formulario.
1. Pulse **[!UICONTROL Crear]** y en el cuadro de diálogo de confirmación, pulse **[!UICONTROL Abrir]** para abrir el editor del modelo de datos de formulario.

Revisemos los diferentes componentes de la interfaz de usuario del editor del modelo de datos de formulario.

![Un modelo de datos de formulario con tres fuentes de datos: un servicio RESTful, un perfil de usuario de AEM y un RDBMS](assets/fdm-ui.png)

**A. Fuentes de datos** Muestra las fuentes de datos en un modelo de datos de formulario. Expanda una fuente de datos para ver los objetos y servicios del modelo de datos.

**B. Actualizar definiciones de fuentes de datos** Recupera cualquier cambio en las definiciones de fuentes de datos configuradas y las actualiza en la pestaña Fuentes de datos del editor del modelo de datos de formulario.

**C. Modelo** Área de contenido en la que aparecen los objetos del modelo de datos añadidos.

**D. Servicios** Área de contenido en la que aparecen las operaciones o los servicios de las fuentes de datos añadidas.

**E. Barra de herramientas** Herramientas para trabajar con el modelo de datos de formulario. La barra de herramientas muestra más opciones en función del objeto seleccionado en el modelo de datos de formulario.

**F. Agregar selección** Agrega objetos y servicios del modelo de datos seleccionado al modelo de datos de formulario.

Para obtener más información sobre el editor del modelo de datos de formulario y cómo puede trabajar con él para editar y configurar el modelo de datos de formulario, consulte [Trabajar con el modelo de datos de formulario](../../forms/using/work-with-form-data-model.md).

## Actualizar fuentes de datos {#update}

Haga lo siguiente para agregar o actualizar fuentes de datos a un modelo de datos de formulario existente.

1. Vaya a **[!UICONTROL Formularios > Integraciones de datos]**, seleccione el modelo de datos de formulario en el que desea agregar o actualizar las fuentes de datos y pulse **[!UICONTROL Propiedades]**.
1. En las propiedades del modelo de datos de formulario, vaya a la pestaña **[!UICONTROL Actualizar fuente]**.

   En la pestaña Actualizar fuente:

   * Pulse el icono Examinar en el campo **[!UICONTROL Configuración según el contexto]** y seleccione un nodo de configuración en el que reside la configuración de nube para la fuente de datos que desea agregar. Si no selecciona ningún nodo, solo se enumeran las configuraciones de nube que residen en el nodo `global` al pulsar **[!UICONTROL Añadir fuentes]**.

   * Para agregar una fuente de datos nueva, pulse **[!UICONTROL Añadir fuentes]** y seleccione las fuentes de datos que desea añadir al modelo de datos de formulario. Se muestran todas las fuentes de datos configuradas en `global` y el nodo de configuración seleccionado, de haber.

   * Para reemplazar una fuente de datos existente por otra fuente de datos del mismo tipo, pulse el icono **[!UICONTROL Editar]** para la fuente de datos y seleccione en la lista de fuentes de datos disponibles.
   * Para eliminar una fuente de datos existente, pulse el icono **[!UICONTROL Eliminar]** para la fuente de datos. El icono Eliminar está desactivado si se añade un objeto de modelo de datos en la fuente de datos en el modelo de datos del formulario.

   ![fdm-properties](assets/fdm-properties.png)

1. Pulse **[!UICONTROL Guardar y cerrar]** para guardar las actualizaciones.

>[!NOTE]
>
>Una vez que agregue nuevas fuentes de datos o actualice las fuentes de datos existentes en un modelo de datos de formulario, asegúrese de actualizar las referencias de enlace, según corresponda, en los formularios adaptables que utilizan el modelo de datos de formulario actualizado.

## Pasos siguientes {#next-steps}

Ahora tiene un modelo de datos de formulario con fuentes de datos agregadas. A continuación, puede editar el modelo de datos de formulario para agregar y configurar objetos y servicios del modelo de datos, agregar asociaciones entre objetos del modelo de datos, editar propiedades, agregar objetos y propiedades del modelo de datos personalizado, generar datos de ejemplo, etc.

Para obtener más información, consulte [Trabajo con el modelo de datos de formulario](../../forms/using/work-with-form-data-model.md).
