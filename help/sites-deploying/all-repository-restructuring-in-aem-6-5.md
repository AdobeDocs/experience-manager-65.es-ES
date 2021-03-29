---
title: Reestructuración común de repositorios en AEM 6.5
seo-title: Reestructuración común de repositorios en AEM 6.5
description: Aprenda a realizar los cambios necesarios para migrar a la nueva estructura de repositorios en AEM 6.5 que son comunes para todas las áreas de AEM.
seo-description: Aprenda a realizar los cambios necesarios para migrar a la nueva estructura de repositorios en AEM 6.5 que son comunes para todas las áreas de AEM.
uuid: a4bb64e5-387b-4084-9258-54e68db12f3b
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 80bd707f-c02d-4616-9b45-90f6c726abea
translation-type: tm+mt
source-git-commit: 8d6818d0f2d90482f930f8e98682670ed6d0dd28
workflow-type: tm+mt
source-wordcount: '2724'
ht-degree: 2%

---


# Reestructuración común de repositorios en AEM 6.5 {#common-repository-restructuring-in-aem}

Como se describe en la página principal [Reestructuración del repositorio en AEM 6.5](/help/sites-deploying/repository-restructuring.md), los clientes que actualicen a AEM 6.5 deben utilizar esta página para evaluar el esfuerzo de trabajo asociado con los cambios del repositorio que puedan afectar a todas las soluciones. Algunos cambios requieren un esfuerzo de trabajo durante el proceso de actualización de AEM 6.5, mientras que otros se pueden aplazar hasta una actualización futura.

**Con actualización a la versión 6.5**

