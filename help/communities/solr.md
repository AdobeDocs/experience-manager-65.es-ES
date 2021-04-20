---
title: Configuración de Solr para SRP
seo-title: Configuración de Solr para SRP
description: Una instalación de Apache Solr se puede compartir entre el almacén de nodos (Oak) y el almacén común (SRP) utilizando diferentes colecciones
seo-description: Una instalación de Apache Solr se puede compartir entre el almacén de nodos (Oak) y el almacén común (SRP) utilizando diferentes colecciones
uuid: 7356343d-073c-4266-bdcb-c7e999281476
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e228f1db-91ea-4ec3-86da-06d89d74bc72
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1484'
ht-degree: 2%

---


# Configuración de Solr para SRP {#solr-configuration-for-srp}

## Solr para AEM Platform {#solr-for-aem-platform}

Se puede compartir una instalación de [Apache Solr](https://lucene.apache.org/solr/) entre el [almacén de nodos](../../help/sites-deploying/data-store-config.md) (Oak) y el [almacén común](working-with-srp.md) (SRP) utilizando diferentes colecciones.

Si las colecciones Oak y SRP se utilizan intensamente, puede instalarse un segundo Solr por motivos de rendimiento.

Para los entornos de producción, [SolrCloud mode](#solrcloud-mode) proporciona un rendimiento mejorado sobre el modo independiente (una única configuración local de Solr).

### Requisitos {#requirements}

Descargue e instale Apache Solr:

* [Versión 7.0](https://archive.apache.org/dist/lucene/solr/7.0.0/)

* Solr requiere Java 1.7 o bueno
* No se necesita ningún servicio
* Elección de modos de ejecución:

   * Modo independiente
   * [Modo SolrCloud](#solrcloud-mode)  (recomendado para entornos de producción)

* Opción de búsqueda multilingüe (MLS)

   * [Instalación de MLS estándar](#installing-standard-mls)
   * [Instalación de MLS avanzados](#installing-advanced-mls)

## Modo SolrCloud {#solrcloud-mode}

[](https://cwiki.apache.org/confluence/display/solr/SolrCloud) Se recomienda SolrCloudmode para entornos de producción. Cuando se ejecuta en modo SolrCloud, SolrCloud debe estar instalado y configurado antes de instalar la búsqueda multilingüe (MLS).

La recomendación es seguir las instrucciones de SolrCloud para instalar:

* 3 nodos de SolrCloud en el mismo servidor.
* Un Apache ZooKeeper externo.

También se recomienda configurar JVM para ajustar el uso de memoria y la colección de residuos.

### Ejemplo de configuración de JVM {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:MaxPermSize=768M -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### Comandos de configuración de SolrCloud {#solrcloud-setup-commands}

Cuando se ejecuta en modo SolrCloud, antes de la instalación de MLS, es necesario utilizar y conocer los siguientes comandos de configuración de SolrCloud.

#### 1. Cargue una configuración en ZooKeeper {#upload-a-configuration-to-zookeeper}

Referencia:
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

Uso:
sh ./scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *server:port* \
-confname *myconfig-name *\
-solrhome *solr-home-path* \
-confidir *config-dir*

#### 2. Crear una colección {#create-a-collection}

Referencia:
[https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create](https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create)

Uso:
./bin/solr crear \
-c *mycollection-name*\
-d *config-dir* \
-n *myconfig-name* \
-p *puerto*\
-s *número de partes* \
-rf *número de réplicas*

#### 3. Vincular una colección a un conjunto de configuración {#link-a-collection-to-a-configuration-set}

Vincule una colección a una configuración ya cargada a ZooKeeper.

Referencia:
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

Uso:
sh ./scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *server:port* \
-collection *mycollection-name* \
-confname *myconfig-name*

### Comparación de MLS estándar y avanzado {#comparison-of-standard-and-advanced-mls}

La búsqueda multilingüe (MLS) para AEM Communities se ha creado para la plataforma Solr con el fin de proporcionar una búsqueda mejorada en todos los idiomas compatibles, incluido el inglés.

MLS para comunidades AEM está disponible como MLS estándar o MLS avanzado. MLS estándar solo incluye los ajustes de configuración de Solr y excluye los complementos o archivos de recursos. Advanced MLS es la solución más completa e incluye configuraciones de Solr, así como complementos y recursos relacionados

MLS estándar incluye mejoras para la búsqueda de contenido en los siguientes idiomas:

* Inglés: Se ha mejorado el lemmer para intentar hacer coincidir derivaciones de palabras.
* Japonés: Se ha mejorado la tokenización japonesa para los caracteres de ancho medio.

MLS avanzado incluye mejoras para la búsqueda de contenido en los siguientes idiomas:

* Inglés: Se sustituyó el tallo por un lemmatizador.
* Alemán: Se ha añadido el descomponedor.
* Francés: Se ha añadido la gestión de elisiones.
* Chino (simplificado): Se ha agregado un tokenizador más inteligente.
* Varios idiomas: Se ha añadido un contenedor, una lista de palabras de parada y un normalizador.

En total, los siguientes 33 idiomas son compatibles con Advanced MLS.

| Árabe | Alemán | Noruego |
|---|---|---|
| Búlgaro | Griego | Polaco |
| Chino (simplificado) | Criollo haitiano | Portugués |
| Chino (tradicional) | Hebreo | Rumano |
| Checo | Húngaro | Ruso |
| Danés | Indonesio | Eslovaco |
| Holandés | Italiano | Esloveno |
| Inglés | Japonés | Español |
| Estonio | Coreano | Sueco |
| Finés | Letón | Thai |
| Francés | Lituano | Turco |

#### Comparación de AEM 6.1 Solr search, Standard MLS y Advanced MLS {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**Nota**: AEM 6.1 se refiere a AEM 6.1 Comunidades FP3 y anteriores.

![compare-solr-mls](assets/compare-solr-mls.png)

### Instalación de MLS estándar {#installing-standard-mls}

Para la colección SRP (MSRP o DSRP), para admitir la búsqueda multilingüe estándar (MLS) es necesario modificar dos de los archivos de configuración de Solr:

* **schema.xml**
* **solrconfig.xml**

Archivos MLS estándar (schema.xml, solrconfig.xml) para Solr 4.10.

Archivos MLS estándar (schema.xml, solrconfig.xml) para Solr 5.x.

Los archivos MLS estándar se almacenan en el repositorio de AEM.

**Nota**: Aunque los archivos Solr se almacenan en la carpeta msrp/ , también son para DSRP (no es necesario realizar cambios).

**Instrucciones** de descarga: Sustituya  `solrX` por  `solr4` o  `solr5` según corresponda.

1. Usando CRXDE|Lite, busque:

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. Descargar al servidor local en el que se implementa Solr.

   * Busque la propiedad `jcr:content` del nodo `jcr:data`.
   * Seleccione `view` para iniciar la descarga.
   * Asegúrese de que los archivos se guardan con los nombres y la codificación adecuados (UTF8).

1. Siga las instrucciones de instalación para el modo independiente o de SolrCloud.

#### Modo SolrCloud: MLS estándar {#solrcloud-mode-standard-mls}

1. Instale y configure Solr en el modo SolrCloud.
1. Prepare una nueva configuración:

   1. Cree new-config-dir* como `solr-install-dir*/myconfig/`

   1. Copie el contenido del directorio de configuración de Solr existente en *new-config-dir*

      * Para Solr4: copiar `solr-install-dir/example/solr/collection1/conf/`
      * Para Solr5: copiar `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. Copie el **schema.xml** descargado y **solrconfig.xml** en *new-config-dir* para sobrescribir los archivos existentes.


1. [Cargue la nueva ](#upload-a-configuration-to-zookeeper) configuración a ZooKeeper.
1. [Cree una ](#create-a-collection) colección que especifique los parámetros necesarios, como el número de elementos compartidos, el número de réplicas y el nombre de configuración.
1. Si el nombre de configuración *no se proporcionó durante la creación de la colección, [vincule esta colección recién creada](#link-a-collection-to-a-configuration-set) con la configuración cargada a ZooKeeper.

1. Para MSRP, ejecute [MSRP Reindex Tool](msrp.md#msrp-reindex-tool), a menos que se trate de una instalación nueva.

#### Modo independiente: MLS estándar {#standalone-mode-standard-mls}

1. Instale Solr en modo independiente.
1. Si ejecuta Solr5, cree una colección1 (similar a Solr4):

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. Copia de seguridad **schema.xml** y **solrconfig.xml** en el directorio de configuración de Solr, como:

   * Para Solr4: `solr-install-dir/example/solr/collection1/conf/`
   * Creado para Solr5: `solr-install-dir/server/solr/collection1/conf/`

1. Copie el **schema.xml** descargado y **solrconfig.xml** en el mismo directorio.

1. Reinicie Solr.
1. Para MSRP, ejecute [MSRP Reindex Tool](#msrpreindextool), a menos que se trate de una instalación nueva.

### Instalación de Advanced MLS {#installing-advanced-mls}

Para que la colección SRP (MSRP o DSRP) admita MLS avanzados, se requieren nuevos complementos Solr, además de un esquema personalizado y una configuración Solr. Todos los elementos necesarios se empaquetan en un archivo zip descargable. Además, se incluye un script de instalación para su uso cuando se implementa Solr en modo independiente.

Para obtener el paquete MLS avanzado, consulte [AEM Advanced MLS](deploy-communities.md#aem-advanced-mls) en la sección de implementación de la documentación.

Para comenzar con la instalación para SolrCloud o el modo independiente:

* Descargue el archivo zip AEM-SOLR-MLS en el servidor que hospeda Solr.
* Desempaquete el archivo.

#### Modo SolrCloud: MLS avanzado {#solrcloud-mode-advanced-mls}

Instrucciones de instalación: tenga en cuenta las pocas diferencias entre Solr4 y Solr5:

1. Instale y configure Solr en el modo SolrCloud.
1. Extraiga el contenido del paquete Advanced MLS al disco. El contenido debe incluir:

   * **schema.xml**
   * **solrconfig.xml**
   * **palabras clave/** carpeta
   * **perfiles/** carpeta
   * **extra-libs/** folder

1. Prepare una nueva configuración:

   1. Crear un *new-config-dir*

      * Por ejemplo, `solr-install-dir/myconfig/`
      * Crear subcarpetas `stopwords/` y `lang/`
   1. Copie el contenido del directorio de configuración de Solr existente en *new-config-dir*

      * Para Solr4: Copiar `solr-install-dir/example/solr/collection1/conf/`
      * Para Solr5: Copiar `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. Copie el **schema.xml** extraído y **solrconfig.xml** en *new-config-dir* para sobrescribir los archivos existentes.
   1. Para Solr5: Copiar `solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt` en `new-config-dir/lang/`
   1. Copie la carpeta **stopwords/** extraída a *new-config-dir* que resulta en `new-config-dir/stopwords/*.txt`



1. [Cargar la nueva ](#upload-a-configuration-to-zookeeper) configuración a ZooKeeper
1. Copie la nueva carpeta **profiles/** ...

   * Para Solr4: Copiar a los recursos/carpeta de cada nodo
   * Para Solr5: Copie en cada carpeta server/resources/ de la instalación de Solr. Si todos los nodos están en el mismo directorio de instalación de Solr, este paso se realiza solo una vez.

1. Cree una carpeta **lib/** en el directorio solr-home (contiene solr.xml) de cada nodo en SolrCloud. Copie jars de las siguientes ubicaciones a la nueva carpeta lib/ en cada nodo:

   * **extra-libs/** extraído del paquete MLS avanzado
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

1. [Cree una ](#create-a-collection) colección que especifique los parámetros necesarios, como el número de elementos compartidos, el número de réplicas y el nombre de configuración.
1. Si el nombre de configuración fue *not* proporcionado durante la creación de la colección, [vincule esta colección recién creada](#link-a-collection-to-a-configuration-set) con la configuración cargada a ZooKeeper.

1. Para MSRP, ejecute [MSRP Reindex Tool](#msrpreindextool), a menos que se trate de una instalación nueva.

#### Modo independiente: MLS avanzado {#standalone-mode-advanced-mls}

Se incluye un script de instalación en el paquete MLS avanzado.

Una vez extraído el contenido del paquete en el servidor que aloja el servidor independiente Solr, simplemente ejecute el script de instalación para instalar los recursos y archivos de configuración necesarios.

* Instale Solr en modo independiente.
* Si ejecuta Solr5, cree una colección1 (similar a Solr4):

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* Ejecute el script de instalación: Instalar [-v 4|5] [-d solrhome] [-c ruta de recopilación]
donde:

   * -d solrhome

      Directorio de instalación de Solr

   * -c ruta de recopilación

      Ruta de recopilación en solr

   * --ayuda

      Imprimir opciones de línea de comandos

   * -v [4|5]

      Configurar versión para solr

* Ejemplo para Solr 4.10.4:

   * Install.bat -v 4 -d c:/solr-4.10.4 -c:/solr-4.10.4/example/solr/collection1

* Ejemplo para Solr 5.4.0:

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**Nota**:

* El script de instalación hará una copia de seguridad de schema.xml y solrconfig.xml antes de instalar nuevas versiones añadiendo &quot;.orig&quot;

### Acerca de solrconfig.xml {#about-solrconfig-xml}

El archivo **solrconfig.xml** controla el intervalo de autoconfirmación y la visibilidad de la búsqueda y requerirá pruebas y ajustes.

`<autoCommit>`: De forma predeterminada, el intervalo de confirmación automática, que es una confirmación sólida para el almacenamiento estable, se establece en 15 segundos. La visibilidad de la búsqueda usa de forma predeterminada el índice de preconfirmación.

Para cambiar la búsqueda y utilizar un índice actualizado para reflejar los cambios debidos a la confirmación, cambie el contenido `openSearcher` a verdadero.

`autoSoftCommit`: Una confirmación &quot;suave&quot; garantiza que los cambios sean visibles (el índice se actualiza), pero no garantiza que los cambios se sincronicen con el almacenamiento estable (confirmación dura). El resultado es una mejora en el rendimiento. De forma predeterminada, `autoSoftCommit` está desactivado con el `maxTime` contenido establecido en -1.
