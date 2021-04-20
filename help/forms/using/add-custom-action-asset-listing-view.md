---
title: Agregar una acción personalizada a la vista Listado de activos
seo-title: Agregar una acción personalizada a la vista Listado de activos
description: Este artículo explica cómo agregar acciones personalizadas a la vista Lista de activos
seo-description: Este artículo explica cómo agregar acciones personalizadas a la vista Lista de activos
uuid: 45f25cfb-f08f-42c6-99c5-01900dd8cdee
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 6378ae30-a351-49f7-8e9a-f0bd4287b9d3
docset: aem65
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1383'
ht-degree: 2%

---


# Agregar una acción personalizada a la vista Listing de activos{#add-custom-action-to-the-asset-listing-view}

## Información general {#overview}

La solución de Gestión de Correspondencia le permite agregar acciones personalizadas a la interfaz de usuario Administrar recursos .

Puede agregar una acción personalizada a la vista Listado de activos para:

* Uno o más tipos de recursos o letras
* Ejecución (la acción/el comando se activa) al seleccionar recursos/letras simples, múltiples o sin selección

Esta personalización se muestra con el escenario que agrega el comando &quot;Descargar PDF plano&quot; a la vista Listado de activos para las letras. Este escenario de personalización permite a los usuarios descargar PDF plano de una sola carta seleccionada.

### Requisitos previos {#prerequisites}

Para completar el siguiente escenario o uno similar, necesita conocer:

* CRX
* JavaScript
* Java

## Escenario: Agregue un comando a la interfaz de usuario de la lista Letras para descargar la versión PDF plana de una carta {#addcommandtoletters}

Los siguientes pasos agregan un comando &quot;Descargar PDF plano&quot; a la vista Lista de recursos para las cartas y permiten a sus usuarios descargar PDF plano de la carta seleccionada. Mediante estos pasos con el código y los parámetros adecuados, puede añadir otras funciones para un recurso diferente, como diccionarios de datos o textos.

Para personalizar la Gestión de Correspondencia para permitir que los usuarios descarguen un PDF plano de letras, complete los siguientes pasos:

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.

