---
title: Assets Insights
description: Descubra cómo la función Assets Insights le permite rastrear las clasificaciones de los usuarios y las estadísticas de uso de las imágenes que se utilizan en sitios web de terceros, campañas de marketing y soluciones creativas de Adobe.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 0130ac40-a72b-4caf-a10f-3c7d76eaa1e6
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 8%

---

# Assets Insights {#asset-insights}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/assets-insights.html?lang=en) |
| AEM 6.5 | Este artículo |
| AEM 6.4 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/touch-ui-configuring-asset-insights.html?lang=en) |

La función Assets Insights le permite realizar un seguimiento de las clasificaciones de los usuarios y las estadísticas de uso de las imágenes que se utilizan en sitios web de terceros, campañas de marketing y soluciones creativas de Adobe. Ayuda a obtener perspectivas sobre su rendimiento y popularidad.

[!DNL Assets] Insights captura los detalles de actividad del usuario, como el número de veces que se clasifica, hace clic en una imagen y las impresiones (el número de veces que se carga una imagen en el sitio web). Asigna puntuaciones a las imágenes en función de estas estadísticas. Puede utilizar las puntuaciones y las estadísticas de rendimiento para seleccionar imágenes populares para incluirlas en catálogos, campañas de marketing, etc. Incluso puede formular políticas de archivado y renovación de licencias basadas en estas estadísticas.

Para [!DNL Assets] Perspectivas para capturar estadísticas de uso de imágenes de un sitio web, debe incluir el código incrustado de la imagen en el código del sitio web.

Para permitir que Assets Insights muestre las estadísticas de uso de los recursos, configure primero la función para recuperar los datos de informes de Adobe Analytics. Para obtener más información, consulte [Configurar perspectivas de recursos](/help/assets/configure-asset-insights.md). Para utilizar esta función en una instalación on-premise, compre [!DNL Adobe Analytics] licencia por separado. Clientes en [!DNL Managed Services] recibir [!DNL Analytics] licencia incluida en [!DNL Experience Manager]. Consulte [Descripción del producto de Managed Services](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Las perspectivas solo son compatibles y se proporcionan para las imágenes.

## Visualización de estadísticas de una imagen {#viewing-statistics-for-an-image}

Puede ver las puntuaciones de Assets Insights desde la página de metadatos.

1. Desde el [!DNL Assets] interfaz de usuario (IU), seleccione la imagen y haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas.
1. En la página Propiedades, haga clic en **[!UICONTROL Insights]** pestaña.
1. Revise los detalles de uso del recurso en la **[!UICONTROL Insights]** pestaña. El **[!UICONTROL Puntuación]** describe el uso total de recursos y las puntuaciones de rendimiento de un recurso

   La puntuación de uso describe el número de veces que el recurso se utiliza en varias soluciones.

   El **[!UICONTROL Impresiones]** la puntuación es el número de veces que el recurso se carga en el sitio web. El número mostrado debajo de **[!UICONTROL Clics]** es el número de veces que se hace clic en el recurso.

1. Revise la **[!UICONTROL Estadísticas de uso]** para saber de qué entidades formaba parte el recurso y qué soluciones creativas lo utilizaron recientemente. Cuanto mayor sea el uso, más buenas serán las probabilidades de que el recurso sea popular entre los usuarios. Los datos de uso se muestran bajo los siguientes encabezados:

   * **Recurso**: el número de veces que el recurso formaba parte de una colección o de un recurso compuesto
   * **Web y dispositivos móviles**: El número de veces que el recurso formaba parte de sitios web y aplicaciones
   * **Social**: el número de veces que se utilizó el recurso en soluciones como Adobe Social y Adobe Campaign
   * **Correo electrónico**: El número de veces que el recurso se utilizó en campañas de correo electrónico

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Debido a que la función de perspectivas de recursos generalmente obtiene los datos de las soluciones de Adobe Analytics de forma periódica, es posible que la sección Soluciones no muestre los datos más recientes. El período de tiempo para el que se muestran los datos depende de la programación de la operación de recuperación que ejecuta Assets Insights para recuperar datos de Analytics.

1. Para ver las estadísticas de rendimiento del recurso gráficamente durante un período de tiempo, seleccione el período en la sección **[!UICONTROL Estadísticas de rendimiento]**. Los detalles, incluidos los clics y las impresiones, se muestran como líneas de tendencia de un gráfico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >A diferencia de los datos de la sección Soluciones, la sección Estadísticas de rendimiento muestra los datos más recientes.

1. Para obtener el código incrustado del recurso que incluye en los sitios web para obtener datos de rendimiento, haga clic en **[!UICONTROL Obtener código incrustado]** debajo de la miniatura del recurso. Para obtener más información sobre cómo incluir el código incrustado en páginas web de terceros, consulte [Uso del rastreador de páginas y el código incrustado en páginas web](/help/assets/use-page-tracker.md).

   ![chlimage_1-98](assets/chlimage_1-303.png)

## Visualización de estadísticas acumuladas de imágenes {#viewing-aggregate-statistics-for-images}

Puede ver las puntuaciones de todos los recursos de una carpeta simultáneamente mediante la **[!UICONTROL Vista de la información]**.

1. En el [!DNL Assets] interfaz de usuario, vaya a la carpeta que contiene los recursos para los que desea ver información.
1. Haga clic en Diseño en la barra de herramientas y, a continuación, elija **[!UICONTROL Vista de perspectivas]**.
1. La página muestra las puntuaciones de uso de los recursos. Compare las clasificaciones de los distintos recursos y obtenga información.

## Programar trabajo en segundo plano {#scheduling-background-job}

Assets Insights recupera datos de uso de recursos de los grupos de informes de Adobe Analytics de forma periódica. De forma predeterminada, Assets Insights ejecuta un trabajo en segundo plano cada 24 horas a las 2 a. m. para recuperar los datos. Sin embargo, puede modificar tanto la frecuencia como el tiempo configurando la variable **[!UICONTROL Trabajo de sincronización del informe de rendimiento del recurso DAM de Adobe CQ]** desde la consola web.

1. Haga clic en [!DNL Experience Manager] y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
1. Abra el **[!UICONTROL Trabajo de sincronización del informe de rendimiento del recurso DAM de Adobe CQ]** configuración del servicio.

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. Especifique la frecuencia del programador deseada y la hora de inicio del trabajo en la expresión del programador de propiedades. Guarde los cambios.
