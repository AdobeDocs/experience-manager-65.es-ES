---
title: Introducción y descripción general
description: Introducción y descripción general del contenido y el comercio. Experience Manager Commerce Integration Framework (CIF) es el patrón recomendado por el Adobe para integrar y ampliar los servicios de comercio de Magento y otras soluciones de comercio de terceros con el Experience Cloud.
thumbnail: introducing-aem-commerce.jpg
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 2%

---

# Contenido y comercio {#content-commerce}

Con el contenido y el comercio de Adobe Experience Manager, las marcas pueden escalar e innovar más rápido para diferenciar las experiencias comerciales y capturar un gasto en línea acelerado. AEM Contenido y comercio combina las experiencias inmersivas, omnicanal y personalizadas en Experience Manager con cualquier cantidad de soluciones de comercio para ofrecer experiencias diferenciadas en todas las partes del recorrido de compras, reduciendo el tiempo de respuesta al valor e impulsando una mayor conversión.

## Cómo el contenido y el comercio ayudan a los clientes a tener éxito

Con las crecientes expectativas de los clientes para las experiencias de comercio en línea, las marcas se ven presionadas para ofrecer experiencias diferenciadas y más contenido más rápido. Sin embargo, la implementación de una plataforma de administración de contenido a menudo requiere de fuertes inversiones en tiempo y presupuesto para desarrollar elementos fundamentales, como componentes personalizados y herramientas de creación, y acumula costos en mantenimiento y actualizaciones. Experience Manager Sites ofrece Contenido y comercio como módulo de complementos para Experience Manager que proporciona componentes comerciales básicos, herramientas de creación y una tienda de referencia para acelerar el lanzamiento, permitir una colaboración fluida entre equipos e impulsar la conversión.

Las marcas pueden integrar Experience Manager con Adobe Commerce, parte de Adobe Experience Cloud, así como cualquier motor de comercio que desee. Con Contenido y comercio Experience Manager, las marcas pueden:

* Escalar e innovar más rápido
* Personalización de experiencias para impulsar la conversión
* Crear una vez y publicar en todas partes
* Enriquecimiento y diferenciación de experiencias para los clientes
* Optimice la creación con acceso a datos de comercio

## Presentación de AEM Commerce Integration Framework (CIF) {#cif-intro}

Como estos proyectos tienen que lidiar con la complejidad de integrar una solución de comercio. Una solución comercial puede ser cualquier cosa, desde una solución comercial como Adobe Commerce hasta un conjunto de servicios de comercio personalizados. La integración depende en gran medida del ecosistema y los casos de uso. Suele afectar a varios lugares y viene con muchos sabores diferentes:

* Integración de un ecosistema complejo y dinámico (por ejemplo, catálogos de productos)
* El negocio necesita administrar el contenido del producto con su propio ciclo de vida de una manera eficiente y omnicanal
* Creación de recorridos de compra complejos y personalizados para varias cabezas
* Capacidad de adaptarse e innovar rápidamente en el back-end y el front-end
* Ejecutando una infraestructura E2E escalable y estable que está diseñada para obtener un rendimiento máximo (venta de Flash, Black Friday, ...). Esto incluye la búsqueda unificada y la administración de la caché.

Esta complejidad abre la puerta a posibles puntos de falla, aumento del TCO, retrasos y menor realización de valor. Estas razones han llevado al desarrollo del marco de integración comercial (CIF), que es un complemento para el Experience Manager. CIF amplía el Experience Manager con capacidades comerciales y estandariza la integración con un motor de comercio. El resultado es una solución estable, escalable y a prueba de futuro con menor TCO. Desbloquea la innovación técnica y empresarial con herramientas ágiles y funciones integradas para crear experiencias comerciales atractivas.

![Elementos del CIF](./assets/CIF/CIF_Overview.png)

## CIF admite clientes correctamente desde 2013

Con más de 200 clientes, CIF se ha establecido como un ingrediente exitoso para un proyecto de comercio y contenido exitoso. Esto proporciona valor para TI y el negocio de hoy y en el futuro. Los proyectos recientes de los clientes describen CIF como un &quot;acelerador Bueno y ahorrador de tiempo enorme con mucho valor&quot;.

## Beneficios del CIF {#cif-benefits}

CIF proporciona componentes básicos de comercio listos para usar que reducen la necesidad de usar código personalizado, lo que acelera el tiempo de comercialización de las marcas. Todos los componentes principales están integrados de forma predeterminada con la capa de datos del lado del cliente de Adobe para hidratar los perfiles de los clientes, como el perfil unificado. Este perfil captura en detalle el comportamiento de un visitante, que puede utilizarse para predecir y personalizar el recorrido del cliente en tiempo real.

El complemento CIF lleva el contexto del producto al Experience Manager y proporciona herramientas de creación, como una consola de producto y selectores de producto/categoría, que permiten al especialista en marketing crear y ofrecer experiencias de ventas en Experience Manager sin depender del desarrollador. Las ventajas incluyen:

### Experiencias

Las potentes herramientas del CIF en AEM permiten a los creadores de contenido crear rápidamente experiencias de comercio enriquecidas y personalizadas de una manera escalable y sin diferencias de envío para aprovechar las oportunidades comerciales.

![Elementos del CIF](./assets/CIF/CIF_Product_Experience_Management.png)

### Tiempo para el valor (TTV)

Acelera el desarrollo de proyectos con [AEM Componentes principales](https://www.aemcomponents.dev/), [AEM tienda de referencia de Venia](https://github.com/adobe/aem-cif-guides-venia), [AEM Tipo de archivo del proyecto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) y patrones de integración para PWA (Contenido y comercio sin encabezado).

El CIF está diseñado para la innovación continua con un complemento siempre actualizado, que permite al cliente acceder a funciones nuevas y mejoradas.

### Integraciones

Conecte su ecosistema (por ejemplo, la solución de comercio) con el Experience Cloud mediante [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html), un PaaS sin servidor basado en microservicios y la implementación de referencia del [CIF](https://github.com/adobe/commerce-cif-graphql-integration-reference).

## Patrones comprobados y prácticas recomendadas

CIF admite clientes con patrones de integración estandarizados basados en prácticas recomendadas. Esto ayuda a los clientes a tener éxito hoy en día y es flexible para crecer con el cliente y adaptarse a los requisitos futuros:

* Elimina los desafíos típicos relacionados con las integraciones de catálogos de productos que pueden producirse. Ejemplos:
   * Problemas de rendimiento con mayor volumen o complejidad del catálogo
   * Sin acceso a los datos clasificados
   * Necesidad de experiencias y datos de productos en tiempo real
* La creciente madurez digital hace que sea necesario administrar la experiencia. El CIF incluye capacidades de administración de experiencia de producto que se pueden incorporar gradualmente sin necesidad de un esfuerzo adicional de TI.
* Listo para todos los canales: CIF admite una variedad de tecnologías de puntos de contacto (del lado del servidor, híbridas, del lado del cliente) con patrones, aceleradores y componentes principales.
