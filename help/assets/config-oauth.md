---
title: Configuración del etiquetado de recursos mediante el servicio de contenido inteligente
description: Obtenga información sobre cómo configurar el etiquetado inteligente y el etiquetado inteligente mejorado en [!DNL Adobe Experience Manager], mediante el servicio de contenido inteligente.
role: Admin
feature: Tagging,Smart Tags
solution: Experience Manager, Experience Manager Assets
source-git-commit: d8d821a64b39b312168733126de8929c04016ff1
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 8%

---

# Solución de problemas de etiquetas inteligentes para credenciales de OAuth {#oauth-config}

Se requiere una configuración de autorización abierta para adoptar el consentimiento para la [!DNL Adobe Experience Manager] para interactuar con Smart Content Services de forma segura.

>[!NOTE]
>
> No puede crear nuevas credenciales de JWT a partir de junio de 2024. A partir de ahora, solo se crean credenciales de servidor a servidor OAuth.
> La integración de JWT sigue funcionando hasta enero de 2025 solo para los usuarios de AMS y locales existentes.

## Configuración de OAuth para los nuevos usuarios de AMS {#oauth-config-existing-ams-users}

Consulte [configuración de servicios de contenido inteligente](#integrate-adobe-io) para la configuración de servicios de OAuth para un nuevo usuario. Una vez finalizado, siga estos pasos [pasos](#prereqs-config-oauth-onprem).

>[!NOTE]
>
>Si es necesario, puede enviar un ticket de asistencia siguiendo las [proceso de soporte](https://experienceleague.adobe.com/?lang=es&amp;support-tab=home?lang=es#support).

## Configuración de OAuth para los usuarios de AMS existentes {#oauth-config-new-ams-users}

Antes de realizar cualquiera de los pasos de esta metodología, es necesario implementar lo siguiente:

### Requisitos previos {#prereqs-config-oauth-onprem}

Una configuración de OAuth requiere los siguientes requisitos previos:

* Cree una nueva integración de OAuth en [Developer Console](https://developer.adobe.com/console/user/servicesandapis). Utilice el `ClientID`, `ClientSecret`, `OrgID`y otras propiedades en los pasos siguientes:
* Los siguientes archivos se pueden encontrar en esta ruta `/apps/system/config in crx/de`:
   * `com.**adobe**.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`
   * `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`

### Configuración de OAuth para los usuarios de AMS y OnPrem existentes {#steps-config-oauth-onprem}

El administrador del sistema puede realizar los siguientes pasos. El cliente de AMS puede ponerse en contacto con el representante del Adobe o enviar un ticket de asistencia después de la [proceso de soporte](https://experienceleague.adobe.com/?lang=es&amp;support-tab=home?lang=es#support).

1. Agregue o actualice las siguientes propiedades en `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`:

   * `auth.token.provider.authorization.grants="client_credentials"`
   * `auth.token.provider.orgId="<OrgID>"`
   * `auth.token.provider.default.claims=("\"iss\"\ :\ \"<OrgID>\"")`
   * `auth.token.provider.scope="read_pc.dma_smart_content,\ openid,\ AdobeID,\ additional_info.projectedProductContext"`
     `auth.token.validator.type="adobe-ims-similaritysearch"`
   * Actualice el `auth.token.provider.client.id` con el ID de cliente de la nueva configuración de OAuth.
   * Actualizar `auth.access.token.request` hasta `"https://ims-na1.adobelogin.com/ims/token/v3"`
1. Cambie el nombre del archivo a `com.adobe.granite.auth.oauth.accesstoken.provider-<randomnumber>.config`.
1. Siga estos pasos en `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`:
   * Actualice la propiedad auth.ims.client.secret con el Secreto del cliente desde la nueva integración de OAuth.
   * Cambie el nombre del archivo a `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl-<randomnumber>.config`
1. Guarde todos los cambios en la consola de desarrollo del repositorio de contenido, por ejemplo, CRXDE.
<!--
1. Navigate to `/system/console/configMgr` and replace the OSGi configuration from `.<randomnumber>` to `-<randomnumber>`.
1. Delete the old OSGi configuration for `"Access Token provider name: adobe-ims-similaritysearch"` in `/system/console/configMgr`.
-->
1. Entrada `System/console/configMgr`, elimine las configuraciones antiguas para `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl` Nombre del proveedor de token de acceso y `adobe-ims-similaritysearch`.
1. Reinicie la consola.

## Validar la configuración {#validate-the-configuration}

Una vez completada la configuración, puede utilizar un MBean de JMX para validar la configuración. Para validar, siga estos pasos.

1. Acceda a su [!DNL Experience Manager] servidor en `https://[aem_server]:[port]`.

1. Ir a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]** para abrir la consola OSGi. Clic **[!UICONTROL Principal] > [!UICONTROL JMX]**.

1. Haga clic en `com.day.cq.dam.similaritysearch.internal.impl`. Se abre **[!UICONTROL Tareas diversas de SimilaritySearch]**.

1. Haga clic en `validateConfigs()`. En el **[!UICONTROL Validar configuraciones]** , haga clic en **[!UICONTROL Invocar]**.

Los resultados de validación se muestran en el mismo cuadro de diálogo.

## Integración con la consola de Adobe Developer {#integrate-adobe-io}

Como nuevo usuario, al integrar con la consola de Adobe Developer, la variable [!DNL Experience Manager] El servidor de autentica las credenciales del servicio con la puerta de enlace de la consola de Adobe Developer antes de reenviar la solicitud al servicio de contenido inteligente. Para integrarse, necesita una cuenta de Adobe ID que tenga privilegios de administrador para la organización y una licencia de Smart Content Service comprada y habilitada para su organización.

Para configurar el servicio de contenido inteligente, siga estos pasos de nivel superior:

1. Para generar una clave pública, [crear un servicio de contenido inteligente](#obtain-public-certificate) configuración en [!DNL Experience Manager]. [Descargar un certificado público](#obtain-public-certificate) para la integración con OAuth.

1. *[No aplicable si es un usuario existente]* [creación de una integración en la consola de Adobe Developer](#create-adobe-i-o-integration).

1. [Configuración de la implementación](#configure-smart-content-service) mediante la clave de API y otras credenciales de la consola de Adobe Developer.

1. [Compruebe la configuración](#validate-the-configuration).

## Descargar un certificado público creando la configuración del servicio de contenido inteligente {#download-public-certificate}

Un certificado público permite autenticar el perfil en la consola de Adobe Developer.

1. En el [!DNL Experience Manager] interfaz de usuario, acceso **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Service heredados]**.

1. En la página Cloud Service, haga clic en **[!UICONTROL Configurar ahora]** bajo **[!UICONTROL Etiquetas inteligentes de recursos]**.

1. En el **[!UICONTROL Crear configuración]** , especifique un título y un nombre para la configuración de Etiquetas inteligentes. Haga clic en **[!UICONTROL Crear]**.

1. En el **[!UICONTROL AEM Servicio de contenido inteligente]** , utilice los siguientes valores:

   **[!UICONTROL URL de servicio]**: `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   Por ejemplo, `https://smartcontent.adobe.io/apac`. Puede especificar `na`, `emea`, o, `apac` como las regiones en las que está alojada la instancia de autor de Experience Manager.

   >[!NOTE]
   >
   >Si el servicio administrado de Experience Manager se aprovisiona antes del 1 de septiembre de 2022, utilice la siguiente URL de servicio:
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Servidor de autorización]**: `https://ims-na1.adobelogin.com`

   Deje los demás campos en blanco por ahora (se proporcionarán más adelante). Haz clic en **[!UICONTROL OK]**.

   ![Cuadro de diálogo Servicio de contenido inteligente del Experience Manager para proporcionar la URL del servicio de contenido](assets/aem_scs12.png)

   *Figura: Cuadro de diálogo Servicio de contenido inteligente para proporcionar la URL del servicio de contenido*

   >[!NOTE]
   >
   >La URL proporcionada como [!UICONTROL URL de servicio] no es accesible a través del explorador y genera un error 404. La configuración funciona correctamente con el mismo valor de [!UICONTROL URL de servicio] parámetro. Para ver el estado general del servicio y el programa de mantenimiento, consulte [https://status.adobe.com](https://status.adobe.com).

1. Clic **[!UICONTROL Descargar certificado público para la integración de OAuth]** y descargue el archivo de certificado público `AEM-SmartTags.crt`. Además, ya no es necesario cargar este certificado en la consola para desarrolladores de Adobe.

   ![Una representación de la configuración creada para el servicio de etiquetado inteligente](assets/smart-tags-download-public-cert1.png)

   *Imagen: configuración del servicio de etiquetado inteligente.*

## Creación de la integración de Adobe Developer Console {#create-adobe-i-o-integration}

Para utilizar las API del servicio de contenido inteligente, cree una integración en la consola de Adobe Developer para obtener lo siguiente [!UICONTROL Clave de API] (generado en [!UICONTROL ID DE CLIENTE] campo de integración de la consola de Adobe Developer), [!UICONTROL ID DE CUENTA TÉCNICA], [!UICONTROL ID DE ORGANIZACIÓN], y [!UICONTROL SECRETO DEL CLIENTE] para [!UICONTROL Configuración del servicio de etiquetado inteligente de recursos] de la configuración de nube en [!DNL Experience Manager].

1. Acceso [https://developer.adobe.com/console/](https://developer.adobe.com/console/) en un explorador. Seleccione la cuenta adecuada y compruebe que la función de organización asociada sea administrador del sistema.

1. Cree un proyecto con el nombre que desee. Haga clic en **[!UICONTROL Añadir API]**.

1. En la página **[!UICONTROL Añadir una API]** , seleccione **[!UICONTROL Experience Cloud]** y **[!UICONTROL Contenido inteligente]**. Haga clic en **[!UICONTROL Siguiente]**. 

1. Elija la **[!UICONTROL Servidor a servidor OAuth]** método de autenticación.

1. Agregar o modificar **[!UICONTROL Nombre de credencial]** según sea necesario. Haga clic en **[!UICONTROL Siguiente]**.

1. Seleccione el perfil de producto **[!UICONTROL Servicios de contenido inteligente]**. Clic **[!UICONTROL Guardar API configurada]**. La API de OAuth se agrega en las credenciales conectadas para su uso posterior. Puede copiar el [!UICONTROL Clave de API (ID de cliente)] o [!UICONTROL Generar token de acceso] de ella.
<!--
1. On the **[!UICONTROL Select product profiles]** page, select **[!UICONTROL Smart Content Services]**. Click **[!UICONTROL Save configured API]**.

   A page displays more information about the configuration. Keep this page open to copy and add these values in [!UICONTROL Assets Smart Tagging Service Settings] of cloud configuration in [!DNL Experience Manager] to configure smart tags.

   ![In the Overview tab, you can review the information provided for integration.](assets/integration_details.png)


   *Figure: Details of integration in Adobe Developer Console*
-->

![configuración de oauth](assets/oauth-config.png)
*Figura: Configuración de OAuth servidor a servidor en la consola de Adobe Developer*

## Configurar el servicio de contenido inteligente {#configure-smart-content-service}

Para configurar la integración, utilice los valores de [!UICONTROL ID DE CUENTA TÉCNICA], [!UICONTROL ID DE ORGANIZACIÓN], [!UICONTROL SECRETO DEL CLIENTE], y [!UICONTROL ID DE CLIENTE] desde la integración de la consola de Adobe Developer. La creación de una configuración de nube de etiquetas inteligentes permite la autenticación de solicitudes de API desde el [!DNL Experience Manager] implementación.

1. Entrada [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Service heredados]** para abrir [!UICONTROL Cloud Service] consola.

1. En el **[!UICONTROL Etiquetas inteligentes de recursos]**, abra la configuración creada anteriormente. En la página de configuración del servicio, haga clic en **[!UICONTROL Editar]**.

1. En el cuadro de diálogo **[!UICONTROL AEM Smart Content Service]**, utilice los valores predefinidos para los campos **[!UICONTROL URL de servicio]** y **[!UICONTROL Servidor de autorización]**.

1. Para los campos [!UICONTROL Clave de API], [!UICONTROL ID de cuenta técnica], [!UICONTROL ID de organización], y [!UICONTROL Secreto del cliente], copie y utilice los siguientes valores generados en [Integración de la consola Adobe Developer](#create-adobe-i-o-integration).

   | [!UICONTROL Configuración del servicio de etiquetado inteligente de recursos] | [!DNL Adobe Developer Console] campos de integración |
   |--- |--- |
   | [!UICONTROL Clave de API] | [!UICONTROL ID DE CLIENTE] |
   | [!UICONTROL ID de cuenta técnica] | [!UICONTROL ID DE CUENTA TÉCNICA] |
   | [!UICONTROL ID de organización] | [!UICONTROL ID DE ORGANIZACIÓN] |
   | [!UICONTROL Secreto del cliente] | [!UICONTROL SECRETO DEL CLIENTE] |

>[!MORELIKETHIS]
>
>* [Información general y formación sobre etiquetas inteligentes](enhanced-smart-tags.md)
>* [Configuración del etiquetado inteligente](config-smart-tagging.md)
>* [Tutorial de vídeo sobre etiquetas inteligentes](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)
