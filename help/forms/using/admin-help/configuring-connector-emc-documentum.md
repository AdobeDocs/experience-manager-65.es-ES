---
title: Configuración de Connector para Documentum de EMC
seo-title: Configuración de Connector para Documentum de EMC
description: Conozca cómo configurar Connector para Documentum de EMC para permitir la comunicación entre formularios AEM y Documentum de EMC.
seo-description: Conozca cómo configurar Connector para Documentum de EMC para permitir la comunicación entre formularios AEM y Documentum de EMC.
uuid: fc96900a-ec8a-4efd-ad8e-25e9967e649b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e62370a7-9d9e-43a3-8014-8e53800c870d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración de Connector para Documentum de EMC {#configuring-connector-for-emc-documentum}

Connector for EMC Documentum permite la comunicación entre formularios AEM y Documentum de EMC. Para obtener más información, consulte &quot;Conectores para ECM&quot; en [Referencia](https://www.adobe.com/go/learn_aemforms_services_63)de servicios.

Configurar Connector para Documentum de EMC implica configurar la conexión al servidor y las credenciales del repositorio.

>[!NOTE]
>
>En versiones anteriores, los recursos se podían almacenar en un repositorio de ECM. En la versión actual, los recursos se almacenan en el repositorio nativo de formularios AEM y los servicios del proveedor de repositorios se han quedado obsoletos. La migración de recursos de un repositorio de ECM al repositorio de formularios de AEM se realiza al realizar una actualización a los formularios de AEM. Para obtener más información, consulte la guía de actualización de formularios de AEM para su servidor de aplicaciones.

## Configuración de la conexión con el servidor {#configuring-the-server-connection}

En este tema se describen las tareas para Connector for EMC Documentum que puede realizar en la página Configuración.

>[!NOTE]
>
>Si está configurando todos los ajustes de forma simultánea, sólo tiene que hacer clic en Guardar una vez.

### Configurar el servidor {#configure-the-server}

Debe configurar la información del servidor del agente de conexiones. Esta información es necesaria para conectarse a los repositorios de contenido de Documentum e iniciar Connector para Documentum de EMC.

1. En la consola de administración, haga clic en Servicios > Conector para Documentum de EMC > Configuración.
1. En el área Información de configuración de Documentum, introduzca el nombre de host o la dirección IP y el número de puerto del agente de conexión. El número de puerto debe ser un entero positivo (por ejemplo, 1489).
1. Haga clic en Guardar.

### Configurar credenciales principales {#configure-principal-credentials}

Al configurar las credenciales principales, el nombre del repositorio que proporcione dependerá de si se proporciona un nombre de repositorio explícito durante el inicio de sesión.

Si introduce un nombre de usuario o una contraseña incorrectos, obtendrá los siguientes resultados, según si el servicio se está ejecutando en ese momento:

* Si se detienen el servicio Proveedor de Repositorios de Documentum de EMC y el servicio Conector de Repositorio de Contenido de Documentum de EMC, cuando se guarda la información de configuración del servicio, no aparece ningún error. Sin embargo, la próxima vez que inicie el servicio, se generará una excepción y el servicio no se iniciará.
* Si se inicia el servicio Proveedor de Repositorios de Documentum de EMC o el servicio Conector de Repositorio de Contenido de Documentum de EMC, al guardar la información de configuración de servicio, el servicio intenta validar la información de credenciales inmediatamente. En este caso, se produce un error y la información de configuración no se guarda.

1. En la consola de administración, haga clic en Servicios > Conector para Documentum de EMC > Configuración.
1. En el área Información de Credenciales de Documentum, escriba el nombre de usuario y la contraseña de un usuario con privilegios de superadministrador.
1. Si no se proporciona un nombre de repositorio explícito durante el inicio de sesión, introduzca el nombre de repositorio con el que están asociadas las credenciales.
1. Haga clic en Guardar.

### Cambiar el proveedor de servicios de repositorio {#change-the-repository-service-provider}

Puede configurar qué proveedor de servicios de repositorio utilizar con Documentum. Las llamadas al servicio de repositorio se delegan al proveedor que configure. Las opciones disponibles son las siguientes:

**** Nombre actual del proveedor de servicios de repositorio: El nombre del proveedor de servicios de repositorio actual

**** Proveedor de repositorio de Documentum de ECM: Convierte al proveedor de repositorio de Documentum en el proveedor del repositorio. Esta opción está en desuso

**** proveedor de repositorio: Convierte al proveedor de repositorio nativo en el proveedor del repositorio

***Nota **: Para seleccionar un proveedor de servicios de repositorio que no esté en la lista, configure RepositoryService en Aplicaciones y servicios > Service Management.<!-- Fix broken link (See Managing Services) -->*

1. En la consola de administración, haga clic en Servicios > Conector para Documentum de EMC > Configuración.
1. En el área Información del proveedor de servicios de repositorio, seleccione el proveedor de servicios de repositorio alternativo.
1. Haga clic en Guardar.

## Configuración de las credenciales del repositorio {#configuring-repository-credentials}

La información de credenciales de Documentum se utiliza en el contexto del sistema de formularios AEM. Las credenciales del repositorio son específicas de repositorios concretos de Documentum. Puede proporcionar credenciales para cualquier número de repositorios; sin embargo, solo puede especificar un conjunto de credenciales por repositorio.

### Agregar una credencial de repositorio {#add-a-repository-credential}

1. En la consola de administración, haga clic en Servicios > Conector para Documentum de EMC > Configuración de credenciales de repositorio.
1. Haga clic en Agregar. Aparece la página Información de Credenciales del Sistema de Documentum.
1. Escriba un nombre para el repositorio.
1. Introduzca un nombre de usuario y una contraseña.
1. Haga clic en Guardar.

Si se están ejecutando el Servicio de Repositorio de Contenido para Documentum de EMC y/o el Servicio de Repositorio para Documentum de EMC, la información de credenciales se verifica con respecto al repositorio especificado antes de que se almacene en la base de datos. Si las credenciales no son válidas o existen, se muestra un mensaje de error.

### Quitar una credencial de repositorio {#remove-a-repository-credential}

1. En la consola de administración, haga clic en Servicios > Conector para Documentum de EMC > Configuración.
1. Seleccione la casilla de verificación situada junto al repositorio desde la que desea quitar las credenciales y haga clic en Eliminar. Las credenciales del repositorio seleccionado se eliminan de la base de datos.

### Cambiar el nombre de usuario y la contraseña de una credencial de repositorio {#change-the-user-name-and-password-for-a-repository-credential}

1. En la consola de administración, haga clic en Servicios > Conector para Documentum de EMC > Configuración.
1. Haga clic en el nombre del repositorio para el que desea editar las credenciales.
1. Cambie el nombre de usuario o la contraseña del repositorio, o ambos. (El nombre del repositorio es de sólo lectura).
1. Haga clic en Guardar.

Si se están ejecutando el Servicio de Repositorio de Contenido para Documentum de EMC y/o el Servicio de Repositorio para Documentum de EMC, la información de credenciales se verifica con respecto al repositorio especificado antes de que se almacene en la base de datos. Si las credenciales no son válidas o existen, se muestra un mensaje de error.

## Habilitar la solicitud para compartir colas de tareas de Workspace {#enable-the-request-for-sharing-of-workspace-task-queues}

Se requieren algunos pasos manuales para garantizar que la función Solicitud de uso compartido de colas de tareas en Workspace funcione correctamente con Connector for EMC Documentum.

1. Una vez implementados los formularios AEM y instalado Workbench, inicie sesión en Workbench y abra la vista Recursos. Determinará desde esta vista dónde se encuentra el archivo QueueSharing.swf.
1. Arrastre el archivo QueueSharing.swf desde la vista Recursos hasta el escritorio de Windows o una ubicación equivalente, según el sistema operativo.
1. En la consola de administración, haga clic en Servicios > Conector para Documentum de EMC > Configuración.
1. En Información del proveedor de servicios de repositorio, cambie el proveedor de repositorio configurado a Proveedor de repositorio de Documentum de EMC.
1. Inicie Workbench y copie el archivo QueueSharing.swf desde la ubicación en la que lo copió originalmente (por ejemplo, el escritorio de Windows u otra ubicación) en un directorio existente dentro del repositorio de Documentum de EMC.
1. En la vista Procesos de Workbench, abra el proceso de uso compartido de colas.
1. En la vista Variables, abra las propiedades de la variable &quot;theForm&quot; y cambie el URI para que coincida con la ruta en la que colocó el archivo QueueSharing.swf en el paso 5.
1. Guarde el proceso.
1. Migrar el proceso al entorno de producción según la política de su organización.

