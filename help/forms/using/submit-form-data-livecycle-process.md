---
title: Configuración de AEM Forms para enviar datos de formulario a un proceso AEM Forms en JEE
seo-title: Configuración de AEM Forms para enviar datos de formulario a un proceso AEM Forms en JEE
description: AEM Forms permite integrar formularios adaptables con AEM Forms en procesos JEE para procesar datos de formulario.
seo-description: AEM Forms permite integrar formularios adaptables con AEM Forms en procesos JEE para procesar datos de formulario.
uuid: 71a894d7-7c0a-43a6-afe5-40c4a15c66d6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: ff97424d-b384-4149-9a3c-b4f00aaa1def
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---


# Configuración de AEM Forms para enviar datos de formulario a un AEM Forms en un proceso JEE{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

Los formularios adaptables admiten el envío de datos a un proceso AEM Forms en JEE para un procesamiento posterior. Permite el déclencheur de un proceso de AEM Forms en JEE con los datos disponibles en el formulario enviado. Realice los siguientes pasos para permitir que la instancia de AEM Forms envíe un formulario adaptable a AEM Forms en el proceso JEE:

## Configure el servidor de AEM Forms {#configure-your-aem-forms-server}

Realice los siguientes pasos para permitir que el servidor de AEM formularios envíe datos a un AEM Forms en un servidor JEE:

1. Vaya a AEM consola de configuración web en https://[*host*]:[*puerto*]/system/console/configMgr.

1. Busque y haga clic en el componente **Configuración del SDK del cliente de Adobe LiveCycle**.
1. Haga clic para editar la dirección URL, el nombre de usuario y la contraseña del servidor de configuración para AEM Forms en el servidor JEE.
1. Revise la configuración y haga clic en **Guardar**.

![Configuración del SDK del cliente de Adobe LiveCycle](assets/clientsdkconfiguration.jpg)

## Asignar datos con campos de proceso {#map-data-with-process-fields}

Una vez configurado el AEM Forms, asigne el XML de datos y los archivos adjuntos del formulario enviado a los campos del proceso AEM Forms en JEE. Para ello:

1. En la consola de configuración web de AEM, haga clic para editar la configuración **Localizador de procesos de LiveCycle de guía y la configuración de Invoker**.
1. Especifique los siguientes parámetros:

   * **Nombre del parámetro**  xml de datos (obligatorio): Especifique el archivo de propiedad XML del proceso AEM Forms en JEE que necesita procesar los datos enviados. El valor predeterminado es **dataxml**.

   * **Nombre del parámetro**  de archivos adjuntos (opcional): Especifique la lista de los objetos de documento que el proceso AEM Forms en JEE debe procesar. El valor predeterminado es **fileAttachmentsList**.

1. Revise la configuración y haga clic en **Guardar**.

![Localizador de procesos de LiveCycle de guía e Invoker](assets/test3.jpg)

Una vez configurada, la acción Enviar al Forms Workflow envía listas de AEM Forms en los procesos del servidor JEE que contienen el parámetro xml de datos especificado.
