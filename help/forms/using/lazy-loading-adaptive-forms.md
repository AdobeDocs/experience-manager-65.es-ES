---
title: Mejore el rendimiento de los formularios grandes con carga lenta
seo-title: Mejore el rendimiento de los formularios grandes con carga lenta
description: La carga diferida mejora significativamente el rendimiento de los formularios adaptables grandes y complejos al aplazar la inicialización y la carga de los fragmentos de formulario hasta que estén visibles.
seo-description: La carga diferida mejora significativamente el rendimiento de los formularios adaptables grandes y complejos al aplazar la inicialización y la carga de los fragmentos de formulario hasta que estén visibles.
uuid: 6be3d2f0-1b2a-4090-af66-2b08487c31bc
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: a20736b7-f7b4-4da1-aa32-2408049b1209
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Mejore el rendimiento de los formularios grandes con carga lenta{#improve-performance-of-large-forms-with-lazy-loading}

## Introducción a la carga diferida {#introduction-to-lazy-loading}

Cuando el formulario se vuelve grande y complejo con cientos y miles de campos, los usuarios finales experimentan un largo tiempo de respuesta al procesar formularios en tiempo de ejecución. Para minimizar el tiempo de respuesta, los formularios adaptables le permiten dividir los formularios en fragmentos lógicos y configurarlos para aplazar la inicialización o carga de fragmentos hasta que el fragmento tenga que ser visible. Se denomina carga diferida. Además, los fragmentos configurados para la carga diferida se descargan una vez que el usuario navega a otras secciones del formulario y los fragmentos ya no están visibles.

Primero comprendamos los requisitos y los pasos preparatorios antes de configurar la carga diferida.

## Preparación para configurar la carga diferida {#preparing-to-configure-lazy-loading}

Antes de configurar la carga diferida de fragmentos en el formulario adaptable, es importante definir estrategias para crear fragmentos, identificar valores que se utilizan en secuencias de comandos o que se mencionan en otros fragmentos y definir reglas para controlar la visibilidad de los campos en fragmentos cargados de forma diferida.

* **Identificar y crear fragmentos** Solo puede configurar fragmentos de formulario adaptables para la carga diferida. Un fragmento es un segmento independiente que reside fuera de un formulario adaptable y puede reutilizarse en todos los formularios. Por lo tanto, el primer paso para implementar la carga diferida es identificar las secciones lógicas de un formulario y convertirlas en fragmentos. Puede crear un fragmento desde cero o guardar un panel de formulario existente como fragmento.

   Para obtener más información sobre la creación de fragmentos, consulte Fragmentos de formulario [adaptables](../../forms/using/adaptive-form-fragments.md).

* **Identifique y marque valores globalesLas transacciones basadas en formularios implican elementos dinámicos para capturar datos relevantes de los usuarios y procesarlos para simplificar la experiencia de cumplimentación de formularios.** Por ejemplo, el formulario tiene el campo A en el fragmento X, cuyo valor determina la validez del campo B en otro fragmento. En este caso, si el fragmento X está marcado para la carga diferida, el valor del campo A debe estar disponible para validar el campo B incluso cuando no se haya cargado el fragmento X. Para lograrlo, puede marcar el campo A como global, lo que garantiza que su valor esté disponible para validar el campo B cuando no se cargue el fragmento X.

   Para obtener información sobre cómo convertir un valor de campo en global, consulte [Configuración de la carga](../../forms/using/lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p)diferida.

* **Escribir reglas para controlar la visibilidad de los campos** Los formularios incluyen algunos campos y secciones que no son aplicables a todos los usuarios y en todas las condiciones. Los autores y desarrolladores de formularios utilizan la visibilidad o las reglas de mostrar y ocultar para controlar su visibilidad en función de las entradas del usuario. Por ejemplo, el campo Dirección de oficina no se muestra a los usuarios que eligen Desempleado en el campo Estado de empleo de un formulario. Para obtener más información sobre la escritura de reglas, consulte [Uso del editor](../../forms/using/rule-editor.md)de reglas.

   Puede aprovechar las reglas de visibilidad en los fragmentos cargados de forma diferida para que los campos condicionales solo se muestren cuando sean necesarios. Asimismo, marque el campo condicional global para hacer referencia a él en la expresión de visibilidad del fragmento cargado de forma diferida.

## Configuración de la carga diferida {#configuring-lazy-loading}

Siga estos pasos para activar la carga diferida en un fragmento de formulario adaptable:

1. Abra el formulario adaptable en modo de creación que contiene el fragmento que desea activar para la carga diferida.
1. Seleccione el fragmento de formulario adaptable y toque ![cmppr](assets/cmppr.png).
1. En la barra lateral, active **[!UICONTROL Cargar fragmento]** de forma diferida y toque **Listo**.

   ![Habilitar la carga diferida para el fragmento de formulario adaptable](assets/lazy-loading-fragment.png)

   El fragmento ahora está habilitado para la carga diferida.

Puede marcar los valores de los objetos del fragmento cargado de forma diferida como globales para que estén disponibles para su uso en secuencias de comandos cuando no se cargue el fragmento que los contiene. Haga lo siguiente:

1. Abra el fragmento de formulario adaptable en modo de creación.
1. Puntee en el campo cuyo valor desee marcar como global y, a continuación, toque ![cmppr](assets/cmppr.png).
1. En la barra lateral, active **Usar valor durante la carga** diferida.

   ![Campo de carga diferido en la barra lateral](assets/enable-lazy-loading.png)

   El valor ahora está marcado como global y estará disponible para su uso en secuencias de comandos incluso cuando se descargue el fragmento que lo contiene.

## Consideraciones y prácticas recomendadas para configurar la carga lenta {#considerations-and-best-practices-for-configuring-lazy-loading}

Algunas limitaciones, recomendaciones y puntos importantes que hay que tener en cuenta al trabajar con la carga diferida son las siguientes:

* Se recomienda utilizar formularios adaptables basados en esquemas XSD en formularios adaptables basados en XFA para configurar la carga diferida en formularios grandes. El aumento de rendimiento debido a la implementación de carga lenta en formularios adaptables basados en XFA es relativamente menor que ganancia en formularios adaptables basados en XSD.
* No configure la carga diferida en fragmentos en un diseño de cuadrícula adaptable. Puede resultar en un rendimiento degradado.
* Se recomienda no configurar la carga diferida en fragmentos en el primer panel que se procesa al cargar el formulario adaptable.
* La carga diferida se admite hasta dos niveles en la jerarquía de fragmentos.
* Asegúrese de que los campos marcados como globales son únicos en un formulario adaptable.
* Considere la posibilidad de escribir reglas de visibilidad para fragmentos que deberían mostrarse u ocultarse en función de una condición. Por ejemplo, puede mostrar u ocultar el fragmento Detalles del cónyuge en función del estado civil especificado por un usuario.
* El archivo adjunto y los componentes Términos y condiciones no se admiten en fragmentos cargados de forma diferida.

### Prácticas recomendadas de secuencias de comandos para configurar la carga diferida {#scripting-best-practices-for-configuring-lazy-loading}

Los puntos importantes que hay que tener en cuenta al desarrollar secuencias de comandos para paneles de carga flotantes son los siguientes:

* Asegúrese de que las secuencias de comandos de inicialización y cálculo utilizadas en los campos de un fragmento cargado diferido son de naturaleza idéntica. Los scripts independientes son aquellos que tienen el mismo efecto incluso después de varias ejecuciones.
* Utilice la propiedad de campos disponible globalmente para que el valor de los campos ubicados en un panel de carga flotante esté disponible para todos los demás paneles de un formulario.
* No reenvíe el valor de referencia de un campo dentro de un panel flotante, independientemente de si el campo se ha marcado globalmente en los fragmentos o no.
* Utilice la función de restablecimiento del panel para restablecer todo lo visible en el panel mediante la siguiente expresión de clic.\
   guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;): &quot;navigablePanel&quot;})).resetData()

