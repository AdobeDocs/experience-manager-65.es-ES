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
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 0%

---


# Importar y administrar archivos {#import-and-manage-archives}

Utilice la ficha Archivos para importar y administrar las LCA creadas en el área de trabajo.

## Importar un archivo {#import-an-archive}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones y, a continuación, haga clic en la ficha Archivos.
1. Haga clic en Importar.
1. Haga clic en Examinar para buscar el archivo que desea importar y, a continuación, haga clic en Previsualización.
1. Revise la lista de recursos y objetos que se instalarán con el archivo. Asegúrese de que no haya conflictos con los recursos, objetos y configuraciones de servicio existentes, ya que no hay ninguna capacidad de deshacer disponible.

   Si selecciona importar las configuraciones de servicio, AEM formularios importa todos los archivos de configuración de proceso (extremos, perfiles de seguridad y parámetros de configuración de servicio) utilizados por los procesos en LCA.

1. Haga clic en Importar.
1. Revise los resultados de la importación y haga clic en Omitir configuración para finalizar el proceso de importación o haga clic en Configurar para configurar el archivo.

   >[!NOTE]
   >
   >Si hace clic en Omitir configuración, puede configurar el archivo más adelante.

1. Si hace clic en Configurar, aparece la página Configurar extremos, donde puede realizar los cambios que necesite:

   * Para cambiar el nombre de un extremo o editar su descripción, haga clic en él.
   * Para agregar un extremo del Administrador de Tareas, haga clic en Añadir TaskManager. Para obtener más información sobre la configuración del Administrador de Tareas, consulte [Configuración de los extremos del Administrador de Tareas](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Para agregar un extremo de carpeta vigilada, haga clic en Añadir carpeta vigilada. Para obtener más información sobre la configuración de la carpeta vigilada, consulte [Configuración del punto final de la carpeta vigilada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Para agregar un extremo de correo electrónico, haga clic en Añadir correo electrónico. Para obtener más información sobre la configuración de Correo electrónico, consulte [Configuración de extremo de correo electrónico](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Para agregar un punto final de EJB, haga clic en Añadir EJB y especifique un nombre y una descripción para el punto final.
   * Para agregar un extremo SOAP, haga clic en Añadir SOAP y especifique un nombre y una descripción para el extremo.
   * Para agregar un extremo Remoting, haga clic en Añadir Remoting. Para obtener más información sobre la configuración de Remoting, consulte [Configuración de punto final remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Para agregar un extremo REST, haga clic en Añadir REST y especifique un nombre y una descripción para el extremo. Observe la URL de invocación REST que se muestra en la página Añadir extremo REST.
   * Para eliminar un punto final, seleccione la casilla de verificación situada junto a él y haga clic en Eliminar.

1. Haga clic en Siguiente. 
1. Si un proceso o servicio de LCA tiene parámetros de configuración, aparece una página Configurar parámetros, donde puede configurar los parámetros de servicio y hacer clic en Siguiente.
1. En la página Configurar Perfil de seguridad, realice los cambios que necesite:

   * **Requerir que los llamadores se autentiquen:** esta configuración indica si el servicio se puede invocar con o sin credenciales.

      Si *Los llamadores necesitan autenticarse* en este momento, se debe autenticar al llamador del servicio y se debe autorizar al principal del usuario para que invoque el servicio; de lo contrario, se rechazará el intento de invocación. Para eliminar la necesidad de autenticarse, haga clic en Permitir llamadas no autenticadas.

      Si no se requiere que *llamadores se autentiquen*, no es necesario autenticar al llamador del servicio. La invocación del servicio siempre tendrá éxito porque no hay comprobación de autorización. Para requerir autenticación, haga clic en Requerir que los llamadores se autentiquen.

   * **Ejecutar como:** especifica la identidad en tiempo de ejecución que utiliza un servicio después de invocarse. Para cambiar esta opción, haga clic en Cambiar. Elija entre las siguientes opciones:

      **No especificado:** se utiliza el comportamiento predeterminado.

      **Invocador:** utiliza la misma identidad que el usuario que invocó el servicio.

      **Sistema:** ejecuta el servicio con privilegios completos. Esta es la configuración predeterminada para los procesos de larga duración.

      **Usuario con nombre:** le permite ejecutar el servicio como un usuario específico. Esta es la configuración predeterminada para los procesos de corta duración. Cuando seleccione esta opción, haga clic en Seleccionar usuario para mostrar la página Seleccionar principal, donde puede buscar y seleccionar el usuario.

   * Para agregar una entidad de seguridad al perfil de seguridad, haga clic en Añadir entidad de seguridad y seleccione el usuario o grupo que desee agregar como entidad de seguridad. Haga clic en Siguiente y, a continuación, seleccione los permisos que desea asignar a esta entidad de seguridad:

      **INVOKE_PERM:** Para invocar todas las operaciones en el servicio

      **MODIFY_CONFIG_PERM:** Para modificar la configuración de un servicio

      **SUPERVISOR_PERM:** Para vista de datos de instancia de proceso para un servicio creado a partir de un proceso

      **INICIO_STOP_PERM:** Para inicio y parada de un servicio

      **AÑADIR_REMOVE_ENDPOINTS_PERM:** Para agregar, quitar y modificar puntos finales de un servicio

      **CREATE_VERSION_PERM:** Para crear una nueva versión del servicio

      **DELETE_VERSION_PERM:** Para eliminar una versión del servicio

      **MODIFY_VERSION_PERM:** Para modificar una versión del servicio

      **READ_PERM:** vista del servicio

      Haga clic en Finalizado para agregar el principal al perfil de seguridad.

1. Haga clic en Finalizado para completar la configuración.

## Configure los formularios AEM que forman parte de un archivo de almacenamiento {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones y, a continuación, haga clic en la ficha Archivos.
1. En la página Administración de archivos, seleccione el archivo que desea configurar.
1. En la página Archivo de Vista, seleccione el recurso de archivo resaltado.
1. Configure el archivo de archivo de proceso importado.

## Utilice el asistente de configuración para configurar los formularios AEM que forman parte de un archivo de almacenamiento {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones y, a continuación, haga clic en la ficha Archivos.
1. Haga clic en Configurar junto al archivo de almacenamiento para configurarlo.
1. Aparecerá la página Configurar Extremos, donde puede realizar los cambios que necesite:

   * Para cambiar el nombre de un extremo o editar su descripción, haga clic en él.
   * Para agregar un extremo del Administrador de Tareas, haga clic en Añadir TaskManager. Para obtener más información sobre la configuración del Administrador de Tareas, consulte [Configuración de los extremos del Administrador de Tareas](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Para agregar un extremo de carpeta vigilada, haga clic en Añadir carpeta vigilada. Para obtener más información sobre la configuración de la carpeta vigilada, consulte [Configuración del punto final de la carpeta vigilada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Para agregar un extremo de correo electrónico, haga clic en Añadir correo electrónico. Para obtener más información sobre la configuración de Correo electrónico, consulte [Configuración de extremo de correo electrónico](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Para agregar un punto final de EJB, haga clic en Añadir EJB y especifique un nombre y una descripción para el punto final.
   * Para agregar un extremo SOAP, haga clic en Añadir SOAP y especifique un nombre y una descripción para el extremo.
   * Para agregar un extremo Remoting, haga clic en Añadir Remoting. Para obtener más información sobre la configuración de Remoting, consulte [Configuración de punto final remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Para agregar un extremo REST, haga clic en Añadir REST y especifique un nombre y una descripción para el extremo. Observe la URL de invocación REST que se muestra en la página Añadir extremo REST.
   * Para eliminar un punto final, seleccione la casilla de verificación situada junto a él y haga clic en Eliminar.

1. Haga clic en Siguiente. 
1. Si un proceso o servicio de LCA tiene parámetros de configuración, aparece una página Configurar parámetros, donde puede configurar los parámetros de servicio y hacer clic en Siguiente.
1. En la página Configurar Perfil de seguridad, puede realizar los cambios que necesite:

   * **Requerir que los llamadores se autentiquen:** esta configuración indica si el servicio se puede invocar con o sin credenciales.

      Si *Los llamadores necesitan autenticarse* en este momento, se debe autenticar al llamador del servicio y se debe autorizar al principal del usuario para que invoque el servicio; de lo contrario, se rechazará el intento de invocación. Para eliminar la necesidad de autenticarse, haga clic en Permitir llamadas no autenticadas.

      Si no se requiere que *llamadores se autentiquen*, el llamador del servicio puede o no autenticarse. La invocación del servicio siempre tendrá éxito porque no hay comprobación de autorización. Para requerir autenticación, haga clic en Requerir que los llamadores se autentiquen.

   * **Ejecutar como:** especifica la identidad en tiempo de ejecución que utiliza un servicio después de invocarse. Para cambiar esta opción, haga clic en Cambiar. Elija entre las siguientes opciones:

      **No especificado:** se utiliza el comportamiento predeterminado.

      **Invocador:** utiliza la misma identidad que el usuario que invocó el servicio.

      **Sistema:** ejecuta el servicio con privilegios completos. Esta es la configuración predeterminada para los procesos de larga duración.

      **Usuario con nombre:** le permite ejecutar el servicio como un usuario específico. Esta es la configuración predeterminada para los procesos de corta duración. Cuando seleccione esta opción, haga clic en Seleccionar usuario para mostrar la página Seleccionar principal, donde puede buscar y seleccionar el usuario.

   * Para agregar una entidad de seguridad al perfil de seguridad, haga clic en Añadir entidad de seguridad y seleccione el usuario o grupo que desee agregar como entidad de seguridad. Haga clic en Siguiente y, a continuación, seleccione los permisos que desea asignar a esta entidad de seguridad:

      **INVOKE_PERM:** Para invocar todas las operaciones en el servicio

      **MODIFY_CONFIG_PERM:** Para modificar la configuración de un servicio

      **SUPERVISOR_PERM:** Para vista de datos de instancia de proceso para un servicio creado a partir de un proceso

      **INICIO_STOP_PERM:** Para inicio y parada de un servicio

      **AÑADIR_REMOVE_ENDPOINTS_PERM:** Para agregar, quitar y modificar puntos finales de un servicio

      **CREATE_VERSION_PERM:** Para crear una nueva versión del servicio

      **DELETE_VERSION_PERM:** Para eliminar una versión del servicio

      **MODIFY_VERSION_PERM:** Para modificar una versión del servicio

      **READ_PERM:** vista del servicio

      Haga clic en Finalizado para agregar el principal al perfil de seguridad.

## Eliminar un archivo {#remove-an-archive}

>[!NOTE]
>
>Para eliminar un archiving que contenga activos almacenados en un repositorio de terceros (Content Server de Documentum de EMC, IBM FileNet Content Manager o IBM Content Manager), también debe eliminar los archivos de recursos del repositorio mediante Workbench.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de archivos.
1. En la página Administración de archivos, active la casilla de verificación del archivo que desea eliminar y haga clic en Eliminar.

