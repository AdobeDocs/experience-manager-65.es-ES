---
title: Uso compartido de recursos mediante un vínculo
description: Comparta recursos, carpetas y colecciones como URL.
contentOwner: AG
translation-type: tm+mt
source-git-commit: e36d08c9ea89e840aecde79ffdd911372c0c54ee
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 5%

---


# Compartir recursos mediante un vínculo {#asset-link-sharing}

[!DNL Adobe Experience Manager Assets] permite compartir recursos, carpetas y colecciones como URL con miembros de la organización y entidades externas, incluidos socios y proveedores. El uso compartido de recursos a través de un vínculo es una manera conveniente de poner los recursos a disposición de terceros externos sin tener que iniciar sesión en [!DNL Assets].

>[!PREREQUISITES]
>
>* Se requiere el permiso Editar ACL en la carpeta o el recurso que se desea compartir como vínculo.
>* Para enviar correos electrónicos a los usuarios, configure los detalles del servidor SMTP en [Servicio de correo de CQ diario](#configmailservice).


## Compartir recursos {#sharelink}

Para generar la URL de los recursos que desea compartir con los usuarios, utilice el cuadro de diálogo Uso compartido de vínculos. Los usuarios con privilegios de administrador o con permisos de lectura en la ubicación `/var/dam/share` pueden realizar la vista de los vínculos compartidos con ellos.

1. En la interfaz de usuario [!DNL Assets], seleccione el recurso que desea compartir como vínculo.
1. En la barra de herramientas, haga clic en el icono **[!UICONTROL Compartir vínculo]** ![compartir recursos](assets/do-not-localize/assets_share.png).

   El vínculo que se creará después de hacer clic en [!UICONTROL Compartir] se muestra por adelantado en el campo [!UICONTROL Vínculo compartido]. El tiempo de caducidad predeterminado para el vínculo es un día.

   ![Cuadro de diálogo con el recurso compartido de vínculos](assets/Link-sharing-dialog-box.png)

   *Figura: Cuadro de diálogo para compartir recursos como vínculo.*

   >[!NOTE]
   >
   >Si desea compartir vínculos de la implementación [!DNL Experience Manager] del autor a entidades externas, asegúrese de que solo muestra las siguientes direcciones URL (que se utilizan para compartir vínculos) para solicitudes `GET`. Bloquear otras direcciones URL por motivos de seguridad.
   >
   >* `http://[aem_server]:[port]/linkshare.html`
   >* `http://[aem_server]:[port]/linksharepreview.html`
   >* `http://[aem_server]:[port]/linkexpired.html`


1. En la interfaz [!DNL Experience Manager], acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola Web]**.

1. Abra la configuración **[!UICONTROL Day CQ Link Externalizer]** y modifique las siguientes propiedades en el campo **[!UICONTROL Dominios]** con los valores mencionados en `local`, `author` y `publish`. Para las propiedades `local` y `author`, proporcione la dirección URL para la instancia local y de autor respectivamente. Tanto las propiedades `local` como `author` tienen el mismo valor si se ejecuta una única instancia de autor [!DNL Experience Manager]. En el caso de instancias de Publish, proporcione la URL para la instancia de publicación [!DNL Experience Manager].

1. En el apartado de la dirección de correo electrónico del cuadro de diálogo **[!UICONTROL Uso compartido de vínculos]**, escriba el ID de correo electrónico del usuario con el que desea compartir el vínculo. Puede agregar uno o más usuarios.

   ![Uso compartido de vínculos a recursos directamente desde el cuadro de diálogo Uso compartido de vínculos](assets/Asset-Sharing-LinkShareDialog.png)

   *Figura: Comparta vínculos con recursos directamente desde el cuadro de diálogo  [!UICONTROL Vincular ] uso compartido.*

   >[!NOTE]
   >
   >Si introduce un ID de correo electrónico de un usuario que no es miembro de su organización, las palabras [!UICONTROL Usuario externo] llevan el prefijo del ID de correo electrónico del usuario.

1. En el cuadro **[!UICONTROL Asunto]**, introduzca un asunto para el recurso que desea compartir.

1. En el cuadro **[!UICONTROL Mensaje]**, escriba un mensaje opcional.

1. En el campo **[!UICONTROL Caducidad]**, especifique una fecha y hora de caducidad para que el vínculo deje de funcionar. De forma predeterminada, la fecha de caducidad se establece para una semana a partir de la fecha en que comparta el vínculo.

   ![Establecer fecha de caducidad del vínculo compartido](assets/Set-shared-link-expiration.png)

1. Para permitir que los usuarios descarguen el recurso original junto con las representaciones, seleccione **[!UICONTROL Permitir la descarga del archivo original]**. De forma predeterminada, los usuarios solo pueden descargar las representaciones del recurso que se comparten como vínculo.

1. Haga clic en **[!UICONTROL Compartir]**. Un mensaje confirma que el vínculo se comparte con los usuarios por correo electrónico.

