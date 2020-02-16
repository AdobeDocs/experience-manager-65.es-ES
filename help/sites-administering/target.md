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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Integración con Adobe Target{#integrating-with-adobe-target}

Como parte de Adobe Marketing Cloud, [Adobe Target](http://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) le permite aumentar la relevancia del contenido mediante la determinación de objetivos y la medición en todos los canales. Los especialistas en marketing utilizan Adobe Target para diseñar y ejecutar pruebas en línea, crear segmentos de audiencia sobre la marcha (según el comportamiento) y automatizar la segmentación del contenido y las experiencias en línea. AEM ha adoptado el flujo de trabajo de segmentación que se utiliza en Adobe Target Standard. Si utiliza Target, estará familiarizado con el entorno de edición de segmentación en AEM.

Integre sus sitios de AEM con Adobe Target para personalizar el contenido de sus páginas:

* Implemente la segmentación de contenido.
* Utilice las audiencias de Target para crear experiencias personalizadas.
* Envíe datos de contexto a Target cuando los visitantes interactúen con sus páginas.
* Rastree las tasas de conversión.

Para realizar la integración con Target, realice las siguientes tareas:

1. [Realizar tareas](/help/sites-administering/target-requirements.md)previas: Regístrese con Adobe Target y configure determinados aspectos de la instancia de creación de AEM. Su cuenta de Adobe Target debe tener como mínimo **aprobador **nivel de permisos. Además, debe proteger la configuración de la actividad en el nodo de publicación para que los usuarios no puedan acceder a ella.

1. O bien:

   1. [Optar por Adobe Target](/help/sites-administering/opt-in.md): El asistente para la selección toma la información de su cuenta de Target y crea una configuración de nube de Adobe Target y un marco de Target. El asistente también asocia los sitios con Target Framework. Si el asistente no se puede conectar al destino, consulte la sección de resolución de problemas [de](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) conexión. A continuación, puede [modificar las configuraciones](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations)de nube predeterminadas: Si es necesario, modifique la configuración de nube y el marco de trabajo que creó el asistente para la selección. Por ejemplo, modifique la estructura para enviar datos de contexto adicionales a Target. Si desea utilizar Adobe Analytics como fuente de informes para Adobe Target, debe modificar la configuración de nube para que señale a la configuración de A4T.
   1. [Integración manual con Adobe Target](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [Configurar actividades](/help/sites-authoring/activitylib.md): Asocie sus actividades a la configuración de la nube de Target.

>[!NOTE]
>
>Consulte también [Integración de AEM con Adobe Target y Adobe Analytics mediante DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

>[!NOTE]
>
>Si está utilizando Target con una configuración proxy personalizada, debe configurar ambas configuraciones proxy del cliente HTTP, ya que algunas funcionalidades de AEM están utilizando las API 3.x y otras, las API 4.x:
>
>* 3.x está configurado con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x está configurado con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



>[!CAUTION]
>
>You must secure the activity settings node **cq:ActivitySettings** on the publish instance so that it is inaccessible to normal users. El nodo de configuración de la actividad solo debe ser accesible para el servicio que administra la sincronización de actividades en Adobe Target.
>
>See [Prerequisites for Integrating with Adobe Target](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node) for detailed information.

Una vez completada la integración, puede [crear contenido](/help/sites-authoring/content-targeting-touch.md) de destino que envíe datos de visitantes a Adobe Target. Tenga en cuenta que los componentes de página requieren código específico para habilitar la segmentación de contenido. (Consulte [Desarrollo de contenido](/help/sites-developing/target.md)de destino).

>[!NOTE]
>
>Cuando se dirige a un componente en un autor de AEM, el componente realiza una serie de llamadas del lado del servidor a Adobe Target para registrar la campaña, configurar ofertas y recuperar segmentos de Adobe Target (si están configurados). No se realiza ninguna llamada al servidor desde la publicación de AEM en Adobe Target.

## Fuentes de información de fondo {#background-information-sources}

La integración de AEM con Adobe Target requiere el conocimiento de Adobe Target, la gestión de actividades de AEM y la gestión de audiencias de AEM. Debe estar familiarizado con la siguiente información:

* Adobe Target (consulte la documentación [de](https://marketing.adobe.com/resources/help/en_US/target/)Adobe Target).
* Consola de actividades de AEM (consulte [Administración de actividades](/help/sites-authoring/activitylib.md)).
* Audiencias AEM (consulte [Administración de audiencias](/help/sites-authoring/managing-audiences.md)).

>[!NOTE]
>
>Al trabajar con Adobe Target, se muestra el número máximo de artefactos permitidos en una campaña:
>
>* 50 ubicaciones
>* 2.000 experiencias
>* 50 métricas
>* 50 segmentos de informes
>



