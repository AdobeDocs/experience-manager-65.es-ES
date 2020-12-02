---
title: '"Base de datos DB2: Ejecución semanal de un proceso"'
seo-title: '"Base de datos DB2: Ejecución semanal de un proceso"'
description: Vea cómo puede mejorar el rendimiento de la base de datos DB2 de formularios AEM.
seo-description: Vea cómo puede mejorar el rendimiento de la base de datos DB2 de formularios AEM.
uuid: 36070087-c250-41df-a841-aa922e777697
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc0e8183-5d50-4fc0-997a-5f3168ba0d70
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Base de datos DB2: Ejecución semanal de un proceso{#db-database-running-a-process-weekly}

Si la base de datos de DB2 de los formularios AEM empieza a ejecutarse lentamente, la ejecución semanal del siguiente proceso puede mejorar su rendimiento:

1. Centro de control DB2 de inicio:

   (Windows) Seleccione Inicio > Programas > IBM DB2 > Herramientas de administración general > Centro de control.

   (Linux y UNIX) En un símbolo del sistema, escriba el comando `db2jcc`.

1. En el árbol de objetos de DB2 Control Center, haga clic en Todas las bases de datos.
1. Haga clic en la base de datos que ha creado para AEM formularios y haga clic en la carpeta Tablas.
1. Seleccione todas las tablas de la base de datos en el panel de contenido, haga clic con el botón derecho en ellas y seleccione Ejecutar estadísticas.
1. Vaya a Estadísticas > Estadísticas de índice.
1. Seleccione Recopilar estadísticas de todos los índices, seleccione Recopilar estadísticas de índices con estadísticas detalladas extendidas y, a continuación, haga clic en Aceptar.

Aparece un mensaje cuando se completa el proceso. Cierre el mensaje.
