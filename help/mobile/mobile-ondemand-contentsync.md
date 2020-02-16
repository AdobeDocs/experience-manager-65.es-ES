---
title: Móvil con sincronización de contenido
seo-title: Móvil con sincronización de contenido
description: Siga esta página para conocer la sincronización de contenido. Las páginas creadas en AEM se pueden usar como contenido de la aplicación, incluso cuando el dispositivo esté sin conexión. Además, dado que las páginas de AEM se basan en estándares web, funcionan en varias plataformas, lo que le permite incrustarlas en cualquier contenedor nativo. Esta estrategia reduce el esfuerzo de desarrollo y le permite actualizar fácilmente el contenido de la aplicación.
seo-description: Siga esta página para conocer la sincronización de contenido. Las páginas creadas en AEM se pueden usar como contenido de la aplicación, incluso cuando el dispositivo esté sin conexión. Además, dado que las páginas de AEM se basan en estándares web, funcionan en varias plataformas, lo que le permite incrustarlas en cualquier contenedor nativo. Esta estrategia reduce el esfuerzo de desarrollo y le permite actualizar fácilmente el contenido de la aplicación.
uuid: 11f74cc5-99a5-4186-9b60-b19351305432
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 8fb70ca4-86fc-477d-9773-35b84d5e85a8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Móvil con sincronización de contenido{#mobile-with-content-sync}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Utilice la sincronización de contenido para empaquetar el contenido de modo que se pueda utilizar en aplicaciones móviles nativas. Las páginas creadas en AEM se pueden usar como contenido de la aplicación, incluso cuando el dispositivo esté sin conexión. Además, dado que las páginas de AEM se basan en estándares web, funcionan en varias plataformas, lo que le permite incrustarlas en cualquier contenedor nativo. Esta estrategia reduce el esfuerzo de desarrollo y le permite actualizar fácilmente el contenido de la aplicación.

El marco de sincronización de contenido crea un archivo que contiene el contenido web. El contenido puede ser cualquier cosa desde páginas simples, imágenes y archivos PDF o aplicaciones web completas. La API de sincronización de contenido proporciona acceso al archivo de archivo desde aplicaciones móviles o procesos de compilación para que el contenido se pueda recuperar e incluir en la aplicación.

La siguiente secuencia de pasos ilustra un caso de uso típico de la sincronización de contenido:

1. El desarrollador de AEM crea una configuración de sincronización de contenido que especifica el contenido que se va a incluir.
1. El marco de sincronización de contenido recopila y almacena en caché el contenido.
1. En un dispositivo móvil, la aplicación móvil se inicia y solicita contenido al servidor, que se entrega en un archivo ZIP.
1. El cliente descomprime el contenido ZIP en el sistema de archivos local. La estructura de carpetas del archivo ZIP simula las rutas que un cliente (por ejemplo, un navegador) solicitaría normalmente al servidor.
1. El cliente abre el contenido en un navegador incrustado o lo utiliza de otra manera.
1. Posteriormente, el cliente solicita contenido actualizado desde el servidor. El marco de sincronización de contenido ofrece actualizaciones incrementales para reducir el tamaño y el tiempo de descarga, lo que puede ser importante para los dispositivos móviles debido al ancho de banda limitado o a los volúmenes de datos.

## Desarrollo de los controladores de sincronización de contenido {#developing-the-content-sync-handlers}

Algunas de las directrices para desarrollar controladores de sincronización de contenido son las siguientes:

* Los controladores deben implementar *com.day.cq.contentsync.handler.ContentUpdateHandler* (ya sea directamente o extendiendo una clase que lo haga)
* Los controladores pueden ampliar *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* El controlador solo debe informar de verdadero si actualiza la caché de ContentSync. Si se informa erróneamente como verdadero, AEM creará una actualización cuando la actualización no se haya producido realmente.
* El controlador solo debe actualizar la caché si el contenido ha cambiado. No escriba en la caché si no es necesario un blanco. Esto resulta en la creación de una actualización innecesaria.

>[!NOTE]
>
>Habilite *el registro* de depuración de ContentSync mediante las configuraciones del registrador OSGI en el paquete *com.day.cq.contentsync*. Esto permite rastrear qué controladores se ejecutaron y si actualizaron la caché e informaron de la actualización.

## Configuración del contenido de la sincronización de contenido {#configuring-the-content-sync-content}

Cree una configuración de sincronización de contenido para especificar el contenido del archivo ZIP que se entrega al cliente. Puede crear cualquier número de configuraciones de sincronización de contenido. Cada configuración tiene un nombre para fines de identificación.

Para crear una configuración de sincronización de contenido, agregue un `cq:ContentSyncConfig` nodo al repositorio, con la `sling:resourceType` propiedad establecida en `contentsync/config`. El `cq:ContentSyncConfig` nodo se puede ubicar en cualquier lugar del repositorio; sin embargo, los usuarios de la instancia de publicación de AEM deben tener acceso al nodo. Por lo tanto, debe agregar el nodo siguiente `/content`.

Para especificar el contenido del archivo ZIP de sincronización de contenido, agregue nodos secundarios al nodo cq:ContentSyncConfig. Las siguientes propiedades de cada nodo secundario identifican un elemento de contenido para incluir y cómo se procesa al agregarlo:

* `path`:: Ubicación del contenido.
* `type`:: Nombre del tipo de configuración que se va a utilizar para procesar el contenido. Hay varios tipos disponibles y se describen en la sección Tipos *de configuración*.

Consulte *Ejemplo de configuración* de sincronización de contenido para obtener más información.

Después de crear la configuración de Sincronización de contenido, ésta aparece en la consola Sincronización de contenido.

>[!NOTE]
>
>El marco de sincronización de contenido no comprueba que las dependencias de los recursos y los archivos relacionados con el diseño se incluyan en los paquetes de sincronización de contenido. Asegúrese de incluir todos los archivos necesarios en el archivo ZIP.

### Configuración del acceso a las descargas de sincronización de contenido {#configuring-access-to-content-sync-downloads}

Especifique un usuario o grupo que pueda descargar de la sincronización de contenido. Puede configurar el usuario o grupo predeterminado que se puede descargar de todas las cachés de sincronización de contenido, así como anular la configuración predeterminada y configurar el acceso para una configuración específica de sincronización de contenido.

Cuando AEM está instalado, los miembros del grupo de administradores pueden descargar de la sincronización de contenido de forma predeterminada.

#### Configuración del acceso predeterminado para las descargas de sincronización de contenido {#setting-the-default-access-for-content-sync-downloads}

El servicio Day CQ Content Sync Manager controla el acceso a la sincronización de contenido. Configure este servicio para especificar el usuario o grupo que puede descargar de la sincronización de contenido de forma predeterminada.

Si está [configurando el servicio mediante la consola](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)Web, escriba el nombre del usuario o grupo como el valor de la propiedad Autorizable de caché de reserva.

Si está [configurando en el repositorio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository), utilice la siguiente información sobre el servicio:

* PID: com.day.cq.contentsync.impl.ContentSyncManagerImpl
* Nombre de propiedad: contentsync.fallback.autorizable

#### Anulación del acceso de descarga para una caché de sincronización de contenido {#overriding-download-access-for-a-content-sync-cache}

Para configurar el acceso de descarga para una configuración específica de Sincronización de contenido, agregue la siguiente propiedad al `cq:ContentSyncConfig` nodo:

* Nombre: autorizable
* Tipo: Cadena
* Valor: Nombre del usuario o grupo que se puede descargar.

Por ejemplo, la aplicación permite a los usuarios instalar actualizaciones directamente desde la sincronización de contenido. Para permitir que todos los usuarios descarguen la actualización, debe establecer el valor de la propiedad autorizable en `everyone`.

Si el `cq:ContentSyncConfig` nodo no tiene una propiedad autorizada, el usuario o grupo predeterminado configurado para la propiedad Autorizable de caché de reserva del servicio Day CQ Content Sync Manager determina quién puede descargar.

### Configuración del usuario para actualizar una caché de sincronización de contenido {#configuring-the-user-for-updating-a-content-sync-cache}

Cuando un usuario realiza una actualización en la caché de sincronización de contenido, una cuenta de usuario específica realiza la acción en nombre del usuario. El usuario anónimo actualiza todas las cachés de sincronización de contenido de forma predeterminada.

Puede anular el usuario predeterminado y especificar un usuario o grupo que actualice una caché de sincronización de contenido específica.

Para anular el usuario predeterminado, especifique un usuario o grupo que realice actualizaciones para una configuración específica de Sincronización de contenido agregando la siguiente propiedad al nodo cq:ContentSyncConfig:

* Nombre: `updateuser`
* Tipo: `String`
* Valor: Nombre del usuario o grupo que puede realizar las actualizaciones.

Si el `cq:ContentSyncConfig` nodo no tiene ninguna `updateuser` propiedad, el `anonymous` usuario predeterminado actualiza la caché.

### Tipos de configuración {#configuration-types}

El procesamiento puede ir desde el procesamiento de JSON simple hasta el procesamiento completo de las páginas, incluidos sus recursos a los que se hace referencia. Esta sección enumera los tipos de configuración disponibles y sus parámetros específicos:

**copiar** simplemente copiar archivos y carpetas.

* **path** : si la ruta apunta a un solo archivo, solo se copia el archivo. Si apunta a una carpeta (esto incluye nodos de página), se copiarán todos los archivos y carpetas siguientes.

**contenido** Representar contenido mediante el procesamiento [de solicitudes](/help/sites-developing/the-basics.md#sling-request-processing)Sling estándar.

* **path** : ruta al recurso que debe generarse.
* **extensión** : extensión que debe utilizarse en la solicitud. Los ejemplos comunes son *html* y *json*, pero es posible cualquier otra extensión.

* **selector** : selectores opcionales separados por puntos. Algunos ejemplos comunes son *el toque* para procesar versiones móviles de una página o el *infinito* para la salida JSON.

**clientlib** Package a Javascript o CSS client library.

* **path** : ruta a la raíz de la biblioteca del cliente.
* **extensión** : tipo de biblioteca de cliente. En este momento, debe establecerse en *js* o *css* .

**activos**

Recopilar representaciones originales de recursos.

* **path** : ruta a una carpeta de recursos debajo de /content/dam.

**imagen** Recopilar una imagen.

* **path** : ruta a un recurso de imagen.

El tipo de imagen se utiliza para incluir el logotipo We Retail en el archivo zip.

**páginas** Procesar páginas de AEM y recopilar recursos a los que se hace referencia.

* **ruta** : ruta a una página.
* **extensión** : extensión que debe utilizarse en la solicitud. Para las páginas esto es casi siempre *html*, pero otras son aún posibles.

* **selector** : selectores opcionales separados por puntos. Los ejemplos habituales son *táctiles* para procesar versiones móviles de una página.

* **deep** - Propiedad booleana opcional que determina si también se deben incluir páginas secundarias. The default value is *true.*

* **includeImages** : propiedad booleana opcional que determina si se deben incluir imágenes. The default value is *true*.

   De forma predeterminada, solo se consideran para la inclusión los componentes de imagen con un tipo de recurso de base/componentes/imagen. Puede agregar más tipos de recursos configurando el controlador **de actualización de páginas WCM de CQ** Day en la consola Web.

**reescribir** El nodo reescribir define cómo se reescriben los vínculos en la página exportada. Los vínculos reescritos pueden apuntar a los archivos incluidos en el archivo zip o a los recursos del servidor.

El `rewrite` nodo debe estar situado debajo del `page` nodo.

El `rewrite` nodo puede tener una o varias de las siguientes propiedades:

* `clientlibs`:: reescribe las rutas de clientlibs.

* `images`:: reescribe las rutas de imágenes.
* `links`:: reescribe las rutas de los vínculos.

Cada propiedad puede tener uno de los siguientes valores:

* `REWRITE_RELATIVE`:: reescribe la ruta con una posición relativa al archivo page.html en el sistema de archivos.

* `REWRITE_EXTERNAL`:: reescribe la ruta señalando al recurso en el servidor, utilizando el servicio [AEM](/help/sites-developing/externalizer.md)Externalizer.

El servicio AEM **PathRewriterTransformerFactory** permite configurar los atributos HTML específicos que se reescribirán. El servicio se puede configurar en la consola web y tiene una configuración para cada propiedad del `rewrite` nodo: `clientlibs`, `images` y `links`.

Esta función se agregó en AEM 5.5.

### Ejemplo de configuración de sincronización de contenido {#example-content-sync-configuration}

La lista siguiente muestra una configuración de ejemplo para la sincronización de contenido.

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

**etc.designs.default y etc.designs.mobile** Las dos primeras entradas de la configuración deberían ser bastante obvias. Como vamos a incluir varias páginas móviles, necesitamos los archivos de diseño relacionados debajo de /etc/designs. Y como no se requiere un procesamiento adicional, la copia es suficiente.

**events.plist** Esta entrada es un poco especial. Como se mencionó en la introducción, la aplicación debe proporcionar una vista de mapa con marcadores de la ubicación de los eventos. Vamos a proporcionar la información de ubicación necesaria como un archivo separado en formato PLIST. Para que esto funcione, el componente de lista de eventos que se utiliza en la página de índice tiene una secuencia de comandos denominada plist.jsp. Esta secuencia de comandos se ejecuta cuando se solicita el recurso del componente con la extensión .plist. Como de costumbre, la ruta de los componentes se proporciona en la propiedad path y el tipo se establece en content, ya que queremos aprovechar el procesamiento [de solicitudes](/help/sites-developing/the-basics.md#sling-request-processing)Sling.

**events.touch.html** A continuación se muestran las páginas reales que se mostrarán en la aplicación. La propiedad path se establece en la página raíz del evento. También se incluirán todas las páginas de eventos debajo de esa página, ya que la propiedad deep tiene el valor predeterminado true. Utilizamos las páginas como tipo de configuración, para que se incluyan todas las imágenes u otros archivos a los que se pueda hacer referencia desde una imagen o un componente de descarga en una página. Además, la configuración del selector de contacto nos proporciona una versión móvil de las páginas. La configuración en el paquete de funciones contiene más entradas de este tipo, pero aquí se dejan de lado por simplicidad.

**logo** El tipo de configuración del logotipo no se ha mencionado hasta ahora y no es ninguno de los tipos integrados. Sin embargo, el marco de sincronización de contenido puede ampliarse hasta cierto punto y este es un ejemplo de ello, que se tratará en la siguiente sección.

**manifest** A menudo es deseable incluir algún tipo de metadatos en el archivo zip, como la página de inicio del contenido, por ejemplo. Sin embargo, la codificación de dicha información evita que pueda cambiarla fácilmente más adelante. El marco de sincronización de contenido admite este caso de uso buscando un nodo de manifiesto en la configuración, que se identifica simplemente por su nombre y no requiere un tipo de configuración. Cada propiedad definida en ese nodo en particular se agrega a un archivo, que también se denomina manifest y reside en la raíz del archivo zip.

En el ejemplo, se supone que la página con la lista de eventos es la página inicial. Esta información se proporciona en la propiedad **indexPage** y, por lo tanto, se puede cambiar fácilmente en cualquier momento. Una segunda propiedad define la ruta del archivo *events.plist* . Como veremos más adelante, la aplicación cliente ahora puede leer el manifiesto y actuar según él.

Tan pronto como se configure la configuración, el contenido se puede descargar con un navegador o con cualquier otro cliente HTTP, o si está desarrollando para iOS, puede utilizar la biblioteca de cliente dedicada de WAppKitSync. La ubicación de descarga está formada por la ruta de la configuración y la extensión *.zip* , por ejemplo, al trabajar con una instancia local de AEM: *http://localhost:4502/content/weretail_go.zip*

### Consola de sincronización de contenido {#the-content-sync-console}

La consola de sincronización de contenido enumera todas las configuraciones de sincronización de contenido del repositorio (todos los nodos del tipo `cq:ContentSyncConfig`) y para cada configuración puede hacer lo siguiente:

* Actualice la caché.
* Borre la caché.
* Descargue un zip completo.
* Descargue un archivo comprimido diferente entre ahora y una fecha y hora específicas.

Puede resultar útil para el desarrollo y la solución de problemas.

Se puede acceder a la consola en:

`http://localhost:4502/libs/cq/contentsync/content/console.html`

Tiene el siguiente aspecto:

![chlimage_1-50](assets/chlimage_1-50.png)

### Ampliación del marco de sincronización de contenido {#extending-the-content-sync-framework}

Aunque el número de opciones de configuración ya es bastante amplio, es posible que no cubra todos los requisitos de su caso de uso específico. Esta sección describe los puntos de extensión del marco de sincronización de contenido y cómo crear tipos de configuración personalizados.

Para cada tipo de configuración, hay un controlador *de actualización de contenido*, que es una fábrica de componentes OSGi registrada para ese tipo específico. Estos controladores recopilan contenido, lo procesan y lo agregan a una caché que mantiene el marco de sincronización de contenido. Implemente la siguiente interfaz o clase base abstracta:

* `com.day.cq.contentsync.handler.ContentUpdateHandler` - Interfaz que todos los controladores de actualización necesitan implementar
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` - Una clase abstracta que simplifica la representación de recursos mediante Sling

Registre su clase como fábrica de componentes OSGi e impleméntelo en el contenedor OSGi en un paquete. Esto se puede hacer con el complemento [Maven SCR](https://felix.apache.org/site/apache-felix-maven-scr-plugin.html) , ya sea mediante etiquetas JavaDoc o anotaciones. El siguiente ejemplo muestra la versión de JavaDoc:

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

Observe que la definición de *fábrica* contiene la interfaz común y el tipo personalizado separados por barras. Esta estrategia permite que el marco de sincronización de contenido encuentre y cree una instancia de la clase personalizada, ya que reconoce el tipo personalizado en una entrada de configuración. La siguiente sección proporciona un ejemplo concreto de un controlador de actualizaciones personalizado.

>[!CAUTION]
>
>Al generar la clase base AbstractSlingResourceUpdateHandler, debe agregar la definición *inherit* . De lo contrario, el contenedor OSGi no establecerá las referencias necesarias que se declaran en la clase base.

### Implementación de un controlador de actualización personalizado {#implementing-a-custom-update-handler}

Cada página de We.Retail Mobile contiene un logotipo en la esquina superior izquierda que nos gustaría incluir en el archivo zip, por supuesto. Sin embargo, para la optimización de la caché, AEM no hace referencia a la ubicación real del archivo de imagen en el repositorio, lo que nos impide utilizar simplemente el tipo de configuración de **copia** . Lo que necesitamos hacer es proporcionar nuestro propio tipo de configuración de **logotipo** que permita que la imagen esté disponible en la ubicación solicitada por AEM. La siguiente lista de códigos muestra la implementación completa del controlador de actualización de logotipo:

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

La `LogoUpdateHandler` clase implementa el `ContentUpdateHandler` método `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` de la interfaz, que toma una serie de argumentos:

* Una `ConfigEntry` instancia que proporciona acceso a la entrada de configuración, para la que se llama a este controlador, y a sus propiedades.
* Marca de `lastUpdated` hora que indica la última vez que la sincronización de contenido actualizó su caché. El controlador no debe actualizar el contenido que no se haya modificado después de esa marca de tiempo.
* Un `configCacheRoot` argumento que especifica la ruta raíz de la caché. Todos los archivos actualizados deben almacenarse debajo de esta ruta para agregarlos al archivo zip.
* Sesión administrativa que debe utilizarse para todas las operaciones de repositorio relacionadas con la caché.
* Sesión de usuario que se puede utilizar para actualizar contenido en el contexto de un determinado usuario y, por lo tanto, para proporcionar un tipo de contenido personalizado.

Para implementar el controlador personalizado, primero cree una instancia de la clase Image basada en el recurso proporcionado en la entrada de configuración. Básicamente, este es el mismo procedimiento que el componente del logotipo real en nuestras páginas. Se asegura de que la ruta de destino de la imagen sea la misma que la que se hace referencia desde una página.

A continuación, compruebe si el recurso se modificó desde la última actualización. Las implementaciones personalizadas deben evitar actualizaciones innecesarias de la caché y devolver false si no cambia nada. Si se modificó el recurso, copie la imagen en la ubicación de destino esperada en relación con la raíz de caché. Finalmente, `true` se devuelve para indicar al marco de trabajo que se actualizó la caché.

## Uso del contenido en el cliente {#using-the-content-on-the-client}

Para utilizar contenido en una aplicación móvil proporcionada por Content Sync, debe solicitar contenido a través de una conexión HTTP o HTTPS. Como resultado, el contenido recuperado (empaquetado en un archivo ZIP) se puede extraer y almacenar localmente en el dispositivo móvil. Tenga en cuenta que el contenido no sólo se refiere a los datos sino también a la lógica, es decir, a las aplicaciones web completas; de este modo, el usuario móvil puede ejecutar las aplicaciones web recuperadas y los datos correspondientes incluso sin conectividad de red.

Content Sync ofrece contenido de forma inteligente: Sólo se entregan los cambios de datos desde la última sincronización de datos correcta, lo que reduce el tiempo necesario para la transferencia de datos. La primera vez que se ejecuta una aplicación, se solicitan cambios en los datos desde el 1 de enero de 1970, mientras que posteriormente sólo se solicitan los datos que hayan cambiado desde la última sincronización correcta. AEM utiliza un marco de comunicación de cliente para iOS a fin de simplificar la comunicación y la transferencia de datos, de modo que se requiera una cantidad mínima de código nativo para habilitar una aplicación web basada en iOS.

Todos los datos transferidos se pueden extraer en la misma estructura de directorio, no se requieren pasos adicionales (por ejemplo, comprobaciones de dependencia) al extraer datos. En el caso de iOS, todos los datos se almacenan en una subcarpeta dentro de la carpeta Documents de la aplicación iOS.

Ruta de ejecución típica de una aplicación de AEM Mobile basada en iOS:

* El usuario inicia la aplicación en un dispositivo iOS.
* La aplicación intenta conectarse al servidor AEM y solicita cambios en los datos desde la última ejecución.
* El servidor recupera los datos en cuestión y los comprime en un archivo.
* Los datos se devuelven al dispositivo cliente, donde se extraen en la carpeta de documentos.
* Se inicia/actualiza el componente UIWebView.

Si no se pudo establecer una conexión, se mostrarán los datos descargados anteriormente.

### Additional Resources {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y un autor, consulte los siguientes recursos:

* [Creación de contenido de AEM para los servicios bajo demanda de AEM Mobile](/help/mobile/mobile-apps-ondemand.md)
* [Administración de contenido para utilizar los servicios bajo demanda de AEM Mobile](/help/mobile/aem-mobile.md)

