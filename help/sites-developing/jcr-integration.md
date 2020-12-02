---
title: Integración de JCR
seo-title: Integración de JCR
description: Sugerencias sobre cuándo debe integrarse en el nivel JCR
seo-description: Sugerencias sobre cuándo debe integrarse en el nivel JCR
uuid: 11518baf-521e-471d-ad4f-2baa76075cfa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: e6647a11-a36e-4808-bb61-29b2895c6b1d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# Integración de JCR{#jcr-integration}

## Preferir la API de recursos de Sling a la API de JCR {#prefer-the-sling-resource-api-to-jcr-api}

La API de Sling funciona en un nivel más alto y abstracto que la API de JCR. Esto permite que el código sea más reutilizable e independiente del almacenamiento subyacente. Esto facilita la inclusión de datos virtuales externos a través del mecanismo ResourceProvider si es necesario.

## Evite consultas siempre que sea posible {#avoid-queries-wherever-possible}

Siempre es más rápido navegar por el repositorio para recuperar datos que ejecutar una consulta. Hay casos en los que serán necesarias consultas, como una consulta de usuario final o la necesidad de encontrar contenido estructurado en todo el repositorio, pero en todos los demás casos, es preferible navegar a los nodos necesarios. Siempre se deben evitar consultas en la lógica de procesamiento, como componentes de navegación, una &quot;lista de elementos recientes&quot;, recuentos de elementos, etc. En estos casos, es mejor recorrer la jerarquía o prealmacenar el resultado para que se pueda utilizar directamente cuando se procese.

## Restringir el alcance de la observación JCR {#restrict-the-scope-of-jcr-observation}

Al escuchar eventos en el repositorio, es importante reducir el ámbito tanto como sea posible. Por ejemplo, es mucho mejor escuchar un evento en `/etc/mycompany` que en `/etc`. Nunca escuche eventos en la raíz del repositorio. Además, asegúrese de que los métodos de llamada de retorno se ejecutan lo más rápido posible cuando no hay nada que hacer.

## Elimine el uso del acceso de administración de JCR {#eliminate-use-of-jcr-admin-access}

A partir del AEM 6, el inicio de sesión en Administración ha quedado obsoleto, al igual que obtener una sesión administrativa de ResourceResolverFactory. En su lugar, se deben crear cuentas de servicio para las operaciones de back-office que requieran este tipo de acceso y ResourceResolverFactory se puede utilizar para obtener un ResourceResolver para esta cuenta.
