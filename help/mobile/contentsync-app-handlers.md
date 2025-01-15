---
title: Controladores de aplicaciones listos para usar
description: Siga esta página para obtener más información sobre los controladores predeterminados para Adobe PhoneGap AEM Enterprise con el servicio de soporte de la aplicación de la interfaz de usuario de Adobe.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 0%

---

# Controladores de aplicaciones listos para usar{#out-of-the-box-app-handlers}

{{ue-over-mobile}}

Consulte las siguientes directrices para desarrollar controladores de sincronización de contenido:

* Los controladores deben implementar *com.day.cq.contentsync.handler.ContentUpdateHandler* (ya sea directamente o ampliando una clase que sí lo haga)
* Los controladores pueden extender *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* El controlador solo debe informar de true si ha actualizado la caché de ContentSync. AEM Informar de forma incorrecta sobre true permitirá crear una actualización de forma.
* El controlador solo debe actualizar la caché si el contenido ha cambiado. No escriba en la caché si no es necesario un espacio en blanco y evite la creación de actualizaciones innecesarias.

## Controladores predeterminados {#out-of-the-box-handlers}

A continuación se enumeran los controladores de aplicación predeterminados:

**mobileapppages** procesa páginas de aplicaciones.

* ***type - String*** - mobileapppages
* ***ruta de acceso - Cadena*** - ruta de acceso a una página
* ***extensión - Cadena*** - Extensión que debe usarse en la solicitud. Para las páginas, esto es casi siempre *html*, pero otros son posibles.

* ***selector - Cadena*** - Selectores opcionales separados por punto. Algunos ejemplos comunes son *touch* para procesar versiones móviles de una página.

* ***deep - Boolean*** - Propiedad booleana opcional que determina si también se deben incluir las páginas secundarias. El valor predeterminado es *true.*

* ***includeImages - Boolean*** - Propiedad booleana opcional que determina si se deben incluir las imágenes. El valor predeterminado es *true*.

   * De forma predeterminada, solo se tienen en cuenta para la inclusión los componentes de imagen con un tipo de recurso de foundation/components/image.

* ***includeVideos - Boolean*** - Propiedad booleana opcional para determinar si los vídeos deben incluirse. El valor predeterminado es *true*.

* ***includeModifiedPagesOnly - Boolean*** - Si es false o se omite, procese todas las páginas y compruebe las actualizaciones en el procesamiento. Si el valor es True, la base difiere en los cambios realizados en una página lastModified.
* ***+ reescribir (nodo)***
  ***- relativeParentPath - String*** - la ruta de acceso para escribir todas las demás rutas de acceso relativas a.

>[!NOTE]
>
>El tipo de recurso de los componentes de imagen y vídeo afectados por este controlador se establece configurando las propiedades de *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*Servicio OSGi de MobilePagesUpdateHandler*.

**mobilepageassets** recopila recursos de página de la aplicación.

**mobilecontentlisting** enumera el contenido del archivo zip de ContentSync. AEM Lo utiliza el js del lado del cliente en el dispositivo para realizar la copia inicial del archivo necesaria para las aplicaciones de la aplicación de la aplicación de.

AEM Este controlador debe agregarse a cualquier configuración de ContentSync de aplicaciones de la aplicación de la aplicación.

* ***type - String - mobilecontentlisting***
* ***ruta*** - Cadena - mantener vacío, debe estar presente para que se vea como un controlador válido, pero se infiere que la ruta es la caché de ContentSync actual. Este valor se ignora.
* ***targetRootDirectory* -**String: el prefijo que se agregará a las rutas como raíz de destino para la actualización de contenido de este controlador.
* ***pedido - Largo* -**Pedido para que ContentSync ejecute este controlador. Este número debe establecerse por encima de todos los demás controladores, como 100. Debe ejecutarse después de los controladores de contenido tradicionales.

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

AEM **mobilecontentpackageslisting** Enumera el paquete de contenido de la aplicación en cuestión y la URL del servidor en la que se van a realizar las solicitudes de actualización. Se utiliza en el lado del cliente js en el dispositivo para solicitar actualizaciones de contenido

