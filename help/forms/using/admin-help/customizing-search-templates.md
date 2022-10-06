---
title: Personalización de plantillas de búsqueda
seo-title: Customizing search templates
description: Puede crear plantillas de búsqueda para usarlas en Workspace para buscar instancias de procesos en las páginas Tareas pendientes y Seguimiento. También puede editar o eliminar las plantillas de búsqueda existentes.
seo-description: You can create search templates to be used in Workspace to search for instances of processes from the To Do and Tracking pages. You can also edit or delete existing search templates.
uuid: 2043ba8a-07f0-4054-af3c-f3a14c2183ab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6e4b4dfa-3af5-4c21-a2a1-b90ef02d8514
exl-id: bf69de86-2ca6-4d21-936c-07c1debacfa0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# Personalización de plantillas de búsqueda {#customizing-search-templates}

Puede crear plantillas de búsqueda para usarlas en Workspace para buscar instancias de procesos en las páginas Tareas pendientes y Seguimiento. También puede editar o eliminar las plantillas de búsqueda existentes.

Al crear o editar una plantilla de búsqueda, puede especificar el diseño y el orden de los resultados de la búsqueda. Sin embargo, los usuarios pueden modificar esta configuración en Workspace después de que aparezcan los resultados de la búsqueda.

Puede crear tantas plantillas de búsqueda como sea necesario.

>[!NOTE]
>
>Al guardar una plantilla de búsqueda, debe darle un nombre único. De lo contrario, una plantilla existente se puede sobrescribir sin un mensaje de advertencia.

## Crear una plantilla de búsqueda simple {#create-a-simple-search-template}

1. En la consola de administración, haga clic en Servicios > Workspace > Buscar plantillas.
1. En la ficha Identificación, en el cuadro Descripción de la plantilla de búsqueda , indique el propósito de la plantilla.
1. (Opcional) Haga clic en la pestaña Criterios y especifique los criterios de búsqueda para la plantilla.
1. Haga clic en la ficha Guardar, escriba un nombre único para la plantilla y, a continuación, haga clic en Guardar.

## Crear o editar una plantilla de búsqueda {#create-or-edit-a-search-template}

1. En la consola de administración, haga clic en Servicios > Workspace > Buscar plantillas.
1. (Opcional) Si está editando una plantilla existente o utilizando una plantilla existente como base para una plantilla nueva, seleccione la plantilla en la lista Buscar nombre de plantilla .
1. En el cuadro Buscar descripción de plantilla , indique el propósito de la plantilla.
1. (Opcional) En el cuadro Instrucciones del usuario, proporcione las instrucciones que puedan ayudarle a usar la plantilla. Estas instrucciones se muestran en Workspace cuando un usuario selecciona la plantilla de búsqueda.
1. Haga clic en la ficha Criterios . Aquí es donde define uno o más criterios de búsqueda. Para agregar un criterio de búsqueda:

   * En la parte superior de la ficha Criterios, seleccione un elemento de proceso o un elemento de tarea.

      **Sugerencia**: *Si previamente seleccionó el elemento Nombre del proceso y especificó un proceso, también se podrán seleccionar las variables de proceso definidas en ese proceso.*

      **Sugerencia**: *Si selecciona el elemento Tarea visible , los usuarios podrán eliminar las tareas completadas de los resultados de búsqueda.*

      Los campos de criterios de búsqueda para el elemento seleccionado aparecen en la parte inferior de la pestaña Criterios .

   * Para cada elemento de proceso, elemento de tarea y variable de proceso que seleccione, rellene los campos de búsqueda correspondientes en la parte inferior de la pestaña Criterios:

      * Seleccione un operador relacional (como &quot;ser igual a&quot;) en la lista proporcionada y especifique el valor del operando en el cuadro que se encuentra junto a él.
      * (Opcional) Para permitir que los usuarios cambien el valor del operando en Workspace, seleccione Permitir que el usuario cambie el operando.
      * (Opcional) Para permitir que los usuarios cambien el operador relacional, seleccione Permitir que el usuario seleccione otro operador relacional. En la lista que aparece, seleccione los operadores que estarán disponibles para el usuario.

      **Sugerencia**: *Si ha seleccionado Nombre del proceso como elemento, puede hacer clic en el icono situado junto al campo de operando para mostrar una lista en la que puede seleccionar un proceso que se esté ejecutando en el servidor de formularios. Después de seleccionar un proceso, las variables de proceso definidas en ese proceso se pueden seleccionar en Variables de proceso , en la sección superior de la pestaña Criterios .*

      **Sugerencia**: *Puede eliminar un elemento de la plantilla de búsqueda haciendo clic en el icono Eliminar situado junto a los criterios de búsqueda del elemento.*


1. (Opcional) Para que cada encabezado de columna se muestre en los resultados de la búsqueda, haga clic en la ficha Diseño y realice los siguientes pasos:

   * Seleccione un elemento de proceso o tarea y haga clic en la flecha derecha para moverlo a la lista Columnas a informe .
   * En la lista Columnas a informe, seleccione el elemento de proceso o tarea y haga clic en las flechas arriba o abajo para moverlo a su lugar en el orden de las columnas. Los encabezados de columna de los resultados de búsqueda aparecerán en el orden en que aparecen aquí.
   * (Opcional) Para cambiar el nombre del elemento para el encabezado de columna, seleccione el elemento en la lista Columnas a informe y proporcione el nuevo nombre.

   >[!NOTE]
   >
   >El diseño especificado en la plantilla de búsqueda anula las preferencias del usuario especificadas para los encabezados de columna en Workspace.

1. (Opcional) Para que cada columna clasifique en los resultados de la búsqueda, haga clic en la ficha Ordenar y realice los siguientes pasos:

   * Seleccione un elemento de proceso o tarea y haga clic en la flecha derecha para moverlo a la lista Orden.
   * En la lista Orden, seleccione el elemento de proceso o tarea y haga clic en las flechas arriba o abajo para moverlo a su lugar en el orden de clasificación. Las columnas de los resultados de búsqueda se ordenarán en función del orden en que aparezcan en la lista.
   * (Opcional) Para ordenar una columna en orden descendente, active la casilla de verificación situada junto al nombre del elemento. Si la casilla de verificación no está seleccionada, la columna se ordena en orden ascendente.

1. Haga clic en la ficha Guardar .
1. (Opcional) Si crea una nueva plantilla de búsqueda, asígnele un nombre único. Si no especifica un nombre único, puede sobrescribir una plantilla existente.
1. Haga clic en el botón Save .

## Eliminar una plantilla de búsqueda {#delete-a-search-template}

1. En la ficha Identificación, seleccione un nombre de la lista Buscar nombre de plantilla .
1. Haga clic en Eliminar esta plantilla y en Aceptar.
