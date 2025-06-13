---
title: Ampliación de  [!DNL Adobe Experience Manager] 6.5 mediante Adobe Developer App Builder.
description: Ampliación de  [!DNL Adobe Experience Manager] 6.5 mediante Adobe Developer App Builder.
exl-id: 8221c2db-82d4-43df-ad38-e8e7831541ac
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Ampliar [!DNL Adobe Experience Manager] mediante Adobe Developer App Builder {#extend-using-app-builder}

## Qué es App Builder para AEM {#project-appbuilder}

La nueva Adobe Developer App Builder proporciona un marco de trabajo de extensibilidad para que un desarrollador pueda ampliar fácilmente las funcionalidades de AEM.

App Builder proporciona un marco de trabajo de extensibilidad unificado de terceros para integrar y crear experiencias personalizadas que amplíen Adobe Experience Manager. Con este marco de trabajo de extensibilidad completo, basado en la infraestructura de Adobe, los desarrolladores pueden crear microservicios personalizados, ampliar e integrar Adobe Experience Manager en todas las soluciones de Adobe y en el resto de la pila de TI.

App Builder permite a los clientes ampliar fácilmente Adobe Experience Manager en varios casos de uso:

* Extensibilidad de middleware: conecte sistemas externos con aplicaciones de Adobe creando conectores personalizados o utilice un conjunto de integraciones prediseñadas.
* Extensibilidad de los servicios principales: amplíe las funciones de las aplicaciones principales ampliando el comportamiento predeterminado con funciones personalizadas y lógica empresarial.
* Extensibilidad de la experiencia del usuario: amplíe la experiencia principal para satisfacer los requisitos comerciales o cree propiedades digitales, tiendas y aplicaciones de back-office específicas para el cliente.

>[!NOTE]
>
>Para los clientes de AEM as a Cloud Service que quieran usar App Builder, vea [Ampliar Adobe Experience Manager as a Cloud Service con Adobe Developer App Builder](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html?lang=es).

## Arquitectura {#architecture}

En lugar de una solución predeterminada, Adobe Developer App Builder proporciona una plataforma de desarrollo común, coherente y estandarizada para ampliar las soluciones de Adobe Cloud como AEM, que incluye:

* Adobe Developer Console: para el desarrollo de microservicios y extensiones personalizadas, permite a los desarrolladores crear y administrar proyectos mientras acceden a todas las herramientas y API que necesitan para crear complementos e integraciones.
* Herramientas para desarrolladores: herramientas de código abierto, SDK y bibliotecas para permitir a los desarrolladores crear fácilmente integraciones y extensiones personalizadas. Utilice React Spectrum (Kit de herramientas de IU de Adobe) para tener una IU común para todas las aplicaciones de Adobe.
* Servicios: I/O Runtime para alojar infraestructura en la plataforma sin servidor de Adobe, y Eventos de I/O para integraciones basadas en eventos. Adobe también es compatible de serie con el almacenamiento de datos y archivos.
* Adobe Experience Cloud: los desarrolladores pueden enviar extensiones e integraciones para que se publiquen dentro de su organización de Experience Cloud. Los administradores del sistema pueden revisar, administrar y aprobar estas extensiones. Una vez publicadas, las extensiones y herramientas personalizadas de App Builder se pueden encontrar junto con otras aplicaciones de Adobe Experience Cloud.

El diagrama siguiente ilustra cómo una aplicación estándar creada en App Builder utiliza estas funcionalidades:

![Arquitectura](assets/appbuilder-architecture.jpg)

Para obtener más información acerca de la arquitectura de App Builder, vea [Descripción general de la arquitectura](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/architecture_overview/architecture-overview).

## Introducción a App Builder {#additional-resources}

Para ayudarle a empezar a usar App Builder, se ha creado una serie de documentos para ayudarle a empezar:

* [Introducción a App Builder](https://developer.adobe.com/app-builder/docs/get_started/)

## Continuar aprendiendo con la documentación {#appbuilder-documentation}

App Builder proporciona vídeos y documentación para desarrolladores, incluidas guías y documentación de referencia, para ayudarle a empezar a desarrollar sus propias aplicaciones personalizadas:

* [Documentación de App Builder](https://developer.adobe.com/app-builder/docs/overview/)
* [Vídeos de App Builder](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## Pruebe una de las aplicaciones de ejemplo {#appbuilder-codesamples}

¿Listo para empezar a desarrollar? Hay muchas aplicaciones de ejemplo para ayudarle a ponerse en marcha rápidamente:

* [App Builder Code Labs en el sitio web de Adobe Developer](https://developer.adobe.com/app-builder/docs/resources/)

