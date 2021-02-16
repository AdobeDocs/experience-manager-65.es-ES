---
title: Conjuntos de giros
description: Aprenda a trabajar con conjuntos de giros en Dynamic Media
uuid: 379a20a3-6a17-499a-b0f1-3a835b97aa7b
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 8e9b3815-2893-4e6b-ac41-77720b42d56b
docset: aem65
translation-type: tm+mt
source-git-commit: c3ae4447581d946554d792c68d31b47a6b67d5df
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 11%

---


# Conjuntos de giros{#spin-sets}

Un conjunto de giros simula el acto real de girar un objeto para examinarlo. Los conjuntos de giros permiten la vista de elementos desde cualquier ángulo, obteniendo los detalles visuales clave desde cualquier ángulo.

Un conjunto de giros simula una experiencia de visualización de 360 grados. Dynamic Media oferta conjuntos de giros de un solo eje en los que los visores pueden rotar un elemento. Además, los usuarios pueden aplicar zoom &quot;de forma libre&quot; y desplazarse por cualquiera de las vistas con unos pocos clics simples del ratón. De este modo, los usuarios pueden examinar un elemento más de cerca desde un punto de vista concreto.

Los conjuntos de giros se designan mediante una pancarta con la palabra **[!UICONTROL SPINSET.]** Además, si se publica el conjunto de giros, se muestra la fecha de publicación, indicada por el  **** Worldicon, junto con la fecha de la última modificación, que indica la  **** asignación de derechos.

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>Para obtener información sobre la interfaz de usuario de Assets, consulte [Administración de recursos](/help/assets/manage-assets.md).

## Inicio rápido: Conjuntos de giros {#quick-start-spin-sets}

Para ayudarle en el uso inicial de los conjuntos de giros, siga estos pasos:

