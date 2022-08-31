---
title: Integración con Adobe Target
seo-title: Integrating with Adobe Target
description: Obtenga información sobre la integración de AEM con Adobe Target.
seo-description: Learn about integrating AEM with Adobe Target.
uuid: b90346e8-9757-4272-a870-bbe5e647303f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 454854f8-6053-406c-888d-f427777bf570
exl-id: 2b17d8cd-a43c-4d54-b990-a6f0cb1db22b
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 63%

---

# Integración con Adobe Target{#integrating-with-adobe-target}

Como parte de Adobe Marketing Cloud, [Adobe Target](https://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) permite aumentar la relevancia del contenido mediante el direccionamiento y efectuando mediciones en todos los canales. Los especialistas en marketing utilizan Adobe Target para diseñar y ejecutar pruebas en línea, crear segmentos de audiencia sobre la marcha (basados en el comportamiento) y automatizar el direccionamiento del contenido y las experiencias en línea. AEM ha adoptado el flujo de trabajo de objetivos que se utiliza en Adobe Target Standard. Si usa Target, estará familiarizado con el entorno de edición de segmentación en AEM.

Integre los AEM Sites con Adobe Target para personalizar el contenido de sus páginas:

* Implemente la segmentación de contenido.
* Utilice las audiencias de Target para crear experiencias personalizadas.
* Envíe datos de contexto a Target cuando los visitantes interactúen con las páginas.
* Rastree las tasas de conversión.

Para integrarse con Target, realice las siguientes tareas:

1. [Realizar tareas previas](/help/sites-administering/target-requirements.md): regístrese en Adobe Target y configure ciertos aspectos de la instancia de autor de AEM. Su cuenta de Adobe Target debe tener permisos de **aprobador **nivel como mínimo. Además, debe proteger la configuración de actividad en el nodo de publicación para que los usuarios no puedan acceder a ella.

1. O bien, haga lo siguiente:

   1. [Opt-in Adobe Target](/help/sites-administering/opt-in.md): El asistente de inclusión toma la información de su cuenta de Target y crea una configuración de nube de Adobe Target y un marco de Target. El asistente también asocia sus sitios con Target Framework. Si el asistente no puede conectarse a target, consulte la sección [solucionar problemas de conexión](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) para obtener más información. Entonces puede [Modificación de las configuraciones de nube predeterminadas](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations): Si es necesario, modifique la configuración de nube y el marco que creó el asistente de inclusión. Por ejemplo, modifique la estructura para enviar datos de contexto adicionales a Target. Si desea utilizar Adobe Analytics como fuente de informes para Adobe Target, debe modificar la configuración de la nube para que apunte a la configuración de A4T.
   1. [Integración manual con Adobe Target](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [Configurar actividades](/help/sites-authoring/activitylib.md): asocie sus actividades a la configuración de nube de Target.

>[!NOTE]
>
>Consulte también [Integración de AEM con Adobe Target y Adobe Analytics mediante DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

>[!NOTE]
>
>Si utiliza Target con una configuración proxy personalizada, debe configurar ambas configuraciones proxy del cliente HTTP, ya que algunas funcionalidades de AEM utilizan las API 3.x y otras las API 4.x.
>
>* 3.x está configurado con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x está configurado con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


>[!CAUTION]
>
>Debe asegurar el nodo de configuración de actividades **cq:ActivitySettings** de la instancia de publicación, para que los usuarios normales no puedan obtener acceso a él. El nodo de configuración de la actividad solo debe ser accesible para el servicio que administra la sincronización de actividades en Adobe Target.
>
>Consulte [Requisitos previos para la integración con Adobe Target](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node) para obtener información detallada.

Cuando se complete la integración, puede [crear contenido de destino](/help/sites-authoring/content-targeting-touch.md) para enviar datos sobre visitantes a Adobe Target. Tenga en cuenta que los componentes de página requieren un código específico para habilitar la segmentación de contenido. (Consulte [Desarrollo de contenido de destino](/help/sites-developing/target.md)).)

>[!NOTE]
>
>Cuando se marca un componente como objetivo en el autor AEM, este realiza una serie de llamadas del lado del servidor a Adobe Target para registrar la campaña, configurar ofertas y recuperar segmentos de Adobe Target (si están configurados). No se realizan llamadas del lado del servidor desde publicaciones de AEM a Adobe Target.

## Fuentes de información de fondo {#background-information-sources}

La integración de AEM con Adobe Target requiere conocimientos de Adobe Target, administración de actividades de AEM y administración AEM audiencias. Debe estar familiarizado con la siguiente información:

* Adobe Target (consulte la [documentación de Adobe Target](https://docs.adobe.com/content/help/en/target/using/target-home.html)).
* Consola AEM actividades (consulte [Administración de actividades](/help/sites-authoring/activitylib.md)).
* Audiencias AEM (Consulte [Administración de audiencias](/help/sites-authoring/managing-audiences.md)).

>[!NOTE]
>
>Al trabajar con Adobe Target, el siguiente número de artefactos es el máximo permitido dentro de una campaña:
>
>* 50 ubicaciones
>* 2000 experiencias
>* 50 métricas
>* 50 segmentos de creación de informes
>

