---
title: Errores de código
seo-title: Errores de código
description: Problemas comunes de codificación que se deben evitar al desarrollar para AEM
seo-description: Problemas comunes de codificación que se deben evitar al desarrollar para AEM
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---


# Errores de código{#code-pitfalls}

## Evitar enlaces de Sling en código Java {#avoid-sling-bindings-in-java-code}

Sling Bindings es una manera inapropiada de obtener acceso a un servicio en el 90% de los casos. En su lugar, debe utilizar las anotaciones *@Reference* o *@Inject*.

## Evite Thread.interrupción en el código Java {#avoid-thread-interrupt-in-java-code}

*Thread.* interruptis es peligroso porque puede cerrar archivos, incluidos archivos Lucene y archivos de caché persistentes, cuando se les llama en el momento incorrecto.

## Evite mezclar la sincronización de Java con ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Esto puede llevar a una condición de carrera en la que el código eventualmente se bloqueará.
