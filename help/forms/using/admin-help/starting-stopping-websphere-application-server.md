---
title: Inicio y parada del servidor de aplicaciones WebSphere
seo-title: Starting and stopping WebSphere Application Server
description: Varios procedimientos requieren que detenga o inicie la instancia de WebSphere donde desee implementar productos de formularios AEM. En este documento se describe cómo iniciar y detener el servidor de aplicaciones WebSphere.
seo-description: Several procedures require you to stop or start the instance of WebSphere where you want to deploy AEM forms products. This document describes how to start and stop the WebSphere Application Server.
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Inicio y parada del servidor de aplicaciones WebSphere {#starting-and-stopping-websphere-application-server}

Varios procedimientos requieren que detenga o inicie la instancia de WebSphere donde desee implementar productos de formularios AEM. Si no está seguro de si el servidor de aplicaciones se ha iniciado, primero puede ver el estado de WebSphere Application Server.

## Ver el estado del servidor de aplicaciones WebSphere {#view-the-status-of-websphere-application-server}

1. Desde un símbolo del sistema, vaya a la `[appserver root]/bin` directorio.
1. Introduzca el siguiente comando, sustituyendo *server_name* con el nombre de su servidor de aplicaciones WebSphere:

   * (Windows) `serverStatus.bat`*server_name*
   * (Linux, UNIX) ./ `serverStatus.sh`*server_name*

## Iniciar servidor de aplicaciones WebSphere {#start-websphere-application-server}

1. Desde un símbolo del sistema, vaya a la `[appserver root]/bin` directorio.
1. Introduzca el siguiente comando, sustituyendo *server_name* con el nombre de su servidor de aplicaciones WebSphere:

   * (Windows) `startServer.bat`*server_name*
   * (Linux, UNIX) ./ `startServer.sh`*server_name*

## Detener el servidor de aplicaciones WebSphere {#stop-websphere-application-server}

1. Desde un símbolo del sistema, vaya a la `[appserver root]/bin` directorio.
1. Introduzca el siguiente comando, sustituyendo *server_name* con el nombre de su servidor de aplicaciones WebSphere:

   * (Windows) `stopServer.bat`*server_name*
   * (Linux, UNIX) ./ `stopServer.sh`*server_name*
