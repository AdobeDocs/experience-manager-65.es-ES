---
title: Tendencias de actividad
seo-title: Activity Trends
description: Adición de un componente de Lista de actividades de la comunidad a una página
seo-description: Adding a Community Activity List component to a page
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 4%

---

# Tendencias de actividad {#activity-trends}

## Introducción {#introduction}

La variable `Community Activity List` proporciona la capacidad de agregar información de tendencias con respecto a anuncios y vistas por miembros, así como anuncios y vistas de contenido.

El documento describe:

* Adición de la variable `Community Activity List` componente a un [sitio de la comunidad](/help/communities/overview.md#community-sites).

* Ajustes de configuración para `Community Activity List` componente.

### Requisito {#requirement}

Los datos del `Community Activity List` solo está disponible cuando Adobe Analytics tiene licencia y está configurado para el sitio de la comunidad.

Consulte [Funciones de Configuración de Analytics para Communities](/help/communities/analytics.md).

### Adición de una lista de actividades de la comunidad a una página {#adding-a-community-activity-list-to-a-page}

Para agregar un `Community Activity List` a una página en modo de autor, busque el componente

* `Communities / Community Activity List`

y arrástrela a su lugar en una página.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de Communities](/help/communities/basics.md).

Cuando se coloca por primera vez en una página de un sitio de comunidad, así es como aparece el componente:

![actividad de la comunidad](assets/community-activity.png)

### Configuración de la lista de actividades de la comunidad  {#configuring-community-activity-list}

Seleccione la colocación `Community Activity List` para acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configure](assets/configure-new.png)

En el **Comentarios** especifique si aparecen los comentarios de los archivos cargados y cómo aparecerán:

![propiedades](assets/activity-list-properties.png)

* **Tipo**

   Especifique si desea mostrar datos sobre los miembros de la comunidad o el contenido generado por el usuario (UGC).

   Seleccione entre:

   * `Members`
   * `Content`

   El valor predeterminado es `Members`.

* **Título que se mostrará**

   Un título descriptivo que se mostrará encima de los datos, como `Trending Content`.
El valor predeterminado no es título.

* **Número de de visualizaciones**

   El número de elementos que desea enumerar.
El valor predeterminado es 10.

* **Tipo de actividad**

   Seleccione una de las siguientes opciones:

   * `Views`(visitas a la página)
   * `Posts`(creación de UGC)
   * `Follows`
   * `Likes`

   El valor predeterminado es Vistas.

* **Período de tiempo**

   Seleccione una de las siguientes opciones:

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`

   El valor predeterminado es `Total`.

* **Ruta de contexto**

   Proporciona la capacidad de ampliar el ámbito de la actividad a un subconjunto del sitio, como un Blog específico.
El valor predeterminado es todo el sitio de la comunidad.

* **Suma de recuento de miembros**

   Cuando se anula la selección (se desactiva), solo se cuentan los anuncios de nivel superior. Por ejemplo, si el contexto es la página raíz (el valor predeterminado), se muestra una `Activity Type` de `Posts` nunca mostrará ninguna actividad, ya que no se puede publicar contenido en la página raíz. Cuando se selecciona, se incluyen los recuentos de todas las páginas descendientes.
El valor predeterminado está marcado.

### Página de ejemplo con 4 componentes {#example-page-with-components}

**Visitantes principales** config: Tipo = Miembros, Tipo de actividad = Vistas

**Colaboradores principales** config: Tipo = Miembros, Tipo de actividad = Anuncios

**Contenido principal** config: Tipo = Contenido, Tipo de actividad = Vistas,

**Tendencias de contenido** config: Tipo = Contenido, Tipo de actividad = Anuncios

![componentes](assets/activity-list-components.png)
