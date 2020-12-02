---
title: Utilice la API por lotes para generar varias comunicaciones interactivas
description: Utilice la API por lotes para generar varias comunicaciones interactivas
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communication
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 1%

---


# Generar varias comunicaciones interactivas mediante la API por lotes {#use-batch-api-to-generate-multiple-ic}

Puede utilizar la API por lotes para generar varias comunicaciones interactivas a partir de una plantilla. La plantilla es una comunicación interactiva sin datos. La API de lote combina datos con una plantilla para generar una comunicación interactiva. La API es útil en la producción masiva de comunicaciones interactivas. Por ejemplo: facturas telefónicas, extractos de tarjetas de crédito para varios clientes.

La API de lote acepta registros (datos) en formato JSON y desde un modelo de datos de formulario. El número de comunicaciones interactivas producidas es igual a los registros especificados en el archivo JSON de entrada en el modelo de datos de formulario configurado. Puede utilizar la API para producir tanto la impresión como la salida web. La opción IMPRIMIR produce un documento PDF y la opción WEB produce datos en formato JSON para cada registro individual.

## Uso de la API por lotes {#using-the-batch-api}

Puede utilizar la API de lote junto con Carpetas vigiladas o como una API de descanso independiente. Puede configurar una plantilla, un tipo de salida (HTML, PRINT o Ambos), una configuración regional, un servicio de relleno previo y un nombre para que las comunicaciones interactivas generadas utilicen la API por lotes.

Combina un registro con una plantilla de comunicación interactiva para producir una comunicación interactiva. Las API de lote pueden leer registros (datos para plantillas de comunicación interactivas) directamente desde un archivo JSON o desde un origen de datos externo al que se accede mediante un modelo de datos de formulario. Puede guardar cada registro en un archivo JSON independiente o crear una matriz JSON para guardar todos los registros en un solo archivo.

**Un único registro en un archivo JSON**

```json
{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}
```

**Varios registros en un archivo JSON**

```json
[{
   "employee": {
       "name": "John",
       "id": 1,
       "mobileNo": 9871996461,
       "age": 39
   }
},{
   "employee": {
       "name": "Jacob",
       "id": 2,
       "mobileNo": 9871996462,
       "age": 38
   }
},{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}]
```

### Uso de la API por lotes con carpetas vigiladas {#using-the-batch-api-watched-folders}

Para facilitar la experiencia de la API, AEM Forms proporciona un servicio de carpetas vigiladas configurado para utilizar la API de lotes de forma predeterminada. Puede acceder al servicio a través de la interfaz de usuario de AEM Forms para generar varias comunicaciones interactivas. También puede crear servicios personalizados según sus necesidades. Puede utilizar los métodos que se indican a continuación para utilizar la API por lotes con la carpeta Watched:

* Especificar datos de entrada (registros) en formato de archivo JSON para generar una comunicación interactiva
* Utilizar datos de entrada (registros) guardados en un origen de datos externo y a los que se accede mediante un modelo de datos de formulario para generar una comunicación interactiva

#### Especifique registros de datos de entrada en formato de archivo JSON para generar una comunicación interactiva {#specify-input-data-in-JSON-file-format}

Combina un registro con una plantilla de comunicación interactiva para producir una comunicación interactiva. Puede crear un archivo JSON independiente para cada registro o crear una matriz JSON para guardar todos los registros en un solo archivo:

Para crear una comunicación interactiva a partir de registros guardados en un archivo JSON:

1. Cree una [carpeta vigilada](https://docs.adobe.com/content/help/en/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html) y configúrela para utilizar la API por lotes:
   1. Inicie sesión en la instancia de creación de AEM Forms.
   1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Forms]** > **[!UICONTROL Configurar carpeta vigilada]**. Toque **[!UICONTROL Nuevo]**.
   1. Especifique el **[!UICONTROL nombre]** y la **[!UICONTROL ruta]** física de la carpeta. Por ejemplo, `c:\batchprocessing`.
   1. Seleccione la opción **[!UICONTROL Servicio]** en el campo **[!UICONTROL Procesar archivo usando]**.
   1. Seleccione el servicio **[!UICONTROL com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** en el campo **[!UICONTROL Nombre del servicio]**.
   1. Especifique un patrón de **[!UICONTROL archivo de salida]**. Por ejemplo, el patrón %F/ [pattern](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) especifica que la carpeta vigilada puede encontrar archivos de entrada en una subcarpeta de la carpeta Watched Folder\input.
1. Configurar parámetros avanzados:
   1. Abra la ficha **[!UICONTROL Avanzado]** y agregue las siguientes propiedades personalizadas:

      | Propiedad | Tipo | Descripción |
      |--- |--- |--- |
      | templatePath | Cadena | Especifique la ruta de la plantilla de comunicación interactiva que se va a utilizar. Por ejemplo, /content/dam/formsanddocuments/testsample/mediumic. Es una propiedad obligatoria. |
      | recordPath | Cadena | El valor del campo recordPath ayuda a establecer el nombre de una comunicación interactiva. Puede establecer la ruta de un campo de un registro como valor del campo recordPath. Por ejemplo, si especifica /empleado/Id, el valor del campo de identificación se convierte en nombre para la comunicación interactiva correspondiente. El valor predeterminado es un UUID aleatorio [aleatorio](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()). |
      | usePrefillService | Booleano | Establezca el valor en False. Puede utilizar el parámetro usePrefillService para rellenar previamente la comunicación interactiva con datos recuperados del servicio de relleno previo configurado para la comunicación interactiva correspondiente. Cuando usePrefillService se establece en true, la entrada de datos JSON (para cada registro) se trata como argumentos FDM. El valor predeterminado es false. |
      | batchType | Cadena | Establezca el valor en PRINT, WEB o WEB_AND_PRINT. El valor predeterminado es WEB_AND_PRINT. |
      | locale | Cadena | Especifique la configuración regional de la comunicación interactiva de salida. El servicio incorporado no utiliza la opción de configuración regional, pero puede crear un servicio personalizado para generar comunicaciones interactivas localizadas. El valor predeterminado es en_US |

   1. Puntee **[!UICONTROL Crear]** Se creará la carpeta vigilada.
1. Utilice la carpeta controlada para generar una comunicación interactiva:
   1. Abra la carpeta vigilada. Vaya a la carpeta de entrada.
   1. Cree una carpeta en la carpeta de entrada y coloque el archivo JSON en la carpeta recién creada.
   1. Espere a que la carpeta vigilada procese el archivo. Cuando se procesan inicios, el archivo de entrada y la subcarpeta que contiene el archivo se mueven a la carpeta de ensayo.
   1. Abra la carpeta de salida para vista de la salida:
      * Al especificar la opción IMPRIMIR en Configuración de carpetas vigiladas, se genera la salida PDF para la comunicación interactiva.
      * Cuando especifica la opción WEB en Configuración de carpetas vigiladas, se genera un archivo JSON por registro. Puede utilizar el archivo JSON para [rellenar previamente una plantilla web](#web-template).
      * Al especificar las opciones IMPRIMIR y WEB, se generan tanto documentos PDF como un archivo JSON por registro.

#### Utilice los datos de entrada guardados en un origen de datos externo y a los que se accede mediante el modelo de datos de formulario para generar una comunicación interactiva {#use-fdm-as-data-source}

Los datos (registros) guardados en un origen de datos externo se combinan con una plantilla de comunicación interactiva para generar una comunicación interactiva. Cuando se crea una comunicación interactiva, se conecta a un origen de datos externo a través de un Modelo de datos de formulario (FDM) para acceder a los datos. Puede configurar el servicio de proceso por lotes Carpetas vigiladas para recuperar datos utilizando el mismo modelo de datos de formulario de un origen de datos externo. Para [crear una comunicación interactiva a partir de registros guardados en un origen de datos externo](https://docs.adobe.com/content/help/en/experience-manager-64/forms/form-data-model/work-with-form-data-model.html):

1. Configure el modelo de datos de formulario de la plantilla:
   1. Abra el Modelo de datos de formulario asociado a la plantilla de comunicación interactiva.
   1. Seleccione el OBJETO MODELO DE NIVEL SUPERIOR y toque Editar propiedades.
   1. Seleccione la búsqueda u obtenga el servicio en el campo Servicio de lectura del panel Editar propiedades.
   1. Toque el icono de lápiz del argumento de servicio de lectura para enlazar el argumento a un atributo de solicitud y especificar el valor de enlace. Enlaza el argumento service al atributo de enlace o valor literal especificado, que se pasa al servicio como argumento para recuperar detalles asociados al valor especificado desde el origen de datos.

      <br>
        En este ejemplo, el argumento id toma el valor del atributo id del perfil de usuario y lo pasa como un argumento al servicio de lectura. Se leerán y devolverán valores de propiedades asociadas del objeto del modelo de datos de empleado para la identificación especificada. Por lo tanto, si especifica 00250 en el campo de identificación del formulario, el servicio de lectura leerá los detalles del empleado con la identificación de empleado 00250.
        <br>

      ![Configurar atributo de solicitud](assets/request-attribute.png)

   1. Guardar propiedades y modelo de datos de formulario.
1. Configurar valor para el atributo de solicitud:
   1. Cree un archivo .json en el sistema de archivos y ábralo para editarlo.
   1. Cree una matriz JSON y especifique el atributo principal para recuperar datos del modelo de datos de formulario. Por ejemplo, el siguiente JSON solicita a FDM que envíe datos de registros donde el identificador es 27126 o 27127:

      ```json
          [
              {
                  "id": 27126
              },
              {
                  "id": 27127
              }
          ]
      ```

   1. Guarde y cierre el archivo.

1. Cree una [carpeta vigilada](https://docs.adobe.com/content/help/en/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html) y configúrela para utilizar el servicio de API por lotes:
   1. Inicie sesión en la instancia de creación de AEM Forms.
   1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Forms]** > **[!UICONTROL Configurar carpeta vigilada]**. Toque **[!UICONTROL Nuevo]**.
   1. Especifique el **[!UICONTROL nombre]** y la **[!UICONTROL ruta]** física de la carpeta. Por ejemplo, `c:\batchprocessing`.
   1. Seleccione la opción **[!UICONTROL Servicio]** en el campo **[!UICONTROL Procesar archivo usando]**.
   1. Seleccione el servicio **[!UICONTROL com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** en el campo **[!UICONTROL Nombre del servicio]**.
   1. Especifique un patrón de **[!UICONTROL archivo de salida]**. Por ejemplo, el patrón %F/ [pattern](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) especifica que la carpeta vigilada puede encontrar archivos de entrada en una subcarpeta de la carpeta Watched Folder\input.
1. Configurar parámetros avanzados:
   1. Abra la ficha **[!UICONTROL Avanzado]** y agregue las siguientes propiedades personalizadas:

      | Propiedad | Tipo | Descripción |
      |--- |--- |--- |
      | templatePath | Cadena | Especifique la ruta de la plantilla de comunicación interactiva que se va a utilizar. Por ejemplo, /content/dam/formsanddocuments/testsample/mediumic. Es una propiedad obligatoria. |
      | recordPath | Cadena | El valor del campo recordPath ayuda a establecer el nombre de una comunicación interactiva. Puede establecer la ruta de un campo de un registro como valor del campo recordPath. Por ejemplo, si especifica /empleado/Id, el valor del campo de identificación se convierte en nombre para la comunicación interactiva correspondiente. El valor predeterminado es un UUID aleatorio [aleatorio](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()). |  |
      | usePrefillService | Booleano | Establezca el valor en True. El valor predeterminado es false.  Cuando el valor se establece en true, la API de lote lee los datos del modelo de datos de formulario configurado y los rellena en la comunicación interactiva. Cuando usePrefillService se establece en true, la entrada de datos JSON (para cada registro) se trata como argumentos FDM. |
      | batchType | Cadena | Establezca el valor en PRINT, WEB o WEB_AND_PRINT. El valor predeterminado es WEB_AND_PRINT. |
      | locale | Cadena | Especifique la configuración regional de la comunicación interactiva de salida. El servicio incorporado no utiliza la opción de configuración regional, pero puede crear un servicio personalizado para generar comunicaciones interactivas localizadas. El valor predeterminado es en_US. |

   1. Puntee **[!UICONTROL Crear]** Se creará la carpeta vigilada.
1. Utilice la carpeta controlada para generar una comunicación interactiva:
   1. Abra la carpeta vigilada. Vaya a la carpeta de entrada.
   1. Cree una carpeta en la carpeta de entrada. Coloque el archivo JSON creado en el paso 2 en la carpeta recién creada.
   1. Espere a que la carpeta vigilada procese el archivo. Cuando se procesan inicios, el archivo de entrada y la subcarpeta que contiene el archivo se mueven a la carpeta de ensayo.
   1. Abra la carpeta de salida para vista de la salida:
      * Al especificar la opción IMPRIMIR en Configuración de carpetas vigiladas, se genera la salida PDF para la comunicación interactiva.
      * Cuando especifica la opción WEB en Configuración de carpetas vigiladas, se genera un archivo JSON por registro. Puede utilizar el archivo JSON para [rellenar previamente una plantilla web](#web-template).
      * Al especificar las opciones IMPRIMIR y WEB, se generan tanto documentos PDF como un archivo JSON por registro.

## Invocar la API de lote mediante solicitudes REST

Puede invocar [la API por lotes](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/index.html) mediante solicitudes de transferencia de estado representativa (REST). Le permite proporcionar un extremo REST a otros usuarios para acceder a la API y configurar sus propios métodos para procesar, almacenar y personalizar la comunicación interactiva. Puede desarrollar su propio servlet Java personalizado para implementar la API en la instancia de AEM.

Antes de implementar el servlet Java, asegúrese de que dispone de una comunicación interactiva y de que los archivos de datos correspondientes están listos. Realice los siguientes pasos para crear e implementar el servlet Java:

1. Inicie sesión en la instancia de AEM y cree una comunicación interactiva. Para utilizar la comunicación interactiva mencionada en el código de muestra que se indica a continuación, [haga clic aquí](assets/SimpleMediumIC.zip).
1. [Cree e implemente un proyecto AEM con Apache ](https://helpx.adobe.com/experience-manager/using/maven_arch13.html) Mavenon en su instancia de AEM.
1. Añada [AEM Forms Client SDK versión 6.0.12](https://repo.adobe.com/nexus/content/repositories/public/com/adobe/aemfd/aemfd-client-sdk/) o posterior en la lista de dependencias del archivo POM de su proyecto AEM. Por ejemplo,

   ```xml
       <dependency>
           <groupId>com.adobe.aemfd</groupId>
           <artifactId>aemfd-client-sdk</artifactId>
           <version>6.0.122</version>
       </dependency>
   ```

1. Abra el proyecto Java, cree un archivo .java, por ejemplo, CCMBatchServlet.java. Añada el siguiente código al archivo:

   ```java
           package com.adobe.fd.ccm.multichannel.batch.integration;
   
           import java.io.File;
           import java.io.FileInputStream;
           import java.io.FileOutputStream;
           import java.io.IOException;
           import java.io.InputStream;
           import java.io.PrintWriter;
           import java.util.List;
           import javax.servlet.Servlet;
           import org.apache.commons.io.IOUtils;
           import org.apache.sling.api.SlingHttpServletRequest;
           import org.apache.sling.api.SlingHttpServletResponse;
           import org.apache.sling.api.servlets.SlingAllMethodsServlet;
           import org.json.JSONArray;
           import org.json.JSONObject;
           import org.osgi.service.component.annotations.Component;
           import org.osgi.service.component.annotations.Reference;
   
           import com.adobe.fd.ccm.multichannel.batch.api.builder.BatchConfigBuilder;
           import com.adobe.fd.ccm.multichannel.batch.api.factory.BatchComponentBuilderFactory;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchConfig;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchInput;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchType;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RecordResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RenditionResult;
           import com.adobe.fd.ccm.multichannel.batch.api.service.BatchGeneratorService;
           import com.adobe.fd.ccm.multichannel.batch.util.BatchConstants;
           import java.util.Date;
   
   
           @Component(service=Servlet.class,
           property={
                   "sling.servlet.methods=GET",
                   "sling.servlet.paths="+ "/bin/batchServlet"
           })
           public class CCMBatchServlet extends SlingAllMethodsServlet {
   
               @Reference
               private BatchGeneratorService batchGeneratorService;
               @Reference
               private BatchComponentBuilderFactory batchBuilderFactory;
               public void doGet(SlingHttpServletRequest req, SlingHttpServletResponse resp) {
                   try {
                       executeBatch(req,resp);
                   } catch (Exception e) {
                       e.printStackTrace();
                   }
               }
               private void executeBatch(SlingHttpServletRequest req, SlingHttpServletResponse resp) throws Exception {
                   int count = 0;
                   JSONArray inputJSONArray = new JSONArray();
                   String filePath = req.getParameter("filePath");
                   InputStream is = new FileInputStream(filePath);
                   String data = IOUtils.toString(is);
                   try {
                       // If input file is json object, then create json object and add in json array, if not then try for json array
                       JSONObject inputJSON = new JSONObject(data);
                       inputJSONArray.put(inputJSON);
                   } catch (Exception e) {
                       try {
                           // If input file is json array, then iterate and add all objects into inputJsonArray otherwise throw exception
                           JSONArray inputArray = new JSONArray(data);
                           for(int i=0;i<inputArray.length();i++) {
                               inputJSONArray.put(inputArray.getJSONObject(i));
                           }
                       } catch (Exception ex) {
                           throw new Exception("Invalid JSON Data. File name : " + filePath, ex);
                       }
                   }
                   BatchInput batchInput = batchBuilderFactory.getBatchInputBuilder().setData(inputJSONArray).setTemplatePath("/content/dam/formsanddocuments/[path of the interactive communcation]").build();
                   BatchConfig batchConfig = batchBuilderFactory.getBatchConfigBuilder().setBatchType(BatchType.WEB_AND_PRINT).build();
                   BatchResult batchResult = batchGeneratorService.generateBatch(batchInput, batchConfig);
                   List<RecordResult> recordList = batchResult.getRecordResults();
                   JSONObject result = new JSONObject();
                   for (RecordResult recordResult : recordList) {
                       String recordId = recordResult.getRecordID();
                       for (RenditionResult renditionResult : recordResult.getRenditionResults()) {
                           if (renditionResult.isRecordPassed()) {
                               InputStream output = renditionResult.getDocumentStream().getInputStream();
                               result.put(recordId +"_"+renditionResult.getContentType(), output);
   
                               Date date= new Date();
                               long time = date.getTime();
   
                               // Print output
                               if(getFileExtension(renditionResult.getContentType()).equalsIgnoreCase(".json")) {
                                   File file = new File(time + getFileExtension(renditionResult.getContentType()));
                                   copyInputStreamToFile(output, file);
                               } else
                               {
                                   File file = new File(time + getFileExtension(renditionResult.getContentType()));
                                   copyInputStreamToFile(output, file);
                               }
                           }
                       }
                   }
                   PrintWriter writer = resp.getWriter();
                   JSONObject resultObj = new JSONObject();
                   resultObj.put("result", result);
                   writer.write(resultObj.toString());
               }
   
   
               private static void copyInputStreamToFile(InputStream inputStream, File file)
                       throws IOException {
   
                       try (FileOutputStream outputStream = new FileOutputStream(file)) {
   
                           int read;
                           byte[] bytes = new byte[1024];
   
                           while ((read = inputStream.read(bytes)) != -1) {
                               outputStream.write(bytes, 0, read);
                           }
   
                       }
   
                   }
   
   
               private String getFileExtension(String contentType) {
                   if (contentType.endsWith(BatchConstants.JSON)) {
                       return ".json";
                   } else return ".pdf";
               }
   
   
           }
   ```

1. En el código anterior, reemplace la ruta de la plantilla (setTemplatePath) por la ruta de la plantilla y establezca el valor de la API setBatchType:
   * Al especificar la opción IMPRIMIR, se genera la salida PDF para la comunicación interactiva.
   * Al especificar la opción WEB, se genera un archivo JSON por registro. Puede utilizar el archivo JSON para [rellenar previamente una plantilla web](#web-template).
   * Al especificar las opciones IMPRIMIR y WEB, se generan tanto documentos PDF como un archivo JSON por registro.

1. [Utilice maven para implementar el código actualizado en la instancia](https://helpx.adobe.com/experience-manager/using/maven_arch13.html#BuildtheOSGibundleusingMaven) de AEM.
1. Invoque la API por lotes para generar la comunicación interactiva. La API por lotes imprime una secuencia de archivos PDF y .json en función del número de registros. Puede utilizar el archivo JSON para [rellenar previamente una plantilla web](#web-template). Si utiliza el código anterior, la API se implementa en `http://localhost:4502/bin/batchServlet`. El código imprime y devuelve una secuencia de archivos PDF y JSON.

### Rellenar previamente una plantilla Web {#web-template}

Cuando establece batchType para procesar el Canal Web, la API genera un archivo JSON para cada registro de datos. Puede utilizar la siguiente sintaxis para combinar el archivo JSON con el Canal Web correspondiente para generar una comunicación interactiva:

**Sintaxis**
`http://host:port/<template-path>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=<guide-merged-json-path>`

****
EjemploSi el archivo JSON se encuentra  `C:\batch\mergedJsonPath.json` y utiliza la siguiente plantilla de comunicación interactiva:  `http://host:port/content/dam/formsanddocuments/testsample/mediumic/jcr:content?channel=web`

A continuación, la siguiente URL del nodo de publicación muestra el Canal Web de la comunicación interactiva
`http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/batch/mergedJsonData.json`

Además de guardar los datos en el sistema de archivos, los archivos JSON se almacenan en el repositorio de CRX, el sistema de archivos, el servidor web o se pueden acceder a los datos a través del servicio de cumplimentación previa de OSGI. La sintaxis para combinar datos mediante varios protocolos es:

* **Protocolo CRX**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=crx:///tmp/fd/af/mergedJsonData.json`

* **Protocolo de archivos**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/Users/af/mergedJsonData.json`

* **Prefill Service Protocol**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=service://[SERVICE_NAME]/[IDENTIFIER]`

   SERVICE_NAME hace referencia al nombre del servicio de cumplimentación previa OSGI. Consulte Crear y ejecutar un servicio de relleno previo.

   IDENTIFIER se refiere a cualquier metadato que requiera el servicio de rellenado previo OSGI para recuperar los datos de relleno previo. Un identificador para el usuario que ha iniciado sesión es un ejemplo de metadatos que se pueden utilizar.

* **Protocolo HTTP**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=http://localhost:8000/somesamplexmlfile.xml`

>[!NOTE]
>
>De forma predeterminada, solo está habilitado el protocolo CRX. Para habilitar otros protocolos admitidos, consulte [Configuración del servicio de relleno previo mediante Configuration Manager](https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#ConfiguringprefillserviceusingConfigurationManager).
