---
title: Comprobaciones de coherencia y travesía
seo-title: Comprobaciones de coherencia y travesía
description: Aprenda a realizar comprobaciones de coherencia y transversal.
seo-description: Aprenda a realizar comprobaciones de coherencia y transversal.
uuid: 0304e378-7c60-4bf5-9052-d01149d2a6df
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: af9a3e9d-194a-42e5-be28-b238e0c1e55e
feature: Configuración
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Comprobaciones de coherencia y travesía{#consistency-and-traversal-checks}

Al actualizar puede haber problemas debido a incoherencias en el espacio de trabajo. Puede ejecutar una actualización de prueba para ver si esto supone un problema o ejecutar las comprobaciones de coherencia como acción preventiva.

Si ejecuta una actualización de prueba que falla debido a incoherencias en el espacio de trabajo, verá entradas similares a las siguientes en crx-quickstart/logs/crx/error.log:

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## Realizar una comprobación de coherencia {#perform-a-consistency-check}

Para realizar una comprobación de consistencia, vaya a la página de administración de JMX Mbean** com.adobe.granite (Repository)**. Desde la pantalla principal de AEM, vaya a:

**Herramientas > Consola web > Principal (en la barra de menús) > JMX > com.adobe.granite (Repositorio)**

En una instalación predeterminada, se encuentra aquí:  **[|Mostrar|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

En la sección **Operations** de la página encontrará dos métodos: **`traversalCheck`** y **`consistencyCheck`**. Para ejecutar una comprobación, haga clic en la operación e introduzca los parámetros deseados.

![chlimage_1-117](assets/chlimage_1-117.png)

