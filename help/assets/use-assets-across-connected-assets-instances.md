---
title: Utilice Recursos conectados para compartir recursos DAM en el flujo de trabajo de creación de [!DNL Adobe Experience Manager Sites].
description: Utilice los recursos disponibles en una implementación remota de [!DNL Adobe Experience Manager Assets] al crear sus páginas web en otra implementación de sitio de Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 2cdcea028814b40fb178e63f583939df27a46cad

---


# Utilice los recursos conectados para compartir recursos de DAM en [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

En las grandes empresas se puede distribuir la infraestructura necesaria para crear sitios web. A veces, las capacidades de creación de sitios web y los recursos digitales utilizados para crear estos sitios web se pueden encontrar en diferentes implementaciones. Algunas razones pueden ser la distribución geográfica de implementaciones existentes que se requieren para trabajar en conjunto, o las adquisiciones que conducen a una infraestructura heterogénea que la compañía principal desea utilizar en conjunto.

[!DNL Adobe Experience Manager Sites] ofrece capacidades de crear páginas web y es el sistema de gestión de recursos digitales (DAM) que proporciona los recursos necesarios para los sitios web.[!DNL Adobe Experience Manager Assets] [!DNL Experience Manager] ahora admite el caso de uso anterior mediante la integración [!DNL Experience Manager Sites] y [!DNL Experience Manager Assets].

## Información general sobre los recursos conectados {#overview-of-connected-assets}

When editing pages in Page Editor, the authors can seamlessly search, browse, and embed assets from a different [!DNL Experience Manager Assets] deployment. To do an [!DNL Experience Manager] administrator do a one-time integration of a local deployment of [!DNL Experience Manager Sites] with a different (remote) deployment of [!DNL Experience Manager Assets].

For the [!DNL Sites] authors, the remote assets are available as read-only local assets. La funcionalidad admite la búsqueda y el uso ininterrumpidos de algunos recursos remotos a la vez. Para que varios recursos remotos estén disponibles en la implementación local en un solo uso, considere migrar los recursos de forma masiva. Consulte la guía [de migración de recursos de Experience Manager](/help/assets/assets-migration-guide.md).

### Requisitos previos e implementaciones admitidas {#prerequisites}

Antes de usar o configurar esta capacidad, asegúrese de lo siguiente:

* Los usuarios forman parte de los grupos correspondientes en cada implementación.
* Para los tipos de implementación de Adobe Experience Manager, se cumple uno de los criterios admitidos. [!DNL Experience Manager] 6.5 [!DNL Assets] funciona [!DNL Experience Manager] como un servicio de nube. Para obtener más información, consulte la funcionalidad Recursos [conectados en Experience Manager como un servicio](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)de nube.

   |  | [!DNL Experience Manager Sites] como servicio de nube | Experience Manager 6.5 [!DNL Sites] en AMS | Experience Manager 6.5 [!DNL Sites] in situ |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]como servicio de nube ** | Compatible | Compatible | Compatible |
   | **Experience Manager 6.5[!DNL Assets]en AMS** | Compatible | Compatible | Compatible |
   | **Experience Manager 6.5[!DNL Assets]in situ** | No compatible | No compatible | No compatible |

### Formatos de archivo compatibles {#mimetypes}

Los creadores pueden buscar imágenes y los siguientes tipos de documentos en el buscador de contenido y utilizar los recursos buscados en el editor de páginas. Se pueden agregar documentos al `Download` componente y se pueden agregar imágenes al `Image` componente. Authors can also add the remote assets in any custom Experience Manager component that extends the default `Download` or `Image` components. La lista de los formatos admitidos es:

