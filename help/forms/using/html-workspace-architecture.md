---
title: Arquitectura de AEM Forms Workspace
seo-title: Arquitectura de AEM Forms Workspace
description: Información conceptual y descripción general de la arquitectura del espacio de trabajo de LiveCycle AEM Forms.
seo-description: Información conceptual y descripción general de la arquitectura del espacio de trabajo de LiveCycle AEM Forms.
uuid: e1a48452-ed44-4ea7-ba38-d961c8faafa5
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c3a312fb-f684-477d-916d-2d3c99aa7607
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Arquitectura de AEM Forms Workspace {#aem-forms-workspace-architecture}

El espacio de trabajo de AEM Forms es una aplicación web alojada en CRX™. Cuando se abre un espacio de trabajo en un navegador, se accede a un recurso CRX y la aplicación se representa como página HTML en el navegador.

La aplicación accede al servidor de AEM Forms en los extremos REST para hacer lo siguiente:

* Buscar tareas de usuario, puntos de inicio de proceso, historial de procesos e información de usuario
* Realizar acciones en tareas
* Tareas de consulta en la base de datos
* Actualizar las preferencias de usuario y más

El servidor de AEM Forms accede a la base de datos de AEM Forms a través de JDBC. La base de datos persiste en tareas, procesos y sus instancias, usuarios e información relacionada.

El espacio de trabajo de AEM Forms está diseñado en componentes modulares de JavaScript™ que pueden personalizarse y reutilizarse individualmente en otras aplicaciones web. Los componentes se basan en BackBone, que es una biblioteca JavaScript que proporciona estructura a las aplicaciones web. Un artículo detallado que describe la interacción de los componentes con BackBone es [aquí](/help/forms/using/backbone-interaction.md). La organización de componentes en la estructura de carpetas CRX se describe en [este](/help/forms/using/folder-structure.md) artículo.

Paquetes entregados para el espacio de trabajo de AEM Forms:

* `adobe-lc-workspace-pkg-<version>.zip`:: Es un paquete CRX, es decir, puede implementarse en CRX mediante el Administrador de paquetes.
* `adobe-lc-workspace-<version>-src.zip`:: Es un archivo que contiene código completo del espacio de trabajo y las secuencias de comandos de AEM Forms para crear los paquetes de implementación: Enviar, Depurar y Dev.
