---
title: Registrar flujos de trabajo de AEM Forms
description: Depure los problemas del flujo de trabajo de AEM Forms y habilite el registro de depuración de los flujos de trabajo de AEM Forms para ver los registros.
uuid: 869d0271-c7e3-4b6d-8e63-893dc6af8b8a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 14bb521a-42ea-4fe2-90fb-202e7ddf917a
docset: aem65
exl-id: 601c8d95-0d1a-4945-a522-e85d3e9fc4ae
source-git-commit: 20b0d0db54dc30285c056a10032f02ba45f8baca
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 94%

---

# Registrar flujos de trabajo de AEM Forms{#logging-in-aem-forms-workflows}

Los pasos de flujo de trabajo de Forms proporcionan registros detallados para depurar convenientemente los problemas relacionados con los flujos de trabajo. Habilite el registro de depuración de los flujos de trabajo de AEM Forms para ver los registros.

De forma predeterminada, toda la información del registro está disponible en el archivo **error.log** del directorio */crx-repository/logs/*.

Los registros de depuración de los flujos de trabajo de formularios incluyen:

* La entrada de cada paso del flujo de trabajo. Por ejemplo:\
  `[DEBUG] "Executing Invoke DDX Process step"`

* La salida de cada paso del flujo de trabajo. Por ejemplo:\
  `[DEBUG] "Successfully finished Invoke DDX Process step"`

* Mensajes de invocación del servicio. Por ejemplo:\
  `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* Mensajes de salida del servicio. Por ejemplo:\
  `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* Variables leídas desde el mapa de metadatos. Por ejemplo:\
  `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* Variables escritas en el repositorio JCR. Por ejemplo:

  ```verilog
     [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
  ```

* Mensajes de excepción con seguimiento de pila completo. Por ejemplo:\
  `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* Parámetros de metadatos de paso dinámico. Por ejemplo:

  ```verilog
  [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
   [DEBUG] Locale to be used for Document of Record is <locale>
  ```

El siguiente ejemplo ilustra los registros del paso Firmar documento:

```verilog
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

Utilice los registros para evaluar lo siguiente:

* Utiliza la configuración correcta de Adobe Sign.
* El servicio de Adobe Sign se cierra después de crear correctamente un acuerdo.
* El paso Firmar documento se cierra con un mensaje de éxito.

Si se produce una excepción, puede ver el seguimiento de pila completo para evaluar la causa del error.

## Habilitar el registro de depuración en flujos de trabajo de AEM Forms {#enable-debug-logging-for-aem-forms-workflows}

Realice los siguientes pasos para habilitar el registro de depuración en flujos de trabajo de AEM Forms:

1. Vaya al Administrador de configuración de la consola web de AEM en:

   https://&#39;[server]:[puerto]&#39;/system/console/configMgr

1. Seleccione **[!UICONTROL Sling]** > **[!UICONTROL Compatibilidad de registros]**.
1. Toque **[!UICONTROL Añadir nuevo registrador.]**
1. Seleccione **[!UICONTROL Depuración]** como **[!UICONTROL Nivel de registro]**.
1. Especifique la ubicación del archivo de registro. La ubicación predeterminada para el archivo de registro es *logs\error.log*.
1. Especifique el nombre del paquete como **com.adobe.granite.workflow.core** en la columna **[!UICONTROL Registrador]**.

   La ejecución de estos pasos permite almacenar los registros de depuración del paquete **com.adobe.granite.workflow.core**. Toque **[!UICONTROL +]** y añada los siguientes nombres de paquete a la lista:

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace
