---
title: Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets
seo-title: Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets
description: Obtenga información sobre la compatibilidad con fragmentos de contenido en la API HTTP de Recursos AEM.
seo-description: Obtenga información sobre la compatibilidad con fragmentos de contenido en la API HTTP de Recursos AEM.
uuid: c500d71e-ceee-493a-9e4d-7016745c544c
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: extending-assets
discoiquuid: 03502b41-b448-47ab-9729-e0a66a3389fa
docset: aem65
translation-type: tm+mt
source-git-commit: eb36f8fe6b08e03eb25e96ed1c31957f7d5aff27

---


# Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets{#content-fragments-support-in-aem-assets-http-api}

## Información general {#overview}

>[!NOTE]
>
>La API [HTTP de](/help/assets/mac-api-assets.md) Assets incluye:
>
>* API de REST de recursos
>* incluida la compatibilidad con fragmentos de contenido
>
>
La implementación actual de la API HTTP de AEM Assets es REST.

La API [REST de Adobe Experience Manager (AEM)](/help/assets/mac-api-assets.md) Assets permite a los desarrolladores acceder al contenido (almacenado en AEM) directamente a través de la API HTTP, mediante operaciones CRUD (Crear, leer, actualizar, eliminar).

La API le permite utilizar AEM como un CMS sin encabezado (Content Management System) al proporcionar servicios de contenido a una aplicación front-end de JavaScript. O cualquier otra aplicación que pueda ejecutar solicitudes HTTP y gestionar respuestas JSON.

Por ejemplo, las aplicaciones de una sola página (SPA), basadas en marcos o personalizadas, requieren contenido proporcionado a través de la API HTTP, a menudo en formato JSON.

Aunque los componentes principales de AEM proporcionan una API muy completa, flexible y personalizable que puede ofrecer las operaciones de lectura necesarias para este fin y cuya salida JSON se puede personalizar, sí que requieren el conocimiento práctico de AEM WCM (Web Content Management) para la implementación, ya que deben alojarse en páginas (API) basadas en plantillas de AEM dedicadas. No todas las organizaciones de desarrollo de la EPA tienen acceso a esos recursos.

Es cuando se puede utilizar la API REST de Assets. Permite a los desarrolladores acceder a los recursos (por ejemplo, imágenes y fragmentos de contenido) directamente, sin necesidad de incrustarlos primero en una página y entregar su contenido en formato JSON serializado. (Tenga en cuenta que no es posible personalizar la salida JSON desde la API REST de Assets). La API de REST de recursos también permite a los desarrolladores modificar contenido mediante la creación, actualización o eliminación de recursos, fragmentos de contenido y carpetas existentes.

La API de REST de Recursos:

* sigue el principio de [HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)

