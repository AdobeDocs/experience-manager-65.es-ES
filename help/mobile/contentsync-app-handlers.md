---
title: Controladores de aplicaciones predeterminados
seo-title: Controladores de aplicaciones predeterminados
description: Siga esta página para conocer los controladores predeterminados para Adobe PhoneGap Enterprise con AEM.
seo-description: Siga esta página para conocer los controladores predeterminados para Adobe PhoneGap Enterprise con AEM.
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Controladores de aplicaciones predeterminados{#out-of-the-box-app-handlers}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Consulte las siguientes directrices para desarrollar controladores de sincronización de contenido:

* Los controladores deben implementar *com.day.cq.contentsync.handler.ContentUpdateHandler* (ya sea directamente o extendiendo una clase que lo haga)
* Los controladores pueden ampliar *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* El controlador solo debe informar de verdadero si ha actualizado la caché de ContentSync. La creación de informes falsos de verdadero permitirá a AEM crear una actualización.
* El controlador solo debe actualizar la caché si el contenido ha cambiado. No escriba en la caché si no es necesario un blanco y evite una creación de actualización innecesaria.

## Controladores listos para usar {#out-of-the-box-handlers}

En la lista siguiente se muestran los controladores de aplicaciones integrados:

**mobileapppages** procesa páginas de aplicación.

* ***type - Cadena*** - mobileapppages
* ***path - String*** - ruta a una página
* ***extension - Cadena*** - Extensión que debe utilizarse en la solicitud. Para las páginas esto es casi siempre *html*, pero otras son aún posibles.

* ***selector - Cadena*** - Selectores opcionales separados por puntos. Los ejemplos habituales son *táctiles* para procesar versiones móviles de una página.

* ***deep - Boolean*** - Propiedad booleana opcional que determina si también se deben incluir páginas secundarias. The default value is *true.*

* ***includeImages - Boolean*** - Propiedad booleana opcional que determina si se deben incluir imágenes. The default value is *true*.

   * De forma predeterminada, solo se consideran para la inclusión los componentes de imagen con un tipo de recurso de base/componentes/imagen.

* ***includeVideos - Boolean*** - Propiedad booleana opcional que determina si se deben incluir vídeos. The default value is *true*.

* ***includeModifiedPagesOnly - Boolean*** - Si es false o se omite, procese todas las páginas y compruebe las actualizaciones en el procesamiento. Si el valor es true, la base difiere de los cambios realizados en las páginas lastModified.
* ***+ reescribir (nodo)***
   ***- relativeParentPath - String*** - la ruta para escribir todas las demás rutas relativas a.

>[!NOTE]
>
>El tipo de recurso de los componentes de imagen y vídeo afectados por este controlador se establece configurando las propiedades de *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*Servicio* MobilePagesUpdateHandler OSGi.

**mobilepageassets** recopila recursos de la página de la aplicación.

**mobilecontentlist** Muestra el contenido del zip de ContentSync. Esto lo utilizan los js del lado del cliente en el dispositivo para realizar la copia de archivo inicial necesaria para las aplicaciones de AEM.

Este controlador debe agregarse a cualquier configuración de ContentSync de aplicaciones de AEM.

* ***type - String - mobilecontentlist***
* ***path*** - String: mantener vacío, debe estar presente para ser visto como un controlador válido, pero la ruta se deduce que es la caché de ContentSync actual. Este valor se omite.
* ***targetRootDirectory *-**String: el prefijo que se agrega a las rutas como raíz de destino para la actualización de contenido para este controlador.
* ***order - Long *-**Order for ContentSync para ejecutar este controlador. Este número debe configurarse más alto que todos los demás controladores, como 100. Debe ejecutarse después de los controladores de contenido tradicionales.

```xml
{
  "files": [
    "config.xml",
    "res/screens/ios/screen-ipad-portrait-2x.png",
    "res/screens/ios/screen-ipad-landscape.png",
    "res/screens/ios/screen-iphone-portrait-2x.png",
    "res/screens/ios/screen-iphone-landscape.png",
    "res/screens/ios/screen-iphone-portrait.png",
    "apps/weretail-app/components/splash-page/clientlibs.css",
    ...
    "pge-content-packages.json"
  ],
  "count": 382,
  "lastModified": 1422902754733
}
```

**mobilecontentpackageslist** Muestra el paquete de contenido de AEM en una aplicación determinada, así como la URL del servidor a la que se van a realizar las solicitudes de actualización. Se utiliza Js del lado del cliente en el dispositivo para solicitar actualizaciones de contenido

El controlador se debe usar en la configuración ContentSync de la shell de la aplicación AEM (nodo con page-type=app-instance)

* ***type - String - mobilecontentpackageslist***
* ***path **-**String*** - Ruta a un shell de aplicación (nodo con page-type=app-instance).
* ***targetRootDirectory - String*** - el prefijo que se agrega a las rutas como raíz de destino para la actualización de contenido para este controlador.
* ***order - Long *-**Ordenar que ContentSync ejecute este controlador. Este número debe configurarse más alto que todos los demás controladores, como 100. Debe ejecutarse después de los controladores de contenido tradicionales.

>[!NOTE]
>
>El siguiente bloque de código no es una implementación exacta y debe utilizarse como ejemplo de referencia:

```xml
{
  "content": [
    {
      "name": "en",
      "title": "We Retail Mobile App - English",
      "type": "CONTENT",
      "path": "/content/phonegap/weretail-outdoors/en",
      "updatePath": "/content/phonegap/weretail/en/jcr:content/pge-app/app-config"
    },
    {
      "name": "shell",
      "title": "We Retail Mobile App",
      "type": "INSTANCE",
      "path": "/content/phonegap/weretail-outdoors/shell",
      "updatePath": "/content/phonegap/weretail/shell/jcr:content/pge-app/app-config"
    }
  ],
  "serverURL": "http://localhost:4503/"
}
```

**widgetconfig** Incluye un archivo config.xml actualizado que combina cualquier edición realizada mediante el Centro de comandos con un archivo config.xml proporcionado. Si este controlador no se incluye, los detalles de la aplicación que se cambien mediante la interfaz de administración no se incluirán en la caché.

Este controlador debe utilizarse en una configuración ContentSync de shell de aplicaciones de AEM (nodo con page-type=[app-instance]).

* ***type - String* - **widgetconfig
* ***path **-**String*** - Ruta a cualquier nodo secundario del shell de la aplicación (nodo con page-type=[app-instance]).
* ***targetRootDirectory - String*** - el prefijo que se agrega a las rutas como raíz de destino para la actualización de contenido para este controlador.
* ***targetIconDirectory - String*** - el directorio en el que se colocan los iconos de la aplicación

**mobileADBMobileConfigJSON** Incluya el archivo ADBMobileConfig.JSON si se ha configurado el servicio de nube AMS.

Esto se utiliza en tiempo de compilación para configurar el complemento AMS para la compatibilidad analítica.

El controlador se debe usar en la configuración ContentSync de la shell de la aplicación AEM (nodo con page-type=app-instance)

* ***type - String*** - mobileADBMobileConfigJSON
* ***path - String*** - Ruta a un shell de aplicación (nodo con page-type=app-instance o RT que extiende /libs/mobileapps/core/components/instance)
* ***targetRootDirectory - String*** - el prefijo que se agrega a las rutas como raíz de destino para la actualización de contenido para este controlador

**notificacionesconfig** Extrae las configuraciones de notificaciones necesarias en el dispositivo. Las propiedades se extraen de la configuración del servicio de nube del servicio push correspondiente asociada a la aplicación.

Las propiedades que no son de AEM en el nodo jcr:content del servicio de nube se extraen y añaden al archivo JSON **page-notifications-config.json** para incluirlas en la raíz www del contenido de la aplicación.

Las propiedades de AEM son aquéllas que llevan el nombre &quot;cq&quot;, &quot;sling&quot; o &quot;jcr&quot;. Se pueden excluir otras propiedades mediante la propiedad &quot;excludeProperties&quot; en el nodo de configuración content-sync.

* ***type - String*** - notificationconfig
* ***excludeProperties - String[]*** - propiedades que se van a excluir

**contentsyncconfigcontent** Recopila contenido de una configuración ContentSync existente.

* ***type - String*** - contentsyncconfigcontent
* ***path - String*** - Ruta a uno de los siguientes:

   * otra configuración de ContentSync
   * a un paquete de contenido (utilizará su propiedad phonegap-exportTemplate para encontrar su configuración de ContentSync)
   * a un recurso móvil (app-content se encontrará en ese recurso y, si esos paquetes de contenido tienen una propiedad page-includeInBuild que es true, se utilizará phonegap-exportTemplate para encontrar su configuración de ContentSync)

* ***autoCreateFirstUpdateBeforeImport - Booleano*** - si es true, cree una **actualización** inicial en la configuración de destino antes de importar si una vez no existe ya

* ***autoFillBeforeImport - Boolean*** - si es true, actualice/rellene la configuración de destino antes de importar
* ***configSuffix - Cadena*** : cadena que se anexa a la ruta indicada en la propiedad &quot;phonegap-exportTemplate&quot; de app-content. Esto se puede utilizar para distinguir diferentes plantillas de exportación. Por ejemplo, esta propiedad se puede establecer en **&quot;-dev&quot;** para indicar que *&quot;/.../../../appconfig-dev&quot;* se debe utilizar (en oposición a *&quot;/../../.../appconfig&quot;*).

**app-assets** Incluye todos los recursos asociados a una instancia de aplicación. Este controlador incluirá todos los recursos encontrados en la ruta especificada junto con los recursos a los que hace referencia la propiedad appAssetPath de una instancia de aplicación.

* ***type - Cadena*** - app-assets

* ***path **-**String*** - ruta a una ubicación en una instancia de aplicación donde se almacenan los recursos de la aplicación

**mobileappoffers** Se ha introducido un nuevo controlador de sincronización de contenido para el caso de uso Personalización para procesar el contenido de destino. El controlador &#39;mobileappoffers&#39; sabe cómo procesar las ofertas de destino asociadas que ha creado el autor del contenido. El controlador mobileappoffers extiende el controlador de actualización de páginas abstractas, por lo que muchas de las propiedades son similares. Los detalles del controlador mobileappoffers tienen las siguientes propiedades.

El controlador mobileappsoffers extiende el controlador mobileappspages y agrega las siguientes propiedades:

* ***locationRoot - String*** - especifique la ubicación de la aplicación móvil
* ***includePageTypes - String*** - valor predeterminado que admite cq/personalization/components/teaserpage y cq/personalization/components/offer proxy
* ***selector - Cadena*** - debe configurarse en tandt
* ***path - String***- la ruta a la marca de la campaña

**mobileappconfig** El controlador de sincronización de contenido mobileappconfig proporciona una forma de insertar datos JSON en MobileAppsConfig.json. Para registrar una clase de proveedor, los desarrolladores agregarán su clase MobileAppsInfoProvider con la lista de proveedores. El controlador repetirá la lista de MobileAppsInfoProviders y permitirá que el proveedor introduzca datos en el archivo json resultante. La lista de propiedades admitidas por este controlador son:

* ***path **-**String*** - la ruta a un nodo de instancia de aplicación con page-type=app-instance o un RT que extiende /libs/mobileapps/core/components/instance
* ***proveedores - Cadena*** - `[]` lista de MobileAppsInfoProviders totalmente cualificados
* ***targetRootDirectory - String*** - directorio en el que se escribe el archivo MobileAppsConfig.json.
* **fileName - Cadena** - nombre opcional del archivo al que se va a escribir el JSON, el valor predeterminado es MobileAppsConfig.json

Es posible tener varios controladores mobileappconfig configurados cada uno con un conjunto único de proveedores que escriben en diferentes archivos JSON.

### Prueba de los controladores de sincronización de contenido {#testing-content-sync-handlers}

**Pasos para comprobar la integridad** : borrar la caché

* Borrar caché
* Ejecutar el controlador (caché actualizada)
* Volver a ejecutar el controlador (no se debe actualizar la caché)

**Pasos para la depuración**

* Ejecutar la configuración
* Exportar la configuración o la revisión en el dispositivo
* Si el procesamiento falla, compruebe si faltan *estilos/recursos/bibliotecas* o si hay rutas incorrectas a *estilos/recursos/bibliotecas*

**Registro** Habilitar el registro de depuración de ContentSync a través de las configuraciones del registrador OSGI en el paquete `com.day.cq.contentsync` Esto le permitirá rastrear qué controladores se ejecutaron y si actualizaron la caché e informaron de la actualización de la misma.

## Additional Resources {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y un desarrollador, consulte los siguientes recursos:

* [Creación para Adobe PhoneGap Enterprise con AEM](/help/mobile/phonegap.md)
* [Administración de contenido para Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>Para empezar a desarrollar aplicaciones de AEM Mobile, haga clic [aquí](/help/mobile/getting-started-aem-mobile.md).

