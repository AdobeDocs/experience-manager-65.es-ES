---
title: Creación de una zona protegida SCF
description: Este tutorial es principalmente para desarrolladores, nuevos en AEM, interesados en utilizar componentes de SCF. Recorre la creación de un sitio de espacio aislado de SCF
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 89858814-6625-4a56-8359-cc1eca402816
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%
---
# Creación de una zona protegida SCF  {#create-an-scf-sandbox}

En las comunidades de AEM 6.1, la forma más sencilla de crear rápidamente una zona protegida es crear un sitio de comunidad. Consulte [Introducción a AEM Communities](getting-started.md).

Otra herramienta útil para los desarrolladores es la [Guía de componentes de la comunidad](components-guide.md), que permite explorar y crear prototipos rápidos de componentes y características de Communities.

El ejercicio de crear un sitio web puede ser útil para comprender la estructura de un sitio web de AEM que puede incluir características de Communities y, al mismo tiempo, proporcionar páginas sencillas en las que explorar el trabajo con el [marco de componentes sociales (SCF)](scf.md).

Este tutorial es principalmente para desarrolladores, nuevos en AEM, interesados en utilizar componentes de SCF. Recorre la creación de un sitio de espacio aislado de SCF, similar al tutorial de [Cómo crear un sitio web de Internet con todas las funciones](../../help/sites-developing/website.md), que se centra en estructuras del sitio, como la navegación, el logotipo, la búsqueda, la barra de herramientas y la lista de páginas secundarias.

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

En este tutorial se da por hecho que tiene instalados un autor de AEM y una instancia de publicación de AEM con la [última versión](deploy-communities.md#latest-releases) de Communities.

A continuación se muestran algunos vínculos útiles para los desarrolladores que utilicen la plataforma AEM por primera vez:

* [Introducción](../../help/sites-deploying/deploy.md#getting-started): para implementar instancias de AEM.

  * [Conceptos básicos](../../help/sites-developing/the-basics.md): para desarrolladores de sitios web y características.
  * [Primeros pasos para los autores](../../help/sites-authoring/first-steps.md): para crear contenido de página.

## Uso del entorno de desarrollo de CRXDE Lite {#using-crxde-lite-development-environment}

Los desarrolladores de AEM pasan gran parte de su tiempo en el entorno de desarrollo de [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) en una instancia de autor. CRXDE Lite proporciona un acceso menos restringido al repositorio de CRX. Las herramientas de IU clásica y las consolas de IU táctiles proporcionan un acceso más estructurado a partes específicas del repositorio de CRX.

Después de iniciar sesión con privilegios administrativos, hay varias formas de acceder a CRXDE Lite:

1. En la navegación global, seleccione la navegación **[!UICONTROL Herramientas > CRXDE Lite]**.

   ![crxde-lite](assets/tools-crxde.png)

2. En la [página de bienvenida de la IU clásica](http://localhost:4502/welcome.html), desplácese hacia abajo y haga clic en **[!UICONTROL CRXDE Lite]** en el panel derecho.

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. Examinar directamente `CRXDE Lite`: `<server>:<port>/crx/de`

   Por ejemplo, en una instancia de autor local: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

Para trabajar con CRXDE Lite, debe iniciar sesión con privilegios de desarrollador o administrador. Para la instancia de localhost predeterminada, puede iniciar sesión con

* `username: admin`
* `password: admin`


Se agota el tiempo de espera de este inicio de sesión y debe volver a iniciarlo periódicamente mediante la lista desplegable situada en el extremo derecho de la barra de herramientas de CRXDE Lite.

Si no ha iniciado sesión, no podrá navegar por el repositorio JCR ni realizar operaciones de edición/guardado.

***¡En caso de duda, vuelva a iniciar sesión!***

![volver a iniciar sesión](assets/relogin.png)
