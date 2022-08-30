---
title: Utilice los recursos conectados para compartir recursos de DAM en [!DNL Sites]
description: Usar recursos disponibles en un sitio remoto [!DNL Adobe Experience Manager Assets] implementación al crear las páginas web en otro [!DNL Adobe Experience Manager Sites] implementación.
contentOwner: AK
mini-toc-levels: 2
role: User, Admin, Leader
feature: Connected Assets,User and Groups
exl-id: 4ceb49d8-b619-42b1-81e7-c3e83d4e6e62
source-git-commit: e3caa3e3067cf5e29cfcdf4286047eb346aefa23
workflow-type: tm+mt
source-wordcount: '3803'
ht-degree: 18%

---

# Utilice los recursos conectados para compartir recursos de DAM en [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/use-assets-across-connected-assets-instances.html?lang=en) |
| AEM 6.5 | Este artículo |


En las grandes empresas se puede distribuir la infraestructura necesaria para crear sitios web. A veces, las capacidades de creación de sitios web y los recursos digitales utilizados para crear estos sitios web se pueden encontrar en diferentes implementaciones. Una razón puede ser la distribución geográfica de implementaciones existentes que son necesarias para trabajar juntas. Otra razón puede ser que las adquisiciones conducen a una infraestructura heterogénea, incluyendo diferentes [!DNL Experience Manager] versiones, que la empresa principal desea utilizar juntos.

La funcionalidad Recursos conectados admite los casos de uso anteriores mediante la integración de [!DNL Experience Manager Sites] y [!DNL Experience Manager Assets]. Los usuarios pueden crear páginas web en [!DNL Sites] que utilizan recursos digitales de una [!DNL Assets] implementaciones.

>[!NOTE]
>
>Configure los recursos conectados solo cuando necesite utilizar los recursos disponibles en una implementación remota de DAM en una implementación independiente de Sites para crear páginas web.

## Información general sobre los recursos conectados {#overview-of-connected-assets}

Al editar páginas en [!UICONTROL Editor de página] como destino, los autores pueden buscar, examinar e incrustar recursos sin problemas desde un [!DNL Assets] implementación que actúa como fuente de recursos. Los administradores crean una integración única de una implementación de [!DNL Experience Manager] con [!DNL Sites] con otra implementación de [!DNL Experience Manager] con [!DNL Assets] capacidad. Los creadores del sitio también pueden utilizar imágenes de Dynamic Media en las páginas web de su sitio a través de los recursos conectados y aprovechar las funcionalidades de Dynamic Media, como los ajustes preestablecidos de imagen y recorte inteligente.

Para la variable [!DNL Sites] autores, los recursos remotos están disponibles como recursos locales de solo lectura. La funcionalidad admite la búsqueda y el acceso ininterrumpidos a los recursos remotos en el Editor de sitios. Para cualquier otro caso de uso que requiera que el cuerpo completo de recursos esté disponible en Sitios, considere migrar los recursos de forma masiva en lugar de utilizar Recursos conectados. Consulte [Guía de migración de Experience Manager Assets](/help/assets/assets-migration-guide.md).

### Requisitos previos e implementaciones admitidas {#prerequisites}

Antes de usar o configurar esta capacidad, asegúrese de lo siguiente:

* Los usuarios forman parte de los grupos de usuarios correspondientes en cada implementación.
* Para [!DNL Adobe Experience Manager] tipos de implementación, se cumple uno de los criterios admitidos. [!DNL Experience Manager] 6,5 [!DNL Assets] funciona con [!DNL Experience Manager] as a Cloud Service. Para obtener más información sobre cómo funciona esta funcionalidad, consulte [!DNL Experience Manager] como [!DNL Cloud Service], consulte [Recursos conectados en Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Sites] as a [!DNL Cloud Service] | [!DNL Experience Manager] 6,5 [!DNL Sites] en AMS | [!DNL Experience Manager] 6,5 [!DNL Sites] local |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]como[!DNL Cloud Service]** | Compatible | Compatible | Compatible |
   | **[!DNL Experience Manager]6,5 [!DNL Assets] en AMS** | Compatible | Compatible | Compatible |
   | **[!DNL Experience Manager]6,5 [!DNL Assets] local** | No compatible | No compatible | No compatible |

### Formatos de archivo compatibles {#mimetypes}

