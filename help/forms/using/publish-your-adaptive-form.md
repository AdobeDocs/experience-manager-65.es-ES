---
title: '"Tutorial: Publicar el formulario adaptable"'
seo-title: '"Tutorial: Publicar el formulario adaptable"'
description: Publique el formulario adaptable como una página de AEM, incruste el formulario en una página de AEM Sites o incruste el formulario adaptable en una página web externa
seo-description: Publique el formulario adaptable como una página de AEM, incruste el formulario en una página de AEM Sites o incruste el formulario adaptable en una página web externa
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
translation-type: tm+mt
source-git-commit: 1a816672b3e97346f5a7a984fcb4dc0df1a5b0da
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 1%

---


# Tutorial: Publicar el formulario adaptable {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

Este tutorial es un paso en la serie [Crear su primer formulario adaptable](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). Se recomienda seguir la serie en secuencia cronológica para comprender, realizar y demostrar el caso de uso completo del tutorial.

Una vez que el formulario adaptable esté listo, puede publicarlo para que esté disponible para los usuarios finales. Los usuarios finales pueden abrir el formulario publicado en cualquier dispositivo y navegador de Internet. Cuando se publica un formulario adaptable, el formulario y el contenido relacionado se copian de una instancia de autor AEM a una instancia de publicación AEM. El formulario se pone a disposición del usuario final a través de la instancia de publicación.

Tiene los siguientes métodos para publicar un formulario adaptable:

* [Publicar el formulario adaptable como una página AEM](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Incrustar el formulario adaptable en una página de AEM Sites](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Incrustar el formulario adaptable en una página web externa (una página web no AEM alojada fuera de AEM)](../../forms/using/publish-your-adaptive-form.md)

## Antes de comenzar {#before-you-start}

