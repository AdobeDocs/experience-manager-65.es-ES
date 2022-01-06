---
title: Obtenga información sobre la creación de modelos de fragmento de contenido en AEM
description: Obtenga información sobre los conceptos y la mecánica del contenido de modelado para su CMS sin encabezado mediante modelos de fragmentos de contenido.
source-git-commit: 38525b6cc14e9f6025564c060b8cfb4f9e0ea473
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 2%

---

# Obtenga información sobre la creación de modelos de fragmento de contenido en AEM {#architect-headless-content-fragment-models}

## La historia hasta ahora {#story-so-far}

Al principio del [recorrido de autor de contenido sin encabezado de AEM](overview.md) el [Conceptos básicos de modelado de contenido para usuarios sin encabezado con AEM](basics.md) abarcaba los conceptos básicos y la terminología relevantes para la creación sin encabezado.

Este artículo se basa en estos modelos para que pueda comprender cómo crear sus propios modelos de fragmento de contenido para su proyecto sin encabezado de AEM.

## Objetivo {#objective}

* **Audiencia**: Principiante
* **Objetivo**: los conceptos y mecanismos de modelado de contenido para su CMS sin encabezado utilizando los modelos de fragmentos de contenido.

<!-- which persona does this? -->
<!-- and who allows the configuration on the folders? -->

<!--
## Enabling Content Fragment Models {#enabling-content-fragment-models}

At the very start you need to enable Content Fragment Models for your site, this is done in the Configuration Browser; under Tools -> General -> Configuration Browser. You can either select to configure the global entry, or create a new configuration. For example:

![Define configuration](/help/assets/content-fragments/assets/cfm-conf-01.png)

>[!NOTE]
>
>See Additional Resources - Content Fragments in the Configuration Browser
-->

## Creación de modelos de fragmento de contenido {#creating-content-fragment-models}

A continuación, se pueden crear los modelos de fragmentos de contenido y definir la estructura. Esto se puede hacer en Herramientas -> Recursos -> Modelos de fragmento de contenido.

![Modelos de fragmento de contenido en herramientas](assets/cfm-tools.png)

Después de seleccionarlo, navegará a la ubicación del modelo y seleccione **Crear**. Aquí puede introducir varios detalles clave.

La opción **Habilitar modelo** está activada de forma predeterminada. Esto significa que el modelo estará disponible para su uso (en la creación de fragmentos de contenido) en cuanto lo haya guardado. Puede desactivarlo si lo desea; más adelante hay oportunidades de habilitar (o deshabilitar) un modelo existente.

![Crear modelo de fragmento de contenido](/help/assets/content-fragments/assets/cfm-models-02.png)

Confirme con **Crear** y entonces puede **Apertura** el modelo para comenzar a definir la estructura.

## Definición de modelos de fragmento de contenido {#defining-content-fragment-models}

Cuando abra un nuevo modelo, verá un gran espacio en blanco a la izquierda y una larga lista de **Tipos de datos** a la derecha:

![Modelo vacío](/help/assets/content-fragments/assets/cfm-models-03.png)

Entonces, ¿qué se debe hacer?

Puede arrastrar instancias del **Tipos de datos** en el espacio izquierdo - ya está definiendo su modelo!

![Definición de campos](/help/assets/content-fragments/assets/cfm-models-04.png)

Una vez agregado un tipo de datos, se le pedirá que defina la variable **Propiedades** para ese campo. Dependen del tipo que se utilice. Por ejemplo:

![Propiedades de datos](/help/assets/content-fragments/assets/cfm-models-05.png)

Puede agregar tantos campos como necesite. Por ejemplo:

![Modelo de fragmento de contenido](/help/assets/content-fragments/assets/cfm-models-07.png)

### Sus autores de contenido {#your-content-authors}

Los autores de contenido no ven los tipos de datos y las propiedades reales que utilizó para crear los modelos. Esto significa que es posible que tenga que proporcionar ayuda e información sobre cómo completan campos específicos. Para obtener información básica, puede utilizar la etiqueta de campo y el valor predeterminado, pero puede que sea necesario considerar casos más complejos como la documentación específica del proyecto.

>[!NOTE]
>
>Consulte Recursos adicionales: Modelos de fragmento de contenido.

## Administración de modelos de fragmento de contenido {#managing-content-fragment-models}

<!-- needs more details -->

La administración de los modelos de fragmento de contenido implica:

* Habilitarlos (o desactivarlos): esto hace que estén disponibles para autores al crear fragmentos de contenido.
* Eliminación: la eliminación siempre es necesaria, pero debe tener en cuenta la eliminación de un modelo que ya se esté utilizando para los fragmentos de contenido, en particular los fragmentos que ya se han publicado.

## Publicación {#publishing}

<!-- needs more details -->

Los modelos de fragmento de contenido deben publicarse cuando se publican fragmentos de contenido dependientes, o antes de hacerlo.

>[!NOTE]
>
>Si un autor intenta publicar un fragmento de contenido para el que el modelo aún no se ha publicado, una lista de selección lo indicará y el modelo se publicará con el fragmento.

En cuanto se publica un modelo, aparece *bloqueado* en modo READ-ONLY en author. Esto tiene como objetivo evitar cambios que pudieran provocar errores en los esquemas y consultas de GraphQL existentes, especialmente en el entorno de publicación. Se indica en la consola mediante **Bloqueado**.

Cuando el modelo es **Bloqueado** (en modo READ-ONLY), puede ver el contenido y la estructura de los modelos, pero no puede editarlos directamente; aunque puede administrar **Bloqueado** modelos desde la consola o desde el editor de modelos.

## Siguientes pasos {#whats-next}

Ahora que ha aprendido los conceptos básicos, el siguiente paso es comenzar a crear sus propios modelos de fragmento de contenido.

## Recursos adicionales {#additional-resources}

* [Conceptos de creación](/help/sites-authoring/author.md)

* [Gestión básica](/help/sites-authoring/basic-handling.md) : esta página se basa principalmente en la variable **Sitios** consola, pero muchas de las funciones principales también son relevantes para desplazarse a y realizar acciones en, **Modelos de fragmento de contenido** en el **Recursos** consola.

* [Trabajar con fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)

   * [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)

      * [Definición del modelo de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md#defining-your-content-fragment-model)

      * [Activación o desactivación de un modelo de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md#enabling-disabling-a-content-fragment-model)

      * [Permitir modelos de fragmento de contenido en la carpeta de recursos](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

      * [Eliminación de un modelo de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md#deleting-a-content-fragment-model)

      * [Publicación de un modelo de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model)

      * [Cancelación de la publicación de un modelo de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md#unpublishing-a-content-fragment-model)

      * [Modelos de fragmento de contenido bloqueados (publicados)](/help/assets/content-fragments/content-fragments-models.md#locked-published-content-fragment-models)

* Guías de introducción

   * [Creación de modelos de fragmento de contenido Guía de inicio rápido sin encabezado](/help/sites-developing/headless/getting-started/create-content-model.md)
