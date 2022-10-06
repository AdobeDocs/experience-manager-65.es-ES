---
title: Uso de registros
seo-title: Working with Logs
description: Obtenga información sobre cómo solucionar problemas de AEM trabajando con registros.
seo-description: Learn how to troubleshoot AEM by working with logs.
uuid: af8b7f50-c8d4-4760-9f00-3feb0b79ee4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: da92d751-6f14-4512-9d77-7ecf098bd58e
docset: aem65
exl-id: ab4fc41f-e0e9-4577-aab2-f0b4298f9a59
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 3%

---

# Uso de registros{#working-with-logs}

Esta sección incluye información detallada sobre los registros disponibles para ayudarle a solucionar el problema.

CRX registra registros detallados. Después de desempaquetar e iniciar QuickStart, puede encontrar los registros en las siguientes ubicaciones:

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## Activación del nivel de registro de depuración {#activating-the-debug-log-level}

El nivel de registro predeterminado es INFO, es decir, los mensajes DEBUG no se registran.

Para activar el nivel de registro de depuración, utilice el explorador CRX para establecer la variable

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

para depurar. No deje el registro en el nivel de registro DEBUG más tiempo del necesario, ya que genera muchos registros.

Una línea en el archivo de depuración normalmente comienza con DEBUG y, a continuación, proporciona el nivel de registro, la acción del instalador y el mensaje de registro. Por ejemplo:

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

Los niveles de registro son los siguientes:

| 0 | Error grave | La acción ha fallado y el instalador no puede continuar. |
|---|---|---|
| 1 | Error | La acción ha fallado. La instalación continúa, pero una parte de CRX no se instaló correctamente y no funcionará. |
| 2 | Advertencia | La acción se ha realizado correctamente, pero se han encontrado problemas. CRX puede o no funcionar correctamente. |
| 3 | Información | La acción se ha realizado correctamente. |

## Opción versbose utilizada para la resolución de problemas {#verbose-option-used-for-troubleshooting}

Cuando inicie CRX, puede agregar la opción -v (verbose) a la línea de comandos como en:

` java -jar crx-<*version*>-<*edition*>.jar -v`

Utilice la opción detallada para la resolución de problemas, ya que esta opción muestra algunos de los resultados del registro de inicio rápido en la consola.
