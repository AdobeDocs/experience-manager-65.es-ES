---
title: Desproteger y desproteger recursos para editarlos
description: Obtenga información sobre cómo retirar recursos para editarlos y volver a protegerlos una vez completados los cambios.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# Archivos de ingreso y salida en [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

[!DNL Adobe Experience Manager Assets] permite retirar recursos para editarlos y volver a protegerlos una vez que haya realizado los cambios. Después de retirar un recurso, solo podrá editarlo, anotarlo, publicarlo, moverlo o eliminarlo. Al retirar un recurso, éste se bloquea. Otros usuarios no pueden realizar ninguna de estas operaciones en el recurso hasta que vuelva a activarlo en [!DNL Assets]. Sin embargo, aún pueden cambiar los metadatos del recurso bloqueado.

Para poder extraer o registrar recursos, necesita tener acceso de escritura en ellos.

Esta función ayuda a evitar que otros usuarios anulen los cambios realizados por un autor en los que varios usuarios colaboran en la edición de flujos de trabajo entre equipos.

## Comprobación de recursos {#checking-out-assets}

1. En la interfaz de usuario, seleccione el recurso que desee desproteger. [!DNL Assets] También puede seleccionar varios recursos para retirarlos.
1. En la barra de herramientas, haga clic en **[!UICONTROL Cierre de compra]**.
La opción **[!UICONTROL Cierre]** de compra cambia a **[!UICONTROL Proteger]**.
Para comprobar si otros usuarios pueden editar el recurso que ha extraído, inicie sesión como un usuario diferente. Aparece un símbolo de bloqueo en la miniatura del recurso que ha extraído.

   ![chlimage_1-471](assets/chlimage_1-471.png)

   Seleccione el recurso. Observe que la barra de herramientas no muestra ninguna opción que le permita editar, anotar, publicar o eliminar el recurso.

   ![chlimage_1-472](assets/chlimage_1-472.png)

   Puede hacer clic en Propiedades **[!UICONTROL de]** Vista para editar los metadatos del recurso bloqueado.

1. Haga clic en **[!UICONTROL Editar]** para abrir el recurso en modo de edición.

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. Edite el recurso y guarde los cambios. Por ejemplo, recorte la imagen y guárdela.

   ![chlimage_1-474](assets/chlimage_1-474.png)

   También puede elegir anotar o publicar el recurso.

1. Seleccione el recurso editado en la [!DNL Assets] interfaz y haga clic en **[!UICONTROL Proteger]** en la barra de herramientas. El recurso modificado está registrado en [!DNL Assets] y está disponible para su edición para otros usuarios.

## Registro forzado {#forced-check-in}

Los administradores pueden proteger recursos que otros usuarios han extraído.

1. Inicie sesión como [!DNL Assets] administrador.
1. En la interfaz de usuario, seleccione uno o varios recursos que hayan sido desprotegidos por otros usuarios. [!DNL Assets]

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. En la barra de herramientas, haga clic en **[!UICONTROL Soltar bloqueo]**. El recurso se vuelve a registrar y se puede editar para otros usuarios.

## Prácticas recomendadas y limitaciones {#tips-limitations}

* Es posible eliminar una *carpeta* que contenga archivos de recursos extraídos. Antes de eliminar una carpeta, asegúrese de que los usuarios no hayan extraído ningún recurso digital.

>[!MORELIKETHIS]
>
>* [Comprender la protección y desprotección en la aplicación de escritorio de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#how-app-works2)
>* [Tutorial de vídeo para comprender la protección y la protección en recursos](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

