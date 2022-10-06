---
title: El Exportador de páginas
description: Aprenda a utilizar el Exportador de páginas AEM.
exl-id: 15d08758-cf75-43c0-9818-98a579d64183
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---

# El Exportador de páginas{#the-page-exporter}

AEM permite exportar una página como una página web completa que incluye imágenes, `.js` y `.css` archivos.

Una vez configurada, solicite una exportación de página desde el explorador y reemplace `html` con `export.zip` en la dirección URL. Esto genera un archivo (zip) que contiene la página representada en formato html junto con los recursos a los que se hace referencia. Todas las rutas de la página (por ejemplo, las rutas a las imágenes) se reescriben para que apunten a los archivos incluidos en el archivo o a los recursos del servidor. El archivo (zip) se puede descargar desde el explorador.

>[!NOTE]
>
>Según el explorador y la configuración, la descarga será:
>* un archivo (`<page-name>.export.zip`)
>* una carpeta (`<page-name>`); efectivamente, el archivo de archivo ya se ha expandido


## Exportación de una página {#exporting-a-page}

Los siguientes pasos describen cómo exportar una página y suponen que existe una plantilla de exportación para el sitio. Una plantilla de exportación define la forma en que se exporta una página y es específica de su sitio. Para crear una plantilla de exportación, consulte [Creación de una configuración del exportador de páginas para su sitio](#creating-a-page-exporter-configuration-for-your-site) para obtener más información.

Para exportar una página:

1. Vaya a la página requerida en la **Sitios** consola.

1. Seleccione la página y, a continuación, abra la **Propiedades** diálogo.

1. Seleccione el **Avanzadas** pestaña .

1. Expanda el **Exportar** para seleccionar una plantilla de exportación.
Seleccione la plantilla necesaria para el sitio y, a continuación, confirme con **OK**.

1. Select **Guardar y cerrar** para cerrar el cuadro de diálogo de propiedades de la página.

1. Solicite la página para la exportación, reemplazando el sufijo `html` con `export.zip` en la dirección URL.

   Por ejemplo:
   * localhost:4502/content/we-retail/language-masters/en.html

   Se accede a través de:
   * localhost:4502/content/we-retail/language-masters/en.export.zip


1. Descargue el archivo de archivo en su sistema de archivos.

1. En su sistema de archivos, descomprima el archivo si es necesario. Una vez expandida, habrá una carpeta con el mismo nombre que la página seleccionada. Esta carpeta contiene:

   * la subcarpeta `content`, que es la raíz de una serie de subcarpetas que reflejan la ruta a la página en el repositorio

      * dentro de esta estructura hay el archivo html para la página seleccionada (`<page-name>.html`)
   * otros recursos (`.js` archivos, `.css` archivos, imágenes, etc.) se encuentran según la configuración de la plantilla de exportación


1. Abra el archivo html de la página (`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`) en el navegador para comprobar la renderización.

## Creación de una configuración del exportador de páginas para su sitio {#creating-a-page-exporter-configuration-for-your-site}

El exportador de páginas se basa en la variable [Marco de sincronización de contenido](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html). Las configuraciones disponibles en la variable **Propiedades de página** son plantillas de exportación que definen las dependencias necesarias para una página.

Cuando se activa una exportación de página, se hace referencia a la plantilla de exportación y tanto la ruta de página como la ruta de diseño se aplican de forma dinámica. A continuación, el archivo zip se crea mediante la funcionalidad estándar de sincronización de contenido.

Una instalación de AEM predeterminada incluye una plantilla predeterminada en `/etc/contentsync/templates/default`.

* Esta plantilla es la plantilla de reserva cuando no se encuentra ninguna plantilla de exportación en el repositorio.

* La variable `default` plantilla muestra cómo se puede configurar una exportación de página, de modo que sirva de base para una nueva plantilla de exportación.

* Para ver la estructura de nodos de la plantilla en el explorador como formato JSON, solicite la siguiente URL:
   `http://localhost:4502/etc/contentsync/templates/default.json`

El método más sencillo para crear una nueva plantilla de exportador de página es:

* copie el `default` plantilla,

* asignar un nombre nuevo, adecuado para el sitio,

* a continuación, realice las actualizaciones necesarias.

Para crear una plantilla completamente nueva:

1. En **CRXDE Lite**, cree un nodo a continuación `/etc/contentsync/templates`:

   * `Name`: un nombre apropiado para el sitio; por ejemplo, `<mysite>`. El nombre aparece en el cuadro de diálogo de propiedades de la página al elegir la plantilla de exportador de páginas.

   * `Type`: `nt:unstructured`

2. Debajo del nodo de plantilla, llamado aquí `mysite`, cree una estructura de nodos utilizando los nodos de configuración que se describen a continuación.

## Activación de una plantilla de exportador de página para las páginas {#activating-a-page-exporter-configuration-for-your-pages}

Una vez configurada la plantilla, debe estar disponible:

1. En CRXDE, vaya a la página requerida en la `/content` rama. Puede ser una página individual o la página raíz de un subárbol.

1. En el `jcr:content` en la página cree la propiedad :
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`: ruta a la plantilla; por ejemplo: `/etc/contentsync/templates/mysite`

### Nodos de configuración del Exportador de páginas {#page-exporter-configuration-nodes}

La plantilla está formada por una estructura de nodos, ya que utiliza la variable [Marco de sincronización de contenido](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html).  Cada nodo tiene un `type` que define una acción específica en el proceso de creación del archivo zip.

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

Los siguientes nodos se pueden utilizar para crear una plantilla de exportación:

* `page`
El nodo de página se utiliza para copiar el html de la página en el archivo zip. Tiene las siguientes características:

   * Es un nodo obligatorio.
   * Se encuentra a continuación `/etc/contentsync/templates/<mysite>`.
   * Se define con la propiedad `Name`configure como `page`.
   * El tipo de nodo es `nt:unstructured`

   La variable `page` tiene las siguientes propiedades:

   * A `type` propiedad establecida con el valor `pages`.

   * No tiene un `path` como la ruta de página actual se copia dinámicamente en la configuración.

   <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
El nodo de reescritura define cómo se reescriben los vínculos en la página exportada. Los vínculos reescritos pueden apuntar a los archivos incluidos en el archivo zip o a los recursos del servidor.
   <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
El nodo de diseño se utiliza para copiar el diseño utilizado para la página exportada. Tiene las siguientes características:

   * Es opcional.
   * Se encuentra a continuación `/etc/contentsync/templates/<mysite>`.
   * Se define con la propiedad `Name` configure como `design`.
   * El tipo de nodo es `nt:unstructured`.

   La variable `design` tiene las siguientes propiedades:

   * A `type` propiedad establecida en el valor `copy`.

   * No tiene un `path` , ya que la ruta de página actual se copia dinámicamente en la configuración.


* `generic`
Se utiliza un nodo genérico para copiar recursos como clientlibs 
`.js` o `.css` archivos al archivo zip. Tiene las siguientes características:

   * Es opcional.
   * Se encuentra a continuación `/etc/contentsync/templates/<mysite>`.
   * No tiene un nombre específico.
   * El tipo de nodo es `nt:unstructured`.
   * Tiene un `type` propiedad y `type` propiedades relacionadas. <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

   Por ejemplo, el siguiente nodo de configuración copia la variable `mysite.clientlibs.js` archivos al archivo zip:

   ```xml
   "mysite.clientlibs.js": {
       "extension": "js",
       "type": "clientlib",
       "path": "/etc/designs/mysite/clientlibs",
       "jcr:primaryType": "nt:unstructured"
   }
   ```

**Implementación de una configuración personalizada**

También es posible realizar configuraciones personalizadas.

<!--
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

Para satisfacer algunos requisitos específicos, es posible que necesite implementar un [controlador de actualización personalizado](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html).

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## Exportación mediante programación de una página {#programmatically-exporting-a-page}

Para exportar una página mediante programación, puede usar la variable [PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) Servicio OSGI. Este servicio le permite:

* Exporte una página y escriba la respuesta del servlet HTTP.
* Exporte una página y guarde el archivo zip en una ubicación específica.

El servlet que está enlazado al `export` y `zip` utiliza el servicio PageExporter.

## Solución de problemas {#troubleshooting}

Si tiene algún problema con la descarga del archivo zip, puede eliminar la variable `/var/contentsync` en el repositorio y vuelva a enviar la solicitud de exportación.
