---
title: Propiedades y nodos de contenido
seo-title: Propiedades y nodos de contenido
description: Siga esta página para conocer las propiedades y los nodos del contenido.
seo-description: Siga esta página para conocer las propiedades y los nodos del contenido.
uuid: 2dad52c8-5b6c-4b90-8498-62217a9a27fc
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: f5721ddc-df5c-496c-be61-38d1cab63ad4
translation-type: tm+mt
source-git-commit: 50c0bdfc3203410d392e53536bc7cd00245406e5
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 20%

---


# Propiedades de contenido y nodos {#content-properties-and-nodes}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Los artículos, los letreros y las colecciones se representan como cq:Pages en AEM.

Comparten las mismas propiedades comunes que se encuentran en cualquier cq:Page, además de otras que se muestran a continuación, que representan los metadatos de Adobe Experience Manager (AEM) Mobile On-Demand Services y las propiedades de compatibilidad con la integración.

Las siguientes tablas describen las propiedades y los nodos de contenido.

## Propiedades de integración común {#common-integration-properties}

| **Nombre de propiedad** | **Tipo** | **Valores predeterminados o esperados** | **Descripción** |
|---|---|---|---|
| dps-id | Cadena |  | asignado por AEM Mobile y almacenado por AEM una vez cargado en AEM Mobile o importado de AEM Mobile |
| dps-resourceType | Cadena | dps:Article | dps:Banner | dps:Collection | entity type, propiedad |
| dps-version | Cadena |  | versión de la entidad AEM Mobile (también incluida en el aemm-id completo) |
| dps-lastSynced | Fecha |  | fecha de la última sincronización/importación de AEM Mobile en AEM |
| dps-lastUploaded | Fecha |  | fecha de la última carga de AEM a AEM Mobile |
| dps-lastUploadedBy | Cadena:userid |  | usuario de ID que realizó la última solicitud de carga de AEM a AEM Mobile |

## Propiedades de metadatos principales {#core-metadata-properties}

| Nombre de propiedad | Tipo | Valores predeterminados o esperados |
|--- |--- |--- |
| dps-title | Cadena |  |
| dps-shortTitle | Cadena |  |
| dps-abstract | Cadena |  |
| dps-shortAbstract | Cadena |  |
| dps-Department | Cadena |  |
| dps-categoría | Cadena |  |
| dps-keywords | Cadena[] |  |
| dps-internalKeywords | Cadena[] |  |
| dps-important | Cadena[] | Importancia de {&quot;low&quot;, &quot;normal&quot;, &quot;high&quot;} |

### Artículos {#articles}

| **Nombre de propiedad** | **Tipo** | **Valores predeterminados o esperados** |
|---|---|---|
| dps-author | Cadena |  |
| dps-authorURL | Cadena |  |
| dps-hideFromBrowsePage | Booleano |  |
| dps-access | Cadena | ProtectedAccess desde {&quot;protected&quot;, &quot;metered&quot;, &quot;free&quot;} |
| **Social** |  |  |
| dps-socialShareURL | Cadena |  |
| dps-articleText | Cadena |  |
| dps-url | Cadena |  |

### Banners {#banners}

| **Nombre de propiedad** | **Tipo** | **Valores predeterminados o esperados** |
|---|---|---|
| dps-tapAction |  | TapAction desde {webLink} |
| dps-tapActionUrl |  |  |

### Colecciones {#collections}

| Nombre de propiedad | Tipo | Valores predeterminados o esperados |
|--- |--- |--- |
| dps-productId | Cadena |  |
| dps-readingPosition | Cadena | desde {&quot;reset&quot;,&quot;keep&quot;} |
| dps-horizontalSwipe | Booleano |  |
| dps-allowDownload | Booleano |  |
| dps-openDefault | Cadena | desde {&quot;browsePage&quot;,&quot;contentView&quot;} |
| dps-layout | Cadena |  |

## Nodos de contenido {#content-nodes}

### Nodos comunes {#common-nodes}

| Nombre de nodo | Tipo | Valores predeterminados o esperados | Descripción |
|--- |--- |--- |--- |
| image | jcr:PrimaryType=nt:unstructure <br> sling:resourceType=foundation/components/image |  |  |

### Entidades {#entities}

#### Artículos {#articles-1}

| Nombre de nodo | Tipo | Valores predeterminados de valores esperados | Descripción |
|--- |--- |--- |--- |
| social-share-image |  | jcr:PrimaryType=nt:unstructure <br> sling:resourceType=foundation/components/image |  |

#### Pancartas {#banners-1}

| Nombre de nodo | Tipo | Valores predeterminados de valores esperados | Descripción |
|---|---|---|---|
| ND |  |  |  |

#### Colecciones {#collections-1}

| Nombre de nodo | Tipo | Valores predeterminados de valores esperados | Descripción |
|--- |--- |--- |--- |
| background-image | jcr:PrimaryType=nt:unstructure <br> sling:resourceType=foundation/components/image |  |  |
