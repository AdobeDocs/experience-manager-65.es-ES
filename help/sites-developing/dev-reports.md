---
title: Desarrollo de informes
description: Adobe Experience Manager AEM () proporciona una selección de informes estándar basados en un marco de informes
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 3891150e-9972-4bbc-ad61-7f46a1f9bbb4
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '5182'
ht-degree: 0%

---


# Desarrollo de informes {#developing-reports}

Adobe Experience Manager AEM () proporciona una selección de [informes estándar](/help/sites-administering/reporting.md) la mayoría de los cuales se basan en un marco de informes.

Con el marco de trabajo, puede ampliar estos informes estándar o desarrollar sus propios informes nuevos. El marco de trabajo de creación de informes se integra estrechamente con los conceptos y principios de CQ5 existentes, de modo que los desarrolladores puedan utilizar sus conocimientos actuales de CQ5 como trampolín para la creación de informes.

AEM Para los informes estándar entregados con la ayuda de:

* Estos informes se basan en el marco de informes:

   * [Informe sobre componentes](/help/sites-administering/reporting.md#component-report)
   * [Informe de actividad de la página](/help/sites-administering/reporting.md#page-activity-report)
   * [Informe del usuario](/help/sites-administering/reporting.md#user-report)
   * [Informe de instancia de flujo de trabajo](/help/sites-administering/reporting.md#workflow-instance-report)

* Los siguientes informes se basan en principios individuales y, por lo tanto, no se pueden ampliar:

   * [Uso del disco](/help/sites-administering/reporting.md#disk-usage)
   * [Comprobación de estado](/help/sites-administering/reporting.md#health-check)
   * [Informe de flujo de trabajo](/help/sites-administering/reporting.md#workflow-report)

>[!NOTE]
>
>El tutorial [Creación De Su Propio Informe: Un Ejemplo](#creating-your-own-report-an-example) también muestra cuántos de los principios siguientes se pueden utilizar.
>
>También puede consultar los informes estándar para ver otros ejemplos de implementación.

>[!NOTE]
>
>En los ejemplos y definiciones siguientes se utiliza la siguiente notación:
>
>* Cada línea define un nodo o una propiedad donde:
>  `N:<name> [<nodeType>]` : Describe un nodo con el nombre de `<*name*>` y el tipo de nodo de `<*nodeType*>`*.*
>  `P:<name> [<propertyType]` : Describe una propiedad con el nombre de `<*name*>` y un tipo de propiedad de `<*propertyType*>`.
>  `P:<name> = <value>` : Describe una propiedad `<name>` que debe establecerse en el valor de `<value>`.
>
>* La sangría muestra las dependencias jerárquicas entre los nodos.
>* Elementos separados por | indica una lista de elementos posibles; por ejemplo, tipos o nombres; por ejemplo, `String|String[]` significa que la propiedad puede ser String o String[].
>
>* `[]` representa una matriz; como Cadena[] o una matriz de nodos como en el [Definición de consulta](#query-definition).
>
>A menos que se indique lo contrario, los tipos predeterminados son:
>
>* Nodos - `nt:unstructured`
>* Propiedades - `String`

## Marco de informes {#reporting-framework}

El marco para la presentación de informes se basa en los siguientes principios:

* Se basa completamente en los conjuntos de resultados que devuelve una consulta ejecutada por el QueryBuilder CQ5.
* El conjunto de resultados define los datos mostrados en el informe. Cada fila del conjunto de resultados corresponde a una fila de la vista tabular del informe.
* Las operaciones disponibles para la ejecución en el conjunto de resultados se parecen a los conceptos de RDBMS; principalmente *agrupación* y *agregación*.

* La mayoría de las operaciones de recuperación y procesamiento de datos se realizan en el servidor.
* El cliente es el único responsable de mostrar los datos preprocesados. Solo las tareas de procesamiento menores (por ejemplo, la creación de vínculos en el contenido de la celda) se ejecutan en el lado del cliente.

El marco de trabajo de creación de informes (ilustrado por la estructura de un informe estándar) utiliza los siguientes componentes básicos, alimentados por la cola de procesamiento:

![chlimage_1-248](assets/chlimage_1-248.png)

### Página de informe {#report-page}

La página del informe es:

* Una página CQ5 estándar.
* Basado en un [plantilla CQ5 estándar, configurada para el informe](#report-template).

### Base del informe {#report-base}

El [`reportbase` componente](#report-base-component) forma la base de cualquier informe porque:

* Conserva la definición de [query](#the-query-and-data-retrieval) que proporciona el conjunto de resultados subyacente de datos.

* Es un sistema de párrafos adaptado que contiene todas las columnas ( `columnbase`) se ha añadido al informe.
* Define qué tipos de gráficos están disponibles y cuáles están activos actualmente.
* Define el cuadro de diálogo Editar, que permite al usuario configurar ciertos aspectos del informe.

### Base de columna {#column-base}

Cada columna es una instancia de [`columnbase` componente](#column-base-component) que:

* Es un párrafo utilizado por parsys ( `reportbase`) del informe respectivo.
* Define el vínculo a [conjunto de resultados subyacente](#the-query-and-data-retrieval). Es decir, define los datos específicos a los que se hace referencia dentro de este conjunto de resultados y cómo se procesan.
* Conserva definiciones adicionales; como los agregados y filtros disponibles, junto con los valores predeterminados.

### La consulta y recuperación de datos {#the-query-and-data-retrieval}

La consulta:

* Se define como parte de [`reportbase`](#report-base) componente.
* Se basa en [CQ QueryBuilder](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/QueryBuilder.html).
* Recupera los datos utilizados como base del informe. Cada fila del conjunto de resultados (tabla) está vinculada a un nodo tal como lo devuelve la consulta. Información específica para [columnas individuales](#column-base-component) a continuación, se extrae de este conjunto de datos.

* Por lo general consta de:

   * Una ruta raíz.

     Esto especifica el subárbol del repositorio que se va a buscar.

     Para minimizar el impacto en el rendimiento, se recomienda restringir (intentar) la consulta a un subárbol específico del repositorio. La ruta raíz puede estar predefinida en el [plantilla de informe](#report-template) o configurado por el usuario en el [Cuadro de diálogo Configuración (Editar)](#configuration-dialog).

   * [Uno o más criterios](#query-definition).

     Se imponen para producir el conjunto de resultados (inicial); incluyen, por ejemplo, restricciones en el tipo de nodo o restricciones de propiedad.

**El punto clave aquí es que cada nodo devuelto en el conjunto de resultados de la consulta se utiliza para generar una sola fila en el informe (con una relación 1:1).**

El desarrollador debe asegurarse de que la consulta definida para un informe devuelva un conjunto de nodos adecuado para ese informe. Sin embargo, el nodo en sí no necesita contener toda la información necesaria, esto también puede derivarse de nodos principales o secundarios. Por ejemplo, la consulta utilizada para [Informe de usuario](/help/sites-administering/reporting.md#user-report) selecciona nodos según el tipo de nodo (en este caso, ). `rep:user`). Sin embargo, la mayoría de las columnas de este informe no toman sus datos directamente de estos nodos, sino de los nodos secundarios `profile`.

### Cola de procesamiento {#processing-queue}

El [query](#the-query-and-data-retrieval) devuelve un conjunto de resultados de datos que se mostrarán como filas en el informe. Cada fila del conjunto de resultados se procesa (del lado del servidor), en [varias fases](#phases-of-the-processing-queue), antes de transferirse al cliente para su visualización en el informe.

Esto permite:

* Extraer y derivar valores del conjunto de resultados subyacente.

  Por ejemplo, permite procesar dos valores de propiedad como un solo valor calculando la diferencia entre los dos.

* Resolver valores extraídos; esto se puede hacer de varias formas.

  Por ejemplo, las rutas se pueden asignar a un título (como en el contenido más legible en lenguaje natural del respectivo *jcr:título* property).

* Aplicación de filtros en varios puntos.
* Crear valores compuestos, si es necesario.

  Por ejemplo, consta de un texto que se muestra al usuario, un valor que se utilizará para ordenar y una dirección URL adicional que se utilizará (en el lado del cliente) para crear un vínculo.

#### Flujo de trabajo de la cola de procesamiento {#workflow-of-the-processing-queue}

El siguiente flujo de trabajo representa la cola de procesamiento:

![chlimage_1-249](assets/chlimage_1-249.png)

#### Fases de la cola de procesamiento {#phases-of-the-processing-queue}

Donde los pasos y elementos detallados son:

1. Transforma los resultados devueltos por [consulta inicial (base de informes)](#query-definition) en el conjunto de resultados básico mediante extractores de valor.

   Los extractores de valores se eligen automáticamente en función de la variable [tipo de columna](#column-specific-definitions). Se utilizan para leer valores de la consulta JCR subyacente y crear un conjunto de resultados a partir de ellos; después de lo cual se puede aplicar un procesamiento adicional. Por ejemplo, para `diff` type, el extractor de valores lee dos propiedades, calcula el valor único que luego se agrega al conjunto de resultados. No se pueden configurar los extractores de valores.

1. Para acceder a ese conjunto de resultados inicial, que contiene datos sin procesar, [filtrado inicial](#column-specific-definitions) (*crudo* fase).

1. Los valores son [preprocesado](#processing-queue); tal como se define para *aplicar* fase.

1. [Filtrado](#column-specific-definitions) (asignado al *preprocesado* fase) se ejecuta en los valores preprocesados.

1. Los valores se resuelven en función de la variable [resolución definida](#processing-queue).
1. [Filtrado](#column-specific-definitions) (asignado al *resuelto* fase) se ejecuta en los valores resueltos.

1. Los datos son [agrupadas y agregadas](#column-specific-definitions).
1. Los datos de matriz se resuelven convirtiéndolos en una lista (basada en cadenas).

   Este es un paso implícito que convierte un resultado de varios valores en una lista que se puede mostrar; es necesario para valores de celda (no agregados) basados en propiedades JCR de varios valores.

1. Los valores vuelven a aparecer [preprocesado](#processing-queue); tal como se define para *afterApply* fase.

1. Se ordenan los datos.
1. Los datos procesados se transfieren al cliente.

>[!NOTE]
>
>La consulta inicial que devuelve el conjunto de resultados de datos base se define en la variable `reportbase` componente.
>
>Otros elementos de la cola de procesamiento se definen en la variable `columnbase` componentes.

## Construcción y configuración de informes {#report-construction-and-configuration}

Para construir y configurar un informe, es necesario lo siguiente:

* a [ubicación para la definición de los componentes del informe](#location-of-report-components)
* a [`reportbase` componente](#report-base-component)
* una o más, [`columnbase` componentes](#column-base-component)
* a [componente de página](#page-component)
* a [diseño de informe](#report-design)
* a [plantilla de informe](#report-template)

### Ubicación de los componentes del informe {#location-of-report-components}

Los componentes predeterminados de creación de informes se encuentran en `/libs/cq/reporting/components`.

Sin embargo, se recomienda no actualizar estos nodos, sino crear sus propios nodos de componente en `/apps/cq/reporting/components` o, si procede, `/apps/<yourProject>/reports/components`.

Donde (por ejemplo):

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
```

En esta sección, se crea la raíz del informe y, en esta sección, el componente de base del informe y los componentes de base de columna:

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
                N:<reportname> [sling:Folder]
                        N:<reportname> [cq:Component]  // report base component
                        N:<columnname> [cq:Component]  // column base component
```

### Componente Página  {#page-component}

Una página de informe debe utilizar el `sling:resourceType` de `/libs/cq/reporting/components/reportpage`.

No debería ser necesario un componente de página personalizado (normalmente).

## Componente de base del informe {#report-base-component}

Cada tipo de informe requiere un componente contenedor derivado de `/libs/cq/reporting/components/reportbase`.

Este componente actúa como un contenedor para el informe en su conjunto y proporciona información para:

* El [definición de consulta](#query-definition).
* Un [Cuadro de diálogo (opcional)](#configuration-dialog) para configurar el informe.
* Cualquiera [Gráficos](#chart-definitions) que se integran con el informe.

```
N:<reportname> [cq:Component]
    P:sling:resourceSuperType = "cq/reporting/components/reportbase"
    N:charting
    N:dialog [cq:Dialog]
    N:queryBuilder
```

### Definición de consulta {#query-definition}

```xml
N:queryBuilder
    N:propertyConstraints
    [
        N:<name> // array of nodes (name irrelevant), each with the following properties:
            P:name
            P:value
    ]
    P:nodeTypes [String|String[]]
    P:mandatoryProperties [String|String[]
  ]
```

* `propertyConstraints`

  Limita el conjunto de resultados a nodos que tienen propiedades específicas con valores específicos. Si se especifican varias restricciones, el nodo debe satisfacerlas todas (operación AND).

  Por ejemplo:

  ```
  N:propertyConstraints
   [
   N:0
   P:sling:resourceType
   P:foundation/components/textimage
   N:1
   P:jcr:modifiedBy
   P:admin
   ]
  ```

  Devolvería todo `textimage` componentes modificados por última vez por el `admin` usuario.

* `nodeTypes`

  Se utiliza para limitar el conjunto de resultados a los tipos de nodo especificados. Se pueden especificar varios tipos de nodo.

* `mandatoryProperties`

  Limita el conjunto de resultados a los nodos que tienen *todo* las propiedades especificadas. El valor de las propiedades no se tiene en cuenta.

Todos son opcionales y se pueden combinar según sea necesario, pero debe definir al menos uno de ellos.

### Definiciones de gráficos {#chart-definitions}

```xml
N:charting
    N:settings
        N:active [cq:WidgetCollection]
        [
            N:<name> // array of nodes, each with the following property
                P:id   // must match the id of a child node of definitions
        ]
    N:definitions [cq:WidgetCollection]
    [
        N:<name> // array of nodes, each with the following properties
            P:id
            P:type
            // additional, chart type specific configurations
    ]
```

* `settings`

  Contiene definiciones de los gráficos activos.

   * `active`

     Como se pueden definir varias configuraciones, puede utilizarlas para definir cuáles están activas actualmente. Se definen mediante una matriz de nodos (no hay una convención de nombres obligatoria para estos nodos, pero los informes estándar suelen utilizar `0`, `1`.. `x`), cada una con la siguiente propiedad:

      * `id`

        Identificación de los gráficos activos. Debe coincidir con el ID de uno de los gráficos `definitions`.

* `definitions`

  Define los tipos de gráficos que pueden estar disponibles para el informe. El `definitions` que se va a utilizar especifica el `active` configuración.

  Las definiciones se especifican mediante una matriz de nodos (también denominados con frecuencia `0`, `1`.. `x`), cada una con las siguientes propiedades:

   * `id`

     La identificación del gráfico.

   * `type`

     Tipo de gráfico disponible. Seleccionar de:

      * `pie`
Gráfico circular. Generado solo a partir de datos actuales.

      * `lineseries`
Serie de líneas (puntos de conexión que representan las instantáneas reales). Generado solo a partir de datos históricos.

   * Hay propiedades adicionales disponibles, según el tipo de gráfico:

      * para el tipo de gráfico `pie`:

         * `maxRadius` ( `Double/Long`)

           El radio máximo permitido para el gráfico circular; por lo tanto, el tamaño máximo permitido para el gráfico (sin leyenda). Ignorado si `fixedRadius` está definida.

         * `minRadius` ( `Double/Long`)

           Radio mínimo permitido para el gráfico circular. Ignorado si `fixedRadius` está definida.

         * `fixedRadius` ( `Double/Long`) Define un radio fijo para el gráfico circular.

      * para el tipo de gráfico [`lineseries`](/help/sites-administering/reporting.md#display-limits):

         * `totals` ( `Boolean`)

           True si se muestra una línea adicional **Total** debería mostrarse.
predeterminada: `false`

         * `series` ( `Long`)

           Número de líneas/series que se mostrarán.
valor predeterminado: `9` (también es el máximo permitido)

         * `hoverLimit` ( `Long`)

           Número máximo de instantáneas agregadas (puntos mostrados en cada línea horizontal, que representan valores distintos) para las que se mostrarán ventanas emergentes. Es decir, cuando el usuario pasa el ratón sobre un valor distinto o la etiqueta correspondiente en la leyenda del gráfico.

           valor predeterminado: `35` (es decir, no se muestran ventanas emergentes si se aplican más de 35 valores distintos a la configuración del gráfico actual).

           Hay un límite adicional de diez ventanas emergentes que se pueden mostrar en paralelo (se pueden mostrar varias ventanas emergentes cuando se pasa el ratón sobre los textos de la leyenda).

### Cuadro de diálogo Configuración {#configuration-dialog}

Cada informe puede tener un cuadro de diálogo de configuración, que permite al usuario especificar varios parámetros para el informe. Se puede acceder a este cuadro de diálogo a través de **Editar** cuando la página del informe está abierta.

Este cuadro de diálogo es un CQ estándar [diálogo](/help/sites-developing/components-basics.md#dialogs) y se pueden configurar como tales (consulte [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Dialog) para obtener más información).

Un cuadro de diálogo de ejemplo puede tener el siguiente aspecto:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    jcr:primaryType="cq:Dialog"
    height="{Long}424">
    <items jcr:primaryType="cq:WidgetCollection">
        <props jcr:primaryType="cq:Panel">
            <items jcr:primaryType="cq:WidgetCollection">
                <title
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/title.infinity.json"
                    xtype="cqinclude"/>
                <description
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/description.infinity.json"
                    xtype="cqinclude"/>
                <rootPath
                    jcr:primaryType="cq:Widget"
                    fieldLabel="Root path"
                    name="./report/rootPath"
                    rootPath=""
                    rootTitle="Repository root"
                    xtype="pathfield"/>
                <processing
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/processing.infinity.json"
                    xtype="cqinclude"/>
                <scheduling
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/scheduling.infinity.json"
                    xtype="cqinclude"/>
            </items>
        </props>
    </items>
</jcr:root>
```

Se proporcionan varios componentes preconfigurados, a los que se puede hacer referencia en el cuadro de diálogo, utilizando `xtype` propiedad con un valor de `cqinclude`:

* **`title`**

  `/libs/cq/reporting/components/commons/title`

  Campo de texto para definir el título del informe.

* **`description`**

  `/libs/cq/reporting/components/commons/description`

  Área de texto para definir la descripción del informe.

* **`processing`**

  `/libs/cq/reporting/components/commons/processing`

  Selector para el modo de procesamiento del informe (carga manual o automática de datos).

* **`scheduling`**

  `/libs/cq/reporting/components/commons/scheduling`

  Selector para programar instantáneas para el gráfico histórico.

>[!NOTE]
>
>Los componentes a los que se hace referencia deben incluirse utilizando `.infinity.json` sufijo (consulte el ejemplo anterior).

### Ruta de acceso raíz {#root-path}

Además, se puede definir una ruta raíz para el informe:

* **`rootPath`**

  Esto limita el informe a una determinada sección (árbol o subárbol) del repositorio, lo que se recomienda para la optimización del rendimiento. La ruta raíz la especifica el `rootPath` propiedad del `report` nodo de cada página del informe (tomado de la plantilla al crear la página).

  Se puede especificar mediante:

   * el [plantilla de informe](#report-template) (como valor fijo o como valor predeterminado para el cuadro de diálogo de configuración).
   * el usuario (con este parámetro)

## Componente de base de columna {#column-base-component}

Cada tipo de columna requiere un componente derivado de `/libs/cq/reporting/components/columnbase`.

Un componente de columna define una combinación de lo siguiente:

* El [Consulta específica de columna](#column-specific-query) configuración.
* El [Resoluciones y preprocesamiento](#resolvers-and-preprocessing).
* El [Definiciones específicas de columna](#column-specific-definitions) (como filtros y agregados; `definitions` nodo secundario).
* [Valores predeterminados de columna](#column-default-values).
* El [Filtro de cliente](#client-filter) para extraer la información que se va a mostrar de los datos devueltos por el servidor.
* Además, un componente de columna debe proporcionar una instancia adecuada de `cq:editConfig`. para definir el [Eventos y acciones](#events-and-actions) requerido.
* La configuración de [columnas genéricas](#generic-columns).

```
N:<columnname> [cq:Component]
    P:componentGroup
    P:jcr:title
    P:sling:resourceSuperType = "cq/reporting/components/columnbase"
    N:cq:editConfig [cq:EditConfig] // <a href="#events-and-actions">Events and Actions</a>
    N:defaults // <a href="#column-default-values">Column Default Values</a>
    N:definitions
      N:queryBuilder // <a href="#column-specific-query">Column Specific Query</a>
        P:property [String|String[]] // Column Specific Query
        P:subPath // Column Specific Query
        P:secondaryProperty [String|String[]] // Column Specific Query
        P:secondarySubPath // Column Specific Query
      N:data
        P:clientFilter [String] // <a href="#client-filter">Client Filter</a>
        P:resolver // <a href="#resolvers-and-preprocessing">Resolvers and Preprocessing</a>
        N:resolverConfig // Resolvers and Preprocessing
        N:preprocessing // Resolvers and Preprocessing
      P:type // <a href="#column-specific-definitions">Column Specific Definitions</a>
      P:groupable [Boolean] // Column Specific Definitions
      N:filters [cq:WidgetCollection] // Column Specific Definitions
      N:aggregates [cq:WidgetCollection] // Column Specific Definitions
```

Consulte también [Definición del nuevo informe](#defining-your-new-report).

### Consulta específica de columna {#column-specific-query}

Define la extracción de datos específica (de la [conjunto de resultados de datos de informe](#the-query-and-data-retrieval)) para su uso en la columna individual.

```xml
N:definitions
    N:queryBuilder
        P:property [String|String[]]
        P:subPath
        P:secondaryProperty [String|String[]]
        P:secondarySubPath
```

* `property`

  Define la propiedad que se utilizará para calcular el valor real de la celda.

  Si una propiedad se define como Cadena[]Sin embargo, se analizan varias propiedades (en secuencia) para encontrar el valor real.

  Por ejemplo, si hay:

  `property = [ "jcr:lastModified", "jcr:created" ]`

  El extractor de valores correspondiente (que está en control aquí):

   * Comprueba si hay una propiedad jcr:lastModified disponible y, si es así, utilícela.
   * Si no hay ninguna propiedad jcr:lastModified disponible, se utiliza el contenido de jcr:created en su lugar.

* `subPath`

  Si el resultado no está en el nodo devuelto por la consulta, `subPath` define dónde se encuentra la propiedad.

* `secondaryProperty`

  Una segunda propiedad que debe utilizarse para calcular el valor real de la celda. Esta definición solo se utiliza para ciertos tipos de columna (diff y ordenable).

  Por ejemplo, si existe el Informe de instancias de flujo de trabajo, la propiedad especificada se utiliza para almacenar el valor real de la diferencia horaria (en milisegundos) entre las horas de inicio y finalización.

* `secondarySubPath`

  Similar a subPath, cuando `secondaryProperty` se utiliza.

Por lo general, solo `property` se utiliza.

### Filtro de cliente {#client-filter}

El filtro de cliente extrae la información que se va a mostrar de los datos devueltos por el servidor.

>[!NOTE]
>
>Este filtro se ejecuta en el lado del cliente, después de aplicar todo el procesamiento del lado del servidor.

```xml
N:definitions
    N:data
        P:clientFilter [String]
```

El `clientFilter` es una función de JavaScript que:

* como entrada, recibe un parámetro; los datos devueltos por el servidor (preprocesados completamente)
* como salida, devuelve el valor filtrado (procesado); los datos extraídos o derivados de la información de entrada

El siguiente ejemplo extrae la ruta de página correspondiente de una ruta de componente:

```
function(v) {
    var sepPos = v.lastIndexOf('/jcr:content');
    if (sepPos < 0) {
        return v;
    }
    return v.substring(sepPos + '/jcr:content'.length, v.length);
}
```

### Resoluciones y preprocesamiento {#resolvers-and-preprocessing}

El [cola de procesamiento](#processing-queue) define los distintos solucionadores y configura el preprocesamiento:

```xml
N:definitions
    N:data
        P:resolver
        N:resolverConfig
        N:preprocessing
            N:apply
            N:applyAfter
```

* `resolver`

  Define la resolución que se va a utilizar. Están disponibles las siguientes soluciones:

   * `const`

     Asigna valores a otros valores; por ejemplo, se utiliza para resolver constantes como `en` a su valor equivalente `English`.

   * `default`

     Resolución predeterminada. Este es un solucionador ficticio que no resuelve nada.

   * `page`

     Resuelve un valor de ruta en la ruta de la página correspondiente; más precisamente, en la correspondiente `jcr:content` nodo. Por ejemplo, `/content/.../page/jcr:content/par/xyz` se ha resuelto en `/content/.../page/jcr:content`.

   * `path`

     Resuelve un valor de ruta añadiendo opcionalmente una subruta y tomando el valor real de una propiedad del nodo (tal como se define en `resolverConfig`) en la ruta resuelta. Por ejemplo, una `path` de `/content/.../page/jcr:content` se puede resolver en el contenido del `jcr:title` , esto significaría que se resuelve una ruta de página en el título de la página.

   * `pathextension`

     Resuelve un valor anteponiendo una ruta y tomando el valor real de una propiedad del nodo en la ruta resuelta. Por ejemplo, un valor `de` puede ir precedido de una ruta como `/libs/wcm/core/resources/languages`, tomando el valor de la propiedad `language`, para resolver el código de país `de` a la descripción del idioma `German`.

* `resolverConfig`

  Proporciona definiciones para la resolución. Las opciones disponibles dependen de la variable `resolver` seleccionados:

   * `const`

     Utilice las propiedades para especificar las constantes que desea resolver. El nombre de la propiedad define la constante que se va a resolver; el valor de la propiedad define el valor resuelto.

     Por ejemplo, una propiedad con **Nombre**= `1` y **Valor** `=One` resuelve 1 en Uno.

   * `default`

     No hay ninguna configuración disponible.

   * `page`

      * `propertyName` (opcional)

        Define el nombre de la propiedad que debe utilizarse para resolver el valor. Si no se especifica, el valor predeterminado de *jcr:título* (el título de la página); para el `page` resolver, esto significa que primero la ruta se resuelve en la ruta de la página y luego se resuelve en el título de la página.

   * `path`

      * `propertyName` (opcional)

        Especifica el nombre de la propiedad que debe utilizarse para resolver el valor. Si no se especifica, el valor predeterminado de `jcr:title` se utiliza.

      * `subPath` (opcional)

        Esta propiedad se puede utilizar para especificar un sufijo que se anexará a la ruta antes de resolver el valor.

   * `pathextension`

      * `path` (mandatory)

        Define la ruta que se va a anteponer.

      * `propertyName` (mandatory)

        Define la propiedad en la ruta de acceso resuelta donde se encuentra el valor real.

      * `i18n` (opcional; escriba booleano)

        Determina si el valor resuelto debe ser *internacionalizado* (es decir, utilizar [Servicios de internacionalización de CQ5](/help/sites-administering/tc-manage.md)).

* `preprocessing`

  El preprocesamiento es opcional y se puede enlazar (por separado) a las fases de procesamiento *aplicar* o *applyAfter*:

   * `apply`

     La fase inicial de preprocesamiento ([paso 3 en la representación de la cola de procesamiento](#processing-queue)).

   * `applyAfter`

     Aplicar después del preprocesamiento ([paso 9 en la representación de la cola de procesamiento](#processing-queue)).

#### Resoluciones {#resolvers}

Los solucionadores se utilizan para extraer la información necesaria. Algunos ejemplos de los distintos solucionadores son:

**Const**

Lo siguiente resuelve un valor constante de `VersionCreated` a la cadena `New version created`.

Consulte `/libs/cq/reporting/components/auditreport/typecol/definitions/data`.

```xml
N:data
    P:resolver=const
    N:resolverConfig
        P:VersionCreated="New version created"
```

**Página**

Resuelve un valor de ruta en la propiedad jcr:description del nodo jcr:content (secundario) de la página correspondiente.

Consulte `/libs/cq/reporting/components/compreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=page
    N:resolverConfig
        P:propertyName="jcr:description"
```

**Ruta**

Lo siguiente resuelve una ruta de `/content/.../page` al contenido de la `jcr:title` , esto significaría que se resuelve una ruta de página en el título de la página.

Consulte `/libs/cq/reporting/components/auditreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=path
    N:resolverConfig
        P:propertyName="jcr:title"
        P:subPath="/jcr:content"
```

**Extensión de ruta**

Lo siguiente antepone un valor `de` con la extensión de ruta `/libs/wcm/core/resources/languages`, luego toma el valor de la propiedad `language`, para resolver el código de país `de` a la descripción del idioma `German`.

Consulte `/libs/cq/reporting/components/userreport/languagecol/definitions/data`.

```xml
N:data
    P:resolver=pathextension
    N:resolverConfig
        P:path="/libs/wcm/core/resources/languages"
        P:propertyName="language"
```

#### Preprocesamiento {#preprocessing}

El `preprocessing` La definición de se puede aplicar a:

* valor original:

  La definición de preprocesamiento para el valor original se especifica en `apply` y/o `applyAfter` directamente.

* valor en estado agregado:

  Si es necesario, se puede proporcionar una definición independiente para cada agregación.

  Para especificar un preprocesamiento explícito para los valores agregados, las definiciones de preprocesamiento deben residir en un `aggregated` nodo secundario ( `apply/aggregated`, `applyAfter/aggregated`). Si se requiere un preprocesamiento explícito para agregados distintos, la definición de preprocesamiento se encuentra en un nodo secundario con el nombre del agregado respectivo (por ejemplo, `apply/aggregated/min/max` u otros agregados).

Puede especificar cualquiera de las siguientes opciones para utilizarlas durante el preprocesamiento:

* [buscar y reemplazar patrones](#preprocessing-find-and-replace-patterns)
Cuando se encuentra, el patrón especificado (que se define como una expresión regular) se reemplaza por otro patrón; por ejemplo, esto se puede utilizar para extraer una subcadena del original.

* [formateadores de tipo de datos](#preprocessing-data-type-formatters)

  Convierte un valor numérico en una cadena relativa; por ejemplo, el valor &quot;que representa una diferencia horaria de una hora&quot; se resuelve en una cadena como `1:24PM (1 hour ago)`.

Por ejemplo:

```xml
N:definitions
    N:data
        N:preprocessing
            N:apply|applyAfter
                P:pattern         // regex
                P:replace         // replacement for regex
                // and/or
                P:format          // data type formatter
```

#### Preprocesamiento: buscar y reemplazar patrones {#preprocessing-find-and-replace-patterns}

Para el preprocesamiento, puede especificar un `pattern` (definido como [expresión regular](https://en.wikipedia.org/wiki/Regular_expression) o regex) que se encuentra y luego se sustituye por la variable `replace` pattern:

* `pattern`

  Expresión regular que se utiliza para localizar una subcadena.

* `replace`

  Cadena o representación de la cadena que se utiliza como reemplazo de la cadena original. A menudo, esto representa una subcadena de la cadena ubicada por la expresión regular `pattern`.

Un reemplazo de ejemplo se puede desglosar como:

* Para el nodo `definitions/data/preprocessing/apply` con las dos propiedades siguientes:

   * `pattern`: `(.*)(/jcr:content)(/|$)(.*)`
   * `replace`: `$1`

* Una cadena que llega como:

   * `/content/geometrixx/en/services/jcr:content/par/text`

* Se divide en cuatro secciones:

   * `$1` - `(.*)` - `/content/geometrixx/en/services`
   * `$2` - `(/jcr:content)` - `/jcr:content`
   * `$3` - `(/|$)` - `/`
   * `$4` - `(.*)` - `par/text`

* Y se sustituye por la cadena representada por `$1`:

   * `/content/geometrixx/en/services`

#### Preprocesamiento: tipos de datos para materias {#preprocessing-data-type-formatters}

Estos formateadores convierten un valor numérico en una cadena relativa.

Por ejemplo, esto se puede utilizar para una columna de tiempo que permita `min`, `avg` y `max` agregados. Como `min`/ `avg`/ `max` los agregados se muestran como una *diferencia horaria* (por ejemplo, `10 days ago`), requieren un formateador de datos. Para esto, un `datedelta` formatter se aplica al `min`/ `avg`/ `max` valores agregados. Si un `count` El agregado también está disponible, no se necesita un formateador ni el valor original.

Actualmente, los formateadores de tipo de datos disponibles son:

* `format`

  Formador de tipo de datos:

   * `duration`

     La duración es el lapso de tiempo entre dos fechas definidas. Por ejemplo, el inicio y el final de una acción de flujo de trabajo que tardó una hora, empezando el 13/2/11 a las 11:23h y finalizando una hora más tarde el 13/2/11 a las 12:23h.

     Convierte un valor numérico (interpretado como milisegundos) en una cadena de duración; por ejemplo, `30000` tiene el formato * `30s`.*

   * `datedelta`

     Los datos son el lapso de tiempo entre una fecha pasada y una &quot;ahora&quot; (por lo que tienen un resultado diferente si el informe se ve en un momento posterior).

     Convierte el valor numérico (interpretado como una diferencia horaria en días) en una cadena de fecha relativa. Por ejemplo, 1 tiene el formato de hace un día.

El siguiente ejemplo define lo siguiente `datedelta` formato para `min` y `max` agregados:

```xml
N:definitions
    N:data
        N:preprocessing
            N:apply
                N:aggregated
                    N:min
                        P:format = "datedelta"
                    N:max
                        P:format = "datedelta"
```

### Definiciones específicas de columna {#column-specific-definitions}

Las definiciones específicas de columna definen los filtros y los agregados disponibles para esa columna.

```xml
N:definitions
    P:type
    P:groupable [Boolean]
    N:filters [cq:WidgetCollection]
    [
        N:<name> // array of nodes (names irrelevant) with the following properties:
            P:filterType
            P:id
            P:phase
    ]
    N:aggregates [cq:WidgetCollection]
    [
        N:<name> // array of nodes (names irrelevant) with the following properties:
            P:text
            P:type
    ]
```

* `type`

  Las siguientes opciones están disponibles como opciones estándar:

   * `string`
   * `number`
   * `int`
   * `date`
   * `diff`
   * `timeslot`

     Se utiliza para extraer partes de una fecha necesaria para la agregación (por ejemplo, agrupar por año para obtener los datos agregados de cada año).

   * `sortable`

     Se utiliza para valores que utilizan valores diferentes (tomados de propiedades diferentes) para ordenarlos y mostrarlos.

  Además, cualquiera de los anteriores puede definirse como de varios valores; por ejemplo, `string[]` define una matriz de cadenas.

  El tipo de columna elige el extractor de valores. Si hay un extractor de valores disponible para un tipo de columna, se utiliza este extractor. De lo contrario, se utiliza el extractor de valores predeterminado.

  Un tipo puede (opcionalmente) tomar un parámetro. Por ejemplo, `timeslot:year` extrae el año de un campo de fecha. Tipos con sus parámetros:

   * `timeslot` - Los valores son comparables a las constantes correspondientes de `java.utils.Calendar`.

      * `timeslot:year` - `Calendar.YEAR`
      * `timeslot:month-of-year` - `Calendar.MONTH`
      * `timeslot:week-of-year` - `Calendar.WEEK_OF_YEAR`
      * `timeslot:day-of-month` - `Calendar.DAY_OF_MONTH`
      * `timeslot:day-of-week` - `Calendar.DAY_OF_WEEK`
      * `timeslot:day-of-year` - `Calendar.DAY_OF_YEAR`
      * `timeslot:hour-of-day` - `Calendar.HOUR_OF_DAY`
      * `timeslot:minute-of-hour` - `Calendar.MINUTE`

* `groupable`

  Define si el informe se puede agrupar por esta columna.

* `filters`

  Definiciones de filtros.

   * `filterType`

     Los filtros disponibles son:

      * `string`

        Un filtro basado en cadenas.

   * `id`

     Identificador de filtro.

   * `phase`

     Fases disponibles:

      * `raw`

        El filtro se aplica a los datos sin procesar.

      * `preprocessed`

        El filtro se aplica a los datos preprocesados.

      * `resolved`

        El filtro se aplica a los datos resueltos.

* `aggregates`

  Definiciones agregadas.

   * `text`

     Nombre textual del agregado. If `text` no se ha especificado, entonces toma la descripción predeterminada del agregado. Por ejemplo, `minimum` se utiliza para `min` acumulado.

   * `type`

     Tipo agregado. Los agregados disponibles son:

      * `count`

        Cuenta el número de filas.

      * `count-nonempty`

        Cuenta el número de filas no vacías.

      * `min`

        Proporciona el valor mínimo.

      * `max`

        Proporciona el valor máximo.

      * `average`

        Proporciona el valor promedio.

      * `sum`

        Proporciona la suma de todos los valores.

      * `median`

        Proporciona el valor medio.

      * `percentile95`

        Utiliza el percentil 95 de todos los valores.

### Valores predeterminados de columna {#column-default-values}

Define los valores predeterminados para la columna:

```xml
N:defaults
    P:aggregate
```

* `aggregate`

  Válido `aggregate` Los valores son los mismos que para `type` bajo `aggregates` (consulte [Definiciones específicas de columna (definiciones - filtros / agregados)](#column-specific-definitions) ).

### Eventos y acciones {#events-and-actions}

Editar configuración define los eventos necesarios para que los oyentes detecten y las acciones que se aplicarán después de que se produzcan dichos eventos. Consulte la [introducción al desarrollo de componentes](/help/sites-developing/components.md) para obtener información general.

Se deben definir los siguientes valores para garantizar que se tengan en cuenta todas las acciones necesarias:

```xml
N:cq:editConfig [cq:EditConfig]
    P:cq:actions [String[]] = "insert", "delete"
    P:cq:dialogMode = "floating"
    P:cq:layout = "auto"
    N:cq:listeners [cq:EditListenersConfig]
        P:aftercreate = "REFRESH_INSERTED"
        P:afterdelete = "REFRESH_SELF"
        P:afteredit = "REFRESH_SELF"
        P:afterinsert = "REFRESH_INSERTED"
        P:aftermove = "REFRESH_SELF"
        P:afterremove = "REFRESH_SELF"
```

### Columnas genéricas {#generic-columns}

Las columnas genéricas son una extensión en la que (la mayoría) de las definiciones de columna se almacenan en la instancia del nodo de columna (en lugar del nodo de componente).

Utilizan un cuadro de diálogo (estándar) que se puede personalizar para el componente genérico individual. Este cuadro de diálogo permite al usuario del informe definir las propiedades de columna de una columna genérica en la página del informe (mediante la opción de menú ) **Propiedades de columna...**).

Un ejemplo es el **Genérico** de la columna **Informe de usuario**. Consulte `/libs/cq/reporting/components/userreport/genericcol`.

Para convertir una columna en genérica:

* Configure las variables `type` propiedad de la columna `definition` nodo a `generic`.

  Consulte `/libs/cq/reporting/components/userreport/genericcol/definitions`

* Especifique una definición de cuadro de diálogo (estándar) en la columna `definition` nodo.

  Consulte `/libs/cq/reporting/components/userreport/genericcol/definitions/dialog`

   * Los campos del cuadro de diálogo deben hacer referencia a los mismos nombres que la propiedad del componente correspondiente, incluida su ruta.

     Por ejemplo, si desea que el tipo de la columna genérica se pueda configurar a través del cuadro de diálogo, utilice un campo con el nombre `./definitions/type`.

   * Las propiedades definidas mediante la interfaz de usuario o el cuadro de diálogo tienen prioridad sobre las definidas en la variable `columnbase` componente.

* Defina Editar configuración.

  Consulte `/libs/cq/reporting/components/userreport/genericcol/cq:editConfig`

* AEM Utilice metodologías estándar de la para definir propiedades de columna (adicionales).

  Para las propiedades definidas tanto en la instancia de componente como en la de columna, el valor de la instancia de columna tiene prioridad.

  Las propiedades disponibles para una columna genérica son:

   * `jcr:title` - nombre de columna
   * `definitions/aggregates` - agregados
   * `definitions/filters` - filtros
   * `definitions/type`: el tipo de columna (que debe definirse en el cuadro de diálogo, ya sea mediante un selector/cuadro combinado o un campo oculto)
   * `definitions/data/resolver` y `definitions/data/resolverConfig` (pero no `definitions/data/preprocessing` o `.../clientFilter`): la resolución y configuración
   * `definitions/queryBuilder` - la configuración del generador de consultas
   * `defaults/aggregate` - el agregado predeterminado

  Si hay una nueva instancia de la columna genérica en la variable **Informe de usuario**, las propiedades definidas con el cuadro de diálogo se conservan en:

  `/etc/reports/userreport/jcr:content/report/columns/genericcol/settings/generic`

## Diseño del informe {#report-design}

El diseño define qué tipos de columnas están disponibles para crear un informe. También define el sistema de párrafos al que se añaden las columnas.

El Adobe recomienda crear un diseño individual para cada informe. Al hacerlo, se garantiza una flexibilidad total. Consulte [Definición del nuevo informe](#defining-your-new-report).

Los componentes predeterminados de creación de informes se encuentran en `/etc/designs/reports`.

La ubicación de los informes puede depender de la ubicación de los componentes:

* `/etc/designs/reports/<yourReport>` es adecuado si el informe se encuentra en `/apps/cq/reporting`

* `/etc/designs/<yourProject>/reports/<*yourReport*>` para informes con el `/apps/<yourProject>/reports` pattern

Las propiedades de diseño requeridas están registradas en `jcr:content/reportpage/report/columns` (por ejemplo, `/etc/designs/reports/<reportName>/jcr:content/reportpage/report/columns`):

* `components`

  Cualquier componente o grupo de componentes que esté permitido en el informe.

* `sling:resourceType`

  Propiedad con valor `cq/reporting/components/repparsys`.

Un ejemplo de fragmento de diseño (tomado del diseño del informe del componente) es el siguiente:

```xml
<!-- ... -->
    <jcr:content
        jcr:primaryType="nt:unstructured"
        jcr:title="Component Report"
        sling:resourceType="wcm/core/components/designer">
        <reportpage jcr:primaryType="nt:unstructured">
            <report jcr:primaryType="nt:unstructured">
                <columns
                    jcr:primaryType="nt:unstructured"
                    sling:resourceType="cq/reporting/components/repparsys"
                    components="group:Component Report"/>
            </report>
        </reportpage>
    </jcr:content>
<!-- ... -->
```

No es necesario especificar diseños para columnas individuales. Las columnas disponibles se pueden definir en el modo de diseño.

>[!NOTE]
>
>El Adobe recomienda no cambiar los diseños estándar de los informes. El objetivo de esto es garantizar que no se pierda ningún cambio al actualizar o instalar revisiones.
>
>Copie el informe y su diseño si desea personalizar un informe estándar.

>[!NOTE]
>
>Las columnas predeterminadas se pueden crear automáticamente cuando se crea un informe. Se especifican en la plantilla.

## Plantilla de informe {#report-template}

Cada tipo de informe debe proporcionar una plantilla. Son estándares [Plantillas CQ](/help/sites-developing/templates.md) y se pueden configurar como tales.

La plantilla debe:

* configure el `sling:resourceType` hasta `cq/reporting/components/reportpage`

* indicar el diseño a utilizar
* crear un `report` nodo secundario que hace referencia al contenedor ( `reportbase`) componente con el `sling:resourceType` propiedad

Un ejemplo de fragmento de plantilla (tomado de la plantilla de informe de componentes) es el siguiente:

```xml
<!-- ... -->
    <jcr:content
        cq:designPath="/etc/designs/reports/compreport"
        jcr:primaryType="cq:PageContent"
        sling:resourceType="cq/reporting/components/reportpage">
        <report
            jcr:primaryType="nt:unstructured"
            sling:resourceType="cq/reporting/components/compreport/compreport"/>
    </jcr:content>
<!-- .. -->
```

Un ejemplo de fragmento de plantilla, que muestra la definición de la ruta raíz (tomada de la plantilla de informe de usuario), es el siguiente:

```xml
<!-- ... -->
    <jcr:content
        cq:designPath="/etc/designs/reports/userreport"
        jcr:primaryType="cq:PageContent"
        sling:resourceType="cq/reporting/components/reportpage">
        <report
            jcr:primaryType="nt:unstructured"
            rootPath="/home/users"
            sling:resourceType="cq/reporting/components/compreport/compreport"/>
    </jcr:content>
<!-- .. -->
```

Las plantillas de informes predeterminadas se encuentran en `/libs/cq/reporting/templates`.

Sin embargo, Adobe recomienda no actualizar estos nodos. Cree sus propios nodos de componente en `/apps/cq/reporting/templates` o, si procede, `/apps/<yourProject>/reports/templates`.

Donde, como ejemplo (consulte también [Ubicación de los componentes del informe](#location-of-report-components)):

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
```

En, cree la raíz para la plantilla:

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
                N:<reportname> [sling:Folder]
```

## Creación De Su Propio Informe: Un Ejemplo {#creating-your-own-report-an-example}

### Definición del nuevo informe {#defining-your-new-report}

Para definir un informe, cree y configure lo siguiente:

1. La raíz de los componentes del informe.
1. Componente de la base del informe.
1. Uno o más componentes base de columna.
1. El diseño del informe.
1. La raíz de la plantilla de informe.
1. La plantilla del informe.

Para ilustrar estos pasos, el siguiente ejemplo define un informe que enumera todas las configuraciones de OSGi dentro del repositorio. Es decir, todas las instancias de `sling:OsgiConfig` nodo.

>[!NOTE]
>
>Copiar un informe existente y luego personalizar la nueva versión es un método alternativo.

1. Cree el nodo raíz para el nuevo informe.

   Por ejemplo, en `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:components [sling:Folder]
               N:osgireport [sling:Folder]
   ```

1. Defina la base de informes. Por ejemplo, `osgireport[cq:Component]` bajo `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:osgireport [sling:Folder]
       N:osgireport [cq:Component]
           P:sling:resourceSuperType [String] = "cq/reporting/components/reportbase"
           N:charting [nt:unstructured]
               N:settings [nt:unstructured]
                   N:active [cq:WidgetCollection]
                       N:0 [nt:unstructured]
                           P:id [String] = "pie"
                       N:1 [nt:unstructured]
                           P:id [String] = "lineseries"
               N:definitions [cq:WidgetCollections]
                   N:0 [nt:unstructured]
                       P:id [String] = "pie"
                       P:maxRadius [Long] = 180
                       P:type [String] = "pie"
                   N:1 [nt:unstructured]
                       P:id [String] = "lineseries"
                       P:type [String] = "lineseries"
           N:dialog [cq:Dialog]
               P:height [Long] = 424
               N:items [cq:WidgetCollection]
                   N:props [cq:Panel]
                       N:items [cq:WidgetCollection]
                           N:title [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/title.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:description [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/description.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:rootPath [cq:Widget]
                               P:fieldLabel [String] = "Root path"
                               P:name [String] = "./report/rootPath"
                               P:xtype [String] = "pathfield"
                           N:processing [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/processing.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:scheduling [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/scheduling.infinity.json"
                               P:xtype [String] = "cqinclude"
           N:queryBuilder [nt:unstructured]
               P:nodeTypes [String[]] = "sling:OsgiConfig"
   ```

   Define un componente de la base de informes que:

   * busca todos los nodos del tipo `sling:OsgiConfig`
   * muestra ambos `pie` y `lineseries` tablas
   * proporciona un cuadro de diálogo para que el usuario configure el informe

1. Defina su primer componente de columna (columnbase). Por ejemplo, `bundlecol[cq:Component]` bajo `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:osgireport [sling:Folder]
       N:bundlecol [cq:Component]
           P:componentGroup [String] = "OSGi Report"
           P:jcr:title = "Bundle"
           P:sling:resourceSuperType [String] = "cq/reporting/components/columnbase"
           N:cq:editConfig [cq:EditConfig]
               P:cq:actions [String[]] = "insert", "delete"
               P:cq:dialogMode [String] = "floating"
               P:cq:layout [String] = "auto"
               N:cq:listeners [cq:EditListenersConfig]
                   P:aftercreate [String] "REFRESH_INSERTED"
                   P:afterdelete [String] "REFRESH_SELF"
                   P:afteredit [String] "REFRESH_SELF"
                   P:afterinsert [String] "REFRESH_INSERTED"
                   P:aftermove [String] "REFRESH_SELF"
                   P:afterremove [String] "REFRESH_SELF"
           N:defaults [nt:unstructured]
               P:aggregate [String] = "count"
           N:definitions [nt:unstructured]
               P:groupable [Boolean] = false
               P:type [String] = "string"
               N:queryBuilder [nt:unstructured]
                   P:property [String] = "jcr:path"
   ```

   Define un componente de base de columna que:

   * busca y devuelve el valor que recibe del servidor; en este caso, la propiedad `jcr:path` para cada `sling:OsgiConfig` nodo
   * proporciona el `count` agregado
   * no se puede agrupar
   * tiene el título `Bundle` (título de columna dentro de la tabla)
   * está en el grupo de tareas `OSGi Report`
   * actualizaciones en eventos especificados

   >[!NOTE]
   >
   >En este ejemplo, no hay definiciones de `N:data` y `P:clientFilter`. Esto se debe a que el valor recibido del servidor se devuelve en 1:1, que es el comportamiento predeterminado.
   >
   >Es lo mismo que las definiciones:
   >
   >```
   >N:data [nt:unstructured]
   >   P:clientFilter [String] = "function(v) { return v; }"
   >```
   >
   >Donde la función simplemente devuelve el valor que recibe.

1. Defina el diseño del informe. Por ejemplo, `osgireport[cq:Page]` bajo `/etc/designs/reports`.

   ```xml
   N:osgireport [cq:Page]
       N:jcr:content [nt:unstructured]
           P:jcr:title [String] = "OSGi report"
           P:sling:resourceType [String] = "wcm/core/components/designer"
           N:reportpage [nt:unstructured]
               N:report [nt:unstructured]
                   N:columns [nt:unstructured]
                       P:components [String] = "group:OSGi Report"
                       P:sling:resourceType [String] = "cq/reporting/components/repparsys"
   ```

1. Cree el nodo raíz para la nueva plantilla de informe.

   Por ejemplo, en `/apps/cq/reporting/templates/osgireport`.

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:templates [sling:Folder]
               N:osgireport [cq:Template]
   ```

1. Defina la plantilla de informe. Por ejemplo, `osgireport[cq:Template]` bajo `/apps/cq/reporting/templates`.

   ```xml
   N:osgireport [cq:Template]
       P:allowedPaths [String[]] = "/etc/reports(/.*)?"
       P:jcr:description [String] = "Use this report generator to create a new OSGi report."
       P:jcr:title [String] = "OSGi Report Template"
       P:ranking [Long] = 100
       P:shortTitle [String] = "OSGi Report"
       N:jcr:content [cq:PageContent]
           P:cq:designPath [String] = "/etc/designs/reports/osgireport"
           P:sling:resourceType [String] = "cq/reporting/components/reportpage"
           N:report [nt:unstructured]
               P:rootPath [String] = "/"
               P:sling:resourceType [String] = "cq/reporting/components/osgireport/osgireport"
       N:thumbnail.png [nt:file]
   ```

   Define una plantilla que:

   * define el `allowedPaths` para los informes resultantes, en el caso anterior, en cualquier lugar bajo `/etc/reports`
   * proporciona títulos y descripciones para la plantilla
   * proporciona una imagen en miniatura para utilizarla en la lista de plantillas (la definición completa de este nodo no aparece en la lista anterior; es más fácil copiar una instancia de thumbnail.png de un informe existente).

### Creación de una instancia del nuevo informe {#creating-an-instance-of-your-new-report}

Ahora se puede crear una instancia del nuevo informe:

1. Abra el **Herramientas** consola.

1. Seleccionar **Informes** en el panel izquierdo.
1. Entonces **Nuevo...** en la barra de herramientas. Defina un **Título** y **Nombre**, seleccione el nuevo tipo de informe (la variable **Plantilla de informe OSGi**) de la lista de plantillas y haga clic en **Crear**.
1. La nueva instancia de informe aparecerá en la lista. Haga doble clic para abrir.
1. Arrastre un componente (para este ejemplo, **Paquete** en el **Informe OSGi** de la barra de tareas para crear la primera columna y [inicio de la definición del informe](/help/sites-administering/reporting.md#the-basics-of-report-customization).

   >[!NOTE]
   >
   >Como este ejemplo no tiene ninguna columna agrupable, los gráficos no están disponibles. Para ver los gráficos, establezca `groupable` hasta `true`:
   >
   >```
   >N:osgireport [sling:Folder]
   > N:bundlecol [cq:Component]
   > N:definitions [nt:unstructured]
   > P:groupable [Boolean] = true
   >```
   >

## Configuración de los servicios de Report Framework {#configuring-the-report-framework-services}

En esta sección se describen las opciones de configuración avanzadas de los servicios OSGi que implementan el marco de informes.

Se pueden ver mediante el menú Configuration de la consola web (disponible en `http://localhost:4502/system/console/configMgr`, por ejemplo). AEM Al trabajar con los servicios de configuración, existen varios métodos para administrar los parámetros de configuración de dichos servicios; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

### Servicio básico (configuración de informes de CQ por día) {#basic-service-day-cq-reporting-configuration}

* **Timezone** define la zona horaria para la que se crean los datos históricos. Esto sirve para garantizar que el gráfico histórico muestre los mismos datos para cada usuario en todo el mundo.
* **Configuración regional** define la configuración regional que se utilizará con **Timezone** para datos históricos. La configuración regional se utiliza para determinar algunas configuraciones de calendario específicas de la configuración regional (por ejemplo, si el primer día de una semana es domingo o lunes).

* **Ruta de instantánea** define la ruta raíz en la que se almacenan las instantáneas de los gráficos históricos.
* **Ruta a los informes** define la ruta donde se encuentran los informes. El servicio de instantáneas lo utiliza para determinar los informes para los que se deben tomar instantáneas.
* **Instantáneas diarias** define la hora de cada día en la que se toman instantáneas diarias. La hora especificada está en la zona horaria local del servidor.
* **Instantáneas por hora** define el minuto de cada hora en el que se toman instantáneas por hora.
* **Filas (máximo)** define el número máximo de filas almacenadas para cada instantánea. Este valor debe elegirse razonablemente. Si es demasiado alto, esto afecta al tamaño del repositorio; si es demasiado bajo, es posible que los datos no sean precisos debido a la forma en que se gestionan los datos históricos.
* **Datos falsos**, si está activada, se pueden crear datos históricos falsos utilizando `fakedata` selector; si está desactivado, utilice el `fakedata` El selector de inicia una excepción.

  Como los datos son falsos, deben *solamente* se utilizará con fines de prueba y depuración.

  Uso del `fakedata` El selector de finaliza el informe de forma implícita, por lo que se pierden todos los datos existentes. Los datos se pueden restaurar manualmente, pero este puede ser un proceso laborioso.

* **Instantánea del usuario** define un usuario opcional que se puede utilizar para tomar instantáneas.

  Básicamente, las instantáneas se toman para el usuario que ha finalizado el informe. Puede haber situaciones (por ejemplo, en un sistema de publicación, en las que este usuario no exista porque su cuenta no se ha duplicado) en las que desee especificar un usuario de reserva que se utilice en su lugar.

  Además, especificar un usuario puede suponer un riesgo para la seguridad.

* **Forzar instantánea del usuario**, si está activada, todas las instantáneas se toman con el usuario especificado en *Instantánea del usuario*. Esto podría tener un impacto grave en la seguridad si no se gestiona correctamente.

### Configuración de caché (caché de informes de CQ de día) {#cache-settings-day-cq-reporting-cache}

* **Activar** permite habilitar o deshabilitar el almacenamiento en caché de los datos del informe. Al habilitar la caché de informes, se guardan los datos del informe en la memoria durante varias solicitudes. Esto puede mejorar el rendimiento, pero conlleva un mayor consumo de memoria y, en circunstancias extremas, puede provocar situaciones de falta de memoria.
* **TTL** define el tiempo (en segundos) durante el cual los datos del informe se almacenan en caché. Un número mayor aumenta el rendimiento, pero también puede devolver datos inexactos si los datos cambian dentro del período de tiempo.
* **Máximo de entradas** define el número máximo de informes que se almacenarán en caché al mismo tiempo.

>[!NOTE]
>
>Los datos del informe pueden ser diferentes para cada usuario e idioma. Por lo tanto, los datos del informe se almacenan en caché por informe, usuario e idioma. Esto significa que una **Máximo de entradas** valor de `2` almacena en caché los datos de:
>
>* un informe para dos usuarios con diferentes configuraciones de idioma
>* un usuario y dos informes
>
