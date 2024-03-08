---
title: Solución de problemas de integración
description: Obtenga información sobre cómo solucionar problemas al integrarse con Adobe Experience Manager.
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 11b0023e-34bd-4dfe-8173-5466db9fbe34
source-git-commit: db0e9d6105484b37e2e21e49bf0f95cef9da2a62
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 1%

---

# Solución de problemas de integración{#troubleshooting-integration-issues}

## Sugerencias generales de resolución de problemas {#general-troubleshooting-tips}

### Asegúrese de que no haya errores de JavaScript {#ensure-there-are-no-javascript-errors}

Compruebe si la consola de JavaScript del explorador muestra algún error. Los errores no controlados pueden impedir que el código siguiente se ejecute correctamente. En caso de errores, compruebe qué secuencia de comandos está causando el error y en qué área. La ruta al script puede dar una indicación de a qué funcionalidad pertenece el script.

### Inicio de sesión en el nivel de componente {#logging-on-component-level}

En algunos casos, podría resultar útil añadir instrucciones adicionales en el nivel de componente. Dado que el componente se procesa, puede agregar un marcado temporal para mostrar valores de variables que puedan ayudarle a identificar posibles problemas. Por ejemplo:

```
<%
log.info("myVariable={}", myVariable);
%>

<!--
<%= myJspVariable %>
-->

<!--
${ myHtlVariable }
-->
```

Para obtener más información sobre el registro, consulte la [Registro](/help/sites-deploying/configure-logging.md) y [Trabajar con registros de auditoría y archivos de registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) páginas.

## Problemas de integración de Analytics {#analytics-integration-issues}

### El importador de informes causa un uso alto de CPU/memoria {#the-report-importer-causes-high-cpu-memory-usage}

El importador de informes causa un uso elevado de CPU/memoria o causa `OutOfMemoryError` excepciones.

#### Solución {#solution}

Para solucionar este problema, puede probar lo siguiente:

* Asegúrese de que no haya una gran cantidad de importadores de encuestas registrados (consulte la sección &quot;El cierre tarda mucho tiempo debido al importador de encuestas&quot; más abajo).
* Ejecutar importadores de informes a una hora determinada del día mediante expresiones CRON para `ManagedPollingImporter` configuraciones en la [Consola OSGi](/help/sites-deploying/configuring-osgi.md).

