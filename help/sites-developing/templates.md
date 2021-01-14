---
title: Plantillas
seo-title: Plantillas
description: Las plantillas se utilizan al crear una página que se utilizará como base para la nueva página
seo-description: Las plantillas se utilizan al crear una página que se utilizará como base para la nueva página
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
translation-type: tm+mt
source-git-commit: 27276945a0bdb20410f4c0e98868ea5ce1c09a47
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 0%

---


# Plantillas{#templates}

Las plantillas se utilizan en varios puntos de AEM:

* Cuando [crea una página, debe seleccionar una plantilla](#templates-pages); se utilizará como base para la nueva página. La plantilla define la estructura de la página resultante, cualquier contenido inicial y los [componentes](/help/sites-authoring/default-components.md) que se pueden utilizar (propiedades de diseño).

* Cuando [crea un fragmento de contenido, también debe seleccionar una plantilla](#templates-content-fragments). Esta plantilla define la estructura, los elementos iniciales y las variaciones.

Las siguientes plantillas se tratan en detalle:

* [Plantillas de página: editables](/help/sites-developing/page-templates-editable.md)
* [Plantillas de página: estáticas](/help/sites-developing/page-templates-static.md)
* [Plantillas de fragmento de contenido](/help/sites-developing/content-fragment-templates.md)
* [Representación de plantilla adaptable](/help/sites-developing/templates-adaptive-rendering.md)

## Plantillas - Páginas {#templates-pages}

AEM ahora oferta dos tipos básicos de plantillas para crear páginas:

>[!NOTE]
>
>Al utilizar una plantilla para [crear una nueva página](/help/sites-authoring/managing-pages.md#creating-a-new-page) no hay ninguna diferencia visible (para el autor de la página) ni indicación del tipo de plantilla que se está utilizando.

### Plantillas editables {#editable-templates}

Las plantillas editables ahora se consideran prácticas recomendadas para el desarrollo con AEM.

Ventajas de las plantillas editables:

* Sus autores pueden [crear](/help/sites-authoring/templates.md#creating-a-new-template-template-author) y [editar](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

* Se han introducido para permitirle definir lo siguiente para cualquier página creada con la plantilla:

   * la estructura
   * el contenido inicial
   * políticas de contenido

* Después de crear la nueva página, se mantiene una conexión dinámica entre la página y la plantilla; esto significa que los cambios en la estructura de la plantilla se reflejarán en cualquier página creada con esa plantilla (los cambios en el contenido inicial no se reflejarán).
* Utiliza políticas de contenido (editadas desde el editor de plantillas) para mantener las propiedades de diseño (no utiliza el modo Diseño dentro del editor de páginas).
* Se almacenan en `/conf`
* Consulte [Plantillas editables](/help/sites-developing/page-templates-editable.md) para obtener más información.

>[!NOTE]
>
>Hay disponible un artículo AEM de la comunidad que explica cómo desarrollar un sitio de Experience Manager con plantillas editables; consulte [Creación de un sitio web de Adobe Experience Manager 6.5 con plantillas editables](https://helpx.adobe.com/experience-manager/using/first_aem64_website.html).

### Plantillas estáticas {#static-templates}

Plantillas estáticas:

* Los desarrolladores deben definirlo y configurarlo.
* Este era el sistema de plantilla original de AEM y ha estado disponible para muchas versiones.
* Una plantilla estática es una jerarquía de nodos que tiene la misma estructura que la página que se va a crear, pero sin ningún contenido real.
* Se copian para crear la nueva página, después de esto no existe ninguna conexión dinámica.
* Utiliza [Modo de diseño](/help/sites-authoring/default-components-designmode.md) para mantener las propiedades de diseño.
* Se almacenan en `/apps`
* Consulte [Plantillas estáticas](/help/sites-developing/page-templates-static.md) para obtener más información.

>[!NOTE]
>
>A partir de AEM 6.5, el uso de plantillas estáticas no se considera una práctica recomendada. Utilice plantillas editables en su lugar.
>
>[AEM ](modernization-tools.md) Modernización, las herramientas pueden ayudarle a migrar de plantillas estáticas a editables.

### Disponibilidad de la plantilla {#template-availability}

>[!CAUTION]
>
>AEM oferta varias propiedades para controlar las plantillas permitidas en **Sites**. Sin embargo, combinarlos puede llevar a reglas muy complejas que son difíciles de rastrear y administrar.
>
>Por lo tanto, Adobe recomienda que el inicio sea sencillo, definiendo:
>
>* sólo la propiedad `cq:allowedTemplates`
   >
   >
* solo en la raíz del sitio
>
>
Para ver un ejemplo, consulte We.Retail: `/content/we-retail/jcr:content`
>
>Las propiedades `allowedPaths`, `allowedParents` y `allowedChildren` también se pueden colocar en las plantillas para definir reglas más sofisticadas. Sin embargo, cuando es posible, es *mucho* más sencillo definir más `cq:allowedTemplates` propiedades en las subsecciones del sitio si es necesario restringir aún más las plantillas permitidas.
>
>Una ventaja adicional es que un autor puede actualizar las propiedades `cq:allowedTemplates` en la ficha **Avanzado** de las **Propiedades de la página**. Las demás propiedades de plantilla no se pueden actualizar con la IU (estándar), por lo que sería necesario que un desarrollador mantuviera las reglas y una implementación de código para cada cambio.

Al crear una nueva página en la interfaz de administración del sitio, la lista de las plantillas disponibles depende de la ubicación de la nueva página y de las restricciones de colocación especificadas en cada plantilla.

Las siguientes propiedades determinan si se permite utilizar una plantilla `T` para colocar una nueva página como elemento secundario de la página `P`. Cada una de estas propiedades es una cadena de varios valores que contiene cero o más Expresiones regulares que se utilizan para hacer coincidir con rutas:

* La propiedad `cq:allowedTemplates` del subnodo `jcr:content` de `P` o un antecesor de `P`.

* La propiedad `allowedPaths` de `T`.

* La propiedad `allowedParents` de `T`.

* La propiedad `allowedChildren` de la plantilla de `P`.

La evaluación funciona de la siguiente manera:

* La primera propiedad `cq:allowedTemplates` no vacía que se encuentra al ascender la jerarquía de páginas comenzando por `P` se compara con la ruta de `T`. Si ninguno de los valores coincide, se rechaza `T`.

* Si `T` tiene una propiedad `allowedPaths` no vacía, pero ninguno de los valores coincide con la ruta de `P`, se rechaza `T`.

* Si las dos propiedades anteriores están vacías o no existen, `T` se rechaza a menos que pertenezca a la misma aplicación que `P`. `T` pertenece a la misma aplicación que  `P` si el nombre del segundo nivel de la ruta de acceso  `T` es el mismo que el nombre del segundo nivel de la ruta de acceso de  `P`. Por ejemplo, la plantilla `/apps/geometrixx/templates/foo` pertenece a la misma aplicación que la página `/content/geometrixx`.

* Si `T` tiene una propiedad `allowedParents` no vacía, pero ninguno de los valores coincide con la ruta de `P`, se rechaza `T`.

* Si la plantilla de `P` tiene una propiedad `allowedChildren` no vacía, pero ninguno de los valores coincide con la ruta de `T`, se rechaza `T`.

* En todos los demás casos, se permite `T`.

El diagrama siguiente muestra el proceso de evaluación de la plantilla:

![chlimage_1-176](assets/chlimage_1-176.png)

#### Limitación de plantillas utilizadas en páginas secundarias {#limiting-templates-used-in-child-pages}

Para limitar qué plantillas se pueden utilizar para crear páginas secundarias en una página determinada, utilice la propiedad `cq:allowedTemplates` del nodo `jcr:content` de la página para especificar la lista de las plantillas que se permitirán como páginas secundarias. Cada valor de la lista debe ser una ruta absoluta a una plantilla para una página secundaria permitida, por ejemplo `/apps/geometrixx/templates/contentpage`.

Puede utilizar la propiedad `cq:allowedTemplates` del nodo `jcr:content` de la plantilla para que esta configuración se aplique a todas las páginas creadas recientemente que utilicen esta plantilla.

Si desea agregar más restricciones, por ejemplo en relación con la jerarquía de plantillas, puede utilizar las propiedades `allowedParents/allowedChildren` de la plantilla. A continuación, puede especificar explícitamente que las páginas creadas a partir de una plantilla T deben ser páginas principales/secundarias de páginas creadas a partir de una plantilla T.

## Plantillas - Fragmentos de contenido {#templates-content-fragments}

Consulte [Plantillas de fragmento de contenido](/help/sites-developing/content-fragment-templates.md) para obtener información completa.
