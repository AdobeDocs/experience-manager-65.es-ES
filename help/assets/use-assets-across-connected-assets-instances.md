---
title: Utilice los recursos conectados para compartir recursos de DAM en [!DNL Sites]
description: Utilice los recursos disponibles en una implementación remota [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] .
contentOwner: AG
role: User, Admin, Leader
feature: Connected Assets,User and Groups
exl-id: 4ceb49d8-b619-42b1-81e7-c3e83d4e6e62
source-git-commit: 218e97eb31061e833f3b291a6607b2ebf4762471
workflow-type: tm+mt
source-wordcount: '2967'
ht-degree: 26%

---

# Utilice los recursos conectados para compartir recursos de DAM en [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

En las grandes empresas se puede distribuir la infraestructura necesaria para crear sitios web. A veces, las capacidades de creación de sitios web y los recursos digitales utilizados para crear estos sitios web se pueden encontrar en diferentes implementaciones. Una razón puede ser la distribución geográfica de implementaciones existentes que son necesarias para trabajar juntas. Otra razón puede ser que las adquisiciones conducen a una infraestructura heterogénea, incluidas distintas versiones [!DNL Experience Manager] que la empresa principal desea utilizar juntas.

La funcionalidad Recursos conectados admite el caso de uso anterior mediante la integración de [!DNL Experience Manager Sites] y [!DNL Experience Manager Assets]. Los usuarios pueden crear páginas web en [!DNL Sites] que utilicen los recursos digitales de implementaciones [!DNL Assets] independientes.

## Información general sobre los recursos conectados {#overview-of-connected-assets}

Al editar páginas en [!UICONTROL Editor de páginas] como destino, los autores pueden buscar, examinar e incrustar recursos sin problemas desde una implementación [!DNL Assets] diferente que actúa como fuente de recursos. Los administradores crean una integración única de una implementación de [!DNL Experience Manager] con capacidad [!DNL Sites] con otra implementación de [!DNL Experience Manager] con capacidad [!DNL Assets]. Los creadores del sitio también pueden utilizar imágenes de Dynamic Media en las páginas web de su sitio a través de los recursos conectados y aprovechar las funcionalidades de Dynamic Media, como los ajustes preestablecidos de imagen y recorte inteligente.

Para los autores [!DNL Sites], los recursos remotos están disponibles como recursos locales de solo lectura. La función admite la búsqueda y el uso ininterrumpidos de algunos recursos remotos a la vez. Para que varios recursos remotos estén disponibles en una implementación [!DNL Sites] en un solo uso, considere migrar los recursos de forma masiva. Consulte [Guía de migración de recursos de Experience Manager](/help/assets/assets-migration-guide.md).

### Requisitos previos e implementaciones admitidas {#prerequisites}

Antes de usar o configurar esta capacidad, asegúrese de lo siguiente:

* Los usuarios forman parte de los grupos de usuarios correspondientes en cada implementación.
* Para los tipos de implementación [!DNL Adobe Experience Manager], se cumple uno de los criterios admitidos. [!DNL Experience Manager] 6.5  [!DNL Assets] funciona  [!DNL Experience Manager] como Cloud Service. Para obtener más información sobre cómo funciona esta funcionalidad en [!DNL Experience Manager] como [!DNL Cloud Service], consulte [Recursos conectados en [!DNL Experience Manager] como  [!DNL Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Sites] as a [!DNL Cloud Service] | [!DNL Experience Manager] 6.5  [!DNL Sites] en AMS | [!DNL Experience Manager] 6.5  [!DNL Sites] local |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]como[!DNL Cloud Service]** | Compatible | Compatible | Compatible |
   | **[!DNL Experience Manager]6.5  [!DNL Assets] en AMS** | Compatible | Compatible | Compatible |
   | **[!DNL Experience Manager]6.5  [!DNL Assets] local** | No compatible | No compatible | No compatible |

### Formatos de archivo compatibles {#mimetypes}

