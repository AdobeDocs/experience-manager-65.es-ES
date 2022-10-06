---
title: Plantillas de recursos
description: Obtenga información sobre las plantillas de recursos en [!DNL Adobe Experience Manager Assets] y cómo usar plantillas de recursos para crear material publicitario de marketing.
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

Las plantillas de recursos son una clase especial de recursos que facilitan un reuso rápido del contenido con gran riqueza visual para medios digitales y de impresión. Una plantilla de recursos incluye dos partes, la sección de mensajería fija y la sección editable. La sección de mensajería fija puede contener contenido propio, como el logotipo de la marca y la información de copyright que está desactivada para la edición. La sección editable puede contener contenido visual y textual en campos que se pueden editar para personalizar la mensajería.

La flexibilidad para realizar ediciones limitadas mientras se asegura la señalización global hace que las plantillas de recursos sean componentes básicos ideales para una rápida adaptación y distribución del contenido como artefactos de contenido para diversas funciones. El redireccionamiento del contenido ayuda a reducir el coste de la administración de canales digitales e impresos y ofrece experiencias holísticas y coherentes en todos estos canales.

Como especialista en marketing, puede almacenar y administrar plantillas dentro de [!DNL Experience Manager Assets] y utilice una sola plantilla base para crear varias experiencias de impresión personalizadas con facilidad. Puede crear varios tipos de material publicitario de marketing, incluidos folletos, folletos, postales, tarjetas de visita, etc., para transmitir su mensaje de marketing a los clientes de forma lúcida. También puede ensamblar salidas de impresión de varias páginas a partir de salidas de impresión existentes o nuevas. Sobre todo, puede ofrecer simultáneamente experiencias digitales e impresas con facilidad para proporcionar una experiencia coherente e integrada a los usuarios.

Mientras que las plantillas de recursos son principalmente [!DNL Adobe InDesign] archivos, competencia en [!DNL Adobe InDesign] no es una barrera para la creación de artefactos estelares. No es necesario que asigne los campos de su [!DNL Adobe InDesign] plantilla con los campos del producto que necesite para crear catálogos. Puede editar las plantillas en modo WYSIWYG directamente en la interfaz web. Sin embargo, para [!DNL Adobe InDesign] para procesar los cambios de edición, primero debe configurar [!DNL Experience Manager Assets] para integrar con [!DNL Adobe InDesign Server].

La capacidad de edición [!DNL Adobe InDesign] las plantillas de la interfaz web ayudan a fomentar la buena colaboración entre el personal creativo y el personal de marketing. La mayor velocidad de contenido reduce el tiempo de salida al mercado para las garantías de marketing.

Puede lograr lo siguiente con las plantillas de recursos:

* Modifique los campos de plantilla editables desde la interfaz web.
* Controle el estilo básico del texto, por ejemplo el tamaño de fuente, el estilo y el tipo en el nivel de etiqueta.
* Cambiar imágenes dentro de la plantilla mediante el selector de contenido.
* Vista previa de las ediciones de plantillas.
* Combine varios archivos de plantilla para crear un artefacto de varias páginas.

Al elegir una plantilla para los activos de garantía, [!DNL Experience Manager Assets] crea una copia de la plantilla que puede editar. Se conserva la plantilla original, lo que garantiza que la señalización global permanezca intacta y se pueda reutilizar para garantizar la coherencia de la marca.

Puede exportar el archivo actualizado dentro de la carpeta principal en los formatos INDD, PDF o JPG. También puede descargar la salida en estos formatos en su sistema de archivos local.

## Creación de un colateral {#creating-a-collateral}

Considere un escenario en el que desee crear garantías digitales imprimibles, como folletos, folletos y publicidades para una próxima campaña, y compartirlas con tiendas de venta en todo el mundo. La creación de material colateral basado en una plantilla ayuda a ofrecer una experiencia de cliente unificada en todos los canales. Los diseñadores pueden crear las plantillas de campaña (una sola página o varias páginas) mediante una solución creativa, como [!DNL InDesign] y cargue las plantillas en [!DNL Experience Manager Assets] para usted. Antes de crear una garantía, haga que una o más plantillas INDD se carguen en y estén disponibles en [!DNL Experience Manager] por adelantado.

1. En [!DNL Experience Manager] clic en la interfaz [!UICONTROL Recursos].

