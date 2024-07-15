---
title: Configuración de la integración de AEM Assets con Experience Cloud
description: Obtenga información sobre cómo configurar la integración de AEM Assets con Experience Cloud.
contentOwner: AG
feature: Asset Management
role: User, Architect, Admin
exl-id: d167cf97-6829-45a7-ba46-2239d530b060
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 0%

---

# Configuración de la integración de AEM Assets con Experience Cloud {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}

Si es cliente de Adobe Experience Cloud, puede sincronizar sus recursos en Adobe Experience Manager Assets con Adobe Creative Cloud y a la inversa. También puede sincronizar sus recursos con Experience Cloud y a la inversa. Puede configurar esta sincronización mediante [!DNL Adobe I/O]. El nombre actualizado de [!DNL Adobe Marketing Cloud] es [!DNL Adobe Experience Cloud].

El flujo de trabajo para configurar esta integración es:

1. Cree una autenticación en [!DNL Adobe I/O] mediante una puerta de enlace pública y obtenga un id. de aplicación.
1. Cree un perfil en la instancia de AEM Assets utilizando el ID de aplicación.
1. Utilice esta configuración para sincronizar los recursos.

AEM En el backend, el servidor de autentica el perfil con la puerta de enlace y, a continuación, sincroniza los datos entre Assets y el Experience Cloud.

>[!NOTE]
>
>Esta característica está obsoleta en [!DNL Assets]. AEM Encuentre reemplazos en [Prácticas recomendadas de integración de Creative Cloud y](/help/assets/aem-cc-integration-best-practices.md). Si tiene alguna pregunta, [póngase en contacto con el Servicio de atención al cliente de Adobe](https://www.adobe.com/account/sign-in.supportportal.html).

<!-- Hiding this for now via cqdoc-16834.
![Flow of data when AEM Assets and Creative Cloud are integrated](assets/chlimage_1-48.png)

>[!NOTE]
>
>Sharing assets between Adobe Experience Cloud and Adobe Creative Cloud requires administrator privileges on the AEM instance.
-->

## Creación de una aplicación {#create-an-application}

1. Para obtener acceso a la interfaz de puerta de enlace de Adobe Developer, inicie sesión en [https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/).

   >[!NOTE]
   >
   >Se necesitan privilegios de administrador para crear un ID de aplicación.

1. En el panel izquierdo, vaya a **[!UICONTROL Herramientas para desarrolladores]** > **[!UICONTROL Aplicaciones]** para ver una lista de aplicaciones.
1. Haga clic en **[!UICONTROL Agregar]** ![aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png) para crear una aplicación.
1. En la lista **[!UICONTROL Credenciales de cliente]**, seleccione **[!UICONTROL Cuenta de servicio (aserción JWT)]**, que es un servicio de comunicación servidor a servidor para la autenticación de servidor.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. Especifique un nombre para la aplicación y una descripción opcional.
1. En la lista **[!UICONTROL Organización]**, seleccione la organización para la que desea sincronizar recursos.
1. En la lista **[!UICONTROL Scope]**, seleccione **[!UICONTROL dam-read]**, **[!UICONTROL dam-sync]**, **[!UICONTROL dam-write]** y **[!UICONTROL cc-share]**.
1. Haga clic en **[!UICONTROL Crear]**. Un mensaje notifica que se ha creado la aplicación.

   ![Notificación de creación correcta de la aplicación para integrar AEM Assets con Creative Cloud](assets/chlimage_1-50.png)

1. Copie el **[!UICONTROL identificador de aplicación]** que se genera para la nueva aplicación.

   >[!CAUTION]
   >
   >Asegúrese de no copiar de forma involuntaria el **[!UICONTROL Secreto de aplicación]** en lugar de **[!UICONTROL ID de aplicación]**.

## Añadir una nueva configuración al Experience Cloud {#add-a-new-configuration}

1. AEM Haga clic en el logotipo de la en la interfaz de usuario de la instancia local de AEM Assets y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Service heredados]**.

