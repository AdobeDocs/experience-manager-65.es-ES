---
title: Importación y exportación de la configuración global
seo-title: Importación y exportación de la configuración global
description: Puede importar y exportar definiciones de plantillas de búsqueda y configuración global para Workspace.
seo-description: Puede importar y exportar definiciones de plantillas de búsqueda y configuración global para Workspace.
uuid: 8f1f210d-e850-4b2c-bb5a-942fa8299791
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 72fe5749-2fa2-442f-b679-7889faeafcac
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 0%

---


# Importación y exportación de configuración global {#importing-and-exporting-global-settings}

Puede importar y exportar definiciones de plantillas de búsqueda y configuración global para Workspace.

>[!NOTE]
>
>Flex Workspace está obsoleto para AEM versión de formularios.

Por ejemplo, puede pasar de un entorno de desarrollo a un entorno de producción exportando las definiciones de plantilla de búsqueda y la configuración global de un entorno e importándolos al otro.

Después de exportar el archivo de configuración global, puede modificar la configuración en un editor de texto o XML. Sin embargo, las únicas configuraciones que puede que desee editar son las de JChannelConnectionProperties, formViewOnly y SpecialRoutes. Para obtener más información, consulte [Configuración global de Workspace](importing-exporting-global-settings.md#workspace-global-settings).


>[!NOTE]
>
>Si cambia las propiedades de evento en el archivo de configuración global, debe reiniciar el servidor.

## Importar una definición de plantilla de búsqueda {#import-a-search-template-definition}

1. En la consola de administración, haga clic en Servicios > Espacio de trabajo > Administración global.
1. En el cuadro Importar definición de plantilla de búsqueda, haga clic en Elegir archivo y seleccione la plantilla de búsqueda. Solo puede importar definiciones de plantillas de búsqueda que se exportaron originalmente desde una instancia de Workspace.
1. Haga clic en Importar.

## Exportar una definición de plantilla de búsqueda {#export-a-search-template-definition}

1. En la página Administración global, en Exportar definición de plantilla de búsqueda, haga clic en Lista de todo.
1. En la lista de las plantillas de búsqueda, seleccione la plantilla que desee exportar.

   >[!NOTE]
   >
   >Puede seleccionar más de una plantilla, pero solo se exportará la última seleccionada.

1. Haga clic en Exportar y guarde el archivo en el equipo.

## Importar configuración global {#import-global-settings}

1. En la página Administración global, en Importar configuración global, haga clic en Elegir archivo y seleccione el archivo de configuración global. El archivo de configuración global debe tener formato XML.
1. Haga clic en Importar.

## Exportar configuración global {#export-global-settings}

1. En la página Administración global, en Exportar configuración global, haga clic en Exportar.
1. Guarde el archivo en el equipo.

## Configuración global del espacio de trabajo {#workspace-global-settings}

Puede modificar el archivo de configuración global; sin embargo, la única configuración que puede desear editar es la de JChannelConnectionProperties, formViewOnly y SpecialRoutes.

>[!NOTE]
>
>Flex Workspace está obsoleto para AEM versión de formularios.

El archivo de configuración global de Workspace incluye la siguiente configuración:

### configuración de SpecialRoutes {#specialroutes-settings}

La configuración *SpecialRoutes* especifica las propiedades de las rutas especiales, aprobar y denegar, en Workspace. En determinadas situaciones, los botones de estas rutas aparecen en las tarjetas de tarea de Workspace y el usuario puede seleccionarlas sin abrir el formulario. Puede modificar la configuración de SpecialRoutes en el archivo de configuración global para agregar nombres personalizados para aprobar y denegar o para crear rutas adicionales.

**client_especialRoutes_route_approved_style:** El nombre del estilo que se encuentra en el tema de Workspace, que identifica los iconos del botón de aprobación. El estilo debe incluir valores para un icono habilitado y un icono deshabilitado. Para definir un estilo para un botón personalizado, debe utilizar la siguiente plantilla:
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` El archivo CSS de Workspace está incrustado en el archivo space-topic.swf, que se encuentra en el archivo adobe-space-client.ear > adobe-Workspace-client.war. Para cambiar el aspecto de Workspace, debe volver a compilar el archivo space-topic.swf.

**client_especialRoutes_route_bold_names:** La variedad de cadenas que un usuario de Workbench puede utilizar para interpretarse como &quot;denigrar&quot;. Las cadenas distinguen entre mayúsculas y minúsculas. Por ejemplo, el valor predeterminado es deniega. Si el usuario de Workbench utiliza la palabra Denegar en un proceso, no se reconocerá la palabra. La palabra Denegar debe agregarse a esta configuración para que el botón de ruta se pueda personalizar y se le aplique el estilo.

**client_especialRoutes_route_bold_style:** El nombre del estilo que se encuentra en el archivo de tema de Workspace, que identifica los iconos del botón de denegación. El estilo debe incluir valores para un icono habilitado y un icono deshabilitado. Para definir un estilo para un botón personalizado, debe utilizar la siguiente plantilla:
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_especialRoutes_route_approved_names:** La variedad de cadenas que un usuario de Workbench puede utilizar para interpretarse como &quot;aprobar&quot;. Las cadenas distinguen entre mayúsculas y minúsculas. Por ejemplo, el valor predeterminado es approved. Si el usuario de Workbench utiliza la palabra Aprobar en un proceso, no se reconocerá la palabra. La palabra Aprobar debe agregarse a esta configuración para que el botón de ruta se pueda personalizar y se le aplique el estilo.

**client_especialRoutes_names:** Las claves utilizadas para localizar el valor de cadena personalizado de los archivos de recursos. Cada entrada de esta configuración debe incluir los valores de los nombres y el estilo.

### Configuración de JGroup {#jgroup-settings}

Esta configuración solo aparece si ha actualizado desde Adobe LiveCycle ES 2.5 o anterior.

**server_remoteevents_ClientTimeoutMilliseconds:** el tiempo máximo que JGroup espera los mensajes de evento. No se debe cambiar esta configuración.

**server_remoteevents_ServerTimeoutMilliseconds:** El tiempo de espera para recibir mensajes JGroup en el servidor. Esta opción establece la demora para enviar mensajes del servidor al cliente.

**server_remoteevents_JChannelConnectionProperties:** las propiedades de conexión del grupo JG que se utilizan para comunicarse entre el servidor (en el que el servicio RemoteEvent procesa un evento de servicio) y todas las instancias de Workspace.

Es posible que deba cambiar los valores UDP para la dirección IP de multidifusión (mcast_addr), el puerto IP de multidifusión (mcast_port) y el TTL para los paquetes de multidifusión (ip_ttl). De forma predeterminada, la dirección IP de multidifusión y los valores de puerto se generan aleatoriamente y, por lo general, no es necesario cambiar los valores. Sin embargo, si su compañía tiene directivas de red con respecto a intervalos de multidifusión específicos para direcciones IP de multidifusión, es posible que tenga que cambiar los valores.

>[!NOTE]
>
>El TTL debe ser bueno al número de conmutadores de red entre los servidores del clúster; sin embargo, si el valor se establece demasiado alto, puede provocar que los paquetes de multidifusión se desplacen a subredes, donde se descartarán.

No se deben cambiar las propiedades restantes de esta configuración.

**server_remoteevents_JGroupName:** el nombre del grupo JG utilizado para la comunicación con evento remoto. Este valor se genera aleatoriamente para evitar conflictos en clústeres. Este valor no debe cambiarse.

Para obtener información adicional sobre JGroups y Workspace, consulte [JGroups and AEM forms Workspace - Explicated](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html).

### configuración de FormView {#formview-settings}

**client_formView_openFormInFullScreen:** para mostrar todos los formularios en Workspace en modo de pantalla completa, establezca esta opción en true. De forma predeterminada, esta opción se establece en false y los formularios no se muestran en modo de pantalla completa. Tenga en cuenta que el servicio Usuario contiene una opción para abrir el documento asociado con una tarea en modo de pantalla completa. Esto le permite controlar la visualización por proceso.

**client_route_formViewOnly:** Cuando se establece en True, las rutas no se muestran en la vista de tarjetas ni en la vista de listas en Workspace. El valor predeterminado es False, lo que significa que las rutas se muestran en la vista de tarjetas y en la vista de listas.

### Otras opciones {#other-settings}

**client_mimeTypes_openOutsideBrowser:** el tipo MIME de documentos que se abrirán fuera de la instancia del explorador de Workspace. Si los procesos de su organización requieren un tipo MIME adicional, especifíquelo aquí. Los valores predeterminados son:

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching:** almacena en caché una interfaz de usuario de tarea personalizada.

**server_debugLevel:** No cambie esta configuración.

**client_pollingInterval:** establece el intervalo de sondeo (en segundos) utilizado en Flex Workspace (obsoleto para formularios AEM en JEE) para detectar tareas nuevas y modificadas. El valor predeterminado es de 3 segundos. Esto no funciona para AEM Forms Workspace.

**client_systemContext_name:** especifique un nombre personalizado (por ejemplo, ciudadano) para mostrar en el campo Añadido por (en la ficha Archivos adjuntos) los datos adjuntos de una tarea en AEM Forms Workspace.

Para definir el nombre personalizado:

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>Para la aplicación Demo, el nombre para mostrar predeterminado es **Ciudadano**. Para una aplicación personalizada que cree, el nombre para mostrar predeterminado es **Cuenta de contexto del sistema**.
>
>**client_inactiveTimeout:** Cuando un usuario permanece inactivo durante un tiempo determinado, la sesión de AEM Forms Workspace caduca. Para habilitar la función, agregue una entrada a Configuración global &lt;client_ralentíTiempo de espera>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_ralentíTiempo de espera>. Puede especificar el valor 0 para deshabilitar el tiempo de espera de inactividad. La cantidad de tiempo se especifica en segundos.
