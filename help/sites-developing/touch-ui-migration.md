---
title: Migración a la IU táctil
description: Migración a la IU táctil
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
docset: aem65
exl-id: 33dc1ee7-1e34-43d8-9265-c66535f5e002
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 6%

---

# Migración a la IU táctil{#migration-to-the-touch-ui}

A partir de la versión 6.0, Adobe Experience Manager AEM () introdujo una nueva interfaz de usuario denominada *IU táctil* (también conocido simplemente como *IU táctil*). Se alinea con Adobe Experience Cloud y con las directrices generales de la interfaz de usuario de Adobe. AEM Esta se ha convertido en la interfaz de usuario estándar en la interfaz heredada y orientada al escritorio, a la que se hace referencia como la interfaz de usuario de, *IU clásica*.

AEM Si ha estado utilizando la interfaz de usuario clásica de, tome medidas para migrar la instancia. Esta página está diseñada para actuar como un trampolín al proporcionar vínculos a recursos individuales.

>[!NOTE]
>
>Este proyecto de migración puede tener un impacto significativo en su instancia. Consulte [Administración de proyectos: prácticas recomendadas](/help/managing/best-practices.md) para obtener instrucciones recomendadas.

## Conceptos básicos {#the-basics}

Al migrar, tenga en cuenta las siguientes diferencias principales entre la IU clásica y la táctil:

<table>
 <tbody>
  <tr>
   <td>IU clásica</td>
   <td>IU táctil.</td>
  </tr>
  <tr>
   <td>Se describe en el repositorio JCR como una estructura de nodos. Cada nodo que representa un elemento de la interfaz de usuario se denomina <em>Widget de ExtJS</em> y representado en el lado del cliente por <code>ExtJS</code>.</td>
   <td>También se describe en el repositorio JCR como una estructura de nodos. Sin embargo, en este caso, cada nodo hace referencia a un tipo de recurso de Sling (componente de Sling), que se encarga de su procesamiento. Por lo tanto, la interfaz de usuario se procesa (básicamente) en el lado del servidor.</td>
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
     <li>Las partes imperativas no pueden incorporarse en la definición del diálogo; separación de responsabilidades.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Gestión de eventos:</p>
    <ul>
     <li>Los widgets de diálogo hacen referencia directamente al código JavaScript.</li>
    </ul> </td>
   <td><p>Gestión de eventos:</p>
    <ul>
     <li>JavaScript observa eventos de diálogo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Representación realizada por el cliente:
    <ul>
     <li>El cliente crea dinámicamente los componentes de la IU.</li>
     <li>El cliente solicita la definición del componente (como JSON) desde el servidor.</li>
    </ul> </td>
   <td>Representación realizada por el servidor:
    <ul>
     <li>El cliente solicita páginas junto con la interfaz de usuario relacionada.</li>
     <li>El servidor envía (push) la interfaz de usuario como documentos del HTML; mediante los componentes de la interfaz de usuario de Coral.<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

En otras palabras, migrar una sección de la interfaz de usuario de la IU clásica a la IU táctil significa trasladar una *Widget de ExtJS* a un *Componente Sling*. Para facilitar esto, la interfaz de usuario táctil se basa en el marco de trabajo de la interfaz de usuario de Granite, que ya proporciona algunos componentes de Sling para la interfaz de usuario (denominados componentes de la interfaz de usuario de Granite).

Antes de empezar, compruebe el estado y las recomendaciones relacionadas:

* [Estado de funciones de IU táctil](/help/release-notes/touch-ui-features-status.md)
* [Interfaz de usuario de Recommendations para clientes](/help/sites-deploying/ui-recommendations.md)

Los conceptos básicos del desarrollo de la IU táctil proporcionan una base sólida:

* [AEM Conceptos de la interfaz de usuario táctil con capacidad para el uso de la](/help/sites-developing/touch-ui-concepts.md)
* [AEM Estructura de la interfaz de usuario táctil de la](/help/sites-developing/touch-ui-structure.md)

## Migración de creación de páginas {#migrating-page-authoring}

Los cuadros de diálogo son un factor importante a la hora de migrar los componentes:

* [AEM Desarrollo de componentes](/help/sites-developing/developing-components.md) (con la IU táctil)
* [Migración desde un componente clásico](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [AEM Herramientas de modernización de](/help/sites-developing/modernization-tools.md) : para ayudarle a convertir los cuadros de diálogo de sus componentes de IU clásicos en IU táctiles.

   * Hay una capa de compatibilidad en la IU táctil para abrir un cuadro de diálogo de IU clásica dentro de un &quot;envoltorio de IU táctil&quot;, pero esto tiene una funcionalidad limitada y no se recomienda a largo plazo.

* [Personalizar campos de diálogo en la IU táctil](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [Creación de un nuevo componente de campo de IU de Granite](/help/sites-developing/granite-ui-component.md)
* [Personalización de la creación de páginas](/help/sites-developing/customizing-page-authoring-touch.md) (con la IU táctil)

## Migración de consolas {#migrating-consoles}

También puede personalizar las consolas:

* [Personalización de las consolas](/help/sites-developing/customizing-consoles-touch.md) (para la IU táctil)

## Consideraciones relacionadas {#related-considerations}

Aunque no están directamente relacionados con una migración a la interfaz de usuario táctil, hay problemas relacionados que vale la pena considerar al mismo tiempo, ya que también son una práctica recomendada:

* [Plantillas](/help/sites-developing/templates.md) - [Plantillas editables](/help/sites-developing/page-templates-editable.md)
* [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)
* [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=es)

>[!NOTE]
>
>Consulte también [Desarrollo: prácticas recomendadas](/help/sites-developing/best-practices.md).

## Otros recursos {#further-resources}

AEM Para obtener información completa sobre el desarrollo de los recursos, consulte la recopilación de recursos en:

* [Guía del usuario sobre desarrollo](/help/sites-developing/home.md)
* [Documentación de Granite UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [AEM Tutorials y vídeos de 6.5 Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/overview.html)
* [Introducción al desarrollo de AEM Sites: Tutorial de WKND](/help/sites-developing/getting-started.md)
* [AEM Gems de](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/overview.html?lang=en)
* [Herramientas de modernización de AEM](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>AEM Las herramientas de modernización son un esfuerzo de la comunidad y no son compatibles ni están garantizadas por el Adobe.
