---
title: Modelos en el repositorio
seo-title: Modelos en el repositorio
description: nulo
seo-description: nulo
uuid: 54f81180-4178-4e33-a6f0-e9e6ea50798e
contentOwner: User
content-type: reference
discoiquuid: ae1a72f4-d8c1-4c75-ba2c-7322f3743b17
noindex: true
redirecttarget: /content/help/en/experience-manager/6-4/mobile/using/administer-mobile-apps
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444
workflow-type: tm+mt
source-wordcount: '1332'
ht-degree: 1%

---


# Modelos en el repositorio{#models-in-repository}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Un modelo contiene un conjunto de tipos de datos que definen las propiedades que los servicios de contenido procesarán en última instancia. Un modelo también define las relaciones entre otros modelos para aplicar la integridad de los datos.

Como desarrollador, debe estar familiarizado con la estructura del modelo en el repositorio. Puede crear sus propios modelos y entidades según los requisitos de la aplicación.

## Creación de tipos de modelo {#creating-model-types}

Existen dos tipos de modelos proporcionados por el sistema en */libs/settings/mobileapps/model-types*. Si desea anular los tipos de modelo de sistema, deberá crear un nodo *mobileapps/model-types* en el nodo de configuración en el que desea que se produzca la anulación.

Por ejemplo, si ha creado configuraciones en */conf/myconf1* y */conf/myconf2* y desea anular los tipos de modelos de sistema en *conf1* sólo, crearía un nodo *mobileapps/model-types* en la configuración de *conf1 a9/>.*

Si desea permitir que se agreguen tipos de datos a un modelo, el tipo de modelo debe tener un nodo secundario denominado &#39;scaffolding&#39; de tipo &#39;cq:Page&#39; y un tipo de recurso de *wcm/scaffolding/components/scaffolding*.

La página de scaffolding también debe incluir una propiedad *dataTypesConfig* en el nodo PageContent que indica que se permitirá el uso de los modelos de tipos de datos creados a partir de este tipo.

>[!NOTE]
>
>Un **andamiaje** es una página que define los tipos de datos que puede editar una entidad basada en el modelo. También se puede configurar cada tipo de datos para definir cómo se presentará el campo en la interfaz de usuario, así como cómo se mantendrá el valor de los datos.

### Configuración de tipos de datos {#data-types-config}

El nodo de configuración de tipos de datos contiene una lista de elementos de tipo de datos. Cada elemento de tipo de datos especifica cómo aparecerá un tipo de datos en el editor de modelos, así como la forma en que debe persistir para que una entidad lo pueda procesar en su momento.

| **Nombre de propiedad** | **Descripción** |
|---|---|
| fieldIcon | clase del icono CoralUI para representar el tipo de datos |
| fieldPropResourceType | componente que representará todas las propiedades para configurar el tipo de datos |
| fieldProperties | lista de varios valores de los componentes de propiedad que se utilizan cuando fieldPropResourceType es *mobileapps/caas/gui/components/models/editor/datatypes/field* |
| fieldResourceType | resourceType del nodo persistente para el tipo de datos (es decir, el componente que procesará la propiedad en el editor de entidades) |
| fieldViewResourceType | componente que se utilizará para procesar el tipo de datos en la vista del editor de modelos (se utilizará fieldResourceType si se omite esta propiedad) |
| fieldTitle | nombre del tipo de datos que se mostrará en el editor de modelos |
| multiFieldResourceType | tipo de recurso que se utilizará en un nodo persistente cuando se seleccione un valor múltiple |
| outputType | pista de procesamiento para la representación del lado del cliente |

### Superposición de configuración de tipos de datos {#data-types-config-overlay}

La propiedad &#39;dataTypesConfig&#39; admite la combinación de recursos de Sling. Esto significa que los tipos de datos utilizados por los tipos de modelo del sistema (o incluso los tipos de modelo personalizados) se pueden personalizar mediante nodos de superposición.

Deberá crearse una superposición de */libs/settings/mobileapps/models/formbuilderconfig/datatypes* y, a continuación, personalizarse según lo desee.

Por ejemplo, se puede agregar una superposición para el tipo de datos String para cambiar fieldResourceType a un componente personalizado.

Para obtener más información sobre la fusión de recursos Sling, consulte [Uso de la fusión de recursos Sling en AEM](/help/sites-developing/sling-resource-merger.md).

![climage_1-7](assets/chlimage_1-7.png)

### Tipos de datos {#data-types}

Un tipo de datos de modelo es un componente de formulario que puede incluir datos que se incluirán al publicar un formulario. El componente de tipo de datos puede ser tan complicado como desee. Un ejemplo de un tipo de datos personalizado podría ser un bloque de direcciones para un país en particular para evitar tener que volver a crearlo todo el tiempo usando los tipos de datos primitivos.

Consulte &#39;/libs/mobileapps/caas/components/form/contentreference&#39; como ejemplo de un tipo de datos personalizado.

Todos los tipos de datos primitivos utilizan los componentes de formulario Granite existentes. Consulte: [https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html)

