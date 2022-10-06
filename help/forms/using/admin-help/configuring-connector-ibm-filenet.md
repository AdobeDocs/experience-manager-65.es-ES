---
title: Configuración del conector para IBM FileNet
seo-title: Configuring Connector for IBM FileNet
description: Aprenda a configurar el conector para IBM FileNet para permitir la comunicación entre AEM formularios y IBM FileNet.
seo-description: Learn how to configure the Connector for IBM FileNet to enable communication between AEM forms and IBM FileNet.
uuid: 29d4e221-97f7-4cfb-b7e4-75a8289d2604
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: be4994de-12f8-436e-926a-49a6783b006e
exl-id: f4045df5-a35b-41d7-910e-971017148597
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 1%

---

# Configuración del conector para IBM FileNet {#configuring-connector-for-ibm-filenet}

El conector para IBM FileNet permite la comunicación entre AEM formularios y IBM FileNet. Para obtener más información, consulte &quot;Conectores para ECM&quot; en [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>En versiones anteriores, los recursos se podían almacenar en un repositorio de ECM. En esta versión, los recursos se almacenan en el repositorio nativo de formularios de AEM y los servicios del proveedor de repositorios se han desaprobado. La migración de recursos de un repositorio ECM al repositorio de formularios AEM se realiza al realizar una actualización a AEM formularios. Para obtener más información, consulte la guía de actualización de formularios AEM para su servidor de aplicaciones.

## Configuración de la conexión con el motor de contenido {#configure-the-connection-to-the-content-engine}

IBM FileNet P8 Content Engine proporciona servicios de software para administrar contenido empresarial y objetos de negocio definidos por el cliente en repositorios de contenido de FileNet.

1. En la consola de administración, haga clic en Servicios > Conector para IBM FileNet.
1. En el cuadro URL del motor de contenido, introduzca la dirección URL de conexión completa. Por ejemplo:

   Si utiliza el motor de contenido de FileNet 4.x con transporte CEWS, introduzca:

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   Si está utilizando el motor de contenido de FileNet 4.x con el transporte de EJB, que solo es compatible con WebLogic, introduzca:

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. En la lista Esquema de protección Credencial, seleccione uno de estos niveles de protección:

   * **Borrar:** Envía credenciales a través de la red en un modo no protegido
   * **Simétrico:** Envía credenciales cifradas a través de la red

1. En el cuadro Ubicación del archivo de codificación, introduzca la ruta al archivo de codificación:

   * Si seleccionó Borrar como esquema de protección de credenciales, se ignorarán esta palabra clave y su valor.
   * Si seleccionó Simétrico como esquema de protección de credenciales, la ruta que introduzca señala a la ubicación de un archivo de codificación en el servidor de formularios que contiene las claves criptográficas que se van a utilizar.

1. En el cuadro Almacén de objetos predeterminado, introduzca el conector del almacén de objetos al que AEM formularios se conecta de forma predeterminada.
1. En el cuadro Nombre de usuario, introduzca el nombre de usuario de un usuario que tenga derechos de acceso al almacén de objetos predeterminado especificado en el paso anterior.
1. En el cuadro Contraseña, introduzca la contraseña del usuario y haga clic en Guardar.

## Configuración de los ajustes del motor de proceso {#configure-the-process-engine-settings}

El conector para IBM FileNet contiene el conector del motor de proceso para el servicio IBM FileNet, que se utiliza para interactuar con el motor de proceso IBM FileNet. Puede configurar las opciones de este servicio.

1. En la consola de administración, haga clic en Servicios > Conector para IBM FileNet.
1. Para habilitar el uso del conector del motor de proceso para el servicio FileNet de IBM, seleccione Usar el servicio del conector del motor de proceso.
1. En el cuadro Enrutador de proceso/Punto de conexión, introduzca el nombre de host o la dirección IP y el número de puerto seguido del nombre del enrutador de proceso. Por ejemplo:

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. En el cuadro Nombre de usuario, introduzca el nombre de usuario que se utiliza para conectarse al motor de proceso.
1. En el cuadro Contraseña, introduzca la contraseña utilizada para conectarse al motor de proceso y haga clic en Guardar.

## Validación de la configuración del servicio {#validation-of-service-settings}

Si introduce un nombre de usuario o una contraseña incorrectos al configurar la conexión con el motor de contenido o la configuración del motor de proceso, obtendrá los siguientes resultados, en función de si los servicios se están ejecutando actualmente:

* Si se detienen el servicio Proveedor de Repositorios para IBM FileNet y el conector de Repositorio de Contenido para el servicio IBM FileNet, al guardar la información de configuración del servicio, no aparece ningún error. Sin embargo, la próxima vez que inicie el servicio, se generará una excepción y el servicio no se iniciará.
* Si se inicia el servicio Proveedor del repositorio para IBM FileNet o el conector del repositorio de contenido para el servicio IBM FileNet, al guardar la información de configuración del servicio, el servicio intenta validar la información de las credenciales inmediatamente. En este caso, se produce un error y la información de configuración no se guarda.

## Cambiar el proveedor de servicios de repositorio {#change-the-repository-service-provider}

Puede configurar qué proveedor de servicios de repositorio utilizar con FileNet. Las llamadas al servicio del repositorio se delegan al proveedor que configure.

Las opciones disponibles son las siguientes:

**Nombre actual del proveedor del repositorio:** Nombre del proveedor de servicios de repositorio actual

**Proveedor de repositorio de IBM FileNet:** Hace que el proveedor de repositorios de FileNet sea el proveedor del repositorio. Esta opción está en desuso.

**proveedor de repositorios:** Convierte al proveedor de repositorios nativo en el proveedor del repositorio

>[!NOTE]
>
>Para seleccionar un proveedor de servicios de repositorio que no esté en la lista, configure RepositoryService en Aplicaciones y Servicios. <!-- Fix broken link(See Managing Services) -->

1. En la consola de administración, haga clic en Servicios > Conector para IBM FileNet.
1. En el área Información del proveedor de servicios de repositorio, seleccione el proveedor de servicios de repositorio alternativo y, a continuación, haga clic en Guardar.
