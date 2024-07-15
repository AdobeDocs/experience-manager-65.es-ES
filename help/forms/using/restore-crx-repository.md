---
title: No se puede restaurar el repositorio de CRX dañado aplicable al servidor de clúster JEE
description: Conozca los pasos sobre cómo restaurar un repositorio de CRX que esté dañado.
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---

# No se puede restaurar el repositorio de CRX dañado {#unable-to-restore-corrupt-crx-repository}

## Problema {#issue}

Para AEM Forms en JEE que utiliza una base de datos relacional, la hora en el equipo que aloja AEM Forms y la base de datos relacional siempre deben estar en sincronización absoluta. Si el tiempo en estos equipos no está sincronizado, es posible que no se pueda acceder al repositorio de CRX de AEM Forms en el servidor JEE. Puede parecer corrupto y volverse inaccesible a través de la URL. Se ha registrado el error `AuthenticationsupportService missing`.

## Requisitos previos {#prerequisites}

Realice la copia de seguridad del repositorio de CRX antes de realizar los pasos mencionados a continuación.

## Solución {#solution}

1. Ir a `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. Busque el paquete `oak-core` y compruebe si se está ejecutando.

1. Reinicie el paquete `oak-core` si no se está ejecutando. Si el icono ![Botón de pausa](/help/forms/using/assets/stop.png) está presente frente al paquete `oak-core`, entonces indica que el paquete se encuentra en estado de ejecución.

1. Si el problema sigue sin resolverse, restaure desde el repositorio de CRX desde la copia de seguridad o vuelva a compilar el repositorio de CRX si la copia de seguridad no está disponible.


## Aplicable a {#applies-to}

Esta solución se aplica a AEM Forms en el clúster de JEE.
