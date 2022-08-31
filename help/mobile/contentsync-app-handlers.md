---
title: Controladores de aplicación predeterminados
seo-title: Out of the Box App Handlers
description: Siga esta página para obtener más información sobre los controladores predeterminados para Adobe PhoneGap Enterprise con AEM.
seo-description: Follow this page to learn about the out-of-the-box handlers for Adobe PhoneGap Enterprise with AEM.
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 0%

---

# Controladores de aplicación predeterminados{#out-of-the-box-app-handlers}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Consulte las siguientes directrices para el desarrollo de los controladores de sincronización de contenido:

* Los controladores deben implementar *com.day.cq.contentsync.handler.ContentUpdateHandler* (directamente o extendiendo una clase que lo haga)
* Los controladores pueden ampliar *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* El controlador solo debe informar de verdadero si ha actualizado la caché de ContentSync. Si se informa erróneamente de true , AEM crear una actualización.
* El controlador solo debe actualizar la caché si el contenido ha cambiado. No escriba en la caché si no es necesario un blanco y evite una creación de actualización innecesaria.

## Controladores fuera de la caja {#out-of-the-box-handlers}

A continuación se enumeran los controladores de aplicaciones predeterminados:

**mobileapppages** Procesa las páginas de la aplicación.

* ***type - String*** - mobileapppages
* ***path - String*** : ruta a una página
* ***extensión - Cadena*** : Extensión que debe utilizarse en la solicitud. Para las páginas esto casi siempre *html*, pero otras aún son posibles.

* ***selector - Cadena*** : selectores opcionales separados por puntos. Los ejemplos comunes son *touch* para procesar versiones móviles de una página.

* ***deep - Boolean*** - Propiedad booleana opcional que determina si también se deben incluir páginas secundarias. El valor predeterminado es *true.*

* ***includeImages - Boolean*** - Propiedad booleana opcional que determina si se deben incluir imágenes. El valor predeterminado es *true*.

   * De forma predeterminada, solo se tienen en cuenta para la inclusión los componentes de imagen con un tipo de recurso de base/componentes/imagen.

* ***includeVideos - Boolean*** - Propiedad booleana opcional que determina si se deben incluir los vídeos. El valor predeterminado es *true*.

* ***includeModifiedPagesOnly - Boolean*** - Si es false o se omite, procese todas las páginas y compruebe las actualizaciones en la renderización. Si es true, la base difiere de los cambios realizados en una página lastModified.
* ***+ reescribir (nodo)***
   ***- relationParentPath - String*** - la ruta para escribir todas las demás rutas relativas a.

>[!NOTE]
>
>El tipo de recurso de los componentes de imagen y vídeo afectados por este controlador se establece configurando las propiedades de la variable *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*Servicio MobilePagesUpdateHandler OSGi*.

**mobilepageassets** Recopila recursos de la página de la aplicación.

**mobilecontentlisting** Muestra el contenido del zip de ContentSync. Esto lo utilizan los js del lado del cliente en el dispositivo para realizar la copia de archivo inicial necesaria para AEM aplicaciones.

Este controlador debe agregarse a cualquier configuración de ContentSync de aplicaciones AEM.

* ***type - String - mobilecontentlisting***
* ***ruta*** - Cadena : manténgase vacío, debe estar presente para que se vea como un controlador válido, pero la ruta se infiere que es la caché actual de ContentSync. Se ignora este valor.
* ***targetRootDirectory* -**String : el prefijo que se agregará a las rutas como raíz de destino para la actualización de contenido de este controlador.
* ***order - Long* -**Solicite que ContentSync ejecute este controlador. Este número debe establecerse más alto que todos los demás controladores, como 100. Debe ejecutarse después de los controladores de contenido tradicionales.

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

**mobilecontentpackageslisting** Enumera el paquete de contenido AEM en una aplicación determinada, así como la URL del servidor a la que realizar solicitudes de actualización. Se utiliza el js del lado del cliente en el dispositivo para solicitar actualizaciones de contenido

