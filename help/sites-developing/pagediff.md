---
title: Desarrollo y diferencia de página
seo-title: Desarrollo y diferencia de página
description: nulo
seo-description: nulo
uuid: 06f27bc2-f42a-4176-ab94-255e721c6933
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6612f89d-c518-4e5a-8df1-6487cc330a9a
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 10%

---


# Desarrollo y diferencia de página{#developing-and-page-diff}

## Información general de características {#feature-overview}

La creación de contenido es un proceso iterativo. La creación con eficiencia de contenido requiere poder ver qué ha cambiado de una iteración a otra. Visualizar una versión de la página y luego otra es un proceso poco eficaz y propenso a errores. Un autor desea poder comparar la página actual con una versión anterior en paralelo con las diferencias resaltadas.

La diferencia de página permite al usuario comparar la página actual con los inicios, las versiones anteriores, etc. Para obtener más información sobre esta función de usuario, consulte [Dif. de página](/help/sites-authoring/page-diff.md).

## Detalles de la operación {#operation-details}

Al comparar versiones de una página, la versión anterior que el usuario desea comparar se vuelve a crear con AEM en segundo plano para facilitar la diferencia. Esto es necesario para poder representar el contenido [para la comparación en paralelo](/help/sites-developing/pagediff.md#operation-details).

Esta operación de recreación la realiza AEM internamente y es transparente para el usuario y no requiere ninguna intervención. Sin embargo, un administrador que visualiza el repositorio, por ejemplo, en CRX DE Lite, vería estas versiones recreadas dentro de la estructura de contenido.

Cuando se compara el contenido, todo el árbol hasta la página que comparar se vuelve a crear en la siguiente ubicación:

`/tmp/versionhistory/`

Una tarea de limpieza se ejecuta automáticamente para limpiar este contenido temporal.

## Permisos    {#permissions}

Anteriormente, en la IU clásica, había que tener especialmente en cuenta el desarrollo para facilitar la difusión de AEM (como el uso de la biblioteca de etiquetas `cq:text` o la integración personalizada del servicio OSGi `DiffService` en los componentes). Esto ya no es necesario para la nueva función de diferencia, ya que la diferencia se produce en el cliente mediante la comparación DOM.

Sin embargo, hay una serie de limitaciones que el desarrollador debe tener en cuenta.

* Esta función utiliza clases CSS que no tienen nombres espaciados en el producto AEM. Si en la página se incluyen otras clases CSS personalizadas o clases CSS de terceros con los mismos nombres, la visualización de la diferencia puede verse afectada.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Debido a que la diferencia es del lado del cliente y se ejecuta al cargar la página, no se contabilizarán los ajustes en el DOM después de ejecutar el servicio de diferencias del lado del cliente. Esto puede afectar

   * Componentes que utilizan AJAX para incluir contenido
   * Aplicaciones de una sola página
   * Componentes basados en JavaScript que manipulan el DOM tras la interacción del usuario.
