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
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 21%

---

# Propiedades y nodos de contenido {#content-properties-and-nodes}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

AEM Los artículos, titulares y colecciones se representan como cq:Pages en la sección de artículos de la página de la página de la página de.

Comparten las mismas propiedades comunes que se encuentran en cualquier cq:Page, además de otras que se muestran a continuación y que representan metadatos de Adobe Experience Manager AEM () Mobile On-Demand Services y propiedades de compatibilidad con la integración.

Las siguientes tablas describen las propiedades y los nodos de contenido.

## Propiedades de integración comunes {#common-integration-properties}

| **Nombre de propiedad** | **Tipo** | **Valores predeterminados o valores esperados** | **Descripción** |
|---|---|---|---|
| dps-id | Cadena |  | asignado por AEM Mobile AEM y almacenado por una vez cargado en AEM Mobile o importado desde AEM Mobile, por el usuario. |
| dps-resourceType | Cadena | dps:Article | dps:Banner | dps:Collection | propiedad de tipo de entidad |
| dps-version | Cadena |  | versión de AEM Mobile entity (también incluida en el aem-id completo) |
| dps-lastSynced | Fecha |  | fecha de la última sincronización/importación de AEM Mobile AEM a la red de distribución de datos |
| dps-lastUploaded | Fecha |  | AEM fecha de la última carga desde el servidor de correo electrónico a AEM Mobile |
| dps-lastUploadedBy | String:id de usuario |  | AEM usuario de id que realizó la última solicitud de carga de la aplicación de la que se hizo la solicitud de acceso desde la base de datos de a AEM Mobile |

## Propiedades de metadatos principales {#core-metadata-properties}

| Nombre de propiedad | Tipo | Valores predeterminados o valores esperados |
|--- |--- |--- |
| dps-title | Cadena |  |
| dps-shortTitle | Cadena |  |
| dps-abstract | Cadena |  |
| dps-shortAbstract | Cadena |  |
| dps-department | Cadena |  |
| dps-category | Cadena |  |
| dps-keywords | String[] |  |
| dps-internalKeywords | String[] |  |
| dps-important | String[] | Importancia desde {&quot;low&quot;, &quot;normal&quot;, &quot;high&quot;} |

### Artículos {#articles}

| **Nombre de propiedad** | **Tipo** | **Valores predeterminados o valores esperados** |
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

| **Nombre de propiedad** | **Tipo** | **Valores predeterminados o valores esperados** |
|---|---|---|
| dps-tapAction |  | Tocar acción desde {webLink} |
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
