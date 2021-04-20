---
title: Integración de Adobe Sign con AEM Forms
seo-title: Integración de Adobe Sign con AEM Forms
description: Obtenga información sobre cómo configurar Adobe Sign para AEM Forms
seo-description: Obtenga información sobre cómo configurar Adobe Sign para AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Adobe Sign
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---


# Integrar [!DNL Adobe Sign] con AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] activa los flujos de trabajo de firma electrónica para formularios adaptables. Las firmas electrónicas mejoran los flujos de trabajo para procesar documentos para áreas legales, de ventas, de nómina, de gestión de recursos humanos y muchas otras áreas.

En un escenario típico de [!DNL Adobe Sign] y formularios adaptables, un usuario rellena un formulario adaptable a **solicitar un servicio**. Por ejemplo, una solicitud de tarjeta de crédito y un formulario de beneficios para los ciudadanos. Cuando un usuario rellena, envía y firma el formulario de solicitud, este se envía al proveedor de servicios para que realice más acciones. El proveedor de servicios revisa la aplicación y utiliza [!DNL Adobe Sign] para marcar la aplicación aprobada. Para habilitar flujos de trabajo de firma electrónica similares, puede integrar [!DNL Adobe Sign] con AEM [!DNL Forms].

Para utilizar [!DNL Adobe Sign] con AEM [!DNL Forms], configure [!DNL Adobe Sign] en AEM Cloud Services:

## Requisitos previos {#prerequisites}

Para integrar [!DNL Adobe Sign] con AEM [!DNL Forms], es necesario lo siguiente:

