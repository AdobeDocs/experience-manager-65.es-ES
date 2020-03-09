---
title: Compatibilidad con nuevas configuraciones regionales para la localización de formularios adaptables
seo-title: Compatibilidad con nuevas configuraciones regionales para la localización de formularios adaptables
description: AEM Forms permite añadir nuevas configuraciones regionales para localizar formularios adaptables. Las configuraciones regionales admitidas de forma predeterminada son inglés, francés, alemán y japonés.
seo-description: AEM Forms permite añadir nuevas configuraciones regionales para localizar formularios adaptables. Las configuraciones regionales admitidas de forma predeterminada son inglés, francés, alemán y japonés.
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
translation-type: tm+mt
source-git-commit: dbfadb0b49c83c38aa2cb55c32517ad70bbd79d0

---


# Compatibilidad con nuevas configuraciones regionales para la localización de formularios adaptables{#supporting-new-locales-for-adaptive-forms-localization}

## Acerca de los diccionarios de configuración regional {#about-locale-dictionaries}

La localización de formularios adaptables se basa en dos tipos de diccionarios de configuración regional:

**Diccionario** específico del formulario Contiene cadenas utilizadas en formularios adaptables. Por ejemplo, etiquetas, nombres de campo, mensajes de error, descripciones de ayuda, etc. Se administra como un conjunto de archivos XLIFF para cada configuración regional y se puede acceder a ellos en `https://<host>:<port>/libs/cq/i18n/translator.html`.

**Diccionarios** globales Existen dos diccionarios globales, administrados como objetos JSON, en la biblioteca de clientes de AEM. Estos diccionarios contienen mensajes de error predeterminados, nombres de mes, símbolos de moneda, patrones de fecha y hora, etc. Puede encontrar estos diccionarios en CRXDe Lite en /libs/fd/xfaforms/clientlibs/I18N. Estas ubicaciones contienen carpetas independientes para cada configuración regional. Debido a que los diccionarios globales generalmente no se actualizan con frecuencia, mantener archivos JavaScript separados para cada configuración regional permite a los navegadores almacenarlos en caché y reducir el uso del ancho de banda de la red al acceder a diferentes formularios adaptables en el mismo servidor.

### Funcionamiento de la localización de formularios adaptables {#how-localization-of-adaptive-form-works}

Cuando se procesa un formulario adaptable, identifica la configuración regional solicitada observando los siguientes parámetros en el orden especificado:

* Parámetro de solicitud `afAcceptLang`Para anular la configuración regional del navegador de los usuarios, puede pasar el parámetro de solicitud `afAcceptLang` para forzar la configuración regional. Por ejemplo, la siguiente URL obligará a procesar el formulario en la configuración regional japonesa:
   `https://[server]:[port]/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* Configuración regional del explorador establecida para el usuario, que se especifica en la solicitud mediante el `Accept-Language` encabezado.

* Configuración de idioma del usuario especificado en AEM.

Una vez identificada la configuración regional, los formularios adaptables seleccionan el diccionario específico del formulario. Si no se encuentra el diccionario específico del formulario para la configuración regional solicitada, se utiliza el diccionario inglés (en).

Si no existe una biblioteca de cliente para la configuración regional solicitada, busca una biblioteca de cliente para el código de idioma presente en la configuración regional. Por ejemplo, si la configuración regional solicitada es `en_ZA` (inglés sudafricano) y la biblioteca del cliente `en_ZA` no existe, el formulario adaptable utilizará la biblioteca del cliente para el idioma `en` (inglés), si existe. Sin embargo, si no existe ninguno, el formulario adaptable utiliza el diccionario para la configuración `en` regional.

## Adición de asistencia para la localización en configuraciones regionales no admitidas {#add-localization-support-for-non-supported-locales}

Actualmente, AEM Forms admite la localización de contenido de formularios adaptables en inglés (en), español (es), francés (fr), italiano (it), alemán (de), japonés (ja), portugués-brasileño (pt-BR), chino (zh-CN), chino-Taiwán (zh-TW) y coreano (ko-KR).

Para añadir compatibilidad con una nueva configuración regional en tiempo de ejecución de formularios adaptables:

1. [Agregar una configuración regional al servicio GuideLocalizationService](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [Agregar una biblioteca de cliente XFA para una configuración regional](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [Agregar una biblioteca de cliente de formulario adaptable para una configuración regional](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [Agregar compatibilidad con la configuración regional para el diccionario](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [Reinicie el servidor](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### Agregar una configuración regional al servicio de localización de guías {#add-a-locale-to-the-guide-localization-service-br}

1. Ir a `https://[server]:[port]/system/console/configMgr`.
1. Haga clic en para editar el componente **Guía del servicio** de localización.
1. Agregue la configuración regional que desee agregar a la lista de configuraciones regionales admitidas.

![GuideLocalizationService](assets/configservice.png)

### Agregar una biblioteca de cliente XFA para una configuración regional {#add-xfa-client-library-for-a-locale-br}

Cree un nodo de tipo `cq:ClientLibraryFolder` en `etc/<folderHierarchy>`, con categoría `xfaforms.I18N.<locale>`, y agregue los siguientes archivos a la biblioteca del cliente:

* **I18N.js** definiendo `xfalib.locale.Strings` para el `<locale>` tal como se define en `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.

* **js.txt** que contiene lo siguiente:

```
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### Agregar una biblioteca de cliente de formulario adaptable para una configuración regional {#add-adaptive-form-client-library-for-a-locale-br}

Cree un nodo de tipo `cq:ClientLibraryFolder` en `etc/<folderHierarchy>`, con categoría como `guides.I18N.<locale>` y dependencias como `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` y `guide.common`. &quot;

Agregue los siguientes archivos a la biblioteca del cliente:

* **La definición de i18n.js** `guidelib.i18n`, que tiene patrones de &quot;calendarSymbols&quot;, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` para las especificaciones `<locale>` [](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)de XFA descritas en la Especificación de conjuntos de configuraciones regionales. También puede ver cómo se define para otras configuraciones regionales admitidas en `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`.
* **LogMessages.js** definiendo `guidelib.i18n.strings` y `guidelib.i18n.LogMessages` para el `<locale>` como se define en `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.
* **js.txt** que contiene lo siguiente:

```
i18n.js
LogMessages.js
```

### Agregar compatibilidad con la configuración regional para el diccionario {#add-locale-support-for-the-dictionary-br}

Realice este paso sólo si el `<locale>` que está agregando no es `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw``ja``ko-kr`.

1. Cree un `nt:unstructured` nodo `languages` en `etc`, si no está presente.

1. Agregue una propiedad de cadena con varios valores `languages` al nodo, si no está presente ya.
1. Agregue los `<locale>` valores de configuración regional predeterminados `de``es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja``ko-kr`, si no están presentes.

1. Agregue el `<locale>` a los valores de la `languages` propiedad de `/etc/languages`.

El `<locale>` aparecerá en `https://[server]:[port]/libs/cq/i18n/translator.html`.

### Restart the server {#restart-the-server}

Reinicie el servidor AEM para que la configuración regional agregada entre en vigor.

## Bibliotecas de muestra para agregar compatibilidad con español {#sample-libraries-for-adding-support-for-spanish}

Bibliotecas cliente de muestra para agregar compatibilidad con español

[Obtener archivo](assets/sample.zip)
