---
title: Importar y administrar archivos
seo-title: Import and manage archives
description: Aprenda a importar y administrar archivos.
seo-description: Learn how to import and manage archives.
uuid: aa1613dd-6350-49a7-9643-44365e2acdcc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b6f6463a-2ae4-43d2-8d16-cc20a954e50e
exl-id: 0c15677a-ee17-425e-a261-fb3ae8688eb2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 0%

---

# Importar y administrar archivos {#import-and-manage-archives}

Utilice la pestaña de archivos para importar y administrar las LCA creadas en Workbench.

## Importar un archivo {#import-an-archive}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones y haga clic en la pestaña Archivos.
1. Haga clic en Importar.
1. Haga clic en Examinar para localizar el archivo que desea importar y, a continuación, haga clic en Vista previa.
1. Revise la lista de recursos y objetos que se instalarán con el archivo. Asegúrese de que no haya conflictos con los recursos, objetos y configuraciones de servicio existentes, ya que no hay ninguna capacidad de deshacer disponible.

   Si selecciona importar las configuraciones de servicio, AEM forms importa todos los archivos de configuración de procesos (endpoints, perfiles de seguridad y parámetros de configuración de servicio) utilizados por los procesos en LCA.

1. Haga clic en Importar.
1. Revise los resultados de la importación y haga clic en Omitir configuración para finalizar el proceso de importación o haga clic en Configurar para configurar el archivo.

   >[!NOTE]
   >
   >Si hace clic en Omitir configuración, puede configurar el archivo más adelante.

