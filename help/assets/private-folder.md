---
title: Cree y comparta una carpeta privada en Adobe Experience Manager.
description: Obtenga información sobre cómo crear una carpeta privada en Adobe Experience Manager Assets y compartirla con otros usuarios y asignarles varios privilegios.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 91caca39b0b6c5c0c98b58be02f518901a3d90e3
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---


# Uso compartido de carpetas privadas {#private-folder-sharing}

Puede crear una carpeta privada en la interfaz de usuario de Recursos Adobe Experience Manager que esté disponible exclusivamente para usted. Puede compartir esta carpeta privada con otros usuarios y asignarles varios privilegios. Según el nivel de privilegios que asigne, los usuarios pueden realizar varias tareas en la carpeta, por ejemplo, vistas de recursos dentro de la carpeta o ediciones de los recursos.

>[!NOTE]
>
>La carpeta privada tiene al menos un miembro con la función Propietario.

1. En la consola Recursos, haga clic en **[!UICONTROL Crear]** en la barra de herramientas y, a continuación, elija **[!UICONTROL Carpeta]** en el menú.

   ![Crear carpeta de recursos](assets/Create-folder.png)

1. En el cuadro de diálogo **[!UICONTROL Crear carpeta]** , introduzca un título y un nombre (opcional) para la carpeta y seleccione **[!UICONTROL Privado]**.

   ![Active la casilla de verificación Privado para convertir la carpeta en privada](assets/private-folder.png)

1. Haga clic en **[!UICONTROL Crear]**. Se crea una carpeta privada en la interfaz de usuario.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. To share the folder with other users and the assign privileges to them, select the folder, and click **[!UICONTROL Properties]** from the toolbar.

   ![opción de información](assets/do-not-localize/info-circle-icon.png)

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
   >La carpeta privada tiene al menos un miembro con la función Propietario. Por lo tanto, el administrador no puede quitar todos los miembros del propietario de una carpeta privada. Sin embargo, para eliminar los propietarios existentes (y el administrador mismo) de la carpeta privada, el administrador debe agregar otro usuario como propietario.

1. Haga clic en **[!UICONTROL Guardar.]** Según la función que asigne, al usuario se le asignará un conjunto de privilegios en la carpeta privada cuando inicie sesión en Assets.
1. Haga clic en **[!UICONTROL Aceptar]** para cerrar el mensaje de confirmación.
1. El usuario con el que comparte la carpeta recibe una notificación de uso compartido. Inicie sesión en Recursos con las credenciales del usuario para la vista de la notificación.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Haga clic en Notificaciones para abrir la lista de las notificaciones.

   ![Lista de las notificaciones](assets/Assets-Notification.png)

1. Haga clic en la entrada de la carpeta privada compartida por el administrador para abrir la carpeta.

>[!NOTE]
>
>Para poder crear una carpeta privada, necesita permisos de lectura y edición de ACL en la carpeta principal en la que desea crear una carpeta privada. Si no es administrador, estos permisos no se habilitan de forma predeterminada para usted en `/content/dam`. En este caso, obtenga primero estos permisos para su ID de usuario o grupo antes de intentar crear carpetas privadas o ajustes de carpeta de vista.
