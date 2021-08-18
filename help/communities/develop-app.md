---
title: Desarrollar aplicación de espacio aislado
seo-title: Desarrollar aplicación de espacio aislado
description: Desarrollo de aplicaciones mediante secuencias de comandos de base
seo-description: Desarrollo de aplicaciones mediante secuencias de comandos de base
uuid: 572f68cd-9ecb-4b43-a7f8-4aa8feb6c64e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 910229a3-38b1-44f1-9c09-55f8fd6cbb1d
exl-id: 7ac0056c-a742-49f4-8312-2cf90ab9f23a
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 5%

---

# Desarrollar aplicación de espacio aislado  {#develop-sandbox-application}

En esta sección, ahora que la plantilla se ha configurado en la sección [aplicación inicial](initial-app.md) y en las páginas iniciales establecidas en la sección [contenido inicial](initial-content.md), la aplicación se puede desarrollar utilizando secuencias de comandos de base, incluida la capacidad de habilitar la creación con componentes de Communities. Al final de esta sección, el sitio web funcionará.

## Uso de scripts de página base {#using-foundation-page-scripts}

La secuencia de comandos predeterminada, creada cuando se agregó el componente que procesa la plantilla de página de reproducción, se modifica para incluir el head.jsp de la página de base y un body.jsp local.

### Tipo de recurso superior {#super-resource-type}

El primer paso es agregar una propiedad de supertipo de recurso al nodo `/apps/an-scf-sandbox/components/playpage` para que herede las secuencias de comandos y propiedades del supertipo.

Uso del CRXDE Lite:

1. Seleccione el nodo `/apps/an-scf-sandbox/components/playpage`.
1. En la pestaña propiedades, introduzca una nueva propiedad con los siguientes valores:

   Nombre: `sling:resourceSuperType`

   Tipo: `String`

   Value: `foundation/components/page`

1. Haga clic en el botón verde **[!UICONTROL +Add]**.
1. Haga clic en **[!UICONTROL Guardar todo]**.

   ![page-script](assets/page-script.png)

### Secuencias de comandos de cabezal y cuerpo {#head-and-body-scripts}

1. En el panel del explorador **CRXDE Lite**, vaya a `/apps/an-scf-sandbox/components/playpage` y haga doble clic en el archivo `playpage.jsp` para abrirlo en el panel de edición.

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

   ```xml
   <%--
   
     An SCF Sandbox Play Component component.
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %><%
   %><%
    // TODO add your code here
   %>
   ```

1. Teniendo en cuenta las etiquetas de script abiertas/cercanas, sustituya &quot; // TODO ...&quot; con incluye secuencias de comandos para las partes del encabezado y del cuerpo de &lt;html>.

   Con un supertipo de `foundation/components/page`, cualquier script que no esté definido en esta misma carpeta se convertirá en un script de la carpeta `/apps/foundation/components/page` (si existe) o en un script de la carpeta `/libs/foundation/components/page`.

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

   ```xml
   <%--
   
       An SCF Sandbox Play Component component: playpage.jsp
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %>
   <html>
     <cq:include script="head.jsp"/>
     <cq:include script="body.jsp"/>
   </html>
   ```

1. No es necesario superponer el script de base `head.jsp`, pero el script de base `body.jsp` está vacío.

   Para configurar la creación, superponga `body.jsp` con un script local e incluya un sistema de párrafos (parsys) en el cuerpo:

   1. Ir a `/apps/an-scf-sandbox/components`.
   1. Seleccione el nodo `playpage`.
   1. Haga clic con el botón derecho y seleccione `Create > Create File...`

      * Nombre: **body.jsp**
   1. Haga clic en **[!UICONTROL Guardar todo]**.

   Abra `/apps/an-scf-sandbox/components/playpage/body.jsp` y pegue el siguiente texto:

   ```xml
   <%--
   
       An SCF Sandbox Play Component component: body.jsp
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %>
   <body>
       <h2>Community Play</h2>
       <cq:include path="par" resourceType="foundation/components/parsys" />
   </body>
   ```

1. Haga clic en **[!UICONTROL Guardar todo]**.

**Vea la página en un explorador en modo de edición:**

* IU estándar: `http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html`

No solo debería ver el encabezado **Reproducción comunitaria**, sino también la IU para editar el contenido de la página.

El panel lateral Recursos/Componente se ve cuando se abre de forma alternada el panel lateral y la ventana es lo suficientemente ancha como para que se muestre tanto el contenido lateral como el contenido de la página.

![ver-página](assets/view-page.png)

* IU clásica: `http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html`

A continuación, se muestra cómo aparece la página de reproducción en la IU clásica, incluso con el buscador de contenido (cf):

![play-page-view](assets/play-page-view.png)

## Componentes de Communities {#communities-components}

Para habilitar los componentes de Communities para la creación, comience por seguir estas instrucciones:

* [Acceso a componentes de Communities](basics.md#accessing-communities-components)

Para los fines de este simulador para pruebas, comience con estos componentes **Communities** (habilite marcando la casilla ):

* Comentarios
* Foro
* Clasificación
* Críticas
* Resumen de críticas (visualización)
* Votación

Además, seleccione los componentes **[!UICONTROL General]**, como

* Imagen
* Tabla
* Texto
* Título (Foundation)

>[!NOTE]
>
>Los componentes habilitados para la página par se almacenan en el repositorio como el valor de la propiedad `components` del
>
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` nodo .

## Página de aterrizaje {#landing-page}

En un entorno de varios idiomas, la página raíz incluiría una secuencia de comandos que analizaría la solicitud del cliente para determinar el idioma preferido.

En este ejemplo sencillo, la página raíz se está configurando de forma estática para redirigir a la página en inglés, que puede desarrollarse en el futuro para ser la página de aterrizaje principal con un vínculo a la página de reproducción.

Cambie la URL del explorador a la página raíz: `http://localhost:4502/editor.html/content/an-scf-sandbox.html`

* Seleccione el icono Información de página
* Seleccione **[!UICONTROL Abrir propiedades]**
* En la ficha AVANZADO

   * Para la entrada de redireccionamiento, vaya a **[!UICONTROL Sitios web]** > **[!UICONTROL Sitio del Simulador para pruebas SCF]** > **[!UICONTROL Espacio para pruebas SCF]**
   * Haga clic en **[!UICONTROL Aceptar]**

* Haga clic en **[!UICONTROL Aceptar]**

Una vez publicado el sitio, la navegación a la página raíz de una instancia de publicación se redirigirá a la página en inglés.

El último paso antes de jugar con los componentes SCF de comunidades es añadir una carpeta de biblioteca de clientes (clientlibs) .... [Agregar Clienlibs](add-clientlibs.md)
