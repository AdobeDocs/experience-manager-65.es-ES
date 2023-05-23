---
title: Promoción de lanzamientos
description: Debe promocionar las páginas de lanzamiento para devolver el contenido al origen (producción) antes de publicar. Cuando se promociona una página de lanzamiento, la página correspondiente de las páginas de origen se reemplaza con el contenido de la página promocionada.
uuid: 91f1c6ac-8c4e-4459-aaab-feaa32befc45
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8d38c6f7-8fea-4d27-992d-03b604b9541f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 3013adc3-bec6-4ecc-aefd-f8df2b86dfef
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 17%

---

# Promoción de lanzamientos{#promoting-launches}

Debe promocionar las páginas de lanzamiento para devolver el contenido al origen (producción) antes de publicar. Cuando se promociona una página de lanzamiento, la página correspondiente de las páginas de origen se reemplaza con el contenido de la página promocionada. Las siguientes opciones están disponibles al promocionar una página de lanzamiento:

* Indica si se promocionará solo la página actual o todo el lanzamiento.
* Indica si se promocionarán las páginas secundarias de la página actual.
* Si se promociona el lanzamiento completo o solo las páginas que han cambiado.

## Promoción de páginas de lanzamiento {#promoting-launch-pages}

Para promocionar páginas, realice los siguientes pasos mientras edita la página de lanzamiento que desea promocionar:

1. En el **Página** en la barra de tareas, haga clic en **Promocionar lanzamiento**.
1. Especifique las páginas que promocionar:

   * (Predeterminado) Para promocionar solo la página actual, seleccione **Promocionar Cambios De Página En La Versión De Producción**.
   * Para promocionar también las páginas secundarias de la página actual, seleccione **Incluir páginas secundarias**.
   * Para promocionar todas las páginas del lanzamiento, seleccione **Promocionar Lanzamiento Completo En La Versión De Producción**.

1. Para añadir las páginas de producción a un paquete de flujo de trabajo, seleccione **Añadir a paquete de flujo de trabajo** y luego seleccione el paquete de flujo de trabajo.
1. Clic **Promocionar**.

## Procesamiento de páginas promocionadas mediante el flujo de trabajo de AEM {#processing-promoted-pages-using-aem-workflow}

Utilice modelos de flujo de trabajo para realizar el procesamiento masivo de páginas de Lanzamientos promocionados:

1. Cree un paquete de flujo de trabajo.
1. Cuando los autores promocionan páginas de Launch, las almacenan en el paquete de flujo de trabajo.
1. Inicie un modelo de flujo de trabajo utilizando el paquete como carga útil.

Para iniciar un flujo de trabajo automáticamente cuando se promocionan páginas, [configuración de un lanzador de flujo de trabajo](/help/sites-administering/workflows-starting.md#workflows-launchers) para el nodo del paquete.

Por ejemplo, puede generar automáticamente solicitudes de activación de página cuando los autores promocionen páginas de Lanzamiento. Configure un iniciador de flujo de trabajo para iniciar el flujo de trabajo de activación de solicitud cuando se modifique el nodo del paquete.

![chlimage_1-136](assets/chlimage_1-136.png)
