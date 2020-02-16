---
title: Configuración de AEM Forms para enviar datos de formulario a un proceso de AEM Forms en JEE
seo-title: Configuración de AEM Forms para enviar datos de formulario a un proceso de AEM Forms en JEE
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

---


# Configuración de AEM Forms para enviar datos de formulario a un proceso de AEM Forms en JEE{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

Los formularios adaptables admiten el envío de datos a un proceso de AEM Forms en JEE para un procesamiento posterior. Le permite activar un proceso de AEM Forms en JEE con los datos disponibles en el formulario enviado. Siga estos pasos para permitir que la instancia de AEM Forms envíe un formulario adaptable al proceso de AEM Forms en JEE:

## Configuración del servidor de AEM Forms {#configure-your-aem-forms-server}

Siga estos pasos para permitir que el servidor de formularios AEM envíe datos a un servidor AEM Forms en JEE:

1. Vaya a la consola de configuración web de AEM en https://[*host*]:[*port*]/system/console/configMgr.

1. Busque y haga clic en el componente de configuración **del SDK de** Adobe LiveCycle Client.
1. Haga clic para editar la URL, el nombre de usuario y la contraseña del servidor de configuración para AEM Forms en el servidor JEE.
1. Revise la configuración y haga clic en **Guardar**.

![Configuración del SDK de Adobe LiveCycle Client](assets/clientsdkconfiguration.jpg)

## Asignar datos a campos de proceso {#map-data-with-process-fields}

Una vez configurados los formularios AEM, asigne los datos XML y los datos adjuntos del formulario enviado a los campos del proceso de AEM Forms en JEE. Para ello:

1. En la consola de configuración web de AEM, haga clic para editar la configuración de **Guide LiveCycle Process Locator e Invoker** .
1. Especifique los siguientes parámetros:

   * **Nombre del parámetro** xml de datos (obligatorio): Especifique el archivo de propiedad XML del proceso AEM Forms en JEE que necesita procesar los datos enviados. The default value is **dataxml**.

   * **Nombre del parámetro** de archivos adjuntos (opcional): Especifique la lista de objetos de documento que debe procesar AEM Forms en JEE. The default value is **fileAttachmentsList**.

1. Revise la configuración y haga clic en **Guardar**.

![Localizador de procesos de guía de LiveCycle e Invoker](assets/test3.jpg)

Una vez configurada, la acción de envío Enviar a Forms Workflow muestra los procesos del servidor AEM Forms en JEE que contienen el parámetro xml de datos especificado.
