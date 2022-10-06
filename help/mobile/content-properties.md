---
title: Propiedades y nodos de contenido
seo-title: Content Properties and Nodes
description: Siga esta página para obtener más información sobre las propiedades y los nodos de contenido.
seo-description: Follow this page to learn about content properties and nodes.
uuid: 2dad52c8-5b6c-4b90-8498-62217a9a27fc
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: f5721ddc-df5c-496c-be61-38d1cab63ad4
exl-id: 05c8c846-69cc-4075-9149-33890b3d1e08
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 21%

---

# Propiedades y nodos de contenido {#content-properties-and-nodes}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Los artículos, los banners y las colecciones se representan como cq:Pages en AEM.

Comparten las mismas propiedades comunes que se encuentran en cualquier cq:Page, además de varias que se muestran a continuación, que representan los metadatos de Adobe Experience Manager (AEM) Mobile On-Demand Services y las propiedades de integración compatibles.

Las tablas siguientes describen las propiedades y los nodos de contenido.

## Propiedades de integración comunes {#common-integration-properties}

| **Nombre de propiedad** | **Tipo** | **Valores predeterminados o esperados** | **Descripción** |
|---|---|---|---|
| dps-id | Cadena |  | asignado por AEM Mobile y almacenado por AEM una vez cargado en AEM Mobile o importado desde AEM Mobile |
| dps-resourceType | Cadena | dps:Article | dps:Banner | dps:Collection | propiedad de tipo de entidad |
| dps-version | Cadena |  | versión de la entidad de AEM Mobile (también incluida en el aemm-id completo) |
| dps-lastSynced | Fecha |  | fecha de la última sincronización/importación de AEM Mobile en AEM |
| dps-lastUploaded | Fecha |  | fecha de la última carga de AEM a AEM Mobile |
| dps-lastUploadedBy | Cadena:userid |  | usuario de id que realizó la última solicitud de carga de AEM a AEM Mobile |

## Propiedades de los metadatos principales {#core-metadata-properties}

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
| dps-access | Cadena | Protegido: Acceso desde {&quot;protegido&quot;, &quot;medido&quot;, &quot;gratuito&quot;} |
| **Social** |  |  |
| dps-socialShareURL | Cadena |  |
| dps-articleText | Cadena |  |
| dps-url | Cadena |  |

### Banners {#banners}

| **Nombre de propiedad** | **Tipo** | **Valores predeterminados o esperados** |
|---|---|---|
| dps-tapAction |  | TapAction de {webLink} |
| dps-tapActionUrl |  |  |

### Colecciones {#collections}

| Nombre de propiedad | Tipo | Valores predeterminados o esperados |
|--- |--- |--- |
| dps-productId | Cadena |  |
| dps-readPosition | Cadena | desde {&quot;reset&quot;,&quot;keep&quot;} |
| dps-horizontalSwipe | Booleano |  |
| dps-allowDownload | Booleano |  |
| dps-openDefault | Cadena | desde {&quot;browsePage&quot;,&quot;contentView&quot;} |
| dps-layout | Cadena |  |

## Nodos de contenido {#content-nodes}

### Nodos comunes {#common-nodes}

| Nombre de nodo | Tipo | Valores predeterminados o esperados | Descripción |
|--- |--- |--- |--- |
| imagen | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |

### Entidades {#entities}

#### Artículos {#articles-1}

| Nombre de nodo | Tipo | Valores predeterminados de los valores esperados | Descripción |
|--- |--- |--- |--- |
| social-share-image |  | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |

#### Banners {#banners-1}

| Nombre de nodo | Tipo | Valores predeterminados de los valores esperados | Descripción |
|---|---|---|---|
| ND |  |  |  |

#### Colecciones {#collections-1}

| Nombre de nodo | Tipo | Valores predeterminados de los valores esperados | Descripción |
|--- |--- |--- |--- |
| imagen de fondo | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
