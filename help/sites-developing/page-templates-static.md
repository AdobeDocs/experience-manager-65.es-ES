---
title: 'Plantillas de página: estáticas'
description: Se utiliza una plantilla para crear una página y define qué componentes se pueden utilizar dentro del ámbito seleccionado
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: b934ac41-78b9-497f-ba95-b05ef1e5660e
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 1%

---

# Plantillas de página: estáticas{#page-templates-static}

Se utiliza una plantilla para crear una página y define qué componentes se pueden utilizar dentro del ámbito seleccionado. Una plantilla es una jerarquía de nodos que tiene la misma estructura que la página que se va a crear, pero sin contenido real.

Cada plantilla le presenta una selección de componentes disponibles para su uso.

* Las plantillas están compuestas por [Componentes](/help/sites-developing/components.md);
* Los componentes utilizan los widgets y permiten el acceso a ellos, y se utilizan para procesar el contenido.

>[!NOTE]
>
>[Las plantillas editables](/help/sites-developing/page-templates-editable.md) también están disponibles y son el tipo de plantillas recomendado para obtener la mayor flexibilidad y las características más recientes.

## Propiedades y nodos secundarios de una plantilla {#properties-and-child-nodes-of-a-template}

Una plantilla es un nodo de tipo cq:Template y tiene las siguientes propiedades y nodos secundarios:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre <br /> </strong></td>
   <td><strong>Tipo <br /> </strong></td>
   <td><strong>Descripción <br /> </strong></td>
  </tr>
  <tr>
   <td>. <br /> </td>
   <td> cq:Template</td>
   <td>Plantilla actual. Una plantilla es del tipo de nodo cq:Template.<br /> </td>
  </tr>
  <tr>
   <td> allowedChildren </td>
   <td> String[]</td>
   <td>Ruta de una plantilla que puede ser secundaria de esta plantilla.<br /> </td>
  </tr>
  <tr>
   <td> allowedParents</td>
   <td> String[]</td>
   <td>Ruta de una plantilla que puede ser una plantilla principal de esta plantilla.<br /> </td>
  </tr>
  <tr>
   <td> allowedPaths</td>
   <td> String[]</td>
   <td>Ruta de una página que puede basarse en esta plantilla.<br /> </td>
  </tr>
  <tr>
   <td> jcr:created</td>
   <td> Fecha</td>
   <td>Fecha de creación de la plantilla.<br /> </td>
  </tr>
  <tr>
   <td> jcr:description</td>
   <td> Cadena</td>
   <td>Descripción de la plantilla.<br /> </td>
  </tr>
  <tr>
   <td> jcr:title</td>
   <td> Cadena</td>
   <td>Título de la plantilla.<br /> </td>
  </tr>
  <tr>
   <td> clasificación</td>
   <td> Largo</td>
   <td>Clasificación de la plantilla. Se usa para mostrar la plantilla en la interfaz de usuario.<br /> </td>
  </tr>
  <tr>
   <td> jcr:contenido</td>
   <td> cq:PageContent</td>
   <td>Nodo que contiene el contenido de la plantilla.<br /> </td>
  </tr>
  <tr>
   <td> thumbnail.png</td>
   <td> nt:archivo</td>
   <td>Miniatura de la plantilla.<br /> </td>
  </tr>
  <tr>
   <td> icon.png</td>
   <td> nt:archivo</td>
   <td>Icono de la plantilla.<br /> </td>
  </tr>
 </tbody>
</table>

Una plantilla es la base de una página.

Para crear una página, la plantilla debe copiarse (árbol de nodos `/apps/<myapp>/template/<mytemplate>`) a la posición correspondiente en el árbol del sitio: esto es lo que sucede si se crea una página con la pestaña **Sitios web**.

Esta acción de copia también proporciona a la página su contenido inicial (normalmente solo contenido de nivel superior) y la propiedad sling:resourceType, la ruta al componente de página que se utiliza para procesar la página (todo en el nodo secundario jcr:content).

