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
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Integración de datos de AEM Forms{#aem-forms-data-integration}

![](do-not-localize/data-integeration.png)

Las infraestructuras empresariales incluyen sistemas de back-end o fuentes de datos dispares, como bases de datos, servicios Web, servicios REST, servicios OData y soluciones CRM. En conjunto, crean un sistema de información que proporciona datos a las aplicaciones empresariales para realizar actividades cotidianas. Por otra parte, las aplicaciones capturan datos y los envían de vuelta para actualizar las fuentes de datos.

Las aplicaciones de AEM Forms, como los formularios adaptables y las comunicaciones interactivas, requieren la integración con orígenes de datos para recuperar datos de clientes mientras procesan formularios y crean comunicaciones interactivas. Hay casos de uso en los que los datos se recuperan de fuentes de datos en función de las entradas del usuario en formularios adaptables. Además, los datos de formulario adaptable enviados se pueden volver a escribir para actualizar las fuentes de datos respectivas.

Si bien un sistema modular y distribuido tiene sus propios beneficios, el desafío reside en integrar y crear asociaciones de datos entre fuentes de datos. La integración de datos es la clave de una infraestructura empresarial funcional y eficiente con fuentes de datos dispares conectadas a las aplicaciones para el intercambio de datos comerciales.

## Información general sobre la integración de datos {#data-integration-overview}

![aem-forms-data-integeration](assets/aem-forms-data-integeration.png)

La integración de datos de AEM Forms permite configurar y conectar orígenes de datos dispares con AEM Forms. Proporciona una interfaz de usuario intuitiva para crear un esquema de representación de datos unificado de entidades comerciales y servicios entre fuentes de datos conectadas. La representación unificada se conoce como modelo de datos de formulario, una extensión del esquema JSON. Las entidades de un modelo de datos de formulario se denominan objetos del modelo de datos. Un modelo de datos de formulario permite:

* Acceda a objetos, propiedades y servicios del modelo de datos desde orígenes de datos conectados.
* Creación de propiedades y objetos del modelo de datos personalizado
* Cree asociaciones entre objetos de modelo de datos dentro de y entre orígenes de datos.
* Invocar los servicios de objetos del modelo de datos para consultar o escribir datos en orígenes de datos y desde ellos.

Una vez creado el modelo de datos de formulario, puede utilizarlo en varios flujos de trabajo de comunicaciones interactivas y formularios adaptables, como:

* Crear formularios adaptables y comunicaciones interactivas basadas en el modelo de datos de formulario
* Rellenar formularios adaptables y comunicaciones interactivas desde orígenes de datos configurados
* Invocar servicios u operaciones de origen de datos mediante reglas de formulario adaptables
* Escribir datos de formularios adaptables enviados en orígenes de datos

## Introducción a la integración de datos {#get-started-with-data-integration}

El primer paso para implementar la integración de datos es identificar y configurar las fuentes de datos que almacenan la información que desea aprovechar en formularios adaptables y casos de uso de comunicaciones interactivas. A continuación, se crea un modelo de datos de formulario que utiliza objetos, propiedades y servicios del modelo de datos de uno o varios orígenes de datos. Puede crear formularios adaptables y comunicaciones interactivas basadas en un modelo de datos de formulario en el que los campos de formulario adaptables o los marcadores de posición de las comunicaciones interactivas estén enlazados a las propiedades de origen de datos correspondientes.

AEM Forms también permite crear un modelo de datos de formulario independiente de los orígenes de datos y asociar o enlazar objetos y propiedades del modelo de datos en el modelo de datos de formulario con el origen de datos más adelante. Elimina cualquier dependencia de los orígenes de datos mientras trabaja en un modelo de datos de formulario.

Revise lo siguiente para empezar, comprender e implementar la integración de datos.

* [Configurar orígenes de datos](../../forms/using/configure-data-sources.md)
* [Crear modelo de datos de formulario](../../forms/using/create-form-data-models.md)
* [Trabajar con el modelo de datos de formulario](../../forms/using/work-with-form-data-model.md)
* [Usar modelo de datos de formulario](../../forms/using/using-form-data-model.md)

