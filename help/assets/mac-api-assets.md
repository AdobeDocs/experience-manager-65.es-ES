---
title: "[!DNL Assets] API HTTP."
description: Cree, lea, actualice, elimine y administre recursos digitales mediante la API HTTP en [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Developer
feature: APIs,Assets HTTP API,Developer Tools
exl-id: 6bc10f4e-a951-49ba-9c71-f568a7f2e40d
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 2%

---

# [!DNL Assets] API HTTP {#assets-http-api}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets.html?lang=en) |
| AEM 6.5 | Este artículo |
| AEM 6.4 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/extending/mac-api-assets.html?lang=en) |

## Información general {#overview}

El [!DNL Assets] La API HTTP permite realizar operaciones de creación, lectura, actualización y eliminación (CRUD) en recursos digitales, incluidos metadatos, representaciones y comentarios, así como contenido estructurado mediante [!DNL Experience Manager] Fragmentos de contenido. Se expone en `/api/assets` y se implementa como API de REST. Incluye [compatibilidad con fragmentos de contenido](/help/assets/assets-api-content-fragments.md).

Para acceder a la API:

1. Abra el documento de servicio de API en `https://[hostname]:[port]/api.json`.
1. Siga las [!DNL Assets] vínculo de servicio que lleva a `https://[hostname]:[server]/api/assets.json`.

La respuesta de la API es un archivo JSON para algunos tipos de MIME y un código de respuesta para todos los tipos de MIME. La respuesta JSON es opcional y es posible que no esté disponible, por ejemplo, para archivos de PDF. Confíe en el código de respuesta para realizar más análisis o acciones.

Después del [!UICONTROL Tiempo de inactividad], un recurso y sus representaciones no están disponibles a través del [!DNL Assets] y a través de la API HTTP. La API devuelve el mensaje de error 404 si la variable [!UICONTROL Tiempo de activación] es en el futuro o [!UICONTROL Tiempo de inactividad] está en el pasado.

