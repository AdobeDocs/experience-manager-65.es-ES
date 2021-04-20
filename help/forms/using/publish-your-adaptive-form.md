---
title: '"Tutorial: Publicar el formulario adaptable"'
seo-title: '"Tutorial: Publicar el formulario adaptable"'
description: Publique el formulario adaptable como página AEM, incruste el formulario en una página de AEM Sites o incruste el formulario adaptable en una página web externa
seo-description: Publique el formulario adaptable como página AEM, incruste el formulario en una página de AEM Sites o incruste el formulario adaptable en una página web externa
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 2%

---


# Tutorial: Publicar el formulario adaptable {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

Este tutorial es un paso de la serie [Create Your First Adaptive Form](https://helpx.adobe.com/es/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). Se recomienda seguir la serie en secuencia cronológica para comprender, realizar y demostrar el caso de uso completo del tutorial.

Una vez que el formulario adaptable esté listo, puede publicarlo para que esté disponible para los usuarios finales. Los usuarios finales pueden abrir el formulario publicado en cualquier dispositivo y navegador de Internet. Cuando se publica un formulario adaptable, el formulario y el contenido relacionado se copian de una instancia de autor AEM a una instancia de publicación AEM. El formulario está disponible para el usuario final a través de la instancia de publicación.

Tiene los siguientes métodos para publicar un formulario adaptable:

* [Publicar el formulario adaptable como una página AEM](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Incrustar el formulario adaptable en una página de AEM Sites](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Incruste el formulario adaptable en una página web externa (una página web que no sea AEM alojada fuera de AEM)](../../forms/using/publish-your-adaptive-form.md)

## Antes de comenzar {#before-you-start}

* **[Configure una instancia](https://helpx.adobe.com/es/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)** de publicación de AEM Forms: La instancia de publicación es una instancia pública de AEM que se  [!DNL Forms] ejecuta en modo de publicación. En un entorno de producción, la instancia de publicación está fuera del cortafuegos de la organización.
* **[Configurar la replicación y la replicación](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)** inversa: La replicación copia el contenido de la instancia de autor en una instancia de publicación y devuelve los datos introducidos por el usuario (por ejemplo, los datos de entrada de formulario) de la instancia de publicación a la instancia de autor.

## Publicar el formulario adaptable como una página AEM {#publish-the-adaptive-form-as-an-aem-page}

Cuando el formulario adaptable se publica como una página AEM, toda la página web contiene solo un formulario publicado. Puede utilizar la dirección URL del formulario adaptable para vincularlo desde otra página web. Para publicar el formulario adaptable **Shipping-address-add-update-form** como una página AEM:

1. Inicie sesión en AEM instancia de autor [!DNL Forms] y busque el formulario adaptable Shipping-address-add-update-form en la interfaz de usuario de AEM [!DNL Forms].
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Seleccione el formulario adaptable Shipping-address-add-update-form y pulse **[!UICONTROL Publicar]**. Se muestra un cuadro de diálogo que contiene recursos relacionados con el formulario adaptable. Toque **[!UICONTROL Publicar]**. El formulario adaptable se publica y aparece un cuadro de diálogo de éxito.
1. Abra el formulario en la instancia de publicación. El formulario está disponible para que el usuario final lo rellene y lo envíe.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Incrustar el formulario adaptable en una página de AEM Sites {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] permite a los desarrolladores de formularios incrustar formularios adaptables sin problemas en una página AEM [!DNL Sites]. El formulario adaptable integrado es totalmente funcional y los usuarios pueden rellenar y enviar el formulario sin salir de la página. Ayuda al usuario a permanecer en el contexto de otros elementos de la página web e interactuar simultáneamente con el formulario.

AEM [!DNL Forms] proporciona un componente, AEM [!DNL Forms] Contenedor, para integrar un formulario adaptable en una página AEM [!DNL Sites]. De forma predeterminada, el componente no está visible en AEM contenedor [!DNL Sites]. Realice los siguientes pasos para habilitar el componente Contenedor de AEM [!DNL Forms] e incrustar el formulario adaptable en una página de AEM [!DNL Sites]:

1. Cree y abra una página en el sitio de We.Retail para editarla. Por ejemplo, [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). El formulario adaptable está incrustado en la página [!DNL Sites].

   También puede incrustar el formulario adaptable en una página de We.Retail [!DNL Site's] existente. Por ejemplo, la página ABOUT US [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Le ahorra tiempo para crear una página. Los pasos siguientes utilizan la página recién creada.

   El sitio de We.Retail se envía con AEM. Si no tiene instalado el sitio de We.Retail, consulte [Implementación de referencia de We.Retail](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) para instalar el sitio.

1. Pulse ![properties](assets/properties.png) en la información de página y seleccione la opción **[!UICONTROL Editar plantilla]** en la página del sitio de We.Retail recién creada. La plantilla de la página se abre en una nueva pestaña del explorador.
1. Pulse dentro del cuadro **[!UICONTROL contenedor de diseño]** y pulse ![administración de fuentes](assets/feedmanagement.png). En la pestaña **[!UICONTROL Componentes permitidos]**, expanda el acordeón **[!UICONTROL General]**, seleccione la opción **[!UICONTROL AEM Formulario]** y pulse ![save_icon](assets/save_icon.svg). El componente Contenedor de AEM [!DNL Forms] está habilitado para la página.

1. Abra la pestaña del explorador que contiene AEM página [!DNL Sites] abierta en el paso 1. Pulse el cuadro **[!UICONTROL Arrastrar componentes aquí]** y pulse **+.** En el cuadro  **[!UICONTROL Insertar nuevo]** componente, pulse  **[!UICONTROL AEM formulario]**. El componente **[!UICONTROL Contenedor de AEM Forms]** se agrega a la página.
1. Pulse el componente **[!UICONTROL Contenedor de AEM Forms]** y pulse ![configure-icon](assets/configure-icon.svg). Aparece un cuadro de diálogo con propiedades de AEM [!DNL Forms] Contenedor. En el campo **[!UICONTROL Asset Path]**, busque y seleccione el formulario adaptable Shipping-address-add-update-form. Pulse ![save_icon](assets/save_icon.svg). El formulario adaptable está incrustado en la página .
1. Publique el formulario adaptable y la página [!DNL Sites]. Tenga en cuenta lo siguiente:

   * Si publica la página AEM [!DNL Sites] por primera vez e incluye un formulario incrustado, publique la página [!DNL Sites] y el formulario incrustado.
   * Si solo modifica el formulario incrustado en una página de sitio publicada, publique el formulario original y los cambios se reflejarán en la página del sitio publicada. La página del sitio publicada incluye una referencia al formulario y no requiere que se vuelva a publicar la página.
   * Si modifica la página [!DNL Sites] y el formulario incrustado, vuelva a publicar la página [!DNL Sites] y el formulario.

      ![embed-in-aem-sites](assets/embed-in-aem-sites.png)
   Formulario de cambio de dirección de envío y facturación agregado a una página de AEM [!DNL Sites].

## Incrustar el formulario adaptable en una página web externa {#embed-the-adaptive-form-in-an-external-webpage}

Puede incrustar un formulario adaptable en una página web externa (una página web que no sea AEM y que esté alojada fuera de AEM) insertando algunas líneas de JavaScript en la página web externa. El código JavaScript envía una solicitud HTTP al servidor AEM [!DNL Forms] para el formulario adaptable y los recursos relacionados, y agrega el formulario adaptable a la página web. Para ver los pasos detallados, consulte [integrar el formulario adaptable en una página web externa](/help/forms/using/embed-adaptive-form-external-web-page.md).