1. Para vista del recurso compartido, haga clic en el vínculo del correo electrónico que se envía al usuario. El recurso compartido se muestra en la página [!UICONTROL Adobe Marketing Cloud].

   ![Los recursos compartidos están disponibles en Adobe Marketing Cloud](assets/chlimage_1-545.png)

1. Para generar una previsualización del recurso, haga clic en el recurso compartido. Para cerrar la previsualización y volver a la página **[!UICONTROL Marketing Cloud]**, haga clic en **[!UICONTROL Atrás]** en la barra de herramientas. Si ha compartido una carpeta, haga clic en **[!UICONTROL Carpeta principal]** para volver a la carpeta principal.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] admite la generación de la previsualización de recursos solo de  [los tipos](/help/assets/assets-formats.md) de archivo admitidos. Si se comparten otros tipos MIME, solo se pueden descargar los recursos y no se puede realizar la previsualización.

1. Para descargar el recurso compartido, haga clic en **[!UICONTROL Seleccionar]** en la barra de herramientas, haga clic en el recurso y, a continuación, haga clic en **[!UICONTROL Descargar]** en la barra de herramientas.

   ![Opción de barra de herramientas para descargar el recurso compartido](assets/chlimage_1-547.png)

1. Para vista de los recursos que ha compartido como vínculos, vaya a la interfaz de usuario [!DNL Assets] y haga clic en el logotipo [!DNL Experience Manager]. Elija **[!UICONTROL Navegación]**. En el panel Navegación, elija **[!UICONTROL Vínculos compartidos]** para mostrar una lista de recursos compartidos.

1. Para dejar de compartir un recurso, selecciónelo y haga clic en **[!UICONTROL Dejar de compartir]** en la barra de herramientas. A continuación se muestra un mensaje de confirmación. La entrada del recurso se elimina de la lista.

## Configurar el servicio de correo de CQ de día {#configmailservice}

1. En la página de inicio [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola Web]**.
1. En la lista de servicios, localice **[!UICONTROL Day CQ Mail Service]**.
1. Haga clic en **[!UICONTROL Editar]** al lado del servicio y configure los siguientes parámetros para **[!UICONTROL Day CQ Mail Service]** con los detalles mencionados en sus nombres:

   * Nombre de host del servidor SMTP: nombre de host del servidor de correo electrónico
   * Puerto del servidor SMTP: puerto del servidor de correo electrónico
   * Usuario SMTP: nombre de usuario del servidor de correo electrónico
   * Contraseña SMTP: contraseña del servidor de correo electrónico

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Haga clic en **[!UICONTROL Guardar]**.

## Configurar el tamaño máximo de datos {#maxdatasize}

Al descargar recursos del vínculo compartido mediante la función de uso compartido de vínculos, [!DNL Experience Manager] comprime la jerarquía de recursos del repositorio y, a continuación, devuelve el recurso en un archivo ZIP. Sin embargo, a falta de límites a la cantidad de datos que se pueden comprimir en un archivo ZIP, grandes cantidades de datos están sujetas a compresión, lo que causa errores de memoria insuficiente en JVM. Para proteger el sistema de un posible ataque de denegación de servicio debido a esta situación, configure el tamaño máximo usando el parámetro **[!UICONTROL Tamaño máximo de contenido (sin comprimir)]** para [!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet] en Configuration Manager. Si el tamaño sin comprimir del recurso supera el valor configurado, se rechazan las solicitudes de descarga de recursos. El valor predeterminado es 100 MB.

1. Haga clic en el logotipo [!DNL Experience Manager] y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola Web]**.
1. Desde la consola web, localice la configuración **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**.
1. Abra la configuración del servlet proxy **[!UICONTROL Day CQ DAM Adhoc Asset Share]** en modo de edición y modifique el valor del parámetro **[!UICONTROL Tamaño de contenido máximo (sin comprimir)]**.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Guarde los cambios.

## Prácticas recomendadas y solución de problemas {#bestpractices}

* Es posible que las carpetas de recursos o las colecciones que contengan un espacio en blanco en su nombre no se compartan.
* Si los usuarios no pueden descargar los recursos compartidos, consulte con el administrador [!DNL Experience Manager] cuáles son los [límites de descarga](#maxdatasize).
* Si no puede enviar correos electrónicos con vínculos a recursos compartidos o si los demás usuarios no pueden recibir su correo electrónico, consulte con su [!DNL Experience Manager] administrador si el [servicio de correo electrónico](#configmailservice) está configurado o no.
* Si no puede compartir recursos con la funcionalidad de uso compartido de vínculos, asegúrese de que dispone de los permisos adecuados. Consulte [recursos compartidos](#sharelink).
* Si un recurso compartido se mueve a una ubicación diferente, su vínculo deja de funcionar. Vuelva a crear el vínculo y a compartirlo con los usuarios.
