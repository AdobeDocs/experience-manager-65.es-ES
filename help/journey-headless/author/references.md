---
title: Obtenga información sobre el uso de referencias en fragmentos de contenido
description: Obtenga información sobre el uso de referencias en fragmentos de contenido para contenido, otros fragmentos y otros recursos (medios). Introduzca la necesidad y la mecánica de los fragmentos anidados para la creación de CMS sin encabezado.
index: true
hide: false
hidefromtoc: false
source-git-commit: 9661061a98c31fbb74bd0716dbedc7abef298f44
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 2%

---

# Obtenga información sobre el uso de referencias en fragmentos de contenido {#author-headless-references}

## La historia hasta ahora {#story-so-far}

Al principio del [recorrido de autor de contenido sin encabezado de AEM](overview.md) el [Introducción](introduction.md) abarcaba los conceptos básicos y la terminología relevantes para la creación sin encabezado.

Ha aprendido los conceptos básicos de la creación de CMS sin encabezado, con una introducción a la creación con AEMaaCS y, en particular, la creación de fragmentos de contenido.

Este artículo se basa en estos elementos para que pueda comprender cómo utilizar las referencias para crear su propio contenido para su proyecto sin encabezado de AEM.

## Objetivo {#objective}

* **Audiencia**: Avanzadas
* **Objetivo**: Introduzca el uso de referencias para la creación de CMS sin encabezado. Qué tipos de referencias están disponibles y cuáles son sus propósitos:

   * Referencias de contenido
   * Referencias de recursos/medios
   * Referencias de fragmento
   * Referencias ad hoc desde dentro de un bloque de texto

## ¿Qué son las referencias? {#what-are-references}

Las referencias son simplemente un mecanismo para conectar los recursos, ya sea otro contenido, recursos (como en imágenes) u otros fragmentos. Aunque son muy similares, hay algunas diferencias.

Algunas referencias tienen tipos de datos específicos (por ejemplo, Referencias de contenido y Referencias de fragmento), mientras que otras se añaden simplemente como una referencia dentro de un bloque de texto (referencias de recursos y referencias ad hoc).

![Fragmentos de contenido: referencias](/help/journey-headless/author/assets/headless-journey-author-references-01.png)

## Referencias de contenido {#content-references}

Las referencias de contenido hacen precisamente eso: le permiten hacer referencia a cualquier otro contenido. Se abrirá un explorador que le permitirá seleccionar el elemento de contenido.

## Referencias de recursos/medios {#assets-media-references}

Se puede hacer referencia a los recursos (por ejemplo, imágenes o medios) dentro de un bloque de texto utilizando la variable **Insertar recurso** . Se abrirá un explorador que le permitirá seleccionar el recurso.

![Fragmentos de contenido: Insertar recurso](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## Referencias de fragmento {#fragment-references}

Una vez más, las referencias de fragmento hacen precisamente eso: le permiten hacer referencia a otro fragmento. Por qué esto es significativo necesita un poco más de explicación.

Por ejemplo, puede tener los siguientes modelos de fragmento de contenido definidos:

* Ciudad
* Empresa
* Person
* Premios

Parece bastante sencillo, pero por supuesto una compañía tiene un CEO y empleados....y todas son personas, cada una definida como una persona.

Y una persona puede tener un premio (o tal vez dos).

* Mi empresa - Empresa
   * CEO - Persona
   * Empleado(s) - Persona
      * Premio personal - Premio

Y eso es sólo para empezar. Según la complejidad, un Premio podría ser específico de la empresa o una empresa podría tener su oficina principal en una ciudad específica.

Representar estas interrelaciones se puede lograr con Referencias de fragmento, tal como las entiende usted (el autor) y las aplicaciones sin encabezado.

Como autor, no es responsable de definir estas relaciones (lo hace el arquitecto de contenido al crear el modelo de fragmento de contenido), pero necesita saber cómo reconocer y editar las referencias.

### Creación de fragmentos anidados {#author-nested-fragment}

La creación de referencias de fragmento es bastante sencilla (aunque normalmente el campo no se etiquetará como **Referencia de fragmento**). Puede escribir la referencia directamente o (lo más probable) seleccionar el icono de carpeta para abrir un navegador que le permita desplazarse y seleccionar el fragmento que necesita.

![Fragmentos de contenido: referencias](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

La definición de los controles del modelo de fragmento de contenido:

* si puede seleccionar agregar varias referencias
* los tipos de modelo de fragmentos de contenido que puede seleccionar; el modelo de fragmento de contenido define los modelos de fragmento permitidos para la referencia, por lo que AEM presenta solo fragmentos basados en esos modelos.

### Navegación por fragmentos anidados {#navigate-nested-fragment}

Al usar la variable **Árbol de estructura** del Editor de fragmentos de contenido puede desplazarse por los fragmentos a los que hace referencia el fragmento y, a continuación, por las referencias que puedan contener. Al seleccionar una referencia, se abre ese fragmento para editarlo.

>[!NOTE]
>
>Con las rutas de exploración del panel principal, puede volver al punto de inicio.

![Árbol de estructura de fragmento de contenido](/help/assets/content-fragments/assets/cfm-structuretree-02.png)

## Referencias Ad Hoc {#adhoc-references}

Las referencias ad hoc se pueden agregar como un vínculo simple dentro de un bloque de texto:

![Fragmentos de contenido: referencias específicas](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## Siguientes pasos {#whats-next}

Ahora que ha aprendido sobre referencias y estructura en fragmentos de contenido, el siguiente paso es [Descubra más información sobre metadatos y etiquetado](metadata-tagging.md). Esto presentará y explicará cómo puede definir metadatos y etiquetas para sus fragmentos de contenido.

## Recursos adicionales {#additional-resources}

* [Trabajar con fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)

   * [Administrar fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md)

      * [Aplicar la configuración a la carpeta de recursos](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [Creación de un fragmento de contenido](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [Variaciones: creación de fragmentos de contenido](/help/assets/content-fragments/content-fragments-variations.md)

   * [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)

      * [Modelos de fragmento de contenido: tipos de datos](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [Modelos de fragmento de contenido: propiedades](/help/assets/content-fragments/content-fragments-models.md#properties)


* Guías de introducción
   * [Creación de una carpeta de recursos Guía de inicio rápido sin encabezado](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [recorrido de arquitecto de contenido sin encabezado de AEM](/help/journey-headless/architect/overview.md)

* [recorrido de traducción AEM sin encabezado](/help/journey-headless/translation/overview.md)
