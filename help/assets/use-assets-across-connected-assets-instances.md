---
title: Utilice los recursos conectados para compartir recursos de DAM en [!DNL Sites]
description: Utilice los recursos disponibles en una implementación remota [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] .
contentOwner: AG
translation-type: tm+mt
source-git-commit: d05dc3af0a885e51758194783e773695086d7956
workflow-type: tm+mt
source-wordcount: '2263'
ht-degree: 41%

---


# Utilice los recursos conectados para compartir recursos de DAM en [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

En las grandes empresas se puede distribuir la infraestructura necesaria para crear sitios web. A veces, las capacidades de creación de sitios web y los recursos digitales utilizados para crear estos sitios web se pueden encontrar en diferentes implementaciones. Una razón puede ser la distribución geográfica de las implementaciones existentes que se requieren para trabajar en conjunto. Otra razón pueden ser las adquisiciones que conducen a una infraestructura heterogénea que la compañía principal desea utilizar en conjunto.

Los usuarios pueden crear páginas Web en [!DNL Experience Manager Sites]. [!DNL Experience Manager Assets] es el sistema de administración de recursos digitales (DAM) que proporciona los recursos necesarios para los sitios web. [!DNL Experience Manager] ahora admite el caso de uso anterior mediante la integración  [!DNL Sites] y  [!DNL Assets].

## Información general sobre los recursos conectados {#overview-of-connected-assets}

Al editar páginas en [!UICONTROL Editor de páginas] como destino de destinatario, los autores pueden buscar, examinar e incrustar recursos de forma transparente desde una implementación [!DNL Assets] diferente que actúa como fuente de recursos. Los administradores crean una integración única de una implementación de [!DNL Experience Manager] con capacidad [!DNL Sites] con otra implementación de [!DNL Experience Manager] con capacidad [!DNL Assets].

Para los autores [!DNL Sites], los recursos remotos están disponibles como recursos locales de sólo lectura. La función admite la búsqueda y el uso ininterrumpidos de algunos recursos remotos a la vez. Para hacer que muchos recursos remotos estén disponibles en una implementación [!DNL Sites] en un solo uso, considere migrar los recursos de forma masiva. Consulte [Guía de migración de recursos de Experience Manager](/help/assets/assets-migration-guide.md).

### Requisitos previos e implementaciones admitidas {#prerequisites}

Antes de usar o configurar esta capacidad, asegúrese de lo siguiente:

* Los usuarios forman parte de los grupos de usuarios correspondientes en cada implementación.
* Para los tipos de implementación [!DNL Adobe Experience Manager], se cumple uno de los criterios admitidos. [!DNL Experience Manager] 6.5  [!DNL Assets] trabaja  [!DNL Experience Manager] como Cloud Service. Para obtener más información sobre cómo funciona esta funcionalidad en [!DNL Experience Manager as a Cloud Service], consulte [Recursos conectados en Experience Manager como Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Sites] como Cloud Service | [!DNL Experience Manager] 6.5  [!DNL Sites] sobre AMS | [!DNL Experience Manager] 6.5  [!DNL Sites] in situ |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]como un[!DNL Cloud Service]** | Compatible | Compatible | Compatible |
   | **[!DNL Experience Manager]6.5  [!DNL Assets] sobre AMS** | Compatible | Compatible | Compatible |
   | **[!DNL Experience Manager]6.5  [!DNL Assets] in situ** | No compatible | No compatible | No compatible |

### Formatos de archivo compatibles {#mimetypes}

Los autores buscan imágenes y los siguientes tipos de documentos en el Buscador de contenido y utilizan los recursos buscados en el Editor de páginas. Se agregan documentos al componente `Download` y a las imágenes al componente `Image`. Los autores también agregan los recursos remotos en cualquier componente [!DNL Experience Manager] personalizado que extienda los componentes predeterminados `Download` o `Image`. Los formatos admitidos son:

