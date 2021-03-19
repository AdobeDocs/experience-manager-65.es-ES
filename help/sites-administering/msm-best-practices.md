---
title: Prácticas recomendadas de MSM
seo-title: Prácticas recomendadas de MSM
description: Encuentre las prácticas recomendadas recopiladas por los equipos de consultoría e ingeniería de Adobe para ayudarle a poner en marcha el administrador de varios sitios de AEM.
seo-description: Encuentre las prácticas recomendadas recopiladas por los equipos de consultoría e ingeniería de Adobe para ayudarle a poner en marcha el administrador de varios sitios de AEM.
uuid: cbb598bb-ec8f-4985-97af-7c87f5891c66
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 04344537-7485-40a9-ad14-804ba448f1e2
feature: Administrador de varios sitios
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 1%

---


# Prácticas recomendadas de MSM{#msm-best-practices}

## General {#general}

MSM es un marco configurable para automatizar la implementación de contenido. Las implementaciones suelen incluir partes importantes de un sitio web y abarcan organizaciones y zonas geográficas. Por lo tanto, es muy recomendable planificar las implementaciones de MSM con el cuidado con que planifica el sitio web:

* **estructura del plan y flujos de contenido** cuidadosamente antes de iniciar la implementación.
* **Mantenga la cantidad de Live Copies como mínimo.** El procesamiento de Live Copies es una tarea que consume muchos recursos. Cuantos más Live Copies existan en su sistema, más rendimiento se verá afectado: desde el procesamiento de índices de Live Copy internos, pasando por operaciones de Live Copy como despliegues, hasta operaciones de interfaz de usuario como mostrar relaciones de Live Copy en el carril de referencias del administrador de Sites. Una práctica recomendada es crear Live Copies de sitios o ramas de un sitio, donde las relaciones de Live Copy se heredan de las páginas del sitio o rama. Evite crear Live Copies individuales para páginas en un sitio o rama cuando toda la estructura se pueda convertir en una Live Copy.
* **Personalice tanto como sea necesario, pero tan poco como sea posible.** Aunque MSM admite un alto grado de personalización (p. ej., configuraciones de implementación), la práctica recomendada para el rendimiento, la fiabilidad y la capacidad de actualización de su sitio web es minimizar la personalización.
* Establezca un modelo de **administración** antes y capacite a los usuarios en consecuencia para garantizar el éxito. Una práctica recomendada desde el punto de vista del gobierno es **minimizar la autoridad que los productores de contenido local tienen** para asignar/conectar contenido a otros usuarios locales y sus respectivas Live Copies. Esto se debe a que las herencias encadenadas y no gobernadas pueden aumentar significativamente la complejidad de una estructura de MSM y comprometer su rendimiento y fiabilidad.

* Una vez que existe un plan para su estructura, flujos de contenido, automatización y administración: **prototipo y pruebe exhaustivamente su sistema**, antes de iniciar la implementación en vivo.
* Tenga en cuenta que los **asesores de Adobe y los integradores de sistemas líderes** tienen una planificación profunda de la experiencia e implementan la automatización de contenido con MSM, de modo que pueden ayudarle a empezar con su proyecto MSM y a lo largo de toda su implementación.

>[!NOTE]
>
>Encontrará más información sobre cómo trabajar con MSM en los artículos de la Base de conocimiento:
>
>* [Preguntas más frecuentes sobre MSM](https://helpx.adobe.com/experience-manager/kb/index/msm_faq.html)
>* [Solución de problemas de MSM](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-msm-issues.html)

>



>[!NOTE]
>
>También puede utilizar el [Componente de referencia](/help/sites-authoring/default-components-foundation.md#reference) para reutilizar una sola página o párrafo. No obstante, tenga en cuenta:
>
>* MSM es más flexible y permite un control detallado sobre qué contenido se sincroniza y cuándo.
>* [Ahora se recomiendan los ](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html) componentes principales en los componentes de base.

>



## Configuraciones de fuentes y modelos de Live Copy {#live-copy-sources-and-blueprint-configurations}

Tenga en cuenta que se puede crear una Live Copy utilizando [páginas normales](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) o una [configuración de modelo](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Ambos son casos de uso válidos.

Los beneficios adicionales de utilizar una configuración de modelo son que:

* Permita que el autor utilice la opción **Rollout** en un modelo para insertar (explícitamente) modificaciones en Live Copies que heredan de este modelo.
* Permita que el autor utilice **Crear sitio**; esto permite al usuario seleccionar fácilmente idiomas y configurar la estructura de la Live Copy.
* Defina una configuración de lanzamiento predeterminada para Live Copies que tengan una relación con el modelo.

En caso de que no se haga referencia a una configuración de modelo, los lanzamientos solo se pueden iniciar desde las propias Live Copies, lo que esencialmente extrae contenido del origen.

Al crear un nuevo sitio con Live Copy, es conveniente crear configuraciones de modelo para garantizar la disponibilidad del conjunto de funciones MSM completo.

## Sincronización de componentes y contenedores {#components-and-container-synchronization}

En general, la regla de implementación en MSM con respecto a la sincronización de componentes es:

* Los componentes se implementan sincronizando cualquier recurso contenido en el modelo.
* Los contenedores solo sincronizan el recurso actual.

Esto significa que los componentes se tratan como un agregado y, en un despliegue, el componente en sí y todos sus elementos secundarios se sustituyen por los de los modelos. Esto significa que si se agrega un recurso a un componente de este tipo localmente, se perderá por el contenido del modelo al implementarse.

Para admitir el anidado de componentes de modo que los componentes añadidos localmente se mantengan en un despliegue, el componente debe declararse como contenedor. Por ejemplo, el parsys predeterminado se declara como contenedor para que admita contenido añadido localmente.

>[!NOTE]
>
>Agregue la propiedad `cq:isContainer` al componente para designarlo como contenedor.

## Crear sitio {#create-site}

Tenga en cuenta que AEM tiene dos enfoques principales para crear Live Copies:

* Al [crear una Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   Este enfoque puede considerarse más genérico y le permite crear Live Copies desde cualquier página. La estructura de contenido de una Live Copy coincide exactamente con el origen.

* Al [crear un sitio](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   Se trata de un enfoque más especializado, principalmente para crear sitios web con una estructura multilingüe.

A continuación se indican algunas consideraciones que deben tenerse en cuenta al crear un sitio:

* Para crear un nuevo sitio, necesita una [configuración de modelo](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations).
* Para permitir la selección de rutas de idioma para crear en un sitio nuevo, las raíces de idioma correspondientes deben existir en el modelo (fuente).
* Una vez que se ha creado un [nuevo sitio como una Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (con **Crear** y, a continuación, **Sitio**), los dos primeros niveles de esta Live Copy son *superficiales*. Los elementos secundarios de la página no pertenecen a la relación de vida, pero se seguirá desplegando si se encuentra una relación de vida que coincida con el déclencheur.

   Ayuda a evitar:

   * adición manual de idiomas en el modelo (por debajo del primer nivel)
   * añadir contenido manualmente directamente debajo de la raíz del idioma,
   * no lleva a que este nuevo contenido se transfiera automáticamente a la Live Copy durante el despliegue.

## MSM y sitios web multilingües {#msm-and-multilingual-websites}

MSM puede ayudar en la creación de sitios web multilingües de dos maneras:

* Al crear maestros de idiomas.

   * Aunque el propio MSM **no proporciona traducción de contenido**, se puede integrar con conectores de traducción de terceros que sí proporcionan. Tenga en cuenta que:

      * MSM le permite cancelar la herencia en el nivel de página o componente. Esto ayuda a evitar sobrescribir el contenido traducido (de una Live Copy, con contenido aún no traducido de un modelo) en la próxima implementación.
      * Algunos conectores de traducción de terceros automatizan esta administración de las heredaciones de MSM.

         Consulte a su proveedor de servicios de traducción para obtener más información.

      * Un enfoque alternativo para crear y traducir maestros de idiomas es usar copias de idiomas junto con AEM marco de integración de traducción listo para usar.

* Al desplegar contenido desde maestros de idiomas.

   * Por ejemplo, desde el maestro de idioma francés hasta sitios específicos de cada país, como Francia/francés, Canadá/francés, Suiza/francés.

Para obtener más información, consulte [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md) y [Prácticas recomendadas de traducción](/help/sites-administering/tc-bp.md).

## Cambios de estructura y lanzamientos {#structure-changes-and-rollouts}

Las modificaciones en la estructura de contenido de un modelo o árbol de origen se reflejan de forma diferente en una Live Copy. Esto depende del tipo de modificación:

* **** Al crear páginas nuevas en un modelo, las páginas correspondientes se crearán en Live Copies después del lanzamiento con la configuración de lanzamiento estándar.

* **** Al eliminar páginas en un modelo, las páginas correspondientes se eliminarán de las Live Copies después del lanzamiento con la configuración de lanzamiento estándar.

* **** Mover páginas en un modelo  **** no dará como resultado que las páginas correspondientes se movieran en Live Copies después del lanzamiento con la configuración de lanzamiento estándar:

   * El motivo de este comportamiento es que un movimiento de página incluye implícitamente una eliminación de página. Esto podría provocar un comportamiento inesperado al publicar, ya que al eliminar páginas en el autor se desactiva automáticamente el contenido correspondiente al publicar. Esto también puede tener un efecto de activación en elementos relacionados, como vínculos, marcadores, etc.
   * La herencia de contenido en las respectivas páginas de Live Copy se actualiza para reflejar la nueva ubicación de sus orígenes en el modelo.
   * Para realizar el paso completo de una página de un modelo a Live Copies, tenga en cuenta las siguientes prácticas recomendadas:

>[!NOTE]
>
>Esto solo funcionará con el [déclencheur de despliegue de activación](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/msm-sync.html#rollout-triggers).

* Cree una configuración de lanzamiento personalizada:

   * Esta nueva configuración debe incluir la acción :

      `PageMoveAction`

      No agregue otras acciones a esta configuración.

* Coloque la nueva configuración:

   * Para desplegar completamente la página, mueva la página mientras elimina las páginas respectivas en su antigua ubicación en la Live Copy:

      * Coloque la configuración recién creada antes de la configuración de lanzamiento estándar.

         La configuración de lanzamiento estándar se encargará de eliminar las páginas en su antigua ubicación.
   * Para desplegar la página, mueva mientras mantiene las páginas respectivas en su antigua ubicación en las Live Copies (básicamente duplicando el contenido):

      * Coloque la configuración recién creada después de la configuración de lanzamiento estándar.

         Esto garantizará que no se elimine contenido en la Live Copy ni se desactive de la publicación.


## Personalización de lanzamientos {#customizing-rollouts}

Las configuraciones de implementación de MSM son altamente personalizables. Debe tener en cuenta que la automatización de las implementaciones puede tener consecuencias de gran alcance. Como práctica recomendada, debe planificar *very* cuidadosamente antes, por ejemplo:

* automatización de lanzamientos; por ejemplo, con [onModify déclencheur](#onmodify),
* personalización de [tipos de nodo/propiedades](#node-types-properties),
* inicio de flujos de trabajo subsiguientes,
* y/o activar contenido como parte de los lanzamientos.

### onModify {#onmodify}

Al utilizar el [déclencheur de implementación](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify` debe tener en cuenta que:

* La automatización de las implementaciones con déclencheur `onModify` puede tener un impacto negativo en el rendimiento de la creación, ya que déclencheur las implementaciones después de *cada* modificación de página.

* El resultado de la implementación puede diferir del esperado, ya que:

   * No se puede especificar el orden de los eventos de modificación resultantes.
   * La arquitectura basada en eventos no puede garantizar la secuencia de eventos pasados al administrador de implementación.

* El uso de una configuración de lanzamiento de este tipo podría provocar conflictos de confirmación si se producen actualizaciones simultáneas del mismo recurso.

Por lo tanto, se recomienda que *solo* utilice `onModify` déclencheur si los beneficios del inicio de la implementación automática superan cualquier posible problema de rendimiento.

### Tipos de nodo/Propiedades {#node-types-properties}

Recuerde que:

* Además de personalizar las acciones de implementación, MSM también le permite personalizar las propiedades de los nodos que se están implementando. La configuración [MSM OSGi permite excluir los tipos de nodo](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) de la copia desde el origen a la Live Copy.

## Información adicional {#further-information}

Esta y las siguientes páginas tratan los problemas relacionados:

* [Creación y sincronización de Live Copies](/help/sites-administering/msm-livecopy.md)
* [Consola de información general de Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Configuración de la sincronización de Live Copy](/help/sites-administering/msm-sync.md)
* [Conflictos de implementación de MSM](/help/sites-administering/msm-rollout-conflicts.md)

