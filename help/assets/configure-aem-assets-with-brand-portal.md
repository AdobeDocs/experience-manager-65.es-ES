---
title: Configurar AEM Assets con Brand Portal
seo-title: Configure AEM Assets with Brand Portal
description: Obtenga información sobre cómo configurar AEM Assets con Brand Portal para publicar recursos y colecciones en Brand Portal.
seo-description: Learn how to configure AEM Assets with Brand Portal for publishing assets and Collections to Brand Portal.
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
feature: Brand Portal
role: Admin
exl-id: ae33181c-9eec-421c-be55-4bd019de40b8
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '2088'
ht-degree: 12%

---

# Configurar AEM Assets con Brand Portal {#configure-integration-65}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=en) |
| AEM 6.5 | Este artículo |
| AEM 6.4 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/brandportal/configure-aem-assets-with-brand-portal.html?lang=es) |

Adobe Experience Manager Assets Brand Portal le permite publicar en Brand Portal recursos de marca aprobados de Adobe Experience Manager Assets y distribuirlos a los usuarios de Brand Portal.

AEM Assets se configura con Brand Portal mediante la consola de Adobe Developer, que obtiene un token de cuenta de Identity Management Services (IMS) de Adobe para la autorización del inquilino de Brand Portal.

>[!NOTE]
>
>La configuración de AEM Assets con Brand Portal mediante la consola de Adobe Developer es compatible con la AEM 6.5.4.0 y versiones posteriores.
>
>Anteriormente, Brand Portal se configuraba mediante la puerta de enlace OAuth heredada, que utiliza el intercambio de tokens web JSON (JWT) para obtener un token de acceso IMS para la autorización.
>
>La configuración a través de la puerta de enlace OAuth heredada ya no es compatible a partir del 6 de abril de 2020 y se cambia a la consola de Adobe Developer.

>[!TIP]
>
>***Solo para clientes existentes***
>
>Se recomienda seguir utilizando la configuración heredada de OAuth Gateway. En caso de que surjan problemas con la configuración heredada de la puerta de enlace de OAuth, elimine la configuración existente y cree una nueva configuración a través de la consola de Adobe Developer.

Esta ayuda describe los dos casos de uso siguientes:

