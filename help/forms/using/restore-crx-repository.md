---
title: No se puede restaurar el repositorio CRX dañado aplicable al servidor de clúster JEE
description: Conozca los pasos sobre cómo restaurar un repositorio CRX que esté dañado.
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---

# No se puede restaurar el repositorio CRX dañado {#unable-to-restore-corrupt-crx-repository}

## Problema {#issue}

Para AEM Forms en JEE que utiliza una base de datos relacional, la hora en el equipo que aloja AEM Forms y la base de datos relacional siempre deben estar en sincronización absoluta. Si el tiempo en estos equipos no está sincronizado, es posible que no se pueda acceder al repositorio CRX de AEM Forms en el servidor JEE. Puede parecer corrupto y volverse inaccesible a través de la URL. El `AuthenticationsupportService missing` se registra el error.

## Requisitos previos {#prerequisites}

Realice la copia de seguridad del repositorio CRX antes de realizar los pasos mencionados a continuación.

## Solución {#solution}

1. Ir a  `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. Busque el `oak-core` paquete y compruebe si se está ejecutando.

1. Reinicie el `oak-core` paquete si no se está ejecutando. If  ![Botón Pausa](/help/forms/using/assets/stop.png) está presente delante de la etiqueta `oak-core` paquete, entonces indica que el paquete está en estado de ejecución.

1. Si el problema aún no se resuelve, restaure desde el repositorio CRX desde la copia de seguridad o vuelva a compilar el repositorio CRX si la copia de seguridad no está disponible.


## Aplicable a {#applies-to}

Esta solución se aplica a AEM Forms en el clúster de JEE.
