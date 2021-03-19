---
title: Prácticas recomendadas para traducir recursos
description: Prácticas recomendadas para una administración eficiente de los recursos con el fin de sincronizar varias versiones traducidas y optimizar los flujos de trabajo de traducción.
contentOwner: AG
role: Administrador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 1%

---


# Prácticas recomendadas para traducir recursos {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] admite flujos de trabajo multilingües para traducir binarios, metadatos y etiquetas para recursos digitales a varias configuraciones regionales y administrar los recursos traducidos. Para obtener más información, consulte [Recursos multilingües](multilingual-assets.md).

Para una administración eficiente de los recursos y garantizar que las distintas versiones traducidas permanezcan sincronizadas, cree [copias de idioma](preparing-assets-for-translation.md) de los recursos antes de ejecutar los flujos de trabajo de traducción.

Una copia de idioma de un recurso o de un grupo de recursos es un elemento del mismo nivel de idioma (o una versión de los recursos en un idioma distinto) con una jerarquía de contenido similar.

Cada copia de idioma es un recurso independiente. Por lo tanto, la traducción de recursos en varias configuraciones regionales puede aumentar drásticamente el tamaño del repositorio CRX. Por ejemplo, la traducción de recursos con un tamaño combinado de 10 GB a dos idiomas puede aumentar el tamaño del repositorio en aproximadamente 20 GB (10 GB por cada idioma).

Los binarios de recursos ocupan un espacio de almacenamiento mucho mayor comparado con los metadatos y las etiquetas. Por lo tanto, si la traducción de metadatos y etiquetas solo cumple con su propósito, omita traducir los binarios. Puede conservar la copia original de los binarios en el repositorio para asociarla con metadatos y etiquetas traducidos a diferentes configuraciones regionales. El mantenimiento de una sola copia de binarios, en lugar de varias versiones traducidas, minimiza el impacto en el tamaño del repositorio.

El almacén de datos de archivos y el almacén de datos Amazon S3 proporcionan una infraestructura de almacenamiento que es más adecuada para estos escenarios. Estos repositorios de almacenamiento almacenan una sola copia de los binarios de recursos (incluidas las representaciones) que pueden compartirse mediante metadatos y etiquetas en varias configuraciones regionales. Por lo tanto, la creación de copias de idiomas de recursos y la traducción de metadatos y etiquetas no afectan al tamaño del repositorio.

También puede realizar algunos cambios en la configuración de un par de flujos de trabajo y del marco de integración de la traducción para racionalizar aún más el proceso.

1. Realice una de las acciones siguientes:

   * [Configuración del almacén de datos de archivos](/help/sites-deploying/data-store-config.md)
   * [Configuración del almacén de datos de Amazon S3](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. Habilite el flujo de trabajo [!UICONTROL Set last modified date] .

   El flujo de trabajo [!UICONTROL DAM MetaData Writeback] configura la última fecha de modificación de un recurso. Dado que deshabilita este flujo de trabajo en el paso 2, [!DNL Assets] ya no puede mantener actualizada la última fecha de modificación de los recursos. Por lo tanto, habilite el flujo de trabajo *Set last modified date* para garantizar que las fechas de las últimas modificaciones de los recursos estén actualizadas. Los recursos con fechas de última modificación obsoletas pueden causar errores.

1. [Configure el ](/help/sites-administering/tc-tic.md) marco de integración de traducción para detener la traducción de binarios de recursos. Desmarque la opción **[!UICONTROL Translate Assets]** en la pestaña [!UICONTROL Assets] para detener la traducción de los binarios de Asset.
1. Traduzca metadatos/etiquetas de recursos mediante [Flujos de trabajo de recursos multilingües](multilingual-assets.md).
