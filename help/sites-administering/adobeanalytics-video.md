---
title: Configuración del seguimiento de vídeo para Adobe Analytics
seo-title: Configuring Video Tracking for Adobe Analytics
description: Obtenga información sobre la configuración del seguimiento de vídeo para SiteCatalyst.
seo-description: Learn about configuring video tracking for SiteCatalyst.
uuid: 5a862f05-abfa-42a2-ad40-4c1c32f1bd75
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: a18ddac1-9e4c-4857-9cb3-4d5eeb8dd9ec
docset: aem65
exl-id: 5d51f898-b6d1-40ac-bdbf-127cda1dc777
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 2%

---

# Configuración del seguimiento de vídeo para Adobe Analytics{#configuring-video-tracking-for-adobe-analytics}

Hay varios métodos disponibles para rastrear eventos de vídeo, dos de los cuales son opciones heredadas de versiones anteriores de Adobe Analytics. Estas opciones heredadas son: Hitos heredados y segundos heredados

>[!NOTE]
>
>Antes de continuar, asegúrese de que tiene un **vídeo reproducible** cargado en AEM.
>
>Para asegurarse de que los vídeos se reproducen en la página, consulte **[este tutorial](/help/sites-authoring/default-components-foundation.md#video)** para obtener información sobre cómo transcodificar archivos de vídeo en AEM.

Utilice el siguiente procedimiento para configurar un marco para el seguimiento de vídeo con cada método.

>[!NOTE]
>
>Para nuevas implementaciones, se recomienda que **no use** las opciones heredadas para el seguimiento de vídeo. Utilice el **Hitos** en su lugar.

## Pasos comunes {#common-steps}

1. Configurar una página web arrastrando un **componente de vídeo** desde la barra de tareas y agregando una tabla **vídeo como recurso** para el componente

1. [Crear una configuración y un marco de Adobe Analytics](/help/sites-administering/adobeanalytics.md).

   * Los ejemplos de las secciones siguientes utilizan el nombre **my-sc-configuration** para la configuración y **videofw** para el marco.

1. En la página del marco, seleccione un RSID y establezca el uso en todos. ([https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html](https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html))
1. En la categoría Componentes generales de la barra de tareas, arrastre el componente Vídeo al marco.
1. Seleccione un método de seguimiento:

   * [Hitos](/help/sites-administering/adobeanalytics.md)
   * [Hitos no heredados](/help/sites-administering/adobeanalytics.md)
   * [Hitos heredados](/help/sites-administering/adobeanalytics.md)
   * [Segundos heredados](/help/sites-administering/adobeanalytics.md)

1. Al seleccionar un método de seguimiento, la lista de variables de CQ cambia en consecuencia. Utilice las secciones siguientes para obtener información sobre cómo seguir configurando el componente y asignar las variables de CQ con propiedades de Adobe Analytics.

## Hitos {#milestones}

El método Milestones rastrea la mayor cantidad de información sobre el vídeo, es altamente personalizable y fácil de configurar.

Para utilizar el método Milestones , especifique desplazamientos de seguimiento basados en el tiempo para definir los hitos. Cuando una reproducción de vídeo supera un hito, la página llama a Adobe Analytics para rastrear el evento. Para cada hito que defina, el componente crea una variable de CQ que puede asignar a una propiedad de Adobe Analytics. El nombre de estas variables de CQ utiliza el siguiente formato:

```shell
eventdata.events.milestoneXX
```

El sufijo XX es el desplazamiento de la pista que define el hito. Por ejemplo, si se especifican desplazamientos de seguimiento de 4, 8, 16, 20 y 28 segundos, se generan las siguientes variables de CQ:

* `eventdata.events.milestone4`
* `eventdata.events.milestone8`
* `eventdata.events.milestone16`
* `eventdata.events.milestone20`
* `eventdata.events.milestone28`

La siguiente tabla describe las variables de CQ predeterminadas que se proporcionan para el método Milestones:

<table>
 <tbody>
  <tr>
   <th>Variables CQ</th>
   <th>Propiedades de Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>Las variables asignadas a esta opción contendrán la variable <strong>fácil de usar</strong> name (<strong>Título</strong>) del vídeo si se configura en el DAM; si no se configura, el informe <strong>nombre de archivo</strong> se enviará en su lugar. Solo se envía una vez, al principio de la reproducción de un vídeo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>Las variables asignadas a esta función contendrán el nombre del archivo. Solo se envía junto con eventdata.events.a.media.view </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>Las variables asignadas a esto contendrán la ruta del archivo en el servidor. Solo se envía junto con eventdata.events.a.media.view </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>Se envía cada vez que se pasa un hito del segmento </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>Se envía cada vez que se activa un hito, junto con este evento, el número de segundos que el usuario ha visto un segmento determinado. Por ejemplo, eventX=21<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>Enviado al inicializar la vista de vídeo</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>Se envía cuando el vídeo termina de reproducirse<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestoneX </td>
   <td>Se envía cuando se pasa el hito determinado, X representa el segundo en el que se activa el hito<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>Enviado en cada hito; aparece como pev3 en la llamada de Adobe Analytics, normalmente enviada como "video"<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>Coincide exactamente con eventdata.videoName </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>Contiene información sobre el segmento que se ha visto, por ejemplo, 2:O:4-8 </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Puede configurar el **fácil de usar** abra el vídeo para editarlo en DAM y configure la variable **Título** campo de metadatos con el nombre deseado.

1. Después de seleccionar Hitos como método de seguimiento, en el cuadro Desplazamiento de seguimiento , introduzca una lista de desplazamientos de seguimiento en segundos separados por coma. Por ejemplo, el siguiente valor define hitos a los 4, 8, 16, 20 y 28 segundos después del inicio del vídeo:

   ```xml
   4,8,16,20,24
   ```

   Los valores de desplazamiento deben ser números enteros buenos a 0. El valor predeterminado es `10,25,50,75`.

1. Para asignar las variables de CQ a las propiedades de Adobe Analytics, arrastre las propiedades de Adobe Analytics desde ContentFinder al lado de la variable de CQ en el componente.

   Para obtener información sobre la optimización de las asignaciones, consulte la [Medición de vídeo en Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html) guía.

1. [Agregar el marco](/help/sites-administering/adobeanalytics.md) a la página.
1. Para probar la configuración en **Modo de vista previa**, reproduzca el vídeo para obtener llamadas de Adobe Analytics al déclencheur.

Los ejemplos de datos de seguimiento de Adobe Analytics que se indican a continuación se aplican al seguimiento de Milestone mediante desplazamientos de seguimiento de 4, 8, 16, 20 y 24, y las siguientes asignaciones para las variables de CQ:

<table>
 <tbody>
  <tr>
   <th>variable de CQ</th>
   <th>Propiedad Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>prop2</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>prop3 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>prop4</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>event1</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>event2<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>event3</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>event4<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestone4</td>
   <td>event10</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone8</td>
   <td>event11</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone16</td>
   <td>event12</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone20</td>
   <td>event13</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone24</td>
   <td>event14</td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>eVar3</td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>eVar1, prop1 </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>eVar2</td>
  </tr>
 </tbody>
</table>

Para este ejemplo, el componente Vídeo aparece de la siguiente manera en la página del marco:

![video1](assets/video1.png)

>[!NOTE]
>
>Para ver las llamadas realizadas a Adobe Analytics, utilice una herramienta adecuada, como DigitalPulse Debugger o Fiddler.

Las llamadas a Adobe Analytics que utilizan el ejemplo proporcionado deben tener este aspecto cuando se visualizan con DigitalPulse Debugger:

![chlimage_1-128](assets/chlimage_1-128.png)

*Esta es la **primera llamada**realizado en Adobe Analytics que contiene los siguientes valores:*

* *prop1 y eVar1 para eventdata.a.media.name,*
* *props2-4, junto con eVar2 y eVar3 que contienen contentType (vídeo) y segment (1):O:1-4)*
* *event3 que se asignó a eventdata.events.a.media.view.*

![chlimage_1-129](assets/chlimage_1-129.png)

*Esta es la **tercera llamada**realizado en Adobe Analytics:*

* *prop1 y eVar1 contienen a.media.name;*
* *event1 porque se ha visto un segmento*
* *event2 enviado con tiempo de reproducción = 4*
* *event11 enviado porque se ha alcanzado eventdata.events.milestone8*
* *no se envían prop2 a 4 (ya que no se activó event.events.a.media.view )*

## Hitos no heredados {#non-legacy-milestones}

El método de hitos no heredados es similar al método de hitos , excepto que los hitos se definen mediante porcentajes de la longitud de la pista. Las características comunes son las siguientes:

* Cuando una reproducción de vídeo supera un hito, la página llama a Adobe Analytics para rastrear el evento.
* La variable [conjunto estático de variables CQ](#cqvars) que se definen para la asignación con propiedades de Adobe Analytics.
* Para cada hito que defina, el componente crea una variable de CQ que puede asignar a una propiedad de Adobe Analytics.

El nombre de estas variables de CQ utiliza el siguiente formato:

El sufijo XX es el porcentaje de longitud de la pista que define el hito. Por ejemplo, si se especifican porcentajes de 10, 25, 50 y 75, se generan las siguientes variables de CQ:

* `eventdata.events.milestone10`
* `eventdata.events.milestone25`
* `eventdata.events.milestone50`
* `eventdata.events.milestone75`

```shell
eventdata.events.milestoneXX
```

1. Después de seleccionar los hitos no heredados como método de seguimiento, en el cuadro Rastrear desplazamiento, introduzca una lista separada por comas de los porcentajes de la longitud de la pista. Por ejemplo, el siguiente valor predeterminado define hitos en el 10, 25, 50 y 75 por ciento de la longitud de la pista:

   ```xml
   10,25,50,75
   ```

   Los valores de desplazamiento deben ser números enteros buenos a 0.

1. Para asignar las variables de CQ a las propiedades de Adobe Analytics, arrastre las propiedades de Adobe Analytics desde ContentFinder al lado de la variable de CQ en el componente.

   Para obtener información sobre la optimización de las asignaciones, consulte la [Medición de vídeo en Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html) guía.

1. [Agregar el marco](/help/sites-administering/adobeanalytics.md) a la página.
1. Para probar la configuración en **Modo de vista previa**, reproduzca el vídeo para obtener llamadas de Adobe Analytics al déclencheur.

## Hitos heredados {#legacy-milestones}

Este método es similar al método Milestones con la diferencia de que los hitos especificados en la variable *Desplazamiento de seguimiento* son porcentajes en lugar de puntos establecidos dentro del vídeo.

>[!NOTE]
>
>El campo Desplazamiento de seguimiento solo acepta una lista separada por comas que contiene números enteros entre 1 y 100.

1. Establezca el desplazamiento de la pista.

   * e.g.10,50,75,100

   Además, la información enviada a Adobe Analytics es menos personalizable; solo hay 3 variables disponibles para la asignación:

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>Las variables asignadas a esta opción contendrán la variable <strong>fácil de usar</strong> name (<strong>Título</strong>) del vídeo si se configura en el DAM; si no se configura el título, el vídeo <strong>nombre de archivo</strong> se enviará en su lugar. Solo se envía una vez, al principio de la reproducción de un vídeo.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>Las variables asignadas a esta función contendrán el nombre del archivo. Solo se envía una vez, al principio de la reproducción de un vídeo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>Variable asignada a esto contendrá la ruta del archivo en el servidor. Solo se envía una vez, al principio de la reproducción de un vídeo.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Puede configurar el **fácil de usar** abra el vídeo para editarlo en DAM y configure la variable **Título** campo de metadatos con el nombre deseado. También debe Guardar los cambios realizados cuando haya terminado.

1. Asigne estas variables a props 1 a 3

   La variable **resto de la información pertinente** en la llamada se envía concatenado a **one** variable denominada **pev3**.

   **Llamadas de ejemplo** para Adobe Analytics mediante el ejemplo proporcionado debe tener este aspecto cuando se visualiza con DigitalPulse Debugger:

   ![lmilestones1](assets/lmilestones1.png)

   *La variable **pev3**enviada en la llamada contiene la siguiente información:*

   * *Nombre* - El nombre del archivo de vídeo (*film.avi*)

   * *Length* - La duración del archivo de vídeo, en segundos (*100*)

   * *Nombre del reproductor* - El reproductor de vídeo utilizado para reproducir el archivo de vídeo (*vídeo de HTML5*)

   * *Total de segundos reproducidos* - El número total de segundos que se reprodujo el vídeo (*25*)

   * *Marca de tiempo de inicio* - Marca de tiempo que identifica cuándo se inició la reproducción del vídeo (*1331035567*)

   * *Reproducir sesión* - Los detalles de la sesión de reproducción. Este campo indica cómo interactuó el usuario con el vídeo. Esto puede incluir datos como dónde empezaron a reproducir el vídeo, si utilizaron el control deslizante para avanzar y dónde dejaron de reproducir el vídeo (*L10E24S58L58: el vídeo se detuvo a los segundos. 25 de la sección L10 y luego se omitió a segundos. 48*)

## Segundos heredados {#legacy-seconds}

Al utilizar el método** de segundos heredados**, las llamadas de Adobe Analytics se activan cada N-ésimo segundo, donde N se especifica en el campo Desplazamiento de seguimiento .

1. Establezca el desplazamiento de seguimiento en cualquier número de segundos,

   * Por ejemplo, 6
   >[!NOTE]
   >
   >El campo Desplazamiento de seguimiento solo acepta números enteros superiores a 0

   La información enviada a Adobe Analytics es menos personalizable. Solo hay 3 variables disponibles para la asignación:

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>Las variables asignadas a esta opción contendrán la variable <strong>fácil de usar</strong> name (<strong>Título</strong>) del vídeo si se configura en el DAM; si no se configura el título, el vídeo <strong>nombre de archivo</strong> se enviará en su lugar. Solo se envía una vez, al principio de la reproducción de un vídeo.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>Variable asignada a esta contiene el nombre del archivo. Solo se envía una vez, al principio de la reproducción de un vídeo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>Variable asignada a esto contendrá la ruta del archivo en el servidor. Solo se envía una vez, al principio de la reproducción de un vídeo.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Puede configurar el **fácil de usar** abra el vídeo para editarlo en DAM y configure la variable **Título** campo de metadatos con el nombre deseado. También debe Guardar los cambios realizados cuando haya terminado.

1. Asigne estas variables a prop1, prop2 y prop3

   La variable **resto de la información pertinente** en la llamada se envía concatenado a **one** variable denominada **pev3**.

   Las llamadas a Adobe Analytics que utilizan el ejemplo proporcionado deben tener este aspecto cuando se visualizan con DigitalPulse Debugger:

   ![lseconds](assets/lseconds.png)

   *La llamada de es similar a la llamada de hitos heredados anterior. Consulte la información sobre pev3 **[siempre que](/help/sites-administering/adobeanalytics.md)**.*

**Referencias utilizadas en este tutorial:**

[0] [https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html)
