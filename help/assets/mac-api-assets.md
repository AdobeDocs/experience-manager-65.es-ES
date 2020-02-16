---
title: API HTTP de recursos
description: Obtenga información sobre la implementación, el modelo de datos y las características de la API HTTP de Assets. Utilice la API HTTP de Assets para realizar varias tareas en torno a los recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# API HTTP de recursos {#assets-http-api}

## Información general {#overview}

La API HTTP de recursos permite crear-leer-actualizar-eliminar (CRUD) operaciones en recursos, incluidos binarios, metadatos, representaciones y comentarios, junto con contenido estructurado mediante fragmentos de contenido de AEM. Se expone en `/api/assets` y se implementa como API de REST. Incluye [compatibilidad con fragmentos](/help/assets/assets-api-content-fragments.md)de contenido.

Para acceder a la API:

1. Abra el documento del servicio API en `https://[hostname]:[port]/api.json`.
1. Siga el vínculo del servicio Recursos que lleva a `https://[hostname]:[server]/api/assets.json`.

La respuesta de API es un archivo JSON para algunos tipos de MIME y un código de respuesta para todos los tipos de MIME. La respuesta JSON es opcional y puede que no esté disponible, por ejemplo, para archivos PDF. Confíe en el código de respuesta para realizar más análisis o acciones.

Después del tiempo de [!UICONTROL inactividad], un recurso y sus representaciones no están disponibles ni a través de la interfaz web de Recursos ni a través de la API HTTP. La API devuelve un mensaje de error 404 si [!UICONTROL Tiempo] de activación está en el futuro o Tiempo de [!UICONTROL desactivación] está en el pasado.

## Fragmentos de contenido {#content-fragments}

Un fragmento [de](/help/assets/content-fragments.md) contenido es un tipo especial de recurso. Puede utilizarse para acceder a datos estructurados, como textos, números, fechas, entre otros. Dado que hay varias diferencias con `standard` los recursos (como imágenes o documentos), algunas reglas adicionales se aplican a la gestión de fragmentos de contenido.

Para obtener más información, consulte Compatibilidad con fragmentos [de contenido en la API](/help/assets/assets-api-content-fragments.md)HTTP de AEM Assets.

## modelo Data {#data-model}

La API HTTP de Recursos expone dos elementos principales, carpetas y recursos (para recursos estándar).

