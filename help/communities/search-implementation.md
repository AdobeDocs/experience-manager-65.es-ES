---
title: Elementos básicos de búsqueda
seo-title: Search Essentials
description: Buscar en comunidades
seo-description: Search in Communities
uuid: 5f35a033-2069-499e-9cdb-db25781312f0
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 300aa9f3-596f-42bc-8d46-e535f2bc4379
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 5%

---

# Elementos básicos de búsqueda {#search-essentials}

## Información general {#overview}

La función de búsqueda es una función esencial de AEM Communities. Además del [búsqueda en AEM plataforma](../../help/sites-deploying/queries-and-indexing.md) , AEM Communities proporciona la variable [API de búsqueda UGC](#ugc-search-api) para buscar contenido generado por el usuario (UGC). UGC tiene propiedades únicas, ya que se introducen y almacenan por separado de otros contenidos AEM y datos de usuario.

Para las comunidades, las dos cosas que se buscan generalmente son:

* Contenido publicado por miembros de la comunidad

   * Utiliza la API de búsqueda UGC de AEM Communities.

* Usuarios y grupos de usuarios (datos de usuario)

   * Utiliza las capacidades de búsqueda de la plataforma AEM.

Esta sección de la documentación es de interés para los desarrolladores que crean componentes personalizados que crean o administran UGC.

## Nodos de seguridad y sombra {#security-and-shadow-nodes}

Para un componente personalizado, es necesario usar la variable [SocialResourceUtilities](socialutils.md#socialresourceutilities-package) métodos. Los métodos de utilidad que crean y buscan UGC establecerán los requisitos [nodos de sombra](srp.md#about-shadow-nodes-in-jcr) y asegúrese de que el miembro tenga los permisos correctos para la solicitud.

Lo que no se administra mediante las utilidades de SRP son propiedades relacionadas con la moderación.

Consulte [Elementos esenciales de SRP y UGC](srp-and-ugc.md) para obtener información sobre los métodos de utilidad utilizados para acceder a los nodos de sombra UGC y ACL.

## API de búsqueda UGC {#ugc-search-api}

La variable [UGC common store](working-with-srp.md) es proporcionado por uno de una variedad de proveedores de recursos de almacenamiento (SRP), cada uno de los cuales posiblemente tenga un idioma de consulta nativo diferente. Por lo tanto, independientemente del SRP elegido, el código personalizado debe utilizar métodos del [Paquete de API de UGC](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*) que invocará el idioma de consulta apropiado para el SRP elegido.

### Búsquedas ASRP {#asrp-searches}

Para [ASRP](asrp.md), UGC se almacena en la nube de Adobe. Aunque UGC no es visible en CRX, [moderación](moderate-ugc.md) está disponible en los entornos de autor y publicación. El uso de [API de búsqueda UGC](#ugc-search-api) funciona para ASRP igual que para otros SRP.

Actualmente no existen herramientas para administrar búsquedas ASRP.

Al crear propiedades personalizadas en las que se pueden buscar, es necesario adherirse a la variable [requisitos de nomenclatura](#naming-of-custom-properties).

### Búsquedas del MSRP {#msrp-searches}

Para [MSRP](msrp.md), UGC se almacena en MongoDB configurado para utilizar Solr para la búsqueda. UGC no será visible en CRX, pero [moderación](moderate-ugc.md) está disponible en los entornos de autor y publicación.

En cuanto al MSRP y Solr:

* El Solr incrustado para la plataforma AEM no se utiliza para MSRP.
* Si utiliza un Solr remoto para la plataforma AEM, puede compartirse con el MSRP, pero deben utilizar colecciones diferentes.
* Solr se puede configurar para la búsqueda estándar o para la búsqueda multilingüe (MLS).
* Para obtener más información sobre la configuración, consulte [Configuración de Solr](msrp.md#solr-configuration) para el MSRP.

Las características de búsqueda personalizadas deben usar la variable [API de búsqueda UGC](#ugc-search-api).

Al crear propiedades personalizadas en las que se pueden buscar, es necesario adherirse a la variable [requisitos de nomenclatura](#naming-of-custom-properties).

### Búsquedas JSRP {#jsrp-searches}

Para [JSRP](jsrp.md), UGC se almacena en [Oak](../../help/sites-deploying/platform.md) y solo es visible en el repositorio de la instancia de autor o publicación AEM en la que se introdujo.

Dado que UGC se introduce generalmente en el entorno de publicación, para los sistemas de producción de varios publicadores, es necesario configurar un [publicar clúster](topologies.md), no un conjunto de servidores de publicación, de modo que el contenido introducido sea visible desde todos los editores.

Para JSRP, el UGC introducido en el entorno de publicación nunca será visible en el entorno de creación. Así, todo [moderación](moderate-ugc.md) las tareas se realizan en el entorno de publicación.

Las características de búsqueda personalizadas deben usar la variable [API de búsqueda UGC](#ugc-search-api).

#### Indexación de Oak {#oak-indexing}

Aunque los índices Oak no se crean automáticamente para la búsqueda en la plataforma AEM, a partir de la AEM 6.2 se han agregado para AEM Communities para mejorar el rendimiento y proporcionar compatibilidad con la paginación al presentar los resultados de búsqueda UGC.

Si las propiedades personalizadas están en uso y las búsquedas son lentas, será necesario crear índices adicionales para las propiedades personalizadas a fin de que tengan un mayor rendimiento. Para mantener la portabilidad, siga los [requisitos de nomenclatura](#naming-of-custom-properties) al crear propiedades personalizadas que se pueden buscar.

Para modificar índices existentes o crear índices personalizados, consulte [Consultas e indexación de Oak](../../help/sites-deploying/queries-and-indexing.md).

La variable [Administrador de índices Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) está disponible en ACS AEM Commons. Proporciona:

* Una vista de los índices existentes.
* La capacidad para iniciar la reindexación.

Para ver los índices Oak existentes en [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md), la ubicación es:

* `/oak:index/socialLucene`

![social-lucene](assets/social-lucene.png)

## Propiedades de búsqueda indexadas {#indexed-search-properties}

### Propiedades de búsqueda predeterminadas {#default-search-properties}

A continuación se presentan algunas de las propiedades de búsqueda utilizadas para varias funciones de Communities:

| **Propiedad** | **Tipo de datos** |
|---|---|
| isFlagged | *Booleana* |
| isSpam | *Booleana* |
| read | *Booleana* |
| influencia | *Booleana* |
| archivos adjuntos | *Booleana* |
| opinión | *Largo* |
| marcado | *Booleana* |
| añadido | *Fecha* |
| modifiedDate | *Fecha* |
| estado | *Cadena* |
| userIdentifier | *Cadena* |
| answers | *Largo* |
| jcr:title | *Cadena* |
| jcr:description | *Cadena* |
| sling:resourceType | *Cadena* |
| allowThreadedReply | *Booleana* |
| isDraft | *Booleana* |
| publishDate | *Fecha* |
| publishJobId | *Cadena* |
| con respuesta | *Booleana* |
| chosenresponse | *Booleana* |
| etiqueta | *Cadena* |
| cq:Tag | *Cadena* |
| author_display_name | *Cadena* |
| location_t | *Cadena* |
| parentPath | *Cadena* |
| parentTitle | *Cadena* |

### Asignación de nombres a las propiedades personalizadas {#naming-of-custom-properties}

Al agregar propiedades personalizadas, para que estas propiedades puedan ser visibles para ordenar y buscar creadas con la variable [API de búsqueda UGC](#ugc-search-api), es *obligatorio* para agregar un sufijo al nombre de la propiedad.

El sufijo es para los idiomas de consulta que utilizan un esquema:

* Identifica la propiedad como de búsqueda.
* Identifica el tipo de datos.

Solr es un ejemplo de lenguaje de consulta que utiliza un esquema.

| **Sufijo** | **Tipo de datos** |
|---|---|
| _b | *Booleana* |
| _dt | *Calendario* |
| _d | *Doble* |
| _tl | *Largo* |
| _s | *Cadena* |
| _t | *Texto* |

**Notas:**

* *Texto* es una cadena con token, *Cadena* no. Uso *Texto* para búsquedas difusas (más como esta).

* Para los tipos de varios valores, añada &quot;s&quot; al sufijo, por ejemplo:

   * `viewDate_dt`: propiedad single date
   * `viewDates_dts`: list of dates, propiedad

## Filtros {#filters}

Los componentes que incluyen la variable [sistema de comentarios](essentials-comments.md) admiten el parámetro de filtro además de sus extremos.

La sintaxis del filtro para la lógica AND y OR se expresa de la siguiente manera (se muestra antes de ser codificada con la URL):

* Para especificar O use un parámetro de filtro con valores separados por comas:

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* Para especificar Y usar varios parámetros de filtro:

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

La implementación predeterminada de la variable [Componente de búsqueda](search.md) utiliza esta sintaxis como se puede ver en la dirección URL que abre la página Resultados de la búsqueda en la [Guía de componentes de comunidad](components-guide.md). Para experimentar, vaya a [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

Los operadores de filtro son:

| EQ | igual a |
|---|---|
| NE | no es igual a |
| LT | menor que |
| LTE | menor o igual que |
| GE | bueno que |
| GTE | mayor o igual que |
| LIKE | coincidencia confusa |

Es importante que la URL haga referencia al componente Comunidades (recurso) y no a la página en la que se coloca el componente:

* Correcto: componente de foro
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* Incorrecto: página del foro
   * `/content/community-components/en/forum.social.json`

## Herramientas SRP {#srp-tools}

Hay un proyecto de Adobe Marketing Cloud GitHub que contiene:

[Herramientas SRP de AEM Communities](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Este repositorio contiene herramientas para administrar datos en SRP.

Actualmente, hay un servlet que proporciona la capacidad de eliminar todo UGC de cualquier SRP.

Por ejemplo, para eliminar todo UGC en ASRP:

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## Solución de problemas {#troubleshooting}

### Consulta Solr {#solr-query}

Para ayudar a solucionar problemas con una consulta Solr, habilite el registro de DEBUG para

`com.adobe.cq.social.srp.impl.SocialSolrConnector`.

La consulta Solr real se mostrará como URL codificada en el registro de depuración:

La consulta a solr es: `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

El valor de la variable `q` es la consulta. Una vez descodificada la codificación de la URL, la consulta se puede pasar a la herramienta Solr Admin Query para depurar más.

## Medios relacionados {#related-resources}

* [Almacenamiento de contenido de la comunidad](working-with-srp.md) - Analiza las opciones de SRP disponibles para una tienda común UGC.
* [Información general del proveedor de recursos de almacenamiento](srp.md) - Introducción y descripción general del uso del repositorio.
* [Acceso a UGC con SRP](accessing-ugc-with-srp.md) - Directrices de codificación.
* [Refactorización de SocialUtils](socialutils.md) - Métodos de utilidad para SRP que reemplazan a SocialUtils.
* [Componentes de búsqueda y resultados de búsqueda](search.md) - Añadir la función de búsqueda UGC a una plantilla.
