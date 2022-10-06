---
title: Uso de flujos de trabajo
seo-title: Working with Workflows
description: Los flujos de trabajo de AEM le permiten automatizar una serie de pasos que se llevan a cabo en una página o un recurso. Por ejemplo, al publicar, un editor debe revisar el contenido antes de que un administrador del sitio active la página. Un flujo de trabajo que automatiza este ejemplo notifica a cada participante cuándo es el momento de realizar el trabajo necesario.
seo-description: AEM Workflows allows you to automate a series of steps that are performed on a page or asset. For example, when publishing, an editor has to review the content - before a site administrator activates the page. A workflow that automates this example notifies each participant when it is time to perform their required work.
uuid: 3eb6e790-6589-414a-8e51-33c358f47a73
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: b11f0e4c-4dec-4b66-9f54-a0aa13ac77b9
exl-id: 298fcfeb-dc8d-4edc-8743-83c0e5e5bc08
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 100%

---

# Uso de flujos de trabajo{#working-with-workflows}

Los flujos de trabajo de AEM le permiten automatizar una serie de pasos que se llevan a cabo en una página o un recurso. Por ejemplo, al publicar, un editor debe revisar el contenido antes de que un administrador del sitio active la página. Un flujo de trabajo que automatiza este ejemplo notifica a cada participante cuándo es el momento de realizar el trabajo necesario:

1. El autor aplica el flujo de trabajo a la página.
1. El editor recibe un elemento de trabajo que indica que es necesario para revisar el contenido de la página. Al terminar, indica que el elemento de trabajo se ha completado.
1. El administrador del sitio recibe un elemento de trabajo que solicita la activación de la página. Al terminar, indica que el elemento de trabajo se ha completado.

Normalmente:

* Los autores de contenido aplican los flujos de trabajo a las páginas y también participan en los flujos de trabajo.
* Los flujos de trabajo que utiliza son específicos de los procesos empresariales de su organización.

En las páginas que se incluyen a continuación, se tratan los temas siguientes:

* [Aplicación de flujos de trabajo a páginas](/help/sites-classic-ui-authoring/classic-workflows-applying.md)
* [Participación en flujos de trabajo](/help/sites-classic-ui-authoring/classic-workflows-participating.md)
