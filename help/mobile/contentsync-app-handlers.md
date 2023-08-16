---
title: Controladores de aplicaciones listos para usar
seo-title: Out of the Box App Handlers
description: Siga esta página para obtener más información sobre los controladores predeterminados para Adobe PhoneGap AEM Enterprise con el servicio de soporte de la aplicación de la interfaz de usuario de Adobe.
seo-description: Follow this page to learn about the out-of-the-box handlers for Adobe PhoneGap Enterprise with AEM.
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 0%

---

# Controladores de aplicaciones listos para usar{#out-of-the-box-app-handlers}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Consulte las siguientes directrices para desarrollar controladores de sincronización de contenido:

* Los controladores deben implementar *com.day.cq.contentsync.handler.ContentUpdateHandler* (directamente o ampliando una clase que sí lo hace)
* Los controladores pueden ampliar *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* El controlador solo debe informar de true si ha actualizado la caché de ContentSync. AEM Informar de forma incorrecta sobre true permitirá crear una actualización de forma.
* El controlador solo debe actualizar la caché si el contenido ha cambiado. No escriba en la caché si no es necesario un espacio en blanco y evite la creación de actualizaciones innecesarias.

## Controladores predeterminados {#out-of-the-box-handlers}

A continuación se enumeran los controladores de aplicación predeterminados:

**mobileapppages** Procesa las páginas de la aplicación.

* ***type: String*** - mobileapppages
* ***path - String*** - ruta a una página
* ***extension: cadena*** : extensión que debe utilizarse en la solicitud. Para páginas esto es casi siempre *html*, pero otras todavía son posibles.

* ***selector - Cadena*** : selectores opcionales separados por puntos. Algunos ejemplos comunes son *touch* para procesar versiones móviles de una página.

* ***deep: Boolean*** : propiedad booleana opcional que determina si también se deben incluir páginas secundarias. El valor predeterminado es *true.*

* ***includeImages - Boolean*** : propiedad booleana opcional que determina si se deben incluir imágenes. El valor predeterminado es *true*.

   * De forma predeterminada, solo se tienen en cuenta para la inclusión los componentes de imagen con un tipo de recurso de foundation/components/image.

* ***includeVideos - Booleano*** : propiedad booleana opcional para determinar si se deben incluir los vídeos. El valor predeterminado es *true*.

* ***includeModifiedPagesOnly - Booleano*** : Si es false o se omite, procese todas las páginas y compruebe las actualizaciones en el procesamiento. Si el valor es True, la base difiere en los cambios realizados en una página lastModified.
* ***+ reescribir (nodo)***
  ***- relativeParentPath - Cadena*** : la ruta para escribir todas las demás rutas relativas a.

>[!NOTE]
>
>El tipo de recurso de los componentes de imagen y vídeo afectados por este controlador se establece configurando las propiedades del *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*Servicio OSGi de MobilePagesUpdateHandler*.

**mobilepageassets** Recopila recursos de página de la aplicación.

**mobilecontentlisting** Muestra el contenido del zip de ContentSync. AEM Lo utiliza el js del lado del cliente en el dispositivo para realizar la copia inicial del archivo necesaria para las aplicaciones de la aplicación de la aplicación de.

AEM Este controlador debe agregarse a cualquier configuración de ContentSync de aplicaciones de la aplicación de la aplicación.

* ***type - String - mobilecontentlisting***
* ***ruta*** - Cadena: si se mantiene vacío, debe estar presente para que se vea como un controlador válido, pero se infiere que la ruta es la caché de ContentSync actual. Este valor se ignora.
* ***targetRootDirectory* -**Cadena: el prefijo que se agrega a las rutas como raíz de destino para la actualización de contenido de este controlador.
* ***order - Long* -**Ordene que ContentSync ejecute este controlador. Este número debe establecerse por encima de todos los demás controladores, como 100. Debe ejecutarse después de los controladores de contenido tradicionales.

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

