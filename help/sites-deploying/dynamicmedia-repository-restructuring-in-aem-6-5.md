---
title: Reestructuración del repositorio de Dynamic Media en Adobe Experience Manager 6.5
description: Aprenda a realizar los cambios necesarios para migrar a la nueva estructura de repositorios en Experience Manager 6.5 para Dynamic Media.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 4e736924-74ea-431a-be19-1c4ff022f464
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 4%

---

# Reestructuración del repositorio de Dynamic Media en Adobe Experience Manager 6.5 {#dynamic-media-repository-restructuring-in-aem}

Como se describe en la página principal [Reestructuración del repositorio en Adobe Experience Manager 6.5](/help/sites-deploying/repository-restructuring.md), los clientes que actualicen a Experience Manager 6.5 deben utilizar esta página para evaluar el esfuerzo de trabajo asociado con los cambios del repositorio que afectan a Dynamic Media. Algunos cambios requieren esfuerzo de trabajo durante el proceso de actualización de Experience Manager 6.5, mientras que otros se pueden aplazar hasta una actualización futura.

**Antes de futuras actualizaciones**

* [Configuraciones personalizadas de codificación de vídeo adaptable](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [Configuración en la nube de Dynamic Media (DMS7)](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [Configuración del Cloud Service de Dynamic Media (DM Hybrid)](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [Dynamic Media: Configuración del Cloud Service de YouTube](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
* [Varios](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#misc)

## Antes de futuras actualizaciones {#prior-to-upgrade}

### Configuraciones personalizadas de codificación de vídeo adaptable  {#custom-adaptive-video-encoding-configurations}

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
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Puede ejecutar el siguiente script de migración para migrar a la nueva ubicación:</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>Como alternativa, puede editar la configuración en la interfaz de usuario de Experience Manager y los cambios se guardan en la nueva ubicación.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configuración en la nube de Dynamic Media (DMS7) {#dynamic-media-dms-cloud-configuration}

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
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>El cliente puede ejecutar un script de migración en esta ubicación:<br /> </p>
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
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Puede ejecutar el siguiente script de migración para alinearlo con el modelo más reciente:</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.jso</em></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media: configuración del Cloud Service de YouTube  {#youtubecloudserviceconfiguration}

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
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>1. Anule la publicación de todos los vídeos de YouTube<br /> 2. Cree la configuración de YouTube con la nueva interfaz de usuario táctil (de <code>/conf</code>), incluida la copia de todos los canales de la ubicación antigua <br /> 3. Publish devuelve todos los vídeos a YouTube.</p> <p>Este flujo de trabajo genera nuevas direcciones URL de YouTube. Si no cancela la publicación antes de crear una configuración de YouTube de IU táctil, tiene varias URL de YouTube enumeradas en Propiedades porque los canales creados de nuevo se publican de nuevo, si se le da la oportunidad. Esta funcionalidad significa que tiene direcciones URL inútiles en Propiedades.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Varios {#misc}

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
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>El cliente puede ejecutar el siguiente script de migración.</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>Como alternativa, puede editar la configuración en la interfaz de usuario de Experience Manager y los cambios se guardan en la nueva ubicación.</p> </td>
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
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>El cliente puede ejecutar el siguiente script de migración.</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>
