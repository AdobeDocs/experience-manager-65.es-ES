---
title: Cómo configurar MongoDB para la demostración
seo-title: Cómo configurar MongoDB para la demostración
description: Cómo configurar MSRP para una instancia de autor y una instancia de publicación
seo-description: Cómo configurar MSRP para una instancia de autor y una instancia de publicación
uuid: d2035a9e-f05c-4f90-949d-7cdae9646750
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0b126218-b142-4d33-a28c-a91ab4fe99ac
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Cómo configurar MongoDB para la demostración {#how-to-setup-mongodb-for-demo}

## Introducción {#introduction}

Este tutorial describe cómo configurar [MSRP](msrp.md) para *una instancia de autor* y *una instancia de publicación* .

Con esta configuración, el contenido de la comunidad es accesible desde los entornos de creación y publicación sin necesidad de reenviar o revertir el contenido generado por el usuario (UGC).

Esta configuración es adecuada para entornos *que no son de producción* , como para desarrollo y/o demostración.

**Un entorno *de producción*debería:**

* Ejecutar MongoDB con un conjunto de réplicas
* Usar SolrCloud
* Contener varias instancias de publicador

## MongoDB {#mongodb}

### Instalar MongoDB {#install-mongodb}

* Descargue MongoDB de [https://www.mongodb.org/](https://www.mongodb.org/)

   * Opción de SO:

      * Linux
      * Mac 10.8
      * Windows 7
   * Elección de la versión:

      * Como mínimo, utilice la versión 2.6


* Configuración básica

   * Siga las instrucciones de instalación de MongoDB
   * Configurar para mono

      * No es necesario configurar los mongos ni el uso compartido
   * La carpeta MongoDB instalada se denominará &lt;mongo-install>
   * La ruta de acceso del directorio de datos definida se denominará &lt;mongo-dbpath>


* MongoDB puede ejecutarse en el mismo host que AEM o de forma remota

### Iniciar MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mongood —dbpath &lt;mongo-dbpath>

Esto iniciará un servidor MongoDB utilizando el puerto predeterminado 27017.

* Para Mac, aumente ulimit con el argumento de inicio &#39;ulimit -n 2048&#39;

>[!NOTE]
>
>Si MongoDB se inicia *después de *AEM, **reiniciar **todo **AEM **instancias para que se conecten correctamente a MongoDB.

### Opción de producción de demostración: Configurar conjunto de réplicas de MongoDB {#demo-production-option-setup-mongodb-replica-set}

Los siguientes comandos son un ejemplo de configuración de un conjunto de réplicas con 3 nodos en localhost:

* bin/mongood —port 27017 —dbpath data —replSet rs0&amp;
* bin/mongo

   * cfg = {&quot;_id&quot;: &quot;rs0&quot;,&quot;version&quot;: 1, &quot;miembros&quot;: [{&quot;_id&quot;: 0,&quot;host&quot;: &quot;127.0.0.1:27017&quot;}]}
   * rs.initiate(cfg)

* bin/mongood —port 27018 —dbpath data1 —replSet rs0&amp;
* bin/mongood —port 27019 —dbpath data2 —replSet rs0&amp;
* bin/mongo

   * rs.add(&quot;127.0.0.1:27018&quot;)
   * rs.add(&quot;127.0.0.1:27019&quot;)
   * rs.status()

## Solr {#solr}

### Instalar Solr {#install-solr}

* Descargar Solr de [Apache Lucene](https://archive.apache.org/dist/lucene/solr/):

   * Adecuado para cualquier SO
   * Utilice la versión 4.10 o la versión 5
   * Solr requiere Java 1.7 o superior

* Configuración básica

   * Siga la configuración de Solr de &quot;ejemplo&quot;
   * No se necesita ningún servicio
   * La carpeta Solr instalada se denominará &lt;solr-install>

### Configurar Solr para comunidades AEM {#configure-solr-for-aem-communities}

Para configurar una colección Solr para MSRP para demostración, hay que tomar dos decisiones (seleccionar los vínculos a la documentación principal para obtener más información):

1. Ejecutar Solr en modo independiente o [SolrCloud](msrp.md#solrcloudmode)
1. Instalación de búsqueda multilingüe [estándar](msrp.md#installingstandardmls) o [avanzada](msrp.md#installingadvancedmls) (MLS)

### Solar independiente {#standalone-solr}

El método de ejecución de Solr puede variar en función de la versión y el modo de instalación. La guía [de referencia](https://archive.apache.org/dist/lucene/solr/ref-guide/) Solr es la documentación autorizada.

Para simplificar, con la versión 4.10 como ejemplo, inicie Solr en modo independiente:

* cd to &lt;solrinstall>/example
* java -jar start.jar

Esto iniciará un servidor HTTP Solr usando el puerto predeterminado 8983. Puede navegar hasta la consola de Solr para obtener una consola de Solr para realizar pruebas.

* consola Solr predeterminada: [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Si la Consola de Solr no está disponible, compruebe los registros en &lt;solrinstall>/example/logs. Compruebe si SOLR está intentando enlazar a un nombre de host específico que no se puede resolver (p. ej. &quot;user-macbook-pro&quot;).
Si es así, actualice el archivo etc/hosts con una nueva entrada para este nombre de host (por ejemplo, 127.0.0.1 user-macbook-pro) y Solr se iniciará correctamente.

### SolrCloud {#solrcloud}

Para ejecutar una configuración de solrCloud muy básica (no de producción), comience con:

* java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar

## Identifique MongoDB como una tienda común {#identify-mongodb-as-common-store}

Inicie el autor y publique las instancias de AEM, si es necesario.

Si AEM se estaba ejecutando antes de que MongoDB se iniciara, entonces será necesario reiniciar las instancias de AEM.

Siga las instrucciones de la página de documentación principal: [MSRP - Tienda común MongoDB](msrp.md)

## Probar {#test}

Para probar y verificar el almacén común de MongoDB, publique un comentario en la instancia de publicación y visualícela en la instancia de autor, así como vea el UGC en MongoDB y Solr:

1. En la instancia de publicación, vaya a la página Guía [de componentes de](http://localhost:4503/content/community-components/en/comments.html) comunidad y seleccione el componente Comentarios.
1. Inicie sesión para publicar un comentario:
1. Escriba el texto en el cuadro de entrada de texto de comentario y haga clic en **[!UICONTROL Publicar]**

   ![chlimage_1-191](assets/chlimage_1-191.png)

1. Solo tiene que ver el comentario en la instancia [de](http://localhost:4502/content/community-components/en/comments.html) autor (posiblemente aún haya iniciado sesión como administrador/administrador).

   ![chlimage_1-192](assets/chlimage_1-192.png)

   Nota: aunque hay nodos JCR debajo de *asipath* en author, estos son para el marco SCF. El UGC real no está en JCR, está en MongoDB.

1. Ver el UGC en **[!UICONTROL comunidades mongodb > Colecciones > Contenido]**

   ![chlimage_1-193](assets/chlimage_1-193.png)

1. Ver UGC en Solr:

   * Vaya al tablero Solr: [http://localhost:8983/solr/](http://localhost:8983/solr/)
   * Usuario `core selector` que seleccionar `collection1`
   * Seleccione `Query`
   * Seleccione `Execute Query`
   ![chlimage_1-194](assets/chlimage_1-194.png)

## Solución de problemas {#troubleshooting}

### No aparece ningún UGC {#no-ugc-appears}

1. Asegúrese de que MongoDB esté instalado y funcionando correctamente.

1. Asegúrese de que MSRP se haya configurado para que sea el proveedor predeterminado:

   * En todas las instancias de AEM de creación y publicación, vuelva a la consola de configuración [de almacenamiento](srp-config.md)
   o compruebe el repositorio de AEM:

   * En JCR, if [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

      * No contiene un nodo [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) , significa que el proveedor de almacenamiento es JSRP
      * Si el nodo srpc existe y contiene la configuración [predeterminada](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)del nodo, las propiedades de configuración predeterminada deben definir MSRP para que sea el proveedor predeterminado


1. Asegúrese de que AEM se reinició después de seleccionar MSRP.
