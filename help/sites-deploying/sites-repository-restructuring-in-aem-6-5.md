---
title: Reestructuración del repositorio de sitios en AEM 6.5
seo-title: Reestructuración del repositorio de sitios en AEM 6.5
description: Aprenda a realizar los cambios necesarios para migrar a la nueva estructura de repositorios en AEM 6.5 para Sites.
seo-description: Aprenda a realizar los cambios necesarios para migrar a la nueva estructura de repositorios en AEM 6.5 para Sites.
uuid: 6dc5f8bd-1680-40af-9b8f-26c1f4bc3304
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 3eccb2d5-c325-43a6-9c03-5f93f7e30712
feature: Actualización
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 1%

---


# Reestructuración del repositorio de sitios en AEM 6.5 {#sites-repository-restructuring-in-aem}

Como se describe en la página principal [Reestructuración del repositorio en AEM 6.5](/help/sites-deploying/repository-restructuring.md), los clientes que actualicen a AEM 6.5 deben utilizar esta página para evaluar el esfuerzo de trabajo asociado con los cambios del repositorio que afectan a la solución de AEM Sites. Algunos cambios requieren un esfuerzo de trabajo durante el proceso de actualización de AEM 6.5, mientras que otros se pueden aplazar hasta una actualización futura.

**Con actualización a la versión 6.5**

