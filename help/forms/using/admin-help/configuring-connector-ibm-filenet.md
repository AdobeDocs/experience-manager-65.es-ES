---
title: Configuración del Conector para IBM FileNet
seo-title: Configuración del Conector para IBM FileNet
description: Obtenga información sobre cómo configurar Connector para IBM FileNet para habilitar la comunicación entre AEM formularios y IBM FileNet.
seo-description: Obtenga información sobre cómo configurar Connector para IBM FileNet para habilitar la comunicación entre AEM formularios y IBM FileNet.
uuid: 29d4e221-97f7-4cfb-b7e4-75a8289d2604
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: be4994de-12f8-436e-926a-49a6783b006e
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 1%

---


# Configuración del Conector para IBM FileNet {#configuring-connector-for-ibm-filenet}

Connector for IBM FileNet permite la comunicación entre AEM formularios y IBM FileNet. Para obtener más información, consulte &quot;Conectores para ECM&quot; en [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>En versiones anteriores, los recursos se podían almacenar en un repositorio de ECM. En esta versión, los recursos se almacenan en el repositorio nativo de formularios de AEM y los servicios del proveedor de repositorios se han quedado obsoletos. La migración de recursos de un repositorio de ECM al repositorio de formularios AEM se realiza cuando se realiza una actualización a AEM formularios. Para obtener más información, consulte la guía de actualización de formularios AEM para su servidor de aplicaciones.

## Configurar la conexión con el motor de contenido {#configure-the-connection-to-the-content-engine}

IBM FileNet P8 Content Engine proporciona servicios de software para administrar contenido empresarial y objetos de negocios definidos por el cliente en repositorios de contenido FileNet.

1. En la consola de administración, haga clic en Servicios > Conector para IBM FileNet.
1. En el cuadro URL del motor de contenido, introduzca la dirección URL de conexión completa. Por ejemplo:

   Si utiliza FileNet Content Engine 4.x con transporte CEWS, introduzca:

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   Si está utilizando FileNet Content Engine 4.x con transporte EJB, que solo es compatible con WebLogic, introduzca:

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. En la lista Esquema de protección de credenciales, seleccione uno de estos niveles de protección:

   * **Borrar:** envía credenciales a través de la red en modo no protegido
   * **Simétrico:** envía credenciales cifradas a través de la red

1. En el cuadro Ubicación del archivo de codificación, introduzca la ruta del archivo de codificación:

   * Si seleccionó Borrar como el esquema de protección de credenciales, se ignorarán esta palabra clave y su valor.
   * Si seleccionó Simétrico como el esquema de protección de credenciales, la ruta que introduzca señalará a la ubicación de un archivo de codificación en el servidor de formularios que contenga las claves criptográficas que se utilizarán.

1. En el cuadro Almacén de objetos predeterminado, introduzca el conector del almacén de objetos al que AEM formularios se conectan de forma predeterminada.
1. En el cuadro Nombre de usuario, introduzca el nombre de usuario de un usuario que tenga derechos de acceso al almacén de objetos predeterminado que especificó en el paso anterior.
1. En el cuadro Contraseña, introduzca la contraseña del usuario y haga clic en Guardar.

## Configurar la configuración del motor de proceso {#configure-the-process-engine-settings}

Connector for IBM FileNet contiene el servicio Process Engine Connector para IBM FileNet, que se utiliza para interactuar con IBM FileNet Process Engine. Puede configurar las opciones de este servicio.

1. En la consola de administración, haga clic en Servicios > Conector para IBM FileNet.
1. Para habilitar el uso del conector de motor de proceso para el servicio FileNet de IBM, seleccione Utilizar el servicio de conector de motor de proceso.
1. En el cuadro Enrutador de proceso/Punto de conexión, introduzca el nombre de host o la dirección IP y el número de puerto seguido del nombre del enrutador de proceso. Por ejemplo:

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. En el cuadro Nombre de usuario, introduzca el nombre de usuario que se utiliza para conectarse al motor de proceso.
1. En el cuadro Contraseña, introduzca la contraseña que se utiliza para conectarse al motor de proceso y haga clic en Guardar.

## Validación de la configuración del servicio {#validation-of-service-settings}

Si introduce un nombre de usuario o una contraseña incorrectos al configurar la conexión con el motor de contenido o la configuración del motor de proceso, obtendrá los siguientes resultados, según si los servicios se están ejecutando en ese momento:

* Si se detienen tanto el servicio Proveedor de Repositorios para IBM FileNet como el conector de repositorio de contenido para IBM FileNet, al guardar la información de configuración de servicio no aparece ningún error. Sin embargo, la próxima vez que inicio el servicio, se generará una excepción y el servicio no se inicio.
* Si se inicia el servicio Proveedor del repositorio para IBM FileNet o el conector del repositorio de contenido para IBM FileNet, al guardar la información de configuración del servicio, el servicio intenta validar la información de las credenciales inmediatamente. En este caso, se produce un error y la información de configuración no se guarda.

## Cambiar el proveedor de servicio del repositorio {#change-the-repository-service-provider}

Puede configurar qué proveedor de servicio de repositorio utilizar con FileNet. Las llamadas al servicio de repositorio se delegan al proveedor que configure.

Las opciones disponibles son las siguientes:

**Nombre actual del proveedor del repositorio:** El nombre del proveedor de servicio del repositorio actual

**Proveedor de repositorio de IBM FileNet:** convierte al proveedor de repositorio de FileNet en el proveedor del repositorio para el repositorio. Esta opción está en desuso.

**proveedor de repositorio:** convierte al proveedor de repositorio nativo en el proveedor del repositorio

>[!NOTE]
>
>Para seleccionar un proveedor de servicio de repositorio distinto de los enumerados, configure RepositoryService en Aplicaciones y servicios. <!-- Fix broken link(See Managing Services) -->

1. En la consola de administración, haga clic en Servicios > Conector para IBM FileNet.
1. En el área Información del Proveedor de servicio del repositorio, seleccione el proveedor de servicio del repositorio alternativo y, a continuación, haga clic en Guardar.
