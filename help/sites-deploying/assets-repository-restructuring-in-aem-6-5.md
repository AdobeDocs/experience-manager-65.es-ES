---
title: Reestructuración del repositorio de recursos en AEM 6.5
seo-title: Reestructuración del repositorio de recursos en AEM 6.5
description: Obtenga información sobre cómo realizar los cambios necesarios para migrar a la nueva estructura de repositorio en AEM 6.5 for Assets.
seo-description: Obtenga información sobre cómo realizar los cambios necesarios para migrar a la nueva estructura de repositorio en AEM 6.5 for Assets.
uuid: 0e3d8163-6274-4d1b-91c7-32ca927fb83c
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 212930fc-3430-4a0a-842c-2fb613ef981f
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# Reestructuración del repositorio de recursos en AEM 6.5 {#assets-repository-restructuring-in-aem}

Como se describe en la página principal Reestructuración [del repositorio en AEM 6.5](/help/sites-deploying/repository-restructuring.md) , los clientes que actualicen a AEM 6.5 deben utilizar esta página para evaluar el esfuerzo de trabajo asociado a los cambios del repositorio que afectan a la solución AEM Assets. Algunos cambios requieren esfuerzo durante el proceso de actualización de AEM 6.5, mientras que otros se pueden aplazar hasta una actualización futura.

**Con actualización a 6.5**

