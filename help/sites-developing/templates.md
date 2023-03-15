---
title: Plantillas
seo-title: Templates
description: Las plantillas se utilizan al crear una página que se utilizará como base para la nueva página
seo-description: Templates are used when creating a page which will be used as the base for the new page
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 1%

---

# Plantillas{#templates}

AEM Las plantillas se utilizan en varios puntos de la lista de elementos

* Cuándo [para crear una página, debe seleccionar una plantilla](#templates-pages); se utilizará como base para la nueva página. La plantilla define la estructura de la página resultante, cualquier contenido inicial y el [componentes](/help/sites-authoring/default-components.md) que se pueden utilizar (propiedades de diseño).

* Cuándo [Para crear un fragmento de contenido, también debe seleccionar una plantilla](#templates-content-fragments). Esta plantilla define la estructura, los elementos iniciales y las variaciones.

Las siguientes plantillas se tratan en detalle:

* [Plantillas de página: editables](/help/sites-developing/page-templates-editable.md)
* [Plantillas de página: estáticas](/help/sites-developing/page-templates-static.md)
* [Plantillas de fragmentos de contenido](/help/sites-developing/content-fragment-templates.md)
* [Representación de plantilla adaptable](/help/sites-developing/templates-adaptive-rendering.md)

## Plantillas - Páginas {#templates-pages}

AEM ahora ofrece dos tipos básicos de plantillas para crear páginas:

>[!NOTE]
>
>Cuando se usa una plantilla para lo siguiente [crear una nueva página](/help/sites-authoring/managing-pages.md#creating-a-new-page) no hay ninguna diferencia visible (para el autor de la página) ni indicación del tipo de plantilla que se está utilizando.

### Plantillas editables {#editable-templates}

AEM Ahora, las plantillas editables se consideran prácticas recomendadas para desarrollar con los.

Las ventajas de las plantillas editables:

* Puede ser [created](/help/sites-authoring/templates.md#creating-a-new-template-template-author) y [editado](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) por sus autores.

* Se han introducido para permitirle definir lo siguiente para cualquier página creada con la plantilla:

   * la estructura
   * el contenido inicial
   * políticas de contenido

* Después de crear la nueva página, se mantiene una conexión dinámica entre la página y la plantilla; esto significa que los cambios en la estructura de la plantilla se reflejarán en cualquier página creada con esa plantilla (los cambios en el contenido inicial no se reflejarán).
* Utiliza directivas de contenido (editadas desde el editor de plantillas) para mantener las propiedades de diseño (no utiliza el modo Diseño en el editor de páginas).
* Se almacenan en `/conf`
* Consulte [Plantillas editables](/help/sites-developing/page-templates-editable.md) para obtener más información.

>[!NOTE]
>
>AEM Hay disponible un artículo de la comunidad de que explica cómo desarrollar un sitio de Experience Manager con plantillas editables, consulte [Creación de un sitio web de Adobe Experience Manager 6.5 con plantillas editables](https://helpx.adobe.com/experience-manager/using/first_aem64_website.html).

### Plantillas estáticas {#static-templates}

Plantillas estáticas:

* Los desarrolladores deben definirlo y configurarlo.
* AEM Este era el sistema de creación de plantillas original de la creación de plantillas de la y ha estado disponible para muchas versiones.
* Una plantilla estática es una jerarquía de nodos que tiene la misma estructura que la página que se va a crear, pero sin contenido real.
* Se copian para crear la nueva página; después de esta acción, no existe ninguna conexión dinámica.
* Usos [Modo de diseño](/help/sites-authoring/default-components-designmode.md) para conservar las propiedades de diseño.
* Se almacenan en `/apps`
* Consulte [Plantillas estáticas](/help/sites-developing/page-templates-static.md) para obtener más información.

>[!NOTE]
>
>AEM A partir de la versión 6.5, el uso de plantillas estáticas no se considera una práctica recomendada. En su lugar, utilice Plantillas editables.
>
>[AEM Modernización de](modernization-tools.md) Las herramientas de pueden ayudarle a migrar de plantillas estáticas a editables.

### Disponibilidad de la plantilla {#template-availability}

>[!CAUTION]
>
>AEM ofrece varias propiedades para controlar las plantillas permitidas en **Sites**. Sin embargo, combinarlas puede dar lugar a reglas muy complejas difíciles de rastrear y administrar.
>
>Por lo tanto, Adobe recomienda empezar de forma sencilla definiendo:
>
>* solo el `cq:allowedTemplates` propiedad
>
>* solo en la raíz del sitio
>
>Por ejemplo, consulte We.Retail: `/content/we-retail/jcr:content`
>
>Las propiedades `allowedPaths`, `allowedParents`, y `allowedChildren` también se puede colocar en las plantillas para definir reglas más sofisticadas. Sin embargo, cuando es posible, lo es *mucho* más fácil de definir `cq:allowedTemplates` propiedades en las subsecciones del sitio si es necesario restringir aún más las plantillas permitidas.
>
>Una ventaja adicional es que el `cq:allowedTemplates` Las propiedades puede actualizarlas un autor en el **Avanzadas** de la pestaña **Propiedades de página**. Las demás propiedades de la plantilla no se pueden actualizar mediante la interfaz de usuario (estándar), por lo que se necesitaría un desarrollador para mantener las reglas y una implementación de código para cada cambio.

Al crear una nueva página en la interfaz de administración del sitio, la lista de plantillas disponibles depende de la ubicación de la nueva página y de las restricciones de colocación especificadas en cada plantilla.

Las siguientes propiedades determinan si una plantilla `T` se puede usar para que una nueva página se coloque como elemento secundario de la página `P`. Cada una de estas propiedades es una cadena de varios valores que contiene cero o más expresiones regulares que se utilizan para la coincidencia con rutas:

* El `cq:allowedTemplates` propiedad del `jcr:content` subnodo de `P` o un antecesor de `P`.

* El `allowedPaths` propiedad de `T`.

* El `allowedParents` propiedad de `T`.

* El `allowedChildren` propiedad de la plantilla de `P`.

La evaluación funciona de la siguiente manera:

* La primera no vacía `cq:allowedTemplates` se encontró la propiedad al ascender la jerarquía de páginas que empieza por `P` se compara con la ruta de `T`. Si ninguno de los valores coincide, `T` se ha rechazado.

* If `T` tiene un no vacío `allowedPaths` , pero ninguno de los valores coincide con la ruta de `P`, `T` se ha rechazado.

* Si ambas propiedades anteriores están vacías o no existen, `T` se rechaza a menos que pertenezca a la misma aplicación que `P`. `T` pertenece a la misma aplicación que `P` if y only si el nombre del segundo nivel de la ruta de `T` es el mismo que el nombre del segundo nivel de la ruta de `P`. Por ejemplo, la plantilla `/apps/geometrixx/templates/foo` pertenece a la misma aplicación que la página `/content/geometrixx`.

* If `T` tiene un no vacío `allowedParents` , pero ninguno de los valores coincide con la ruta de `P`, `T` se ha rechazado.

* Si la plantilla de `P` tiene un no vacío `allowedChildren` , pero ninguno de los valores coincide con la ruta de `T`, `T` se ha rechazado.

* En todos los demás casos, `T` está permitido.

El diagrama siguiente muestra el proceso de evaluación de la plantilla:

![chlimage_1-176](assets/chlimage_1-176.png)

#### Limitación de plantillas utilizadas en páginas secundarias {#limiting-templates-used-in-child-pages}

Para limitar qué plantillas se pueden utilizar para crear páginas secundarias en una página determinada, utilice la variable `cq:allowedTemplates` propiedad de `jcr:content` de la página para especificar la lista de plantillas que pueden utilizarse como páginas secundarias. Cada valor de la lista debe ser una ruta absoluta a una plantilla para una página secundaria permitida, por ejemplo `/apps/geometrixx/templates/contentpage`.

Puede usar el complemento `cq:allowedTemplates` propiedad en la plantilla  `jcr:content` para que esta configuración se aplique a todas las páginas recién creadas que utilicen esta plantilla.

Si desea agregar más restricciones, por ejemplo con respecto a la jerarquía de plantillas, puede utilizar la variable `allowedParents/allowedChildren` propiedades en la plantilla. A continuación, puede especificar explícitamente que las páginas creadas a partir de una plantilla T tengan que ser páginas principales o secundarias de páginas creadas a partir de una plantilla T.

## Plantillas: fragmentos de contenido {#templates-content-fragments}

Consulte [Plantillas de fragmentos de contenido](/help/sites-developing/content-fragment-templates.md) para obtener información completa.
