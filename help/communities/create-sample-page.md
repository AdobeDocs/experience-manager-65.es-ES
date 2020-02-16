---
title: Crear una página de muestra
seo-title: Crear una página de muestra
description: Crear un sitio de comunidad de muestra
seo-description: Crear un sitio de comunidad de muestra
uuid: 04a8f027-b7d8-493a-a9bd-5c4a6715d754
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
discoiquuid: a03145f7-6697-4797-b73e-6f8d241ce469
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Crear una página de muestra {#create-a-sample-page}

A partir de AEM 6.1 Communities, la forma más sencilla de crear una página de muestra consiste en crear un sitio de comunidad sencillo, compuesto simplemente por una función Page.

Esto incluirá un componente parsys para que pueda [habilitar componentes para la creación](basics.md#accessing-communities-components).

Otra opción para explorar con componentes de muestra es utilizar las funciones presentadas en la Guía [de componentes de](components-guide.md)comunidad.

## Crear un sitio de comunidad {#create-a-community-site}

Esto es muy similar a crear un nuevo sitio descrito en [Introducción a las comunidades](getting-started.md)de AEM.

La diferencia principal es que este tutorial creará una nueva plantilla de sitio de comunidad que sólo contiene la función [](functions.md#page-function) Página para crear un sitio de comunidad simple sin otras características (aparte de las funciones precableadas básicas para todos los sitios de la comunidad).

### Crear nueva plantilla de sitio {#create-new-site-template}

Para empezar, cree una plantilla [de sitio de](sites.md)comunidad sencilla.

En la navegación global de una instancia de autor, seleccione **[!UICONTROL Herramientas > Comunidades > Plantillas]** de sitio.

![chlimage_1-82](assets/chlimage_1-82.png)

* Seleccione `Create button`
* INFORMACIÓN BÁSICA

   * `Name`:: Plantilla de página única
   * `Description`:: Una plantilla que consta de una sola función de página.
   * select `Enabled`

![chlimage_1-83](assets/chlimage_1-83.png)

* ESTRUCTURA

   * Arrastre una `Page` función al Generador de plantillas
   * Para Detalles de la función de configuración, introduzca

      * `Title`:: Página única
      * `URL`: page

![chlimage_1-84](assets/chlimage_1-84.png)

* Seleccionar **`Save`** para la configuración
* Seleccionar **`Save`** para la plantilla de sitio

### Crear nuevo sitio de comunidad {#create-new-community-site}

Ahora cree un nuevo sitio de comunidad basado en la plantilla de sitio simple.

Después de crear la plantilla de sitio, en la navegación global seleccione **[!UICONTROL Comunidades > Sitios]**.

![chlimage_1-85](assets/chlimage_1-85.png)

* Seleccionar **`Create`** icono

* Etapa `1 - Site Template`

   * `Title`:: Sitio de comunidad simple
   * `Description`:: Un sitio de comunidad que consiste en una sola página para la experimentación.
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`:: muestra

      * url = http://localhost:4502/content/sites/sample
   * `Template`:: elegir `Single Page Template`


![chlimage_1-86](assets/chlimage_1-86.png)

* Seleccione `Next`
* Etapa `2 - Design`

   * Seleccionar cualquier diseño

* Seleccione `Next`
* Seleccione `Next`

   (Acepte todos los ajustes predeterminados)

* Seleccione `Create`

![chlimage_1-87](assets/chlimage_1-87.png)

## Publicar el sitio {#publish-the-site}

![chlimage_1-88](assets/chlimage_1-88.png)

En la consola [Sitios de](sites-console.md)comunidad, seleccione el icono de publicación para publicar el sitio, de forma predeterminada en http://localhost:4503.

## Abrir el sitio al autor en modo de edición {#open-the-site-on-author-in-edit-mode}

![chlimage_1-89](assets/chlimage_1-89.png)

Seleccione el icono del sitio abierto para ver el sitio en modo de edición.

La dirección URL será [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![chlimage_1-90](assets/chlimage_1-90.png)

En la página de inicio simple es posible ver lo que está preconectado a través de las funciones y plantillas de la comunidad, y jugar con la adición y configuración de componentes de la comunidad.

## Ver sitio al publicar {#view-site-on-publish}

Después de publicar la página, abra la página en la instancia [de](http://localhost:4503/content/sites/sample/en.html) publicación para experimentar con las funciones como visitante anónimo del sitio, miembro con sesión iniciada o administrador. El vínculo Administración visible en el entorno de creación no aparecerá en el entorno de publicación a menos que un administrador inicie sesión.
