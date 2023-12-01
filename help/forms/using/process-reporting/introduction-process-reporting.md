---
title: Introducción a la creación de informes de procesos
seo-title: Introduction to Process Reporting
description: Introducción y capacidades principales de Process Reporting de AEM Forms en JEE
seo-description: Introduction and key capabilities of AEM Forms on JEE Process Reporting
uuid: a7f2455b-1b09-41a7-817b-e2e7a1ff9936
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e83ed7b-3f48-4bf6-be4c-89f79949c1df
docset: aem65
exl-id: 674d28dc-7353-49de-9e12-b1998e1509c7
source-git-commit: 5e56441d2dc9b280547c91def8d971e7b1dfcfe3
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 86%

---

# Introducción a la creación de informes de procesos{#introduction-to-process-reporting}

![Process-Reporting](assets/process-reporting.png)

Process Reporting es una herramienta basada en explorador que se utiliza para crear y ver informes sobre los procesos y las tareas de AEM Forms.

Process Reporting proporciona un conjunto de informes integrados que le permiten filtrar y ver información sobre los procesos de larga ejecución, la duración de los procesos y el volumen del flujo de trabajo.

Además, Process Reporting proporciona una interfaz para ejecutar consultas ad hoc e integrar vistas de informes personalizadas en la interfaz de usuario de Process Reporting.

Para obtener la lista de exploradores admitidos, consulte [Plataformas compatibles con AEM Forms](/help/forms/using/aem-forms-jee-supported-platforms.md).

Process Reporting se basa en módulos que hacen lo siguiente:

* Leer datos de proceso de la base de datos de AEM Forms
* Publicar datos de proceso en un repositorio incrustado de Process Reporting
* Proporciona una interfaz de usuario basada en explorador para ver los informes

## Capacidades clave {#key-capabilities}

### Informes siempre disponibles {#always-on-reporting}

![administración del sitio](assets/site-management.png)

Vea la lista de procesos de larga ejecución, procese gráficos de duración y ejecute consultas personalizadas mediante filtros.

Process Reporting también proporciona la opción de exportar los datos de los informes y las consultas en formato CSV.

### Informes ad hoc {#adhoc-reports}

![impresión-y-color](assets/print-&-colour.png)

Utilice filtros para obtener una vista específica de los datos.

Puede buscar procesos o tareas por ID, duración, fechas de inicio y finalización, iniciador de procesos, etc.

Puede combinar varios filtros para crear informes específicos.

A continuación, puede guardar los filtros de informe para que se ejecuten en una fecha u hora posteriores.

### Historial de procesos/tareas {#process-task-history}

![administración de archivos](assets/file-management.png)

Los servidores de AEM Forms ejecutan numerosos procesos en paralelo. Estos procesos siguen en transición de un estado a otro. Al publicar datos de Forms en su repositorio a intervalos regulares, Process Reporting conserva la información de transición sobre los procesos que se ejecutan en AEM Forms.

### Control de acceso {#access-control-br}

![sin título](assets/untitled.png)

Process Reporting proporciona acceso basado en permisos en la interfaz de usuario.

Eso significa que solo los usuarios con permisos de informes tienen acceso a la interfaz de usuario de Process Reporting.