## Estructura de las plantillas {#how-templates-are-structured}

Hay dos aspectos que hay que tener en cuenta:

* la estructura de la propia plantilla
* la estructura del contenido producido cuando se utiliza una plantilla

### La estructura de una plantilla {#the-structure-of-a-template}

Se crea una plantilla en un nodo de tipo **cq:Template**.

![screen_shot_2012-02-13at63646pm](assets/screen_shot_2012-02-13at63646pm.png)

Se pueden configurar varias propiedades, en particular:

* **jcr:title** - título de la plantilla; aparece en el cuadro de diálogo al crear una página.
* **jcr:description**: descripción de la plantilla; aparece en el cuadro de diálogo al crear una página.

Este nodo contiene un nodo jcr:content (cq:PageContent) que se utiliza como base para el nodo de contenido de las páginas resultantes; esto hace referencia, mediante sling:resourceType, al componente que se va a utilizar para procesar el contenido real de una nueva página.

![screen_shot_2012-02-13at64010pm](assets/screen_shot_2012-02-13at64010pm.png)

Este componente se utiliza para definir la estructura y el diseño del contenido cuando se crea una nueva página.

![screen_shot_2012-02-13at64137pm](assets/screen_shot_2012-02-13at64137pm.png)

### El contenido producido por una plantilla {#the-content-produced-by-a-template}

Las plantillas se utilizan para crear páginas de tipo `cq:Page` (como se mencionó anteriormente, una página es un tipo especial de componente). AEM Cada página de la tiene un nodo estructurado `jcr:content`. Así pues:

* es de tipo cq:PageContent
* es un tipo de nodo estructurado que contiene una definición de contenido definida
* tiene una propiedad `sling:resourceType` para hacer referencia al componente que contiene los scripts de sling utilizados para procesar el contenido

### Plantillas predeterminadas {#default-templates}

AEM El paquete incluye varias plantillas predeterminadas disponibles de forma predeterminada. A veces, es posible que desee utilizar las plantillas tal cual. En ese caso, debe asegurarse de que la plantilla esté disponible para el sitio web.

AEM Por ejemplo, la viene con varias plantillas, incluidas una página de contenido y una página de inicio.

| **Título** | **Componente** | **Ubicación** | **Propósito** |
|---|---|---|---|
| Página principal | homepage | geometrixx | Plantilla de la página de inicio de la Geometrixx. |
| Página de contenido | contentpage | geometrixx | Plantilla de la página de contenido Geometrixx. |

#### Visualización de plantillas predeterminadas {#displaying-default-templates}

Para ver una lista de todas las plantillas del repositorio, siga este procedimiento:

1. En el CRXDE Lite, abra el menú **Herramientas** y haga clic en **Consulta**.

1. En la pestaña Consulta
1. Como **Tipo**, seleccione **XPath**.

1. En el campo de entrada **Consulta**, escriba la siguiente cadena:
//element(&#42;, cq:Template)

1. Haga clic en **Ejecutar**. La lista se muestra en el cuadro de resultados.

