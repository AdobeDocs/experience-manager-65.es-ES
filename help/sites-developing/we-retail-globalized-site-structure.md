---
title: Cómo probar la estructura de sitios globalizados en We.Retail
seo-title: Cómo probar la estructura de sitios globalizados en We.Retail
description: Cómo probar la estructura de sitios globalizados en We.Retail
seo-description: nulo
uuid: 5e5a809d-578f-4171-8226-cb65aa995754
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d674458c-d5f3-4dee-a673-b0777c02ad30
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# Probar la estructura de sitio globalizada en We.Retail{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail se ha creado con una estructura de sitio globalizada que ofrece maestros de idioma que pueden copiarse en directo en sitios web específicos de cada país. Todo está listo para usar para que pueda experimentar con esta estructura y las capacidades de traducción integradas.

## Probándolo {#trying-it-out}

1. Abra la consola Sitios desde **Navegación global -> Sitios**.
1. Cambie a la vista de columna (si no está activo) y seleccione We.Retail. Observe la estructura de país de ejemplo con Suiza, los Estados Unidos, Francia, etc., junto a los Maestros de idiomas.

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. Seleccione Suiza y vea las raíces lingüísticas de los idiomas de ese país. Tenga en cuenta que todavía no hay contenido debajo de estas raíces.

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. Cambie a la vista de lista y vea que las copias de idioma de los países son Live Copies.

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. Vuelva a la vista de columna, haga clic en el Maestro de idioma y vea las raíces del maestro de idioma con contenido. Tenga en cuenta que solo el inglés tiene contenido.

   We.Retail no incluye ningún contenido traducido, pero la estructura y la configuración están implementadas para permitirle mostrar los servicios de traducción.

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. Con el English Language Master seleccionado, abra el carril **References** en la consola Sitios y seleccione **Language Copies**.

   ![imagen_1-91](assets/chlimage_1-91.png)

1. Marque la casilla de verificación situada junto a la etiqueta **Language Copies** para seleccionar todas las copias de idioma. En la sección **Update language Copies** del carril, seleccione la opción **Create a new translation project**. Proporcione un nombre para el proyecto y haga clic en **Actualizar**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Se crea un proyecto para cada traducción de idioma. Verlas en **Navegación -> Proyectos**.

   ![imagen_1-93](assets/chlimage_1-93.png)

1. Haga clic en alemán para ver los detalles del proyecto de traducción. Tenga en cuenta que el estado es **Borrador**. Para iniciar la traducción con el servicio de traducción de Microsoft, haga clic en el elemento adicional situado junto al encabezado **Trabajo de traducción** y seleccione **Inicio**.

   ![imagen_1-94](assets/chlimage_1-94.png)

1. Se inicia el proyecto de traducción. Haga clic en los puntos suspensivos en la parte inferior de la tarjeta denominada Trabajo de traducción para ver los detalles. El servicio de traducción ya ha traducido las páginas con el estado **Ready for review**.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Al seleccionar una de las páginas de la lista y, a continuación, **Vista previa en Sites** en la barra de herramientas, se abre la página traducida en el editor de páginas.

   ![imagen_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>Este procedimiento demostró la integración integrada con la traducción automática de Microsoft. Con el [AEM Translation Integration Framework](/help/sites-administering/translation.md), puede integrar con muchos servicios de traducción estándar para orquestar la traducción de AEM.

## Información adicional {#further-information}

Para obtener más información, consulte el documento de creación [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md) para obtener información técnica completa.
