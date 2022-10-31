---
title: Integración de Adobe Sign con AEM Forms
seo-title: Integrate Adobe Sign with AEM Forms
description: Obtenga información sobre cómo configurar Adobe Sign para AEM Forms
seo-description: Learn how to configure Adobe Sign for AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 34%

---

# Integrar [!DNL Adobe Sign] con AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] activa los flujos de trabajo de firma electrónica para formularios adaptables. Las firmas electrónicas mejoran los flujos de trabajo para procesar documentos para el área legal, ventas, nóminas, administración de recursos humanos y muchas más.

En un [!DNL Adobe Sign] y el escenario de formularios adaptables, un usuario rellena un formulario adaptable a **solicitud de un servicio**. Por ejemplo, una solicitud de tarjeta de crédito y un formulario de solicitud para una prestación. Cuando un usuario rellena, envía y firma el formulario de solicitud, este se envía al proveedor de servicios para que realice más acciones. El proveedor de servicios revisa la solicitud y utiliza [!DNL Adobe Sign] para marcarla como aprobada. Para habilitar flujos de trabajo de firma electrónica similares, puede integrar [!DNL Adobe Sign] con AEM [!DNL Forms].

Para usar [!DNL Adobe Sign] con AEM [!DNL Forms], configure [!DNL Adobe Sign] en AEM Cloud Services:

## Requisitos previos {#prerequisites}

Debe integrar lo siguiente [!DNL Adobe Sign] con AEM [!DNL Forms]:

