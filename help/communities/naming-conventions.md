---
title: Convenciones de nomenclatura
seo-title: Naming Conventions
description: Guiones en nombre de paquete Java
seo-description: Hyphens in Java Package Name
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 3%

---

# Convenciones de nomenclatura {#naming-conventions}

## Guiones en nombre de paquete Java {#hyphens-in-java-package-name}

Al crear una ubicación para una clase Java, tenga en cuenta que el nombre del paquete debe coincidir con el de la ubicación de la carpeta del repositorio con los guiones de la ruta de acceso que se hayan escapado correctamente.

Aunque el uso de guiones en los nombres de elementos del repositorio es una práctica recomendada en AEM desarrollo, los guiones son ilegales en los nombres de paquetes Java.

La plataforma CRX subyacente debe ser capaz de distinguir entre un guión bajo real `_ `y un guión `-`. Por lo tanto, en JCR, el guión debe reemplazarse por su valor Unicode (u002d) y evitarse con un guión bajo `_`.

Por ejemplo, si la ruta del repositorio es **/apps/my-example/component/info/Info.java**, el nombre del paquete debe ser `java package apps.my_002dexample.component.info;`

Observe que se debe escapar un guión bajo de forma similar, de modo que `_` se convierte `_005f`.
