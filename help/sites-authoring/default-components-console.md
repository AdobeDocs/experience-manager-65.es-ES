---
title: Consola Componentes
description: La consola Componentes permite examinar todos los componentes definidos para la instancia y ver información clave de cada componente.
exl-id: d79107b9-dfa4-4e80-870e-0b7ea72f0bc7
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 51%

---

# Consola Componentes{#components-console}

La consola Componentes permite examinar todos los componentes definidos para la instancia y ver información clave de cada componente.

Se puede acceder a ella desde **Herramientas ->** **General ->** **Componentes**. En la consola, están disponibles la vista de tarjeta y la vista de lista. Como no hay una estructura de árbol para los componentes, la vista de columna no está disponible.

![screen-shot_2019-03-05at113145](assets/screen-shot_2019-03-05at113145.png)

>[!NOTE]
>
>La consola Componentes muestra todos los componentes del sistema. El [navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser) muestra los componentes disponibles para los autores y oculta cualquier grupo de componentes que comience con un punto ( `.`).

## Búsqueda {#searching}

Con el icono **Solo contenido** (parte superior izquierda) podrá abrir el panel **Buscar** para buscar o para filtrar los componentes: 

![screen-shot_2019-03-05at113251](assets/screen-shot_2019-03-05at113251.png)

### Detalles de los componentes {#component-details}

Para ver los detalles de un componente específico, toque o haga clic en el recurso requerido. Hay tres pestañas que proporcionan:

* **Propiedades**

  ![screen_shot_2018-03-27at165847](assets/screen_shot_2018-03-27at165847.png)

  En la pestaña Propiedades puede:

   * Consulte las propiedades generales del componente.
   * Ver cómo se [se ha definido un icono o una abreviatura](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) para el componente.

      * Al hacer clic en el origen del icono, se le dirigirá a ese componente.

   * Ver el **Tipo de medio** y **Supertipo de recurso** (si se define) para el componente.

      * Al hacer clic en el supertipo de recurso, accederá a ese componente.

  >[!NOTE]
  >
  >Debido a que `/apps` no se puede editar en el tiempo de ejecución, la consola Componentes es de solo lectura.

* **Políticas**

  ![Políticas](assets/chlimage_1-169.png)

* **Uso de Live**

  ![Uso de Live](assets/chlimage_1-170.png)

  >[!CAUTION]
  >
  >Dada la naturaleza de la información recopilada para esta vista, puede tardar un rato en recopilarse o mostrarse. 

* **Documentación**

  Si el desarrollador ha proporcionado [documentación del componente](/help/sites-developing/developing-components.md#documenting-your-component), aparecerá en la **Documentación** pestaña. Si no hay documentación disponible, no se mostrará la pestaña **Documentación.**

  ![Documentación](assets/chlimage_1-171.png)
