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

AEM Como en las comunidades de 6.1, la forma más sencilla de crear una página de muestra es crear un sitio de comunidad simple que consista simplemente en una función Página.

Esto incluirá un componente parsys para que pueda [habilitar componentes para la creación](basics.md#accessing-communities-components).

Otra opción para la exploración con componentes de muestra es utilizar las funciones presentadas en la variable [Guía de componentes de la comunidad](components-guide.md).

## Crear un sitio de la comunidad {#create-a-community-site}

Esto es muy similar a crear un nuevo sitio descrito en [Introducción a AEM Communities](getting-started.md).

La diferencia principal es que este tutorial creará una nueva plantilla del sitio de la comunidad que solo contenga la variable [Page, función](functions.md#page-function) para crear un sitio de la comunidad simple sin otras características (que no sean las características preconfiguradas básicas para todos los sitios de la comunidad).

### Crear nueva plantilla del sitio {#create-new-site-template}

Para empezar, cree un [plantilla del sitio de la comunidad](sites.md).

En la navegación global en una instancia de autor, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Communities]** > **[!UICONTROL Plantillas de sitio]**.

![create-site-template](assets/create-site-template1.png)

* Seleccionar `Create button`
* INFORMACIÓN BÁSICA

   * `Name`: Plantilla de una sola página
   * `Description`: una plantilla que consta de una sola función Página.
   * Seleccionar `Enabled`

![site-template-editor](assets/site-template-editor.png)

* ESTRUCTURA

   * Arrastre una `Page` al Generador de plantillas
   * Para Detalles de la función de configuración, introduzca

      * `Title`: Una página
      * `URL`: página

![site-template-editor-structure](assets/site-template-editor1.png)

* Seleccionar **`Save`** para la configuración
* Seleccionar **`Save`** para la plantilla del sitio

### Crear nuevo sitio de la comunidad {#create-new-community-site}

Ahora cree un nuevo sitio de comunidad basado en la plantilla de sitio simple.

Después de crear la plantilla del sitio, en navegación global, seleccione **[!UICONTROL Comunidades > Sitios]**.

![create-community-site](assets/create-community-site1.png)

* Seleccionar **`Create`** icono

* Paso `1 - Site Template`

   * `Title`: Sitio de comunidad simple
   * `Description`: un sitio de la comunidad que consta de una sola página para la experimentación.
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`: muestra

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

## Publicación del sitio {#publish-the-site}

![publish-site](assets/publish-site.png)

Desde el [consola sitios de la comunidad](sites-console.md), seleccione el icono de publicación para publicar el sitio, de forma predeterminada, en http://localhost:4503.

## Abrir el sitio en Autor en modo de edición {#open-the-site-on-author-in-edit-mode}

![de sitio abierto](assets/open-site.png)

Seleccione el icono de abrir sitio para ver el sitio en modo de edición.

La dirección URL será [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![Author-Site](assets/author-site.png)

En la página de inicio simple es posible ver lo que está precableado a través de las funciones y plantillas de la comunidad, y jugar con la adición y configuración de componentes de la comunidad.

## Ver sitio al publicar {#view-site-on-publish}

Después de publicar la página, ábrala en el [instancia de publicación](http://localhost:4503/content/sites/sample/en.html) para experimentar con las funciones como visitante anónimo del sitio, miembro conectado o administrador. El vínculo Administración visible en el entorno de creación no aparecerá en el entorno de publicación a menos que un administrador inicie sesión.
