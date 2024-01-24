---
title: 'Configuración de Dynamic Media: modo híbrido'
description: 'Obtenga información sobre cómo configurar Dynamic Media: modo híbrido.'
mini-toc-levels: 3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/config-dynamic
role: User, Admin
exl-id: 5719d32c-4f19-47c1-bea9-8fd0bc8439ed
feature: Configuration,Hybrid Mode
source-git-commit: 3fa8680480e0da1c58c99e8ce127ce228ab87803
workflow-type: tm+mt
source-wordcount: '7733'
ht-degree: 1%

---

# Configuración de Dynamic Media: modo híbrido {#configuring-dynamic-media-hybrid-mode}

>[!IMPORTANT]
>
>Fin de la compatibilidad con Secure Socket Layer 2.0 y 3.0 y Transport Layer Security 1.0 y 1.1.
>A partir del 30 de abril de 2024, Adobe Dynamic Media dejará de ofrecer asistencia para lo siguiente:
>
>* SSL (Secure Socket Layer) 2.0
>* SSL 3.0
>* TLS (Transport Layer Security) 1.0 y 1.1
>* Los siguientes cifrados débiles en TLS 1.2:
> `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
> `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
> `TLS_RSA_WITH_AES_256_GCM_SHA384`
> `TLS_RSA_WITH_AES_256_CBC_SHA256`
> `TLS_RSA_WITH_AES_256_CBC_SHA`
> `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
> `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
> `TLS_RSA_WITH_AES_128_GCM_SHA256`
> `TLS_RSA_WITH_AES_128_CBC_SHA256`
> `TLS_RSA_WITH_AES_128_CBC_SHA`
> `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
> `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
> `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
> `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

<!-- FOR ABOVE - CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022) -->


