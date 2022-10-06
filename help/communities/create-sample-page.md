---
title: Crear una página de muestra
seo-title: Create a Sample Page
description: Crear un sitio de comunidad de muestra
seo-description: Create a Sample community site
uuid: 04a8f027-b7d8-493a-a9bd-5c4a6715d754
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
discoiquuid: a03145f7-6697-4797-b73e-6f8d241ce469
exl-id: d66fc1ff-a669-4a2c-b45a-093060facd97
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 2%

---

# Crear una página de muestra {#create-a-sample-page}

A partir de AEM comunidades 6.1, la forma más sencilla de crear una página de muestra es crear un sitio de comunidad simple que consista simplemente en una función Página .

Esto incluirá un componente parsys para que pueda [activación de componentes para la creación](basics.md#accessing-communities-components).

Otra opción para explorar con componentes de muestra es utilizar las funciones presentadas en la [Guía de componentes de comunidad](components-guide.md).

## Crear un sitio de comunidad {#create-a-community-site}

Esto es muy similar a la creación de un nuevo sitio descrito en [Introducción a AEM Communities](getting-started.md).

La diferencia principal es que este tutorial creará una nueva plantilla de sitio de la comunidad que solo contiene la variable [Función de página](functions.md#page-function) para crear un sitio de comunidad simple libre de otras características (aparte de las características precableadas básicas de todos los sitios de la comunidad).

### Crear nueva plantilla de sitio {#create-new-site-template}

Para empezar, cree un [plantilla del sitio de la comunidad](sites.md).

En la navegación global en una instancia de autor, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Plantillas de sitio]**.

![create-site-template](assets/create-site-template1.png)

* Seleccione `Create button`
* INFORMACIÓN BÁSICA

   * `Name`: Plantilla de una sola página
   * `Description`: Una plantilla que consiste en una función Page única.
   * Seleccione `Enabled`

![site-template-editor](assets/site-template-editor.png)

* ESTRUCTURA

   * Arrastre un `Page` al Generador de plantillas
   * Para Detalles de función de configuración, introduzca

      * `Title`: Página única
      * `URL`: page

![site-template-editor-structure](assets/site-template-editor1.png)

* Select **`Save`** para la configuración
* Select **`Save`** para la plantilla de sitio

### Crear nuevo sitio de comunidad {#create-new-community-site}

Ahora cree un nuevo sitio de comunidad basado en la plantilla de sitio simple.

Después de crear la plantilla del sitio, en la navegación global, seleccione **[!UICONTROL Comunidades > Sitios]**.

![create-community-site](assets/create-community-site1.png)

* Select **`Create`** icono

* Paso `1 - Site Template`

   * `Title`: Sitio de comunidad simple
   * `Description`: Un sitio de la comunidad que consiste en una sola página para la experimentación.
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`: ejemplo

      * url = http://localhost:4502/content/sites/sample

      * `Template`: elija `Single Page Template`

      ![create-community-site-template](assets/create-community-site-template.png)


* Seleccione `Next`
* Paso `2 - Design`

   * Seleccionar cualquier diseño

* Seleccione `Next`
* Seleccione `Next`

   (Acepte todos los ajustes predeterminados)

* Seleccione `Create`

   ![create-community-site](assets/create-community-site.png)

## Publicar el sitio {#publish-the-site}

![publish-site](assets/publish-site.png)

En el [consola sitios de comunidad](sites-console.md), seleccione el icono de publicación para publicar el sitio, de forma predeterminada a http://localhost:4503.

## Abra el sitio en modo de autor en el modo de edición . {#open-the-site-on-author-in-edit-mode}

![open-site](assets/open-site.png)

Seleccione el icono para abrir el sitio en modo de edición.

La dirección URL será [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![author-site](assets/author-site.png)

En la página de inicio simple es posible ver qué está preconectado a través de las funciones y plantillas de la comunidad, y jugar con la adición y configuración de componentes de la comunidad.

## Ver sitio en publicación {#view-site-on-publish}

Después de publicar la página, ábrala en el [instancia de publicación](http://localhost:4503/content/sites/sample/en.html) para experimentar con las funciones como visitante anónimo del sitio, miembro registrado o administrador. El vínculo Administration visible en el entorno de creación no aparecerá en el entorno de publicación a menos que un administrador inicie sesión.
