---
title: Configuración de Solr para SRP
seo-title: Configuración de Solr para SRP
description: Una instalación de Apache Solr puede compartirse entre el almacén de nodos (Oak) y el almacén común (SRP) mediante diferentes colecciones
seo-description: Una instalación de Apache Solr puede compartirse entre el almacén de nodos (Oak) y el almacén común (SRP) mediante diferentes colecciones
uuid: 7356343d-073c-4266-bdcb-c7e999281476
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e228f1db-91ea-4ec3-86da-06d89d74bc72
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración de Solr para SRP {#solr-configuration-for-srp}

## Solr para la plataforma AEM {#solr-for-aem-platform}

Se puede compartir una instalación de [Apache Solr](https://lucene.apache.org/solr/) entre el almacén [de](../../help/sites-deploying/data-store-config.md) nodos (Oak) y el almacén [](working-with-srp.md) común (SRP) utilizando diferentes colecciones.

Si las colecciones Oak y SRP se utilizan intensamente, se puede instalar un segundo Solr por motivos de rendimiento.

Para los entornos de producción, el modo [](#solrcloud-mode) SolrCloud ofrece un rendimiento mejorado respecto al modo independiente (una única configuración local de Solr).

### Requisitos {#requirements}

Descargar e instalar Apache Solr:

* [Versión 4.10](https://archive.apache.org/dist/lucene/solr/4.10.4/) o [versión 5](https://archive.apache.org/dist/lucene/solr/5.5.3/)

* Solr requiere Java 1.7 o superior
* No se necesita ningún servicio
* Opción de modos de ejecución:

   * Modo independiente
   * [Modo](#solrcloud-mode) SolrCloud (recomendado para entornos de producción)

* Opción de búsqueda multilingüe (MLS)

   * [Instalación de MLS estándar](#installing-standard-mls)
   * [Instalación de MLS avanzados](#installing-advanced-mls)

## Modo SolrCloud {#solrcloud-mode}

[Se recomienda el modo SolrCloud](https://cwiki.apache.org/confluence/display/solr/SolrCloud) para los entornos de producción. Cuando se ejecuta en modo SolrCloud, SolrCloud debe instalarse y configurarse antes de instalar la búsqueda multilingüe (MLS).

La recomendación es seguir las instrucciones de SolrCloud para la instalación:

* 3 nodos de SolrCloud en el mismo servidor
* Un Apache ZooKeeper externo

También se recomienda configurar JVM para ajustar el uso de la memoria y la recolección de elementos no utilizados.

### Ejemplo de configuración de JVM {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:MaxPermSize=768M -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### Comandos de configuración de SolrCloud {#solrcloud-setup-commands}

Cuando se ejecuta en modo SolrCloud, antes de la instalación de MLS, es necesario utilizar y conocer los siguientes comandos de configuración de SolrCloud.

#### 1. Cargar una configuración en ZooKeeper {#upload-a-configuration-to-zookeeper}

Referencia:
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

Uso:
sh ./scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost, *servidor:puerto* \
-confname *myconfig-name *\
-solrhome *solr-home-path* \
-confidir *config-dir*

#### 2.Creación de una colección {#create-a-collection}

Referencia:
[https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create](https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create)

Uso:
./bin/solr create \
-c *mycollection-name*\
-d *config-dir* \
-n *myconfig-name* \
-p *puerto*\
-s *número de partes* \
-rf *número de réplicas*

#### 3. Vinculación de una colección a un conjunto de configuración {#link-a-collection-to-a-configuration-set}

Vincule una colección a una configuración ya cargada a ZooKeeper.

Referencia:
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

Uso:
sh ./scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost, *servidor:puerto* \
-collection *mycollection-name* \
-confname *myconfig-name*

### Comparación de MLS estándar y avanzado {#comparison-of-standard-and-advanced-mls}

La búsqueda multilingüe (MLS) para comunidades AEM está diseñada para la plataforma Solr a fin de proporcionar una búsqueda mejorada en todos los idiomas admitidos, incluido el inglés.

MLS para comunidades AEM está disponible como MLS estándar o MLS avanzado. MLS estándar solo incluye la configuración de Solr y excluye los complementos o archivos de recursos. Advanced MLS es una solución más completa que incluye la configuración de Solr, así como complementos y recursos relacionados

MLS estándar incluye mejoras para la búsqueda de contenido en los siguientes idiomas:

* Inglés: se ha mejorado el sistema para intentar hacer coincidir derivaciones de palabras
* Japonés: token japonés mejorado para caracteres de ancho medio

MLS avanzado incluye mejoras para la búsqueda de contenido en los siguientes idiomas:

* Inglés: tallo sustituido por lemmatizer
* Alemán: descomponedor agregado
* Francés: se ha añadido la gestión de elisiones
* Chino (simplificado): agregó un token más inteligente
* Varios idiomas: se ha añadido un sistema, una lista de palabras de detención y un normalizador.

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

#### Comparación de la búsqueda de AEM 6.1 Solr, MLS estándar y MLS avanzado {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**Nota**: AEM 6.1 hace referencia a AEM 6.1 Communities FP3 y versiones anteriores.

![chlimage_1-283](assets/chlimage_1-283.png)

### Instalación de MLS estándar {#installing-standard-mls}

Para la colección SRP (MSRP o DSRP), para admitir la búsqueda multilingüe estándar (MLS) es necesario modificar dos de los archivos de configuración de Solr:

* **schema.xml**
* **solrconfig.xml**

Archivos MLS estándar (schema.xml, solrconfig.xml) para Solr 4.10

Archivos MLS estándar (schema.xml, solrconfig.xml) para Solr 5

Los archivos MLS estándar se almacenan en el repositorio de AEM.

**Nota**: Mientras los archivos Solr se almacenan en la carpeta msrp/, también son para DSRP (no se necesitan cambios).

**Instrucciones** de descarga: reemplazar `solrX` por `solr4` o `solr5` según proceda

1. Con CRXDE|Lite, busque

   * /libs/social/config/datastore/msrp/*solrX*/**schema.xml**
   * /libs/social/config/datastore/msrp/*solrX*/**solrconfig.xml**

1. Descargar en el servidor local en el que se implementa Solr

   * Localizar la `jcr:content` propiedad del `jcr:data` nodo
   * Seleccione `view` para iniciar la descarga
   * Asegúrese de guardar los archivos con los nombres y la codificación adecuados (UTF8)

1. Siga las instrucciones de instalación para el modo independiente o de SolrCloud

#### Modo SolrCloud: MLS estándar {#solrcloud-mode-standard-mls}

1. Instalar y configurar Solr en modo SolrCloud
1. Preparar una nueva configuración:

   1. Cree *new-config-dir* como *solr-install-dir*/myconfig/

   1. Copie el contenido del directorio de configuración Solr existente en *new-config-dir*

      * Para Solr4: copy *solr-install-dir*/example/solr/collection1/conf/&amp;ast;
      * Para Solr5: copy *solr-install-dir*/server/solr/configsets/data_guided_schema_configs/&amp;ast;
   1. Copie los archivos **schema.xml** y **solrconfig.xml** descargados en *new-config-dir* para sobrescribir los archivos existentes


1. [Cargar la nueva configuración](#upload-a-configuration-to-zookeeper) en ZooKeeper
1. [Cree una colección](#create-a-collection) que especifique los parámetros necesarios, como el número de partes compartidas, el número de réplicas y el nombre de configuración.
1. Si el nombre de configuración *no se proporcionó durante la creación de la colección, [vincule esta colección](#link-a-collection-to-a-configuration-set) recién creada con la configuración cargada a ZooKeeper

1. Para MSRP, ejecute [MSRP Reindex Tool](msrp.md#msrp-reindex-tool), a menos que se trate de una nueva instalación

#### Modo independiente: MLS estándar {#standalone-mode-standard-mls}

1. Instalar Solr en modo independiente
1. Si ejecuta Solr5, cree una colección1 (similar a Solr4):

   * ./bin/solr start
   * ./bin/solr create_core -c collection1 -d sample_techproducts_configs

1. Realice una copia de seguridad de **schema.xml** y **solrconfig.xml** en el directorio de configuración de Solr, como por ejemplo:

   * Para Solr4: *solr-install-dir*/example/solr/collection1/conf/
   * Creado para Solr5: *solr-install-dir*/server/solr/collection1/conf/

1. Copie los **esquemas.xml** y **solrconfig.xml** descargados en el mismo directorio

1. Reiniciar Solr
1. Para MSRP, ejecute [MSRP Reindex Tool](#msrpreindextool), a menos que se trate de una nueva instalación

### Instalación de MLS avanzados {#installing-advanced-mls}

Para que la colección SRP (MSRP o DSRP) admita MLS avanzados, se necesitan nuevos complementos Solr además de un esquema personalizado y una configuración Solr. Todos los elementos necesarios se empaquetan en un archivo zip descargable. Además, se incluye una secuencia de comandos de instalación para su uso cuando se implementa Solr en modo independiente.

Para obtener el paquete MLS avanzado, consulte [AEM Advanced MLS](deploy-communities.md#aem-advanced-mls) en la sección de implementación de la documentación.

Para comenzar con la instalación para SolrCloud o modo independiente:

* Descargar el archivo zip AEM-SOLR-MLS en el servidor que aloja Solr
* Desempaquetar el archivo

#### Modo SolrCloud: MLS avanzado {#solrcloud-mode-advanced-mls}

Instrucciones de instalación: tenga en cuenta las pocas diferencias entre Solr4 y Solr5:

1. Instalar y configurar Solr en modo SolrCloud
1. Extraiga el contenido del paquete MLS avanzado al disco. El contenido debe incluir:

   * **schema.xml**
   * **solrconfig.xml**
   * **Palabras clave/** carpeta
   * **perfiles/** carpeta
   * **extra-libs/** folder

1. Preparar una nueva configuración:

   1. Crear un *nuevo directorio-config*

      * Como *solr-install-dir*/myconfig/
      * Crear subcarpetas palabras clave/ y lang/
   1. Copie el contenido del directorio de configuración de Solr existente en *new-config-dir*

      * Para Solr4: Copiar *solr-install-dir*/example/solr/collection1/conf/&amp;ast;
      * Para Solr5: Copiar *solr-install-dir*/server/solr/configsets/data_guided_schema_configs/&amp;ast;
   1. Copie el **esquema.xml** y **solrconfig.xml** extraídos en *new-config-dir* para sobrescribir los archivos existentes
   1. Para Solr5: Copie *solr_install_dir*/server/solr/configsets/sample_techproducts_configs/conf/lang/&amp;ast;.txt&quot; en *new-config-dir*/lang/
   1. Copie la **carpeta/** palabras clave extraídas en *new-config-dir* , lo que resulta en *new-config-dir*/stopwords/&amp;ast;.txt



1. [Cargar la nueva configuración](#upload-a-configuration-to-zookeeper) en ZooKeeper
1. Copiar los nuevos **perfiles/** carpeta ...

   * Para Solr4: Copiar en los recursos/carpetas de cada nodo
   * Para Solr5: Copie en cada carpeta server/resources/ de la instalación de Solr. Si todos los nodos están en el mismo directorio de instalación de Solr, este paso se realiza una sola vez.

1. Cree una **carpeta lib/** en el directorio solr-home (contiene solr.xml) de cada nodo en SolrCloud. Copie los tarros de las siguientes ubicaciones en la nueva carpeta lib/ de cada nodo:

   * **extra-libs/** extraído del paquete MLS avanzado
   * *solr-install-dir/contrib/extract/lib/*.jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *solr-install-dir/contrib/clustering/lib/*.jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr-install-dir/contrib/langid/lib/*.jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *solr-install-dir/contrib/Velocity/lib/*.jar
   * *solr-install-dir/dist/solr-Velocity*.jar
   * *solr-install-dir/contrib/analysis-extras/lib/*.jar
   * *solr-install-dir/contrib/analysis-extras/lucene-libs/*.jar

1. [Cree una colección](#create-a-collection) que especifique los parámetros necesarios, como el número de partes compartidas, el número de réplicas y el nombre de configuración.
1. Si *no se proporcionó* el nombre de configuración durante la creación de la colección, [vincule esta colección](#link-a-collection-to-a-configuration-set) recién creada con la configuración cargada a ZooKeeper

1. Para MSRP, ejecute [MSRP Reindex Tool](#msrpreindextool), a menos que se trate de una nueva instalación

#### Modo independiente: MLS avanzado {#standalone-mode-advanced-mls}

Se incluye una secuencia de comandos de instalación en el paquete MLS avanzado.

Después de extraer el contenido del paquete en el servidor que aloja el servidor independiente de Solr, simplemente ejecute la secuencia de comandos de instalación para instalar los recursos y archivos de configuración necesarios.

* Instalar Solr en modo independiente
* Si ejecuta Solr5, cree una colección1 (similar a Solr4):

   * ./bin/solr start
   * ./bin/solr create_core -c collection1 -d sample_techproducts_configs

* Ejecute la secuencia de comandos de instalación: Install [-v 4|5] [-d solrhome] [-c collection path]donde:

   * -d inicio único

      Directorio de instalación de Solr

   * -c ruta de recopilación

      Ruta de recopilación en sollo

   * --ayuda

      Imprimir opciones de línea de comandos

   * -v [4|5]

      Configurar versión para solr

* Ejemplo de Solr 4.10.4:

   * Install.bat -v 4 -d c:/solr-4.10.4 -c:/solr-4.10.4/example/solr/collection1

* Ejemplo de Solr 5.4.0:

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**Nota**:

* La secuencia de comandos de instalación realizará una copia de seguridad de schema.xml y solrconfig.xml antes de instalar nuevas versiones añadiendo &quot;.orig&quot;

### Acerca de solrconfig.xml {#about-solrconfig-xml}

El archivo **solrconfig.xml** controla el intervalo de autoconfirmación y la visibilidad de la búsqueda y requerirá pruebas y ajustes.

&lt;autoCommit>: De forma predeterminada, el intervalo de Autoconfirmación, que es una confirmación dura del almacenamiento estable, se establece en 15 segundos. La visibilidad de búsqueda utiliza de forma predeterminada el índice de preconfirmación.

Para cambiar la búsqueda y utilizar un índice actualizado para reflejar los cambios debidos a la confirmación, cambie el &lt;openSearcher> contenido a true.

&lt;autoSoftCommit>: Una confirmación &#39;suave&#39; garantiza que los cambios sean visibles (el índice se actualiza), pero no garantiza que los cambios se sincronizen con almacenamiento estable (confirmación dura). El resultado es una mejora en el rendimiento. De forma predeterminada, &lt;autoSoftCommit> está deshabilitado con el &lt;maxTime> contenido establecido en -1.
