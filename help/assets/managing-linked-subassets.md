---
title: Administrar recursos compuestos con referencias y varias páginas
description: Obtenga información sobre cómo crear referencias a recursos digitales desde [!DNL Adobe InDesign], [!DNL Adobe Illustrator], y [!DNL Adobe Photoshop]. Utilice la función Visualizador de páginas para ver páginas de subrecursos individuales de archivos de varias páginas, como archivos de PDF, INDD, PPT, PPTX e AI.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 0%

---

# Administración de recursos compuestos y de varias páginas {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] puede identificar si un archivo cargado contiene referencias a recursos que ya existen en el repositorio. Esta función solo está disponible para formatos de archivo compatibles. Si el recurso cargado contiene referencias a [!DNL Experience Manager] recursos, se crea un vínculo bidireccional entre los recursos cargados y los referenciados.

Además de eliminar la redundancia, haga referencia a los recursos en [!DNL Adobe Creative Cloud] Las aplicaciones de mejoran la colaboración y aumentan la eficiencia y la productividad de los usuarios.

[!DNL Experience Manager Assets] admite referencias bidireccionales. Puede encontrar recursos a los que se hace referencia en la página de detalles de recursos del archivo cargado. Además, puede ver los archivos de referencia en la página de detalles de recurso del recurso al que se hace referencia.

Las referencias se resuelven en función de la ruta, el ID de documento y el ID de instancia de los recursos a los que se hace referencia.

## [!DNL Adobe Illustrator]: Agregar recursos digitales como referencias {#refai}

Puede hacer referencia a recursos digitales existentes desde una [!DNL Adobe Illustrator] archivo.

1. Uso de [[!DNL Experience Manager] aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html), recupere los recursos digitales en el sistema de archivos local. Vaya a la ubicación del sistema de archivos del recurso al que desee hacer referencia.
1. Arrastre el recurso de la carpeta local a la carpeta [!DNL Illustrator] archivo.

