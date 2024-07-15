---
title: Creación de una zona protegida SCF
description: AEM Este tutorial es principalmente para desarrolladores, nuevos en el ámbito de la aplicación, que están interesados en utilizar componentes de SCF. Recorre la creación de un sitio de espacio aislado de SCF
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 89858814-6625-4a56-8359-cc1eca402816
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# Creación de una zona protegida SCF  {#create-an-scf-sandbox}

AEM A partir de comunidades de 6.1, la forma más sencilla de crear rápidamente una zona protegida es crear un sitio de comunidad. Consulte [Introducción a AEM Communities](getting-started.md).

Otra herramienta útil para los desarrolladores es la [Guía de componentes de la comunidad](components-guide.md), que permite explorar y crear prototipos rápidos de componentes y características de Communities.

AEM El ejercicio de crear un sitio web puede ser útil para comprender la estructura de un sitio web de la comunidad que puede incluir características de comunidades, a la vez que proporciona páginas sencillas en las que explorar el trabajo con el [marco de componentes sociales (SCF)](scf.md).

AEM Este tutorial es principalmente para desarrolladores, nuevos en el ámbito de la aplicación, que están interesados en utilizar componentes de SCF. Recorre la creación de un sitio de espacio aislado de SCF, similar al tutorial de [Cómo crear un sitio web de Internet con todas las funciones](../../help/sites-developing/website.md), que se centra en estructuras del sitio, como la navegación, el logotipo, la búsqueda, la barra de herramientas y la lista de páginas secundarias.

El desarrollo se produce en una instancia de autor, mientras que la experimentación con el sitio es mejor en una instancia de publicación.

Los pasos de este tutorial son los siguientes:

* [Configurar estructura del sitio web](setup-website.md)
* [Aplicación de zona protegida inicial](initial-app.md)
* [Contenido inicial de zona protegida](initial-content.md)
* [Desarrollar aplicación de zona protegida](develop-app.md)
* [Añadir Clientlibs](add-clientlibs.md)
* [Desarrollar contenido de zona protegida](develop-content.md)

>[!CAUTION]
>
>Este tutorial no crea un sitio de comunidad con la funcionalidad creada mediante la consola [Sitios de comunidades](sites-console.md). Por ejemplo, este tutorial no describe cómo configurar el inicio de sesión, el registro automático, el [inicio de sesión social](social-login.md), la mensajería, los perfiles, etc.
>
>Si prefiere un sitio de comunidad simple, siga el tutorial [Crear una página de muestra](create-sample-page.md).

## Requisitos previos {#prerequisites}

AEM AEM En este tutorial se da por hecho que tiene instalados una instancia de autor y una instancia de publicación que tiene instalada la [última versión](deploy-communities.md#latest-releases) de Comunidades, y que tienen instaladas una sola instancia de autor y una instancia de publicación, respectivamente.

AEM A continuación se muestran algunos vínculos útiles para los desarrolladores que son nuevos en la plataforma de:

* AEM [Primeros pasos](../../help/sites-deploying/deploy.md#getting-started): para implementar instancias de.

   * [Conceptos básicos](../../help/sites-developing/the-basics.md): para desarrolladores de sitios web y características.
   * [Primeros pasos para los autores](../../help/sites-authoring/first-steps.md): para crear contenido de página.

## Uso del entorno de desarrollo de CRXDE Lite {#using-crxde-lite-development-environment}

AEM Los desarrolladores de pasan gran parte de su tiempo en el entorno de desarrollo [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) en una instancia de autor. CRXDE Lite proporciona un acceso menos restringido al repositorio de CRX. Las herramientas de IU clásica y las consolas de IU táctiles proporcionan un acceso más estructurado a partes específicas del repositorio de CRX.

Después de iniciar sesión con privilegios de administrador, hay varias formas de acceder a CRXDE Lite:

1. En la navegación global, seleccione la navegación **[!UICONTROL Herramientas > CRXDE Lite]**.

   ![crxde-lite](assets/tools-crxde.png)

2. En la [página de bienvenida de la IU clásica](http://localhost:4502/welcome.html), desplácese hacia abajo y haga clic en **[!UICONTROL CRXDE Lite]** en el panel derecho.

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. Examinar directamente `CRXDE Lite`: `<server>:<port>/crx/de`

   Por ejemplo, en una instancia de autor local: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

Para trabajar con CRXDE Lite, debe iniciar sesión con privilegios de desarrollador o administrador. Para la instancia de localhost predeterminada, puede iniciar sesión con

* `username: admin`
* `password: admin`


Este inicio de sesión agota el tiempo de espera y debe volver a iniciarlo periódicamente mediante la lista desplegable situada en el extremo derecho de la barra de herramientas del CRXDE Lite.

Si no ha iniciado sesión, no podrá navegar por el repositorio JCR ni realizar operaciones de edición/guardado.

***¡En caso de duda, vuelva a iniciar sesión!***

![volver a iniciar sesión](assets/relogin.png)