El controlador debe usarse en AEM configuración de ContentSync de App Shell (nodo con page-type=app-instance)

* ***type - String - mobilecontentpackageslisting***
* ***ruta **-**Cadena*** : Ruta a un shell de aplicación (nodo con page-type=app-instance).
* ***targetRootDirectory - String*** - el prefijo que se agregará a las rutas como raíz de destino para la actualización de contenido para este controlador.
* ***order - Long* -**Ordene que ContentSync ejecute este controlador. Este número debe establecerse más alto que todos los demás controladores, como 100. Debe ejecutarse después de los controladores de contenido tradicionales.

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

**widgetconfig** Incluye un archivo config.xml actualizado que combina cualquier edición realizada mediante el Centro de comandos con un archivo config.xml proporcionado. Si no se incluye este controlador, los detalles de la aplicación que se modifiquen a través de la interfaz de administración no se incluirán en la caché.

Este controlador debe usarse en una configuración de ContentSync de App Shell AEM (nodo con page-type=[app-instance]).

* ***type - String* - **widgetconfig
* ***ruta **-**Cadena*** - Ruta a cualquier nodo secundario del shell de la aplicación (nodo con page-type=[app-instance]).
* ***targetRootDirectory - String*** - el prefijo que se agregará a las rutas como raíz de destino para la actualización de contenido para este controlador.
* ***targetIconDirectory - String*** : el directorio para colocar los iconos de la aplicación.

**mobileADBMobileConfigJSON** Incluya el archivo ADBMobileConfig.JSON si se ha configurado el servicio de nube AMS.

Esto se utiliza en el tiempo de compilación para configurar el complemento de AMS para la compatibilidad con Analytics.

El controlador debe usarse en AEM configuración de ContentSync de App Shell (nodo con page-type=app-instance)

* ***type - String*** - mobileADBMobileConfigJSON
* ***path - String*** : Ruta a un shell de aplicación (nodo con page-type=app-instance o RT que extiende /libs/mobileapps/core/components/instance)
* ***targetRootDirectory - String*** - el prefijo que se agregará a las rutas como raíz de destino para la actualización de contenido para este controlador

**notificationsconfig** Extrae las configuraciones de notificaciones necesarias en el dispositivo. Las propiedades se extraen de la configuración de servicio en la nube correspondiente del servicio push asociado a la aplicación.

Las propiedades que no son de AEM en el nodo jcr:content del servicio de nube se extraen y se añaden al **page-notifications-config.json** Archivo JSON para su inclusión en la raíz www del contenido de la aplicación.

AEM propiedades son aquellas que tienen un espacio entre nombres con &quot;cq&quot;, &quot;sling&quot; o &quot;jcr&quot;. Se pueden excluir otras propiedades con la propiedad &quot;excludeProperties&quot; en el nodo de configuración content-sync.

* ***type - String*** - notificationsconfig
* ***excludeProperties - String[]*** - propiedades que se van a excluir

**contentsyncconfigcontent** Recopila contenido de una configuración de ContentSync existente.

* ***type - String*** - contentsyncconfigcontent
* ***path - String*** - Ruta a uno de:

   * otra configuración de ContentSync
   * a un paquete de contenido (se utilizará su propiedad phonegap-exportTemplate para encontrar su configuración ContentSync)
   * a un recurso móvil (el contenido de la aplicación se encontrará en ese recurso y, si esos paquetes de contenido tienen una propiedad page-includeInBuild que es verdadera, phonegap-exportTemplate se utilizará para encontrar su configuración de ContentSync)

* ***autoCreateFirstUpdateBeforeImport - Booleano*** - si es true, cree un **actualizar** en la configuración de target antes de importar si una vez no existe

