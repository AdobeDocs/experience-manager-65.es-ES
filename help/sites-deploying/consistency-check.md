---
title: Comprobaciones de coherencia y recorrido
description: Aprenda a realizar comprobaciones de coherencia y transversales.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
feature: Configuring
exl-id: 10dde29b-5dc7-4d4e-80ae-3d4fd0397f7e
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Comprobaciones de coherencia y recorrido{#consistency-and-traversal-checks}

Al actualizar, puede haber problemas debido a incoherencias en el espacio de trabajo. Puede ejecutar una actualización de prueba para ver si se trata de un problema o ejecutar las comprobaciones de coherencia como acción preventiva.

Si ejecuta una actualización de prueba que falla debido a incoherencias en el espacio de trabajo, verá entradas similares a las siguientes en crx-quickstart/logs/crx/error.log:

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## Realizar una comprobación de coherencia {#perform-a-consistency-check}

Para realizar una comprobación de coherencia, vaya a la página de administración del MBean JMX **com.adobe.granite (Repositorio)**. AEM En la pantalla principal de la, vaya a:

**Herramientas > Consola web > Principal (en la barra de menús) > JMX > com.adobe.granite (Repositorio)**

En una instalación predeterminada, se encuentra aquí:  **[|Mostrarme|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

En el **Operaciones** de la página, encontrará dos métodos: **`traversalCheck`** y **`consistencyCheck`**. Para ejecutar una comprobación, haga clic en la operación e introduzca los parámetros deseados.

![chlimage_1-117](assets/chlimage_1-117.png)
