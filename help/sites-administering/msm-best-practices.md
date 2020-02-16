---
title: Prácticas recomendadas de MSM
seo-title: Prácticas recomendadas de MSM
description: Encuentre las prácticas recomendadas compiladas por los equipos de ingeniería y consultoría de Adobe para ayudarle en el uso inicial del administrador de multisitio de AEM.
seo-description: Encuentre las prácticas recomendadas compiladas por los equipos de ingeniería y consultoría de Adobe para ayudarle en el uso inicial del administrador de multisitio de AEM.
uuid: cbb598bb-ec8f-4985-97af-7c87f5891c66
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 04344537-7485-40a9-ad14-804ba448f1e2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Prácticas recomendadas de MSM{#msm-best-practices}

## General {#general}

MSM es un marco configurable para automatizar la implementación de contenido. Las implementaciones suelen incluir partes importantes de un sitio web y abarcan organizaciones y regiones geográficas. Por lo tanto, es muy recomendable planificar las implementaciones de MSM con el cuidado con que planifica el sitio web:

* Antes de iniciar la implementación, **planifique cuidadosamente la estructura y los flujos** de contenido.
* **Personalice tanto como sea necesario, pero tan poco como sea posible.** Aunque MSM admite un alto grado de personalización (por ejemplo, configuraciones de implementación), la mejor práctica para el rendimiento, la fiabilidad y la actualización del sitio Web es minimizar la personalización.
* Establezca un modelo de **gobernanza** pronto y capacite a los usuarios en consecuencia para garantizar el éxito. Una práctica recomendada desde el punto de vista de la gobernanza es **minimizar la autoridad que los productores de contenido local tienen** para asignar/conectar contenido a otros usuarios locales y sus respectivas copias en vivo. Esto se debe a que las herencias encadenadas y no gobernadas pueden aumentar significativamente la complejidad de una estructura de MSM y comprometer su rendimiento y fiabilidad.

* Una vez que existe un plan para su estructura, los flujos de contenido, la automatización y la gobernanza: **cree prototipos y realice pruebas exhaustivas del sistema** antes de iniciar la implementación en directo.
* Tenga en cuenta que los **asesores de Adobe y los integradores** líderes del sistema tienen una amplia experiencia en la planificación e implementación de la automatización de contenido con MSM, por lo que pueden ayudarle a empezar a trabajar con su proyecto MSM y a lo largo de toda su implementación.

>[!NOTE]
>
>Encontrará más información sobre cómo trabajar con MSM en los artículos de la Base de conocimiento:
>
>* [Preguntas más frecuentes sobre MSM](https://helpx.adobe.com/experience-manager/kb/index/msm_faq.html)
>* [Resolución de problemas de MSM](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-msm-issues.html)
>



>[!NOTE]
>
>También puede utilizar el componente [](/help/sites-authoring/default-components-foundation.md#reference) Referencia para reutilizar una sola página o párrafo. Sin embargo, tenga en cuenta:
>
>* MSM es más flexible y permite un control preciso sobre qué contenido se sincroniza y cuándo.
>* [Ahora se recomiendan los componentes](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) principales a lo largo de los componentes básicos.
>



## Fuentes de Live Copy y configuraciones de modelo {#live-copy-sources-and-blueprint-configurations}

Tenga en cuenta que una Live Copy se puede crear con páginas [](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) regulares o con una configuración [de](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)modelo. Ambos son casos de uso válidos.

Las ventajas adicionales del uso de una configuración de modelo son que:

* Permita que el autor utilice la opción **Desplegar** en un modelo; para (explícitamente) insertar modificaciones en las copias en vivo que hereden de este modelo.
* Permitir al autor utilizar **Crear sitio**; esto permite al usuario seleccionar idiomas fácilmente y configurar la estructura de la Live Copy.
* Defina una configuración de implementación predeterminada para las copias en vivo que tengan una relación con el modelo.

En el caso de que no se haga referencia a una configuración de modelo, solo se pueden iniciar las implementaciones desde las propias copias en vivo, principalmente extrayendo contenido del origen.

Al crear un nuevo sitio con Live Copy, resulta ventajoso crear configuraciones de modelo para garantizar la disponibilidad del conjunto completo de funciones de MSM.

## Sincronización de componentes y contenedores {#components-and-container-synchronization}

En general, la regla de implementación en MSM con respecto a la sincronización de componentes es:

* Los componentes se distribuyen sincronizando los recursos contenidos en el modelo.
* Los contenedores solo sincronizan el recurso actual.

Esto significa que los componentes se tratan como un agregado y, en un despliegue, el componente mismo y todos sus elementos secundarios se reemplazan por los de los modelos. Esto significa que si un recurso se agrega a un componente de este tipo localmente, se perderá en el contenido del modelo durante la implementación.

Para admitir el anidado de componentes de modo que los componentes agregados localmente se mantengan en una implementación, el componente debe declararse como contenedor. Por ejemplo, el parsys predeterminado se declara como contenedor para que admita contenido agregado localmente.

>[!NOTE]
>
>Agregue la propiedad `cq:isContainer` al componente para designarlo como contenedor.

## Crear sitio {#create-site}

Tenga en cuenta que AEM tiene dos métodos principales para crear copias en directo:

* When [creating a Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   Este enfoque puede considerarse más genérico y le permite crear copias en vivo desde cualquier página. La estructura de contenido de una Live Copy coincide exactamente con el origen.

* Al [crear un sitio](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   Se trata de un enfoque más especializado, principalmente para crear sitios web con una estructura multilingüe.

A continuación se indican algunas consideraciones que deben tenerse en cuenta al crear un sitio:

* Para crear un nuevo sitio, necesita una configuración [de modelo](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations).
* Para permitir la selección de rutas de idioma que se van a crear en un nuevo sitio, las raíces de idioma correspondientes deben existir en el modelo (origen).
* Una vez que se ha creado un [nuevo sitio como Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (mediante **Crear**, luego **Sitio**), los dos primeros niveles de esta Live Copy son *poco profundos*. Los elementos secundarios de la página no pertenecen a la relación activa, pero un despliegue seguirá descendiendo si se encuentra una relación activa que coincida con el activador.

   Ayuda a evitar:

   * adición manual de idiomas en el modelo (por debajo del primer nivel)
   * agregar contenido manualmente directamente debajo de la raíz del idioma,
   * no resulta en la transmisión automática de este nuevo contenido a la Live Copy durante la implementación.

## MSM y sitios web multilingües {#msm-and-multilingual-websites}

MSM puede ayudar en la creación de sitios web multilingües de dos maneras:

* Al crear maestros de idioma.

   * Aunque MSM **no proporciona traducción** de contenido, puede integrarse con conectores de traducción de terceros que sí lo hacen. Tenga en cuenta que:

      * MSM permite cancelar la herencia en el nivel de página y/o componente. Esto ayuda a evitar la sobrescritura de contenido traducido (de una Live Copy, con contenido aún no traducido de un modelo) en la próxima implementación.
      * Algunos conectores de traducción de terceros automatizan esta administración de las herencias de MSM.

         Consulte con su proveedor de servicios de traducción para obtener más información.

      * Un método alternativo para crear y traducir maestros de idiomas es utilizar copias de idiomas junto con el marco de integración de traducción incorporado de AEM.

* Cuando se despliega contenido desde maestros de idiomas.

   * Por ejemplo, desde el maestro de francés a sitios específicos de países, como Francia/francés, Canadá/francés, Suiza/francés.

Para obtener más información, consulte [Traducción de contenido para sitios](/help/sites-administering/translation.md) multilingües y Prácticas recomendadas [de](/help/sites-administering/tc-bp.md)traducción.

## Cambios y versiones de estructura {#structure-changes-and-rollouts}

Las modificaciones en la estructura de contenido de un modelo o árbol de origen se reflejan de forma diferente en una Live Copy. Esto depende del tipo de modificación:

* **La creación** de nuevas páginas en un modelo dará como resultado que las páginas correspondientes se creen en Live Copies después de la implementación con la configuración de implementación estándar.

* **Al eliminar** páginas en un modelo, las páginas correspondientes se eliminarán de las Live Copies después de la implementación con la configuración de implementación estándar.

* **Si mueve** páginas en un modelo, **no se moverán** las páginas correspondientes en Live Copy después de la implementación con la configuración de implementación estándar:

   * El motivo de este comportamiento es que un movimiento de página incluye implícitamente una eliminación de página. Esto podría provocar un comportamiento inesperado al publicar, ya que al eliminar páginas del autor, se desactiva automáticamente el contenido correspondiente al publicar. Esto también puede tener un efecto de contagio en elementos relacionados como vínculos, marcadores y otros.
   * La herencia de contenido en las páginas de Live Copy respectivas se actualiza para reflejar la nueva ubicación de sus orígenes en el modelo.
   * Para realizar un paso completo de una página de un modelo a copias en vivo, considere las siguientes optimizaciones:

>[!NOTE]
>
>Esto solo funcionará con el activador [](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/msm-sync.html#rollout-triggers)Al desplegar.

* Cree una configuración de implementación personalizada:

   * Esta nueva configuración debe incluir la acción:

      `PageMoveAction`

      No agregue otras acciones a esta configuración.

* Coloque la nueva configuración:

   * Para desplegar completamente la página, se mueve, mientras se eliminan las páginas respectivas en su ubicación anterior en la Live Copy:

      * Coloque la configuración recién creada antes de la configuración de implementación estándar.

         La configuración de implementación estándar se encargará de eliminar las páginas en su ubicación anterior.
   * Para desplegar la página, mueva las páginas respectivas en su ubicación anterior en las copias en vivo (básicamente duplicando el contenido):

      * Coloque la configuración recién creada después de la configuración de implementación estándar.

         Esto garantizará que no se elimine ningún contenido de la Live Copy ni se desactive de la publicación.


## Personalización de grupos de trabajo {#customizing-rollouts}

Las configuraciones de implementación de MSM son altamente personalizables. Debe tener en cuenta que la automatización de las implementaciones puede tener consecuencias de gran alcance. Como práctica recomendada, debe planear *muy* cuidadosamente antes, por ejemplo:

* automatización de implementaciones; por ejemplo, con los activadores [onModify](#onmodify),
* personalizar tipos y propiedades [de nodos](#node-types-properties),
* iniciar flujos de trabajo subsiguientes,
* y/o activar contenido como parte de los lanzamientos.

### onModify {#onmodify}

Al utilizar el [activador](/help/sites-administering/msm-sync.md#rollout-triggers) de despliegue `onModify` debe tener en cuenta lo siguiente:

* La automatización de los despliegues con `onModify` activadores puede tener un impacto negativo en el rendimiento de la creación, ya que activan los despliegues después de *cada* modificación de página.

* El resultado de la implementación puede diferir del esperado, ya que:

   * No se puede especificar el orden de los eventos de modificación resultantes.
   * La arquitectura basada en eventos no puede garantizar la secuencia de eventos pasados al Administrador de implementación.

* El uso de una configuración de implementación de este tipo podría provocar conflictos de confirmación si se producen actualizaciones simultáneas del mismo recurso.

Por lo tanto, se recomienda que *solo* utilice `onModify` activadores si los beneficios de la iniciación automática de la implementación superan cualquier problema de rendimiento potencial.

### Tipos de nodo/Propiedades {#node-types-properties}

Recuerde que:

* Además de personalizar las acciones de implementación, MSM también permite personalizar las propiedades de nodo que se están implementando. La configuración OSGi de [MSM le permite excluir los tipos](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) de nodos de la copia desde el origen a la Live Copy.

## Información adicional {#further-information}

Esta y las páginas siguientes cubren los problemas relacionados:

* [Creación y sincronización de Live Copies](/help/sites-administering/msm-livecopy.md)
* [Consola de información general de Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Configuración de la sincronización de Live Copy](/help/sites-administering/msm-sync.md)
* [Conflictos de despliegue de MSM](/help/sites-administering/msm-rollout-conflicts.md)

