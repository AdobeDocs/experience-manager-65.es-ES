---
title: Administración de actividades
seo-title: Administración de actividades
description: La consola Actividades permite crear, organizar y administrar las actividades de marketing de las marcas
seo-description: La consola Actividades permite crear, organizar y administrar las actividades de marketing de las marcas
uuid: 0aebf88e-f298-410a-8c82-4076b671624f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: ef2321a3-cd51-4298-8782-e1a2ca721868
docset: aem65
translation-type: tm+mt
source-git-commit: 90c99e527a40bb663d4f32d8746b46cf34a2319f
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 87%

---


# Administración de actividades{#managing-activities}

La consola Actividades permite crear, organizar y administrar las [actividades](/help/sites-authoring/personalization.md#activities) de marketing de las marcas.

* Añadir marcas.
* Añadir y configurar las actividades de cada marca.
* Administrar actividades.

>[!NOTE]
>
>Si utiliza Adobe Target como motor de segmentación, también puede [ver los datos de rendimiento de las actividades](#viewing-performance-and-converting-winning-experiences-a-b-test). Si utiliza la prueba A/B, puede [convertir los ganadores](#viewing-performance-and-converting-winning-experiences-a-b-test).

En la consola de actividades, las actividades se organizan según la marca. Puede utilizar marcas y carpetas para estructurar la organización de las actividades. Vaya a la consola de actividades; para ello, pulse o haga clic en **Personalización** y pulse o haga clic en **Actividades**.

Las actividades están disponibles en el modo de objetivo para [crear contenido de destino](/help/sites-authoring/content-targeting-touch.md), donde también puede crear actividades. Las actividades que cree en el modo Segmentación aparecerán en la consola de actividades.

Las actividades se muestran con una etiqueta que describe qué tipo de actividad se define:

* XT: segmentación de la experiencia de Adobe Target
* A/B: prueba de A/B de Adobe Target
* AEM: segmentación de Adobe Experience Manager (basado en contexthub o clientcontext)

![chlimage_1-114](assets/chlimage_1-114.png)

>[!NOTE]
>
>Los tipos de actividades estarán disponibles dependiendo de lo siguiente:
>
>* Si la opción **xt_only** está habilitada en el inquilino de Adobe Target (clientcode) que se usa en el lado AEM para conectar con Adobe Target, **solo** puede crear actividades de XT en AEM.
   >
   >
* Si las opciones **xt_only** **no** están habilitadas en el inquilino de Adobe Target (clientcode), puede crear **ambas** actividades de XT y de pruebas A/B en AEM.
>
>
**Nota adicional:** las opciones de **xt_only** son una configuración aplicada en un inquilino de Target (clientcode) y sólo se pueden modificar directamente en Adobe Target. No puede activar ni desactivar esta opción en AEM.

>[!CAUTION]
>
>Debe proteger el nodo de configuración de actividad **cq:ActivitySettings** en la instancia de publicación para que los usuarios normales no puedan acceder a él. El nodo de configuración de la actividad solo debe ser accesible para el servicio que administra la sincronización de actividades en Adobe Target.
>
>Consulte [Requisitos previos para la integración con Adobe Target](/help/sites-administering/target-requirements.md#securingtheactivitysettings) para obtener información detallada.

## Crear una marca mediante la consola de actividades {#creating-a-brand-using-the-activities-console}

Cree una marca para la que quiera administrar actividades de marketing.

Cuando crea una marca con la consola Actividades, también aparece en la consola [Ofertas](/help/sites-authoring/offerlib.md), donde puede crear ofertas para las experiencias de sus actividades.

1. En la consola de navegación, haga clic o pulse **Personalización**. Haga clic o pulse **Actividades**.

   ![screen_shot_2018-03-21at151821](assets/screen_shot_2018-03-21at151821.png)

1. En la consola de actividades, haga clic o pulse **Crear** y, a continuación, **Crear marca**.
1. Seleccione la plantilla de marca y haga clic o pulse **Siguiente**.
1. Escriba un título para la marca tal y como desea que aparezca en las consolas de actividades y de ofertas. De forma opcional, escriba o seleccione una o más etiquetas para asociarlas a la marca.
1. Haga clic o pulse **Crear**. La marca aparece en la consola de actividades.

## Añadir/editar una actividad mediante la consola de actividades {#adding-editing-an-activity-using-the-activities-console}

Añada una actividad o edite una actividad existente para centrar sus esfuerzos de marketing en audiencias más específicas. Cuando cree o edite una actividad, deberá indicar la siguiente información:

* **Nombre:** Nombre de la actividad.
* **Motor de segmentación:** [AEM](/help/sites-authoring/personalization.md#aem) o [Adobe Target](/help/sites-authoring/personalization.md#adobe-target) como motor del contenido segmentado.

* **Seleccione una configuración de Target:** (Solo Adobe Target) La configuración de nube que esta actividad debe utilizar para conectarse a Adobe Target. Esta opción solo aparece cuando Adobe Target está seleccionado como motor de segmentación.
* **Tipo de Actividad: **Tipo de actividad: Prueba A/B o segmentación de experiencias
* **Objetivo:** (Opcional) Una descripción de la actividad.
* **Experiencias:** Asignaciones entre los nombres de audiencia y los segmentos de marketing a los que está dirigiendo.
* **Porcentajes de tráfico:** Si se selecciona la prueba A/B, puede cambiar el tráfico (en porcentaje) que se destina a cada experiencia.
* **Duración:** Período de tiempo en el que se aplica la actividad.
* **Prioridad:** Prioridad relativa de la actividad. Cuando las actividades proporcionan contenido para los mismos segmentos de usuario, la actividad de la prioridad mayor prevalece por encima de la otra.
* **Métrica de objetivo:** Si Adobe Target está seleccionado como motor de determinación de objetivos, puede agregar métricas de éxito a la actividad. Se requiere una métrica de éxito.

>[!NOTE]
>
>Es necesario ***crear*** nuevas actividades de Adobe Target en el editor de contenido segmentado, no en la consola **Actividades**, ya que la sincronización con Adobe Target fallará.
>
>Sin embargo, puede editar las actividades existentes de Adobe Target en la consola.

Para añadir una actividad:

1. Toque o haga clic en la marca para la que está creando la actividad y, a continuación, toque o haga clic en **Crear **luego** Crear Actividad. **Si está editando, seleccione la actividad en la pantalla Área maestra y pulse o haga clic en **Editar actividad**.
1. Proporcione la información siguiente y, a continuación, haga clic o pulse **Siguiente**:

   * El nombre de la actividad.
   * El motor de búsqueda de segmentación que se va a usar. ContextHub (AEM) está seleccionada de forma predeterminada. Si necesita utilizar Adobe Target, cree la actividad en el editor de contenido de destino.
   * Si seleccionó Adobe Target como motor de segmentación, seleccione o edite la configuración de la nube que se utiliza para conectar con Adobe Target. (Procure no seleccionar un marco que haya creado para la configuración de la nube).
   * (Opcional) El objetivo o una descripción de la actividad.
   * Seleccione el tipo de actividad.

1. Agregue una o varias experiencias a la actividad. Pulse o haga clic en **Agregar experiencia**.
1. Si utiliza la segmentación AEM o la segmentación por experiencia de Adobe Target:

   1. Haga clic o toque **Seleccione Audiencia **y seleccione el segmento que destinatario su experiencia.
   1. Haga clic o pulse **Añadir experiencia**, escriba un nombre y haga clic o pulse **Aceptar**.

   1. Haga clic o pulse **Siguiente**.

   Si utiliza la prueba A/B de Adobe Target:

   1. Haga clic o pulse el lápiz en el cuadro de audiencias para seleccionar una audiencia.
   1. Haga clic o pulse **Añadir experiencia**, escriba un nombre y haga clic o pulse **Aceptar**.

   1. Especifique el porcentaje de tráfico que muestra cada experiencia.
   1. Haga clic o pulse **Siguiente**.


1. Para especificar el momento en que la actividad comenzará, use el menú desplegable **Inicio** para seleccionar uno de los siguientes valores:

   * **Cuando se activa:** la actividad se inicia cuando se active la página que contiene el contenido de destino.
   * **Fecha y hora especificadas:** una hora específica. Cuando seleccione esta opción, pulse o haga clic en el icono de calendario, seleccione una fecha y especifique la hora a la que desea iniciar la actividad.

1. Para especificar cuándo finaliza la actividad, utilice el menú desplegable final para seleccionar uno de los siguientes valores:

   * **Cuando se desactiva:** la actividad finaliza cuando la página que tiene el contenido de destino se desactiva.
   * **Fecha y hora especificadas**: una hora específica. Al seleccionar esta opción, toque o haga clic en el icono de calendario, seleccione una fecha y especifique la hora de finalización de la actividad.

1. Para especificar una prioridad de la actividad, utilice el regulador para seleccionar cualquier valor: **Baja**, **Normal** o **Alta**.
1. Si utiliza Adobe Target como motor de segmentación, seleccione qué desea medir con esta actividad. Consulte [Configuración de la Actividad y Configuración de objetivos](/help/sites-authoring/content-targeting-touch.md) para obtener más información sobre las métricas de éxito disponibles. Debe seleccionar por lo menos un objetivo.
1. Haga clic o pulse **Guardar**.

   >[!NOTE]
   >
   >Después de crear una actividad, debe publicarla de forma que esté disponible.

## Publicar y cancelar la publicación de actividades {#publishing-and-unpublishing-activities}

Debe publicar actividades para que puedan estar disponibles. Por el contrario, es posible que no quiera que las actividades estén disponibles al cancelar su publicación.

>[!NOTE]
>
>Al cancelar la publicación de una actividad, el estado de la actividad no cambia a menos que actualice la página.

Para publicar o cancelar la publicación de actividades:

1. Haga clic o pulse la marca y, a continuación, el área que contiene la actividad que quiera publicar o de la cual quiera cancelar la publicación.
1. Haga clic o pulse el icono junto a la actividad o actividades que desee publicar o cuya publicación quiera cancelar.

   ![screen-shot_2019-03-05at123846](assets/screen-shot_2019-03-05at123846.png)

1. Para publicar, pulse o haga clic en **Publicar**. Para cancelar la publicación, pulse o haga clic en **Cancelar publicación**. La actividad o actividades se publicarán (o no), y su estado cambiará en la consola de actividades (es posible que sea necesaria una actualización).

## Actividades en las instancias de Publicación y Autor  {#activities-on-author-and-publish-instances}

Cuando se activa una actividad que utiliza el motor de segmentación de Adobe Target, una segunda actividad se crea en la instancia de publicación:

* La actividad en la instancia de autor realiza el seguimiento de la actividad de la instancia de autor y resulta útil para simular la experiencia de los visitantes. El análisis que se grabó para esta actividad refleja únicamente lo que ocurre en la instancia de autor.
* La actividad de la instancia refleja y responde a la actividad en el servidor de publicación. Esta es la actividad que se ejecuta en el sitio web público. Publicar únicamente la actividad es importante si se quiere hacer el seguimiento y analizar el uso real del sitio público.

## Visualizar el rendimiento y convertir experiencias ganadoras (pruebas A/B)  {#viewing-performance-and-converting-winning-experiences-a-b-test}

Puede ver el rendimiento de cualquier actividad de Adobe Target (XT o A/B). Si utiliza la prueba A/B también puede convertir la experiencia ganadora, que a su vez se convertirá en la experiencia predeterminada.

Para ver el rendimiento de las actividades y convertirlas en experiencias ganadoras:

1. En **Personalización**, toque o haga clic en **Actividades** para navegar a la consola **Actividades**.
1. Haga clic o pulse la marca de la cual quiera ver actividades.
1. Seleccione la actividad y pulse o haga clic en **Ver propiedades**, seleccione la pestaña **Informes** y haga clic en la actividad para la que desee ver el rendimiento o convertir las experiencias ganadoras. Se muestran los datos de rendimiento.

   ![chlimage_1-115](assets/chlimage_1-115.png)

1. Toque o haga clic en el vínculo **Impulsar al ganador** para insertar esa experiencia como experiencia predeterminada.

   Convertir al ganador hace lo siguiente:

   * Desactiva la actividad actual
   * Modifica todas las páginas y reemplaza el contenido de destino con el contenido real de la experiencia ganadora. El contenido de la experiencia ganadora se convierte en parte de la página normal **sin** segmentación.

   ![chlimage_1-116](assets/chlimage_1-116.png)

   Una experiencia ganadora es la que más crece en los informes, y está basada en la tasa de conversión.

1. Haga clic o pulse **Sí** para confirmar que desea convertir el ganador, deshabilitar la experiencia actual y reemplazarla por el contenido de experiencia ganadora.

## Sincronizar actividades con Adobe Target  {#synchronizing-activities-with-adobe-target}

Las actividades que utilizan el motor de segmentación de Adobe Target se sincronizan con las campañas de Adobe Target. Una actividad se sincroniza automáticamente con Adobe Target cuando se cumplen las siguientes condiciones:

* La actividad contiene al menos una experiencia.
* Por lo menos una experiencia contiene un segmento asignado y una oferta.
* Cada experiencia de la actividad debe tener el mismo número de ofertas.

Estas condiciones se aplican a las actividades de las instancias de publicación y autor.

Cuando se sincroniza una actividad, se crea la campaña correspondiente en Adobe Target:

* Las actividades de la instancia de publicación tienen el mismo nombre que la campaña de Adobe Target correspondiente.
* Las actividades de la instancia de autor se corresponden con campañas de Destinatario del mismo nombre con el sufijo `_author`.

![chlimage_1-117](assets/chlimage_1-117.png)

Las actividades de _autor se sincronizan inmediatamente cuando se modifica la actividad. La sincronización inmediata permite la simulación de actividades con Client Context o ContextHub.

La publicación de actividades se sincroniza cuando la actividad está publicada en una instancia de publicación de AEM.

## Solución de problemas con la sincronización de la actividad  {#troubleshooting-activity-synchronization}

Cuando AEM sincroniza una actividad con Adobe Target, incluye una propiedad de la actividad denominada `thirdPartyId`. El valor de esta propiedad se basa en la ruta de acceso de la actividad del repositorio de AEM. Dos campañas de Adobe Target no pueden tener el mismo valor para la propiedad `thirdPartyId`. Por lo tanto, una actividad no se podrá sincronizar si una campaña existente (de un tipo AB o XT diferente) en Adobe Target utiliza el mismo valor para `thirdPartyId`.

Este problema también puede ocurrir en las siguientes circunstancias:

1. Una actividad se crea y se sincroniza con Adobe Target.
1. En otra instancia AEM, se crea una actividad según la misma marca y utiliza el mismo nombre. Se produce un error al intentar sincronizar esta actividad.

Este problema también puede ocurrir en las siguientes circunstancias:

1. Una actividad se crea y se sincroniza con Adobe Target. La actividad se eliminará de AEM.
1. Una actividad se crea según la misma marca y se usa el mismo nombre que el de la actividad eliminada. Se produce un error al intentar sincronizar esta actividad.

Para evitar problemas de sincronización, use siempre nombres exclusivos para las actividades. Si una actividad no se sincroniza, puede eliminar la campaña en Adobe Target que utilice el mismo nombre si dicha campaña no se está utilizando.

>[!NOTE]
>
>Cuando se crea una campaña en Adobe Target, se asigna una propiedad denominada `thirdPartyId t`a cada campaña. Cuando elimine una campaña en Adobe Target, la propiedad `thirdPartyId` no se eliminará. No puede volver a utilizar `thirdPartyId` para las campañas de distintos tipos (AB, XT) y no se puede quitar manualmente. Para evitar este problema, asigne a cada campaña un nombre único; Por lo tanto, los nombres de campaña no pueden reutilizarse en diferentes tipos de campaña.
>
>Si utiliza el mismo nombre en el mismo tipo de campaña, sobrescribirá la campaña existente.
>
>Si al sincronizar se muestra el mensaje de error “Se ha producido un error en la solicitud. `thirdPartyId` ya existe”, cambie el nombre de la campaña y vuelva a sincronizar.

