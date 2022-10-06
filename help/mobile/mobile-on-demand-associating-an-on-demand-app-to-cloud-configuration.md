---
title: Configuración de nube
seo-title: Cloud Configuration
description: La asociación de una aplicación bajo demanda a una configuración de nube permite que Adobe Experience Manager (AEM) se comunique directamente con un proyecto alojado por Mobile On-Demand estableciendo un vínculo bidireccional. Siga esta página para obtener más información.
seo-description: Associating an On-Demand App to a Cloud Configuration allows Adobe Experience Manager (AEM) to communicate directly with a Mobile On-Demand hosted project by establishing a two way link. Follow this page to learn more.
uuid: f377f2af-864b-43df-9d42-4a5fd6cd70d5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: d0d29b99-53d4-4b0d-947b-39d91b381de7
exl-id: 37428543-c310-4712-a4ec-1f482579fb4b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 2%

---

# Configuración de nube{#cloud-configuration}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

La asociación de una aplicación bajo demanda a una configuración de nube permite que Adobe Experience Manager (AEM) se comunique directamente con un proyecto alojado por Mobile On-Demand estableciendo un vínculo bidireccional. Al vincular su aplicación a un proyecto móvil bajo demanda, podrá crear contenido, como artículos, titulares y colecciones dentro de AEM, pero también servirlo en Mobile On-Demand.

A partir de ahí, será posible publicar, previsualizar y administrar contenido. También puede importar contenido existente de Mobile On-Demand en AEM y realizar ediciones de contenido.

## Configuración de Cloud {#setting-up-cloud-configuration}

>[!CAUTION]
>
>Antes de empezar a configurar la nube para la aplicación On-Demand, debe estar familiarizado con el aprovisionamiento y la configuración del cliente de AEM Mobile On-demand Services de AEM Mobile.
>
>Para obtener más información, consulte [Configuración de AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) en la sección Administración .

Para configurar los Cloud Services móviles bajo demanda, haga clic en el engranaje superior en la esquina superior derecha de la **Administrar conexión** desde el panel de la aplicación.

Debe estar familiarizado con el panel de aplicaciones y los mosaicos disponibles. Consulte [Panel de aplicaciones de AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md) para obtener más información.

### Configuración del vínculo a la nube {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>Asegúrese de que tiene una configuración de cliente y nube On-Demand existente.
>
>Para obtener más información, consulte [Configuración de AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) en la sección Administración .

Los pasos siguientes describen la configuración del vínculo a la configuración de la nube:

1. De **Móvil**, elija **Aplicaciones** y, a continuación, la aplicación móvil bajo demanda del catálogo.
1. Haga clic en el icono del engranaje en la **Administrar conexión** mosaico.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Introduzca la configuración ya existente o cree una nueva introduciendo el **Título de configuración**, **ID del dispositivo** y **Token de dispositivo**.

   ![imagen_1-66](assets/chlimage_1-66.png)

1. Una vez que **ID del dispositivo** y **Token de dispositivo** estén verificados, seleccione el proyecto bajo demanda de la lista.

   Haga clic en **Submit**.

   ![chlimage_1-67](assets/chlimage_1-67.png)

   La variable **Administrar conexión** El mosaico muestra la configuración de Cloud.

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >Si intenta cambiar el proyecto al que está asociada esta aplicación al cambiar de proyecto en el panel, recibirá una advertencia para los problemas de integridad del contenido, como se muestra en la figura siguiente:

   ![chlimage_1-69](assets/chlimage_1-69.png)

### Pasos siguientes {#the-next-steps}

Una vez configurada la configuración de nube para la aplicación, consulte los siguientes recursos para administrar contenido:

* [Administración de artículos](/help/mobile/mobile-on-demand-managing-articles.md)
* [Administración de titulares](/help/mobile/mobile-on-demand-managing-banners.md)
* [Administración de colecciones](/help/mobile/mobile-on-demand-managing-collections.md)
* [Carga de recursos compartidos](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicación/cancelación de la publicación del contenido](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Vista previa con comprobación preliminar](/help/mobile/aem-mobile-manage-ondemand-services.md)