* Un activo [Cuenta de desarrollador de Adobe Sign.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* Un [Habilitado para SSL](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] servidor.
* un [aplicación API de Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md);
* las credenciales (ID de cliente y Secreto de cliente) de la aplicación API de [!DNL Adobe Sign];
* Al volver a configurar, elimine la [!DNL Adobe Sign] configuración de las instancias de autor y publicación.
* usar una [clave criptográfica idéntica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) para las instancias de autor y publicación;

## Configurar [!DNL Adobe Sign] con AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

Una vez cumplidos los requisitos previos, realice los siguientes pasos para configurar [!DNL Adobe Sign] con AEM [!DNL Forms] en la instancia de autor:

1. En AEM [!DNL Forms] instancia de autor, vaya a **Herramientas** ![martillo](assets/hammer.png) > **[!UICONTROL General]** > **[!UICONTROL Explorador de configuración]**.
1. En la página **[!UICONTROL Explorador de configuración]**, pulse **[!UICONTROL Crear]**.
   * Consulte la documentación del [Explorador de configuración](/help/sites-administering/configurations.md) para obtener más información.
1. En el cuadro de diálogo **[!UICONTROL Crear configuración]**, especifique un **[!UICONTROL Título]** para la configuración, habilite **[!UICONTROL Configuraciones de nube]** y pulse **[!UICONTROL Crear]**. Crea un contenedor de configuración para servicios en la nube.
1. Vaya a **Herramientas** ![martillo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** y seleccione el contenedor de configuración que creó en el paso anterior.

   >[!NOTE]
   >
   >Puede ejecutar los pasos 1-4 para crear un nuevo contenedor de configuración y crear un [!DNL Adobe Sign] configuración en el contenedor o utilice la `global` carpeta **Herramientas** ![martillo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Si crea la configuración en el nuevo contenedor de configuración, asegúrese de especificar el nombre del contenedor en la variable **[!UICONTROL Contenedor de configuración]** al crear un formulario adaptable.

   >[!NOTE]
   Asegúrese de que la dirección URL de la página de configuración de los servicios de nube comience por **HTTPS**. Si no, [habilitar SSL](/help/sites-administering/ssl-by-default.md) para AEM [!DNL Forms] servidor.

1. En la página de configuración, pulse **[!UICONTROL Crear]** para crear una configuración de [!DNL Adobe Sign] en AEM [!DNL Forms].
1. En el **[!UICONTROL General]** de la pestaña **[!UICONTROL Crear configuración de Adobe Sign]** página, especifique un **[!UICONTROL Nombre]** para la configuración y pulse **[!UICONTROL Siguiente]**. Si lo desea, puede especificar un título y examinar para seleccionar una miniatura para la configuración.

1. Copie la URL de la ventana actual del explorador en un bloc de notas. Es necesario configurar [!DNL Adobe Sign] aplicación con AEM[!DNL Forms].

1. En el **[!UICONTROL Configuración]** , la pestaña **[!UICONTROL URL de OAuth]** contiene la dirección URL predeterminada. El formato del URL es el siguiente:

   `https://<shard>/public/oAuth/v2`

   Por ejemplo:
   `https://secure.na1.echosign.com/public/oauth/v2`

   donde:

   **na1** hace referencia a la partición predeterminada de la base de datos. Puede modificar el valor de la partición de la base de datos. Asegúrese de que las configuraciones en la nube de [!DNL  Adobe Sign] apuntan a la [partición correcta](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   Si crea otra configuración de [!DNL Adobe Sign] para una función o componente de Adobe Experience Manager, asegúrese de que todas las configuraciones en la nube de [!DNL Adobe Sign] apuntan a la misma partición.

   >[!NOTE]
   Mantenga el **Crear configuración de Adobe Sign** página abierta. No lo cierre. Puede recuperar **ID de cliente** y **Secreto del cliente** después de configurar la configuración de OAuth para [!DNL Adobe Sign] como se describe en los pasos siguientes.


1. Configure OAuth para la aplicación [!DNL Adobe Sign]:

   1. Abra una ventana del explorador e inicie sesión en la [!DNL Adobe Sign] cuenta de desarrollador.
   1. Seleccione la aplicación configurada para AEM [!DNL Forms]y toque **[!UICONTROL Configuración de OAuth para aplicación]**.
   1. Copie el **[!UICONTROL ID de cliente]** y **[!UICONTROL Secreto del cliente]** a un bloc de notas.
   1. En el **[!UICONTROL Dirección URL de redireccionamiento]** , añada la URL HTTPS copiada en el paso anterior.
   1. Habilite la siguiente configuración de OAuth para la aplicación de [!DNL Adobe Sign] y haga clic en **[!UICONTROL Guardar]**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   Para obtener información paso a paso sobre cómo configurar OAuth para una aplicación [!DNL Adobe Sign] y obtener las claves, consulte la documentación para desarrolladores [Configurar OAuth para la aplicación](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md).

   ![Configuración de OAuth](assets/oauthconfig_new.png)

1. Vuelva a la página **[!UICONTROL Crear configuración de Adobe Sign]**. En la pestaña **[!UICONTROL Configuración]**, el campo **[!UICONTROL URL de OAuth]** muestra la URL predeterminada. El formato del URL es el siguiente:

   `https://<shard>/public/oAuth/v2`

   Por ejemplo:
   `https://secure.na1.echosign.com/public/oauth/v2`

   donde:

   **na1** hace referencia a la partición predeterminada de la base de datos.

   Puede modificar el valor de la partición de la base de datos. Reinicie el servidor para poder utilizar el nuevo valor para el uso compartido de la base de datos.

   >[!NOTE]
   Asegúrese de que las configuraciones de instancia de autor y publicación apuntan al mismo uso compartido. Si crea varias configuraciones de Adobe Sign para una organización, asegúrese de que todas las configuraciones utilicen el mismo uso compartido.

1. Vuelva a la página **[!UICONTROL Crear configuración de Adobe Sign]**. En el **[!UICONTROL Configuración]** especifique la **ID de cliente** (también denominado ID de aplicación) y **Secreto del cliente**. Utilice la variable [ID de cliente y Secreto de cliente de la aplicación Adobe Sign](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) creado para AEM Forms.

1. Seleccione el **[!UICONTROL Activar Adobe Sign para archivos adjuntos también]** para anexar archivos adjuntos a un formulario adaptable al correspondiente [!DNL Adobe Sign] documento enviado para firma.

1. Pulse **[!UICONTROL Conectar con Adobe Sign]**. Cuando se le soliciten credenciales, indique el nombre de usuario y la contraseña de la cuenta utilizada al crear la aplicación [!DNL Adobe Sign]. 

1. Pulse **[!UICONTROL Crear]** para crear la configuración de [!DNL Adobe Sign].

1. Abra AEM consola web. La URL es `https://'[server]:[port]'/system/console/configMgr`. 
1. Apertura **[!UICONTROL Servicio de configuración común de Forms].**
1. En el **[!UICONTROL Permitir]** field, **select** Todos los usuarios: Todos los usuarios, anónimos o conectados, pueden obtener una vista previa de los archivos adjuntos, comprobar y firmar formularios y hacer clic en **[!UICONTROL Guardar].** La instancia de autor está configurada para usar [!DNL Adobe Sign].
1. Publique la configuración.
1. Uso [replicación](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) para crear una configuración idéntica en las instancias de publicación correspondientes.

Ahora, [!DNL Adobe Sign] está integrado con AEM [!DNL Forms] y listo para su uso en formularios adaptables. Hasta [usar el servicio Adobe Sign en un formulario adaptable](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), especifique el contenedor de configuración creado anteriormente en las propiedades del formulario adaptable.



## Configurar [!DNL Adobe Sign] planificador para sincronizar el estado de firma {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Un [!DNL Adobe Sign] el formulario adaptable habilitado solo se envía una vez que todos los firmantes hayan completado el proceso de firma. De forma predeterminada, la variable [!DNL Adobe Sign] Los servicios de planificador tienen programada la comprobación (encuesta) de la respuesta del firmante cada 24 horas. Puede cambiar el intervalo predeterminado para su entorno. Realice los siguientes pasos para cambiar el intervalo predeterminado:

1. Iniciar sesión en AEM [!DNL Forms] servidor con credenciales de administrador y vaya a **Herramientas** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.

   También puede abrir la siguiente URL en una ventana del explorador:
   `https://[localhost]:'port'/system/console/configMgr`

1. Busque y abra el **[!UICONTROL Servicio de configuración de Adobe Sign]** . Especifique un [expresión cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) en el **[!UICONTROL Expresión del programador de actualización de estado]** y haga clic en **[!UICONTROL Guardar]**. Por ejemplo, para ejecutar el servicio de configuración diariamente a las 00:00 a. m., especifique `0 0 0 1/1 * ? *` en el **[!UICONTROL Expresión del programador de actualización de estado]** campo .

Intervalo predeterminado para sincronizar el estado de [!DNL Adobe Sign] ahora cambia.

## Artículos relacionados {#related-articles}

* [Uso de Adobe Sign en un formulario adaptable](../../forms/using/working-with-adobe-sign.md)
* [Uso de Adobe Sign con AEM Forms (vídeo)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
