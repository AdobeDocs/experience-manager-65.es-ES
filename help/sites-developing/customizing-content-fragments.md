---
title: Personalizar y ampliar fragmentos de contenido
seo-title: Customizing and Extending Content Fragments
description: Un fragmento de contenido amplía un recurso estándar.
seo-description: A content fragment extends a standard asset.
uuid: f72c3a23-9b0d-4fab-a960-bb1350f01175
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d0770bee-4be5-4a6a-8415-70fdfd75015c
docset: aem65
exl-id: 08c88e70-4df9-4627-8a66-1fabe3aee50b
source-git-commit: 2ec9625d480eb8cae23f44aa247fce2a519dec31
workflow-type: tm+mt
source-wordcount: '2772'
ht-degree: 1%

---

# Personalizar y ampliar fragmentos de contenido{#customizing-and-extending-content-fragments}

Un fragmento de contenido amplía un recurso estándar; consulte:

* [Creación y administración de ](/help/assets/content-fragments/content-fragments.md) fragmentos de contenido y  [creación de páginas con ](/help/sites-authoring/content-fragments.md) fragmentos de contenido para obtener más información sobre los fragmentos de contenido.

* [Administración de ](/help/assets/manage-assets.md) recursos y  [personalización y ampliación de ](/help/assets/extending-assets.md) recursos para obtener más información sobre los recursos estándar.

## Arquitectura {#architecture}

Las [partes constituyentes](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) básicas de un fragmento de contenido son:

* Un *fragmento de contenido,*
* formado por uno o más *Content Element* s,
* y que pueden tener una o más *Variación de contenido* s.

Según el tipo de fragmento, también se utilizan modelos o plantillas:

>[!CAUTION]
>
>[Ahora se recomiendan los ](/help/assets/content-fragments/content-fragments-models.md) modelos de fragmento de contenido para crear todos los fragmentos.
>
>Los modelos de fragmentos de contenido se utilizan en todos los ejemplos de We.Retail.

>[!NOTE]
>
>Antes de AEM 6.3, los fragmentos de contenido se creaban con el uso de plantillas en lugar de modelos. Las plantillas ya no están disponibles para crear nuevos fragmentos, pero los fragmentos creados con una plantilla de este tipo siguen siendo compatibles.

* Modelos de fragmento de contenido:

   * Se utiliza para definir fragmentos de contenido que contienen contenido estructurado.
   * Los modelos de fragmento de contenido definen la estructura de un fragmento de contenido cuando se crea.
   * Un fragmento hace referencia al modelo; por lo tanto, los cambios en el modelo pueden/afectarán a cualquier fragmento dependiente.
   * Los modelos son tipos de datos integrados.
   * Las funciones para agregar nuevas variaciones, etc., deben actualizar el fragmento en consecuencia.

   >[!CAUTION]
   >
   >Cualquier cambio en un modelo de fragmento de contenido existente puede afectar a los fragmentos dependientes; esto puede llevar a propiedades huérfanas en esos fragmentos.

* Plantillas de fragmento de contenido:

   * Se utiliza para definir fragmentos de contenido simples.
   * Las plantillas definen la estructura (básica, de solo texto) de un fragmento de contenido cuando se crea.
   * La plantilla se copia en el fragmento cuando se crea; por lo tanto, los cambios adicionales en la plantilla no se reflejarán en los fragmentos existentes.
   * Las funciones para agregar nuevas variaciones, etc., deben actualizar el fragmento en consecuencia.
   * [Las ](/help/sites-developing/content-fragment-templates.md) plantillas de fragmento de contenido funcionan de una manera diferente a la de otros mecanismos de creación de plantillas dentro del ecosistema de AEM (por ejemplo, plantillas de página, etc.). Por lo tanto, deben considerarse por separado.
   * Cuando se basa en una plantilla, el tipo MIME del contenido se administra en el contenido real; esto significa que cada elemento y variación puede tener un tipo MIME diferente.

