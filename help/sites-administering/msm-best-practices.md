---
title: Prácticas recomendadas de MSM
description: Encuentre las prácticas recomendadas recopiladas por los equipos de consultoría e ingeniería de Adobe para ayudarle a poner en marcha el administrador de varios sitios de AEM.
topic-tags: site-features, best-practices
feature: Multi Site Manager
exl-id: 3fedc1ba-64f5-4fbe-9ee5-9b96b75dda58
source-git-commit: c6ccd204dbd514d6195424aff495bc38f1f31bce
workflow-type: tm+mt
source-wordcount: '1617'
ht-degree: 43%

---

# Prácticas recomendadas de MSM{#msm-best-practices}

## General {#general}

MSM es un marco de trabajo configurable para automatizar la implementación de contenido. Las implementaciones suelen incluir partes importantes de un sitio web y abarcan organizaciones y áreas geográficas. Por lo tanto, es muy recomendable planificar las implementaciones de MSM con el cuidado con que planifica el sitio web:

* Planifique con cuidado la **estructura y los flujos de contenido** antes de iniciar la implementación.
* **Mantenga la cantidad de Live Copies como mínimo.** El procesamiento de Live Copies es una tarea que consume muchos recursos. Cuantos más Live Copies existan en su sistema, más rendimiento se verá afectado: desde el procesamiento de índices de Live Copy internos, pasando por operaciones de Live Copy como despliegues, hasta operaciones de interfaz de usuario como mostrar relaciones de Live Copy en el carril de referencias del administrador de Sites. Una práctica recomendada es crear Live Copies de sitios o ramas de un sitio, donde las relaciones de Live Copy se heredan de las páginas del sitio o rama. Evite crear Live Copies individuales para páginas en un sitio o rama cuando toda la estructura se pueda convertir en una Live Copy.
* **Personalice tanto como sea necesario, pero tan poco como sea posible.** Aunque MSM admite un alto grado de personalización (p. ej., configuraciones de implementación), la práctica recomendada para el rendimiento, la fiabilidad y la capacidad de actualización de su sitio web es minimizar la personalización.
* Establezca un modelo de **gobernanza** desde el principio, y capacite a los usuarios debidamente para garantizar el éxito. Una práctica recomendada desde el punto de vista de la gobernanza es **minimizar la autoridad que tienen los productores de contenido local** para asignar o conectar contenido a otros usuarios locales y sus respectivas Live Copies. Esto se debe a que las herencias encadenadas no gobernadas pueden aumentar significativamente la complejidad de una estructura de MSM y comprometer su rendimiento y fiabilidad.

* Una vez que exista un plan para su estructura, flujos de contenido, automatización y gobernanza: **prototipo y prueba exhaustivamente su sistema** antes de iniciar la implementación en directo.
* Tenga en cuenta que la **consultoría de Adobe y los integradores de sistemas líderes** tienen una amplia experiencia en la planificación e implementación de la automatización de contenido con MSM, por lo que pueden ayudarle a empezar su proyecto MSM y a lo largo de toda su implementación.

>[!NOTE]
>
>Encontrará más información sobre cómo trabajar con MSM en los artículos de la Base de conocimiento:
>
>* [Solución de problemas y preguntas más frecuentes sobre MSM](troubleshoot-msm.md)
>


