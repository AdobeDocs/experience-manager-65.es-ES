---
title: Integración comercial de AEM y terceros con Commerce Integration Framework
description: Los negocios empresariales pueden requerir soluciones de comercio de terceros adicionales para impulsar su tienda. Commerce Integration Framework (CIF) se puede utilizar en estos escenarios de integración para conectar una solución de comercio de terceros a Adobe Experience Manager mediante I/O Runtime.
thumbnail: cif-third-party-architecture.jpg
exl-id: e99899a4-df86-4108-991a-8b30d303a279
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 4%

---

# Integración del comercio de AEM y terceros con Commerce Integration Framework {#aem-third-party}

La integración de soluciones que no son de Adobe Commerce es un escenario común para CIF. las soluciones de terceros con diferentes API y esquemas se conectan mediante una capa de integración.

## Arquitectura {#architecture}

La arquitectura general es la siguiente:

![Descripción general de la arquitectura de terceros/no Magento de AEM](../assets//AEM_nonMagento_Architecture.png)

El propósito de esta capa de integración es asignar las API y los esquemas de terceros a las API y los esquemas compatibles de Adobe Commerce GraphQL fuera del Experience Manager. Gracias a esta encapsulación, la lógica de integración y los sistemas se pueden actualizar sin cambiar el código dentro del Experience Manager.

## Requisitos de solución para una integración

A medida que el Experience Manager recupera los datos bajo demanda, se requieren API en tiempo real para el catálogo de productos.

>[!TIP]
>
>Si no hay API en tiempo real disponibles, se debe utilizar una caché de producto externa con API para la integración. Ejemplo [Magento de código abierto](https://business.adobe.com/products/magento/open-source.html).

No es necesario implementar el esquema completo de GraphQL, solo los objetos del esquema para habilitar los casos de uso deseados.

## Casos de uso back-end

CIF amplía el Experience Manager con herramientas de administración de experiencia de producto y acceso al catálogo de productos en tiempo real. Esta integración perfecta permite a los autores acceder a los datos de comercio mediante las IU incrustadas siempre que sea necesario sin abandonar el contexto de contenido.

La integración de las API del catálogo de productos es necesaria para desbloquear estos casos de uso.

## Casos de uso del front-end

[Componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components) recupere e e intercambie datos mediante las API de Adobe Commerce compatibles con CIF. Para reutilizar componentes, es necesario implementar las API correspondientes.

La recomendación para los componentes críticos del cliente de rendimiento es comunicarse directamente con la solución de terceros para evitar la latencia.

## Desarrollo de una integración {#develop-integration}

Se recomienda usar [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html) para la capa de integración. Se incluye en el complemento CIF para terceros. Como funciona con un enfoque de microservicio, es adecuado para integrar fácilmente varias soluciones.

La variable [implementación de referencia](https://github.com/adobe/commerce-cif-graphql-integration-reference) es un bueno punto de partida para integrar su solución de comercio. Aunque es compatible con GraphQL, también se puede integrar con cualquier otro tipo de API, como REST.

Esta capa de integración no es necesaria si hay disponible una capa de terceros (como Mulesoft) o si la integración se integra sobre la solución de terceros.
