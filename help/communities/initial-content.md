---
title: Contenido inicial de zona protegida
description: Crear contenido
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 068a0fff-ca48-4847-ba3f-d78416c97f6d
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 4%

---

# Contenido inicial de zona protegida {#initial-sandbox-content}

En esta sección, cree las siguientes páginas, que utilizan la variable [plantilla de página](initial-app.md#createthepagetemplate):

* Sitio de zona protegida de SCF, que redirige a la versión en inglés de la página principal.

   * Zona protegida de SCF: página principal de la versión en inglés del sitio.

   * Reproducción SCF: elemento secundario de la página principal en la que se va a reproducir.

Aunque este tutorial no profundiza en [copias de idioma](../../help/sites-administering/tc-prep.md), está diseñado para que la página raíz pueda implementar la detección del idioma preferido del usuario a través del encabezado del HTML y redirigir a la página principal adecuada para el idioma. La convención es utilizar el código de país de dos letras para el nombre del nodo de la página como, por ejemplo, &quot;en&quot; para inglés y &quot;fr&quot; para francés.

## Crear primeras páginas {#create-first-pages}

Ahora que hay un [plantilla de página](initial-app.md#createthepagetemplate), puede establecer la página raíz del sitio web en el directorio /content.

1. Actualmente, la IU estándar proporciona modelos para la creación de sitios. Como este tutorial crea un sitio simple, la IU clásica resulta útil.

   Para cambiar a la IU clásica, seleccione navegación global y pase el ratón sobre la parte derecha del icono Proyectos. Seleccione el *Cambiar a IU clásica* icono que aparece:

   ![classic-ui](assets/classic-ui.png)

   La capacidad para cambiar a la IU clásica debe ser [activado por un administrador](../../help/sites-administering/enable-classic-ui.md).

1. Desde el [Página de bienvenida de IU clásica](http://localhost:4502/welcome.html), seleccione **[!UICONTROL Sitios web]**.

   ![classic-ui-website](assets/classic-ui-website.png)

   También puede acceder a la IU clásica de los sitios web directamente desde el vínculo a [/siteadmin.](http://localhost:4502/siteadmin)

1. En el panel del explorador, seleccione **[!UICONTROL Sitios web]** y, en la barra de herramientas, seleccione **[!UICONTROL Nuevo]** > **[!UICONTROL Nueva página]**.

   En el **[!UICONTROL Crear página]** , introduzca lo siguiente:

   * Título: `SCF Sandbox Site`
   * Nombre: `an-scf-sandbox`
   * Seleccionar **[!UICONTROL Una plantilla de reproducción de zona protegida SCF]**
   * Haga clic en **[!UICONTROL Crear]**

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. En el panel del explorador, seleccione la página que ha creado, `/Websites/SCF Sandbox Site`y haga clic en **[!UICONTROL Nuevo]** > **[!UICONTROL Nueva página]**:

   * Título: `SCF Sandbox`
   * Nombre: `en`
   * Seleccionar **[!UICONTROL Una plantilla de reproducción de zona protegida SCF]**
   * Haga clic en **[!UICONTROL Crear]**

1. En el panel del explorador, seleccione la página que ha creado, `/Websites/SCF Sandbox Site/SCF Sandbox`y haga clic en **[!UICONTROL Nuevo]** > **[!UICONTROL Nueva página]**

   * Título: `SCF Play`
   * Nombre: `play`
   * Seleccionar **[!UICONTROL Una plantilla de reproducción de zona protegida SCF]**
   * Haga clic en **[!UICONTROL Crear]**

1. Así es como aparece ahora el sitio web en la consola Sitios web. Observe que las páginas secundarias del elemento seleccionado en el panel del explorador se muestran en el panel derecho donde se pueden administrar.

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   Esta es la vista del repositorio de lo que se creó con la herramienta Sitio web y la plantilla:

   ![classic-ui-repository-view](assets/classic-ui-repository-view.png)

## Añadir la ruta de diseño {#add-the-design-path}

Cuándo ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` se ha creado utilizando la sección diseños de la consola Herramientas, la propiedad &quot;

* `cq:template="/libs/wcm/core/templates/designpage"`

Se definió, lo que proporciona la capacidad opcional de hacer referencia a los recursos de diseño en una secuencia de comandos utilizando `currentDesign.getPath()`. Por ejemplo

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * Nombre: `cq:designPath`
   * Tipo: `String`
   * Valor: `/etc/designs/an-scf-sandbox`

* Haga clic en el icono verde `[+] Add`

El repositorio debe aparecer de la siguiente manera:

![classic-ui-repository-path](assets/classic-ui-repository-path.png)

* Haga clic en **[!UICONTROL Guardar todo]**

Si hay algún problema al guardar la configuración, vuelva a iniciar sesión y configure de nuevo.

>[!NOTE]
>
>El uso de `cq:designPath` es opcional y no está relacionado con el [uso de clientlibs](develop-app.md#includeclientlibsintemplate), que son necesarios, ya que los componentes de SCF utilizan [clientlibs](client-customize.md#clientlibs-for-scf) para administrar su JS y CSS.
