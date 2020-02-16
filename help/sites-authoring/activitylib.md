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
source-git-commit: d53e72b198db91d368ddddac768d19b88ee29050

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

Activities are available in Targeting mode for [authoring targeted content](/help/sites-authoring/content-targeting-touch.md), where you can also create activities. Las actividades que cree en el modo Segmentación aparecerán en la consola de actividades.

Las actividades se muestran con una etiqueta que describe qué tipo de actividad se define:

* XT: segmentación de la experiencia de Adobe Target
* A/B: prueba de A/B de Adobe Target
* AEM: segmentación de Adobe Experience Manager (basado en contexthub o clientcontext)

![chlimage_1-114](assets/chlimage_1-114.png)

>[!NOTE]
>
>Los tipos de actividades estarán disponibles dependiendo de lo siguiente:

>* Si la opción **xt_only** está habilitada en el inquilino de Adobe Target (clientcode) que se usa en el lado AEM para conectar con Adobe Target, **solo** puede crear actividades de XT en AEM.
   >
* Si las opciones **xt_only** **no** están habilitadas en el inquilino de Adobe Target (clientcode), puede crear **ambas** actividades de XT y de pruebas A/B en AEM.

**Nota adicional:** las opciones de **xt_only** son una configuración aplicada en un inquilino de Target (clientcode) y sólo se pueden modificar directamente en Adobe Target. No se puede activar o desactivar esta opción en AEM.

