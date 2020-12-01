---
title: Uso compartido de recursos mediante un vínculo
description: Comparta recursos, carpetas y colecciones como URL.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 1f6da1c69ea3b3c3f07e8ac10fd8e1e9c7208158
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 5%

---


# Compartir recursos mediante un vínculo {#asset-link-sharing}

[!DNL Adobe Experience Manager Assets] permite compartir recursos, carpetas y colecciones como URL con miembros de la organización y entidades externas, incluidos socios y proveedores. El uso compartido de recursos a través de un vínculo es una manera conveniente de poner los recursos a disposición de terceros externos sin que estos tengan que iniciar sesión en [!DNL Assets].

>[!PREREQUISITES]
>
>* Se requiere el permiso Editar ACL en la carpeta o el recurso que se desea compartir como vínculo.
>* Para enviar correos electrónicos a los usuarios, configure los detalles del servidor SMTP en [Día del servicio](#configmailservice)de correo de CQ.


## Compartir recursos {#sharelink}

Para generar la URL de los recursos que desea compartir con los usuarios, utilice el cuadro de diálogo Uso compartido de vínculos. Los usuarios con privilegios de administrador o con permisos de lectura en la `/var/dam/share` ubicación pueden realizar la vista de los vínculos compartidos con ellos.

1. En la interfaz de usuario, seleccione el recurso que desea compartir como vínculo. [!DNL Assets]
1. En la barra de herramientas, haga clic en el icono **** Compartir vínculo ![para](assets/do-not-localize/assets_share.png)compartir recursos.

   El vínculo que se creará después de hacer clic en [!UICONTROL Compartir] se muestra por adelantado en el campo [!UICONTROL Compartir vínculo] . El tiempo de caducidad predeterminado para el vínculo es un día.

   ![Cuadro de diálogo con el recurso compartido de vínculos](assets/Link-sharing-dialog-box.png)

   *Figura: Cuadro de diálogo para compartir recursos como vínculo.*

   >[!NOTE]
   >
   >Si desea compartir vínculos de la implementación de [!DNL Experience Manager] Autor con entidades externas, asegúrese de que solo muestra las siguientes URL (que se utilizan para compartir vínculos) para `GET` solicitudes. Bloquear otras direcciones URL por motivos de seguridad.
   >
   >* `http://[aem_server]:[port]/linkshare.html`
   >* `http://[aem_server]:[port]/linksharepreview.html`
   >* `http://[aem_server]:[port]/linkexpired.html`


1. En [!DNL Experience Manager] la interfaz, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > Consola **** web.

1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration and modify the following properties in the **[!UICONTROL Domains]** field with the values mentioned against `local`, `author`, and `publish`. Para las propiedades `local` y `author` , proporcione la URL para la instancia local y la instancia de autor respectivamente. Tanto `local` como `author` las propiedades tienen el mismo valor si se ejecuta una única instancia de [!DNL Experience Manager] autor. En el caso de instancias de Publish, especifique la URL de la instancia de [!DNL Experience Manager] publicación.

1. En el apartado de la dirección de correo electrónico del cuadro de diálogo **[!UICONTROL Uso compartido de vínculos]**, escriba el ID de correo electrónico del usuario con el que desea compartir el vínculo. Puede agregar uno o más usuarios.

   ![Uso compartido de vínculos a recursos directamente desde el cuadro de diálogo Uso compartido de vínculos](assets/Asset-Sharing-LinkShareDialog.png)

   *Figura: Comparta vínculos con recursos directamente desde el cuadro de diálogo Uso compartido de [!UICONTROL vínculos] .*

   >[!NOTE]
   >
   >Si introduce un ID de correo electrónico de un usuario que no es miembro de su organización, las palabras Usuario  externo llevan el prefijo ID de correo electrónico del usuario.

1. En el campo **[!UICONTROL Asunto]** , introduzca una línea de asunto.

1. En el campo **[!UICONTROL Mensaje]** , introduzca un mensaje opcional.

1. En el campo **[!UICONTROL Caducidad]** , especifique una fecha y hora de caducidad para que el vínculo deje de funcionar. De forma predeterminada, la fecha de caducidad se establece para una semana a partir de la fecha en que comparta el vínculo.

   ![Establecer fecha de caducidad del vínculo compartido](assets/Set-shared-link-expiration.png)

1. Para permitir que los usuarios descarguen el recurso original junto con las representaciones, seleccione **[!UICONTROL Permitir la descarga del archivo]** original. De forma predeterminada, los usuarios solo pueden descargar las representaciones del recurso que se comparten como vínculo.

1. Haga clic en **[!UICONTROL Compartir]**. Un mensaje confirma que el vínculo se comparte con los usuarios por correo electrónico.

1. Para vista del recurso compartido, haga clic en el vínculo del correo electrónico que se envía al usuario. El recurso compartido se muestra en la página de **[!UICONTROL Adobe Marketing Cloud]** .

   ![chlimage_1-260](assets/chlimage_1-545.png)

1. Para generar una previsualización del recurso, haga clic en el recurso compartido. To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click **[!UICONTROL Parent Folder]** to return to the parent folder.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] admite la generación de la previsualización de recursos solo de [los tipos](/help/assets/assets-formats.md)de archivo admitidos. Si se comparten otros tipos MIME, solo se pueden descargar los recursos y no se puede realizar la previsualización.

