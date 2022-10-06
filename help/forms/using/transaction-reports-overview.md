---
title: Información general sobre los informes de transacciones
seo-title: Transaction Reports Overview
description: Mantenga un recuento de todos los formularios enviados, la comunicación interactiva representada, los documentos convertidos en un formato a otro, y más
seo-description: Keep a count of all the forms submitted, interactive communication rendered, Documents converted to one format to another, and more
uuid: 2c3dc1f3-5bbf-4aab-aa84-7aef5aabadf6
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b2c09e6b-a1d8-4b30-af2c-988442a3a986
docset: aem65
exl-id: bb812614-f4d8-4f57-bea2-8f7d31457039
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# Información general sobre los informes de transacciones{#transaction-reports-overview}

## Introducción {#introduction}

Los informes de transacciones de AEM Forms permiten mantener un recuento de todas las transacciones realizadas desde una fecha especificada en la implementación de AEM Forms. El objetivo es proporcionar información sobre el uso del producto y ayudar a las partes interesadas del negocio a comprender sus volúmenes de procesamiento digital. Algunos ejemplos de transacciones son:

* Envío de un formulario adaptable, un formulario HTML5 o un conjunto de formularios
* Representación de una impresión o una versión web de una comunicación interactiva
* Conversión de un documento de un formato de archivo a otro

Para obtener más información sobre lo que se considera una transacción, consulte [API facturables](../../forms/using/transaction-reports-billable-apis.md).

El registro de transacciones está desactivado de forma predeterminada. Puede [activar registro de transacciones](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) desde AEM consola web. Puede ver informes de transacciones sobre instancias de autor, procesamiento o publicación. Vea informes de transacciones sobre instancias de autor o procesamiento para una suma agregada de todas las transacciones. Vea informes de transacciones en las instancias de publicación para un recuento de todas las transacciones que se realizan solamente en esa instancia de publicación desde la que se ejecuta el informe.

No cree contenido (cree formularios adaptables, comunicación interactiva, temas y otras actividades de creación) ni procese documentos (utilice flujos de trabajo, servicios de documentos y otras actividades de procesamiento) en la misma instancia de AEM. Mantenga la grabación de transacciones deshabilitada para los servidores de AEM Forms utilizados para crear contenido. Mantenga la grabación de transacciones habilitada para los servidores de AEM Forms utilizados para procesar documentos.

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

Una transacción permanece en el búfer durante un período especificado (tiempo de búfer de vaciado + tiempo de replicación inversa). De forma predeterminada, el recuento de transacciones tarda aproximadamente 90 segundos en reflejarse en el informe de transacciones.

Las acciones como enviar un formulario de PDF, usar la interfaz de usuario del agente para obtener una vista previa de una comunicación interactiva o usar métodos de envío de formularios no estándar no se contabilizan como transacciones. AEM Forms proporciona una API para registrar estas transacciones. Llame a la API desde las implementaciones personalizadas para registrar una transacción.

## Topología admitida {#supported-topology}

Los informes de transacciones solo están disponibles en AEM Forms en el entorno OSGi. Admite autor-publicación, autor-procesamiento-publicación y solo procesa topologías. Por ejemplo, topologías, consulte [Arquitectura y topologías de implementación para AEM Forms](../../forms/using/transaction-reports-overview.md).

El recuento de transacciones se replica de forma inversa de las instancias de publicación a las instancias de autor o procesamiento. A continuación se muestra una topología indicativa de creación-publicación:

![simple-author-publish-topología](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>Los informes de transacciones de AEM Forms no admiten topologías que contengan solo instancias de publicación.

### Directrices para el uso de informes de transacciones {#guidelines-for-using-transaction-reports}

* Desactive los informes de transacciones en todas las instancias de autor, ya que los informes de instancias de autor incluyen transacciones registradas durante las actividades de creación.
* Active la variable **Mostrar transacciones sólo de publicación** en la instancia de autor para ver las transacciones acumulativas de todas las instancias de publicación. También puede ver informes de transacciones en cada instancia de publicación para transacciones reales solo en esa instancia de publicación en particular.
* No utilice instancias de autor para ejecutar flujos de trabajo y procesar documentos.
* Antes de usar los informes de transacciones, si tiene una toplogía con servidores de publicación, asegúrese de que la replicación inversa esté habilitada para todas las instancias de publicación.
* Los datos de transacción se replican de forma inversa de una instancia de publicación a la instancia de autor o procesamiento correspondiente. El autor o la instancia de procesamiento no pueden replicar más datos en otra instancia. Por ejemplo, si tiene topología de publicación-procesamiento de autor, los datos de transacción agregados se replican solo en la instancia de procesamiento.

## Artículos relacionados {#related-articles}

* [Visualización y comprensión de informes de transacciones](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [API facturables de informes de transacciones](../../forms/using/transaction-reports-billable-apis.md)
* [Registrar una transacción para implementaciones personalizadas](/help/forms/using/record-transaction-custom-implementation.md)
