---
title: Configurar la integración de AEM Assets con Experience Cloud y Creative Cloud
seo-title: Configurar la integración de AEM Assets con Marketing Cloud y Creative Cloud
description: Obtenga información sobre cómo configurar la integración de AEM Assets con Experience Cloud y Creative Cloud.
seo-description: Obtenga información sobre cómo configurar la integración de AEM Assets con Experience Cloud y Creative Cloud.
uuid: ec36ea0e-607f-4c73-89df-e095067fccd4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 82a8e807-a2df-4fe3-a68c-2dabc9328eca
docset: aem65
translation-type: tm+mt
source-git-commit: 0560eb8e3c127964920827609a9982acf07b515f
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 1%

---


# Configurar la integración de AEM Assets con Experience Cloud y Creative Cloud {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}

Si es cliente de Adobe Experience Cloud, puede sincronizar los recursos de Adobe Experience Manager Assets con Adobe Creative Cloud y viceversa. También puede sincronizar los recursos con Experience Cloud y viceversa. Puede configurar esta sincronización mediante [!DNL Adobe I/O].

El flujo de trabajo para configurar esta integración es:

1. Cree una autenticación en [!DNL Adobe I/O] mediante una puerta de enlace pública y obtenga un ID de aplicación.
1. Cree un perfil en la instancia de AEM Assets mediante el ID de aplicación.
1. Utilice esta configuración para sincronizar los recursos de AEM Assets con Creative Cloud.

En segundo plano, el servidor de AEM autentica el perfil con la puerta de enlace y, a continuación, sincroniza los datos entre AEM Assets y Experience Cloud.

>[!CAUTION]
>
>La función de uso compartido de carpetas de AEM a Creative Cloud está en desuso en AEM Assets. Obtenga más información y encuentre reemplazos en [Prácticas recomendadas de integración de AEM y Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

![Flujo de datos cuando AEM Assets y Creative Cloud están integrados](assets/chlimage_1-48.png)

Flujo de datos cuando AEM Assets y Creative Cloud están integrados

>[!NOTE]
>
>El uso compartido de recursos entre Adobe Experience Cloud y Adobe Creative Cloud requiere privilegios de administrador en la instancia de AEM.

>[!CAUTION]
>
>Adobe Marketing Cloud ha sido rebautizado como Adobe Experience Cloud. Los procedimientos que siguen mencionan el Marketing Cloud para reflejar la interfaz actual. Estas menciones se cambiarán más adelante.

## Crear una aplicación {#create-an-application}

1. Acceda a la interfaz de puerta de enlace de Adobe Developer iniciando sesión en [https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/).

   >[!NOTE]
   >
   >Se requieren privilegios de administrador para crear un ID de aplicación.

1. En el panel izquierdo, vaya a **[!UICONTROL Herramientas para desarrolladores]** > **[!UICONTROL Aplicaciones]** para vista de una lista de aplicaciones.
1. Haga clic en **[!UICONTROL Añadir]** ![aem_assets_addcírculo_icon](assets/aem_assets_addcircle_icon.png) para crear una aplicación.
1. En la lista **[!UICONTROL Credenciales de cliente]**, seleccione **[!UICONTROL Cuenta de servicio (aserción JWT)]**, que es un servicio de comunicación de servidor a servidor para la autenticación de servidor.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. Especifique un nombre para la aplicación y una descripción opcional.
1. En la lista **[!UICONTROL Organization]**, seleccione la organización para la que desea sincronizar los recursos.
1. En la lista **[!UICONTROL Scope]**, seleccione **[!UICONTROL dam-read]**, **[!UICONTROL dam-sync]**, **[!UICONTROL dam-write]** y **[!UICONTROL cc-share]**.
1. Haga clic en **[!UICONTROL Crear]**. Un mensaje notifica que se ha creado la aplicación.

   ![Notificación de creación correcta de la aplicación para integrar AEM Assets con Adobe CC](assets/chlimage_1-50.png)

1. Copie el **[!UICONTROL ID de aplicación]** que se genera para la nueva aplicación.

   >[!CAUTION]
   >
   >Asegúrese de no copiar inadvertidamente el **[!UICONTROL Secreto de aplicación]** en lugar del **[!UICONTROL ID de aplicación]**.

## Añadir una nueva configuración en Marketing Cloud {#add-a-new-configuration-to-marketing-cloud}

1. Haga clic en el logotipo AEM en la interfaz de usuario de la instancia de AEM Assets local y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Cloud Services heredados]**.

