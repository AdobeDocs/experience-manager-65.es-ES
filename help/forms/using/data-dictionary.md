---
title: Diccionario de datos
seo-title: Diccionario de datos
description: El diccionario de datos de la gestión de correspondencia le permite integrar datos back-end en letras como entradas para su uso en la correspondencia con los clientes.
seo-description: El diccionario de datos de la gestión de correspondencia le permite integrar datos back-end en letras como entradas para su uso en la correspondencia con los clientes.
uuid: 178a285e-b4a4-4a36-a2aa-b43ecb0871ed
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: a1a0ad6b-023a-4822-9cce-0618657c3f9d
docset: aem65
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3861'
ht-degree: 1%

---


# Diccionario de datos{#data-dictionary}

## Introducción {#introduction}

Un diccionario de datos permite a los usuarios empresariales utilizar información de fuentes de datos back-end sin conocer detalles técnicos sobre sus modelos de datos subyacentes. Un diccionario de datos está compuesto por elementos de diccionario de datos (DDE). Estos elementos de datos se utilizan para integrar datos del back-end en las cartas como entrada para su uso en una correspondencia de cliente.

Un diccionario de datos es una representación independiente de metadatos que describe estructuras de datos subyacentes y sus atributos asociados. Se crea un diccionario de datos con vocabulario empresarial. Se puede asignar a uno o más modelos de datos subyacentes.

El diccionario de datos está formado por elementos de tres tipos: Elementos simples, compuestos y de colección. Los DDE simples son elementos primitivos como cadenas, números, fechas y valores booleanos que contienen información como un nombre de ciudad. Un DDE compuesto contiene otros DDE, que pueden ser de tipo primitivo, compuesto o colección. Por ejemplo, una dirección que consta de una dirección de calle, ciudad, provincia, país y código postal. Una colección es una lista de DDE simples o compuestos similares. Por ejemplo, un cliente con varias ubicaciones o distintas direcciones de facturación y envío.

La gestión de correspondencia utiliza los datos del back end, del cliente o específicos del destinatario almacenados según la estructura del diccionario de datos para crear correspondencia destinada a diferentes clientes. Por ejemplo, se puede crear un documento con nombres descriptivos, como &quot;Estimado {Nombre}&quot;, &quot;Sr. {Apellidos}&quot;.

Normalmente, los usuarios empresariales no necesitan conocer las representaciones de metadatos, como XSD (esquema XML) y clases Java. Sin embargo, normalmente requieren acceso a estas estructuras y atributos de datos para crear soluciones.

### Flujo de trabajo del diccionario de datos {#data-dictionary-workflow}

