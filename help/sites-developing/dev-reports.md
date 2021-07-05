---
title: Desarrollo de informes
seo-title: Desarrollo de informes
description: AEM ofrece una selección de informes estándar basados en un marco de informes
seo-description: AEM ofrece una selección de informes estándar basados en un marco de informes
uuid: 1b406d15-bd77-4531-84c0-377dbff5cab2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 50fafc64-d462-4386-93af-ce360588d294
exl-id: 3891150e-9972-4bbc-ad61-7f46a1f9bbb4
source-git-commit: 071bc0e36ed2d8eb4ce7bd0ba46823adc0e43095
workflow-type: tm+mt
source-wordcount: '5252'
ht-degree: 0%

---


# Desarrollo de informes {#developing-reports}

AEM ofrece una selección de [informes estándar](/help/sites-administering/reporting.md), la mayoría de los cuales se basan en un marco de informes.

Con el marco puede ampliar estos informes estándar o desarrollar sus propios informes completamente nuevos. El marco de informes se integra estrechamente con los conceptos y principios existentes de CQ5 para que los desarrolladores puedan usar sus conocimientos existentes de CQ5 como trampolín para desarrollar informes.

Para los informes estándar entregados con AEM:

* Estos informes se basan en el marco de informes:

   * [Informe de componentes](/help/sites-administering/reporting.md#component-report)
   * [Informe de actividad de la página](/help/sites-administering/reporting.md#page-activity-report)
   * [Informe del usuario](/help/sites-administering/reporting.md#user-report)
   * [Informe de instancia de flujo de trabajo](/help/sites-administering/reporting.md#workflow-instance-report)

* Los siguientes informes se basan en principios individuales y, por lo tanto, no se pueden ampliar:

   * [Uso del disco](/help/sites-administering/reporting.md#disk-usage)
   * [Comprobación de estado](/help/sites-administering/reporting.md#health-check)
   * [Informe de flujo de trabajo](/help/sites-administering/reporting.md#workflow-report)

>[!NOTE]
>
>El tutorial [Creación de su propio informe: un ejemplo](#creating-your-own-report-an-example) también muestra cuántos de los principios siguientes se pueden utilizar.
>
>También puede consultar los informes estándar para ver otros ejemplos de implementación.

>[!NOTE]
>
>En los ejemplos y definiciones que aparecen a continuación, se utiliza la notación siguiente:
>
>* Cada línea define un nodo o una propiedad donde:
   >  `N:<name> [<nodeType>]` : Describe un nodo con el nombre  `<*name*>` y el tipo de nodo de  `<*nodeType*>`*.*
   >  `P:<name> [<propertyType]` : Describe una propiedad con el nombre de  `<*name*>` y un tipo de propiedad de  `<*propertyType*>`.
   >  `P:<name> = <value>` : Describe una propiedad  `<name>` que debe establecerse en el valor de  `<value>`.
   >
   >
* La sangría muestra las dependencias jerárquicas entre los nodos.
>* Elementos separados por | denota una lista de posibles elementos; por ejemplo, tipos o nombres; p. ej. `String|String[]` significa que la propiedad puede ser String o String[].

   >
   >
* `[]` representa una matriz; como [] Cadenas o una matriz de nodos como en la  [Definición de consulta](#query-definition).
>
>
A menos que se indique lo contrario, los tipos predeterminados son:
>
>* Nodos: `nt:unstructured`
>* Propiedades - `String`


## Marco de informes {#reporting-framework}

El marco de presentación de informes se basa en los siguientes principios:

* Se basa completamente en conjuntos de resultados devueltos por una consulta ejecutada por CQ5 QueryBuilder.
* El conjunto de resultados define los datos mostrados en el informe. Cada fila del conjunto de resultados corresponde a una fila de la vista tabular del informe.
* Las operaciones disponibles para la ejecución en el conjunto de resultados se asemejan a los conceptos de RDBMS; principalmente *agrupación* y *agregación*.

* La mayoría de la recuperación y el procesamiento de los datos se realizan en el servidor.
* El cliente es el único responsable de mostrar los datos preprocesados. Solo las tareas de procesamiento menores (por ejemplo, la creación de vínculos en el contenido de la celda) se ejecutan en el lado del cliente.

El marco de informes (ilustrado por la estructura de un informe estándar) utiliza los siguientes componentes básicos, alimentados por la cola de procesamiento:

![chlimage_1-248](assets/chlimage_1-248.png)

### Página Informe {#report-page}

La página del informe:

* Es una página estándar de CQ5.
* Se basa en una [plantilla CQ5 estándar, configurada para el informe](#report-template).

### Base de informes {#report-base}

El [ `reportbase` componente](#report-base-component) forma la base de cualquier informe tal como:

* Contiene la definición de la [consulta](#the-query-and-data-retrieval) que proporciona el conjunto de resultados subyacente de los datos.

* Es un sistema de párrafos adaptado que contendrá todas las columnas ( `columnbase`) agregadas al informe.
* Define qué tipos de gráficos están disponibles y cuáles están activos actualmente.
* Define el cuadro de diálogo Editar, que permite al usuario configurar ciertos aspectos del informe.

### Base de columna {#column-base}

Cada columna es una instancia del [ `columnbase` componente](#column-base-component) que:

* Es un párrafo, utilizado por el parsys ( `reportbase`) del informe correspondiente.
* Define el vínculo al [conjunto de resultados subyacente](#the-query-and-data-retrieval); es decir, define los datos específicos a los que se hace referencia dentro de este conjunto de resultados y cómo se procesa.
* Contiene definiciones adicionales; como los agregados y filtros disponibles, junto con cualquier valor predeterminado.

### Consulta y recuperación de datos {#the-query-and-data-retrieval}

La consulta:

* Se define como parte del componente [ `reportbase`](#report-base) .
* Se basa en [CQ QueryBuilder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html).
* Recupera los datos utilizados como base del informe. Cada fila del conjunto de resultados (tabla) está vinculada a un nodo como devuelve la consulta. A continuación, se extrae información específica para [columnas individuales](#column-base-component) de este conjunto de datos.

* Normalmente consta de:

   * Una ruta raíz.

      Esto especifica el subárbol del repositorio que se va a buscar.

      Para ayudar a minimizar el impacto en el rendimiento, es aconsejable (intentar) restringir la consulta a un sub-árbol específico del repositorio. La ruta raíz puede predefinirse en la [plantilla de informe](#report-template) o configurarse por el usuario en el cuadro de diálogo [Configuración (Editar)](#configuration-dialog).

   * [Uno o más criterios](#query-definition).

      Se imponen para producir el conjunto de resultados (inicial); incluyen, por ejemplo, restricciones en el tipo de nodo o restricciones de propiedad.

**El punto clave aquí es que cada nodo individual devuelto en el conjunto de resultados de la consulta se utiliza para generar una sola fila en el informe (así que una relación 1:1).**

El desarrollador debe asegurarse de que la consulta definida para un informe devuelva un conjunto de nodos apropiado para ese informe. Sin embargo, el nodo en sí no necesita contener toda la información necesaria, sino que también puede derivarse de nodos principales y/o secundarios. Por ejemplo, la consulta utilizada para el [Informe de usuario](/help/sites-administering/reporting.md#user-report) selecciona los nodos en función del tipo de nodo (en este caso `rep:user`). Sin embargo, la mayoría de las columnas de este informe no toman sus datos directamente de estos nodos, sino de los nodos secundarios `profile`.

### Cola de procesamiento {#processing-queue}

La [consulta](#the-query-and-data-retrieval) devuelve un conjunto de datos de resultado que se mostrará como filas en el informe. Cada fila del conjunto de resultados se procesa (del lado del servidor) en [varias fases](#phases-of-the-processing-queue), antes de transferirse al cliente para que se muestre en el informe.

Esto permite:

* Extraer y derivar valores del conjunto de resultados subyacente.

   Por ejemplo, le permite procesar dos valores de propiedad como un solo valor calculando la diferencia entre los dos.

* Resolver valores extraídos; esto se puede hacer de varias maneras.

   Por ejemplo, las rutas se pueden asignar a un título (como en el contenido más legible en lenguaje natural de la propiedad *jcr:title* correspondiente).

* Aplicación de filtros en varios puntos.
* Crear valores compuestos, si es necesario.

   Por ejemplo, consiste en un texto que se muestra al usuario, un valor que se utiliza para ordenar y una URL adicional que se utiliza (en el lado del cliente) para crear un vínculo.

#### Flujo de trabajo de la cola de procesamiento {#workflow-of-the-processing-queue}

El siguiente flujo de trabajo representa la cola de procesamiento:

![chlimage_1-249](assets/chlimage_1-249.png)

#### Fases de la cola de procesamiento {#phases-of-the-processing-queue}

Donde los pasos y elementos detallados son:

1. Transforma los resultados devueltos por la [consulta inicial (reportbase)](#query-definition) en el conjunto de resultados básico mediante extractores de valores.

   Los extractores de valores se eligen automáticamente según el [tipo de columna](#column-specific-definitions). Se utilizan para leer valores de la consulta JCR subyacente y crear un conjunto de resultados a partir de ellos; después de lo cual podrá aplicarse un nuevo tratamiento. Por ejemplo, para el tipo `diff`, el extractor de valores lee dos propiedades, calcula el valor único que se agrega al conjunto de resultados. Los extractores de valores no se pueden configurar.

1. A ese conjunto de resultados inicial, que contiene datos sin procesar, se aplica [filtro inicial](#column-specific-definitions) (*fase sin procesar*).

1. Los valores son [preprocesados](#processing-queue); tal como se define para la fase *apply*.

1. [El filtrado](#column-specific-definitions)  (asignado a la fase  ** preprocesada) se ejecuta en los valores preprocesados.

1. Los valores se resuelven; según la resolución [definida](#processing-queue).
1. [El filtrado](#column-specific-definitions)  (asignado a la fase  ** resuelta) se ejecuta en los valores resueltos.

1. Los datos se [agrupan y agregan](#column-specific-definitions).
1. Los datos de matriz se resuelven convirtiéndolos en una lista (basada en cadenas).

   Se trata de un paso implícito que convierte un resultado de varios valores en una lista que se puede mostrar; es necesario para valores de celda (no agregados) basados en propiedades JCR de varios valores.

1. Los valores se vuelven a [preprocesar](#processing-queue); tal como se define para la fase *afterApply* .

1. Los datos se ordenan.
1. Los datos procesados se transfieren al cliente.

>[!NOTE]
>
>La consulta inicial que devuelve el conjunto de resultados de datos base se define en el componente `reportbase` .
>
>Otros elementos de la cola de procesamiento se definen en los componentes `columnbase` .

## Construcción y configuración de informes {#report-construction-and-configuration}

Para construir y configurar un informe es necesario lo siguiente:

* una [ubicación para la definición de los componentes del informe](#location-of-report-components)
* un [ `reportbase` componente](#report-base-component)
* uno o más componentes [ `columnbase`](#column-base-component)
* un [componente de página](#page-component)
* a [diseño de informe](#report-design)
* a [plantilla de informe](#report-template)

### Ubicación de los componentes del informe {#location-of-report-components}

Los componentes de informes predeterminados se encuentran en `/libs/cq/reporting/components`.

Sin embargo, se recomienda no actualizar estos nodos, pero crear sus propios nodos de componentes en `/apps/cq/reporting/components` o si es más apropiado `/apps/<yourProject>/reports/components`.

Donde (por ejemplo):

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
```

En esta sección, se crea la raíz para el informe y, en esta, el componente base del informe y los componentes de la columna base:

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
                N:<reportname> [sling:Folder]
                        N:<reportname> [cq:Component]  // report base component
                        N:<columnname> [cq:Component]  // column base component
```

### Componente de página {#page-component}

Una página de informe debe utilizar el `sling:resourceType` de `/libs/cq/reporting/components/reportpage`.

No debe ser necesario un componente de página personalizado (en la mayoría de los casos).

## Componente de base de informes {#report-base-component}

Cada tipo de informe requiere un componente de contenedor derivado de `/libs/cq/reporting/components/reportbase`.

Este componente actúa como contenedor del informe en su conjunto y proporciona información para:

* La [definición de consulta](#query-definition).
* Un [ (opcional) diálogo](#configuration-dialog) para configurar el informe.
* Cualquier [gráfico](#chart-definitions) integrado en el informe.

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

   Se puede utilizar para limitar el conjunto de resultados a nodos que tengan propiedades específicas con valores específicos. Si se especifican varias restricciones, el nodo debe satisfacer todas ellas (operación AND).

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

   Devolvería todos los componentes `textimage` que el usuario `admin` modificó por última vez.

* `nodeTypes`

   Se utiliza para limitar el conjunto de resultados a los tipos de nodo especificados. Se pueden especificar varios tipos de nodos.

* `mandatoryProperties`

   Se puede utilizar para limitar el conjunto de resultados a nodos que tengan *todos* de las propiedades especificadas. No se tiene en cuenta el valor de las propiedades.

Todas son opcionales y se pueden combinar según sea necesario, pero debe definir al menos una de ellas.

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

   Contiene definiciones para los gráficos activos.

   * `active`

      Como se pueden definir varias opciones de configuración, puede utilizarlas para definir cuáles están activas actualmente. Estos se definen mediante una matriz de nodos (no existe ninguna convención de nombres obligatoria para estos nodos, pero los informes estándar suelen utilizar `0`, `1`. `x`), cada una con la siguiente propiedad:

      * `id`

         Identificación de los gráficos activos. Debe coincidir con el id de uno de los gráficos `definitions`.

* `definitions`

   Define los tipos de gráficos que están disponibles para el informe. La `definitions` que se va a usar la especificará la configuración de `active`.

   Las definiciones se especifican utilizando una matriz de nodos (también denominada `0`, `1`. `x`), cada uno con las siguientes propiedades:

   * `id`

      La identificación del gráfico.

   * `type`

      Tipo de gráfico disponible. Seleccione entre:

      * `pie`
Gráfico circular. Generado solo a partir de datos actuales.

      * `lineseries`
Serie de líneas (puntos de conexión que representan las instantáneas reales). Generado solo a partir de datos históricos.
   * Hay propiedades adicionales disponibles, según el tipo de gráfico:

      * para el tipo de gráfico `pie`:

         * `maxRadius` ( `Double/Long`)

            El radio máximo permitido para el gráfico circular; por lo tanto, el tamaño máximo permitido para el gráfico (sin leyenda). Se omite si `fixedRadius` está definido.

         * `minRadius` (  `Double/Long`)

            El radio mínimo permitido para el gráfico circular. Se omite si `fixedRadius` está definido.

         * `fixedRadius` (  `Double/Long`) Define un radio fijo para el gráfico circular.
      * para el tipo de gráfico [`lineseries`](/help/sites-administering/reporting.md#display-limits):

         * `totals` (  `Boolean`)

            True si se debe mostrar una línea adicional que muestre el **Total**.
predeterminada: `false`

         * `series` (  `Long`)

            Número de líneas/series que se van a mostrar.
predeterminado: `9` (también es el máximo permitido)

         * `hoverLimit` (  `Long`)

            Número máximo de instantáneas agregadas (puntos mostrados en cada línea horizontal, que representan valores distintos) para las que se deben mostrar ventanas emergentes, es decir, cuando el usuario pasa el ratón sobre un valor distinto o etiqueta correspondiente en la leyenda del gráfico.

            predeterminado: `35` (es decir, no se muestran ventanas emergentes si se aplican más de 35 valores distintos a la configuración actual del gráfico).

            Hay un límite adicional de 10 ventanas emergentes que se pueden mostrar en paralelo (se pueden mostrar varias ventanas emergentes cuando se pasa el ratón sobre los textos de la leyenda).



### Cuadro de diálogo Configuración {#configuration-dialog}

Cada informe puede tener un cuadro de diálogo de configuración, que permite al usuario especificar varios parámetros para el informe. Se puede acceder a este cuadro de diálogo a través del botón **Edit** cuando la página del informe está abierta.

Este cuadro de diálogo es un cuadro de diálogo estándar CQ [](/help/sites-developing/components-basics.md#dialogs) y se puede configurar como tal (consulte [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog) para obtener más información).

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

Se proporcionan varios componentes preconfigurados; se puede hacer referencia a estas variables en el cuadro de diálogo, utilizando la propiedad `xtype` con un valor de `cqinclude`:

* **`title`**

   `/libs/cq/reporting/components/commons/title`

   Campo de texto para definir el título del informe.

* **`description`**

   `/libs/cq/reporting/components/commons/description`

   Área de texto para definir la descripción del informe.

* **`processing`**

   `/libs/cq/reporting/components/commons/processing`

   Selector del modo de procesamiento del informe (carga manual/automática de datos).

* **`scheduling`**

   `/libs/cq/reporting/components/commons/scheduling`

   Selector para programar instantáneas para el gráfico histórico.

>[!NOTE]
>
>Los componentes a los que se hace referencia deben incluirse mediante el sufijo `.infinity.json` (consulte el ejemplo anterior).

### Ruta de acceso raíz {#root-path}

Además, se puede definir una ruta raíz para el informe:

* **`rootPath`**

   Esto limita el informe a una determinada sección (árbol o subárbol) del repositorio, que se recomienda para la optimización del rendimiento. La ruta raíz se especifica mediante la propiedad `rootPath` del nodo `report` de cada página del informe (tomada de la plantilla al crearla).

   Se puede especificar mediante:

   * la [plantilla de informe](#report-template) (como valor fijo o como valor predeterminado para el cuadro de diálogo de configuración).
   * el usuario (con este parámetro)

## Componente de base de columna {#column-base-component}

Cada tipo de columna requiere un componente derivado de `/libs/cq/reporting/components/columnbase`.

Un componente de columna define una combinación de lo siguiente:

* La configuración [Consulta específica de columna](#column-specific-query).
* [Resuelven y preprocesa](#resolvers-and-preprocessing).
* Las [Definiciones Específicas de Columna](#column-specific-definitions) (como filtros y agregados; `definitions` nodo secundario).
* [Valores predeterminados de columna](#column-default-values).
* El [filtro de cliente](#client-filter) para extraer la información que se mostrará de los datos que devuelve el servidor.
* Además, un componente de columna debe proporcionar una instancia adecuada de `cq:editConfig`. para definir los [Eventos y acciones](#events-and-actions) necesarios.
* La configuración para [columnas genéricas](#generic-columns).

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

Esto define la extracción de datos específica (del [conjunto de resultados de datos del informe](#the-query-and-data-retrieval)) para su uso en la columna individual.

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

   Si la propiedad se define como String[] se analizan varias propiedades (en secuencia) para encontrar el valor real.

   Por ejemplo, en el caso de:

   `property = [ "jcr:lastModified", "jcr:created" ]`

   El extractor de valor correspondiente (que está en control aquí):

   * Compruebe si hay una propiedad jcr:lastModified disponible y, si es así, utilícela.
   * Si no hay ninguna propiedad jcr:lastModified disponible, se usará el contenido de jcr:created en su lugar.

* `subPath`

   Si el resultado no está ubicado en el nodo devuelto por la consulta, `subPath` define dónde se encuentra realmente la propiedad.

* `secondaryProperty`

   Define una segunda propiedad que también debe utilizarse para calcular el valor de celda real; solo se utilizará para determinados tipos de columna (diff y ordenable).

   Por ejemplo, en el caso del informe de instancias de flujo de trabajo, la propiedad especificada se utiliza para almacenar el valor real de la diferencia de tiempo (en milisegundos) entre las horas de inicio y finalización.

* `secondarySubPath`

   Similar a subPath, cuando se utiliza `secondaryProperty`.

En la mayoría de los casos, solo se utilizará `property`.

### Filtro de cliente {#client-filter}

El filtro cliente extrae la información que se va a mostrar de los datos que devuelve el servidor.

>[!NOTE]
>
>Este filtro se ejecuta en el lado del cliente después de aplicar todo el procesamiento en el lado del servidor.

```xml
N:definitions
    N:data
        P:clientFilter [String]
```

`clientFilter` se define como una función de JavaScript que:

* como entrada, recibe un parámetro; los datos devueltos por el servidor (completamente preprocesados)
* como resultado, devuelve el valor filtrado (procesado); los datos extraídos o derivados de la información de entrada

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

La [cola de procesamiento](#processing-queue) define los distintos solucionadores y configura el preprocesamiento:

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

   Define la resolución que se va a utilizar. Están disponibles los siguientes resolventes:

   * `const`

      Asigna valores a otros valores; por ejemplo, esto se utiliza para resolver constantes como `en` a su valor equivalente `English`.

   * `default`

      Resolución predeterminada. Esta es una resolución ficticia que en realidad no resuelve nada.

   * `page`

      Resuelve un valor de ruta a la ruta de la página adecuada; más precisamente, al nodo `jcr:content` correspondiente. Por ejemplo, `/content/.../page/jcr:content/par/xyz` se resuelve en `/content/.../page/jcr:content`.

   * `path`

      Resuelve un valor de ruta añadiendo opcionalmente una subruta y tomando el valor real de una propiedad del nodo (como se define en `resolverConfig`) en la ruta resuelta. Por ejemplo, se puede resolver un `path` de `/content/.../page/jcr:content` en el contenido de la propiedad `jcr:title`, lo que significaría que una ruta de página se resuelve en el título de la página.

   * `pathextension`

      Resuelve un valor anteponiendo una ruta y tomando el valor real de una propiedad del nodo en la ruta resuelta. Por ejemplo, un valor `de` puede ir precedido de una ruta como `/libs/wcm/core/resources/languages`, tomando el valor de la propiedad `language`, para resolver el código de país `de` en la descripción de idioma `German`.

* `resolverConfig`

   Proporciona definiciones para la resolución; las opciones disponibles dependen del `resolver` seleccionado:

   * `const`

      Utilice propiedades para especificar las constantes que se deben resolver. El nombre de la propiedad define la constante que se va a resolver. el valor de la propiedad define el valor resuelto.

      Por ejemplo, una propiedad con **Name**= `1` y **Value** `=One` resolverá 1 en Uno.

   * `default`

      No hay ninguna configuración disponible.

   * `page`

      * `propertyName` (opcional)

         Define el nombre de la propiedad que debe utilizarse para resolver el valor. Si no se especifica, se utiliza el valor predeterminado *jcr:title* (el título de la página); para la resolución `page`, esto significa que primero la ruta se resuelve en la ruta de página y, a continuación, se resuelve en el título de la página.
   * `path`

      * `propertyName` (opcional)

         Especifica el nombre de la propiedad que debe utilizarse para resolver el valor. Si no se especifica, se utiliza el valor predeterminado de `jcr:title`.

      * `subPath` (opcional)

         Esta propiedad se puede utilizar para especificar un sufijo que se anexará a la ruta antes de que se resuelva el valor.
   * `pathextension`

      * `path` (obligatorio)

         Define la ruta que se va a anteponer.

      * `propertyName` (obligatorio)

         Define la propiedad en la ruta resuelta donde se encuentra el valor real.

      * `i18n` (opcional; type Boolean)

         Determina si el valor resuelto debe estar *internacionalizado* (es decir, usar los [servicios de internacionalización de CQ5](/help/sites-administering/tc-manage.md)).



* `preprocessing`

   El preprocesamiento es opcional y puede enlazarse (por separado) a las fases de procesamiento *apply* o *applyAfter*:

   * `apply`

      La fase de preprocesamiento inicial ([paso 3 en la representación de la cola de procesamiento](#processing-queue)).

   * `applyAfter`

      Se aplica después del preprocesamiento ([paso 9 en la representación de la cola de procesamiento](#processing-queue)).

#### Resueltos {#resolvers}

Los resolventes se utilizan para extraer la información necesaria. Algunos ejemplos de los diferentes resolventes son:

**Const**

Lo siguiente resolverá un valor de contenido de `VersionCreated` en la cadena `New version created`.

Consulte `/libs/cq/reporting/components/auditreport/typecol/definitions/data`.

```xml
N:data
    P:resolver=const
    N:resolverConfig
        P:VersionCreated="New version created"
```

**Página**

Resuelve un valor de ruta a la propiedad jcr:description en el nodo jcr:content (secundario) de la página correspondiente.

Consulte `/libs/cq/reporting/components/compreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=page
    N:resolverConfig
        P:propertyName="jcr:description"
```

**Ruta**

Lo siguiente resuelve una ruta de `/content/.../page` al contenido de la propiedad `jcr:title`, lo que significa que una ruta de página se resuelve en el título de la página.

Consulte `/libs/cq/reporting/components/auditreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=path
    N:resolverConfig
        P:propertyName="jcr:title"
        P:subPath="/jcr:content"
```

**Extensión de ruta**

El siguiente antepone un valor `de` con la extensión de ruta `/libs/wcm/core/resources/languages` y luego toma el valor de la propiedad `language` para resolver el código de país `de` a la descripción de idioma `German`.

Consulte `/libs/cq/reporting/components/userreport/languagecol/definitions/data`.

```xml
N:data
    P:resolver=pathextension
    N:resolverConfig
        P:path="/libs/wcm/core/resources/languages"
        P:propertyName="language"
```

#### Preprocesamiento {#preprocessing}

La definición `preprocessing` puede aplicarse a:

* valor original:

   La definición de preprocesamiento del valor original se especifica en `apply` o `applyAfter` directamente.

* en el estado agregado:

   Si es necesario, se puede proporcionar una definición separada para cada agregación.

   Para especificar un preprocesamiento explícito para los valores agregados, las definiciones de preprocesamiento deben residir en un nodo `aggregated` secundario correspondiente ( `apply/aggregated`, `applyAfter/aggregated`). Si se requiere un preprocesamiento explícito para agregados distintos, la definición de preprocesamiento se encuentra en un nodo secundario con el nombre del acumulado respectivo (por ejemplo `apply/aggregated/min/max` u otros agregados).

Puede especificar una de las siguientes opciones para utilizarla durante el procesamiento previo:

* [buscar y reemplazar ](#preprocessing-find-and-replace-patterns)
patronesCuando se encuentran, el patrón especificado (que se define como expresión regular) se reemplaza por otro patrón; por ejemplo, se puede utilizar para extraer una subcadena del original.

* [formateadores de tipo de datos](#preprocessing-data-type-formatters)

   Convierte un valor numérico en una cadena relativa; por ejemplo, el valor &quot;que representa una diferencia de tiempo de 1 hora se resolvería en una cadena como `1:24PM (1 hour ago)`.

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

Para el preprocesamiento, puede especificar un `pattern` (definido como una [expresión regular](https://en.wikipedia.org/wiki/Regular_expression) o regex) que se encuentre y luego sustituirlo por el patrón `replace`:

* `pattern`

   Expresión regular utilizada para localizar una subcadena.

* `replace`

   La cadena, o representación de la cadena, que se utilizará como reemplazo de la cadena original. A menudo esto representa una subcadena de la cadena ubicada por la expresión regular `pattern`.

Un ejemplo de reemplazo puede desglosarse como:

* Para el nodo `definitions/data/preprocessing/apply` con las dos propiedades siguientes:

   * `pattern`: `(.*)(/jcr:content)(/|$)(.*)`
   * `replace`:  `$1`

* Una cadena que llega como:

   * `/content/geometrixx/en/services/jcr:content/par/text`

* Se dividirá en cuatro secciones:

   * `$1` - `(.*)` - `/content/geometrixx/en/services`
   * `$2` -  `(/jcr:content)` -  `/jcr:content`
   * `$3` -  `(/|$)` -  `/`
   * `$4` -  `(.*)` -  `par/text`

* Y reemplazado por la cadena representada por `$1`:

   * `/content/geometrixx/en/services`

#### Preprocesamiento: tipo de datos para asuntos {#preprocessing-data-type-formatters}

Estos formateadores convierten un valor numérico en una cadena relativa.

Por ejemplo, esto se puede utilizar para una columna de tiempo que permita agregados `min`, `avg` y `max`. Como los agregados `min`/ `avg`/ `max` se muestran como una *diferencia horaria* (p. ej. `10 days ago`), requieren un formateador de datos. Para ello, se aplica un formateador `datedelta` a los valores agregados `min`/ `avg`/ `max`. Si también está disponible un agregado `count`, no es necesario un formateador, ni el valor original.

Actualmente, los formatos de tipo de datos disponibles son:

* `format`

   Formato de tipo de datos:

   * `duration`

      Duración es el lapso de tiempo entre dos fechas definidas. Por ejemplo, el inicio y el final de una acción de flujo de trabajo que tardó 1 hora, desde el 13/2/11 a las 11:23h y hasta el final una hora después a las 13/2/11 a las 12:23h.

      Convierte un valor numérico (interpretado como milisegundos) en una cadena de duración; por ejemplo, `30000` tiene el formato * `30s`.*

   * `datedelta`

      Datadelta es el lapso de tiempo entre una fecha del pasado y &quot;ahora&quot; (por lo que tendrá un resultado diferente si el informe se ve en un momento posterior).

      Convierte el valor numérico (interpretado como una diferencia horaria en días) en una cadena de fecha relativa. Por ejemplo, 1 tiene el formato de hace 1 día.

El siguiente ejemplo define el formato `datedelta` para los agregados `min` y `max`:

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

### Definiciones específicas de columnas {#column-specific-definitions}

Las definiciones específicas de la columna definen los filtros y agregados disponibles para esa columna.

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

      Se utiliza para extraer partes de una fecha necesaria para la agregación (por ejemplo, grupo por año para obtener datos agregados para cada año).

   * `sortable`

      Se utiliza para valores que utilizan valores diferentes (tomados de propiedades diferentes) para la ordenación y visualización.
   Además, cualquiera de los anteriores puede definirse como multivalor; por ejemplo, `string[]` define una matriz de cadenas.

   El tipo de columna elige el extractor de valores. Si hay un extractor de valores disponible para un tipo de columna, se utilizará este extractor. De lo contrario, se utiliza el extractor de valor predeterminado.

   Un tipo puede (opcionalmente) tomar un parámetro. Por ejemplo, `timeslot:year` extrae el año de un campo de fecha. Tipos con sus parámetros:

   * `timeslot` - Los valores son comparables a las constantes correspondientes de  `java.utils.Calendar`.

      * `timeslot:year` - `Calendar.YEAR`
      * `timeslot:month-of-year` -  `Calendar.MONTH`
      * `timeslot:week-of-year` -  `Calendar.WEEK_OF_YEAR`
      * `timeslot:day-of-month` -  `Calendar.DAY_OF_MONTH`
      * `timeslot:day-of-week` -  `Calendar.DAY_OF_WEEK`
      * `timeslot:day-of-year` -  `Calendar.DAY_OF_YEAR`
      * `timeslot:hour-of-day` -  `Calendar.HOUR_OF_DAY`
      * `timeslot:minute-of-hour` -  `Calendar.MINUTE`


* `groupable`

   Define si el informe se puede agrupar por esta columna.

* `filters`

   Definiciones del filtro.

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

      Nombre textual del agregado. Si no se especifica `text`, entonces tomará la descripción predeterminada del agregado; por ejemplo, `minimum` se utilizará para el agregado `min`.

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

         Toma el percentil 95 de todos los valores.

### Valores predeterminados de columna {#column-default-values}

Se utiliza para definir los valores predeterminados de la columna :

```xml
N:defaults
    P:aggregate
```

* `aggregate`

   Los valores válidos `aggregate` son los mismos que para `type` en `aggregates` (consulte [Definiciones específicas de columnas (definiciones - filtros / agregados)](#column-specific-definitions) ).

### Eventos y acciones {#events-and-actions}

Editar configuración define los eventos necesarios para que los oyentes detecten y las acciones que se aplicarán después de que se produzcan esos eventos. Consulte la [introducción al desarrollo de componentes](/help/sites-developing/components.md) para obtener información general.

Se deben definir los siguientes valores para garantizar que todas las acciones necesarias estén cubiertas para:

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

Las columnas genéricas son una extensión en la que (la mayoría de) las definiciones de columna se almacenan en la instancia del nodo de columna (en lugar del nodo de componente).

Utilizan un cuadro de diálogo (estándar), que personaliza, para el componente genérico individual. Este cuadro de diálogo permite que el usuario del informe defina las propiedades de columna de una columna genérica en la página del informe (mediante la opción de menú **Propiedades de columna...**).

Un ejemplo es la columna **Generic** del **User Report**; consulte `/libs/cq/reporting/components/userreport/genericcol`.

Para que una columna sea genérica:

* Establezca la propiedad `type` del nodo `definition` de la columna en `generic`.

   Consulte `/libs/cq/reporting/components/userreport/genericcol/definitions`

* Especifique una definición de cuadro de diálogo (estándar) en el nodo `definition` de la columna.

   Consulte `/libs/cq/reporting/components/userreport/genericcol/definitions/dialog`

   * Los campos del cuadro de diálogo deben hacer referencia a los mismos nombres que la propiedad del componente correspondiente (incluida su ruta).

      Por ejemplo, si desea que el tipo de columna genérica se pueda configurar a través del cuadro de diálogo, utilice un campo con el nombre `./definitions/type`.

   * Las propiedades definidas con la IU/cuadro de diálogo tienen prioridad sobre las definidas en el componente `columnbase`.

* Defina la Configuración de edición.

   Consulte `/libs/cq/reporting/components/userreport/genericcol/cq:editConfig`

* Utilice metodologías de AEM estándar para definir propiedades de columna (adicionales).

   Tenga en cuenta que para las propiedades definidas en las instancias de componente y columna, el valor de la instancia de columna tiene prioridad.

   Las propiedades disponibles para una columna genérica son:

   * `jcr:title` - nombre de columna
   * `definitions/aggregates` - agregados
   * `definitions/filters` - filtros
   * `definitions/type`: tipo de columna (debe definirse en el cuadro de diálogo, ya sea mediante un selector/combobox o un campo oculto)
   * `definitions/data/resolver` y  `definitions/data/resolverConfig` (pero no  `definitions/data/preprocessing` o  `.../clientFilter`): la resolución y la configuración
   * `definitions/queryBuilder` - la configuración del generador de consultas
   * `defaults/aggregate` - el agregado predeterminado

   En el caso de una nueva instancia de la columna genérica del **Informe de usuario**, las propiedades definidas con el cuadro de diálogo se mantienen en:

   `/etc/reports/userreport/jcr:content/report/columns/genericcol/settings/generic`

## Diseño de informes {#report-design}

El diseño define qué tipos de columnas están disponibles para crear un informe. También define el sistema de párrafos al que se añaden las columnas.

Se recomienda crear un diseño individual para cada informe. Esto garantiza una flexibilidad total. Consulte también [Definición del nuevo informe](#defining-your-new-report).

Los componentes de informes predeterminados se encuentran en `/etc/designs/reports`.

La ubicación de los informes puede depender de la ubicación de los componentes:

* `/etc/designs/reports/<yourReport>` es adecuado si el informe se encuentra en  `/apps/cq/reporting`

* `/etc/designs/<yourProject>/reports/<*yourReport*>` para informes que utilizan el  `/apps/<yourProject>/reports` patrón

Las propiedades de diseño requeridas se registran en `jcr:content/reportpage/report/columns` (por ejemplo, `/etc/designs/reports/<reportName>/jcr:content/reportpage/report/columns`):

* `components`

   Cualquier componente o grupo de componentes permitidos en el informe.

* `sling:resourceType`

   Propiedad con valor `cq/reporting/components/repparsys`.

Un ejemplo de fragmento de diseño (tomado del diseño del informe de componentes) es:

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
>Se recomienda no realizar ningún cambio en los diseños de informe estándar. Esto sirve para garantizar que no se pierdan los cambios al actualizar o instalar revisiones.
>
>Copie el informe y su diseño si desea personalizar un informe estándar.

>[!NOTE]
>
>Las columnas predeterminadas se pueden crear automáticamente cuando se crea un informe. Se especifican en la plantilla.

## Plantilla de informe {#report-template}

Cada tipo de informe debe proporcionar una plantilla. Son [Plantillas de CQ](/help/sites-developing/templates.md) estándar y se pueden configurar como tales.

La plantilla debe:

* establezca `sling:resourceType` en `cq/reporting/components/reportpage`

* indicar el diseño que se va a utilizar
* cree un nodo secundario `report` que haga referencia al componente contenedor ( `reportbase`) mediante la propiedad `sling:resourceType`

Un ejemplo de fragmento de plantilla (tomado de la plantilla de informe del componente) es:

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

Un ejemplo de fragmento de plantilla que muestra la definición de la ruta raíz (tomada de la plantilla de informe del usuario) es:

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

Las plantillas de informes predeterminadas se mantienen en `/libs/cq/reporting/templates`.

Sin embargo, se recomienda no actualizar estos nodos, pero crear sus propios nodos de componentes en `/apps/cq/reporting/templates` o si es más apropiado `/apps/<yourProject>/reports/templates`.

Donde, como ejemplo (consulte también [Ubicación de los componentes del informe](#location-of-report-components)):

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
```

En esto, cree la raíz para la plantilla:

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
                N:<reportname> [sling:Folder]
```

## Creación De Su Propio Informe: Un Ejemplo {#creating-your-own-report-an-example}

### Definición del nuevo informe {#defining-your-new-report}

Para definir un nuevo informe debe crear y configurar:

1. La raíz de los componentes del informe.
1. El componente base del informe.
1. Uno o más componentes básicos de columna.
1. El diseño del informe.
1. La raíz de la plantilla de informe.
1. La plantilla del informe.

Para ilustrar estos pasos, el siguiente ejemplo define un informe que enumera todas las configuraciones de OSGi dentro del repositorio; es decir, todas las instancias del nodo `sling:OsgiConfig`.

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

1. Defina la base de informes. Por ejemplo, `osgireport[cq:Component]` en `/apps/cq/reporting/components/osgireport`.

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

   Esto define un componente base de informe que:

   * busca todos los nodos de tipo `sling:OsgiConfig`
   * muestra los gráficos `pie` y `lineseries`
   * proporciona un cuadro de diálogo para que el usuario configure el informe

1. Defina el primer componente de columna (base de columnas). Por ejemplo, `bundlecol[cq:Component]` en `/apps/cq/reporting/components/osgireport`.

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

   Esto define un componente base de columna que:

   * busca y devuelve el valor que recibe del servidor; en este caso, la propiedad `jcr:path` para cada nodo `sling:OsgiConfig`
   * proporciona el agregado `count`
   * no es agrupable
   * tiene el título `Bundle` (título de columna dentro de la tabla)
   * está en el grupo de la barra de tareas `OSGi Report`
   * se actualiza en eventos especificados

   >[!NOTE]
   >
   >En este ejemplo no hay definiciones de `N:data` y `P:clientFilter`. Esto se debe a que el valor recibido del servidor se devuelve 1:1, que es el comportamiento predeterminado.
   >
   >Esto es lo mismo que las definiciones:
   >
   >
   ```
   >N:data [nt:unstructured]
   >   P:clientFilter [String] = "function(v) { return v; }"
   >```
   >
   >Cuando la función simplemente devuelve el valor que recibe.

1. Defina el diseño del informe. Por ejemplo, `osgireport[cq:Page]` en `/etc/designs/reports`.

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

1. Defina la plantilla del informe. Por ejemplo, `osgireport[cq:Template]` en `/apps/cq/reporting/templates`.

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

   * define el `allowedPaths` para los informes resultantes: en el caso anterior, en cualquier lugar bajo `/etc/reports`
   * proporciona títulos y descripciones para la plantilla
   * proporciona una imagen en miniatura para utilizarla en la lista de plantillas (la definición completa de este nodo no aparece enumerada anteriormente; lo más fácil es copiar una instancia de thumbnail.png de un informe existente).

### Creación de una instancia del nuevo informe {#creating-an-instance-of-your-new-report}

Ahora se puede crear una instancia del nuevo informe:

1. Abra la consola **Tools**.

1. Seleccione **Informes** en el panel izquierdo.
1. Luego **Nuevo...** de la barra de herramientas. Defina un **Título** y **Nombre**, seleccione el nuevo tipo de informe (la **Plantilla de informe OSGi**) en la lista de plantillas y haga clic en **Crear**.
1. La nueva instancia del informe aparecerá en la lista. Haga doble clic en esto para abrirlo.
1. Arrastre un componente (por ejemplo, **Paquete** en el grupo **Informe OSGi**) desde la barra de tareas para crear la primera columna y [iniciar la definición del informe](/help/sites-administering/reporting.md#the-basics-of-report-customization).

   >[!NOTE]
   >
   >Como este ejemplo no tiene columnas agrupables, los gráficos no estarán disponibles. Para ver gráficos, establezca `groupable` en `true`:
   >
   >
   ```
   >N:osgireport [sling:Folder]
   > N:bundlecol [cq:Component]
   > N:definitions [nt:unstructured]
   > P:groupable [Boolean] = true
   >```

## Configuración de los servicios del marco de informes {#configuring-the-report-framework-services}

En esta sección se describen las opciones de configuración avanzadas para los servicios OSGi que implementan el marco de trabajo del informe.

Se pueden ver mediante el menú Configuración de la consola web (disponible por ejemplo en `http://localhost:4502/system/console/configMgr`). Al trabajar con AEM hay varios métodos para administrar los ajustes de configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

### Servicio básico (Configuración de informes Day CQ) {#basic-service-day-cq-reporting-configuration}

* **** La zona horaria define los datos históricos de zona horaria para los que se crean. Esto sirve para garantizar que el gráfico histórico muestre los mismos datos para cada usuario de todo el mundo.
* **** Localedefine la configuración regional que se utilizará junto con el  **** Lapso de tiempo para los datos históricos. La configuración regional se utiliza para determinar algunas configuraciones de calendario específicas de la configuración regional (por ejemplo, si el primer día de una semana es domingo o lunes).

* **La ruta de acceso de las** instantáneas define la ruta raíz en la que se almacenan las instantáneas de los gráficos históricos.
* **La ruta a los** informes define la ruta en la que se encuentran los informes. El servicio de instantáneas utiliza esto para determinar los informes para tomar instantáneas.
* **Las instantáneas diarias** definen la hora de cada día en que se toman instantáneas diarias. La hora especificada se encuentra en la zona horaria local del servidor.
* **Las instantáneas por hora** definen el minuto de cada hora en que se toman instantáneas por hora.
* **Filas (máximo)** define el número máximo de filas almacenadas para cada instantánea. Este valor debe elegirse razonablemente; si es demasiado alto, esto afectará al tamaño del repositorio, si es demasiado bajo, los datos pueden no ser precisos debido a la forma en que se gestionan los datos históricos.
* **Si se habilita, se pueden crear datos históricos falsos** usando el  `fakedata` selector; si está desactivado, el uso del  `fakedata` selector generará una excepción.

   Como los datos son falsos, *solo* deben utilizarse para realizar pruebas y depurar.

   El uso del selector `fakedata` terminará el informe de forma implícita, por lo que se perderán todos los datos existentes; los datos se pueden restaurar manualmente, pero este proceso puede llevar mucho tiempo.

* **El** usuario de instantáneas define un usuario opcional que puede utilizarse para tomar instantáneas.

   Básicamente, las instantáneas se toman para el usuario que ha finalizado el informe. Puede haber situaciones (por ejemplo, en un sistema de publicación, donde este usuario no existe ya que su cuenta no se ha duplicado) en las que desee especificar un usuario de reserva que se utilice en su lugar.

   Además, especificar un usuario puede suponer un riesgo para la seguridad.

* **Aplique al usuario** de instantáneas, si está habilitado, todas las instantáneas se tomarán con el usuario especificado en  *Usuario* de instantáneas. Esto puede tener graves repercusiones en la seguridad si no se gestiona correctamente.

### Configuración de caché (caché de informes de Day CQ) {#cache-settings-day-cq-reporting-cache}

* **** Habilitar le permite habilitar o deshabilitar el almacenamiento en caché de datos de informes. Al habilitar la caché del informe, los datos del informe se mantendrán en la memoria durante varias solicitudes. Esto puede aumentar el rendimiento, pero dará lugar a un mayor consumo de memoria y, en circunstancias extremas, puede provocar situaciones de falta de memoria.
* **** TTLdefine el tiempo (en segundos) durante el cual se almacenan en caché los datos del informe. Un número mayor aumentará el rendimiento, pero también puede devolver datos inexactos si los datos cambian dentro del período de tiempo.
* **El número máximo de** entradas define el número máximo de informes que se almacenarán en la caché en cualquier momento.

>[!NOTE]
>
>Los datos del informe pueden ser diferentes para cada usuario y cada idioma. Por lo tanto, los datos del informe se almacenan en la caché por informe, usuario e idioma. Esto significa que un valor **Max entry** de `2` realmente almacena en caché los datos para:
>
>* un informe para dos usuarios con diferentes configuraciones de idioma
>* un usuario y dos informes

>


