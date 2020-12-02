---
title: Configuración de la administración segura para AEM Forms en JEE
seo-title: Configuración de la administración segura para AEM Forms en JEE
description: Obtenga información sobre cómo administrar cuentas de usuario y servicios que, aunque son necesarios en un entorno de desarrollo privado, no son necesarios en un entorno de producción de AEM Forms en JEE.
seo-description: Obtenga información sobre cómo administrar cuentas de usuario y servicios que, aunque son necesarios en un entorno de desarrollo privado, no son necesarios en un entorno de producción de AEM Forms en JEE.
uuid: 04e45d06-f57d-406c-8228-15f483199430
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: d211d8b0-e75f-49c3-808d-5d0e26ad3a6b
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---


# Configuración de la configuración de administración segura para AEM Forms en JEE {#configuring-secure-administration-settings-for-aem-forms-on-jee}

Obtenga información sobre cómo administrar cuentas de usuario y servicios que, aunque son necesarios en un entorno de desarrollo privado, no son necesarios en un entorno de producción de AEM Forms en JEE.

Generalmente, los desarrolladores no utilizan el entorno de producción para crear y probar sus aplicaciones. Por lo tanto, debe administrar cuentas de usuario y servicios que, aunque sean necesarios en un entorno de desarrollo privado, no sean necesarios en un entorno de producción.

Este artículo describe métodos para reducir la superficie de ataque global mediante las opciones de administración que proporciona AEM Forms en JEE.

## Desactivación del acceso remoto no esencial a los servicios {#disabling-non-essential-remote-access-to-services}

Después de instalar y configurar AEM Forms en JEE, hay muchos servicios disponibles para la invocación remota a través de SOAP y Enterprise JavaBeans™ (EJB). El término remoto, en este caso, hace referencia a cualquier llamante que tenga acceso de red a los puertos SOAP, EJB o Action Message Format (AMF) para el servidor de aplicaciones.

Aunque AEM Forms en los servicios JEE requiere que se pasen credenciales válidas para un llamante autorizado, solo debe permitir el acceso remoto a los servicios a los que necesita tener acceso remoto. Para lograr una accesibilidad limitada, debe reducir el conjunto de servicios de acceso remoto al mínimo posible para un sistema que funcione y, a continuación, habilitar la invocación remota para los servicios adicionales que necesite.

Los servicios de AEM Forms en JEE siempre necesitan al menos acceso SOAP. Estos servicios suelen ser necesarios para su uso en Workbench, pero también incluyen servicios a los que llama la aplicación web de Workspace.

Complete este procedimiento mediante la página web Aplicaciones y servicios de la Consola de administración:

1. Inicie sesión en la Consola de administración escribiendo la siguiente URL en un explorador Web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Haga clic en **Servicios > Aplicaciones y servicios > Preferencias**.
1. Configure las preferencias para que la vista alcance un máximo de 200 servicios y extremos en la misma página.
1. Haga clic en **Servicios** > **Aplicaciones y servicios** > **Administración de extremos**.
1. Seleccione **EJB** en la lista **Provider** y haga clic en **Filter**.
1. Para deshabilitar todos los extremos de EJB, active la casilla de verificación situada junto a cada uno de los extremos de la lista y haga clic en **Deshabilitar**.
1. Haga clic en **Siguiente** y repita el paso anterior para todos los extremos de EJB. Asegúrese de que EJB aparece en la columna Proveedor antes de deshabilitar los extremos.
1. Seleccione **SOAP** en la lista **Provider** y haga clic en **Filter**.
1. Para eliminar los extremos de SOAP, active la casilla de verificación situada junto a cada uno de los extremos de la lista y haga clic en **Eliminar**. No elimine los puntos finales siguientes:

   * AuthenticationManagerService
   * DirectoryManagerService
   * JobManager
   * evento_management_service
   * evento_configuration_service
   * ProcessManager
   * TemplateManager
   * RepositoryService
   * TaskManagerService
   * TaskQueueManager
   * TaskManagerQueryService
   * WorkspaceSingleSignOn
   * ApplicationManager

1. Haga clic en **Siguiente** y repita el paso anterior para los extremos de SOAP que no se encuentran en la lista anterior. Asegúrese de que SOAP aparece en la columna Proveedor antes de eliminar los extremos.

## Desactivación del acceso anónimo no esencial a los servicios {#disabling-non-essential-anonymous-access-to-services}

Algunos servicios de servidor de formularios permiten la invocación no autenticada (anónima) en algunas operaciones. Esto significa que una o más operaciones expuestas por el servicio pueden invocarse como un usuario autenticado o como un usuario no autenticado.

1. Inicie sesión en la consola de administración escribiendo la siguiente URL en un explorador Web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Haga clic en **Servicios > Aplicaciones y servicios > Administración de servicios**.
1. Haga clic en el nombre del servicio que desea deshabilitar (por ejemplo, AuthenticationManagerService).
1. Haga clic en la ficha **Seguridad**, anule la selección de **Acceso anónimo permitido** y haga clic en **Guardar**.
1. Complete los pasos 3 y 4 para los siguientes servicios:

   * AuthenticationManagerService
   * EJB
   * Correo electrónico
   * JobManager
   * WatchedFolder
   * UsermanagerUtilService
   * Remoto
   * RepositoryProviderService
   * EMCDocumentumRepositoryProvider
   * IBMFilenetRepositoryProvider
   * FormAugmenter
   * TaskManagerService
   * TaskManagerConnector
   * TaskManagerQueryService
   * TaskQueueManager
   * TaskEndpointManager
   * UserService
   * WorkspaceSearchTemplateService
   * WorkspacePropertyService
   * OutputService
   * FormsService

   Si desea exponer cualquiera de estos servicios para la invocación remota, también debe considerar la posibilidad de desactivar el acceso anónimo a estos servicios. De lo contrario, cualquier llamante con acceso de red a este servicio puede invocar el servicio sin pasar credenciales válidas.

   El acceso anónimo debe deshabilitarse para cualquier servicio que no sea necesario. Muchos servicios internos requieren que se habilite la autenticación anónima, ya que es necesario que cualquier usuario potencial del sistema los invoque sin tener autorización previa.

## Cambio del tiempo de espera global predeterminado {#changing-the-default-global-time-out}

Los usuarios finales pueden autenticarse en AEM Forms a través de Workbench, aplicaciones web de AEM Forms o aplicaciones personalizadas que invocan servicios de servidor de AEM Forms. Se utiliza una configuración de tiempo de espera global para especificar cuánto tiempo pueden estos usuarios interactuar con AEM Forms (mediante una afirmación basada en SAML) antes de que se vean obligados a volver a autenticarse. La configuración predeterminada es de dos horas. En un entorno de producción, la cantidad de tiempo debe reducirse al número mínimo de minutos aceptable.

### Minimizar el límite de tiempo de reautenticación {#minimize-reauthentication-time-limit}

1. Inicie sesión en la consola de administración escribiendo la siguiente URL en un explorador Web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Haga clic en **Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración**.
1. Haga clic en **Exportar** para generar un archivo config.xml con la configuración de AEM Forms existente.
1. Abra el archivo XML en un editor y busque la siguiente entrada:

   `<entry key=”assertionValidityInMinutes” value=”120”/>`

1. Cambie el valor a cualquier número bueno de 5 (en minutos) y guarde el archivo.
1. En la consola de administración, vaya a la página Importar y exportar archivos de configuración.
1. Introduzca la ruta al archivo config.xml modificado o haga clic en Examinar para ir a él.
1. Haga clic en **Importar** para cargar el archivo config.xml modificado y, a continuación, haga clic en **Aceptar**.