**mobilecontentpackageslisting** AEM Enumera el paquete de contenido de la aplicación en cuestión en una aplicación determinada, así como la URL del servidor en la que realizar las solicitudes de actualización. Se utiliza en el lado del cliente js en el dispositivo para solicitar actualizaciones de contenido

AEM El controlador debe usarse en la configuración de ContentSync de App Shell (nodo con page-type=app-instance)

* ***type - String - mobilecontentpackageslisting***
* ***ruta **-**Cadena*** - Ruta a un shell de aplicación (nodo con page-type=app-instance).
* ***targetRootDirectory - Cadena*** : el prefijo que se agregará a las rutas como raíz de destino para la actualización de contenido de este controlador.
* ***order - Long* -**Orden para que ContentSync ejecute este controlador. Este número debe establecerse por encima de todos los demás controladores, como 100. Debe ejecutarse después de los controladores de contenido tradicionales.

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

**widgetconfig** Incluye un archivo config.xml actualizado que combina las ediciones realizadas mediante el Centro de comandos con un archivo config.xml proporcionado. Si no se incluye este controlador, los detalles de la aplicación que se cambien a través de la interfaz de administración no se incluirán en la caché.

AEM Este controlador debe usarse en una configuración de ContentSync de App Shell de la aplicación de la aplicación (nodo con page-type=[app-instance]).

* ***type: String* - **widgetconfig
* ***ruta **-**Cadena*** - Ruta a cualquier nodo secundario del shell de la aplicación (nodo con page-type=[app-instance]).
* ***targetRootDirectory - Cadena*** : el prefijo que se agregará a las rutas como raíz de destino para la actualización de contenido de este controlador.
* ***targetIconDirectory: cadena*** - el directorio donde colocar los iconos de la aplicación

**mobileADBMobileConfigJSON** Incluya el archivo ADBMobileConfig.JSON si se configuró el servicio en la nube de AMS.

Se utiliza en tiempo de compilación para configurar el complemento AMS para la compatibilidad con análisis.

AEM El controlador debe usarse en la configuración de ContentSync de App Shell (nodo con page-type=app-instance)

* ***type: String*** - mobileADBMobileConfigJSON
* ***path - String*** - Ruta a un shell de aplicación (nodo con page-type=app-instance o RT que amplía /libs/mobileapps/core/components/instance)
* ***targetRootDirectory - Cadena*** : el prefijo que se agregará a las rutas como raíz de destino para la actualización de contenido de este controlador

**notificationsconfig** Extrae las configuraciones de notificaciones necesarias en el dispositivo. Las propiedades se extraen de la configuración respectiva del servicio en la nube de servicios push asociado a la aplicación.

AEM Las propiedades que no son de la clase de la lista de propiedades del nodo jcr:content del servicio en la nube se extraen y se añaden al **page-notifications-config.json** Archivo JSON para su inclusión en la raíz www del contenido de la aplicación.

AEM Las propiedades de son aquellas que se espacian con nombres como &quot;cq&quot;, &quot;sling&quot; o &quot;jcr&quot;. Otras propiedades se pueden excluir mediante la propiedad excludeProperties en el nodo de configuración de sincronización de contenido.

* ***type: String*** - notificationsconfig
* ***excludeProperties: cadena[]*** - propiedades que se excluirán

**contentsyncconfigcontent** Recopila contenido de una configuración de ContentSync existente.

* ***type: String*** - contentsyncconfigcontent
* ***path - String*** - Ruta a una de:

   * otra configuración de ContentSync
   * a un paquete de contenido (se utilizará su propiedad phonegap-exportTemplate para encontrar su configuración ContentSync)
   * a un recurso móvil (el contenido de la aplicación se encontrará debajo de ese recurso y, si esos paquetes de contenido tienen una propiedad page-includeInBuild que es true, se utilizará phonegap-exportTemplate para encontrar su configuración de ContentSync)

* ***autoCreateFirstUpdateBeforeImport: booleano*** : si es true, cree una **actualizar** en la configuración de target antes de importar si una vez no existe ya

