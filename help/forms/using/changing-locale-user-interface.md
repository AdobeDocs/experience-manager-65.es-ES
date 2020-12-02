---
title: Cambio de la configuración regional de la interfaz de usuario del espacio de trabajo de AEM Forms
seo-title: Cambio de la configuración regional de la interfaz de usuario del espacio de trabajo de AEM Forms
description: Cómo modificar el espacio de trabajo de AEM Forms para localizar texto, categorías contraídas, colas y procesos, y el selector de fechas de la interfaz.
seo-description: Cómo modificar el espacio de trabajo de AEM Forms para localizar texto, categorías contraídas, colas y procesos, y el selector de fechas de la interfaz.
uuid: c89ff150-a36e-45cc-99a6-8768dbe58eab
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 89f9d666-28e2-4201-8467-ae90693ca5d2
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---


# Cambio de la configuración regional de la interfaz de usuario del área de trabajo de AEM Forms{#changing-the-locale-of-aem-forms-workspace-user-interface}

El espacio de trabajo de AEM Forms ofrece compatibilidad inmediata con los idiomas inglés, francés, alemán y japonés. También permite localizar la interfaz de usuario del espacio de trabajo de AEM Forms en cualquier otro idioma.

Para localizar la interfaz de usuario del espacio de trabajo de AEM Forms según el idioma que elija:

* Localizar texto del espacio de trabajo de AEM Forms.
* Localice categorías contraídas, colas y procesos.
* Localizar selector de fechas

Antes de realizar los pasos anteriores, asegúrese de seguir los pasos enumerados en [Pasos genéricos para la personalización del espacio de trabajo de AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md).

>[!NOTE]
>
>Para cambiar el idioma de la pantalla de inicio de sesión del espacio de trabajo de AEM Forms, consulte [Creación de una nueva pantalla de inicio de sesión](../../forms/using/creating-new-login-screen.md).

## Localización de texto {#localizing-text}

Realice los siguientes pasos para agregar soporte para un idioma *Nuevo* y el código de configuración regional del explorador *nuevo*.

1. Inicie sesión en el CRXDE Lite.
La dirección URL predeterminada del CRXDE Lite es `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Vaya a la ubicación `apps/ws/locales` y cree una nueva carpeta `nw.`
1. Copie el archivo `translation.json`desde la ubicación `/apps/ws/locales/en-US` a la ubicación `/apps/ws/locales/nw`.
1. Vaya a `/apps/ws/locales/nw` y abra `translation.json` para editarlo. Realice cambios específicos de la configuración regional en el archivo translate.json.

   Los siguientes ejemplos contienen el archivo translate.json para las configuraciones regionales en inglés y francés del espacio de trabajo de AEM Forms.

   ![translate_json_in_](assets/translation_json_in_en.png) ![entranslation_json_in_fr](assets/translation_json_in_fr.png)

## Localización de categorías contraídas, colas y procesos {#localizing-collapsed-categories-queues-and-processes}

El espacio de trabajo de AEM Forms utiliza imágenes para mostrar encabezados de categorías, colas y procesos. Es necesario un paquete de desarrollo para localizar estos encabezados. Para obtener información detallada sobre la creación de paquetes de desarrollo, consulte [Generación de código de área de trabajo de AEM Forms.](introduction-customizing-html-workspace.md#building-html-workspace-code)

En los pasos siguientes, se da por hecho que los nuevos archivos de imagen localizados son *Categorías_nw.png*, *Queue_nw.png* y *Processes_nw.png*. La anchura recomendada de las imágenes es de 19 píxeles.

>[!NOTE]
>
>Para buscar el código de configuración regional del idioma del explorador. Abra `https://'[server]:[port]'/lc/libs/ws/Locale.html`.

![contraer_paneles_imagen](assets/collapsing_panels_image.png)

Siga estos pasos para localizar las imágenes:

1. Con un cliente WebDAV, coloque los archivos de imagen en la carpeta */apps/ws/images*.
1. Vaya a */apps/ws/css*. Abra *newStyle.css* para editar y agregue las siguientes entradas:

   ```css
   #categoryListBar .content.nw {
        background: #3e3e3e url(../images/Categories_nw.png) no-repeat 10px 10px;
    }
   
   #filterListBar .content.nw {
       background: #3e3e3e url(../images/Queues_nw.png) no-repeat 10px 10px;
   }
   
   #processNameListBar .content.nw {
       background: #3e3e3e url(../images/Processes_nw.png) no-repeat 10px 10px;
   }
   ```