AEM El controlador debe usarse en la configuración de ContentSync de App Shell (nodo con page-type=app-instance)

* ***type - String - mobilecontentpackageslisting***
* ***ruta **-**Cadena*** - Ruta a un shell de aplicación (nodo con pge-type=app-instance).
* ***targetRootDirectory - String*** - el prefijo que se agrega a las rutas como raíz de destino para la actualización de contenido de este controlador.
* ***order - Long* -**Order para que ContentSync ejecute este controlador. Este número debe establecerse por encima de todos los demás controladores, como 100. Debe ejecutarse después de los controladores de contenido tradicionales.

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

**widgetconfig** incluye un config.xml actualizado que combina las ediciones realizadas a través del Centro de comandos con un config.xml proporcionado. Si no se incluye este controlador, los detalles de la aplicación que se cambien a través de la interfaz de administración no se incluirán en la caché.

AEM Este controlador debe usarse en una configuración de ContentSync de App Shell de la aplicación (nodo con page-type=[app-instance]).

* ***type - String* - **widgetconfig
* ***ruta **-**Cadena*** - Ruta a cualquier nodo secundario del shell de la aplicación (nodo con tipo de página=[instancia de aplicación]).
* ***targetRootDirectory - String*** - el prefijo que se agrega a las rutas como raíz de destino para la actualización de contenido de este controlador.
* ***targetIconDirectory - String*** - el directorio donde colocar los iconos de la aplicación

**mobileADBMobileConfigJSON** Incluya el archivo ADBMobileConfig.JSON si se configuró el servicio en la nube de AMS.

Se utiliza en tiempo de compilación para configurar el complemento AMS para la compatibilidad con análisis.

AEM El controlador debe usarse en la configuración de ContentSync de App Shell (nodo con page-type=app-instance)

* ***type - String*** - mobileADBMobileConfigJSON
* ***ruta - Cadena*** - Ruta a un shell de aplicación (nodo con tipo de página=instancia de aplicación o RT que amplía /libs/mobileapps/core/components/instance)
* ***targetRootDirectory - String*** - el prefijo que se agregará a las rutas como raíz de destino para la actualización de contenido de este controlador

**notificationsconfig** Extrae las configuraciones de notificaciones requeridas en el dispositivo. Las propiedades se extraen de la configuración respectiva del servicio en la nube de servicios push asociado a la aplicación.

AEM Las propiedades que no son de la nube en el nodo jcr:content del servicio se extraen y se agregan al archivo JSON **pge-notifications-config.json** para su inclusión en la raíz www del contenido de la aplicación.

AEM Las propiedades de son aquellas que se espacian con nombres como &quot;cq&quot;, &quot;sling&quot; o &quot;jcr&quot;. Otras propiedades se pueden excluir mediante la propiedad excludeProperties en el nodo de configuración de sincronización de contenido.

* ***type - String*** - notificationsconfig
* ***excludeProperties - String[]*** - propiedades que se van a excluir

**contentsyncconfigcontent** recopila contenido de una configuración ContentSync existente.

* ***type - String*** - contentsyncconfigcontent
* ***ruta de acceso - Cadena*** - Ruta de acceso a uno de:

   * otra configuración de ContentSync
   * a un paquete de contenido (se utilizará su propiedad phonegap-exportTemplate para encontrar su configuración ContentSync)
   * a un recurso móvil (los de app-content se encuentran debajo de ese recurso y, si esos paquetes de contenido tienen una propiedad page-includeInBuild que es true, se utiliza phonegap-exportTemplate para encontrar su configuración de ContentSync)

* ***autoCreateFirstUpdateBeforeImport - Boolean*** - si es true, cree una **actualización** inicial en la configuración de destino antes de importar si una vez no existe ya

