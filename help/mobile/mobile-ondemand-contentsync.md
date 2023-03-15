---
title: Móvil con sincronización de contenido
seo-title: Mobile with Content Sync
description: Siga esta página para obtener más información sobre la sincronización de contenido. AEM Las páginas creadas en la aplicación se pueden usar como contenido de la aplicación, incluso cuando el dispositivo está sin conexión. AEM Además, dado que las páginas de la se basan en estándares web, funcionan en plataformas múltiples, lo que permite incrustarlas en cualquier envoltorio nativo. Esta estrategia reduce el esfuerzo de desarrollo y le permite actualizar fácilmente el contenido de la aplicación.
seo-description: Follow this page to learn about Content Sync. Pages that are authored in AEM can be used as app content, even when the device is offline. Furthermore, because AEM pages are based on web standards, they work cross-platform enabling you to embed them in any native wrapper. This strategy reduces develoment effort and enables you to easily update app content.
uuid: 11f74cc5-99a5-4186-9b60-b19351305432
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 8fb70ca4-86fc-477d-9773-35b84d5e85a8
exl-id: a6e59334-09e2-4bb8-b445-1868035da556
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2993'
ht-degree: 0%

---

# Móvil con sincronización de contenido{#mobile-with-content-sync}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran procesamiento del lado del cliente basado en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Utilice la sincronización de contenido para empaquetar contenido de modo que se pueda utilizar en aplicaciones móviles nativas. AEM Las páginas creadas en la aplicación se pueden usar como contenido de la aplicación, incluso cuando el dispositivo está sin conexión. AEM Además, dado que las páginas de la se basan en estándares web, funcionan en plataformas múltiples, lo que permite incrustarlas en cualquier envoltorio nativo. Esta estrategia reduce el esfuerzo de desarrollo y le permite actualizar fácilmente el contenido de la aplicación.

El marco de trabajo de sincronización de contenido crea un archivo de almacenamiento que contiene el contenido web. El contenido puede ser desde páginas simples, imágenes y archivos de PDF, o aplicaciones web completas. La API de sincronización de contenido proporciona acceso al archivo desde aplicaciones móviles o procesos de compilación para que el contenido se pueda recuperar e incluir en la aplicación.

La siguiente secuencia de pasos ilustra un caso de uso típico para la sincronización de contenido:

1. AEM El desarrollador de crea una configuración de sincronización de contenido que especifica el contenido que se va a incluir.
1. El marco de trabajo Sincronización de contenido recopila y almacena en caché el contenido.
1. En un dispositivo móvil, la aplicación móvil se inicia y solicita contenido al servidor, que se entrega en un archivo ZIP.
1. El cliente desempaqueta el contenido ZIP en el sistema de archivos local. La estructura de carpetas del archivo ZIP simula las rutas que un cliente (por ejemplo, un explorador) solicitaría normalmente al servidor.
1. El cliente abre el contenido en un explorador incrustado o lo utiliza de alguna otra manera.
1. Posteriormente, el cliente solicita contenido actualizado desde el servidor. El marco de trabajo de sincronización de contenido ofrece actualizaciones incrementales para reducir el tamaño y el tiempo de descarga, lo que puede ser importante para dispositivos móviles debido al ancho de banda limitado o los volúmenes de datos.

## Desarrollo de los controladores de sincronización de contenido {#developing-the-content-sync-handlers}

Algunas de las directrices para desarrollar controladores de sincronización de contenido son las siguientes:

* Los controladores deben implementar *com.day.cq.contentsync.handler.ContentUpdateHandler* (directamente o ampliando una clase que sí lo hace)
* Los controladores pueden ampliar *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* El controlador solo debe informar de true si actualiza la caché de ContentSync. AEM Informar de forma incorrecta sobre true tendrá que crear una actualización cuando en realidad no se haya producido.
* El controlador solo debe actualizar la caché si el contenido ha cambiado. No escriba en la caché si no es necesario un blanco. Esto da como resultado la creación de una actualización innecesaria.

>[!NOTE]
>
>Activar *Registro de ContentSync Debug* mediante las configuraciones del registrador OSGI en el paquete *com.day.cq.contentsync*. Esto permite rastrear qué controladores se ejecutaron y si actualizaron la caché e informaron de su actualización.

## Configuración del contenido de sincronización de contenido {#configuring-the-content-sync-content}

