---
title: Incrustar un formulario adaptable o una comunicación interactiva en una aplicación de página única de AEM Sites
seo-title: Incrustar formularios adaptables o comunicaciones interactivas en páginas de sitios de AEM
description: Incruste formularios adaptables o comunicaciones interactivas en páginas de sitios de AEM. Los usuarios pueden rellenar y enviar formularios sin salir de la página Sitios.
seo-description: Puede incrustar formularios adaptables o comunicación interactiva en páginas de sitios de AEM. Los usuarios pueden rellenar y enviar formularios sin salir de la página Sitios.
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
translation-type: tm+mt
source-git-commit: d12d35bf8355d3069071523427a7794b88c09b13

---


# Incrustar un formulario adaptable o una comunicación interactiva en una aplicación de página única de AEM Sites{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## Información general {#overview}

AEM Forms permite a los desarrolladores de formularios integrar sin problemas formularios adaptables y comunicaciones interactivas en una aplicación de una sola página de AEM Sites (SPA). El formulario adaptable incrustado y la comunicación interactiva son totalmente funcionales y los usuarios pueden rellenar y enviar el formulario sin salir de la página. Ayuda al usuario a permanecer en el contexto de otros elementos de la página web e interactuar simultáneamente con el formulario adaptable o la comunicación interactiva.

