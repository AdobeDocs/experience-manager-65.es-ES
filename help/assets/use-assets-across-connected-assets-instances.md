---
title: Uso de recursos conectados para compartir recursos DAM en el flujo de trabajo de creación de sitios de Adobe Experience Manager
description: Utilice los recursos disponibles en una implementación remota de Recursos Adobe Experience Manager al crear sus páginas web en otra implementación de sitio de Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a7082bc47bea1b8514121f482911da44919da73c

---


# Uso de recursos conectados para compartir recursos de DAM en sitios de AEM {#use-connected-assets-to-share-dam-assets-in-aem-sites}

En las grandes empresas se puede distribuir la infraestructura necesaria para crear sitios web. A veces, las capacidades de creación de sitios web y los recursos digitales utilizados para crear estos sitios web pueden residir en diferentes implementaciones. Pueden darse algunas razones por las que las implementaciones distribuidas geográficamente son necesarias para trabajar en conjunto; las adquisiciones que conducen a una infraestructura heterogénea que la empresa matriz desea consolidar; crecimiento que conduce a tal escala que la instancia dedicada es necesaria para la administración de activos.

AEM Sites ofrece capacidades de crear páginas web, y AEM Assets es el sistema de gestión de recursos digitales (DAM) que proporciona los recursos necesarios para los sitios web. AEM ahora es compatible con el caso de uso anterior mediante la integración de AEM Sites y AEM Assets.

## Información general sobre los recursos conectados {#overview-of-connected-assets}

Al editar páginas en el Editor de páginas, los autores pueden buscar, examinar e incrustar recursos sin problemas desde una implementación de AEM Assets diferente. Para hacer esto, un administrador de AEM debe realizar una integración única de una implementación local de AEM Sites con una implementación diferente (remota) de AEM Assets.

Para los autores de Sitios, los recursos remotos están disponibles como recursos locales de solo lectura. La funcionalidad admite la búsqueda y el uso ininterrumpidos de algunos recursos remotos a la vez. Para que muchos recursos remotos estén disponibles en la implementación local en un solo uso, considere migrar los recursos de forma masiva. Consulte Guía [de migración de](/help/assets/assets-migration-guide.md)recursos.

### Requisitos previos e implementaciones admitidas {#prerequisites}

Antes de usar o configurar esta capacidad, asegúrese de lo siguiente:

* Los usuarios forman parte de los grupos de usuarios correspondientes en cada implementación.
* Para los tipos de implementación de Adobe Experience Manager, se cumple uno de los criterios admitidos. Recursos AEM 6.5 funciona con AEM como un servicio de nube. Para obtener más información, consulte Funcionalidad de Recursos [conectados en AEM como un servicio](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)de nube.

   |  | AEM Sites como Cloud Service | Sitios de AEM 6.5 en AMS | Sitios AEM 6.5 in situ |
   |---|---|---|---|
   | **AEM Assets como Cloud Service** | Admitido | Admitido | Admitido |
   | **AEM 6.5 Assets en AMS** | No admitido | Admitido | Admitido |
   | **Recursos AEM 6.5 in situ** | No admitido | No admitido | No admitido |

### Formatos de archivo admitidos {#mimetypes}

Los autores pueden buscar imágenes y los siguientes tipos de documentos en Content Finder y utilizar los recursos buscados en el Editor de páginas. Se pueden añadir documentos al componente y `Download` imágenes al `Image` componente. Los autores también pueden añadir recursos remotos en cualquier componente personalizado de AEM que extienda los componentes predeterminados `Download` o `Image` .

* Microsoft Word (DOC y DOCX)
* Microsoft Excel (XLS y XLSX)
* Microsoft PowerPoint (PPT y PPTX)
* Adobe PDF (PDF)
* Texto OpenDocument (ODT)
* Formato de texto enriquecido (RTF)
* Texto sin formato (TXT)
* Páginas Web (HTML)

### Users and groups involved {#users-and-groups-involved}

A continuación se describen las distintas funciones que se utilizan para configurar y utilizar la capacidad y sus grupos de usuarios correspondientes. El ámbito local se utiliza para el caso de uso en el que un autor crea una página web. El ámbito remoto se utiliza para la implementación de DAM que aloja los recursos necesarios. El autor de Sitios obtiene estos recursos remotos.

