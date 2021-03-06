---
title: Crear proyectos de traducción
description: Aprenda a crear proyectos de traducción en [!DNL Adobe Experience Manager].
contentOwner: AG
role: Architect, Admin
feature: Traducción
exl-id: 8990feca-cfda-4974-915e-27aa9d8f2ee1
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1875'
ht-degree: 17%

---

# Crear proyectos de traducción {#creating-translation-projects}

Para crear una copia de idioma, asigne un déclencheur a uno de los siguientes flujos de trabajo de copia de idioma disponibles en el carril Referencias de la interfaz de usuario [!DNL Experience Manager].

* **Crear y traducir**: En este flujo de trabajo, los recursos que se van a traducir se copian en la raíz del idioma al que se desea traducir. Además, según las opciones que elija, se crea un proyecto de traducción para los recursos en la consola Proyectos . Según la configuración, el proyecto de traducción se puede iniciar manualmente o se le puede permitir que se ejecute automáticamente en cuanto se cree el proyecto de traducción.

* **Actualizar copias** de idioma: Ejecute este flujo de trabajo para traducir un grupo adicional de recursos e incluirlo en una copia de idioma para una configuración regional concreta. En este caso, los recursos traducidos se añaden a la carpeta de destino que ya contiene recursos traducidos anteriormente.

>[!PREREQUISITES]
>
>* Los usuarios que crean proyectos de traducción son miembros del grupo `projects-administrators`.
>* El proveedor de servicios de traducción admite la traducción de binarios.


## Creación y traducción de flujos de trabajo {#create-and-translate-workflow}

Utilice el flujo de trabajo crear y traducir para generar copias de idioma para un idioma en particular por primera vez. El flujo de trabajo ofrece las siguientes opciones:

* Crear solo una estructura.
* Crear un nuevo proyecto de traducción.
* Añadir a un proyecto de traducción existente.

### Crear solo una estructura {#create-structure-only}

Utilice la opción **[!UICONTROL Crear solo estructura]** para diseñar una jerarquía de carpetas de destino dentro de la raíz del idioma de destino para que coincida con la jerarquía de la carpeta de origen dentro de la raíz del idioma de origen. En este caso, los recursos de origen se copian en la carpeta de destino. Sin embargo, no se genera ningún proyecto de traducción.

1. En la interfaz [!DNL Assets], seleccione la carpeta de origen para la que desea crear una estructura en la raíz del idioma de destino.

1. Abra el panel **[!UICONTROL Referencias]** y haga clic en **[!UICONTROL Textos en idiomas]** en **[!UICONTROL Textos]**.

   ![Copias de idioma](assets/translation-language-copies.png)

1. Haga clic en **[!UICONTROL Crear y traducir]**. En la lista **[!UICONTROL Idiomas de destino]**, seleccione el idioma para el que desea crear una estructura de carpetas.

1. En la lista **[!UICONTROL Proyecto]**, seleccione **[!UICONTROL Crear estructura únicamente]**.

1. Haga clic en **[!UICONTROL Crear]**. La nueva estructura para el idioma de destino se muestra en **[!UICONTROL Textos en idiomas]**.

   ![copias de idioma](assets/lang-copy2.png)

1. Haga clic en la estructura de la lista y, a continuación, haga clic en **[!UICONTROL Mostrar en recursos]** para desplazarse a la estructura de carpetas dentro del idioma de destino.

   ![mostrar en recursos](assets/reveal-in-assets.png)

### Crear un nuevo proyecto de traducción {#create-a-new-translation-project}

Si utiliza esta opción, los recursos que desea traducir se copian en la raíz del idioma al que desea traducir. Según las opciones que elija, se crea un proyecto de traducción para los recursos en la consola Proyectos . Según la configuración, el proyecto de traducción se puede iniciar manualmente o se ejecuta automáticamente en cuanto se crea el proyecto de traducción.

1. En la interfaz de usuario [!DNL Assets], seleccione la carpeta de origen para la que desea crear una copia de idioma.
1. Abra el panel **[!UICONTROL Referencias]** y haga clic en **[!UICONTROL Textos en idiomas]** en **[!UICONTROL Textos]**.

   ![imagen_1-63](assets/chlimage_1-63.png)

1. Haga clic en **[!UICONTROL Crear y traducir]** en la parte inferior.

