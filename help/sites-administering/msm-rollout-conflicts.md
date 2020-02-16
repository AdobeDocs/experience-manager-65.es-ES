---
title: Conflictos de despliegue de MSM
seo-title: Conflictos de despliegue de MSM
description: Conozca cómo lidiar con los conflictos de implementación de Multi Site Manager.
seo-description: Conozca cómo lidiar con los conflictos de implementación de Multi Site Manager.
uuid: 7a640905-aae2-498e-b95c-2c73008fa1cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 16db5334-604f-44e2-9993-10d683dee5bb
translation-type: tm+mt
source-git-commit: 47b69098a45f774501ebb62ee1a14a8d209ad101

---


# Conflictos de despliegue de MSM{#msm-rollout-conflicts}

Pueden producirse conflictos si se crean páginas nuevas con el mismo nombre de página en la rama de modelo y en una rama de Live Copy dependiente.

Estos conflictos deben ser tratados y resueltos en el momento de su implementación.

## Gestión de conflictos {#conflict-handling}

Cuando existen páginas en conflicto (en el modelo y en las ramas de Live Copy), MSM permite definir cómo se deben gestionar (o incluso si).

Para asegurarse de que la implementación no está bloqueada, las definiciones posibles pueden incluir:

* ¿Qué página (modelo o Live Copy) tendrá prioridad durante la implementación?
* qué páginas se cambiarán de nombre (y cómo),
* cómo afectará esto a cualquier contenido publicado.

   El comportamiento predeterminado de AEM (lista para usar) es que el contenido publicado no se verá afectado. Por lo tanto, si se ha publicado una página que se creó manualmente en la rama de Live Copy, dicho contenido se seguirá publicando después de la gestión y la implementación del conflicto.

Además de la funcionalidad estándar, se pueden agregar controladores de conflictos personalizados para implementar distintas reglas. También pueden permitir acciones de publicación como un proceso individual.

### Ejemplo de escenario {#example-scenario}

En las siguientes secciones se utiliza el ejemplo de una nueva página `b`, creada tanto en el modelo como en la rama de Live Copy (creada manualmente), para ilustrar los distintos métodos de resolución de conflictos:

* blueprint: `/b`

   Una página de formato; con 1 página secundaria, bp-level-1.

* live copy: `/b`

   Una página creada manualmente en la rama Live Copy; con una página secundaria, `lc-level-1`.

   * Se activa al publicar como `/b`, junto con la página secundaria.

**Antes de la implementación**

<table>
 <tbody>
  <tr>
   <td><strong>modelo antes de la implementación</strong></td>
   <td><strong>Live Copy antes del lanzamiento</strong></td>
   <td><strong>publicar antes de la implementación</strong></td>
  </tr>
  <tr>
   <td><code>b</code> <br /> (creado en rama de modelo, listo para la implementación)<br /> </td>
   <td><code>b</code> <br /> (creado manualmente en una rama de Live Copy)<br /> </td>
   <td><code>b</code> <br /> (contiene el contenido de la página b que se creó manualmente en la rama Live Copy)</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> (creado manualmente en una rama de Live Copy)<br /> </td>
   <td><code> /lc-level-1</code> <br /> (contiene el contenido de la página<br /> child-level-1 que se creó manualmente en la rama Live Copy)</td>
  </tr>
 </tbody>
</table>

## Administrador de implementación y administración de conflictos {#rollout-manager-and-conflict-handling}

El administrador de implementación le permite activar o desactivar la administración de conflictos.

Esto se lleva a cabo mediante la configuración [OSGi del Administrador](/help/sites-deploying/configuring-osgi.md) de implementación de CQ **** Day WCM:

* **Controlar conflictos con páginas** creadas manualmente:

   ( `rolloutmgr.conflicthandling.enabled`)

   Se establece en true si el administrador de implementación debe gestionar conflictos de una página creada en la Live Copy con un nombre que exista en el modelo.