| Función | Ámbito | Grupo de usuarios | Nombre de usuario en la introducción | Requisito |
|----------------------------------|--------|------------------------------------------------------------------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Administrador de AEM Sites | Local | Administrador de AEM | `admin` | Configure AEM, configure la integración con la implementación remota de Recursos. |
| Usuario DAM | Local | Creación | `ksaner` | Se utiliza para ver y duplicar los recursos recuperados en `/content/DAM/connectedassets/`. |
| Autor de AEM Sites | Local | Autor (con acceso de lectura en el DAM remoto y acceso de autor en sitios locales) | `ksaner` | Los usuarios finales son autores de sitios que utilizan esta integración para mejorar la velocidad de contenido. Los autores buscan y exploran recursos en DAM remoto mediante Content Finder y utilizando las imágenes necesarias en las páginas web locales. Se utilizan las credenciales del usuario de `ksaner` DAM. |
| Administrador de AEM Assets | Remoto | Administrador de AEM | `admin` en AEM remoto | Configurar el uso compartido de recursos de origen cruzado (CORS). |
| Usuario DAM | Remoto | Creación | `ksaner` en AEM remoto | Función de autor en la implementación remota de AEM. Busque y examine recursos en Recursos conectados mediante el buscador de contenido. |
| Distribuidor DAM (usuario técnico) | Remoto | creadores de paquetes y creadores de sitios | `ksaner` en AEM remoto | Este usuario presente en la implementación remota lo utiliza el servidor local de AEM (no la función de autor del sitio) para recuperar los recursos remotos, en nombre del autor del sitio. Esta función no es la misma que las dos `ksaner` funciones anteriores y pertenece a un grupo de usuarios diferente. |

## Configurar una conexión entre las implementaciones Sitios y Recursos {#configure-a-connection-between-sites-and-assets-deployments}

Un administrador de AEM puede crear esta integración. Una vez creados, los permisos necesarios para utilizarlos se establecen mediante grupos de usuarios definidos en la implementación de Sitios y en la implementación de DAM.

Para configurar la conectividad de los recursos conectados y los sitios locales, siga estos pasos.

1. Acceda a una implementación existente de AEM Sites o cree una implementación con el siguiente comando:

   1. En la carpeta del archivo JAR, ejecute el siguiente comando en un terminal para crear cada servidor AEM.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Tras unos minutos, el servidor AEM se inicia correctamente. Considere esta implementación de AEM Sites como el equipo local para la creación de páginas web, por ejemplo, en `https://[local_sites]:4502`.

1. Asegúrese de que los usuarios y las funciones con ámbito local existan en la implementación de AEM Sites y en la implementación de AEM Assets en AMS. Cree un usuario técnico sobre la implementación de Recursos y añádalo al grupo de usuarios mencionado en [los usuarios y grupos involucrados](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Acceda a la implementación local de AEM Sites en `https://[local_sites]:4502`. Haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > Configuración **[!UICONTROL de recursos]** conectados y proporcione los siguientes valores:

   1. La ubicación de Recursos AEM es `https://[assets_servername_ams]:[port]`.
   1. Credenciales de un distribuidor DAM (usuario técnico).
   1. En el campo Punto **[!UICONTROL de]** montaje, introduzca la ruta de AEM local donde AEM obtiene los recursos. Por ejemplo, `remoteassets` carpeta.

   1. Ajuste los valores del Umbral **[!UICONTROL de optimización de transferencia binaria]** original en función de la red. Una representación de recursos con un tamaño mayor que este umbral se transfiere asincrónicamente.
   1. Seleccione Almacén **[!UICONTROL de datos compartido con recursos]** conectados, si utiliza un almacén de datos para almacenar los recursos y el almacén de datos es el almacenamiento común entre ambas implementaciones de AEM. En este caso, el límite de umbral no importa, ya que los binarios de activos reales residen en el almacén de datos y no se transfieren.
   ![Una configuración típica para recursos conectados](assets/connected-assets-typical-config.png)

   *Figura: Una configuración típica para recursos conectados*

1. Como los recursos ya se han procesado y se han recuperado las representaciones, deshabilite los iniciadores de flujo de trabajo. Ajuste las configuraciones del iniciador en la implementación local (AEM Sites) para excluir la `connectedassets` carpeta en la que se recuperan los recursos remotos.

   1. En la implementación de AEM Sites, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Iniciadores]**.

   1. Busque lanzadores con flujos de trabajo como **[!UICONTROL DAM Update Asset]** y **[!UICONTROL DAM Metadata Writback]**.

   1. Seleccione el iniciador del flujo de trabajo y haga clic en **[!UICONTROL Propiedades]** en la barra de acciones.

   1. En el asistente Propiedades, cambie los campos **[!UICONTROL Ruta]** como las asignaciones siguientes para actualizar sus expresiones regulares y excluir los recursos **[!UICONTROL conectados]** al punto de montaje.
   | Antes | Después |
   |---|---|
   | /content/dam(/(?!/subassets).)*/)representaciones/originales | /content/dam(/(?!/subassets)(?!connectedassets)).)*/)representaciones/originales |
   | /content/dam(/.*/)representaciones/originales | /content/dam(/(?!connectedassets)).*/)representaciones/originales |
   | /content/dam(/.*)/jcr:content/metadata | /content/dam(/(?!connectedassets)).*/)jcr:content/metadata |

   >[!NOTE]
   >
   >Todas las representaciones disponibles en la implementación remota de AEM se buscan cuando los autores buscan un recurso. Si desea crear más representaciones de un recurso buscado, omita este paso de configuración. El flujo de trabajo de recursos de actualización de DAM se activa y crea más representaciones. Estas representaciones solo están disponibles en la implementación local de Sitios y no en la implementación remota de DAM.

