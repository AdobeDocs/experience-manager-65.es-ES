---
title: Configuración de nube
description: La asociación de una aplicación bajo demanda a una configuración en la nube permite a Adobe Experience Manager AEM () comunicarse directamente con un proyecto alojado de Mobile On-Demand mediante el establecimiento de un vínculo bidireccional. Siga esta página para obtener más información.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: 37428543-c310-4712-a4ec-1f482579fb4b
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 2%

---

# Configuración de nube{#cloud-configuration}

{{ue-over-mobile}}

La asociación de una aplicación bajo demanda a una configuración en la nube permite a Adobe Experience Manager AEM () comunicarse directamente con un proyecto alojado de Mobile On-Demand mediante el establecimiento de un vínculo bidireccional. AEM Al vincular la aplicación a un proyecto de Mobile On-Demand, podrá crear contenido, como artículos, titulares y colecciones, dentro de la aplicación, pero también podrá servir ese contenido a Mobile On-Demand.

A partir de ahí, es posible publicar, previsualizar y administrar contenido. AEM También puede importar contenido existente de Mobile On-Demand en y realizar ediciones de contenido en la interfaz de usuario de.

## Configuración de nube {#setting-up-cloud-configuration}

>[!CAUTION]
>
>Antes de empezar a configurar la nube para la aplicación On-Demand, debe estar familiarizado con el aprovisionamiento de AEM Mobile y la configuración del cliente de AEM Mobile On-demand Services.
>
>Para obtener más información, consulte [Configuración de AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) en la sección Administración.

Para configurar los Cloud Service de Mobile On-Demand, haga clic en la parte superior derecha del mosaico **Administrar conexión** desde el panel de la aplicación.

Debe estar familiarizado con el panel de la aplicación y los mosaicos disponibles. Consulte [Tablero de aplicación de AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md) para obtener más información.

### Configuración del vínculo a la nube {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>Asegúrese de que tiene una configuración de cliente On-Demand y de nube existente.
>
>Para obtener más información, consulte [Configuración de AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) en la sección Administración.

Los siguientes pasos describen la configuración del vínculo a la nube:

1. Desde **Mobile**, elige **Aplicaciones** y luego tu aplicación de Mobile On-Demand en el catálogo.
1. Haga clic en el icono de engranaje en el mosaico **Administrar conexión**.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Escriba la configuración ya existente o cree una escribiendo **Título de configuración**, **Id. de dispositivo** y **Token de dispositivo**.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Una vez verificados **Id. de dispositivo** y **Token de dispositivo**, elija su proyecto a petición en la lista.

   Haga clic en **Enviar**.

   ![chlimage_1-67](assets/chlimage_1-67.png)

   El mosaico **Administrar conexión** muestra su configuración de nube.

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >Si intenta cambiar a qué proyecto está asociada esta aplicación, mientras cambia de proyecto en el panel, recibirá una advertencia por problemas de integridad del contenido, como se muestra en la figura siguiente:

   ![chlimage_1-69](assets/chlimage_1-69.png)

### Pasos siguientes {#the-next-steps}

Una vez que haya configurado la nube para su aplicación, consulte los siguientes recursos para administrar contenido:

* [Administrar artículos](/help/mobile/mobile-on-demand-managing-articles.md)
* [Administración de titulares](/help/mobile/mobile-on-demand-managing-banners.md)
* [Administración de colecciones](/help/mobile/mobile-on-demand-managing-collections.md)
* [Carga de recursos compartidos](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicación/cancelación de la publicación del contenido](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Vista previa con comprobación preliminar](/help/mobile/aem-mobile-manage-ondemand-services.md)
