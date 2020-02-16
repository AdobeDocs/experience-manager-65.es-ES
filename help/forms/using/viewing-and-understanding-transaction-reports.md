---
title: Visualización y comprensión de los informes de transacciones
seo-title: Visualización y comprensión de los informes de transacciones
description: Utilice los informes de transacciones para tomar una decisión informada sobre el uso del producto y reequilibrar las inversiones en hardware y software.
seo-description: Utilice los informes de transacciones para tomar una decisión informada sobre el uso del producto y reequilibrar las inversiones en hardware y software.
uuid: 56d9f01d-4778-47c9-bbb2-6650a73a3f59
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c04c488b-73f3-49ba-9e89-f97497965757
docset: aem65
translation-type: tm+mt
source-git-commit: 8f90dc4865126d52e04effc9197ef7145b1a167e

---


# Visualización y comprensión de los informes de transacciones{#viewing-and-understanding-transaction-reports}

Los informes de transacciones permiten capturar y rastrear el número de formularios enviados, documentos procesados y documentos procesados. El objetivo detrás del seguimiento de estas transacciones es tomar una decisión informada sobre el uso del producto y reequilibrar las inversiones en hardware y software. Para obtener más información, consulte Información general sobre los informes de transacciones de [AEM Forms](../../forms/using/transaction-reports-overview.md).

## Configuración de informes de transacciones {#setting-up-transaction-reports}

La función Informes de transacciones está disponible como parte del paquete complementario de formularios AEM. Para obtener información sobre la instalación del paquete de complementos en todas las instancias de creación y publicación, consulte [Instalación y configuración de formularios](/help/forms/using/installing-configuring-aem-forms-osgi.md)AEM. Una vez que tenga instalado el paquete de complementos de formularios AEM, haga lo siguiente:

* Habilitar la replicación inversa en todas las instancias de publicación
* Habilitar informes de transacciones
* Proporcionar derechos para ver un informe de transacciones
* (Opcional) Configuración del período de vaciado de transacciones y las bandejas de salida [](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* Los informes de transacciones de AEM Forms no admiten topologías que solo contienen instancias de publicación.
>* Antes de utilizar los informes de transacciones, asegúrese de que la replicación inversa está habilitada para todas las instancias de publicación.
>* Los datos de transacción se replican de forma inversa desde una instancia de publicación a la instancia de creación o procesamiento correspondiente. El autor o la instancia de procesamiento no pueden replicar más datos en otra instancia.
>



### Habilitar la replicación inversa en todas las instancias de publicación {#enable-reverse-replication-on-all-the-publish-instances}

Los informes de transacciones utilizan la replicación inversa para consolidar el recuento de transacciones desde instancias de publicación hasta instancias de creación. Configure la replicación inversa en todas las instancias de publicación. Para obtener instrucciones detalladas para configurar la replicación inversa, consulte [Replicación](/help/sites-deploying/replication.md).

### Habilitar informes de transacciones {#enable-transaction-reports}

Los informes de transacciones están deshabilitados de forma predeterminada. Puede activar los informes desde la consola web de AEM. para activar informes de transacciones en un entorno de AEM Forms, realice los siguientes pasos en todas las instancias de creación y publicación:

1. Inicie sesión en una instancia de AEM como administrador. Vaya a **Herramientas** > **Operaciones** > Consola **** Web.
1. Busque y abra el servicio **Forms Transaction Reporting** .
1. Active la casilla de verificación Registrar transacciones. Haga clic en **Guardar**.

   Repita los pasos del 1 al 3 en todas las instancias de creación y publicación.

### Proporcionar derechos para ver un informe de transacciones {#provide-rights-to-view-a-transaction-report}

Sólo los miembros del grupo fd-admin pueden ver los informes de transacciones. Para permitir que un usuario vea los informes de transacciones, haga que los usuarios sean miembros del grupo fd-admin. Para obtener instrucciones sobre cómo convertir a un usuario en miembro de un grupo de AEM, consulte Administración [de derechos de usuario, grupo y acceso](/help/sites-administering/user-group-ac-admin.md).

### (Opcional) Configuración del período de vaciado de transacciones y las bandejas de salida {#optional-configure-transaction-flush-period-and-outboxes}

Las transacciones se almacenan en la memoria caché antes de almacenarse en el repositorio. De forma predeterminada, el período de almacenamiento en caché (Período de vaciado de transacción) se establece en 60 segundos. Realice los siguientes pasos para cambiar el período de almacenamiento en caché predeterminado:

1. Inicie sesión como administrador para crear instancias. Vaya a **Herramientas** > **Operaciones** > Consola **** Web.
1. Busque y abra el servicio Proveedor **de almacenamiento del repositorio de transacciones de** Forms.
1. Especifique el número de segundos en el campo Período **de vaciado de** transacción. Haga clic en **Guardar**.

La replicación inversa copia los datos de transacción en la bandeja de salida predeterminada de las instancias de creación. Puede colocar los datos de transacción en una bandeja de salida personalizada. Realice los siguientes pasos para especificar una bandeja de salida personalizada:

1. Inicie sesión como administrador para crear instancias. Vaya a **Herramientas** > **Operaciones** > Consola **** Web.
1. Busque y abra el servicio Proveedor **de almacenamiento del repositorio de transacciones de** Forms.
1. Especifique el nombre de la bandeja de salida personalizada en el campo **Bandeja de salida** . Haga clic en **Guardar.** Se crea una bandeja de salida con el nombre especificado en todas las instancias de creación.

## Visualización del informe de transacciones {#viewing-the-transaction-report}

Puede ver los informes de transacción en instancias de autor o publicación. El informe de transacciones de la instancia de autor proporciona una suma agregada de todas las transacciones que se realizan en las instancias de creación y publicación configuradas. El informe de transacciones de la instancia de publicación proporciona un recuento de las transacciones que solo se producen en la instancia de publicación subyacente. Realice los siguientes pasos para ver el informe:

1. Inicie sesión en el servidor de AEM Forms en `https://[hostname]:[port]`.
1. Vaya a **Herramientas** > **Formularios**>**Ver informe** de transacciones.

## Explicación del informe {#understanding-the-report}

AEM Forms muestra los informes de transacciones desde la fecha configurada, como se muestra en el informe de resumen siguiente:

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* Utilice las opciones **Restablecer la fecha a hoy** para restablecer los registros de transacciones. Cuando restablece la fecha a hoy, se pierden todos los registros de transacciones anteriores. Cuando se restablece la fecha en una instancia de autor, el cambio no afecta a los informes de transacción en las instancias de publicación y, por el contrario, no afecta a los informes de transacción.
* Utilice **Mostrar transacciones de solo instancias** de publicación para ver todas las transacciones que se produjeron únicamente en la instancia de publicación o en el conjunto de servidores de publicación configurados.
* Utilice las categorías: **Documento procesado**, **Documentos procesados** y **Formularios enviados** para ver las transacciones correspondientes. Para el tipo de transacciones contabilizadas en estas categorías, consulte API de informes de transacciones [facturables](../../forms/using/transaction-reports-billable-apis.md).

## Ver registros de informes de transacciones {#view-transaction-reporting-logs}

Los informes de transacciones colocan toda la información mostrada en el informe y cierta información adicional en los registros. La información proporcionada en los registros resulta útil para los usuarios avanzados. Por ejemplo: los registros dividen las transacciones en varias categorías granulares en comparación con tres categorías consolidadas que se muestran en el informe. Los registros se encuentran en /crx-quickstart/logs/aem-forms-transaction.log.

## Artículos relacionados {#related-articles}

* [Información general sobre los informes de transacciones](../../forms/using/transaction-reports-overview.md)
* [Informes de transacciones API facturables](../../forms/using/transaction-reports-billable-apis.md)
* [Registrar una transacción para implementaciones personalizadas](/help/forms/using/record-transaction-custom-implementation.md)