1. Agregue la instancia de AEM Sites como uno de los orígenes **** permitidos en la configuración CORS de AEM Assets remota.

   1. Inicie sesión con las credenciales del administrador. Busque Cross-Origin. Acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > Consola **** Web.

   1. Para crear una configuración CORS para una instancia de AEM Sites, haga clic en el icono ![aem_assets_add_icon](assets/aem_assets_add_icon.png) junto a la directiva **[!UICONTROL de uso compartido de recursos de origen cruzado de]** Adobe Granite.

   1. En el campo **[!UICONTROL Permitidos orígenes]**, introduzca la dirección URL de los sitios locales, es decir, `https://[local_sites]:[port]`. Guarde la configuración.

## Uso de recursos remotos {#use-remote-assets}

Los creadores del sitio web utilizan Content Finder para conectarse a la instancia de DAM. Los autores pueden examinar, buscar y arrastrar los recursos remotos de un componente. Para autenticarse en el DAM remoto, mantenga a mano las credenciales del usuario DAM proporcionadas por el administrador.

Los autores pueden utilizar los recursos disponibles en ambas instancias, DAM local y DAM remota, en una sola página web. Utilice Content Finder para cambiar entre buscar en el DAM local o en el DAM remoto.

Solo se buscan las etiquetas de recursos remotos que tienen una etiqueta correspondiente exacta (con la misma jerarquía de taxonomía) disponible en la instancia de sitios local. Todas las demás etiquetas se descartan. Los autores pueden buscar recursos remotos utilizando todas las etiquetas presentes en la implementación remota de AEM, ya que AEM ofrece una búsqueda de texto completo.

### Explicación del uso {#walk-through-of-usage}

Utilice la configuración anterior para probar la experiencia de creación y comprender cómo funciona la funcionalidad. Use documentos o imágenes de su elección en la implementación remota de DAM.

1. Vaya a la interfaz de usuario de Recursos en la implementación remota accediendo a **[!UICONTROL Recursos]** > **[!UICONTROL Archivos]** desde el espacio de trabajo de AEM. También puede acceder `https://[assets_servername_ams]:[port]/assets.html/content/dam` en un explorador. Cargue los recursos que desee.
1. En la instancia Sitios, en el activador de perfil en la esquina superior derecha, haga clic en **[!UICONTROL Suplantar como]**. Proporcione `ksaner` como nombre de usuario, seleccione la opción proporcionada y haga clic en **[!UICONTROL Aceptar]**.
1. Abra una página web de We.Retail en **[!UICONTROL Sitios]** > **[!UICONTROL We.Retail]** > **[!UICONTROL nosotros]** > **[!UICONTROL en]**. Edite la página. También puede acceder a `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` una página en un navegador para editarla.

   Haga clic en **[!UICONTROL Alternar panel]** lateral en la esquina superior izquierda de la página.