* [Nueva configuración](#configure-new-integration-65): Si es un nuevo usuario de Brand Portal y desea configurar la instancia de autor de AEM Assets con Brand Portal, puede crear la configuración a través de la consola de Adobe Developer.
* [Actualización de la configuración](#upgrade-integration-65): Si ya es un usuario de Brand Portal con configuración en la puerta de enlace OAuth heredada, elimine la configuración existente y cree una nueva configuración a través de la consola de Adobe Developer.

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

* Si ya es cliente de AEM, descargue AEM 6.5 desde [Sitio web de licencias de Adobe](https://licensing.adobe.com).

* Si es socio de Adobe, utilice [Programa de formación para socios de Adobe](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) para solicitar AEM 6.5.

Después de descargar AEM, para obtener instrucciones para configurar una instancia de autor de AEM, consulte [implementación y mantenimiento](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html#default-local-install).

### Descargar e instalar AEM último Service Pack {#servicepack}

Para obtener instrucciones detalladas, consulte

* [Notas de la versión de Service Pack de AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html?lang=es)

**Contacto con el servicio de asistencia** si no puede encontrar el paquete de AEM o Service Pack más reciente.

## Crear configuración {#configure-new-integration-65}

La configuración de AEM Assets con Brand Portal requiere configuraciones tanto en la instancia de autor de AEM Assets como en la consola de Adobe Developer.

1. En AEM Assets, cree una cuenta de IMS y genere un certificado público (clave pública).
1. En Adobe Developer Console, cree un proyecto para el inquilino (organización) de Brand Portal.
1. En el proyecto, configure una API con la clave pública para crear una conexión de cuenta de servicio (JWT).
1. Obtenga las credenciales de cuenta de servicio y la información de carga útil de JWT.
1. En AEM Assets, configure la cuenta IMS con las credenciales de cuenta de servicio y la carga útil JWT.
1. En AEM Assets, configure el servicio en la nube de Brand Portal con la cuenta IMS y el extremo de Brand Portal (URL de organización).
1. Pruebe la configuración publicando un recurso de AEM Assets a Brand Portal.

>[!NOTE]
>
>Una instancia de autor de AEM Assets solo se debe configurar con un inquilino de Brand Portal.

Realice los siguientes pasos en la secuencia indicada si configura AEM Assets con Brand Portal por primera vez:
1. [Obtener un certificado público](#public-certificate)
1. [Crear conexión de cuenta de servicio (JWT)](#createnewintegration)
1. [Configurar la cuenta de IMS](#create-ims-account-configuration)
1. [Configurar el servicio en la nube de ](#configure-the-cloud-service)
1. [Probar la configuración](#test-integration)

### Crear la configuración de IMS {#create-ims-configuration}

La configuración de IMS autentica la instancia de autor de AEM Assets con el inquilino de Brand Portal.

La configuración de IMS incluye dos pasos:

* [Obtener un certificado público](#public-certificate)
* [Configurar la cuenta de IMS](#create-ims-account-configuration)

### Obtener un certificado público {#public-certificate}

La clave pública (certificado) autentica el perfil en la consola de Adobe Developer.

1. Inicie sesión en la instancia de autor de AEM Assets. El URL predeterminado es `http://localhost:4502/aem/start.html`.

1. En el **Herramientas** ![Herramientas](assets/do-not-localize/tools.png) , vaya a **[!UICONTROL Seguridad]** > **[!UICONTROL Configuraciones de IMS de Adobe]**.

1. En la página Configuraciones de IMS de Adobe , haga clic en **[!UICONTROL Crear]**. Se redireccionará a la variable **[!UICONTROL Configuración de cuenta técnica de Adobe IMS]** página. De forma predeterminada, la variable **Certificado** se abre.

1. Select **[!UICONTROL Adobe Brand Portal]** en el **[!UICONTROL Solución en la nube]** lista desplegable.

1. Seleccione el **[!UICONTROL Crear nuevo certificado]** y especifique un **alias** para la clave pública. El alias sirve como nombre de la clave pública.

1. Haga clic en **[!UICONTROL Crear certificado]**. A continuación, haga clic en **[!UICONTROL OK]** para generar la clave pública.

   ![Crear certificado](assets/ims-config2.png)

1. Haga clic en el **[!UICONTROL Descargar clave pública]** y guarde el archivo de clave pública (.crt) en el equipo.

   La clave pública se utilizará más adelante para configurar la API para el inquilino de Brand Portal y generar credenciales de cuenta de servicio en la consola de Adobe Developer.

   ![Descargar certificado](assets/ims-config3.png)

1. Haga clic en **[!UICONTROL Siguiente]**. 

   En el **Cuenta** , se crea la cuenta de Adobe IMS, que requiere las credenciales de cuenta de servicio generadas en la consola de Adobe Developer. Mantenga esta página abierta por ahora.

   Abra una nueva pestaña y [crear una conexión de cuenta de servicio (JWT) en la consola de Adobe Developer](#createnewintegration) para obtener las credenciales y la carga útil JWT para configurar la cuenta de IMS.

### Crear conexión de cuenta de servicio (JWT) {#createnewintegration}

En la consola de Adobe Developer, los proyectos y las API se configuran en el nivel de inquilino (organización) de Brand Portal. La configuración de una API crea una conexión de cuenta de servicio (JWT). Existen dos métodos para configurar la API, mediante la generación de un par de claves (claves privadas y públicas) o cargando una clave pública. Para configurar AEM Assets con Brand Portal, debe generar una clave pública (certificado) en AEM Assets y crear credenciales en la consola de Adobe Developer cargando la clave pública. Estas credenciales son necesarias para configurar la cuenta de IMS en AEM Assets. Una vez configurada la cuenta de IMS, puede configurar el servicio en la nube de Brand Portal en AEM Assets.

Realice los siguientes pasos para generar las credenciales de cuenta de servicio y la carga útil JWT:

1. Inicie sesión en la consola de Adobe Developer con privilegios de administrador del sistema en la organización IMS (inquilino de Brand Portal). La dirección URL predeterminada es [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Asegúrese de seleccionar la organización de IMS (inquilino de Brand Portal) correcta en la lista desplegable (organización) situada en la esquina superior derecha.

1. Haga clic en **[!UICONTROL Crear nuevo proyecto]**. Se crea un proyecto en blanco con un nombre generado por el sistema para su organización.

   Haga clic en **[!UICONTROL Editar proyecto]** para actualizar el **[!UICONTROL Título del proyecto]** y **[!UICONTROL Descripción]** y haga clic en **[!UICONTROL Guardar]**.

1. En el **[!UICONTROL Información general del proyecto]** , haga clic en **[!UICONTROL Añadir API]**.

1. En el **[!UICONTROL Añadir una ventana de API]**, seleccione **[!UICONTROL AEM Brand Portal]** y haga clic en **[!UICONTROL Siguiente]**.

   Asegúrese de tener acceso al servicio AEM Brand Portal.

1. En el **[!UICONTROL Configuración de API]** ventana, haga clic en **[!UICONTROL Cargar la clave pública]**. A continuación, haga clic en **[!UICONTROL Seleccionar un archivo]** y cargue la clave pública (archivo .crt) que descargó en la variable [obtener certificado público](#public-certificate) para obtener más información.

   Haga clic en **[!UICONTROL Siguiente]**.

   ![Cargar clave pública](assets/service-account3.png)

1. Compruebe la clave pública y haga clic en **[!UICONTROL Siguiente]**.

1. Select **[!UICONTROL Assets Brand Portal]** como perfil de producto predeterminado y haga clic en **[!UICONTROL Guardar la API configurada]**.

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![Seleccionar perfil de producto](assets/service-account4.png)

1. Una vez configurada la API, se le redirige a la página de información general de la API. Desde la navegación izquierda debajo de **[!UICONTROL Credenciales]**, haga clic en el botón **[!UICONTROL Cuenta de servicio (JWT)]** .

   >[!NOTE]
   >
   >Puede ver las credenciales y realizar acciones como generar tokens JWT, copiar detalles de credenciales, recuperar secreto de cliente, etc.

1. En el **[!UICONTROL Credenciales del cliente]** , copie la **[!UICONTROL ID de cliente]**.

   Haga clic en **[!UICONTROL Recuperar secreto de cliente]** y copie el **[!UICONTROL secreto de cliente]**.

   ![Credenciales de cuenta de servicio](assets/service-account5.png)

1. Vaya a la **[!UICONTROL Generar JWT]** y copie **[!UICONTROL Carga útil JWT]** información.

Ahora puede utilizar el ID de cliente (clave de API), el secreto del cliente y la carga útil JWT para [configurar la cuenta IMS](#create-ims-account-configuration) en AEM Assets.

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

1. Abra la configuración de IMS y vaya a la **[!UICONTROL Cuenta]** pestaña . Mantuvo la página abierta mientras [obtención del certificado público](#public-certificate).

1. Especifique un **[!UICONTROL Título]** para la cuenta de IMS.

   En el **[!UICONTROL Servidor de autorización]** especifique la dirección URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   Especifique el ID de cliente en la variable **[!UICONTROL Clave de API]** field, **[!UICONTROL Secreto del cliente]** y **[!UICONTROL Carga útil]** (carga útil JWT) que ha copiado mientras [creación de la conexión de cuenta de servicio (JWT)](#createnewintegration).

   Haga clic en **[!UICONTROL Crear]**.

   La cuenta de IMS está configurada.

   ![Configuración de cuenta de IMS](assets/create-new-integration6.png)

1. Seleccione la configuración de la cuenta de IMS y haga clic en **[!UICONTROL Comprobar estado]**.

   Haga clic en **[!UICONTROL Marque]** en el cuadro de diálogo. Si la configuración se realiza correctamente, aparece un mensaje que indica que la variable *El token se recupera correctamente*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Sólo debe tener una configuración de IMS.
>
>Asegúrese de que la configuración de IMS pase la comprobación de estado. Si la configuración no pasa la comprobación de estado, no es válida. Debe eliminarla y crear una configuración nueva y válida.

### Configurar el servicio en la nube de  {#configure-the-cloud-service}

Siga estos pasos para configurar el servicio en la nube de Brand Portal:

1. Inicie sesión en la instancia de autor de AEM Assets.

1. En el **Herramientas** ![Herramientas](assets/do-not-localize/tools.png) , vaya a **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. En la página Configuraciones de Brand Portal , haga clic en **[!UICONTROL Crear]**.

1. Especifique un **[!UICONTROL Título]** para la configuración.

   Seleccione la configuración de IMS que ha creado mientras [configuración de la cuenta IMS](#create-ims-account-configuration).

   En el **[!UICONTROL URL del servicio]** especifique la URL del inquilino (organización) de Brand Portal.

   ![](assets/create-cloud-service.png)

1. Haga clic en **[!UICONTROL Guardar y cerrar]**. Se crea la configuración de nube.

   La instancia de autor de AEM Assets ahora está configurada con el inquilino de Brand Portal.

### Probar la configuración {#test-integration}

Realice los siguientes pasos para validar la configuración:

1. Inicie sesión en la instancia de nube de AEM Assets.

1. En el **Herramientas** ![Herramientas](assets/do-not-localize/tools.png) , vaya a **[!UICONTROL Implementación]** > **[!UICONTROL Replicación]**.

   ![](assets/test-integration1.png)

1. En la página Replicación, haga clic en **[!UICONTROL Agentes en autor]**.

   ![](assets/test-integration2.png)

   Puede ver los cuatro agentes de replicación creados para su inquilino de Brand Portal.

   Busque los agentes de replicación de su inquilino de Brand Portal y haga clic en la URL del agente de replicación.

   ![](assets/test-integration3.png)

   >[!NOTE]
   >
   >Los agentes de replicación trabajan en paralelo y comparten la distribución del trabajo por igual, aumentando así la velocidad de publicación en cuatro veces la velocidad original. Una vez configurado el servicio en la nube, no se requiere una configuración adicional para habilitar los agentes de replicación activados de forma predeterminada para permitir la publicación en paralelo de varios recursos.

1. Para comprobar la conexión entre AEM Assets y Brand Portal, haga clic en el botón **[!UICONTROL Probar conexión]** icono.

   ![](assets/test-integration4.png)

   Aparece un mensaje que indica que *el paquete de prueba se entrega correctamente*.

   ![](assets/test-integration5.png)

1. Compruebe los resultados de la prueba en los cuatro agentes de replicación.


   >[!NOTE]
   >
   >Evite desactivar cualquiera de los agentes de replicación, ya que puede provocar errores en la replicación de los recursos (que se ejecutan en la cola).
   >
   >Asegúrese de que los cuatro agentes de replicación estén configurados para evitar errores de tiempo de espera. Consulte [solución de problemas en la publicación paralela de Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html#connection-timeout).
   >
   >No modifique ninguna configuración generada automáticamente.

Ahora puede:

* [Publicar recursos desde AEM Assets en Brand Portal](../assets/brand-portal-publish-assets.md)
* [Publicar recursos de Brand Portal en AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=es) - Abastecimiento de recursos en Brand Portal
* [Publicar carpetas desde AEM Assets en Brand Portal](../assets/brand-portal-publish-folder.md)
* [Publicar colecciones desde AEM Assets en Brand Portal](../assets/brand-portal-publish-collection.md)
* [Publicar ajustes preestablecidos, esquemas y facetas en Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicar etiquetas en Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

Consulte [Documentación de Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para obtener más información.


## Actualización de la configuración {#upgrade-integration-65}

Siga estos pasos en la secuencia indicada para actualizar las configuraciones existentes a la consola de Adobe Developer:
1. [Comprobar trabajos en ejecución](#verify-jobs)
1. [Eliminar configuraciones existentes](#delete-existing-configuration)
1. [Crear configuración](#configure-new-integration-65)

### Comprobar trabajos en ejecución {#verify-jobs}

Asegúrese de que no se esté ejecutando ningún trabajo de publicación en la instancia de autor de AEM Assets antes de realizar ninguna modificación. Para ello, puede verificar el estado de los trabajos activos en los cuatro agentes de replicación y asegurarse de que las colas estén inactivas.

1. Inicie sesión en la instancia de autor de AEM Assets.

1. En el **Herramientas** ![Herramientas](assets/do-not-localize/tools.png) , vaya a **[!UICONTROL Implementación]** > **[!UICONTROL Replicación de implementación]**.

1. En la página Replicación, haga clic en **[!UICONTROL Agentes en autor]**.

   ![](assets/test-integration2.png)

1. Busque los agentes de replicación del inquilino de Brand Portal.

   Asegúrese de que la variable **La cola está inactiva** para todos los agentes de replicación, no hay ningún trabajo de publicación activo.

   ![](assets/test-integration3.png)

### Eliminar configuraciones existentes {#delete-existing-configuration}

Debe ejecutar la siguiente lista de comprobación al eliminar las configuraciones existentes:
* Eliminar los cuatro agentes de replicación
* Eliminar el servicio en la nube de Brand Portal
* Eliminar usuario de MAC

1. Inicie sesión en la instancia de autor de AEM Assets y abra CRX Lite como administrador. El URL predeterminado es `http://localhost:4502/crx/de/index.jsp`.

1. Vaya a `/etc/replications/agents.author` y elimine los cuatro agentes de replicación del inquilino de Brand Portal.

   ![](assets/delete-replication-agent.png)

1. Vaya a `/etc/cloudservices/mediaportal` y elimine la configuración del servicio en la nube de Brand Portal.

   ![](assets/delete-cloud-service.png)

1. Vaya a `/home/users/mac` y elimine el **Usuario de Mac** del inquilino de Brand Portal.

   ![](assets/delete-mac-user.png)


Ahora puede [crear configuración](#configure-new-integration-65) mediante la consola de Adobe Developer en la instancia de autor de AEM 6.5.



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
