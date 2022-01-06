---
title: Publicar contenido traducido
description: Aprenda a publicar el contenido traducido y a actualizar las traducciones como actualizaciones de contenido.
source-git-commit: 38525b6cc14e9f6025564c060b8cfb4f9e0ea473
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 0%

---

# Publicar contenido traducido {#publish-content}

Aprenda a publicar el contenido traducido y a actualizar las traducciones como actualizaciones de contenido.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de traducción sin AEM, [Traducir contenido,](configure-connector.md) ha aprendido a utilizar AEM proyectos de traducción para traducir su contenido sin encabezado. Ahora debería:

* Comprender qué es un proyecto de traducción.
* Poder crear nuevos proyectos de traducción.
* Utilice proyectos de traducción para traducir el contenido sin encabezado.

Ahora que la traducción inicial ha finalizado, este artículo le explica el siguiente paso para publicar ese contenido y qué hacer para actualizar sus traducciones como el contenido subyacente en la raíz del idioma cambia.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo publicar contenido sin encabezado en AEM y cómo crear un flujo de trabajo continuo para mantener las traducciones actualizadas. Después de leer este documento, debe:

* Comprender el modelo de creación y publicación de AEM.
* Obtenga información sobre cómo publicar el contenido traducido.
* Puede implementar un modelo de actualización continua para el contenido traducido.

## Modelo de AEM Author-Publish {#author-publish}

Antes de publicar el contenido, es aconsejable comprender AEM modelo de creación y publicación. En términos simplificados, AEM divide a los usuarios del sistema en dos grupos.

1. Aquellos que crean y administran el contenido y el sistema
1. Aquellos que consumen el contenido del sistema

Por lo tanto, AEM se separa físicamente en dos instancias.

1. La variable **author** es el sistema donde los autores y administradores de contenido trabajan para crear y administrar contenido.
1. La variable **publicar** es el sistema que envía el contenido a los consumidores.

Una vez creado el contenido en la instancia de autor, debe transferirse a la instancia de publicación para que esté disponible para el consumo. Se llama al proceso de transferencia del autor a la publicación **publicación**.

## Publicación del contenido traducido {#publishing}

Una vez que esté satisfecho con el estado del contenido traducido, debe publicarse para que los servicios sin periféricos puedan consumirlo. Esta tarea no suele ser responsabilidad del especialista en traducción, pero se documenta aquí para ilustrar el flujo de trabajo completo.

>[!NOTE]
>
>Por lo general, cuando se completa la traducción, el especialista en traducciones informa a los propietarios de los contenidos de que las traducciones están listas para su publicación. A continuación, los propietarios de contenido los publican.
>
>Se proporcionan los siguientes pasos para que sean completos.

La forma más sencilla de publicar las traducciones es navegar a la carpeta de recursos del proyecto.

```text
/content/dam/<your-project>/
```

En esta ruta tiene subcarpetas para cada idioma de traducción y puede elegir cuál publicar.

1. Vaya a **Navegación** -> **Recursos** -> **Archivos** y abra la carpeta del proyecto.
1. Aquí puede ver la carpeta raíz del idioma y todas las demás carpetas del idioma. Seleccione el idioma o los idiomas localizados que desee publicar.
   ![Seleccionar carpeta de idioma](assets/select-language-folder.png)
1. Toque o haga clic **Administrar publicación**.
1. En el **Administrar publicación** , asegúrese de que **Publicación** se selecciona automáticamente en **Acción** y **Ahora** se selecciona en **Programación**. Haga clic o pulse **Siguiente**.
   ![Administrar opciones de publicación](assets/manage-publication-options.png)
1. En el siguiente **Administrar publicación** , confirme que la ruta o rutas correctas están seleccionadas. Toque o haga clic **Publicación**.
   ![Administrar ámbito de publicación](assets/manage-publication-scope.png)
1. AEM confirma la acción de publicación con un mensaje emergente en la parte superior de la pantalla.
   ![Pancarta publicada de recursos](assets/resources-published-message.png)

El contenido traducido sin encabezado ya está publicado. Ahora puede ser accedido y consumido por sus servicios sin periféricos.

>[!TIP]
>
>Puede seleccionar varios elementos (es decir, carpetas de varios idiomas) al publicar para publicar varias traducciones al mismo tiempo.

