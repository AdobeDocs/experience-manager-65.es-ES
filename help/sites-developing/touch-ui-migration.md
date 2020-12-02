---
title: Migración a la IU táctil
seo-title: Migración a la IU táctil
description: Migración a la IU táctil
seo-description: Migración a la IU táctil
uuid: 47c43b56-532b-4ada-8503-04d66bab3564
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: b315720f-e9b8-4063-99e2-1b9aa6bba460
docset: aem65
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 6%

---


# Migración a la IU táctil{#migration-to-the-touch-ui}

A partir de la versión 6.0, Adobe Experience Manager (AEM) introdujo una nueva interfaz de usuario denominada *IU táctil* (también conocida como *IU táctil*). Está alineado con el Adobe Marketing Cloud y con las directrices generales de la interfaz de usuario de Adobe. Esta se ha convertido en la interfaz de usuario estándar en AEM con la interfaz heredada y orientada al escritorio denominada *IU clásica*.

Si ha estado utilizando AEM con la IU clásica, deberá realizar una acción para migrar la instancia. Esta página tiene como objetivo actuar como trampolín proporcionando vínculos a recursos individuales.

>[!NOTE]
>
>Este proyecto de migración puede tener un impacto significativo en su caso. Consulte [Administración de proyectos - Optimizaciones](/help/managing/best-practices.md) para obtener instrucciones recomendadas.

## Conceptos básicos {#the-basics}

Al migrar, debe tener en cuenta las siguientes diferencias (principales) entre la IU clásica y la táctil:

<table>
 <tbody>
  <tr>
   <td>IU clásica</td>
   <td>IU táctil</td>
  </tr>
  <tr>
   <td>Se describe en el repositorio JCR como una estructura de nodos. Todos los nodos que representan un elemento de la interfaz de usuario se denominan <em>widget ExtJS</em> y se representan en el lado del cliente mediante <code>ExtJS</code>.</td>
   <td>También se describe en el repositorio JCR como una estructura de nodos. Sin embargo, en este caso, cada nodo hace referencia a un tipo de recurso Sling (componente Sling), que se encarga de su procesamiento. La interfaz de usuario se representa básicamente en el servidor.</td>
  </tr>
  <tr>
   <td><p><code>sling:resourceType</code></p>
    <ul>
     <li>no utilizado</li>
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
     <li>jcr:parentType: <code>nt:unstructured</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Ubicación de JavaScript:</p>
    <ul>
     <li>Las partes imperativas se incrustan directamente mediante oyentes o se administran en clientlibs.</li>
    </ul> </td>
   <td><p>Ubicación de JavaScript:</p>
    <ul>
     <li>Las partes imperativas no pueden incrustarse en la definición de cuadro de diálogo; separación de responsabilidades.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Manejo de eventos:</p>
    <ul>
     <li>Las utilidades de cuadro de diálogo hacen referencia directa al código Javascript.</li>
    </ul> </td>
   <td><p>Manejo de eventos:</p>
    <ul>
     <li>Javascript observa eventos de diálogo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Representación realizada por el cliente:
    <ul>
     <li>El cliente crea dinámicamente los componentes de la interfaz de usuario.</li>
     <li>El cliente solicita la definición del componente (como JSON) desde el servidor.</li>
    </ul> </td>
   <td>Representación realizada por el servidor:
    <ul>
     <li>El cliente solicita páginas junto con la IU relacionada.</li>
     <li>El servidor envía (push) la interfaz de usuario como documentos HTML; uso de componentes de Coral UI.<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

En otras palabras, la migración de una sección de la interfaz de usuario de la IU clásica a la IU táctil significa transferir una *utilidad ExtJS* a un *componente Sling*. Para facilitar esto, la IU táctil se basa en el marco de la interfaz de usuario Granite, que ya proporciona algunos componentes Sling para la interfaz de usuario (denominados componentes de la interfaz de usuario Granite).

Antes de realizar el inicio, compruebe el estado y las recomendaciones relacionadas:

* [Estado de las funciones de la IU táctil](/help/release-notes/touch-ui-features-status.md)
* [Interfaz de usuario de Recommendations para clientes](/help/sites-deploying/ui-recommendations.md)

Los conceptos básicos del desarrollo de la IU táctil proporcionan una base sólida:

* [Conceptos de la IU táctil AEM](/help/sites-developing/touch-ui-concepts.md)
* [Estructura de la IU táctil AEM](/help/sites-developing/touch-ui-structure.md)

## Migración de la creación de páginas {#migrating-page-authoring}

Los diálogos son un factor importante a la hora de migrar los componentes:

* [Desarrollo de componentes](/help/sites-developing/developing-components.md)  AEM (con la IU táctil)
* [Migración desde un componente clásico](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [Herramienta](/help/sites-developing/dialog-conversion.md)  de conversión de cuadro de diálogo: para ayudarle a convertir los cuadros de diálogo de los componentes clásicos de la interfaz de usuario a la IU táctil

   * Hay una capa de compatibilidad en la IU táctil para abrir un cuadro de diálogo de IU clásica en un &quot;ajustador de IU táctil&quot;, pero esta función tiene una funcionalidad limitada y no se recomienda para el largo plazo.

* [Personalización de los campos del cuadro de diálogo en la IU táctil](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [Creación de un nuevo componente de campo de interfaz de usuario de Granite](/help/sites-developing/granite-ui-component.md)
* [Personalización de la creación](/help/sites-developing/customizing-page-authoring-touch.md)  de páginas (con la IU táctil)

## Migración de consolas {#migrating-consoles}

También puede personalizar las consolas:

* [Personalización de las consolas](/help/sites-developing/customizing-consoles-touch.md)  (para la IU táctil)

## Consideraciones relacionadas {#related-considerations}

Aunque no están directamente relacionados con una migración a la IU táctil, hay problemas relacionados que vale la pena tener en cuenta al mismo tiempo, ya que también son una práctica recomendada:

* [Plantillas](/help/sites-developing/templates.md) : plantillas  [editables](/help/sites-developing/page-templates-editable.md)
* [Componentes principales](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html)
* [HTL](https://docs.adobe.com/content/help/es-ES/experience-manager-htl/using/overview.html)

>[!NOTE]
>
>Consulte también [Desarrollo: optimizaciones](/help/sites-developing/best-practices.md).

## Recursos adicionales {#further-resources}

Para obtener información completa sobre el desarrollo de AEM, consulte la recopilación de recursos en:

* [Desarrollo de la guía del usuario](/help/sites-developing/home.md)
* [Documentación de la interfaz de usuario de Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [AEM 6.5 Sitios, Tutorials y videos](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/overview.html)
* [Introducción al desarrollo de AEM Sites: Tutorial de WKND](/help/sites-developing/getting-started.md)
* [Gemas AEM](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [Herramientas de modernización de AEM](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>AEM herramientas de modernización son un esfuerzo de la comunidad y no están soportadas ni garantizadas por el Adobe.

