---
title: Compatibilidad con versiones anteriores en AEM 6.5
seo-title: Compatibilidad con versiones anteriores en AEM 6.5
description: Descubra cómo mantener sus aplicaciones y configuraciones compatibles con AEM 6.5
seo-description: Descubra cómo mantener sus aplicaciones y configuraciones compatibles con AEM 6.5
uuid: 81dc2771-f59b-4b24-8932-9e938cba05e0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: f3b4ec1d-9054-47d4-afcb-0a0121b94190
docset: aem65
translation-type: tm+mt
source-git-commit: c863e438df45fd54c29c1b99114eea07aaeb6162

---


# Compatibilidad con versiones anteriores en AEM 6.5{#backward-compatibility-in-aem}

## Información general {#overview}

>[!NOTE]
>
>Para obtener una lista de los cambios de contenido y configuración que no están dentro del ámbito del paquete de compatibilidad, consulte Reestructuración [del repositorio en AEM](/help/sites-deploying/repository-restructuring.md).

En AEM 6.5, todas las funciones se han desarrollado teniendo en cuenta la compatibilidad con versiones anteriores.

En la mayoría de los casos, los clientes que ejecutan AEM 6.3 no deben cambiar el código o las personalizaciones al realizar la actualización. Para los clientes de AEM 6.1 y 6.2, no hay cambios de ruptura adicionales que los que se producirían durante una actualización a 6.3.

En el caso de excepciones en las que las funciones no se podían mantener compatibles con versiones anteriores, los problemas de incompatibilidad con versiones anteriores para paquetes y contenido se pueden mitigar mediante la instalación de un paquete de compatibilidad para 6.4 (consulte cómo configurar a continuación para obtener más detalles sobre dónde descargar). Este paquete compat ayudará a restaurar la compatibilidad en la mayoría de los casos para las aplicaciones compatibles con AEM 6.4.

El paquete de compatibilidad le permite ejecutar AEM en modo de compatibilidad y aplazar el desarrollo personalizado con las nuevas funciones de AEM:

>[!NOTE]
>
>Tenga en cuenta que el paquete de compatibilidad es sólo una solución temporal para aplazar el desarrollo necesario para ser compatible con AEM 6.5, y su recomendación solo es una última opción si no puede resolver problemas de compatibilidad mediante el desarrollo inmediatamente después de la actualización. Se recomienda encarecidamente cambiar al modo nativo y desinstalar el paquete de compatibilidad una vez que decida continuar con el desarrollo personalizado basado en 6.5 y aprovechar la funcionalidad completa de 6.5.

![sase](assets/sase.png)

El paquete de compatibilidad tiene dos modos: **Enrutamiento habilitado** y **enrutamiento deshabilitado**.

Esto permite que AEM 6.5 se ejecute en tres modos:

**Modo nativo:**

El modo nativo es para clientes que desean utilizar todas las nuevas funciones de AEM 6.5 y están listos para realizar algunas tareas de desarrollo para que sus personalizaciones funcionen con todas las nuevas funciones.

Esto significa que es posible que deba realizar ajustes en la aplicación inmediatamente después de la actualización.

**Modo de compatibilidad: Paquete de compatibilidad instalado con enrutamiento habilitado**

El modo de compatibilidad es para clientes que tienen personalizaciones de interfaces que no son compatibles con versiones anteriores. Esto permite que AEM se ejecute en modo de compatibilidad y aplace el desarrollo personalizado necesario para las nuevas funciones de AEM que no sean compatibles con algunos de sus códigos personalizados.

**Modo heredado: Paquete de compatibilidad instalado con enrutamiento deshabilitado**

El modo heredado es para clientes que tienen interfaces personalizadas basadas en código heredado o obsoleto de AEM que se ha trasladado al paquete de compatibilidad.

![sapte](assets/sapte.png)

## Cómo configurar {#how-to-set-up}

El paquete de compatibilidad de AEM 6.3 se podrá instalar como paquete mediante el Administrador de paquetes en este [vínculo](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/compatpack/aem-compat-cq64-to-cq63).

Una vez instalado el Paquete de compatibilidad, el enrutamiento se puede habilitar o deshabilitar mediante un conmutador en la configuración OSGI, como se muestra a continuación:

![screen_shot_2017-11-27at122421pm](assets/screen_shot_2017-11-27at122421pm.png)

Una vez que se haya instalado y configurado el paquete de compatibilidad, las funciones se utilizarán según el modo de compatibilidad elegido.
