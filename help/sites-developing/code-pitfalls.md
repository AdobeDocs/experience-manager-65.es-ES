---
title: Precauciones del código
seo-title: Code pitfalls
description: Problemas comunes de codificación que se evitan al desarrollar para AEM
seo-description: Common coding pitfalls to avoid when developing for AEM
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Precauciones del código{#code-pitfalls}

## Evitar enlaces de Sling en código Java {#avoid-sling-bindings-in-java-code}

Los enlaces de Sling son una manera inapropiada de obtener acceso a un servicio en el 90% de los casos. En su lugar, debe usar *@Reference* o *@Inject* anotaciones.

## Evitar Thread.interrupt en el código Java {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* es peligroso porque puede cerrar archivos, incluidos archivos Lucene y archivos de caché persistentes, cuando se los llama en el momento incorrecto.

## Evite mezclar la sincronización de Java con ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Esto puede llevar a una condición de carrera en la que el código eventualmente se bloqueará.
