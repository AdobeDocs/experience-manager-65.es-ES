---
title: Configurar AEM Assets con Brand Portal
seo-title: Configurar AEM Assets con Brand Portal
description: Descubra cómo configurar AEM Assets con Brand Portal para publicar recursos y colecciones en Brand Portal.
seo-description: Descubra cómo configurar AEM Assets con Brand Portal para publicar recursos y colecciones en Brand Portal.
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: tm+mt
source-git-commit: 8633216807061c73f4bc692d13f9eba37845cffc
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 12%

---


# Configurar AEM Assets con Brand Portal {#configure-integration-65}

Adobe Experience Manager (AEM) Assets se configura con Brand Portal a través de Adobe Developer Console, que proporciona un distintivo IMS para la autorización del inquilino de Brand Portal.

>[!NOTE]
>
>La configuración de AEM Assets con Brand Portal mediante Adobe Developer Console es compatible con AEM 6.5.4.0 y versiones posteriores.
>
>Anteriormente, Brand Portal se configuraba mediante OAuth Gateway heredado, que utiliza el intercambio de tokens JWT para obtener un Token de acceso IMS para la autorización.
>
>La configuración mediante OAuth Gateway heredado ya no se admite a partir del 6 de abril de 2020 y se cambia a Adobe Developer Console.


>[!TIP]
>
>***Solo para clientes existentes***
>
>Se recomienda seguir utilizando la configuración heredada de OAuth Gateway. En caso de que surjan problemas con la configuración heredada de OAuth Gateway, elimine la configuración existente y cree una nueva mediante Adobe Developer Console.



