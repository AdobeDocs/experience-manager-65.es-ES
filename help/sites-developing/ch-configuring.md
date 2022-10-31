---
title: Configuración de ContextHub
seo-title: Configuring ContextHub
description: Obtenga información sobre cómo configurar ContextHub.
seo-description: Learn how to configure Context Hub.
uuid: f2988bb9-6878-42a2-bb51-c3f8683248c5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 61208bd5-475b-40be-ba00-31bbbc952adf
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1842'
ht-degree: 2%

---

# Configuración de ContextHub {#configuring-contexthub}

ContextHub es un marco para almacenar, manipular y presentar datos de contexto. Para obtener más información sobre ContextHub, consulte la [documentación para desarrolladores](/help/sites-developing/contexthub.md). Sustituciones de ContextHub [ClientContext](/help/sites-administering/client-context.md) en la IU táctil.

Configure las variables [ContextHub](/help/sites-developing/contexthub.md) para controlar si aparece en el modo de vista previa, para crear almacenes de ContextHub y añadir módulos de IU con la IU táctil optimizada.

## Desactivación de ContextHub {#disabling-contexthub}

De forma predeterminada, ContextHub está habilitado en una instalación AEM. ContextHub se puede deshabilitar para evitar que cargue js/css e inicialice. Existen dos opciones para deshabilitar ContextHub:

* Edite la configuración de ContextHub y marque la opción **Deshabilitar ContextHub**

   1. En el carril, toque o haga clic en **Herramientas > Sitios > ContextHub**
   1. Toque o haga clic en la opción predeterminada **Contenedor de configuración**
   1. Seleccione el **Configuración de ContextHub** y toque o haga clic en **Editar elemento seleccionado**
   1. Toque o haga clic en **Deshabilitar ContextHub** y toque o haga clic en **Guardar**

o

* Usar CRXDE Lite para establecer la propiedad `disabled` a **true** under `/libs/settings/cloudsettings`

>[!NOTE]
>
>[Debido a la reestructuración de repositorios en AEM 6.4,](/help/sites-deploying/repository-restructuring.md) la ubicación de las configuraciones de ContextHub cambió de `/etc/cloudsettings` a:
>
>* `/libs/settings/cloudsettings`
>* `/conf/global/settings/cloudsettings`
>* `/conf/<tenant>/settings/cloudsettings`


## Mostrar y ocultar la interfaz de usuario de ContextHub {#showing-and-hiding-the-contexthub-ui}

Configure el servicio OSGi de ContextHub de Granite de Adobe para que muestre u oculte el [Interfaz de usuario de ContextHub](/help/sites-authoring/ch-previewing.md) en sus páginas. El PID de este servicio es `com.adobe.granite.contexthub.impl.ContextHubImpl.`

