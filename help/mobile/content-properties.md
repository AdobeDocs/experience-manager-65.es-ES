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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Propiedades y nodos de contenido {#content-properties-and-nodes}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Los artículos, los letreros y las colecciones se representan como cq:Pages en AEM.

Comparten las mismas propiedades comunes que se encuentran en cualquier cq:Page, además de otras que se muestran a continuación, que representan los metadatos de los servicios bajo demanda de Adobe Experience Manager (AEM) Mobile y las propiedades compatibles con la integración.

Las siguientes tablas describen las propiedades y los nodos de contenido.

## Propiedades de integración comunes {#common-integration-properties}

| **Nombre de propiedad** | **Tipo** | **Valores predeterminados o esperados** | **Descripción** |
|---|---|---|---|
| dps-id | Cadena |  | asignado por AEM Mobile y almacenado por AEM una vez cargado en AEM Mobile o importado de AEM Mobile |
| dps-resourceType | Cadena | dps:Article | dps:Banner | dps:Collection | entity type, propiedad |
| dps-version | Cadena |  | versión de la entidad de AEM Mobile (también incluida en el aemm-id completo) |
| dps-lastSynced | Fecha |  | fecha de la última sincronización/importación de AEM Mobile a AEM |
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
| dps-category | Cadena |  |
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
--- |--- |--- |--- |
| imagen | jcr:PrimaryType=nt: <br> sling no estructurado:resourceType=foundation/components/image |  |  |

### Entidades {#entities}

#### Artículos {#articles-1}

| Nombre de nodo | Tipo | Valores predeterminados de valores esperados | Descripción |
|--- |--- |--- |--- |
| social-share-image |  | jcr:PrimaryType=nt: <br> sling no estructurado:resourceType=foundation/components/image |  |

#### Banners {#banners-1}

| Nombre de nodo | Tipo | Valores predeterminados de valores esperados | Descripción |
|---|---|---|---|
| ND |  |  |  |

#### Colecciones {#collections-1}

| Nombre de nodo | Tipo | Valores predeterminados de valores esperados | Descripción |
|--- |--- |--- |--- |
| background-image | jcr:PrimaryType=nt: <br> sling no estructurado:resourceType=foundation/components/image |  |  |
