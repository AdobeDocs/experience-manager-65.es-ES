---
title: Solución de problemas de integración de Adobe Campaign Classic
description: Obtenga información sobre cómo solucionar problemas con la integración de Adobe Campaign Classic.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 317bab41-3504-4e46-9ddc-72e291a34e06
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---


# Solución de problemas de integración de Adobe Campaign Classic{#troubleshooting-your-adobe-campaign-classic-integration}

Obtenga información sobre cómo solucionar problemas con la integración de Adobe Campaign Classic (ACC).

AEM Las siguientes sugerencias para la resolución de problemas le ayudarán a resolver los problemas más comunes que pueda encontrar al integrarse con el sistema de control de acceso de la red (ACC) de la red de administración de la red.

## Sugerencias generales de resolución de problemas {#general-troubleshooting-tips}

AEM Compruebe si las llamadas HTTP se envían y reciben en ambas soluciones (> Adobe Campaign Classic, Adobe Campaign Classic AEM >). Esta sugerencia le ayuda a evitar problemas de firewall/SSL.

* AEM AEM Para obtener la funcionalidad de la, puede ver que las llamadas de JSON se solicitan desde la interfaz de autor de la aplicación
   * Estas llamadas no deberían provocar el error HTTP-500.
   * Si ve errores HTTP-500, compruebe `error.log` para obtener más información.
* AEM Elevar el nivel de depuración de las clases de campaña en la también puede ayudar a solucionar problemas.

## Si la conexión falla {#when-the-connection-fails}

Compruebe que ha configurado el operador **`aemserver`** en Adobe Campaign Classic.

## Si las imágenes no aparecen en la consola de Adobe Campaign Classic {#if-images-do-not-appear-in-the-adobe-campaign-console}

Compruebe el origen del HTML y valide que puede abrir la dirección URL desde el equipo cliente. AEM Si la dirección URL contiene `localhost:4503`, cambie la configuración del Externalizador de vínculos de CQ de día en la instancia de autor de la. Haga que apunte a una instancia de publicación a la que se pueda acceder desde el equipo de consola de Adobe Campaign Classic.

