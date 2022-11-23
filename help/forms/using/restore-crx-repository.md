---
title: No se puede restaurar el repositorio CRX dañado aplicable al servidor de clúster JEE
description: Pasos para restaurar el repositorio CRX dañado
source-git-commit: a7d125503b0bd3c52cb3a959e2f0dde1a69cbe2b
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 5%

---

# No se puede restaurar el repositorio CRX dañado {#unable-to-restore-corrupt-crx-repository}

## Problema {#issue}

Para AEM Forms implementado en JEE con persistencia de RDB, es necesario que los equipos host de AEM Forms y los equipos de base de datos estén sincronizados en tiempo absoluto. Sin embargo, si por alguna razón los relojes salen de la sincronización, el repositorio CRX se corrompe y sus URL se vuelven inaccesibles. El error como `AuthenticationsupportService missing` se produce en archivos de registro.

## Solución {#solution}

Siga estos pasos para resolver el problema:
1. Vaya a  [https://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).

1. Busque la variable `oak-core` paquete y compruebe si se está ejecutando.

1. Reinicie el `oak-core` paquete si no se está ejecutando. Si el botón de pausa está presente delante del `oak-core` paquete, entonces indica que el paquete está en estado de ejecución.

1. Si el problema aún no se ha resuelto, restaure desde el repositorio CRX desde la copia de seguridad o reconstruya el repositorio CRX si la copia de seguridad no está disponible.

   >[!NOTE]
   >
   >Realice la copia de seguridad de su repositorio CRX antes de realizar los pasos anteriores.

## Se aplica a {#applies-to}

Esta solución se aplica a:

* AEM Forms en JEE Cluster Server


