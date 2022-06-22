---
title: Limitaciones de Dynamic Media
description: 'Obtenga información sobre las prácticas recomendadas y los límites aplicados al crear un conjunto de imágenes o un conjunto de giros, o al cargar un PDF. Obtenga información también sobre las combinaciones de navegador web y sistema operativo no compatibles con los visores de Dynamic Media. '
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Viewers,Image Sets,Spin Sets,eCatalog
role: User
source-git-commit: cd3dcd0232e1ecf69c79b03ab960cfbfc283ee76
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 3%

---

# Limitaciones de Dynamic Media

En las secciones siguientes se describen las limitaciones de Dynamic Media.

Este tema incluye las siguientes secciones:

* Prácticas recomendadas y límites aplicados por Dynamic Media en los tipos de recursos

<!-- * Unsupported web browser and operating system combinations for Dynamic Media Viewers -->

## Prácticas recomendadas y límites aplicados por Dynamic Media en los tipos de recursos

Cuando se crea un conjunto de giros o un conjunto de imágenes, o se cargan PDF para la extracción de páginas, Adobe recomienda las siguientes prácticas recomendadas y aplica los límites siguientes:

| Recurso: tipo de límite | Práctica recomendada | Límite implementado | Cambios en el límite 31 de diciembre de 2022 |
| --- | --- | --- | --- |
| **Imagen** - Número de recortes inteligentes por imagen | 5 | 100 |  |
| **Conjunto de imágenes** - Número de activos duplicados por conjunto | Sin duplicados | 100 | 20 |
| **Conjunto de imágenes** - Número máximo de imágenes por conjunto | 5 a 10 imágenes por conjunto | 1000 |
| **Conjunto de giros** - Número máximo de filas/columnas por conjunto 2D | 12 a 18 imágenes por conjunto | 1000 |
| **PDF** - Número máximo de páginas para un PDF a tener en cuenta para la extracción |  | 5000 (para nuevas cargas) | 100 |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

<!-- ## Unsupported web browser and operating system combinations for Dynamic Media Viewers

Dynamic Media Viewers do not support following combinations of web browser and operating system.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1 Update
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + macOS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + macOS X 10.10 Yosemite -->