1. En la carpeta de aplicaciones, cree una carpeta denominada items with path/structure similar a la carpeta de elementos ubicada en la carpeta de selección siguiendo los pasos siguientes:

   1. Haga clic con el botón derecho en la carpeta **items** en la siguiente ruta y seleccione **Overlay Node**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/selection/items`

      >[!NOTE]
      >
      >Esta ruta es específica para la creación de una acción que funcione con la selección de uno o varios recursos o letras. Si desea crear una acción que funcione sin selección, debe crear un nodo de superposición para la siguiente ruta y completar los pasos restantes en consecuencia:
      >
      >
      >`/libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/default/items`

      ![Crear nodo](assets/1_itemscreatenode.png)

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tiene los siguientes valores:

      **Ruta:** /libs/fd/cm/ma/gui/content/massets/jcr:content/body/content/header/items/selection/items

      **Ubicación:** /apps/

      **Coincidir tipos de nodo:** seleccionados

      ![Nodo de superposición](assets/2_createnodedownloadflatpdf.png)

   1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

      Haga clic en **Guardar todo**.

1. En la carpeta de elementos recién creada, añada un nodo para el botón o la acción personalizados en un recurso concreto (Ejemplo: downloadFlatPDF) siguiendo estos pasos:

   1. Haga clic con el botón derecho en la carpeta **items** y seleccione **Create** > **Create Node**.

   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** downloadFlatPDF (o el nombre que desee dar a esta propiedad)

      **Tipo:** nt:unstructured

   1. Haga clic en el nuevo nodo que ha creado (aquí downloadFlatPDF). CRX muestra las propiedades del nodo.

   1. Agregue las siguientes propiedades al nodo (aquí downloadFlatPDF) y haga clic en **Guardar todo**:

      <table>
        <tbody>
        <tr>
        <td><strong>Nombre</strong></td>
        <td><strong>Tipo</strong></td>
        <td><strong>Valor y descripción</strong></td>
        </tr>
        <tr>
        <td>clase</td>
        <td>Cadena</td>
        <td>foundation-collection-action</td>
        </tr>
        <tr>
        <td>foundation-collection-action</td>
        <td>Cadena</td>
        <td><p>{"target": ".cq-managementAsset-admin-childpages", "activeSelectionCount": "single","type": "LETTER"}<br /> <br /> <br /> <strong>activeSelectionCount</strong> puede ser único o múltiple para permitir selecciones de recursos únicos o múltiples en los que se realiza la acción personalizada.</p> <p><strong></strong> puede ser una o más (entradas múltiples separadas por coma) de lo siguiente: LETRA,TEXTO,LISTA,CONDICIÓN,DICCIONARIO DE DATOS</p> </td>
        </tr>
        <tr>
        <td>icono</td>
        <td>Cadena</td>
        <td>icon-download<br /> <br /> El icono que la Gestión de Correspondencia muestra a la izquierda del comando/menú. Para ver los diferentes iconos y configuraciones disponibles, consulte <a href="https://docs.adobe.com/docs/en/aem/6-3/develop/ref/coral-ui/coralui3/Coral.Icon.html" target="_blank">Documentación de los iconos de CoralUI</a>.<br /> </td>
        </tr>
        <tr>
        <td>jcr:primaryType</td>
        <td>Nombre</td>
        <td>nt:unstructured</td>
        </tr>
        <tr>
        <td>rel</td>
        <td>Cadena</td>
        <td>download-plain-pdf-button</td>
        </tr>
        <tr>
        <td>sling:resourceType</td>
        <td>Cadena</td>
        <td>granite/ui/components/endor/actionbar/button</td>
        </tr>
        <tr>
        <td>text</td>
        <td>Cadena</td>
        <td>Descargar PDF plano (o cualquier otra etiqueta)<br /> <br /> El comando que aparece en la interfaz de listado de recursos</td>
        </tr>
        <tr>
        <td>el título</td>
        <td>Cadena</td>
        <td>Descargue un PDF plano de la letra seleccionada (o cualquier otra etiqueta/texto alternativo)<br /> <br /> El título es el texto alternativo que la Gestión de Correspondencia muestra cuando el usuario pasa el ratón sobre el comando personalizado.</td>
        </tr>
        </tbody>
       </table>

1. En la carpeta de aplicaciones, cree una carpeta denominada js con una ruta o estructura similares a la carpeta de elementos ubicada en la carpeta de administración siguiendo los pasos siguientes:

   1. Haga clic con el botón derecho en la carpeta **js** en la siguiente ruta y seleccione **nodo de superposición**:

      `/libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js`

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tiene los siguientes valores:

      **Ruta:** /libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js

      **Ubicación:** /apps/

      **Coincidir tipos de nodo:** seleccionados

   1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones. Haga clic en **Guardar todo**.

1. En la carpeta js, cree un archivo llamado formaction.js con el código para la gestión de acciones del botón siguiendo los pasos siguientes:

   1. Haga clic con el botón derecho en la carpeta **js** en la siguiente ruta y seleccione **Crear > Crear archivo**:

      `/apps/fd/cm/ma/gui/components/admin/clientlibs/admin/js`

      Asigne un nombre al archivo formaction.js.

   1. Haga doble clic en el archivo para abrirlo en CRX.
   1. En el archivo formaction.js (en la rama /apps), copie el código del archivo formaction.js en la siguiente ubicación:

      `/libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js/formaction.js`

      A continuación, añada el siguiente código al final del archivo formaction.js (en la rama /apps) y haga clic en **Guardar todo**:

      ```javascript
      /* Action url for xml file to be added.*/
      var ACTION_URL = "/apps/fd/cm/ma/gui/content/commons/actionhandlers/items/letterpdfdownloader.html";
      
      /* File upload handling*/
      var fileSelectedHandler = function(e){
          if(e && e.target && e.target.value)
              $(".downloadLetterPDFBtn").removeAttr('disabled');
          else
              $(".downloadLetterPDFBtn").attr('disabled','disabled');
      }
      
      /*Handing of Download button in pop up.*/
      var downloadClickHandler = function(){
          $('#downloadLetterPDFDilaog').modal("hide");
          var element = $('.foundation-selections-item');
          var path = $(element).data("path");
          $("#fileUploadForm").attr('action', ACTION_URL + "?letterId="+path).submit();
      }
      
      /*Click handling on action button.*/
      $(document).on("click",'.download-flat-pdf-button',function(e){
          $("#uploadSamepledata").val("");
           if($('#downloadLetterPDFDilaog').length == 0){
              $(document).on("click",".downloadLetterPDFBtn",downloadClickHandler);
              $(document).on("change","#uploadSamepledata",fileSelectedHandler);
              $("body").append(downloadLetterPDFDilaog);
          }
            $('#downloadLetterPDFDilaog').modal("show");
      });
      
      /*Download popup.*/
      var downloadLetterPDFDilaog = '<div id="downloadLetterPDFDilaog" class="coral-Modal notice " role="dialog"  aria-hidden="true">'+
          '<form id="fileUploadForm" method="POST" enctype="multipart/form-data">'+
              '<div class="coral-Modal-header">'+
                  '<h2 class="coral-Modal-title coral-Heading coral-Heading--2" id="modal-header1443020790107-label" tabindex="0">Download Letter as PDF.</h2>'+
                  '<button type="button" class="coral-MinimalButton coral-Modal-closeButton" data-dismiss="modal">×</button>'+
              '</div>'+
              '<div class="coral-Modal-body" id="modal-header1443020790107-message" role="document" tabindex="0">'+
                  '<div class="coral-Modal-message">'+
                      '<p></p>'+
                  '</div>'+
                  '<div class="coral-Modal-uploader">'+
                      '<p>Select sample data for letter.</p>'+
                      '<input type="file" id="uploadSamepledata" name="file" accept=".xml" size="70px">'+
                  '</div>'+
              '</div>'+
           '</form>'+
              '<div class="coral-Modal-footer">'+
                  '<button type="button" class="coral-Button" data-dismiss="modal">Cancel</button>'+
                  '<button type="button" class="coral-Button coral-Button--primary downloadLetterPDFBtn" disabled="disabled">Download</button>'+
              '</div>'+
      '</div>';
      ```

      El código que agregue en este paso anula el código de la carpeta libs, por lo que copie el código anterior en el archivo formaction.js de la rama /apps. Copiar el código de la rama /libs a la rama /apps garantiza que la funcionalidad anterior también funcione.

      El código anterior es para la gestión de acciones específicas de letras del comando creado en este procedimiento. Para la gestión de acciones de otros recursos, modifique el código JavaScript.

1. En la carpeta de aplicaciones, cree una carpeta denominada items with path/structure similar a la carpeta de elementos ubicada en la carpeta de controladores de acciones siguiendo los pasos siguientes:

   1. Haga clic con el botón derecho en la carpeta **items** en la siguiente ruta y seleccione **Overlay Node**:

      `/libs/fd/cm/ma/gui/content/commons/actionhandlers/items/`

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tiene los siguientes valores:

      **Ruta:** /libs/fd/cm/ma/gui/content/commons/actionhandlers/items/

      **Ubicación:** /apps/

      **Coincidir tipos de nodo:** seleccionados

   1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

   1. Haga clic en **Guardar todo**.

1. En el nodo de elementos recién creado, añada un nodo para el botón o la acción personalizados en un recurso concreto (Ejemplo: letterpdfdownloader) siguiendo estos pasos:

   1. Haga clic con el botón derecho en la carpeta de elementos y seleccione **Crear > Crear nodo**.

   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** letterpdfdownloader (o el nombre que desee dar a esta propiedad) debe ser único. Si usa un nombre diferente aquí, especifique el mismo en la variable ACTION_URL del archivo formaction.js).

      **Tipo:** nt:unstructured

   1. Haga clic en el nuevo nodo que ha creado (aquí downloadFlatPDF). CRX muestra las propiedades del nodo.

   1. Agregue la siguiente propiedad al nodo (aquí letterpdfdownloader) y haga clic en **Guardar todo**:

      | **Nombre** | **Tipo** | **Value** |
      |---|---|---|
      | sling:resourceType | Cadena | fd/cm/ma/gui/components/admin/clientlibs/admin |

1. Cree un archivo llamado POST.jsp con el código para la gestión de acciones del comando en la siguiente ubicación:

   /apps/fd/cm/ma/gui/components/admin/clientlibs/admin

   1. Haga clic con el botón derecho en la carpeta **admin** en la siguiente ruta y seleccione **Crear > Crear archivo**:

      /apps/fd/cm/ma/gui/components/admin/clientlibs/admin

      Asigne al archivo el nombre POST.jsp. (El nombre de archivo solo debe ser POST.jsp).

   1. Haga doble clic en el archivo **POST.jsp** para abrirlo en CRX.
   1. Agregue el siguiente código al archivo POST.jsp y haga clic en **Guardar todo**:

      Este código es específico del servicio de procesamiento de letras. Para cualquier otro recurso, agregue las bibliotecas java de ese recurso a este código. Para obtener más información sobre las API de AEM Forms, consulte [API de AEM Forms](https://adobe.com/go/learn_aemforms_javadocs_63_en).

      Para obtener más información sobre AEM bibliotecas, consulte AEM [Componentes](/help/sites-developing/components.md).

      ```xml
      /*Import libraries. Here we are downloading letter flat pdf with input xml data so we require letterRender Api. For any other Module functionality we need to first import that library. */
      <%@include file="/libs/foundation/global.jsp"%>
      <!DOCTYPE html lang="en" PUBLIC "-//W3C//DTD XHTML 1.1//EN" "https://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
      <%@page import="com.adobe.icc.ddg.api.*"%>
      <%@page import="com.adobe.icc.dbforms.obj.*"%>
      <%@page import="com.adobe.icc.render.obj.*" %>
      <%@page import="com.adobe.icc.services.api.*" %>
      <%@page import="org.apache.sling.api.resource.*" %>
      <%@page import="java.io.File" %>
      <%@page import="java.util.*" %>
      <%@page import="com.adobe.livecycle.content.appcontext.AppContextManager"%>
      <%@page import=" com.adobe.icc.dbforms.exceptions.ICCException"%>
      <%@page import="java.io.InputStream" %>
      <%@page import="java.io.FileInputStream" %>
      <%@page import="org.apache.commons.io.IOUtils" %>
      <%@page session="false" contentType="text/html; charset=utf-8"%>
      <%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0"%>
      <%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
       <%@page session="false" contentType="text/html; charset=utf-8"%>
      <%
         AppContextManager.setCurrentAppContext("/content/apps/cm");
         /*Get letter id sent in js file.*/
          String letterId = request.getParameter("letterId");
          if(letterId.lastIndexOf("?") != -1)
              letterId = letterId.substring(0, letterId.indexOf("?"));
          String fileName = null;
          String letterName = null;
          InputStream inputStream = null;
          /*Get xml file data*/
          if (slingRequest.getRequestParameter("file") != null)
              inputStream = slingRequest.getRequestParameter("file").getInputStream();
          if(letterId != null){
              String xmlData = null;
              try{
                  xmlData = IOUtils.toString(inputStream, "UTF-8");
              }
              catch (Exception e) {
                  log.error("Xml data does not exists.");
              }
              /*letter Name from letter letter id.*/
              letterName = letterId.substring(letterId.lastIndexOf("/")+1);
              /*Invoking letter render services API.*/
              LetterRenderService letterRenderService = sling.getService(LetterRenderService.class);
              /*using CM renderLetter api to get pdfbytes.*/
              PDFResponseType  pdfResponseType= letterRenderService.renderLetter(letterId,xmlData,true,false,false,false);
              byte[] bytes = null;
              /*Downloading pdf bytes as pdf.*/
              if(pdfResponseType != null && pdfResponseType.getFile() != null){
                  bytes = pdfResponseType.getFile().getDocument();
                  /*set the response header to enable download*/
                  response.setContentType("application/OCTET-STREAM");
                  response.setHeader("Content-Disposition", "attachment;filename=\"" + letterName + ".pdf\"");
                  response.setHeader("Pragma", "cache");
                  response.setHeader("Cache-Control", "private");
                  out.clear();
                  response.getOutputStream().write(bytes);
              }
          }
          else{
              log.error("Letter id does not exists.");
          }
      %>
      ```

## Descargar PDF plano de una carta utilizando la funcionalidad personalizada {#download-flat-pdf-of-a-letter-using-the-custom-functionality}

Después de haber agregado funcionalidad personalizada para descargar PDF plano de sus cartas, puede seguir los siguientes pasos para descargar una versión PDF plana de la carta seleccionada:

1. Vaya a `https://'[server]:[port]'/[ContextPath]/projects.html` e inicie sesión.

1. Seleccione **Forms > Letras**. Correspondence Management enumera las cartas disponibles en el sistema.
1. Haga clic en **Select** y, a continuación, haga clic en una letra para seleccionarla.
1. Seleccione **Más** > **&lt;Descargar PDF plano>** (la funcionalidad personalizada creada con las instrucciones de este artículo). Aparece el cuadro de diálogo Descargar carta como PDF.

   El nombre del elemento de menú, la funcionalidad y el texto alternativo dependen de la personalización creada en [Escenario: Agregue un comando a la interfaz de usuario de la lista Letras para descargar la versión PDF plana de una carta.](#addcommandtoletters)

   ![Funcionalidad personalizada: Descargar PDF plano](assets/5_downloadflatpdf.png)

1. En el cuadro de diálogo Descargar carta como PDF, seleccione el XML relevante desde el que desea rellenar los datos en el PDF.

   >[!NOTE]
   >
   >Antes de descargar la carta como PDF plano, puede crear el archivo XML con los datos de la carta utilizando la opción **Crear informe**.

   ![Descargar carta como PDF](assets/6_downloadflatpdf.png)

   La carta se descarga en su ordenador como PDF plano.

