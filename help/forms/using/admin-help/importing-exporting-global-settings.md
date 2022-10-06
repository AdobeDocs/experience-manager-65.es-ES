---
title: Importación y exportación de la configuración global
seo-title: Importing and exporting global settings
description: Puede importar y exportar definiciones de plantillas de búsqueda y configuración global para Workspace.
seo-description: You can import and export search template definitions and global settings for Workspace.
uuid: 8f1f210d-e850-4b2c-bb5a-942fa8299791
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 72fe5749-2fa2-442f-b679-7889faeafcac
exl-id: cdb7ff54-7891-45b1-a921-10b01ef5188d
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 0%

---

# Importación y exportación de la configuración global {#importing-and-exporting-global-settings}

Puede importar y exportar definiciones de plantillas de búsqueda y configuración global para Workspace.

>[!NOTE]
>
>Flex Workspace está en desuso para AEM versión de formularios.

Por ejemplo, puede pasar de un entorno de desarrollo a un entorno de producción exportando las definiciones de plantillas de búsqueda y la configuración global de un entorno e importándolas en el otro.

Después de exportar el archivo de configuración global, puede modificar la configuración en un editor de texto o XML. Sin embargo, los únicos ajustes que puede que desee editar son los ajustes JChannelConnectionProperties, formViewOnly y SpecialRoutes . Para obtener más información, consulte [Configuración global de Workspace](importing-exporting-global-settings.md#workspace-global-settings).


>[!NOTE]
>
>Si cambia las propiedades de evento en el archivo de configuración global, debe reiniciar el servidor.

## Importación de una definición de plantilla de búsqueda {#import-a-search-template-definition}

1. En la consola de administración, haga clic en Servicios > Workspace > Administración global.
1. En el cuadro Importar definición de plantilla de búsqueda, haga clic en Elegir archivo y seleccione la plantilla de búsqueda. Solo puede importar definiciones de plantillas de búsqueda que se exportaron originalmente desde una instancia de Workspace.
1. Haga clic en Importar.

## Exportación de una definición de plantilla de búsqueda {#export-a-search-template-definition}

1. En la página Administración global, en Exportar definición de plantilla de búsqueda, haga clic en Lista todo.
1. En la lista de plantillas de búsqueda, seleccione la plantilla que desea exportar.

   >[!NOTE]
   >
   >Puede seleccionar más de una plantilla, pero solo se exporta la última plantilla seleccionada.

1. Haga clic en Exportar y, a continuación, guarde el archivo en el equipo.

## Importar configuración global {#import-global-settings}

1. En la página Administración global, en Importar configuración global, haga clic en Elegir archivo y seleccione el archivo de configuración global. El archivo de configuración global debe estar en formato XML.
1. Haga clic en Importar.

## Exportar configuración global {#export-global-settings}

1. En la página Administración global, en Exportar configuración global, haga clic en Exportar.
1. Guarde el archivo en el equipo.

## Configuración global de Workspace {#workspace-global-settings}

Puede modificar el archivo de configuración global; sin embargo, los únicos ajustes que puede que desee editar son los ajustes JChannelConnectionProperties, formViewOnly y SpecialRoutes .

>[!NOTE]
>
>Flex Workspace está en desuso para AEM versión de formularios.

El archivo de configuración global de Workspace incluye la siguiente configuración:

### configuración de rutas especiales {#specialroutes-settings}

La variable *SpecialRoutes* la configuración especifica las propiedades de las rutas especiales, aprobar y denegar, en Workspace. En determinadas situaciones, los botones de estas rutas aparecen en las tarjetas de tareas de Workspace y el usuario puede seleccionarlos sin abrir el formulario. Puede modificar la configuración de SpecialRoutes en el archivo de configuración global para agregar nombres personalizados para aprobar y denegar o para crear rutas adicionales.

**client_SpecialRoutes_route_approve_style:** Nombre del estilo que se encuentra en el tema de Workspace, que identifica los iconos de botón de aprobación. El estilo debe incluir valores para un icono habilitado y un icono deshabilitado. Para definir un estilo para un botón personalizado, debe utilizar la siguiente plantilla:
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` El archivo CSS de Workspace está incrustado en el archivo workspace-theme.swf , que se encuentra en el archivo adobe-workspace-client.ear > adobe-workspace-client.war . Para cambiar el aspecto de Workspace, debe volver a compilar el archivo workspace-theme.swf .

**client_SpecialRoutes_route_deny_names:** La variedad de cadenas que un usuario de Workbench puede utilizar para interpretarse como &quot;denegado&quot;. Las cadenas distinguen entre mayúsculas y minúsculas. Por ejemplo, el valor predeterminado es deny. Si el usuario de Workbench utiliza la palabra Denegar en un proceso, la palabra no se reconocerá. La palabra Denegar debe agregarse a esta configuración para que el botón de ruta se personalice y se le aplique el estilo.

**client_SpecialRoutes_route_deny_style:** El nombre del estilo que se encuentra en el archivo de tema de Workspace, que identifica los iconos de botón denegar. El estilo debe incluir valores para un icono habilitado y un icono deshabilitado. Para definir un estilo para un botón personalizado, debe utilizar la siguiente plantilla:
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_SpecialRoutes_route_approve_names:** La variedad de cadenas que un usuario de Workbench puede utilizar para interpretarse como &quot;aprobar&quot;. Las cadenas distinguen entre mayúsculas y minúsculas. Por ejemplo, el valor predeterminado es approve. Si el usuario de Workbench utiliza la palabra Aprobar en un proceso, la palabra no se reconocerá. La palabra Aprobar debe agregarse a esta configuración para que el botón de ruta se personalice y se le aplique el estilo.

**client_SpecialRoutes_names:** Claves utilizadas para localizar el valor de cadena personalizado de los archivos de recursos. Cada entrada de esta configuración debe incluir los valores de los nombres y el estilo.

### Configuración de JGroup {#jgroup-settings}

Estos ajustes solo aparecen si ha actualizado desde el LiveCycle de Adobe ES 2.5 o anterior.

**server_remoteevents_ClientTimeoutMilliseconds:** El tiempo máximo que el grupo de informes espera para recibir mensajes de evento. Esta configuración no debe cambiarse.

**server_remoteevents_ServerTimeoutMilliseconds:** Tiempo de espera para recibir mensajes JGroup en el servidor. Esta opción establece la demora para enviar mensajes desde el servidor al cliente.

**server_remoteevents_JChannelConnectionProperties:** Las propiedades de conexión para el grupo JG que se utilizan para comunicarse entre el servidor (en el que el servicio RemoteEvent procesa un evento de servicio) y todas las instancias de Workspace.

Es posible que necesite cambiar los valores UDP para la dirección IP de multidifusión (mcast_addr), el puerto IP de multidifusión (mcast_port) y el TTL para los paquetes de multidifusión (ip_ttl). De forma predeterminada, la dirección IP de multidifusión y los valores de puerto se generan aleatoriamente y, por lo general, no es necesario cambiar los valores. Sin embargo, si su empresa tiene alguna política de red relacionada con rangos de multidifusión específicos para direcciones IP de multidifusión, es posible que tenga que cambiar los valores.

>[!NOTE]
>
>El TTL debe ser bueno que el número de conmutadores de red entre los servidores del clúster; sin embargo, si el valor es demasiado alto, puede causar que los paquetes de multidifusión viajen a subredes, donde se descartarán.

Las propiedades restantes de esta configuración no deben cambiarse.

**server_remoteevents_JGroupName:** Nombre del grupo JG utilizado para la comunicación de eventos remotos. Este valor se genera aleatoriamente para evitar conflictos en clústeres. Este valor no debe cambiarse.

<!--

For additional information on JGroups and Workspace, see [JGroups and AEM forms Workspace - Explained](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html).

-->

### configuración de formView {#formview-settings}

**client_formView_openFormInFullScreen:** Para mostrar todos los formularios en Workspace en modo de pantalla completa, establezca esta opción en true. De forma predeterminada, esta opción se establece en false y los formularios no se muestran en el modo de pantalla completa. Tenga en cuenta que el servicio Usuario contiene una opción para abrir el documento asociado a una tarea en modo de pantalla completa. Esto permite controlar la visualización por proceso.

**client_route_formViewOnly:** Cuando se establece en True, las rutas no se muestran en la vista de tarjeta ni en la vista de lista en Workspace. El valor predeterminado es False, lo que significa que las rutas se muestran en la vista de tarjeta y en la vista de lista.

### Otra configuración {#other-settings}

**client_mimeTypes_openOutsideBrowser:** Tipo MIME de los documentos que se abrirán fuera de la instancia del explorador de Workspace. Si los procesos de su organización requieren un tipo MIME adicional, especifíquelo aquí. Los valores predeterminados son:

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching:** Almacena en caché una interfaz de usuario de tarea personalizada.

**server_debugLevel:** No cambie esta configuración.

**client_pollingInterval:** Establece el intervalo de sondeo (en segundos) utilizado en Flex Workspace (obsoleto para AEM formularios en JEE) para detectar tareas nuevas y modificadas. El valor predeterminado es de 3 segundos. Esto no funciona para AEM Forms Workspace.

**client_systemContext_name:** Especifique un nombre personalizado (por ejemplo, Ciudadano) para que aparezca en el campo Agregado por (en la pestaña Archivos adjuntos) para los archivos adjuntos de una tarea en AEM Forms Workspace.

Para definir el nombre personalizado:

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>Para la aplicación Demostración, el nombre para mostrar predeterminado es **Ciudadano**. Para una aplicación personalizada que cree, el nombre para mostrar predeterminado es **Cuenta de contexto del sistema**.
>
>**client_idleTimeout:** Cuando un usuario permanece inactivo durante un tiempo determinado, la sesión de AEM Forms Workspace caduca. Para habilitar la función, agregue una entrada a Configuración global . &lt;client_idletimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_idletimeout>. Puede especificar el valor 0 para deshabilitar el tiempo de espera inactivo. La cantidad de tiempo se especifica en segundos.