1. Para descargar el recurso compartido, haga clic en **[!UICONTROL Seleccionar]** en la barra de herramientas, haga clic en el recurso y, a continuación, haga clic en **[!UICONTROL Descargar]** desde la barra de herramientas.

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. Para vista de los recursos que ha compartido como vínculos, vaya a la interfaz de usuario y haga clic en el [!DNL Assets] logotipo [!DNL Experience Manager] . Seleccione **[!UICONTROL Navegación]**. In the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.

1. Para dejar de compartir un recurso, selecciónelo y haga clic en **[!UICONTROL Dejar de compartir]** en la barra de herramientas. A continuación se muestra un mensaje de confirmación. La entrada del recurso se elimina de la lista.

## Configurar el servicio de correo CQ Day {#configmailservice}

1. En la [!DNL Experience Manager] página de inicio, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > Consola **** web.
1. En la lista de servicios, localice **[!UICONTROL Day CQ Mail Service]**.
1. Click **[!UICONTROL Edit]** beside the service, and configure the following parameters for **[!UICONTROL Day CQ Mail Service]** with the details mentioned against their names:

   * Nombre de host del servidor SMTP: nombre de host del servidor de correo electrónico
   * Puerto del servidor SMTP: puerto del servidor de correo electrónico
   * Usuario SMTP: nombre de usuario del servidor de correo electrónico
   * Contraseña SMTP: contraseña del servidor de correo electrónico

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Haga clic en **[!UICONTROL Guardar]**.

## Configurar el tamaño máximo de datos {#maxdatasize}

Al descargar recursos desde el vínculo compartido mediante la función de uso compartido de vínculos, comprime la jerarquía de recursos desde el repositorio y, a continuación, devuelve el recurso en un archivo ZIP. [!DNL Experience Manager] Sin embargo, a falta de límites a la cantidad de datos que se pueden comprimir en un archivo ZIP, grandes cantidades de datos están sujetas a compresión, lo que causa errores de memoria insuficiente en JVM. Para proteger el sistema de un posible ataque de denegación de servicio debido a esta situación, configure el tamaño máximo usando el parámetro Tamaño de contenido **[!UICONTROL máximo (sin comprimir)]** para el servlet proxy [!UICONTROL Day CQ DAM Adhoc Asset Share] en Configuration Manager. Si el tamaño sin comprimir del recurso supera el valor configurado, se rechazan las solicitudes de descarga de recursos. El valor predeterminado es 100 MB.

1. Click the [!DNL Experience Manager] logo and then go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Desde la consola web, localice la configuración del servlet **[!UICONTROL proxy de uso compartido de recursos ad hoc CQ DAM]** Day.
1. Abra la configuración del servlet proxy **[!UICONTROL Day CQ DAM Adhoc Asset Share]** en modo de edición y modifique el valor del parámetro **[!UICONTROL Tamaño de contenido máximo (sin comprimir)]**.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Guarde los cambios.

## Best practices and troubleshooting {#bestpractices}

* Es posible que las carpetas de recursos o las colecciones que contengan un espacio en blanco en su nombre no se compartan.
* Si los usuarios no pueden descargar los recursos compartidos, compruebe con su [!DNL Experience Manager] administrador cuáles son los límites [de](#maxdatasize) descarga.
* Si no puede enviar correos electrónicos con vínculos a recursos compartidos o si los demás usuarios no pueden recibir su correo electrónico, consulte con su [!DNL Experience Manager] administrador si el servicio [de](#configmailservice) correo electrónico está configurado o no.
* Si no puede compartir recursos con la funcionalidad de uso compartido de vínculos, asegúrese de que dispone de los permisos adecuados. Consulte [Uso compartido de recursos](#sharelink).
* Si un recurso compartido se mueve a una ubicación diferente, su vínculo deja de funcionar. Vuelva a crear el vínculo y a compartirlo con los usuarios.
