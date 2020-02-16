---
title: 'Resolución de problemas de Dynamic Media: modo de Scene7'
description: Resolución de problemas de Dynamic Media en el modo de ejecución de Scene7.
uuid: 77e04ccf-33dc-4d2f-8950-318d4b008f74
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 0d48c031-d3ee-4143-b739-a79ba28fd63a
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Resolución de problemas de Dynamic Media: modo de Scene7{#troubleshooting-dynamic-media-scene-mode}

En el siguiente documento se describe la solución de problemas de Dynamic Media que ejecuta el modo de ejecución **dynamicmedia_scene7** .

##  Configuración y configuración {#setup-and-configuration}

Asegúrese de que Dynamic Media se ha configurado correctamente haciendo lo siguiente:

* El comando Start up contiene el argumento `-r dynamicmedia_scene7` runmode.
* Todos los paquetes de correcciones acumulativas (CFP) de AEM 6.4 se han instalado primero *antes* de los paquetes de funciones de Dynamic Media disponibles.
* Se ha instalado el Feature Pack 18912 opcional.

   Este paquete de funciones opcional es compatible con FTP o si está migrando recursos a Dynamic Media desde Dynamic Media Classic (Scene7).

* Vaya a la interfaz de usuario de Cloud Services y confirme que la cuenta aprovisionada aparece en Configuraciones **** disponibles.
* Asegúrese de que el agente de `Dynamic Media Asset Activation (scene7)` replicación esté habilitado.

   Este agente de replicación se encuentra en Agentes en Autor.

## General (Todos los recursos) {#general-all-assets}

Los siguientes son algunos trucos y sugerencias generales para todos los recursos.

### Propiedades del estado de sincronización de recursos {#asset-synchronization-status-properties}

Las siguientes propiedades de recurso se pueden revisar en CRXDE Lite para confirmar la sincronización correcta del recurso de AEM a Dynamic Media:

| **Propiedad** | **Ejemplo** | **Descripción** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | Indicador general de que el nodo está vinculado a Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** o texto de error | Estado de la carga de recursos a Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Debe rellenarse para poder generar direcciones URL en un recurso remoto de Dynamic Media. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **success** o **failed:`<error text>`** | Estado de sincronización de conjuntos (conjuntos de giros, conjuntos de imágenes, etc.), ajustes preestablecidos de imagen, ajustes preestablecidos de visor, actualizaciones de mapas de imagen para un recurso o imágenes editadas. |

### Registro de sincronización {#synchronization-logging}

Los errores y problemas de sincronización se registran `error.log` (directorio del servidor AEM `/crx-quickstart/logs/`). Hay suficiente registro para determinar la causa raíz de la mayoría de los problemas, pero puede aumentar el registro en DEBUG en el `com.adobe.cq.dam.ips` paquete a través de la consola de Sling ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) para recopilar más información.

### Mover, copiar, eliminar {#move-copy-delete}

Antes de realizar una operación de movimiento, copia o eliminación, haga lo siguiente:

* Para imágenes y vídeos, confirme que existe un `<object_node>/jcr:content/metadata/dam:scene7ID` valor antes de realizar operaciones de movimiento, copia o eliminación.
* Para los ajustes preestablecidos de imagen y visor, confirme que existe un `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` valor antes de realizar operaciones de movimiento, copia o eliminación.
* Si falta el valor de metadatos superior, deberá volver a cargar los recursos antes de mover, copiar o eliminar operaciones.

### Control de versión {#version-control}

Al reemplazar un recurso de Dynamic Media existente (el mismo nombre y la misma ubicación), tiene la opción de conservar ambos recursos o de reemplazar o crear una versión:

* Al mantener ambos, se creará un nuevo recurso con un nombre único para la URL del recurso publicado. Por ejemplo, `image.jpg` es el recurso original y `image1.jpg` es el recurso recién cargado.

* La creación de una versión no es compatible con la entrega en modo Dynamic Media - Scene7. La nueva versión reemplazará al recurso existente en la entrega.

## Imágenes y conjuntos {#images-and-sets}