* **Formatos** de imagen: Recursos conectados admiten los formatos de imagen admitidos por el componente [](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/components/image.html) Imagen. [!DNL Dynamic Media] las imágenes no son compatibles.
* **Formatos de documento**: Consulte [Formatos de documento compatibles con recursos conectados](assets-formats.md#supported-document-formats).

### Usuarios y grupos implicados {#users-and-groups-involved}

A continuación se describen las distintas funciones que se usan para configurar y utilizar la capacidad y sus grupos de usuarios correspondientes. El ámbito local se utiliza para el caso de uso en el que un autor crea una página web. El ámbito remoto se utiliza para la implementación de DAM que aloja los recursos necesarios. The [!DNL Sites] author fetches these remote assets.

| Función | Ámbito | Grupo de usuarios | Nombre de usuario en la introducción | Requisito |
|---|---|---|---|---|
| [!DNL Sites] administrador | Local | Experience Manager `administrators` | `admin` | Configure Experience Manager y configure la integración con la implementación remota [!DNL Assets] . |
| Usuario DAM | Local | `Authors` | `ksaner` | Se utiliza para ver y duplicar los recursos recuperados en `/content/DAM/connectedassets/`. |
| [!DNL Sites] author | Local | `Authors` (con acceso de lectura en el DAM remoto y acceso de autor en local [!DNL Sites]) | `ksaner` | End user are [!DNL Sites] authors who use this integration to improve their content velocity. Los autores buscan y exploran recursos en el DAM remoto mediante el buscador de contenido y utilizando las imágenes necesarias en las páginas web locales. Se utilizan las credenciales del usuario de DAM `ksaner`. |
| [!DNL Assets] administrador | Remoto | Experience Manager `administrators` | `admin` en Experience Manager remoto | Configurar el intercambio de recursos de origen cruzado (CORS). |
| Usuario DAM | Remoto | `Authors` | `ksaner` en Experience Manager remoto | Función de autor en la implementación remota de Experience Manager. Buscar y examinar recursos en recursos conectados con el buscador de contenido. |
| Distribuidor DAM (usuario técnico) | Remoto | `Authors` | `ksaner` en Experience Manager remoto | This user present on the remote deployment is used by Experience Manager local server (not the Site author role) to fetch the remote assets, on behalf of [!DNL Sites] author. Esta función no es la misma que las dos funciones `ksaner` anteriores y pertenece a un grupo de usuarios diferente. |

## Configure a connection between [!DNL Sites] and [!DNL Assets] deployments {#configure-a-connection-between-sites-and-assets-deployments}

Un administrador de Experience Manager puede crear esta integración. Once created, the permissions required to use it are established via user groups that are defined on the [!DNL Sites] deployment and on the DAM deployment.

To configure Connected Assets and local [!DNL Sites] connectivity, follow these steps.

1. Access an existing [!DNL Experience Manager Sites] deployment or create a deployment using the following command:

   1. En la carpeta del archivo JAR, ejecute el siguiente comando en un terminal para crear cada servidor de Experience Manager.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Tras unos minutos, el servidor de Experience Manager inicio correctamente. Consider this [!DNL Experience Manager Sites] deployment as the local machine for web page authoring, say at `https://[local_sites]:4502`.

1. Ensure that the users and roles with local scope exist on the Experience Manager Sites deployment and on the [!DNL Experience Manager Assets] deployment on AMS. Create a technical user on [!DNL Assets] deployment and add to the user group mentioned in [users and groups involved](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Access the local [!DNL Experience Manager Sites] deployment at `https://[local_sites]:4502`. Haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Configuración de recursos conectados]** y proporcione los siguientes valores:

   1. [!DNL Experience Manager Assets] la ubicación es `https://[assets_servername_ams]:[port]`.
   1. Credenciales de un distribuidor DAM (usuario técnico).
   1. In **[!UICONTROL Mount Point]** field, enter the local Experience Manager path where Experience Manager fetches the assets. Por ejemplo, la carpeta `remoteassets`.
   1. Ajuste los valores del **[!UICONTROL umbral de optimización de transferencia binaria original]** en función de la red. Las representaciones de recursos superiores a este umbral se transfieren de forma asíncrona.
   1. Select **[!UICONTROL Datastore Shared with Connected Assets]**, if you use a datastore to store your assets and the Datastore is the common storage between both Experience Manager deployments. En este caso, el límite de umbral no importa, ya que los binarios de activos reales se encuentran en el almacén de datos y no se transfieren.
      ![Una configuración típica para los recursos conectados](assets/connected-assets-typical-config.png)
   *Figura: Una configuración típica para los recursos conectados.*

1. Dado que los recursos ya se han procesado y se han recuperado las representaciones, deshabilite los iniciadores del flujo de trabajo. Adjust the launcher configurations on the local ([!DNL Experience Manager Sites]) deployment to exclude the `connectedassets` folder, in which the remote assets are fetched.

   1. On [!DNL Experience Manager Sites] deployment, click **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Launchers]**.

   1. Busque iniciadores con flujos de trabajo como **[!UICONTROL Recurso de actualización DAM]** y **[!UICONTROL Reescritura de metadatos DAM]**.

   1. Seleccione el lanzador del flujo de trabajo y haga clic en **[!UICONTROL Propiedades]** en la barra de acciones.

   1. En el asistente Propiedades, cambie los campos **[!UICONTROL Ruta]** como las asignaciones siguientes para actualizar sus expresiones regulares y excluir **[!UICONTROL connectedassets]**.
   | Antes | Después |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Todas las representaciones disponibles en la implementación remota de Experience Manager se buscan cuando los autores buscan un recurso. Si desea crear más representaciones de un recurso recuperado, omita este paso de configuración. The [!UICONTROL DAM Update Asset] workflow gets triggered and creates more renditions. These renditions are available only on the local [!DNL Sites] deployment and not on the remote DAM deployment.

