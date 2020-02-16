---
title: '"Tutorial: Publicar el formulario adaptable"'
seo-title: '"Tutorial: Publicar el formulario adaptable"'
description: Publique el formulario adaptable como página de AEM, incruste el formulario en una página de AEM Sites o incruste el formulario adaptable en una página web externa
seo-description: Publique el formulario adaptable como página de AEM, incruste el formulario en una página de AEM Sites o incruste el formulario adaptable en una página web externa
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
translation-type: tm+mt
source-git-commit: 709d8fe467f5449eb1e844a49126535a4a4a6e7a

---


# Tutorial: Publicación del formulario adaptable {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

Este tutorial es un paso de la serie [Crear su primer formulario](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) adaptable. Se recomienda seguir la serie en secuencia cronológica para comprender, realizar y demostrar el caso de uso completo del tutorial.

Una vez que el formulario adaptable esté listo, puede publicarlo para que esté disponible para los usuarios finales. Los usuarios finales pueden abrir el formulario publicado en cualquier dispositivo y navegador de Internet. Cuando se publica un formulario adaptable, el formulario y el contenido relacionado se copian de una instancia de autor de AEM a una instancia de publicación de AEM. El formulario se pone a disposición del usuario final a través de la instancia de publicación.

Tiene los siguientes métodos para publicar un formulario adaptable:

* [Publicación del formulario adaptable como página de AEM](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Incrustar el formulario adaptable en una página Sitios de AEM](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Incrustar el formulario adaptable en una página web externa (una página web que no es de AEM alojada fuera de AEM)](../../forms/using/publish-your-adaptive-form.md)

## Antes de comenzar {#before-you-start}

* **[Configure una instancia](https://helpx.adobe.com/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**de publicación de AEM Forms: La instancia de publicación es una instancia pública de AEM Forms que se ejecuta en modo de publicación. En un entorno de producción, la instancia de publicación está fuera del servidor de seguridad de la organización.
* **[Configure la replicación y la replicación](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**inversa: La replicación copia el contenido de la instancia de autor en una instancia de publicación y devuelve los datos introducidos por el usuario (por ejemplo, los datos introducidos en el formulario) desde la instancia de publicación a la instancia de autor.

## Publicación del formulario adaptable como página de AEM {#publish-the-adaptive-form-as-an-aem-page}

Cuando el formulario adaptable se publica como una página de AEM, toda la página web solo contiene un formulario publicado. Puede utilizar la dirección URL del formulario adaptable para vincularlo desde otra página web. Para publicar el formulario adaptable **Shipping-address-add-update-form** como página de AEM:

1. Inicie sesión en la instancia de creación de AEM Forms y busque el formulario adaptable Shipping-address-add-update-form en la interfaz de usuario de AEM Forms.
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Seleccione el formulario adaptable Shipping-address-add-update-form y toque **Publicar**. Se muestra un cuadro de diálogo que contiene recursos relacionados con el formulario adaptable. Toque **Publicar**. Se publica el formulario adaptable y aparece un cuadro de diálogo de éxito.
1. Abra el formulario en la instancia de publicación. El formulario está disponible para que el usuario final lo rellene y lo envíe.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Incrustar el formulario adaptable en una página Sitios de AEM {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM Forms permite a los desarrolladores de formularios incrustar formularios adaptables sin problemas en una página Sitios de AEM. El formulario adaptable incrustado es totalmente funcional y los usuarios pueden rellenar y enviar el formulario sin salir de la página. Ayuda al usuario a permanecer en el contexto de otros elementos de la página web e interactuar simultáneamente con el formulario.

AEM Forms proporciona un componente, AEM Forms Container, para incrustar un formulario adaptable en una página de AEM Sites. De forma predeterminada, el componente no está visible en el contenedor Sitios de AEM. Siga estos pasos para activar el componente Contenedor de AEM Forms e incrustar el formulario adaptable en una página Sitios de AEM:

1. Cree y abra una página en el sitio de We.Retail para editarla. Por ejemplo, [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). El formulario adaptable se incrusta en la página de sitios.

   También puede incrustar el formulario adaptable en una página existente del sitio Web.Retail. Por ejemplo, la página ABOUT US [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Le ahorra tiempo para crear una página. Los pasos a continuación utilizan la página recién creada.

   El sitio Web de We.Retail se envía con AEM. Si no tiene instalado el sitio Web de We.Retail, consulte Implementación [de referencia de](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) We.Retail para instalar el sitio.

1. Toque ![propiedades](assets/properties.png) de la información de la página y seleccione la opción **Editar plantilla** en la página del sitio Web We.Retail recientemente creada. La plantilla de la página se abre en una nueva ficha del explorador.
1. Toque dentro del cuadro contenedor **de** diseño y toque ![Administración de fuentes](assets/feedmanagement.png). En la ficha Componentes **** permitidos, expanda el acordeón **General** , seleccione la opción Formulario **** AEM y toque ![](https://helpx.adobe.com/content/dam/help/en/aem-forms/icons/AEM_6_3_Forms_save.PNG). El componente Contenedor de AEM Forms está habilitado para la página.

1. Abra la ficha del navegador que contiene la página Sitios AEM abierta en el paso 1. Puntee en el cuadro **Arrastrar componentes aquí** y toque **+.** En el cuadro **Insertar nuevo componente** , toque Formulario **AEM.** El componente Contenedor **de formularios** AEM se agrega a la página.
1. Toque el componente contenedor **de formularios** AEM y toque ![](https://helpx.adobe.com/content/dam/help/en/aem-forms/6-2/cmppr.png). Aparece un cuadro de diálogo con las propiedades de AEM Forms Container. En el campo Ruta **del** recurso, busque y seleccione el formulario adaptable Shipping-address-add-update-form. Tocar ![](https://helpx.adobe.com/content/dam/help/en/aem-forms/icons/AEM_6_3_Forms_save.PNG). El formulario adaptable se incrusta en la página.
1. Publique el formulario adaptable y la página de sitios. Tenga en cuenta lo siguiente:

   * Si publica la página Sitios de AEM por primera vez e incluye un formulario incrustado, publique la página Sitios y el formulario incrustado.
   * Si solo modifica el formulario incrustado en una página de sitio publicada, publique el formulario original y los cambios se reflejarán en la página de sitio publicada. La página del sitio publicada incluye una referencia al formulario y no requiere volver a publicar la página.
   * Si modifica la página Sitios y el formulario incrustado, vuelva a publicar la página Sitios y el formulario.
   ![embed-in-aem-sites](assets/embed-in-aem-sites.png)

   Se ha agregado el formulario Cambio de dirección de envío y facturación a una página Sitios de AEM.

## Incrustar el formulario adaptable en una página web externa {#embed-the-adaptive-form-in-an-external-webpage}

Puede incrustar un formulario adaptable en una página web externa (una página web que no sea de AEM alojada fuera de AEM) insertando algunas líneas de JavaScript en la página web externa. El código JavaScript envía una solicitud HTTP al servidor de AEM Forms para el formulario adaptable y los recursos relacionados y agrega el formulario adaptable a la página web. Para ver los pasos detallados, consulte [Incrustar el formulario adaptable en una página](/help/forms/using/embed-adaptive-form-external-web-page.md)web externa.
