---
title: La consola Componentes
seo-title: La consola Componentes
description: La consola Componentes
seo-description: nulo
uuid: a4e34d81-7875-4e26-8b48-4473e2905c37
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: b657f95d-7be3-4409-a31b-d47fb2bfa550
docset: aem65
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# La consola Componentes{#components-console}

La consola Componentes permite examinar todos los componentes definidos para la instancia y ver información clave de cada componente.

Se puede acceder a ella desde **Herramientas ->** **General ->** **Componentes**. En la consola, están disponibles la vista de tarjeta y la vista de lista. Como no hay una estructura de árbol para los componentes, la vista de columna no está disponible.

![screen-shot_2019-03-05at113145](assets/screen-shot_2019-03-05at113145.png)

>[!NOTE]
>
>La consola Componentes muestra todos los componentes en el sistema. El [navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser) muestra los componentes disponibles para los autores y oculta cualquier grupo de componentes que comience con un punto ( `.`).

## Búsqueda {#searching}

Con el icono **Solo contenido** (parte superior izquierda) podrá abrir el panel **Buscar** para buscar o para filtrar los componentes: 

![screen-shot_2019-03-05at113251](assets/screen-shot_2019-03-05at113251.png)

### Detalles de los componentes {#component-details}

Para ver los detalles de un componente específico, toque o haga clic en el recurso necesario. Encontrará lo siguiente en tres fichas:

* **Propiedades**

   ![screen_shot_2018-03-27at165847](assets/screen_shot_2018-03-27at165847.png)

   En la pestaña Propiedades puede:

   * Consulte las propiedades generales del componente.
   * Ver cómo [se ha definido el icono o la abreviatura](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) para el componente.

      * Si hace clic en el origen del icono, se le dirigirá a dicho componente.
   * Ver el **tipo de recurso** y el **supertipo de recurso** (si está definido) para el componente.

      * Si hace clic en el supertipo de recurso, se le dirigirá a dicho componente.
   >[!NOTE]
   >
   >Debido a que `/apps` no se puede editar en el tiempo de ejecución, la consola Componentes es de solo lectura.

* **Políticas**

   ![chlimage_1-169](assets/chlimage_1-169.png)

* **Uso de Live**

   ![chlimage_1-170](assets/chlimage_1-170.png)

   >[!CAUTION]
   >
   >Dada la naturaleza de la información recopilada para esta vista, puede tardar un rato en recopilarse o mostrarse. 

* **Documentación**

   Si el desarrollador ha proporcionado [documentación del componente](/help/sites-developing/developing-components.md#documenting-your-component), esta aparecerá en la pestaña **Documentación**. Si no hay documentación disponible, no se mostrará la pestaña **Documentación.**

   ![chlimage_1-171](assets/chlimage_1-171.png)