1. Busque el servicio **[!UICONTROL Adobe Experience Cloud]**. Si no existen configuraciones, haga clic en **[!UICONTROL Configurar ahora]**. Si existen configuraciones, haga clic en **[!UICONTROL Mostrar configuraciones]** y haga clic en `+` para agregar una configuración nueva.

   >[!NOTE]
   >
   >Utilice una cuenta de Adobe ID que tenga privilegios de administrador para la organización.

1. En el cuadro de diálogo **[!UICONTROL Crear configuración]**, especifique un título y un nombre para la nueva configuración y haga clic en **[!UICONTROL Crear]**.

   ![Asigne un nombre a una nueva configuración para integrar AEM Assets y Creative Cloud](assets/aem-ec-integration-config1.png)

1. En el campo **[!UICONTROL URL de inquilino]**, especifique la URL de AEM Assets. En el pasado, si la dirección URL se definía como `https://<tenant_id>.marketing.adobe.com`, cambie a `https://<tenant_id>.experiencecloud.adobe.com`.

   1. Vaya a **Herramientas > Cloud Service > Cloud Service heredados**. En Adobe Experience Cloud, haga clic en **Mostrar configuraciones**.
   1. Seleccione la configuración existente que desea editar. Editar la configuración y reemplazar `marketing.adobe.com` a `experiencecloud.adobe.com`.
   1. Guarde la configuración. Pruebe los agentes de replicación de sincronización de MAC.

