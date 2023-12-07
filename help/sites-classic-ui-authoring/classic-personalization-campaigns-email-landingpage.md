---
title: Creación de una página de aterrizaje de newsletter efectiva
description: Una página de aterrizaje de newsletter efectiva le ayuda a que el mayor número de personas posible se suscriban a su newsletter (u otra campaña de marketing por correo electrónico). Puede utilizar la información que recopila de las suscripciones a la newsletter para obtener posibles clientes.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: c2fbf858-8815-426e-a2e5-f92bcf909ad0
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Creación de una página de aterrizaje de newsletter efectiva{#creating-an-effective-newsletter-landing-page}

Una página de aterrizaje de newsletter efectiva le ayuda a que el mayor número de personas posible se suscriban a su newsletter (u otra campaña de marketing por correo electrónico). Puede utilizar la información que recopila de las suscripciones a la newsletter para obtener posibles clientes.

Para crear una página de aterrizaje de newsletter efectiva, debe hacer lo siguiente:

1. Cree una lista para la newsletter, de modo que los usuarios puedan suscribirse a ella.
1. Cree el formulario de registro. Al hacerlo, agregue un paso del flujo de trabajo que añada automáticamente a la lista de posibles clientes a la persona que se suscribe a la newsletter.
1. Cree una página de confirmación que agradezca a los usuarios su registro y que posiblemente les proporcione una promoción.
1. Agregar teasers.

>[!NOTE]
>
>El Adobe no tiene previsto mejorar esta capacidad (administración de posibles clientes y listas).
>La recomendación es utilizar [Adobe Campaign AEM y la integración para la integración de los recursos](/help/sites-administering/campaign.md).

## Creación de una lista para la newsletter {#creating-a-list-for-the-newsletter}

Cree una lista, por ejemplo, **Newsletter de Geometrixx**, en MCM para la newsletter a la que deben suscribirse las personas. La creación de listas se describe en [Creación de listas](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingnewlists).

A continuación se muestra un ejemplo de lista:

![mcm_listcreate](assets/mcm_listcreate.png)

## Creación de un formulario de registro {#create-a-sign-up-form}

Cree un formulario de registro de newsletter que permita a los usuarios suscribirse a las etiquetas. El sitio web de Geometrixx de ejemplo proporciona una página de newsletter en la barra de herramientas de Geometrixx donde puede crear el formulario.

Para crear su propio formulario de newsletter, consulte la información sobre la creación de formularios en la [Documentación de Forms](/help/sites-authoring/default-components.md#form). La newsletter utiliza las etiquetas de la Biblioteca de etiquetas. Para añadir etiquetas adicionales, consulte [Administración de etiquetas](/help/sites-authoring/tags.md#tagadministration).

Los campos ocultos en el siguiente ejemplo proporcionan la mínima cantidad de información (correo electrónico); además, puede agregar más campos más adelante, pero esto afectará a la tasa de conversión.

El siguiente ejemplo es un formulario creado en https://localhost:4502/cf#/content/geometrixx/en/toolbar/newsletter.html.

1. Cree el formulario.

   ![mcm_newsletterpage](assets/mcm_newsletterpage.png)

1. Clic **Editar** en el componente Formulario para configurar el formulario y que vaya a una página de agradecimiento (consulte [Creación de páginas de agradecimiento](#creating-a-thank-you-page)).

   ![dc_formstart_thankyou](assets/dc_formstart_thankyou.png)

1. Establezca la acción Formulario (que es lo que ocurrirá cuando envíe el formulario) y configure el grupo para asignar usuarios registrados a la lista creada anteriormente (por ejemplo, newsletter de Geometrixx).

   ![dc_formstart_thankyouadvanced](assets/dc_formstart_thankyouadvanced.png)

### Creación de una página de agradecimiento {#creating-a-thank-you-page}

Cuando los usuarios hagan clic **Suscribirse ahora**, desea que una página de agradecimiento se abra automáticamente. Cree la página de agradecimiento en la página de la newsletter de Geometrixx. Después de crear el formulario de la newsletter, edite el componente Formulario y añada la ruta a la página de agradecimiento.

Al enviar la solicitud, el usuario pasa a un **Gracias.** página tras la cual recibirán un correo electrónico. Esta página de agradecimiento se ha creado en /content/geometrixx/en/toolbar/newsletter/thank_you.

![mcm_newsletter_thank_youpage](assets/mcm_newsletter_thankyoupage.png)

### Añadir teasers {#adding-teasers}

Añadir [teasers](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers) para dirigirse a audiencias específicas. Por ejemplo, puede agregar teasers a la página de agradecimiento y a la página de registro de la newsletter.

Para agregar teasers para crear una página de aterrizaje de newsletter efectiva:

1. Cree un párrafo de teaser para un regalo de registro. Seleccionar **Primero** como estrategia e incluir texto que les informe qué regalo recibirán.

   ![dc_teaser_thank_you](assets/dc_teaser_thankyou.png)

1. Cree un párrafo de teaser para la página de agradecimiento. Seleccionar **Primero** como estrategia e incluir texto que indique que el regalo está en camino.

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. Cree una campaña con los dos teasers: etiquete uno con el negocio y otro sin etiquetar.

### Inserción de contenido a los suscriptores {#pushing-content-to-subscribers}

Insertar cualquier cambio en las páginas a través de la funcionalidad Newsletter en el MCM. A continuación, puede insertar contenido actualizado a los suscriptores.

Consulte [Envío de boletines](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters).
