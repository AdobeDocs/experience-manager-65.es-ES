---
title: Retención de datos en AEM Forms
description: Descubra cómo Adobe Experience Manager (AEM) Forms, de forma predeterminada, actúa como servidor de paso a través y no almacena datos de usuarios finales de formularios, lo que admite la privacidad de datos.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin, User
solution: Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ca1448119778a2bcfeca7189aab5b360d992d99d
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 1%
---
# Retención de datos en AEM Forms {#data-retention-in-aem-forms}

¿AEM Forms almacena datos de formulario? De forma predeterminada, no. Adobe Experience Manager (AEM) Forms actúa como servidor de paso a través para los datos capturados a través de Forms adaptable y no almacena datos del usuario final en el repositorio de AEM. En su lugar, el servidor pasa los datos enviados al destino que posee y configura. Este comportamiento predeterminado le ayuda a cumplir los objetivos de conformidad y privacidad de datos, y se aplica tanto a AEM Forms en OSGi como a AEM Forms en JEE.

Como AEM Forms es una plataforma ampliable, puede personalizar AEM para cambiar este comportamiento predeterminado. Si la personalización almacena los datos enviados a través de un formulario adaptable en el repositorio de AEM o los escribe en los registros de AEM, debe asegurarse de que dichos datos no se retengan en los sistemas de producción y ensayo.

## Comportamiento predeterminado con funciones listas para usar {#default-behavior}

Al utilizar funciones de Forms adaptables integradas, AEM Forms no almacena datos del usuario final. El servidor pasa directamente los datos enviados al destino que posee y configura.

Entre los mecanismos predeterminados que conectan un formulario a un destino de su propiedad se incluyen el Modelo de datos de formulario (FDM), los conectores predeterminados y las acciones de envío. Cada una de ellas envía datos a una ubicación que usted posee y configura, de modo que no se conservan en el repositorio de AEM. Un formulario también puede invocar un servicio externo o de terceros, como una API REST, desde una regla o una acción de envío y reenviar datos a ese servicio sin mantener los datos en AEM.

