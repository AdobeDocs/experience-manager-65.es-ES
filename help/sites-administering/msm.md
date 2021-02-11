---
title: '"Reutilización del contenido: administrador de varios sitios y Live Copy"'
seo-title: '"Reutilización del contenido: administrador de varios sitios y Live Copy"'
description: Obtenga información sobre la reutilización de contenido con Live Copies y el Administrador de varios sitios.
seo-description: Obtenga información sobre la reutilización de contenido con Live Copies y el Administrador de varios sitios.
uuid: 9f955226-8fc9-4357-b90c-c6896b0dc4b4
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: c21debc3-ecf4-4aa9-ab5a-18ddd5cf2fff
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2684'
ht-degree: 1%

---


# Reutilización del contenido: administrador de varios sitios y Live Copy{#reusing-content-multi-site-manager-and-live-copy}

Multi Site Manager (MSM) le permite utilizar el mismo contenido del sitio en varias ubicaciones. MSM utiliza la funcionalidad Live Copy para lograr esto:

* Con MSM puede:

   * Crear contenido una vez y después
   * Copie este contenido en otras áreas ([Live Copies](#live-copies)) del mismo sitio u otros sitios y vuelva a utilizarlo.

* A continuación, MSM mantiene las relaciones (activas) entre el contenido de origen y sus Live Copies para que:

   * Al realizar cambios en el contenido de origen, las copias originales y las Live Copy se sincronizan (para aplicar estos cambios también a las Live Copies).
   * Puede realizar ajustes en el contenido de las copias en vivo desconectando la relación en vivo de subpáginas o componentes individuales. Al hacer esto, los cambios en el origen ya no se aplicarán a la Live Copy.

Esta y las páginas siguientes cubren los problemas relacionados:

* [Creación y sincronización de Live Copies](/help/sites-administering/msm-livecopy.md)
* [Consola de información general de Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Configuración de la sincronización de Live Copy](/help/sites-administering/msm-sync.md)
* [Conflictos de despliegue de MSM](/help/sites-administering/msm-rollout-conflicts.md)
* [Prácticas recomendadas de MSM](/help/sites-administering/msm-best-practices.md)

## Posibles escenarios {#possible-scenarios}

Hay muchos casos de uso para MSM y copias en vivo, algunos escenarios incluyen:

* **Multinacionales: Compañía de Global a Local**

   Un caso de uso típico que admite MSM es reutilizar contenido en varios sitios multinacionales en el mismo idioma. Esto permite reutilizar el contenido principal, permitiendo al mismo tiempo variaciones nacionales.

   Por ejemplo: la sección en inglés del ejemplo del sitio de referencia We.Retail se crea para los clientes de EE.UU. La mayor parte del contenido de este sitio también puede utilizarse para otros sitios Web.Retail que atienden a clientes angloparlantes de diferentes países y culturas. El contenido principal sigue siendo el mismo en todos los sitios, mientras que se pueden realizar ajustes regionales.

   Se puede utilizar la siguiente estructura para los sitios de Estados Unidos, Reino Unido, Canadá y Australia:

   ```xml
   /content
       |- we.retail
           |- language-masters
               |- en
       |- we.retail
           |- us
               |- en
       |- we.retail
           |- gb
               |- en
       |- we.retail
           |- ca
               |- en
       |- we.retail
           |- au
               |- en
   ```

   >[!NOTE]
   >
   >MSM no traduce el contenido. Se utiliza para crear la estructura necesaria e implementar el contenido.
   >
   >
   >Consulte [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md) si desea ampliar este ejemplo.

* **Nacional - Oficina Central de las Sucursales Regionales**

   Otra posibilidad es que una compañía con una red de agentes desee sitios web separados para sus concesionarios individuales, cada uno de los cuales sea una variación del sitio principal proporcionado por la oficina principal. Esto podría ser para una sola compañía con múltiples oficinas regionales, o un sistema nacional de franquicia compuesto por un franquiciador central y múltiples franquiciados locales.

   La oficina central puede proporcionar la información básica, mientras que las entidades regionales pueden añadir información local, como datos de contacto, horas de apertura y eventos.

   ```xml
   /content
       |- head-office-Berlin
       |- branch-Hamburg
       |- branch-Stuttgart
       |- branch-Munich
       |- branch-Frankfurt
   ```

* **Varias versiones**

   O bien, puede utilizar MSM para crear versiones de una subrama específica; por ejemplo, un subsitio de soporte que contenga detalles de las diferentes versiones de un producto específico, donde la información de base permanezca constante y solo se deban cambiar las características actualizadas:

   ```xml
   /content
       |- support
           |- product X
               |- v5.0
               |- v4.0
               |- v3.0
               |- v2.0
               |- v1.0
   ```

   >[!NOTE]
   >
   >En este escenario siempre se plantea la cuestión de si hacer una copia directa o utilizar copias en directo.
   >
   >Hay un equilibrio entre:
   >
   >  * Cuánta parte del contenido principal necesitará actualizarse en las distintas versiones.
   >
   >En contra:
   >
   >  * La cantidad de copias individuales deberá ajustarse.


## MSM de la interfaz de usuario {#msm-from-the-ui}

Se puede acceder directamente a MSM en la interfaz de usuario mediante diversas opciones desde la consola adecuada. Para presentar las siguientes listas, especifique las ubicaciones principales:

* **Crear sitio** (**sitios**)

   * MSM le ayuda a administrar varios sitios web que comparten contenido común; por ejemplo, los sitios web suelen proporcionarse para audiencias internacionales, de modo que la mayor parte del contenido es común en todos los países, con un subconjunto del contenido específico de cada país. MSM le permite [crear copias en vivo que actualizan automáticamente uno o más sitios en función del sitio de origen](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Esto también le ayuda a aplicar una estructura base común, a utilizar el contenido común en varios sitios, a mantener un aspecto y una presentación comunes y a concentrar los esfuerzos en la administración del contenido que en realidad difiere entre los sitios.
   * Requiere una configuración de modelo predefinida para especificar el origen.
   * Crea una Live Copy del origen (predefinido).
   * Proporciona al usuario el botón **Desplegar**.

* **Crear Live Copy** (**Sitios**)

   * MSM le permite [crear una Live Copy ad-hoc (única) de una página o subrama individual de un sitio Web](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page); por ejemplo, duplicar una subrama para proporcionar información sobre una versión nueva o actualizada de un producto.
   * Crea una Live Copy ad-hoc (no se requiere configuración de modelo).
   * Se puede utilizar para crear (inmediatamente) una Live Copy de cualquier página o rama.
   * Requiere **Sincronizar** (no proporciona el botón **Desplegar**).

* **Propiedades**  de vista(**sitios**)

   * Cuando corresponda, esta opción le ayuda a [monitorear su Live Copy](/help/sites-administering/msm-livecopy.md#monitoring-your-live-copy) al proporcionar información sobre el **Live Cop** y o **modelo** relacionado.

* **Referencias** (**Sitios**)

   * El carril [References](/help/sites-authoring/basic-handling.md#references) proporciona información sobre **Live Copies** junto con acceso a las acciones apropiadas.

* **Live Copy Overview** (**Sitios**)

   * Esta consola le permite [vista y administrar su modelo y sus copias en vivo](/help/sites-administering/msm-livecopy-overview.md).

* **Modelos** (**Herramientas** -  **Sitios**)

   * Esta consola le permite [crear y administrar sus configuraciones de modelo](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration).

>[!NOTE]
>
>Los aspectos de la funcionalidad de MSM se utilizan en varias otras funciones de AEM (por ejemplo, Lanzamientos, Catálogo); en estos casos, la Live Copy se administra mediante esa función.

### Términos utilizados {#terms-used}

Como introducción, la siguiente tabla proporciona una visión general de los principales términos utilizados con MSM; estas secciones y páginas se tratarán en mayor detalle:

<table>
 <tbody>
  <tr>
   <td><strong>Término</strong></td>
   <td><strong>Definición</strong></td>
   <td><strong>Detalles adicionales</strong></td>
  </tr>
  <tr>
   <td><strong>Origen</strong></td>
   <td>Las páginas originales.</td>
   <td>Sinónimo de las páginas Blueprints y/o Blueprint.</td>
  </tr>
  <tr>
   <td><strong>Live Copy   </strong></td>
   <td>La copia (del origen), mantenida por las acciones de sincronización definidas por las configuraciones de despliegue. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Configuración de Live Copy</strong></td>
   <td>Definición de los detalles de configuración de una Live Copy.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Relación activa</strong><br /> </td>
   <td>Definición efectiva de la herencia para un recurso determinado; las conexiones entre el origen y las copias en vivo.<br /> </td>
   <td>Garantiza que los cambios en el origen se puedan sincronizar con la Live Copy.</td>
  </tr>
  <tr>
   <td><strong>Modelo</strong></td>
   <td>Sinónimo de Source.</td>
   <td>Se puede definir mediante una configuración de modelo.</td>
  </tr>
  <tr>
   <td><strong>Configuración del modelo</strong></td>
   <td>Configuración predefinida que especifica una ruta de origen.</td>
   <td>Cuando se hace referencia a una página de modelo en una configuración de modelo, el comando Desplegar está disponible.</td>
  </tr>
  <tr>
   <td><strong>Sincronización</strong></td>
   <td>Término genérico para la sincronización de contenido entre el origen y las copias en vivo (por <strong>Despliegue</strong> y <strong>Sincronización</strong>).</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Despliegue</strong><br /> </td>
   <td>Sincroniza desde el origen con la Live Copy.<br /> Puede activarlo un autor (en una página de modelo) o un evento del sistema (según lo definido por la configuración de implementación).</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Configuración de despliegue</strong></td>
   <td>Reglas que determinan qué propiedades se sincronizarán, cómo y cuándo.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Sincronizar</strong></td>
   <td>Solicitud manual de sincronización, realizada a partir de las páginas de Live Copy.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Herencia</strong></td>
   <td>Una página o componente de Live Copy hereda el contenido de su componente o página de origen cuando se produce la sincronización.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Suspender</strong></td>
   <td>Elimina temporalmente la relación activa entre una Live Copy y su página de modelo.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Desasociar</strong></td>
   <td>Elimina permanentemente la relación activa entre una Live Copy y su página de modelo.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Restablecer</strong></td>
   <td><p>Restablecer una página de Live Copy a:</p>
    <ul>
     <li>Eliminar todas las cancelaciones de herencia y<br /> </li>
     <li>Devuelva la página al mismo estado que la página de origen.</li>
    </ul> <p>Restablecer afecta a los cambios realizados en las propiedades de página, el sistema de párrafos y los componentes.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Superficial</strong></td>
   <td>Una Live Copy de una sola página.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Profundo</strong></td>
   <td>Copia en vivo de una página, junto con sus páginas secundarias.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Consulte [Información general de la API de Java](/help/sites-developing/extending-msm.md#overview-of-the-java-api) para conocer los nombres de los objetos.

## Live Copies {#live-copies}

Una Live Copy MSM es una copia del contenido específico del sitio para el cual se mantiene una relación activa con el origen original:

* La Live Copy hereda el contenido de su origen.
* La sincronización realiza la transferencia real de contenido cuando se realizan cambios en el origen.
* Una Live Copy puede considerarse como:

   * Superficial: una sola página
   * Profundo: la página, junto con sus páginas secundarias

* Las reglas de sincronización, llamadas configuraciones de implementación, determinan qué propiedades se sincronizan y cuándo se produce la sincronización.

En el ejemplo anterior, `/content/we-retail/language-masters/en` es la ubicación maestra global en inglés. Para reutilizar el contenido de este sitio, se crean copias en vivo de MSM:

* El contenido que se muestra a continuación `/content/we-retail/language-masters/en` es el origen.

* El contenido que se muestra a continuación `/content/we-retail/language-masters/en` se copia debajo de los nodos `/content/we-retail/us/en/`, `/content/we-retail/gb/en`, `/content/we-retail/ca/en` y `/content/we-retail/au/en`. Estas son las copias en vivo.

* Los autores realizan cambios en las páginas siguientes `/content/we-retail/language-masters/en`.
* Cuando se activa, MSM sincroniza estos cambios con las copias activas.

### Live Copies - Composición {#live-copies-composition}

>[!NOTE]
>
>Los diagramas y las descripciones de esta sección representan instantáneas de copias en directo potenciales. No son exhaustivas, pero proporcionan una visión general para resaltar características específicas.

Al crear una Live Copy por primera vez, las páginas de origen seleccionadas se reflejan en 1:1 en la Live Copy. Después de esto, también se pueden crear nuevos recursos (páginas y/o párrafos) directamente dentro de la Live Copy, por lo que es útil tener en cuenta estas variaciones y cómo afectan a la sincronización. Las composiciones posibles incluyen:

* [Live Copy con páginas que no sean Live Copy](#live-copy-with-non-live-copy-pages)
* [Live Copies anidadas](#nested-live-copies)

La forma básica de Live Copy es:

* Copie en vivo las páginas que reflejan las páginas de origen seleccionadas en 1:1.
* Una definición de configuración.
* Una relación activa definida para cada recurso:

   * Vincule el recurso de Live Copy con su modelo/origen.
   * Se utilizan al realizar la herencia y la implementación.

* Los cambios pueden [sincronizarse](/help/sites-administering/msm-livecopy.md#synchronizing-your-live-copy) según los requisitos.

![chlimage_1-367](assets/chlimage_1-367.png)

#### Live Copy con páginas que no sean Live Copy {#live-copy-with-non-live-copy-pages}

Cuando crea una Live Copy en AEM puede ver y navegar por la rama Live Copy, y utilizar la funcionalidad AEM normal en la rama Live Copy. Esto significa que usted (o un proceso) puede crear nuevos recursos (páginas y/o párrafos) dentro de la rama Live Copy (p. ej. `myCanadaOnlyProduct`).

* Estos recursos no tienen una relación activa con las páginas de origen/modelo y no están sincronizados.
* Se pueden producir escenarios que MSM maneja como casos especiales. Por ejemplo, cuando crea (o un proceso) una página con la misma posición y nombre en las ramas de origen/modelo y Live Copy. Para estas situaciones, consulte [Conflictos de despliegue de MSM](/help/sites-administering/msm-rollout-conflicts.md) para obtener más información.

![chlimage_1-368](assets/chlimage_1-368.png)

#### Copias Live Copies anidadas {#nested-live-copies}

Cuando usted (o un proceso) crea una [nueva página dentro de una Live Copy](#live-copy-with-non-live-copy-pages) existente, esta nueva página también se puede configurar como una Live Copy de un modelo diferente. Esto se conoce como Live Copy anidada, donde el comportamiento de la segunda Live Copy (interna) se ve afectado por la primera Live Copy (externa) de la siguiente manera:

* Un despliegue profundo activado para la Live Copy de nivel superior se puede continuar en la Live Copy anidada (por ejemplo, si el déclencheur coincide).
* Los vínculos entre las fuentes se reescribirán dentro de las copias en vivo.

   Por ejemplo, los vínculos del segundo al primer modelo se reescribirán como vínculos desde la Live Copy anidada/segunda a la primera Live Copy.

![chlimage_1-369](assets/chlimage_1-369.png)

>[!NOTE]
>
>Si mueve o cambia el nombre de una página dentro de la rama de Live Copy, se tratará (internamente) como una Live Copy anidada para permitir que AEM rastreen las relaciones.

#### Copias Live Copies apiladas {#stacked-live-copies}

Una Live Copy se denomina Live Copy apilada cuando se crea como el elemento secundario de una Live Copy superficial. Se comporta de la misma manera que una [Live Copy anidada](#nested-live-copies).

### Configuraciones de origen, modelos y modelo {#source-blueprints-and-blueprint-configurations}

Cualquier página o rama de páginas puede utilizarse como fuente de una Live Copy.

Sin embargo, MSM también permite definir una configuración de modelo que especifica una ruta de origen. Las ventajas de utilizar una configuración de modelo son que:

* Permita que el autor utilice la opción **Desplegar** en un modelo: para (explícitamente) insertar modificaciones en las copias en vivo que heredan de este modelo.
* Permitir al autor utilizar **Crear sitio**; esto permite al usuario seleccionar idiomas fácilmente y configurar la estructura de la Live Copy.
* Defina una configuración de implementación predeterminada para las copias en vivo que tengan una relación con el modelo.

El origen de una Live Copy puede ser páginas normales o páginas englobadas por una configuración de modelo; ambos son casos de uso válidos.

El origen forma el modelo para la Live Copy. El modelo se define cuando:

* [Crear una configuración de modelo](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)

   La configuración define (con antelación) las páginas que se utilizarán para crear la Live Copy.

* [Creación de una Live Copy de una página](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   Las páginas utilizadas para crear la Live Copy (las páginas de origen) son las páginas de modelo.

   Se puede hacer referencia a la página de origen mediante una configuración de modelo o no.

### Despliegue y sincronización {#rollout-and-synchronize}

Un despliegue es la acción MSM central que sincroniza las copias en vivo con su origen. Puede realizar las implementaciones manualmente o automáticamente:

* Se puede definir una [configuración de implementación](#rollout-configurations) para que [eventos](/help/sites-administering/msm-sync.md#rollout-triggers) específicos puedan provocar que se produzca un despliegue automáticamente.
* Al crear una página de modelo, puede utilizar el comando [Desplegar](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) para insertar cambios en la Live Copy.

   **El** comando Rolloutcommand está disponible en una página de modelo a la que se hace referencia mediante una configuración de modelo.

   ![chlimage_1-370](assets/chlimage_1-370.png)

* Al crear una página de Live Copy, puede utilizar el comando [Sincronizar](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) para extraer los cambios del origen a la Live Copy.

   El comando **Sincronizar** siempre está disponible en la página de Live Copy (independientemente de si la página de origen/modelo está incluida en una configuración de modelo).

   ![chlimage_1-371](assets/chlimage_1-371.png)

### Opciones de configuración del lanzamiento {#rollout-configurations}

Una configuración de implementación define cuándo y cómo se sincroniza una Live Copy con el contenido de origen. Una configuración de implementación consiste en un déclencheur y una o varias acciones de sincronización:

* **Activador**

   Un déclencheur es un evento que provoca la sincronización de la acción activa, como la activación de una página de origen. MSM define los déclencheur que puede utilizar.

* **Acciones de sincronización**

   Se realizan en la Live Copy para sincronizarla con el origen. Las acciones de ejemplo son copiar contenido, ordenar nodos secundarios y activar la página de Live Copy. MSM proporciona una serie de acciones de sincronización.

   >[!NOTE]
   >
   >Puede crear acciones personalizadas para su instancia mediante la API de Java.

Las configuraciones de despliegue se pueden reutilizar para que más de una Live Copy pueda utilizar la misma configuración de implementación. En una instalación estándar se incluyen varias [configuraciones de implementación](/help/sites-administering/msm-sync.md#installed-rollout-configurations).

### Conflictos de despliegue {#rollout-conflicts}

Los despliegues pueden resultar complicados, especialmente cuando los autores editan contenido tanto en el origen como en la Live Copy, por lo que es útil tener en cuenta cómo AEM gestiona los [conflictos que puedan producirse durante la implementación](/help/sites-administering/msm-rollout-conflicts.md).

### Suspensión y cancelación de herencia y sincronización {#suspending-and-cancelling-inheritance-and-synchronization}

Cada página y componente de una Live Copy se asocia con su página de origen y componente mediante una relación activa. La relación activa configura la sincronización del contenido de Live Copy desde el origen.

Puede **Suspender** la herencia de Live Copy de una página de Live Copy para poder cambiar las propiedades y los componentes de la página. Al suspender la herencia, las propiedades y los componentes de la página ya no se sincronizan con el origen.

Al editar una página individual, los autores pueden **Cancelar herencia** para un componente. Cuando se cancela la herencia, la relación activa se suspende y la sincronización no se produce para ese componente. La cancelación de la herencia y la sincronización resulta útil cuando es necesario personalizar las subsecciones del contenido.

### Desconexión de Live Copy {#detaching-a-live-copy}

También puede [separar una Live Copy](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) de su modelo para eliminar todas las conexiones.

>[!CAUTION]
>
>La acción Desconectar es permanente e irreversible.

Separar de forma permanente elimina la relación activa entre una Live Copy y su página de modelo. Todas las propiedades relevantes para MSM se eliminan de la Live Copy y las páginas de Live Copy se convierten en una copia independiente.

>[!NOTE]
>
>Consulte [Desconexión de una Live Copy](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) para obtener más detalles. incluyendo el impacto relacionado en las páginas secundarias y superiores.

## Pasos estándar para usar MSM {#standard-steps-for-using-msm}

Los siguientes pasos describen el procedimiento estándar para utilizar MSM para reutilizar contenido y sincronizar cambios en copias en vivo.

1. Desarrollar el contenido del sitio de origen.
1. Determine la configuración de despliegue que se va a utilizar.

   1. MSM [instala varias configuraciones de implementación](/help/sites-administering/msm-sync.md#installed-rollout-configurations) que pueden satisfacer una serie de casos de uso.
   1. Opcionalmente, puede [crear una configuración de implementación](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) si es necesario.

1. Determinar dónde debe [especificar las configuraciones de implementación para utilizar](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use) y configurarlas según sea necesario.
1. Si es necesario, [cree una configuración de modelo](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration) que identifique el contenido de origen de la Live Copy.
1. [Cree una Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy).
1. Realice los cambios necesarios en el contenido de origen. Debe emplear el proceso normal de revisión y aprobación de contenido que su organización ha establecido.
1. [Desplácese ](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) por el plano o  [sincronice la ](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) copia en vivo con los cambios.

## Personalización de MSM {#customizing-msm}

MSM proporciona herramientas para que la implementación se pueda adaptar a las complejidades excepcionales que pueden existir al compartir contenido:

* **Configuraciones de implementación personalizadas**
   [Cree una ](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) configuración de implementación cuando las configuraciones de implementación instaladas no cumplan con sus requisitos. Puede utilizar cualquier déclencheur de implementación y acción de sincronización disponibles.

* **Acciones de sincronización personalizada**
   [Cree una ](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) acción de sincronización personalizada cuando las acciones instaladas no cumplan los requisitos específicos de la aplicación. MSM proporciona una API de Java para crear acciones de sincronización personalizadas.

## Prácticas recomendadas   {#best-practices}

La página [Prácticas recomendadas de MSM](/help/sites-administering/msm-best-practices.md) contiene información importante sobre la implementación.