* **Formatos** de imagen: Formatos compatibles con el  [componente ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html) Imagen. [!DNL Dynamic Media] las imágenes no son compatibles.
* **Formatos** de documento: Consulte los formatos [ de documento ](assets-formats.md#supported-document-formats)admitidos.

### Usuarios y grupos implicados {#users-and-groups-involved}

A continuación se describen las distintas funciones que se usan para configurar y utilizar la capacidad y sus grupos de usuarios correspondientes. El ámbito local se utiliza para el caso de uso en el que un autor crea una página web. El ámbito remoto se utiliza para la implementación de DAM que aloja los recursos necesarios. El autor [!DNL Sites] obtiene estos recursos remotos.

| Función | Ámbito | Grupo de usuarios | Nombre de usuario en la introducción | Requisito |
|---|---|---|---|---|
| [!DNL Sites] administrador | Local | [!DNL Experience Manager] `administrators` | `admin` | Configure [!DNL Experience Manager] y configure la integración con la implementación remota [!DNL Assets]. |
| Usuario DAM | Local | `Authors` | `ksaner` | Se utiliza para ver y duplicar los recursos recuperados en `/content/DAM/connectedassets/`. |
| [!DNL Sites] author | Local | <ul><li>`Authors` (con acceso de lectura en el DAM remoto y acceso de autor en local  [!DNL Sites]) </li> <li>`dam-users` en local  [!DNL Sites]</li></ul> | `ksaner` | Los usuarios finales son [!DNL Sites] autores que utilizan esta integración para mejorar la velocidad de contenido. Los autores buscan y exploran recursos en DAM remoto mediante [!UICONTROL Buscador de contenido] y utilizando las imágenes requeridas en las páginas Web locales. Se utilizan las credenciales del usuario de DAM `ksaner`. |
| [!DNL Assets] administrador | Remoto | [!DNL Experience Manager] `administrators` | `admin` en remoto  [!DNL Experience Manager] | Configurar el intercambio de recursos de origen cruzado (CORS). |
| Usuario DAM | Remoto | `Authors` | `ksaner` en remoto  [!DNL Experience Manager] | Función de autor en la implementación remota [!DNL Experience Manager]. Busque y examine recursos en Recursos conectados mediante el [!UICONTROL Buscador de contenido]. |
| Distribuidor DAM (usuario técnico) | Remoto | [!DNL Sites] `Authors` | `ksaner` en remoto  [!DNL Experience Manager] | Este usuario presente en la implementación remota lo utiliza el servidor local [!DNL Experience Manager] (no la función de autor [!DNL Sites]) para recuperar los recursos remotos, en nombre del autor [!DNL Sites]. Esta función no es la misma que las dos funciones `ksaner` anteriores y pertenece a un grupo de usuarios diferente. |

## Configurar una conexión entre [!DNL Sites] y [!DNL Assets] implementaciones {#configure-a-connection-between-sites-and-assets-deployments}

Un administrador [!DNL Experience Manager] puede crear esta integración. Una vez creados, los permisos necesarios para utilizarlos se establecen mediante grupos de usuarios. Los grupos de usuarios se definen en la implementación [!DNL Sites] y en la implementación de DAM.

Para configurar los recursos conectados y la conectividad [!DNL Sites] local, siga estos pasos:

1. Acceda a una implementación existente [!DNL Sites] o cree una implementación con el siguiente comando:

   1. En la carpeta del archivo JAR, ejecute el siguiente comando en un terminal para crear cada servidor [!DNL Experience Manager].
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Después de unos minutos, el servidor [!DNL Experience Manager] inicio correctamente. Considere esta [!DNL Sites] implementación como el equipo local para la creación de páginas Web, digamos en `https://[local_sites]:4502`.

1. Asegúrese de que los usuarios y las funciones con ámbito local existan en la implementación [!DNL Sites] y en la implementación [!DNL Assets] en AMS. Cree un usuario técnico en la implementación [!DNL Assets] y añádalo al grupo de usuarios mencionado en [usuarios y grupos involucrados](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Acceda a la implementación local [!DNL Sites] en `https://[local_sites]:4502`. Haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Configuración de recursos conectados]** y proporcione los siguientes valores:

   1. [!DNL Assets] la ubicación es  `https://[assets_servername_ams]:[port]`.
   1. Credenciales de un distribuidor DAM (usuario técnico).
   1. En el campo **[!UICONTROL Punto de montaje]**, introduzca la ruta [!DNL Experience Manager] local donde [!DNL Experience Manager] busca los recursos. Por ejemplo, la carpeta `remoteassets`.
   1. Ajuste los valores del **[!UICONTROL umbral de optimización de transferencia binaria original]** en función de la red. Las representaciones de recursos superiores a este umbral se transfieren de forma asíncrona.
   1. Seleccione **[!UICONTROL almacén de datos compartido con recursos conectados]**, si utiliza un almacén de datos para almacenar los recursos y este es el almacenamiento común entre ambas implementaciones de En este caso, el límite de umbral no importa, ya que los binarios de activos reales se encuentran en el almacén de datos y no se transfieren.

   ![Una configuración típica para los recursos conectados](assets/connected-assets-typical-config.png)

   *Figura: Una configuración típica para los recursos conectados.*

1. Dado que los recursos ya se han procesado y se han recuperado las representaciones, deshabilite los iniciadores del flujo de trabajo. Ajuste las configuraciones del iniciador en la implementación local ([!DNL Sites]) para excluir la carpeta `connectedassets`, en la que se recuperan los recursos remotos.

   1. En la implementación [!DNL Sites], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Lanzadores]**.

   1. Busque iniciadores con flujos de trabajo como **[!UICONTROL Recurso de actualización DAM]** y **[!UICONTROL Reescritura de metadatos DAM]**.

   1. Seleccione el lanzador del flujo de trabajo y haga clic en **[!UICONTROL Propiedades]** en la barra de acciones.

   1. En el asistente [!UICONTROL Properties], cambie los campos **[!UICONTROL Path]** como las siguientes asignaciones para actualizar sus expresiones regulares y excluir el punto de montaje **[!UICONTROL recursos conectados]**.

   | Antes | Después |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Todas las representaciones disponibles en la implementación remota de se recuperan cuando los autores recuperan un recurso. Si desea crear más representaciones de un recurso recuperado, omita este paso de configuración. El flujo de trabajo [!UICONTROL Recurso de actualización de DAM] se activa y crea más representaciones. Estas representaciones solo están disponibles en la implementación local [!DNL Sites] y no en la implementación remota de DAM.

