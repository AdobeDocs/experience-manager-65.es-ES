---
title: Recursos relacionados
description: Obtenga información sobre cómo relacionar recursos digitales que comparten algunos atributos comunes. Cree también relaciones derivadas del origen entre recursos digitales.
contentOwner: AG
role: User
feature: Collaboration,Asset Management
exl-id: ddb69727-74a0-4a4d-a14e-7d3bb5ceea2a
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# Recursos relacionados {#related-assets}

[!DNL Adobe Experience Manager Assets] permite relacionar recursos manualmente según las necesidades de la organización mediante la función recursos relacionados. Por ejemplo, puede relacionar un archivo de licencia con un recurso o una imagen/vídeo sobre un tema similar. Puede relacionar recursos que comparten ciertos atributos comunes. También puede utilizar la función para crear relaciones de origen/derivadas entre recursos. Por ejemplo, si tiene un archivo PDF generado a partir de un archivo INDD, puede relacionar el archivo PDF con su archivo INDD de origen.

Al utilizar esta función, tiene la flexibilidad de compartir un archivo de PDF de baja resolución o un archivo de JPG con proveedores u agencias, y hacer que el archivo INDD de alta resolución solo esté disponible bajo petición.

>[!NOTE]
>
>Solo los usuarios con permisos de edición en los recursos pueden relacionarlos y desrelacionarlos.

## Relacionar recursos {#relating-assets}

1. Desde el [!DNL Experience Manager] interfaz, abra la **[!UICONTROL Propiedades]** página de un recurso que desea relacionar.

   ![abra la página Propiedades de un recurso para relacionarlo](assets/asset-properties-relate-assets.png)

   *Figura: [!DNL Assets] [!UICONTROL Propiedades] página para relacionar recursos.*

   También puede seleccionar el recurso en la vista de lista.

   ![chlimage_1-273](assets/chlimage_1-273.png)

   También puede seleccionar el recurso de una colección.

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. Para relacionar otro recurso con el recurso seleccionado, haga clic en **[!UICONTROL Relacionar]** ![relacionar recursos](assets/do-not-localize/link-relate.png) en la barra de herramientas.
1. Realice una de las siguientes acciones:

   * Para relacionar el archivo de origen del recurso, seleccione **[!UICONTROL Origen]** de la lista.
   * Para relacionar un archivo derivado, seleccione **[!UICONTROL Derivado]** de la lista.
   * Para crear una relación bidireccional entre los recursos, seleccione **[!UICONTROL Otros]** de la lista.

1. Desde el **[!UICONTROL Seleccionar recurso]** , vaya a la ubicación del recurso que desea relacionar y selecciónelo.

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. Clic **[!UICONTROL Confirmar]**.
1. Clic **[!UICONTROL OK]** para cerrar el cuadro de diálogo. Según la elección de la relación en el paso 3, el activo relacionado se enumera en una categoría adecuada del **[!UICONTROL Relacionado]** sección. Por ejemplo, si el recurso relacionado es el archivo de origen del recurso actual, aparece en **[!UICONTROL Origen]**.

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. Para anular la relación de un recurso, haga clic en **[!UICONTROL Desrelacionar]** ![recursos no relacionados](assets/do-not-localize/link-unrelate-icon.png) en la barra de herramientas.

1. Seleccione los recursos que desea anular la relación en **[!UICONTROL Quitar relaciones]** y haga clic en **[!UICONTROL Desrelacionar]**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. Clic **[!UICONTROL OK]** para cerrar el cuadro de diálogo. Los recursos para los que se han eliminado relaciones se eliminan de la lista de recursos relacionados en **[!UICONTROL Relacionado]** sección.

## Traducir recursos relacionados {#translating-related-assets}

La creación de relaciones de origen/derivadas entre recursos mediante la función de recursos relacionados también es útil en los flujos de trabajo de traducción. Cuando se ejecuta un flujo de trabajo de traducción en un recurso derivado, [!DNL Experience Manager Assets] recupera automáticamente cualquier recurso al que hace referencia el archivo de origen y lo incluye para su traducción. De este modo, el recurso al que hace referencia el recurso de origen se traduce junto con los recursos de origen y derivados. Por ejemplo, considere un escenario en el que la copia en inglés incluya un recurso derivado y su archivo de origen como se muestra.

![chlimage_1-281](assets/chlimage_1-281.png)

Si el archivo de origen está relacionado con otro recurso, [!DNL Experience Manager Assets] recupera el recurso al que se hace referencia y lo incluye para su traducción.

![La página Propiedades del recurso muestra el archivo de origen del recurso relacionado que se va a incluir en la traducción](assets/asset-properties-source-asset.png)

*Imagen: recurso de origen de los recursos relacionados que se van a incluir en la traducción.*

1. Traduzca los recursos de la carpeta de origen a un idioma de destino siguiendo los pasos indicados en [Creación de un proyecto de traducción](translation-projects.md#create-a-new-translation-project). Por ejemplo, en este caso, traduzca sus recursos al francés.

1. Desde el [!UICONTROL Proyectos] , abra la carpeta de traducción.

1. Haga clic en el mosaico del proyecto para abrir la página de detalles.

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. Haga clic en los puntos suspensivos debajo de la tarjeta Trabajo de traducción para ver el estado de la traducción.

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. Seleccione el recurso y haga clic en **[!UICONTROL Mostrar en Assets]** en la barra de herramientas para ver el estado de traducción del recurso.

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. Para comprobar si se han traducido los recursos relacionados con el origen, haga clic en el recurso de origen.

1. Seleccione el recurso relacionado con el origen y haga clic en **[!UICONTROL Mostrar en Assets]**. Se muestra el recurso relacionado traducido.
