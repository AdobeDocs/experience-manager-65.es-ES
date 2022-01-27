---
title: Integración de AEM y Adobe Commerce con Commerce Integration Framework
description: AEM y Adobe Commerce se integran perfectamente con Commerce Integration Framework (CIF). CIF permite a AEM acceder a una instancia de Adobe Commerce y comunicarse con Adobe Commerce a través de GraphQL. También permite a los autores de AEM utilizar los seleccionadores de productos y categorías, así como la consola de productos, para examinar los datos de productos y categorías que se obtienen a petición de Adobe Commerce . Además, CIF ofrece una tienda predeterminada que puede acelerar los proyectos de comercio.
thumbnail: aem-magento-architecture.jpg
exl-id: f843784c-5ff7-41d1-97c5-13facb8459b2
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 29%

---

# Integración de AEM y Adobe Commerce (Magento) con Commerce Integration Framework {#aem-commerce-framework}

El Experience Manager y Adobe Commerce se integran perfectamente con Commerce Integration Framework (CIF). CIF permite a AEM acceder directamente a la instancia de comercio y comunicarse con ella mediante Adobe Commerce [API de GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
> La versión mínima de la API de GraphQL admitida es 2.3.5. Algunas funciones solo se admiten en versiones más recientes o solo en la edición de Adobe Commerce.

## Información general sobre la arquitectura {#overview}

La arquitectura general es la siguiente:

![Información general sobre la arquitectura del CIF](../assets/AEM_Magento_Architecture.png)

Dentro de CIF, existe compatibilidad con patrones de comunicación del lado del servidor y del lado del cliente.
Las llamadas de API del lado del servidor se implementan mediante el complemento genérico [Cliente de GraphQL](https://github.com/adobe/commerce-cif-graphql-client) en combinación con un [conjunto de modelos de datos generados](https://github.com/adobe/commerce-cif-magento-graphql) para el esquema commerce GraphQL. Además, se puede utilizar cualquier consulta o mutación de GraphQL en formato GQL.

Para los componentes del lado del cliente, que se generan mediante [React](https://reactjs.org/), se utiliza el cliente [Apollo](https://www.apollographql.com/docs/react/).

## Arquitectura de los componentes principales del CIF de AEM {#cif-core-components}

![Arquitectura de los componentes principales del CIF de AEM](../assets/cif-component-architecture.jpg)

[Componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components) siga patrones de diseño y prácticas recomendadas muy similares a los de [Componentes principales AEM WCM](https://github.com/adobe/aem-core-wcm-components).

La lógica empresarial y la comunicación back-end con Adobe Commerce para los componentes principales del CIF de AEM se implementan en los modelos Sling. En caso de que sea necesario personalizar esta lógica para cumplir los requisitos específicos del proyecto, se puede utilizar el patrón de delegación para modelos Sling.

>[!TIP]
>
>La página [Personalización de los componentes principales del CIF de AEM](../customizing/customize-cif-components.md) tiene un ejemplo detallado y una práctica recomendada sobre cómo personalizar los componentes principales del CIF.

Dentro de los proyectos, AEM componentes principales del CIF y los componentes de proyecto personalizados pueden recuperar fácilmente el cliente configurado para una tienda de Adobe Commerce asociada a una página AEM mediante la configuración según el contexto de Sling.
