---
title: Compartir recursos mediante un vínculo
description: Comparta recursos, carpetas y colecciones como URL.
contentOwner: AG
role: User
feature: Link Sharing,Asset Management
exl-id: 20370b00-862e-4d04-af2f-7d1c74a842dd
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 6%

---

# Compartir recursos como un vínculo {#asset-link-sharing}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/share-assets.html?lang=en) |
| AEM 6.5 | Este artículo |

[!DNL Adobe Experience Manager Assets] permite compartir recursos, carpetas y colecciones como URL con miembros de su organización y entidades externas, incluidos socios y proveedores. Compartir recursos a través de un vínculo es una forma cómoda de poner los recursos a disposición de terceros externos sin que tengan que iniciar sesión por primera vez en [!DNL Assets].

>[!PREREQUISITES]
>
>* Debe `Edit ACL` en la carpeta o el recurso que desea compartir como vínculo.
>* Para enviar correos electrónicos a los usuarios, configure los detalles del servidor SMTP en [Day CQ Mail Service](#configmailservice).


## Compartir recursos {#share-assets}

Para generar la dirección URL de los recursos que desea compartir con los usuarios, use el [!UICONTROL Uso compartido de vínculos] diálogo.

* Los usuarios con privilegios de administrador o con permisos de lectura en `/var/dam/share` puede ver los vínculos compartidos con ellos.
* Los usuarios que tienen permisos de lectura en `/var/dam/jobs/download` puede descargar recursos desde el vínculo compartido.

1. En el [!DNL Assets] interfaz de usuario, seleccione el recurso que desea compartir como vínculo.

1. En la barra de herramientas, haga clic en el **[!UICONTROL Compartir vínculo]** ![icono para compartir recursos](assets/do-not-localize/assets_share.png). El vínculo que se creará después de hacer clic en **[!UICONTROL Compartir]** se muestra de antemano en la variable [!UICONTROL Compartir vínculo] campo . El vínculo no se crea hasta que seleccione **[!UICONTROL Submit]**.

   ![Diálogo con el uso compartido de vínculos](assets/share-assets-as-link.png)

   *Figura: El cuadro de diálogo para compartir recursos como vínculo.*

1. En el apartado de la dirección de correo electrónico del cuadro de diálogo **[!UICONTROL Uso compartido de vínculos]**, escriba el ID de correo electrónico del usuario con el que desea compartir el vínculo. Puede agregar uno o más usuarios.

   >[!NOTE]
   >
   >Si introduce un ID de correo electrónico de un usuario que no es miembro de su organización, las palabras [!UICONTROL Usuario externo] llevan el prefijo email ID del usuario.

1. En el **[!UICONTROL Asunto]** , escriba un asunto para el recurso que desea compartir.

1. En el **[!UICONTROL Mensaje]** , escriba un mensaje opcional.

1. En el **[!UICONTROL Caducidad]** especifique una fecha y hora de caducidad para que el vínculo deje de funcionar. El tiempo de caducidad predeterminado del vínculo es de un día.

   ![Establecer fecha de caducidad del vínculo compartido](assets/Set-shared-link-expiration.png)

1. Para permitir a los usuarios descargar el recurso original, seleccione **[!UICONTROL Permitir descarga del archivo original]**. Para permitir a los usuarios descargar solo las representaciones de los recursos compartidos, seleccione **[!UICONTROL Permitir descarga de representaciones de archivos]**.

1. Haga clic en **[!UICONTROL Compartir]**. Un mensaje confirma que el vínculo se comparte con los usuarios por correo electrónico.

1. Para ver el recurso compartido, haga clic en el vínculo del correo electrónico que se envía al usuario. Para generar una vista previa del recurso, haga clic en el recurso compartido. Para cerrar la vista previa, haga clic en **[!UICONTROL Atrás]**. Si ha compartido una carpeta, haga clic en **[!UICONTROL Carpeta principal]** para volver a la carpeta principal.

   ![Vista previa del recurso compartido](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] permite generar la vista previa de recursos de solo [los tipos de archivo admitidos](/help/assets/assets-formats.md). Si se comparten otros tipos de MIME, solo se pueden descargar los recursos y no se puede obtener una vista previa.

1. Para descargar el recurso compartido, haga clic en **[!UICONTROL Select]** en la barra de herramientas, haga clic en el recurso y, a continuación, haga clic en **[!UICONTROL Descargar]** en la barra de herramientas.

   ![Opción de la barra de herramientas para descargar el recurso compartido](assets/chlimage_1-547.png)

1. Para ver los recursos que ha compartido como vínculos, vaya a la [!DNL Assets] interfaz de usuario de y haga clic en el botón [!DNL Experience Manager] logotipo. Choose **[!UICONTROL Navegación]**. En el panel Navegación, elija **[!UICONTROL Vínculos compartidos]** para mostrar una lista de recursos compartidos.

1. Para dejar de compartir un recurso, selecciónelo y haga clic en **[!UICONTROL Dejar de compartir]** en la barra de herramientas. A continuación se muestra un mensaje de confirmación. La entrada del recurso se elimina de la lista.

## Configurar el servicio de correo Day CQ {#configure-day-cq-mail-service}

1. En el [!DNL Experience Manager] página principal, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
1. En la lista de servicios, busque **[!UICONTROL Day CQ Mail Service]**.
1. Haga clic en **[!UICONTROL Editar]** al lado del servicio y configure los siguientes parámetros para **[!UICONTROL Day CQ Mail Service]** con los detalles mencionados en contra de sus nombres:

   * Nombre de host del servidor SMTP: nombre de host del servidor de correo electrónico
   * Puerto del servidor SMTP: puerto del servidor de correo electrónico
   * Usuario SMTP: nombre de usuario del servidor de correo electrónico
   * Contraseña SMTP: contraseña del servidor de correo electrónico

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Haga clic en **[!UICONTROL Guardar]**.

## Configurar el tamaño máximo de datos {#configure-maximum-data-size}

Cuando descarga recursos del vínculo compartido mediante la función Compartir vínculos , [!DNL Experience Manager] comprime la jerarquía de recursos del repositorio y, a continuación, devuelve el recurso en un archivo ZIP. Sin embargo, en ausencia de límites a la cantidad de datos que se pueden comprimir en un archivo ZIP, grandes cantidades de datos están sujetos a compresión, lo que causa errores de memoria en JVM. Para proteger el sistema de un posible ataque de denegación de servicio debido a esta situación, configure el tamaño máximo utilizando la variable **[!UICONTROL Tamaño máximo de contenido (sin comprimir)]** para **[!UICONTROL Servlet proxy Day CQ DAM Adhoc Asset Share]** en Configuration Manager. Si el tamaño sin comprimir del recurso supera el valor configurado, se rechazan las solicitudes de descarga de recursos. El valor predeterminado es 100 MB.

1. Haga clic en el [!DNL Experience Manager] y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
1. En la consola web, busque la **[!UICONTROL Servlet proxy Day CQ DAM Adhoc Asset Share]** configuración.
1. Abra la configuración del servlet proxy **[!UICONTROL Day CQ DAM Adhoc Asset Share]** en modo de edición y modifique el valor del parámetro **[!UICONTROL Tamaño de contenido máximo (sin comprimir)]**.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Guarde los cambios.

## Prácticas recomendadas y resolución de problemas {#best-practices-and-troubleshooting}

* Es posible que las carpetas de recursos o las colecciones que contienen un espacio en blanco en su nombre no se compartan.
* Si los usuarios no pueden descargar los recursos compartidos, consulte con su [!DNL Experience Manager] administrador: [límites de descarga](#configure-maximum-data-size) son.
* Si no puede enviar correos electrónicos con vínculos a recursos compartidos o si los demás usuarios no pueden recibir su correo electrónico, consulte a su [!DNL Experience Manager] administrador si el [servicio de correo electrónico](#configure-day-cq-mail-service) está configurado o no.
* Si no puede compartir recursos con la funcionalidad de uso compartido de vínculos, compruebe que dispone de los permisos adecuados. Consulte [compartir recursos](#share-assets).
* Si un recurso compartido se mueve a una ubicación diferente, su vínculo deja de funcionar. Vuelva a crear el vínculo y vuelva a compartirlo con los usuarios.

* Si desea compartir vínculos de su [!DNL Experience Manager] Implementación del autor en entidades externas, asegúrese de que solo muestra las siguientes direcciones URL que se usan para compartir vínculos, para `GET` solo solicitudes. Bloquear otras direcciones URL por motivos de seguridad.

   * `http://[aem_server]:[port]/linkshare.html`
   * `http://[aem_server]:[port]/linksharepreview.html`
   * `http://[aem_server]:[port]/linkexpired.html`
   En [!DNL Experience Manager] interfaz, acceso **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**. Abra el **[!UICONTROL Externalizador de vínculos de CQ de día]** y modifique las siguientes propiedades en la sección **[!UICONTROL Dominios]** con los valores mencionados en contra `local`, `author`y `publish`. Para la variable `local` y `author` proporcione la URL para las instancias local y Autor, respectivamente. Si ejecuta una sola [!DNL Experience Manager] Instancia de autor, utilice el mismo valor para `local` y `author` propiedades. En el caso de instancias de publicación, proporcione la URL de la variable [!DNL Experience Manager] Publicar instancia.
