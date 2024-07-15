---
title: Search Essentials
description: Obtenga información acerca de la función de búsqueda, que es una función esencial de AEM Communities. Las comunidades también proporcionan la API de búsqueda para el contenido generado por el usuario.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 3%

---

# Search Essentials {#search-essentials}

## Información general {#overview}

La función de búsqueda es una característica esencial de las comunidades de Adobe Experience Manager AEM (). AEM Además de las capacidades de [búsqueda en la plataforma ](../../help/sites-deploying/queries-and-indexing.md), AEM Communities proporciona la [API de búsqueda UGC](#ugc-search-api) para la búsqueda de contenido generado por el usuario (UGC). AEM UGC tiene propiedades únicas, ya que se introduce y almacena por separado de otros datos de usuario y de contenido de la.

Para Communities, las dos cosas que se buscan generalmente son:

* Contenido publicado por miembros de la comunidad

   * Utiliza la API de búsqueda UGC de AEM Communities.

* Usuarios y grupos de usuarios (datos de usuario)

   * AEM Utiliza las funcionalidades de búsqueda de la plataforma de.

Esta sección de la documentación es de interés para los desarrolladores que crean componentes personalizados que crean o administran UGC.

## Seguridad y nodos en la sombra {#security-and-shadow-nodes}

Para un componente personalizado, es necesario usar los métodos [SocialResourceUtilities](socialutils.md#socialresourceutilities-package). Los métodos de utilidad que crean y buscan UGC establecen los [nodos en la sombra](srp.md#about-shadow-nodes-in-jcr) necesarios y garantizan que el miembro tenga los permisos correctos para la solicitud.

Lo que no se administra mediante las utilidades SRP son propiedades relacionadas con la moderación.

Consulte [SRP y UGC Essentials](srp-and-ugc.md) para obtener información sobre los métodos de utilidad utilizados para acceder a los nodos de sombra de UGC y ACL.

## API de búsqueda UGC {#ugc-search-api}

El almacén común [UGC](working-with-srp.md) lo proporciona uno de varios proveedores de recursos de almacenamiento (SRP), cada uno de los cuales posiblemente tenga un idioma de consulta nativo diferente. Por lo tanto, independientemente del SRP elegido, el código personalizado debe utilizar métodos del [paquete de API de UGC](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*) que invoca el idioma de consulta apropiado para el SRP elegido.

### Búsquedas ASRP {#asrp-searches}

Para [ASRP](asrp.md), UGC se almacena en la nube de Adobe. Aunque UGC no es visible en CRX, la [moderación](moderate-ugc.md) está disponible en los entornos Author y Publish. El uso de la [API de búsqueda UGC](#ugc-search-api) funciona para ASRP igual que para otros SRP.

Actualmente no existen herramientas para administrar búsquedas ASRP.

Al crear propiedades personalizadas en las que se pueden realizar búsquedas, es necesario cumplir los [requisitos de nomenclatura](#naming-of-custom-properties).

### Búsquedas MSRP {#msrp-searches}

Para [MSRP](msrp.md), UGC se almacena en MongoDB configurado para usar Solr para la búsqueda. UGC no es visible en CRX, pero la [moderación](moderate-ugc.md) está disponible en los entornos Author y Publish.

Con respecto al MSRP y Solr:

* AEM El Solr incrustado para la plataforma de no se utiliza para el MSRP.
* AEM Si se utiliza un Solr remoto para la plataforma de, puede compartirse con el MSRP, pero deben utilizar colecciones diferentes.
* Solr puede configurarse para la búsqueda estándar o para la búsqueda multilingüe (MLS).
* Para obtener detalles de configuración, consulte [Configuración de Solr](msrp.md#solr-configuration) para MSRP.

Las características de búsqueda personalizada deben usar la [API de búsqueda UGC](#ugc-search-api).

Al crear propiedades personalizadas en las que se pueden realizar búsquedas, es necesario cumplir los [requisitos de nomenclatura](#naming-of-custom-properties).

### Búsquedas JSRP {#jsrp-searches}

Para [JSRP](jsrp.md), el UGC se almacena en [Oak AEM](../../help/sites-deploying/platform.md) y solo es visible en el repositorio de la instancia de autor de la o Publish en la que se ingresó.

Dado que UGC se introduce normalmente en el entorno de Publish, en los sistemas de producción de varios editores es necesario configurar un [clúster de publicación](topologies.md), no una granja de servidores de publicación, de modo que el contenido introducido sea visible desde todos los editores.

Para JSRP, el UGC introducido en el entorno de Publish nunca es visible en el entorno de creación. Por lo tanto, todas las tareas de [moderación](moderate-ugc.md) tienen lugar en el entorno de Publish.

Las características de búsqueda personalizada deben usar la [API de búsqueda UGC](#ugc-search-api).

#### Indexación de Oak {#oak-indexing}

Aunque los índices Oak AEM AEM no se crean automáticamente para la búsqueda en la plataforma de la, a partir de la versión 6.2 de la versión, se han añadido para AEM Communities a fin de mejorar el rendimiento y ofrecer compatibilidad con la paginación al presentar resultados de búsqueda UGC.

Si las propiedades personalizadas están en uso y las búsquedas son lentas, se deben crear índices adicionales para las propiedades personalizadas para que tengan un mejor rendimiento. Para mantener la portabilidad, cumpla con los [requisitos de nomenclatura](#naming-of-custom-properties) al crear propiedades personalizadas en las que se pueden realizar búsquedas.

Para modificar los índices existentes o crear índices personalizados, consulte [Consultas e indexación de Oak](../../help/sites-deploying/queries-and-indexing.md).

El [Administrador de índices Oak AEM](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) está disponible en ACS Commons. Proporciona lo siguiente:

* Una vista de los índices existentes.
* La capacidad para iniciar la reindexación.

Para ver los índices Oak existentes en [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md), la ubicación es:

* `/oak:index/socialLucene`

![social-lucene](assets/social-lucene.png)

## Propiedades de búsqueda indizada {#indexed-search-properties}

### Propiedades de búsqueda predeterminadas {#default-search-properties}

A continuación, se muestran algunas de las propiedades en las que se pueden realizar búsquedas utilizadas para diversas funciones de Communities:

| **Propiedad** | **Tipo de datos** |
|---|---|
| isFlagged | *Booleana* |
| isSpam | *Booleana* |
| leer | *Booleana* |
| influenciar | *Booleana* |
| attachments | *Booleana* |
| opinión | *Largo* |
| marcado | *Booleana* |
| añadido | *Fecha* |
| modifiedDate | *Fecha* |
| estado | *Cadena* |
| userIdentifier | *Cadena* |
| respuestas | *Largo* |
| jcr:title | *Cadena* |
| jcr:description | *Cadena* |
| sling:resourceType | *Cadena* |
| allowThreadedReply | *Booleana* |
| isDraft | *Booleana* |
| publishDate | *Fecha* |
| publishJobId | *Cadena* |
| con respuesta | *Booleana* |
| chosenanswer | *Booleana* |
| etiqueta | *Cadena* |
| cq:Etiqueta | *Cadena* |
| author_display_name | *Cadena* |
| location_t | *Cadena* |
| parentPath | *Cadena* |
| parentTitle | *Cadena* |

### Nomenclatura de propiedades personalizadas {#naming-of-custom-properties}

Al agregar propiedades personalizadas, para que esas propiedades sean visibles para las ordenaciones y búsquedas creadas con la [API de búsqueda UGC](#ugc-search-api), es *obligatorio* agregar un sufijo al nombre de la propiedad.

El sufijo es para idiomas de consulta que utilizan un esquema:

* Identifica la propiedad como una propiedad en la que se pueden buscar.
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

* *Texto* es una cadena con token, *Cadena* no. Use *Texto* para búsquedas difusas (más parecidas a esta).

* Para los tipos de varios valores, agregue &quot;s&quot; al sufijo, por ejemplo:

   * `viewDate_dt`: propiedad de fecha única
   * `viewDates_dts`: lista de propiedad de fechas

## Filtros {#filters}

Los componentes, que incluyen el [sistema de comentarios](essentials-comments.md), admiten el parámetro de filtro además de sus extremos.

La sintaxis del filtro para la lógica AND y OR se expresa de la siguiente manera (se muestra antes de codificarse con URL):

* Para especificar OR, utilice un parámetro de filtro con valores separados por comas:

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* Para especificar AND, utilice varios parámetros de filtro:

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

La implementación predeterminada de [Search component](search.md) usa esta sintaxis, como se puede ver en la dirección URL que abre la página de resultados de búsqueda en la [guía de componentes de la comunidad](components-guide.md). Para experimentar, vaya a [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

Los operadores de filtro son:

| EQ | igual a |
|---|---|
| NE | no igual a |
| LT | menor que |
| LTE | menor que o igual a |
| GE | mayor que |
| GTE | mayor que o igual a |
| LIKE | coincidencia aproximada |

Es importante que la dirección URL haga referencia al componente (recurso) de Communities y no a la página en la que se coloca el componente:

* Correcto: componente de foro
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* Incorrecto: página de foro
   * `/content/community-components/en/forum.social.json`

## Herramientas SRP {#srp-tools}

Hay un proyecto de Adobe Experience Cloud GitHub que contiene:

[Herramientas SRP de AEM Communities](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Este repositorio contiene herramientas para administrar datos en SRP.

Actualmente, hay un servlet que puede eliminar todos los UGC de cualquier SRP.

Por ejemplo, para eliminar todos los UGC en ASRP:

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## Resolución de problemas {#troubleshooting}

### Consulta de Solr {#solr-query}

Para solucionar problemas con una consulta Solr, habilite el registro DEBUG para

`com.adobe.cq.social.srp.impl.SocialSolrConnector`.

La consulta Solr real se muestra mediante una dirección URL codificada en el registro de depuración:

La consulta a solr es: `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

El valor del parámetro `q` es la consulta. Una vez descodificada la codificación de la URL, la consulta se puede pasar a la herramienta Solr Admin Query para una depuración posterior.

## Recursos relacionados {#related-resources}

* [Almacenamiento de contenido de la comunidad](working-with-srp.md): analiza las opciones de SRP disponibles para un almacén común de UGC.
* [Resumen del proveedor de recursos de almacenamiento](srp.md) - Introducción y descripción general del uso del repositorio.
* [Acceder a UGC con SRP](accessing-ugc-with-srp.md): directrices de codificación.
* [Refactorización de SocialUtils](socialutils.md): métodos de utilidad para SRP que reemplazan SocialUtils.
* [Componentes de búsqueda y resultados de búsqueda](search.md) - Agregando la característica de búsqueda UGC a una plantilla.
