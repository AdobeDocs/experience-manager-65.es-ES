---
title: "Base de datos IBM DB2: Ejecución de comandos para el mantenimiento regular"
description: Este documento enumera los comandos de IBM AEM DB2 recomendados para realizar un mantenimiento regular de la base de datos de formularios en la que se realiza un seguimiento de los formularios en la.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a4281e7-1544-473a-a471-e9a4c2819a58
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 2%

---

# Base de datos IBM DB2: Ejecución de comandos para el mantenimiento regular {#ibm-db-database-running-commands-for-regular-maintenance}

Se recomiendan los siguientes comandos de IBM AEM DB2 para el mantenimiento regular de la base de datos de formularios de la aplicación de formularios de la. Para obtener información detallada sobre el mantenimiento y la optimización del rendimiento de la base de datos DB2, consulte *Guía de administración de IBM DB2*.

* **runstats:** Este comando actualiza las estadísticas que describen las características físicas de una tabla de base de datos, junto con sus índices asociados. AEM Las instrucciones SQL dinámicas generadas por los formularios utilizan automáticamente estas estadísticas actualizadas, pero las instrucciones SQL estáticas creadas dentro de una base de datos requieren que la variable `db2rbind` también se puede ejecutar el comando.
* **db2rbind:** Este comando vuelve a enlazar todos los paquetes de la base de datos. Utilice este comando después de ejecutar el `runstats` para volver a validar todos los paquetes de la base de datos.
* **reorganizar tabla o índice:** Este comando comprueba si es necesaria una reorganización de algunas tablas e índices.

  A medida que las bases de datos crecen y cambian, es fundamental recalcular las estadísticas de tabla para mejorar el rendimiento de la base de datos, y esto debe hacerse regularmente. Estos comandos se pueden ejecutar manualmente mediante scripts o mediante un trabajo cron.

>[!NOTE]
>
>Antes de ejecutar el `runstats` , la base de datos debe contener datos y se debe haber realizado al menos una sincronización de directorios.

Para una base de datos pequeña, como para 10 000 usuarios o 2500 grupos, basta con invocar el método `runstats` para reducir los tiempos de sincronización.

Para bases de datos más grandes, como para 100 000 usuarios o 10 000 grupos, ejecute el `reorg` antes de ejecutar el `runstats` comando.

## AEM Utilice el comando runstats de la base de datos de formularios de la {#use-the-runstats-command-on-your-aem-forms-database}

Ejecute el `runstats` AEM en las siguientes tablas e índices de la base de datos de formularios de la.

>[!NOTE]
>
>El `runstats` El comando solo debe ejecutarse durante la primera sincronización de la base de datos. Sin embargo, debe ejecutarse dos veces durante ese proceso: una vez durante la sincronización de Usuarios y Grupos y luego durante la sincronización de Miembros del Grupo. Asegúrese de que la secuencia de comandos se ejecuta por completo cada vez que la ejecuta.

Para obtener información sobre la sintaxis y el uso correctos, consulte la documentación del fabricante de la base de datos. Abajo, `<schema>` se utiliza para denotar el esquema asociado al nombre de usuario de DB2. Si tiene una instalación DB2 predeterminada simple, este es el nombre del esquema de la base de datos.

```sql
     TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALGROUPENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY FOR INDEXES ALL
```

## AEM Ejecute el comando reorg en la base de datos de formularios de la {#run-the-reorg-command-on-your-aem-forms-database}

Ejecute el `reorg` AEM en las siguientes tablas e índices de la base de datos de formularios de la. Para obtener información sobre la sintaxis y el uso correctos, consulte la documentación del fabricante de la base de datos.

```sql
     TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
```
