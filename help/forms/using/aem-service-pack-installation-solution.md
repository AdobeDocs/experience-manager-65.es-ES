---
title: CRX/bundle y el servicio de página de inicio errores no disponibles una vez que se haya instalado el último Service Pack 6.5.15.0
description: CRX/bundle y el servicio de página de inicio errores no disponibles una vez que se haya instalado el último Service Pack 6.5.15.0
source-git-commit: be7a9cfc226537ab4b360064220fa03bf2045310
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 2%

---


# Errores de servicio no disponibles después de instalar AEM (6.5.15.0) service pack {#steps-to-resolve-error-after-installing-service-pack}

## Problema {#issue}

Después de instalar el [Paquete de servicio de AEM 6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), el error se produce como:
* ERROR [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException: No se puede resolver org.apache.sling.scripting.console

Después de instalar AEM 6.5.15.0 service pack, el CRX/bundle y la página de inicio muestran errores no disponibles.

## Solución {#solution}

>[!NOTE]
>
>Los pasos de resolución de problemas son aplicables para todos los servidores de aplicaciones excepto JBoss EAP 7.4.

Después de instalar [Paquete de servicio de AEM 6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), si el CRX/bundle y la página de inicio muestran errores de servicio no disponible, realice los siguientes pasos:

1. Detenga el servidor de aplicaciones.
1. Vaya a `[aem-forms root]\crx-repository\launchpad\felix\bundle52`.
1. Busque la variable `bundle.info` archivo.
1. Abra el `bundle.info` en el editor de texto ant y busque el nombre del paquete como `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >En caso de que `bundle.info` under `bundle52` no contiene el `org.apache.felix.http.bridge` paquete, compruebe el número de paquete en corchetes junto al `org.apache.felix.http.bridge`. A continuación, vaya a [raíz de aem-forms]\crx-repository\launchpad\felix\bundle[x] y realice los pasos siguientes en esta ubicación.

1. Ir a URL: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. Buscar `bundle.jar` y cambie el nombre de `bundle.jar` a `bundle.jar.bak`.
1. Copiar `bundle.jar` en esta ubicación desde el [Distribución de software](https://jira.corp.adobe.com/secure/attachment/9402702/bundle.jar).
1. Inicie Application Server, espere a que los registros se estabilicen y compruebe el estado del paquete.
1. Una vez que todos los paquetes estén en estado activado, instale la variable `org.apache.felix.http.servlet-api-1.2.0_fragment-full.jar` fragmento de servlet desde el `system/console/bundles` descargado de [Distribución de software.](https://jira.corp.adobe.com/secure/attachment/9396977/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)
1. De nuevo, espere a que el servidor de aplicaciones se estabilice.
1. Detenga el servidor de aplicaciones.
1. Vaya a `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` y elimine el `bundle.jar`.
1. Cambiar el nombre de `bundle.jar.bak` a `bundle.jar`.
1. Inicie el servidor de aplicaciones.

## Aplicable a {#applies-to}

Esta solución se aplica a:
* AEM Forms en todos los servidores JEE excepto en los que se ejecutan en JBoss EAP 7.4.0
