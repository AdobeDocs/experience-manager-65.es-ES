---
title: Procesamiento y entrega
description: Aprenda a procesar contenido de Adobe Experience Manager mediante Sling Default Servlets para procesar JSON y otros formatos.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: f0c543ae-33ed-40bb-9eb7-0dc3bdea69e0
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 6%

---

# Procesamiento y entrega{#rendering-and-delivery}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

El contenido de Adobe Experience Manager AEM () se puede representar fácilmente mediante [Servlets predeterminados de Sling](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) para procesar [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) y otros formatos.

Estas representaciones listas para usar suelen recorrer el repositorio y devolver el contenido tal cual.

AEM A través de Sling, también admite el desarrollo y la implementación de procesadores sling personalizados para tomar el control total del esquema y el contenido procesados.

Los procesadores predeterminados de Content Services llenan el vacío entre los valores predeterminados de Sling y el desarrollo personalizado, lo que permite la personalización y el control de muchos aspectos del contenido procesado sin necesidad de desarrollo.

El diagrama siguiente muestra la renderización de los servicios de contenido.

![chlimage_1-15](assets/chlimage_1-15.png)

## Solicitar JSON {#requesting-json}

Uso **&lt;resource.caas span=&quot;&quot; id=&quot;1&quot; translate=&quot;no&quot; />.[&lt;export-config span=&quot;&quot; id=&quot;0&quot; translate=&quot;no&quot; />.][&lt;export-config span=&quot;&quot; id=&quot;0&quot; translate=&quot;no&quot; />.json** para solicitar JSON.]

<table>
 <tbody>
  <tr>
   <td>RECURSO</td>
   <td>un recurso de entidad en /content/entities<br /> o <br /> un recurso de contenido en /content</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>OPCIONAL</strong><br /> </p> <p>se ha encontrado una configuración de exportación en /apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG<br /> <br /> Si se omite, se aplica la configuración de exportación predeterminada </p> </td>
  </tr>
  <tr>
   <td>DEPTH-INT</td>
   <td><strong>OPCIONAL</strong><br /> <br /> recursión de profundidad para la renderización de tareas secundarias tal como se utiliza en la renderización Sling</td>
  </tr>
 </tbody>
</table>

## Creación de configuraciones de exportación {#creating-export-configs}

Se pueden crear configuraciones de exportación para personalizar la renderización JSON.

Puede crear un nodo de configuración en */apps/mobileapps/caas/exportConfigs.*

| Nombre de nodo | Nombre de la configuración (para el selector de procesamiento) |
|---|---|
| jcr:primaryType | nt:unstructured |

En la tabla siguiente se muestran las propiedades de las configuraciones de exportación:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Predeterminado (si no está configurado)</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td>String[]</td>
   <td>incluir todo</td>
   <td>sling:resourceType</td>
   <td>excluir detalles de nodos con sling:resourceType especificado de la exportación JSON</td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td>String[]</td>
   <td>no excluir nada</td>
   <td>sling:resourceType</td>
   <td>incluir detalles solo para nodos con sling:resourceType especificado de la exportación JSON</td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>String[]</td>
   <td>no excluir nada</td>
   <td>Prefijos de propiedad</td>
   <td>excluir de la exportación JSON las propiedades que comienzan con prefijos especificados</td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td>String[]</td>
   <td>no excluir nada</td>
   <td>Nombres de propiedades</td>
   <td>excluir las propiedades especificadas de la exportación de JSON</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>String[]</td>
   <td>incluir todo</td>
   <td>Nombres de propiedades</td>
   <td><p>si excludePropertyPrefixes establecido<br /> esto incluye las propiedades especificadas, a pesar de que coinciden con el prefijo que se excluye,</p> <p>else (excluyendo propiedades ignoradas) solo incluye estas propiedades</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>String[]</td>
   <td>incluir todo</td>
   <td>nombres secundarios</td>
   <td>excluir los elementos secundarios especificados de la exportación de JSON</td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td>Cadena[]<br /> <br /> </td>
   <td>no excluir nada</td>
   <td>nombres secundarios</td>
   <td>incluir solo los elementos secundarios especificados de la exportación JSON, excluir otros</td>
  </tr>
  <tr>
   <td>nameProperties</td>
   <td>Cadena[]<br /> <br /> </td>
   <td>cambiar nombre nada</td>
   <td>&lt;actual_property_name&gt;,&lt;replacement_property_name&gt;</td>
   <td>cambiar el nombre de propiedades mediante reemplazos</td>
  </tr>
 </tbody>
</table>

### Anulaciones de exportación de tipo de recurso {#resource-type-export-overrides}

Cree un nodo de configuración en */apps/mobileapps/caas/exportConfigs.*

| name | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt:unstructured |

En la tabla siguiente se muestran las propiedades:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Predeterminado (si no está configurado)</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>&lt;SELECTOR_TO_INC&gt;</td>
   <td>String[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>Para los siguientes tipos de recursos de sling, no devuelva la exportación JSON de CaaS predeterminada.<br /> Devolver una exportación de json de cliente procesando el recurso como;<br /> &lt;resource&gt;.&lt;selector_to_inc&gt;.json </td>
  </tr>
 </tbody>
</table>

### Configuraciones de exportación de Content Services existentes {#existing-content-services-export-configs}

Los servicios de contenido incluyen dos configuraciones de exportación:

* predeterminado (no se especificó ninguna configuración)
* página (para procesar páginas de sitio)

#### Configuración de exportación predeterminada {#default-export-configuration}

La configuración de exportación predeterminada de Content Services se aplica si se especifica una configuración en el URI solicitado.

&lt;resource>.caas[.&lt;depth-int>].json

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
   <td>jcr:texto,texto<br /> jcr:título,título<br /> jcr:description,description<br /> jcr:lastModified,lastModified<br /> cq:tags,etiquetas<br /> cq:lastModified,lastModified</td>
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
   <td>Anulaciones de Sling JSON</td>
   <td>foundation/components/image<br /> wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### Configuración de exportación de página {#page-export-configuration}

Esta configuración amplía el valor predeterminado para incluir la agrupación de tareas secundarias en un nodo secundario.

&lt;site_page>.caas.page[.&lt;depth-int>].json

### Recursos adicionales {#additional-resources}

Consulte los recursos siguientes para obtener más información sobre temas adicionales en Content Services:

* [Desarrollo de modelos](/help/mobile/administer-mobile-apps.md)
* [Creación de servicios de contenido](/help/mobile/develop-content-as-a-service.md)
* [Administración de servicios de contenido](/help/mobile/developing-content-services.md)
