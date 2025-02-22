---
title: Depurar datos de procesos
description: AEM Los datos de proceso que se generan cuando se invoca un proceso de larga duración pueden llegar a ser demasiado grandes, lo que da como resultado un rendimiento de formularios más bajo y el uso de espacio en disco innecesario. Consulte cómo puede depurar datos de proceso.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 3%

---

# Depurar datos de procesos {#purging-process-data}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

AEM Los datos de proceso que se generan cuando se invoca un proceso de larga duración pueden llegar a ser demasiado grandes, lo que da como resultado un rendimiento de formularios más bajo y el uso de espacio en disco innecesario. Se recomienda depurar los datos de proceso cuando ya no son necesarios los registros. AEM Los formularios de ofrecen varios medios para purgar datos de procesos:

* Puede utilizar la consola de administración para realizar una depuración única de registros obsoletos relacionados con procesos de larga duración o para programar depuraciones automáticas regulares. (Consulte [Purgar registros de la base de datos de Job Manager](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* AEM Puede utilizar la API de Java y la API del servicio web de formularios para depurar mediante programación los datos de proceso relacionados con procesos de larga duración. AEM (Consulte &quot;Depuración de datos de proceso&quot; en [Programación con formularios de la lista de distribución de formularios](https://www.adobe.com/go/learn_aemforms_programming_63)).
* Utilice la herramienta de depuración de procesos para depurar procesos en función del nombre del proceso y otros parámetros. Para obtener más información, consulte el archivo léame de la herramienta de depuración de procesos, en *[raíz de aem_forms]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.
