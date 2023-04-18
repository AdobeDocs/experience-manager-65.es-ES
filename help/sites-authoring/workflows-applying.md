---
title: Aplicación de flujos de trabajo a páginas de contenido
description: Durante la creación, puede invocar flujos de trabajo para realizar acciones en las páginas; también es posible aplicar más de un flujo de trabajo.
uuid: 652d9a23-907d-43ad-9eef-7ab1d07918cd
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 6472dc94-96e0-4286-8f86-d85726cc843c
docset: aem65
exl-id: e00da2b3-046a-4d93-aed0-07dd8c66899f
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 53%

---

# Aplicación de flujos de trabajo a páginas{#applying-workflows-to-pages}

Durante la creación, puede invocar flujos de trabajo para realizar acciones en las páginas; también es posible aplicar más de un flujo de trabajo.

Al aplicar el flujo de trabajo, debe especificar la siguiente información:

* Flujo de trabajo que se va a aplicar.
Puede aplicar cualquier flujo de trabajo (al que tenga acceso, según lo haya asignado el administrador de AEM).
* De forma opcional, un título que ayuda a identificar la instancia de flujo de trabajo en la bandeja de entrada de un usuario.
* La carga útil del flujo de trabajo; puede ser una o más páginas.

Los flujos de trabajo se pueden iniciar desde:

* [la consola Sitios](#starting-a-workflow-from-the-sites-console).
* [al editar una página, en Información de la página](#starting-a-workflow-from-the-page-editor). 

>[!NOTE]
>
>Consulte también lo siguiente:
>
>* [Cómo aplicar flujos de trabajo a recursos DAM](/help/assets/assets-workflow.md).
>* [Uso de flujos de trabajo de proyecto](/help/sites-authoring/projects-with-workflows.md).
>


>[!NOTE]
>
>Los administradores de AEM pueden [iniciar flujos de trabajo mediante varios métodos más](/help/sites-administering/workflows-starting.md).

## Inicio de un flujo de trabajo desde la consola Sitios {#starting-a-workflow-from-the-sites-console}

Puede iniciar un flujo de trabajo desde:

* [la opción Crear de la barra de herramientas del sitio](#starting-a-workflow-from-the-sites-toolbar).
* [el carril Escala de tiempo de la consola Sitios](#starting-a-workflow-from-the-timeline).

En ambos casos, deberá:

* [Especificar los detalles del flujo de trabajo en el asistente Crear flujo de trabajo](#specifying-workflow-details-in-the-create-workflow-wizard).

### Inicio de un flujo de trabajo desde la barra de herramientas Sitios {#starting-a-workflow-from-the-sites-toolbar}

Puede iniciar un flujo de trabajo desde la barra de herramientas de la consola **Sitios**:

1. Busque y seleccione la página deseada. 

1. En la opción **Crear** de la barra de herramientas, ahora puede seleccionar el **Flujo de trabajo**.

   ![screen_shot_2019-03-06at121237pm](assets/screen_shot_2019-03-06at121237pm.png)

1. La variable **Crear flujo de trabajo** asistente le ayudará [especificar los detalles del flujo de trabajo](#specifying-workflow-details-in-the-create-workflow-wizard).

### Inicio de un flujo de trabajo desde la línea de tiempo {#starting-a-workflow-from-the-timeline}

En el **Cronología** puede iniciar un flujo de trabajo para aplicarlo al recurso seleccionado.

1. [Seleccione el recurso](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources) y abra [Cronología](/help/sites-authoring/basic-handling.md#timeline) (o abra Cronología y seleccione el recurso).
1. La punta de flecha junto al campo Comentario puede utilizarse para mostrar **Iniciar flujo de trabajo**:

   ![screen-shot_2019-03-05at120026](assets/screen-shot_2019-03-05at120026.png)

1. La variable **Crear flujo de trabajo** asistente le ayudará [especificar los detalles del flujo de trabajo](#specifying-workflow-details-in-the-create-workflow-wizard).

### Especificación de los detalles del flujo de trabajo en el asistente Crear flujo de trabajo {#specifying-workflow-details-in-the-create-workflow-wizard}

La variable **Crear flujo de trabajo** le ayudará a seleccionar el flujo de trabajo y a especificar los detalles necesarios.

Después de abrir el **Crear flujo de trabajo** desde:

* [la opción Crear de la barra de herramientas del sitio](#starting-a-workflow-from-the-sites-toolbar).
* [el carril Escala de tiempo de la consola Sitios](#starting-a-workflow-from-the-timeline).

Puede especificar detalles:

1. En el **Propiedades** , se definen las opciones básicas del flujo de trabajo:

   * **Modelo de flujo de trabajo**
   * **Título del flujo de trabajo**

      * Puede especificar un título para esta instancia, para ayudarle a identificarlo en una etapa posterior.

   Según el modelo de flujo de trabajo, también están disponibles las siguientes opciones. Permiten que el paquete creado como carga útil se mantenga después de que se complete el flujo de trabajo.

   * **Conservar paquete de flujo de trabajo**
   * **Título del paquete**

      * Puede especificar un título para el paquete, para ayudar a la identificación.
   >[!NOTE]
   >
   >La opción **Mantener paquete de flujo de trabajo** está disponible cuando el flujo de trabajo se ha configurado para la compatibilidad con varios recursos y se han seleccionado varios recursos.[](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support)

   Cuando haya terminado, seleccione **Siguiente** para continuar.

   ![wf-52](assets/wf-52.png)

1. En la etapa **Ámbito**, puede seleccionar lo siguiente:

   * **Añadir contenido** para abrir el [explorador de rutas](/help/sites-authoring/author-environment-tools.md#path-browser) y seleccionar recursos adicionales. En el explorador, haga clic o pulse en **Seleccionar** para añadir contenido a la instancia de flujo de trabajo.

   * Un recurso existente para ver acciones adicionales:

      * **Incluir elementos secundarios** para especificar que en el flujo de trabajo se incluirán los elementos secundarios de ese recurso.
Se abrirá un cuadro de diálogo para que pueda ajustar la selección según lo siguiente:

         * Incluir solo los elementos secundarios inmediatos.
         * Incluir solo las páginas modificadas.
         * Incluir solo las páginas ya publicadas.

         Los elementos secundarios especificados se añaden a la lista de recursos a los que se aplica el flujo de trabajo.

      * **Eliminar selección** para eliminar ese recurso del flujo de trabajo.

   ![wf-53](assets/wf-53.png)

   >[!NOTE]
   >
   >Si agrega recursos adicionales, puede utilizar **Atrás** para ajustar la configuración **Mantener flujo de trabajo del paquete** en el paso **Propiedades**.

1. Use la opción **Crear** para cerrar el asistente y crear la instancia de flujo de trabajo. Se muestra una notificación en la consola Sitios .

## Inicio de un flujo de trabajo desde el editor de páginas {#starting-a-workflow-from-the-page-editor}

Al editar una página, puede seleccionar **Información de la página** en la barra de herramientas. El menú desplegable tiene la opción **Iniciar en flujo de trabajo**. Se abrirá un cuadro de diálogo en el que puede especificar el flujo de trabajo necesario junto con un título, si fuera necesario: 

![wf-54](assets/wf-54.png)