>[!CAUTION]
You must secure the activity settings node **cq:ActivitySettings** on the publish instance so that it is inaccessible to normal users. El nodo de configuración de la actividad solo debe ser accesible para el servicio que administra la sincronización de actividades en Adobe Target.
See [Prerequisites for Integrating with Adobe Target](/help/sites-administering/target-requirements.md#securingtheactivitysettings) for detailed information.

## Crear una marca mediante la consola de actividades {#creating-a-brand-using-the-activities-console}

Cree una marca para la que quiera administrar actividades de marketing.

When you create a brand using the Activities console, it also appears in the [Offers console](/help/sites-authoring/offerlib.md) where you can create offers for the experiences of your activities.

1. En la consola de navegación, haga clic o pulse **Personalización**. Haga clic o pulse **Actividades**.

   ![screen_shot_2018-03-21at151821](assets/screen_shot_2018-03-21at151821.png)

1. En la consola de actividades, haga clic o pulse **Crear** y, a continuación, **Crear marca**.
1. Seleccione la plantilla de marca y haga clic o pulse **Siguiente**.
1. Escriba un título para la marca tal y como desea que aparezca en las consolas de actividades y de ofertas. De forma opcional, escriba o seleccione una o más etiquetas para asociarlas a la marca.
1. Haga clic o pulse **Crear**. La marca aparece en la consola de actividades.

## Añadir/editar una actividad mediante la consola de actividades {#adding-editing-an-activity-using-the-activities-console}

Añada una actividad o edite una actividad existente para centrar sus esfuerzos de marketing en audiencias más específicas. Cuando cree o edite una actividad, deberá indicar la siguiente información:

* **Nombre:** el nombre de la actividad.
* **Motor de segmentación:** [AEM](/help/sites-authoring/personalization.md#aem) o [ Adobe Target](/help/sites-authoring/personalization.md#adobe-target) como motor de búsqueda para el contenido de destino.

* **Seleccionar una configuración de Target:** (Adobe Target solamente) la configuración de nube que esta actividad debe utilizar para conectarse a Adobe Target. Esta opción solo aparece cuando se selecciona Adobe Target en el motor de segmentación.
* **Tipo de actividad: **El tipo de actividad: Prueba A/B o Segmentación de experiencias
* **Objetivo:** (opcional) descripción de la actividad.
* **Experiencias:** asignaciones entre los nombres de audiencia y los segmentos de marketing que desea utilizar.
* **** Porcentajes de tráfico: Si se selecciona la prueba A/B, puede cambiar el tráfico (en porcentaje) que se destina a cada experiencia.
* **Duración:** cantidad de tiempo para aplicar la actividad.
* **Prioridad:** la prioridad relativa de la actividad. Cuando las actividades proporcionan contenido para los mismos segmentos de usuarios, predomina la actividad de mayor prioridad.
* **** Métrica de objetivo: Si Adobe Target está seleccionado como motor de determinación de objetivos, puede agregar métricas de éxito a la actividad. Es obligatoria una métrica válida.

>[!NOTE]
Las nuevas actividades de Adobe Target deben ***crearse*** en el editor de contenido de destino, y no en la consola **Actividades**, ya que se podría producir un error en la sincronización con Adobe Target.
Sin embargo, puede editar las actividades existentes de Adobe Target en la consola.

Para añadir una actividad:

1. Click or tap the brand for which you are creating the activity, and then click or tap **Create **then** Create Activity. **If editing, select the activity in the Master Area screen and clicking or tapping **Edit Activity**.
1. Proporcione la información siguiente y, a continuación, haga clic o pulse **Siguiente**:

   * El nombre de la actividad.
   * El motor de búsqueda de segmentación que se va a usar. ContextHub (AEM) está seleccionada de forma predeterminada. Si necesita utilizar Adobe Target, cree la actividad en el editor de contenido de destino.
   * Si seleccionó Adobe Target como motor de segmentación, seleccione o edite la configuración de la nube que se utiliza para conectar con Adobe Target. (Procure no seleccionar un marco que haya creado para la configuración de la nube).
   * (Opcional) El objetivo o una descripción de la actividad.
   * Seleccione el tipo de actividad.

1. Añada una o más experiencias a la actividad. Haga clic o pulse **Añadir experiencia**.
1. Si utiliza la segmentación AEM o la segmentación por experiencia de Adobe Target:

   1. Toque o haga clic en **Seleccionar audiencia **y seleccione el segmento al que se dirige la experiencia.
   1. Haga clic o pulse **Añadir experiencia**, escriba un nombre y haga clic o pulse **Aceptar**.

   1. Haga clic o pulse **Siguiente**.
   Si utiliza la prueba A/B de Adobe Target:

   1. Haga clic o pulse el lápiz en el cuadro de audiencias para seleccionar una audiencia.
   1. Haga clic o pulse **Añadir experiencia**, escriba un nombre y haga clic o pulse **Aceptar**.

   1. Especifique el porcentaje de tráfico que muestra cada experiencia.
   1. Haga clic o pulse **Siguiente**.


1. Para especificar el momento en que la actividad comenzará, use el menú desplegable **Inicio** para seleccionar uno de los siguientes valores:

   * **Cuando se activa:** la actividad se inicia cuando se active la página que contiene el contenido de destino.
   * **Fecha y hora especificadas:** una hora específica. Al seleccionar esta opción, toque o haga clic en el icono de calendario, seleccione una fecha y especifique la hora de inicio de la actividad.

1. Para especificar cuándo finaliza la actividad, utilice el menú desplegable final para seleccionar uno de los siguientes valores:

   * **Cuando se desactiva:** la actividad finaliza cuando la página que tiene el contenido de destino se desactiva.
   * **Fecha y hora especificadas**: una hora específica. Al seleccionar esta opción, toque o haga clic en el icono de calendario, seleccione una fecha y especifique la hora de finalización de la actividad.

1. Para especificar una prioridad de la actividad, utilice el regulador para seleccionar cualquier valor: **Baja**, **Normal** o **Alta**.
1. Si utiliza Adobe Target como motor de segmentación, seleccione qué desea medir con esta actividad. See [Configuring the Activity and Setting Goals](/help/sites-authoring/content-targeting-touch.md) for more information on the success metrics available. Debe seleccionar por lo menos un objetivo.
1. Haga clic o pulse **Guardar**.

   >[!NOTE]
   Después de crear una actividad, debe publicarla de forma que esté disponible.

## Publicar y cancelar la publicación de actividades {#publishing-and-unpublishing-activities}

Debe publicar actividades para que puedan estar disponibles. Por el contrario, es posible que no quiera que las actividades estén disponibles al cancelar su publicación.

>[!NOTE]
Cuando se cancela la publicación de una actividad,

Para publicar o cancelar la publicación de actividades:

1. Haga clic o pulse la marca y, a continuación, el área que contiene la actividad que quiera publicar o de la cual quiera cancelar la publicación.
1. Haga clic o pulse el icono junto a la actividad o actividades que desee publicar o cuya publicación quiera cancelar.

   ![screen-shot_2019-03-05at123846](assets/screen-shot_2019-03-05at123846.png)

1. Para publicar, pulse o haga clic en **Publicar**. Para cancelar la publicación, pulse o haga clic en **Cancelar publicación**. La actividad o actividades se publicarán (o no), y su estado cambiará en la consola de actividades (es posible que sea necesaria una actualización).

## Actividades en las instancias de Publicación y Autor {#activities-on-author-and-publish-instances}

Cuando se activa una actividad que utiliza el motor de segmentación de Adobe Target, una segunda actividad se crea en la instancia de publicación:

* La actividad en la instancia de autor realiza el seguimiento de la actividad de la instancia de autor y resulta útil para simular la experiencia de los visitantes. El análisis que se grabó para esta actividad refleja únicamente lo que ocurre en la instancia de autor.
* La actividad de la instancia refleja y responde a la actividad en el servidor de publicación. Esta es la actividad que se ejecuta en el sitio web público. Publicar únicamente la actividad es importante si se quiere hacer el seguimiento y analizar el uso real del sitio público.

## Visualizar el rendimiento y convertir experiencias ganadoras (pruebas A/B) {#viewing-performance-and-converting-winning-experiences-a-b-test}

Puede ver el rendimiento de cualquier actividad de Adobe Target (XT o A/B). Si utiliza la prueba A/B también puede convertir la experiencia ganadora, que a su vez se convertirá en la experiencia predeterminada.

Para ver el rendimiento de las actividades y convertirlas en experiencias ganadoras:

1. In **Personalization**, click or tap **Activities** to navigate to the **Activities** console.
1. Haga clic o pulse la marca de la cual quiera ver actividades.
1. Select the activity and click or tap **View Properties** and click the **Reports** tab and select the activity that you want to view performance for/convert winning experiences for. Se muestran los datos de rendimiento.

   ![chlimage_1-115](assets/chlimage_1-115.png)

1. Click or tap the **Push winner** link to push that experience as the default experience.

   Convertir al ganador hace lo siguiente:

   * Desactiva la actividad actual
   * Modifica todas las páginas y reemplaza el contenido de destino con el contenido real de la experiencia ganadora. The content of the winning experience becomes part of the normal page **without** targeting.
   ![chlimage_1-116](assets/chlimage_1-116.png)

   Una experiencia ganadora es la que más crece en los informes, y está basada en la tasa de conversión.

1. Haga clic o pulse **Sí** para confirmar que desea convertir el ganador, deshabilitar la experiencia actual y reemplazarla por el contenido de experiencia ganadora.

## Sincronizar actividades con Adobe Target {#synchronizing-activities-with-adobe-target}

Las actividades que utilizan el motor de segmentación de Adobe Target se sincronizan con las campañas de Adobe Target. Una actividad se sincroniza automáticamente con Adobe Target cuando se cumplen las siguientes condiciones:

* La actividad contiene al menos una experiencia.
* Por lo menos una experiencia contiene un segmento asignado y una oferta.
* Cada experiencia de la actividad debe tener el mismo número de ofertas.

Estas condiciones se aplican a las actividades de las instancias de publicación y autor.

Cuando se sincroniza una actividad, se crea la campaña correspondiente en Adobe Target:

* Las actividades de la instancia de publicación tienen el mismo nombre que la campaña de Adobe Target correspondiente.
* Activities on the author instance correspond with Target campaigns of the same name with the `_author` suffix.

![chlimage_1-117](assets/chlimage_1-117.png)

Las actividades de _autor se sincronizan inmediatamente cuando se modifica la actividad. La sincronización inmediata permite la simulación de actividades con Client Context o ContextHub.

La publicación de actividades se sincroniza cuando la actividad está publicada en una instancia de publicación de AEM.

## Solución de problemas con la sincronización de la actividad {#troubleshooting-activity-synchronization}

Cuando AEM sincroniza una actividad con Adobe Target, incluye una propiedad de la actividad denominada `thirdPartyId`. El valor de esta propiedad se basa en la ruta de acceso de la actividad del repositorio de AEM. Dos campañas de Adobe Target no pueden tener el mismo valor para la propiedad `thirdPartyId`. Por lo tanto, una actividad no se podrá sincronizar si una campaña existente (de un tipo AB o XT diferente) en Adobe Target utiliza el mismo valor para `thirdPartyId`.

Este problema también puede ocurrir en las siguientes circunstancias:

1. Una actividad se crea y se sincroniza con Adobe Target.
1. En otra instancia AEM, se crea una actividad según la misma marca y utiliza el mismo nombre. Se produce un error al intentar sincronizar esta actividad.

Este problema también puede ocurrir en las siguientes circunstancias:

1. Una actividad se crea y se sincroniza con Adobe Target. La actividad se eliminará de AEM.
1. Una actividad se crea según la misma marca y se usa el mismo nombre que el de la actividad eliminada. Se produce un error al intentar sincronizar esta actividad.

Para evitar problemas de sincronización, use siempre nombres exclusivos para las actividades. Si una actividad no se sincroniza, puede eliminar la campaña en Adobe Target que utilice el mismo nombre si dicha campaña no se está utilizando.

>[!NOTE]
When you create a campaign in Adobe Target, it assigns a property called `thirdPartyId t`o each campaign. Cuando elimine una campaña en Adobe Target, la propiedad `thirdPartyId` no se eliminará. No puede volver a utilizar `thirdPartyId` para las campañas de distintos tipos (AB, XT) y no se puede quitar manualmente. Para evitar este problema, asigne a cada campaña un nombre único; por lo tanto, los nombres de campaña no se pueden reutilizar en diferentes tipos de campaña.
Si utiliza el mismo nombre en el mismo tipo de campaña, sobrescribirá la campaña existente.
Si al sincronizar se muestra el mensaje de error “Se ha producido un error en la solicitud. `thirdPartyId` ya existe”, cambie el nombre de la campaña y vuelva a sincronizar.

