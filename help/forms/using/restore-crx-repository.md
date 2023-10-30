---
title: No se puede restaurar el repositorio CRX dañado aplicable al servidor de clúster JEE
description: Pasos para restaurar el repositorio CRX dañado.
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 8%

---

# No se puede restaurar el repositorio CRX dañado {#unable-to-restore-corrupt-crx-repository}

## Problema {#issue}

Para AEM Forms en JEE que utiliza una base de datos relacional, la hora en el equipo que aloja AEM Forms y la base de datos relacional siempre deben estar en sincronización absoluta. Si el tiempo en estos equipos no está sincronizado, es posible que no se pueda acceder al repositorio CRX de AEM Forms en el servidor JEE. Puede parecer corrupto y volverse inaccesible a través de la URL. El `AuthenticationsupportService missing` se registra el error.

## Requisitos previos {#prerequisites}

Realice la copia de seguridad del repositorio CRX antes de realizar los pasos mencionados a continuación.

## Solución {#solution}

Siga estos pasos para resolver el problema:
1. Vaya a  `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. Busque el `oak-core` paquete y compruebe si se está ejecutando.

1. Reinicie el `oak-core` paquete si no se está ejecutando. If  ![Botón Pausa](/help/forms/using/assets/stop.png) está presente delante de la etiqueta `oak-core` paquete, entonces indica que el paquete está en estado de ejecución.

1. Si el problema aún no se resuelve, restaure desde el repositorio CRX desde la copia de seguridad o vuelva a compilar el repositorio CRX si la copia de seguridad no está disponible.


## Aplicable a {#applies-to}

Esta solución se aplica a:

* AEM Forms en clúster JEE