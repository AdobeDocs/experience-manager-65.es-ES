---
title: Inicio y parada de WebSphere Application Server
seo-title: Inicio y parada de WebSphere Application Server
description: Varios procedimientos requieren que detenga o inicio la instancia de WebSphere en la que desea implementar productos de formularios AEM. Este documento describe cómo realizar el inicio y detener el servidor de aplicaciones WebSphere.
seo-description: Varios procedimientos requieren que detenga o inicio la instancia de WebSphere en la que desea implementar productos de formularios AEM. Este documento describe cómo realizar el inicio y detener el servidor de aplicaciones WebSphere.
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
translation-type: tm+mt
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# Inicio y parada de WebSphere Application Server {#starting-and-stopping-websphere-application-server}

Varios procedimientos requieren que detenga o inicio la instancia de WebSphere en la que desea implementar productos de formularios AEM. Si no está seguro de si el servidor de aplicaciones se ha iniciado, primero puede vista el estado de WebSphere Application Server.

## Vista del estado de WebSphere Application Server {#view-the-status-of-websphere-application-server}

1. Desde un símbolo del sistema, vaya al directorio `[appserver root]/bin`.
1. Introduzca el siguiente comando, reemplazando *server_name* por el nombre de su servidor de aplicaciones WebSphere:

   * (Windows) `serverStatus.bat`*nombre_servidor*
   * (Linux, UNIX) ./ `serverStatus.sh`*nombre_servidor*

## Servidor de aplicaciones WebSphere de inicio {#start-websphere-application-server}

1. Desde un símbolo del sistema, vaya al directorio `[appserver root]/bin`.
1. Introduzca el siguiente comando, reemplazando *server_name* por el nombre de su servidor de aplicaciones WebSphere:

   * (Windows) `startServer.bat`*nombre_servidor*
   * (Linux, UNIX) ./ `startServer.sh`*nombre_servidor*

## Detener el servidor de aplicaciones WebSphere {#stop-websphere-application-server}

1. Desde un símbolo del sistema, vaya al directorio `[appserver root]/bin`.
1. Introduzca el siguiente comando, reemplazando *server_name* por el nombre de su servidor de aplicaciones WebSphere:

   * (Windows) `stopServer.bat`*nombre_servidor*
   * (Linux, UNIX) ./ `stopServer.sh`*nombre_servidor*

