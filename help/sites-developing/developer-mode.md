---
title: Modo de desarrollador
seo-title: Modo de desarrollador
description: El modo de desarrollador abre un panel lateral con varias fichas que proporcionan a los desarrolladores información sobre la página actual
seo-description: El modo de desarrollador abre un panel lateral con varias fichas que proporcionan a los desarrolladores información sobre la página actual
uuid: 8301ab51-93d6-44f9-a813-ba7f03f54485
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 589e3a83-7d1a-43fd-98b7-3b947122829d
docset: aem65
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---


# Modo de desarrollador{#developer-mode}

Al editar páginas en AEM, hay varios [modos](/help/sites-authoring/author-environment-tools.md#modestouchoptimizedui) disponibles, incluido el modo de desarrollador. Esto abre un panel lateral con varias fichas que proporcionan a un desarrollador información sobre la página actual. Las tres fichas son:

* **[](#components)** Componentes para ver la información de estructura y rendimiento.
* **[](#tests)** Pruebas para ejecutar pruebas y analizar los resultados.
* **[](#errors)** Errores para ver si se producen problemas.

Esto ayuda a los desarrolladores a:

* Discover: de qué páginas se componen.
* Depurar: lo que está sucediendo, dónde y cuándo, lo que a su vez ayuda a resolver los problemas.
* Prueba: ¿Se comporta la aplicación como se espera?

>[!CAUTION]
>
>Modo de desarrollador:
>
>* Solo está disponible en la IU táctil (al editar páginas).
>* No está disponible en dispositivos móviles o ventanas pequeñas en el escritorio (debido a restricciones de espacio).

   >
   >   
   * Esto ocurre cuando la anchura es inferior a 1024 píxeles.
>* Solo está disponible para los usuarios que son miembros del grupo `administrators`.


>[!CAUTION]
>
>El modo de desarrollador solo está disponible en una instancia de autor estándar que no utilice el modo de ejecución nosamplecontent.
>
>Si es necesario, puede configurarse para su uso:
>
>* en una instancia de autor mediante nosamplecontent run-mode
>* una instancia de publicación

>
>
Debe deshabilitarse de nuevo después de su uso.

>[!NOTE]
>
>Consulte:
>
>* Artículo de la Base de conocimiento, [Solución de problemas de AEM TouchUI](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html), para obtener más sugerencias y herramientas.
>* AEM sesión de Gems sobre [AEM 6.0 Developer Mode](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html).

>



## Apertura del modo de desarrollador {#opening-developer-mode}

El modo de desarrollador se implementa como un panel lateral en el editor de páginas. Para abrir el panel, seleccione **Desarrollador** en el selector de modo de la barra de herramientas del editor de páginas:

![chlimage_1-11](assets/chlimage_1-11.png)

El panel se divide en dos fichas:

* **[Componentes](/help/sites-developing/developer-mode.md#components)** : Muestra un árbol de componentes, similar al árbol de  [contenido ](/help/sites-authoring/author-environment-tools.md#content-tree) para autores

* **[Errores](/help/sites-developing/developer-mode.md#errors)** : cuando se producen problemas, se muestran detalles para cada componente.

### Componentes {#components}

![chlimage_1-12](assets/chlimage_1-12.png)

Muestra un árbol de componentes que:

* Describe la cadena de componentes y plantillas procesadas en la página (SLY, JSP, etc.). El árbol se puede expandir para mostrar el contexto dentro de la jerarquía.
* Muestra el tiempo de cálculo del lado del servidor necesario para procesar el componente.
* Permite expandir el árbol y seleccionar componentes específicos dentro del árbol. La selección proporciona acceso a los detalles del componente; como:

   * Ruta del repositorio
   * Vínculos a secuencias de comandos (a los que se accede en CRXDE Lite)

* Los componentes seleccionados (en el flujo de contenido, indicados con un borde azul) se resaltarán en el árbol de contenido (y viceversa).

Esto puede ayudar a:

* Determinar y comparar el tiempo de procesamiento por componente.
* Ver y comprender la jerarquía.
* Comprenda y mejore el tiempo de carga de la página buscando componentes lentos.

Cada entrada de componente puede mostrar (por ejemplo):

![chlimage_1-13](assets/chlimage_1-13.png)

* **Detalles** de vista: vínculo a una lista que muestra:

   * todas las secuencias de comandos de componentes utilizadas para procesar el componente.
   * la ruta de contenido del repositorio para este componente específico.

   ![chlimage_1-14](assets/chlimage_1-14.png)

* **Editar secuencia de comandos**: un vínculo que:

   * abre la secuencia de comandos de componente en CRXDE Lite.

* La expansión de una entrada de componente (punta de flecha) también puede mostrar:

   * La jerarquía dentro del componente seleccionado.
   * Tiempos de procesamiento para el componente seleccionado de forma aislada, componentes individuales anidados en él y el total combinado.

   ![chlimage_1-15](assets/chlimage_1-15.png)

>[!CAUTION]
>
>Algunos vínculos apuntan a secuencias de comandos en `/libs`. Sin embargo, sólo para referencia, **no debe** editar nada en `/libs`, ya que cualquier cambio que realice puede perderse. Esto se debe al hecho de que esta rama puede cambiar cada vez que actualice o aplique un paquete de revisión o función. Cualquier cambio que necesite se debe realizar en `/apps`, consulte [Overlays and Overrides](/help/sites-developing/overlays.md).

### Errores {#errors}

![chlimage_1-16](assets/chlimage_1-16.png)

Es de esperar que la ficha **Errors** siempre esté vacía (como se muestra arriba), pero cuando se producen problemas se muestran los siguientes detalles para cada componente:

* Una advertencia si el componente escribe una entrada en el registro de errores, junto con detalles del error y vínculos directos al código apropiado dentro del CRXDE Lite.
* Una advertencia si el componente abre una sesión de administración.

Por ejemplo, en una situación en la que se llama a un método no definido, el error resultante se mostrará en la ficha **Errors**:

![chlimage_1-17](assets/chlimage_1-17.png)

La entrada de componente en el árbol de la ficha Componentes también se marcará con un indicador cuando se produzca un error.

### Pruebas {#tests}

>[!CAUTION]
>
>En AEM 6.2, las funciones de prueba del modo de desarrollador se volvieron a implementar como una aplicación de herramientas independiente.
>
>Para obtener más información, consulte [Prueba de la interfaz de usuario](/help/sites-developing/hobbes.md).

