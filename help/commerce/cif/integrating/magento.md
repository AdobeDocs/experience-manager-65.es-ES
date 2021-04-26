---
title: Integración de comercio de AEM y Adobe (Magento) mediante Commerce Integration Framework
description: AEM y Adobe Commerce (Magento) se integran perfectamente con Commerce Integration Framework (CIF). CIF permite a AEM acceder a una instancia de Magento y comunicarse con Magento a través de GraphQL. También permite a los autores de AEM utilizar los seleccionadores de productos y categorías, así como la consola de productos para examinar los datos de productos y categorías que se obtienen a petición de Magento. Además, CIF ofrece una tienda predeterminada que puede acelerar los proyectos de comercio.
thumbnail: aem-magento-architecture.jpg
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 42%

---

# Integración de comercio de AEM y Adobe (Magento) mediante Commerce Integration Framework {#aem-magento-framework}

El Experience Manager y el Magento de comercio (Adobe Commerce) se integran perfectamente con Commerce Integration Framework (CIF). CIF permite a AEM acceder directamente a la instancia de comercio y comunicarse con ella mediante las [API de GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) de Adobe Commerce.

## Información general sobre la arquitectura {#overview}

La arquitectura general es la siguiente:

![Información general sobre la arquitectura del CIF](../assets/AEM_Magento_Architecture.png)

Dentro de CIF hay asistencia para patrones de comunicación del lado del servidor y del lado del cliente.
Las llamadas del lado del servidor de API se implementan mediante el [cliente de GraphQL](https://github.com/adobe/commerce-cif-graphql-client) genérico integrado en combinación con un [conjunto de modelos de datos generados](https://github.com/adobe/commerce-cif-magento-graphql) para el esquema de comercio GraphQL. Además, se puede utilizar cualquier consulta o mutación de GraphQL en formato GQL.

Para los componentes del lado del cliente, que se generan mediante [React](https://reactjs.org/), se utiliza el cliente [Apollo](https://www.apollographql.com/docs/react/).

## Arquitectura de los componentes principales del CIF de AEM {#cif-core-components}

![Arquitectura de los componentes principales del CIF de AEM](../assets/cif-component-architecture.jpg)

[AEM componentes principales del CIF ](https://github.com/adobe/aem-core-cif-components) siguen patrones de diseño y prácticas recomendadas muy similares a los de los  [AEM componentes principales de WCM](https://github.com/adobe/aem-core-wcm-components).

La lógica empresarial y la comunicación back-end con Adobe Commerce para los componentes principales del CIF de AEM se implementan en los modelos Sling. En caso de que sea necesario personalizar esta lógica para cumplir los requisitos específicos del proyecto, se puede utilizar el patrón de delegación para modelos Sling.

>[!TIP]
>
>La página [Personalización de los componentes principales del CIF de AEM](../customizing/customize-cif-components.md) tiene un ejemplo detallado y una práctica recomendada sobre cómo personalizar los componentes principales del CIF.

Dentro de los proyectos, AEM componentes principales del CIF y los componentes de proyecto personalizados pueden recuperar fácilmente el cliente configurado para un almacén de comercio de Adobe asociado a una página de AEM mediante la configuración según el contexto de Sling.
