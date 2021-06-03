---
title: 'Configuración de Dynamic Media: modo híbrido'
description: Obtenga información sobre cómo configurar Dynamic Media en modo híbrido.
uuid: 39ad7d83-d310-4baf-9d85-5532c2f201f3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 7d8e7273-29f3-4a45-ae94-aad660d2c71d
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/config-dynamic
role: Business Practitioner, Administrator
exl-id: 5719d32c-4f19-47c1-bea9-8fd0bc8439ed
feature: Configuración,Modo híbrido
source-git-commit: d2649ec83424978ba01b9bb61e9f935bdc79aa62
workflow-type: tm+mt
source-wordcount: '7843'
ht-degree: 1%

---

# Configuración de Dynamic Media: modo híbrido {#configuring-dynamic-media-hybrid-mode}

Dynamic Media-Hybrid debe estar habilitado y configurado para su uso. Según el caso de uso, Dynamic Media tiene varias [configuraciones admitidas](#supported-dynamic-media-configurations).

>[!NOTE]
>
>Si tiene intención de configurar y ejecutar Dynamic Media en modo de ejecución de Scene7, consulte [Configuración de Dynamic Media - modo Scene7](/help/assets/config-dms7.md).
>
>Si desea configurar y ejecutar Dynamic Media en modo de ejecución híbrido, siga las instrucciones de esta página.

Obtenga más información sobre cómo trabajar con [video](/help/assets/video.md) en Dynamic Media.

>[!NOTE]
>
>Si utiliza la configuración de Adobe Experience Manager para diferentes entornos, como uno para desarrollo, ensayo y producción en directo, configure los Cloud Services de Dynamic Media para cada entorno.

>[!NOTE]
>
>Si tiene problemas con la configuración de Dynamic Media, busque en los archivos de registro específicos de Dynamic Media. Estos archivos se instalan automáticamente al habilitar Dynamic Media:
>
>* `s7access.log`
>* `ImageServing.log`

>
>
Están documentados en [Monitorización y mantenimiento de la instancia de Experience Manager](/help/sites-deploying/monitoring-and-maintaining.md).

La publicación y entrega híbridas es una función central de la adición de Dynamic Media a Adobe Experience Manager. La publicación híbrida permite enviar recursos de Dynamic Media, como imágenes, conjuntos y vídeos, desde la nube en lugar de desde los nodos de publicación del Experience Manager.

Otros contenidos, como los visores de Dynamic Media, las páginas del sitio y el contenido estático, se siguen suministrando desde los nodos de publicación del Experience Manager.

Si es cliente de Dynamic Media, debe utilizar el envío híbrido como mecanismo de envío para todo el contenido de Dynamic Media.

## Arquitectura de publicación híbrida para vídeos {#hybrid-publishing-architecture-for-videos}

![chlimage_1-506](assets/chlimage_1-428.png)

## Arquitectura de publicación híbrida para imágenes {#hybrid-publishing-architecture-for-images}

![chlimage_1-507](assets/chlimage_1-507.png)

## Configuraciones admitidas de Dynamic Media {#supported-dynamic-media-configurations}

Las tareas de configuración que siguen hacen referencia a los términos siguientes:

| **Término** | **Habilitado para Dynamic Media** | **Descripción** |
|---|---|---|
| Nodo Autor del Experience Manager | Marca de verificación blanca en círculo verde | El nodo de creación que implementa en On-Premise o a través de Managed Services. |
| Nodo Publicación de Experience Manager | &quot;X&quot; blanco en un cuadrado rojo. | El nodo de publicación que implementa en On-Premise o a través de Managed Services. |
| Nodo de publicación del servicio de imágenes | Marca de verificación blanca en un círculo verde. | El nodo de publicación que se ejecuta en los centros de datos administrados por Adobe. Hace referencia a la URL del servicio de imágenes. |

Puede optar por implementar Dynamic Media solo para imágenes, solo para vídeo o tanto para imágenes como para vídeo. Para determinar los pasos para configurar Dynamic Media para un escenario específico, consulte la siguiente tabla.

<table>
 <tbody>
  <tr>
   <td><strong>Situación</strong></td>
   <td ><strong>Cómo funciona</strong></td>
   <td><strong>Pasos de configuración</strong></td>
  </tr>
  <tr>
   <td>Entregar SOLO imágenes en producción</td>
   <td>Las imágenes se entregan a través de servidores en los centros de datos mundiales de Adobe y luego se almacenan en caché mediante una CDN para obtener un rendimiento escalable y un alcance global.</td>
   <td>
    <ol>
     <li>En el nodo <strong>author</strong> del Experience Manager, <a href="#enabling-dynamic-media">habilite Dynamic Media</a>.</li>
     <li>Configure imágenes en <a href="#configuring-dynamic-media-cloud-services">Cloud Services de Dynamic Media</a>.</li>
     <li><a href="#configuring-image-replication">Configurar la replicación de imágenes</a>.</li>
     <li><a href="#replicating-catalog-settings">Replicar la configuración del catálogo</a>.</li>
     <li><a href="#replicating-viewer-presets">Duplique los ajustes preestablecidos de visor</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">Utilice filtros de recursos predeterminados para la replicación</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Configuración del servidor de imágenes de Dynamic Media</a>.</li>
     <li><a href="#delivering-assets">Enviar recursos</a>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Enviar SOLO imágenes en la preproducción (desarrollo, control de calidad, fase, etc.)</td>
   <td>Las imágenes se entregan a través del nodo de publicación del Experience Manager. En esta situación, como el tráfico es mínimo, no es necesario enviar imágenes al centro de datos de Adobe. Además, permite una previsualización segura del contenido antes del inicio de la producción.</td>
   <td>
    <ol>
     <li>En el nodo <strong>author</strong> del Experience Manager, <a href="#enabling-dynamic-media">habilite Dynamic Media</a>.</li>
     <li>En el nodo <strong>publish</strong> del Experience Manager, <a href="#enabling-dynamic-media">habilite Dynamic Media</a>.</li>
     <li><a href="#replicating-viewer-presets">Duplique los ajustes preestablecidos de visor</a>.</li>
     <li>Configure el <a href="#setting-up-asset-filters-for-imaging-in-non-production-deployments">filtro de recursos para imágenes que no sean de producción</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Configure Dynamic Media Image Server.</a></li>
     <li><a href="#delivering-assets">Enviar recursos.</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Enviar SOLO vídeo en cualquier entorno (producción, desarrollo, QE, fase, etc.)</td>
   <td>Los vídeos son entregados y almacenados en caché por una CDN para un rendimiento escalable y alcance global. La imagen del póster de vídeo (miniatura del vídeo que se muestra antes de que se inicie la reproducción) la entrega la instancia de publicación del Experience Manager.</td>
   <td>
    <ol>
     <li>En el nodo <strong>author</strong> del Experience Manager, <a href="#enabling-dynamic-media">habilite Dynamic Media</a>.</li>
     <li>En el nodo <strong>publish</strong> del Experience Manager, <a href="#enabling-dynamic-media">enable Dynamic Media</a> (la instancia de publicación sirve para la imagen del póster de vídeo y proporciona metadatos para la reproducción del vídeo).</li>
     <li>Configure el vídeo en <a href="#configuring-dynamic-media-cloud-services">Cloud Services de Dynamic Media.</a></li>
     <li><a href="#replicating-viewer-presets">Duplique los ajustes preestablecidos de visor</a>.</li>
     <li>Configure el <a href="#setting-up-asset-filters-for-video-only-deployments">filtro de recursos para solo vídeo</a>.</li>
     <li><a href="#delivering-assets">Enviar recursos.</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Entregar imágenes y vídeo en producción</td>
   <td><p>Los vídeos son entregados y almacenados en caché por una CDN para un rendimiento escalable y alcance global. Las imágenes y las imágenes de póster de vídeo se entregan a través de servidores en los centros de datos mundiales de Adobe y luego se almacenan en la caché de una CDN para lograr un rendimiento escalable y un alcance global.</p> <p>Consulte las secciones anteriores para configurar la imagen o el vídeo antes de la producción. </p> </td>
   <td>
    <ol>
     <li>En el nodo <strong>author</strong> del Experience Manager, <a href="#enabling-dynamic-media">habilite Dynamic Media</a>.</li>
     <li>Configure el vídeo en <a href="#configuring-dynamic-media-cloud-services">Cloud Services de Dynamic Media.</a></li>
     <li>Configure imágenes en <a href="#configuring-dynamic-media-cloud-services">Cloud Services de Dynamic Media.</a></li>
     <li><a href="#configuring-image-replication">Configurar la replicación de imágenes</a>.</li>
     <li><a href="#replicating-catalog-settings">Replicar la configuración del catálogo</a>.</li>
     <li><a href="#replicating-viewer-presets">Duplique los ajustes preestablecidos de visor</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">Utilice filtros de recursos predeterminados para la replicación.</a></li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Configure Dynamic Media Image Server.</a></li>
     <li><a href="#delivering-assets">Enviar recursos.</a></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Habilitación de Dynamic Media {#enabling-dynamic-media}

[Dynamic Media está desactivado de forma predeterminada. ](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) Para aprovechar las funciones de Dynamic Media, debe habilitar Dynamic Media utilizando el modo de ejecución `dynamicmedia` como lo haría, por ejemplo, en el modo de ejecución `publish`. Antes de habilitarlo, asegúrese de revisar los [requisitos técnicos](/help/sites-deploying/technical-requirements.md#requirements-for-aem-dynamic-media-add-on).

>[!NOTE]
>
>Al habilitar Dynamic Media mediante el modo de ejecución, se sustituye la funcionalidad de Experience Manager 6.1 y Experience Manager 6.0, donde se habilitó Dynamic Media, estableciendo el indicador `dynamicMediaEnabled` en **[!UICONTROL true]**. Este indicador no tiene funcionalidad en Experience Manager 6.2 y posteriores. Además, no es necesario reiniciar el inicio rápido para habilitar Dynamic Media.

Al habilitar Dynamic Media, las funciones de Dynamic Media están disponibles en la interfaz de usuario y cada recurso de imagen cargado recibe una *cqdam.pyramid.tiff* representación que se utiliza para el envío rápido de representaciones de imágenes dinámicas. Estos PTIFF tienen ventajas significativas como las siguientes:

* La capacidad de administrar sólo una única imagen de origen principal y generar infinitas representaciones sobre la marcha sin ningún almacenamiento de información adicional.
* La capacidad para utilizar la visualización interactiva, como el zoom, la panorámica y el giro.

Si desea utilizar Dynamic Media Classic en Experience Manager, no habilite Dynamic Media a menos que esté utilizando un [escenario específico](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media). Dynamic Media está desactivado a menos que habilite Dynamic Media mediante el modo de ejecución.

Para habilitar Dynamic Media, debe habilitar el modo de ejecución de Dynamic Media desde la línea de comandos o desde el nombre del archivo de inicio rápido.

**Para habilitar Dynamic Media:**

1. En la línea de comandos, al iniciar el inicio rápido, haga lo siguiente:

   * Agregue `-r dynamicmedia` al final de la línea de comandos al iniciar el archivo jar.

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -r dynamicmedia
   ```

   Si está publicando en s7delivery, también debe incluir los siguientes argumentos trustStore:

   ```
   -Djavax.net.ssl.trustStore=<absoluteFilePath>/customerTrustStoreFileName>
   
    -Djavax.net.ssl.trustStorePassword=<passwordForTrustStoreFile>
   ```

1. Solicite `https://localhost:4502/is/image` y asegúrese de que Image Server se esté ejecutando.

   >[!NOTE]
   >
   >Para solucionar problemas con Dynamic Media, consulte los siguientes registros en el directorio `crx-quickstart/logs/`:
   >
   >* ImageServer-&lt;PortId>-&lt;yyyy>&lt;mm>&lt;dd>.log: el registro de ImageServer proporciona estadísticas e información analítica utilizada para analizar el comportamiento del proceso interno de ImageServer.

   Ejemplo de nombre de archivo de registro del servidor de imágenes: `ImageServer-57346-2020-07-25.log`
   * s7access-&lt;yyyy>&lt;mm>&lt;dd>.log: el registro de acceso s7registra cada solicitud realizada a Dynamic Media a través de `/is/image` y `/is/content`.

   Estos registros solo se utilizan cuando Dynamic Media está habilitado. No se incluyen en el paquete **Download Full** que se genera desde la página `system/console/status-Bundlelist`; cuando llame al servicio de atención al cliente si tiene un problema con Dynamic Media, anexe ambos registros al problema.

### Si instaló un Experience Manager en un puerto o una ruta de contexto diferente... {#if-you-installed-aem-to-a-different-port-or-context-path}

Si está implementando el [Experience Manager en un servidor de aplicaciones](/help/sites-deploying/application-server-install.md) y tiene Dynamic Media habilitado, debe configurar el dominio **self** en el externalizador. De lo contrario, la generación de miniaturas de los recursos no funciona correctamente para los recursos de Dynamic Media.

Además, si ejecuta inicio rápido en un puerto o ruta de contexto diferente, también debe cambiar el dominio **self**.

Cuando Dynamic Media está habilitado, las representaciones de miniaturas estáticas para los recursos de imagen se generan mediante Dynamic Media. Para que la generación de miniaturas funcione correctamente en Dynamic Media, el Experience Manager debe realizar una solicitud de URL y conocer el número de puerto y la ruta de contexto.

En Experience Manager:

* El dominio **self** del [externalizador](/help/sites-developing/externalizer.md) se utiliza para recuperar el número de puerto y la ruta de contexto.
* Si no hay ningún dominio **self** configurado, el número de puerto y la ruta de contexto se recuperan del servicio HTTP Jetty.

En una implementación de QuickStart WAR para Experience Manager, el número de puerto y la ruta de contexto no se pueden derivar, por lo que debe configurar un dominio **self**. Consulte la [documentación del externalizador](/help/sites-developing/externalizer.md) sobre cómo configurar el dominio **self**.

>[!NOTE]
En una implementación independiente [Quickstart del Experience Manager](/help/sites-deploying/deploy.md), generalmente no es necesario configurar un dominio **self** porque el número de puerto y la ruta de contexto se pueden configurar automáticamente. Sin embargo, si todas las interfaces de red están desactivadas, debe configurar el dominio **self**.

## Desactivación de Dynamic Media {#disabling-dynamic-media}

Dynamic Media no está habilitado de forma predeterminada. Sin embargo, si ha habilitado previamente Dynamic Media, puede desactivarlo más tarde.

Para deshabilitar Dynamic Media después de haberla habilitado, debe quitar el indicador del modo de ejecución `-r dynamicmedia`.

**Para deshabilitar Dynamic Media después de haberla habilitado**

1. En la línea de comandos, al iniciar el inicio rápido, puede realizar una de las siguientes acciones:

   * No agregue `-r dynamicmedia` a la línea de comandos al iniciar el archivo jar.

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar
   ```

1. Solicitar `https://localhost:4502/is/image`. Recibe un mensaje que indica que Dynamic Media está deshabilitado.

   >[!NOTE]
   Una vez desactivado el modo de ejecución de Dynamic Media, el paso del flujo de trabajo que genera la representación `cqdam.pyramid.tiff` se omite automáticamente. También deshabilita la compatibilidad con representaciones dinámicas y otras funciones de Dynamic Media.
   Tenga en cuenta también que cuando el modo de ejecución de Dynamic Media está desactivado después de configurar el servidor de Experience Manager, todos los recursos cargados en ese modo de ejecución no son válidos.

## (Opcional) Migración de ajustes preestablecidos y configuraciones de Dynamic Media de 6.3 a 6.5 Zero Downtime {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

Si está actualizando Experience Manager Dynamic Media de 6.3 a 6.5 (que ahora incluye la capacidad de cero implementaciones de tiempo de inactividad), debe ejecutar el siguiente comando curl. El comando migra todos los ajustes preestablecidos y configuraciones de `/etc` a `/conf` en el CRXDE Lite.

>[!NOTE]
Si ejecuta la instancia de Experience Manager en modo de compatibilidad (es decir, tiene instalado el paquete de compatibilidad), no es necesario ejecutar estos comandos.

Para todas las actualizaciones, ya sea con o sin el paquete de compatibilidad, puede copiar los ajustes preestablecidos de visor predeterminados y listos para usar que se incluyeron originalmente con Dynamic Media ejecutando el siguiente comando Linux® curl:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

Para migrar cualquier ajuste preestablecido y configuración de visor personalizado que haya creado de `/etc` a `/conf`, ejecute el siguiente comando curl de Linux®:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## Configuración de la replicación de imágenes {#configuring-image-replication}

La entrega de imágenes de Dynamic Media funciona mediante la publicación de recursos de imagen, incluidas miniaturas de vídeo, desde el Autor de Experience Manager y su replicación al servicio de replicación bajo demanda de Adobe (la URL del servicio de replicación). A continuación, los recursos se entregan mediante el servicio de entrega de imágenes bajo demanda (la URL del servicio de imágenes).

Haga lo siguiente:

1. [Configure la autenticación](#setting-up-authentication).
1. [Configure el agente de replicación](#configuring-the-replication-agent).

El agente de replicación publica recursos de Dynamic Media, como imágenes, metadatos de vídeo y establece el servicio de imágenes alojado en Adobe. El agente de replicación no está habilitado de forma predeterminada.

Después de configurar el agente de replicación, debe [validar y probar que se ha configurado correctamente](#validating-the-replication-agent-for-dynamic-media). En esta sección se describen estos procedimientos.

>[!NOTE]
El límite de memoria predeterminado para la creación de PTIFF es de 3 GB en todos los flujos de trabajo. Por ejemplo, puede procesar una imagen que requiera 3 GB de memoria mientras otros flujos de trabajo están en pausa, o puede procesar 10 imágenes en paralelo que requieran 300 MB de memoria cada una.
El límite de memoria es configurable y se ajusta a la disponibilidad de recursos del sistema y al tipo de contenido de imagen que se está procesando. Si tiene muchos recursos grandes y tiene suficiente memoria en el sistema, puede aumentar este límite para garantizar que las imágenes se procesen en paralelo.
Se rechaza una imagen que requiere más del límite máximo de memoria.
Para cambiar el límite de memoria para la creación de PTIFF, vaya a **[!UICONTROL Tools > Operations > Web Console > Adobe CQ Scene7 PTiffManager]** y cambie el valor **[!UICONTROL maxMemory]**.

### Configuración de la autenticación {#setting-up-authentication}

Configure la autenticación de replicación en el autor para que pueda replicar imágenes en el servicio de entrega de imágenes de Dynamic Media. Primero obtiene un KeyStore y luego lo guarda en el usuario **[!UICONTROL dynamic-media-replication]** y lo configura. El administrador de su empresa recibió un correo electrónico de bienvenida con el archivo KeyStore y las credenciales necesarias durante el proceso de aprovisionamiento. Si no recibió esta información, póngase en contacto con el Servicio de atención al cliente de Adobe.

**Para configurar la autenticación**

1. Póngase en contacto con el Servicio de atención al cliente de Adobe para obtener su archivo y contraseña de KeyStore si todavía no tiene el archivo y la contraseña. Esta información es una parte necesaria del aprovisionamiento. Asocia las claves a su cuenta.
1. En el Experience Manager, pulse el logotipo del Experience Manager para acceder a la consola de navegación global y, a continuación, pulse **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.
1. En la página Administración de usuarios , vaya al usuario **[!UICONTROL dynamic-media-replication]** y, a continuación, pulse para abrir.

   ![dm-replication](assets/dm-replication.png)

1. En la página Editar configuración de usuario para la replicación de Dynamic Media, pulse la pestaña **[!UICONTROL Almacén de claves]** y haga clic en **[!UICONTROL Crear almacén de claves]**.

   ![dm-replication-keystore](assets/dm-replication-keystore.png)

1. Introduzca una contraseña y confirme la contraseña en el cuadro de diálogo **[!UICONTROL Establecer contraseña de acceso al almacén de claves]**.

   >[!NOTE]
   Recuerde la contraseña porque debe introducirla de nuevo cuando configure el agente de replicación más tarde.

   ![chlimage_1-508](assets/chlimage_1-508.png)

1. En la página **[!UICONTROL Editar configuración de usuario para la replicación de medios dinámicos]**, expanda el área **Agregar clave privada del archivo KeyStore** y añada lo siguiente (vea las imágenes que siguen):

   * En el campo **[!UICONTROL Nuevo alias]**, introduzca el nombre de un alias que desee utilizar posteriormente en la configuración de replicación. Por ejemplo, puede utilizar `replication` como alias.
   * Toque **[!UICONTROL Archivo KeyStore]**. Vaya al archivo KeyStore proporcionado por Adobe, selecciónelo y pulse **[!UICONTROL Abrir]**.
   * En el campo **[!UICONTROL KeyStore File Password]**, introduzca la contraseña del archivo KeyStore. Esta contraseña es **no** la contraseña de KeyStore que creó en el paso 5, pero es el Adobe de contraseña del archivo KeyStore que proporciona el correo electrónico de bienvenida que se le envió durante el aprovisionamiento. Póngase en contacto con el Servicio de atención al cliente de Adobe si no recibió una contraseña para el archivo KeyStore.
   * En el campo **[!UICONTROL Private Key Password]**, introduzca la contraseña de clave privada (puede ser la misma contraseña de clave privada proporcionada en el paso anterior). Adobe proporciona la contraseña de clave privada en el correo electrónico de bienvenida que se le envía durante el aprovisionamiento. Póngase en contacto con el Servicio de atención al cliente de Adobe si no recibió una contraseña de clave privada.
   * En el campo **[!UICONTROL Private Key Alias]**, introduzca el alias de clave privada. Por ejemplo, `*companyname*-alias`. Adobe proporciona el alias de clave privada en el correo electrónico de bienvenida que se le envía durante el aprovisionamiento. Póngase en contacto con el Servicio de atención al cliente de Adobe si no recibió un alias de clave privada.

   ![edit_settings_fordynamic-media-replication2](assets/edit_settings_fordynamic-media-replication2.png)

1. Toque **[!UICONTROL Guardar y cerrar]** para guardar los cambios en este usuario.

   A continuación, debe [configurar el agente de replicación](#configuring-the-replication-agent).

### Configuración del Agente de replicación {#configuring-the-replication-agent}

1. En el Experience Manager, pulse el logotipo del Experience Manager para acceder a la consola de navegación global y, a continuación, pulse **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on author]**.
1. En la página Agentes del autor, pulse **[!UICONTROL Replicación de imagen híbrida de Dynamic Media (s7delivery)]**.
1. Toque **[!UICONTROL Editar]**.
1. Pulse la pestaña **[!UICONTROL Settings]** e introduzca lo siguiente:

   * **[!UICONTROL Habilitado]** : seleccione esta casilla de verificación para habilitar el agente de replicación.
   * **[!UICONTROL Región]** : configure en la región adecuada: América del Norte, Europa o Asia
   * **[!UICONTROL ID del inquilino]** : este valor es el nombre de su empresa o inquilino que está publicando en el servicio de replicación. Este valor es el ID del inquilino que proporciona el Adobe en el correo electrónico de bienvenida que se le envió durante el aprovisionamiento. Si no recibió esta información, póngase en contacto con el Servicio de atención al cliente de Adobe.
   * **[!UICONTROL Alias]**  del almacén de claves: Este valor es el mismo que el  **nuevo valor de** Aliasvalue establecido al generar la clave en  [Configuración de la autenticación](#setting-up-authentication); por ejemplo,  `replication`. (Consulte el paso 7 en [Configuración de la autenticación](#setting-up-authentication)).
   * **[!UICONTROL Contraseña del almacén de claves]** : la contraseña del almacén de claves que se creó al pulsar  **[!UICONTROL Crear almacén de claves]**. Adobe no proporciona esta contraseña. Consulte el paso 5 de [Configuración de la autenticación](#setting-up-authentication).

   La siguiente imagen muestra el agente de replicación con datos de ejemplo:

   ![chlimage_1-509](assets/chlimage_1-509.png)

1. Pulse **[!UICONTROL Aceptar]**.

### Validación del agente de replicación para Dynamic Media {#validating-the-replication-agent-for-dynamic-media}

Para validar el agente de replicación para Dynamic Media, haga lo siguiente:

Toque **[!UICONTROL Probar conexión]**. El resultado de ejemplo es el siguiente:

```shell
11.03.2016 10:57:55 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1457722675402, userId='admin', revision='null'}
11.03.2016 10:57:55 - * Auth User: replication-receiver
11.03.2016 10:57:55 - * HTTP Version: 1.1
11.03.2016 10:57:55 - * Using OAuth 2.0 Authorization Grants
11.03.2016 10:57:55 - * OAuth 2.0 User: dynamic-media-replication
11.03.2016 10:57:55 - * OAuth 2.0 Token: '*****' initialized
11.03.2016 10:57:55 - Publishing: POST[https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=xfpuu-6613]
11.03.2016 10:57:55 - Publish response: OK[]
11.03.2016 10:57:55 - Transfer succeeded in 141 ms for ReplicationAction{type=TEST, path[0]='/content/dam', time=1457722675402, userId='admin', revision='null'}
-------------------------------------------------------------------------------------------------------------------------------
Replication test succeeded
```

>[!NOTE]
También puede comprobarlo realizando una de las siguientes acciones:
* Compruebe los registros de replicación para asegurarse de que el recurso se replica.
* Publicar una imagen. Pulse la imagen y seleccione **[!UICONTROL Visualizadores]** en el menú desplegable y, a continuación, seleccione un ajuste preestablecido de visualizador. Haga clic en **[!UICONTROL URL]**. Para comprobar que puede ver la imagen, copie y pegue la ruta URL en el explorador.



### Resolución de problemas de autenticación {#troubleshooting-authentication}

Al configurar la autenticación, estos son algunos problemas con los que puede encontrar soluciones. Antes de comprobar estos problemas, asegúrese de haber configurado la replicación.

#### Problema: Código de estado HTTP 401 con mensaje - Autorización requerida {#problem-http-status-code-with-message-authorization-required}

Este problema puede deberse a un error al configurar KeyStore para el usuario `dynamic-media-replication`.

```shell
Replication test to s7delivery:https://s7bern.macromedia.com:8580/is-publish/
17.06.2016 18:54:43 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309, userId='admin', revision='null'}
17.06.2016 18:54:43 - * Auth User: replication-receiver
17.06.2016 18:54:43 - * HTTP Version: 1.1
17.06.2016 18:54:43 - * Using OAuth 2.0 Authorization Grants
17.06.2016 18:54:43 - * OAuth 2.0 User: dynamic-media-replication
17.06.2016 18:54:43 - No OAuth token available. OAuth not initialized
17.06.2016 18:54:43 - * Using Client Auth SSL alias - replication-alias *
17.06.2016 18:54:43 - Publishing: POST[https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough]
17.06.2016 18:54:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309, userId='admin', revision='null'}. java.io.IOException: Failed to execute request
'https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough':
 Server returned status code 401 with message: Authorization required.
17.06.2016 18:54:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309,
 userId='admin', revision='null'}. java.io.IOException: Failed to execute request
'https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough':
 Server returned status code 401 with message: Authorization required.
```

**Solución**: Compruebe que  `KeyStore` se guarde en  **dynamic-media-** replicationuser y que se proporcione con la contraseña correcta.

#### Problema: No Se Pudo Descifrar La Clave: No Se Pudieron Descifrar Los Datos {#problem-could-not-decrypt-key-could-not-decrypt-data}

```xml
Replication test to s7delivery:https://<localhost>:8580/is-publish/
17.06.2016 19:00:16 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466215216662, userId='admin', revision='null'}
17.06.2016 19:00:16 - * Auth User: replication-receiver
17.06.2016 19:00:16 - * HTTP Version: 1.1
17.06.2016 19:00:16 - * Using OAuth 2.0 Authorization Grants
17.06.2016 19:00:16 - * OAuth 2.0 User: dynamic-media-replication
17.06.2016 19:00:16 - No OAuth token available. OAuth not initialized
17.06.2016 19:00:16 - * Using Client Auth SSL alias - replication-alias *
17.06.2016 19:00:16 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466215216662, userId='admin', revision='null'}. java.lang.SecurityException: java.security.UnrecoverableKeyException: Could not decrypt key: Could not decrypt data.
```

**Solución**: Compruebe la contraseña. La contraseña guardada en el agente de replicación no es la misma contraseña que se utilizó para crear el almacén de claves.

#### Problema: InvalidAlgorithmParameterException {#problem-invalidalgorithmparameterexception}

Este problema se debe a un error de configuración en la instancia de Autor del Experience Manager. El proceso Java™ del Autor no está obteniendo el `javax.net.ssl.trustStore` correcto. Verá este error en el registro de replicación:

```shell
14.04.2016 09:37:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
14.04.2016 09:37:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
```

O el registro de errores:

```shell
07.25.2019 12:00:59.893 *ERROR* [sling-threadpool-db2763bb-bc50-4bb5-bb64-10a09f432712-(apache-sling-job-thread-pool)-90-com_day_cq_replication_job_s7delivery(com/day/cq/replication/job/s7delivery)] com.day.cq.replication.Agent.s7delivery.queue Error during processing of replication.

java.io.IOException: Failed to execute request 'https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
        at com.scene7.is.catalog.service.publish.atomic.PublishingServiceHttp.executePost(PublishingServiceHttp.scala:195)
```

**Solución**: Asegúrese de que el proceso Java™ del Autor del Experience Manager tiene la propiedad del sistema  `-Djavax.net.ssl.trustStore=` configurada en un almacén de confianza válido.

#### Problema: KeyStore no está configurado o no se inicializa {#problem-keystore-is-either-not-set-up-or-it-is-not-initialized}

Es probable que este problema se deba a una corrección o a un paquete de funciones que sobrescribe el nodo de usuario de Dynamic Media o del almacén de claves.

Ejemplo de registro de replicación:

```shell
Replication test to s7delivery:https://replicate-na.assetsadobe.com/is-publish
02.08.2016 14:37:44 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470173864834, userId='admin', revision='null'}
02.08.2016 14:37:44 - * Auth User: replication-receiver
02.08.2016 14:37:44 - * HTTP Version: 1.1
02.08.2016 14:37:44 - * Using OAuth 2.0 Authorization Grants
02.08.2016 14:37:44 - * OAuth 2.0 User: dynamic-media-replication
02.08.2016 14:37:44 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470173864834, userId='admin', revision='null'}. com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised key store for user dynamic-media-replication
```

**Solución**:

1. Vaya a la página Administración de usuarios :
   `localhost:4502/libs/granite/security/content/useradmin.html`
1. En la página Administración de usuarios , vaya al usuario `dynamic-media-replication` y, a continuación, pulse para abrir.
1. Haga clic en la pestaña **[!UICONTROL KeyStore]**. Si aparece el botón **[!UICONTROL Create KeyStore]**, debe rehacer los pasos que se encuentran en [Configuración de la autenticación](#setting-up-authentication) anteriormente.
1. Si tuvo que rehacer la configuración de KeyStore, también debe [Configurar el agente de replicación](/help/assets/config-dynamic.md#configuring-the-replication-agent).

   Vuelva a configurar el agente de replicación de s7delivery.
   `localhost:4502/etc/replication/agents.author/s7delivery.html`

1. Toque **[!UICONTROL Probar conexión]** para verificar que la configuración es válida.

#### Problema: El agente de publicación utiliza SSL en lugar de OAuth {#problem-publish-agent-is-using-ssl-instead-of-oauth}

Es probable que este problema se deba a una corrección o a un paquete de funciones que no se instalaron correctamente o que sobrescribieron la configuración.

Ejemplo de registro de réplica:

```shell
01.08.2016 18:42:59 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}
01.08.2016 18:42:59 - * Auth User: replication-receiver
01.08.2016 18:42:59 - * HTTP Version: 1.1
01.08.2016 18:42:59 - * Using Client Auth SSL alias - replication-receiver *
01.08.2016 18:42:59 - Publishing: POST[https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=altayerstaging]
01.08.2016 18:42:59 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=rbroughstaging': Server returned status code 401 with message: Authorization required.
01.08.2016 18:42:59 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=rbroughstaging': Server returned status code 401 with message: Authorization required.
```

**Solución:**

1. En el Experience Manager, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.

   `localhost:4502/crx/de/index.jsp`

1. Vaya al nodo del agente de replicación de s7delivery.
   `localhost:4502/crx/de/index.jsp#/etc/replication/agents.author/s7delivery/jcr:content`

1. Agregue esta configuración al agente de replicación (booleano con el valor establecido en **[!UICONTROL True]**):

   `enableOauth=true`

1. Cerca de la esquina superior izquierda de la página, pulse **[!UICONTROL Guardar todo]**.

### Prueba de la configuración {#testing-your-configuration}

Adobe recomienda realizar una prueba de extremo a extremo de la configuración.

Asegúrese de que ya ha hecho lo siguiente antes de comenzar esta prueba:

* Se Han Agregado Ajustes Preestablecidos De Imagen.
* Configure **[!UICONTROL Configuración de Dynamic Media (Pre 6.3)]** en Cloud Services. La URL del servicio de imágenes es necesaria para esta prueba

**Para probar la configuración:**

1. Cargue un recurso de imagen. (En Assets, pulse **[!UICONTROL Crear]** > **[!UICONTROL Archivos]** y seleccione el archivo).
1. Espere a que finalice el flujo de trabajo.
1. Publique el recurso de imagen. (Seleccione el recurso y pulse **[!UICONTROL Publicación rápida]**).
1. Vaya a las representaciones de esa imagen abriendo la imagen y tocando **[!UICONTROL Representaciones]**.

   ![chlimage_1-510](assets/chlimage_1-510.png)

1. Seleccione cualquier representación dinámica.
1. Para obtener la URL de este recurso, haga clic en **[!UICONTROL URL]**.
1. Vaya a la dirección URL seleccionada y compruebe si la imagen se comporta según lo esperado.

Otra forma de probar que los recursos se han entregado es añadir req=exists a su URL.

## Configuración de los Cloud Services de Dynamic Media {#configuring-dynamic-media-cloud-services}

El Cloud Service de Dynamic Media admite la publicación y entrega híbridos de imágenes y vídeo, análisis de vídeo y codificación de vídeo, entre otras cosas.

Como parte de la configuración, debe introducir un ID de registro, una URL de servicio de vídeo, una URL de servicio de imágenes, una URL de servicio de replicación y configurar la autenticación. Esta información se le envió por correo electrónico como parte del proceso de aprovisionamiento de cuentas. Si no recibió esta información, póngase en contacto con el administrador de Adobe Experience Manager o con el servicio de atención al cliente de Adobe para obtener la información.

>[!NOTE]
Antes de configurar los Cloud Services de Dynamic Media, asegúrese de configurar la instancia de publicación. También debe tener la replicación configurada antes de configurar los Cloud Services de Dynamic Media.

Para configurar los Cloud Services de Dynamic Media:

1. En el Experience Manager, pulse el logotipo del Experience Manager para acceder a la consola de navegación global y pulse **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de Dynamic Media (Pre-6.3)]**.
1. En la página Explorador de configuración de Dynamic Media, en el panel izquierdo, seleccione **[!UICONTROL global]** y, a continuación, pulse **[!UICONTROL Crear]**.
1. En el cuadro de diálogo **[!UICONTROL Crear configuración de Dynamic Media]**, en el campo Título, escriba un título.
1. Si está configurando Dynamic Media para vídeo,

   * En el campo **[!UICONTROL Registration ID]**, escriba su ID de registro.
   * En el campo **[!UICONTROL Video Service URL]**, introduzca la URL del servicio de vídeo para Dynamic Media Gateway.

1. Si está configurando Dynamic Media para imágenes, en el campo **[!UICONTROL Image Service URL]** introduzca la URL del servicio de imágenes para Dynamic Media Gateway.
1. Toque **[!UICONTROL Guardar]** para volver a la página Explorador de configuración de Dynamic Media.
1. Para acceder a la consola de navegación global, pulse el logotipo del Experience Manager.

## Configuración de informes de vídeo {#configuring-video-reporting}

Puede configurar los informes de vídeo en varias instalaciones de Experience Manager mediante Dynamic Media Hybrid.

**Cuándo usar:** Al configurar la configuración de Dynamic Media (versión anterior a la 6.3), se inician numerosas funciones, incluido el sistema de informes de vídeo. La configuración crea un grupo de informes en una empresa regional de Analytics. Si configura varios nodos Autor , debe crear un grupo de informes independiente para cada uno. Como resultado, los datos de los informes son incoherentes entre las instalaciones. Además, si cada nodo Autor hace referencia al mismo servidor de publicación híbrido, la última instalación de Autor cambia el grupo de informes de destino para todos los informes de vídeo. Este problema sobrecarga el sistema de Analytics con demasiados grupos de informes.

**Introducción:** configure los informes de vídeo completando las tres tareas siguientes.

1. Cree un paquete de ajustes preestablecidos de Video Analytics después de configurar Dynamic Media Configuration (Pre 6.3) en el primer nodo Author . Esta tarea inicial es importante porque permite que una nueva configuración continúe usando el mismo grupo de informes.
1. Instale el paquete de ajustes preestablecidos de Video Analytics en cualquier ***nuevo*** nodo Autor ***antes*** de configurar la configuración de Dynamic Media (Pre 6.3).
1. Compruebe y depure la instalación del paquete.

### Creación de un paquete de ajustes preestablecidos de Video Analytics después de configurar el primer nodo Autor {#creating-a-video-analytics-preset-package-after-configuring-the-first-author-node}

Cuando haya terminado esta tarea, tendrá un archivo de paquete que contiene los ajustes preestablecidos de Video Analytics. Estos ajustes preestablecidos contienen un grupo de informes, el servidor de seguimiento, el área de nombres de seguimiento y el ID de organización de Experience Cloud, si está disponible.

1. Si aún no lo ha hecho, configure Dynamic Media Configuration (Pre 6.3).
1. (Opcional) Vea y copie la ID del grupo de informes (debe tener acceso al JCR). Aunque no es necesario tener el ID del grupo de informes, facilita la validación.
1. Cree un paquete mediante el Administrador de paquetes.
1. Edite el paquete para incluir un filtro.

   En Experience Manager: `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

1. Cree el paquete.
1. Descargue o comparta el paquete de ajustes preestablecidos de Video Analytics para que se pueda compartir con los nuevos nodos de Author subsiguientes.

### Instalación del paquete de ajustes preestablecidos de Video Analytics antes de configurar más nodos de Author {#installing-the-video-analytics-preset-package-before-you-configure-additional-author-nodes}

Asegúrese de completar esta tarea ***antes*** de configurar la Configuración de Dynamic Media (Pre 6.3). Si no lo hace, se crea otro grupo de informes que no se utiliza. Además, aunque los informes de vídeo siguen funcionando correctamente, la recopilación de datos no está optimizada.

Asegúrese de que el paquete de ajustes preestablecidos de Video Analytics del primer nodo Autor es accesible en el nuevo nodo Autor.

1. Cargue el paquete de ajustes preestablecidos de Video Analytics que creó anteriormente en el Administrador de paquetes.
1. Instale el paquete de ajustes preestablecidos de Video Analytics.
1. Configuración de Dynamic Media (anterior a la versión 6.3).

### Verificación y depuración de la instalación del paquete {#verifying-and-debugging-the-package-installation}

1. Realice una de las siguientes acciones para verificar y, si es necesario, depurar la instalación del paquete:

   * **Compruebe el ajuste preestablecido de Video Analytics mediante el**
JCRTpara comprobar el ajuste preestablecido de Video Analytics mediante el JCR, debe tener acceso al CRXDE Lite.

      Experience Manager: en el CRXDE Lite, vaya a `/conf/global/settings/
dam/dm/presets/analytics/jcr:content/userdata`

      Como en `https://localhost:4502/crx/de/index.jsp#/conf/global/settings/dam/dm/presets/analytics/jcr%3Acontent/userdata`

      Si no tiene acceso al CRXDE Lite en el nodo Autor , puede comprobar el ajuste preestablecido a través del servidor de publicación.

   * **Comprobación del ajuste preestablecido de Video Analytics mediante el servidor de imágenes**

      Puede validar el ajuste preestablecido de Video Analytics directamente realizando una solicitud req=userdata del Image Server.
Por ejemplo, para ver el ajuste preestablecido de Analytics en el nodo Autor , puede realizar la siguiente solicitud:

      `https://localhost:4502/is/image/conf/global/settings/dam/dm/presets/analytics?req=userdata`

      Para validar el ajuste preestablecido en los servidores de publicación, puede realizar una solicitud directa similar al servidor de publicación. Las respuestas son las mismas en los nodos Autor y Publicación . La respuesta es similar a la siguiente:

      ```
      marketingCloudOrgId=0FC4E86B573F99CC7F000101
       reportSuite=aemaem6397618-2018-05-23
       trackingNamespace=aemvideodal
       trackingServer=aemvideodal.d2.sc.omtrdc.net
      ```

   * **Compruebe el ajuste preestablecido de Video Analytics mediante la herramienta Informes de vídeo de Experience**
ManagerToque  **[!UICONTROL Herramientas > Assets > Informes de vídeo]**

      `https://localhost:4502/mnt/overlay/dam/gui/content/s7dam/videoreports/videoreport.html`

      Si ve el siguiente mensaje de error, el grupo de informes está disponible, pero no se rellena. Este error es correcto (y deseado) en una nueva instalación antes de que el sistema recopile datos.
   ![screen_shot_2018-05-23at52254pm](assets/screen_shot_2018-05-23at52254pm.png)

   Para generar datos de informes, cargue y publique un vídeo. Utilice **[!UICONTROL Copiar URL]** y ejecute el vídeo al menos una vez.

   Pueden pasar hasta 12 horas antes de que los datos de informes se rellenen a partir del uso del visualizador de vídeo.

   Si hay un error y el grupo de informes no está configurado correctamente, se muestra la siguiente alerta.

   ![screen_shot_2018-05-23at52612pm](assets/screen_shot_2018-05-23at52612pm.png)

   Este error también se muestra si los informes de vídeo se ejecutan antes de configurar los servicios de Configuración de Dynamic Media (Pre 6.3).

### Solución de problemas de la configuración de informes de vídeo {#troubleshooting-the-video-reporting-configuration}

* Durante la instalación, a veces se agota el tiempo de espera de las conexiones al servidor de API de Analytics. La instalación vuelve a intentar la conexión 20 veces, pero sigue fallando. Cuando se produce esta situación, el archivo de registro registra varios errores. Buscar `SiteCatalystReportService`.
* Si no se instala primero el paquete de ajustes preestablecidos de Analytics, puede crearse un nuevo grupo de informes.
* Al actualizar de Experience Manager 6.3 a Experience Manager 6.4 o Experience Manager 6.4.1 y, a continuación, al configurar la configuración de Dynamic Media (anterior a 6.3), se seguirá creando un grupo de informes. Se sabe que este problema se solucionará para el Experience Manager 6.4.2.

### Acerca del ajuste preestablecido de Video Analytics {#about-the-video-analytics-preset}

El ajuste preestablecido de Video Analytics (a veces conocido simplemente como ajuste preestablecido de análisis) se almacena junto a los ajustes preestablecidos de visor en Dynamic Media. Básicamente es lo mismo que un ajuste preestablecido de visualizador, pero con información utilizada para configurar los informes de AppMeasurement y Video Heartbeat.

Las propiedades del ajuste preestablecido son las siguientes:

* `reportSuite`
* `trackingServer`
* `trackingNamespace`
* `marketingCloudOrgId` (no está presente en versiones de Experience Manager anteriores)

Experience Manager 6.4 y versiones más recientes: guarde este ajuste preestablecido en `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

## Duplicación de la configuración del catálogo {#replicating-catalog-settings}

Publique su propia configuración de catálogo predeterminada como parte del proceso de configuración a través de JCR. Para replicar la configuración del catálogo:

1. En una ventana Terminal , ejecute lo siguiente:

   `curl -u admin:admin localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

1. En Experience Manager, vaya a la siguiente ubicación en CRXDE Lite (requiere privilegios de administrador):

   `https://<*server*>:<*port*>/crx/de/index.jsp#/conf/global/settings/dam/dm/imageserver/`

1. Pulse la pestaña **[!UICONTROL Replication]**.
1. Toque **[!UICONTROL Replicar]**.

## Duplicación de ajustes preestablecidos de visor {#replicating-viewer-presets}

Para entregar *un recurso con un ajuste preestablecido de visualizador, debe duplicar/publicar* el ajuste preestablecido de visualizador. (Todos los ajustes preestablecidos de visualizador deben activarse *y* replicarse para obtener la URL o el código incrustado de un recurso.
Consulte [Ajustes preestablecidos del visualizador de publicaciones](/help/assets/managing-viewer-presets.md#publishing-viewer-presets) para obtener más información.

>[!NOTE]
De forma predeterminada, el sistema muestra varias representaciones al seleccionar **[!UICONTROL Representaciones]** y varios ajustes preestablecidos de visualizador al seleccionar **[!UICONTROL Visualizadores]** en la vista de detalles del recurso. Puede aumentar o disminuir el número de visitas. Consulte [Aumento del número de ajustes preestablecidos de imagen que se muestran](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) o [Aumento del número de ajustes preestablecidos de visor que se muestran](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

## Filtrado de recursos para replicación {#filtering-assets-for-replication}

En implementaciones que no son de Dynamic Media, se replican *todos* los recursos (tanto imágenes como vídeo) desde el entorno de creación de Experience Manager al nodo de publicación de Experience Manager. Este flujo de trabajo es necesario porque los servidores de publicación de Experience Manager también entregan los recursos.

Sin embargo, en las implementaciones de Dynamic Media, como los recursos se entregan a través de la nube, no es necesario replicar esos mismos recursos en los nodos de publicación de Experience Manager. Este flujo de trabajo de &quot;publicación híbrida&quot; evita costos de almacenamiento adicionales y tiempos de procesamiento más largos para replicar recursos. Otros contenidos, como los visores de Dynamic Media, las páginas del sitio y el contenido estático, se siguen suministrando desde los nodos de publicación del Experience Manager.

Además de replicar los recursos, también se replican los siguientes recursos que no son de :

* Configuración de Dynamic Media Delivery: `/conf/global/settings/dam/dm/imageserver/jcr:content`
* Ajustes preestablecidos de imagen: `/conf/global/settings/dam/dm/presets/macros`
* Ajustes preestablecidos de visor: `/conf/global/settings/dam/dm/presets/viewer`

Los filtros permiten excluir *los recursos* de la replicación en el nodo de publicación del Experience Manager.

### Uso de filtros de recurso predeterminados para la replicación {#using-default-asset-filters-for-replication}

Si está utilizando Dynamic Media para (1) imágenes en producción de **o** (2) imágenes y vídeo, puede utilizar los filtros predeterminados que Adobe proporciona tal cual. Los siguientes filtros están activos de forma predeterminada:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Filtro</strong></td>
   <td><strong>Tipo MIME</strong></td>
   <td><strong>Representaciones</strong></td>
  </tr>
  <tr>
   <td>Entrega de imágenes de Dynamic Media</td>
   <td><p>filter-images</p> <p>filter-sets</p> <p> </p> </td>
   <td><p>Comienza con <strong>image/</strong></p> <p>Contiene <strong>application/</strong> y termina con <strong>set</strong>.</p> </td>
   <td>Las "imágenes de filtro" integradas (se aplican a recursos de imágenes únicas, incluidas imágenes interactivas) y "conjuntos de filtros" (se aplica a conjuntos de giros, conjuntos de imágenes, conjuntos de medios mixtos y conjuntos de carrusel):
    <ul>
     <li>Incluir imágenes y metadatos PTIFF para la replicación (cualquier representación que comience por <strong>cqdam</strong>).</li>
     <li>Excluir de la replicación la imagen original y las representaciones de imágenes estáticas.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Entrega de vídeo de Dynamic Media</td>
   <td>filter-video</td>
   <td>Comienza con <strong>video/</strong></td>
   <td>El "filtro-vídeo" listo para usar:
    <ul>
     <li>Incluya representaciones de vídeo proxy, imágenes de póster/miniatura de vídeo, metadatos (tanto en las representaciones de vídeo principal como en las representaciones de vídeo) para la replicación (cualquier representación que comience por <strong>cqdam</strong>).</li>
     <li>Excluir de la replicación el vídeo original y las representaciones de miniaturas estáticas.<br /> <br /> <strong>Nota:</strong> Las representaciones de vídeo proxy no contienen binarios, sino que solo son propiedades de nodo. Por lo tanto, no hay ningún impacto en el tamaño del repositorio del editor.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Integración con Dynamic Media Classic (Scene7)</td>
   <td><p>filter-images</p> <p>filter-sets</p> <p>filter-video</p> </td>
   <td><p>Comienza con <strong>image/</strong></p> <p>Contiene <strong>application/</strong> y termina con <strong>set</strong>.</p> <p>Comienza con <strong>video/</strong></p> </td>
   <td><p>Configure el URI de transporte para que apunte al servidor de publicación del Experience Manager en lugar de la URL del servicio de replicación en la nube de Dynamic Media de Adobe. La configuración de este filtro permite que Dynamic Media Classic envíe recursos en lugar de la instancia de publicación del Experience Manager.</p> <p>Las "imágenes de filtro", "conjuntos de filtros" y "video de filtro" incorporados:</p>
    <ul>
     <li>Incluya imágenes PTIFF, representaciones de vídeo proxy y metadatos para la replicación. Sin embargo, como no existen en el JCR (para los que ejecutan el Experience Manager de integración de Dynamic Media Classic), no hace nada de forma efectiva.</li>
     <li>Excluya de la replicación la imagen original, las representaciones de imágenes estáticas, el vídeo original y las representaciones de miniaturas estáticas. En su lugar, Dynamic Media Classic ofrece recursos de imagen y vídeo.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
Los filtros se aplican a tipos MIME y no pueden ser específicos de la ruta.

### Configuración de filtros de recursos para implementaciones de solo vídeo {#setting-up-asset-filters-for-video-only-deployments}

Si utiliza Dynamic Media solo para vídeo, siga estos pasos para configurar filtros de recursos para la replicación:

1. En el Experience Manager, pulse el logotipo del Experience Manager para acceder a la consola de navegación global y pulse **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on author]**.
1. En la página Agentes del autor, pulse **[!UICONTROL Agente predeterminado (publicar)]**.
1. Toque **[!UICONTROL Editar]**.
1. En el cuadro de diálogo **[!UICONTROL Configuración del agente]**, en la pestaña **[!UICONTROL Configuración]**, marque **[!UICONTROL Habilitado]** para activar el agente.
1. Pulse **[!UICONTROL Aceptar]**.
1. En el Experience Manager, pulse **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. En el árbol de carpetas de la izquierda, vaya a `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`
1. Busque **[!UICONTROL filter-video]**, haga clic con el botón derecho del ratón y seleccione **[!UICONTROL Copy]**.
1. En el árbol de carpetas de la izquierda, vaya a `/etc/replication/agents.author/publish`
1. Busque **[!UICONTROL jcr:content]**, haga clic con el botón derecho en él y seleccione **[!UICONTROL Pegar]**.

Estos pasos configuran la instancia de publicación del Experience Manager para proporcionar la imagen del póster de vídeo y los metadatos de vídeo necesarios para la reproducción, mientras que el Cloud Service de Dynamic Media entrega el vídeo en sí. El filtro también excluye de la replicación el vídeo original y las representaciones de miniaturas estáticas, que no son necesarias en la instancia de publicación.

### Configuración de filtros de recursos para imágenes en implementaciones que no sean de producción {#setting-up-asset-filters-for-imaging-in-non-production-deployments}

Si utiliza Dynamic Media para imágenes en implementaciones que no sean de producción, siga estos pasos para configurar filtros de recursos para la replicación:

1. En el Experience Manager, pulse el logotipo del Experience Manager para acceder a la consola de navegación global y pulse **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on author]**.
1. En la página Agentes del autor, pulse **[!UICONTROL Agente predeterminado (publicar)]**.
1. Toque **[!UICONTROL Editar]**.
1. En el cuadro de diálogo **[!UICONTROL Configuración del agente]**, en la pestaña **[!UICONTROL Configuración]**, marque **[!UICONTROL Habilitado]** para activar el agente.
1. Pulse **[!UICONTROL Aceptar]**.
1. En el Experience Manager, pulse **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. En el árbol de carpetas de la izquierda, vaya a `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`

   ![image-2018-01-16-10-22-40-410](assets/image-2018-01-16-10-22-40-410.png)

1. Busque **[!UICONTROL filter-images]**, haga clic con el botón derecho del ratón y seleccione **[!UICONTROL Copy]**.
1. En el árbol de carpetas de la izquierda, vaya a `/etc/replication/agents.author/publish`
1. Busque **[!UICONTROL jcr:content]**, haga clic con el botón derecho en él y seleccione **[!UICONTROL Crear]** > **[!UICONTROL Crear nodo]**. Introduzca el nombre `damRenditionFilters` del tipo `nt:unstructured`.
1. Busque `damRenditionFilters`, haga clic con el botón derecho en él y seleccione **[!UICONTROL Pegar]**.

Estos pasos configuran la instancia de publicación del Experience Manager para entregar las imágenes a un entorno que no sea de producción. El filtro también excluye de la replicación la imagen original y las representaciones estáticas, que no son necesarias en la instancia de publicación.

>[!NOTE]
Si hay muchos filtros diferentes en un autor, cada agente necesita que se le asigne un usuario diferente. El código de granito aplica un modelo de filtro por usuario. Siempre tenga un usuario diferente para cada configuración de filtro.
¿Está utilizando más de un filtro en un servidor? Por ejemplo, un filtro para que la replicación se publique y un segundo filtro para s7delivery. Si es así, debe asegurarse de que estos dos filtros tengan un **userId** diferente asignado en el nodo **jcr:content**. Consulte la imagen siguiente:

![image-2018-01-16-10-26-28-465](assets/image-2018-01-16-10-26-28-465.png)

### Personalización de filtros de recursos para replicación {#customizing-asset-filters-for-replication}

Para personalizar de forma opcional los filtros de recursos para la replicación:

1. En el Experience Manager, pulse el logotipo del Experience Manager para acceder a la consola de navegación global y pulse **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. En el árbol de carpetas de la izquierda, vaya a `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters` para revisar los filtros.

   ![chlimage_1-511](assets/chlimage_1-511.png)

1. Para definir el tipo de hora para el filtro, puede localizar el tipo de hora de la siguiente manera:

   En el carril izquierdo, expanda `content > dam > <locate_your_asset> >  jcr:content > metadata` y, a continuación, en la tabla, busque **[!UICONTROL dc:format]**.

   El siguiente gráfico es un ejemplo de la ruta de un recurso al formato dc:format.

   ![chlimage_1-512](assets/chlimage_1-512.png)

   Observe que `dc:format` para el recurso `Fiji Red.jpg` es `image/jpeg`.

   Para que este filtro se aplique a todas las imágenes, independientemente de su formato, establezca el valor en `image/*` donde `*` es una expresión regular que se aplica a todas las imágenes de cualquier formato.

   Para que el filtro se aplique solo a imágenes del tipo JPEG, introduzca un valor de `image/jpeg`.

1. Defina qué representaciones desea incluir o excluir de la replicación.

   Los caracteres que se pueden usar para filtrar para la replicación son los siguientes:

<table>
 <tbody>
  <tr>
   <td><strong>Carácter que se va a usar</strong></td>
   <td><strong>Cómo se filtran los recursos para la replicación</strong></td>
  </tr>
  <tr>
   <td>*</td>
   <td>Carácter comodín<br /> </td>
  </tr>
  <tr>
   <td>+</td>
   <td>Incluye recursos para replicación.</td>
  </tr>
  <tr>
   <td>-</td>
   <td>Excluye los recursos de la replicación.</td>
  </tr>
 </tbody>
</table>

Ir a `content/dam/<locate your asset>/jcr:content/renditions`.

El siguiente gráfico es un ejemplo de las representaciones de un recurso.

![chlimage_1-513](assets/chlimage_1-4.png)

Con el ejemplo anterior, si solo desea replicar el PTIFF (TIFF piramidal), debe introducir `+cqdam,*` que incluye todas las representaciones que comienzan por `cqdam`. En el ejemplo, esa representación es `cqdam.pyramid.tiff`.

Si solo desea replicar el original, entonces debe introducir `+original`.

## Configuración de Dynamic Media Image Server {#configuring-dynamic-media-image-server-settings}

La configuración de Dynamic Media Image Server implica la edición del paquete Adobe CQ Scene7 ImageServer y del paquete Adobe CQ Scene7 Platform Server.

>[!NOTE]
Dynamic Media funciona de forma predeterminada [después de estar habilitado](#enabling-dynamic-media). Sin embargo, si lo desea, puede ajustar la instalación configurando Dynamic Media Image Server para que cumpla determinadas especificaciones o requisitos.

**Requisito previo**:  ** Antes de configurar Dynamic Media Image Server, asegúrese de que la VM de Windows® incluya una instalación de las bibliotecas Microsoft® Visual C++. Las bibliotecas son necesarias para ejecutar Dynamic Media Image Server. Puede [descargar el paquete redistribuible de Microsoft® Visual C++ 2010 (x64) aquí](https://www.microsoft.com/en-us/download/details.aspx?id=26999).

Para definir la configuración del servidor de imágenes de Dynamic Media:

1. En la esquina superior izquierda del Experience Manager, pulse **[!UICONTROL Adobe Experience Manager]** para acceder a la consola de navegación global y, a continuación, pulse **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
1. En la página Configuración de la consola web de Adobe Experience Manager, pulse **[!UICONTROL OSGi > Configuración]** para enumerar todos los paquetes que se están ejecutando actualmente en el Experience Manager.

   Los servidores de envío de Dynamic Media se encuentran en los nombres siguientes de la lista:

   * `Adobe CQ Scene7 ImageServer`
   * `Adobe CQ Scene7 PlatformServer`

1. En la lista de paquetes, a la derecha de Adobe CQ Scene7 ImageServer, pulse el icono **[!UICONTROL Editar]**.
1. En el cuadro de diálogo Adobe CQ Scene7 ImageServer, establezca los siguientes valores de configuración:

   >[!NOTE]
   Normalmente, no es necesario cambiar los valores predeterminados. Sin embargo, si cambia los valores predeterminados, debe reiniciar el paquete para que los cambios surtan efecto.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Valor predeterminado</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>TcpPort.name</td>
   <td><code><em>empty</em></code></td>
   <td>Número de puerto que se utilizará para la comunicación con el proceso ImageServer. De forma predeterminada, el puerto libre se detecta automáticamente.</td>
  </tr>
  <tr>
   <td>AllowRemoteAccess.name</td>
   <td><code><em>empty</em></code></td>
   <td><p>Permitir o no permitir el acceso remoto al proceso ImageServer. Si es false, el servidor de imágenes escucha solo en localhost.</p> <p>La configuración predeterminada del externalizador que señala al host local debe especificar el dominio o la dirección IP reales de la instancia de VM específica. El motivo es que el host local apunta al sistema principal de la VM.</p> <p>Los dominios o las direcciones IP de la VM deben tener una entrada de archivo host para que pueda resolverse a sí misma.</p> </td>
  </tr>
  <tr>
   <td>MaxRenderRgnPixels</td>
   <td>16 MPíxeles</td>
   <td>Tamaño máximo en megapíxeles procesados.</td>
  </tr>
  <tr>
   <td>MaxMessageSize</td>
   <td>16 MBytes</td>
   <td>Tamaño máximo del mensaje en megabytes que se entrega.</td>
  </tr>
  <tr>
   <td>RandomAccessUrlTimeout</td>
   <td>20</td>
   <td>Valor de tiempo de espera de tiempo de espera durante segundos que el servidor de imágenes espera a que el JCR responda a una solicitud de mosaico de rango.</td>
  </tr>
  <tr>
   <td>Subprocesos de trabajo</td>
   <td>10</td>
   <td>Número de subprocesos de trabajo.</td>
  </tr>
 </tbody>
</table>

1. Toque **[!UICONTROL Guardar]**.
1. En la lista de paquetes, a la derecha de Adobe CQ Scene7 Platform Server, pulse el icono **[!UICONTROL Editar]**.
1. En el cuadro de diálogo Adobe CQ Scene7 Platform Server, establezca las siguientes opciones de valor predeterminadas:

   >[!NOTE]
   Dynamic Media Image Server utiliza su propia caché de disco para almacenar en caché las respuestas. La caché HTTP del Experience Manager y Dispatcher no se pueden usar para almacenar en caché las respuestas del servidor de imágenes de Dynamic Media.

   | Propiedad | Valor predeterminado | Descripción |
   |---|---|---|
   | Caché habilitada | Activados | Indica si la caché de respuesta está habilitada |
   | Raíz de caché | cache | Una o más rutas a las carpetas de caché de respuestas. Las rutas relativas se resuelven en la carpeta interna del paquete de imágenes s7imaging. |
   | Tamaño máximo de caché | 20000000 | Tamaño máximo de la caché de respuesta en bytes. |
   | Entradas máximas en caché | 100 000 | Número máximo de entradas permitidas en la caché. |

### Configuración de manifiesto predeterminada {#default-manifest-settings}

El manifiesto predeterminado permite configurar los valores predeterminados que se utilizan para generar las respuestas de entrega de Dynamic Media. Puede ajustar la calidad (calidad JPEG, resolución, modo de remuestreo), el almacenamiento en caché (caducidad) y evitar la representación de imágenes demasiado grandes (defaultpix, defaultthumbpix, maxpix).

La ubicación de la configuración de manifiesto predeterminada se toma del valor predeterminado **[!UICONTROL Catalog root]** del paquete **[!UICONTROL Adobe CQ Scene7 Platform Server]**. De forma predeterminada, este valor se encuentra en la siguiente ruta dentro de **[!UICONTROL Tools > General > CRXDE Lite]**:

`/conf/global/settings/dam/dm/imageserver/`

![Configuración del servidor de imágenes en el CRXDE Lite](assets/configimageservercrxdelite.png)

Puede cambiar los valores de las propiedades, como se describe en la tabla siguiente, introduciendo nuevos valores.

Cuando haya terminado de cambiar el manifiesto predeterminado, en la esquina superior izquierda de la página, pulse **[!UICONTROL Guardar todo]**.

Asegúrese de pulsar la pestaña **[!UICONTROL Control de acceso]** (a la derecha de la pestaña Propiedades) y, a continuación, establezca los privilegios de control de acceso en `jcr:read` para todos los usuarios y para los usuarios de replicación de Dynamic Media.

![Configuración del servidor de imágenes en el CRXDE Lite y configuración de la ficha Control de acceso](assets/configimageservercrxdeliteaccesscontroltab.png)

Tabla de configuración de manifiesto y sus valores predeterminados:

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Valor predeterminado</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>bkgcolor</td>
   <td>FFFFFF</td>
   <td><p>Color de fondo predeterminado. Valor RGB utilizado para rellenar cualquier área de una imagen de respuesta que no contenga datos de imagen reales.</p> <p>Consulte también <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html#image-serving-api">BkgColor</a> en la API de servicio de imágenes.</p> </td>
  </tr>
  <tr>
   <td>defaultpix</td>
   <td>300.300</td>
   <td><p>Tamaño de vista predeterminado. El servidor restringe el tamaño de las imágenes de respuesta a un tamaño no mayor que este ancho y alto, si la solicitud no especifica el tamaño de vista explícitamente mediante wid=, hei= o scl=.</p> <p>Se especifica como dos números enteros, 0 o más, separados por coma. Anchura y altura en píxeles. Puede establecerse uno o ambos valores en 0 para mantenerlos sin restricciones. No se aplica a solicitudes anidadas/incrustadas.</p> <p>Consulte también <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html#image-serving-api">DefaultPix</a> en la API de servicio de imágenes.</p> <p>Sin embargo, normalmente se utiliza un ajuste preestablecido de visor o de imagen para entregar el recurso. Defaultpix solo se aplica a un recurso que no utiliza un ajuste preestablecido de visor o de imagen.</p> </td>
  </tr>
  <tr>
   <td>defaultthumbpix</td>
   <td>100.100</td>
   <td><p>Tamaño de miniatura predeterminado. Se utiliza en lugar del atributo::DefaultPix para solicitudes de miniatura (req=tmb).</p> <p>El servidor restringe el tamaño de las imágenes de respuesta para que no superen esta anchura y altura. Esta acción es verdadera si una solicitud de miniatura (req=tmb) no especifica el tamaño explícitamente y no especifica el tamaño de la vista utilizando `wid=`, `hei=` o `scl=`.</p> <p>Se especifica como dos números enteros, 0 o más, separados por coma. Anchura y altura en píxeles. Puede establecerse uno o ambos valores en 0 para mantenerlos sin restricciones. </p> <p>No se aplica a solicitudes anidadas/incrustadas.</p> <p>Consulte también <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html#image-serving-api">DefaultThumbPix</a> en la API de servicio de imágenes. </p> </td>
  </tr>
  <tr>
   <td>caducidad</td>
   <td>3600000</td>
   <td><p>Tiempo de vida predeterminado de la caché del cliente. Proporciona un intervalo de caducidad predeterminado en caso de que un registro de catálogo en particular no contenga un valor de catálogo válido::Expiration .</p> <p>Número real, 0 o bueno. Número de milisegundos hasta la caducidad desde que se generaron los datos de respuesta. Establézcalo en 0 para que siempre caduque la imagen de respuesta inmediatamente, lo que deshabilita efectivamente el almacenamiento en caché del cliente. De forma predeterminada, este valor se establece en 10 horas, lo que significa que si se publica una nueva imagen, tardará 10 horas en que la imagen antigua deje la caché del usuario. Póngase en contacto con el Servicio de atención al cliente si necesita que la caché se borre antes.</p> <p>Consulte también <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html">Caducidad</a> en la API de servicio de imágenes.</p> </td>
  </tr>
  <tr>
   <td>jpegquality</td>
   <td>80</td>
   <td><p>Atributos de codificación JPEG predeterminados. Especifica los atributos predeterminados para las imágenes de respuesta JPEG.</p> <p>Número entero y marca, separados por coma. El primer valor está en el rango 1.100 y define la calidad. El segundo valor puede ser 0 para el comportamiento normal o 1 para desactivar el muestreo descendente de cromaticidad RGB empleado por los codificadores JPEG.</p> <p>Consulte también <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html#image-serving-api">JpegQuality</a> en la API de servicio de imágenes.</p> </td>
  </tr>
  <tr>
   <td>maxpix</td>
   <td>2.000.2000</td>
   <td><p>Responder límite de tamaño de imagen. Ancho y alto máximo de la imagen de respuesta que se devuelve al cliente.</p> <p>El servidor devuelve un error si una solicitud causa una imagen de respuesta cuyo ancho o alto es mayor que el atributo::MaxPix.</p> <p>Consulte también <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html?lang=en#image-serving-api">MaxPix</a> en la API de servicio de imágenes.</p> </td>
  </tr>
  <tr>
   <td>resmode</td>
   <td>SHARP2</td>
   <td><p>Modo de remuestreo predeterminado. Especifica los atributos de remuestreo e interpolación predeterminados que se utilizarán para escalar datos de imagen.</p> <p>Se utiliza cuando resMode= no se especifica en una solicitud.</p> <p>Los valores permitidos incluyen BILIN, BICUB o SHARP2.</p> <p>Enum. Establézcalo en 2 para bilin, 3 para bicub o 4 para modo de interpolación de agudo2. Utilice Sharp2 para obtener los mejores resultados.</p> <p>Consulte también <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html#image-serving-api">ResMode</a> en la API de servicio de imágenes.</p> </td>
  </tr>
  <tr>
   <td>resolución</td>
   <td>72</td>
   <td><p>Resolución de objeto predeterminada. Proporciona una resolución de objeto predeterminada en caso de que un registro de catálogo concreto no contenga un valor de catálogo válido::Resolution .</p> <p>Número real, mayor que 0. Normalmente se expresa como píxeles por pulgada, pero también puede estar en otras unidades, como píxeles por metro.</p> <p>Consulte también <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-resolution.html#image-serving-api">Resolution</a> en la API de servicio de imágenes.</p> </td>
  </tr>
  <tr>
   <td>thumbnailtime</td>
   <td>1%,11%,21%,31%,41%,51%,61%,71%,81%,91%</td>
   <td>Estos valores representan una instantánea del tiempo de reproducción de vídeo y se pasan a <a href="https://www.encoding.com/">encoding.com</a>. Consulte <a href="/help/assets/video.md#about-video-thumbnails-in-dynamic-media-hybrid-mode">Acerca de las miniaturas de vídeo</a> para obtener más información.</td>
  </tr>
 </tbody>
</table>

## Configuración de la administración de color de Dynamic Media {#configuring-dynamic-media-color-management}

La gestión de color de Dynamic Media permite colorear los recursos correctos para la previsualización.

Con la corrección de color, los recursos incorporados conservan su espacio de color (RGB, CMYK, Gris) y su perfil de color incrustado en la representación TIFF de la pirámide generada. Cuando se solicita una representación dinámica, el color de la imagen se corrige en el espacio de color de destino. Puede configurar el perfil de color de salida en la configuración de publicación de Dynamic Media en el JCR.

La gestión de color de Adobe utiliza perfiles ICC (International Color Consortium), un formato definido por ICC.

Puede configurar la administración de color de Dynamic Media y los ajustes preestablecidos de imagen mediante la salida CMYK, RGB o Gris. Consulte [Configuración de ajustes preestablecidos de imagen](/help/assets/managing-image-presets.md).

Los casos de uso avanzados podrían utilizar un modificador `icc=` de configuración manual para seleccionar explícitamente un perfil de color de salida:

* `icc` -  [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html)

* `iccEmbed` -  [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html)

>[!NOTE]
El conjunto estándar de perfiles de color del Adobe solo está disponible si tiene [Feature Pack 12445 de Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-12445) instalado. Todos los paquetes de funciones y service packs están disponibles en [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). El paquete de características 12445 proporciona perfiles de color del Adobe.


### Instalación del Feature Pack 12445 {#installing-feature-pack}

Para utilizar las funcionalidades de administración de color de Dynamic Media, instale el paquete de características 12445.

**Para instalar el paquete de características 12445:**

1. Vaya a [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) y descargue `cq-6.3.0-featurepack-12445`.

   Consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md) para obtener más información sobre el uso de paquetes en [!DNL Adobe Experience Manager].

1. Instale el paquete de características.

### Configuración de los perfiles de color predeterminados {#configuring-the-default-color-profiles}

Después de instalar el paquete de características, configure los perfiles de color predeterminados adecuados para habilitar la corrección de color al solicitar datos de imagen RGB o CMYK.

**Para configurar los perfiles de color predeterminados**

1. En **[!UICONTROL Herramientas > General > CRXDE Lite]**, vaya a `/conf/global/settings/dam/dm/imageserver/jcr:content` que contiene los perfiles predeterminados de Adobe Color.

   ![chlimage_1-514](assets/chlimage_1-514.png)

1. Agregue una propiedad de corrección de color desplazándose hasta la parte inferior de la pestaña **[!UICONTROL Properties]**. Introduzca manualmente el nombre, tipo y valor de la propiedad, que se describe en las tablas siguientes. Después de introducir los valores, pulse **[!UICONTROL Add]** y **[!UICONTROL Save All]** para guardar los valores.

   Las propiedades de corrección de color se describen en la tabla **Propiedades de corrección de color**. Los valores que se pueden asignar a las propiedades de corrección de color se encuentran en la tabla **Perfil de color**.

   Por ejemplo, en **[!UICONTROL Name]**, añada `iccprofilecmyk`, seleccione **[!UICONTROL Type]** `String` y añada `WebCoated` como **[!UICONTROL Value]**. A continuación, pulse **[!UICONTROL Agregar]** y **[!UICONTROL Guardar todo]** para guardar los valores.

   ![chlimage_1-515](assets/chlimage_1-515.png)

   **Tabla de propiedades de corrección de color**

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Predeterminado</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html">iccprofilergb</a></td>
   <td>Cadena</td>
   <td>&lt;empty&gt;</td>
   <td>Nombre del perfil de color RGB predeterminado.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html">iccprofilecmyk</a></td>
   <td>Cadena</td>
   <td>&lt;empty&gt;</td>
   <td>Nombre del perfil de color CMYK predeterminado.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html">iccprofilegray</a></td>
   <td>Cadena</td>
   <td>&lt;empty&gt;</td>
   <td>Nombre del perfil de color gris predeterminado.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcrgb.html">iccprofilesrcrgb</a></td>
   <td>Cadena</td>
   <td>&lt;empty&gt;</td>
   <td>Nombre del perfil de color RGB predeterminado que se utiliza para imágenes RGB que no tienen un perfil de color incrustado</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrccmyk.html">iccprofilesrccmyk</a></td>
   <td>Cadena</td>
   <td>&lt;empty&gt;</td>
   <td>Nombre del perfil de color CMYK predeterminado utilizado para imágenes CMYK que no tienen un perfil de color incrustado.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcgray.html">iccprofilesrcgray</a></td>
   <td>Cadena</td>
   <td>&lt;empty&gt;</td>
   <td>Nombre del perfil de color gris predeterminado utilizado para imágenes CMYK que no tienen un perfil de color incrustado.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccblackpointcompensation.html">iccblackpointcompensación</a></td>
   <td>Booleano</td>
   <td>Verdadero</td>
   <td>Especifica si se realiza una compensación de punto negro durante la corrección de color. Adobe recomienda que esta configuración esté activada.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccdither.html">iccdither</a></td>
   <td>Booleano</td>
   <td>False</td>
   <td>Especifica si el vaciado se realiza durante la corrección de color.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html">iccrendertry</a></td>
   <td>Cadena</td>
   <td>relativo</td>
   <td><p>Especifica la interpretación. Los valores aceptables son: <strong>perceptual, relativo, saturación, absoluto. </strong><i></i>Adobe recomienda  <strong>relativo  </strong><i></i>como valor predeterminado.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
Los nombres de propiedades distinguen entre mayúsculas y minúsculas y deben escribirse todos en minúsculas.

**Tabla de perfil de color**

Están instalados los siguientes perfiles de color:

<table>
 <tbody>
  <tr>
   <th><p>Nombre</p> </th>
   <th><p>Espacio color</p> </th>
   <th><p>Descripción</p> </th>
  </tr>
  <tr>
   <td>AdobeRGB</td>
   <td>RGB</td>
   <td>Adobe RGB (1998)</td>
  </tr>
  <tr>
   <td>AppleRGB</td>
   <td>RGB</td>
   <td>Apple RGB</td>
  </tr>
  <tr>
   <td>CIERGB</td>
   <td>RGB</td>
   <td>CIE RGB</td>
  </tr>
  <tr>
   <td>CoatedFogra27</td>
   <td>CMYK</td>
   <td>Recubierto FOGRA27 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedFogra39</td>
   <td>CMYK</td>
   <td>Recubierto FOGRA39 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedGraCol</td>
   <td>CMYK</td>
   <td>Recubierto GRACoL 2006 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>ColorMatchRGB</td>
   <td>RGB</td>
   <td>ColorMatch RGB</td>
  </tr>
  <tr>
   <td>EuropeISOCoated</td>
   <td>CMYK</td>
   <td>Europa ISO Coated FOGRA27</td>
  </tr>
  <tr>
   <td>EuroscaleCoated</td>
   <td>CMYK</td>
   <td>Euroscale Coated v2</td>
  </tr>
  <tr>
   <td>EuroscaleUncovered</td>
   <td>CMYK</td>
   <td>Euroscale Uncovered v2</td>
  </tr>
  <tr>
   <td>JapanColorCoated</td>
   <td>CMYK</td>
   <td>Color japonés 2001 recubierto</td>
  </tr>
  <tr>
   <td>Diario JapanColor</td>
   <td>CMYK</td>
   <td>Diario Japan Color 2002</td>
  </tr>
  <tr>
   <td>JapanColorUncovered</td>
   <td>CMYK</td>
   <td>Color japonés 2001 sin recubrir</td>
  </tr>
  <tr>
   <td>JapanColorWebCoated</td>
   <td>CMYK</td>
   <td>Japan Color 2003 Web Coated</td>
  </tr>
  <tr>
   <td>JapanWebCoated</td>
   <td>CMYK</td>
   <td>Japón Web Coated (anuncio)</td>
  </tr>
  <tr>
   <td>NewsprintSNAP2007</td>
   <td>CMYK</td>
   <td>US Newsprint (SNAP 2007)</td>
  </tr>
  <tr>
   <td>NTSC</td>
   <td>RGB</td>
   <td>NTSC (1953)</td>
  </tr>
  <tr>
   <td>PAL</td>
   <td>RGB</td>
   <td>PAL/SECAM</td>
  </tr>
  <tr>
   <td>ProPhoto</td>
   <td>RGB</td>
   <td>ProPhoto RGB</td>
  </tr>
  <tr>
   <td>PS4Default</td>
   <td>CMYK</td>
   <td>CMYK predeterminado de Photoshop 4</td>
  </tr>
  <tr>
   <td>PS5Default</td>
   <td>CMYK</td>
   <td>CMYK predeterminado de Photoshop 5</td>
  </tr>
  <tr>
   <td>Coated</td>
   <td>CMYK</td>
   <td>U.S. Sheetfeed Coated v2</td>
  </tr>
  <tr>
   <td>SheetedUncovered</td>
   <td>CMYK</td>
   <td>U.S. Sheetfeed Uncovered v2</td>
  </tr>
  <tr>
   <td>SMPTE</td>
   <td>RGB</td>
   <td>SMPTE-C</td>
  </tr>
  <tr>
   <td>sRGB</td>
   <td>RGB</td>
   <td>sRGB IEC61966-2.1</td>
  </tr>
  <tr>
   <td>FograNoCubierta29</td>
   <td>CMYK</td>
   <td>FOGRA29 no recubierto (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoated</td>
   <td>CMYK</td>
   <td>U.S. Web Coated (SWOP) v2</td>
  </tr>
  <tr>
   <td>WebCoatedFogra28</td>
   <td>CMYK</td>
   <td>Web Coated FOGRA28 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoatedGrade3</td>
   <td>CMYK</td>
   <td>Papel Web Coated SWOP 2006 Grado 3</td>
  </tr>
  <tr>
   <td>WebCoatedGrade5</td>
   <td>CMYK</td>
   <td>Papel Web Coated SWOP 2006 Grado 5</td>
  </tr>
  <tr>
   <td>WebUncovered</td>
   <td>CMYK</td>
   <td>U.S. Web Uncovered v2</td>
  </tr>
  <tr>
   <td>WideGamutRGB</td>
   <td>RGB</td>
   <td>RGB de gama amplia</td>
  </tr>
 </tbody>
</table>

1. Toque **[!UICONTROL Guardar todo]**.

Por ejemplo, puede configurar **[!UICONTROL iccprofilergb]** en `sRGB` y **[!UICONTROL iccprofilecmyk]** en **[!UICONTROL WebCoated]**.

Al hacerlo, se haría lo siguiente:

* Habilita la corrección de color para imágenes RGB y CMYK.
* Se supone que las imágenes RGB que no tienen un perfil de color están en el espacio de color *sRGB*.
* Las imágenes CMYK que no tienen un perfil de color se presuponen que están en *espacio de color WebCoated*.
* Representaciones dinámicas que devuelven la salida RGB, la devuelven en el *sRGB *espacio de color.
* Representaciones dinámicas que devuelven la salida CMYK, la devuelven en el espacio de color *WebCoated*.

## Distribución de recursos {#delivering-assets}

Después de completar todas las tareas anteriores, los recursos de Dynamic Media activados se proporcionan desde Image o Video Service. En el Experience Manager, esta capacidad se muestra en **[!UICONTROL Copiar URL de imagen]**, **[!UICONTROL Copiar URL del visor]**, **[!UICONTROL Incrustar código del visor]** y en WCM.

Consulte [Entrega de recursos de Dynamic Media](/help/assets/delivering-dynamic-media-assets.md).

<table>
 <tbody>
  <tr>
   <td><strong>Cuando...</strong></td>
   <td><strong>Resultado</strong></td>
  </tr>
  <tr>
   <td>Copiar una URL de imagen</td>
   <td><p>El cuadro de diálogo Copiar URL muestra una dirección URL similar a la siguiente (la dirección URL es solo para fines de demostración):</p> <p><code>https://IMAGESERVICEPUBLISHNODE/is/image/content/dam/path/to/Image.jpg?$preset$</code></p> <p>Donde <code>IMAGESERVICEPUBLISHNODE</code> hace referencia a la URL del servicio de imágenes.</p> <p>Consulte también <a href="/help/assets/delivering-dynamic-media-assets.md">Entrega de recursos de Dynamic Media</a>.</p> </td>
  </tr>
  <tr>
   <td>Copiar una URL de visor</td>
   <td><p>El cuadro de diálogo Copiar URL muestra una dirección URL similar a la siguiente (la dirección URL es solo para fines de demostración):</p> <p><code>https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/BasicZoomViewer.html?asset=/content/dam/path/to/Image.jpg&amp;config=/conf/global/settings/dam/dm/presets/viewer/Zoom_dark&amp;serverUrl=https://IMAGESERVICEPUBLISHNODE/is/image/&amp;contentRoot=%2F</code></p> <p>Donde <code>PUBLISHNODE</code> hace referencia al nodo de publicación del Experience Manager normal y <code>IMAGESERVICEPUBLISHNODE</code> hace referencia a la URL del servicio de imagen.</p> <p>Consulte también <a href="/help/assets/delivering-dynamic-media-assets.md">Entrega de recursos de Dynamic Media</a>.</p> </td>
  </tr>
  <tr>
   <td>Copiar el código incrustado de un visor</td>
   <td><p>El cuadro de diálogo Copiar código incrustado muestra un fragmento de código similar al siguiente (el ejemplo de código es solo para fines de demostración):</p> <p><code class="code">&lt;style type="text/css"&gt;
       #s7basiczoom_div.s7basiczoomviewer{
       width:100%;
       height:auto;
       }
       &lt;/style&gt;
       &lt;script
       type="text/javascript" src="https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/js/BasicZoomViewer.js"&gt;&lt;/script&gt;
       &lt;div id="s7basiczoom_div"&gt;&lt;/div&gt;
       &lt;script type="text/javascript"&gt;
       var s7basiczoomviewer = new s7viewers.BasicZoomViewer({
       "containerId" : "s7basiczoom_div",
       "params" : {
       "serverurl" : "https://IMAGESERVICEPUBLISHNODE/is/image/",
       "contenturl" : "https://PUBLISHNODE/",
       "config" : "/conf/global/settings/dam/dm/presets/viewer/Zoom_dark",
       "asset" : "/content/dam/path/to/Image.jpg" }
       }).init();
       &lt;/script&gt;</code></p> <p>Donde <code>PUBLISHNODE</code> hace referencia al nodo de publicación del Experience Manager normal y <code>IMAGESERVICEPUBLISHNODE</code> hace referencia a la URL del servicio de imagen.</p> <p>Consulte también <a href="/help/assets/delivering-dynamic-media-assets.md">Entrega de recursos de Dynamic Media</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Componentes de WCM Dynamic Media y Medios interactivos {#wcm-dynamic-media-and-interactive-media-components}

Las páginas WCM que hacen referencia a componentes de Dynamic Media y Medios interactivos hacen referencia al servicio de entrega.
