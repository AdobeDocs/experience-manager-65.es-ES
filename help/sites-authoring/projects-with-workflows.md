---
title: Uso de flujos de trabajo de proyecto
seo-title: Working with Project Workflows
description: Hay varios flujos de trabajo de proyectos disponibles de forma integrada.
seo-description: A variety of project workflows are available out of the box.
uuid: 376922ca-e09e-4ac8-88c8-23dac2b49dbe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 9d2bf30c-5190-4924-82cd-bcdfde24eb39
exl-id: 407fc164-291d-42f6-8c46-c1df9ba3d454
source-git-commit: 200b47070b7ead54ee54eea504bd960d4e0731d9
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 53%

---


# Uso de flujos de trabajo de proyecto {#working-with-project-workflows}

Entre los flujos de trabajo de proyecto disponibles de fábrica se incluye lo siguiente:

* **Flujo de trabajo de aprobación del proyecto** : este flujo de trabajo le permite asignar contenido a un usuario, revisarlo y aprobarlo.
* **Solicitar lanzamiento** : un flujo de trabajo solicita un lanzamiento.
* **Solicitar página de aterrizaje** : este flujo de trabajo solicita una página de aterrizaje.
* **Solicitar correo electrónico**: flujo de trabajo para solicitar un correo electrónico.
* **Sesión fotográfica del producto y sesión fotográfica del producto (comercio)**: se asignan recursos a productos.
* **Crear y traducir copia DAM y Crear copia de idioma DAM**: crea elementos binarios, metadatos y etiquetas traducidos para los recursos y las carpetas.

Según la plantilla Proyecto que seleccione, tendrá a su disposición determinados flujos de trabajo:

|  | **Proyecto simple** | **Proyecto multimedia** | **Proyecto de sesión fotográfica del producto** | **Proyecto de traducción** |
|---|:-:|:-:|:-:|:-:|
| Solicitar copia |  | x |  |  |
| Sesión fotográfica del producto |  | x | x |  |
| Sesión fotográfica del producto (comercio) |  |  | x |  |
| Aprobación del proyecto | x |  |  |  |
| Solicitar lanzamiento | x |  |  |  |
| Solicitar página de aterrizaje | x |  |  |  |
| Solicitar correo electrónico | x |  |  |  |
| Creación de copia y último idioma de DAM; |  |  |  | x |
| Crear y traducir DAM copia y último idioma; |  |  |  | x |

>[!NOTE]
>
>&amp;ast; Estos flujos de trabajo no se inician desde la **Flujo de trabajo** en Proyectos. Consulte [Creación de copias de idioma para recursos](/help/sites-administering/tc-manage.md). 

Las etapas para iniciar y completar flujos de trabajo no son las mismas, independientemente del flujo de trabajo que se elija. Solo las etapas cambian.

Un flujo de trabajo se inicia directamente en Proyectos (excepto Crear copia de idioma DAM y Crear y traducir copia de idioma DAM). La información sobre cualquier tarea pendiente de un proyecto aparece en el mosaico **Tareas**. Las notificaciones para las tareas que se deben completar aparecen junto al icono de usuario.

Para obtener más información sobre el trabajo con flujos de trabajo en AEM, consulte los siguientes documentos:

* [Participación en flujos de trabajo](/help/sites-authoring/workflows-participating.md)
* [Aplicación de flujos de trabajo a páginas](/help/sites-authoring/workflows-applying.md)
* [Configuración de flujos de trabajo ](/help/sites-administering/workflows.md)

En esta sección se describen los flujos de trabajo disponibles para Proyectos.

## Flujo de trabajo de solicitud de copia {#request-copy-workflow}

Este flujo de trabajo permite solicitar un manuscrito de un usuario y, a continuación, aprobarlo. Para iniciar el flujo de trabajo Solicitar copia:

1. En un proyecto de medios, toque o haga clic en la cadena secundaria inferior de la parte superior derecha de la variable **Flujos de trabajo** mosaico y seleccione **Iniciar flujo de trabajo**.
1. En el asistente de flujo de trabajo, seleccione **Solicitar copia** y haga clic en **Siguiente**.
1. Introduzca un título para el manuscrito y un breve resumen de lo que se solicita. Si fuera necesario, introduzca un recuento de palabras de destino, la prioridad de las tareas y una fecha de vencimiento.

   ![Flujo de trabajo Solicitar copia](assets/project-request-copy-workflow.png)

1. Haga clic en **Submit**.

