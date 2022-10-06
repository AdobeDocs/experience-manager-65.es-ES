---
title: Acceso y entrega de fragmentos de contenido Guía de inicio rápido sin encabezado
description: Aprenda a utilizar AEM API de REST de Assets para administrar fragmentos de contenido y la API de GraphQL para ofrecer contenido sin encabezado de fragmentos de contenido.
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
source-git-commit: 6c75af3957c319c38177cd62c90e781a982ba91b
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 77%

---

# Acceso y entrega de fragmentos de contenido Guía de inicio rápido sin encabezado {#accessing-delivering-content-fragments}

Aprenda a utilizar AEM API de REST de Assets para administrar fragmentos de contenido y la API de GraphQL para ofrecer contenido sin encabezado de fragmentos de contenido.

## ¿Qué son las API de REST de GraphQL y Assets? {#what-are-the-apis}

[Ahora que ha creado algunos fragmentos de contenido,](create-content-fragment.md) puede utilizar las API de AEM para entregarlas sin problemas.

* [La API de GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) permite crear solicitudes para acceder a fragmentos de contenido y enviarlos.
   * Para usar esto, [los puntos de conexión deben definirse y habilitarse en AEM](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint) y, si es necesario, la [interfaz de GraphiQL debe instalarse](/help/assets/content-fragments/graphql-api-content-fragments.md#installing-graphiql-interface).
* La [API de REST de Assets](/help/assets/assets-api-content-fragments.md) permite crear y modificar fragmentos de contenido (y otros recursos).

El resto de esta guía se centrará en el acceso a GraphQL y la entrega de fragmentos de contenido.

## Cómo entregar un fragmento de contenido mediante GraphQL {#how-to-deliver-a-content-fragment}

Los arquitectos de la información deberán diseñar consultas para sus puntos de conexión de canal para poder entregar contenido. Por lo general, estas consultas solo tendrán que considerarse una vez por punto de conexión y modelo. Para los fines de esta guía de introducción solo tendremos que crear una.

1. Inicie sesión en AEM y acceda a la interfaz de GraphiQL:
   * Por ejemplo: `https://<host>:<port>/content/graphiql.html`.

1. El de GraphiQL es un editor de consultas en el explorador para GraphQL. Puede utilizarlo para crear consultas, recuperar fragmentos de contenido y entregarlos sin encabezado como JSON.
   * El panel izquierdo le permite crear la consulta.
   * El panel derecho muestra los resultados.
   * El editor de consultas incluye la finalización del código y teclas de función para ejecutar fácilmente la consulta.
      ![Editor de GraphiQL](../assets/graphiql.png)

1. Suponiendo que el modelo que hemos creado se llamara `person` con campos `firstName`, `lastName` y `position`, podemos generar una consulta sencilla para recuperar el contenido de nuestro fragmento de contenido.

   ```text
   query 
   {
     personList {
       items {
         _path
         firstName
         lastName
         position
       }
     }
   }
   ```

1. Introduzca la consulta en el panel izquierdo.
   ![Consulta de GraphiQL](../assets/graphiql-query.png)

1. Haga clic en el botón **Ejecutar consulta** o use la tecla de función `Ctrl-Enter`, los resultados se mostrarán como JSON en el panel derecho.
   ![Resultados de GraphiQL](../assets/graphiql-results.png)

1. Haga clic:
   * **Documentos** en la parte superior derecha de la página para mostrar documentación en contexto que le ayude a crear sus consultas que se adapten a sus propios modelos.
   * **Historial** en la barra de herramientas superior para mostrar consultas anteriores.
      ![Documentación de GraphiQL](../assets/graphiql-documentation.png)

GraphQL permite consultas estructuradas que pueden dirigirse no solo a conjuntos de datos específicos u objetos de datos individuales, sino que también pueden proporcionar elementos específicos de los objetos, resultados anidados, compatibilidad con variables de consulta y mucho más.

GraphQL puede evitar las solicitudes de API iterativas, así como el exceso de entrega, y en su lugar permite realizar entregas masivas de exactamente lo que se necesita para procesar como respuesta a una única consulta de API. El JSON resultante se puede utilizar para entregar datos en otros sitios o aplicaciones.

## Siguientes pasos {#next-steps}

¡Eso es todo! Ahora tiene una comprensión básica de la administración de contenido sin encabezado en AEM. Por supuesto, hay muchos más recursos en los que puede profundizar para comprender las funciones disponibles.

* **[Explorador de configuración](create-configuration.md)** - Para obtener más información sobre el Explorador de configuración de AEM
* **[Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)**: para obtener más información acerca de la creación y administración de fragmentos de contenido
* **[Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets](/help/assets/assets-api-content-fragments.md)**: para obtener más información sobre el acceso al contenido de AEM directamente a través de la API HTTP, mediante las operaciones CRUD (Crear, Leer, Actualizar, Eliminar)
* **[API de GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md)**: para obtener más información sobre cómo enviar fragmentos de contenido sin encabezado
