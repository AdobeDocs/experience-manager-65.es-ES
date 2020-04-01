---
title: Utilice los recursos conectados para compartir recursos DAM en el flujo de trabajo de Adobe Experience Manager Sites
description: Utilice los recursos disponibles en una implementación remota de recursos de Adobe Experience Manager al crear sus páginas web en otra implementación de Experience Manager Sites.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 3c2c47b5d660fefd31470ce8d555c7bb949fa036

---


# Utilice los recursos conectados para compartir recursos de DAM en AEM Sites {#use-connected-assets-to-share-dam-assets-in-aem-sites}

En las grandes empresas se puede distribuir la infraestructura necesaria para crear sitios web. A veces, las capacidades de creación de sitios web y los recursos digitales utilizados para crear estos sitios web se pueden encontrar en diferentes implementaciones. Algunas razones pueden ser la distribución geográfica de las implementaciones existentes que se requieren para trabajar en conjunto o las adquisiciones que conducen a una infraestructura heterogénea que la compañía principal desea utilizar en conjunto.

AEM Sites ofrece capacidades de crear páginas web, y AEM Assets es el sistema de gestión de recursos digitales (DAM) que proporciona los recursos necesarios para los sitios web. AEM ahora es compatible con el caso de uso anterior mediante la integración de AEM Sites y AEM Assets.

## Información general sobre los recursos conectados {#overview-of-connected-assets}

Al editar páginas en el Editor de páginas, los creadores pueden buscar, examinar e incrustar recursos sin problemas desde una implementación diferente de AEM Assets. Para hacer esto, un administrador de AEM debe llevar a cabo una integración única de una implementación local de AEM Sites con una implementación diferente (remota) de AEM Assets.

Para los creadores de Sites, los recursos remotos están disponibles como recursos locales de solo lectura. La funcionalidad admite la búsqueda y el uso ininterrumpidos de algunos recursos remotos a la vez. Para que varios recursos remotos estén disponibles en la implementación local en un solo uso, considere migrar los recursos de forma masiva. Consulte [Guía de migración de recursos](/help/assets/assets-migration-guide.md).

### Requisitos previos e implementaciones admitidas {#prerequisites}

Antes de usar o configurar esta capacidad, asegúrese de lo siguiente:

* Los usuarios forman parte de los grupos correspondientes en cada implementación.
* Para los tipos de implementación de Adobe Experience Manager, se cumple uno de los criterios admitidos. Recursos AEM 6.5 funciona con AEM como un servicio de nube. Para obtener más información, consulte Funcionalidad de Recursos [conectados en AEM como un servicio](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)de nube.

   |  | AEM Sites as a Cloud Service | AEM 6.5 Sites en AMS | AEM 6.5 Sites local |
   |---|---|---|---|
   | **AEM Assets as a Cloud Service** | Compatible | Compatible | Compatible |
   | **AEM 6.5 Assets en AMS** | Compatible | Compatible | Compatible |
   | **AEM 6.5 Assets local** | No compatible | No compatible | No compatible |

### Formatos de archivo admitidos {#mimetypes}

Los creadores pueden buscar imágenes y los siguientes tipos de documentos en el buscador de contenido y utilizar los recursos buscados en el editor de páginas. Se pueden añadir documentos al componente `Download` e imágenes al componente `Image`. Los creadores también pueden agregar recursos remotos en cualquier componente personalizado de AEM que extienda los componentes predeterminados `Download` o `Image`. La lista de los formatos admitidos es:

