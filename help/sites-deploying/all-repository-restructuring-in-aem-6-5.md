---
title: Reestructuración común de repositorios en AEM 6.5
seo-title: Reestructuración común de repositorios en AEM 6.5
description: Aprenda a realizar los cambios necesarios para migrar a la nueva estructura de repositorio en AEM 6.5, que son comunes para todas las áreas de AEM.
seo-description: Aprenda a realizar los cambios necesarios para migrar a la nueva estructura de repositorio en AEM 6.5, que son comunes para todas las áreas de AEM.
uuid: a4bb64e5-387b-4084-9258-54e68db12f3b
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 80bd707f-c02d-4616-9b45-90f6c726abea
translation-type: tm+mt
source-git-commit: 6396660b642fd78ac7f311fa416efe0e0d52a9e3
workflow-type: tm+mt
source-wordcount: '2721'
ht-degree: 2%

---


# Reestructuración común del repositorio en AEM 6.5 {#common-repository-restructuring-in-aem}

Como se describe en la página principal [Reestructuración del repositorio en AEM 6.5](/help/sites-deploying/repository-restructuring.md), los clientes que actualicen a AEM 6.5 deben utilizar esta página para evaluar el esfuerzo de trabajo asociado con los cambios del repositorio que potencialmente impactan en todas las soluciones. Algunos cambios requieren esfuerzo de trabajo durante el proceso de actualización a AEM 6.5, mientras que otros se pueden posponer hasta una actualización futura.

**Con actualización a 6.5**