1. Busque el servicio **[!UICONTROL Adobe Marketing Cloud]**. Si no existe ninguna configuración, haga clic en **[!UICONTROL Configurar ahora]**. Si existen configuraciones, haga clic en **[!UICONTROL Mostrar configuraciones]** y haga clic en `+` para agregar una nueva configuración.

   >[!NOTE]
   >
   >Utilice una cuenta de Adobe ID con privilegios de administrador para la organización.

1. En el cuadro de diálogo **[!UICONTROL Crear configuración]**, especifique un título y un nombre para la nueva configuración y haga clic en **[!UICONTROL Crear]**.

   ![Asigne un nombre a una nueva configuración para integrar AEM Assets y CC](assets/chlimage_1-51.png)

1. En el campo **[!UICONTROL URL del inquilino]**, especifique la dirección URL de AEM Assets.

   >[!CAUTION]
   >
   >Debido al cambio de marca, si ingresó la dirección URL del inquilino como `https://<tenant_id>.marketing.adobe.com` debe cambiarla a `https://<tenant_id>.experiencecloud.adobe.com.` Para hacerlo, siga los pasos a continuación:
   >
   >1. Vaya a **Herramientas > Cloud Services > Servicios de nube heredados**.
   1. En Adobe Marketing Cloud, haga clic en **Mostrar configuraciones**.
   1. Seleccione la configuración que se creó al configurar la sincronización AEM-MAC-CC.
   1. Edite la configuración de cloudservice y reemplace **marketing.adobe.com** en el campo URL del inquilino a **experience ecloud.adobe.com**.
   1. Guarde la configuración.
   1. Pruebe los agentes de replicación mac-sync.