* ***autoFillBeforeImport - Booleano*** - si es true, actualice/rellene la configuración de destino antes de importar
* ***configSuffix - String*** : una cadena que se anexará a la ruta indicada en la propiedad phonegap-exportTemplate del contenido de la aplicación. Se puede utilizar para distinguir distintas plantillas de exportación. Por ejemplo, esta propiedad se puede establecer en **&quot;-dev&quot;** para indicar que *&quot;/../../../appconfig-dev&quot;* debe usarse (en lugar de *&quot;/../../../appconfig&quot;*).

**app-assets** Incluye todos los recursos asociados a una instancia de aplicación. Este controlador incluirá todos los recursos que se encuentren en la ruta especificada junto con los recursos a los que haga referencia la propiedad appAssetPath de una instancia de aplicación.

* ***type - String*** - app-assets

* ***ruta **-**Cadena*** : ruta a una ubicación en una instancia de aplicación en la que se almacenan los recursos de la aplicación

**mobileappoffers** Se ha introducido un nuevo controlador de sincronización de contenido para que el caso de uso Personalización represente el contenido de destino. El controlador &quot;mobileappoffers&quot; sabe cómo procesar las ofertas de destino asociadas que ha creado el autor del contenido. El controlador mobileappoffers extiende el controlador de actualización de páginas abstractas, por lo que muchas de las propiedades son similares. Los detalles del controlador mobileappoffers tienen las siguientes propiedades.

El controlador mobileappsoffers extiende el controlador mobileappspages y agrega las siguientes propiedades:

* ***locationRoot - String*** - especifique la ubicación de la aplicación móvil
* ***includePageTypes - String*** : los valores predeterminados admiten cq/personalization/components/teaserpage y cq/personalization/components/offer proxy
* ***selector - Cadena*** - se debe configurar en tandy
* ***path - String***- la ruta a la marca de la campaña

**mobileappconfig** El controlador de sincronización de contenido mobileappconfig proporciona una forma de insertar datos JSON en MobileAppsConfig.json. Para registrar una clase de proveedor, los desarrolladores agregarán su clase MobileAppsInfoProvider con la lista de proveedores. El controlador se iterará sobre la lista de MobileAppsInfoProviders y permitirá que el proveedor inserte datos en el archivo json resultante. La lista de propiedades que admite este controlador es:

* ***ruta **-**Cadena*** : la ruta a un nodo de instancia de aplicación con page-type=app-instance o un RT que extiende /libs/mobileapps/core/components/instance
* ***proveedores - Cadena*** `[]` - la lista de MobileAppsInfoProviders totalmente cualificados
* ***targetRootDirectory - String*** : el directorio en el que se debe escribir el archivo MobileAppsConfig.json.
* **fileName - String** : nombre opcional del archivo al que se va a escribir el JSON, el valor predeterminado es MobileAppsConfig.json

Es posible tener varios controladores mobileappconfig configurados cada uno con un conjunto único de proveedores escribiendo en diferentes archivos JSON.

### Prueba de los controladores de sincronización de contenido {#testing-content-sync-handlers}

**Pasos para comprobar la integridad** Borrar caché

* Borrar caché
* Ejecute el controlador (caché actualizada)
* Ejecute el controlador de nuevo (la caché no debe actualizarse)

**Pasos para la depuración**

* Ejecutar su configuración
* Exportar la configuración o la revisión en el dispositivo
* Si la renderización falla, compruebe si falta *estilos/recursos/bibliotecas* o compruebe si hay rutas incorrectas para *estilos/recursos/bibliotecas*

**Registro** Habilitar el registro de depuración de ContentSync mediante las configuraciones del registrador OSGI en el paquete `com.day.cq.contentsync` Esto le permitirá rastrear qué controladores se ejecutaron y si actualizaron la caché y notificaron haber actualizado la caché.

## Recursos adicionales {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y desarrollador, consulte los siguientes recursos:

* [Creación para Adobe PhoneGap Enterprise con AEM](/help/mobile/phonegap.md)
* [Administración de contenido para Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>Para comenzar con el desarrollo de aplicaciones de AEM Mobile, haga clic en [here](/help/mobile/getting-started-aem-mobile.md).