En la aplicación de una sola página de AEM Sites, puede agregar un formulario adaptable o Comunicación interactiva mediante el componente [Contenedor de SPA de](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[AEM Forms.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) Es un componente de AEM Forms para los SPA de AEM Sites que puede agregar a la página Sitios.

Para obtener información sobre la incrustación de un formulario adaptable en sitios AEM que no sean SPA, consulte [Incrustar un formulario adaptable o comunicación interactiva en la página](/help/forms/using/embed-adaptive-form-aem-sites.md)Sitios de AEM.

## Requisitos previos {#prerequisites}

Para incrustar un formulario adaptable o una comunicación interactiva en un SPA de sitios de AEM mediante el componente Contenedor de SPA de AEM Forms, asegúrese de haber instalado:

* Kit de desarrollo Java SE 8 o posterior
* Apache Maven 3.3.1 o posterior
* Instancia de creación de AEM
* [Paquete](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) de complemento de AEM Forms 6.4.2 en la instancia de creación

## Instalación del componente de contenedor de SPA de AEM Forms {#install-aem-forms-spa-container-component}

Ejecute los siguientes pasos para instalar el componente Contenedor de AEM Forms SPA:

1. [Clona o descarga el componente AEM Forms para SPA](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. Instale el componente AEM Forms para SPA. Las instrucciones para instalar el componente están disponibles en el archivo [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component) .

   El componente incluye un componente [React de](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) muestra que puede utilizarse para integrar el componente de contenedor SPA con un proyecto SPA basado en React.

1. [Clonar o descargar un proyecto](https://github.com/adobe/aem-sample-we-retail-journal)SPA basado en React.
1. Integre el componente contenedor SPA con un proyecto SPA basado en React siguiendo las instrucciones disponibles en el archivo [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) .

   Después de instalar el componente Contenedor de AEM Forms SPA e integrar el componente con un proyecto de SPA basado en React, puede incrustar formularios adaptables y comunicaciones interactivas en la página Sitios de AEM.

## Incrustar un formulario adaptable o una comunicación interactiva {#af-component}

Para incrustar un formulario adaptable o una comunicación interactiva con el componente Contenedor de AEM Forms para SPA:

1. Abra la página de sitios de AEM, en modo de edición, en la que desea incrustar un formulario adaptable o una comunicación interactiva.
1. Inserte el componente Formulario **AEM para SPA** en la página con cualquiera de las siguientes opciones:

   * Toque el contenedor de diseño en la página Sitios, toque **+** y seleccione el componente Formulario **AEM para SPA** .

   * En el panel Navegador de componentes, arrastre y suelte el componente Formulario **AEM para SPA** en la página.
   * Busque un formulario adaptable o una comunicación interactiva en el navegador de recursos y arrástrelo y suéltelo en la página Sitios. Incrusta el formulario en un contenedor de componentes de AEM Forms para SPA.
   >[!NOTE]
   >
   >No se admite el procesamiento de varios componentes de contenedor SPA de AEM Forms en una página. Puede tener varios contenedores SPA de AEM Forms en una página, pero solo se procesa un componente a la vez. Asegúrese de que solo un componente esté visible en una página para evitar discrepancias.

1. Puntee en el componente Contenedor de AEM Forms incrustado en la página Sitios y, a continuación, toque ![settings_icon](assets/settings_icon.png) en la barra de acciones. Se abre el cuadro de diálogo **Editar contenedor** SPA de AEM Forms.
1. En el cuadro de diálogo **Editar contenedor** de AEM Forms, especifique lo siguiente:

   * **** Tipo de recurso: Seleccione el tipo de recurso que desea incrustar. Las opciones son **Formulario** adaptable y Comunicación **interactiva**

   * **Ruta** del recurso: Busque y seleccione el formulario adaptable o la comunicación interactiva que desea incrustar. El campo se rellena automáticamente si se inserta un formulario adaptable o Comunicación interactiva mediante el navegador de recursos.
   * **Canal** (solo comunicación interactiva): Seleccione el tipo de canal interactivo que desea incrustar. Las opciones son Canal **web** y Canal **de impresión**.

   * **Tema**: Seleccione un tema que defina el estilo para los componentes de su formulario adaptable o Comunicación interactiva. El estilo incluye propiedades de apariencia como el estilo de fuente, el color de fondo, las dimensiones y la alineación.

1. Toque ![](assets/done_icon.png) para guardar la configuración. El formulario adaptable o Comunicación interactiva ahora está incrustado en la página.

## Publicación de formularios adaptables incrustados y comunicación interactiva {#publish-embedded-adaptive-form-and-interactive-communication}

Considere los siguientes escenarios para publicar un recurso incrustado (formulario adaptable o Comunicación interactiva) en la página Sitios de AEM:

* Si está publicando la página Sitios de AEM por primera vez e incluye un formulario adaptable incrustado o Comunicación interactiva, publique la página Sitios y el recurso incrustado.
* Si solo ha modificado el formulario adaptable incrustado o la Comunicación interactiva en una página Sitios publicada, publique el recurso original y los cambios se reflejarán en la página Sitios publicada. La página Sitios publicada incluye una referencia al recurso y no requiere volver a publicar la página.
* Si ha modificado la página Sitios y el formulario adaptable incrustado o Comunicación interactiva, vuelva a publicar la página Sitios y el recurso incrustado.

## Modificar el formulario adaptable incrustado y la comunicación interactiva {#modify-embedded-adaptive-form-and-interactive-communication}

La página Sitios de AEM mantiene una referencia al formulario adaptable y a la comunicación interactiva en el contenedor de AEM Forms. Por lo tanto, todas las configuraciones y propiedades, como el tema, los estilos y la acción de envío, configuradas en el formulario adaptable original y la comunicación interactiva, se conservan en el formulario adaptable incrustado y en la comunicación interactiva.

Para modificar cualquier configuración o propiedad del formulario adaptable incrustado y Comunicación interactiva, realice una de las siguientes acciones.

* Abra el formulario original en formularios adaptables o Comunicación interactiva en los editores respectivos y modifíquelo.
* Toque el formulario adaptable o Comunicación interactiva desde la página Sitios en modo de edición y, a continuación, toque **Editar en una ventana** nueva. El formulario original se abre en modo de edición.

## Consideraciones y prácticas recomendadas {#considerations-and-best-practices}

Tenga en cuenta los siguientes puntos al incrustar formularios adaptables en páginas de sitios de AEM:

* El encabezado y el pie de página del formulario original no se incluyen en el formulario incrustado.
* Los borradores de usuario y los envíos de formularios incrustados son compatibles y visibles en las fichas Borradores y Formularios enviados del portal de formularios.
* La acción de envío configurada en el formulario original se conserva en el formulario incrustado.
* La segmentación de experiencias y las pruebas A/B configuradas en el formulario original no funcionan en el formulario incrustado. Sin embargo, puede utilizar la segmentación de experiencias en la página Sitios para presentar distintos formularios en función de los perfiles de usuario.
* Si Adobe Analytics está configurado para el formulario original, los datos de análisis del formulario incrustado se capturan en Adobe Analytics. Sin embargo, no está disponible en el informe de análisis de formularios.

