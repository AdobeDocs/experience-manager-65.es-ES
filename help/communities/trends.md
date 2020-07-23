---
title: Tendencias de Actividad
seo-title: Tendencias de Actividad
description: Añadir un componente de Lista de Actividad comunitaria en una página
seo-description: Añadir un componente de Lista de Actividad comunitaria en una página
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
translation-type: tm+mt
source-git-commit: 17088abc71bb820693259088c8a9b938a43cd9d3
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Tendencias de Actividad {#activity-trends}

## Introducción {#introduction}

El `Community Activity List` componente proporciona la capacidad de agregar información de tendencias con respecto a anuncios y vistas de miembros, así como anuncios y vistas de contenido.

El documento describe:

* Añadir el `Community Activity List` componente en un sitio [de](/help/communities/overview.md#community-sites)comunidad.

* Configuración del `Community Activity List` componente.

### Requisito {#requirement}

Los datos para el `Community Activity List` sitio solo están disponibles cuando Adobe Analytics tiene licencia y está configurado para el sitio de la comunidad.

Consulte las funciones de Configuración de [Analytics para comunidades](/help/communities/analytics.md).

### Añadir una Lista de Actividad de comunidad en una página {#adding-a-community-activity-list-to-a-page}

Para agregar un `Community Activity List` componente a una página en modo de autor, ubique el componente

* `Communities / Community Activity List`

y arrástrelo a su lugar en una página.

Para obtener la información necesaria, visite [Communities Components Basics](/help/communities/basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se coloca por primera vez en una página de un sitio de comunidad, así es como aparece el componente:

![comunidad-actividad](assets/community-activity.png)

### Configuración de la Lista de Actividad de la comunidad  {#configuring-community-activity-list}

Seleccione el componente colocado al que desea acceder y seleccione el `Community Activity List` `Configure` icono que abre el cuadro de diálogo de edición.

![chlimage_1-55](assets/chlimage_1-55.png)

En la ficha **Comentarios** , especifique si se mostrarán los comentarios de los archivos cargados y cómo se mostrarán:

![chlimage_1-56](assets/chlimage_1-56.png)

* **Tipo**

   Especifique si desea mostrar datos sobre miembros de la comunidad o contenido generado por el usuario (UGC).

   Seleccionar de:

   * `Members`
   * `Content`

   El valor predeterminado es `Members`.

* **Título que se mostrará**

   Un título descriptivo que se muestra encima de los datos, como `Trending Content`.
El valor predeterminado no es un título.

* **Número de de visualizaciones**

   Número de elementos que se van a lista.
El valor predeterminado es 10.

* **Tipo de actividad**

   Seleccione uno de los siguientes:

   * `Views`(visitas a la página)
   * `Posts`(creación de UGC)
   * `Follows`
   * `Likes`

   El valor predeterminado es Vistas.

* **Período de tiempo**

   Seleccione uno de los siguientes:

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`

   El valor predeterminado es `Total`.

* **Ruta de contexto**

   Proporciona la capacidad de ampliar el ámbito de la actividad a un subconjunto del sitio, como un blog específico.
El valor predeterminado es todo el sitio de la comunidad.

* **Suma de recuento de miembros**

   Cuando se anula la selección (se desactiva), solo se cuentan los anuncios de nivel superior. Por ejemplo, si el contexto es la página raíz (el valor predeterminado), un `Activity Type` de `Posts` nunca mostrará ninguna actividad, ya que no se puede publicar contenido en la página raíz. Cuando se selecciona, se incluyen los recuentos de todas las páginas descendientes.
El valor predeterminado está marcado.

### Ejemplo de página con 4 componentes {#example-page-with-components}

**Configuración de Visitantes** principales: Tipo = Miembros, tipo de Actividad = Vistas

**Configuración de colaboradores** principales: Tipo = Miembros, tipo de Actividad = Anuncios

**Configuración de contenido** superior: Tipo = Contenido, tipo de Actividad = Vistas,

**Configuración de contenido** de tendencias: Tipo = Contenido, tipo de Actividad = Anuncios

![chlimage_1-57](assets/chlimage_1-57.png)

