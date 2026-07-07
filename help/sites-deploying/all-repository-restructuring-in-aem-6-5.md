---
title: Reestructuración de repositorios comunes en AEM 6.5
description: Aprenda a realizar los cambios necesarios para migrar a la nueva estructura de repositorios de AEM 6.5, que son comunes en todas las áreas de AEM.
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
exl-id: 2d852d9d-9be3-487a-966a-4902bd7df7f9
solution: Experience Manager, Experience Manager Sites
feature: Upgrading
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2770'
ht-degree: 4%

---

# Reestructuración de repositorios comunes en AEM 6.5 {#common-repository-restructuring-in-aem}

Como se describe en la página principal [Reestructuración del repositorio en AEM 6.5](/help/sites-deploying/repository-restructuring.md), los clientes que actualicen a AEM 6.5 deben utilizar esta página para evaluar el esfuerzo de trabajo asociado con los cambios del repositorio que pueden afectar a todas las soluciones. Algunos cambios requieren esfuerzo durante el proceso de actualización de AEM 6.5, mientras que otros se pueden aplazar hasta una actualización futura.

**Con Actualización 6.5**

* [Configuración de ContextHub](#contexthub-6.5)
* [Instancias de flujo de trabajo](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [Modelos de flujo de trabajo](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [Lanzadores de flujo de trabajo](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [Scripts de flujo de trabajo](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**Antes de una actualización futura**

* [Configuración de ContextHub](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [Diseños de servicios de nube clásicos](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [Diseños de paneles clásicos](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [Diseños clásicos de informes](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [Diseños predeterminados](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [Punto final de Adobe DTM JavaScript](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [Punto final de enlace web de Adobe DTM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [Tareas de bandeja de entrada](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [Configuraciones del modelo de administración de varios sitios](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Configuraciones de gadgets del panel de proyectos AEM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [Plantilla de correo electrónico de notificación de replicación](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [Etiquetas](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [Cloud Services de traducción](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [Idiomas de traducción](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [Reglas de traducción](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [Biblioteca de cliente del widget de traducción](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [Consola web de activación de árbol](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [Cloud Services de conector de traducción del proveedor](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [Plantillas de correo electrónico de notificación de flujo de trabajo](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## Con actualización a 6.5 {#with-upgrade}

### Configuración de ContextHub {#contexthub-6.5}

A partir de AEM 6.4, no hay ninguna configuración predeterminada de ContextHub. Por lo tanto, en el nivel raíz del sitio, se debe establecer un `cq:contextHubPathproperty` para indicar qué configuración se debe utilizar.

1. Vaya a la raíz del sitio.
1. Abra las propiedades de página de la página raíz y seleccione la pestaña Personalization.
1. En el campo Ruta de Contexthub, introduzca su propia ruta de configuración de ContextHub.

Además, en la configuración de ContextHub, `sling:resourceType` debe actualizarse para que sea relativo y no absoluto.

1. Abra las propiedades del nodo de configuración de ContextHub en CRX DE Lite; por ejemplo, `/apps/settings/cloudsettings/legacy/contexthub`
1. Cambiar `sling:resourceType` de `/libs/granite/contexthub/cloudsettings/components/baseconfiguration` a `granite/contexthub/cloudsettings/components/baseconfiguration`

Es decir, el `sling:resourceType` de la configuración de ContextHub debe ser relativo en lugar de absoluto.

### Modelos de flujo de trabajo {#workflow-models}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/workflow/models</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> <p><code>/var/workflow/models</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier modelo de flujo de trabajo nuevo o modificado debe migrarse a /conf/global/workflow/models.</p>
    <ol>
     <li>Implemente los modelos de flujo de trabajo modificados en una instancia de desarrollo de AEM 6.5 local, de modo que existan en la ubicación Anterior.</li>
     <li>Edite el modelo de flujo de trabajo con el Editor del modelo de flujo de trabajo de AEM en AEM &gt; Herramientas &gt; Flujo de trabajo &gt; Modelos.</li>
     <li>Al migrar modelos de flujo de trabajo modificados proporcionados por AEM
      <ol>
       <li>Con el Editor del modelo de flujo de trabajo abierto, modifique la dirección URL del explorador y reemplace el segmento de ruta /libs/settings/workflow/models por /etc/workflow/models.
        <ul>
         <li>Por ejemplo, cambie: <em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/models</strong>/dam/update_asset.html</em> a <em>http://localhost:4502/editor.html<strong>/etc/workflow/models</strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>Habilite el modo de edición en el Editor del modelo de flujo de trabajo, que copiará la definición del modelo de flujo de trabajo en /conf/global/workflow/models.</li>
     <li>Seleccione el botón Sincronizar para sincronizar los cambios en el Modelo de flujo de trabajo en tiempo de ejecución en /var/workflow/models.</li>
     <li>Exporte el modelo de flujo de trabajo (/conf/global/workflow/models/&lt;workflow-model&gt;) y el modelo de flujo de trabajo de tiempo de ejecución (/var/workflow/models/&lt;workflow-model&gt;) e integre en el proyecto de AEM.
      <ol>
       <li>Por ejemplo, exportar:
        <ul>
         <li><code>/conf/global/settings/workflow/models/dam/my_workflow_model</code><br /> y </li>
         <li><code>/var/workflow/models/dam/my_workflow_model</code></li>
        </ul> </li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>La resolución del modelo de flujo de trabajo se produce en el siguiente orden:</p>
    <ol>
     <li><code>/conf/global/settings/workflow/models</code></li>
     <li><code>/libs/settings/workflow/models</code></li>
     <li><code>/etc/workflow/models</code></li>
    </ol> <p>Por lo tanto, cualquier personalización de los modelos de flujo de trabajo proporcionados por AEM que persista en la ubicación anterior debe moverse a /conf/global/settings/workflow/models si se va a conservar, de lo contrario, se reemplazarán con la definición del modelo de flujo de trabajo proporcionado por AEM en /libs/settings/workflow/models.</p> </td>
  </tr>
 </tbody>
</table>

### Instancias de flujo de trabajo {#workflow-instances}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><code>/var/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>No se requiere ninguna acción para alinearse con la Nueva ubicación.</p> <p>Las instancias de flujo de trabajo históricas pueden seguir residiendo de forma segura en la ubicación anterior y se crearán nuevas instancias de flujo de trabajo en la nueva ubicación.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Cualquier referencia de ruta explícita en
    El código <code>
     custom
    </code> de la ubicación anterior también debe tener en cuenta la nueva ubicación. Se recomienda refactorizar este código para utilizar las API de flujo de trabajo de AEM.</td>
  </tr>
 </tbody>
</table>

### Lanzadores de flujo de trabajo {#workflow-launchers}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/workflow/launcher/config</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/workflow/launcher/config</code></p> <p><code>/conf/global/settings/workflow/launcher/config</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier lanzador de flujo de trabajo nuevo o modificado debe migrarse a <code>/conf/global/workflow/launcher/config</code>.</p>
    <ol>
     <li>Copie cualquier configuración del lanzador de flujos de trabajo nueva o modificada de la ubicación anterior a la nueva ubicación (<code>/conf/global</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>La resolución del lanzador de flujos de trabajo se produce en el siguiente orden:</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>Por lo tanto, cualquier personalización del lanzador de flujos de trabajo proporcionado por AEM que persista en la ubicación anterior debe moverse a la nueva ubicación (<code>/conf/global/settings/workflow/launcher</code>) si se va a conservar; de lo contrario, se reemplazará con la definición del lanzador de flujos de trabajo proporcionada por AEM en <code>/libs/settings/workflow/launcher</code>.</p> </td>
  </tr>
 </tbody>
</table>

### Scripts de flujo de trabajo {#workflow-scripts}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/workflow/scripts</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier script de flujo de trabajo nuevo o modificado debe migrarse a la nueva ubicación y los modelos de flujo de trabajo de referencia deben actualizarse para reflejar la nueva ubicación.</p>
    <ol>
     <li>Copie cualquier script de flujo de trabajo nuevo o modificado de la ubicación anterior a la nueva ubicación.
      <ul>
       <li><code>/apps/workflow/scripts</code> debe mantenerse en SCM.</li>
      </ul> </li>
     <li>Actualice las referencias a los scripts de flujo de trabajo en la ubicación anterior en modelos de flujo de trabajo para que apunten a las nuevas ubicaciones.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>AEM 6.4 SP1, cuando se publica, hace que esta reestructuración se pueda aplazar hasta 6.5
     <code>
      upgrade
     </code>.</p> <p>Si la actualización a AEM 6.4 es anterior a la publicación de AEM 6.4 SP1, esta reestructuración debe realizarse como parte del proyecto de actualización. Sin hacerlo, editar y guardar los pasos del flujo de trabajo que hacen referencia a scripts en la ubicación anterior eliminará por completo la referencia de script de flujo de trabajo del paso de flujo de trabajo, y solo los scripts de flujo de trabajo en nuevas ubicaciones estarán disponibles en la lista desplegable de selección de scripts.</p> </td>
  </tr>
 </tbody>
</table>

## Antes de una actualización futura {#prior-to-upgrade}

### Configuración de ContextHub {#contexthub-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/cloudsettings</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/global/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier configuración de ContextHub nueva o modificada debe migrarse a la nueva ubicación y las páginas de referencia de AEM Sites deben actualizarse para reflejar la nueva ubicación.</p>
    <ol>
     <li>Copie cualquier configuración de ContextHub nueva o modificada de la ubicación anterior a la nueva ubicación.</li>
     <li>Asocie las configuraciones de AEM aplicables a las jerarquías de contenido de AEM.
      <ol>
       <li><strong>Jerarquías de páginas de AEM Sites mediante AEM Sites &gt; Página &gt; Propiedades de página &gt; Pestaña Avanzadas &gt; Configuración de nube</strong>.</li>
      </ol> </li>
     <li>Desasocie cualquier configuración de ContextHub heredada migrada de las jerarquías de contenido de AEM mencionadas anteriormente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Diseños de servicios de nube clásicos {#classic-cloud-services-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/designs/cloudservices</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/wcm/designs/cloudservices</code></p> <p><code>/apps/settings/wcm/designs/cloudservices</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en en tiempo de ejecución mediante cuadros de diálogo de diseño.</p>
    <ol>
     <li>Copie los diseños de la ubicación anterior en la nueva ubicación (<code>/apps</code>).</li>
     <li>Convierta cualquier recurso CSS, JavaScript y estático del diseño en una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">biblioteca de cliente</a> con <code>allowProxy = true</code>.</li>
     <li>Actualice las referencias a la Ubicación anterior en la <span class="code">
       <code>
        cq
       </code>:
       Propiedad <code>
        designPath
       </code></span>.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría Biblioteca de clientes (esto requiere la actualización del código de implementación de la página).</li>
     <li>Actualice las reglas de AEM Dispatcher para permitir el servicio de bibliotecas de cliente a través del servlet proxy /etc.clientlibs/...</li>
    </ol> <p>Para cualquier diseño que NO se haya administrado en SCM y que se haya modificado en tiempo de ejecución mediante cuadros de diálogo de diseño.</p>
    <ul>
     <li>No mueva los diseños que permiten crear de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Diseños de paneles clásicos {#classic-dashboards-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/designs/dashboards</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/wcm/designs/dashboards</code></p> <p><code>/apps/settings/wcm/designs/dashboards</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en en tiempo de ejecución mediante cuadros de diálogo de diseño.</p>
    <ol>
     <li>Copie los diseños de la Ubicación anterior a la Nueva ubicación (/apps).</li>
     <li>Convierta cualquier recurso CSS, JavaScript y estático del diseño en una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">biblioteca de cliente</a> con <code>allowProxy = true</code>.</li>
     <li>Actualice las referencias a la Ubicación anterior en la
      <code>
       cq
      </code>:
      Propiedad <code>
       designPath
      </code>.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría Biblioteca de clientes (esto requiere la actualización del código de implementación de la página).</li>
     <li>Actualice las reglas de AEM Dispatcher para permitir el servicio de bibliotecas de cliente a través del servlet proxy /etc.clientlibs/...</li>
    </ol> <p>Para cualquier diseño que NO se haya administrado en SCM y que se haya modificado en tiempo de ejecución mediante cuadros de diálogo de diseño.</p>
    <ul>
     <li>No mueva los diseños que permiten crear de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Diseños clásicos de informes {#classic-reports-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/designs/reports</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/wcm/designs/reports</code></p> <p><code>/apps/settings/wcm/designs/reports</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en en tiempo de ejecución mediante cuadros de diálogo de diseño.</p>
    <ol>
     <li>Copie los diseños de la Ubicación anterior a la Nueva ubicación (/apps).</li>
     <li>Convierta cualquier recurso CSS, JavaScript y estático del diseño en una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">biblioteca de cliente</a> con <code>allowProxy = true</code>.</li>
     <li>Actualice las referencias a la Ubicación anterior en la
      <code>
       cq
      </code>:
      Propiedad <code>
       designPath
      </code>.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría Biblioteca de clientes (esto requiere la actualización del código de implementación de la página).</li>
     <li>Actualice las reglas de AEM Dispatcher para permitir el servicio de bibliotecas de cliente a través del servlet proxy /etc.clientlibs/...</li>
    </ol> <p>Para cualquier diseño que NO se haya administrado en SCM y que se haya modificado en tiempo de ejecución mediante cuadros de diálogo de diseño.</p>
    <ul>
     <li>No mueva los diseños que permiten crear de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Diseños predeterminados {#default-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/designs/default</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/wcm/designs/default</code></p> <p><code>/apps/settings/wcm/designs/default</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en en tiempo de ejecución mediante cuadros de diálogo de diseño.</p>
    <ol>
     <li>Copie los diseños de la Ubicación anterior a la Nueva ubicación (/apps).</li>
     <li>Convierta cualquier recurso CSS, JavaScript y estático del diseño en una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">biblioteca de cliente</a> con <code>allowProxy = true</code>.</li>
     <li>Actualice las referencias a la Ubicación anterior en la
      <code>
       cq
      </code>:
      Propiedad <code>
       designPath
      </code>.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría Biblioteca de clientes (esto requiere la actualización del código de implementación de la página).</li>
     <li>Actualice las reglas de AEM Dispatcher para permitir el servicio de bibliotecas de cliente a través del servlet proxy /etc.clientlibs/...</li>
    </ol> <p>Para cualquier diseño que NO se haya administrado en SCM y que se haya modificado en tiempo de ejecución mediante cuadros de diálogo de diseño.</p>
    <ul>
     <li>No mueva los diseños que permiten crear de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Punto final de Adobe DTM JavaScript {#adobe-dtm-javascript-endpoint}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/clientlibs/dtm</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><code>/var/cq/dtm/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>No se requiere ninguna acción.</p> <p>La ubicación anterior pública actúa como extremo proxy para la nueva ubicación privada.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Punto final de enlace web de Adobe DTM {#adobe-dtm-web-hook-endpoint}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/dtm-hook</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>No se requiere ninguna acción.</p> <p>La ubicación anterior pública actúa como extremo proxy para la nueva ubicación privada.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Tareas de bandeja de entrada {#inbox-tasks}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><code>/var/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td>Use la <strong>Tarea de mantenimiento de purga de la bandeja de entrada</strong> para quitar las tareas antiguas de la ubicación anterior según sea necesario.</td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>No se requiere ninguna acción para migrar tareas a la nueva ubicación.</p>
    <ul>
     <li>Las tareas presentes en la Ubicación anterior siguen estando disponibles y funcionan.</li>
     <li>Las Tareas nuevas se crean en la Nueva ubicación.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Configuraciones del modelo de administración de varios sitios {#multi-site-manager-blueprint-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong><em></em>Ubicación anterior</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/msm</code></p> <p><code>/apps/msm</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td>
    <ol>
     <li>Copiar configuraciones personalizadas de <code>/etc/blueprints</code> a <code>/apps/msm</code>.</li>
     <li>Quitar <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Configuraciones de gadgets del panel de proyectos AEM {#aem-projects-dashboard-gadget-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/projects/dashboard/gadgets</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/cq/core/content/projects/dashboard/gadgets</code></p> <p><code>/apps/cq/core/content/projects/dashboard/gadgets</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier configuración de gadget del panel de proyectos de AEM nueva o modificada debe migrarse a la nueva ubicación (<code>/apps</code>).</p>
    <ol>
     <li>Copie cualquier configuración de gadget del panel de proyectos de AEM nueva o modificada de la ubicación anterior a la nueva ubicación (<code>/apps</code>).
      <ol>
       <li>No copie configuraciones de gadget del panel de proyectos de AEM sin modificar, ya que ahora existen en la nueva ubicación (<code>/libs</code>).</li>
      </ol> </li>
     <li>Actualice cualquier plantilla de AEM Projects que haga referencia a la ubicación anterior para que apunte a la nueva ubicación adecuada.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Si se aplica el paquete de compatibilidad de AEM 6.4, será necesario realizar las actividades de alineación del repositorio en el momento de la eliminación del paquete de compatibilidad.</td>
  </tr>
 </tbody>
</table>

### Plantilla de correo electrónico de notificación de replicación {#replication-notification-e-mail-template}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/notification/email/default/com.day.cq.replication</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.replication</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.replication</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier plantilla de correo electrónico de notificación de replicación nueva o modificada debe migrarse a la nueva ubicación (<code>/apps</code>)</p>
    <ol>
     <li>Copie las plantillas de correo electrónico de notificación de replicación nuevas o modificadas de la ubicación anterior a la nueva ubicación (<code>/apps</code>).</li>
     <li>Quite las plantillas de correo electrónico de notificación de replicación migradas de la ubicación anterior.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Las únicas plantillas de correo electrónico de notificación de replicación nuevas admitidas son las nuevas configuraciones regionales.</p> <p>La resolución de la plantilla de correo electrónico de notificación de replicación se produce en el siguiente orden:</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.replication</code></li>
     <li><code class="code">/apps/settings/notification-templates/com.day.cq.replication
        </code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.replication</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Etiquetas {#tags}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/tags</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><code>/content/cq:tags</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Todas las etiquetas deben migrarse a <code>/content/cq:tags</code>.</p>
    <ol>
     <li>Copie todas las etiquetas de la ubicación anterior a la nueva ubicación.</li>
     <li>Quitar todas las etiquetas de la ubicación anterior.</li>
     <li>A través de la consola web de AEM, reinicie el paquete OSGi de etiquetado del Día Comunicado 5 en <em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em> para que AEM reconozca que la Nueva ubicación contiene contenido y debe usarse.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Al reiniciar el paquete OSGi de etiquetado comunitario de día, solo se registrará la nueva ubicación como raíz de etiqueta si la ubicación anterior está vacía.</p> <p>Las referencias a la ubicación anterior seguirán funcionando después de migrar a la nueva ubicación para todas las funcionalidades que utilicen la API TagManager de AEM para la resolución de etiquetas.</p> <p>Cualquier código personalizado que haga referencia explícita a la ruta de acceso <code>/etc/tags</code> debe actualizarse a <span class="code">/content/<code>
       cq
      </code>
      <code>
       :tags
      </code></span>, o preferiblemente reescrito para utilizar la API de Java de TagManager junto con esta migración.</p> </td>
  </tr>
 </tbody>
</table>

### Cloud Services de traducción {#translation-cloud-services}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/cloudservices/translation</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/apps/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/global/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier nuevo servicio de nube de traducción debe migrarse a la nueva ubicación (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Migre las configuraciones existentes en la ubicación anterior a la nueva ubicación.
      <ul>
       <li>Vuelva a crear manualmente las nuevas configuraciones de los servicios de nube de traducción mediante la interfaz de usuario de creación de AEM en <strong>Herramientas &gt; Cloud Services &gt; Servicios de nube de traducción</strong>.<br /> OR </li>
       <li>Copie cualquier configuración nueva de los servicios de nube de traducción de la ubicación anterior a la nueva ubicación (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Asocie las configuraciones de AEM aplicables a las jerarquías de contenido de AEM.
      <ol>
       <li>Jerarquías de páginas de AEM Sites mediante <strong>AEM Sites &gt; Página &gt; Propiedades de página &gt; Pestaña Avanzadas &gt; Configuración de nube</strong>.</li>
       <li>Jerarquías de fragmentos de experiencias de AEM mediante <strong>Fragmentos de experiencias de AEM &gt; Fragmento de experiencias &gt; Propiedades &gt; Pestaña Servicios de nube &gt; Configuración de nube</strong>.</li>
       <li>Jerarquías de carpetas de fragmentos de experiencias de AEM a través de <strong>Fragmentos de experiencias de AEM &gt; Carpeta &gt; Propiedades &gt; Pestaña Servicios de nube &gt; Configuración de nube</strong>.<br /> </li>
       <li>AEM Assets las jerarquías de carpetas mediante <strong>AEM Assets &gt; Carpeta &gt; Propiedades de carpeta &gt; Pestaña Cloud Services &gt; Configuración</strong>.</li>
       <li>Proyectos AEM mediante <strong>Proyectos AEM &gt; Proyecto &gt; Propiedades del proyecto &gt; Pestaña Avanzadas &gt; Configuración de nube</strong>.</li>
      </ol> </li>
     <li>Desasocie los servicios de nube de traducción heredados migrados de las jerarquías de contenido de AEM mencionadas anteriormente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>La resolución de los servicios de nube de traducción se produce en el siguiente orden:</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/translationcfg</code></li>
    </ol> <p>Los servicios de nube de traducción migrados deben ser compatibles con AEM 6.4.</p> </td>
  </tr>
 </tbody>
</table>

### Idiomas de traducción {#translation-languages}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/translation/supportedLanguages</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier definición de idioma de traducción nueva o modificada requiere una migración de todas las definiciones de idioma de traducción a la nueva ubicación (<code>/apps</code>).</p>
    <ol>
     <li>Si se han realizado adiciones o modificaciones en las definiciones de idioma de traducción, copie todas las definiciones de idioma de traducción de la ubicación anterior a la nueva ubicación (<code>/apps</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>La resolución de la ruta del idioma de traducción se produce en el siguiente orden:</p>
    <ol>
     <li><code>/etc/translation/supportedLanguages</code></li>
     <li><code>/apps/settings/translation/supportedLanguage</code></li>
     <li><code>/libs/settings/translation/supportedLanguages</code></li>
    </ol> <p>Esta resolución no admite una superposición combinada, lo que significa que la ruta resuelta debe contener todos los idiomas compatibles y no heredará los idiomas compatibles de resoluciones de orden superior.</p> </td>
  </tr>
 </tbody>
</table>

### Reglas de traducción {#translation-rules}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Se debe migrar un archivo XML de reglas de traducción modificado a la nueva ubicación (<code>/apps</code> o <code>/conf/global</code>).</p> <p>1. Copie el archivo XML de reglas de traducción modificado de la ubicación anterior a la nueva ubicación.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>La resolución XML de reglas de traducción de replicación se produce en el siguiente orden:</p>
    <ol>
     <li><code>/conf/global/settings/translation/rules/translation_rules.xml</code></li>
     <li><code class="code">/apps/settings/translation/rules/translation_rules.xml
        </code></li>
     <li><code class="code">/etc/workflow/models/translation/translation_rules.xml
        </code></li>
     <li><code>/libs/settings/translation/rules/translation_rules.xml</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Biblioteca de cliente del widget de traducción {#translation-widget-client-library}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/designs/translation/translationwidget</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/wcm/designs/translation/translationwidget</code></p> <p><code>/apps/settings/wcm/designs/translation/translationwidget</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en en tiempo de ejecución mediante cuadros de diálogo de diseño.</p>
    <ol>
     <li>Copie los diseños de la Ubicación anterior a la Nueva ubicación (/apps).</li>
     <li>Convierta cualquier recurso CSS, JavaScript y estático del diseño en una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">biblioteca de cliente</a> con <code>allowProxy = true</code>.</li>
     <li>Actualice las referencias a la Ubicación anterior en la
      <code>
       cq
      </code>:
      Propiedad <code>
       designPath
      </code>.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría Biblioteca de clientes (esto requiere la actualización del código de implementación de la página).</li>
     <li>Actualice las reglas de AEM Dispatcher para permitir el servicio de bibliotecas de cliente a través del servlet proxy /etc.clientlibs/...</li>
    </ol> <p>Para cualquier diseño que NO se haya administrado en SCM y que se haya modificado en tiempo de ejecución mediante cuadros de diálogo de diseño.</p>
    <ul>
     <li>No mueva los diseños que permiten crear de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Consola web de activación de árbol {#tree-activation-web-console}

| **Ubicación anterior** | `/etc/replication/treeactivation` |
|---|---|
| **Nueva(s) ubicación(es)** | `/libs/replication/treeactivation` |
| **Directrices de reestructuración** | No se requiere ninguna acción. |
| **Notas** | La consola web de activación de árbol ahora está disponible a través de **Herramientas > Implementación > Replicación > Activar árbol**. |

{style="table-layout:auto"}

### Cloud Services de conector de traducción del proveedor {#vendor-translation-connector-cloud-services}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/cloudservices/&lt;vendor&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> <p><code class="code">/apps/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code class="code">/conf/global/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier nuevo conector de traducción de proveedor de Cloud Services debe migrarse a la nueva ubicación (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Migre las configuraciones existentes en la ubicación anterior a la nueva ubicación.
      <ul>
       <li>Cree manualmente configuraciones de Cloud Services del conector de traducción de proveedor a través de la <strong>IU de creación de AEM en Herramientas &gt; Cloud Services &gt; Cloud Services de traducción</strong>.<br /> OR </li>
       <li>Copie cualquier nueva configuración de Cloud Services de Vendor Translation Connector de la ubicación anterior a la nueva ubicación (<code>/apps</code>, <code>/conf/global </code>o <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Asocie las configuraciones de AEM aplicables a las jerarquías de contenido de AEM.
      <ol>
       <li>Jerarquías de páginas de AEM Sites mediante <strong>AEM Sites &gt; Página &gt; Propiedades de página &gt; Pestaña Avanzadas &gt; Configuración de nube</strong>.</li>
       <li>Jerarquías de fragmentos de experiencias de AEM mediante <strong>Fragmentos de experiencias de AEM &gt; Fragmento de experiencias &gt; Propiedades &gt; Pestaña Servicios de nube &gt; Configuración de nube</strong>.</li>
       <li>Jerarquías de carpetas de fragmentos de experiencias de AEM a través de <strong>Fragmentos de experiencias de AEM &gt; Carpeta &gt; Propiedades &gt; Pestaña Servicios de nube &gt; Configuración de nube</strong>.</li>
       <li>AEM Assets las jerarquías de carpetas mediante <strong>AEM Assets &gt; Carpeta &gt; Propiedades de carpeta &gt; Pestaña Cloud Services &gt; Configuración</strong>.</li>
       <li>Proyectos AEM mediante <strong>Proyectos AEM &gt; Proyecto &gt; Propiedades del proyecto &gt; Pestaña Avanzadas &gt; Configuración de nube</strong>.</li>
      </ol> </li>
     <li>Desasocie los servicios de nube de traducción heredados migrados de las jerarquías de contenido de AEM mencionadas anteriormente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>La resolución de los servicios de nube de traducción se produce en el siguiente orden:</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Plantillas de correo electrónico de notificación de flujo de trabajo {#workflow-notification-email-templates}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/workflow/notification</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier plantilla de correo electrónico de notificación de flujo de trabajo modificada debe migrarse a la nueva ubicación (<code>/conf/global</code>).</p>
    <ol>
     <li>Copie cualquier plantilla de correo electrónico de notificación de flujo de trabajo modificada de la ubicación anterior a la nueva ubicación.</li>
     <li>Quitar las plantillas de correo electrónico de notificación de flujo de trabajo migradas de la ubicación anterior.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>La resolución de la plantilla de correo electrónico de notificación de flujo de trabajo se produce en el siguiente orden:</p>
    <ol>
     <li><code>/etc/workflow/notification</code></li>
     <li><code>/conf/global/settings/workflow/notification</code></li>
     <li><code>/libs/settings/workflow/notification</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Paquetes de flujo de trabajo {#workflow-packages}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><code>/var/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Los paquetes de flujo de trabajo existentes en la ubicación anterior deben migrarse a la nueva ubicación.</p>
    <ol>
     <li>Elimine cualquier paquete de flujo de trabajo de la ubicación anterior al que no haga referencia otro contenido y que, por lo demás, no sea necesario.</li>
     <li>Mueva cualquier paquete de flujo de trabajo en la ubicación anterior al que no haga referencia otro contenido pero que sea necesario en la nueva ubicación.</li>
     <li>Deje los paquetes de flujo de trabajo a los que haga referencia otro contenido en la ubicación anterior.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Los paquetes de flujo de trabajo creados mediante la consola Miscadmin de la IU clásica se mantienen en la ubicación anterior, mientras que todos los demás se mantienen en la nueva ubicación.</p> <p>Los paquetes de flujo de trabajo almacenados en las ubicaciones anteriores o bajas se pueden administrar mediante la consola Miscadmin de la IU clásica.</p> </td>
  </tr>
 </tbody>
</table>