1. Abra la ficha Recursos y haga clic en **[!UICONTROL Iniciar sesión en Recursos]** conectados.
1. Proporcione las credenciales ( `ksaner` como nombre de usuario y `password` como contraseña). Este usuario tiene permisos de creación en ambas implementaciones de AEM.
1. Busque el recurso que ha agregado a DAM. Los recursos remotos se muestran en el panel izquierdo. Filtra para imágenes o documentos y filtre más para tipos de documentos admitidos. Arrastre las imágenes a un `Image` componente y los documentos a un `Download` componente.

   Los recursos recuperados son de solo lectura en la implementación local de AEM Sites. Puede seguir utilizando las opciones proporcionadas por los componentes de AEM Sites para editar el recurso buscado. La edición por componentes no es destructiva.

   ![Opciones para filtrar tipos de documentos e imágenes al buscar recursos en DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura:Opciones para filtrar tipos de documentos e imágenes al buscar recursos en DAM remoto*

1. Se notifica al autor del sitio si se busca un recurso de forma asincrónica y si falla alguna tarea de recuperación. Durante la creación o incluso después de la creación, los autores pueden ver información detallada sobre las tareas de recuperación y los errores en la interfaz de usuario de trabajos [](/help/assets/asynchronous-jobs.md) asincrónicos.

   ![Notificación sobre la captura asincrónica de recursos que se produce en segundo plano.](assets/assets_async_transfer_fails.png)

   *Figura:Notificación sobre la captura asincrónica de recursos que se produce en segundo plano.*

1. Al publicar una página, AEM muestra una lista completa de los recursos que se utilizan en ella. Asegúrese de que los recursos remotos se recuperan correctamente en el momento de la publicación. Para comprobar el estado de cada recurso buscado, consulte la interfaz de usuario de trabajos [asincrónicos](/help/assets/asynchronous-jobs.md) .

   >[!NOTE]
   >
   >Aunque no se recuperen uno o varios recursos remotos, la página se publicará. El componente que utiliza el recurso remoto se publica en blanco. El área de notificación de AEM muestra notificaciones de errores que se muestran en la página de trabajos asincrónicos.

>[!CAUTION]
>
>Una vez que se utilizan en una página web, los recursos remotos recuperados pueden ser buscados y utilizados por cualquier persona que tenga permiso para acceder a la carpeta local en la que se almacenan los recursos recuperados (`connectedassets` en el tutorial anterior). Los recursos también se pueden buscar y ver en el repositorio local mediante [!UICONTROL Content Finder].

Los recursos recuperados se pueden usar como cualquier otro recurso local, excepto que los metadatos asociados no se pueden editar.

## Restricciones  {#limitations}

**Permisos y administración de recursos**

* Los recursos locales no se sincronizan con los recursos originales de la implementación remota. Las ediciones, eliminaciones o revocación de permisos en la implementación de DAM no se propagan en la secuencia posterior.
* Los recursos locales son copias de solo lectura. Los componentes de AEM realizan ediciones no destructivas en los recursos. No se permiten otras ediciones.
* Los recursos recuperados localmente solo están disponibles para la creación. Los flujos de trabajo de actualización de recursos no se pueden aplicar y los metadatos no se pueden editar.
* Solo se admiten las imágenes y los formatos de documento enumerados. Los recursos de Dynamic Media, los fragmentos de contenido y los fragmentos de experiencia no son compatibles.
* No se buscan esquemas de metadatos.
* Todos los autores de sitios tienen permisos de lectura en las copias recuperadas, incluso si no tienen acceso a la implementación de DAM remota.
* No hay compatibilidad con API para personalizar la integración.
* La funcionalidad admite la búsqueda y el uso ininterrumpidos de recursos remotos. Para que muchos recursos remotos estén disponibles en la implementación local en un solo uso, considere la posibilidad de migrar los recursos. Consulte Guía [de migración de](assets-migration-guide.md)recursos.
* No es posible utilizar un recurso remoto como miniatura de página en la interfaz de usuario Propiedades [!UICONTROL de la] página. Puede establecer una miniatura de una página web en la interfaz de usuario Propiedades [!UICONTROL de] página desde la [!UICONTROL miniatura] haciendo clic en [!UICONTROL Seleccionar imagen].

**Configuración y licencia**

* Se admite la implementación de AEM Assets en AMS.
* AEM Sites puede conectarse a un único repositorio de Recursos AEM a la vez.
* Licencia de Recursos AEM que funciona como repositorio remoto.
* Una o varias licencias de AEM Sites que funcionan como implementación de creación local.

**Uso**

* Solo se admite la funcionalidad de buscar recursos remotos y arrastrar los recursos remotos de la página local para crear contenido.
* El tiempo de espera de la operación de captura finaliza al cabo de 5 segundos. Los autores pueden tener problemas para recuperar recursos, por ejemplo, si hay problemas de red. Los autores pueden volver a intentarlo arrastrando el recurso remoto desde [!UICONTROL Content Finder] al Editor [!UICONTROL de]páginas.
* Las ediciones simples que no son destructivas y que se admiten mediante el componente AEM `Image` , se pueden realizar en los recursos recuperados. Los recursos son de solo lectura.

## Solución de problemas {#troubleshoot}

Siga estos pasos para solucionar los problemas de los escenarios de error comunes:

* Si no puede buscar recursos remotos desde el Buscador de contenido, vuelva a comprobar y asegúrese de que las funciones y los permisos necesarios están establecidos.
* Es posible que un recurso recuperado de una presa remota no se publique en una página web por las siguientes razones: no existe en remoto; la falta de permisos adecuados para recuperarla; error de red. Asegúrese de que el recurso no se elimina del DAM remoto o de que los permisos no se modifican; garantizar que se cumplen los requisitos previos adecuados; vuelva a intentar agregar el recurso a la página y vuelva a publicar. Compruebe en la [lista de trabajos](/help/assets/asynchronous-jobs.md) asincrónicos si hay errores en la captura de recursos.
