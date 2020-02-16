---
title: Inicio de sesión social con Facebook y Twitter
seo-title: Inicio de sesión social con Facebook y Twitter
description: El inicio de sesión en Social permite a los visitantes del sitio iniciar sesión con su cuenta de Facebook o Twitter.
seo-description: El inicio de sesión en Social permite a los visitantes del sitio iniciar sesión con su cuenta de Facebook o Twitter.
uuid: f70e346e-0d8c-41a0-a100-206a420088dc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c0a71870-8f95-40c8-9ffd-b7af49723288
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Inicio de sesión social con Facebook y Twitter {#social-login-with-facebook-and-twitter}

El inicio de sesión en Social es la capacidad para presentar a un visitante del sitio la opción de iniciar sesión con su cuenta de Facebook o Twitter. Por lo tanto, incluya los datos permitidos de Facebook o Twitter en su perfil de miembro de AEM.

![socialloginweretail](assets/socialloginweretail.png)

## Información general de inicio de sesión en Social {#social-login-overview}

Para incluir el inicio de sesión social, *es necesario *crear aplicaciones personalizadas de Facebook y Twitter.

Aunque el ejemplo de venta minorista web proporciona aplicaciones de Facebook y Twitter de muestra y servicios en la nube, no están disponibles en un sitio web [de](../../help/sites-administering/production-ready.md)producción.

Los pasos necesarios son:

1. [Habilite la autenticación](#adobe-granite-oauth-authentication-handler) OAuth en todas las instancias de publicación de AEM.

   Sin OAuth habilitado, los intentos de inicio de sesión fallan.

1. **Cree** una aplicación social y un servicio en la nube.

   * Para admitir el inicio de sesión en Facebook:

      * Cree una aplicación [de](#create-a-facebook-app)Facebook.
      * Cree y publique un servicio [de nube de](#create-a-facebook-connect-cloud-service)Facebook Connect.
   * Para admitir el inicio de sesión en Twitter:

      * Cree una aplicación [de Twitter](#create-a-twitter-app).
      * Cree y publique un servicio [de nube de](#create-a-twitter-connect-cloud-service)Twitter Connect.


1. [**Habilite **el inicio de sesión](#enable-social-login)social para un sitio de comunidad.

Existen dos conceptos básicos:

1. **Ámbito** (permisos) especifica los datos que la aplicación puede solicitar.

   * De forma predeterminada, las instancias de aplicación y proveedor [de](#adobe-granite-oauth-application-and-provider) Adobe Granite OAuth de Facebook y Twitter incluyen los permisos básicos de la aplicación dentro de su ámbito.

1. **Campos** (params) especifica los datos reales solicitados mediante parámetros de URL.

   * Estos campos se especifican en [AEM Communities Facebook OAuth Provider](#aem-communities-facebook-oauth-provider) y [AEM Communities Twitter OAuth Provider](#aem-communities-twitter-oauth-provider).
   * Los campos predeterminados son suficientes para la mayoría de los casos de uso, pero se pueden modificar.

## Inicio de sesión en Facebook {#facebook-login}

### Versión de API de Facebook {#facebook-api-version}

El inicio de sesión social y la muestra de Facebook de venta minorista se desarrollaron cuando la API de gráfico de Facebook era la versión 1.0.
A partir de AEM 6.4 GA y AEM 6.3 SP1, el inicio de sesión social se ha actualizado para que funcione con la versión más reciente de la API de gráficos de Facebook 2.5.

>[!NOTE]
>
>En el caso de versiones anteriores de AEM, si tiene una excepción en los registros **No se puede extraer un token de esto, **actualice a CFP más reciente para esa versión de AEM.

Para obtener información sobre la versión de la API de Facebook Graph, consulte el registro de cambios de la API de [Facebook](https://developers.facebook.com/docs/apps/changelog).

### Crear una aplicación de Facebook {#create-a-facebook-app}

Se requiere una aplicación de Facebook configurada correctamente para habilitar el inicio de sesión social en Facebook.

Para crear una aplicación de Facebook, siga las instrucciones de Facebook en [https://developers.facebook.com/apps/](https://developers.facebook.com/apps/). Los cambios en sus instrucciones no se reflejan en la siguiente información.

En general, desde la API de Facebook v2.7:

* *Agregar una nueva aplicación de Facebook:*
   * Para *plataforma*, elija Sitio web
      * Para la dirección URL ** del sitio, introduzca `  https://<server>:<port>.`
   * En Nombre *para* mostrar, escriba un título para utilizarlo como título del servicio de conexión de Facebook.
   * En *Categoría*, se recomienda elegir *Aplicaciones para páginas,* pero puede ser cualquier cosa.
   * *Agregar producto:  Inicio de sesión en Facebook*
      * Para URI de redireccionamiento *válidos de OAuth*, introduzca `  https://<server>:<port>.`

>[!NOTE]
>
>Para el desarrollo, http://localhost:4503 funcionará.

Una vez creada la aplicación, ubique la configuración de ID **[!UICONTROL de]** aplicación y Secreto de **[!UICONTROL aplicación]** . Esta información es necesaria para configurar el servicio [de nube de](#createafacebookcloudservice)Facebook.

### Creación de un servicio de nube de Facebook Connect {#create-a-facebook-connect-cloud-service}

La instancia de [Adobe Granite OAuth Application and Provider](https://chl-author.corp.adobe.com/content/help/en/experience-manager/6-4/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) , creada mediante la creación de una configuración de servicio en la nube, identifica la aplicación de Facebook y los grupos de miembros a los que se agregan los nuevos usuarios.

1. En la instancia de creación de AEM, inicie sesión con privilegios de administrador.
1. En la navegación global, seleccione **[!UICONTROL Herramientas > Servicios de nube > Configuración]** de inicio de sesión de Facebook Social.
1. Seleccione la ruta de **[!UICONTROL contexto]** de configuración.

   **[!UICONTROL La ruta]** de contexto debe ser la misma que la ruta de configuración de la nube seleccionada al crear o editar un sitio de comunidad.

1. Compruebe si la ruta de contexto está habilitada para crear servicios en la nube debajo de ella.
1. Vaya a **[!UICONTROL Herramientas > General > Navegador]** de configuración. Seleccione el contexto y edite las propiedades. Habilite las configuraciones de nube si aún no están habilitadas.

   ![config-propertiesping](assets/config-propertiespng.png)

1. Crear/editar la configuración del servicio en la nube de Facebook.

   ![fbsocialloginconfigpng](assets/fbsocialloginconfigpng.png)

   * **[!UICONTROL Título]** (*obligatorio*) Escriba un título para mostrar que identifique la aplicación de Facebook. Se recomienda utilizar el mismo nombre introducido que el nombre *para* mostrar de la aplicación de Facebook.
   * **[!UICONTROL ID de aplicación/Clave]** de API (*obligatoria*) Introduzca el ID de ***aplicación*** para la aplicación de Facebook. Identifica la instancia de [Adobe Granite OAuth Application y Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) creada a partir del cuadro de diálogo.
   * **[!UICONTROL Secreto]** de la aplicación (*obligatorio*) Introduzca el secreto de la ***aplicación*** para la aplicación de Facebook.
   * **[!UICONTROL Crear usuarios]** Si está marcado, el inicio de sesión con una cuenta de Facebook creará una entrada de usuario de AEM y la agregará como miembro a los grupos de usuarios seleccionados.  El valor predeterminado está marcado (se recomienda enfáticamente).
   * **[!UICONTROL Enmascarar ID de usuario]**: No se seleccione.
   * **[!UICONTROL Correo electrónico]** del ámbito: la ID de correo electrónico del usuario debe buscarse en Facebook.
   * **[!UICONTROL Agregar a grupos]** de usuarios seleccione Agregar grupo de usuarios para elegir uno o varios grupos [de](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) miembros para el sitio de la comunidad al que se agregarán los usuarios.
   >[!NOTE]
   >
   >Los grupos pueden agregarse o eliminarse en cualquier momento. Sin embargo, las membresías de los usuarios existentes no se verán afectadas. La pertenencia automática solo se aplica a los usuarios nuevos que se crean después de esta actualización de campo. En Sitios donde los usuarios anónimos están deshabilitados, elija agregar usuarios al grupo de miembros de la comunidad correspondiente para ese sitio de comunidad cerrado.

   * Select **[!UICONTROL SAVE]**.
   * **[!UICONTROL Publicación]**.



El resultado es una instancia de [Adobe Granite OAuth Application y Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) que no requiere ninguna modificación adicional a menos que se agregue un ámbito adicional (permisos). El ámbito predeterminado son los permisos estándar para iniciar sesión en Facebook. Si se desea un ámbito adicional, es necesario editar la configuración OSGI directamente. Si se realizan modificaciones directamente a través del sistema o la consola, evite editar las configuraciones del servicio en la nube desde la IU táctil para evitar la sobrescritura.

### Proveedor de OAuth de Facebook de AEM Communities {#aem-communities-facebook-oauth-provider}

El proveedor Comunidades de AEM amplía la aplicación [Adobe Granite OAuth y la instancia de proveedor](#adobe-granite-oauth-application-and-provider) .

Este proveedor necesitará editar para:

* Permitir actualizaciones de usuarios
* Agregar campos adicionales [dentro del ámbito](#adobe-granite-oauth-application-and-provider)

   * De forma predeterminada, no se incluyen todos los campos permitidos.

Si es necesario editar, en cada instancia de publicación de AEM:

1. Inicie sesión con privilegios de administrador.
1. Vaya a la consola [web](../../help/sites-deploying/configuring-osgi.md). Por ejemplo, http://localhost:4503/system/console/configMgr.
1. Localice el proveedor de OAuth de Facebook de AEM Communities.
1. Seleccione el icono del lápiz para abrirlo y editarlo.

   ![fboauthprov_png](assets/fboauthprov_png.png)

   * **[!UICONTROL ID de proveedor de OAuth]**

      (*Requerido*) El valor predeterminado es *soco-facebook*. No edite.

   * **[!UICONTROL Configuración del servicio de nube]**

      El valor predeterminado es */etc/ cloudservices/facebookconnect*. No edite.

   * **[!UICONTROL Configuración del servicio proveedor de OAuth]**

      El valor predeterminado es */apps/social/facebookprovider/config/*. No edite.

   * **[!UICONTROL Habilitar etiquetas]**

      No editar.

   * **[!UICONTROL Ruta del usuario]**

      Ubicación en el repositorio donde se almacenan los datos del usuario. Para que un sitio de comunidad tenga permisos para que los miembros puedan ver el perfil de los demás, la ruta debe ser la ruta predeterminada */inicio/usuarios/comunidad*.

   * **[!UICONTROL Habilitar campos]**

      Si se selecciona, los campos enumerados se especifican en la solicitud a Facebook para la autenticación y la información del usuario. El valor predeterminado no está seleccionado.

   * **[!UICONTROL Fields]**

      Cuando los campos están habilitados, se incluyen los siguientes campos al llamar a la API de gráficos de Facebook. Los campos deben permitirse dentro del ámbito definido en la configuración del servicio en la nube. Los campos adicionales pueden requerir la aprobación de Facebook. Consulte la sección Permisos de inicio de sesión de Facebook de la documentación de Facebook. Los campos predeterminados agregados como parámetros son:

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
   Si se agrega o se cambia algún campo, actualice la configuración del controlador de sincronización predeterminada correspondiente para corregir la asignación.

   * **[!UICONTROL Actualizar usuario]** Si está activado, actualiza los datos de usuario en el repositorio de cada inicio de sesión para reflejar los cambios de perfil o los datos adicionales solicitados. El valor predeterminado no está seleccionado.


#### Próximos pasos {#next-steps}

Los siguientes pasos son los mismos para Facebook y Twitter:

* [Publicar las configuraciones del servicio en la nube](#publishcloudservices)
* [Habilitar para un sitio de comunidad](#enable-social-login)

## Inicio de sesión en Twitter {#twitter-login}

### Crear una aplicación de Twitter {#create-a-twitter-app}

Se requiere una aplicación de Twitter configurada para habilitar el inicio de sesión social en Twitter.

Siga las instrucciones más recientes para crear una nueva aplicación de Twitter en [https://apps.twitter.com](https://apps.twitter.com/).

En general:

1. Introduzca un *nombre* que identifique la aplicación de Twitter con los usuarios del sitio web.
1. Especificar una *Descripción.*
1. Para el *sitio web* , escriba https://&lt;servidor>/.
1. Para la URL *de* llamada de retorno: escriba https://&lt;servidor>/.

   >[!NOTE]
   >
   >No es necesario especificar el puerto.
   >
   >Para el desarrollo, https://127.0.0.1/ funcionará.

1. Una vez creada la aplicación, localice la clave **[!UICONTROL de]** consumidor (API) y el secreto **[!UICONTROL de]** consumidor (API). Esta información será necesaria para configurar el servicio [de nube de](#createatwittercloudservice)Twitter.

#### Permisos {#permissions}

En la sección Permisos de la administración de aplicaciones de Twitter:

* **[!UICONTROL Acceso]**:Seleccione `Read only`.

   * Otras opciones no son compatibles

* **[!UICONTROL Permisos]** adicionales: De forma opcional, elija `Request email addresses from users`.

   * Si no se selecciona, el perfil de usuario en AEM no incluirá su dirección de correo electrónico.
   * Las instrucciones de Twitter indican pasos adicionales que deben seguirse.

La única solicitud de REST que se realiza para iniciar sesión en redes sociales es para *[OBTENER las credenciales](https://dev.twitter.com/rest/reference/get/account/verify_credentials)*de cuenta o verificación.

### Creación de un servicio de nube de Twitter Connect {#create-a-twitter-connect-cloud-service}

La instancia de [Adobe Granite OAuth Application and Provider](#adobe-granite-oauth-application-and-provider) , creada mediante la creación de una configuración de servicio en la nube, identifica la aplicación de Twitter y los grupos de miembros a los que se agregan los nuevos usuarios.

1. En la instancia de autor, inicie sesión con privilegios de administrador.
1. En la navegación global, seleccione **[!UICONTROL Herramientas > Servicios de nube > Configuración]** de inicio de sesión de Twitter Social.
1. Elija la configuración de ruta de acceso **[!UICONTROL de]** contexto.

   La ruta de contexto debe ser la misma que la ruta de configuración de la nube que seleccionó al crear o editar un sitio de comunidad.

1. Compruebe si la ruta de contexto está habilitada para crear servicios en la nube debajo de ella.
1. Vaya a **[!UICONTROL Herramientas > General > Navegador]** de configuración. Seleccione el contexto y edite las propiedades. Habilite las configuraciones de nube si aún no están habilitadas.

   ![twitterconfigproping](assets/twitterconfigproppng.png)

1. Crear/editar la configuración del servicio en la nube de Twitter.

   ![twittersocialloginpng](assets/twittersocialloginpng.png)

   * **[!UICONTROL Título]** (*obligatorio*) Introduzca un título que identifique la aplicación de Twitter. Se recomienda utilizar el mismo nombre introducido que el nombre *para* mostrar para la aplicación de Twitter.

   * **[!UICONTROL Clave]** de consumidor (*obligatoria*) Introduzca la clave **de** consumidor (API) para la aplicación de Twitter. Identifica la instancia de [Adobe Granite OAuth Application y Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) creada a partir del cuadro de diálogo.

   * **[!UICONTROL Secreto]** del consumidor (*obligatorio*) Introduzca el secreto ***de*** consumidor (API) para la aplicación de Twitter.

   * **[!UICONTROL Crear usuarios]** Si está marcado, el inicio de sesión con una cuenta de Twitter creará una entrada de usuario de AEM y la agregará como miembro a los grupos de usuarios seleccionados. El valor predeterminado está marcado (se recomienda enfáticamente).

   * **[!UICONTROL Máscara ID de usuario]** No se ha seleccionado.

   * **[!UICONTROL Agregar a grupos]** de usuarios seleccione Agregar grupo de usuarios para elegir uno o varios grupos [de](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) miembros para el sitio de la comunidad al que se agregarán los usuarios.
   >[!NOTE]
   >
   >Los grupos pueden agregarse o eliminarse en cualquier momento. Pero la pertenencia de los usuarios existentes no se verá afectada. La pertenencia automática solo se aplica a los usuarios nuevos que se crean después de esta actualización de campo. En Sitios donde los usuarios anónimos están deshabilitados, agregue usuarios al grupo de miembros de la comunidad correspondiente que se dirija a ese sitio de comunidad cerrado.

1. Seleccione **[!UICONTROL GUARDAR]** y **[!UICONTROL Publicar]**.

El resultado es una instancia de [Adobe Granite OAuth Application y Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) que no requiere ninguna modificación adicional. El ámbito predeterminado son los permisos estándar para iniciar sesión en Twitter.

### Proveedor de OAuth de AEM Communities Twitter {#aem-communities-twitter-oauth-provider}

La configuración de Comunidades de AEM amplía la aplicación [Adobe Granite OAuth y la instancia de proveedor](#adobe-granite-oauth-application-and-provider) . Este proveedor requerirá de edición para permitir las actualizaciones del usuario.

Si es necesario editar, en cada instancia de publicación de AEM:

1. Inicie sesión con privilegios de administrador.
1. Vaya a la consola [web](../../help/sites-deploying/configuring-osgi.md).

   Por ejemplo, http://localhost:4503/system/console/configMgr.

1. Busque el proveedor de OAuth de Twitter de AEM Communities.
1. Seleccione el icono del lápiz para abrirlo y editarlo.

   ![twitteroauth_png](assets/twitteroauth_png.png)

   * **[!UICONTROL ID]** de proveedor de OAuth (*requerido*)

      El valor predeterminado es *soco-twitter*. No edite.

   * **[!UICONTROL Configuración del servicio de nube]**

      The default value is *conf.* No edite.

   * **[!UICONTROL Configuración del servicio proveedor de OAuth]**

      El valor predeterminado es */apps/social/twitterprovider/config/*. No edite.

   * **[!UICONTROL Ruta del usuario]**

      Ubicación en el repositorio donde se almacenan los datos del usuario. Para que un sitio de comunidad tenga permisos para que los miembros puedan ver el perfil de los demás, la ruta debe ser la ruta predeterminada */inicio/usuarios/comunidad*.

   * **[!UICONTROL Habilitar parámetros]** no edita
   * **[!UICONTROL Los parámetros]** de URL no se editan
   * **[!UICONTROL Actualizar usuario]**

      Si se selecciona, se actualizan los datos de usuario en el repositorio de cada inicio de sesión para reflejar los cambios de perfil o los datos adicionales solicitados. El valor predeterminado no está seleccionado.

#### Próximos pasos {#next-steps-1}

Los siguientes pasos son los mismos para Facebook y Twitter:

* [Publicar las configuraciones del servicio en la nube](#publishcloudservices)
* [Habilitar para un sitio de comunidad](#enable-social-login)

## Habilitar inicio de sesión social {#enable-social-login}

### Consola Sitios de comunidades AEM {#aem-communities-sites-console}

Una vez configurado un servicio en la nube, puede habilitarse para la configuración de inicio de sesión social correspondiente para un sitio de la comunidad mediante el subpanel Configuración de administración [de](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#USERMANAGEMENT) usuarios durante la [creación](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#SiteCreation) o [administración](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#ModifyingSiteProperties)del sitio de la comunidad.

1. Elija el contexto de configuración del sitio en el que guardó las configuraciones de inicio de sesión social.

1. En la ficha General, establezca las configuraciones de nube.

   ![manage_esites_png](assets/managesites_png.png)

1. En la ficha Configuración, habilite Inicios de sesión **[!UICONTROL de]** Social y Guardar.

   ![usermgmt_png](assets/usermgmt_png.png)

## Inicio de sesión en Test Social {#test-social-login}

* Asegúrese de que [Adobe Granite OAuth Authentication Handler](#adobe-granite-oauth-authentication-handler) esté habilitado en todas las instancias de publicación
* Asegúrese de que se han publicado los servicios en la nube
* Asegúrese de que el sitio de la comunidad se haya publicado
* Iniciar el sitio publicado en un navegadorPor ejemplo, http://localhost:4503/content/sites/engage/en.html
* Seleccione **[!UICONTROL Iniciar sesión]**
* Seleccione **[!UICONTROL Iniciar sesión con Facebook]** o **[!UICONTROL Iniciar sesión con Twitter]**
* Si aún no ha iniciado sesión en Facebook o Twitter, inicie sesión con las credenciales correspondientes
* Puede que sea necesario conceder permiso en función del cuadro de diálogo que muestre la aplicación de Facebook o Twitter
* Observe que la barra de herramientas situada en la parte superior de la página se actualiza para reflejar el inicio de sesión correcto
* Seleccionar **[!UICONTROL perfil]**: la página Perfil muestra la imagen de avatar, el nombre y los apellidos del usuario. También muestra la información del perfil de Facebook o Twitter según los campos o parámetros permitidos.

## Configuraciones de AEM Platform OAuth {#aem-platform-oauth-configurations}

### Controlador de autenticación OAuth de Adobe Granite {#adobe-granite-oauth-authentication-handler}

El `Adobe Granite OAuth Authentication Handler` archivo no está habilitado de forma predeterminada y ***debe estar habilitado en todas las instancias de publicación de AEM.***

Para habilitar el controlador de autenticación en la publicación, simplemente abra la configuración OSGi y guárdela:

* Iniciar sesión con privilegios de administrador
* Vaya a la Consola [Web](../../help/sites-deploying/configuring-osgi.md). Por ejemplo: http://localhost:4503/system/console/configMgr
* Localizar `Adobe Granite OAuth Authentication Handler`
* Seleccione esta opción para abrir la configuración y editarla
* Seleccione **[!UICONTROL Guardar]**

![chlimage_1-489](assets/chlimage_1-489.png)

>[!CAUTION]
>
>Tenga cuidado de no confundir el controlador de autenticación con una instancia de Facebook o Twitter de *Adobe Granite OAuth Application and Provider*.

![chlimage_1-490](assets/chlimage_1-490.png)

### Aplicación y proveedor Adobe Granite OAuth {#adobe-granite-oauth-application-and-provider}

Cuando se crea un servicio en la nube para Facebook o Twitter, se crea una instancia de `Adobe Granite OAuth Authentication Handler` .

Para localizar la instancia creada para una aplicación de Facebook o Twitter:

1. Inicie sesión con privilegios de administrador.
1. Vaya a la consola [web](../../help/sites-deploying/configuring-osgi.md).

   Por ejemplo, http://localhost:4503/system/console/configMgr.

1. Busque la aplicación y el proveedor de OAuth de Adobe Granite.

   * Busque la instancia en la que el ID **** de cliente coincide con el ID de **[!UICONTROL aplicación]**
   ![chlimage_1-491](assets/chlimage_1-491.png)

   Salvo las siguientes propiedades, no modifique las demás propiedades de la configuración:

   * **[!UICONTROL Id. de configuración]**

      (*Requerido*) Los ID de configuración de OAuth deben ser únicos. Se genera automáticamente cuando se crea el servicio en la nube.

   * **[!UICONTROL ID del cliente]**

      (*Requerido*) El ID de la aplicación proporcionado cuando se creó el servicio en la nube.

   * **[!UICONTROL Secreto del cliente]**

      (*Requerido*) El secreto de la aplicación proporcionado cuando se creó el servicio en la nube.

   * **[!UICONTROL Ámbito]**

      (*Opcional*) Se puede solicitar al proveedor un ámbito adicional para lo permitido. El ámbito predeterminado cubre los permisos necesarios para proporcionar autenticación social y datos de perfil.

   * **[!UICONTROL ID del proveedor]**

      (*Obligatorio*) El ID de proveedor de AEM Communities se establece al crear el servicio en la nube. No edite. Para Facebook Connect, el valor es *soco-facebook*. Para Twitter Connect, el valor es *soco-twitter*.

   * **[!UICONTROL Grupos]**

      (*Recomendado*) Se agregan uno o varios grupos de miembros a los que se han creado usuarios. Para comunidades AEM, se recomienda incluir el grupo de miembros en el sitio de la comunidad.

   * **[!UICONTROL URL de llamada de retorno]**

      URL (*opcional*) configurada con los proveedores de OAuth para redireccionar al cliente. Utilice una dirección URL relativa para utilizar el host de la solicitud original. Deje vacío para utilizar la dirección URL solicitada originalmente. El sufijo &quot;/callback/j_security_check&quot; se anexa automáticamente a esta dirección URL.
   >[!NOTE]
   >
   >El dominio de la llamada de retorno debe estar registrado en el proveedor (Facebook o Twitter).

Para cada configuración del controlador de autenticación OAuth, hay dos configuraciones adicionales creadas en la instancia:

* Controlador de sincronización predeterminado Apache Jackrabbit Oak (org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler) - No se requieren ediciones allí pero puede ver las asignaciones de campo de usuario cómo se asignan los campos de Facebook a un nodo de perfil de usuario de CQ. También observe que &#39;Nombre del controlador de sincronización&#39; coincide con el identificador de configuración de la configuración del proveedor de OAuth.
* Módulo de inicio de sesión externo Apache Jackrabbit Oak (org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory) - Aquí no se requieren ediciones, pero puede que observe que &#39;Nombre de proveedor de identidad&#39; y &#39;Nombre del controlador de sincronización&#39; son iguales y apuntan a las configuraciones correspondientes de OAuth y controlador de sincronización respectivamente.

Para obtener más información, consulte [Autenticación con el módulo](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)Apache Oak External Login.

## Rendimiento de recorrido del usuario de OAuth {#oauth-user-traversal-performance}

Para los sitios de la comunidad que ven que cientos de miles de usuarios se registran mediante su inicio de sesión en Facebook o Twitter, el rendimiento transversal de la consulta realizada cuando un visitante del sitio utiliza su inicio de sesión social puede mejorarse agregando el siguiente índice Oak.

Si se ven advertencias transversales en los registros, se recomienda agregar este índice.

En una instancia de autor, ha iniciado sesión con privilegios administrativos:

1. Desde la navegación global: seleccione **Herramientas,[CRX/DE Lite](../../help/sites-developing/developing-with-crxde-lite.md).**
1. Cree un índice denominado ntBaseLucene-oauth a partir de una copia de ntBaseLucene:

   * En node /oak:index
   * Seleccionar nodo ntBaseLucene
   * Seleccionar **[!UICONTROL copia]**
   * Seleccione `/oak:index`
   * Seleccionar **[!UICONTROL pegar]**
   * Cambiar el nombre de la copia de ntBaseLucene a ntBaseLucene-oauth

1. Modifique las propiedades del nodo ntBaseLucene-oauth:

   * **[!UICONTROL indexPath]**: /oak:index/ntBaseLucene-oauth
   * **[!UICONTROL name]**: oauthid-123****
   * **[!UICONTROL reindexar]**:true
   * **[!UICONTROL reindexCount]**: 1

1. Bajo el nodo /oak:index/ntBaseLucene-oauth/indexRules/nt:base/properties:

   * Elimine todos los nodos secundarios, excepto cqTags.
   * Cambiar el nombre de cqTags a oauthid-123****
   * Modificar las propiedades del nodo oauthid-123****

      * **[!UICONTROL name]**: oauthid-123****
   * Seleccione **[!UICONTROL Guardar todo]**.


**** &amp;ast; Para el **nombre** oauthid-*123*, reemplace *123* por el ID ***de*** aplicación de Facebook o la clave ***de*** **** [](social-login.md#adobe-granite-oauth-application-and-provider)consumidor de Twitter (API) que es el valor del ID de cliente en la configuración de la aplicación de Granite OAuth y la aplicación de Providerite.

![chlimage_1-492](assets/chlimage_1-492.png)

Para obtener información y herramientas adicionales, consulte [Consulta de Oak e Indexación](../../help/sites-deploying/queries-and-indexing.md).

## Dispatcher Configuration {#dispatcher-configuration}

Consulte [Configuración de Dispatcher para Comunidades](dispatcher.md).