1. En el campo **[!UICONTROL ID de cliente]**, pegue el ID de aplicación que copió al final del procedimiento [Crear una aplicación](/help/sites-administering/configure-assets-cc-integration.md#create-an-application).

   ![Proporcione los valores de ID de aplicación necesarios para integrar AEM Assets y Creative Cloud](assets/cloudservices_tenant_info.png)

1. En **[!UICONTROL Sincronización]** seleccione **[!UICONTROL Habilitado]** para habilitar la sincronización y haga clic en **[!UICONTROL Aceptar]**.

   >[!NOTE]
   Si selecciona **deshabilitado**, la sincronización funcionará en una sola dirección.

1. En la página de configuración, haga clic en **[!UICONTROL Mostrar clave pública]** para mostrar la clave pública generada para la instancia. Como alternativa, haga clic en **[!UICONTROL Descargar clave pública para OAuth Gateway]** para descargar el archivo que contiene la clave pública. A continuación, abra el archivo para mostrar la clave pública.

## Habilitar sincronización {#enable-synchronization}

1. Muestre la clave pública utilizando uno de los siguientes métodos mencionados en el último paso del procedimiento [Añada una nueva configuración en Marketing Cloud](/help/sites-administering/configure-assets-cc-integration.md#add-a-new-configuration-to-marketing-cloud). Haga clic en **[!UICONTROL Mostrar clave pública]**.

   ![chlimage_1-52](assets/chlimage_1-52.png)

1. Copie la clave pública y péguela en el campo **[!UICONTROL Clave pública]** de la interfaz de configuración de la aplicación que ha creado en [Cree una aplicación](/help/sites-administering/configure-assets-cc-integration.md#create-an-application).

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. Haga clic en **[!UICONTROL Actualizar]**. Sincronice los recursos con la instancia de AEM Assets ahora.

## Probar la sincronización {#test-the-synchronization}

1. Haga clic en el logotipo de AEM en la interfaz de usuario de la instancia de AEM Assets local y vaya a **[!UICONTROL Herramientas]**> **[!UICONTROL Implementación]**> **[!UICONTROL Replicación]** para localizar los perfiles de replicación creados para la sincronización.
1. En la página **[!UICONTROL Replicación]**, haga clic en **[!UICONTROL Agentes del autor]**.
1. En la lista de perfiles, haga clic en el perfil de replicación predeterminado para que su organización lo abra.
1. En el cuadro de diálogo, haga clic en **[!UICONTROL Probar conexión]**.

   ![Probar la conexión y establecer el perfil de replicación predeterminado para su organización](assets/chlimage_1-54.png)

1. Cuando se complete el reposo de replicación, compruebe si hay un mensaje de éxito al final de los resultados de la prueba.

## Añadir usuarios a Marketing Cloud {#add-users-to-marketing-cloud}

1. Inicie sesión en Marketing Cloud con las credenciales del administrador.
1. En los carriles, vaya a **[!UICONTROL Administración]** y luego toque o haga clic en **[!UICONTROL Iniciar Panel empresarial]**.
1. En el carril, haga clic en **[!UICONTROL Usuarios]** para abrir la página **[!UICONTROL Administración de usuarios]**.
1. En la barra de herramientas, toque o haga clic en **Añadir** ![aem_assets_add_icon](assets/aem_assets_add_icon.png).
1. Añada uno o varios usuarios que desee que puedan compartir recursos con Creative Cloud.

   >[!NOTE]
   Solo los usuarios que agregue a Marketing Cloud pueden compartir recursos de AEM Assets con Creative Cloud.

## Intercambiar recursos entre AEM Assets y Marketing Cloud {#exchange-assets-between-aem-assets-and-marketing-cloud}

1. Inicie sesión en AEM Assets.
1. En la consola Recursos, cree una carpeta y cargue algunos recursos en ella. Por ejemplo, cree una carpeta **mc-demo** y cargue un recurso en ella.
1. Seleccione la carpeta y haga clic en **Compartir** ![recursos_compartidos](assets/assets_share.png).
1. En el menú, seleccione **[!UICONTROL Adobe Marketing Cloud]** y haga clic en **[!UICONTROL Compartir]**. Un mensaje notifica que la carpeta se comparte con Marketing Cloud.

   ![chlimage_1-55](assets/chlimage_1-55.png)

   >[!NOTE]
   No se puede compartir una carpeta de recursos del tipo `sling:OrderedFolder` en el contexto de compartir en Adobe Marketing Cloud. Si desea compartir una carpeta, al crearla en AEM Assets, no seleccione la opción **[!UICONTROL Pedido]**.

1. Actualice la interfaz de usuario de AEM Assets. La carpeta que ha creado en la consola Recursos de la instancia de AEM Assets local se copia en la interfaz de usuario de Marketing Cloud. El recurso que se carga en la carpeta de AEM Assets aparece en la copia de la carpeta en Marketing Cloud después de que el servidor de AEM lo haya procesado.
1. También puede cargar un recurso en la copia replicada de la carpeta en Marketing Cloud. Una vez procesado, el recurso aparece en la carpeta compartida de AEM Assets.

## Intercambiar recursos entre AEM Assets y Creative Cloud {#exchange-assets-between-aem-assets-and-creative-cloud}

>[!CAUTION]
La función de uso compartido de carpetas de AEM a Creative Cloud está en desuso. Se recomienda encarecidamente a los clientes que utilicen las nuevas funciones, como [Vínculo de recursos de Adobe](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html) o [AEM aplicación de escritorio](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html). Obtenga más información en [Prácticas recomendadas de integración de AEM y Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

AEM Assets permite compartir carpetas que contienen recursos con usuarios de Adobe Creative Cloud.

1. En la consola Recursos, seleccione la carpeta que desee compartir con Creative Cloud.
1. En la barra de herramientas, haga clic en **[!UICONTROL Compartir]** ![recursos_compartidos](assets/assets_share.png).
1. En la lista, seleccione la opción **[!UICONTROL Adobe Creative Cloud]**.

   >[!NOTE]
   Las opciones están disponibles para los usuarios con permisos de lectura en la raíz. Los usuarios deben tener el permiso necesario para acceder a la información del agente de replicación de Marketing Cloud.

1. En la página **[!UICONTROL Uso compartido de Creative Cloud]**, agregue el usuario para compartir la carpeta y elija una función para el usuario. Haga clic en **[!UICONTROL Guardar]** y haga clic en **[!UICONTROL Aceptar]**.

1. Inicie sesión en el Creative Cloud con las credenciales del usuario con el que ha compartido la carpeta. La carpeta compartida está disponible en Creative Cloud.

La sincronización de AEM Assets-Marketing Cloud está diseñada de tal forma que la instancia de ordenador del usuario desde la que se carga el recurso conserva el derecho de modificar el recurso. Sólo estos cambios se propagan a la otra instancia.

Por ejemplo, si un recurso se carga desde una instancia de AEM Assets (local), los cambios realizados en el recurso desde esta instancia se propagan a la instancia de Marketing Cloud. Sin embargo, los cambios realizados desde la instancia de Marketing Cloud al mismo recurso no se propagan a la instancia de AEM y viceversa para el recurso cargado desde Marketing Cloud.

>[!MORELIKETHIS]
* [Prácticas recomendadas de integración de AEM y Creative Cloud](/help/assets/aem-cc-integration-best-practices.md)
* [Prácticas recomendadas de uso compartido de carpetas de AEM a Creative Cloud](/help/assets/aem-cc-folder-sharing-best-practices.md)

