---
title: Rellenar previamente campos de formulario adaptables
seo-title: Rellenar previamente campos de formulario adaptables
description: Utilice los datos existentes para rellenar previamente los campos de un formulario adaptable.
seo-description: Con los formularios adaptables, los usuarios pueden rellenar previamente la información básica en un formulario iniciando sesión con sus perfiles sociales. Este artículo describe cómo puede lograr esto.
uuid: 574de83a-7b5b-4a1f-ad37-b9717e5c14f1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 7139a0e6-0e37-477c-9e0b-aa356991d040
docset: aem65
feature: Formularios adaptables
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2202'
ht-degree: 0%

---


# Rellene previamente los campos de formulario adaptables{#prefill-adaptive-form-fields}

## Introducción {#introduction}

Puede rellenar previamente los campos de un formulario adaptable utilizando los datos existentes. Cuando un usuario abre un formulario, los valores de esos campos se rellenan previamente. Para rellenar previamente los datos en un formulario adaptable, haga que los datos del usuario estén disponibles como un XML/JSON de relleno previo en el formato que se adhiera a la estructura de datos de rellenado previo de los formularios adaptables.

## Estructura de los datos de relleno previo {#the-prefill-structure}

Un formulario adaptable puede tener una combinación de campos enlazados y no enlazados. Los campos enlazados son campos que se arrastran desde la ficha Buscador de contenido y que contienen un valor de propiedad `bindRef` no vacío en el cuadro de diálogo de edición de campos. Los campos no enlazados se arrastran directamente desde el navegador de componentes de la barra de tareas y tienen un valor vacío `bindRef`.

Puede rellenar previamente los campos enlazados y no enlazados de un formulario adaptable. Los datos de relleno previo contienen las secciones afBoundData y afUnBoundData para rellenar previamente los campos enlazados y no enlazados de un formulario adaptable. La sección `afBoundData` contiene los datos de rellenado previo de los campos y paneles enlazados. Estos datos deben cumplir con el esquema del modelo de formulario asociado:

* Para formularios adaptables que utilicen la plantilla de formulario [XFA](../../forms/using/prepopulate-adaptive-form-fields.md), utilice el XML de relleno previo compatible con el esquema de datos de la plantilla XFA.
* Para los formularios adaptables que utilizan [XML schema](#xml-schema-af), utilice el XML de relleno previo compatible con la estructura de esquema XML.
* Para los formularios adaptables que utilizan [JSON schema](#json-schema-based-adaptive-forms), utilice el JSON de relleno previo compatible con el esquema JSON.
* Para los formularios adaptables que utilizan el esquema FDM, utilice el JSON de relleno previo compatible con el esquema FDM.
* Para los formularios adaptables con [sin modelo de formulario](#adaptive-form-with-no-form-model), no hay datos enlazados. Cada campo es un campo independiente y se rellena previamente utilizando el XML independiente.

### Ejemplo de estructura XML de relleno previo {#sample-prefill-xml-structure}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<afData>
  <afBoundData>
     <employeeData>
        .
     </employeeData>
  </afBoundData>

  <afUnboundData>
    <data>
      <textbox>Hello World</textbox>
         .
         .
      <numericbox>12</numericbox>
         . 
         .              
    </data>
  </afUnboundData>
</afData>
```

### Ejemplo de estructura JSON de prerelleno {#sample-prefill-json-structure}

```javascript
{
   "afBoundData": {
      "employeeData": { }
   },
   "afUnboundData": {
      "data": {
         "textbox": "Hello World",
         "numericbox": "12"
      }
   }
}
```

Para los campos enlazados con los mismos campos bindref o unbound con el mismo nombre, los datos especificados en la etiqueta XML o el objeto JSON se rellenan en todos los campos. Por ejemplo, dos campos de un formulario se asignan al nombre `textbox` en los datos de relleno previo. Durante el tiempo de ejecución, si el primer campo de cuadro de texto contiene &quot;A&quot;, entonces &quot;A&quot; se rellena automáticamente en el segundo cuadro de texto. Esta vinculación se denomina vinculación activa de campos de formulario adaptables.

### Formulario adaptable con plantilla de formulario XFA {#xfa-based-af}

La estructura de XML de relleno previo y el XML enviado para formularios adaptables basados en XFA es la siguiente:

* **Estructura** XML de relleno previo: El formulario adaptable prefill XML para XFA debe ser compatible con el esquema de datos de la plantilla de formulario XFA. Para rellenar previamente los campos no enlazados, ajuste la estructura XML de relleno previo en la etiqueta `/afData/afBoundData` .

* **Estructura** XML enviada: Cuando no se utiliza ningún XML de relleno previo, el XML enviado contiene datos para los campos enlazados y no enlazados en la etiqueta  `afData` wrapper. Si se utiliza un XML de relleno previo, el XML enviado tiene la misma estructura que el XML de relleno previo. Si el XML de relleno previo comienza con la etiqueta raíz `afData` , el XML de salida también tiene el mismo formato. Si el XML de relleno previo no tiene `afData/afBoundData`wrapper y en su lugar comienza directamente desde la etiqueta raíz del esquema como `employeeData`, el XML enviado también comienza con la etiqueta `employeeData`.

Prefill-Submit-Data-ContentPackage.zip

[Obtener ](assets/prefill-submit-data-contentpackage.zip)
FileSample que contiene datos de relleno previo y datos enviados

### Formularios adaptables basados en esquemas XML  {#xml-schema-af}

La estructura de XML de relleno previo y XML enviado para formularios adaptables basados en esquema XML es la siguiente:

* **Estructura** XML de relleno previo: El XML de relleno previo debe ser compatible con el esquema XML asociado. Para rellenar previamente los campos no enlazados, ajuste la estructura XML de relleno previo a la etiqueta /afData/afBoundData .
* **Estructura** XML enviada: si no se utiliza ningún XML de relleno previo, el XML enviado contiene datos para los campos enlazados y no enlazados en la etiqueta  `afData` wrapper. Si se utiliza el XML de relleno previo, el XML enviado tiene la misma estructura que el XML de relleno previo. Si el XML de relleno previo comienza con la etiqueta raíz `afData` , el XML de salida tiene el mismo formato. Si el XML de relleno previo no tiene `afData/afBoundData` envolvente y en su lugar comienza directamente desde la etiqueta raíz del esquema como `employeeData`, el XML enviado también comienza con la etiqueta `employeeData`.

```xml
<?xml version="1.0" encoding="utf-8" ?> 
<xs:schema targetNamespace="https://adobe.com/sample.xsd"
            xmlns="https://adobe.com/sample.xsd"
            xmlns:xs="https://www.w3.org/2001/XMLSchema">
 
    <xs:element name="sample" type="SampleType"/>
         
    <xs:complexType name="SampleType">
        <xs:sequence>
            <xs:element name="noOfProjectsAssigned" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

Para los campos cuyo modelo es un esquema XML, los datos se rellenan previamente en la etiqueta `afBoundData` como se muestra en el ejemplo XML siguiente. Se puede utilizar para colocar el prefijo en un formulario adaptable uno o varios campos de texto sin enlazar.

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <textbox>Ignorance is bliss :) </textbox>
    </data>
  </afUnboundData>
  <afBoundData>
    <data>
      <noOfProjectsAssigned>twelve</noOfProjectsAssigned>
    </data>
  </afBoundData>
</afData>
```

>[!NOTE]
>
>Se recomienda no utilizar campos no enlazados en paneles enlazados (paneles con `bindRef` no vacíos que se hayan creado arrastrando componentes de la barra de tareas o la ficha Fuentes de datos). Puede causar la pérdida de datos de estos campos independientes. Además, se recomienda que los nombres de los campos sean únicos en todo el formulario, especialmente para los campos independientes.

#### Un ejemplo sin afData y afBoundData wrapper {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### Formularios adaptables basados en esquemas JSON {#json-schema-based-adaptive-forms}

En el caso de los formularios adaptables basados en el esquema JSON, a continuación se describe la estructura de JSON de relleno previo y JSON enviado. Para obtener más información, consulte [Creación de formularios adaptables utilizando el esquema JSON](../../forms/using/adaptive-form-json-schema-form-model.md).

* **Estructura** JSON de relleno previo: El JSON de relleno previo debe ser compatible con el esquema JSON asociado. Opcionalmente, se puede ajustar en el objeto /afData/afBoundData si desea rellenar previamente también los campos no enlazados.
* **Estructura** JSON enviada: si no se utiliza un JSON de relleno previo, el JSON enviado contiene datos para los campos enlazados y no enlazados en la etiqueta de envoltura afData. Si se utiliza el JSON de relleno previo, el JSON enviado tiene la misma estructura que el JSON de relleno previo. Si el JSON de relleno previo comienza con el objeto raíz afData, el JSON de salida tiene el mismo formato. Si el JSON de relleno previo no tiene un envoltorio afData/afBoundData y en su lugar comienza directamente desde el objeto raíz de esquema como usuario, el JSON enviado también comienza con el objeto de usuario.

```json
{
    "id": "https://some.site.somewhere/entry-schema#",
    "$schema": "https://json-schema.org/draft-04/schema#",
    "type": "object",
    "properties": {
        "address": {
            "type": "object",
            "properties": { 
    "name": {
     "type": "string"
    },
    "age": {
     "type": "integer"
}}}}}
```

Para los campos que utilizan el modelo de esquema JSON, los datos se rellenan previamente en el objeto afBoundData como se muestra en el archivo JSON de muestra siguiente. Se puede utilizar para colocar el prefijo en un formulario adaptable uno o varios campos de texto sin enlazar. A continuación se muestra un ejemplo de datos con el envoltorio `afData/afBoundData`:

```json
{
  "afData": {
    "afUnboundData": {
      "data": { "textbox": "Ignorance is bliss :) " }
    },
    "afBoundData": {
      "data": { {
   "user": {
    "address": {
     "city": "Noida",
     "country": "India"
}}}}}}}
```

A continuación se muestra un ejemplo sin `afData/afBoundData` envolvente:

```json
{
 "user": {
  "address": {
   "city": "Noida",
   "country": "India"
}}}
```

>[!NOTE]
>
>Se recomienda utilizar campos no enlazados en paneles enlazados (paneles con bindRef no vacío que se hayan creado arrastrando componentes de la barra de tareas o la ficha Fuentes de datos), ya que podría causar la pérdida de datos de los campos no enlazados. **** Se recomienda tener nombres de campo únicos en todo el formulario, especialmente en los campos no enlazados.

### Formulario adaptable sin modelo de formulario {#adaptive-form-with-no-form-model}

Para los formularios adaptables sin modelo de formulario, los datos de todos los campos se encuentran bajo la etiqueta `<data>` de `<afUnboundData> tag`.

Asimismo, tome nota de lo siguiente:

Las etiquetas XML para los datos de usuario enviados para varios campos se generan utilizando el nombre de los campos. Por lo tanto, los nombres de campo deben ser únicos.

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <radiobutton>2</radiobutton>
      <repeatable_panel_no_form_model>
        <numericbox>12</numericbox>
      </repeatable_panel_no_form_model>
      <repeatable_panel_no_form_model>
        <numericbox>21</numericbox>
      </repeatable_panel_no_form_model>
      <checkbox>2</checkbox>
      <textbox>Nopes</textbox>
    </data>
  </afUnboundData>
  <afBoundData/>
</afData>
```

## Configuración del servicio de prerelleno mediante Configuration Manager {#configuring-prefill-service-using-configuration-manager}

Para habilitar el servicio de prellenado, especifique la Configuración predeterminada del servicio de prellenado en la Configuración AEM de la consola web. Siga los siguientes pasos para configurar el servicio Prefill:

>[!NOTE]
>
>La configuración del servicio de relleno previo es aplicable a formularios adaptables, formularios HTML5 y conjuntos de formularios HTML5.

1. Abra **[!UICONTROL Configuración de la consola web de Adobe Experience Manager]** utilizando la dirección URL:\
   https://&lt;server>:&lt;port>/system/console/configMgr
1. Busque y abra **[!UICONTROL Default Prefill Service Configuration]**.

   ![Configuración previa](assets/prefill_config_new.png)

1. Introduzca la ubicación de datos o una expresión regular para las **ubicaciones de archivos de datos**. Algunos ejemplos de ubicaciones de archivos de datos válidos son:

   * file:///C:/Users/public/Document/Prefill/.*
   * https://localhost:8000/somesamplexmlfile.xml

   >[!NOTE]
   >
   >De forma predeterminada, se permite el rellenado previo mediante archivos crx para todos los tipos de Forms adaptable (XSD, XDP, JSON, FDM y sin modelo de formulario). El rellenado previo solo se permite con archivos JSON y XML.

1. El servicio de cumplimentación previa ya está configurado para el formulario.

   >[!NOTE]
   >
   >El protocolo crx se encarga de la seguridad de los datos rellenados previamente y, por lo tanto, está permitido de forma predeterminada. La cumplimentación previa a través de otros protocolos usando regex genéricos puede causar vulnerabilidad. En la configuración, especifique una configuración de URL segura para proteger los datos.

## El curioso caso de los paneles repetibles {#the-curious-case-of-repeatable-panels}

Por lo general, los campos enlazados (esquema de formulario) y no enlazados se crean en la misma forma adaptativa, pero las siguientes son algunas excepciones en caso de que el enlace sea repetible:

* Los paneles repetibles no enlazados no son compatibles con los formularios adaptables que utilizan la plantilla de formulario XFA, XSD, el esquema JSON o el esquema FDM.
* No utilice campos independientes en paneles repetibles enlazados.

>[!NOTE]
>
>Como regla general, no mezcle campos enlazados y no enlazados si están intersectados en datos rellenados por el usuario final en campos no enlazados. Si es posible, debe modificar el esquema o la plantilla de formulario XFA y agregar una entrada para los campos no enlazados, de modo que también se convierta en enlazado y sus datos estén disponibles como otros campos en los datos enviados.

## Protocolos admitidos para prefijar datos de usuario {#supported-protocols-for-prefilling-user-data}

Los formularios adaptables se pueden rellenar previamente con datos de usuario en formato de datos de relleno previo mediante los protocolos siguientes cuando se configuran con regex válido:

### El protocolo crx:// {#the-crx-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

El nodo especificado debe tener una propiedad denominada `jcr:data` y contener los datos.

### El protocolo file://  {#the-file-protocol-nbsp}

```http
https://localhost:4502/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

El archivo de referencia debe estar en el mismo servidor.

### El protocolo https:// {#the-http-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://localhost:8000/somesamplexmlfile.xml
```

### El protocolo service:// {#the-service-protocol}

```http
https://localhost:4502/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

* SERVICE_NAME hace referencia al nombre del servicio de relleno previo OSGI. Consulte [Crear y ejecutar un servicio de relleno previo](../../forms/using/prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service).
* IDENTIFIER se refiere a cualquier metadato que requiera el servicio de rellenado previo OSGI para recuperar los datos de rellenado previo. Un identificador para el usuario que ha iniciado sesión es un ejemplo de metadatos que se pueden utilizar.

>[!NOTE]
>
>No se admite el paso de parámetros de autenticación.

### Configuración del atributo de datos en slingRequest {#setting-data-attribute-in-slingrequest}

También puede establecer el atributo `data` en `slingRequest`, donde el atributo `data` es una cadena que contiene XML o JSON, como se muestra en el código de ejemplo siguiente (el ejemplo es para XML):

```javascript
<%
           String dataXML="<afData>" +
                            "<afUnboundData>" +
                                "<data>" +
                                    "<first_name>"+ "Tyler" + "</first_name>" +
                                    "<last_name>"+ "Durden " + "</last_name>" +
                                    "<gender>"+ "Male" + "</gender>" +
                                    "<location>"+ "Texas" + "</location>" +
                                    "</data>" +
                            "</afUnboundData>" +
                        "</afData>";
        slingRequest.setAttribute("data", dataXML);
%>
```

Puede escribir una cadena XML o JSON simple que contenga todos los datos y definirlos en slingRequest. Esto se puede hacer fácilmente en el JSP del procesador para cualquier componente, que desea incluir en la página donde puede establecer el atributo de datos slingRequest .

Por ejemplo, donde desea un diseño específico para la página con un tipo específico de encabezado. Para conseguirlo, puede escribir su propio `header.jsp`, que puede incluir en el componente de página y establecer el atributo `data`.

Otro buen ejemplo es un caso de uso en el que le gustaría rellenar previamente los datos de inicio de sesión a través de cuentas sociales como Facebook, Twitter o LinkedIn. En este caso, puede incluir un JSP simple en `header.jsp`, que obtiene datos de la cuenta de usuario y establece el parámetro de datos.

prefill-page component.zip

[Obtener ](assets/prefill-page-component.zip)
FileSample prefill.jsp en el componente de página

## Servicio de precarga personalizado de AEM Forms {#aem-forms-custom-prefill-service}

Se puede utilizar el servicio de rellenado previo personalizado para las situaciones en las que se leen constantemente datos de una fuente predefinida. El servicio de rellenado previo lee datos de orígenes de datos definidos y prefiere los campos del formulario adaptable con el contenido del archivo de datos de rellenado previo. También le ayuda a asociar permanentemente los datos prerellenados con un formulario adaptable.

### Crear y ejecutar un servicio de prerelleno {#create-and-run-a-prefill-service}

El servicio de prefill es un servicio OSGi y se empaqueta a través del paquete OSGi. Puede crear el paquete OSGi, cargarlo e instalarlo en paquetes AEM Forms. Antes de comenzar a crear el paquete:

* [Descargar el SDK de cliente de AEM Forms](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html)
* Descargar el paquete repetitivo

* Coloque el archivo de datos (datos de relleno previo) en el repositorio crx. Puede colocar el archivo en cualquier ubicación de la carpeta \content del repositorio crx.

[Obtener archivo](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### Crear un servicio de prerelleno {#create-a-prefill-service}

El paquete repetitivo (paquete de servicio de prellenado de muestra) contiene una implementación de muestra del servicio de prerellenado de AEM Forms. Abra el paquete repetitivo en un editor de código. Por ejemplo, abra el proyecto repetitivo en Eclipse para editarlo. Después de abrir el paquete repetitivo en un editor de código, realice los siguientes pasos para crear el servicio.

1. Abra el archivo src\main\java\com\adobe\test\Prefill.java para editarlo.
1. En el código, establezca el valor de:

   * `nodePath:` La variable de ruta de nodo que señala a la ubicación del repositorio crx contiene la ruta del archivo de datos (prefill). Por ejemplo, /content/prefilldata.xml
   * `label:` El parámetro label especifica el nombre para mostrar del servicio. Por ejemplo, el servicio de precarga predeterminado

1. Guarde y cierre el archivo `Prefill.java`.
1. Añada el paquete `AEM Forms Client SDK` a la ruta de compilación del proyecto repetitivo.
1. Compile el proyecto y cree el .jar para el paquete.

#### Inicie y utilice el servicio de precarga {#start-and-use-the-prefill-service}

Para iniciar el servicio de rellenado previo, cargue el archivo JAR en AEM Forms Web Console y active el servicio. Ahora, el servicio empieza a aparecer en el editor de formularios adaptables. Para asociar un servicio de rellenado previo a un formulario adaptable:

1. Abra el formulario adaptable en Forms Editor y abra el panel Propiedades del contenedor de formularios.
1. En la consola Propiedades, vaya al contenedor de AEM Forms > Básico > Servicio de relleno previo.
1. Seleccione el servicio de relleno predeterminado y haga clic en **[!UICONTROL Guardar]**. El servicio está asociado al formulario.

## Rellenado previo de datos en el cliente {#prefill-at-client}

Cuando se rellena previamente un formulario adaptable, el servidor de AEM Forms combina los datos con un formulario adaptable y le envía el formulario rellenado. De forma predeterminada, la acción de combinación de datos se realiza en el servidor.

Puede configurar el servidor de AEM Forms para que realice la acción de combinación de datos en el cliente en lugar del servidor. Reduce considerablemente el tiempo necesario para rellenar y procesar formularios adaptables. De forma predeterminada, la función está desactivada. Puede activarlo desde el Administrador de configuración o la línea de comandos.

* Para habilitar o deshabilitar desde el administrador de configuración:
   1. Abra AEM Administrador de configuración.
   1. Localice y abra la configuración del canal web de comunicaciones interactivas y formularios adaptables
   1. Habilitar la opción Configuration.af.clientside.datamerge.enabled.name
* Para habilitar o deshabilitar desde la línea de comandos:
   * Para habilitar, ejecute el siguiente comando cURL:
      `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=true \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

   * Para desactivarlo, ejecute el siguiente comando cURL:
      `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=false \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`
   Para aprovechar al máximo la opción de rellenar previamente los datos en el cliente, actualice el servicio de relleno previo para devolver [FileAttachmentMap](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) y [CustomContext](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html)