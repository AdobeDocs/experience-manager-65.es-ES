---
title: API para acceder a instancias de letras
seo-title: API para acceder a instancias de letras
description: Aprenda a utilizar las API para acceder a las instancias de letras.
seo-description: Aprenda a utilizar las API para acceder a las instancias de letras.
uuid: e7fb7798-f49d-458f-87f5-22df5f3e7d10
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9c27f976-972a-4250-b56d-b84a7d72f8c8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---


# API para acceder a instancias de carta {#apis-to-access-letter-instances}

## Información general {#overview}

Mediante la interfaz de usuario Crear correspondencia de la administración de correspondencia, puede guardar borradores de instancias de cartas en curso y se envían instancias de cartas.

Correspondence Management le proporciona API que permiten crear la interfaz de listado para trabajar con las instancias de cartas enviadas o los borradores. La lista de API y las instancias de carta de borrador y envío abiertas de un agente, de modo que el agente pueda continuar trabajando en las instancias de carta de borrador o envío.

## Obteniendo instancias de letras {#fetching-letter-instances}

Correspondence Management expone a las API a recuperar instancias de letras a través del servicio LetterInstanceService.

| Método | Descripción |
|--- |--- |
| getAllLetterInstances | Recoge instancias de letras basadas en el parámetro de consulta de entrada. Para recuperar todas las instancias de letras, pase el parámetro de consulta como nulo. |
| getLetterInstance | Recoge la instancia de letra especificada en función del identificador de instancia de letra. |
| letterInstanceExists | Comprueba si existe una instancia de carta por el nombre dado. |

>[!NOTE]
>
>LetterInstanceService es un servicio OSGI y su instancia se puede recuperar mediante @Reference en Java
>Class o sling.getService(LetterInstanceService. Clase ) en JSP.

### Uso de getAllLetterInstances {#using-nbsp-getallletterinstances}

La siguiente API busca las instancias de letras basadas en el objeto de consulta (tanto Enviada como Borrador). Si el objeto de consulta es nulo, devuelve todas las instancias de letras. Esta API devuelve la lista de [objetos LetterInstanceVO](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html), que se pueden utilizar para extraer información adicional de la instancia de letra

**Sintaxis**:  `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>Parámetro</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>query</td>
   <td>El parámetro de consulta se utiliza para buscar/filtrar la instancia de Letter. Aquí la consulta solo admite atributos/propiedades de nivel superior del objeto. La consulta consta de sentencias y "attributeName" utilizado en el objeto Statement debe ser el nombre de la propiedad en el objeto de instancia Letter.<br /> </td>
  </tr>
 </tbody>
</table>

#### Ejemplo 1: Buscar todas las instancias de letras de tipo ENVIADO {#example-fetch-all-the-letter-instances-of-type-submitted}

El siguiente código devuelve la lista de instancias de cartas enviadas. Para obtener solo borradores, cambie `LetterInstanceType.COMPLETE.name()` a `LetterInstanceType.DRAFT.name().`

```java
@Reference
LetterInstanceService letterInstanceService;
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

#### Ejemplo 2: Buscar todas las instancias de letras enviadas por un usuario y el tipo de instancia de letra es DRAFT {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

El siguiente código tiene varias afirmaciones en la misma consulta para que los resultados se filtren en función de diferentes criterios como la instancia de carta enviada (atributo enviado por) por un usuario y el tipo de letterInstanceType es DRAFT.

```java
@Reference
LetterInstanceService letterInstanceService;

String submittedBy = "tglodman";
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);

Statement statementForSubmittedBy = new Statement();
statementForSubmittedBy .setAttributeName("submittedby");
statementForSubmittedBy .setOperator(Operator.EQUALS);
statementForSubmittedBy .setAttributeValue(submittedBy);
query.addStatement(statementForSubmittedBy );
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

### Uso de getLetterInstance {#using-nbsp-getletterinstance}

Recupere la instancia de letra identificada por la identificación de instancia de letra dada. Devuelve &quot;null si no coincide la identificación de instancia.

**Sintaxis:** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### Comprobando si LetterInstance existe {#verifying-if-letterinstance-exist}

Comprobar si existe una instancia de carta con el nombre dado

**Sintaxis**:  `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **Parámetro** | **Descripción** |
|---|---|
| letterInstanceName | Nombre de la instancia de carta que desea comprobar si existe. |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## Abrir instancias de carta {#opening-letter-instances}

La instancia de carta puede ser del tipo Enviado o Borrador. La apertura de ambos tipos de instancias de letras muestra diferentes comportamientos:

* En el caso de la instancia de carta enviada, se abre un PDF que representa la instancia de carta. La instancia de carta enviada que persiste en el servidor también contiene el archivo dataXML y XDP procesado, que se puede utilizar para realizar y utilizar un caso personalizado como crear un archivo PDF/A.
* En el caso de la instancia de borrador de carta, la interfaz de usuario de creación de correspondencia se vuelve a cargar con el estado anterior exacto, tal como era durante el tiempo en que se creó el borrador

### Abrir instancia de letra borrador  {#opening-draft-letter-instance-nbsp}

La interfaz de usuario de CCR admite el parámetro cmLetterInstanceId, que se puede utilizar para volver a cargar la letra.

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>No es necesario especificar cmLetterId o cmLetterName/State/Version al volver a cargar una correspondencia, ya que los datos enviados ya contienen todos los detalles sobre la correspondencia que se recarga. RandomNo se utiliza para evitar problemas con la caché del navegador, puede utilizar la marca de tiempo como un número aleatorio.

### Abriendo instancia de carta enviada {#opening-submitted-letter-instance}

El PDF enviado se puede abrir directamente con el identificador de instancia de la carta:

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