Cree una configuración de sincronización de contenido para especificar el contenido del archivo ZIP que se envía al cliente. Puede crear cualquier cantidad de configuraciones de sincronización de contenido. Cada configuración tiene un nombre para fines de identificación.

Para crear una configuración de sincronización de contenido, agregue una `cq:ContentSyncConfig` al repositorio, con el `sling:resourceType` propiedad establecida en `contentsync/config`. El `cq:ContentSyncConfig` AEM El nodo se puede encontrar en cualquier lugar del repositorio, pero los usuarios de la instancia de publicación de la aplicación deben poder acceder a él. Por lo tanto, debe agregar el nodo siguiente `/content`.

Para especificar el contenido del archivo ZIP de sincronización de contenido, agregue nodos secundarios al nodo cq:ContentSyncConfig. Las siguientes propiedades de cada nodo secundario identifican un elemento de contenido para incluir y cómo se procesa al agregarlo:

* `path`: la ubicación del contenido.
* `type`: Nombre del tipo de configuración que se utilizará para procesar el contenido. Hay varios tipos disponibles y se describen en esta sección *Tipos de configuración*.

Consulte *Ejemplo de configuración de sincronización de contenido* para obtener más información.

Después de crear la configuración de sincronización de contenido, esta aparece en la consola Sincronización de contenido.

>[!NOTE]
>
>El marco de trabajo de sincronización de contenido no comprueba que las dependencias de los recursos y los archivos relacionados con el diseño estén incluidos en los paquetes de sincronización de contenido. Asegúrese de incluir todos los archivos necesarios en el archivo ZIP.

### Configuración del acceso a las descargas de sincronización de contenido {#configuring-access-to-content-sync-downloads}

Especifique un usuario o grupo que pueda descargar desde Sincronización de contenido. Puede configurar el usuario o grupo predeterminado que puede descargar de todas las cachés de sincronización de contenido, así como anular el valor predeterminado y configurar el acceso para una configuración de sincronización de contenido específica.

AEM Cuando se instala la opción, los miembros del grupo de administradores pueden descargar desde Sincronización de contenido de forma predeterminada.

#### Configuración del acceso predeterminado para descargas de sincronización de contenido {#setting-the-default-access-for-content-sync-downloads}

El servicio Administrador de sincronización de contenido de CQ diario controla el acceso a la sincronización de contenido. Configure este servicio para especificar el usuario o grupo que puede descargar desde Sincronización de contenido de forma predeterminada.

Si es usted [configuración del servicio mediante la consola web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), escriba el nombre del usuario o grupo como el valor de la propiedad Autorizable Caché de reserva.

Si es usted [configuración en el repositorio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository), utilice la siguiente información sobre el servicio:

* PID: com.day.cq.contentsync.impl.ContentSyncManagerImpl
* Nombre de propiedad: contentsync.fallback.authorizable

#### Anulación del acceso de descarga para una caché de sincronización de contenido {#overriding-download-access-for-a-content-sync-cache}

Para configurar el acceso de descarga para una configuración de sincronización de contenido específica, agregue la siguiente propiedad al `cq:ContentSyncConfig` nodo:

* Nombre: autorizable
* Tipo: cadena
* Valor: Nombre del usuario o grupo que puede descargar.

Por ejemplo, la aplicación permite a los usuarios instalar actualizaciones directamente desde la sincronización de contenido. Para permitir que todos los usuarios descarguen la actualización, debe establecer el valor de la propiedad autorizable en `everyone`.

Si la variable `cq:ContentSyncConfig` El nodo no tiene una propiedad autorizable, el usuario o grupo predeterminado configurado para la propiedad autorizable Caché de reserva del servicio Administrador de sincronización de contenido de CQ Day determina quién puede descargar.

### Configuración del usuario para actualizar una caché de sincronización de contenido {#configuring-the-user-for-updating-a-content-sync-cache}

Cuando un usuario realiza una actualización de la caché de sincronización de contenido, una cuenta de usuario específica realiza la acción en nombre del usuario. El usuario anónimo actualiza todas las cachés de sincronización de contenido de forma predeterminada.

Puede anular el usuario predeterminado y especificar un usuario o grupo que actualice una caché de sincronización de contenido específica.

Para anular el usuario predeterminado, especifique un usuario o grupo que realice actualizaciones para una configuración de sincronización de contenido específica agregando la siguiente propiedad al nodo cq:ContentSyncConfig:

* Nombre: `updateuser`
* Tipo: `String`
* Valor: Nombre del usuario o grupo que puede realizar las actualizaciones.

