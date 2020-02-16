---
title: Depuración de formularios HTML5
seo-title: Depuración de formularios HTML5
description: La lista de documentos muestra los pasos para solucionar varios problemas conocidos.
seo-description: La lista de documentos muestra los pasos para solucionar varios problemas conocidos.
uuid: df1835aa-6033-4ecb-97c8-4c3b7b96b943
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Depuración de formularios HTML5 {#debugging-html-forms}

Este documento incluye varios escenarios de solución de problemas. Para cada escenario, se proporcionan algunos pasos para solucionar el problema. Siga estos pasos y, si el problema persiste, configure el Registrador para obtener y revisar los registros de errores y advertencias. Para obtener más información sobre el registro de formularios HTML5, consulte [Generación de registros para formularios](/help/forms/using/enable-logs.md)HTML5.

## Problema: Al procesar el formulario, veo la página de excepción org.apache.sling.api.SlingException {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

En los detalles de la excepción, busque la palabra **causada por**.

El motivo probable es que uno o más parámetros de la dirección URL sean incorrectos.

Compruebe los siguientes parámetros:

<table>
 <tbody>
  <tr>
   <td><strong>Parámetro</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>template</td>
   <td>El nombre de archivo de la plantilla</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>La ruta donde residen la plantilla y los recursos asociados</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Ruta absoluta del archivo de datos que se combina con la plantilla.<br /> Nota: La ruta define la ruta absoluta del archivo de datos.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>Bytes de datos codificados UTF-8 que se combinan con la plantilla.</td>
  </tr>
 </tbody>
</table>

## Problema: No se puede procesar un formulario (se muestra un mensaje de error) {#problem-unable-to-render-a-form-an-error-message-is-displayed}

1. Asegúrese de que los parámetros especificados son correctos. Para obtener información detallada sobre los parámetros, consulte Parámetros [de procesamiento](/help/forms/using/debug.md#main-pars-table).
1. Inicie sesión en el Administrador de paquetes CRX (en https://&lt;server>:&lt;port>/crx/packmgr/index.jsp) y compruebe si los siguientes paquetes están correctamente instalados:

   * adobe-lc-forms-content-pkg-&lt;versión>.zip
   * adobe-lc-forms-Runtime-pkg-&lt;versión>.zip

1. Inicie sesión en la consola web de CQ (Felix Console) en https://&lt;server>:&lt;port>/system/console/buncles.

   Asegúrese de que el estado de los siguientes paquetes está &quot;activo&quot;:

   * scala-lang.bundle [osgi]
   (adobe.livecyclcom.com-lang.bundle)

   * Adobe XFA Forms Renderer
   (com.adobe.livecycle.adobe-lc-forms-core)

   * Adobe XFA Forms LC Connector
   (com.adobe.livecycle.adobe-lc-forms-lc-Connector)

## Problema: El formulario se procesa sin estilos {#problem-form-renders-without-styles}

1. En el explorador, abra Herramientas **para desarrolladores**. Asegúrese de que profile.css está disponible.
1. Si el archivo profile.css no está disponible, inicie sesión en CRX DE en https://&lt;server>:&lt;port>/crx/de.
1. En la jerarquía de carpetas de la izquierda, navegue a /etc/clientlibs/fd/xfaforms/. Abra los archivos css.txt que aparecen en las carpetas.

   * El perfil.
   * tiempo de ejecución
   * scrollnav
   * toolbar
   * xfalib

1. Compruebe que los archivos mencionados dentro de css.txt están presentes en CRX DE lite en /libs/fd/xfaforms/clientlibs/xfalib/css.

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. Si los archivos mencionados no están disponibles, instale de nuevo el paquete adobe-lc-forms-Runtime-pkg-&lt;version>.zip.

### Problema: Error inesperado {#problem-unexpected-error-encountered}

1. En la dirección URL del formulario, agregue un parámetro de consulta debugClientLibs y defina su valor en true (por ejemplo: https://&lt;servidor>:&lt;puerto>/content/xfaforms/profiles/test.html?contentRoot=&lt;ruta de acceso>&amp;template=&lt;nombre del archivo xdp>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. En el navegador de escritorio, como Chrome, vaya a Herramientas para desarrolladores -> Consola.
1. Abra los registros para identificar el tipo de error. Para obtener información detallada sobre los registros, consulte [registros para formularios](/help/forms/using/enable-logs.md)HTML5.
1. Vaya a Herramientas del desarrollador -> Consola. Utilice el seguimiento de pila para localizar el código que está causando el error. Depurar el error para resolver el problema.

   >[!NOTE]
   >
   >Si se trata de un error de secuencia de comandos, compruebe también si se produce el mismo problema durante la representación en PDF del formulario. Si es así, la lógica de secuencias de comandos del formulario presenta un problema.

## Problema: No se puede enviar el formulario {#problem-unable-to-submit-the-form}

1. Asegúrese de que tiene derechos para acceder al servidor AEM y de que está conectado al servidor.
1. Compruebe que el parámetro submitUrl es correcto.
1. Habilite los registros del lado del cliente como se indica en [Registros para los formularios](/help/forms/using/enable-logs.md) HTML5 mediante la opción de depuración **1-a5-b5-c5**. A continuación, procese el formulario y haga clic en Enviar. Abra la consola de depuración del navegador y compruebe si hay algún error.
1. Localice los registros del servidor como se indica en [Registros para los formularios](/help/forms/using/enable-logs.md)HTML5. Compruebe si hubo algún error en los registros del servidor durante el envío.

## Problema: Los mensajes de error localizados no se muestran {#problem-localized-error-messages-do-not-display}

1. Procese el formulario con el parámetro de consulta adicional **debugClientLibs=true** en el navegador de escritorio y, a continuación, vaya a Herramientas de desarrollador -> Recursos y compruebe el archivo I18N.css.
1. Si el archivo no está disponible, inicie sesión en CRX DE en https://&lt;server>:&lt;port>/crx/de.
1. En la jerarquía de carpetas de la izquierda, vaya a /libs/fd/xfaforms/clientlibs/I18N y asegúrese de que existen los siguientes archivos y carpetas:

   * Namespace.js
   * LogMessages.js
   * Carpetas para idiomas

1. Si alguno de los archivos o carpetas anteriores no existe, instale de nuevo el paquete **adobe-lc-forms-Runtime-pkg-&lt;version>.zip** .
1. Vaya a la carpeta que tiene el mismo nombre que el nombre de la configuración regional y compruebe su contenido. La carpeta debe contener los siguientes archivos:

   * I18N.js
   * js.txt

1. Compruebe el contenido de js.txt y asegúrese de que tiene las siguientes entradas.

   ```
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## Problema: La imagen no se muestra {#problem-image-not-showing-up}

1. Asegúrese de que la dirección URL de la imagen sea correcta.
1. Compruebe si el explorador admite este tipo de imagen.
1. En los detalles de la excepción, busque la palabra **causada por**.

   El motivo probable es que uno o más parámetros de la dirección URL sean incorrectos.

   Compruebe los siguientes parámetros:
Texto del paso

<table>
 <tbody>
  <tr>
   <td><strong>Parámetro</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>template</td>
   <td>El nombre de archivo de la plantilla</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>La ruta donde residen la plantilla y los recursos asociados</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Ruta absoluta del archivo de datos que se combina con la plantilla.<br /> Nota: La ruta define la ruta absoluta del archivo de datos.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>Bytes de datos codificados UTF-8 que se combinan con la plantilla.</td>
  </tr>
 </tbody>
</table>

1. En el navegador de escritorio, vaya a Herramientas para desarrolladores -> Recursos.

   Si se muestra la imagen, marque la casilla de verificación situada en el lado izquierdo de Marcos.

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
