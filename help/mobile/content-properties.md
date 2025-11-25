---
title: Propiedades y nodos de contenido
description: Siga esta página para obtener más información sobre las propiedades y los nodos de contenido.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 05c8c846-69cc-4075-9149-33890b3d1e08
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 20%

---

# Propiedades y nodos de contenido {#content-properties-and-nodes}

{{ue-over-mobile}}

Los artículos, titulares y colecciones se representan como cq:Pages en AEM.

Comparten las mismas propiedades comunes que se encuentran en cualquier cq:Page, además de varias otras que se muestran a continuación y que representan metadatos de Adobe Experience Manager (AEM) Mobile On-Demand Services y propiedades de compatibilidad con integraciones.

Las siguientes tablas describen las propiedades y los nodos de contenido.

## Propiedades de integración comunes {#common-integration-properties}

| **Nombre de propiedad** | **Tipo** | **Valores predeterminados o esperados** | **Descripción** |
|---|---|---|---|
| dps-id | Cadena |  | asignado por AEM Mobile y almacenado por AEM una vez cargado en AEM Mobile o importado desde AEM Mobile |
| dps-resourceType | Cadena | dps:Article | `dps:Banner` \| `dps:Collection` \| `entity type property` |
| dps-version | Cadena |  | versión de AEM Mobile entity (también incluida en el aem-id completo) |
| dps-lastSynced | Fecha |  | fecha de la última sincronización/importación de AEM Mobile a AEM |
| dps-lastUploaded | Fecha |  | fecha de la última carga de AEM a AEM Mobile |
| dps-lastUploadedBy | Cadena :userid |  | usuario de id que realizó la última solicitud de carga de AEM a AEM Mobile |

## Propiedades de metadatos principales {#core-metadata-properties}

| Nombre de propiedad | Tipo | Valores predeterminados o valores esperados |
|--- |--- |--- |
| dps-title | Cadena |  |
| dps-shortTitle | Cadena |  |
| dps-abstract | Cadena |  |
| dps-shortAbstract | Cadena |  |
| dps-department | Cadena |  |
| dps-category | Cadena |  |
| dps-keywords | Cadena [] |  |
| dps-internalKeywords | Cadena [] |  |
| dps-important | Cadena [] | Importancia desde {&quot;low&quot;, &quot;normal&quot;, &quot;high&quot;} |

### Artículos {#articles}

| **Nombre de propiedad** | **Tipo** | **Valores predeterminados o esperados** |
|---|---|---|
| dps-author | Cadena |  |
| dps-authorURL | Cadena |  |
| dps-hideFromBrowsePage | Booleano |  |
| dps-access | Cadena | ProtectedAccess from {&quot;protegido&quot;, &quot;medido&quot;, &quot;libre&quot;} |
| **Social** |  |  |
| dps-socialShareURL | Cadena |  |
| dps-articleText | Cadena |  |
| dps-url | Cadena |  |

### Banners {#banners}

| **Nombre de propiedad** | **Tipo** | **Valores predeterminados o esperados** |
|---|---|---|
| dps-tapAction |  | Pulse Acción desde {webLink} |
| dps-tapActionUrl |  |  |

### Colecciones {#collections}

| Nombre de propiedad | Tipo | Valores predeterminados o valores esperados |
|--- |--- |--- |
| dps-productId | Cadena |  |
| dps-readingPosition | Cadena | de {&quot;reset&quot;,&quot;keep&quot;} |
| dps-horizontalSwipe | Booleano |  |
| dps-allowDownload | Booleano |  |
| dps-openDefault | Cadena | de {&quot;browsePage&quot;,&quot;contentView&quot;} |
| dps-layout | Cadena |  |

## Nodos de contenido {#content-nodes}

### Nodos comunes {#common-nodes}

| Nombre de nodo | Tipo | Valores predeterminados o valores esperados | Descripción |
|--- |--- |--- |--- |
| image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |

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
| background-image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
