---
title: Solución de problemas y preguntas más frecuentes sobre MSM
description: Descubra cómo solucionar los problemas más comunes relacionados con MSM y obtenga respuestas a las preguntas más comunes relacionadas con MSM.
feature: Multi Site Manager
role: Admin
source-git-commit: d4fa331ad048e1d8bd57e0944c8bc5b67be1d203
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 0%

---

# Solución de problemas y preguntas más frecuentes sobre MSM {#troubleshooting-msm}

## Solución de problemas de los primeros pasos {#first-steps}

Si está experimentando lo que cree que es un comportamiento incorrecto o un error en MSM, antes de comenzar y realizar la solución de problemas detallada, asegúrese de:

* Marque la [Preguntas más frecuentes sobre MSM](#faq) ya que puede que sus problemas o preguntas ya se hayan solucionado allí.
* Marque la [Artículo de prácticas recomendadas de MSM](msm-best-practices.md) se ofrecen varias sugerencias, así como aclaraciones sobre una serie de ideas erróneas.

## Búsqueda de información avanzada sobre el modelo y el estado de Live Copy {#advanced-info}

MSM registra varios servlets que se pueden solicitar con selectores en las direcciones URL de los recursos. Las utiliza la interfaz de usuario de , pero también se pueden solicitar directamente para ver estados de MSM calculados avanzados y directamente adicionales para sus páginas:

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * Utilícelo en una página de modelo para recuperar la lista de todas las Live Copies vinculadas a ella, con información de estado de Live Copy adicional.
1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * Utilícelo en páginas de Live Copy para recuperar información avanzada sobre su conexión con sus páginas de modelo. Si la página no es una Live Copy, no se devuelve nada.

Estos servlets generan mensajes de registro de depuración a través de la variable `com.day.cq.wcm.msm` logger que también puede ser útil.

## Comprobación de información específica de MSM en el repositorio {#checking-repo}

Los servlets anteriores devolvían información calculada basada en los nodos y mezclas específicos de MSM. La información se almacena en el repositorio de la siguiente manera.

* `cq:LiveSync` tipo de mezcla
   * Esto está configurado en `jcr:content` y definir las páginas raíz de Live Copy.
   * Estas páginas tendrán un `cq:LiveSyncConfig` nodo secundario del tipo `cq:LiveCopy` que contendrán información básica y obligatoria sobre Live Copy a través de las siguientes propiedades:
      * `cq:master` apunta a la página de modelo de Live Copy.
      * `cq:rolloutConfigs` indica las configuraciones de lanzamiento activas aplicadas a Live Copy.
      * `cq:isDeep` es verdadero si las páginas secundarias de esta página raíz de Live Copy están incluidas en Live Copy.
* `cq:LiveRelationship` tipo de mezcla
   * Cualquier página de Live Copy tiene este tipo de mezcla en su `jcr:content` nodo .
   * Si no es así, la página en algún momento se ha separado o creado manualmente mediante la interfaz de creación fuera de una acción de Live Copy (crear o desplegar).
* `cq:LiveSyncCancelled` tipo de mezcla
   * Se ha añadido a `jcr:content` nodos de páginas de Live Copy que se suspendieron.
   * Si la suspensión es efectiva también para páginas secundarias, `cq:isCancelledForChildren` se establece en true en el mismo nodo.

La información presente en estas propiedades debe reflejarse en la interfaz de usuario, sin embargo, al solucionar problemas, puede resultar útil observar el comportamiento de MSM directamente en el repositorio a medida que se producen acciones de MSM.

Conocer esas propiedades también puede ser útil para consultar el repositorio y averiguar conjuntos de páginas que están en estados particulares. Por ejemplo:

* `select * from cq:LiveSync` devuelve todas las páginas raíz de Live Copy.

## Preguntas más frecuentes {#faq}

Estas son algunas de las preguntas más frecuentes relacionadas con MSM y Live Copy.

### ¿Por qué algunas propiedades (p. ej., título, anotaciones) no se actualizan durante una implementación de MSM? {#missing-properties}

Las acciones de sincronización de MSM son altamente configurables. Las propiedades o los componentes que se modifican durante las implementaciones dependen directamente de las propiedades de dichas configuraciones.

Consulte [este artículo](msm-best-practices.md) para obtener más información sobre este tema.

### ¿Cómo puedo eliminar los permisos de implementación de un grupo de autores? {#remove-rollout-permissions}

No hay **despliegue** que se pueden establecer o eliminar para AEM principales (usuarios o grupos).

Como alternativa, puede:

* Personalice la interfaz de usuario del producto para ocultar las acciones de implementación de una entidad de seguridad determinada.
* Elimine los privilegios de escritura del árbol de Live Copy para los autores a los que no se les permite desplegar.

### ¿Por qué veo páginas de Live Copy con el sufijo &quot;_msm_move&quot;? {#moved-pages}

Si se despliega una página de modelo, actualizará su página de Live Copy o creará una nueva página de Live Copy si aún no existe (por ejemplo, cuando se implemente por primera vez o cuando se elimine manualmente la página de Live Copy).

Sin embargo, en este último caso, si una página no tiene `cq:LiveRelationship` existe la propiedad con el mismo nombre, se cambiará el nombre de esta página en consecuencia antes de crear la página Live Copy.

De forma predeterminada, el despliegue espera una página de Live Copy vinculada, a la que se implementarán las actualizaciones de los modelos o ninguna página cuando se cree una página de Live Copy.

Si se encuentra una página &quot;independiente&quot;, MSM elige cambiar el nombre de esta página y crear una página de Live Copy separada y vinculada.

Esta página independiente en un subárbol de Live Copy suele ser el resultado de una **Desasociar** o la página anterior de Live Copy fue eliminada manualmente por un autor y luego recreada con el mismo nombre.

Para evitar esto, use Live Copy **Suspender** en lugar de **Desasociar**. Más información sobre **Desasociar** acción en [este artículo.](msm-livecopy.md)