Los autores buscan imágenes y los siguientes tipos de documentos en el buscador de contenido y arrastran los recursos buscados en el editor de páginas. Los documentos se añaden al `Download` componente e imágenes a la variable `Image` componente. Los autores también pueden añadir recursos remotos en cualquier [!DNL Experience Manager] componente que amplía el valor predeterminado `Download` o `Image` componentes. Los formatos admitidos son:

* **Formatos de imagen**: Los formatos que la variable [Componente de imagen](assets-formats.md#supported-raster-image-formats) admite .
* **Formatos de documento**: Consulte la [formatos de documento compatibles](assets-formats.md#supported-document-formats).

### Usuarios y grupos implicados {#users-and-groups-involved}

A continuación se describen las distintas funciones que se usan para configurar y utilizar la capacidad y sus grupos de usuarios correspondientes. El ámbito local se utiliza para el caso de uso en el que un autor crea una página web. El ámbito remoto se utiliza para la implementación de DAM que aloja los recursos necesarios. La variable [!DNL Sites] author recupera estos recursos remotos.

| Función | Ámbito | Grupo de usuarios | Nombre de usuario en la introducción | Descripciones |
|---|---|---|---|---|
| [!DNL Sites] administrador | Local | [!DNL Experience Manager] `administrators` | `admin` | Configuración [!DNL Experience Manager] y configurar la integración con el [!DNL Assets] implementación. |
| Usuario DAM | Local | `Authors` | `ksaner` | Se utiliza para ver y duplicar los recursos recuperados en `/content/DAM/connectedassets/`. |
| [!DNL Sites] author | Local | <ul><li>`Authors` (con acceso de lectura en el DAM remoto y acceso de autor en el [!DNL Sites]) </li> <li>`dam-users` en local [!DNL Sites]</li></ul> | `ksaner` | Los usuarios finales son [!DNL Sites] autores que utilizan esta integración para mejorar la velocidad de contenido. Los autores buscan y exploran recursos en el DAM remoto mediante [!UICONTROL Buscador de contenido] y utilizando las imágenes necesarias en páginas web locales. Se utilizan las credenciales del usuario de DAM `ksaner`. |
| [!DNL Assets] administrador | Remoto | [!DNL Experience Manager] `administrators` | `admin` en remoto [!DNL Experience Manager] | Configurar el intercambio de recursos de origen cruzado (CORS). |
| Usuario DAM | Remoto | `Authors` | `ksaner` en remoto [!DNL Experience Manager] | Función de autor en el remoto [!DNL Experience Manager] implementación. Busque y examine los recursos en los recursos conectados mediante la [!UICONTROL Buscador de contenido]. |
| Distribuidor DAM (usuario técnico) | Remoto | [!DNL Sites] `Authors` | `ksaner` en remoto [!DNL Experience Manager] | Este usuario presente en la implementación remota lo utiliza [!DNL Experience Manager] servidor local (no el [!DNL Sites] función de autor) para recuperar los recursos remotos, en nombre de [!DNL Sites] autor. Esta función no es la misma que las dos funciones `ksaner` anteriores y pertenece a un grupo de usuarios diferente. |

### Arquitectura de recursos conectados {#connected-assets-architecture}

El Experience Manager le permite conectar una implementación remota de DAM como fuente a varios Experience Manager [!DNL Sites] implementaciones. Puede conectar un máximo de cuatro [!DNL Sites] implementaciones en un DAM remoto de origen. Sin embargo, puede conectar un [!DNL Sites] implementación con solo una implementación remota de DAM.

Los siguientes diagramas ilustran los escenarios admitidos:

![Arquitectura de recursos conectados](assets/connected-assets-architecture.png)

El diagrama siguiente ilustra un escenario no admitido:

![Arquitectura de recursos conectados](assets/connected-assets-architecture-unsupported.png)

## Configurar una conexión entre [!DNL Sites] y [!DNL Assets] implementaciones {#configure-a-connection-between-sites-and-assets-deployments}

Un [!DNL Experience Manager] puede crear esta integración. Una vez creados, los permisos necesarios para utilizarlos se establecen mediante grupos de usuarios. Los grupos de usuarios se definen en la variable [!DNL Sites] implementación y en la implementación de DAM.

Para configurar los recursos conectados y locales [!DNL Sites] conectividad, siga estos pasos:

1. Acceso a una [!DNL Sites] despliegue o cree una implementación con el siguiente comando:

   1. En la carpeta del archivo JAR, ejecute el siguiente comando en un terminal para crear cada [!DNL Experience Manager] servidor.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Después de unos minutos, la variable [!DNL Experience Manager] el servidor se inicia correctamente. Tenga en cuenta lo siguiente: [!DNL Sites] implementación como equipo local para la creación de páginas web, por ejemplo, en `https://[local_sites]:4502`.

1. Asegúrese de que los usuarios y las funciones con el ámbito adecuado existan en la variable [!DNL Sites] implementación y [!DNL Assets] implementación en AMS. Crear un usuario técnico en [!DNL Assets] implementación y adición al grupo de usuarios mencionado en [usuarios y grupos implicados](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Acceda a la [!DNL Sites] implementación en `https://[local_sites]:4502`. Haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Configuración de recursos conectados]** y proporcione los siguientes valores:

   1. A **[!UICONTROL Título]** de la configuración.
   1. **[!UICONTROL URL de DAM remota]** es la dirección URL del [!DNL Assets] ubicación en el formato `https://[assets_servername]:[port]`.
   1. Credenciales de un distribuidor DAM (usuario técnico).
   1. En el **[!UICONTROL Punto de montaje]** , introduzca el [!DNL Experience Manager] ruta donde [!DNL Experience Manager] recupera los recursos. Por ejemplo, la carpeta `remoteassets`. Los recursos recuperados de DAM se almacenan en esta carpeta en la [!DNL Sites] implementación.
   1. **[!UICONTROL URL de sitios locales]** es la ubicación de la variable [!DNL Sites] implementación. [!DNL Assets] la implementación utiliza este valor para mantener referencias a los recursos digitales recuperados mediante esta [!DNL Sites] implementación.
   1. Credenciales de [!DNL Sites] usuario técnico.
   1. El valor de **[!UICONTROL Umbral de optimización de transferencia binaria original]** El campo especifica si los recursos originales (incluidas las representaciones) se transfieren sincrónicamente o no. Los recursos con un tamaño de archivo más pequeño se pueden recuperar fácilmente, mientras que los recursos con un tamaño de archivo relativamente mayor se sincronizan mejor asincrónicamente. El valor depende de las capacidades de red.
   1. Select **[!UICONTROL Almacén de datos compartido con recursos conectados]**, si utiliza un almacén de datos para almacenar los recursos y este se comparte entre ambas implementaciones. En este caso, el límite de umbral no importa, ya que los binarios de activos reales están disponibles en el almacén de datos y no se transfieren.

   ![Una configuración típica para la funcionalidad de los recursos conectados](assets/connected-assets-typical-config.png)

   *Figura: Una configuración típica para la funcionalidad Recursos conectados.*

1. Los recursos digitales existentes en [!DNL Assets] la implementación ya se ha procesado y se han generado las representaciones. Estas representaciones se recuperan mediante esta funcionalidad, por lo que no es necesario volver a generar las representaciones. Deshabilite los iniciadores del flujo de trabajo para evitar la regeneración de las representaciones. Ajuste las configuraciones del iniciador en el ([!DNL Sites]) para excluir la `connectedassets` (los recursos se recuperan en esta carpeta).

   1. Activado [!DNL Sites] implementación, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Lanzadores]**.

   1. Busque iniciadores con flujos de trabajo como **[!UICONTROL Recurso de actualización DAM]** y **[!UICONTROL Reescritura de metadatos DAM]**.

   1. Seleccione el lanzador del flujo de trabajo y haga clic en **[!UICONTROL Propiedades]** en la barra de acciones.

   1. En el [!UICONTROL Propiedades] , cambie la **[!UICONTROL Ruta]** campos como las asignaciones siguientes para actualizar sus expresiones regulares y excluir el punto de montaje **[!UICONTROL connectedassets]**.

   | Antes | Después |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Todas las representaciones disponibles en la implementación remota de se recuperan cuando los autores recuperan un recurso. Si desea crear más representaciones de un recurso recuperado, omita este paso de configuración. La variable [!UICONTROL Recurso de actualización DAM] el flujo de trabajo se activa y crea más representaciones. Estas representaciones solo están disponibles en el [!DNL Sites] implementación y no en la implementación remota de DAM.

1. Agregue la variable [!DNL Sites] implementación como origen permitido en la configuración de CORS en la variable [!DNL Assets] implementación. Para obtener más información, consulte [entender CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html).

1. Configurar [compatibilidad con cookies del mismo sitio](/help/sites-administering/same-site-cookie-support.md).

Puede comprobar la conectividad entre [!DNL Sites] implementaciones y [!DNL Assets] implementación.

![Prueba de conexión de los recursos conectados configurados [!DNL Sites]](assets/connected-assets-multiple-config.png)
*Figura: Prueba de conexión de los recursos conectados configurados [!DNL Sites].*

## Uso de recursos de Dynamic Media {#dynamic-media-assets}


Con los recursos conectados, puede utilizar recursos de imagen procesados por [!DNL Dynamic Media] desde la implementación remota de DAM en páginas de Sites, y aproveche las funcionalidades de Dynamic Media, como los ajustes preestablecidos de imagen y recorte inteligente.

Para usar [!DNL Dynamic Media] con recursos conectados:

1. Configurar [!DNL Dynamic Media] en la implementación remota de DAM con el modo de sincronización habilitado.
1. Configurar [Recursos conectados](#configure-a-connection-between-sites-and-assets-deployments).
1. Configurar [!DNL Dynamic Media] en la instancia Sites con el mismo nombre de empresa que se configura en el DAM remoto. La implementación Sitios debe tener acceso de solo lectura a la cuenta de Dynamic Media para trabajar con recursos conectados. Por lo tanto, asegúrese de desactivar el modo de sincronización en la configuración de Dynamic Media en la instancia de Sites.

>[!CAUTION]
>
>Con recursos conectados y [!DNL Dynamic Media] configuración, no puede utilizar [!DNL Dynamic Media] para procesar los recursos locales disponibles en la variable [!DNL Sites] implementación.

## Configuración de [!DNL Dynamic Media] {#configure-dynamic-media}

Para configurar [!DNL Dynamic Media] en [!DNL Assets] y [!DNL Sites] implementaciones:

1. Habilitar y configurar [!DNL Dynamic Media] como configuración global en remoto [!DNL Assets] implementación de autor. Para configurar Dynamic Media, consulte [Configuración de Dynamic Media](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services).
En remoto [!DNL Assets] implementación, en [!UICONTROL Modo de sincronización de Dynamic Media], seleccione **[!UICONTROL Habilitado de forma predeterminada]**.

1. Cree la configuración de los recursos conectados como se describe en [Configuración de la conexión entre las implementaciones de sitios y recursos](#configure-a-connection-between-sites-and-assets-deployments). También, seleccione **[!UICONTROL Recuperación de la representación original para los recursos conectados a Dynamic Media]** .

1. Configurar [!DNL Dynamic Media] en local [!DNL Sites] y remoto [!DNL Assets] implementaciones. Siga las instrucciones para [configure [!DNL Dynamic Media]](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services).

   * Utilice el mismo nombre de empresa en todas las configuraciones.
   * En local [!DNL Sites], en [!UICONTROL Modo de sincronización de Dynamic Media], seleccione **[!UICONTROL Deshabilitado de forma predeterminada]**. La variable [!DNL Sites] la implementación debe tener acceso de solo lectura al [!DNL Dynamic Media] cuenta.
   * En local [!DNL Sites], en el **[!UICONTROL Publicar recursos]** , seleccione **[!UICONTROL Publicación selectiva]**. No seleccione **[!UICONTROL Sincronizar todo el contenido]**.

1. Habilitar [[!DNL Dynamic Media] compatibilidad con el componente principal de imagen](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html#dynamic-media). Esta función habilita la opción predeterminada [Componente de imagen](https://www.aemcomponents.dev/content/core-components-examples/library/core-content/image.html) para mostrar [!DNL Dynamic Media] imágenes al [!DNL Dynamic Media] los autores utilizan las imágenes en las páginas web locales [!DNL Sites] implementación.

## Usar recursos remotos {#use-remote-assets}

Los creadores del sitio web utilizan el buscador de contenido para conectarse a la implementación de DAM. Los autores pueden examinar, buscar y arrastrar los recursos remotos de un componente. Para autenticarse en el DAM remoto, mantenga a mano las credenciales proporcionadas por su administrador (si las hay).

Los autores pueden utilizar los recursos disponibles en el DAM local y en la implementación remota de DAM, en una sola página web. Utilice el buscador de contenido para decidir si buscar en el DAM local o en el DAM remoto.

Solo se recuperan las etiquetas de recursos remotos que tienen una etiqueta correspondiente exacta junto con la misma jerarquía de taxonomía, disponible en el [!DNL Sites] implementación. Todas las demás etiquetas se descartan. Los autores pueden buscar recursos remotos utilizando todas las etiquetas presentes en el control remoto [!DNL Experience Manager] , ya que ofrece una búsqueda de texto completo.

### Introducción al uso {#walk-through-of-usage}

Utilice la configuración anterior para probar la experiencia de creación y comprender cómo se utiliza la funcionalidad. Utilice documentos o imágenes de su elección en la implementación remota de DAM.

1. Vaya a la [!DNL Assets] interfaz en la implementación remota accediendo a **[!UICONTROL Recursos]** > **[!UICONTROL Archivos]** from [!DNL Experience Manager] espacio de trabajo. También puede acceder a `https://[assets_servername_ams]:[port]/assets.html/content/dam` en un explorador. Cargue los recursos que desee.
1. En el [!DNL Sites] implementación, en el activador de perfil en la esquina superior derecha, haga clic en **[!UICONTROL Suplantar como]**. Utilice `ksaner` como nombre de usuario, seleccione la opción proporcionada y haga clic en **[!UICONTROL Aceptar]**.
1. Abra una página web de We.Retail en **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Edite la página. También puede acceder a `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` en un navegador para editar una página.

   Haga clic en **[!UICONTROL Alternar panel lateral]** en la esquina superior izquierda de la página.

1. Abra el [!UICONTROL Recursos] (Buscador de contenido remoto) y haga clic en **[!UICONTROL Iniciar sesión en los recursos conectados]**.
1. Proporcione las credenciales (`ksaner` como nombre de usuario y `password` como contraseña). Este usuario tiene permisos de creación en ambos [!DNL Experience Manager] implementaciones.
1. Busque el recurso que agregó a DAM. Los recursos remotos se muestran en el panel izquierdo. Filtre por imágenes o documentos y por tipos de documentos compatibles. Arrastre las imágenes a un componente `Image` y los documentos a un componente `Download`.

   Los recursos recuperados son de solo lectura en la variable local [!DNL Sites] implementación. Puede seguir utilizando las opciones proporcionadas por su [!DNL Sites] para editar el recurso buscado. La edición por componentes no es destructiva.

   ![Opciones para filtrar tipos de documentos e imágenes al buscar recursos en DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: Opciones para filtrar tipos de documentos e imágenes al buscar recursos en DAM remoto.*

1. Se notifica al autor del sitio si el original de un recurso se recupera de forma asíncrona y si falla alguna tarea de recuperación. Durante la creación o incluso después de la creación, los autores pueden ver información detallada sobre las tareas de recuperación y los errores en la sección [trabajos asincrónicos](/help/sites-administering/asynchronous-jobs.md) interfaz de usuario.

   ![Notificación sobre la captura asincrónica de recursos que se produce en segundo plano.](assets/assets_async_transfer_fails.png)

   *Figura: Notificación sobre la captura asincrónica de recursos que se produce en segundo plano.*

1. Al publicar una página, [!DNL Experience Manager] muestra una lista completa de los recursos que se utilizan en la página. Asegúrese de que los recursos remotos se recuperan correctamente en el momento de la publicación. Para comprobar el estado de cada recurso recuperado, consulte [trabajos asincrónicos](/help/sites-administering/asynchronous-jobs.md) interfaz de usuario.

   >[!NOTE]
   >
   >Aunque uno o varios recursos remotos no se recuperen completamente, la página se publicará. La variable [!DNL Experience Manager] área de notificación muestra una notificación de errores que se muestran en la página de trabajos asincrónicos.

>[!CAUTION]
>
>Una vez que se utilizan en una página web, cualquier persona que tenga permiso para acceder a la carpeta local puede buscar y utilizar los recursos remotos. Los recursos recuperados se almacenan en la carpeta local (`connectedassets` en la guía anterior). Los recursos también se pueden buscar y ver en el repositorio local mediante [!UICONTROL Buscador de contenido].

Los recursos recuperados se pueden usar como cualquier otro recurso local, pero los metadatos asociados no se pueden editar.

### Comprobar el uso de un recurso en las páginas web {#asset-usage-references}

[!DNL Experience Manager] permite a los usuarios de DAM comprobar todas las referencias a un recurso. Ayuda a comprender y administrar el uso de un recurso en remoto [!DNL Sites] y en activos compuestos. Muchos autores de páginas web en [!DNL Experience Manager Sites] la implementación puede utilizar un recurso en un [!DNL Assets] en diferentes páginas web. Para simplificar la administración de recursos y no provocar referencias rotas, es importante que los usuarios de DAM comprueben el uso de un recurso en las páginas web locales y remotas. La variable [!UICONTROL Referencias] en el [!UICONTROL Propiedades] lista las referencias locales y remotas del recurso.

Para ver y administrar referencias en la variable [!DNL Assets] implementación, siga estos pasos:

1. Seleccionar un recurso en [!DNL Assets] Consola y haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas.
1. Haga clic en **[!UICONTROL Referencias]** pestaña . Consulte **[!UICONTROL Referencias locales]** para el uso del recurso en la variable [!DNL Assets] implementación. Consulte **[!UICONTROL Referencias remotas] para el uso del recurso en [!DNL Sites] implementación en la que se recuperó el recurso mediante la funcionalidad Recursos conectados .

   ![Referencias remotas en la página Propiedades del recurso](assets/connected-assets-remote-reference.png)

1. Las referencias para [!DNL Sites] Las páginas muestran el recuento total de referencias para cada [!DNL Sites]. Puede tardar algún tiempo en encontrar todas las referencias y mostrar el número total de referencias.
1. La lista de referencias es interactiva y los usuarios de DAM pueden hacer clic en una referencia para abrir la página de referencia. Si por algún motivo no se pueden recuperar referencias remotas, se muestra una notificación que informa al usuario del error.
1. Los usuarios pueden mover o eliminar el recurso. Al mover o eliminar un recurso, el número total de referencias de todos los recursos o carpetas seleccionados se muestra en un cuadro de diálogo de advertencia. Al eliminar un recurso para el que aún no se han recuperado las referencias, se muestra un cuadro de diálogo de advertencia.

   ![forzar advertencia de eliminación](assets/delete-referenced-asset.png)

### Administrar actualizaciones de recursos en DAM remoto {#manage-updates-in-remote-dam}

Después [configuración de una conexión](#configure-a-connection-between-sites-and-assets-deployments) entre DAM remoto y [!DNL Sites] implementaciones, los recursos en DAM remoto están disponibles en la variable [!DNL Sites] implementación. A continuación, puede realizar las operaciones de actualización, eliminación, cambio de nombre y movimiento en los recursos o carpetas DAM remotos. Las actualizaciones, con algún retraso, están disponibles automáticamente en la variable [!DNL Sites] implementación. Además, si se utiliza un recurso en DAM remoto en una [!DNL Experience Manager Sites] , las actualizaciones del recurso en DAM remoto se muestran en la página [!DNL Sites] página.

Al mover un recurso de una ubicación a otra, asegúrese de que [ajustar referencias](/help/assets/manage-assets.md) para que el recurso se muestre en la [!DNL Sites] página. Si mueve un recurso a una ubicación a la que no se puede acceder desde la ubicación local [!DNL Sites] implementación, el recurso no se muestra en la implementación Sitios .

También puede actualizar las propiedades de metadatos de un recurso en DAM remoto y los cambios estarán disponibles en el [!DNL Sites] implementación.

[!DNL Sites] los autores pueden obtener una vista previa de las actualizaciones disponibles en el [!DNL Sites] implementación y, a continuación, vuelva a publicar los cambios para que estén disponibles en el [!DNL Experience Manager] publicar instancia.

[!DNL Experience Manager] muestra un indicador visual de estado caducado en los recursos de `Remote Assets Content Finder` para impedir que los autores del sitio utilicen el recurso en un [!DNL Sites] página. Si utiliza un recurso con un estado caducado en una [!DNL Sites] , el recurso no se muestra en la página [!DNL Experience Manager] publicar instancia.

>[!NOTE]
>
>Las actualizaciones de los recursos en DAM remoto están disponibles para la [!DNL Sites] implementación solo si es un DAM remoto y [!DNL Sites] implementaciones están activadas [!DNL Experience Manager].

## Preguntas frecuentes  {#frequently-asked-questions}

+++**Si necesita utilizar recursos disponibles en su [!DNL Sites] implementación?**

No es necesario configurar los recursos conectados en ese caso. Puede utilizar los recursos disponibles en la variable [!DNL Sites] implementación.

+++

+++**¿Cuándo necesita configurar la función Recursos conectados?**

Configure la función Recursos conectados solo cuando necesite utilizar los recursos disponibles en una implementación DAM remota en una [!DNL Sites] implementación.

+++

+++**Cuántos [!DNL Sites] las implementaciones pueden conectarse a una implementación de DAM remota después de configurar los recursos conectados?**

Puede conectar un máximo de cuatro [!DNL Sites] implementaciones en una implementación de DAM remota después de configurar los recursos conectados. Para obtener más información, consulte [Arquitectura de recursos conectados](#connected-assets-architecture).

+++

+++**Cuántas implementaciones remotas de DAM pueden conectarse a un [!DNL Sites] implementación después de configurar los recursos conectados?**

Puede conectar una implementación remota de DAM a un [!DNL Sites] después de configurar los recursos conectados. Para obtener más información, consulte [Arquitectura de recursos conectados](#connected-assets-architecture).

+++

+++**¿Puede utilizar los recursos de Dynamic Media desde su [!DNL Sites] implementación después de configurar los recursos conectados?**

Después de configurar los recursos conectados, [!DNL Dynamic Media] los recursos están disponibles en [!DNL Sites] implementación en modo de solo lectura. Como resultado, no puede usar [!DNL Dynamic Media] para procesar recursos en la variable [!DNL Sites] implementación. Para obtener más información, consulte [Configuración de una conexión entre las implementaciones de Sites y Dynamic Media](#dynamic-media-assets).

+++

+++**¿Puede utilizar recursos de tipos de formato de imagen y documento desde la implementación remota de DAM en la [!DNL Sites] implementación después de configurar los recursos conectados?**

Sí, puede utilizar recursos de tipos de formato de imagen y documento desde la implementación remota de DAM en la [!DNL Sites] después de configurar los recursos conectados.

+++

+++**¿Puede utilizar fragmentos de contenido y recursos de vídeo desde la implementación remota de DAM en la [!DNL Sites] implementación después de configurar los recursos conectados?**

No, no se pueden usar fragmentos de contenido y recursos de vídeo desde la implementación remota de DAM en [!DNL Sites] después de configurar los recursos conectados.

+++

+++**¿Puede utilizar recursos de Dynamic Media desde la implementación remota de DAM en la [!DNL Sites] implementación después de configurar los recursos conectados?**

Sí, puede configurar y utilizar recursos de imagen de Dynamic Media desde la implementación remota de DAM en la [!DNL Sites] después de configurar los recursos conectados. Para obtener más información, consulte [Configuración de una conexión entre las implementaciones de Sites y Dynamic Media](#dynamic-media-assets).

+++

+++**Después de configurar los recursos conectados, ¿puede realizar las operaciones de actualización, eliminación, cambio de nombre y movimiento en los recursos o carpetas DAM remotos?**

Sí, después de configurar los recursos conectados, puede realizar las operaciones de actualización, eliminación, cambio de nombre y movimiento en los recursos o carpetas DAM remotos. Las actualizaciones, con algún retraso, están disponibles automáticamente en la implementación de Sites. Para obtener más información, consulte [Administrar actualizaciones de recursos en DAM remoto](#handling-updates-to-remote-assets).

+++

+++**Después de configurar los recursos conectados, puede agregar o modificar recursos en su [!DNL Sites] implementación y haga que estén disponibles en la implementación remota de DAM?**

Puede agregar recursos al [!DNL Sites] sin embargo, estos recursos no se pueden poner a disposición de la implementación remota de DAM.

+++

## Limitaciones y prácticas recomendadas {#tip-and-limitations}

* Para obtener información sobre el uso de los recursos, configure la variable [Insight de recursos](/help/assets/asset-insights.md) en la función [!DNL Sites] instancia.

### Permisos y administración de recursos {#permissions-and-managing-assets}

* Los recursos locales son copias de solo lectura. [!DNL Experience Manager]Los componentes de realizan ediciones no destructivas en los recursos. No se permiten otras ediciones.
* Los recursos recuperados localmente solo están disponibles para la creación. Los flujos de trabajo de actualización de recursos no se pueden aplicar y los metadatos no se pueden editar.
* Solo se admiten las imágenes y los formatos de documento enumerados. [!DNL Content Fragments] y [!DNL Experience Fragments] no son compatibles.
* [!DNL Experience Manager] no recupera los esquemas de metadatos. Significa que es posible que no se muestren todos los metadatos recuperados. Si el esquema se actualiza por separado en la variable [!DNL Sites] implementación, se muestran todas las propiedades de metadatos.
* Todo [!DNL Sites] los autores tienen permisos de lectura en las copias recuperadas, incluso si los autores no pueden acceder a la implementación remota de DAM.
* No se admiten las API para personalizar la integración.
* La funcionalidad admite la búsqueda y el uso ininterrumpidos de recursos remotos. Para que varios recursos remotos estén disponibles en la implementación local, considere migrar los recursos. Consulte [Guía de migración de recursos](assets-migration-guide.md).
* No es posible utilizar un recurso remoto como una miniatura de página en [!UICONTROL Propiedades de página] interfaz de usuario. Puede establecer una miniatura de una página web en [!UICONTROL Propiedades de página] interfaz de usuario de [!UICONTROL Miniatura] haciendo clic en [!UICONTROL Seleccionar imagen].

### Configuración y licencia {#setup-licensing}

* [!DNL Assets] implementación en [!DNL Adobe Managed Services] es compatible.
* [!DNL Sites] puede conectarse a un [!DNL Assets] implementación a la vez.
* Una licencia de [!DNL Assets] se requiere trabajar como repositorio remoto.
* Una o más licencias de [!DNL Sites] funciona como implementación de creación local.

### Uso {#usage}

* Los usuarios pueden buscar recursos remotos y arrastrarlos a la página local durante la creación. No se admite ninguna otra funcionalidad.
* La operación de recuperación expira al cabo de 5 segundos. Los autores pueden tener problemas para recuperar recursos, por ejemplo, si hay problemas de red. Los autores pueden volver a probar arrastrando el recurso remoto desde [!UICONTROL Buscador de contenido] a [!UICONTROL Editor de página].
* Las ediciones simples que no son destructivas y que se admiten mediante el componente `Image`, se pueden realizar en los recursos recuperados. Los recursos son de solo lectura.
* El único método para recuperar el recurso es arrastrarlo a una página. No hay compatibilidad con API ni otros métodos para recuperar un recurso y actualizarlo.
* Si los activos se retiran del DAM, se siguen utilizando en [!DNL Sites] páginas.
* Las entradas de referencia remotas de un recurso se recuperan asincrónicamente. Las referencias y el recuento total no son en tiempo real y puede haber alguna diferencia si un autor de Sites utiliza el recurso mientras un usuario de DAM está viendo la referencia. Los usuarios de DAM pueden actualizar la página e intentarlo de nuevo en unos minutos para obtener el recuento total.

## Solución de problemas {#troubleshoot}

Para solucionar errores comunes, siga estos pasos:

* Si no puede buscar recursos remotos desde el [!UICONTROL Buscador de contenido]y, a continuación, asegúrese de que las funciones y los permisos necesarios estén establecidos.

* Es posible que un recurso recuperado del DAM remoto no se publique en una página web por uno o varios motivos. No existe en el servidor remoto, la falta de permisos adecuados para recuperarlo o el error de red pueden ser las razones. Asegúrese de que el recurso no se elimine del DAM remoto. Asegúrese de que se hayan establecido los permisos adecuados y de que se cumplan los requisitos previos. Vuelva a intentar agregar el recurso a la página y vuelva a publicar. Compruebe la [lista de trabajos asincrónicos](/help/sites-administering/asynchronous-jobs.md) si hay errores en la recuperación de recursos.

* Si no puede acceder a la implementación remota de DAM desde el [!DNL Sites] implementación, asegúrese de que se permiten cookies entre sitios y [compatibilidad con cookies del mismo sitio](/help/sites-administering/same-site-cookie-support.md) está configurado. Si las cookies entre sitios están bloqueadas, las implementaciones de [!DNL Experience Manager] no se puede autenticar. Por ejemplo, [!DNL Google Chrome] en el modo Incognito puede bloquear las cookies de terceros. Para permitir cookies en [!DNL Chrome] navegador, haga clic en el icono &quot;ojo&quot; de la barra de direcciones, vaya a **El sitio no funciona** > **Bloqueado**, seleccione la URL de DAM remota y permita la cookie de token de inicio de sesión. Como alternativa, consulte [cómo habilitar cookies de terceros](https://support.google.com/chrome/answer/95647).

   ![Error de cookie en el navegador Chrome en modo Incognito](assets/chrome-cookies-incognito-dialog.png)

* Si las referencias remotas no se recuperan y genera un mensaje de error, compruebe si [!DNL Sites] la implementación está disponible y compruebe si hay problemas de conectividad de red. Vuelva a intentarlo más tarde para comprobarlo. [!DNL Assets] la implementación intenta establecer conexión con [!DNL Sites] y luego informa de un error.

   ![error al recuperar referencias remotas de recursos](assets/reference-report-failure.png)



