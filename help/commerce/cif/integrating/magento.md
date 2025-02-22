---
title: AEM Integración de Adobe Commerce y de con Commerce integration framework
description: AEM Las soluciones de Adobe Commerce y de se integran perfectamente con el Commerce integration framework CIF (). CIF AEM La permite a los usuarios acceder a una instancia de Adobe Commerce y comunicarse con Adobe Commerce a través de GraphQL. AEM También permite a los autores de la utilizar los seleccionadores de productos y categorías, así como la consola de productos para examinar los datos de productos y categorías que se obtienen a petición de Adobe Commerce Además, CIF ofrece una tienda predeterminada que puede acelerar los proyectos de comercio.
thumbnail: aem-magento-architecture.jpg
exl-id: f843784c-5ff7-41d1-97c5-13facb8459b2
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 23%

---

# AEM Integración de y Adobe Commerce (Magento) con Commerce integration framework {#aem-commerce-framework}

El Experience Manager y Adobe Commerce se integran perfectamente con el Commerce integration framework CIF (). CIF AEM La permite a los usuarios acceder directamente a la instancia de commerce y comunicarse con ella mediante las [API de GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) de Adobe Commerce.

>[!NOTE]
>
>La versión mínima de la API de GraphQL admitida es 2.3.5. Algunas funciones solo son compatibles con las versiones más recientes o solo con la edición de Adobe Commerce.

## Información general sobre la arquitectura {#overview}

La arquitectura general es la siguiente:

![Información general sobre la arquitectura del CIF](../assets/AEM_Magento_Architecture.png)

CIF Dentro de, hay compatibilidad con patrones de comunicación del lado del servidor y del lado del cliente.
Las llamadas de API del lado del servidor se implementan mediante el [cliente GraphQL](https://github.com/adobe/commerce-cif-graphql-client) genérico integrado en combinación con un [conjunto de modelos de datos generados](https://github.com/adobe/commerce-cif-magento-graphql) para el esquema de Commerce GraphQL. Además, se puede utilizar cualquier consulta o mutación de GraphQL en formato GQL.

Para los componentes del lado del cliente, que se generan mediante [React](https://reactjs.org/), se utiliza el cliente [Apollo](https://www.apollographql.com/docs/react/).

## AEM CIF Arquitectura de componentes principales de {#cif-core-components}

![Arquitectura de los componentes principales del CIF de AEM](../assets/cif-component-architecture.jpg)

AEM CIF AEM [Los componentes principales de la](https://github.com/adobe/aem-core-cif-components) siguen patrones de diseño y prácticas recomendadas muy similares a los de los [componentes principales de WCM de la](https://github.com/adobe/aem-core-wcm-components).

La lógica empresarial y la comunicación back-end con Adobe Commerce AEM CIF para los componentes principales de la se implementan en los modelos Sling. En caso de que sea necesario personalizar esta lógica para cumplir los requisitos específicos del proyecto, se puede utilizar el patrón de delegación para modelos Sling.

>[!TIP]
>
>La página [Personalización de los componentes principales del CIF de AEM](../customizing/customize-cif-components.md) tiene un ejemplo detallado y una práctica recomendada sobre cómo personalizar los componentes principales del CIF.

AEM CIF Dentro de los proyectos, los componentes principales de la y los componentes de proyecto personalizados pueden recuperar fácilmente el cliente configurado para una tienda de Adobe Commerce AEM asociado a una página mediante la configuración según el contexto de Sling.
