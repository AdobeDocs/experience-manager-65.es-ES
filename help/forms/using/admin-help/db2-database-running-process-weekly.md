---
title: "Base de datos DB2: Ejecución semanal de un proceso"
seo-title: "DB2 database: Running a process weekly"
description: Vea cómo puede mejorar el rendimiento de la base de datos DB2 de AEM forms.
seo-description: See how you can improve the performance of your AEM forms DB2 database.
uuid: 36070087-c250-41df-a841-aa922e777697
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc0e8183-5d50-4fc0-997a-5f3168ba0d70
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Base de datos DB2: Ejecución de un proceso semanalmente{#db-database-running-a-process-weekly}

Si la base de datos DB2 de los formularios AEM empieza a ejecutarse lentamente, la ejecución semanal del siguiente proceso puede mejorar su rendimiento:

1. Iniciar centro de control DB2:

   (Windows) Seleccione Inicio > Programas > IBM DB2 > Herramientas de administración general > Centro de control.

   (Linux y UNIX) Desde un símbolo del sistema, escriba la variable `db2jcc` comando.

1. En el árbol de objetos del Centro de control de DB2, haga clic en Todas las bases de datos.
1. Haga clic en la base de datos creada para AEM formularios y haga clic en la carpeta Tablas .
1. Seleccione todas las tablas de la base de datos en el panel de contenido, haga clic con el botón derecho en ellas y seleccione Ejecutar estadísticas.
1. Vaya a Estadísticas > Estadísticas de índice.
1. Seleccione Recopilar estadísticas para todos los índices, seleccione Recopilar estadísticas para índices con estadísticas detalladas extendidas y, a continuación, haga clic en Aceptar.

Aparece un mensaje cuando se completa el proceso. Cierre el mensaje.
