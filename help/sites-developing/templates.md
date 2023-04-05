---
title: Plantillas
description: Las plantillas se utilizan al crear una página que se utiliza como base para la nueva página.
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
source-git-commit: 95638b6dd9527c567b38d8cd9da14633bd4142b5
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 1%

---

# Plantillas{#templates}

Las plantillas se utilizan en varios puntos de AEM:

* [Al crear una página, se selecciona una plantilla](#templates-pages). Esta plantilla se utiliza como base para la nueva página. La plantilla define la estructura de la página, cualquier contenido inicial y el [componentes](/help/sites-authoring/default-components.md) que se puede utilizar (propiedades de diseño).

* [Al crear un fragmento de contenido, también se selecciona una plantilla](#templates-content-fragments). Esta plantilla define la estructura, los elementos iniciales y las variaciones.

Las siguientes plantillas se tratan en detalle:

* [Plantillas de página: editables](/help/sites-developing/page-templates-editable.md)
* [Plantillas de página: estáticas](/help/sites-developing/page-templates-static.md)
* [Plantillas de fragmento de contenido](/help/sites-developing/content-fragment-templates.md)
* [Representación de plantilla adaptable](/help/sites-developing/templates-adaptive-rendering.md)

## Plantillas - Páginas {#templates-pages}

AEM ahora ofrece dos tipos básicos de plantillas para la creación de páginas:

>[!NOTE]
>
>Al utilizar una plantilla para [crear una página](/help/sites-authoring/managing-pages.md#creating-a-new-page), no hay diferencia visible (para el autor de la página) ni indicación del tipo de plantilla que se está utilizando.

### Plantillas editables {#editable-templates}

Las plantillas editables ahora se consideran prácticas recomendadas para el desarrollo con AEM.

Las ventajas de las plantillas editables:

* Puede [created](/help/sites-authoring/templates.md#creating-a-new-template-template-author) y [editado](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) por sus autores.

* Se han introducido para permitirle definir lo siguiente para cualquier página creada con la plantilla:

   * la estructura
   * el contenido inicial
   * políticas de contenido

* Una vez creada la nueva página, se mantiene una conexión dinámica entre la página y la plantilla. Esta conexión significa que los cambios en la estructura de la plantilla se reflejan en cualquier página creada con esa plantilla; los cambios en el contenido inicial no se reflejan.
* Utiliza políticas de contenido (editadas desde el editor de plantillas) para mantener las propiedades de diseño (no utiliza el modo Diseño dentro del editor de páginas).
* Se almacenan en `/conf`
* Consulte [Plantillas editables](/help/sites-developing/page-templates-editable.md) para obtener más información.

>[!NOTE]
>
>Consulte [Uso de plantillas de página editables para desarrollar un sitio de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/template-editor-feature-video-use.html?lang=en).

### Plantillas estáticas {#static-templates}

Plantillas estáticas:

* Los desarrolladores deben definirlo y configurarlo.
* El sistema de creación de plantillas original de AEM que ha estado disponible para muchas versiones.
* Una plantilla estática es una jerarquía de nodos que tiene la misma estructura que la página que se va a crear, pero sin contenido real.
* Se copian para crear la página; después no existe ninguna conexión dinámica.
* Usos [Modo de diseño](/help/sites-authoring/default-components-designmode.md) para mantener las propiedades de diseño.
* Se almacenan en `/apps`
* Consulte [Plantillas estáticas](/help/sites-developing/page-templates-static.md) para obtener más información.

>[!NOTE]
>
>A partir de AEM 6.5, el uso de plantillas estáticas no se considera una práctica recomendada. En su lugar, utilice plantillas editables.
>
>[Modernización AEM](modernization-tools.md) las herramientas pueden ayudarle a migrar de plantillas estáticas a plantillas editables.

### Disponibilidad de la plantilla {#template-availability}

>[!CAUTION]
>
>AEM ofrece varias propiedades para controlar las plantillas permitidas en **Sitios**. Sin embargo, combinarlas puede llevar a reglas complejas que son difíciles de rastrear y administrar.
>
>Por lo tanto, Adobe recomienda que comience con sencillez, definiendo:
>
>* solo la variable `cq:allowedTemplates` property
>
>* solo en la raíz del sitio
>
>Para ver un ejemplo, consulte We.Retail: `/content/we-retail/jcr:content`
>
>Las propiedades `allowedPaths`, `allowedParents`y `allowedChildren` también se puede colocar en las plantillas para definir reglas más sofisticadas. Sin embargo, cuando es posible, es *many* más sencillo de definir `cq:allowedTemplates` propiedades en subsecciones del sitio si es necesario restringir aún más las plantillas permitidas.
>
>La ventaja adicional es que la variable `cq:allowedTemplates` un autor puede actualizar las propiedades en la variable **Avanzadas** de la pestaña **Propiedades de página**. Las demás propiedades de la plantilla no se pueden actualizar mediante la interfaz de usuario (estándar), por lo que sería necesario que un desarrollador mantuviera las reglas y una implementación de código para cada cambio.

Al crear una página en la interfaz de administración del sitio, la lista de plantillas disponibles depende de la ubicación de la nueva página y las restricciones de colocación especificadas en cada plantilla.

Las siguientes propiedades determinan si una plantilla `T` se utiliza para que una nueva página se coloque como un elemento secundario de la página `P`. Cada una de estas propiedades es una cadena de varios valores que contiene cero o más expresiones regulares que se utilizan para hacer coincidir con rutas:

* La variable `cq:allowedTemplates` propiedad de la variable `jcr:content` subnodo de `P` o un antecesor de `P`.

* La variable `allowedPaths` propiedad de `T`.

* La variable `allowedParents` propiedad de `T`.

* La variable `allowedChildren` propiedad de la plantilla de `P`.

La evaluación funciona de la siguiente manera:

* El primer no vacío `cq:allowedTemplates` propiedad encontrada al ascender la jerarquía de páginas comenzando por `P` se compara con la ruta de `T`. Si ninguno de los valores coincide, `T` se rechaza.

* If `T` tiene un no vacío `allowedPaths` , pero ninguno de los valores coincide con la ruta de `P`, `T` se rechaza.

* Si ambas propiedades anteriores están vacías o no existen, `T` se rechaza a menos que pertenezca a la misma aplicación que `P`. `T` pertenece a la misma aplicación que `P` if y only si el nombre del segundo nivel de la ruta de acceso de `T` es el mismo que el nombre del segundo nivel de la ruta de `P`. Por ejemplo, la plantilla `/apps/geometrixx/templates/foo` pertenece a la misma aplicación que la página `/content/geometrixx`.

* If `T` tiene un no vacío `allowedParents` , pero ninguno de los valores coincide con la ruta de `P`, `T` se rechaza.

* Si la plantilla de `P` tiene un no vacío `allowedChildren` , pero ninguno de los valores coincide con la ruta de `T`, `T` se rechaza.

* En todos los demás casos, `T` está permitido.

El diagrama siguiente muestra el proceso de evaluación de la plantilla:

![chlimage_1-176](assets/chlimage_1-176.png)

#### Limitación de plantillas utilizadas en páginas secundarias {#limiting-templates-used-in-child-pages}

Para limitar las plantillas que se pueden usar para crear páginas secundarias en una página determinada, use la variable `cq:allowedTemplates` propiedad de `jcr:content` de la página para especificar la lista de plantillas que se permitirán como páginas secundarias. Cada valor de la lista debe ser una ruta absoluta a una plantilla para una página secundaria permitida, por ejemplo `/apps/geometrixx/templates/contentpage`.

Puede usar la variable `cq:allowedTemplates` en la plantilla  `jcr:content` para que esta configuración se aplique a todas las páginas recién creadas que utilicen esta plantilla.

Si desea agregar más restricciones, por ejemplo, con respecto a la jerarquía de plantillas, puede usar la variable `allowedParents/allowedChildren` propiedades de la plantilla. A continuación, puede especificar explícitamente que las páginas creadas a partir de una plantilla T deben ser páginas principales o secundarias de páginas creadas a partir de una plantilla T.

## Plantillas: fragmentos de contenido {#templates-content-fragments}

Consulte [Plantillas de fragmento de contenido](/help/sites-developing/content-fragment-templates.md).