* Una cuenta de desarrollador activa de [Adobe Sign.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* Un servidor [SSL habilitado](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms].
* Una [aplicación de API de Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Credenciales (ID de cliente y Secreto de cliente) de la aplicación de API [!DNL Adobe Sign].
* Al reconfigurar, elimine la configuración existente [!DNL Adobe Sign] de las instancias de autor y publicación.
* Utilice la [clave criptográfica idéntica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) para las instancias de autor y publicación.

## Configurar [!DNL Adobe Sign] con AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

Una vez cumplidos los requisitos previos, realice los siguientes pasos para configurar [!DNL Adobe Sign] con AEM [!DNL Forms] en la instancia de autor:

1. En AEM instancia de autor [!DNL Forms], vaya a **Tools** ![hammer](assets/hammer.png) > **[!UICONTROL General]** > **[!UICONTROL Configuration Browser]**.
1. En la página **[!UICONTROL Explorador de configuración]**, pulse **[!UICONTROL Crear]**.
   * Consulte la documentación [Configuration Browser](/help/sites-administering/configurations.md) para obtener más información.
1. En el cuadro de diálogo **[!UICONTROL Crear configuración]**, especifique un **[!UICONTROL Título]** para la configuración, habilite **[!UICONTROL Configuraciones de nube]** y pulse **[!UICONTROL Crear]**. Crea un contenedor de configuración para servicios en la nube.
1. Vaya a **Tools** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** y seleccione el contenedor de configuración que creó en el paso anterior.

   >[!NOTE]
   >
   >Puede ejecutar los pasos 1-4 para crear un nuevo contenedor de configuración y una configuración [!DNL Adobe Sign] en el contenedor o utilizar la carpeta `global` existente en **Herramientas** ![martillo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Si crea la configuración en el nuevo contenedor de configuración, asegúrese de especificar el nombre del contenedor en el campo **[!UICONTROL Contenedor de configuración]** al crear un formulario adaptable.

   >[!NOTE]
   Asegúrese de que la dirección URL de la página de configuración de los servicios de nube comience por **HTTPS**. Si no es así, [habilite SSL](/help/sites-administering/ssl-by-default.md) para AEM servidor [!DNL Forms].

1. En la página de configuración, pulse **[!UICONTROL Crear]** para crear la configuración [!DNL Adobe Sign] en AEM [!DNL Forms].
1. En la pestaña **[!UICONTROL General]** de la página **[!UICONTROL Crear configuración de Adobe Sign]**, especifique un **[!UICONTROL Nombre]** para la configuración y pulse **[!UICONTROL Siguiente]**. Si lo desea, puede especificar un título y examinar para seleccionar una miniatura para la configuración.

1. Copie la dirección URL de la ventana actual del explorador en un bloc de notas. Es necesario configurar la aplicación [!DNL Adobe Sign] con AEM[!DNL Forms].

1. Configure los ajustes de OAuth para la aplicación [!DNL Adobe Sign]:

   1. Abra una ventana del explorador e inicie sesión en la cuenta de desarrollador de [!DNL Adobe Sign].
   1. Seleccione la aplicación configurada para AEM [!DNL Forms] y pulse **[!UICONTROL Configurar OAuth para la aplicación]**.
   1. Copie el **[!UICONTROL Client ID]** y **[!UICONTROL Client Secret]** en un bloc de notas.
   1. En el cuadro **[!UICONTROL Redirigir URL]**, añada la URL HTTPS copiada en el paso anterior.
   1. Habilite la siguiente configuración de OAuth para la aplicación [!DNL Adobe Sign] y haga clic en **[!UICONTROL Guardar]**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   Para obtener información paso a paso sobre la configuración de OAuth para una aplicación [!DNL Adobe Sign] y obtener las claves, consulte [Configuración de autenticación para la documentación para desarrolladores de la aplicación](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) .

   ![Configuración de OAuth](assets/oauthconfig_new.png)

1. Vuelva a la página **[!UICONTROL Crear configuración de Adobe Sign]**. En la pestaña **[!UICONTROL Settings]** , el campo **[!UICONTROL OAuth URL]** menciona la siguiente dirección URL predeterminada:

   https://secure.na1.echosign.com/public/oauth

   donde:

   **na1** hace referencia al uso compartido predeterminado de la base de datos.

   Puede modificar el valor del compartido de la base de datos. Reinicie el servidor para poder utilizar el nuevo valor para el uso compartido de la base de datos.

   >[!NOTE]
   Asegúrese de que las configuraciones de instancia de autor y publicación apuntan al mismo uso compartido. Si crea varias configuraciones de Adobe Sign para una organización, asegúrese de que todas las configuraciones utilicen el mismo uso compartido.

1. Especifique el **ID de cliente** (también denominado ID de aplicación) y el **Secreto de cliente** copiados en el paso 8. Seleccione la opción **[!UICONTROL Enable Adobe Sign for attachment also]** para anexar los archivos adjuntos a un formulario adaptable al documento [!DNL Adobe Sign] correspondiente enviado para firmar.

   Toque **[!UICONTROL Conectarse a Adobe Sign]**. Cuando se le soliciten credenciales, proporcione el nombre de usuario y la contraseña de la cuenta utilizada al crear la aplicación [!DNL Adobe Sign].

   Pulse **[!UICONTROL Crear]** para crear la configuración [!DNL Adobe Sign].

1. Abra AEM consola web. La dirección URL es `https://'[server]:[port]'/system/console/configMgr`
1. Abra **[!UICONTROL Servicio de configuración común de Forms].**
1. En el campo **[!UICONTROL Permitir]**, **seleccione** Todos los usuarios: todos los usuarios, anónimos o conectados, pueden obtener una vista previa de los archivos adjuntos, verificar y firmar formularios y hacer clic en **[!UICONTROL Guardar].** La instancia de autor está configurada para usar  [!DNL Adobe Sign].
1. Publique la configuración.
1. Utilice [replication](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) para crear una configuración idéntica en las instancias de publicación correspondientes.

Ahora, [!DNL Adobe Sign] está integrado con AEM [!DNL Forms] y listo para usar en formularios adaptables. Para [utilizar el servicio Adobe Sign en un formulario adaptable](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), especifique el contenedor de configuración creado anteriormente en las propiedades del formulario adaptable.



## Configure el programador [!DNL Adobe Sign] para sincronizar el estado de firma {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Un formulario adaptable habilitado para [!DNL Adobe Sign] solo se envía después de que todos los firmantes hayan completado el proceso de firma. De forma predeterminada, los [!DNL Adobe Sign] servicios del planificador están programados para comprobar la respuesta del firmante (encuesta) cada 24 horas. Puede cambiar el intervalo predeterminado para su entorno. Realice los siguientes pasos para cambiar el intervalo predeterminado:

1. Inicie sesión en AEM servidor [!DNL Forms] con credenciales de administrador y vaya a **Herramientas** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.

   También puede abrir la siguiente URL en una ventana del explorador:
   `https://[localhost]:'port'/system/console/configMgr`

1. Busque y abra la opción **[!UICONTROL Adobe Sign Configuration Service]**. Especifique una [expresión de cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) en el campo **[!UICONTROL Expresión del programador de actualización de estado]** y haga clic en **[!UICONTROL Guardar]**. Por ejemplo, para ejecutar el servicio de configuración diariamente a las 00:00 a.m., especifique `0 0 0 1/1 * ? *` en el campo **[!UICONTROL Expresión del programador de actualización de estado]**.

El intervalo predeterminado para sincronizar el estado de [!DNL Adobe Sign] ahora cambia.

## Artículos relacionados {#related-articles}

* [Uso de Adobe Sign en un formulario adaptable](../../forms/using/working-with-adobe-sign.md)
* [Uso de Adobe Sign con AEM Forms (vídeo)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)


