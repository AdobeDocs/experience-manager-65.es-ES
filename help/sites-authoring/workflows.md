---
title: Uso de flujos de trabajo
description: Los flujos de trabajo de Adobe Experience Manager le permiten automatizar una serie de pasos que se realizan en una página o recurso.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 7383d590-c6b7-440a-a33d-196dce9736ef
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Workflow
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
  - id: f6a6f91a-8819-530a-8e7b-c50884a25aef
    internal-label: Workflow
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 74%
---
# Uso de flujos de trabajo{#working-with-workflows}

Los flujos de trabajo de AEM le permiten automatizar una serie de pasos que se realizan en (una o más) páginas o recursos.

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
