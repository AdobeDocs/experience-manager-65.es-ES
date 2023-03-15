---
title: Depurar datos de procesos
seo-title: Purging process data
description: AEM Los datos de proceso que se generan cuando se invoca un proceso de larga duración pueden llegar a ser demasiado grandes, lo que da como resultado un rendimiento de formularios más bajo y el uso de espacio en disco innecesario. Consulte cómo puede depurar datos de proceso.
seo-description: Process data that is generated when a long-lived process is invoked can become too large, resulting in lower AEM forms performance and the use of unnecessary disk space. See how you can purge process data.
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 6%

---

# Depurar datos de procesos {#purging-process-data}

AEM Los datos de proceso que se generan cuando se invoca un proceso de larga duración pueden llegar a ser demasiado grandes, lo que da como resultado un rendimiento de formularios más bajo y el uso de espacio en disco innecesario. Se recomienda depurar los datos de proceso cuando ya no son necesarios los registros. AEM Los formularios de ofrecen varios medios para purgar datos de procesos:

* Puede utilizar la consola de administración para realizar una depuración única de registros obsoletos relacionados con procesos de larga duración o para programar depuraciones automáticas regulares. (Consulte [Purgar registros de la base de datos de Job Manager](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* AEM Puede utilizar la API de Java y la API del servicio web de formularios para depurar mediante programación los datos de proceso relacionados con procesos de larga duración. (Consulte &quot;Depuración de datos de proceso&quot; en [AEM Programar con formularios de](https://www.adobe.com/go/learn_aemforms_programming_63).)
* Utilice la herramienta de depuración de procesos para depurar procesos en función del nombre del proceso y otros parámetros. Para obtener más información, consulte el archivo léame de la herramienta de depuración de procesos, ubicado en *[raíz de aem_forms]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.
