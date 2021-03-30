---
title: Insertar y extraer archivos en [!DNL Assets]
description: Obtenga información sobre cómo extraer recursos para editarlos y volver a protegerlos una vez completados los cambios.
contentOwner: AG
role: Profesional empresarial
translation-type: tm+mt
source-git-commit: eb87d77e1366786e8574f84590dfe9a3303efda0
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---


# Archivos de desprotección y registro en [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

[!DNL Adobe Experience Manager Assets] permite extraer recursos para editarlos y volver a protegerlos después de completar los cambios. Después de retirar un recurso, solo puede editarlo, anotarlo, publicarlo, moverlo o eliminarlo. Si se retira un recurso, este se bloquea. Otros usuarios no pueden realizar ninguna de estas operaciones en el recurso hasta que vuelva a proteger el recurso en [!DNL Assets]. Sin embargo, aún pueden cambiar los metadatos del recurso bloqueado.

Para poder extraer o incorporar recursos, debe disponer de acceso de escritura.

Esta función ayuda a evitar que otros usuarios anulen los cambios realizados por un autor en los que varios usuarios colaboran en la edición de flujos de trabajo entre equipos.

## Consulte los recursos {#checking-out-assets}

1. En la interfaz de usuario [!DNL Assets], seleccione el recurso que desee extraer. También puede seleccionar varios recursos para desproteger.
1. En la barra de herramientas, haga clic en **[!UICONTROL Cierre de compra]**. La opción **[!UICONTROL Checkout]** cambia a **[!UICONTROL Checkin]**.
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

1. Seleccione el recurso editado en la interfaz [!DNL Assets] y haga clic en **[!UICONTROL Proteger]** en la barra de herramientas. El recurso modificado está registrado en [!DNL Assets] y está disponible para que lo editen otros usuarios.

## Registro forzado en {#forced-check-in}

Los administradores pueden proteger los recursos que han extraído otros usuarios.

1. Inicie sesión en [!DNL Assets] como administrador.
1. En la interfaz de usuario [!DNL Assets] seleccione uno o varios recursos que otros usuarios hayan extraído.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. En la barra de herramientas, haga clic en **[!UICONTROL Liberar bloqueo]**. El recurso se vuelve a registrar y se puede editar para otros usuarios.

## Prácticas recomendadas y limitaciones {#tips-limitations}

* Es posible eliminar una *carpeta* que contenga archivos de recursos extraídos. Antes de eliminar una carpeta, asegúrese de que los usuarios no hayan extraído ningún recurso digital.

>[!MORELIKETHIS]
>
>* [Comprender la entrada y la salida en la aplicación de  [!DNL Experience Manager] escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#how-app-works2)
>* [Tutorial de vídeo para comprender cómo registrar y registrar [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

