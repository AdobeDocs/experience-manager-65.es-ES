---
title: Mejorar el rendimiento de los formularios grandes mediante la carga diferida
seo-title: Improve performance of large forms with lazy loading
description: La carga diferida mejora significativamente el rendimiento de los formularios adaptables grandes y complejos al aplazar la inicialización y carga de los fragmentos de formulario hasta que sean visibles.
seo-description: Lazy loading significantly improves the performance of large and complex adaptive forms by deferring initialization and loading of form fragments until they are visible.
uuid: 6be3d2f0-1b2a-4090-af66-2b08487c31bc
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: a20736b7-f7b4-4da1-aa32-2408049b1209
docset: aem65
feature: Adaptive Forms
exl-id: f7e3e2cd-0cbe-4b26-9e55-7afc6dc3af63
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 59%

---

# Mejorar el rendimiento de los formularios grandes mediante la carga diferida{#improve-performance-of-large-forms-with-lazy-loading}

## Introducción a la carga diferida {#introduction-to-lazy-loading}

Cuando un formulario se vuelve grande y complejo e incluye cientos y miles de campos, los usuarios finales experimentan tiempos de respuesta largos cuando representan formularios en tiempo de ejecución. Para minimizar el tiempo de respuesta, los formularios adaptables permiten dividir los formularios en fragmentos lógicos y configurarlos para retrasar la inicialización o carga de los fragmentos hasta que el fragmento tenga que ser visible. Este proceso se denomina carga diferida. Además, los fragmentos configurados para la carga diferida se descargan una vez que el usuario se desplaza a otras secciones del formulario y los fragmentos ya no son visibles.

En primer lugar, vamos a explicar cuáles son los requisitos y los pasos preparatorios antes de configurar la carga diferida.

## Preparación para configurar la carga diferida {#preparing-to-configure-lazy-loading}

Antes de configurar la carga diferida de fragmentos en el formulario adaptable, es importante definir estrategias para crear fragmentos, identificar valores que se utilizan en secuencias de comandos o que se mencionan en otros fragmentos y definir reglas para controlar la visibilidad de los campos en fragmentos cargados de forma diferida.

* **Identificar y crear fragmentos**
Solo se pueden configurar fragmentos de formulario adaptables para la carga diferida. Un fragmento es un segmento independiente que reside fuera de un formulario adaptable y que puede reutilizarse en todos los formularios. Por lo tanto, el primer paso para implementar la carga diferida es identificar las secciones lógicas de un formulario y convertirlas en fragmentos. Puede crear un fragmento desde cero o guardar un panel de formulario existente como fragmento.

   Para obtener más información sobre la creación de fragmentos, consulte [Fragmentos de formulario adaptables](../../forms/using/adaptive-form-fragments.md).

* **Identificar y marcar los valores globales**: las transacciones basadas en Forms implican elementos dinámicos para capturar datos relevantes de los usuarios y procesarlos para simplificar la experiencia de rellenado de los formularios. Por ejemplo, el formulario tiene el campo A en el fragmento X, cuyo valor determina la validez del campo B en otro fragmento. En este caso, si el fragmento X está marcado para la carga diferida, el valor del campo A debe estar disponible para validar el campo B incluso cuando el fragmento X no está cargado. Para conseguirlo, puede marcar el campo A como global, lo que garantiza que su valor esté disponible para validar el campo B cuando el fragmento X no está cargado.

   Para obtener información sobre cómo convertir un valor de campo en global, consulte [Configuración de la carga diferida](../../forms/using/lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p).

* **Escribir reglas para controlar la visibilidad de los campos**: los formularios incluyen algunos campos y secciones que no son aplicables a todos los usuarios y en todas las condiciones. Los autores y desarrolladores de formularios utilizan la visibilidad o las reglas de Mostrar u ocultar para controlar su visibilidad en función de las entradas del usuario. Por ejemplo, el campo Dirección de la oficina no se muestra a los usuarios que eligen Desempleado en el campo Situación laboral en un formulario. Para obtener más información sobre cómo escribir reglas, consulte [Uso del Editor de reglas](../../forms/using/rule-editor.md).

   Puede aprovechar las reglas de visibilidad en los fragmentos cargados de forma diferida para que los campos condicionales se muestren solo cuando sean necesarios. Además, puede marcar el campo condicional como global para hacer referencia a él en la expresión de visibilidad del fragmento cargado de forma diferida.

