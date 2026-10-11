---
title: Leaderboard Essentials
description: Aprenda a configurar la puntuación y los distintivos de las comunidades para que pueda trabajar con el componente Tabla de posiciones en las comunidades de Adobe Experience Manager.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: fd1b1749-13f9-4079-ae39-348676105852
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 4%
---
# Leaderboard Essentials {#leaderboard-essentials}

Esta página proporciona información esencial para trabajar con la función de clasificación.

Antes de incluir el componente de tabla de clasificación en una página, es necesario configurar [insignias y puntuación de comunidades](implementing-scoring.md).

Ver [Aspectos básicos de puntuación e insignias](configure-scoring.md).

## Essentials para el lado del cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/gamification/components/hbs/clasificación</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluible</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.gamification.hbs.scoreboard</td>
  </tr>
  <tr>
   <td> <strong>plantillas</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/leaderboard.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/clientlibs/leaderboard.css</td>
  </tr>
  <tr>
   <td><strong> propiedades</strong></td>
   <td>Ver <a href="enabling-leaderboard.md">Característica de tabla de posiciones</a></td>
  </tr>
 </tbody>
</table>

* [Personalizaciones del lado del cliente](client-customize.md)

### Función Biblioteca del archivo {#file-library-function}

Una estructura de sitio de la comunidad que incluye la función [Tabla de posiciones](functions.md#leaderboard-function), incluye un componente `leaderboard` configurado.