### Integración con Assets {#integration-with-assets}

La administración de fragmentos de contenido (CFM) forma parte de AEM Assets como:

* Los fragmentos de contenido son recursos.
* Utilizan la funcionalidad de recursos existente.
* Están totalmente integrados con Assets (consolas de administración, etc.).

#### Asignación de fragmentos de contenido estructurados a recursos {#mapping-structured-content-fragments-to-assets}

![estructurada de fragmento a activo](assets/fragment-to-assets-structured.png)

Los fragmentos de contenido con contenido estructurado (es decir, basados en un modelo de fragmento de contenido) se asignan a un único recurso:

* Todo el contenido se almacena en el nodo `jcr:content/data` del recurso:

   * Los datos del elemento se almacenan en el subnodo maestro:
      `jcr:content/data/master`

   * Las variaciones se almacenan en un subnodo que lleva el nombre de la variación:
p. ej. `jcr:content/data/myvariation`

   * Los datos de cada elemento se almacenan en el subnodo respectivo como una propiedad con el nombre del elemento:
Por ejemplo, el contenido del elemento `text` se almacena como propiedad `text` en `jcr:content/data/master`

* Los metadatos y el contenido asociado se almacenan debajo de `jcr:content/metadata`
Excepto el título y la descripción, que no se consideran metadatos tradicionales y se almacenan en 
`jcr:content`

#### Asignación de fragmentos de contenido simples a recursos {#mapping-simple-content-fragments-to-assets}

![chlimage_1-90](assets/chlimage_1-90.png)

Los fragmentos de contenido simples (basados en una plantilla) se asignan a una composición compuesta que consta de un recurso principal y subrecursos (opcionales):

* Toda la información que no sea de contenido de un fragmento (como título, descripción, metadatos, estructura) se administra exclusivamente en el recurso principal.
* El contenido del primer elemento de un fragmento se asigna a la representación original del recurso principal.

   * Las variaciones (si hay alguna) del primer elemento se asignan a otras representaciones del recurso principal.

* Los elementos adicionales (si existen) se asignan a subrecursos del recurso principal.

   * El contenido principal de estos elementos adicionales se asigna a la representación original del subactivo correspondiente.
   * Otras variaciones (si procede) de cualquier elemento adicional se corresponden con otras representaciones del subactivo respectivo.

#### Ubicación del recurso {#asset-location}

Al igual que con los recursos estándar, un fragmento de contenido se mantiene en:

`/content/dam`

#### Permisos de recursos {#asset-permissions}

Para obtener más información, consulte [Fragmento de contenido - Eliminar consideraciones](/help/assets/content-fragments/content-fragments-delete.md).

#### Integración de funciones {#feature-integration}

* La función Administración de fragmentos de contenido (CFM) se basa en el núcleo de recursos, pero debe ser lo más independiente posible.
* CFM proporciona sus propias implementaciones para los elementos de las vistas de tarjeta, columna o lista; estos complementos en las implementaciones de renderización de contenido de Assets existentes.
* Se han ampliado varios componentes de Assets para adaptarse a los fragmentos de contenido.

### Uso de fragmentos de contenido en páginas {#using-content-fragments-in-pages}

>[!CAUTION]
>
>Ahora se recomienda el [Componente principal del fragmento de contenido](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html). Consulte [Desarrollo de componentes principales](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) para obtener más información.

Se puede hacer referencia a los fragmentos de contenido desde AEM páginas, igual que a cualquier otro tipo de recurso. AEM proporciona el [**fragmento de contenido** componente principal](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html), un [componente que le permite incluir fragmentos de contenido en sus páginas](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page). También puede ampliar este componente principal **Fragmento de contenido**.

* El componente utiliza la propiedad `fragmentPath` para hacer referencia al fragmento de contenido real. La propiedad `fragmentPath` se gestiona de la misma manera que las propiedades similares de otros tipos de recursos; por ejemplo, cuando el fragmento de contenido se mueve a otra ubicación.

