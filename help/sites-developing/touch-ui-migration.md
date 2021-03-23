---
title: Migración a la interfaz de usuario táctil
seo-title: Migración a la interfaz de usuario táctil
description: Migración a la interfaz de usuario táctil
seo-description: Migración a la interfaz de usuario táctil
uuid: 47c43b56-532b-4ada-8503-04d66bab3564
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: b315720f-e9b8-4063-99e2-1b9aa6bba460
docset: aem65
translation-type: tm+mt
source-git-commit: 7035c19a109ff67655ee0419aa37d1723e2189cc
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 6%

---


# Migración a la IU táctil{#migration-to-the-touch-ui}

A partir de la versión 6.0, Adobe Experience Manager (AEM) introdujo una nueva interfaz de usuario denominada *IU táctil* (también conocida como *IU táctil*). Se alinea con Adobe Marketing Cloud y con las directrices generales de la interfaz de usuario del Adobe. Esta se ha convertido en la interfaz de usuario estándar en AEM con la interfaz heredada y orientada al escritorio denominada *IU clásica*.

Si ha estado utilizando AEM con la IU clásica, deberá realizar una acción para migrar la instancia. Esta página pretende servir de trampolín al proporcionar vínculos a recursos individuales.

>[!NOTE]
>
>Este proyecto de migración puede tener un impacto significativo en su instancia. Consulte [Administración de proyectos: prácticas recomendadas](/help/managing/best-practices.md) para obtener instrucciones recomendadas.

## Conceptos básicos {#the-basics}

Al migrar, debe tener en cuenta las siguientes diferencias (principales) entre la IU clásica y la táctil:

<table>
 <tbody>
  <tr>
   <td>IU clásica</td>
   <td>IU táctil</td>
  </tr>
  <tr>
   <td>Se describe en el repositorio JCR como una estructura de nodos. Cada nodo que representa un elemento de la interfaz de usuario se denomina <em>utilidad ExtJS</em> y se representa en el lado del cliente mediante <code>ExtJS</code>.</td>
   <td>También se describe en el repositorio JCR como una estructura de nodos. Sin embargo, en este caso cada nodo hace referencia a un tipo de recurso de Sling (componente Sling), que se encarga de su renderización. Por lo tanto, la interfaz de usuario se representa (básicamente) en el lado del servidor.</td>
  </tr>
  <tr>
   <td><p><code>sling:resourceType</code></p>
    <ul>
     <li>no se usa</li>
    </ul> </td>
   <td><code>sling:resourceType</code>
    <ul>
     <li>usado</li>
     <li>por ejemplo<br /> <code>cq/gui/components/authoring/dialog</code><br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Nodos de diálogo:</p>
    <ul>
     <li>Nombre: <code>dialog</code></li>
     <li>jcr:primaryType: <code>cq:Dialog</code></li>
    </ul> </td>
   <td><p>Nodos de diálogo:</p>
    <ul>
     <li>Nombre: <code>cq:dialog</code></li>
     <li>jcr:primaryType: <code>nt:unstructured</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Ubicación de JavaScript:</p>
    <ul>
     <li>Las partes imperativas se incrustan directamente mediante oyentes o se administran en clientlibs.</li>
    </ul> </td>
   <td><p>Ubicación de JavaScript:</p>
    <ul>
     <li>Las partes imperativas no se pueden incrustar en la definición del cuadro de diálogo; separación de responsabilidades.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Gestión de eventos:</p>
    <ul>
     <li>Los widgets de cuadro de diálogo hacen referencia directamente al código JavaScript.</li>
    </ul> </td>
   <td><p>Gestión de eventos:</p>
    <ul>
     <li>Javascript observa eventos de diálogo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Renderización realizada por el cliente:
    <ul>
     <li>El cliente crea de forma dinámica los componentes de la interfaz de usuario.</li>
     <li>El cliente solicita la definición del componente (como JSON) desde el servidor.</li>
    </ul> </td>
   <td>Renderización realizada por el servidor:
    <ul>
     <li>El cliente solicita páginas junto con la IU relacionada.</li>
     <li>El servidor envía (push) la interfaz de usuario como documentos HTML; uso de los componentes de Coral UI.<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

En otras palabras, migrar una sección de la interfaz de usuario de la IU clásica a la táctil significa transferir un *widget ExtJS* a un *componente Sling*. Para facilitar esto, la IU táctil se basa en el marco de la interfaz de usuario de Granite, que ya proporciona algunos componentes de Sling para la interfaz de usuario (denominados componentes de Granite UI).

Antes de comenzar, compruebe el estado y las recomendaciones relacionadas:

* [Estado de las funciones de la interfaz de usuario táctil](/help/release-notes/touch-ui-features-status.md)
* [Interfaz de usuario de Recommendations para clientes](/help/sites-deploying/ui-recommendations.md)

Los conceptos básicos del desarrollo de la IU táctil proporcionan una base sólida:

* [Conceptos de la IU táctil AEM](/help/sites-developing/touch-ui-concepts.md)
* [Estructura de la interfaz de usuario táctil AEM](/help/sites-developing/touch-ui-structure.md)

## Migración de la creación de páginas {#migrating-page-authoring}

Los cuadros de diálogo son un factor importante a la hora de migrar los componentes:

* [Desarrollo de componentes AEM](/help/sites-developing/developing-components.md)  (con la IU táctil)
* [Migración desde un componente clásico](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [AEM herramientas de modernización](/help/sites-developing/modernization-tools.md) : para ayudarle a convertir los cuadros de diálogo de los componentes de la IU clásica a la IU táctil

   * Existe una capa de compatibilidad en la IU táctil para abrir un cuadro de diálogo de IU clásica dentro de un &quot;envoltorio de IU táctil&quot;, pero esta función tiene una funcionalidad limitada y no se recomienda a largo plazo.

* [Personalización de campos de cuadro de diálogo en la IU táctil](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [Creación de un nuevo componente de campo de interfaz de usuario de Granite](/help/sites-developing/granite-ui-component.md)
* [Personalización de la creación de páginas](/help/sites-developing/customizing-page-authoring-touch.md)  (con la IU táctil)

## Migración de consolas {#migrating-consoles}

También puede personalizar las consolas:

* [Personalización de las consolas](/help/sites-developing/customizing-consoles-touch.md)  (para la IU táctil)

## Consideraciones relacionadas {#related-considerations}

Aunque no está directamente relacionado con la migración a la interfaz de usuario táctil, hay problemas relacionados que vale la pena tener en cuenta al mismo tiempo, ya que también son una práctica recomendada:

* [Plantillas](/help/sites-developing/templates.md) : plantillas  [editables](/help/sites-developing/page-templates-editable.md)
* [Componentes principales](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html)
* [HTL](https://docs.adobe.com/content/help/es-ES/experience-manager-htl/using/overview.html)

>[!NOTE]
>
>Consulte también [Desarrollo: prácticas recomendadas](/help/sites-developing/best-practices.md).

## Recursos adicionales {#further-resources}

Para obtener información completa sobre el desarrollo de AEM, consulte la recopilación de recursos en:

* [Guía del usuario sobre desarrollo](/help/sites-developing/home.md)
* [Documentación de Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [Tutorials y vídeos de AEM 6.5 Sites](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/overview.html)
* [Introducción al desarrollo de AEM Sites: Tutorial de WKND](/help/sites-developing/getting-started.md)
* [AEM](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [Herramientas de modernización de AEM](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>AEM herramientas de modernización son un esfuerzo de la comunidad y no son compatibles ni están garantizadas por el Adobe.

