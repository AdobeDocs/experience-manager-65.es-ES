---
title: Convenciones de nomenclatura para la prueba de recursos
seo-title: Naming conventions for assets
description: Los nodos del repositorio están sujetos a las convenciones de nomenclatura del Repositorio de contenidos de Java. Sin embargo, Adobe Experience Manager impone otras convenciones para el nombre de los nodos del recurso.
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
ht-degree: 88%

---

# Convenciones de nomenclatura de los recursos prueba{#naming-conventions-for-assets-testing}

Los nodos del repositorio están sujetos a las convenciones de nomenclatura de la [Repositorio de contenido Java](/help/sites-developing/the-basics.md#java-content-repository). Sin embargo, Adobe Experience Manager impone otras convenciones para el nombre de los nodos del recurso.

## IU clásica {#classic-ui}

La IU clásica impone restricciones más estrictas:

* Valida el nombre del recurso cuando hay un nombre de nodo explícito:

   * se proporciona un título del recurso para convertirlo en el nombre de nodo
   * se proporciona un nombre de nodo explícito

* Caracteres válidos (solo estos caracteres son realmente válidos cuando se crea un recurso en la IU clásica):

   * De la &quot;a&quot; a la &quot;z&quot;
   * De la &quot;A&quot; a la &quot;Z&quot;
   * &quot;0&quot; a &quot;9&quot;
   * _ (guion bajo)
   * `-` (guion/signo menos)