* [Configuración de ContextHub](#contexthub-6.5)
* [Instancias de flujo de trabajo](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [Modelos de flujo de trabajo](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [Lanzadores de flujo de trabajo](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [Scripts de flujo de trabajo](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**Antes de una actualización futura**

* [Configuración de ContextHub](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [Diseños de Cloud Services clásicos](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [Diseños de tableros clásicos](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [Diseños de informes clásicos](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [Diseños predeterminados](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [Punto final de JavaScript de DTM de Adobe](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [Punto final de enlace web de la DTM de Adobe](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [Tareas de la bandeja de entrada](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [Configuraciones del modelo de Multi-Site Manager](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Configuraciones de Gadget del panel AEM Proyectos](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [Plantilla de correo electrónico de notificación de replicación](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [Etiquetas](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [Cloud Services de traducción](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [Idiomas de traducción](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [Reglas de traducción](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [Biblioteca de cliente de utilidades de traducción](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [Consola Web de activación de árbol](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [Cloud Services del conector de traducción del proveedor](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [Plantillas de correo electrónico de notificación de flujo de trabajo](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## Con actualización de 6.5 {#with-upgrade}

### Configuración de ContextHub {#contexthub-6.5}

A partir de AEM 6.4, no hay ninguna configuración predeterminada de ContextHub. Por lo tanto, en el nivel raíz del sitio debe configurarse un `cq:contextHubPathproperty` para indicar qué configuración debe utilizarse.

1. Vaya a la raíz del sitio.
1. Abra las propiedades de página de la página raíz y seleccione la pestaña Personalization .
1. En el campo Ruta de Contexthub introduzca su propia ruta de configuración de ContextHub.

Además, en la configuración de ContextHub, el `sling:resourceType` debe actualizarse para que sea relativo y no absoluto.

1. Abra las propiedades del nodo de configuración de ContextHub en CRX DE Lite, por ejemplo `/apps/settings/cloudsettings/legacy/contexthub`
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
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> <p><code>/var/workflow/models</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Los modelos de flujo de trabajo nuevos o modificados deben migrarse a /conf/global/workflow/models.</p>
    <ol>
     <li>Implemente los modelos de flujo de trabajo modificados en una instancia de desarrollo local AEM 6.5, de forma que existan en la ubicación Anterior.</li>
     <li>Edite el modelo de flujo de trabajo mediante AEM Editor de modelos de flujo de trabajo en AEM &gt; Herramientas &gt; Flujo de trabajo &gt; Modelos.</li>
     <li>Al migrar modelos de flujo de trabajo modificados proporcionados por AEM
      <ol>
       <li>Con el Editor de modelos de flujo de trabajo abierto, modifique la dirección URL del navegador y reemplace el segmento de ruta /libs/settings/workflow/models por /etc/workflow/models.
        <ul>
         <li>Por ejemplo, cambie: <em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/models</strong>/dam/update_asset.html</em> a <em>http://localhost:4502/editor.html<strong>/etc/workflow/models</strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>Habilite el modo de edición en el Editor de modelos de flujo de trabajo que copiará la definición del modelo de flujo de trabajo en /conf/global/workflow/models.</li>
     <li>Pulse el botón Sincronizar para sincronizar los cambios en el Modelo de flujo de trabajo en tiempo de ejecución en /var/workflow/models.</li>
     <li>Exporte el modelo de flujo de trabajo (/conf/global/workflow/models/&lt;workflow-model&gt;) y el modelo de flujo de trabajo en tiempo de ejecución (/var/workflow/models/&lt;workflow-model&gt;) e integre el proyecto AEM.
      <ol>
       <li>Por ejemplo, exportar:
        <ul>
         <li><code>/config/settings/workflow/models/dam/my_workflow_model</code> y </li>
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
    </ol> <p>Por lo tanto, cualquier personalización de los modelos de flujo de trabajo proporcionados por AEM persistió en la ubicación Anterior debe moverse a /conf/global/settings/workflow/models si se van a conservar; de lo contrario, se sustituirán por la definición del modelo de flujo de trabajo proporcionada por el AEM en /libs/settings/workflow/models.</p> </td>
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
   <td><strong>Nuevas ubicaciones</strong></td>
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
    </code> de la ubicación anterior también debe tener en cuenta la ubicación nueva. Se recomienda refactorizar este código para utilizar las API de flujo de trabajo AEM.</td>
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
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/workflow/launcher/config</code></p> <p><code>/conf/global/settings/workflow/launcher/config</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Los iniciadores de flujo de trabajo nuevos o modificados deben migrarse a <code>/conf/global/workflow/launcher/config</code>.</p>
    <ol>
     <li>Copie cualquier configuración de Workflow Launcher nueva o modificada de la Ubicación anterior a Nueva ubicación (<code>/conf/global</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>La resolución del iniciador del flujo de trabajo se produce en el siguiente orden:</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>Por lo tanto, cualquier personalización de Workflow Launcher proporcionado por AEM que persiste en la ubicación Anterior debe moverse a la Nueva ubicación (<code>/conf/global/settings/workflow/launcher</code>) si se van a conservar, de lo contrario se reemplazará por la definición de Workflow Launcher proporcionada por AEM en <code>/libs/settings/workflow/launcher</code>.</p> </td>
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
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Los scripts de flujo de trabajo nuevos o modificados deben migrarse a la ubicación nueva y los modelos de flujo de trabajo de referencia deben actualizarse para reflejar la ubicación nueva.</p>
    <ol>
     <li>Copie cualquier script de flujo de trabajo nuevo o modificado de la ubicación anterior a la nueva ubicación.<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> debe mantenerse en SCM.</li>
      </ul> </li>
     <li>Actualice cualquier referencia a las secuencias de comandos de flujo de trabajo en la ubicación anterior en los modelos de flujo de trabajo para que apunten a las nuevas ubicaciones.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>AEM 6.4 SP1, cuando se libera, lo hace para que esta reestructuración pueda aplazarse hasta 6.5
     <code>
      upgrade
     </code>.</p> <p>Si se actualiza a AEM 6.4 antes de que se libere AEM 6.4 SP1, esta reestructuración debe realizarse como parte del proyecto de actualización. Sin ello, al editar y guardar los Pasos del flujo de trabajo que hacen referencia a las secuencias de comandos en la ubicación anterior, se eliminará por completo la referencia del script de flujo de trabajo del paso del flujo de trabajo y solo estarán disponibles los scripts de flujo de trabajo en nuevas ubicaciones en la lista desplegable de selección de secuencias de comandos.</p> </td>
  </tr>
 </tbody>
</table>

## Antes de la actualización futura {#prior-to-upgrade}

### Configuración de ContextHub {#contexthub-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/cloudsettings</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/global/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Las configuraciones de ContextHub nuevas o modificadas deben migrarse a la nueva ubicación y las páginas de AEM Sites de referencia deben actualizarse para reflejar la nueva ubicación.</p>
    <ol>
     <li>Copie cualquier configuración de ContextHub nueva o modificada de la ubicación anterior a la nueva ubicación.</li>
     <li>Asocie las configuraciones de AEM aplicables con las jerarquías de contenido de AEM.
      <ol>
       <li><strong>Jerarquías de página de AEM Sites mediante AEM Sites &gt; Página &gt; Propiedades de página &gt; Pestaña avanzada &gt; Configuración de nube</strong>.</li>
      </ol> </li>
     <li>Desasocie cualquier configuración heredada de ContextHub migrada de las jerarquías de contenido AEM anteriormente mencionadas.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Diseños de Cloud Services clásicos {#classic-cloud-services-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/designs/cloudservices</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/wcm/designs/cloudservices</code></p> <p><code>/apps/settings/wcm/designs/cloudservices</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en tiempo de ejecución mediante los cuadros de diálogo de diseño.</p>
    <ol>
     <li>Copie los diseños de la ubicación anterior a la nueva ubicación (<code>/apps</code>).</li>
     <li>Convierta cualquier recurso CSS, JavaScript y estático en el diseño a una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">biblioteca de cliente</a> con <code>allowProxy = true</code>.</li>
     <li>Actualizar referencias a la ubicación anterior en el <span class="code">
       <code>
        cq
       </code>:
       <code>
        designPath
       </code></span>.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría Biblioteca de cliente (esto requiere actualizar el código de implementación de página).</li>
     <li>Actualice AEM reglas de Dispatcher para permitir el servicio de bibliotecas de cliente a través de /etc.clientlibs/.. proxy servlet.</li>
    </ol> <p>Para cualquier diseño que NO se administre en SCM y que se modifique en tiempo de ejecución mediante los cuadros de diálogo de diseño.</p>
    <ul>
     <li>No mueva los diseños de autor fuera de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Diseños de tableros clásicos {#classic-dashboards-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/designs/dashboards</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/wcm/designs/dashboards</code></p> <p><code>/apps/settings/wcm/designs/dashboards</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en tiempo de ejecución mediante los cuadros de diálogo de diseño.</p>
    <ol>
     <li>Copie los diseños de la ubicación anterior a la nueva ubicación (/apps).</li>
     <li>Convierta cualquier recurso CSS, JavaScript y estático en el diseño a una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">biblioteca de cliente</a> con <code>allowProxy = true</code>.</li>
     <li>Actualizar referencias a la ubicación anterior en la
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría Biblioteca de cliente (esto requiere actualizar el código de implementación de página).</li>
     <li>Actualice AEM reglas de Dispatcher para permitir el servicio de bibliotecas de cliente a través de /etc.clientlibs/.. proxy servlet.</li>
    </ol> <p>Para cualquier diseño que NO se administre en SCM y que se modifique en tiempo de ejecución mediante los cuadros de diálogo de diseño.</p>
    <ul>
     <li>No mueva los diseños de autor fuera de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Diseños de informes clásicos {#classic-reports-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/designs/reports</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/wcm/designs/reports</code></p> <p><code>/apps/settings/wcm/designs/reports</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en tiempo de ejecución mediante los cuadros de diálogo de diseño.</p>
    <ol>
     <li>Copie los diseños de la ubicación anterior a la nueva ubicación (/apps).</li>
     <li>Convierta cualquier recurso CSS, JavaScript y estático en el diseño a una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">biblioteca de cliente</a> con <code>allowProxy = true</code>.</li>
     <li>Actualizar referencias a la ubicación anterior en la
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría Biblioteca de cliente (esto requiere actualizar el código de implementación de página).</li>
     <li>Actualice AEM reglas de Dispatcher para permitir el servicio de bibliotecas de cliente a través de /etc.clientlibs/.. proxy servlet.</li>
    </ol> <p>Para cualquier diseño que NO se administre en SCM y que se modifique en tiempo de ejecución mediante los cuadros de diálogo de diseño.</p>
    <ul>
     <li>No mueva los diseños de autor fuera de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
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
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/wcm/designs/default</code></p> <p><code>/apps/settings/wcm/designs/default</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en tiempo de ejecución mediante los cuadros de diálogo de diseño.</p>
    <ol>
     <li>Copie los diseños de la ubicación anterior a la nueva ubicación (/apps).</li>
     <li>Convierta cualquier recurso CSS, JavaScript y estático en el diseño a una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">biblioteca de cliente</a> con <code>allowProxy = true</code>.</li>
     <li>Actualizar referencias a la ubicación anterior en la
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría Biblioteca de cliente (esto requiere actualizar el código de implementación de página).</li>
     <li>Actualice AEM reglas de Dispatcher para permitir el servicio de bibliotecas de cliente a través de /etc.clientlibs/.. proxy servlet.</li>
    </ol> <p>Para cualquier diseño que NO se administre en SCM y que se modifique en tiempo de ejecución mediante los cuadros de diálogo de diseño.</p>
    <ul>
     <li>No mueva los diseños de autor fuera de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Punto final de JavaScript de DTM de Adobe {#adobe-dtm-javascript-endpoint}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/clientlibs/dtm</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/var/cq/dtm/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>No se requiere ninguna acción.</p> <p>La ubicación pública anterior actúa como punto final de proxy para la nueva ubicación privada.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Punto final de enlace web de la DTM de Adobe {#adobe-dtm-web-hook-endpoint}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/dtm-hook</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>No se requiere ninguna acción.</p> <p>La ubicación pública anterior actúa como punto final de proxy para la nueva ubicación privada.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Tareas de la bandeja de entrada {#inbox-tasks}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/var/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td>Utilice la <strong>Tarea de mantenimiento de purga de la bandeja de entrada</strong> para eliminar las tareas antiguas de la ubicación anterior según sea necesario.</td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>No es necesario realizar ninguna acción para migrar tareas a la nueva ubicación.</p>
    <ul>
     <li>Las tareas presentes en Ubicación anterior siguen estando disponibles y funcionando.</li>
     <li>Las tareas nuevas se crean en la ubicación nueva.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Configuraciones del modelo del administrador de varios sitios {#multi-site-manager-blueprint-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong><em></em>Ubicación anterior</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/msm</code></p> <p><code>/apps/msm</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td>
    <ol>
     <li>Copie las configuraciones personalizadas de <code>/etc/blueprints</code> a <code>/apps/msm</code>.</li>
     <li>Quitar <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Configuraciones de Gadget del panel de AEM de proyectos {#aem-projects-dashboard-gadget-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/projects/dashboard/gadgets</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/cq/core/content/projects/dashboard/gadgets</code></p> <p><code>/apps/cq/core/content/projects/dashboard/gadgets</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Las configuraciones de Gadget del panel de proyectos de AEM nuevas o modificadas deben migrarse a la nueva ubicación (<code>/apps</code>).</p>
    <ol>
     <li>Copie cualquier configuración de Gadget del panel de AEM de proyectos nueva o modificada de la ubicación anterior a la nueva ubicación (<code>/apps</code>).
      <ol>
       <li>No copie las configuraciones de Gadget del panel de proyectos AEM sin modificar, ya que ahora existen en la nueva ubicación (<code>/libs</code>).</li>
      </ol> </li>
     <li>Actualice las plantillas de Proyectos AEM que hagan referencia a la Ubicación anterior para que apunten a la nueva ubicación adecuada.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Si se aplica el paquete de compatibilidad AEM 6.4, será necesario realizar las actividades de alineación del repositorio en el momento de la eliminación del paquete de compatibilidad.</td>
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
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.replication</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.replication</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Las plantillas de correo electrónico de notificación de replicación nuevas o modificadas deben migrarse a la nueva ubicación (<code>/apps</code>)</p>
    <ol>
     <li>Copie cualquier plantilla de correo electrónico de notificación de replicación nueva o modificada de la ubicación anterior a la nueva ubicación (<code>/apps</code>).</li>
     <li>Elimine las plantillas de correo electrónico de notificación de replicación migradas de la ubicación anterior.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Las únicas plantillas de correo electrónico de notificación de replicación compatibles son las nuevas configuraciones regionales.</p> <p>La resolución de la plantilla de correo electrónico de notificación de replicación se produce en el siguiente orden:</p>
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
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/content/cq:tags</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Todas las etiquetas deben migrarse a <code>/content/cq:tags</code>.</p>
    <ol>
     <li>Copie todas las etiquetas de la ubicación anterior a la nueva ubicación.</li>
     <li>Elimine todas las etiquetas de la ubicación anterior.</li>
     <li>A través de la Consola Web AEM, reinicie el paquete OSGi Day Communique 5 Tagging en <em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em> para que AEM que reconoce la Nueva ubicación contiene contenido y debe usarse.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Al reiniciar el paquete OSGi Day Communique Tagging solo se registrará la Nueva ubicación como la raíz de la etiqueta si la Ubicación anterior está vacía.</p> <p>Las referencias a la ubicación anterior seguirán funcionando después de migrar a Nueva ubicación para todas las funciones que aprovechen AEM API de TagManager para la resolución de etiquetas.</p> <p>Cualquier código personalizado que haga referencia explícita a la ruta <code>/etc/tags</code> debe actualizarse a <span class="code">/content/
      <code>
       cq
      </code>
      <code>
       :tags
      </code></span>, o preferiblemente reescrito para aprovechar la API Java de TagManager, junto con esta migración.</p> </td>
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
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/apps/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/global/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Los Cloud Services de traducción nuevos deben migrarse a la nueva ubicación (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Migre las configuraciones existentes en la ubicación anterior a la nueva ubicación.
      <ul>
       <li>Vuelva a crear manualmente las nuevas configuraciones de Cloud Services de traducción mediante la IU de creación de AEM en <strong>Herramientas &gt; Cloud Services &gt; Cloud Services de traducción</strong>.<br /> O </li>
       <li>Copie cualquier configuración nueva de Cloud Services de traducción de la Ubicación anterior a la Nueva ubicación (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Asocie las configuraciones de AEM aplicables con las jerarquías de contenido de AEM.
      <ol>
       <li>Jerarquías de página de AEM Sites mediante <strong>AEM Sites &gt; Página &gt; Propiedades de página &gt; Pestaña avanzada &gt; Configuración de nube</strong>.</li>
       <li>AEM las jerarquías de fragmentos de experiencia a través de <strong>AEM Fragmentos de experiencia &gt; Fragmento de experiencia &gt; Propiedades &gt; Pestaña Cloud Services &gt; Configuración de nube</strong>.</li>
       <li>AEM jerarquías de carpetas de fragmentos de experiencias a través de <strong>AEM Fragmentos de experiencias &gt; Carpeta &gt; Propiedades &gt; Pestaña Cloud Services &gt; Configuración de nube</strong>.<br /> </li>
       <li>Las jerarquías de carpetas de AEM Assets a través de <strong>AEM Assets &gt; Folder &gt; Folder Properties &gt; Cloud Services Tab &gt; Configuration</strong>.</li>
       <li>AEM Proyectos a través de <strong>AEM Proyectos &gt; Proyecto &gt; Propiedades del proyecto &gt; Pestaña Avanzadas &gt; Configuración de la nube</strong>.</li>
      </ol> </li>
     <li>Desasocie los Cloud Services de traducción heredados migrados de las jerarquías de contenido AEM anteriormente mencionadas.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>La resolución de los Cloud Services de traducción se produce en el siguiente orden:</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/translationcfg</code></li>
    </ol> <p>Los Cloud Services de traducción migrados deben ser compatibles con AEM 6.4.</p> </td>
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
   <td><strong>Nuevas ubicaciones</strong></td>
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
    </ol> <p>Esta resolución no admite una superposición combinada, lo que significa que la ruta resuelta debe contener todos los idiomas compatibles y no heredará los idiomas admitidos de resoluciones de orden superior.</p> </td>
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
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Se debe migrar un archivo XML de reglas de traducción modificado a la nueva ubicación (<code>/apps</code> o <code>/conf/global</code>).</p> <p>1. Copie el archivo XML de reglas de traducción modificado de la ubicación anterior a la nueva ubicación.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>La resolución XML de las reglas de traducción de replicación se produce en el siguiente orden:</p>
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

### Biblioteca de cliente de utilidades de traducción {#translation-widget-client-library}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/designs/translation/translationwidget</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/wcm/designs/translation/translationwidget</code></p> <p><code>/apps/settings/wcm/designs/translation/translationwidget</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en tiempo de ejecución mediante los cuadros de diálogo de diseño.</p>
    <ol>
     <li>Copie los diseños de la ubicación anterior a la nueva ubicación (/apps).</li>
     <li>Convierta cualquier recurso CSS, JavaScript y estático en el diseño a una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">biblioteca de cliente</a> con <code>allowProxy = true</code>.</li>
     <li>Actualizar referencias a la ubicación anterior en la
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría Biblioteca de cliente (esto requiere actualizar el código de implementación de página).</li>
     <li>Actualice AEM reglas de Dispatcher para permitir el servicio de bibliotecas de cliente a través de /etc.clientlibs/.. proxy servlet.</li>
    </ol> <p>Para cualquier diseño que NO se administre en SCM y que se modifique en tiempo de ejecución mediante los cuadros de diálogo de diseño.</p>
    <ul>
     <li>No mueva los diseños de autor fuera de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Consola Web de activación de árbol {#tree-activation-web-console}

| **Ubicación anterior** | `/etc/replication/treeactivation` |
|---|---|
| **Nuevas ubicaciones** | `/libs/replication/treeactivation` |
| **Directrices de reestructuración** | No se requiere ninguna acción. |
| **Notas** | La consola web de Activación de árbol ahora está disponible a través de **Tools > Deployment > Replication > Activate Tree**. |

{style=&quot;table-layout:auto&quot;}

### Cloud Services del conector de traducción del proveedor {#vendor-translation-connector-cloud-services}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/cloudservices/&lt;vendor&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> <p><code class="code">/apps/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code class="code">/conf/global/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Los nuevos Cloud Services de conector de traducción del proveedor deben migrarse a la nueva ubicación (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Migrar las configuraciones existentes en la ubicación anterior a la nueva ubicación.
      <ul>
       <li>Cree manualmente las nuevas configuraciones de Cloud Services del conector de traducción del proveedor a través de la <strong>AEM interfaz de usuario de creación en Herramientas &gt; Cloud Services &gt; Cloud Services de traducción</strong>.<br /> O </li>
       <li>Copie cualquier configuración nueva de Cloud Services de conector de traducción de proveedores de la ubicación anterior a la nueva ubicación (<code>/apps</code>, <code>/conf/global </code>o <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Asocie las configuraciones de AEM aplicables con las jerarquías de contenido de AEM.
      <ol>
       <li>Jerarquías de página de AEM Sites mediante <strong>AEM Sites &gt; Página &gt; Propiedades de página &gt; Pestaña avanzada &gt; Configuración de nube</strong>.</li>
       <li>AEM las jerarquías de fragmentos de experiencia a través de <strong>AEM Fragmentos de experiencia &gt; Fragmento de experiencia &gt; Propiedades &gt; Pestaña Cloud Services &gt; Configuración de nube</strong>.</li>
       <li>AEM las jerarquías de carpetas de fragmentos de experiencias a través de <strong>AEM Fragmentos de experiencias &gt; Carpeta &gt; Propiedades &gt; Pestaña Cloud Services &gt; Configuración de nube</strong>.</li>
       <li>Las jerarquías de carpetas de AEM Assets a través de <strong>AEM Assets &gt; Folder &gt; Folder Properties &gt; Cloud Services Tab &gt; Configuration</strong>.</li>
       <li>AEM Proyectos a través de <strong>AEM Proyectos &gt; Proyecto &gt; Propiedades del proyecto &gt; Pestaña Avanzadas &gt; Configuración de la nube</strong>.</li>
      </ol> </li>
     <li>Desasocie los Cloud Services de traducción heredados migrados de las jerarquías de contenido AEM anteriormente mencionadas.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>La resolución de los Cloud Services de traducción se produce en el siguiente orden:</p>
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
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Las plantillas de correo electrónico de notificación de flujo de trabajo modificadas deben migrarse a la nueva ubicación (<code>/conf/global</code>).</p>
    <ol>
     <li>Copie cualquier plantilla de correo electrónico de notificación de flujo de trabajo modificada de la ubicación anterior a la nueva ubicación.</li>
     <li>Elimine las plantillas de correo electrónico de notificación de flujo de trabajo migradas de la ubicación anterior.</li>
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
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/var/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Los paquetes de flujo de trabajo existentes en la ubicación anterior deben migrarse a la nueva ubicación.</p>
    <ol>
     <li>Elimine cualquier paquete de flujo de trabajo de la ubicación anterior al que no se haga referencia en otro contenido y que, por lo demás, no sea necesario.</li>
     <li>Mueva cualquier paquete de flujo de trabajo de la ubicación anterior al que no se haga referencia en otro contenido pero que por lo demás sea necesario en la nueva ubicación.</li>
     <li>Deje cualquier paquete de flujo de trabajo al que se haga referencia con otro contenido en la ubicación anterior.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Los paquetes de flujo de trabajo creados mediante la consola Miscadmin de la IU clásica se mantienen en la ubicación anterior, mientras que el resto se mantienen en la nueva ubicación.</p> <p>Los paquetes de flujo de trabajo almacenados en las ubicaciones anteriores o inferiores se pueden administrar mediante la consola Miscadmin de la IU clásica.</p> </td>
  </tr>
 </tbody>
</table>

