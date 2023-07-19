---
title: Tendencias de actividades
seo-title: Activity Trends
description: Adición de un componente de lista de actividades de la comunidad a una página
seo-description: Adding a Community Activity List component to a page
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 4%

---

# Tendencias de actividades {#activity-trends}

## Introducción {#introduction}

El `Community Activity List` Este componente permite agregar información de tendencias sobre las publicaciones y las vistas de los miembros, así como publicaciones y vistas del contenido.

El documento describe:

* Añadir el `Community Activity List` componente a [sitio comunitario](/help/communities/overview.md#community-sites).

* Ajustes de configuración para `Community Activity List` componente.

### Requisito {#requirement}

Datos de la `Community Activity List` solo está disponible cuando Adobe Analytics tiene licencia y está configurado para el sitio de la comunidad.

Consulte [Configuración de Analytics para funciones de Communities](/help/communities/analytics.md).

### Agregar una lista de actividades de la comunidad a una página {#adding-a-community-activity-list-to-a-page}

Para agregar un `Community Activity List` a una página en modo de autor, busque el componente

* `Communities / Community Activity List`

y arrástrela a su lugar en una página.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](/help/communities/basics.md).

Cuando se coloca por primera vez en una página de un sitio de la comunidad, así es como aparece el componente:

![actividad de la comunidad](assets/community-activity.png)

### Configurar la lista de actividades de comunidad  {#configuring-community-activity-list}

Seleccione el colocado `Community Activity List` para acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configurar](assets/configure-new.png)

En el **Comentarios** , especifique si aparecen los comentarios de los archivos cargados y cómo:

![propiedades](assets/activity-list-properties.png)

* **Tipo**

  Especifique si desea mostrar datos sobre los miembros de la comunidad o sobre el contenido generado por el usuario (UGC).

  Seleccionar de:

   * `Members`
   * `Content`

  El valor predeterminado es `Members`.

* **Título que se mostrará**

  Título descriptivo que se mostrará sobre los datos, como `Trending Content`.
El valor predeterminado es sin título.

* **Número de de visualizaciones**

  Número de elementos que se van a enumerar.
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

  Proporciona la capacidad de asignar el ámbito de la actividad a un subconjunto del sitio, como un blog específico.
De forma predeterminada, se muestra todo el sitio de la comunidad.

* **Suma de recuento de miembros**

  Cuando no está seleccionada (desactivada), solo se cuentan las publicaciones de nivel superior. Por ejemplo, si el contexto es la página raíz (el valor predeterminado), un `Activity Type` de `Posts` nunca mostrará ninguna actividad, ya que no hay capacidad para publicar contenido en la página raíz. Cuando se selecciona, se incluyen los recuentos de todas las páginas descendientes.
La opción predeterminada está activada.

### Página de ejemplo con 4 componentes {#example-page-with-components}

**Visitantes principales** config: Tipo = Miembros, Tipo de actividad = Vistas

**Colaboradores principales** config: Tipo = Miembros, Tipo de actividad = Entradas

**Contenido principal** config: Tipo = Contenido, Tipo de actividad = Vistas,

**Contenido de tendencias** config: Tipo = Contenido, Tipo de actividad = Publicaciones

![componentes](assets/activity-list-components.png)
