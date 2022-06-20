---
title: Insertar y desproteger archivos [!DNL Assets]
description: Obtenga información sobre cómo extraer recursos para editarlos y volver a protegerlos una vez completados los cambios.
contentOwner: AG
role: User
feature: Asset Management
exl-id: 544ef73c-4e4b-433f-a173-fdf1c8f45d8e
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 2%

---

# Archivos de desprotección y registro en [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/check-out-and-submit-assets.html?lang=en) |
| AEM 6.5 | Este artículo |
| AEM 6.4 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/check-out-and-submit-assets.html?lang=en) |

[!DNL Adobe Experience Manager Assets] permite extraer recursos para editarlos y volver a protegerlos después de completar los cambios. Después de retirar un recurso, solo puede editarlo, anotarlo, publicarlo, moverlo o eliminarlo. Si se retira un recurso, este se bloquea. Otros usuarios no pueden realizar ninguna de estas operaciones en el recurso hasta que vuelva a proteger el recurso en [!DNL Assets]. Sin embargo, aún pueden cambiar los metadatos del recurso bloqueado.

Para poder extraer o incorporar recursos, debe disponer de acceso de escritura.

Esta función ayuda a evitar que otros usuarios anulen los cambios realizados por un autor en los que varios usuarios colaboran en la edición de flujos de trabajo entre equipos.

## Comprobar recursos {#checking-out-assets}

1. En el [!DNL Assets] interfaz de usuario de , seleccione el recurso que desee desproteger. También puede seleccionar varios recursos para desproteger.
1. En la barra de herramientas, haga clic en **[!UICONTROL Cierre de compra]**. La variable **[!UICONTROL Cierre de compra]** la opción cambia a **[!UICONTROL Proteger]**.
Para verificar si otros usuarios pueden editar el recurso que ha desprotegido, inicie sesión como un usuario diferente. Aparece un símbolo de bloqueo en la miniatura del recurso que ha extraído.

   ![chlimage_1-471](assets/chlimage_1-471.png)

   Seleccione el recurso. Observe que la barra de herramientas no muestra ninguna opción que le permita editar, anotar, publicar o eliminar el recurso.

   ![chlimage_1-472](assets/chlimage_1-472.png)

   Para editar los metadatos del recurso bloqueado, haga clic en **[!UICONTROL Ver propiedades]**.

1. Haga clic en **[!UICONTROL Editar]** para abrir el recurso en modo de edición.

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. Edite el recurso y guarde los cambios. Por ejemplo, recorte la imagen y guárdela.

   ![chlimage_1-474](assets/chlimage_1-474.png)

   También puede elegir anotar o publicar el recurso.

1. Seleccione el recurso editado en el [!DNL Assets] y haga clic en **[!UICONTROL Proteger]** en la barra de herramientas. El recurso modificado está registrado en [!DNL Assets] y está disponible para otros usuarios para su edición.

## Registro forzado {#forced-check-in}

Los administradores pueden proteger los recursos que han extraído otros usuarios.

1. Iniciar sesión en [!DNL Assets] como administrador.
1. En el [!DNL Assets] interfaz de usuario de seleccione uno o varios recursos que otros usuarios hayan extraído.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. En la barra de herramientas, haga clic en **[!UICONTROL Bloqueo de la versión]**. El recurso se vuelve a registrar y se puede editar para otros usuarios.

## Prácticas recomendadas y limitaciones {#tips-limitations}

* Es posible eliminar un *carpeta* que contiene archivos de recursos extraídos. Antes de eliminar una carpeta, asegúrese de que los usuarios no hayan extraído ningún recurso digital.

>[!MORELIKETHIS]
>
>* [Comprender la entrada y la salida [!DNL Experience Manager] aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [Tutorial de vídeo para comprender cómo registrar y registrar [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

