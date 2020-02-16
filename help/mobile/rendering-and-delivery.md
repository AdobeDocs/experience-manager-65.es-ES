---
title: Procesamiento y envío
seo-title: Procesamiento y envío
description: nulo
seo-description: nulo
uuid: 1253b6a5-6bf3-42b1-be3a-efa23b6ddb51
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 672d5b1e-6b2f-4afe-ab04-c398e5ef45d5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Procesamiento y envío{#rendering-and-delivery}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

El contenido de AEM se puede procesar fácilmente mediante [Sling Default Servlets](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) para procesar [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) y otros formatos.

Los procesamientos listos para usar generalmente dirigen el repositorio y devuelven contenido tal cual.

AEM, a través de Sling, también admite el desarrollo y la implementación de representadores de sling personalizados para controlar completamente el esquema y el contenido procesados.

Los procesadores predeterminados de Content Services llenan el espacio entre los valores predeterminados de Sling predeterminados y el desarrollo personalizado, lo que permite la personalización y el control de muchos aspectos del contenido procesado sin necesidad de desarrollo.

El diagrama siguiente muestra la representación de los servicios de contenido.

![chlimage_1-15](assets/chlimage_1-15.png)

## Solicitud de JSON {#requesting-json}

Utilice **&lt;RESOURCE.caas[.&lt;EXPORT-CONFIG][.&lt;EXPORT-CONFIG].json** para solicitar JSON.

<table>
 <tbody>
  <tr>
   <td>RECURSO</td>
   <td>un recurso de entidad en /content/entity<br /> o <br /> un recurso de contenido en /content</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>OPCIONAL</strong><br /> </p> <p>se encontró una configuración de exportación en /apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG<br /> <br /> . Si se omite, se aplicará la configuración de exportación predeterminada </p> </td>
  </tr>
  <tr>
   <td>PROFUNDIDAD-INT</td>
   <td><strong>Recursión de profundidad OPCIONAL</strong><br /><br /> para procesar niños como se utiliza en el procesamiento de Sling</td>
  </tr>
 </tbody>
</table>

## Creación de configuraciones de exportación {#creating-export-configs}

Se pueden crear configuraciones de exportación para personalizar el procesamiento JSON.

Puede crear un nodo de configuración en */apps/mobileapps/caas/exportConfigs.*

| Nombre de nodo | Nombre de la configuración (para el selector de procesamiento) |
|---|---|
| jcr:primaryType | nt:unstructured |

En la tabla siguiente se muestran las propiedades de la configuración de exportación:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Predeterminado (si, no establecido)</strong></td>
   <td><strong>Value</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td>Cadena[]</td>
   <td>incluir todo</td>
   <td>sling:resourceType</td>
   <td>excluir detalles para nodos con sling:resourceType especificado de la exportación JSON</td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td>Cadena[]</td>
   <td>excluir nada</td>
   <td>sling:resourceType</td>
   <td>incluir detalles solo para nodos con sling:resourceType especificado de la exportación JSON</td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>Cadena[]</td>
   <td>excluir nada</td>
   <td>Prefijos de propiedad</td>
   <td>excluya las propiedades que comienzan con prefijos especificados de la exportación JSON</td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td>Cadena[]</td>
   <td>excluir nada</td>
   <td>Nombres de propiedades</td>
   <td>excluir propiedades especificadas de la exportación JSON</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>Cadena[]</td>
   <td>incluir todo</td>
   <td>Nombres de propiedades</td>
   <td><p>si excludePropertyPrefixes está establecido<br /> , incluye las propiedades especificadas a pesar de coincidir con el prefijo que se está excluyendo,</p> <p>else (las propiedades de exclusión ignoradas) solo incluyen estas propiedades</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>Cadena[]</td>
   <td>incluir todo</td>
   <td>nombres secundarios</td>
   <td>excluir elementos secundarios especificados de la exportación JSON</td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td>Cadena[]<br /> <br /> </td>
   <td>excluir nada</td>
   <td>nombres secundarios</td>
   <td>incluir solo elementos secundarios especificados de la exportación JSON, excluir otros</td>
  </tr>
  <tr>
   <td>RenameProperties</td>
   <td>Cadena[]<br /> <br /> </td>
   <td>cambiar el nombre de nada</td>
   <td>&lt;nombre_propiedad_real&gt;,&lt;nombre_propiedad_reemplazo&gt;</td>
   <td>cambio del nombre de las propiedades mediante reemplazos</td>
  </tr>
 </tbody>
</table>

### Anulaciones de exportación de tipo de recurso {#resource-type-export-overrides}

Cree un nodo de configuración en */apps/mobileapps/caas/exportConfigs.*

| name | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt:unstructured |

La tabla siguiente muestra las propiedades:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Predeterminado (si, no establecido)</strong></td>
   <td><strong>Value</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>&lt;SELECTOR_TO_INC&gt;</td>
   <td>Cadena[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>Para los siguientes tipos de recursos de sling, no devuelva la exportación predeterminada de JavaScript de CaaS.<br /><br /> Devolver una exportación de json de cliente mediante el procesamiento del recurso como; &lt;RECURSO&gt;.&lt;SELECTOR_TO_INC&gt;.json </td>
  </tr>
 </tbody>
</table>

### Configuraciones de exportación de Content Services existentes {#existing-content-services-export-configs}

Content Services incluye dos configuraciones de exportación:

* predeterminado (no se especificó ninguna configuración)
* página (para procesar páginas del sitio)

#### Configuración de exportación predeterminada {#default-export-configuration}

La configuración de exportación predeterminada de Content Services se aplicará si se especifica una configuración en el URI solicitado.

&lt;RESOURCE>.caas[.&lt;DEPTH-INT>].json

<table>
 <tbody>
  <tr>
   <td><strong>Nombre</strong></td>
   <td><strong>Value</strong></td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>jcr:,sling:,cq:,oak:,pge-</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>jcr:text,text<br /> jcr:title,title<br /> jcr:description,description<br /> jcr:lastModified,lastModified<br /> cq:tags,tags<br /> cq:lastModified,lastModified</td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>Anulaciones de JSON de Sling</td>
   <td>foundation/components/image<br /> wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReferencia<br /> a mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### Configuración de exportación de página {#page-export-configuration}

Esta configuración amplía el valor predeterminado para incluir elementos secundarios de agrupación en un nodo secundario.

&lt;SITE_PAGE>.caas.page[.&lt;DEPTH-INT>].json

### Additional Resources {#additional-resources}

Consulte los recursos siguientes para obtener información sobre temas adicionales en Content Services:

* [Desarrollo de modelos](/help/mobile/models-in-repository.md)
* [Creación de Content Services](/help/mobile/develop-content-as-a-service.md)
* [Administración de servicios de contenido](/help/mobile/developing-content-services.md)