1. Si hace clic en Configurar, aparecerá la página Configurar puntos de conexión, donde puede realizar los cambios que necesite:

   * Para cambiar el nombre de un extremo o editar su descripción, haga clic en él.
   * Para agregar un extremo de Administrador de tareas, haga clic en Agregar administrador de tareas. Para obtener más información sobre la configuración del Administrador de tareas, consulte [Configuración de los extremos del Administrador de tareas](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Para agregar un extremo de carpeta vigilada, haga clic en Agregar carpeta vigilada. Para obtener más información sobre la configuración de la carpeta vigilada, consulte [Configuración de extremo de carpeta vigilada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Para añadir un extremo de correo electrónico, haga clic en Añadir correo electrónico. Para obtener más información sobre la configuración del correo electrónico, consulte [Configuración de extremo de correo electrónico](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Para agregar un punto final de EJB, haga clic en Agregar EJB y especifique un nombre y una descripción para el punto final.
   * Para agregar un extremo SOAP, haga clic en Agregar SOAP y especifique un nombre y una descripción para el extremo.
   * Para agregar un extremo Remoting, haga clic en Agregar Remoting. Para obtener más información sobre la configuración de Remoting, consulte [Configuración de extremo remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Para agregar un extremo REST, haga clic en Agregar REST y especifique un nombre y una descripción para el extremo. Tenga en cuenta que la URL de invocación de REST se muestra en la página Agregar extremo de REST .
   * Para quitar un punto final, active la casilla que hay junto a él y haga clic en Quitar.

1. Haga clic en Siguiente.
1. Si un proceso o servicio de la LCA tiene parámetros de configuración, aparecerá una página Configurar parámetros, donde puede configurar los parámetros del servicio y hacer clic en Siguiente.
1. En la página Configurar perfil de seguridad , realice los cambios que necesite:

   * **Requerir que los llamadores se autentiquen:** Esta configuración indica si el servicio se puede invocar con o sin credenciales.

      If *Los llamadores deben autenticarse actualmente* se muestra, el llamador del servicio debe estar autenticado y el principal del usuario de la llamada debe estar autorizado a invocar el servicio; de lo contrario, se rechazará el intento de invocación. Para eliminar la necesidad de autenticarse, haga clic en Permitir llamadas no autenticadas.

      If *No es necesario que los llamadores se autentiquen* , el llamador del servicio no necesita ser autenticado. La invocación del servicio siempre se realizará correctamente porque no hay comprobación de autorización. Para requerir autenticación, haga clic en Requerir llamadas para autenticarse.

   * **Ejecutar como:** Especifica la identidad en tiempo de ejecución utilizada por un servicio después de invocarse. Para cambiar esta opción, haga clic en Cambiar. Elija entre las siguientes opciones:

      **No especificado:** Se utiliza el comportamiento predeterminado.

      **Invocador:** Utiliza la misma identidad que el usuario que invocó el servicio.

      **Sistema:** Ejecuta el servicio con privilegios completos. Esta es la configuración predeterminada para los procesos de larga duración.

      **Usuario con nombre:** Permite ejecutar el servicio como un usuario específico. Esta es la configuración predeterminada para los procesos de corta duración. Cuando seleccione esta opción, haga clic en Seleccionar usuario para mostrar la página Seleccionar principal, donde puede buscar y seleccionar al usuario.

   * Para agregar una entidad de seguridad al perfil de seguridad, haga clic en Agregar entidad de seguridad y seleccione el usuario o grupo que desee agregar como entidad de seguridad. Haga clic en Siguiente y, a continuación, seleccione los permisos que desea asignar a esta entidad de seguridad:

      **INVOKE_PERM:** Para invocar todas las operaciones en el servicio

      **MODIFY_CONFIG_PERM:** Para modificar la configuración de un servicio

      **SUPERVISOR_PERM:** Para ver los datos de instancias de proceso de un servicio creado a partir de un proceso

      **START_STOP_PERM:** Para iniciar y detener un servicio

      **ADD_REMOVE_ENDPOINTS_PERM:** Agregar, quitar y modificar puntos finales de un servicio

      **CREATE_VERSION_PERM:** Para crear una nueva versión del servicio

      **DELETE_VERSION_PERM:** Para eliminar una versión del servicio

      **MODIFY_VERSION_PERM:** Para modificar una versión del servicio

      **READ_PERM:** Para ver el servicio

      Haga clic en Finalizado para agregar la entidad de seguridad al perfil de seguridad.

1. Haga clic en Finalizado para completar la configuración.

## Configuración de los AEM formularios que forman parte de un archivo {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones y haga clic en la pestaña Archivos.
1. En la página Administración de archivos , seleccione el archivo que desea configurar.
1. En la página Ver archivo , seleccione el recurso de archivo resaltado.
1. Configure el archivo de proceso importado.

## Utilice el asistente de configuración para configurar los AEM formularios que forman parte de un archivo {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones y haga clic en la pestaña Archivos.
1. Haga clic en Configurar junto al archivo de archivo para configurarlo.
1. Aparecerá la página Configurar Puntos Finales, donde puede realizar los cambios que necesite:

   * Para cambiar el nombre de un extremo o editar su descripción, haga clic en él.
   * Para agregar un extremo de Administrador de tareas, haga clic en Agregar administrador de tareas. Para obtener más información sobre la configuración del Administrador de tareas, consulte [Configuración de los extremos del Administrador de tareas](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Para agregar un extremo de carpeta vigilada, haga clic en Agregar carpeta vigilada. Para obtener más información sobre la configuración de la carpeta vigilada, consulte [Configuración de extremo de carpeta vigilada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Para añadir un extremo de correo electrónico, haga clic en Añadir correo electrónico. Para obtener más información sobre la configuración del correo electrónico, consulte [Configuración de extremo de correo electrónico](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Para agregar un punto final de EJB, haga clic en Agregar EJB y especifique un nombre y una descripción para el punto final.
   * Para agregar un extremo SOAP, haga clic en Agregar SOAP y especifique un nombre y una descripción para el extremo.
   * Para agregar un extremo Remoting, haga clic en Agregar Remoting. Para obtener más información sobre la configuración de Remoting, consulte [Configuración de extremo remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Para agregar un extremo REST, haga clic en Agregar REST y especifique un nombre y una descripción para el extremo. Tenga en cuenta que la URL de invocación de REST se muestra en la página Agregar extremo de REST .
   * Para quitar un punto final, active la casilla que hay junto a él y haga clic en Quitar.

1. Haga clic en Siguiente.
1. Si un proceso o servicio de la LCA tiene parámetros de configuración, aparecerá una página Configurar parámetros, donde puede configurar los parámetros del servicio y hacer clic en Siguiente.
1. En la página Configurar perfil de seguridad, puede realizar los cambios que necesite:

   * **Requerir que los llamadores se autentiquen:** Esta configuración indica si el servicio se puede invocar con o sin credenciales.

      If *Los llamadores deben autenticarse actualmente* se muestra, el llamador del servicio debe estar autenticado y el principal del usuario de la llamada debe estar autorizado a invocar el servicio; de lo contrario, se rechazará el intento de invocación. Para eliminar la necesidad de autenticarse, haga clic en Permitir llamadas no autenticadas.

      If *No es necesario que los llamadores se autentiquen* , el llamador del servicio puede o no estar autenticado. La invocación del servicio siempre se realizará correctamente porque no hay comprobación de autorización. Para requerir autenticación, haga clic en Requerir llamadas para autenticarse.

   * **Ejecutar como:** Especifica la identidad en tiempo de ejecución utilizada por un servicio después de invocarse. Para cambiar esta opción, haga clic en Cambiar. Elija entre las siguientes opciones:

      **No especificado:** Se utiliza el comportamiento predeterminado.

      **Invocador:** Utiliza la misma identidad que el usuario que invocó el servicio.

      **Sistema:** Ejecuta el servicio con privilegios completos. Esta es la configuración predeterminada para los procesos de larga duración.

      **Usuario con nombre:** Permite ejecutar el servicio como un usuario específico. Esta es la configuración predeterminada para los procesos de corta duración. Cuando seleccione esta opción, haga clic en Seleccionar usuario para mostrar la página Seleccionar principal, donde puede buscar y seleccionar al usuario.

   * Para agregar una entidad de seguridad al perfil de seguridad, haga clic en Agregar entidad de seguridad y seleccione el usuario o grupo que desee agregar como entidad de seguridad. Haga clic en Siguiente y, a continuación, seleccione los permisos que desea asignar a esta entidad de seguridad:

      **INVOKE_PERM:** Para invocar todas las operaciones en el servicio

      **MODIFY_CONFIG_PERM:** Para modificar la configuración de un servicio

      **SUPERVISOR_PERM:** Para ver los datos de instancias de proceso de un servicio creado a partir de un proceso

      **START_STOP_PERM:** Para iniciar y detener un servicio

      **ADD_REMOVE_ENDPOINTS_PERM:** Agregar, quitar y modificar puntos finales de un servicio

      **CREATE_VERSION_PERM:** Para crear una nueva versión del servicio

      **DELETE_VERSION_PERM:** Para eliminar una versión del servicio

      **MODIFY_VERSION_PERM:** Para modificar una versión del servicio

      **READ_PERM:** Para ver el servicio

      Haga clic en Finalizado para agregar la entidad de seguridad al perfil de seguridad.

## Eliminación de un archivo {#remove-an-archive}

>[!NOTE]
>
>Para eliminar un archiving que contenga activos almacenados en un repositorio de terceros (Content Server de Documentum de EMC, IBM FileNet Content Manager o IBM Content Manager), también debe eliminar los archivos de activos del repositorio mediante Workbench.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de archivos.
1. En la página Administración de archivos, active la casilla de verificación del archivo que desea quitar y haga clic en Quitar.
