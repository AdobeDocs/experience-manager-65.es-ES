---
title: Analizar el rendimiento de la página
seo-title: Analizar el rendimiento de la página
description: Utilice la página Perspectiva de contenido para analizar el rendimiento de la página que esté creando
seo-description: Utilice la página Perspectiva de contenido para analizar el rendimiento de la página que esté creando
uuid: 563d3e98-20d9-4cca-a174-bafd6e65c1bb
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 57cd61d5-78f2-4f8c-99ee-75e100c052ef
docset: aem65
translation-type: tm+mt
source-git-commit: cf0c80928bc9f6cfcf472fc5c75215b3812e2c7c

---


# Analizar el rendimiento de la página{#analyzing-page-performance}

Abra la página Perspectiva de contenido[](/help/sites-authoring/content-insights.md) para analizar el rendimiento de la página que esté creando. Configure el período de informe para centrar su análisis.

## Abrir Analítica y recomendaciones para una página {#opening-analytics-and-recommendations-for-a-page}

Utilice el procedimiento siguiente para ver Analítica y recomendaciones para una página:

1. Vaya a la página que desee analizar.
1. En la barra de herramientas, toque o haga clic en **Analítica y recomendaciones**.

   >[!NOTE]
   >
   >Analítica y recomendaciones para una página solo se muestra si ha configurado AEM para [integrarse con Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md).

   ![screen-shot_2019-03-05at115319](assets/screen-shot_2019-03-05at115319.png)

### Cambio del período de informe {#changing-the-reporting-period}

Cambie las siguientes proporciones temporales de los informes analíticos:

* El período de tiempo sobre el que se informa.
* La granularidad de los datos.

Las herramientas para cambiar las proporciones temporales de los informes aparecen en la parte superior de la página Perspectiva de contenido. ![chlimage_1-126](assets/chlimage_1-126.png)

#### Cambio del período de informe {#changing-the-reporting-period-1}

Cambie el período de informe de la página Perspectiva de contenido para centrar el análisis de la actividad de la página en un período de tiempo concreto. Al cambiar el período de informe, los informes se actualizan automáticamente. El área sombreada del intervalo de tiempo representa el período de informe. En el intervalo de tiempo, las fechas ascienden de izquierda a derecha.

![chlimage_1-127](assets/chlimage_1-127.png)

Para cambiar el período de informe de una página Perspectiva de contenido:

1. Si el período de tiempo no aparece en la parte superior de la página, toque o haga clic en el icono Alternar intervalo de tiempo.

   ![](do-not-localize/chlimage_1-22.png)

1. Para cambiar la fecha de inicio del período de informe, arrastre el círculo que aparece en la parte izquierda del área sombreada a la fecha de inicio deseada.

   Si no puede ver la parte izquierda del área sombreada, utilice la barra de desplazamiento para que se vea.

1. Para cambiar la fecha de finalización del período de informe, arrastre el círculo que aparece en la parte derecha del área sombreada a la fecha de finalización deseada.

#### Cambio de la granularidad del período de informe {#changing-the-granularity-of-the-reporting-period}

Cambie la cantidad de tiempo que cada punto de datos abarca en un informe. Por ejemplo, al seleccionar la granularidad Semana, cada punto de datos del informe Vistas representa la cantidad de vistas realizadas durante una semana.

![screen_shot_2017-11-29at141001](assets/screen_shot_2017-11-29at141001.png)

La granularidad afecta a los informes que asignan datos a valores temporales, como los informes Vistas y Promedio de minutos de visita de la página. La granularidad también afecta a la escala del período de tiempo.

1. Si no aparece el control de la granularidad, toque o haga clic en el icono Alternar granularidad.

   ![chlimage_1-128](assets/chlimage_1-128.png)

1. Toque o haga clic en la granularidad que desee. Una vez seleccionado, el informe se actualiza automáticamente para reflejar la granularidad.

### Asignación de tareas para Recomendaciones de SEO {#assigning-tasks-for-seo-recommendations}

Utilice el informe Recomendaciones de SEO para crear tareas para mejorar la visibilidad de la página para los motores de búsqueda. Para cada recomendación del informe que no tenga una marca, puede crear una tarea que asigna a un usuario para realizar el trabajo necesario.

![chlimage_1-129](assets/chlimage_1-129.png)

El estado de la recomendación de SEO indica cuándo se ha creado la tarea, pero aún no se ha completado.

![chlimage_1-130](assets/chlimage_1-130.png)

Una vez creada, la tarea aparece en la lista Tareas del usuario. Para obtener información sobre las tareas, consulte [Trabajo con tareas](/help/sites-authoring/task-content.md).

Siga el procedimiento que aparece a continuación para crear una tarea para una recomendación de SEO.

1. Toque o haga clic en el icono de información para la recomendación de SEO.

   ![](do-not-localize/chlimage_1-23.png)

1. Haga clic en el icono de triángulo dentro del círculo que aparece al lado del icono de información.

   ![chlimage_1-135](assets/chlimage_1-131.png)

1. Rellene los campos del formulario que aparecen y, a continuación, toque Crear:

   * Proyecto: seleccione el proyecto en el que se va a crear la tarea.
   * Nombre: el nombre que identifica la tarea. El nombre predeterminado es el título de la recomendación de SEO.
   * Asignar a: seleccione al usuario a quien asignará la tarea. Comience a escribir el nombre de usuario para filtrar la lista.
   * Descripción: una descripción de la actividad necesaria para completar la tarea. La descripción predeterminada es la información que acompaña a la recomendación de SEO.
   * Prioridad de tareas: la prioridad de la tarea.
   * Fecha de caducidad: la fecha en la que la tarea debe terminarse.
   **Nota**: la tarea creada también incluye la ruta de acceso a la página a la que se aplica la recomendación de SEO.

1. Toque o haga clic en Hecho para cerrar el mensaje Tarea creada.

