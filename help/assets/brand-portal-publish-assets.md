---
title: Publicar recursos en Brand Portal
seo-title: Publish assets to Brand Portal
description: Obtenga información sobre cómo publicar y cancelar la publicación de recursos en Brand Portal.
seo-description: Learn how to publish and unpublish assets to Brand Portal.
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
feature: Brand Portal
role: User
exl-id: 76652a16-cad6-4e95-9e66-41efec452b03
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 42%

---

# Publicar recursos en Brand Portal {#publish-assets-to-brand-portal}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en) |
| AEM 6.5 | Este artículo |
| AEM 6.4 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/brandportal/brand-portal-publish-assets.html?lang=en) |

Como administrador de recursos de Adobe Experience Manager (AEM), puede publicar recursos y carpetas en la instancia de AEM Assets Brand Portal (o programar el flujo de trabajo de publicación para una fecha y hora posteriores) para su organización. Sin embargo, primero debe configurar AEM Assets con Brand Portal. Para obtener más información, consulte [Configurar AEM Assets con Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Una vez que la replicación se haya realizado correctamente, puede publicar recursos, carpetas y colecciones en Brand Portal. Para publicar recursos en Brand Portal, siga estos pasos:

>[!NOTE]
>
>Adobe recomienda la publicación escalonada, de preferencia durante las horas no pico, para que el autor de AEM no ocupe recursos excesivos.

1. En la consola Recursos, seleccione los recursos o la carpeta que desee publicar y haga clic en **[!UICONTROL Publicación rápida]** en la barra de herramientas.

   También puede seleccionar los recursos que desea publicar en Brand Portal.

   ![publish2bp-2](assets/publish2bp.png)

1. Para publicar los recursos en Brand Portal, hay dos opciones disponibles:
   * [Publicar recursos inmediatamente](#publish-to-bp-now)
   * [Publicar recursos más tarde](#publish-to-bp-now)

## Publicar recursos ahora {#publish-to-bp-now}

Para publicar los recursos seleccionados en Brand Portal, haga una de las acciones siguientes:

* En la barra de herramientas, seleccione **[!UICONTROL Publicación rápida]**. A continuación, en el menú , seleccione **[!UICONTROL Publicar en Brand Portal]**.

* En la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**.

   1. A continuación, desde el **[!UICONTROL Acción]** select **[!UICONTROL Publicar en Brand Portal]** y de **[!UICONTROL Programación]** select **[!UICONTROL Ahora]**. Haga clic en **[!UICONTROL Siguiente]**.

   2. Within **[!UICONTROL Ámbito]**, confirme la selección y haga clic en **[!UICONTROL Publicar en Brand Portal]**.

Aparece un mensaje que indica que los recursos se han puesto en cola para su publicación en Brand Portal. Inicie sesión en la interfaz de Brand Portal para ver los recursos publicados.

## Publicar recursos más tarde {#publish-to-bp-later}

Para programar la publicación de recursos en Brand Portal para una fecha u hora posterior:

1. Una vez que haya seleccionado los recursos o carpetas que desea publicar, seleccione **[!UICONTROL Administrar publicación]** en la barra de herramientas de la parte superior.

1. Activado **[!UICONTROL Administrar publicación]** página, seleccione **[!UICONTROL Publicar en Brand Portal]** from **[!UICONTROL Acción]** y seleccione **[!UICONTROL Más tarde]** from **[!UICONTROL Programación]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Seleccione una **[!UICONTROL Fecha de activación]** y especifique la hora. Haga clic en **[!UICONTROL Siguiente]**. 

1. Seleccione una **Fecha de activación** y especifique la hora. Haga clic en **Siguiente**. 

1. Especifique un **[!UICONTROL título de flujo de trabajo]** en **[!UICONTROL Flujos de trabajo]**. Haga clic en **[!UICONTROL Publicar más tarde]**.

   ![publishworkflow](assets/publishworkflow.png)

Ahora, inicie sesión en Brand Portal para ver si los recursos publicados están disponibles en la interfaz de Brand Portal.

![bp_landingpage](assets/bp_landingpage.png)
