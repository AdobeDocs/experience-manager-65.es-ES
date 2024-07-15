---
title: Crear una página de muestra
description: Aprenda a crear una plantilla de sitio de comunidad que solo contenga la función Página que puede ayudarle a crear un sitio de comunidad sencillo.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
exl-id: d66fc1ff-a669-4a2c-b45a-093060facd97
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Crear una página de muestra {#create-a-sample-page}

AEM Como en las comunidades de 6.1, la forma más sencilla de crear una página de muestra es crear un sitio de comunidad simple que consista simplemente en una función Página.

Esto incluye un componente parsys para que pueda [habilitar componentes para la creación](basics.md#accessing-communities-components).

Otra opción para la exploración con componentes de ejemplo es utilizar las características presentadas en la [Guía de componentes de la comunidad](components-guide.md).

## Crear un sitio de la comunidad {#create-a-community-site}

Esto es similar a crear un sitio descrito en [Introducción a AEM Communities](getting-started.md).

La diferencia principal es que este tutorial crea una plantilla de sitio de comunidad que solo contiene la [función Página](functions.md#page-function) para crear un sitio de comunidad simple. Esto se realiza sin necesidad de otras funciones (además de las funciones precableadas básicas para todos los sitios de la comunidad).

### Crear nueva plantilla del sitio {#create-new-site-template}

Para empezar, cree una [plantilla del sitio de la comunidad](sites.md) sencilla.

Desde la navegación global en una instancia de autor, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Plantillas de sitio]**.

![create-site-template](assets/create-site-template1.png)

* Seleccionar `Create button`
* INFORMACIÓN BÁSICA

   * `Name`: plantilla de una sola página
   * `Description`: una plantilla que consta de una sola función Página.
   * Seleccionar `Enabled`

![editor-plantilla-sitio](assets/site-template-editor.png)

* ESTRUCTURA

   * Arrastre una función `Page` al Generador de plantillas
   * Para Detalles de la función de configuración, introduzca

      * `Title`: una sola página
      * `URL`: página

![estructura-editor-de-plantillas-de-sitio](assets/site-template-editor1.png)

* Seleccione **`Save`** para la configuración
* Seleccione **`Save`** para la plantilla del sitio

### Crear nuevo sitio de la comunidad {#create-new-community-site}

Ahora cree un sitio de comunidad basado en la plantilla de sitio simple.

Después de crear la plantilla del sitio, en navegación global, seleccione **[!UICONTROL Comunidades > Sitios]**.

![create-community-site](assets/create-community-site1.png)

* Icono Seleccionar **`Create`**

* Paso `1 - Site Template`

   * `Title`: sitio de comunidad simple
   * `Description`: sitio de la comunidad que consta de una sola página para experimentación.
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`: ejemplo

      * url = http://localhost:4502/content/sites/sample

      * `Template`: elija `Single Page Template`

     ![create-community-site-template](assets/create-community-site-template.png)

* Seleccionar `Next`
* Paso `2 - Design`

   * Seleccione cualquier diseño

* Seleccionar `Next`
* Seleccionar `Next`

  (Aceptar todos los ajustes predeterminados)

* Seleccionar `Create`

  ![create-community-site](assets/create-community-site.png)

## Publish el sitio {#publish-the-site}

![sitio de publicación](assets/publish-site.png)

En la consola [sitios de la comunidad](sites-console.md), seleccione el icono Publicar para publicar el sitio, de forma predeterminada en http://localhost:4503.

## Abrir el sitio en Autor en modo de edición {#open-the-site-on-author-in-edit-mode}

![sitio abierto](assets/open-site.png)

Seleccione el icono de abrir sitio para poder ver el sitio en modo de edición.

La dirección URL es [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![sitio-autor](assets/author-site.png)

En la página de inicio simple, es posible ver lo que está preconfigurado a través de las funciones y plantillas de la comunidad, y jugar con la adición y configuración de componentes de la comunidad.

## Ver sitio en Publish {#view-site-on-publish}

Después de publicar la página, ábrala en la [instancia de publicación](http://localhost:4503/content/sites/sample/en.html) para experimentar con las características como visitante anónimo del sitio, miembro con sesión iniciada o administrador. El vínculo Administración visible en el entorno de creación no aparece en el entorno de publicación a menos que un administrador inicie sesión.
