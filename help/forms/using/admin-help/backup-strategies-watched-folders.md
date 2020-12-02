---
title: Estrategias de copia de seguridad para carpetas vigiladas
seo-title: Estrategias de copia de seguridad para carpetas vigiladas
description: Este documento describe cómo las carpetas vigiladas se ven afectadas por diferentes escenarios de backup y recuperación, las limitaciones y los resultados de estos escenarios y cómo minimizar la pérdida de datos.
seo-description: Este documento describe cómo las carpetas vigiladas se ven afectadas por diferentes escenarios de backup y recuperación, las limitaciones y los resultados de estos escenarios y cómo minimizar la pérdida de datos.
uuid: c61997b8-6c36-4bd9-90e5-411841a6c176
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f775933-e989-4456-ad01-9bdf5dee3dad
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 2%

---


# Estrategias de copia de seguridad para carpetas vigiladas {#backup-strategies-for-watched-folders}

Este contenido describe cómo las carpetas vigiladas se ven afectadas por diferentes escenarios de backup y recuperación, las limitaciones y los resultados de estos escenarios y cómo minimizar la pérdida de datos.

*Watched* Folderis es una aplicación basada en el sistema de archivos que invoca operaciones de servicio configuradas que manipulan el archivo en una de las siguientes carpetas de la jerarquía de carpetas vigiladas:

* Entrada
* Escenario
* Salida
* Error
* Conservar

Un usuario o una aplicación cliente coloca primero el archivo o la carpeta en la carpeta de entrada. A continuación, la operación de servicio mueve el archivo a la carpeta de etapa para su procesamiento. Una vez que el servicio realiza la operación especificada, guarda el archivo modificado en la carpeta de salida. Los archivos de origen procesados correctamente se mueven a la carpeta de conservación y los archivos de procesamiento con errores se mueven a la carpeta con errores. Cuando el atributo `Preserve On Failure` de la carpeta vigilada está habilitado, los archivos de origen procesados con errores se mueven a la carpeta preserve. (Consulte [Configuración de los puntos finales de carpeta observados](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints)).

Puede realizar una copia de seguridad de las carpetas vigiladas haciendo una copia de seguridad del sistema de archivos.

>[!NOTE]
>
>Este backup es independiente del proceso de backup y recuperación de la base de datos o el almacenamiento de documento.

## Cómo funcionan las carpetas vigiladas {#how-watched-folders-work}

Este contenido describe el proceso de manipulación de archivos de carpetas vigiladas. Es importante comprender este proceso antes de desarrollar un plan de recuperación. En este ejemplo, se habilita el atributo `Preserve On Failure` para la carpeta observada. Los archivos se procesan en el orden en que llegan.

La siguiente tabla describe la manipulación de archivos de cinco archivos de ejemplo (archivo1, archivo2, archivo3, archivo4, archivo5) durante todo el proceso. En la tabla, el eje x representa el tiempo, como Tiempo 1 o T1, y el eje y representa las carpetas dentro de la jerarquía de carpetas observada, como Entrada.

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
   <td><p>file1, file2, file3, file4</p></td>
   <td><p>file2, file3, file4</p></td>
   <td><p>file3, file4</p></td>
   <td><p>archivo4</p></td>
   <td><p>vacío</p></td>
   <td><p>archivo5</p></td>
   <td><p>vacío</p></td>
  </tr>
  <tr>
   <td><p>Escenario</p></td>
   <td><p>vacío</p></td>
   <td><p>file1</p></td>
   <td><p>file2</p></td>
   <td><p>file3</p></td>
   <td><p>archivo4</p></td>
   <td><p>vacío</p></td>
   <td><p>archivo5</p></td>
  </tr>
  <tr>
   <td><p>Salida</p></td>
   <td><p>vacío</p></td>
   <td><p>vacío</p></td>
   <td><p>file1_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
  </tr>
  <tr>
   <td><p>Error</p></td>
   <td><p>vacío</p></td>
   <td><p>vacío</p></td>
   <td><p>vacío</p></td>
   <td><p>vacío</p></td>
   <td><p>file3_fail, file3 </p></td>
   <td><p>file3_fail, file3 </p></td>
   <td><p>file3_fail, file3 </p></td>
  </tr>
  <tr>
   <td><p>Conservar</p></td>
   <td><p>vacío</p></td>
   <td><p>vacío</p></td>
   <td><p>file1 </p></td>
   <td><p>file1, file2 </p></td>
   <td><p>file1, file2 </p></td>
   <td><p>file1, file2, file4 </p></td>
   <td><p>file1, file2, file4 </p></td>
  </tr>
 </tbody>
</table>

El siguiente texto describe la manipulación de archivos para cada vez:

**T1:** Los cuatro archivos de ejemplo se colocan en la carpeta de entrada.

**T2:** La operación de servicio mueve el archivo1 a la carpeta stage para su manipulación.

**T3:** La operación de servicio mueve el archivo2 a la carpeta stage para su manipulación. Coloca los resultados de file1 en la carpeta de salida y mueve file1 a la carpeta preserve.

**T4:** La operación de servicio coloca el archivo3 en la carpeta stage para su manipulación. Coloca los resultados de file2 en la carpeta de salida y coloca file2 en la carpeta preserve.

**T5:** La operación de servicio coloca el archivo4 en la carpeta stage para su manipulación. La manipulación de file3 falla y la operación de servicio la coloca en la carpeta de errores.

**T6:** La operación de servicio coloca el archivo5 en la carpeta de entrada. Coloca los resultados de file4 en la carpeta de salida y coloca file4 en la carpeta preserve.

**T7:** La operación de servicio coloca el archivo5 en la carpeta stage para su manipulación.

## Copia de seguridad de carpetas vigiladas {#backing-up-watched-folders}

Se recomienda realizar una copia de seguridad de todo el sistema de archivos de carpetas vigiladas en otro sistema de archivos.

## Restauración de carpetas vigiladas {#restoring-watched-folders}

En esta sección se describe cómo restaurar carpetas vigiladas. Las carpetas vigiladas suelen invocar procesos de corta duración que se completan en un minuto. En estos casos, la restauración de la carpeta vigilada con una copia de seguridad que se realiza cada hora no impedirá la pérdida de datos.

Por ejemplo, si se realiza una copia de seguridad en el momento T1 y el servidor falla en T7, el archivo1, el archivo2, el archivo3 y el archivo4 ya están manipulados. La restauración de la carpeta vigilada con una copia de seguridad realizada en T1 no impide la pérdida de datos.

Si se realizó una copia de seguridad más reciente, puede restaurar los archivos. Al restaurar los archivos, tenga en cuenta en qué carpeta de jerarquía de carpetas vigiladas reside el archivo actual:

**Etapa:** Los archivos de esta carpeta se procesan de nuevo una vez restaurada la carpeta vigilada.

**Entrada:** Los archivos de esta carpeta se procesan de nuevo una vez restaurada la carpeta vigilada.

**Resultado:** Los archivos de esta carpeta no se procesan.

**Salida:** los archivos de esta carpeta no se procesan.

**Conservar:** los archivos de esta carpeta no se procesan.

## Estrategias para minimizar la pérdida de datos {#strategies-to-minimize-data-loss}

Las siguientes estrategias pueden minimizar la pérdida de datos de carpeta de entrada y salida al restaurar una carpeta controlada:

* Realice copias de seguridad de las carpetas de salida y de error con frecuencia, como por hora, para evitar la pérdida de los archivos de resultado y de error.
* Realice una copia de seguridad de los archivos de entrada en una carpeta que no sea la carpeta vigilada. Esto garantiza la disponibilidad del archivo después de la recuperación en caso de que no pueda encontrar los archivos en la carpeta de salida o de error. Asegúrese de que el esquema de asignación de nombres de archivos sea coherente.

   Por ejemplo, si está guardando la salida con `%F.`*extensión*, el archivo de salida tendrá el mismo nombre que el archivo de entrada. Esto le ayuda a determinar qué archivos de entrada se manipulan y cuáles se deben reenviar. Si solo ve el archivo 1_out en la carpeta de resultados y no file2_out, file3_out y file4_out, debe volver a enviar el archivo 2, el archivo3 y el archivo4.

* Si la copia de seguridad de la carpeta vigilada disponible es anterior al tiempo necesario para procesar el trabajo, debe permitir que el sistema cree una nueva carpeta vigilada y coloque automáticamente los archivos en la carpeta de entrada.
* Si la copia de seguridad disponible más reciente no es lo suficientemente reciente, el tiempo de copia de seguridad es menor que el tiempo necesario para procesar los archivos y se restaura la carpeta vigilada, el archivo se manipuló en una de las siguientes etapas:

   * **Etapa 1:** En la carpeta de entrada
   * **Etapa 2:** Copiado en la carpeta de etapa, pero el proceso aún no se ha invocado
   * **Etapa 3:** Se copia en la carpeta de etapa y se invoca el proceso
   * **Etapa 4:** Manipulación en curso
   * **Etapa 5:** Resultados devueltos

   Si los archivos están en la fase 1, se manipularán. Si los archivos se encuentran en la fase 2 o 3, colóquelos en la carpeta de entrada para que la manipulación vuelva a producirse.

   >[!NOTE]
   >
   >Si la manipulación de un archivo se produce más de una vez, se evitará la pérdida de datos, pero los resultados pueden duplicarse.

## Conclusión {#conclusion}

Debido a la naturaleza dinámica y cambiante de una carpeta vigilada, la restauración de carpetas vigiladas debe realizarse con archivos de los que se haga una copia de seguridad en un día. Se recomienda realizar una copia de seguridad de los resultados, almacenar la carpeta de entrada en un servidor y realizar un seguimiento de los archivos de entrada para poder volver a enviar el trabajo en caso de error.