1. Añada la implementación [!DNL Sites] como uno de los **[!UICONTROL Orígenes permitidos]** en la configuración [!DNL Assets'] CORS remota.

   1. Inicie sesión con las credenciales del administrador. Buscar `Cross-Origin`. Acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.

   1. Para crear una configuración CORS para [!DNL Sites] implementación, haga clic en la opción ![Agregar icono de recursos](assets/do-not-localize/assets_add_icon.png) junto a **[!UICONTROL Política de uso compartido de recursos de Adobe Granite Cross-Origen]**.

   1. En el campo **[!UICONTROL Orígenes permitidos]**, introduzca la dirección URL del [!DNL Sites] local, es decir, `https://[local_sites]:[port]`. Guarde la configuración.

## Usar recursos remotos {#use-remote-assets}

Los creadores del sitio web utilizan Content Finder para conectarse a la implementación de DAM. Los autores pueden examinar, buscar y arrastrar los recursos remotos de un componente. Para autenticarse en el DAM remoto, conserve las credenciales del usuario DAM proporcionadas por el administrador.

Los autores pueden utilizar los recursos disponibles en el DAM local y en la implementación remota de DAM, en una sola página web. Utilice el buscador de contenido para decidir si buscar en el DAM local o en el DAM remoto.

Solo se buscan las etiquetas de los recursos remotos que tienen una etiqueta correspondiente exacta junto con la misma jerarquía de taxonomía, disponible en la implementación local [!DNL Sites]. Todas las demás etiquetas se descartan. Los autores pueden buscar recursos remotos utilizando todas las etiquetas presentes en la implementación remota [!DNL Experience Manager], ya que oferta una búsqueda de texto completo.

### Introducción al uso {#walk-through-of-usage}

Utilice la configuración anterior para probar la experiencia de creación y comprender cómo se utiliza la funcionalidad. Utilice documentos o imágenes de su elección en la implementación remota de DAM.

1. Navegue hasta la interfaz [!DNL Assets] en la implementación remota accediendo a **[!UICONTROL Assets]** > **[!UICONTROL Files]** desde el área de trabajo [!DNL Experience Manager]. También puede acceder a `https://[assets_servername_ams]:[port]/assets.html/content/dam` en un explorador. Cargue los recursos que desee.
1. En la implementación [!DNL Sites], en el activador de perfil en la esquina superior derecha, haga clic en **[!UICONTROL Suplantar como]**. Utilice `ksaner` como nombre de usuario, seleccione la opción proporcionada y haga clic en **[!UICONTROL Aceptar]**.
1. Abra una página web de We.Retail en **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Edite la página. También puede acceder a `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` en un navegador para editar una página.

   Haga clic en **[!UICONTROL Alternar panel lateral]** en la esquina superior izquierda de la página.

1. Abra la ficha [!UICONTROL Recursos] y haga clic en **[!UICONTROL Iniciar sesión en Recursos conectados]**.
1. Proporcione las credenciales (`ksaner` como nombre de usuario y `password` como contraseña). Este usuario tiene permisos de creación en ambas implementaciones [!DNL Experience Manager].
1. Busque el recurso que agregó a DAM. Los recursos remotos se muestran en el panel izquierdo. Filtre por imágenes o documentos y por tipos de documentos compatibles. Arrastre las imágenes a un componente `Image` y los documentos a un componente `Download`.

   Los recursos recuperados son de sólo lectura en la implementación local [!DNL Sites]. Puede seguir utilizando las opciones proporcionadas por los componentes [!DNL Sites] para editar el recurso buscado. La edición por componentes no es destructiva.

   ![Opciones para filtrar tipos de documentos e imágenes al buscar recursos en DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: Opciones para filtrar tipos de documentos e imágenes al buscar recursos en DAM remoto.*

1. Se notifica al creador del sitio si se busca un recurso de forma asincrónica y si falla alguna tarea de recuperación. Durante la creación o incluso después de esta, los autores pueden ver información detallada sobre las tareas de recuperación y los errores en la interfaz de usuario de [trabajos asincrónicos](/help/sites-administering/asynchronous-jobs.md).

   ![Notificación sobre la captura asincrónica de recursos que se produce en segundo plano.](assets/assets_async_transfer_fails.png)

   *Figura: Notificación sobre la captura asincrónica de recursos que se produce en segundo plano.*

1. Al publicar una página, [!DNL Experience Manager] muestra una lista completa de los recursos que se utilizan en la página. Asegúrese de que los recursos remotos se recuperan correctamente en el momento de la publicación. Para comprobar el estado de cada recurso recuperado, consulte la interfaz de usuario de [trabajos asincrónicos](/help/sites-administering/asynchronous-jobs.md) .

   >[!NOTE]
   >
   >Aunque no se recuperen uno o varios recursos remotos, la página se publicará. El componente que utiliza el recurso remoto se publica en blanco. El área de notificación [!DNL Experience Manager] muestra una notificación para los errores que se muestran en la página de trabajos asincrónicos.

>[!CAUTION]
>
>Una vez utilizados en una página web, los recursos remotos recuperados pueden ser buscados y utilizados por cualquier persona que tenga permiso para acceder a la carpeta local. Los recursos recuperados se almacenan en la carpeta local (`connectedassets` en la ruta anterior). Los recursos también se pueden buscar y ver en el repositorio local mediante [!UICONTROL Buscador de contenido].

Los recursos recuperados se pueden usar como cualquier otro recurso local, pero los metadatos asociados no se pueden editar.

## Restricciones          y prácticas recomendadas {#tips-and-limitations}

* Para obtener información sobre el uso de los recursos, configure la funcionalidad [Asset Insight](/help/assets/asset-insights.md) en la instancia [!DNL Sites].

### Permisos y administración de recursos {#permissions-and-managing-assets}

* Los recursos locales no se sincronizan con los recursos originales en la implementación remota. Las ediciones, eliminaciones o revocaciones de permisos en la implementación de DAM no se propagan de forma descendente.
* Los recursos locales son copias de solo lectura. [!DNL Experience Manager]Los componentes de realizan ediciones no destructivas en los recursos. No se permiten otras ediciones.
* Los recursos recuperados localmente solo están disponibles para la creación. Los flujos de trabajo de actualización de recursos no se pueden aplicar y los metadatos no se pueden editar.
* Solo se admiten las imágenes y los formatos de documento enumerados. [!DNL Dynamic Media]Los recursos de , los fragmentos de contenido y los fragmentos de experiencia no son admitidos.
* [!DNL Experience Manager] no captura los esquemas de metadatos. Significa que es posible que no se muestren todos los metadatos buscados. Si el esquema se actualiza por separado, se muestran todas las propiedades.
* Todos los autores [!DNL Sites] tienen permisos de lectura en las copias buscadas, incluso si los autores no pueden acceder a la implementación remota de DAM.
* No se admiten las API para personalizar la integración.
* La funcionalidad admite la búsqueda y el uso ininterrumpidos de recursos remotos. Para que varios recursos remotos estén disponibles en la implementación local, considere migrar los recursos. Consulte [Guía de migración de recursos](assets-migration-guide.md).
* No es posible utilizar un recurso remoto como miniatura de página en la interfaz de usuario [!UICONTROL Propiedades de la página]. Puede establecer una miniatura de una página Web en la interfaz de usuario [!UICONTROL Propiedades de la página] desde la [!UICONTROL Miniatura] haciendo clic en [!UICONTROL Seleccionar imagen].

### Configuración y licencia {#setup-licensing}

* [!DNL Assets] se  [!DNL Adobe Managed Services] admite la implementación en.
* [!DNL Sites] Puede conectarse a un único  [!DNL Assets] repositorio a la vez.
* Licencia de [!DNL Assets] que trabaja como repositorio remoto.
* Una o más licencias de [!DNL Sites] que funcionan como implementación de creación local.

### Uso {#usage}

* Los usuarios pueden buscar recursos remotos y arrastrarlos a la página local durante la creación. No se admite ninguna otra funcionalidad.
* La operación de recuperación expira al cabo de 5 segundos. Los autores pueden tener problemas para recuperar recursos, por ejemplo, si hay problemas de red. Los autores pueden volver a tentarse arrastrando el recurso remoto desde [!UICONTROL Content Finder] a [!UICONTROL Page Editor].
* Las ediciones simples que no son destructivas y que se admiten mediante el componente `Image`, se pueden realizar en los recursos recuperados. Los recursos son de solo lectura.
* El único método para recuperar el recurso es arrastrarlo a una página. No hay soporte API ni otros métodos para recuperar un recurso para actualizarlo.
* Si los recursos se retiran del DAM, se seguirán utilizando en [!DNL Sites] páginas.

## Solución de problemas {#troubleshoot}

Para solucionar problemas del escenario de error común, siga estos pasos:

* Si no puede buscar recursos remotos desde el [!UICONTROL Buscador de contenido], asegúrese de que las funciones y los permisos necesarios estén establecidos.
* Es posible que un recurso recuperado de la presa remota no se publique en una página web por una o varias razones. No existe en el servidor remoto, la falta de los permisos adecuados para recuperarlo o la falla de red pueden ser las razones. Asegúrese de que el recurso no se elimina del DAM remoto. Asegúrese de que se han establecido los permisos adecuados y de que se cumplen los requisitos previos. Vuelva a intentar agregar el recurso a la página y vuelva a publicarlo. Compruebe la [lista de trabajos asincrónicos](/help/sites-administering/asynchronous-jobs.md) si hay errores en la recuperación de recursos.
* Si no puede acceder a la implementación remota de DAM desde la implementación local [!DNL Sites], asegúrese de que se permiten cookies entre sitios. Si las cookies entre sitios están bloqueadas, es posible que las dos implementaciones de [!DNL Experience Manager] no se autentiquen. Por ejemplo: [!DNL Google Chrome] en el modo Incognito puede bloquear las cookies de terceros. Para permitir las cookies en el explorador [!DNL Chrome], haga clic en el icono &#39;ojo&#39; en la barra de direcciones, vaya a Sitio que no funciona > Bloqueado, seleccione la URL DAM remota y permita la cookie de autentificador de inicio de sesión. De forma alternativa, consulte la ayuda sobre [cómo habilitar las cookies de terceros](https://support.google.com/chrome/answer/95647).

   ![Error de cookie en Chrome en modo incógnito](assets/chrome-cookies-incognito-dialog.png)
