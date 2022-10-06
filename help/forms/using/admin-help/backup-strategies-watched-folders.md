---
title: Estrategias de copia de seguridad para carpetas vigiladas
seo-title: Backup strategies for watched folders
description: Este documento describe cómo las carpetas vigiladas se ven afectadas por diferentes escenarios de backup y recuperación, las limitaciones y los resultados de estos escenarios y cómo minimizar la pérdida de datos.
seo-description: This document describes how watched folders are affected by different backup and recovery scenarios, the limitations and outcomes of these scenarios, and how to minimize data loss.
uuid: c61997b8-6c36-4bd9-90e5-411841a6c176
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f775933-e989-4456-ad01-9bdf5dee3dad
exl-id: 0d36160a-29fa-4cc4-a0ff-fc681d3e040e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 2%

---

# Estrategias de copia de seguridad para carpetas vigiladas {#backup-strategies-for-watched-folders}

Este contenido describe cómo las carpetas vigiladas se ven afectadas por diferentes escenarios de backup y recuperación, las limitaciones y los resultados de estos escenarios y cómo minimizar la pérdida de datos.

*Carpeta vigilada* es una aplicación basada en el sistema de archivos que invoca operaciones de servicio configuradas que manipulan el archivo dentro de una de las siguientes carpetas en la jerarquía de carpetas vigiladas:

* Entrada
* Escenario
* Salida
* Error
* Preservar

Una aplicación de usuario o cliente coloca primero el archivo o la carpeta en la carpeta de entrada. A continuación, la operación de servicio mueve el archivo a la carpeta de escenario para su procesamiento. Una vez que el servicio realiza la operación especificada, guarda el archivo modificado en la carpeta de salida. Los archivos de origen procesados correctamente se mueven a la carpeta de conservación y los archivos de procesamiento fallidos se mueven a la carpeta de errores. Cuando la variable `Preserve On Failure` para la carpeta observada está activada, los archivos de origen procesados con errores se mueven a la carpeta preserve. (Consulte [Configuración de extremos de carpeta vigilados](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints).)

Puede realizar una copia de seguridad de las carpetas vigiladas haciendo una copia de seguridad del sistema de archivos.

>[!NOTE]
>
>Esta copia de seguridad es independiente del proceso de backup y recuperación de la base de datos o del almacenamiento de documentos.

## Cómo funcionan las carpetas vigiladas {#how-watched-folders-work}

Este contenido describe el proceso de manipulación de archivos de carpetas vigiladas. Es importante comprender este proceso antes de desarrollar un plan de recuperación. En este ejemplo, la variable `Preserve On Failure` para la carpeta observada está activada. Los archivos se procesan en el orden en que llegan.

En la tabla siguiente se describe la manipulación de archivos de cinco archivos de ejemplo (archivo1, archivo2, archivo3, archivo4, archivo5) a lo largo del proceso. En la tabla, el eje x representa el tiempo, como Tiempo 1 o T1, y el eje y representa las carpetas dentro de la jerarquía de carpetas vigilada, como Entrada.

<table>
 <thead>
  <tr>
   <th><p>Carpeta</p></th>
   <th><p>T1</p></th>
   <th><p>T2</p></th>
   <th><p>T3</p></th>
   <th><p>T4</p></th>
   <th><p>T5</p></th>
   <th><p>T6</p></th>
   <th><p>T7</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Entrada</p></td>
   <td><p>archivo1, archivo2, archivo3, archivo4</p></td>
   <td><p>archivo2, archivo3, archivo4</p></td>
   <td><p>file3, file4</p></td>
   <td><p>file4</p></td>
   <td><p>empty</p></td>
   <td><p>file5</p></td>
   <td><p>empty</p></td>
  </tr>
  <tr>
   <td><p>Escenario</p></td>
   <td><p>empty</p></td>
   <td><p>file1</p></td>
   <td><p>file2</p></td>
   <td><p>file3</p></td>
   <td><p>file4</p></td>
   <td><p>empty</p></td>
   <td><p>file5</p></td>
  </tr>
  <tr>
   <td><p>Salida</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>file1_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
  </tr>
  <tr>
   <td><p>Error</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>file3_failed, file3 </p></td>
   <td><p>file3_failed, file3 </p></td>
   <td><p>file3_failed, file3 </p></td>
  </tr>
  <tr>
   <td><p>Preservar</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>file1 </p></td>
   <td><p>archivo1, archivo2 </p></td>
   <td><p>archivo1, archivo2 </p></td>
   <td><p>archivo1, archivo2, archivo4 </p></td>
   <td><p>archivo1, archivo2, archivo4 </p></td>
  </tr>
 </tbody>
</table>

El siguiente texto describe la manipulación de archivos para cada vez:

**T1:** Los cuatro archivos de ejemplo se colocan en la carpeta de entrada.

**T2:** La operación de servicio mueve el archivo1 a la carpeta de etapa para su manipulación.

