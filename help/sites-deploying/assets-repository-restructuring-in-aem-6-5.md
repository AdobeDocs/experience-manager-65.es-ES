---
title: Reestructuración de repositorios de Assets AEM en 6.5
description: Obtenga información sobre cómo realizar los cambios necesarios para migrar a la nueva estructura de repositorios en Adobe Experience Manager AEM () 6.5 para Assets.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 28ddd23c-5907-4356-af56-ebc7589a2b5d
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 2%

---

# Reestructuración de repositorios de Assets AEM en 6.5 {#assets-repository-restructuring-in-aem}

AEM Como se describe en la página principal [Reestructuración del repositorio en la página de 6.5](/help/sites-deploying/repository-restructuring.md), los clientes que actualicen a Adobe Experience Manager AEM () 6.5 deben utilizar esta página para evaluar el esfuerzo de trabajo asociado con los cambios del repositorio que afectan a la solución AEM Assets. AEM Algunos cambios requieren un esfuerzo durante el proceso de actualización de la versión 6.5 de la, mientras que otros se pueden aplazar hasta una actualización futura.

**Con Actualización 6.5**

* [Varios](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**Antes de una actualización futura**

* [Plantilla de notificación de correo electrónico de evento de colección/recurso](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [Diseños clásicos de uso compartido de recursos](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [Descargar plantilla de notificación de correo electrónico del recurso](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [Ejemplo de licencias de DRM](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [Vincular plantilla de notificación de correo electrónico compartido](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [InDesign Scripts de flujo de trabajo](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [Configuraciones de transcodificación de vídeo](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
* [Varios](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc2)

## Con actualización a 6.5 {#with-upgrade}

### Varios {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td>/etc/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td>/var/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Si algún código personalizado depende de esta ubicación (es decir, el código depende explícitamente de esta ruta), el código debe actualizarse para utilizar la nueva ubicación antes de actualizar. Lo ideal es que las API de Java™ se utilicen cuando estén disponibles para reducir las dependencias de cualquier ruta específica en el JCR.</p> <p>Ubicación temporal que contiene un archivo zip para que el cliente lo descargue. No es necesario actualizar desde el momento en que el cliente solicita descargar el recurso. Genera un archivo en la nueva ubicación.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

## Antes de una actualización futura {#prior-to-upgrade}

### Plantilla de notificación de correo electrónico de evento de colección/recurso {#asset-collection-event-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/notification/email/default</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/dam/notification</code></p> <p><code>/apps/settings/dam/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Si el cliente modificó las plantillas de correo electrónico, realice las siguientes acciones para alinearlas con la nueva estructura del repositorio:</p>
    <ol>
     <li>La plantilla de correo electrónico <code>/libs/settings/dam/notification</code> debe copiarse de <strong><code>/etc/notification/email/default</code></strong> a <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>Dado que el destino se encuentra en <strong> <code>/apps</code></strong>, este cambio debe persistir en SCM.</li>
      </ol> </li>
     <li>Quitar la carpeta: <strong><code>/etc/dam/notification/email/default</code></strong> después de mover las plantillas de correo electrónico que contiene.<br />
      <ol>
       <li>AEM Si no se han realizado actualizaciones en la plantilla de correo electrónico en <strong> <code>/etc/notification/email/default</code></strong>, la carpeta se puede quitar, ya que la plantilla de correo electrónico original existe en <strong><code>/libs/settings/notification/email/default</code></strong> como parte de la instalación de la versión 4 de la instalación de la aplicación de correo electrónico en la que se ha realizado el proceso de instalación de la aplicación de la.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Diseños clásicos de uso compartido de recursos {#classic-asset-share-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/designs/assetshare</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/wcm/designs/assetshare</code></p> <p><code>/apps/settings/wcm/designs/assetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para cualquier diseño que se administre en SCM y no se escriba en tiempo de ejecución mediante cuadros de diálogo de diseño, realice las siguientes acciones para alinearlo con el modelo más reciente:</p>
    <ol>
     <li>Copie los diseños de la ubicación anterior en la nueva ubicación bajo <code>/apps</code>.</li>
     <li>Convierta cualquier recurso CSS, JavaScript y estático del diseño en una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">biblioteca de cliente</a> con <code>allowProxy = true</code>.</li>
     <li>AEM Actualice las referencias a la ubicación anterior en la propiedad <code>cq:designPath</code> mediante <strong>Administración de DAM &gt; Página de uso compartido de recursos &gt; Propiedades de página &gt; Pestaña Avanzadas &gt; Campo de diseño</strong>.</li>
     <li>Para utilizar la nueva categoría Biblioteca de cliente, actualice todas las páginas que hagan referencia a la ubicación anterior. Esto requiere actualizar el código de implementación de página.</li>
     <li>Actualice las reglas de Dispatcher para permitir el servicio de bibliotecas de cliente mediante el servlet proxy <code>/etc.clientlibs/</code>.</li>
    </ol> <p>Para cualquier diseño que no se administre en SCM y que se modifique en tiempo de ejecución mediante cuadros de diálogo de diseño, no mueva diseños legibles fuera de <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Descargar plantilla de notificación de correo electrónico del recurso {#download-asset-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/dam/workflownotification/email/downloadasset</code></p> <p><code>/apps/settings/dam/workflownotification/email/downloadasset</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Si se han modificado las plantillas de correo electrónico (<strong>downloadasset</strong> o <strong>transientworkflowcompleted</strong>), siga el siguiente procedimiento para alinearse con la nueva estructura:</p>
    <ol>
     <li>La plantilla de correo electrónico actualizada debe copiarse de <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> a <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>Dado que el destino se encuentra en <strong> <code>/apps</code></strong>, este cambio debe persistir en SCM.</li>
      </ol> </li>
     <li>Quitar la carpeta: <code>/etc/dam/workflow/notification/email/downloadasset </code>después de mover las plantillas de correo electrónico que contiene.<br />
      <ol>
       <li>AEM Si no se han realizado actualizaciones en la plantilla de correo electrónico en <strong> <code>/etc</code></strong>, la carpeta se puede quitar, ya que la plantilla de correo electrónico original existe en <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> como parte de la instalación de la versión 6.4 de.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Aunque <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> es técnicamente compatible con la búsqueda (tiene prioridad antes de /apps por medio de la búsqueda Sling CAConfig habitual, pero después de <code>/etc</code>), la plantilla podría colocarse en <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. Sin embargo, esto no se recomienda, ya que no hay ninguna interfaz de usuario de tiempo de ejecución para facilitar la edición de la plantilla de correo electrónico.</td>
  </tr>
 </tbody>
</table>

### Ejemplo de licencias de DRM {#example-drm-licenses}

| **Ubicación anterior** | `/etc/dam/drm/licenses/` |
|---|---|
| **Nueva(s) ubicación(es)** | `/libs/settings/dam/drm` |
| **Directrices de reestructuración** | N/D |
| **Notas** | N/D |

### Vincular plantilla de notificación de correo electrónico compartido {#link-share-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/dam/adhocassetshare</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/dam/adhocassetshare</code></p> <p><code>/apps/settings/dam/adhocassetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Si el cliente modificó la plantilla de correo electrónico, para alinearla con la nueva estructura del repositorio:</p>
    <ol>
     <li>La plantilla de correo electrónico actualizada debe copiarse de <strong><code>/etc/dam/adhocassetshare</code></strong> a <strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>Como el destino está en <strong><code>/apps</code></strong>, este cambio debe persistir en SCM.</li>
      </ol> </li>
     <li>Quitar la carpeta: <strong><code>/etc/dam/adhocassetshare</code></strong> después de mover las plantillas de correo electrónico que contiene.<br />
      <ol>
       <li>AEM Si no se han realizado actualizaciones en la plantilla de correo electrónico en <strong> <code>/etc</code></strong>, la carpeta se puede quitar, ya que la plantilla de correo electrónico original existe en <strong><code>/libs/settings/dam/adhocassetshare</code></strong> como parte de la instalación de la versión 6.4 de.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Aunque <code>/conf/global/settings/dam/adhocassetshare</code> es técnicamente compatible con la búsqueda (tiene prioridad antes de <code>/apps</code> mediante la búsqueda de configuración CAC de Sling habitual, pero después de <code>/etc</code>), la plantilla se puede colocar en <code>/conf/global/settings/dam/adhocassetshare</code>. Sin embargo, esto no se recomienda, ya que no hay ninguna interfaz de usuario de tiempo de ejecución para facilitar la edición de la plantilla de correo electrónico</td>
  </tr>
 </tbody>
</table>

### InDesign Scripts de flujo de trabajo {#indesign-workflow-scripts}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/dam/indesign/scripts</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/dam/indesign</code></p> <p><code>/apps/settings/dam/indesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para alinearse con la nueva estructura del repositorio:</p>
    <ol>
     <li>Copiar todos los scripts personalizados o modificados de <strong><code>/etc/dam/indesign/scripts</code></strong> a <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>AEM AEM Copiar solo los scripts nuevos o modificados como scripts no modificados proporcionados por los que se han proporcionado, se encuentra disponible mediante <strong><code>/libs/settings</code></strong> en la versión 6.5 de la versión de</li>
      </ol> </li>
     <li>Localice todos los modelos de flujo de trabajo que utilizan el paso WF del proceso de extracción de medios y
      <ol>
       <li>Para cada instancia del paso del flujo de trabajo, actualice las rutas en la configuración para que apunten explícitamente a los scripts adecuados en <strong> <code>/apps/settings/dam/indesign/scripts</code></strong> o <strong><code>/libs/settings/dam/indesign/scripts</code></strong>, según corresponda.</li>
      </ol> </li>
     <li>Quitar <strong> <code>/etc/dam/indesign/scripts</code></strong> por completo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Se recomienda almacenar los scripts personalizados en <code>/apps</code>, ya que esa es la ubicación donde se debe almacenar el código.</td>
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
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/dam/video</code></p> <p><code>/apps/settings/dam/video</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Las personalizaciones de nivel de proyecto deben cortarse y pegarse en rutas equivalentes de <code>/apps</code> o <code>/conf</code>, según corresponda.</p> <p>AEM Para alinearse con la estructura del repositorio de 6.4:</p>
    <ol>
     <li>Copie cualquier configuración de vídeo modificada de <code>/etc/dam/video</code> a <code>/apps/settings/dam/video</code></li>
     <li>Quitar <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Configuraciones preestablecidas del visor {#viewer-preset-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/dam/presets/viewer</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para el ajuste preestablecido de visor predeterminado, solo está disponible en la nueva ubicación.</p> <p>Para el ajuste preestablecido de visualizador personalizado:</p>
    <ul>
     <li>ejecute un script de migración para poder mover el nodo de <code>/etc</code> a <code>/conf</code>. El script se encuentra en <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>o puede editar la configuración y se guardan automáticamente en la nueva ubicación.</li>
    </ul> <p>No tiene que ajustar su código copyURL/embed para que apunte a <code>/conf</code>. La solicitud existente a <code>/etc</code> se redireccionó al contenido correcto desde <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Varios {#misc2}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><code>/libs/dam/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Ajuste cualquier referencia para que apunte a los nuevos recursos de <code>/libs</code> mediante el prefijo del proxy de permiso <code>/etc.clientlibs/</code>.</p> <p>Por último, limpie eliminando las carpetas para los clientlibs migrados de <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>
