---
title: Compatibilidad con fragmentos de contenido de Adobe Experience Manager en la API HTTP de Assets
description: AEM Obtenga información acerca de la compatibilidad con fragmentos de contenido en la API HTTP de Assets, una parte importante de la función de envío sin encabezado de la aplicación de la interfaz de usuario de.
feature: Content Fragments,Assets HTTP API
exl-id: 0f9efb47-a8d1-46d9-b3ff-a6c0741ca138
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1957'
ht-degree: 24%

---

# Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets {#content-fragments-support-in-aem-assets-http-api}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/assets-api-content-fragments.html?lang=es) |
| AEM 6.5 | Este artículo |


## Información general {#overview}

AEM Obtenga información acerca de la compatibilidad con fragmentos de contenido en la API HTTP de Assets, una parte importante de la función de envío sin encabezado de la aplicación de la interfaz de usuario de.

>[!NOTE]
>
>El [API HTTP de Assets](/help/assets/mac-api-assets.md) incluye:
>
>* La API de REST de Recursos
>* incluye compatibilidad con los fragmentos de contenido
>
>La implementación actual de la API HTTP de Assets se basa en la variable [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) estilo arquitectónico.

El [API de REST de Assets](/help/assets/mac-api-assets.md) permite a los desarrolladores de Adobe Experience Manager AEM acceder al contenido (almacenado en la) directamente a través de la API HTTP, a través de operaciones CRUD (crear, leer, actualizar, eliminar).

La API de le permite utilizar Adobe Experience Manager como un CMS (sistema de administración de contenido) sin encabezado proporcionando servicios de contenido a una aplicación front-end de JavaScript. O cualquier otra aplicación que pueda ejecutar solicitudes HTTP y gestionar respuestas JSON.

SPA Por ejemplo, las aplicaciones de una sola página (), basadas en un marco de trabajo o personalizadas, requieren contenido proporcionado mediante la API HTTP, a menudo en formato JSON.

While [AEM Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) AEM AEM proporcionan una API muy completa, flexible y personalizable que puede servir las operaciones de lectura necesarias para este fin y cuya salida JSON se puede personalizar, requieren conocimientos técnicos de WCM (gestión de contenido web) de la implementación, ya que deben alojarse en páginas basadas en plantillas dedicadas a la. SPA No todas las organizaciones de desarrollo de la tienen acceso directo a esos conocimientos.

Es entonces cuando se puede utilizar la API de REST de Assets. Permite a los desarrolladores acceder a recursos (por ejemplo, imágenes y fragmentos de contenido) directamente, sin necesidad de incrustarlos primero en una página, y enviar su contenido en formato JSON serializado.

>[!NOTE]
>
>No es posible personalizar la salida JSON desde la API de REST de Assets.

La API de REST de Assets también permite a los desarrolladores modificar contenido: creando nuevos recursos, fragmentos de contenido y carpetas, actualizándolos o eliminándolos.

La API de REST de Assets:

* sigue al [Principio HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)

