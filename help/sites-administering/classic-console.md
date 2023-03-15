---
title: Consola de etiquetado de IU clásica
seo-title: Classic UI Tagging Console
description: Obtenga información acerca de la consola de etiquetado de IU clásica.
seo-description: Learn about the Classic UI Tagging Console.
uuid: 51e29422-f967-424b-a7fd-4ca2ddc6b8a3
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: b279c033-bc93-4e62-81ad-123c40b9fdd2
docset: aem65
exl-id: 8c6ba22f-5555-4e3c-998a-9353bd44715b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 37%

---

# Consola de etiquetado de IU clásica{#classic-ui-tagging-console}

Esta sección es para la Consola de etiquetado de IU clásica.

La consola de etiquetado de IU táctil está optimizada [aquí](/help/sites-administering/tags.md#tagging-console).

Para acceder a la consola de etiquetado de IU clásica:

* sobre el autor
* iniciar sesión con privilegios administrativos
* vaya a la consola, por ejemplo: [https://localhost:4502/tagging](https://localhost:4502/tagging)

![](assets/managing_tags_usingthetagasministrationconsole.png)

## Creación de tags y espacios de nombres {#creating-tags-and-namespaces}

1. Según el nivel desde el que comience, puede crear una etiqueta o un espacio de nombres con **Nuevo**:

   Si selecciona **Etiquetas**, puede crear un espacio de nombres:

   ![](assets/creating_tags_andnamespaces.png)

   Si selecciona un espacio de nombres (por ejemplo **Demo**), puede crear una etiqueta dentro de ese espacio de nombres:

   ![](assets/creating_tags_andnamespacesinnewnamespace.png)

1. En ambos casos, introduzca

   * **Título**
(
*Requerido*) El título para mostrar de la etiqueta. Aunque se puede introducir cualquier carácter, se recomienda no utilizar estos caracteres especiales:

      * `colon (:)` - delimitador de área de nombres
      * `forward slash (/)` - delimitador de subetiqueta

      Estos caracteres no se mostrarán si se introducen.

   * **Nombre**
(
*Requerido*) El nombre del nodo de la etiqueta.

   * **Descripción**
(
*Opcional*) Una descripción para la etiqueta.

   * select **Crear**


## Edición de tags {#editing-tags}

1. En el panel de la derecha, seleccione la etiqueta que desee editar.
1. Haga clic en **Editar**.
1. Puede modificar el **Título** y la **Descripción**.
1. Haga clic en **Guardar** para cerrar el cuadro de diálogo.

## Eliminación de tags {#deleting-tags}

1. En el panel derecho, seleccione la etiqueta que desee eliminar.
1. Haga clic en **Eliminar**.
1. Clic **Sí** para cerrar el cuadro de diálogo.

   La etiqueta ya no debería aparecer en la lista.

## Activación y desactivación de tags {#activating-and-deactivating-tags}

1. En el panel derecho, seleccione el área de nombres o la etiqueta que desea activar (publicar) o desactivar (cancelar la publicación).
1. Haga clic en **Activar** o **Desactivar** según sea necesario.

## Lista - mostrar el lugar donde se hace referencia a los tags {#list-showing-where-tags-are-referenced}

**Lista** abre una nueva ventana donde se muestran las rutas de todas las páginas mediante la etiqueta resaltada:

![](assets/list_showing_wheretagsarereferenced.png)

## Movimiento de tags {#moving-tags}

Para ayudar a los administradores y desarrolladores de etiquetas a limpiar la taxonomía o cambiar el nombre de un ID de etiqueta, es posible mover una etiqueta a una nueva ubicación:

1. Abra la consola **Tagging**.
1. Seleccione la etiqueta y haga clic en **Mover...** en la barra de herramientas superior (o en el menú contextual).
1. En el cuadro de diálogo **Mover etiqueta**, defina:

   * **hasta**, el nodo de destino.
   * **Cambiar nombre a**, el nuevo nombre del nodo.

1. Haga clic en **Mover**.

El cuadro de diálogo **Mover etiqueta** tiene el siguiente aspecto:

![](assets/move_tag.png)

>[!NOTE]
>
>Los autores no deben mover etiquetas ni cambiar el nombre de un ID de etiqueta. Cuando sea necesario, los autores solo deben [cambiar los títulos de las etiquetas](#editing-tags).

## Combinación de tags {#merging-tags}

Se pueden combinar etiquetas cuando una taxonomía tiene duplicados. Cuando la etiqueta A se combina con la etiqueta B, todas las páginas etiquetadas con la etiqueta A se etiquetarán con la etiqueta B y la etiqueta A ya no está disponible para los autores.

Para combinar una etiqueta con otra:

1. Abra la consola **Tagging**.
1. Seleccione la etiqueta y haga clic en **Combinar...** en la barra de herramientas superior (o en el menú contextual).
1. En el cuadro de diálogo **Combinar etiqueta**, defina:

   * **en**, el nodo de destino.

1. Haga clic en **Combinar**.

El **Combinar etiqueta** tiene el siguiente aspecto:

![](assets/mergetag.png)

## Recuento de uso de tags {#counting-usage-of-tags}

Para ver cuántas veces se está usando una etiqueta:

1. Abra la consola **Tagging**.
1. Haga clic en **Uso de recuento** en la barra de herramientas superior: en la columna Recuento se muestra el resultado.

## Administración de tags en distintos idiomas {#managing-tags-in-different-languages}

El opcional `title`La propiedad de una etiqueta se puede traducir a varios idiomas. Etiqueta `titles` a continuación, se puede mostrar según el idioma del usuario o el idioma de la página.

### Definición de títulos de tags en varios idiomas {#defining-tag-titles-in-multiple-languages}

El siguiente procedimiento muestra cómo traducir el `title`de la etiqueta **Animales** en inglés, alemán y francés:

1. Vaya a la **Etiquetado** consola.
1. Editar la etiqueta **Animales** abajo **Etiquetas** > **Fotografías de archivo**.
1. Agregue las traducciones en los siguientes idiomas:

   * **Inglés**: Animals
   * **Alemán**: Tiere
   * **Francés**: Animaux

1. Guarde los cambios.

El cuadro de diálogo tiene este aspecto:

![](assets/edit_tag.png)

La consola de etiquetado utiliza la configuración de idioma del usuario, por lo que para la etiqueta Animal, se muestra &quot;Animaux&quot; para un usuario que establece el idioma en francés en las propiedades del usuario.

Para añadir un nuevo idioma al cuadro de diálogo, consulte la sección [Adición de un nuevo idioma al cuadro de diálogo Editar etiqueta](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) en el **Etiquetado para desarrolladores** sección.

### Mostrar títulos de etiquetas en las propiedades de página en un idioma especificado {#displaying-tag-titles-in-page-properties-in-a-specified-language}

De forma predeterminada, la etiqueta `titles`en la página, las propiedades se muestran en el idioma de la página. El cuadro de diálogo de etiquetas de las propiedades de página tiene un campo de idioma que permite mostrar la etiqueta `titles`en un idioma diferente. El siguiente procedimiento describe cómo mostrar la etiqueta `titles`en francés:

1. Consulte la sección anterior para añadir la traducción al francés a la **Animales** abajo **Etiquetas** > **Fotografías de archivo**.
1. Abra las propiedades de página correspondientes a la página **Products** en la rama en inglés del sitio **Geometrixx**.
1. Abra el **Etiquetas/Palabras clave** (seleccionando el menú desplegable a la derecha del área de visualización de Etiquetas/Palabras clave) y seleccione la opción **francés** idioma del menú desplegable en la esquina inferior derecha.
1. Desplácese utilizando las flechas izquierda-derecha hasta que pueda seleccionar la variable **Fotografías de archivo** pestaña

   Seleccione el **Animales** (**Animaux**) y seleccione fuera del cuadro de diálogo para cerrarlo y añadir la etiqueta a las propiedades de página.

   ![](assets/french_tag.png)

De forma predeterminada, el cuadro de diálogo Propiedades de página muestra la etiqueta `titles`según el idioma de la página.

En general, el idioma de la etiqueta se toma del idioma de la página si este está disponible. Si la variable [ `tag` widget](/help/sites-developing/building.md#tagging-on-the-client-side) se utiliza en otros casos (por ejemplo, en formularios o cuadros de diálogo), el idioma de la etiqueta depende del contexto.

>[!NOTE]
>
>La nube de etiquetas y las palabras clave meta del componente de página estándar utilizan la etiqueta localizada `titles`en función del idioma de la página, si está disponible.
