---
title: Consola de informes
seo-title: Consola de informes
description: Obtenga información sobre cómo acceder a los informes
seo-description: Obtenga información sobre cómo acceder a los informes
uuid: 7bb15a15-077b-4bfb-aaf4-50fddc67f237
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: fde053ff-b671-456b-869c-81f16ea1f1be
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Consola de informes{#reports-console}

## Información general {#overview}

Para Comunidades AEM, existen varios informes a los que se puede acceder de varias formas desde el entorno de creación.

En general, los diferentes informes son:

* [Informe](#assignments-report) de asignaciones: para una comunidad [de](/help/communities/overview.md#enablement-community)habilitación, proporciona una visión general del progreso de los alumnos en sus asignaciones, incluida una puntuación asociada si se implementa el estándar SCORM
* [Informe](#views-report) Vistas: proporciona un gráfico de las vistas del contenido por miembros de la comunidad y visitantes del sitio para cualquier sitio de la comunidad
* [Informe](#posts-report) Anuncios: proporciona un gráfico de los distintos tipos de anuncios de los miembros de la comunidad en cualquier sitio de la comunidad

Cuando [Adobe Analytics está habilitado](/help/communities/sites-console.md#analytics), los informes incluirán el número de vistas, reproducciones, comentarios y clasificaciones de cada recurso de activación con el paso del tiempo

Los informes tabulares se pueden exportar en formato .csv para su procesamiento posterior.

## Consolas de informes {#reporting-consoles}

### Informes para sitios de la comunidad {#reports-for-community-sites}

* desde la navegación global: **Navegación**, **Comunidades, Informes**

* elija entre

   * **Informe de asignaciones**

      * generar un informe para el sitio de la comunidad, el usuario o el grupo y la asignación seleccionados

      * **Informe de anuncios**

         * generar un informe para el sitio de la comunidad, el tipo de contenido y el período de tiempo seleccionados
      * **Informe de vistas**

         * generar un informe para el sitio de la comunidad, el tipo de contenido y el período de tiempo seleccionados


![chlimage_1-236](assets/chlimage_1-236.png)

### Informes para recursos de habilitación y rutas de aprendizaje {#reports-for-enablement-resources-and-learning-paths}

* desde la navegación global: **Navegación**, **Comunidades, Recursos**

* seleccionar un sitio de comunidad de habilitación existente

   * seleccione **Informe **icono para generar informes que cubran todos los recursos de habilitación
   * seleccionar una ruta de aprendizaje de habilitación
   * seleccione **Informe **icono para generar informes

      * los recursos de habilitación incluidos
      * los alumnos asignados a la ruta de aprendizaje

* estos informes proporcionan:

   * datos de tabla, descargables como CSV

      * identificación del alumno
      * su estado
      * si se ha asignado o se ha accedido a ellos a través del catálogo
      * número de observaciones formuladas
      * clasificación de estrella asignada

Para obtener más información, consulte la sección [](/help/communities/resources.md#report) Informes de la consola Recursos.

## Informe de asignaciones {#assignments-report}

La consola Asignaciones permite que los informes se filtren mediante la habilitación de sitios de la comunidad, usuarios o grupos, y la asignación.

En el informe se proporciona información sobre su progreso, así como sobre las observaciones o calificaciones que se hayan proporcionado.

![chlimage_1-237](assets/chlimage_1-237.png)

Seleccione los criterios para el informe:

* **Sitio**

   seleccionar un sitio de comunidad de habilitación

* **Usuario o grupo**
   * seleccione Usuario para generar un informe para un alumno
   * seleccione Grupo para generar un informe para un grupo de alumnos
   El servicio de túnel tendrá acceso a miembros y grupos de miembros desde el entorno de publicación

* **Asignación**

   Elija entre los recursos de habilitación asignados a los alumnos seleccionados

Seleccione **Generar** para crear el informe:

![chlimage_1-238](assets/chlimage_1-238.png)

## Informe de vistas {#views-report}

La consola Vistas permite que los informes se generen en las vistas de página según las características de la comunidad durante un período de tiempo determinado.

![chlimage_1-239](assets/chlimage_1-239.png)

Seleccione los criterios para el informe:

* **Sitio**

   seleccionar un sitio de comunidad

* **Tipo de contenido**

   puede elegir Todo el contenido o seleccionar una de las funciones presentes en el sitio

* intervalo de tiempo

   seleccionar uno de

   * Últimos 7 días
   * Últimos 30 días
   * Últimos 90 días
   * Año pasado

Seleccione **Generar** para crear el informe:

![chlimage_1-240](assets/chlimage_1-240.png)

## Informe de anuncios {#posts-report}

La consola Anuncios permite generar informes en función del número de anuncios de las funciones de la comunidad durante un período de tiempo determinado.

![chlimage_1-241](assets/chlimage_1-241.png)

Seleccione los criterios para el informe:

* **Sitio**

   seleccionar un sitio de comunidad

* **Tipo de contenido**

   puede elegir Todo el contenido o seleccionar una de las funciones presentes en el sitio

* intervalo de tiempo

   seleccionar uno de

   * Últimos 7 días
   * Últimos 30 días
   * Últimos 90 días
   * Año pasado

Seleccione **Generar** para crear el informe:

![chlimage_1-242](assets/chlimage_1-242.png)

## Solución de problemas {#troubleshooting}

### No hay sitios de comunidad enumerados {#no-community-sites-listed}

Si no aparece ningún sitio de la comunidad, asegúrese de que Adobe Analytics esté habilitado para un sitio. Si elige informes en las asignaciones, asegúrese de que la función de asignaciones se encuentra en la estructura del sitio de la comunidad.

### Los informes no se muestran en la instancia de AEM Author {#reports-do-not-show-in-aem-author-instance}

Si los informes no aparecen en la instancia de AEM Author, compruebe si hay personalizaciones, como la asignación de URL en la instancia de Publish. Si la asignación de URL solo se realiza en la instancia de AEM Publish del sitio de comunidades, asegúrese de que la misma se ha configurado en la instancia de AEM Author en la configuración **Informe de tendencias del sitio de Social Component Factory **configuración.

![Asignación de URL en AEM Author](assets/sitetrend.png)