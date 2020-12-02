---
title: 'Plantillas de página: estáticas'
seo-title: 'Plantillas de página: estáticas'
description: Se utiliza una plantilla para crear una página y define qué componentes se pueden utilizar dentro del ámbito seleccionado
seo-description: Se utiliza una plantilla para crear una página y define qué componentes se pueden utilizar dentro del ámbito seleccionado
uuid: 7a473c19-9565-476e-9e54-ab179da04d71
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cfd90e8f-9b9b-4d0b-be31-828469b961de
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 6%

---


# Plantillas de página: estáticas{#page-templates-static}

Se utiliza una plantilla para crear una página y define qué componentes se pueden utilizar dentro del ámbito seleccionado. Una plantilla es una jerarquía de nodos que tiene la misma estructura que la página que se va a crear, pero sin ningún contenido real.

Cada plantilla le presentará una selección de componentes disponibles para su uso.

* Las plantillas están compuestas de [Componentes](/help/sites-developing/components.md);
* Los componentes utilizan y permiten el acceso a los widgets y se utilizan para representar el contenido.

>[!NOTE]
>
>[También hay disponibles ](/help/sites-developing/page-templates-editable.md) plantillas editables, que son el tipo recomendado de plantillas para la mayor flexibilidad y las funciones más recientes.

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
   <td> allowChildren </td>
   <td> Cadena[]</td>
   <td>Ruta de una plantilla que puede ser secundaria de esta plantilla.<br /> </td>
  </tr>
  <tr>
   <td> allowParents</td>
   <td> Cadena[]</td>
   <td>Ruta de una plantilla que puede ser una plantilla principal de esta plantilla.<br /> </td>
  </tr>
  <tr>
   <td> allowPaths</td>
   <td> Cadena[]</td>
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
   <td>Clasificación de la plantilla. Se utiliza para mostrar la plantilla en la interfaz de usuario.<br /> </td>
  </tr>
  <tr>
   <td> jcr:content</td>
   <td> cq:PageContent</td>
   <td>Nodo que contiene el contenido de la plantilla.<br /> </td>
  </tr>
  <tr>
   <td> thumbnail.png</td>
   <td> nt:file</td>
   <td>Miniatura de la plantilla.<br /> </td>
  </tr>
  <tr>
   <td> icon.png</td>
   <td> nt:file</td>
   <td>Icono de la plantilla.<br /> </td>
  </tr>
 </tbody>
</table>

Una plantilla es la base de una página.

Para crear una página, la plantilla debe copiarse (node-tree `/apps/<myapp>/template/<mytemplate>`) en la posición correspondiente en el árbol del sitio: esto es lo que sucede si se crea una página con la ficha **Sitios web**.

Esta acción de copia también proporciona a la página su contenido inicial (generalmente solo contenido de nivel superior) y la propiedad sling:resourceType, la ruta al componente de página que se utiliza para representar la página (todo en el nodo secundario jcr:content).

## Cómo se estructuran las plantillas {#how-templates-are-structured}

Hay dos aspectos que deben considerarse:

* la estructura de la plantilla misma
* la estructura del contenido producido al utilizar una plantilla

### La estructura de una plantilla {#the-structure-of-a-template}

Se crea una plantilla bajo un nodo de tipo **cq:Template**.

![screen_shot_2012-02-13at63646pm](assets/screen_shot_2012-02-13at63646pm.png)

Se pueden definir varias propiedades, en particular:

* **jcr:title** - título de la plantilla; aparece en el cuadro de diálogo al crear una página.
* **jcr:description** - descripción de la plantilla; aparece en el cuadro de diálogo al crear una página.

Este nodo contiene un nodo jcr:content (cq:PageContent) que se utilizará como base para el nodo de contenido de las páginas resultantes; esto hace referencia, mediante sling:resourceType, al componente que se utilizará para procesar el contenido real de una página nueva.

![screen_shot_2012-02-13at64010pm](assets/screen_shot_2012-02-13at64010pm.png)

Este componente se utiliza para definir la estructura y el diseño del contenido cuando se crea una página nueva.

![screen_shot_2012-02-13at64137pm](assets/screen_shot_2012-02-13at64137pm.png)

### El contenido producido por una plantilla {#the-content-produced-by-a-template}

Las plantillas se utilizan para crear páginas de tipo `cq:Page` (como se mencionó anteriormente, una página es un tipo especial de componente). Cada página AEM tiene un nodo estructurado `jcr:content`. Así pues:

* es del tipo cq:PageContent
* es un tipo de nodo estructurado que contiene una definición de contenido definida
* tiene una propiedad `sling:resourceType` para hacer referencia al componente que contiene las secuencias de comandos de sling utilizadas para procesar el contenido