* [Configuración de ContextHub](#contexthub-6.5)
* [Instancias de flujo de trabajo](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [Modelos de flujo de trabajo](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [Lanzadores de flujo de trabajo](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [Secuencias de comandos de flujo de trabajo](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**Antes de la actualización futura**

* [Configuración de ContextHub](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [Diseños de Cloud Services clásicos](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [Diseños de Paneles clásicos](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [Diseños de informes clásicos](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [Diseños predeterminados](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [Extremo JavaScript de DTM de Adobe](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [Extremo de enlace web de la DTM de Adobe](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [Tareas de la bandeja de entrada](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [Configuraciones del modelo del administrador de varios sitios](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Configuraciones de gadget de Panel de AEM Projects](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [Plantilla de correo electrónico de notificación de replicación](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [Etiquetas](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [Cloud Services de traducción](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [Idiomas de traducción](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [Reglas de conversión](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [Biblioteca del cliente de utilidades de traducción](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [Consola web de Activación de árbol](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [Cloud Services del conector de traducción de proveedores](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [Plantillas de correo electrónico de notificación de flujo de trabajo](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## Con Actualización 6.5 {#with-upgrade}

### Configuración de ContextHub {#contexthub-6.5}

A partir de AEM 6.4, no hay ninguna configuración predeterminada de ContextHub. Por lo tanto, en el nivel raíz del sitio debe configurarse un `cq:contextHubPathproperty` para indicar qué configuración debe utilizarse.

1. Navegue hasta la raíz del sitio.
1. Abra las propiedades de página de la página raíz y seleccione la ficha Personalización.
1. En el campo Ruta de Contexthub, introduzca su propia ruta de configuración de ContextHub.

Además, en la configuración de ContextHub, el `sling:resourceType` debe actualizarse para que sea relativo y no absoluto.

1. Abra las propiedades del nodo de configuración de ContextHub en CRX DE Lite, por ejemplo: `/apps/settings/cloudsettings/legacy/contexthub`
1. Cambiar `sling:resourceType` de `/libs/granite/contexthub/cloudsettings/components/baseconfiguration` a `granite/contexthub/cloudsettings/components/baseconfiguration`

Es decir, el `sling:resourceType` de la configuración de ContextHub debe ser relativo en lugar de absoluto.

### Modelos de flujo de trabajo {#workflow-models}

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Cualquier modelo de flujo de trabajo nuevo o modificado debe migrarse a /conf/global/workflow/models.</p>
    <ol>
     <li>Implemente los modelos de flujo de trabajo modificados en una instancia de desarrollo AEM 6.4 local, de forma que existan en la ubicación Anterior.</li>
     <li>Edite el modelo de flujo de trabajo con AEM editor de modelos de flujo de trabajo en AEM &gt; Herramientas &gt; Flujo de trabajo &gt; Modelos.</li>
     <li>Al migrar modelos de flujo de trabajo modificados proporcionados por AEM
      <ol>
       <li>Con el Editor del modelo de flujo de trabajo abierto, modifique la dirección URL del navegador y sustituya el segmento de ruta /libs/settings/workflow/models por /etc/workflow/models.
        <ul>
         <li>Por ejemplo, cambie: <em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/models</strong>/dam/update_asset.html</em> a <em>http://localhost:4502/editor.html<strong>/etc/workflow/models</strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>Active el modo de edición en el Editor del modelo de flujo de trabajo, que copiará la definición del modelo de flujo de trabajo en /conf/global/workflow/models.</li>
     <li>Toque el botón Sincronizar para sincronizar los cambios en el modelo de flujo de trabajo en tiempo de ejecución en /var/workflow/models.</li>
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
    </ol> <p>Por lo tanto, cualquier personalización de los modelos de flujo de trabajo proporcionados por AEM que persista en la ubicación Anterior debe moverse a /conf/global/settings/workflow/models si se desea conservar; de lo contrario, se sustituirán por la definición del modelo de flujo de trabajo proporcionada por AEM en /libs/settings/workflow/models.</p> </td>
  </tr>
 </tbody>
</table>

### Instancias de flujo de trabajo {#workflow-instances}

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>No se requiere ninguna acción para alinear con la nueva ubicación.</p> <p>Las instancias de flujo de trabajo históricas pueden continuar residiendo de forma segura en la ubicación anterior y se crearán nuevas instancias de flujo de trabajo en la nueva ubicación.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Cualquier referencia de ruta explícita en
    El código <code>
     custom
    </code> de la Ubicación anterior también debe tener en cuenta la Nueva ubicación. Se recomienda refactorizar este código para utilizar las API de flujo de trabajo de AEM.</td>
  </tr>
 </tbody>
</table>

### Lanzadores de flujo de trabajo {#workflow-launchers}

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Cualquier iniciador de flujo de trabajo nuevo o modificado debe migrarse a <code>/conf/global/workflow/launcher/config</code>.</p>
    <ol>
     <li>Copie cualquier configuración del iniciador de flujo de trabajo nueva o modificada de la ubicación anterior a la nueva ubicación (<code>/conf/global</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>La resolución del iniciador del flujo de trabajo se produce en el siguiente orden:</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>Por lo tanto, cualquier personalización del iniciador de flujo de trabajo proporcionado por AEM que persista en la ubicación anterior debe moverse a la nueva ubicación (<code>/conf/global/settings/workflow/launcher</code>) si se desea conservar, de lo contrario, se reemplazará por la definición del iniciador de flujo de trabajo proporcionada por AEM en <code>/libs/settings/workflow/launcher</code>.</p> </td>
  </tr>
 </tbody>
</table>

### Secuencias de comandos de flujo de trabajo {#workflow-scripts}

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Los scripts de flujo de trabajo nuevos o modificados se deben migrar a la nueva ubicación y los modelos de flujo de trabajo de referencia se deben actualizar para reflejar la nueva ubicación.</p>
    <ol>
     <li>Copie los scripts de flujo de trabajo nuevos o modificados de la ubicación anterior a la nueva ubicación.<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> debe mantenerse en SCM.</li>
      </ul> </li>
     <li>Actualice las referencias a las secuencias de comandos de flujo de trabajo en la ubicación anterior de los modelos de flujo de trabajo para que apunten a las nuevas ubicaciones.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>AEM 6.4 SP1, cuando se libera, lo hace para que esta reestructuración pueda aplazarse hasta 6.5
     <code>
      upgrade
     </code>.</p> <p>Si la actualización a AEM 6.4 antes de la publicación de AEM 6.4 SP1, esta reestructuración debería realizarse como parte del proyecto de actualización. Sin ello, la edición y el guardado de los pasos del flujo de trabajo que hacen referencia a las secuencias de comandos en la ubicación anterior quitará por completo la referencia de secuencias de comandos del flujo de trabajo del paso del flujo de trabajo y solo estarán disponibles en la lista desplegable de selección de secuencias de comandos las secuencias de comandos de Nuevas ubicaciones.</p> </td>
  </tr>
 </tbody>
</table>

## Antes de la actualización futura {#prior-to-upgrade}

### Configuración de ContextHub {#contexthub-configurations}

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Todas las configuraciones de ContextHub nuevas o modificadas deben migrarse a la nueva ubicación y las páginas de AEM Sites de referencia deben actualizarse para reflejar la nueva ubicación.</p>
    <ol>
     <li>Copie las configuraciones de ContextHub nuevas o modificadas de la ubicación anterior a la nueva ubicación.</li>
     <li>Asocie las configuraciones de AEM aplicables con las jerarquías de contenido AEM.
      <ol>
       <li><strong>Jerarquías de páginas de AEM Sites mediante AEM Sites &gt; Página &gt; Propiedades de la página &gt; Ficha Avanzadas &gt; Configuración</strong> de la nube.</li>
      </ol> </li>
     <li>Desasocie las configuraciones de ContextHub heredadas migradas de las jerarquías de contenido de AEM antes mencionadas.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Diseños de Cloud Services clásicos {#classic-cloud-services-designs}

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en tiempo de ejecución mediante los diálogos de diseño.</p>
    <ol>
     <li>Copie los diseños de la ubicación anterior a la nueva ubicación (<code>/apps</code>).</li>
     <li>Convierta los recursos CSS, JavaScript y estáticos del diseño a una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">biblioteca de clientes</a> con <code>allowProxy = true</code>.</li>
     <li>Actualizar referencias a la ubicación anterior en el <span class="code">
       <code>
        cq
       </code>:
       <code>
        designPath
       </code></span>.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría de biblioteca de clientes (esto requiere actualizar el código de implementación de página).</li>
     <li>Actualice AEM reglas de Dispatcher para permitir el servicio de bibliotecas de cliente a través de /etc.clientlibs/. servlet proxy.</li>
    </ol> <p>Para cualquier diseño que NO se administre en SCM y se modifique en tiempo de ejecución mediante los diálogos de diseño.</p>
    <ul>
     <li>No mueva los diseños que pueden crear <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Diseños de Paneles clásicos {#classic-dashboards-designs}

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en tiempo de ejecución mediante los diálogos de diseño.</p>
    <ol>
     <li>Copie los diseños de la ubicación anterior a la nueva ubicación (/apps).</li>
     <li>Convierta los recursos CSS, JavaScript y estáticos del diseño a una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">biblioteca de clientes</a> con <code>allowProxy = true</code>.</li>
     <li>Actualizar referencias a la ubicación anterior en la
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría de biblioteca de clientes (esto requiere actualizar el código de implementación de página).</li>
     <li>Actualice AEM reglas de Dispatcher para permitir el servicio de bibliotecas de cliente a través de /etc.clientlibs/. servlet proxy.</li>
    </ol> <p>Para cualquier diseño que NO se administre en SCM y se modifique en tiempo de ejecución mediante los diálogos de diseño.</p>
    <ul>
     <li>No mueva los diseños que pueden crear <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Diseños de informes clásicos {#classic-reports-designs}

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en tiempo de ejecución mediante los diálogos de diseño.</p>
    <ol>
     <li>Copie los diseños de la ubicación anterior a la nueva ubicación (/apps).</li>
     <li>Convierta los recursos CSS, JavaScript y estáticos del diseño a una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">biblioteca de clientes</a> con <code>allowProxy = true</code>.</li>
     <li>Actualizar referencias a la ubicación anterior en la
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría de biblioteca de clientes (esto requiere actualizar el código de implementación de página).</li>
     <li>Actualice AEM reglas de Dispatcher para permitir el servicio de bibliotecas de cliente a través de /etc.clientlibs/. servlet proxy.</li>
    </ol> <p>Para cualquier diseño que NO se administre en SCM y se modifique en tiempo de ejecución mediante los diálogos de diseño.</p>
    <ul>
     <li>No mueva los diseños que pueden crear <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Diseños predeterminados {#default-designs}

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en tiempo de ejecución mediante los diálogos de diseño.</p>
    <ol>
     <li>Copie los diseños de la ubicación anterior a la nueva ubicación (/apps).</li>
     <li>Convierta los recursos CSS, JavaScript y estáticos del diseño a una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">biblioteca de clientes</a> con <code>allowProxy = true</code>.</li>
     <li>Actualizar referencias a la ubicación anterior en la
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría de biblioteca de clientes (esto requiere actualizar el código de implementación de página).</li>
     <li>Actualice AEM reglas de Dispatcher para permitir el servicio de bibliotecas de cliente a través de /etc.clientlibs/. servlet proxy.</li>
    </ol> <p>Para cualquier diseño que NO se administre en SCM y se modifique en tiempo de ejecución mediante los diálogos de diseño.</p>
    <ul>
     <li>No mueva los diseños que pueden crear <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Extremo JavaScript de DTM de Adobe {#adobe-dtm-javascript-endpoint}

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>No se requiere ninguna acción.</p> <p>La ubicación pública anterior actúa como punto final proxy para la nueva ubicación privada.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Extremo de enlace web de la DTM de Adobe {#adobe-dtm-web-hook-endpoint}

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>No se requiere ninguna acción.</p> <p>La ubicación pública anterior actúa como punto final proxy para la nueva ubicación privada.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Tareas de bandeja de entrada {#inbox-tasks}

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td>Utilice la <strong>Tarea de mantenimiento de depuración de la bandeja de entrada</strong> para quitar tareas antiguas de la ubicación anterior según sea necesario.</td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>No se requiere ninguna acción para migrar Tareas a la nueva ubicación.</p>
    <ul>
     <li>Las tareas presentes en la Ubicación anterior siguen estando disponibles y funcionando.</li>
     <li>Las nuevas Tareas se crean en la nueva ubicación.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Configuraciones del modelo de múltiples sitios {#multi-site-manager-blueprint-configurations}

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td>
    <ol>
     <li>Copie configuraciones personalizadas de <code>/etc/blueprints</code> a <code>/apps/msm</code>.</li>
     <li>Quitar <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Configuraciones de gadget de Panel de AEM Projects {#aem-projects-dashboard-gadget-configurations}

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Cualquier configuración de gadget de Panel de proyectos de AEM nueva o modificada debe migrarse a la nueva ubicación (<code>/apps</code>).</p>
    <ol>
     <li>Copie las configuraciones de gadget de Panel de proyectos de AEM nuevas o modificadas de la ubicación anterior a la nueva ubicación (<code>/apps</code>).
      <ol>
       <li>No copie las configuraciones de gadget de Panel de proyectos AEM sin modificar, ya que ahora existen en la nueva ubicación (<code>/libs</code>).</li>
      </ol> </li>
     <li>Actualice las plantillas de proyectos AEM que hagan referencia a la ubicación anterior para que apunten a la nueva ubicación adecuada.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Si se aplica el paquete de compatibilidad AEM 6.4, será necesario realizar las actividades de alineación del repositorio en el momento de la eliminación del paquete de compatibilidad.</td>
  </tr>
 </tbody>
</table>

### Plantilla de correo electrónico de notificación de replicación {#replication-notification-e-mail-template}

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Cualquier plantilla de correo electrónico de notificación de replicación nueva o modificada debe migrarse a la nueva ubicación (<code>/apps</code>)</p>
    <ol>
     <li>Copie las plantillas de correo electrónico de notificación de replicación nuevas o modificadas de la ubicación anterior a la nueva ubicación (<code>/apps</code>).</li>
     <li>Elimine las plantillas de correo electrónico de notificación de replicación migradas de la ubicación anterior.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Las únicas plantillas de correo electrónico de notificación de replicación admitidas son las nuevas configuraciones regionales.</p> <p>La resolución de la plantilla de correo electrónico de notificación de replicación se produce en el siguiente orden:</p>
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

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Todas las etiquetas deben migrarse a <code>/content/cq:tags</code>.</p>
    <ol>
     <li>Copie todas las etiquetas de la ubicación anterior en la nueva ubicación.</li>
     <li>Elimine todas las etiquetas de la ubicación anterior.</li>
     <li>A través de la consola web de AEM, reinicie el paquete OSGi de etiquetado de Day Community 5 en <em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em> para AEM reconocer que la nueva ubicación contiene contenido y debe utilizarse.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Si se reinicia el paquete OSGi de etiquetado de comunidad de día, solo se registrará la nueva ubicación como raíz de etiqueta si la ubicación anterior está vacía.</p> <p>Las referencias a la ubicación anterior seguirán funcionando después de migrar a Nueva ubicación para todas las funcionalidades que utilicen AEM API de TagManager para la resolución de etiquetas.</p> <p>Cualquier código personalizado que haga referencia explícita a la ruta <code>/etc/tags</code> debe actualizarse a <span class="code">/content/
      <code>
       cq
      </code>
      <code>
       :tags
      </code></span>, o preferiblemente reescrito para aprovechar la API de Java de TagManager, junto con esta migración.</p> </td>
  </tr>
 </tbody>
</table>

### Cloud Services de traducción {#translation-cloud-services}

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Cualquier nuevo Cloud Services de traducción debe migrarse a la nueva ubicación (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Migrar configuraciones existentes en la ubicación anterior a la nueva ubicación.
      <ul>
       <li>Vuelva a crear manualmente las nuevas configuraciones de Cloud Services de traducción mediante la IU de creación de AEM en <strong>Herramientas &gt; Cloud Services &gt; Cloud Services de traducción</strong>.<br /> O </li>
       <li>Copie cualquier configuración nueva de Cloud Services de traducción de la Ubicación anterior a la Nueva ubicación (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Asocie las configuraciones de AEM aplicables con las jerarquías de contenido AEM.
      <ol>
       <li>Jerarquías de páginas de AEM Sites mediante <strong>AEM Sites &gt; Página &gt; Propiedades de la página &gt; Ficha avanzada &gt; Configuración de nube</strong>.</li>
       <li>AEM jerarquías de fragmentos de experiencia mediante <strong>AEM fragmentos de experiencia &gt; Fragmento de experiencia &gt; Propiedades &gt; ficha Cloud Services &gt; Configuración de nube</strong>.</li>
       <li>Jerarquías de carpetas de fragmentos de experiencia de AEM mediante <strong>AEM fragmentos de experiencia &gt; Carpeta &gt; Propiedades &gt; ficha Cloud Services &gt; Configuración de nube</strong>.<br /> </li>
       <li>Jerarquías de carpetas de AEM Assets mediante <strong>AEM Assets &gt; Carpeta &gt; Propiedades de la carpeta &gt; Ficha Cloud Services &gt; Configuración</strong>.</li>
       <li>AEM proyectos mediante <strong>AEM proyectos &gt; Proyecto &gt; Propiedades del proyecto &gt; Ficha avanzada &gt; Configuración de la nube</strong>.</li>
      </ol> </li>
     <li>Desasocie los Cloud Services de traducción heredados migrados de las jerarquías de contenido de AEM antes mencionadas.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>La resolución de Cloud Services de traducción se produce en el siguiente orden:</p>
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

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
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
    </ol> <p>Esta resolución no admite una superposición de combinación, lo que significa que la ruta resuelta debe contener todos los idiomas admitidos y no heredará los idiomas admitidos de resoluciones de orden superior.</p> </td>
  </tr>
 </tbody>
</table>

### Reglas de conversión {#translation-rules}

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Un archivo XML de reglas de traducción modificado debe migrarse a la nueva ubicación (<code>/apps</code> o <code>/conf/global</code>).</p> <p>1. Copie el archivo XML modificado de reglas de traducción de la ubicación anterior a la nueva ubicación.</p> </td>
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

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en tiempo de ejecución mediante los diálogos de diseño.</p>
    <ol>
     <li>Copie los diseños de la ubicación anterior a la nueva ubicación (/apps).</li>
     <li>Convierta los recursos CSS, JavaScript y estáticos del diseño a una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">biblioteca de clientes</a> con <code>allowProxy = true</code>.</li>
     <li>Actualizar referencias a la ubicación anterior en la
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría de biblioteca de clientes (esto requiere actualizar el código de implementación de página).</li>
     <li>Actualice AEM reglas de Dispatcher para permitir el servicio de bibliotecas de cliente a través de /etc.clientlibs/. servlet proxy.</li>
    </ol> <p>Para cualquier diseño que NO se administre en SCM y se modifique en tiempo de ejecución mediante los diálogos de diseño.</p>
    <ul>
     <li>No mueva los diseños que pueden crear <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Consola Web de Activación de árbol {#tree-activation-web-console}

| **Ubicación anterior** | `/etc/replication/treeactivation` |
|---|---|
| **Nuevas ubicaciones** | `/libs/replication/treeactivation` |
| **Orientación de reestructuración** | No se requiere ninguna acción. |
| **Notas** | La consola web de Activación de árbol ahora está disponible mediante **Herramientas > Implementación > Replicación > Activar árbol**. |

### Cloud Services del conector de traducción del proveedor {#vendor-translation-connector-cloud-services}

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Todos los nuevos Cloud Services del conector de traducción de proveedores deben migrarse a la nueva ubicación (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Migrar configuraciones existentes en la ubicación anterior a la nueva ubicación.
      <ul>
       <li>Cree manualmente las nuevas configuraciones de Cloud Services del conector de traducción de proveedores mediante la <strong>IU de creación de AEM en Herramientas &gt; Cloud Services &gt; Cloud Services de traducción</strong>.<br /> O </li>
       <li>Copie cualquier configuración nueva de Cloud Services del conector de traducción de proveedores desde la ubicación anterior a la nueva ubicación (<code>/apps</code>, <code>/conf/global </code>o <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Asocie las configuraciones de AEM aplicables con las jerarquías de contenido AEM.
      <ol>
       <li>Jerarquías de páginas de AEM Sites mediante <strong>AEM Sites &gt; Página &gt; Propiedades de la página &gt; Ficha avanzada &gt; Configuración de nube</strong>.</li>
       <li>AEM jerarquías de fragmentos de experiencia mediante <strong>AEM fragmentos de experiencia &gt; Fragmento de experiencia &gt; Propiedades &gt; ficha Cloud Services &gt; Configuración de nube</strong>.</li>
       <li>AEM jerarquías de carpetas de fragmentos de experiencia mediante <strong>AEM fragmentos de experiencia &gt; Carpeta &gt; Propiedades &gt; ficha Cloud Services &gt; Configuración de nube</strong>.</li>
       <li>Jerarquías de carpetas de AEM Assets mediante <strong>AEM Assets &gt; Carpeta &gt; Propiedades de la carpeta &gt; Ficha Cloud Services &gt; Configuración</strong>.</li>
       <li>AEM proyectos mediante <strong>AEM proyectos &gt; Proyecto &gt; Propiedades del proyecto &gt; Ficha avanzada &gt; Configuración de la nube</strong>.</li>
      </ol> </li>
     <li>Desasocie los Cloud Services de traducción heredados migrados de las jerarquías de contenido de AEM antes mencionadas.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>La resolución de Cloud Services de traducción se produce en el siguiente orden:</p>
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

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Cualquier plantilla de correo electrónico de notificación de flujo de trabajo modificada debe migrarse a la nueva ubicación (<code>/conf/global</code>).</p>
    <ol>
     <li>Copie las plantillas de correo electrónico de notificación de flujo de trabajo modificadas de la ubicación anterior a la nueva ubicación.</li>
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

<table>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Los paquetes de flujo de trabajo existentes en la ubicación anterior deben migrarse a la nueva ubicación.</p>
    <ol>
     <li>Elimine los paquetes de flujo de trabajo de la ubicación anterior a los que no se hace referencia en otro contenido y que, de lo contrario, no son obligatorios.</li>
     <li>Mueva cualquier paquete de flujo de trabajo de la ubicación anterior al que no se haga referencia en otro contenido, pero que por lo demás sea necesario en la nueva ubicación.</li>
     <li>Deje los paquetes de flujo de trabajo a los que hace referencia otro contenido en la ubicación anterior.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Los paquetes de flujo de trabajo creados mediante la consola Miscadmin de la IU clásica se conservan en la ubicación anterior, mientras que los demás se mantienen en la nueva ubicación.</p> <p>Los paquetes de flujo de trabajo almacenados en las ubicaciones anteriores o secundarias se pueden administrar mediante la consola Miscadmin de la IU clásica.</p> </td>
  </tr>
 </tbody>
</table>

