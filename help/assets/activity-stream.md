---
title: Flujo de actividad de recursos digitales en la vista de cronología
description: Este artículo describe cómo mostrar los registros de actividad de los recursos en la cronología.
contentOwner: AG
feature: Asset Management
role: User, Admin
exl-id: 28dc0aa5-f2be-4e27-b7d8-415569b7ecd4
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 12%

---

# Flujo de actividad en la cronología {#activity-stream-in-timeline}

Esta función muestra los registros de actividad de los recursos en la cronología. Si realiza cualquiera de las siguientes operaciones relacionadas con recursos en [!DNL Adobe Experience Manager Assets], la función flujo de actividad actualiza la cronología para reflejar la actividad.

Las siguientes operaciones se registran en el flujo de actividad:

* Crear
* Eliminar
* Descargar (incluidas representaciones)
* Publicación
* Cancelar publicación
* Aprobar
* Rechazar
* Mover

Los registros de actividad que se mostrarán en la cronología se recuperan de la ubicación `/var/audit/com.day.cq.dam/content/dam` en CRX, donde se almacenan los archivos de registro. Además, la actividad de la cronología se registra cuando se cargan nuevos recursos o cuando se modifican y se registran los recursos existentes [!DNL Experience Manager] mediante [Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) o [aplicación de escritorio de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

>[!NOTE]
>
>Los flujos de trabajo transitorios no se muestran en la cronología porque no se guarda información del historial para estos flujos de trabajo.

Para ver el flujo de actividad, realice una o varias de las operaciones en el recurso, selecciónelo y, a continuación, elija **[!UICONTROL Cronología]** de la lista GlobalNav.

![cronología-2](assets/timeline-2.png)

La cronología muestra el flujo de actividad para las operaciones que realiza en los recursos.

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>La ubicación de almacenamiento de registro predeterminada para las tareas **[!UICONTROL Publicar]** y **[!UICONTROL Cancelar la publicación]** es `/var/audit/com.day.cq.replication/content`. Para las tareas **[!UICONTROL Mover]**, la ubicación predeterminada es `/var/audit/com.day.cq.wcm.core.page`.