* [Segmentos de ContextHub](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**Antes de una actualización futura**

* [Bibliotecas de cliente de Adobe Analytics](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [Diseños clásicos de Microsoft Word para páginas web](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [Configuraciones del emulador de dispositivos móviles](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [Configuraciones del modelo de Multi-Site Manager](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Configuraciones de lanzamiento del administrador de varios sitios](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [Plantilla de correo electrónico de notificación de eventos de página](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [Andamiaje de páginas](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [Cuadrícula adaptable MENOS](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [Diseños de plantilla estáticos](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)
* [Bibliotecas de clientes de Adobe Search and Promote Integration](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries)
* [Bibliotecas de clientes de integración de Adobe Target](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [Bibliotecas de cliente de WCM Foundation](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

## Con actualización de 6.5 {#with-upgrade}

### Segmentos de ContextHub {#contexthub-segments}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/segmentation/contexthub</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/apps/settings/wcm/segments</code> </p> <p><code>/conf/settings/settings/wcm/segments</code> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Si algún segmento de ContextHub nuevo o modificado está pensado para editarse en control de código fuente en lugar de editarse en AEM, debe migrarse a la nueva ubicación:</p>
    <ol>
     <li>Copie cualquier segmento de ContextHub nuevo o modificado de la ubicación anterior a la nueva ubicación apropiada (/<code>apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>)</li>
     <li>Actualice las referencias a los segmentos de ContextHub en la ubicación anterior a los segmentos de ContextHub migrados en las nuevas ubicaciones (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
    </ol> <p>La siguiente consulta de QueryBuilder localiza todas las referencias a los segmentos de ContextHub en las ubicaciones anteriores.<br /> <br /> <code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> <br /> Esto se puede ejecutar a través de  <a href="/help/sites-developing/querybuilder-api.md" target="_blank">AEM interfaz de usuario de QueryBuilder Debugger</a>. Tenga en cuenta que esta es una consulta que atraviesa, por lo que no la ejecute con la producción y asegúrese de que los límites transversales estén ajustados según sea necesario.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Los segmentos de ContextHub persistían en la visualización de la ubicación anterior como solo lectura en <strong>AEM &gt; Personalización &gt; Audiencias</strong>.</p> <p>Si los segmentos de ContextHub se pueden editar en AEM, se deben migrar a la nueva ubicación (<code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>). Los segmentos de ContentHub creados en AEM se mantienen en la nueva ubicación (<code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</p> <p>Las propiedades de página de AEM Sites solo permiten seleccionar la ubicación anterior (<code>/etc</code>) o una sola ubicación nueva (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>), por lo que los segmentos de ContextHub deben migrarse según corresponda.</p> <p>Los segmentos de ContextHub no utilizados de AEM sitios de referencia se pueden eliminar y no migrar a la nueva ubicación:</p>
    <ul>
     <li>/etc/segmentation/geometrixx/</li>
     <li>/etc/segmentation/geometrixx-outdoors</li>
    </ul> <p>Nota: Si el ClientContext está en uso, se recomienda convertir a ContextHub.</p> </td>
  </tr>
 </tbody>
</table>

## Antes de la actualización futura {#prior-to-upgrade}

### Bibliotecas de cliente de Adobe Analytics {#adobe-analytics-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><p><code>/etc/clientlibs/foundation/sitecatalyst</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier uso personalizado de estas bibliotecas de cliente debe hacer referencia a la biblioteca de cliente por categoría y no por ruta:</p>
    <ol>
     <li>Cualquier referencia a la biblioteca de cliente por ruta de acceso en la ubicación anterior debe actualizarse para utilizar <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM Client Library reference framework</a>.</li>
     <li>Si no se puede utilizar AEM marco de referencia de la biblioteca de cliente, se puede hacer referencia a la ruta absoluta de las bibliotecas de cliente mediante AEM servlet proxy de la biblioteca de cliente.
      <ul>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/appmeasurement.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/plugins.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/tracking.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/util.js</code></li>
      </ul> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Nunca se admitió la edición de estas bibliotecas de cliente.</p> <p>Para obtener las categorías de la biblioteca de cliente, visite cada nodo <code>cq:ClientLIbraryFolder</code> a través de CRXDELite e inspeccione la propiedad categories .</p>
    <ul>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/appmeasurement</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/plugins</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/tracking</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/util</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Diseños clásicos de Microsoft Word para páginas web {#classic-microsoft-word-to-web-page-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/designs/wordDesign</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/wcm/designs/wordDesign</code></p> <p><code>/apps/settings/wcm/designs/wordDesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en tiempo de ejecución mediante los cuadros de diálogo de diseño.</p>
    <ol>
     <li>Copie los diseños de la ubicación anterior a la nueva ubicación (<code>/apps</code>).</li>
     <li>Convierta cualquier recurso CSS, JavaScript y estático en el diseño a una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">biblioteca de cliente</a> con <code>allowProxy = true</code>.</li>
     <li>Actualice las referencias a la ubicación anterior en la propiedad cq:designPath.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría Biblioteca de cliente (esto requiere actualizar el código de implementación de página).</li>
     <li>Actualice AEM reglas de Dispatcher para permitir el servicio de bibliotecas de cliente a través del servlet proxy <code>/etc.clientlibs/</code>.</li>
    </ol> <p>Para cualquier diseño que NO se administre en SCM y que se modifique en tiempo de ejecución mediante los cuadros de diálogo de diseño:</p>
    <ul>
     <li>No mueva los diseños de autor fuera de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configuraciones del emulador de dispositivos móviles {#mobile-device-emulator-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><p><code>/etc/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/mobile</code></p> <p><code>/apps/settings/mobile</code></p> <p><code>/conf/global/settings/mobile</code></p> <p><code>/conf/&lt;tenant&gt;/settings/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td>Las configuraciones del emulador de dispositivos móviles nuevas deben migrarse a la ubicación nueva.
    <ol>
     <li>Copie cualquier configuración nueva del emulador de dispositivo móvil de la ubicación anterior a la nueva ubicación (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
     <li>Para cualquier página de AEM Sites que dependa de estas configuraciones del emulador de dispositivos móviles, actualice la página <span class="code">
       <code>
        jcr
       </code>
       <code>
        :content
       </code></span> nodo: <br /> <span class="code">[cq:Page]/jcr:content@cq:
       <code>
        deviceGroups
       </code> = String[ mobile/groups/responsive ]</span></li>
     <li>Para cualquier plantilla editable que dependa de estas configuraciones del emulador de dispositivos móviles, actualice las plantillas editables señalando el <span class="code">
       <code>
        cq
       </code>:
       <code>
        deviceGroups
       </code></span> a la ubicación nueva.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>La resolución de configuraciones del emulador de dispositivos móviles se produce en el siguiente orden:</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/mobile</code></li>
     <li><code>/conf/global/settings/mobile</code></li>
     <li><code>/apps/settings/mobile</code></li>
     <li><code>/libs/settings/mobile</code></li>
     <li><code>/etc/mobile</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Configuraciones del modelo del administrador de varios sitios {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/apps/msm</code> (Configuraciones del modelo del cliente)</p> <p><code>/libs/msm</code> (Configuraciones de modelo predeterminadas para Screens, Commerce)</p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier configuración de modelo de Multi-site Manager nueva o modificada debe migrarse a la nueva ubicación (<code>/apps</code>).</p>
    <ol>
     <li>Copie cualquier configuración de modelo de Multi-site Manager nueva o modificada de la ubicación anterior a la nueva ubicación (<code>/apps</code>).</li>
     <li>Elimine cualquier configuración de modelo de Multi-site Manager migrada de la ubicación anterior.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Todas las configuraciones de modelo de Multi-site Manager proporcionadas AEM existen en la Nueva ubicación de <code>/libs</code>.</p> <p>El contenido no hace referencia a las configuraciones azules del administrador de varios sitios, por lo que no hay referencias de contenido para ajustar.</p> </td>
  </tr>
 </tbody>
</table>

### Configuraciones de lanzamiento del administrador de varios sitios {#multi-site-manager-rollout-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><p><code>/etc/msm/rolloutConfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/msm/wcm/rolloutconfigs</code></p> <p><code>/apps/msm/wcm/rolloutconfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier configuración de lanzamiento del administrador de varios sitios nueva o modificada debe migrarse a la ubicación nueva.</p>
    <ol>
     <li>Copie cualquier configuración de lanzamiento del administrador de varios sitios nueva o modificada de la ubicación anterior a la nueva ubicación (<code>/apps</code>).</li>
     <li>Actualice cualquier referencia en AEM páginas a configuraciones de despliegue de administrador de varios sitios en la ubicación anterior, para que apunte a sus homólogos en las nuevas ubicaciones (<code>/libs</code> o <code>/apps</code>).</li>
    </ol> <p>Elimine las configuraciones de lanzamiento migradas del administrador de varios sitios de la ubicación anterior.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Si no se eliminan las configuraciones de implementación migradas del administrador de varios sitios de la ubicación anterior, se mostrarán opciones de implementación duplicadas a los autores de AEM.</td>
  </tr>
 </tbody>
</table>

### Plantilla de correo electrónico de notificación de eventos de página {#page-event-notification-e-mail-template}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Las únicas plantillas de correo electrónico de notificación de eventos de página compatibles son las nuevas configuraciones regionales.</p> <p>La resolución de la plantilla de correo electrónico de Evento de página se produce en el siguiente orden:</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li>
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Las plantillas de correo electrónico de notificación de eventos de página nuevas o modificadas deben migrarse a la nueva ubicación en <code>/apps</code>:</p>
    <ol>
     <li>Copie cualquier plantilla de correo electrónico de notificación de eventos de página nueva o modificada de la Ubicación anterior a la nueva ubicación (<code>/apps</code>).</li>
     <li>Elimine las plantillas de correo electrónico de notificación de eventos de página migradas de la ubicación anterior.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Andamiaje de páginas {#page-scaffolding}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/scaffolding</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><span class="code">/libs/settings/
      <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> <p><span class="code">/apps/settings/
      <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td>El scaffolding creado en Ubicación anterior utiliza el marco de scaffolding heredado y no se puede migrar a la Nueva ubicación. Para alinearse con la Nueva ubicación, cualquier Scaffolding heredado debe ser redesarrollado usando el marco de Scaffolding admitido.</td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Cuadrícula interactiva MENOS {#responsive-grid-less}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier referencia a la Ubicación anterior en los archivos LESS personalizados debe actualizarse para importarse desde la Nueva ubicación.</p>
    <ul>
     <li>Actualice cualquier referencia a archivos LESS personalizados que hagan referencia a grid_base.less en la Ubicación anterior para hacer referencia a la nueva ubicación.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Al hacer referencia a un archivo <code>grid_base.less</code> no existente, el modo Diseño del Editor de plantillas y páginas no funciona, y se interrumpe el diseño de la página.</td>
  </tr>
 </tbody>
</table>

### Diseños de plantilla estáticos {#static-template-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/apps/settings/wcm/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en tiempo de ejecución mediante los cuadros de diálogo de diseño.</p>
    <ol>
     <li>Copie los diseños de la ubicación anterior a la nueva ubicación (<code>/apps</code>).</li>
     <li>Convierta cualquier recurso CSS, JavaScript y estático en el diseño a una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">biblioteca de cliente</a> con <code>allowProxy = true</code>.</li>
     <li>Actualice las referencias a la ubicación anterior en la propiedad <code>cq:designPath</code> mediante <strong>AEM &gt; Sitios &gt; Páginas de sitio personalizadas &gt; Propiedades de página &gt; Pestaña avanzada &gt; Campo de diseño</strong>.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría Biblioteca de cliente (esto requiere actualizar el código de implementación de página).</li>
     <li>Actualice AEM reglas de Dispatcher para permitir el servicio de bibliotecas de cliente a través del servlet proxy <code>/etc.clientlibs/</code>.</li>
    </ol> <p>Para cualquier diseño que NO se administre en SCM y que se modifique en tiempo de ejecución mediante los cuadros de diálogo de diseño:</p>
    <ul>
     <li>No mueva los diseños de autor fuera de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>El método recomendado es crear AEM Sites y páginas utilizando plantillas editables que utilicen contenido de estructura y políticas en lugar de diseños.</td>
  </tr>
 </tbody>
</table>

### Bibliotecas de cliente de integración de Adobe Search and Promote {#adobe-search-and-promote-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><p><code>/etc/clientlibs/foundation/searchpromote</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier uso personalizado de estas bibliotecas de cliente debe hacer referencia a la biblioteca de cliente por categoría y no por ruta.</p>
    <ol>
     <li>Cualquier referencia a la biblioteca de cliente por ruta de acceso en la ubicación anterior debe actualizarse para utilizar <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM Client Library reference framework</a>.</li>
     <li>Si no se puede utilizar AEM marco de referencia de la biblioteca de cliente, se puede hacer referencia a la ruta absoluta de las bibliotecas de cliente mediante AEM servlet proxy de la biblioteca de cliente:</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/searchpromote/clientlibs/searchpromotei.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Nunca se admitió la edición de estas bibliotecas de cliente.</p> <p>Para obtener las categorías de la biblioteca de cliente, visite cada nodo cq:ClientLIbraryFolder a través de CRXDELite e inspeccione la propiedad categories :</p>
    <ul>
     <li><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Bibliotecas de cliente de integración de Adobe Target {#adobe-target-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><p><code>/etc/clientlibs/foundation/target</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/libs/cq/testandtarget/clientlibs/testandtarget</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier uso personalizado de estas bibliotecas de cliente debe hacer referencia a la biblioteca de cliente por categoría y no por ruta.</p>
    <ol>
     <li>Cualquier referencia a la biblioteca de cliente por ruta de acceso en la ubicación anterior debe actualizarse para utilizar <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM Client Library reference framework</a>.</li>
     <li>Si no se puede utilizar AEM marco de referencia de la biblioteca de cliente, se puede hacer referencia a la ruta absoluta de las bibliotecas de cliente mediante AEM servlet proxy de la biblioteca de cliente:</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/testandtarget.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/atjs.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/atjs-integration.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/init.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/mbox.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/parameters.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/util.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Nunca se admitió la edición de estas bibliotecas de cliente.</p> <p>Para obtener las categorías de la biblioteca de cliente, visite cada nodo cq:ClientLIbraryFolder a través de CRXDELite e inspeccione la propiedad categories :</p>
    <ul>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/testandtarget</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/atjs</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/atjs-integration</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/init</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/mbox</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/parameters</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/util</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Bibliotecas de cliente de WCM Foundation {#wcm-foundation-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><p><code>/etc/clientlibs/wcm/foundation</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier uso personalizado de estas bibliotecas de cliente debe hacer referencia a la biblioteca de cliente por categoría y no por ruta.</p>
    <ol>
     <li>Cualquier referencia a la biblioteca de cliente por ruta de acceso en la ubicación anterior debe actualizarse para utilizar <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM Client Library reference framework</a>.</li>
     <li>Si no se puede utilizar AEM marco de referencia de la biblioteca de cliente, se puede hacer referencia a la ruta absoluta de las bibliotecas de cliente mediante AEM servlet proxy de la biblioteca de cliente.</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/accessibility.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Nunca se admitió la edición de estas bibliotecas de cliente.</p> <p>Para obtener las categorías de la biblioteca de cliente, visite cada nodo <code>cq:ClientLIbraryFolder</code> a través de CRXDELite e inspeccione la propiedad categories :</p>
    <ul>
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li>
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

