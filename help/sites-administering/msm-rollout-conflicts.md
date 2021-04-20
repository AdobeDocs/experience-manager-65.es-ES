---
title: Conflictos de implementación de MSM
seo-title: Conflictos de implementación de MSM
description: Obtenga información sobre cómo lidiar con los conflictos de implementación del administrador de varios sitios.
seo-description: Obtenga información sobre cómo lidiar con los conflictos de implementación del administrador de varios sitios.
uuid: 7a640905-aae2-498e-b95c-2c73008fa1cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 16db5334-604f-44e2-9993-10d683dee5bb
feature: Multi Site Manager
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 0%

---


# Conflictos de despliegue de MSM{#msm-rollout-conflicts}

Pueden producirse conflictos si se crean nuevas páginas con el mismo nombre de página en la rama del modelo y en una rama de Live Copy dependiente.

Estos conflictos deben manejarse y resolverse en el momento de su implementación.

## Gestión de conflictos {#conflict-handling}

Cuando existen páginas en conflicto (en las ramas de modelo y Live Copy), MSM le permite definir cómo deben manejarse (o incluso si).

Para garantizar que el despliegue no esté bloqueado, las definiciones posibles pueden incluir:

* qué página (modelo o Live Copy) tendrá prioridad durante el lanzamiento,
* qué páginas se cambiarán de nombre (y cómo),
* cómo afectará esto a cualquier contenido publicado.

   El comportamiento predeterminado de AEM (predeterminado) es que el contenido publicado no se verá afectado. Por lo tanto, si se ha publicado una página creada manualmente en la rama de Live Copy, dicho contenido se publicará después de la gestión y el despliegue del conflicto.

Además de la funcionalidad estándar, se pueden agregar controladores de conflicto personalizados para implementar distintas reglas. También pueden permitir acciones de publicación como un proceso individual.

### Ejemplo de escenario {#example-scenario}

En las secciones siguientes utilizamos el ejemplo de una nueva página `b`, creada tanto en el modelo como en la rama de Live Copy (creada manualmente), para ilustrar los distintos métodos de resolución de conflictos:

* modelo: `/b`

   Una página de formato; con 1 página secundaria, bp-level-1.

* Live Copy: `/b`

   Una página creada manualmente en la rama de Live Copy; con 1 página secundaria, `lc-level-1`.

   * Se activa en la publicación como `/b`, junto con la página secundaria.

**Antes de la implementación**

<table>
 <tbody>
  <tr>
   <td><strong>modelo antes de la implementación</strong></td>
   <td><strong>Live Copy antes del lanzamiento</strong></td>
   <td><strong>publicar antes del lanzamiento</strong></td>
  </tr>
  <tr>
   <td><code>b</code> <br /> (creado en rama de modelo, listo para lanzamiento)<br /> </td>
   <td><code>b</code> <br /> (creado manualmente en la rama de Live Copy)<br /> </td>
   <td><code>b</code> <br /> (contiene el contenido de la página b que se creó manualmente en la rama de Live Copy)</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> (creado manualmente en la rama de Live Copy)<br /> </td>
   <td><code> /lc-level-1</code> <br /> (contiene el contenido de la página<br /> child-level-1 que se creó manualmente en la rama de Live Copy)</td>
  </tr>
 </tbody>
</table>

## Gestor de implementación y administración de conflictos {#rollout-manager-and-conflict-handling}

El administrador de implementación le permite activar o desactivar la administración de conflictos.

Esto se realiza mediante la [configuración OSGi](/help/sites-deploying/configuring-osgi.md) del **administrador de implementación de CQ WCM de día**:

* **Gestione los conflictos con las páginas creadas manualmente**:

   ( `rolloutmgr.conflicthandling.enabled`)

   Se establece en true si el administrador de implementaciones debe gestionar los conflictos de una página creada en la Live Copy con un nombre que exista en el modelo.

