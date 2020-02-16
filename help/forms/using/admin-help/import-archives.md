---
title: Importar y administrar archivos
seo-title: Importar y administrar archivos
description: Obtenga información sobre cómo importar y administrar archivos.
seo-description: Obtenga información sobre cómo importar y administrar archivos.
uuid: aa1613dd-6350-49a7-9643-44365e2acdcc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b6f6463a-2ae4-43d2-8d16-cc20a954e50e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Importar y administrar archivos {#import-and-manage-archives}

Utilice la ficha Archivos para importar y administrar las LCA creadas en el área de trabajo.

## Importar un archivo {#import-an-archive}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones y, a continuación, haga clic en la ficha Archivos.
1. Haga clic en Importar.
1. Haga clic en Examinar para buscar el archivo que desea importar y, a continuación, haga clic en Vista previa.
1. Revise la lista de recursos y objetos que se instalarán con el archivo. Asegúrese de que no haya conflictos con los recursos, objetos y configuraciones de servicio existentes, ya que no hay ninguna capacidad de deshacer disponible.

   Si selecciona importar las configuraciones de servicio, los formularios de AEM importan todos los archivos de configuración de proceso (extremos, perfiles de seguridad y parámetros de configuración de servicio) utilizados por los procesos de LCA.

1. Haga clic en Importar.
1. Revise los resultados de la importación y haga clic en Omitir configuración para finalizar el proceso de importación o haga clic en Configurar para configurar el archivo.

   >[!NOTE]
   >
   >Si hace clic en Omitir configuración, puede configurar el archivo más adelante.

1. Si hace clic en Configurar, aparece la página Configurar extremos, donde puede realizar los cambios que necesite:

   * Para cambiar el nombre de un extremo o editar su descripción, haga clic en él.
   * Para agregar un extremo del Administrador de tareas, haga clic en Agregar Administrador de tareas. Para obtener más información sobre la configuración del Administrador de tareas, consulte [Configuración de los extremos](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)del Administrador de tareas.
   * Para agregar un extremo de carpeta vigilada, haga clic en Agregar carpeta vigilada. Para obtener más información sobre la configuración de la carpeta vigilada, consulte Configuración del punto final de la carpeta [vigilada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Para agregar un extremo de correo electrónico, haga clic en Agregar correo electrónico. Para obtener más información sobre la configuración de correo electrónico, consulte Configuración de los extremos [de correo electrónico](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Para agregar un punto final de EJB, haga clic en Agregar EJB y especifique un nombre y una descripción para el punto final.
   * Para agregar un extremo SOAP, haga clic en Agregar SOAP y especifique un nombre y una descripción para el extremo.
   * Para agregar un extremo Remoting, haga clic en Agregar remoto. Para obtener más información acerca de la configuración de Remoting, consulte Configuración de los extremos [Remoting](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Para agregar un extremo REST, haga clic en Agregar REST y especifique un nombre y una descripción para el extremo. Observe la URL de invocación REST que se muestra en la página Agregar extremo REST.
   * Para eliminar un punto final, seleccione la casilla de verificación situada junto a él y haga clic en Eliminar.

1. Haga clic en Siguiente.
1. Si un proceso o servicio de LCA tiene parámetros de configuración, aparece una página Configurar parámetros, donde puede configurar los parámetros de servicio y hacer clic en Siguiente.
1. En la página Configurar perfil de seguridad, realice los cambios que necesite:

   * **** Requerir que los llamadores se autentiquen: Esta configuración indica si el servicio se puede invocar con o sin credenciales.

      Si *los llamadores están actualmente obligados a autenticarse* , se debe autenticar al llamante del servicio y se debe autorizar al principal del usuario para que invoque el servicio; de lo contrario, se rechazará el intento de invocación. Para eliminar la necesidad de autenticarse, haga clic en Permitir llamadas no autenticadas.

      Si *los llamadores no necesitan autenticarse* , no es necesario autenticar al llamador del servicio. La invocación del servicio siempre tendrá éxito porque no hay comprobación de autorización. Para requerir autenticación, haga clic en Requerir que los llamadores se autentiquen.

   * **** Ejecutar como: Especifica la identidad en tiempo de ejecución que utiliza un servicio después de invocarse. Para cambiar esta opción, haga clic en Cambiar. Elija entre las siguientes opciones:

      **** No especificado: Se utiliza el comportamiento predeterminado.

      **** Invocador: Utiliza la misma identidad que el usuario que invocó el servicio.

      **** Sistema: Ejecuta el servicio con privilegios completos. Esta es la configuración predeterminada para los procesos de larga duración.

      **** Usuario con nombre: Permite ejecutar el servicio como un usuario específico. Esta es la configuración predeterminada para los procesos de corta duración. Cuando seleccione esta opción, haga clic en Seleccionar usuario para mostrar la página Seleccionar principal, donde puede buscar y seleccionar el usuario.

   * Para agregar un principal al perfil de seguridad, haga clic en Agregar entidad de seguridad y seleccione el usuario o grupo que desee agregar como principal. Haga clic en Siguiente y, a continuación, seleccione los permisos que desea asignar a esta entidad de seguridad:

      **** INVOKE_PERM: Para invocar todas las operaciones en el servicio

      **** MODIFY_CONFIG_PERM: Para modificar la configuración de un servicio

      **** SUPERVISOR_PERM: Para ver los datos de instancia de proceso de un servicio creado a partir de un proceso

      **** START_STOP_PERM: Para iniciar y detener un servicio

      **** ADD_REMOVE_ENDPOINTS_PERM: Adición, eliminación y modificación de puntos finales de un servicio

      **** CREATE_VERSION_PERM: Para crear una nueva versión del servicio

      **** DELETE_VERSION_PERM: Para eliminar una versión del servicio

      **** MODIFY_VERSION_PERM: Para modificar una versión del servicio

      **** READ_PERM: Para ver el servicio

      Haga clic en Finalizado para agregar el principal al perfil de seguridad.

1. Haga clic en Finalizado para completar la configuración.

## Configuración de los formularios de AEM que forman parte de un archivo {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones y, a continuación, haga clic en la ficha Archivos.
1. En la página Administración de archivos, seleccione el archivo que desea configurar.
1. En la página Ver archivo, seleccione el recurso de archivo resaltado.
1. Configure el archivo de archivo de proceso importado.

## Utilice el asistente de configuración para configurar los formularios de AEM que forman parte de un archivo {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones y, a continuación, haga clic en la ficha Archivos.
1. Haga clic en Configurar junto al archivo de almacenamiento para configurarlo.
1. Aparecerá la página Configurar Extremos, donde puede realizar los cambios que necesite:

   * Para cambiar el nombre de un extremo o editar su descripción, haga clic en él.
   * Para agregar un extremo del Administrador de tareas, haga clic en Agregar Administrador de tareas. Para obtener más información sobre la configuración del Administrador de tareas, consulte [Configuración de los extremos](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)del Administrador de tareas.
   * Para agregar un extremo de carpeta vigilada, haga clic en Agregar carpeta vigilada. Para obtener más información sobre la configuración de la carpeta vigilada, consulte Configuración del punto final de la carpeta [vigilada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Para agregar un extremo de correo electrónico, haga clic en Agregar correo electrónico. Para obtener más información sobre la configuración de correo electrónico, consulte Configuración de los extremos [de correo electrónico](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Para agregar un punto final de EJB, haga clic en Agregar EJB y especifique un nombre y una descripción para el punto final.
   * Para agregar un extremo SOAP, haga clic en Agregar SOAP y especifique un nombre y una descripción para el extremo.
   * Para agregar un extremo Remoting, haga clic en Agregar remoto. Para obtener más información acerca de la configuración de Remoting, consulte Configuración de los extremos [Remoting](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Para agregar un extremo REST, haga clic en Agregar REST y especifique un nombre y una descripción para el extremo. Observe la URL de invocación REST que se muestra en la página Agregar extremo REST.
   * Para eliminar un punto final, seleccione la casilla de verificación situada junto a él y haga clic en Eliminar.

1. Haga clic en Siguiente.
1. Si un proceso o servicio de LCA tiene parámetros de configuración, aparece una página Configurar parámetros, donde puede configurar los parámetros de servicio y hacer clic en Siguiente.
1. En la página Configurar perfil de seguridad, puede realizar los cambios que necesite:

   * **** Requerir que los llamadores se autentiquen: Esta configuración indica si el servicio se puede invocar con o sin credenciales.

      Si *los llamadores están actualmente obligados a autenticarse* , se debe autenticar al llamante del servicio y se debe autorizar al principal del usuario para que invoque el servicio; de lo contrario, se rechazará el intento de invocación. Para eliminar la necesidad de autenticarse, haga clic en Permitir llamadas no autenticadas.

      Si *los llamadores no están obligados a autenticarse* , el llamador del servicio puede o no estar autenticado. La invocación del servicio siempre tendrá éxito porque no hay comprobación de autorización. Para requerir autenticación, haga clic en Requerir que los llamadores se autentiquen.

   * **** Ejecutar como: Especifica la identidad en tiempo de ejecución que utiliza un servicio después de invocarse. Para cambiar esta opción, haga clic en Cambiar. Elija entre las siguientes opciones:

      **** No especificado: Se utiliza el comportamiento predeterminado.

      **** Invocador: Utiliza la misma identidad que el usuario que invocó el servicio.

      **** Sistema: Ejecuta el servicio con privilegios completos. Esta es la configuración predeterminada para los procesos de larga duración.

      **** Usuario con nombre: Permite ejecutar el servicio como un usuario específico. Esta es la configuración predeterminada para los procesos de corta duración. Cuando seleccione esta opción, haga clic en Seleccionar usuario para mostrar la página Seleccionar principal, donde puede buscar y seleccionar el usuario.

   * Para agregar un principal al perfil de seguridad, haga clic en Agregar entidad de seguridad y seleccione el usuario o grupo que desee agregar como principal. Haga clic en Siguiente y, a continuación, seleccione los permisos que desea asignar a esta entidad de seguridad:

      **** INVOKE_PERM: Para invocar todas las operaciones en el servicio

      **** MODIFY_CONFIG_PERM: Para modificar la configuración de un servicio

      **** SUPERVISOR_PERM: Para ver los datos de instancia de proceso de un servicio creado a partir de un proceso

      **** START_STOP_PERM: Para iniciar y detener un servicio

      **** ADD_REMOVE_ENDPOINTS_PERM: Adición, eliminación y modificación de puntos finales de un servicio

      **** CREATE_VERSION_PERM: Para crear una nueva versión del servicio

      **** DELETE_VERSION_PERM: Para eliminar una versión del servicio

      **** MODIFY_VERSION_PERM: Para modificar una versión del servicio

      **** READ_PERM: Para ver el servicio

      Haga clic en Finalizado para agregar el principal al perfil de seguridad.

## Eliminar un archivo {#remove-an-archive}

>[!NOTE]
>
>Para eliminar un archiving que contenga activos almacenados en un repositorio de terceros (Content Server de Documentum de EMC, IBM FileNet Content Manager o IBM Content Manager), también debe eliminar los archivos de recursos del repositorio mediante Workbench.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de archivos.
1. En la página Administración de archivos, active la casilla de verificación del archivo que desea eliminar y haga clic en Eliminar.

