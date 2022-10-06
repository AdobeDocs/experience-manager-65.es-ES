---
title: Uso de flujos de trabajo
seo-title: Working with Workflows
description: Los flujos de trabajo en AEM le permiten automatizar una serie de pasos que se llevan a cabo en una página o un recurso.
seo-description: Workflows in AEM allow you to automate a series of steps that are performed on a page or asset.
uuid: c4442d2a-c6b0-49d4-a1ce-384017c45bf0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 7cb99618-d903-4cfb-b0d9-b23d189f6e78
exl-id: 7383d590-c6b7-440a-a33d-196dce9736ef
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 100%

---

# Uso de flujos de trabajo{#working-with-workflows}

Los flujos de trabajo de AEM le permiten automatizar una serie de pasos que se llevan a cabo en páginas (una o más) o recursos.

Por ejemplo, al publicar, un editor debe revisar el contenido antes de que un administrador del sitio active la página. Un flujo de trabajo que automatiza este ejemplo notifica a cada participante cuándo es el momento de realizar el trabajo necesario:

1. El autor aplica el flujo de trabajo a la página.
1. El editor recibe un elemento de trabajo que indica que es necesario para revisar el contenido de la página. Al terminar, indica que el elemento de trabajo se ha completado.
1. El administrador del sitio recibe un elemento de trabajo que solicita la activación de la página. Al terminar, indica que el elemento de trabajo se ha completado.

Normalmente:

* Los autores de contenido aplican los flujos de trabajo a las páginas y también participan en los flujos de trabajo.
* Los flujos de trabajo que utiliza son específicos de los procesos empresariales de su organización.

En las páginas que se incluyen a continuación, se tratan los temas siguientes:

* [Aplicación de flujos de trabajo a páginas](/help/sites-authoring/workflows-applying.md)
* [Participación en flujos de trabajo](/help/sites-authoring/workflows-participating.md)
