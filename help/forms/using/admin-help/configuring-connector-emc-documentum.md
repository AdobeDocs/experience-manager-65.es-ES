---
title: Configuración de Connector para Documentum de EMC
seo-title: Configuración de Connector para Documentum de EMC
description: Conozca cómo configurar Connector para Documentum de EMC para permitir la comunicación entre AEM formularios y Documentum de EMC.
seo-description: Conozca cómo configurar Connector para Documentum de EMC para permitir la comunicación entre AEM formularios y Documentum de EMC.
uuid: fc96900a-ec8a-4efd-ad8e-25e9967e649b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e62370a7-9d9e-43a3-8014-8e53800c870d
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 1%

---


# Configuración del Conector para Documentum de EMC {#configuring-connector-for-emc-documentum}

Connector for EMC Documentum permite la comunicación entre AEM formularios y Documentum de EMC. Para obtener más información, consulte &quot;Conectores para ECM&quot; en [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_63).

Configurar Connector para Documentum de EMC implica configurar la conexión al servidor y las credenciales del repositorio.

>[!NOTE]
>
>En versiones anteriores, los recursos se podían almacenar en un repositorio de ECM. En la versión actual, los recursos se almacenan en el repositorio nativo de formularios de AEM y los servicios del proveedor de repositorios se han quedado obsoletos. La migración de recursos de un repositorio de ECM al repositorio de formularios AEM se realiza cuando se realiza una actualización a AEM formularios. Para obtener más información, consulte la guía de actualización de formularios AEM para su servidor de aplicaciones.

## Configuración de la conexión al servidor {#configuring-the-server-connection}

En este tema se describen las tareas de Connector para Documentum de EMC que puede realizar en la página Configuración.

>[!NOTE]
>
>Si está configurando todos los ajustes de forma simultánea, sólo tiene que hacer clic en Guardar una vez.

### Configurar el servidor {#configure-the-server}

Debe configurar la información del servidor del agente de conexiones. Esta información es necesaria para conectarse a los repositorios de contenido de Documentum e iniciar Connector para Documentum de EMC.

1. En la consola de administración, haga clic en Servicios > Conector para Documentum de EMC > Configuración.
1. En el área Información de configuración de Documentum, introduzca el nombre de host o la dirección IP y el número de puerto del agente de conexión. El número de puerto debe ser un entero positivo (por ejemplo, 1489).
1. Haga clic en Guardar.

### Configurar las credenciales principales {#configure-principal-credentials}

Al configurar las credenciales principales, el nombre del repositorio que proporcione dependerá de si se proporciona un nombre de repositorio explícito durante el inicio de sesión.

Si introduce un nombre de usuario o una contraseña incorrectos, obtendrá los siguientes resultados, según si el servicio se está ejecutando en ese momento:

* Si se detienen el servicio Proveedor de Repositorios de Documentum de EMC y el servicio Conector de Repositorio de Contenido de Documentum de EMC, cuando se guarda la información de configuración del servicio, no aparece ningún error. Sin embargo, la próxima vez que inicio el servicio, se generará una excepción y el servicio no se inicio.
* Si se inicia el servicio Proveedor de Repositorios de Documentum de EMC o el servicio Conector de Repositorio de Contenido de Documentum de EMC, al guardar la información de configuración de servicio, el servicio intenta validar la información de credenciales inmediatamente. En este caso, se produce un error y la información de configuración no se guarda.

1. En la consola de administración, haga clic en Servicios > Conector para Documentum de EMC > Configuración.
1. En el área Información de Credenciales de Documentum, escriba el nombre de usuario y la contraseña de un usuario con privilegios de superadministrador.
1. Si no se proporciona un nombre de repositorio explícito durante el inicio de sesión, introduzca el nombre de repositorio con el que están asociadas las credenciales.
1. Haga clic en Guardar.

### Cambiar el proveedor de servicio del repositorio {#change-the-repository-service-provider}

Puede configurar qué proveedor de servicio de repositorio utilizar con Documentum. Las llamadas al servicio de repositorio se delegan al proveedor que configure. Las opciones disponibles son las siguientes:

**Nombre del Proveedor de servicio del repositorio actual:** El nombre del proveedor de servicio del repositorio actual

**Proveedor de repositorio de Documentum de EMC:** convierte al proveedor de repositorio de Documentum en el proveedor del repositorio para el repositorio. Esta opción está en desuso

**proveedor de repositorio:** convierte al proveedor de repositorio nativo en el proveedor del repositorio

>[!NOTE]
>
>Para seleccionar un proveedor de servicio de repositorio distinto de los enumerados, configure RepositoryService en Aplicaciones y servicios > Administración de servicios. <!-- Fix broken link (See Managing Services) -->.

1. En la consola de administración, haga clic en Servicios > Conector para Documentum de EMC > Configuración.
1. En el área Información del Proveedor de servicio del repositorio, seleccione el proveedor de servicio del repositorio alternativo.
1. Haga clic en Guardar.

## Configuración de las credenciales del repositorio {#configuring-repository-credentials}

La información de credenciales de Documentum se utiliza en el contexto del sistema de formularios AEM. Las credenciales del repositorio son específicas de repositorios concretos de Documentum. Puede proporcionar credenciales para cualquier número de repositorios; sin embargo, solo puede especificar un conjunto de credenciales por repositorio.

### Añadir una credencial de repositorio {#add-a-repository-credential}

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

## Habilitar la solicitud para compartir las colas de tareas de Workspace {#enable-the-request-for-sharing-of-workspace-task-queues}

Se requieren algunos pasos manuales para garantizar que la función Solicitud de uso compartido de cola de Tarea en Workspace funcione correctamente con Connector for EMC Documentum.

1. Una vez que se hayan implementado AEM formularios y se haya instalado Workbench, inicie sesión en Workbench y abra la vista Recursos. Determinará la ubicación del archivo QueueSharing.swf desde esta vista.
1. Arrastre el archivo QueueSharing.swf desde la Vista Recursos hasta el escritorio de Windows o una ubicación equivalente, según el sistema operativo.
1. En la consola de administración, haga clic en Servicios > Conector para Documentum de EMC > Configuración.
1. En Información del Proveedor de servicio de Repositorios, cambie el proveedor de repositorios configurado a Proveedor de Repositorios de Documentum de EMC.
1. Inicio Workbench y copie el archivo QueueSharing.swf desde la ubicación donde originalmente lo copió (por ejemplo, el escritorio de Windows u otra ubicación) en un directorio existente dentro del repositorio de Documentum de EMC.
1. En la vista Procesos de Workbench, abra el proceso de uso compartido de colas.
1. En la vista Variables, abra las propiedades de la variable &quot;theForm&quot; y cambie el URI para que coincida con la ruta de acceso donde colocó el archivo QueueSharing.swf en el paso 5.
1. Guarde el proceso.
1. Migrar el proceso al entorno de producción según la política de su organización.

