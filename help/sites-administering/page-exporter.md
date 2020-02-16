---
title: Exportador de páginas
seo-title: Exportador de páginas
description: Aprenda a utilizar AEM Page Exporter.
seo-description: Aprenda a utilizar AEM Page Exporter.
uuid: 2ca2b8f1-c723-4e6b-8c3d-f5886cd0d3f1
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6ab07b5b-ee37-4029-95da-be2031779107
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Exportador de páginas{#the-page-exporter}

AEM le permite exportar una página como una página web completa que incluye imágenes, archivos .js y archivos .css.

Una vez configurada la exportación, solo tiene que solicitar una página en el navegador sustituyéndola `html` por `export.zip` en la URL y obtener una descarga de archivo zip que contenga la página representada en formato html y los recursos a los que se hace referencia. Todas las rutas de la página, por ejemplo las rutas a las imágenes, se reescriben para que apunten a los archivos incluidos en el archivo zip o a los recursos del servidor.

## Exportación de una página {#exporting-a-page}

Los siguientes pasos describen cómo exportar una página y suponen que existe una plantilla de configuración de exportación para el sitio. Una plantilla de configuración define la forma en que se exporta una página y es específica para su sitio. Para crear una plantilla de configuración, consulte la sección [Creación de una configuración del exportador de páginas para su sitio](#creating-a-page-exporter-configuration-for-your-site) .

Para exportar una página:

1. En el explorador, abra la página. Por ejemplo:
1. `http://localhost:4502/content/geometrixx/en/products/triangle.html`
1. Abra el cuadro de diálogo de propiedades de página, seleccione la ficha **Avanzadas** y expanda el conjunto de campos **Exportar** .

1. Haga clic en el icono de lupa y seleccione una plantilla de configuración. Seleccione la plantilla **geometrixx** , ya que es la predeterminada para el sitio Geometrixx. Haga clic en **Aceptar**.

1. Haga clic en **Aceptar** para cerrar el cuadro de diálogo de propiedades de página.
1. Solicite la página reemplazando `html` por `export.zip` en la dirección URL.

1. Descargue el `<page-name>.export.zip` archivo en su sistema de archivos.

1. En el sistema de archivos, descomprima el archivo:

   * el archivo html de la página ( `<page-name>.html`) está disponible a continuación `<unzip-dir>/<page-path>`
   * otros recursos (archivos .js, archivos .css, imágenes, etc.) se encuentran según la configuración de la plantilla de exportación. En este ejemplo, algunos recursos se encuentran debajo `<unzip-dir>/etc`, algunos a continuación `<unzip-dir>/<page-path>`.

1. Abra el archivo html de página ( `<unzip-dir>/<page-path>.html`) en el navegador para comprobar el procesamiento.

## Creación de una configuración del exportador de páginas para el sitio {#creating-a-page-exporter-configuration-for-your-site}

El exportador de páginas se basa en el marco de sincronización de contenido. Las configuraciones disponibles en el cuadro de diálogo de propiedades de página son plantillas de configuración. Definen todas las dependencias necesarias para una página. Cuando se activa una exportación de página, se utiliza la plantilla de configuración y tanto la ruta de página como la ruta de diseño se aplican de forma dinámica a la configuración. A continuación, el archivo zip se crea mediante la funcionalidad estándar de sincronización de contenido.

AEM incrusta algunas plantillas, entre las que se incluyen:

* Una predeterminada en `/etc/contentsync/templates/default`. Esta plantilla:

   * Es la plantilla de reserva cuando no se encuentra ninguna plantilla de configuración en el repositorio.
   * Puede servir de base para una nueva plantilla de configuración.

* Una que está dedicada al sitio **Geometrixx** , en `/etc/contentsync/templates/geometrixx`. Esta plantilla puede utilizarse como ejemplo para crear una nueva.

Para crear una plantilla de configuración de exportador de páginas:

1. En **CRXDE Lite**, cree un nodo a continuación `/etc/contentsync/templates`:

   * Nombre:p. ej. `mysite`. El nombre aparece en el cuadro de diálogo de propiedades de página al elegir la plantilla del exportador de páginas.
   * Tipo: `nt:unstructured`

1. Debajo del nodo de plantilla, llamado aquí `mysite`, cree una estructura de nodos utilizando los nodos de configuración que se describen a continuación.

### Nodos de configuración del exportador de páginas {#page-exporter-configuration-nodes}

La plantilla de configuración consta de una estructura de nodos. Cada nodo tiene una `type` propiedad que define una acción específica en el proceso de creación del archivo zip. Para obtener más información sobre la propiedad type, consulte la sección Información general sobre los tipos de configuración en la página del marco de sincronización de contenido.

Se pueden utilizar los nodos siguientes para crear una plantilla de configuración de exportación:

**nodo** de página El nodo de página se utiliza para copiar el HTML de la página en el archivo zip. Tiene las características siguientes:

* Es un nodo obligatorio.
* Se encuentra debajo `/etc/contentsync/templates/<sitename>`.
* Su nombre es `page`.
* Su tipo de nodo es `nt:unstructured`

El `page` nodo tiene las siguientes propiedades:

* Una `type` propiedad establecida con el valor `pages`.

* No tiene una `path` propiedad ya que la ruta de la página actual se copia dinámicamente en la configuración.

* Las demás propiedades se describen en la sección Información general sobre los tipos de configuración del marco de sincronización de contenido.

**nodo** de reescritura El nodo de reescritura define cómo se reescriben los vínculos en la página exportada. Los vínculos reescritos pueden apuntar a los archivos incluidos en el archivo zip o a los recursos del servidor.

Consulte la página Sincronización de contenido para obtener una descripción completa del `rewrite` nodo.

**nodo** de diseño El nodo de diseño se utiliza para copiar el diseño utilizado para la página exportada. Tiene las características siguientes:

* Es opcional.
* Se encuentra debajo `/etc/contentsync/templates/<sitename>`.
* Su nombre es `design`.
* Su tipo de nodo es `nt:unstructured`.

El `design` nodo tiene las siguientes propiedades:

* Una `type` propiedad establecida en el valor `copy`.

* No tiene una `path` propiedad ya que la ruta de la página actual se copia dinámicamente en la configuración.

**nodo** genérico Se utiliza un nodo genérico para copiar recursos como archivos clientlibs.js o .css en el archivo zip. Tiene las características siguientes:

* Es opcional.
* Se encuentra debajo `/etc/contentsync/templates/<sitename>`.
* No tiene un nombre específico.
* Su tipo de nodo es `nt:unstructured`.
* Tiene una `type` propiedad y cualquier propiedad `type` relacionada, tal como se define en la sección Información general de los tipos de configuración del marco de sincronización de contenido.

Por ejemplo, el siguiente nodo de configuración copia los archivos geometrixx clientlibs.js en el archivo zip:

```xml
"geometrixx.clientlibs.js": {
    "extension": "js",
    "type": "clientlib",
    "path": "/etc/designs/geometrixx/clientlibs",
    "jcr:primaryType": "nt:unstructured"
}
```

La plantilla de configuración de exportación de página **Geometrixx** muestra cómo se puede configurar una exportación de página. Para ver la estructura de nodos de la plantilla en el navegador como formato json, solicite la siguiente URL:

`http://localhost:4502/etc/contentsync/templates/geometrixx.-1.json`

**Implementación de una configuración personalizada**

Como puede haber notado en la estructura de nodos, la plantilla de configuración de exportación de página de **Geometrixx** tiene un `logo` nodo con una `type` propiedad establecida en `image`. Se trata de un tipo de configuración especial que se ha creado para copiar el logotipo de la imagen en el archivo zip. Para cumplir algunos requisitos específicos, es posible que tenga que implementar una `type` propiedad personalizada: para ello, consulte la sección Implementación de un controlador de actualización personalizado en la página Sincronización de contenido.

## Exportación de una página mediante programación {#programmatically-exporting-a-page}

Para exportar una página mediante programación, puede utilizar el servicio [PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI. Este servicio le permite:

* Exporte una página y escriba en la respuesta del servlet HTTP.
* Exporte una página y guarde el archivo zip en una ubicación específica.

El servlet que está enlazado al `export` selector y la `zip` extensión utiliza el servicio PageExporter.

## Solución de problemas {#troubleshooting}

Si experimenta un problema con la descarga del archivo zip, puede eliminar el `/var/contentsync` nodo en el repositorio y volver a enviar la solicitud de exportación.