1. Add the [!DNL Experience Manager Sites] instance as one of the **[!UICONTROL Allowed Origins]** on the remote [!DNL Experience Manager Assets] CORS configuration.

   1. Inicie sesión con las credenciales del administrador. Buscar `Cross-Origin`. Acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.

   1. To create a CORS configuration for [!DNL Experience Manager Sites] instance, click ![aem_assets_add_icon](assets/aem_assets_add_icon.png) icon next to **[!UICONTROL Adobe Granite Cross-Origin Resource Sharing Policy]**.

   1. In the field **[!UICONTROL Allowed Origins]**, input the URL of the local [!DNL Sites], that is, `https://[local_sites]:[port]`. Guarde la configuración.

## Usar recursos remotos {#use-remote-assets}

Los creadores del sitio web utilizan el buscador de contenido para conectarse a la instancia de DAM. Los autores pueden examinar, buscar y arrastrar los recursos remotos de un componente. Para autenticarse en el DAM remoto, conserve las credenciales del usuario DAM proporcionadas por el administrador.

Los autores pueden utilizar los recursos disponibles en las instancias DAM local y DAM remota en una sola página web. Utilice el buscador de contenido para decidir si buscar en el DAM local o en el DAM remoto.

Only those tags of remote assets are fetched that have an exact corresponding tag along with the same taxonomy hierarchy, available on the local [!DNL Sites] instance. Todas las demás etiquetas se descartan. Los autores pueden buscar recursos remotos utilizando todas las etiquetas presentes en la implementación remota de Experience Manager, ya que Experience Manager oferta una búsqueda de texto completo.

### Introducción al uso {#walk-through-of-usage}

Utilice la configuración anterior para probar la experiencia de creación y comprender cómo se utiliza la funcionalidad. Utilice documentos o imágenes de su elección en la implementación remota de DAM.

1. Navigate to the [!DNL Assets] user interface on the remote deployment by accessing **[!UICONTROL Assets]** > **[!UICONTROL Files]** from [!DNL Experience Manager] workspace. También puede acceder a `https://[assets_servername_ams]:[port]/assets.html/content/dam` en un explorador. Cargue los recursos que desee.
1. On the [!DNL Sites] instance, in the profile activator in the upper-right corner, click **[!UICONTROL Impersonate as]**. Utilice `ksaner` como nombre de usuario, seleccione la opción proporcionada y haga clic en **[!UICONTROL Aceptar]**.
1. Abra una página web de We.Retail en **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Edite la página. También puede acceder a `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` en un navegador para editar una página.

   Haga clic en **[!UICONTROL Alternar panel lateral]** en la esquina superior izquierda de la página.