* ***autoFillBeforeImport: booleano*** : si es true, actualice/rellene la configuración de target antes de importar
* ***configSuffix: cadena*** : una cadena que se anexará a la ruta indicada en la propiedad &quot;phonegap-exportTemplate&quot; de app-content. Esto se puede utilizar para distinguir diferentes plantillas de exportación. Por ejemplo, esta propiedad se puede establecer en **&quot;-dev&quot;** para indicar que *&quot;/../../../appconfig-dev&quot;* debería utilizarse (en lugar de *&quot;/../../../appconfig&quot;*).

**app-assets** Incluye todos los recursos asociados a una instancia de aplicación. Este controlador incluirá todos los recursos encontrados en la ruta especificada junto con los recursos a los que hace referencia la propiedad appAssetPath de una instancia de aplicación.

* ***type: String*** - app-assets

* ***ruta **-**Cadena*** : ruta a una ubicación en una instancia de aplicación donde se almacenan los recursos de la aplicación

**mobileappoffers** Se ha introducido un nuevo controlador de sincronización de contenido para el caso de uso Personalización para procesar contenido de destino. El controlador &quot;mobileapps&quot; sabe cómo procesar las ofertas de destino asociadas que ha creado el autor del contenido. El controlador mobileapps amplía el controlador de actualización de páginas abstractas, por lo que muchas de las propiedades son similares. Los detalles del controlador mobileapps tienen las siguientes propiedades.

El controlador mobileappsoffers amplía el controlador mobileappspages y agrega las siguientes propiedades:

* ***locationRoot: cadena*** : especifique la ubicación de la aplicación móvil
* ***includePageTypes: cadena*** : de forma predeterminada, admite cq/personalization/components/teaserpage y cq/personalization/components/offerproxy
* ***selector - Cadena*** - debe configurarse como tandt
* ***path - String***- el camino a la marca de la campaña

**mobileappconfig** El controlador de sincronización de contenido mobileappconfig proporciona una forma de insertar datos JSON en MobileAppsConfig.json. Para registrar una clase de proveedor, los desarrolladores agregarán su clase MobileAppsInfoProvider a la lista de proveedores. El controlador iterará en la lista de MobileAppsInfoProviders y permitirá al proveedor insertar datos en el archivo json resultante. La lista de propiedades que admite este controlador es la siguiente:

* ***ruta **-**Cadena*** - la ruta a un nodo de instancia de aplicación con page-type=app-instance o un RT que extienda /libs/mobileapps/core/components/instance
* ***providers - Cadena*** `[]` - la lista de MobileAppsInfoProviders completos
* ***targetRootDirectory - Cadena*** : el directorio en el que escribir el archivo MobileAppsConfig.json.
* **fileName - Cadena** : nombre opcional del archivo en el que escribir el JSON, el valor predeterminado es MobileAppsConfig.json

Es posible tener varios controladores de configuración mobileappconfig configurados, cada uno con un conjunto único de proveedores que escriben en diferentes archivos JSON.

### Prueba de controladores de sincronización de contenido {#testing-content-sync-handlers}

**Pasos para comprobar la integridad** Borrar caché

* Borrar caché
* Ejecute el controlador (caché actualizada)
* Vuelva a ejecutar el controlador (la caché no debe actualizarse)

**Pasos para la depuración**

* Ejecute la configuración
* Exportar la configuración o revisar en el dispositivo
* Si el procesamiento falla, compruebe si falta *styles/assets/libs* o compruebe si hay rutas incorrectas a *styles/assets/libs*

**Registro** Habilitar el registro de depuración de ContentSync mediante las configuraciones del registrador OSGI en el paquete `com.day.cq.contentsync` Esto le permitirá rastrear qué controladores se ejecutaron y si actualizaron la caché e informaron de su actualización.

## Recursos adicionales {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y un desarrollador, consulte los recursos siguientes:

* [Creación para Adobe PhoneGap AEM Enterprise con](/help/mobile/phonegap.md)
* [Administración de contenido para Adobe PhoneGap AEM Enterprise con el servicio de administración de](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>Para empezar a desarrollar aplicaciones de AEM Mobile, haga clic en [aquí](/help/mobile/getting-started-aem-mobile.md).
