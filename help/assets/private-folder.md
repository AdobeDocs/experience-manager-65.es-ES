---
title: Carpetas privadas para compartir recursos
description: Obtenga información sobre cómo crear una carpeta privada en la [!DNL Adobe Experience Manager Assets] y compartirlo con otros usuarios y asignarles distintos privilegios.
contentOwner: AG
role: User
feature: Collaboration
exl-id: c1aece06-7c1c-43a0-bea0-6f11ecda7e68
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 2%

---

# Carpeta privada en [!DNL Adobe Experience Manager Assets] {#private-folder}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/private-folder.html?lang=en) |
| AEM 6.5 | Este artículo |
| AEM 6.4 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/private-folder.html?lang=en) |

Puede crear una carpeta privada en la [!DNL Adobe Experience Manager Assets] interfaz de usuario que está disponible exclusivamente para usted. Puede compartir esta carpeta privada con otros usuarios y asignarles varios privilegios. En función del nivel de privilegios que asigne, los usuarios pueden realizar varias tareas en la carpeta, como ver los recursos dentro de la carpeta o editar los recursos.

>[!NOTE]
>
>La carpeta privada tiene al menos un miembro con la función Propietario.

## Creación y uso compartido de carpetas privadas {#create-share-private-folder}

Para crear y compartir una carpeta privada:

1. En el [!DNL Assets] consola, haga clic en **[!UICONTROL Crear]** en la barra de herramientas y, a continuación, seleccione **[!UICONTROL Carpeta]** del menú .

   ![Crear carpeta de recursos](assets/Create-folder.png)

1. En el **[!UICONTROL Crear carpeta]** , introduzca un título y un nombre (opcional) para la carpeta y seleccione **[!UICONTROL Privado]** .

1. Haga clic en **[!UICONTROL Crear]**. Se crea una carpeta privada.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. Para compartir la carpeta con otros usuarios y asignarles privilegios, seleccione la carpeta y haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas.

   ![opción de información](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >Ningún otro usuario puede ver la carpeta hasta que la comparta.

1. En el **[!UICONTROL Propiedades de carpeta]** seleccione un usuario de la **[!UICONTROL Agregar usuario]** , asigne una función al usuario de la carpeta privada y haga clic en **[!UICONTROL Agregar]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >Puede asignar varias funciones, como `Editor`, `Owner`o `Viewer` al usuario con el que comparte la carpeta. Si asigna una `Owner` función para el usuario, el usuario tiene `Editor` privilegios en la carpeta . Además, el usuario puede compartir la carpeta con otros usuarios. Si asigna una `Editor` , el usuario puede editar los recursos de la carpeta privada. Si asigna una función de visor, el usuario solo puede ver los recursos de la carpeta privada.

   >[!NOTE]
   >
   >La carpeta privada tiene al menos un miembro con `Owner` función. Por lo tanto, el administrador no puede quitar todos los miembros propietarios de una carpeta privada. Sin embargo, para eliminar los propietarios existentes (y el administrador mismo) de la carpeta privada, el administrador debe agregar otro usuario como propietario.

1. Haga clic en **[!UICONTROL Guardar]**. Según la función que asigne, al usuario se le asignará un conjunto de privilegios en su carpeta privada cuando inicie sesión en [!DNL Assets].
1. Haga clic en **[!UICONTROL Ok]** para cerrar el mensaje de confirmación.
1. El usuario con el que comparte la carpeta recibe una notificación para compartir. Iniciar sesión en [!DNL Assets] con las credenciales del usuario para ver la notificación.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Haga clic en [!UICONTROL Notificaciones] para abrir una lista de notificaciones.

   ![Lista de notificaciones](assets/Assets-Notification.png)

1. Haga clic en la entrada de la carpeta privada compartida por el administrador para abrir la carpeta.

>[!NOTE]
>
>Para crear una carpeta privada, necesita Leer y Modificar [permisos de control de acceso](/help/sites-administering/security.md#permissions-in-aem) en la carpeta principal en la que desea crear una carpeta privada. Si no es administrador, estos permisos no están habilitados para usted de forma predeterminada en `/content/dam`. En este caso, obtenga primero estos permisos para su ID o grupo de usuarios antes de intentar crear carpetas privadas.

## Eliminación de carpeta privada {#delete-private-folder}

Puede eliminar una carpeta seleccionando la carpeta y [!UICONTROL Eliminar] en el menú superior o utilizando la tecla Retroceso en el teclado.

![opción eliminar del menú superior](assets/delete-option.png)

>[!CAUTION]
>
>Si elimina una carpeta privada del CRXDE Lite, los grupos de usuarios redundantes se dejarán en el repositorio.

>[!NOTE]
>
>Si elimina una carpeta utilizando el método anterior de la interfaz de usuario, también se eliminan los grupos de usuarios asociados.
>
>Sin embargo, los grupos de usuarios redundantes, no utilizados y autogenerados existentes se pueden eliminar del repositorio utilizando `clean` en JMX en la instancia de autor (`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).