AEM tiene [comportamiento predefinido cuando la administración de conflictos se ha desactivado](#behavior-when-conflict-handling-deactivated).

## Controlador de conflictos {#conflict-handlers}

AEM utiliza controladores de conflictos para resolver cualquier conflicto de páginas que exista al implementar contenido desde un modelo a una Live Copy. Cambiar el nombre de las páginas es uno de los métodos (habituales) para resolver estos conflictos. Puede haber más de un controlador de conflictos en funcionamiento para permitir una selección de comportamientos diferentes.

AEM proporciona:

* El [controlador de conflicto predeterminado](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* La posibilidad de implementar un [controlador personalizado](#customized-handlers).
* Mecanismo de clasificación de servicios que permite establecer la prioridad de cada controlador individual. Se utiliza el servicio con la clasificación más alta.

### Controlador de conflictos predeterminado {#default-conflict-handler}

El controlador de conflicto predeterminado:

* Se llama `ResourceNameRolloutConflictHandler`

* Con este controlador, la página de modelo tiene prioridad.
* La clasificación de servicio para este controlador se establece en menor ( &quot;p. ej. debajo del valor predeterminado de la propiedad `service.ranking` ), ya que se supone que los controladores personalizados necesitarán una clasificación más alta. Sin embargo, la clasificación no es el mínimo absoluto para garantizar la flexibilidad cuando sea necesario.

Este controlador de conflicto da prioridad al modelo. La página de Live Copy `/b` se mueve (dentro de la rama de Live Copy) a `/b_msm_moved`.

* Live Copy: `/b`

   Se mueve (dentro de la Live Copy) a `/b_msm_moved`. Esto actúa como una copia de seguridad y garantiza que no se pierda contenido.

   * `lc-level-1` no se mueve.

* modelo: `/b`

   Se despliega en la página de Live Copy `/b`.

   * `bp-level-1` se despliega en livecopy.

**Después de la implementación**

<table>
 <tbody>
  <tr>
   <td><strong>modelo después del lanzamiento</strong></td>
   <td><strong>Live Copy después del lanzamiento</strong><br /> </td>
   <td></td>
   <td><strong>Live Copy después del lanzamiento</strong><br /> <br /> <br /> </td>
   <td><strong>publicar después del lanzamiento</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (tiene el contenido de la página de modelo b que se presentó)<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br /> (tiene el contenido de la página b que se creó manualmente en la rama de Live Copy)</td>
   <td><code>b</code> <br /> (sin cambios; contiene el contenido de la página original b que se creó manualmente en la rama de Live Copy y ahora se denomina b_msm_move)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> (sin cambio)</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code> <br /> (sin cambio)</td>
  </tr>
 </tbody>
</table>

### Controladores personalizados {#customized-handlers}

Los controladores de conflicto personalizados le permiten implementar sus propias reglas. Con el mecanismo de clasificación de servicios también puede definir cómo interactúan con otros controladores.

Los controladores de conflictos personalizados pueden:

* Reciba un nombre según sus necesidades.
* Ser desarrollado/configurado según sus necesidades; por ejemplo, puede desarrollar un controlador para que la página de Live Copy tenga prioridad.
* Se puede diseñar para que se configure usando la [configuración OSGi](/help/sites-deploying/configuring-osgi.md); en particular:

   * **Clasificación de servicios**:

      Define el orden relacionado con otros controladores de conflicto ( `service.ranking`).

      El valor predeterminado es 0.

### Comportamiento cuando el manejo de conflictos está desactivado {#behavior-when-conflict-handling-deactivated}

Si desactiva manualmente [la gestión de conflictos](#rollout-manager-and-conflict-handling), no AEM ninguna acción en ninguna página en conflicto (las páginas que no entran en conflicto se despliegan según lo esperado).

>[!CAUTION]
>
>AEM no da ninguna indicación de que se estén ignorando los conflictos, ya que este comportamiento debe configurarse explícitamente, por lo que se supone que es el comportamiento requerido.

En este caso, la Live Copy tiene prioridad. La página de modelo `/b` no se copia y la página de copia activa `/b` no se modifica.

* modelo: `/b`

   No se copia, pero se ignora.

* Live Copy: `/b`

   Sigue igual.

<table>
 <caption>
   Después de la implementación
 </caption>
 <tbody>
  <tr>
   <td><strong>modelo después del lanzamiento</strong></td>
   <td><strong>Live Copy después del lanzamiento</strong><br /> <br /> <br /> </td>
   <td><strong>publicar después del lanzamiento</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (sin cambios; tiene el contenido de la página b que se creó manualmente en la rama de Live Copy)</td>
   <td><code>b</code> <br /> (sin cambios; contiene el contenido de la página b que se creó manualmente en la rama de Live Copy)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code> </td>
   <td><code> /lc-level-1</code> <br /> (sin cambio)</td>
   <td><code> /lc-level-1</code> <br /> (sin cambio)</td>
  </tr>
 </tbody>
</table>

### Clasificación de servicios {#service-rankings}

La clasificación del servicio [OSGi](https://www.osgi.org/) se puede utilizar para definir la prioridad de los controladores de conflictos individuales.