Si utiliza flujos de trabajo de AEM con procesos de larga duración que implican un paso de aprobación, AEM Forms puede almacenar los datos en la memoria y en el almacenamiento temporal para completar la operación. Para obtener información sobre cómo evitar que estos datos se guarden en AEM, consulte la sección [Datos en procesos de flujo de trabajo de larga duración](#long-lived-workflow-processes).

La acción de envío del portal de Forms retiene los datos capturados o enviados mediante Forms adaptable, pero los datos se guardan en una ubicación de almacenamiento que usted proporcione y posea, no en el repositorio de AEM ni en los registros. Para obtener más información, consulte [Proteger los datos guardados mediante la acción de envío del portal de formularios](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-data-saved-by-forms-portal-submit-action).

## Datos en tránsito {#data-in-transit}

Aunque AEM Forms no almacena los datos del usuario final de forma predeterminada, los datos se siguen moviendo entre el usuario final, AEM Forms y el destino que configure. Proteja este tráfico con Seguridad de la capa de transporte (TLS) para que los datos se cifren en tránsito.

Para proteger la conexión entre el explorador y AEM, habilite HTTPS en la instancia de AEM. Para ver los pasos, consulte [SSL/TLS de forma predeterminada](/help/sites-administering/ssl-by-default.md).

Además, asegúrese de que los puntos de conexión a los que AEM Forms envía datos, como las configuraciones de nube, las direcciones URL de acción de envío y las fuentes de datos del modelo de datos de formulario, utilizan puntos de conexión HTTPS seguros. Como AEM Forms no almacena los datos que pasa, el cifrado en reposo no se aplica a esos datos. Para obtener más instrucciones sobre cómo proteger la conexión, consulte [Capa de transporte segura](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-transport-layer).

## Modelo de datos de formulario para almacenes de datos externos {#form-data-model}

Para leer y escribir datos en un almacén de datos, utilice un modelo de datos de formulario (FDM). FDM es el mecanismo recomendado para conectar un formulario a una fuente de datos que usted posea y administre, como una base de datos o un servicio web RESTful.

Para obtener más información, consulte [Introducción a la integración de datos de AEM Forms](/help/forms/using/data-integration.md). Para obtener instrucciones sobre cómo proteger los datos que administra un FDM, consulte [Proteger datos administrados por el modelo de datos de formulario (FDM)](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-data-handled-by-form-data-model-fdm).

## Datos en procesos de flujo de trabajo de larga duración {#long-lived-workflow-processes}

Si utiliza procesos de flujo de trabajo de larga duración, AEM puede guardar datos temporalmente como parte de la carga útil del flujo de trabajo. Las variables de flujo de trabajo que llevan esta carga útil se almacenan en los metadatos de la instancia de flujo de trabajo del repositorio de AEM y pueden contener información de identificación personal (PII) o datos personales confidenciales (SPD) proporcionados por los usuarios finales al rellenar un formulario adaptable.

Para mantener estos datos en un repositorio que usted posea y administre, como el almacenamiento del blob de Azure, en lugar de en AEM, utilice la capacidad de externalización de datos de AEM. Al externalizar las variables, los datos no se guardan en el repositorio de AEM, sino que se almacenan en su propio repositorio de datos.

Para ver los pasos para externalizar los datos, consulte [Parametrizar datos confidenciales a variables de flujo de trabajo y almacenarlos en almacenes de datos externos](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables).

## Personalización y registro {#customization-and-logging}

AEM es una solución personalizable. Si personaliza AEM, asegúrese de que la personalización no almacene datos en el repositorio o los registros de AEM.

Cuando se utilizan funciones predeterminadas, AEM Forms no escribe datos de usuarios finales de formularios en los registros.

El código personalizado puede escribir datos en registros. Si agrega seguimiento o registro durante el desarrollo, quite los seguimientos y los datos enviados a los registros antes de implementar el código en los entornos de ensayo y producción.

## Preguntas frecuentes sobre la retención de datos de AEM Forms {#faq}

**¿AEM Forms almacena datos de formulario?**

No. De forma predeterminada, Adobe Experience Manager (AEM) Forms actúa como servidor de paso a través para los datos capturados a través de Forms adaptable y no almacena datos del usuario final en el repositorio de AEM. El servidor pasa los datos enviados al destino que posee y configura, como una fuente de datos del modelo de datos de formulario, un destino de acción de envío o una API externa. Este comportamiento predeterminado se aplica tanto a AEM Forms en OSGi como a AEM Forms en JEE.

**¿Dónde se almacenan los datos del formulario adaptable?**

Los datos de los formularios adaptables enviados se almacenan en el destino que posee y configura, no en el repositorio de Adobe Experience Manager (AEM). Los mecanismos predeterminados como el modelo de datos de formulario (FDM), los conectores y las acciones de envío envían datos a su propia ubicación. Un formulario también puede reenviar datos a un servicio externo, como una API de REST, sin persistir en AEM. La acción de envío del portal de Forms también guarda los datos en una ubicación de almacenamiento que usted proporciona y posee.

**¿Los flujos de trabajo de larga duración almacenan datos de formulario?**

Los procesos de flujo de trabajo de larga duración de Adobe Experience Manager (AEM) Forms pueden guardar datos temporalmente como parte de la carga útil de flujo de trabajo, que se almacena en los metadatos de la instancia de flujo de trabajo en el repositorio de AEM. Para mantener estos datos en un repositorio de su propiedad y que usted administre, como el almacenamiento del blob de Azure, en lugar de en AEM, use la capacidad de externalización de datos [AEM para variables de flujo de trabajo](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables).

**¿AEM Forms escribe datos en los registros?**

No. Con las funciones predeterminadas, Adobe Experience Manager (AEM) Forms no escribe datos de usuarios finales de formularios en los registros. Como AEM es una plataforma personalizable, el código personalizado puede escribir datos en los registros. Si agrega seguimiento o registro durante el desarrollo, quite esos seguimientos y los datos registrados antes de implementarlos en los entornos de ensayo y producción. Una personalización no debe almacenar datos en el repositorio de AEM ni en los registros.

**¿Cómo se protegen los datos en tránsito?**

Los datos en tránsito están protegidos con Seguridad de la capa de transporte (TLS) en Adobe Experience Manager (AEM) Forms. Habilite HTTPS en la instancia de AEM para proteger la conexión entre el explorador y AEM. Además, asegúrese de que los puntos de conexión a los que AEM Forms envía datos, como las configuraciones de nube, las direcciones URL de acción de envío y las fuentes de datos del modelo de datos de formulario, utilizan puntos de conexión HTTPS seguros. Como AEM Forms no almacena los datos que pasa, el cifrado en reposo no se aplica a esos datos.

## Recursos relacionados {#related-resources}

* [Introducción a la integración de datos de AEM Forms](/help/forms/using/data-integration.md)
* [Parametrizar datos confidenciales a variables de flujo de trabajo y almacenarlos en repositorios de datos externos](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables)
* [Configurar la acción de envío](/help/forms/using/configuring-submit-actions.md)
* [Protección y seguridad de AEM Forms en el entorno OSGi](/help/forms/using/hardening-securing-aem-forms-environment.md)