* El componente permite seleccionar la variación que se va a mostrar.
* Además, se puede seleccionar un rango de párrafos para restringir el resultado; por ejemplo, esto se puede utilizar para la salida de varias columnas.
* El componente permite [contenido intermedio](/help/sites-developing/components-content-fragments.md#in-between-content):

   * Aquí el componente le permite colocar otros recursos (imágenes, etc.) entre los párrafos del fragmento al que se hace referencia.
   * Para el contenido intermedio, debe:

      * ser conscientes de la posibilidad de referencias inestables; el contenido intermedio (añadido al crear una página) no tiene relación fija con el párrafo al que está colocado, insertando un nuevo párrafo (en el editor de fragmentos de contenido) antes de que la posición del contenido intermedio pueda perder la posición relativa
      * considere los parámetros adicionales (como los filtros de variación y párrafo) para evitar falsos positivos en los resultados de búsqueda

>[!NOTE]
>
>**Modelo de fragmento de contenido:**
>
>Cuando se utiliza un fragmento de contenido basado en un modelo de fragmento de contenido en una página, se hace referencia al modelo. Esto significa que si el modelo no se ha publicado en el momento de publicar la página, se marcará y el modelo se añadirá a los recursos que se publicarán con la página.
>
>**Plantilla de fragmento de contenido:**
>
>Cuando se utiliza un fragmento de contenido basado en una plantilla de fragmento de contenido en una página, no hay referencia ya que la plantilla se copió al crear el fragmento.

#### Configuración mediante la consola OSGi {#configuration-using-osgi-console}

La implementación back-end de los fragmentos de contenido es, por ejemplo, responsable de hacer que las instancias de un fragmento se utilicen en una página en la que se pueda buscar, o de administrar el contenido de medios mixtos. Esta implementación debe saber qué componentes se utilizan para procesar fragmentos y cómo se parametriza la renderización.

Los parámetros para esto se pueden configurar en la [Consola Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), para el paquete OSGi **Configuración del componente de fragmento de contenido**.

* **Tipos de**
recursoUna lista de 
`sling:resourceTypes` se puede proporcionar para definir los componentes que se utilizan para procesar fragmentos de contenido y a los que se debe aplicar el procesamiento en segundo plano.

* **Propiedades de**
referenciaSe puede configurar una lista de propiedades para especificar dónde se almacena la referencia al fragmento para el componente correspondiente.

>[!NOTE]
>
>No hay asignación directa entre propiedad y tipo de componente.
>
>AEM simplemente toma la primera propiedad que se puede encontrar en un párrafo. Por lo tanto, debe elegir las propiedades con cuidado.

![captura de pantalla_2019-03-18at100941](assets/screenshot_2019-03-18at100941.png)

Todavía hay algunas directrices que debe seguir para asegurarse de que el componente sea compatible con el procesamiento de fondo del fragmento de contenido:

* El nombre de la propiedad donde se definen los elementos que se van a procesar debe ser `element` o `elementNames`.

* El nombre de la propiedad donde se define la variación que se va a procesar debe ser `variation` o `variationName`.

* Si se admite la salida de varios elementos (utilizando `elementNames` para especificar varios elementos), el modo de visualización real se define con la propiedad `displayMode`:

   * Si el valor es `singleText` (y solo hay un elemento configurado), el elemento se representa como texto con contenido intermedio, compatibilidad con el diseño, etc. Este es el valor predeterminado de los fragmentos en los que solo se procesa un elemento.
   * De lo contrario, se utiliza un enfoque mucho más sencillo (podría llamarse &quot;vista de formulario&quot;), en el que no se admite contenido intermedio y el contenido del fragmento se representa &quot;tal cual&quot;.

* Si el fragmento se procesa para `displayMode` == `singleText` (implícita o explícitamente), entran en juego las siguientes propiedades adicionales:

   * `paragraphScope` define si se deben representar todos los párrafos, o solo un rango de párrafos (valores:  `all` vs.  `range`)

   * si `paragraphScope` == `range` entonces la propiedad `paragraphRange` define el rango de párrafos que se van a procesar

### Integración con otros Marcos {#integration-with-other-frameworks}

Los fragmentos de contenido se pueden integrar con:

* **Traducciones**

   Los fragmentos de contenido están totalmente integrados con el [AEM flujo de trabajo de traducción](/help/sites-administering/tc-manage.md). A nivel arquitectónico, esto significa:

   * Las traducciones individuales de un fragmento de contenido son en realidad fragmentos independientes; por ejemplo:

      * se encuentran bajo diferentes raíces lingüísticas:

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
   >    * Como los modelos de fragmento de contenido residen en `/conf`, no se incluyen en dichas traducciones. Puede [internacionalizar las cadenas de IU](/help/sites-developing/i18n-dev.md).
   >
   >    * Las plantillas se copian para crear el fragmento, por lo que está implícito.


* **Esquemas de metadatos**

   * Los fragmentos de contenido (re)utilizan los [esquemas de metadatos](/help/assets/metadata-schemas.md), que se pueden definir con recursos estándar.
   * CFM proporciona su propio esquema específico:

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      esto se puede ampliar si es necesario.

   * El formulario de esquema correspondiente se integra con el editor de fragmentos.

## La API de administración de fragmentos de contenido: del lado del servidor {#the-content-fragment-management-api-server-side}

Puede utilizar la API del lado del servidor para acceder a los fragmentos de contenido; consulte:

[com.adobe.cq.dam.cfm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/package-summary.html)

>[!CAUTION]
>
>Se recomienda utilizar la API del lado del servidor en lugar de acceder directamente a la estructura de contenido.

### Interfaces clave {#key-interfaces}

Las tres interfaces siguientes pueden servir como puntos de entrada:

* **Plantilla de fragmento**  ([plantilla de fragmento](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html))

   Utilice `FragmentTemplate.createFragment()` para crear un nuevo fragmento.

   ```
   Resource templateOrModelRsc = resourceResolver.getResource("...");
   FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
   ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
   ```

   Esta interfaz representa:

   * un modelo de fragmento de contenido o una plantilla de fragmento de contenido desde la que crear un fragmento de contenido,
   * y (tras la creación) la información estructural de dicho fragmento

   Esta información puede incluir:

   * Acceso a datos básicos (título, descripción)
   * Acceda a plantillas/modelos para los elementos del fragmento:

      * Plantillas de elementos de lista
      * Obtener información estructural de un elemento determinado
      * Acceder a la plantilla de elemento (consulte `ElementTemplate`)
   * Acceso a plantillas para las variaciones del fragmento:

      * Enumerar plantillas de variación
      * Obtener información estructural de una variación determinada
      * Acceso a la plantilla de variación (consulte `VariationTemplate`)
   * Obtener contenido inicial asociado

   Interfaces que representan información importante:

   * `ElementTemplate`

      * Obtener datos básicos (nombre, título)
      * Obtener contenido del elemento inicial
   * `VariationTemplate`

      * Obtener datos básicos (nombre, título, descripción)






* **Fragmento de contenido**  ([fragmento de contenido](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   Esta interfaz le permite trabajar con un fragmento de contenido de forma abstracta.

   >[!CAUTION]
   >
   >Se recomienda acceder a un fragmento a través de esta interfaz. Se debe evitar cambiar la estructura de contenido directamente.

   La interfaz le proporciona los medios para:

   * Administrar datos básicos (por ejemplo, obtener nombre; get/set title/description)
   * Acceso a metadatos
   * Acceder a elementos:

      * Elementos de lista
      * Obtener elementos por nombre
      * Crear nuevos elementos (consulte [Advertencias](#caveats))

      * Acceso a datos de elementos (consulte `ContentElement`)
   * Variaciones de lista definidas para el fragmento
   * Crear nuevas variaciones globalmente
   * Administrar contenido asociado:

      * Enumerar colecciones
      * Agregar colecciones
      * Eliminar colecciones
   * Acceso al modelo o la plantilla del fragmento

   Las interfaces que representan los elementos principales de un fragmento son:

   * **Elemento de contenido**  ([ContentElement](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Obtener datos básicos (nombre, título, descripción)
      * Obtener/Establecer contenido
      * Variaciones de acceso de un elemento:

         * Enumerar variaciones
         * Obtener variaciones por nombre
         * Crear nuevas variaciones (consulte [Advertencias](#caveats))
         * Eliminar variaciones (consulte [Advertencias](#caveats))
         * Acceso a los datos de variación (consulte `ContentVariation`)
      * Método abreviado para resolver variaciones (aplicar alguna lógica adicional de reserva específica de implementación si la variación especificada no está disponible para un elemento)
   * **Variación de contenido**  ([ContentVariation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Obtener datos básicos (nombre, título, descripción)
      * Obtener/Establecer contenido
      * Sincronización sencilla, basada en la información modificada por última vez

   Las tres interfaces ( `ContentFragment`, `ContentElement`, `ContentVariation`) amplían la interfaz `Versionable`, que agrega capacidades de versiones, necesarias para los fragmentos de contenido:

   * Crear una nueva versión del elemento
   * Enumerar versiones del elemento
   * Obtener el contenido de una versión específica del elemento con versiones







### Adaptación: Uso de adaptTo() {#adapting-using-adaptto}

Se puede adaptar lo siguiente:

* `ContentFragment` puede adaptarse a:

   * `Resource` - el recurso Sling subyacente; tenga en cuenta que actualizar el subyacente  `Resource` directamente requiere la reconstrucción del  `ContentFragment` objeto.

   * `Asset` - la  `Asset` abstracción DAM que representa el fragmento de contenido; tenga en cuenta que la actualización  `Asset` directa requiere la reconstrucción del  `ContentFragment` objeto.

* `ContentElement` puede adaptarse a:

   * `ElementTemplate` - para acceder a la información estructural del elemento.

* `FragmentTemplate` puede adaptarse a:

   * `Resource` - la  `Resource` determinación del modelo al que se hace referencia o de la plantilla original copiada;

      * los cambios realizados a través de `Resource` no se reflejan automáticamente en `FragmentTemplate`.

* `Resource` puede adaptarse a:

   * `ContentFragment`
   * `FragmentTemplate`

### Advertencias {#caveats}

Cabe señalar que:

* La API está implementada para proporcionar funciones compatibles con la interfaz de usuario de .
* Toda la API está diseñada para **no** mantener los cambios automáticamente (a menos que se indique lo contrario en el JavaDoc de la API). Por lo tanto, siempre tendrá que confirmar la resolución del recurso de la solicitud correspondiente (o la resolución que esté utilizando).
* Tareas que pueden requerir un esfuerzo adicional:

   * La creación/eliminación de nuevos elementos no actualizará la estructura de datos de fragmentos simples (basados en una plantilla de fragmento).
   * La creación de nuevas variaciones desde `ContentElement` no actualizará la estructura de datos (pero se creará globalmente a partir de `ContentFragment`).

   * La eliminación de variaciones existentes no actualizará la estructura de datos.

## La API de administración de fragmentos de contenido: del lado del cliente {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>Para AEM 6.5, la API del lado del cliente es interna.

### Información adicional {#additional-information}

Consulte lo siguiente:

* `filter.xml`

   El `filter.xml` para la administración de fragmentos de contenido está configurado de modo que no se superponga con el paquete de contenido principal de Assets.

## Editar sesiones {#edit-sessions}

Una sesión de edición se inicia cuando el usuario abre un fragmento de contenido en una de las páginas del editor. La sesión de edición finaliza cuando el usuario abandona el editor seleccionando **Save** o **Cancel**.

### Requisitos {#requirements}

Los requisitos para controlar una sesión de edición son:

* La edición de un fragmento de contenido, que puede abarcar varias vistas (= páginas HTML), debe ser atómica.
* La edición también debe ser *transaccional*; al final de la sesión de edición, los cambios deben confirmarse (guardarse) o revertirse (cancelarse).
* Los casos de Edge deben manejarse correctamente; entre estas situaciones se incluyen situaciones en las que el usuario abandona la página introduciendo una dirección URL manualmente o utilizando la navegación global.
* Debe estar disponible un guardado automático periódico (cada x minutos) para evitar la pérdida de datos.
* Si dos usuarios editan simultáneamente un fragmento de contenido, no deben sobrescribir los cambios de los demás.

#### Procesos {#processes}

Los procesos involucrados son:

* Inicio de una sesión

   * Se crea una nueva versión del fragmento de contenido.
   * Se ha iniciado el guardado automático.
   * Las cookies están configuradas; definen el fragmento editado actualmente y que hay una sesión de edición abierta.

* Finalización de una sesión

   * Se ha detenido el guardado automático.
   * Tras la confirmación:

      * Se actualiza la última información modificada.
      * Las cookies se eliminan.
   * Tras la reversión:

      * Se restaura la versión del fragmento de contenido que se creó cuando se inició la sesión de edición.
      * Las cookies se eliminan.


* Edición

   * Todos los cambios (guardado automático incluido) se realizan en el fragmento de contenido activo, no en un área separada y protegida.
   * Por lo tanto, esos cambios se reflejan inmediatamente en AEM páginas que hacen referencia al fragmento de contenido correspondiente

#### Acciones {#actions}

Las posibles acciones son:

* Introducción de una página

   * Compruebe si ya existe una sesión de edición; comprobando la cookie respectiva.

      * Si existe, compruebe que la sesión de edición se inició para el fragmento de contenido que se está editando actualmente

         * Si el fragmento actual, restablezca la sesión.
         * Si no es así, intente cancelar la edición del fragmento de contenido editado anteriormente y eliminar las cookies (sin sesión de edición posterior).
      * Si no existe ninguna sesión de edición, espere al primer cambio realizado por el usuario (consulte a continuación).
   * Compruebe si ya se hace referencia al fragmento de contenido en una página y muestre la información apropiada en caso afirmativo.



* Cambio de contenido

   * Siempre que el usuario cambia de contenido y no hay ninguna sesión de edición presente, se crea una nueva sesión de edición (consulte [Inicio de una sesión](#processes)).

* Dejar una página

   * Si hay una sesión de edición presente y los cambios no se han mantenido, se muestra un cuadro de diálogo de confirmación modal para notificar al usuario la posible pérdida de contenido y permitirle permanecer en la página.

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

El intervalo de guardado automático (medido en segundos) se puede definir mediante el administrador de configuración (ConfMgr):

* Nodo: `<*conf-root*>/settings/dam/cfm/jcr:content`
* Nombre de propiedad: `autoSaveInterval`
* Tipo: `Long`

* Predeterminado: `600` (10 minutos); esto se define en `/libs/settings/dam/cfm/jcr:content`

Si desea establecer un intervalo de guardado automático de 5 minutos, debe definir la propiedad en el nodo ; por ejemplo:

* Nodo: `/conf/global/settings/dam/cfm/jcr:content`
* Nombre de propiedad: `autoSaveInterval`

* Tipo: `Long`

* Valor: `300` (5 minutos equivale a 300 segundos)

## Plantillas de fragmento de contenido {#content-fragment-templates}

Consulte [Plantillas de fragmento de contenido](/help/sites-developing/content-fragment-templates.md) para obtener información completa.

## Componentes para la creación de páginas {#components-for-page-authoring}

Para obtener más información, consulte

* [Componentes principales: componente de fragmento de contenido](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)  (recomendado)
* [Componentes de fragmento de contenido: componentes para la creación de páginas](/help/sites-developing/components-content-fragments.md#components-for-page-authoring)