Existen opciones adicionales al publicar el contenido, como programar una hora de publicación, que están fuera del ámbito de este recorrido. Consulte la [Recursos adicionales](#additional-resources) al final del documento para obtener más información.

## Actualización del contenido traducido {#updating-translations}

La traducción rara vez es un ejercicio excepcional. Normalmente, los autores de contenido siguen agregando y modificando el contenido en la raíz del idioma una vez completada la traducción inicial. Esto significa que también debe actualizar el contenido traducido.

Los requisitos específicos del proyecto definen la frecuencia con la que debe actualizar las traducciones y qué proceso de decisión se sigue antes de realizar una actualización. Una vez que haya decidido actualizar sus traducciones, el proceso en AEM es muy sencillo. Como la traducción inicial se basó en un proyecto de traducción, también lo son las actualizaciones.

Sin embargo, como antes, el proceso difiere ligeramente si elige crear automáticamente el proyecto de traducción o crear manualmente el proyecto de traducción.

### Actualización de un proyecto de traducción creado automáticamente {#updating-automatic-project}

1. Vaya a **Navegación** -> **Recursos** -> **Archivos**. Recuerde que el contenido sin encabezado de AEM se almacena como recursos conocidos como fragmentos de contenido.
1. Seleccione la raíz de idioma del proyecto. En este caso, se ha seleccionado `/content/dam/wknd/en`.
1. Toque o haga clic en el selector de raíl y muestre el **Referencias** panel.
1. Toque o haga clic en **Copias de idioma**.
1. Marque la **Copias de idioma** casilla de verificación.
1. Expanda la sección . **Actualizar copias de idioma** en la parte inferior del panel de referencias.
1. En el **Proyecto** menú desplegable, seleccione **Agregar a un proyecto de traducción existente**.
1. En el **Proyecto de traducción existente** , seleccione el proyecto creado para la traducción inicial.
1. Toque o haga clic **Inicio**.

![Agregar elementos a un proyecto de traducción existente](assets/add-to-existing-project.png)

El contenido se agrega al proyecto de traducción existente. Para ver el proyecto de traducción:

1. Vaya a **Navegación** -> **Proyectos**.
1. Toque o haga clic en el proyecto que acaba de actualizar.
1. Toque o haga clic en el idioma o en uno de los idiomas que ha actualizado.

Verá que se agregan nuevas tarjetas de trabajo al proyecto según corresponda.

<!--
You see that a new job card was added to the project. In this example, another Spanish translation was added.

![Additional translation job added](assets/additional-translation-job.png)
-->

Puede observar que las estadísticas que aparecen en la nueva tarjeta (número de recursos y fragmentos de contenido) son diferentes. Esto se debe a que AEM reconoce qué ha cambiado desde la última traducción y solo incluye el contenido que debe traducirse. Esto incluye la retraducción del contenido actualizado, así como la primera traducción del contenido nuevo.

A partir de este punto, [inicie y administre su trabajo de traducción igual que hizo el original.](translate-content.md#using-translation-project)

### Actualización de un proyecto de traducción creado manualmente {#updating-manual-project}

Para actualizar una traducción, puede agregar un nuevo trabajo al proyecto existente que sea responsable de traducir el contenido actualizado.

1. Vaya a **Navegación** -> **Proyectos**.
1. Toque o haga clic en el proyecto que debe actualizar.
1. Toque o haga clic en el botón **Agregar** en la parte superior de la ventana.
1. En el **Agregar mosaico** ventana, toque o haga clic **Trabajo de traducción** y luego **Submit**.

   ![Agregar mosaico](assets/add-translation-job-tile.png)

1. En la tarjeta del nuevo trabajo de traducción, pulse o haga clic en el botón de cheurón en la parte superior de la tarjeta y seleccione **Actualizar Target** para definir el idioma de destino del nuevo trabajo.

   ![Actualizar destino](assets/update-target.png)

1. En el **Seleccionar idioma de destino** , utilice la lista desplegable para seleccionar el idioma y toque o haga clic en **Listo**.

   ![Seleccionar idioma de destino](assets/select-target-language.png)

1. Una vez configurado el idioma de destino del nuevo trabajo de traducción, toque o haga clic en el botón de puntos suspensivos en la parte inferior de la tarjeta de trabajo para ver los detalles del trabajo.
1. El trabajo está vacío la primera vez que se crea. Agregue contenido al trabajo tocando o haciendo clic en el botón **Agregar** y utilizando el explorador de rutas [como hacía antes al crear originalmente el proyecto de traducción.](translate-content.md##manually-creating)

>[!TIP]
>
>Los poderosos filtros del navegador de rutas pueden ser útiles de nuevo para encontrar solo el contenido que se ha actualizado.
>
>Puede obtener más información sobre el explorador de rutas en la [recursos adicionales .](#additional-resources)

A partir de este punto, [inicie y administre su trabajo de traducción igual que hizo el original.](translate-content.md#using-translation-project)

## ¿Fin del Recorrido? {#end-of-journey}

Felicitaciones! ¡Ha completado el recorrido de traducción sin periféricos! Ahora debería:

* Obtenga información general sobre qué es la entrega de contenido sin encabezado.
* Tenga una comprensión básica AEM las funciones sin encabezado.
* Comprenda AEM funciones de traducción y cómo se relacionan con contenido sin encabezado.
* Tener la capacidad de empezar a traducir su propio contenido sin encabezado.

Ahora está listo para traducir su propio contenido sin encabezado en AEM. Sin embargo, AEM es una herramienta potente y hay muchas opciones adicionales disponibles. Consulte algunos de los recursos adicionales disponibles en la [Sección Recursos adicionales](#additional-resources) para obtener más información sobre las funciones que ha visto en este recorrido.

## Recursos adicionales {#additional-resources}

* [Administración de proyectos de traducción](/help/sites-administering/tc-manage.md) : Conozca los detalles de los proyectos de traducción y las funciones adicionales, como flujos de trabajo de traducción humana y proyectos en varios idiomas.
* [Conceptos de creación](/help/sites-authoring/author.md) - Obtenga más información sobre el modelo de autor y publicación de AEM en más detalle. Este documento se centra en la creación de páginas en lugar de en los fragmentos de contenido, pero la teoría sigue aplicándose.
* [Publicación de páginas](/help/sites-authoring/publishing-pages.md) : Obtenga información sobre las funciones adicionales disponibles al publicar contenido. Este documento se centra en la creación de páginas en lugar de en los fragmentos de contenido, pero la teoría sigue aplicándose.
* [Herramientas y entorno de creación](/help/sites-authoring/author-environment-tools.md##path-selection) : AEM ofrece varios mecanismos para organizar y editar el contenido, incluido un navegador de rutas robusto.
