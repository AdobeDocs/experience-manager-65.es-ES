---
title: Configuración de Connector para Documentum de EMC
seo-title: Configuring Connector for EMC Documentum
description: Aprenda a configurar el Connector para Documentum de EMC para permitir la comunicación entre formularios AEM y Documentum de EMC.
seo-description: Learn how to configure the Connector for EMC Documentum to enable communication between AEM forms and EMC Documentum.
uuid: fc96900a-ec8a-4efd-ad8e-25e9967e649b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e62370a7-9d9e-43a3-8014-8e53800c870d
exl-id: a31a496f-87b9-43c0-a98c-5f6ca5d11690
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---

# Configuración de Connector para Documentum de EMC {#configuring-connector-for-emc-documentum}

Connector for EMC Documentum permite la comunicación entre formularios AEM y Documentum de EMC. Para obtener más información, consulte &quot;Conectores para ECM&quot; en [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_63).

Configurar Connector para Documentum de EMC implica configurar la conexión del servidor y las credenciales del repositorio.

>[!NOTE]
>
>En versiones anteriores , los recursos se podían almacenar en un repositorio de ECM. En la versión actual, los recursos se almacenan en el repositorio nativo de formularios de AEM y los servicios del proveedor de repositorios se han desaprobado. La migración de recursos de un repositorio ECM al repositorio de formularios AEM se realiza al realizar una actualización a AEM formularios. Para obtener más información, consulte la guía de actualización de formularios AEM para su servidor de aplicaciones.

## Configuración de la conexión del servidor {#configuring-the-server-connection}

En este tema se describen las tareas para Connector for EMC Documentum que puede realizar en la página Configuración.

>[!NOTE]
>
>Si está configurando todos los ajustes simultáneamente, solo necesita hacer clic en Guardar una vez.

### Configuración del servidor {#configure-the-server}

Debe configurar la información del servidor del agente de conexión. Esta información es necesaria para conectarse a los repositorios de contenido de Documentum e iniciar el Connector para Documentum de EMC.

1. En la consola de administración, haga clic en Servicios > Conector para Documentum de EMC > Configuración.
1. En el área de información de configuración de Documentum, introduzca el nombre de host o la dirección IP y el número de puerto del agente de conexión. El número de puerto debe ser un número entero positivo (por ejemplo, 1489).
1. Haga clic en Guardar.

### Configuración de las credenciales principales {#configure-principal-credentials}

Al configurar las credenciales principales, el nombre del repositorio que proporcione depende de si se proporciona un nombre de repositorio explícito durante el inicio de sesión.

Si introduce un nombre de usuario o una contraseña incorrectos, obtendrá los siguientes resultados, en función de si el servicio se está ejecutando actualmente:

* Si se detienen el servicio Proveedor de Repositorios de Documentum de EMC y el servicio Conector de Repositorio de Contenido de Documentum de EMC, cuando se guarda la información de configuración del servicio, no aparece ningún error. Sin embargo, la próxima vez que inicie el servicio, se generará una excepción y el servicio no se iniciará.
* Si se inicia el servicio Proveedor de Repositorios de Documentum de EMC o el servicio Conector de Repositorio de Contenido de Documentum de EMC, cuando se guarda la información de configuración del servicio, el servicio intenta validar la información de credenciales inmediatamente. En este caso, se produce un error y la información de configuración no se guarda.

1. En la consola de administración, haga clic en Servicios > Conector para Documentum de EMC > Configuración.
1. En el área Información de Credenciales Principal de Documentum, escriba el nombre de usuario y la contraseña de un usuario con privilegios de superadministrador.
1. Si no se proporciona un nombre de repositorio explícito durante el inicio de sesión, introduzca el nombre de repositorio al que están asociadas las credenciales.
1. Haga clic en Guardar.

### Cambiar el proveedor de servicios de repositorio {#change-the-repository-service-provider}

Puede configurar qué proveedor de servicios de repositorio utilizar con Documentum. Las llamadas al servicio del repositorio se delegan al proveedor que configure. Las opciones disponibles son las siguientes:

**Nombre actual del proveedor de servicios de repositorio:** Nombre del proveedor de servicios de repositorio actual

**Proveedor de repositorio de Documentum de ECM:** Hace que el proveedor de repositorios de Documentum sea el proveedor del repositorio. Esta opción está en desuso