* ***autoFillBeforeImport - Boolean*** - si es true, actualice/rellene la configuración de destino antes de importar
* ***configSuffix - String*** - una cadena que se anexará a la ruta indicada en la propiedad &quot;phonegap-exportTemplate&quot; de app-content. Esto se puede utilizar para distinguir diferentes plantillas de exportación. Por ejemplo, esta propiedad se puede establecer en **&quot;-dev&quot;** para indicar que se debe usar *&quot;/../../appconfig-dev&quot;* (en oposición a *&quot;/../../../appconfig&quot;*).

**app-assets** incluye todos los recursos asociados con una instancia de aplicación. Este controlador incluirá todos los recursos encontrados en la ruta especificada junto con los recursos a los que hace referencia la propiedad appAssetPath de una instancia de aplicación.

* ***type - String*** - app-assets

* ***ruta **-**cadena*** - ruta a una ubicación bajo una instancia de aplicación donde se almacenan los recursos de la aplicación

**mobileappoffers**: se ha introducido un nuevo controlador de sincronización de contenido para el caso de uso de Personalization para procesar contenido de destino. El controlador &quot;mobileapps&quot; sabe cómo procesar las ofertas de destino asociadas que ha creado el autor del contenido. El controlador mobileapps amplía el controlador de actualización de páginas abstractas, por lo que muchas de las propiedades son similares. Los detalles del controlador mobileapps tienen las siguientes propiedades.

El controlador mobileappsoffers amplía el controlador mobileappspages y agrega las siguientes propiedades:

* ***locationRoot - String*** - especifique la ubicación de la aplicación móvil
* ***includePageTypes - String*** - de forma predeterminada admite cq/personalization/components/teaserpage y cq/personalization/components/offerproxy
* ***selector - Cadena*** - debe establecerse como tandt
* ***ruta de acceso - Cadena*** - la ruta de acceso a la marca de la campaña

**mobileappconfig**: El controlador de sincronización de contenido mobileappconfig proporciona una forma de insertar datos JSON en MobileAppsConfig.json. Para registrar una clase de proveedor, los desarrolladores agregarán su clase MobileAppsInfoProvider a la lista de proveedores. El controlador iterará en la lista de MobileAppsInfoProviders y permitirá al proveedor insertar datos en el archivo json resultante. La lista de propiedades que admite este controlador es la siguiente:

* ***ruta **-**Cadena*** - la ruta a un nodo de instancia de aplicación con tipo de página=instancia de aplicación o un RT que extienda /libs/mobileapps/core/components/instance
* ***proveedores - Cadena*** `[]` - la lista de MobileAppsInfoProviders completos
* ***targetRootDirectory - String*** - el directorio donde escribir el archivo MobileAppsConfig.json.
* **fileName - String** - nombre opcional del archivo en el que escribir el JSON, el valor predeterminado es MobileAppsConfig.json

Es posible tener varios controladores de configuración mobileappconfig configurados, cada uno con un conjunto único de proveedores que escriben en diferentes archivos JSON.

### Prueba de controladores de sincronización de contenido {#testing-content-sync-handlers}

**Pasos para comprobar la integridad** Borrar caché

* Borrar caché
* Ejecute el controlador (caché actualizada)
* Vuelva a ejecutar el controlador (la caché no debe actualizarse)

**Pasos para la depuración**

* Ejecute la configuración
* Exportar la configuración o revisar en el dispositivo
* Si falla la representación, compruebe que faltan *style/assets/libs* o compruebe si hay rutas incorrectas para *styles/assets/libs*

**Registro** Habilitar el registro de ContentSync Debug mediante las configuraciones del registrador OSGI en el paquete `com.day.cq.contentsync` Esto le permitirá hacer un seguimiento de qué controladores se ejecutaron y si actualizaron la caché e informaron de su actualización.

## Recursos adicionales {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y un desarrollador, consulte los recursos siguientes:

* [Creación para Adobe PhoneGap AEM Enterprise con](/help/mobile/phonegap.md)
* [Administración de contenido para Adobe PhoneGap AEM Enterprise con el servicio de administración de](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>Para comenzar con el desarrollo de aplicaciones de AEM Mobile, haga clic [aquí](/help/mobile/getting-started-aem-mobile.md).
