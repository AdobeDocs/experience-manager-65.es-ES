---
title: Inicio de sesión en Social con Facebook y Twitter
seo-title: Social Login with Facebook and Twitter
description: El inicio de sesión en Social permite a los visitantes del sitio iniciar sesión con su cuenta de Facebook o Twitter.
seo-description: Social login lets site visitors to sign in with their Facebook or Twitter account.
uuid: f70e346e-0d8c-41a0-a100-206a420088dc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c0a71870-8f95-40c8-9ffd-b7af49723288
role: Admin
exl-id: aed9247c-eb81-470c-9fa4-a98c3df2dcaa
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2783'
ht-degree: 2%

---

# Inicio de sesión en Social con Facebook y Twitter {#social-login-with-facebook-and-twitter}

El inicio de sesión en Social es la capacidad para presentar a un visitante del sitio la opción de iniciar sesión con su cuenta de Facebook o Twitter. Por lo tanto, incluya los datos permitidos de Facebook o Twitter en su perfil de miembro AEM.

![socialloginweretail](assets/socialloginweretail.png)

## Información general de inicio de sesión en Social {#social-login-overview}

Para incluir el inicio de sesión social, es *obligatorio* para crear aplicaciones personalizadas de Facebook y Twitter.

Aunque el ejemplo de venta minorista proporciona aplicaciones y servicios en la nube de Facebook y Twitter de ejemplo, no están disponibles en un [sitio web de producción](../../help/sites-administering/production-ready.md).

Los pasos necesarios son:

1. [Habilitar la autenticación OAuth](#adobe-granite-oauth-authentication-handler) en todas las instancias de publicación AEM.

   Sin OAuth habilitado, los intentos de iniciar sesión fallan.

1. **Crear** una aplicación social y un servicio en la nube.

   * Para admitir el inicio de sesión en Facebook:

      * Cree un [aplicación facebook](#create-a-facebook-app).
      * Cree y publique un [Servicio en la nube facebook Connect](#create-a-facebook-connect-cloud-service).
   * Para admitir el inicio de sesión en Twitter:

      * Cree un [aplicación twitter](#create-a-twitter-app).
      * Cree y publique un [Servicio en la nube twitter Connect](#create-a-twitter-connect-cloud-service).


1. [**Habilitar** inicio de sesión social](#enable-social-login) para un sitio de comunidad.

Existen dos conceptos básicos:

1. **Ámbito** (permisos) especifica los datos que la aplicación puede solicitar.

   * Facebook y Twitter [Adobe Granite OAuth Aplicación y Proveedor](#adobe-granite-oauth-application-and-provider) de forma predeterminada, incluyen los permisos básicos de la aplicación dentro de su ámbito.

1. **Campos** (params) especifica los datos reales solicitados mediante parámetros de URL.

   * Estos campos se especifican en [Proveedor de OAuth de AEM Communities Facebook](#aem-communities-facebook-oauth-provider) y [Proveedor de OAuth de AEM Communities Twitter](#aem-communities-twitter-oauth-provider).
   * Los campos predeterminados son suficientes para la mayoría de los casos de uso, pero se pueden modificar.

## Inicio de sesión en facebook {#facebook-login}

### Versión de la API de facebook {#facebook-api-version}

El inicio de sesión en Social y el ejemplo de Facebook de venta minorista se desarrollaron cuando la API de Facebook Graph era la versión 1.0. A partir de AEM 6.4 GA y AEM 6.3 SP1, el inicio de sesión en redes sociales se actualizó para que funcionara con la versión más reciente de la API de Facebook Graph 2.5.

>[!NOTE]
>
>Para versiones de AEM anteriores, si se enfrenta a una excepción en los registros **No se puede extraer un token de esto**, actualice a la última versión de CFP para esa versión de AEM.

Para obtener información sobre la versión de la API de Facebook Graph, consulte la [Registro de cambios de la API de facebook](https://developers.facebook.com/docs/apps/changelog).

### Crear una aplicación de Facebook {#create-a-facebook-app}

Se requiere una aplicación de Facebook configurada correctamente para habilitar el inicio de sesión social de Facebook.

Para crear una aplicación de Facebook, siga las instrucciones de Facebook en [https://developers.facebook.com/apps/](https://developers.facebook.com/apps/). Los cambios en sus instrucciones no se reflejan en la siguiente información.

En general, desde la API de Facebook v2.7:

* *Agregar nueva aplicación de Facebook*
   * Para *Plataforma*, elija Sitio web:
      * Para *Dirección URL del sitio*, introduzca `  https://<server>:<port>.`
      * Para *Nombre para mostrar*, introduzca un título para utilizarlo como Título del servicio de conexión de Facebook.
      * Para *Categoría*, se recomienda elegir *Aplicaciones para páginas*, pero puede ser cualquier cosa.
      * *Agregar producto: Inicio de sesión en facebook*
      * Para *URI de redireccionamiento de OAuth válidos*, introduzca `  https://<server>:<port>.`

>[!NOTE]
>
>Para el desarrollo, http://localhost:4503 funcionará.

Una vez creada la aplicación, localice la variable **[!UICONTROL ID de la aplicación]** y **[!UICONTROL Secreto de la aplicación]** configuración. Esta información es necesaria para configurar la variable [Servicio en la nube de facebook](#createafacebookcloudservice).

### Creación de un Cloud Service de Facebook Connect {#create-a-facebook-connect-cloud-service}

La variable [Adobe Granite OAuth Aplicación y Proveedor](#adobe-granite-oauth-application-and-provider) , creada mediante la creación de una configuración de Cloud Service, identifica la aplicación de Facebook y los grupos de miembros a los que se agregan los nuevos usuarios.

1. En la instancia de autor de AEM, inicie sesión con privilegios de administrador.
1. En la navegación global, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de inicio de sesión de facebook Social]**.
1. Seleccione la configuración **[!UICONTROL ruta de contexto]**.

   **[!UICONTROL Ruta de contexto]** debe ser la misma que la ruta de configuración de la nube que ha seleccionado al crear o editar un sitio de la comunidad.

1. Compruebe si la ruta de contexto está habilitada para crear servicios en la nube debajo de ella.
1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL Explorador de configuración]**. Seleccione el contexto y edite las propiedades. Habilite Configuraciones de nube si aún no está habilitado.

   ![config-propertiesping](assets/config-propertiespng.png)

   * Consulte la documentación del [Explorador de configuración](/help/sites-administering/configurations.md) para obtener más información.

1. **Crear/editar** Configuración del servicio en la nube de facebook.

   ![fbsocialloginconfigpng](assets/fbsocialloginconfigpng.png)

   * **[!UICONTROL Título]** (*Requerido*) Introduzca un título para mostrar que identifique la aplicación Facebook. Se recomienda utilizar el mismo nombre introducido que la variable *Nombre para mostrar* para la aplicación de Facebook.
   * **[!UICONTROL ID de la aplicación/Clave de API]** (*Requerido*) Introduzca la variable ***ID de la aplicación*** para la aplicación de Facebook. Identifica el [Adobe Granite OAuth Aplicación y Proveedor](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) instancia creada a partir del cuadro de diálogo.
   * **[!UICONTROL Secreto de la aplicación]** (*Requerido*) Introduzca la variable ***Secreto de la aplicación*** para la aplicación de Facebook.
   * **[!UICONTROL Crear usuarios]** Si se selecciona, el inicio de sesión con una cuenta de Facebook creará una entrada de usuario AEM y la agregará como miembro a los grupos de usuarios seleccionados.  El valor predeterminado está marcado (se recomienda encarecidamente).
   * **[!UICONTROL Enmascarar ID de usuario]**: Deje sin seleccionar.
   * **[!UICONTROL Correo electrónico del ámbito]**: el id. de correo electrónico del usuario debe buscarse desde Facebook.
   * **[!UICONTROL Agregar a grupos de usuarios]** seleccione Agregar grupo de usuarios para elegir uno o varios [grupos de miembros](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) para el sitio de la comunidad al que se agregarán los usuarios.

   >[!NOTE]
   >
   >Los grupos pueden agregarse o eliminarse en cualquier momento. Pero las membresías de los usuarios existentes no se verán afectadas. La pertenencia automática solo se aplica a los nuevos usuarios que se crean después de esta actualización de campo. En Sitios donde los usuarios anónimos están deshabilitados, elija agregar usuarios al grupo de miembros de la comunidad correspondiente que esté destinado a ese sitio de comunidad cerrado.

   * Select **[!UICONTROL GUARDAR]**.
   * **[!UICONTROL Publicación]**.


El resultado es un [Adobe Granite OAuth Aplicación y Proveedor](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) que no requiere ninguna modificación adicional a menos que agregue un ámbito (permisos) adicional. El ámbito predeterminado son los permisos estándar para el inicio de sesión en Facebook. Si desea un ámbito adicional, es necesario editar la configuración OSGI directamente. Si hay modificaciones realizadas directamente a través del sistema o la consola, evite editar las configuraciones del servicio en la nube desde la interfaz de usuario táctil para evitar sobrescribirlas.

### Proveedor de OAuth de AEM Communities Facebook {#aem-communities-facebook-oauth-provider}

El proveedor de AEM Communities amplía la variable [Adobe Granite OAuth Aplicación y Proveedor](#adobe-granite-oauth-application-and-provider) instancia.

Este proveedor necesitará editar para:

* Permitir actualizaciones de usuarios
* Añadir campos adicionales [dentro del ámbito](#adobe-granite-oauth-application-and-provider)

   * De forma predeterminada, no se incluyen todos los campos permitidos.

Si es necesario editar, en cada instancia de publicación AEM:

1. Inicie sesión con privilegios de administrador.
1. Vaya a la [Consola web](../../help/sites-deploying/configuring-osgi.md). Por ejemplo, http://localhost:4503/system/console/configMgr.
1. Busque el proveedor de OAuth de AEM Communities Facebook.
1. Seleccione el icono de lápiz para abrirlo y editarlo.

   ![fboauthprov_png](assets/fboauthprov_png.png)

   * **[!UICONTROL ID de proveedor de OAuth]**

      (*Requerido*) El valor predeterminado es *soco-facebook*. No edite.

   * **[!UICONTROL Configuración del Cloud Service]**

      El valor predeterminado es `/etc/  cloudservices /  facebookconnect`. No edite.

   * **[!UICONTROL Configuración del servicio de proveedor de OAuth]**

      El valor predeterminado es `/apps/social/facebookprovider/config/`. No edite.

   * **[!UICONTROL Habilitar etiquetas]**

      No edite.

   * **[!UICONTROL Ruta del usuario]**

      Ubicación en el repositorio donde se almacenan los datos del usuario. Para un sitio de comunidad, para garantizar que los permisos de los miembros para ver el perfil de los demás, la ruta debe ser la predeterminada */home/users/community*.

   * **[!UICONTROL Habilitar campos]**

      Si está activada, los campos que aparecen en la lista se especifican en la solicitud a Facebook para obtener autenticación e información de los usuarios. Se anula la selección del valor predeterminado.

   * **[!UICONTROL Campos]**

      Cuando los campos están habilitados, se incluyen los siguientes campos al llamar a la API de Facebook Graph. Los campos deben estar permitidos dentro del ámbito definido en la configuración del servicio en la nube. Los campos adicionales pueden requerir la aprobación de Facebook. Consulte la sección Permisos de inicio de sesión de Facebook de la documentación de Facebook . Los campos predeterminados añadidos como parámetros son:

      * id
      * name
      * first_name
      * last_name
      * link
      * locale
      * picture
      * timezone
      * update_time
      * verificado
      * correo electrónico

   Si se agrega o cambia algún campo, actualice la configuración del controlador de sincronización predeterminado correspondiente para corregir la asignación.

   * **[!UICONTROL Actualizar usuario]**

      Si se selecciona, actualiza los datos de usuario en el repositorio en cada inicio de sesión para reflejar los cambios de perfil o los datos adicionales solicitados. El valor predeterminado no está seleccionado.


#### Siguientes pasos {#next-steps}

Los siguientes pasos son los mismos para Facebook y Twitter:

* [Publicar las configuraciones del servicio en la nube](#publishcloudservices)
* [Habilitar para un sitio de la comunidad](#enable-social-login)

## Inicio de sesión en twitter {#twitter-login}

### Crear una aplicación de Twitter {#create-a-twitter-app}

Se requiere una aplicación de Twitter configurada para habilitar el inicio de sesión social de Twitter.

Siga las instrucciones más recientes para crear una nueva aplicación de Twitter en [https://apps.twitter.com](https://apps.twitter.com/).

En general:

1. Escriba un *Nombre* que identificará la aplicación de Twitter con los usuarios del sitio web.
1. Especificar una *Descripción*.
1. Para *sitio web* - introduzca `https://<server>`.
1. Para *URL de devolución de llamada* - introduzca `https://server`.

   >[!NOTE]
   >
   >No es necesario especificar el puerto.
   >
   >Para el desarrollo, https://127.0.0.1/ funcionará.

1. Una vez creada la aplicación, localice la variable **[!UICONTROL Clave de consumidor (API)]** y **[!UICONTROL Secreto del consumidor (API)]**. Esta información será necesaria para configurar la variable [Servicio en la nube de twitter](#createatwittercloudservice).

#### Permisos {#permissions}

En la sección Permisos de la administración de aplicaciones de Twitter:

* **[!UICONTROL Acceso]**: Select `Read only`.

   * Otras opciones no son compatibles

* **[!UICONTROL Permisos adicionales]**: Elija `Request email addresses from users`.

   * Si no se selecciona, el perfil de usuario de AEM no incluirá su dirección de correo electrónico.
   * En las instrucciones de twitter se indican otros pasos que hay que seguir.

La única solicitud REST realizada para el inicio de sesión social es para *[cuenta de GET/verificar credenciales](https://dev.twitter.com/rest/reference/get/account/verify_credentials)*.

### Creación de un Cloud Service de Twitter Connect {#create-a-twitter-connect-cloud-service}

La variable [Adobe Granite OAuth Aplicación y Proveedor](#adobe-granite-oauth-application-and-provider) , creada mediante la creación de una configuración de Cloud Service, identifica la aplicación de Twitter y los grupos de miembros a los que se agregan los nuevos usuarios.

1. En la instancia de autor, inicie sesión con privilegios de administrador.
1. En la navegación global, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de inicio de sesión de twitter Social]**.
1. Elija la **[!UICONTROL ruta de contexto]** configuración.

   La ruta de contexto debe ser la misma que la ruta de configuración de nube que seleccionó al crear o editar un sitio de comunidad.

1. Compruebe si la ruta de contexto está habilitada para crear servicios en la nube debajo de ella.
1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL Explorador de configuración]**. Seleccione el contexto y edite las propiedades. Habilite Configuraciones de nube si aún no está habilitado.

   ![twitterconfigproping](assets/twitterconfigproppng.png)

   * Consulte la documentación del [Explorador de configuración](/help/sites-administering/configurations.md) para obtener más información.

1. Cree/edite la configuración del servicio en la nube de Twitter.

   ![twittersocialloginpng](assets/twittersocialloginpng.png)

   * **[!UICONTROL Título]**

      (*Requerido*) Introduzca un título para mostrar que identifique la aplicación Twitter. Se recomienda utilizar el mismo nombre introducido que la variable *Nombre para mostrar* para la aplicación de Twitter.

   * **[!UICONTROL Clave de consumidor]**

      (*Requerido*) Introduzca la variable **Clave de consumidor (API)** para la aplicación de Twitter. Identifica el [Adobe Granite OAuth Aplicación y Proveedor](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) instancia creada a partir del cuadro de diálogo.

   * **[!UICONTROL Secreto del consumidor]**

      (*Requerido*) Introduzca la variable ***Secreto del consumidor (API)*** para la aplicación de Twitter.

   * **[!UICONTROL Crear usuarios]**

      Si se selecciona, el inicio de sesión con una cuenta de Twitter creará una entrada de usuario AEM y la agregará como miembro a los grupos de usuarios seleccionados. El valor predeterminado está marcado (se recomienda encarecidamente).

   * **[!UICONTROL Enmascarar los ID de usuario]**

      Deje sin seleccionar.

   * **[!UICONTROL Añadir a los grupos de usuarios]**

      Seleccione Agregar grupo de usuarios para elegir uno o varios [grupos de miembros](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) para el sitio de la comunidad al que se agregarán los usuarios.
   >[!NOTE]
   >
   >Los grupos pueden agregarse o eliminarse en cualquier momento. Pero las membresías de los usuarios existentes no se verán afectadas. La pertenencia automática solo se aplica a los nuevos usuarios que se crean después de esta actualización de campo. En Sitios donde los usuarios anónimos están deshabilitados, agregue usuarios al grupo de miembros de la comunidad correspondiente que esté diseñado para ese sitio de comunidad cerrado.

1. Select **[!UICONTROL GUARDAR]** y **[!UICONTROL Publicación]**.

El resultado es un [Adobe Granite OAuth Aplicación y Proveedor](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) que no requiere ninguna modificación. El ámbito predeterminado son los permisos estándar para el inicio de sesión en Twitter.

### Proveedor de OAuth de AEM Communities Twitter {#aem-communities-twitter-oauth-provider}

La configuración de AEM Communities amplía el [Adobe Granite OAuth Aplicación y Proveedor](#adobe-granite-oauth-application-and-provider) instancia. Este proveedor necesitará la edición para permitir actualizaciones del usuario.

Si es necesario editar, en cada instancia de publicación AEM:

1. Inicie sesión con privilegios de administrador.
1. Vaya a la [Consola web](../../help/sites-deploying/configuring-osgi.md).

   Por ejemplo, http://localhost:4503/system/console/configMgr.

1. Busque el proveedor de OAuth de AEM Communities Twitter.
1. Seleccione el icono de lápiz para abrirlo y editarlo.

   ![twitteroauth_png](assets/twitteroauth_png.png)

   * **[!UICONTROL ID de proveedor de OAuth]**

   (*Requerido*) El valor predeterminado es *soco-twitter*. No edite.

   * **[!UICONTROL Configuración del Cloud Service]**

      El valor predeterminado es *conf.* No edite.

   * **[!UICONTROL Configuración del servicio de proveedor de OAuth]**

      El valor predeterminado es `/apps/social/twitterprovider/config/`. No edite.

   * **[!UICONTROL Ruta del usuario]**

      Ubicación en el repositorio donde se almacenan los datos del usuario. Para un sitio de comunidad, para garantizar que los permisos de los miembros para ver el perfil de los demás, la ruta debe ser la predeterminada `/home/users/community`.

   * **[!UICONTROL Habilitar parámetros]** no editar
   * **[!UICONTROL Parámetros de URL]** no editar
   * **[!UICONTROL Actualizar usuario]**

      Si se selecciona, actualiza los datos de usuario en el repositorio en cada inicio de sesión para reflejar los cambios de perfil o los datos adicionales solicitados. Se anula la selección del valor predeterminado.


#### Siguientes pasos {#next-steps-1}

Los siguientes pasos son los mismos para Facebook y Twitter:

* [Publicar las configuraciones del servicio en la nube](#publishcloudservices)
* [Habilitar para un sitio de la comunidad](#enable-social-login)

## Habilitar inicio de sesión social {#enable-social-login}

### Consola AEM Communities Sites {#aem-communities-sites-console}

Una vez configurado un servicio en la nube, puede habilitarse para el ajuste de inicio de sesión social correspondiente para un sitio de la comunidad mediante la variable [Administración de usuarios](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#USERMANAGEMENT) Subpanel Configuración durante el sitio de la comunidad [creación](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#SiteCreation) o [administración](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#ModifyingSiteProperties).

1. Elija el contexto de configuración del sitio donde guardó las configuraciones de inicio de sesión de Social.

1. En la pestaña General , configure las configuraciones de nube.

   ![managesites_png](assets/managesites_png.png)

1. En la ficha Configuración , habilite **[!UICONTROL Inicios de sesión de Social]** y Guardar.

   ![usermgmt_png](assets/usermgmt_png.png)

## Probar inicio de sesión social {#test-social-login}

* Asegúrese [Controlador de autenticación OAuth de Granite de Adobe](#adobe-granite-oauth-authentication-handler) se ha habilitado en todas las instancias de publicación.
* Asegúrese de que se hayan publicado los servicios de nube.
* Asegúrese de que el sitio de la comunidad se haya publicado.
* Inicie el sitio publicado en un explorador.
Por ejemplo, http://localhost:4503/content/sites/engage/en.html
* Select **[!UICONTROL Iniciar sesión]**.
* Seleccione: **[!UICONTROL Iniciar sesión con Facebook]** o **[!UICONTROL Iniciar sesión con Twitter]**.
* Si aún no ha iniciado sesión en Facebook o Twitter, inicie sesión con las credenciales adecuadas.
* Puede ser necesario conceder permiso en función del cuadro de diálogo que muestre la aplicación Facebook o Twitter.
* Observe que la barra de herramientas de la parte superior de la página se actualiza para reflejar el inicio de sesión correcto.
* Select **[!UICONTROL Perfil]**: la página Perfil muestra la imagen de avatar, el nombre y los apellidos del usuario. También muestra la información del perfil de Facebook o Twitter según los campos o parámetros permitidos.

## Configuraciones de AEM Platform OAuth {#aem-platform-oauth-configurations}

### Controlador de autenticación OAuth de Granite de Adobe {#adobe-granite-oauth-authentication-handler}

La variable `Adobe Granite OAuth Authentication Handler` no está activada de forma predeterminada y ***debe estar habilitado en todas AEM instancias de publicación.***

Para habilitar el controlador de autenticación en la publicación, simplemente abra la configuración OSGi y guárdela:

* Inicie sesión con privilegios de administrador.
* Vaya a la [Consola web](../../help/sites-deploying/configuring-osgi.md).
Por ejemplo, http://localhost:4503/system/console/configMgr
* Localizar `Adobe Granite OAuth Authentication Handler`.
* Seleccione para abrir la configuración y editarla.
* Seleccione **[!UICONTROL Guardar]**.

![graniteoauth](assets/graniteoauth.png)

>[!CAUTION]
>
>Tenga cuidado de no confundir el controlador de autenticación con una instancia de Facebook o Twitter de *Adobe Granite OAuth Aplicación y Proveedor*.

![graniteoauth1](assets/graniteoauth1.png)

### Adobe Granite OAuth Aplicación y Proveedor {#adobe-granite-oauth-application-and-provider}

Cuando se crea un servicio en la nube para Facebook o Twitter, se crea una instancia de `Adobe Granite OAuth Authentication Handler` se crea.

Para localizar la instancia creada para una aplicación de Facebook o Twitter:

1. Inicie sesión con privilegios de administrador.
1. Vaya a la [Consola web](../../help/sites-deploying/configuring-osgi.md).

   Por ejemplo, http://localhost:4503/system/console/configMgr.

1. Localice la aplicación y el proveedor de Adobe Granite OAuth.

   * Busque la instancia donde **[!UICONTROL ID de cliente]** coincide con la variable **[!UICONTROL ID de la aplicación]**.

      ![graniteoauth2](assets/graniteoauth2.png)

      Salvo las siguientes propiedades, deje las demás propiedades de la configuración sin modificar:

   * **[!UICONTROL ID de configuración]**

      (*Requerido*) Los ID de configuración de OAuth deben ser únicos. Generado automáticamente cuando se crea el servicio en la nube.

   * **[!UICONTROL ID del cliente]**

      (*Requerido*) ID de aplicación que se proporciona cuando se crea el servicio en la nube.

   * **[!UICONTROL Secreto del cliente]**

      (*Requerido*) El secreto de la aplicación que se proporciona cuando se creó el servicio en la nube.

   * **[!UICONTROL Ámbito]**

      (*Opcional*) Se puede solicitar al proveedor un ámbito adicional para lo que está permitido. El ámbito predeterminado cubre los permisos necesarios para proporcionar autenticación social y datos de perfil.

   * **[!UICONTROL ID del proveedor]**

      (*Requerido*) El ID del proveedor para AEM Communities se establece cuando se creó el servicio en la nube. No edite. Para Facebook Connect, el valor es *soco-facebook*. Para Twitter Connect, el valor es *soco-twitter*.

   * **[!UICONTROL Grupos]**

      (*Recomendado*) Uno o más grupos de miembros a los que se agregan los usuarios creados. Para AEM Communities, se recomienda incluir el grupo de miembros para el sitio de la comunidad.

   * **[!UICONTROL URL de llamada de retorno]**

      (*Opcional*) URL configurada con los proveedores de OAuth para redirigir al cliente de nuevo. Utilice una dirección URL relativa para utilizar el host de la solicitud original. Deje vacío para usar la dirección URL solicitada originalmente. El sufijo &quot;/callback/j_security_check&quot; se anexa automáticamente a esta URL .
   >[!NOTE]
   >
   >El dominio de la rellamada debe estar registrado con el proveedor (Facebook o Twitter).

Para cada configuración del controlador de autenticación de OAuth, hay dos configuraciones adicionales creadas en la instancia:

* Controlador de sincronización predeterminado Apache Jackrabbit Oak (org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler) : no se requieren ediciones allí pero puede ver las asignaciones de campos de usuario cómo se asignan los campos de Facebook a un nodo de perfil de usuario de CQ. Tenga en cuenta también que &quot;Nombre del controlador de sincronización&quot; coincide con el ID de configuración de la configuración del proveedor de OAuth.
* Módulo de inicio de sesión externo Apache Jackrabbit Oak (org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory): no se requieren modificaciones allí, pero puede notar que &#39;Nombre de proveedor de identidad&#39; y &#39;Nombre del controlador de sincronización&#39; son iguales y apuntan a las configuraciones de controlador de sincronización y OAuth correspondientes respectivamente.

Para obtener más información, consulte [Autenticación con el módulo de inicio de sesión externo Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).

## Rendimiento transversal del usuario de OAuth {#oauth-user-traversal-performance}

Para los sitios de la comunidad que ven que cientos de miles de usuarios se registran usando su inicio de sesión en Facebook o Twitter, el rendimiento transversal de la consulta realizada cuando un visitante del sitio utiliza su inicio de sesión social se puede mejorar añadiendo el siguiente índice Oak.

Si se observan advertencias transversales en los registros, se recomienda añadir este índice.

En una instancia de autor, ha iniciado sesión con privilegios administrativos:

1. Desde la navegación global: select **Herramientas, [CRX/DE Lite](../../help/sites-developing/developing-with-crxde-lite.md).**
1. Cree un índice llamado ntBaseLucene-oauth a partir de una copia de ntBaseLucene:

   * Bajo nodo `/oak:index`
   * Seleccionar nodo `ntBaseLucene`
   * Select **[!UICONTROL Copiar]**
   * Seleccione `/oak:index`
   * Select **[!UICONTROL Pegar]**
   * Cambiar el nombre de la copia de ntBaseLucene a `ntBaseLucene-oauth`

1. Modifique las propiedades del nodo ntBaseLucene-oauth:

   * **[!UICONTROL indexPath]**: `/oak:index/ntBaseLucene-oauth`
   * **[!UICONTROL name]**: `oauthid-123****`
   * **[!UICONTROL reindex]**: `true`
   * **[!UICONTROL reindexCount]**: `1`

1. En el nodo /oak:index/ntBaseLucene-oauth/indexRules/nt:base/properties:

   * Elimine todos los nodos secundarios, excepto cqTags.
   * Cambiar el nombre de cqTags a `oauthid-123****`
   * Modificación de las propiedades del nodo `oauthid-123****`

      * **[!UICONTROL name]**: `oauthid-123****`
   * Select **[!UICONTROL Guardar todo]**.


* Para la variable **name** `oauthid-123`, reemplazar *123* con Facebook ***ID de la aplicación*** o Twitter ***Clave de consumidor (API)*** que es el valor de la variable **ID de cliente** en el [Adobe Granite OAuth Aplicación y Proveedor](social-login.md#adobe-granite-oauth-application-and-provider) configuración.

   ![graniteoauth-crxde](assets/graniteoauth-crxde.png)

Para obtener información y herramientas adicionales, consulte [Consultas e indexación de Oak](../../help/sites-deploying/queries-and-indexing.md).

## Configuración de Dispatcher {#dispatcher-configuration}

Consulte [Configuración de Dispatcher para Communities](dispatcher.md).
