---
title: Integración de Adobe Experience Manager con Dynamic Media Classic
description: Aprenda a integrar Adobe Experience Manager con Dynamic Media Classic.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: f244cfb5-5550-4f20-92f0-bb296e2bf76e
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '5484'
ht-degree: 1%

---

# Integración de Adobe Experience Manager con Dynamic Media Classic {#integrating-with-dynamic-media-classic-scene}

Adobe Dynamic Media Classic es una solución alojada para administrar, mejorar, publicar y distribuir recursos de medios enriquecidos en la Web, dispositivos móviles, correo electrónico y pantallas e impresiones conectadas a Internet.

Para utilizar Dynamic Media Classic, debe configurar la configuración de nube para que Dynamic Media Classic y Adobe Experience Manager Assets puedan interactuar entre sí. En este documento se describe cómo configurar Experience Manager y Dynamic Media Classic.

Para obtener información sobre el uso de todos los componentes de Dynamic Media Classic en una página y el trabajo con vídeo, consulte [Uso de Dynamic Media Classic](../assets/scene7.md).

>[!NOTE]
>
>* La plataforma del visor DHTML de Dynamic Media Classic llegó oficialmente al final de su vida útil el 31 de enero de 2014. Para obtener más información, consulte las [Preguntas frecuentes sobre la caducidad del visor DHTML](../sites-administering/dhtml-viewer-endoflifefaqs.md).
>* Antes de configurar Dynamic Media Classic para que funcione con Experience Manager, consulte [Prácticas recomendadas](#best-practices-for-integrating-scene-with-aem) para integrar Dynamic Media Classic con Experience Manager.
>* Si utiliza Dynamic Media Classic con una configuración proxy personalizada, debe configurar ambas configuraciones proxy del cliente HTTP, ya que algunas funcionalidades de Experience Manager utilizan las API 3.x y otras utilizan las API 4.x. 3.x se configura con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) y 4.x se configura con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator).

>



## Integración Experience Manager/Dynamic Media Classic frente a Dynamic Media {#aem-scene-integration-versus-dynamic-media}

Los usuarios Experience Manager pueden elegir entre dos soluciones para trabajar con Dynamic Media. Puede utilizar una de las siguientes opciones:

* Integre la instancia de Experience Manager con Dynamic Media Classic.
* Utilice Dynamic Media integrado en Experience Manager.

Utilice los siguientes criterios para determinar qué solución elegir:

