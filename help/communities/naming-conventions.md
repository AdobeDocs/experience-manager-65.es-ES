---
title: Convenciones de nomenclatura
seo-title: Convenciones de nomenclatura
description: Guiones en el nombre del paquete Java
seo-description: Guiones en el nombre del paquete Java
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
translation-type: tm+mt
source-git-commit: 22e853ecaf2696c7329a81bb9d375b1dbc74452c
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Convenciones de nombres {#naming-conventions}

## Guiones en el nombre del paquete Java {#hyphens-in-java-package-name}

Al crear una ubicación para una clase Java, tenga en cuenta que el nombre del paquete debe coincidir con el de la ubicación de la carpeta del repositorio con cualquier guión de la ruta de acceso que haya escapado correctamente.

Aunque el uso de guiones en los nombres de los elementos del repositorio es una práctica recomendada en el desarrollo de AEM, los guiones no son válidos en los nombres de paquetes de Java.

La plataforma CRX subyacente debe poder distinguir entre un guión bajo real `_ `y un guión `-`. Por lo tanto, en JCR, el guión debe reemplazarse por su valor Unicode (u002d) y escaparse con un guión bajo `_`.

Por ejemplo, si la ruta del repositorio es **/apps/my-example/component/info/Info.java**, el nombre del paquete debe ser `java package apps.my_002dexample.component.info;`

Tenga en cuenta que un subrayado debe tener un carácter de escape similar, de modo que `_` se convierta en `_005f`.
