---
title: AEM Compatibilidad con versiones anteriores en 6.5
seo-title: Backward Compatibility in AEM 6.5
description: AEM Aprenda a mantener sus aplicaciones y configuraciones compatibles con la versión 6.5 de la versión de
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
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# AEM Compatibilidad con versiones anteriores en 6.5{#backward-compatibility-in-aem}

## Información general {#overview}

>[!NOTE]
>
>Para obtener una lista de los cambios de contenido y configuración que no están dentro del ámbito del paquete de compatibilidad, consulte [AEM Reestructuración de repositorios en el sector de la](/help/sites-deploying/repository-restructuring.md).

AEM En la versión 6.5, todas las características se han desarrollado teniendo en cuenta la compatibilidad con versiones anteriores.

AEM En la mayoría de los casos, los clientes que ejecutan la versión 6.3 no deben tener que cambiar el código o las personalizaciones al realizar la actualización. AEM Para los clientes de 6.1 y 6.2 no hay cambios importantes adicionales a los que se enfrentarían durante una actualización a 6.3.

Para las excepciones en las que las funciones no se podían mantener compatibles con versiones anteriores, los problemas de incompatibilidad con versiones anteriores para paquetes y contenido se pueden mitigar instalando un paquete de compatibilidad para 6.4 (consulte cómo configurar a continuación para obtener detalles sobre dónde descargar). AEM Este paquete de compatibilidad ayudará a restaurar la compatibilidad en la mayoría de los casos para las aplicaciones compatibles con la versión 6.4 de la.

AEM AEM El paquete de compatibilidad permite ejecutar la compatibilidad en modo de compatibilidad y diferir el desarrollo personalizado respecto a las nuevas funciones de la aplicación

>[!NOTE]
>
>AEM Tenga en cuenta que el paquete de compatibilidad es solo una solución temporal para retrasar el desarrollo necesario para ser compatible con la versión 6.5 de la aplicación, y se recomienda solo como última opción si no puede abordar los problemas de compatibilidad mediante el desarrollo inmediatamente después de la actualización. Se recomienda cambiar al modo nativo y desinstalar el paquete de compatibilidad una vez que decida continuar con el desarrollo personalizado basado en 6.5 y disponer de la funcionalidad completa de 6.5.

![malla](assets/sase.png)

El paquete de compatibilidad tiene dos modos: **Enrutamiento habilitado** y **Enrutamiento deshabilitado**.

AEM Esto permite ejecutar la versión 6.5 en tres modos:

**Modo nativo:**

AEM El modo nativo es para los clientes que desean utilizar todas las nuevas funciones de la versión 6.5 y están listos para realizar algún desarrollo a fin de que sus personalizaciones funcionen con todas las nuevas funciones.

Esto significa que es posible que tenga que realizar ajustes en la aplicación inmediatamente después de la actualización.

**Modo de compatibilidad: paquete de compatibilidad instalado con enrutamiento habilitado**

El modo de compatibilidad es para clientes que tienen personalizaciones de interfaces que no son compatibles con versiones anteriores. AEM AEM Esto permite a los usuarios ejecutar en modo de compatibilidad y retrasar el desarrollo personalizado requerido en relación con las nuevas funciones de la aplicación que no son compatibles con algunos de sus códigos personalizados.

**Modo heredado: paquete de compatibilidad instalado con enrutamiento deshabilitado**

AEM El modo heredado es para clientes que tienen interfaces personalizadas basadas en código heredado o obsoleto de los que se ha movido el código del paquete de compatibilidad.

![sapete](assets/sapte.png)

## Configuración {#how-to-set-up}

El **AEM Paquete de compatibilidad de 6.4 para.5** se puede instalar como paquete utilizando el Administrador de paquetes. Puede descargar el [AEM Paquete de compatibilidad de 6.4 para 6.5 desde Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=compat*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=20&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fcompatpack%2Faem-compat-cq65-to-cq64) sitio.

Una vez instalado el paquete de compatibilidad, el enrutamiento se puede habilitar o deshabilitar mediante un conmutador en la configuración OSGI, como se muestra a continuación:

![Conmutadores de compatibilidad](assets/compat-switches.png)

Una vez instalado y configurado el paquete de compatibilidad, las funciones se utilizarán en función del modo de compatibilidad que se haya elegido.
