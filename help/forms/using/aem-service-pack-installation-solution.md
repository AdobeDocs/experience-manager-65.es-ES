---
title: Errores no disponibles del servicio CRX/paquete y la página de inicio una vez instalado el último paquete de servicio 6.5.15.0
description: Errores no disponibles del servicio CRX/paquete y la página de inicio una vez instalado el último paquete de servicio 6.5.15.0
SEO Description: Trouble shooting steps to resolve the errors after installing latest 6.5.15.0 service pack
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: 8c4fb903-572c-5473-ad45-8ebb0d5d8134
    internal-label: AEM Forms on OSGi
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 30%
---
# Error de servicio no disponible después de instalar AEM (6.5.15.0) service pack {#steps-to-resolve-error-after-installing-service-pack}

## Problema {#issue}

Después de instalar el Service Pack [AEM 6.5.15.0 &#x200B;](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), el error se produce de la siguiente manera:
* ERROR [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException: No se puede resolver org.apache.sling.scripting.console

Después de instalar el Service Pack de AEM 6.5.15.0, el CRX/paquete y la página de inicio muestran errores de servicio no disponible.

## Se aplica a {#applies-to}

Esta solución se aplica a:
* AEM Forms en todos los servidores JEE excepto en los que se ejecutan en JBoss EAP 7.4.0

## Solución {#solution}

>[!NOTE]
>
>Los pasos de solución de problemas son aplicables a todos los servidores de aplicaciones excepto JBoss EAP 7.4.

Después de instalar [AEM 6.5.15.0 service pack](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), si CRX/bundle y la página de inicio muestran errores de servicio no disponible, realice los siguientes pasos:

1. Detenga el servidor de aplicaciones.
1. Navegue hasta `[aem-forms root]\crx-repository\launchpad\felix\bundle52`.
1. Guarde el archivo `bundle.info`.
1. Abra el archivo `bundle.info` en el editor de texto ANT y busque el nombre del paquete como `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >En caso de que el `bundle.info` de `bundle52` no contenga el paquete `org.apache.felix.http.bridge`, compruebe el número de paquete entre corchetes junto al `org.apache.felix.http.bridge`. A continuación, vaya a [aem-forms root]\crx-repository\launchpad\felix\bundle[x] y realice los siguientes pasos en esta ubicación.

1. Vaya a la dirección URL: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. Busque `bundle.jar` y cambie el nombre de `bundle.jar` a `bundle.jar.bak`.
1. Copie `Bundle for AEM 6.5 Forms on JEE Service Pack 15` en esta ubicación desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. Inicie el servidor de aplicaciones, espere a que los registros se estabilicen y compruebe el estado del paquete.
1. Una vez que todos los paquetes estén en estado activo, instale el [Fragmento para AEM 6.5 Forms en el paquete de servicio JEE 15](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) de `system/console/bundles` y espere a que se estabilice el servidor de aplicaciones.
1. Detenga el servidor de aplicaciones.
1. Vaya a `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` y elimine `bundle.jar`.
1. Cambie el nombre de `bundle.jar.bak` a `bundle.jar`.
1. Inicie el servidor de aplicaciones.