Consulte [Configuración del externalizador.](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## AEM Si no puede conectarse desde la conexión de la red de a Adobe Campaign Classic  {#if-you-cannot-connect-from-aem-to-adobe-campaign}

Busque el siguiente mensaje de error en Adobe Campaign Classic.

* `No datasource defined in the instance 'default'.`

* `Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

Para solucionar este problema, cambie lo siguiente en `$CAMPAIGN_HOME/conf/config-<instance-name>.xml`:

* `<dataStore hosts="*" lang="en_GB">`

## Si no se muestran datos en el cuadro de diálogo Adobe Campaign Classic {#if-no-data-displays-in-the-adobe-campaign-dialog}

En Adobe Campaign Classic, asegúrese de que no tiene una barra diagonal (`/`) después del número de puerto.

![Adobe Campaign Classic: asegúrese de que no hay barra diagonal después del número de puerto](assets/chlimage_1-149.png)

## Si recibe una advertencia sobre setlocale {#if-you-get-a-warning-about-your-setlocale}

Al iniciar el servicio Apache HTTPD para Adobe Campaign Classic, puede ver el error `Warning: setlocale: LC_CTYPE cannot change locale`

Asegúrese de que tiene `en_CA.ISO-8859-15 locale` instalado en el servidor de Adobe Campaign Classic.

* Puede comprobar si está instalado usando `local -a`.
* Si no está instalado, puede aplicar parches al script `/usr/local/neolane/nl6/env.sh` y cambiar la configuración regional a una instalada.

## Si se produce un error al compilar el script &quot;get_nms_amcGetSeedMetaData_jssp&quot; {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

AEM Si ve el siguiente mensaje de error en el archivo de registro de la:

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

Utilice la siguiente solución en el servidor de Adobe Campaign Classic.

1. Abrir archivo `$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js`
1. Modificar línea 467 del método `amcGetSeedMetaData`
1. Cambiar `label : [inclView.@label](mailto:inclView.@label)` a `label : String([inclView.@label](mailto:inclView.@label))`
1. Guardar.
1. Vuelva a iniciar el servidor.

## Si Adobe Campaign Classic muestra un error al hacer clic en el botón Sincronizar {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

Al hacer clic en el botón **Sincronizar** en Adobe Campaign Classic, es posible que vea el siguiente error.

* `Error while executing the method 'aemListContent' of service [nms:delivery](https://nmsdelivery/)`

AEM Para solucionar este problema, asegúrese de que la dirección URL de conexión de la red de seguridad configurada en **Cuentas externas** en Adobe Campaign Classic es accesible desde el equipo.

Este problema se suele resolver cambiando de `localhost` a una dirección IP para la dirección URL.

## Si recibe un error &quot;No se puede analizar la fecha y hora XTK &quot;indefinido&quot;&quot; {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

AEM Después de hacer clic en **Sincronizar** en la, es posible que reciba un error que indique que se ha producido un script en las páginas.

* `Cannot parse XTK Date+Time 'undefined': not a valid XTK value.`

Este error se produce si hay información de Adobe Campaign Classic AEM obsoleta en la instancia de. Puede resolver este problema haciendo lo siguiente:

1. Elimine todas las configuraciones de integración de Adobe Campaign Classic AEM que se encuentren en la fase de ejecución de la.
1. Vuelva a compilar la integración.
1. Cree una plantilla.

## Si una conexión a SSL muestra un error al configurar el Cloud Service {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

Envíe un ticket al equipo de asistencia de Adobe Campaign AEM si ve lo siguiente en la `error.log` de la aplicación de.

```text
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

## Si ve HTTP en lugar de los vínculos HTTPS esperados en el cuadro de diálogo de sincronización {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

Al intentar sincronizar el contenido en la entrega de Adobe Campaign Classic AEM, devuelve una lista de boletines informativos, que se muestra a continuación: Sin embargo, las direcciones URL de los boletines de la lista pueden ser direcciones HTTP en lugar de HTTPS. Se produce un error al seleccionar uno de los elementos de la lista. Este error puede ocurrir con la siguiente configuración.

* Adobe Campaign AEM alojado mediante https para la comunicación con el autor de la
* SSL de terminación de proxy inverso
* AEM Instancia de autor de On-Premise

Para resolver este problema, haga lo siguiente:

* AEM El Dispatcher o el proxy inverso deben configurarse para pasar el protocolo original como un encabezado.
* AEM El **filtro SSL del servicio Http Apache Felix** en la configuración OSGi de la aplicación debe estar configurado con los valores de encabezado requeridos.
   * `https://<host>:<port>/system/console/configMgr`
   * Ver [https://github.com/apache/felix-dev/tree/master/http#using-the-ssl-filter](https://github.com/apache/felix-dev/tree/master/http#using-the-ssl-filter)

## No se puede seleccionar una plantilla personalizada en las propiedades de la página {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

AEM Al crear una plantilla de correo electrónico en la para Adobe Campaign Classic, debe incluir la propiedad `acMapping` con el valor `mapRecipient` en el nodo `jcr:content` de la plantilla. Si no lo hace, no podrá seleccionar la plantilla de Adobe Campaign Classic AEM en **Propiedades de página** de la. El campo aparece desactivado.

## AEM Si ve el error &quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot; en los registros de la {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

AEM Es posible que vea el error `com.day.cq.mcm.campaign.servlets.util.ParameterMapper` en los registros de trabajo de la al utilizar una plantilla personalizada.

Este error se produce si la propiedad `acMapping` se establece en un valor distinto de `recipient.firstName` y se crea un valor en blanco en el Administrador de Adobe Campaign.

AEM Si se produce este error, instale el paquete de características 6576 para su instalación en el espacio de trabajo de [Uso compartido de paquetes](/help/sites-administering/package-manager.md#package-share).
