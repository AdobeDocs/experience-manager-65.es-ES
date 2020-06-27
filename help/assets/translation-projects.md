---
title: Creación de proyectos de traducción
description: Aprenda a crear proyectos de traducción en [!DNL Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: a61e1e9ffb132b59c725b2078f09641a3c2a479a
workflow-type: tm+mt
source-wordcount: '1895'
ht-degree: 16%

---


# Creación de proyectos de traducción {#creating-translation-projects}

Para crear una copia de idioma, active una de las siguientes flujos de trabajo de copia de idioma disponibles en el carril Referencias de la interfaz de [!DNL Experience Manager] usuario.

* **Crear y traducir**: En este flujo de trabajo, los recursos que se van a traducir se copian en la raíz de idioma del idioma al que se desea traducir. Además, según las opciones que elija, se creará un proyecto de traducción para los recursos en la consola Proyectos. Según la configuración, el proyecto de traducción puede iniciarse manualmente o puede ejecutarse automáticamente en cuanto se cree el proyecto de traducción.

* **Actualizar copias** de idioma: Ejecute este flujo de trabajo para traducir un grupo adicional de recursos e incluirlo en una copia de idioma para una configuración regional concreta. En este caso, los recursos traducidos se agregan a la carpeta de destinatario que ya contiene recursos traducidos anteriormente.

>[!NOTE]
>
>Los binarios de recursos se traducen únicamente si el proveedor de servicio de traducción admite la traducción de binarios.

>[!NOTE]
>
>Si se inicia un flujo de trabajo de traducción para recursos complejos, como archivos PDF y [!DNL Adobe InDesign] archivos, sus subrecursos o representaciones (si existen) no se envían para su traducción.

## Crear y traducir flujos de trabajo {#create-and-translate-workflow}

El flujo de trabajo de creación y traducción se utiliza para generar copias de idiomas para un idioma determinado por primera vez. El flujo de trabajo ofrece las siguientes opciones:

* Crear solo una estructura.
* Crear un nuevo proyecto de traducción.
* Añadir a un proyecto de traducción existente.

### Crear solo una estructura {#create-structure-only}

Utilice la opción **[!UICONTROL Crear solo estructura]** para diseñar una jerarquía de carpetas de destino dentro de la raíz del idioma de destino para que coincida con la jerarquía de la carpeta de origen dentro de la raíz del idioma de origen. En este caso, los recursos de origen se copian en la carpeta de destino. Sin embargo, no se genera ningún proyecto de traducción.

1. En la [!DNL Assets] interfaz, seleccione la carpeta de origen para la que desea crear una estructura en la raíz del idioma del destinatario.
1. Open the **[!UICONTROL References]** pane and click **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]**.

   ![chlimage_1-57](assets/chlimage_1-57.png)

1. Haga clic en **[!UICONTROL Crear y traducir]** en la parte inferior.

   ![chlimage_1-58](assets/chlimage_1-58.png)

1. From the **[!UICONTROL Target Languages]** list, select the language for which you want to create a folder structure.

   ![chlimage_1-59](assets/chlimage_1-59.png)

1. En la lista **[!UICONTROL Proyecto]**, seleccione **[!UICONTROL Crear estructura únicamente]**.

   ![chlimage_1-60](assets/chlimage_1-60.png)

1. Haga clic en **[!UICONTROL Crear]**. La nueva estructura del idioma de destinatario se muestra en Copias **[!UICONTROL de idioma]**.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Haga clic en la estructura de la lista y, a continuación, haga clic en **[!UICONTROL Mostrar en recursos]** para desplazarse a la estructura de carpetas dentro del idioma del destinatario.

   ![chlimage_1-62](assets/chlimage_1-62.png)

### Crear un nuevo proyecto de traducción {#create-a-new-translation-project}

Si utiliza esta opción, los recursos que se van a traducir se copian en la raíz del idioma en el que desea traducir. Según las opciones que elija, se creará un proyecto de traducción para los recursos en la consola Proyectos. Según la configuración, el proyecto de traducción se puede iniciar manualmente o automáticamente en cuanto se cree el proyecto de traducción.

1. En la interfaz de usuario de Recursos, seleccione la carpeta de origen para la que desea crear una copia de idioma.
1. Open the **[!UICONTROL References]** pane and click **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