* [Misc](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**Antes de la actualización futura**

* [Plantilla de notificación por correo electrónico de evento de recurso/colección](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [Diseños de uso compartido de recursos clásicos](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [Descargar plantilla de notificación de correo electrónico de recursos](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [Ejemplos de licencias DRM](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [Plantilla de notificación de correo electrónico de uso compartido de vínculos](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [Secuencias de comandos de flujo de trabajo de InDesign](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [Configuraciones de transcodificación de vídeo](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
* [Misc](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc2)

## Con actualización a 6.5 {#with-upgrade}

### Misc {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td>/etc/dam/Jobs</td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td>/var/dam/Jobs</td>
  </tr>
  <tr>
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Si algún código personalizado depende de esta ubicación (por ejemplo: el código depende explícitamente de esta ruta), el código debe actualizarse para utilizar la nueva ubicación antes de la actualización; Idealmente, las API de Java se utilizan cuando están disponibles para reducir las dependencias en cualquier ruta específica del JCR.</p> <p>Ubicación temporal para guardar el archivo zip para que el cliente lo descargue. No hay necesidad de actualizar desde que el cliente solicita descargar el recurso. Generará un archivo en la nueva ubicación.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

## Antes de la actualización futura {#prior-to-upgrade}

### Plantilla de notificación por correo electrónico de evento de recurso/colección {#asset-collection-event-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/notification/email/default</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/dam/notification</code></p> <p><code>/apps/settings/dam/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Si el cliente modificó las plantillas de correo electrónico, realice las siguientes acciones para alinearse con la nueva estructura de repositorio:</p>
    <ol>
     <li>La plantilla de <code>/libs/settings/dam/notification</code> correo electrónico se debe copiar de <strong><code>/etc/notification/email/default</code></strong> a <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>Dado que el destino está en<strong> <code>/apps</code></strong> este cambio, debe persistir en SCM.</li>
      </ol> </li>
     <li>Elimine la carpeta: <strong><code>/etc/dam/notification/email/default</code></strong> después de que se hayan movido las plantillas de correo electrónico que contiene.<br />
      <ol>
       <li>Si no se han realizado actualizaciones en la plantilla de correo electrónico debajo<strong> de, la carpeta se puede quitar, ya que la plantilla de correo electrónico original existe <code>/etc/notification/email/default</code></strong><strong><code>/libs/settings/notification/email/default</code></strong> como parte de la instalación de AEM 4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Diseños de uso compartido de recursos clásicos {#classic-asset-share-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/designs/assetshare</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/wcm/designs/assetshare</code></p> <p><code>/apps/settings/wcm/designs/assetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Para los diseños que se administran en SCM y no se escriben en tiempo de ejecución mediante los cuadros de diálogo de diseño, realice las siguientes acciones para alinearse con el modelo más reciente:</p>
    <ol>
     <li>Copie los diseños de la ubicación anterior a la nueva ubicación debajo de <code>/apps</code>.</li>
     <li>Convierta cualquier recurso CSS, JavaScript y estático del diseño en una biblioteca <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">de</a> clientes con <code>allowProxy = true</code>.</li>
     <li>Actualice las referencias a la ubicación anterior en la <code>cq:designPath</code> propiedad mediante <strong>AEM &gt; Administración de DAM &gt; Página de uso compartido de recursos &gt; Propiedades de la página &gt; Ficha avanzada &gt; Campo</strong>de diseño.</li>
     <li>Actualice las páginas que hagan referencia a la ubicación anterior para utilizar la nueva categoría Biblioteca de clientes. Esto requiere actualizar el código de implementación de la página.</li>
     <li>Actualice las reglas de Dispatcher para permitir el servicio de bibliotecas de cliente mediante el servlet <code>/etc.clientlibs/</code> proxy.</li>
    </ol> <p>En el caso de los diseños que no se gestionan en SCM y que se modifican en tiempo de ejecución mediante los diálogos de diseño, no se eliminan los diseños con autorización de <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Descargar plantilla de notificación de correo electrónico de recursos {#download-asset-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/dam/workflownotification/email/downloadasset</code></p> <p><code>/apps/settings/dam/workflownotification/email/downloadasset</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Si se han modificado las plantillas de correo electrónico (<strong>downloadasset</strong> o <strong>transientworkflowComplete</strong>), siga el procedimiento siguiente para alinearse con la nueva estructura:</p>
    <ol>
     <li>La plantilla de correo electrónico actualizada debe copiarse de <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> a <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>Dado que el destino está en<strong> <code>/apps</code></strong> este cambio, debe persistir en SCM.</li>
      </ol> </li>
     <li>Elimine la carpeta: <code>/etc/dam/workflow/notification/email/downloadasset </code>después de mover las plantillas de correo electrónico que contiene.<br />
      <ol>
       <li>Si no se han realizado actualizaciones en la plantilla de correo electrónico debajo<strong> de, la carpeta se puede quitar, ya que la plantilla de correo electrónico original existe <code>/etc</code></strong><strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> como parte de la instalación de AEM 6.4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Aunque <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> es técnicamente compatible con la búsqueda (tiene prioridad antes de /apps a través de la búsqueda usual de CAConfig, pero después <code>/etc</code>) la plantilla podría colocarse en <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. Sin embargo, esto no se recomienda ya que no hay ninguna interfaz de usuario de tiempo de ejecución para facilitar la edición de la plantilla de correo electrónico.</td>
  </tr>
 </tbody>
</table>

### Ejemplos de licencias DRM {#example-drm-licenses}

| **Ubicación anterior** | `/etc/dam/drm/licenses/` |
|---|---|
| **Nuevas ubicaciones** | `/libs/settings/dam/drm` |
| **Orientación de reestructuración** | N/D |
| **Notas** | N/D |

### Plantilla de notificación de correo electrónico de uso compartido de vínculos {#link-share-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/dam/adhocassetshare</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/dam/adhocassetshare</code></p> <p><code>/apps/settings/dam/adhocassetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Si el cliente ha modificado la plantilla de correo electrónico, alinéela con la nueva estructura de repositorio:</p>
    <ol>
     <li>La plantilla de correo electrónico actualizada debe copiarse de <strong><code>/etc/dam/adhocassetshare</code></strong> a <strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>Dado que el destino está en<strong> <code>/apps</code></strong> este cambio, debe persistir en SCM.</li>
      </ol> </li>
     <li>Elimine la carpeta: <strong><code>/etc/dam/adhocassetshare</code></strong> después de que se hayan movido las plantillas de correo electrónico que contiene.<br />
      <ol>
       <li>Si no se han realizado actualizaciones en la plantilla de correo electrónico debajo<strong> de, la carpeta se puede quitar, ya que la plantilla de correo electrónico original existe <code>/etc</code></strong><strong><code>/libs/settings/dam/adhocassetshare</code></strong> como parte de la instalación de AEM 6.4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Aunque <code>/conf/global/settings/dam/adhocassetshare</code> se admite técnicamente para la búsqueda (tiene prioridad antes <code>/apps</code> de la búsqueda habitual de Sling CAConfig, pero después de <code>/etc</code>), la plantilla se puede colocar en <code>/conf/global/settings/dam/adhocassetshare</code>. Sin embargo, esto no se recomienda ya que no hay ninguna interfaz de usuario de tiempo de ejecución para facilitar la edición de la plantilla de correo electrónico</td>
  </tr>
 </tbody>
</table>

### Secuencias de comandos de flujo de trabajo de InDesign {#indesign-workflow-scripts}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/dam/indesign/scripts</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/dam/indesign</code></p> <p><code>/apps/settings/dam/indesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Para alinearse con la nueva estructura de repositorio:</p>
    <ol>
     <li>Copiar todas las secuencias de comandos personalizadas o modificadas de <strong><code>/etc/dam/indesign/scripts</code></strong> a <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>En AEM 6.5 solo se podrán copiar scripts nuevos o modificados como scripts no modificados proporcionados por AEM a través <strong><code>/libs/settings</code></strong> de AEM 6.5</li>
      </ol> </li>
     <li>Localice todos los modelos de flujo de trabajo que utilizan el paso WF del proceso de extracción de medios y
      <ol>
       <li>Para cada instancia del paso de flujo de trabajo, actualice las rutas de la configuración para que señalen explícitamente las secuencias de comandos correctas en o debajo<strong> de las <code>/apps/settings/dam/indesign/scripts</code></strong> o <strong><code>/libs/settings/dam/indesign/scripts</code></strong> según corresponda.</li>
      </ol> </li>
     <li>Desmonte<strong> por completo <code>/etc/dam/indesign/scripts</code></strong> .</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Se recomienda almacenar secuencias de comandos personalizadas en <code>/apps</code>, ya que es la ubicación donde se debe almacenar el código.</td>
  </tr>
 </tbody>
</table>

### Configuraciones de transcodificación de vídeo {#video-transcoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/dam/video</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/dam/video</code></p> <p><code>/apps/settings/dam/video</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Las personalizaciones de nivel de proyecto deben cortarse y pegarse en rutas equivalentes <code>/apps</code> o <code>/conf</code> según corresponda.</p> <p>Para alinearse con la estructura de repositorio de AEM 6.4:</p>
    <ol>
     <li>Copiar las configuraciones de vídeo modificadas de <code>/etc/dam/video</code> a <code>/apps/settings/dam/video</code></li>
     <li>Quitar <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Configuraciones de ajustes preestablecidos de visor {#viewer-preset-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/dam/presets/viewer</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Para el ajuste preestablecido de visor predeterminado, solo estará disponible en la nueva ubicación.</p> <p>Para el ajuste preestablecido de visor personalizado:</p>
    <ul>
     <li>tendrá que ejecutar una secuencia de comandos de migración para mover el nodo de <code>/etc</code> a <code>/conf</code>. La secuencia de comandos se encuentra en <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>o puede editar la configuración y se guardarán automáticamente en la nueva ubicación.</li>
    </ul> <p>Tenga en cuenta que no es necesario ajustar el código copyURL/embed para que apunte <code>/conf</code>. La solicitud existente de <code>/etc</code> se redirigirá al contenido correcto desde <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Misc {#misc2}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/libs/dam/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Ajuste las referencias para que apunten a los nuevos recursos en <code>/libs</code> Uso del prefijo <code>/etc.clientlibs/</code> de proxy de permiso.</p> <p>Por último, limpie quitando las carpetas de los clientes migrados <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

