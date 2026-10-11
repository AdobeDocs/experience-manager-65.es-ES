---
title: Iniciar y detener del servidor de aplicaciones WebSphere
description: Varios procedimientos requieren que detenga o inicie la instancia de WebSphere en la que desea implementar productos de formularios AEM Forms. Este documento describe cómo iniciar y detener el servidor de aplicaciones WebSphere.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 6%
---
# Iniciar y detener del servidor de aplicaciones WebSphere {#starting-and-stopping-websphere-application-server}

Varios procedimientos requieren que detenga o inicie la instancia de WebSphere en la que desea implementar productos de formularios AEM Forms. Si no está seguro de si el servidor de aplicaciones se ha iniciado, puede ver primero el estado del servidor de aplicaciones de WebSphere.

## Ver el estado del servidor de aplicaciones WebSphere {#view-the-status-of-websphere-application-server}

1. Desde un símbolo del sistema, vaya al directorio `[appserver root]/bin`.
1. Introduzca el siguiente comando y reemplace *server_name* por el nombre de su servidor de aplicaciones de WebSphere:

   * (Windows) `serverStatus.bat`*nombre_servidor*
   * (Linux, UNIX) ./ `serverStatus.sh`*nombre_servidor*

## Iniciar el servidor de aplicaciones WebSphere {#start-websphere-application-server}

1. Desde un símbolo del sistema, vaya al directorio `[appserver root]/bin`.
1. Introduzca el siguiente comando y reemplace *server_name* por el nombre de su servidor de aplicaciones de WebSphere:

   * (Windows) `startServer.bat`*nombre_servidor*
   * (Linux, UNIX) ./ `startServer.sh`*nombre_servidor*

## Detener el servidor de aplicaciones WebSphere {#stop-websphere-application-server}

1. Desde un símbolo del sistema, vaya al directorio `[appserver root]/bin`.
1. Introduzca el siguiente comando y reemplace *server_name* por el nombre de su servidor de aplicaciones de WebSphere:

   * (Windows) `stopServer.bat`*nombre_servidor*
   * (Linux, UNIX) ./ `stopServer.sh`*nombre_servidor*
