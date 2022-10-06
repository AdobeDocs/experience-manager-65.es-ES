---
title: Depuración de formularios HTML5
seo-title: Debugging HTML5 forms
description: Los pasos de la lista de documentos para solucionar varios problemas conocidos.
seo-description: The document list steps to troubleshoot various known issues.
uuid: df1835aa-6033-4ecb-97c8-4c3b7b96b943
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
feature: Mobile Forms
exl-id: 7330c03f-7102-43c0-aac6-825cce8a113d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 1%

---

# Depuración de formularios HTML5 {#debugging-html-forms}

Este documento incluye varios casos de resolución de problemas. Para cada escenario, se proporcionan algunos pasos para solucionar el problema. Siga estos pasos y, si el problema persiste, configure el registrador para obtener y revisar los registros en busca de errores/advertencias. Para obtener más información sobre el registro de formularios de HTML5, consulte [Generación de registros para formularios HTML5](/help/forms/using/enable-logs.md).

## Problema: Al procesar el formulario, veo la página de excepciones org.apache.sling.api.SlingException {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

En los detalles de la excepción, busque palabra **causado por**.

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
   <td>bytes de datos codificados UTF-8 que se combinan con la plantilla.</td>
  </tr>
 </tbody>
</table>

## Problema: No se puede procesar un formulario (se muestra un mensaje de error) {#problem-unable-to-render-form}

1. Asegúrese de que los parámetros especificados sean correctos. Para obtener información detallada sobre los parámetros, consulte [Parámetros de procesamiento](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page).
1. Inicie sesión en el Administrador de paquetes CRX (en https://&lt;server>:&lt;port>/crx/packmgr/index.jsp) y compruebe si los siguientes paquetes están correctamente instalados:

   * adobe-lc-forms-content-pkg&lt;version>.zip
   * adobe-lc-forms-runtime-pkg&lt;version>.zip

1. Inicie sesión en la consola web de CQ (Consola Felix) en https://&lt;server>:&lt;port>/system/console/bundles.

   Asegúrese de que el estado de los siguientes paquetes esté &quot;activo&quot;:

   * escala-lang.bundle [osgi]

   (adobe.liveccom.clem-lang.bundle)

   * Procesador de Forms XFA de Adobe

   (com.adobe.livecycle.adobe-lc-forms-core)

   * Conector XFA Forms LC de Adobe

   (com.adobe.livecycle.adobe-lc-forms-lc-connector)

## Problema: El formulario se procesa sin estilos {#problem-form-renders-without-styles}

1. En el explorador, abra **Herramientas para desarrolladores**. Asegúrese de que profile.css está disponible.
1. Si el archivo profile.css no está disponible, inicie sesión en CRX DE en https://&lt;server>:&lt;port>/crx/de.
1. En la jerarquía de carpetas de la izquierda, vaya a /etc/clientlibs/fd/xfaforms/. Abra los archivos css.txt que aparecen en las carpetas.

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

1. Si los archivos mencionados no están disponibles, instale adobe-lc-forms-runtime-pkg-&lt;version>paquete .zip de nuevo.

### Problema: Error inesperado encontrado {#problem-unexpected-error-encountered}

1. En la dirección URL del formulario, agregue un parámetro de consulta debugClientLibs y establezca su valor en true (Por ejemplo: https://&lt;server>:&lt;port>/content/xfaforms/profiles/test.html?contentRoot=&lt;some path=&quot;&quot;>&amp;template=&lt;name of=&quot;&quot; xdp=&quot;&quot; file=&quot;&quot;>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. En el navegador de escritorio, como chrome, vaya a Herramientas para desarrolladores -> Consola.
1. Abra los registros para identificar el tipo de error. Para obtener información detallada sobre los registros, consulte [registros para formularios HTML5](/help/forms/using/enable-logs.md).
1. Vaya a Herramientas para desarrolladores -> Consola. Utilice el seguimiento de pila para localizar el código que está causando el error. Depurar el error para resolver el problema.

   >[!NOTE]
   >
   >Si se trata de un error de secuencia de comandos, compruebe si el mismo problema se produce durante la representación del PDF del formulario. Si es así, hay un problema en la lógica de secuencias de comandos del formulario.

## Problema: No se puede enviar el formulario {#problem-unable-to-submit-the-form}

1. Asegúrese de que tiene derechos para acceder al servidor de AEM y de que está conectado al servidor.
1. Compruebe que el parámetro submitUrl sea correcto.
1. Habilite los registros del lado del cliente como se menciona en [Registros para los formularios de HTML5](/help/forms/using/enable-logs.md) uso de la opción debug como **1-a5-b5-c5**. A continuación, procese el formulario y haga clic en enviar. Abra la consola de depuración del explorador y compruebe si hay un error.
1. Localice los registros del servidor como se menciona en [Registros para los formularios de HTML5](/help/forms/using/enable-logs.md). Compruebe si hubo algún error en los registros del servidor durante el envío.

## Problema: Los mensajes de error localizados no se muestran {#problem-localized-error-messages-do-not-display}

1. Representar el formulario con un parámetro de consulta adicional **debugClientLibs=true** en el navegador de escritorio y, a continuación, vaya a Herramientas para desarrolladores -> Recursos y busque el archivo I18N.css.
1. Si el archivo no está disponible, inicie sesión en CRX DE en https://&lt;server>:&lt;port>/crx/de.
1. En la jerarquía de carpetas de la izquierda, vaya a /libs/fd/xfaforms/clientlibs/I18N y asegúrese de que existen los siguientes archivos y carpetas:

   * Namespace.js
   * LogMessages.js
   * Carpetas para idiomas

1. Si alguno de los archivos o carpetas anteriores no existe, instale la variable **adobe-lc-forms-runtime-pkg&lt;version>.zip** de nuevo.
1. Vaya a la carpeta que tiene el mismo nombre que la configuración regional y compruebe su contenido. La carpeta debe contener los siguientes archivos:

   * I18N.js
   * js.txt

1. Compruebe el contenido de js.txt y asegúrese de que tiene las siguientes entradas.

   ```javascript
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## Problema: La imagen no aparece {#problem-image-not-showing-up}

1. Asegúrese de que la dirección URL de la imagen sea correcta.
1. Compruebe si su navegador admite este tipo de imagen.
1. En los detalles de la excepción, busque palabra **causado por**.

   El motivo probable es que uno o más parámetros de la dirección URL sean incorrectos.

   Compruebe los siguientes parámetros: Texto de paso

<table>
 <tbody>
  <tr>
   <td><strong>Parámetro</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>plantilla</td>
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
   <td>bytes de datos codificados UTF-8 que se combinan con la plantilla.</td>
  </tr>
 </tbody>
</table>

1. En el navegador de escritorio, vaya a Herramientas para desarrolladores -> Recursos.

   Marque en el lado izquierdo en Fotogramas si la imagen se muestra.
