---
title: Sincronización de contenido para Adobe PhoneGap Enterprise con Adobe Experience Manager
description: Obtenga información acerca de la sincronización de contenido para Adobe PhoneGap Enterprise con Adobe Experience Manager.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
docset: aem65
exl-id: 2cadd9c5-4335-48d0-8d1c-941fca717409
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '2924'
ht-degree: 0%

---

# Móvil con sincronización de contenido{#mobile-with-content-sync}

{{ue-over-mobile}}

>[!NOTE]
>
>Este documento forma parte de la guía [Introducción a Adobe Experience Manager AEM () Mobile](/help/mobile/getting-started-aem-mobile.md), un punto de partida recomendado para la referencia de AEM Mobile.

Utilice la sincronización de contenido para empaquetar contenido de modo que se pueda utilizar en aplicaciones móviles nativas. AEM Las páginas creadas en la aplicación se pueden usar como contenido de la aplicación, incluso cuando el dispositivo está sin conexión. AEM Además, dado que las páginas de la se basan en estándares web, funcionan en plataformas múltiples, lo que permite incrustarlas en cualquier envoltorio nativo. Esta estrategia reduce el esfuerzo de desarrollo y le permite actualizar fácilmente el contenido de la aplicación.

>[!NOTE]
>
>AEM AEM Las aplicaciones de PhoneGap que creas con Herramientas de ya están configuradas para usar páginas de la red social como contenido a través de Sincronización de contenido.

El marco de trabajo de sincronización de contenido crea un archivo de almacenamiento que contiene el contenido web. El contenido puede ser desde páginas simples, imágenes y archivos de PDF, o aplicaciones web completas. La API de sincronización de contenido proporciona acceso al archivo desde aplicaciones móviles o procesos de compilación para que el contenido se pueda recuperar e incluir en la aplicación.

La siguiente secuencia de pasos ilustra un caso de uso típico para la sincronización de contenido:

1. AEM El desarrollador de crea una configuración de sincronización de contenido que especifica el contenido que se va a incluir.
1. El marco de trabajo Sincronización de contenido recopila y almacena en caché el contenido.
1. En un dispositivo móvil, la aplicación móvil se inicia y solicita contenido al servidor, que se entrega en un archivo ZIP.
1. El cliente desempaqueta el contenido ZIP en el sistema de archivos local. La estructura de carpetas del archivo ZIP simula las rutas que un cliente (por ejemplo, un explorador) solicitaría normalmente al servidor.
1. El cliente abre el contenido en un explorador incrustado o lo utiliza de alguna otra manera.
1. Posteriormente, el cliente solicita contenido actualizado desde el servidor. El marco de trabajo de sincronización de contenido ofrece actualizaciones incrementales para reducir el tamaño y el tiempo de descarga, lo que puede ser importante para dispositivos móviles debido al ancho de banda limitado o los volúmenes de datos.

>[!NOTE]
>
>Para obtener más información sobre las directrices para desarrollar controladores de sincronización de contenido, consulte [Desarrollo de controladores de sincronización de contenido](/help/mobile/contentsync-app-handlers.md).

## Configuración del contenido de sincronización de contenido {#configuring-the-content-sync-content}

Cree una configuración de sincronización de contenido para especificar el contenido del archivo ZIP que se envía al cliente. Puede crear cualquier cantidad de configuraciones de sincronización de contenido. Cada configuración tiene un nombre para fines de identificación.

Para crear una configuración de sincronización de contenido, agregue un nodo `cq:ContentSyncConfig` al repositorio, con la propiedad `sling:resourceType` establecida en `contentsync/config`. AEM El nodo `cq:ContentSyncConfig` se puede ubicar en cualquier lugar del repositorio; sin embargo, los usuarios de la instancia de publicación de la deben tener acceso al nodo. Por lo tanto, debe agregar el nodo debajo de `/content`.

Para especificar el contenido del archivo ZIP de sincronización de contenido, agregue nodos secundarios al nodo cq:ContentSyncConfig. Las siguientes propiedades de cada nodo secundario identifican un elemento de contenido para incluir y cómo se procesa al agregarlo:

* `path`: la ubicación del contenido.
* `type`: nombre del tipo de configuración que se utilizará para procesar el contenido. Hay varios tipos disponibles y se describen en Tipos de configuración.

Consulte Ejemplo de configuración de sincronización de contenido.

Después de crear la configuración de sincronización de contenido, esta aparece en la consola Sincronización de contenido.

>[!NOTE]
>
>El marco de trabajo de sincronización de contenido no comprueba que las dependencias de los recursos y los archivos relacionados con el diseño estén incluidos en los paquetes de sincronización de contenido. Asegúrese de incluir todos los archivos necesarios en el archivo ZIP.

### Configuración del acceso a las descargas de sincronización de contenido {#configuring-access-to-content-sync-downloads}

Especifique un usuario o grupo que pueda descargar desde Sincronización de contenido. Puede configurar el usuario o grupo predeterminado que puede descargar de todas las cachés de sincronización de contenido, así como anular el valor predeterminado y configurar el acceso para una configuración de sincronización de contenido específica.

AEM Cuando se instala la sincronización de contenido, los miembros del grupo del administrador pueden descargar desde Sincronización de contenido de forma predeterminada.

### Configuración del acceso predeterminado para descargas de sincronización de contenido {#setting-the-default-access-for-content-sync-downloads}

El servicio Administrador de sincronización de contenido de CQ diario controla el acceso a la sincronización de contenido. Configure este servicio para especificar el usuario o grupo que puede descargar desde Sincronización de contenido de forma predeterminada.

Si está [configurando el servicio mediante la consola web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), escriba el nombre del usuario o grupo como el valor de la propiedad autorizable Caché de reserva.

Si está [configurando en el repositorio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository), use la siguiente información sobre el servicio:

* PID: com.day.cq.contentsync.impl.ContentSyncManagerImpl
* Nombre de propiedad: contentsync.fallback.authorizable

#### Anulación del acceso de descarga para una caché de sincronización de contenido {#overriding-download-access-for-a-content-sync-cache}

Para configurar el acceso de descarga para una configuración de sincronización de contenido específica, agregue la siguiente propiedad al nodo `cq:ContentSyncConfig`:

* Nombre: autorizable
* Tipo: cadena
* Valor: Nombre del usuario o grupo que puede descargar.

Por ejemplo, la aplicación permite a los usuarios instalar actualizaciones directamente desde la sincronización de contenido. Para permitir que todos los usuarios descarguen la actualización, establezca el valor de la propiedad autorizable en `everyone`.

Si el nodo `cq:ContentSyncConfig` no tiene una propiedad autorizable, el usuario o grupo predeterminado configurado para la propiedad Autorizable de caché de reserva del servicio Administrador de sincronización de contenido de CQ Day determina quién puede descargar.

### Configuración del usuario para actualizar una caché de sincronización de contenido {#configuring-the-user-for-updating-a-content-sync-cache}

Cuando un usuario realiza una actualización de la caché de sincronización de contenido, una cuenta de usuario específica realiza la acción en nombre del usuario. El usuario anónimo actualiza todas las cachés de sincronización de contenido de forma predeterminada.

Puede anular el usuario predeterminado y especificar un usuario o grupo que actualice una caché de sincronización de contenido específica.

Para anular el usuario predeterminado, especifique un usuario o grupo que realice actualizaciones para una configuración de sincronización de contenido específica agregando la siguiente propiedad al nodo cq:ContentSyncConfig:

* Nombre: updateuser
* Tipo: cadena
* Valor: Nombre del usuario o grupo que puede realizar las actualizaciones.

Si el nodo cq:ContentSyncConfig no tiene la propiedad `updateuser`, el usuario anónimo predeterminado actualiza la caché.

### Tipos de configuración {#configuration-types}

El procesamiento puede abarcar desde el procesamiento de JSON simple hasta el procesamiento completo de páginas, incluidos los recursos a los que se hace referencia. En esta sección se enumeran los tipos de configuración disponibles y sus parámetros específicos:

**copiar** Simplemente copia archivos y carpetas.

* **ruta**: si la ruta apunta a un solo archivo, solo se copia el archivo. Si apunta a una carpeta (incluidos los nodos de página), se copiarán todos los archivos y carpetas siguientes.

**content**: procese contenido mediante el procesamiento estándar de solicitudes de Sling.

* **ruta** - Ruta de acceso al recurso que debería ser el resultado.
* **extensión** - Extensión que debe usarse en la solicitud. Algunos ejemplos comunes son *html* y *json*, pero cualquier otra extensión es posible.

* **selector**: selectores opcionales separados por puntos. Algunos ejemplos comunes son *touch* para procesar versiones móviles de una página o *infinity* para la salida JSON.

**clientlib**: empaquete una biblioteca de cliente JavaScript o CSS.

* **ruta** - Ruta a la raíz de la biblioteca de cliente.
* **extensión** - Tipo de biblioteca de cliente. Debe establecerse en *js* o *css* en este momento.

* **includeFolders** - Type es una matriz de cadenas y permite al usuario especificar carpetas adicionales para analizar en la biblioteca de cliente y recuperar archivos (como fuentes personalizadas).

**recursos** - Recopilar representaciones originales de recursos.

* **ruta** - Ruta a una carpeta de recursos debajo de /content/dam.
* **representaciones**: el tipo es una matriz de cadenas que permite al usuario especificar qué representaciones utilizar en lugar de la imagen predeterminada. La siguiente lista resume algunas representaciones integradas, pero también puede utilizar cualquier representación creada por el flujo de trabajo:

   * *original*
   * *cq5dam.thumbnail.48.48.png*
   * *cq5dam.thumbnail.319.319.png*
   * *cq5dam.thumbnail.140.100.png*
   * *cq5dam.web.1280.1280.png*

**imagen** - Recopilar una imagen.

* **ruta** - Ruta a un recurso de imagen.

El tipo de imagen se utiliza para incluir el logotipo de We.Retail en el archivo zip.

AEM **páginas** - Procesar páginas de la y recopilar recursos a los que se hace referencia.

* **ruta** - Ruta a una página.
* **extensión** - Extensión que debe usarse en la solicitud. Para las páginas, esto es casi siempre *html*, pero otros son posibles.

* **selector**: selectores opcionales separados por puntos. Algunos ejemplos comunes son *touch* para procesar versiones móviles de una página.

* **deep**: propiedad booleana opcional que determina si también se deben incluir las páginas secundarias. El valor predeterminado es *true.*

* **includeImages**: propiedad booleana opcional que determina si se deben incluir las imágenes. El valor predeterminado es *true*.
De forma predeterminada, solo se tienen en cuenta para la inclusión los componentes de imagen con un tipo de recurso de foundation/components/image. Puede agregar más tipos de recursos configurando el controlador de actualización de páginas WCM **Day CQ** en la consola web.

**rewrite**: el nodo de reescritura define cómo se reescriben los vínculos en la página exportada. Los vínculos reescritos pueden apuntar a los archivos incluidos en el archivo zip o a los recursos del servidor.

El nodo `rewrite` debe estar ubicado debajo del nodo `page`.

El nodo `rewrite` puede tener una o más de las siguientes propiedades:

* `clientlibs`: reescribe las rutas clientlibs.

* `images`: reescribe las rutas de las imágenes.
* `links`: reescribe las rutas de los vínculos.

Cada propiedad puede tener uno de los siguientes valores:

* `REWRITE_RELATIVE`: reescribe la ruta de acceso con una posición relativa al archivo .html de la página en el sistema de archivos.

* AEM `REWRITE_EXTERNAL`: reescribe la ruta de acceso señalando al recurso del servidor mediante el servicio [ExternalizerService](/help/sites-developing/externalizer.md) de la.

AEM El servicio de correo llamado **PathRewriterTransformerFactory** le permite configurar los atributos html específicos que se reescribirán. El servicio se puede configurar en la consola web y tiene una configuración para cada propiedad del nodo `rewrite`: `clientlibs`, `images` y `links`.

AEM Esta función se añadió en la versión 5.5 de.

### Ejemplo de configuración de sincronización de contenido {#example-content-sync-configuration}

La lista siguiente muestra un ejemplo de configuración para la sincronización de contenido.

```java
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

**etc.designs.default y etc.designs.mobile**: las dos primeras entradas de la configuración son obvias. Como vamos a incluir varias páginas móviles, necesitamos los archivos de diseño relacionados debajo de /etc/designs. Y como no se requiere ningún procesamiento adicional, la copia es suficiente.

**events.plist**: esta entrada es un poco especial. Como se mencionó en la introducción, la aplicación debe proporcionar una vista de mapa con marcadores de las ubicaciones de los eventos. Vamos a proporcionar la información de ubicación necesaria como un archivo independiente en formato PLIST. Para que esto funcione, el componente de lista de eventos que se utiliza en la página de índice tiene un script llamado plist.jsp. Este script se ejecuta cuando se solicita el recurso del componente con la extensión `.plist`. Como de costumbre, la ruta de los componentes se da en la propiedad path y el tipo se establece en content, ya que queremos utilizar el procesamiento de solicitudes de Sling.

**events.touch.html**: a continuación, aparecerán las páginas que se muestran en la aplicación. La propiedad path se establece en la página raíz de los eventos. Todas las páginas de eventos debajo de esa página también se incluyen, ya que la propiedad deep tiene el valor predeterminado true. Utilizamos páginas como tipo de configuración, de modo que se incluya cualquier imagen u otro archivo al que se pueda hacer referencia desde un componente de imagen o descarga de una página. Además, configurar el selector táctil nos da una versión móvil de las páginas. La configuración del paquete de funciones contiene más entradas de este tipo, pero se omiten por simplicidad.

**logotipo**: el tipo de configuración del logotipo no se ha mencionado hasta el momento y no es ninguno de los tipos integrados. Sin embargo, el marco de trabajo de sincronización de contenido es extensible hasta cierto punto y este es un ejemplo de ello, que se tratará en la siguiente sección.

**manifiesto**: A menudo es deseable incluir algún tipo de metadatos en el archivo zip, como la página de inicio del contenido, por ejemplo. Sin embargo, codificar dicha información impide cambiarla fácilmente más adelante. El marco de trabajo de sincronización de contenido admite este caso de uso al buscar un nodo de manifiesto en la configuración, que se identifica con el nombre y no requiere un tipo de configuración. Todas las propiedades definidas en ese nodo en particular se agregan a un archivo, que también se denomina manifest y reside en la raíz del archivo zip.

En el ejemplo, se supone que la página con la lista de eventos es la página inicial. Esta información se proporciona en la propiedad **indexPage** y, por lo tanto, se puede cambiar fácilmente en cualquier momento. Una segunda propiedad define la ruta del archivo *events.plist*. Como vemos más adelante, la aplicación cliente ahora puede leer el manifiesto y actuar según él.

Cuando se establece la configuración, el contenido se puede descargar con un explorador o con cualquier otro cliente HTTP, o si está desarrollando para iOS, puede utilizar la biblioteca de cliente de WAppKitSync dedicada. AEM La ubicación de descarga se compone de la ruta de acceso de la configuración y de la extensión *.zip*, por ejemplo, al trabajar con una instancia de local: *https://localhost:4502/content/weretail_go.zip*

### La consola de sincronización de contenido {#the-content-sync-console}

La consola Sincronización de contenido enumera todas las configuraciones de Sincronización de contenido en el repositorio (todos los nodos de tipo `cq:ContentSyncConfig`) y para cada configuración le permite hacer lo siguiente:

* Actualice la caché.
* Borre la caché.
* Descargue un archivo zip completo.
* Descargue un zip de diferencia entre ahora y una fecha y hora específicas.

Puede resultar útil para el desarrollo y la solución de problemas.

Se puede acceder a la consola en:

`https://localhost:4502/libs/cq/contentsync/content/console.html`

Tiene el siguiente aspecto:

![chlimage_1](assets/chlimage_1.png)

### Ampliación del marco de sincronización de contenido {#extending-the-content-sync-framework}

Aunque la cantidad de opciones de configuración ya es extensa, es posible que no cubra todos los requisitos de su caso de uso específico. En esta sección se describen los puntos de extensión del marco de trabajo de sincronización de contenido y cómo crear tipos de configuración personalizados.

Para cada tipo de configuración, hay un *controlador de actualización de contenido*, que es un generador de componentes OSGi registrado para ese tipo específico. Estos controladores recopilan contenido, lo procesan y lo agregan a una caché que mantiene el marco de trabajo de sincronización de contenido. Implemente la siguiente interfaz o clase base abstracta:

* `com.day.cq.contentsync.handler.ContentUpdateHandler`: interfaz que todos los controladores de actualización deben implementar
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler`: una clase abstracta que simplifica la representación de recursos mediante Sling

Registre su clase como fábrica de componentes OSGi e impleméntelo en el contenedor OSGi en un paquete. Esto se puede hacer con el [complemento Maven SCR](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/apache-felix-maven-scr-plugin-use.html), ya sea con etiquetas JavaDoc o anotaciones. El siguiente ejemplo muestra la versión de JavaDoc:

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

Observe que la definición de *factory* contiene la interfaz común y el tipo personalizado separados por una barra diagonal. Esta estrategia permite al marco de trabajo de sincronización de contenido buscar y crear una instancia de la clase personalizada a medida que reconoce el tipo personalizado en una entrada de configuración. En la siguiente sección se muestra un ejemplo concreto de un controlador de actualización personalizado.

>[!CAUTION]
>
>Cuando se basa en la clase base AbstractSlingResourceUpdateHandler, debe agregar la definición *inherit*. De lo contrario, el contenedor OSGi no establecerá las referencias necesarias declaradas en la clase base.

### Implementar un controlador de actualización personalizado {#implementing-a-custom-update-handler}

Cada página de We.Retail Mobile contiene un logotipo en la esquina superior izquierda que queremos incluir en el archivo zip. AEM Sin embargo, para la optimización de caché, no hace referencia a la ubicación real del archivo de imagen en el repositorio, lo que nos impide usar simplemente el tipo de configuración **copy**. AEM Lo que debemos hacer en su lugar es proporcionar nuestro propio tipo de configuración de **logo** que haga que la imagen esté disponible en la ubicación solicitada por el usuario. La siguiente lista de códigos muestra la implementación completa del controlador de actualización de logotipos:

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

La clase `LogoUpdateHandler` implementa el método `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` de la interfaz `ContentUpdateHandler`, que toma varios argumentos:

* Instancia de `ConfigEntry` que proporciona acceso a la entrada de configuración, para la que se llama a este controlador, y a sus propiedades.
* Una marca de tiempo `lastUpdated` que indica la última vez que la sincronización de contenido actualizó su caché. El controlador no debe actualizar el contenido que no se haya modificado después de esa marca de tiempo.
* Argumento `configCacheRoot` que especifica la ruta de acceso raíz de la caché. Todos los archivos actualizados deben almacenarse bajo esta ruta para agregarse al archivo zip.
* Una sesión administrativa que debe utilizarse para todas las operaciones de repositorio relacionadas con la caché.
* Una sesión de usuario que se puede utilizar para actualizar contenido en el contexto de un usuario determinado y, por lo tanto, para proporcionar un tipo de contenido personalizado.

Para implementar el controlador personalizado, cree primero una instancia de la clase Image basada en el recurso proporcionado en la entrada de configuración. Este es básicamente el mismo procedimiento que el componente de logotipo real en nuestras páginas. Se asegura de que la ruta de destino de la imagen sea la misma que la referenciada desde una página.

A continuación, compruebe si el recurso se ha modificado desde la última actualización. Las implementaciones personalizadas deben evitar actualizaciones innecesarias de la caché y devolver &quot;false&quot; si no cambia nada. Si se ha modificado el recurso, copie la imagen en la ubicación de destino esperada en relación con la raíz de la caché. Por último, se devuelve `true` para indicar al marco de trabajo que la caché se ha actualizado.

## Uso del contenido en el cliente {#using-the-content-on-the-client}

Para utilizar contenido en una aplicación móvil proporcionada por la sincronización de contenido, debe solicitar contenido mediante una conexión HTTP o HTTPS. Como resultado, el contenido recuperado (empaquetado en un archivo ZIP) se puede extraer y almacenar localmente en el dispositivo móvil. El contenido no solo se refiere a los datos, sino también a la lógica, es decir, a las aplicaciones web completas; por lo tanto, permite al usuario móvil ejecutar aplicaciones web recuperadas y los datos correspondientes, incluso sin conectividad de red.

La sincronización de contenido ofrece el contenido de forma inteligente: solo se entregan los cambios de datos desde la última sincronización de datos correcta, lo que reduce el tiempo necesario para la transferencia de datos. En la primera ejecución de los datos de una aplicación, se solicitan cambios desde el 1 de enero de 1970, mientras que posteriormente solo se solicitan los datos que han cambiado desde la última sincronización correcta. AEM utiliza un marco de comunicación de cliente para iOS para simplificar la comunicación y transferencia de datos, de modo que se requiera una cantidad mínima de código nativo para habilitar una aplicación web basada en iOS.

Todos los datos transferidos se pueden extraer en la misma estructura de directorio, no se requieren pasos adicionales (por ejemplo, comprobaciones de dependencia) al extraer datos. Si hay iOS, todos los datos se almacenan en una subcarpeta de la carpeta Documents de la aplicación de iOS.

Ruta de ejecución típica de una aplicación de AEM Mobile basada en iOS:

* El usuario inicia la aplicación en el dispositivo iOS.
* AEM La aplicación intenta conectarse al back-end de la aplicación y solicita cambios de datos desde la última ejecución de la aplicación.
* El servidor recupera los datos en cuestión y los comprime en un archivo.
* Los datos se devuelven al dispositivo cliente, donde se extraen en la carpeta de documentos.
* Se inicia/actualiza el componente UIWebView.

Si no se ha podido establecer una conexión, se muestran los datos descargados anteriormente.

### Primeros pasos {#getting-ahead}

Para obtener más información sobre las funciones y responsabilidades de un administrador y un desarrollador, consulte los recursos siguientes:

* [Creación para Adobe PhoneGap AEM Enterprise con](/help/mobile/phonegap.md)
* [Administración de contenido para Adobe PhoneGap AEM Enterprise con el servicio de administración de](/help/mobile/administer-phonegap.md)
