---
title: Arquitectura de AEM Forms Workspace
seo-title: AEM Forms Workspace Architecture
description: Información conceptual y descripción general de la arquitectura del espacio de trabajo de LiveCycle AEM Forms.
seo-description: Conceptual information and overview of the architecture of LiveCycle AEM Forms workspace.
uuid: e1a48452-ed44-4ea7-ba38-d961c8faafa5
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c3a312fb-f684-477d-916d-2d3c99aa7607
exl-id: c6f216d4-781c-4356-b9f0-3324903a28e7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Arquitectura de AEM Forms Workspace {#aem-forms-workspace-architecture}

El espacio de trabajo de AEM Forms es una aplicación web alojada en CRX™. Cuando se abre el espacio de trabajo en un explorador, se accede a un recurso CRX y la aplicación se representa como página HTML en el explorador.

La aplicación accede al servidor de AEM Forms en los extremos REST para hacer lo siguiente:

* Buscar tareas de usuario, puntos de inicio de procesos, historial de procesos e información de usuarios
* Realizar acciones en tareas
* Tareas de consulta en la base de datos
* Actualizar las preferencias de usuario y más

El servidor de AEM Forms accede a la base de datos de AEM Forms a través de JDBC. La base de datos mantiene las tareas, los procesos y sus instancias, usuarios y la información relacionada.

El espacio de trabajo de AEM Forms está diseñado en componentes modulares JavaScript™ que pueden personalizarse y reutilizarse individualmente en otras aplicaciones web. Los componentes se basan en BackBone, que es una biblioteca JavaScript que da estructura a las aplicaciones web. Un artículo detallado que describe la interacción de componentes con BackBone es [here](/help/forms/using/backbone-interaction.md). La organización de componentes en la estructura de carpetas CRX se analiza en [this](/help/forms/using/folder-structure.md) artículo.

Paquetes entregados para el espacio de trabajo de AEM Forms:

* `adobe-lc-workspace-pkg-<version>.zip`: Es un paquete CRX, es decir, se puede implementar en CRX usando el Administrador de paquetes.
* `adobe-lc-workspace-<version>-src.zip`: Es un archivo que contiene código completo del espacio de trabajo de AEM Forms y las secuencias de comandos para crear los paquetes de implementación: paquetes de envío, depuración y desarrollo.
