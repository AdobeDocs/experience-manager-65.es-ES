---
title: Activos relacionados
description: Aprenda a relacionar recursos digitales que comparten algunos atributos comunes. También cree relaciones derivadas de origen entre recursos digitales.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Activos relacionados {#related-assets}

[!DNL Adobe Experience Manager Assets] permite relacionar recursos manualmente en función de las necesidades de la organización mediante la función de recursos relacionados. Por ejemplo, puede relacionar un archivo de licencia con un recurso o una imagen/vídeo en un tema similar. Puede relacionar recursos que comparten determinados atributos comunes. También puede utilizar la función para crear relaciones de origen/derivadas entre recursos. Por ejemplo, si tiene un archivo PDF que se genera a partir de un archivo INDD, puede relacionar el archivo PDF con su archivo INDD de origen.

Con esta función, tiene la flexibilidad de compartir un archivo PDF de baja resolución o un archivo JPG con proveedores o agencias y de hacer que el archivo INDD de alta resolución solo esté disponible bajo petición.

>[!NOTE] Solo los usuarios con permisos de edición de recursos pueden relacionar y desrelacionar los recursos.
>

## Relate assets {#relating-assets}

1. En la interfaz de Experience Manager, abra la página **[!UICONTROL Propiedades]** de un recurso que desee relacionar.

   ![abrir la página Propiedades de un recurso para relacionarlo](assets/asset-properties-relate-assets.png)

   *Figura: página[!DNL Assets]Propiedadespara relacionar recursos.*

   Como alternativa, seleccione el recurso en la vista de lista.

   ![chlimage_1-273](assets/chlimage_1-273.png)

   También puede seleccionar el recurso de una colección.

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. Para relacionar otro recurso con el recurso seleccionado, toque o haga clic en el icono **[!UICONTROL Relacionar]** de la barra de herramientas.

   ![chlimage_1-275](assets/chlimage_1-275.png)

1. Realice una de las acciones siguientes:

   * Para relacionar el archivo de origen del recurso, seleccione **[!UICONTROL Origen]** en la lista.
   * Para relacionar un archivo derivado, seleccione **[!UICONTROL Derivado]** de la lista.
   * Para crear una relación bidireccional entre los recursos, seleccione **[!UICONTROL Otros]** en la lista.
   ![chlimage_1-276](assets/chlimage_1-276.png)

1. En la pantalla **[!UICONTROL Seleccionar recurso]** , navegue hasta la ubicación del recurso que desee relacionar y selecciónelo.

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. Toque o haga clic en el icono **[!UICONTROL Confirmar]** .
1. Toque o haga clic en **[!UICONTROL Aceptar]** para cerrar el cuadro de diálogo. Según la relación que elija en el paso 3, el recurso relacionado se muestra en una categoría adecuada en la sección **[!UICONTROL Relacionado]** . Por ejemplo, si el recurso relacionado es el archivo de origen del recurso actual, aparece en **[!UICONTROL Origen]**.

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. Para desrelacionar un recurso, toque o haga clic en **[!UICONTROL Desrelacionar]** en la barra de herramientas.

   ![chlimage_1-279](assets/chlimage_1-279.png)

1. Seleccione los recursos que desea desrelacionar en el cuadro de diálogo **[!UICONTROL Eliminar relaciones]** y toque o haga clic en **[!UICONTROL Desrelacionar]**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. Haga clic o toque **[!UICONTROL Aceptar]** para cerrar el cuadro de diálogo. Los recursos para los que se han eliminado relaciones se eliminan de la lista de recursos relacionados en la sección **[!UICONTROL Relacionado]** .

## Traducción de recursos relacionados {#translating-related-assets}

La creación de relaciones de origen y derivadas entre recursos mediante la función Recursos relacionados también resulta útil en los flujos de trabajo de traducción. Cuando se ejecuta un flujo de trabajo de traducción en un recurso derivado, obtiene automáticamente cualquier recurso al que hace referencia el archivo de origen y lo incluye para su traducción. [!DNL Experience Manager Assets] De este modo, el recurso al que hace referencia el recurso de origen se traduce junto con el recurso de origen y los recursos derivados. Por ejemplo, imaginemos un escenario en el que la copia en inglés incluye un recurso derivado y su archivo de origen como se muestra.

![chlimage_1-281](assets/chlimage_1-281.png)

Si el archivo de origen está relacionado con otro recurso, [!DNL Experience Manager Assets] recopila el recurso al que se hace referencia y lo incluye para su traducción.

![la página Propiedades del recurso muestra el archivo de origen del recurso relacionado para incluirlo en la traducción](assets/asset-properties-source-asset.png)

*Figura: Recurso de origen de los recursos relacionados que se van a incluir para su traducción.*

1. Traduzca los recursos de la carpeta de origen a un idioma de destinatario siguiendo los pasos de [Creación de un nuevo proyecto](translation-projects.md#create-a-new-translation-project)de traducción. Por ejemplo, en este caso, traduzca sus recursos al francés.

1. En la página [!UICONTROL Proyectos] , abra la carpeta de traducción.

   ![chlimage_1-283](assets/chlimage_1-283.png)

1. Toque o haga clic en el mosaico del proyecto para abrir la página de detalles.

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. Toque o haga clic en las elipses debajo de la tarjeta Trabajo de traducción para vista del estado de la traducción.

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. Seleccione el recurso y, a continuación, toque o haga clic en **[!UICONTROL Mostrar en recursos]** en la barra de herramientas para vista del estado de traducción del recurso.

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. Para comprobar si los recursos relacionados con el origen se han traducido, toque o haga clic en el recurso de origen.

   ![chlimage_1-287](assets/chlimage_1-287.png)

1. Seleccione el recurso relacionado con el origen y, a continuación, toque o haga clic en **[!UICONTROL Mostrar en recursos]**. Se muestra el recurso relacionado traducido.

   ![chlimage_1-288](assets/chlimage_1-288.png)