Si tiene problemas con las imágenes y los conjuntos, consulte las siguientes instrucciones para solucionar problemas.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Cómo depurar</strong></td>
   <td><strong>Solución</strong></td>
  </tr>
  <tr>
   <td>No se puede acceder al botón Copiar URL/Incrustar en la vista de detalles del recurso</td>
   <td>
    <ol>
     <li><p>Vaya a CRX/DE:</p>
      <ul>
       <li>Compruebe si el ajuste preestablecido del JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> está definido. Tenga en cuenta que esta ubicación se aplica si ha actualizado AEM 6.x a 6.4 y ha optado por no migrar. De lo contrario, la ubicación es <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Asegúrese de que el recurso del JCR está <code>dam:scene7FileStatus</code><strong> en la sección Metadatos se muestra como </strong><code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>Actualice la página/navegue a otra página y regrese (es necesario volver a compilar JSP del carril lateral)</p> <p>Si eso no funciona:</p>
    <ul>
     <li>Publicar recurso.</li>
     <li>Vuelva a cargar el recurso y publíquelo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Selector de recursos en el editor de conjuntos atascado en la carga permanente</td>
   <td><p>Problema conocido que se va a solucionar en 6.4</p> </td>
   <td><p>Cierre el selector y vuelva a abrirlo.</p> </td>
  </tr>
  <tr>
   <td><strong>El botón Seleccionar</strong> no está activo después de seleccionar un recurso como parte de la edición de un conjunto</td>
   <td><p> </p> <p>Problema conocido que se va a solucionar en 6.4</p> <p> </p> </td>
   <td><p>Haga clic primero en otra carpeta del Selector de recursos y vuelva para seleccionar el recurso.</p> </td>
  </tr>
  <tr>
   <td>La zona interactiva de carrusel se desplaza después de cambiar entre diapositivas</td>
   <td><p>Compruebe que todas las diapositivas tengan el mismo tamaño.</p> </td>
   <td><p>Utilice solo imágenes con el mismo tamaño para el carrusel.</p> </td>
  </tr>
  <tr>
   <td>La imagen no se previsualiza con el visor de Dynamic Media</td>
   <td><p>Compruebe que el recurso contiene <code>dam:scene7File</code> en las propiedades de metadatos (CRXDE Lite)</p> </td>
   <td><p>Compruebe que todos los recursos han terminado de procesarse.</p> </td>
  </tr>
  <tr>
   <td>El recurso cargado no se muestra en el selector de recursos</td>
   <td><p>El recurso de verificación tiene la propiedad <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Compruebe que todos los recursos han terminado de procesarse.</p> </td>
  </tr>
  <tr>
   <td>La pancarta en la vista de tarjeta muestra <strong>Nuevo</strong> cuando el recurso no ha empezado a procesarse</td>
   <td>Marque el recurso <code>jcr:content</code> &gt; <code>dam:assetState</code> = si el flujo de trabajo no <code>unprocessed</code> lo recogió.</td>
   <td>Espere hasta que el flujo de trabajo recoja el recurso.</td>
  </tr>
  <tr>
   <td>Las imágenes o los conjuntos no muestran la dirección URL del visor ni el código incrustado</td>
   <td>Compruebe si se ha publicado el ajuste preestablecido de visor.</td>
   <td><p>Vaya a <strong>Herramientas</strong> &gt; <strong>Recursos</strong> &gt; Ajustes preestablecidos <strong></strong> de visor y publique el ajuste preestablecido de visor.</p> </td>
  </tr>
 </tbody>
</table>

## El vídeo {#video}

