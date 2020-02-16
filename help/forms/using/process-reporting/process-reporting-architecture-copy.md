---
title: Funcionamiento de los informes de procesos
seo-title: Funcionamiento de los informes de procesos
description: Descripción de los servicios que conforman AEM Forms en los informes de procesos JEE y una introducción a la interfaz de usuario de informes de procesos
seo-description: Descripción de los servicios que conforman AEM Forms en los informes de procesos JEE y una introducción a la interfaz de usuario de informes de procesos
uuid: 4631b734-a679-495c-a708-2348bf22c1f7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a1af9920-5d2a-462f-bdee-ccec4c047c5b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Funcionamiento de los informes de procesos {#how-process-reporting-works}

Process Reporting es el módulo de informes de AEM Forms en JEE.

Los informes de procesos le permiten ejecutar informes sobre procesos y tareas de AEM Forms.

Process Reporting utiliza el repositorio incrustado de Process Reporting para publicar datos de Forms. Luego utiliza esos datos para ejecutar informes.

Los informes de procesos constan de los siguientes módulos:

* [Servicio ProcessDataPublisher](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatapublisher-service-br-p)
* [Servicio ProcessDataStorage](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatastorageprovider-service-br-p)
* [Servicio OSGi](/help/forms/using/process-reporting/process-reporting-architecture.md#p-osgi-service-br-p)
* [Servlet de datos de consulta](/help/forms/using/process-reporting/process-reporting-architecture.md#p-querydataservlet-service-br-p)
* [Interfaz de usuario de Informes de procesos](/help/forms/using/process-reporting/process-reporting-architecture.md#p-process-reporting-user-interface-br-p)

## Arquitectura de informes de procesos {#process-reporting-architecture-br}

![processreportararquitectura](assets/processreportingarchitecture.png)

## Módulos de informes de procesos {#process-reporting-modules}

### Servicio ProcessDataPublisher {#processdatapublisher-service-br}

El servidor ProcessDataPublisher se ejecuta periódicamente en la base de datos de AEM Forms y extrae los datos que han cambiado desde la última ejecución del servicio. A continuación, publica los datos en el servicio de almacenamiento de datos de proceso.

Para obtener más información sobre la configuración del servicio, consulte [Configurar el servicio](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p)ProcessDataPublisher.

### Servicio ProcessDataStorageProvider {#processdatastorageprovider-service-br}

El servicio ProcessDataStorageProvider recibe datos de proceso del servicio ProcessDataPublisher y los guarda en el repositorio de Process Reporting.

Para obtener más información sobre la configuración del servicio, consulte [Configurar el servicio](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p)ProcessDataStorageProvider.

### Servicio OSGi {#osgi-service-br}

QueryDataServlet utiliza este servicio para obtener los datos de informes del repositorio de Process Reporting.

### Servicio QueryDataServlet {#querydataservlet-service-br}

El servicio QueryDataServlet acepta consultas de la interfaz de usuario de Process Reporting.

A continuación, el servicio utiliza los servicios OSGi para obtener los datos de informes relevantes, procesa los datos y los devuelve a la interfaz de usuario.

### Interfaz de usuario de Informes de procesos {#process-reporting-user-interface-br}

La interfaz de usuario de Informes de procesos es una interfaz basada en explorador Web. Esta interfaz se utiliza para ver la información de procesos y tareas que se publica desde la base de datos de AEM Forms.

### Servicio QueryDataServlet {#querydataservlet-service-br-1}

El servicio QueryDataServlet acepta consultas de la interfaz de usuario de Process Reporting.

A continuación, el servicio utiliza los servicios OSGi para obtener los datos de informes relevantes, procesa los datos y los devuelve a la interfaz de usuario.

### Informes personalizados {#custom-reports-br}

Puede crear sus propios informes personalizados y mostrarlos en la ficha Informes personalizados de la interfaz de usuario de Informes de procesos.

Para ver los pasos para crear un informe personalizado, consulte Para crear un informe personalizado en el artículo Informes [personalizados en proceso Informes](/help/forms/using/process-reporting/process-reporting-custom-reports.md).

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