* implementa el [Formato de SIRENA](https://github.com/kevinswiber/siren)

## Requisitos previos {#prerequisites}

AEM La API de REST de Assets está disponible en cada instalación predeterminada de una versión reciente de un paquete de instalación de la versión de la aplicación de la versión de la aplicación de la aplicación de forma predeterminada.

## Conceptos clave {#key-concepts}

Las ofertas de API de REST de Assets [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)AEM Acceso de tipo a a recursos almacenados en una instancia de.

Utiliza el `/api/assets` punto final y requiere la ruta del recurso para acceder a él (sin el interlineado `/content/dam`).

* Esto significa que para acceder al recurso en:
   * `/content/dam/path/to/asset`
* Debe solicitar:
   * `/api/assets/path/to/asset`

Por ejemplo, para acceder a `/content/dam/wknd/en/adventures/cycling-tuscany`, solicite `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>Acceso:
>
>* `/api/assets` **no** necesita el uso del selector `.model`.
>* `/content/path/to/page` **sí** necesita el uso del selector `.model`.


El método HTTP determina la operación que se va a ejecutar:

* **GET**: recuperar una representación JSON de un recurso o una carpeta.
* **POST**: crear nuevos recursos o carpetas.
* **PUT**: actualizar las propiedades de un recurso o carpeta.
* **DELETE**: eliminar un recurso o carpeta.

>[!NOTE]
>
>El cuerpo de solicitud o los parámetros de URL se pueden usar para configurar algunas de estas operaciones; por ejemplo, definir que una carpeta o un recurso deben crearse mediante una solicitud **POST**.

El formato exacto de las solicitudes admitidas se define en la variable [Referencia de API](/help/assets/assets-api-content-fragments.md#api-reference) documentación.

### Comportamiento transaccional {#transactional-behavior}

Todas las solicitudes son atómicas.

Esto significa que los siguientes (`write`) las solicitudes no se pueden combinar en una sola transacción que podría realizarse correctamente o fallar como una sola entidad.

### AEM AEM API de REST de (Assets) frente a componentes de {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>Aspecto</td>
   <td>La API de REST de Recursos<br/> </td>
   <td>AEM Componente<br/> (componentes que utilizan modelos Sling)</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Casos de uso admitidos</td>
   <td>De uso general.</td>
   <td><p>SPA Optimizado para el consumo en una aplicación de una sola página () o en cualquier otro contexto (consumo de contenido).</p> <p>También puede contener información de diseño.</p> </td>
  </tr>
  <tr>
   <td>Operaciones compatibles</td>
   <td><p>Crear, leer, actualizar, eliminar.</p> <p>Con operaciones adicionales en función del tipo de entidad.</p> </td>
   <td>Solo lectura.</td>
  </tr>
  <tr>
   <td>Acceso</td>
   <td><p>Se puede acceder directamente.</p> <p>Utiliza el <code>/api/assets </code>extremo, asignado a <code>/content/dam</code> (en el repositorio).</p> 
   <p>Una ruta de ejemplo tendría este aspecto: <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>AEM AEM Es necesario hacer referencia a él a través de un componente de la en una página de la aplicación.</p> <p>Utiliza el <code>.model</code> para crear la representación JSON.</p> <p>Una ruta de ejemplo tendría este aspecto:<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>Seguridad</td>
   <td><p>Se pueden seleccionar varias opciones.</p> <p>Se propone OAuth; se puede configurar por separado de la configuración estándar.</p> </td>
   <td>AEM Utiliza la configuración estándar.</td>
  </tr>
  <tr>
   <td>Observaciones arquitectónicas</td>
   <td><p>El acceso de escritura normalmente se dirige a una instancia de autor.</p> <p>La lectura también se puede dirigir a una instancia de publicación.</p> </td>
   <td>Como este método es de solo lectura, normalmente se utiliza para instancias de publicación.</td>
  </tr>
  <tr>
   <td>Salida</td>
   <td>Salida SIREN basada en JSON: detallada, pero potente. Permite la navegación dentro del contenido.</td>
   <td>Salida propia basada en JSON; configurable mediante modelos Sling. La navegación por la estructura de contenido es difícil de implementar (pero no necesariamente imposible).</td>
  </tr>
 </tbody>
</table>

### Seguridad {#security}

AEM Si la API de REST de Assets se utiliza en un entorno sin requisitos de autenticación específicos, es necesario configurar correctamente el filtro CORS de manera que se pueda usar en cualquier momento.

>[!NOTE]
>
>Para obtener más información, consulte lo siguiente:
>
>* [Explicación de CORS/AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)
>* [Vídeo: Desarrollo para CORS con AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html)
>


En entornos con requisitos de autenticación específicos, se recomienda OAuth.

## Funciones disponibles {#available-features}

Los fragmentos de contenido son un tipo específico de recurso. Consulte [Uso de fragmentos de contenido](/help/assets/content-fragments/content-fragments.md).

Para obtener más información sobre las funciones disponibles a través de la API, consulte:

* El [API de REST de Assets](/help/assets/mac-api-assets.md)
* [Tipos de entidad](/help/assets/assets-api-content-fragments.md#entity-types), donde se explican las funciones específicas de cada tipo admitido (según corresponda a los fragmentos de contenido)

### Paginación {#paging}

La API de REST de Assets admite la paginación (para solicitudes de GET) mediante los parámetros de URL:

* `offset` : el número de la primera entidad (secundaria) que se va a recuperar.
* `limit` : el número máximo de entidades devueltas

La respuesta contendrá información de paginación como parte de `properties` de la salida SIREN. Esta `srn:paging` contiene el número total de entidades (secundarias) ( `total`), el desplazamiento y el límite ( `offset`, `limit`) tal como se especifica en la solicitud.

>[!NOTE]
>
>La paginación se aplica normalmente a entidades contenedoras (es decir, carpetas o recursos con representaciones), en lo que se refiere a los elementos secundarios de la entidad solicitada.

#### Ejemplo: Paginación {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
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

## Tipos de entidad {#entity-types}

### Carpetas {#folders}

Las carpetas actúan como contenedores para recursos y otras carpetas. AEM Reflejan la estructura del repositorio de contenido de la.

La API de REST de Assets expone el acceso a las propiedades de una carpeta; por ejemplo, su nombre, título, etc. Los recursos se exponen como entidades secundarias de carpetas y subcarpetas.

>[!NOTE]
>
>Según el tipo de recurso de los recursos y carpetas secundarios, la lista de entidades secundarias puede contener ya el conjunto completo de propiedades que define la entidad secundaria correspondiente. Alternativamente, solo se puede exponer un conjunto reducido de propiedades para una entidad de esta lista de entidades secundarias.

### Assets {#assets}

Si se solicita un recurso, la respuesta devolverá sus metadatos, como título, nombre y otra información definida por el esquema de recursos respectivo.

Los datos binarios de un recurso se exponen como un vínculo SIREN de tipo `content`.

Los recursos pueden tener varias representaciones. Normalmente se exponen como entidades secundarias, una excepción es una representación en miniatura, que se expone como un vínculo de tipo `thumbnail` ( `rel="thumbnail"`).

### Fragmentos de contenido {#content-fragments}

A [fragmento de contenido](/help/assets/content-fragments/content-fragments.md) es un tipo especial de recurso. Pueden utilizarse para acceder a datos estructurados, como textos, números, fechas, entre otros.

Dado que existen varias diferencias con *standard* recursos (como imágenes o audio), se aplican algunas reglas adicionales para administrarlos.

#### Representación {#representation}

Fragmentos de contenido:

* No exponga ningún dato binario.
* Están completamente contenidos en la salida JSON (dentro de la variable `properties` property).

* También se consideran atómicos, es decir, los elementos y las variaciones se exponen como parte de las propiedades del fragmento en lugar de como vínculos o entidades secundarias. Esto permite un acceso eficiente a la carga útil de un fragmento.

#### Modelos de contenido y fragmentos de contenido {#content-models-and-content-fragments}

Actualmente, los modelos que definen la estructura de un fragmento de contenido no se exponen a través de una API HTTP. Por lo tanto, *consumidor* necesita conocer el modelo de un fragmento (al menos un mínimo), aunque la mayoría de la información se puede inferir de la carga útil, como tipos de datos, etc. forman parte de la definición de.

Para crear un nuevo fragmento de contenido, se debe proporcionar la ruta (repositorio interno) del modelo.

#### Contenido asociado {#associated-content}

El contenido asociado no está expuesto actualmente.

## Utilización {#using}

El uso puede variar en función de si utiliza un entorno de publicación o autor de AEM, junto con el caso de uso específico.

* Se recomienda que la creación esté enlazada a una instancia de autor ([y actualmente no hay medios para replicar un fragmento para publicarlo con esta API](/help/assets/assets-api-content-fragments.md#limitations)).
* La entrega es posible desde ambos, ya que AEM sirve contenido solicitado solo en formato JSON.

   * El almacenamiento y el envío desde una instancia de autor de AEM deben ser suficientes para las aplicaciones de la biblioteca de medios, detrás del cortafuegos.

   * Para la entrega web activa, se recomienda una instancia de publicación de AEM.

>[!CAUTION]
>
>AEM La configuración de Dispatcher en instancias de puede bloquear el acceso a `/api`.

>[!NOTE]
>
>Para obtener más información, consulte la [Referencia de API](/help/assets/assets-api-content-fragments.md#api-reference). En particular, la [API de Adobe Experience Manager Assets: fragmentos de contenido](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html).

### Lectura/entrega {#read-delivery}

El uso se realiza mediante:

`GET /{cfParentPath}/{cfName}.json`

Por ejemplo:

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

La respuesta es un archivo JSON serializado con el contenido estructurado como en el fragmento de contenido. Las referencias se envían como direcciones URL de referencia.

Se pueden realizar dos tipos de operaciones de lectura:

* Al leer un fragmento de contenido específico por la ruta, se devuelve la representación JSON del fragmento de contenido.
* Lectura de una carpeta de fragmentos de contenido por la ruta: se devuelven las representaciones JSON de todos los fragmentos de contenido de la carpeta.

### Crear {#create}

El uso se realiza mediante:

`POST /{cfParentPath}/{cfName}`

El cuerpo debe contener una representación JSON del fragmento de contenido que se va a crear, incluido cualquier contenido inicial que se deba establecer en los elementos del fragmento de contenido. Es obligatorio establecer la propiedad `cq:model` y debe señalar a un modelo de fragmento de contenido válido. Si no lo hace, se producirá un error. También es necesario añadir el encabezado `Content-Type` que se establece en `application/json`.

### Actualizar {#update}

El uso se realiza mediante

`PUT /{cfParentPath}/{cfName}`

El cuerpo debe contener una representación JSON de lo que se debe actualizar para el fragmento de contenido determinado.

Puede ser simplemente el título o la descripción de un fragmento de contenido, o un solo elemento, o todos los valores de elementos o metadatos.

### Eliminar {#delete}

El uso se realiza mediante:

`DELETE /{cfParentPath}/{cfName}`

## Restricciones {#limitations}

Hay algunas limitaciones:

* **Actualmente no se admiten modelos de fragmento de contenido**: no se pueden leer ni crear. Para poder crear un fragmento de contenido nuevo o actualizar uno existente, los desarrolladores deben conocer la ruta correcta al modelo de fragmento de contenido. Actualmente, el único método para obtener una descripción general de estos es a través de la IU de administración.
* **Las referencias se omiten**. Actualmente no hay comprobaciones sobre si se hace referencia a un fragmento de contenido existente. Por lo tanto, por ejemplo, si elimina un fragmento de contenido, podrían producirse problemas en una página que contenga una referencia al fragmento de contenido eliminado.
* **Tipo de datos JSON** La salida de la API de REST del *Tipo de datos JSON* es actualmente *salida basada en cadenas*.

## Códigos de estado y mensajes de error {#status-codes-and-error-messages}

Los siguientes códigos de estado se pueden ver en las circunstancias relevantes:

* **200** (OK) Devuelto cuando:

   * solicitud de un fragmento de contenido mediante `GET`
   * actualización correcta de un fragmento de contenido mediante `PUT`

* **201** (Creado) Devuelto cuando:

   * creación correcta de un fragmento de contenido mediante `POST`

* **404** (No encontrado) Devuelto cuando:

   * el fragmento de contenido solicitado no existe

* **500** (Error interno del servidor)

   >[!NOTE]
   >
   >Se devuelve este error:
   >
   >* cuando se ha producido un error que no se puede identificar con un código específico
   >* cuando la carga útil proporcionada no era válida


   A continuación se enumeran los escenarios comunes en los que se devuelve este estado de error, junto con el mensaje de error (monoespacio) generado:

   * La carpeta principal no existe (al crear un fragmento de contenido mediante `POST`)
   * No se ha proporcionado ningún modelo de fragmento de contenido (falta cq:model), no se puede leer (debido a una ruta no válida o a un problema de permisos) o no hay ningún modelo de fragmento válido:

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`
   * No se ha podido crear el fragmento de contenido (potencialmente un problema de permisos):

      * `Could not create content fragment`
   * No se han podido actualizar el título o la descripción:

      * `Could not set value on content fragment`
   * No se pudieron establecer los metadatos:

      * `Could not set metadata on content fragment`
   * El elemento de contenido no se ha podido encontrar o actualizar

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

## Referencia de la API {#api-reference}

Consulte aquí las referencias detalladas de la API:

* [API de Adobe Experience Manager Assets: fragmentos de contenido](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)
* [API HTTP de Recursos](/help/assets/mac-api-assets.md)

   * [Funciones disponibles](/help/assets/mac-api-assets.md#assets)

## Recursos adicionales {#additional-resources}

Para obtener más información, consulte lo siguiente:

* [Documentación de la API HTTP de Assets](/help/assets/mac-api-assets.md)
* [AEM Sesión de Gem de: OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)
