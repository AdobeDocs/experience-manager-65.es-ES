---
title: Esenciales de búsqueda
seo-title: Esenciales de búsqueda
description: Buscar en comunidades
seo-description: Buscar en comunidades
uuid: 5f35a033-2069-499e-9cdb-db25781312f0
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 300aa9f3-596f-42bc-8d46-e535f2bc4379
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Esenciales de búsqueda {#search-essentials}

## Información general {#overview}

La función de búsqueda es una característica esencial de las comunidades AEM. Además de las funciones de búsqueda [de la plataforma](../../help/sites-deploying/queries-and-indexing.md) AEM, AEM Communities proporciona la API [de búsqueda](#ugc-search-api) UGC para buscar contenido generado por el usuario (UGC). UGC tiene propiedades únicas, ya que se introduce y se almacena de forma independiente de otros datos de usuario y de contenido de AEM.

En el caso de las comunidades, las dos cosas que generalmente se buscan son:

* Contenido publicado por miembros de la comunidad

   * Utiliza la API de búsqueda UGC de AEM Communities

* Usuarios y grupos de usuarios (datos de usuario)

   * Utiliza las capacidades de búsqueda de la plataforma AEM

Esta sección de la documentación es de interés para los desarrolladores que crean componentes personalizados que crean o administran UGC.

## Nodos de seguridad y sombra {#security-and-shadow-nodes}

Para un componente personalizado, es necesario utilizar los métodos [SocialResourceUtilities](socialutils.md#socialresourceutilities-package) . Los métodos de utilidad que crean y buscan UGC establecerán los nodos [de](srp.md#about-shadow-nodes-in-jcr) sombra necesarios y garantizarán que el miembro tenga los permisos correctos para la solicitud.

Lo que no se administra mediante las utilidades de SRP son propiedades relacionadas con la moderación.

Consulte [SRP y UGC Essentials](srp-and-ugc.md) para obtener información sobre los métodos de utilidad utilizados para acceder a nodos de sombra UGC y ACL.

## API de búsqueda UGC {#ugc-search-api}

El almacén [común](working-with-srp.md) UGC lo proporciona uno de los diversos proveedores de recursos de almacenamiento (SRP), cada uno de los cuales posiblemente tenga un idioma de consulta nativo diferente. Por lo tanto, independientemente del SRP elegido, el código personalizado debe utilizar métodos del paquete [de API de](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) UGC (*com.adobe.cq.social.ugc.api*) que invocarán el lenguaje de consulta apropiado para el SRP seleccionado.

### Búsquedas ASRP {#asrp-searches}

Para [ASRP](asrp.md), UGC se almacena en Adobe Cloud. Aunque UGC no está visible en CRX, la [moderación](moderate-ugc.md) está disponible tanto en los entornos de autor como de publicación. El uso de la API [de búsqueda](#ugc-search-api) UGC funciona para ASRP igual que para otros SRP.

Actualmente no existen herramientas para administrar las búsquedas ASRP.

Al crear propiedades personalizadas en las que se pueden realizar búsquedas, es necesario cumplir los requisitos [de](#naming-of-custom-properties)nomenclatura.

### Búsquedas del MSRP {#msrp-searches}

Para [MSRP](msrp.md), UGC se almacena en MongoDB configurado para utilizar Solr para la búsqueda. UGC no estará visible en CRX, pero la [moderación](moderate-ugc.md) está disponible tanto en los entornos de autor como de publicación.

Respecto del MSRP y Solr:

* El Solr incrustado para la plataforma AEM no se utiliza para MSRP
* Si se utiliza un Solr remoto para la plataforma AEM, puede compartirse con MSRP, pero deben utilizar diferentes colecciones
* Solr se puede configurar para la búsqueda estándar o para la búsqueda multilingüe (MLS)
* Para obtener más información sobre la configuración, consulte [Configuración](msrp.md#solr-configuration) de Solr para MSRP

Las funciones de búsqueda personalizada deben utilizar la API [de búsqueda de](#ugc-search-api)UGC.

Al crear propiedades personalizadas en las que se pueden realizar búsquedas, es necesario cumplir los requisitos [de](#naming-of-custom-properties)nomenclatura.

### Búsquedas JSRP {#jsrp-searches}

Para [JSRP](jsrp.md), UGC se almacena en [Oak](../../help/sites-deploying/platform.md) y solo es visible en el repositorio de la instancia de publicación o autor de AEM en la que se introdujo.

Dado que, normalmente, se introduce UGC en el entorno de publicación, para los sistemas de producción de varios publicadores es necesario configurar un clúster [de](topologies.md)publicación, no un conjunto de servidores de publicación, de modo que el contenido introducido esté visible desde todos los editores.

Para JSRP, la UGC introducida en el entorno de publicación nunca será visible en el entorno de creación. Por lo tanto, todas las tareas de [moderación](moderate-ugc.md) se realizan en el entorno de publicación.

Las funciones de búsqueda personalizada deben utilizar la API [de búsqueda de](#ugc-search-api)UGC.

#### Indexación de roble {#oak-indexing}

Aunque los índices Oak no se crean automáticamente para la búsqueda de plataformas AEM, a partir de AEM 6.2 se han añadido para comunidades AEM para mejorar el rendimiento y ofrecer compatibilidad con la paginación al presentar los resultados de la búsqueda UGC.

Si las propiedades personalizadas están en uso y las búsquedas son lentas, será necesario crear índices adicionales para las propiedades personalizadas a fin de aumentar su rendimiento. Para mantener la portabilidad, cumpla los requisitos [de](#naming-of-custom-properties) nomenclatura al crear propiedades personalizadas en las que se pueden realizar búsquedas.

Para modificar índices existentes o crear índices personalizados, consulte [Consultas de Oak e Indexación](../../help/sites-deploying/queries-and-indexing.md).

El [Oak Index Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) está disponible en ACS AEM Commons. Proporciona:

* Vista de los índices existentes
* La capacidad para iniciar la reindexación

Para ver los índices Oak existentes en [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md), la ubicación es:

* `/oak:index/socialLucene`

![chlimage_1-235](assets/chlimage_1-235.png)

## Propiedades de búsqueda indizadas {#indexed-search-properties}

### Propiedades de búsqueda predeterminadas {#default-search-properties}

A continuación se indican algunas de las propiedades que se pueden buscar y que se utilizan para diversas funciones de Comunidades:

| **Propiedad** | **Tipo de datos** |
|---|---|
| isFlagged | *Booleano* |
| isSpam | *Booleano* |
| read | *Booleano* |
| influir | *Booleano* |
| adjuntos | *Booleano* |
| opinión | *Largo* |
| marcado | *Booleano* |
| añadido | *Fecha* |
| modifiedDate | *Fecha* |
| estado | *Cadena* |
| userIdentifier | *Cadena* |
| respuestas | *Largo* |
| jcr:title | *Cadena* |
| jcr:description | *Cadena* |
| sling:resourceType | *Cadena* |
| allowThreadedReply | *Booleano* |
| isDraft | *Booleano* |
| publishDate | *Fecha* |
| publishJobId | *Cadena* |
| con respuesta | *Booleano* |
| chosenanswer | *Booleano* |
| tag | *Cadena* |
| cq:Tag | *Cadena* |
| author_display_name | *Cadena* |
| location_t | *Cadena* |
| parentPath | *Cadena* |
| parentTitle | *Cadena* |

### Asignación de nombres a las propiedades personalizadas {#naming-of-custom-properties}

Al agregar propiedades personalizadas, para que dichas propiedades puedan ser visibles para ordenarse y buscar creadas con la API [de búsqueda](#ugc-search-api)UGC, *es necesario *agregar un sufijo al nombre de la propiedad.

El sufijo es para los idiomas de consulta que utilizan un esquema:

* Identifica la propiedad como de búsqueda
* Identifica el tipo de datos

Solr es un ejemplo de un lenguaje de consulta que utiliza un esquema.

| **Sufijo** | **Tipo de datos** |
|---|---|
| _b | *Booleano* |
| _dt | *Calendario* |
| _d | *Doble* |
| _tl | *Largo* |
| _s | *Cadena* |
| _t | *Texto* |

**Notas:**

* *El texto* es una cadena con token, *la cadena* no. Use *Texto* para búsquedas borrosas (más o menos así).

* Para tipos de varios valores, añada ‘s’ al sufijo, por ejemplo:

   * `viewDate_dt`:: single date, propiedad
   * `viewDates_dts`:: list of date, propiedad

## Filtros {#filters}

Los componentes que incluyen el sistema [de](essentials-comments.md) comentarios admiten el parámetro de filtro además de sus extremos.

La sintaxis del filtro para la lógica Y y O se expresa de la siguiente manera (se muestra antes de ser codificada con la dirección URL):

* Para especificar O, utilice un parámetro de filtro con valores separados por comas:

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* Para especificar AND, utilice varios parámetros de filtro:

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

La implementación predeterminada del componente [](search.md) Buscar utiliza esta sintaxis como se puede ver en la dirección URL que abre la página Resultados de la búsqueda en la guía [Componentes de la](components-guide.md)comunidad. Para experimentar, vaya a [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

Los operadores de filtro son:

| EQ | igual a |
|---|---|
| NE | no es igual a |
| LT | menor que |
| LTE | menor o igual que |
| GE | mayor que |
| GTE | mayor o igual que |
| COMO | coincidencia confusa |

Es importante que la dirección URL haga referencia al componente Comunidades (recurso) y no a la página en la que se coloca el componente:

* Correcto: componente de foro
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* Incorrecto: página del foro
   * `/content/community-components/en/forum.social.json`

## Herramientas SRP {#srp-tools}

Hay un proyecto GitHub de Adobe Marketing Cloud que contiene:

[Herramientas SRP de AEM Communities](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Este repositorio contiene herramientas para administrar datos en SRP.

Actualmente, hay un servlet que permite eliminar todo el UGC de cualquier SRP.

Por ejemplo, para eliminar todo el UGC en ASRP:

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## Solución de problemas {#troubleshooting}

### Consulta de Solr {#solr-query}

Para ayudar a solucionar problemas con una consulta Solr, habilite el registro DEBUG para

`com.adobe.cq.social.srp.impl.SocialSolrConnector`.

La consulta Solr real se mostrará con la dirección URL codificada en el registro de depuración:

La consulta que se va a resolver es: `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

El valor del `q` parámetro es la consulta. Una vez descodificada la codificación de la dirección URL, la consulta se puede pasar a la herramienta de consulta de administración de Solr para continuar la depuración.

## Medios relacionados {#related-resources}

* [Almacenamiento](working-with-srp.md) de contenido de la comunidad: analiza las opciones de SRP disponibles para una tienda común UGC
* [Información general](srp.md) del proveedor de recursos de almacenamiento de información: Introducción y uso del repositorio
* [Acceso a UGC con SRP](accessing-ugc-with-srp.md) - Directrices de codificación
* [Refactorización](socialutils.md) de SocialUtils: métodos de utilidad para SRP que reemplazan a SocialUtils
* [Componentes](search.md) de búsqueda y resultados de búsqueda: Adición de la función de búsqueda UGC a una plantilla