A continuación, se puede agregar cualquier tipo de datos personalizado a una configuración de tipo de datos para que lo utilice el editor de modelos.

## Creación de modelos {#creating-models}

Puede crear inicios de modelos una vez que se hayan desarrollado todos los tipos de modelo y tipos de datos deseados. En última instancia, los autores utilizarán modelos para crear entidades a partir de las cuales los servicios de contenido utilizan para procesar sus datos.

La creación de un modelo consiste en elegir un tipo de modelo permitido basado en la configuración actual y, a continuación, proporcionar un título y una descripción.

Para obtener más información sobre la creación y administración de un modelo desde el panel, consulte [Creación de un modelo](/help/mobile/administer-mobile-apps.md) en la sección de creación de aplicaciones móviles.

### Propiedades de un modelo {#properties-of-a-model}

La tabla siguiente muestra las propiedades definidas para un modelo:

| **Nombre de propiedad** | **Descripción** |
|---|---|
| Título del modelo | nombre del modelo |
| Descripción | descripción del modelo |
| Miniatura    | imagen en miniatura del modelo |
| Tipo de modelo | tipo del modelo (puede ser una cadena simple o una ruta a un componente real) |
| Elementos secundarios permitidos | ruta de una plantilla que puede ser secundaria de esta plantilla |
| Principales permitidos | ruta de una plantilla que puede ser un elemento principal de esta plantilla |

>[!NOTE]
>
>Las propiedades *elementos secundarios* y *elementos principales* permitidos siguen las mismas reglas que las plantillas de página. Para obtener más información, consulte [Plantillas de página](/help/sites-developing/page-templates-static.md).
>
>En referencia a la propiedad *Tipo de modelo*, todos los modelos deben tener un supertipo de *mobileapps/caas/components/data/entity* pero pueden tener un subtipo que permita personalizar el envío de contenido. Garantizar que todos los tipos de modelos sean únicos también puede ayudar a los clientes de los servicios de contenido a distinguir entre objetos de los datos.

### Edición de un modelo {#editing-a-model}

Editar un modelo implica abrir el formulario de diálogo de scaffolding asociado a un modelo para su edición. Generalmente, el scaffolding es un nodo secundario del modelo, pero puede ubicarse fuera del modelo si lo desea especificando su ruta mediante la propiedad &#39;cq:scaffolding&#39;. Esto resulta útil si desea compartir el mismo andamiaje entre varios modelos que necesitan tener propiedades diferentes.

Cuando se encuentra el andamiaje del modelo, el editor de modelos procesará lo que se encuentre en &#39;jcr:content/cq:dialog/content&#39;. Actualmente, el motor formbuilder del lado del cliente solo admite un diseño fijo de hasta 3 columnas. A la derecha del cuadro de diálogo del formulario procesado encontrará una lista de todos los tipos de datos especificados en la configuración de tipos de datos. Para editar los tipos de datos, haga clic en ellos. A continuación, el carril derecho cambiará a la ficha de propiedades del tipo de datos seleccionado. Se pueden agregar nuevos tipos de datos arrastrándolos al lienzo de la previsualización. Al hacer clic en Guardar se propagan los cambios al servidor. Al hacer clic en Cancelar se cierra el editor de modelos.

>[!NOTE]
>
>Todos los modelos son plantillas, por lo que siguen todas las reglas de plantilla AEM. Esto permite utilizar propiedades como *permissionParents* y *allowChildren*. Son eficaces a la hora de crear nuevas entidades basadas en un modelo. Las reglas de plantilla garantizan que las entidades solo se pueden basar en determinados modelos según su jerarquía.
>
>Para obtener más información sobre la edición de un modelo desde el panel, consulte [Creación de un modelo](/help/mobile/administer-mobile-apps.md) en la sección de creación de aplicaciones móviles.

### Modelos de sistema {#system-models}

Se proporcionan dos tipos de modelos de sistema predefinidos para la reutilización de contenido simple. Estos modelos no se pueden editar.

**Modelo** de páginasEl modelo de páginas proporciona un método rápido para reutilizar contenido existente de sitios para su envío por servicios de contenido.

El resourceType de entidades basadas en el modelo Pages es: mobileapps/caas/components/data/pages

Ruta: Ruta a una página Sitios. Los controladores de servicios de contenido representarán el contenido de esta ruta (y sus elementos secundarios).

**Modelo** de recursosEl modelo Assets proporciona un método rápido para reutilizar contenido existente de Recursos para su envío por servicios de contenido.

El resourceType de entidades basadas en el modelo Pages es: *aplicaciones/caas/componentes/datos/recursos.*

Lista de recursos: Lista de rutas desde Recursos. Cada recurso se agregará como nodo de entidad secundario con un resourceType de *wcm/foundation/components/image*.

>[!NOTE]
>
>Para obtener más información sobre el uso de estas plantillas para crear modelos desde el panel, consulte [Creación de un modelo](/help/mobile/administer-mobile-apps.md) en la sección de creación de aplicaciones móviles.
