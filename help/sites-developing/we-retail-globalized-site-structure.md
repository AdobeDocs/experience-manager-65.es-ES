---
title: Prueba de la estructura del sitio globalizada en We.Retail
description: Prueba de la estructura del sitio globalizada en We.Retail
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: e1de20b0-6d7a-4bda-b62f-c2808fd0af28
source-git-commit: 69346a710708ee659ee97e9fdc193c8ea2658fe6
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# Prueba de la estructura del sitio globalizada en We.Retail{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail se ha creado con una estructura de sitio globalizada que ofrece un formato de idioma que se puede copiar en directo en sitios web específicos de cada país. Todo está configurado de forma predeterminada para permitirle experimentar con esta estructura y las capacidades de traducción integradas.

## Probando a cabo {#trying-it-out}

1. Abra la consola Sitios desde **Navegación global -> Sitios**.
1. Cambie a la vista de columna (si no está activa) y seleccione We.Retail. Observe la estructura de país de ejemplo con Suiza, Estados Unidos, Francia, etc., junto al Idioma principal.

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. Seleccione Suiza y vea las raíces lingüísticas de los idiomas de ese país. Todavía no hay ningún contenido debajo de estas raíces.

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. Cambie a la vista de lista y compruebe que las copias de idioma de los países sean Live Copies.

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. Vuelva a la vista de columna, haga clic en el Patrón de idioma y vea las raíces maestras de idioma con contenido. Solo el inglés tiene contenido.

   We.Retail no incluye ningún contenido traducido, pero la estructura y la configuración están configuradas para permitirle demostrar los servicios de traducción.

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. Con el Idioma principal de inglés seleccionado, abra el **Referencias** en la consola sitios y seleccione **Copias de idioma**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Marque la casilla que aparece junto a la etiqueta **Copias de idioma** para seleccionar todas las copias de idioma. En el **Actualizar copias de idioma** del carril, seleccione la opción para **Creación de un nuevo proyecto de traducción**. Proporcione un nombre al proyecto y haga clic en **Actualizar**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Se crea un proyecto para cada traducción de idioma. Véalas en **Navegación -> Proyectos**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. Haga clic en alemán para ver los detalles del proyecto de traducción. El estado es **Borrador**. Para iniciar la traducción con el servicio de traducción de Microsoft®, haga clic en las comillas angulares junto al icono **Trabajo de traducción** encabezado y seleccione **Inicio**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Se inicia el proyecto de traducción. Haga clic en los puntos suspensivos en la parte inferior de la tarjeta denominada Trabajo de traducción para ver los detalles. Páginas con el estado **Listo para revisión** ya han sido traducidos por el servicio de traducción.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Seleccionar una de las páginas de la lista y, a continuación, **Vista previa en sitios** en la barra de herramientas, se abre la página traducida en el editor de páginas.

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>Este procedimiento demostró la integración integrada con la traducción automática de Microsoft®. Uso del [AEM Marco de integración de traducción](/help/sites-administering/translation.md)AEM , puede integrarlo con muchos servicios de traducción estándar para organizar la traducción de los recursos de traducción de la manera más rápida y sencilla

## Información adicional {#further-information}

Para obtener más información, consulte el documento de creación [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md) para obtener información técnica completa.
