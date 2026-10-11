---
title: Convenciones de nomenclatura en Java&trade; nombre del paquete
description: Obtenga información sobre las convenciones de nomenclatura y el uso de guiones en el nombre del paquete Java&trade;.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 1%
---
# Convenciones de nomenclatura {#naming-conventions}

## Guiones en el nombre del paquete Java™ {#hyphens-in-java-package-name}

Al crear una ubicación para una clase Java™, el nombre del paquete debe coincidir con el de la ubicación de la carpeta del repositorio con los guiones de la ruta correctamente omitidos.

Aunque el uso de guiones en los nombres de los elementos del repositorio es una práctica recomendada en el desarrollo de AEM, los guiones no son válidos en los nombres de paquetes Java™.

La plataforma CRX subyacente debe poder distinguir entre un guion bajo real `_ ` y un guion `-`. Por lo tanto, en JCR, el guión debe reemplazarse con su valor Unicode (u002d) y escapar con un guion bajo `_`.

Por ejemplo, si la ruta del repositorio es **/apps/my-example/component/info/Info.java**, el nombre del paquete debe ser `java package apps.my_002dexample.component.info;`

Observe que un guion bajo debe evitarse de manera similar, de modo que `_` se convierta en `_005f`.
