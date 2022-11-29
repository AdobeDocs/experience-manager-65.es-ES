---
title: No se puede restaurar el repositorio CRX dañado aplicable al servidor de clúster JEE
description: Pasos para restaurar el repositorio CRX dañado
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
source-git-commit: c4f776b08cb8cc8c6eea78a3757735e063bec20c
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---

# No se puede restaurar el repositorio CRX dañado {#unable-to-restore-corrupt-crx-repository}

## Problema {#issue}

Para AEM Forms en JEE que utiliza una base de datos relacional, el tiempo en el equipo que aloja AEM Forms y la base de datos relacional siempre debe estar en sincronización absoluta. Si el tiempo en estos equipos se desincroniza, el repositorio CRX de AEM Forms en el servidor JEE puede volverse inaccesible. Puede parecer corrupto y resultar inaccesible a través de la dirección URL. La variable `AuthenticationsupportService missing` se registra.

## Requisitos previos {#prerequisites}

Realice la copia de seguridad de su repositorio CRX antes de realizar los pasos que se mencionan a continuación.

## Solución {#solution}

Siga estos pasos para resolver el problema:
1. Vaya a  `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. Busque la variable `oak-core` paquete y compruebe si se está ejecutando.

1. Reinicie el `oak-core` paquete si no se está ejecutando. If  ![Botón Pausar](/help/forms/using/assets/stop.png) está presente delante de `oak-core` paquete, entonces indica que el paquete está en estado de ejecución.

1. Si el problema aún no se ha resuelto, restaure desde el repositorio CRX desde la copia de seguridad o reconstruya el repositorio CRX si la copia de seguridad no está disponible.


## Se aplica a {#applies-to}

Esta solución se aplica a:

* AEM Forms en clúster JEE