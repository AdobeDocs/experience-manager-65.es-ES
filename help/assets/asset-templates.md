---
title: Plantillas de recursos en [!DNL Adobe Experience Manager Assets].
description: Obtenga información sobre las plantillas de recursos [!DNL Adobe Experience Manager Assets] en y cómo utilizar plantillas de recursos para crear material publicitario de marketing.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 91caca39b0b6c5c0c98b58be02f518901a3d90e3
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 0%

---


# Asset templates {#asset-templates}

Las plantillas de recursos son una clase especial de recursos que facilitan la reutilización rápida de contenido con gran riqueza visual para medios digitales e impresos. Una plantilla de recurso incluye dos partes, la sección de mensajería fija y la sección editable. La sección de mensajes fijos puede contener contenido propio, como el logotipo de la marca y la información de copyright que está desactivada para la edición. La sección editable puede contener contenido visual y textual en los campos que se pueden editar para personalizar la mensajería.

La flexibilidad para realizar ediciones limitadas y, al mismo tiempo, asegurar la señalización global, hace que las plantillas de recursos sean los componentes básicos idóneos para una rápida adaptación y distribución del contenido como artefactos de contenido para diversas funciones. La reasignación del propósito del contenido ayuda a reducir el costo de la administración de canales digitales e impresos y ofrece experiencias holísticas y coherentes en estos canales.

Como especialista en mercadotecnia, puede almacenar y administrar plantillas dentro [!DNL Experience Manager Assets] y utilizar una única plantilla base para crear varias experiencias de impresión personalizadas con facilidad. Puede crear varios tipos de material publicitario de marketing, como folletos, volantes, postales, tarjetas de presentación, etc., para transmitir con lentitud su mensaje de marketing a los clientes. También puede montar salidas de impresión de varias páginas a partir de salidas de impresión nuevas o existentes. Por encima de todo, puede ofrecer simultáneamente experiencias digitales y de impresión con facilidad para ofrecer una experiencia coherente e integrada a los usuarios.

Si bien las plantillas de recursos son principalmente [!DNL Adobe InDesign] archivos, la competencia en [!DNL Adobe InDesign] no es una barrera para la creación de artefactos estelares. No es necesario asignar los campos de la [!DNL Adobe InDesign] plantilla a los campos de producto que, de lo contrario, se requieren al crear catálogos. Puede editar las plantillas en modo WYSIWYG directamente en la interfaz web. Sin embargo, para [!DNL Adobe InDesign] procesar los cambios de edición, primero debe configurarlos [!DNL Experience Manager Assets] para integrarlos con [!DNL Adobe InDesign Server].

La capacidad de editar [!DNL Adobe InDesign] plantillas desde la interfaz web ayuda a fomentar la buena colaboración entre el personal creativo y el de marketing. La mayor velocidad de contenido reduce el tiempo de comercialización de las garantías de marketing.

Puede lograr lo siguiente con plantillas de recursos:

* Modifique los campos de plantilla editables desde la interfaz web.
* Controle el estilo básico del texto, por ejemplo, el tamaño de fuente, el estilo y el tipo en el nivel de etiqueta.
* Cambie las imágenes dentro de la plantilla mediante el selector de contenido.
* Se editan las plantillas de Previsualización.
* Combine varios archivos de plantilla para crear un artefacto de varias páginas.

Al elegir una plantilla para el material promocional, [!DNL Experience Manager Assets] crea una copia de la plantilla que puede editar. Se conserva la plantilla original, lo que garantiza que la señalización global permanezca intacta y se pueda reutilizar para reforzar la coherencia de la marca.

Puede exportar el archivo actualizado dentro de la carpeta principal en los formatos INDD, PDF o JPG. También puede descargar la salida en estos formatos al sistema de archivos local.

## Crear una garantía {#creating-a-collateral}

Considere un escenario en el que desee crear material publicitario digital imprimible, como folletos, volantes y publicidades para una próxima campaña y compartirlo con tiendas de venta en todo el mundo. La creación de material publicitario basado en una plantilla ayuda a ofrecer una experiencia unificada al cliente en todos los canales. Los diseñadores pueden crear las plantillas de campaña (de una sola página o de varias páginas) mediante una solución creativa, como [!DNL InDesign] y cargar las plantillas a [!DNL Experience Manager Assets] su nombre. Antes de crear un colateral, tenga una o varias plantillas INDD cargadas y disponibles con [!DNL Experience Manager] antelación.

1. En [!DNL Experience Manager] la interfaz, haga clic en [!UICONTROL Recursos].

1. En las opciones, seleccione **[!UICONTROL Plantillas]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. Haga clic en **[!UICONTROL Crear]** y, a continuación, elija el material que desee crear en el menú. Por ejemplo, elija **[!UICONTROL Folleto]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. Cargue una o más plantillas INDD y esté disponible con [!DNL Experience Manager] antelación. Elija una plantilla para el folleto y haga clic en **[!UICONTROL Siguiente]**.

   ![chlimage_1-103](assets/chlimage_1-308.png)

