---
title: El exportador de página
description: Aprenda a utilizar el Exportador de páginas de Adobe Experience Manager AEM ().
exl-id: 15d08758-cf75-43c0-9818-98a579d64183
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# El exportador de página{#the-page-exporter}

Adobe Experience Manager AEM () permite exportar una página como una página web completa que incluye imágenes, `.js`, y `.css` archivos.

Cuando se configura, solicita una exportación de página desde el explorador reemplazando `html` con `export.zip` en la dirección URL. Esto genera un archivo (zip) que contiene la página procesada en formato html, junto con los recursos a los que se hace referencia. Todas las rutas de la página (por ejemplo, las rutas a imágenes) se vuelven a escribir para que apunten a los archivos incluidos en el archivo o a los recursos del servidor. A continuación, se puede descargar el archivo (zip) desde el explorador.

>[!NOTE]
>
>Según el explorador y la configuración, la descarga puede ser:
>
>* un archivo (`<page-name>.export.zip`)
>* una carpeta (`<page-name>`); efectivamente el archivo ya está expandido

## Exportar una página {#exporting-a-page}

Los siguientes pasos describen cómo exportar una página y suponen que existe una plantilla de exportación para el sitio. Una plantilla de exportación define la forma en que se exporta una página y es específica del sitio. Para crear una plantilla de exportación, consulte [Creación de una configuración de exportador de página para el sitio](#creating-a-page-exporter-configuration-for-your-site).

Para exportar una página:

1. Navegue hasta la página requerida en la **Sites** consola.

1. Seleccione la página y abra la **Propiedades** diálogo.

1. Seleccione el **Avanzadas** pestaña.

1. Expanda el **Exportar** para seleccionar una plantilla de exportación.
Seleccione la plantilla necesaria para el sitio y confirme con **OK**.

1. Seleccionar **Guardar y cerrar** para cerrar el cuadro de diálogo propiedades de página.

1. Solicite la exportación de la página, reemplazando el sufijo `html` con `export.zip` en la dirección URL.

   Por ejemplo:
   * localhost:4502/content/we-retail/language-masters/en.html

   Se accede a él mediante:
   * localhost:4502/content/we-retail/language-masters/en.export.zip

1. Descargue el archivo en su sistema de archivos.

1. En el sistema de archivos, descomprima el archivo si es necesario. Cuando se expande, hay una carpeta con el mismo nombre que la página seleccionada. Esta carpeta contiene:

   * la subcarpeta `content`, que es la raíz de una serie de subcarpetas que reflejan la ruta a la página en el repositorio

      * dentro de esta estructura está el archivo html de la página seleccionada (`<page-name>.html`)

   * otros recursos (`.js` archivos, `.css` archivos, imágenes, etc.) se encuentran según la configuración de la plantilla de exportación

1. Abra el archivo html de la página (`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`) en el navegador para poder comprobar la renderización.

## Creación de una configuración de exportador de página para el sitio {#creating-a-page-exporter-configuration-for-your-site}

El exportador de páginas se basa en [Marco de sincronización de contenido](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html). Las configuraciones disponibles en la variable **Propiedades de página** son plantillas de exportación que definen las dependencias necesarias para una página.

Cuando se activa una exportación de página, se hace referencia a la plantilla de exportación. Tanto la ruta de página como la ruta de diseño se aplican de forma dinámica. A continuación, el archivo zip se crea mediante la funcionalidad estándar de sincronización de contenido.

AEM Una instalación predeterminada de incluye una plantilla predeterminada en, que incluye lo siguiente: `/etc/contentsync/templates/default`.

* Esta plantilla es la plantilla de reserva cuando no se encuentra ninguna plantilla de exportación en el repositorio.

* El `default` La plantilla muestra cómo se puede configurar una exportación de página, de modo que puede servir de base para una nueva plantilla de exportación.

* Para ver la estructura de nodos de la plantilla en el explorador como formato JSON, solicite la siguiente URL:
  `http://localhost:4502/etc/contentsync/templates/default.json`

El método más sencillo para crear una plantilla de exportador de páginas es:

* copie el `default` plantilla,

* asignar un nombre nuevo, apropiado para su sitio,

* a continuación, realice las actualizaciones necesarias.

Para crear una plantilla completamente nueva:

1. Entrada **CRXDE Lite**, cree un nodo debajo de `/etc/contentsync/templates`:

   * `Name`: un nombre apropiado para el sitio; por ejemplo, `<mysite>`. El nombre aparece en el cuadro de diálogo de propiedades de página al elegir la plantilla del exportador de página.

   * `Type`: `nt:unstructured`

2. Bajo el nodo de plantilla, llamado aquí `mysite`, cree una estructura de nodos utilizando los nodos de configuración descritos a continuación.

## Activación de una plantilla del exportador de páginas para las páginas {#activating-a-page-exporter-configuration-for-your-pages}

Cuando la plantilla esté configurada, haga que esté disponible:

1. En CRXDE, vaya a la página requerida en la `/content` Rama. Puede ser una página individual o la página raíz de un subárbol.

1. En el `jcr:content` de la página, cree la propiedad:
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`: ruta a la plantilla; por ejemplo: `/etc/contentsync/templates/mysite`

### Nodos de configuración del exportador de página {#page-exporter-configuration-nodes}

La plantilla consta de una estructura de nodos, ya que utiliza la variable [Marco de sincronización de contenido](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html). Cada nodo tiene un `type` que define una acción específica en el proceso de creación del archivo zip.

<!-- For more details about the type property, see the Overview of configuration types section in the Content Sync framework page.
-->

Se pueden utilizar los siguientes nodos para crear una plantilla de exportación:

* `page`
El nodo de página se utiliza para copiar el HTML de página en el archivo zip. Tiene las siguientes características:

   * Un nodo obligatorio.
   * Situado debajo `/etc/contentsync/templates/<mysite>`.
   * Definido con la propiedad `Name`establezca en `page`.
   * El tipo de nodo es `nt:unstructured`

  El `page` tiene las siguientes propiedades:

   * A `type` propiedad establecida con el valor `pages`.

   * No tiene un. `path` como la ruta de la página actual se copia dinámicamente en la configuración.
  <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
El nodo de reescritura define cómo se reescriben los vínculos en la página exportada. Los vínculos reescritos pueden apuntar a los archivos incluidos en el archivo zip o a los recursos del servidor.
  <!-- See the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
El nodo de diseño se utiliza para copiar el diseño utilizado para la página exportada. Tiene las siguientes características:

   * Opcional.
   * Situado debajo `/etc/contentsync/templates/<mysite>`.
   * Definido con la propiedad `Name` establezca en `design`.
   * El tipo de nodo es `nt:unstructured`.

  El `design` tiene las siguientes propiedades:

   * A `type` propiedad establecida en el valor `copy`.

   * No tiene un. `path` , ya que la ruta de la página actual se copia dinámicamente en la configuración.

* `generic`
Se utiliza un nodo genérico para copiar recursos como clientlibs `.js` o `.css` al archivo zip. Tiene las siguientes características:

   * Opcional.
   * Situado debajo `/etc/contentsync/templates/<mysite>`.
   * No hay un nombre específico.
   * El tipo de nodo es `nt:unstructured`.
   * Tiene un `type` propiedad y `type` propiedades relacionadas. <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

  Por ejemplo, el siguiente nodo de configuración copia el `mysite.clientlibs.js` archivos en el archivo zip:

  ```xml
  "mysite.clientlibs.js": {
      "extension": "js",
      "type": "clientlib",
      "path": "/etc/designs/mysite/clientlibs",
      "jcr:primaryType": "nt:unstructured"
  }
  ```

**Implementación de una configuración personalizada**

También son posibles las configuraciones personalizadas.

<!--
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

Para cumplir algunos requisitos específicos, implemente una [controlador de actualización personalizado](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/handler/package-summary.html).

<!-- To meet some specific requirements, you may need to implement a custom `type` property. To do so, see the Implementing a custom update handler section in the Content Sync page.
-->

## Exportación de una página mediante programación {#programmatically-exporting-a-page}

Para exportar una página mediante programación, puede utilizar el complemento [PageExporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) Servicio OSGI. Este servicio le permite:

* Exporte una página y escriba en la respuesta del servlet HTTP.
* Exporte una página y guarde el archivo zip en una ubicación específica.

El servlet enlazado a la variable `export` y el `zip` utiliza el servicio PageExporter.

## Solución de problemas {#troubleshooting}

Si tiene algún problema con la descarga del archivo zip, puede eliminar el `/var/contentsync` en el repositorio y vuelva a enviar la solicitud de exportación.