AEM Para obtener más información sobre la creación de servicios de importador de datos personalizados en, consulte el siguiente artículo en la página de ayuda de [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

### El cierre tarda mucho tiempo debido al importador de encuestas {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

Analytics se ha diseñado teniendo en cuenta un mecanismo de herencia. Normalmente, para habilitar Analytics para un sitio, agrega una referencia a una configuración de Analytics dentro de las propiedades de página [Cloud Service](/help/sites-developing/extending-cloud-config.md) pestaña. A continuación, la configuración se hereda automáticamente a todas las páginas secundarias sin necesidad de volver a hacer referencia a ella a menos que una página requiera una configuración diferente. AEM AEM Al agregar una referencia a un sitio, también se crean automáticamente varios nodos (12 para la versión 6.3 y versiones anteriores o 6 para la versión 6.4 y posteriores de la versión de la aplicación de) del tipo `cq;PollConfig` AEM , que crea una instancia de los importadores de encuestas utilizados para importar datos de Analytics en las instancias de. Como resultado:

* Tener muchas páginas que hacen referencia a Analytics lleva a una gran cantidad de importadores de encuestas.
* Además, copiar y pegar páginas con una referencia a una configuración de Analytics provoca una duplicación de los importadores de encuestas.

#### Solución {#solution-1}

En primer lugar, el análisis de [error.log](/help/sites-deploying/configure-logging.md) puede proporcionarle información sobre la cantidad de importadores de encuestas activos o registrados. Por ejemplo:

```
# Count PollingImporter entries
$ sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\),interval.*/\1/p" error.log | wc -l
86415
# Count PollingImporter entries for last30days
$ sed -n "s/.*(aem-analytics-integration-last30Days).*target=\(.*\),interval.*/\1/p" error.log | wc -l
14531
# Count unique paths of PollingImporter registrations
sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\)\/jcr:content.*/\1/p" error.log | sort | uniq -c
28115
```

En segundo lugar, asegúrese de que solo las páginas principales (las que están en la parte superior de la jerarquía) tengan una configuración de Analytics a la que se haga referencia.

AEM Para obtener más información sobre la creación de servicios de importador de datos personalizados en, consulte el siguiente artículo en la página de ayuda de [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

## Problemas de DTM (heredados) {#dtm-legacy-issues}

### La etiqueta de script de DTM no se representa en el origen de página {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

El [DTM](/help/sites-administering/dtm.md) la etiqueta de script no se incluye correctamente en la página aunque se haya hecho referencia a la configuración en las propiedades de página [Cloud Service](/help/sites-developing/extending-cloud-config.md) pestaña.

#### Solución {#solution-2}

Para solucionar el problema, puede probar lo siguiente:

* AEM Asegúrese de que las propiedades cifradas se puedan descifrar (tenga en cuenta que el cifrado puede utilizar una clave generada automáticamente diferente en cada instancia de la). Para obtener más información, lea también [Compatibilidad con cifrado para propiedades de configuración](/help/sites-administering/encryption-support-for-configuration-properties.md).
* Volver a publicar las configuraciones encontradas en `/etc/cloudservices/dynamictagmanagement`
* Comprobación de ACL en `/etc/cloudservices`. Las ACL deben ser:

   * permitir; jcr:read; webservice-support-servicelibfinder
   * permitir; jcr:leer; todos; `rep:glob:`&amp;ast;`/defaults/`&amp;ast;
   * permitir; jcr:leer; todos; `rep:glob:`&amp;ast;`/defaults`
   * permitir; jcr:leer; todos; `rep:glob:`&amp;ast;`/public/`&amp;ast;
   * permitir; jcr:leer; todos; `rep:glob:`&amp;ast;`/public`

Para obtener más información sobre la administración de ACL, lea la [Administración de usuarios y seguridad](/help/sites-administering/security.md#permissions-in-aem) página.

## Problemas de integración de Target {#target-integration-issues}

### Contenido dirigido no visible en el modo de vista previa al utilizar componentes de página personalizados {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

Este problema se debe a que los componentes de página personalizados no incluyen las bibliotecas de cliente o JSP correctas que administran las integraciones de Target DTM.

#### Solución {#solution-3}

Puede probar las siguientes soluciones:

* Asegúrese de que el personalizado `headlibs.jsp` (si procede) `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`) incluye lo siguiente:

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* Asegúrese de que el personalizado `head.html` (si procede) `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) **no tiene** incluya de forma selectiva encabezados de integración específicos como el ejemplo siguiente:

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

El `servicelibs.jsp` añade los objetos JavaScript de análisis necesarios y carga las bibliotecas del servicio en la nube asociadas al sitio web. Para el servicio Target, las bibliotecas se cargan mediante el `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

El conjunto de bibliotecas que se cargan depende del tipo de biblioteca de cliente de destino ( `mbox.js` o `at.js`) se utiliza en la configuración de Target.

Al utilizar DTM para la entrega de `mbox.js` o `at.js` asegúrese de que las bibliotecas se cargan antes de que se procese el contenido. El uso de sistemas Tag Management que carguen estas bibliotecas de forma asíncrona podría provocar problemas al ejecutar el código JavaScript específico de destino.

Para obtener más información, lea la [Desarrollo de contenido de destino](/help/sites-developing/target.md#understanding-the-target-component) página.

### El error &quot;Falta la ID del grupo de informes en la inicialización de la AppMeasurement&quot; se muestra en la consola del explorador {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

Este problema puede aparecer cuando Adobe Analytics se implementa en el sitio web mediante DTM y utiliza código personalizado. La causa es el uso de `s = new AppMeasurement()` para crear una instancia de `s` objeto.

#### Solución {#solution-4}

Uso `s_gi` en lugar del `new AppMeasurement` método de creación de instancias. Por ejemplo:

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### Se muestra aleatoriamente una oferta predeterminada en lugar de la oferta correcta {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

Este problema puede tener varias causas:

* Cargando bibliotecas de cliente de Target ( `mbox.js` o `at.js`) de forma asíncrona, el uso de sistemas Tag Management de terceros puede interrumpir la segmentación de forma aleatoria. Se supone que las bibliotecas de Target se cargan sincrónicamente en el encabezado de la página. AEM Esto siempre es así cuando las bibliotecas se entregan desde el propio servidor de.

* Carga de dos bibliotecas de cliente de Target ( `at.js`AEM ) simultáneamente, por ejemplo, uno que utiliza DTM y otro que utiliza la configuración de Target en la configuración de. Esto puede provocar enfrentamientos para el `adobe.target` definición si la variable `at.js` Las versiones difieren.

#### Solución {#solution-5}

Puede probar las siguientes soluciones:

* Asegúrese de que el código de cliente que carga las bibliotecas de tipo DTM (que a su vez cargan las bibliotecas de Target) se ejecuta sincrónicamente en [encabezado de página](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages).
* si el sitio está configurado para utilizar DTM para ofrecer bibliotecas de Target, asegúrese de que las variables **Clientlib entregado por DTM** está marcada en la [Configuración de Target](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html) para el sitio.

### Siempre se muestra una oferta predeterminada en lugar de la oferta correcta al utilizar AT.js 1.3+ {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

AEM De serie, la versión 6.2 y 6.3 de no es compatible con la versión 1.3.0 o posterior de AT.js. Con la versión 1.3.0 de AT.js que introduce la validación de parámetros para sus API, `adobe.target.applyOffer()` requiere un parámetro &quot;mbox&quot; que no proporciona el `atjs-itegration.js` código.

#### Solución {#solution-6}

Para resolver este problema, edite `atjs-itegration.js` y añada el `"mbox": mboxName` campo en el objeto de parámetro para `adobe.target.applyOffer()` como sigue:

```
adobe.target.getOffer({
    "mbox": mboxName,
    "params": params,
    "success": function (response) {
        adobe.target.applyOffer({
            "mbox": mboxName, //<--- ADDED PARAM
            "selector": "#" + mboxName,
            "offer": response
        })
    },
```

### La página Objetivos y configuración no muestra la sección Fuentes de informes {#the-goals-settings-page-does-not-show-the-reporting-sources-section}

Este problema es probablemente un [Configuración de A4T Analytics Cloud](/help/sites-administering/target-configuring.md) problema de aprovisionamiento.

#### Solución {#solution-7}

AEM Debe comprobar que A4T está correctamente habilitado para su cuenta de Target mediante la emisión de la siguiente solicitud de verificación a la siguiente dirección de correo electrónico:

```
http://localhost:4502/etc/cloudservices/testandtarget/<YOUR-CONFIG>/jcr:content.a4t.json

{
    "a4tEnabled": true,
    "sharedsecret": "SECRET",
    "proxyUrl": "/libs/cq/contentinsight/content/proxy.reportingservices.json",
    "active": "true",
    "pageName": "",
    "url": "https://api5.omniture.com/rs/0.5/",
    "username": "USER@DOMAIN"
}
```

Si la respuesta contiene la línea `a4tEnabled:false`, contenido [Adobe del Servicio de atención al cliente](https://helpx.adobe.com/contact.html) para que su cuenta se aprovisione correctamente.

### API de Target útiles {#helpful-target-apis}

A continuación se presentan dos API de Target que pueden resultar útiles para solucionar problemas de Target:

* Recuperar el extremo de Target para un código de cliente determinado

```
https://admin.testandtarget.omniture.com/rest/v1/endpoint/<CLIENTCODE>.json

{"api":"https://admin<N>.testandtarget.omniture.com/admin/rest/v1"}
```

* Recuperación del perfil de un cliente

```
https://admin<N>.testandtarget.omniture.com/admin/rest/v1/clients/<CLIENT>?email=<EMAIL>&password=<PASSWORD>

Response for N=4, CLIENT-dayintegrationintern
{
    "clientCode": "dayintegrationintern",
    "companyName": "Day Integration - Internal",
    "omnitureCompanyId": "Day Integration Internal",
    "softTraxId": -1,
    "address1": "XYZ",
    "city": "San Francisco",
    "state": "ca",
    "zip": "94107",
    "country": "UNITED STATES",
    "locale": "de_DE",
    "timeZone": "Europe/Berlin",
    "phone": "XX-XX-XXXX",
    "serviceLevel": "Up to 100,000",
    "privileges": [
        "a4t",
        "hosts",
        "TnT-SC-integration",
        "mvt",
        "steps",
        "testing-campaigns",
        "view-snapshot",
        "on-site-editor",
        "optimizing-campaign",
        "third-party-id-support",
        "landing-page-campaigns",
        "segment",
        "rest-create-user",
        "advanced-targeting",
        "mobile-device-targeting",
        "beta",
        "geolocation"
    ]
}
```
