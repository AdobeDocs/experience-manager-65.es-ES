---
title: Uso de flujos de trabajo
description: Los flujos de trabajo de Adobe Experience Manager le permiten automatizar una serie de pasos que se realizan en una página o recurso.
uuid: c4442d2a-c6b0-49d4-a1ce-384017c45bf0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 7cb99618-d903-4cfb-b0d9-b23d189f6e78
exl-id: 7383d590-c6b7-440a-a33d-196dce9736ef
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 74%

---

# Uso de flujos de trabajo{#working-with-workflows}

AEM Los flujos de trabajo le permiten automatizar una serie de pasos que se realizan en (una o más) páginas o recursos.

Por ejemplo, al publicar, un editor debe revisar el contenido antes de que un administrador del sitio active la página. Un flujo de trabajo que automatiza este ejemplo notifica a cada participante cuándo es el momento de realizar el trabajo necesario:

1. El autor aplica el flujo de trabajo a la página.
1. El editor recibe un elemento de trabajo que indica que es necesario para revisar el contenido de la página. Al terminar, indican que el elemento de trabajo se ha completado.
1. El administrador del sitio recibe un elemento de trabajo que solicita la activación de la página. Al terminar, indican que el elemento de trabajo se ha completado.

Típicamente ocurre lo siguiente:

* Los autores de contenido aplican flujos de trabajo a las páginas y participan en flujos de trabajo.
* Los flujos de trabajo que utiliza son específicos de los procesos empresariales de su organización.

En las páginas que se incluyen a continuación, se tratan los temas siguientes:

* [Aplicación de flujos de trabajo a páginas](/help/sites-authoring/workflows-applying.md)
* [Participación en flujos de trabajo](/help/sites-authoring/workflows-participating.md)
