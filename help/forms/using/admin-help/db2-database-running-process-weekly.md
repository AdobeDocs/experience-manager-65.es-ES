---
title: "DB2&reg; database: Ejecución de un proceso semanal"
description: Descubra cómo puede mejorar el rendimiento de su base de datos AEM Forms DB2&reg;.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Base de datos DB2®: Ejecución semanal de un proceso{#db-database-running-a-process-weekly}

Si la base de datos AEM Forms DB2® empieza a ejecutarse lentamente, la ejecución semanal del siguiente proceso puede mejorar su rendimiento:

1. Iniciar el Centro de control de DB2®:

   (Windows) Seleccione Inicio > Programas > IBM® DB2® > Herramientas generales de administración > Centro de control.

   (Linux® y UNIX®) Desde un símbolo del sistema, escriba el `db2jcc` comando.

1. En el árbol de objetos del Centro de control de DB2®, haga clic en Todas las bases de datos.
1. Haga clic en la base de datos que ha creado para AEM Forms y haga clic en la carpeta Tablas.
1. Seleccione todas las tablas de base de datos en el panel de contenido, haga clic con el botón secundario en ellas y seleccione Ejecutar estadísticas.
1. Vaya a Estadísticas > Estadísticas de índice.
1. Seleccione Recopilar estadísticas para todos los índices, seleccione Recopilar estadísticas para índices con estadísticas detalladas extendidas y, a continuación, haga clic en Aceptar.

Aparece un mensaje cuando se completa el proceso. Cierre el mensaje.
