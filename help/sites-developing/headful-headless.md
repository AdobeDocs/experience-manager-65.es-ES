---
title: Encabezado y sin cabeza en AEM
description: AEM proyectos se pueden implementar en un modelo de cabeza y cabeza, pero la elección no es binaria. AEM ofrece la flexibilidad para aprovechar las ventajas de ambos modelos en un proyecto.
source-git-commit: cf7e9061bac9004c7efd2f045b4900e4a92d67e9
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 0%

---

# Encabezado y sin cabeza en AEM {#headful-headless}

Los proyectos de Adobe Experience Manager se pueden implementar tanto en modelos encabezados como sin encabezado, pero la elección no es binaria. AEM ofrece la flexibilidad para aprovechar las ventajas de ambos modelos en un proyecto. Este documento proporciona información general sobre los diferentes modelos y describe los niveles de integración de SPA.

## Información general {#overview}

AEM ofrece potentes herramientas para administrar la creación de contenido y su envío en una plataforma. Se trata de un modelo tradicional de gestión de contenido &quot;optimista&quot;, en el que los autores y desarrolladores de contenido trabajan en la misma plataforma para ofrecer las experiencias a los consumidores de contenido.

AEM puede utilizarse simplemente para administrar el contenido, lo que permite que la presentación y el envío del contenido se gestionen mediante otra plataforma. Este es el modelo &quot;sin objetivos&quot; de la administración de contenido, donde los autores y desarrolladores de contenido trabajan en distintas plataformas para ofrecer experiencia a los consumidores de contenido.

Pero no tiene por qué ser una elección binaria. AEM ofrece una flexibilidad sin precedentes, lo que le permite aprovechar las ventajas de ambos modelos para su proyecto.

![Modelos de implementación de AEM](headless/assets/aem-implementation-models.png)

En un modelo de pila completa o con encabezado, el contenido se administra en el repositorio de AEM y en los componentes de AEM basados en Java, HTL, etc. se utilizan para representar el contenido para la experiencia del usuario. En este modelo, la creación del contenido, el estilo, la presentación y la entrega se realizan en AEM.

En un modelo sin encabezado, el contenido se administra en el repositorio de AEM, pero se envía mediante API como REST y GraphQL a otro sistema para procesar el contenido para la experiencia del usuario. En este modelo, el contenido se crea en AEM, pero diseñándolo, presentándolo y entregándolo todo se produce en otra plataforma.

Las aplicaciones de una sola página (SPA) suelen ser el destino del contenido que AEM entrega sin encabezado. Sin embargo, estos SPA no tienen que ser completamente externos a AEM. AEM le permite decidir en qué medida sus SPA están integradas en AEM. Veamos un ejemplo.

## Ejemplo de Web Shop {#web-shop-example}

Digamos que tiene una tienda web existente para su empresa como SPA. En él tiene todos sus detalles e imágenes de productos. A continuación, introduzca AEM para impulsar sus esfuerzos de marketing, como sitios promocionales, blogs y contenido de campaña. ¿Cómo se integran los dos? AEM permite una amplia gama de opciones:

* **Permita que los sistemas funcionen de forma independiente.**
* **Proporcione a la tienda web contenido limitado de AEM a través de GraphQL.** Los autores pueden crear el contenido en AEM, pero solo se puede ver a través del SPA de tienda web.
* **Incruste la tienda web SPA en AEM.** Los autores pueden crear el contenido en AEM y verlo en AEM en el contexto de la tienda web, pero no manipularlo.
* **Incruste la tienda web SPA en AEM y habilite puntos editables.** Los autores pueden crear el contenido en AEM y verlo en AEM en el contexto de la tienda web, y los autores tienen una capacidad limitada para manipular el contenido de la tienda web SPA dentro de AEM.
* **Incruste los SPA de webs en AEM y habilite zonas enteras para editarlas.** Los autores pueden crear el contenido en AEM y verlo en AEM en el contexto de la tienda web, y los autores tienen una capacidad limitada para manipular el contenido de la tienda web SPA dentro de AEM.

La siguiente sección explora estos niveles de integración con más detalle.

>[!NOTE]
>
>Por supuesto, también puede volver a implementar el SPA de tienda web como un AEM que funcione completamente SPA [uso del marco AEM SPA Editor.](/help/sites-developing/spa-walkthrough.md) Si ya tiene AEM y desea crear una nueva tienda web u otra SPA, este es el método recomendado, pero está fuera del ámbito de este documento.

## Niveles de integración SPA {#integration-levels}

SPA integración se encuentra en un espectro de cuatro niveles en AEM.

* **Nivel 0: Sin integración**
   * Los SPA y AEM existen por separado y no intercambian información.
   * El contenido se crea, administra y entrega de forma independiente en dos sistemas independientes.
* **Nivel 1: Integración de fragmentos de contenido**
   * [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) se utilizan en AEM para crear y administrar contenido limitado para el SPA.
   * El SPA recupera este contenido a través de AEM [API de GraphQL.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * Algunos contenidos se administran en AEM y otros en un sistema externo.
   * El contenido solo se puede ver en la SPA.
* **Nivel 2: Incrustar el SPA en AEM**
   * [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) se utilizan en AEM para crear y administrar el contenido del SPA.
   * El SPA recupera este contenido a través de AEM [API de GraphQL.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * Algunos contenidos se administran en AEM y otros en un sistema externo.
   * El contenido se puede ver en contexto dentro de AEM.
   * El contenido limitado se puede editar dentro de AEM.
* **Nivel 3: Incrustar y habilitar completamente SPA en AEM**
   * [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) se utilizan en AEM para crear y administrar el contenido del SPA.
   * El SPA recupera este contenido a través de AEM [API de GraphQL.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * El contenido se puede ver en contexto dentro de AEM.
   * La mayoría del contenido se puede editar dentro de AEM.

El nivel 1 es un ejemplo de una implementación típica sin encabezado. Sin embargo, los autores de contenido solo pueden ver su contenido en contexto dentro del SPA. AEM es solo una herramienta de creación.

La ventaja y flexibilidad de la AEM se hace evidente con los niveles 2 y 3, conservando al mismo tiempo las ventajas de la SPA. Los autores de contenido pueden crear su contenido en AEM, pero también verlo en contexto dentro de AEM. El SPA obtiene la capacidad de ser creado en AEM, pero aun así se puede entregar como SPA.

## Implementación de los niveles de integración {#implementing}

Hay diferentes herramientas disponibles en AEM según el nivel de integración que elija. Cada nivel se basa en las herramientas utilizadas en el anterior. La siguiente lista vincula a los recursos relevantes.

* **Nivel 1:** Los fragmentos de contenido y la variable [Marco AEM sin encabezado](/help/sites-developing/headless/introduction.md) se puede utilizar para enviar AEM contenido al SPA.
* **Nivel 2:** Además del nivel uno:
   * [El componente RemotePage](/help/sites-developing/spa-remote-page.md) se puede utilizar para integrar la SPA externa en AEM donde AEM contenido se puede ver en contexto.
   * Algunos puntos del SPA también se pueden habilitar para [permitir la edición limitada en AEM.](/help/sites-developing/spa-edit-external.md)
* **Nivel 3:** Además del nivel dos:
   * Las zonas enteras del SPA se pueden habilitar para permitir una edición completa en AEM.
