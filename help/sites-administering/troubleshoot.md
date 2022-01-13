---
title: Solución de problemas AEM
seo-title: Troubleshooting AEM
description: Obtenga información sobre la resolución de problemas con AEM.
seo-description: Learn about troubleshooting issues with AEM.
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
exl-id: d2d351e7-87a5-4895-b4ec-391fb0b66798
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 11%

---

# Solución de problemas AEM {#troubleshooting-aem}

La siguiente sección cubre algunos problemas que pueden producirse al utilizar AEM, así como sugerencias para solucionarlos.

>[!NOTE]
>
>Si está solucionando problemas de creación en AEM, consulte [Resolución de problemas para autores.](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>Si está experimentando problemas, puede consultar la lista de [Problemas conocidos](/help/release-notes/release-notes.md) de su instancia (versión y Service Packs).

## Situaciones de solución de problemas para administradores {#troubleshooting-scenarios-for-administrators}

La siguiente tabla proporciona una descripción general de los problemas que los administradores pueden necesitar para solucionar:

<table>
 <tbody>
  <tr>
   <td><strong>Funciones</strong></td>
   <td><strong>Problema </strong></td>
  </tr>
  <tr>
   <td>Administrador del sistema</td>
   <td><p>Hacer doble clic en el jar de inicio rápido no tiene ningún efecto o abre el archivo jar con otro programa (por ejemplo, el administrador de archivos)</p> </td>
  </tr>
  <tr>
   <td><p>Administrador del sistema</p> </td>
   <td><p>Mi aplicación que se ejecuta en CRX arroja errores de memoria insuficiente</p> </td>
  </tr>
  <tr>
   <td><p>Administrador del sistema</p> </td>
   <td><p>La pantalla de bienvenida de AEM no se muestra en el explorador después de hacer doble clic en AEM inicio rápido de CM</p> </td>
  </tr>
  <tr>
   <td><p>Administrador del sistema</p> <p>usuario administrador</p> </td>
   <td><p>Realización de un volcado de subprocesos</p> </td>
  </tr>
  <tr>
   <td><p>Administrador del sistema</p> <p>usuario administrador</p> </td>
   <td><p>Comprobación de sesiones JCR no cerradas</p> </td>
  </tr>
 </tbody>
</table>

## Problemas de instalación {#installation-issues}

Consulte [Problemas comunes de instalación](/help/sites-deploying/troubleshooting.md#common-installation-issues) para obtener información sobre los siguientes escenarios de solución de problemas:

* Cuando se hace doble clic en el archivo JAR de inicio rápido, no sucede nada o el archivo se abre con otro programa (como un gestor de archivos).
* Las aplicaciones que se ejecutan en CRX devuelven errores de memoria insuficiente.
* La pantalla de bienvenida de AEM no se muestra en el navegador después de hacer doble clic en el inicio rápido de AEM.

## Métodos para el análisis de resolución de problemas {#methods-for-troubleshooting-analysis}

### Realización de un volcado de subprocesos {#making-a-thread-dump}

El volcado de subprocesos es una lista de todos los subprocesos Java que están activos actualmente. Si AEM no responde correctamente, el volcado de subprocesos puede ayudarle a identificar interbloqueos u otros problemas.

### Uso del vaciador de subprocesos de Sling {#using-sling-thread-dumper}

1. Abra el **Consola web AEM**; por ejemplo, en `https://localhost:4502/system/console/`.
1. Seleccione el **Subprocesos** under **Estado** pestaña .

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### Uso de jstack (línea de comandos) {#using-jstack-command-line}

1. Busque el PID (id de proceso) de la instancia de Java AEM.

   Por ejemplo, puede utilizar `ps -ef` o `jps`.

1. Ejecución:

   `jstack <pid>`

1. Esto mostrará el volcado de subprocesos.

>[!NOTE]
>
>Puede anexar los volcados de subprocesos a un archivo de registro utilizando la variable `>>` redirección de salida:
>
>`jstack <pid> >> /path/to/logfile.log`

Consulte la [Cómo tomar volcados de subprocesos de una JVM](https://helpx.adobe.com/cq/kb/TakeThreadDump.html) documentación para obtener más información

### Comprobación de sesiones JCR no cerradas {#checking-for-unclosed-jcr-sessions}

Cuando se desarrolla la funcionalidad para AEM WCM, se pueden abrir sesiones JCR (comparables a la apertura de una conexión de base de datos). Si las sesiones abiertas nunca se cierran, su sistema puede experimentar los siguientes síntomas:

* El sistema se vuelve más lento.
* Se puede ver un montón de CacheManager: resizeAll entradas en el archivo de registro; el siguiente número (size=&lt;x>) muestra el número de cachés, cada sesión abre varias cachés.
* De vez en cuando el sistema se queda sin memoria (después de unas horas, días o semanas, dependiendo de la gravedad).

Para analizar sesiones no cerradas y averiguar qué código no está cerrando una sesión, consulte el artículo de la Base de conocimiento [Analizar sesiones no cerradas](https://helpx.adobe.com/crx/kb/AnalyzeUnclosedSessions.html).

### Uso de la consola web de Adobe Experience Manager {#using-the-adobe-experience-manager-web-console}

El estado de los paquetes OSGi también puede proporcionar una indicación temprana de posibles problemas.

1. Abra el **Consola web AEM**; por ejemplo, en `https://localhost:4502/system/console/`.
1. Select **Paquetes** under **OSGI** pestaña .
1. Comprobar:

   * el estado de los paquetes. Si alguno está inactivo o insatisfecho, intente detener y reiniciar el paquete. Si el problema persiste, es posible que tenga que investigar más usando otros métodos.
   * si faltan dependencias en alguno de los paquetes. Estos detalles se pueden ver haciendo clic en el nombre del paquete individual, que es un vínculo (el siguiente ejemplo no tiene ningún problema):

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
