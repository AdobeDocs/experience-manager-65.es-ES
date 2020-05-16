---
title: Creación y uso compartido de una carpeta privada en AEM
description: Obtenga información sobre cómo crear una carpeta privada en Recursos Adobe Experience Manager (AEM) y compartirla con otros usuarios, así como sobre cómo asignarles varios privilegios.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 979d5074fcf94ca999fd941c77038ab6305cc67d
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 5%

---


# Uso compartido de carpetas privadas {#private-folder-sharing}

Puede crear una carpeta privada en la interfaz de usuario Recursos Adobe Experience Manager (AEM) que esté disponible exclusivamente para usted. Puede compartir esta carpeta privada con otros usuarios y asignarles varios privilegios. Según el nivel de privilegios que asigne, los usuarios pueden realizar varias tareas en la carpeta, por ejemplo, vistas de recursos dentro de la carpeta o ediciones de los recursos.

>[!NOTE]
>
> La carpeta privada siempre tiene al menos un miembro con la función Propietario.


1. En la consola Recursos, toque o haga clic en **[!UICONTROL Crear]** en la barra de herramientas y, a continuación, elija **[!UICONTROL Carpeta]** en el menú.

   ![Crear carpeta de recursos](assets/Create-folder.png)

1. En el cuadro de diálogo **[!UICONTROL Crear carpeta]** , introduzca un título y un nombre (opcional) para la carpeta y seleccione **[!UICONTROL Privado]**.

   ![Active la casilla de verificación Privado para convertir la carpeta en privada](assets/private-folder.png)

1. Toque o haga clic en **[!UICONTROL Crear]**. Se crea una carpeta privada en la interfaz de usuario.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. Para compartir la carpeta con otros usuarios y asignarles privilegios, seleccione la carpeta y pulse o haga clic en el icono **[!UICONTROL Propiedades]** de la barra de herramientas.

   ![chlimage_1-414](assets/chlimage_1-414.png)

   >[!NOTE]
   >
   >La carpeta no estará visible para ningún otro usuario hasta que la comparta.

1. In the **[!UICONTROL Folder Properties]** page, select a user from the **[!UICONTROL Add User]** list, assign a role to the user on your private folder, and click **[!UICONTROL Add]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >Puede asignar varias funciones, como Editor, Propietario o Visor, al usuario con el que comparte la carpeta. Si asigna una función Propietario al usuario, este tiene privilegios de editor en la carpeta. Además, el usuario puede compartir la carpeta con otros usuarios. Si asigna una función de editor, el usuario puede editar los recursos de la carpeta privada. Si asigna una función de visor, el usuario solo puede vista los recursos de la carpeta privada.

   >[!NOTE]
   >
   > La carpeta privada siempre tiene al menos un miembro con la función Propietario. Por lo tanto, el administrador no puede quitar todos los miembros del propietario de una carpeta privada. Sin embargo, para eliminar los propietarios existentes del administrador de carpetas privadas, debe agregar otro usuario como propietario.

1. Haga clic en **[!UICONTROL Guardar.]** Según la función que asigne, al usuario se le asignará un conjunto de privilegios en su carpeta privada cuando inicie sesión en Recursos AEM.
1. Haga clic en **[!UICONTROL Aceptar]** para cerrar el mensaje de confirmación.
1. El usuario con el que comparte la carpeta recibe una notificación de uso compartido. Inicie sesión en Recursos AEM con las credenciales del usuario para la vista de la notificación.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Toque o haga clic en el icono Notificación para abrir la lista de las notificaciones.

   ![Lista de las notificaciones](assets/Assets-Notification.png)

1. Toque o haga clic en la entrada de la carpeta privada compartida por el administrador para abrir la carpeta.

>[!NOTE]
>
>Para poder crear una carpeta privada, necesita permisos de lectura y edición de ACL en la carpeta principal en la que desea crear una carpeta privada. Si no es administrador, estos permisos no se habilitan de forma predeterminada para usted en `/content/dam`. En este caso, obtenga primero estos permisos para su ID de usuario o grupo antes de intentar crear carpetas privadas o ajustes de carpeta de vista.
