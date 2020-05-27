---
title: Prácticas recomendadas para traducir recursos
description: Prácticas recomendadas para una gestión eficiente de los recursos a fin de sincronizar varias versiones traducidas y racionalizar los flujos de trabajo de traducción.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 1%

---


# Prácticas recomendadas para traducir recursos {#best-practices-for-translating-assets-efficiently}

Recursos Adobe Experience Manager admite flujos de trabajo multilingües para traducir binarios, metadatos y etiquetas para recursos digitales en varias configuraciones regionales y para administrar los recursos traducidos. Para obtener más información, consulte Recursos [multilingües](multilingual-assets.md).

Para una administración eficiente de los recursos a fin de garantizar que las distintas versiones traducidas permanezcan sincronizadas, cree copias [de](preparing-assets-for-translation.md) idioma de los recursos antes de ejecutar flujos de trabajo de traducción.

Una copia de idioma de un recurso o un grupo de recursos es un elemento secundario de idioma (o una versión de los recursos en un idioma de dominio) con una jerarquía de contenido similar.

Cada copia de idioma es un recurso independiente. Por lo tanto, la traducción de recursos en varias configuraciones regionales puede aumentar drásticamente el tamaño del repositorio de CRX. Por ejemplo, la traducción de recursos con un tamaño combinado de 10 GB a dos idiomas puede aumentar el tamaño del repositorio en aproximadamente 20 GB (10 GB para cada idioma).

Los binarios de recursos ocupan un espacio de almacenamiento mucho mayor en comparación con los metadatos y las etiquetas. Por lo tanto, si la traducción de metadatos y etiquetas sólo sirve a su propósito, omita traducir los binarios. Puede conservar la copia original de los binarios en el repositorio para asociarla con metadatos y etiquetas traducidas a diferentes configuraciones regionales. El mantenimiento de una única copia de los binarios, en lugar de múltiples versiones traducidas, minimiza el impacto en el tamaño del repositorio.

El almacén de datos de archivos y el almacén de datos de Amazon S3 proporcionan una infraestructura de almacenamiento que se adapta mejor a estos escenarios. Estos repositorios de almacenamiento almacenan una única copia de los binarios de recursos (incluidas las representaciones) que pueden compartirse con metadatos y etiquetas en varias configuraciones regionales. Por lo tanto, la creación de copias del idioma del recurso y la traducción de metadatos y etiquetas no afectan al tamaño del repositorio.

También puede realizar algunos cambios en la configuración de un par de flujos de trabajo y en el marco de integración de traducción para racionalizar aún más el proceso.

1. Realice una de las acciones siguientes:

   * [Configuración del almacén de datos de archivos](/help/sites-deploying/data-store-config.md)
   * [Configurar el almacén de datos de Amazon S3](/help/sites-deploying/data-store-config.md)

1. Deshabilite el flujo de trabajo [DAM MetaData Write](/help/sites-administering/workflow-offloader.md#disable-offloading) .

   Como indica el nombre, el flujo de trabajo de reescritura [!UICONTROL de metadatos] DAM vuelve a escribir los metadatos en el archivo binario. Como los metadatos cambian después de la traducción, volver a escribirlos en el archivo binario genera un binario diferente para una copia de idioma.

   >[!NOTE]
   >
   >Al desactivar el flujo de trabajo de [!UICONTROL reescritura de metadatos] DAM, se desactiva la reescritura de metadatos XMP en los binarios de recursos. En consecuencia, los cambios futuros en los metadatos ya no se guardan dentro de los recursos. Evalúe las consecuencias antes de desactivar este flujo de trabajo.

1. Habilite el flujo de trabajo [!UICONTROL Establecer fecha] de última modificación.

   El flujo de trabajo de [!UICONTROL reescritura de metadatos] DAM configura la fecha de la última modificación de un recurso. Como este flujo de trabajo se desactiva en el paso 2, Recursos ya no puede mantener actualizada la última fecha de modificación de los recursos. Por lo tanto, habilite el flujo de trabajo *Establecer fecha* de última modificación para garantizar que las últimas fechas de modificación de los recursos estén actualizadas. Los recursos con fechas de última modificación desactualizadas pueden provocar errores.

1. [Configure el marco](/help/sites-administering/tc-tic.md) de integración de traducción para dejar de traducir los binarios de recursos. Anule la selección de la opción **[!UICONTROL Traducir recursos]** de la ficha Recursos para detener la traducción de los binarios de recursos.
1. Traduzca metadatos y etiquetas de recursos mediante flujos de trabajo [de recursos](multilingual-assets.md)multilingües.