AEM tiene un comportamiento [predefinido cuando la administración de conflictos se ha desactivado](#behavior-when-conflict-handling-deactivated).

## Controladores de conflictos {#conflict-handlers}

AEM utiliza controladores de conflictos para resolver cualquier conflicto de páginas que exista al distribuir contenido de un modelo a una Live Copy. Cambiar el nombre de las páginas es uno de los métodos habituales para resolver estos conflictos. Puede haber más de un controlador de conflictos en funcionamiento para permitir una selección de comportamientos diferentes.

AEM proporciona:

* El controlador de conflictos [predeterminado](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* Posibilidad de implementar un controlador [personalizado](#customized-handlers).
* Mecanismo de clasificación de servicios que permite establecer la prioridad de cada controlador individual. Se utiliza el servicio con la clasificación más alta.

### Controlador de conflictos predeterminado {#default-conflict-handler}

El controlador de conflictos predeterminado:

* Se llama `ResourceNameRolloutConflictHandler`

* Con este controlador se da prioridad a la página de modelo.
* La clasificación del servicio para este controlador se establece en un valor bajo ( &quot;i.e. por debajo del valor predeterminado de la `service.ranking` propiedad), ya que se supone que los controladores personalizados necesitarán una clasificación más alta. Sin embargo, la clasificación no es el mínimo absoluto para garantizar la flexibilidad cuando sea necesario.

Este controlador de conflictos da prioridad al modelo. La página de Live Copy `/b` se mueve (dentro de la rama de Live Copy) a `/b_msm_moved`.

* live copy: `/b`

   Se mueve (dentro de la Live Copy) a `/b_msm_moved`. Actúa como una copia de seguridad y garantiza que no se pierda contenido.

   * `lc-level-1` no se mueve.

* blueprint: `/b`

   Se despliega en la página de Live Copy `/b`.

   * `bp-level-1` se despliega en la Live Copy.

**Después del despliegue**

<table>
 <tbody>
  <tr>
   <td><strong>modelo después de la implementación</strong></td>
   <td><strong>Live Copy después del lanzamiento</strong><br /> </td>
   <td></td>
   <td><strong>Live Copy después del lanzamiento</strong><br /> <br /><br /> </td>
   <td><strong>publicar después de la implementación</strong><br /><br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (tiene el contenido de la página de modelo b que se presentó)<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br /> (tiene el contenido de la página b que se creó manualmente en la rama Live Copy)</td>
   <td><code>b</code> <br /> (sin cambios; contiene el contenido de la página original b que se creó manualmente en la rama Live Copy y ahora se denomina b_msm_move)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> (sin cambios)</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code> <br /> (sin cambios)</td>
  </tr>
 </tbody>
</table>

### Controladores personalizados {#customized-handlers}

Los controladores de conflictos personalizados le permiten implementar sus propias reglas. Con el mecanismo de clasificación de servicios también puede definir cómo interactúan con otros controladores.

Los controladores de conflictos personalizados pueden:

* Reciba un nombre según sus necesidades.
* Ser desarrollado/configurado según sus necesidades; por ejemplo, puede desarrollar un controlador para que la página de Live Copy tenga prioridad.
* Se puede diseñar para configurarse mediante la configuración [](/help/sites-deploying/configuring-osgi.md)OSGi; en particular:

   * **Clasificación** de servicios:

      Define el orden relacionado con otros controladores de conflictos ( `service.ranking`).

      El valor predeterminado es 0.

### Comportamiento al desactivar la gestión de conflictos {#behavior-when-conflict-handling-deactivated}

Si [desactiva manualmente la gestión](#rollout-manager-and-conflict-handling) de conflictos, AEM no realiza ninguna acción en las páginas en conflicto (las páginas que no entran en conflicto se distribuyen según lo previsto).

>[!CAUTION]
>
>AEM no indica que se estén ignorando los conflictos, ya que este comportamiento debe configurarse explícitamente, por lo que se supone que es el comportamiento necesario.

En este caso, la Live Copy tiene prioridad. La página de modelo no `/b` se copia y la página de Live Copy `/b` se deja intacta.

* blueprint: `/b`

   No se copia en absoluto, pero se ignora.

* live copy: `/b`

   Sigue igual.

<table>
 <caption>
   Después del despliegue
 </caption>
 <tbody>
  <tr>
   <td><strong>modelo después de la implementación</strong></td>
   <td><strong>Live Copy después del lanzamiento</strong><br /> <br /><br /> </td>
   <td><strong>publicar después de la implementación</strong><br /><br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (sin cambios; tiene el contenido de la página b que se creó manualmente en la rama Live Copy)</td>
   <td><code>b</code> <br /> (sin cambios; contiene el contenido de la página b que se creó manualmente en la rama Live Copy)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code> </td>
   <td><code> /lc-level-1</code> <br /> (sin cambios)</td>
   <td><code> /lc-level-1</code> <br /> (sin cambios)</td>
  </tr>
 </tbody>
</table>

### Clasificación de servicios {#service-rankings}

La clasificación del servicio [OSGi](https://www.osgi.org/) se puede utilizar para definir la prioridad de los controladores de conflictos individuales.
