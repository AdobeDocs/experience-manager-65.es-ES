---
title: Introducción a los informes de procesos
seo-title: Introducción a los informes de procesos
description: Introducción y funciones clave de AEM Forms en informes de procesos JEE
seo-description: Introducción y funciones clave de AEM Forms en informes de procesos JEE
uuid: a7f2455b-1b09-41a7-817b-e2e7a1ff9936
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e83ed7b-3f48-4bf6-be4c-89f79949c1df
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Introducción a los informes de procesos{#introduction-to-process-reporting}

![informes de procesos](assets/process-reporting.png)

Process Reporting es una herramienta basada en navegador que se utiliza para crear y ver informes sobre procesos y tareas de AEM Forms.

Los informes de procesos proporcionan un conjunto de informes predeterminados que le permiten filtrar, ver información sobre procesos de larga duración, duración del proceso y volumen del flujo de trabajo.

Además, Informes de procesos proporciona una interfaz para ejecutar consultas ad hoc e integrar vistas de informes personalizadas en la interfaz de usuario de Informes de procesos.

Para obtener la lista de exploradores admitidos, consulte Plataformas [compatibles con formularios](/help/forms/using/aem-forms-jee-supported-platforms.md)AEM Forms.

La generación de informes de procesos se basa en módulos que:

* Leer datos de proceso de la base de datos de AEM Forms
* Publicación de datos de proceso en un repositorio incrustado de Process Reporting
* Proporciona una interfaz de usuario basada en explorador para ver los informes

## Capacidades clave {#key-capabilities}

### Informes siempre activos {#always-on-reporting}

![administración del sitio](assets/site-management.png)

Vea la lista de procesos de larga ejecución, procese gráficos de duración y ejecute consultas personalizadas mediante filtros.

Los informes de procesos también ofrecen la opción de exportar los datos de informes y consultas en formato CSV.

### Informes específicos {#adhoc-reports}

![print-&amp;-color](assets/print-&-colour.png)

Utilice filtros para obtener una vista específica de los datos.

Puede buscar procesos o tareas por ID, duración, fechas de inicio y finalización, iniciador de procesos, etc.

Puede combinar varios filtros para crear informes específicos.

A continuación, puede guardar los filtros del informe para que se ejecuten en una fecha u hora posterior.

### Historial de procesos/tareas {#process-task-history}

![administración de archivos](assets/file-management.png)

Los servidores de AEM Forms ejecutan numerosos procesos en paralelo. Estos procesos continúan en la transición de un estado a otro. Al publicar datos de Forms en el repositorio de Process Reporting a intervalos regulares, Process Reporting conserva la información de transición sobre los procesos que se ejecutan en AEM Forms.

### Control de acceso {#access-control-br}

![sin título](assets/untitled.png)

Los informes de procesos proporcionan acceso basado en permisos a la interfaz de usuario.

Esto significa que solo los usuarios con permisos de informes tienen acceso a la interfaz de usuario de Process Reporting.

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
