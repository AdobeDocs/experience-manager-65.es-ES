---
title: '"Base de datos de Microsoft SQL Server: Ajustar la configuración"'
seo-title: '"Base de datos de Microsoft SQL Server: Ajustar la configuración"'
description: Descubra cómo puede ajustar la configuración de la base de datos de Microsoft SQL Server.
seo-description: Descubra cómo puede ajustar la configuración de la base de datos de Microsoft SQL Server.
uuid: 2d618aab-3c67-4edb-a28f-a20904689e6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 70559a94-42ea-411a-a32f-5f38bc17ff96
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Base de datos de Microsoft SQL Server: Ajustar la configuración {#microsoft-sql-server-database-fine-tuning-the-configuration}

Debe cambiar la configuración predeterminada al utilizar Microsoft SQL Server. Haga clic con el botón derecho en el servidor local de Oracle Enterprise Manager para acceder al cuadro de diálogo de propiedades.

## Configuración de memoria {#memory-settings}

Cambie la asignación mínima de memoria a un número lo más grande posible. Si la base de datos se está ejecutando en un equipo independiente, utilice toda la memoria. La configuración predeterminada no asigna la memoria de forma agresiva, lo que dificulta el rendimiento en casi cualquier base de datos. Debe ser más agresivo en la asignación de memoria a los equipos de producción.

## Configuración del procesador {#processor-settings}

Modifique la configuración del procesador y, lo que es más importante, active la casilla de verificación Ampliar prioridad de SQL Server en Windows para que el servidor utilice tantos ciclos como sea posible. El ajuste Usar fibras NT es menos importante, pero es posible que también desee seleccionarlo.

## Configuración de la base de datos {#database-settings}

Cambie la configuración de la base de datos. La configuración más importante es Intervalo de recuperación, que especifica la cantidad máxima de tiempo de espera para la recuperación después de un bloqueo. La configuración predeterminada es de un minuto. El uso de un valor mayor, de 5 a 15 minutos, mejora el rendimiento porque le da al servidor más tiempo para escribir cambios desde el registro de la base de datos en los archivos de la base de datos.

>[!NOTE]
>
>Esta configuración no pone en peligro el comportamiento transaccional porque sólo cambia la duración de la reproducción del archivo de registro que debe realizarse al iniciar.

Configure el tamaño asignado de espacio tanto para el registro como para el archivo de datos para que sea mucho mayor que el de la base de datos inicial. Considere cuánto puede crecer la base de datos a lo largo de un año. Lo ideal es que los archivos de registro y datos se asignen en forma contigua para que los datos no terminen fragmentados en todo el disco.
