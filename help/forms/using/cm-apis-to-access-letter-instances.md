---
title: API para acceder a instancias de carta
seo-title: API para acceder a instancias de carta
description: Aprenda a utilizar las API para acceder a las instancias de carta.
seo-description: Aprenda a utilizar las API para acceder a las instancias de carta.
uuid: e7fb7798-f49d-458f-87f5-22df5f3e7d10
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9c27f976-972a-4250-b56d-b84a7d72f8c8
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# API para acceder a instancias de carta {#apis-to-access-letter-instances}

## Información general {#overview}

Mediante la IU Crear Correspondencia de Gestión de Correspondencia, puede guardar borradores de instancias de carta en curso y hay instancias de carta enviadas.

Correspondence Management proporciona API que permiten crear la interfaz de listado para trabajar con instancias de cartas enviadas o borradores. Las API enumeran y abren las instancias de carta en borrador y enviadas de un agente, de modo que el agente pueda seguir trabajando en las instancias de carta en borrador o enviadas.

## Recuperando instancias de letras {#fetching-letter-instances}

Correspondence Management expone las API para recuperar instancias de carta a través del servicio LetterInstanceService.

| Método | Descripción |
|--- |--- |
| getAllLetterInstances | Obtiene instancias de letras basadas en el parámetro de consulta de entrada. Para recuperar todas las instancias de letras, pase el parámetro de consulta como nulo. |
| getLetterInstance | Obtiene la instancia de letra especificada en función del ID de instancia de letra. |
| letterInstanceExists | Comprueba si existe una LetterInstance por el nombre dado. |

>[!NOTE]
>
>LetterInstanceService es un servicio OSGI y su instancia se puede recuperar mediante @Reference en Java
>Class o sling.getService(LetterInstanceService. Clase ) en JSP.

### Uso de getAllLetterInstances {#using-nbsp-getallletterinstances}

La siguiente API encuentra las instancias de la carta en función del objeto de consulta (tanto Enviado como Borrador). Si el objeto de consulta es nulo entonces, devuelve todas las instancias de letras. Esta API devuelve la lista de objetos [LetterInstanceVO](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html), que pueden utilizarse para extraer información adicional de la instancia de letra

**Sintaxis**:  `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>Parámetro</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>query</td>
   <td>El parámetro de consulta se utiliza para buscar/filtrar la instancia Carta. En este caso, la consulta solo admite atributos o propiedades de nivel superior del objeto. La consulta consiste en instrucciones y el "attributeName" utilizado en el objeto de instrucción debe ser el nombre de la propiedad en el objeto de instancia Letter.<br /> </td>
  </tr>
 </tbody>
</table>

#### Ejemplo 1: Recupere todas las instancias de letras del tipo ENVIADO {#example-fetch-all-the-letter-instances-of-type-submitted}

El siguiente código devuelve la lista de instancias de carta enviadas. Para obtener solo borradores, cambie `LetterInstanceType.COMPLETE.name()` a `LetterInstanceType.DRAFT.name().`

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

#### Ejemplo 2: Recuperación de todas las instancias de letras enviadas por un usuario y el tipo de instancia de letra es DRAFT {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

El siguiente código tiene varias instrucciones en la misma consulta para obtener los resultados filtrados según diferentes criterios, como la instancia de carta enviada (atributo enviado por) por un usuario y el tipo de letterInstanceType es DRAFT.

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

Recupere la instancia de carta identificada por el id. de instancia de letra dado. Devuelve &quot;null&quot; si no coincide el id de instancia.

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
| letterInstanceName | Nombre de la instancia de letra que desea comprobar si existe. |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## Apertura de instancias de carta {#opening-letter-instances}

La instancia de carta puede ser de tipo Enviado o Borrador. Al abrir ambos tipos de instancias de letras, se muestran diferentes comportamientos:

* En el caso de la instancia de carta enviada, se abre un PDF que representa la instancia de carta. La instancia de carta enviada que persiste en el servidor también contiene el dataXML y el XDP procesado, que se pueden utilizar para llevar a cabo y utilizar un caso personalizado como la creación de un PDF/A.
* En el caso de la instancia de letra borrador, la interfaz de usuario de creación de correspondencia se vuelve a cargar hasta el estado anterior, tal como estaba durante el momento en que se creó el borrador

### Abrir instancia de letra borrador  {#opening-draft-letter-instance-nbsp}

La interfaz de usuario de CCR admite el parámetro cmLetterInstanceId , que se puede utilizar para volver a cargar la carta.

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>No es necesario especificar cmLetterId o cmLetterName/State/Version al volver a cargar una correspondencia, ya que los datos enviados ya contienen todos los detalles sobre la correspondencia que se recarga. RandomNo se usa para evitar problemas con la caché del navegador, puede usar la marca de tiempo como un número aleatorio.

### Apertura de la instancia de carta enviada {#opening-submitted-letter-instance}

El PDF enviado se puede abrir directamente mediante el identificador de instancia de la letra:

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
