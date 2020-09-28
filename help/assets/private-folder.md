---
title: Carpetas privadas para compartir recursos
description: Obtenga información sobre cómo crear una carpeta privada en [!DNL Adobe Experience Manager Assets] su equipo y compartirla con otros usuarios y asignarles varios privilegios.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 0%

---


# Carpeta privada en [!DNL Adobe Experience Manager Assets] {#private-folder}

Puede crear una carpeta privada en la interfaz de [!DNL Adobe Experience Manager Assets] usuario que esté disponible exclusivamente para usted. Puede compartir esta carpeta privada con otros usuarios y asignarles varios privilegios. Según el nivel de privilegios que asigne, los usuarios pueden realizar varias tareas en la carpeta, por ejemplo, vistas de recursos dentro de la carpeta o ediciones de los recursos.

>[!NOTE]
>
>La carpeta privada tiene al menos un miembro con la función Propietario.

## Creación y uso compartido de carpetas privadas {#create-share-private-folder}

Para crear y compartir una carpeta privada:

1. En la [!DNL Assets] consola, haga clic en **[!UICONTROL Crear]** en la barra de herramientas y, a continuación, elija **[!UICONTROL Carpeta]** en el menú.

   ![Crear carpeta de recursos](assets/Create-folder.png)

1. En el cuadro de diálogo **[!UICONTROL Crear carpeta]** , introduzca un título y un nombre (opcional) para la carpeta y seleccione la opción **[!UICONTROL Privado]** .

1. Haga clic en **[!UICONTROL Crear]**. Se crea una carpeta privada.

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

1. Haga clic en **[!UICONTROL Guardar.]** Según la función que asigne, al usuario se le asignará un conjunto de privilegios en la carpeta privada cuando inicie sesión en [!DNL Assets].
1. Haga clic en **[!UICONTROL Aceptar]** para cerrar el mensaje de confirmación.
1. El usuario con el que comparte la carpeta recibe una notificación de uso compartido. Inicie sesión [!DNL Assets] con las credenciales del usuario para la vista de la notificación.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Haga clic en Notificaciones para abrir la lista de las notificaciones.

   ![Lista de las notificaciones](assets/Assets-Notification.png)

1. Haga clic en la entrada de la carpeta privada compartida por el administrador para abrir la carpeta.

>[!NOTE]
>
>Para crear una carpeta privada, necesita permisos [de lectura y modificación de](/help/sites-administering/security.md#permissions-in-aem) control de acceso en la carpeta principal en la que desea crear una carpeta privada. Si no es administrador, estos permisos no se habilitan de forma predeterminada para usted en `/content/dam`. En este caso, obtenga primero estos permisos para su ID de usuario o grupo antes de intentar crear carpetas privadas.

## Eliminación de carpetas privadas {#delete-private-folder}

Puede eliminar una carpeta seleccionando la carpeta y la opción [!UICONTROL Eliminar] del menú superior, o bien utilizando la tecla Retroceso del teclado.

![opción Eliminar en el menú superior](assets/delete-option.png)

>[!CAUTION]
>
>Si elimina una carpeta privada del CRXDE Lite, los grupos de usuarios redundantes se dejarán en el repositorio.

>[!NOTE]
>
>Si elimina una carpeta utilizando el método anterior de la interfaz de usuario, también se eliminarán los grupos de usuarios asociados.
Sin embargo, los grupos de usuarios redundantes, no utilizados y autogenerados existentes se pueden limpiar del repositorio mediante [JMX](#group-clean-up-jmx).

### Utilizar JMX para limpiar los grupos de usuarios no utilizados {#group-clean-up-jmx}

Para limpiar el repositorio de grupos de usuarios no utilizados:

1. Abra el JMX para limpiar los grupos redundantes para Recursos en la instancia de [!DNL Experience Manager] creación desde `http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`.
Por ejemplo, `http://no1010042068039.corp.adobe.com:4502/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`.

1. Invocar el `clean` método desde este JMX.

Puede ver que todos los grupos de usuarios redundantes o los grupos generados automáticamente (que se crean al crear una carpeta con el mismo nombre que un grupo eliminado anteriormente) se eliminan de la ruta `/home/groups/mac/default/<user_name>/<folder_name>`.