Se inicia el flujo de trabajo. La tarea aparece en el **Tareas** tarjeta.

## Flujo de trabajo de la sesión fotográfica del producto {#product-photo-shoot-workflow}

La variable **Sesión fotográfica del producto** los flujos de trabajo (comerciales y sin comercio) se tratan detalladamente en el documento [Proyectos creativos](/help/sites-authoring/managing-product-information.md)

## Flujo de trabajo de aprobación del proyecto {#project-approval-workflow}

En el **Aprobación del proyecto** flujo de trabajo, asigne contenido a un usuario, revise y, a continuación, apruebe el contenido.

1. En un proyecto simple, toque o haga clic en el elemento adicional inferior derecho del **Flujos de trabajo** mosaico y seleccione **Iniciar flujo de trabajo**.
1. En el asistente de flujo de trabajo, seleccione **Flujo de trabajo de aprobación del proyecto** y haga clic en **Siguiente**.
1. Introduzca un título y seleccione a quién asignarlo. Si fuera necesario, introduzca una descripción, ruta de contenido, prioridad de las tareas y una fecha de vencimiento.

   ![Flujo de trabajo de aprobación del proyecto](assets/project-approval-workflow.png)

1. Haga clic en **Submit**.

Se inicia el flujo de trabajo. La tarea aparece en el **Tareas** tarjeta.

## Flujo de trabajo Solicitar lanzamiento {#request-launch-workflow}

Este flujo de trabajo permite solicitar un lanzamiento.

1. En un proyecto simple, toque o haga clic en el elemento adicional inferior derecho del **Flujos de trabajo** mosaico y seleccione **Iniciar flujo de trabajo**.
1. En el asistente de flujo de trabajo, seleccione **Flujo de trabajo Solicitar lanzamiento** y haga clic en **Siguiente**.
1. Introduzca un título para el lanzamiento y proporcione la ruta de origen de este. También puede añadir una descripción y la fecha de lanzamiento, si procede. Seleccione Heredar datos en directo de la página de origen o Excluir páginas secundarias según el comportamiento deseado del lanzamiento.

   ![Flujo de trabajo Solicitar inicio](assets/project-request-launch-workflow.png)

1. Haga clic en **Submit**.

Se inicia el flujo de trabajo. El flujo de trabajo aparece en la sección **Flujos de trabajo** lista.

## Flujo de trabajo Solicitar página de aterrizaje {#request-landing-page-workflow}

Este flujo de trabajo permite solicitar una página de aterrizaje.

1. En un proyecto simple, toque o haga clic en el elemento adicional inferior derecho del **Flujos de trabajo** mosaico y seleccione **Iniciar flujo de trabajo**.
1. En el asistente de flujo de trabajo, seleccione **Solicitar página de aterrizaje** y haga clic en **Siguiente**.
1. Introduzca un título para la página de aterrizaje y la ruta principal. Si fuera necesario, introduzca una fecha de lanzamiento o elija un archivo para la página de aterrizaje.

   ![Solicitud del flujo de trabajo de la página de aterrizaje](assets/project-request-landing-page-workflow.png)

1. Haga clic en **Submit**.

Se inicia el flujo de trabajo. La tarea aparece en el **Tareas** tarjeta.

## Flujo de trabajo Solicitar correo electrónico {#request-email-workflow}

Este flujo de trabajo permite solicitar un correo electrónico. Es el mismo flujo de trabajo que aparece en el mosaico **Correo electrónico**.

1. En un proyecto simple, toque o haga clic en el elemento adicional inferior derecho del **Flujos de trabajo** mosaico y seleccione **Iniciar flujo de trabajo**.
1. En el asistente de flujo de trabajo, seleccione **Solicitar correo electrónico** y haga clic en **Siguiente**.
1. Introduzca un título de correo electrónico, así como las rutas de la campaña y la plantilla. Además, puede proporcionar un nombre, una descripción y una fecha de lanzamiento.

   ![Flujo de trabajo de solicitud de correo electrónico](assets/project-request-email-workflow.png)

1. Haga clic en **Submit**.

Se inicia el flujo de trabajo. La tarea aparece en el **Tareas** tarjeta.

## Crear (y traducir) el flujo de trabajo de copia de idioma de los activos {#create-and-translate-language-copy-workflow-for-assets}

La variable **Crear copia de idioma** y **Crear y traducir copia de idioma** los flujos de trabajo se tratan detalladamente en el documento [Creación de copias de idioma para recursos.](/help/assets/translation-projects.md)
