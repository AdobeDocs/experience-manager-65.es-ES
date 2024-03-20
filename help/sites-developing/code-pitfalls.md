---
title: Peligros de código
description: AEM Peligros comunes de codificación que se deben evitar al desarrollar para la
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Peligros de código{#code-pitfalls}

## Evite los enlaces de Sling en el código Java {#avoid-sling-bindings-in-java-code}

Los enlaces de Sling son una forma inadecuada de obtener acceso a un servicio en el 90 % de los casos. En su lugar, debe utilizar *@Reference* o *@Inject* anotaciones.

## Evite Thread.interrupt en el código Java {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* es peligroso porque puede cerrar archivos, incluidos archivos Lucene y archivos de caché persistentes, cuando se llama en el momento incorrecto.

## Evite mezclar la sincronización de Java con ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Esto puede provocar una condición de carrera en la que el código se interbloqueará finalmente.
