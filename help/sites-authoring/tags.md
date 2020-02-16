---
title: Uso de etiquetas
seo-title: Uso de etiquetas
description: Las etiquetas son un método rápido y fácil de clasificar contenido dentro del sitio web
seo-description: Las etiquetas son un método rápido y fácil de clasificar contenido dentro del sitio web
uuid: 5d922443-f924-426e-acf4-27dffd1053f6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 9fb6d603-eb17-4192-bfa6-6c316f14ac7d
docset: aem65
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15

---


# Uso de etiquetas{#using-tags}

Las etiquetas son un método rápido y fácil de clasificar contenido dentro de un sitio web. Las etiquetas pueden considerarse como palabras clave o marcas que se pueden adjuntar a una página, un recurso o cualquier otro contenido para que con las búsquedas se encuentre ese contenido y el contenido relacionado.

* See [Administering Tags](/help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.
* See [Tagging for Developers](/help/sites-developing/tags.md) for information about the tagging framework as well as including and extending tags in custom applications.

## Diez motivos para utilizar etiquetas {#ten-reasons-to-use-tagging}

1. **Organizar contenido** : el etiquetado facilita la vida de los autores, ya que pueden organizar contenido rápidamente con poco esfuerzo.
1. **Organización de etiquetas** : mientras las etiquetas organizan el contenido, las taxonomías jerárquicas y los espacios de nombres organizan las etiquetas.
1. **Etiquetas** profundamente organizadas: Con la capacidad de crear etiquetas y subetiquetas, se puede expresar todo el sistema taxonómico, cubriendo términos, subtérminos y sus relaciones. Esto permite crear una segunda (o tercera) jerarquía de contenido en paralelo a la oficial.
1. **Etiquetado** controlado: el etiquetado se puede controlar aplicando permisos a etiquetas y/o espacios de nombres para controlar la creación de etiquetas y la aplicación.
1. **Etiquetado** flexible: las etiquetas tienen muchos nombres y caras: etiquetas, términos de taxonomía, categorías, etiquetas y mucho más. Son flexibles en el modelo de contenido y en la manera de usarlas. Por ejemplo, al trazar información demográfica de destino, categorizar y calificar contenido o para crear una jerarquía de contenido secundario.
1. **Búsqueda** mejorada: el componente de búsqueda predeterminado en AEM incluye generalmente etiquetas creadas y etiquetas aplicadas a las que se pueden aplicar filtros para reducir los resultados a los que sean relevantes.
1. **Habilitación** de SEO: las etiquetas aplicadas como propiedades de página se mostrarán automáticamente en las etiquetas de la página, haciéndolo visible para los motores de búsqueda.
1. **Sofisticación** simple: las etiquetas se pueden crear simplemente a partir de una palabra y el toque de un botón. Después, se pueden añadir un título, una descripción y marcas ilimitadas para proporcionar más semántica a la etiqueta.
1. **Coherencia** principal: el sistema de etiquetado es un componente principal de AEM y lo utilizan todas las capacidades de AEM para categorizar el contenido. Además, la API de etiquetado está disponible para los desarrolladores para que creen aplicaciones compatibles con el etiquetado con acceso a las mismas taxonomías.
1. **Combina estructura y flexibilidad** : AEM es ideal para trabajar con información estructurada, debido al anidado de páginas y rutas. También es extremadamente útil a la hora de trabajar con información sin estructurar, debido a la búsqueda incorporada de texto completo. El etiquetado combina las ventajas que aportan tanto la estructura como la flexibilidad.

A la hora de diseñar la estructura de contenido para un sitio y el esquema de metadatos para los recursos, considere la ligereza y la accesibilidad que el etiquetado proporciona.

## Aplicación de etiquetas {#applying-tags}

In the author environment, authors may apply tags by accessing the page properties and entering one or more tags in the **Tags/Keywords** field.

To apply [pre-defined tags](/help/sites-administering/tags.md), in the **Page Properties** window use the **Tags** field and the **Select Tags** window. The **Standard Tags** tab is the default namespace, which means there is no `namespace-string:` prefixed to the taxonomy.

![chlimage_1-41](assets/chlimage_1-41.png)

### Publicación de etiquetas {#publishing-tags}

Al igual que con las páginas, puede realizar las siguientes acciones con etiquetas y espacios de nombres:

**Activar**

* Activar etiquetas individuales.

   Al igual que con las páginas, las nuevas etiquetas que se creen deberán activarse antes de que estén disponibles en el entorno de publicación.

>[!NOTE]
>
>Cuando se activa una página, se abre automáticamente un cuadro de diálogo que le permite activar las etiquetas desactivadas que pertenecen a la página.

**Desactivar**

* Desactivar las etiquetas seleccionadas.
