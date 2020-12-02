---
title: Reestructuración del repositorio de Dynamic Media en AEM 6.5
seo-title: Reestructuración del repositorio de Dynamic Media en AEM 6.5
description: Obtenga información sobre cómo realizar los cambios necesarios para migrar a la nueva estructura de repositorio en AEM 6.5 para Dynamic Media.
seo-description: Obtenga información sobre cómo realizar los cambios necesarios para migrar a la nueva estructura de repositorio en AEM 6.5 para Dynamic Media.
uuid: e26d61a4-47b6-493a-9ba2-4c58b200ddd9
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 61cd5751-0dc8-48e0-873e-3a64899489bb
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 4%

---


# Reestructuración del repositorio de Dynamic Media en AEM 6.5 {#dynamic-media-repository-restructuring-in-aem}

Como se describe en la página principal [Reestructuración del repositorio en AEM 6.5](/help/sites-deploying/repository-restructuring.md), los clientes que actualicen a AEM 6.5 deben utilizar esta página para evaluar el esfuerzo de trabajo asociado con los cambios del repositorio que afectan a la solución Dynamic Media. Algunos cambios requieren esfuerzo de trabajo durante el proceso de actualización a AEM 6.5, mientras que otros se pueden posponer hasta una actualización futura.

**Antes de la actualización futura**

* [Configuraciones personalizadas de codificación de vídeo adaptable](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [Configuración de nube de Dynamic Media (DMS7)](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [Configuración de Cloud Service de Dynamic Media (DM híbrido)](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [Medios dinámicos: configuración del Cloud Service de YouTube](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
* [Misc](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#misc)

## Antes de la actualización futura {#prior-to-upgrade}

### Configuraciones de codificación de vídeo adaptable personalizadas {#custom-adaptive-video-encoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
  </tr>
  <tr>
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Puede ejecutar la siguiente secuencia de comandos de migración para migrar a la nueva ubicación:</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>También puede editar la configuración en AEM interfaz de usuario y los cambios se guardarán en la nueva ubicación.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configuración de nube de Dynamic Media (DMS7) {#dynamic-media-dms-cloud-configuration}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>El cliente puede ejecutar una secuencia de comandos de migración en esta ubicación:<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>Reinicie el paquete OSGi de Dynamic Media.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Configuración del Cloud Service de Dynamic Media (DM Hybrid) {#cloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Puede ejecutar la secuencia de comandos de migración siguiente para alinearla con el modelo más reciente:</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.jso</em></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Medios dinámicos: configuración del Cloud Service de YouTube {#youtubecloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/cloudservices/youtube</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
  </tr>
  <tr>
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>1. Cancelar la publicación de todos los vídeos de YouTube<br /> 2. Cree la configuración de YouTube mediante la nueva IU táctil (desde <code>/conf</code>), incluida la copia de todos los Canales de la ubicación anterior<br /> 3. Publique todos los vídeos en YouTube.</p> <p>Este flujo de trabajo resulta en nuevas direcciones URL de YouTube. Si no cancela la publicación antes de crear una nueva configuración de YouTube de TouchUI, tendrá varias URL de YouTube en Propiedades, ya que los Canales recreados se publicarán de nuevo si se les da la oportunidad. Esto significa que tendrá direcciones URL inútiles en la lista Propiedades.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Misc {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/dam/imageserver/macros</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
  </tr>
  <tr>
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>El cliente puede ejecutar la secuencia de comandos de migración siguiente.</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>También puede editar la configuración en AEM interfaz de usuario y los cambios se guardarán en la nueva ubicación.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/dam/presets/analytics</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
  </tr>
  <tr>
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>El cliente puede ejecutar la secuencia de comandos de migración siguiente.</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

