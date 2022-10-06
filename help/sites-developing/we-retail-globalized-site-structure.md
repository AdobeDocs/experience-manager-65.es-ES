---
title: Cómo probar la estructura de sitios globalizados en We.Retail
seo-title: Trying out the Globalized Site Structure in We.Retail
description: Cómo probar la estructura de sitios globalizados en We.Retail
seo-description: null
uuid: 5e5a809d-578f-4171-8226-cb65aa995754
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d674458c-d5f3-4dee-a673-b0777c02ad30
exl-id: e1de20b0-6d7a-4bda-b62f-c2808fd0af28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Cómo probar la estructura de sitios globalizados en We.Retail{#trying-out-the-globalized-site-structure-in-we-retail}

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

1. Con el maestro de idioma inglés seleccionado, abra la **Referencias** carril en la consola Sitios y seleccione **Copias de idioma**.

   ![imagen_1-91](assets/chlimage_1-91.png)

1. Marque la casilla de verificación situada junto a la **Copias de idioma** para seleccionar todas las copias de idioma. En el **Actualizar copias de idioma** del carril, seleccione la opción para **Crear un nuevo proyecto de traducción**. Proporcione un nombre al proyecto y haga clic en **Actualizar**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Se crea un proyecto para cada traducción de idioma. Visualizarlos debajo de **Navegación -> Proyectos**.

   ![imagen_1-93](assets/chlimage_1-93.png)

1. Haga clic en alemán para ver los detalles del proyecto de traducción. Tenga en cuenta que el estado se encuentra en **Borrador**. Para iniciar la traducción con el servicio de traducción de Microsoft, haga clic en las comillas angulares que hay junto al **Trabajo de traducción** encabezado y seleccione **Inicio**.

   ![imagen_1-94](assets/chlimage_1-94.png)

1. Se inicia el proyecto de traducción. Haga clic en los puntos suspensivos en la parte inferior de la tarjeta denominada Trabajo de traducción para ver los detalles. Páginas con el estado **Listo para revisión** ya han sido traducidas por el servicio de traducción.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Seleccionar una de las páginas de la lista y, a continuación, **Vista previa en Sitios** en la barra de herramientas, se abre la página traducida en el editor de páginas.

   ![imagen_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>Este procedimiento demostró la integración integrada con la traducción automática de Microsoft. Al usar la variable [Marco de integración de traducción AEM](/help/sites-administering/translation.md), puede integrarse con muchos servicios de traducción estándar para orquestar la traducción de AEM.

## Información adicional {#further-information}

Para obtener más información, consulte el documento de creación [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md) para obtener todos los detalles técnicos.