Si tiene problemas con el vídeo, consulte las siguientes instrucciones para solucionar problemas.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Cómo depurar</strong></td>
   <td><strong>Solución</strong></td>
  </tr>
  <tr>
   <td>No se puede previsualizar el vídeo</td>
   <td>
    <ul>
     <li>Compruebe que la carpeta tiene un perfil de vídeo asignado (si el formato de archivo no es compatible). Si no se admite, solo se muestra una imagen.</li>
     <li>El perfil de vídeo debe contener más de un ajuste preestablecido de codificación para generar un conjunto AVS (las codificaciones únicas se tratan como contenido de vídeo para archivos MP4; para los archivos no admitidos, se trata igual que los archivos no procesados).</li>
     <li>Compruebe que el vídeo ha terminado de procesarse confirmando <code>dam:scene7FileAvs</code> de <code>dam:scene7File</code> los metadatos.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Asigne un perfil de vídeo a la carpeta.</li>
     <li>Edite el perfil de vídeo para incluir más de un ajuste preestablecido de codificación.</li>
     <li>Espere a que el vídeo termine de procesarse.</li>
     <li>Para volver a cargar el vídeo, asegúrese de que el flujo de trabajo de codificación de vídeo de Dynamic Media no se está ejecutando.<br /> </li>
     <li>Vuelva a cargar el vídeo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>El vídeo no está codificado</td>
   <td>
    <ul>
     <li>Compruebe que el modo de ejecución es <code>dynamicmedia_scene7</code>.</li>
     <li>Compruebe si el servicio de nube de Dynamic Media está configurado.</li>
     <li>Compruebe si un perfil de vídeo está asociado a la carpeta de carga.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Compruebe su instancia de AEM con <code>-r dynamicmedia_scene7</code></li>
     <li>Compruebe que la configuración de Dynamic Media en Cloud Services está correctamente configurada.</li>
     <li>Compruebe que la carpeta tiene un perfil de vídeo. Además, compruebe el perfil de vídeo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>El procesamiento de vídeo tarda demasiado</td>
   <td><p>Para determinar si la codificación de vídeo sigue en curso o si ha entrado en un estado de error:</p>
    <ul>
     <li>Compruebe el estado del vídeo <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
     <li>Monitoree el vídeo desde las fichas Consola de flujo de trabajo <code>https://localhost:4502/libs/cq/workflow/content/console.html</code> &gt; Instancias, Archivar, Errores.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Falta la representación de vídeo</td>
   <td><p>Cuando se carga el vídeo, pero no hay representaciones codificadas:</p>
    <ul>
     <li>Compruebe que la carpeta tiene un perfil de vídeo asignado.</li>
     <li>Compruebe que el vídeo ha terminado de procesarse confirmando <code>dam:scene7FileAvs</code> los metadatos.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Asigne un perfil de vídeo a la carpeta.</li>
     <li>Espere a que el vídeo termine de procesarse.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Visores {#viewers}

Si tiene problemas con los visores, consulte las siguientes instrucciones para solucionar problemas.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Cómo depurar</strong></td>
   <td><strong>Solución</strong></td>
  </tr>
  <tr>
   <td>Los ajustes preestablecidos de visor no se publican</td>
   <td><p>Vaya a la página de diagnóstico del administrador de muestra: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>Observe los valores calculados. Cuando funcione correctamente, debería ver:</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>Nota</strong>: Los recursos del visor pueden tardar unos 10 minutos en sincronizarse tras la configuración de la nube de Dynamic Media.</p> <p>Si los recursos no activados permanecen, haga clic en cualquiera de los botones <strong>Enumerar todos los recursos</strong> no activados para ver los detalles.</p> </td>
   <td>
    <ol>
     <li>Vaya a la lista de ajustes preestablecidos de visor en las herramientas de administración: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>Seleccione todos los ajustes preestablecidos de visor y, a continuación, haga clic en <strong>Publicar</strong>.</li>
     <li>Vuelva al administrador de muestra y observe que el recuento de recursos no activado es ahora cero.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>La ilustración de Ajustes preestablecidos de visor devuelve 404 desde la vista previa en los detalles del recurso o desde la URL de copia o el código incrustado</td>
   <td><p>En CRXDE Lite, haga lo siguiente:</p>
    <ol>
     <li>Vaya a <code>&lt;sync-folder&gt;/_CSS/_OOTB</code> la carpeta de sincronización de Dynamic Media (por ejemplo, <code>/content/dam/_CSS/_OOTB</code>),</li>
     <li>Busque el nodo de metadatos del recurso problemático (por ejemplo, <code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>).</li>
     <li>Compruebe la presencia de <code>dam:scene7*</code> propiedades. Si el recurso se ha sincronizado y publicado correctamente, verá que el <code>dam:scene7FileStatus</code> conjunto es <strong>PublishComplete</strong>.</li>
     <li>Intente solicitar la ilustración directamente desde Dynamic Media concatenando los valores de las siguientes propiedades y literales de cadena
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>Ejemplo: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>Si los recursos de muestra o la ilustración de ajustes preestablecidos de visor no se han sincronizado o publicado, reinicie todo el proceso de copia/sincronización:</p>
    <ol>
     <li>Vaya a CRXDE Lite.
      <ul>
       <li>Eliminar <code>&lt;sync-folder&gt;/_CSS/_OOTB</code>.</li>
      </ul> </li>
     <li>Vaya al administrador de paquetes de CRX: <code>https://localhost:4502/crx/packmgr/</code><a href="https://localhost:4502/crx/packmgr/"></a>
      <ol>
       <li>Buscar el paquete de visor en la lista (empieza por <code>cq-dam-scene7-viewers-content</code>)</li>
       <li>Haga clic en <strong>Reinstalar</strong>.</li>
      </ol> </li>
     <li>En Cloud Services, vaya a la página de configuración de Dynamic Media y, a continuación, abra el cuadro de diálogo de configuración de Dynamic Media - S7.
      <ul>
       <li>No realice cambios, haga clic en <strong>Guardar</strong>. Esto desencadena la lógica de nuevo para crear y sincronizar los recursos de muestra, el ajuste preestablecido de visor CSS y la ilustración.<br />  </li>
      </ul> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