1. [Cargue las imágenes para varias vistas.](#uploading-assets-for-spin-sets)

   Como mínimo, necesitará entre 8 y 12 tomas de un elemento para un conjunto de giros unidimensional y entre 16 y 24 para un conjunto de giros bidimensional. Las tomas deben realizarse a intervalos regulares para dar la impresión de que el elemento está rotando y volteando. Por ejemplo, si un conjunto de giros unidimensional incluye 12 tomas, gire el elemento 30 grados (360/12) para cada toma.

1. [Crear conjuntos de giros.](#creating-spin-sets)

   Para crear un conjunto de giros, seleccione **[!UICONTROL Crear > Conjunto de giros]** y, a continuación, asigne un nombre al conjunto, elija los recursos y elija el orden en que aparecen las imágenes.

   Consulte [Uso de selectores](/help/assets/working-with-selectors.md).

   >[!NOTE]
   >
   >También puede crear conjuntos de giros automáticamente mediante los [ajustes preestablecidos de conjuntos de lotes](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets). **Importante:Los conjuntos de** lotes son creados por IPS (Image Production System) como parte de la ingesta de recursos y solo están disponibles en el modo Dynamic Media - Scene7.

1. Configure [ajustes preestablecidos del visor de conjuntos de giros](/help/assets/managing-viewer-presets.md) según sea necesario.

   Los administradores pueden crear o modificar ajustes preestablecidos de visualizador de conjuntos de giros. Para ver el conjunto de giros con un ajuste preestablecido de visualizador, seleccione el conjunto de giros y, en el menú desplegable del carril izquierdo, seleccione **Visualizadores**.

   Consulte **[!UICONTROL Herramientas > Recursos > Ajustes preestablecidos de visor]** para crear o editar ajustes preestablecidos de visor.

   Consulte [Añadir y editar ajustes preestablecidos de visor.](/help/assets/managing-viewer-presets.md)

1. [Visualización de conjuntos](#viewing-spin-sets) de giros.

   Puede vista y acceder a los conjuntos creados mediante ajustes preestablecidos de conjunto de lotes de tres formas diferentes. (Los conjuntos creados con ajustes preestablecidos de conjunto de lotes, no *a1/> aparecen en la interfaz de usuario).*

1. [Conjuntos de giros de previsualización.](/help/assets/previewing-assets.md)

   Seleccione el conjunto de giros y puede previsualización. Girar el conjunto de giros. Puede elegir diferentes visores en el menú **[!UICONTROL Visores]**, disponible en el menú desplegable del carril izquierdo.

1. [Publicar conjuntos de giros.](/help/assets/publishing-dynamicmedia-assets.md)

   Al publicar un conjunto de giros, se activa la URL y la cadena Incrustar. Además, debe [publicar el ajuste preestablecido de visor](/help/assets/managing-viewer-presets.md).

1. [Vincule las direcciones URL a la ](/help/assets/linking-urls-to-yourwebapplication.md) aplicación web o  [incruste el visor](/help/assets/embed-code.md) de vídeo o de imágenes.

   AEM Assets crea llamadas mediante URL para conjuntos de giros y los activa después de publicar los conjuntos de giros. Puede copiar estas direcciones URL cuando previsualización recursos. Como alternativa, puede incrustarlos en su sitio Web.

   Seleccione el conjunto de giros y, a continuación, en el menú desplegable del carril izquierdo, seleccione **[!UICONTROL Visualizadores.]**

   Consulte [Vinculación de un conjunto de giros a una página web](/help/assets/linking-urls-to-yourwebapplication.md) e [Incrustación del visualizador de imágenes o vídeos](/help/assets/embed-code.md).

Si lo necesita, puede [editar conjuntos de giros](#editing-spin-sets). Además, puede vista y modificación de [propiedades del conjunto de giros](/help/assets/manage-assets.md#editing-properties).

## Carga de recursos para conjuntos de giros {#uploading-assets-for-spin-sets}

Como mínimo, necesitará entre 8 y 12 tomas de un elemento para un conjunto de giros unidimensional y entre 16 y 24 para un conjunto de giros bidimensional. Las tomas deben realizarse a intervalos regulares para dar la impresión de que el elemento está rotando y volteando. Por ejemplo, si un conjunto de giros unidimensional incluye 12 tomas, gire el elemento 30 grados (360/12) para cada toma.

Puede cargar imágenes para los conjuntos de giros del mismo modo que [carga cualquier otro recurso en AEM Assets](/help/assets/manage-assets.md).

### Pautas para capturar imágenes para el conjunto de giros {#guidelines-for-shooting-spin-set-images}

A continuación se indican algunas prácticas recomendadas en relación con las imágenes de conjuntos de giros. En general, cuantas más imágenes haya en un conjunto de giros, mejor será el efecto de giro de la imagen. Sin embargo, incluir muchas imágenes en el conjunto también aumenta el tiempo que tardan las imágenes en cargarse. AEM recomienda estas directrices para la toma de imágenes para su uso en conjuntos de giros:

* Como mínimo, utilice entre 8 y 12 imágenes en un conjunto de giros unidimensional y entre 16 y 24 imágenes en un conjunto de giros bidimensional. Se necesita un mínimo de 8 imágenes para poder girar 360 grados. Los conjuntos de giros unidimensionales son más comunes ya que la creación de conjuntos de giros bidimensionales requiere mucho trabajo.
* Utilizar un formato sin pérdida; Se recomiendan TIFF y PNG.
* Enmascara todas las imágenes para que el elemento aparezca sobre un fondo blanco puro u otro de alto contraste. De forma opcional, agregue sombras.
* Asegúrese de que los detalles del producto están bien iluminados y enfocados.
* Tome imágenes de giro para ropa de moda con un maniquí o modelo. A menudo, el maniquí está completamente enmascarado (con un maniquí de vidrio) o se muestra en la imagen un maniquí o una forma de vestir estilizada. Puede crear un conjunto de giros en modelo definiendo el número de ángulos. Marque cada ángulo con cinta en el suelo para guiar al modelo hacia el paso y mirar en la dirección de cada toma.

## Creación de conjuntos de giros {#creating-spin-sets}

En esta sección se describe cómo crear conjuntos de giros en AEM.

>[!NOTE]
>
>También puede crear conjuntos de giros automáticamente mediante los [ajustes preestablecidos de conjuntos de lotes](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets). **Importante:Los conjuntos de** lotes son creados por IPS (Image Production System) como parte de la ingesta de recursos y solo están disponibles en el modo Dynamic Media - Scene7.
>
>Consulte &quot;Creación de ajustes preestablecidos de conjunto de lotes para generar automáticamente conjuntos de imágenes y conjuntos de giros&quot; en [Configuración de Dynamic Media - modo Scene7](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets).


>[!NOTE]
>
>El orden en que aparecen las imágenes en un conjunto de giros es importante. Asegúrese de ordenarlos para que el giro sea una vista suave de 360 grados.

**Creación de conjuntos de giros**

1. En Assets, navegue hasta el lugar donde desee crear un conjunto de giros, haga clic en **[!UICONTROL Crear]** y seleccione **[!UICONTROL Conjunto de giros.]** También puede crear el conjunto desde una carpeta que contenga los recursos. Aparece el Editor de conjuntos de giros.

   ![6_5_spinset-createpulldownmenu](assets/6_5_spinset-createpulldownmenu.png)

1. En el Editor de conjuntos de giros, en el campo **[!UICONTROL Título]**, introduzca un nombre para el conjunto de giros. El nombre aparece en la pancarta del conjunto de giros. De forma opcional, introduzca una descripción.

   ![6_5_spinset-spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >Al crear el conjunto de giros, puede cambiar la miniatura del conjunto de giros o permitir que AEM seleccione la miniatura automáticamente en función de los recursos del conjunto de giros. Para seleccionar una miniatura, haga clic en **[!UICONTROL Cambiar miniatura]** y seleccione cualquier imagen (puede navegar a otras carpetas para buscar imágenes también). Si ha seleccionado una miniatura y luego decide que AEM generar una del conjunto de giros, seleccione **[!UICONTROL Cambiar a miniatura automática.]**

1. Realice una de las siguientes acciones:

   * Cerca de la esquina superior izquierda de la página Editor de conjuntos de giros, toque **[!UICONTROL Añadir recurso.]**

   * Cerca del centro de la página Editor de conjuntos de giros, toque **[!UICONTROL Tocar para abrir el Selector de recursos.]**
   Toque para seleccionar los recursos que desea incluir en el conjunto de giros. Los recursos seleccionados tienen un icono de marca de verificación sobre ellos. Cuando termine, cerca de la esquina superior derecha de la página, toque **[!UICONTROL Seleccionar.]**

   Con el Selector de recursos, puede buscar recursos escribiendo una palabra clave y pulsando **[!UICONTROL Retorno]**. También puede aplicar filtros para restringir los resultados de búsqueda. Puede filtrar por ruta, colección, tipo de archivo y etiqueta. Seleccione el filtro y, a continuación, pulse el icono **[!UICONTROL Filtro]** en la barra de herramientas. Para cambiar la vista, pulse el icono Ver y seleccione **[!UICONTROL Vista de columna]**, **[!UICONTROL Vista de tarjeta]** o **[!UICONTROL Vista de lista.]**

   Consulte [Uso de selectores](/help/assets/working-with-selectors.md).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. Cuando se agregan recursos al conjunto, se añaden automáticamente en orden alfanumérico. Después de agregarlos, puede reordenar o ordenar manualmente los recursos.

   Si es necesario, arrastre el icono Reordenar de un recurso a la derecha del nombre de archivo del recurso para reordenar las imágenes hacia arriba o hacia abajo en la lista establecida.

   ![Reordenación del fotograma 11 en el conjunto de giros arrastrándolo a una nueva ubicación.](assets/6_5_spinset-reorderassets.png)

   Reordenación del fotograma 11 en el conjunto de giros arrastrándolo a una nueva ubicación.

1. (Opcional) Realice cualquiera de las siguientes acciones:

   * Para eliminar una imagen, seleccione la imagen y toque **[!UICONTROL Eliminar recurso.]**

   * Para aplicar un ajuste preestablecido, cerca de la esquina superior derecha de la página, toque **[!UICONTROL Ajuste preestablecido]** y, a continuación, seleccione un ajuste preestablecido para aplicar a todos los recursos a la vez.

1. Haga clic en **[!UICONTROL Guardar.]** El conjunto de giros recién creado aparece en la carpeta en la que lo creó.

## Visualización de conjuntos de giros {#viewing-spin-sets}

Puede crear conjuntos de giros en la interfaz de usuario o automáticamente mediante [ajustes preestablecidos de conjunto de lotes](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets). Sin embargo, los conjuntos creados con ajustes preestablecidos de conjunto de lotes, no *a1/> aparecen en la interfaz de usuario.* Puede acceder a los conjuntos creados mediante ajustes preestablecidos de conjunto de lotes de tres formas diferentes. (Estos métodos están disponibles aunque haya creado los conjuntos de giros en la interfaz de usuario).

>[!NOTE]
>
>También puede realizar vistas de conjuntos mediante la interfaz de usuario como se describe en [Edición de conjuntos de giros](#editing-spin-sets).

**A los conjuntos de giros de vista**

1. Al abrir las propiedades de un recurso individual. Las propiedades indican los conjuntos de los que el recurso seleccionado es miembro (en **[!UICONTROL Miembro de conjuntos]**). Haga clic en el nombre del conjunto para ver el conjunto completo.

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. Desde una imagen de miembro de cualquier conjunto. Seleccione el menú **[!UICONTROL Conjuntos]** para mostrar los conjuntos de los que es miembro el recurso.

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. Desde la búsqueda, puede seleccionar **[!UICONTROL Filtros]**, luego expandir **[!UICONTROL Dynamic Media]** y seleccionar **[!UICONTROL Conjuntos.]**

   La búsqueda devuelve conjuntos coincidentes creados manualmente en la interfaz de usuario o creados automáticamente mediante ajustes preestablecidos de conjunto por lotes. Para los conjuntos automatizados, la consulta de búsqueda se lleva a cabo utilizando criterios de búsqueda `Starts with` diferentes de AEM búsqueda que se basa en el uso de criterios de búsqueda `Contains`. La configuración del filtro en **[!UICONTROL Sets]** es la única manera de buscar conjuntos automatizados.

   ![chlimage_1-158](assets/chlimage_1-386.png)

## Edición de conjuntos de giros {#editing-spin-sets}

Puede realizar varias tareas de edición en los conjuntos de giros, como las siguientes:

* Añada imágenes al conjunto de giros.
* Vuelva a ordenar las imágenes en el conjunto de giros.
* Eliminar recursos del conjunto de giros.
* Aplicación de ajustes preestablecidos de visor.
* Elimine el conjunto de giros.

**Para editar un conjunto de giros**

1. Realice una de las siguientes acciones:

   * Pase el ratón sobre un recurso de conjunto de giros y, a continuación, toque **[!UICONTROL Editar]** (icono de lápiz).
   * Pase el ratón sobre un recurso de conjunto de giros, toque **[!UICONTROL Seleccionar]** (icono de marca de verificación) y, a continuación, toque **[!UICONTROL Editar]** en la barra de herramientas.

   * Toque en un recurso de conjunto de giros y, a continuación, toque **[!UICONTROL Editar]** (icono de lápiz) en la barra de herramientas.

1. Para editar el conjunto de giros, realice una de las siguientes acciones:

   * Para reordenar imágenes, arrastre una imagen a una nueva ubicación (seleccione el icono de reordenar para mover elementos).
   * Para ordenar los elementos en orden ascendente o descendente, haga clic en el encabezado de la columna.
   * Para agregar un recurso o actualizar un recurso existente, haga clic en **[!UICONTROL Añadir recurso.]** Vaya a un recurso, selecciónelo y, a continuación, toque  **** Seleccionar cerca de la esquina superior derecha.
Si elimina la imagen que AEM utiliza para la miniatura reemplazándola por otra imagen, el recurso original seguirá mostrándose.
   * Para eliminar un recurso, selecciónelo y toque o haga clic en **[!UICONTROL Eliminar recurso.]**
   * Para aplicar un ajuste preestablecido, toque o haga clic en el icono Ajuste preestablecido y seleccione un ajuste preestablecido.
   * Para eliminar un conjunto de giros completo, vaya al conjunto de giros, selecciónelo y seleccione **[!UICONTROL Eliminar]**

   >[!NOTE]
   >
   >Puede editar las imágenes de un conjunto de giros navegando hasta el conjunto, tocando **[!UICONTROL Establecer miembros]** en el carril izquierdo y, a continuación, tocando el icono Lápiz en un recurso individual para abrir la ventana de edición.

1. Haga clic en **[!UICONTROL Guardar]** cuando termine de editar.

## Vista previa de conjuntos de giros {#previewing-spin-sets}

Consulte [Vista previa de recursos](/help/assets/previewing-assets.md).

## Publicación de conjuntos de giros {#publishing-spin-sets}

Consulte [Publishing Assets](/help/assets/publishing-dynamicmedia-assets.md).
