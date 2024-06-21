---
title: Configurar el conector para IBM FileNet
description: Obtenga información sobre cómo configurar el conector de IBM AEM FileNet para habilitar la comunicación entre los formularios de y IBM FileNet.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORM
exl-id: f4045df5-a35b-41d7-910e-971017148597
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 2%

---

# Configurar el conector para IBM FileNet {#configuring-connector-for-ibm-filenet}

El conector para IBM AEM FileNet permite la comunicación entre los formularios de y IBM FileNet. Para obtener más información, consulte &quot;Conectores para ECM&quot; en [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>En versiones anteriores, los recursos se podían almacenar en un repositorio de ECM. AEM En esta versión, los recursos se almacenan en el repositorio nativo de los formularios de los formularios de la aplicación y los servicios del proveedor de repositorios se han quedado obsoletos. AEM AEM La migración de recursos de un repositorio de ECM al repositorio de formularios de la se realiza al actualizar a formularios de la aplicación de forma libre. AEM Para obtener más información, consulte la Guía de actualización de formularios de la aplicación para su servidor de aplicaciones.

## Configuración de la conexión con el motor de contenido {#configure-the-connection-to-the-content-engine}

El motor de contenido IBM FileNet P8 proporciona servicios de software para administrar contenido empresarial y objetos empresariales definidos por el cliente en repositorios de contenido FileNet.

1. En la consola de administración, haga clic en Servicios > Conector para IBM FileNet.
1. En el cuadro URL del motor de contenido, introduzca la URL de conexión completa. Por ejemplo:

   Si utiliza FileNet Content Engine 4.x con transporte CEWS, introduzca:

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   Si está utilizando el motor de contenido FileNet 4.x con transporte EJB, que solo es compatible con WebLogic, introduzca:

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. En la lista Esquema de protección de credenciales, seleccione uno de estos niveles de protección:

   * **Borrar:** Envía credenciales a través de la red en modo no protegido
   * **Simétrico:** Envía credenciales cifradas por la red

1. En el cuadro Ubicación del archivo de cifrado, escriba la ruta de acceso al archivo de cifrado:

   * Si seleccionó Borrar como esquema de protección de credenciales, se omitirán esta palabra clave y su valor.
   * Si ha seleccionado Simétrico como esquema de protección de credenciales, la ruta de acceso que ha especificado apunta a la ubicación de un archivo de cifrado en el servidor de Forms que contiene las claves criptográficas que se van a utilizar.

1. AEM En el cuadro Almacén de objetos predeterminado, escriba el conector del almacén de objetos al que se conecta de forma predeterminada el formulario de la forma de la aplicación.
1. En el cuadro Nombre de usuario, escriba el nombre de usuario de un usuario que tenga derechos de acceso al almacén de objetos predeterminado especificado en el paso anterior.
1. En el cuadro Contraseña, escriba la contraseña del usuario y haga clic en Guardar.

## Configuración del motor de proceso {#configure-the-process-engine-settings}

Connector for IBM FileNet contiene el servicio Process Engine Connector for IBM FileNet, que se utiliza para interactuar con IBM FileNet Process Engine. Puede configurar las opciones de este servicio.

1. En la consola de administración, haga clic en Servicios > Conector para IBM FileNet.
1. Para habilitar el uso del conector del motor de procesos para el servicio FileNet de IBM, seleccione Usar el servicio del conector del motor de procesos.
1. En el cuadro Punto de conexión/enrutador de proceso, escriba el nombre de host o la dirección IP y el número de puerto seguidos del nombre del enrutador de proceso. Por ejemplo:

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. En el cuadro Nombre de usuario, introduzca el nombre de usuario que se utiliza para conectarse al motor de proceso.
1. En el cuadro Contraseña, introduzca la contraseña utilizada para conectarse al motor de proceso y haga clic en Guardar.

## Validación de la configuración del servicio {#validation-of-service-settings}

Si introduce un nombre de usuario o una contraseña incorrectos al configurar la conexión con el motor de contenido o la configuración del motor de procesos, obtendrá los siguientes resultados, en función de si los servicios se están ejecutando actualmente:

* Si se detienen tanto el servicio Proveedor de repositorios para IBM FileNet como el Conector del repositorio de contenido para el servicio FileNet de IBM, al guardar la información de configuración del servicio, no aparece ningún error. Sin embargo, la próxima vez que inicie el servicio, se producirá una excepción y el servicio no se iniciará.
* Si se inicia el servicio Proveedor de repositorio para IBM FileNet o el Conector del repositorio de contenido para el servicio IBM FileNet, al guardar la información de configuración del servicio, el servicio intenta validar la información de credenciales inmediatamente. En este caso, se produce un error y la información de configuración no se guarda.

## Cambio del proveedor de servicios del repositorio {#change-the-repository-service-provider}

Puede configurar qué proveedor de servicios de repositorio utilizar con FileNet. Las llamadas al servicio del repositorio se delegan al proveedor que configure.

Las opciones disponibles son las siguientes:

**Nombre del proveedor del repositorio actual:** El nombre del proveedor de servicios del repositorio actual

**Proveedor del repositorio de IBM FileNet:** Convierte al proveedor del repositorio de FileNet en el proveedor del repositorio. Esta opción ha quedado obsoleta.

**proveedor del repositorio:** Convierte al proveedor del repositorio nativo en el proveedor del repositorio

>[!NOTE]
>
>Para seleccionar un proveedor de servicios de repositorio distinto de los enumerados, configure RepositoryService en Aplicaciones y servicios. <!-- Fix broken link(See Managing Services) -->

1. En la consola de administración, haga clic en Servicios > Conector para IBM FileNet.
1. En el área Información del proveedor de servicios de repositorio, seleccione el proveedor de servicios de repositorio alternativo y, a continuación, haga clic en Guardar.