Dynamic Media-Hybrid debe estar habilitado y configurado para su uso. Según el caso de uso, Dynamic Media tiene varias [configuraciones admitidas](#supported-dynamic-media-configurations).

>[!NOTE]
>
>Si desea configurar y ejecutar Dynamic Media en el modo de ejecución de Scene7, consulte [Configuración de Dynamic Media: modo Scene7](/help/assets/config-dms7.md).
>
>Si tiene intención de configurar y ejecutar Dynamic Media en modo de ejecución híbrido, siga las instrucciones de esta página.

Más información sobre cómo trabajar con [video](/help/assets/video.md) en Dynamic Media.

>[!NOTE]
>
>Si utiliza la configuración de Adobe Experience Manager para diferentes entornos, como uno para desarrollo, ensayo y producción en directo, configure los Cloud Service de Dynamic Media para cada entorno.

>[!NOTE]
>
>Si tiene problemas con la configuración de Dynamic Media, consulte los archivos de registro específicos de Dynamic Media. Estos archivos se instalan automáticamente al habilitar Dynamic Media:
>
>* `s7access.log`
>* `ImageServing.log`
>
>Están documentados en [Monitorización y mantenimiento de la instancia de Experience Manager](/help/sites-deploying/monitoring-and-maintaining.md).

La publicación y el envío híbridos son una función central de Dynamic Media, además de Adobe Experience Manager. La publicación híbrida permite enviar recursos de Dynamic Media, como imágenes, conjuntos y vídeos, desde la nube en lugar de desde los nodos de publicación del Experience Manager.

Otros contenidos, como los visualizadores de Dynamic Media, las páginas del sitio y el contenido estático, se siguen mostrando desde los nodos de publicación del Experience Manager.

Si es cliente de Dynamic Media, debe utilizar la entrega híbrida como mecanismo de entrega para todo el contenido de Dynamic Media.

## Arquitectura de publicación híbrida para vídeos {#hybrid-publishing-architecture-for-videos}

![chlimage_1-506](assets/chlimage_1-428.png)

## Arquitectura de publicación híbrida para imágenes {#hybrid-publishing-architecture-for-images}

![chlimage_1-507](assets/chlimage_1-507.png)

## Configuraciones de Dynamic Media compatibles {#supported-dynamic-media-configurations}

Las tareas de configuración que siguen hacen referencia a los siguientes términos:

| **Término** | **Dynamic Media habilitado** | **Descripción** |
|---|---|---|
| Nodo Experience Manager Author | Marca de verificación blanca en un círculo verde | Nodo de autor que se implementa en las instalaciones o a través de Managed Services. |
| Nodo Publicación del Experience Manager | &quot;X&quot; blanca en un cuadrado rojo. | Nodo de publicación que se implementa en las instalaciones o a través de Managed Services. |
| Nodo de publicación del servicio de imágenes | Marca de verificación blanca en un círculo verde. | Nodo de publicación que se ejecuta en centros de datos administrados por Adobe. Hace referencia a la URL del servicio de imágenes. |

Puede elegir implementar Dynamic Media solo para imágenes, solo para vídeo o tanto para imágenes como para vídeo. Para determinar los pasos para configurar Dynamic Media para su escenario específico, consulte la siguiente tabla.

<table>
 <tbody>
  <tr>
   <td><strong>Escenario</strong></td>
   <td ><strong>Cómo funciona</strong></td>
   <td><strong>Pasos de configuración</strong></td>
  </tr>
  <tr>
   <td>Distribuya SOLO imágenes en producción</td>
   <td>Las imágenes se envían a través de servidores en los centros de datos de todo el mundo de Adobe y, a continuación, una CDN las almacena en caché para obtener un rendimiento escalable y un alcance global.</td>
   <td>
    <ol>
     <li>En el Experience Manager <strong>autor</strong> nodo, <a href="#enabling-dynamic-media">habilitar Dynamic Media</a>.</li>
     <li>Configuración de imágenes en <a href="#configuring-dynamic-media-cloud-services">Cloud Service de Dynamic Media</a>.</li>
     <li><a href="#configuring-image-replication">Configurar la replicación de imágenes</a>.</li>
     <li><a href="#replicating-catalog-settings">Replicar configuración del catálogo</a>.</li>
     <li><a href="#replicating-viewer-presets">Replicar ajustes preestablecidos de visor</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">Usar filtros de recursos predeterminados para la replicación</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Configuración del servidor de imágenes de Dynamic Media</a>.</li>
     <li><a href="#delivering-assets">Entrega de recursos</a>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Distribuya SOLO imágenes en preproducción (desarrollo, QE, ensayo, etc.)</td>
   <td>Las imágenes se envían mediante el nodo de publicación Experience Manager. En esta situación, como el tráfico es mínimo, no es necesario enviar imágenes al centro de datos de Adobe. Y permite una previsualización segura del contenido antes del lanzamiento de producción.</td>
   <td>
    <ol>
     <li>En el Experience Manager <strong>autor</strong> nodo, <a href="#enabling-dynamic-media">habilitar Dynamic Media</a>.</li>
     <li>En el Experience Manager <strong>publicar</strong> nodo, <a href="#enabling-dynamic-media">habilitar Dynamic Media</a>.</li>
     <li><a href="#replicating-viewer-presets">Replicar ajustes preestablecidos de visor</a>.</li>
     <li>Configuración de <a href="#setting-up-asset-filters-for-imaging-in-non-production-deployments">filtro de recursos para imágenes que no son de producción</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Configure Dynamic Media Image Server.</a></li>
     <li><a href="#delivering-assets">Entrega de recursos.</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ofrezca SOLO vídeo en cualquier entorno (producción, desarrollo, QE, fase, etc.)</td>
   <td>Una CDN entrega y almacena en caché los vídeos para un rendimiento escalable y un alcance global. La imagen de póster de vídeo (miniatura del vídeo que se muestra antes de que se inicie la reproducción) la entrega la instancia de publicación del Experience Manager.</td>
   <td>
    <ol>
     <li>En el Experience Manager <strong>autor</strong> nodo, <a href="#enabling-dynamic-media">habilitar Dynamic Media</a>.</li>
     <li>En el Experience Manager <strong>publicar</strong> nodo, <a href="#enabling-dynamic-media">habilitar Dynamic Media</a> (la instancia de publicación sirve para la imagen del póster de vídeo y proporciona metadatos para la reproducción de vídeo).</li>
     <li>Configuración de vídeo en <a href="#configuring-dynamic-media-cloud-services">Cloud Service de Dynamic Media.</a></li>
     <li><a href="#replicating-viewer-presets">Replicar ajustes preestablecidos de visor</a>.</li>
     <li>Configuración de <a href="#setting-up-asset-filters-for-video-only-deployments">filtro de recursos solo para vídeo</a>.</li>
     <li><a href="#delivering-assets">Entrega de recursos.</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Distribución de imágenes y vídeo en producción</td>
   <td><p>Una CDN entrega y almacena en caché los vídeos para un rendimiento escalable y un alcance global. Las imágenes y los pósters de vídeo se envían a través de servidores de los centros de datos de todo el mundo de Adobe y, a continuación, una red de distribución de contenido (CDN) las almacena en caché para obtener un rendimiento escalable y un alcance global.</p> <p>Consulte las secciones anteriores para configurar imágenes o vídeos en preproducción. </p> </td>
   <td>
    <ol>
     <li>En el Experience Manager <strong>autor</strong> nodo, <a href="#enabling-dynamic-media">habilitar Dynamic Media</a>.</li>
     <li>Configuración de vídeo en <a href="#configuring-dynamic-media-cloud-services">Cloud Service de Dynamic Media.</a></li>
     <li>Configuración de imágenes en <a href="#configuring-dynamic-media-cloud-services">Cloud Service de Dynamic Media.</a></li>
     <li><a href="#configuring-image-replication">Configurar la replicación de imágenes</a>.</li>
     <li><a href="#replicating-catalog-settings">Replicar configuración del catálogo</a>.</li>
     <li><a href="#replicating-viewer-presets">Replicar ajustes preestablecidos de visor</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">Utilice los filtros de recursos predeterminados para la replicación.</a></li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Configure Dynamic Media Image Server.</a></li>
     <li><a href="#delivering-assets">Entrega de recursos.</a></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Habilitar Dynamic Media {#enabling-dynamic-media}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) está desactivado de forma predeterminada. Para aprovechar las funciones de Dynamic Media, debe habilitar Dynamic Media mediante el `dynamicmedia` modo de ejecución como lo haría, por ejemplo, `publish` modo de ejecución. Antes de habilitar, asegúrese de revisar la [requisitos técnicos](/help/sites-deploying/technical-requirements.md#requirements-for-aem-dynamic-media-add-on).

>[!NOTE]
>
>Al habilitar Dynamic Media mediante el modo de ejecución, se sustituye la funcionalidad de Experience Manager 6.1 y Experience Manager 6.0, donde habilitaba Dynamic Media configurando `dynamicMediaEnabled` marcar como **[!UICONTROL true]**. Este indicador no tiene funcionalidad en Experience Manager 6.2 y versiones posteriores. Además, no es necesario reiniciar el inicio rápido para habilitar Dynamic Media.

Al habilitar Dynamic Media, las funciones de Dynamic Media están disponibles en la interfaz de usuario y cada recurso de imagen cargado recibe un *cqdam.pyramid.tiff* representación que se utiliza para el envío rápido de representaciones de imágenes dinámicas. Estos PTIFF tienen ventajas significativas como las siguientes:

* La capacidad de administrar una sola imagen de origen principal y generar representaciones infinitas sobre la marcha sin ningún almacenamiento adicional.
* La capacidad de utilizar visualizaciones interactivas como zoom, desplazamiento y giro.

Si desea utilizar Dynamic Media Classic en Experience Manager, no habilite Dynamic Media a menos que esté utilizando un [escenario específico](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media). Dynamic Media está deshabilitado a menos que habilite Dynamic Media mediante el modo de ejecución.

Para habilitar Dynamic Media, debe habilitar el modo de ejecución de Dynamic Media desde la línea de comandos o desde el nombre del archivo de inicio rápido.

**Para habilitar Dynamic Media:**

1. En la línea de comandos, al iniciar el inicio rápido, haga lo siguiente:

   * Añadir `-r dynamicmedia` al final de la línea de comandos al iniciar el archivo jar.

   ```shellsession {.line-numbers}
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -r dynamicmedia
   ```

   Si publica en s7delivery, también debe incluir los siguientes argumentos trustStore:

   ```shellsession {.line-numbers}
   -Djavax.net.ssl.trustStore=<absoluteFilePath>/customerTrustStoreFileName>
   
    -Djavax.net.ssl.trustStorePassword=<passwordForTrustStoreFile>
   ```

1. Solicitud `https://localhost:4502/is/image` y asegúrese de que Image Server se esté ejecutando.

   >[!NOTE]
   >
   >Para solucionar problemas con Dynamic Media, consulte los siguientes registros en la `crx-quickstart/logs/` directorio:
   >
   >* ImageServer-&lt;portid>-&lt;yyyy>&lt;mm>&lt;dd>.log: el registro de ImageServer proporciona estadísticas e información analítica utilizada para analizar el comportamiento del proceso interno de ImageServer.
   >
   Ejemplo de nombre de archivo de registro de Image Server: `ImageServer-57346-2020-07-25.log`
   >
   * s7access-&lt;yyyy>&lt;mm>&lt;dd>.log: el registro de acceso de s7registra cada solicitud realizada a Dynamic Media a través de `/is/image` y `/is/content`.
   >
   Estos registros solo se utilizan cuando Dynamic Media está habilitado. No se incluyen en la **Descargar completo** paquete que se genera a partir de `system/console/status-Bundlelist` página; al llamar a Asistencia al cliente si tiene un problema con Dynamic Media, anexe ambos registros al problema.

### Si instaló Experience Manager en un puerto o ruta de contexto diferente... {#if-you-installed-aem-to-a-different-port-or-context-path}

Si va a realizar la implementación [Experience Manager a un servidor de aplicaciones](/help/sites-deploying/application-server-install.md) y tener Dynamic Media habilitado, debe configurar el **dominio propio** en el Externalizador. De lo contrario, la generación de miniaturas para los recursos de no funciona correctamente para los de Dynamic Media.

Además, si ejecuta el inicio rápido en un puerto o ruta de contexto diferente, también tiene que cambiar el **dominio propio**.

Cuando Dynamic Media está habilitado, las representaciones de miniaturas estáticas para los recursos de imagen se generan mediante Dynamic Media. Para que la generación de miniaturas funcione correctamente en Dynamic Media, el Experience Manager debe realizar una solicitud de URL a sí mismo y debe conocer tanto el número de puerto como la ruta de contexto.

En el Experience Manager:

* El **dominio propio** en el [Externalizador](/help/sites-developing/externalizer.md) se utiliza para recuperar el número de puerto y la ruta de contexto.
* Si no **dominio propio** , el número de puerto y la ruta de contexto se recuperan del servicio HTTP de Jetty.

En una implementación WAR de QuickStart de Experience Manager, el número de puerto y la ruta de contexto no se pueden derivar, por lo que debe configurar un **dominio propio**. Consulte [Documentación del externalizador](/help/sites-developing/externalizer.md) sobre cómo configurar el **dominio propio**.

>[!NOTE]
>
En un [Implementación independiente de Quickstart de Experience Manager](/help/sites-deploying/deploy.md), a **dominio propio** generalmente no necesita configurarse, ya que el número de puerto y la ruta de contexto se pueden configurar automáticamente. Sin embargo, si todas las interfaces de red están desactivadas, debe configurar el **dominio propio**.

## Deshabilitar Dynamic Media  {#disabling-dynamic-media}

Dynamic Media no está habilitado de forma predeterminada. Sin embargo, si ya ha habilitado Dynamic Media, puede desactivarlo más adelante.

Para deshabilitar Dynamic Media después de haberla habilitado, quite el `-r dynamicmedia` indicador del modo de ejecución.

**Para deshabilitar Dynamic Media:**

1. En la línea de comandos, al iniciar el inicio rápido, puede realizar una de las siguientes acciones:

   * No añadir `-r dynamicmedia` a la línea de comandos al iniciar el archivo jar.

   ```shellsession {.line-numbers}
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar
   ```

1. Solicitud `https://localhost:4502/is/image`. Recibirá un mensaje que indica que Dynamic Media está deshabilitado.

   >[!NOTE]
   >
   Una vez deshabilitado el modo de ejecución de Dynamic Media, el paso del flujo de trabajo que genera la variable `cqdam.pyramid.tiff` la representación se omite automáticamente. También deshabilita la compatibilidad con representaciones dinámicas y otras funciones de Dynamic Media.
   >
   Tenga en cuenta también que cuando el modo de ejecución de Dynamic Media está deshabilitado después de configurar el servidor de Experience Manager, todos los recursos que se cargaron en ese modo de ejecución ahora no son válidos.

## (Opcional) Migre los ajustes preestablecidos y las configuraciones de Dynamic Media de la versión 6.3 a la versión 6.5 sin tiempo de inactividad {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

Si está actualizando Experience Manager - Dynamic Media de 6.3 a 6.5 (que ahora incluye la capacidad de realizar implementaciones sin tiempo de inactividad), debe ejecutar el siguiente comando curl. El comando migra todos los ajustes preestablecidos y configuraciones desde `/etc` hasta `/conf` en CRXDE Lite.

>[!NOTE]
>
Si ejecuta la instancia de Experience Manager en modo de compatibilidad (es decir, tiene instalado el paquete de compatibilidad), no necesita ejecutar estos comandos.

Para todas las actualizaciones, ya sea con o sin el paquete de compatibilidad, puede copiar los ajustes preestablecidos predeterminados del visualizador incorporado originalmente con Dynamic Media ejecutando el siguiente comando Linux® curl:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

Para migrar cualquier ajuste preestablecido y configuración de visor personalizado que haya creado desde `/etc` hasta `/conf`, ejecute el siguiente comando Linux® curl:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## Configurar la replicación de imágenes {#configuring-image-replication}

La entrega de imágenes de Dynamic Media funciona publicando recursos de imagen, incluidas miniaturas de vídeo, de Experience Manager Author y replicándolos en el servicio de replicación bajo demanda de Adobe (la URL del servicio de replicación). A continuación, los recursos se entregan mediante el servicio de entrega de imágenes bajo demanda (la URL del servicio de imágenes).

Haga lo siguiente:

1. [Configurar autenticación](#setting-up-authentication).
1. [Configuración del agente de replicación](#configuring-the-replication-agent).

El agente de replicación publica recursos de Dynamic Media, como imágenes y metadatos de vídeo, y establece en el servicio de imágenes alojado en el Adobe. El Agente de replicación no está habilitado de forma predeterminada.

Después de configurar el agente de replicación, debe [validar y probar que se ha configurado correctamente](#validating-the-replication-agent-for-dynamic-media). En esta sección se describen estos procedimientos.

>[!NOTE]
>
El límite de memoria predeterminado para la creación de PTIFF es de 3 GB en todos los flujos de trabajo. Por ejemplo, puede procesar una imagen que requiera 3 GB de memoria mientras otros flujos de trabajo están en pausa, o puede procesar 10 imágenes en paralelo que requieran 300 MB de memoria cada una.
>
El límite de memoria es configurable y se ajusta a la disponibilidad de recursos del sistema y al tipo de contenido de imagen que se procesa. Si tiene muchos recursos grandes y memoria suficiente en el sistema, puede aumentar este límite para asegurarse de que las imágenes se procesen en paralelo.
>
Se rechaza una imagen que requiera más del límite máximo de memoria.
>
Para cambiar el límite de memoria para la creación de PTIFF, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]** > **[!UICONTROL Adobe CQ Scene7 FiffManager]** y cambie el **[!UICONTROL maxMemory]** valor.

### Configurar autenticación {#setting-up-authentication}

Configure la autenticación de replicación en el autor para que pueda replicar imágenes en el servicio de entrega de imágenes de Dynamic Media. En primer lugar, obtenga un almacén de claves y guárdelo en la **[!UICONTROL dynamic-media-replication]** y configúrelo. El administrador de su empresa recibió un correo electrónico de bienvenida con el archivo KeyStore y las credenciales necesarias durante el proceso de aprovisionamiento. Si no recibe esta información, póngase en contacto con el servicio de atención al cliente de Adobe.

**Para configurar la autenticación:**

1. Póngase en contacto con Asistencia al cliente de Adobe para obtener el archivo y la contraseña de KeyStore si aún no dispone del archivo y la contraseña. Esta información es una parte necesaria del aprovisionamiento. Asocia las claves a su cuenta.

1. En Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.

1. En la página Administración de usuarios, vaya a **[!UICONTROL dynamic-media-replication]** usuario y, a continuación, seleccione para abrir.

   ![dm-replication](assets/dm-replication.png)

1. En la página Editar configuración de usuario para replicación de medios dinámicos, seleccione **[!UICONTROL Keystore]** pestaña, luego seleccione **[!UICONTROL Crear almacén de claves]**.

   ![dm-replication-keystore](assets/dm-replication-keystore.png)

1. Introduzca una contraseña y confírmela en la **[!UICONTROL Establecer contraseña de acceso a KeyStore]** Cuadro de diálogo.

   >[!NOTE]
   >
   Recuerde la contraseña porque debe introducirla de nuevo cuando configure el Agente de replicación más adelante.

   ![chlimage_1-508](assets/chlimage_1-508.png)

1. En el **[!UICONTROL Editar la configuración de usuario para la replicación de medios dinámicos]** , expanda la **Añadir clave privada del archivo de KeyStore** y agregue lo siguiente (consulte las imágenes que aparecen a continuación):

   * En el **[!UICONTROL Nuevo alias]** , introduzca el nombre de un alias que desee utilizar más adelante en la configuración de replicación. Por ejemplo, puede utilizar `replication` como un alias.
   * Seleccionar **[!UICONTROL Archivo de KeyStore]**. Vaya al archivo de KeyStore que le proporcionó el Adobe, selecciónelo y, a continuación, seleccione **[!UICONTROL Abrir]**.
   * En el **[!UICONTROL Contraseña del archivo de KeyStore]** , introduzca la contraseña del archivo de KeyStore. Esta contraseña es **no** Adobe la contraseña de KeyStore que creó en el paso 5, pero que es la contraseña de archivo de KeyStore proporcionada en el correo electrónico de bienvenida que se le envió durante el aprovisionamiento. Póngase en contacto con Atención al cliente de Adobe si no recibió una contraseña de archivo de KeyStore.
   * En el **[!UICONTROL Contraseña de clave privada]** , introduzca la contraseña de la clave privada (puede ser la misma contraseña de clave privada proporcionada en el paso anterior). Adobe proporciona la contraseña de la clave privada en el correo electrónico de bienvenida que se le ha enviado durante el . Póngase en contacto con Atención al cliente de Adobe si no recibió una contraseña de clave privada.
   * En el **[!UICONTROL Alias de clave privada]** , introduzca el alias de la clave privada. Por ejemplo, `*companyname*-alias`. Adobe proporciona el alias de la clave privada en el correo electrónico de bienvenida que se le ha enviado durante el . Póngase en contacto con Atención al cliente de Adobe si no recibió un alias de clave privada.

   ![edit_settings_fordynamic-media-replication2](assets/edit_settings_fordynamic-media-replication2.png)

1. Seleccionar **[!UICONTROL Guardar y cerrar]** para guardar los cambios realizados en este usuario.

   A continuación, debe [configuración del agente de replicación](#configuring-the-replication-agent).

### Configuración del agente de replicación {#configuring-the-replication-agent}

1. En Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Implementación]** > **[!UICONTROL Replicación]** > **[!UICONTROL Agentes en el autor]**.
1. En la página Agentes del autor, seleccione **[!UICONTROL Replicación de imagen híbrida de Dynamic Media (s7delivery)]**.
1. Seleccione **[!UICONTROL Editar]**.
1. Seleccione el **[!UICONTROL Configuración]** y, a continuación, introduzca lo siguiente:

   * **[!UICONTROL Habilitado]** - Seleccione esta casilla de verificación para habilitar el agente de replicación.
   * **[!UICONTROL Región]** - Configure en la región adecuada: Norteamérica, Europa o Asia
   * **[!UICONTROL ID de inquilino]** - Este valor es el nombre de su empresa/inquilino que está publicando en el servicio de replicación. Este valor es el ID de inquilino que proporciona el Adobe en el correo electrónico de bienvenida que se le ha enviado durante el aprovisionamiento. Si no recibe esta información, póngase en contacto con el servicio de atención al cliente de Adobe.
   * **[!UICONTROL Alias de almacén de claves]** - Este valor es el mismo que el **Nuevo alias** valor establecido al generar la clave en [Configuración de la autenticación](#setting-up-authentication); por ejemplo, `replication`. (Consulte el paso 7 de [Configuración de la autenticación](#setting-up-authentication).)
   * **[!UICONTROL Contraseña de almacén de claves]** - La contraseña de KeyStore que se creó al pulsar **[!UICONTROL Crear almacén de claves]**. El Adobe no proporciona esta contraseña. Consulte el paso 5 de [Configuración de la autenticación](#setting-up-authentication).

   La siguiente imagen muestra el agente de replicación con datos de ejemplo:

   ![chlimage_1-509](assets/chlimage_1-509.png)

1. Seleccionar **[!UICONTROL OK]**.

### Validación del agente de replicación para Dynamic Media {#validating-the-replication-agent-for-dynamic-media}

Para validar el agente de replicación para Dynamic Media, haga lo siguiente:

Seleccionar **[!UICONTROL Probar conexión]**. Ejemplo de salida es la siguiente:

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
>
También puede comprobarlo realizando una de las siguientes acciones:
>
* Compruebe los registros de replicación para asegurarse de que el recurso esté replicado.
* Publique una imagen. Seleccione la imagen y seleccione **[!UICONTROL Espectadores]** en el menú desplegable, seleccione un ajuste preestablecido de visualizador. Seleccionar **[!UICONTROL URL]**. Para comprobar que puede ver la imagen, copie y pegue la ruta URL en el explorador.
>

### Solucionar problemas de autenticación {#troubleshooting-authentication}

Al configurar la autenticación, puede encontrar algunos problemas con sus soluciones. Antes de comprobar estos problemas, asegúrese de haber configurado la replicación.

#### Problema: Código de estado HTTP 401 con mensaje: se requiere autorización {#problem-http-status-code-with-message-authorization-required}

Este problema puede deberse a un error al configurar el almacén de claves para `dynamic-media-replication` usuario.

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

**Solución:**
Compruebe que la variable `KeyStore` se ha guardado en **dynamic-media-replication** usuario y se proporciona con la contraseña correcta.

#### Problema: No Se Pudo Descifrar La Clave - No Se Pudieron Descifrar Los Datos {#problem-could-not-decrypt-key-could-not-decrypt-data}

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

**Solución:**
Compruebe la contraseña. La contraseña guardada en el agente de replicación no es la misma contraseña que se utilizó para crear el almacén de claves.

#### Problema: InvalidAlgorithmParameterException {#problem-invalidalgorithmparameterexception}

Este problema se debe a un error de configuración en la instancia de autor de Experience Manager. El proceso Java™ del autor no está obteniendo el correcto `javax.net.ssl.trustStore`. Verá este error en el registro de replicación:

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

**Solución:**
Asegúrese de que el proceso de Java™ del Autor del Experience Manager tenga la propiedad del sistema `-Djavax.net.ssl.trustStore=` establezca en un almacén de confianza válido.

#### Problema: KeyStore no está configurado o no se ha inicializado {#problem-keystore-is-either-not-set-up-or-it-is-not-initialized}

Es probable que este problema se deba a una corrección rápida o a que un paquete de funciones sobrescriba el nodo dynamic-media-user o keystore.

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

**Solución:**

1. Navegue hasta la página Administración de usuarios:
   `localhost:4502/libs/granite/security/content/useradmin.html`
1. En la página Administración de usuarios, vaya a `dynamic-media-replication` usuario y, a continuación, seleccione para abrir.
1. Seleccione el **[!UICONTROL KeyStore]** pestaña. Si la variable **[!UICONTROL Crear almacén de claves]** aparece el botón y debe volver a realizar los pasos en [Configuración de la autenticación](#setting-up-authentication) antes.
1. Si tuvo que rehacer la configuración de KeyStore, debe hacer lo siguiente [Configuración del agente de replicación](/help/assets/config-dynamic.md#configuring-the-replication-agent) otra vez, también.

   Vuelva a configurar el agente de replicación de s7delivery.
   `localhost:4502/etc/replication/agents.author/s7delivery.html`

1. Seleccionar **[!UICONTROL Probar conexión]** para que pueda comprobar que la configuración es válida.

#### Problema: El agente de publicación utiliza SSL en lugar de OAuth {#problem-publish-agent-is-using-ssl-instead-of-oauth}

Es probable que este problema se deba a una revisión o a que un paquete de funciones no se instaló correctamente o sobrescribió la configuración.

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

1. En Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.

   `localhost:4502/crx/de/index.jsp`

1. Vaya al nodo s7delivery Replication Agent.
   `localhost:4502/crx/de/index.jsp#/etc/replication/agents.author/s7delivery/jcr:content`

1. Agregue esta configuración al agente de replicación (booleano con el valor establecido en ) **[!UICONTROL Verdadero]**):

   `enableOauth=true`

1. Cerca de la esquina superior izquierda de la página, seleccione **[!UICONTROL Guardar todo]**.

### Pruebe la configuración {#testing-your-configuration}

El Adobe recomienda realizar una prueba completa de la configuración.

Asegúrese de haber realizado lo siguiente antes de comenzar esta prueba:

* Se agregaron ajustes preestablecidos de imagen.
* Configurar **[!UICONTROL Configuración de Dynamic Media (anterior a 6.3)]** bajo Cloud Service. Se requiere la URL del servicio de imágenes para esta prueba

**Para probar la configuración:**

1. Cargue un recurso de imagen. (En Assets, vaya a **[!UICONTROL Crear]** > **[!UICONTROL Archivos]** y seleccione el archivo).
1. Espere a que finalice el flujo de trabajo.
1. Publique el recurso de imagen. (Seleccione el recurso y seleccione **[!UICONTROL Publicación rápida]**.)
1. Vaya a las representaciones de esa imagen al abrir la imagen y pulsar **[!UICONTROL Representaciones]**.

   ![chlimage_1-510](assets/chlimage_1-510.png)

1. Seleccione cualquier representación dinámica.
1. Para obtener la URL de este recurso, seleccione **[!UICONTROL URL]**.
1. Vaya a la dirección URL seleccionada y compruebe si la imagen se comporta según lo esperado.

Otra forma de probar que los recursos se entregaron es anexar req=exists a la dirección URL.

## Configuración de Cloud Service de Dynamic Media {#configuring-dynamic-media-cloud-services}

El Cloud Service de Dynamic Media admite la publicación y entrega híbridas de imágenes y vídeo, análisis de vídeo y codificación de vídeo, entre otras cosas.

Como parte de la configuración, debe introducir un ID de registro, una URL de servicio de vídeo, una URL de servicio de imagen, una URL de servicio de replicación y configurar la autenticación. Esta información se le envió por correo electrónico como parte del proceso de aprovisionamiento de cuentas. Si no recibe esta información, póngase en contacto con el administrador de Adobe Experience Manager o con Asistencia al cliente de Adobe para obtener la información.

>[!NOTE]
>
Antes de configurar los Cloud Service de Dynamic Media, asegúrese de que ha configurado la instancia de publicación. También debe tener configurada la replicación antes de configurar los Cloud Service de Dynamic Media.

**Para configurar los Cloud Service de Dynamic Media:**

1. En Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configuración de Dynamic Media (anterior a 6.3)]**.
1. En la página Explorador de configuración de Dynamic Media, en el panel izquierdo, seleccione **[!UICONTROL global]**, luego seleccione **[!UICONTROL Crear]**.
1. En el **[!UICONTROL Crear configuración de Dynamic Media]** , en el campo Título, escriba un título.
1. Si está configurando Dynamic Media para vídeo,

   * En el **[!UICONTROL ID de registro]** , escriba su ID de registro.
   * En el **[!UICONTROL URL del servicio de vídeo]** , introduzca la URL del servicio de vídeo para Dynamic Media Gateway.

1. Si está configurando Dynamic Media para imágenes, en la **[!UICONTROL URL del servicio de imágenes]** , introduzca la URL del servicio de imágenes para Dynamic Media Gateway.
1. Seleccionar **[!UICONTROL Guardar]** para volver a la página Explorador de configuración de Dynamic Media.
1. Para acceder a la consola de navegación global, seleccione el logotipo del Experience Manager.

## Configuración de informes de vídeo {#configuring-video-reporting}

Puede configurar los informes de vídeo en varias instalaciones de Experience Manager mediante Dynamic Media Hybrid.

**Cuándo usar:** Al configurar la Configuración de Dynamic Media (anterior a 6.3), se inician numerosas funciones, incluidos los informes de vídeo. La configuración crea un grupo de informes en una empresa regional de Analytics. Si configura varios nodos Author, creará un grupo de informes independiente para cada uno de ellos. Como resultado, los datos de los informes no son coherentes entre las instalaciones. Además, si cada nodo Autor hace referencia al mismo servidor de publicación híbrido, la última instalación de Autor cambia el grupo de informes de destino para todos los informes de vídeo. Este problema sobrecarga el sistema de Analytics con demasiados grupos de informes.

**Introducción a:** Configure los informes de vídeo realizando las tres tareas siguientes.

1. Cree un paquete de ajustes preestablecidos de Video Analytics después de configurar Dynamic Media Configuration (anterior a 6.3) en el primer nodo Author. Esta tarea inicial es importante porque permite que una nueva configuración siga utilizando el mismo grupo de informes.
1. Instale el paquete de ajustes preestablecidos de Video Analytics en cualquier ***nuevo*** Nodo Autor ***antes*** puede configurar la configuración de Dynamic Media (anterior a 6.3).
1. Compruebe y depure la instalación del paquete.

### Cree un paquete de ajustes preestablecidos de Video Analytics después de configurar el primer nodo Autor {#creating-a-video-analytics-preset-package-after-configuring-the-first-author-node}

Cuando haya terminado esta tarea, tendrá un archivo de paquete que contiene los ajustes preestablecidos de Video Analytics. Estos ajustes preestablecidos contienen un grupo de informes, el servidor de seguimiento, el área de nombres de seguimiento y el ID de organización de Experience Cloud, si están disponibles.

1. Si aún no lo ha hecho, configure Configuración de Dynamic Media (anterior a 6.3).
1. (Opcional) Consulte y copie la ID del grupo de informes (debe tener acceso al JCR). Aunque no es obligatorio tener el ID del grupo de informes, facilita la validación.
1. Cree un paquete con el Administrador de paquetes.
1. Edite el paquete para incluir un filtro.

   En el Experience Manager: `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

1. Genere el paquete.
1. Descargue o comparta el paquete de ajustes preestablecidos de Video Analytics para que se pueda compartir con los nuevos nodos de Author subsiguientes.

### Instale el paquete de ajustes preestablecidos de Video Analytics antes de configurar más nodos de autor {#installing-the-video-analytics-preset-package-before-you-configure-additional-author-nodes}

Asegúrese de completar esta tarea ***antes*** puede configurar la configuración de Dynamic Media (anterior a 6.3). Si no se hace esto, se creará otro grupo de informes que no se esté utilizando. Además, aunque los informes de vídeo siguen funcionando correctamente, la recopilación de datos no está optimizada.

Asegúrese de que se puede acceder al paquete de ajustes preestablecidos de Video Analytics desde el primer nodo Autor en el nuevo nodo Autor.

1. Cargue el paquete de ajustes preestablecidos de Video Analytics que creó anteriormente en el Administrador de paquetes.
1. Instale el paquete de ajustes preestablecidos de Video Analytics.
1. Configure la Configuración de Dynamic Media (anterior a 6.3).

### Verificar y depurar la instalación del paquete {#verifying-and-debugging-the-package-installation}

1. Realice una de las siguientes acciones para verificar y, si es necesario, depurar la instalación del paquete:

   * **Compruebe el ajuste preestablecido de Video Analytics mediante el JCR**
Para comprobar el ajuste preestablecido de Video Analytics mediante el JCR, debe tener acceso al CRXDE Lite.

     Experience Manager: en CRXDE Lite, vaya a `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

     Como en `https://localhost:4502/crx/de/index.jsp#/conf/global/settings/dam/dm/presets/analytics/jcr%3Acontent/userdata`

     Si no tiene acceso al CRXDE Lite en el nodo Autor, puede comprobar el ajuste preestablecido a través del servidor de publicación.

   * **Compruebe el ajuste preestablecido de Video Analytics en el servidor de imágenes**

     Puede validar el ajuste preestablecido de Video Analytics directamente realizando una solicitud req=userdata de Image Server.
Por ejemplo, para ver el ajuste preestablecido de Analytics en el nodo Autor, puede realizar la siguiente solicitud:

     `https://localhost:4502/is/image/conf/global/settings/dam/dm/presets/analytics?req=userdata`

     Para validar el ajuste preestablecido en los servidores de publicación, puede realizar una solicitud directa similar al servidor de publicación. Las respuestas son las mismas en los nodos Author y Publish. La respuesta tiene un aspecto similar al siguiente:

     ```
     marketingCloudOrgId=0FC4E86B573F99CC7F000101
      reportSuite=aemaem6397618-2018-05-23
      trackingNamespace=aemvideodal
      trackingServer=aemvideodal.d2.sc.omtrdc.net
     ```

   * **Compruebe el ajuste preestablecido de Video Analytics con la herramienta de informes de vídeo en Experience Manager**
Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Informes de vídeo]**

     `https://localhost:4502/mnt/overlay/dam/gui/content/s7dam/videoreports/videoreport.html`

     Si ve el siguiente mensaje de error, el grupo de informes está disponible, pero no se ha rellenado. Este error es correcto (y lo desea) en una nueva instalación antes de que el sistema recopile datos.

   ![screen_shot_2018-05-23at52254pm](assets/screen_shot_2018-05-23at52254pm.png)

   Para generar datos de informes, cargue y publique un vídeo. Uso **[!UICONTROL Copiar URL]** y ejecute el vídeo al menos una vez.

   Pueden pasar hasta 12 horas antes de que los datos de informes se rellenen a partir del uso del Visor de vídeo.

   Si se produce un error y el grupo de informes no se configura correctamente, se muestra la siguiente alerta.

   ![screen_shot_2018-05-23at52612pm](assets/screen_shot_2018-05-23at52612pm.png)

   Este error también se muestra si se ejecuta Informes de vídeo antes de configurar los servicios de Configuración de Dynamic Media (anterior a 6.3).

### Solucionar problemas de configuración de informes de vídeo {#troubleshooting-the-video-reporting-configuration}

* Durante la instalación, a veces se agota el tiempo de espera de las conexiones al servidor de API de Analytics. La instalación reintenta la conexión 20 veces, pero sigue fallando. Cuando se produce esta situación, el archivo de registro registra varios errores. Buscar por `SiteCatalystReportService`.
* Si no instala primero el paquete de ajustes preestablecidos de Analytics, se puede crear un nuevo grupo de informes.
* La actualización de Experience Manager 6.3 a Experience Manager 6.4 o Experience Manager 6.4.1 y, a continuación, la configuración de Dynamic Media (anterior a 6.3), sigue creando un grupo de informes. Se sabe que este problema está programado para solucionarse en el Experience Manager 6.4.2.

### Acerca del ajuste preestablecido de Video Analytics {#about-the-video-analytics-preset}

El ajuste preestablecido de Video Analytics, a veces denominado simplemente ajuste preestablecido de Analytics, se almacena junto a los ajustes preestablecidos de Visor en Dynamic Media. Es básicamente igual que un ajuste preestablecido de Visor, pero con información utilizada para configurar los informes de AppMeasurement y Video Heartbeat.

Las propiedades del ajuste preestablecido son las siguientes:

* `reportSuite`
* `trackingServer`
* `trackingNamespace`
* `marketingCloudOrgId` (no está presente en las versiones anteriores del Experience Manager)

Experience Manager 6.4 y versiones más recientes guardan este ajuste preestablecido en `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

## Replicar configuración del catálogo {#replicating-catalog-settings}

Publique su propia configuración de catálogo predeterminada como parte del proceso de configuración a través del JCR. Para replicar la configuración del catálogo:

1. En una ventana de terminal, ejecute lo siguiente:

   `curl -u admin:admin localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

1. En Experience Manager, vaya a la siguiente ubicación en CRXDE Lite (requiere privilegios de administrador):

   `https://<*server*>:<*port*>/crx/de/index.jsp#/conf/global/settings/dam/dm/imageserver/`

1. Seleccione el **[!UICONTROL Replicación]** pestaña.
1. Seleccionar **[!UICONTROL Replicar]**.

## Replicar ajustes preestablecidos de visor {#replicating-viewer-presets}

Para enviar *Para un recurso con un ajuste preestablecido de visualizador, debe replicar/publicar* el ajuste preestablecido de visor. (Todos los ajustes preestablecidos del visor deben activarse) *y* replicado para obtener la URL o el código incrustado de un recurso.
Consulte [Publicar ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md#publishing-viewer-presets) para obtener más información.

>[!NOTE]
>
De forma predeterminada, el sistema muestra varias representaciones al seleccionar **[!UICONTROL Representaciones]** y varios ajustes preestablecidos de visualizador al seleccionar **[!UICONTROL Espectadores]** en la vista de detalles del recurso. Puede aumentar o disminuir el número de visualizaciones. Consulte [Aumente el número de ajustes preestablecidos de imagen que se muestran](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) o [Aumente el número de ajustes preestablecidos de visualizador que se muestran](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

## Filtrado de recursos para la replicación {#filtering-assets-for-replication}

En implementaciones que no son de Dynamic Media, puede realizar la replicación *todo* recursos (tanto imágenes como vídeo) del entorno de creación del Experience Manager al nodo de publicación del Experience Manager. Este flujo de trabajo es necesario porque los servidores de publicación de Experience Manager también proporcionan los recursos.

Sin embargo, en implementaciones de Dynamic Media, como los recursos se entregan a través de la nube, no es necesario replicar esos mismos recursos en nodos de publicación de Experience Manager. Este flujo de trabajo de &quot;publicación híbrida&quot; evita costes de almacenamiento adicionales y tiempos de procesamiento más largos para replicar recursos. Otros contenidos, como los visualizadores de Dynamic Media, las páginas del sitio y el contenido estático, se siguen mostrando desde los nodos de publicación del Experience Manager.

Además de replicar los recursos, también se replican los siguientes recursos que no son de:

* Configuración de envío de Dynamic Media: `/conf/global/settings/dam/dm/imageserver/jcr:content`
* Ajustes preestablecidos de imagen: `/conf/global/settings/dam/dm/presets/macros`
* Ajustes preestablecidos de visor: `/conf/global/settings/dam/dm/presets/viewer`

Los filtros proporcionan una forma de *excluir* los recursos no se replicarán en el nodo de publicación Experience Manager.

### Usar filtros de recursos predeterminados para la replicación {#using-default-asset-filters-for-replication}

Si utiliza Dynamic Media para (1) imágenes en producción *o* (2) imágenes y vídeo, a continuación, puede utilizar los filtros predeterminados que proporciona el Adobe tal cual. Los siguientes filtros están activos de forma predeterminada:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Filter</strong></td>
   <td><strong>Tipo MIME</strong></td>
   <td><strong>Representaciones</strong></td>
  </tr>
  <tr>
   <td>Entrega de imágenes de Dynamic Media</td>
   <td><p>filter-images</p> <p>conjuntos de filtros</p> <p> </p> </td>
   <td><p>Comienza por <strong>image/</strong></p> <p>Contains <strong>application/</strong> y termina por <strong>set</strong>.</p> </td>
   <td>Los "filter-images" predeterminados (se aplica a recursos de imágenes únicas, incluidas imágenes interactivas) y "filter-sets" (se aplica a conjuntos de giros, conjuntos de imágenes, conjuntos de medios mixtos y conjuntos de carrusel):
    <ul>
     <li>Incluir imágenes PTIFF y metadatos para replicación (cualquier representación que comience por <strong>cqdam</strong>).</li>
     <li>Excluir de la replicación las representaciones de imagen original e imagen estática.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Entrega de vídeo en Dynamic Media</td>
   <td>filter-video</td>
   <td>Comienza por <strong>video/</strong></td>
   <td>El "filter-video" incorporado hará lo siguiente:
    <ul>
     <li>Incluya representaciones de vídeo proxy, miniaturas de vídeo/imagen de póster, metadatos (tanto en representaciones de vídeo como de vídeo principales) para la replicación (cualquier representación que comience por <strong>cqdam</strong>).</li>
     <li>Excluya de la replicación el vídeo original y las representaciones de miniaturas estáticas.<br /> <br /> <strong>Nota:</strong> Las representaciones de vídeo proxy no contienen binarios, sino que solo son propiedades de nodo. Por lo tanto, no afecta al tamaño del repositorio del editor.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Integración de Dynamic Media Classic (Scene7)</td>
   <td><p>filter-images</p> <p>conjuntos de filtros</p> <p>filter-video</p> </td>
   <td><p>Comienza por <strong>image/</strong></p> <p>Contains <strong>application/</strong> y termina por <strong>set</strong>.</p> <p>Comienza por <strong>video/</strong></p> </td>
   <td><p>Puede configurar el URI de transporte para que apunte al servidor de publicación de Experience Manager en lugar de a la URL del servicio de replicación en la nube de Dynamic Media de Adobe. La configuración de este filtro permite que Dynamic Media Classic envíe recursos en lugar de la instancia de publicación del Experience Manager.</p> <p>Los "filter-images", "filter-sets" y "filter-video" predeterminados harán lo siguiente:</p>
    <ul>
     <li>Incluya imágenes PTIFF, representaciones de vídeo proxy y metadatos para la replicación. Sin embargo, como no existen en el JCR (para los que ejecutan Experience Manager), la integración de Dynamic Media Classic no hace nada.</li>
     <li>Excluya de la replicación la imagen original, las representaciones de imágenes estáticas, el vídeo original y las representaciones de miniaturas estáticas. En su lugar, Dynamic Media Classic ofrece recursos de imagen y vídeo.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
Los filtros se aplican a los tipos MIME y no pueden ser específicos de la ruta.

### Configurar filtros de recursos para implementaciones solo de vídeo {#setting-up-asset-filters-for-video-only-deployments}

Si utiliza Dynamic Media solo para vídeo, siga estos pasos para configurar filtros de recursos para la replicación:

1. En Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Implementación]** > **[!UICONTROL Replicación]** > **[!UICONTROL Agentes en el autor]**.
1. En la página Agentes del autor, seleccione **[!UICONTROL Agente predeterminado (publicar)]**.
1. Seleccione **[!UICONTROL Editar]**.
1. En el **[!UICONTROL Configuración de agente]** , en el **[!UICONTROL Configuración]** pestaña, marca **[!UICONTROL Habilitado]** para activar el agente.
1. Seleccionar **[!UICONTROL OK]**.
1. En Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. En el árbol de carpetas izquierdo, navegue hasta `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`
1. Localizar **[!UICONTROL filter-video]**, haga clic con el botón derecho en él y seleccione **[!UICONTROL Copiar]**.
1. En el árbol de carpetas izquierdo, navegue hasta `/etc/replication/agents.author/publish`
1. Localizar `jcr:content`, haga clic con el botón derecho en él y seleccione **[!UICONTROL Pegar]**.

Estos pasos configuran la instancia Publicación del Experience Manager para que proporcione la imagen de póster de vídeo y los metadatos de vídeo necesarios para la reproducción, mientras que el propio vídeo lo proporciona el Cloud Service de Dynamic Media. El filtro también excluye de la replicación el vídeo original y las representaciones de miniaturas estáticas, que no son necesarias en la instancia de publicación.

### Configuración de filtros de recursos para imágenes en implementaciones que no sean de producción {#setting-up-asset-filters-for-imaging-in-non-production-deployments}

Si utiliza Dynamic Media para generar imágenes en implementaciones que no sean de producción, siga estos pasos para configurar filtros de recursos para la replicación:

1. En Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Implementación]** > **[!UICONTROL Replicación]** > **[!UICONTROL Agentes en el autor]**.
1. En la página Agentes del autor, seleccione **[!UICONTROL Agente predeterminado (publicar)]**.
1. Seleccione **[!UICONTROL Editar]**.
1. En el **[!UICONTROL Configuración de agente]** , en el **[!UICONTROL Configuración]** pestaña, marca **[!UICONTROL Habilitado]** para activar el agente.
1. Seleccionar **[!UICONTROL OK]**.
1. En Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. En el árbol de carpetas izquierdo, navegue hasta `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`

   ![image-2018-01-16-10-22-40-410](assets/image-2018-01-16-10-22-40-410.png)

1. Localizar **[!UICONTROL filter-images]**, haga clic con el botón derecho en él y seleccione **[!UICONTROL Copiar]**.
1. En el árbol de carpetas izquierdo, navegue hasta `/etc/replication/agents.author/publish`
1. Localizar `jcr:content`, haga clic con el botón derecho en él y, a continuación, vaya a **[!UICONTROL Crear]** > **[!UICONTROL Crear nodo]**. Introduzca el nombre `damRenditionFilters` de tipo `nt:unstructured`.
1. Localizar `damRenditionFilters`, haga clic con el botón derecho en él y seleccione **[!UICONTROL Pegar]**.

Estos pasos configuran la instancia Publicación del Experience Manager para entregar las imágenes en el entorno que no sea de producción. El filtro también excluye de la replicación la imagen original y las representaciones estáticas, que no son necesarias en la instancia de publicación.

>[!NOTE]
>
Si hay muchos filtros diferentes en un autor, cada agente necesita que se le asigne un usuario diferente. El código Granite aplica un modelo de filtro por usuario. Siempre tenga un usuario diferente para cada configuración de filtro.
>
¿Está utilizando más de un filtro en un servidor? Por ejemplo, un filtro para que se publique la replicación y un segundo filtro para la entrega de s7. Si es así, debe asegurarse de que estos dos filtros tengan un **userId** asignado a ellos en la `jcr:content` nodo. Vea la siguiente imagen:

![image-2018-01-16-10-26-28-465](assets/image-2018-01-16-10-26-28-465.png)

### Personalizar filtros de recursos para la replicación (opcional) {#customizing-asset-filters-for-replication}

1. En Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. En el árbol de carpetas izquierdo, navegue hasta `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters` para revisar los filtros.

   ![chlimage_1-511](assets/chlimage_1-511.png)

1. Para definir el tipo MIME para el filtro, puede localizar el tipo MIME de la siguiente manera:

   En el carril izquierdo, expanda `content > dam > <locate_your_asset> >  jcr:content > metadata` y, a continuación, en la tabla, busque `dc:format`.

   El siguiente gráfico es un ejemplo de la ruta de un recurso a `dc:format`.

   ![chlimage_1-512](assets/chlimage_1-512.png)

   Observe que la variable `dc:format` para el recurso `Fiji Red.jpg` es `image/jpeg`.

   Para que este filtro se aplique a todas las imágenes, independientemente de su formato, establezca el valor en `image/*` donde `*` es una expresión regular que se aplica a todas las imágenes de cualquier formato.

   Para que el filtro se aplique solo a imágenes del JPEG de tipo, introduzca un valor de `image/jpeg`.

1. Defina qué representaciones desea incluir o excluir de la replicación.

   Los caracteres que puede utilizar para filtrar la replicación son los siguientes:

   | Carácter que utilizar | Cómo filtra los recursos para la replicación |
   | --- | --- |
   | `*` | Carácter comodín |
   | `+` | Incluye recursos para la replicación |
   | `-` | Excluye recursos de la replicación |

   Navegue hasta `content/dam/<locate your asset>/jcr:content/renditions`.

   El siguiente gráfico es un ejemplo de las representaciones de un recurso.

   ![chlimage_1-513](assets/chlimage_1-4.png)

   En el ejemplo anterior, si solo desea duplicar el PTIFF (TIFF piramidal), debe introducir `+cqdam,*` que incluye todas las representaciones que comienzan con `cqdam`. En el ejemplo, esa representación es `cqdam.pyramid.tiff`.

   Si solo desea replicar el original, debe introducir `+original`.

## Configuración del servidor de imágenes de Dynamic Media {#configuring-dynamic-media-image-server-settings}

La configuración del servidor de imágenes de Dynamic Media implica la edición del paquete Adobe CQ Scene7 ImageServer y del paquete Adobe CQ Scene7 Platform Server.

>[!NOTE]
>
Dynamic Media funciona de forma predeterminada [una vez activado](#enabling-dynamic-media). Sin embargo, si lo desea, puede ajustar la instalación configurando Dynamic Media Image Server para que cumpla determinadas especificaciones o requisitos.

**Requisito previo** - *Antes* Cuando configure Dynamic Media Image Server, asegúrese de que la VM de Windows® incluye una instalación de las bibliotecas de Microsoft® Visual C++. Las bibliotecas son necesarias para ejecutar Dynamic Media Image Server. Puede [descargue el paquete redistribuible de Microsoft® Visual C++ 2010 (x64) aquí](https://www.microsoft.com/en-us/download/details.aspx?id=26999).

Para establecer la configuración de Dynamic Media Image Server:

1. En la esquina superior izquierda de Experience Manager, seleccione **[!UICONTROL Adobe Experience Manager]** para acceder a la consola de navegación global, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
1. En la página Configuración de la consola web de Adobe Experience Manager, vaya a **[!UICONTROL OSGi]** > **[!UICONTROL Configuración]** para enumerar todos los paquetes que se están ejecutando actualmente en Experience Manager.

   Los servidores de entrega de Dynamic Media se encuentran con los siguientes nombres en la lista:

   * `Adobe CQ Scene7 ImageServer`
   * `Adobe CQ Scene7 PlatformServer`

1. En la lista de paquetes, a la derecha de Adobe CQ Scene7 ImageServer, seleccione la **[!UICONTROL Editar]** icono.
1. En el cuadro de diálogo Adobe CQ Scene7 ImageServer, defina los siguientes valores de configuración:

   >[!NOTE]
   >
   Normalmente, no es necesario cambiar los valores predeterminados. Sin embargo, si cambia los valores predeterminados, debe reiniciar el paquete para que los cambios surtan efecto.

   | Propiedad | Valor predeterminado | Descripción |
   | --- | --- | --- |
   | `TcpPort.name` | *`empty`* | Número de puerto que se utilizará para la comunicación con el proceso de ImageServer. De forma predeterminada, el puerto libre se detecta automáticamente. |
   | `AllowRemoteAccess.name` | *`empty`* | Permitir o impedir el acceso remoto al proceso de ImageServer. Si es false, el servidor de imágenes solo escucha en localhost.<br> La configuración del externalizador predeterminado que apunta al host local debe especificar el dominio o la dirección IP reales de la instancia de VM específica. El motivo es que el host local apunta al sistema principal de la VM.<br>Los dominios o direcciones IP de la VM deben tener una entrada de archivo host para que pueda resolverse por sí misma. |
   | `MaxRenderRgnPixels` | 16 MP | Tamaño máximo en megapíxeles que se procesa. |
   | `MaxMessageSize` | 16 MB | Tamaño máximo del mensaje en megabytes que se envía. |
   | `RandomAccessUrlTimeout` | 20 | Valor de tiempo de espera del tiempo en segundos que el servidor de imágenes espera a que el JCR responda a una solicitud de mosaico de intervalo. |
   | `WorkerThreads` | 10 | Número máximo de subprocesos de trabajo. |

1. Seleccione **[!UICONTROL Guardar]**.
1. En la lista de paquetes, a la derecha de Adobe CQ Scene7 Platform Server, seleccione la **[!UICONTROL Editar]** icono.
1. En el cuadro de diálogo Adobe CQ Scene7 Platform Server, defina las siguientes opciones de valor predeterminadas:

   >[!NOTE]
   >
   Dynamic Media Image Server utiliza su propia caché de disco para almacenar en caché las respuestas. La caché HTTP del Experience Manager y Dispatcher no se pueden usar para almacenar en caché las respuestas del servidor de imágenes de Dynamic Media.

   | Propiedad | Valor predeterminado | Descripción |
   |---|---|---|
   | Caché activada | Comprobado | Si la caché de respuestas está habilitada |
   | Raíces de caché | escondrijo | Una o varias rutas a las carpetas de la caché de respuestas. Las rutas relativas se resuelven en la carpeta del paquete de imagen s7 interna. |
   | Tamaño máximo de caché | 200000000 | Tamaño máximo de la caché de respuestas en bytes. |
   | Entradas máximas de caché | 100 000 | Número máximo de entradas permitidas en la caché. |

### Configuración de manifiesto predeterminada {#default-manifest-settings}

El manifiesto predeterminado permite configurar los valores predeterminados que se utilizan para generar las respuestas de envío de Dynamic Media. Puede ajustar la calidad (calidad JPEG, resolución, modo de remuestreo), el almacenamiento en caché (caducidad) y evitar la representación de imágenes demasiado grandes (defaultpix, defaultthumbpix, maxpix).

La ubicación de la configuración de manifiesto predeterminada se toma del **[!UICONTROL Raíz de catálogo]** valor predeterminado de **[!UICONTROL Adobe CQ Scene7 PlatformServer]** paquete. De forma predeterminada, este valor se encuentra en la siguiente ruta dentro de **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**

`/conf/global/settings/dam/dm/imageserver/`

![Configuración del servidor de imágenes en CRXDE Lite](assets/configimageservercrxdelite.png)

Puede cambiar los valores de las propiedades, tal como se describe en la tabla siguiente, introduciendo nuevos valores.

Cuando haya terminado de cambiar el manifiesto predeterminado, en la esquina superior izquierda de la página, seleccione **[!UICONTROL Guardar todo]**.

Asegúrese de seleccionar la **[!UICONTROL Control de acceso]** (a la derecha de la pestaña Properties) y establezca los privilegios de control de acceso en `jcr:read` para todos los usuarios y dynamic-media-replication.

![Configuración de Image Server en el CRXDE Lite y de la pestaña Control de acceso](assets/configimageservercrxdeliteaccesscontroltab.png)

Configuración de tabla de manifiesto y sus valores predeterminados:

| Propiedad | Valor predeterminado | Descripción |
| --- | --- | --- |
| `bkgcolor` | `FFFFFF` | Color de fondo predeterminado. Valor de RGB que se utiliza para rellenar las áreas de la imagen de respuesta que no contengan datos de imagen reales. Consulte también [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html#image-serving-api) en la API del servicio de imágenes. |
| `defaultpix` | `300,300` | Tamaño de vista predeterminado. El servidor limita el tamaño de las imágenes de respuesta a esta altura y anchura máximas, a no ser que la solicitud especifique el tamaño de vista por medio de wid=, hei= o scl=.<br>Se especifica como dos números enteros, 0 o más, separados por una coma. Ancho y alto en píxeles. Cualquiera de los dos valores, o ambos, se puede establecer en 0 para mantenerlos sin restricciones. No se aplica a solicitudes anidadas o incrustadas.<br>Consulte también [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html#image-serving-api) en la API del servicio de imágenes.<br>Sin embargo, normalmente utiliza un ajuste preestablecido de visualizador o de imagen para entregar el recurso. La opción predeterminada solo se aplica a un recurso que no utiliza un ajuste preestablecido de visualizador o de imagen. |
| `defaultthumbpix` | `100,100` | Tamaño de miniatura predeterminado. Se utiliza en lugar del atributo::DefaultPix para solicitudes de miniaturas (`req=tmb`).<br>El servidor limita el tamaño de las imágenes de respuesta a esta altura y anchura máximas. Esta acción es verdadera si se realiza una solicitud de miniatura (`req=tmb`) no especifica el tamaño explícitamente y no especifica el tamaño de vista explícitamente usando `wid=`, `hei=`, o `scl=`.<br>Se especifica como dos números enteros, 0 o más, separados por una coma. Ancho y alto en píxeles. Cualquiera de los dos valores, o ambos, se puede establecer en 0 para mantenerlos sin restricciones.<br>No se aplica a solicitudes anidadas o incrustadas.<br>Consulte también [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html#image-serving-api) en la API del servicio de imágenes. |
| `expiration` | `36000000` | Duración predeterminada de la caché del cliente. Proporciona un intervalo de caducidad predeterminado en el caso de que el valor de catálogo::Expiration no sea válido en un registro de catálogo determinado.<br>Número real, 0 o superior. Número de milisegundos hasta la caducidad desde que se generaron los datos de respuesta. Si se establece en 0, la imagen de respuesta siempre caducará inmediatamente, lo que deshabilita el almacenamiento en caché del cliente. De forma predeterminada, este valor se establece en 10 horas, lo que significa que si se publica una imagen nueva, la imagen antigua tarda 10 horas en abandonar la caché del usuario. Póngase en contacto con Asistencia al cliente si necesita borrar la caché antes.<br>Consulte también [Caducidad](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) en la API del servicio de imágenes. |
| `jpegquality` | `80` | Atributos de codificación de JPEG predeterminados. Especifica los atributos predeterminados para las imágenes de respuesta del JPEG.<br>Número entero e indicador, separados por coma. El primer valor está en el rango 1.. 100 y define la calidad. El segundo valor puede ser 0 para el comportamiento normal o 1 para desactivar la disminución de resolución de cromaticidad RGB empleada por los codificadores JPEG.<br>Consulte también [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html#image-serving-api) en la API del servicio de imágenes. |
| `maxpix` | `2000,2000` | Límite de tamaño de imagen de respuesta. Anchura y altura máximas para la imagen de respuesta que se devuelve al cliente.<br>El servidor devuelve un error si una solicitud genera una imagen de respuesta cuya anchura o altura sea mayor que el atributo::MaxPix.<br>Consulte también [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html#image-serving-api) en la API del servicio de imágenes. |
| `resmode` | `SHARP2` | Modo de remuestreo predeterminado. Especifica los atributos predeterminados de remuestreo e interpolación que se utilizarán para escalar los datos de imagen.<br>Se utiliza cuando `resMode=` no se ha especificado en una solicitud.<br>Los valores permitidos incluyen `BILIN`, `BICUB`, o `SHARP2`.<br>Enumeración. Establezca en 2 para `bilin`, 3 para `bicub`, o 4 para `sharp2` modo de interpolación. Uso `sharp2` para obtener los mejores resultados.<br>Consulte también [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html#image-serving-api) en la API del servicio de imágenes. |
| `resolution` | `72` | Resolución de objeto predeterminada. Proporciona una resolución de objeto predeterminada en el caso de que el valor de catálogo::Resolution no sea válido en un registro de catálogo determinado.<br>Número real, mayor que 0. Normalmente se expresa como píxeles por pulgada, pero también puede expresarse en otras unidades, como píxeles por metro.<br>Consulte también [Resolución](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-resolution.html#image-serving-api) en la API del servicio de imágenes. |
| `thumbnailtime` | `1%,11%,21%,31%,41%,51%,61%,71%,81%,91%` | Estos valores representan una instantánea del tiempo de reproducción del vídeo y se pasan a [encoding.com](https://www.encoding.com/). Consulte [Acerca de la miniatura de vídeo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-hybrid-mode) para obtener más información. |

## Configuración de la gestión de color Dynamic Media {#configuring-dynamic-media-color-management}

La administración de color de Dynamic Media le permite corregir el color de los recursos para previsualizarlos.

Con la corrección de color, los recursos ingeridos conservan su espacio de color (RGB, CMYK, gris) y el perfil de color incrustado en la representación de TIFF piramidal generada. Cuando se solicita una representación dinámica, el color de la imagen se corrige en el espacio de color de destino. Puede configurar el perfil de color de salida en la configuración de publicación de Dynamic Media en el JCR.

La gestión del color de Adobe utiliza perfiles ICC (International Color Consortium), un formato definido por ICC.

Puede configurar la gestión de color de Dynamic Media y los ajustes preestablecidos de imagen mediante CMYK, RGB o salida gris. Consulte [Configurar ajustes preestablecidos de imagen](/help/assets/managing-image-presets.md).

Los casos de uso avanzados podrían utilizar una configuración manual `icc=` para seleccionar explícitamente un perfil de color de salida:

* `icc` - [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html)

* `iccEmbed` - [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html)

>[!NOTE]
>
El conjunto estándar de perfiles de color del Adobe solo está disponible si tiene [Paquete de funciones 12445 desde Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-12445) instalado. Todos los paquetes de funciones y paquetes de servicio están disponibles en [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html). Feature Pack 12445 proporciona los perfiles de color del Adobe.


### Instalación del paquete de funciones 12445 {#installing-feature-pack}

Para utilizar las funcionalidades de administración de color de Dynamic Media, instale el paquete de funciones 12445.

**Para instalar el paquete de funciones 12445:**

1. Vaya a [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html) y descargue `cq-6.3.0-featurepack-12445`.

   Consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md) para obtener más información sobre el uso de paquetes en [!DNL Adobe Experience Manager].

1. Instale el paquete de funciones.

### Configuración de los perfiles de color predeterminados {#configuring-the-default-color-profiles}

Después de instalar el paquete de funciones, configure los perfiles de color predeterminados adecuados para habilitar la corrección de color al solicitar datos de imagen CMYK o de RGB.

**Para configurar los perfiles de color predeterminados:**

1. Entrada **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**, vaya a `/conf/global/settings/dam/dm/imageserver/jcr:content` que contiene los perfiles de Adobe Color predeterminados.

   ![chlimage_1-514](assets/chlimage_1-514.png)

1. Añada una propiedad de corrección de color desplazándose hasta la parte inferior de la **[!UICONTROL Propiedades]** pestaña. Introduzca manualmente el nombre, el tipo y el valor de la propiedad, que se describe en las tablas siguientes. Después de introducir los valores, seleccione **[!UICONTROL Añadir]** y luego **[!UICONTROL Guardar todo]** para guardar los valores.

   Las propiedades de corrección de color se describen en la **Propiedades de correcciones de color** tabla. Los valores que puede asignar a las propiedades de corrección de color se encuentran en la variable **Perfil de color** tabla.

   Por ejemplo, en **[!UICONTROL Nombre]**, agregue `iccprofilecmyk`, seleccione **[!UICONTROL Tipo]** `String`y agregue. `WebCoated` as a **[!UICONTROL Valor]**. A continuación seleccione **[!UICONTROL Añadir]** y luego **[!UICONTROL Guardar todo]** para guardar los valores.

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
   <td>Nombre del perfil de color de RGB predeterminado.</td>
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
   <td>Nombre del perfil de color predeterminado del RGB utilizado para las imágenes del RGB que no tienen un perfil de color incrustado</td>
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
   <td>Especifica si la compensación del punto negro se realiza durante la corrección de color. El Adobe recomienda que esta configuración esté activada.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccdither.html">icoditera</a></td>
   <td>Booleano</td>
   <td>False</td>
   <td>Especifica si el tramado se realiza durante la corrección de color.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html">iccrenderIntent</a></td>
   <td>Cadena</td>
   <td>relativo</td>
   <td><p>Especifica la intención de procesamiento. Los valores aceptables son: <strong>perceptual, relativo, saturación, absoluto. </strong><i></i>Adobe recomienda <strong>relativo </strong><i></i>como valor predeterminado.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
Los nombres de propiedad distinguen entre mayúsculas y minúsculas y deben estar en minúscula.

**Tabla de perfil de color**

Se instalan los siguientes perfiles de color:

<table>
 <tbody>
  <tr>
   <th><p>Nombre</p> </th>
   <th><p>Ritmo de colores</p> </th>
   <th><p>Descripción</p> </th>
  </tr>
  <tr>
   <td>Adobe RGB</td>
   <td>RGB</td>
   <td>Adobe RGB (1998)</td>
  </tr>
  <tr>
   <td>AppleRGB</td>
   <td>RGB</td>
   <td>RGB de Apple</td>
  </tr>
  <tr>
   <td>CIERGB</td>
   <td>RGB</td>
   <td>RGB CIE</td>
  </tr>
  <tr>
   <td>CoatedFogra27</td>
   <td>CMYK</td>
   <td>FOGRA27 recubierto (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedFogra39</td>
   <td>CMYK</td>
   <td>FOGRA39 recubierto (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedGraCol</td>
   <td>CMYK</td>
   <td>Revestido GRACoL 2006 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>ColorMatchRGB</td>
   <td>RGB</td>
   <td>RGB ColorMatch</td>
  </tr>
  <tr>
   <td>EuropeISOCoated</td>
   <td>CMYK</td>
   <td>Europa ISO Coated FOGRA27</td>
  </tr>
  <tr>
   <td>EuroscaleCoated</td>
   <td>CMYK</td>
   <td>Euro scale Coated v2</td>
  </tr>
  <tr>
   <td>EuroscaleUncovered</td>
   <td>CMYK</td>
   <td>Escala de euro sin recubrir v2</td>
  </tr>
  <tr>
   <td>JapanColorCoated</td>
   <td>CMYK</td>
   <td>Japón Color 2001 Revestido</td>
  </tr>
  <tr>
   <td>JapanColorNewspaper</td>
   <td>CMYK</td>
   <td>Japón Color 2002 Periódico</td>
  </tr>
  <tr>
   <td>JapanColorUncovered</td>
   <td>CMYK</td>
   <td>Japón Color 2001 Sin recubrimiento</td>
  </tr>
  <tr>
   <td>JapanColorWebCoated</td>
   <td>CMYK</td>
   <td>Japón Color 2003 Web Coated</td>
  </tr>
  <tr>
   <td>JapanWebCoated</td>
   <td>CMYK</td>
   <td>Japón Web Coated (Ad)</td>
  </tr>
  <tr>
   <td>NewsprintSNAP2007</td>
   <td>CMYK</td>
   <td>Boletín de Estados Unidos (SNAP 2007)</td>
  </tr>
  <tr>
   <td>NTSC</td>
   <td>RGB</td>
   <td>NTSC (1953)</td>
  </tr>
  <tr>
   <td>AMIGO</td>
   <td>RGB</td>
   <td>PAL/SECAM</td>
  </tr>
  <tr>
   <td>ProPhoto</td>
   <td>RGB</td>
   <td>RGB ProPhoto</td>
  </tr>
  <tr>
   <td>PS4Predeterminado</td>
   <td>CMYK</td>
   <td>CMYK predeterminado de Photoshop 4</td>
  </tr>
  <tr>
   <td>PS5Default</td>
   <td>CMYK</td>
   <td>CMYK predeterminado de Photoshop 5</td>
  </tr>
  <tr>
   <td>Revestido Con Hojas</td>
   <td>CMYK</td>
   <td>U.S. Sheetfed Coated v2</td>
  </tr>
  <tr>
   <td>Con hojasSin recubrir</td>
   <td>CMYK</td>
   <td>U.S. Sheetfed Uncovered v2</td>
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
   <td>Fogra29 sin recubrimiento</td>
   <td>CMYK</td>
   <td>FOGRA29 sin recubrimiento (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoated</td>
   <td>CMYK</td>
   <td>U.S. Web Coated (SWOP) v2</td>
  </tr>
  <tr>
   <td>WebCoatedFogra28</td>
   <td>CMYK</td>
   <td>Revestimiento Web FOGRA28 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoatedGrade3</td>
   <td>CMYK</td>
   <td>Papel SWOP 2006 Grado 3 Revestido por Web</td>
  </tr>
  <tr>
   <td>WebCoatedGrade5</td>
   <td>CMYK</td>
   <td>Papel SWOP 2006 Grado 5 Revestido por Web</td>
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

1. Seleccionar **[!UICONTROL Guardar todo]**.

Por ejemplo, puede establecer la variable **[!UICONTROL iccprofilergb]** hasta `sRGB`, y **[!UICONTROL iccprofilecmyk]** hasta **[!UICONTROL WebCoated]**.

Al hacerlo, se haría lo siguiente:

* Activa la corrección de color para imágenes RGB y CMYK.
* Se supone que las imágenes de RGB que no tienen un perfil de color están en la *sRGB* espacio de color.
* Se supone que las imágenes CMYK que no tienen un perfil de color están en *WebCoated* espacio de color.
* Representaciones dinámicas que devuelven la salida del RGB, devuélvala en el espacio de color *sRGB.
* Representaciones dinámicas que devuelven salida CMYK, devuélvala en el *WebCoated* espacio de color.

## Entrega de recursos {#delivering-assets}

Una vez completadas todas las tareas anteriores, los recursos activados de Dynamic Media se proporcionan desde el servicio de imagen o vídeo. En Experience Manager, esta capacidad se muestra en un **[!UICONTROL Copiar URL de imagen]**, **[!UICONTROL Copiar URL del visor]**, **[!UICONTROL Incrustar código de visor]** y en el WCM.

Consulte [Entrega de recursos de Dynamic Media](/help/assets/delivering-dynamic-media-assets.md).

<table>
 <tbody>
  <tr>
   <td><strong>Cuando...</strong></td>
   <td><strong>Resultado</strong></td>
  </tr>
  <tr>
   <td>Copiar una URL de imagen</td>
   <td><p>El cuadro de diálogo Copiar URL muestra una URL similar a la siguiente (la URL solo es para fines de demostración):</p> <p><code>https://IMAGESERVICEPUBLISHNODE/is/image/content/dam/path/to/Image.jpg?$preset$</code></p> <p>Donde <code>IMAGESERVICEPUBLISHNODE</code> hace referencia a la URL del servicio de imágenes.</p> <p>Consulte también <a href="/help/assets/delivering-dynamic-media-assets.md">Entrega de recursos de Dynamic Media</a>.</p> </td>
  </tr>
  <tr>
   <td>Copiar una URL de visor</td>
   <td><p>El cuadro de diálogo Copiar URL muestra una URL similar a la siguiente (la URL solo es para fines de demostración):</p> <p><code>https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/BasicZoomViewer.html?asset=/content/dam/path/to/Image.jpg&amp;config=/conf/global/settings/dam/dm/presets/viewer/Zoom_dark&amp;serverUrl=https://IMAGESERVICEPUBLISHNODE/is/image/&amp;contentRoot=%2F</code></p> <p>Donde <code>PUBLISHNODE</code> hace referencia al nodo de publicación normal del Experience Manager y <code>IMAGESERVICEPUBLISHNODE</code> hace referencia a la URL del servicio de imágenes.</p> <p>Consulte también <a href="/help/assets/delivering-dynamic-media-assets.md">Entrega de recursos de Dynamic Media</a>.</p> </td>
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
       &lt;/script&gt;</code></p> <p>Donde <code>PUBLISHNODE</code> hace referencia al nodo de publicación normal del Experience Manager y <code>IMAGESERVICEPUBLISHNODE</code> hace referencia a la URL del servicio de imágenes.</p> <p>Consulte también <a href="/help/assets/delivering-dynamic-media-assets.md">Entrega de recursos de Dynamic Media</a>.</p> </td>
  </tr>
 </tbody>
</table>

### WCM Dynamic Media y componentes de medios interactivos {#wcm-dynamic-media-and-interactive-media-components}

Las páginas de WCM que hacen referencia a componentes de Dynamic Media y medios interactivos hacen referencia al servicio de envío.
