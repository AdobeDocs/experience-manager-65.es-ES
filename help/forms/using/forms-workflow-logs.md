---
title: Inicio de sesión en flujos de trabajo de AEM Forms
seo-title: Inicio de sesión en flujos de trabajo de AEM Forms
description: Use logs to debug AEM Forms workflow issues.
seo-description: Utilice los registros para depurar problemas de flujo de trabajo de AEM Forms.
uuid: 869d0271-c7e3-4b6d-8e63-893dc6af8b8a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 14bb521a-42ea-4fe2-90fb-202e7ddf917a
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Inicio de sesión en flujos de trabajo de AEM Forms{#logging-in-aem-forms-workflows}

Los pasos del flujo de trabajo de formularios proporcionan registros detallados para depurar convenientemente los problemas relacionados con el flujo de trabajo. Habilite el registro de depuración para flujos de trabajo de AEM Forms para la vista de los registros.

De forma predeterminada, toda la información de registro está disponible en el archivo **error.log** en el directorio */crx-repository/logs/* .

Los registros de depuración de los flujos de trabajo de formularios incluyen:

* Entrada de cada paso del flujo de trabajo. Por ejemplo:\
   `[DEBUG] "Executing Invoke DDX Process step"`

* Salida de cada paso del flujo de trabajo. Por ejemplo:\
   `[DEBUG] "Successfully finished Invoke DDX Process step"`

* Mensajes de invocación del servicio. Por ejemplo:\
   `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* Mensajes de salida del servicio. Por ejemplo:\
   `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* Variables leídas desde el mapa de metadatos. Por ejemplo:\
   `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* Variables escritas en el repositorio JCR. Por ejemplo:

   ```
      [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
   ```

* Mensajes de excepción con seguimiento de pila completo. Por ejemplo:\
   `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* Parámetros de metadatos de pasos dinámicos. Por ejemplo:

   ```
   [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
    [DEBUG] Locale to be used for Document of Record is <locale>
   ```

El siguiente ejemplo ilustra los registros del paso Firmar Documento:

```xml
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

Utilice los registros para evaluar que:

* Está utilizando una configuración de firma de adobe correcta.
* El servicio Adobe Sign se cierra después de crear un acuerdo correctamente.
* El paso Firmar Documento sale con un mensaje de éxito.

Si hay una excepción, puede realizar la vista del seguimiento completo de la pila para evaluar la causa del error.

## Habilitar el registro de depuración para flujos de trabajo de AEM Forms {#enable-debug-logging-for-aem-forms-workflows}

Siga estos pasos para habilitar el registro de depuración para flujos de trabajo de AEM Forms:

1. Vaya al administrador de configuración de la consola web de AEM en:

   https://&#39;[server]:[port]&#39;/system/console/configMgr

1. Seleccione **[!UICONTROL Sling]** > Compatibilidad con **[!UICONTROL registro]**.
1. Toque **[!UICONTROL Añadir nuevo registrador.]**
1. Seleccione **[!UICONTROL Depurar]** como nivel **[!UICONTROL de registro]**.
1. Especifique la ubicación del archivo de registro. La ubicación predeterminada para el archivo de registro es: *logs\error.log*
1. Especifique el nombre del paquete como **com.adobe.granite.workflow.core** en la columna **[!UICONTROL Logger]** .

   La ejecución de estos pasos permite almacenar los registros de depuración para el paquete **com.adobe.granite.workflow.core** . Toque **[!UICONTROL +]** y agregue los siguientes nombres de paquete a la lista:

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace

