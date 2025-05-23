---
title: Configuración de Solr para SRP
description: Una instalación de Apache Solr se puede compartir entre el almacén de nodos (Oak) y el almacén común (SRP) mediante diferentes colecciones
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: a9fc9c06-b9e6-4a5e-ab5e-0930ecd4b51b
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 2%

---

# Configuración de Solr para SRP {#solr-configuration-for-srp}

## AEM Solr para plataforma de {#solr-for-aem-platform}

Una instalación de [Apache Solr](https://solr.apache.org/) se puede compartir entre el [almacén de nodos](../../help/sites-deploying/data-store-config.md) (Oak) y el [almacén común](working-with-srp.md) (SRP) usando diferentes colecciones.

Si las colecciones Oak y SRP se utilizan de forma intensiva, se puede instalar un segundo Solr por motivos de rendimiento.

Para entornos de producción, [SolrCloud mode](#solrcloud-mode) proporciona un rendimiento mejorado con respecto al modo independiente (una única configuración de Solr local).

### Requisitos  {#requirements}

Descargue e instale Apache Solr:

* [Versión 7.0](https://archive.apache.org/dist/lucene/solr/7.0.0/)

* Solr requiere Java™ 1.7 o superior
* No se necesita ningún servicio
* Elección de los modos de ejecución:

   * Modo independiente
   * [Modo SolrCloud](#solrcloud-mode) (recomendado para entornos de producción)

* Opción de búsqueda multilingüe (MLS)

   * [Instalación de MLS estándar](#installing-standard-mls)
   * [Instalación de MLS avanzado](#installing-advanced-mls)

## Modo SolrCloud {#solrcloud-mode}

Se recomienda el modo [SolrCloud](https://solr.apache.org/guide/6_6/solrcloud.html) para entornos de producción. Cuando se ejecuta en modo SolrCloud, SolrCloud debe instalarse y configurarse antes de instalar la búsqueda multilingüe (MLS).

La recomendación es seguir las instrucciones de SolrCloud para instalar:

* 3 nodos de SolrCloud en el mismo servidor.
* Un Apache ZooKeeper externo.

También se recomienda configurar JVM para ajustar el uso de memoria y la recopilación de elementos no utilizados.

### Ejemplo de configuración de JVM {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### Comandos de configuración de SolrCloud {#solrcloud-setup-commands}

Cuando se ejecuta en modo SolrCloud, antes de la instalación de MLS, es necesario usar y conocer los siguientes comandos de configuración de SolrCloud.

#### 1. Cargue una configuración en ZooKeeper {#upload-a-configuration-to-zookeeper}

Referencia:
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

Uso:
sh./scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *servidor:puerto* \
-confname *myconfig-name *\
-solrhome *solr-home-path* \
-confdir *config-dir*

#### 2. Crear una colección {#create-a-collection}

Referencia:
[https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create](https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create)

Uso:
./bin/solr crear \
-c *nombre_colección_mim*\
-d *config-dir* \
-n *nombre_configuración* \
-p *puerto*\
-s *número de fragmentos* \
-rf *número-de-réplicas*

#### 3. Vincule una colección a un conjunto de configuración {#link-a-collection-to-a-configuration-set}

Vincula una colección a una configuración ya cargada en ZooKeeper.

Referencia:
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

Uso:
sh./scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *servidor:puerto* \
-collection *nombre_colección* \
-confname *nombre_configuración*

### Comparación de MLS estándar y avanzado {#comparison-of-standard-and-advanced-mls}

La búsqueda multilingüe (MLS) de AEM Communities está diseñada para la plataforma Solr y ofrece una búsqueda mejorada en todos los idiomas admitidos, incluido el inglés.

MLS para AEM Communities está disponible como MLS estándar o MLS avanzado. MLS estándar solo incluye los ajustes de configuración de Solr y excluye los complementos o archivos de recursos. Advanced MLS es la solución más completa e incluye opciones de configuración de Solr, complementos y recursos relacionados

MLS estándar incluye mejoras para la búsqueda de contenido en los siguientes idiomas:

* Inglés: Se ha mejorado el stemmer para intentar hacer coincidir las derivaciones de palabras.
* Japonés: se ha mejorado la tokenización japonesa para caracteres de media anchura.

MLS avanzado incluye mejoras para la búsqueda de contenido en los siguientes idiomas:

* Inglés: Reemplazo de stemmer por lemmatizer.
* Alemán: Se ha agregado decompositor.
* Francés: se ha agregado la gestión de elisiones.
* Chino (simplificado): se ha añadido un token más inteligente.
* Varios idiomas: se ha agregado un compilador, una lista de palabras de detención y un normalizador.

En total, los siguientes 33 idiomas son compatibles con MLS avanzado.

| Árabe | Alemán | Noruego |
|---|---|---|
| Búlgaro | Griego | Polaco |
| Chino (simplificado) | Criollo haitiano | Portugués |
| Chino (tradicional) | Hebreo | Rumano |
| Checo | Húngaro | Ruso |
| Danés | Indonesio | Eslovaco |
| Neerlandés | Italiano | Esloveno |
| Inglés | Japonés | Español |
| Estonio | Coreano | Sueco |
| Finés | Letón | Tailandés |
| Francés | Lituano | Turco |

#### AEM Comparación de la búsqueda de Solr de la versión 6.1 de la versión de la aplicación, MLS estándar y MLS avanzado {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

AEM AEM **Nota**: la versión 6.1 de la se refiere a las versiones anteriores y posteriores del FP3 de las comunidades 6.1.

![compare-solr-mls](assets/compare-solr-mls.png)

### Instalación de MLS estándar {#installing-standard-mls}

Para que la colección SRP (ya sea MSRP o DSRP) admita la búsqueda multilingüe estándar (MLS), es necesario modificar dos de los archivos de configuración de Solr:

* **schema.xml**
* **solrconfig.xml**

Archivos MLS estándar (schema.xml, solrconfig.xml) para Solr 4.10.

Archivos MLS estándar (schema.xml, solrconfig.xml) para Solr 5.x.

AEM Los archivos MLS estándar se almacenan en el repositorio de la.

**Nota**: mientras que los archivos Solr se almacenan en la carpeta msrp/, también son para DSRP (no es necesario realizar cambios).

**Instrucciones de descarga**: reemplace `solrX` por `solr4` o `solr5` según corresponda.

1. Con CRXDE|Lite, busque:

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. Descargar en el servidor local en el que está implementado Solr.

   * Busque la propiedad `jcr:data` del nodo `jcr:content`.
   * Para iniciar la descarga, seleccione `view`.
   * Asegúrese de que los archivos se guardan con los nombres y la codificación adecuados (UTF8).

1. Siga las instrucciones de instalación para el modo independiente o SolrCloud.

#### Modo SolrCloud: MLS estándar {#solrcloud-mode-standard-mls}

1. Instale y configure Solr en el modo SolrCloud.
1. Prepare una nueva configuración:

   1. Crear nuevo-config-dir* como `solr-install-dir*/myconfig/`

   1. Copie el contenido del directorio de configuración de Solr existente en *new-config-dir*

      * Para Solr4: copiar `solr-install-dir/example/solr/collection1/conf/`
      * Para Solr5: copiar `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`

   1. Copie los archivos **schema.xml** y **solrconfig.xml** descargados en *new-config-dir* para sobrescribir los archivos existentes.

1. [Cargar la nueva configuración](#upload-a-configuration-to-zookeeper) a ZooKeeper.
1. [Cree una colección](#create-a-collection) que especifique los parámetros necesarios, como el número de fragmentos, el número de réplicas y el nombre de configuración.
1. Si el nombre de la configuración *no se proporcionó durante la creación de la colección, [vincule esta colección recién creada](#link-a-collection-to-a-configuration-set) con la configuración cargada en ZooKeeper.

1. Para MSRP, ejecute [MSRP Reindex Tool](msrp.md#msrp-reindex-tool), a menos que esta instalación sea nueva.

#### Modo independiente - MLS estándar {#standalone-mode-standard-mls}

1. Instale Solr en modo independiente.
1. Si ejecuta Solr5, cree una colección1 (similar a Solr4):

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. Haga una copia de seguridad de **schema.xml** y **solrconfig.xml** en el directorio de configuración de Solr, como:

   * Para Solr4: `solr-install-dir/example/solr/collection1/conf/`
   * Creado para Solr5: `solr-install-dir/server/solr/collection1/conf/`

1. Copie los archivos **schema.xml** y **solrconfig.xml** descargados en el mismo directorio.

1. Reinicie Solr.
1. Para MSRP, ejecute [MSRP Reindex Tool](#msrpreindextool), a menos que esta instalación sea nueva.

### Instalación de MLS avanzado {#installing-advanced-mls}

Para que la colección SRP (MSRP o DSRP) admita MLS avanzado, se requieren nuevos complementos de Solr, además de un esquema personalizado y una configuración de Solr. Todos los elementos necesarios se empaquetan en un archivo zip descargable. Además, se incluye una secuencia de comandos de instalación para utilizarla cuando Solr se implemente en modo independiente.

AEM Para obtener el paquete MLS avanzado, consulte [MLS avanzado](deploy-communities.md#aem-advanced-mls) en la sección de implementación de la documentación de &lbrace;Advanced MLS.

Para empezar a instalar en SolrCloud o en modo independiente:

* AEM Descargue el archivo zip de SOLR-MLS en el servidor que aloja Solr.
* Desempaquete el archivo.

#### Modo SolrCloud: MLS avanzado {#solrcloud-mode-advanced-mls}

Instrucciones de instalación: tenga en cuenta las pocas diferencias entre Solr4 y Solr5:

1. Instale y configure Solr en el modo SolrCloud.
1. Extraiga el contenido del paquete MLS avanzado en el disco. El contenido debe incluir:

   * **schema.xml**
   * **solrconfig.xml**
   * carpeta **stopwords/**
   * **perfiles/** carpeta
   * **extra-libs/** carpeta

1. Prepare una nueva configuración:

   1. Crear un *nuevo-config-dir*

      * Como `solr-install-dir/myconfig/`
      * Crear subcarpetas `stopwords/` y `lang/`

   1. Copie el contenido del directorio de configuración de Solr existente en *new-config-dir*

      * Para Solr4: Copiar `solr-install-dir/example/solr/collection1/conf/`
      * Para Solr5: Copiar `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`

   1. Copie los archivos extraídos **schema.xml** y **solrconfig.xml** a *new-config-dir* para sobrescribir los archivos existentes.
   1. Para Solr5: copiar `solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt` a `new-config-dir/lang/`
   1. Copie la carpeta extraída **stopwords/** en *new-config-dir*, con el resultado `new-config-dir/stopwords/*.txt`

1. [Cargar la nueva configuración](#upload-a-configuration-to-zookeeper) a ZooKeeper
1. Copie la nueva carpeta **profiles/**...

   * Para Solr4: copie en los recursos o carpetas de cada nodo
   * Para Solr5: copie en cada carpeta server/resources/ de la instalación de Solr. Si todos los nodos están en el mismo directorio de instalación de Solr, este paso se realiza solo una vez.

1. Cree una carpeta **lib/** en el directorio solr-home (contiene solr.xml) de cada nodo en SolrCloud. Copie los Jars de las siguientes ubicaciones a la nueva carpeta lib/ en cada nodo:

   * **extra-libs/** extraídas del paquete avanzado de MLS
   * *solr-install-dir/contrib/extraction/lib/*.jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *solr-install-dir/contrib/clustering/lib/*.jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr-install-dir/contrib/langid/lib/*.jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *solr-install-dir/contrib/velocity/lib/*.jar
   * *solr-install-dir/dist/solr-velocity*.jar
   * *solr-install-dir/contrib/analysis-extras/lib/*.jar
   * *solr-install-dir/contrib/analysis-extras/lucene-libs/*.jar

1. [Cree una colección](#create-a-collection) que especifique los parámetros necesarios, como el número de fragmentos, el número de réplicas y el nombre de configuración.
1. Si se proporcionó el nombre de la configuración *no* durante la creación de la colección, [vincule esta colección recién creada](#link-a-collection-to-a-configuration-set) con la configuración cargada en ZooKeeper.

1. Para MSRP, ejecute [MSRP Reindex Tool](#msrpreindextool), a menos que esta instalación sea nueva.

#### Modo independiente: MLS avanzado {#standalone-mode-advanced-mls}

Se incluye una secuencia de comandos de instalación en el paquete MLS avanzado.

Una vez extraído el contenido del paquete en el servidor que aloja el servidor Solr independiente, ejecute el script de instalación para instalar los recursos y los archivos de configuración necesarios.

* Instale Solr en modo independiente.
* Si ejecuta Solr5, cree una colección1 (similar a Solr4):

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* Ejecutar el script de instalación: Instalar [-v 4|5] [-d solrhome] [-c collectionPath]
donde:

   * -d solrhome

     Directorio de instalación de Solr

   * -c rutaDeColección

     Ruta de recopilación en solr

   * —help

     Imprimir opciones de línea de comandos

   * -v [4|5]

     Establecer versión para solr

* Ejemplo de Solr 4.10.4:

   * Install.bat -v 4 -d c:/solr-4.10.4 -c c:/solr-4.10.4/example/solr/collection1

* Ejemplo de Solr 5.4.0:

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**Nota**:

* El script de instalación realiza una copia de seguridad de schema.xml y solrconfig.xml antes de instalar nuevas versiones añadiendo &quot;.orig&quot;.

### Acerca de solrconfig.xml {#about-solrconfig-xml}

El archivo **solrconfig.xml** controla el intervalo de confirmación automática y la visibilidad de la búsqueda, y requiere pruebas y ajustes.

`<autoCommit>`: de forma predeterminada, el intervalo de confirmación automática, que es una confirmación dura para un almacenamiento estable, se establece en 15 segundos. La visibilidad de la búsqueda toma como valor predeterminado el uso del índice de confirmación previa.

Para cambiar la búsqueda y utilizar un índice actualizado para reflejar los cambios debidos a la confirmación, cambie el `openSearcher` contenido a true.

`autoSoftCommit`: una confirmación &quot;suave&quot; garantiza que los cambios sean visibles (el índice está actualizado), pero no garantiza que los cambios se sincronicen con un almacenamiento estable (confirmación grave). El resultado es una mejora en el rendimiento. De manera predeterminada, `autoSoftCommit` está deshabilitado con el `maxTime` contenido establecido en -1.