* ¿Es usted **cliente existente** de Dynamic Media Classic cuyos recursos residen en Dynamic Media Classic para su publicación y envío, pero desea integrarlos con la creación de sitios (WCM) o Experience Manager Assets, o ambos? Si es así, utilice la [integración punto a punto](#aem-scene-point-to-point-integration) del Experience Manager/Dynamic Media Classic descrita en este documento.

* Si es cliente de **new** Experience Manager que tiene necesidades de envío de medios enriquecidos, seleccione la [opción de Dynamic Media](#aem-dynamic-media). Esta opción tiene más sentido si no tiene una cuenta de S7 existente y muchos recursos almacenados en ese sistema.

* En algunos casos, utilice ambas soluciones. El [escenario de doble uso](/help/sites-administering/scene7.md#dual-use-scenario) describe ese escenario.

### Integración punto a punto de Experience Manager/Dynamic Media Classic {#aem-scene-point-to-point-integration}

Cuando trabaje con recursos en esta solución, realice una de las siguientes acciones:

* Cargue recursos directamente en Dynamic Media Classic y, a continuación, acceda a través del explorador de contenido **Dynamic Media Classic** para la creación de páginas o
* Cargue en Recursos Experience Manager y, a continuación, active la publicación automática en Dynamic Media Classic; puede acceder a través del explorador de contenido **Assets** para la creación de páginas

Los componentes que utiliza para esta integración se encuentran en el área del componente **Dynamic Media Classic** en [Design mode](/help/sites-authoring/author-environment-tools.md#page-modes).

### Experience Manager Dynamic Media {#aem-dynamic-media}

Experience Manager Dynamic Media es la unificación de las funciones de Dynamic Media Classic directamente en la plataforma de Experience Manager.

Cuando trabaje con recursos en esta solución, siga este flujo de trabajo:

1. Cargue recursos de imagen y vídeo únicos directamente en el Experience Manager.
1. Codifique los vídeos directamente en Experience Manager.
1. Cree conjuntos basados en imágenes directamente en Experience Manager.
1. Si corresponde, agregue interactividad a imágenes o vídeos.

Los componentes que utiliza para Dynamic Media se encuentran en el área del componente **[!UICONTROL Dynamic Media]** en [Design mode](/help/sites-authoring/author-environment-tools.md#page-modes). Incluyen lo siguiente:

* **[!UICONTROL Dynamic Media]** : el componente  **[!UICONTROL Dynamic]** Mediacomponent es inteligente, ya que, dependiendo de si agrega una imagen o un vídeo, dispone de varias opciones. El componente admite ajustes preestablecidos de imagen, visores basados en imágenes, como conjuntos de imágenes, conjuntos de giros, conjuntos de medios mixtos y vídeo. Además, el visor es interactivo: el tamaño de la pantalla cambia automáticamente según el tamaño de la pantalla. Todos los visores son visores HTML5.

* **[!UICONTROL Medios interactivos]** : el componente  **[!UICONTROL interactivo de]** medios es para recursos como banners de carrusel, imágenes interactivas y vídeo interactivo. Estos activos tienen interactividad en ellos, como zonas interactivas o mapas de imágenes. Este componente es inteligente. Es decir, en función de si agrega una imagen o un vídeo, tiene varias opciones. Además, el visor es interactivo: el tamaño de la pantalla cambia automáticamente según el tamaño de la pantalla. Todos los visores son visores HTML5.

### Escenario de doble uso {#dual-use-scenario}

De serie, puede utilizar simultáneamente las funciones de integración de Dynamic Media y Dynamic Media Classic de Experience Manager. En la siguiente tabla de casos de uso se describe cuándo se activan y desactivan determinadas áreas.

Para usar Dynamic Media y Dynamic Media Classic simultáneamente:

1. Configure [Dynamic Media Classic](#creating-a-cloud-configuration-for-scene) en Cloud Services.
1. Siga las instrucciones específicas de su caso de uso:

   <table>
    <tbody>
    <tr>
    <td> </td>
    <td> </td>
    <td><strong>Dynamic Media</strong></td>
    <td> </td>
    <td><strong>Integración de Dynamic Media Classic</strong></td>
    <td> </td>
    </tr>
    <tr>
    <td><strong>Si usted es ...</strong></td>
    <td><strong>Flujo de trabajo de caso de uso</strong></td>
    <td><strong>Imágenes/Vídeo</strong></td>
    <td><strong>Componente de Dynamic Media</strong></td>
    <td><strong>Navegador de contenido y componentes de S7</strong></td>
    <td><strong>Carga automática de Assets a S7</strong></td>
    </tr>
    <tr>
    <td>Novedades en Sitios y Dynamic Media</td>
    <td>Cargar recursos a Experience Manager y utilizar el componente Dynamic Media de Experience Manager para crear recursos en páginas de Sites</td>
    <td><p>Activado</p> <p>(Véase el paso 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Activado</a></td>
    <td>Desactivado</td>
    <td>Desactivado</td>
    </tr>
    <tr>
    <td>En el comercio minorista y nuevas en Sites y Dynamic Media</td>
    <td>Cargue recursos que no sean de productos a Experience Manager para su administración y envío. Cargue recursos de PRODUCTO en Dynamic Media Classic y utilice el navegador de contenido de Dynamic Media Classic en Experience Manager y componente para crear páginas de detalles de producto en Sites.</td>
    <td><p>Activado</p> <p>(Véase el paso 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Activado</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Activado</a></td>
    <td>Desactivado</td>
    </tr>
    <tr>
    <td>Novedades en Assets y Dynamic Media</td>
    <td>Cargar recursos a recursos de Experience Manager y usar una URL o un código incrustado publicados de Dynamic Media</td>
    <td><p>Activado</p> <p>(Véase el paso 3)</p> </td>
    <td>Desactivado</td>
    <td>Desactivado</td>
    <td>Desactivado</td>
    </tr>
    <tr>
    <td>Novedades en Dynamic Media y Plantillas</td>
    <td>Utilice Dynamic Media para imágenes y vídeos. Cree plantillas de imagen en Dynamic Media Classic y use el buscador de contenido de Dynamic Media Classic para incluir plantillas en las páginas de Sites.</td>
    <td><p>Activado</p> <p>(Véase el paso 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Activado</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Activado</a></td>
    <td>Desactivado</td>
    </tr>
    <tr>
    <td>Un cliente de Dynamic Media Classic existente y es nuevo en Sites</td>
    <td>Cargar recursos a Dynamic Media Classic y usar el navegador de contenido de Experience Manager Dynamic Media Classic para buscar y crear recursos en las páginas de Sites</td>
    <td>Desactivado</td>
    <td>Desactivado</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Activado</a></td>
    <td>Desactivado</td>
    </tr>
    <tr>
    <td>Un cliente existente de Dynamic Media Classic y son nuevos en Sites y Assets</td>
    <td>Cargue recursos en DAM y publíquelos automáticamente en Dynamic Media Classic para su envío. Utilice el navegador de contenido de Dynamic Media Classic de Experience Manager para buscar y crear recursos en las páginas de Sites.</td>
    <td>Desactivado</td>
    <td>Desactivado</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Activado</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">Activado</a></p> <p>(Véase el paso 4)</p> </td>
    </tr>
    <tr>
    <td>Cliente Dynamic Media Classic existente y nuevo en Assets</td>
    <td><p>Cargue recursos a Experience Manager y utilice Dynamic Media para generar representaciones para descargarlos o compartirlos. Publicar automáticamente los recursos del Experience Manager en Dynamic Media Classic para su envío.</p> <p><strong>Importante:</strong> Incurre en que el procesamiento duplicado y las representaciones generadas en el Experience Manager no se sincronizan con Dynamic Media Classic</p> </td>
    <td><p>Activado</p> <p>(Véase el paso 3)</p> </td>
    <td>Desactivado</td>
    <td>Desactivado</td>
    <td><p><a href="#configuringautouploadingfromaemassets">Activado</a></p> <p>(Véase el paso 4)</p> </td>
    </tr>
    </tbody>
    </table>

1. (Opcional; consulte tabla de casos de uso): Configure la [configuración de nube de Dynamic Media](/help/assets/config-dynamic.md) y [habilite el servidor de Dynamic Media](/help/assets/config-dynamic.md).
1. (Opcional; consulte la tabla de casos de uso): Si elige habilitar la carga automática de Assets a Dynamic Media Classic, debe añadir lo siguiente:

   1. Configure la carga automática en Dynamic Media Classic.
   1. Añada el paso **Dynamic Media Classic upload** después de todos los pasos del flujo de trabajo de Dynamic Media *al final del flujo de trabajo* **Dam Update Asset** ( `https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`
   1. (Opcional) Restrinja la carga de recursos de Dynamic Media Classic por tipo MIME en [https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl). Los tipos MIME de recurso que no están en esta lista no se cargan en el servidor de Dynamic Media Classic.
   1. (Opcional) Configure el vídeo en la configuración de Dynamic Media Classic. Puede habilitar la codificación de vídeo para Dynamic Media o Dynamic Media Classic simultáneamente. Las representaciones dinámicas se utilizan para la vista previa y la reproducción localmente en la instancia de Experience Manager, mientras que las representaciones de vídeo de Dynamic Media Classic se generan y almacenan en los servidores de Dynamic Media Classic. Al configurar los servicios de codificación de vídeo tanto para Dynamic Media como para Dynamic Media Classic, aplique un [perfil de procesamiento de vídeo](/help/assets/video-profiles.md) a la carpeta de recursos de Dynamic Media Classic.
   1. (Opcional) [Configure la previsualización segura en Dynamic Media Classic](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene).

#### Restricciones     {#limitations}

Cuando tiene activados Dynamic Media Classic y Dynamic Media, existen las siguientes limitaciones:

* La carga manual en Dynamic Media Classic seleccionando un recurso y arrastrándolo a un componente de Dynamic Media Classic en una página de Experience Manager no funciona.
* Aunque los recursos sincronizados con Experience Manager y Dynamic Media Classic se actualizan automáticamente a Dynamic Media Classic cuando el recurso se edita en Assets, una acción de reversión no déclencheur una nueva carga. Como tal, Dynamic Media Classic no obtiene la última versión inmediatamente después de una reversión. La solución es volver a editarse una vez completada la reversión.
* ¿Es necesario utilizar Dynamic Media para un caso de uso e integración con Dynamic Media Classic para otro de modo que los recursos de Dynamic Media no interactúen con el sistema de Dynamic Media Classic? Si es así, no aplique la configuración de Dynamic Media Classic a la carpeta Dynamic Media. Además, no aplique la configuración de Dynamic Media (perfil de procesamiento) a una carpeta de Dynamic Media Classic.

## Prácticas recomendadas para integrar Dynamic Media Classic con Experience Manager {#best-practices-for-integrating-scene-with-aem}

Al integrar Dynamic Media Classic con Experience Manager, hay que seguir algunas prácticas recomendadas importantes en las siguientes áreas:

* Probar la integración
* Carga de recursos directamente desde Dynamic Media Classic recomendada para determinados escenarios

Consulte [limitaciones conocidas](#known-limitations-and-design-implications).

### Probar la integración {#test-driving-your-integration}

Adobe recomienda probar la integración haciendo que la carpeta raíz apunte solo a una subcarpeta en lugar de a toda una empresa.

>[!CAUTION]
>
>La importación de recursos desde una cuenta de empresa de Dynamic Media Classic existente puede tardar bastante en mostrarse en Experience Manager. Asegúrese de designar una carpeta en Dynamic Media Classic que no tenga demasiados recursos (por ejemplo, la carpeta raíz a menudo tiene demasiados recursos y puede bloquear el sistema).

### Cargar recursos de Recursos Experience Manager frente a Dynamic Media Classic {#uploading-assets-from-aem-assets-versus-from-scene}

Puede cargar recursos utilizando la funcionalidad Recursos (administración de recursos digitales) o accediendo a Dynamic Media Classic directamente en el Experience Manager a través del navegador de contenido de Dynamic Media Classic. El que elija dependerá de los siguientes factores:

* Los tipos de recursos de Dynamic Media Classic que Experience Manager Assets aún no admite deben agregarse directamente a un sitio web de Experience Manager desde Dynamic Media Classic, a través del explorador de contenido de Dynamic Media Classic. Por ejemplo, plantillas de imagen.
* Para los tipos de recursos compatibles con Recursos Experience Manager y Dynamic Media Classic, decidir cómo cargarlos depende de lo siguiente:

   * Dónde están los activos hoy Y
   * La importancia de administrarlas en un repositorio común

Supongamos que los recursos ya están en Dynamic Media Classic y administrarlos en un repositorio común no es importante. Si ese es el caso, la exportación de los recursos a Recursos de Experience Manager solo para sincronizarlos de nuevo con Dynamic Media Classic para su envío es un viaje de ida y vuelta innecesario. Adobe recomienda mantener los recursos en un único repositorio y sincronizarlos con Dynamic Media Classic solo para su envío.

## Configuración de la integración con Dynamic Media Classic {#configuring-scene-integration}

Puede configurar el Experience Manager para cargar recursos en Dynamic Media Classic. Los recursos de una carpeta de destino de CQ se pueden cargar (automática o manualmente) de Experience Manager a una cuenta de empresa de Dynamic Media Classic.

>[!NOTE]
>
>Adobe recomienda usar solo la carpeta de destino designada para importar recursos de Dynamic Media Classic. Los recursos digitales que residen fuera de la carpeta de destino solo se pueden usar en componentes de Dynamic Media Classic en páginas en las que se ha habilitado la configuración de Dynamic Media Classic. Además, se colocan en una carpeta bajo demanda en Dynamic Media Classic. La carpeta bajo demanda no se sincroniza con el Experience Manager (pero los recursos se pueden descubrir en el navegador de contenido de Dynamic Media Classic).

**Para configurar Dynamic Media Classic para la integración con el Experience Manager:**

1. [Definir una configuración de nube](#creating-a-cloud-configuration-for-scene) : define la asignación entre una carpeta de Dynamic Media Classic y una carpeta de Assets. Complete este paso aunque solo desee sincronizar de forma unidireccional (Experience Manager Assets a Dynamic Media Classic).
1. [Habilite el Receptor de represas s7dam de  **Adobe CQ**](#enabling-the-adobe-cq-scene-dam-listener)  - Hecho en   OSGiconsole.
1. Si desea que Recursos Experience Manager se carguen automáticamente en Dynamic Media Classic, debe activar esa opción y agregar Dynamic Media Classic al flujo de trabajo [!UICONTROL Recurso de actualización de DAM]. También puede cargar recursos manualmente.
1. Adición de componentes de Dynamic Media Classic a la barra de tareas. Esta funcionalidad permite a los usuarios utilizar los componentes de Dynamic Media Classic en sus páginas de Experience Manager.
1. [Asigne la configuración a la página en Experience Manager](#enabling-scene-for-wcm) : este paso es necesario para ver los ajustes preestablecidos de vídeo que haya creado en Dynamic Media Classic. También es necesario si debe publicar un recurso desde fuera de la carpeta de destino de CQ en Dynamic Media Classic.

En esta sección se explica cómo realizar todos estos pasos y se enumeran las limitaciones importantes.

### Funcionamiento de la sincronización entre Dynamic Media Classic y Experience Manager Assets {#how-synchronization-between-scene-and-aem-assets-works}

Al configurar la sincronización de Experience Manager Assets y Dynamic Media Classic, es importante comprender lo siguiente:

#### Cargar a Dynamic Media Classic desde Experience Manager Assets {#uploading-to-scene-from-aem-assets}

* Hay una carpeta de sincronización designada en Experience Manager para las cargas de Dynamic Media Classic.
* Las cargas a Dynamic Media Classic se pueden automatizar si los recursos digitales se colocan en la carpeta de sincronización designada.
* La estructura de carpetas y subcarpetas de Experience Manager se duplica en Dynamic Media Classic.

>[!NOTE]
>
>Experience Manager incrusta todos los metadatos como XMP antes de cargarlos en Dynamic Media Classic, por lo que todas las propiedades del nodo de metadatos están disponibles en Dynamic Media Classic como XMP.

#### Limitaciones conocidas e implicaciones de diseño {#known-limitations-and-design-implications}

Con la sincronización entre Experience Manager Assets y Dynamic Media Classic, existen actualmente las siguientes limitaciones/implicaciones de diseño:

<table>
 <tbody>
  <tr>
   <td><strong>Implicación de limitación/diseño</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Una carpeta de sincronización designada (destino)</td>
   <td>Solo puede tener una carpeta designada por empresa en Experience Manager para las cargas de Dynamic Media Classic. Puede crear varias configuraciones si debe tener acceso a más de una cuenta de empresa en Dynamic Media Classic.</td>
  </tr>
  <tr>
   <td>Estructura de carpetas</td>
   <td>Si elimina una carpeta sincronizada con recursos, se eliminarán todos los recursos remotos de Dynamic Media Classic, pero la carpeta permanecerá.</td>
  </tr>
  <tr>
   <td>Carpeta bajo demanda</td>
   <td>Los recursos que residen fuera de la carpeta de destino y que se cargan manualmente en Dynamic Media Classic en WCM se colocan automáticamente en una carpeta independiente a petición en Dynamic Media Classic. Puede configurar esta carpeta en la configuración de nube en Experience Manager.</td>
  </tr>
  <tr>
   <td>Medios mixtos</td>
   <td>Los conjuntos de medios mixtos aparecen en el Experience Manager, aunque no son compatibles con el Experience Manager.</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>Los PDF generados a partir de catálogos electrónicos en Dynamic Media Classic se importan en la carpeta de destino de CQ.</td>
  </tr>
  <tr>
   <td>Actualización de la interfaz de usuario</td>
   <td>Al sincronizar entre Experience Manager y Dynamic Media Classic, asegúrese de actualizar la interfaz de usuario para ver los cambios. </td>
  </tr>
  <tr>
   <td>Miniaturas de vídeo</td>
   <td>Si se carga un vídeo en Recursos Experience Manager para su codificación mediante Dynamic Media Classic, las miniaturas de vídeo y los vídeos codificados pueden tardar algún tiempo en estar disponibles en Recursos Experience Manager, en función del tiempo de procesamiento del vídeo.</td>
  </tr>
  <tr>
   <td>Subcarpetas de destino</td>
   <td><p>Si utiliza subcarpetas dentro de la carpeta de destino, asegúrese de utilizar nombres únicos para cada recurso (independientemente de la ubicación). Además, asegúrese de configurar Dynamic Media Classic (en el área Configuración) para que no sobrescriba los recursos, independientemente de la ubicación.</p> <p>De lo contrario, se cargarán recursos con el mismo nombre que se carguen en una subcarpeta de destino de Dynamic Media Classic, pero se eliminará el recurso con el mismo nombre en la carpeta de destino. </p> </td>
  </tr>
 </tbody>
</table>

### Configuración de servidores de Dynamic Media Classic {#configuring-scene-servers}

Si ejecuta un Experience Manager detrás de un proxy o tiene una configuración especial del cortafuegos, debe habilitar explícitamente los hosts de las diferentes regiones. Los servidores se administran en contenido en `/etc/cloudservices/scene7/endpoints` y se pueden personalizar según sea necesario. Seleccione una URL y, a continuación, edite para cambiar la URL, si es necesario. En versiones anteriores de Experience Manager, estos valores estaban codificados.

Si va a `/etc/cloudservices/scene7/endpoints.html`, verá los servidores en la lista (y puede editarlos tocando la dirección URL):

![chlimage_1-296](assets/chlimage_1-296.png)

### Crear una configuración de nube para Dynamic Media Classic {#creating-a-cloud-configuration-for-scene}

Una configuración de nube define la asignación entre una carpeta de Dynamic Media Classic y una carpeta de recursos de Experience Manager. Debe configurarse para sincronizar Experience Manager Assets con Dynamic Media Classic. Consulte Funcionamiento de la sincronización para obtener más información.

>[!CAUTION]
>
>La importación de recursos desde una cuenta de empresa de Dynamic Media Classic existente puede tardar bastante en mostrarse en Experience Manager. Asegúrese de designar una carpeta en Dynamic Media Classic que no tenga demasiados recursos. Por ejemplo, la carpeta raíz suele tener demasiados recursos.
>
>Si desea probar la integración, haga que la carpeta raíz apunte solo a una subcarpeta, en lugar de a toda la empresa.

>[!NOTE]
>
>Puede tener varias configuraciones: una configuración de nube representa a un usuario de una empresa de Dynamic Media Classic. Si desea acceder a otras empresas o usuarios de Dynamic Media Classic, debe crear varias configuraciones.

**Para crear una configuración de nube para Dynamic Media Classic:**

1. Seleccione el icono del Experience Manager y vaya a **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]** para acceder a Adobe Dynamic Media Classic.

1. Seleccione **[!UICONTROL Configurar ahora]**.

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. En el campo **[!UICONTROL Title]** y, opcionalmente, en el campo **[!UICONTROL Name]**, introduzca la información apropiada. Seleccione **[!UICONTROL Crear]**.

   >[!NOTE]
   >
   >Al crear más configuraciones, se muestra el campo **[!UICONTROL configuración principal]**.
   >
   >**not** cambia la configuración principal. Cambiar la configuración principal puede romper la integración.

1. Introduzca la dirección de correo electrónico, la contraseña y la región de su cuenta de Dynamic Media Classic y seleccione **[!UICONTROL Connect to Dynamic Media Classic]**. Está conectado al servidor de Dynamic Media Classic y el cuadro de diálogo se amplía con más opciones.

1. Introduzca el nombre **[!UICONTROL Company]** y **[!UICONTROL Root Path]**. Esta información es el nombre del servidor publicado junto con cualquier ruta que desee especificar. Si no conoce el nombre del servidor publicado, en Dynamic Media Classic, vaya a **[!UICONTROL Configuración > Configuración de la aplicación]**).

   >[!NOTE]
   >
   >La ruta raíz de Dynamic Media Classic es la carpeta a la que se conecta el Experience Manager de carpetas de Dynamic Media Classic. Se puede reducir a una carpeta específica.

   >[!CAUTION]
   >
   >Según el tamaño de la carpeta de Dynamic Media Classic, la importación de una carpeta raíz puede tardar mucho tiempo. Además, los datos de Dynamic Media Classic podrían superar el almacenamiento del Experience Manager. Asegúrese de que está importando la carpeta correcta. La importación de demasiados datos puede detener el sistema.

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. Seleccione **[!UICONTROL OK]**. Experience Manager guarda la configuración.

>[!NOTE]
>
>Si está reconectando:
>
>* Al volver a conectarse a Dynamic Media Classic al publicar, restablecer la contraseña al publicar o volver a conectar no funciona (no es un problema en la instancia de autor).
>* Si modifica valores como región o nombre de empresa, debe volver a conectarse a Dynamic Media Classic. Si las opciones de configuración se han modificado pero no se han guardado, el Experience Manager indica erróneamente que la configuración es válida. Asegúrese de volver a conectarse.

>



### Habilitar el detector de represas de Adobe CQ Dynamic Media Classic {#enabling-the-adobe-cq-scene-dam-listener}

Habilite el Receptor de represas de Adobe CQ Dynamic Media Classic, que está deshabilitado de forma predeterminada.

**Para habilitar el Receptor de represas de Adobe CQ Dynamic Media Classic:**

1. Seleccione el icono [!UICONTROL Tools] y, a continuación, vaya a **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. En la consola web, vaya a **[!UICONTROL Adobe CQ Dynamic Media Classic Dam Listener]** y seleccione la casilla **[!UICONTROL Enabled]**.

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. Seleccione **[!UICONTROL Guardar]**.

### Añadir tiempo de espera configurable al flujo de trabajo de carga de Dynamic Media Classic {#adding-configurable-timeout-to-scene-upload-workflow}

Cuando se configura una instancia de Experience Manager para gestionar la codificación de vídeo mediante Dynamic Media Classic, de forma predeterminada, cualquier trabajo de carga supera el tiempo de espera de 35 minutos. Para dar cabida a trabajos de codificación de vídeo que pueden tardar más tiempo en ejecutarse, puede configurar esta configuración.

1. Vaya a **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**.

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. Cambie el número como desee en el campo **[!UICONTROL Tiempo de espera del trabajo activo]**. Se acepta cualquier número no negativo con la unidad de medida en segundos. De forma predeterminada, este número está establecido en 2100.

   >[!NOTE]
   >
   >Práctica recomendada: La mayoría de los recursos se introducen en cuestión de minutos como máximo (por ejemplo, imágenes). Sin embargo, en algunos casos (vídeos más grandes, por ejemplo), el valor de tiempo de espera aumenta a 7200 segundos (dos horas) para dar cabida a un tiempo de procesamiento largo. De lo contrario, este trabajo de carga de Dynamic Media Classic se marca como **[!UICONTROL UploadFailed]** en los metadatos de JCR (repositorio de contenido Java™).

1. Seleccione **[!UICONTROL Guardar]**.

### Carga automática desde recursos de Experience Manager {#autouploading-from-aem-assets}

A partir de Experience Manager 6.3.2, Experience Manager Assets está configurado para que cualquier recurso digital cargado se actualice a Dynamic Media Classic, si los recursos están en una carpeta de destino de CQ.

Cuando se añade un recurso a Recursos de Experience Manager, este se carga automáticamente y se publica en Dynamic Media Classic.

>[!NOTE]
>
>El tamaño máximo de archivo para la carga automática de recursos de Experience Manager a Dynamic Media Classic es de 500 MB.

**Para cargar automáticamente desde recursos de Experience Manager:**

1. Seleccione el icono del Experience Manager y vaya a **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]**.
1. En el encabezado Dynamic Media, en Configuraciones disponibles, seleccione **[!UICONTROL dms7 (Dynamic Media]**).
1. Seleccione la pestaña **[!UICONTROL Avanzado]**, seleccione la casilla de verificación **[!UICONTROL Habilitar carga automática]** y, a continuación, seleccione **[!UICONTROL Aceptar]**. Ahora debe configurar el flujo de trabajo de DAM Asset para que incluya la carga en Dynamic Media Classic.

   >[!NOTE]
   >
   >Consulte [Configuración del estado (publicado/no publicado) de los recursos insertados en Dynamic Media Classic](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene) para obtener información sobre cómo insertar recursos en Dynamic Media Classic en un estado no publicado.

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. Vuelva a la página de bienvenida del Experience Manager y seleccione **[!UICONTROL Flujos de trabajo]**. Haga doble clic en el flujo de trabajo **DAM Update Asset** para que se abra.
1. En la barra de tareas, vaya a los componentes **[!UICONTROL Workflow]** y seleccione **[!UICONTROL Dynamic Media Classic]**. Arrastre **[!UICONTROL Dynamic Media Classic]** al flujo de trabajo y seleccione **[!UICONTROL Guardar]**. Los recursos añadidos a Recursos de Experience Manager en la carpeta de destino se cargan automáticamente en Dynamic Media Classic.

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* Al añadir recursos después de la automatización, si no se colocan en la carpeta de destino de CQ, no se cargan en Dynamic Media Classic.
   >* Experience Manager incrusta todos los metadatos como XMP antes de cargarlos en Dynamic Media Classic, por lo que todas las propiedades del nodo de metadatos están disponibles en Dynamic Media Classic como XMP.


### Configurar el estado (publicado/no publicado) de los recursos insertados en Dynamic Media Classic {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

Si va a insertar recursos de Recursos Experience Manager en Dynamic Media Classic, puede publicarlos automáticamente (comportamiento predeterminado) o colocarlos en Dynamic Media Classic sin publicar.

Es posible que no desee publicar recursos inmediatamente en Dynamic Media Classic si desea probarlos en un entorno de ensayo antes de publicarlos. Puede utilizar Experience Manager con el entorno Secure Test de Dynamic Media Classic para insertar recursos directamente de Assets en Dynamic Media Classic en un estado no publicado.

Los recursos de Dynamic Media Classic siguen estando disponibles mediante una vista previa segura. Solo cuando los recursos se publican en Experience Manager, los recursos de Dynamic Media Classic también se activan en producción.

Si desea publicar recursos inmediatamente al insertarlos en Dynamic Media Classic, no es necesario configurar ninguna opción. Esta funcionalidad es el comportamiento predeterminado.

Sin embargo, si no desea que los recursos insertados en Dynamic Media Classic se publiquen automáticamente, en esta sección se describe cómo configurar Experience Manager y Dynamic Media Classic para que realicen esta funcionalidad.

#### Requisitos previos para insertar recursos en Dynamic Media Classic sin publicar {#prerequisites-to-push-assets-to-scene-unpublished}

Para insertar recursos en Dynamic Media Classic sin publicarlos, debe configurar lo siguiente:

1. [Utilice el Admin Console para crear un caso](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) de asistencia. En su caso de asistencia, solicite la activación de la vista previa segura para su cuenta de Dynamic Media Classic.
1. [Configure la vista previa segura para su cuenta](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en) de Dynamic Media Classic.

Estos pasos son los mismos que seguiría para crear cualquier configuración de prueba segura en Dynamic Media Classic.

>[!NOTE]
>
>Si su entorno de instalación es un sistema operativo UNIX® de 64 bits, consulte [https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) acerca de otras opciones de configuración que debe configurar.

#### Limitaciones conocidas para insertar recursos en un estado no publicado  {#known-limitations-for-pushing-assets-in-unpublished-state}

Si utiliza esta función, tenga en cuenta las siguientes limitaciones:

* No se admite el control de versiones.
* Si un recurso ya está publicado en Experience Manager y se crea una versión posterior, esa nueva versión se publica inmediatamente en directo en producción. Publicar tras la activación solo funciona con la publicación inicial de un recurso.

>[!NOTE]
>
>Si desea publicar recursos instantáneamente, se recomienda mantener **[!UICONTROL Habilitar vista previa segura]** establecido en **[!UICONTROL Inmediatamente]** y utilizar la función **[!UICONTROL Habilitar carga automática]**.

### Establecer el estado de los recursos insertados en Dynamic Media Classic como no publicados {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>Si un usuario publica el recurso en Experience Manager, automáticamente lo déclencheur al recurso S7 en producción/activo (el recurso ya no está en vista previa segura/sin publicar).

**Para establecer el estado de los recursos insertados en Dynamic Media Classic como no publicados:**

1. Seleccione el icono del Experience Manager y vaya a **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]**.
1. Seleccione **[!UICONTROL Dynamic Media Classic]**.
1. Seleccione la configuración en Dynamic Media Classic.
1. Seleccione la pestaña **[!UICONTROL Advanced]**.
1. En el menú desplegable **[!UICONTROL Habilitar vista segura]**, seleccione **[!UICONTROL Al activar AEM Publish]** para insertar recursos en Dynamic Media Classic sin publicarlos. (De forma predeterminada, este valor se establece en **[!UICONTROL Inmediatamente]**, donde los recursos de Dynamic Media Classic se publican inmediatamente).

   Consulte la [documentación de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html) para obtener más información sobre cómo probar los recursos antes de hacerlos públicos.

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. Seleccione **[!UICONTROL OK]**.

Habilitar la vista previa segura significa que los recursos se insertan en el servidor de vista previa seguro sin publicar.

Para ver si **[!UICONTROL Secure Preview]** está habilitado, vaya a un componente de Dynamic Media Classic en una página de Experience Manager. Seleccione **[!UICONTROL Editar]**. El recurso tiene el servidor de vista previa seguro enumerado en la dirección URL. Después de publicar en el Experience Manager, el dominio del servidor en la referencia del archivo se actualiza de la dirección URL de vista previa a la URL de producción.

### Habilitar Dynamic Media Classic para WCM {#enabling-scene-for-wcm}

La activación de Dynamic Media Classic para WCM es necesaria por dos motivos:

* Habilita la lista desplegable de perfiles de vídeo universales para la creación de páginas. Sin esta lista, la lista desplegable **[!UICONTROL Ajuste preestablecido de vídeo universal]** está vacía y no se puede establecer.
* Si un recurso digital no está en la carpeta de destino, puede cargarlo en Dynamic Media Classic si activa Dynamic Media Classic para esa página en las propiedades de la página. A continuación, arrastre y suelte el recurso en un componente de Dynamic Media Classic. Se aplican reglas de herencia normales (lo que significa que las páginas secundarias heredan la configuración de la página principal).

Al habilitar Dynamic Media Classic para WCM, al igual que con otras configuraciones, se aplican las reglas de herencia. Puede activar Dynamic Media Classic para WCM en la interfaz de usuario táctil o clásica.

#### Habilitar Dynamic Media Classic para WCM en la interfaz de usuario táctil {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

1. Seleccione el icono del Experience Manager y vaya a **[!UICONTROL Sites]** y, a continuación, a la página raíz del sitio web (no específica del idioma).

1. En la barra de herramientas, seleccione el icono [!UICONTROL settings] y seleccione **[!UICONTROL Abrir propiedades]**.

1. Seleccione **[!UICONTROL Cloud Services]**, **[!UICONTROL Agregar configuración]** y seleccione **[!UICONTROL Dynamic Media Classic]**.
1. En la lista desplegable **[!UICONTROL Adobe Dynamic Media Classic]**, seleccione la configuración que desee y seleccione **[!UICONTROL Aceptar]**.

   ![chlimage_1-303](assets/chlimage_1-303.png)

   Los ajustes preestablecidos de vídeo de esa configuración de Dynamic Media Classic están disponibles para su uso en Experience Manager con el componente de vídeo de Dynamic Media Classic en esa página y en las páginas secundarias.

#### Habilitar Dynamic Media Classic para WCM en la interfaz de usuario clásica {#enabling-scene-for-wcm-in-the-classic-user-interface}

1. En el Experience Manager, seleccione **[!UICONTROL Sitios web]** y vaya a la página raíz del sitio web (no específica del idioma).

1. En la barra de tareas, seleccione el icono **[!UICONTROL Página]** y seleccione **[!UICONTROL Propiedades de página]**.

1. Seleccione **[!UICONTROL Cloud Services]** > **[!UICONTROL Agregar servicios]** > **[!UICONTROL Dynamic Media Classic]**.
1. En la lista desplegable **[!UICONTROL Adobe Dynamic Media Classic]**, seleccione la configuración que desee y seleccione **[!UICONTROL Aceptar]**.

   Los ajustes preestablecidos de vídeo de esa configuración de Dynamic Media Classic están disponibles para su uso en Experience Manager con el componente de vídeo de Dynamic Media Classic en esa página y en las páginas secundarias.

### Configuración predeterminada {#configuring-a-default-configuration}

Si tiene varias configuraciones de Dynamic Media Classic, puede especificar una de ellas como la predeterminada para el explorador de contenido de Dynamic Media Classic.

En un momento determinado, solo se puede marcar como predeterminada una configuración de Dynamic Media Classic. La configuración predeterminada son los recursos de la empresa que se muestran de forma predeterminada en el navegador de contenido de Dynamic Media Classic.

**Para configurar una configuración predeterminada:**

1. Seleccione el icono del Experience Manager y vaya a **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]**.
1. Seleccione **[!UICONTROL Dynamic Media Classic]**.
1. Seleccione la configuración en Dynamic Media Classic.
1. Para abrir la configuración, seleccione **[!UICONTROL Editar]**.

1. En la pestaña **[!UICONTROL General]**, seleccione la casilla de verificación **[!UICONTROL Configuración predeterminada]** para que sea la empresa predeterminada y la ruta raíz que aparece en el explorador de contenido de Dynamic Media Classic.

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >Si solo hay una configuración, seleccionar la casilla **[!UICONTROL Configuración predeterminada]** no tiene ningún efecto.

### Configuración de la carpeta Ad Hoc {#configuring-the-ad-hoc-folder}

Puede configurar la carpeta bajo demanda en la que se cargan los recursos en Dynamic Media Classic cuando el recurso no está en la carpeta de destino de CQ. Consulte Publicación de recursos desde fuera de la carpeta de destino de CQ.

**Para configurar la carpeta Ad Hoc:**

1. Seleccione el icono del Experience Manager y vaya a **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]**.
1. Seleccione **[!UICONTROL Dynamic Media Classic]**.
1. Seleccione la configuración en Dynamic Media Classic.
1. Para abrir la configuración, seleccione **[!UICONTROL Editar]**.

1. Seleccione la pestaña **[!UICONTROL Advanced]**. En el campo **[!UICONTROL Carpeta ad hoc]**, puede modificar la carpeta **Ad-hoc**. De forma predeterminada, es **name_of_the_company/CQ5_adhoc**.

   ![chlimage_1-305](assets/chlimage_1-305.png)

### Configuración de ajustes preestablecidos de vídeo universales {#configuring-universal-presets}

Para configurar los ajustes preestablecidos de vídeo universales para el componente de vídeo, consulte [Vídeo](/help/assets/s7-video.md).

## Habilitación de la compatibilidad con los parámetros de trabajo de carga de recursos basados en tipos MIME/Dynamic Media Classic {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

Puede habilitar los parámetros configurables de trabajos de carga de Dynamic Media Classic que se activan mediante la sincronización de recursos de Digital Asset Manager/Dynamic Media Classic.

Específicamente, se configura el formato de archivo aceptado por tipo MIME en el área OSGi (Open Service Gateway Initiative) del panel Configuración de la consola web del Experience Manager. A continuación, puede personalizar los parámetros individuales del trabajo de carga que se utilizan para cada tipo MIME en el JCR (repositorio de contenido Java™).

**Para habilitar recursos basados en tipos MIME:**

1. Seleccione el icono del Experience Manager y vaya a **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. En el panel Configuración de la consola web de Adobe Experience Manager, en el menú **[!UICONTROL OSGi]**, seleccione **[!UICONTROL Configuración]**.
1. En la columna Nombre , busque y seleccione **[!UICONTROL Adobe CQ Dynamic Media Classic Asset MIME type Service]** para editar la configuración.
1. En el área Asignación de tipo de MIME , seleccione cualquier signo más (+) para agregar un tipo MIME.

   Consulte [Tipos MIME admitidos](/help/assets/assets-formats.md#supported-mime-types).

1. En el campo de texto, escriba el nuevo nombre de tipo MIME.

   Por ejemplo, escribiría `<file_extension>=<mime_type>` como en `EPS=application/postscript` O `PSD=image/vnd.adobe.photoshop`.

1. En la esquina inferior derecha de la ventana de configuración, seleccione **[!UICONTROL Save]**.
1. Vuelva al Experience Manager y, en el carril izquierdo, seleccione **[!UICONTROL CRXDE Lite]**.
1. En la página CRXDE Lite, en el carril izquierdo, vaya a `/etc/cloudservices/scene7/<environment>` (reemplace `<environment>` por el nombre real).
1. Expanda `<environment>` (reemplace `<environment>` por el nombre real) para mostrar el nodo `mimeTypes`.
1. Seleccione el mimeType que acaba de añadir.

   Por ejemplo, `mimeTypes > application_postscript` O `mimeTypes > image_vnd.adobe.photoshop`.

1. En el lado derecho de la página CRXDE Lite, seleccione la pestaña **[!UICONTROL Properties]**.
1. Especifique un parámetro de trabajo de carga de Dynamic Media Classic en el campo de valor **[!UICONTROL jobParam]** .

   Por ejemplo, `psprocess="rasterize"&psresolution=120` .

   Consulte la [API del sistema de producción de imágenes Dynamic Media Classic de Adobe](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html) para obtener más parámetros de trabajo de carga que pueda utilizar.

   >[!NOTE]
   >
   >Si está cargando archivos PSD y desea procesarlos como plantillas con extracciones de capas, introduzca lo siguiente en el campo de valor **[!UICONTROL jobParam]** :
   >
   >`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`
   >
   >Asegúrese de que el archivo PSD tenga &quot;capas&quot;. Si es estrictamente una imagen o una imagen con máscara, se procesa como una imagen porque no hay capas para procesar.

1. En la esquina superior izquierda de la página CRXDE Lite, seleccione **[!UICONTROL Guardar todo]**.

## Resolución de problemas de integración de Dynamic Media Classic y Experience Manager {#troubleshooting-scene-and-aem-integration}

Si tiene problemas para integrar Experience Manager con Dynamic Media Classic, consulte los siguientes escenarios para soluciones.

**Si la publicación de recursos digitales en Dynamic Media Classic falla:**

* Compruebe que el recurso que está cargando se encuentra en la carpeta **[!UICONTROL CQ target]** (especifica esta carpeta en la configuración de nube de Dynamic Media Classic).
* Si no es así, debe configurar la configuración de nube en **[!UICONTROL Propiedades de página]** para esa página a fin de permitir la carga en la carpeta **[!UICONTROL CQ ad hoc]**.

* Compruebe los registros para obtener información.

**Si no aparecen los ajustes preestablecidos de vídeo:**

* Asegúrese de haber configurado la configuración de nube de esa página a través de **[!UICONTROL Propiedades de página]**. Los ajustes preestablecidos de vídeo están disponibles en el componente de vídeo de Dynamic Media Classic.

**Si los recursos de vídeo no se reproducen en el Experience Manager:**

* Asegúrese de que ha utilizado el componente de vídeo correcto. El componente de vídeo de Dynamic Media Classic es diferente del componente de vídeo base. Consulte [Componente de vídeo base frente a Componente de vídeo clásico de Dynamic Media](/help/assets/s7-video.md).

**Si los recursos nuevos o modificados en Experience Manager no se cargan automáticamente en Dynamic Media Classic:**

* Asegúrese de que los recursos están en la carpeta de destino de CQ. Solo se actualizan automáticamente los recursos que se encuentran en la carpeta de destino de CQ (siempre que haya configurado Recursos de Experience Manager para cargar recursos automáticamente).
* Asegúrese de haber configurado la configuración de Cloud Services para Habilitar carga automática y de haber actualizado y guardado el flujo de trabajo de recursos DAM para incluir la carga de Dynamic Media Classic.
* Al cargar una imagen en una subcarpeta de la carpeta de destino de Dynamic Media Classic, asegúrese de realizar una de las siguientes acciones:

   * Asegúrese de que los nombres de todos los recursos, independientemente de la ubicación, sean únicos. De lo contrario, el recurso de la carpeta de destino principal se elimina y solo permanece el recurso de la subcarpeta.
   * Cambie el modo en que Dynamic Media Classic sobrescribe los recursos en el área Configuración de la cuenta de Dynamic Media Classic . No configure Dynamic Media Classic para sobrescribir recursos independientemente de la ubicación si utiliza recursos con el mismo nombre en subcarpetas.

**Si los recursos o carpetas eliminados no están sincronizados entre Dynamic Media Classic y Experience Manager:**

* Los recursos y carpetas eliminados en Recursos de Experience Manager siguen apareciendo en la carpeta sincronizada de Dynamic Media Classic. Eliminarlos manualmente.

**Si falla la carga de vídeo:**

* Si la carga de vídeo falla y utiliza un Experience Manager para codificar vídeo a través de la integración de Dynamic Media Classic, consulte [Añadir un tiempo de espera configurable al flujo de trabajo de carga de Dynamic Media Classic](#adding-configurable-timeout-to-scene-upload-workflow).

>[!CAUTION]
>
>La importación de recursos desde una cuenta de empresa de Dynamic Media Classic existente puede tardar bastante en mostrarse en Experience Manager. Asegúrese de designar una carpeta en Dynamic Media Classic que no tenga demasiados recursos. Por ejemplo, la carpeta raíz suele tener demasiados recursos.
>
>Si desea probar la integración, haga que la carpeta raíz apunte solo a una subcarpeta, en lugar de a toda la empresa.
