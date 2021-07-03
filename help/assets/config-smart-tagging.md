---
title: Configuración del etiquetado de recursos mediante el servicio de contenido inteligente
description: Aprenda a configurar el etiquetado inteligente y el etiquetado inteligente mejorado en [!DNL Adobe Experience Manager], mediante el servicio de contenido inteligente.
contentOwner: AG
role: Admin
feature: Etiquetado,Etiquetas inteligentes
exl-id: 9f68804f-ba15-4f83-ab1b-c249424b1396
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '2173'
ht-degree: 25%

---

# Preparación [!DNL Assets] para el etiquetado inteligente {#configure-asset-tagging-using-the-smart-content-service}

Antes de empezar a etiquetar sus recursos mediante Smart Content Services, integre [!DNL Experience Manager Assets] con Adobe Developer Console para aprovechar el servicio inteligente de [!DNL Adobe Sensei]. Una vez configurado, entrene el servicio con algunas imágenes y una etiqueta.

Antes de utilizar el servicio de contenido inteligente, asegúrese de lo siguiente:

* [Integración con Adobe Developer Console](#integrate-adobe-io).
* [Capacite el servicio de contenido inteligente](#training-the-smart-content-service).

* Instale el último [[!DNL Experience Manager] Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html).

## Integración con Adobe Developer Console {#integrate-adobe-io}

Cuando se integra con Adobe Developer Console, el servidor [!DNL Experience Manager] autentica las credenciales del servicio con la puerta de enlace de Adobe Developer Console antes de reenviar la solicitud al servicio de contenido inteligente. Para integrarse, necesita una cuenta de Adobe ID con privilegios de administrador para la organización y una licencia del servicio de contenido inteligente comprada y habilitada para su organización.

Para configurar el servicio de contenido inteligente, siga estos pasos de nivel superior:

1. Para generar una clave pública, [Cree una configuración de servicio de contenido inteligente](#obtain-public-certificate) en [!DNL Experience Manager]. [Obtenga un certificado público para la integración de OAuth.](#obtain-public-certificate)

1. [Cree una integración en Adobe Developer Console y cargue la clave pública generada.](#create-adobe-i-o-integration)

1. [Configure la ](#configure-smart-content-service) implementación utilizando la clave de API y otras credenciales de Adobe Developer Console.

1. [Compruebe la configuración](#validate-the-configuration).

1. De forma opcional, [habilite el etiquetado automático en la carga de recursos](#enable-smart-tagging-in-the-update-asset-workflow-optional).

### Obtener un certificado público creando la configuración del servicio de contenido inteligente {#obtain-public-certificate}

El certificado público permite autenticar el perfil en Adobe Developer Console.

1. En la interfaz de usuario [!DNL Experience Manager], acceda a **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Legacy Cloud Services]**.

1. En la página Cloud Services, haga clic en **[!UICONTROL Configurar ahora]** en **[!UICONTROL Etiquetas inteligentes de recursos]**.

1. En el cuadro de diálogo **[!UICONTROL Crear configuración]**, especifique un título y un nombre para la configuración de etiquetas inteligentes. Haga clic en **[!UICONTROL Crear]**.

1. En el cuadro de diálogo **[!UICONTROL AEM servicio de contenido inteligente]**, utilice los siguientes valores:

   **[!UICONTROL URL de servicio]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Servidor de autorización]**: `https://ims-na1.adobelogin.com`

   Deje los demás campos en blanco por ahora (para proporcionar más adelante). Haga clic en **[!UICONTROL Aceptar]**.

   ![Cuadro de diálogo del servicio de contenido inteligente del Experience Manager para proporcionar la URL del servicio de contenido](assets/aem_scs.png)


   *Figura: Cuadro de diálogo del servicio de contenido inteligente para proporcionar la URL del servicio de contenido*

   >[!NOTE]
   >
   >La URL proporcionada como [!UICONTROL Service URL] no es accesible a través del explorador y genera un error 404. La configuración funciona correctamente con el mismo valor del parámetro [!UICONTROL Service URL]. Para el estado general del servicio y la programación de mantenimiento, consulte [https://status.adobe.com](https://status.adobe.com).

1. Haga clic en **[!UICONTROL Descargar certificado público para la integración de OAuth]** y descargue el archivo de certificado público `AEM-SmartTags.crt`.

   ![Una representación de la configuración creada para el servicio de etiquetado inteligente](assets/smart-tags-download-public-cert.png)


   *Figura: Configuración del servicio de etiquetado inteligente.*

#### Volver a configurar cuándo caduca un certificado {#certrenew}

Una vez caducado un certificado, ya no es de confianza. No puede renovar un certificado caducado. Para agregar un certificado, siga estos pasos.

1. Inicie sesión en la implementación [!DNL Experience Manager] como administrador. Haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.

1. Busque y haga clic en el usuario **[!UICONTROL dam-update-service]**. Haga clic en la pestaña **[!UICONTROL Almacén de claves]**.

1. Elimine el almacén de claves **[!UICONTROL similaritysearch]** y el certificado caducado. Haga clic en **[!UICONTROL Guardar y cerrar]**.

   ![Elimine la entrada de búsqueda por similitudes existente en el almacén de claves para agregar un certificado de seguridad](assets/smarttags_delete_similaritysearch_keystore.png)


   *Figura: Elimine la  `similaritysearch` entrada existente en el almacén de claves para agregar un certificado de seguridad.*

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Servicios de nube heredados]**. Haga clic en **[!UICONTROL Etiquetas inteligentes de recursos]** > **[!UICONTROL Mostrar configuración]** > **[!UICONTROL Configuraciones disponibles]**. Haga clic en la configuración requerida.

1. Para descargar un certificado público, haga clic en **[!UICONTROL Descargar certificado público para la integración de OAuth]**.

1. Acceda a [https://console.adobe.io](https://console.adobe.io) y vaya a los servicios de contenido inteligente existentes en la página **[!UICONTROL Integraciones]**. Cargue el nuevo certificado. Para obtener más información, consulte las instrucciones de [Creación de la integración de Adobe Developer Console](#create-adobe-i-o-integration).

### Creación de la integración de Adobe Developer Console {#create-adobe-i-o-integration}

Para utilizar las API del servicio de contenido inteligente, cree una integración en la consola del desarrollador de Adobe para obtener [!UICONTROL Clave de API] (generada en el campo [!UICONTROL CLIENT ID] de integración de la consola del desarrollador de Adobe), [!UICONTROL ID DE CUENTA TÉCNICA], [!UICONTROL ID de organización] y [!UICONTROL CLICLICLIENT SECRET] para [!UICONTROL Configuración del servicio de etiquetado inteligente de recursos] de la configuración de nube en [!DNL Experience Manager].

1. Acceda a [https://console.adobe.io](https://console.adobe.io/) en el explorador. Seleccione la cuenta adecuada y compruebe que la función de organización asociada sea administrador del sistema.

1. Cree un proyecto con el nombre que desee. Haga clic en **[!UICONTROL Añadir API]**.

1. En la página **[!UICONTROL Añadir una API]** , seleccione **[!UICONTROL Experience Cloud]** y **[!UICONTROL Contenido inteligente]**. Haga clic en **[!UICONTROL Siguiente]**. 

1. Seleccione **[!UICONTROL Cargar la clave pública]**. Proporcione el archivo de certificado descargado de [!DNL Experience Manager]. Se muestra un mensaje con las [!UICONTROL claves públicas cargadas correctamente]. Haga clic en **[!UICONTROL Siguiente]**. 

   [!UICONTROL La página de ] credenciales Crear una nueva cuenta de servicio (JWT) muestra la clave pública de la cuenta de servicio.

1. Haga clic en **[!UICONTROL Siguiente]**. 

1. En la página **[!UICONTROL Seleccionar perfiles de producto]**, seleccione **[!UICONTROL Servicios de contenido inteligente]**. Haga clic en **[!UICONTROL Guardar API configurada]**.

   La página muestra más información sobre la configuración. Mantenga esta página abierta para copiar y añadir estos valores en [!UICONTROL Configuración del servicio de etiquetado inteligente de recursos] de la configuración de nube en [!DNL Experience Manager] para configurar las etiquetas inteligentes.

   ![En la pestaña Información general, puede revisar la información proporcionada para la integración.](assets/integration_details.png)


   *Figura: Detalles sobre la integración en Adobe Developer Console*

### Configuración del servicio de contenido inteligente {#configure-smart-content-service}

Para configurar la integración, utilice los valores de los campos [!UICONTROL TECHNICAL ACCOUNT ID], [!UICONTROL ORGANIZATION ID], [!UICONTROL CLIENT SECRET] y [!UICONTROL CLIENT ID] de la integración de Adobe Developer Console. La creación de una configuración de nube de etiquetas inteligentes permite la autenticación de solicitudes de API desde la implementación [!DNL Experience Manager].

1. En [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Services heredados]** para abrir la consola [!UICONTROL Cloud Services].

1. En **[!UICONTROL Etiquetas inteligentes de recursos]**, abra la configuración creada anteriormente. En la página de configuración del servicio, haga clic en **[!UICONTROL Editar]**.

1. En el cuadro de diálogo **[!UICONTROL AEM Smart Content Service]**, utilice los valores predefinidos para los campos **[!UICONTROL URL de servicio]** y **[!UICONTROL Servidor de autorización]**.

1. Para los campos [!UICONTROL Api Key], [!UICONTROL Technical Account ID], [!UICONTROL Organization ID] y [!UICONTROL Client Secret], copie y utilice los siguientes valores generados en [Adobe Developer Console integration](#create-adobe-i-o-integration).

   | [!UICONTROL Configuración del servicio de etiquetado inteligente de recursos] | [!DNL Adobe Developer Console] campos de integración |
   |--- |--- |
   | [!UICONTROL Clave de API] | [!UICONTROL ID DE CLIENTE] |
   | [!UICONTROL Id. de cuenta técnica] | [!UICONTROL ID DE CUENTA TÉCNICA] |
   | [!UICONTROL Id. de organización] | [!UICONTROL ID. DE ORGANIZACIÓN] |
   | [!UICONTROL Secreto del cliente] | [!UICONTROL SECRETO DEL CLIENTE] |

### Validación de la configuración {#validate-the-configuration}

Una vez completada la configuración, puede utilizar un MBean JMX para validarla. Para validar, siga estos pasos.

1. Acceda a su servidor [!DNL Experience Manager] en `https://[aem_server]:[port]`.

1. Vaya a **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** para abrir la consola OSGi. Haga clic en **[!UICONTROL Principal] > [!UICONTROL JMX]**.

1. Haga clic `com.day.cq.dam.similaritysearch.internal.impl`. Abre **[!UICONTROL SimilaritySearch Tareas varias]**.

1. Haga clic `validateConfigs()`. En el cuadro de diálogo **[!UICONTROL Validar configuraciones]**, haga clic en **[!UICONTROL Invocar]**.

Los resultados de validación se muestran en el mismo cuadro de diálogo.

### Habilitar el etiquetado inteligente en el flujo de trabajo [!UICONTROL DAM Update Asset] (opcional) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. En [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.

1. En la página **[!UICONTROL Modelos de flujo de trabajo]**, seleccione el modelo de flujo de trabajo de **[!UICONTROL recursos de actualización de DAM]**.

1. Haga clic en **[!UICONTROL Editar]** en la barra de herramientas.

1. Expanda el panel lateral para mostrar los pasos. Arrastre el paso **[!UICONTROL Recurso de etiqueta inteligente]** que está disponible en la sección Flujo de trabajo de DAM y colóquelo después del paso **[!UICONTROL Miniaturas del proceso]**.

   ![Añada el paso del recurso de etiquetas inteligentes después del paso de miniaturas de proceso en el flujo de trabajo de recursos de actualización de DAM](assets/smart-tag-in-dam-update-asset-workflow.png)

   *Imagen: Añada el paso del recurso de etiquetas inteligentes después del paso de miniaturas de proceso en el flujo de trabajo de recursos de actualización de DAM*

1. Abra el paso en modo de edición. En **[!UICONTROL Configuración avanzada]**, compruebe que la opción **[!UICONTROL Avance del controlador]** está seleccionada.

   ![Configurar el flujo de trabajo de recursos de actualización de DAM y añadir el paso de etiquetas inteligentes](assets/smart-tag-step-properties-workflow1.png)


   *Figura: Configurar el flujo de trabajo de recursos de actualización de DAM y añadir el paso de etiquetas inteligentes*

1. En la pestaña **[!UICONTROL Argumentos]**, seleccione **[!UICONTROL Omitir errores]** si desea que el flujo de trabajo se complete aunque falle el paso de etiquetado automático.

   ![Configurar el flujo de trabajo de recursos de actualización de DAM para añadir el paso de etiquetas inteligentes y seleccionar el avance del controlador](assets/smart-tag-step-properties-workflow2.png)


   *Figura: Configurar el flujo de trabajo de recursos de actualización de DAM para añadir el paso de etiquetas inteligentes y seleccionar el avance del controlador*

   Para etiquetar recursos al cargarlos, independientemente de si el etiquetado inteligente está activado en las carpetas, seleccione **[!UICONTROL Omitir indicador de etiqueta inteligente]**.

   ![Configure el flujo de trabajo de recursos de actualización de DAM para añadir el paso de etiquetas inteligentes y seleccione Omitir el indicador de etiqueta inteligente](assets/smart-tag-step-properties-workflow3.png)


   *Figura: Configure el flujo de trabajo de recursos de actualización de DAM para añadir el paso de etiqueta inteligente y seleccione Omitir indicador de etiqueta inteligente.*

1. Haga clic en **[!UICONTROL Aceptar]** para cerrar el paso del proceso y, a continuación, guarde el flujo de trabajo.

## Formación del servicio de contenido inteligente {#training-the-smart-content-service}

Para que el servicio de contenido inteligente reconozca su taxonomía empresarial, ejecútelo en un conjunto de recursos que ya incluyen etiquetas que son relevantes para su negocio. Para etiquetar de forma eficaz las imágenes de marca, el servicio de contenido inteligente requiere que las imágenes de formación se ajusten a determinadas directrices. Después de la formación, el servicio puede aplicar la misma taxonomía en un conjunto de activos similar.

Puede entrenar el servicio varias veces para mejorar su capacidad de aplicar etiquetas relevantes. Después de cada ciclo de formación, ejecute un flujo de trabajo de etiquetado y compruebe si los recursos están etiquetados correctamente.

Puede entrenar el servicio de contenido inteligente de forma periódica o según sus necesidades.

>[!NOTE]
>
>El flujo de trabajo de formación solo se ejecuta en carpetas.

### Directrices para la formación {#guidelines-for-training}

Para obtener mejores resultados, las imágenes del conjunto de formación se ajustan a las siguientes directrices:

**Cantidad y tamaño:** Mínimo de 30 imágenes por etiqueta. Mínimo de 500 píxeles en el lado más largo.

**Coherencia**: Las imágenes utilizadas para una etiqueta específica son visualmente similares.

Por ejemplo, no es aconsejable etiquetar todas estas imágenes como `my-party` (para formación) porque no son visualmente similares.

![Imágenes ilustrativas para ejemplificar las directrices de formación](/help/assets/assets/do-not-localize/coherence.png)

**Cobertura**: Utilice una variedad suficiente en las imágenes de la formación. La idea es dar algunos ejemplos, pero razonablemente diversos, para que el Experience Manager aprenda a centrarse en las cosas correctas. Si está aplicando la misma etiqueta en imágenes visualmente diferentes, incluya al menos cinco ejemplos de cada tipo.

Por ejemplo, para la etiqueta *model-down-pose*, incluya más imágenes de capacitación similares a la imagen resaltada a continuación para que el servicio identifique imágenes similares con mayor precisión durante el etiquetado.

![Imágenes ilustrativas para ejemplificar las directrices de formación](/help/assets/assets/do-not-localize/coverage_1.png)

**Distracción/obstrucción**: El servicio forma mejor con imágenes que tienen menos distracción (fondos destacados, acompañamientos no relacionados, como objetos/personas con el tema principal).

Por ejemplo, para la etiqueta *casual-shoe*, la segunda imagen no es un buen candidato para la formación.

![Imágenes ilustrativas para ejemplificar las directrices de formación](/help/assets/assets/do-not-localize/distraction.png)

**Complejidad:** Si una imagen cumple los requisitos para más de una etiqueta, agregue todas las etiquetas aplicables antes de incluir la imagen para formación. Por ejemplo, para etiquetas como `raincoat` y `model-side-view`, agregue ambas etiquetas en el recurso que cumple los requisitos antes de incluirlo para formación.

![Imágenes ilustrativas para ejemplificar las directrices de formación](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>La capacidad del servicio de contenido inteligente para formarse sobre sus etiquetas y aplicarlas en otras imágenes depende de la calidad de las imágenes que utilice para la formación. Para obtener mejores resultados, Adobe recomienda utilizar imágenes visualmente similares para entrenar el servicio para cada etiqueta.

### Formación periódica {#periodic-training}

Puede permitir que el servicio de contenido inteligente imparta formación periódicamente sobre los recursos y las etiquetas asociadas de una carpeta. Abra la página [!UICONTROL Properties] de la carpeta de recursos, seleccione **[!UICONTROL Enable Smart Tags]** en la pestaña **[!UICONTROL Details]** y guarde los cambios.

![enable_smart_tags](assets/enable_smart_tags.png)

Una vez seleccionada esta opción para una carpeta, [!DNL Experience Manager] ejecuta un flujo de trabajo de formación automáticamente para entrenar el servicio de contenido inteligente en los recursos de la carpeta y sus etiquetas. De forma predeterminada, el flujo de trabajo de formación se ejecuta de forma semanal a las 12:30 AM de los sábados.

### Capacitación a pedido {#on-demand-training}

Puede entrenar el servicio de contenido inteligente siempre que sea necesario desde la consola Flujo de trabajo.

1. En la interfaz [!DNL Experience Manager], vaya a **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. En la página **[!UICONTROL Modelos de flujo de trabajo]**, seleccione el flujo de trabajo **[!UICONTROL Formación sobre etiquetas inteligentes]** y, a continuación, haga clic en **[!UICONTROL Iniciar flujo de trabajo]** en la barra de herramientas.
1. En el cuadro de diálogo **[!UICONTROL Ejecutar flujo de trabajo]**, vaya a la carpeta de carga útil que incluye los recursos etiquetados para entrenar el servicio.
1. Especifique un título para el flujo de trabajo y añada un comentario. A continuación, haga clic en **[!UICONTROL Ejecutar]**. Los recursos y las etiquetas se envían para formación.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>Una vez que los recursos de una carpeta se procesan para formación, solo los recursos modificados se procesan en ciclos de formación posteriores.

### Ver informes de capacitación {#viewing-training-reports}

Para comprobar si el servicio de contenido inteligente ha recibido formación sobre las etiquetas en el conjunto de recursos de formación, revise el informe del flujo de trabajo de formación desde la consola Informes .

1. En la interfaz [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Informes]**.
1. En la página **[!UICONTROL Informes de recursos]**, haga clic en **[!UICONTROL Crear]**.
1. Seleccione el informe **[!UICONTROL Formación sobre etiquetas inteligentes]** y, a continuación, haga clic en **[!UICONTROL Siguiente]** en la barra de herramientas.
1. Especifique un título y una descripción para el informe. En **[!UICONTROL Programar informe]**, deje seleccionada la opción **[!UICONTROL Ahora]**. Si desea programar el informe para más adelante, seleccione **[!UICONTROL Más adelante]** e indique una fecha y una hora. A continuación, haga clic en **[!UICONTROL Create]** en la barra de herramientas.
1. En la página **[!UICONTROL Informes de recursos]**, seleccione el informe que ha generado. Para ver el informe, haga clic en **[!UICONTROL Ver]** en la barra de herramientas.
1. Revise los detalles del informe.

   El informe muestra el estado de la formación de las etiquetas que ha entrenado. El color verde de la columna **[!UICONTROL Estado de formación]** indica que el servicio de contenido inteligente ha recibido formación para la etiqueta. El color amarillo indica que el servicio no está completamente entrenado para una etiqueta en particular. En este caso, agregue más imágenes con la etiqueta en concreto y ejecute el flujo de trabajo de formación para que el servicio se imparta completamente en la etiqueta.

   Si no ve las etiquetas en este informe, ejecute de nuevo el flujo de trabajo de formación para estas etiquetas.

1. Para descargar el informe, selecciónelo en la lista y haga clic en **[!UICONTROL Descargar]** en la barra de herramientas. El informe se descarga como hoja de cálculo de Microsoft Excel.

## Restricciones     {#limitations}

* Las etiquetas inteligentes mejoradas se basan en modelos de aprendizaje de imágenes y sus etiquetas. Estos modelos no siempre son perfectos para identificar etiquetas. La versión actual del servicio de contenido inteligente tiene las siguientes limitaciones:

   * Incapacidad para reconocer sutiles diferencias en imágenes. Por ejemplo, camisas delgadas contra las vestidas regulares.
   * Incapacidad para identificar etiquetas basadas en pequeños patrones o partes de una imagen. Por ejemplo, logotipos en camisetas.
   * El etiquetado es compatible con las configuraciones regionales compatibles con [!DNL Experience Manager]. Para obtener una lista de idiomas, consulte las [notas de la versión de los servicios de contenido inteligente](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html).

* Para buscar recursos con etiquetas inteligentes (normales o mejoradas), utilice la [!DNL Assets] Omnisearch (búsqueda de texto completo). No hay predicado de búsqueda independiente para las etiquetas inteligentes.

>[!MORELIKETHIS]
>
>* [Descripción general y formación de etiquetas inteligentes](enhanced-smart-tags.md)
* [Tutorial en vídeo sobre etiquetas inteligentes](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)