1. En la lista **[!UICONTROL Idiomas de destino]**, seleccione los idiomas para los que desea crear una estructura de carpetas.

1. En la lista **[!UICONTROL Proyecto]**, seleccione **[!UICONTROL Crear un nuevo proyecto de traducción]**.

1. En el campo **[!UICONTROL Título del proyecto]**, introduzca un título.

1. Haga clic en **[!UICONTROL Crear]**. [!DNL Assets] de la carpeta de origen se copian en las carpetas de destino para las configuraciones regionales seleccionadas en el paso 4.

   ![copias de idioma](assets/lang-copy2.png)

1. Para desplazarse a la carpeta, seleccione la copia de idioma y haga clic en **[!UICONTROL Mostrar en Assets]**.

   ![mostrar en recursos](assets/reveal-in-assets.png)

1. Vaya a la consola Proyectos . La carpeta de traducción se copia en la consola Proyectos .

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. Abra la carpeta para ver el proyecto de traducción.

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. Haga clic en el proyecto para abrir la página de detalles.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Para ver el estado del trabajo de traducción, haga clic en los puntos suspensivos en la parte inferior del mosaico **[!UICONTROL Trabajo de traducción]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

   Para obtener más información sobre los estados del trabajo, consulte [Monitorización del estado de un trabajo de traducción](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Vaya a la interfaz de usuario [!DNL Assets] y abra la página [!UICONTROL Properties] de cada uno de los recursos traducidos para ver los metadatos traducidos.

   ![ver los metadatos traducidos en la página Propiedades del recurso](assets/translated-metadata-asset-properties.png)

   *Figura: Metadatos traducidos en la página de propiedades del recurso.*

   >[!NOTE]
   >
   >Esta función está disponible tanto para recursos como para carpetas. Cuando se selecciona un recurso en lugar de una carpeta, toda la jerarquía de carpetas hasta la raíz del idioma se copia para crear una copia de idioma para el recurso.

### Añadir a un proyecto de traducción existente {#add-to-existing-translation-project}

Si utiliza esta opción, el flujo de trabajo de traducción se ejecuta para los recursos que agregue a la carpeta de origen después de ejecutar un flujo de trabajo de traducción anterior. Solo los recursos recién añadidos se copian en la carpeta de destino que contiene recursos traducidos anteriormente. En este caso no se crea ningún proyecto de traducción nuevo.

1. En la interfaz de usuario de [!DNL Assets], vaya a la carpeta de origen que contiene recursos sin traducir.
1. Seleccione un recurso que desee traducir y abra el **[!UICONTROL panel Referencias]**. La sección **[!UICONTROL Textos en idiomas]** muestra el número de traducciones disponibles en ese momento.
1. Haga clic en **[!UICONTROL Textos en idiomas]** en **[!UICONTROL Textos]**. Se muestra una lista de las traducciones disponibles.
1. Haga clic en **[!UICONTROL Crear y traducir]** en la parte inferior.

1. En la lista **[!UICONTROL Idiomas de destino]**, seleccione los idiomas para los que desea crear una estructura de carpetas.

1. En la lista **[!UICONTROL Proyecto]**, seleccione **[!UICONTROL Agregar a proyecto de traducción]** existente para ejecutar el flujo de trabajo de traducción en la carpeta.

   >[!NOTE]
   >
   >Si elige la opción **[!UICONTROL Add to existing translation project]** , el proyecto de traducción se agregará a un proyecto preexistente solo si la configuración del proyecto coincide exactamente con la configuración del proyecto preexistente. De lo contrario, se crea un nuevo proyecto.

1. En la lista **[!UICONTROL Existing translation project]**, seleccione un proyecto para agregar el recurso para su traducción.

1. Haga clic en **[!UICONTROL Crear]**. Los recursos que se van a traducir se agregan a la carpeta de destino. La carpeta actualizada se muestra en la sección **[!UICONTROL Textos en idiomas]**.

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. Vaya a la consola Proyectos y abra el proyecto de traducción existente que ha agregado a.
1. Haga clic en el proyecto de traducción para ver la página de detalles del proyecto.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. Haga clic en los puntos suspensivos en la parte inferior del mosaico **Trabajo de traducción** para ver los recursos en el flujo de trabajo de traducción. En la lista de trabajos de traducción también se muestran las entradas para los metadatos y las etiquetas de los recursos. Estas entradas indican que los metadatos y las etiquetas de los recursos también se traducen.

   >[!NOTE]
   >
   >Si elimina la entrada de etiquetas o metadatos, no se traducirá ninguna etiqueta ni metadatos para ninguno de los recursos.

   >[!NOTE]
   >
   >Si el recurso que agrega al trabajo de traducción incluye subrecursos, selecciónelos y elimínelos para que la traducción continúe sin problemas.

1. Para iniciar la traducción de los recursos, haga clic en la flecha del mosaico **[!UICONTROL Trabajo de traducción]** y seleccione **[!UICONTROL Inicio]** en la lista.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   Un mensaje notifica el inicio del trabajo de traducción.

1. Para ver el estado del trabajo de traducción, haga clic en los puntos suspensivos en la parte inferior del mosaico **[!UICONTROL Trabajo de traducción]**.

   ![chlimage_1-83](assets/chlimage_1-83.png)

   Para obtener más información, consulte [Monitorización del estado de un trabajo de traducción](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Una vez finalizada la traducción, el estado cambia a Listo para revisión. Vaya a la interfaz de usuario [!DNL Assets] y abra la página Propiedades de cada uno de los recursos traducidos para ver los metadatos traducidos.

## Actualizar copias de idioma {#update-language-copies}

Ejecute este flujo de trabajo para traducir cualquier conjunto adicional de recursos e incluirlo en una copia de idioma para una configuración regional concreta. En este caso, los recursos traducidos se añaden a la carpeta de destino que ya contiene recursos traducidos anteriormente. Según la elección de opciones, se crea un proyecto de traducción o se actualiza un proyecto de traducción existente para los nuevos recursos. El flujo de trabajo Update language Copies incluye las siguientes opciones:

* Crear un nuevo proyecto de traducción
* Añadir a un proyecto de traducción existente

### Crear un nuevo proyecto de traducción {#create-a-new-translation-project-1}

Si utiliza esta opción, se crea un proyecto de traducción para el conjunto de recursos para el que desea actualizar una copia de idioma.

1. En la interfaz de usuario de [!DNL Assets], seleccione la carpeta de origen en la que añadió un recurso.
1. Abra el panel **[!UICONTROL Referencias]** y haga clic en **[!UICONTROL Textos en idiomas]** en **[!UICONTROL Textos]** para mostrar la lista de textos en diferentes idiomas.
1. Seleccione la casilla de verificación antes de **[!UICONTROL Textos en idiomas]** y, a continuación, seleccione la carpeta de destino correspondiente a la configuración regional adecuada.

   ![seleccionar copia de idioma](assets/lang-copy1.png)

1. Haga clic en **[!UICONTROL Actualizar copias de idioma]** en la parte inferior.

1. En la lista **[!UICONTROL Proyecto]**, elija **[!UICONTROL Crear un nuevo proyecto de traducción]**.

1. En el campo **[!UICONTROL Título del proyecto]**, introduzca un título.

1. Haga clic en **[!UICONTROL Start]**.
1. Vaya a la consola Proyectos . La carpeta de traducción se copia en la consola Proyectos .

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Abra la carpeta para ver el proyecto de traducción.

   ![chlimage_1-89](assets/chlimage_1-89.png)

1. Haga clic en el proyecto para abrir la página de detalles.

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Para iniciar la traducción de los recursos, haga clic en la flecha del mosaico **[!UICONTROL Trabajo de traducción]** y seleccione **[!UICONTROL Inicio]** en la lista.

   ![imagen_1-91](assets/chlimage_1-91.png)

   Un mensaje notifica el inicio del trabajo de traducción.

1. Para ver el estado del trabajo de traducción, haga clic en los puntos suspensivos en la parte inferior del mosaico **[!UICONTROL Trabajo de traducción]**.

   ![imagen_1-93](assets/chlimage_1-93.png)

   Para obtener más información sobre los estados del trabajo, consulte [Monitorización del estado de un trabajo de traducción](../sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Vaya a la interfaz de usuario [!DNL Assets] y abra la página Propiedades de cada uno de los recursos traducidos para ver los metadatos traducidos.

### Añadir a un proyecto de traducción existente {#add-to-existing-translation-project-1}

Si utiliza esta opción, el conjunto de recursos se agregará a un proyecto de traducción existente para actualizar la copia de idioma para la configuración regional que elija.

1. En la interfaz de usuario de [!DNL Assets], seleccione la carpeta de origen en la que añadió una carpeta de recursos.
1. Abra el panel **[!UICONTROL Referencias]** y haga clic en **[!UICONTROL Textos en idiomas]** en **[!UICONTROL Textos]** para mostrar la lista de textos en diferentes idiomas.

   ![imagen_1-94](assets/chlimage_1-94.png)

1. Seleccione la casilla de verificación que se encuentra delante de **[!UICONTROL Textos en idiomas]**, de esta forma, selecciona los textos disponibles en diferentes idiomas. Anule la selección de otros textos excepto el texto (textos) en el idioma correspondiente a las configuraciones regionales a las que desea traducir.

   ![seleccionar copia de idioma](assets/lang-copy1.png)

1. Haga clic en **[!UICONTROL Actualizar copias de idioma]** en la parte inferior.

1. En la lista **[!UICONTROL Proyecto]**, elija **[!UICONTROL Agregar al proyecto de traducción existente]**.

1. En la lista **[!UICONTROL Existing translation project]**, seleccione un proyecto para agregar el recurso para su traducción.

1. Haga clic en **[!UICONTROL Start]**.
1. Consulte los pasos 9-14 de [Agregar al proyecto de traducción existente](translation-projects.md#add-to-existing-translation-project) para completar el resto del procedimiento.

## Crear copias de idioma temporales {#creating-temporary-language-copies}

Cuando se ejecuta un flujo de trabajo de traducción para actualizar una copia de idioma con versiones editadas de los recursos originales, la copia de idioma existente se conserva hasta que se aprueban los recursos traducidos. [!DNL Adobe Experience Manager Assets] almacena los recursos recién traducidos en una ubicación temporal y actualiza la copia de idioma existente después de aprobar explícitamente los recursos. Si rechaza los recursos, la copia de idioma permanece sin cambios.

1. Haga clic en la carpeta raíz de origen en **[!UICONTROL Textos en idiomas]** para la que ya ha creado un texto en un idioma y, a continuación, haga clic en **[!UICONTROL Mostrar en recursos]** para abrir la carpeta en [!DNL Experience Manager Assets].

   ![imagen_1-99](assets/chlimage_1-99.png)

1. En la interfaz [!DNL Assets], seleccione un recurso que ya haya traducido y haga clic en **[!UICONTROL Editar]** en la barra de herramientas para abrir el recurso en modo de edición.
1. Edite el recurso y, a continuación, guarde los cambios.
1. Realice los pasos 2-14 del procedimiento [Add to existing translation project](#add-to-existing-translation-project) para actualizar la copia de idioma.
1. Haga clic en los puntos suspensivos en la parte inferior del mosaico **[!UICONTROL Trabajo de traducción]**. Desde la lista de recursos de la página **[!UICONTROL Trabajo de traducción]**, puede ver claramente la ubicación temporal en la que se almacena la versión traducida del recurso.

   ![chlimage_1-101](assets/chlimage_1-101.png)

1. Seleccione la casilla de verificación situada junto a **[!UICONTROL Title]**.
1. En la barra de herramientas, haga clic en **[!UICONTROL Aceptar traducción]** ![aceptar traducción](assets/do-not-localize/thumb-up.png) y, a continuación, haga clic en **[!UICONTROL Aceptar]** en el cuadro de diálogo para sobrescribir el recurso traducido en la carpeta de destino con la versión traducida del recurso editado.

   >[!NOTE]
   >
   >Para habilitar el flujo de trabajo de traducción para actualizar los recursos de destino, acepte el recurso y los metadatos.

   Haga clic en **[!UICONTROL Rechazar traducción]** ![rechazar traducción](assets/do-not-localize/thumb-down.png) para conservar la versión traducida originalmente del recurso en la raíz de configuración regional de destino y rechazar la versión editada.

1. Para ver los metadatos traducidos, vaya a la consola [!DNL Assets] y abra la página [!UICONTROL Properties] de cada uno de los recursos traducidos.

## Sugerencias y limitaciones {#tips-limitations}

* Si inicia un flujo de trabajo de traducción para recursos complejos, como archivos PDF y [!DNL Adobe InDesign] , sus subrecursos o representaciones (si hay) no se envían para su traducción.
* Si utiliza la traducción automática, los binarios de recursos no se traducen.
