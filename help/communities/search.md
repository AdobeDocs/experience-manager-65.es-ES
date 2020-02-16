---
title: Función de búsqueda
seo-title: Función de búsqueda
description: Adición y configuración de la búsqueda en un sitio de comunidades
seo-description: Adición y configuración de la búsqueda en un sitio de comunidades
uuid: ca633456-911f-447f-881e-653533125d5f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3acac082-efbe-4995-b374-851cb9aaf62d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Función de búsqueda {#search-feature}

La función de búsqueda funciona con otras funciones, como los foros, para proporcionar la capacidad de buscar contenido.

Al agregar la capacidad de buscar publicaciones ingresadas por miembros de la comunidad, denominada contenido generado por el usuario (UGC), hay dos componentes: [`Search`](#search) y [`Search Results`](#search-results).

La página que incluye el `Search Results` componente admite tanto la búsqueda como la visualización de resultados.

La página que incluye el `Search`componente proporciona un lugar para iniciar una búsqueda con resultados que aparecen en la `Search Results` página.

La función de búsqueda se puede utilizar con cualquier otra función que permita a los visitantes y miembros del sitio ver el contenido.

## Búsqueda {#search-features}

### Agregar búsqueda a una página {#add-search-to-a-page}

Para agregar un `Search` componente a una página en modo de autor, utilice el navegador de componentes para ubicarlo `Communities / Search` y arrastrarlo a su lugar en una página. El uso de `Search` requiere una segunda página para el `Search Results.`

Para obtener la información necesaria, visite [Communities Components Basics](basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se incluye la biblioteca del lado del cliente requerida, `cq.social.hbs.search`, así es como aparecerá el `Search` componente.

![chlimage_1-373](assets/chlimage_1-373.png)

### Configurar la búsqueda agregada {#configure-the-added-search}

Seleccione el componente colocado al que desea acceder y seleccione el `Search` `Configure` icono que abre el cuadro de diálogo de edición.

![chlimage_1-374](assets/chlimage_1-374.png)

En la ficha Configuración **[!UICONTROL de]** búsqueda, especifique cómo se buscan las rutas cuando un visitante introduce una consulta.

![chlimage_1-375](assets/chlimage_1-375.png)

* **[!UICONTROL Rutas]** de búsqueda Al agregar rutas de búsqueda mediante el botón Agregar elemento, la búsqueda de contenido es limitada. Por ejemplo, para limitar la búsqueda a un foro específico, seleccione un componente de foro ubicado en una página:

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL Página]** de resultados Los resultados aparecerán en una página independiente especificada mediante el navegador para seleccionar una página que contenga el `Search Results` componente.

## Resultados de la búsqueda {#search-results}

### Agregar resultados de búsqueda a una página {#add-search-results-to-a-page}

Para agregar un `Search Results` componente a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Search Results`

y arrástrelo a su lugar en una página. A diferencia del componente Buscar, no se necesita una segunda página, ya que los resultados se mostrarán en la misma página.

Si utiliza Buscar en cualquier parte del sitio web, esta página con `Search Results` puede configurarse para que sea la `Result Page` de todas las instancias de `Search`.

Para obtener la información necesaria, visite [Communities Components Basics](basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se incluye la biblioteca del lado del cliente requerida, `cq.social.hbs.search`, así es como aparecerá el `Search Result` componente:

![chlimage_1-376](assets/chlimage_1-376.png)

### Configurar el resultado de la búsqueda agregada {#configure-the-added-search-result}

Seleccione el componente colocado al que desea acceder y seleccione el `Search Results` `Configure` icono que abre el cuadro de diálogo de edición.

![chlimage_1-377](assets/chlimage_1-377.png)

En la ficha Configuración **[!UICONTROL de resultados de]** búsqueda, es posible especificar qué rutas se incluyen en la búsqueda cuando un visitante introduce una consulta.

![chlimage_1-378](assets/chlimage_1-378.png)

* **[!UICONTROL Resultados de búsqueda por página]** Defina el número de temas/publicaciones que se muestran por página. El valor predeterminado es 10.

* **[!UICONTROL Rutas]** de búsqueda Al agregar rutas de búsqueda mediante el botón Agregar elemento, la búsqueda de contenido es limitada.

## Información adicional {#additional-information}

Puede encontrar más información en la página [Search Essentials](search-implementation.md) para desarrolladores.
