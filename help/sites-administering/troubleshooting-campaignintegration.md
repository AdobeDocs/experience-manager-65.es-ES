---
title: Solución de problemas de la integración de Adobe Campaign
seo-title: Solución de problemas de la integración de Adobe Campaign
description: Obtenga información sobre cómo solucionar problemas con la integración de Adobe Campaign.
seo-description: Obtenga información sobre cómo solucionar problemas con la integración de Adobe Campaign.
uuid: 835ac2c3-ef2f-4963-9047-aeda3647b114
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b1d45f01-78de-423c-8f6b-5cb7067c3a2f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---


# Solución de problemas de la integración de Adobe Campaign{#troubleshooting-your-adobe-campaign-integration}

>[!NOTE]
>
>Esta página se aplica al Campaign Classic.

Las siguientes sugerencias de solución de problemas ayudan a resolver los problemas más comunes que puede encontrar al integrar AEM con Adobe Campaign:

## Sugerencias generales para la resolución de problemas {#general-troubleshooting-tips}

Para ambas integraciones, puede comprobar si se envían llamadas HTTP (AEM > Adobe Campaign, Adobe Campaign > AEM):

* Cuando las integraciones fallan, asegúrese de que estas llamadas llegan al otro extremo (para evitar problemas de firewall/SSL).
* Para AEM funcionalidad, verá que las llamadas json se solicitan desde la interfaz de creación de AEM; esto no debe generar un error HTTP-500. Si ve errores HTTP-500, consulte `error.log` para obtener más información sobre este tema.
* El aumento del nivel de depuración de las clases de campaña en AEM también ayuda a solucionar problemas.

## Si falla la conexión {#if-the-connection-fails}

Compruebe que ha configurado el operador **aemserver** en Adobe Campaign.

## Si las imágenes no aparecen en la consola de Adobe Campaign {#if-images-do-not-appear-in-the-adobe-campaign-console}

Compruebe el código fuente HTML y valide que puede abrir la dirección URL desde el ordenador cliente. Si la dirección URL tiene localhost:4503 en ella, cambie la configuración de Day CQ Link Externalizer en la instancia de autor para que apunte a una instancia de publicación a la que se puede acceder desde el equipo de la consola de Adobe Campaign.

Consulte [Configuración del Externalizador.](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## Si no puede conectarse de AEM a Adobe Campaign {#if-you-cannot-connect-from-aem-to-adobe-campaign}

Busque el siguiente mensaje de error en Adobe Campaign:

`No datasource defined in the instance 'default'.`

`Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

Para solucionar este problema, cambie lo siguiente en **$CAMPAÑA_HOME/conf/config-&lt;instance-name>.xml**:

`<dataStore hosts="*" lang="en_GB">`

## Si no se muestra ningún dato en el cuadro de diálogo de Adobe Campaign {#if-no-data-displays-in-the-adobe-campaign-dialog}

En Adobe Campaign, asegúrese de que no hay ninguna barra diagonal final (/) después del número de puerto.

![chlimage_1-149](assets/chlimage_1-149.png)

## Si recibe una advertencia sobre la configuración regional {#if-you-get-a-warning-about-your-setlocale}

Si está iniciando el servicio Apache HTTPD y ve el error `"Warning: setlocale: LC_CTYPE cannot change locale"` asegúrese de tener su **en_CA.ISO-8859-15 configuración regional** instalada en el sistema.

Puede comprobar si está instalado mediante `local -a`. Si no está instalado, puede parchear **/usr/local/neolane/nl6/env.sh** script y cambiar la configuración regional a una instalada.

## Si se produce un error al compilar la secuencia de comandos &#39;get_nms_amcGetSeedMetaData_jssp&#39; {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

Si ve el siguiente mensaje de error en el archivo de registro de AEM:

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

Utilice la siguiente solución:

1. Abrir archivo **$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js**
1. Modificar la línea 467 del método &quot;amcGetSeedMetaData&quot;
1. Cambiar `label : [inclView.@label](mailto:inclView.@label)` a `label : String([inclView.@label](mailto:inclView.@label))`

1. Guardar.
1. Reinicie el servidor.

## Si Adobe Campaign muestra un error al hacer clic en el botón Sincronizar {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

Si al hacer clic en el botón **Sincronizar** en Adobe Campaign Classic, aparece el siguiente error:

`Error while executing the method ‘aemListContent' of service [nms:delivery](https://nmsdelivery/)`

Para solucionar este problema, asegúrese de que la dirección URL de conexión AEM configurada en las Cuentas externas esté disponible desde el equipo.

Se ha solucionado este problema con un cambio de **localhost** a una dirección IP.

## Si aparece el error &#39;No se puede analizar la fecha y hora XTK &#39;sin definir&#39; {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

Después de hacer clic en Sincronizar, aparece un error que indica que se ha producido una secuencia de comandos en las páginas: No se puede analizar la fecha y la hora XTK &#39;sin definir&#39;: no es un valor XTK válido.

Esto sucede si todavía hay información de Adobe Campaign obsoleta en la instancia de AEM. Solucione este problema eliminando todas las configuraciones de integración de campaña que se encuentran en AEM y reconstruyéndolas. A continuación, cree una nueva plantilla.

## Si una conexión a SSL muestra un error al configurar el servicio de nube {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

En el error.log de AEM, si ve lo siguiente:

```xml
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

Por favor, levante un ticket con el equipo de soporte de Adobe Campaign.

## Si ve http en lugar de los vínculos https esperados en el cuadro de diálogo de sincronización {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

Con la siguiente configuración:

* Alojado en Adobe Campaign mediante https para la comunicación con AEM Author
* Invertir proxy que termina SSL
* Instancia de AEM Author in situ

Al intentar sincronizar contenido en Adobe Campaign envío, AEM devuelve una lista de newsletters. Sin embargo, las direcciones URL de los boletines informativos de la lista son direcciones http. Al seleccionar uno de los elementos de la lista, se produce un error.

Para resolver este problema:

* El despachante o proxy inverso debe configurarse para pasar el protocolo original como encabezado.
* El *Filtro SSL de servicio Apache Felix Http* en la configuración OSGi ([https://&lt;host>:&lt;puerto>/system/console/configMgr](http://localhost:4502/system/console/configMgr)) debe configurarse con los ajustes de encabezado respectivos. Consulte [https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter](https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter)

## Si la plantilla personalizada que he creado no se puede seleccionar en Propiedades de página {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

Al crear una plantilla de correo para Adobe Campaign, debe incluir la propiedad **acMapping** con el valor **mapRecipient** en el nodo **jcr:content** de la plantilla, o no podrá seleccionar la plantilla Adobe Campaign en **Propiedades de la página** de AEM (el campo está deshabilitado).

## Si aparece el error &quot;com.day.cq.mcm.campaña.servlets.util.ParameterMapper&quot; en los registros {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

Al utilizar la plantilla personalizada, aparece el error &quot;com.day.cq.mcm.campaña.servlets.util.ParameterMapper&quot; en los registros. En este evento, asegúrese de instalar Featurepack 6576 desde [Package Share](/help/sites-administering/package-manager.md#package-share). Se trata de un problema en el que, si la propiedad acMapping se establece en un valor distinto de destinatario.firstName, se crea un valor en blanco en el lado de Adobe Campaign Manager.
