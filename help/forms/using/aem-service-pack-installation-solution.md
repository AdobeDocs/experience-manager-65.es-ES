---
title: Errores no disponibles del servicio CRX/paquete y la página de inicio una vez instalado el último paquete de servicio 6.5.15.0
description: Errores no disponibles del servicio CRX/paquete y la página de inicio una vez instalado el último paquete de servicio 6.5.15.0
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
source-git-commit: e961f0c7107b4eacb0d5e50565cb64f5fa30e265
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 3%

---

# AEM Error de servicio no disponible después de instalar el paquete de servicio de (6.5.15.0). {#steps-to-resolve-error-after-installing-service-pack}

## Problema {#issue}

Después de instalar el [AEM Paquete de servicio 6.5.15.0 de](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), el error se produce de la siguiente manera:
* ERROR [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException: No se puede resolver org.apache.sling.scripting.console

AEM Después de instalar el paquete de servicio 6.5.15.0 de, el CRX/paquete y la página de inicio muestran errores de servicio no disponible.

## Se aplica a {#applies-to}

Esta solución se aplica a:
* AEM Forms en todos los servidores JEE excepto en los que se ejecutan en JBoss EAP 7.4.0

## Solución {#solution}

>[!NOTE]
>
>Los pasos de solución de problemas son aplicables a todos los servidores de aplicaciones excepto JBoss EAP 7.4.

Después de la instalación [AEM Paquete de servicio 6.5.15.0 de](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)Sin embargo, si el CRX/paquete y la página de inicio muestran errores de servicio no disponible, realice los siguientes pasos:

1. Detenga el servidor de aplicaciones.
1. Navegue hasta `[aem-forms root]\crx-repository\launchpad\felix\bundle52`.
1. Busque el `bundle.info` archivo.
1. Abra el `bundle.info` en el editor de texto de ant y busque el nombre del paquete como `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >En caso de que la `bundle.info` bajo `bundle52` no contiene la variable `org.apache.felix.http.bridge` paquete, compruebe el número de paquete entre corchetes junto al `org.apache.felix.http.bridge`. A continuación, vaya a [raíz de aem-forms]\crx-repository\launchpad\felix\bundle[x] y realice los siguientes pasos en esta ubicación.

1. Ir a URL: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. Buscar por `bundle.jar` y cambie el nombre de `bundle.jar` hasta `bundle.jar.bak`.
1. Copie el `Bundle for AEM 6.5 Forms on JEE Service Pack 15` en esta ubicación desde el [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. Inicie el servidor de aplicaciones, espere a que los registros se estabilicen y compruebe el estado del paquete.
1. Una vez que todos los paquetes estén en estado activo, instale el [AEM Fragmento para Forms de 6.5 en el paquete de servicio 15 de JEE](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) desde el `system/console/bundles` y espere a que se estabilice el servidor de aplicaciones.
1. Detenga el servidor de aplicaciones.
1. Vaya a `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` y elimine el `bundle.jar`.
1. Cambie el nombre del `bundle.jar.bak` a la `bundle.jar`.
1. Inicie el servidor de aplicaciones.
