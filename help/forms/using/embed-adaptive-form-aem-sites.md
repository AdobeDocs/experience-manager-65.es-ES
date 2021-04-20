---
title: Incrustar un formulario adaptable o una comunicación interactiva en AEM página de sitios
seo-title: Incrustar un formulario adaptable o una comunicación interactiva en AEM página de sitios
description: Puede incrustar formularios adaptables en páginas AEM sitios. Los usuarios pueden rellenar y enviar formularios sin salir de las páginas del sitio.
seo-description: Puede incrustar formularios adaptables en páginas AEM sitios. Los usuarios pueden rellenar y enviar formularios sin salir de las páginas del sitio.
uuid: 59b49e2f-6d95-42e5-b31e-fc40936c42d2
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author, interactive-communications
discoiquuid: 43362643-69cd-4006-a613-f998c79eeddc
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 1%

---


# Incruste un formulario adaptable o una comunicación interactiva en AEM página de sitios {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

## Información general {#overview}

AEM Forms permite a los desarrolladores de formularios incrustar sin problemas formularios adaptables y comunicaciones interactivas en una página de AEM Sites o una página web alojada fuera de AEM. El formulario adaptable integrado y la comunicación interactiva son totalmente funcionales y los usuarios pueden rellenar y enviar el formulario sin salir de la página. Ayuda al usuario a permanecer en el contexto de otros elementos de la página web e interactuar simultáneamente con el formulario o la comunicación interactiva.

Para obtener información sobre la incrustación de un formulario adaptable en una página web externa, consulte [Incrustar formulario adaptable en una página web externa](/help/forms/using/embed-adaptive-form-external-web-page.md).

En la página AEM Sites, puede añadir un formulario adaptable o una comunicación interactiva mediante:

* **[Componente Contenedor de AEM Forms](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**
AEM Forms proporciona un componente que puede agregar a las páginas del sitio. El componente Contenedor de AEM Forms le permite incrustar un formulario adaptable y una comunicación interactiva.

* **[Navegador de](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
recursosTodos los formularios y las comunicaciones interactivas que cree están disponibles en Assets. Puede arrastrar y soltar el formulario como un recurso en la página.

## Requisitos previos {#prerequisites}

Para incrustar un formulario adaptable o una comunicación interactiva en una página de sitios AEM que utilice una plantilla editable, asegúrese de que el componente AEM Formulario esté configurado como un componente permitido en la plantilla asociada. Para obtener más información, consulte la sección **Política y propiedades (contenedor de diseño)** en [Creación de plantillas de página](/help/sites-authoring/templates.md).

En el caso de una página Sitios que use una plantilla estática, debe configurarla en el sistema de párrafos de la página del sitio. Consulte [Configuración de componentes en el modo Diseño](/help/sites-authoring/default-components-designmode.md) para obtener más información.

## Incrustación de un formulario adaptable o comunicación interactiva {#af-component}

Para incrustar un formulario adaptable o una comunicación interactiva mediante el componente Contenedor de AEM Forms:

1. Abra la página AEM sitios en modo de edición, en la que desea incrustar un formulario adaptable o una comunicación interactiva.
1. En el panel Navegador de componentes , arrastre y suelte el componente Contenedor de AEM Forms en la página.

   También puede buscar un formulario adaptable o una comunicación interactiva en el navegador Recursos y arrastrarlo y colocarlo en la página Sitios . Incrusta el formulario en un contenedor de AEM Forms.

   >[!NOTE]
   >
   >No se admiten varios componentes de contenedor de AEM Forms en una página.

1. Pulse el componente Contenedor de AEM Forms incrustado en la página Sitios y, a continuación, pulse ![settings_icon](assets/settings_icon.png) en la barra de acciones. Se abre el cuadro de diálogo **[!UICONTROL Editar contenedor de AEM Forms]**.
1. En el cuadro de diálogo Editar contenedor de AEM Forms , especifique lo siguiente.

   * **Tipo de recurso:** seleccione el tipo de recurso que desea incrustar. Las opciones son forma adaptable y comunicación interactiva
   * **Ruta** del recurso: Busque y seleccione el formulario adaptable o la comunicación interactiva que desea incrustar. Se rellena automáticamente si se ha soltado desde el explorador de Assets.
   * (Solo formulario adaptable) **Publicar envío**: Seleccione la acción a déclencheur en el envío del formulario. Puede elegir mostrar un mensaje de agradecimiento o una página de agradecimiento.

      * **Mensaje** de agradecimiento: Escriba un mensaje con el editor de texto enriquecido para mostrarlo en el envío del formulario. Esta opción solo está disponible cuando elige mostrar un mensaje de agradecimiento.
      * **Página de agradecimiento**: Busque y seleccione la página que desea mostrar en el envío del formulario. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
      * **Actualizar página en envío**: Habilite para actualizar la página que contiene el formulario adaptable incrustado para mostrar la página de agradecimiento. De lo contrario, la página de agradecimiento sustituye al formulario adaptable en el contenedor de AEM Forms, sin actualizar la página. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
   * **Tema**: Seleccione un tema que defina el estilo para los componentes de su formulario adaptable o comunicación interactiva. El estilo incluye propiedades de aspecto como el estilo de fuente, el color de fondo, las dimensiones y la alineación.
   * **Altura**: Especifique la altura del contenedor. Déjelo en blanco para cambiar automáticamente el tamaño del contenedor.
   * **Biblioteca** de cliente CSS: Especifique la ruta a una biblioteca de cliente CSS.


1. Guarde la configuración. El formulario adaptable o la comunicación interactiva están incrustados en la página.

## Publicación de formularios adaptables incrustados y comunicación interactiva {#publishing-embedded-adaptive-form-and-interactive-communication}

Consideremos los siguientes escenarios para publicar un recurso incrustado (formulario adaptable o comunicación interactiva) en AEM página de sitios:

* Si publica la página de AEM sitios por primera vez e incluye un formulario adaptable incrustado o una comunicación interactiva, publique la página de sitios y el recurso incrustado.
* Si ha modificado únicamente el formulario adaptable incrustado o la comunicación interactiva en una página del sitio publicada, publique el recurso original y los cambios se reflejarán en la página del sitio publicada. La página del sitio publicada incluye una referencia al recurso y no requiere que se vuelva a publicar la página.
* Si ha modificado la página Sitios y el formulario adaptable o la comunicación interactiva incrustados, vuelva a publicar la página Sitios y el recurso incrustado.

## Modificación del formulario adaptable incrustado y la comunicación interactiva {#modifying-embedded-adaptive-form-and-interactive-communication}

AEM página sitios mantiene una referencia al formulario adaptable y la comunicación interactiva en el contenedor de AEM Forms. Por lo tanto, todas las configuraciones y propiedades, como el tema, los estilos y la acción de envío, configuradas en el formulario adaptable original y la comunicación interactiva se conservan en el formulario adaptable incrustado y en la comunicación interactiva.

Para modificar cualquier configuración o propiedad del formulario adaptable incrustado y la comunicación interactiva, realice una de las siguientes acciones:

* Abra el formulario original en formularios adaptables o comunicación interactiva en los editores respectivos y modifíquelo.
* Pulse el formulario adaptable o la comunicación interactiva desde la página del sitio en modo de edición y, a continuación, pulse **[!UICONTROL Editar en una nueva ventana]**. El formulario original se abre en modo de edición que puede modificar.

>[!NOTE]
>
>Los cambios realizados en el formulario adaptable original o en la comunicación interactiva se reflejan automáticamente en el formulario incrustado. Sin embargo, vuelva a publicar el formulario adaptable, la comunicación interactiva o la página del sitio para reflejar los cambios en la página publicada.

## Consideraciones y prácticas recomendadas {#considerations-and-best-practices}

Tenga en cuenta los siguientes puntos al incrustar formularios adaptables en páginas AEM sitios:

* El encabezado y pie de página del formulario original no se incluyen en el formulario incrustado.
* Los borradores de usuario y los envíos de formularios incrustados son compatibles y visibles en las fichas Borradores y Forms enviado del portal de formularios.
* La acción de envío configurada en el formulario original se conserva en el formulario incrustado.
* La segmentación de experiencias y las pruebas A/B configuradas en el formulario original no funcionan en el formulario incrustado. Sin embargo, puede utilizar la segmentación de experiencias en la página Sitios para presentar distintos formularios basados en perfiles de usuario.
* Si Adobe Analytics está configurado para el formulario original, los datos de análisis del formulario incrustado se capturan en Adobe Analytics. Sin embargo, no está disponible en el informe de análisis de formularios.

