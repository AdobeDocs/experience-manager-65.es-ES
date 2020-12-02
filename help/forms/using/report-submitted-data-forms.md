---
title: API para trabajar con formularios enviados en el portal de formularios
seo-title: API para trabajar con formularios enviados en el portal de formularios
description: AEM Forms proporciona API que se pueden usar para realizar consultas y acciones en los datos de formularios enviados en el portal de formularios.
seo-description: AEM Forms proporciona API que se pueden usar para realizar consultas y acciones en los datos de formularios enviados en el portal de formularios.
uuid: c47c8392-e5a9-4c40-b65e-4a7f379a6b45
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish, developer-reference
discoiquuid: 9457effd-3595-452f-a976-ad9eda6dc909
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 7%

---


# API para trabajar con formularios enviados en el portal de formularios {#apis-to-work-with-submitted-forms-on-forms-portal}

AEM Forms proporciona API que puede utilizar para la consulta de datos de formularios enviados a través del portal de formularios. Además, puede publicar comentarios o actualizar las propiedades de los formularios enviados mediante las API explicadas en este documento.

>[!NOTE]
>
>Los usuarios que invoquen las API deben agregarse al grupo de revisores como se describe en [Asociación de revisores de envío a un formulario](/help/forms/using/adding-reviewers-form.md).

## GET /content/forms/portal/submission.review.json?func=getFormsForSubmissionReview {#get-content-forms-portal-submission-review-json-func-getformsforsubmissionreview-br}

Devuelve una lista de todos los formularios elegibles.

### Parámetros de URL {#url-parameters}

Esta API no requiere parámetros adicionales.

### Respuesta {#response}

El objeto response contiene una matriz JSON que incluye nombres de formularios y su ruta de repositorio. La estructura de la respuesta es la siguiente:

```json
[
 {formName: "<form name>",
 formPath: "<path to the form>" },
 {.....},
 ......]
```

### Ejemplo {#example}

**URL de solicitud**

```http
https://[host]:[port]/content/forms/portal/submission.review.json?func=getFormsForSubmissionReview
```

**Respuesta**

```json
[{"formPath":"/content/dam/formsanddocuments/forms-review/form2","formName":"form2"},{"formPath":"/content/dam/formsanddocuments/forms-review/form1","formName":"form1"}]
```

## GET /content/forms/portal/submission.review.json?func=getAllSubsions {#get-content-forms-portal-submission-review-json-func-getallsubmissions}

Devuelve detalles de todos los formularios enviados. Sin embargo, puede utilizar parámetros de URL para limitar los resultados.

### Parámetros de URL {#url-parameters-1}

Especifique los siguientes parámetros en la dirección URL de la solicitud:

<table>
 <tbody>
  <tr>
   <th>Parámetro</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>formPath</code></td>
   <td>Especifica la ruta del repositorio de CRX donde reside el formulario. Si no especifica la ruta del formulario, devuelve una respuesta vacía.<br /> </td>
  </tr>
  <tr>
   <td><code>offset</code> (opcional)</td>
   <td>Especifica el punto inicial en el índice del conjunto de resultados. El valor predeterminado es <strong>0</strong>.</td>
  </tr>
  <tr>
   <td><code>limit</code> (opcional)</td>
   <td>Limita el número de resultados. El valor predeterminado es <strong>30</strong>.</td>
  </tr>
  <tr>
   <td><code>orderby</code> <br /> (opcional)</td>
   <td>Especifica la propiedad para ordenar los resultados. El valor predeterminado es <strong>jcr:lastModified</strong>, que ordena los resultados en función de la última vez que se modificó.</td>
  </tr>
  <tr>
   <td><code>sort</code> <br /> (opcional)</td>
   <td>Especifica el orden para ordenar los resultados. El valor predeterminado es <strong>desc</strong>, que ordena los resultados en orden descendente. Puede especificar <code>asc</code> para ordenar los resultados en orden ascendente.</td>
  </tr>
  <tr>
   <td><code>cutPoints</code> <br /> (opcional)</td>
   <td>Especifica una lista separada por comas de las propiedades del formulario que se incluirán en los resultados. Las propiedades predeterminadas son:<br /> <code>formName</code>, <code>formPath</code>, <code>submitID</code>, <code>formType</code>, <code>jcr:lastModified</code>, <code>owner</code></td>
  </tr>
  <tr>
   <td><code>search</code> <br /> (opcional)</td>
   <td>Busca el valor especificado en las propiedades del formulario y devuelve formularios con valores coincidentes. El valor predeterminado es <strong>""</strong>.</td>
  </tr>
 </tbody>