1. Realice todos los cambios semánticos enumerados en el artículo [Personalización del espacio de trabajo](../../forms/using/introduction-customizing-html-workspace.md).
1. Vaya a la carpeta *js/Runtime/Utility* y abra el archivo *usersession.js* para editarlo.
1. Busque el código que aparece en el bloque de código original y agregue la condición *lang !== &#39;nw&#39;* a la sentencia if:

   ```javascript
   // Orignal code
   setLocale = function () {
           var lang = $.trim(i18n.lng());
           if (lang === null || lang === '' || (lang !== 'fr-FR' && lang !== 'de-DE' && lang !== 'ja-JP')) {
               window.lcWorkspace.locale = 'en-US';
           } else {
               window.lcWorkspace.locale = lang;
           }
       }
   ```

   ```javascript
   //new code
    setLocale = function () {
           var lang = $.trim(i18n.lng());
           if (lang === null || lang === '' || (lang !== 'fr-FR' && lang !== 'de-DE' && lang !== 'ja-JP' && lang !== 'nw')) {
               window.lcWorkspace.locale = 'en-US';
           } else {
               window.lcWorkspace.locale = lang;
           }
       }
   ```

## Localización del selector de fechas {#localizing-date-picker}

Se requiere un paquete de desarrollo para localizar la API *datepicker*. Para obtener información detallada sobre la creación de paquetes de desarrollo, consulte [Generación de código de área de trabajo de AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code).

1. Descargue y extraiga el [paquete de IU de jQuery](https://jqueryui.com/download/all/), vaya a *&lt;paquete de IU de jquery extraído>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n.
1. Copie el archivo jquery.ui.datepicker-nw.js para el código de configuración regional ahora en las aplicaciones/ws/js/libs/jqueryui y realice cambios específicos de configuración regional en el archivo.
1. Vaya a `apps/ws/js` y abra el archivo `jquery.ui.datepicker-nw.js` para editarlo.
1. En el archivo main.js, cree un alias para `jquery.ui.datepicker-nw.js.` El código para crear un alias para el archivo `jquery.ui.datepicker-nw.js` es:

   ```javascript
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. Utilice el alias `jqueryuidatepickernw` para incluir el archivo `jquery.ui.datepicker-nw.js` en todos los archivos que utilicen datepicker. El selector de datos se utiliza en los siguientes archivos:

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`

   El código de muestra siguiente muestra cómo agregar la entrada de jquery.ui.datepicker-nw.js:

   ```json
   //Original Code
   define([
       'jquery',
       'underscore',
       'backbone',
       'jqueryui',
       'jqueryuidatepickerja',
       'jqueryuidatepickerde',
       'jqueryuidatepickerfr',
       'slimscroll',
       'usersearchview',
       'logmanagerutil',
       'loggerutil'
   ], function ($, _, Backbone, jQueryUI, jQueryUIDatePickerJA, jQueryUIDatePickerDE, jQueryUIDatePickerFR, slimScroll, UserSearch, LogManager, Logger) {
   ```

   ```json
   // Code with Date Picker alias for new language
   define([
       'jquery',
       'underscore',
       'backbone',
       'jqueryui',
       'jqueryuidatepickerja',
       'jqueryuidatepickerde',
       'jqueryuidatepickerfr',
       'jqueryuidatepickernw', // Date Picker alias
       'slimscroll',
       'usersearchview',
       'logmanagerutil',
       'loggerutil'
   ], function ($, _, Backbone, jQueryUI, jQueryUIDatePickerJA, jQueryUIDatePickerDE, jQueryUIDatePickerFR, jQueryUIDatePickerNW, slimScroll, UserSearch, LogManager, Logger) {
   ```

1. En todos los archivos que utilizan la API de datepicker, cambie la configuración predeterminada de la API de datepicker. La API de datepicker se utiliza en los siguientes archivos:

   * apps\ws\js\runtime\views\searchtemplatedetails.js
   * apps\ws\js\runtime\views\outofoffice.js

   Cambie el siguiente código para agregar la nueva configuración regional:

   ```javascript
   if (locale === 'ja-JP') {
      $.datepicker.setDefaults($.datepicker.regional.ja);
   } else if (locale === 'de-DE') {
      $.datepicker.setDefaults($.datepicker.regional.de);
   } else if (locale === 'fr-FR') {
      $.datepicker.setDefaults($.datepicker.regional.fr);
   } else {
      $.datepicker.setDefaults($.datepicker.regional['']);
   }
   ```

   ```javascript
   if (locale === 'ja-JP') {
       $.datepicker.setDefaults($.datepicker.regional.ja);
   } else if (locale === 'de-DE') {
       $.datepicker.setDefaults($.datepicker.regional.de);
   } else if (locale === 'fr-FR') {
       $.datepicker.setDefaults($.datepicker.regional.fr);
   } else if (locale === 'nw') {
       $.datepicker.setDefaults($.datepicker.regional.nw);
   } else {
       $.datepicker.setDefaults($.datepicker.regional['']);
   }
   ```