**proveedor de repositorios:** Convierte al proveedor de repositorios nativo en el proveedor del repositorio

>[!NOTE]
>
>Para seleccionar un proveedor de servicios de repositorio que no esté en la lista, configure RepositoryService en Aplicaciones y Servicios > Administración de servicios. <!-- Fix broken link (See Managing Services) -->.

1. En la consola de administración, haga clic en Servicios > Conector para Documentum de EMC > Configuración.
1. En el área Información del proveedor de servicios de repositorio, seleccione el proveedor de servicios de repositorio alternativo.
1. Haga clic en Guardar.

## Configuración de las credenciales del repositorio {#configuring-repository-credentials}

La información de credenciales de Documentum se utiliza en el contexto del sistema de formularios AEM. Las credenciales del repositorio son específicas de repositorios concretos de Documentum. Puede proporcionar credenciales para cualquier número de repositorios; sin embargo, solo puede especificar un conjunto de credenciales por repositorio.

### Agregar una credencial de repositorio {#add-a-repository-credential}

1. En la consola de administración, haga clic en Servicios > Conector para Documentum de EMC > Configuración de Credenciales de Repositorio.
1. Haga clic en Agregar. Aparecerá la página Información de Credenciales de Sistema de Documentum.
1. Escriba un nombre para el repositorio.
1. Introduzca un nombre de usuario y una contraseña.
1. Haga clic en Guardar.

Si el Content Repository Connector para el servicio Documentum de EMC o el Repository Service para Documentum de EMC se están ejecutando, la información de las credenciales se verifica en relación con el repositorio especificado antes de almacenarse en la base de datos. Si las credenciales no son válidas o existen, se muestra un mensaje de error.

### Quitar una credencial de repositorio {#remove-a-repository-credential}

1. En la consola de administración, haga clic en Servicios > Conector para Documentum de EMC > Configuración.
1. Seleccione la casilla de verificación situada junto al repositorio desde la que desea quitar las credenciales y haga clic en Quitar. Las credenciales del repositorio seleccionado se eliminan de la base de datos.

### Cambiar el nombre de usuario y la contraseña de una credencial de repositorio {#change-the-user-name-and-password-for-a-repository-credential}

1. En la consola de administración, haga clic en Servicios > Conector para Documentum de EMC > Configuración.
1. Haga clic en el nombre del repositorio para editar las credenciales.
1. Cambie el nombre de usuario o la contraseña del repositorio, o ambos. (El nombre del repositorio es de solo lectura).
1. Haga clic en Guardar.

Si el Content Repository Connector para el servicio Documentum de EMC o el Repository Service para Documentum de EMC se están ejecutando, la información de las credenciales se verifica en relación con el repositorio especificado antes de almacenarse en la base de datos. Si las credenciales no son válidas o existen, se muestra un mensaje de error.

## Habilitar la solicitud para compartir colas de tareas de Workspace {#enable-the-request-for-sharing-of-workspace-task-queues}

Se requieren algunos pasos manuales para garantizar que la función Solicitud para compartir cola de tareas en Workspace funcione correctamente con Connector para Documentum de EMC.

1. Una vez que se hayan implementado AEM formularios y haya instalado Workbench, inicie sesión en Workbench y abra la vista Recursos. Determinará desde dónde se encuentra el archivo QueueSharing.swf de esta vista.
1. Arrastre el archivo QueueSharing.swf desde la vista Recursos hasta el escritorio de Windows o una ubicación equivalente, en función del sistema operativo.
1. En la consola de administración, haga clic en Servicios > Conector para Documentum de EMC > Configuración.
1. En Información del Proveedor de Servicios de Repositorio, cambie el proveedor de repositorios configurado a Proveedor de Repositorios de Documentum de EMC.
1. Inicie Workbench y copie el archivo QueueSharing.swf desde la ubicación en la que lo copió originalmente (por ejemplo, el escritorio de Windows u otra ubicación) en un directorio existente dentro del repositorio de Documentum de EMC.
1. En la vista Procesos de Workbench, abra el proceso Uso compartido de colas.
1. En la vista Variables, abra las propiedades de la variable &quot;theForm&quot; y cambie el URI para que coincida con la ruta en la que colocó el archivo QueueSharing.swf en el paso 5.
1. Guarde el proceso.
1. Migre el proceso al entorno de producción según la política de su organización.
