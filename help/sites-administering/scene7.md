---
title: Integración con Dynamic Media Classic (Scene7)
seo-title: Integración con Dynamic Media Classic (Scene7)
description: Aprenda a integrar AEM con Dynamic Media Classic.
seo-description: Aprenda a integrar AEM con Dynamic Media Classic.
uuid: b014d643-1cc1-47f3-a79c-7f6f9e45637a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: f55e68c3-3309-4400-bef9-fd3afa6e2b5f
translation-type: tm+mt
source-git-commit: e95f26cc1a084358b6bcb78605e3acb98f257b66
workflow-type: tm+mt
source-wordcount: '5485'
ht-degree: 1%

---


# Integración con Dynamic Media Classic (Scene7){#integrating-with-dynamic-media-classic-scene}

[Adobe Dynamic Media ](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) Classicis es una solución alojada para administrar, mejorar, publicar y distribuir recursos de medios enriquecidos en pantallas e impresiones web, móviles, de correo electrónico y conectadas a Internet.

Para utilizar Dynamic Media Classic, debe configurar la configuración de nube para que Dynamic Media Classic y AEM Assets puedan interactuar entre sí. Este documento describe cómo configurar AEM y Dynamic Media Classic.

Para obtener información sobre el uso de todos los componentes de Dynamic Media Classic en una página y el trabajo con vídeo, consulte [Uso de Dynamic Media Classic](../assets/scene7.md).

>[!NOTE]
>
>* La plataforma de visor DHTML de Dynamic Media Classic llegó oficialmente al final de su vida útil el 31 de enero de 2014. Para obtener más información, consulte las [preguntas más frecuentes sobre el final de la vida útil del visor DHTML](../sites-administering/dhtml-viewer-endoflifefaqs.md).
>* Antes de configurar Dynamic Media Classic para que funcione con AEM, consulte [Prácticas recomendadas](#best-practices-for-integrating-scene-with-aem) para integrar Dynamic Media Classic con AEM.
>* Si utiliza Dynamic Media Classic con una configuración proxy personalizada, debe configurar ambas configuraciones proxy del cliente HTTP, ya que algunas funcionalidades de AEM utilizan las API 3.x y otras las API 4.x. 3.x está configurado con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) y 4.x está configurado con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator).

>



## Integración AEM/Dynamic Media Classic frente a Dynamic Media {#aem-scene-integration-versus-dynamic-media}

AEM usuarios pueden elegir entre dos soluciones para trabajar con medios dinámicos: Integrar su instancia de AEM con Dynamic Media Classic o utilizar la solución Dynamic Media integrada en AEM.

Utilice los siguientes criterios para determinar qué solución elegir:

* Si es **cliente existente** de Dynamic Media Classic cuyos recursos de medios enriquecidos residen en Dynamic Media Classic para publicación y envío, pero desea integrar esos recursos con la creación de sitios (WCM) o AEM Assets para administración, utilice la [integración punto a punto de AEM/Dynamic Media Classic](#aem-scene-point-to-point-integration) que se describe en este documento.

* Si es un **cliente nuevo** AEM que tiene necesidades de envío de medios enriquecidos, seleccione la [opción de Dynamic Media](#aem-dynamic-media). Esta opción tiene el mayor sentido si no tiene una cuenta S7 existente y muchos recursos almacenados en ese sistema.

* En algunos casos, es posible que desee utilizar ambas soluciones. El [escenario de doble uso](/help/sites-administering/scene7.md#dual-use-scenario) describe ese escenario.

### Integración punto a punto de AEM/Dynamic Media Classic {#aem-scene-point-to-point-integration}

Cuando se trabaja con recursos en esta solución, se realiza una de las siguientes acciones:

* Cargue recursos directamente en Dynamic Media Classic y, a continuación, acceda a ellos mediante el navegador de contenido **Dynamic Media Classic** para la creación de páginas o
* Cargue en AEM Assets y, a continuación, active la publicación automática en Dynamic Media Classic; se accede a través del navegador de contenido **Assets** para la creación de páginas

Los componentes que utiliza para esta integración se encuentran en el área del componente **Dynamic Media Classic** en el modo [Diseño.](/help/sites-authoring/author-environment-tools.md#page-modes)

### AEM Dynamic Media {#aem-dynamic-media}

AEM Dynamic Media es la unificación de las funciones de Dynamic Media Classic directamente dentro de la plataforma AEM.

Cuando trabaje con recursos en esta solución, siga este flujo de trabajo:

1. Cargue recursos de imagen y vídeo individuales directamente en AEM.
1. Codifique los vídeos directamente en AEM.
1. Cree conjuntos basados en imágenes directamente dentro de AEM.
1. Si corresponde, agregue interactividad a imágenes o vídeos.

Los componentes que utiliza para Dynamic Media se encuentran en el área del componente **[!UICONTROL Dynamic Media]** en [modo de diseño](/help/sites-authoring/author-environment-tools.md#page-modes). Incluyen lo siguiente:

* **[!UICONTROL Dynamic Media]** : el  **[!UICONTROL componente]** Mediacomponent dinámico es inteligente, ya que, dependiendo de si agrega una imagen o un vídeo, tiene varias opciones. El componente admite ajustes preestablecidos de imagen, visores basados en imágenes, como conjuntos de imágenes, conjuntos de giros, conjuntos de medios mixtos y vídeo. Además, el visor es interactivo: el tamaño de la pantalla cambia automáticamente en función del tamaño de la pantalla. Todos los visores son visores HTML5.

* **[!UICONTROL Medios]**  interactivos: el componente  **[!UICONTROL interactivo de]** MediaPonent es para los recursos, como pancartas de carrusel, imágenes interactivas y vídeos interactivos, que tienen interactividad en ellos, como puntos interactivos o mapas de imágenes. Este componente es inteligente, ya que, dependiendo de si agrega una imagen o un vídeo, dispone de varias opciones. Además, el visor es interactivo: el tamaño de la pantalla cambia automáticamente en función del tamaño de la pantalla. Todos los visores son visores HTML5.

### Escenario de doble uso {#dual-use-scenario}

De forma predeterminada, puede utilizar las funciones de integración de Dynamic Media y Dynamic Media Classic de AEM simultáneamente. La tabla de casos de uso siguiente describe cuándo se activan y desactivan determinadas áreas.

Para utilizar Dynamic Media y Dynamic Media Classic simultáneamente:

1. Configure [Dynamic Media Classic](#creating-a-cloud-configuration-for-scene) en servicios en la nube.
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
    <td><strong>Si eres...</strong></td>
    <td><strong>Flujo de trabajo de caso de uso</strong></td>
    <td><strong>Imágenes/Vídeo</strong></td>
    <td><strong>Componente de Dynamic Media</strong></td>
    <td><strong>Navegador de contenido y componentes de S7</strong></td>
    <td><strong>Carga automática de recursos a S7</strong></td>
    </tr>
    <tr>
    <td>Nuevo en sitios y Dynamic Media</td>
    <td>Cargar recursos en AEM y utilizar AEM componente de Dynamic Media para crear recursos en páginas de sitios</td>
    <td><p>Activado</p> <p>(Consulte el paso 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Activado</a></td>
    <td>Desactivado</td>
    <td>Desactivado</td>
    </tr>
    <tr>
    <td>En el sector minorista y son nuevos en Sitios y Dynamic Media</td>
    <td>Cargue recursos que no sean de productos en AEM para su administración y envío. Cargue recursos del PRODUCTO en Dynamic Media Classic y utilice el navegador de contenido de Dynamic Media Classic en AEM y componentes para crear páginas de detalles del producto en sitios.</td>
    <td><p>Activado</p> <p>(Consulte el paso 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Activado</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Activado</a></td>
    <td>Desactivado</td>
    </tr>
    <tr>
    <td>Nuevo en Assets y Dynamic Media</td>
    <td>Cargar recursos en AEM Assets y usar la URL publicada/código incrustado de Dynamic Media</td>
    <td><p>Activado</p> <p>(Consulte el paso 3)</p> </td>
    <td>Desactivado</td>
    <td>Desactivado</td>
    <td>Desactivado</td>
    </tr>
    <tr>
    <td>Nuevo en Dynamic Media y plantilla</td>
    <td>Utilice Dynamic Media para imágenes y vídeos. Cree plantillas de imagen en Dynamic Media Classic y utilice el buscador de contenido de Dynamic Media Classic para incluir plantillas en las páginas Sitios.</td>
    <td><p>Activado</p> <p>(Consulte el paso 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Activado</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Activado</a></td>
    <td>Desactivado</td>
    </tr>
    <tr>
    <td>Un cliente de Dynamic Media Classic existente y es nuevo en Sitios</td>
    <td>Cargue recursos en Dynamic Media Classic y utilice AEM navegador de contenido de Dynamic Media Classic para buscar y crear recursos en páginas de sitios</td>
    <td>Desactivado</td>
    <td>Desactivado</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Activado</a></td>
    <td>Desactivado</td>
    </tr>
    <tr>
    <td>Un cliente de Dynamic Media Classic existente y es nuevo en Sitios y recursos</td>
    <td>Cargue recursos en DAM y publíquelos automáticamente en Dynamic Media Classic para envío. Utilice AEM navegador de contenido de Dynamic Media Classic para buscar y crear recursos en páginas de sitios.</td>
    <td>Desactivado</td>
    <td>Desactivado</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Activado</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">Activado</a></p> <p>(Consulte el paso 4)</p> </td>
    </tr>
    <tr>
    <td>Cliente existente de Dynamic Media Classic y nuevo en Assets</td>
    <td><p>Cargue recursos en AEM y utilice Dynamic Media para generar representaciones para descarga/uso compartido. Publicar automáticamente AEM recursos en Dynamic Media Classic para envío.</p> <p><strong>Importante:</strong> Incurre en que el procesamiento de duplicados y las representaciones generadas en AEM no se sincronizarán con Dynamic Media Classic</p> </td>
    <td><p>Activado</p> <p>(Consulte el paso 3)</p> </td>
    <td>Desactivado</td>
    <td>Desactivado</td>
    <td><p><a href="#configuringautouploadingfromaemassets">Activado</a></p> <p>(Consulte el paso 4)</p> </td>
    </tr>
    </tbody>
    </table>

1. (Opcional; consulte la tabla de casos de uso): configure la [configuración de nube de Dynamic Media](/help/assets/config-dynamic.md) y [habilite el servidor de Dynamic Media](/help/assets/config-dynamic.md).
1. (Opcional; consulte la tabla de casos de uso): si decide activar la carga automática de recursos a Dynamic Media Classic, deberá agregar lo siguiente:

   1. Configure la carga automática en Dynamic Media Classic.
   1. Añada el paso **carga de Dynamic Media Classic** después de todos los pasos del flujo de trabajo de Dynamic Media *al final del flujo de trabajo* **Recurso de actualización de presas** ( `https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`)
   1. (Opcional) Restrinja la carga de recursos de Dynamic Media Classic por tipo MIME en [https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl). Los tipos MIME de recurso que no estén en esta lista no se cargarán en el servidor de Dynamic Media Classic.
   1. (Opcional) Configure el vídeo en la configuración de Dynamic Media Classic. Puede activar la codificación de vídeo para Dynamic Media y Dynamic Media Classic simultáneamente o para ambos. Las representaciones dinámicas se utilizan para la previsualización y reproducción local en AEM instancia, mientras que las representaciones de vídeo de Dynamic Media Classic se generan y almacenan en los servidores de Dynamic Media Classic. Al configurar los servicios de codificación de vídeo tanto para Dynamic Media como para Dynamic Media Classic, aplique un [perfil de procesamiento de vídeo](/help/assets/video-profiles.md) a la carpeta de recursos de Dynamic Media Classic.
   1. (Opcional) [Configurar previsualización segura en Dynamic Media Classic](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene).

#### Restricciones     {#limitations}

Cuando tiene activados Dynamic Media Classic y Dynamic Media, existen las siguientes limitaciones:

* La carga manual a Dynamic Media Classic seleccionando un recurso y arrastrándolo a un componente de Dynamic Media Classic en una página AEM no funciona.
* Aunque los recursos sincronizados AEM-Dynamic Media Classic se actualizan automáticamente a Dynamic Media Classic cuando se edita el recurso en Recursos, una acción de reversión no activa una nueva carga, por lo tanto Dynamic Media Classic no obtendría la última versión inmediatamente después de una reversión. La solución consiste en volver a editarse una vez que se haya completado la reversión.
* Si necesita utilizar Dynamic Media para un caso de uso e integración con Dynamic Media Classic para otro caso de uso, de modo que los recursos de Dynamic Media no interactúen con el sistema Dynamic Media Classic, no aplique la configuración de Dynamic Media Classic a la carpeta Dynamic Media ni la configuración de Dynamic Media (perfil de procesamiento) a una carpeta Dynamic Media Classic.

## Prácticas recomendadas para integrar Dynamic Media Classic con AEM {#best-practices-for-integrating-scene-with-aem}

Al integrar Dynamic Media Classic con AEM, hay que observar algunas prácticas recomendadas importantes en las siguientes áreas:

* Probar la integración
* Se recomienda cargar recursos directamente desde Dynamic Media Classic en determinados casos

Consulte [limitaciones conocidas](#known-limitations-and-design-implications).

### Probar la integración {#test-driving-your-integration}

Adobe recomienda que realice una prueba de la integración haciendo que la carpeta raíz apunte a una subcarpeta en lugar de a una compañía entera.

>[!CAUTION]
>
>La importación de recursos desde una cuenta de compañía existente de Dynamic Media Classic puede tardar mucho tiempo en mostrarse en AEM. Asegúrese de designar una carpeta en Dynamic Media Classic que no tenga demasiados recursos (por ejemplo, la carpeta raíz tendrá con frecuencia demasiados recursos y podría bloquear el sistema).

### Carga de recursos desde AEM Assets en comparación con Dynamic Media Classic {#uploading-assets-from-aem-assets-versus-from-scene}

Puede cargar recursos utilizando la funcionalidad Recursos (administración de recursos digitales) o accediendo a Dynamic Media Classic directamente en AEM mediante el navegador de contenido de Dynamic Media Classic. El que elija dependerá de los siguientes factores:

* Los tipos de recursos de Dynamic Media Classic que AEM Assets aún no admite deben agregarse directamente a un sitio web de AEM desde Dynamic Media Classic mediante el navegador de contenido de Dynamic Media Classic, por ejemplo, plantillas de imagen.
* Para los tipos de recursos compatibles con AEM Assets y Dynamic Media Classic, la decisión de cargarlos depende de lo siguiente:

   * Dónde están los recursos hoy Y
   * La importancia de administrarlas en un repositorio común

Si los recursos ya están en Dynamic Media Classic y administrarlos en un repositorio común no es tan importante, exportarlos a AEM Assets solo para sincronizarlos de nuevo en Dynamic Media Classic para envío sería un viaje de ida y vuelta innecesario. De lo contrario, puede ser preferible mantener los recursos en un único repositorio y sincronizarlos con Dynamic Media Classic solo para envío.

## Configuración de la integración de Dynamic Media Classic {#configuring-scene-integration}

Puede configurar AEM para cargar recursos en Dynamic Media Classic. Los recursos de una carpeta de destinatario de CQ se pueden cargar (automática o manualmente) de AEM a una cuenta de compañía de Dynamic Media Classic.

>[!NOTE]
>
>Adobe recomienda utilizar únicamente la carpeta de destinatario designada para importar los recursos de Dynamic Media Classic. Los recursos digitales que residen fuera de la carpeta destinatario solo se pueden usar en componentes de Dynamic Media Classic en páginas en las que se ha activado la configuración de Dynamic Media Classic. Además, se colocan en una carpeta ad hoc de Dynamic Media Classic. La carpeta ad hoc no está sincronizada con AEM (pero los recursos se pueden detectar en el navegador de contenido de Dynamic Media Classic).

Para configurar Dynamic Media Classic para integrarlo con AEM, debe completar los siguientes pasos:

1. [Definir una configuración](#creating-a-cloud-configuration-for-scene)  de nube: define la asignación entre una carpeta de Dynamic Media Classic y una carpeta de recursos. Debe completar este paso aunque solo desee sincronizar unidireccionalmente (de AEM Assets a Dynamic Media Classic).
1. [Habilite el detector **de represas de**](#enabling-the-adobe-cq-scene-dam-listener) Adobe CQ s7dam - Hecho en   OSGiconsole.
1. Si desea que AEM recursos se carguen automáticamente a Dynamic Media Classic, debe activar esa opción y agregar Dynamic Media Classic al flujo de trabajo [!UICONTROL Recurso de actualización de DAM]. También puede cargar recursos manualmente.
1. Añadir componentes de Dynamic Media Classic en la barra de tareas. Esto permite a los usuarios utilizar componentes de Dynamic Media Classic en sus páginas AEM.
1. [Asigne la configuración a la página en AEM](#enabling-scene-for-wcm) : Este paso es necesario para realizar la vista de cualquier ajuste preestablecido de vídeo que haya creado en Dynamic Media Classic. También es necesario si necesita publicar un recurso desde fuera de la carpeta de destinatario de CQ en Dynamic Media Classic.

Esta sección trata cómo realizar todos estos pasos y listas importantes limitaciones.

### Cómo funciona la sincronización entre Dynamic Media Classic y AEM Assets {#how-synchronization-between-scene-and-aem-assets-works}

Al configurar la sincronización de AEM Assets y Dynamic Media Classic, es importante comprender lo siguiente:

#### Cargar a Dynamic Media Classic desde AEM Assets {#uploading-to-scene-from-aem-assets}

* Hay una carpeta de sincronización designada en AEM para las cargas de Dynamic Media Classic.
* Las cargas a Dynamic Media Classic se pueden automatizar si los recursos digitales se colocan en la carpeta de sincronización designada.
* La estructura de carpetas y subcarpetas de AEM se replica en Dynamic Media Classic.

>[!NOTE]
>
>AEM incrusta todos los metadatos como XMP antes de cargarlos en Dynamic Media Classic, por lo que todas las propiedades del nodo de metadatos están disponibles en Dynamic Media Classic como XMP.

#### Limitaciones conocidas e implicaciones de diseño {#known-limitations-and-design-implications}

Con la sincronización entre AEM Assets y Dynamic Media Classic, actualmente hay las siguientes limitaciones/implicaciones de diseño:

<table>
 <tbody>
  <tr>
   <td><strong>Implicación de limitaciones/diseño</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Una carpeta de sincronización (destinatario) designada</td>
   <td>Solo puede tener una carpeta designada por compañía en AEM para las cargas de Dynamic Media Classic. Puede crear varias configuraciones si necesita tener acceso a más de una cuenta de compañía en Dynamic Media Classic.</td>
  </tr>
  <tr>
   <td>Estructura de carpetas</td>
   <td>Si elimina una carpeta sincronizada con recursos, se eliminarán todos los recursos remotos de Dynamic Media Classic, pero la carpeta permanecerá.</td>
  </tr>
  <tr>
   <td>Carpeta ad-hoc</td>
   <td>Los recursos que residen fuera de la carpeta destinatario y que se cargan manualmente en Dynamic Media Classic en WCM se colocan automáticamente en una carpeta ad-hoc independiente en Dynamic Media Classic. Esto se configura en la configuración de la nube en AEM.</td>
  </tr>
  <tr>
   <td>Medios mixtos</td>
   <td>Los conjuntos de medios mixtos aparecen en AEM aunque no son compatibles con AEM.</td>
  </tr>
  <tr>
   <td>Archivos PDF</td>
   <td>Los archivos PDF generados a partir de catálogos electrónicos en Dynamic Media Classic se importan a la carpeta de destinatario de CQ.</td>
  </tr>
  <tr>
   <td>Actualización de la interfaz de usuario</td>
   <td>Al sincronizar entre AEM y Dynamic Media Classic, asegúrese de actualizar la interfaz de usuario para realizar cambios en la vista. </td>
  </tr>
  <tr>
   <td>Miniaturas de vídeo</td>
   <td>Si se carga un vídeo en AEM Assets para su codificación mediante Dynamic Media Classic, las miniaturas de vídeo y los vídeos codificados pueden tardar algún tiempo en estar disponibles en AEM Assets, según el tiempo de procesamiento del vídeo.</td>
  </tr>
  <tr>
   <td>Subcarpetas de destinatario</td>
   <td><p>Si utiliza subcarpetas dentro de la carpeta destinatario, asegúrese de utilizar nombres únicos para cada recurso (independientemente de la ubicación) o de configurar Dynamic Media Classic (en el área Configuración) para que no sobrescriba los recursos independientemente de la ubicación.</p> <p>De lo contrario, se cargarán los recursos con el mismo nombre que se cargan en una subcarpeta de destinatario de Dynamic Media Classic, pero se eliminará el recurso con el mismo nombre de la carpeta de destinatario. </p> </td>
  </tr>
 </tbody>
</table>

### Configuración de los servidores de Dynamic Media Classic {#configuring-scene-servers}

Si ejecuta AEM detrás de un proxy o tiene una configuración de firewall especial, es posible que deba habilitar explícitamente los hosts de las distintas regiones. Los servidores se administran en contenido en `/etc/cloudservices/scene7/endpoints` y se pueden personalizar según sea necesario. Toque una dirección URL y, a continuación, edítela para cambiar la dirección URL, si es necesario. En versiones anteriores de AEM, estos valores estaban codificados.

Si se desplaza a `/etc/cloudservices/scene7/endpoints.html`, verá los servidores enumerados (y puede editarlos haciendo clic en la dirección URL):

![chlimage_1-296](assets/chlimage_1-296.png)

### Creación de una configuración de nube para Dynamic Media Classic {#creating-a-cloud-configuration-for-scene}

Una configuración de nube define la asignación entre una carpeta de Dynamic Media Classic y una carpeta de AEM Assets. Debe configurarse para sincronizar AEM Assets con Dynamic Media Classic. Consulte Funcionamiento de la sincronización para obtener más información.

>[!CAUTION]
>
>La importación de recursos desde una cuenta de compañía existente de Dynamic Media Classic puede tardar mucho tiempo en mostrarse en AEM. Asegúrese de designar una carpeta en Dynamic Media Classic que no tenga demasiados recursos (por ejemplo, la carpeta raíz tendrá con frecuencia demasiados recursos).
>
>Si desea probar la unidad de integración, puede que desee que la carpeta raíz apunte solo a una subcarpeta, en lugar de a toda la compañía.

>[!NOTE]
>
>Puede tener varias configuraciones: una configuración de nube representa a un usuario en una compañía de Dynamic Media Classic. Si desea acceder a otras compañías o usuarios de Dynamic Media Classic, debe crear varias configuraciones.

Para configurar AEM para poder publicar recursos en Dynamic Media Classic:

1. Toque el icono de AEM y vaya a **[!UICONTROL Implementación > Cloud Services]** para acceder a Adobe Dynamic Media Classic.

1. Toque **[!UICONTROL Configurar ahora.]**

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. En el campo **[!UICONTROL Título]** y, opcionalmente, en el campo **[!UICONTROL Nombre]**, introduzca la información adecuada. Toque **[!UICONTROL Crear.]**

   >[!NOTE]
   >
   >Al crear configuraciones adicionales, se muestra el campo **[!UICONTROL configuración principal]**.
   >
   >**no** cambia la configuración principal. Cambiar la configuración principal puede dañar la integración.

1. Introduzca la dirección de correo electrónico, la contraseña y la región de su cuenta de Dynamic Media Classic y toque **[!UICONTROL Conectar con Dynamic Media Classic.]** Está conectado al servidor de Dynamic Media Classic y el cuadro de diálogo se expande con más opciones.

1. Escriba el nombre **[!UICONTROL Compañía]** y **[!UICONTROL Ruta de raíz]** (es el nombre del servidor publicado junto con cualquier ruta que desee especificar; si no conoce el nombre del servidor publicado, en Dynamic Media Classic, vaya a **[!UICONTROL Ajustes > Ajustes de aplicación.]**)

   >[!NOTE]
   >
   >La ruta raíz de Dynamic Media Classic es la carpeta a la que AEM conecta Dynamic Media Classic. Se puede reducir a una carpeta específica.

   >[!CAUTION]
   >
   >Según el tamaño de la carpeta Dynamic Media Classic, la importación de una carpeta raíz puede tardar mucho tiempo. Además, los datos de Dynamic Media Classic podrían superar el almacenamiento de AEM. Asegúrese de que está importando la carpeta correcta. La importación de demasiados datos puede detener el sistema.

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. Haga clic en **[!UICONTROL Aceptar.]** AEM guarda la configuración.

>[!NOTE]
>
>Si está reconectando:
>
>* Al volver a conectarse a Dynamic Media Classic al realizar la publicación, es posible que tenga que restablecer la contraseña al publicar o que la reconexión no funcione. No se trata de un problema en la instancia de creación.
>* Si modifica valores como la región, el nombre de la compañía, debe volver a conectarse a Dynamic Media Classic. Si las opciones de configuración se han modificado pero no se han guardado, AEM erróneamente indica que la configuración es válida. Asegúrese de volver a conectarse.

>



### Activación del detector de presas Dynamic Media Classic de Adobe CQ {#enabling-the-adobe-cq-scene-dam-listener}

Debe habilitar el detector de presas Dynamic Media Classic de Adobe CQ, que está deshabilitado de forma predeterminada.

Para habilitarlo:

1. Toque el icono [!UICONTROL Herramientas] y luego vaya a **[!UICONTROL Operaciones > Consola Web.]** Se abre la consola Web.
1. Vaya a **[!UICONTROL Adobe CQ Classic Dam Listener]** y seleccione la casilla de verificación **[!UICONTROL Enabled]**.

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. Toque **[!UICONTROL Guardar.]**

### Añadir el tiempo de espera configurable al flujo de trabajo de carga de Dynamic Media Classic {#adding-configurable-timeout-to-scene-upload-workflow}

Cuando se configura una instancia de AEM para gestionar la codificación de vídeo a través de Dynamic Media Classic (Scene7), de forma predeterminada, se agota el tiempo de espera de 35 minutos en cualquier trabajo de carga. Para dar cabida a trabajos de codificación de vídeo potencialmente más largos, puede configurar esta configuración:

1. Vaya a **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**.

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. Cambie el número como desee en el campo **[!UICONTROL Tiempo de espera de trabajo activo]**. Se acepta cualquier número no negativo con la unidad de medida en segundos. De forma predeterminada, se establece en 2100.

   >[!NOTE]
   >
   >Práctica recomendada: La mayoría de los recursos se ingieren en minutos como máximo (por ejemplo, imágenes). Pero en algunos casos (por ejemplo, vídeos más grandes), el valor de tiempo de espera debe aumentarse a 7200 segundos (2 horas) para dar cabida a un tiempo de procesamiento prolongado. De lo contrario, este trabajo de carga de Dynamic Media Classic se marca como **[!UICONTROL UploadFailed]** en los metadatos de JCR.

1. Toque **[!UICONTROL Guardar.]**

### Carga automática desde AEM Assets {#autouploading-from-aem-assets}

A partir de AEM 6.3.2, AEM Assets se ha configurado para que todos los recursos digitales que cargue en el administrador de recursos digitales se actualicen automáticamente a Dynamic Media Classic si los recursos están en una carpeta de destinatario de CQ.

Cuando se agrega un recurso a AEM Assets, se carga y publica automáticamente en Dynamic Media Classic.

>[!NOTE]
>
>El tamaño máximo de archivo para la carga automática de AEM Assets a Dynamic Media Classic es de 500 MB.

Para configurar la carga automática desde AEM Assets:

1. Toque el icono de AEM y vaya a **[!UICONTROL Implementación > Cloud Services]** y, a continuación, en el encabezado de Dynamic Media, en Configuraciones disponibles, toque **[!UICONTROL dms7 (Dynamic Media]**)
1. Toque la ficha **[!UICONTROL Avanzado]**, seleccione la casilla de verificación **[!UICONTROL Habilitar carga automática]** y luego toque **[!UICONTROL Aceptar.]** Ahora debe configurar el flujo de trabajo de recursos DAM para incluir la carga en Dynamic Media Classic.

   >[!NOTE]
   >
   >Consulte [Configuración del estado (publicado/sin publicar) de los recursos insertados en Dynamic Media Classic](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene) para obtener información sobre cómo insertar recursos en Dynamic Media Classic en un estado sin publicar.

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. Vuelva a la página de bienvenida de AEM y toque **[!UICONTROL Flujos de trabajo.]** Haga clic con el botón doble en el flujo de trabajo  **de recursos de actualización de** DAM para abrirlo.
1. En la barra de tareas, vaya a los componentes **[!UICONTROL Workflow]** y seleccione **[!UICONTROL Dynamic Media Classic.]** Arrastre  **[!UICONTROL Dynamic Media]** Classic al flujo de trabajo y toque  **[!UICONTROL Guardar.]** Los recursos añadidos a AEM Assets en la carpeta destinatario se cargarán automáticamente en Dynamic Media Classic.

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* Al agregar recursos después de la automatización, si no se colocan en la carpeta de destinatario de CQ, no se cargan en Dynamic Media Classic.
   >* AEM incrusta todos los metadatos como XMP antes de cargarlos en Dynamic Media Classic, por lo que todas las propiedades del nodo de metadatos están disponibles en Dynamic Media Classic como XMP.


### Configuración del estado (publicado/no publicado) de los recursos insertados en Dynamic Media Classic {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

Si va a transferir recursos de AEM Assets a Dynamic Media Classic, puede publicarlos automáticamente (comportamiento predeterminado) o insertarlos en Dynamic Media Classic en un estado sin publicar.

Es posible que no desee publicar recursos inmediatamente en Dynamic Media Classic si desea probarlos en un entorno de ensayo antes de activarlos. Puede utilizar AEM con el entorno Secure Test de Dynamic Media Classic para insertar recursos directamente desde Assets en Dynamic Media Classic en un estado sin publicar.

Los recursos de Dynamic Media Classic siguen disponibles mediante previsualización segura. Los recursos de Dynamic Media Classic solo se activan en la producción cuando se publican en AEM.

Si desea publicar recursos inmediatamente al impulsarlos a Dynamic Media Classic, no es necesario configurar ninguna opción. Este es el comportamiento predeterminado.

Sin embargo, si no desea que los recursos insertados en Dynamic Media Classic se publiquen automáticamente, en esta sección se describe cómo configurar AEM y Dynamic Media Classic para hacerlo.

#### Requisitos previos para insertar recursos en Dynamic Media Classic sin publicar {#prerequisites-to-push-assets-to-scene-unpublished}

Para poder insertar recursos en Dynamic Media Classic sin publicarlos, debe configurar lo siguiente:

1. [Utilice el Admin Console para crear un caso de soporte técnico.](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) En el caso de soporte, solicite que la previsualización segura se habilite para su cuenta de Dynamic Media Classic.
1. Siga las instrucciones para [configurar la previsualización segura para su cuenta de Dynamic Media Classic.](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)

Estos son los mismos pasos que debe seguir para crear cualquier configuración de prueba segura en Dynamic Media Classic.

>[!NOTE]
>
>Si el entorno de instalación es un sistema operativo Unix de 64 bits, consulte [https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) acerca de las opciones de configuración adicionales que necesita configurar.

#### Limitaciones conocidas para insertar recursos en estado no publicado {#known-limitations-for-pushing-assets-in-unpublished-state}

Si utiliza esta función, tenga en cuenta las siguientes limitaciones:

* No se admite el control de versiones.
* Si un recurso ya se ha publicado en AEM y se crea una versión posterior, dicha nueva versión se publicará inmediatamente en directo en producción. Publicar tras la activación solo funciona con la publicación inicial de un recurso.

>[!NOTE]
>
>Si desea publicar recursos instantáneamente, se recomienda mantener **[!UICONTROL Habilitar Previsualización segura]** configurada en **[!UICONTROL Inmediatamente]** y utilizar la función **[!UICONTROL Habilitar carga automática]**.

### Configuración del estado de los recursos insertados en Dynamic Media Classic como no publicados {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>Si un usuario publica el recurso en AEM, lo activa automáticamente en el recurso activo/de producción (el recurso ya no estará en previsualización segura/sin publicar).

Para definir el estado de los recursos insertados en Dynamic Media Classic como no publicados:

1. Toque el icono de AEM y vaya a **[!UICONTROL Implementación > Cloud Services]**, toque **[!UICONTROL Dynamic Media Classic]** y seleccione su configuración en Dynamic Media Classic.
1. Toque la ficha **[!UICONTROL Avanzado]**. En el menú desplegable **[!UICONTROL Habilitar Vista segura]**, seleccione **[!UICONTROL Al publicar Activación]** de AEM para insertar recursos en Dynamic Media Classic sin publicarlos. (De forma predeterminada, este valor se establece en **[!UICONTROL Inmediatamente]**, donde los recursos de Dynamic Media Classic se publican inmediatamente).

   Consulte la [documentación de Dynamic Media Classic](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html) para obtener más información sobre cómo probar los recursos antes de hacerlos públicos.

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. Toque **[!UICONTROL Aceptar.]**

Al habilitar la Vista segura, los recursos se insertan en el servidor de previsualización segura sin publicar.

Puede comprobarlo si va a un componente de Dynamic Media Classic en una página de AEM y toca **[!UICONTROL Editar.]** El recurso tendrá el servidor de previsualización seguro enumerado en la dirección URL. Después de publicar en AEM, el dominio del servidor en la referencia del archivo se actualiza de la URL de previsualización a la URL de producción.

### Activación de Dynamic Media Classic para WCM {#enabling-scene-for-wcm}

Se requiere activar Dynamic Media Classic para WCM por dos motivos:

* Para habilitar la lista desplegable de perfiles de vídeo universales para la creación de páginas. Sin esto, la lista desplegable **[!UICONTROL Ajuste preestablecido de vídeo universal]** está vacía y no se puede establecer.
* Si un recurso digital no está en la carpeta destinatario, puede cargarlo en Dynamic Media Classic si activa Dynamic Media Classic para esa página en las propiedades de la página y arrastrarlo y soltarlo en un componente de Dynamic Media Classic. Se aplican reglas de herencia normales (lo que significa que las páginas secundarias heredarán la configuración de la página principal).

Al habilitar Dynamic Media Classic para WCM, tenga en cuenta que, al igual que con otras configuraciones, se aplican las reglas de herencia. Puede activar Dynamic Media Classic para WCM en la interfaz de usuario táctil o clásica.

#### Activación de Dynamic Media Classic para WCM en la interfaz de usuario táctil optimizada {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

Para activar Dynamic Media Classic para WCM en la IU táctil:

1. Toque el icono de AEM y vaya a **[!UICONTROL Sitios]** y luego a la página raíz del sitio Web (no específica del idioma).

1. En la barra de herramientas, seleccione el icono [!UICONTROL configuración] y toque **[!UICONTROL Abrir propiedades.]**

1. Toque **[!UICONTROL Cloud Services]** y toque **[!UICONTROL Añadir configuración]** y seleccione **[!UICONTROL Dynamic Media Classic.]**
1. En la lista desplegable **[!UICONTROL Adobe Dynamic Media Classic]**, seleccione la configuración deseada y toque **[!UICONTROL Aceptar.]**

   ![chlimage_1-303](assets/chlimage_1-303.png)

   Los ajustes preestablecidos de vídeo de esa configuración de Dynamic Media Classic están disponibles para su uso en AEM con el componente de vídeo de Dynamic Media Classic en esa página y en las páginas secundarias.

#### Activación de Dynamic Media Classic para WCM en la interfaz de usuario clásica {#enabling-scene-for-wcm-in-the-classic-user-interface}

Para activar Dynamic Media Classic para WCM en la IU clásica:

1. En AEM, toque **[!UICONTROL Sitios web]** y navegue a la página raíz del sitio web (no específica del idioma).

1. En la barra de tareas, toque el icono **[!UICONTROL Página]** y toque **[!UICONTROL Propiedades de la página.]**

1. Toque **[!UICONTROL Cloud Services > Añadir servicios > Dynamic Media Classic.]**
1. En la lista desplegable **[!UICONTROL Adobe Dynamic Media Classic]**, seleccione la configuración deseada y toque **[!UICONTROL Aceptar.]**

   Los ajustes preestablecidos de vídeo de esa configuración de Dynamic Media Classic están disponibles para su uso en AEM con el componente de vídeo de Dynamic Media Classic en esa página y en las páginas secundarias.

### Configuración de una configuración predeterminada {#configuring-a-default-configuration}

Si tiene varias configuraciones de Dynamic Media Classic, puede especificar una de ellas como la predeterminada para el navegador de contenido de Dynamic Media Classic.

Solo se puede marcar una configuración de Dynamic Media Classic como predeterminada en un momento dado. La configuración predeterminada son los recursos de compañía que se muestran de forma predeterminada en el navegador de contenido de Dynamic Media Classic.

Para configurar la configuración predeterminada:

1. Toque el icono de AEM y vaya a **[!UICONTROL Implementación > Cloud Services]**, toque **[!UICONTROL Dynamic Media Classic]** y seleccione su configuración en Dynamic Media Classic.
1. Toque **[!UICONTROL Editar]** para abrir la configuración.

1. En la ficha **[!UICONTROL General]**, active la casilla de verificación **[!UICONTROL Configuración predeterminada]** para que ésta sea la compañía y la ruta raíz predeterminadas que aparecen en el explorador de contenido de Dynamic Media Classic.

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >Si sólo hay una configuración, la selección de la casilla de verificación **[!UICONTROL Configuración predeterminada]** no tiene ningún efecto.

### Configuración de la carpeta Ad-hoc {#configuring-the-ad-hoc-folder}

Puede configurar la carpeta en la que se cargan los recursos en Dynamic Media Classic cuando el recurso no se encuentra en la carpeta de destinatario de CQ. Consulte Publicación de recursos desde fuera de la carpeta de destinatario de CQ.

Para configurar la carpeta ad hoc:

1. Toque el icono de AEM y vaya a **[!UICONTROL Implementación > Cloud Services]**, toque **[!UICONTROL Dynamic Media Classic]** y seleccione su configuración en Dynamic Media Classic.
1. Toque **[!UICONTROL Editar]** para abrir la configuración.

1. Toque la ficha **[!UICONTROL Avanzado]**. En el campo **[!UICONTROL Carpeta ad-hoc]**, puede modificar la carpeta **Ad-hoc**. De forma predeterminada, es **nombre de la compañía/CQ5_adhoc**.

   ![chlimage_1-305](assets/chlimage_1-305.png)

### Configuración de ajustes preestablecidos universales {#configuring-universal-presets}

Para configurar los ajustes preestablecidos universales para el componente de vídeo, consulte [Vídeo](/help/assets/s7-video.md).

## Habilitación de la compatibilidad con el parámetro de trabajo de carga de Recursos MIME basados en tipos/Dynamic Media Classic {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

Puede activar los parámetros configurables de trabajos de carga de Dynamic Media Classic activados por la sincronización de recursos de Digital Asset Manager/Dynamic Media Classic.

Concretamente, puede configurar el formato de archivo aceptado por tipo MIME en el área OSGi (Iniciativa de puerta de enlace de servicio abierta) del panel Configuración de la consola web de AEM. A continuación, puede personalizar los parámetros individuales del trabajo de carga que se utilizan para cada tipo MIME en el JCR (repositorio de contenido de Java).

**Para habilitar los recursos basados en tipos MIME:**

1. Toque el icono de AEM y vaya a **[!UICONTROL Herramientas > Operaciones > Consola web.]**
1. En el panel Configuración de la consola web de Adobe Experience Manager, en el menú **[!UICONTROL OSGi]**, toque **[!UICONTROL Configuración.]**
1. En la columna Nombre, busque y toque **[!UICONTROL Servicio MIME de Dynamic Media Classic Asset de Adobe CQ]** para editar la configuración.
1. En el área Asignación de tipos de MIME, toque cualquier signo más (+) para agregar un tipo MIME.

   Consulte [Tipos MIME admitidos](/help/assets/assets-formats.md#supported-mime-types).

1. En el campo de texto, escriba el nuevo nombre del tipo MIME.

   Por ejemplo, escribiría `<file_extension>=<mime_type>` como en `EPS=application/postscript` OR `PSD=image/vnd.adobe.photoshop`.

1. En la esquina inferior derecha de la ventana de configuración, toque **[!UICONTROL Guardar.]**
1. Vuelva a AEM y, en el carril izquierdo, toque CRXDE Lite.
1. En la página CRXDE Lite, en el carril izquierdo, navegue a `/etc/cloudservices/scene7/<environment>` (reemplace `<environment>` por el nombre real).
1. Expanda `<environment>` (reemplace `<environment>` por el nombre real) para mostrar el nodo `mimeTypes`.
1. Toque el mimeType que acaba de agregar.

   Por ejemplo, `mimeTypes > application_postscript` OR `mimeTypes > image_vnd.adobe.photoshop`.

1. En la parte derecha de la página CRXDE Lite, toque la ficha **[!UICONTROL Propiedades]**.
1. Especifique un parámetro de trabajo de carga de Dynamic Media Classic en el campo de valor **[!UICONTROL jobParam]**.

   Por ejemplo, `psprocess="rasterize"&psresolution=120` .

   Consulte la [API de Dynamic Media Classic Image Production System de Adobe](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html) para obtener parámetros de trabajo de carga adicionales que puede utilizar.

   >[!NOTE]
   >
   >Si está cargando archivos PSD y desea procesarlos como plantillas con extracciones de capa, introduzca lo siguiente en el campo de valor **[!UICONTROL jobParam]**:
   >
   >`process=MaintainLayers&createTemplate=true`
   >
   >Asegúrese de que el archivo PSD tiene &quot;capas&quot;. Si es estrictamente una imagen o una imagen con máscara, se procesa como una imagen porque no hay capas que procesar.

1. En la esquina superior izquierda de la página CRXDE Lite, toque **[!UICONTROL Guardar todo.]**

## Solución de problemas de integración de Dynamic Media Classic y AEM {#troubleshooting-scene-and-aem-integration}

Si tiene problemas para integrar AEM con Dynamic Media Classic, consulte los siguientes escenarios para obtener soluciones.

**Si falla la publicación de recursos digitales en Dynamic Media Classic:**

* Compruebe que el recurso que está intentando cargar se encuentra en la carpeta **[!UICONTROL CQ destinatario]** (especifique esta carpeta en la configuración de nube de Dynamic Media Classic).
* Si no es así, debe configurar la configuración de nube en **[!UICONTROL Propiedades de la página]** para esa página a fin de permitir la carga en la carpeta **[!UICONTROL CQ adhoc]**.

* Consulte los registros para obtener información.

**Si no aparecen los ajustes preestablecidos de vídeo:**

* Asegúrese de haber configurado la configuración de nube de esa página mediante **[!UICONTROL Propiedades de la página.]** Los ajustes preestablecidos de vídeo están disponibles en el componente de vídeo de Dynamic Media Classic.

**Si los recursos de vídeo no se reproducen en AEM:**

* Asegúrese de que ha utilizado el componente de vídeo correcto. El componente de vídeo de Dynamic Media Classic es diferente del componente de vídeo de base. Consulte [Componente de vídeo de base versus Componente de vídeo de Dynamic Media Classic](/help/assets/s7-video.md).

**Si los recursos nuevos o modificados de AEM no se cargan automáticamente a Dynamic Media Classic:**

* Asegúrese de que los recursos están en la carpeta de destinatario de CQ. Solo se actualizan automáticamente los recursos que se encuentran en la carpeta destinatario de CQ (siempre que haya configurado AEM Assets para cargar recursos automáticamente).
* Asegúrese de haber configurado la configuración de Cloud Services para activar la carga automática y de haber actualizado y guardado el flujo de trabajo de recursos DAM para incluir la carga de Dynamic Media Classic.
* Al cargar una imagen en una subcarpeta de la carpeta destinatario de Dynamic Media Classic, asegúrese de realizar una de las siguientes acciones:

   * Asegúrese de que los nombres de todos los recursos, independientemente de la ubicación, son únicos. De lo contrario, se elimina el recurso de la carpeta de destinatario principal y solo permanece el recurso de la subcarpeta.
   * Cambie el modo en que Dynamic Media Classic sobrescribe los recursos en el área Configuración de la cuenta de Dynamic Media Classic. No configure Dynamic Media Classic para sobrescribir recursos independientemente de la ubicación si utiliza recursos con el mismo nombre en las subcarpetas.

**Si los recursos o carpetas eliminados no están sincronizados entre Dynamic Media Classic y AEM:**

* Los recursos y las carpetas eliminados en AEM Assets siguen apareciendo en la carpeta sincronizada de Dynamic Media Classic. Debe eliminarlos manualmente.

**Si falla la carga de vídeo**

* Si falla la carga de vídeo y utiliza AEM para codificar vídeo mediante la integración de Dynamic Media Classic, consulte [Añadir el tiempo de espera configurable al flujo de trabajo de carga de Dynamic Media Classic](#adding-configurable-timeout-to-scene-upload-workflow).

>[!CAUTION]
>
>La importación de recursos desde una cuenta de compañía existente de Dynamic Media Classic puede tardar mucho tiempo en mostrarse en AEM. Asegúrese de designar una carpeta en Dynamic Media Classic que no tenga demasiados recursos (por ejemplo, la carpeta raíz tendrá con frecuencia demasiados recursos).
>
>Si desea probar la unidad de integración, puede que desee que la carpeta raíz apunte solo a una subcarpeta, en lugar de a toda la compañía.