* **[Configure una instancia](https://helpx.adobe.com/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)** de publicación de AEM Forms: La instancia de publicación es una instancia pública de AEM  [!DNL Forms] ejecución en modo de publicación. En un entorno de producción, la instancia de publicación está fuera del servidor de seguridad de la organización.
* **[Configure la replicación y la replicación](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)** inversa: La replicación copia el contenido de la instancia de autor en una instancia de publicación y devuelve los datos introducidos por el usuario (por ejemplo, los datos introducidos en el formulario) desde la instancia de publicación a la instancia de autor.

## Publicar el formulario adaptable como una página AEM {#publish-the-adaptive-form-as-an-aem-page}

Cuando el formulario adaptable se publica como una página de AEM, toda la página web contiene solo un formulario publicado. Puede utilizar la dirección URL del formulario adaptable para vincularlo desde otra página web. Para publicar el formulario adaptable **Shipping-address-add-update-form** como una página AEM:

1. Inicie sesión en AEM instancia de creación [!DNL Forms] y busque el formulario adaptable Shipping-address-add-update-form en la interfaz de usuario de AEM [!DNL Forms].
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Seleccione el formulario adaptable Shipping-address-add-update-form y toque **[!UICONTROL Publicar]**. Se muestra un cuadro de diálogo que contiene recursos relacionados con el formulario adaptable. Toque **[!UICONTROL Publicar]**. Se publica el formulario adaptable y aparece un cuadro de diálogo de éxito.
1. Abra el formulario en la instancia de publicación. El formulario está disponible para que el usuario final lo rellene y lo envíe.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Incrustar el formulario adaptable en una página de AEM Sites {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] permite que los desarrolladores de formularios incorporen formularios adaptables de forma transparente en una página AEM [!DNL Sites]. El formulario adaptable incrustado es totalmente funcional y los usuarios pueden rellenar y enviar el formulario sin salir de la página. Ayuda al usuario a permanecer en el contexto de otros elementos de la página web e interactuar simultáneamente con el formulario.

AEM [!DNL Forms] proporciona un componente, AEM [!DNL Forms] Contenedor, para incrustar un formulario adaptable en una página AEM [!DNL Sites]. De forma predeterminada, el componente no está visible en AEM contenedor [!DNL Sites]. Realice los siguientes pasos para habilitar el componente de Contenedor AEM [!DNL Forms] e incrustar el formulario adaptable en una página AEM [!DNL Sites]:

1. Cree y abra una página en el sitio de We.Retail para editarla. Por ejemplo, [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). El formulario adaptable se incrusta en la página [!DNL Sites].

   También puede incrustar el formulario adaptable en una página existente de We.Retail [!DNL Site's]. Por ejemplo: la página ABOUT US [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Le ahorra tiempo para crear una página. Los pasos a continuación utilizan la página recién creada.

   El sitio Web de We.Retail se envía con AEM. Si no tiene instalado el sitio Web de We.Retail, consulte [Implementación de referencia de We.Retail](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) para instalar el sitio.

1. Toque ![propiedades](assets/properties.png) información de página y seleccione la opción **[!UICONTROL Editar plantilla]** en la página del sitio Web de We.Retail recientemente creada. La plantilla de la página se abre en una nueva ficha del explorador.
1. Toque dentro del cuadro **[!UICONTROL contenedor de diseño]** y toque ![administración de fuentes](assets/feedmanagement.png). En la ficha **[!UICONTROL Componentes permitidos]**, expanda el acordeón **[!UICONTROL General]**, seleccione la opción **[!UICONTROL Formulario de AEM]** y toque ![save_icon](assets/save_icon.svg). El componente de Contenedor AEM [!DNL Forms] está habilitado para la página.

1. Abra la ficha del explorador que contiene AEM [!DNL Sites] página abierta en el paso 1. Toque el cuadro **[!UICONTROL Arrastre los componentes aquí]** y toque **+.** En el cuadro  **[!UICONTROL Insertar nuevo]** componente, toque  **[!UICONTROL AEM formulario]**. El componente **[!UICONTROL Contenedor de AEM Forms]** se agrega a la página.
1. Toque el componente **[!UICONTROL AEM Forms contenedor]** y toque ![configure-icon](assets/configure-icon.svg). Aparece un cuadro de diálogo con propiedades de AEM [!DNL Forms] Contenedor. En el campo **[!UICONTROL Ruta del recurso]**, busque y seleccione el formulario adaptable Shipping-address-add-update-form. Toque ![save_icon](assets/save_icon.svg). El formulario adaptable se incrusta en la página.
1. Publique el formulario adaptable y la página [!DNL Sites]. Tenga en cuenta lo siguiente:

   * Si publica la página de AEM [!DNL Sites] por primera vez e incluye un formulario incrustado, publique la página [!DNL Sites] y el formulario incrustado.
   * Si solo modifica el formulario incrustado en una página de sitio publicada, publique el formulario original y los cambios se reflejarán en la página de sitio publicada. La página del sitio publicada incluye una referencia al formulario y no requiere volver a publicar la página.
   * Si modifica la página [!DNL Sites] y el formulario incrustado, vuelva a publicar la página [!DNL Sites] y el formulario.

      ![embed-in-aem-sites](assets/embed-in-aem-sites.png)
   Se agregó el formulario Cambio de dirección de envío y facturación a una página de AEM [!DNL Sites].

## Incrustar el formulario adaptable en una página web externa {#embed-the-adaptive-form-in-an-external-webpage}

Puede incrustar un formulario adaptable en una página web externa (una página web no AEM alojada fuera de AEM) insertando algunas líneas de JavaScript en la página web externa. El código JavaScript envía una solicitud HTTP al servidor AEM [!DNL Forms] para el formulario adaptable y los recursos relacionados y agrega el formulario adaptable a la página web. Para ver los pasos detallados, consulte [incrustar el formulario adaptable en una página Web externa](/help/forms/using/embed-adaptive-form-external-web-page.md).
