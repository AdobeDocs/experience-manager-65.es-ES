---
title: Personalización de plantillas de búsqueda
seo-title: Personalización de plantillas de búsqueda
description: Puede crear plantillas de búsqueda que se utilizarán en Workspace para buscar instancias de procesos en las páginas Tareas pendientes y Seguimiento. También puede editar o eliminar las plantillas de búsqueda existentes.
seo-description: Puede crear plantillas de búsqueda que se utilizarán en Workspace para buscar instancias de procesos en las páginas Tareas pendientes y Seguimiento. También puede editar o eliminar las plantillas de búsqueda existentes.
uuid: 2043ba8a-07f0-4054-af3c-f3a14c2183ab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6e4b4dfa-3af5-4c21-a2a1-b90ef02d8514
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Personalización de plantillas de búsqueda {#customizing-search-templates}

Puede crear plantillas de búsqueda que se utilizarán en Workspace para buscar instancias de procesos en las páginas Tareas pendientes y Seguimiento. También puede editar o eliminar las plantillas de búsqueda existentes.

Al crear o editar una plantilla de búsqueda, puede especificar el diseño y el orden de los resultados de la búsqueda. Sin embargo, los usuarios pueden modificar esta configuración en Workspace después de que aparezcan los resultados de la búsqueda.

Puede crear tantas plantillas de búsqueda como sea necesario.

>[!NOTE]
>
>Al guardar una plantilla de búsqueda, debe darle un nombre único. De lo contrario, una plantilla existente se puede sobrescribir sin un mensaje de advertencia.

## Crear una plantilla de búsqueda simple {#create-a-simple-search-template}

1. En la consola de administración, haga clic en Servicios > Espacio de trabajo > Buscar plantillas.
1. En la ficha Identificación, en el cuadro Descripción de la plantilla de búsqueda, especifique el propósito de la plantilla.
1. (Opcional) Haga clic en la ficha Criterios y especifique los criterios de búsqueda de la plantilla.
1. Haga clic en la ficha Guardar, escriba un nombre único para la plantilla y, a continuación, haga clic en Guardar.

## Crear o editar una plantilla de búsqueda {#create-or-edit-a-search-template}

1. En la consola de administración, haga clic en Servicios > Espacio de trabajo > Buscar plantillas.
1. (Opcional) Si está editando una plantilla existente o utilizando una plantilla existente como base para una nueva plantilla, seleccione la plantilla en la lista Buscar nombre de plantilla.
1. En el cuadro Buscar descripción de plantilla, especifique el propósito de la plantilla.
1. (Opcional) En el cuadro Instrucciones del usuario, proporcione todas las instrucciones que puedan ayudar a utilizar la plantilla. Estas instrucciones se muestran en Workspace cuando un usuario selecciona la plantilla de búsqueda.
1. Haga clic en la ficha Criterios. Aquí es donde define uno o más criterios de búsqueda. Para agregar un criterio de búsqueda:

   * En la parte superior de la ficha Criterios, seleccione un elemento de proceso o un elemento de tarea.

      **Sugerencia**: *Si previamente seleccionó el elemento Nombre del proceso y especificó un proceso, también se podrán seleccionar todas las variables de proceso definidas en ese proceso.*

      **Sugerencia**: *Si selecciona el elemento Tarea visible, los usuarios podrán eliminar las tareas completadas de los resultados de búsqueda.*

      Los campos de criterios de búsqueda del elemento seleccionado aparecen en la parte inferior de la ficha Criterios.

   * Para cada elemento de proceso, elemento de tarea y variable de proceso que seleccione, rellene los campos de búsqueda correspondientes en la parte inferior de la ficha Criterios:

      * Seleccione un operador relacional (por ejemplo, &quot;ser igual a&quot;) en la lista proporcionada y especifique el valor del operando en el cuadro que hay junto a él.
      * (Opcional) Para permitir que los usuarios cambien el valor del operando en Workspace, seleccione Permitir al usuario cambiar el operando.
      * (Opcional) Para permitir que los usuarios cambien el operador relacional, seleccione Permitir que el usuario seleccione otro operador relacional. En la lista que aparece, seleccione los operadores que estarán disponibles para el usuario.
      **Sugerencia**: *Si ha seleccionado Nombre del proceso como elemento, puede hacer clic en el icono situado junto al campo de operando para mostrar una lista en la que puede seleccionar un proceso que se está ejecutando en el servidor de formularios. Después de seleccionar un proceso, todas las variables de proceso definidas en ese proceso se pueden seleccionar en Variables de proceso en la sección superior de la ficha Criterios.*

      **Sugerencia**: *Puede eliminar un elemento de la plantilla de búsqueda haciendo clic en el icono Eliminar situado junto a los criterios de búsqueda del elemento.*


1. (Opcional) Para que el encabezado de cada columna se muestre en los resultados de la búsqueda, haga clic en la ficha Diseño y lleve a cabo los siguientes pasos:

   * Seleccione un elemento de proceso o tarea y haga clic en la flecha derecha para moverlo a la lista Columnas a informe.
   * En la lista Columnas a informar, seleccione el elemento de proceso o tarea y haga clic en las flechas arriba o abajo para moverlo a su lugar en el orden de las columnas. Los encabezados de columna de los resultados de búsqueda aparecerán en el orden en que aparecen aquí.
   * (Opcional) Para cambiar el nombre del elemento para el encabezado de la columna, seleccione el elemento en la lista Columnas a informar y proporcione el nuevo nombre.

      **Nota**: *El diseño especificado en la plantilla de búsqueda anula las preferencias del usuario especificadas para los encabezados de columna en Workspace.*

1. (Opcional) Para que cada columna se ordene en los resultados de la búsqueda, haga clic en la ficha Ordenar y lleve a cabo los siguientes pasos:

   * Seleccione un elemento de proceso o tarea y haga clic en la flecha derecha para moverlo a la lista Orden.
   * En la lista Orden, seleccione el elemento de proceso o tarea y haga clic en la flecha arriba o abajo para moverlo a su lugar en el orden de clasificación. Las columnas de los resultados de la búsqueda se ordenarán en función del orden en que aparecen aquí.
   * (Opcional) Para ordenar una columna en orden descendente, active la casilla de verificación situada junto al nombre del elemento. Si la casilla de verificación no está seleccionada, la columna se ordena en orden ascendente.

1. Haga clic en la ficha Guardar.
1. (Opcional) Si crea una nueva plantilla de búsqueda, asígnele un nombre único. Si no especifica un nombre único, puede sobrescribir una plantilla existente.
1. Haga clic en el botón Guardar.

## Eliminar una plantilla de búsqueda {#delete-a-search-template}

1. En la ficha Identificación, seleccione un nombre en la lista Buscar nombre de plantilla.
1. Haga clic en Eliminar esta plantilla y en Aceptar.

