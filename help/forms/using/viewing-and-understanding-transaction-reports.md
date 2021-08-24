---
title: Visualización y comprensión de informes de transacciones
seo-title: Visualización y comprensión de informes de transacciones
description: Utilice los informes de transacciones para tomar una decisión informada sobre el uso del producto y las inversiones de reequilibrio en hardware y software.
seo-description: Utilice los informes de transacciones para tomar una decisión informada sobre el uso del producto y las inversiones de reequilibrio en hardware y software.
uuid: 56d9f01d-4778-47c9-bbb2-6650a73a3f59
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c04c488b-73f3-49ba-9e89-f97497965757
docset: aem65
exl-id: 3c7cbe1f-ac81-4df9-96b2-662cbc5f2075
source-git-commit: 75e1697c301dca3a649833a45caa1753fdc81514
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 0%

---

# Visualización y comprensión de informes de transacciones{#viewing-and-understanding-transaction-reports}

Los informes de transacciones permiten capturar y rastrear el número de formularios enviados, documentos procesados y documentos procesados. El objetivo detrás del seguimiento de estas transacciones es tomar una decisión informada sobre el uso del producto y reequilibrar las inversiones en hardware y software. Para obtener más información, consulte [Información general sobre los informes de transacciones de AEM Forms](../../forms/using/transaction-reports-overview.md).

## Configuración de informes de transacciones  {#setting-up-transaction-reports}

La función de informes de transacciones está disponible como parte del paquete de complementos de formularios AEM. Para obtener información sobre la instalación del paquete de complementos en todas las instancias de autor y publicación, consulte [Instalación y configuración de AEM formularios](/help/forms/using/installing-configuring-aem-forms-osgi.md). Una vez que tenga instalado el paquete de complementos de AEM forms, haga lo siguiente:

* Habilitar la replicación inversa en todas las instancias de publicación
* Habilitar informes de transacciones
* Proporcionar derechos para ver un informe de transacciones
* (Opcional) Configure el período de vaciado de la transacción y las bandejas de salida [](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* Los informes de transacciones de AEM Forms no admiten topologías que contengan solo instancias de publicación.
>* Antes de usar informes de transacciones, asegúrese de que la replicación inversa esté habilitada para todas las instancias de publicación.
>* Los datos de transacción se replican de forma inversa de una instancia de publicación a la instancia de autor o procesamiento correspondiente. El autor o la instancia de procesamiento no pueden replicar más datos en otra instancia.

>



### Habilitar la replicación inversa en todas las instancias de publicación {#enable-reverse-replication-on-all-the-publish-instances}

Los informes de transacciones utilizan la replicación inversa para consolidar el recuento de transacciones desde instancias de publicación hasta instancias de autor. Configure la replicación inversa en todas las instancias de publicación. Para obtener instrucciones detalladas para configurar la replicación inversa, consulte [replicación](/help/sites-deploying/replication.md).

### Habilitar informes de transacciones {#enable-transaction-reports}

Los informes de transacciones están desactivados de forma predeterminada. Puede habilitar los informes desde AEM consola web. para activar informes de transacciones en un entorno de AEM Forms, realice los siguientes pasos en todas las instancias de autor y publicación:

1. Inicie sesión en una instancia de AEM como administrador. Vaya a **Herramientas** > **Operaciones** > **Consola Web**.
1. Busque y abra el servicio **Forms Transaction Reporting**.
1. Active la casilla Registrar Transacciones. Haga clic en **Guardar**.

   Repita los pasos del 1 al 3 en todas las instancias de autor y publicación.

### Proporcionar derechos para ver un informe de transacciones {#provide-rights-to-view-a-transaction-report}

Solo los miembros del grupo fd-administrator pueden ver los informes de transacción. Para permitir que un usuario vea informes de transacciones, haga que los usuarios sean miembros del grupo fd-administrator. Para obtener instrucciones sobre cómo hacer que un usuario sea miembro de un grupo de AEM, consulte [Administración de derechos de usuario, grupo y acceso](/help/sites-administering/user-group-ac-admin.md).

### (Opcional) Configurar el período de vaciado de la transacción y las bandejas de salida {#optional-configure-transaction-flush-period-and-outboxes}

Las transacciones se almacenan en la memoria caché antes de almacenarse en el repositorio. Se sigue el proceso para garantizar que no haya escrituras frecuentes en el repositorio. De forma predeterminada, el periodo de almacenamiento en caché (Período de vaciado de la transacción) está establecido en 60 segundos. Puede cambiar el periodo predeterminado para adaptarlo a su entorno. Realice los siguientes pasos para cambiar el período de almacenamiento en caché predeterminado:

1. Inicie sesión en instancias de autor como administrador. Vaya a **Herramientas** > **Operaciones** > **Consola Web**.
1. Busque y abra el servicio **Forms Transaction Repository Storage Provider**.
1. Especifique el número de segundos en el campo **Período de vaciado de transacción**. Haga clic en **Guardar**.

La replicación inversa copia los datos de transacción en la bandeja de salida predeterminada de las instancias de autor. Puede colocar los datos de transacción en una bandeja de salida personalizada. Siga estos pasos para especificar una bandeja de salida personalizada:

1. Inicie sesión en instancias de autor como administrador. Vaya a **Herramientas** > **Operaciones** > **Consola Web**.
1. Busque y abra el servicio **Forms Transaction Repository Storage Provider**.
1. Especifique el nombre de la bandeja de salida personalizada en el campo **Bandeja de salida**. Haga clic en **Guardar**. Se crea una bandeja de salida con el nombre especificado en todas las instancias de autor.

## Visualización del informe de transacciones {#viewing-the-transaction-report}

Puede ver informes de transacciones en instancias de autor o publicación. El informe de transacción de la instancia de autor proporciona una suma agregada de todas las transacciones que se realizan en las instancias de autor y publicación configuradas. El informe de transacciones de la instancia de publicación proporciona un recuento de transacciones que se realizan solamente en la instancia de publicación subyacente. Siga estos pasos para ver el informe:

1. Inicie sesión en el servidor de AEM Forms en `https://[hostname]:'port'`.
1. Vaya a **Herramientas** > **Forms****Ver informe de transacciones**.

## Explicación del informe {#understanding-the-report}

AEM Forms muestra los informes de transacciones desde la fecha configurada, como se muestra en el siguiente informe de resumen:

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* Utilice las opciones **Reset the date to today** para restablecer los registros de transacciones. Cuando restablece la fecha a hoy, se pierden todos los registros de transacción anteriores. Cuando restablece la fecha en una instancia de autor, el cambio no afecta a los informes de transacción en las instancias de publicación y, a la inversa.
* Utilice **Mostrar transacciones de solo instancias de publicación** para ver todas las transacciones que se produjeron únicamente en la instancia de publicación o granja de publicación configurada.
* Utilice las categorías: **Documentos procesados**, **Documentos procesados** y **Forms enviados** para ver las transacciones correspondientes. Para ver el tipo de transacciones contabilizadas en estas categorías, consulte [API de informes de transacciones facturables](../../forms/using/transaction-reports-billable-apis.md).

## Ver registros de informes de transacciones {#view-transaction-reporting-logs}

Los informes de transacciones colocan toda la información mostrada en el informe y cierta información adicional en los registros. La información proporcionada en los registros es útil para los usuarios avanzados. Por ejemplo, los registros dividen las transacciones en varias categorías granulares en comparación con tres categorías consolidadas mostradas en el informe. Los registros están disponibles en el archivo `error.log` en el directorio `/crx-repository/logs/`. Los registros están disponibles aunque no habilite los informes de transacción desde AEM consola web.

## Artículos relacionados {#related-articles}

* [Información general sobre los informes de transacciones](../../forms/using/transaction-reports-overview.md)
* [API facturables de informes de transacciones](../../forms/using/transaction-reports-billable-apis.md)
* [Registrar una transacción para implementaciones personalizadas](/help/forms/using/record-transaction-custom-implementation.md)
