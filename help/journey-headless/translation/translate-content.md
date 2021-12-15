---
title: Traducir contenido
description: Utilice el conector de traducción y las reglas para traducir el contenido sin encabezado.
index: true
hide: false
hidefromtoc: false
source-git-commit: 7cf68868e0963930bde9fcda647822a03914b61d
workflow-type: tm+mt
source-wordcount: '2174'
ht-degree: 0%

---

# Traducir contenido {#translate-content}

Utilice el conector de traducción y las reglas para traducir el contenido sin encabezado.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de traducción sin AEM, [Configurar reglas de traducción](translation-rules.md) ha aprendido a utilizar AEM reglas de traducción para identificar el contenido de traducción. Ahora debería:

* Comprender lo que hacen las reglas de traducción.
* Puede definir sus propias reglas de traducción.

Ahora que sus reglas de conector y traducciones están configuradas, este artículo le guía por el siguiente paso de traducir su contenido sin encabezado.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo utilizar AEM proyectos de traducción junto con el conector y las reglas de traducción para traducir contenido. Después de leer este documento, debe:

* Comprender qué es un proyecto de traducción.
* Poder crear nuevos proyectos de traducción.
* Utilice proyectos de traducción para traducir el contenido sin encabezado.

## Creación de un proyecto de traducción {#creating-translation-project}

Los proyectos de traducción permiten administrar la traducción de contenido AEM sin encabezado. Un proyecto de traducción reúne el contenido que se traduce a otros idiomas en una ubicación para obtener una visión central del esfuerzo de traducción.

Cuando se añade contenido a un proyecto de traducción, se crea un trabajo de traducción para él. Los trabajos proporcionan comandos e información de estado que se utilizan para administrar los flujos de trabajo de traducción humana y traducción automática que se ejecutan en los recursos.

Los proyectos de traducción se pueden crear de dos formas:

1. Seleccione la raíz de idioma del contenido y AEM crear automáticamente el proyecto de traducción en función de la ruta de contenido.
1. Cree un proyecto vacío y seleccione manualmente el contenido que desee añadir al proyecto de traducción

Ambos son enfoques válidos normalmente solo difieren según el usuario que realice la traducción:

* El administrador de proyectos de traducción (TPM) suele necesitar la flexibilidad de seleccionar manualmente el contenido en el proyecto de traducción.
* Si el propietario del contenido también es responsable de la traducción, AEM crear automáticamente el proyecto en función de la ruta de contenido seleccionada suele ser más fácil.

Ambos enfoques se analizan en las secciones siguientes.

### Creación automática de un proyecto de traducción basado en la ruta de contenido {#automatically-creating}

Para los propietarios de contenido que también son responsables de la traducción, a menudo es más fácil tener AEM crear automáticamente el proyecto de traducción. Para AEM crear automáticamente un proyecto de traducción basado en la ruta de contenido:

1. Vaya a **Navegación** -> **Recursos** -> **Archivos**. Recuerde que el contenido sin encabezado de AEM se almacena como recursos conocidos como fragmentos de contenido.
1. Seleccione la raíz de idioma del proyecto. En este caso, se ha seleccionado `/content/dam/wknd/en`.
1. Toque o haga clic en el selector de raíl y muestre el **Referencias** panel.
1. Toque o haga clic en **Copias de idioma**.
1. Marque la **Copias de idioma** casilla de verificación.
1. Expanda la sección . **Actualizar copias de idioma** en la parte inferior del panel de referencias.
1. En el **Proyecto** menú desplegable, seleccione **Crear proyecto de traducción**.
1. Proporcione un título adecuado para el proyecto de traducción.
1. Toque o haga clic **Inicio**.

![Crear un proyecto de traducción](assets/create-translation-project.png)

Recibe un mensaje que indica que el proyecto se creó.

