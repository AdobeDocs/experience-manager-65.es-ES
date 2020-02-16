---
title: Configuración del etiquetado de recursos mediante el servicio de contenido inteligente
description: Obtenga información sobre cómo configurar el etiquetado inteligente y el etiquetado inteligente mejorado en AEM mediante el servicio de contenido inteligente.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Configuración del etiquetado de recursos mediante el servicio de contenido inteligente {#configure-asset-tagging-using-the-smart-content-service}

Puede integrar Adobe Experience Manager (AEM) con Smart Content Service mediante Adobe I/O. Utilice esta configuración para acceder al servicio de contenido inteligente desde AEM.

En el artículo se detallan las siguientes tareas clave necesarias para configurar el servicio de contenido inteligente. En el back-end, el servidor AEM autentica las credenciales de servicio con la puerta de enlace de E/S de Adobe antes de reenviar la solicitud al servicio de contenido inteligente.

* Cree una configuración de Smart Content Service en AEM para generar una clave pública. Obtenga un certificado público para la integración de OAuth.
* Cree una integración en Adobe I/O y cargue la clave pública generada.
* Configure la instancia de AEM utilizando la clave de API y otras credenciales de Adobe I/O.
* De forma opcional, habilite el etiquetado automático en la carga de recursos.

## Requisitos previos {#prerequisites}

Antes de utilizar el servicio de contenido inteligente, asegúrese de lo siguiente para crear una integración en Adobe I/O:

* Una cuenta de Adobe ID que tiene privilegios de administrador para la organización.
* El servicio de Smart Content Service está habilitado para su organización.

## Obtener certificado público {#obtain-public-certificate}

Un certificado público le permite autenticar su perfil en Adobe I/O.

1. En la interfaz de usuario de AEM, toque el logotipo de AEM y vaya a **[!UICONTROL Herramientas > Servicios]** de nube > Servicios **[!UICONTROL de nube]** preexistentes.

1. En la página Servicios de nube, toque o haga clic en **[!UICONTROL Configurar ahora]** en Etiquetas **[!UICONTROL inteligentes de]** recursos.
1. En el cuadro de diálogo **[!UICONTROL Crear configuración]** , especifique un título y un nombre para la configuración de etiquetas inteligentes. Toque o haga clic en **[!UICONTROL Crear]**.
1. En el cuadro de diálogo **[!UICONTROL AEM Smart Content Service]** , utilice los valores siguientes:

   **[!UICONTROL URL de servicio]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Servidor de autorización]**: `https://ims-na1.adobelogin.com`

   Deje el resto de campos en blanco por ahora (se proporcionará más tarde). Tap/click **[!UICONTROL OK]**.

   ![Cuadro de diálogo de AEM Smart Content Service para proporcionar la URL del servicio de contenido](assets/aem_scs.png)

1. Toque o haga clic en **[!UICONTROL Descargar certificado público para la integración]** de OAuth y descargue el archivo de certificado público `AEM-SmartTags.crt`.

   ![Una representación de la configuración creada para el servicio de etiquetado inteligente](assets/download_link.png)

### Volver a configurar cuando caduque un certificado {#certrenew}

Cuando caduca el certificado, ya no es de confianza. Para agregar un nuevo certificado, siga estos pasos. No puede renovar un certificado caducado.

1. Inicie sesión en la implementación de AEM como administrador. Haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.

1. Busque y haga clic en **[!UICONTROL dam-update-service]** user. Haga clic en la ficha **[!UICONTROL Almacén]** de claves.
1. Elimine la **[!UICONTROL similitud existente en el almacén de claves de búsqueda]** con el certificado caducado. Haga clic en **[!UICONTROL Guardar y cerrar]**.

   ![Eliminar la entrada de búsqueda por similitudes existente en Keystore para agregar un nuevo certificado de seguridad](assets/smarttags_delete_similaritysearch_keystore.png)

   Eliminar la entrada de búsqueda por similitudes existente en Keystore para agregar un nuevo certificado de seguridad

1. Vaya a **[!UICONTROL Herramientas]** > Servicios **[!UICONTROL de]** nube > Servicios **[!UICONTROL de nube]** heredados. Haga clic en **[!UICONTROL Etiquetas]** inteligentes de recursos > **[!UICONTROL Mostrar configuración]** > Configuraciones **** disponibles. Haga clic en la configuración requerida.

