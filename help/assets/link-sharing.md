---
title: Generación de una URL para los recursos compartidos
description: En este artículo se describe cómo compartir recursos, carpetas y colecciones dentro de Recursos AEM como una URL para terceros externos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 44daaa61f7328e79fd4e11a503b0eef3ff9ffb56

---


# Compartir recursos mediante un vínculo {#asset-link-sharing}

Recursos Adobe Experience Manager (AEM) le permite compartir recursos, carpetas y colecciones como URL con miembros de su organización y entidades externas, incluidos socios y proveedores. El uso compartido de recursos a través de un vínculo es una forma práctica de poner los recursos a disposición de terceros externos sin que estos tengan que iniciar sesión en Recursos AEM en primer lugar.

>[!NOTE]
>
>Se requiere el permiso Editar ACL en la carpeta o el recurso que se desea compartir como vínculo.

## Uso compartido de recursos {#sharelink}

Para generar la URL de los recursos que desea compartir con los usuarios, utilice el cuadro de diálogo Uso compartido de vínculos. Los usuarios con privilegios de administrador o con permisos de lectura en la `/var/dam/share` ubicación pueden ver los vínculos compartidos con ellos.

>[!NOTE]
>
>Antes de compartir un vínculo con los usuarios, asegúrese de que el servicio de correo de CQ de día está configurado. Se produce un error si intenta compartir un vínculo sin [configurar primero el servicio](/help/assets/link-sharing.md#configmailservice)de correo de Day CQ.

1. En la interfaz de usuario de Recursos, seleccione el recurso que desea compartir como vínculo.
1. En la barra de herramientas, toque o haga clic en **[!UICONTROL Compartir vínculo]** ![assets_share](assets/assets_share.png).

   Se crea automáticamente un vínculo de recurso en el campo **[!UICONTROL Compartir vínculo]** . Copie este vínculo y compártalo con los usuarios. El tiempo de caducidad predeterminado para el vínculo es un día.

   ![Cuadro de diálogo con el recurso compartido de vínculos](assets/Link-sharing-dialog-box.png)

   *Figura:Cuadro de diálogo con el recurso compartido de vínculos*

   Como alternativa, realice los pasos 3 a 7 de este procedimiento para agregar destinatarios de correo electrónico, configurar la caducidad del vínculo y enviarlo desde el cuadro de diálogo.

   >[!NOTE]
   >
   >Si desea compartir vínculos de la instancia de AEM Author con entidades externas, asegúrese de que solo muestra las siguientes URL (que se utilizan para compartir vínculos) para `GET` solicitudes. Bloquear otras direcciones URL para garantizar la seguridad de AEM Author.
   >
   >* http://&lt;aem_server>:&lt;puerto>/linkshare.html
   * http://&lt;aem_server>:&lt;puerto>/linksharepreview.html
   * http://&lt;aem_server>:&lt;puerto>/linkexpired.html


   >[!NOTE]
   Si un recurso compartido se mueve a una ubicación diferente, su vínculo deja de funcionar. Vuelva a crear el vínculo y a compartirlo con los usuarios.

1. Desde la consola web, abra la configuración **[!UICONTROL Day CQ Link Externalizer]** y modifique las siguientes propiedades en el campo **[!UICONTROL Dominios]** con los valores mencionados en relación con cada uno de ellos:

   * local
   * author
   * instancias de publicación
   Para las propiedades local y de autor, proporcione la URL para la instancia local y de autor respectivamente. Tanto las propiedades locales como las de autor tienen el mismo valor si se ejecuta una única instancia de autor de AEM. Para la publicación, especifique la URL de la instancia de publicación.

1. En el apartado de la dirección de correo electrónico del cuadro de diálogo **[!UICONTROL Uso compartido de vínculos]**, escriba el ID de correo electrónico del usuario con el que desea compartir el vínculo. También puede compartir el vínculo con varios usuarios.

   Si el usuario es miembro de su organización, seleccione el ID de correo electrónico del usuario en los ID de correo electrónico sugeridos que aparecen en la lista debajo del área de escritura. Para un usuario externo, escriba el ID de correo electrónico completo y selecciónelo en la lista.

   Para habilitar el envío de mensajes de correo electrónico a los usuarios, configure los detalles del servidor SMTP en [Día del servicio](#configmailservice)de correo de CQ.

   ![Uso compartido de vínculos a recursos directamente desde el cuadro de diálogo Uso compartido de vínculos](assets/Asset-Sharing-LinkShareDialog.png)

   Uso compartido de vínculos a recursos directamente desde el cuadro de diálogo Uso compartido de vínculos

   >[!NOTE]
   Si introduce un ID de correo electrónico de un usuario que no es miembro de su organización, las palabras &quot;Usuario externo&quot; llevan el prefijo &quot;ID de correo electrónico del usuario.

1. En el **[!UICONTROL cuadro Asunto]** , introduzca un asunto para el recurso que desea compartir.
1. En el cuadro **[!UICONTROL Mensaje]** , escriba un mensaje opcional.
1. En el campo **[!UICONTROL Caducidad]** , especifique una fecha y hora de caducidad para el vínculo mediante el selector de fechas. De forma predeterminada, la fecha de caducidad se establece para una semana a partir de la fecha en que comparta el vínculo.

   ![Establecer fecha de caducidad del vínculo compartido](assets/Set-shared-link-expiration.png)

1. Para permitir que los usuarios descarguen la imagen original junto con las representaciones, seleccione **[!UICONTROL Permitir la descarga del archivo]** original.

   >[!NOTE]
   De forma predeterminada, los usuarios solo pueden descargar las representaciones del recurso que se comparten como vínculo.

1. Haga clic en **[!UICONTROL Compartir]**. Un mensaje confirma que el vínculo se comparte con los usuarios a través de un correo electrónico.
1. Para ver el recurso compartido, toque o haga clic en el vínculo del correo electrónico que se envía al usuario. El recurso compartido se muestra en la página de **[!UICONTROL Adobe Marketing Cloud]** .

   ![chlimage_1-260](assets/chlimage_1-545.png)

   Para cambiar a la vista de lista, toque o haga clic en la opción de diseño en la barra de herramientas.

1. Para generar una vista previa del recurso, pulse o haga clic en el recurso compartido. Para cerrar la vista previa y volver a la página de **[!UICONTROL Experience Cloud]**, pulse o haga clic en **[!UICONTROL Atrás]** en la barra de herramientas. Si ha compartido una carpeta, pulse o haga clic en **[!UICONTROL Carpeta principal]** para regresar a la carpeta principal.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   AEM admite la generación de la vista previa de recursos de estos tipos MIME: JPG, PNG, GIF, BMP, INDD, PDF y PPT. Solo puede descargar los recursos de los otros tipos MIME.

1. Para descargar el recurso compartido, toque **[!UICONTROL Seleccionar]** en la barra de herramientas, toque o haga clic en el recurso y, a continuación, toque o haga clic en **[!UICONTROL Descargar]** desde la barra de herramientas.

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. Para ver los recursos que ha compartido como vínculos, vaya a la interfaz de usuario de Recursos y toque el logotipo de Experience Manager. Elija **[!UICONTROL Navegación]** en la lista para mostrar el panel Navegación.
1. En el panel Navegación, seleccione **[!UICONTROL Vínculos compartidos]** para mostrar una lista de recursos compartidos.
1. Para dejar de compartir un recurso, selecciónelo y toque o haga clic en **[!UICONTROL Dejar de compartir]** en la barra de herramientas. A continuación se muestra un mensaje de confirmación. La entrada del recurso se elimina de la lista.

## Configurar el servicio de correo CQ Day {#configmailservice}

1. En la página de inicio de Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > Consola **** web.
1. En la lista de servicios, busque **[!UICONTROL Day CQ Mail Service]**.
1. Tap **[!UICONTROL Edit]** beside the service, and configure the following parameters for **[!UICONTROL Day CQ Mail Service]** with the details mentioned against their names:

   * Nombre de host del servidor SMTP: nombre de host del servidor de correo electrónico
   * Puerto del servidor SMTP: puerto del servidor de correo electrónico
   * Usuario SMTP: nombre de usuario del servidor de correo electrónico
   * Contraseña SMTP: contraseña del servidor de correo electrónico
   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Click/tap **[!UICONTROL Save]**.

## Configurar el tamaño máximo de datos {#maxdatasize}

Al descargar recursos del vínculo compartido mediante la función de uso compartido de vínculos, AEM comprime la jerarquía de recursos del repositorio y, a continuación, devuelve el recurso en un archivo ZIP. Sin embargo, a falta de límites a la cantidad de datos que se pueden comprimir en un archivo ZIP, grandes cantidades de datos están sujetas a compresión, lo que causa errores de memoria insuficiente en JVM. Para proteger el sistema de un posible ataque de denegación de servicio debido a esta situación, configure el tamaño máximo usando el parámetro Tamaño de contenido **[!UICONTROL máximo (sin comprimir)]** para el servlet proxy [!UICONTROL Day CQ DAM Adhoc Asset Share] en Configuration Manager. Si el tamaño sin comprimir del recurso supera el valor configurado, se rechazan las solicitudes de descarga de recursos. El valor predeterminado es 100 MB.

1. Haga clic o pulse el logotipo de AEM y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
1. Desde la consola web, localice la configuración del servlet **[!UICONTROL proxy de uso compartido de recursos ad hoc CQ DAM]** Day.
1. Abra la configuración del servlet proxy **[!UICONTROL Day CQ DAM Adhoc Asset Share]** en modo de edición y modifique el valor del parámetro **[!UICONTROL Tamaño de contenido máximo (sin comprimir)]**.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Guarde los cambios.

## Best practices and troubleshooting {#bestpractices}

* Es posible que las carpetas de recursos o las colecciones que contengan un espacio en blanco en su nombre no se compartan.
* Si los usuarios no pueden descargar los recursos compartidos, compruebe con el administrador de AEM cuáles son los límites [de](#maxdatasize) descarga.
* Si no puede enviar correos electrónicos con vínculos a recursos compartidos o si los demás usuarios no pueden recibir su correo electrónico, consulte con el administrador de AEM si el servicio [de](#configmailservice) correo electrónico está configurado o no.
* Si no puede compartir recursos con la funcionalidad de uso compartido de vínculos, asegúrese de que dispone de los permisos adecuados. Consulte [Uso compartido de recursos](#sharelink).