## Configuración de la carga diferida {#configuring-lazy-loading}

Realice los siguientes pasos para habilitar la carga diferida en un fragmento de formulario adaptable:

1. Abra el formulario adaptable en modo de creación que contenga el fragmento que desea activar para la carga diferida.
1. Seleccione el fragmento de formulario adaptable y pulse ![cmppr](assets/cmppr.png).
1. En la barra lateral, habilite la opción **[!UICONTROL Cargar fragmento de forma diferida]** y pulse **Listo**.

   ![Habilitar la carga diferida para el fragmento de formulario adaptable](assets/lazy-loading-fragment.png)

   Ahora la carga diferida está habilitada en el fragmento.

Puede marcar los valores de los objetos del fragmento cargado de forma diferida como globales, de modo que estén disponibles para su uso en scripts cuando el fragmento que los contiene no esté cargado. Haga lo siguiente:

1. Abra el fragmento de formulario adaptable en modo de creación.
1. Pulse el campo cuyo valor desee marcar como global y, a continuación, pulse ![cmppr](assets/cmppr.png).
1. En la barra lateral, habilite la opción **Utilizar valor durante la carga diferida**.

   ![Campo de carga diferida en la barra lateral](assets/enable-lazy-loading.png)

   El valor ahora está marcado como global y estará disponible para su uso en scripts incluso cuando se descargue el fragmento que lo contiene.

## Consideraciones y prácticas recomendadas para configurar la carga diferida {#considerations-and-best-practices-for-configuring-lazy-loading}

A continuación encontrará algunas limitaciones, recomendaciones y puntos importantes a tener en cuenta a la hora de trabajar con la carga diferida:

* Se recomienda utilizar formularios adaptables basados en esquemas XSD sobre formularios adaptables basados en XFA para configurar la carga diferida en formularios grandes. El aumento de rendimiento debido a la implementación de carga diferida en formularios adaptables basados en XFA es relativamente menor que ganancia en formularios adaptables basados en XSD.
* No configure la carga diferida en fragmentos en un formulario adaptable que utilice **[!UICONTROL Responsable: todo en una página sin navegación]** diseño para el panel raíz. Como resultado de la configuración de diseño adaptable, todos los fragmentos se cargan simultáneamente en un formulario adaptable. También puede provocar una reducción del rendimiento.
* Se recomienda no configurar la carga diferida en el primer fragmento en un formulario adaptable.
* Se recomienda no configurar la carga diferida en fragmentos en el primer panel que se muestre al cargar el formulario adaptable.
* La carga diferida es compatible con hasta dos niveles de la jerarquía de fragmentos.
* Asegúrese de que los campos marcados como globales sean únicos en un formulario adaptable.
* Considere la posibilidad de escribir reglas de visibilidad para aquellos fragmentos que deban mostrarse u ocultarse según una condición. Por ejemplo, puede mostrar u ocultar el fragmento Datos del cónyuge en función del estado civil especificado por el usuario.
* Los componentes Archivo adjunto y Términos y condiciones no son compatibles con los fragmentos cargados de forma diferida.

### Prácticas recomendadas de scripts para configurar la carga diferida {#scripting-best-practices-for-configuring-lazy-loading}

Estos son algunos puntos importantes que debe tener en cuenta al desarrollar scripts para paneles de carga diferida:

* Asegúrese de que las secuencias de comandos initialize y calculate utilizadas en los campos de un fragmento cargado diferentemente tengan un carácter idéntico. Los scripts idempotentes son aquellos que tienen el mismo efecto incluso después de varias ejecuciones.
* Utilice la propiedad de los campos disponible de forma global para que el valor de los campos situados en un panel de carga diferida esté disponible en el resto de los paneles de un formulario.
* No reenvíe el valor de referencia de un campo dentro de un panel de carga diferida, independientemente de si el campo está marcado como global en los fragmentos o no.
* Utilice la función Restablecer del panel para restablecer todos sus elementos visibles mediante la siguiente expresión de clic.\
   guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;: &quot;navigablePanel&quot;})).resetData()
