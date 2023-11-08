---
title: AEM Uso de la fusión de recursos de Sling en la
seo-title: Using the Sling Resource Merger in AEM
description: La fusión de recursos de Sling proporciona servicios para acceder y combinar recursos
seo-description: The Sling Resource Merger provides services to access and merge resources
uuid: 0a28fdc9-caea-490b-8f07-7c4a6b802e09
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ec712ba0-0fd6-4bb8-93d6-07d09127df58
exl-id: 1eed754e-9a7d-4b65-a929-757fc962614d
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 1%

---

# AEM Uso de la fusión de recursos de Sling en la{#using-the-sling-resource-merger-in-aem}

## Función {#purpose}

La fusión de recursos de Sling proporciona servicios para acceder y combinar recursos. Proporciona mecanismos de diferencia (diferenciación) para:

* **[Superposiciones](/help/sites-developing/overlays.md)** de recursos mediante el [rutas de búsqueda configuradas](/help/sites-developing/overlays.md#configuring-the-search-paths).

* **Invalidaciones** de cuadros de diálogo de componentes para la IU táctil (`cq:dialog`), utilizando la jerarquía de tipos de recurso (mediante la propiedad ) `sling:resourceSuperType`).

Con la fusión de recursos de Sling, los recursos de superposición/anulación o las propiedades se combinan con los recursos/propiedades originales:

* El contenido de la definición personalizada tiene una prioridad mayor que la del original (es decir, *superposiciones* o *invalidaciones* it).

