---
title: AEM Reestructuración de repositorios de Sites en 6.5
description: AEM Obtenga información sobre cómo realizar los cambios necesarios para migrar a la nueva estructura de repositorios en la versión 6.5 de la versión para sitios de.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: b4531792-06dd-4545-9dbb-57224be20dc7
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1464'
ht-degree: 1%

---

# AEM Reestructuración de repositorios de Sites en 6.5 {#sites-repository-restructuring-in-aem}

Como se describe en el elemento principal [AEM Reestructuración de repositorios en 6.5](/help/sites-deploying/repository-restructuring.md) AEM , los clientes que actualicen a la versión 6.5 deben utilizar esta página para evaluar el esfuerzo de trabajo asociado con los cambios del repositorio que afectan a la solución de AEM Sites. AEM Algunos cambios requieren un esfuerzo durante el proceso de actualización de la versión 6.5 de la, mientras que otros se pueden aplazar hasta una actualización futura.

**Con actualización a 6.5**

* [Segmentos de ContextHub](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**Antes de una actualización futura**

* [Bibliotecas de cliente de Adobe Analytics](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [Diseños clásicos de Word a página web de Microsoft](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [Configuraciones del emulador de dispositivos móviles](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [Configuraciones del modelo de administración de varios sitios](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Configuraciones de despliegue del administrador de varios sitios](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [Plantilla de correo electrónico de notificación de eventos de página](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [Andamiaje de página](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [Cuadrícula interactiva LESS](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [Diseños de plantilla estática](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)
<!-- Search&Promote is end-of-life September 1, 2022 * [Adobe Search and Promote Integration Client Libraries](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries) -->
* [Bibliotecas de cliente de integración de Adobe Target](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [Bibliotecas de cliente de WCM Foundation](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

## Con actualización a 6.5 {#with-upgrade}

### Segmentos de ContextHub {#contexthub-segments}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/segmentation/contexthub</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/apps/settings/wcm/segments</code><br /> </p> <p><code>/conf/settings/settings/wcm/segments</code><br /> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>AEM Si algún segmento de ContextHub nuevo o modificado se edita en el control de código fuente en lugar de editarse en el control de código fuente, se debe migrar a la nueva ubicación:</p>
    <ol>
     <li>Copie cualquier segmento de ContextHub nuevo o modificado de la ubicación anterior a la nueva ubicación adecuada (/)<code>apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>)</li>
     <li>Actualizar referencias a segmentos de ContextHub en la ubicación anterior a segmentos de ContextHub migrados en las nuevas ubicaciones (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
    </ol> <p>La siguiente consulta de QueryBuilder busca todas las referencias a segmentos de ContextHub en las ubicaciones anteriores.<br /> <br /> <code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> <br /> Esto se puede ejecutar mediante <a href="/help/sites-developing/querybuilder-api.md" target="_blank">AEM IU de QueryBuilder Debugger</a>. Tenga en cuenta que se trata de una consulta de recorrido, por lo que no la ejecute en producción y asegúrese de ajustar los límites transversales según sea necesario.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Los segmentos de ContextHub que persistieron en la ubicación anterior se muestran como de solo lectura en <strong>AEM &gt; Personalización &gt; Audiencias</strong>.</p> <p>AEM Si los segmentos de ContextHub van a poder editarse en la, deben migrarse a la nueva ubicación (<code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>). AEM Cualquier nuevo segmento de segmentos de ContentHub creado en la se mantiene en la nueva ubicación (<code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</p> <p>Las propiedades de página de AEM Sites solo permiten la ubicación anterior (<code>/etc</code>) o una sola ubicación nueva (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>) que se van a seleccionar, por lo que los segmentos de ContextHub deben migrarse en consecuencia.</p> <p>AEM Los segmentos de ContextHub no utilizados de los sitios de referencia de la se pueden eliminar y no migrar a la nueva ubicación:</p>
    <ul>
     <li>/etc/segmentation/geometrixx/</li>
     <li>/etc/segmentation/geometrixx-outdoors</li>
    </ul> <p>Nota: Si el ClientContext está en uso, se recomienda convertirlo a ContextHub.</p> </td>
  </tr>
 </tbody>
</table>

## Antes de una actualización futura {#prior-to-upgrade}

### Bibliotecas de cliente de Adobe Analytics {#adobe-analytics-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><p><code>/etc/clientlibs/foundation/sitecatalyst</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier uso personalizado de estas bibliotecas de cliente debe hacer referencia a la biblioteca de cliente por categoría y no por ruta:</p>
    <ol>
     <li>Cualquier referencia a la biblioteca de cliente por ruta en la ubicación anterior debe actualizarse para utilizar <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM Marco de referencia de la biblioteca de clientes</a>.</li>
     <li>AEM AEM Si no se puede utilizar el marco de referencia de la biblioteca de cliente de la biblioteca de cliente, se puede hacer referencia a la ruta absoluta de las bibliotecas de cliente mediante el servlet proxy de la biblioteca de cliente de la biblioteca de cliente de la biblioteca de cliente.
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
   <td><p>Nunca se admitió la edición de estas bibliotecas de cliente.</p> <p>Para obtener las categorías de Biblioteca de clientes, visite cada una <code>cq:ClientLIbraryFolder</code> a través de CRXDELite e inspeccione la propiedad categories.</p>
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

### Diseños clásicos de Word a página web de Microsoft {#classic-microsoft-word-to-web-page-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/designs/wordDesign</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/wcm/designs/wordDesign</code></p> <p><code>/apps/settings/wcm/designs/wordDesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en en tiempo de ejecución mediante cuadros de diálogo de diseño.</p>
    <ol>
     <li>Copie los diseños de la Ubicación anterior en la Ubicación nueva (<code>/apps</code>).</li>
     <li>Convierta cualquier recurso CSS, JavaScript y estático de Design a un <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Biblioteca de cliente</a> con <code>allowProxy = true</code>.</li>
     <li>Actualice las referencias a la Ubicación anterior en la propiedad cq:designPath.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría Biblioteca de clientes (esto requiere la actualización del código de implementación de la página).</li>
     <li>AEM Actualizar las reglas de Dispatcher para permitir el servicio de bibliotecas de cliente a través de <code>/etc.clientlibs/</code> servlet proxy.</li>
    </ol> <p>Para cualquier diseño que NO se administre en SCM y que se modifique en tiempo de ejecución mediante cuadros de diálogo de diseño:</p>
    <ul>
     <li>No saque los diseños con autor de <code>/etc</code>.</li>
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
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/mobile</code></p> <p><code>/apps/settings/mobile</code></p> <p><code>/conf/global/settings/mobile</code></p> <p><code>/conf/&lt;tenant&gt;/settings/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td>Cualquier nueva configuración del emulador de dispositivos móviles debe migrarse a la nueva ubicación.
    <ol>
     <li>Copie cualquier nueva configuración del emulador de dispositivos móviles de la ubicación anterior a la nueva ubicación (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
     <li>Para cualquier página de AEM Sites que dependa de estas configuraciones del emulador de dispositivos móviles, actualice el <span class="code">
       <code>
        jcr
       </code>
       <code>
        :content
       </code></span> nodo: <br /> <span class="code">[cq:Page]/jcr:content@cq:
       <code>
        deviceGroups
       </code> = String[ mobile/groups/responsive ]</span></li>
     <li>Para cualquier plantilla editable que dependa de estas configuraciones del emulador de dispositivos móviles, actualice las plantillas editables, señalando la opción <span class="code">
       <code>
        cq
       </code>:
       <code>
        deviceGroups
       </code></span> a la Nueva ubicación.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>La resolución de las configuraciones del emulador de dispositivos móviles se produce en el siguiente orden:</p>
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

### Configuraciones del modelo de administración de varios sitios {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/apps/msm</code> (Configuraciones del modelo del cliente)</p> <p><code>/libs/msm</code> (Configuraciones de modelo listas para usar para Screens, Commerce)</p> </td>
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
   <td><p>AEM Todas las configuraciones de modelo de administración de varios sitios proporcionadas se encuentran en la nueva ubicación de <code>/libs</code>.</p> <p>El contenido no hace referencia a las configuraciones azules del Administrador de varios sitios, por lo que no hay referencias de contenido que ajustar.</p> </td>
  </tr>
 </tbody>
</table>

### Configuraciones de despliegue del administrador de varios sitios {#multi-site-manager-rollout-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><p><code>/etc/msm/rolloutConfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/msm/wcm/rolloutconfigs</code></p> <p><code>/apps/msm/wcm/rolloutconfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier configuración de despliegue del administrador de varios sitios nueva o modificada debe migrarse a la nueva ubicación.</p>
    <ol>
     <li>Copie cualquier configuración de lanzamiento del Administrador de varios sitios nueva o modificada de la ubicación anterior a la nueva ubicación (<code>/apps</code>).</li>
     <li>AEM Actualice las referencias de las páginas de la lista de direcciones a Configuraciones de despliegue del Administrador de varios sitios en la ubicación anterior para que apunten a sus equivalentes en las nuevas ubicaciones (<code>/libs</code> o <code>/apps</code>).</li>
    </ol> <p>Quitar las configuraciones de despliegue del Administrador de varios sitios migradas de la ubicación anterior.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>AEM Si no se quitan las configuraciones de despliegue del Administrador de varios sitios migradas de la ubicación anterior, se mostrarán opciones de despliegue duplicadas a los autores de la.</td>
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
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Las únicas plantillas de correo electrónico de notificación de eventos de página nuevas admitidas son las nuevas configuraciones regionales.</p> <p>Evento de página La resolución de la plantilla de correo electrónico se produce en el siguiente orden:</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li>
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Cualquier plantilla de correo electrónico de notificación de eventos de página nueva o modificada debe migrarse a la nueva ubicación en <code>/apps</code>:</p>
    <ol>
     <li>Copie cualquier plantilla de correo electrónico de notificación de eventos de página nueva o modificada de la ubicación anterior a la nueva ubicación (<code>/apps</code>).</li>
     <li>Quite las plantillas de correo electrónico de notificación de eventos de página migradas de la ubicación anterior.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Andamiaje de página {#page-scaffolding}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/scaffolding</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
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
   <td>El andamiaje creado en la ubicación anterior utiliza el marco de andamiaje heredado y no se puede migrar a la nueva ubicación. Para alinearse con la Nueva ubicación, cualquier andamiaje heredado debe volver a desarrollarse utilizando el marco de andamiaje admitido.</td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Cuadrícula interactiva LESS {#responsive-grid-less}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier referencia a la Ubicación anterior en los archivos personalizados LESS debe actualizarse para poder importarse desde la Nueva ubicación.</p>
    <ul>
     <li>Actualice los archivos LESS personalizados que hagan referencia a grid_base.less en la Ubicación anterior para hacer referencia a la nueva ubicación.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Referencia a un archivo no existente <code>grid_base.less</code> Esto provoca que el modo Diseño del Editor de páginas y plantillas no funcione y que se interrumpa el diseño de la página.</td>
  </tr>
 </tbody>
</table>

### Diseños de plantilla estática {#static-template-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><code>/apps/settings/wcm/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en en tiempo de ejecución mediante cuadros de diálogo de diseño.</p>
    <ol>
     <li>Copie los diseños de la Ubicación anterior en la Ubicación nueva (<code>/apps</code>).</li>
     <li>Convierta cualquier recurso CSS, JavaScript y estático de Design a un <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Biblioteca de cliente</a> con <code>allowProxy = true</code>.</li>
     <li>Actualice las referencias a la Ubicación anterior en la <code>cq:designPath</code> propiedad mediante <strong>AEM &gt; Sitios &gt; Páginas de sitio personalizadas &gt; Propiedades de página &gt; Pestaña Avanzadas &gt; Campo de diseño</strong>.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría Biblioteca de clientes (esto requiere la actualización del código de implementación de la página).</li>
     <li>AEM Actualizar las reglas de Dispatcher para permitir el servicio de bibliotecas de cliente a través de <code>/etc.clientlibs/</code> servlet proxy.</li>
    </ol> <p>Para cualquier diseño que NO se administre en SCM y que se modifique en tiempo de ejecución mediante cuadros de diálogo de diseño:</p>
    <ul>
     <li>No saque los diseños con autor de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>El método recomendado es crear AEM Sites y páginas mediante plantillas editables que utilicen contenido de estructura y directivas en lugar de diseños.</td>
  </tr>
 </tbody>
</table>

<!-- Search&Promote is end of life as of September 1, 2022 ### Adobe Search and Promote Integration Client Libraries {#adobe-search-and-promote-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Previous location</strong></td>
   <td><p><code>/etc/clientlibs/foundation/searchpromote</code></p> </td>
  </tr>
  <tr>
   <td><strong>New location(s)</strong></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
  </tr>
  <tr>
   <td><strong>Restructuring guidance</strong></td>
   <td><p>Any custom use of these Client Libraries should reference the Client Library by category, and not by path.</p>
    <ol>
     <li>Any references to the Client Library by path at the Previous Location should be updated to use <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM's Client Library referencing framework</a>.</li>
     <li>If AEM's Client Library referencing framework cannot be used, the absolute path of the Client Libraries can be referenced via AEM's Client Library Proxy servlet:</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/searchpromote/clientlibs/searchpromotei.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td><p>Editing of these Client Libraries was never supported.</p> <p>To obtain the Client Library categories, visit each cq:ClientLIbraryFolder node via CRXDELite and inspect the categories property:</p>
    <ul>
     <li><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table> -->

### Bibliotecas de cliente de integración de Adobe Target {#adobe-target-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><p><code>/etc/clientlibs/foundation/target</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><code>/libs/cq/testandtarget/clientlibs/testandtarget</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier uso personalizado de estas bibliotecas de cliente debe hacer referencia a la biblioteca de cliente por categoría y no por ruta.</p>
    <ol>
     <li>Cualquier referencia a la biblioteca de cliente por ruta en la ubicación anterior debe actualizarse para utilizar <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM Marco de referencia de la biblioteca de clientes</a>.</li>
     <li>AEM AEM Si no se puede utilizar el marco de referencia de la biblioteca de cliente de la biblioteca de cliente, se puede hacer referencia a la ruta absoluta de las bibliotecas de cliente mediante el servlet proxy de la biblioteca de cliente:</li>
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
   <td><p>Nunca se admitió la edición de estas bibliotecas de cliente.</p> <p>Para obtener las categorías de la Biblioteca de clientes, visite cada nodo cq:ClientLibraryFolder a través de CRXDELite e inspeccione la propiedad categories:</p>
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
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier uso personalizado de estas bibliotecas de cliente debe hacer referencia a la biblioteca de cliente por categoría y no por ruta.</p>
    <ol>
     <li>Cualquier referencia a la biblioteca de cliente por ruta en la ubicación anterior debe actualizarse para utilizar <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM Marco de referencia de la biblioteca de clientes</a>.</li>
     <li>AEM AEM Si no se puede utilizar el marco de referencia de la biblioteca de cliente de la biblioteca de cliente, se puede hacer referencia a la ruta absoluta de las bibliotecas de cliente mediante el servlet proxy de la biblioteca de cliente de la biblioteca de cliente de la biblioteca de cliente.</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/accessibility.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Nunca se admitió la edición de estas bibliotecas de cliente.</p> <p>Para obtener las categorías de Biblioteca de clientes, visite cada una <code>cq:ClientLIbraryFolder</code> a través de CRXDELite e inspeccione la propiedad categories:</p>
    <ul>
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li>
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>