* **Formatos** de imagen: Recursos conectados admiten los formatos de imagen admitidos por el componente [](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/image.html) Imagen. Las imágenes de Dynamic Media no se admiten.
* **Formatos de documento**: Consulte [Formatos de documento admitidos con recursos conectados](assets-formats.md#supported-document-formats).

### Usuarios y grupos implicados {#users-and-groups-involved}

A continuación se describen las distintas funciones que se usan para configurar y utilizar la capacidad y sus grupos de usuarios correspondientes. El ámbito local se utiliza para el caso de uso en el que un autor crea una página web. El ámbito remoto se utiliza para la implementación de DAM que aloja los recursos necesarios. El creador de Sites recupera los recursos remotos.

| Función | Ámbito | Grupo de usuarios | Nombre de usuario en la introducción | Requisito |
|----------------------------------|--------|------------------------------------------------------------------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Administrador de AEM Sites | Local | Administrador de AEM | `admin` | Establezca AEM y configure la integración con la implementación remota de recursos. |
| Usuario DAM | Local | Creación | `ksaner` | Se utiliza para ver y duplicar los recursos recuperados en `/content/DAM/connectedassets/`. |
| Creador de AEM Sites | Local | Creador (con acceso de lectura en el DAM remoto y acceso de creador en el Sites local) | `ksaner` | Los usuarios finales son creadores de Sites que utilizan esta integración para mejorar la velocidad de contenido. Los creadores buscan y exploran recursos en el DAM remoto mediante el buscador de contenido y utilizando las imágenes necesarias en las páginas web locales. Se utilizan las credenciales del usuario de DAM `ksaner`. |
| Administrador de AEM Assets | Remoto | Administrador de AEM | `admin` en AEM remoto | Configurar el intercambio de recursos de origen cruzado (CORS). |
| Usuario DAM | Remoto | Creación | `ksaner` en AEM remoto | Función de creador en la implementación remota de AEM. Busque y examine recursos en recursos conectados utilizando el buscador de contenido. |
| Distribuidor DAM (usuario técnico) | Remoto | creadores de paquetes y creadores de sitios | `ksaner` en AEM remoto | El servidor local de AEM (no la función de creador del sitio) utiliza al usuario presente en la implementación remota para recuperar los recursos remotos, en nombre del creador de Sites. Esta función no es la misma que las dos funciones `ksaner` anteriores y pertenece a un grupo de usuarios diferente. |

## Configurar una conexión entre las implementaciones de Sites y Assets {#configure-a-connection-between-sites-and-assets-deployments}

Un administrador de AEM puede crear esta integración. Una vez creada, los permisos necesarios para utilizarla se establece mediante grupos de usuarios definidos en la implementación de Sites y en la implementación de DAM.

Para configurar la conectividad de los recursos conectados y los sitios locales, siga estos pasos.

1. Acceda a una implementación existente de AEM Sites o cree una implementación con el siguiente comando:

   1. En la carpeta del archivo JAR, ejecute el siguiente comando en un terminal para crear cada servidor AEM.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Tras unos minutos, el servidor AEM se inicia correctamente. Piense en la implementación de AEM Sites como el equipo local para la creación de páginas web, por ejemplo, en `https://[local_sites]:4502`.

1. Asegúrese de que los usuarios y las funciones con ámbito local existan en la implementación de AEM Sites y en la implementación de AEM Assets en AMS. Cree un usuario técnico sobre la implementación de Assets y añádalo al grupo de usuarios mencionado en los [usuarios y grupos involucrados](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Acceda a la implementación local de AEM Sites en `https://[local_sites]:4502`. Haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Configuración de recursos conectados]** y proporcione los siguientes valores:

   1. La ubicación de AEM Assets es `https://[assets_servername_ams]:[port]`.
   1. Credenciales de un distribuidor DAM (usuario técnico).
   1. En el campo **[!UICONTROL Punto de montaje]**, introduzca la ruta local de AEM donde AEM recupera los recursos. Por ejemplo, la carpeta `remoteassets`.

   1. Ajuste los valores del **[!UICONTROL umbral de optimización de transferencia binaria original]** en función de la red. Las representaciones de recursos superiores a este umbral se transfieren de forma asíncrona.
   1. Seleccione **[!UICONTROL almacén de datos compartido con recursos conectados]**, si utiliza un almacén de datos para almacenar los recursos y este es el almacenamiento común entre ambas implementaciones de AEM. En este caso, el límite de umbral no importa, ya que los binarios de activos reales se encuentran en el almacén de datos y no se transfieren.
   ![Una configuración típica para los recursos conectados](assets/connected-assets-typical-config.png)

   *Figura: Una configuración típica para los recursos conectados*

1. Dado que los recursos ya se han procesado y se han recuperado las representaciones, deshabilite los iniciadores del flujo de trabajo. Ajuste las configuraciones del iniciador en la implementación local (AEM Sites) para excluir la carpeta `connectedassets`, en la que se recuperan los recursos remotos.

   1. En la implementación de AEM Sites, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Iniciadores]**.

   1. Busque iniciadores con flujos de trabajo como **[!UICONTROL Recurso de actualización DAM]** y **[!UICONTROL Reescritura de metadatos DAM]**.

   1. Seleccione el iniciador del flujo de trabajo y haga clic en **[!UICONTROL Propiedades]** en la barra de acciones.

   1. En el asistente Propiedades, cambie los campos **[!UICONTROL Ruta]** como las asignaciones siguientes para actualizar sus expresiones regulares y excluir **[!UICONTROL connectedassets]**.
   | Antes | Después |
   |---|---|
   | /content/dam(/((?!/subassets).)*/)renditions/original | /content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original |
   | /content/dam(/.*/)renditions/original | /content/dam(/((?!connectedassets).)*/)renditions/original |
   | /content/dam(/.*)/jcr:content/metadata | /content/dam(/((?!connectedassets).)*/)jcr:content/metadata |

   >[!NOTE]
   >
   >Todas las representaciones disponibles en la implementación remota de AEM se buscan cuando los creadores recuperan un recurso. Si desea crear más representaciones de un recurso recuperado, omita este paso de configuración. El flujo de trabajo del recurso de actualización DAM se activa y crea más representaciones. Estas representaciones solo están disponibles en la implementación local de Sites y no en la implementación remota de DAM.

