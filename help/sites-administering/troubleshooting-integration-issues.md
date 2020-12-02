---
title: Resolución de problemas de integración
seo-title: Resolución de problemas de integración
description: Obtenga información sobre cómo solucionar problemas de integración.
seo-description: Obtenga información sobre cómo solucionar problemas de integración.
uuid: fe080e58-a855-4308-a611-f72eb47ba82d
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 422ee332-23ae-46bd-8394-a4e0915beaa2
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 2%

---


# Resolución de problemas de integración{#troubleshooting-integration-issues}

## Sugerencias generales para la resolución de problemas {#general-troubleshooting-tips}

### Asegúrese de que no haya errores de JavaScript {#ensure-there-are-no-javascript-errors}

Compruebe si la consola JavaScript del explorador muestra algún error. Los errores no controlados podrían evitar que el código subsiguiente se ejecutara correctamente. En caso de que haya errores, compruebe qué secuencia de comandos está causando el error y en qué área. La ruta de acceso a la secuencia de comandos puede indicar a qué funcionalidad pertenece la secuencia de comandos.

### Inicio de sesión en el nivel de componente {#logging-on-component-level}

En algunos casos, podría ser útil agregar instrucciones adicionales a nivel de componente. Como el componente se procesa, puede agregar una marca temporal para mostrar valores de variables que le ayudarán a identificar posibles problemas. Por ejemplo:

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

Para obtener más información sobre el registro, consulte las [Páginas de registro](/help/sites-deploying/configure-logging.md) y [Uso de registros de auditoría y archivos de registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files).

## Problemas de integración de Analytics {#analytics-integration-issues}

### El importador de informes causa un alto uso de CPU/memoria {#the-report-importer-causes-high-cpu-memory-usage}

El importador de informes causa un alto uso de CPU/memoria o `OutOfMemoryError` excepciones.

#### Solución {#solution}

Para solucionar este problema, puede probar lo siguiente:

* Asegúrese de que no haya una gran cantidad de PollingImporters registrados (consulte la sección &quot;El cierre se demora mucho debido a PollingImporter&quot; que aparece a continuación).
* Ejecute Importadores de informes a una hora determinada del día utilizando expresiones CRON para las configuraciones `ManagedPollingImporter` en la [consola OSGi](/help/sites-deploying/configuring-osgi.md).

