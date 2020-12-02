---
title: Contenido inicial del Simulador para pruebas
seo-title: Contenido inicial del Simulador para pruebas
description: Crear contenido
seo-description: Crear contenido
uuid: 9810fe47-8d1a-4238-9b9c-0cc47c63d97a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e8f28cd5-7950-4aab-bf62-3d4ed3d33cbd
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 5%

---


# Contenido inicial del Simulador para pruebas {#initial-sandbox-content}

En esta sección, se crean las páginas siguientes que utilizan la [plantilla de página](initial-app.md#createthepagetemplate):

* Sitio de Simulador para pruebas SCF, que redireccionará a la versión en inglés de la página principal.

   * Simulador para pruebas SCF: la página principal de la versión en inglés del sitio.

   * Reproducción SCF - Elemento secundario de la página principal en la que se va a reproducir.

Aunque este tutorial no profundiza en [copias de idioma](../../help/sites-administering/tc-prep.md), está diseñado para que la página raíz pueda implementar la detección del idioma preferido para el usuario a través del encabezado HTML y redireccionar a la página principal correspondiente para el idioma. La convención es utilizar el código de país de dos letras para el nombre de nodo de la página, por ejemplo, &quot;en&quot; para inglés, &quot;fr&quot; para francés, etc.

## Crear primeras páginas {#create-first-pages}

Ahora que existe una [plantilla de página](initial-app.md#createthepagetemplate), podemos establecer la página raíz del sitio Web en el directorio /content.

1. La interfaz de usuario estándar actualmente proporciona modelos para crear sitios. Como este tutorial está creando un sitio sencillo, la IU clásica resulta útil.

   Para cambiar a la IU clásica, seleccione la navegación global y coloque el puntero sobre el lado derecho del icono Proyectos. Seleccione el icono *Cambiar a IU clásica* que aparece:

   ![classic-ui](assets/classic-ui.png)

   La capacidad de cambiar a la IU clásica debe estar [habilitada por un administrador](../../help/sites-administering/enable-classic-ui.md).

1. En la [página de bienvenida de la IU clásica](http://localhost:4502/welcome.html), seleccione **[!UICONTROL Sitios web]**.

   ![classic-ui-website](assets/classic-ui-website.png)

   También puede acceder a la IU clásica para sitios web directamente navegando a [/siteadmin.](http://localhost:4502/siteadmin)

1. En el panel del explorador, seleccione **[!UICONTROL Sitios web]** y, a continuación, en la barra de herramientas, seleccione **[!UICONTROL Nueva]** > **[!UICONTROL Nueva página]**.

   En el cuadro de diálogo **[!UICONTROL Crear página]**, escriba lo siguiente:

   * Título: `SCF Sandbox Site`
   * Nombre: `an-scf-sandbox`
   * Seleccione **[!UICONTROL Una plantilla de reproducción de Simulador para pruebas SCF]**
   * Haga clic en **[!UICONTROL Crear]**

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. En el panel del explorador, seleccione la página que acaba de crear, `/Websites/SCF Sandbox Site`, y haga clic en **[!UICONTROL Nueva]** > **[!UICONTROL Nueva página]**:

   * Título: `SCF Sandbox`
   * Nombre: `en`
   * Seleccione **[!UICONTROL Una plantilla de reproducción de Simulador para pruebas SCF]**
   * Haga clic en **[!UICONTROL Crear]**

1. En el panel del explorador, seleccione la página que acaba de crear, `/Websites/SCF Sandbox Site/SCF Sandbox`, y haga clic en **[!UICONTROL Nueva]** > **[!UICONTROL Nueva página]**

   * Título: `SCF Play`
   * Nombre: `play`
   * Seleccione **[!UICONTROL Una plantilla de reproducción de Simulador para pruebas SCF]**
   * Haga clic en **[!UICONTROL Crear]**

1. Así es como el sitio web aparece ahora en la consola Sitios web. Observe que las páginas secundarias del elemento seleccionado en el panel del explorador se muestran en el panel derecho donde se pueden administrar.

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   Esta es la vista del repositorio de lo que se creó con la herramienta Sitio web y la plantilla:

   ![classic-ui-repository-vista](assets/classic-ui-repository-view.png)

## Añadir la ruta de diseño {#add-the-design-path}

Cuando ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` se creó mediante la sección de diseños de la consola Herramientas, la propiedad &quot;

* `cq:template="/libs/wcm/core/templates/designpage"`

, que proporciona la capacidad opcional de hacer referencia a recursos de diseño en una secuencia de comandos mediante `currentDesign.getPath()`. Por ejemplo

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * Nombre: `cq:designPath`
   * Tipo: `String`
   * Value: `/etc/designs/an-scf-sandbox`

* Haga clic en el `[+] Add` verde

El texto del repositor será el siguiente:

![classic-ui-Repository-path](assets/classic-ui-repository-path.png)

* Haga clic en **[!UICONTROL Guardar todo]**

Si hay algún problema al guardar la configuración, vuelva a iniciar sesión y configúrela de nuevo.

>[!NOTE]
>
>El uso de `cq:designPath` es opcional y no está relacionado con el [uso de clientlibs](develop-app.md#includeclientlibsintemplate), que son esencialmente necesarios ya que los componentes de SCF utilizan [clientlibs](client-customize.md#clientlibs-for-scf) para administrar sus JS y CSS.
