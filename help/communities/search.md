---
title: Función de búsqueda
description: Agregar y configurar la búsqueda en un sitio de Communities
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 1%

---

# Función de búsqueda {#search-feature}

La función de búsqueda funciona con varias otras funciones, como foros, para proporcionar la capacidad de buscar contenido.

Al agregar la capacidad de buscar publicaciones ingresadas por miembros de la comunidad, lo que se conoce como contenido generado por el usuario (UGC), hay dos componentes: [Buscar](#search) y [Resultados de búsqueda](#search-results).

La página que incluye el componente `Search Results` admite tanto la búsqueda como la visualización de los resultados.

La página que incluye el componente `Search` proporciona un lugar para iniciar una búsqueda con los resultados que aparecen en la página `Search Results`.

La función de búsqueda se puede utilizar con cualquier otra función que permita a los visitantes y miembros del sitio ver el contenido.

## Búsqueda {#search-features}

### Agregar la búsqueda a una página {#add-search-to-a-page}

Para agregar un componente `Search` a una página en modo de autor, use el explorador de componentes para localizar `Communities / Search` y arrástrelo hasta su lugar en una página. El uso de `Search` requiere una segunda página para `Search Results.`

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](basics.md).

Cuando se incluya la biblioteca necesaria del lado del cliente `cq.social.hbs.search`, así es como aparecerá el componente `Search`.

![add-search](assets/add-search.png)

### Configuración de la búsqueda añadida {#configure-the-added-search}

Seleccione el componente `Search` colocado al que desee acceder y seleccione el icono `Configure` que abre el cuadro de diálogo de edición.

![configurar](assets/configure-new.png)

En la ficha **[!UICONTROL Configuración de búsqueda]**, especifique las rutas que se buscarán cuando un visitante introduzca una consulta.

![configuración de búsqueda](assets/search-settings.png)

* **[!UICONTROL Rutas de búsqueda]**
Al agregar rutas de búsqueda mediante el botón Agregar elemento, la búsqueda de contenido está limitada. Por ejemplo, para limitar la búsqueda a un foro específico, seleccione un componente de foro ubicado en una página:

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL Página de resultados]**
Los resultados aparecerán en una página independiente especificada mediante el explorador para seleccionar una página que contenga el componente `Search Results`.

## Resultados de la búsqueda {#search-results}

### Agregar resultados de búsqueda a una página {#add-search-results-to-a-page}

Para agregar un componente `Search Results` a una página en modo de autor, use el explorador de componentes para localizar

* `Communities / Search Results`

y arrástrela a su lugar en una página. A diferencia del componente Buscar, no se necesita una segunda página, ya que los resultados se muestran en la misma página.

Si usa la búsqueda en otro lugar del sitio web, esta página con `Search Results` puede configurarse para que sea la `Result Page` de cualquiera o todas las instancias de `Search`.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](basics.md).

Cuando se incluya la biblioteca del lado del cliente necesaria, `cq.social.hbs.search`, así es como aparecerá el componente `Search Result`:

![resultado de búsqueda](assets/search-result1.png)

### Configurar el resultado de búsqueda agregado {#configure-the-added-search-result}

Seleccione el componente `Search Results` colocado al que desee acceder y seleccione el icono `Configure` que abre el cuadro de diálogo de edición.

![configurar](assets/configure-new.png)

En la ficha **[!UICONTROL Configuración de resultados de búsqueda]**, es posible especificar las rutas que se incluyen en la búsqueda cuando un visitante introduce una consulta.

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL Resultados de búsqueda por página]**

  Defina el número de temas/entradas que se muestran por página. El valor predeterminado es 10.

* **[!UICONTROL Rutas de búsqueda]**

  Al agregar rutas de búsqueda mediante el botón Agregar elemento, la búsqueda de contenido está limitada.

## Información adicional {#additional-information}

Encontrará más información en la página de [Search Essentials](search-implementation.md) para desarrolladores.
