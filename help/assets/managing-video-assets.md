---
title: Administrar recursos de vídeo
description: Cargar, previsualizar, anotar y publicar recursos de vídeo en [!DNL Adobe Experience Manager].
contentOwner: AG
role: User
feature: Asset Management
exl-id: 21d3e0bd-5955-470a-8ca2-4d995c17eb4c
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '5499'
ht-degree: 8%

---

# Administrar recursos de vídeo {#manage-video-assets}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-video-assets.html?lang=en) |
| AEM 6.5 | Este artículo |

El formato de vídeo es una parte fundamental de los recursos digitales de una organización. [!DNL Adobe Experience Manager] ofrece ofertas y funciones maduras para administrar todo el ciclo de vida de los recursos de vídeo tras su creación.

Obtenga información sobre cómo administrar y editar los recursos de vídeo en [!DNL Adobe Experience Manager Assets]. La codificación y transcodificación de vídeo, por ejemplo, la transcodificación FFmpeg, es posible mediante [!DNL Dynamic Media] integración.

## Cargar y previsualizar recursos de vídeo {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] genera vistas previas para recursos de vídeo con la extensión MP4. Si el formato del recurso no es MP4, instale el paquete FFmpeg para generar una vista previa. FFmpeg crea representaciones de vídeo de tipo OGG y MP4. Puede obtener una vista previa de las representaciones en la [!DNL Assets] interfaz de usuario.

