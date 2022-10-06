---
title: Aplicación de flujos de trabajo a páginas
seo-title: Applying Workflows to Pages
description: Los flujos de trabajo se pueden iniciar desde la consola sitios web o, al editar una página, desde la barra de tareas.
seo-description: Workflows can be started from either the Websites console or, when editing a page, from Sidekick.
uuid: 55f6f1d7-da54-4732-b9ff-b7479622db51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 22712b73-90f2-4329-b32f-dbb7ce802d1d
exl-id: d8b604c5-a6da-47c4-9422-b519e224c7ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 85%

---

# Aplicación de flujos de trabajo a páginas{#applying-workflows-to-pages}

A la hora de aplicar el flujo de trabajo, puede especificar la siguiente información:

* Flujo de trabajo que se va a aplicar.

   Puede aplicar cualquier flujo de trabajo (al que tenga acceso, según lo haya asignado el administrador de AEM).
* De forma opcional:

   * Un comentario que proporciona información sobre por qué se inició el flujo de trabajo.
   * Un título que ayuda a identificar la instancia del flujo de trabajo en la bandeja de entrada de un usuario.

>[!NOTE]
>
>Los administradores de AEM pueden iniciar flujos de trabajo mediante [muchos otros métodos](/help/sites-administering/workflows-starting.md).

## Aplicar flujos de trabajo {#applying-workflows}

Los flujos de trabajo se pueden iniciar desde la consola sitios web o, al editar una página, desde la barra de tareas.

La variable **Estado** en la columna **Sitios web** console indica si se ha aplicado un flujo de trabajo a una página:

![estado del flujo de trabajo](assets/workflowstatus.png)

### Iniciar un flujo de trabajo desde la consola de sitios web {#starting-a-workflow-from-the-websites-console}

1. Abra la consola Sitios web. ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))
1. En el árbol de páginas web, seleccione la página principal a la que desee aplicar el flujo de trabajo.
1. En la lista de la página, seleccione la página y, a continuación, haga clic en el flujo de trabajo.
1. En el cuadro de diálogo Iniciar un flujo de trabajo, seleccione el flujo de trabajo que quiera. De forma opcional, escriba un comentario y un título. A continuación, haga clic en Inicio.

### Iniciar un flujo de trabajo mediante la barra de tareas {#starting-a-workflow-using-sidekick}

1. Abra la consola Sitios web. 
1. Abra la página necesaria.
1. Seleccione la ficha del flujo de trabajo de la barra de tareas.
1. Expanda el **Flujo de trabajo** , lo que le permite seleccionar la **Flujo de trabajo** y, opcionalmente, introduzca **Título del flujo de trabajo** y **Comentario**.

   ![workflowstartsidekick](assets/workflowstartsidekick.png)

1. Haga clic en el **Flujo de trabajo** para iniciar una nueva instancia de flujo de trabajo con las propiedades que configuró y la página actual como carga. El flujo de trabajo se está ejecutando.
