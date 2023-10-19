---
title: Convenciones de nomenclatura en Java&trade; nombre del paquete
description: Obtenga información sobre las convenciones de nomenclatura y el uso de guiones en el nombre del paquete Java&trade;.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 1%

---

# Convenciones de nomenclatura {#naming-conventions}

## Guiones en el nombre del paquete Java™ {#hyphens-in-java-package-name}

Al crear una ubicación para una clase Java™, el nombre del paquete debe coincidir con el de la ubicación de la carpeta del repositorio con los guiones de la ruta correctamente omitidos.

AEM Aunque el uso de guiones en los nombres de los elementos del repositorio es una práctica recomendada en el desarrollo de la ™, los guiones no son válidos en los nombres de paquetes de Java.

La plataforma CRX subyacente debe poder distinguir entre un guion bajo real `_ `y un guión `-`. Por lo tanto, en JCR, el guión debe reemplazarse por su valor Unicode (u002d) y escaparse con un guion bajo `_`.

Por ejemplo, si la ruta del repositorio es **/apps/my-example/component/info/Info.java**, el nombre del paquete debe ser `java package apps.my_002dexample.component.info;`

Observe que un guion bajo debe evitarse de manera similar, de modo que `_` pasa a `_005f`.