Esta ayuda describe los dos casos de uso siguientes:
* [Nueva configuración](#configure-new-integration-65): Si es un usuario nuevo de Brand Portal y desea configurar la instancia de autor de AEM Assets con Brand Portal, puede crear una configuración en Adobe Developer Console.
* [Configuración](#upgrade-integration-65)de actualización: Si ya es usuario de Brand Portal y la instancia de autor de AEM Assets está configurada con Brand Portal en OAuth Gateway heredada, elimine la configuración existente y cree una nueva configuración en Adobe Developer Console.

La información proporcionada se basa en el supuesto de que cualquiera que lea esta Ayuda está familiarizado con las siguientes tecnologías:

* Instalación, configuración y administración de paquetes de Adobe Experience Manager y AEM.

* Uso de sistemas operativos Linux y Microsoft Windows.

## Requisitos previos {#prerequisites}

Para configurar AEM Assets con Brand Portal, es necesario lo siguiente:

* Una instancia de autor de AEM Assets activa y en ejecución con el último Service Pack.
* Dirección URL del inquilino de Brand Portal.
* Un usuario con privilegios de administrador del sistema en la organización IMS del inquilino de Brand Portal.


[Descargar e instalar AEM 6.5](#aemquickstart)

[Descargar e instalar AEM Service Pack más reciente](#servicepack)

### Descargar e instalar AEM 6.5 {#aemquickstart}

Se recomienda tener AEM 6.5 para configurar una instancia de autor AEM. Si no AEM en ejecución, descárguelo de las siguientes ubicaciones:

* Si ya es cliente de AEM, descargue AEM 6.5 del sitio web [de licencias de](http://licensing.adobe.com)Adobe.

* Si es socio de Adobe, utilice el Programa [de formación de socios de](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) Adobe para solicitar AEM 6.5.

Después de descargar AEM, para obtener instrucciones sobre cómo configurar una instancia de AEM autor, consulte [Implementación y mantenimiento](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/deploy.html#default-local-install).

### Descargar e instalar AEM último Service Pack {#servicepack}

Para obtener instrucciones detalladas, consulte

* [Notas de la versión de Service Pack de AEM 6.5](https://docs.adobe.com/content/help/en/experience-manager-65/release-notes/service-pack/sp-release-notes.html)

**Póngase en contacto con el Servicio de atención** al cliente si no puede encontrar el paquete de AEM o Service Pack más recientes.

## Crear configuración {#configure-new-integration-65}

La configuración de AEM Assets con Brand Portal requiere configuraciones tanto en la instancia de creación de AEM Assets como en la consola de desarrollador de Adobe.

1. En AEM Assets, cree una cuenta IMS y genere un certificado público (clave pública).
1. En Adobe Developer Console, cree un proyecto para el inquilino (organización) de Brand Portal.
1. En el proyecto, configure una API con la clave pública para crear una conexión de cuenta de servicio (JWT).
1. Obtenga las credenciales de la cuenta de servicio y la información de carga útil de JWT.
1. En AEM Assets, configure la cuenta IMS con las credenciales de cuenta de servicio y la carga útil JWT.
1. En AEM Assets, configure el servicio en la nube de Brand Portal con la cuenta IMS y el extremo de Brand Portal (dirección URL de la organización).
1. Pruebe la configuración publicando un recurso de AEM Assets en Brand Portal.


>[!NOTE]
>
>Una instancia de autor de AEM Assets solo se configurará con un inquilino de Brand Portal.



Realice los siguientes pasos en la secuencia mostrada si va a configurar AEM Assets con Brand Portal por primera vez:
1. [Obtener un certificado público](#public-certificate)
1. [Crear conexión de cuenta de servicio (JWT)](#createnewintegration)
1. [Configurar cuenta de IMS](#create-ims-account-configuration)
1. [Configurar el servicio en la nube](#configure-the-cloud-service)
1. [Probar la configuración](#test-integration)

### Crear la configuración de IMS {#create-ims-configuration}

La configuración de IMS autentica el inquilino de Brand Portal con la instancia de creación de AEM Assets.

La configuración de IMS incluye dos pasos:

* [Obtener un certificado público](#public-certificate)
* [Configurar cuenta de IMS](#create-ims-account-configuration)

### Obtener un certificado público {#public-certificate}

El certificado público le permite autenticar su perfil en Adobe Developer Console.

1. Inicie sesión en la instancia de creación de AEM Assets. La dirección URL predeterminada es
   `http://localhost:4502/aem/start.html`

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

   ![Interfaz de usuario de configuración de cuenta de Adobe IMS](assets/ims-config1.png)

1. En la página Configuraciones de IMS de Adobe, haga clic en **[!UICONTROL Crear]**.

1. Se le redirige a la página de configuración **[!UICONTROL de la cuenta técnica de IMS de]** Adobe. By default, the **Certificate** tab opens.

   Seleccione el portal **[!UICONTROL de marcas de]** Adobe de la solución de nube.

1. Mark the **[!UICONTROL Create new certificate]** checkbox and specify an **alias** for the certificate. El alias sirve como nombre del cuadro de diálogo.

1. Haga clic en **[!UICONTROL Crear certificado]**. A continuación, haga clic en **[!UICONTROL Aceptar]** en el cuadro de diálogo para generar el certificado público.

   ![Crear certificado](assets/ims-config2.png)

1. Click **[!UICONTROL Download Public Key]** and save the certificate (.crt) file on your machine.

   El archivo de certificado se utilizará más adelante para configurar la API para el inquilino de Brand Portal y generar las credenciales de cuenta de servicio en Adobe Developer Console.

   ![Descargar certificado](assets/ims-config3.png)

1. Haga clic en **[!UICONTROL Siguiente]**. 

   En la ficha **Cuenta** , se crea la cuenta IMS de Adobe, pero para ello necesitará las credenciales de cuenta de servicio que se generan en la Consola de programadores de Adobe. Mantenga esta página abierta por ahora.

   Abra una nueva ficha y [cree una conexión de cuenta de servicio (JWT) en Adobe Developer Console](#createnewintegration) para obtener las credenciales y la carga útil JWT para configurar la cuenta de IMS.

### Crear conexión de cuenta de servicio (JWT) {#createnewintegration}

En Adobe Developer Console, los proyectos y las API se configuran en el nivel de inquilino (organización) de Brand Portal. La configuración de una API crea una conexión de cuenta de servicio (JWT) en la consola de desarrollador de Adobe. Existen dos métodos para configurar la API, mediante la generación de un par de claves (claves privadas y públicas) o mediante la carga de una clave pública. Para configurar AEM Assets con Brand Portal, debe generar un certificado público (clave pública) en AEM Assets y crear credenciales en Adobe Developer Console cargando la clave pública. Esta clave pública se utiliza para configurar la API para el inquilino de Brand Portal seleccionado y genera las credenciales y la carga útil JWT para la cuenta de servicio. Estas credenciales se utilizan además para configurar la cuenta de IMS en AEM Assets. Una vez configurada la cuenta de IMS, puede configurar el servicio en la nube de Brand Portal en AEM Assets.

Realice los siguientes pasos para generar las credenciales de cuenta de servicio y la carga útil JWT:

1. Inicie sesión en Adobe Developer Console con privilegios de administrador del sistema en la organización de IMS (inquilino de Brand Portal). La dirección URL predeterminada es

   [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)


   >[!NOTE]
   >
   >Asegúrese de seleccionar la organización de IMS correcta (inquilino de Brand Portal) en la lista desplegable (organización) situada en la esquina superior derecha.

1. Click **[!UICONTROL Create new project]**. Se crea un proyecto en blanco para su organización.

   Haga clic en **[!UICONTROL Editar proyecto]** para actualizar el título **[!UICONTROL y la]** descripción **[!UICONTROL del]** proyecto y, a continuación, haga clic en **[!UICONTROL Guardar]**.

   ![Crear proyecto](assets/service-account1.png)

1. En la ficha Información general **[!UICONTROL del]** proyecto, haga clic en **[!UICONTROL Añadir API]**.

   ![Añadir API](assets/service-account2.png)

1. En la ventana **** Añadir una API, seleccione **[!UICONTROL AEM portal]** de marca y haga clic en **[!UICONTROL Siguiente]**.

   Asegúrese de tener acceso al servicio AEM Brand Portal.

1. En la ventana **[!UICONTROL Configurar API]** , haga clic en **[!UICONTROL Cargar la clave]** pública. A continuación, haga clic en **[!UICONTROL Seleccionar un archivo]** y cargue el certificado público (archivo .crt) que ha descargado en la sección [Obtener certificado](#public-certificate) público.

   Haga clic en **[!UICONTROL Siguiente]**. 

   ![Cargar clave pública](assets/service-account3.png)

1. Compruebe el certificado público y haga clic en **[!UICONTROL Siguiente]**.

1. Seleccione el portal **[!UICONTROL de marca perfil]** Assets del producto predeterminado y haga clic en **[!UICONTROL Guardar API]** configurada.

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![Seleccionar Perfil de producto](assets/service-account4.png)

1. Con la API configurada, se le redirige a la información general de la API. En el panel de navegación izquierdo, en **[!UICONTROL Credenciales]**, haga clic en Cuenta **[!UICONTROL de servicio (JWT)]**.

   >[!NOTE]
   >
   >Puede vista de las credenciales y realizar otras acciones (generar tokens JWT, copiar detalles de credenciales, recuperar el secreto del cliente, etc.) según sea necesario.

1. En la ficha **[!UICONTROL Credenciales]** de cliente, copie el ID **[!UICONTROL de]** cliente.

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![Credenciales de cuenta de servicio](assets/service-account5.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]**.

Ahora puede utilizar el ID de cliente (clave de API), el secreto de cliente y la carga útil JWT para [configurar la cuenta](#create-ims-account-configuration) IMS en AEM Assets.

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

### Configurar cuenta de IMS {#create-ims-account-configuration}

Asegúrese de haber realizado los siguientes pasos:

* [Obtener un certificado público](#public-certificate)
* [Crear conexión de cuenta de servicio (JWT)](#createnewintegration)

Realice los siguientes pasos para configurar la cuenta de IMS.

1. Abra la Configuración de IMS y vaya a la ficha **[!UICONTROL Cuenta]** . Mantuvo la página abierta mientras [obtenía el certificado](#public-certificate)público.

1. Especifique un **[!UICONTROL Título]** para la cuenta de IMS.

   En **[!UICONTROL Servidor de autorización]**, introduzca la dirección URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Pegue la clave **[!UICONTROL de]** API (ID de cliente), **[!UICONTROL Secreto]** de cliente y Carga **[!UICONTROL útil]** (carga útil JWT) que ha copiado al [crear la conexión](#createnewintegration)de cuenta de servicio (JWT).

   Haga clic en **[!UICONTROL Crear]**.

   La cuenta de IMS está configurada.

   ![Configuración de cuenta de IMS](assets/create-new-integration6.png)


1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Haga clic en **[!UICONTROL Proteger]** en el cuadro de diálogo. Si la configuración es correcta, aparece un mensaje que indica que el *token se recupera correctamente*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Sólo debe tener una configuración de IMS.
>
>Asegúrese de que la configuración de IMS pase la comprobación de estado. Si la configuración no pasa la comprobación de estado, no es válida. Debe eliminarla y crear una configuración nueva y válida.



### Configurar el servicio en la nube {#configure-the-cloud-service}

Siga los pasos siguientes para configurar el servicio en la nube de Brand Portal:

1. Inicie sesión en la instancia de creación de AEM Assets.

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. En la página Configuraciones de Brand Portal, haga clic en **[!UICONTROL Crear]**.

1. Especifique un **[!UICONTROL Título]** para la configuración.

   Seleccione la configuración de IMS que ha creado al [configurar la cuenta](#create-ims-account-configuration)de IMS.

   In the **[!UICONTROL Service URL]**, enter your Brand Portal tenant (organization URL).

   ![](assets/create-cloud-service.png)

1. Haga clic en **[!UICONTROL Guardar y cerrar]**. Se crea la configuración de nube.

   La instancia de autor de AEM Assets ahora está configurada con el inquilino de Brand Portal.

### Probar la configuración{#test-integration}

Realice los siguientes pasos para validar la configuración:

1. Inicie sesión en la instancia de AEM Assets Cloud.

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**.

   ![](assets/test-integration1.png)

1. En la página Replicación, haga clic en **[!UICONTROL Agentes en el autor]**.

   ![](assets/test-integration2.png)

1. Se crean cuatro agentes de replicación para cada inquilino.

   Busque los agentes de replicación del inquilino de Brand Portal.

   Haga clic en la dirección URL del agente de replicación.

   ![](assets/test-integration3.png)


   >[!NOTE]
   >
   >Los agentes de replicación trabajan en paralelo y comparten la distribución del trabajo por igual, aumentando así la velocidad de publicación en cuatro veces la velocidad original. Una vez configurado el servicio en la nube, no se requiere una configuración adicional para habilitar los agentes de replicación activados de forma predeterminada para habilitar la publicación en paralelo de varios recursos.


1. Para comprobar la conexión entre AEM Assets y Brand Portal, haga clic en **[!UICONTROL Probar conexión]**.

   ![](assets/test-integration4.png)

   Aparece un mensaje en la parte inferior de la página que indica que el *paquete de prueba se ha entregado correctamente.

   ![](assets/test-integration5.png)

1. Compruebe los resultados de la prueba en los cuatro agentes de replicación.


   >[!NOTE]
   >
   >Evite deshabilitar cualquiera de los agentes de replicación. Puede provocar errores en la replicación de algunos de los recursos.
   >
   >Asegúrese de que los cuatro agentes de replicación estén configurados para evitar errores de tiempo de espera. See [troubleshoot issues in parallel publishing to Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html#connection-timeout).

La instancia de autor de AEM Assets se ha configurado correctamente con Brand Portal y ahora puede:

* [Publicar recursos desde AEM Assets en Brand Portal](../assets/brand-portal-publish-assets.md)
* [Publicar carpetas desde AEM Assets en Brand Portal](../assets/brand-portal-publish-folder.md)
* [Publicar colecciones desde AEM Assets en Brand Portal](../assets/brand-portal-publish-collection.md)
* [Origen de recursos en Brand Portal](https://docs.adobe.com/content/help/es-ES/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) : Publique recursos de Brand Portal en AEM Assets.

## Configuración de actualización {#upgrade-integration-65}

Realice los siguientes pasos en la secuencia indicada para actualizar las configuraciones existentes:
1. [Verificar trabajos en ejecución](#verify-jobs)
1. [Eliminar configuraciones existentes](#delete-existing-configuration)
1. [Crear configuración](#configure-new-integration-65)

### Verificar trabajos en ejecución {#verify-jobs}

Asegúrese de que no se esté ejecutando ningún trabajo de publicación en la instancia de creación de AEM Assets antes de realizar ninguna modificación. Para ello, puede verificar los cuatro agentes de replicación y asegurarse de que las colas están inactivas.

1. Inicie sesión en la instancia de creación de AEM Assets.

1. En el panel **Herramientas** ![Herramientas](assets/do-not-localize/tools.png) , vaya a **[!UICONTROL Implementación]** > Replicación **[!UICONTROL de implementación]**.

1. En la página Replicación, haga clic en **[!UICONTROL Agentes en el autor]**.

   ![](assets/test-integration2.png)

1. Busque los agentes de replicación del inquilino de Brand Portal.

   Asegúrese de que la **cola esté inactiva** para todos los agentes de replicación y de que no haya ningún trabajo de publicación activo.

   ![](assets/test-integration3.png)

### Eliminar configuraciones existentes {#delete-existing-configuration}

Debe ejecutar la siguiente lista de comprobación mientras elimina las configuraciones existentes.
* Eliminar los cuatro agentes de replicación
* Eliminar el servicio en la nube de Brand Portal
* Eliminar usuario de MAC

1. Inicie sesión en la instancia de creación de AEM Assets y abra CRX Lite como administrador. La dirección URL predeterminada es

   `http://localhost:4502/crx/de/index.jsp`

1. Navegue hasta los cuatro agentes de replicación del inquilino de Brand Portal `/etc/replications/agents.author` y elimínelos.

   ![](assets/delete-replication-agent.png)

1. Vaya a la configuración `/etc/cloudservices/mediaportal` del **Cloud Service y elimínela**.

   ![](assets/delete-cloud-service.png)

1. Navegue hasta `/home/users/mac` y elimine el usuario **** MAC del inquilino de Brand Portal.

   ![](assets/delete-mac-user.png)


Ahora puede [crear la configuración](#configure-new-integration-65) mediante Adobe Developer Console en la instancia de creación de AEM 6.5.



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->


