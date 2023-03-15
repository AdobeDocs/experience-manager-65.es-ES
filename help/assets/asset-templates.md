---
title: Plantillas de recursos
description: Obtenga información sobre las plantillas de recursos en [!DNL Adobe Experience Manager Assets] y cómo utilizar plantillas de activos para crear garantías de marketing.
contentOwner: AG
role: User
feature: Asset Management,Developer Tools
exl-id: 12c92aad-3a1d-486e-a830-31de2fc6d07b
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---

# Plantillas de recursos {#asset-templates}

Las plantillas de recursos son una clase especial de recursos que facilitan la reutilización rápida de contenido con gran riqueza visual para medios digitales e impresos. Una plantilla de activos consta de dos partes, la sección de mensajería fija y la sección editable. La sección de mensajería fija puede contener contenido de propiedad, como el logotipo de la marca y la información de copyright, que no se pueden editar. La sección editable puede contener contenido visual y textual en campos que se pueden editar para personalizar la mensajería.

La flexibilidad para realizar ediciones limitadas y, al mismo tiempo, proteger la señalización global hace que las plantillas de recursos sean los bloques de creación ideales para una adaptación y distribución rápidas del contenido como artefactos de contenido para diversas funciones. La reutilización del contenido ayuda a reducir el coste de gestión de los canales impresos y digitales, y ofrece experiencias integrales y coherentes en todos estos canales.

Como especialista en marketing, puede almacenar y administrar plantillas en [!DNL Experience Manager Assets] y utilice una sola plantilla base para crear varias experiencias de impresión personalizadas con facilidad. Puede crear varios tipos de material promocional de marketing, incluidos folletos, prospectos, postales, tarjetas de presentación, etc., para transmitir con lucidez su mensaje de marketing a los clientes. También puede montar salidas de impresión de varias páginas a partir de salidas de impresión nuevas o existentes. Por encima de todo, puede ofrecer simultáneamente experiencias digitales e impresas con facilidad para proporcionar una experiencia coherente e integrada para los usuarios.

Mientras que las plantillas de recursos son principalmente [!DNL Adobe InDesign] archivos, competencia en [!DNL Adobe InDesign] no es una barrera para crear artefactos estelares. No es necesario asignar los campos del [!DNL Adobe InDesign] plantilla con los campos de producto que, de lo contrario, deberá rellenar al crear catálogos. Puede editar las plantillas en modo WYSIWYG directamente en la interfaz web. Sin embargo, para [!DNL Adobe InDesign] para procesar los cambios de edición, primero debe configurar [!DNL Experience Manager Assets] para integrar con [!DNL Adobe InDesign Server].

La capacidad de edición [!DNL Adobe InDesign] Las plantillas de la interfaz web ayudan a fomentar la buena colaboración entre el personal creativo y de marketing. El aumento de la velocidad de contenido reduce el tiempo de comercialización de las garantías reales de marketing.

Puede lograr lo siguiente con las plantillas de recursos:

* Modifique los campos de plantilla editables desde la interfaz web.
* Controle el estilo básico del texto, por ejemplo el tamaño de fuente, el estilo y el tipo en el nivel de etiqueta.
* Cambiar imágenes dentro de la plantilla mediante el Selector de contenido.
* Previsualizar ediciones de plantilla.
* Combine varios archivos de plantilla para crear un artefacto de varias páginas.

Al elegir una plantilla para el material colateral, [!DNL Experience Manager Assets] crea una copia de la plantilla que puede editar. La plantilla original se conserva, lo que garantiza que la señalización global permanezca intacta y se pueda reutilizar para reforzar la coherencia de la marca.

Puede exportar el archivo actualizado dentro de la carpeta principal en los formatos INDD, PDF o JPG. También puede descargar la salida en estos formatos en su sistema de archivos local.

## Crear un aval {#creating-a-collateral}

Imagine un escenario en el que desee crear material promocional imprimible digital, como folletos, prospectos y anuncios para una próxima campaña, y compártalo con tiendas de venta directa de todo el mundo. La creación de material promocional basado en una plantilla ayuda a ofrecer una experiencia de cliente unificada en todos los canales. Los diseñadores pueden crear las plantillas de campaña (de una sola página o de varias páginas) mediante una solución creativa, como [!DNL InDesign] y cargue las plantillas en [!DNL Experience Manager Assets] para usted. Antes de crear un material colateral, tenga una o más plantillas INDD cargadas en y disponibles en [!DNL Experience Manager] por adelantado.

1. Entrada [!DNL Experience Manager] clic de interfaz [!UICONTROL Assets].

