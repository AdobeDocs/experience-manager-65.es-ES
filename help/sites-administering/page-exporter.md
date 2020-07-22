---
title: Exportador de páginas
description: Aprenda a utilizar AEM Page Exporter.
translation-type: tm+mt
source-git-commit: b0126894dec33648a24c0308972aa5b47d7e4b84
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 0%

---


# Exportador de páginas{#the-page-exporter}

AEM le permite exportar una página como una página web completa que incluye imágenes `.js` y `.css` archivos.

Una vez configurada, puede solicitar una exportación de página desde el explorador reemplazando `html` por `export.zip` en la dirección URL. Esto genera un archivo (zip) que contiene la página representada en formato html, junto con los recursos a los que se hace referencia. Todas las rutas de la página (por ejemplo, las rutas a las imágenes) se reescriben para que apunten a los archivos incluidos en el archivo o a los recursos del servidor. El archivo (zip) se puede descargar del explorador.

>!![NOTE]
Según el explorador y la configuración, la descarga será:
* un archivo de archivo (`<page-name>.export.zip`)
* una carpeta (`<page-name>`); el archivo de archiving ya se ha ampliado


## Exportación de una página {#exporting-a-page}

Los siguientes pasos describen cómo exportar una página y suponen que existe una plantilla de exportación para el sitio. Una plantilla de exportación define la forma en que se exporta una página y es específica para su sitio. Para crear una plantilla de exportación, consulte la sección [Creación de una configuración del exportador de páginas para su sitio](#creating-a-page-exporter-configuration-for-your-site) .

Para exportar una página:

1. Vaya a la página requerida en la consola **Sitios** .

1. Seleccione la página y, a continuación, abra el cuadro de diálogo **Propiedades** .

1. Select the **Advanced** tab.

1. Expanda el campo **Exportar** para seleccionar una plantilla de exportación.
Seleccione la plantilla requerida para el sitio y confirme con **Aceptar**.

1. Seleccione **Guardar y cerrar** para cerrar el cuadro de diálogo de propiedades de página.

1. Solicite la exportación de la página, reemplazando el sufijo `html` por `export.zip` en la dirección URL.

   Por ejemplo:
   * localhost:4502/content/we-retail/language-masters/en.html

   Se accede a él a través de:
   * localhost:4502/content/we-retail/language-masters/en.export.zip


1. Descargue el archivo de archivo en el sistema de archivos.

1. En el sistema de archivos, descomprima el archivo si es necesario. Una vez expandida, habrá una carpeta con el mismo nombre que la página seleccionada. Esta carpeta contiene:

   * la subcarpeta `content`, que es la raíz de una serie de subcarpetas que reflejan la ruta a la página en el repositorio

      * dentro de esta estructura hay el archivo html para la página seleccionada (`<page-name>.html`)
   * otros recursos (`.js` archivos, `.css` archivos, imágenes, etc.) se ubican según la configuración de la plantilla de exportación


1. Abra el archivo html de página (`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`) en el navegador para comprobar el procesamiento.

## Creación de una configuración del exportador de páginas para el sitio {#creating-a-page-exporter-configuration-for-your-site}

El exportador de páginas se basa en el marco de sincronización de [contenido](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html). Las configuraciones disponibles en el cuadro de diálogo Propiedades **de la** página son plantillas de exportación que definen las dependencias necesarias para una página.

Cuando se activa una exportación de página, se hace referencia a la plantilla de exportación y tanto la ruta de página como la ruta de diseño se aplican de forma dinámica. A continuación, el archivo zip se crea mediante la funcionalidad estándar de sincronización de contenido.

Una instalación AEM lista para usar incluye una plantilla predeterminada en `/etc/contentsync/templates/default`.

* Esta plantilla es la plantilla de reserva cuando no se encuentra ninguna plantilla de exportación en el repositorio.

* La `default` plantilla muestra cómo se puede configurar una exportación de página, de modo que puede servir de base para una nueva plantilla de exportación.

* Para vista de la estructura de nodos de la plantilla en el navegador como formato JSON, solicite la siguiente URL:
   `http://localhost:4502/etc/contentsync/templates/default.json`

El método más sencillo para crear una nueva plantilla de exportador de páginas es:

* copiar la `default` plantilla,

* asignar un nuevo nombre, adecuado para el sitio,

* a continuación, realice las actualizaciones necesarias.

Para crear una plantilla completamente nueva:

1. En **CRXDE Lite**, cree un nodo a continuación `/etc/contentsync/templates`:

   * `Name`:: un nombre apropiado para el sitio; por ejemplo, `<mysite>`. El nombre aparece en el cuadro de diálogo de propiedades de página al elegir la plantilla del exportador de páginas.

   * `Type`: `nt:unstructured`

2. Debajo del nodo de plantilla, llamado aquí `mysite`, cree una estructura de nodos utilizando los nodos de configuración que se describen a continuación.

## Activación de una plantilla de exportador de páginas para las páginas {#activating-a-page-exporter-configuration-for-your-pages}

Una vez configurada la plantilla, debe ponerla a disposición:

1. En CRXDE, navegue a la página requerida en la `/content` rama.

1. En el `jcr:content` nodo de la página, cree la propiedad:
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`:: ruta a la plantilla; por ejemplo: `/etc/contentsync/templates/mysite`

### Nodos de configuración del exportador de páginas {#page-exporter-configuration-nodes}

La plantilla consta de una estructura de nodos, ya que utiliza el marco de sincronización de [contenido](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html).  Cada nodo tiene una `type` propiedad que define una acción específica en el proceso de creación del archivo zip.

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

Se pueden utilizar los nodos siguientes para crear una plantilla de exportación:

* `page`
El nodo de página se utiliza para copiar el HTML de la página en el archivo zip. Tiene las características siguientes:

   * Es un nodo obligatorio.
   * Se encuentra debajo `/etc/contentsync/templates/<mysite>`.
   * Se define con la propiedad `Name`definida como `page`.
   * El tipo de nodo es `nt:unstructured`

   El `page` nodo tiene las siguientes propiedades:

   * Una `type` propiedad establecida con el valor `pages`.

   * No tiene una `path` propiedad ya que la ruta de la página actual se copia dinámicamente en la configuración.

   <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
El nodo reescribir define cómo se reescriben los vínculos en la página exportada. Los vínculos reescritos pueden apuntar a los archivos incluidos en el archivo zip o a los recursos del servidor.
   <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
El nodo de diseño se utiliza para copiar el diseño utilizado para la página exportada. Tiene las características siguientes:

   * Es opcional.
   * Se encuentra debajo `/etc/contentsync/templates/<mysite>`.
   * Se define con la propiedad `Name` definida como `design`.
   * El tipo de nodo es `nt:unstructured`.

   El `design` nodo tiene las siguientes propiedades:

   * Una `type` propiedad establecida en el valor `copy`.

   * No tiene una `path` propiedad, ya que la ruta de la página actual se copia dinámicamente en la configuración.


* `generic`
Se utiliza un nodo genérico para copiar recursos como clientlibs 
`.js` o `.css` archivos en el archivo zip. Tiene las características siguientes:

   * Es opcional.
   * Se encuentra debajo `/etc/contentsync/templates/<mysite>`.
   * No tiene un nombre específico.
   * El tipo de nodo es `nt:unstructured`.
   * Tiene una `type` propiedad y propiedades `type` relacionadas. <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

   Por ejemplo, el siguiente nodo de configuración copia los `mysite.clientlibs.js` archivos en el archivo zip:

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

Para cumplir algunos requisitos específicos, es posible que tenga que implementar un controlador de actualización [personalizado](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html).

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## Exportación de una página mediante programación {#programmatically-exporting-a-page}

Para exportar una página mediante programación, puede utilizar el servicio [PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI. Este servicio le permite:

* Exporte una página y escriba en la respuesta del servlet HTTP.
* Exporte una página y guarde el archivo zip en una ubicación específica.

El servlet que está enlazado al `export` selector y la `zip` extensión utiliza el servicio PageExporter.

## Solución de problemas {#troubleshooting}

Si experimenta un problema con la descarga del archivo zip, puede eliminar el `/var/contentsync` nodo en el repositorio y volver a enviar la solicitud de exportación.
