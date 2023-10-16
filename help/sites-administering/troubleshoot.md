---
title: Solución de problemas de Adobe Experience Manager
description: Obtenga información sobre la resolución de algunos problemas que pueden surgir con Adobe Experience Manager.
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
exl-id: d2d351e7-87a5-4895-b4ec-391fb0b66798
source-git-commit: 3400df1ecd545aa0fb0e3fcdcc24f629ce4c99ba
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 3%

---

# Solución de problemas de Adobe Experience Manager {#troubleshooting-aem}

AEM En la siguiente sección se tratan algunos problemas que pueden producirse al utilizar la solución de problemas de (Adobe Experience Manager), junto con sugerencias para solucionarlos.

>[!NOTE]
>
>AEM Si está solucionando problemas relacionados con la creación de documentos en la documentación de, consulte la sección [Solución de problemas para autores.](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>Cuando experimenta problemas, también vale la pena comprobar la lista de [Problemas conocidos](/help/release-notes/release-notes.md) para su instancia (versión y paquetes de servicio).

## Escenarios de resolución de problemas para administradores {#troubleshooting-scenarios-for-administrators}

En la tabla siguiente se proporciona una descripción general de los problemas que los administradores pueden solucionar:

<table>
 <tbody>
  <tr>
   <td><strong>Función</strong></td>
   <td><strong>Problema </strong></td>
  </tr>
  <tr>
   <td>Administrador del sistema</td>
   <td><p>Al hacer doble clic en el JAR de inicio rápido no se produce ningún efecto o se abre el archivo JAR con otro programa (por ejemplo, archive manager)</p> </td>
  </tr>
  <tr>
   <td><p>Administrador del sistema</p> </td>
   <td><p>Mi aplicación que se ejecuta en CRX genera errores de memoria insuficiente</p> </td>
  </tr>
  <tr>
   <td><p>Administrador del sistema</p> </td>
   <td><p>AEM AEM La pantalla de bienvenida de la pantalla no se muestra en el explorador después de hacer doble clic en Inicio rápido de CM de la</p> </td>
  </tr>
  <tr>
   <td><p>Administrador del sistema</p> <p>usuario administrador</p> </td>
   <td><p>Realización de un volcado de procesos</p> </td>
  </tr>
  <tr>
   <td><p>Administrador del sistema</p> <p>usuario administrador</p> </td>
   <td><p>Comprobación de sesiones JCR sin cerrar</p> </td>
  </tr>
 </tbody>
</table>

## Problemas de instalación {#installation-issues}

Consulte [Problemas comunes de instalación](/help/sites-deploying/troubleshooting.md#common-installation-issues) para obtener información sobre los siguientes escenarios de solución de problemas:

* Hacer doble clic en el JAR de inicio rápido no tiene efecto o el archivo JAR con otro programa (como el administrador de archivos).
* Las aplicaciones que se ejecutan en CRX generan errores de memoria insuficiente.
* AEM AEM La pantalla de bienvenida de la pantalla no se muestra en el explorador después de hacer doble clic en el inicio rápido de la aplicación de la.

## Métodos para el análisis de resolución de problemas {#methods-for-troubleshooting-analysis}

### Realización de un volcado de procesos {#making-a-thread-dump}

El volcado de hilos es una lista de todos los hilos Java™ que están activos actualmente. AEM Si el volcado de hilos no responde correctamente, el volcado de hilos puede ayudarle a identificar interbloqueos u otros problemas.

### Uso del volcado de hilos Sling {#using-sling-thread-dumper}

1. Abra el **AEM Consola web de**; por ejemplo, en `https://localhost:4502/system/console/`.
1. Seleccione el **Threads** bajo **Estado** pestaña.

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### Uso de jstack (línea de comandos) {#using-jstack-command-line}

1. AEM Busque el PID (ID de proceso) de la instancia de Java™ de la.

   Por ejemplo, puede utilizar `ps -ef` o `jps`.

1. Ejecución:

   `jstack <pid>`

1. Muestra el volcado de hilos.

>[!NOTE]
>
>Puede anexar los volcados de procesos a un archivo de registro utilizando el `>>` redirección de salida:
>
>`jstack <pid> >> /path/to/logfile.log`

Consulte la [Cómo tomar volcados de procesos de una JVM](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html?lang=es) para obtener más información

### Comprobación de sesiones JCR sin cerrar {#checking-for-unclosed-jcr-sessions}

AEM Cuando la funcionalidad está desarrollada para WCM, se pueden abrir sesiones JCR (comparables a la apertura de una conexión a base de datos). Si las sesiones abiertas nunca se cierran, su sistema puede experimentar los siguientes síntomas:

* El sistema se vuelve más lento.
* Puede ver gran parte de CacheManager: resizeAll entradas en el archivo de registro; el siguiente número (size=&lt;x>) muestra el número de cachés, cada sesión abre varias cachés.
* De vez en cuando, el sistema se queda sin memoria (después de unas pocas horas, días o semanas, según la gravedad).

Para analizar las sesiones no cerradas y averiguar qué código no cierra una sesión, consulte el artículo de la Base de conocimiento [Analizar sesiones no cerradas](https://helpx.adobe.com/experience-manager/kb/AnalyzeUnclosedSessions.html).

### Uso de la consola web de Adobe Experience Manager {#using-the-adobe-experience-manager-web-console}

El estado de los paquetes OSGi también puede proporcionar una indicación temprana de posibles problemas.

1. Abra el **AEM Consola web de**; por ejemplo, en `https://localhost:4502/system/console/`.
1. Seleccionar **Paquetes** bajo **OSGI** pestaña.
1. Comprobación:

   * el estado de los paquetes. Si alguno de ellos está Inactivo o Insatisfecho, intente detener y reiniciar el paquete. Si el problema persiste, investigue más a fondo con otros métodos.
   * si alguno de los paquetes tiene dependencias que faltan. Estos detalles se pueden ver haciendo clic en el Nombre del paquete individual, que es un vínculo (el siguiente ejemplo no tiene ningún problema):

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
