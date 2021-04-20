---
title: Configurar AEM Assets con Brand Portal
seo-title: Configurar AEM Assets con Brand Portal
description: Obtenga información sobre cómo configurar AEM Assets con Brand Portal para publicar recursos y colecciones en Brand Portal.
seo-description: Obtenga información sobre cómo configurar AEM Assets con Brand Portal para publicar recursos y colecciones en Brand Portal.
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
feature: Brand Portal
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2087'
ht-degree: 12%

---


# Configurar AEM Assets con Brand Portal {#configure-integration-65}

Adobe Experience Manager Assets Brand Portal le permite publicar recursos de marca aprobados de Adobe Experience Manager Assets en Brand Portal y distribuirlos a los usuarios de Brand Portal.

AEM Assets se configura con Brand Portal a través de Adobe Developer Console, que obtiene un token de cuenta de Adobe Identity Management Services (IMS) para la autorización del inquilino de Brand Portal.

>[!NOTE]
>
>La configuración de AEM Assets con Brand Portal a través de Adobe Developer Console es compatible con AEM 6.5.4.0 y versiones posteriores.
>
>Anteriormente, Brand Portal se configuraba mediante la puerta de enlace OAuth heredada, que utiliza el intercambio de tokens web JSON (JWT) para obtener un token de acceso IMS para la autorización.
>
>La configuración mediante la puerta de enlace OAuth heredada ya no es compatible a partir del 6 de abril de 2020 y se cambia a Adobe Developer Console.

>[!TIP]
>
>***Solo para clientes existentes***
>
>Se recomienda seguir utilizando la configuración heredada de OAuth Gateway. En caso de que surjan problemas con la configuración heredada de OAuth Gateway, elimine la configuración existente y cree una nueva configuración a través de Adobe Developer Console.

Esta ayuda describe los dos casos de uso siguientes:

* [Nueva configuración](#configure-new-integration-65): Si es un nuevo usuario de Brand Portal y desea configurar la instancia de autor de AEM Assets con Brand Portal, puede crear la configuración a través de Adobe Developer Console.
* [Actualización de la configuración](#upgrade-integration-65): Si ya es un usuario de Brand Portal que tiene una configuración en la puerta de enlace OAuth heredada, elimine la configuración existente y cree una nueva configuración a través de Adobe Developer Console.

La información proporcionada se basa en el supuesto de que cualquier persona que lea esta Ayuda está familiarizada con las siguientes tecnologías:

* Instalación, configuración y administración de paquetes de Adobe Experience Manager y AEM.

* Uso de sistemas operativos Linux y Microsoft Windows.

## Requisitos previos {#prerequisites}

Para configurar AEM Assets con Brand Portal, es necesario lo siguiente:

* Una instancia de autor de AEM Assets en ejecución con el Service Pack más reciente
* Una URL de inquilino de Brand Portal
* Un usuario con privilegios de administrador del sistema en la organización IMS del inquilino de Brand Portal

[Descargar e instalar AEM 6.5](#aemquickstart)

[Descargar e instalar AEM Service Pack más reciente](#servicepack)

### Descargar e instalar AEM 6.5 {#aemquickstart}

Se recomienda tener AEM 6.5 para configurar una instancia de autor AEM. Si no tiene AEM en funcionamiento, descárguelo desde las siguientes ubicaciones:

* Si ya es cliente de AEM, descargue AEM 6.5 del [sitio web de licencias de Adobe](http://licensing.adobe.com).

* Si es socio de Adobe, utilice el [Programa de formación de socios de Adobe](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) para solicitar AEM 6.5.

Después de descargar AEM, para obtener instrucciones para configurar una instancia de autor AEM, consulte [implementación y mantenimiento](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/deploy.html#default-local-install).

### Descargue e instale AEM último Service Pack {#servicepack}

Para obtener instrucciones detalladas, consulte

* [Notas de la versión de Service Pack de AEM 6.5](https://docs.adobe.com/content/help/es-ES/experience-manager-65/release-notes/service-pack/sp-release-notes.html)

**Póngase en contacto con** soporte técnico si no puede encontrar el paquete de AEM o Service Pack más reciente.

## Crear configuración {#configure-new-integration-65}

La configuración de AEM Assets con Brand Portal requiere configuraciones tanto en la instancia de autor de AEM Assets como en la consola de desarrollador de Adobe.

1. En AEM Assets, cree una cuenta de IMS y genere un certificado público (clave pública).
1. En Adobe Developer Console, cree un proyecto para el inquilino (organización) de Brand Portal.
1. En el proyecto, configure una API con la clave pública para crear una conexión de cuenta de servicio (JWT).
1. Obtenga las credenciales de cuenta de servicio y la información de carga útil de JWT.
1. En AEM Assets, configure la cuenta IMS con las credenciales de cuenta de servicio y la carga útil JWT.
1. En AEM Assets, configure el servicio en la nube de Brand Portal con la cuenta IMS y el extremo de Brand Portal (URL de la organización).
1. Pruebe la configuración publicando un recurso de AEM Assets en Brand Portal.

>[!NOTE]
>
>Una instancia de autor de AEM Assets solo se debe configurar con un inquilino de Brand Portal.

Realice los siguientes pasos en la secuencia indicada si configura AEM Assets con Brand Portal por primera vez:
1. [Obtener un certificado público](#public-certificate)
1. [Crear conexión de cuenta de servicio (JWT)](#createnewintegration)
1. [Configurar la cuenta de IMS](#create-ims-account-configuration)
1. [Configurar el servicio en la nube](#configure-the-cloud-service)
1. [Probar la configuración](#test-integration)

### Crear la configuración de IMS {#create-ims-configuration}

La configuración de IMS autentica la instancia de autor de AEM Assets con el inquilino de Brand Portal.

La configuración de IMS incluye dos pasos:

* [Obtener un certificado público](#public-certificate)
* [Configurar la cuenta de IMS](#create-ims-account-configuration)

### Obtener un certificado público {#public-certificate}

La clave pública (certificado) autentica el perfil en Adobe Developer Console.

1. Inicie sesión en la instancia de autor de AEM Assets. La dirección URL predeterminada es `http://localhost:4502/aem/start.html`.

1. En el panel **Herramientas** ![Herramientas](assets/do-not-localize/tools.png), vaya a **[!UICONTROL Seguridad]** > **[!UICONTROL Configuraciones de IMS de Adobe]**.

1. En la página Configuraciones de IMS de Adobe, haga clic en **[!UICONTROL Crear]**. Se redirigirá a la página **[!UICONTROL Configuración de cuenta técnica de IMS de Adobe]**. De forma predeterminada, se abre la pestaña **Certificate**.

1. Seleccione **[!UICONTROL Adobe Brand Portal]** en la lista desplegable **[!UICONTROL Cloud Solution]**.

1. Seleccione la casilla **[!UICONTROL Create new certificate]** y especifique un **alias** para la clave pública. El alias sirve como nombre de la clave pública.

1. Haga clic en **[!UICONTROL Crear certificado]**. A continuación, haga clic en **[!UICONTROL OK]** para generar la clave pública.

   ![Crear certificado](assets/ims-config2.png)

1. Haga clic en el icono **[!UICONTROL Descargar clave pública]** y guarde el archivo de clave pública (.crt) en el equipo.

   La clave pública se utilizará más adelante para configurar la API para el inquilino de Brand Portal y generar credenciales de cuenta de servicio en Adobe Developer Console.

   ![Descargar certificado](assets/ims-config3.png)

1. Haga clic en **[!UICONTROL Siguiente]**. 

   En la pestaña **Account**, se crea la cuenta IMS de Adobe, que requiere las credenciales de cuenta de servicio que se generan en Adobe Developer Console. Mantenga esta página abierta por ahora.

   Abra una nueva pestaña y [cree una conexión de cuenta de servicio (JWT) en Adobe Developer Console](#createnewintegration) para obtener las credenciales y la carga útil JWT para configurar la cuenta de IMS.

### Crear conexión de cuenta de servicio (JWT) {#createnewintegration}

En Adobe Developer Console, los proyectos y las API se configuran en el nivel de inquilino (organización) de Brand Portal. La configuración de una API crea una conexión de cuenta de servicio (JWT). Existen dos métodos para configurar la API, mediante la generación de un par de claves (claves privadas y públicas) o cargando una clave pública. Para configurar AEM Assets con Brand Portal, debe generar una clave pública (certificado) en AEM Assets y crear credenciales en Adobe Developer Console cargando la clave pública. Estas credenciales son necesarias para configurar la cuenta de IMS en AEM Assets. Una vez configurada la cuenta de IMS, puede configurar el servicio en la nube de Brand Portal en AEM Assets.

Realice los siguientes pasos para generar las credenciales de cuenta de servicio y la carga útil JWT:

1. Inicie sesión en Adobe Developer Console con privilegios de administrador del sistema en la organización IMS (inquilino de Brand Portal). La dirección URL predeterminada es [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Asegúrese de seleccionar la organización de IMS correcta (inquilino de Brand Portal) en la lista desplegable (organización) situada en la esquina superior derecha.

1. Haga clic en **[!UICONTROL Crear nuevo proyecto]**. Se crea un proyecto en blanco con un nombre generado por el sistema para su organización.

   Haga clic en **[!UICONTROL Editar proyecto]** para actualizar el **[!UICONTROL Título del proyecto]** y **[!UICONTROL Descripción]** y haga clic en **[!UICONTROL Guardar]**.

1. En la pestaña **[!UICONTROL Project overview]**, haga clic en **[!UICONTROL Add API]**.

1. En **[!UICONTROL Add an API window]**, seleccione **[!UICONTROL AEM Brand Portal]** y haga clic en **[!UICONTROL Next]**.

   Asegúrese de tener acceso al servicio AEM Brand Portal.

1. En la ventana **[!UICONTROL Configure API]**, haga clic en **[!UICONTROL Upload your public key]**. A continuación, haga clic en **[!UICONTROL Seleccionar un archivo]** y cargue la clave pública (archivo .crt) que descargó en la sección [obtener certificado público](#public-certificate).

   Haga clic en **[!UICONTROL Siguiente]**. 

   ![Cargar clave pública](assets/service-account3.png)

1. Compruebe la clave pública y haga clic en **[!UICONTROL Next]**.

1. Seleccione **[!UICONTROL Assets Brand Portal]** como perfil de producto predeterminado y haga clic en **[!UICONTROL Guardar API configurada]**.

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![Seleccionar perfil de producto](assets/service-account4.png)

1. Una vez configurada la API, se le redirige a la página de información general de la API. En el panel de navegación izquierdo de **[!UICONTROL Credentials]**, haga clic en la opción **[!UICONTROL Service Account (JWT)]**.

   >[!NOTE]
   >
   >Puede ver las credenciales y realizar acciones como generar tokens JWT, copiar detalles de credenciales, recuperar secreto de cliente, etc.

1. En la pestaña **[!UICONTROL Client Credentials]**, copie el **[!UICONTROL client ID]**.

   Haga clic en **[!UICONTROL Recuperar secreto de cliente]** y copie el **[!UICONTROL secreto de cliente]**.

   ![Credenciales de cuenta de servicio](assets/service-account5.png)

1. Vaya a la pestaña **[!UICONTROL Generate JWT]** y copie la información **[!UICONTROL JWT Payload]**.

Ahora puede utilizar el ID de cliente (clave de API), el secreto del cliente y la carga útil JWT para [configurar la cuenta de IMS](#create-ims-account-configuration) en AEM Assets.

<!--
### Create Adobe I/O integration {#createnewintegration}

Adobe I/O integration generates API Key, Client Secret, and Payload (JWT) which is required in setting up the IMS Account configurations.

1. Login to Adobe I/O Console with system administrator privileges on the IMS organization of the Brand Portal tenant.

   Default URL: [https://console.adobe.io/](https://console.adobe.io/) 

1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create a new integration page opens. 
   
   Select your organization from the drop-down list.

   In **[!UICONTROL Experience Cloud]**, Select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Continue]**. 

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. If you do not know your organization, contact your administrator.

   ![Create Integration](assets/create-new-integration2.png)

1. Specify a name and description for the integration. Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. Select the profile of your organization. 

   Or, select the default profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Create Integration]**. The integration is created.

1. Click **[!UICONTROL Continue to integration details]** to view the integration information. 

   Copy the **[!UICONTROL API Key]** 
   
   Click **[!UICONTROL Retrieve Client Secret]** and copy the Client Secret key.

   ![API Key, Client Secret, and payload information of an integration](assets/create-new-integration3.png)

1. Navigate to **[!UICONTROL JWT]** tab, and copy the **[!UICONTROL JWT payload]**.

   The API Key, Client Secret key, and JWT payload information will be used to create IMS account configuration.
-->

### Configurar la cuenta de IMS {#create-ims-account-configuration}

Asegúrese de haber realizado los siguientes pasos:

* [Obtener un certificado público](#public-certificate)
* [Crear conexión de cuenta de servicio (JWT)](#createnewintegration)

Realice los siguientes pasos para configurar la cuenta de IMS.

1. Abra la configuración de IMS y vaya a la pestaña **[!UICONTROL Account]**. Mantuvo la página abierta mientras [obtenía el certificado público](#public-certificate).

1. Especifique un **[!UICONTROL Título]** para la cuenta de IMS.

   En el campo **[!UICONTROL Servidor de autorización]**, especifique la dirección URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   Especifique el ID de cliente en el campo **[!UICONTROL API key]**, **[!UICONTROL Client Secret]** y **[!UICONTROL Payload]** (carga útil JWT) que ha copiado mientras [crea la conexión de cuenta de servicio (JWT)](#createnewintegration).

   Haga clic en **[!UICONTROL Crear]**.

   La cuenta de IMS está configurada.

   ![Configuración de cuenta de IMS](assets/create-new-integration6.png)

1. Seleccione la configuración de la cuenta de IMS y haga clic en **[!UICONTROL Comprobar estado]**.

   Haga clic en **[!UICONTROL Check]** en el cuadro de diálogo. Si la configuración es correcta, aparece un mensaje que indica que el *Token se recupera correctamente*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Sólo debe tener una configuración de IMS.
>
>Asegúrese de que la configuración de IMS pase la comprobación de estado. Si la configuración no pasa la comprobación de estado, no es válida. Debe eliminarla y crear una configuración nueva y válida.

### Configurar el servicio en la nube {#configure-the-cloud-service}

Siga estos pasos para configurar el servicio en la nube de Brand Portal:

1. Inicie sesión en la instancia de autor de AEM Assets.

1. En el panel **Herramientas** ![Herramientas](assets/do-not-localize/tools.png), vaya a **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. En la página Configuraciones de Brand Portal, haga clic en **[!UICONTROL Crear]**.

1. Especifique un **[!UICONTROL Título]** para la configuración.

   Seleccione la configuración de IMS que ha creado mientras [configura la cuenta de IMS](#create-ims-account-configuration).

   En el campo **[!UICONTROL Service URL]** , especifique la dirección URL del inquilino (organización) de Brand Portal.

   ![](assets/create-cloud-service.png)

1. Haga clic en **[!UICONTROL Guardar y cerrar]**. Se crea la configuración de nube.

   La instancia de autor de AEM Assets ahora está configurada con el inquilino de Brand Portal.

### Probar la configuración{#test-integration}

Realice los siguientes pasos para validar la configuración:

1. Inicie sesión en la instancia de nube de AEM Assets.

1. En el panel **Herramientas** ![Herramientas](assets/do-not-localize/tools.png), vaya a **[!UICONTROL Implementación]** > **[!UICONTROL Replicación]**.

   ![](assets/test-integration1.png)

1. En la página Replicación, haga clic en **[!UICONTROL Agentes del autor]**.

   ![](assets/test-integration2.png)

   Puede ver los cuatro agentes de replicación creados para el inquilino de Brand Portal.

   Busque los agentes de replicación del inquilino de Brand Portal y haga clic en la URL del agente de replicación.

   ![](assets/test-integration3.png)

   >[!NOTE]
   >
   >Los agentes de replicación trabajan en paralelo y comparten la distribución del trabajo por igual, aumentando así la velocidad de publicación en cuatro veces la velocidad original. Una vez configurado el servicio en la nube, no se requiere una configuración adicional para habilitar los agentes de replicación activados de forma predeterminada para permitir la publicación en paralelo de varios recursos.

1. Para verificar la conexión entre AEM Assets y Brand Portal, haga clic en el icono **[!UICONTROL Probar conexión]**.

   ![](assets/test-integration4.png)

   Aparece un mensaje que el paquete de prueba *se entrega correctamente*.

   ![](assets/test-integration5.png)

1. Compruebe los resultados de la prueba en los cuatro agentes de replicación.


   >[!NOTE]
   >
   >Evite desactivar cualquiera de los agentes de replicación, ya que puede provocar errores en la replicación de los recursos (que se ejecutan en la cola).
   >
   >Asegúrese de que los cuatro agentes de replicación estén configurados para evitar errores de tiempo de espera. Consulte [solución de problemas en la publicación paralela en Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html#connection-timeout).

Ahora puede:

* [Publicar recursos desde AEM Assets en Brand Portal](../assets/brand-portal-publish-assets.md)
* [Publicar recursos desde Brand Portal en AEM Assets](https://docs.adobe.com/content/help/es-ES/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) : abastecimiento de recursos en Brand Portal
* [Publicar carpetas desde AEM Assets en Brand Portal](../assets/brand-portal-publish-folder.md)
* [Publicar colecciones desde AEM Assets en Brand Portal](../assets/brand-portal-publish-collection.md)
* [Publicar ajustes preestablecidos, esquemas y facetas en Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicar etiquetas en Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

Consulte la [documentación de Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) para obtener más información.


## Actualización de la configuración {#upgrade-integration-65}

Siga estos pasos en la secuencia indicada para actualizar las configuraciones existentes a Adobe Developer Console:
1. [Comprobar trabajos en ejecución](#verify-jobs)
1. [Eliminar configuraciones existentes](#delete-existing-configuration)
1. [Crear configuración](#configure-new-integration-65)

### Comprobar trabajos en ejecución {#verify-jobs}

Asegúrese de que no se esté ejecutando ningún trabajo de publicación en la instancia de autor de AEM Assets antes de realizar ninguna modificación. Para ello, puede verificar el estado de los trabajos activos en los cuatro agentes de replicación y asegurarse de que las colas estén inactivas.

1. Inicie sesión en la instancia de autor de AEM Assets.

1. En el panel **Herramientas** ![Herramientas](assets/do-not-localize/tools.png), vaya a **[!UICONTROL Implementación]** > **[!UICONTROL Replicación de implementación]**.

1. En la página Replicación, haga clic en **[!UICONTROL Agentes del autor]**.

   ![](assets/test-integration2.png)

1. Busque los agentes de replicación del inquilino de Brand Portal.

   Asegúrese de que la **Cola esté inactiva** para todos los agentes de replicación, que no haya ningún trabajo de publicación activo.

   ![](assets/test-integration3.png)

### Eliminar configuraciones existentes {#delete-existing-configuration}

Debe ejecutar la siguiente lista de comprobación al eliminar las configuraciones existentes:
* Eliminar los cuatro agentes de replicación
* Eliminar el servicio en la nube de Brand Portal
* Eliminar usuario MAC

1. Inicie sesión en la instancia de autor de AEM Assets y abra CRX Lite como administrador. La dirección URL predeterminada es `http://localhost:4502/crx/de/index.jsp`.

1. Vaya a `/etc/replications/agents.author` y elimine los cuatro agentes de replicación del inquilino de Brand Portal.

   ![](assets/delete-replication-agent.png)

1. Vaya a `/etc/cloudservices/mediaportal` y elimine la configuración del servicio en la nube de Brand Portal.

   ![](assets/delete-cloud-service.png)

1. Vaya a `/home/users/mac` y elimine el **usuario MAC** del inquilino de Brand Portal.

   ![](assets/delete-mac-user.png)


Ahora puede [crear configuración](#configure-new-integration-65) a través de Adobe Developer Console en la instancia de autor de AEM 6.5.



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->


