---
title: Usar el rastreador de páginas e incrustar código en páginas web
description: Aprenda a incluir el rastreador de páginas e incrustar códigos JavaScript en el código del sitio web para permitir que Adobe Analytics capture los datos de uso alrededor de los recursos.
contentOwner: AG
role: Architect, Admin
feature: Informes del recurso
exl-id: 14d02015-df00-4566-a098-de76eaf42605
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 1%

---

# Uso del rastreador de páginas e incrustar código en páginas web {#using-page-tracker-and-embed-code-in-web-pages}

El rastreador de páginas es un fragmento de código JavaScript que se incluye en el código de los sitios web de terceros para permitir que Adobe Analytics capture los datos de uso alrededor de [!DNL Adobe Experience Manager Assets] en estos sitios web.

Para capturar eventos, como clics, etc. específicos de los recursos, también debe incluir el código de incrustación en el código de sitios web de terceros.

El siguiente código de ejemplo muestra el aspecto que tiene una página web que contiene tanto el código del rastreador de páginas como el código incrustado:

```html
<!DOCTYPE html>
<html>
    <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in milliseconds
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","xxxx","xxx","list1","eVar3","event8","event7");
            </script>

    </head>

    <body>

                                <img
            src="https://10.41.52.147:4502/xxxx/content/dam/test/abc.jpg"
            data-aem-asset-id="aaid:a386f2cd78234becb66bd11575f9452d"
            data-trackable=true
            onload=assetAnalytics.core.assetLoaded(this)>

        <a
            href="https://www.adobe.com"

            onclick="assetAnalytics.core.assetClicked(this);return false">
                <img
                    src="http://localhost/xxxx/content/dam/test/xyz.jpg"
                    data-aem-asset-id="aaid:7fa01fce0ebe40268cd6dcf07e2d9cb1"
                    data-trackable=true
                    onload=assetAnalytics.core.assetLoaded(this)>
        </a>

    </body>
</html>
```

## Añadir código de seguimiento de página {#adding-page-tracker-code}

El código del rastreador de páginas se agrega dentro de la sección del encabezado del código del sitio web. El siguiente fragmento de código muestra el código Rastreador de páginas incluido en una página web de muestra:

```xml
 <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/foundation/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in millis
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","abc.net","bee","list1","eVar3","event8","event7");
            </script>

 </head>
```

## Añadir código incrustado {#add-embed-code}

El código incrustado se agrega al cuerpo del código del sitio web. El siguiente fragmento de código muestra el código incrustado incluido en una página web de ejemplo:

```xml
<body>

      <img
            src="http://localhost:4502/xxxx/content/dam/test/xyz.jpg"
            data-aem-asset-id="aaid:a386f2cd78234becb66bd11575f9452d"
            data-trackable=true
            onload=assetAnalytics.core.assetLoaded(this)>

        <a
            href="https://www.adobe.com"

            onclick="assetAnalytics.core.assetClicked(this);return false">
           <img
                    src="http://localhost:4502/xxxx/content/dam/test/xyz.jpg"
                    data-aem-asset-id="aaid:7fa01fce0ebe40268cd6dcf07e2d9cb1"
                    data-trackable=true
                    onload=assetAnalytics.core.assetLoaded(this)>
        </a>

    </body>
```