>[!CAUTION]
>
>[La API HTTP actualiza las propiedades de metadatos](#update-asset-metadata) en el `jcr` namespace. Sin embargo, la interfaz de usuario del Experience Manager actualiza las propiedades de metadatos en la `dc` namespace.

## Fragmentos de contenido {#content-fragments}

A [fragmento de contenido](/help/assets/content-fragments/content-fragments.md) es un tipo especial de recurso. Se puede utilizar para acceder a datos estructurados, como textos, números, fechas, entre otros. Dado que existen varias diferencias con `standard` recursos (como imágenes o documentos), algunas reglas adicionales se aplican a la gestión de fragmentos de contenido.

Para obtener más información, consulte [Compatibilidad con fragmentos de contenido en la API HTTP de Experience Manager Assets](/help/assets/assets-api-content-fragments.md).

## modelo Data {#data-model}

El [!DNL Assets] La API HTTP expone dos elementos principales, carpetas y recursos (para recursos estándar).

Además, expone elementos más detallados para los modelos de datos personalizados que describen el contenido estructurado en Fragmentos de contenido. Consulte [Modelos de datos de fragmentos de contenido](/help/assets/assets-api-content-fragments.md#content-fragments) para obtener más información.

### Carpetas {#folders}

Las carpetas son como los directorios de los sistemas de archivos tradicionales. Son contenedores para otras carpetas o aserciones. Las carpetas tienen los siguientes componentes:

**Entidades**: las entidades de una carpeta son sus elementos secundarios, que pueden ser carpetas y recursos.

**Propiedades**:

* `name` es el nombre de la carpeta. Es igual que el último segmento de la ruta URL sin la extensión.
* `title` es un título opcional de la carpeta que se puede mostrar en lugar de su nombre.

>[!NOTE]
>
>Algunas propiedades de la carpeta o el recurso se asignan a un prefijo diferente. El `jcr` prefijo de `jcr:title`, `jcr:description`, y `jcr:language` se han reemplazado por `dc` prefijo. Por lo tanto, en el JSON devuelto, `dc:title` y `dc:description` contiene los valores de `jcr:title` y `jcr:description`, respectivamente.

**Vínculos** Las carpetas muestran tres vínculos:

* `self`: vínculo a sí mismo.
* `parent`: vínculo a la carpeta principal.
* `thumbnail`: (Opcional) vínculo a una imagen en miniatura de la carpeta.

### Assets {#assets}

En Experience Manager, un recurso contiene los siguientes elementos:

* Las propiedades y los metadatos del recurso.
* Varias representaciones, como la representación original (que es el recurso cargado originalmente), una miniatura y varias otras representaciones. Las representaciones adicionales pueden ser imágenes de diferentes tamaños, codificaciones de vídeo diferentes o páginas extraídas del PDF o [!DNL Adobe InDesign] archivos.
* Comentarios opcionales.

Para obtener información sobre los elementos de los fragmentos de contenido, consulte [Compatibilidad con fragmentos de contenido en la API HTTP de Experience Manager Assets](/help/assets/assets-api-content-fragments.md#content-fragments).

Entrada [!DNL Experience Manager] una carpeta tiene los siguientes componentes:

* Entidades: las representaciones secundarias de los recursos.
* Propiedades.
* Vínculos.

El [!DNL Assets] La API HTTP incluye las siguientes funciones:

* [Recuperar una lista de carpetas](#retrieve-a-folder-listing).
* [Crear una carpeta](#create-a-folder).
* [Crear un recurso](#create-an-asset).
* [Actualizar binario de recursos](#update-asset-binary).
* [Actualizar metadatos del recurso](#update-asset-metadata).
* [Crear una representación de recursos](#create-an-asset-rendition).
* [Actualizar una representación de recursos](#update-an-asset-rendition).
* [Crear un comentario de recurso](#create-an-asset-comment).
* [Copiar una carpeta o un recurso](#copy-a-folder-or-asset).
* [Mover una carpeta o un recurso](#move-a-folder-or-asset).
* [Eliminar una carpeta, un recurso o una representación](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>Para facilitar la legibilidad, los siguientes ejemplos omiten la notación cURL completa. De hecho, la notación no se correlaciona con [Resty](https://github.com/micha/resty) que es un contenedor de scripts para `cURL`.

**Requisitos previos**

* Acceso `https://[aem_server]:[port]/system/console/configMgr`.
* Vaya a **[!UICONTROL Adobe Granite CSRF Filter]**.
* Asegúrese de que la propiedad **[!UICONTROL Métodos de filtro]** incluye: `POST`, `PUT`, `DELETE`.

## Recuperar una lista de carpetas {#retrieve-a-folder-listing}

Recupera una representación de sirena de una carpeta existente y de sus entidades secundarias (subcarpetas o recursos).

**Solicitud**: `GET /api/assets/myFolder.json`

**Códigos de respuesta**: Los códigos de respuesta son:

* 200 - OK - success.
* 404 - NO ENCONTRADO: la carpeta no existe o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

**Respuesta**: la clase de la entidad devuelta es un recurso o una carpeta. Las propiedades de las entidades contenidas son un subconjunto del conjunto completo de propiedades de cada entidad. Para obtener una representación completa de la entidad, los clientes deben recuperar el contenido de la dirección URL a la que apunta el vínculo con una `rel` de `self`.

## Crear una carpeta. {#create-a-folder}

Crea un nuevo `sling`: `OrderedFolder` en la ruta determinada. Si un `*` se proporciona en lugar de un nombre de nodo, el servlet utiliza el nombre del parámetro como nombre de nodo. Se acepta como datos de solicitud una representación de sirena de la nueva carpeta o un conjunto de pares de nombre-valor, codificados como `application/www-form-urlencoded` o `multipart`/ `form`- `data`, útil para crear una carpeta directamente desde un formulario de HTML. Además, las propiedades de la carpeta se pueden especificar como parámetros de consulta de URL.

Una llamada de API falla con un `500` código de respuesta si el nodo principal de la ruta proporcionada no existe. Una llamada a devuelve un código de respuesta `409` si la carpeta ya existe.

**Parámetros**: `name` es el nombre de la carpeta.

**Solicitar**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"jcr:title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"jcr:title=My Folder"`

**Códigos de respuesta**: Los códigos de respuesta son:

* 201 - CREADO: sobre creación correcta.
* 409 - CONFLICTO - si la carpeta ya existe.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Crear un recurso {#create-an-asset}

Coloque el archivo proporcionado en la ruta proporcionada para crear un recurso en el repositorio de DAM. Si un `*` se proporciona en lugar de un nombre de nodo, el servlet utiliza el nombre de parámetro o el nombre de archivo como nombre de nodo.

**Parámetros**: los parámetros son `name` para el nombre del recurso y `file` para la referencia de archivo.

**Solicitar**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**Códigos de respuesta**: Los códigos de respuesta son:

* 201: CREADO: si el recurso se ha creado correctamente.
* 409 - CONFLICTO - si el activo ya existe.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Actualizar un binario de recursos {#update-asset-binary}

Actualiza el archivo binario de un recurso (representación con el nombre original). Una actualización déclencheur el flujo de trabajo de procesamiento de recursos predeterminado que se ejecutará, si está configurado.

**Solicitud**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**Códigos de respuesta**: Los códigos de respuesta son:

* 200 - Correcto - si el recurso se ha actualizado correctamente.
* 404 - NO ENCONTRADO: si no se pudo encontrar el recurso o no se pudo acceder a él en el URI proporcionado.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Actualizar metadatos del recurso {#update-asset-metadata}

Actualiza las propiedades de los metadatos del recurso. Si actualiza cualquier propiedad en la variable `dc:` , la API actualiza la misma propiedad en el `jcr` namespace. La API no sincroniza las propiedades en las dos áreas de nombres.

**Solicitud**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"jcr:title":"My Asset"}}'`

**Códigos de respuesta**: Los códigos de respuesta son:

* 200 - Correcto - si el recurso se ha actualizado correctamente.
* 404 - NO ENCONTRADO: si no se pudo encontrar el recurso o no se pudo acceder a él en el URI proporcionado.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

### Sincronizar actualización de metadatos entre `dc` y `jcr` namespace {#sync-metadata-between-namespaces}

El método de API actualiza las propiedades de metadatos en la variable `jcr` namespace. Las actualizaciones realizadas mediante la interfaz de usuario de cambian las propiedades de los metadatos en la `dc` namespace. Para sincronizar los valores de metadatos entre `dc` y `jcr` , puede crear un flujo de trabajo y configurar un Experience Manager para ejecutar el flujo de trabajo tras la edición del recurso. Utilice un script ECMA para sincronizar las propiedades de metadatos requeridas. El siguiente script de ejemplo sincroniza la cadena de título entre `dc:title` y `jcr:title`.

```javascript
var workflowData = workItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH")
{
 var path = workflowData.getPayload().toString();
 var node = workflowSession.getSession().getItem(path);
 var metadataNode = node.getNode("jcr:content/metadata");
 var jcrcontentNode = node.getNode("jcr:content");
if (jcrcontentNode.hasProperty("jcr:title"))
{
 var jcrTitle = jcrcontentNode.getProperty("jcr:title");
 metadataNode.setProperty("dc:title", jcrTitle.toString());
 metadataNode.save();
}
}
```

## Crear una representación de recursos {#create-an-asset-rendition}

Crear una nueva representación de recursos para un recurso. Si no se proporciona el nombre del parámetro de solicitud, se utilizará el nombre de archivo como nombre de representación.

**Parámetros**: los parámetros son `name` para el nombre de la representación y `file` como referencia de archivo.

**Solicitar**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Códigos de respuesta**: Los códigos de respuesta son:

* 201: CREADO: si la representación se ha creado correctamente.
* 404 - NO ENCONTRADO: si no se pudo encontrar el recurso o no se pudo acceder a él en el URI proporcionado.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Actualizar una representación de recursos {#update-an-asset-rendition}

Las actualizaciones reemplazan respectivamente una representación de recursos con los nuevos datos binarios.

**Solicitud**: `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Códigos de respuesta**: Los códigos de respuesta son:

* 200 - Correcto - si la representación se ha actualizado correctamente.
* 404 - NO ENCONTRADO: si no se pudo encontrar el recurso o no se pudo acceder a él en el URI proporcionado.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Agregar un comentario en un recurso {#create-an-asset-comment}

Crea un nuevo comentario de recurso.

**Parámetros**: los parámetros son `message` para el cuerpo del mensaje del comentario y `annotationData` para los datos de anotación en formato JSON.

**Solicitud**: `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Códigos de respuesta**: Los códigos de respuesta son:

* 201: CREADO: si el comentario se ha creado correctamente.
* 404 - NO ENCONTRADO: si no se pudo encontrar el recurso o no se pudo acceder a él en el URI proporcionado.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Copiar una carpeta o un recurso {#copy-a-folder-or-asset}

Copia una carpeta o un recurso disponible en la ruta proporcionada a un nuevo destino.

**Encabezados de solicitud**: Los parámetros son:

* `X-Destination` : un nuevo URI de destino dentro del ámbito de la solución API en el que copiar el recurso.
* `X-Depth` - bien `infinity` o `0`. Uso de `0` solo copia el recurso y sus propiedades y no sus elementos secundarios.
* `X-Overwrite` - Uso `F` para evitar sobrescribir un recurso en el destino existente.

**Solicitud**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Códigos de respuesta**: Los códigos de respuesta son:

* 201: CREADO: si la carpeta o el recurso se ha copiado en un destino no existente.
* 204 - SIN CONTENIDO: si la carpeta/recurso se ha copiado a un destino existente.
* 412 - ERROR DE PRECONDICIÓN: si falta un encabezado de solicitud.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Mover una carpeta o un recurso {#move-a-folder-or-asset}

Mueve una carpeta o un recurso en la ruta determinada a un nuevo destino.

**Encabezados de solicitud**: Los parámetros son:

* `X-Destination` : un nuevo URI de destino dentro del ámbito de la solución API en el que copiar el recurso.
* `X-Depth` - bien `infinity` o `0`. Uso de `0` solo copia el recurso y sus propiedades y no sus elementos secundarios.
* `X-Overwrite` - Utilice una de estas opciones `T` para forzar la eliminación de recursos existentes o `F` para evitar sobrescribir un recurso existente.

**Solicitud**: `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

No use `/content/dam` en la dirección URL. Un comando de ejemplo para mover recursos y sobrescribir los existentes es el siguiente:

```shell
curl -u admin:admin -X MOVE https://[aem_server]:[port]/api/assets/source/file.png -H "X-Destination: https://[aem_server]:[port]/api/assets/destination/file.png" -H "X-Overwrite: T"
```

**Códigos de respuesta**: Los códigos de respuesta son:

* 201: CREADO: si la carpeta o el recurso se ha copiado en un destino no existente.
* 204 - SIN CONTENIDO: si la carpeta/recurso se ha copiado a un destino existente.
* 412 - ERROR DE PRECONDICIÓN: si falta un encabezado de solicitud.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Eliminar una carpeta, un recurso o una representación {#delete-a-folder-asset-or-rendition}

Elimina un recurso (-tree) en la ruta proporcionada.

**Solicitar**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**Códigos de respuesta**: Los códigos de respuesta son:

* 200 - Aceptar - si la carpeta se ha eliminado correctamente.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Sugerencias y limitaciones {#tips-best-practices-limitations}

* [La API HTTP actualiza las propiedades de metadatos](#update-asset-metadata) en el `jcr` namespace. Sin embargo, la interfaz de usuario del Experience Manager actualiza las propiedades de metadatos en la `dc` namespace.

* La API HTTP de Assets no devuelve los metadatos completos. Las áreas de nombres están codificadas y solo se devuelven esas áreas de nombres. Para ver los metadatos completos, consulte la ruta del recurso `/jcr_content/metadata.json`.