1. En la carpeta o subcarpetas de recursos digitales, vaya a la ubicación en la que desee agregar recursos digitales.
1. Para cargar el recurso, haga clic en **[!UICONTROL Crear]** en la barra de herramientas y seleccione **[!UICONTROL Archivos]**. También puede arrastrar un archivo en la interfaz de usuario. Consulte [cargar recursos](manage-assets.md#uploading-assets) para obtener más información.
1. Para obtener una vista previa de un vídeo en la vista de tarjeta, haga clic en el botón **[!UICONTROL Play]** ![opción play](assets/do-not-localize/play.png) en el recurso de vídeo. Puede pausar o reproducir vídeo solo en la vista de tarjeta. La variable [!UICONTROL Play] y [!UICONTROL Pausa] no están disponibles en la vista de lista.

1. Para obtener una vista previa del vídeo en la página de detalles del recurso, haga clic en **[!UICONTROL Editar]** en la tarjeta. El vídeo se reproduce en el reproductor de vídeo nativo del explorador. Puede reproducir, pausar, controlar el volumen y hacer zoom en el vídeo hasta la pantalla completa.

   ![Controles de reproducción de vídeo](assets/video-playback-controls.png)

## Configuración para cargar recursos de más de 2 GB {#configuration-to-upload-assets-that-are-larger-than-gb}

De forma predeterminada, [!DNL Assets] no permite cargar ningún recurso que supere los 2 GB debido a un límite de tamaño de archivo. Sin embargo, puede sobrescribir este límite entrando en CRXDE Lite y creando un nodo en el `/apps` directorio. El nodo debe tener el mismo nombre de nodo, estructura de directorio y propiedades de nodo comparables de order.

Además de [!DNL Assets] cambie las siguientes configuraciones para cargar recursos de gran tamaño:

* Aumente el tiempo de caducidad del token. Consulte [!UICONTROL Servlet Adobe Granite CSRF] en la consola web en `https://[aem_server]:[port]/system/console/configMgr`. Para obtener más información, consulte [Protección CSRF](/help/sites-developing/csrf-protection.md).
* Aumente el `receiveTimeout` en la configuración de Dispatcher. Para obtener más información, consulte [Configuración de Dispatcher de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options).

>[!NOTE]
>
>La variable [!DNL Experience Manager] La interfaz de usuario clásica no tiene una restricción de tamaño de archivo de 2 GB. Además, el flujo de trabajo completo para vídeo de gran tamaño no es totalmente compatible.

Para configurar un límite de tamaño de archivo más alto, realice los pasos siguientes en la sección `/apps` directorio.

1. En [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. En el CRXDE Lite, vaya a `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. Para ver la ventana del directorio, haga clic en el botón `>>`.
1. En la barra de herramientas, haga clic en el **[!UICONTROL Nodo de superposición]**. También puede seleccionar **[!UICONTROL Nodo de superposición]** en el menú contextual.
1. En el **[!UICONTROL Nodo de superposición]** cuadro de diálogo, haga clic en **[!UICONTROL OK]**.

   ![Nodo de superposición](assets/overlay-node-path.png)

1. Actualice el explorador. El nodo de superposición `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` está seleccionado.
1. En el **[!UICONTROL Propiedades]** , introduzca el valor apropiado en bytes para aumentar el límite de tamaño al tamaño deseado. Por ejemplo, para aumentar el límite de tamaño a 30 GB, introduzca `32212254720` valor.

1. En la barra de herramientas, haga clic en **[!UICONTROL Guardar todo]**.
1. En [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
1. En el [!DNL Adobe Experience Manager] [!UICONTROL Paquetes de la consola web] , en la columna Nombre de la tabla, busque y haga clic en **[!UICONTROL Controlador de trabajos de proceso externo de flujo de trabajo de Granite de Adobe]**.
1. En el [!UICONTROL Controlador de trabajos de proceso externo de flujo de trabajo de Granite de Adobe] , establezca los segundos para ambas **[!UICONTROL Tiempo de espera predeterminado]** y **[!UICONTROL Tiempo de espera máximo]** campos a `18000` (cinco horas). Haga clic en **[!UICONTROL Guardar]**.
1. En [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página Modelos de flujo de trabajo , seleccione **[!UICONTROL Codificar vídeo de Dynamic Media]** y haga clic en **[!UICONTROL Editar]**.
1. En la página de flujo de trabajo, haga doble clic en el botón **[!UICONTROL Proceso del servicio de vídeo de Dynamic Media]** componente.
1. En el cuadro de diálogo [!UICONTROL Propiedades del paso], en la pestaña **[!UICONTROL Común]**, expanda **Configuración avanzada**.
1. En el **[!UICONTROL Tiempo de espera]** , especifique un valor de `18000`y haga clic en **[!UICONTROL OK]** para volver a la **[!UICONTROL Codificar vídeo de Dynamic Media]** página de flujo de trabajo.
1. Cerca de la parte superior de la página, debajo de la variable [!UICONTROL Codificar vídeo de Dynamic Media] título de página, haga clic en **[!UICONTROL Guardar]**.

## Publicar recursos de vídeo {#publish-video-assets}

Después de la publicación, puede incluir los recursos de vídeo en una página web como URL o incrustar directamente los recursos. Para obtener más información, consulte [publicar recursos de Dynamic Media](/help/assets/publishing-dynamicmedia-assets.md).

## Publicar vídeos en YouTube {#publishing-videos-to-youtube}

Puede publicar recursos de vídeo del Experience Manager local directamente en un canal de YouTube que haya creado anteriormente.

Para publicar recursos de vídeo en YouTube, configure Experience Manager Assets con etiquetas. Estas etiquetas se asocian a un canal de YouTube. Si la etiqueta de un recurso de vídeo coincide con la etiqueta de un canal de YouTube, el vídeo se publica en YouTube. La publicación en YouTube se produce junto con una publicación normal del vídeo, siempre que se utilice una etiqueta asociada.

YouTube hace su propia codificación. De este modo, el archivo de vídeo original que se cargó en Experience Manager se publica en YouTube en lugar de en cualquier representación de vídeo que haya creado la codificación de Dynamic Media. Aunque no es necesario procesar vídeos con Dynamic Media, se espera que lo hagan en caso de que se necesite un ajuste preestablecido de visualizador para la reproducción.

Al omitir el perfil de procesamiento de vídeo y publicar directamente en YouTube, solo significa que el recurso de vídeo en Experience Manager Asset no obtiene una miniatura visible. También significa que si se ejecuta en `dynamicmedia` o `dynamicmedia_scene7` los modos de ejecución, los vídeos que no están codificados, no funcionan con ninguno de los tipos de recursos de Dynamic Media.

La publicación de recursos de vídeo en servidores de YouTube implica completar las siguientes tareas para garantizar una autenticación segura de servidor a servidor con YouTube:

1. [Configuración de la nube de Google](#configuring-google-cloud-settings)
1. [Creación de un canal de YouTube](#creating-a-youtube-channel)
1. [Agregar etiquetas para su publicación](#adding-tags-for-publishing)
1. [Habilitar el agente de replicación de YouTube Publish](#enabling-the-youtube-publish-replication-agent)
1. [Configuración de YouTube en Experience Manager](#setting-up-youtube-in-aem)
1. [(Opcional) Automatice la configuración de las propiedades predeterminadas de YouTube para los vídeos cargados](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [Publicación de vídeos en el canal de YouTube](#publishing-videos-to-your-youtube-channel)
1. [(Opcional) Verifique el vídeo publicado en YouTube](/help/assets/video.md#optional-verifying-the-published-video-on-youtube)
1. [Vincule las URL de YouTube a su aplicación web](#linking-youtube-urls-to-your-web-application)

También puede [cancelar la publicación de vídeos para eliminarlos de YouTube](#unpublishing-videos-to-remove-them-from-youtube).

### Configuración de la nube de Google {#configuring-google-cloud-settings}

Para publicar en YouTube, necesita una cuenta de Google. Si tiene una cuenta de GMAIL, ya tiene una cuenta de Google; si no tiene una cuenta de Google, puede crearla fácilmente. Necesita la cuenta porque necesita credenciales para publicar recursos de vídeo en YouTube. Si ya ha creado una cuenta, omita esta tarea y continúe directamente a [Creación de un canal de YouTube](#creating-a-youtube-channel).

La cuenta utilizada con Google Cloud y la cuenta de Google utilizada para YouTube no tienen por qué ser la misma.

Google cambia periódicamente su interfaz de usuario. De este modo, los pasos para publicar vídeos en YouTube pueden variar ligeramente con respecto a lo que se documenta a continuación. Esta advertencia también se aplica a YouTube cuando intenta comprobar si los vídeos se han cargado en él.

>[!NOTE]
>
>Los siguientes pasos eran precisos en el momento de escribir este artículo. Sin embargo, Google actualiza periódicamente sus sitios web sin previo aviso. Como tal, estos pasos pueden ser ligeramente diferentes.

Para configurar la configuración de Google Cloud:

1. Cree una cuenta de Google.
   [https://accounts.google.com/SignUp?service=mail](https://accounts.google.com/SignUp?service=mail)

   Si ya tiene una cuenta de Google, vaya al paso siguiente.

1. Vaya a [https://cloud.google.com/](https://cloud.google.com/).
1. En la página de Google Cloud, cerca de la esquina superior derecha, haga clic en **[!UICONTROL Consola]**.

   Si es necesario, **[!UICONTROL Iniciar sesión]** uso de las credenciales de la cuenta de Google para ver la variable **[!UICONTROL Consola]** .

1. En la página Tablero , a la derecha de **[!UICONTROL Google Cloud Platform]**, haga clic en la lista desplegable Proyecto para abrir el cuadro de diálogo Seleccionar un proyecto .
1. En el cuadro de diálogo Seleccionar un proyecto, pulse **[!UICONTROL Nuevo proyecto]**.

   ![6_5_googleaccount-newproject](assets/6_5_googleaccount-newproject.png)

1. En el cuadro de diálogo Nuevo proyecto, en el campo Nombre del proyecto , escriba el nombre del nuevo proyecto.

   El ID del proyecto se basa en el nombre del proyecto. Como tal, elija cuidadosamente el nombre del proyecto; no se puede cambiar una vez creada. Además, debe volver a introducir el mismo ID de proyecto cuando configure YouTube en Experience Manager más adelante; considero anotarlo.

1. Haga clic en **[!UICONTROL Crear]**.

1. Realice una de las siguientes acciones:

   * En el panel del proyecto, en la tarjeta Introducción , pulse **[!UICONTROL Explorar y habilitar API]**.
   * En el panel del proyecto, en la tarjeta API, pulse **[!UICONTROL Información general sobre las API]**.

   ![6_5_googleaccount-apis-enable2](assets/6_5_googleaccount-apis-enable2.png)

1. Cerca de la parte superior de la página API y servicios, pulse **[!UICONTROL Habilitar API y servicios]**.
1. En la página Biblioteca de API, a la izquierda, debajo de **[!UICONTROL Categoría]**, toque **[!UICONTROL YouTube]**. En el lado derecho de la página, pulse **[!UICONTROL API de datos de YouTube]**.
1. En la página API de datos de YouTube v3 , pulse **[!UICONTROL Habilitar]**.

   ![6_5_googleaccount-apis-enable3](assets/6_5_googleaccount-apis-enable3.png)

1. Para utilizar la API, necesita credenciales. Si es necesario, haga clic en **[!UICONTROL Crear credenciales]**.

   ![6_5_googleaccount-apis-createcredentials](assets/6_5_googleaccount-apis-createcredentials.png)

1. En el **[!UICONTROL Agregar credenciales al proyecto]** página, paso 1, haga lo siguiente:

   * En el **[!UICONTROL ¿Qué API utiliza?]** lista desplegable, seleccione **[!UICONTROL API de datos de YouTube v3]**.

   * En el **[!UICONTROL ¿Desde dónde llama a la API?]** lista desplegable, seleccione **[!UICONTROL Servidor web (por ejemplo, node.js, Tomcat)]**

   * En el **[!UICONTROL ¿A qué datos accede?]** lista desplegable, toque **[!UICONTROL Datos de usuario]**.

   ![6_5_googleaccount-apis-createcredentials2](assets/6_5_googleaccount-apis-createcredentials2.png)

1. Toque **[!UICONTROL ¿Qué credenciales necesito?]**
1. En la página **[!UICONTROL Agregar credenciales al proyecto]**, paso 2, en el encabezado **[!UICONTROL Crear un ID de cliente de OAuth 2.0]**, introduzca un nombre único (si lo desea) en el campo Nombre. También puede utilizar el nombre predeterminado especificado por Google.
1. En el **[!UICONTROL Orígenes de JavaScript autorizados]** , en el campo de texto, introduzca la siguiente ruta, sustituyendo su propio dominio y número de puerto en la ruta y, a continuación, pulse **[!UICONTROL Entrar]** para agregar la ruta a la lista:

   `https://<servername.domain>:<port_number>`

   Por ejemplo, `https://1a2b3c.mycompany.com:4321`. 

   **Nota**: El ejemplo de ruta anterior está diseñado únicamente para fines de demostración.

   ![6_5_googleaccount-apis-createcredentials-oauth](assets/6_5_googleaccount-apis-createcredentials-oauth.png)

1. En el **[!UICONTROL URI de redireccionamiento autorizado]** , en el campo de texto, introduzca la siguiente ruta, sustituyendo su propio dominio y número de puerto en la ruta y, a continuación, pulse **[!UICONTROL Entrar]** para agregar la ruta a la lista:

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   Por ejemplo, `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`. 

   **Nota**: El ejemplo de ruta anterior está diseñado únicamente para fines de demostración.

1. Haga clic en **[!UICONTROL Crear ID de cliente de OAuth]**.
1. En la página **[!UICONTROL Agregar credenciales a su proyecto]**, paso 3, en el encabezado **[!UICONTROL Configurar la pantalla de consentimiento de OAuth 2.0]**, seleccione la dirección de correo electrónico de Gmail que está utilizando actualmente.

   ![6_5_googleaccount-apis-createcredentials-consentscreen](assets/6_5_googleaccount-apis-createcredentials-consentscreen.png)

1. En el **[!UICONTROL Nombre del producto que se muestra a los usuarios]** , en el campo de texto, introduzca lo que desee mostrar en la pantalla de consentimiento.

   La pantalla de consentimiento se muestra al administrador del Experience Manager cuando se autentica en YouTube; El Experience Manager se pone en contacto con YouTube para obtener permiso.

1. Haga clic en **[!UICONTROL Continuar]**.
1. En la página Agregar credenciales a su proyecto, paso 4, bajo el encabezado **[!UICONTROL Descargar credenciales]**, pulse **[!UICONTROL Descargar]**.

   ![6_5_googleaccount-apis-createcredentials-downloadcredentials](assets/6_5_googleaccount-apis-createcredentials-downloadcredentials.png)

1. Guarde el `client_id.json` archivo.

   Necesita este archivo json descargado cuando configure YouTube en Adobe Experience Manager más adelante.

1. Haga clic en **[!UICONTROL Listo]**.

   Cierre la sesión de su cuenta de Google. Ahora cree un canal de YouTube.

### Creación de un canal de YouTube {#creating-a-youtube-channel}

La publicación de vídeos en YouTube requiere que tenga uno o más canales. Si ya ha creado un canal de YouTube, puede omitir esta tarea y ir a [Agregar etiquetas para su publicación](/help/assets/video.md#adding-tags-for-publishing).

>[!WARNING]
>
>Asegúrese de que ya ha configurado uno o varios canales en YouTube *before* los canales se agregan en Configuración de YouTube en Experience Manager (consulte [Configuración de YouTube en Experience Manager](#setting-up-youtube-in-aem) más abajo). Si no puede configurar uno o más canales, no se le avisará de que no existen canales. Sin embargo, la autenticación de Google sigue produciéndose cuando se agrega un canal, pero no hay opción de elegir el canal al que se envía el vídeo.

**Para crear un canal de YouTube:**

1. Vaya a [https://www.youtube.com](https://www.youtube.com/) e inicie sesión con sus credenciales de cuenta de Google.
1. En la esquina superior derecha de la página de YouTube, haga clic en la imagen de perfil (también puede aparecer como una carta dentro de un círculo de color sólido) y, a continuación, haga clic en **[!UICONTROL Configuración de YouTube]** (icono de engranaje redondo).
1. En la página Información general , en el encabezado Funciones adicionales , haga clic en **[!UICONTROL Ver todos mis canales o crear un canal]**.
1. En la página Canales , haga clic en **[!UICONTROL Crear un nuevo canal]**.
1. En la página Cuenta de marca , en el campo Nombre de cuenta de marca , introduzca un nombre comercial o cualquier otro nombre de canal que elija donde desea publicar los recursos de vídeo y, a continuación, haga clic en **[!UICONTROL Crear]**.

   Recuerde el nombre que introduce aquí porque debe introducirlo de nuevo cuando configure YouTube en Experience Manager.

1. (Opcional) Si es necesario, agregue más canales.

   Ahora agregue etiquetas para la publicación.

### Agregar etiquetas para su publicación {#adding-tags-for-publishing}

Para publicar en YouTube sus vídeos, el Experience Manager asocia las etiquetas a uno o varios canales de YouTube. Para agregar etiquetas para la publicación, consulte [Administración de etiquetas](/help/sites-administering/tags.md).

O bien, si desea utilizar las etiquetas predeterminadas en Experience Manager, puede omitir esta tarea y ir a [Habilitar el agente de replicación de YouTube Publish](#enabling-the-youtube-publish-replication-agent).

### Habilitar el agente de replicación de YouTube Publish {#enabling-the-youtube-publish-replication-agent}

Después de habilitar el agente de replicación de YouTube Publish, si desea probar la conexión con la cuenta de Google Cloud, pulse **[!UICONTROL Probar conexión]**. La ficha del explorador muestra los resultados de la conexión. Si ha añadido canales de YouTube, se mostrará una lista de ellos como parte de la prueba.

1. En la esquina superior izquierda del Experience Manager, haga clic en el logotipo del Experience Manager y, a continuación, en el carril izquierdo, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Implementación]** > **[!UICONTROL Replicación]** > **[!UICONTROL Agentes en Author]**.
1. En la página Agentes del autor , haga clic en **[!UICONTROL Publicación en YouTube]**.
1. En la barra de herramientas, a la derecha de Configuración, haga clic en **[!UICONTROL Editar]**.
1. Seleccione el **[!UICONTROL Habilitado]** para activar el agente de replicación.
1. Haga clic en **[!UICONTROL Aceptar]**.

   Ahora, configure YouTube en Experience Manager.

### Configuración de YouTube en Experience Manager {#setting-up-youtube-in-aem}

A partir de Experience Manager 6.4, se introdujo un nuevo método de interfaz de usuario táctil para configurar la publicación de YouTube en Experience Manager. En función de la instancia instalada de Experience Manager que esté utilizando, realice una de las siguientes acciones:

* Para configurar YouTube en Experience Manager antes de la versión 6.4, consulte [Configuración de YouTube en Experience Manager antes de la versión 6.4](/help/assets/video.md#setting-up-youtube-in-aem-before).
* Para configurar YouTube en Experience Manager 6.4 o posterior, consulte [Configuración de YouTube en Experience Manager 6.4 y posterior](#setting-up-youtube-in-aem-and-later).

#### Configuración de YouTube en Experience Manager 6.4 y posterior {#setting-up-youtube-in-aem-and-later}

1. Asegúrese de iniciar sesión en la instancia de Dynamic Media as a Administrator.
1. En la esquina superior izquierda, pulse el logotipo del Experience Manager y, a continuación, en el carril izquierdo, pulse **[!UICONTROL Herramientas]**(icono de martillo) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de publicación de YouTube]**.
1. Toque **[!UICONTROL global]** (no lo seleccione).

1. Cerca de la esquina superior derecha de la página global, pulse **[!UICONTROL Crear]**.
1. En la página Crear configuración de YouTube, en Configuración de plataforma de Google Cloud, en el campo **[!UICONTROL Nombre de aplicación]**, introduzca el ID de proyecto de Google.

   Ha especificado el ID del proyecto al configurar Google Cloud por primera vez.
Deje abierta la página Crear configuración de YouTube . en un momento, volverás a eso.

   ![6_5_youtubepublish-createyoutubfiguration](assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. Con un editor de texto sin formato, abra el archivo JSON que descargó y guardó anteriormente en la tarea [Configuración de la nube de Google](/help/assets/video.md#configuring-google-cloud-settings).
1. Seleccione y copie todo el texto JSON.
1. Vuelva al cuadro de diálogo Configuración de cuenta de YouTube. En el campo **[!UICONTROL Configuración JSON]**, pegue el texto JSON.
1. Cerca de la esquina superior derecha de la página, pulse **[!UICONTROL Guardar]**.

   Ahora, configure los canales de YouTube en Experience Manager.

1. Toque **[!UICONTROL Agregar canal]**.
1. En el campo Nombre de canal , introduzca el nombre del canal que ha creado en la tarea **[!UICONTROL Adición de uno o más canales a YouTube]** más temprano.

   Si lo desea, puede agregar una descripción.

1. Pulse **[!UICONTROL Agregar]**.
1. Se muestra la autenticación de YouTube/Google. Si aún no ha iniciado sesión en la cuenta de Google Cloud, omita este paso.

   * Introduzca el nombre de usuario y la contraseña de Google asociados al ID del proyecto de Google y el texto JSON anterior.
   * Dependiendo de cuántos canales haya visto su cuenta, verá dos o más artículos. Seleccione un canal. No seleccione la dirección de correo electrónico; no es un canal.
   * En la página siguiente, pulse **[!UICONTROL Accept]** para permitir el acceso a este canal.

1. Toque **[!UICONTROL Permitir]**.

   Ahora, configure las etiquetas para su publicación.

1. **[!UICONTROL Configuración de etiquetas para la publicación]** - En la página Cloud Services > YouTube , pulse el icono del lápiz para editar la lista de etiquetas que desee utilizar.
1. Pulse el icono de lista desplegable (acento circunflejo invertido) para poder mostrar la lista de etiquetas disponibles en Experience Manager.
1. Toque una o más etiquetas para poder agregarlas.

   Para eliminar una etiqueta que haya agregado, seleccione la etiqueta y pulse **[!UICONTROL X]**.

1. Cuando haya terminado de agregar las etiquetas que desee, pulse **[!UICONTROL Guardar]**.

   Ahora publica vídeos en su canal de YouTube.

#### Configuración de YouTube en Experience Manager antes de la versión 6.4 {#setting-up-youtube-in-aem-before}

1. Asegúrese de iniciar sesión en la instancia de Dynamic Media as a Administrator.

1. En la esquina superior izquierda, pulse el logotipo del Experience Manager y, a continuación, en el carril izquierdo, pulse **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Implementación]** > **[!UICONTROL Cloud Services]**.
1. En el encabezado Servicios de terceros, en YouTube, pulse **[!UICONTROL Configurar ahora]**.
1. En el cuadro de diálogo Crear configuración, introduzca un título (obligatorio) y un nombre (opcional) en los campos correspondientes.
1. Pulse **[!UICONTROL Crear]**.
1. En el cuadro de diálogo Configuración de cuenta de YouTube, en el campo **[!UICONTROL Nombre de la aplicación]**, introduzca el ID del proyecto de Google.

   Ha especificado el ID del proyecto al principio [configuración de la configuración de Google Cloud](/help/assets/video.md#configuring-google-cloud-settings) más temprano.
Deje abierto el cuadro de diálogo Configuración de cuenta de YouTube; vas a volver en un momento.

1. Con un editor de texto sin formato, abra el archivo JSON que descargó y guardó anteriormente en la tarea Configuración de Google Cloud .
1. Seleccione y copie todo el texto JSON.
1. Vuelva al cuadro de diálogo Configuración de cuenta de YouTube. En el campo **[!UICONTROL Configuración JSON]**, pegue el texto JSON.
1. Pulse **[!UICONTROL Aceptar]**.

   Ahora, configure los canales de YouTube en Experience Manager.

1. A la derecha de **[!UICONTROL Canales disponibles]**, pulse **+** (icono del signo “más”).
1. En el cuadro de diálogo Configuración de canal de YouTube, en el apartado Título, escriba el nombre del canal que creó en la tarea **[!UICONTROL Agregar uno o más canales a YouTube]** anteriormente.

   Si lo desea, puede agregar una descripción.

1. Pulse **[!UICONTROL Aceptar]**.
1. Se muestra la autenticación de YouTube/Google. Si aún no ha iniciado sesión en la cuenta de Google Cloud, omita este paso.

   * Introduzca el nombre de usuario y la contraseña de Google asociados al ID del proyecto de Google y el texto JSON anterior.
   * Dependiendo de cuántos canales haya visto su cuenta, verá dos o más artículos. Seleccione un canal. No seleccione la dirección de correo electrónico; no es un canal.
   * En la página siguiente, pulse **[!UICONTROL Accept]** para permitir el acceso a este canal.

1. Toque **[!UICONTROL Permitir]**.

   Ahora, configure las etiquetas para su publicación.

1. **[!UICONTROL Configuración de etiquetas para la publicación]** - En la página Cloud Services > YouTube , pulse el icono del lápiz para editar la lista de etiquetas que desee utilizar.
1. Pulse el icono de lista desplegable (acento circunflejo invertido) para poder mostrar la lista de etiquetas disponibles en Experience Manager.
1. Toque una o más etiquetas para poder agregarlas.

   Para eliminar una etiqueta que haya agregado, seleccione la etiqueta y pulse **X**.

1. Cuando haya terminado de agregar las etiquetas que desee, pulse **[!UICONTROL OK]**.

   Ahora publica vídeos en su canal de YouTube.

### (Opcional) Automatice la configuración de las propiedades predeterminadas de YouTube para los vídeos cargados {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

Si lo desea, puede automatizar la configuración de las propiedades de YouTube al cargar los vídeos creando un perfil de procesamiento de metadatos en el Experience Manager.

Para crear el perfil de procesamiento de metadatos, en primer lugar copiará valores de los campos **[!UICONTROL Etiqueta de campo]**, **[!UICONTROL Asignar a propiedad]** y **[!UICONTROL Opciones]**, todos se encuentran en Esquemas de metadatos para vídeo. A continuación, cree su perfil de procesamiento de metadatos de vídeo de YouTube agregándole esos valores.

Para automatizar la configuración de las propiedades predeterminadas de YouTube para los vídeos cargados:

1. En la esquina superior izquierda, pulse el logotipo del Experience Manager y, a continuación, en el carril izquierdo, haga clic en **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Recursos]** > **[!UICONTROL Esquemas de metadatos]**.
1. Haga clic en **[!UICONTROL default]**. (No agregue una marca de verificación al cuadro de selección a la izquierda de &quot;predeterminado&quot;).
1. En el **[!UICONTROL default]** , marque la casilla a la izquierda de **[!UICONTROL video]** y, a continuación, toque **[!UICONTROL Editar]**.
1. En la página Editor de esquemas de metadatos , pulse el botón **[!UICONTROL Avanzadas]** pestaña .
1. Bajo el encabezado Publicación de YouTube, haga clic en **[!UICONTROL Categoría de YouTube]**.
1. En el lado derecho de la página, debajo de la sección **[!UICONTROL Configuración]** , haga lo siguiente:

   * En el **[!UICONTROL Asignar a la propiedad]** campo de texto, seleccione y copie el valor.
Pegue el valor copiado en el editor de texto abierto. Necesitará este valor más adelante cuando cree su perfil de procesamiento de metadatos. Deje abierto el editor de texto.

   * En **[!UICONTROL Opciones]**, seleccione y copie el valor predeterminado que desee usar (como People &amp; Blogs o Science &amp; Technology).
Pegue el valor copiado en el editor de texto abierto. Necesitará este valor más adelante cuando cree su perfil de procesamiento de metadatos. Deje abierto el editor de texto.

1. Bajo el encabezado Publicación de YouTube , pulse **[!UICONTROL Privacidad de YouTube]**.
1. En el lado derecho de la página, debajo de la sección **[!UICONTROL Configuración]** , haga lo siguiente:

   * En el **[!UICONTROL Asignar a la propiedad]** campo de texto, seleccione y copie el valor.
Pegue el valor copiado en el editor de texto abierto. Necesitará este valor más adelante cuando cree su perfil de procesamiento de metadatos. Deje abierto el editor de texto.

   * En **[!UICONTROL Opciones]**, seleccione y copie el valor predeterminado que desee utilizar. Tenga en cuenta que las opciones se agrupan en pares de dos. El campo inferior del par es el valor predeterminado que desea copiar, como público, no enumerado o privado.
Pegue el valor copiado en el editor de texto abierto. Necesitará este valor más adelante cuando cree su perfil de procesamiento de metadatos. Deje abierto el editor de texto.

1. Cerca de la esquina superior derecha de la página Editor de esquemas de metadatos , haga clic en **[!UICONTROL Cancelar]**.
1. En la esquina superior izquierda del Experience Manager, pulse el logotipo del Experience Manager y, a continuación, en el carril izquierdo, haga clic en **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Recursos]** > **[!UICONTROL Perfiles de metadatos]**.

1. En la página Perfiles de metadatos , cerca de la esquina superior derecha de la página, haga clic en **[!UICONTROL Crear]**.
1. En el cuadro de diálogo Agregar perfil de metadatos, en el campo de texto **[!UICONTROL Título del perfil]**, escriba el nombre `YouTube Video` y haga clic en **[!UICONTROL Crear]**.
1. En la página Editor de perfiles de metadatos , haga clic en el botón **[!UICONTROL Avance]** pestaña .
1. Agregue al perfil los valores de publicación de YouTube copiados haciendo lo siguiente:

   * En el lado derecho de la página, haga clic en el botón **[!UICONTROL Generar formulario]** pestaña .
   * (Opcional) Arrastre el componente etiquetado **[!UICONTROL Encabezado de sección]** a la izquierda y suéltela en el área del formulario.
   * (Opcional) Haga clic en **[!UICONTROL Etiqueta de campo]** para seleccionar el componente.
   * (Opcional) En la parte derecha de la página, debajo de la ficha Configuración , en el campo de texto Etiqueta de campo , introduzca `YouTube Publishing`.
   * Haga clic en el **[!UICONTROL Generar formulario]** y, a continuación, arrastre el componente etiquetado **[!UICONTROL Texto de varios valores]** y suéltelo debajo de la variable **[!UICONTROL Publicación en YouTube]** que ha creado.

   * Haga clic en **[!UICONTROL Etiqueta de campo]** por lo que el componente está seleccionado.
   * A la derecha de la página, en la ficha Configuración , pegue los valores de Publicación de YouTube (valor de Etiqueta de campo y Valor de Asignar a propiedad ) que ha copiado anteriormente en sus respectivos campos del formulario. Pegue el valor Opciones en el campo Valor predeterminado .

1. Agregue al perfil los valores de privacidad de YouTube copiados haciendo lo siguiente:

   * En el lado derecho de la página, haga clic en el botón **[!UICONTROL Generar formulario]** pestaña .
   * (Opcional) Arrastre el componente etiquetado **[!UICONTROL Encabezado de sección]** a la izquierda y suéltela en el área del formulario.
   * (Opcional) Haga clic en **[!UICONTROL Etiqueta de campo]** para seleccionar el componente.
   * (Opcional) En la parte derecha de la página, debajo de la ficha Configuración , en el campo de texto Etiqueta de campo , introduzca `YouTube Privacy`.
   * Haga clic en el **[!UICONTROL Generar formulario]** y, a continuación, arrastre el componente etiquetado **[!UICONTROL Texto de varios valores]** y suéltelo debajo de la variable **[!UICONTROL Privacidad de YouTube]** creado.

   * Haga clic en **[!UICONTROL Etiqueta de campo]** por lo que el componente está seleccionado.
   * A la derecha de la página, en la ficha Configuración , pegue los valores de Publicación de YouTube (valor de Etiqueta de campo y Valor de Asignar a propiedad ) que ha copiado anteriormente en sus respectivos campos del formulario. Pegue el valor Opciones en el campo Valor predeterminado .

1. Junto a la esquina superior derecha de la página, haga clic en **[!UICONTROL Guardar]**.
1. Aplique el perfil de metadatos de publicación de YouTube a las carpetas donde vaya a cargar los vídeos. Debe tener configurados tanto el perfil de metadatos como el perfil de vídeo.

   Consulte [Perfiles de metadatos](/help/assets/metadata-config.md#metadata-profiles) y [Perfiles de vídeo](/help/assets/video-profiles.md).

### Publicación de vídeos en el canal de YouTube {#publishing-videos-to-your-youtube-channel}

Ahora asocia las etiquetas que agregó anteriormente a los recursos de vídeo. Este proceso permite al Experience Manager saber qué recursos publicar en el canal de YouTube.

>[!NOTE]
>
>Cuando se ejecuta en Dynamic Media en modo Scene7, la publicación inmediata no se publica automáticamente en YouTube. Cuando se configura el modo Dynamic Media - Scene7, hay dos opciones de publicación entre las que elegir: **[!UICONTROL Inmediatamente]** o **[!UICONTROL Tras la activación]**.
>
>**[!UICONTROL Publicar inmediatamente]** significa que el recurso cargado (una vez sincronizado con IPS) se publica automáticamente en el sistema de entrega. Aunque eso es cierto para Dynamic Media, no es así para YouTube. Para publicar en YouTube, debe publicar mediante Autor Experience Manager.

>[!NOTE]
>
>Para publicar contenido de YouTube, el Experience Manager utiliza la variable **[!UICONTROL Publicar en YouTube]** flujo de trabajo, que permite controlar el progreso y ver la información de los errores.
>
>Consulte [Monitorización de la codificación de vídeo y progreso de publicación de YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).
>
>Para obtener información de progreso más detallada, puede monitorizar el registro de YouTube en la replicación. Sin embargo, tenga en cuenta que esta supervisión requiere acceso de administrador.

**Para publicar vídeos en el canal de YouTube:**

1. En Experience Manager, vaya a un recurso de vídeo que desee publicar en el canal de YouTube.
1. Seleccione el recurso de vídeo (el conjunto de vídeos adaptables).
1. En la barra de herramientas, haga clic en **[!UICONTROL Propiedades]**.
1. En la pestaña Básico , bajo el encabezado Metadatos , haga clic en **[!UICONTROL Abrir cuadro de diálogo de selección]** a la derecha del campo Etiquetas .
1. En la página Seleccionar etiquetas , vaya a las etiquetas que desee utilizar y, a continuación, seleccione una o varias etiquetas.

   Recuerde que las etiquetas deben estar asociadas al canal de YouTube.

1. En la esquina superior derecha de la página, haga clic en **[!UICONTROL Select]**.
1. En la esquina superior derecha de la página de propiedades del vídeo, haga clic en **[!UICONTROL Guardar y cerrar]**.
1. En la barra de herramientas, haga clic en **[!UICONTROL Publicación rápida]**.

   Consulte también [Uso de la administración de publicaciones con Experience Manager Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html).

   Si lo desea, puede verificar el vídeo publicado en su canal de YouTube.

### (Opcional) Verifique el vídeo publicado en YouTube {#optional-verifying-the-published-video-on-youtube}

Si lo desea, puede supervisar el progreso de su publicación en YouTube (o cancelar la publicación).

Consulte [Monitorización de la codificación de vídeo y progreso de publicación de YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

Los tiempos de publicación pueden variar en gran medida en función de numerosos factores que incluyen el formato del vídeo de origen principal, el tamaño del archivo y el tráfico de carga. El proceso de publicación puede tardar entre unos minutos y varias horas. Además, los formatos de mayor resolución se procesan mucho más lentamente. Por ejemplo, 720p y 1080p tardan más en aparecer que 480p.

Después de ocho horas si sigue viendo un mensaje de estado que dice **[!UICONTROL Cargado (procesando, espere)]**, intente quitar el vídeo del sitio de Adobe y cargarlo de nuevo.

### Vincular URL de YouTube a la aplicación web {#linking-youtube-urls-to-your-web-application}

Puede obtener una cadena URL de YouTube que Dynamic Media genera después de publicar el vídeo. Cuando copia la URL de YouTube, esta se coloca en el Portapapeles para que pueda pegarla según sea necesario en las páginas de su sitio web o aplicación.

>[!NOTE]
>
>La URL de YouTube no está disponible para copiarse hasta que no haya publicado el recurso de vídeo en YouTube.

**Para vincular URL de YouTube a su aplicación web:**

1. Vaya a la *YouTube publicado* recurso de vídeo cuya URL desee copiar y, a continuación, selecciónelo.

   Recuerde que las URL de YouTube solo están disponibles para copiarse *after* primero *publicado* los recursos de vídeo a YouTube.

1. En la barra de herramientas, haga clic en **[!UICONTROL Propiedades]**.
1. Haga clic en el **[!UICONTROL Avanzadas]** pestaña .
1. En el encabezado Publicación de YouTube , en la Lista de URL de YouTube, seleccione y copie el texto de la URL en el navegador web para obtener una vista previa del recurso o para agregarlo a la página de contenido web.

### Cancelar la publicación de vídeos para poder eliminarlos de YouTube {#unpublishing-videos-to-remove-them-from-youtube}

Cuando cancela la publicación de un recurso de vídeo en Experience Manager, el vídeo se elimina de YouTube.

>[!CAUTION]
>
>Si elimina un vídeo directamente desde YouTube, el Experience Manager no lo sabe y sigue comportándose como si el vídeo aún se hubiera publicado en YouTube. Cancele siempre la publicación de un recurso de vídeo de YouTube mediante el Experience Manager .

>[!NOTE]
>
>Para eliminar contenido de YouTube, el Experience Manager utiliza la variable **[!UICONTROL Cancelar publicación desde YouTube]** flujo de trabajo, que permite controlar el progreso y ver la información de los errores.
>
>Consulte [Monitorización de la codificación de vídeo y progreso de publicación de YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

**Para cancelar la publicación de vídeos para eliminarlos de YouTube:**

1. Vaya a los recursos de vídeo que desea cancelar la publicación desde el canal de YouTube.
1. En un modo de selección de recursos, seleccione uno o varios recursos de vídeo publicados.
1. En la barra de herramientas, haga clic en **[!UICONTROL Administrar publicación]**. Pulse el icono de tres puntos (. . .) en la barra de herramientas, de modo que **[!UICONTROL Administrar publicación]** se abre.
1. En la página Administrar publicación , pulse **[!UICONTROL Cancelar la publicación]**.
1. En la esquina superior derecha de la página, pulse **[!UICONTROL Siguiente]**.
1. En la esquina superior derecha de la página, pulse **[!UICONTROL Cancelar la publicación]**.

## Monitorización de la codificación de vídeo y progreso de publicación de YouTube {#monitoring-video-encoding-and-youtube-publishing-progress}

Cuando se carga un nuevo vídeo en una carpeta que tiene aplicada la codificación de vídeo o se publica en YouTube, se puede supervisar el progreso de la codificación de vídeo/publicación de YouTube. El progreso real de publicación de YouTube solo está disponible mediante los registros. Sin embargo, su fracaso o éxito se enumera de maneras adicionales descritas en el siguiente procedimiento. Además, recibe notificaciones por correo electrónico cuando se completa o interrumpe un flujo de trabajo de publicación o una codificación de vídeo de YouTube.

### Monitorización del progreso {#monitoring-progress}

1. Vea el progreso de la codificación de vídeo en la carpeta de recursos:

   * En la vista de tarjeta, el progreso de la codificación de vídeo se muestra en el recurso por porcentaje. Si hay un error, esta información también se muestra en el recurso.

   ![chlimage_1-429](assets/chlimage_1-429.png)

   * En la vista de lista, el progreso de codificación de vídeo se muestra en la variable **[!UICONTROL Estado de procesamiento]** para abrir el Navegador. Si hay un error, este mensaje se muestra en la misma columna.

   ![chlimage_1-430](assets/chlimage_1-430.png)

   Esta columna no se muestra de forma predeterminada. Para habilitar la columna, seleccione **[!UICONTROL Ver configuración]** en el menú desplegable de vistas, agregue la columna **[!UICONTROL Estado de procesamiento]** y pulse o haga clic en **[!UICONTROL Actualizar]**.

   ![chlimage_1-431](assets/chlimage_1-431.png)

1. Vea el progreso en los detalles del recurso. Cuando toque o haga clic en un recurso, abra el menú desplegable y seleccione **[!UICONTROL Cronología]**. Para reducirlo a actividades de flujo de trabajo como codificación o publicación en YouTube, seleccione **[!UICONTROL Flujos de trabajo]**.

   ![chlimage_1-432](assets/chlimage_1-432.png)

   La información del flujo de trabajo, como la codificación, se muestra en la cronología. Para la publicación en YouTube, la cronología de flujo de trabajo también incluye el nombre del canal de YouTube y la URL de vídeo de YouTube. Además, puede ver cualquier notificación de error en la cronología del flujo de trabajo una vez finalizada la publicación.

   >[!NOTE]
   >
   >Podría llevar mucho tiempo que los mensajes de error/error finalmente se registren debido a varias configuraciones de flujo de trabajo en **[!UICONTROL reintentos]**, **[!UICONTROL retraso de reintentos]** y **[!UICONTROL timeout]** from [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), por ejemplo:
   >
   >    * Configuración de cola de trabajos Apache Sling
   >    * Controlador de trabajos de proceso externo de flujo de trabajo de Granite de Adobe
   >    * Cola de tiempo de espera de flujo de trabajo de Granite

   >
   >Puede ajustar el **[!UICONTROL reintentos]**, **[!UICONTROL retraso de reintentos]** y **[!UICONTROL timeout]** en estas configuraciones.

1. Para los flujos de trabajo en curso, consulte Instancias de flujo de trabajo disponibles en **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Instancias]**.

   >[!NOTE]
   >
   >Necesita derechos administrativos para acceder al **[!UICONTROL Herramientas]** para abrir el Navegador.

   ![chlimage_1-433](assets/chlimage_1-433.png)

   Seleccione la instancia y pulse **[!UICONTROL Abrir historial]**.

   ![chlimage_1-434](assets/chlimage_1-434.png)

   Desde el área Instancias de flujo de trabajo, también puede suspender, finalizar o cambiar el nombre de los flujos de trabajo. Consulte [Administración de flujos de trabajo](/help/sites-administering/workflows-administering.md) para obtener más información.

1. Para los trabajos con errores, consulte Errores de flujo de trabajo disponibles en **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Errores]**. El **[!UICONTROL error de flujo de trabajo]** muestra todas las actividades de flujo de trabajo con errores.

   >[!NOTE]
   >
   >Necesita derechos administrativos para acceder al **[!UICONTROL Herramientas]** para abrir el Navegador.

   ![chlimage_1-435](assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >Podría llevar mucho tiempo que el mensaje de error finalmente se registre debido a varias configuraciones de flujo de trabajo en **[!UICONTROL reintentos]**, **[!UICONTROL retraso de reintentos]** y **[!UICONTROL timeout]** from [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), por ejemplo:
   >
   >
   >
   >    * Configuración de cola de trabajos Apache Sling
   >    * Controlador de trabajos de proceso externo de flujo de trabajo de Granite de Adobe
   >    * Cola de tiempo de espera de flujo de trabajo de Granite

   >
   >
   >Puede ajustar el **[!UICONTROL reintentos]**, **[!UICONTROL retraso de reintentos]** y **[!UICONTROL timeout]** en estas configuraciones.

1. Para ver los flujos de trabajo completados, consulte Archivo de flujo de trabajo, disponible en **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Archivar]**. El **[!UICONTROL archivo de flujo de trabajo]** enumera todas las actividades de flujo de trabajo completadas.

   >[!NOTE]
   >
   >Necesita derechos administrativos para acceder al **[!UICONTROL Herramientas]** para abrir el Navegador.

   ![chlimage_1-436](assets/chlimage_1-436.png)

1. Recibe notificaciones por correo electrónico sobre los trabajos de flujo de trabajo anulados o fallidos. Un administrador puede configurar estas notificaciones por correo electrónico. Consulte [Configuración de notificaciones por correo electrónico](#configuring-e-mail-notifications).

#### Configuración de notificaciones por correo electrónico {#configuring-e-mail-notifications}

>[!NOTE]
>
>Necesita derechos administrativos para acceder al **[!UICONTROL Herramientas]** para abrir el Navegador.

La configuración de la notificación depende de si desea que se envíen notificaciones para trabajos de codificación o trabajos de publicación de YouTube:

* Para los trabajos de codificación, puede acceder a la página de configuración de todas las notificaciones por correo electrónico del flujo de trabajo del Experience Manager en **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]** y buscando **[!UICONTROL Servicio de notificación de correo electrónico del flujo de trabajo CQ de día]**. Consulte [Configurar la notificación por correo electrónico en el Experience Manager](/help/sites-administering/notification.md). Puede seleccionar o desmarcar las casillas de verificación de **[!UICONTROL Notificar al anular]** o **[!UICONTROL Notificar al finalizar]** en consecuencia.

* Para los trabajos de publicación de YouTube, haga lo siguiente:

1. En el Experience Manager, pulse **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página Modelos de flujo de trabajo , seleccione **[!UICONTROL Publicar en YouTube]** y, a continuación, toque **[!UICONTROL Editar]** en la barra de herramientas.
1. Cerca de la esquina superior derecha de la página de flujo de trabajo Publicar en YouTube , pulse **[!UICONTROL Editar]**.
1. Pase el puntero del ratón sobre el componente Carga de YouTube y, a continuación, pulse una vez para mostrar la barra de herramientas en línea.

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. En la barra de herramientas en línea, pulse el icono Configuración (llave inglesa). Haga clic en el **[!UICONTROL Argumentos]** pestaña .

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. En el cuadro de diálogo Proceso de carga de YouTube: Propiedades de los pasos , pulse el botón **[!UICONTROL Argumentos]** pestaña .

   ![6_5_publishtoyoutubeworkflow-discussions-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. Puede seleccionar o desmarcar las siguientes casillas de verificación:

   * Inicio de publicación
   * Error durante la publicación
   * Finalización de la publicación : incluye información sobre canales y direcciones URL

   Si desactiva una casilla de verificación, no recibirá la notificación de correo electrónico especificada del flujo de trabajo de YouTube Publish.

   >[!NOTE]
   >
   >Estos correos electrónicos son específicos de YouTube y se suman a las notificaciones de correo electrónico genéricas del flujo de trabajo. Como resultado, puede recibir dos conjuntos de notificaciones por correo electrónico: la notificación genérica disponible en la variable **[!UICONTROL Servicio de notificación de correo electrónico del flujo de trabajo CQ de día]** y una específica de YouTube según los ajustes de configuración.

1. Cuando haya terminado, pulse el botón **[!UICONTROL Listo]** (marca de verificación).
1. En la página de flujo de trabajo Publicar en YouTube , cerca de la esquina superior derecha, pulse **[!UICONTROL Sincronización]**.

## Anotar recursos de vídeo {#annotate-video-assets}

1. En el [!DNL Assets] consola, seleccione **[!UICONTROL Editar]** en la tarjeta del recurso para mostrar la página de detalles del recurso.
1. Para reproducir el vídeo, haga clic en **[!UICONTROL Vista previa]**.
1. Para realizar anotaciones en el vídeo, haga clic en **[!UICONTROL Anotar]**. Se añade una anotación en el momento (fotograma) concreto del vídeo. Al anotar, puede dibujar en el lienzo e incluir un comentario con el dibujo. Los comentarios se guardan automáticamente. Para salir del asistente de anotaciones, haga clic en **[!UICONTROL Cerrar]**.

   ![Dibujar y anotar en un marco de vídeo](assets/annotate-video.png)

1. Busque un punto específico en el vídeo, establezca el tiempo en segundos en el campo de **texto** y haga clic en **Saltar**. Por ejemplo, para omitir los primeros 20 segundos de vídeo, introduzca 20 en el campo de texto.

   ![Busque un momento en un vídeo para omitir en segundos especificados](assets/seek-in-video.png)

1. Para verla en la línea de tiempo, haga clic en una anotación. Para eliminar la anotación de la cronología, haga clic en **[!UICONTROL Eliminar]**.

   ![Ver anotaciones y los detalles en la cronología](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [Administrar recursos digitales en Experience Manager Assets](/help/assets/manage-assets.md)
>* [Administrar colecciones en Experience Manager Assets](/help/assets/manage-collections.md)
>* [Documentación de vídeo de Dynamic Media](/help/assets/video.md).