1. Agregue la instancia de AEM Sites como uno de los **[!UICONTROL orígenes permitidos]** en la configuración CORS de AEM Assets remota.

   1. Inicie sesión con las credenciales del administrador. Busque Origen cruzado. Acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.

   1. Para crear una configuración CORS para una instancia de AEM Sites, haga clic en el icono ![aem_assets_add_icon](assets/aem_assets_add_icon.png) junto a la **[!UICONTROL política de uso compartido de recursos de origen cruzado de Adobe Granite]**.

   1. En el campo **[!UICONTROL Orígenes permitidos]**, introduzca la dirección URL local de Sites, es decir, `https://[local_sites]:[port]`. Guarde la configuración.

## Uso de recursos remotos {#use-remote-assets}

Los creadores del sitio web utilizan el buscador de contenido para conectarse a la instancia de DAM. Los creadores pueden examinar, buscar y arrastrar los recursos remotos de un componente. Para autenticarse en el DAM remoto, conserve las credenciales del usuario DAM proporcionadas por el administrador.

Los creadores pueden utilizar los recursos disponibles en las instancias DAM local y DAM remota en una sola página web. Utilice el buscador de contenido para decidir si buscar en el DAM local o en el DAM remoto.

Solo se buscan las etiquetas de recursos remotos que tienen una etiqueta correspondiente exacta (con la misma jerarquía de taxonomía) disponible en la instancia local de Sites. Todas las demás etiquetas se descartan. Los creadores pueden buscar recursos remotos utilizando todas las etiquetas presentes en la implementación remota de AEM, ya que ofrece una búsqueda de texto completo.

### Introducción al uso {#walk-through-of-usage}

Utilice la configuración anterior para probar la experiencia de creación y comprender cómo se utiliza la funcionalidad. Utilice documentos o imágenes de su elección en la implementación remota de DAM.

1. Vaya a la interfaz de usuario de Recursos en la implementación remota accediendo a **[!UICONTROL Recursos]** > **[!UICONTROL Archivos]** desde el espacio de trabajo de AEM. También puede acceder a `https://[assets_servername_ams]:[port]/assets.html/content/dam` en un explorador. Cargue los recursos que desee.
1. En la instancia Sites, en el activador de perfil en la esquina superior derecha, haga clic en **[!UICONTROL Suplantar como]**. Utilice `ksaner` como nombre de usuario, seleccione la opción proporcionada y haga clic en **[!UICONTROL Aceptar]**.
1. Abra una página web de We.Retail en **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Edite la página. También puede acceder a `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` en un navegador para editar una página.

   Haga clic en **[!UICONTROL Alternar panel lateral]** en la esquina superior izquierda de la página.