Además, expone elementos más detallados para los modelos de datos personalizados que describen el contenido estructurado en fragmentos de contenido. Consulte Modelos [de datos de fragmento de contenido](/help/assets/assets-api-content-fragments.md#content-fragments) para obtener más información.

### Carpetas {#folders}

Las carpetas son como directorios en sistemas de archivos tradicionales. Son contenedores para otras carpetas o aserciones. Las carpetas tienen los siguientes componentes:

**Entidades**: Las entidades de una carpeta son sus elementos secundarios, que pueden ser carpetas y recursos.

**Propiedades**:
* `name`  — Nombre de la carpeta. Es lo mismo que el último segmento de la ruta URL sin la extensión
* `title` — Título opcional de la carpeta que se puede mostrar en lugar de su nombre

>[!NOTE]
>
>Algunas propiedades de carpeta o recurso se asignan a un prefijo diferente. El `jcr` prefijo `jcr:title`, `jcr:description`y `jcr:language` se reemplazan con `dc` prefijo. Por lo tanto, en el JSON devuelto `dc:title` y `dc:description` contener los valores de `jcr:title` y `jcr:description`, respectivamente.

**Las carpetas de vínculos** exponen tres vínculos:
* `self`:: Vínculo a sí mismo
* `parent`:: Vínculo a la carpeta principal
* `thumbnail`:: (Opcional) vínculo a una imagen en miniatura de la carpeta

### Recursos {#assets}

En AEM, los recursos contienen los siguientes elementos:

* Propiedades y metadatos del recurso
* Varias representaciones, como la representación original (que es el recurso cargado originalmente), una miniatura y otras representaciones. Las representaciones adicionales pueden ser imágenes de diferentes tamaños, codificaciones de vídeo diferentes o páginas extraídas de PDF o InDesign.
* Comentarios opcionales

Para obtener información sobre los elementos de los fragmentos de contenido, consulte Compatibilidad con fragmentos [de contenido en la API](/help/assets/assets-api-content-fragments.md#content-fragments)HTTP de Recursos AEM.

En AEM, una carpeta tiene los siguientes componentes:

* Entidades: Los elementos secundarios de Assets son sus representaciones.
* Propiedades
* Vínculos

La API HTTP de Assets incluye las siguientes funciones:

* Recuperar una lista de carpetas
* Crear una carpeta
* Crear un recurso
* Actualizar binario de recursos
* Actualización de metadatos de recursos
* Creación de una representación de recursos
* Actualización de una representación de recursos
* Creación de un comentario de recurso
* Copiar una carpeta o un recurso
* Mover una carpeta o un recurso
* Eliminación de una carpeta, recurso o representación

>[!NOTE]
>
>Para facilitar la lectura, en los siguientes ejemplos se omite la notación completa de cURL. De hecho, la notación sí se correlaciona con [Resty](https://github.com/micha/resty) , que es un contenedor de secuencias de comandos para `cURL`.

**Requisitos previos**

* Ir a `https://[aem_server]:[port]/system/console/configMgr`.
* Vaya al Filtro **CSRF de** Adobe Granite.
* Asegúrese de que la propiedad Métodos **de** filtro incluye: PUBLICAR, PUBLICAR, ELIMINAR.

## Recuperar una lista de carpetas {#retrieve-a-folder-listing}

Recupera una representación sirena de una carpeta existente y de sus entidades secundarias (subcarpetas o recursos).

**Solicitar**

```
GET /api/assets/myFolder.json
```

**Códigos de respuesta**

```
200 - OK - success
404 - NOT FOUND - folder does not exist or is not accessible
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

**Respuesta**

La clase de la entidad devuelta es assets/folder.

Las propiedades de las entidades contenidas son un subconjunto del conjunto completo de propiedades de cada entidad. Para obtener una representación completa de la entidad, los clientes deben recuperar el contenido de la URL señalada por el vínculo con un `rel` de `self`.

## Crear una carpeta {#create-a-folder}

Crea un nuevo `sling`: `OrderedFolder` en la ruta dada. Si se da un * en lugar de un nombre de nodo, el servlet utilizará el nombre del parámetro como nombre de nodo. Se acepta como datos de solicitud una representación sirena de la nueva carpeta o un conjunto de pares nombre-valor, codificados como `application/www-form-urlencoded` o `multipart`/ `form`- `data`, que resulta útil para crear una carpeta directamente desde un formulario HTML. Además, las propiedades de la carpeta se pueden especificar como parámetros de consulta de URL.

La operación fallará con un código de `500` respuesta si el nodo principal de la ruta dada no existe. Si la carpeta ya existe, se devuelve un código de `409` respuesta.

**Parámetros**

* `name` - Nombre de la carpeta

**Solicitar**

```
POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'
```

o

```
POST /api/assets/* -F"name=myfolder" -F"title=My Folder"
```

**Códigos de respuesta**

```
201 - CREATED - on successful creation
409 - CONFLICT - if folder already exist
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Crear un recurso {#create-an-asset}

Crea un recurso DAM en la ruta dada con el archivo dado. Si se da un * en lugar de un nombre de nodo, el servlet utilizará el nombre del parámetro o el nombre del archivo como nombre de nodo.

**Parámetros**

* `name` - Nombre del recurso
* `file` - Referencia de archivo

**Solicitar**

```
POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"
```

o

```
POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"
```

**Códigos de respuesta**

```
201 - CREATED - if Asset has been created successfully
409 - CONFLICT - if Asset already exist
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Actualizar binario de recursos {#update-asset-binary}

Actualiza un binario de Assets (representación con el nombre original). Esto activará el flujo de trabajo de recursos predeterminado si está configurado.

**Solicitar**

```
PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png
```

**Códigos de respuesta**

```
200 - OK - if Asset has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Actualización de metadatos de recursos {#update-asset-metadata}

Actualiza las propiedades de metadatos de recurso. Si actualiza cualquier propiedad del `dc:` espacio de nombres, la API actualiza la misma propiedad en el `jcr` espacio de nombres. La API no sincroniza las propiedades de los dos espacios de nombres.

**Solicitar**

```
PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'
```

**Códigos de respuesta**

```
200 - OK - if Asset has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Creación de una representación de recursos {#create-an-asset-rendition}

Crea una nueva representación de recursos para un recurso. Si no se proporciona el nombre del parámetro de solicitud, el nombre del archivo se utiliza como nombre de representación.

**Parámetros**

* `name` - Nombre de la representación
* `file` - Referencia de archivo

**Solicitar**

```
POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"
```

o

```
POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"
```

**Códigos de respuesta**

```
201 - CREATED - if Rendition has been created successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Actualizar una representación de recursos {#update-an-asset-rendition}

Las actualizaciones reemplazan respectivamente una representación de recursos con los nuevos datos binarios.

**Solicitar**

```
PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png
```

**Códigos de respuesta**

```
200 - OK - if Rendition has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Crear un comentario de recurso {#create-an-asset-comment}

Crea un nuevo comentario de recurso.

**Parámetros**

* `message` - Mensaje
* `annotationData` - Datos de anotación (JSON)

**Solicitar**

```
POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"
```

**Códigos de respuesta**

```
201 - CREATED - if Comment has been created successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Copiar una carpeta o un recurso {#copy-a-folder-or-asset}

Copia una carpeta o un recurso en la ruta dada a un nuevo destino.

**Encabezados de solicitud**

```
X-Destination - a new destination URI within the API solution scope to copy the resource to
X-Depth - either 'infinity' or '0'. The value '0' only copies the resource and its properties, no children.
X-Overwrite - 'F' to prevent overwriting an existing destination
```

**Solicitar**

```
COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"
```

**Códigos de respuesta**

```
201 - CREATED - if folder/asset has been copied to a non-existing destination
204 - NO CONTENT - if the folder/asset has been copied to an existing destination
412 - PRECONDITION FAILED - if a request header is missing or
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Mover una carpeta o un recurso {#move-a-folder-or-asset}

Mueve una carpeta o un recurso de la ruta dada a un nuevo destino.

**Encabezados de solicitud**

```
X-Destination - a new destination URI within the API solution scope to copy the resource to
X-Depth - either 'infinity' or '0'. The value '0' only copies the resource and its properties, no children.
X-Overwrite - either 'T' to force deletion of existing resources or 'F' to prevent overwriting an existing resource.
```

**Solicitar**

```
MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"
```

**Códigos de respuesta**

```
201 - CREATED - if folder/asset has been copied to a non-existing destination
204 - NO CONTENT - if the folder/asset has been copied to an existing destination
412 - PRECONDITION FAILED - if a request header is missing or
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Eliminar una carpeta, recurso o representación {#delete-a-folder-asset-or-rendition}

Elimina un recurso (-tree) en la ruta dada.

**Solicitar**

```
DELETE /api/assets/myFolder
```

o

```
DELETE /api/assets/myFolder/myAsset.png
```

o

```xml
DELETE /api/assets/myFolder/myAsset.png/renditions/original
```

**Códigos de respuesta**

```
200 - OK - if folder has been deleted successfully
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```
