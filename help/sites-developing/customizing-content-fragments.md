---
title: Personalizar y ampliar fragmentos de contenido
seo-title: Personalizar y ampliar fragmentos de contenido
description: Un fragmento de contenido amplía un recurso estándar.
seo-description: Un fragmento de contenido amplía un recurso estándar.
uuid: f72c3a23-9b0d-4fab-a960-bb1350f01175
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d0770bee-4be5-4a6a-8415-70fdfd75015c
docset: aem65
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '2749'
ht-degree: 1%

---


# Personalizar y ampliar fragmentos de contenido{#customizing-and-extending-content-fragments}

Un fragmento de contenido extiende un recurso estándar; consulte:

* [Creación y administración de ](/help/assets/content-fragments/content-fragments.md) fragmentos de contenido y  [creación de páginas con ](/help/sites-authoring/content-fragments.md) fragmentos de contenido para obtener más información sobre los fragmentos de contenido.

* [Administración de ](/help/assets/manage-assets.md) recursos y  [personalización y ampliación de ](/help/assets/extending-assets.md) recursos para obtener más información sobre los recursos estándar.

## Arquitectura {#architecture}

Las [partes constituyentes](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) básicas de un fragmento de contenido son:

* Un *fragmento de contenido,*
* consistente en uno o más *Elemento de contenido* s,
* y que pueden tener una o más *Variación de contenido* s.

Según el tipo de fragmento, también se utilizan modelos o plantillas:

>[!CAUTION]
>
>[Ahora se recomiendan ](/help/assets/content-fragments/content-fragments-models.md) los modelos de fragmentos de contenido para crear todos los fragmentos.
>
>Los modelos de fragmentos de contenido se utilizan en todos los ejemplos de We.Retail.

* Modelos de fragmento de contenido:

   * Se utiliza para definir fragmentos de contenido que contienen contenido estructurado.
   * Los modelos de fragmento de contenido definen la estructura de un fragmento de contenido al crearlo.
   * Un fragmento hace referencia al modelo; por lo tanto, los cambios en el modelo pueden/afectarán a cualquier fragmento dependiente.
   * Los modelos están compuestos por tipos de datos.
   * Las funciones para agregar nuevas variaciones, etc., deben actualizar el fragmento según corresponda.

   >[!CAUTION]
   >
   >Cualquier cambio en un modelo de fragmento de contenido existente puede afectar a los fragmentos dependientes; esto puede llevar a propiedades huérfanas en esos fragmentos.

* Plantillas de fragmento de contenido:

   * Se utiliza para definir fragmentos de contenido sencillos.
   * Las plantillas definen la estructura (básica, de solo texto) de un fragmento de contenido cuando se crea.
   * La plantilla se copia en el fragmento cuando se crea; por lo tanto, los cambios adicionales en la plantilla no se reflejarán en los fragmentos existentes.
   * Las funciones para agregar nuevas variaciones, etc., deben actualizar el fragmento según corresponda.
   * [Las ](/help/sites-developing/content-fragment-templates.md) plantillas de fragmento de contenido funcionan de una manera diferente a la de otros mecanismos de plantilla dentro del ecosistema de AEM (por ejemplo, plantillas de página, etc.). Por lo tanto, deben considerarse por separado.
   * Cuando se basa en una plantilla, el tipo MIME del contenido se administra en el contenido real; esto significa que cada elemento y variación puede tener un tipo MIME diferente.

### Integración con Assets {#integration-with-assets}

Content Fragment Management (CFM) es parte de AEM Assets como:

* Los fragmentos de contenido son recursos.
* Utilizan la funcionalidad de Recursos existente.
* Están totalmente integrados con Recursos (consolas de administración, etc.).

#### Asignación de fragmentos de contenido estructurado a recursos {#mapping-structured-content-fragments-to-assets}

![fragmento a recursos estructurados](assets/fragment-to-assets-structured.png)

Los fragmentos de contenido con contenido estructurado (es decir, basados en un modelo de fragmento de contenido) se asignan a un solo recurso:

* Todo el contenido se almacena en el nodo `jcr:content/data` del recurso:

   * Los datos del elemento se almacenan en el subnodo maestro:
      `jcr:content/data/master`

   * Las variaciones se almacenan bajo un subnodo que lleva el nombre de la variación:
p. ej. `jcr:content/data/myvariation`

   * Los datos de cada elemento se almacenan en el subnodo correspondiente como una propiedad con el nombre del elemento:
Por ejemplo: el contenido del elemento `text` se almacena como propiedad `text` en `jcr:content/data/master`

* Los metadatos y el contenido asociado se almacenan por debajo de `jcr:content/metadata`
Excepto el título y la descripción, que no se consideran metadatos tradicionales y se almacenan en 
`jcr:content`

#### Asignación de fragmentos de contenido simple a recursos {#mapping-simple-content-fragments-to-assets}

![chlimage_1-90](assets/chlimage_1-90.png)

Los fragmentos de contenido simple (basados en una plantilla) se asignan a una composición compuesta por un recurso principal y subrecursos (opcionales):

* Toda la información que no sea de contenido de un fragmento (como título, descripción, metadatos, estructura) se administra exclusivamente en el recurso principal.
* El contenido del primer elemento de un fragmento se asigna a la representación original del recurso principal.

   * Las variaciones (si las hay) del primer elemento se asignan a otras representaciones del recurso principal.

* Los elementos adicionales (si existen) se asignan a subrecursos del recurso principal.

   * El contenido principal de estos elementos adicionales se asigna a la representación original del subactivo correspondiente.
   * Otras variaciones (si procede) de cualquier elemento adicional se relacionan con otras representaciones del subactivo correspondiente.

#### Ubicación del recurso {#asset-location}

Al igual que con los recursos estándar, un fragmento de contenido se incluye en:

`/content/dam`

#### Permisos de recursos {#asset-permissions}

Para obtener más información, consulte [Fragmento de contenido - Eliminar consideraciones](/help/assets/content-fragments/content-fragments-delete.md).

#### Integración de funciones {#feature-integration}

* La función Administración de fragmentos de contenido (CFM) se basa en el núcleo de recursos, pero debe ser lo más independiente posible.
* CFM proporciona sus propias implementaciones para los elementos de las vistas de tarjeta/columna/lista; estos complementos se conectan a las implementaciones de representación de contenido de Recursos existentes.
* Se han ampliado varios componentes de Recursos para incluir fragmentos de contenido.

### Uso de fragmentos de contenido en páginas {#using-content-fragments-in-pages}

>[!CAUTION]
>
>Ahora se recomienda el [componente principal del fragmento de contenido](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html). Consulte [Desarrollo de componentes principales](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) para obtener más detalles.

Se puede hacer referencia a los fragmentos de contenido desde AEM páginas, al igual que a cualquier otro tipo de recurso. AEM proporciona el componente principal [**Fragmento de contenido**](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html), un [componente que permite incluir fragmentos de contenido en las páginas](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page). También puede ampliar este componente principal **Fragmento de contenido**.

* El componente utiliza la propiedad `fragmentPath` para hacer referencia al fragmento de contenido real. La propiedad `fragmentPath` se administra de la misma manera que otras propiedades similares de otros tipos de recursos; por ejemplo, cuando el fragmento de contenido se mueve a otra ubicación.

