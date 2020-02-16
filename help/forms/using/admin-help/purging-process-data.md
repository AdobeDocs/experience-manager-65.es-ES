---
title: Depuración de datos de proceso
seo-title: Depuración de datos de proceso
description: Los datos de proceso que se generan cuando se invoca un proceso de larga duración pueden llegar a ser demasiado grandes, lo que reduce el rendimiento de los formularios AEM y reduce el uso de espacio en disco innecesario. Vea cómo puede depurar los datos del proceso.
seo-description: Los datos de proceso que se generan cuando se invoca un proceso de larga duración pueden llegar a ser demasiado grandes, lo que reduce el rendimiento de los formularios AEM y reduce el uso de espacio en disco innecesario. Vea cómo puede depurar los datos del proceso.
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Depuración de datos de proceso {#purging-process-data}

Los datos de proceso que se generan cuando se invoca un proceso de larga duración pueden llegar a ser demasiado grandes, lo que reduce el rendimiento de los formularios AEM y reduce el uso de espacio en disco innecesario. Se recomienda depurar los datos del proceso cuando ya no se necesitan registros. Los formularios AEM ofrecen varios medios para depurar datos de proceso:

* Puede utilizar la consola de administración para realizar una purga única de registros obsoletos relacionados con procesos de larga duración o programar purgas automáticas regulares. (Consulte [Purgar registros de la base de datos](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)de Job Manager).
* Puede utilizar la API de Java y la API de servicio web de AEM Forms para purgar mediante programación los datos de procesos relacionados con procesos de larga duración. (Consulte &quot;Depuración de datos de proceso&quot; en [Programación con formularios](https://www.adobe.com/go/learn_aemforms_programming_63)AEM).
* Utilice la herramienta de depuración de procesos para purgar procesos en función del nombre del proceso y otros parámetros. Para obtener más información, consulte el archivo léame de la herramienta de depuración de procesos, ubicado en *[aem_forms root]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.