Para obtener más información sobre la creación de servicios personalizados de importación de datos en AEM, lea el siguiente artículo [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

### El cierre lleva mucho tiempo debido a PollingImporter {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

Analytics se ha diseñado teniendo en cuenta un mecanismo de herencia. Normalmente, se activa Analytics para un sitio agregando una referencia a una configuración de Analytics en la ficha Propiedades de página [Cloud Services](/help/sites-developing/extending-cloud-config.md). La configuración se hereda automáticamente a todas las páginas secundarias sin necesidad de volver a hacer referencia a ella a menos que una página requiera una configuración diferente. Añadir una referencia a un sitio también crea automáticamente varios nodos (12 para AEM 6.3 y anteriores o 6 para AEM 6.4   y posteriores) del tipo `cq;PollConfig` que crea instancias de PollingImporters utilizadas para importar datos de Analytics en AEM. Como resultado:

* Tener muchas páginas que hagan referencia a Analytics provoca una gran cantidad de PollingImporters.
* Además, copiar y pegar páginas con una referencia a una configuración de Analytics provoca una duplicación de sus PollingImporters.

#### Solución {#solution-1}

En primer lugar, analizar el [error.log](/help/sites-deploying/configure-logging.md) puede proporcionarle información sobre la cantidad de PollingImporters activos o registrados. Por ejemplo:

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

En segundo lugar, asegúrese de que solo las páginas principales (superiores en la jerarquía) tienen una configuración de Analytics referenciada.

Para obtener más información sobre la creación de servicios personalizados de importación de datos en AEM, lea el siguiente artículo [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

## Problemas de DTM (heredados) {#dtm-legacy-issues}

### La etiqueta de secuencia de comandos de DTM no se representa en el origen de la página {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

La etiqueta de script [DTM](/help/sites-administering/dtm.md) no se incluye correctamente en la página aunque se haya hecho referencia a la configuración en la ficha Propiedades de página [Cloud Services](/help/sites-developing/extending-cloud-config.md).

#### Solución {#solution-2}

Para solucionar el problema, puede probar lo siguiente:

* Asegúrese de que las propiedades cifradas se pueden descifrar (tenga en cuenta que el cifrado puede utilizar una clave generada automáticamente diferente en cada instancia de AEM). Para obtener más información, lea también [Compatibilidad con cifrado para propiedades de configuración](/help/sites-administering/encryption-support-for-configuration-properties.md).
* Vuelva a publicar las configuraciones encontradas en `/etc/cloudservices/dynamictagmanagement`
* Compruebe las ACL en `/etc/cloudservices`. Las ACL deben ser:

   * allow; jcr:read; webservice-support-service-libfinder
   * allow; jcr:read; todos; rep:glob:&amp;ast;/default/&amp;ast;
   * allow; jcr:read; todos; rep:glob:&amp;ast;/predeterminados
   * allow; jcr:read; todos; rep:glob:&amp;ast;/public/&amp;ast;
   * allow; jcr:read; todos; rep:glob:&amp;ast;/public

Para obtener más información sobre la administración de ACL, lea la página [Administración de usuarios y seguridad](/help/sites-administering/security.md#permissions-in-aem).

## Problemas de integración de destinatario {#target-integration-issues}

### Contenido de destino no visible en el modo de Previsualización al utilizar componentes de página personalizados {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

Este problema se debe a que los componentes de página personalizados no incluyen el JSP o las bibliotecas de cliente correctas que gestionan las integraciones de Destinatario DTM.

#### Solución {#solution-3}

Puede probar las siguientes soluciones:

* Asegúrese de que el `headlibs.jsp` personalizado (si existe `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`) incluye lo siguiente:

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* Asegúrese de que el `head.html` (si existe `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) **no incluye de manera selectiva** encabezados de integración específicos como el ejemplo siguiente:

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

El `servicelibs.jsp` agrega los objetos JavaScript de análisis necesarios y carga las bibliotecas de servicios de nube asociadas con el sitio web. Para el servicio de Destinatario, las bibliotecas se cargan mediante `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

El conjunto de bibliotecas que se cargan depende del tipo de biblioteca de cliente de destinatario ( `mbox.js` o `at.js`) utilizada en la configuración de Destinatario.

Al utilizar la DTM para entregar `mbox.js` o `at.js`, asegúrese de que las bibliotecas se cargan antes de que se procese el contenido. El uso de sistemas de administración de etiquetas que cargan estas bibliotecas de forma asíncrona podría causar problemas en la ejecución del código JavaScript específico de destinatario.

Para obtener más información, lea la página [Desarrollar para contenido de objetivo](/help/sites-developing/target.md#understanding-the-target-component).

### El error &quot;Falta la ID del grupo de informes en la inicialización de AppMeasurement&quot; se muestra en la consola del explorador {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

Este problema puede aparecer cuando Adobe Analytics se implementa en el sitio web mediante DTM y utiliza código personalizado. La causa está usando el `s = new AppMeasurement()` para crear una instancia del objeto `s`.

#### Solución {#solution-4}

Utilice `s_gi` en lugar del método de creación de instancias `new AppMeasurement`. Por ejemplo:

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### Se muestra aleatoriamente una oferta predeterminada en lugar de la oferta correcta {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

Este problema puede tener varias causas:

* Cargar de forma asíncrona bibliotecas de cliente de Destinatario ( `mbox.js` o `at.js`) mediante el uso de sistemas de administración de etiquetas de terceros puede dañar aleatoriamente la segmentación. Se supone que las bibliotecas de Destinatario se cargan sincrónicamente en el encabezado de página. Esto siempre es cierto cuando las bibliotecas se entregan desde AEM.

* Cargando dos bibliotecas de cliente de Destinatario ( `at.js`) simultáneamente, por ejemplo, una con DTM y otra con la configuración de Destinatario en AEM. Esto puede provocar conflictos en la definición `adobe.target` si las versiones `at.js` difieren.

#### Solución {#solution-5}

Puede probar las siguientes soluciones:

* Asegúrese de que el código del cliente que carga las bibliotecas de tipo DTM (que a su vez carga las bibliotecas de Destinatario) se ejecuta sincrónicamente en el [encabezado de página](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages).
* si el sitio está configurado para utilizar la DTM para entregar bibliotecas de Destinatario, asegúrese de que la opción **Clientlib proporcionada por la DTM** esté marcada en la [configuración de Destinatario](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html) del sitio.

### Siempre se muestra una oferta predeterminada en lugar de la oferta correcta al usar AT.js 1.3+ {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

Fuera de la caja AEM 6.2 y 6.3 no es compatible con la versión 1.3.0 o posterior de AT.js. Con la versión 1.3.0 de AT.js introduciendo la validación de parámetros para sus API, `adobe.target.applyOffer()` requiere un parámetro &quot;mbox&quot; que no proporciona el código `atjs-itegration.js`.

#### Solución {#solution-6}

Para resolver este problema, edite `atjs-itegration.js` y agregue el campo `"mbox": mboxName` en el objeto de parámetro para `adobe.target.applyOffer()` de la siguiente manera:

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

### La página Objetivos y configuración no muestra la sección Fuentes de Sistema de informes {#the-goals-settings-page-does-not-show-the-reporting-sources-section}

Es muy probable que este problema se deba a un problema de aprovisionamiento de [Configuración de Analytics Cloud de A4T](/help/sites-administering/target-configuring.md).

#### Solución {#solution-7}

Debe comprobar que A4T está correctamente habilitado para su cuenta de Destinatario mediante la siguiente solicitud de verificación para AEM:

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

Si la respuesta contiene la línea `a4tEnabled:false`, póngase en contacto con [Servicio de atención al cliente de Adobe](https://helpx.adobe.com/contact.html) para obtener el aprovisionamiento correcto de su cuenta.

### API de Destinatario útiles {#helpful-target-apis}

A continuación se presentan dos API de Destinatario que pueden resultar útiles para solucionar problemas de Destinatario:

* Recuperar el extremo de Destinatario para un código de cliente determinado

```
https://admin.testandtarget.omniture.com/rest/v1/endpoint/<CLIENTCODE>.json

{"api":"https://admin<N>.testandtarget.omniture.com/admin/rest/v1"}
```

* Recuperar el perfil de un cliente

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

