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
source-git-commit: 21330d460d1080ab1dee3e82bc3c3877677c1420
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---


# Consola de etiquetado de IU clásica{#classic-ui-tagging-console}

Esta sección es para la Consola de etiquetado de IU clásica.

La consola de etiquetado de IU táctil está optimizada [aquí](/help/sites-administering/tags.md#tagging-console).

Para acceder a la consola de etiquetado de IU clásica:

* sobre el autor
* iniciar sesión con privilegios administrativos
* vaya a la consola, por ejemplo: [https://localhost:4502/tagging](https://localhost:4502/tagging)

![Ventana de consola clásica](assets/managing_tags_usingthetagasministrationconsole.png)

## Creación de etiquetas y espacios de nombre {#creating-tags-and-namespaces}

1. Según el nivel en el que comience, puede crear una etiqueta o un área de nombres mediante **Nuevo**:

   Si selecciona **Etiquetas** puede crear un área de nombres:

   ![Creación de un cuadro de diálogo de espacio de nombres](assets/creating_tags_andnamespaces.png)

   Si selecciona un área de nombres (por ejemplo, **Demostración**) puede crear una etiqueta dentro de ese área de nombres:

   ![Creación de un cuadro de diálogo de etiquetas](assets/creating_tags_andnamespacesinnewnamespace.png)

1. En ambos casos, introduzca

   * **Título**
(*Requerido*) El título para mostrar de la etiqueta. Aunque se puede introducir cualquier carácter, se recomienda no utilizar estos caracteres especiales:

      * `colon (:)` - delimitador de área de nombres
      * `forward slash (/)` - delimitador de subetiqueta

     Estos caracteres no se mostrarán si se introducen.

   * **Nombre**
(*Requerido*) El nombre del nodo de la etiqueta.

   * **Descripción**
(*Opcional*) Una descripción para la etiqueta.

   * select **Crear**

## Edición de etiquetas {#editing-tags}

1. En el panel derecho, seleccione la etiqueta que desee editar.
1. Clic **Editar**.
1. Puede modificar la variable **Título** y el **Descripción**.
1. Clic **Guardar** para cerrar el cuadro de diálogo.

## Eliminación de etiquetas {#deleting-tags}

1. En el panel derecho, seleccione la etiqueta que desee eliminar.
1. Haga clic en **Eliminar**.
1. Clic **Sí** para cerrar el cuadro de diálogo.

   La etiqueta ya no debería aparecer en la lista.

## Activación y desactivación de etiquetas {#activating-and-deactivating-tags}

1. En el panel derecho, seleccione el área de nombres o la etiqueta que desea activar (publicar) o desactivar (cancelar la publicación).
1. Clic **Activar** o **Desactivar** según sea necesario.

## Lista: mostrar dónde se hace referencia a las etiquetas {#list-showing-where-tags-are-referenced}

**Lista** abre una nueva ventana que muestra las rutas de todas las páginas que utilizan la etiqueta resaltada:

![Búsqueda de lugares donde se hace referencia a las etiquetas](assets/list_showing_wheretagsarereferenced.png)

## Mover etiquetas {#moving-tags}

Para ayudar a los administradores y desarrolladores de etiquetas a limpiar la taxonomía o cambiar el nombre de un ID de etiqueta, es posible mover una etiqueta a una nueva ubicación:

1. Abra el **Etiquetado** consola.
1. Seleccione la etiqueta y haga clic en **Mover...** en la barra de herramientas superior (o en el menú contextual).
1. En el **Mover etiqueta** diálogo, definir:

   * **hasta**, el nodo de destino.
   * **Cambiar nombre a**, el nuevo nombre del nodo.

1. Clic **Mover**.

El **Mover etiqueta** tiene el siguiente aspecto:

![Mover una etiqueta](assets/move_tag.png)

>[!NOTE]
>
>Los autores no deben mover etiquetas ni cambiar el nombre de un ID de etiqueta. Cuando sea necesario, los autores solo deben [cambiar los títulos de las etiquetas](#editing-tags).

## Combinación de etiquetas {#merging-tags}

La combinación de etiquetas se puede utilizar cuando una taxonomía tiene duplicados. Cuando la etiqueta A se combina con la etiqueta B, todas las páginas etiquetadas con la etiqueta A se etiquetarán con la etiqueta B y la etiqueta A ya no está disponible para los autores.

Para combinar una etiqueta en otra:

1. Abra el **Etiquetado** consola.
1. Seleccione la etiqueta y haga clic en **Combinar...** en la barra de herramientas superior (o en el menú contextual).
1. En el **Combinar etiqueta** diálogo, definir:

   * **en**, el nodo de destino.

1. Clic **Combinar**.

El **Combinar etiqueta** tiene el siguiente aspecto:

![Combinación de una etiqueta](assets/mergetag.png)

## Recuento del uso de etiquetas {#counting-usage-of-tags}

Para ver cuántas veces se está utilizando una etiqueta:

1. Abra el **Etiquetado** consola.
1. Clic **Uso de recuento** en la barra de herramientas superior: la columna Count muestra el resultado.

## Administración de etiquetas en diferentes idiomas {#managing-tags-in-different-languages}

El opcional `title`La propiedad de una etiqueta se puede traducir a varios idiomas. Etiqueta `titles` a continuación, se puede mostrar según el idioma del usuario o el idioma de la página.

### Definición de títulos de etiquetas en varios idiomas {#defining-tag-titles-in-multiple-languages}

El siguiente procedimiento muestra cómo traducir el `title`de la etiqueta **Animales** en inglés, alemán y francés:

1. Vaya a la **Etiquetado** consola.
1. Editar la etiqueta **Animales** abajo **Etiquetas** > **Fotografías de archivo**.
1. Añada las traducciones en los siguientes idiomas:

   * **Inglés**: Animales
   * **Alemán**: Neumático
   * **francés**: Animales

1. Guarde los cambios.

El cuadro de diálogo tiene el siguiente aspecto:

![Edición de una etiqueta](assets/edit_tag.png)

La consola de etiquetado utiliza la configuración de idioma del usuario, por lo que para la etiqueta Animal, se muestra &quot;Animaux&quot; para un usuario que establece el idioma en francés en las propiedades del usuario.

Para añadir un nuevo idioma al cuadro de diálogo, consulte la sección [Adición de un nuevo idioma al cuadro de diálogo Editar etiqueta](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) en el **Etiquetado para desarrolladores** sección.

### Mostrar títulos de etiquetas en las propiedades de página en un idioma especificado {#displaying-tag-titles-in-page-properties-in-a-specified-language}

De forma predeterminada, la etiqueta `titles`en la página, las propiedades se muestran en el idioma de la página. El cuadro de diálogo de etiquetas de las propiedades de página tiene un campo de idioma que permite mostrar la etiqueta `titles`en un idioma diferente. El siguiente procedimiento describe cómo mostrar la etiqueta `titles`en francés:

1. Consulte la sección anterior para añadir la traducción al francés a la **Animales** abajo **Etiquetas** > **Fotografías de archivo**.
1. Abra las propiedades de página de **Productos** página en la rama en inglés de **Geometrixx** sitio.
1. Abra el **Etiquetas/Palabras clave** (seleccionando el menú desplegable a la derecha del área de visualización de Etiquetas/Palabras clave) y seleccione la opción **francés** idioma del menú desplegable en la esquina inferior derecha.
1. Desplácese utilizando las flechas izquierda-derecha hasta que pueda seleccionar la variable **Fotografías de archivo** pestaña

   Seleccione el **Animales** (**Animaux**) y seleccione fuera del cuadro de diálogo para cerrarlo y añadir la etiqueta a las propiedades de página.

   ![Edición de otra etiqueta](assets/french_tag.png)

De forma predeterminada, el cuadro de diálogo Propiedades de página muestra la etiqueta `titles`según el idioma de la página.

En general, el idioma de la etiqueta se toma del idioma de la página si este está disponible. Si la variable [`tag` widget](/help/sites-developing/building.md#tagging-on-the-client-side) se utiliza en otros casos (por ejemplo, en formularios o cuadros de diálogo), el idioma de la etiqueta depende del contexto.

>[!NOTE]
>
>La nube de etiquetas y las palabras clave meta del componente de página estándar utilizan la etiqueta localizada `titles`en función del idioma de la página, si está disponible.
