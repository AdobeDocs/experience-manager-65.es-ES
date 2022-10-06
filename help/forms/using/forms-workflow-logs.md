---
title: Inicio de sesión en flujos de trabajo de AEM Forms
seo-title: Logging in AEM Forms workflows
description: Utilice los registros para depurar los problemas del flujo de trabajo de AEM Forms.
seo-description: Use logs to debug AEM Forms workflow issues.
uuid: 869d0271-c7e3-4b6d-8e63-893dc6af8b8a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 14bb521a-42ea-4fe2-90fb-202e7ddf917a
docset: aem65
exl-id: 601c8d95-0d1a-4945-a522-e85d3e9fc4ae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 8%

---

# Inicio de sesión en flujos de trabajo de AEM Forms{#logging-in-aem-forms-workflows}

Los pasos del flujo de trabajo de Forms proporcionan registros detallados para depurar convenientemente los problemas relacionados con el flujo de trabajo. Habilite el registro de depuración para flujos de trabajo de AEM Forms para ver los registros.

De forma predeterminada, toda la información de registro está disponible en la **error.log** en el */crx-repository/logs/* directorio.

Los registros de depuración para los flujos de trabajo de formularios incluyen:

* Entrada de cada paso del flujo de trabajo. Por ejemplo:\
   `[DEBUG] "Executing Invoke DDX Process step"`

* Salida de cada paso del flujo de trabajo. Por ejemplo:\
   `[DEBUG] "Successfully finished Invoke DDX Process step"`

* Mensajes de invocación de servicio. Por ejemplo:\
   `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* Mensajes de salida del servicio. Por ejemplo:\
   `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* Variables leídas desde el mapa de metadatos. Por ejemplo:\
   `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* Variables escritas en el repositorio JCR. Por ejemplo:

   ```verilog
      [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
   ```

* Mensajes de excepción con seguimiento completo de pila. Por ejemplo:\
   `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* Parámetros de metadatos de paso dinámico. Por ejemplo:

   ```verilog
   [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
    [DEBUG] Locale to be used for Document of Record is <locale>
   ```

El siguiente ejemplo ilustra los registros del paso Firmar documento :

```verilog
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

Utilice los registros para evaluar que:

* Está utilizando una configuración correcta de adobe sign.
* El servicio de Adobe Sign se cierra después de crear un acuerdo correctamente.
* El paso Firmar documento se cierra con un mensaje de éxito.

Si hay una excepción, puede ver el seguimiento completo de la pila para evaluar la causa del error.

## Habilitar el registro de depuración para flujos de trabajo de AEM Forms {#enable-debug-logging-for-aem-forms-workflows}

Realice los siguientes pasos para habilitar el registro de depuración para los flujos de trabajo de AEM Forms:

1. Vaya al Administrador de configuración de la consola web de AEM en:

   https://&#39;[server]:[puerto]&#39;/system/console/configMgr

1. Select **[!UICONTROL Sling]** > **[!UICONTROL Compatibilidad de registros]**.
1. Toque **[!UICONTROL Añada un nuevo registrador.]**
1. Select **[!UICONTROL Depuración]** como el **[!UICONTROL Nivel de registro]**.
1. Especifique la ubicación del archivo de registro. La ubicación predeterminada para el archivo de registro es: *logs\error.log*
1. Especifique el nombre del paquete como **com.adobe.granite.workflow.core** en el **[!UICONTROL Registrador]** para abrir el Navegador.

   La ejecución de estos pasos permite almacenar los registros de depuración para la variable **com.adobe.granite.workflow.core** paquete. Toque **[!UICONTROL +]** y añada los siguientes nombres de paquete a la lista:

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace
