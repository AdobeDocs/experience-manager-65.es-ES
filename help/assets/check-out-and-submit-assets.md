---
title: Proteger y desproteger archivos en [!DNL Assets]
description: Obtenga información sobre cómo extraer recursos para editarlos y volver a protegerlos una vez completados los cambios.
contentOwner: AG
role: User
feature: Asset Management
exl-id: 544ef73c-4e4b-433f-a173-fdf1c8f45d8e
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 4%

---

# Archivos de protección y desprotección en [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/check-out-and-submit-assets.html?lang=en) |
| AEM 6.5 | Este artículo |

[!DNL Adobe Experience Manager Assets] le permite extraer recursos para editarlos y volver a registrarlos después de completar los cambios. Después de desproteger un recurso, solo puede editarlo, anotarlo, publicarlo, moverlo o eliminarlo. La extracción de un recurso bloquea el recurso. Otros usuarios no podrán realizar ninguna de estas operaciones en el recurso hasta que vuelva a registrarlo en [!DNL Assets]. Sin embargo, aún pueden cambiar los metadatos del recurso bloqueado.

Para poder desproteger o proteger recursos, se requiere acceso de escritura en ellos.

Esta función ayuda a evitar que otros usuarios anulen los cambios realizados por un autor en el que varios usuarios colaboran en la edición de flujos de trabajo entre equipos.

## Desproteger recursos {#checking-out-assets}

1. Desde el [!DNL Assets] interfaz de usuario, seleccione el recurso que desea extraer. También puede seleccionar varios recursos para extraerlos.
1. En la barra de herramientas, haga clic en **[!UICONTROL Finalizar compra]**. El **[!UICONTROL Finalizar compra]** la opción cambia a **[!UICONTROL Registrar]**.
Para comprobar si otros usuarios pueden editar el recurso que ha desprotegido, inicie sesión con otro usuario. Se muestra un símbolo de bloqueo en la miniatura del recurso que ha extraído.

   ![chlimage_1-471](assets/chlimage_1-471.png)

   Seleccione el recurso. Tenga en cuenta que la barra de herramientas no muestra ninguna opción que le permita editar, anotar, publicar o eliminar el recurso.

   ![chlimage_1-472](assets/chlimage_1-472.png)

   Para editar los metadatos del recurso bloqueado, haga clic en **[!UICONTROL Ver propiedades]**.

1. Clic **[!UICONTROL Editar]** para abrir el recurso en modo de edición.

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. Edite el recurso y guarde los cambios. Por ejemplo, recorte la imagen y guárdela.

   ![chlimage_1-474](assets/chlimage_1-474.png)

   También puede realizar anotaciones o publicar el recurso.

1. Seleccione el recurso editado del [!DNL Assets] y haga clic en **[!UICONTROL Registrar]** en la barra de herramientas. El recurso modificado está registrado en [!DNL Assets] y está disponible para que otros usuarios lo editen.

## Protección forzada {#forced-check-in}

Los administradores pueden proteger los recursos que han desprotegido otros usuarios.

1. Inicie sesión en [!DNL Assets] como administrador.
1. Desde el [!DNL Assets] interfaz de usuario seleccione uno o varios recursos que otros usuarios han extraído.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. En la barra de herramientas, haga clic en **[!UICONTROL Liberar bloqueo]**. El recurso se vuelve a registrar y está disponible para su edición por parte de otros usuarios.

## Prácticas recomendadas y limitaciones {#tips-limitations}

* Es posible eliminar un *carpeta* que contiene archivos de recursos desprotegidos. Antes de eliminar una carpeta, asegúrese de que los usuarios no desprotejan ningún recurso digital.

>[!MORELIKETHIS]
>
>* [Comprender el registro y la salida [!DNL Experience Manager] aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [Tutorial de vídeo para comprender el registro y el cierre de compra en [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

