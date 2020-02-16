---
title: Configuración del seguimiento de vídeo para Adobe Analytics
seo-title: Configuración del seguimiento de vídeo para Adobe Analytics
description: Obtenga información sobre la configuración del seguimiento de videos para SiteCatalyst.
seo-description: Obtenga información sobre la configuración del seguimiento de videos para SiteCatalyst.
uuid: 5a862f05-abfa-42a2-ad40-4c1c32f1bd75
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: a18ddac1-9e4c-4857-9cb3-4d5eeb8dd9ec
docset: aem65
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# Configuración del seguimiento de vídeo para Adobe Analytics{#configuring-video-tracking-for-adobe-analytics}

Hay varios métodos disponibles para el seguimiento de eventos de vídeo, dos de los cuales son opciones heredadas para versiones anteriores de Adobe Analytics. Estas opciones heredadas son: Hitos heredados y segundos heredados.

>[!NOTE]
>
>Antes de continuar, asegúrese de **que tiene un** vídeo reproducible** cargado en AEM.

>Para asegurarse de que los vídeos se reproducen en la página, consulte **[este tutorial](/help/sites-authoring/default-components-foundation.md#video)**para obtener información sobre cómo transcodificar archivos de vídeo en AEM.

Utilice el procedimiento siguiente para configurar un marco para el seguimiento de vídeo con cada método.

>[!NOTE]
>
>En implementaciones nuevas, se recomienda **no utilizar** las opciones heredadas para el seguimiento de vídeo. En su lugar, utilice el método **Hitos** .

## Pasos comunes {#common-steps}

1. Configure una página web arrastrando un componente **de** vídeo de la barra de tareas y agregando un **vídeo reproducible como recurso** para el componente

1. [Cree una configuración y un marco](/help/sites-administering/adobeanalytics.md)de trabajo de Adobe Analytics.

   * Los ejemplos de las secciones siguientes utilizan el nombre **my-sc-configuration** para la configuración y la **videofw** para la estructura.

1. En la página de marco, seleccione un RSID y defina el uso en todos. ([https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html](https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html))
1. En la categoría de componentes General de la barra de tareas, arrastre el componente Vídeo al marco.
1. Seleccione un método de seguimiento:

   * [Hitos](/help/sites-administering/adobeanalytics.md)
   * [Hitos no heredados](/help/sites-administering/adobeanalytics.md)
   * [Hitos heredados](/help/sites-administering/adobeanalytics.md)
   * [Segundos heredados](/help/sites-administering/adobeanalytics.md)

1. Al seleccionar un método de seguimiento, la lista de variables de CQ cambia en consecuencia. Utilice las secciones siguientes para obtener información sobre cómo seguir configurando el componente y asignar las variables de CQ con las propiedades de Adobe Analytics.

## Milestones {#milestones}

El método Hitos rastrea la mayor cantidad de información sobre el vídeo, es altamente personalizable y fácil de configurar.

Para utilizar el método Hitos, especifique los desplazamientos de seguimiento basados en el tiempo para definir los hitos. Cuando una reproducción de vídeo supera un hito, la página llama a Adobe Analytics para realizar el seguimiento del evento. Para cada hito que defina, el componente crea una variable de CQ que puede asignar a una propiedad de Adobe Analytics. El nombre de estas variables de CQ utiliza el siguiente formato:

```shell
eventdata.events.milestoneXX
```

El sufijo XX es el desplazamiento de la pista que define el hito. Por ejemplo, si se especifican desplazamientos de seguimiento de 4, 8, 16, 20 y 28 segundos, se generan las siguientes variables de CQ:

* `eventdata.events.milestone4`
* `eventdata.events.milestone8`
* `eventdata.events.milestone16`
* `eventdata.events.milestone20`
* `eventdata.events.milestone28`

En la tabla siguiente se describen las variables de CQ predeterminadas que se proporcionan para el método Milestones:

<table>
 <tbody>
  <tr>
   <th>Variables de CQ</th>
   <th>Propiedades de Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>Las variables asignadas a esto contendrán el nombre <strong>práctico</strong> (<strong>Título</strong>) del vídeo si se establece en el DAM; si no se establece, se enviará el nombre <strong>del</strong> archivo del vídeo. Solo se envía una vez, al comienzo de la reproducción de un vídeo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>Las variables asignadas a esto contendrán el nombre del archivo. Solo se envía junto con eventdata.events.a.media.view </td>
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
   <td>Se envía cada vez que se activa un hito, junto con este evento, el número de segundos que el usuario ha pasado viendo el segmento determinado. por ejemplo: eventX=21<br /> </td>
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
   <td>Enviado cuando se pasa el hito determinado, X representa el segundo en que se activa el hito<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>Enviado en cada hito; se muestra como pev3 en la llamada de Adobe Analytics, generalmente enviada como "video"<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>Coincide exactamente con eventdata.videoName </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>Contiene información sobre el segmento que se ha visto, por ejemplo: 2:O:4-8 </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Puede definir el nombre **práctico** de un vídeo abriendo el vídeo para editarlo en DAM y estableciendo el campo de metadatos **Título** en el nombre deseado.

1. Después de seleccionar Hitos como método de seguimiento, en el cuadro Desplazamiento de seguimiento, introduzca una lista separada por comas de los desplazamientos de seguimiento en segundos. Por ejemplo, el siguiente valor define hitos en 4, 8, 16, 20 y 28 segundos después del inicio del vídeo:

   ```xml
   4,8,16,20,24
   ```

   Los valores de desplazamiento deben ser enteros mayores que 0. El valor predeterminado es `10,25,50,75`.

1. Para asignar las variables de CQ a las propiedades de Adobe Analytics, arrastre las propiedades de Adobe Analytics desde ContentFinder junto a la variable de CQ del componente.

   Para obtener información sobre la optimización de las asignaciones, consulte la guía [Medición de vídeo en Adobe Analytics](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_overview.html) .

1. [Agregue el marco](/help/sites-administering/adobeanalytics.md) a la página.
1. Para probar la configuración en modo **de** vista previa, reproduzca el vídeo para que se activen las llamadas de Adobe Analytics.

Los siguientes ejemplos de datos de seguimiento de Adobe Analytics se aplican al seguimiento de hitos mediante compensaciones de seguimiento de 4, 8, 16, 20 y 24, y las siguientes asignaciones para las variables de CQ:

<table>
 <tbody>
  <tr>
   <th>variable de CQ</th>
   <th>Propiedad de Adobe Analytics</th>
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

Para este ejemplo, el componente Vídeo aparece de la siguiente manera en la página de marco:

![video1](assets/video1.png)

>[!NOTE]
>
>Para ver las llamadas realizadas a Adobe Analytics, utilice una herramienta adecuada, como DigitalPulse Debugger o Fiddler.

Las llamadas a Adobe Analytics que utilicen el ejemplo proporcionado deben tener este aspecto cuando se visualizan con DigitalPulse Debugger:

![chlimage_1-128](assets/chlimage_1-128.png)

*Esta es la **primera llamada**realizada a Adobe Analytics que contiene los siguientes valores:*

* *prop1 y eVar1 para eventdata.a.media.name,*
* *props2-4, junto con eVar2 y eVar3 que contienen contentType (vídeo) y segment (1:O:1-4)*
* *event3 que se asignó a eventData.events.a.media.view.*

![chlimage_1-129](assets/chlimage_1-129.png)

*Esta es la **tercera llamada**realizada a Adobe Analytics:*

* *prop1 y eVar1 contienen a.media.name;*
* *event1 porque se ha visto un segmento*
* *event2 enviado con tiempo de reproducción = 4*
* *event11 enviado porque se ha alcanzado event.events.milestone8*
* *no se envían prop2 a 4 (ya que event.events.a.media.view no se activó)*

## Hitos no heredados {#non-legacy-milestones}

El método de hitos no heredados es similar al método de hitos, excepto que los hitos se definen usando porcentajes de la longitud de la pista. Las características comunes son las siguientes:

* Cuando una reproducción de vídeo supera un hito, la página llama a Adobe Analytics para realizar el seguimiento del evento.
* Conjunto [estático de variables](#cqvars) de CQ que se definen para la asignación con propiedades de Adobe Analytics.
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

1. Después de seleccionar Hitos no heredados como método de seguimiento, en el cuadro Desplazamiento de seguimiento, introduzca una lista separada por comas de los porcentajes de la longitud de la pista. Por ejemplo, el siguiente valor predeterminado define hitos en un 10, 25, 50 y 75 por ciento de la longitud de la pista:

   ```xml
   10,25,50,75
   ```

   Los valores de desplazamiento deben ser enteros mayores que 0.

1. Para asignar las variables de CQ a las propiedades de Adobe Analytics, arrastre las propiedades de Adobe Analytics desde ContentFinder junto a la variable de CQ del componente.

   Para obtener información sobre la optimización de las asignaciones, consulte la guía [Medición de vídeo en Adobe Analytics](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_overview.html) .

1. [Agregue el marco](/help/sites-administering/adobeanalytics.md) a la página.
1. Para probar la configuración en modo **de** vista previa, reproduzca el vídeo para que se activen las llamadas de Adobe Analytics.

## Hitos heredados {#legacy-milestones}

Este método es similar al método Hitos con la diferencia de que los hitos especificados en el campo Desplazamiento *de* seguimiento son porcentajes en lugar de puntos establecidos dentro del vídeo.

>[!NOTE]
>
>El campo Desplazamiento de seguimiento solo acepta una lista separada por comas que contenga números enteros entre 1 y 100.

1. Establezca el desplazamiento de la pista.

   * p. ej. 10,50,75,100
   Además, la información enviada a Adobe Analytics es menos personalizable; solo hay 3 variables disponibles para la asignación:

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>Las variables asignadas a esto contendrán el nombre <strong>práctico</strong> (<strong>Título</strong>) del vídeo si se establece en el DAM; si no se establece el Título, se enviará el nombre <strong>del</strong> archivo del vídeo. Solo se envía una vez, al comienzo de la reproducción de un vídeo.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>Las variables asignadas a esto contendrán el nombre del archivo. Solo se envía una vez, al comienzo de la reproducción de un vídeo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>La variable asignada a esto contendrá la ruta del archivo en el servidor. Solo se envía una vez, al comienzo de la reproducción de un vídeo.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Puede definir el nombre **práctico** de un vídeo abriendo el vídeo para editarlo en DAM y estableciendo el campo de metadatos **Título** en el nombre deseado. También debe guardar los cambios realizados al finalizar.

1. Asigne estas variables a props 1 a 3

   El **resto de la información** relevante en la llamada se enviará concatenada en **una** variable denominada **pev3**.

   **Las llamadas** de muestra a Adobe Analytics que utilicen el ejemplo proporcionado deben tener este aspecto cuando se visualizan con DigitalPulse Debugger:

   ![lmilestones1](assets/lmilestones1.png)

   *La variable **pev3**enviada en la llamada contiene la siguiente información:*

   * *Nombre* : el nombre del archivo de vídeo (*film.avi*)

   * *Duración* : duración del archivo de vídeo, en segundos (*100*)

   * *Nombre* del reproductor: reproductor de vídeo utilizado para reproducir el archivo de vídeo (vídeo ** HTML5)

   * *Segundos totales reproducidos* : el número total de segundos que se reprodujo el vídeo (*25*)

   * *Marca de hora* de inicio: marca de hora que identifica cuándo se inició la reproducción del vídeo (*1331035567*)

   * *Sesión* de reproducción: los detalles de la sesión de reproducción. Este campo indica cómo interactuó el usuario con el vídeo. Esto puede incluir datos como dónde empezaron a reproducir el vídeo, si utilizaron el control deslizante para avanzar en el vídeo y dónde dejaron de reproducirlo (*L10E24S58L58 - el vídeo se detuvo en segundos. 25 de la sección L10, luego se omitió a seg. 48*)

## Segundos heredados {#legacy-seconds}

Al utilizar el método** de segundos heredados**, las llamadas de Adobe Analytics se activan cada N-ésimo segundo, donde N se especifica en el campo Desplazamiento de seguimiento.

1. Establezca el desplazamiento de seguimiento en cualquier número de segundos,

   * p. ej. 6
   >[!NOTE]
   >
   >El campo Desplazamiento de seguimiento solo acepta números enteros superiores a 0

   La información enviada a Adobe Analytics es menos personalizable. Solo hay 3 variables disponibles para la asignación:

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>Las variables asignadas a esto contendrán el nombre <strong>práctico</strong> (<strong>Título</strong>) del vídeo si se establece en el DAM; si no se establece el Título, se enviará el nombre <strong>del</strong> archivo del vídeo. Solo se envía una vez, al comienzo de la reproducción de un vídeo.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>La variable asignada a esto contendrá el nombre del archivo. Solo se envía una vez, al comienzo de la reproducción de un vídeo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>La variable asignada a esto contendrá la ruta del archivo en el servidor. Solo se envía una vez, al comienzo de la reproducción de un vídeo.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Puede definir el nombre **práctico** de un vídeo abriendo el vídeo para editarlo en DAM y estableciendo el campo de metadatos **Título** en el nombre deseado. También debe guardar los cambios realizados al finalizar.

1. Asigne estas variables a prop1, prop2 y prop3

   El **resto de la información** relevante en la llamada se enviará en **una** variable denominada **pev3**.

   Las llamadas a Adobe Analytics que utilicen el ejemplo proporcionado deben tener este aspecto cuando se visualizan con DigitalPulse Debugger:

   ![lseconds](assets/lseconds.png)

   *La llamada es similar a la llamada de hitos heredados de arriba. Consulte la información sobre pev3 **[proporcionada allí](/help/sites-administering/adobeanalytics.md)**.*

**Referencias utilizadas en este tutorial:**

[0] [https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_overview.html](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_overview.html)
