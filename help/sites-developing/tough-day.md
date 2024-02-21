---
title: Día difícil
description: La prueba de Día difícil simula la carga diaria de unos 1000 autores en el peor de los casos, con todas las operaciones en marcha al mismo tiempo.
topic-tags: testing
content-type: reference
exl-id: ceb9671c-57f9-4d81-94c0-0dbccd4d90a2
source-git-commit: b1012548630affd697edd27c90bdac4eeb35125f
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 1%

---

# Día difícil{#tough-day}

## Qué es el Día Duro 2 {#what-is-tough-day}

AEM &quot;Tough Day 2&quot; es una aplicación que te permite probar los límites de tu instancia de. Se puede ejecutar de forma predeterminada con el grupo de pruebas predeterminado o se puede configurar para adaptarse a sus necesidades de prueba. Puedes mirar [esta grabación](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2017/aem-toughday2-stress-testing-benchmarking-tool.html) para una presentación de la solicitud.

>[!CAUTION]
>
>El día 2 difícil requiere Java™ 8.

## Cómo correr duro día 2 {#how-to-run-tough-day}

Descargue la última versión de Tough Day 2 desde el [Repositorio de Adobe](https://repo1.maven.org/maven2/com/adobe/qe/toughday2/). Después de descargar la aplicación, puede ejecutarla de forma predeterminada proporcionando la variable `host` parámetro. AEM En el ejemplo siguiente, la instancia de la se ejecuta localmente para que la variable `localhost` se utiliza este valor:

```xml
java -jar toughday2.jar --host=localhost
```

El grupo predeterminado que se ejecuta después de agregar los parámetros se denomina `toughday`. Contiene los siguientes casos de uso:

* Crear páginas y Live Copies para ellos (incluidos despliegues)
* Obtener página principal
* Ejecutar consultas en querybuilder
* Creación de jerarquías de recursos
* Eliminar recursos

El grupo contiene un 15 % de acciones de escritura y un 85 % de acciones de lectura.

Para ejecutar las pruebas de grupo, Tough Day 2 instalará su paquete de contenido predeterminado. Esto se puede evitar configurando la variable `installsamplecontent`parámetro a `false`, pero recuerde que también debe cambiar las rutas predeterminadas de las pruebas que desea ejecutar. Si el JAR se ejecuta sin parámetros, Día difícil 2 muestra el [información de ayuda](/help/sites-developing/tough-day.md#getting-help).

Como regla general, puede utilizar la aplicación siguiendo este patrón:

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>El Día 2 difícil no tiene una etapa de limpieza. Como resultado, se recomienda ejecutar Día difícil 2 en una instancia de ensayo clonada y no en la instancia de producción principal. La instancia de ensayo debe eliminarse después de las pruebas.
>

### Obtención de ayuda {#getting-help}

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
   <td><strong>Ejemplos</strong></td>
  </tr>
  <tr>
   <td>—help</td>
   <td>Imprime información global, por ejemplo: las acciones disponibles, los grupos predefinidos, los modos de ejecución y los parámetros globales.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_publish</td>
   <td>Imprime todos los editores disponibles.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_tests</td>
   <td>Imprime las clases de prueba y su descripción.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_full</td>
   <td>Imprime todo lo anterior, además de pruebas, editores y componentes de grupo.</td>
   <td> </td>
  </tr>
  <tr>
   <td> —help —runmode/publishmode type=&lt;mode&gt;</td>
   <td>Muestra información acerca del modo de ejecución o publicación especificado.</td>
   <td><p>Java™ -jar toughday2.jar —help —runmode type=constantload</p> <p>Java™ -jar toughday2.jar —help —publishmode type=interval</p> </td>
  </tr>
  <tr>
   <td>—help —suite=&lt;suitename&gt;</td>
   <td>Enumera todas las pruebas de un grupo determinado y sus propiedades configurables respectivas.</td>
   <td><br /> Java™ -jar toughday2.jar —help —suite=get_tests</td>
  </tr>
  <tr>
   <td> —help —tag=&lt;tag&gt;</td>
   <td><br /> Enumera todos los elementos que tienen la etiqueta especificada.</td>
   <td>Java™ -jar toughday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td>—help &lt;testclass publisherclass=""&gt;</td>
   <td><br /> Enumera todas las propiedades configurables para la prueba o el publicador determinados.</td>
   <td><p>Java™ -jar toughday2.jar —help UploadPDFTest</p> <p>Java™ -jar toughday2.jar —help CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### Parámetros globales {#global-parameters}

El Día 2 difícil ofrece parámetros globales que establecen o cambian el entorno de las pruebas. Estos incluyen el host de destino, el número de puerto, el protocolo utilizado, el usuario y la contraseña de la instancia, y muchos más. Por ejemplo:

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

Puede encontrar los parámetros relevantes en la siguiente lista:

| **Parámetro** | **Descripción** | **Valor predeterminado** | **Valores posibles** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | Instala o omite el paquete de contenido predeterminado de Día difícil 2. | true | true o false |
| `--protocol=<Val>` | El protocolo utilizado para el host. | http | http o https |
| `--host=<Val>` | El nombre de host o la IP que se va a segmentar. |  |  |
| `--port=<Val>` | El puerto del host. | 4502 |  |
| `--user=<Val>` | El nombre de usuario de la instancia. | administrador |  |
| `--password=<Val>` | Contraseña del usuario determinado. | administrador |  |
| `--duration=<Val>` | La duración de las pruebas. Se puede expresar en (**s**)segundos, (**m**)minutos, (**h**)ours y (**d**)días. | 1d |  |
| `--timeout=<Val>` | El tiempo que debe transcurrir para que una prueba se interrumpa y se marque como errónea. Se expresa en segundos. | 180 |  |
| `--suite=<Val>` | El valor puede ser uno o una lista (separados por comas) de grupos de pruebas predefinidos. | día difícil |  |
| `--configfile=<Val>` | El archivo de configuración yaml de destino. |  |  |
| `--contextpath=<Val>` | Ruta de contexto de la instancia. |  |  |
| `--loglevel=<Val>` | Nivel de registro del motor de Día difícil 2. | INFORMACIÓN | TODO, DEPURAR, INFORMACIÓN, ADVERTENCIA, ERROR, FATAL, DESACTIVADO |
| `--dryrun=<Val>` | Si el valor es True, imprime la configuración resultante y no ejecuta ninguna prueba. | false | true o false |

## Personalización {#customizing}

La personalización se puede lograr de dos maneras: parámetros de línea de comandos o archivos de configuración yaml. **Los archivos de configuración se utilizan para grupos de informes personalizados grandes y anulan los parámetros predeterminados de Día difícil 2. Los parámetros de la línea de comandos anulan tanto los archivos de configuración como los parámetros predeterminados.**

La única manera de guardar una configuración de prueba es copiarla en formato yaml.

### Agregar una nueva prueba {#adding-a-new-test}

Si no desea utilizar el valor predeterminado `toughday` grupo puede agregar una prueba de su elección utilizando el `add` parámetro. Los ejemplos siguientes muestran cómo añadir la variable `CreateAssetTreeTest` realice pruebas utilizando parámetros de línea de comandos o un archivo de configuración yaml.

Mediante parámetros de la línea de comandos:

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

### Adición de varias instancias de la misma prueba  {#adding-multiple-instances-of-the-same-test}

También puede agregar y ejecutar varias instancias de la misma prueba, pero cada una debe tener un nombre único. Los ejemplos siguientes muestran cómo agregar dos instancias de la misma prueba mediante parámetros de línea de comandos o un archivo de configuración yaml.

Mediante parámetros de la línea de comandos:

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

### Cambiar las propiedades de prueba {#changing-the-test-properties}

Si necesita cambiar una o más propiedades de prueba, puede agregar esa propiedad a la línea de comandos o al archivo de configuración yaml. Para ver todas las propiedades de prueba disponibles, agregue la variable `--help <TestClass/PublisherClass>` a la línea de comandos, por ejemplo:

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

Tenga en cuenta que los archivos de configuración yaml sobrescribirán los parámetros predeterminados del Día difícil 2 y los parámetros de línea de comandos anularán tanto los archivos de configuración como los valores predeterminados.

Los ejemplos siguientes muestran cómo cambiar el `template` propiedad para `CreatePageTreeTest` realice la prueba utilizando parámetros de línea de comandos o un archivo de configuración yaml.

Mediante parámetros de la línea de comandos:

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

Los ejemplos siguientes muestran cómo añadir una prueba a un grupo predefinido y cómo reconfigurar y excluir una prueba existente de un grupo predefinido.

Puede agregar una nueva prueba a un grupo predefinido utilizando `add` y especificando el grupo de informes predefinido de destino.

Mediante parámetros de la línea de comandos:

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

Las pruebas existentes en un grupo determinado también se pueden reconfigurar mediante la variable `config`* *parámetro. Especifique también el nombre del grupo de informes y el nombre real de la prueba (no el nombre de la clase de prueba). Puede encontrar el nombre de la prueba en la `name` propiedad de la clase Test. Para obtener más información sobre cómo buscar propiedades de prueba, lea la [Cambiar propiedades de prueba](/help/sites-developing/tough-day.md#changing-the-test-properties) sección.

En el ejemplo siguiente, el título de recurso predeterminado de la variable `CreatePageTreeTest` (denominado `UploadAsset`) se cambia a &quot;Nuevo recurso&quot;.

Mediante parámetros de la línea de comandos:

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

Además, también puede quitar pruebas de grupos de informes predefinidos o editores de la configuración predeterminada con el uso de `exclude` parámetro. Especifique también el nombre del grupo de informes y el nombre real de la prueba (no la prueba C) `lass` nombre). Puede encontrar el nombre de la prueba en la `name` propiedad de la clase test. En el ejemplo siguiente, la variable `CreatePageTreeTest` (denominado `UploadAsset`) la prueba se ha eliminado del grupo toughday.

Mediante parámetros de la línea de comandos:

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

El Día 2 difícil puede ejecutarse en uno de los siguientes modos: **normal** y **carga constante**.

El **normal** el modo de ejecución tiene dos parámetros:

* `concurrency` : la concurrencia representa el número de subprocesos que el Día difícil 2 creará para la ejecución de pruebas. En estos subprocesos, las pruebas se ejecutarán hasta que se haya agotado la duración o hasta que no haya más pruebas para ejecutar.

* `waittime` : el tiempo de espera entre dos ejecuciones de prueba consecutivas en el mismo subproceso. El valor debe expresarse en milisegundos.

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

El **carga constante** el modo de ejecución difiere del modo de ejecución normal al generar un número constante de ejecuciones de prueba iniciadas, en lugar de un número constante de subprocesos. Puede establecer la carga utilizando el parámetro del modo de ejecución con el mismo nombre.

### Selección de prueba {#test-selection}

El proceso de selección de pruebas es el mismo para ambos modos de ejecución y funciona de la siguiente manera: todas las pruebas tienen un `weight` , que determina la probabilidad de ejecución en un subproceso. Por ejemplo, si tiene dos pruebas, una con un peso de 5 y otra con un peso de 10, la última tiene dos veces más probabilidades de ejecutarse que la primera.

Además, las pruebas pueden tener un `count` , que limita el número de ejecuciones a un número determinado. Una vez pasado este número, no se producirán más ejecuciones de la prueba. Todas las instancias de prueba que ya se están ejecutando finalizarán la ejecución según lo configurado. El siguiente ejemplo muestra cómo agregar estos parámetros en la línea de comandos o mediante un archivo de configuración yaml.

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
>Debido a las ejecuciones paralelas, el número real de ejecuciones de prueba no será exactamente la cantidad configurada en la `count` parámetro. Esperar una desviación proporcional al número de hilos en ejecución (controlado por el `concurrency parameter`).

### Ensayo {#dry-run}

Una ejecución en seco analiza todas las entradas dadas (parámetros de línea de comandos o archivos de configuración), combinándolas con los valores predeterminados y, a continuación, genera los resultados. No ejecuta ninguna de las pruebas.

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## Salida {#output}

El Día 2 difícil genera tanto métricas de prueba como registros. Para obtener más información, lea las secciones siguientes.

### Métricas de prueba {#test-metrics}

Actualmente, el Día 2 difícil informa de nueve métricas de prueba que puede evaluar. Métricas con el **&#42;** Los símbolos de solo se registran después de ejecuciones correctas:

| **Nombre** | **Descripción** |
|---|---|
| Marca de tiempo | Marca de tiempo de la última ejecución de prueba finalizada. |
| Superado | Número de ejecuciones correctas. |
| Error | Número de ejecuciones fallidas. |
| Min&#42; | La duración más baja de la ejecución de pruebas. |
| Max&#42; | Duración máxima de la ejecución de la prueba. |
| Mediana&#42; | Duración media calculada de todas las ejecuciones de prueba. |
| Media&#42; | Duración media calculada de todas las ejecuciones de prueba. |
| StdDev&#42; | La desviación estándar. |
| 90p&#42; | 90 %. |
| 99p&#42; | Percentil 99. |
| 99,9p&#42; | Percentil 99,9. |
| Rendimiento real&#42; | Número de ejecuciones divididas por el tiempo de ejecución transcurrido. |

Estas métricas se escriben con la ayuda de editores que se pueden agregar con la variable `add` parámetro (similar a añadir pruebas). Actualmente, hay dos opciones:

* **CSVPublisher** - el resultado es un archivo CSV.
* **ConsolePublisher** : la salida se muestra en la consola.

De forma predeterminada, ambos editores están habilitados.

Además, hay dos modos en los que se crean los informes de las métricas:

* El **simple** modo de publicación: informa de los resultados desde el principio de la ejecución hasta el momento de la publicación.
* El **intervalos** modo de publicación: informa de los resultados en un lapso de tiempo determinado. Puede establecer el lapso de tiempo con **intervalo** parámetro de modo de publicación.

El siguiente ejemplo muestra cómo configurar la variable `intervals` parámetro en la línea de comandos o utilizando un archivo de configuración yaml.

Mediante parámetros de la línea de comandos:

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

Día difícil 2 crea una carpeta de registros en el mismo directorio en el que ejecutó Día difícil 2. Esta carpeta contiene dos tipos de registros:

* **toughday.log**: contiene mensajes relacionados con el estado de la aplicación, la información de depuración y los mensajes globales.
* **toughday_&lt;testname>.log**: mensajes relacionados con la prueba especificada.

Los registros no se sobrescriben, las ejecuciones posteriores anexan mensajes a los registros existentes. Los registros tienen varios niveles. Para obtener más información, consulte la [parámetro loglevel.](#global-parameters).

<!--
#### Example Usage {#example-usage}

#### Known Issues {#known-issues}

[Get File](assets/toughday-6_1.jar)
-->
