---
title: '"Base de datos IBM DB2: Ejecución de comandos para mantenimiento regular"'
seo-title: '"Base de datos IBM DB2: Ejecución de comandos para mantenimiento regular"'
description: Este documento lista comandos IBM DB2 recomendados para el mantenimiento regular de la base de datos de formularios AEM.
seo-description: Este documento lista comandos IBM DB2 recomendados para el mantenimiento regular de la base de datos de formularios AEM.
uuid: 235d59df-b9b9-4770-8b7d-00713701c3c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a62b68b4-7735-49b1-8938-f0d9e4c4a051
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# Base de datos IBM DB2: Ejecución de comandos para mantenimiento regular {#ibm-db-database-running-commands-for-regular-maintenance}

Se recomiendan los siguientes comandos IBM DB2 para el mantenimiento regular de la base de datos de formularios AEM. Para obtener información detallada sobre el mantenimiento y el ajuste del performance de la base de datos DB2, consulte *Guía de administración de IBM DB2*.

* **runstats:** Este comando actualiza las estadísticas que describen las características físicas de una tabla de base de datos, junto con sus índices asociados. Las sentencias SQL dinámicas generadas por AEM formularios utilizan automáticamente estas estadísticas actualizadas, pero las sentencias SQL estáticas generadas dentro de una base de datos requieren que el comando `db2rbind` también se ejecute.
* **db2rbind:** Este comando reune todos los paquetes de la base de datos. Utilice este comando después de ejecutar la utilidad `runstats` para revalidar todos los paquetes de la base de datos.
* **reorganizar tabla o índice:** Este comando comprueba si es necesario reorganizar algunas tablas e índices.

   A medida que las bases de datos crecen y cambian, es fundamental volver a calcular las estadísticas de las tablas para mejorar el rendimiento de las bases de datos y se deben realizar con regularidad. Estos comandos se pueden ejecutar manualmente mediante secuencias de comandos o mediante un trabajo cron.

>[!NOTE]
>
>Antes de ejecutar el comando `runstats`, la base de datos debe contener datos y se debe realizar al menos una sincronización de directorio.

Para una base de datos pequeña, como para 10.000 usuarios o 2.500 grupos, es suficiente invocar el comando `runstats` para reducir los tiempos de sincronización.

Para bases de datos más grandes, como por ejemplo para 100.000 usuarios o 10.000 grupos, ejecute el comando `reorg` antes de ejecutar el comando `runstats`.

## Utilice el comando runstats de la base de datos de formularios AEM {#use-the-runstats-command-on-your-aem-forms-database}

Ejecute el comando `runstats` en las siguientes tablas e índices de la base de datos de formularios AEM.

>[!NOTE]
>
>El comando `runstats` sólo debe ejecutarse durante la primera sincronización de la base de datos. Sin embargo, debe ejecutarse dos veces durante ese proceso: una vez durante la sincronización de Usuarios y Grupos y luego durante la sincronización de Miembros del Grupo. Asegúrese de que la secuencia de comandos se ejecuta completamente cada vez que la ejecute.

Para obtener información sobre la sintaxis y el uso correctos, consulte la documentación del fabricante de la base de datos. A continuación, `<schema>` se utiliza para denotar el esquema asociado con el nombre de usuario de DB2. Si tiene una simple instalación de DB2 predeterminada, éste es el nombre del esquema de la base de datos.

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

## Ejecute el comando reorganizar en la base de datos de formularios AEM {#run-the-reorg-command-on-your-aem-forms-database}

Ejecute el comando `reorg` en las siguientes tablas e índices de la base de datos de formularios AEM. Para obtener información sobre la sintaxis y el uso correctos, consulte la documentación del fabricante de la base de datos.

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