* Si es necesario, [propiedades](#properties) definida en la personalización, indique cómo se utilizará el contenido combinado del original.

>[!CAUTION]
>
>La fusión de recursos de Sling y los métodos relacionados solo se pueden usar con [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Esto también significa que solo es apropiado para la interfaz de usuario táctil estándar; en particular, las invalidaciones definidas de esta manera solo son aplicables al cuadro de diálogo táctil de un componente.
>
>Las superposiciones/anulaciones para otras áreas (incluidos otros aspectos de un componente táctil o de la IU clásica) implican copiar el nodo y la estructura adecuados del original al lugar donde se definirá la personalización.

### AEM Metas para la {#goals-for-aem}

AEM Los objetivos para utilizar la fusión de recursos de Sling en son los siguientes:

* asegúrese de que no se realizan cambios de personalización en `/libs`.
* reducir la estructura que se duplica desde `/libs`.

  Al utilizar la fusión de recursos de Sling, no se recomienda copiar toda la estructura de `/libs` ya que esto conllevaría que se almacenara demasiada información en la personalización (normalmente `/apps`). La duplicación de información aumenta innecesariamente las posibilidades de que se produzcan problemas cuando el sistema se actualiza de alguna manera.

>[!NOTE]
>
>Las anulaciones no dependen de las rutas de búsqueda, sino que utilizan la propiedad `sling:resourceSuperType` para establecer la conexión.
>
>Sin embargo, las invalidaciones suelen definirse en `/apps`AEM , como práctica recomendada en el uso de es definir personalizaciones en `/apps`; esto se debe a que no debe cambiar nada en `/libs`.

>[!CAUTION]
>
>Usted ***debe*** no cambie nada en el `/libs` ruta.
>
>Esto se debe al contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de funciones).
>
>El método recomendado para la configuración y otros cambios es:
>
>1. Vuelva a crear el elemento necesario (es decir, tal como existe en `/libs`) en `/apps`
>
>1. Realice cualquier cambio en `/apps`
>

### Propiedades {#properties}

La combinación de recursos proporciona las siguientes propiedades:

* `sling:hideProperties` ( `String` o `String[]`)

  Especifica la propiedad o lista de propiedades que se van a ocultar.

  El comodín `*` oculta todo.

* `sling:hideResource` ( `Boolean`)

  Indica si los recursos deben estar completamente ocultos, incluidos sus elementos secundarios.

* `sling:hideChildren` ( `String` o `String[]`)

  Contiene el nodo secundario o la lista de nodos secundarios que se van a ocultar. Se mantendrán las propiedades del nodo.

  El comodín `*` oculta todo.

* `sling:orderBefore` ( `String`)

  Contiene el nombre del nodo del mismo nivel en el que el nodo actual debe colocarse delante de.

Estas propiedades afectan a la forma en que los recursos/propiedades correspondientes/originales (de `/libs`) las utiliza la superposición/anulación (a menudo en `/apps`).

### Creación de la estructura {#creating-the-structure}

Para crear una superposición o sobrescritura, debe volver a crear el nodo original, con la estructura equivalente, debajo del destino (normalmente `/apps`). Por ejemplo:

* Superposición

   * La definición de la entrada de navegación para la consola Sitios, como se muestra en el carril, se define en:

     `/libs/cq/core/content/nav/sites/jcr:title`

   * Para superponer esto, cree el siguiente nodo:

     `/apps/cq/core/content/nav/sites`

     Luego actualice la propiedad `jcr:title` según sea necesario.

* Omitir

   * La definición del cuadro de diálogo táctil para la consola Textos se define en:

     `/libs/foundation/components/text/cq:dialog`

   * Para anular esto, cree el siguiente nodo, por ejemplo:

     `/apps/the-project/components/text/cq:dialog`

Para crear cualquiera de estos elementos, sólo es necesario volver a crear la estructura del esqueleto. Para simplificar la recreación de la estructura, todos los nodos intermedios pueden ser del tipo `nt:unstructured` (no tienen que reflejar el tipo de nodo original; por ejemplo, en `/libs`).

Por lo tanto, en el ejemplo de superposición anterior, se necesitan los siguientes nodos:

```shell
/apps
  /cq
    /core
      /content
        /nav
          /sites
```

>[!NOTE]
>
>Al utilizar la fusión de recursos de Sling (es decir, al trabajar con la interfaz de usuario táctil estándar), no se recomienda copiar toda la estructura de `/libs` ya que se almacenaría demasiada información en `/apps`. Esto puede causar problemas cuando el sistema se actualiza de alguna manera.

### Casos de uso {#use-cases}

Estas funciones, junto con las funciones estándar, permiten:

* **Añadir una propiedad**

  La propiedad no existe en `/libs` definición, pero es obligatorio en la `/apps` superposición/anulación.

   1. Cree el nodo correspondiente en `/apps`
   1. Crear la nueva propiedad en este nodo &quot;

* **Redefinir una propiedad (no propiedades creadas automáticamente)**

  La propiedad se define en `/libs`, pero se requiere un nuevo valor en la variable `/apps` superposición/anulación.

   1. Cree el nodo correspondiente en `/apps`
   1. Cree la propiedad correspondiente en este nodo (en / `apps`)

      * La propiedad tendrá una prioridad basada en la configuración de Sling Resource Resolver.
      * Se admite el cambio del tipo de propiedad.

        Si utiliza un tipo de propiedad diferente del utilizado en `/libs`, se utilizará el tipo de propiedad definido.

  >[!NOTE]
  >
  >Se admite el cambio del tipo de propiedad.

* **Redefinir una propiedad creada automáticamente**

  De forma predeterminada, las propiedades creadas automáticamente (como `jcr:primaryType`) no están sujetos a una superposición/anulación para garantizar que el tipo de nodo actualmente en `/libs` se respeta. Para imponer una superposición/anulación, debe volver a crear el nodo en `/apps`, oculte explícitamente la propiedad y redefina:

   1. Cree el nodo correspondiente en `/apps` con el deseado `jcr:primaryType`
   1. Creación de la propiedad `sling:hideProperties` en ese nodo, con el valor establecido en el de la propiedad creada automáticamente; por ejemplo, `jcr:primaryType`

      Esta propiedad, definida en `/apps`, ahora tendrá prioridad sobre la definida en `/libs`

* **Redefinición de un nodo y sus tareas secundarias**

  El nodo y sus tareas secundarias se definen en `/libs`, pero se requiere una nueva configuración en la `/apps` superposición/anulación.

   1. Combine las acciones de:

      1. Ocultar tareas secundarias de un nodo (conservando las propiedades del nodo)
      1. Redefinir la propiedad o las propiedades

* **Ocultar una propiedad**

  La propiedad se define en `/libs`, pero no es obligatorio en `/apps` superposición/anulación.

   1. Cree el nodo correspondiente en `/apps`
   1. Creación de una propiedad `sling:hideProperties` de tipo `String` o `String[]`. Utilice esta opción para especificar las propiedades que se ocultarán o ignorarán. También se pueden utilizar caracteres comodín. Por ejemplo:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **Ocultar un nodo y sus tareas secundarias**

  El nodo y sus tareas secundarias se definen en `/libs`, pero no es obligatorio en `/apps` superposición/anulación.

   1. Cree el nodo correspondiente en /apps
   1. Creación de una propiedad `sling:hideResource`

      * type: `Boolean`
      * value: `true`

* **Ocultar tareas secundarias de un nodo (conservando las propiedades del nodo)**

  El nodo, sus propiedades y sus tareas secundarias se definen en `/libs`. El nodo y sus propiedades son necesarios en la variable `/apps` superposición/anulación, pero algunos o todos los nodos secundarios no son obligatorios en la `/apps` superposición/anulación.

   1. Cree el nodo correspondiente en `/apps`
   1. Creación de la propiedad `sling:hideChildren`:

      * type: `String[]`
      * value: una lista de los nodos secundarios (como se define en `/libs`) para ocultar/omitir

      El comodín &amp;ast; se puede usar para ocultar o ignorar todos los nodos secundarios.

* **Reordenar nodos**

  El nodo y sus hermanos se definen en `/libs`. Se requiere una nueva posición para que el nodo se vuelva a crear en `/apps` superposición/anulación, donde la nueva posición se define en referencia al nodo del mismo nivel adecuado en `/libs`.

   * Utilice el `sling:orderBefore` propiedad:

      1. Cree el nodo correspondiente en `/apps`
      1. Creación de la propiedad `sling:orderBefore`:

         Esto especifica el nodo (como en `/libs`) que el nodo actual debe colocarse antes de:

         * type: `String`
         * value: `<before-SiblingName>`

### Invocar la fusión de recursos de Sling desde el código {#invoking-the-sling-resource-merger-from-your-code}

La fusión de recursos de Sling incluye dos proveedores de recursos personalizados: uno para superposiciones y otro para invalidaciones. Cada uno de ellos se puede invocar dentro del código utilizando un punto de montaje:

>[!NOTE]
>
>Al acceder al recurso, se recomienda utilizar el punto de montaje adecuado.
>
>Esto garantiza que se invoque la fusión de recursos de Sling y que se devuelva el recurso completamente combinado (reduciendo la estructura que debe replicarse desde ) `/libs`).

* Superposición:

   * objetivo: combinar recursos en función de su ruta de búsqueda
   * punto de montaje: `/mnt/overlay`
   * uso: `mount point + relative path`
   * ejemplo:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* Omitir:

   * objetivo: combinar recursos en función de su supertipo
   * punto de montaje: `/mnt/overide`
   * uso: `mount point + absolute path`
   * ejemplo:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### Ejemplo de uso {#example-of-usage}

Se tratan algunos ejemplos:

* Superposición:

   * [Personalización de las consolas](/help/sites-developing/customizing-consoles-touch.md)
   * [Personalización de la creación de páginas](/help/sites-developing/customizing-page-authoring-touch.md)

* Omitir:

   * [Configuración de las propiedades de página](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