1. Haga clic en **[!UICONTROL Crear y traducir]** en la parte inferior.

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. En la lista **[!UICONTROL Idiomas de destino]**, seleccione los idiomas para los que desea crear una estructura de carpetas.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. En la lista **[!UICONTROL Proyecto]** , seleccione **[!UICONTROL Crear un nuevo proyecto]** de traducción.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. En el campo **[!UICONTROL Título del proyecto]**, introduzca un título.

   ![chlimage_1-67](assets/chlimage_1-67.png)

1. Haga clic en **[!UICONTROL Crear]**. Los recursos de la carpeta de origen se copian en las carpetas de destinatario para las configuraciones regionales seleccionadas en el paso 4.

   ![chlimage_1-68](assets/chlimage_1-68.png)

1. Para desplazarse a la carpeta, seleccione la copia de idioma y haga clic en **[!UICONTROL Mostrar en recursos]**.

   ![chlimage_1-69](assets/chlimage_1-69.png)

1. Vaya a la consola Proyectos. La carpeta de traducción se copia en la consola Proyectos.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. Abra la carpeta para vista del proyecto de traducción.

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. Haga clic en el proyecto para abrir la página de detalles.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Para vista del estado del trabajo de traducción, haga clic en los puntos suspensivos en la parte inferior del mosaico Trabajo **[!UICONTROL de]** traducción.

   ![chlimage_1-73](assets/chlimage_1-73.png)

   Para obtener más información sobre los estados de los trabajos, consulte [Supervisión del estado de un trabajo](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job)de traducción.

1. Vaya a la interfaz de usuario de Recursos y abra la página Propiedades de cada uno de los recursos traducidos para realizar la vista de los metadatos traducidos.

   ![vista de los metadatos traducidos en la página Propiedades del recurso](assets/translated-metadata-asset-properties.png)

   *Figura: Metadatos traducidos en la página de propiedades del recurso.*


   >[!NOTE]
   >
   >Esta función está disponible para recursos y carpetas. Cuando se selecciona un recurso en lugar de una carpeta, se copia toda la jerarquía de carpetas hasta la raíz del idioma para crear una copia de idioma para el recurso.

### Añadir a un proyecto de traducción existente {#add-to-existing-translation-project}

Si utiliza esta opción, el flujo de trabajo de traducción se ejecuta para los recursos que agregue a la carpeta de origen después de ejecutar un flujo de trabajo de traducción anterior. Solo los recursos recién añadidos se copian en la carpeta de destinatario que contiene los recursos traducidos anteriormente. En este caso no se crea ningún proyecto de traducción nuevo.

1. En la interfaz de usuario de Recursos, navegue a la carpeta de origen que contenga recursos sin traducir.
1. Seleccione un recurso que desee traducir y abra el **[!UICONTROL panel Referencias]**. La sección **[!UICONTROL Textos en idiomas]** muestra el número de traducciones disponibles en ese momento.
1. Click **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]**. Se muestra una lista de las traducciones disponibles.
1. Haga clic en **[!UICONTROL Crear y traducir]** en la parte inferior.

   ![chlimage_1-75](assets/chlimage_1-75.png)

1. En la lista **[!UICONTROL Idiomas de destino]**, seleccione los idiomas para los que desea crear una estructura de carpetas.

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. En la lista **[!UICONTROL Proyecto]**, seleccione **[!UICONTROL Agregar a proyecto de traducción]** existente para ejecutar el flujo de trabajo de traducción en la carpeta.

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >Si selecciona la opción **[!UICONTROL Añadir a proyecto]** de traducción existente, el proyecto de traducción se agrega a un proyecto preexistente solo si la configuración del proyecto coincide exactamente con la del proyecto preexistente. De lo contrario, se crea un nuevo proyecto.

