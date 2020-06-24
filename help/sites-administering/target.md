---
title: Integración con Adobe Target
seo-title: Integración con Adobe Target
description: Obtenga información sobre la integración de AEM con Adobe Target.
seo-description: Obtenga información sobre la integración de AEM con Adobe Target.
uuid: b90346e8-9757-4272-a870-bbe5e647303f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 454854f8-6053-406c-888d-f427777bf570
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 5%

---


# Integración con Adobe Target{#integrating-with-adobe-target}

Como parte del Adobe Marketing Cloud, [Adobe Target](http://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) le permite aumentar la relevancia del contenido mediante la determinación de objetivos y la medición en todos los canales. Los especialistas en marketing utilizan Adobe Target para diseñar y ejecutar pruebas en línea, crear segmentos de audiencia sobre la marcha (según el comportamiento) y automatizar la segmentación del contenido y las experiencias en línea. AEM ha adoptado el flujo de trabajo de segmentación que se utiliza en Adobe Target Standard. Si utiliza Destinatario, estará familiarizado con el entorno de edición de segmentación en AEM.

Integre sus sitios de AEM con Adobe Target para personalizar el contenido de sus páginas:

* Implemente la segmentación de contenido.
* Utilice audiencias de Destinatario para crear experiencias personalizadas.
* Enviar datos de contexto a Destinatario cuando los visitantes interactúen con las páginas.
* Rastrear tasas de conversión.

Para realizar la integración con Destinatario, realice las siguientes tareas:

1. [Realizar tareas](/help/sites-administering/target-requirements.md)previas: Regístrese con Adobe Target y configure determinados aspectos de la instancia de creación de AEM. La cuenta de Adobe Target debe tener como mínimo **aprobador **nivel de permisos. Además, debe proteger la configuración de actividad en el nodo de publicación para que los usuarios no puedan acceder a ella.

1. O bien:

   1. [Optar por el Adobe Target](/help/sites-administering/opt-in.md): El asistente para la selección toma la información de su cuenta de Destinatario y crea una configuración de nube de Adobe Target y un Destinatario Framework. El asistente también asocia los sitios con Destinatario Framework. Si el asistente no puede conectarse a destinatario, consulte la sección de resolución de problemas de [conexión](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) . A continuación, puede [modificar las configuraciones](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations)de nube predeterminadas: Si es necesario, modifique la configuración de nube y el marco de trabajo que creó el asistente para la selección. Por ejemplo, modifique la estructura para enviar datos de contexto adicionales a Destinatario. Si desea utilizar Adobe Analytics como fuente de sistema de informes para Adobe Target, debe modificar la configuración de nube para que señale a la configuración de A4T.
   1. [Integración manual con Adobe Target](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [Configurar Actividades](/help/sites-authoring/activitylib.md): Asocie sus Actividades con la configuración de la nube de Destinatario.

>[!NOTE]
>
>Consulte también [Integración de AEM con Adobe Target y Adobe Analytics mediante DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

>[!NOTE]
>
>Si está utilizando Destinatario con una configuración proxy personalizada, debe configurar ambas configuraciones proxy del cliente HTTP, ya que algunas funcionalidades de AEM están utilizando las API 3.x y otras las API 4.x:
>
>* 3.x está configurado con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x está configurado con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



>[!CAUTION]
>
>You must secure the activity settings node **cq:ActivitySettings** on the publish instance so that it is inaccessible to normal users. El nodo de configuración de la actividad solo debe ser accesible para el servicio que administra la sincronización de actividades en Adobe Target.
>
>See [Prerequisites for Integrating with Adobe Target](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node) for detailed information.

Una vez completada la integración, puede [crear contenido](/help/sites-authoring/content-targeting-touch.md) de destino que envíe datos de visitante a Adobe Target. Tenga en cuenta que los componentes de página requieren código específico para habilitar la segmentación de contenido. (Consulte [Desarrollo de contenido](/help/sites-developing/target.md)de destino).

>[!NOTE]
>
>Cuando se destinatario un componente en el autor de AEM, el componente realiza una serie de llamadas del lado del servidor a Adobe Target para registrar la campaña, configurar ofertas y recuperar segmentos de Adobe Target (si están configurados). No se realizan llamadas del lado del servidor desde la publicación de AEM en Adobe Target.

## Fuentes de información de fondo {#background-information-sources}

La integración de AEM con Adobe Target requiere conocimientos sobre Adobe Target, administración de Actividades de AEM y administración de Audiencias de AEM. Debe estar familiarizado con la siguiente información:

* Adobe Target (consulte la documentación [de](https://docs.adobe.com/content/help/en/target/using/target-home.html)Adobe Target).
* Consola de Actividades AEM (consulte [Administración de Actividades](/help/sites-authoring/activitylib.md)).
* Audiencias AEM (consulte [Administración de Audiencias](/help/sites-authoring/managing-audiences.md)).

>[!NOTE]
>
>Cuando se trabaja con Adobe Target, el número máximo de artefactos permitidos dentro de una campaña es el siguiente:
>
>* 50 ubicaciones
>* 2.000 experiencias
>* 50 métricas
>* 50 segmentos de sistema de informes

>



