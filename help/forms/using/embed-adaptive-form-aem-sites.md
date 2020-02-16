---
title: Incrustar un formulario adaptable o una comunicación interactiva en la página de sitios de AEM
seo-title: Incrustar un formulario adaptable o una comunicación interactiva en la página de sitios de AEM
description: Puede incrustar formularios adaptables en páginas de sitios de AEM. Los usuarios pueden rellenar y enviar formularios sin salir de las páginas del sitio.
seo-description: Puede incrustar formularios adaptables en páginas de sitios de AEM. Los usuarios pueden rellenar y enviar formularios sin salir de las páginas del sitio.
uuid: 59b49e2f-6d95-42e5-b31e-fc40936c42d2
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
discoiquuid: 43362643-69cd-4006-a613-f998c79eeddc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Incrustar un formulario adaptable o una comunicación interactiva en la página de sitios de AEM {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

## Información general {#overview}

AEM Forms permite a los desarrolladores de formularios incrustar sin problemas formularios adaptables y comunicaciones interactivas en una página de AEM Sites o en una página web alojada fuera de AEM. El formulario adaptable incrustado y la comunicación interactiva son totalmente funcionales y los usuarios pueden rellenar y enviar el formulario sin salir de la página. Ayuda al usuario a permanecer en el contexto de otros elementos de la página web e interactuar simultáneamente con el formulario o la comunicación interactiva.

Para obtener información sobre la incrustación de un formulario adaptable en una página web externa, consulte [Incrustar formulario adaptable en una página](/help/forms/using/embed-adaptive-form-external-web-page.md)web externa.

En la página Sitios de AEM, puede agregar un formulario adaptable o una comunicación interactiva mediante:

* **[Contenedor de AEM Forms](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**AEM Forms proporciona un componente que puede agregar a las páginas del sitio. El componente Contenedor de AEM Forms permite incrustar un formulario adaptable y una comunicación interactiva.

* **[Navegador](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**de recursos Todos los formularios y las comunicaciones interactivas que cree estarán disponibles en Recursos. Puede arrastrar y soltar el formulario como recurso en la página.

## Requisitos previos {#prerequisites}

Para incrustar un formulario adaptable o una comunicación interactiva en una página de sitios de AEM que utilice una plantilla editable, asegúrese de que el componente Formulario AEM está configurado como un componente permitido en la plantilla asociada. Para obtener más información, consulte la sección **Política y propiedades (Contenedor de diseño)** en [Creación de plantillas](/help/sites-authoring/templates.md)de página.

En el caso de una página Sitios que utilice una plantilla estática, debe configurarla en el sistema de párrafos de la página del sitio. Consulte [Configuración de componentes en el modo Diseño](/help/sites-authoring/default-components-designmode.md) para obtener más información.

## Incrustación de un formulario adaptable o una comunicación interactiva {#af-component}

Para incrustar un formulario adaptable o una comunicación interactiva mediante el componente Contenedor de AEM Forms:

1. Abra la página Sitios de AEM, en modo de edición, en la que desea incrustar un formulario adaptable o una comunicación interactiva.
1. En el panel Navegador de componentes, arrastre y suelte el componente Contenedor de AEM Forms en la página.

   También puede buscar un formulario adaptable o una comunicación interactiva en el navegador de recursos y arrastrarlo y colocarlo en la página Sitios. Incrusta el formulario en un contenedor de AEM Forms.

   >[!NOTE]
   >
   >No se admiten varios componentes de contenedor de AEM Forms en una página.

1. Toque el componente AEM Forms Container incrustado en la página Sitios y, a continuación, toque ![settings_icon](assets/settings_icon.png) en la barra de acciones. Se abre el cuadro de diálogo **[!UICONTROL Editar contenedor]** de AEM Forms.
1. En el cuadro de diálogo Editar contenedor de AEM Forms, especifique lo siguiente.

   * **** Tipo de recurso: Seleccione el tipo de recurso que desea incrustar. Las opciones son formulario adaptable y comunicación interactiva
   * **Ruta** del recurso: Busque y seleccione el formulario adaptable o la comunicación interactiva que desea incrustar. Se rellena automáticamente si se ha soltado desde el navegador de recursos.
   * (Solo formulario adaptable) Envío **posterior**: Seleccione la acción que se activará al enviar el formulario. Puede elegir mostrar un mensaje de agradecimiento o una página de agradecimiento.

      * **Mensaje** de agradecimiento: Escriba un mensaje con el editor de texto enriquecido para mostrarlo en el envío del formulario. Esta opción solo está disponible cuando elige mostrar un mensaje de agradecimiento.
      * **Página** de agradecimiento: Explore y seleccione la página que desea mostrar al enviar el formulario. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
      * **Actualizar página al enviar**: Active esta opción para actualizar la página que contiene el formulario adaptable incrustado y mostrar la página de agradecimiento. De lo contrario, la página de agradecimiento sustituye el formulario adaptable en el contenedor de AEM Forms, sin actualizar la página. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
   * **Tema**: Seleccione un tema que defina el estilo para los componentes del formulario adaptable o la comunicación interactiva. El estilo incluye propiedades de apariencia como el estilo de fuente, el color de fondo, las dimensiones y la alineación.
   * **Altura**: Especifique la altura del contenedor. Déjelo en blanco para cambiar automáticamente el tamaño del contenedor.
   * **Biblioteca** del cliente de CSS: Especifique la ruta a una biblioteca de cliente CSS.


1. Guarde la configuración. El formulario adaptable o la comunicación interactiva ahora se incrustan en la página.

## Publicación de formularios adaptables integrados y comunicación interactiva {#publishing-embedded-adaptive-form-and-interactive-communication}

Analicemos los siguientes escenarios para publicar un recurso incrustado (formulario adaptable o comunicación interactiva) en la página de sitios de AEM:

* Si va a publicar la página de sitios de AEM por primera vez e incluye un formulario adaptable incrustado o una comunicación interactiva, publique la página de sitios y el recurso incrustado.
* Si solo ha modificado el formulario adaptable incrustado o la comunicación interactiva en una página del sitio publicada, publique el recurso original y los cambios se reflejarán en la página del sitio publicada. La página del sitio publicada incluye una referencia al recurso y no requiere volver a publicar la página.
* Si ha modificado la página Sitios y el formulario adaptable incrustado o la comunicación interactiva, vuelva a publicar la página Sitios y el recurso incrustado.

## Modificación del formulario adaptable incrustado y la comunicación interactiva {#modifying-embedded-adaptive-form-and-interactive-communication}

La página Sitios de AEM mantiene una referencia al formulario adaptable y a la comunicación interactiva en el contenedor de AEM Forms. Por lo tanto, todas las configuraciones y propiedades, como el tema, los estilos y la acción de envío, configuradas en el formulario adaptable original y la comunicación interactiva, se conservan en el formulario adaptable incrustado y en la comunicación interactiva.

Para modificar cualquier configuración o propiedad del formulario adaptable incrustado y la comunicación interactiva, realice una de las acciones siguientes.

* Abra el formulario original en formularios adaptables o comunicación interactiva en los editores respectivos y modifíquelo.
* Toque el formulario adaptable o la comunicación interactiva desde la página del sitio en modo de edición y, a continuación, toque **[!UICONTROL Editar en una ventana]** nueva. El formulario original se abre en modo de edición que puede modificar.

>[!NOTE]
>
>Los cambios realizados en el formulario adaptable original o en la comunicación interactiva se reflejan automáticamente en el formulario incrustado. Sin embargo, vuelva a publicar el formulario adaptable, la comunicación interactiva o la página del sitio para reflejar los cambios en la página publicada.

## Consideraciones y prácticas recomendadas {#considerations-and-best-practices}

Tenga en cuenta los siguientes puntos al incrustar formularios adaptables en páginas de sitios de AEM:

* El encabezado y el pie de página del formulario original no se incluyen en el formulario incrustado.
* Los borradores de usuario y los envíos de formularios incrustados son compatibles y visibles en las fichas Borradores y Formularios enviados del portal de formularios.
* La acción de envío configurada en el formulario original se conserva en el formulario incrustado.
* La segmentación de experiencias y las pruebas A/B configuradas en el formulario original no funcionan en el formulario incrustado. Sin embargo, puede utilizar la segmentación de experiencias en la página del sitio para presentar distintos formularios en función de los perfiles de usuario.
* Si Adobe Analytics está configurado para el formulario original, los datos de análisis del formulario incrustado se capturan en Adobe Analytics. Sin embargo, no está disponible en el informe de análisis de formularios.

