---
title: Creación De Un Simulador Para Pruebas SCF
seo-title: Create An SCF Sandbox
description: Este tutorial es principalmente para desarrolladores, nuevos AEM, interesados en utilizar componentes SCF.  Recorre la creación de un sitio de espacio aislado de SCF
seo-description: This tutorial is primarily for developers, new to AEM, who are interested in using SCF components.  It walks through the creation of An SCF Sandbox site
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
exl-id: 89858814-6625-4a56-8359-cc1eca402816
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---

# Creación De Un Simulador Para Pruebas SCF  {#create-an-scf-sandbox}


A partir de AEM 6.1 Comunidades, la forma más sencilla de crear rápidamente un simulador de pruebas es crear un sitio de comunidad. Consulte [Introducción a AEM Communities](getting-started.md).

Otra herramienta útil para los desarrolladores es la [Guía de componentes de comunidad](components-guide.md), que permite la exploración y la creación rápida de prototipos de componentes y funciones de Communities.

El ejercicio de crear un sitio web puede ser útil para comprender la estructura de un sitio web AEM que puede incluir características de las comunidades, al mismo tiempo que proporciona páginas sencillas en las que explorar la posibilidad de trabajar con el [marco de componentes sociales (SCF)](scf.md).

Este tutorial es principalmente para desarrolladores, nuevos AEM, interesados en utilizar componentes SCF. Recorre la creación de un sitio de espacio aislado de SCF, similar al tutorial de [Cómo crear un sitio web de Internet con todas las funciones](../../help/sites-developing/website.md) que se centra en las estructuras del sitio, como la navegación, el logotipo, la búsqueda, la barra de herramientas y el listado de páginas secundarias.

El desarrollo tiene lugar en una instancia de autor, mientras que la mejor manera de experimentar con el sitio es en una instancia de publicación.

Los pasos de este tutorial son:

* [Configuración de la estructura del sitio web](setup-website.md)
* [Aplicación de espacio aislado inicial](initial-app.md)
* [Contenido inicial del Simulador para pruebas](initial-content.md)
* [Desarrollar aplicación de espacio aislado](develop-app.md)
* [Agregar Clientlibs](add-clientlibs.md)
* [Desarrollar contenido de espacio aislado](develop-content.md)

>[!CAUTION]
>
>Este tutorial no crea un sitio de comunidad con la funcionalidad creada con el [Consola Sitios de Communities](sites-console.md). Por ejemplo, este tutorial no describe cómo configurar el inicio de sesión, el registro propio, [inicio de sesión social](social-login.md), mensajes, perfiles, etc.
>
>Si prefiere un sitio de comunidad simple, siga la [Crear una página de muestra](create-sample-page.md) tutorial.

## Requisitos previos {#prerequisites}

Este tutorial supone que tiene instalado un autor AEM y una instancia de publicación AEM que tiene la variable [última versión](deploy-communities.md#latest-releases) de las Comunidades.

A continuación, se muestran algunos vínculos útiles para los desarrolladores que van a la plataforma AEM:

* [Introducción](../../help/sites-deploying/deploy.md#getting-started): para implementar instancias de AEM.

   * [Conceptos básicos](../../help/sites-developing/the-basics.md): para desarrolladores de sitios web y funciones.
   * [Primeros pasos de creación](../../help/sites-authoring/first-steps.md): para crear contenido de página.

## Uso del entorno de desarrollo de CRXDE Lite {#using-crxde-lite-development-environment}

AEM desarrolladores pasan gran parte de su tiempo en el [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) entorno de desarrollo en una instancia de autor. CRXDE Lite proporciona un acceso menos restringido al repositorio CRX. Las herramientas de IU clásica y las consolas de IU con capacidad táctil proporcionan un acceso más estructurado a partes específicas del repositorio CRX.

Después de iniciar sesión con privilegios administrativos, hay varias formas de acceder al CRXDE Lite:

1. En la navegación global, seleccione navegación **[!UICONTROL Herramientas > CRXDE Lite]**.

   ![crxde-lite](assets/tools-crxde.png)

2. En el [página de bienvenida de la IU clásica](http://localhost:4502/welcome.html), desplácese hacia abajo y haga clic en **[!UICONTROL CRXDE Lite]** en el panel derecho.

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. Vaya directamente a `CRXDE Lite`: `<server>:<port>/crx/de`

   Por ejemplo, en una instancia de autor local: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

Para trabajar con CRXDE Lite, debe iniciar sesión con los privilegios de desarrollador o administrador. Para la instancia de host local predeterminada, puede iniciar sesión con

* `username: admin`
* `password: admin`


**Tenga en cuenta** que este inicio de sesión se agotará y tendrá que volver a iniciar sesión periódicamente mediante la lista desplegable del extremo derecho de la barra de herramientas CRXDe Lite.

Si no ha iniciado sesión, no podrá navegar por el repositorio de JCR ni realizar ninguna operación de edición o guardado.

***Cuando tenga dudas, vuelva a iniciar sesión.***

![volver a iniciar sesión](assets/relogin.png)
