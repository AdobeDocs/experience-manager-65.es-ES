---
title: Gestión de recursos compuestos con referencias y recursos de varias páginas en Experience Manager
description: Aprenda a crear referencias a recursos de AEM desde InDesign, Illustrator y Photoshop. Utilice la función Visor de páginas para ver páginas de subrecursos individuales de archivos de varias páginas, como archivos PDF, INDD, PPT, PPTX y AI.
contentOwner: AG
translation-type: tm+mt
source-git-commit: d15273e9308926ca4745fc1045e2da9fe8ed91d4

---


# Administrar recursos compuestos y de varias páginas {#managing-compound-assets}

Los recursos de Adobe Experience Manager (AEM) pueden identificar si un archivo cargado contiene referencias a recursos que ya existen en el repositorio. Esta función solo está disponible para los formatos de archivo admitidos. Si el recurso cargado contiene referencias a recursos de AEM, se crea un vínculo bidireccional entre los recursos cargados y los a los que se hace referencia.

Además de eliminar la redundancia, hacer referencia a los recursos de AEM en las aplicaciones de Adobe Creative Cloud mejora la colaboración y aumenta la eficiencia y la productividad de los usuarios.

Recursos AEM admite referencias bidireccionales. Los recursos a los que se hace referencia se encuentran en la página de detalles del recurso del archivo cargado. Además, puede ver los archivos de referencia de los recursos de AEM en la página de detalles de recursos del recurso al que se hace referencia.

Las referencias se resuelven en función de la ruta de acceso, el ID del documento y el ID de instancia de los recursos a los que se hace referencia.

## AEM Assets como referencias en Adobe Illustrator {#refai}

Puede hacer referencia a recursos de AEM existentes desde un archivo de Adobe Illustrator.

1. Con la aplicación [de escritorio de](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)AEM, monte el repositorio de AEM Assets como una unidad en el equipo local. En la unidad montada, navegue a la ubicación del recurso al que desee hacer referencia.
1. Arrastre el recurso desde la unidad montada al archivo de Illustrator.