>[!NOTE]
>
>También puede usar la variable [Componente de referencia](/help/sites-authoring/default-components-foundation.md#reference) para reutilizar una sola página o párrafo. No obstante, tenga en cuenta:
>
>* MSM es más flexible y permite un control detallado sobre qué contenido se sincroniza y cuándo.
>* [Componentes básicos](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) ahora se recomiendan en los componentes de base.
>


## Fuentes de Live Copy y configuraciones de modelo {#live-copy-sources-and-blueprint-configurations}

Tenga en cuenta que se puede crear una Live Copy mediante una de las acciones siguientes: [páginas regulares](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) o [configuración de modelo](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Ambos son casos de uso válidos.

Los beneficios adicionales de utilizar una configuración de modelo son que:

* Permita que el autor use el **Despliegue** en un modelo: para insertar (explícitamente) modificaciones en Live Copies que heredan de este modelo.
* Permita que el autor utilice **Crear sitio**; esto permite al usuario seleccionar fácilmente idiomas y configurar la estructura de la Live Copy.
* Defina una configuración de lanzamiento predeterminada para Live Copies que tengan una relación con el modelo.

En caso de que no se haga referencia a una configuración de modelo, los lanzamientos solo se pueden iniciar desde las propias Live Copies, lo que esencialmente extrae contenido del origen.

Al crear un nuevo sitio con Live Copy, es conveniente crear configuraciones de modelo para garantizar la disponibilidad del conjunto de funciones MSM completo.

>[NOTA!]
>
> Tenga en cuenta que los CUG de la pestaña Permisos no se pueden desplegar en Live Copies desde modelos. Tenga en cuenta esto al configurar Live Copy.

## Sincronización de componentes y contenedores {#components-and-container-synchronization}

En general, la regla de despliegue en MSM con respecto a la sincronización de componentes es:

* Los componentes se despliegan sincronizando cualquier recurso contenido en el modelo.
* Los contenedores solo sincronizan el recurso actual.

Esto significa que los componentes se tratan como un acumulado y, en un despliegue, el componente en sí y todos sus elementos secundarios se sustituyen por los de los modelos. Esto significa que si se agrega un recurso a un componente de este tipo localmente, se reemplazará por el contenido del modelo al desplegarse.

Para admitir el anidado de componentes de modo que los componentes añadidos localmente se mantengan en un despliegue, el componente debe declararse como contenedor. Por ejemplo, el parsys predeterminado se declara como contenedor para que admita contenido añadido localmente.

>[!NOTE]
>
>Añada la propiedad `cq:isContainer` al componente para designarlo como contenedor.

## Crear sitio {#create-site}

Tenga en cuenta que AEM tiene dos enfoques principales para crear Live Copies:

* When [creación de una Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   Este enfoque puede considerarse más genérico y le permite crear Live Copies desde cualquier página. La estructura de contenido de una Live Copy coincide exactamente con el origen.

* When [creación de un sitio](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   Se trata de un enfoque más especializado, principalmente para crear sitios web con una estructura multilingüe.

A continuación se indican algunas consideraciones que deben tenerse en cuenta al crear un sitio:

* Para crear un nuevo sitio, necesita una [configuración de modelo](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations).
* Para permitir la selección de rutas de idioma a crear en un sitio nuevo, las raíces de idioma correspondientes deben existir en el modelo (fuente).
* Una vez [se ha creado un nuevo sitio como Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (mediante **Crear**, luego **Sitio**), los dos primeros niveles de esta Live Copy son *superficial*. Los elementos secundarios de la página no pertenecen a la relación dinámica, pero se desplegará si se encuentra una relación dinámica que coincida con el activador.

   Ayuda a evitar:

   * adición manual de idiomas en el modelo (por debajo del primer nivel)
   * añadir contenido manualmente directamente debajo de la raíz del idioma,
   * no lleva a que este nuevo contenido se transfiera automáticamente a la Live Copy durante el despliegue.

## MSM y sitios web multilingües {#msm-and-multilingual-websites}

MSM puede ayudar en la creación de sitios web multilingües de dos maneras:

* Al crear maestros de idiomas.

   * Mientras que MSM en sí **no proporciona traducción de contenido**, se puede integrar con conectores de traducción de terceros que sí lo hagan. Tenga en cuenta lo siguiente:

      * MSM le permite cancelar la herencia en el nivel de página o componente. Esto ayuda a evitar sobrescribir el contenido traducido (de una Live Copy, con contenido aún no traducido de un modelo) en la próxima implementación.
      * Algunos conectores de traducción de terceros automatizan esta administración de las herencias de MSM.

         Consulte a su proveedor de servicios de traducción para obtener más información.

      * Un enfoque alternativo para crear y traducir maestros de idiomas es usar copias de idiomas junto con el marco de trabajo de integración de traducción listo para usar de AEM.

* Al desplegar contenido desde maestros de idiomas.

   * Por ejemplo, desde el maestro de idioma francés hasta sitios específicos de cada país, como Francia/francés, Canadá/francés, Suiza/francés.

Para obtener más información, consulte [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md) y [Prácticas recomendadas de traducción](/help/sites-administering/tc-bp.md).

## Cambios y despliegues de la estructura {#structure-changes-and-rollouts}

Las modificaciones en la estructura de contenido de un modelo o árbol de origen se reflejan de forma diferente en una Live Copy. Esto depende del tipo de modificación:

* **Creación** las páginas nuevas de un modelo harán que las páginas correspondientes se creen en Live Copies después de la implementación con la configuración de lanzamiento estándar.

* **Eliminación** las páginas de un modelo harán que las páginas correspondientes se eliminen de las Live Copies después de la implementación con la configuración de lanzamiento estándar.

* **Mover** páginas en un modelo **not** como resultado, las páginas correspondientes se mueven en Live Copies después del lanzamiento con la configuración de lanzamiento estándar:

   * El motivo de este comportamiento es que mover una página incluye implícitamente eliminar una página. Esto podría provocar un comportamiento inesperado al publicar, ya que al eliminar páginas en el autor se desactiva automáticamente el contenido correspondiente al publicar. Esto también puede tener un efecto de activación en elementos relacionados, como vínculos, marcadores, etc.
   * La herencia de contenido en las respectivas páginas de Live Copy se actualiza para reflejar la nueva ubicación de sus orígenes en el modelo.
   * Para realizar el paso completo de una página de un modelo a Live Copies, tenga en cuenta las siguientes prácticas recomendadas:

>[!NOTE]
>
>Esto solo funcionará con la variable [Déclencheur de implementación](/help/sites-administering/msm-sync.md#rollout-triggers).

* Cree una configuración de despliegue personalizada:

   * Esta nueva configuración debe incluir la acción:

      `PageMoveAction`

      No agregue otras acciones a esta configuración.

* Coloque la nueva configuración:

   * Para desplegar completamente la página, mueva la página mientras elimina las páginas respectivas en su antigua ubicación en la Live Copy:

      * Coloque la configuración recién creada antes de la configuración de despliegue estándar.

         La configuración de lanzamiento estándar se encargará de eliminar las páginas en su antigua ubicación.
   * Para desplegar la página, mueva mientras mantiene las páginas respectivas en su antigua ubicación en las Live Copies (básicamente duplicando el contenido):

      * Coloque la configuración recién creada después de la configuración de despliegue estándar.

         Esto garantizará que no se elimine contenido en la Live Copy ni se desactive de la publicación.


## Personalización de despliegues {#customizing-rollouts}

Las configuraciones de despliegue de MSM son altamente personalizables. Debe tener en cuenta que la automatización de los despliegues puede tener consecuencias de gran alcance. Como práctica recomendada, debe planificar *very* cuidadosamente antes, por ejemplo:

* automatización de lanzamientos; por ejemplo, con [déclencheur onModify](#onmodify),
* personalización [tipos de nodo/propiedades](#node-types-properties),
* inicio de flujos de trabajo subsiguientes,
* y/o activar contenido como parte de los lanzamientos.

### onModify {#onmodify}

Al usar el [activador de despliegue](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify` debe tener en cuenta lo siguiente:

* Automatizar despliegues con activadores `onModify` puede tener un impacto negativo en el rendimiento de la creación, ya que activan despliegues después de cada modificación de la página.**

* El resultado del despliegue puede diferir del esperado, ya que:

   * No se puede especificar el orden de los eventos de modificación resultantes.
   * La arquitectura basada en eventos no puede garantizar la secuencia de eventos transferidos al administrador de despliegue.

* El uso de una configuración de despliegue de este tipo podría provocar conflictos de confirmación si se producen actualizaciones simultáneas del mismo recurso.

Por lo tanto, se recomienda que *only* use `onModify` déclencheur si los beneficios del inicio automático de la implementación superan cualquier problema de rendimiento potencial.

### Tipos de nodo/Propiedades {#node-types-properties}

Recuerde que:

* Además de personalizar las acciones de despliegue, MSM también le permite personalizar las propiedades de los nodos que se están desplegando. La variable [La configuración OSGi de MSM le permite excluir tipos de nodos](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) desde que se copia desde el origen a la Live Copy.

## Información adicional {#further-information}

Esta y las siguientes páginas tratan los problemas relacionados:

* [Creación y sincronización de Live Copies](/help/sites-administering/msm-livecopy.md)
* [Información general de Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Configuración de la sincronización de Live Copy](/help/sites-administering/msm-sync.md)
* [Conflictos de despliegue de MSM](/help/sites-administering/msm-rollout-conflicts.md)
