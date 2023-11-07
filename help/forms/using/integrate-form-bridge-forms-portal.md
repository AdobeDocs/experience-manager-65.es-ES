---
title: Integrar Form Bridge con el portal personalizado para formularios HTML5
seo-title: Integrating Form Bridge with custom portal for HTML5 forms
description: Puede utilizar la API de FormBridge para obtener o establecer los valores de los campos de formulario de la página HTML y enviar el formulario.
seo-description: You can use the FormBridge API to get or set the values of form fields from the HTML page and submit the form.
uuid: c8911f82-1a25-47a5-9a06-19b5dce74a2c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bd9bf095-d74d-458c-afe7-fab04050849d
docset: aem65
feature: Mobile Forms
exl-id: 89118bb8-6ec8-4048-b3d6-5c73a9eea33e
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 87%

---

# Integrar Form Bridge con el portal personalizado para formularios HTML5{#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge es una API de Forms Bridge de HTML5 que le permite interactuar con un formulario. Para obtener la referencia de la API de FormBridge, consulte [Referencia de la API de FormBridge](/help/forms/using/form-bridge-apis.md).

Puede utilizar la API de FormBridge para obtener o establecer los valores de los campos de formulario de la página HTML y enviar el formulario. Por ejemplo, puede utilizar la API para crear una experiencia similar a un asistente.

Una aplicación de HTML existente puede utilizar la API de FormBridge para interactuar con un formulario e incrustarlo en la página de HTML. Puede seguir los siguientes pasos para establecer el valor de un campo mediante la API de Form Bridge.

## Integración de formularios HTML5 en una página web {#integrating-html-forms-to-a-web-page}

1. **Elegir un perfil o crear un perfil**

   1. En la interfaz CRX DE, vaya a: `https://'[server]:[port]'/crx/de`.
   1. Inicie sesión con credenciales de administrador.
   1. Cree un perfil o seleccione un perfil existente.

      Para obtener más información sobre cómo crear un perfil, consulte [Creación de un perfil](/help/forms/using/custom-profile.md).

1. **Modificación del perfil del HTML**

   Incluya el tiempo de ejecución de XFA, la biblioteca de configuración regional XFA y el fragmento de HTML del formulario XFA en el procesador de perfiles, diseñe la página web y coloque el formulario en la página.

   Por ejemplo, utilice el siguiente fragmento de código para crear una aplicación con dos campos de entrada y un formulario para mostrar la interacción entre el formulario y una aplicación externa.

   ```xml
   <%@ page session="false"
                  contentType="text/html; charset=utf-8"%><%
   %><%@ taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
   %><!DOCTYPE html>
   <html manifest="${param.offlineSpec}">
       <head>
          <cq:include script="formRuntime.jsp"/>
           <!-- Portal Scripts and Styles -->
          <cq:include script="portalheader.jsp"/>
       </head>
       <body>
           <div id="leftdiv" >
               <div id="leftdivcontentarea">
                   <!-- Portal Body -->
                 <cq:include script="portalbody.jsp"/>
               </div>
           </div>
           <div id="rightdiv">
               <div id="formBody">
               <cq:include script="config.jsp"/>
               <!-- Form body -->
               <cq:include script="formBody.jsp"/>
               <!  --To assist in page transitions -- add navigation, based on scrolling -->
               <cq:include  script="../nav/scroll/nav_footer.jsp"/>
               <cq:include script="footer.jsp"/>
               </div>
           </div>
       </body>
   </html>
   ```

   >[!NOTE]
   >
   >La **línea 9**, contiene una referencia JSP adicional para estilos CSS y archivos JavaScript para diseñar la página.
   >
   >
   >La etiqueta &lt;div id=&quot;rightdiv&quot;> de la **línea 18** contiene el fragmento de HTML del formulario XFA.
   >
   >
   La página tiene un estilo de dos contenedores: **left** y **right**. El contenedor derecho (right) contiene el formulario. El contenedor izquierdo (left) contiene dos campos de entrada y parte de la página HTML externa.
   >
   >
   La siguiente captura de pantalla muestra cómo se muestra el formulario en un explorador.

   ![portal](assets/portal.jpg)

   El lado izquierdo es parte de la **página HTML**. El lado derecho que contiene los campos es el **formulario XFA**.

1. **Acceso a los campos del formulario desde la página**

   El siguiente es un ejemplo de script que puede agregar para definir valores en un campo de formulario.

   Por ejemplo, si desea establecer el **NombreEmpleado** usando los valores de los campos **Nombre** y **Apellidos**, llame a la función **window.formBridge.setFieldValue**.

   Del mismo modo, puede leer el valor llamando a la API **window.formBridge.getFieldValue**.

   ```javascript
   $(function() {
               $(".input").blur(function() {
                   window.formBridge.setFieldValue(
                               'xfa.form.form1.#subform[0].EmployeeName',
                                $("#lname").val()+' '+$("#fname").val()
                              )
                   });
           });
   ```