1. Guarde el archivo de Illustrator en la unidad montada o [cárguelo](/help/assets/managing-assets-touch-ui.md#uploading-assets) en el repositorio de AEM.

1. Una vez finalizado el flujo de trabajo, vaya a la página de detalles del recurso. Las referencias a los recursos de AEM existentes se enumeran en **[!UICONTROL Dependencias]** en la columna **[!UICONTROL Referencias]** .

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Los recursos a los que se hace referencia y que aparecen en **[!UICONTROL Dependencias]** también pueden ser referenciados por otros archivos que no sean el actual. Para ver una lista de archivos de referencia para un recurso, haga clic en el recurso en la sección **[!UICONTROL Dependencias]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Haga clic en **[!UICONTROL Ver propiedades]** en la barra de herramientas. En la página [!UICONTROL Propiedades] , la lista de archivos que hacen referencia al recurso actual aparece en la columna **[!UICONTROL Referencias]** de la ficha **[!UICONTROL Básico]** .

   ![ver las referencias de Recursos de Experience Manager en la columna Referencias de los detalles del recurso](assets/asset-references.png)

   *Figura: Referencias de recursos en detalles de recursos*

## Adición de recursos de AEM como referencias en Adobe InDesign {#add-aem-assets-as-references-in-adobe-indesign}

Para hacer referencia a recursos de AEM desde un archivo de InDesign, arrastre los recursos de AEM al archivo de InDesign o exporte el archivo de InDesign como archivo ZIP.

Los recursos a los que se hace referencia ya existen en Recursos AEM. Puede extraer subrecursos [configurando el servidor](/help/assets/indesign.md)de InDesign. Los recursos incrustados en un archivo de InDesign se extraen como subrecursos.

>[!NOTE]
>
>Si se procesa como proxy el servidor de InDesign, la vista previa de los archivos de InDesign se incrusta en los metadatos XMP. En este caso, no se requiere explícitamente la extracción de miniaturas. Sin embargo, si el servidor de InDesign no se procesa como proxy, las miniaturas se deben extraer explícitamente para los archivos de InDesign.

### Creación de referencias arrastrando recursos {#create-references-by-dragging-aem-assets}

Este procedimiento es similar a [Agregar recursos de AEM como referencias en Adobe Illustrator](#refai).

### Creación de referencias a recursos mediante la exportación de un archivo ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Siga los pasos que se describen en [Crear modelos](/help/sites-developing/workflows-models.md) de flujo de trabajo para crear un nuevo flujo de trabajo.
1. Utilice la función Empaquetar de Adobe InDesign para exportar el documento.
Adobe InDesign puede exportar un documento y los recursos vinculados como un paquete. En este caso, la carpeta exportada contiene una carpeta Links que contiene subrecursos en el archivo de InDesign.
1. Cree un archivo ZIP y cárguelo en el repositorio de AEM.
1. Inicie el `Unarchiver` flujo de trabajo.
1. Cuando se completa el flujo de trabajo, se hace referencia automáticamente a las referencias de la carpeta Vínculos como subrecursos. Para ver una lista de los recursos referidos, vaya a la página de detalles del recurso de InDesign y cierre el [raíl](/help/sites-authoring/basic-handling.md#rail-selector).

## Adición de recursos de AEM como referencias en Adobe Photoshop {#refps}

1. Con un cliente WebDav, monte Recursos AEM como unidad.
1. Para crear referencias a recursos AEM en un archivo de Photoshop, navegue hasta los recursos correspondientes de la unidad montada utilizando la función Colocar el vínculo en Photoshop.

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. Guarde el archivo en Photoshop en la unidad montada o [cárguelo](/help/assets/managing-assets-touch-ui.md#uploading-assets) en el repositorio de AEM.
1. Una vez finalizado el flujo de trabajo, las referencias a los recursos de AEM existentes se muestran en la página de detalles de los recursos.

   Para ver los recursos a los que se hace referencia, cierre el [raíl](/help/sites-authoring/basic-handling.md#rail-selector) en la página de detalles del recurso.

1. Los recursos a los que se hace referencia también contienen la lista de recursos desde los que se hace referencia. Para ver una lista de los recursos a los que se hace referencia, vaya a la página de detalles del recurso y cierre el [raíl](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>También se puede hacer referencia a los recursos dentro de los recursos compuestos en función de su ID de documento y su ID de instancia. Esta funcionalidad solo está disponible en las versiones de Adobe Illustrator y Adobe Photoshop. Para otros, la referencia se realiza en función de la ruta relativa de los recursos vinculados en el recurso compuesto principal, como se hacía en versiones anteriores de AEM.

## Creación de subrecursos {#generate-subassets}

Para los recursos admitidos con formatos de varias páginas: archivos PDF, archivos AI, archivos de Microsoft PowerPoint y Apple Keynote y archivos de Adobe InDesign: AEM puede generar subrecursos que corresponden a cada página individual del recurso original. Estos subrecursos están vinculados al recurso *principal* y facilitan la vista de varias páginas. Para todos los demás fines, los subrecursos se tratan como recursos normales en AEM.

La generación de subconjuntos está deshabilitada de forma predeterminada. Para habilitar la generación de subrecursos, siga estos pasos:

1. Inicie sesión en Experience Manager como administrador. Acceda a **[!UICONTROL Herramientas > Flujo de trabajo > Modelos]**.
1. Seleccione **[!UICONTROL Flujo de trabajo de recursos]** de actualización de DAM y haga clic en **[!UICONTROL Editar]**.
1. Haga clic en **[!UICONTROL Alternar panel]** lateral y busque el paso **[!UICONTROL Crear subrecurso]** . Agregue el paso al flujo de trabajo. Haga clic en **[!UICONTROL Sincronizar]**.

Para generar los subrecursos, realice una de las siguientes acciones:

* Nuevos recursos: El flujo de trabajo de Recursos [!UICONTROL de actualización de] DAM se ejecuta en cualquier recurso nuevo que se cargue en AEM. Los subrecursos se generan automáticamente para los nuevos recursos de varias páginas.
* Recursos existentes de varias páginas: Ejecute manualmente el flujo de trabajo de Recursos [!UICONTROL de actualización de] DAM siguiendo uno de los pasos siguientes:

   * Seleccione un recurso y haga clic en [!UICONTROL Línea de tiempo] para abrir el panel izquierdo. Como alternativa, utilice el método abreviado de teclado `alt + 3`. Haga clic en [!UICONTROL Iniciar flujo de trabajo], seleccione Actualizar recurso DAM, haga clic en [!UICONTROL Iniciar]y, a continuación, en [!UICONTROL Continuar].
   * Seleccione un recurso y haga clic en [!UICONTROL Crear > Flujo de trabajo] en la barra de herramientas. En el cuadro de diálogo emergente, seleccione [!UICONTROL DAM Update Asset] workflow, haga clic en [!UICONTROL Iniciar]y, a continuación, en [!UICONTROL Continuar].

Específicamente para documentos de Microsoft Word, ejecute el flujo de trabajo **[!UICONTROL Análisis de documentos]** de Word DAM. Genera un `cq:Page` componente a partir del contenido del documento de Microsoft Word. Se hace referencia a las imágenes extraídas del documento desde el `cq:Page` componente. Estas imágenes se extraen aunque la generación de subrecursos esté desactivada.

## View subassets {#viewing-subassets}

Los subrecursos solo se muestran si se generan y están disponibles para el recurso de varias páginas seleccionado. Para ver los subrecursos generados, abra el recurso de varias páginas. En el área superior izquierda de la página, haga clic en el icono ![del carril](assets/do-not-localize/aem_leftrail_contentonly.png) izquierdo y haga clic en **[!UICONTROL Subrecursos]** en la lista. Al seleccionar **[!UICONTROL Subrecursos]** en la lista. Como alternativa, utilice el método abreviado de teclado `alt + 5`.

![Ver subrecursos para un recurso de varias páginas](assets/view_subassets_simulation.gif)

## Ver páginas de un archivo de varias páginas {#view-pages-of-a-multi-page-file}

Puede ver un archivo de varias páginas, como un archivo PDF, INDD, PPT, PPTX y AI, mediante la función Visor de páginas de Recursos AEM. Abra un recurso de varias páginas y haga clic en **[!UICONTROL Ver páginas]** en la esquina superior izquierda de la página. El visor de páginas que se abre muestra las páginas del recurso y los controles para examinar y aplicar zoom en cada página.

![Ver y ver páginas de un recurso de varias páginas](assets/view_multipage_asset_fmr.gif)

En InDesign, puede extraer páginas con el servidor de InDesign. Si las vistas previas de las páginas se guardan durante la creación de archivos de InDesign, InDesign Server no es necesario para la extracción de páginas.

Las siguientes opciones están disponibles en la barra de herramientas, en el carril izquierdo y en los controles del visor de páginas:

* **[!UICONTROL Acciones]** de escritorio para abrir o mostrar un subrecurso específico mediante la aplicación de escritorio AEM. Consulte cómo [configurar acciones](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2) de escritorio si utiliza la aplicación de escritorio AEM.

* **[!UICONTROL La opción Propiedades]** abre la página [!UICONTROL Propiedades] del subrecurso específico.

* **[!UICONTROL La opción Anotar]** le permite anotar el subrecurso específico. Las anotaciones que se utilizan en subrecursos independientes se recopilan y muestran juntas cuando se abre el recurso principal para su visualización.

* **[!UICONTROL La opción Información general]** de página muestra todos los subrecursos simultáneamente.

* **[!UICONTROL La opción Línea de tiempo]** del carril izquierdo después de hacer clic en el icono ![del carril](assets/do-not-localize/aem_leftrail_contentonly.png) izquierdo muestra el flujo de actividades del archivo.