1. Open the [!UICONTROL Assets] tab and click **[!UICONTROL Log in to Connected Assets]**.
1. Proporcione las credenciales (`ksaner` como nombre de usuario y `password` como contraseña). This user has authoring permissions on both the [!DNL Experience Manager] deployments.
1. Busque el recurso que agregó a DAM. Los recursos remotos se muestran en el panel izquierdo. Filtre por imágenes o documentos y por tipos de documentos compatibles. Arrastre las imágenes a un componente `Image` y los documentos a un componente `Download`.

   The fetched assets are read-only on the local [!DNL Experience Manager Sites] deployment. You can still use the options provided by your [!DNL Experience Manager Sites] components to edit the fetched asset. La edición por componentes no es destructiva.

   ![Opciones para filtrar tipos de documentos e imágenes al buscar recursos en DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: Opciones para filtrar tipos de documentos e imágenes al buscar recursos en DAM remoto.*

1. Se notifica al creador del sitio si se busca un recurso de forma asincrónica y si falla alguna tarea de recuperación. Durante la creación o incluso después de esta, los autores pueden ver información detallada sobre las tareas de recuperación y los errores en la interfaz de usuario de [trabajos asincrónicos](/help/assets/asynchronous-jobs.md).

   ![Notificación sobre la captura asincrónica de recursos que se produce en segundo plano.](assets/assets_async_transfer_fails.png)

   *Figura: Notificación sobre la captura asincrónica de recursos que se produce en segundo plano.*

1. When publishing a page, [!DNL Experience Manager] displays a complete list of assets that are used in the page. Asegúrese de que los recursos remotos se recuperan correctamente en el momento de la publicación. Para comprobar el estado de cada recurso recuperado, consulte la interfaz de usuario de [trabajos asincrónicos](/help/assets/asynchronous-jobs.md) .

   >[!NOTE]
   >
   >Aunque no se recuperen uno o varios recursos remotos, la página se publicará. El componente que utiliza el recurso remoto se publica en blanco. The [!DNL Experience Manager] notification area displays notification for errors that show in async jobs page.

>[!CAUTION]
>
>Una vez que se utilizan en una página web, cualquier persona que tenga permiso para acceder a la carpeta local en la que se almacenan los recursos recuperados puede acceder y utilizar los recursos remotos (`connectedassets` en el tutorial anterior). Los recursos también se pueden buscar y ver en el repositorio local mediante [!UICONTROL Buscador de contenido].

Los recursos recuperados se pueden usar como cualquier otro recurso local, pero los metadatos asociados no se pueden editar.

## Restricciones          {#limitations}

**Permisos y administración de recursos**

* Los recursos locales no se sincronizan con los recursos originales en la implementación remota. Las ediciones, eliminaciones o revocaciones de permisos en la implementación de DAM no se propagan de forma descendente.
* Los recursos locales son copias de solo lectura. Los componentes de Experience Manager realizan ediciones no destructivas en los recursos. No se permiten otras ediciones.
* Los recursos recuperados localmente solo están disponibles para la creación. Los flujos de trabajo de actualización de recursos no se pueden aplicar y los metadatos no se pueden editar.
* Solo se admiten las imágenes y los formatos de documento enumerados. [!DNL Dynamic Media]Los recursos de , los fragmentos de contenido y los fragmentos de experiencia no son admitidos.
* No se recuperan los esquemas de metadatos.
* All [!DNL Sites] authors have read permissions on the fetched copies, even if they do not have access to the remote DAM deployment.
* No se admiten las API para personalizar la integración.
* La funcionalidad admite la búsqueda y el uso ininterrumpidos de recursos remotos. Para que varios recursos remotos estén disponibles en la implementación local, considere migrar los recursos. Consulte [Guía de migración de recursos](assets-migration-guide.md).
* No es posible utilizar un recurso remoto como miniatura de página en la interfaz de usuario Propiedades [!UICONTROL de la] página. Puede establecer una miniatura de una página web en la interfaz de usuario Propiedades [!UICONTROL de] página desde la [!UICONTROL miniatura] haciendo clic en [!UICONTROL Seleccionar imagen].

**Configuración y licencia**

* [!DNL Experience Manager Assets] se admite la implementación en AMS.
* [!DNL Experience Manager Sites] Puede conectarse a un único [!DNL Experience Manager Assets] repositorio a la vez.
* A license of [!DNL Experience Manager Assets] working as remote repository.
* One or more licenses of [!DNL Experience Manager Sites] working as local authoring deployment.

**Uso**

* Solo se admite la funcionalidad de buscar recursos remotos y arrastrarlos a la página local para crear contenido.
* La operación de recuperación expira al cabo de 5 segundos. Los autores pueden tener problemas para recuperar recursos, por ejemplo, si hay problemas de red. Los autores pueden volver a intentarlo arrastrando el recurso remoto desde [!UICONTROL Buscador de contenido] al [!UICONTROL Editor de páginas].
* Las ediciones simples que no son destructivas y que se admiten mediante el componente [!DNL Experience Manager], se pueden realizar en los recursos recuperados. `Image` Los recursos son de solo lectura.

## Solución de problemas {#troubleshoot}

Siga estos pasos para solucionar los problemas de los escenarios de error comunes:

* Si no puede buscar recursos remotos desde el Buscador de contenido, vuelva a comprobar y asegúrese de que las funciones y los permisos necesarios estén establecidos.
* Puede que un recurso recuperado de un DAM remoto no se publique en una página web por las siguientes razones: no existe en remoto; falta de permisos adecuados para recuperarla; error de red. Asegúrese de que no se elimine el recurso del DAM remoto o de que los permisos no se modifiquen. Garantice que se cumplan los requisitos previos adecuados. Vuelva a intentar agregar el recurso a la página y vuelva a publicar. Compruebe la [lista de trabajos asincrónicos](/help/assets/asynchronous-jobs.md) si hay errores en la recuperación de recursos.
