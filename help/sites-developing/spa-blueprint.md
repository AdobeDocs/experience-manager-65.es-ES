---
title: SPA modelo
seo-title: SPA modelo
description: En el presente documento se describe el contrato general, independiente del marco, que debe cumplir cualquier marco SPA para aplicar componentes SPA editables en AEM.
seo-description: En el presente documento se describe el contrato general, independiente del marco, que debe cumplir cualquier marco SPA para aplicar componentes SPA editables en AEM.
uuid: 48f2d415-ec34-49dc-a8e1-6feb5a8a5bbe
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 04ac8203-320b-4671-aaad-6e1397b12b6f
docset: aem65
translation-type: tm+mt
source-git-commit: c1b5df634eba0628c8d2e0b38b9c220cbee8ec62
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 0%

---


# Modelo de SPA{#spa-blueprint}

Para permitir que el autor utilice el Editor de SPA de AEM para editar el contenido de un SPA, hay requisitos que el SPA debe cumplir, que se describen en este documento.

>[!NOTE]
>
>El Editor de SPA es la solución recomendada para proyectos que requieren SPA procesamiento del lado del cliente basado en el marco de trabajo (por ejemplo, React o Angular).

## Introducción {#introduction}

En este documento se describe el contrato general que debe cumplir cualquier marco de trabajo SPA (es decir, el tipo de capa de soporte AEM) para implementar componentes SPA editables dentro de AEM.

>[!NOTE]
>
>Los siguientes requisitos son independientes del marco. Si se cumplen estos requisitos, se puede proporcionar una capa específica del marco compuesta de módulos, componentes y servicios.
>
>**Estos requisitos ya se cumplen para los marcos React y Angular en AEM.** Los requisitos de este modelo sólo son relevantes si desea implementar otro marco para su uso con AEM.

>[!CAUTION]
>
>Aunque las capacidades SPA de AEM son independientes del marco, actualmente solo se admiten los marcos React y Angular.

Para permitir que el autor utilice el Editor de páginas AEM para editar los datos expuestos por un marco de aplicación de una sola página, un proyecto debe poder interpretar la estructura del modelo que representa la semántica de los datos almacenados para una aplicación dentro del repositorio de AEM. Para lograr este objetivo, se proporcionan dos bibliotecas que no dependen del marco de trabajo: el `PageModelManager` y el `ComponentMapping`.

### PageModelManager {#pagemodelmanager}

La biblioteca `PageModelManager` se proporciona como un paquete NPM para que lo utilice un proyecto SPA. Acompaña al SPA y sirve como administrador de modelos de datos.

En nombre del SPA, abstrae la recuperación y administración de la estructura JSON que representa la estructura de contenido real. También es responsable de sincronizar con el SPA para informarle de cuándo tiene que volver a procesar sus componentes.

Consulte el paquete NPM [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)

Al inicializar `PageModelManager`, la biblioteca carga primero el modelo raíz proporcionado de la aplicación (mediante parámetro, meta propiedad o dirección URL actual). Si la biblioteca identifica que el modelo de la página actual no forma parte del modelo raíz que busca e incluye como modelo de una página secundaria.

![page_model_SoloConsolidación](assets/page_model_consolidation.png)

### ComponentMapping {#componentmapping}

El módulo `ComponentMapping` se proporciona como paquete NPM al proyecto front-end. Almacena componentes front-end y proporciona una forma para que el SPA asigne componentes front-end a AEM tipos de recursos. Esto permite una resolución dinámica de los componentes al analizar el modelo JSON de la aplicación.

Cada elemento presente en el modelo contiene un campo `:type` que expone un tipo de recurso AEM. Cuando se monta, el componente front-end puede procesarse utilizando el fragmento de modelo que ha recibido de las bibliotecas subyacentes.

#### Asignación dinámica de modelos a componentes {#dynamic-model-to-component-mapping}

