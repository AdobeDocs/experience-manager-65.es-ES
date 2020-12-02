---
title: Integración de Form Bridge con un portal personalizado para formularios HTML5
seo-title: Integración de Form Bridge con un portal personalizado para formularios HTML5
description: Puede utilizar la API de FormBridge para obtener o establecer los valores de los campos de formulario desde la página HTML y enviar el formulario.
seo-description: Puede utilizar la API de FormBridge para obtener o establecer los valores de los campos de formulario desde la página HTML y enviar el formulario.
uuid: c8911f82-1a25-47a5-9a06-19b5dce74a2c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bd9bf095-d74d-458c-afe7-fab04050849d
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---


# Integración de Form Bridge con un portal personalizado para formularios HTML5{#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge es una API de puente de formularios HTML5 que le permite interactuar con un formulario. Para obtener la referencia de la API de FormBridge, consulte [Referencia de la API de FormBridge](/help/forms/using/form-bridge-apis.md).

Puede utilizar la API de FormBridge para obtener o establecer los valores de los campos de formulario desde la página HTML y enviar el formulario. Por ejemplo, puede utilizar API para crear una experiencia similar a un asistente.

Una aplicación HTML existente puede aprovechar la API de FormBridge para interactuar con un formulario e incrustarlo en la página HTML. Puede utilizar los siguientes pasos para establecer el valor de un campo mediante la API de puente de formulario.

## Integración de formularios HTML5 en una página web {#integrating-html-forms-to-a-web-page}

1. **Elija un Perfil o cree un Perfil**

   1. En la interfaz CRX DE, navegue a: `https://'[server]:[port]'/crx/de`.
   1. Inicie sesión con credenciales de administrador.
   1. Cree un perfil o elija un perfil existente.

      Para obtener más información sobre cómo crear un perfil, consulte [Creación de un nuevo Perfil](/help/forms/using/custom-profile.md).

1. **Modificación del Perfil HTML**

   Incluya el tiempo de ejecución XFA, la biblioteca de configuración regional XFA y el fragmento de código HTML de formulario XFA en el procesador de perfil, diseñe la página web y coloque el formulario dentro de la página web.

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
   >La **línea 9** contiene una referencia JSP adicional para estilos CSS y archivos JavaScript para diseñar la página.
   >
   >
   >La etiqueta &lt;div id=&quot;rightdiv&quot;> de la **línea 18** contiene el fragmento HTML del formulario XFA.
   La página tiene dos contenedores: **izquierda** y **derecha**. El contenedor correcto tiene el formulario. El contenedor izquierdo tiene dos campos de entrada y parte de la página HTML externa.
   La siguiente captura de pantalla muestra cómo se muestra el formulario en un explorador.

   ![portal](assets/portal.jpg)

   El lado izquierdo es parte de la **página HTML**. El lado derecho que contiene los campos es el **formulario xfa**.

1. **Acceso a los campos del formulario desde la página**

   A continuación se muestra una secuencia de comandos de ejemplo que puede agregar para definir valores en un campo de formulario.

   Por ejemplo, si desea establecer **NombreEmpleado** utilizando los valores de la función Campos **Nombre** y **Apellido**, llame a la función **window.formBridge.setFieldValue**.

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
