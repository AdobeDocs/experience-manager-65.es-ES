---
title: Convenciones de nomenclatura para pruebas de recursos
seo-title: Naming conventions for assets
description: Los nodos del repositorio están sujetos a las convenciones de nomenclatura del repositorio de contenido Java. Sin embargo, Adobe Experience Manager impone más convenciones para el nombre de los nodos de recursos.
seo-description: Nodes in the repository are subject to naming conventions of the Java Content Repository. However, Adobe Experience Manager imposes further conventions for the name of asset nodes.
uuid: 6b622a60-90e8-461e-9b67-42c11c7038f9
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 55e66c66-0120-4ed4-94c5-d65a434bb59b
exl-id: bb6a5913-0871-47c7-8641-936e98920ec0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 2%

---

# Convenciones de nomenclatura para pruebas de recursos{#naming-conventions-for-assets-testing}

Los nodos del repositorio están sujetos a las convenciones de nomenclatura de [Repositorio de contenido Java](/help/sites-developing/the-basics.md#java-content-repository). Sin embargo, Adobe Experience Manager impone más convenciones para el nombre de los nodos de recursos.

## IU clásica {#classic-ui}

La IU clásica impone restricciones más estrictas:

* Valida el nombre del recurso cuando un nombre de nodo explícito:

   * se proporciona un título de recurso para la conversión en el nombre del nodo
   * se proporciona un nombre de nodo explícito

* Caracteres válidos (solo estos caracteres son realmente válidos cuando se crea un recurso desde la IU clásica):

   * &#39;a&#39; a &#39;z&#39;
   * De &#39;A&#39; a &#39;Z&#39;
   * De &#39;0&#39; a &#39;9&#39;
   * _ (guion bajo)
   * `-` (guión/signo menos)
