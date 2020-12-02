---
title: Compilación del plan de pruebas
seo-title: Compilación del plan de pruebas
description: Los casos de prueba individuales se combinan en el plan de pruebas
seo-description: Los casos de prueba individuales se combinan en el plan de pruebas
uuid: d83ef902-e0ef-4f84-9477-be12dfe91742
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 82b8a5f4-583b-47ba-9579-b47364b56aa2
docset: aem65
translation-type: tm+mt
source-git-commit: da08613be784f43ad3e3c3652b7e015640a48a9d
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Compilación del plan de pruebas{#compiling-your-test-plan}

Los casos de prueba individuales se fusionarán en el plan de pruebas, que también definirá:

**Prioridades**

Algunas pruebas tendrán más importancia que otras, por lo que es aconsejable indicar su prioridad.

Por ejemplo, algunas pruebas pueden afectar a una decisión de Go / No-Go y, por lo tanto, deben confirmarse con cada versión provisional probada.

**Iteraciones**

Si su proyecto utiliza cualquier forma de iteración de desarrollo (que implica que se están poniendo a disposición varias versiones), es posible que necesite o desee una indicación de los resultados de cada iteración. Esto puede utilizarse para indicar:

* qué pruebas se incluirán en qué iteración.
* los resultados observados para las pruebas repetidas en varias iteraciones.
* que las pruebas prioritarias y las pruebas sobre características básicas se repiten a intervalos regulares.

**Tester**

En algún momento puede asignar el equipo de prueba adecuado o una persona de prueba específica (posiblemente según la disponibilidad o la experiencia).

**Resumen o Información general**

Para fines de sistema de informes, debe proporcionar una descripción general de los resultados de la prueba:

* Porcentaje de pruebas ya cubiertas.
* Porcentaje de éxito/error.
* Cifras específicas relacionadas con las pruebas prioritarias.