Normalmente, se toma una plantilla existente y se desarrolla una nueva para uso propio. Consulte [Desarrollo de plantillas de página](#developing-page-templates) para obtener más información.

Para habilitar una plantilla existente para su sitio web y desea que se muestre en el cuadro de diálogo **Crear página** al crear una página directamente debajo de **Sitios web** desde la consola **Sitios web**, establezca la propiedad allowedPaths del nodo de la plantilla en: **/content(/.&#42;)?**

## Aplicación de los diseños de plantilla {#how-template-designs-are-applied}

Cuando los estilos se definen en la interfaz de usuario con [Modo de diseño](/help/sites-authoring/default-components-designmode.md), el diseño se mantiene en la ruta exacta del nodo de contenido para el que se define el estilo.

>[!CAUTION]
>
>El Adobe recomienda aplicar únicamente diseños mediante [Modo de diseño](/help/sites-authoring/default-components-designmode.md).
>
>La modificación de diseños en CRXDE Lite, por ejemplo, no es una práctica recomendada y la aplicación de dichos diseños puede variar del comportamiento esperado.

Si los diseños solo se aplican mediante el modo de diseño, las siguientes secciones, [Resolución de la ruta de diseño](/help/sites-developing/page-templates-static.md#design-path-resolution), [Árbol de decisiones](/help/sites-developing/page-templates-static.md#decision-tree) y el [Ejemplo](/help/sites-developing/page-templates-static.md#example) no son aplicables.

### Resolución de ruta de diseño {#design-path-resolution}

AEM Al procesar contenido basado en una plantilla estática, intenta aplicar los estilos y el diseño más relevantes al contenido en función de un recorrido de la jerarquía de contenido.

AEM determina el estilo más relevante para un nodo de contenido en el siguiente orden:

* Si hay un diseño para la ruta completa y exacta del nodo de contenido (como cuando el diseño se define en el modo Diseño), utilice ese diseño.
* Si hay un diseño para el nodo de contenido del elemento principal, utilice ese diseño.
* Si hay un diseño para cualquier nodo en la ruta del nodo de contenido, utilice ese diseño.

En los dos últimos casos, si hay más de un diseño aplicable, utilice el más cercano al nodo de contenido.

### Árbol de decisión {#decision-tree}

Esta es una representación gráfica de la lógica [Resolución de ruta de diseño](/help/sites-developing/page-templates-static.md#design-path-resolution).

![design_path_resolution](assets/design_path_resolution.png)

### Ejemplos {#example}

Considere una estructura de contenido simple como se muestra a continuación, donde un diseño podría aplicarse a cualquiera de los nodos:

`/root/branch/leaf`

AEM En la tabla siguiente se describe cómo elige el diseño el usuario.

<table>
 <tbody>
  <tr>
   <td><strong>Búsqueda De Diseño Para<br /> </strong></td>
   <td><strong>Hay Diseños Para<br /> </strong></td>
   <td><strong>Diseño elegido<br /> </strong></td>
   <td><strong>Comentar</strong></td>
  </tr>
  <tr>
   <td><code class="code">leaf
      </code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> <p><code>leaf</code></p> </td>
   <td><code>leaf</code></td>
   <td>La coincidencia más exacta siempre se toma.<br /> </td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> </td>
   <td><code>branch</code></td>
   <td>Vuelva a la coincidencia más cercana más abajo en el árbol.</td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><code>root</code></td>
   <td><code>root</code></td>
   <td>Si todo lo demás falla, tome lo que queda.<br /> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><code>branch</code></td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>branch</code></p> <p><code class="code">leaf
       </code></p> </td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>root</code></p> <p><code class="code">branch
       </code></p> </td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>root</code></p> <p><code class="code">leaf
       </code></p> </td>
   <td><code>root</code></td>
   <td><p>Si no hay una coincidencia exacta, tome la que esté más abajo en el árbol.</p> <p>Se supone que esto siempre será aplicable, pero más arriba en el árbol puede ser demasiado específico.<br /> </p> </td>
  </tr>
 </tbody>
</table>

## Desarrollo de plantillas de página {#developing-page-templates}

AEM Las plantillas de página de son simplemente modelos utilizados para crear páginas. Pueden contener tan poco contenido inicial como sea necesario, y su función es crear las estructuras de nodos iniciales correctas, con las propiedades necesarias (principalmente sling:resourceType) configuradas para permitir la edición y el procesamiento.

### Creación de una plantilla (basada en una plantilla existente) {#creating-a-new-template-based-on-an-existing-template}

Se puede crear una plantilla nueva completamente desde cero, pero a menudo se copia una plantilla existente y se actualiza para ahorrarle tiempo y esfuerzo. Por ejemplo, las plantillas dentro de Geometrixx se pueden utilizar para ayudarle a empezar.

Para crear una plantilla basada en una plantilla existente:

1. Copie una plantilla existente (preferiblemente con una definición lo más cercana posible a lo que desea lograr) en un nuevo nodo.

   Las plantillas se almacenan en **/apps/&lt;website-name>/templates/&lt;template-name>**.

   >[!NOTE]
   >
   >La lista de plantillas disponibles depende de la ubicación de la nueva página y de las restricciones de colocación especificadas en cada plantilla. Ver [Disponibilidad de plantillas](#templateavailibility).

1. Cambie **jcr:title** del nuevo nodo de plantilla para reflejar su nuevo rol. También puede actualizar **jcr:description** si corresponde. Asegúrese de cambiar la disponibilidad de la plantilla de la página según corresponda.

   >[!NOTE]
   >
   >Si desea que la plantilla se muestre en el cuadro de diálogo **Crear página** al crear una página directamente en **Sitios web** desde la consola **Sitios web**, establezca la propiedad `allowedPaths` del nodo de la plantilla en: `/content(/.*)?`

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Copie el componente en el que se basa la plantilla (así lo indica la propiedad **sling:resourceType** del nodo **jcr:content** dentro de la plantilla) para crear una instancia.

   Los componentes se almacenan en **/apps/&lt;website-name>/components/&lt;component-name>**.

1. Actualice **jcr:title** y **jcr:description** del nuevo componente.
1. Reemplace thumbnail.png si desea que se muestre una nueva imagen en miniatura en la lista de selección de plantillas (tamaño 128 x 98 px).
1. Actualice **sling:resourceType** del nodo **jcr:content** de la plantilla para hacer referencia al nuevo componente.
1. Realice cambios adicionales en la funcionalidad o el diseño de la plantilla, en su componente subyacente o en ambos.

   >[!NOTE]
   >
   >Los cambios realizados en el nodo **/apps/&lt;website>/templates/&lt;template-name>** afectan a la instancia de la plantilla (como en la lista de selección).
   >
   >
   >Los cambios realizados en el nodo **/apps/&lt;website>/components/&lt;component-name>** afectan a la página de contenido creada cuando se utiliza la plantilla.

   Ahora puede crear una página dentro del sitio web con la nueva plantilla.

>[!NOTE]
>
>La biblioteca de cliente del editor supone la presencia del área de nombres `cq.shared` en las páginas de contenido y, si está ausente, los resultados del error de JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined`.
>
>Todas las páginas de contenido de muestra contienen `cq.shared`, por lo que cualquier contenido basado en ellas incluye automáticamente `cq.shared`. Sin embargo, si decide crear sus propias páginas de contenido desde cero sin basarlas en contenido de ejemplo, debe asegurarse de incluir el área de nombres `cq.shared`.
>
>Consulte [Uso de bibliotecas del lado del cliente](/help/sites-developing/clientlibs.md) para obtener más información.

## Disponibilidad de una plantilla existente {#making-an-existing-template-available}

Este ejemplo ilustra cómo permitir que se utilice una plantilla para determinadas rutas de contenido. Las plantillas disponibles para el autor de la página al crear páginas están determinadas por la lógica definida en [Disponibilidad de plantillas](/help/sites-developing/templates.md#template-availability).

1. En CRXDE Lite, vaya a la plantilla que desee utilizar para la página, por ejemplo, la plantilla Newsletter.
1. Cambie la propiedad `allowedPaths` y otras propiedades utilizadas para [disponibilidad de la plantilla](/help/sites-developing/templates.md#template-availability). Por ejemplo, `allowedPaths`: `/content/geometrixx-outdoors/[^/]+(/.*)?` significa que esta plantilla está permitida en cualquier ruta de acceso bajo `/content/geometrixx-outdoors`.

   ![chlimage_1-89](assets/chlimage_1-89.png)
