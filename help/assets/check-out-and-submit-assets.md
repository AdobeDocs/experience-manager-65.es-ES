---
title: Proteja y desproteja los recursos digitales para editarlos
description: Obtenga información sobre cómo retirar recursos para editarlos y volver a protegerlos una vez completados los cambios.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 07c1a4102539ba4678c55dee3a4882101e39864f

---


# Archivos de ingreso y salida en AEM DAM {#check-in-and-check-out-files-in-assets}

Recursos Adobe Experience Manager (AEM) le permite retirar recursos para editarlos y volver a protegerlos después de realizar los cambios. Después de retirar un recurso, solo podrá editarlo, anotarlo, publicarlo, moverlo o eliminarlo. Al retirar un recurso, éste se bloquea. Otros usuarios no pueden realizar ninguna de estas operaciones en el recurso hasta que vuelva a activarlo en Recursos AEM. Sin embargo, aún pueden cambiar los metadatos del recurso bloqueado.

Para poder extraer o registrar recursos, necesita tener acceso de escritura en ellos.

Esta función ayuda a evitar que otros usuarios anulen los cambios realizados por un autor en los que varios usuarios colaboran en la edición de flujos de trabajo entre equipos.

## Comprobación de recursos {#checking-out-assets}

1. En la interfaz de usuario de Recursos, seleccione el recurso que desee desproteger. También puede seleccionar varios recursos para retirarlos.
1. En la barra de herramientas, toque o haga clic en **[!UICONTROL Cierre de compra]**.
La opción **[!UICONTROL Cierre]** de compra cambia a **[!UICONTROL Proteger]**.
Para comprobar si otros usuarios pueden editar el recurso que ha extraído, inicie sesión como un usuario diferente. Aparece un símbolo de bloqueo en la miniatura del recurso que ha extraído.

   ![chlimage_1-471](assets/chlimage_1-471.png)

   Seleccione el recurso. Observe que la barra de herramientas no muestra ninguna opción que le permita editar, anotar, publicar o eliminar el recurso.

   ![chlimage_1-472](assets/chlimage_1-472.png)

   Sin embargo, puede tocar **[!UICONTROL Ver propiedades]** para editar los metadatos del recurso bloqueado.

1. Toque **[!UICONTROL Editar]** para abrir el recurso en modo de edición.

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. Edite el recurso y guarde los cambios. Por ejemplo, recorte la imagen y guárdela.

   ![chlimage_1-474](assets/chlimage_1-474.png)

   También puede elegir anotar o publicar el recurso.

1. Seleccione el recurso editado en la interfaz de usuario de Recursos y toque **[!UICONTROL Proteger]** en la barra de herramientas. El recurso modificado está registrado en Recursos AEM y está disponible para su edición para otros usuarios.

## Registro forzado {#forced-check-in}

Los administradores pueden proteger recursos que otros usuarios han extraído.

1. Inicie sesión en Recursos AEM como administrador.
1. En la interfaz de usuario de Recursos, seleccione uno o varios recursos que hayan sido retirados por otros usuarios.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. En la barra de herramientas, toque **[!UICONTROL Soltar bloqueo]**. El recurso se vuelve a registrar y se puede editar para otros usuarios.

>[!MORELIKETHIS]
>
>* [Obtenga información sobre cómo registrarse y desprotegerse en la aplicación de escritorio de AEM](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [Tutorial de vídeo para comprender la protección y la protección en Recursos AEM](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/collaboration/checkin-checkout-technical-video-understand.html)