1. Abra la pestaña Recursos y haga clic en **[!UICONTROL Iniciar sesión en recursos conectados]**.
1. Proporcione las credenciales (`ksaner` como nombre de usuario y `password` como contraseña). El usuario tiene permisos de creación en ambas implementaciones de AEM.
1. Busque el recurso que ha agregado a DAM. Los recursos remotos se muestran en el panel izquierdo. Filtre por imágenes o documentos y por tipos de documentos compatibles. Arrastre las imágenes a un componente `Image` y los documentos a un componente `Download`.

   Los recursos recuperados son de solo lectura en la implementación local de AEM Sites. Puede seguir utilizando las opciones proporcionadas por los componentes de AEM Sites para editar el recurso buscado. La edición por componentes no es destructiva.

   ![Opciones para filtrar tipos de documentos e imágenes al buscar recursos en DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: Opciones para filtrar tipos de documentos e imágenes al buscar recursos en DAM remoto*

1. Se notifica al creador del sitio si se busca un recurso de forma asincrónica y si falla alguna tarea de recuperación. Durante la creación o incluso después de esta, los creadores pueden ver información detallada sobre las tareas de recuperación y los errores en la interfaz de usuario de [trabajos asincrónicos](/help/assets/asynchronous-jobs.md).

   ![Notificación sobre la captura asincrónica de recursos que se produce en segundo plano.](assets/assets_async_transfer_fails.png)

   *Figura: Notificación sobre la captura asincrónica de recursos que se produce en segundo plano*

1. Al publicar una página, AEM muestra una lista completa de los recursos que se utilizan en ella. Asegúrese de que los recursos remotos se recuperan correctamente en el momento de la publicación. Para comprobar el estado de cada recurso recuperado, consulte la interfaz de usuario de [trabajos asincrónicos](/help/assets/asynchronous-jobs.md) .

   >[!NOTE]
   >
   >Aunque no se recuperen uno o varios recursos remotos, la página se publicará. El componente que utiliza el recurso remoto se publica en blanco. El área de notificación de AEM muestra notificaciones de errores que se muestran en la página de trabajos asincrónicos.

>[!CAUTION]
>
>Una vez que se utilizan en una página web, cualquier persona que tenga permiso para acceder a la carpeta local en la que se almacenan los recursos recuperados puede acceder y utilizar los recursos remotos (`connectedassets` en el tutorial anterior). Los recursos también se pueden buscar y ver en el repositorio local mediante [!UICONTROL Buscador de contenido].

Los recursos recuperados se pueden usar como cualquier otro recurso local, pero los metadatos asociados no se pueden editar.

## Restricciones     {#limitations}

**Permisos y administración de recursos**

* Los recursos locales no se sincronizan con los recursos originales en la implementación remota. Las ediciones, eliminaciones o revocaciones de permisos en la implementación de DAM no se propagan de forma descendente.
* Los recursos locales son copias de solo lectura. Los componentes de AEM realizan ediciones no destructivas en los recursos. No se permiten otras ediciones.
* Los recursos recuperados localmente solo están disponibles para la creación. Los flujos de trabajo de actualización de recursos no se pueden aplicar y los metadatos no se pueden editar.
* Solo se admiten las imágenes y los formatos de documento enumerados. Los recursos de Dynamic Media, los fragmentos de contenido y los fragmentos de experiencia no son admitidos.
* No se recuperan los esquemas de metadatos.
* Todos los creadores de Sites tienen permisos de lectura en las copias recuperadas, incluso si no tienen acceso a la implementación de DAM remota.
* No se admiten las API para personalizar la integración.
* La funcionalidad admite la búsqueda y el uso ininterrumpidos de recursos remotos. Para que varios recursos remotos estén disponibles en la implementación local, considere migrar los recursos. Consulte [Guía de migración de recursos](assets-migration-guide.md).
* No es posible utilizar un recurso remoto como miniatura de página en la interfaz de usuario Propiedades [!UICONTROL de la] página. Puede establecer una miniatura de una página web en la interfaz de usuario Propiedades [!UICONTROL de] página desde la [!UICONTROL miniatura] haciendo clic en [!UICONTROL Seleccionar imagen].

**Configuración y licencia**

* Se admite la implementación de AEM Assets en AMS.
* AEM Sites puede conectarse a un único repositorio de AEM Assets a la vez.
* Licencia de AEM Assets como repositorio remoto.
* Una o varias licencias de AEM Sites que funcionan como una implementación de creación local.

**Uso**

* Solo se admite la funcionalidad de buscar recursos remotos y arrastrarlos a la página local para crear contenido.
* La operación de recuperación expira al cabo de 5 segundos. Los creadores pueden tener problemas para recuperar recursos, por ejemplo, si hay problemas de red. Los creadores pueden volver a intentarlo arrastrando el recurso remoto desde [!UICONTROL Buscador de contenido] al [!UICONTROL Editor de páginas].
* Las ediciones simples que no son destructivas y que se admiten mediante el componente AEM `Image`, se pueden realizar en los recursos recuperados. Los recursos son de solo lectura.

## Solución de problemas {#troubleshoot}

Siga estos pasos para solucionar los problemas de los escenarios de error comunes:

* Si no puede buscar recursos remotos desde el Buscador de contenido, vuelva a comprobar y asegúrese de que las funciones y los permisos necesarios estén establecidos.
* Puede que un recurso recuperado de un DAM remoto no se publique en una página web por las siguientes razones: no existe en remoto; falta de permisos adecuados para recuperarla; error de red. Asegúrese de que no se elimine el recurso del DAM remoto o de que los permisos no se modifiquen. Garantice que se cumplan los requisitos previos adecuados. Vuelva a intentar agregar el recurso a la página y vuelva a publicar. Compruebe la [lista de trabajos asincrónicos](/help/assets/asynchronous-jobs.md) si hay errores en la recuperación de recursos.
