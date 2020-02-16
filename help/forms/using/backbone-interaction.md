---
title: Interacción de la red troncal
seo-title: Interacción de la red troncal
description: Información conceptual sobre el uso de modelos JavaScript de red troncal en el espacio de trabajo de AEM Forms.
seo-description: Información conceptual sobre el uso de modelos JavaScript de red troncal en el espacio de trabajo de AEM Forms.
uuid: 040f42cb-3b76-4657-ba05-9e52647efb12
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 538591fe-29e4-40c4-a045-06095cc0c6b8
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Interacción de la red troncal{#backbone-interaction}

La estructura básica es una biblioteca que ayuda a crear y seguir la arquitectura MVC en aplicaciones web. La idea básica de la red troncal es organizar la interfaz en vistas lógicas, respaldadas por modelos, cada uno de los cuales se puede actualizar de forma independiente cuando cambia el modelo, sin tener que volver a dibujar la página. Para obtener más información sobre la red troncal, consulte [https://backbonejs.org](https://backbonejs.org/).

Algunos conceptos clave son los siguientes:

**Modelo** de red troncal Contiene datos y la mayor parte de la lógica relacionada con estos datos.

**Vista** de red troncal Se utiliza para representar el estado del modelo correspondiente. En realidad, una vista de red troncal se comporta como un controlador, escuchando los eventos de la interfaz de usuario como clics del usuario o los eventos de modelo (como los datos cambiados) y modifica la interfaz de usuario según corresponda.

**Plantilla** HTML Una plantilla de envoltorio que tiene marcadores de posición rellenados por el modelo.

**Espacio de trabajo** de AEM Forms Contiene varios componentes individuales. Cada componente:

* Representa un solo elemento de interfaz de usuario lógico.
* Puede ser una colección de componentes similares.
* Se compone de modelo Backbone, vista Backbone y plantilla HTML.
* Contiene una referencia a un servicio.
* Contiene una referencia a las utilidades requeridas.

Cuando se inicializa un componente, se crean los siguientes objetos:

* Se crea una nueva instancia del modelo de red troncal para el componente. El servicio se inyecta en el modelo.
* Se crea una nueva instancia de la vista de red troncal.
* La instancia del modelo correspondiente, la plantilla HTML y las utilidades se insertan en la vista.

En la vista de red troncal, hay un mapa de eventos que asigna los distintos eventos que pueden surgir debido a las interacciones de la interfaz de usuario con un controlador correspondiente. Esta asignación se inicia una vez que se inicializa un componente.

Cuando se inicializa una vista, la vista llama a su modelo correspondiente para recuperar datos del servidor. Una vez que todos los datos requeridos por una vista están disponibles, la vista procesa los datos en el formato especificado por la plantilla HTML. Varias vistas pueden compartir el mismo modelo de comunicación.

![](do-not-localize/aem_forms_workflow.png)

Un ejemplo:

1. El usuario hace clic en una plantilla de tarea en la lista de tareas.
1. La vista de tareas escucha el clic y llama a la función de procesamiento en el modelo de tareas.
1. El modelo de tareas llama posteriormente al servicio, que es un punto común para todas las comunicaciones con el servidor de AEM Forms.
1. La clase de servicio llama al extremo REST de AEM Forms para el método de procesamiento mediante ajax.
1. La devolución de llamada correcta para esta invocación de Ajax se define en el modelo de tareas.
1. El modelo de tareas genera un evento de red troncal como notificación de que se ha completado la llamada de procesamiento.
1. Otra vista, la vista de detalles de tareas, escucha este evento desde el modelo de tareas.
1. La vista de detalles de la tarea cambia la plantilla de detalles de la tarea para mostrar la tarea procesada (formulario, detalles, datos adjuntos, notas, etc.) al usuario.

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
