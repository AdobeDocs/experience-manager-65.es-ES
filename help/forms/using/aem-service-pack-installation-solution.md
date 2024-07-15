---
title: Errores no disponibles del servicio CRX/paquete y la página de inicio una vez instalado el último paquete de servicio 6.5.15.0
description: Errores no disponibles del servicio CRX/paquete y la página de inicio una vez instalado el último paquete de servicio 6.5.15.0
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 3%

---

# AEM Error de servicio no disponible después de instalar el paquete de servicio de (6.5.15.0). {#steps-to-resolve-error-after-installing-service-pack}

## Problema {#issue}

AEM Después de instalar el paquete de servicio [6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), el error se produce de la siguiente manera:
* ERROR [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException: No se puede resolver org.apache.sling.scripting.console

AEM Después de instalar el paquete de servicio 6.5.15.0 de, el CRX/paquete y la página de inicio muestran errores de servicio no disponible.

## Se aplica a lo siguiente: {#applies-to}

Esta solución se aplica a:
* AEM Forms en todos los servidores JEE excepto en los que se ejecutan en JBoss EAP 7.4.0

## Solución {#solution}

>[!NOTE]
>
>Los pasos de solución de problemas son aplicables a todos los servidores de aplicaciones excepto JBoss EAP 7.4.

AEM Después de instalar el paquete de servicio [6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), si el CRX/paquete y la página de inicio muestran errores de servicio no disponible, realice los siguientes pasos:

1. Detenga el servidor de aplicaciones.
1. Navegue hasta `[aem-forms root]\crx-repository\launchpad\felix\bundle52`.
1. Busque el archivo `bundle.info`.
1. Abra el archivo `bundle.info` en el editor de texto ANT y busque el nombre del paquete como `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >En caso de que el `bundle.info` de `bundle52` no contenga el paquete `org.apache.felix.http.bridge`, compruebe el número de paquete entre corchetes junto al `org.apache.felix.http.bridge`. A continuación, vaya a [aem-forms root]\crx-repository\launchpad\felix\bundle[x] y realice los siguientes pasos en esta ubicación.

1. Vaya a la dirección URL: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. Busque `bundle.jar` y cambie el nombre de `bundle.jar` a `bundle.jar.bak`.
1. Copie `Bundle for AEM 6.5 Forms on JEE Service Pack 15` en esta ubicación desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. Inicie el servidor de aplicaciones, espere a que los registros se estabilicen y compruebe el estado del paquete.
1. AEM Una vez que todos los paquetes estén en estado activo, instale el [Fragmento para Forms de la versión 6.5 en el paquete de servicio JEE 15](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) de `system/console/bundles` y espere a que se estabilice el servidor de aplicaciones.
1. Detenga el servidor de aplicaciones.
1. Vaya a `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` y elimine `bundle.jar`.
1. Cambie el nombre de `bundle.jar.bak` a `bundle.jar`.
1. Inicie el servidor de aplicaciones.
