---
title: Diferencias de página
seo-title: Page Diff
description: La función de diferencia de página permite realizar una comparación en paralelo de dos páginas con sus diferencias resaltadas.
seo-description: The page diff feature allows for the convenient side-by-side comparison of two pages with their differences highlighted.
uuid: 5af8b466-5922-4fe6-9eae-7bad99be23e0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8386a16a-9d47-46d5-bc60-5f290c59e60e
docset: aem65
exl-id: 3beea5cd-5ae0-485b-8dfc-8b3a23c11586
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 32%

---

# Diferencias de página  {#page-diff}

## Introducción {#introduction}

La creación de contenido es un proceso iterativo. Crear con eficacia requiere poder ver qué ha cambiado de una iteración a otra. Ver una versión de la página y luego la otra es ineficiente y propensa a errores. Un autor quiere poder comparar fácilmente la página actual en paralelo con otra versión.

La función de diferencia de página permite realizar una comparación en paralelo de dos páginas con sus diferencias resaltadas.

>[!TIP]
>
>Consulte [Desarrollo y diferencia de página](/help/sites-developing/pagediff.md#operation-details) para obtener más información técnica sobre esta función.

## Uso de {#use}

La comparación de diferencias en paralelo permite comparar lo siguiente:

* [Versiones](/help/sites-authoring/working-with-page-versions.md#comparing-a-version-with-current-page): versión anterior de una página con el estado actual.
* [Live Copies](/help/sites-administering/msm-livecopy.md#comparing-a-live-copy-page-with-a-blueprint-page): Live Copy con su modelo.
* [Lanzamientos](/help/sites-authoring/launches-editing.md#comparing-a-launch-page-to-its-source-page): lanzamiento con su origen.
* [Copias de idioma](/help/sites-administering/tc-manage.md#comparing-language-copies): una página antes y después de la traducción.

Consulte los temas respectivos sobre cómo iniciar la comparación de diferencias dentro de esos contextos.

### Presentación de diferencias   {#presentation-of-differences}

Independientemente del contenido que se compare, la presentación de la comparación de diferencias sigue siendo la misma.

* El contenido seleccionado al iniciar la comparación de diferencias se muestra a la izquierda (el punto de entrada de diferencia).
* El contenido comparativo se muestra a la derecha (con qué se compara el contenido seleccionado).

Por ejemplo, si se comparan versiones, la versión actual se muestra a la izquierda y la anterior a la derecha.

El origen de ambas páginas se muestra claramente en la barra de encabezado de la parte superior de la ventana del explorador.

![chlimage_1-109](assets/chlimage_1-109.png)

La comparación de diferencias detecta los cambios en los niveles de componente y HTML. Los elementos que se han cambiado se resaltan con colores diferentes.

**Cambios de componentes**

* Verde claro: componente añadido
* Rosa: componente eliminado

**Cambios del HTML**

* Verde oscuro: HTML añadido
* Rojo: HTML eliminado

>[!NOTE]
>
>Al comparar copias de idioma, se desactiva el resaltado, ya que en una traducción todo cambia y el resaltado no sería de ninguna utilidad.

### Pantalla completa y salida   {#fullscreen-and-exiting}

Para centrarse en un contenido específico, puede hacer clic en el icono de pantalla completa para que cualquier &quot;lado&quot; de la comparación de diferencias en paralelo se amplíe en la ventana completa del navegador.

![](do-not-localize/chlimage_1-18.png)

El lado seleccionado llenará toda la ventana, pero la barra permanecerá en la parte superior para que pueda cambiar entre las dos páginas.

![chlimage_1-110](assets/chlimage_1-110.png)

También puede cerrar la vista de pantalla completa haciendo clic en el icono para salir del modo de pantalla completa.

![](do-not-localize/chlimage_1-19.png)

Puede salir de la comparación de diferencias en cualquier momento haciendo clic en el botón Close del encabezado.

## Restricciones   {#limitations}

Hay algunas situaciones en las que la diferencia de página puede no detectarse según lo esperado.

* Al diferenciar versiones y lanzamientos, la comparación de diferencias no tiene en cuenta componentes dinámicos como rutas de exploración, menús, listas de productos o logotipos (componentes que dependen de la estructura del sitio para procesar su contenido).
* Para las versiones, la comparación de diferencias no vuelve a crear la política de control de acceso ni las relaciones de Live Copy.
* Si se mueve una página, ya no se puede realizar una diferencia con las versiones realizadas antes del movimiento.

   * Si tiene problemas con una comparación de diferencias, consulte la [Cronología](/help/sites-authoring/basic-handling.md#timeline) para que la página vea si la página se ha movido.

>[!NOTE]
>
>Las versiones no se pueden comparar entre sí. Solo la versión actual se puede comparar con otras versiones de la página. La versión actual siempre es la versión que se resalta con los cambios.

>[!NOTE]
>
>Para obtener más información sobre el funcionamiento del mecanismo de diferencia de página, así como las limitaciones que pueden afectar a dicho mecanismo, consulte la [documentación para desarrolladores](/help/sites-developing/pagediff.md) de esta función.
