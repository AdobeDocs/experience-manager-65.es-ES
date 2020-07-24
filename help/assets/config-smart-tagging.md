---
title: Configure el etiquetado de recursos mediante el servicio de contenido inteligente.
description: Aprenda a configurar el etiquetado inteligente y el etiquetado inteligente mejorado en [!DNL Adobe Experience Manager], mediante el servicio de contenido inteligente.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 29cf202b2522b4e624960e8b911f77ec7f291e24
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 43%

---


# Configuración del etiquetado de recursos mediante el servicio de contenido inteligente {#configure-asset-tagging-using-the-smart-content-service}

Puede realizar la integración [!DNL Adobe Experience Manager] con Smart Content Service mediante Adobe Developer Console. Utilice esta configuración para acceder al servicio de contenido inteligente desde dentro [!DNL Experience Manager].

En el artículo se detallan las siguientes tareas clave necesarias para configurar el servicio de contenido inteligente. At the back end, the [!DNL Experience Manager] server authenticates your service credentials with the Adobe Developer Console gateway before forwarding your request to the Smart Content Service.

1. Create a Smart Content Service configuration in [!DNL Experience Manager] to generate a public key. [Obtenga un certificado público para la integración de OAuth.](#obtain-public-certificate)
1. [Cree una integración en Adobe Developer Console y cargue la clave pública generada.](#create-adobe-i-o-integration)
1. [Configure la implementación](#configure-smart-content-service) utilizando la clave de API y otras credenciales de Adobe Developer Console.
1. [Compruebe la configuración](#validate-the-configuration).
1. Optionally, [enable auto-tagging on asset upload](#enable-smart-tagging-in-the-update-asset-workflow-optional).

## Requisitos previos {#prerequisites}

Antes de utilizar Smart Content Service, asegúrese de lo siguiente para crear una integración en Adobe Developer Console:

* Cuenta de Adobe ID que tiene privilegios de administrador para la organización.
* El servicio de Smart Content Service está habilitado para su organización.

Para habilitar Etiquetas inteligentes mejoradas, además de las anteriores, instale también el último Service Pack [de](https://helpx.adobe.com/es/experience-manager/aem-releases-updates.html)AEM.

## Obtener un certificado público {#obtain-public-certificate}

El certificado público permite autenticar el perfil en Adobe Developer Console.

1. En la interfaz [!DNL Experience Manager] de usuario, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Service]** > Cloud Service **** preexistentes.

1. In the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.
1. En el cuadro de diálogo **[!UICONTROL Crear configuración]** , especifique un título y un nombre para la configuración de etiquetas inteligentes. Haga clic en **[!UICONTROL Crear]**.
1. En el cuadro de diálogo **[!UICONTROL AEM Smart Content Service]** , utilice los valores siguientes:

   **[!UICONTROL URL de servicio]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Servidor de autorización]**: `https://ims-na1.adobelogin.com`

   Deje el resto de campos en blanco por ahora (se proporcionará más tarde). Haga clic en **[!UICONTROL Aceptar]**.

   ![Cuadro de diálogo Experience Manager Smart Content Service para proporcionar la URL del servicio de contenido](assets/aem_scs.png)

   >[!NOTE]
   >
   >La dirección URL proporcionada como URL [!UICONTROL de servicio] no es accesible a través del explorador y genera un error 404. La configuración funciona correctamente con el mismo valor del parámetro de URL [!UICONTROL de] servicio. Para obtener información sobre el estado general del servicio y la programación de mantenimiento, consulte [https://status.adobe.com](https://status.adobe.com).

1. Haga clic en **[!UICONTROL Descargar certificado público para la integración]** de OAuth y descargue el archivo de certificado público `AEM-SmartTags.crt`.

   ![Una representación de la configuración creada para el servicio de etiquetado inteligente](assets/smart-tags-download-public-cert.png)

### Reconfigure when a certificate expires {#certrenew}

Una vez que caduca un certificado, ya no es de confianza. No puede renovar un certificado caducado. Para añadir un nuevo certificado, siga estos pasos.

1. Inicie sesión en la implementación [!DNL Experience Manager] como administrador. Haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.

1. Busque y haga clic en el usuario **[!UICONTROL dam-update-service]**. Haga clic en la pestaña **[!UICONTROL Almacén de claves.]**
1. Elimine el almacén de claves **[!UICONTROL similaritysearch]** y el certificado caducado. Haga clic en **[!UICONTROL Guardar y cerrar]**.

   ![Eliminar la entrada de búsqueda por similitudes existente en Keystore para agregar un nuevo certificado de seguridad](assets/smarttags_delete_similaritysearch_keystore.png)

   *Imagen: Elimine la entrada`similaritysearch`en el almacén de claves para añadir un nuevo certificado de seguridad.*

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Servicios de nube heredados]**. Haga clic en **[!UICONTROL Etiquetas inteligentes de recursos]** > **[!UICONTROL Mostrar configuración]** > **[!UICONTROL Configuraciones disponibles]**. Haga clic en la configuración requerida.

1. To download a public certificate, click **[!UICONTROL Download Public Certificate for OAuth Integration]**.
1. Acceda a [https://console.adobe.io](https://console.adobe.io) y vaya a los servicios de contenido inteligente existentes en la página **[!UICONTROL Integraciones]** . Cargue el nuevo certificado. For more information, see the instructions in [Create Adobe Developer Console integration](#create-adobe-i-o-integration).

## Creación de la integración de Adobe Developer Console {#create-adobe-i-o-integration}

Para utilizar las API de Smart Content Service, cree una integración en Adobe Developer Console para generar clave de API, ID de cuenta técnica, ID de organización y Secreto de cliente.

1. Acceda a [https://console.adobe.io](https://console.adobe.io/) en el explorador. Seleccione la cuenta adecuada y compruebe que la función de organización asociada sea administrador del sistema.
1. Cree un proyecto con el nombre que desee. Haga clic en **[!UICONTROL Añadir API]**.
1. En la página **[!UICONTROL Añadir una API]** , seleccione **[!UICONTROL Experience Cloud]** y **[!UICONTROL Contenido inteligente]**. Haga clic en **[!UICONTROL Siguiente]**. 
1. Seleccione **[!UICONTROL Cargar la clave pública]**. Proporcione el archivo de certificado descargado de [!DNL Experience Manager]. Se muestra un mensaje con las [!UICONTROL claves públicas cargadas correctamente]. Haga clic en **[!UICONTROL Siguiente]**. 
1. La página [!UICONTROL Crear una nueva página de credenciales de cuenta de servicio (JWT)] muestra la clave pública de la cuenta de servicio que se acaba de configurar. Haga clic en **[!UICONTROL Siguiente]**. 
1. En la página **[!UICONTROL Seleccionar perfiles de producto]**, seleccione **[!UICONTROL Servicios de contenido inteligente]**. Haga clic en **[!UICONTROL Guardar API configurada]**. La página muestra más información sobre la configuración. Mantenga esta página abierta para copiar y añadir estos valores en Experience Manager al configurar las etiquetas inteligentes en [!DNL Experience Manager].

   ![En la pestaña Información general, puede revisar la información proporcionada para la integración.](assets/integration_details.png)

## Configurar el servicio de contenido inteligente {#configure-smart-content-service}

Para configurar la integración, utilice los valores de los campos ID de cuenta técnica, ID de organización, Secreto de cliente, Servidor de autorización y Clave de API de la integración de Adobe Developer Console. La creación de una configuración de nube de etiquetas inteligentes permite la autenticación de solicitudes de API desde la [!DNL Experience Manager] implementación.

1. En [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Service]** > Cloud Service **** preexistentes para abrir la consola de [!UICONTROL Cloud Service] .
1. En Etiquetas **[!UICONTROL inteligentes de]** recursos, abra la configuración creada anteriormente. En la página de configuración del servicio, haga clic en **[!UICONTROL Editar]**.
1. En el cuadro de diálogo **[!UICONTROL AEM Smart Content Service]**, utilice los valores predefinidos para los campos **[!UICONTROL URL de servicio]** y **[!UICONTROL Servidor de autorización]**.
1. Para los campos **[!UICONTROL Clave de API]**, **[!UICONTROL Id de cuenta técnica]**, **[!UICONTROL Id de organización]** y **[!UICONTROL Secreto de cliente]**, utilice los valores generados anteriormente.

## Validación de la configuración {#validate-the-configuration}

Después de completar la configuración, puede utilizar un MBean de JMX para validar la configuración. Para validar, siga estos pasos.

1. Acceda a su [!DNL Experience Manager] servidor en `https://[aem_server]:[port]`.
1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > Consola **** Web para abrir la consola OSGi. Haga clic en **[!UICONTROL Principal]>[!UICONTROL JMX]**.
1. Haga clic `com.day.cq.dam.similaritysearch.internal.impl`. Abre **[!UICONTROL SimilitudBuscar Tareas]** diversas.
1. Haga clic `validateConfigs()`. En el cuadro de diálogo **[!UICONTROL Validar configuraciones]** , haga clic en **[!UICONTROL Invocar]**. Los resultados de validación se muestran en el mismo cuadro de diálogo.

## Habilitar el etiquetado inteligente en el flujo de trabajo de recursos [!UICONTROL de actualización de] DAM (opcional) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. In [!DNL Experience Manager], go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. En la página **[!UICONTROL Modelos de flujo de trabajo]**, seleccione el modelo de flujo de trabajo de **[!UICONTROL recursos de actualización de DAM]**.
1. Haga clic en **[!UICONTROL Editar]** en la barra de herramientas.
1. Expanda el panel lateral para mostrar los pasos. Arrastre el paso **[!UICONTROL Recurso de etiqueta inteligente]** que está disponible en la sección Flujo de trabajo de DAM y colóquelo después del paso **[!UICONTROL Miniaturas del proceso]**.

   ![Añada el paso del recurso de etiquetas inteligentes después del paso de miniaturas de proceso en el flujo de trabajo de recursos de actualización de DAM](assets/smart-tag-in-dam-update-asset-workflow.png)

   *Imagen: Añada el paso del recurso de etiquetas inteligentes después del paso de miniaturas de proceso en el flujo de trabajo de recursos de actualización de DAM*

1. Abra el paso en modo de edición. En **[!UICONTROL Configuración avanzada]**, compruebe que la opción **[!UICONTROL Avance del controlador]** está seleccionada.

   ![Configurar el flujo de trabajo de recursos de actualización de DAM y agregar el paso de etiquetas inteligentes](assets/smart-tag-step-properties-workflow1.png)

1. En la pestaña **[!UICONTROL Argumentos]**, seleccione **[!UICONTROL Omitir errores]** si desea que el flujo de trabajo se complete aunque falle el paso de etiquetado automático.

   Para etiquetar recursos al cargarlos, independientemente de si el etiquetado inteligente está activado en las carpetas, seleccione **[!UICONTROL Omitir indicador de etiqueta inteligente]**.

   ![Configure el flujo de trabajo de recursos de actualización DAM para agregar el paso de la etiqueta inteligente y seleccione Omitir el indicador de etiqueta inteligente](assets/smart-tag-step-properties-workflow2.png)

1. Haga clic en **[!UICONTROL Aceptar]** para cerrar el paso del proceso y, a continuación, guarde el flujo de trabajo.

>[!MORELIKETHIS]
>
>* [Administrar etiquetas inteligentes](managing-smart-tags.md)
>* [Descripción general y cómo se enseñan las etiquetas inteligentes](enhanced-smart-tags.md)
>* [Directrices y reglas para la formación del servicio de contenido inteligente](smart-tags-training-guidelines.md)
>* [Tutorial de vídeo sobre cómo configurar etiquetas inteligentes](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)

