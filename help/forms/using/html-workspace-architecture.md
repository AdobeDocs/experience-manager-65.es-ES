---
title: Arquitectura de AEM Forms Workspace
description: Información conceptual y descripción general de la arquitectura de LiveCycle AEM Forms Workspace.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: c6f216d4-781c-4356-b9f0-3324903a28e7
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
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
source-wordcount: '220'
ht-degree: 100%
---
# Arquitectura de AEM Forms Workspace {#aem-forms-workspace-architecture}

AEM Forms Workspace es una aplicación web alojada en CRX™. Cuando se abre Workspace en un explorador, se accede a un recurso CRX y la aplicación se representa como una página HTML en el explorador.

La aplicación accede al servidor de AEM Forms en los extremos REST para hacer lo siguiente:

* Buscar tareas de usuario, puntos de inicio de procesos, historial de procesos e información de usuarios
* Realizar acciones en tareas
* Consultar tareas en la base de datos
* Actualizar las preferencias de usuario y mucho más

El servidor de AEM Forms accede a la base de datos de AEM Forms a través de JDBC. La base de datos mantiene las tareas, los procesos y sus instancias, los usuarios y la información relacionada.

AEM Forms Workspace está diseñado en componentes modulares JavaScript™ que pueden personalizarse y reutilizarse de forma individual en otras aplicaciones web. Los componentes se basan en BackBone, que es una biblioteca JavaScript que da estructura a las aplicaciones web. En el siguiente [enlace](/help/forms/using/backbone-interaction.md) encontrará un artículo detallado que describe la interacción de los componentes con BackBone. [Este](/help/forms/using/folder-structure.md) artículo explica la organización de los componentes en la estructura de carpetas CRX.

Paquetes entregados para AEM Forms Workspace:

* `adobe-lc-workspace-pkg-<version>.zip`: es un paquete CRX, es decir, se puede implementar en CRX usando el Administrador de paquetes.
* `adobe-lc-workspace-<version>-src.zip`: es un archivo que contiene el código completo de AEM Forms Workspace y los scripts para crear los paquetes de implementación: los paquetes Ship, Debug y Dev.
