---
title: Funcionamiento de los informes de procesos
seo-title: How Process Reporting Works
description: Descripción de los servicios que conforman AEM Forms en JEE Process Reporting y una introducción a la interfaz de usuario de Process Reporting
seo-description: Description of the services that make up the AEM Forms on JEE Process Reporting and an introduction to the Process Reporting UI
uuid: 37e31985-088a-4ef6-ba57-10a01597a873
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a6ff50df-273d-48f7-b0c6-0e69e900b97f
docset: aem65
exl-id: 66dfac36-5b7e-40be-9921-efa9f2a9521c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---

# Funcionamiento de los informes de procesos{#how-process-reporting-works}

Process Reporting es el módulo de informes de AEM Forms en JEE.

Los informes de procesos permiten ejecutar informes sobre procesos y tareas de AEM Forms.

Process Reporting utiliza el repositorio incrustado de Process Reporting para publicar datos de Forms. A continuación, utiliza esos datos para ejecutar informes.

Process Reporting consta de los siguientes módulos:

* [Servicio ProcessDataPublisher](#processdatapublisher-service-br-p)
* [Servicio ProcessDataStorage](#processdatastorageprovider-service-br-p)
* [Servicio OSGi](#osgi-service-br-p)
* [Servlet de datos de consulta](#querydataservlet-service-br-p)
* [Interfaz de usuario de Process Reporting](#process-reporting-user-interface-br-p)

## Arquitectura de informes de procesos {#process-reporting-architecture-br}

![processreportingplatform](assets/processreportingarchitecture.png)

## Módulos de informes de procesos {#process-reporting-modules}

### Servicio ProcessDataPublisher {#processdatapublisher-service-br}

El servidor ProcessDataPublisher se ejecuta periódicamente en la base de datos de AEM Forms y extrae los datos que han cambiado desde la última ejecución del servicio. A continuación, publica los datos en el servicio de almacenamiento de datos de proceso.

Para obtener más información sobre la configuración del servicio, consulte [Configurar el servicio ProcessDataPublisher](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p).

### Servicio ProcessDataStorageProvider {#processdatastorageprovider-service-br}

El servicio ProcessDataStorageProvider recibe datos de proceso del servicio ProcessDataPublisher y los guarda en el repositorio de Process Reporting.

Para obtener más información sobre la configuración del servicio, consulte [Configurar el servicio ProcessDataStorageProvider](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p).

### Servicio OSGi {#osgi-service-br}

QueryDataServlet utiliza este servicio para obtener los datos de informes del repositorio de Process Reporting.

### Servicio QueryDataServlet {#querydataservlet-service-br}

El servicio QueryDataServlet acepta consultas de la interfaz de usuario de Process Reporting.

A continuación, el servicio utiliza los servicios OSGi para obtener los datos de informes relevantes, procesa los datos y devuelve los datos a la interfaz de usuario.

### Interfaz de usuario de Process Reporting {#process-reporting-user-interface-br}

La interfaz de usuario de Informes de procesos es una interfaz basada en explorador web. Esta interfaz se utiliza para ver la información de procesos y tareas publicada en la base de datos de AEM Forms.

Para obtener una introducción a la interfaz de usuario de Process Reporting, consulte [Interfaz de usuario de Process Reporting](/help/forms/using/process-reporting/introduction-process-reporting.md).

### Servicio QueryDataServlet {#querydataservlet-service-br-1}

El servicio QueryDataServlet acepta consultas de la interfaz de usuario de Process Reporting.

A continuación, el servicio utiliza los servicios OSGi para obtener los datos de informes relevantes, procesa los datos y devuelve los datos a la interfaz de usuario.

### Informes personalizados {#custom-reports-br}

Puede crear sus propios informes personalizados y mostrarlos en la pestaña Informes personalizados de la interfaz de usuario de Informes de procesos .

Para ver los pasos para crear un informe personalizado, consulte Para crear un informe personalizado en el artículo [Informes personalizados en proceso de informes](/help/forms/using/process-reporting/process-reporting-custom-reports.md).
