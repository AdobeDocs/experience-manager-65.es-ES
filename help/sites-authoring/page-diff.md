---
title: Diferencias de página
seo-title: Diferencias de página
description: La función Diferencias de página permite realizar una cómoda comparación en paralelo de dos páginas con las diferencias resaltadas.
seo-description: La función Diferencias de página permite realizar una cómoda comparación en paralelo de dos páginas con las diferencias resaltadas.
uuid: 5af8b466-5922-4fe6-9eae-7bad99be23e0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8386a16a-9d47-46d5-bc60-5f290c59e60e
docset: aem65
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15

---


# Diferencias de página{#page-diff}

## Introducción {#introduction}

La creación de contenido es un proceso iterativo. La creación con eficiencia de contenido requiere poder ver qué ha cambiado de una iteración a otra. Visualizar una versión de la página y luego otra es un proceso poco eficaz y propenso a errores. Un autor desea poder comparar fácilmente la página actual en paralelo con otra versión.

La función Diferencias de página permite realizar una cómoda comparación en paralelo de dos páginas con las diferencias resaltadas.

>[!CAUTION]
>
>The user must have the **Modify/Create/Delete** permission on the node `/content/versionhistory` in order to use the feature.
>
>Consulte [Desarrollo y diferencia de página](/help/sites-developing/pagediff.md#operation-details) para obtener más información técnica sobre esta función.

## Uso {#use}

La comparación de diferencias en paralelo permite comparar lo siguiente:

* [Versiones](/help/sites-authoring/working-with-page-versions.md#comparing-a-version-with-current-page) : versión anterior de una página con su estado actual
* [Live Copies](/help/sites-administering/msm-livecopy.md#comparing-a-live-copy-page-with-a-blueprint-page) : Live Copy con su modelo
* [Lanzamientos](/help/sites-authoring/launches-editing.md#comparing-a-launch-page-to-its-source-page) : Iniciar con su origen
* [Copias](/help/sites-administering/tc-manage.md#comparing-language-copies) de idioma: una página antes y después de la (re)traducción

Consulte los temas correspondientes sobre cómo iniciar la comparación de diferencias en esos contextos.

### Presentación de diferencias {#presentation-of-differences}

Independientemente del contenido que se va a comparar, la presentación de las diferencias sigue siendo la misma.

* El contenido seleccionado al iniciar la comparación de diferencias se muestra a la izquierda (punto de entrada de las diferencias).
* El contenido con el que se va a comparar se muestra a la derecha (elemento con el que se compara el contenido seleccionado).

Por ejemplo, si se comparan versiones, la versión actual se muestra a la izquierda y la versión anterior se muestra a la derecha.

El origen de ambas páginas se muestra claramente en la barra de encabezado de la parte superior de la ventana del navegador.

![chlimage_1-109](assets/chlimage_1-109.png)

La comparación de diferencias detecta los cambios en el nivel de componente y de HTML. Los elementos modificados se resaltan con colores diferentes.

**Cambios en los componentes** 

* Verde claro: componente añadido
* Rosa: componente eliminado
* Azul: componente modificado
* Azul: componente movido

Tenga en cuenta que los colores de componente modificado y movido son los mismos.

**Cambios en HTML** 

* Verde oscuro: HTML añadido
* Rojo: HTML eliminado

>[!NOTE]
>
>Al comparar copias de idioma, el resaltado está desactivado, ya que en una traducción cambia todo y el resaltado no proporcionará ninguna ventaja.

### Pantalla completa y salida {#fullscreen-and-exiting}

Para centrarse en un contenido específico, puede hacer clic en el icono de pantalla completa para que cualquier &quot;lado&quot; de la comparación de diferencias en paralelo se amplíe en la ventana completa del navegador.

![](do-not-localize/chlimage_1-18.png)

El lado seleccionado llenará toda la ventana, pero la barra permanecerá en la parte superior para que pueda cambiar entre las dos páginas.

![chlimage_1-110](assets/chlimage_1-110.png)

También puede cerrar la vista de pantalla completa haciendo clic en el icono para salir del modo de pantalla completa.

![](do-not-localize/chlimage_1-19.png)

Puede salir de la comparación de diferencias en paralelo en cualquier momento haciendo clic en el botón Cerrar del encabezado.

## Restricciones {#limitations}

Hay algunas situaciones en las que la comparación de diferencias de la página quizás no detecte una diferencia de la forma esperada.

* Al realizar la comparación de diferencias de versiones y lanzamientos, no se tienen en cuenta componentes dinámicos como rutas de exploración, menús, listas de productos o logotipos (componentes que se basan en la estructura del sitio para procesar su contenido).
* Para las versiones, la comparación de diferencias no vuelve a crear la política de control de acceso ni las relaciones de Live Copy.
* Si se realiza algún cambio en una imagen, como modificar los atributos alt, title o src, se resaltará en azul como cambiado. Sin embargo, en algunos casos la imagen tiene una representación Base64 del atributo src e incluso si ambas imágenes tienen el mismo aspecto, la diferencia las marcará como diferentes debido a los diferentes atributos src.
* La comparación de diferencias no puede detectar la rotación de la imagen.
* Si se mueve una página, ya no se puede realizar una diferencia con ninguna versión hecha antes del movimiento.

   * Si tiene problemas con una diferencia, compruebe la [línea de tiempo](/help/sites-authoring/basic-handling.md#timeline) para ver si la página se ha movido.

>[!NOTE]
>
>Las versiones no se pueden comparar entre sí. Solo la versión actual se puede comparar con otras versiones de la página. La versión actual siempre es la versión que se resalta con los cambios.

>[!NOTE]
>
>Para obtener más información sobre cómo funciona el mecanismo de diferencia de página, así como las limitaciones que pueden afectar a dicho mecanismo, consulte la [documentación para desarrolladores](/help/sites-developing/pagediff.md) de esta función.