1. Un autor [crea el diccionario de datos](#createdatadictionary) cargando un esquema o desde cero.
1. El Autor crea comunicaciones por carta e interactivas basadas en el diccionario de datos y asocia los elementos del diccionario de datos en comunicaciones por carta e interactivas siempre que sea necesario.
1. Un autor puede descargar un archivo XML de datos de ejemplo, que se basa en el esquema de un diccionario de datos. El autor puede modificar el archivo XML de datos de ejemplo, que puede asociarse como datos de prueba con el diccionario de datos. Lo mismo se utiliza durante la vista previa de la carta.
1. Mientras [se obtiene una vista previa de una carta](../../forms/using/create-letter.md#p-types-of-linkage-available-for-each-of-the-fields-p), un autor elige obtener una vista previa de la carta con datos (vista previa personalizada). La carta se abre previamente rellenada con los datos proporcionados por Author. Se abre en la interfaz de creación de correspondencia. El agente que está previsualizando esta carta puede modificar el contenido, los datos y los archivos adjuntos de esta carta y puede enviar la carta final. Para obtener más información sobre la creación de cartas, consulte [Creación de correspondencia](../../forms/using/create-letter.md).

## Requisitos previos {#prerequisite}

Instale el [Paquete de compatibilidad](compatibility-package.md) para ver la opción **Diccionarios de datos** en la página **Forms**.

## Crear un diccionario de datos {#createdatadictionary}

Puede usar el Editor de diccionario de datos para crear un diccionario de datos o cargar un archivo de esquema XSD para crear un diccionario de datos basado en él. A continuación, puede ampliar el diccionario de datos agregando más información necesaria, incluidos campos. Independientemente de cómo se haya creado el diccionario de datos, el propietario del proceso empresarial no necesita conocer los sistemas back-end. El propietario del proceso empresarial solo necesita conocer los objetos de dominio y sus definiciones para su proceso.

>[!NOTE]
>
>Para varias letras que requieran elementos similares, puede crear un diccionario de datos común. Sin embargo, un diccionario de datos grandes con un gran número de elementos puede provocar problemas de rendimiento al utilizar el diccionario de datos y cargar los elementos, como en letras y fragmentos de documento. Si tiene problemas de rendimiento, intente crear diccionarios de datos independientes para letras diferentes.

1. Seleccione **Forms** > **Diccionarios de datos**.
1. Toque **Crear diccionario de datos**.
1. En la pantalla Propiedades, agregue lo siguiente:

   * **Título:** (opcional) introduzca el título del diccionario de datos. El título no tiene que ser único y puede tener caracteres especiales y caracteres que no sean de inglés. Las letras y otros fragmentos de documento son referidos con su título (cuando están disponibles), como en miniaturas y propiedades de recursos. Se hace referencia a los diccionarios de datos con sus nombres y no títulos.
   * **Nombre:** el nombre exclusivo del diccionario de datos. En el campo Nombre, solo se pueden introducir caracteres, números y guiones en inglés. El campo Nombre se rellena automáticamente en función del campo Título y los caracteres especiales, espacios, números y caracteres que no sean de inglés introducidos en el campo Título se sustituyen por guiones. Aunque el valor del campo Título se copia automáticamente en el Nombre, puede editarlo.

   * **Descripción**: (Opcional) Descripción del diccionario de datos.
   * **Etiquetas:** (opcional) para crear una etiqueta personalizada, introduzca un valor en el campo de texto y pulse Intro. Puede ver la etiqueta debajo del campo de texto de las etiquetas. Al guardar este texto, también se crean las etiquetas recientemente agregadas.
   * **Propiedades** extendidas: (Opcional) Toque  **Agregar** campo para especificar atributos de metadatos para el diccionario de datos. En la columna Nombre de propiedad , introduzca un nombre de propiedad único. En la columna Value , introduzca un valor para asociarlo a la propiedad.

   ![Propiedades del diccionario de datos especificadas en alemán](do-not-localize/1_ddproperties.png)

1. (Opcional) Para cargar una definición de esquema XSD para el diccionario de datos, en el panel Estructura del diccionario de datos, pulse **Cargar esquema XML**. Vaya al archivo XSD, selecciónelo y pulse **Abrir**. Se crea un diccionario de datos en función del esquema XML cargado. Es necesario modificar los nombres para mostrar y las descripciones de los elementos en el diccionario de datos. Para ello, seleccione los nombres de los elementos tocándolos y editando sus descripciones, nombres para mostrar y otros detalles en los campos del panel derecho.

   Para obtener más información sobre los elementos de DD calculados, consulte [Elementos de diccionario de datos calculados](#computedddelements).

   >[!NOTE]
   >
   >Puede omitir la carga del archivo de esquema y crear el diccionario de datos desde cero mediante la interfaz de usuario. Para ello, omita este paso y continúe con los pasos siguientes.

1. Toque **Siguiente**.
1. En la pantalla Agregar propiedades , agregue los elementos al diccionario de datos. También puede añadir o eliminar elementos y editar sus detalles si ha cargado un esquema para obtener una estructura básica del diccionario de datos.

   Puede pulsar los tres puntos del lado derecho de un elemento y agregar un elemento a la estructura del diccionario de datos.

   ![1_2_createanelement](assets/1_2_createanelement.png)

   Seleccione Elemento compuesto, Elemento de colección o Elemento primitivo.

   * Un DDE compuesto contiene otros DDE, que pueden ser de tipo primitivo, compuesto o colección. Por ejemplo, una dirección que consta de una dirección de calle, ciudad, provincia, país y código postal.
   * Los DDE primitivos son elementos como cadenas, números, fechas y valores booleanos que contienen información como un nombre de ciudad.
   * Una colección es una lista de DDE simples o compuestos similares. Por ejemplo, un cliente con varias ubicaciones o distintas direcciones de facturación y envío.

   A continuación se indican algunas reglas para crear un diccionario de datos:

   * Solo se permite el tipo compuesto como DDE de nivel superior en un diccionario de datos.
   * Nombre, nombre de referencia y tipo de elemento son campos obligatorios para un diccionario de datos y DDE.
   * El nombre de referencia debe ser único.
   * Un DDE principal (compuesto) no puede tener dos elementos secundarios con el mismo nombre.
   * Los números solo contienen tipos de cadena primitivos.

   Para obtener más información sobre los elementos compuestos, de colección y primitivos y trabajar con elementos de diccionario de datos, consulte [Asignación de elementos de diccionario de datos al esquema XML](#mappingddetoschema).

   Para obtener información sobre las validaciones en el diccionario de datos, consulte [Validaciones del editor de diccionarios de datos](#ddvalidations).

   ![2_adddpropertiesbasic](assets/2_addddpropertiesbasic.png)

1. (Opcional) Después de seleccionar un elemento, en la pestaña Avanzado puede añadir propiedades (atributos). También puede pulsar **Agregar campo** y ampliar las propiedades de un elemento DD.

   ![3_adddpropertiesadvanced](assets/3_addddpropertiesadvanced.png)

1. (Opcional) Para eliminar cualquier elemento, toque los tres puntos a la derecha de un elemento y seleccione **Eliminar**.

   ![4_deleteelement](assets/4_deleteelement.png)

   >[!NOTE]
   >
   >Al eliminar un elemento compuesto/de colección con nodos secundarios, también se eliminan sus nodos secundarios.

1. (Opcional) Seleccione un elemento en el panel Estructura del diccionario de datos y en el panel Lista de campos y variables . Cambie o agregue cualquier atributo necesario asociado al elemento.
1. Toque **Guardar**.

### Crear copias de uno o más diccionario de datos {#create-copies-of-one-or-more-data-dictionary}

Para crear rápidamente uno o más diccionarios de datos con propiedades y elementos similares a diccionarios de datos existentes, puede copiarlos y pegarlos.

1. En la lista de diccionarios de datos, seleccione los diccionarios de datos correspondientes. La interfaz de usuario muestra el icono Copiar .
1. Pulse Copiar. La interfaz de usuario muestra el icono Pegar .
1. Pulse Pegar. Aparecerá el cuadro de diálogo Pegar. El sistema asigna automáticamente nombres y títulos a los nuevos diccionarios de datos.
1. Si es necesario, edite el Título y el Nombre con los que desea guardar la copia del diccionario de datos.
1. Pulse Pegar. Se crea la copia del diccionario de datos. Ahora puede realizar los cambios necesarios en el diccionario de datos recién creado.

## Consulte los fragmentos del documento o documentos que hacen referencia a un elemento de diccionario de datos {#see-the-document-fragments-or-documents-that-refer-to-a-data-dictionary-element}

Mientras edita o visualiza un diccionario de datos, puede ver qué elementos del diccionario de datos son referidos en qué textos, condiciones, letras y comunicaciones interactivas.

1. Realice una de las siguientes acciones para editar el diccionario de datos:

   * Pase el ratón sobre un diccionario de datos y pulse Editar.
   * Seleccione un diccionario de datos y, a continuación, pulse Editar en el encabezado.
   * Pase el ratón sobre un diccionario de datos y pulse Seleccionar. A continuación, pulse Editar en el encabezado.

   O toque un diccionario de datos para verlo.

1. En el diccionario de datos, pulse un elemento simple para seleccionarlo. Los elementos compuestos y de colección no tienen referencias.

   Junto con las propiedades Básicas y Avanzadas del elemento, también aparece Contenido de Cuarentena .

1. Puntee en Contenido de Cuarentena.

   La pestaña Contenido de la Cuaresma aparece con lo siguiente: Textos, condiciones, cartas y comunicaciones interactivas. Cada uno de estos encabezados también muestra el número de referencias al elemento seleccionado.

1. Pulse en un encabezado para ver el nombre de los recursos que hacen referencia al elemento.

   ![lentcontent](assets/lentcontent.png)

1. Para ver el contenido prestado de otro elemento, pulse el elemento .
1. Para mostrar un recurso que hace referencia al elemento, pulse su nombre. El navegador muestra el recurso, la carta o la comunicación interactiva.

## Trabajo con datos de prueba {#working-with-test-data}

1. En la página Diccionarios de datos , pulse **Seleccionar**.
1. Pulse un diccionario de datos para el que desee descargar datos de prueba y, a continuación, pulse **Descargar datos XML de ejemplo**.
1. Pulse **Aceptar** en el mensaje de alerta. Se descarga un archivo XML.
1. Abra el archivo XML con el Bloc de notas u otro editor XML. El archivo XML tiene la misma estructura que el diccionario de datos y las cadenas de marcador de posición de los elementos. Reemplace las cadenas de marcador de posición por los datos con los que desea probar una letra.

   ```xml
   <?xml version="1.0" encoding="UTF-8" standalone="no"?>
   <Company>
   <Name>string</Name>
   <Type>string</Type>
   <HeadOfficeAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </HeadOfficeAddress>
   <SalesOfficeAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </SalesOfficeAddress>
   <HeadCount>1.0</HeadCount>
   <CEO>
   <PersonName>
   <FirstName>string</FirstName>
   <MiddleName>string</MiddleName>
   <LastName>string</LastName>
   </PersonName>
   <DOB>string</DOB>
   <CurrAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </CurrAddress>
   <DOJ>14-04-1973</DOJ>
   <Phone>1.0</Phone>
   </CEO>
   </Company>
   ```

   >[!NOTE]
   >
   >En este ejemplo, XML crea espacio para tres valores en un elemento de colección, pero el número de valores se puede aumentar/reducir según sea necesario.

1. Después de realizar las entradas de datos, puede utilizar este archivo XML cuando esté previsualizando una carta con datos de prueba.

   Puede agregar estos datos de prueba con DD (seleccione DD y pulse Cargar datos de prueba y cargar este archivo xml)
Así que después de esto, cuando obtiene una vista previa de la carta normalmente (no personalizada), estos datos XML se utilizan en la carta. También puede pulsar Personalizado y, a continuación, cargar este XML.

## Ejemplos {#samples}

Los siguientes ejemplos de código muestran los detalles de implementación del diccionario de datos.

### Esquema de ejemplo que se puede cargar en el diccionario de datos {#sample-schema-that-can-be-uploaded-to-the-data-dictionary}

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema xmlns="DCT" targetNamespace="DCT" xmlns:xs="https://www.w3.org/2001/XMLSchema"
  elementFormDefault="qualified" attributeFormDefault="unqualified">
  <xs:element name="Company">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="Name" type="xs:string"/>
        <xs:element name="Type" type="xs:anySimpleType"/>
        <xs:element name="HeadOfficeAddress" type="Address"/>
        <xs:element name="SalesOfficeAddress" type="Address" minOccurs="0"/>
        <xs:element name="HeadCount" type="xs:integer"/>
        <xs:element name="CEO" type="Employee"/>
        <xs:element name="Workers" type="Employee" maxOccurs="unbounded"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
  <xs:complexType name="Employee">
    <xs:complexContent>
      <xs:extension  base="Person">
        <xs:sequence>
          <xs:element name="CurrAddress" type="Address"/>
          <xs:element name="DOJ" type="xs:date"/>
          <xs:element name="Phone" type="xs:integer"/>
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:complexType name="Person">
    <xs:sequence>
      <xs:element name="PersonName" type="Name"/>
      <xs:element name="DOB" type="xs:dateTime"/>
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Name">
    <xs:sequence>
      <xs:element name="FirstName" type="xs:string"/>
      <xs:element name="MiddleName" type="xs:string"/>
      <xs:element name="LastName" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Address">
    <xs:sequence>
      <xs:element name="Street" type="xs:string"/>
      <xs:element name="City" type="xs:string"/>
      <xs:element name="State" type="xs:string"/>
      <xs:element name="Zip" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
</xs:schema>
```

## Atributos comunes asociados a un DDE {#common-attributes-associated-with-a-dde}

La siguiente tabla detalla los atributos comunes asociados con un DDE:

<table>
 <tbody>
  <tr>
   <td><strong>Atributo</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Nombre</td>
   <td>Cadena</td>
   <td>Requerido.<br /> Nombre del DDE. Debe ser único.</td>
  </tr>
  <tr>
   <td>Nombre de referencia<br /></td>
   <td>Cadena</td>
   <td>Requerido. Nombre de referencia único para el DDE que permite referencias al DDE que son independientes de los cambios en la jerarquía o estructura del diccionario de datos. Los módulos de texto se asignan con este nombre</td>
  </tr>
  <tr>
   <td>displayname</td>
   <td>Cadena</td>
   <td>Un nombre opcional descriptivo del DDE.</td>
  </tr>
  <tr>
   <td>Descripción</td>
   <td>Cadena</td>
   <td>Descripción del DDE.</td>
  </tr>
  <tr>
   <td>elementType</td>
   <td>Cadena</td>
   <td>Requerido. Tipo de DDE: CADENA, NÚMERO, FECHA, Booleano, COMPUESTO, COLECCIÓN.</td>
  </tr>
  <tr>
   <td>elementSubType</td>
   <td>Cadena</td>
   <td>El subtipo para DDE: ENUM. Solo se permite para STRING y NUMBER elementType.</td>
  </tr>
  <tr>
   <td>Clave</td>
   <td>Booleano</td>
   <td>Campo booleano que indica si un DDE es un elemento clave.</td>
  </tr>
  <tr>
   <td>Calculado</td>
   <td>Booleano</td>
   <td>Campo booleano que indica si se calcula un DDE. Un valor DDE calculado es una función de otros valores DDE. De forma predeterminada, se admiten expresiones jsp.</td>
  </tr>
  <tr>
   <td>expression</td>
   <td>Cadena</td>
   <td>La expresión para el DDE "calculado". El servicio de evaluación de expresiones enviado de forma predeterminada admite expresiones JSP EL. Puede reemplazar el servicio de expresiones con una implementación personalizada.</td>
  </tr>
  <tr>
   <td>valueSet</td>
   <td>Lista</td>
   <td>Conjunto de valores permitidos para un DDE de tipo Enum. Por ejemplo, el tipo de cuenta solo puede tener valores (Guardar, Actual).</td>
  </tr>
  <tr>
   <td>ExtendedProperties</td>
   <td>Objeto</td>
   <td>Mapa de propiedades personalizadas agregadas al DDE (interfaz de usuario específica o cualquier otra información).</td>
  </tr>
  <tr>
   <td>Requerido</td>
   <td>Booleano</td>
   <td>El indicador indica que el origen de los datos de instancia correspondientes al diccionario de datos debe contener el valor de este DDE concreto.</td>
  </tr>
  <tr>
   <td>Enlace</td>
   <td>BindingElement</td>
   <td>Enlace XML o Java del elemento.</td>
  </tr>
 </tbody>
</table>

### Elementos de diccionario de datos calculados {#computedddelements}

Un diccionario de datos también puede incluir elementos calculados. Un elemento de diccionario de datos calculado siempre está asociado a una expresión. Esta expresión se evalúa para obtener el valor de un elemento de diccionario de datos durante la ejecución. Un valor DDE calculado es una función de otros valores o literales DDE. De forma predeterminada, se admiten las expresiones de lenguaje de expresión JSP (EL). Las expresiones EL utilizan los caracteres ${ } y las expresiones válidas pueden incluir literales, operadores, variables (referencias de elementos del diccionario de datos) y llamadas a funciones. Al hacer referencia a un elemento de diccionario de datos en la expresión, se utiliza el nombre de referencia del DDE. El nombre de referencia es único para cada elemento de diccionario de datos dentro de un diccionario de datos.

Se puede asociar un DDE PersonFullName calculado con una expresión de concatenación EL como ${PersonFirstName} ${PersonLastName}.

## Asignación de tipos de datos entre XSD y el diccionario de datos {#data-type-mapping-between-xsd-and-data-dictionary-br}

La exportación de un XSD requiere una asignación de datos específica, que se detalla en la siguiente tabla. La columna DDI indica el tipo del valor DDE disponible en el DDI.

<table>
 <tbody>
  <tr>
   <td>XSD <br /> </td>
   <td><p>Diccionario de datos <br /> </p> </td>
   <td>DDI (Tipo de datos de valor de instancia)<br /> </p> </td>
  </tr>
  <tr>
   <td><p>xs:element de tipo - Tipo compuesto<br /> </p> </td>
   <td>DDE de tipo COMPUESTO<br /> </p> </td>
   <td>java.util.Map<br /> </td>
  </tr>
  <tr>
   <td><p>xs:element donde maxOcurrs &gt; 1<br /> </p> </td>
   <td>DDE de tipo - COLLECTION-<br /> Se crea un nodo DDE junto al DDE de COLECCIÓN que captura información del nodo COLLECTION principal. Lo mismo se crea para ambas colecciones de tipos de datos simples/compuestos. Siempre que se tiene una COLECCIÓN del tipo compuesto, el árbol del diccionario de datos captura los campos constitutivos en los elementos secundarios del DDE creados para capturar información de tipo.<br /> - DDE (COLLECTION)<br />  - DDE(COMPOSITE for type info)<br />  - DDE(STRING) field1<br />  - DDE(STRING) field2<br /> <br /> </p> </td>
   <td>java.util.List<br /> </td>
  </tr>
  <tr>
   <td>Atributo de tipo - xs:id <br /> </p> </td>
   <td>DDE de tipo - CADENA <br /> </td>
   <td>java.lang.String<br /> </td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element de tipo - xs:string</p> </td>
   <td>DDE de tipo - STRING<br /> </td>
   <td>java.lang.String<br /> </td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element de tipo - xs: booleano <br /> </td>
   <td>DDE de tipo: booleano <br /> </td>
   <td>java.lang.Boolean<br /> </td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element de tipo - xs:date </td>
   <td>DDE de tipo - FECHA </td>
   <td>java.lang.String</td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element de tipo - xs:integer </td>
   <td>DDE de tipo - NUMBER </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element de tipo - xs:long</td>
   <td>DDE de tipo - NUMBER </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element de tipo - xs:double</td>
   <td>DDE de tipo - NUMBER </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>Elemento de tipo enum y baseType - xs:string</td>
   <td>DDE de tipo <br /> - Subtipo STRING<br /> - ENUM<br /> valueSet - los valores permitidos para ENUM<br /> </td>
   <td>java.lang.String</td>
  </tr>
 </tbody>
</table>

## Descargar un archivo de datos de ejemplo desde un diccionario de datos {#download-a-sample-data-file-from-a-data-dictionary}

Una vez creado un diccionario de datos, puede descargarlo como un archivo de datos de ejemplo XML para crear entradas de texto en él.

1. En la página Diccionarios de datos , pulse **Seleccionar** y, a continuación, pulse un diccionario de datos para seleccionarlo.
1. Seleccione **Descargar datos XML de ejemplo**.
1. Pulse **Aceptar** en el mensaje de alerta.

   Correspondence Management crea un archivo XML basado en la estructura del diccionario de datos seleccionado y lo descarga en su equipo con el nombre &lt;data-dictionary-name>-SampleData. Ahora puede editar este archivo en un editor de texto o XML para realizar entradas de datos mientras [crea una carta](../../forms/using/create-letter.md).

## Internacionalización de metadatos {#internationalization-of-meta-data}

Si desea enviar la misma carta en distintos idiomas a sus clientes, puede localizar los conjuntos de nombre para mostrar, descripción y valor de enumeración de los elementos del diccionario de datos y del diccionario de datos.

### Localizar diccionario de datos {#localize-data-dictionary}

1. En la página Diccionarios de datos , pulse **Seleccionar** y, a continuación, pulse un diccionario de datos para seleccionarlo.
1. Pulse **Descargar datos de localización**.
1. Pulse **Aceptar** en la alerta. Correspondence Management descarga un archivo zip en su equipo con el nombre DataDictionary-&lt;Dname>.zip.
1. El archivo zip contiene un archivo .properties . Este archivo define el diccionario de datos descargado. El contenido del archivo de propiedad es similar al siguiente:

   ```ini
   #Wed May 20 16:06:23 BST 2015
   DataDictionary.EmployeeDD.description=
   DataDictionary.EmployeeDD.displayName=EmployeeDataDictionary
   DataDictionaryElement.name.description=
   DataDictionaryElement.name.displayName=name
   DataDictionaryElement.person.description=
   DataDictionaryElement.person.displayName=person
   ```

   La estructura del archivo de propiedades define una línea para la descripción y el nombre para mostrar para el diccionario de datos y cada elemento del diccionario de datos en el diccionario de datos. Además, el archivo de propiedades define una línea para un valor de enumeración establecido para cada elemento del diccionario de datos. Al igual que con un diccionario de datos, el archivo de propiedades correspondiente puede tener varias definiciones de elementos de diccionario de datos. Además, el archivo puede contener las definiciones de uno o varios conjuntos de valores de enumeración.

1. Para actualizar el archivo .properties en una configuración regional diferente, actualice los valores de nombre para mostrar y descripción en el archivo . Cree más instancias del archivo para cada idioma en el que desee localizar. Solo se admiten los idiomas francés, alemán, japonés e inglés.

1. Guarde los diferentes archivos de propiedades actualizadas con los nombres siguientes:

   _fr_FR.properties Francés

   _de_DE.properties Alemán

   _ja_JA.properties Japonés

   _en_EN.properties Inglés

1. Archive el archivo .properties (o los archivos para varias configuraciones regionales) en un único archivo .zip.

1. En la página Diccionarios de datos , seleccione **Más** > **Cargar datos de localización** y seleccione el archivo zip con archivos de propiedades localizados.
1. Para ver los cambios de localización, cambie la configuración regional del explorador.

## Validaciones del diccionario de datos {#ddvalidations}

El Editor de diccionarios de datos aplica las siguientes validaciones al crear o actualizar un diccionario de datos.

* Solo se permite el tipo compuesto como elemento de nivel superior en un diccionario de datos.
* Los elementos compuestos y de colección no están permitidos a nivel de hoja. Solo se permiten elementos primitivos (cadena, fecha, número, booleano) en el nivel de hoja. Esta validación garantiza que no haya ningún elemento compuesto y de colección sin un DDE secundario.
* Cuando se carga un archivo XSD para crear un diccionario de datos, el Editor de diccionarios de datos solicita un elemento de nivel superior, si existen varios, para crear el diccionario de datos.
* El nombre es el único parámetro necesario para un diccionario de datos.
* Un DDE principal (compuesto) no puede tener dos elementos secundarios con el mismo nombre
* Garantiza que un DDE se marque como computado, solo si no es un parámetro requerido. No se puede calcular un elemento requerido y no se puede requerir un elemento calculado. Además, el elemento de colección y el elemento compuesto no pueden ser elementos calculados.
* Garantiza que se marque un DDE como obligatorio, solo cuando no se calcule. También garantiza que no sea el &quot;collectionElement&quot; el que indica el tipo de Collection (que es el único elemento secundario de un elemento de colección).
* Las claves vacías o Duplicate no están permitidas en ExtendedProperties para un diccionario de datos o DDE.
* No utilice los caracteres de dos puntos (:) o barra vertical (|) dentro de la clave o el valor de una propiedad extendida. No hay validación para el uso de estos caracteres prohibidos.

Validaciones aplicadas en el nivel del diccionario de datos

* El nombre del diccionario de datos no debe ser nulo.
* El nombre del diccionario de datos solo debe contener caracteres alfanuméricos.
* La lista de elementos secundarios del diccionario de datos no debe ser nula ni estar vacía.
* El diccionario de datos no debe contener más de un elemento del diccionario de datos de nivel superior.
* Solo se permite el tipo compuesto como elemento de nivel superior en un diccionario de datos.

Validaciones que se aplican en el nivel de elemento del diccionario de datos.

* Todos los nombres DDE no deben ser nulos y no deben contener espacios.
* Todos los DDE deben tener un tipo de elemento &quot;no nulo/no nulo&quot;.
* Todos los nombres de referencia de DDE no deben ser nulos.
* Todos los nombres de referencia de DDE deben ser únicos.
* Toda referencia de DDE solo debe contener caracteres alfanuméricos y &quot;_&quot;.
* Todos los nombres para mostrar DDE solo deben contener caracteres alfanuméricos y &quot;_&quot;.
* Los elementos compuestos y de colección no están permitidos a nivel de hoja. Solo se permiten elementos primitivos (cadena, fecha, número, booleano) en el nivel de hoja. Esta validación garantiza que no haya ningún elemento compuesto y de colección sin un DDE secundario.
* Un DDE principal compuesto no debe tener dos elementos secundarios con el mismo nombre.
* El subtipo ENUM solo se utiliza para los elementos String y Number .
* Los elementos de colección y compuestos no se pueden calcular.
* Un DDE no se puede calcular ni es necesario.
* Los DDE calculados deben contener una expresión válida.
* Los DDE calculados no deben tener enlaces XML.
* Un DDE que indica el tipo de un DDE de colección no se puede calcular ni es necesario.
* Los DDE de subtipo ENUM no deben contener conjuntos de valores nulos o vacíos.
* El enlace XML de un DDE de colección no debe asignarse a un atributo.
* La sintaxis de enlace XML debe ser válida, como, por ejemplo, solo aparece una @, sólo se permite la @ cuando va seguida de un nombre de atributo.

## Asignación de elementos del diccionario de datos al esquema XML {#mappingddetoschema}

Puede crear un diccionario de datos a partir de un esquema XML o crearlo mediante la interfaz de usuario del diccionario de datos. Todos los elementos del diccionario de datos (DDE) de un diccionario de datos tienen un campo de enlace XML para almacenar el enlace del DDE a un elemento del esquema XML. El enlace en cada DDE es relativo al DDE principal.

Los siguientes detalles incluyen ejemplos de modelos y ejemplos de código que muestran detalles de implementación para el diccionario de datos.

## Asignación de elementos simples (primitivos) {#mapping-simple-primitive-elements}

Un DDE primitivo representa un campo o atributo que es de naturaleza atómica. Los DDE primitivos definidos fuera del ámbito de un tipo complejo (DDE compuesto) o un elemento repetitivo (DDE de colección) se pueden almacenar en cualquier ubicación dentro del esquema XML. La ubicación de los datos correspondientes a un DDE primitivo no depende de la asignación de su DDE principal. El DDE primitivo utiliza la información de asignación del campo Enlace XML para determinar su valor y las asignaciones se traducen en uno de los siguientes:

* un atributo
* un elemento
* un contexto de texto
* nada (un DDE ignorado)

El siguiente ejemplo muestra un esquema simple.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="https://www.w3.org/2001/XMLSchema">
  <xs:element name='age' type='integer'/>
  <xs:element name='price' type='decimal'/>
</xs:schema>
```

| **Elemento Diccionario de datos** | **Enlace XML predeterminado** |
|---|---|
| age | /age |
| precio | /precio |

### Asignación de elementos compuestos {#mapping-composite-elements}

El enlace no es compatible con los elementos compuestos; si se proporciona el enlace, se ignora. El enlace para todos los DDE secundarios constituyentes de tipo primitivo debe ser absoluto. Al permitir la asignación absoluta para elementos secundarios de un DDE compuesto, se proporciona más flexibilidad en términos de enlace XPath. La asignación de un DDE compuesto a un elemento de tipo complejo en el esquema XML limita el ámbito de enlace para sus elementos secundarios.

El siguiente ejemplo muestra el esquema de una nota.

```xml
<xs:element name="note">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="to" type="xs:string"/>
            <xs:element name="from" type="xs:string"/>
            <xs:element name="heading" type="xs:string"/>
            <xs:element name="body" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:element>
```

<table>
 <tbody>
  <tr>
   <td><strong>Elemento Diccionario de datos</strong></td>
   <td><strong>Enlace XML predeterminado</strong></td>
  </tr>
  <tr>
   <td>nota</td>
   <td>empty(null)<br /> </td>
  </tr>
  <tr>
   <td>hasta</td>
   <td>/note/to</td>
  </tr>
  <tr>
   <td>de</td>
   <td>/note/from</td>
  </tr>
  <tr>
   <td>encabezado</td>
   <td>/nota/encabezado</td>
  </tr>
  <tr>
   <td>body</td>
   <td>/note/body</td>
  </tr>
 </tbody>
</table>

### Asignación de elementos de colección {#mapping-collection-elements}

Un elemento de colección solo está asignado a otro elemento de colección que tiene cardinalidad > 1. Los DDE secundarios de un DDE de colección tienen un enlace XML relativo (local) con respecto al enlace XML de su padre. Dado que los DDE secundarios de un elemento de colección deben tener la misma cardinalidad que la del elemento principal, el enlace relativo debe garantizar la restricción de cardinalidad para que los DDE secundarios no apunten a un elemento de esquema XML no repetitivo. En el siguiente ejemplo, la cardinalidad de &quot;TokenID&quot; debe ser la misma que &quot;Tokens&quot;, que es su DDE de recopilación principal.

Al asignar un DDE de colección a un elemento de esquema XML:

* el enlace para el DDE correspondiente al elemento Collection debe ser XPath absoluto

* No proporcione ningún enlace para el DDE que represente el tipo de elemento Collection . Si se proporciona, se ignorará el enlace.

* El enlace para todos los DDE secundarios del elemento Collection debe ser relativo al elemento Collection principal.

El esquema XML siguiente declara un elemento con el nombre Tokens y un atributo maxOccurs de &quot;ilimitado&quot;. Por lo tanto, Tokens es un elemento de colección.

```xml
<?xml version="1.0" encoding="utf-8"?>
<Root>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
</Root>
```

El Token.xsd asociado a este ejemplo sería:

```xml
<xs:element name="Root">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="Tokens" type="TokenType" maxOccurs="unbounded"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>

<xs:complexType name="TokenType">
  <xs:sequence>
    <xs:element name="TokenID" type="xs:string"/>
    <xs:element name="TokenText">
      <xs:complexType>
        <xs:sequence>
          <xs:element name="TextHeading" type="xs:string"/>
          <xs:element name="TextBody" type="xs:string"/>
        </xs:sequence>
      </xs:complexType>
    </xs:element>
  </xs:sequence>
</xs:complexType>
```

| **Elemento Diccionario de datos** | **Enlace XML predeterminado** |
|---|---|
| Raíz | empty(null) |
| Tokens | /Root/Tokens |
| Compuesto | empty(null) |
| TokenID | TokenID |
| TokenText | empty(null) |
| EncabezamientoToken | Encabezado de texto/texto |
| TokenBody | TokenText/TextBody |