1. En la lista de proyecto **[!UICONTROL de traducción]** existente, seleccione un proyecto para agregar el recurso a la traducción.

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. Haga clic en **[!UICONTROL Crear]**. Los recursos que se van a traducir se agregan a la carpeta de destino. La carpeta actualizada se muestra en la sección **[!UICONTROL Textos en idiomas]**.

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. Vaya a la consola Proyectos y abra el proyecto de traducción existente que ha agregado.
1. Haga clic en la vista del proyecto de traducción en la página de detalles del proyecto.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. Click the ellipsis at the bottom of the **Translation Job** tile to view the assets in the translation workflow. En la lista de trabajos de traducción también se muestran las entradas para los metadatos y las etiquetas de los recursos. Estas entradas indican que los metadatos y las etiquetas de los recursos también se traducen.

   >[!NOTE]
   >
   >Si elimina la entrada de etiquetas o metadatos, no se traducirá ninguna etiqueta o metadatos para ninguno de los recursos.

   >[!NOTE]
   >
   >Si utiliza Traducción automática, los binarios de recursos no se traducen.

   >[!NOTE]
   >
   >Si el recurso que agrega al trabajo de traducción incluye subrecursos, selecciónelos y elimínelos para que la traducción continúe sin problemas.

1. Para inicio de la traducción de los recursos, haga clic en la flecha del mosaico Trabajo **[!UICONTROL de]** traducción y seleccione **[!UICONTROL Inicio]** en la lista.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   Un mensaje notifica el inicio del trabajo de traducción.

   ![chlimage_1-82](assets/chlimage_1-82.png)

1. Para vista del estado del trabajo de traducción, haga clic en los puntos suspensivos en la parte inferior del mosaico Trabajo **[!UICONTROL de]** traducción.

   ![chlimage_1-83](assets/chlimage_1-83.png)

   Para obtener más información, consulte [Supervisión del estado de un trabajo](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job)de traducción.

1. Una vez finalizada la traducción, el estado cambia a Listo para revisar. Vaya a la interfaz de usuario de Recursos y abra la página Propiedades de cada uno de los recursos traducidos para realizar la vista de los metadatos traducidos.

## Actualizar copias de idioma {#update-language-copies}

Ejecute este flujo de trabajo para traducir cualquier conjunto adicional de recursos e incluirlo en una copia de idioma para una configuración regional concreta. En este caso, los recursos traducidos se agregan a la carpeta de destinatario que ya contiene recursos traducidos anteriormente. Según la elección de opciones, se crea un proyecto de traducción o se actualiza un proyecto de traducción existente para los nuevos recursos. El flujo de trabajo Actualizar copias de idioma incluye las siguientes opciones:

* Crear un nuevo proyecto de traducción
* Añadir a un proyecto de traducción existente

### Crear un nuevo proyecto de traducción {#create-a-new-translation-project-1}

Si utiliza esta opción, se crea un proyecto de traducción para el conjunto de recursos para los que desea actualizar una copia de idioma.

1. En la interfaz de usuario de Recursos, seleccione la carpeta de origen en la que ha agregado un recurso.
1. Open the **[!UICONTROL References]** pane, and click **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]** to display the list of language copies.
1. Seleccione la casilla de verificación antes de **[!UICONTROL Textos en idiomas]** y, a continuación, seleccione la carpeta de destino correspondiente a la configuración regional adecuada.

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. Haga clic en **[!UICONTROL Actualizar copias]** de idioma en la parte inferior.

   ![chlimage_1-85](assets/chlimage_1-85.png)

1. En la lista **[!UICONTROL Proyecto]** , elija **[!UICONTROL Crear un nuevo proyecto]** de traducción.

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. En el campo **[!UICONTROL Título del proyecto]**, introduzca un título.

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. Haga clic en **[!UICONTROL Inicio]**.
1. Vaya a la consola Proyectos. La carpeta de traducción se copia en la consola Proyectos.

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Abra la carpeta para vista del proyecto de traducción.

   ![chlimage_1-89](assets/chlimage_1-89.png)

1. Haga clic en el proyecto para abrir la página de detalles.

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Para inicio de la traducción de los recursos, haga clic en la flecha del mosaico Trabajo **[!UICONTROL de]** traducción y seleccione **[!UICONTROL Inicio]** en la lista.

   ![chlimage_1-91](assets/chlimage_1-91.png)

   Un mensaje notifica el inicio del trabajo de traducción.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Para vista del estado del trabajo de traducción, haga clic en los puntos suspensivos en la parte inferior del mosaico Trabajo **[!UICONTROL de]** traducción.

   ![chlimage_1-93](assets/chlimage_1-93.png)

   Para obtener más información sobre los estados de los trabajos, consulte [Supervisión del estado de un trabajo](../sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job)de traducción.