1. En las opciones , elija **[!UICONTROL Plantillas]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. Haga clic en **[!UICONTROL Crear]** y, a continuación, elija el material que desea crear en el menú . Por ejemplo, elija **[!UICONTROL Folleto]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. Tener una o más plantillas INDD cargadas en y disponibles en [!DNL Experience Manager] por adelantado. Elija una plantilla para el folleto y haga clic en **[!UICONTROL Siguiente]**.
1. Especifique un nombre y una descripción opcional para el folleto.

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. (Opcional) Haga clic en **[!UICONTROL Etiquetas]** y seleccione una o varias etiquetas para el folleto. Haga clic en **[!UICONTROL Confirmar]** para confirmar la selección.
1. Haga clic en **[!UICONTROL Crear]**. Un cuadro de diálogo confirma que se crea un nuevo folleto. Haga clic en **[!UICONTROL Apertura]** para abrir el folleto en modo de edición.

   <!--![chlimage_1-106](assets/.png) -->

   Como alternativa, cierre el cuadro de diálogo y vaya a la carpeta de la página Plantillas con la que comenzó a trabajar para ver el folleto que ha creado. El tipo de garantía aparece en su miniatura en la vista de tarjeta. Por ejemplo, en este caso, la palabra [!UICONTROL Folleto] se muestra en la miniatura.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## Editar una garantía {#editing-a-collateral}

Puede editar un colateral inmediatamente después de crearlo. También puede abrirlo desde el [!UICONTROL Plantillas] o la página de recursos.

