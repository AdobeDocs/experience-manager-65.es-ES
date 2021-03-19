---
title: Integración de datos de AEM Forms
seo-title: Integración de datos de AEM Forms
description: La integración de datos permite integrar AEM Forms con orígenes de datos dispares y crear un modelo de datos de formulario para crear y trabajar con formularios adaptables y comunicaciones interactivas.
seo-description: La integración de datos permite integrar AEM Forms con orígenes de datos dispares y crear un modelo de datos de formulario para crear y trabajar con formularios adaptables y comunicaciones interactivas.
uuid: 01df045e-1b26-437c-9674-fd223ecd5097
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: e397c6ce-d73f-4183-8445-1897a8906960
docset: aem65
feature: Modelo de datos de formulario
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# [!DNL AEM Forms] Integración de datos  {#aem-forms-data-integration}

![](do-not-localize/data-integeration.png)

Las infraestructuras empresariales incluyen sistemas back-end o fuentes de datos dispares, como bases de datos, servicios web, servicios REST, servicios OData y soluciones CRM. En conjunto, crean un sistema de información que sirve datos a las aplicaciones empresariales para realizar el trabajo diario. Por otro lado, las aplicaciones capturan datos y los envían de vuelta para actualizar las fuentes de datos.

[!DNL AEM Forms] las aplicaciones como formularios adaptables y comunicaciones interactivas requieren la integración con orígenes de datos para recuperar datos de clientes mientras se procesan formularios y se crean comunicaciones interactivas. Hay casos de uso en los que se recuperan datos de fuentes de datos basadas en entradas del usuario en formularios adaptables. Además, los datos de formulario adaptable enviados se pueden volver a escribir para actualizar las fuentes de datos correspondientes.

Si bien un sistema modular y distribuido tiene sus propias ventajas, el desafío reside en integrar y crear asociaciones de datos entre fuentes de datos. La integración de datos es la clave de una infraestructura empresarial funcional y eficiente con fuentes de datos dispares conectadas a aplicaciones para el intercambio de datos del negocio.

## Información general sobre la integración de datos {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] La integración de datos permite configurar y conectar diferentes fuentes de datos con  [!DNL AEM Forms]. Proporciona una interfaz de usuario intuitiva para crear un esquema de representación de datos unificado de entidades y servicios empresariales a través de fuentes de datos conectadas. La representación unificada se conoce como modelo de datos de formulario, una extensión del esquema JSON. Las entidades de un modelo de datos de formulario se denominan objetos del modelo de datos. Un modelo de datos de formulario le permite:

* Acceda a objetos, propiedades y servicios del modelo de datos desde fuentes de datos conectadas.
* Creación de objetos y propiedades personalizadas del modelo de datos
* Cree asociaciones entre objetos de modelo de datos dentro de y entre orígenes de datos.
* Invoque los servicios de objeto del modelo de datos para consultar o escribir datos desde y hacia orígenes de datos.

Una vez creado un modelo de datos de formulario, puede utilizarlo en diversos flujos de trabajo de comunicaciones interactivos y de formularios adaptables, como:

* Creación de formularios adaptables y comunicaciones interactivas basadas en el modelo de datos de formulario
* Rellene previamente formularios adaptables y comunicaciones interactivas desde fuentes de datos configuradas
* Invocar servicios u operaciones de fuentes de datos mediante reglas de formulario adaptables
* Escribir datos de formulario adaptable enviados en fuentes de datos

## Introducción a la integración de datos {#get-started-with-data-integration}

El primer paso para implementar la integración de datos es identificar y configurar las fuentes de datos que almacenan información que desea aprovechar en los formularios adaptables y en los casos de uso de comunicaciones interactivas. A continuación, se crea un modelo de datos de formulario que utiliza objetos, propiedades y servicios del modelo de datos de uno o varios orígenes de datos. Se pueden crear formularios adaptables y comunicaciones interactivas basadas en un modelo de datos de formulario en el que los campos de formulario adaptables o los marcadores de posición de comunicaciones interactivas están enlazados a las respectivas propiedades del origen de datos.

[!DNL AEM Forms] también permite crear un modelo de datos de formulario independiente de los orígenes de datos y asociar o enlazar objetos y propiedades del modelo de datos en el modelo de datos de formulario con el origen de datos más adelante. Elimina las dependencias de los orígenes de datos mientras trabaja en un modelo de datos de formulario.

Revise lo siguiente para comenzar, comprender e implementar la integración de datos.

* [Configuración de fuentes de datos](../../forms/using/configure-data-sources.md)
* [Crear modelo de datos de formulario](../../forms/using/create-form-data-models.md)
* [Trabajo con el modelo de datos de formulario](../../forms/using/work-with-form-data-model.md)
* [Uso del modelo de datos de formulario](../../forms/using/using-form-data-model.md)

