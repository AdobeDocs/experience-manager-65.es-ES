---
title: Personalizar mensajes de error para formularios HTML5
seo-title: Customizing error messages for HTML5 forms
description: Aprenda a personalizar la visualización de mensajes de error para formularios HTML5, incluido cómo cambiar su posición y apariencia.
seo-description: Learn how to customize the display of error messages for HTML5 forms including how to change their position and appearance.
uuid: 6f48b64e-858f-4323-ad50-88e25f3c2e3d
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 44e49789-9075-41b3-bce8-03e8efce2d5a
feature: Mobile Forms
exl-id: c4ae53a3-8de1-4985-a73e-829749de9814
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 100%

---

# Personalizar mensajes de error para formularios HTML5 {#customizing-error-messages-for-html-forms}

En los formularios HTML5, de forma predeterminada, los mensajes de error y las advertencias tienen una posición y aspecto fijos (fuente y color), el error se muestra solo para un campo seleccionado y solo se muestra un error.

El artículo proporciona los pasos para personalizar los mensajes de error de formularios HTML5,

* cambiar el aspecto y la posición de los mensajes de error. Puede hacer que aparezca un error en la parte superior, inferior y derecha de cualquier campo.
* mostrar mensajes de error para varios campos en un momento determinado.
* mostrar el error independientemente de si un campo está seleccionado o no.

## Personalizar mensajes de error  {#customizing-error-messages-nbsp}

Antes de personalizar los mensajes de error, descargue y extraiga el paquete adjunto (CustomErrorManager-1.0-SNAPSHOT.zip).

Después de extraer el paquete, abra la carpeta CustomErrorManager-1.0-SNAPSHOT. Contiene carpetas jcr_root y META-INF. Estas carpetas contienen los archivos CSS y .JS necesarios para personalizar el mensaje de error.

[Obtener archivo](assets/customerrormanager-1.0-snapshot.zip)

### Personalizar la posición de los mensajes de error  {#customizing-the-position-of-error-messages-nbsp}

Para personalizar la posición del mensaje de error, agregue la etiqueta &lt;div> a cada campo de error y advertencia, coloque la etiqueta &lt;div> a la izquierda o a la derecha, y aplique estilos css en la etiqueta &lt;div>. Para ver los pasos detallados, consulte el procedimiento que se muestra a continuación:

1. Navegue hasta la carpeta `CustomErrorManager-1.0-SNAPSHOT` y abra la carpeta `etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript`.
1. Abra el archivo `customErrorManager.js` para editarlo. La función `markError` del el archivo acepta los siguientes parámetros:

   |  |  |
   |---|---|
   | jqWidget | jqWidget es el controlador del widget. |
   | msg | contiene el mensaje de error. |
   | type | indica si se trata de un error o de una advertencia. |

1. En la implementación predeterminada, los mensajes de error aparecen a la derecha del campo. Para que los mensajes de error aparezcan en la parte superior utilice el siguiente código.

   ```javascript
   markError: function (jqWidget, msg, type) {
               var element = jqWidget.element,                                //Gives the div containing widget
                   pos = $(element).offset(),                          //Calculates the position of the div in the view port
                                                                   msgHeight = xfalib.view.util.TextMetrics.measureExtent(msg).height + 5;  //Calculating the height of the Error Message
                   styles = {};
                   styles.left = pos.left + "px";         // Assign the desired left position using pos.left. Here it is calculated for exact left of the field
                   styles.top = pos.top - msgHeight + "px";  // Assign the desired top position using pos.top. Here it is calculated for top of the field
               if (type != "warning") {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the warning div if it is not present already
                       jqWidget.errorDiv=$("<div id='customError'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the warning div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               } else {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the error div if it is not present already
                       jqWidget.errorDiv=$("<div id='customWarning'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the error div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               }
   
           },
   ```

1. Guarde y cierre el archivo.
1. Navegue hasta la carpeta `CustomErrorManager-1.0-SNAPSHOT` y cree un archivo de carpetas jcr_root y META-INF. Cambie el nombre del archivo a CustomErrorManager-1.0-SNAPSHOT.zip.
1. Utilice el administrador de paquetes para cargar e instalar el paquete.

## Mostrar mensajes de error para varios campos  {#display-error-messages-for-multiple-fields-nbsp}

Utilice el paquete adjunto para mostrar simultáneamente los mensajes de error de todos los campos. Para mostrar un solo mensaje de error, utilice el perfil predeterminado.

### Personalizar la apariencia de los mensajes de error.  {#customizing-the-appearance-of-error-messages-nbsp}

1. Navegue hasta la carpeta etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css.

1. Abra el archivo sample.css para editarlo. El archivo css contiene 2 ids- #customError, #customWarning. Puede utilizar estos identificadores para cambiar varias propiedades como el color, el tamaño de la fuente, etc.

   Utilice el siguiente código para cambiar el tamaño de la fuente y el color de los mensajes de error/advertencia.

   ```css
   #customError {
   color: #0000FF; // it changes the color of Error Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 24px;  // it changes the font size of Error Message
   z-index:5;
   }
   
   #customWarning {
   color: #00FF00;  // it changes the color of Warning Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 18px;   // it changes the font size of Warning Message
   z-index:5;
   }
   
   Save the changes.
   ```

1. Guarde y cierre el archivo.
1. Navegue hasta la carpeta CustomErrorManager-1.0-SNAPSHOT y cree un archivo de carpetas jcr_root y META-INF. Cambie el nombre del archivo a CustomErrorManager-1.0-SNAPSHOT.zip.
1. Utilice el administrador de paquetes para cargar e instalar el paquete.

## Procese el formulario con el nuevo perfil.  {#render-the-form-with-the-new-profile-nbsp}

De forma predeterminada, los formularios HTML5 utilizan un perfil predeterminado: https://&lt;server>/content/xfaforms/profiles/default.html?contentRoot=&lt;xdp location>&amp;template=&lt;name of the xdp>

Para ver un formulario con los mensajes de error personalizados, procese el formulario con un perfil de error: https://&lt;server>/content/xfaforms/profiles/error.html?contentRoot=&lt;xdp location>&amp;template=&lt;name of the xdp>

>[!NOTE]
>
>El paquete adjunto instala el perfil de error.