1. Para abrir el material secundario para editarlo, realice una de las siguientes acciones:

   * Abra el colateral (folleto en este caso) que creó en el paso 7 de [Creación de un colateral](/help/assets/asset-templates.md#creating-a-collateral).
   * En la página Plantillas , vaya a la carpeta en la que creó el material secundario y haga clic en el botón [!UICONTROL Editar] acción rápida en la miniatura de una garantía.
   * En la página de activos de la garantía, haga clic en **[!UICONTROL Editar]** en la barra de herramientas.
   * Seleccione el colateral y haga clic en **[!UICONTROL Editar]** en la barra de herramientas.

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   El buscador de recursos y el editor de texto se muestran a la izquierda de la página. El editor de texto está abierto de forma predeterminada.

   Puede utilizar el editor de texto para modificar el texto que desea que se muestre en el campo de texto. Puede modificar el tamaño de fuente, el estilo, el color y el tipo en el nivel de etiqueta.

   Con el buscador de recursos, puede examinar o buscar imágenes en [!DNL Experience Manager Assets] y reemplace las imágenes editables de la plantilla por las imágenes que elija.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   Los editables se muestran a la derecha. Para que un campo se pueda editar en [!DNL Experience Manager Assets], el campo correspondiente de la plantilla debe etiquetarse en [!DNL InDesign]. En otras palabras, deben marcarse como editables en [!DNL InDesign].

   >[!NOTE]
   >
   >Asegúrese de que su [!DNL Experience Manager] la implementación se integra con un [!DNL InDesign Server] para habilitar [!DNL Experience Manager Assets] para extraer datos de [!DNL InDesign] y haga que esté disponible para edición. Para obtener más información, consulte [integrar Experience Manager Assets con InDesign Server](/help/assets/indesign.md).

1. Para modificar el texto de un campo editable, haga clic en el campo de texto de la lista de campos editables y edite el texto en el campo.

   ![chlimage_1-111](assets/chlimage_1-316.png)

   Puede editar las propiedades del texto, por ejemplo el estilo de fuente, el color y el tamaño, utilizando las opciones proporcionadas.

1. Haga clic en **[!UICONTROL Vista previa]** para obtener una vista previa de los cambios de texto.

1. Para intercambiar una imagen, haga clic en el botón **[!UICONTROL Buscador de recursos]** ![chlimage_1-113](assets/chlimage_1-318.png).

1. Seleccione el campo de imagen de la lista de campos editables y, a continuación, arrastre una imagen desde el selector de recursos al campo editable.

   ![chlimage_1-114](assets/chlimage_1-319.png)

   También puede buscar imágenes utilizando palabras clave, etiquetas y según su estado de publicación. Puede navegar por el [!DNL Experience Manager Assets] y navegue hasta la ubicación de la imagen deseada.

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. Haga clic en **[!UICONTROL Vista previa]** para previsualizar la imagen.
1. Para editar una página específica en un material de varias páginas, utilice el navegador de páginas de la parte inferior.

1. Haga clic en **[!UICONTROL Vista previa]** en la barra de herramientas para obtener una vista previa de todos los cambios. Haga clic en **[!UICONTROL Listo]** para guardar los cambios de edición en el material.

   >[!NOTE]
   >
   >Las opciones Vista previa y Listo solo se activan cuando los campos de imagen editables del material no tienen iconos que falten. Si faltan iconos en el colateral, es porque [!DNL Experience Manager] no puede resolver las imágenes en la [!DNL InDesign] plantilla. Normalmente, [!DNL Experience Manager] no puede resolver imágenes en los siguientes casos:
   >
   >* Las imágenes no están incrustadas en el subyacente [!DNL InDesign] plantilla.
   >* Las imágenes están vinculadas desde el sistema de archivos local.

   >
   >Para habilitar [!DNL Experience Manager] para resolver las imágenes, haga lo siguiente:
   >
   >* Incrustar imágenes al crear [!DNL InDesign] plantillas (consulte [Acerca de los vínculos y los gráficos incrustados](https://helpx.adobe.com/indesign/using/graphics-links.html)).
   >* Monte [!DNL Experience Manager] al sistema de archivos local y, a continuación, asigne los iconos que faltan con los recursos existentes en [!DNL Experience Manager].

   >
   >Para obtener más información, consulte [!DNL InDesign] documentos, consulte [prácticas recomendadas para trabajar con documentos de InDesign en Experience Manager](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. Para generar una representación de PDF para el folleto, seleccione la opción Acrobat en el cuadro de diálogo y haga clic en **[!UICONTROL Continuar]**.
1. El material colateral se crea en la carpeta con la que comenzó. Para ver las representaciones, abra la garantía y elija **[!UICONTROL Representaciones]** de la lista de navegación global.

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. Haga clic en la representación del PDF en la lista de representaciones para descargar el archivo del PDF. Abra el archivo del PDF para revisar el colateral.

   ![chlimage_1-119](assets/chlimage_1-324.png)

## Combinar material colateral {#merge-collateral}

1. En el [!DNL Experience Manager] clic en la interfaz [!UICONTROL Recursos] en la página Navegación .

1. En las opciones , elija **[!UICONTROL Plantillas]**.

1. Haga clic en **[!UICONTROL Crear]** y elija **[!UICONTROL Combinar]** del menú .

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. En el [!UICONTROL Combinación de plantillas] página, haga clic en **[!UICONTROL Combinar]** ![agregar recursos](assets/do-not-localize/assets_add_icon.png).

1. Vaya a la ubicación del material que desea combinar, haga clic en las miniaturas del material que desea combinar para seleccionarlo.

   ![chlimage_1-122](assets/chlimage_1-327.png)

   También puede buscar plantillas en el cuadro Omnisearch .

   Puede navegar por el [!DNL Experience Manager Assets] repositorio o colecciones, desplácese a la ubicación de las plantillas deseadas y selecciónelas para fusionarlas.

   Puede aplicar varios filtros para buscar en las plantillas que desee. Por ejemplo, puede buscar plantillas basadas en el tipo de archivo o en etiquetas.

1. Haga clic en **[!UICONTROL Siguiente]** en la barra de herramientas.
1. En el **[!UICONTROL Vista previa y reordenación]** , reorganice las plantillas si es necesario y previsualice la selección de plantillas que desea combinar. A continuación, haga clic en **[!UICONTROL Siguiente]** en la barra de herramientas.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. En el [!UICONTROL Configurar plantilla] , especifique un nombre para el colateral. De forma opcional, especifique las etiquetas que considere adecuadas. Si desea exportar la salida en formato de PDF, seleccione **[!UICONTROL Acrobat (.PDF)]**. De forma predeterminada, la garantía se exporta en JPG y [!DNL InDesign] formato. Para cambiar la miniatura de visualización del material de varias páginas, haga clic en **[!UICONTROL Cambiar miniatura]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. Haga clic en **[!UICONTROL Guardar]** y haga clic en **[!UICONTROL OK]** en el cuadro de diálogo para cerrar el cuadro de diálogo. El material colateral de varias páginas se crea en la carpeta con la que comenzó.

   >[!NOTE]
   >
   >No se puede editar un material combinado posteriormente ni utilizarlo para crear otro material colateral.

## Prácticas recomendadas y limitaciones {#best-practices-limitations-tips}

* La variable [!DNL InDesign] editor en [!DNL Experience Manager] funciona en el nivel de etiqueta y todo el texto de una sola etiqueta se considera una sola entidad. Para conservar el formato y los estilos de texto durante la edición, etiquete cada párrafo (o texto con un estilo diferente) por separado.