Si la variable `cq:ContentSyncConfig` el nodo no tiene `updateuser` propiedad, el valor predeterminado `anonymous` el usuario actualiza la caché.

### Tipos de configuración {#configuration-types}

El procesamiento puede abarcar desde el procesamiento de JSON simple hasta el procesamiento completo de páginas, incluidos los recursos a los que se hace referencia. En esta sección se enumeran los tipos de configuración disponibles y sus parámetros específicos:

**copia** Simplemente copie archivos y carpetas.

* **ruta** : Si la ruta apunta a un solo archivo, solo se copia el archivo. Si apunta a una carpeta (incluidos los nodos de página), se copiarán todos los archivos y carpetas siguientes.

**content** Procesar contenido mediante estándar [Procesamiento de solicitudes de Sling](/help/sites-developing/the-basics.md#sling-request-processing).

* **ruta** - Ruta al recurso que se debe generar.
* **extensión** : extensión que debe utilizarse en la solicitud. Algunos ejemplos comunes son *html* y *json*, pero cualquier otra extensión es posible.

* **selector** : selectores opcionales separados por puntos. Algunos ejemplos comunes son *touch* para procesar versiones móviles de una página o *infinito* para la salida JSON.

**clientlib** Empaquete una biblioteca de cliente JavaScript o CSS.

* **ruta** - Ruta a la raíz de la biblioteca del cliente.
* **extensión** - Tipo de biblioteca de cliente. Debe configurarse como lo siguiente *js* o *css* en este momento.

**activos**

Recopilar representaciones originales de recursos.

* **ruta** - Ruta a una carpeta de recursos debajo de /content/dam.

**imagen** Recopile una imagen.

* **ruta** - Ruta a un recurso de imagen.

El tipo de imagen se utiliza para incluir el logotipo de We Retail en el archivo zip.

**páginas** AEM Procesar páginas de la y recopilar recursos referenciados.

* **ruta** - Ruta a una página.
* **extensión** : extensión que debe utilizarse en la solicitud. Para páginas esto es casi siempre *html*, pero otras todavía son posibles.

* **selector** : selectores opcionales separados por puntos. Algunos ejemplos comunes son *touch* para procesar versiones móviles de una página.

* **profundo** : propiedad booleana opcional que determina si también se deben incluir páginas secundarias. El valor predeterminado es *true.*

* **includeImages** : propiedad booleana opcional que determina si se deben incluir imágenes. El valor predeterminado es *true*.

   De forma predeterminada, solo se tienen en cuenta para la inclusión los componentes de imagen con un tipo de recurso de foundation/components/image. Puede agregar más tipos de recursos configurando la variable **Controlador de actualización de páginas de CQ WCM por día** en la consola web.

**reescribir** El nodo de reescritura define cómo se reescriben los vínculos en la página exportada. Los vínculos reescritos pueden apuntar a los archivos incluidos en el archivo zip o a los recursos del servidor.

El `rewrite` El nodo debe encontrarse debajo de `page` nodo.

El `rewrite` El nodo puede tener una o varias de las siguientes propiedades:

* `clientlibs`: reescribe las rutas clientlibs.

* `images`: reescribe las rutas de las imágenes.
* `links`: reescribe las rutas de los vínculos.

Cada propiedad puede tener uno de los siguientes valores:

* `REWRITE_RELATIVE`: reescribe la ruta con una posición relativa al archivo .html de la página en el sistema de archivos.

* `REWRITE_EXTERNAL`AEM : reescribe la ruta señalando al recurso en el servidor, utilizando la función de búsqueda de recursos de la [Servicio externalizador](/help/sites-developing/externalizer.md).

AEM El servicio llamó a **PathRewriterTransformerFactory** permite configurar los atributos html específicos que se van a reescribir. El servicio se puede configurar en la consola web y tiene una configuración para cada propiedad del `rewrite` nodo: `clientlibs`, `images` y `links`.

AEM Esta función se añadió en la versión 5.5 de.

### Ejemplo de configuración de sincronización de contenido {#example-content-sync-configuration}

La lista siguiente muestra un ejemplo de configuración para la sincronización de contenido.

```xml
+ weretail_go [cq:ContentSyncConfig]
  - sling:resourceType = "contentsync/config"

  + etc.designs.default [nt:unstructured]
    - path = "/etc/designs/default"
    - type = "copy"

  + etc.designs.mobile [nt:unstructured]
    - path = "/etc/designs/mobile"
    - type = "copy"

  + events.plist [nt:unstructured]
    - path = "/content/weretail_mobile/en/events/jcr:content/par/events"
    - type = "content"
    - extension = "plist"

  + events.touch.html [nt:unstructured]
    - path = "/content/weretail_mobile/en/events"
    - type = "pages"
    - extension = "html"
    - selector = "touch"

  + logo [nt:unstructured]
    - path = "/etc/designs/mobile/jcr:content/mobilecontentpage/logo"
    - type = "logo"

  + manifest [nt:unstructured]
    - indexPage = "/content/weretail_mobile/en/events.touch.html"
    - metadataPlist = "/content/weretail_mobile/en/events/_jcr_content/par/events.plist"

  + ...
```

**etc.designs.default y etc.designs.mobile** Las dos primeras entradas de la configuración deberían ser bastante obvias. Como vamos a incluir varias páginas móviles, necesitamos los archivos de diseño relacionados debajo de /etc/designs. Y como no se requiere ningún procesamiento adicional, la copia es suficiente.

**events.plist** Esta entrada es un poco especial. Como se mencionó en la introducción, la aplicación debe proporcionar una vista de mapa con marcadores de las ubicaciones de los eventos. Vamos a proporcionar la información de ubicación necesaria como un archivo independiente en formato PLIST. Para que esto funcione, el componente de lista de eventos que se utiliza en la página de índice tiene un script llamado plist.jsp. Este script se ejecuta cuando se solicita el recurso del componente con la extensión .plist. Como de costumbre, la ruta de los componentes se da en la propiedad de ruta y el tipo se establece en contenido, porque queremos aprovechar [Procesamiento de solicitudes de Sling](/help/sites-developing/the-basics.md#sling-request-processing).

**events.touch.html** A continuación, aparecen las páginas que se mostrarán en la aplicación. La propiedad path se establece en la página raíz de los eventos. También se incluirán todas las páginas de evento debajo de esa página, ya que la propiedad deep tiene el valor predeterminado true. Utilizamos páginas como tipo de configuración, de modo que se incluya cualquier imagen u otro archivo al que se pueda hacer referencia desde un componente de imagen o descarga de una página. Además, configurar el selector táctil nos da una versión móvil de las páginas. La configuración del paquete de funciones contiene más entradas de este tipo, pero se omiten por simplicidad.

**logo** El tipo de configuración de logotipo no se ha mencionado hasta ahora y no es ninguno de los tipos integrados. Sin embargo, el marco de trabajo de sincronización de contenido es extensible hasta cierto punto y este es un ejemplo de ello, que se tratará en la siguiente sección.

**manifestar** A menudo es deseable incluir algún tipo de metadatos en el archivo zip, como la página de inicio del contenido, por ejemplo. Sin embargo, codificar dicha información impide cambiarla fácilmente más adelante. El marco de trabajo de sincronización de contenido es compatible con este caso de uso al buscar un nodo de manifiesto en la configuración, que se identifica simplemente por el nombre y no requiere un tipo de configuración. Todas las propiedades definidas en ese nodo en particular se agregan a un archivo, que también se denomina manifest y reside en la raíz del archivo zip.

En el ejemplo, se supone que la página de lista de eventos es la página inicial. Esta información se proporciona en la **indexPage** propiedad y, por lo tanto, se pueden cambiar fácilmente en cualquier momento. Una segunda propiedad define la ruta del *events.plist* archivo. Como veremos más adelante, la aplicación cliente ahora puede leer el manifiesto y actuar según él.

Tan pronto como se establezca la configuración, el contenido se puede descargar con un explorador o con cualquier otro cliente HTTP, o si está desarrollando para iOS, puede utilizar la biblioteca de cliente de WAppKitSync dedicada. La ubicación de descarga está formada por la ruta de la configuración y la variable *.zip* AEM , p. ej., al trabajar con una instancia local de la instancia de la: *http://localhost:4502/content/weretail_go.zip*

### La consola de sincronización de contenido {#the-content-sync-console}

La consola Sincronización de contenido enumera todas las configuraciones de Sincronización de contenido del repositorio (todos los nodos de tipo `cq:ContentSyncConfig`) y para cada configuración le permite hacer lo siguiente:

* Actualice la caché.
* Borre la caché.
* Descargue un archivo zip completo.
* Descargue un zip de diferencia entre ahora y una fecha y hora específicas.

Puede resultar útil para el desarrollo y la solución de problemas.

Se puede acceder a la consola en:

`http://localhost:4502/libs/cq/contentsync/content/console.html`

Tiene el siguiente aspecto:

![chlimage_1-50](assets/chlimage_1-50.png)

### Ampliación del marco de sincronización de contenido {#extending-the-content-sync-framework}

Aunque el número de opciones de configuración ya es bastante amplio, es posible que no cubra todos los requisitos de su caso de uso específico. En esta sección se describen los puntos de extensión del marco de trabajo de sincronización de contenido y cómo crear tipos de configuración personalizados.

Para cada tipo de configuración, hay un *Controlador de actualización de contenido*, que es una fábrica de componentes OSGi registrada para ese tipo específico. Estos controladores recopilan contenido, lo procesan y lo agregan a una caché que mantiene el marco de trabajo de sincronización de contenido. Implemente la siguiente interfaz o clase base abstracta:

* `com.day.cq.contentsync.handler.ContentUpdateHandler` : Interfaz que todos los controladores de actualizaciones deben implementar
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` : Una clase abstracta que simplifica la representación de recursos mediante Sling

Registre su clase como fábrica de componentes OSGi e impleméntelo en el contenedor OSGi en un paquete. Esto se puede hacer con la variable [Complemento Maven SCR](https://felix.apache.org/site/apache-felix-maven-scr-plugin.html) mediante etiquetas JavaDoc o anotaciones. El siguiente ejemplo muestra la versión de JavaDoc:

```java
/*
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/customtype"
 */
public class CustomTypeUpdateHandler implements ContentUpdateHandler {
    // add your code here
}

/*
 * @scr.component metatype="no" inherit="true"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/othertype"
 */
public class OtherTypeUpdateHandler extends AbstractSlingResourceUpdateHandler {
    // add your code here
}
```

Observe que la variable *fábrica* La definición de contiene la interfaz común y el tipo personalizado separados por una barra diagonal. Esta estrategia permite al marco de trabajo de sincronización de contenido buscar y crear una instancia de la clase personalizada a medida que reconoce el tipo personalizado en una entrada de configuración. En la siguiente sección se muestra un ejemplo concreto de un controlador de actualización personalizado.

>[!CAUTION]
>
>Cuando se genera a partir de la clase base AbstractSlingResourceUpdateHandler, debe agregar la variable *heredar* definición. De lo contrario, el contenedor OSGi no establecerá las referencias necesarias declaradas en la clase base.

### Implementar un controlador de actualización personalizado {#implementing-a-custom-update-handler}

Cada página de We.Retail Mobile contiene un logotipo en la esquina superior izquierda que queremos incluir en el archivo zip, por supuesto. AEM Sin embargo, para la optimización de la caché, no hace referencia a la ubicación real del archivo de imagen en el repositorio, lo que nos impide simplemente utilizar la variable **copia** tipo de configuración. Lo que tenemos que hacer en su lugar es proporcionar el nuestro **logo** AEM tipo de configuración que hace que la imagen esté disponible en la ubicación solicitada por el usuario de. La siguiente lista de códigos muestra la implementación completa del controlador de actualización de logotipos:

#### LogoUpdateHandler.java {#logoupdatehandler-java}

```java
package com.day.cq.wcm.apps.weretail.impl;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.day.cq.commons.jcr.JcrUtil;
import com.day.cq.contentsync.config.ConfigEntry;
import com.day.cq.contentsync.handler.ContentUpdateHandler;
import com.day.cq.wcm.foundation.Image;
import com.day.text.Text;

/**
 * The <code>LogoUpdateHandler</code> is used to update the content sync cache
 * with a page logo added using a logo component.
 *
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/logo"
 */
public class LogoUpdateHandler implements ContentUpdateHandler {

    private static final Logger log = LoggerFactory.getLogger(LogoUpdateHandler.class);

    /** @scr.reference policy="static" */
    protected JcrResourceResolverFactory resolverFactory;

    public boolean updateCacheEntry(ConfigEntry configEntry, Long lastUpdated, String configCacheRoot, Session admin, Session session) {
        ResourceResolver resolver = resolverFactory.getResourceResolver(admin);
        Resource resource = resolver.getResource(configEntry.getContentPath());

        Image img = new Image(resource);
        img.setItemName(Image.NN_FILE, "image");
        img.setItemName(Image.PN_REFERENCE, "imageReference");
        img.setSelector("img");

        try {
            if(img.getLastModified() == null || lastUpdated < img.getLastModified().getTime().getTime()) {
                String src = img.getSrc();
                String parentPath = configCacheRoot + Text.getRelativeParent(src, 1);

                Node parent = JcrUtil.createPath(parentPath, "sling:Folder", admin);
                Node image = resolver.getResource(resource.getPath() + "/image").adaptTo(Node.class);
                JcrUtil.copy(image, parent, Text.getName(src));

                admin.save();

                return true;
            }
        } catch (RepositoryException e) {
            log.error("Unexpected error while updating logo: ", e);
        }

        return false;
    }
}
```

El `LogoUpdateHandler` implementa la clase `ContentUpdateHandler` de la interfaz `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` , que toma una serie de argumentos:

* A `ConfigEntry` instancia que proporciona acceso a la entrada de configuración, para la que se llama a este controlador, y sus propiedades.
* A `lastUpdated` marca de tiempo que indica la última vez que la sincronización de contenido actualizó su caché. El controlador no debe actualizar el contenido que no se haya modificado después de esa marca de tiempo.
* A `configCacheRoot` que especifica la ruta raíz de la caché. Todos los archivos actualizados deben almacenarse bajo esta ruta para agregarse al archivo zip.
* Una sesión administrativa que debe utilizarse para todas las operaciones de repositorio relacionadas con la caché.
* Una sesión de usuario que se puede utilizar para actualizar contenido en el contexto de un usuario determinado y, por lo tanto, para proporcionar un tipo de contenido personalizado.

Para implementar el controlador personalizado, cree primero una instancia de la clase Image basada en el recurso proporcionado en la entrada de configuración. Este es básicamente el mismo procedimiento que el componente de logotipo real en nuestras páginas. Se asegura de que la ruta de destino de la imagen sea la misma que la referenciada desde una página.

A continuación, compruebe si el recurso se ha modificado desde la última actualización. Las implementaciones personalizadas deben evitar actualizaciones innecesarias de la caché y devolver &quot;false&quot; si no cambia nada. Si se ha modificado el recurso, copie la imagen en la ubicación de destino esperada en relación con la raíz de la caché. Finalmente, `true` se devuelve para indicar al marco de trabajo que la caché se ha actualizado.

## Uso del contenido en el cliente {#using-the-content-on-the-client}

Para utilizar contenido en una aplicación móvil proporcionada por la sincronización de contenido, debe solicitar contenido a través de una conexión HTTP o HTTPS. Como resultado, el contenido recuperado (empaquetado en un archivo ZIP) se puede extraer y almacenar localmente en el dispositivo móvil. Tenga en cuenta que el contenido no solo hace referencia a datos, sino también a lógica, es decir, aplicaciones web completas; esto permite al usuario móvil ejecutar aplicaciones web recuperadas y los datos correspondientes, incluso sin conectividad de red.

La sincronización de contenido ofrece el contenido de forma inteligente: solo se entregan los cambios de datos desde la última sincronización de datos correcta, lo que reduce el tiempo necesario para la transferencia de datos. En la primera ejecución de una aplicación, se solicitan cambios de datos desde el 1 de enero de 1970, mientras que posteriormente solo se solicitan los datos que han cambiado desde la última sincronización correcta. AEM utiliza un marco de comunicación de cliente para iOS a fin de simplificar la comunicación y transferencia de datos, de modo que se requiera una cantidad mínima de código nativo para habilitar una aplicación web basada en iOS.

Todos los datos transferidos se pueden extraer en la misma estructura de directorio, no se requieren pasos adicionales (por ejemplo, comprobaciones de dependencia) al extraer datos. En el caso de iOS, todos los datos se almacenan en una subcarpeta dentro de la carpeta Documents de la aplicación de iOS.

Ruta de ejecución típica de una aplicación de AEM Mobile basada en iOS:

* El usuario inicia la aplicación en el dispositivo iOS.
* AEM La aplicación intenta conectarse al back-end de la aplicación y solicita cambios de datos desde la última ejecución de la aplicación.
* El servidor recupera los datos en cuestión y los comprime en un archivo.
* Los datos se devuelven al dispositivo cliente, donde se extraen en la carpeta de documentos.
* Se inicia/actualiza el componente UIWebView.

Si no se ha podido establecer una conexión, se mostrarán los datos descargados anteriormente.

### Recursos adicionales {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y un autor, consulte los siguientes recursos:

* [AEM Creación de contenido de la para AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)
* [Administración de contenido para utilizar AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