* El componente permite seleccionar la variación que se va a mostrar.
* Además, se puede seleccionar un rango de párrafos para restringir el resultado; por ejemplo, esto se puede utilizar para la salida de varias columnas.
* El componente permite [contenido intermedio](/help/sites-developing/components-content-fragments.md#in-between-content):

   * Aquí el componente permite colocar otros recursos (imágenes, etc.) entre los párrafos del fragmento al que se hace referencia.
   * Para el contenido intermedio debe:

      * ser conscientes de la posibilidad de referencias inestables; el contenido intermedio (agregado al crear una página) no tiene una relación fija con el párrafo al que está situado, insertando un nuevo párrafo (en el editor de fragmentos de contenido) antes de que la posición del contenido intermedio pueda perder la posición relativa
      * considere los parámetros adicionales (como los filtros de variante y párrafo) para evitar falsos positivos en los resultados de búsqueda

>[!NOTE]
>
>**Modelo de fragmento de contenido:**
>
>Cuando se utiliza un fragmento de contenido basado en un modelo de fragmento de contenido en una página, se hace referencia al modelo. Esto significa que si el modelo no se ha publicado en el momento de publicar la página, se marcará y el modelo se agregará a los recursos que se publicarán con la página.
>
>**Plantilla de fragmento de contenido:**
>
>Cuando se utiliza un fragmento de contenido basado en una plantilla de fragmento de contenido en una página, no hay referencia ya que la plantilla se copió al crear el fragmento.

#### Configuración mediante la consola OSGi {#configuration-using-osgi-console}

La implementación back-end de fragmentos de contenido es, por ejemplo, responsable de hacer que las instancias de un fragmento se utilicen en una página en la que se pueda buscar o de administrar el contenido de medios mixtos. Esta implementación necesita saber qué componentes se utilizan para procesar fragmentos y cómo se parametriza el procesamiento.

Los parámetros para esto se pueden configurar en la [Consola Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), para el paquete OSGi **Configuración del componente de fragmento de contenido**.

* **Tipos**
de recursoslista de 
`sling:resourceTypes` se puede proporcionar para definir los componentes que se utilizan para procesar fragmentos de contenido y a los que se debe aplicar el procesamiento en segundo plano.

* **Propiedades de**
referenciaSe puede configurar una lista de propiedades para especificar dónde se almacena la referencia al fragmento para el componente correspondiente.

>[!NOTE]
>
>No existe una asignación directa entre el tipo de componente y la propiedad.
>
>AEM simplemente toma la primera propiedad que se encuentra en un párrafo. Así que debe elegir las propiedades con cuidado.

![captura de pantalla_2019-03-18at100941](assets/screenshot_2019-03-18at100941.png)

Aún hay algunas directrices que debe seguir para garantizar que el componente sea compatible con el procesamiento en segundo plano del fragmento de contenido:

* El nombre de la propiedad donde se definen los elementos que se van a procesar debe ser `element` o `elementNames`.

* El nombre de la propiedad donde se define la variación que se va a representar debe ser `variation` o `variationName`.

* Si se admite la salida de varios elementos (mediante `elementNames` para especificar varios elementos), el modo de visualización real se define con la propiedad `displayMode`:

   * Si el valor es `singleText` (y sólo hay un elemento configurado), el elemento se representa como texto con contenido intermedio, compatibilidad con el diseño, etc. Es el valor predeterminado para los fragmentos en los que solo se procesa un solo elemento.
   * De lo contrario, se utiliza un enfoque mucho más sencillo (podría denominarse &quot;vista de formulario&quot;), en el que no se admite contenido intermedio y el contenido del fragmento se representa &quot;tal cual&quot;.

* Si el fragmento se procesa para `displayMode` == `singleText` (implícita o explícitamente), entran en juego las siguientes propiedades adicionales:

   * `paragraphScope` define si se deben representar todos los párrafos, o solo un rango de párrafos (valores:  `all` vs.  `range`)

   * si `paragraphScope` == `range` la propiedad `paragraphRange` define el rango de párrafos que se van a procesar

### Integración con otros marcos {#integration-with-other-frameworks}

Los fragmentos de contenido se pueden integrar con:

* **Traducciones**

   Los fragmentos de contenido están completamente integrados con el [flujo de trabajo de traducción de ](/help/sites-administering/tc-manage.md) AEM. A nivel arquitectónico, esto significa:

   * Las traducciones individuales de un fragmento de contenido son en realidad fragmentos independientes; por ejemplo:

      * están situadas bajo diferentes raíces lingüísticas:

         `/content/dam/<path>/en/<to>/<fragment>`

         vs.

         `/content/dam/<path>/de/<to>/<fragment>`

      * pero comparten exactamente la misma ruta relativa debajo de la raíz del idioma:

         `/content/dam/<path>/en/<to>/<fragment>`

         vs.

         `/content/dam/<path>/de/<to>/<fragment>`
   * Además de las rutas basadas en reglas, no hay más conexión entre las distintas versiones de idioma de un fragmento de contenido; se gestionan como dos fragmentos independientes, aunque la interfaz de usuario proporciona los medios para desplazarse entre las variantes de idioma.
   >[!NOTE]
   >
   >El flujo de trabajo de traducción AEM funciona con `/content`:
   >
   >    * Dado que los modelos de fragmentos de contenido residen en `/conf`, no se incluyen en dichas traducciones. Puede [internacionalizar las cadenas de IU](/help/sites-developing/i18n-dev.md).
      >
      >    
   * Las plantillas se copian para crear el fragmento de modo que quede implícito.


* **Esquemas de metadatos**

   * Los fragmentos de contenido (re)utilizan los [esquemas de metadatos](/help/assets/metadata-schemas.md), que se pueden definir con recursos estándar.
   * CFM ofrece su propio esquema específico:

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      esto se puede ampliar si es necesario.

   * El formulario de esquema correspondiente se integra con el editor de fragmentos.

## La Content Fragment Management API - Server-Side {#the-content-fragment-management-api-server-side}

Puede utilizar la API del lado del servidor para acceder a los fragmentos de contenido; consulte:

[com.adobe.cq.dam.cfm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/package-summary.html)

>[!CAUTION]
>
>Se recomienda encarecidamente utilizar la API del lado del servidor en lugar de acceder directamente a la estructura de contenido.

### Interfaces clave {#key-interfaces}

Las tres interfaces siguientes pueden servir como puntos de entrada:

* **Plantilla**  de fragmento([FragmentTemplate](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html))

   Utilice `FragmentTemplate.createFragment()` para crear un nuevo fragmento.

   ```
   Resource templateOrModelRsc = resourceResolver.getResource("...");
   FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
   ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
   ```

   Esta interfaz representa:

   * un modelo de fragmento de contenido o una plantilla de fragmento de contenido desde la cual crear un fragmento de contenido,
   * y (después de la creación) la información estructural de dicho fragmento

   Esta información puede incluir:

   * Acceso a datos básicos (título, descripción)
   * Obtenga acceso a plantillas y modelos para los elementos del fragmento:

      * Plantillas de elementos de lista
      * Obtener información estructural para un elemento determinado
      * Acceder a la plantilla de elementos (consulte `ElementTemplate`)
   * Acceder a plantillas para las variaciones del fragmento:

      * Plantillas de variación de lista
      * Obtener información estructural para una variación determinada
      * Acceder a la plantilla de variación (consulte `VariationTemplate`)
   * Obtener contenido asociado inicial

   Interfaces que representan información importante:

   * `ElementTemplate`

      * Obtener datos básicos (nombre, título)
      * Obtener contenido inicial del elemento
   * `VariationTemplate`

      * Obtener datos básicos (nombre, título, descripción)






* **Fragmento**  de contenido([ContentFragment](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   Esta interfaz le permite trabajar con un fragmento de contenido de forma abstracta.

   >[!CAUTION]
   >
   >Se recomienda enfáticamente acceder a un fragmento a través de esta interfaz. Se debe evitar cambiar directamente la estructura de contenido.

   La interfaz le proporciona los medios para:

   * Administrar datos básicos (por ejemplo, obtener nombre; get/set title/description)
   * Acceso a metadatos
   * Elementos de acceso:

      * Elementos de lista
      * Obtener elementos por nombre
      * Crear nuevos elementos (consulte [Advertencias](#caveats))

      * Acceso a datos de elementos (consulte `ContentElement`)
   * Variaciones de lista definidas para el fragmento
   * Crear nuevas variaciones globalmente
   * Administrar contenido asociado:

      * Colecciones de lista
      * Añadir colecciones
      * Eliminar colecciones
   * Acceso al modelo o plantilla del fragmento

   Las interfaces que representan los elementos principales de un fragmento son:

   * **Elemento**  de contenido([ContentElement](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Obtener datos básicos (nombre, título, descripción)
      * Obtener o definir contenido
      * Variaciones de acceso de un elemento:

         * Variaciones de lista
         * Obtener variaciones por nombre
         * Crear nuevas variaciones (consulte [Advertencias](#caveats))
         * Quitar variaciones (consulte [Advertencias](#caveats))
         * Acceso a datos de variación (consulte `ContentVariation`)
      * Método abreviado para resolver variaciones (aplicando alguna lógica adicional de reserva específica para la implementación si la variación especificada no está disponible para un elemento)
   * **Variación**  de contenido([ContentVariation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Obtener datos básicos (nombre, título, descripción)
      * Obtener o definir contenido
      * Sincronización simple, basada en la información modificada por última vez

   Las tres interfaces ( `ContentFragment`, `ContentElement`, `ContentVariation`) extienden la interfaz `Versionable`, que agrega capacidades de versiones, requeridas para los fragmentos de contenido:

   * Crear nueva versión del elemento
   * Versiones de lista del elemento
   * Obtener el contenido de una versión específica del elemento con versiones







### Adaptación: Uso de adaptabilidad() {#adapting-using-adaptto}

Se pueden adaptar los siguientes elementos:

* `ContentFragment` puede adaptarse a:

   * `Resource` - el recurso Sling subyacente; tenga en cuenta que la actualización del subyacente  `Resource` directamente requiere la reconstrucción del  `ContentFragment` objeto.

   * `Asset` - la  `Asset` abstracción DAM que representa el fragmento de contenido; tenga en cuenta que la actualización  `Asset` directa requiere la reconstrucción del  `ContentFragment` objeto.

* `ContentElement` puede adaptarse a:

   * `ElementTemplate` - para acceder a la información estructural del elemento.

* `FragmentTemplate` puede adaptarse a:

   * `Resource` -  `Resource` determinar el modelo al que se hace referencia o la plantilla original copiada;

      * los cambios realizados a través del `Resource` no se reflejan automáticamente en el `FragmentTemplate`.

* `Resource` puede adaptarse a:

   * `ContentFragment`
   * `FragmentTemplate`

### Advertencias {#caveats}

Cabe señalar que:

* La API se implementa para proporcionar funcionalidad admitida por la interfaz de usuario.
* Toda la API está diseñada para **no** persistir cambios automáticamente (a menos que se indique lo contrario en el JavaDoc de API). Por lo tanto, siempre tendrá que transferir la resolución de recursos de la solicitud correspondiente (o la resolución que esté utilizando).
* Tareas que podrían requerir un esfuerzo adicional:

   * La creación o eliminación de nuevos elementos no actualizará la estructura de datos de fragmentos simples (basados en una plantilla de fragmento).
   * La creación de nuevas variaciones desde `ContentElement` no actualizará la estructura de datos (pero crearlas globalmente desde `ContentFragment` sí lo hará).

   * La eliminación de las variaciones existentes no actualizará la estructura de datos.

## Content Fragment Management API - Cliente {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>Para AEM 6.5, la API del lado del cliente es interna.

### Información adicional {#additional-information}

Consulte lo siguiente:

* `filter.xml`

   El `filter.xml` para la administración de fragmentos de contenido está configurado para que no se superponga con el paquete de contenido principal de Recursos.

## Editar sesiones {#edit-sessions}

Una sesión de edición se inicia cuando el usuario abre un fragmento de contenido en una de las páginas del editor. La sesión de edición finaliza cuando el usuario abandona el editor seleccionando **Guardar** o **Cancelar**.

### Requisitos {#requirements}

Los requisitos para controlar una sesión de edición son:

* Editar un fragmento de contenido, que puede abarcar varias vistas (= páginas HTML), debe ser atómico.
* La edición también debe ser *transaccional*; al final de la sesión de edición, los cambios se deben confirmar (guardar) o revertir (cancelar).
* Los casos perimetrales deben gestionarse correctamente; estas situaciones incluyen situaciones como cuando el usuario abandona la página introduciendo una dirección URL manualmente o utilizando la navegación global.
* Debe estar disponible un guardado automático periódico (cada x minutos) para evitar la pérdida de datos.
* Si dos usuarios editan un fragmento de contenido al mismo tiempo, no deben sobrescribir los cambios de los demás.

#### Procesos {#processes}

Los procesos involucrados son:

* Inicio de una sesión

   * Se crea una nueva versión del fragmento de contenido.
   * Se ha iniciado el guardado automático.
   * Se configuran las cookies; definen el fragmento que se está editando y que hay una sesión de edición abierta.

* Finalización de una sesión

   * Se ha detenido el guardado automático.
   * Al confirmar:

      * Se actualiza la última información modificada.
      * Las cookies se eliminan.
   * Al revertir:

      * Se restaura la versión del fragmento de contenido que se creó al iniciar la sesión de edición.
      * Las cookies se eliminan.


* Edición

   * Todos los cambios (guardado automático incluido) se realizan en el fragmento de contenido activo, no en un área separada y protegida.
   * Por lo tanto, esos cambios se reflejan inmediatamente en AEM páginas que hacen referencia al fragmento de contenido correspondiente

#### Acciones {#actions}

Las acciones posibles son:

* Introducción de una página

   * Compruebe si ya hay una sesión de edición; comprobando la cookie correspondiente.

      * Si existe una, compruebe que la sesión de edición se inició para el fragmento de contenido que se está editando actualmente

         * Si el fragmento actual, vuelva a establecer la sesión.
         * Si no es así, intente cancelar la edición del fragmento de contenido editado anteriormente y eliminar las cookies (no habrá ninguna sesión de edición posterior).
      * Si no existe ninguna sesión de edición, espere a que el usuario realice el primer cambio (véase más abajo).
   * Compruebe si ya se hace referencia al fragmento de contenido en una página y, en caso afirmativo, muestre la información adecuada.



* Cambio de contenido

   * Siempre que el usuario cambia de contenido y no hay una sesión de edición presente, se crea una nueva sesión de edición (consulte [Inicio de una sesión](#processes)).

* Salida de una página

   * Si hay una sesión de edición presente y los cambios no se han mantenido, se muestra un cuadro de diálogo de confirmación modal para notificar al usuario la pérdida potencial de contenido y permitirle permanecer en la página.

## Ejemplos {#examples}

### Ejemplo: Acceso a un fragmento de contenido existente {#example-accessing-an-existing-content-fragment}

Para conseguirlo, puede adaptar el recurso que representa la API a:

`com.adobe.cq.dam.cfm.ContentFragment`

Por ejemplo:

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### Ejemplo: Creación de un nuevo fragmento de contenido {#example-creating-a-new-content-fragment}

Para crear un nuevo fragmento de contenido mediante programación, debe utilizar:

`com.adobe.cq.dam.cfm.ContentFragmentManager#create`

Por ejemplo:

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Ejemplo: Especificación del intervalo de guardado automático {#example-specifying-the-auto-save-interval}

El intervalo de guardado automático (medido en segundos) se puede definir con el administrador de configuración (ConfMgr):

* Nodo: `<*conf-root*>/settings/dam/cfm/jcr:content`
* Nombre de propiedad: `autoSaveInterval`
* Tipo: `Long`

* Predeterminado: `600` (10 minutos); esto se define en `/libs/settings/dam/cfm/jcr:content`

Si desea establecer un intervalo de guardado automático de 5 minutos, debe definir la propiedad en el nodo; por ejemplo:

* Nodo: `/conf/global/settings/dam/cfm/jcr:content`
* Nombre de propiedad: `autoSaveInterval`

* Tipo: `Long`

* Valor: `300` (5 minutos equivale a 300 segundos)

## Plantillas de fragmento de contenido {#content-fragment-templates}

Consulte [Plantillas de fragmento de contenido](/help/sites-developing/content-fragment-templates.md) para obtener información completa.

## Componentes para la creación de páginas {#components-for-page-authoring}

Para obtener más información, consulte

* [Componentes principales - Componente](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)  de fragmento de contenido (recomendado)
* [Componentes de fragmento de contenido: Componentes para la creación de páginas](/help/sites-developing/components-content-fragments.md#components-for-page-authoring)
