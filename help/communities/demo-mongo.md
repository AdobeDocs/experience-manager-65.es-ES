---
title: Cómo configurar MongoDB para la demostración
description: Cómo configurar MSRP para una instancia de autor y una instancia de publicación
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 7e257b34-a0f5-47db-b1a9-e26333c287d9
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# Cómo configurar MongoDB para la demostración {#how-to-setup-mongodb-for-demo}

## Introducción {#introduction}

Este tutorial describe cómo configurar [MSRP](msrp.md) para *una instancia de autor* y *una instancia de publicación*.

Con esta configuración, se puede acceder al contenido de la comunidad desde los entornos de creación y publicación sin necesidad de reenviar o revertir el contenido generado por el usuario (UGC).

Esta configuración es adecuada para *entornos que no son de producción*, como para desarrollo o demostración.

**Un entorno de *producción* debería:**

* Ejecutar MongoDB con un conjunto de réplicas
* Usar SolrCloud
* Contiene varias instancias de editor

## MongoDB {#mongodb}

### Instalar MongoDB {#install-mongodb}

* Descargar MongoDB desde [https://www.mongodb.com/](https://www.mongodb.com/)

   * Opción de SO:

      * Linux®
      * Mac 10.8
      * Windows 7

   * Elección de la versión:

      * Como mínimo, utilice la versión 2.6

* Configuración básica

   * Siga las instrucciones de instalación de MongoDB.
   * Configure para mongood:

      * No es necesario configurar los móngos ni el uso compartido.

   * La carpeta MongoDB instalada se llama &lt;mongo-install>.
   * La ruta del directorio de datos definida se denomina &lt;mongo-dbpath>.

* AEM MongoDB se puede ejecutar en el mismo host que el de los servidores de red o ejecutar de forma remota.

### Iniciar MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mongood —dbpath &lt;mongo-dbpath>

Se inicia un servidor MongoDB mediante el 27017 de puerto predeterminado.

* Para Mac, aumente ulimit con el argumento de inicio &quot;ulimit -n 2048&quot;

>[!NOTE]
>
>AEM AEM Si MongoDB se inicia *después de*, **reinicia** todas las instancias de **** para que se conecten correctamente a MongoDB.

### Opción de producción de demostración: Configurar conjunto de réplicas de MongoDB {#demo-production-option-setup-mongodb-replica-set}

Los siguientes comandos son un ejemplo de cómo configurar un conjunto de réplicas con 3 nodos en localhost:

* `bin/mongod --port 27017 --dbpath data --replSet rs0&`
* `bin/mongo`

   * `cfg = {"_id": "rs0","version": 1,"members": [{"_id": 0,"host": "127.0.0.1:27017"}]}`
   * `rs.initiate(cfg)`

* `bin/mongod --port 27018 --dbpath data1 --replSet rs0&`
* `bin/mongod --port 27019 --dbpath data2 --replSet rs0&`
* `bin/mongo`

   * `rs.add("127.0.0.1:27018")`
   * `rs.add("127.0.0.1:27019")`
   * `rs.status()`

## Solr {#solr}

### Instalar Solr {#install-solr}

* Descargar Solr desde [Apache Lucene](https://archive.apache.org/dist/lucene/solr/):

   * Adecuado para cualquier sistema operativo.
   * Solr versión 7.0.
   * Solr requiere Java™ 1.7 o superior.

* Configuración básica

   * Siga &#39;ejemplo&#39; de configuración de Solr.
   * No se necesita ningún servicio.
   * La carpeta Solr instalada se denomina &lt;solr-install>.

### Configuración de Solr para AEM Communities {#configure-solr-for-aem-communities}

Para configurar una colección Solr para MSRP para demostración, hay dos decisiones que se deben tomar (seleccione los vínculos a la documentación principal para obtener detalles):

1. Ejecute Solr en modo independiente o [SolrCloud](msrp.md#solrcloudmode).
1. Instalar [búsqueda multilingüe estándar](msrp.md#installingstandardmls) o [avanzada](msrp.md#installingadvancedmls) (MLS).

### Solr independiente {#standalone-solr}

El método para ejecutar Solr puede variar según la versión y la forma de instalación. La [guía de referencia de Solr](https://archive.apache.org/dist/lucene/solr/ref-guide/) es la documentación autorizada.

Para simplificar, utilizando la versión 4.10 como ejemplo, inicie Solr en modo independiente:

* cd to &lt;solrinstall>/example
* Java™ -jar start.jar

Este proceso inicia un servidor HTTP Solr utilizando el puerto predeterminado 8983. Puede ir a la consola de Solr para obtener una consola de Solr para realizar pruebas.

* consola Solr predeterminada: [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Si la consola Solr no está disponible, compruebe los registros en &lt;solrinstall>/example/logs. Compruebe si SOLR está intentando enlazar con un nombre de host específico que no se pueda resolver (por ejemplo, &quot;user-macbook-pro&quot;).
>
Si es así, actualice el archivo `etc/hosts` con una nueva entrada para este nombre de host (por ejemplo, 127.0.0.1 user-macbook-pro) para iniciar Solr correctamente.

### Solr Cloud {#solrcloud}

Para ejecutar una configuración básica (que no sea de producción) de solrCloud, inicie solr con:

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## Identificar MongoDB como almacén común {#identify-mongodb-as-common-store}

AEM Inicie las instancias de creación y publicación de la instancia de la publicación, si es necesario.

AEM AEM Si se estaba ejecutando antes de que se iniciara MongoDB, entonces se deben reiniciar las instancias de.

Siga las instrucciones de la página de documentación principal: [MSRP - Almacén común de MongoDB](msrp.md)

## Prueba {#test}

Para probar y verificar el almacén común de MongoDB, publique un comentario en la instancia de publicación y visualícelo en la instancia de autor, y vea el UGC en MongoDB y Solr:

1. En la instancia de publicación, vaya a la página [Guía de componentes de la comunidad](http://localhost:4503/content/community-components/en/comments.html) y seleccione el componente Comentarios.
1. Inicie sesión para publicar un comentario:
1. Escriba texto en el cuadro de entrada de texto del comentario y haga clic en **[!UICONTROL Post]**

   ![comentario posterior](assets/post-comment.png)

1. Solo tiene que ver el comentario en la [instancia de autor](http://localhost:4502/content/community-components/en/comments.html) (probablemente aún haya iniciado sesión como administrador/administrador).

   ![comentario-vista](assets/view-comment.png)

   Nota: Aunque hay nodos JCR bajo *asipath* en el autor, estos nodos son para el marco SCF. El UGC real no está en JCR, está en MongoDB.

1. Ver el UGC en mongodb **[!UICONTROL Communities]** > **[!UICONTROL Colecciones]** > **[!UICONTROL Contenido]**

   ![ugc-content](assets/ugc-content.png)

1. Vea el UGC en Solr:

   * Vaya al panel de Solr: [http://localhost:8983/solr/](http://localhost:8983/solr/).
   * El usuario `core selector` para seleccionar `collection1`.
   * Seleccione `Query`.
   * Seleccione `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## Resolución de problemas {#troubleshooting}

### No aparece UGC {#no-ugc-appears}

1. Asegúrese de que MongoDB está instalado y se ejecuta correctamente.

1. Asegúrese de que MSRP se ha configurado para ser el proveedor predeterminado:

   * AEM AEM En todas las instancias de creación y publicación de la publicación, vuelva a visitar la [consola de configuración de almacenamiento](srp-config.md) o compruebe el repositorio de la:

   * En JCR, si [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) no contiene un nodo [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc), significa que el proveedor de almacenamiento es JSRP.
   * Si el nodo srpc existe y contiene el nodo [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), las propiedades de defaultconfiguration deben definir MSRP como el proveedor predeterminado.

1. AEM Asegúrese de que se ha reiniciado la después de seleccionar MSRP.
