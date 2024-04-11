---
title: Integración con Adobe Analytics
description: Obtenga información sobre cómo integrar Adobe Experience Manager AEM () con Adobe Analytics.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 0a87ece4-57ed-4022-a78a-264c1edf4b4e
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 60%

---

# Integración con Adobe Analytics{#integrating-with-adobe-analytics}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/integrations/integrating-adobe-analytics.html) |
| AEM 6.5 | Este artículo |


La integración de Adobe Analytics AEM y la integración de le permite realizar un seguimiento de la actividad de la página web:

* Una configuración de Adobe Analytics permite a AEM autenticarse con Adobe Analytics.
* Un marco de trabajo identifica los datos que se envían al grupo de informes de Adobe Analytics.

Los datos incluyen datos de páginas y usuarios; por ejemplo:

* datos que recopilan los componentes de AEM
* clics en vínculos
* información de uso de vídeo
* número de visitas a la página desde Adobe Analytics

Las siguientes páginas le ayudan a configurar la integración:

* [Conectarse a Adobe Analytics y crear marcos](/help/sites-administering/adobeanalytics-connect.md)
* [Configuración del seguimiento de vínculos para Adobe Analytics](/help/sites-administering/adobeanalytics-link.md)
* [Asignación de datos de componente con propiedades de Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md)
* [Configuración del seguimiento de vídeo para Adobe Analytics](/help/sites-administering/adobeanalytics-video.md)
* [Clasificaciones de Adobe](/help/sites-administering/adobeanalytics-classifications.md)

También puede utilizar la variable [Asistente de inclusión](/help/sites-administering/opt-in.md) para realizar fácilmente la integración.

>[!NOTE]
>
>Consulte también el artículo de procedimientos: [AEM Integración de los recursos de la con Adobe Target y Adobe Analytics mediante DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

## Información adicional {#further-information}

Consulte:

* [Ampliación de la integración de Adobe Analytics](/help/sites-developing/extending-analytics.md) para obtener información sobre el desarrollo de componentes que recopilan datos de usuario y la personalización del marco de trabajo de Adobe Analytics.
* El artículo de la base de conocimiento, [Integración de Adobe Analytics: solución de problemas](https://helpx.adobe.com/es/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), para obtener información acerca de la solución de problemas de la integración de Adobe Analytics.

>[!NOTE]
>
>Si utiliza Adobe Analytics con una configuración proxy personalizada, debe [configurar dos paquetes](/help/sites-deploying/configuring-osgi.md) OSGi (por ejemplo, con la consola web) necesarios para las configuraciones proxy del cliente **HTTP de Apache**. Ambas son necesarias, ya que algunas funcionalidades de AEM utilizan las API 3.x, mientras que otras utilizan las API 4.x. Configuración de:
>
>* **Cliente HTTP 3.1 de Day Commons** para configurar la API 3.x;
>  por ejemplo, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Configuración proxy de componentes HTTP de Apache** para configurar la API 4.x;
>  por ejemplo, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>
