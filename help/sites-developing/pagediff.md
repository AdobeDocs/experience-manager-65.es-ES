---
title: Desarrollo y diferencia de página
description: Aprenda a desarrollar y utilizar la función de diferencia de página en Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: b07134b2-074a-4d52-8d0c-7e7abe51fc3a
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 10%

---

# Desarrollo y diferencia de página{#developing-and-page-diff}

## Descripción general de funciones {#feature-overview}

La creación de contenido es un proceso iterativo. La creación con eficiencia de contenido requiere poder ver qué ha cambiado de una iteración a otra. Visualizar la versión de la página y luego otra es un proceso poco eficaz y propenso a errores. Un autor desea poder comparar la página actual con una versión anterior en paralelo con las diferencias resaltadas.

La diferencia de página permite al usuario comparar la página actual con lanzamientos, versiones anteriores, etc. Para obtener más información sobre esta función de usuario, consulte [Diferencias de página](/help/sites-authoring/page-diff.md).

## Detalles de operación {#operation-details}

AEM Cuando se comparan versiones de una página, la versión anterior que el usuario desea comparar se vuelve a crear en segundo plano para facilitar la comparación con otras versiones de una página. Se puede acceder a esta versión desde el segundo plano, lo que permite la comparación con otras versiones de una página. Esto es necesario para poder procesar el contenido [para una comparación en paralelo](/help/sites-developing/pagediff.md#operation-details).

AEM Esta operación de recreación se realiza por parte de los usuarios de forma interna, es transparente para el usuario y no requiere intervención alguna. Sin embargo, un administrador que visualice el repositorio, por ejemplo, en CRXDE Lite, vería estas versiones recreadas dentro de la estructura de contenido.

Cuando se compara contenido, todo el árbol hasta la página para comparar se vuelve a crear en la siguiente ubicación:

`/tmp/versionhistory/`

Se ejecuta automáticamente una tarea de limpieza para limpiar este contenido temporal.

## Permisos {#permissions}

AEM Anteriormente, en la IU clásica, se tenía que tener especial consideración en el desarrollo para facilitar la diferenciación de los recursos (por ejemplo, el uso de ) `cq:text` biblioteca de etiquetas o integración personalizada de `DiffService` servicio OSGi en componentes). Esto ya no es necesario para la nueva función de diferencia, ya que la diferencia se produce en el lado del cliente mediante la comparación DOM.

Sin embargo, hay algunas limitaciones que el desarrollador debe tener en cuenta.

* AEM Esta función utiliza clases CSS a las que no se les asigna un espacio de nombres para el producto de. Si se incluyen en la página otras clases CSS personalizadas o clases CSS de terceros con los mismos nombres, la visualización de la diferencia puede verse afectada.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Dado que la comparación de diferencias es del lado del cliente y se ejecuta al cargar la página, no se contabilizará ningún ajuste en el DOM después de ejecutar el servicio de comparación de diferencias del lado del cliente. Esto puede afectar a

   * AJAX Componentes que utilizan la para incluir contenido
   * Aplicaciones de una sola página
   * Componentes basados en JavaScript que manipulan el DOM tras la interacción del usuario.

>[!NOTE]
>
>La comparación de diferencias de página solo funciona para los componentes que tienen nodos cq:editConfig válidos.
