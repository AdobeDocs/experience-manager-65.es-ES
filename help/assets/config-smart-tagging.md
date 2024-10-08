---
title: Configuración del etiquetado de recursos mediante el servicio de contenido inteligente
description: Aprenda a configurar el etiquetado inteligente y el etiquetado inteligente mejorado en  [!DNL Adobe Experience Manager] mediante el servicio de contenido inteligente.
contentOwner: AG
role: Admin
feature: Tagging,Smart Tags
exl-id: 9f68804f-ba15-4f83-ab1b-c249424b1396
solution: Experience Manager, Experience Manager Assets
source-git-commit: 5aff321eb52c97e076c225b67c35e9c6d3371154
workflow-type: tm+mt
source-wordcount: '2415'
ht-degree: 20%

---

# Preparar [!DNL Assets] para el etiquetado inteligente {#configure-asset-tagging-using-the-smart-content-service}

Antes de empezar a etiquetar recursos usando Smart Content Services, integre [!DNL Experience Manager Assets] con Adobe Developer Console para usar el servicio inteligente de [!DNL Adobe Sensei]. Una vez configurado, entrene el servicio con unas pocas imágenes y una etiqueta.

>[!NOTE]
>
>* Smart Content Services ya no está disponible para los nuevos clientes locales de [!DNL Experience Manager Assets]. Los clientes locales existentes, que ya tienen esta capacidad habilitada, pueden seguir utilizando los servicios de contenido inteligente.
>* Servicios de contenido inteligente disponible para los clientes existentes de Managed Services [!DNL Experience Manager Assets], que ya tienen esta capacidad habilitada.
>* Los nuevos clientes de [!DNL Experience Manager Assets] Managed Services pueden seguir las instrucciones que se mencionan en este artículo para configurar Smart Content Services.

Antes de usar el servicio de contenido inteligente, asegúrese de lo siguiente:

* [Integrar con Adobe Developer Console](#integrate-adobe-io).
* [Entrenar el servicio de contenido inteligente](#training-the-smart-content-service).

* Instale el [[!DNL Experience Manager] Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=es) más reciente.

## Integración con Adobe Developer Console {#integrate-adobe-io}

Al integrarse con Adobe Developer Console, el servidor [!DNL Experience Manager] autentica las credenciales del servicio con la puerta de enlace de Adobe Developer Console antes de reenviar la solicitud al servicio de contenido inteligente. Para integrarse, necesita una cuenta de Adobe ID que tenga privilegios de administrador para la organización y la licencia de Smart Content Service comprada y habilitada para su organización.

Para configurar el servicio de contenido inteligente, siga estos pasos de nivel superior:

1. Para generar una clave pública, [Cree una configuración de Smart Content Service](#obtain-public-certificate) en [!DNL Experience Manager]. [Obtenga un certificado público para la integración de OAuth.](#obtain-public-certificate)

1. [Cree una integración en Adobe Developer Console y cargue la clave pública generada.](#create-adobe-i-o-integration)

1. [Configure su implementación](#configure-smart-content-service) con la clave de API y otras credenciales de Adobe Developer Console.

1. [Compruebe la configuración](#validate-the-configuration).

1. De manera opcional, [habilite el etiquetado automático en la carga de recursos](#enable-smart-tagging-in-the-update-asset-workflow-optional).

### Obtenga un certificado público creando la configuración del servicio de contenido inteligente {#obtain-public-certificate}

Un certificado público permite autenticar el perfil en Adobe Developer Console.

1. En la interfaz de usuario de [!DNL Experience Manager], acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Service heredados]**.

1. En la página Cloud Service, haga clic en **[!UICONTROL Configurar ahora]** en **[!UICONTROL Etiquetas inteligentes de Assets]**.

1. En el cuadro de diálogo **[!UICONTROL Crear configuración]**, especifique un título y un nombre para la configuración de etiquetas inteligentes. Haga clic en **[!UICONTROL Crear]**.

1. AEM En el cuadro de diálogo **[!UICONTROL Servicio de contenido inteligente]**, use los siguientes valores:

   **[!UICONTROL URL de servicio]**: `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   Por ejemplo, `https://smartcontent.adobe.io/apac`. Puede especificar `na`, `emea` o `apac` como las regiones en las que está alojada la instancia de autor de Experience Manager.

   >[!NOTE]
   >
   >Si el servicio administrado de Experience Manager se aprovisiona antes del 1 de septiembre de 2022, utilice la siguiente URL de servicio:
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Servidor de autorización]**: `https://ims-na1.adobelogin.com`

   Deje los demás campos en blanco por ahora (se proporcionarán más adelante). Haga clic en **[!UICONTROL OK]**.

   ![Cuadro de diálogo Servicio de contenido inteligente de Experience Manager para proporcionar la URL del servicio de contenido](assets/aem_scs.png)


   *Figura: Cuadro de diálogo Servicio de contenido inteligente para proporcionar la URL del servicio de contenido*

   >[!NOTE]
   >
   >La URL proporcionada como [!UICONTROL URL de servicio] no es accesible a través del explorador y genera un error 404. La configuración funciona correctamente con el mismo valor del parámetro [!UICONTROL Service URL]. Para ver el estado general del servicio y el programa de mantenimiento, consulte [https://status.adobe.com](https://status.adobe.com).

1. Haga clic en **[!UICONTROL Descargar certificado público para la integración de OAuth]** y descargue el archivo de certificado público `AEM-SmartTags.crt`.

   ![Representación de la configuración creada para el servicio de etiquetado inteligente](assets/smart-tags-download-public-cert.png)


   *Figura: Configuración del servicio de etiquetado inteligente.*

#### Volver a configurar cuando caduque un certificado {#certrenew}

Una vez que caduca un certificado, ya no es de confianza. No puede renovar un certificado caducado. Para agregar un certificado, siga estos pasos.

1. Inicie sesión en la implementación [!DNL Experience Manager] como administrador. Haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.

1. Busque y haga clic en el usuario **[!UICONTROL dam-update-service]**. Haga clic en la pestaña **[!UICONTROL Keystore]**.

1. Elimine el almacén de claves **[!UICONTROL similaritysearch]** y el certificado caducado. Haga clic en **[!UICONTROL Guardar y cerrar]**.

   ![Elimine la entrada de búsqueda de similitud existente en el almacén de claves para agregar un certificado de seguridad](assets/smarttags_delete_similaritysearch_keystore.png)


   *Imagen: elimine la entrada `similaritysearch` existente en el almacén de claves para agregar un certificado de seguridad.*

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Servicios de nube heredados]**. Haga clic en **[!UICONTROL Etiquetas inteligentes de recursos]** > **[!UICONTROL Mostrar configuración]** > **[!UICONTROL Configuraciones disponibles]**. Haga clic en la configuración requerida.

1. Para descargar un certificado público, haga clic en **[!UICONTROL Descargar certificado público para la integración de OAuth]**.

1. Acceda a [https://console.adobe.io](https://console.adobe.io) y vaya a los Servicios de contenido inteligente existentes en la página **[!UICONTROL Integraciones]**. Cargue el nuevo certificado. Para obtener más información, consulte las instrucciones de [Crear integración de Adobe Developer Console](#create-adobe-i-o-integration).

### Creación de la integración con Adobe Developer Console {#create-adobe-i-o-integration}

Para usar las API del servicio de contenido inteligente, cree una integración en Adobe Developer Console para obtener [!UICONTROL clave de API] (generada en el campo [!UICONTROL ID de cliente] de la integración de Adobe Developer Console), [!UICONTROL ID de cuenta técnica], [!UICONTROL ID de organización] y [!UICONTROL SECRETO DE CLIENTE] para la [!UICONTROL configuración del servicio de etiquetado inteligente de Assets] de la nube en [!DNL Experience Manager].

1. Acceda a [https://console.adobe.io](https://console.adobe.io/) en el explorador. Seleccione la cuenta adecuada y compruebe que la función de organización asociada sea administrador del sistema.

1. Cree un proyecto con el nombre que desee. Haga clic en **[!UICONTROL Añadir API]**.

1. En la página **[!UICONTROL Añadir una API]** , seleccione **[!UICONTROL Experience Cloud]** y **[!UICONTROL Contenido inteligente]**. Haga clic en **[!UICONTROL Siguiente]**. 

1. Seleccione **[!UICONTROL Cargar la clave pública]**. Proporcione el archivo de certificado descargado de [!DNL Experience Manager]. Se muestra un mensaje con las [!UICONTROL claves públicas cargadas correctamente]. Haga clic en **[!UICONTROL Siguiente]**. 

   [!UICONTROL La página Crear una nueva credencial de cuenta de servicio (JWT)] muestra la clave pública de la cuenta de servicio.

1. Haga clic en **[!UICONTROL Siguiente]**. 

1. En la página **[!UICONTROL Seleccionar perfiles de producto]**, seleccione **[!UICONTROL Servicios de contenido inteligente]**. Haga clic en **[!UICONTROL Guardar API configurada]**.

   La página muestra más información sobre la configuración. Mantenga esta página abierta para copiar y agregar estos valores en [!UICONTROL Configuración del servicio de etiquetado inteligente de Assets] de la configuración de la nube en [!DNL Experience Manager] para configurar las etiquetas inteligentes.

   ![En la pestaña Información general, puede revisar la información proporcionada para la integración.](assets/integration_details.png)


   *Figura: Detalles de la integración en Adobe Developer Console*

### Configurar el servicio de contenido inteligente {#configure-smart-content-service}

>[!CAUTION]
>
>Antes, las configuraciones que se realizaban con las credenciales de JWT ahora están sujetas a desaprobación en Adobe Developer Console. No puede crear nuevas credenciales de JWT después del 3 de junio de 2024. Estas configuraciones ya no se pueden crear ni actualizar, pero sí migrar a las configuraciones de OAuth.
> AEM Consulte [Configuración de integraciones de IMS para el usuario](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service)
>Consulte [Pasos para configurar OAuth para usuarios locales](#config-oauth-onprem)
> Consulte [Solución de problemas de etiquetas inteligentes para credenciales de OAuth](#config-smart-tagging.md)

Para configurar la integración, use los valores de los campos [!UICONTROL ID. DE CUENTA TÉCNICA], [!UICONTROL ID. DE ORGANIZACIÓN], [!UICONTROL SECRETO DE CLIENTE] e [!UICONTROL ID. DE CLIENTE] de la integración de Adobe Developer Console. La creación de una configuración de nube de etiquetas inteligentes permite la autenticación de solicitudes de API desde la implementación de [!DNL Experience Manager].

1. En [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Services heredados]** para abrir la consola de [!UICONTROL Cloud Services].

1. En **[!UICONTROL Etiquetas inteligentes de Assets]**, abra la configuración creada anteriormente. En la página de configuración del servicio, haga clic en **[!UICONTROL Editar]**.

1. En el cuadro de diálogo **[!UICONTROL AEM Smart Content Service]**, utilice los valores predefinidos para los campos **[!UICONTROL URL de servicio]** y **[!UICONTROL Servidor de autorización]**.

1. Para los campos [!UICONTROL Clave de API], [!UICONTROL ID de cuenta técnica], [!UICONTROL ID de organización] y [!UICONTROL Secreto de cliente], copie y utilice los siguientes valores generados en la [integración de Adobe Developer Console](#create-adobe-i-o-integration).

   | [!UICONTROL Configuración del servicio de etiquetado inteligente de Assets] | [!DNL Adobe Developer Console] campos de integración |
   |--- |--- |
   | [!UICONTROL Clave De Api] | [!UICONTROL ID. DE CLIENTE] |
   | [!UICONTROL Id. de cuenta técnica] | [!UICONTROL ID. DE CUENTA TÉCNICA] |
   | [!UICONTROL ID de organización] | [!UICONTROL ID. DE ORGANIZACIÓN] |
   | [!UICONTROL Secreto de cliente] | [!UICONTROL SECRETO DE CLIENTE] |

### Configuración de OAuth para usuarios locales {#config-oauth-onprem}

#### Requisitos previos {#prereqs-config-oauth-onprem}

Un ámbito de autorización es una cadena OAuth que contiene los siguientes requisitos previos:

* Cree una nueva integración de OAuth en [Developer Console](https://developer.adobe.com/console/user/servicesandapis) con `ClientID`, `ClientSecretID` y `OrgID`.
* Agregar los siguientes archivos en esta ruta de acceso `/apps/system/config in crx/de`:
   * `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`
   * `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`

#### Configuración de OAuth para usuarios locales {#steps-config-oauth-onprem}

1. Agregar o actualizar las siguientes propiedades en `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`:

   * `auth.token.provider.authorization.grants="client_credentials"`
   * `auth.token.provider.orgId="<OrgID>"`
   * `auth.token.provider.default.claims=("\"iss\"\ :\ \"<OrgID>\"")`
   * `auth.token.provider.scope="read_pc.dma_smart_content,\ openid,\ AdobeID,\ additional_info.projectedProductContext"`
     `auth.token.validator.type="adobe-ims-similaritysearch"`
   * Actualice `auth.token.provider.client.id` con el ID de cliente de la nueva configuración de OAuth.
   * Actualizar `auth.access.token.request` a `"https://ims-na1.adobelogin.com/ims/token/v3"`
2. Cambie el nombre del archivo a `com.adobe.granite.auth.oauth.accesstoken.provider-<randomnumber>.config`.
3. Siga estos pasos en `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`:
   * Actualice la propiedad auth.ims.client.secret con el Secreto del cliente desde la nueva integración de OAuth.
   * Cambie el nombre del archivo a `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl-<randomnumber>.config`
4. Guarde todos los cambios en la consola de desarrollo del repositorio de contenido, por ejemplo, CRXDE.
5. Vaya a `/system/console/configMgr` y reemplace la configuración de OSGi de `.<randomnumber>` a `-<randomnumber>`.
6. Elimine la configuración anterior de `"Access Token provider name: adobe-ims-similaritysearch"` en `/system/console/configMgr`.
7. Reinicie la consola.

### Validar la configuración {#validate-the-configuration}

Una vez completada la configuración, puede utilizar un MBean de JMX para validar la configuración. Para validar, siga estos pasos.

1. Obtenga acceso a su servidor [!DNL Experience Manager] en `https://[aem_server]:[port]`.

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]** para abrir la consola OSGi. Haga clic en **[!UICONTROL Principal] > [!UICONTROL JMX]**.

1. Haga clic en `com.day.cq.dam.similaritysearch.internal.impl`. Se abrirá **[!UICONTROL Tareas varias de SimilaritySearch]**.

1. Haga clic en `validateConfigs()`. En el diálogo **[!UICONTROL Validar configuraciones]**, haga clic en **[!UICONTROL Invocar]**.

Los resultados de validación se muestran en el mismo cuadro de diálogo.

### Habilitar el etiquetado inteligente en el flujo de trabajo [!UICONTROL Recurso de actualización DAM] (opcional) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. En [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.

1. En la página **[!UICONTROL Modelos de flujo de trabajo]**, seleccione el modelo de flujo de trabajo de **[!UICONTROL recursos de actualización de DAM]**.

1. Haga clic en **[!UICONTROL Editar]** en la barra de herramientas.

1. Expanda el panel lateral para mostrar los pasos. Arrastre el paso **[!UICONTROL Recurso de etiqueta inteligente]** que está disponible en la sección Flujo de trabajo de DAM y colóquelo después del paso **[!UICONTROL Miniaturas del proceso]**.

   ![Añada el paso del recurso de etiquetas inteligentes después del paso de miniaturas de proceso en el flujo de trabajo de recursos de actualización de DAM](assets/smart-tag-in-dam-update-asset-workflow.png)

   *Imagen: agregue el paso del recurso de etiquetas inteligentes después del paso de miniaturas de proceso en el flujo de trabajo [!UICONTROL Recurso de actualización DAM].*

1. Abra el paso en modo de edición. En **[!UICONTROL Configuración avanzada]**, compruebe que la opción **[!UICONTROL Avance del controlador]** está seleccionada.

   ![Configurar el flujo de trabajo de recursos de actualización DAM y agregar el paso de etiquetas inteligentes](assets/smart-tag-step-properties-workflow1.png)


   *Figura: Configurar el flujo de trabajo de recursos de actualización de DAM y agregar el paso de etiquetas inteligentes*

1. En la pestaña **[!UICONTROL Argumentos]**, seleccione **[!UICONTROL Omitir errores]** si desea que el flujo de trabajo se complete aunque falle el paso de etiquetado automático.

   ![Configure el flujo de trabajo del recurso de actualización DAM para agregar el paso de la etiqueta inteligente y seleccionar el avance del controlador](assets/smart-tag-step-properties-workflow2.png)


   *Figura: Configurar el flujo de trabajo de recursos de actualización de DAM para agregar el paso de etiquetas inteligentes y seleccionar el avance del controlador*

   Para etiquetar recursos al cargarlos, independientemente de si el etiquetado inteligente está activado en las carpetas, seleccione **[!UICONTROL Omitir indicador de etiqueta inteligente]**.

   ![Configure el flujo de trabajo del recurso de actualización DAM para agregar el paso de la etiqueta inteligente y seleccione omitir indicador de etiqueta inteligente](assets/smart-tag-step-properties-workflow3.png)


   *Figura: Configurar el flujo de trabajo de recursos de actualización de DAM para agregar el paso de etiquetas inteligentes y seleccionar la opción para omitir el indicador de etiquetas inteligentes.*

1. Haga clic en **[!UICONTROL Aceptar]** para cerrar el paso del proceso y, a continuación, guarde el flujo de trabajo.

## Formación del servicio de contenido inteligente {#training-the-smart-content-service}

Para que el servicio de contenido inteligente reconozca su taxonomía empresarial, ejecútela en un conjunto de recursos que ya incluyan etiquetas relevantes para su negocio. Para etiquetar de forma eficaz las imágenes de marca, el servicio de contenido inteligente requiere que las imágenes de formación se ajusten a determinadas directrices. Después de la formación, el servicio puede aplicar la misma taxonomía a un conjunto similar de recursos.

Puede entrenar el servicio varias veces para mejorar su capacidad de aplicar etiquetas relevantes. Después de cada ciclo de formación, ejecute un flujo de trabajo de etiquetado y compruebe si los recursos están etiquetados correctamente.

Puede entrenar el Servicio de contenido inteligente periódicamente o según sea necesario.

>[!NOTE]
>
>El flujo de trabajo de formación se ejecuta únicamente en carpetas.

### Directrices para la formación {#guidelines-for-training}

Para obtener los mejores resultados, las imágenes del conjunto de formación se ajustan a las siguientes directrices:

**Cantidad y tamaño:** Mínimo de 30 imágenes por etiqueta. Mínimo de 500 píxeles en el lado más largo.

**Coherencia**: las imágenes utilizadas para una etiqueta específica son visualmente similares.

Por ejemplo, no es aconsejable etiquetar todas estas imágenes como `my-party` (para aprendizaje) porque no son visualmente similares.

![Imágenes ilustrativas para ejemplificar las directrices de formación](/help/assets/assets/do-not-localize/coherence.png)

**Cobertura**: Use suficiente variedad en las imágenes del curso de formación. La idea es ofrecer algunos ejemplos, pero razonablemente diversos, para que el Experience Manager aprenda a centrarse en las cosas correctas. Si aplica la misma etiqueta a imágenes visualmente distintas, incluya al menos cinco ejemplos de cada tipo.

Por ejemplo, para la etiqueta *model-down-pose*, incluya más imágenes de aprendizaje similares a la imagen resaltada a continuación para que el servicio identifique las imágenes similares con mayor precisión durante el etiquetado.

![Imágenes ilustrativas para ejemplificar las directrices de formación](/help/assets/assets/do-not-localize/coverage_1.png)

**Distracción/obstrucción**: El servicio se entrena mejor con las imágenes que tienen menos distracción (fondos destacados, acompañamientos no relacionados, como objetos/personas con el asunto principal).

Por ejemplo, para la etiqueta *casual-shoe*, la segunda imagen no es una buena candidata para entrenamiento.

![Imágenes ilustrativas para ejemplificar las directrices de formación](/help/assets/assets/do-not-localize/distraction.png)

**Complejidad:** Si una imagen cumple los requisitos para más de una etiqueta, agregue todas las etiquetas aplicables antes de incluir la imagen para formación. Por ejemplo, para etiquetas, como `raincoat` y `model-side-view`, agregue ambas etiquetas en el recurso que cumple los requisitos antes de incluirlo para formación.

![Imágenes ilustrativas para ejemplificar las directrices de formación](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>La capacidad del servicio de contenido inteligente para aprender sobre sus etiquetas y aplicarlas a otras imágenes depende de la calidad de las imágenes que utilice para la formación. Para obtener los mejores resultados, Adobe recomienda utilizar imágenes visualmente similares para entrenar el servicio de para cada etiqueta.

### Formación periódica {#periodic-training}

Puede habilitar el Servicio de contenido inteligente para que se imparta formación periódicamente sobre los recursos y las etiquetas asociadas dentro de una carpeta. Abra la página [!UICONTROL Propiedades] de la carpeta de recursos, seleccione **[!UICONTROL Habilitar etiquetas inteligentes]** en la pestaña **[!UICONTROL Detalles]** y guarde los cambios.

![enable_smart_tags](assets/enable_smart_tags.png)

Una vez seleccionada esta opción para una carpeta, [!DNL Experience Manager] ejecuta un flujo de trabajo de formación automáticamente para entrenar el servicio de contenido inteligente en los recursos de la carpeta y sus etiquetas. De forma predeterminada, el flujo de trabajo de formación se ejecuta semanalmente a las 12:30 los sábados.

### Formación a la carta {#on-demand-training}

Puede entrenar el servicio de contenido inteligente siempre que sea necesario desde la consola Flujo de trabajo.

1. En la interfaz de [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página **[!UICONTROL Modelos de flujo de trabajo]**, seleccione el flujo de trabajo **[!UICONTROL Formación sobre etiquetas inteligentes]** y, a continuación, haga clic en **[!UICONTROL Iniciar flujo de trabajo]** en la barra de herramientas.
1. En el cuadro de diálogo **[!UICONTROL Ejecutar flujo de trabajo]**, vaya a la carpeta de carga útil que incluye los recursos etiquetados para entrenar el servicio.
1. Especifique un título para el flujo de trabajo y añada un comentario. A continuación, haga clic en **[!UICONTROL Ejecutar]**. Los recursos y las etiquetas se envían para su formación.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>Una vez que los recursos de una carpeta se procesan para formación, solo los modificados se procesan en ciclos de formación posteriores.

### Ver informes de formación {#viewing-training-reports}

Para comprobar si el servicio de contenido inteligente ha recibido formación sobre las etiquetas del conjunto de recursos de formación, consulte el informe de flujo de trabajo de formación desde la consola Informes.

1. En la interfaz de [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Informes]**.
1. En la página **[!UICONTROL Informes de recursos]**, haga clic en **[!UICONTROL Crear]**.
1. Seleccione el informe **[!UICONTROL Formación sobre etiquetas inteligentes]** y, a continuación, haga clic en **[!UICONTROL Siguiente]** en la barra de herramientas.
1. Especifique un título y una descripción para el informe. En **[!UICONTROL Programar informe]**, deje seleccionada la opción **[!UICONTROL Ahora]**. Si desea programar el informe para más adelante, seleccione **[!UICONTROL Más adelante]** e indique una fecha y una hora. A continuación, haga clic en **[!UICONTROL Crear]** en la barra de herramientas.
1. En la página **[!UICONTROL Informes de recursos]**, seleccione el informe que ha generado. Para ver el informe, haz clic en **[!UICONTROL Ver]** en la barra de herramientas.
1. Revise los detalles del informe.

   El informe muestra el estado de la formación de las etiquetas que ha entrenado. El color verde de la columna **[!UICONTROL Estado de formación]** indica que el servicio de contenido inteligente ha recibido formación para la etiqueta. El color amarillo indica que el servicio no está completamente entrenado para una etiqueta en particular. En este caso, agregue más imágenes con la etiqueta en concreto y ejecute el flujo de trabajo de formación para que el servicio se imparta completamente en la etiqueta.

   Si no ve las etiquetas en este informe, ejecute de nuevo el flujo de trabajo de formación para estas etiquetas.

1. Para descargar el informe, selecciónelo en la lista y haga clic en **[!UICONTROL Descargar]** en la barra de herramientas. El informe se descarga como una hoja de cálculo de Microsoft Excel.

## Limitaciones {#limitations}

* Las etiquetas inteligentes mejoradas se basan en modelos de aprendizaje de imágenes y sus etiquetas. Estos modelos no siempre son perfectos para identificar etiquetas. La versión actual del servicio de contenido inteligente tiene las siguientes limitaciones:

   * Incapacidad para reconocer diferencias sutiles en las imágenes. Por ejemplo, camisetas ajustadas delgadas versus regulares.
   * Incapacidad para identificar etiquetas en función de patrones o partes diminutos de una imagen. Por ejemplo, logotipos en camisetas.
   * El etiquetado es compatible con las configuraciones regionales que admiten [!DNL Experience Manager].

* Para buscar recursos con etiquetas inteligentes (regulares o mejoradas), use el Omnisearch [!DNL Assets] (búsqueda de texto completo). No hay ningún predicado de búsqueda independiente para las etiquetas inteligentes.

>[!MORELIKETHIS]
>
>* [Información general y cómo entrenar etiquetas inteligentes](enhanced-smart-tags.md)
>* [Solución de problemas de etiquetas inteligentes para credenciales de OAuth](config-oauth.md)
>* [Tutorial de vídeo sobre etiquetas inteligentes](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)
