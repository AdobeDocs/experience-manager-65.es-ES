---
title: Notificaciones push
seo-title: Notificaciones push
description: Siga esta página para obtener información sobre cómo utilizar las notificaciones push en una aplicación de AEM Mobile.
seo-description: Siga esta página para obtener información sobre cómo utilizar las notificaciones push en una aplicación de AEM Mobile.
uuid: 0ed8b183-ef81-487f-8f35-934d74ec82af
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: ed8c51d2-5aac-4fe8-89e8-c175d4ea1374
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '3291'
ht-degree: 1%

---


# Notificaciones push{#push-notifications}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Poder avisar instantáneamente a los usuarios de la aplicación de AEM Mobile con notificaciones importantes es crucial para el valor de una aplicación móvil y sus campañas de marketing. Aquí describimos los pasos que deben seguirse para permitir que la aplicación reciba notificaciones push y cómo configurar y enviar notificaciones push desde AEM Mobile a la aplicación instalada en el teléfono. Además, en esta sección se describe cómo configurar la función [Vinculación profunda](#deeplinking) para las notificaciones push.

>[!NOTE]
>
>*Las notificaciones push no tienen envío garantizado; son más como anuncios. Se hace el mejor esfuerzo para asegurarse de que todos los demás los reciban, pero no son un mecanismo de envío garantizado. Además, el tiempo para enviar una notificación push puede variar de menos de un segundo a media hora.*

El uso de notificaciones push con AEM requiere unas tecnologías diferentes. En primer lugar, se debe utilizar un proveedor de servicio de notificaciones push para administrar las notificaciones y los dispositivos (AEM aún no lo hace). Hay dos proveedores configurados de forma predeterminada con AEM: [Servicio de notificación simple de Amazon](https://aws.amazon.com/sns/) (o SNS) y [Pushwoosh](https://www.pushwoosh.com/). En segundo lugar, la tecnología push para un sistema operativo móvil determinado debe pasar por el servicio adecuado — Servicio de notificaciones push de Apple (o APNS) para dispositivos iOS; y Google Cloud Messaging (o GCM) para dispositivos Android. Aunque AEM no se comunica directamente con estos servicios específicos de la plataforma, AEM debe proporcionar cierta información de configuración relacionada junto con las notificaciones para que estos servicios ejecuten la notificación push.

Una vez instalado y configurado (como se explica a continuación) funciona de esta manera:

1. Se crea una notificación push en AEM y se envía al proveedor de servicio (Amazon SNS o Pushwoosh).
1. El proveedor de servicio lo recibe y lo envía al proveedor principal (APNS o GCM).
1. El proveedor principal envía la notificación a todos los dispositivos registrados para esa notificación push. Para cada dispositivo utiliza la red de datos móviles o WiFi, lo que esté disponible en el dispositivo.
1. La notificación se muestra en el dispositivo si la aplicación para la que está registrado no se está ejecutando. Si un usuario toca la notificación, se inicio la aplicación y se muestra la notificación dentro de la aplicación. En el caso de que la aplicación ya se esté ejecutando, solo se mostrará la notificación en la aplicación.

Esta versión de AEM admite dispositivos móviles iOS y Android.

## Información general y procedimiento {#overview-and-procedure}

Para utilizar las notificaciones push en una aplicación de AEM Mobile, deben realizarse los siguientes pasos de alto nivel.

Normalmente, un desarrollador AEM:

1. Registrarse con los servicios de mensajería de Apple y Google
1. Regístrese con un servicio de mensajería push y configúrelo
1. Añadir compatibilidad push en la aplicación
1. Preparar un teléfono para realizar pruebas

Mientras que un administrador AEM:

1. Configurar push en aplicaciones AEM
1. Creación e implementación de la aplicación
1. Enviar una notificación push
1. Configurar vinculación profunda *(opcional)*

### Paso 1: Regístrese con los servicios de mensajería de Apple y Google {#step-register-with-apple-and-google-messaging-services}

#### Uso del servicio de notificaciones push de Apple (APNS) {#using-the-apple-push-notification-service-apns}

Vaya a la página de Apple [aquí](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html) para familiarizarse con el servicio de notificaciones push de Apple.

Para utilizar APNS, necesitará un archivo **Certificate** (un archivo .cer), una push **Private Key** (un archivo .p12) y una **Private Key Password** de Apple. Las instrucciones sobre cómo hacerlo pueden encontrarse [aquí](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html).

#### Uso del servicio Google Cloud Messaging (GCM) {#using-the-google-cloud-messaging-gcm-service}

>[!NOTE]
>
>Google está reemplazando GCM con un servicio similar llamado Firebase Cloud Messaging (FCM). Para obtener más información sobre FCM, haga clic [aquí](https://developers.google.com/cloud-messaging/faq).

Vaya a la página de Google [aquí](https://developer.android.com/google/gcm/index.html) para familiarizarse con Google Cloud Messaging para Android.

Deberá seguir los pasos [aquí](https://developer.android.com/google/gcm/gs.html) para **Crear un proyecto de Google API**, **Habilitar el servicio GCM** y **Obtener una clave de API**. Necesitará la **clave de API** para enviar notificaciones push a dispositivos Android. Además, registre su **Número de proyecto**, que a veces también se denomina **Id de remitente de GCM**.

Los siguientes pasos muestran un método diferente para crear claves de API de GCM:

1. Inicie sesión en Google y vaya a la [página de desarrolladores de Google](https://developers.google.com/mobile/add?platform=android&amp;cntapi=gcm).
1. Elija la aplicación en la lista (o cree una nueva).
1. En Nombre del paquete de Android, introduzca su ID de aplicación, por ejemplo: `com.adobe.cq.mobile.weretail.outdoorsapp`. (Si no funciona, inténtelo nuevamente con &quot;test.test&quot;).
1. Haga clic en **Continuar para elegir y configurar servicios**
1. Seleccione Cloud Messaging y, a continuación, haga clic en **Habilitar Google Cloud Messaging**.
1. Se mostrarán la nueva clave de API de servidor y el ID del remitente (nuevo o existente).

>[!NOTE]
>
>Registre la clave de API del servidor. Este valor se introduce en el sitio del proveedor push.

### Paso 2: Registrar y configurar un servicio de mensajería push {#step-register-and-configure-a-push-messaging-service}

AEM está configurado para usar uno de los tres servicios para notificaciones push:

* SNS de Amazon
* Pushwoosh
* Adobe Mobile Services

*Las configuraciones* SNS y  ** Pushwoshte de Amazon le permitirán enviar datos insertados desde AEM pantallas.

*La configuración de Adobe Mobile* Services permite configurar y enviar notificaciones push desde Adobe Mobile Services mediante una cuenta de Adobe Analytics (pero la aplicación debe crearse con este conjunto de configuración para activar las notificaciones push de AMS).

#### Uso del servicio de mensajería SNS de Amazon {#using-the-amazon-sns-messaging-service}

>[!NOTE]
>
>*Puede encontrar información sobre Amazon SNS y un vínculo para crear una nueva cuenta de AWS  [aquí](https://aws.amazon.com/sns/). Puede obtener una cuenta gratuita durante un año.*

Si no desea utilizar Amazon SNS, puede omitir estos pasos.

Siga estos pasos para configurar Amazon SNS para notificaciones push:

1. **Registrarse con Amazon SNS**

   1. Registre su ID de cuenta. El formato debe ser de doce dígitos sin espacios ni guiones, es decir &quot;123456789012&quot;.
   1. Asegúrese de que se encuentra en la región &quot;us-east&quot; o &quot;eu&quot;, ya que un paso posterior (Creación de grupos de identidades) requiere uno de ellos.
   1. Después de registrarse, inicie sesión en la consola de administración y seleccione [SNS](https://console.aws.amazon.com/sns/) (Servicio de notificaciones push). Haga clic en &quot;Comenzar&quot; si aparece.

1. **Crear clave de acceso e ID**

   1. Haga clic en el nombre de inicio de sesión en la parte superior derecha de la pantalla y elija Credenciales de seguridad en el menú.
   1. Haga clic en Teclas de acceso y, en el espacio siguiente, haga clic en **Crear nueva clave de acceso**.
   1. Haga clic en **Mostrar clave de acceso** y copie y guarde el ID de clave de acceso y la clave de acceso secreto que se muestran. Si elige la opción de descargar las claves, obtendrá un archivo csv que contenga esos mismos valores.
   1. En esta página se pueden administrar otros certificados relacionados con la seguridad, entre otros.

   >[!NOTE]
   >
   >Se puede usar una clave de acceso para varias aplicaciones.

   Para las organizaciones que utilizan una cuenta de &quot;Simulador para pruebas de AWS&quot;, los pasos son muy similares y se describen a continuación:

   1. Haga clic en el nombre de inicio de sesión en la parte superior derecha de la pantalla y elija Mis credenciales de seguridad en el menú.
   1. Haga clic en Usuarios en la lista izquierda de acciones y elija su nombre de usuario.
   1. Haga clic en la ficha Credenciales de seguridad.
   1. Desde aquí puede ver sus claves y crear nuevas claves. Guarde las claves para usarlas posteriormente.


1. **Crear un tema**

   1. Haga clic en **Crear tema** y elija un nombre de tema. Registre todos los campos, como ARN del tema, Propietario del tema, Región, Nombre para mostrar.
   1. Haga clic en **Otras acciones de tema** > **Editar directiva de tema**. En **Permitir que estos usuarios se suscriban a este tema**, seleccione **Todos.**
   1. Haga clic en **Actualizar directiva**.

   >[!NOTE]
   >
   >Puede crear varios temas para distintos escenarios, como dev, test, demo, etc. El resto de la configuración de SNS puede seguir siendo la misma. Cree la aplicación con el tema diferente; las notificaciones push enviadas a ese tema solo serán recibidas por la aplicación creada con ese tema.

1. **Crear aplicaciones de plataforma**

   1. Haga clic en Aplicaciones y, a continuación, en Crear aplicación de plataforma. Elija un nombre y seleccione una plataforma (APNS para iOS, GCM para Android). En función de la plataforma, deberán rellenarse otros campos:

      1. Para APNS, se debe introducir un archivo P12, una contraseña, un certificado y una clave privada. Estos deben haberse obtenido en el paso *Uso del servicio de notificaciones push de Apple (APNS)* anterior.
      1. Para GCM, se debe introducir una clave de API. Esto debería haberse obtenido en el paso *Uso del servicio Google Cloud Messaging (GCM)* anterior.
   1. Repita el paso anterior una vez para cada plataforma que admita. Para poder insertar tanto en iOS como en Android, se deben crear dos aplicaciones de plataforma.


1. **Crear un grupo de identidades**

   1. Utilice [Cognito](https://console.aws.amazon.com/cognito) para crear un grupo de identidades que almacenará datos básicos de usuarios no autenticados. En este momento, Amazon Cognito solo admite las regiones &quot;us-east&quot; y &quot;eu&quot;.
   1. Póngale un nombre y marque la casilla &quot;Habilitar el acceso a identidades no autenticadas&quot;.
   1. En la página siguiente (&quot;*Las identidades de Cognito requieren acceso a sus recursos*&quot;), haga clic en Permitir.
   1. En la parte superior derecha de la página, haga clic en el vínculo &quot;*Editar grupo de identidades&quot;*. Se muestra el Id. del grupo de identidades. Guarde este texto para más adelante.
   1. En la misma página, elija la lista desplegable junto a &quot;Función no autenticada&quot; y asegúrese de que tiene seleccionada la función Cognito_&lt;nombre del grupo>UnauthRole. Guarde los cambios.

1. **Configurar el acceso**

   1. Inicie sesión en [Administración de identidades y acceso](https://console.aws.amazon.com/iam/home) (IAM)
   1. Seleccionar funciones
   1. Haga clic en la función creada en el paso anterior, llamada Cognito_&lt;yourIdentityPoolName>Unauth_Role. Registre el &quot;ARN de rol&quot; mostrado.
   1. Abra &quot;Directivas en línea&quot; si aún no se ha abierto. Debe ver una directiva con un nombre como oneClick_Cognito_&lt;yourIdentityPoolName>Unauth_Role_1234567890123.
   1. Haga clic en &quot;Editar directiva&quot;. Reemplace el contenido del Documento de directivas con este fragmento de JSON:

   <table>
    <tbody>
     <tr>
     <td><p> </p> <p>{</p> <p> "Versión": "2012-10-17",</p> <p> "Declaración": [</p> <p> {</p> <p> "Acción": [</p> <p> "mobileanalytics:PutEvents",</p> <p> "cognito-sync:*",</p> <p> "SNS:CreatePlatformEndpoint",</p> <p> "SNS:Subscribe"</p> <p> ],</p> <p> "Efecto": "Allow",</p> <p> "Medio": [</p> <p> "*"</p> <p> ]</p> <p> }</p> <p> ]</p> <p>}</p> <p> </p> </td>
     </tr>
    </tbody>
    </table>

   1. Haga clic en **Aplicar directiva**


#### Uso del servicio de mensajería Pushwoosh {#using-the-pushwoosh-messaging-service}

Si no desea utilizar Pushwoosh, puede omitir este paso.

Para usar Pushwoosh:

1. **Registrarse con Pushwoosh**

   1. Vaya a pushwoosh.com y cree una nueva cuenta.

1. **Creación de un Token de acceso de API**

   1. En el sitio de Pushwoosh, vaya al elemento de menú Acceso a API para generar un Token de acceso de API. Tendrá que registrar esto de forma segura.

1. **Crear una aplicación nueva**

   1. Para la compatibilidad con Android, debe proporcionar la clave de API de GCM.
   1. Al configurar la aplicación, elija Cordova como marco.
   1. Para la compatibilidad con iOS, debe proporcionar el archivo de certificado (.cer), el certificado push (.p12) y la contraseña de clave privada; estos deberían haberse obtenido en el sitio APNS de Apple. En Marco, elija Cordova.
   1. Pushwoosh generará un ID de aplicación para esa aplicación, en la forma &quot;XXXXX-XXXXX&quot;, donde cada X es un valor hexadecimal (de 0 a F).

>[!NOTE]
>
>*Si se configura una segunda aplicación en AEM con el mismo ID de aplicación (y otros valores relacionados: TOKEN DE ACCESO de API e ID de GCM), cualquier notificación push enviada a través de la segunda aplicación en AEM irá a cualquier otra aplicación con ese ID de aplicación.*

### Paso 3: Añadir compatibilidad push para la aplicación {#step-add-push-support-to-the-app}

#### Añadir configuración de ContentSync {#add-contentsync-configuration}

Cree dos nodos de contenido (uno en app-config y otro en app-config-dev) llamados notificationsConfig:

* /content/`<your app>`/shell/jcr:content/page-app/app-config-dev/notificationsConfig
* /content/`<your app>`/shell/jcr:content/page-app/app-config/notificationsConfig

Con estas propiedades (archivos .content.xml):
&lt;jcr:root xmlns:jcr=&quot; [https://www.jcp.org/jcr/1.0](https://www.jcp.org/jcr/1.0)&quot; xmlns:nt=&quot; [https://www.jcp.org/jcr/nt/1.0](https://www.jcp.org/jcr/nt/1.0)&quot;
jcr:PrimaryType=&quot;nt:unstructure&quot;
excludeProperties=&quot;[appAPIAccessToken]&quot;
path=&quot;../.../.../...&quot;
targetRootDirectory=&quot;www&quot;
type=&quot;notificationsconfig&quot;/>

>[!NOTE]
>
>El controlador de sincronización de contenido busca esos nodos y, si no están allí, no escribe el archivo page-notifications-config.json.

#### Añadir bibliotecas de clientes {#add-client-libraries}

Las bibliotecas de cliente de notificaciones push deben agregarse a la aplicación siguiendo estos pasos:

En CRXDE Lite:

1. Vaya a */etc/designs/phonegap/&lt;nombre de la aplicación>/clientlibsall.*
1. Doble haga clic en la sección incrustar del panel de propiedades.
1. En el cuadro de diálogo que aparece, agregue una nueva biblioteca de cliente haciendo clic en el botón +.
1. En el nuevo campo de texto, agregue &quot;cq.mobile.push&quot; y haga clic en Aceptar.
1. Añada otro llamado cq.mobile.push.amazon y haga clic en Aceptar.
1. Guarde los cambios.

>[!NOTE]
>
>Si las notificaciones push se eliminan o no se utilizan por consideraciones de espacio en la aplicación y para evitar mensajes de error de la consola, elimine estos clientes de la aplicación.

### Paso 4: Preparar un teléfono para realizar pruebas {#step-prepare-a-phone-for-testing}

>[!NOTE]
>
>*Para las notificaciones push, debe realizar pruebas en un dispositivo real, ya que los emuladores no pueden recibir notificaciones push.*

#### IOS {#ios}

Para iOS deberá utilizar un equipo Mac OS y unirse al [Programa para desarrolladores de iOS](https://developer.apple.com/programs/ios/). Algunas corporaciones tienen licencias corporativas que pueden estar disponibles para todos los desarrolladores.

Con XCode 8.1, antes de utilizar las notificaciones push, debe ir a la ficha Capacidades del proyecto y activar la opción Notificaciones push.

#### Android {#android}

Para instalar la aplicación en un teléfono Android mediante CLI (consulte a continuación: **Paso 6: Cree e implemente la aplicación**), primero debe poner el teléfono en &quot;modo de desarrollador&quot;. Consulte [Activación de las opciones de desarrollador en el dispositivo](https://developer.android.com/tools/device.html#developer-device-options) para obtener más información sobre cómo hacerlo.

### Paso 5: Configurar push en aplicaciones AEM {#step-configure-push-on-aem-apps}

Antes de compilar e implementar en el dispositivo móvil configurado, debe configurar las opciones de notificación para el servicio de mensajería que decidió utilizar.

1. Cree los grupos de autorización adecuados para las notificaciones push.
1. Inicie sesión para AEM como el usuario adecuado, haga clic en la ficha Aplicaciones.
1. Haga clic en la aplicación.
1. Busque el mosaico Administrar Cloud Services y haga clic en el lápiz para modificar las configuraciones de nube.
1. Seleccione Conexión Amazon SNS, Conexión Pushwoosh o Adobe Mobile Services como configuración de notificación.
1. Introduzca las propiedades del proveedor y haga clic en Enviar para guardarlas y en Finalizado. No se verifican a distancia en esta fase, salvo en el caso de AMS.
1. Ahora debería ver la configuración que acaba de introducir en el mosaico Administrar Cloud Services.

### Paso 6: Cree e implemente la aplicación {#step-build-and-deploy-the-app}

**Nota:** Consulte también nuestras instrucciones  [](/help/mobile/building-app-mobile-phonegap.md) aquí sobre la creación de aplicaciones PhoneGap.

Existen dos formas de crear e implementar la aplicación mediante PhoneGap.

**Nota:** Para las pruebas de notificaciones push, los emuladores no serán suficientes porque las notificaciones push utilizan un protocolo distinto entre el proveedor push (Apple o Google) y el dispositivo. El hardware y los emuladores actuales de Mac/PC no admiten esto.

1. *PhoneGap* Builder es un servicio ofrecido por PhoneGap que creará su aplicación en sus servidores y le permitirá descargarla directamente en su dispositivo. Consulte la [documentación de PhoneGap Build](https://build.phonegap.com/) para obtener información sobre cómo configurar y utilizar PhoneGap Build.

1. *La interfaz*  de línea de comandos de PhoneGap (CLI) le permite utilizar un completo conjunto de comandos de PhoneGap en la línea de comandos para crear, depurar e implementar la aplicación. Consulte la [documentación para desarrolladores de PhoneGap](https://docs.phonegap.com/en/edge/guide_cli_index.md.html#The%20Command-Line%20Interface) para obtener información sobre cómo configurar y utilizar la CLI de PhoneGap.

### Paso 7: Enviar una notificación push {#step-send-a-push-notification}

Para crear una nueva notificación y enviarla, siga estos pasos.

1. Crear una nueva notificación

   * En el panel de su aplicación de AEM Mobile, busque el mosaico Notificaciones push.
   * En el menú de la esquina superior derecha, elija &quot;Crear&quot;. Tenga en cuenta que este botón no estará disponible hasta que se configure la configuración de nube por primera vez.
   * En el Asistente para crear notificaciones, escriba un título y un mensaje y, a continuación, haga clic en el botón &quot;Crear&quot;. Su notificación ya está lista para enviarse inmediatamente o más tarde. Se puede editar y el mensaje y/o el título se pueden cambiar y guardar.

1. Enviar la notificación

   * En el panel Aplicaciones, busque el mosaico Notificaciones push.
   * Seleccione la notificación o haga clic en el botón de detalles en la parte inferior derecha (. . .), para mostrar la lista de las notificaciones. Esta lista también indica si una notificación está lista para ser enviada, si ya se ha enviado o si se ha producido un error durante el envío.
   * Seleccione la casilla de verificación de una notificación (solamente) y haga clic en el botón &quot;Enviar notificación&quot; encima de la lista. Tendrá la oportunidad de &quot;Cancelar&quot; o &quot;Enviar&quot; la notificación en el cuadro de diálogo que aparece.

1. Tratamiento de los resultados

   * Si el servicio de notificaciones push (Amazon SNS o Pushwoosh) recibe la solicitud de envío, la confirma como válida y la envía a los proveedores nativos (APNS y GCM) correctamente, el cuadro de diálogo de envío se cerrará sin mensaje. En la lista de notificación, el estado de la notificación se indicará como Enviada.
   * Si falla el envío push, el cuadro de diálogo mostrará un mensaje que indicará el problema. En la lista de notificación, el estado de esa notificación se mostrará como Error, pero si se corrige el problema, la notificación se podrá volver a enviar. En el evento de un error, debe aparecer información adicional sobre el error en el registro de errores del servidor.
   * Tenga en cuenta que existen algunas diferencias de plataforma entre las notificaciones push de iOS y Android. Entre ellos:

      * La creación con CLI inicio la aplicación después de implementarla en Android. En iOS, debe inicio manual. Dado que el paso de registro push se produce al iniciar, las aplicaciones de Android pueden recibir notificaciones push de inmediato (ya que se iniciarán y se registrarán) mientras que las aplicaciones de iOS no.
      * En Android, el texto del botón Aceptar está en mayúsculas (y en cualquier otro botón que se añada a la notificación en la aplicación), mientras que en iOS no lo está.

Para las notificaciones push de AMS, las notificaciones deben estar compuestas y enviadas desde el servidor de AMS. AMS proporciona capacidades adicionales de notificación push más allá de las que proporcionan las notificaciones AEM con AWS y Pushwoosh.

>[!NOTE]
>
>*Las notificaciones push no tienen envío garantizado; son más como anuncios. Se hace el mejor esfuerzo para asegurarse de que todos lo escuchen, pero no son un mecanismo de envío garantizado. Además, el tiempo para enviar una notificación push puede variar de menos de un segundo a media hora.*

### Configuración de vinculación profunda con notificaciones push {#configuring-deep-linking-with-push-notifications}

¿Qué es la vinculación profunda? En el contexto de una notificación push, es un medio para permitir que una aplicación se abra o dirija (si está abierta) a una ubicación específica dentro de la aplicación.

¿Cómo funciona? El autor de una notificación push agrega opcionalmente una etiqueta de botón (p. ej. &quot;¡Muéstrame!&quot;) a la notificación y elige la página que desea vincular en la notificación, a través de un navegador de rutas visuales. Cuando se envía, la pulsación se produce de la forma normal, excepto que en el mensaje en la aplicación, el botón Aceptar se reemplaza por el botón &quot;Rechazar&quot; y se especifica el nuevo botón (&quot;¡Mostrar!&quot;) también aparece. Al hacer clic en el botón nuevo, la aplicación pasará a la página especificada dentro de la aplicación. Al hacer clic en Descartar, simplemente se descartará el mensaje.

Si la aplicación no está abierta, el sombreado aparecerá como normal. Si se realiza una acción en la notificación a la sombra, se abrirá la aplicación y, a continuación, se presentarán al usuario los botones de vínculo profundo en función de la configuración de la notificación push.

Cree la notificación, agregue un texto de botón y una ruta de vínculo para el vínculo profundo opcional:

>[!CAUTION]
>
>.Para acceder al mosaico de notificaciones push de su panel, siga los pasos a continuación.

1. Haga clic en la edición en la esquina superior derecha del mosaico **Administrar Cloud Services**.

   ![chlimage_1-108](assets/chlimage_1-108.png)

1. Seleccione la **Conexión de Pushwoosh**. Haga clic en **Siguiente**. 

   ![chlimage_1-109](assets/chlimage_1-109.png)

1. Introduzca los detalles de las propiedades y haga clic en **Enviar**.

   ![chlimage_1-110](assets/chlimage_1-110.png)

   Cuando se envía la configuración, se muestra el icono **Notificaciones push** en el panel.

   ![chlimage_1-111](assets/chlimage_1-111.png)

### Crear asistente de notificación {#create-notification-wizard}

Una vez que se muestre el mosaico **Notificaciones push** en el panel, utilice el asistente para crear notificaciones para agregar contenido:

1. Haga clic en el símbolo de adición en la esquina superior derecha del mosaico **Notificaciones push** para abrir el **Asistente para crear notificaciones**.

   ![chlimage_1-112](assets/chlimage_1-112.png)

1. Al hacer clic en el icono Examinar de la ruta del vínculo, se muestra al usuario la estructura de contenido de la aplicación.

   Una vez seleccionada la ruta, haga clic en el icono de verificación.

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!NOTE]
   >
   >El texto del botón Vínculo está limitado a 20 caracteres.
   >
   >Si el usuario final no tiene la versión más reciente de la aplicación y la ruta de acceso vinculada no está disponible, la confirmación de la acción del vínculo profundo llevará al usuario a la página principal de la aplicación.

1. Escriba **Detalles de texto** en el **Asistente para crear notificación** y haga clic en **Crear**.

   ![chlimage_1-115](assets/chlimage_1-114.png)

   Para abrir los detalles, haga clic en la notificación push que creó en el mosaico **Notificaciones push**.

   Puede editar propiedades, enviar notificaciones o eliminar la notificación.

   ![chlimage_1-115](assets/chlimage_1-115.png)

>[!NOTE]
>
>**Información adicional**:
>
>Pushwoosh y Amazon SNS no serán compatibles después de la versión 6.4 y estarán disponibles como complemento desde el recurso compartido de paquetes.

### Pasos siguientes {#the-next-steps}

Una vez que conozca los detalles de las notificaciones push para su aplicación, consulte [Personalización del contenido de AEM Mobile](/help/mobile/phonegap-aem-mobile-content-personalization.md).

