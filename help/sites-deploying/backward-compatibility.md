---
title: Compatibilidad con versiones anteriores en AEM 6.5
seo-title: Backward Compatibility in AEM 6.5
description: Obtenga información sobre cómo mantener las aplicaciones y configuraciones compatibles con AEM 6.5
seo-description: Learn how to keep your apps and configurations compatible with AEM 6.5
uuid: 81dc2771-f59b-4b24-8932-9e938cba05e0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: f3b4ec1d-9054-47d4-afcb-0a0121b94190
docset: aem65
feature: Upgrading
exl-id: c432a014-2dab-4c49-a25b-e4f461d13f9b
source-git-commit: 50a11e30ccd720065962e8dd03cbcc71ec9f715a
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# Compatibilidad con versiones anteriores en AEM 6.5{#backward-compatibility-in-aem}

## Información general {#overview}

>[!NOTE]
>
>Para obtener una lista de los cambios de contenido y configuración que no están dentro del ámbito del paquete de compatibilidad, consulte [Reestructuración del repositorio en AEM](/help/sites-deploying/repository-restructuring.md).

En AEM 6.5, todas las características se han desarrollado teniendo en cuenta la compatibilidad con versiones anteriores.

En la mayoría de los casos, los clientes que ejecutan AEM 6.3 no deben cambiar el código o las personalizaciones al realizar la actualización. Para los clientes de AEM 6.1 y 6.2, no hay cambios de ruptura adicionales que los que se enfrentarían durante una actualización a 6.3.

Para excepciones en las que las funciones no se podían mantener compatibles con versiones anteriores, los problemas de incompatibilidad con versiones anteriores de paquetes y contenido se pueden mitigar instalando un paquete de compatibilidad para la versión 6.4 (consulte cómo configurar la configuración siguiente para obtener más información sobre dónde descargar). Este paquete compat ayudará a restaurar la compatibilidad en la mayoría de los casos para aplicaciones compatibles con AEM 6.4.

El paquete de compatibilidad le permite ejecutar AEM en modo de compatibilidad y diferir el desarrollo personalizado con las nuevas funciones de AEM:

>[!NOTE]
>
>Tenga en cuenta que el paquete de compatibilidad es solo una solución temporal para retrasar el desarrollo necesario para ser compatible con AEM 6.5. Se recomienda solo como última opción si no puede abordar los problemas de compatibilidad mediante el desarrollo inmediatamente después de la actualización. Se recomienda cambiar al modo nativo y desinstalar el paquete de compatibilidad cuando decida continuar con el desarrollo personalizado basado en 6.5 y disponer de la funcionalidad completa 6.5.

![sase](assets/sase.png)

El paquete de compatibilidad tiene dos modos: **Enrutamiento habilitado** y **Enrutamiento deshabilitado**.

Esto permite ejecutar AEM 6.5 en tres modos:

**Modo nativo:**

El modo nativo es para clientes que desean utilizar todas las nuevas funciones de AEM 6.5 y están listos para hacer algo de desarrollo para que sus personalizaciones funcionen con todas las nuevas funciones.

Esto significa que es posible que tenga que realizar ajustes en la aplicación inmediatamente después de la actualización.

**Modo de compatibilidad: Paquete de compatibilidad instalado con enrutamiento habilitado**

El modo de compatibilidad es para clientes que tienen personalizaciones de interfaces que no son compatibles con versiones anteriores. Esto permite que la AEM se ejecute en modo de compatibilidad y que se aplace el desarrollo personalizado necesario para las nuevas funciones de AEM que no son compatibles con algunos de sus códigos personalizados.

**Modo heredado: Paquete de compatibilidad instalado con enrutamiento deshabilitado**

El modo heredado es para clientes que tienen interfaces personalizadas basadas en código heredado o obsoleto de AEM que se ha movido fuera del paquete de compatibilidad.

![sapte](assets/sapte.png)

## Configuración {#how-to-set-up}

La variable **AEM 6.4 Compatability Pack para 6.5** se puede instalar como un paquete mediante el Administrador de paquetes. Puede descargar el [AEM 6.4 Compatability Pack para 6.5 de la distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=compat*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=20&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fcompatpack%2Faem-compat-cq65-to-cq64) sitio.

Una vez instalado el paquete de compatibilidad, el enrutamiento se puede habilitar o deshabilitar utilizando un conmutador en la configuración OSGI como se muestra a continuación:

![Conmutadores compactos](assets/compat-switches.png)

Una vez instalado y configurado el paquete de compatibilidad, las funciones se utilizan en función del modo de compatibilidad seleccionado.
