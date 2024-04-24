---
title: AEM Compatibilidad con versiones anteriores en 6.5
description: Obtenga información sobre cómo mantener las aplicaciones y configuraciones compatibles con Adobe Experience Manager AEM () 6.5
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
docset: aem65
feature: Upgrading
exl-id: c432a014-2dab-4c49-a25b-e4f461d13f9b
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# AEM Compatibilidad con versiones anteriores en 6.5{#backward-compatibility-in-aem}

## Información general {#overview}

>[!NOTE]
>
>Para obtener una lista de los cambios de contenido y configuración que no están dentro del ámbito del paquete de compatibilidad, consulte [AEM Reestructuración de repositorios en el sector de la](/help/sites-deploying/repository-restructuring.md).

En Adobe Experience Manager AEM () 6.5, todas las funciones se han desarrollado teniendo en cuenta la compatibilidad con versiones anteriores.

AEM Normalmente, los clientes que ejecutan la versión 6.3 no deberían tener que cambiar el código o las personalizaciones al realizar la actualización. AEM Para los clientes de la versión 6.1 y 6.2, no hay cambios importantes adicionales a los que se enfrentaría durante una actualización a la versión 6.3.

En el caso de las excepciones en las que las funciones no se podían mantener compatibles con versiones anteriores, se pueden mitigar los problemas de incompatibilidad con versiones anteriores para paquetes y contenido. Para ello, instale un paquete de compatibilidad para 6.4 (consulte cómo configurarlo a continuación para obtener más información sobre dónde descargarlo). AEM Este paquete de compatibilidad ayuda a restaurar la compatibilidad normalmente para las aplicaciones compatibles con la versión 6.4 de la aplicación de.

AEM AEM El paquete de compatibilidad permite ejecutar la compatibilidad en modo de compatibilidad y diferir el desarrollo personalizado respecto a las nuevas funciones de la aplicación

>[!NOTE]
>
>AEM El paquete de compatibilidad es solo una solución temporal para aplazar el desarrollo necesario para ser compatible con la versión 6.5 de la versión de. El Adobe solo lo recomienda como última opción si no puede abordar los problemas de compatibilidad mediante el desarrollo inmediatamente después de la actualización. Además, Adobe recomienda cambiar al modo nativo y desinstalar el paquete de compatibilidad una vez que decida continuar con el desarrollo personalizado basado en 6.5 y disponer de la funcionalidad completa de 6.5.

![malla](assets/sase.png)

El paquete de compatibilidad tiene dos modos: **Enrutamiento habilitado** y **Enrutamiento deshabilitado**.

AEM Esto permite que la versión 6.5 se ejecute en tres modos:

**Modo nativo:**

AEM El modo nativo es para los clientes que desean utilizar todas las nuevas funciones de la versión 6.5 y están listos para realizar algún desarrollo a fin de que sus personalizaciones funcionen con todas las nuevas funciones.

Esto significa que debe ajustar la aplicación inmediatamente después de la actualización.

**Modo de compatibilidad: paquete de compatibilidad instalado con enrutamiento habilitado**

El modo de compatibilidad es para clientes que tienen personalizaciones de interfaces que no son compatibles con versiones anteriores. AEM AEM Esto permite a los usuarios ejecutar en modo de compatibilidad y retrasar el desarrollo personalizado requerido en relación con las nuevas funciones de la aplicación que no son compatibles con algunos de sus códigos personalizados.

**Modo heredado: paquete de compatibilidad instalado con enrutamiento deshabilitado**

AEM El modo heredado es para clientes que tienen interfaces personalizadas basadas en código heredado o obsoleto de los que se ha movido el código del paquete de compatibilidad.

![sapete](assets/sapte.png)

## Configuración {#how-to-set-up}

El **AEM Paquete de compatibilidad de 6.4 para.5** se puede instalar como paquete utilizando el Administrador de paquetes. Puede descargar el [AEM Paquete de compatibilidad de.4 para 6.5 desde Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=compat*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=20&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fcompatpack%2Faem-compat-cq65-to-cq64) sitio.

Una vez instalado el paquete de compatibilidad, el enrutamiento se puede habilitar o deshabilitar mediante un conmutador en la configuración OSGI, como se muestra a continuación:

![Conmutadores de compatibilidad](assets/compat-switches.png)

Una vez instalado y configurado el paquete de compatibilidad, las funciones se utilizan en función del modo de compatibilidad que se haya elegido.
