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
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# Plantillas{#templates}

Las plantillas se utilizan en varios puntos de AEM:

* When [creating a page you need to select a template](#templates-pages); this will be used as the base for the new page. The template defines the structure of the resultant page, any initial content and the [components](/help/sites-authoring/default-components.md) that can be used (design properties).

* Al [crear un fragmento de contenido, también debe seleccionar una plantilla](#templates-content-fragments). Esta plantilla define la estructura, los elementos iniciales y las variaciones.

Las siguientes plantillas se tratan en detalle:

* [Plantillas de página: editables](/help/sites-developing/page-templates-editable.md)
* [Plantillas de página: estáticas](/help/sites-developing/page-templates-static.md)
* [Plantillas de fragmento de contenido](/help/sites-developing/content-fragment-templates.md)
* [Representación de plantilla adaptable](/help/sites-developing/templates-adaptive-rendering.md)

## Plantillas - Páginas {#templates-pages}

AEM ahora ofrece dos tipos básicos de plantillas para crear páginas:

>[!NOTE]
>
>Al utilizar una plantilla para [crear una nueva página](/help/sites-authoring/managing-pages.md#creating-a-new-page) , no hay ninguna diferencia visible (para el autor de la página) ni indicación del tipo de plantilla que se está utilizando.

### Plantillas editables {#editable-templates}

Las plantillas editables ahora se consideran prácticas recomendadas para el desarrollo con AEM.

Ventajas de las plantillas editables:

* Los autores pueden [crearlos](/help/sites-authoring/templates.md#creating-a-new-template-template-author) y [editarlos](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) .

* Se han introducido para permitirle definir lo siguiente para cualquier página creada con la plantilla:

   * la estructura
   * el contenido inicial
   * políticas de contenido

* Después de crear la nueva página, se mantiene una conexión dinámica entre la página y la plantilla; esto significa que los cambios en la estructura de la plantilla se reflejarán en cualquier página creada con esa plantilla (los cambios en el contenido inicial no se reflejarán).
* Utiliza políticas de contenido (editadas desde el editor de plantillas) para mantener las propiedades de diseño (no utiliza el modo Diseño dentro del editor de páginas).
* Se almacenan en `/conf`
* Consulte Plantillas [editables](/help/sites-developing/page-templates-editable.md) para obtener más información.

>[!NOTE]
>
>Hay disponible un artículo de la comunidad de AEM que explica cómo desarrollar un sitio de Experience Manager con plantillas editables; consulte [Creación de un sitio web de Adobe Experience Manager 6.5 con plantillas](https://helpx.adobe.com/experience-manager/using/first_aem64_website.html)editables.

### Plantillas estáticas {#static-templates}

Plantillas estáticas:

* Los desarrolladores deben definirlo y configurarlo.
* Este era el sistema de plantilla original de AEM y ha estado disponible para muchas versiones.
* Una plantilla estática es una jerarquía de nodos que tiene la misma estructura que la página que se va a crear, pero sin ningún contenido real.
* Se copian para crear la nueva página, después de esto no existe ninguna conexión dinámica.
* Uses [Design Mode](/help/sites-authoring/default-components-designmode.md) to persist design properties.
* Se almacenan en `/apps`
* Consulte Plantillas [estáticas](/help/sites-developing/page-templates-static.md) para obtener más información.

>[!NOTE]
>
>A partir de AEM 6.5, el uso de plantillas estáticas no se considera una práctica recomendada. Utilice plantillas editables en su lugar.
>
>[Las herramientas de modernización](modernization-tools.md) de AEM pueden ayudarle a migrar de plantillas estáticas a plantillas editables.

### Disponibilidad de la plantilla {#template-availability}

>[!CAUTION]
>
>AEM ofrece varias propiedades para controlar las plantillas permitidas en **Sitios**. Sin embargo, combinarlos puede llevar a reglas muy complejas que son difíciles de rastrear y administrar.
>
>Por lo tanto, Adobe recomienda empezar con sencillez, definiendo:
>
>* solo la `cq:allowedTemplates` propiedad
   >
   >
* solo en la raíz del sitio
>
>
Para ver un ejemplo, consulte We.Retail: `/content/we-retail/jcr:content`
>
>Las propiedades `allowedPaths`, `allowedParents`y `allowedChildren` también se pueden colocar en las plantillas para definir reglas más sofisticadas. Sin embargo, cuando es posible, es *mucho* más sencillo definir más `cq:allowedTemplates` propiedades en las subsecciones del sitio si es necesario restringir aún más las plantillas permitidas.
>
>Una ventaja adicional es que un autor puede actualizar las `cq:allowedTemplates` propiedades en la ficha **Avanzadas** de las Propiedades de la **página**. Las demás propiedades de plantilla no se pueden actualizar con la IU (estándar), por lo que sería necesario que un desarrollador mantuviera las reglas y una implementación de código para cada cambio.

Al crear una nueva página en la interfaz de administración del sitio, la lista de plantillas disponibles depende de la ubicación de la nueva página y de las restricciones de colocación especificadas en cada plantilla.

Las siguientes propiedades determinan si `T` se permite utilizar una plantilla para que una nueva página se coloque como elemento secundario de la página `P`. Cada una de estas propiedades es una cadena de varios valores que contiene cero o más expresiones regulares que se utilizan para hacer coincidir con rutas:

* La `cq:allowedTemplates` propiedad del `jcr:content` subnodo de `P` o un antecesor de `P`.

* La `allowedPaths` propiedad de `T`.

* La `allowedParents` propiedad de `T`.

* La `allowedChildren` propiedad de la plantilla de `P`.

La evaluación funciona de la siguiente manera:

* La primera propiedad no vacía `cq:allowedTemplates` encontrada al ascender la jerarquía de páginas empezando por `P` se compara con la ruta de `T`. Si ninguno de los valores coincide, `T` se rechaza.

* Si `T` tiene una propiedad no vacía `allowedPaths` , pero ninguno de los valores coincide con la ruta de `P`, `T` se rechaza.

* Si las dos propiedades anteriores están vacías o no existen, `T` se rechaza a menos que pertenezcan a la misma aplicación que `P`. `T` pertenece a la misma aplicación que `P` si el nombre del segundo nivel de la ruta de `T` acceso es el mismo que el nombre del segundo nivel de la ruta de `P`. Por ejemplo, la plantilla `/apps/geometrixx/templates/foo` pertenece a la misma aplicación que la página `/content/geometrixx`.

* Si `T` tiene una propiedad no vacía `allowedParents` , pero ninguno de los valores coincide con la ruta de `P`, `T` se rechaza.

* Si la plantilla de `P` tiene una propiedad no vacía `allowedChildren` , pero ninguno de los valores coincide con la ruta de `T`, `T` se rechaza.

* En todos los demás casos, `T` se permite.

El diagrama siguiente muestra el proceso de evaluación de la plantilla:

![chlimage_1-176](assets/chlimage_1-176.png)

#### Limitación de plantillas utilizadas en páginas secundarias {#limiting-templates-used-in-child-pages}

Para limitar qué plantillas se pueden utilizar para crear páginas secundarias en una página determinada, utilice la `cq:allowedTemplates` propiedad del `jcr:content` nodo de la página para especificar la lista de plantillas que se permitirán como páginas secundarias. Cada valor de la lista debe ser una ruta absoluta a una plantilla para una página secundaria permitida, por ejemplo `/apps/geometrixx/templates/contentpage`.

Puede utilizar la `cq:allowedTemplates` `jcr:content` propiedad en el nodo de la plantilla para que esta configuración se aplique a todas las páginas creadas recientemente que utilicen esta plantilla.

Si desea agregar más restricciones, por ejemplo en relación con la jerarquía de plantillas, puede utilizar las `allowedParents/allowedChildren` propiedades de la plantilla. A continuación, puede especificar explícitamente que las páginas creadas a partir de una plantilla T deben ser páginas principales/secundarias de páginas creadas a partir de una plantilla T.

## Plantillas - Fragmentos de contenido {#templates-content-fragments}

Consulte Plantillas [de fragmento de contenido](/help/sites-developing/content-fragment-templates.md) para obtener información completa.