1. En el campo **[!UICONTROL ID de cliente]**, pegue el ID de aplicación que copió al final del procedimiento [crear una aplicación](#create-an-application).

   ![Proporcione los valores de ID de aplicación necesarios para integrar AEM Assets y Creative Cloud](assets/cloudservices_tenant_info.png)

1. En **[!UICONTROL Sincronización]**, seleccione **[!UICONTROL Habilitado]** para habilitar la sincronización y haga clic en **[!UICONTROL Aceptar]**. Si selecciona **disabled**, la sincronización funciona en una sola dirección.

1. En la página de configuración, haga clic en **[!UICONTROL Mostrar clave pública]** para mostrar la clave pública generada para su instancia. También puede hacer clic en **[!UICONTROL Descargar clave pública para OAuth Gateway]** para descargar el archivo que contiene la clave pública. A continuación, abra el archivo para mostrar la clave pública.

## Habilitar sincronización {#enable-synchronization}

1. Muestre la clave pública mediante uno de los siguientes métodos mencionados en el último paso del procedimiento [agregar una nueva configuración al Experience Cloud](#add-a-new-configuration). Haga clic en **[!UICONTROL Mostrar clave pública]**.

1. Copie la clave pública y péguela en el campo **[!UICONTROL Clave pública]** de la interfaz de configuración de la aplicación que creó en [crear una aplicación](#create-an-application).

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. Haga clic en **[!UICONTROL Actualizar]**. Sincronice sus recursos ahora con la instancia de AEM Assets.

## Prueba de la sincronización {#test-the-synchronization}

1. AEM Haga clic en el logotipo de la en la interfaz de usuario de la instancia local de AEM Assets y vaya a **[!UICONTROL Herramientas]**> **[!UICONTROL Implementación]**> **[!UICONTROL Replicación]** para localizar los perfiles de replicación creados para la sincronización.
1. En la página **[!UICONTROL Replicación]**, haga clic en **[!UICONTROL Agentes del autor]**.
1. En la lista de perfiles, haga clic en el perfil de replicación predeterminado para su organización para abrirlo.
1. En el cuadro de diálogo, haga clic en **[!UICONTROL Probar conexión]**.

   ![Probar la conexión y establecer el perfil de replicación predeterminado para su organización](assets/chlimage_1-54.png)

1. Cuando se complete el resto de la replicación, compruebe si aparece un mensaje de éxito al final de los resultados de la prueba.

## Añadir usuarios al Experience Cloud {#add-users-to-experience-cloud}

1. Inicie sesión en el Experience Cloud con las credenciales de administrador.
1. Desde los carriles, ve a **[!UICONTROL Administración]** y luego haz clic en **[!UICONTROL Iniciar Enterprise Dashboard]**.
1. En el carril, haga clic en **[!UICONTROL Usuarios]** para abrir la página **[!UICONTROL Administración de usuarios]**.
1. En la barra de herramientas, haga clic en **Agregar** ![aem_assets_add_icon](assets/aem_assets_add_icon.png).
1. Agregue uno o varios usuarios a los que desee permitir compartir recursos con Creative Cloud.

<!-- TBD: Check.
   >[!NOTE]
   >
   >Only the users that you add to Experience Cloud can share assets from AEM Assets to Creative Cloud.

-->

## Intercambio de recursos entre AEM Assets y Experience Cloud {#exchange-assets-between-aem-and-experience-cloud}

1. Inicie sesión en AEM Assets.
1. En la consola de Assets, cree una carpeta y cargue algunos recursos. Por ejemplo, cree una carpeta **mc-demo** y cárguele un recurso.
1. Seleccione la carpeta y haga clic en **Compartir** ![assets_share](assets/do-not-localize/assets_share.png).
1. En el menú, seleccione **[!UICONTROL Adobe Experience Cloud]** y haga clic en **[!UICONTROL Compartir]**. Un mensaje notifica que la carpeta se comparte con el Experience Cloud.

   >[!NOTE]
   >
   >No se admite el uso compartido de una carpeta Assets del tipo `sling:OrderedFolder` en el contexto del uso compartido en Adobe Experience Cloud. Si desea compartir una carpeta, al crearla en AEM Assets, no seleccione la opción **[!UICONTROL Ordenado]**.

1. Actualice la interfaz de usuario de AEM Assets. La carpeta que ha creado en la consola de Assets de su instancia local de AEM Assets se copia en la interfaz de usuario del Experience Cloud. El recurso que cargue en la carpeta de AEM Assets aparecerá en la copia de la carpeta en Experience Cloud AEM después de que el servidor de la carpeta lo haya procesado
1. También puede cargar un recurso en la copia duplicada de la carpeta en Experience Cloud. Una vez procesado, el recurso aparece en la carpeta compartida de AEM Assets.

<!-- Removing as per PM guidance via https://jira.corp.adobe.com/browse/CQDOC-16834?focusedCommentId=22881523&page=com.atlassian.jira.plugin.system.issuetabpanels:comment-tabpanel#comment-22881523.

## Exchange assets between AEM Assets and Creative Cloud {#exchange-assets-between-aem-assets-and-creative-cloud}

>[!CAUTION]
>
>The AEM to Creative Cloud Folder Sharing feature is deprecated. Customers are strongly advised to use newer capabilities, like [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) or [AEM desktop app](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html). Learn more in [AEM and Creative Cloud Integration Best Practices](/help/assets/aem-cc-integration-best-practices.md).

AEM Assets lets you share folders containing assets with Adobe Creative Cloud users.

1. In the Assets console, select the folder to share with Creative Cloud.
1. From the toolbar, click **[!UICONTROL Share]** ![assets_share](assets/do-not-localize/assets_share.png).
1. From the list, select the **[!UICONTROL Adobe Creative Cloud]** option.

   >[!NOTE]
   >
   >The options are available for users with read permissions on the root. Users must have the required permission to access the replication agent information of Marketing Cloud.

1. In the **[!UICONTROL Creative Cloud Sharing]** page, add the user to share the folder with and choose a role for the user. Click **[!UICONTROL Save]** and click **[!UICONTROL OK]**.

1. Log on to Creative Cloud with the credentials of the user you shared the folder with. The shared folder is available in Creative Cloud.

The AEM Assets-Marketing Cloud synchronization is designed in a way that the user machine instance from where the asset is uploaded retains the right to modify the asset. Only these changes are propagated to the other instance.

For example, if an asset is uploaded from an AEM Assets (on premises) instance, the changes to the asset from this instance are propagated to the Marketing Cloud instance. However, the changes done from the Marketing Cloud instance to the same asset aren’t propagated to the AEM instance and conversely for asset uploaded from Marketing Cloud.
-->

>[!MORELIKETHIS]
>
>* [Prácticas recomendadas de integración de Assets y Creative Cloud](/help/assets/aem-cc-integration-best-practices.md)