Para configurar el servicio, puede utilizar el [Consola web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o use un [Nodo JCR en el repositorio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository):

* **Consola web:** Para mostrar la IU, seleccione la propiedad Mostrar IU . Para ocultar la interfaz de usuario, desactive la propiedad Ocultar IU .
* **Nodo JCR:** Para mostrar la interfaz de usuario, establezca el `com.adobe.granite.contexthub.show_ui` propiedad a `true`. Para ocultar la interfaz de usuario, establezca la propiedad en `false`.

Al mostrar la interfaz de usuario de ContextHub, solo aparece en páginas de AEM instancias de autor. La interfaz de usuario no aparece en páginas de instancias de publicación.

## Adición de modos y módulos de IU de ContextHub {#adding-contexthub-ui-modes-and-modules}

Configure los modos y módulos de IU que aparecen en la barra de herramientas de ContextHub en el modo de vista previa:

* Modos de IU: Grupos de módulos relacionados
* Módulos: Widgets que exponen datos de contexto de una tienda y permiten a los autores manipular el contexto

Los modos de IU aparecen como una serie de iconos en la parte izquierda de la barra de herramientas. Cuando se selecciona, los módulos de un modo de IU aparecen a la derecha.

![chlimage_1-319](assets/chlimage_1-319.png)

Los iconos son referencias del [Biblioteca de iconos de la IU de Coral](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons).

### Adición de un modo de IU {#adding-a-ui-mode}

Agregue un modo de IU para agrupar los módulos relacionados de ContextHub. Cuando cree el modo de IU, proporcione el título y el icono que aparecen en la barra de herramientas de ContextHub.

1. En el carril del Experience Manager, pulse o haga clic en Herramientas > Sitios > Context Hub.
1. Toque o haga clic en el contenedor de configuración predeterminado.
1. Toque o haga clic en la configuración de ContextHub.
1. Toque o haga clic en el botón Crear y, a continuación, toque o haga clic en el modo de IU de ContextHub.

   ![chlimage_1-320](assets/chlimage_1-320.png)

1. Proporcione valores para las siguientes propiedades:

   * Título del modo IU: El título que identifica el modo de IU
   * Icono de modo: El selector de la variable [Icono de Coral UI](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) para usar, por ejemplo `coral-Icon--user`
   * Habilitado: Seleccione esta opción para mostrar el modo de IU en la barra de herramientas de ContextHub

1. Haga clic o pulse Guardar.

### Adición de un módulo de IU {#adding-a-ui-module}

Agregue un módulo de IU de ContextHub a un modo de IU para que aparezca en la barra de herramientas de ContextHub para obtener una vista previa del contenido de la página. Al agregar un módulo de IU, se crea una instancia de un tipo de módulo registrado con ContextHub. Para agregar un módulo de interfaz de usuario, debe conocer el nombre del tipo de módulo asociado.

AEM proporciona un tipo de módulo de interfaz de usuario base, así como varios tipos de módulo de interfaz de usuario de ejemplo en los que puede basar un módulo de interfaz de usuario. En la tabla siguiente se proporciona una breve descripción de cada uno de ellos. Para obtener información sobre el desarrollo de un módulo de IU personalizado, consulte [Creación de módulos de IU de ContextHub](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

Las propiedades del módulo de IU incluyen una configuración detallada en la que puede proporcionar valores para propiedades específicas del módulo. Proporcione la configuración detallada en formato JSON. La columna Tipo de módulo de la tabla proporciona vínculos a información sobre el código JSON necesario para cada tipo de módulo de interfaz de usuario.

| Tipo de módulo | Descripción | Almacenar |
|---|---|---|
| [contexthub.base](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) | Un tipo de módulo de IU genérico | Configurado en las propiedades del módulo de IU |
| [contexthub.browserinfo](/help/sites-developing/ch-samplemodules.md#contexthub-browserinfo-ui-module-type) | Muestra información sobre el explorador | surferinfo |
| [contexthub.datetime](/help/sites-developing/ch-samplemodules.md#contexthub-datetime-ui-module-type) | Muestra información de fecha y hora | datetime |
| [contexthub.device](/help/sites-developing/ch-samplemodules.md#contexthub-device-ui-module-type) | Mostrar el dispositivo cliente | emuladores |
| [contexthub.location](/help/sites-developing/ch-samplemodules.md#contexthub-location-ui-module-type) | Muestra la latitud y longitud del cliente, así como la ubicación en un mapa. Permite cambiar la ubicación. | geolocalización |
| [contexthub.screen-orientation](/help/sites-developing/ch-samplemodules.md#contexthub-screen-orientation-ui-module-type) | Muestra la orientación de pantalla del dispositivo (horizontal o vertical) | emuladores |
| [contexthub.tagcloud](/help/sites-developing/ch-samplemodules.md#contexthub-tagcloud-ui-module-type) | Muestra estadísticas sobre las etiquetas de página | tagcloud |
| [granite.profile](/help/sites-developing/ch-samplemodules.md#granite-profile-ui-module-type) | Muestra la información de perfil del usuario actual, incluido authorizableID, displayName y familyName. Puede cambiar el valor de displayName y familyName. | El perfil. |

1. En el carril del Experience Manager, pulse o haga clic en Herramientas > Sitios > ContextHub.
1. Toque o haga clic en el contenedor de configuración al que desee agregar un módulo de interfaz de usuario.
1. Haga clic o escriba la configuración de ContextHub a la que desea agregar el módulo de IU.
1. Toque o haga clic en el modo de IU al que está agregando el módulo de IU.
1. Toque o haga clic en el botón Crear y, a continuación, toque o haga clic en el módulo de interfaz de usuario de ContextHub (genérico).

   ![chlimage_1-321](assets/chlimage_1-321.png)

1. Proporcione valores para las siguientes propiedades:

   * Título del módulo de la interfaz de usuario: Un título que identifica el módulo de IU
   * Tipo de módulo: El tipo de módulo
   * Habilitado: Seleccione esta opción para mostrar el módulo de IU en la barra de herramientas de ContextHub

1. (Opcional) Para anular la configuración predeterminada de la tienda, introduzca un objeto JSON para configurar el módulo de interfaz de usuario.
1. Haga clic o pulse Guardar.

## Creación de un almacén de ContextHub {#creating-a-contexthub-store}

Cree un almacén de ContextHub para mantener los datos del usuario y acceder a los datos según sea necesario. Los almacenes de ContextHub se basan en candidatos de tiendas registrados. Cuando crea la tienda, necesita el valor de storeType con el que se registró el candidato de la tienda. (Consulte [Creación de candidatos de tienda personalizados](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).)

### Configuración detallada del almacén {#detailed-store-configuration}

Al configurar un almacén, la propiedad Configuración de detalles permite proporcionar valores para propiedades específicas del almacén. El valor se basa en la variable `config` del `init` función. Por lo tanto, si necesita proporcionar este valor y el formato del valor, depende del almacén.

El valor de la propiedad Configuración de detalles es un `config` en formato JSON.

### Candidatos de tienda de muestra {#sample-store-candidates}

AEM proporciona los siguientes candidatos de almacén de muestra en los que puede basar una tienda.

| Tipo de tienda | Descripción |
|---|---|
| [aem.segmentation](/help/sites-developing/ch-samplestores.md#aem-segmentation-sample-store-candidate) | Almacenar para segmentos de ContextHub resueltos y no resueltos. Recupera automáticamente los segmentos desde el Administrador de segmentos de ContextHub |
| [aem.resolvedsegments](/help/sites-developing/ch-samplestores.md#aem-resolvedsegments-sample-store-candidate) | Almacena los segmentos resueltos actualmente. Presta atención al servicio de Administrador de segmentos de ContextHub para actualizar automáticamente la tienda |
| [contexthub.geolocation](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) | Almacena la latitud y la longitud de la ubicación del explorador. |
| [contexthub.datetime](/help/sites-developing/ch-samplestores.md#contexthub-datetime-sample-store-candidate) | Almacena la fecha, la hora y la temporada actuales para la ubicación del explorador |
| [granite.emulators](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) | Define las propiedades y capacidades de varios dispositivos y detecta el dispositivo cliente actual |
| [contexthub.generic-jsonp](/help/sites-developing/ch-samplestores.md#contexthub-generic-jsonp-sample-store-candidate) | Recupera y almacena datos de un servicio JSONP |
| [granite.profile](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) | Almacena datos de perfil para el usuario actual |
| [contexthub.surferinfo](/help/sites-developing/ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) | Almacena información sobre el cliente, como información del dispositivo, tipo de explorador y orientación de la ventana. |
| [contexthub.tagcloud](/help/sites-developing/ch-samplestores.md#contexthub-tagcloud-sample-data-store) | Almacena las etiquetas de página y los recuentos de etiquetas |

1. En el carril del Experience Manager, pulse o haga clic en Herramientas > Sitios > ContextHub.
1. Toque o haga clic en el contenedor de configuración predeterminado.
1. Toque o haga clic en Configuración de Contexthub
1. Para agregar una tienda, toque o haga clic en el icono Crear y, a continuación, toque o haga clic en Configuración de la tienda de ContextHub.

   ![chlimage_1-322](assets/chlimage_1-322.png)

1. Proporcione valores para las propiedades de configuración básicas y, a continuación, toque o haga clic en Siguiente:

   * **Título de configuración:** El título que identifica el almacén
   * **Tipo de tienda:** El valor de la propiedad storeType del candidato de almacén en el que se basará el almacén
   * **Requerido:** Select
   * **Habilitado:** Seleccione para habilitar la tienda

1. (Opcional) Para anular la configuración de almacén predeterminada, introduzca un objeto JSON en el cuadro Configuración de detalles (JSON) .
1. Haga clic o pulse Guardar.

## Ejemplo: Uso de un servicio JSONP  {#example-using-a-jsonp-service}

Este ejemplo ilustra cómo configurar un almacén y mostrar los datos en un módulo de interfaz de usuario. En este ejemplo, el servicio MD5 del sitio jsontest.com se utiliza como fuente de datos para un almacén. El servicio devuelve el código hash MD5 de una cadena determinada, en formato JSON.

Se ha configurado un almacén contexthub.generic-jsonp para que almacene datos para la llamada de servicio `https://md5.jsontest.com/?text=%22text%20to%20md5%22`. El servicio devuelve los siguientes datos que se muestran en un módulo de interfaz de usuario:

```xml
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### Creación de una tienda contexthub.generic-jsonp {#creating-a-contexthub-generic-jsonp-store}

El candidato al almacén de muestras contexthub.generic-jsonp le permite recuperar datos de un servicio JSONP o de un servicio web que devuelve datos JSON. Para este candidato a tienda, utilice la configuración de la tienda para proporcionar detalles sobre el servicio JSONP que desea utilizar.

La variable [init](/help/sites-developing/contexthub-api.md#init-name-config) de la función `ContextHub.Store.JSONPStore` La clase JavaScript define una `config` que inicializa este candidato de tienda. La variable `config` contiene un `service` que incluye detalles sobre el servicio JSONP. Para configurar la tienda, proporcione la variable `service` en formato JSON como valor de la propiedad Configuración de detalles .

Para guardar datos del servicio MD5 del sitio jsontest.com, utilice el procedimiento indicado en [Creación de un almacén de ContextHub](/help/sites-developing/ch-configuring.md#creating-a-contexthub-store) con las siguientes propiedades:

* **Título de configuración:** md5
* **Tipo de tienda:** contexthub.generic-jsonp
* **Requerido:** Select
* **Habilitado:** Select
* **Configuración detallada (JSON):**

   ```xml
   {
    "service": {
    "jsonp": false,
    "timeout": 1000,
    "ttl": 1800000,
    "secure": false,
    "host": "md5.jsontest.com",
    "port": 80,
    "params":{
    "text":"text to md5"
        }
      }
    }
   ```

### Adición de un módulo de interfaz de usuario para los datos de md5 {#adding-a-ui-module-for-the-md-data}

Agregue un módulo de IU a la barra de herramientas de ContextHub para mostrar los datos almacenados en el almacén md5 de ejemplo. En este ejemplo, el módulo contexthub.base se utiliza para producir el siguiente módulo de IU:

![chlimage_1-323](assets/chlimage_1-323.png)

Utilice el procedimiento descrito en [Adición de un módulo de IU](#adding-a-ui-module) para agregar el módulo de IU a un modo de IU existente, como el modo de IU Perona de ejemplo. Para el módulo UI, utilice los siguientes valores de propiedad:

* **Título del módulo de la interfaz de usuario:** MD5
* **Tipo de módulo:** contexthub.base
* **Configuración detallada (JSON):**

   ```xml
   {
    "icon": "coral-Icon--data",
    "title": "MD5 Converstion",
    "storeMapping": { "md5": "md5" },
    "template": "<p> {{md5.original}}</p>;
                 <p>{{md5.md5}}</p>"
   }
   ```

## Depuración de ContextHub {#debugging-contexthub}

Se puede habilitar un modo de depuración para ContextHub para permitir la resolución de problemas. El modo de depuración se puede habilitar mediante la configuración de ContextHub o mediante CRXDE.

### Mediante la configuración {#via-the-configuration}

Edite la configuración de ContextHub y marque la opción **Depuración**

1. En el carril, toque o haga clic en **Herramientas > Sitios > ContextHub**
1. Toque o haga clic en la opción predeterminada **Contenedor de configuración**
1. Seleccione el **Configuración de ContextHub** y toque o haga clic en **Editar elemento seleccionado**
1. Toque o haga clic en **Depuración** y toque o haga clic en **Guardar**

### A través de CRXDE {#via-crxde}

Usar CRXDE Lite para establecer la propiedad `debug` a **true** en:

* `/conf/global/settings/cloudsettings` o
* `/conf/<tenant>/settings/cloudsettings`

>[!NOTE]
>
>En el caso de las configuraciones de ContextHub que siguen estando debajo de sus rutas heredadas, la ubicación para establecer la variable `debug property` es `/libs/settings/cloudsettings/legacy/contexthub`.

### Modo silencioso {#silent-mode}

El modo silencioso suprime toda la información de depuración. A diferencia de la opción de depuración normal, que se puede establecer de forma independiente para cada configuración de ContextHub, el modo silencioso es una configuración global que precede a cualquier configuración de depuración en el nivel de configuración de ContextHub.

Esto resulta útil para la instancia de publicación, donde no desea información de depuración. Como es una configuración global, se habilita mediante OSGi.

1. Abra el **Configuración de la consola web de Adobe Experience Manager** at `http://<host>:<port>/system/console/configMgr`
1. Buscar **ContextHub de Granite de Adobe**
1. Haga clic en la configuración **ContextHub de Granite de Adobe** para editar sus propiedades
1. Marque la opción **Modo silencioso** y haga clic en **Guardar**

## Recuperación de las configuraciones de ContextHub tras la actualización {#recovering-contexthub-configurations-after-upgrading}

Cuando una [actualizar a AEM](/help/sites-deploying/upgrade.md) se realiza una copia de seguridad de las configuraciones de ContextHub y se almacenan en una ubicación segura. Durante la actualización, se instalan las configuraciones predeterminadas de ContextHub, reemplazando las configuraciones existentes. La copia de seguridad es necesaria para conservar los cambios o adiciones que haya realizado.

Las configuraciones de ContextHub se almacenan en una carpeta denominada `contexthub` en los siguientes nodos:

* `/conf/global/settings/cloudsettings`
* `/conf/<tenant>/settings/cloudsettings`

Después de una actualización, la copia de seguridad se almacena en una carpeta denominada `contexthub` debajo de un nodo llamado:

`/conf/global/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx` o
`/conf/<tenant>/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx`

La variable `yyyymmdd` parte del nombre del nodo es la fecha en la que se realizó la actualización.

Para recuperar las configuraciones de ContextHub, utilice CRXDE Lite para copiar los nodos que representan sus tiendas, modos de interfaz de usuario y módulos de IU desde debajo de la `default-pre-upgrade_yyyymmdd_xxxxxx` nodo a continuación:

* `/conf/global/settings/cloudsettings` o
* `/conf/<tenant>/settings/cloudsettings`
