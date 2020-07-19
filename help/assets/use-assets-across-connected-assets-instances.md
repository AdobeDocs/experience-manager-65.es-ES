---
title: Use Connected Assets to share DAM assets in [!DNL Adobe Experience Manager Sites] authoring workflow.
description: Utilice los recursos disponibles en una [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] implementación remota.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 28c55333e0eebb68ada46ee89785f5f6475abf9e
workflow-type: tm+mt
source-wordcount: '2105'
ht-degree: 44%

---


# Utilice los recursos conectados para compartir recursos de DAM en [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

En las grandes empresas se puede distribuir la infraestructura necesaria para crear sitios web. A veces, las capacidades de creación de sitios web y los recursos digitales utilizados para crear estos sitios web se pueden encontrar en diferentes implementaciones. Una razón puede ser la distribución geográfica de las implementaciones existentes que se requieren para trabajar en conjunto. Otra razón pueden ser las adquisiciones que conducen a una infraestructura heterogénea que la compañía principal desea utilizar en conjunto.

Los usuarios pueden crear páginas web en [!DNL Experience Manager Sites]. [!DNL Experience Manager Assets] es el sistema de administración de recursos digitales (DAM) que proporciona los recursos necesarios para los sitios web. [!DNL Experience Manager] ahora admite el caso de uso anterior mediante la integración [!DNL Sites] y [!DNL Assets].

## Información general sobre los recursos conectados {#overview-of-connected-assets}

When editing pages in [!UICONTROL Page Editor], the authors can seamlessly search, browse, and embed assets from a different [!DNL Assets] deployment. Los administradores crean una integración única de una implementación de [!DNL Sites] con otra implementación (remota) de [!DNL Assets].

For the [!DNL Sites] authors, the remote assets are available as read-only local assets. La función admite la búsqueda y el uso ininterrumpidos de algunos recursos remotos a la vez. To make many remote assets available on a [!DNL Sites] deployment in one-go, consider migrating the assets in bulk. Consulte la guía [de migración de recursos de](/help/assets/assets-migration-guide.md)Experience Manager.

### Requisitos previos e implementaciones admitidas {#prerequisites}

Antes de usar o configurar esta capacidad, asegúrese de lo siguiente:

* Los usuarios forman parte de los grupos de usuarios correspondientes en cada implementación.
* For [!DNL Adobe Experience Manager] deployment types, one of the supported criteria is met. [!DNL Experience Manager] 6.5 [!DNL Assets] funciona [!DNL Experience Manager] como Cloud Service. Para obtener más información, consulte Funcionalidad de Recursos [conectados en Experience Manager como Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Sites] como Cloud Service | [!DNL Experience Manager] 6.5 [!DNL Sites] sobre AMS | [!DNL Experience Manager] 6.5 [!DNL Sites] in situ |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]como Cloud Service ** | Compatible | Compatible | Compatible |
   | **[!DNL Experience Manager]6.5[!DNL Assets]sobre AMS ** | Compatible | Compatible | Compatible |
   | **[!DNL Experience Manager]6.5[!DNL Assets]in situ ** | No compatible | No compatible | No compatible |

### Formatos de archivo compatibles {#mimetypes}

Los autores buscan imágenes y los siguientes tipos de documentos en el Buscador de contenido y utilizan los recursos buscados en el Editor de páginas. Se añaden Documentos al `Download` componente y a las imágenes al `Image` componente. Authors also add the remote assets in any custom [!DNL Experience Manager] component that extends the default `Download` or `Image` components. Los formatos admitidos son:

* **Formatos** de imagen: Formatos que admite el componente [](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/components/image.html) Imagen. [!DNL Dynamic Media] las imágenes no son compatibles.
* **Formatos** de Documento: Consulte los formatos [de documento](assets-formats.md#supported-document-formats)admitidos.

### Usuarios y grupos implicados {#users-and-groups-involved}

A continuación se describen las distintas funciones que se usan para configurar y utilizar la capacidad y sus grupos de usuarios correspondientes. El ámbito local se utiliza para el caso de uso en el que un autor crea una página web. El ámbito remoto se utiliza para la implementación de DAM que aloja los recursos necesarios. The [!DNL Sites] author fetches these remote assets.

| Función | Ámbito | Grupo de usuarios | Nombre de usuario en la introducción | Requisito |
|---|---|---|---|---|
| [!DNL Sites] administrador | Local | [!DNL Experience Manager] `administrators` | `admin` | Set up [!DNL Experience Manager] and configure integration with the remote [!DNL Assets] deployment. |
| Usuario DAM | Local | `Authors` | `ksaner` | Se utiliza para ver y duplicar los recursos recuperados en `/content/DAM/connectedassets/`. |
| [!DNL Sites] author | Local | `Authors` (con acceso de lectura en el DAM remoto y acceso de autor en local [!DNL Sites]) | `ksaner` | End user are [!DNL Sites] authors who use this integration to improve their content velocity. The authors search and browse assets in remote DAM using [!UICONTROL Content Finder] and using the required images in local web pages. Se utilizan las credenciales del usuario de DAM `ksaner`. |
| [!DNL Assets] administrador | Remoto | [!DNL Experience Manager] `administrators` | `admin` en remoto [!DNL Experience Manager] | Configurar el intercambio de recursos de origen cruzado (CORS). |
| Usuario DAM | Remoto | `Authors` | `ksaner` en remoto [!DNL Experience Manager] | Author role on the remote [!DNL Experience Manager] deployment. Search and browse assets in Connected Assets using the [!UICONTROL Content Finder]. |
| Distribuidor DAM (usuario técnico) | Remoto | [!DNL Sites] `Authors` | `ksaner` en remoto [!DNL Experience Manager] | This user present on the remote deployment is used by [!DNL Experience Manager] local server (not the [!DNL Sites] author role) to fetch the remote assets, on behalf of [!DNL Sites] author. Esta función no es la misma que las dos funciones `ksaner` anteriores y pertenece a un grupo de usuarios diferente. |

## Configure a connection between [!DNL Sites] and [!DNL Assets] deployments {#configure-a-connection-between-sites-and-assets-deployments}

An [!DNL Experience Manager] administrator can create this integration. Una vez creados, los permisos necesarios para utilizarlos se establecen mediante grupos de usuarios. Los grupos de usuarios se definen en la implementación y en la implementación de DAM [!DNL Sites] .

To configure Connected Assets and local [!DNL Sites] connectivity, follow these steps:

1. Access an existing [!DNL Sites] deployment or create a deployment using the following command:

   1. In the folder of the JAR file, execute the following command on a terminal to create each [!DNL Experience Manager] server.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. After a few minutes, the [!DNL Experience Manager] server starts successfully. Consider this [!DNL Sites] deployment as the local machine for web page authoring, say at `https://[local_sites]:4502`.

1. Ensure that the users and roles with local scope exist on the [!DNL Sites] deployment and on the [!DNL Assets] deployment on AMS. Create a technical user on [!DNL Assets] deployment and add to the user group mentioned in [users and groups involved](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Access the local [!DNL Sites] deployment at `https://[local_sites]:4502`. Haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Configuración de recursos conectados]** y proporcione los siguientes valores:

   1. [!DNL Assets] la ubicación es `https://[assets_servername_ams]:[port]`.
   1. Credenciales de un distribuidor DAM (usuario técnico).
   1. In the **[!UICONTROL Mount Point]** field, enter the local [!DNL Experience Manager] path where [!DNL Experience Manager] fetches the assets. Por ejemplo, la carpeta `remoteassets`.
   1. Ajuste los valores del **[!UICONTROL umbral de optimización de transferencia binaria original]** en función de la red. Las representaciones de recursos superiores a este umbral se transfieren de forma asíncrona.
   1. Seleccione **[!UICONTROL almacén de datos compartido con recursos conectados]**, si utiliza un almacén de datos para almacenar los recursos y este es el almacenamiento común entre ambas implementaciones de En este caso, el límite de umbral no importa, ya que los binarios de activos reales se encuentran en el almacén de datos y no se transfieren.

   ![Una configuración típica para los recursos conectados](assets/connected-assets-typical-config.png)

   *Figura: Una configuración típica para los recursos conectados.*

1. Dado que los recursos ya se han procesado y se han recuperado las representaciones, deshabilite los iniciadores del flujo de trabajo. Adjust the launcher configurations on the local ([!DNL Sites]) deployment to exclude the `connectedassets` folder, in which the remote assets are fetched.

   1. On [!DNL Sites] deployment, click **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Launchers]**.

   1. Busque iniciadores con flujos de trabajo como **[!UICONTROL Recurso de actualización DAM]** y **[!UICONTROL Reescritura de metadatos DAM]**.

   1. Seleccione el lanzador del flujo de trabajo y haga clic en **[!UICONTROL Propiedades]** en la barra de acciones.

   1. In the [!UICONTROL Properties] wizard, change the **[!UICONTROL Path]** fields as the following mappings to update their regular expressions to exclude the mount point **[!UICONTROL connectedassets]**.

   | Antes | Después |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Todas las representaciones disponibles en la implementación remota de se recuperan cuando los autores recuperan un recurso. Si desea crear más representaciones de un recurso recuperado, omita este paso de configuración. The [!UICONTROL DAM Update Asset] workflow gets triggered and creates more renditions. These renditions are available only on the local [!DNL Sites] deployment and not on the remote DAM deployment.

