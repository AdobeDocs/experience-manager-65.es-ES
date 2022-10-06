---
title: "Tutorial: Publicar el formulario adaptable"
seo-title: "Tutorial: Publish your adaptive form"
description: Publique el formulario adaptable como página AEM, incruste el formulario en una página de AEM Sites o incruste el formulario adaptable en una página web externa
seo-description: Publish the adaptive form as an AEM page, embed the form to an AEM Sites page, or embed the adaptive form in an external webpage
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
feature: Adaptive Forms
exl-id: c039faec-f832-43d5-8a86-22afa3bef2a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 2%

---

# Tutorial: Publicar el formulario adaptable {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

Este tutorial es un paso en la [Crear el primer formulario adaptable](https://helpx.adobe.com/es/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) serie. Se recomienda seguir la serie en secuencia cronológica para comprender, realizar y demostrar el caso de uso completo del tutorial.

Una vez que el formulario adaptable esté listo, puede publicarlo para que esté disponible para los usuarios finales. Los usuarios finales pueden abrir el formulario publicado en cualquier dispositivo y navegador de Internet. Cuando se publica un formulario adaptable, el formulario y el contenido relacionado se copian de una instancia de autor AEM a una instancia de publicación AEM. El formulario está disponible para el usuario final a través de la instancia de publicación.

Tiene los siguientes métodos para publicar un formulario adaptable:

* [Publicar el formulario adaptable como una página AEM](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Incrustar el formulario adaptable en una página de AEM Sites](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Incruste el formulario adaptable en una página web externa (una página web que no sea AEM alojada fuera de AEM)](../../forms/using/publish-your-adaptive-form.md)

## Antes de comenzar {#before-you-start}

* **[Configuración de una instancia de publicación de AEM Forms](https://helpx.adobe.com/es/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**: La instancia de publicación es una instancia pública de AEM [!DNL Forms] se está ejecutando en modo de publicación. En un entorno de producción, la instancia de publicación está fuera del cortafuegos de la organización.
* **[Configurar replicación y replicación inversa](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**: La replicación copia el contenido de la instancia de autor en una instancia de publicación y devuelve los datos introducidos por el usuario (por ejemplo, los datos de entrada de formulario) de la instancia de publicación a la instancia de autor.

## Publicar el formulario adaptable como una página AEM {#publish-the-adaptive-form-as-an-aem-page}

Cuando el formulario adaptable se publica como una página AEM, toda la página web contiene solo un formulario publicado. Puede utilizar la dirección URL del formulario adaptable para vincularlo desde otra página web. Para publicar el **Shipping-address-add-update-form** formulario adaptable como página AEM:

1. Iniciar sesión en AEM [!DNL Forms] instancia de autor y busque el formulario adaptable Shipping-address-add-update-form en la AEM [!DNL Forms] IU.
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Seleccione el formulario adaptable Shipping-address-add-update-form y pulse **[!UICONTROL Publicación]**. Se muestra un cuadro de diálogo que contiene recursos relacionados con el formulario adaptable. Toque **[!UICONTROL Publicación]**. El formulario adaptable se publica y aparece un cuadro de diálogo de éxito.
1. Abra el formulario en la instancia de publicación. El formulario está disponible para que el usuario final lo rellene y lo envíe.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Incrustar el formulario adaptable en una página de AEM Sites {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] permite a los desarrolladores de formularios incrustar formularios adaptables sin problemas en un AEM [!DNL Sites] página. El formulario adaptable integrado es totalmente funcional y los usuarios pueden rellenar y enviar el formulario sin salir de la página. Ayuda al usuario a permanecer en el contexto de otros elementos de la página web e interactuar simultáneamente con el formulario.

AEM [!DNL Forms] proporcionar un componente, AEM [!DNL Forms] Contenedor, para incrustar un formulario adaptable en un AEM [!DNL Sites] página. De forma predeterminada, el componente no está visible en AEM [!DNL Sites] contenedor. Siga estos pasos para habilitar el AEM [!DNL Forms] Componente de contenedor e incrustar el formulario adaptable en un AEM [!DNL Sites] Página:

1. Cree y abra una página en el sitio de We.Retail para editarla. Por ejemplo, [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). El formulario adaptable está incrustado en la variable [!DNL Sites] página.

   También puede incrustar el formulario adaptable en un We.Retail existente [!DNL Site's] página. Por ejemplo, la página ABOUT US [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Le ahorra tiempo para crear una página. Los pasos siguientes utilizan la página recién creada.

   El sitio de We.Retail se envía con AEM. Si no tiene instalado el sitio de We.Retail, consulte [Implementación de referencia de We.Retail](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) instale el sitio.

1. Toque ![propiedades](assets/properties.png) información de la página y seleccione **[!UICONTROL Editar plantilla]** en la página de sitio de We.Retail recién creada. La plantilla de la página se abre en una nueva pestaña del explorador.
1. Toque dentro de la **[!UICONTROL contenedor de diseño]** cuadro y toque ![feed management](assets/feedmanagement.png). En el **[!UICONTROL Componentes permitidos]** expanda la pestaña **[!UICONTROL General]** acordeón, seleccione **[!UICONTROL Formulario AEM]** y pulse ![save_icon](assets/save_icon.svg). El AEM [!DNL Forms] El componente Contenedor está habilitado para la página.

1. Abra la ficha del explorador que contenga AEM [!DNL Sites] página abierta en el paso 1. Toque . **[!UICONTROL Arrastre los componentes aquí]** cuadro y toque **+.** En el **[!UICONTROL Insertar nuevo componente]** cuadro, toque **[!UICONTROL Formulario AEM]**. La variable **[!UICONTROL Contenedor de AEM Forms]** se añade a la página.
1. Toque . **[!UICONTROL Contenedor de AEM Forms]** componente y toque ![configure-icon](assets/configure-icon.svg). Cuadro de diálogo con propiedades de AEM [!DNL Forms] Aparece el contenedor. En el **[!UICONTROL Ruta de recursos]** , busque y seleccione el formulario adaptable Shipping-address-add-update-form . Toque ![save_icon](assets/save_icon.svg). El formulario adaptable está incrustado en la página .
1. Publicar el formulario adaptable y [!DNL Sites] página. Tenga en cuenta lo siguiente:

   * Si publica el AEM [!DNL Sites] por primera vez e incluye un formulario incrustado, publique el [!DNL Sites] y el formulario incrustado.
   * Si solo modifica el formulario incrustado en una página de sitio publicada, publique el formulario original y los cambios se reflejarán en la página del sitio publicada. La página del sitio publicada incluye una referencia al formulario y no requiere que se vuelva a publicar la página.
   * Si modifica la variable [!DNL Sites] y el formulario incrustado, vuelva a publicar el [!DNL Sites] y el formulario.

      ![embed-in-aem-sites](assets/embed-in-aem-sites.png)
   Formulario de cambio de dirección de envío y facturación añadido a un AEM [!DNL Sites] página.

## Incrustar el formulario adaptable en una página web externa {#embed-the-adaptive-form-in-an-external-webpage}

Puede incrustar un formulario adaptable en una página web externa (una página web que no sea AEM y que esté alojada fuera de AEM) insertando algunas líneas de JavaScript en la página web externa. El código JavaScript envía una solicitud HTTP a la AEM [!DNL Forms] para el formulario adaptable y los recursos relacionados y agrega el formulario adaptable a la página web. Para ver los pasos detallados, consulte [integrar el formulario adaptable en una página web externa](/help/forms/using/embed-adaptive-form-external-web-page.md).