1. Guarde el [!DNL Illustrator] a la unidad montada, o [cargar](/help/assets/manage-assets.md#uploading-assets) a la [!DNL Experience Manager] repositorio.

1. Una vez completado el flujo de trabajo, vaya a la página de detalles del recurso para el recurso. Las referencias a recursos digitales existentes se enumeran en **[!UICONTROL Dependencias]** en el **[!UICONTROL Referencias]** columna.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Los recursos a los que se hace referencia aparecen bajo **[!UICONTROL Dependencias]** también pueden hacer referencia a él archivos que no sean el actual. Para ver una lista de archivos de referencia de un recurso, haga clic en el recurso en, en **[!UICONTROL Dependencias]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Clic **[!UICONTROL Ver propiedades]** en la barra de herramientas. En el [!UICONTROL Propiedades] página, la lista de archivos que hacen referencia al recurso actual aparece en la **[!UICONTROL Referencias]** en la columna **[!UICONTROL Básico]** pestaña.

   ![ver las referencias de Experience Manager Assets en la columna Referencias en los detalles del recurso](assets/asset-references.png)

   *Imagen: referencias de recursos en detalles de recursos.*

## [!DNL Adobe InDesign]: Agregar recursos digitales como referencias {#add-aem-assets-as-references-in-adobe-indesign}

Para hacer referencia a recursos digitales desde un [!DNL InDesign] , arrastre los recursos al archivo [!DNL InDesign] archivar o exportar el [!DNL InDesign] como archivo ZIP.

Ya existen recursos de referencia en [!DNL Experience Manager Assets]. Puede extraer subrecursos mediante [configurar InDesign Server](indesign.md). Recursos incrustados en una [!DNL InDesign] Los archivos de se extraen como subrecursos.

>[!NOTE]
>
>Si la variable [!DNL InDesign Server] es proxy, [!DNL InDesign] XMP Los archivos tienen la vista previa incrustada en los metadatos de la. En este caso, la extracción de miniaturas no es obligatoria de forma explícita. Sin embargo, si la variable [!DNL InDesign Server] no está proxy, las miniaturas deben extraerse explícitamente para [!DNL InDesign] archivos.

Cuando se carga un archivo INDD, las referencias se recuperan consultando los recursos que tienen `xmpMM:InstanceID` y `xmpMM:DocumentID` en el repositorio.

### Creación de referencias arrastrando recursos {#create-references-by-dragging-aem-assets}

Este procedimiento es similar al siguiente [adición de recursos digitales como referencias en Adobe Illustrator](#refai).

### Crear referencias a recursos exportando un archivo ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Siga los pasos de [Creación de modelos de flujo de trabajo](/help/sites-developing/workflows-models.md) para crear un flujo de trabajo.
1. Utilice el [Funcionalidad de paquete](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) de [!DNL Adobe InDesign] para exportar el documento. [!DNL Adobe InDesign] Puede exportar un documento y los recursos vinculados como un paquete. En este caso, la carpeta exportada contiene un `Links` carpeta que contiene subrecursos en el [!DNL InDesign] archivo. El `Links` está presente en la misma carpeta que el archivo INDD.
1. Cree un archivo ZIP y cárguelo en [!DNL Experience Manager] repositorio.
1. Inicie el `Unarchiver` flujo de trabajo.
1. Cuando se completa el flujo de trabajo, se hace referencia automáticamente a las referencias de la carpeta Links como subrecursos. Para ver una lista de los recursos a los que se hace referencia, vaya a la página de detalles de recursos de [!DNL InDesign] y cierre el recurso [Carril](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]: Agregar recursos digitales como referencias {#refps}

1. Uso [!DNL Experience Manager] aplicación de escritorio para acceder a [!DNL Experience Manager Assets]. Descargue y muestre los recursos en el sistema de archivos local. Utilice el [!UICONTROL Colocar elemento vinculado] funcionalidad en [!DNL Adobe Photoshop]. Consulte [colocar recursos en la aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

1. Guardar en [!DNL Photoshop] a la unidad montada o [cargar](/help/assets/manage-assets.md#uploading-assets) a la [!DNL Experience Manager] repositorio.
1. Una vez finalizado el flujo de trabajo, las referencias a los campos existentes [!DNL Experience Manager] los recursos se muestran en la página detalles del recurso.

   Para ver los recursos a los que se hace referencia, cierre el [Carril](/help/sites-authoring/basic-handling.md#rail-selector) en la página detalles del recurso.

1. Los recursos a los que se hace referencia también contienen la lista de recursos desde la que se hace referencia a ellos. Para ver una lista de los recursos a los que se hace referencia, vaya a la página de detalles del recurso y cierre la [Carril](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>También se puede hacer referencia a los recursos de los recursos compuestos en función de su ID de documento e ID de instancia. Esta funcionalidad está disponible con [!DNL Adobe Illustrator] y [!DNL Adobe Photoshop] solo versiones. Para otros, la referencia se realiza en función de la ruta relativa de los recursos vinculados en el recurso compuesto principal, como se hace en versiones anteriores de [!DNL Experience Manager].

## Creación de subrecursos {#generate-subassets}

Para los recursos compatibles con formatos de varias páginas: archivos de PDF, archivos AI, [!DNL Microsoft PowerPoint] y [!DNL Apple Keynote] archivos, y [!DNL Adobe InDesign] archivos — [!DNL Experience Manager] Puede generar subrecursos que se correspondan con cada página individual del recurso original. Estos subrecursos están vinculados a *parent* y facilitar la vista de varias páginas. Para todos los demás fines, los subactivos se tratan como activos normales en [!DNL Experience Manager].

La generación de subrecursos está deshabilitada de forma predeterminada. Para habilitar la generación de subrecursos, siga estos pasos:

1. Iniciar sesión en [!DNL Experience Manager] como administrador. Acceso **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. Seleccionar **[!UICONTROL Recurso de actualización DAM]** flujo de trabajo y clic **[!UICONTROL Editar]**.
1. Clic **[!UICONTROL Alternar panel lateral]** y busque el **[!UICONTROL Crear subrecurso]** paso. Añada la etapa al flujo de trabajo. Haga clic en **[!UICONTROL Sincronizar]**.

Para generar los subrecursos, realice una de las siguientes acciones:

* Nuevos recursos: La [!UICONTROL Actualizar recursos DAM] el flujo de trabajo se ejecuta en cualquier nuevo recurso que se haya cargado en [!DNL Experience Manager]. Los subrecursos se generan automáticamente para los nuevos recursos de varias páginas.
* Recursos de varias páginas existentes: Ejecute manualmente la variable [!UICONTROL Actualizar recursos DAM] flujo de trabajo siguiendo cualquiera de los pasos:

   * Seleccione un recurso y haga clic en [!UICONTROL Cronología] para abrir el panel izquierdo. También puede utilizar el método abreviado de teclado `alt + 3`. Clic [!UICONTROL Iniciar flujo de trabajo], seleccione [!UICONTROL Recurso de actualización DAM], haga clic en [!UICONTROL Inicio]y haga clic en [!UICONTROL Continuar].
   * Seleccione un recurso y haga clic en [!UICONTROL Crear] > [!UICONTROL Flujo de trabajo] en la barra de herramientas. En el cuadro de diálogo emergente, seleccione [!UICONTROL Recurso de actualización DAM] flujo de trabajo, haga clic en [!UICONTROL Inicio]y haga clic en [!UICONTROL Continuar].

Específicamente para documentos de Microsoft Word, ejecute el **[!UICONTROL Análisis de documentos Word DAM]** flujo de trabajo. Esto genera un `cq:Page` del contenido del documento de Microsoft Word. Se hace referencia a las imágenes extraídas del documento desde el `cq:Page` componente. Estas imágenes se extraen incluso si la generación de subrecursos está desactivada.

>[!NOTE]
>
>En el [!UICONTROL Proceso de creación de subrecursos - Propiedades de la etapa] in [!UICONTROL Argumentos del proceso], puede especificar el número de subrecursos que desea [!DNL Experience Manager] genera. El valor predeterminado es 5. Para generar todos los subrecursos, deje vacío el campo. Si el campo tiene un valor negativo, no se generan subrecursos.

## Ver subrecursos {#viewing-subassets}

Los subrecursos solo se muestran si se generan y están disponibles para el recurso de varias páginas seleccionado. Para ver los subrecursos generados, abra el recurso de varias páginas. En el área superior izquierda de la página, haga clic en ![Opción para abrir el carril izquierdo](assets/do-not-localize/aem_leftrail_contentonly.png) y haga clic en **[!UICONTROL Recursos secundarios]** de la lista. Al seleccionar **[!UICONTROL Recursos secundarios]** de la lista. También puede utilizar el método abreviado de teclado `alt + 5`.

![Ver subrecursos de un recurso de varias páginas](assets/view_subassets_simulation.gif)

## Ver páginas de un archivo de varias páginas {#view-pages-of-a-multi-page-file}

Puede ver un archivo de varias páginas, como PDF, INDD, PPT, PPTX y archivo AI, mediante la función Visor de páginas de [!DNL Experience Manager Assets]. Abra un recurso de varias páginas y haga clic en **[!UICONTROL Ver páginas]** desde la esquina superior izquierda de la página. El visor de páginas que se abre muestra las páginas del recurso y los controles para examinar y ampliar cada página.

![Ver y ver páginas de un recurso de varias páginas](assets/view_multipage_asset_fmr.gif)

Para [!DNL InDesign], puede extraer páginas utilizando [!DNL InDesign Server]. Si las vistas previas de las páginas se guardan durante [!DNL InDesign] creación de archivos, entonces [!DNL InDesign Server] no es necesario para la extracción de páginas.

Las siguientes opciones están disponibles en la barra de herramientas, en el carril izquierdo y en los controles del visor de páginas:

* **[!UICONTROL Acciones de escritorio]** para abrir o mostrar un subrecurso específico mediante [!DNL Experience Manager] aplicación de escritorio. Consulte cómo [configurar acciones de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2) si está utilizando [!DNL Experience Manager] aplicación de escritorio.

* **[!UICONTROL Propiedades]** abre la opción [!UICONTROL Propiedades] página del subactivo específico.

* **[!UICONTROL Anotar]** La opción permite realizar anotaciones en el subrecurso específico. Las anotaciones que utilice en subrecursos independientes se recopilan y se muestran juntas cuando el recurso principal se abre para su visualización.

* **[!UICONTROL Información general de página]** La opción muestra todos los subrecursos simultáneamente.

* **[!UICONTROL Cronología]** del carril izquierdo después de hacer clic en ![Opción para abrir el carril izquierdo](assets/do-not-localize/aem_leftrail_contentonly.png) muestra el flujo de actividad del archivo.

## Prácticas recomendadas y limitación {#best-practice-limitation-tips}

* La generación de subrecursos puede consumir muchos recursos en cualquier [!DNL Experience Manager] implementación. Si está generando subrecursos cuando se cargan recursos complejos, agregue el paso en el flujo de trabajo de recursos de actualización de DAM. Si está generando subrecursos bajo demanda, cree un flujo de trabajo independiente para generar subrecursos. Un flujo de trabajo dedicado le permite omitir los demás pasos del flujo de trabajo de recursos de actualización de DAM y guardar recursos de cálculo.

>[!MORELIKETHIS]
>
>* [Uso de la aplicación de escritorio de Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Configuración de acciones de escritorio en Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Crear objetos inteligentes vinculados en Adobe Photoshop](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Colocar gráficos en Adobe InDesign](https://helpx.adobe.com/indesign/using/placing-graphics.html)