>[!NOTE]
>
>Se supone que ya se ha creado la estructura lingüística necesaria para los idiomas de traducción como parte del [definición de la estructura de contenido.](getting-started.md#content-structure) Esto debería hacerse en colaboración con el arquitecto de contenido.
>
>Si las carpetas de idioma no se crean con antelación, no podrá crear copias de idioma como se describió en los pasos anteriores.

### Creación manual de un proyecto de traducción seleccionando su contenido {#manually-creating}

Para los administradores de proyectos de traducción, a menudo es necesario seleccionar manualmente contenido específico para incluirlo en un proyecto de traducción. Para crear un proyecto de traducción manual de este tipo, debe empezar creando un proyecto vacío y luego seleccionar el contenido que desea añadir.

1. Vaya a **Navegación** -> **Proyectos**.
1. Toque o haga clic **Crear** -> **Carpeta** para crear una carpeta para sus proyectos.
   * Esto es opcional, pero resulta útil para organizar los esfuerzos de traducción.
1. En el **Crear carpeta** ventana, agregue una **Título** para la carpeta y, a continuación, toque o haga clic en **Crear**.

   ![Crear carpeta de proyecto](assets/create-project-folder.png)

1. Toque o haga clic en la carpeta para abrirla.
1. En la nueva carpeta del proyecto, toque o haga clic en **Crear** -> **Proyecto**.
1. Los proyectos se basan en plantillas. Toque o haga clic en el botón **Proyecto de traducción** plantilla para seleccionarla y, a continuación, toque o haga clic en **Siguiente**.

   ![Seleccionar plantilla de proyecto de traducción](assets/select-translation-project-template.png)

1. En el **Básico** , escriba un nombre para el nuevo proyecto.

   ![Ficha Básico del proyecto](assets/project-basic-tab.png)

1. En el **Avanzadas** utilice la pestaña **Idioma de Target** para seleccionar los idiomas a los que se debe traducir el contenido. Haga clic o pulse **Crear**.

   ![Pestaña Avanzado del proyecto](assets/project-advanced-tab.png)

1. Toque o haga clic **Apertura** en el cuadro de diálogo de confirmación.

   ![Cuadro de diálogo de confirmación del proyecto](assets/project-confirmation-dialog.png)

El proyecto se ha creado, pero no contiene contenido para traducir. La siguiente sección detalla cómo se estructura el proyecto y cómo añadir contenido.

## Uso de un proyecto de traducción {#using-translation-project}

Los proyectos de traducción están diseñados para recopilar todo el contenido y las tareas relacionadas con un esfuerzo de traducción en un solo lugar para que su traducción sea sencilla y fácil de administrar.

Para ver el proyecto de traducción:

1. Vaya a **Navegación** -> **Proyectos**.
1. Toque o haga clic en el proyecto creado en la sección anterior.

![Proyecto de traducción](assets/translation-project.png)

El proyecto se divide en varias tarjetas.

* **Resumen** - Esta tarjeta muestra la información básica del encabezado del proyecto, incluido el propietario, el idioma y el proveedor de traducción.
* **Trabajo de traducción** - Esta tarjeta o estos programas de tarjetas proporcionan una visión general del trabajo de traducción real incluyendo el estado, el número de recursos, etc. Generalmente hay un trabajo por idioma con el código de idioma ISO-2 anexado al nombre del trabajo.
* **Equipo** - Esta tarjeta muestra los usuarios que están colaborando en este proyecto de traducción. Este recorrido no cubre este tema.
* **Tareas** : Tareas adicionales asociadas con la traducción del contenido, como hacer elementos o elementos de flujo de trabajo. Este recorrido no cubre este tema.

El uso de un proyecto de traducción depende de cómo se creó: automáticamente por AEM o manualmente.

### Uso de un proyecto de traducción creado automáticamente {#using-automatic-project}

Al crear automáticamente el proyecto de traducción, AEM evalúa el contenido sin encabezado en la ruta seleccionada en función de las reglas de traducción que definió anteriormente. Basándose en esa evaluación, extrae el contenido que requiere traducción en un nuevo proyecto de traducción.

Para ver el detalle del contenido sin encabezado incluido en este proyecto:

1. Toque o haga clic en el botón de puntos suspensivos en la parte inferior del **Trabajo de traducción** tarjeta.
1. La variable **Trabajo de traducción** lista todos los elementos del trabajo.
   ![Detalles del trabajo de traducción](assets/translation-job-detail.png)
1. Toque o haga clic en una línea para ver el detalle de esa línea, teniendo en cuenta que una línea puede representar varios elementos de contenido para traducir.
1. Toque o haga clic en la casilla de verificación de selección de un elemento de línea para ver más opciones, como la opción de eliminarlo del trabajo o verlo en las consolas Fragmentos de contenido o Recursos .
   ![Opciones de trabajo de traducción](assets/translation-job-options.png)

Normalmente, el contenido del trabajo de traducción se inicia en el **Borrador** tal como indica el **Estado** en la columna **Trabajo de traducción** ventana.

Para iniciar el trabajo de traducción, vuelva a la descripción general del proyecto de traducción y toque o haga clic en el botón de cheurón en la parte superior del **Trabajo de traducción** tarjeta y seleccione **Inicio**.

![Iniciar trabajo de traducción](assets/start-translation-job.png)

AEM ahora se comunica con la configuración de traducción y el conector para enviar el contenido al servicio de traducción. Para ver el progreso de la traducción, vuelva al **Trabajo de traducción** ventana y visualización del **Estado** de las entradas.

![Trabajo de traducción aprobado](assets/translation-job-approved.png)

Las traducciones automáticas se devuelven automáticamente con un estado de **Aprobado**. La traducción humana permite una mayor interacción, pero está fuera del alcance de este recorrido.

### Uso de un proyecto de traducción creado manualmente {#using-manual-project}

Al crear manualmente un proyecto de traducción, AEM crea los trabajos necesarios, pero no selecciona automáticamente ningún contenido que se deba incluir. Esto permite al administrador del proyecto de traducción tener la flexibilidad de elegir qué contenido traducir.

Para añadir contenido a un trabajo de traducción:

1. Toque o haga clic en el botón de puntos suspensivos en la parte inferior de uno de los **Trabajo de traducción** tarjetas.
1. Compruebe que el trabajo no contenga contenido. Toque o haga clic en el botón **Agregar** en la parte superior de la ventana y, a continuación, **Recursos/Páginas** en la lista desplegable .

   ![Trabajo de traducción vacío](assets/empty-translation-job.png)

1. Se abre un navegador de rutas que le permite seleccionar específicamente qué contenido añadir. Busque el contenido y toque o haga clic para seleccionarlo.

   ![Navegador de rutas](assets/path-browser.png)

1. Toque o haga clic **Select** para añadir el contenido seleccionado al trabajo.
1. En el **Traducir** , especifique que desea **Crear copia de idioma**.

   ![Crear copia de idioma](assets/translate-copy-master.png)

1. El contenido ahora se incluye en el trabajo.

   ![Contenido añadido al trabajo de traducción](assets/content-added.png)

1. Toque o haga clic en la casilla de verificación de selección de un elemento de línea para ver más opciones, como la opción de eliminarlo del trabajo o verlo en las consolas Fragmentos de contenido o Recursos .
   ![Opciones de trabajo de traducción](assets/translation-job-options-manual.png)

1. Repita estos pasos para incluir todo el contenido necesario en el trabajo.

>[!TIP]
>
>El navegador de rutas es una potente herramienta que le permite buscar, filtrar y navegar por el contenido. Toque o haga clic en el botón **Solo contenido/Filtros** para alternar el panel lateral y mostrar filtros avanzados como **Fecha de modificación** o **Estado de traducción**.
>
>Puede obtener más información sobre el explorador de rutas en la [recursos adicionales .](#additional-resources)

Puede utilizar los pasos anteriores para agregar el contenido necesario a todos los idiomas (trabajos) del proyecto. Una vez que haya seleccionado todo el contenido, puede iniciar la traducción.

Normalmente, el contenido del trabajo de traducción se inicia en el **Borrador** tal como indica el **Estado** en la columna **Trabajo de traducción** ventana.

Para iniciar el trabajo de traducción, vuelva a la descripción general del proyecto de traducción y toque o haga clic en el botón de cheurón en la parte superior del **Trabajo de traducción** tarjeta y seleccione **Inicio**.

![Iniciar trabajo de traducción](assets/start-translation-job-manual.png)

AEM ahora se comunica con la configuración de traducción y el conector para enviar el contenido al servicio de traducción. Para ver el progreso de la traducción, vuelva al **Trabajo de traducción** ventana y visualización del **Estado** de las entradas.

![Trabajo de traducción aprobado](assets/translation-job-approved-manual.png)

Las traducciones automáticas se devuelven automáticamente con un estado de **Aprobado**. La traducción humana permite una mayor interacción, pero está fuera del alcance de este recorrido.

## Revisión del contenido traducido {#reviewing}

[Como se ha visto anteriormente,](#using-translation-project) el contenido traducido por el equipo vuelve a AEM con el estado de **Aprobado** dado que se supone que como se está utilizando la traducción automática, no se requiere ninguna intervención humana. Sin embargo, por supuesto que todavía es posible revisar el contenido traducido.

Simplemente vaya al trabajo de traducción completado y seleccione un elemento de línea tocando o haciendo clic en la casilla de verificación. El icono **Mostrar en fragmento de contenido** se muestra en la barra de herramientas.

![Mostrar en fragmento de contenido](assets/reveal-in-content-fragment.png)

Toque o haga clic en ese icono para abrir el fragmento de contenido traducido en su consola de editor para ver los detalles del contenido traducido.

![Un fragmento de contenido traducido](assets/translated-content-fragment.png)

Puede modificar el fragmento de contenido según sea necesario, siempre que tenga el permiso adecuado, pero la edición de fragmentos de contenido está fuera del ámbito de este recorrido. Consulte la [Recursos adicionales](#additional-resources) al final de este documento para obtener más información sobre este tema.

El propósito del proyecto es reunir todos los recursos relacionados con una traducción en un solo lugar para facilitar el acceso y una visión general clara. Sin embargo, como puede ver viendo el detalle de un elemento traducido, las traducciones en sí mismas regresan a la carpeta de recursos del idioma de traducción. En este ejemplo, la carpeta es

```text
/content/dam/wknd/es
```

Si va a esta carpeta mediante **Navegación** -> **Recursos** -> **Archivos**, verá el contenido traducido.

![Estructura de carpetas de contenido traducida](assets/translated-file-content.png)

AEM marco de traducción recibe las traducciones del conector de traducción y, a continuación, crea automáticamente la estructura de contenido en función de la raíz del idioma y utilizando las traducciones proporcionadas por el conector.

Es importante comprender que este contenido no se publica y, por lo tanto, no está disponible para los servicios sin encabezado. Aprenderemos sobre esta estructura de creación y publicación y veremos cómo publicar nuestro contenido traducido en el siguiente paso del recorrido de traducción.

## Traducción humana {#human-translation}

Si el servicio de traducción proporciona traducción humana, el proceso de revisión ofrece más opciones. Por ejemplo, las traducciones vuelven al proyecto con el estado . **Borrador** y deben revisarse y aprobarse o rechazarse manualmente.

La traducción humana está fuera del alcance de este recorrido de localización. Consulte la [Recursos adicionales](#additional-resources) al final de este documento para obtener más información sobre este tema. Sin embargo, más allá de las opciones de aprobación adicionales, el flujo de trabajo para las traducciones humanas es el mismo que las traducciones automáticas, tal como se describe en este recorrido.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido de traducción sin encabezado, debe:

* Comprender qué es un proyecto de traducción.
* Poder crear nuevos proyectos de traducción.
* Utilice proyectos de traducción para traducir el contenido sin encabezado.

Aproveche este conocimiento y continúe su recorrido de traducción sin AEM cabeza revisando el documento [Publicar contenido traducido](publish-content.md) donde aprenderá a publicar su contenido traducido y a actualizar esas traducciones a medida que cambie su contenido raíz de idioma.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de traducción sin encabezado revisando el documento [Publicar contenido traducido,](publish-content.md) los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no son necesarios para continuar en el recorrido sin encabezado.

* [Administración de proyectos de traducción](/help/sites-administering/tc-manage.md) : Conozca los detalles de los proyectos de traducción y las funciones adicionales, como flujos de trabajo de traducción humana y proyectos en varios idiomas.
* [Herramientas y entorno de creación](/help/sites-authoring/author-environment-tools.md##path-selection) : AEM ofrece varios mecanismos para organizar y editar el contenido, incluido un navegador de rutas robusto.
