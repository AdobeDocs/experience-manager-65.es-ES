---
title: Integrar Adobe Sign con AEM Forms
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
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 100%

---

# Integrar [!DNL Adobe Sign]con AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] habilita los flujos de trabajo de firma electrónica para formularios adaptables. Las firmas electrónicas mejoran los flujos de trabajo para procesar documentos para el área legal, ventas, nóminas, administración de recursos humanos y mucho más.

Cuando se trabaja con [!DNL Adobe Sign] y los formularios adaptables, normalmente los usuarios rellenan un formulario adaptable para **solicitar un servicio**. Por ejemplo, una solicitud de tarjeta de crédito y un formulario de solicitud para una prestación. Cuando un usuario rellena, envía y firma el formulario de solicitud, este se envía al proveedor de servicios para que realice más acciones. El proveedor de servicios revisa la solicitud y utiliza [!DNL Adobe Sign] para marcarla como aprobada. Para habilitar flujos de trabajo de firma electrónica similares, puede integrar [!DNL Adobe Sign] con AEM [!DNL Forms].

Para usar [!DNL Adobe Sign] con AEM [!DNL Forms], configure [!DNL Adobe Sign] en AEM Cloud Services:

## Requisitos previos {#prerequisites}

Para integrar [!DNL Adobe Sign] con AEM [!DNL Forms], necesita lo siguiente:

* Una [cuenta de desarrollador de Adobe Sign](https://acrobat.adobe.com/es/es/why-adobe/developer-form.html) activa.
* Un servidor AEM [Habilitado para SSL](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms].
* Un [aplicación API de Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md);
* Las credenciales (ID de cliente y Secreto de cliente) de la aplicación API de [!DNL Adobe Sign];
* Al volver a configurar, quite la [!DNL Adobe Sign] configuración de las instancias de autor y publicación.
* Use una [clave criptográfica idéntica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) para las instancias de autor y publicación.

## Configurar[!DNL Adobe Sign] con AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

Una vez cumplidos los requisitos previos, realice los siguientes pasos para configurar [!DNL Adobe Sign] con AEM [!DNL Forms] en la instancia de autor:

1. En la instancia de autor de AEM [!DNL Forms], navegue hasta **Herramientas** ![martillo](assets/hammer.png) > **[!UICONTROL General]** > **[!UICONTROL Explorador de configuración]**.
1. En la página **[!UICONTROL Explorador de configuración]**, pulse **[!UICONTROL Crear]**.
   * Consulte la documentación del [Explorador de configuración](/help/sites-administering/configurations.md) para obtener más información.
1. En el cuadro de diálogo **[!UICONTROL Crear configuración]**, especifique un **[!UICONTROL Título]** para la configuración, habilite **[!UICONTROL Configuraciones de nube]** y pulse **[!UICONTROL Crear]**. Crea un contenedor de configuración para los servicios en la nube.
1. Navegue hasta **Herramientas** ![martillo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** y abra el contenedor de configuración que creó en el paso anterior.

   >[!NOTE]
   >
   >Puede ejecutar los pasos 1-4 para crear un nuevo contenedor de configuración y crear una configuración [!DNL Adobe Sign] en el contenedor o utilizar la carpeta existente `global` en **Herramientas** ![martillo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Si crea la configuración en el nuevo contenedor de configuración, asegúrese de especificar el nombre del contenedor en el campo **[!UICONTROL Contenedor de configuración]** al crear un formulario adaptable.

   >[!NOTE]
   >Asegúrese de que la dirección URL de la página de configuración de los servicios de nube comience por **HTTPS**. Si no, [habilite SSL](/help/sites-administering/ssl-by-default.md) para el servidor de AEM [!DNL Forms].

1. En la página de configuración, pulse **[!UICONTROL Crear]** para crear una configuración de [!DNL Adobe Sign] en AEM [!DNL Forms].
1. En la pestaña **[!UICONTROL General]** de la página **[!UICONTROL Crear configuración de Adobe Sign]**, especifique un **[!UICONTROL Nombre]** para la configuración y pulse **[!UICONTROL Siguiente]**. Si lo desea, puede especificar un Título y examinar los archivos para seleccionar una miniatura para la configuración.

1. Copie la URL de la ventana actual del explorador en un bloc de notas. Es necesario configurar la aplicación [!DNL Adobe Sign] con AEM[!DNL Forms].

1. En la pestaña **[!UICONTROL Configuración]**, el campo **[!UICONTROL URL de OAuth]** muestra la URL predeterminada. El formato de la URL es el siguiente:

   `https://<shard>/public/oAuth/v2`

   Por ejemplo:
   `https://secure.na1.echosign.com/public/oauth/v2`

   donde:

   **na1** hace referencia a la partición predeterminada de la base de datos. Puede modificar el valor de la partición de la base de datos. Asegúrese de que las configuraciones en la nube de [!DNL  Adobe Sign] apuntan a la [partición correcta](https://helpx.adobe.com/es/sign/using/identify-account-shard.html).

   Si crea otra configuración de [!DNL Adobe Sign] para una función o componente de Adobe Experience Manager, asegúrese de que todas las configuraciones en la nube de [!DNL Adobe Sign] apuntan a la misma partición.

   >[!NOTE]
   >Mantenga la página **Crear la configuración de Adobe Sign** abierta. No la cierre. Puede recuperar la **ID de cliente** y el **Secreto de cliente** después de configurar OAuth para la aplicación [!DNL Adobe Sign] como se describe en los pasos siguientes.


1. Configure OAuth para la aplicación [!DNL Adobe Sign]:

   1. Abra una ventana del explorador e inicie sesión en su cuenta de desarrollador de [!DNL Adobe Sign].
   1. Seleccione la aplicación configurada para AEM [!DNL Forms] y pulse **[!UICONTROL Configurar OAuth para la aplicación]**.
   1. Copie el **[!UICONTROL ID de cliente]** y el **[!UICONTROL Secreto del cliente]** a un bloc de notas.
   1. En el cuadro **[!UICONTROL URL de redireccionamiento]**, agregue la URL HTTPS copiada en el paso anterior.
   1. Habilite la siguiente configuración de OAuth para la aplicación de [!DNL Adobe Sign] y haga clic en **[!UICONTROL Guardar]**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   Para obtener información paso a paso sobre cómo configurar OAuth para una aplicación [!DNL Adobe Sign] y obtener las claves, consulte la documentación para desarrolladores [Configurar OAuth para la aplicación](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md).

   ![Configuración de OAuth](assets/oauthconfig_new.png)

1. Vuelva a la página **[!UICONTROL Crear configuración de Adobe Sign]**. En la pestaña **[!UICONTROL Configuración]**, el campo **[!UICONTROL URL de OAuth]** muestra la URL predeterminada. El formato de la URL es el siguiente:

   `https://<shard>/public/oAuth/v2`

   Por ejemplo:
   `https://secure.na1.echosign.com/public/oauth/v2`

   donde:

   **na1** hace referencia a la partición predeterminada de la base de datos.

   Puede modificar el valor de la partición de la base de datos. Reinicie el servidor para poder utilizar el nuevo valor para el uso compartido de la base de datos.

   >[!NOTE]
   >Asegúrese de que las configuraciones de instancia de autor y publicación apuntan al mismo uso compartido. Si crea varias configuraciones de Adobe Sign para una organización, asegúrese de que todas las configuraciones utilicen el mismo uso compartido.

1. Vuelva a la página **[!UICONTROL Crear configuración de Adobe Sign]**. En la pestaña **[!UICONTROL Configuración]** especifique el **ID de cliente** (también denominado ID de aplicación) y el **secreto de cliente**. Utilice la aplicación [ID de cliente y Secreto de cliente de la aplicación Adobe Sign](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) creada para AEM Forms.

1. Seleccione la opción **[!UICONTROL Habilitar Adobe Sign para archivos adjuntos]** para anexar los archivos adjuntos a un formulario adaptable al documento de [!DNL Adobe Sign]correspondiente enviado para su firma.

1. Pulse **[!UICONTROL Conectar con Adobe Sign]**. Cuando se le soliciten credenciales, indique el nombre de usuario y la contraseña de la cuenta utilizada al crear la aplicación [!DNL Adobe Sign]. 

1. Pulse **[!UICONTROL Crear]** para crear la configuración de [!DNL Adobe Sign].

1. Abra la consola web de AEM. La URL es `https://'[server]:[port]'/system/console/configMgr`. 
1. Abra el **[!UICONTROL Servicio de configuración común de Forms].**
1. En el campo **[!UICONTROL Permitir]**, **seleccione** Todos los usuarios: todos los usuarios, anónimos o conectados, pueden obtener una vista previa de los archivos adjuntos, comprobar y firmar formularios y hacer clic en **[!UICONTROL Guardar].** La instancia de autor está configurada para usar [!DNL Adobe Sign].
1. Publique la configuración.
1. Use [replicación](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=es) para crear una configuración idéntica en las instancias de publicación correspondientes.

Ahora, [!DNL Adobe Sign] está integrado con AEM [!DNL Forms] y listo para utilizarlo en formularios adaptables. Para [usar el servicio Adobe Sign en un formulario adaptable](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), especifique el contenedor de configuración creado anteriormente en las propiedades del formulario adaptable.



## Configure el planificador [!DNL Adobe Sign] para sincronizar el estado de la firma {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Un [!DNL Adobe Sign] el formulario adaptable habilitado solo se envía una vez que todos los firmantes hayan completado el proceso de firma. De forma predeterminada, los servicios [!DNL Adobe Sign] de planificador tienen programada la comprobación (encuesta) de la respuesta del firmante cada 24 horas. Puede cambiar el intervalo predeterminado para su entorno. Realice los siguientes pasos para cambiar el intervalo predeterminado:

1. Inicie sesión en el servidor de AEM [!DNL Forms] con las credenciales de administrador y navegue hasta **Herramientas** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.

   También puede abrir la siguiente URL en una ventana del explorador:
   `https://[localhost]:'port'/system/console/configMgr`

1. Busque y abra la opción **[!UICONTROL Servicio de configuración de Adobe Sign]**. Especifique una [expresión cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) en el campo **[!UICONTROL Expresión del programador de actualización de estado]** y haga clic en **[!UICONTROL Guardar]**. Por ejemplo, para ejecutar el servicio de configuración diariamente a las 00:00, especifique `0 0 0 1/1 * ? *` en el campo **[!UICONTROL Expresión del programador de actualización de estado]**.

El intervalo predeterminado para sincronizar el estado de [!DNL Adobe Sign] ahora ha cambiado.

## Artículos relacionados {#related-articles}

* [Usar Adobe Sign en un formulario adaptable](../../forms/using/working-with-adobe-sign.md)
* [Usar Adobe Sign con AEM Forms (vídeo)](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/forms-and-sign/introduction.html?lang=es)