</table>

### Respuesta {#response-1}

El objeto response contiene una matriz JSON que incluye detalles de los formularios especificados. La estructura de la respuesta es la siguiente:

```json
{
 total: "<total number of submissions>",
 items: [{ formName: "<name of the form>", formPath: "<path to the form>", owner: "<owner of the form>"},
 ....]}
```

### Ejemplo {#example-1}

**URL de solicitud**

```http
https://[host]:[port]/content/forms/portal/submission.review.json?func=getAllSubmissions&formPath=/content/dam/formsanddocuments/forms-review/form2
```

**Respuesta**

```json
{"total":1,"items":[{"formName":"form2","formPath":"/content/dam/formsanddocuments/forms-review/form2","submitID":"1403037413508500","formType":"af","jcr:lastModified":"2015-11-05T17:52:32.243+05:30","owner":"admin"}]}
```

## POST /content/forms/portal/submission.review.json?func=addComment {#post-content-forms-portal-submission-review-json-func-addcomment-br}

Añade un comentario en la instancia de envío especificada.

### Parámetros de URL {#url-parameters-2}

Especifique los siguientes parámetros en la dirección URL de la solicitud:

| Parámetro | Descripción |
|---|---|
| `submitID` | Especifica el ID de metadatos asociado a una instancia de envío. |
| `Comment` | Especifica el texto que se va a agregar al comentario a la instancia de envío especificada. |

### Respuesta {#response-2}

Devuelve un ID de comentario al publicar correctamente un comentario.

### Ejemplo {#example-2}

**URL de solicitud**

```http
https://[host:'port'/content/forms/portal/submission.review.json?func=addComment&submitID=1403037413508500&comment=API+test+comment
```

**Respuesta**

```java
1403873422601300
```

## GET /content/forms/portal/submission.review.json?func=getComments   {#get-content-forms-portal-submission-review-json-func-getcomments-nbsp}

Devuelve todos los comentarios publicados en la instancia de envío especificada.

### Parámetros de URL {#url-parameters-3}

Especifique el siguiente parámetro en la dirección URL de la solicitud:

| Parámetro | Descripción |
|---|---|
| `submitID` | Especifica el ID de metadatos de una instancia de envío. |

### Respuesta {#response-3}

El objeto response contiene una matriz JSON que incluye todos los comentarios asociados al ID de envío especificado. La estructura de la respuesta es la siguiente:

```json
[{
 owner: "<name of the commenter>",
 comment: "<comment text>",
 time: "<time when the comment was posted>"},
 { }......]
```

### Ejemplo {#example-3}

**URL de solicitud**

```http
https://[host]:'port'/content/forms/portal/submission.review.json?func=getComments&submitID=1403037413508500
```

**Respuesta**

```java
[{"owner":"fr1","comment":"API test comment","time":1446726988250}]
```

## POST /content/forms/portal/submission.review.json?func=updateSubmission {#post-content-forms-portal-submission-review-json-func-updatesubmission-br}

Actualiza el valor de la propiedad especificada de la instancia de formulario enviada especificada.

### Parámetros de URL {#url-parameters-4}

Especifique los siguientes parámetros en la dirección URL de la solicitud:

| Parámetro | Descripción |
|---|---|
| `submitID` | Especifica el ID de metadatos asociado a una instancia de envío. |
| `property` | Especifica la propiedad de formulario que se va a actualizar. |
| `value` | Especifica el valor de la propiedad de formulario que se va a actualizar. |

### Respuesta {#response-4}

Devuelve un objeto JSON con información sobre la actualización publicada.

### Ejemplo {#example-4}

**URL de solicitud**

```http
https://[host]:'port'/content/forms/portal/submission.review.json?func=updateSubmission&submitID=1403037413508500&value=sample_value&property=some_new_prop
```

**Respuesta**

```json
{"formName":"form2","owner":"admin","jcr:lastModified":1446727516593,"path":"/content/forms/fp/admin/submit/metadata/1403037413508500.html","submitID":"1403037413508500","status":"submitted"}
```

