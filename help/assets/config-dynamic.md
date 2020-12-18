---
title: Configuración de Dynamic Media - Modo híbrido
description: Obtenga información sobre cómo configurar Dynamic Media en modo híbrido.
uuid: 39ad7d83-d310-4baf-9d85-5532c2f201f3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 7d8e7273-29f3-4a45-ae94-aad660d2c71d
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/config-dynamic
translation-type: tm+mt
source-git-commit: e95f26cc1a084358b6bcb78605e3acb98f257b66
workflow-type: tm+mt
source-wordcount: '7835'
ht-degree: 1%

---


# Configuración de Dynamic Media - Modo híbrido {#configuring-dynamic-media-hybrid-mode}

Dynamic Media-Hybrid debe habilitarse y configurarse para su uso. Según el caso de uso, Dynamic Media tiene varias [configuraciones admitidas](#supported-dynamic-media-configurations).

>[!NOTE]
>
>Si desea configurar y ejecutar Dynamic Media en modo de ejecución de Scene7, consulte [Configuración de Dynamic Media - modo Scene7](/help/assets/config-dms7.md).
>
>Si desea configurar y ejecutar Dynamic Media en modo de ejecución híbrido, siga las instrucciones de esta página.

Obtenga más información sobre cómo trabajar con [video](/help/assets/video.md) en Dynamic Media.

>[!NOTE]
>
>Si utiliza la configuración de Adobe Experience Manager para diferentes entornos, como uno para desarrollo, uno para ensayo y otro para producción en directo, debe configurar Cloud Services de Dynamic Media para cada uno de esos entornos.

>[!NOTE]
>
>Si tiene problemas con la configuración de Dynamic Media, un lugar importante para ver son los archivos de registro específicos de los medios dinámicos. Estos se instalan automáticamente al activar Dynamic Media:
>
>* `s7access.log`
>* `ImageServing.log`

>
>
Están documentados en [Monitoreo y mantenimiento de la instancia de AEM](/help/sites-deploying/monitoring-and-maintaining.md).

La publicación y el envío híbridos es una característica central de la incorporación de Dynamic Media a Adobe Experience Manager. La publicación híbrida permite distribuir recursos de Dynamic Media, como imágenes, conjuntos y vídeos, desde la nube en lugar de desde los nodos de publicación AEM.

Otros contenidos, como los visores de Dynamic Media, las páginas del sitio y el contenido estático, se seguirán ofreciendo desde los nodos de publicación de AEM.

Si es cliente de Dynamic Media, debe utilizar el envío híbrido como mecanismo de envío para todo el contenido de Dynamic Media.

## Arquitectura de publicación híbrida para vídeos {#hybrid-publishing-architecture-for-videos}

![chlimage_1-506](assets/chlimage_1-428.png)

## Arquitectura de publicación híbrida para imágenes {#hybrid-publishing-architecture-for-images}

![chlimage_1-507](assets/chlimage_1-507.png)

## Configuraciones de Dynamic Media admitidas {#supported-dynamic-media-configurations}

Las tareas de configuración que siguen hacen referencia a los siguientes términos:

| **Término** | **Dynamic Media habilitado** | **Descripción** |
|---|---|---|
| Nodo de creación AEM | Marca de verificación blanca en círculo verde | El nodo de creación que implementa en On-Premise o a través de Managed Services. |
| AEM nodo de publicación | &quot;X&quot; blanca en un cuadrado rojo. | El nodo de publicación que implementa en On-Premise o a través de Managed Services. |
| Nodo de publicación de servicio de imágenes | Marca de verificación blanca en un círculo verde. | El nodo de publicación que se ejecuta en los centros de datos administrados por Adobe. Se refiere a la URL del servicio de imágenes. |

Puede elegir implementar Dynamic Media solo para imágenes, solo para vídeo o para imágenes y vídeo. Para determinar los pasos para configurar Dynamic Media para su escenario específico, consulte la siguiente tabla.

<table>
 <tbody>
  <tr>
   <td><strong>Escenario</strong></td>
   <td ><strong>Cómo funciona</strong></td>
   <td><strong>Pasos de configuración</strong></td>
  </tr>
  <tr>
   <td>Entregar SOLO imágenes en producción</td>
   <td>Las imágenes se entregan a través de servidores en los centros de datos mundiales de Adobe y luego se almacenan en caché mediante una CDN para obtener un rendimiento escalable y un alcance global.</td>
   <td>
    <ol>
     <li>En el nodo AEM <strong>author</strong>, <a href="#enabling-dynamic-media">habilite Dynamic Media</a>.</li>
     <li>Configure imágenes en <a href="#configuring-dynamic-media-cloud-services">Cloud Services de Dynamic Media</a>.</li>
     <li><a href="#configuring-image-replication">Configure la replicación</a> de imágenes.</li>
     <li><a href="#replicating-catalog-settings">Replicar la configuración</a> del catálogo.</li>
     <li><a href="#replicating-viewer-presets">Replicar ajustes preestablecidos</a> de visor.</li>
     <li><a href="#using-default-asset-filters-for-replication">Utilice filtros de recursos predeterminados para la replicación</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Configure los ajustes</a> de Dynamic Media Image Server.</li>
     <li><a href="#delivering-assets">Entregar recursos</a>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Distribuya SÓLO imágenes en la preproducción (Dev, QE, Stage, etc.)</td>
   <td>Las imágenes se entregan a través del nodo de publicación AEM. En este escenario, como el tráfico es mínimo, no es necesario entregar imágenes al centro de datos de Adobe. Una ventaja adicional es que esto permite una previsualización segura del contenido antes del inicio de la producción</td>
   <td>
    <ol>
     <li>En el nodo AEM <strong>author</strong>, <a href="#enabling-dynamic-media">habilite Dynamic Media</a>.</li>
     <li>En AEM nodo <strong>publish</strong>, <a href="#enabling-dynamic-media">habilite Dynamic Media</a>.</li>
     <li><a href="#replicating-viewer-presets">Replicar ajustes preestablecidos</a> de visor.</li>
     <li>Configure <a href="#setting-up-asset-filters-for-imaging-in-non-production-deployments">filtro de recursos para imágenes que no sean de producción</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Configuración de Dynamic Media Image Server.</a></li>
     <li><a href="#delivering-assets">Entregar recursos.</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Entregar SÓLO vídeo en cualquier entorno (producción, desarrollo, FC, etapa, etc.)</td>
   <td>Los vídeos son entregados y almacenados en caché por una CDN para un rendimiento escalable y un alcance global. La imagen del póster de vídeo (miniatura del vídeo que se muestra antes de que se inicie la reproducción) la proporcionará la instancia de publicación de AEM.</td>
   <td>
    <ol>
     <li>En el nodo AEM <strong>author</strong>, <a href="#enabling-dynamic-media">habilite Dynamic Media</a>.</li>
     <li>En el nodo AEM <strong>publish</strong>, <a href="#enabling-dynamic-media">habilite Dynamic Media</a> (la instancia de publicación sirve la imagen del póster de vídeo y proporciona metadatos para la reproducción de vídeo).</li>
     <li>Configurar vídeo en <a href="#configuring-dynamic-media-cloud-services">Cloud Services de Dynamic Media.</a></li>
     <li><a href="#replicating-viewer-presets">Replicar ajustes preestablecidos</a> de visor.</li>
     <li>Configure <a href="#setting-up-asset-filters-for-video-only-deployments">filtro de recursos para solo vídeo</a>.</li>
     <li><a href="#delivering-assets">Entregar recursos.</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Entregar imágenes y vídeos en producción</td>
   <td><p>Los vídeos son entregados y almacenados en caché por una CDN para un rendimiento escalable y un alcance global. Las imágenes y las imágenes de póster de vídeo se entregan a través de los servidores de los centros de datos internacionales de Adobe y, a continuación, se almacenan en caché mediante una CDN para obtener un rendimiento escalable y un alcance global.</p> <p>Consulte las secciones anteriores para configurar la imagen o el vídeo en la preproducción. </p> </td>
   <td>
    <ol>
     <li>En el nodo AEM <strong>author</strong>, <a href="#enabling-dynamic-media">habilite Dynamic Media</a>.</li>
     <li>Configurar vídeo en <a href="#configuring-dynamic-media-cloud-services">Cloud Services de Dynamic Media.</a></li>
     <li>Configure imágenes en <a href="#configuring-dynamic-media-cloud-services">Cloud Services de Dynamic Media.</a></li>
     <li><a href="#configuring-image-replication">Configure la replicación</a> de imágenes.</li>
     <li><a href="#replicating-catalog-settings">Replicar la configuración</a> del catálogo.</li>
     <li><a href="#replicating-viewer-presets">Replicar ajustes preestablecidos</a> de visor.</li>
     <li><a href="#using-default-asset-filters-for-replication">Utilice filtros de recursos predeterminados para la replicación.</a></li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Configuración de Dynamic Media Image Server.</a></li>
     <li><a href="#delivering-assets">Entregar recursos.</a></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Habilitación de Dynamic Media {#enabling-dynamic-media}

[Medios dinámicos ](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html) deshabilitados de forma predeterminada. Para aprovechar las funciones de Dynamic Media, debe habilitar los medios dinámicos utilizando el modo de ejecución `dynamicmedia` como lo haría, por ejemplo, el modo de ejecución `publish`. Antes de habilitarlo, asegúrese de revisar los [requisitos técnicos.](/help/sites-deploying/technical-requirements.md#requirements-for-aem-dynamic-media-add-on)

>[!NOTE]
>
>Al habilitar los medios dinámicos a través del modo de ejecución, se reemplaza la funcionalidad de AEM 6.1 y AEM 6.0, donde se habilita el medio dinámico estableciendo el indicador `dynamicMediaEnabled` en **[!UICONTROL true.]** Este indicador no tiene funcionalidad en AEM 6.2 y posterior. Además, no es necesario reiniciar el inicio rápido para habilitar los medios dinámicos.

Al habilitar Dynamic Media, las funciones de Dynamic Media estarán disponibles en la interfaz de usuario y cada recurso de imagen cargado recibirá una *representación cqdam.pyramid.tiff* que se utiliza para un envío rápido de las representaciones de imágenes dinámicas. Estos PTIFF tienen ventajas significativas, como (1) la capacidad de administrar sólo una imagen de origen principal única y generar infinitas representaciones sobre la marcha sin ningún almacenamiento adicional y (2) la capacidad de utilizar la visualización interactiva como zoom, recorrido, giro, etc.

Si desea utilizar Dynamic Media Classic (Scene7) en AEM, no debe habilitar Dynamic Media a menos que utilice un [escenario específico](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media). Dynamic Media está desactivado a menos que active Dynamic Media mediante el modo de ejecución.

Para activar Dynamic Media, debe habilitar el modo de ejecución de Dynamic Media desde la línea de comandos o desde el nombre del archivo de inicio rápido.

**Para activar Dynamic Media**

1. En la línea de comandos, al iniciar el inicio rápido, haga lo siguiente:

   * Añada `-r dynamicmedia` al final de la línea de comandos al iniciar el archivo jar.

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -r dynamicmedia
   ```

   Si está publicando en s7envío, también debe incluir los siguientes argumentos trustStore:

   ```
   -Djavax.net.ssl.trustStore=<absoluteFilePath>/customerTrustStoreFileName>
   
    -Djavax.net.ssl.trustStorePassword=<passwordForTrustStoreFile>
   ```

1. Solicite `https://localhost:4502/is/image` y asegúrese de que el servidor de imágenes se esté ejecutando.

   >[!NOTE]
   >
   >Para solucionar problemas con Dynamic Media, consulte los siguientes registros en el directorio `crx-quickstart/logs/`:
   >
   >* ImageServer-&lt;PortId>-&lt;yyyy>&lt;mm>&lt;dd>.log: el registro de ImageServer proporciona estadísticas e información analítica utilizadas para analizar el comportamiento del proceso interno de ImageServer.

   Ejemplo de un nombre de archivo de registro de Image Server: `ImageServer-57346-2020-07-25.log`
   * s7access-&lt;aaaa>&lt;mm>&lt;dd>.log: el registro de acceso s7registra cada solicitud realizada a Dynamic Media a través de `/is/image` y `/is/content`.

   Estos registros solo se utilizan cuando Dynamic Media está habilitado. No se incluyen en el paquete **Descargar completo** que se genera desde la página `system/console/status-Bundlelist`; cuando llame a Asistencia al cliente si tiene un problema con Dynamic Media, anexe ambos registros al problema.

### Si ha instalado AEM en otro puerto o ruta de contexto... {#if-you-installed-aem-to-a-different-port-or-context-path}

Si va a implementar [AEM en un servidor de aplicaciones](/help/sites-deploying/application-server-install.md) y tiene Dynamic Media habilitado, debe configurar el dominio **self** en el externalizador. De lo contrario, la generación de miniaturas para los recursos no funcionará correctamente en los recursos de medios dinámicos.

Además, si ejecuta el inicio rápido en un puerto o ruta de contexto diferente, también debe cambiar el dominio **self**.

Cuando Dynamic Media está activado, las representaciones de miniaturas estáticas para los recursos de imagen se generan mediante Dynamic Media. Para que la generación de miniaturas funcione correctamente en los medios dinámicos, AEM realizar una solicitud de URL a sí misma y debe conocer tanto el número de puerto como la ruta de contexto.

En AEM:

* El dominio **self** del [externalizador](/help/sites-developing/externalizer.md) se utiliza para recuperar el número de puerto y la ruta de contexto.
* Si no hay ningún dominio **self** configurado, el número de puerto y la ruta de contexto se recuperan del servicio HTTP Jetty.

En una implementación de QuickStart WAR de AEM, no se pueden derivar el número de puerto y la ruta de contexto, por lo tanto debe configurar un dominio **self**. Consulte [documentación de externalizer](/help/sites-developing/externalizer.md) sobre cómo configurar el dominio **self**.

>[!NOTE]
En una implementación independiente de [AEM QuickStart](/help/sites-deploying/deploy.md), generalmente no es necesario configurar un dominio **self** porque el número de puerto y la ruta de contexto se pueden configurar automáticamente. Sin embargo, si todas las interfaces de red están desactivadas, debe configurar el dominio **self**.

## Desactivación de Dynamic Media {#disabling-dynamic-media}

Los medios dinámicos no están activados de forma predeterminada. Sin embargo, si ha activado medios dinámicos anteriormente, puede que desee desactivarlos más adelante.

Para deshabilitar los medios dinámicos después de haberlos habilitado, debe quitar el indicador de modo de ejecución `-r dynamicmedia`.

**Para deshabilitar Dynamic Media después de haberla habilitado**

1. En la línea de comandos, al iniciar el inicio rápido, puede realizar una de las siguientes acciones:

   * No agregue `-r dynamicmedia` a la línea de comandos al iniciar el archivo jar.

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar
   ```

1. Solicitar `https://localhost:4502/is/image`. Recibirá un mensaje que indica que Dynamic Media está deshabilitado.

   >[!NOTE]
   Una vez deshabilitado el modo de ejecución de Dynamic Media, el paso del flujo de trabajo que genera la representación `cqdam.pyramid.tiff` se omite automáticamente. Esto también deshabilita la compatibilidad con representaciones dinámicas y otras funciones de Dynamic Media.
   Tenga en cuenta también que cuando el modo de ejecución de Dynamic Media está desactivado después de configurar el servidor de AEM, todos los recursos cargados en ese modo de ejecución no son válidos.

## (Opcional) Migración de ajustes preestablecidos y configuraciones de Dynamic Media de 6.3 a 6.5 Zero Downtime {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

Si está actualizando AEM Dynamic Media de 6.3 a 6.5 (lo que ahora incluye la capacidad de cero implementaciones de tiempo de inactividad), debe ejecutar el siguiente comando curl para migrar todos los ajustes preestablecidos y configuraciones de `/etc` a `/conf` en CRXDE Lite.

**Nota**: Si ejecuta la instancia de AEM en modo de compatibilidad (es decir, tiene instalado el paquete de compatibilidad), no es necesario ejecutar estos comandos.

Para todas las actualizaciones, ya sea con o sin el paquete de compatibilidad, puede copiar los ajustes preestablecidos de visor predeterminados y listos para usar que originalmente se incluyeron con Dynamic Media ejecutando el siguiente comando de control de Linux:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

Para migrar cualquier ajuste preestablecido de visor personalizado y configuración que haya creado de `/etc` a `/conf`, ejecute el siguiente comando de control de Linux:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## Configuración de la replicación de imágenes {#configuring-image-replication}

El envío de imágenes de Dynamic Media funciona mediante la publicación de recursos de imagen, incluidas miniaturas de vídeo, desde AEM Author y replicándolos en el servicio de replicación bajo demanda de Adobe (la URL del servicio de replicación). A continuación, los recursos se entregan mediante el servicio de envío de imágenes a petición (la URL del servicio de imágenes).

Debe hacer lo siguiente:

1. [Configure la autenticación](#setting-up-authentication).
1. [Configure el agente](#configuring-the-replication-agent) de replicación.

Replication Agent publica recursos de Dynamic Media como imágenes, metadatos de vídeo y conjuntos en el servicio de imágenes alojado en Adobe. El Agente de replicación no está habilitado de forma predeterminada.

Después de configurar el agente de replicación, debe [validar y probar que se configuró con éxito](#validating-the-replication-agent-for-dynamic-media). En esta sección se describen estos procedimientos.

>[!NOTE]
El límite de memoria predeterminado para la creación de PTIFF es de 3 GB en todos los flujos de trabajo. Por ejemplo, puede procesar una imagen que requiera 3 GB de memoria mientras se ponen en pausa otros flujos de trabajo, o puede procesar 10 imágenes en paralelo que requieran 300 MB de memoria cada una.
El límite de memoria es configurable y debe ajustarse a la disponibilidad de recursos del sistema y al tipo de contenido de imagen que se está procesando. Si tiene muchos recursos muy grandes y tiene suficiente memoria en el sistema, puede aumentar este límite para garantizar que las imágenes se procesen en paralelo.
Se rechazará una imagen que requiera más del límite máximo de memoria.
Para cambiar el límite de memoria para la creación de PTIFF, vaya a **[!UICONTROL Herramientas > Operaciones > Consola Web > Adobe CQ Scene7 PTiffManager]** y cambie el valor **[!UICONTROL maxMemory]**.

### Configuración de la autenticación {#setting-up-authentication}

Debe configurar la autenticación de replicación en el autor para replicar imágenes en el servicio de envío de imágenes de Dynamic Media. Para ello, obtenga un KeyStore y luego guárdelo bajo el **[!UICONTROL usuario de replicación de medios dinámicos]** y configúrelo. El administrador de compañía debería haber recibido un correo electrónico de bienvenida con el archivo KeyStore y las credenciales necesarias durante el proceso de aprovisionamiento. Si no recibió esto, póngase en contacto con el Servicio de atención al cliente.

**Para configurar la autenticación**

1. Póngase en contacto con el Servicio de atención al cliente para obtener el archivo y la contraseña de KeyStore si aún no lo tiene. Esto forma parte del aprovisionamiento y asociará las claves a su cuenta.
1. En AEM, toque el logotipo de AEM para acceder a la consola de navegación global y, a continuación, toque **[!UICONTROL Herramientas > Seguridad > Usuarios.]**
1. En la página Administración de usuarios, navegue hasta el **[!UICONTROL usuario de replicación de medios dinámicos]** y toque para abrir.

   ![dm-replicación](assets/dm-replication.png)

1. En la página Editar configuración de usuario para replicación de medios dinámicos, toque la ficha **[!UICONTROL Almacén de claves]** y haga clic en **[!UICONTROL Crear almacén de claves.]**

   ![dm-replicación-keystore](assets/dm-replication-keystore.png)

1. Escriba una contraseña y confirme la contraseña en el cuadro de diálogo **[!UICONTROL Establecer contraseña de acceso a KeyStore]**.

   >[!NOTE]
   Recuerde la contraseña introducida. Tendrá que volver a introducirlo cuando configure el Agente de replicación más adelante.

   ![chlimage_1-508](assets/chlimage_1-508.png)

1. En la página **[!UICONTROL Editar configuración de usuario para la replicación de medios dinámicos]**, expanda el área **Añadir clave privada del archivo KeyStore** y agregue lo siguiente (vea las imágenes que se muestran a continuación):

   * En el campo **[!UICONTROL Nuevo alias]**, introduzca el nombre de un alias que utilizará posteriormente en la configuración de replicación; por ejemplo, `replication`.
   * Toque **[!UICONTROL Archivo KeyStore.]** Vaya al archivo KeyStore que se le proporcionó por Adobe, selecciónelo y, a continuación, toque  **[!UICONTROL Abrir.]**
   * En el campo **[!UICONTROL Contraseña del archivo KeyStore]**, introduzca la contraseña del archivo KeyStore. Ésta es **no** la contraseña de KeyStore que creó en el paso 5, pero es el Adobe de contraseña de KeyStore File que se proporciona en el correo electrónico de bienvenida que se le envió durante el aprovisionamiento. Póngase en contacto con el servicio de atención al cliente de Adobe si no ha recibido una contraseña para el archivo KeyStore.
   * En el campo **[!UICONTROL Contraseña de clave privada]**, introduzca la contraseña de clave privada (puede ser la misma contraseña de clave privada proporcionada en el paso anterior). Adobe proporciona la contraseña de clave privada en el correo electrónico de bienvenida que se le ha enviado durante el aprovisionamiento. Póngase en contacto con el Servicio de atención al cliente de Adobe si no ha recibido una contraseña de clave privada.
   * En el campo **[!UICONTROL Alias de clave privada]**, introduzca el alias de clave privada. Por ejemplo, `*companyname*-alias`. Adobe proporciona el alias de clave privada en el correo electrónico de bienvenida que se le ha enviado durante el aprovisionamiento. Póngase en contacto con el Servicio de atención al cliente de Adobe si no recibió un alias de clave privada.

   ![edit_settings_fordynamic-media-Replication2](assets/edit_settings_fordynamic-media-replication2.png)

1. Toque **[!UICONTROL Guardar y cerrar]** para guardar los cambios en este usuario.

   A continuación, debe [configurar el agente de replicación.](#configuring-the-replication-agent)

### Configuración del Agente de replicación {#configuring-the-replication-agent}

1. En AEM, toque el logotipo de AEM para acceder a la consola de navegación global y, a continuación, toque **[!UICONTROL Herramientas > Implementación > Replicación > Agentes en el autor.]**
1. En la página Agentes del autor, toque **[!UICONTROL Replicación de imágenes híbridas de Dynamic Media (s7envío).]**
1. Toque **[!UICONTROL Editar.]**
1. Puntee en la ficha **[!UICONTROL Configuración]** y luego escriba lo siguiente:

   * **[!UICONTROL Habilitado]** : seleccione esta casilla de verificación para habilitar el agente de replicación.
   * **[!UICONTROL Región]** : se establece en la región adecuada: Norteamérica, Europa o Asia
   * **[!UICONTROL ID]**  del inquilino: este valor es el nombre de su compañía/inquilino que está publicando en el servicio de replicación. Este valor es el ID del inquilino que Adobe proporciona en el correo electrónico de bienvenida que se le envía durante el aprovisionamiento. Póngase en contacto con el Servicio de atención al cliente de Adobe si no ha recibido esto.
   * **[!UICONTROL Alias]**  de almacén de claves: este valor es el mismo que el valor** Nuevo alias** establecido al generar la clave en  [Configuración de autenticación](#setting-up-authentication); por ejemplo,  `replication`. (Consulte el paso 7 en [Configuración de la autenticación](#setting-up-authentication)).
   * **[!UICONTROL Contraseña]**  del almacén de claves: es la contraseña de KeyStore que se creó al tocar  **[!UICONTROL Crear KeyStore.]** Adobe no proporciona esta contraseña. Consulte el paso 5 de [Configuración de la autenticación](#setting-up-authentication).

   La siguiente imagen muestra el agente de replicación con datos de ejemplo:

   ![chlimage_1-509](assets/chlimage_1-509.png)

1. Toque **[!UICONTROL Aceptar.]**

### Validación del Agente de replicación para Dynamic Media {#validating-the-replication-agent-for-dynamic-media}

Para validar el agente de replicación para medios dinámicos, haga lo siguiente:

Toque **[!UICONTROL Conexión de prueba.]** El resultado de ejemplo es el siguiente:

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
También puede realizar una de las siguientes comprobaciones:
* Compruebe los registros de replicación para asegurarse de que el recurso se replica.
* Publique una imagen. Toque la imagen y seleccione **[!UICONTROL Visores]** en el menú desplegable. A continuación, seleccione un ajuste preestablecido de visor, haga clic en URL y copie o pegue la URL en el navegador para comprobar que puede ver la imagen.



### Solución de problemas de autenticación {#troubleshooting-authentication}

A la hora de configurar la autenticación, se presentan algunos problemas con sus soluciones. Antes de comprobarlos, asegúrese de haber configurado la replicación.

#### Problema: Código de estado HTTP 401 con mensaje - Autorización requerida {#problem-http-status-code-with-message-authorization-required}

Este problema puede deberse a un error al configurar KeyStore para `dynamic-media-replication` usuario.

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

**Solución**: Compruebe que  `KeyStore` se guarda en  **dynamic-media-** replicationuser y que se proporciona la contraseña correcta.

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

**Solución**: Compruebe la contraseña. La contraseña guardada en el agente de replicación no es la misma que se utilizó para crear el almacén de claves.

#### Problema: InvalidAlgorithmParameterException {#problem-invalidalgorithmparameterexception}

Este problema se debe a un error de configuración en la instancia de AEM Author. El proceso de Java del autor no está obteniendo el `javax.net.ssl.trustStore` correcto. Puede ver este error en el registro de replicación:

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

**Solución**: Asegúrese de que el proceso de Java de AEM Author tenga la propiedad del sistema  `-Djavax.net.ssl.trustStore=` establecida en un almacén de confianza válido.

#### Problema: KeyStore no está configurado o no se inicializa {#problem-keystore-is-either-not-set-up-or-it-is-not-initialized}

Este problema puede deberse a una corrección urgente o a que un paquete de funciones sobrescriba el nodo del almacén de claves o el usuario de Dynamic Media.

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

1. Vaya a la página Administración de usuarios:
   `localhost:4502/libs/granite/security/content/useradmin.html`
1. En la página Administración de usuarios, navegue hasta el usuario `dynamic-media-replication` y toque para abrir.
1. Haga clic en la ficha **[!UICONTROL KeyStore]**. Si aparece el botón **[!UICONTROL Crear KeyStore]**, debe rehacer los pasos que se encuentran en [Configuración de la autenticación](#setting-up-authentication) anteriormente.
1. Si tuvo que rehacer la configuración de KeyStore, es posible que tenga que [configurar el agente de replicación](/help/assets/config-dynamic.md#configuring-the-replication-agent) de nuevo.

   Vuelva a configurar el agente de replicación de s7envío.
   `localhost:4502/etc/replication/agents.author/s7delivery.html`

1. Toque **[!UICONTROL Probar conexión]** para verificar que la configuración es válida.

#### Problema: El Agente de publicación está usando SSL en lugar de OAuth {#problem-publish-agent-is-using-ssl-instead-of-oauth}

Este problema puede deberse a una corrección urgente o a un paquete de funciones que no se instaló correctamente o que sobrescribió la configuración.

Ejemplo de registro de replicación:

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

1. En AEM, haga clic en **[!UICONTROL Herramientas > General > CRXDE Lite.]**

   `localhost:4502/crx/de/index.jsp`

1. Vaya al nodo del agente de replicación de envío s7.
   `localhost:4502/crx/de/index.jsp#/etc/replication/agents.author/s7delivery/jcr:content`

1. Añada esta configuración en el agente de replicación (booleano con el valor establecido en **[!UICONTROL True]**):

   `enableOauth=true`

1. Cerca de la esquina superior izquierda de la página, toque **[!UICONTROL Guardar todo.]**

### Prueba de la configuración {#testing-your-configuration}

Adobe recomienda que realice una prueba end-to-end de la configuración.

Asegúrese de que ya ha hecho lo siguiente antes de comenzar esta prueba:

* Ajustes preestablecidos de imagen añadidos.
* Configure **[!UICONTROL Configuración de Dynamic Media (Pre 6.3)]** en Cloud Services. Se requiere la dirección URL del servicio de imágenes para esta prueba

**Para probar la configuración**

1. Cargue un recurso de imagen. (En Recursos, toque **[!UICONTROL Crear > Archivos]** y seleccione el archivo).
1. Espere a que finalice el flujo de trabajo.
1. Publique el recurso de imagen. (Seleccione el recurso y toque **[!UICONTROL Publicación rápida.]**)
1. Vaya a las representaciones de esa imagen abriendo la imagen y tocando **[!UICONTROL Representaciones.]**

   ![chlimage_1-510](assets/chlimage_1-510.png)

1. Seleccione cualquier representación dinámica.
1. Haga clic en **[!UICONTROL URL]** para obtener la dirección URL de este recurso.
1. Vaya a la dirección URL seleccionada y compruebe si la imagen se comporta como se espera.

Otra forma de comprobar que los recursos se han entregado es adjuntar req=exists a la dirección URL.

## Configuración de Cloud Services de Dynamic Media {#configuring-dynamic-media-cloud-services}

El servicio de Dynamic Media Cloud ofrece compatibilidad con servicios en la nube, como la publicación híbrida y el envío de imágenes y vídeos, análisis de vídeo y codificación de vídeo, entre otras cosas.

Como parte de la configuración, debe introducir un ID de registro, una URL de servicio de vídeo, una URL de servicio de imágenes, una URL de servicio de replicación y configurar la autenticación. Debería haber recibido toda esta información como parte del proceso de aprovisionamiento de cuentas. Si no ha recibido esta información, póngase en contacto con el administrador de Adobe Experience Manager o con el servicio de asistencia técnica de Adobe para obtener la información.

>[!NOTE]
Antes de configurar los servicios de Dynamic Media Cloud, asegúrese de tener configurada la instancia de publicación. También debe tener la replicación configurada antes de configurar los servicios de Dynamic Media Cloud.

Para configurar los servicios de nube de medios dinámicos:

1. En AEM, toque el logotipo de AEM para acceder a la consola de navegación global y toque **[!UICONTROL Herramientas > Cloud Services > Configuración de Dynamic Media (Pre-6.3).]**
1. En la página Explorador de configuración de Dynamic Media, en el panel izquierdo, seleccione **[!UICONTROL global]** y, a continuación, toque **[!UICONTROL Crear.]**
1. En el cuadro de diálogo **[!UICONTROL Crear configuración de Dynamic Media]**, en el campo Título, escriba un título.
1. Si está configurando Dynamic Media para vídeo,

   * En el campo **[!UICONTROL ID de registro]**, escriba su ID de registro.
   * En el campo **V[!UICONTROL URL del servicio de vídeo]**, introduzca la URL del servicio de vídeo para Dynamic Media Gateway.

1. Si está configurando Dynamic Media para imágenes, en el campo **[!UICONTROL URL del servicio de imágenes]**, introduzca la URL del servicio de imágenes para Dynamic Media Gateway.
1. Toque **[!UICONTROL Guardar]** para volver a la página del explorador de configuración de Dynamic Media.
1. Toque el logotipo AEM para acceder a la consola de navegación global.

## Configuración del Sistema de informes de vídeo {#configuring-video-reporting}

Puede configurar el sistema de informes de vídeo en varias instalaciones de AEM mediante Dynamic Media Hybrid.

**Cuándo utilizar:** al configurar la configuración de Dynamic Media (anterior a 6.3), se inician numerosas funciones, incluido el sistema de informes de vídeo. La configuración crea un grupo de informes en una compañía regional de Analytics. Si configura varios nodos Autor, creará un grupo de informes independiente para cada uno. Como resultado, los datos de sistema de informes son incoherentes entre las instalaciones. Además, si cada nodo Autor hace referencia al mismo servidor de publicación híbrido, la última instalación de Autor cambia el grupo de informes de destino para todos los sistemas de informes de vídeo. Este problema sobrecarga el sistema de Analytics con demasiados grupos de informes.

**Introducción:** Configuración del sistema de informes de vídeo completando las tres tareas siguientes.

1. Cree un paquete de ajustes preestablecidos de Video Analytics después de configurar Dynamic Media Configuration (Pre 6.3) en el primer nodo Author. Esta tarea inicial es importante porque permite que una nueva configuración continúe utilizando el mismo grupo de informes.
1. Instale el paquete de ajustes preestablecidos de Video Analytics en cualquier ***nuevo*** nodo de creación ***antes de*** configurar la Configuración de Dynamic Media (anterior a 6.3).
1. Compruebe y depure la instalación del paquete.

### Creación de un paquete de ajustes preestablecidos de Video Analytics después de configurar el primer nodo Autor {#creating-a-video-analytics-preset-package-after-configuring-the-first-author-node}

Cuando haya finalizado esta tarea, tendrá un archivo de paquete que contiene los ajustes preestablecidos de Video Analytics. Estos ajustes preestablecidos contienen un grupo de informes, el servidor de seguimiento, la Área de nombres de seguimiento y la ID de organización de Marketing Cloud, si están disponibles.

1. Si aún no lo ha hecho, configure la Configuración de Dynamic Media (Pre 6.3).
1. (Opcional) Vista y copie la ID del grupo de informes (debe tener acceso al JCR). Aunque no se requiere la ID del grupo de informes, la validación es más sencilla.
1. Cree un paquete mediante el Administrador de paquetes.
1. Edite el paquete para incluir un filtro.

   En AEM: `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

1. Cree el paquete.
1. Descargue o comparta el paquete de ajustes preestablecidos de Video Analytics para que se pueda compartir con los nuevos nodos de creación subsiguientes.

### Instalación del paquete de ajustes preestablecidos de Video Analytics antes de configurar nodos de creación adicionales {#installing-the-video-analytics-preset-package-before-you-configure-additional-author-nodes}

Asegúrese de completar esta tarea ***antes de*** configurar la Configuración de Dynamic Media (Pre 6.3). Si no lo hace, se crea otro grupo de informes no utilizado. Además, aunque el sistema de informes de vídeo seguirá funcionando correctamente, la recopilación de datos no se optimiza.

Asegúrese de que el paquete de ajustes preestablecidos de Video Analytics del primer nodo Autor esté accesible en el nuevo nodo Autor.

1. Cargue el paquete de ajustes preestablecidos de Video Analytics que creó anteriormente en el Administrador de paquetes.
1. Instale el paquete de ajustes preestablecidos de Video Analytics.
1. Configuración de Dynamic Media (anterior a 6.3).

### Verificación y depuración de la instalación del paquete {#verifying-and-debugging-the-package-installation}

1. Realice una de las siguientes acciones para verificar y, si es necesario, depurar la instalación del paquete:

   * **Compruebe el ajuste preestablecido de Video Analytics mediante**
JCRT Para comprobar el ajuste preestablecido de Video Analytics mediante el JCR, debe tener acceso al CRXDE Lite.

      AEM - En CRXDE Lite, navegue a `/conf/global/settings/
dam/dm/presets/analytics/jcr:content/userdata`

      Es `https://localhost:4502/crx/de/index.jsp#/conf/global/settings/dam/dm/presets/analytics/jcr%3Acontent/userdata`

      Si no tiene acceso al CRXDE Lite en el nodo Autor, puede comprobar el ajuste preestablecido a través del servidor de publicación.

   * **Compruebe el ajuste preestablecido de Video Analytics a través del servidor de imágenes**

      Puede validar el ajuste preestablecido de Video Analytics directamente realizando una solicitud req=userdata del servidor de imágenes.
Por ejemplo, para ver el ajuste preestablecido de Analytics en el nodo Autor, puede realizar la siguiente solicitud:

      `https://localhost:4502/is/image/conf/global/settings/dam/dm/presets/analytics?req=userdata`

      Para validar el ajuste preestablecido en servidores de publicación, puede realizar una solicitud directa similar en el servidor de publicación. Las respuestas son las mismas en los nodos Autor y Publicación. La respuesta es similar a la siguiente:**

      ```
      marketingCloudOrgId=0FC4E86B573F99CC7F000101
       reportSuite=aemaem6397618-2018-05-23
       trackingNamespace=aemvideodal
       trackingServer=aemvideodal.d2.sc.omtrdc.net
      ```

   * **Compruebe el ajuste preestablecido de Video Analytics a través de la herramienta Sistema de informes de vídeo en**
AEMTap  **[!UICONTROL Tools > Assets > Video Sistema de informes]**

      `https://localhost:4502/mnt/overlay/dam/gui/content/s7dam/videoreports/videoreport.html`

      Si ve el siguiente mensaje de error, el grupo de informes está disponible, pero sin rellenar. Este error es correcto (y deseado) en una nueva instalación antes de que el sistema recopile datos.
   ![screen_shot_2018-05-23at52254pm](assets/screen_shot_2018-05-23at52254pm.png)

   Para generar datos de sistema de informes, cargue y publique un vídeo. Utilice **[!UICONTROL Copiar URL]** y ejecute el vídeo al menos una vez.

   Tenga en cuenta que los datos de sistema de informes pueden tardar hasta 12 horas en completarse a partir del uso del visor de vídeo.

   Si hay un error y el grupo de informes no está configurado correctamente, se muestra la siguiente alerta.

   ![screen_shot_2018-05-23at52612pm](assets/screen_shot_2018-05-23at52612pm.png)

   Este error también se muestra si se ejecuta Video Sistema de informes antes de configurar los servicios de Dynamic Media Configuration (Pre 6.3).

### Resolución de problemas de la configuración del sistema de informes de vídeo {#troubleshooting-the-video-reporting-configuration}

* Durante la instalación, a veces se agota el tiempo de espera de las conexiones al servidor de la API de Analytics. La instalación reintentos la conexión 20 veces, pero sigue fallando. Cuando se produce esta situación, el archivo de registro registra varios errores. Buscar `SiteCatalystReportService`.
* Si no instala primero el paquete de ajustes preestablecidos de Analytics, puede crear un nuevo grupo de informes.
* Al actualizar de AEM 6.3 a AEM 6.4 o AEM 6.4.1 y, a continuación, configurar la Configuración de Dynamic Media (anterior a 6.3), se crea un grupo de informes. Se sabe que este problema se ha solucionado para AEM 6.4.2.

### Acerca del ajuste preestablecido de Video Analytics {#about-the-video-analytics-preset}

El ajuste preestablecido de Video Analytics (a veces conocido simplemente como ajuste preestablecido de análisis) se almacena junto a los ajustes preestablecidos de visor en Dynamic Media. Es básicamente lo mismo que un ajuste preestablecido de visor, pero con información utilizada para configurar AppMeasurement y el sistema de informes de Video Heartbeat.

Las propiedades del ajuste preestablecido son las siguientes:

* `reportSuite`
* `trackingServer`
* `trackingNamespace`
* `marketingCloudOrgId` (no está presente en versiones anteriores de AEM)

AEM 6.4 y versiones posteriores guardan este ajuste preestablecido en `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

## Replicando configuración de catálogo {#replicating-catalog-settings}

Debe publicar su propia configuración de catálogo predeterminada como parte del proceso de configuración mediante el JCR. Para replicar la configuración del catálogo:

1. En una ventana Terminal, ejecute lo siguiente:

   `curl -u admin:admin localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

1. En AEM, navegue a la siguiente ubicación en CRXDE Lite (requiere privilegios de administrador):

   `https://<*server*>:<*port*>/crx/de/index.jsp#/conf/global/settings/dam/dm/imageserver/`

1. Toque la ficha **[!UICONTROL Replicación]**.
1. Toque **[!UICONTROL Replicar.]**

## Replicar ajustes preestablecidos de visor {#replicating-viewer-presets}

Para entregar *un recurso con un ajuste preestablecido de visor, debe replicar/publicar* el ajuste preestablecido de visor. (Todos los ajustes preestablecidos de visor deben activarse *y* replicarse para obtener la URL o el código incrustado de un recurso.
Consulte [Ajustes preestablecidos de visor de publicaciones](/help/assets/managing-viewer-presets.md#publishing-viewer-presets) para obtener más información.

>[!NOTE]
De forma predeterminada, el sistema muestra una variedad de representaciones al seleccionar **[!UICONTROL Representaciones]** y una variedad de ajustes preestablecidos de visor al seleccionar **[!UICONTROL Visores]** en la vista de detalles del recurso. Puede aumentar o disminuir el número visto. Consulte [Aumento del número de ajustes preestablecidos de imagen que muestran](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) o [Aumento del número de ajustes preestablecidos de visor que muestran](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

## Filtrado de Recursos para Replicación {#filtering-assets-for-replication}

En implementaciones que no son de Dynamic Media, se replican *todos* recursos (tanto imágenes como vídeo) desde el entorno de creación de AEM al nodo de publicación de AEM. Este flujo de trabajo es necesario porque los servidores de publicación AEM también entregan los recursos.

Sin embargo, en las implementaciones de Dynamic Media, como los recursos se entregan a través de la nube, no es necesario replicar esos mismos recursos en AEM nodos de publicación. Este flujo de trabajo de &quot;publicación híbrida&quot; evita costes de almacenamiento adicionales y tiempos de procesamiento más largos para replicar recursos. Otros contenidos, como los visores de Dynamic Media, las páginas del sitio y el contenido estático, se siguen ofreciendo desde los nodos de publicación de AEM.

Además de replicar los recursos, también se replican los siguientes no activos:

* Configuración de Dynamic Media Envío: `/conf/global/settings/dam/dm/imageserver/jcr:content`
* Ajustes preestablecidos de imagen: `/conf/global/settings/dam/dm/presets/macros`
* Ajustes preestablecidos de visor: `/conf/global/settings/dam/dm/presets/viewer`

Los filtros proporcionan una manera de *excluir* recursos de la replicación en el nodo de publicación AEM.

### Uso de Filtros de Recursos Predeterminados para Replicación {#using-default-asset-filters-for-replication}

Si está utilizando Dynamic Media para (1) imágenes en producción **o** (2) imágenes y vídeo, puede utilizar los filtros predeterminados que proporcionamos tal cual. Los siguientes filtros están activos de forma predeterminada:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Filtro</strong></td>
   <td><strong>Tipo MIME</strong></td>
   <td><strong>Representaciones</strong></td>
  </tr>
  <tr>
   <td>Dynamic Media Image Envío</td>
   <td><p>filter-images</p> <p>filter-sets</p> <p> </p> </td>
   <td><p>Inicios con <strong>imagen/</strong></p> <p>Contiene <strong>application/</strong> y termina con <strong>set</strong>.</p> </td>
   <td>Las "imágenes de filtro" integradas (se aplican a recursos de imágenes únicas, incluidas imágenes interactivas) y "conjuntos de filtros" (se aplican a conjuntos de giros, conjuntos de imágenes, conjuntos de medios mixtos y conjuntos de carrusel):
    <ul>
     <li>Incluya imágenes PTIFF y metadatos para la replicación (cualquier representación que empiece por <strong>cqdam</strong>).</li>
     <li>Excluya de la replicación la imagen original y las representaciones de imágenes estáticas.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media Video Envío</td>
   <td>filter-video</td>
   <td>Inicios con <strong>video/</strong></td>
   <td>El "video-filtro" incorporado:
    <ul>
     <li>Incluya representaciones de vídeo proxy, miniaturas de vídeo/imagen de póster, metadatos (tanto en las representaciones de vídeo principales como en las representaciones de vídeo) para la replicación (cualquier representación que empiece por <strong>cqdam</strong>).</li>
     <li>Excluya de la replicación el vídeo original y las representaciones de miniaturas estáticas.<br /> <br /> <strong>Nota:</strong> Las representaciones de vídeo proxy no contienen binarios, sino que solo son propiedades de nodo. Por lo tanto, no hay impacto en el tamaño del repositorio del editor.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Integración con Dynamic Media Classic (Scene7)</td>
   <td><p>filter-images</p> <p>filter-sets</p> <p>filter-video</p> </td>
   <td><p>Inicios con <strong>imagen/</strong></p> <p>Contiene <strong>application/</strong> y termina con <strong>set</strong>.</p> <p>Inicios con <strong>video/</strong></p> </td>
   <td><p>Configure el URI de transporte para que señale al servidor de publicación de AEM en lugar de la URL del servicio de replicación de Dynamic Media Cloud de Adobe. Al configurar este filtro, Dynamic Media Classic podrá entregar recursos en lugar de la instancia de publicación AEM.</p> <p>Las "imágenes de filtro" integradas, "conjuntos de filtros" y "video-filtro" incorporadas:</p>
    <ul>
     <li>Incluya imágenes PTIFF, representaciones de vídeo proxy y metadatos para la replicación. Sin embargo, como no existen en el JCR para los que ejecutan AEM (integración con Dynamic Media Classic), no hace nada de forma efectiva.</li>
     <li>Excluya de la replicación la imagen original, las representaciones de imágenes estáticas, el vídeo original y las representaciones de miniaturas estáticas. En su lugar, Dynamic Media Classic proporcionará recursos de imagen y vídeo.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
Los filtros se aplican a tipos de MIME y no pueden ser específicos de la ruta.

### Configuración de Filtros de recursos para implementaciones de solo vídeo {#setting-up-asset-filters-for-video-only-deployments}

Si utiliza Dynamic Media solo para vídeo, siga estos pasos para configurar filtros de recursos para la replicación:

1. En AEM, toque el logotipo de AEM para acceder a la consola de navegación global y toque **[!UICONTROL Herramientas > Implementación > Replicación > Agentes en el autor.]**
1. En la página Agentes del autor, toque **[!UICONTROL Agente predeterminado (publicar).]**
1. Toque **[!UICONTROL Editar.]**
1. En el cuadro de diálogo **[!UICONTROL Configuración del agente]**, en la ficha **[!UICONTROL Configuración]**, marque **[!UICONTROL Habilitado]** para activar el agente.
1. Toque **[!UICONTROL Aceptar.]**
1. En AEM, pulse **[!UICONTROL Herramientas > General > CRXDE Lite.]**
1. En el árbol de carpetas de la izquierda, vaya a `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`
1. Localice **[!UICONTROL filter-video]**, haga clic con el botón derecho y seleccione **[!UICONTROL Copiar.]**
1. En el árbol de carpetas de la izquierda, vaya a `/etc/replication/agents.author/publish`
1. Localice **[!UICONTROL jcr:content]**, haga clic con el botón derecho en él y seleccione **[!UICONTROL Pegar.]**

Esto configura la instancia de publicación de AEM para ofrecer la imagen del póster de vídeo, así como los metadatos de vídeo necesarios para la reproducción, mientras que el propio vídeo lo entrega el servicio en la nube de Dynamic Media. El filtro también excluirá de la replicación el vídeo original y las representaciones de miniaturas estáticas, que no son necesarias en la instancia de publicación.

### Configuración de Filtros de recursos para imágenes en implementaciones que no son de producción {#setting-up-asset-filters-for-imaging-in-non-production-deployments}

Si utiliza Dynamic Media para la creación de imágenes en implementaciones que no son de producción, siga estos pasos para configurar filtros de recursos para la replicación:

1. En AEM, toque el logotipo de AEM para acceder a la consola de navegación global y toque **[!UICONTROL Herramientas > Implementación > Replicación > Agentes en el autor.]**
1. En la página Agentes del autor, toque **[!UICONTROL Agente predeterminado (publicar).]**
1. Toque **[!UICONTROL Editar.]**
1. En el cuadro de diálogo **[!UICONTROL Configuración del agente]**, en la ficha **[!UICONTROL Configuración]**, marque **[!UICONTROL Habilitado]** para activar el agente.
1. Toque **[!UICONTROL Aceptar.]**
1. En AEM, pulse **[!UICONTROL Herramientas > General > CRXDE Lite.]**
1. En el árbol de carpetas de la izquierda, vaya a `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`

   ![image-2018-01-16-10-22-40-410](assets/image-2018-01-16-10-22-40-410.png)

1. Localice **[!UICONTROL filter-images]**, haga clic con el botón derecho y seleccione **[!UICONTROL Copiar.]**
1. En el árbol de carpetas de la izquierda, vaya a `/etc/replication/agents.author/publish`
1. Localice **[!UICONTROL jcr:content]**, haga clic con el botón derecho en él y seleccione **[!UICONTROL Crear > Crear nodo.]** Escriba el nombre  `damRenditionFilters` del tipo  `nt:unstructured`.
1. Localice `damRenditionFilters`, haga clic con el botón derecho y seleccione **[!UICONTROL Pegar.]**

Esto configura la instancia de publicación de AEM para entregar las imágenes a su entorno que no sea de producción. El filtro también excluirá de la replicación la imagen original y las representaciones estáticas, que no son necesarias en la instancia de publicación.

>[!NOTE]
Si hay muchos filtros diferentes en un autor, cada agente necesita un usuario diferente asignado a él. El código de granito aplica un modelo de filtro por usuario. Tener siempre un usuario diferente para cada filtro configurado.
Si utiliza más de un filtro en un servidor (por ejemplo, un filtro para que la replicación se publique y otro para s7envío), debe asegurarse de que estos dos filtros tengan un **userId** diferente asignado en el nodo **jcr:content**. Consulte la siguiente imagen:

![image-2018-01-16-10-26-28-465](assets/image-2018-01-16-10-26-28-465.png)

### Personalización de Filtros de Recursos para Replicación {#customizing-asset-filters-for-replication}

Para personalizar de forma opcional los filtros de recursos para la replicación:

1. En AEM, toque el logotipo de AEM para acceder a la consola de navegación global y toque **[!UICONTROL Herramientas > General > CRXDE Lite.]**
1. En el árbol de carpetas de la izquierda, vaya a `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters` para revisar los filtros.

   ![chlimage_1-511](assets/chlimage_1-511.png)

1. Para definir el tipo de MIME para el filtro, puede localizar el tipo de MIME de la siguiente manera:

   En el carril izquierdo, expanda `content > dam > <locate_your_asset> >  jcr:content > metadata` y, a continuación, en la tabla, localice **[!UICONTROL dc:format.]**

   El siguiente gráfico es un ejemplo de la ruta de un recurso al formato dc:format.

   ![chlimage_1-512](assets/chlimage_1-512.png)

   Observe que `dc:format` para el recurso `Fiji Red.jpg` es `image/jpeg`.

   Para que este filtro se aplique a todas las imágenes, independientemente de su formato, establezca el valor en `image/*` donde `*` es una expresión normal que se aplica a todas las imágenes de cualquier formato.

   Para que el filtro solo se aplique a imágenes del tipo JPEG, introduzca un valor de `image/jpeg`.

1. Defina qué representaciones desea incluir o excluir de la replicación.

   Los caracteres que se pueden usar para filtrar para la replicación son los siguientes:

<table>
 <tbody>
  <tr>
   <td><strong>Carácter que utilizar</strong></td>
   <td><strong>Filtros de recursos para replicación</strong></td>
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

Utilizando el ejemplo anterior, si sólo desea replicar el PTIFF (Pyramid TIFF), debe ingresar `+cqdam,*` que incluye todas las representaciones que inicio con `cqdam`. En el ejemplo, esa representación es `cqdam.pyramid.tiff`.

Si sólo desea replicar el original, debe ingresar `+original`.

## Configuración de la configuración de Dynamic Media Image Server {#configuring-dynamic-media-image-server-settings}

La configuración del servidor de imágenes de Dynamic Media implica la edición del paquete Adobe CQ Scene7 ImageServer y del paquete Adobe CQ Scene7 PlatformServer.

>[!NOTE]
Dynamic Media funciona de inmediato [después de habilitarlo](#enabling-dynamic-media). Sin embargo, si lo desea, puede ajustar la instalación configurando el servidor de imágenes de Dynamic Media para que cumpla determinadas especificaciones o requisitos.

**Requisito previo**:  ** Antes de configurar Dynamic Media Image Server, asegúrese de que la VM de Windows incluye una instalación de las bibliotecas de Microsoft Visual C++. Las bibliotecas son necesarias para ejecutar Dynamic Media Image Server. Puede [descargar el paquete redistribuible de Microsoft Visual C++ 2010 (x64) aquí](https://www.microsoft.com/en-us/download/details.aspx?id=14632).

Para configurar el servidor de imágenes de Dynamic Media:

1. En la esquina superior izquierda de AEM, toque **[!UICONTROL Adobe Experience Manager]** para acceder a la consola de navegación global y, a continuación, toque **[!UICONTROL Herramientas > Operaciones > Consola Web.]**
1. En la página de configuración de la consola web de Adobe Experience Manager, toque **[!UICONTROL OSGi > Configuration]** para lista de todos los paquetes que se están ejecutando en AEM.

   Los servidores Envío de Dynamic Media se encuentran bajo los siguientes nombres en la lista:

   * `Adobe CQ Scene7 ImageServer`
   * `Adobe CQ Scene7 PlatformServer`

1. En la lista de paquetes, a la derecha de Adobe CQ Scene7 ImageServer, toque el icono Editar.
1. En el cuadro de diálogo Adobe CQ Scene7 ImageServer, establezca los siguientes valores de configuración:

   >[!NOTE]
   En la mayoría de los casos, no es necesario cambiar los valores predeterminados. Sin embargo, si cambia los valores predeterminados, debe reiniciar el paquete para que los cambios se vean afectados.

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
   <td>Número de puerto que se usará para la comunicación con el proceso de ImageServer. De forma predeterminada, el puerto libre se detecta automáticamente.</td>
  </tr>
  <tr>
   <td>AllowRemoteAccess.name</td>
   <td><code><em>empty</em></code></td>
   <td><p>Permitir o no permitir el acceso remoto al proceso ImageServer. Si es false, el servidor de imágenes solo escucha en localhost.</p> <p>La configuración predeterminada del externalizador que apunta al host local debe especificar el dominio o la dirección IP reales de la instancia de VM específica. El motivo de esto es que el host local puede estar apuntando al sistema principal de la VM.</p> <p>Es posible que los dominios o las direcciones IP de la VM necesiten tener una entrada de archivo host para poder resolverse por sí mismos.</p> </td>
  </tr>
  <tr>
   <td>MaxRenderRgnPixels</td>
   <td>16 MPixels</td>
   <td>Tamaño máximo en megapíxeles que se procesa.</td>
  </tr>
  <tr>
   <td>MaxMessageSize</td>
   <td>16 MBytes</td>
   <td>Tamaño máximo del mensaje en megabytes que se entrega.</td>
  </tr>
  <tr>
   <td>RandomAccessUrlTimeout</td>
   <td>20</td>
   <td>Valor de tiempo de espera durante el tiempo en segundos que el ImageServer esperará a que el JCR responda a una solicitud de mosaico de rango.</td>
  </tr>
  <tr>
   <td>WorkerThread</td>
   <td>10</td>
   <td>Número de subprocesos de trabajo.</td>
  </tr>
 </tbody>
</table>

1. Toque **[!UICONTROL Guardar.]**
1. En la lista de paquetes, a la derecha de Adobe CQ Scene7 PlatformServer, toque el icono **[!UICONTROL Editar]**.
1. En el cuadro de diálogo Adobe CQ Scene7 PlatformServer, establezca las siguientes opciones de valor predeterminadas:

   >[!NOTE]
   Dynamic Media Image Server utiliza su propia caché de disco para almacenar en caché las respuestas. La caché HTTP AEM y el Dispacher no se pueden usar para almacenar en caché las respuestas del servidor de imágenes de Dynamic Media.

   | **Propiedad** | **Valor predeterminado** | **Descripción** |
   |---|---|---|
   | Caché habilitada | Activados | Indica si la caché de respuestas está habilitada o no. |
   | Raíz de caché | caché | Una o más rutas a las carpetas de la caché de respuesta. Las rutas relativas se resuelven con la carpeta interna del paquete de imágenes s7s. |
   | Tamaño máximo de caché | 200000000 | Tamaño máximo de la caché de respuesta en bytes. |
   | Entradas máximas de caché | 100 000 | Número máximo de entradas permitidas en la caché. |

### Configuración de manifiesto predeterminada {#default-manifest-settings}

El manifiesto predeterminado permite configurar los valores predeterminados que se utilizan para generar las respuestas de Dynamic Media Envío. Puede ajustar la calidad (calidad JPEG, resolución, modo de remuestreo), el almacenamiento en caché (caducidad) y evitar la representación de imágenes que son demasiado grandes (predeterminado, predeterminado, miniatura, máximo).

La ubicación de la configuración de manifiesto predeterminada se toma del valor predeterminado **[!UICONTROL raíz del catálogo]** del paquete **[!UICONTROL Adobe CQ Scene7 PlatformServer]**. De forma predeterminada, este valor se encuentra en la siguiente ruta dentro de **[!UICONTROL Herramientas > General > CRXDE Lite]**:

`/conf/global/settings/dam/dm/imageserver/`

![configimageservercrxdelite](assets/configimageservercrxdelite.png)

Puede cambiar los valores de las propiedades, como se describe en la tabla siguiente, introduciendo nuevos valores.

Cuando haya terminado de realizar cambios en el manifiesto predeterminado, en la esquina superior izquierda de la página, toque **[!UICONTROL Guardar todo.]**

Asegúrese de tocar la ficha **[!UICONTROL Control de acceso]** (a la derecha de la ficha Propiedades) y, a continuación, establezca los privilegios de control de acceso en `jcr:read` para todos los usuarios y los usuarios de replicación dinámica de medios.

![configimageservercrxdeliteaccescontroltab](assets/configimageservercrxdeliteaccesscontroltab.png)

Tabla de la configuración de manifiesto y sus valores predeterminados:

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
   <td><p>Tamaño de vista predeterminado. El servidor restringe las imágenes de respuesta para que no superen este ancho y alto, si la solicitud no especifica el tamaño de vista usando explícitamente wid=, hei= o scl=.</p> <p>Se especifica como dos números enteros, 0 o más, separados por una coma. Anchura y altura en píxeles. Puede que uno o ambos valores estén establecidos en 0 para mantenerlos sin restricciones. No se aplica a solicitudes anidadas o incrustadas.</p> <p>Consulte también <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html#image-serving-api">DefaultPix</a> en la API de servicio de imágenes.</p> <p>Sin embargo, normalmente se utiliza un ajuste preestablecido de visor o de imagen para distribuir el recurso. El valor predeterminado solo se aplica a un recurso que no utiliza un ajuste preestablecido de visor o de imagen.</p> </td>
  </tr>
  <tr>
   <td>defaultthumbpix</td>
   <td>100.100</td>
   <td><p>Tamaño de miniatura predeterminado. Se utiliza en lugar de attribute::DefaultPix para solicitudes de miniatura (req=tmb).</p> <p>El servidor restringe las imágenes de respuesta para que no sean mayores que este ancho y alto, si una solicitud de miniatura (req=tmb) no especifica el tamaño explícitamente, no especifica el tamaño de vista usando explícitamente wid=, hei= o scl=.</p> <p>Se especifica como dos números enteros, 0 o más, separados por una coma. Anchura y altura en píxeles. Puede que uno o ambos valores estén establecidos en 0 para mantenerlos sin restricciones. </p> <p>No se aplica a solicitudes anidadas o incrustadas.</p> <p>Consulte también <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html#image-serving-api">DefaultThumbPix</a> en la API de servicio de imágenes. </p> </td>
  </tr>
  <tr>
   <td>caducidad</td>
   <td>36000000</td>
   <td><p>Tiempo de espera predeterminado de la caché del cliente. Proporciona un intervalo de caducidad predeterminado en caso de que un registro de catálogo en particular no contenga un valor de catálogo válido::Expiration.</p> <p>Número real, 0 o bueno. Número de milisegundos hasta la caducidad desde que se generaron los datos de respuesta. Establezca el valor 0 para que la imagen de respuesta caduque siempre inmediatamente, lo que deshabilita el almacenamiento en caché del cliente. De forma predeterminada, este valor se establece en 10 horas, lo que significa que si se publica una imagen nueva, la imagen antigua tarda 10 horas en dejarse en caché para el usuario. Póngase en contacto con el Servicio de atención al cliente si necesita borrar la caché antes.</p> <p>Consulte también <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html">Caducidad</a> en la API de servicio de imágenes.</p> </td>
  </tr>
  <tr>
   <td>jpegquality</td>
   <td>80</td>
   <td><p>Atributos de codificación JPEG predeterminados. Especifica los atributos predeterminados para las imágenes de respuesta JPEG.</p> <p>Número entero y indicador, separados por coma. El primer valor está en el rango 1.100 y define la calidad. El segundo valor puede ser 0 para el comportamiento normal, o 1 para desactivar el descenso de resolución de cromaticidad RGB que suelen utilizar los codificadores JPEG.</p> <p>Consulte también <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html#image-serving-api">JpegQuality</a> en la API de servicio de imágenes.</p> </td>
  </tr>
  <tr>
   <td>maxpix</td>
   <td>2000.2000</td>
   <td><p>Límite de tamaño de la imagen de respuesta. Ancho y altura máximos de la imagen de respuesta que se devuelve al cliente.</p> <p>El servidor devuelve un error si una solicitud genera una imagen de respuesta cuyo ancho o alto es mayor que el atributo::MaxPix.</p> <p>Consulte también <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html?lang=en#image-serving-api">MaxPix</a> en la API de servicio de imágenes.</p> </td>
  </tr>
  <tr>
   <td>resmode</td>
   <td>SHARP2</td>
   <td><p>Modo de remuestreo predeterminado. Especifica los atributos predeterminados de remuestreo e interpolación que se utilizarán para escalar datos de imagen.</p> <p>Se utiliza cuando resMode= no se especifica en una solicitud.</p> <p>Los valores permitidos incluyen BILIN, BICUB o SHARP2.</p> <p>Enum. Se establece en 2 para bilin, 3 para bicub o 4 para modo de interpolación sharp2. Utilice sharp2 para obtener los mejores resultados.</p> <p>Consulte también <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html#image-serving-api">ResMode</a> en la API de servicio de imágenes.</p> </td>
  </tr>
  <tr>
   <td>resolución</td>
   <td>72</td>
   <td><p>Resolución de objeto predeterminada. Proporciona una resolución de objeto predeterminada en caso de que un registro de catálogo en particular no contenga un valor de catálogo válido::Resolution.</p> <p>Número real, mayor que 0. Normalmente se expresa como píxeles por pulgada, pero también puede estar en otras unidades, como píxeles por metro.</p> <p>Consulte también <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-resolution.html#image-serving-api">Resolución</a> en la API de servicio de imágenes.</p> </td>
  </tr>
  <tr>
   <td>thumbnailtime</td>
   <td>1,11%,21%,31%,41%,51%,61%,71%,81%,91%</td>
   <td>Estos valores representan una instantánea del tiempo de reproducción del vídeo y se pasan a <a href="https://encoding.com/">encoding.com</a>. Consulte <a href="/help/assets/video.md#about-video-thumbnails-in-dynamic-media-hybrid-mode">Acerca de las miniaturas de vídeo</a> para obtener más información.</td>
  </tr>
 </tbody>
</table>

## Configuración de la administración de color de Dynamic Media {#configuring-dynamic-media-color-management}

La administración dinámica de color de los medios le permite colorear los recursos correctos para la vista previa.

Con la corrección de color, los recursos ingestados conservan su espacio de color (RGB, CMYK, Gris) y su perfil de color incrustado en la representación TIFF de la pirámide generada. Cuando se solicita una representación dinámica, el color de la imagen se corrige en el espacio de color del destinatario. Puede configurar el perfil de color de salida en la configuración de publicación de Dynamic Media en el JCR.

La administración de color de Adobe utiliza perfiles ICC, un formato definido por International Color Consortium (ICC).

Puede configurar la administración dinámica de color de los medios y configurar los ajustes preestablecidos de imagen mediante la salida CMYK, RGB o gris. Consulte [Configuración de ajustes preestablecidos de imagen](/help/assets/managing-image-presets.md).

Los casos de uso avanzados podrían utilizar un modificador `icc=` de configuración manual para seleccionar explícitamente un perfil de color de salida:

* `icc` -  [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html)

* `iccEmbed` -  [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html)

>[!NOTE]
El conjunto estándar de perfiles de color de Adobe sólo está disponible si tiene [Feature Pack 12445 de Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-12445) instalado. Todos los paquetes de funciones y Service Packs están disponibles en [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Feature Pack 12445 proporciona los perfiles de color del Adobe.

### Instalación de Feature Pack 12445 {#installing-feature-pack}

Debe instalar el paquete de funciones 12445 para utilizar las funciones de administración de color de Dynamic Media.

**Para instalar el paquete de funciones 12445**

1. Vaya a [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) y descargue `cq-6.3.0-featurepack-12445`.

   Consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md) para obtener más información sobre cómo utilizar paquetes en [!DNL Adobe Experience Manager].

1. Instale el paquete de funciones.

### Configuración de los perfiles de color predeterminados {#configuring-the-default-color-profiles}

Después de instalar el paquete de funciones, debe configurar los perfiles de color predeterminados adecuados para habilitar la corrección de color al solicitar datos de imagen RGB o CMYK.

**Para configurar los perfiles de color predeterminados**

1. En **[!UICONTROL Herramientas > General > CRXDE Lite]**, navegue a `/conf/global/settings/dam/dm/imageserver/jcr:content`, que contiene los Perfiles predeterminados de Adobe Color.

   ![chlimage_1-514](assets/chlimage_1-514.png)

1. Para añadir una propiedad de corrección de color, desplácese hasta la parte inferior de la ficha **[!UICONTROL Propiedades]** e introduzca manualmente el nombre, el tipo y el valor de la propiedad, que se describen en las siguientes tablas. Después de introducir los valores, toque **[!UICONTROL Añadir]** y luego **[!UICONTROL Guardar todo]** para guardar los valores.

   Las propiedades de corrección de color se describen en la tabla **Propiedades de corrección de color**. Los valores que puede asignar a las propiedades de corrección de color se encuentran en la tabla **Perfil de color**.

   Por ejemplo, en **[!UICONTROL Nombre]**, agregue `iccprofilecmyk`, seleccione **[!UICONTROL Tipo]** `String` y agregue `WebCoated` como **[!UICONTROL Valor.]** A continuación, toque  **** Agregar y luego  **[!UICONTROL Guardar]** Allpara guardar los valores.

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
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcrgb.html">iccprofiles rcrgb</a></td>
   <td>Cadena</td>
   <td>&lt;empty&gt;</td>
   <td>Nombre del perfil de color RGB predeterminado utilizado para imágenes RGB que no tienen un perfil de color incrustado</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrccmyk.html">iccprofiles rccmyk</a></td>
   <td>Cadena</td>
   <td>&lt;empty&gt;</td>
   <td>Nombre del perfil de color CMYK predeterminado utilizado para imágenes CMYK que no tienen un perfil de color incrustado.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcgray.html">iccprofiles rcgris</a></td>
   <td>Cadena</td>
   <td>&lt;empty&gt;</td>
   <td>Nombre del perfil de color gris predeterminado utilizado para imágenes CMYK que no tienen un perfil de color incrustado.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccblackpointcompensation.html">iccblackpointcompensación</a></td>
   <td>Booleano</td>
   <td>Verdadero</td>
   <td>Especifica si se debe realizar una compensación de punto negro durante la corrección de color. Adobe recomienda que esto esté activado.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccdither.html">iccdither</a></td>
   <td>Booleano</td>
   <td>False</td>
   <td>Especifica si se debe realizar el tramado durante la corrección de color.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html">iccrenderintent</a></td>
   <td>Cadena</td>
   <td>relativo</td>
   <td><p>Especifica la interpretación. Los valores aceptables son: <strong>perceptual, relativo, saturación, absoluto. </strong><i></i>Adobe recomienda  <strong>Relativo  </strong><i></i>como valor predeterminado.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
Los nombres de propiedades distinguen entre mayúsculas y minúsculas y deben escribirse en minúsculas.

**Tabla de Perfil de color**

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
   <td>Coated FOGRA27 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedFogra39</td>
   <td>CMYK</td>
   <td>Coated FOGRA39 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedGraCol</td>
   <td>CMYK</td>
   <td>Coated GRACoL 2006 (ISO 12647-2:2004)</td>
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
   <td>EuroscaleUncover</td>
   <td>CMYK</td>
   <td>Euroscale sin revestimiento v2</td>
  </tr>
  <tr>
   <td>JapanColorCoated</td>
   <td>CMYK</td>
   <td>Recubierto en color japonés 2001</td>
  </tr>
  <tr>
   <td>JapanColorNewspaper</td>
   <td>CMYK</td>
   <td>Japan Color 2002 Newspaper</td>
  </tr>
  <tr>
   <td>JapanColorUncover</td>
   <td>CMYK</td>
   <td>Japan Color 2001 sin recubrir</td>
  </tr>
  <tr>
   <td>JapanColorWebCoated</td>
   <td>CMYK</td>
   <td>Japan Color 2003 Web Coated</td>
  </tr>
  <tr>
   <td>JapanWebCoated</td>
   <td>CMYK</td>
   <td>Japan Web Coated (Ad)</td>
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
   <td>SheetfeedCoated</td>
   <td>CMYK</td>
   <td>U.S. Sheetfeed Coated v2</td>
  </tr>
  <tr>
   <td>SheetfeedUncover</td>
   <td>CMYK</td>
   <td>U.S. Sheetfeed Uncover v2</td>
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
   <td>No recubiertoFogra29</td>
   <td>CMYK</td>
   <td>FOGRA29 sin estucar (ISO 12647-2:2004)</td>
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
   <td>Papel Web Coated SWOP 2006 de grado 3</td>
  </tr>
  <tr>
   <td>WebCoatedGrade5</td>
   <td>CMYK</td>
   <td>Papel Web Coated SWOP 2006 de grado 5</td>
  </tr>
  <tr>
   <td>WebUnsquare</td>
   <td>CMYK</td>
   <td>U.S. Web sin estucar v2</td>
  </tr>
  <tr>
   <td>WideGamutRGB</td>
   <td>RGB</td>
   <td>RGB de gama amplia</td>
  </tr>
 </tbody>
</table>

1. Toque **[!UICONTROL Guardar todo.]**

Por ejemplo, podría establecer **[!UICONTROL iccprofilergb]** en `sRGB` y **[!UICONTROL iccprofilecmyk]** en **[!UICONTROL WebCoated.]**

Al hacerlo, se haría lo siguiente:

* Permite la corrección de color para imágenes RGB y CMYK.
* Las imágenes RGB que no tengan un perfil de color se considerarán como del espacio de color *sRGB*.
* Las imágenes CMYK que no tengan un perfil de color se supondrán que están en *espacio de color WebCoated*.
* Las representaciones dinámicas que devuelven salida RGB la devolverán en el *sRGB *espacio de color.
* Las representaciones dinámicas que devuelven una salida CMYK la devolverán en el espacio de color *WebCoated*.

## Distribución de recursos {#delivering-assets}

Después de completar todas las tareas anteriores, los recursos de Dynamic Media activados se proporcionan desde el servicio de imágenes o vídeo. En AEM, esta capacidad se muestra en **[!UICONTROL Copiar URL de imagen]**, **[!UICONTROL Copiar URL del visor]**, **[!UICONTROL Incrustar código del visor]** y en WCM.

Consulte [Entrega de Dynamic Media Assets](/help/assets/delivering-dynamic-media-assets.md).

<table>
 <tbody>
  <tr>
   <td><strong>Cuando...</strong></td>
   <td><strong>Resultado</strong></td>
  </tr>
  <tr>
   <td>Copiar una dirección URL de imagen</td>
   <td><p>El cuadro de diálogo Copiar URL muestra una URL similar a la siguiente (la URL se muestra únicamente con fines de demostración):</p> <p><code>https://IMAGESERVICEPUBLISHNODE/is/image/content/dam/path/to/Image.jpg?$preset$</code></p> <p>Donde <code>IMAGESERVICEPUBLISHNODE</code> hace referencia a la dirección URL del servicio de imágenes.</p> <p>Consulte también <a href="/help/assets/delivering-dynamic-media-assets.md">Entrega de Dynamic Media Assets</a>.</p> </td>
  </tr>
  <tr>
   <td>Copiar una URL de visor</td>
   <td><p>El cuadro de diálogo Copiar URL muestra una URL similar a la siguiente (la URL se muestra únicamente con fines de demostración):</p> <p><code>https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/BasicZoomViewer.html?asset=/content/dam/path/to/Image.jpg&amp;config=/conf/global/settings/dam/dm/presets/viewer/Zoom_dark&amp;serverUrl=https://IMAGESERVICEPUBLISHNODE/is/image/&amp;contentRoot=%2F</code></p> <p>Donde <code>PUBLISHNODE</code> hace referencia al nodo de publicación AEM normal y <code>IMAGESERVICEPUBLISHNODE</code> hace referencia a la dirección URL del servicio de imágenes.</p> <p>Consulte también <a href="/help/assets/delivering-dynamic-media-assets.md">Entrega de Dynamic Media Assets</a>.</p> </td>
  </tr>
  <tr>
   <td>Copia del código incrustado de un visor</td>
   <td><p>El cuadro de diálogo Copiar código incrustado muestra un fragmento de código similar al siguiente (el ejemplo de código se muestra únicamente con fines de demostración):</p> <p><code class="code">&lt;style type="text/css"&gt;
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
       &lt;/script&gt;</code></p> <p>Donde <code>PUBLISHNODE</code> hace referencia al nodo de publicación AEM normal y <code>IMAGESERVICEPUBLISHNODE</code> hace referencia a la dirección URL del servicio de imágenes.</p> <p>Consulte también <a href="/help/assets/delivering-dynamic-media-assets.md">Entrega de Dynamic Media Assets</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Componentes de medios interactivos de WCM Dynamic Media {#wcm-dynamic-media-and-interactive-media-components}

Las páginas WCM que hacen referencia a componentes de Dynamic Media y medios interactivos hacen referencia al servicio de envío.
