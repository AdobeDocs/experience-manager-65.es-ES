---
title: Tendencias de actividades
seo-title: Tendencias de actividades
description: Adición de un componente Lista de actividades de comunidad a una página
seo-description: Adición de un componente Lista de actividades de comunidad a una página
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Tendencias de actividades{#activity-trends}

## Introducción {#introduction}

El `Community Activity List` componente proporciona la capacidad de agregar información de tendencias con respecto a las publicaciones y vistas de los miembros, así como las publicaciones y vistas del contenido.

El documento describe:

* adición del `Community Activity List` componente a un sitio [de comunidad](/help/communities/overview.md#community-sites)

* configuración del `Community Activity List` componente

### Requisito {#requirement}

Los datos para el `Community Activity List` sitio solo están disponibles cuando Adobe Analytics tiene licencia y está configurado para el sitio de la comunidad.

Consulte Configuración [de Analytics para funciones](/help/communities/analytics.md)de comunidades.

### Adición de una lista de actividades de comunidad a una página {#adding-a-community-activity-list-to-a-page}

Para agregar un `Community Activity List` componente a una página en modo de autor, ubique el componente

* `Communities / Community Activity List`

y arrástrelo a su lugar en una página.

Para obtener la información necesaria, visite [Communities Components Basics](/help/communities/basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se coloca por primera vez en una página de un sitio de comunidad, así es como aparece el componente:

![chlimage_1-54](assets/chlimage_1-54.png)

### Configuración de la lista de actividades de la comunidad {#configuring-community-activity-list}

Seleccione el componente colocado al que desea acceder y seleccione el `Community Activity List` `Configure` icono que abre el cuadro de diálogo de edición.

![chlimage_1-55](assets/chlimage_1-55.png)

En la ficha **Comments **tab, especifique si los comentarios de los archivos cargados aparecen y cómo aparecerán:

![chlimage_1-56](assets/chlimage_1-56.png)

* **Tipo**

   Especifique si desea mostrar datos sobre miembros de la comunidad o contenido generado por el usuario (UGC).

   Seleccionar de

   * `Members`
   * `Content`
   El valor predeterminado es `Members`.

* **Título que se mostrará**

   Un título descriptivo que se muestra encima de los datos, como `Trending Content`.
El valor predeterminado no es un título.

* **Número de de visualizaciones**

   El número de elementos que se van a mostrar.
El valor predeterminado es 10.

* **Tipo de actividad**

   Seleccione uno de los

   * `Views`(visitas a la página)
   * `Posts`(creación de UGC)
   * `Follows`
   * `Likes`
   El valor predeterminado es Vistas.

* **Período de tiempo**

   Seleccione uno de los

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`
   El valor predeterminado es `Total`.

* **Ruta de contexto**

   Proporciona la capacidad de ampliar la actividad a un subconjunto del sitio, como un blog específico.
El valor predeterminado es todo el sitio de la comunidad.

* **Suma de recuento de miembros**

   Cuando se anula la selección (se desactiva), solo se cuentan los anuncios de nivel superior. Por ejemplo, si el contexto es la página raíz (el valor predeterminado), un `Activity Type`de nunca `Posts`mostrará ninguna actividad, ya que no se puede publicar contenido en la página raíz. Cuando se selecciona, se incluyen los recuentos de todas las páginas descendientes.
El valor predeterminado está marcado.

### Ejemplo de página con 4 componentes {#example-page-with-components}

**Configuración de visitantes** principales: Tipo = Miembros, tipo de actividad = Vistas

**Configuración de colaboradores** principales: Tipo = Miembros, Tipo de actividad = Anuncios

**Configuración de contenido** superior: Tipo = Contenido, Tipo de actividad = Vistas,

**Configuración de contenido** de tendencias: Tipo = Contenido, Tipo de actividad = Anuncios

![chlimage_1-57](assets/chlimage_1-57.png)