Para obtener más información sobre cómo se produce la asignación de modelos dinámicos a componentes en el SDK de SPA de Javascript para AEM, consulte el artículo [Asignación de modelos dinámicos a componentes para SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

### Capa específica del marco {#framework-specific-layer}

Se debe implementar una tercera capa para cada marco de trabajo front-end. Esta tercera biblioteca es responsable de interactuar con las bibliotecas subyacentes y proporciona una serie de puntos de entrada bien integrados y fáciles de usar para interactuar con el modelo de datos.

En el resto del presente documento se describen los requisitos de este nivel intermedio específico y se aspira a ser independiente del marco. Si se cumplen los siguientes requisitos, se puede proporcionar una capa específica del marco para que los componentes del proyecto interactúen con las bibliotecas subyacentes encargadas de administrar el modelo de datos.

## Conceptos generales {#general-concepts}

### Modelo de página {#page-model}

La estructura de contenido de la página se almacena en AEM. El modelo de la página se utiliza para asignar y crear instancias de componentes de SPA. Los desarrolladores de SPA crean SPA componentes que asignan a AEM componentes. Para ello, utilizan el tipo de recurso (o ruta al componente AEM) como clave única.

Los componentes de SPA deben estar sincronizados con el modelo de página y actualizarse con los cambios correspondientes en su contenido. Se debe utilizar un patrón que aproveche los componentes dinámicos para crear instancias de los componentes sobre la marcha siguiendo la estructura del modelo de página proporcionada.

### Campos meta {#meta-fields}

El modelo de página aprovecha el exportador de modelos JSON, que se basa en la API [Sling Model](https://sling.apache.org/documentation/bundles/models.html). Los modelos de ventas exportables exponen la siguiente lista de campos para permitir que las bibliotecas subyacentes interpreten el modelo de datos:

* `:type`:: Tipo del recurso AEM (predeterminado = tipo de recurso)
* `:children`:: Hijos jerárquicos del recurso actual. Los elementos secundarios no forman parte del contenido interno del recurso actual (se pueden encontrar en elementos que representan una página)
* `:hierarchyType`:: Tipo jerárquico de un recurso. El `PageModelManager` admite actualmente el tipo de página

* `:items`:: Recursos de contenido secundario del recurso actual (estructura anidada, solo presentes en contenedores)
* `:itemsOrder`:: Lista ordenada de los niños. El objeto de mapa JSON no garantiza el orden de sus campos. Al tener el mapa y la matriz actual, el consumidor de la API tiene las ventajas de ambas estructuras
* `:path`:: Ruta de contenido de un elemento (presente en elementos que representan una página)

Consulte también [Introducción a AEM Content Services.](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)

### Módulo específico de marco {#framework-specific-module}

La separación de las preocupaciones ayuda a facilitar la ejecución del proyecto. Por lo tanto, debe proporcionarse un paquete específico para npm. Este paquete es responsable de agregar y exponer los módulos base, servicios y componentes. Estos componentes deben encapsular la lógica de administración del modelo de datos y proporcionar acceso a los datos que espera el componente del proyecto. El módulo también se encarga de exponer de forma transitoria los puntos de entrada útiles de las bibliotecas subyacentes.

Para facilitar la interoperabilidad de las bibliotecas, Adobe aconseja al módulo específico de la estructura que agrupe las siguientes bibliotecas. Si es necesario, la capa puede encapsular y adaptar las API subyacentes antes de exponerlas al proyecto.

* [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)
* [@adobe/aem-spa-mapeo de componentes](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

#### Implementaciones {#implementations}

#### Reaccionar {#react}

módulo npm: [@adobe/aem-response-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### Angular {#angular}

módulo npm: próximamente

## Servicios principales y componentes {#main-services-and-components}

Las siguientes entidades deben aplicarse de conformidad con las directrices específicas de cada marco. En función de la arquitectura del marco, la implementación puede variar ampliamente, pero se deben proporcionar las funcionalidades descritas.

### El proveedor de modelos {#the-model-provider}

Los componentes del proyecto deben delegar el acceso a los fragmentos de un modelo en un proveedor de modelos. A continuación, el proveedor de modelos se encarga de escuchar los cambios realizados en el fragmento especificado del modelo y devolver el modelo actualizado al componente que delega.

Para ello, el proveedor de modelos debe registrarse en ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`. A continuación, cuando se produce un cambio, recibe y pasa los datos actualizados al componente que delega. Por convención, la propiedad puesta a disposición del componente de delegación que transportará el fragmento de modelo se denomina `cqModel`. La implementación puede proporcionar esta propiedad al componente, pero debe considerar aspectos como la integración con la arquitectura del marco, la capacidad de descubrimiento y la facilidad de uso.

### El decorador HTML de componentes {#the-component-html-decorator}

El decorador de componentes es responsable de decorar el HTML exterior del elemento de cada instancia de componente con una serie de atributos de datos y nombres de clase que espera el Editor de páginas.

#### Declaración de componente {#component-declaration}

Los metadatos siguientes deben agregarse al elemento HTML externo producido por el componente del proyecto. Permiten al Editor de páginas recuperar la configuración de edición correspondiente.

* `data-cq-data-path`:: Ruta al recurso en relación con la variable  `jcr:content`

#### Declaración y marcador de posición de capacidad de edición {#editing-capability-declaration-and-placeholder}

Los siguientes metadatos y nombres de clase deben agregarse al elemento HTML externo producido por el componente del proyecto. Permiten que el Editor de páginas oferta las funcionalidades relacionadas.

* `cq-placeholder`:: Nombre de clase que identifica el marcador de posición de un componente vacío
* `data-emptytext`:: Etiqueta que mostrará la superposición cuando una instancia de componente esté vacía

**Marcador de posición para componentes vacíos**

Cada componente debe ampliarse con una funcionalidad que decorará el elemento HTML exterior con atributos de datos y nombres de clase específicos de los marcadores de posición y las superposiciones relacionadas cuando el componente se identifique como vacío.

**Vacío de un componente**

* ¿El componente está lógicamente vacío?
* ¿Cuál debe ser la etiqueta que muestra la superposición cuando el componente está vacío?

### Contenedor {#container}

Un contenedor es un componente diseñado para contener y procesar componentes secundarios. Para ello, el contenedor repite las propiedades `:itemsOrder`, `:items` y `:children` de su modelo.

El contenedor obtiene dinámicamente los componentes secundarios del almacén de la biblioteca ` [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping)`. A continuación, el contenedor amplía el componente secundario con las funciones del proveedor de modelos y finalmente lo crea una instancia.

### Página {#page}

El componente `Page` amplía el componente `Container`. Un contenedor es un componente diseñado para contener y procesar componentes secundarios, incluidas páginas secundarias. Para ello, el contenedor repite las propiedades `:itemsOrder`, `:items` y `:children` de su modelo. El componente `Page` obtiene dinámicamente los componentes secundarios del almacén de la biblioteca [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping). El `Page` es responsable de crear instancias de componentes secundarios.

### Cuadrícula interactiva {#responsive-grid}

El componente Cuadrícula adaptable es un contenedor. Contiene una variante específica del proveedor de modelos que representa sus columnas. La cuadrícula adaptable y sus columnas son responsables de decorar el elemento HTML exterior del componente del proyecto con los nombres de clase específicos contenidos en el modelo.

El componente Cuadrícula adaptable debe estar preasignado a su contraparte AEM, ya que este componente es complejo y raramente personalizado.

#### Campos de modelo específicos {#specific-model-fields}

* `gridClassNames:` Nombres de clase proporcionados para la cuadrícula adaptable
* `columnClassNames:` Nombres de clase proporcionados para la columna adaptable

Consulte también el recurso npm [@adobe/aem-response-editable-components#srccomponentsSresponsivegridjsx](https://www.npmjs.com/package/@adobe/aem-react-editable-components#srccomponentsresponsivegridjsx)

#### Marcador de posición de la cuadrícula de respuesta {#placeholder-of-the-reponsive-grid}

El componente SPA se asigna a un contenedor gráfico como la cuadrícula interactiva y debe agregar un marcador de posición secundario virtual cuando se crea el contenido. Cuando el Editor de páginas crea el contenido de la SPA, este se incrusta en el editor mediante un iframe y el atributo `data-cq-editor` se agrega al nodo de documento de dicho contenido. Cuando el atributo `data-cq-editor` está presente, el contenedor debe incluir un elemento HTML para representar el área con la que interactúa el autor al insertar un nuevo componente en la página.

Por ejemplo:

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>El editor de páginas requiere actualmente los nombres de clase utilizados en el ejemplo.
>
>* `"new section"`:: Indica que el elemento actual es el marcador de posición del contenedor
>* `"aem-Grid-newComponent"`:: Normaliza el componente para la creación de maquetaciones

>



#### Asignación de componentes {#component-mapping}

La biblioteca [`Component Mapping`](/help/sites-developing/spa-blueprint.md#componentmapping) subyacente y su función `MapTo` pueden encapsularse y ampliarse para proporcionar las funcionalidades relativas a la configuración de edición proporcionada junto con la clase de componente actual.

```
const EditConfig = {

    emptyLabel: 'My Component',

    isEmpty: function() {
        return !this.props || !this.props.cqModel || this.props.cqModel.isEmpty;
    }
};

class MyComponent extends Component {

    render() {
        return <div className={'my-component'}></div>;
    }
}

MapTo('component/resource/path')(MyComponent, EditConfig);
```

En la implementación anterior, el componente del proyecto se amplía con la funcionalidad de vacío antes de que se registre realmente en el almacén [Asignación de componentes](/help/sites-developing/spa-blueprint.md#componentmapping). Esto se lleva a cabo encapsulando y extendiendo la biblioteca [`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping) para introducir la compatibilidad con el objeto de configuración `EditConfig`:

```
/**
 * Configuration object in charge of providing the necessary data expected by the page editor to initiate the authoring. The provided data will be decorating the associated component
 *
 * @typedef {{}} EditConfig
 * @property {String} [dragDropName]       If defined, adds a specific class name enabling the drag and drop functionality
 * @property {String} emptyLabel           Label to be displayed by the placeholder when the component is empty. Optionally returns an empty text value
 * @property {function} isEmpty            Should the component be considered empty. The function is called using the context of the wrapper component giving you access to the component model
 */

/**
 * Map a React component with the given resource types. If an {@link EditConfig} is provided the <i>clazz</i> is wrapped to provide edition capabilities on the AEM Page Editor
 *
 * @param {string[]} resourceTypes                      - List of resource types for which to use the given <i>clazz</i>
 * @param {class} clazz                                 - Class to be instantiated for the given resource types
 * @param {EditConfig} [editConfig]                     - Configuration object for enabling the edition capabilities
 * @returns {class}                                     - The resulting decorated Class
 */
ComponentMapping.map = function map (resourceTypes, clazz, editConfig) {};
```

## Contrato con el Editor de páginas {#contract-with-the-page-editor}

Los componentes del proyecto deben generar como mínimo los siguientes atributos de datos para permitir al editor interactuar con ellos.

* `data-cq-data-path`:: Ruta relativa del componente según lo proporciona  `PageModel` (por ejemplo,  `"root/responsivegrid/image"`). Este atributo no debe agregarse a las páginas.

En resumen, para que el editor de páginas lo interprete como editable, un componente de proyecto debe respetar el siguiente contrato:

* Proporcione los atributos esperados para asociar una instancia de componente front-end a un recurso AEM.
* Proporcione la serie esperada de atributos y nombres de clase que permiten la creación de marcadores de posición vacíos.
* Proporcione los nombres de clase esperados que permiten arrastrar y soltar recursos.

### Estructura de elementos HTML típica {#typical-html-element-structure}

El siguiente fragmento ilustra la representación HTML típica de una estructura de contenido de página. Estos son algunos puntos importantes:

* El elemento de cuadrícula adaptable lleva nombres de clase con el prefijo `aem-Grid--`
* El elemento de columna interactivo lleva nombres de clase con el prefijo `aem-GridColumn--`
* Una cuadrícula adaptable que también es la columna de una cuadrícula principal está ajustada, como por ejemplo los dos prefijos anteriores no aparecen en el mismo elemento
* Los elementos correspondientes a recursos editables llevan una propiedad `data-cq-data-path`. Consulte la sección [Contrato con el Editor de páginas](#contract-wtih-the-page-editor) de este documento.

```
<div data-cq-data-path="/content/page">
    <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
        <div class="aem-container aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/content/page/jcr:content/root/responsivegrid">
            <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
                <div class="cmp-image cq-dd-image aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/root/responsivegrid/image">
                    <img src="/content/we-retail-spa-sample/react/jcr%3acontent/root/responsivegrid/image.img.jpeg/1512113734019.jpeg">
                </div>
            </div>
        </div>
    </div>
</div>
```

## Navegación y Enrutamiento {#navigation-and-routing}

La aplicación posee el enrutamiento. El desarrollador front-end primero debe implementar un componente de navegación (asignado a un componente de navegación AEM). Este componente procesaría los vínculos de URL que se usarían junto con una serie de rutas que mostrarán u ocultarán fragmentos de contenido.

La biblioteca [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) subyacente y su módulo ` [ModelRouter](/help/sites-developing/spa-routing.md)` (habilitado de forma predeterminada) son responsables de la recuperación previa y el acceso al modelo asociado con una ruta de recursos determinada.

Las dos entidades están relacionadas con la noción de enrutamiento, pero ` [ModelRouter](/help/sites-developing/spa-routing.md)` sólo es responsable de que el ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)` se cargue con un modelo de datos estructurado en sincronización con el estado de la aplicación actual.

Consulte el artículo [SPA Enrutamiento del modelo](/help/sites-developing/spa-routing.md) para obtener más información.

## SPA en acción {#spa-in-action}

Vea cómo funciona un SPA simple y experimente con un SPA usted mismo continuando con el documento [Introducción a SPA en AEM](/help/sites-developing/spa-getting-started-react.md).

## Lectura adicional {#further-reading}

Para obtener más información sobre SPA en AEM, consulte los siguientes documentos:

* [SPA ](/help/sites-developing/spa-overview.md) Descripción general de creación para obtener información general sobre SPA en AEM y el modelo de comunicación
* [Introducción a SPA en ](/help/sites-developing/spa-getting-started-react.md) AEMpara obtener una guía sobre una SPA sencilla y cómo funciona
