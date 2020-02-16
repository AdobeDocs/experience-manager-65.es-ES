---
title: Inicio y parada de WebSphere Application Server
seo-title: Inicio y parada de WebSphere Application Server
description: Varios procedimientos requieren que detenga o inicie la instancia de WebSphere en la que desea implementar los productos de formularios AEM. Este documento describe cómo iniciar y detener el servidor de aplicaciones WebSphere.
seo-description: Varios procedimientos requieren que detenga o inicie la instancia de WebSphere en la que desea implementar los productos de formularios AEM. Este documento describe cómo iniciar y detener el servidor de aplicaciones WebSphere.
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Inicio y parada de WebSphere Application Server {#starting-and-stopping-websphere-application-server}

Varios procedimientos requieren que detenga o inicie la instancia de WebSphere en la que desea implementar los productos de formularios AEM. Si no está seguro de si el servidor de aplicaciones se ha iniciado, puede ver primero el estado de WebSphere Application Server.

## Ver el estado de WebSphere Application Server {#view-the-status-of-websphere-application-server}

1. Desde un símbolo del sistema, vaya al directorio raíz *[/bin de]* appserver.
1. Introduzca el siguiente comando, reemplazando *server_name* por el nombre de su servidor de aplicaciones WebSphere:

   * (Windows) `serverStatus.bat`*server_name *
   * (Linux, UNIX) ./ `serverStatus.sh`*server_name *

## Iniciar servidor de aplicaciones WebSphere {#start-websphere-application-server}

1. Desde un símbolo del sistema, vaya al directorio raíz *[/bin de]* appserver.
1. Introduzca el siguiente comando, reemplazando *server_name* por el nombre de su servidor de aplicaciones WebSphere:

   * (Windows) `startServer.bat`*server_name *
   * (Linux, UNIX) ./ `startServer.sh`*server_name *

## Detener servidor de aplicaciones WebSphere {#stop-websphere-application-server}

1. Desde un símbolo del sistema, vaya al directorio raíz *[/bin de]* appserver.
1. Introduzca el siguiente comando, reemplazando *server_name* por el nombre de su servidor de aplicaciones WebSphere:

   * (Windows) `stopServer.bat`*server_name *
   * (Linux, UNIX) ./ `stopServer.sh`*server_name *