Los autores buscan imágenes y los siguientes tipos de documentos en el buscador de contenido y utilizan los recursos buscados en el editor de páginas. Los documentos se añaden al componente `Download` y las imágenes al componente `Image`. Los autores también agregan los recursos remotos en cualquier componente personalizado [!DNL Experience Manager] que amplía los componentes predeterminados `Download` o `Image`. Los formatos admitidos son:

* **Formatos** de imagen: Los formatos compatibles con el  [componente ](https://www.aemcomponents.dev/content/core-components-examples/library/page-authoring/image.html) Imagen.
* **Formatos** de documento: Consulte los formatos de documento  [admitidos](assets-formats.md#supported-document-formats).

### Usuarios y grupos implicados {#users-and-groups-involved}

A continuación se describen las distintas funciones que se usan para configurar y utilizar la capacidad y sus grupos de usuarios correspondientes. El ámbito local se utiliza para el caso de uso en el que un autor crea una página web. El ámbito remoto se utiliza para la implementación de DAM que aloja los recursos necesarios. El autor [!DNL Sites] recupera estos recursos remotos.

| Función | Ámbito | Grupo de usuarios | Nombre de usuario en la introducción | Requisito |
|---|---|---|---|---|
| [!DNL Sites] administrador | Local | [!DNL Experience Manager] `administrators` | `admin` | Configure [!DNL Experience Manager] y configure la integración con la implementación remota [!DNL Assets]. |
| Usuario DAM | Local | `Authors` | `ksaner` | Se utiliza para ver y duplicar los recursos recuperados en `/content/DAM/connectedassets/`. |
| [!DNL Sites] author | Local | <ul><li>`Authors` (con acceso de lectura en el DAM remoto y acceso de autor en el local  [!DNL Sites]) </li> <li>`dam-users` en local  [!DNL Sites]</li></ul> | `ksaner` | Los usuarios finales son [!DNL Sites] autores que utilizan esta integración para mejorar la velocidad de contenido. Los autores buscan y exploran recursos en DAM remoto utilizando [!UICONTROL Buscador de contenido] y utilizando las imágenes necesarias en las páginas web locales. Se utilizan las credenciales del usuario de DAM `ksaner`. |
| [!DNL Assets] administrador | Remoto | [!DNL Experience Manager] `administrators` | `admin` en remoto  [!DNL Experience Manager] | Configurar el intercambio de recursos de origen cruzado (CORS). |
| Usuario DAM | Remoto | `Authors` | `ksaner` en remoto  [!DNL Experience Manager] | Función de autor en la implementación remota [!DNL Experience Manager]. Busque y examine recursos en Recursos conectados mediante el [!UICONTROL Buscador de contenido]. |
| Distribuidor DAM (usuario técnico) | Remoto | [!DNL Sites] `Authors` | `ksaner` en remoto  [!DNL Experience Manager] | El servidor local [!DNL Experience Manager] (no la función de autor [!DNL Sites]) utiliza a este usuario presente en la implementación remota para recuperar los recursos remotos en nombre del autor [!DNL Sites]. Esta función no es la misma que las dos funciones `ksaner` anteriores y pertenece a un grupo de usuarios diferente. |

## Configurar una conexión entre las implementaciones [!DNL Sites] y [!DNL Assets] {#configure-a-connection-between-sites-and-assets-deployments}

Un administrador [!DNL Experience Manager] puede crear esta integración. Una vez creados, los permisos necesarios para utilizarlos se establecen mediante grupos de usuarios. Los grupos de usuarios se definen en la implementación [!DNL Sites] y en la implementación de DAM.

Para configurar los recursos conectados y la conectividad local [!DNL Sites], siga estos pasos:

1. Acceda a una implementación existente [!DNL Sites] o cree una implementación con el siguiente comando:

   1. En la carpeta del archivo JAR, ejecute el siguiente comando en un terminal para crear cada servidor [!DNL Experience Manager].
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Después de unos minutos, el servidor [!DNL Experience Manager] se inicia correctamente. Considere esta implementación [!DNL Sites] como el equipo local para la creación de páginas web, por ejemplo, en `https://[local_sites]:4502`.

1. Asegúrese de que los usuarios y las funciones con el ámbito adecuado existan en la implementación [!DNL Sites] y en la implementación [!DNL Assets] en AMS. Cree un usuario técnico en la implementación [!DNL Assets] y añádalo al grupo de usuarios mencionado en [usuarios y grupos involucrados](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Acceda a la implementación local [!DNL Sites] en `https://[local_sites]:4502`. Haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Configuración de recursos conectados]** y proporcione los siguientes valores:

   1. Un **[!UICONTROL Título]** de la configuración.
   1. **[!UICONTROL La]** URL de DAM remota es la URL de la  [!DNL Assets] ubicación con el formato  `https://[assets_servername]:[port]`.
   1. Credenciales de un distribuidor DAM (usuario técnico).
   1. En el campo **[!UICONTROL Punto de montaje]**, introduzca la ruta local [!DNL Experience Manager] donde [!DNL Experience Manager] recupera los recursos. Por ejemplo, la carpeta `remoteassets`. Los recursos recuperados de DAM se almacenan en esta carpeta en la implementación [!DNL Sites] .
   1. **[!UICONTROL La]** URL de sitios locales es la ubicación de la  [!DNL Sites] implementación. [!DNL Assets] la implementación utiliza este valor para mantener referencias a los recursos digitales recuperados mediante esta  [!DNL Sites] implementación.
   1. Credenciales del usuario técnico [!DNL Sites].
   1. El valor del campo **[!UICONTROL Umbral de optimización de transferencia binaria original]** especifica si los recursos originales (incluidas las representaciones) se transfieren sincrónicamente o no. Los recursos con un tamaño de archivo más pequeño se pueden recuperar fácilmente, mientras que los recursos con un tamaño de archivo relativamente mayor se sincronizan mejor asincrónicamente. El valor depende de las capacidades de red.
   1. Seleccione **[!UICONTROL almacén de datos compartido con recursos conectados]**, si utiliza un almacén de datos para almacenar los recursos y este es el almacenamiento común entre ambas implementaciones de En este caso, el límite de umbral no importa, ya que los binarios de activos reales están disponibles en el almacén de datos y no se transfieren.

   ![Una configuración típica para la funcionalidad de los recursos conectados](assets/connected-assets-typical-config.png)

   *Figura: Una configuración típica para la funcionalidad Recursos conectados.*

1. Los recursos digitales existentes en la implementación [!DNL Assets] ya se han procesado y se han generado las representaciones. Estas representaciones se recuperan mediante esta funcionalidad, por lo que no es necesario volver a generar las representaciones. Deshabilite los iniciadores del flujo de trabajo para evitar la regeneración de las representaciones. Ajuste las configuraciones del iniciador en la implementación ([!DNL Sites]) para excluir la carpeta `connectedassets` (los recursos se recuperan en esta carpeta).

   1. En la implementación [!DNL Sites], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Iniciadores]**.

   1. Busque iniciadores con flujos de trabajo como **[!UICONTROL Recurso de actualización DAM]** y **[!UICONTROL Reescritura de metadatos DAM]**.

   1. Seleccione el lanzador del flujo de trabajo y haga clic en **[!UICONTROL Propiedades]** en la barra de acciones.

   1. En el asistente [!UICONTROL Properties], cambie los campos **[!UICONTROL Path]** como las asignaciones siguientes para actualizar sus expresiones regulares y excluir el punto de montaje **[!UICONTROL connectedassets]**.

   | Antes | Después |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Todas las representaciones disponibles en la implementación remota de se recuperan cuando los autores recuperan un recurso. Si desea crear más representaciones de un recurso recuperado, omita este paso de configuración. El flujo de trabajo [!UICONTROL Activo de actualización de DAM] se activa y crea más representaciones. Estas representaciones solo están disponibles en la implementación local [!DNL Sites] y no en la implementación remota de DAM.

1. Agregue la implementación [!DNL Sites] como origen permitido en la configuración CORS de la implementación [!DNL Assets]. Para obtener más información, consulte [Understanding CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html).

1. Configure [el mismo soporte para cookies del sitio](/help/sites-administering/same-site-cookie-support.md).

Puede comprobar la conectividad entre las implementaciones configuradas [!DNL Sites] y la implementación [!DNL Assets].

![Prueba de conexión de los recursos conectados configurada  [!DNL Sites]](assets/connected-assets-multiple-config.png)
*Figura: Prueba de conexión de los recursos conectados configurados  [!DNL Sites].*

### Configuración de una conexión para recursos de Dynamic Media {#sites-dynamic-media-connected-assets}

Puede configurar una conexión entre la implementación [!DNL Sites] y la implementación [!DNL Dynamic Media] que permita que los autores de las páginas web utilicen imágenes [!DNL Dynamic Media] en sus páginas web. Durante la creación de páginas web, la experiencia de usar recursos remotos e implementaciones [!DNL Dynamic Media] remotas permanece igual.

Para configurar la funcionalidad Recursos conectados para implementaciones de Dynamic Media, siga estos pasos:

1. Habilite y configure [!DNL Dynamic Media] como configuración global en la implementación de autor [!DNL Assets] remota. Para configurar Dynamic Media, consulte [Configuración de Dynamic Media](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services).<br/>
En la  [!DNL Assets] implementación remota, en el modo [!UICONTROL  de sincronización de ]Dynamic Media, seleccione  **[!UICONTROL Habilitado de forma predeterminada]**.

1. Cree la configuración de los recursos conectados como se describe en [Configure la conexión entre las implementaciones de sitios y recursos](#configure-a-connection-between-sites-and-assets-deployments). Además, seleccione la opción **[!UICONTROL Buscar representación original para los recursos conectados con Dynamic Media]**.

1. Configure [!DNL Dynamic Media] en implementaciones locales [!DNL Sites] y remotas [!DNL Assets]. Siga las instrucciones para [configurar [!DNL Dynamic Media]](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services).

   * Utilice el mismo nombre de empresa en todas las configuraciones.
   * En [!DNL Sites] local, en [!UICONTROL modo de sincronización de Dynamic Media], seleccione **[!UICONTROL Deshabilitado de forma predeterminada]**. La implementación [!DNL Sites] solo necesita acceso de solo lectura a la cuenta [!DNL Dynamic Media].
   * En [!DNL Sites] local, en la opción **[!UICONTROL Publicar recursos]**, seleccione **[!UICONTROL Publicación selectiva]**. No seleccione **[!UICONTROL Sincronizar todo el contenido]**.

1. Habilite la compatibilidad con [[!DNL Dynamic Media] en el componente principal de imagen](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html#dynamic-media). Esta función permite que el [componente de imagen](https://www.aemcomponents.dev/content/core-components-examples/library/page-authoring/image.html) predeterminado muestre [!DNL Dynamic Media] imágenes cuando los autores utilizan [!DNL Dynamic Media] imágenes en páginas web en la implementación local [!DNL Sites].

## Usar recursos remotos {#use-remote-assets}

Los creadores del sitio web utilizan el buscador de contenido para conectarse a la implementación de DAM. Los autores pueden examinar, buscar y arrastrar los recursos remotos de un componente. Para autenticarse en el DAM remoto, conserve las credenciales del usuario DAM proporcionadas por el administrador.

Los autores pueden utilizar los recursos disponibles en el DAM local y en la implementación remota de DAM, en una sola página web. Utilice el buscador de contenido para decidir si buscar en el DAM local o en el DAM remoto.

Solo se recuperan las etiquetas de recursos remotos que tienen una etiqueta correspondiente exacta junto con la misma jerarquía de taxonomía, disponible en la implementación local [!DNL Sites]. Todas las demás etiquetas se descartan. Los autores pueden buscar recursos remotos utilizando todas las etiquetas presentes en la implementación remota [!DNL Experience Manager], ya que ofrece una búsqueda de texto completo.

### Introducción al uso {#walk-through-of-usage}

Utilice la configuración anterior para probar la experiencia de creación y comprender cómo se utiliza la funcionalidad. Utilice documentos o imágenes de su elección en la implementación remota de DAM.

1. Vaya a la interfaz [!DNL Assets] en la implementación remota accediendo a **[!UICONTROL Assets]** > **[!UICONTROL Files]** desde el espacio de trabajo [!DNL Experience Manager]. También puede acceder a `https://[assets_servername_ams]:[port]/assets.html/content/dam` en un explorador. Cargue los recursos que desee.
1. En la implementación [!DNL Sites], en el activador de perfil en la esquina superior derecha, haga clic en **[!UICONTROL Suplantar como]**. Utilice `ksaner` como nombre de usuario, seleccione la opción proporcionada y haga clic en **[!UICONTROL Aceptar]**.
1. Abra una página web de We.Retail en **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Edite la página. También puede acceder a `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` en un navegador para editar una página.

   Haga clic en **[!UICONTROL Alternar panel lateral]** en la esquina superior izquierda de la página.

1. Abra la pestaña [!UICONTROL Assets] y haga clic en **[!UICONTROL Iniciar sesión en los recursos conectados]**.
1. Proporcione las credenciales (`ksaner` como nombre de usuario y `password` como contraseña). Este usuario tiene permisos de creación en ambas implementaciones de [!DNL Experience Manager].
1. Busque el recurso que agregó a DAM. Los recursos remotos se muestran en el panel izquierdo. Filtre por imágenes o documentos y por tipos de documentos compatibles. Arrastre las imágenes a un componente `Image` y los documentos a un componente `Download`.

   Los recursos recuperados son de solo lectura en la implementación local [!DNL Sites]. Puede seguir utilizando las opciones proporcionadas por los componentes [!DNL Sites] para editar el recurso buscado. La edición por componentes no es destructiva.

   ![Opciones para filtrar tipos de documentos e imágenes al buscar recursos en DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: Opciones para filtrar tipos de documentos e imágenes al buscar recursos en DAM remoto.*

1. Se notifica al creador del sitio si se busca un recurso de forma asincrónica y si falla alguna tarea de recuperación. Durante la creación o incluso después de la creación, los autores pueden ver información detallada sobre las tareas de recuperación y los errores en la interfaz de usuario [trabajos asincrónicos](/help/sites-administering/asynchronous-jobs.md).

   ![Notificación sobre la captura asincrónica de recursos que se produce en segundo plano.](assets/assets_async_transfer_fails.png)

   *Figura: Notificación sobre la captura asincrónica de recursos que se produce en segundo plano.*

1. Al publicar una página, [!DNL Experience Manager] muestra una lista completa de los recursos que se utilizan en ella. Asegúrese de que los recursos remotos se recuperan correctamente en el momento de la publicación. Para comprobar el estado de cada recurso recuperado, consulte la interfaz de usuario [trabajos asincrónicos](/help/sites-administering/asynchronous-jobs.md) .

   >[!NOTE]
   >
   >Aunque no se recuperen uno o varios recursos remotos, la página se publicará. El componente que utiliza el recurso remoto se publica en blanco. El área de notificación [!DNL Experience Manager] muestra una notificación para los errores que se muestran en la página de trabajos asincrónicos.

>[!CAUTION]
>
>Una vez que se utilizan en una página web, cualquier persona que tenga permiso para acceder a la carpeta local puede buscar y utilizar los recursos remotos. Los recursos recuperados se almacenan en la carpeta local (`connectedassets` en el tutorial anterior). Los recursos también se pueden buscar y ver en el repositorio local mediante [!UICONTROL Buscador de contenido].

Los recursos recuperados se pueden usar como cualquier otro recurso local, pero los metadatos asociados no se pueden editar.

### Comprobar el uso de un recurso en las páginas web {#asset-usage-references}

[!DNL Experience Manager] permite a los usuarios de DAM comprobar todas las referencias a un recurso. Ayuda a comprender y administrar el uso de un recurso en [!DNL Sites] remoto y en recursos compuestos. Muchos autores de páginas web en la implementación [!DNL Experience Manager Sites] pueden utilizar un recurso en un [!DNL Assets] remoto en diferentes páginas web. Para simplificar la administración de recursos y no provocar referencias rotas, es importante que los usuarios de DAM comprueben el uso de un recurso en las páginas web locales y remotas. La pestaña [!UICONTROL Referencias] de la página [!UICONTROL Propiedades] de un recurso muestra las referencias locales y remotas del recurso.

Para ver y administrar referencias en la implementación [!DNL Assets] , siga estos pasos:

1. Seleccione un recurso en la consola [!DNL Assets] y haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas.
1. Haga clic en la pestaña **[!UICONTROL References]**. Consulte **[!UICONTROL Referencias locales]** para el uso del recurso en la implementación [!DNL Assets]. Consulte **[!UICONTROL Referencias remotas] para usar el recurso en la implementación [!DNL Sites] donde se recuperó el recurso mediante la funcionalidad Recursos conectados.

   ![Referencias remotas en la página Propiedades del recurso](assets/connected-assets-remote-reference.png)

1. Las referencias para las páginas [!DNL Sites] muestran el recuento total de referencias para cada [!DNL Sites] local. Puede tardar algún tiempo en encontrar todas las referencias y mostrar el número total de referencias.
1. La lista de referencias es interactiva y los usuarios de DAM pueden hacer clic en una referencia para abrir la página de referencia. Si por algún motivo no se pueden recuperar referencias remotas, se muestra una notificación que informa al usuario del error.
1. Los usuarios pueden mover o eliminar el recurso. Al mover o eliminar un recurso, el número total de referencias de todos los recursos o carpetas seleccionados se muestra en un cuadro de diálogo de advertencia. Al eliminar un recurso para el que aún no se muestran las referencias, se muestra un cuadro de diálogo de advertencia.

   ![forzar advertencia de eliminación](assets/delete-referenced-asset.png)

## Limitaciones y prácticas recomendadas {#tip-and-limitations}

* Para obtener información sobre el uso de los recursos, configure la funcionalidad [Insight de recursos](/help/assets/asset-insights.md) en la instancia [!DNL Sites] .

### Permisos y administración de recursos {#permissions-and-managing-assets}

* Los recursos locales no se sincronizan con los recursos originales en la implementación remota. Las ediciones, eliminaciones o revocaciones de permisos en la implementación de DAM no se propagan de forma descendente.
* Los recursos locales son copias de solo lectura. [!DNL Experience Manager]Los componentes de realizan ediciones no destructivas en los recursos. No se permiten otras ediciones.
* Los recursos recuperados localmente solo están disponibles para la creación. Los flujos de trabajo de actualización de recursos no se pueden aplicar y los metadatos no se pueden editar.
* Solo se admiten las imágenes y los formatos de documento enumerados. [!DNL Content Fragments] y no  [!DNL Experience Fragments] son compatibles.
* [!DNL Experience Manager] no recupera los esquemas de metadatos. Significa que es posible que no se muestren todos los metadatos recuperados. Si el esquema se actualiza por separado en la implementación [!DNL Sites] , se muestran todas las propiedades de los metadatos.
* Todos los autores [!DNL Sites] tienen permisos de lectura en las copias recuperadas, incluso si los autores no pueden acceder a la implementación remota de DAM.
* No se admiten las API para personalizar la integración.
* La funcionalidad admite la búsqueda y el uso ininterrumpidos de recursos remotos. Para que varios recursos remotos estén disponibles en la implementación local, considere migrar los recursos. Consulte [Guía de migración de recursos](assets-migration-guide.md).
* No es posible utilizar un recurso remoto como una miniatura de página en la interfaz de usuario [!UICONTROL Propiedades de página]. Puede establecer una miniatura de una página web en la interfaz de usuario [!UICONTROL Propiedades de página] desde la [!UICONTROL Miniatura] haciendo clic en [!UICONTROL Seleccionar imagen].

### Configuración y licencia {#setup-licensing}

* [!DNL Assets] se  [!DNL Adobe Managed Services] admite la implementación en .
* [!DNL Sites] puede conectarse a un único  [!DNL Assets] repositorio a la vez.
* Se requiere una licencia de [!DNL Assets] que funcione como repositorio remoto.
* Se requieren una o más licencias de [!DNL Sites] que funcionen como implementación de creación local.

### Uso {#usage}

* Los usuarios pueden buscar recursos remotos y arrastrarlos a la página local durante la creación. No se admite ninguna otra funcionalidad.
* La operación de recuperación expira al cabo de 5 segundos. Los autores pueden tener problemas para recuperar recursos, por ejemplo, si hay problemas de red. Los autores pueden volver a intentarlo arrastrando el recurso remoto de [!UICONTROL Buscador de contenido] a [!UICONTROL Editor de páginas].
* Las ediciones simples que no son destructivas y que se admiten mediante el componente `Image`, se pueden realizar en los recursos recuperados. Los recursos son de solo lectura.
* El único método para recuperar el recurso es arrastrarlo a una página. No hay compatibilidad con API ni otros métodos para recuperar un recurso y actualizarlo.
* Si se retiran activos del DAM, estos seguirán utilizándose en las páginas [!DNL Sites].
* Las entradas de referencia remotas de un recurso se recuperan asincrónicamente. Las referencias y el recuento total no son en tiempo real y puede haber alguna diferencia si un autor de Sites utiliza el recurso mientras un usuario de DAM está viendo la referencia. Los usuarios de DAM pueden actualizar la página e intentarlo de nuevo en unos minutos para obtener el recuento total.

## Solución de problemas {#troubleshoot}

Para solucionar errores comunes, siga estos pasos:

* Si no puede buscar recursos remotos desde el [!UICONTROL Buscador de contenido], asegúrese de que las funciones y los permisos necesarios estén establecidos.

* Es posible que un recurso recuperado del DAM remoto no se publique en una página web por uno o varios motivos. No existe en el servidor remoto, la falta de permisos adecuados para recuperarlo o el error de red pueden ser las razones. Asegúrese de que el recurso no se elimine del DAM remoto. Asegúrese de que se hayan establecido los permisos adecuados y de que se cumplan los requisitos previos. Vuelva a intentar agregar el recurso a la página y vuelva a publicar. Compruebe la [lista de trabajos asincrónicos](/help/sites-administering/asynchronous-jobs.md) si hay errores en la recuperación de recursos.

* Si no puede acceder a la implementación remota de DAM desde la implementación local [!DNL Sites], asegúrese de que las cookies entre sitios estén permitidas y de que [se haya configurado el ](/help/sites-administering/same-site-cookie-support.md) soporte para las cookies del mismo sitio. Si las cookies entre sitios están bloqueadas, es posible que las implementaciones de [!DNL Experience Manager] no se autentiquen. Por ejemplo, [!DNL Google Chrome] en modo Incognito puede bloquear las cookies de terceros. Para permitir cookies en el explorador [!DNL Chrome], haga clic en el icono &quot;ojo&quot; de la barra de direcciones, vaya a **Sitio que no funciona** > **Bloqueado**, seleccione la URL de DAM remoto y permita la cookie de token de inicio de sesión. Como alternativa, consulte [cómo habilitar cookies de terceros](https://support.google.com/chrome/answer/95647).

   ![Error de cookie en el navegador Chrome en modo Incognito](assets/chrome-cookies-incognito-dialog.png)

* Si no se recuperan las referencias remotas y se genera un mensaje de error, compruebe si la implementación [!DNL Sites] está disponible y compruebe si hay problemas de conectividad de red. Vuelva a intentarlo más tarde para comprobarlo. [!DNL Assets] la implementación intenta establecer conexión dos veces con la  [!DNL Sites] implementación y luego informa de un error.

   ![error al recuperar referencias remotas de recursos](assets/reference-report-failure.png)