1. En las opciones, elija **[!UICONTROL Plantillas]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. Clic **[!UICONTROL Crear]** y, a continuación, elija el material colateral que desea crear en el menú. Por ejemplo, elija **[!UICONTROL Folleto]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. Tener una o más plantillas INDD cargadas en y disponibles en [!DNL Experience Manager] por adelantado. Seleccione una plantilla para el folleto y haga clic en **[!UICONTROL Siguiente]**.
1. Especifique un nombre y una descripción opcional para el folleto.

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. (Opcional) Haga clic en **[!UICONTROL Etiquetas]** y seleccione una o varias etiquetas para el folleto. Clic **[!UICONTROL Confirmar]** para confirmar la selección.
1. Haga clic en **[!UICONTROL Crear]**. Un cuadro de diálogo confirma que se ha creado un nuevo folleto. Clic **[!UICONTROL Abrir]** para abrir el folleto en modo de edición.

   <!--![chlimage_1-106](assets/.png) -->

   También puede cerrar el cuadro de diálogo y desplazarse a la carpeta de la página Plantillas con la que comenzó para ver el folleto que ha creado. El tipo de material colateral aparece en la miniatura en la vista de tarjeta. Por ejemplo, en este caso, la palabra [!UICONTROL Folleto] se muestra en la miniatura.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## Editar un material colateral {#editing-a-collateral}

Puede editar un material colateral inmediatamente después de crearlo. Como alternativa, puede abrirlo desde el [!UICONTROL Plantillas] o la página de recursos.

