---
title: Día duro
seo-title: Día duro
description: La prueba del día duro simula la carga diaria de unos 1000 autores en el peor de los casos, con todas las operaciones que se realizan al mismo tiempo.
seo-description: La prueba del día duro simula la carga diaria de unos 1000 autores en el peor de los casos, con todas las operaciones que se realizan al mismo tiempo.
uuid: 1b672182-40f5-4580-b038-2e3c8fbfb8b7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: ea6b40fe-b6e1-495c-b34f-8815a4e2e42e
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Día duro{#tough-day}

## ¿Qué es el día duro 2? {#what-is-tough-day}

&quot;Día duro 2&quot; es una aplicación que le permite probar los límites de su instancia de AEM. Se puede agotar con el grupo de pruebas predeterminado o se puede configurar para que se ajuste a sus necesidades de prueba. Puede ver [esta grabación](https://docs.adobe.com/ddc/en/gems/Toughday2---A-new-and-improved-stress-testing-and-benchmarking-tool.html) para ver una presentación de la aplicación.

## Cómo correr duro día 2 {#how-to-run-tough-day}

Descargue la versión más reciente de Tough Day 2 desde el repositorio [de](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/qe/toughday2/)Adobe. Después de descargar la aplicación, puede ejecutarla de forma predeterminada proporcionando el `host` parámetro . En el ejemplo siguiente, la instancia de AEM se ejecuta localmente para que se utilice el `localhost` valor:

```xml
java -jar toughday2.jar --host=localhost
```

Se asigna un nombre al grupo predeterminado que se ejecuta después de agregar los parámetros `toughday`. Contiene los siguientes casos de uso:

* Cree páginas y Live Copies para ellas (incluidos los lanzamientos)
* Obtener página principal
* Ejecutar consultas en querybuilder
* Creación de jerarquías de recursos
* Eliminar recursos

El grupo contiene acciones de escritura del 15 % y acciones de lectura del 85 %.

Para ejecutar las pruebas de grupo, el Día duro 2 instalará su paquete de contenido predeterminado. Esto se puede evitar estableciendo el `installsamplecontent`parámetro en `false`, pero recuerde que también debe cambiar las rutas predeterminadas para las pruebas que se van a ejecutar. Si el tarro se ejecuta sin parámetros, el Día duro 2 muestra la información [de](/help/sites-developing/tough-day.md#getting-help)ayuda.

Como regla general, puede utilizar la aplicación siguiendo este patrón:

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>El duro Día 2 no tiene un paso de limpieza. Como resultado, se recomienda ejecutar el Día duro 2 en una instancia de ensayo clonada y no en la instancia de producción principal. La instancia de ensayo debe eliminarse después de las pruebas.


### Ayuda {#getting-help}

Tough Day 2 ofrece una amplia gama de opciones de ayuda a las que se puede acceder desde la línea de comandos. Por ejemplo:

```xml
java -jar toughday2.jar --help_full
```

En la tabla siguiente, puede encontrar los parámetros de ayuda relevantes.

<table>
 <tbody>
  <tr>
   <td><strong>Parámetro</strong></td>
   <td><strong>Descripción</strong></td>
   <td><strong>Ejemplo</strong></td>
  </tr>
  <tr>
   <td>--ayuda</td>
   <td>Imprime la información global, por ejemplo: las acciones disponibles, los grupos predefinidos, los modos de ejecución y los parámetros globales.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_publish</td>
   <td>Imprime todos los editores disponibles.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_testing</td>
   <td>Imprime las clases de prueba y su descripción.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_full</td>
   <td>Imprime todo lo anterior, además de pruebas, editores y componentes de grupo.</td>
   <td> </td>
  </tr>
  <tr>
   <td> —help —runmode/publishmode type=&lt;Modo&gt;</td>
   <td>Muestra información sobre el modo de ejecución o publicación especificado.</td>
   <td><p>java -jar toughday2.jar —help —runmode type=constantload</p> <p>java -jar toughday2.jar —help —publishmode type=periods</p> </td>
  </tr>
  <tr>
   <td>—help —suite=&lt;nombreDeGrupo&gt;</td>
   <td>Enumera todas las pruebas de un conjunto determinado y sus respectivas propiedades configurables.</td>
   <td><br /> java -jar toughday2.jar —help —suite=get_testing</td>
  </tr>
  <tr>
   <td> —help —tag=&lt;Etiqueta&gt;</td>
   <td><br /> Enumera todos los elementos que tienen la etiqueta especificada.</td>
   <td>java -jar toughday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td>—help &lt;TestClass/PublisherClass&gt;</td>
   <td><br /> Enumera todas las propiedades configurables para una prueba o publicador determinado.</td>
   <td><p>java -jar toughday2.jar —help UploadPDFTest</p> <p>java -jar toughday2.jar —help CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### Parámetros globales {#global-parameters}

El Día duro 2 ofrece parámetros globales que establecen o modifican el entorno para las pruebas. Entre ellos se incluyen el host de destino, el número de puerto, el protocolo utilizado, el usuario y la contraseña de la instancia y muchos más. Por ejemplo:

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

Puede encontrar los parámetros relevantes en la lista siguiente:

| **Parámetro** | **Descripción** | **Valor predeterminado** | **Valores posibles** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | Instala o omite el paquete de contenido predeterminado Día duro 2. | verdadero |  true o false |
| `--protocol=<Val>` | Protocolo utilizado para el host. | http | http o https |
| `--host=<Val>` | El nombre de host o la dirección IP objetivo. |  |  |
| `--port=<Val>` | El puerto del host. | 4502 |  |
| `--user=<Val>` | El nombre de usuario de la instancia. | administrador |  |
| `--password=<Val>` | Contraseña para el usuario determinado. | administrador |  |
| `--duration=<Val>` | Duración de las pruebas. Puede expresarse en (**s**)segundos, (**m**)minutos, (**h**)horas y (**d**)días. | 1d |  |
| `--timeout=<Val>` | Duración de la prueba antes de que se interrumpa y se marque como fallida. Se expresa en segundos. | 180 |  |
| `--suite=<Val>` | El valor puede ser uno o una lista (separados por comas) de conjuntos de pruebas predefinidos. | toughday |  |
| `--configfile=<Val>` | El archivo de configuración yaml de destino. |  |  |
| `--contextpath=<Val>` | Ruta de contexto de la instancia. |  |  |
| `--loglevel=<Val>` | Nivel de registro para el motor del Día duro 2. | INFORMACIÓN | TODOS, DEPURAR, INFORMACIÓN, ADVERTENCIA, ERROR, FATAL, DESACTIVADO |
| `--dryrun=<Val>` | Si es true, imprime la configuración resultante y no ejecuta ninguna prueba. | false |  true o false |

## Personalización {#customizing}

La personalización se puede lograr de dos maneras: parámetros de línea de comandos o archivos de configuración de yaml. **Los archivos de configuración generalmente se utilizan para grupos personalizados de gran tamaño y anulan los parámetros predeterminados del Día duro 2. Los parámetros de línea de comandos anulan tanto los archivos de configuración como los parámetros predeterminados.**

La única manera de guardar una configuración de prueba es copiarla en formato yaml. Para obtener más información, consulte esta configuración [toughday.yaml](https://repo.adobe.com/nexus/service/local/repositories/releases/content/com/adobe/qe/toughday2/0.2.1/toughday2-0.2.1.yaml) y los ejemplos de configuración yaml en las secciones siguientes.

### Adición de una nueva prueba {#adding-a-new-test}

Si no desea utilizar el grupo `toughday` predeterminado, puede agregar una prueba de su elección utilizando el `add` parámetro . Los ejemplos siguientes muestran cómo agregar la `CreateAssetTreeTest` prueba utilizando parámetros de línea de comandos o un archivo de configuración de yaml.

Mediante parámetros de línea de comandos:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest
```

Mediante un archivo de configuración yaml:

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
```

### Adición de varias instancias de la misma prueba {#adding-multiple-instances-of-the-same-test}

También puede agregar y ejecutar varias instancias de la misma prueba, pero cada instancia debe tener un nombre único. Los ejemplos siguientes muestran cómo agregar dos instancias de la misma prueba, ya sea mediante parámetros de línea de comandos o mediante un archivo de configuración yaml.

Mediante parámetros de línea de comandos:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest name=FirstAssetTree --add CreateAssetTreeTest name=SecondAssetTree
```

Mediante un archivo de configuración yaml:

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
    properties:
      name : FirstAssetTree
  - add : CreateAssetTreeTest
    properties:
      name : SecondAssetTree
```

### Cambio de las propiedades de la prueba {#changing-the-test-properties}

En caso de que necesite cambiar una o varias de las propiedades de prueba, puede agregar esa propiedad a la línea de comandos o al archivo de configuración yaml. Para ver todas las propiedades de prueba disponibles, agregue el `--help <TestClass/PublisherClass>` parámetro a la línea de comandos, por ejemplo:

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

Tenga en cuenta que los archivos de configuración yaml sobrescribirán los parámetros predeterminados de Día difícil 2 y los parámetros de línea de comandos anularán tanto los archivos de configuración como los valores predeterminados.

Los ejemplos siguientes muestran cómo cambiar la `template` propiedad de la `CreatePageTreeTest` prueba mediante parámetros de línea de comandos o un archivo de configuración de yaml.

Mediante parámetros de línea de comandos:

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest template=/conf/toughday-templates/settings/wcm/templates/toughday-template
```

Mediante un archivo de configuración yaml:

```xml
globals:
  host : localhost
tests:
  - add : CreatePageTreeTest
    properties:
      template : /conf/toughday-templates/settings/wcm/templates/toughday-template
```

### Uso de grupos de pruebas predefinidos {#working-with-predefined-test-suites}

Los ejemplos siguientes muestran cómo agregar una prueba a un grupo predefinido y cómo reconfigurar y excluir una prueba existente de un grupo predefinido.

Puede agregar una nueva prueba a un grupo predefinido utilizando el `add` parámetro y especificando el grupo predefinido de destino.

Mediante parámetros de línea de comandos:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest
```

Mediante un archivo de configuración yaml:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - add : CreatePageTreeTest
```

Las pruebas existentes en un grupo dado también se pueden reconfigurar usando el parámetro `config`* *. Tenga en cuenta que también debe especificar el nombre del conjunto y el nombre real de la prueba (no el nombre de la clase de prueba). El nombre de la prueba se encuentra en la propiedad `name` de la clase de prueba. Para obtener más información sobre cómo encontrar las propiedades de prueba, consulte la sección [Cambio de las propiedades](/help/sites-developing/tough-day.md#changing-the-test-properties) de la prueba.

En el ejemplo siguiente, el título de recurso predeterminado para el `CreatePageTreeTest` (denominado `UploadAsset`) se cambia a &quot;NewAsset&quot;.

Mediante parámetros de línea de comandos:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --config UploadAsset title=NewAsset
```

Mediante un archivo de configuración yaml:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - config : UploadAsset
    properties :
      title : NewAsset
```

Además, también puede eliminar pruebas de grupos o editores predefinidos de la configuración predeterminada con el uso del `exclude` parámetro . Tenga en cuenta que también debe especificar el nombre del conjunto y el nombre real de la prueba (no el nombre de la prueba C `lass` ). El nombre de la prueba se encuentra en la propiedad `name` de la clase test. En el ejemplo siguiente, la prueba `CreatePageTreeTest` (con nombre `UploadAsset`) se elimina del grupo toughday.

Mediante parámetros de línea de comandos:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --exclude UploadAsset
```

Mediante un archivo de configuración yaml:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - exclude : UploadAsset
```

### Ejecutar modos {#run-modes}

El Día duro 2 se puede ejecutar en uno de los siguientes modos: carga **normal** y **constante**.

El modo de ejecución **normal** tiene dos parámetros:

* `concurrency` - la concurrencia representa el número de subprocesos que el Día duro 2 creará para la ejecución de la prueba. En estos subprocesos, las pruebas se ejecutarán hasta que la duración se haya agotado o hasta que no haya más pruebas que ejecutar.

* `waittime` - el tiempo de espera entre dos ejecuciones de prueba consecutivas en el mismo subproceso. El valor debe expresarse en milisegundos.

El ejemplo siguiente muestra cómo agregar los parámetros mediante la línea de comandos:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

o utilizando un archivo de configuración yaml:

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

El modo de ejecución de carga **** constante difiere del modo de ejecución normal al generar un número constante de ejecuciones de prueba iniciadas, en lugar de un número constante de subprocesos. Puede configurar la carga utilizando el parámetro de modo de ejecución con el mismo nombre.

### Selección de prueba {#test-selection}

El proceso de selección de la prueba es el mismo para ambos modos de ejecución y sigue este procedimiento: todas las pruebas tienen una `weight` propiedad que determina la probabilidad de ejecución en un subproceso. Por ejemplo, si tenemos dos pruebas, una con un peso de 5 y otra con un peso de 10, la segunda tiene dos veces más probabilidades de ser ejecutada que la primera.

Además, las pruebas pueden tener una `count` propiedad que limita el número de ejecuciones a un número determinado. Después de superar este número, no se realizarán más ejecuciones de la prueba. Todas las instancias de prueba que ya se estén ejecutando finalizarán la ejecución según la configuración. En el siguiente ejemplo se muestra cómo agregar estos parámetros en la línea de comandos o mediante un archivo de configuración yaml.

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest weight=5 --add CreatePageTreeTest weight=10 count=100 --runmode=normal concurrency=20
```

o

```xml
- add : CreateAssetTreeTest
    properties :
      name : UploadAsset
      weight : 5
      base : 3
      foldertitle : IAmAFolder
      assettitle : IAmAnAsset
      count : 100
```

>[!NOTE]
>
>Debido a las ejecuciones paralelas, el número real de ejecuciones de prueba no será exactamente la cantidad configurada en el `count` parámetro. Se espera una desviación proporcional al número de subprocesos en ejecución (controlados por el `concurrency parameter`).

### Simulacro {#dry-run}

Una ejecución seca analiza toda la entrada dada (parámetros de línea de comandos o archivos de configuración), combinándola con los valores predeterminados y, a continuación, genera los resultados. No ejecuta ninguna de las pruebas.

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## Salida {#output}

El Día duro 2 genera tanto métricas de prueba como registros. Para obtener más información, lea las secciones siguientes.

### Métricas de prueba {#test-metrics}

El Día duro 2 actualmente informa 9 métricas de prueba que puede evaluar. Las métricas con el ***** símbolo solo se informan después de ejecutarse correctamente:

| **Nombre** | **Descripción** |
|---|---|
| Marca de hora | Marca de tiempo de la última ejecución de prueba finalizada. |
| Aprobado | Número de ejecuciones correctas. |
| Error | Número de ejecuciones fallidas. |
| Mínimo* | Duración mínima de la ejecución de la prueba. |
| Máximo* | Duración máxima de la ejecución de la prueba. |
| Mediana* | Duración media calculada de todas las ejecuciones de prueba. |
| Promedio* | Duración media calculada de todas las ejecuciones de prueba. |
| StdDev* | La desviación estándar. |
| 90p* | 90 percentil. |
| 99p* | Percentil 99. |
| 99,9p* | Percentil 99,9. |
| Rendimiento real* | Número de ejecuciones divididas por el tiempo de ejecución transcurrido. |

Estas métricas se escriben con la ayuda de editores que se pueden agregar con el `add` parámetro (de manera similar a agregar pruebas). Actualmente, hay dos opciones:

* **CSVPublisher** : el resultado es un archivo CSV.
* **ConsolePublisher** : la salida se muestra en la consola.

De forma predeterminada, ambos editores están habilitados.

Además, existen dos modos en los que se informan las métricas:

* El modo de publicación **simple** : informa de los resultados desde el comienzo de la ejecución hasta el momento de la publicación.
* El modo de publicación de **intervalos** : informa de los resultados en un intervalo de tiempo determinado. Puede establecer el intervalo de tiempo con el parámetro de modo de publicación de **intervalo** .

El siguiente ejemplo muestra cómo configurar el `intervals` parámetro en la línea de comandos o mediante un archivo de configuración yaml.

Mediante parámetros de línea de comandos:

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest --publishmode type=intervals interval=10s
```

Mediante un archivo de configuración yaml:

```xml
publishmode:
     type : intervals
     interval : 10s
     tests:
        -add : CreatePageTreeTest
```

### Registro {#logging}

El Día duro 2 crea una carpeta de registros en el mismo directorio donde se ejecuta el Día duro 2. Esta carpeta contiene dos tipos de registros:

* **toughday.log**: contiene mensajes relacionados con el estado de la aplicación, información de depuración y mensajes globales.
* **toughday_&lt;nombre_prueba>.log**: mensajes relacionados con la prueba especificada.

Los registros no se sobrescriben, las ejecuciones posteriores anexarán mensajes a los registros existentes. Los registros tienen varios niveles; para obtener más información, consulte la sección ` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`.

#### Uso de ejemplo {#example-usage}

#### Problemas conocidos {#known-issues}

[Obtener archivo](assets/toughday-6_1.jar)