1. Para descargar un certificado público, haga clic en **[!UICONTROL Descargar certificado público para la integración]** de OAuth.
1. Acceda a [https://console.adobe.io](https://console.adobe.io) y vaya a los servicios de contenido inteligente existentes en la página **[!UICONTROL Integraciones]** . Cargue el nuevo certificado. Para obtener más información, consulte las instrucciones de [Creación de la integración](#create-adobe-i-o-integration)de Adobe I/O.

## Creación de la integración de Adobe I/O {#create-adobe-i-o-integration}

Para utilizar las API de Smart Content Service, cree una integración en Adobe I/O para generar clave de API, ID de cuenta técnica, ID de organización y Secreto de cliente.

1. Acceda a [https://console.adobe.io](https://console.adobe.io/).
1. En la página **[!UICONTROL Integraciones]** , seleccione la cuenta adecuada y compruebe que la función de organización asociada sea administrador del sistema.
1. Toque **[!UICONTROL Nueva integración]**.
1. En la página **[!UICONTROL Crear una nueva integración]** , seleccione **[!UICONTROL Acceder a una API]**. Puntee **[!UICONTROL Continuar]**.
1. En **[!UICONTROL Experience Cloud]**, seleccione Contenido **** inteligente. Puntee **[!UICONTROL Continuar]**.

   ![Al crear una nueva integración, seleccione Contenido inteligente en Experience Cloud, en las opciones disponibles](assets/smart_content.png)

1. En la página siguiente, seleccione **[!UICONTROL Nueva integración]**. Toque o haga clic en **[!UICONTROL Continuar]**.
1. En la página Detalles **[!UICONTROL de la]** integración, especifique un nombre para la puerta de enlace de integración y agregue una descripción.
1. En los certificados **[!UICONTROL de claves]** públicas, cargue el `AEM-SmartTags.crt` archivo que descargó anteriormente.
1. Tap/click **[!UICONTROL Create Integration]**.
1. Para ver la información de la integración, toque o haga clic en **[!UICONTROL Continuar a los detalles]** de la integración.

   ![En la ficha Información general, puede revisar la información proporcionada para la integración.](assets/integration_details.png)

## Configurar el servicio de contenido inteligente {#configure-smart-content-service}

Para configurar la integración, utilice los valores de los campos de ID de cuenta técnica, ID de organización, Secreto de cliente, Servidor de autorización y clave de API de la integración de Adobe I/O. La creación de una configuración de nube de etiquetas inteligentes permite la autenticación de solicitudes de API desde la instancia de AEM.

1. En la interfaz de usuario de AEM, toque o haga clic en el logotipo de AEM. Vaya a **[!UICONTROL Herramientas > Servicio de nube > Servicios]** de nube heredados para abrir la consola de Cloud Services.
1. En Etiquetas **[!UICONTROL inteligentes de]** recursos, abra la configuración creada anteriormente. En la página de configuración del servicio, haga clic en **[!UICONTROL Editar]**.
1. En el cuadro de diálogo **[!UICONTROL AEM Smart Content Service]** , utilice los valores predefinidos para los campos URL **[!UICONTROL de]** servicio y Servidor **[!UICONTROL de]** autorización.
1. Para los campos Clave **[!UICONTROL de]** API, Id **[!UICONTROL de cuenta]** técnica, Id **[!UICONTROL de]** organización y Secreto **[!UICONTROL de cliente]**, utilice los valores generados anteriormente.

## Validar la configuración {#validate-the-configuration}

Después de completar la configuración, puede utilizar un MBean de JMX para validar la configuración. Para validar, siga estos pasos.

1. Acceda a su servidor AEM en `https://[server]:[port]`.

1. Vaya a **[!UICONTROL Herramientas > Operaciones > Consola]** Web para abrir la consola OSGi. Haga clic en **[!UICONTROL Principal > JMX]**.
1. Haga clic en **[!UICONTROL com.day.cq.dam.similaritysearch.internal.impl]**. Abre **[!UICONTROL SimilitudBuscar varias tareas.]**
1. Haga clic en **[!UICONTROL validateConfigs()]**. En el cuadro de diálogo **[!UICONTROL Validar configuraciones]** , haga clic en **[!UICONTROL Invocar]**.

   El resultado de validación se muestra en el mismo cuadro de diálogo.

## Habilitar el etiquetado inteligente en el flujo de trabajo Actualizar recurso (opcional) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. En la interfaz de usuario de AEM, toque o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Herramientas > Flujo de trabajo > Modelos]**.
1. En la página Modelos **** de flujo de trabajo, seleccione el modelo de flujo de trabajo de recursos **[!UICONTROL de actualización de]** DAM.
1. Toque o haga clic en **[!UICONTROL Editar]** desde la barra de herramientas.
1. Expanda el panel lateral para mostrar los pasos. Arrastre el paso **[!UICONTROL Smart Tag Asset]** que está disponible en la sección DAM Workflow y colóquelo después del paso **[!UICONTROL Process Thumbnails]** .

   ![Agregue el paso del recurso de etiquetas inteligentes después del paso de la miniatura del proceso en el flujo de trabajo de recursos de actualización de DAM](assets/chlimage_1-105.png)

1. Abra el paso en modo de edición. En Configuración **** avanzada, asegúrese de que la opción **[!UICONTROL Avance]** del controlador está seleccionada.

   ![climage_1-3](assets/chlimage_1-106.png)

1. En la ficha **[!UICONTROL Argumentos]** , seleccione **[!UICONTROL Omitir errores]** si desea que el flujo de trabajo se complete aunque falle el paso de etiquetado automático.

   ![climage_1-4](assets/chlimage_1-107.png)

   Para etiquetar recursos al cargarlos, independientemente de si el etiquetado inteligente está activado en las carpetas, seleccione **[!UICONTROL Omitir marca]** de etiqueta inteligente.

   ![climage_1-5](assets/chlimage_1-108.png)

1. Toque **[!UICONTROL Aceptar]** para cerrar el paso del proceso y, a continuación, guarde el flujo de trabajo.

>[!MORELIKETHIS]
>
>* [Administrar etiquetas inteligentes](managing-smart-tags.md)
>* [Descripción general y cómo se enseñan las etiquetas inteligentes](enhanced-smart-tags.md)
>* [Directrices y reglas para la formación del servicio de contenido inteligente](smart-tags-training-guidelines.md)
>* [Tutorial de vídeo sobre cómo configurar etiquetas inteligentes](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)

