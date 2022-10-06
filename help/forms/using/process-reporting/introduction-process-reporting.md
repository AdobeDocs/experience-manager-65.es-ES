---
title: Introducción a la creación de informes de procesos
seo-title: Introduction to Process Reporting
description: Introducción y funciones clave de AEM Forms en la creación de informes de procesos JEE
seo-description: Introduction and key capabilities of AEM Forms on JEE Process Reporting
uuid: a7f2455b-1b09-41a7-817b-e2e7a1ff9936
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e83ed7b-3f48-4bf6-be4c-89f79949c1df
docset: aem65
exl-id: 674d28dc-7353-49de-9e12-b1998e1509c7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Introducción a la creación de informes de procesos{#introduction-to-process-reporting}

![informes de procesos](assets/process-reporting.png)

Process Reporting es una herramienta basada en explorador que se utiliza para crear y ver informes sobre procesos y tareas de AEM Forms.

Process Reporting proporciona un conjunto de informes integrados que le permiten filtrar y ver información sobre procesos de larga duración, duración del proceso y volumen del flujo de trabajo.

Además, Process Reporting proporciona una interfaz para ejecutar consultas ad hoc e integrar vistas de informes personalizadas en la interfaz de usuario de Process Reporting.

Para obtener la lista de exploradores admitidos, consulte [Plataformas compatibles con AEM Forms](/help/forms/using/aem-forms-jee-supported-platforms.md).

Process Reporting se basa en módulos que:

* Leer datos de proceso de la base de datos de AEM Forms
* Publicar datos de proceso en un repositorio incrustado de Process Reporting
* Proporciona una interfaz de usuario basada en navegador para ver informes

## Funcionalidades Clave {#key-capabilities}

### Informes siempre activos {#always-on-reporting}

![administración del sitio](assets/site-management.png)

Vea la lista de procesos de larga duración, procese gráficos de duración y ejecute consultas personalizadas con filtros.

Process Reporting también proporciona la opción de exportar los datos de informes y consultas en formato CSV.

### Informes específicos {#adhoc-reports}

![print-&amp;-color](assets/print-&-colour.png)

Utilice filtros para obtener una vista específica de los datos.

Puede buscar procesos o tareas por ID, duración, fechas de inicio y finalización, iniciador de procesos, etc.

Puede combinar varios filtros para crear informes específicos.

A continuación, puede guardar los filtros de informe para que se ejecuten en una fecha u hora posteriores.

### Historial de procesos/tareas {#process-task-history}

![administración de archivos](assets/file-management.png)

Los servidores de AEM Forms ejecutan numerosos procesos en paralelo. Estos procesos siguen en transición de un estado a otro. Al publicar datos de Forms en el repositorio de Process Reporting a intervalos regulares, Process Reporting conserva la información de transición sobre los procesos que se ejecutan en AEM Forms.

### Control de acceso {#access-control-br}

![sin título](assets/untitled.png)

Los informes de procesos proporcionan acceso basado en permisos a la interfaz de usuario.

Esto significa que solo los usuarios con permisos de informes tienen acceso a la interfaz de usuario de Process Reporting.