1. Add the [!DNL Sites] deployment as one of the **[!UICONTROL Allowed Origins]** on the remote [!DNL Assets'] CORS configuration.

   1. Inicie sesión con las credenciales del administrador. Buscar `Cross-Origin`. Acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.

   1. To create a CORS configuration for [!DNL Sites] deployment, click add option ![Assets add icon](assets/do-not-localize/assets_add_icon.png) next to **[!UICONTROL Adobe Granite Cross-Origin Resource Sharing Policy]**.

   1. In the field **[!UICONTROL Allowed Origins]**, input the URL of the local [!DNL Sites], that is, `https://[local_sites]:[port]`. Guarde la configuración.

## Usar recursos remotos {#use-remote-assets}

Los creadores del sitio web utilizan Content Finder para conectarse a la implementación de DAM. Los autores pueden examinar, buscar y arrastrar los recursos remotos de un componente. Para autenticarse en el DAM remoto, conserve las credenciales del usuario DAM proporcionadas por el administrador.

Los autores pueden utilizar los recursos disponibles en el DAM local y en la implementación remota de DAM, en una sola página web. Utilice el buscador de contenido para decidir si buscar en el DAM local o en el DAM remoto.

Solo se buscan las etiquetas de los recursos remotos que tienen una etiqueta correspondiente exacta junto con la misma jerarquía de taxonomía, disponible en la [!DNL Sites] implementación local. Todas las demás etiquetas se descartan. Authors can search for remote assets using all the tags present on the remote [!DNL Experience Manager] deployment, as it offers a full-text search.

### Introducción al uso {#walk-through-of-usage}

Utilice la configuración anterior para probar la experiencia de creación y comprender cómo se utiliza la funcionalidad. Utilice documentos o imágenes de su elección en la implementación remota de DAM.

1. Navigate to the [!DNL Assets] interface on the remote deployment by accessing **[!UICONTROL Assets]** > **[!UICONTROL Files]** from [!DNL Experience Manager] workspace. También puede acceder a `https://[assets_servername_ams]:[port]/assets.html/content/dam` en un explorador. Cargue los recursos que desee.
1. On the [!DNL Sites] deployment, in the profile activator in the upper-right corner, click **[!UICONTROL Impersonate as]**. Utilice `ksaner` como nombre de usuario, seleccione la opción proporcionada y haga clic en **[!UICONTROL Aceptar]**.
1. Abra una página web de We.Retail en **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Edite la página. También puede acceder a `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` en un navegador para editar una página.

   Haga clic en **[!UICONTROL Alternar panel lateral]** en la esquina superior izquierda de la página.

1. Open the [!UICONTROL Assets] tab and click **[!UICONTROL Log in to Connected Assets]**.
1. Proporcione las credenciales (`ksaner` como nombre de usuario y `password` como contraseña). This user has authoring permissions on both the [!DNL Experience Manager] deployments.
1. Busque el recurso que agregó a DAM. Los recursos remotos se muestran en el panel izquierdo. Filtre por imágenes o documentos y por tipos de documentos compatibles. Arrastre las imágenes a un componente `Image` y los documentos a un componente `Download`.

   The fetched assets are read-only on the local [!DNL Sites] deployment. You can still use the options provided by your [!DNL Sites] components to edit the fetched asset. La edición por componentes no es destructiva.

   ![Opciones para filtrar tipos de documentos e imágenes al buscar recursos en DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: Opciones para filtrar tipos de documentos e imágenes al buscar recursos en DAM remoto.*

1. Se notifica al creador del sitio si se busca un recurso de forma asincrónica y si falla alguna tarea de recuperación. Durante la creación o incluso después de esta, los autores pueden ver información detallada sobre las tareas de recuperación y los errores en la interfaz de usuario de [trabajos asincrónicos](/help/sites-administering/asynchronous-jobs.md).

   ![Notificación sobre la captura asincrónica de recursos que se produce en segundo plano.](assets/assets_async_transfer_fails.png)

   *Figura: Notificación sobre la captura asincrónica de recursos que se produce en segundo plano.*

1. When publishing a page, [!DNL Experience Manager] displays a complete list of assets that are used on the page. Asegúrese de que los recursos remotos se recuperan correctamente en el momento de la publicación. Para comprobar el estado de cada recurso recuperado, consulte la interfaz de usuario de [trabajos asincrónicos](/help/sites-administering/asynchronous-jobs.md) .

   >[!NOTE]
   >
   >Aunque no se recuperen uno o varios recursos remotos, la página se publicará. El componente que utiliza el recurso remoto se publica en blanco. The [!DNL Experience Manager] notification area displays a notification for errors that show in async jobs page.

>[!CAUTION]
>
>Una vez utilizados en una página web, los recursos remotos recuperados pueden ser buscados y utilizados por cualquier persona que tenga permiso para acceder a la carpeta local. Los recursos recuperados se almacenan en la carpeta local (`connectedassets` en la ruta anterior). Los recursos también se pueden buscar y ver en el repositorio local mediante [!UICONTROL Buscador de contenido].

Los recursos recuperados se pueden usar como cualquier otro recurso local, pero los metadatos asociados no se pueden editar.

## Restricciones          {#limitations}

### Permisos y administración de recursos {#permissions-and-managing-assets}

* Los recursos locales no se sincronizan con los recursos originales en la implementación remota. Las ediciones, eliminaciones o revocaciones de permisos en la implementación de DAM no se propagan de forma descendente.
* Los recursos locales son copias de solo lectura. [!DNL Experience Manager]Los componentes de realizan ediciones no destructivas en los recursos. No se permiten otras ediciones.
* Los recursos recuperados localmente solo están disponibles para la creación. Los flujos de trabajo de actualización de recursos no se pueden aplicar y los metadatos no se pueden editar.
* Solo se admiten las imágenes y los formatos de documento enumerados. [!DNL Dynamic Media]Los recursos de , los fragmentos de contenido y los fragmentos de experiencia no son admitidos.
* No se recuperan los esquemas de metadatos.
* Todos los [!DNL Sites] autores tienen permisos de lectura en las copias recuperadas, incluso si los autores no pueden acceder a la implementación de DAM remota.
* No se admiten las API para personalizar la integración.
* La funcionalidad admite la búsqueda y el uso ininterrumpidos de recursos remotos. Para que varios recursos remotos estén disponibles en la implementación local, considere migrar los recursos. Consulte [Guía de migración de recursos](assets-migration-guide.md).
* No es posible utilizar un recurso remoto como miniatura de página en la interfaz de usuario Propiedades [!UICONTROL de la] página. Puede establecer una miniatura de una página web en la interfaz de usuario Propiedades [!UICONTROL de] página desde la [!UICONTROL miniatura] haciendo clic en [!UICONTROL Seleccionar imagen].

### Configuración y licencia {#setup-licensing}

* [!DNL Assets] la implementación en [!DNL Adobe Managed Services] es compatible.
* [!DNL Sites] Puede conectarse a un único [!DNL Assets] repositorio a la vez.
* A license of [!DNL Assets] working as remote repository.
* One or more licenses of [!DNL Sites] working as local authoring deployment.

### Uso {#usage}

* Los usuarios pueden buscar recursos remotos y arrastrarlos a la página local durante la creación. No se admite ninguna otra funcionalidad.
* La operación de recuperación expira al cabo de 5 segundos. Los autores pueden tener problemas para recuperar recursos, por ejemplo, si hay problemas de red. Authors can reattempt by dragging the remote asset from [!UICONTROL Content Finder] to [!UICONTROL Page Editor].
* Las ediciones simples que no son destructivas y que se admiten mediante el componente `Image`, se pueden realizar en los recursos recuperados. Los recursos son de solo lectura.
* El único método para recuperar el recurso es arrastrarlo a una página. No hay soporte API ni otros métodos para recuperar un recurso para actualizarlo.

## Solución de problemas {#troubleshoot}

Para solucionar problemas del escenario de error común, siga estos pasos:

* If you cannot search for remote assets from the [!UICONTROL Content Finder], then ensure that the required roles and permissions are in place.
* Es posible que un recurso recuperado de la presa remota no se publique en una página web por una o varias razones. No existe en el servidor remoto, la falta de los permisos adecuados para recuperarlo o la falla de red pueden ser las razones. Asegúrese de que el recurso no se elimina del DAM remoto. Asegúrese de que se han establecido los permisos adecuados y de que se cumplen los requisitos previos. Vuelva a intentar agregar el recurso a la página y vuelva a publicarlo. Compruebe la [lista de trabajos asincrónicos](/help/sites-administering/asynchronous-jobs.md) si hay errores en la recuperación de recursos.