1. Especifique un nombre y una descripción opcional para el folleto.

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. (Opcional) Haga clic en **[!UICONTROL Etiquetas]** y seleccione una o varias etiquetas para el folleto. Haga clic en **[!UICONTROL Confirmar]** para confirmar la selección.

   ![chlimage_1-105](assets/chlimage_1-310.png)

1. Haga clic en **[!UICONTROL Crear]**. Un cuadro de diálogo confirma que se crea un nuevo folleto. Haga clic en **[!UICONTROL Abrir]** para abrir el folleto en modo de edición.

   <!--![chlimage_1-106](assets/.png) -->

   De forma alternativa, cierre el cuadro de diálogo y vaya a la carpeta de la página Plantillas con la que comenzó a crear la vista del folleto que ha creado. El tipo de garantía aparece en su miniatura en la vista de la tarjeta. Por ejemplo, en este caso, la palabra [!UICONTROL Folleto] se muestra en la miniatura.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## Editar una garantía {#editing-a-collateral}

Puede editar un colateral inmediatamente después de crearlo. También puede abrirlo desde la página [!UICONTROL Plantillas] o desde la página de recursos.

1. Para abrir el material publicitario para la edición, realice una de las siguientes acciones:

   * Abra el colateral (folleto en este caso) que ha creado en el paso 7 de [Crear una colateral](/help/assets/asset-templates.md#creating-a-collateral).
   * En la página Plantillas, desplácese hasta la carpeta en la que haya creado el colateral y haga clic en la acción rápida [!UICONTROL Editar] en la miniatura de un colateral.
   * En la página de recursos para el material promocional, haga clic en **[!UICONTROL Editar]** en la barra de herramientas.
   * Select the collateral and click **[!UICONTROL Edit]** from the toolbar.

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   El buscador de recursos y el editor de texto se muestran a la izquierda de la página. El editor de texto está abierto de forma predeterminada.

   Puede utilizar el editor de texto para modificar el texto que desea que se muestre en el campo de texto. Puede modificar el tamaño, el estilo, el color y el tipo de fuente en el nivel de etiqueta.

   Con el buscador de recursos, puede buscar o buscar imágenes dentro de la plantilla [!DNL Experience Manager Assets] y reemplazar las imágenes editables con las imágenes que desee.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   Los editables se muestran a la derecha. Para que un campo se pueda editar en [!DNL Experience Manager Assets], se debe etiquetar el campo correspondiente de la plantilla en [!DNL InDesign]. En otras palabras, deben marcarse como editables en [!DNL InDesign].

   ![chlimage_1-110](assets/chlimage_1-315.png)

   >[!NOTE]
   >
   >Asegúrese de que [!DNL Experience Manager] la implementación está integrada con un [!DNL InDesign Server] para permitir [!DNL Experience Manager Assets] extraer datos de la [!DNL InDesign] plantilla y ponerlos a disposición para su edición. Para obtener más información, consulte [Integración de recursos de Experience Manager con InDesign Server](/help/assets/indesign.md).

1. Para modificar el texto de un campo editable, haga clic en el campo de texto de la lista de campos editables y edite el texto del campo.

   ![chlimage_1-111](assets/chlimage_1-316.png)

   Puede editar las propiedades del texto, por ejemplo, el estilo de fuente, el color y el tamaño utilizando las opciones proporcionadas.

1. Haga clic en **[!UICONTROL Previsualización]** para previsualización de los cambios de texto.

   ![chlimage_1-112](assets/chlimage_1-317.png)

1. Para intercambiar una imagen, haga clic en el **[!UICONTROL Buscador]** de recursos.

   ![chlimage_1-113](assets/chlimage_1-318.png)

1. Seleccione el campo de imagen de la lista de campos editables y, a continuación, arrastre una imagen deseada del selector de recursos al campo editable.

   ![chlimage_1-114](assets/chlimage_1-319.png)

   También puede buscar imágenes mediante palabras clave, etiquetas y según su estado de publicación. Puede navegar por el repositorio y navegar hasta la ubicación de la imagen deseada [!DNL Experience Manager Assets] .

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. Haga clic en **[!UICONTROL Previsualización]** para previsualización de la imagen.

   ![chlimage_1-116](assets/chlimage_1-321.png)

1. Para editar una página específica en una página secundaria de varias páginas, utilice el navegador de páginas en la parte inferior.

   ![chlimage_1-117](assets/chlimage_1-322.png)

1. Haga clic en **[!UICONTROL Previsualización]** en la barra de herramientas para previsualización de todos los cambios. Haga clic en **[!UICONTROL Listo]** para guardar los cambios de edición en el colateral.

   >[!NOTE]
   >
   >Las opciones Previsualización y Finalizado solo se activan cuando los campos de imagen editables del material no tienen iconos que faltan. Si falta algún icono en el colateral, es porque [!DNL Experience Manager] no puede resolver las imágenes de la [!DNL InDesign] plantilla. Normalmente, [!DNL Experience Manager] no puede resolver imágenes en los siguientes casos:
   >
   >* Las imágenes no se incrustan en la [!DNL InDesign] plantilla subyacente.
   >* Las imágenes están vinculadas desde el sistema de archivos local.

   >
   >Para habilitar [!DNL Experience Manager] la resolución de imágenes, haga lo siguiente:
   >
   >* Incrustar imágenes al crear [!DNL InDesign] plantillas (consulte [Acerca de los vínculos y los gráficos](https://helpx.adobe.com/indesign/using/graphics-links.html)incrustados).
   >* Monte [!DNL Experience Manager] en el sistema de archivos local y, a continuación, asigne los iconos que faltan con los recursos existentes en [!DNL Experience Manager].

   >
   >Para obtener más información sobre cómo trabajar con [!DNL InDesign] documentos, consulte Prácticas [recomendadas para trabajar con documentos de InDesign en Experience Manager](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. Para generar una representación en PDF del folleto, seleccione la opción Acrobat en el cuadro de diálogo y haga clic en **[!UICONTROL Continuar]**.
1. El colateral se crea en la carpeta en la que se inició. Para realizar la vista de las representaciones, abra el colateral y seleccione **[!UICONTROL Representaciones]** en la lista GlobalNav.

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. Haga clic en la representación PDF desde la lista de representaciones para descargar el archivo PDF. Abra el archivo PDF para revisar el material promocional.

   ![chlimage_1-119](assets/chlimage_1-324.png)

## Combinar material publicitario {#merge-collateral}

1. En la [!DNL Experience Manager] interfaz, haga clic en [!UICONTROL Recursos] en la página de navegación.

1. En las opciones, seleccione **[!UICONTROL Plantillas]**.

1. Haga clic en **[!UICONTROL Crear]** y elija **[!UICONTROL Combinar]** en el menú.

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. En la página Combinar  plantillas, haga clic en **[!UICONTROL Combinar]** ![agregar recursos](assets/do-not-localize/assets_add_icon.png).

1. Vaya a la ubicación del material que desea combinar, haga clic en las miniaturas del material que desea combinar para seleccionarlo.

   ![chlimage_1-122](assets/chlimage_1-327.png)

   También puede buscar plantillas desde el cuadro Omniture.

   ![chlimage_1-123](assets/chlimage_1-328.png)

   Puede navegar por el repositorio o las [!DNL Experience Manager Assets] colecciones, navegar hasta la ubicación de las plantillas que desee y seleccionarlas para combinarlas.

   ![chlimage_1-124](assets/chlimage_1-329.png)

   Puede aplicar varios filtros para buscar en las plantillas que desee. Por ejemplo, puede buscar plantillas en función del tipo de archivo o las etiquetas.

   ![chlimage_1-125](assets/chlimage_1-330.png)

1. Click **[!UICONTROL Next]** from the toolbar.
1. En la pantalla **[!UICONTROL Previsualización y reorganización]** , reorganice las plantillas si es necesario y previsualización la selección de las plantillas que se van a combinar. A continuación, haga clic en **[!UICONTROL Siguiente]** en la barra de herramientas.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. En la pantalla [!UICONTROL Configurar plantilla] , especifique un nombre para el colateral. De forma opcional, especifique las etiquetas que considere adecuadas. Si desea exportar la salida en formato PDF, seleccione **[!UICONTROL Acrobat (.PDF)]**. De forma predeterminada, la garantía se exporta en formato JPG y [!DNL InDesign] . Para cambiar la miniatura de visualización del material publicitario de varias páginas, haga clic en **[!UICONTROL Cambiar miniatura]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. Haga clic en **[!UICONTROL Guardar]** y, a continuación, haga clic en **[!UICONTROL Aceptar]** en el cuadro de diálogo para cerrar el cuadro de diálogo. El colateral de varias páginas se crea en la carpeta en la que se inició.

   >[!NOTE]
   >
   >No puede editar una garantía combinada posteriormente ni utilizarla para crear otra garantía.

## Prácticas recomendadas y limitaciones {#best-practices-limitations-tips}

* El [!DNL InDesign] editor de [!DNL Experience Manager] funciona a nivel de etiqueta y todo el texto de una sola etiqueta se considera una sola entidad. Para conservar el formato y los estilos de texto al editarlos, etiquete cada párrafo (o texto con un estilo diferente) por separado.
