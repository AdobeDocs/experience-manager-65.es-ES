---
title: Integración con Adobe Analytics
seo-title: Integración con Adobe Analytics
description: Aprenda a integrar AEM con Adobe Analytics.
seo-description: Aprenda a integrar AEM con Adobe Analytics.
uuid: d8548263-6ac5-45fb-8c70-52ecd4161bbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 444c522e-2f33-4f41-846c-8d317e799659
docset: aem65
translation-type: tm+mt
source-git-commit: ca25e66b280db479f69c487753a557b0240233da

---


# Integración con Adobe Analytics{#integrating-with-adobe-analytics}

La integración de Adobe Analytics y AEM le permite realizar un seguimiento de la actividad de su página web:

* Una configuración de Adobe Analytics permite que AEM se autentique con Adobe Analytics.
* Un marco identifica los datos que se envían al grupo de informes de Adobe Analytics.

Los datos incluyen datos de página y de usuario; por ejemplo:

* datos que recopilan los componentes de AEM
* clics en vínculos
* información de uso de vídeo
* el número de visitas de página de Adobe Analytics

Las páginas siguientes le ayudan a configurar la integración:

* [Conexión a Adobe Analytics y creación de marcos](/help/sites-administering/adobeanalytics-connect.md)
* [Configuración del seguimiento de vínculos para Adobe Analytics](/help/sites-administering/adobeanalytics-link.md)
* [Asignación de datos de componentes con propiedades de Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md)
* [Configuración del seguimiento de vídeo para Adobe Analytics](/help/sites-administering/adobeanalytics-video.md)
* [Clasificaciones de Adobe](/help/sites-administering/adobeanalytics-classifications.md)

También puede utilizar el asistente para la [inclusión](/help/sites-administering/opt-in.md) para realizar fácilmente la integración.

>[!NOTE]
>
>Consulte también el artículo explicativo: [Integración de AEM con Adobe Target y Adobe Analytics mediante DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

## Información adicional {#further-information}

Consulte:

* [Ampliación de la integración](/help/sites-developing/extending-analytics.md) de Adobe Analytics para obtener información sobre el desarrollo de componentes que recopilan datos de usuario y la personalización del marco de trabajo de Adobe Analytics.
* El artículo de la base de conocimientos, Integración de [Adobe Analytics: solución de problemas](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), para obtener información sobre la solución de problemas de la integración de Adobe Analytics.

>[!NOTE]
>
>Si utiliza Adobe Analytics con una configuración proxy personalizada, debe [configurar dos paquetes](/help/sites-deploying/configuring-osgi.md) OSGi (por ejemplo, con la consola web) necesarios para las configuraciones proxy del cliente **HTTP de** Apache. Ambas son necesarias, ya que algunas funcionalidades de AEM utilizan las API 3.x, mientras que otras utilizan las API 4.x. Configurar:
>
>* **Day Commons HTTP Client 3.1** para configurar la API 3.x;
   >  por ejemplo, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Configuración** proxy de componentes HTTP de Apache para configurar la API 4.x;
   >  por ejemplo, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



