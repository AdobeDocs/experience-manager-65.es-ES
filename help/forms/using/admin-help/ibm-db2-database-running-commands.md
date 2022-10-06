---
title: "Base de datos IBM DB2: Ejecución de comandos para mantenimiento regular"
seo-title: "IBM DB2 database: Running commands for regular maintenance"
description: Este documento enumera los comandos IBM DB2 recomendados para el mantenimiento regular de la base de datos de formularios AEM.
seo-description: This document lists IBM DB2 commands that are recommended for regular maintenance of your AEM forms database.
uuid: 235d59df-b9b9-4770-8b7d-00713701c3c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a62b68b4-7735-49b1-8938-f0d9e4c4a051
exl-id: 7a4281e7-1544-473a-a471-e9a4c2819a58
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Base de datos IBM DB2: Ejecución de comandos para mantenimiento regular {#ibm-db-database-running-commands-for-regular-maintenance}

Se recomiendan los siguientes comandos IBM DB2 para el mantenimiento regular de la base de datos de formularios AEM. Para obtener información detallada sobre el mantenimiento y el ajuste del rendimiento de la base de datos DB2, consulte *Guía de administración de IBM DB2*.

* **runstats:** Este comando actualiza las estadísticas que describen las características físicas de una tabla de base de datos, junto con sus índices asociados. Las instrucciones SQL dinámicas generadas por AEM formularios utilizan automáticamente estas estadísticas actualizadas, pero las instrucciones SQL estáticas creadas dentro de una base de datos requieren que la variable `db2rbind` ejecute también.
* **db2rbind:** Este comando reagrupa todos los paquetes de la base de datos. Utilice este comando después de ejecutar el `runstats` para revalidar todos los paquetes de la base de datos.
* **tabla de reorganización o índice:** Este comando comprueba si es necesario reorganizar algunas tablas e índices.

   A medida que sus bases de datos crecen y cambian, es fundamental volver a calcular las estadísticas de las tablas para mejorar el rendimiento de las bases de datos y se debe hacer con regularidad. Estos comandos se pueden ejecutar manualmente utilizando secuencias de comandos o utilizando un trabajo cron.

>[!NOTE]
>
>Antes de ejecutar el `runstats` , la base de datos debe contener datos y se debe haber realizado al menos una sincronización de directorios.

Para una base de datos pequeña, como para 10 000 usuarios o 2 500 grupos, es suficiente invocar la variable `runstats` para reducir los tiempos de sincronización.

Para bases de datos más grandes, como para 100.000 usuarios o 10.000 grupos, ejecute el `reorg` antes de ejecutar el `runstats` comando.

## Utilice el comando runstats de la base de datos de AEM forms {#use-the-runstats-command-on-your-aem-forms-database}

Ejecute el `runstats` en las siguientes tablas e índices de base de datos de formularios AEM.

>[!NOTE]
>
>La variable `runstats` solo debe ejecutarse durante la primera sincronización de base de datos. Sin embargo, debe ejecutarse dos veces durante ese proceso: una vez durante la sincronización de Usuarios y Grupos y, a continuación, durante la sincronización de Miembros del grupo. Asegúrese de que la secuencia de comandos se ejecuta completamente cada vez que la ejecute.

Para obtener información sobre la sintaxis y el uso correctos, consulte la documentación del fabricante de la base de datos. Debajo, `<schema>` se utiliza para denotar el esquema asociado con su nombre de usuario de DB2. Si tiene una instalación DB2 predeterminada simple, este es el nombre del esquema de la base de datos.

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

## Ejecute el comando reorg en la base de datos de AEM forms {#run-the-reorg-command-on-your-aem-forms-database}

Ejecute el `reorg` en las siguientes tablas e índices de base de datos de formularios AEM. Para obtener información sobre la sintaxis y el uso correctos, consulte la documentación del fabricante de la base de datos.

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
