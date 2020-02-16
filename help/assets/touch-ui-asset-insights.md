---
title: Perspectivas de recursos
description: Descubra cómo la función de perspectivas de recursos le permite realizar un seguimiento de las clasificaciones de usuarios y las estadísticas de uso de las imágenes que se utilizan en sitios web de terceros, campañas de marketing y soluciones creativas de Adobe.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Perspectivas de recursos {#asset-insights}

La función de perspectivas de recursos le permite realizar un seguimiento de las clasificaciones de usuarios y las estadísticas de uso de las imágenes que se utilizan en sitios web de terceros, campañas de marketing y soluciones creativas de Adobe. Ayuda a obtener perspectivas sobre su rendimiento y popularidad.

Assets Insights captura los detalles de la actividad del usuario, como el número de veces que se califica, hace clic e imprime una imagen (el número de veces que se carga una imagen en el sitio web). Asigna puntuaciones a las imágenes en función de estas estadísticas. Puede utilizar las estadísticas de rendimiento y puntuaciones para seleccionar imágenes populares para incluirlas en catálogos, campañas de marketing, etc. Puede incluso formular políticas de archivado y renovación de licencias basadas en estas estadísticas.

Para que Assets Insights capture estadísticas de uso de imágenes de un sitio web, debe incluir el código incrustado de la imagen en el código del sitio web.

Para permitir que Asset Insights muestre las estadísticas de uso de los recursos, primero configure la función para recuperar datos de informes de Adobe Analytics. Para obtener más información, consulte [Configuración de perspectivas](/help/assets/touch-ui-configuring-asset-insights.md)de recursos.

>[!NOTE]
>
>Las perspectivas solo son compatibles y se proporcionan para imágenes.

## Ver estadísticas de una imagen {#viewing-statistics-for-an-image}

Puede ver las puntuaciones de perspectivas de recursos desde la página de metadatos.

1. En la interfaz de usuario de Recursos, seleccione la imagen y, a continuación, toque o haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas.
1. En la página Propiedades, toque o haga clic en la ficha **[!UICONTROL Perspectivas]** .
1. Revise los detalles de uso del recurso en la ficha **[!UICONTROL Perspectivas]** . La sección **[!UICONTROL Puntuación]** describe el uso total de recursos y las recuperaciones de rendimiento de un recurso.

   La puntuación de uso describe la cantidad de veces que se utiliza el recurso en varias soluciones.

   La puntuación de **[!UICONTROL impresiones]** es el número de veces que el recurso se carga en el sitio web. El número que se muestra en **[!UICONTROL Clics]** es el número de veces que se hace clic en el recurso.

1. Revise la sección Estadísticas **[!UICONTROL de]** uso para saber de qué entidades formaba parte el recurso y qué soluciones creativas lo utilizaron recientemente. Cuanto mayor sea el uso, mayores serán las posibilidades de que el recurso sea popular entre los usuarios. Los datos de uso se muestran en los siguientes encabezados:

   * **Recurso**: Número de veces que el recurso formaba parte de una colección o un recurso compuesto
   * **Web y móvil**: El número de veces que el recurso formaba parte de sitios web y aplicaciones
   * **Social**: El número de veces que se ha utilizado el recurso en soluciones como Adobe Social y Adobe Campaign
   * **Correo electrónico**: El número de veces que se utilizó el recurso en campañas de correo electrónico
   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Debido a que la función de perspectivas de recursos generalmente recopila los datos de soluciones de Adobe Analytics de forma periódica, es posible que la sección Soluciones no muestre los datos más recientes. El período de tiempo durante el cual se muestran los datos depende de la programación de la operación de recuperación que se ejecuta Asset Insights para recuperar datos de Analytics.

1. Para ver las estadísticas de rendimiento del activo gráficamente durante un período de tiempo, seleccione el período en la sección Estadísticas **[!UICONTROL de]** rendimiento. Los detalles, incluidos los clics y las impresiones, se muestran como líneas de tendencia de un gráfico.

   ![climage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >A diferencia de los datos de la sección Soluciones, la sección Estadísticas de rendimiento muestra los datos más recientes.

1. Para obtener el código incrustado del recurso que incluye en los sitios web con el fin de obtener datos de rendimiento, toque o haga clic en **[!UICONTROL Obtener código]** incrustado debajo de la miniatura del recurso. Para obtener más información sobre cómo incluir el código incrustado en páginas web de terceros, consulte [Uso del rastreador de páginas y código incrustado en páginas](/help/assets/touch-ui-using-page-tracker.md)web.

   ![chlimage_1-98](assets/chlimage_1-303.png)

## Ver estadísticas agregadas de imágenes {#viewing-aggregate-statistics-for-images}

Puede ver las puntuaciones de todos los recursos de una carpeta simultáneamente mediante la Vista de **[!UICONTROL perspectivas]**.

1. En la interfaz de usuario de Recursos, desplácese a la carpeta que contiene los recursos para los que desea ver perspectivas.
1. Toque o haga clic en el icono Diseño de la barra de herramientas y, a continuación, elija **[!UICONTROL Vista]** de perspectivas.
1. La página muestra las puntuaciones de uso de los recursos. Compare las clasificaciones de los distintos recursos y obtenga perspectivas.

## Programar trabajo en segundo plano {#scheduling-background-job}

Asset Insights obtiene datos de uso de recursos de los grupos de informes de Adobe Analytics de forma periódica. De forma predeterminada, Asset Insights ejecuta un trabajo en segundo plano cada 24 horas a las 2 de la madrugada para recuperar datos. Sin embargo, puede modificar tanto la frecuencia como la hora configurando el servicio Trabajo **[!UICONTROL de sincronización de informes de rendimiento de recursos de]** Adobe CQ DAM desde la consola web.

1. Toque el logotipo de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > Consola **** web.
1. Abra la configuración del servicio Trabajo **[!UICONTROL de sincronización de informes de rendimiento de recursos DAM de]** Adobe CQ.

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. Especifique la frecuencia del programador que desee y la hora de inicio del trabajo en la expresión del programador de propiedades. Guarde los cambios.
