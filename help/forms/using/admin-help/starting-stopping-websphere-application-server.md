---
title: Iniciar y detener del servidor de aplicaciones WebSphere
description: AEM Varios procedimientos requieren que detenga o inicie la instancia de WebSphere en la que desea implementar productos de formularios de la forma que desee. Este documento describe cómo iniciar y detener el servidor de aplicaciones WebSphere.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 6%

---

# Iniciar y detener del servidor de aplicaciones WebSphere {#starting-and-stopping-websphere-application-server}

AEM Varios procedimientos requieren que detenga o inicie la instancia de WebSphere en la que desea implementar productos de formularios de la forma que desee. Si no está seguro de si el servidor de aplicaciones se ha iniciado, puede ver primero el estado del servidor de aplicaciones de WebSphere.

## Ver el estado del servidor de aplicaciones WebSphere {#view-the-status-of-websphere-application-server}

1. Desde un símbolo del sistema, vaya a `[appserver root]/bin` directorio.
1. Introduzca el siguiente comando, sustituyendo *server_name* con el nombre de su servidor de aplicaciones WebSphere:

   * (Windows) `serverStatus.bat`*server_name*
   * (Linux, UNIX) ./ `serverStatus.sh`*server_name*

## Iniciar el servidor de aplicaciones WebSphere {#start-websphere-application-server}

1. Desde un símbolo del sistema, vaya a `[appserver root]/bin` directorio.
1. Introduzca el siguiente comando, sustituyendo *server_name* con el nombre de su servidor de aplicaciones WebSphere:

   * (Windows) `startServer.bat`*server_name*
   * (Linux, UNIX) ./ `startServer.sh`*server_name*

## Detener el servidor de aplicaciones WebSphere {#stop-websphere-application-server}

1. Desde un símbolo del sistema, vaya a `[appserver root]/bin` directorio.
1. Introduzca el siguiente comando, sustituyendo *server_name* con el nombre de su servidor de aplicaciones WebSphere:

   * (Windows) `stopServer.bat`*server_name*
   * (Linux, UNIX) ./ `stopServer.sh`*server_name*
