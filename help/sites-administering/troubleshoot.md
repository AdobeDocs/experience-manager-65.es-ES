---
title: Solución de problemas de AEM
seo-title: Solución de problemas de AEM
description: Obtenga información sobre la resolución de problemas con AEM.
seo-description: Obtenga información sobre la resolución de problemas con AEM.
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538

---


# Solución de problemas de AEM {#troubleshooting-aem}

En la siguiente sección se explican algunos problemas que puede encontrar al utilizar AEM, así como sugerencias sobre cómo solucionarlos.

>[!NOTE]
>
>Si está solucionando problemas de creación en AEM, consulte [Solución de problemas de creación.](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>Si está experimentando problemas, puede consultar la lista de [Problemas conocidos](/help/release-notes/known-issues.md) de su instancia (versión y Service Packs).

## Resolución de problemas para administradores {#troubleshooting-scenarios-for-administrators}

En la tabla siguiente se proporciona una descripción general de los problemas que los administradores pueden necesitar para solucionar:

<table>
 <tbody>
  <tr>
   <td><strong>Funciones</strong></td>
   <td><strong>Problema </strong></td>
  </tr>
  <tr>
   <td>Administrador de sistemas</td>
   <td><p>Al hacer doble clic en el frasco de inicio rápido no se produce ningún efecto o se abre el archivo jar con otro programa (por ejemplo, el administrador de archivos)</p> </td>
  </tr>
  <tr>
   <td><p>Administrador de sistemas</p> </td>
   <td><p>Mi aplicación que se ejecuta en CRX genera errores de memoria insuficiente</p> </td>
  </tr>
  <tr>
   <td><p>Administrador de sistemas</p> </td>
   <td><p>La pantalla de bienvenida de AEM no se muestra en el navegador después de hacer doble clic en Inicio rápido de AEM CM</p> </td>
  </tr>
  <tr>
   <td><p>Administrador de sistemas</p> <p>admin user</p> </td>
   <td><p>Realización de un volcado de subprocesos</p> </td>
  </tr>
  <tr>
   <td><p>Administrador de sistemas</p> <p>admin user</p> </td>
   <td><p>Comprobación de sesiones JCR no cerradas</p> </td>
  </tr>
 </tbody>
</table>

## Problemas de instalación {#installation-issues}

Consulte [Problemas](/help/sites-deploying/troubleshooting.md#common-installation-issues) comunes de instalación para obtener información sobre los siguientes escenarios de solución de problemas:

* Cuando se hace doble clic en el archivo JAR de inicio rápido, no sucede nada o el archivo se abre con otro programa (como un gestor de archivos).
* Las aplicaciones que se ejecutan en CRX devuelven errores de memoria insuficiente.
* La pantalla de bienvenida de AEM no se muestra en el navegador después de hacer doble clic en el inicio rápido de AEM.

## Métodos para el análisis de resolución de problemas {#methods-for-troubleshooting-analysis}

### Realización de un volcado de subprocesos {#making-a-thread-dump}

El volcado de subprocesos es una lista de todos los subprocesos de Java que están activos actualmente. Si AEM no responde correctamente, el volcado de subprocesos puede ayudarle a identificar interbloqueos u otros problemas.

### Uso del tapón de rosca Sling {#using-sling-thread-dumper}

1. Abra la consola **web de** AEM; por ejemplo, en `https://localhost:4502/system/console/`.
1. Seleccione los **hilos** en **la ficha Estado** .

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### Uso de jstack (línea de comandos) {#using-jstack-command-line}

1. Busque el PID (id. de proceso) de la instancia de AEM Java.

   Por ejemplo, puede usar `ps -ef` o `jps`.

1. Ejecutar:

   `jstack <pid>`

1. Esto mostrará el volcado de subprocesos.

>[!NOTE]
>
>Puede anexar los volcados de subproceso a un archivo de registro utilizando la redirección de salida `>>` :
>
>`jstack <pid> >> /path/to/logfile.log`

Consulte la documentación de [Cómo tomar descargas de subprocesos de una JVM](https://helpx.adobe.com/cq/kb/TakeThreadDump.html) para obtener más información

### Comprobación de sesiones JCR no cerradas {#checking-for-unclosed-jcr-sessions}

Cuando se desarrolla la funcionalidad para AEM WCM, se pueden abrir sesiones JCR (comparable a la apertura de una conexión de base de datos). Si las sesiones abiertas nunca se cierran, su sistema puede experimentar los siguientes síntomas:

* El sistema se vuelve más lento.
* Se puede ver un montón de CacheManager: resizeTodas las entradas del archivo de registro; el siguiente número (size=&lt;x>) muestra el número de cachés, cada sesión abre varias cachés.
* De vez en cuando el sistema se queda sin memoria (después de unas horas, días o semanas, según la gravedad).

Para analizar las sesiones no cerradas y averiguar qué código no cierra una sesión, consulte el artículo de la Base de conocimiento [Analizar sesiones](https://helpx.adobe.com/crx/kb/AnalyzeUnclosedSessions.html)no cerradas.

### Uso de la consola web de Adobe Experience Manager {#using-the-adobe-experience-manager-web-console}

El estado de los paquetes OSGi también puede dar una indicación temprana de los posibles problemas.

1. Abra la consola **web de** AEM; por ejemplo, en `https://localhost:4502/system/console/`.
1. Seleccione **Paquetes** en la ficha **OSGI** .
1. Comprobar:

   * el estado de los paquetes. Si alguno está inactivo o insatisfecho, intente detener y reiniciar el paquete. Si el problema persiste, es posible que tenga que investigar más a fondo usando otros métodos.
   * si alguno de los paquetes no tiene dependencias. Estos detalles se pueden ver haciendo clic en el nombre del paquete individual, que es un vínculo (el siguiente ejemplo no tiene ningún problema):

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)

