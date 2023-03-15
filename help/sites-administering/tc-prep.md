---
title: Preparación del contenido para su traducción
seo-title: Preparing Content for Translation
description: Aprenda a preparar el contenido para la traducción.
seo-description: Learn how to prepare content for translation.
uuid: 369630a8-2ed7-48db-973e-bd8213231d49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 8bd67d71-bcb7-4ca0-9751-3ff3ee054011
feature: Language Copy
exl-id: 81978733-89a6-4436-bcf1-4bde962ed54f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 66%

---

# Preparación del contenido para su traducción{#preparing-content-for-translation}

Por lo general, los sitios web multilingües ofrecen contenido en varios idiomas. El sitio es creado en un idioma y luego traducido a otros idiomas. Por lo general, los sitios multilingües constan de ramas de páginas, donde cada rama contiene las páginas del sitio en un idioma diferente.

El sitio de muestra de Geometrixx incluye varias ramas de idioma y utiliza la siguiente estructura:

```xml
/content
    |- geometrixx
             |- en
             |- fr
             |- de
             |- es
             |- it
             |- ja
             |- zh
```

Cada rama de idioma de un sitio se denomina copia de idioma. La página raíz de una copia de idioma, conocida como raíz de idioma, identifica el idioma del contenido en la copia de idioma. Por ejemplo, `/content/geometrixx/fr` es la raíz del idioma para la copia en francés. Las copias de idioma deben utilizar una [raíz de idioma configurada correctamente](/help/sites-administering/tc-prep.md#creating-a-language-root) para que el idioma correcto se dirija cuando se realicen traducciones de un sitio de origen.

La copia de idioma para la que creó originalmente el contenido del sitio es el maestro de idioma. El maestro de idiomas es la fuente que se traduce a otros idiomas.

Siga estos pasos para preparar su sitio para la traducción:

1. Cree la raíz de idioma del maestro de idioma. Por ejemplo, la raíz de idioma del sitio de demostración de Geometrixx en inglés es /content/geometrixx/en. Asegúrese de que la raíz del idioma esté configurada correctamente según la información de [Creación de una raíz de idioma](/help/sites-administering/tc-prep.md#creating-a-language-root).
1. Cree el contenido del maestro de idioma.
1. Cree la raíz de idioma de cada copia de idioma para su sitio. Por ejemplo, la copia en francés del sitio de muestra del Geometrixx es /content/geometrixx/fr.

Después de preparar el contenido para la traducción, puede crear automáticamente las páginas que faltan en las copias de idioma y en los proyectos de traducción asociados. (Consulte [Creación de un proyecto de traducción](/help/sites-administering/tc-manage.md).) Para obtener una descripción general del proceso de traducción de contenido en AEM, consulte [Traducción de contenido para sitios web multilingües](/help/sites-administering/translation.md).

## Creación de una raíz de idioma {#creating-a-language-root}

Cree una raíz de idioma como la página raíz de una copia de idioma que identifique el idioma del contenido. Después de crear la raíz del idioma, puede crear proyectos de traducción que incluyan la copia del idioma.

Para crear la raíz de idioma, cree una página y utilice un código de idioma ISO como valor para la propiedad Nombre. El código de idioma debe tener uno de los siguientes formatos:

* `<language-code>`El código de idioma admitido es un código de dos letras como se define en la norma ISO-639-1, por ejemplo `en`.

* `<language-code>_<country-code>` o `<language-code>-<country-code>`El código de país admitido es un código de dos letras en minúsculas o mayúsculas, tal como se define en la norma ISO 3166, por ejemplo `en_US`, `en_us`, `en_GB`, `en-gb`.

Puede utilizar cualquiera de los dos formatos, según la estructura que haya elegido para el sitio global.  Por ejemplo, la página raíz de la copia en francés del sitio de Geometrixx tiene lo siguiente `fr` como la propiedad Name. Tenga en cuenta que la propiedad Nombre se utiliza como nombre del nodo de página en el repositorio y, por lo tanto, determina la ruta de la página. (http://localhost:4502/content/geometrixx/fr.html)

El siguiente procedimiento utiliza la interfaz de usuario táctil para crear una copia de idioma de un sitio web. Para obtener instrucciones sobre el uso de la IU clásica, consulte [Creación de una raíz de idioma mediante la IU clásica](/help/sites-administering/tc-lroot-classic.md).

1. Vaya a Sitios.
1. Toque o haga clic en el sitio para el que desea crear una copia de idioma.

   Por ejemplo, para crear una copia de idioma del sitio de Geometrixx Outdoors, debe tocar o hacer clic en Sitio de Geometrixx Outdoors.

1. Toque o haga clic en Crear y, a continuación, toque o haga clic en Crear página.

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. Seleccione la plantilla Página y, a continuación, haga clic o pulse Siguiente.
1. En el campo Nombre escriba el código de país con el formato de `<language-code>` o `<language-code>_<country-code>`, por ejemplo `en`, `en_US`, `en_us`, `en_GB`, `en_gb`. Escriba un título para la página.

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. Haga clic o pulse Crear. En el cuadro de diálogo de confirmación, toque o haga clic en **Listo** para volver a la consola Sitios, o **Abierto** para abrir la copia de idioma.

## Ver el estado de las raíces de los idiomas {#seeing-the-status-of-language-roots}

La IU táctil optimizada proporciona un panel Referencias que muestra una lista de las raíces de idioma que se han creado.

![chlimage_1-23](assets/chlimage_1-23a.png)

El siguiente procedimiento utiliza la IU táctil optimizada para abrir el panel Referencias de una página.

1. En la consola Sitios, seleccione una página del sitio y toque o haga clic en **Referencias**.

   ![chlimage_1-24](assets/chlimage_1-24a.png)

1. En el panel Referencias, toque o haga clic en **Copias de idioma**. El panel Copias de idioma muestra las copias de idioma del sitio web.