1. Para abrir el material colateral para editarlo, siga uno de estos procedimientos:

   * Abra el material colateral (folleto en este caso) que creó en el paso 7 de [Crear un aval](/help/assets/asset-templates.md#creating-a-collateral).
   * En la página Plantillas, vaya a una carpeta en la que haya creado el material colateral y haga clic en [!UICONTROL Editar] acción rápida en la miniatura de un material colateral.
   * En la página de activos de garantía, haga clic en **[!UICONTROL Editar]** en la barra de herramientas.
   * Seleccione la garantía y haga clic en **[!UICONTROL Editar]** en la barra de herramientas.

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   El buscador de recursos y el editor de texto se muestran a la izquierda de la página. El editor de texto está abierto de forma predeterminada.

   Puede utilizar el editor de texto para modificar el texto que desea mostrar en el campo de texto. Puede modificar el tamaño, el estilo, el color y el tipo de fuente en el nivel de etiqueta.

   Con el buscador de recursos, puede examinar o buscar imágenes en [!DNL Experience Manager Assets] y reemplace las imágenes editables de la plantilla por imágenes de su elección.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   Los editables se muestran a la derecha. Para que un campo se pueda editar en [!DNL Experience Manager Assets], el campo correspondiente de la plantilla debe estar etiquetado en [!DNL InDesign]. En otras palabras, deben marcarse como editables en [!DNL InDesign].

   >[!NOTE]
   >
   >Asegúrese de que su [!DNL Experience Manager] la implementación está integrada con un [!DNL InDesign Server] para habilitar [!DNL Experience Manager Assets] para extraer datos de [!DNL InDesign] y ponerla a disposición para su edición. Para obtener más información, consulte [integración de Experience Manager Assets con InDesign Server](/help/assets/indesign.md).

1. Para modificar el texto de un campo editable, haga clic en el campo de texto de la lista de campos editables y edite el texto del campo.

   ![chlimage_1-111](assets/chlimage_1-316.png)

   Puede editar las propiedades del texto, por ejemplo, el estilo de fuente, el color y el tamaño, mediante las opciones proporcionadas.

1. Clic **[!UICONTROL Previsualizar]** para previsualizar los cambios de texto.

1. Para intercambiar una imagen, haga clic en **[!UICONTROL Buscador de recursos]** ![chlimage_1-113](assets/chlimage_1-318.png).

1. Seleccione el campo de imagen de la lista de campos editables y, a continuación, arrastre una imagen deseada del selector de recursos al campo editable.

   ![chlimage_1-114](assets/chlimage_1-319.png)

   También puede buscar imágenes mediante palabras clave, etiquetas y en función de su estado de publicación. Puede navegar por las [!DNL Experience Manager Assets] y vaya a la ubicación de la imagen deseada.

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. Clic **[!UICONTROL Previsualizar]** para previsualizar la imagen.
1. Para editar una página específica en un material colateral de varias páginas, utilice el navegador de páginas en la parte inferior.

1. Clic **[!UICONTROL Previsualizar]** en la barra de herramientas para previsualizar todos los cambios. Clic **[!UICONTROL Listo]** para guardar los cambios de edición en el material colateral.

   >[!NOTE]
   >
   >Las opciones Vista previa y Listo solo se activan cuando no falta ningún icono en los campos de imagen editables del material colateral. Si faltan iconos en el material colateral, es porque [!DNL Experience Manager] no puede resolver las imágenes en la [!DNL InDesign] plantilla. Normalmente, [!DNL Experience Manager] no puede resolver imágenes en los siguientes casos:
   >
   >* Las imágenes no están incrustadas en el subyacente [!DNL InDesign] plantilla.
   >* Las imágenes están vinculadas desde el sistema de archivos local.

   >
   >Para habilitar [!DNL Experience Manager] para resolver imágenes, haga lo siguiente:
   >
   >* Incrustar imágenes al crear [!DNL InDesign] plantillas (consulte [Acerca de los vínculos y los gráficos incrustados](https://helpx.adobe.com/indesign/using/graphics-links.html)).
   >* Montar [!DNL Experience Manager] al sistema de archivos local y, a continuación, asigne los iconos que faltan a los recursos existentes en [!DNL Experience Manager].

   >
   >Para obtener más información sobre cómo trabajar con [!DNL InDesign] documentos, consulte [prácticas recomendadas para trabajar con documentos de InDesign en Experience Manager](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. Para generar una representación del PDF para el folleto, seleccione la opción Acrobat en el cuadro de diálogo y, a continuación, haga clic en **[!UICONTROL Continuar]**.
1. El material colateral se crea en la carpeta con la que comenzó. Para ver las representaciones, abra el material colateral y elija **[!UICONTROL Representaciones]** de la lista GlobalNav.

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. Haga clic en la representación del PDF de la lista de representaciones para descargar el archivo del PDF. Abra el archivo del PDF para revisar el material colateral.

   ![chlimage_1-119](assets/chlimage_1-324.png)

## Combinar garantía {#merge-collateral}

1. En el [!DNL Experience Manager] clic de interfaz [!UICONTROL Assets] en la página Navegación.

1. En las opciones, elija **[!UICONTROL Plantillas]**.

1. Clic **[!UICONTROL Crear]** y elija **[!UICONTROL Combinar]** en el menú.

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. Desde el [!UICONTROL Combinación de plantillas] página, haga clic en **[!UICONTROL Combinar]** ![añadir recursos](assets/do-not-localize/assets_add_icon.png).

1. Navegue hasta la ubicación del material colateral que desee fusionar, haga clic en las miniaturas del material colateral que desee fusionar para seleccionarlas.

   ![chlimage_1-122](assets/chlimage_1-327.png)

   También puede buscar plantillas desde el cuadro Omnisearch.

   Puede navegar por las [!DNL Experience Manager Assets] repositorio o colecciones, y vaya a la ubicación de las plantillas deseadas y, a continuación, selecciónelas para combinarlas.

   Puede aplicar varios filtros para buscar las plantillas deseadas. Por ejemplo, puede buscar plantillas basadas en el tipo de archivo o en las etiquetas.

1. Clic **[!UICONTROL Siguiente]** en la barra de herramientas.
1. En el **[!UICONTROL Previsualizar y reordenar]** , reorganice las plantillas si es necesario y previsualice la selección de plantillas para combinar. A continuación, haga clic en **[!UICONTROL Siguiente]** en la barra de herramientas.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. En el [!UICONTROL Configurar plantilla] , especifique un nombre para el material complementario. Si lo desea, especifique las etiquetas que considere adecuadas. Si desea exportar la salida en formato de PDF, seleccione **[!UICONTROL Acrobat (.PDF)]**. De forma predeterminada, la garantía se exporta en JPG y [!DNL InDesign] formato. Para cambiar la miniatura de visualización del material colateral de varias páginas, haga clic en **[!UICONTROL Cambiar miniatura]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. Clic **[!UICONTROL Guardar]** y luego haga clic en **[!UICONTROL OK]** en el cuadro de diálogo para cerrarlo. El material colateral de varias páginas se crea en la carpeta con la que comenzó.

   >[!NOTE]
   >
   >No se puede editar un material colateral combinado posteriormente ni utilizarlo para crear otro material colateral.

## Prácticas recomendadas y limitaciones {#best-practices-limitations-tips}

* El [!DNL InDesign] editor en [!DNL Experience Manager] funciona a nivel de etiqueta y todo el texto de una sola etiqueta se considera una sola entidad. Para conservar el formato y los estilos del texto al editar, etiquete por separado cada párrafo (o texto con un estilo diferente).
