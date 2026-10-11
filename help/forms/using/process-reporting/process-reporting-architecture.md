---
title: Funcionamiento de los informes de procesos
description: Descripción de los servicios que conforman AEM Forms en JEE Process Reporting e introducción a la interfaz de usuario de Process Reporting.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
docset: aem65
exl-id: 66dfac36-5b7e-40be-9921-efa9f2a9521c
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
source-wordcount: '359'
ht-degree: 96%
---
# Funcionamiento de los informes de procesos{#how-process-reporting-works}

Process Reporting es el módulo de informes de AEM Forms en JEE.

Process Reporting permite ejecutar informes sobre procesos y tareas de AEM Forms.

Process Reporting utiliza el repositorio incrustado del módulo para publicar datos de Forms. A continuación, utiliza esos datos para ejecutar informes.

Process Reporting consta de los siguientes módulos:

* [Servicio ProcessDataPublisher](#processdatapublisher-service-br-p)
* [Servicio ProcessDataStorage](#processdatastorageprovider-service-br-p)
* [Servicio OSGi](#osgi-service-br-p)
* [Servlet Query Data](#querydataservlet-service-br-p)
* [Interfaz de usuario de Process Reporting](#process-reporting-user-interface-br-p)

## Arquitectura de Process Reporting {#process-reporting-architecture-br}

![plataforma_process_reporting](assets/processreportingarchitecture.png)

## Módulos de Process Reporting {#process-reporting-modules}

### Servicio ProcessDataPublisher {#processdatapublisher-service-br}

El servidor ProcessDataPublisher se ejecuta periódicamente en la base de datos de AEM Forms y extrae los datos que han cambiado desde la última ejecución del servicio. A continuación, publica los datos en el servicio Process Data Storage.

Para obtener más información sobre la configuración del servicio, consulte [Configuración del servicio ProcessDataPublisher](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p).

### Servicio ProcessDataStorageProvider {#processdatastorageprovider-service-br}

El servicio ProcessDataStorageProvider recibe datos de proceso del servicio ProcessDataPublisher y los guarda en el repositorio de Process Reporting.

Para obtener más información sobre la configuración del servicio, consulte [Configuración del servicio ProcessDataStorageProvider](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p).

### Servicio OSGi {#osgi-service-br}

QueryDataServlet utiliza este servicio para obtener los datos de informe del repositorio de Process Reporting.

### Servicio QueryDataServlet {#querydataservlet-service-br}

El servicio QueryDataServlet acepta consultas de la interfaz de usuario de Process Reporting.

A continuación, utiliza los servicios OSGi para obtener los datos de informe relevantes, procesa los datos y los devuelve a la interfaz de usuario.

### Interfaz de usuario de Process Reporting {#process-reporting-user-interface-br}

La interfaz de usuario de Process Reporting es una interfaz basada en explorador web. Esta interfaz se utiliza para ver la información de procesos y tareas publicada en la base de datos de AEM Forms.

Para ver una introducción a la interfaz de usuario de Process Reporting, consulte [Interfaz de usuario de Process Reporting](/help/forms/using/process-reporting/introduction-process-reporting.md).

### Servicio QueryDataServlet {#querydataservlet-service-br-1}

El servicio QueryDataServlet acepta consultas de la interfaz de usuario de Process Reporting.

A continuación, utiliza los servicios OSGi para obtener los datos de informe relevantes, procesa los datos y los devuelve a la interfaz de usuario.

### Informes personalizados {#custom-reports-br}

Puede crear sus propios informes personalizados y mostrarlos en la pestaña Informes personalizados de la interfaz de usuario de Process Reporting.

Para ver los pasos para crear un informe personalizado, consulte Creación de un informe personalizado en el artículo [Informes personalizados en Process Reporting](/help/forms/using/process-reporting/process-reporting-custom-reports.md).
