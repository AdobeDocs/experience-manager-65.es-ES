---
title: Uso de registros
description: AEM Obtenga información sobre cómo solucionar problemas de los registros de trabajo de la aplicación de.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: ab4fc41f-e0e9-4577-aab2-f0b4298f9a59
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 3%

---

# Uso de registros{#working-with-logs}

Esta sección incluye información detallada sobre los registros disponibles para ayudarle a solucionar problemas.

>[!NOTE]
>
>Para obtener más información sobre los registros, consulte:
>
>* AEM [Mantenimiento del registro de auditoría en el](/help/sites-administering/operations-audit-log.md)
>* [Trabajando con registros de auditoría y archivos de registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)

CRX registra los registros detallados. Después de desempaquetar e iniciar Quickstart, puede encontrar registros en las siguientes ubicaciones:

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## Activación del nivel de registro de depuración {#activating-the-debug-log-level}

El nivel de registro predeterminado es INFO, es decir, los mensajes de DEPURACIÓN no se registran.

Para activar el nivel de registro DEBUG, utilice el explorador de CRX para establecer el

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

propiedad para depurar. No deje el registro en el nivel de registro DEBUG más tiempo del necesario, ya que genera numerosos registros.

Una línea del archivo de depuración suele comenzar con DEBUG y, a continuación, proporciona el nivel de registro, la acción del instalador y el mensaje de registro. Por ejemplo:

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

Los niveles de registro son los siguientes:

| 0 | Error grave | La acción ha fallado y el instalador no puede continuar. |
|---|---|---|
| 1 | Error | La acción ha fallado. La instalación continúa, pero una parte de CRX no se instaló correctamente y no funcionará. |
| 2 | Advertencia | La acción se realizó correctamente pero se encontraron problemas. Es posible que CRX funcione o no correctamente. |
| 3 | Información | La acción se ha realizado correctamente. |

## Opción detallada utilizada para la resolución de problemas {#verbose-option-used-for-troubleshooting}

Al iniciar CRX, puede agregar la opción -v (detallada) a la línea de comandos como en:

` java -jar crx-<*version*>-<*edition*>.jar -v`

Utilice la opción detallada para la resolución de problemas, ya que esta opción muestra algunos de los resultados del registro de inicio rápido en la consola.