**T3:** La operación de servicio mueve el archivo2 a la carpeta de escenario para su manipulación. Coloca los resultados del archivo1 en la carpeta de salida y mueve el archivo1 a la carpeta de preservación.

**T4:** La operación de servicio coloca file3 en la carpeta de etapa para su manipulación. Coloca los resultados de file2 en la carpeta de salida y coloca file2 en la carpeta preserve.

**T5:** La operación de servicio coloca file4 en la carpeta de etapa para su manipulación. La manipulación de file3 falla y la operación de servicio la coloca en la carpeta de errores.

**T6:** La operación de servicio coloca file5 en la carpeta de entrada. Coloca los resultados de file4 en la carpeta de salida, coloca file4 en la carpeta preserve.

**T7:** La operación de servicio coloca file5 en la carpeta de etapa para su manipulación.

## Copia de seguridad de carpetas vigiladas {#backing-up-watched-folders}

Se recomienda realizar una copia de seguridad de todo el sistema de archivos de carpetas vigilado en otro sistema de archivos.

## Restauración de carpetas vigiladas {#restoring-watched-folders}

En esta sección se describe cómo restaurar carpetas vigiladas. Las carpetas vigiladas suelen invocar procesos de corta duración que se completan en un minuto. En estos casos, restaurar la carpeta vigilada con una copia de seguridad que se realiza cada hora no impedirá la pérdida de datos.

Por ejemplo, si se realiza una copia de seguridad en el momento T1 y el servidor falla en T7, entonces file1, file2, file3 y file4 ya están manipulados. Restaurar la carpeta vigilada con una copia de seguridad realizada en T1 no impide la pérdida de datos.

Si se realizó una copia de seguridad más reciente, puede restaurar los archivos. Al restaurar los archivos, tenga en cuenta en qué carpeta de jerarquía de carpetas vigiladas reside el archivo actual:

**Etapa:** Los archivos de esta carpeta se procesan de nuevo una vez restaurada la carpeta vigilada.

**Entrada:** Los archivos de esta carpeta se procesan de nuevo una vez restaurada la carpeta vigilada.

**Resultado:** Los archivos de esta carpeta no se procesan.

**Salida:** Los archivos de esta carpeta no se procesan.

**Conservar:** Los archivos de esta carpeta no se procesan.

## Estrategias para minimizar la pérdida de datos {#strategies-to-minimize-data-loss}

Las siguientes estrategias pueden minimizar la pérdida de datos de la carpeta de entrada y salida al restaurar una carpeta vigilada:

* Haga una copia de seguridad de las carpetas de salida y de error con frecuencia, como cada hora, para evitar la pérdida de archivos de resultado y de error.
* Haga una copia de seguridad de los archivos de entrada en una carpeta que no sea la carpeta vigilada. Esto garantiza la disponibilidad del archivo después de la recuperación en caso de que no pueda encontrar los archivos en la carpeta de salida o de error. Asegúrese de que el esquema de nombres de archivos sea coherente.

   Por ejemplo, si está guardando la salida con `%F.`*Extensión*, el archivo de salida tendrá el mismo nombre que el archivo de entrada. Esto le ayuda a determinar qué archivos de entrada se manipulan y cuáles se deben volver a enviar. Si solo ve el archivo file1_out en la carpeta de resultados y no file2_out, file3_out y file4_out, debe volver a enviar el archivo2, file3 y file4.

* Si la copia de seguridad de la carpeta vigilada disponible es anterior al tiempo que se tarda en procesar el trabajo, debe permitir que el sistema cree una nueva carpeta vigilada y coloque automáticamente los archivos en la carpeta de entrada.
* Si la última copia de seguridad disponible no es lo suficientemente reciente, el tiempo de copia de seguridad es menor que el tiempo que se tarda en procesar los archivos y se restaura la carpeta vigilada, el archivo se manipuló en una de las siguientes etapas:

   * **Etapa 1:** En la carpeta de entrada
   * **Etapa 2:** Se ha copiado en la carpeta del escenario, pero el proceso aún no se ha invocado
   * **Etapa 3:** Se copia en la carpeta de ensayo y se invoca el proceso
   * **Fase 4:** Manipulación en curso
   * **Etapa 5:** Resultados devueltos

   Si los archivos están en la fase 1, se manipularán. Si los archivos están en las etapas 2 o 3, colóquelos en la carpeta de entrada para que la manipulación vuelva a tener lugar.

   >[!NOTE]
   >
   >Si la manipulación de un archivo se produce más de una vez, se evitará la pérdida de datos, pero los resultados pueden duplicarse.

## Conclusión {#conclusion}

Debido a la naturaleza dinámica y cambiante de una carpeta vigilada, la restauración de las carpetas vigiladas debe realizarse con archivos de los que se haga una copia de seguridad en un día. Una práctica recomendada sería realizar una copia de seguridad de los resultados, almacenar la carpeta de entrada en un servidor y realizar un seguimiento de los archivos de entrada para que pueda volver a enviar el trabajo en caso de que se produzca un error.