* implementa el formato [SIREN](https://github.com/kevinswiber/siren)

## Requisitos previos {#prerequisites}

La API de REST de Assets está disponible en cada instalación predeterminada de una versión reciente de AEM.

## Conceptos clave {#key-concepts}

La API de REST de Recursos ofrece acceso al estilo [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)a los recursos almacenados en una instancia de AEM. Utiliza el punto final y requiere la ruta del recurso para acceder a él (sin el encabezado `/api/assets` `/content/dam`).

El método HTTP determina la operación que se va a ejecutar:

* **GET** : para recuperar una representación JSON de un recurso o una carpeta
* **POST** : para crear nuevos recursos o carpetas
* **PUT** : para actualizar las propiedades de un recurso o una carpeta
* **ELIMINAR** : para eliminar un recurso o una carpeta

>[!NOTE]
>
>El cuerpo de la solicitud y/o los parámetros de URL pueden utilizarse para configurar algunas de estas operaciones; por ejemplo, defina que una carpeta o un recurso debe crearse mediante una solicitud **POST** .

El formato exacto de las solicitudes admitidas se define en la documentación de referencia [de la](/help/assets/assets-api-content-fragments.md#api-reference) API.

### Comportamiento transaccional {#transactional-behavior}

Todas las solicitudes son atómicas.

Esto significa que las siguientes (`write`) solicitudes no pueden combinarse en una sola transacción que pueda tener éxito o fallar como una sola entidad.

### AEM (Assets) REST API y AEM Components {#aem-assets-rest-api-versus-aem-components}

<table>
 <tbody>
  <tr>
   <td>Aspecto</td>
   <td>API de REST de recursos<br /> </td>
   <td>Componente<br /> AEM (componentes que utilizan modelos Sling)</td>
  </tr>
  <tr>
   <td>Casos de uso admitidos</td>
   <td>Finalidad general.</td>
   <td><p>Optimizado para el consumo en una aplicación de una sola página (SPA) o en cualquier otro contexto (que requiera contenido).</p> <p>También puede contener información de diseño.</p> </td>
  </tr>
  <tr>
   <td>Operaciones admitidas</td>
   <td><p>Crear, leer, actualizar, eliminar.</p> <p>Con operaciones adicionales en función del tipo de entidad.</p> </td>
   <td>Solo lectura.</td>
  </tr>
  <tr>
   <td>Acceso</td>
   <td><p>Se puede acceder directamente.</p> <p>Utiliza el <code>/api/assets </code>punto final, asignado a <code>/content/dam</code> (en el repositorio).</p> <p><code class="code">
       /content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten</code><br /> Por ejemplo, para acceder a: solicitud:<br /> <code>/api/assets/we-retail/en/experiences/arctic-surfing-in-lofoten.model.json</code></p> </td>
   <td><p>Es necesario hacer referencia a través de un componente de AEM en una página de AEM.</p> <p>Utiliza el <code>.model</code> selector para crear la representación JSON.</p> <p>Un ejemplo de URL sería el siguiente:<br /> <code>https://localhost:4502/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.model.json</code></p> </td>
  </tr>
  <tr>
   <td>Seguridad</td>
   <td><p>Se pueden usar varias opciones.</p> <p>Se propone un OAuth; puede configurarse de forma independiente de la configuración estándar.</p> </td>
   <td>Utiliza la configuración estándar de AEM.</td>
  </tr>
  <tr>
   <td>Observaciones arquitectónicas</td>
   <td><p>El acceso de escritura generalmente se dirige a una instancia de autor.</p> <p>La lectura también puede dirigirse a una instancia de publicación.</p> </td>
   <td>Dado que este enfoque es de solo lectura, se utilizará generalmente para instancias de publicación.</td>
  </tr>
  <tr>
   <td>Salida</td>
   <td>Salida SIREN basada en JSON: verboso, pero poderoso. Permite desplazarse dentro del contenido.</td>
   <td>la producción propia basada en JSON; configurable mediante modelos Sling. La navegación por la estructura de contenido es difícil de implementar (pero no necesariamente imposible).</td>
  </tr>
 </tbody>
</table>

### Seguridad {#security}

Si la API REST de Assets se utiliza en un entorno sin requisitos de autenticación específicos, el filtro CORS de AEM debe configurarse correctamente.

>[!NOTE]
>
>Para obtener más información, consulte:
>
>* [Se explica CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
>* [Vídeo: Desarrollo para CORS con AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
>



En entornos con requisitos de autenticación específicos, se recomienda OAuth.

## Funciones disponibles {#available-features}

Los fragmentos de contenido son un tipo específico de recurso; consulte [Uso de fragmentos](/help/assets/content-fragments.md)de contenido.

Para obtener más información sobre las funciones disponibles a través de la API, consulte:

* [Características](/help/assets/mac-api-assets.md#available-features) disponibles de la API REST de Assets
* [Tipos de entidades](/help/assets/assets-api-content-fragments.md#entity-types)

### Paginación {#paging}

La API de REST de Recursos admite paginación (para solicitudes GET) mediante parámetros de URL:

* `offset` - el número de la primera entidad (secundaria) que se va a recuperar
* `limit` - el número máximo de entidades devueltas

La respuesta contendrá información de paginación como parte de la `properties` sección de salida SIREN. Esta `srn:paging` propiedad contiene el número total de entidades (secundarias) ( `total`), el desplazamiento y el límite ( `offset`, `limit`) según se especifica en la solicitud.

>[!NOTE]
>
>La paginación se suele aplicar a entidades contenedores (es decir, carpetas o recursos con representaciones), ya que está relacionada con los elementos secundarios de la entidad solicitada.

#### Ejemplo:Paginación {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## Tipos de entidades {#entity-types}

### Carpetas {#folders}

Las carpetas actúan como contenedores de recursos y otras carpetas. Reflejan la estructura del repositorio de contenido de AEM.

La API de REST de Recursos expone el acceso a las propiedades de una carpeta; por ejemplo su nombre, título, etc. Los recursos se exponen como entidades secundarias de carpetas.

>[!NOTE]
>
>Según el tipo de recurso, la lista de entidades secundarias puede contener ya el conjunto completo de propiedades que define la entidad secundaria correspondiente. Otra posibilidad es que solo se pueda exponer un conjunto reducido de propiedades para una entidad de esta lista de entidades secundarias.

### Recursos {#assets}

Si se solicita un recurso, la respuesta devolverá sus metadatos; como título, nombre y otra información según la definición del esquema de recursos correspondiente.

Los datos binarios de un recurso se exponen como un vínculo SIREN de tipo `content` (también conocido como el `rel attribute`).

Los recursos pueden tener varias representaciones. Normalmente se exponen como entidades secundarias, con una excepción una representación en miniatura, que se expone como un vínculo de tipo `thumbnail` ( `rel="thumbnail"`).

### Fragmentos de contenido {#content-fragments}

Un fragmento [de](/help/assets/content-fragments.md) contenido es un tipo especial de recurso. Pueden utilizarse para acceder a datos estructurados, como textos, números, fechas, entre otros.

Dado que existen varias diferencias con los recursos *estándar* (como imágenes o audio), se aplican algunas reglas adicionales para su gestión.

#### Representación {#representation}

Fragmentos de contenido:

* No exponer ningún dato binario.
* Están completamente contenidos en la salida JSON (dentro de la `properties` propiedad).

* También se consideran atómicos, es decir, los elementos y las variaciones se exponen como parte de las propiedades del fragmento frente a como vínculos o entidades secundarias. Esto permite un acceso eficaz a la carga útil de un fragmento.

#### Modelos de contenido y fragmentos de contenido {#content-models-and-content-fragments}

Actualmente, los modelos que definen la estructura de un fragmento de contenido no se exponen a través de una API HTTP. Por lo tanto, el *consumidor* debe conocer el modelo de un fragmento (al menos un mínimo), aunque la mayor parte de la información puede inferirse de la carga útil; como tipos de datos, etc. forman parte de la definición.

Para crear un nuevo fragmento de contenido, se debe proporcionar la ruta (repositorio interno).

#### Contenido asociado {#associated-content}

El contenido asociado no está expuesto actualmente.

## Utilizando {#using}

El uso puede variar en función de si utiliza un entorno de publicación o de creación de AEM, junto con el caso de uso específico.

* La creación está estrictamente enlazada a una instancia de autor ([y actualmente no hay forma de replicar un fragmento para publicar con esta API](/help/assets/assets-api-content-fragments.md#limitations)).
* La entrega es posible desde ambos, ya que AEM ofrece contenido solicitado únicamente en formato JSON.

   * El almacenamiento y la entrega desde una instancia de autor de AEM deben ser suficientes para las aplicaciones de biblioteca multimedia que se encuentran detrás del servidor de seguridad.
   * Para la publicación web en directo, se recomienda una instancia de publicación de AEM.

>[!CAUTION]
>
>La configuración del despachante en las instancias de nube de AEM podría bloquear el acceso a `/api`.

>[!NOTE]
>
>Para obtener más información, consulte la Referencia [de API](/help/assets/assets-api-content-fragments.md#api-reference). En concreto, [Adobe Experience Manager Assets API - Fragmentos](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)de contenido.

### Lectura/Entrega {#read-delivery}

El uso se realiza mediante:

`GET /{cfParentPath}/{cfName}.json`

Por ejemplo:

`https://localhost:4502/api/assets/we-retail/en/experiences/arctic-surfing-in-lofoten.json`

La respuesta se serializa con JSON con el contenido estructurado como en el fragmento de contenido. Las referencias se entregan como direcciones URL de referencia.

Se pueden realizar dos tipos de operaciones de lectura:

* Al leer un fragmento de contenido específico por ruta, se devuelve la representación JSON del fragmento de contenido.
* Lectura de una carpeta de fragmentos de contenido por ruta: esto devuelve las representaciones JSON de todos los fragmentos de contenido de la carpeta.

### Crear {#create}

El uso se realiza mediante:

`POST /{cfParentPath}/{cfName}`

El cuerpo debe contener una representación JSON del fragmento de contenido que se va a crear, incluido el contenido inicial que se debe establecer en los elementos del fragmento de contenido. Es obligatorio establecer la `cq:model` propiedad y debe apuntar a un modelo de fragmento de contenido válido. Si no lo hace, se producirá un error. También es necesario agregar un encabezado `Content-Type` que esté establecido en `application/json`.

### Actualizar {#update}

El uso se realiza mediante

`PUT /{cfParentPath}/{cfName}`

El cuerpo debe contener una representación JSON de lo que se debe actualizar para el fragmento de contenido determinado.

Puede ser simplemente el título o la descripción de un fragmento de contenido, o un solo elemento, o todos los valores o metadatos del elemento. También es obligatorio proporcionar una propiedad válida `cq:model` para las actualizaciones.

### Eliminar {#delete}

El uso se realiza mediante:

`DELETE /{cfParentPath}/{cfName}`

## Restricciones {#limitations}

Existen algunas limitaciones:

* **Las variaciones no se pueden escribir ni actualizar.** Si estas variaciones se agregan a una carga útil (por ejemplo, para actualizaciones), se ignorarán. Sin embargo, la variación se enviará mediante entrega ( `GET`).

* **Actualmente no se admiten** los modelos de fragmentos de contenido: no se pueden leer ni crear. Para poder crear un fragmento de contenido nuevo o actualizar uno existente, los desarrolladores deben conocer la ruta correcta al modelo de fragmento de contenido. Actualmente, el único método para obtener una descripción general de estos es a través de la interfaz de usuario de administración.
* **Las referencias se omiten**. Actualmente no hay comprobaciones para comprobar si se hace referencia a un fragmento de contenido existente. Por lo tanto, por ejemplo, la eliminación de un fragmento de contenido podría provocar problemas en una página que contenga una referencia.

## Códigos de estado y mensajes de error {#status-codes-and-error-messages}

Los siguientes códigos de estado se pueden ver en las circunstancias pertinentes:

1. 202 (Aceptar)

   Se devuelve cuando:

   * solicitud de un fragmento de contenido mediante `GET`

   * actualización satisfactoria de un fragmento de contenido mediante `PUT`

1. 201 (Creación)

   Se devuelve cuando:

   * crear correctamente un fragmento de contenido mediante `POST`

1. 404 (No encontrado)

   Se devuelve cuando:

   * el fragmento de contenido solicitado no existe

1. 500 (error interno del servidor)

   >[!NOTE]
   >
   >Se devuelve este error:
   >
   >
   >
   >    * cuando se produce un error que no se puede identificar con un código específico
   >    * cuando la carga útil dada no era válida


   A continuación se enumeran los escenarios comunes cuando se devuelve este estado de error, junto con el mensaje de error (monospace) generado:

   * La carpeta principal no existe (al crear un fragmento de contenido mediante `POST`)
   * No se proporciona ningún modelo de fragmento de contenido (valor nulo), el recurso es nulo (posiblemente un problema de permisos) o el recurso no es una plantilla de fragmento válida:

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`
      * `Cannot adapt the resource '/foo/bar/qux' to a content fragment template`
   * No se pudo crear el fragmento de contenido (posiblemente sea un problema de permisos):

      * `Could not create content fragment`
   * No se pudo actualizar el título ni la descripción:

      * `Could not set value on content fragment`
   * No se pudieron establecer los metadatos:

      * `Could not set metadata on content fragment`
   * No se encontró el elemento de contenido o no se pudo actualizar

      * `Could not update content element`
      * `Could not update fragment data of element`
   Los mensajes de error detallados suelen devolverse de la siguiente manera:

   ```xml
   {
     "class": "core/response",
     "properties": {
       "path": "/api/assets/foo/bar/qux",
       "location": "/api/assets/foo/bar/qux.json",
       "parentLocation": "/api/assets/foo/bar.json",
       "status.code": 500,
       "status.message": "...{error message}.."
     }
   }
   ```

## API Reference {#api-reference}

Consulte aquí las referencias de API detalladas:

* [API de recursos de Adobe Experience Manager: fragmentos de contenido](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)
* [API HTTP de recursos](/help/assets/mac-api-assets.md)

   * [Funciones disponibles](/help/assets/mac-api-assets.md#available-features)

## Additional Resources {#additional-resources}

Para obtener más información, consulte:

* [Documentación de la API HTTP de Assets](/help/assets/mac-api-assets.md)
* [Sesión de AEM Gem: OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)

