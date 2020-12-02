---
title: Administración de las categorías mostradas en Workspace
seo-title: Administración de las categorías mostradas en Workspace
description: En Workspace, los procesos que un usuario puede inicio se muestran en categorías en el panel de navegación izquierdo. Descubra cómo puede administrar estas categorías que se muestran en Workspace.
seo-description: En Workspace, los procesos que un usuario puede inicio se muestran en categorías en el panel de navegación izquierdo. Descubra cómo puede administrar estas categorías que se muestran en Workspace.
uuid: c2a275f5-872e-467f-9f07-4b130631e8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0d1536a2-10ac-4031-bd7f-264b02d0d75f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# Administración de las categorías mostradas en Workspace {#managing-the-categories-displayed-in-workspace}

En Workspace, los procesos que un usuario puede inicio se muestran en categorías en el panel de navegación izquierdo. Puede configurar las categorías en la consola de administración o los diseñadores de procesos pueden configurarlas en Workbench. Cuando los diseñadores de procesos crean procesos, los asignan a categorías.

Cuando especifique nombres de categoría, créelos para que aparezcan correctamente en el panel de navegación del espacio de trabajo. De forma predeterminada, el panel de navegación izquierdo tiene una anchura fija de 210 píxeles, que es de aproximadamente 24 caracteres. Si el nombre de la categoría especificado es demasiado largo para ajustarse al ancho fijo del panel de navegación izquierdo, se trunca. El nombre completo solo aparece cuando se pone en pausa el puntero del ratón sobre él. Intente evitar los nombres de categoría que se truncarán. Los siguientes ejemplos ilustran los nombres de categorías que encajan y los que se truncan:

**Nombre de categoría que se ajusta:** Asistencia y salir

**Nombre de categoría truncado:** Asistencia y salida (Estados Unidos)

En Workspace, los procesos dentro de una categoría suelen mostrarse como tarjetas en la página Proceso de Inicio. En general, se pueden mostrar seis tarjetas en la pantalla para una categoría antes de que el usuario tenga que desplazarse hasta las tarjetas restantes de la vista. Debido a que el desplazamiento dificulta la búsqueda de un proceso, considere la posibilidad de limitar cada categoría a seis procesos o, según la resolución, limitar el número de procesos que se pueden mostrar en la pantalla sin necesidad de desplazamiento.

Si utiliza MySQL como base de datos de formularios AEM, la Consola de administración no puede diferenciar entre dos nombres de categoría que difieran sólo en el uso de caracteres extendidos. Por ejemplo, si crea una categoría con el nombre abcde y una categoría con el nombre âbcdè, se considerarán iguales.

## Añadir una categoría {#add-a-category}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de Categorías.
1. Haga clic en Agregar. Si desea agregar una subcategoría, seleccione una categoría y haga clic en Añadir.
1. En el cuadro Nombre, escriba un nombre para la categoría y, en el cuadro Descripción, escriba una descripción de la categoría.
1. Haga clic en Agregar. La categoría se muestra en la página Administración de Categorías.

   ***nota **: Solo se pueden agregar hasta cinco niveles de jerarquía al crear categorías.*

## Editar una categoría {#edit-a-category}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de Categorías.
1. Seleccione la categoría que desee editar y haga clic en Editar. Como alternativa, puede hacer clic en una categoría en doble para editarla.
1. Edite el nombre de la categoría en el cuadro Nombre.

## Eliminar una categoría {#remove-a-category}

Solo puede eliminar las categorías que no se estén utilizando.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de Categorías.
1. En la página Administración de Categorías, active la casilla de verificación de la categoría que desea eliminar y haga clic en Eliminar. La categoría ya no se muestra.