### Plantillas predeterminadas {#default-templates}

AEM incluye una serie de plantillas predeterminadas disponibles de forma predeterminada. En algunos casos, es posible que desee utilizar las plantillas tal cual. En ese caso, debe asegurarse de que la plantilla está disponible para su sitio Web.

Por ejemplo, AEM incluye varias plantillas, incluidas una página de contenido y una página de inicio.

| **Título** | **Componente** | **Ubicación** | **Función** |
|---|---|---|---|
| Página principal | homepage | geometrixx | La plantilla de la página principal de Geometrixx. |
| Página de contenido | contentpage | geometrixx | La plantilla de la página de contenido de Geometrixx. |

#### Visualización de plantillas predeterminadas {#displaying-default-templates}

Para ver una lista de todas las plantillas en el repositorio, siga este procedimiento:

1. En CRXDE Lite, abra el menú **Herramientas** y haga clic en **Consulta**.

1. En la ficha Consulta
1. Como **Tipo**, seleccione **XPath**.

1. En el campo de entrada **Consulta**, escriba la cadena siguiente:
//element(*, cq:Template)

1. Haga clic en **Ejecutar**. Se muestra la lista en el cuadro de resultados.

En la mayoría de los casos, tomará una plantilla existente y desarrollará una nueva para su propio uso. Consulte [Desarrollo de plantillas de página](#developing-page-templates) para obtener más información.

Para habilitar una plantilla existente para el sitio Web y desea que se muestre en el cuadro de diálogo **Crear página** al crear una página directamente en **Sitios Web** desde la consola **Sitios Web**, establezca la propiedad permissionPaths del nodo de plantilla en: **/content(/.*)?**

## Cómo se aplican los diseños de plantilla {#how-template-designs-are-applied}

Cuando los estilos se definen en la interfaz de usuario mediante [modo de diseño](/help/sites-authoring/default-components-designmode.md), el diseño se mantiene en la ruta exacta del nodo de contenido para el que se está definiendo el estilo.

>[!CAUTION]
>
>Adobe solo recomienda aplicar diseños mediante [modo de diseño](/help/sites-authoring/default-components-designmode.md).
>
>La modificación de diseños en CRX DE, por ejemplo, no es recomendable y la aplicación de dichos diseños puede diferir del comportamiento esperado.

Si los diseños solo se aplican mediante el modo Diseño, no se aplican las siguientes secciones: [Resolución de ruta de diseño](/help/sites-developing/page-templates-static.md#design-path-resolution), [Árbol de decisiones](/help/sites-developing/page-templates-static.md#decision-tree) y [Ejemplo](/help/sites-developing/page-templates-static.md#example).

### Resolución de ruta de diseño {#design-path-resolution}

Al procesar contenido basado en una plantilla estática, AEM intentará aplicar el diseño y los estilos más relevantes al contenido en función de una transversal de la jerarquía de contenido.

AEM determina el estilo más relevante para un nodo de contenido en el siguiente orden:

* Si hay un diseño para la ruta completa y exacta del nodo de contenido (como cuando el diseño se define en el modo de diseño), utilice ese diseño.
* Si hay un diseño para el nodo de contenido del elemento principal, utilice dicho diseño.
* Si hay un diseño para cualquier nodo en la ruta del nodo de contenido, utilice ese diseño.

En los dos últimos casos, si hay más de un diseño aplicable, utilice el más cercano al nodo de contenido.

### Árbol de decisiones {#decision-tree}

Es una representación gráfica de la lógica [Resolución de ruta de diseño](/help/sites-developing/page-templates-static.md#design-path-resolution).

![design_path_resolution](assets/design_path_resolution.png)

### Ejemplo {#example}

Considere una estructura de contenido simple como se indica a continuación, donde un diseño podría aplicarse a cualquiera de los nodos:

`/root/branch/leaf`

En la tabla siguiente se describe cómo AEM un diseño.

<table>
 <tbody>
  <tr>
   <td><strong>Búsqueda De Diseño Para<br /> </strong></td>
   <td><strong>Existen diseños para<br /> </strong></td>
   <td><strong>Diseño seleccionado<br /> </strong></td>
   <td><strong>Comentario</strong></td>
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
   <td>Volvamos a la coincidencia más cercana en la parte inferior del árbol.</td>
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
   <td><p>Si no hay una coincidencia exacta, tome la una parte inferior del árbol.</p> <p>Se supone que esto siempre será aplicable, pero más arriba el árbol puede ser demasiado específico.<br /> </p> </td>
  </tr>
 </tbody>
</table>

## Desarrollo de plantillas de página {#developing-page-templates}

AEM plantillas de página son simplemente modelos utilizados para crear nuevas páginas. Pueden contener tan poco o tanto contenido inicial como sea necesario y su función consiste en crear las estructuras de nodos iniciales correctas, con las propiedades necesarias (principalmente sling:resourceType) definidas para permitir la edición y el procesamiento.

### Creación de una nueva plantilla (basada en una plantilla existente) {#creating-a-new-template-based-on-an-existing-template}

Huelga decir que una nueva plantilla se puede crear completamente desde cero, pero a menudo se copiará y actualizará una plantilla existente para ahorrarle tiempo y esfuerzo. Por ejemplo, las plantillas de Geometrixx se pueden utilizar para empezar.

Para crear una nueva plantilla basada en una plantilla existente:

1. Copie una plantilla existente (preferiblemente con una definición lo más cercana posible a lo que desea lograr) en un nuevo nodo.

   Las plantillas generalmente se almacenan en **/apps/&lt;nombre-sitio_web>/templates/&lt;nombre-plantilla>**.

   >[!NOTE]
   >
   >La lista de las plantillas disponibles depende de la ubicación de la nueva página y de las restricciones de colocación especificadas en cada plantilla. Consulte [Disponibilidad de la plantilla](#templateavailibility).

1. Cambie el **jcr:title** del nuevo nodo de plantilla para reflejar su nueva función. También puede actualizar **jcr:description** si corresponde. Asegúrese de cambiar la disponibilidad de la plantilla de la página según corresponda.

   >[!NOTE]
   >
   >Si desea que la plantilla se muestre en el cuadro de diálogo **Crear página** al crear una página directamente en **Sitios web** desde la consola **Sitios web**, establezca la propiedad `allowedPaths` del nodo de plantilla en: `/content(/.*)?`

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Copie el componente en el que se basa la plantilla (esto se indica con la propiedad **sling:resourceType** del nodo **jcr:content** de la plantilla) para crear una nueva instancia.

   Los componentes se almacenan generalmente en **/apps/&lt;nombre-sitio_web>/components/&lt;nombre-componente>**.

1. Actualice los **jcr:title** y **jcr:description** del nuevo componente.
1. Reemplace thumbnail.png si desea que se muestre una nueva imagen en miniatura en la lista de selección de plantillas (tamaño 128 x 98 px).
1. Actualice el **sling:resourceType** del nodo **jcr:content** de la plantilla para hacer referencia al nuevo componente.
1. Realice cualquier otro cambio en la funcionalidad o el diseño de la plantilla o su componente subyacente.

   >[!NOTE]
   >
   >Los cambios realizados en el nodo **/apps/&lt;website>/templates/&lt;template-name>** afectarán a la instancia de plantilla (como en la lista de selección).
   Los cambios realizados en el nodo **/apps/&lt;sitio Web>/components/&lt;nombre-componente>** afectarán a la página de contenido creada al utilizar la plantilla.

   Ahora puede crear una página dentro del sitio web con la nueva plantilla.

>[!NOTE]
La biblioteca de cliente del editor asume la presencia de la Área de nombres `cq.shared` en las páginas de contenido y, si no se encuentra, se producirá el error de JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined`.
Todas las páginas de contenido de muestra contienen `cq.shared`, por lo que cualquier contenido basado en ellas incluye automáticamente `cq.shared`. Sin embargo, si decide crear sus propias páginas de contenido desde cero sin basarlas en contenido de muestra, debe asegurarse de incluir la Área de nombres `cq.shared`.
Consulte [Uso de bibliotecas del lado del cliente](/help/sites-developing/clientlibs.md) para obtener más información.

## Disponibilidad de una plantilla existente {#making-an-existing-template-available}

Este ejemplo ilustra cómo permitir que se utilice una plantilla para determinadas rutas de contenido. Las plantillas que están disponibles para el autor de la página al crear nuevas páginas están determinadas por la lógica definida en [Disponibilidad de plantilla](/help/sites-developing/templates.md#template-availability).

1. En CRXDE Lite, vaya a la plantilla que desee utilizar para la página, por ejemplo, la plantilla Newsletter.
1. Cambie la propiedad `allowedPaths` y otras propiedades utilizadas para [disponibilidad de la plantilla](/help/sites-developing/templates.md#template-availability). Por ejemplo, `allowedPaths`: `/content/geometrixx-outdoors/[^/]+(/.*)?` significa que esta plantilla está permitida en cualquier ruta bajo `/content/geometrixx-outdoors`.

   ![chlimage_1-89](assets/chlimage_1-89.png)
