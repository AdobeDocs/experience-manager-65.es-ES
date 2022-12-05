---
title: Limitaciones de Dynamic Media
description: Obtenga información sobre las prácticas recomendadas y los límites aplicados al crear un conjunto de imágenes o un conjunto de giros, o al cargar un PDF. Además, obtenga información sobre las combinaciones de navegador web y sistema operativo no compatibles con Dynamic Media.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Image Sets,Spin Sets,eCatalog
role: User
exl-id: e4d4059e-ac0b-42e7-910c-001310796574
source-git-commit: 9604d950d33e1b5d32ba8141a35059c6e5787aeb
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 6%

---

# Limitaciones de Dynamic Media

En las secciones siguientes se describen las limitaciones de Dynamic Media.

Este tema incluye las siguientes secciones:

* [Prácticas recomendadas y límites aplicados por Dynamic Media en los tipos de recursos](#best-practice-enforced-limits)
* [Combinaciones de navegador web y sistema operativo no compatibles con Dynamic Media](#unsupported-browser-os)

## Prácticas recomendadas y límites aplicados por Dynamic Media en los tipos de recursos {#best-practice-enforced-limits}

Cuando se crea un conjunto de giros o un conjunto de imágenes, o se cargan PDF para la extracción de páginas, Adobe recomienda las siguientes prácticas recomendadas y aplica los límites siguientes:

| Recurso: tipo de límite | Práctica recomendada | Límite impuesto | Cambio al límite el 31 de diciembre de 2022 |
| --- | --- | --- | --- |
| **Imagen** - Número de recortes inteligentes por imagen | 5 | 100 | No aplicable |
| **Todos los conjuntos** - Número de activos duplicados por conjunto | Sin duplicados | 20 | No aplicable |
| **Todos los conjuntos** - Número máximo de activos por conjunto | 5 a 10 imágenes por conjunto | 1000 | No aplicable |
| **Conjunto de giros** - Número máximo de filas/columnas por conjunto 2D | 12 a 18 imágenes por conjunto | 1000 | No aplicable |
| **PDF** - Número máximo de páginas para un PDF a tener en cuenta para la extracción |  | 5000 (para nuevas cargas) | 100 (para todos los PDF) |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Combinaciones de navegador web y sistema operativo no compatibles con Dynamic Media {#unsupported-browser-os}

Dynamic Media no admite las siguientes combinaciones de navegador web y sistema operativo.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Actualización de Internet Explorer 11 + Windows Phone 8.1
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + OS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + OS X 10.10 Yosemite

<!-- ## End of support for TLS 1.0 and 1.1 {#tls}

CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022)

Effective September 30, 2022, Adobe Dynamic Media will end support for the following:

* TLS (Transport Layer Security) 1.0 and 1.1
* The following weak ciphers in TLS 1.2:
  * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
  * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
  * `TLS_RSA_WITH_AES_256_GCM_SHA384`
  * `TLS_RSA_WITH_AES_256_CBC_SHA256`
  * `TLS_RSA_WITH_AES_256_CBC_SHA`
  * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
  * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
  * `TLS_RSA_WITH_AES_128_GCM_SHA256`
  * `TLS_RSA_WITH_AES_128_CBC_SHA256`
  * `TLS_RSA_WITH_AES_128_CBC_SHA`
  * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
  * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
  * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
  * `TLS_RSA_WITH_SDES_EDE_CBC_SHA` -->

