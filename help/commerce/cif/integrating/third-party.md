---
title: AEM Integración de Commerce de terceros y de con Commerce integration framework
description: Los negocios empresariales pueden requerir soluciones de comercio de terceros adicionales para impulsar su tienda. El Commerce integration framework CIF () se puede utilizar en estos casos de integración para conectar una solución de comercio de terceros a Adobe Experience Manager mediante I/O Runtime.
thumbnail: cif-third-party-architecture.jpg
exl-id: e99899a4-df86-4108-991a-8b30d303a279
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# AEM Integración de Commerce de terceros y de mediante Commerce integration framework {#aem-third-party}

La integración de soluciones diferentes de Adobe Commerce CIF es un escenario común para los clientes de los servicios de. Las soluciones de terceros con diferentes API y esquemas se conectan mediante una capa de integración.

## Arquitectura {#architecture}

La arquitectura general es la siguiente:

AEM ![Información general sobre la arquitectura de terceros/no Magento en el servicio de correo electrónico](../assets//AEM_nonMagento_Architecture.png)

El propósito de esta capa de integración es asignar API y esquemas de terceros a las API y esquemas de Adobe Commerce GraphQL compatibles fuera del Experience Manager. Gracias a esta encapsulación, la lógica y los sistemas de integración pueden actualizarse sin cambiar el código dentro del Experience Manager.

## Requisitos de solución para una integración

A medida que el Experience Manager recupera los datos bajo demanda, se requieren API en tiempo real para el catálogo de productos.

>[!TIP]
>
>Si no hay API en tiempo real disponibles, se debe utilizar una caché de producto externo con API para la integración. Ejemplo [Magento de código abierto](https://business.adobe.com/products/magento/open-source.html).

No es necesario implementar el esquema GraphQL completo, solo los objetos del esquema para habilitar los casos de uso deseados.

## Casos de uso back-end

CIF Amplia el Experience Manager con acceso al catálogo de productos en tiempo real y herramientas de administración de experiencias del producto. Esta integración optimizada permite a los autores acceder a los datos de comercio mediante IU incrustadas siempre que sea necesario sin salir del contexto de contenido.

Se requiere la integración de las API del catálogo de productos para desbloquear estos casos de uso.

## Casos de uso de front-end

AEM CIF CIF [Los componentes principales de la](https://github.com/adobe/aem-core-cif-components) recuperan e intercambian datos a través de las API de Adobe Commerce admitidas por la comunidad de usuarios de la plataforma de datos de la plataforma de datos de. Para reutilizar componentes, se deben implementar las API respectivas.

La recomendación para los componentes del lado del cliente esenciales para el rendimiento es comunicarse directamente con la solución de terceros para evitar la latencia.

## Desarrollo de una integración {#develop-integration}

El Adobe recomienda usar [Adobe I/O Runtime](https://developer.adobe.com/apis/experienceplatform/runtime.html) para la capa de integración. CIF Se incluye en el complemento de la para terceros. Como funciona con un enfoque similar a un microservicio, es adecuado para integrar fácilmente varias soluciones.

La [implementación de referencia](https://github.com/adobe/commerce-cif-graphql-integration-reference) es un excelente punto de partida para compilar la integración en su solución de comercio. Aunque es compatible con GraphQL, también se puede integrar con cualquier otro tipo de API, como REST.

Esta capa de integración no es necesaria si hay una capa de terceros disponible (como Mulesoft) o la integración se crea sobre la solución de terceros.

## Conectores creados previamente {#connectors}

Los conectores son un buen punto de partida para los proyectos. Vienen con una conexión específica de la solución de comercio y una asignación de API predeterminada. Estos conectores son construidos por terceros y no mantenidos por Adobe. Póngase en contacto con el socio correspondiente para obtener información.

* [SAP Commerce](https://github.com/diconium/commerce-cif-graphql-integration-hybris), creado por Diconium
* [Herramientas de comercio](https://github.com/diconium/commerce-cif-graphql-integration-commercetool), creadas por Diconium

>[!TIP]
>
>Aunque los conectores ayudan a los proyectos a acelerar la integración comercial, no son plug-n-play. Las soluciones de comercio empresarial están muy personalizadas y requieren una integración personalizada. Se requiere un buen conocimiento de la plataforma de comercio, los esquemas de Adobe Commerce GraphQL y Adobe I/O Runtime.