1. Vaya a la interfaz de usuario de Recursos y abra la página Propiedades de cada uno de los recursos traducidos para realizar la vista de los metadatos traducidos.

### Añadir a un proyecto de traducción existente {#add-to-existing-translation-project-1}

Si utiliza esta opción, el conjunto de recursos se agrega a un proyecto de traducción existente para actualizar la copia de idioma de la configuración regional que elija.

1. En la interfaz de usuario de Recursos, seleccione la carpeta de origen en la que ha agregado una carpeta de recursos.
1. Open the **[!UICONTROL References pane]**, and click **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]** to display the list of language copies.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Seleccione la casilla de verificación que se encuentra delante de **[!UICONTROL Textos en idiomas]**, de esta forma, selecciona los textos disponibles en diferentes idiomas. Anule la selección de otros textos excepto el texto (textos) en el idioma correspondiente a las configuraciones regionales a las que desea traducir.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Haga clic en **[!UICONTROL Actualizar copias]** de idioma en la parte inferior.

   ![chlimage_1-96](assets/chlimage_1-96.png)

1. En la lista **[!UICONTROL Proyecto]** , elija **[!UICONTROL Añadir a proyecto]** de traducción existente.

   ![chlimage_1-97](assets/chlimage_1-97.png)

1. En la lista de proyecto **[!UICONTROL de traducción]** existente, seleccione un proyecto para agregar el recurso a la traducción.

   ![chlimage_1-98](assets/chlimage_1-98.png)

1. Haga clic en **[!UICONTROL Inicio]**.
1. Véanse los pasos 9 a 14 de [Añadir al proyecto](translation-projects.md#add-to-existing-translation-project) de traducción existente para completar el resto del procedimiento.

## Crear copias temporales de idioma {#creating-temporary-language-copies}

Cuando se ejecuta un flujo de trabajo de traducción para actualizar una copia de idioma con versiones editadas de los recursos originales, la copia de idioma existente se conserva hasta que se aprueban los recursos traducidos. [!DNL Adobe Experience Manager Assets] almacena los recursos recién traducidos en una ubicación temporal y actualiza la copia de idioma existente después de aprobar explícitamente los recursos. Si rechaza los recursos, la copia de idioma permanece sin cambios.

1. Click the source root folder under **[!UICONTROL Language Copies]** for which you already created a language copy, and then click **[!UICONTROL Reveal in Assets]** to open the folder in [!DNL Experience Manager Assets].

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. En la [!DNL Assets] interfaz, seleccione un recurso que ya haya traducido y haga clic en **[!UICONTROL Editar]** en la barra de herramientas para abrir el recurso en modo de edición.
1. Edite el recurso y guarde los cambios.
1. Realice los pasos 2 a 14 del procedimiento de [Añadir al proyecto](#add-to-existing-translation-project) de traducción existente para actualizar la copia del idioma.
1. Haga clic en los puntos suspensivos en la parte inferior del mosaico Trabajo **[!UICONTROL de]** traducción. Desde la lista de recursos en la página Trabajo **[!UICONTROL de]** traducción, puede realizar una vista clara de la ubicación temporal en la que se almacena la versión traducida del recurso.

   ![chlimage_1-101](assets/chlimage_1-101.png)

1. Seleccione la casilla de verificación situada junto a **[!UICONTROL Título]**.
1. From the toolbar, click **[!UICONTROL Accept Translation]** and then click **[!UICONTROL Accept]** in the dialog to overwrite the translated asset in the target folder with the translated version of the edited asset.

   ![chlimage_1-102](assets/chlimage_1-102.png)

   >[!NOTE]
   >
   >Para habilitar el flujo de trabajo de traducción para actualizar los recursos de destino, acepte tanto el recurso como los metadatos.

   Haga clic en **[!UICONTROL Rechazar traducción]** para conservar la versión traducida originalmente del recurso en la raíz de configuración regional de destinatario y rechazar la versión editada.

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. Para vista de los metadatos traducidos, desplácese hasta la [!DNL Assets] consola y abra la página [!UICONTROL Propiedades] de cada uno de los recursos traducidos.

>[!MORELIKETHIS]
>
>* [Sugerencias para traducir metadatos](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/)de forma eficaz.

