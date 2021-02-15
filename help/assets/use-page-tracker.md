---
title: Usar el rastreador de páginas e incrustar código en páginas web
description: Obtenga información sobre cómo incluir el rastreador de páginas y los códigos JavaScript incrustados en el código de su sitio web para permitir que Adobe Analytics capture los datos de uso en torno a los recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: fc433851c24f9049e7ba6dfada24d6e552eb6d05
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Utilizar el rastreador de páginas y código incrustado en páginas Web {#using-page-tracker-and-embed-code-in-web-pages}

El rastreador de páginas es un fragmento de código JavaScript que se incluye en el código de los sitios web de terceros para permitir que Adobe Analytics capture los datos de uso alrededor de [!DNL Adobe Experience Manager Assets] en estos sitios web.

Para capturar eventos, como clics, etc., específicos de los recursos, también debe incluir el código incrustado en el código de sitios web de terceros.

El siguiente código de ejemplo muestra cómo se ve una página web que contiene tanto el código del rastreador de páginas como el código incrustado:

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

## Añadir código de rastreador de páginas {#adding-page-tracker-code}

El código del rastreador de páginas se agrega a la sección de encabezado del código del sitio web. El siguiente fragmento de código muestra el código Rastreador de páginas incluido en una página web de muestra:

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

Puede agregar el código incrustado en el cuerpo del código del sitio web. El siguiente fragmento de código muestra el código incrustado incluido en una página web de muestra:

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
