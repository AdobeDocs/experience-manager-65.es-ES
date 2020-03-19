---
title: Desarrollar aplicación de Simulador para pruebas
seo-title: Desarrollar aplicación de Simulador para pruebas
description: Desarrollo de aplicaciones mediante scripts de base
seo-description: Desarrollo de aplicaciones mediante scripts de base
uuid: 572f68cd-9ecb-4b43-a7f8-4aa8feb6c64e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 910229a3-38b1-44f1-9c09-55f8fd6cbb1d
translation-type: tm+mt
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# Desarrollar aplicación de Simulador para pruebas {#develop-sandbox-application}

En esta sección, ahora que la plantilla se ha configurado en la sección de aplicación [](initial-app.md) inicial y en las páginas iniciales establecidas en la sección de contenido [](initial-content.md) inicial, la aplicación se puede desarrollar utilizando secuencias de comandos de base, incluida la capacidad de habilitar la creación con componentes de Comunidades. Al final de esta sección, el sitio web funcionará.

## Uso de scripts de página de base {#using-foundation-page-scripts}

La secuencia de comandos predeterminada, creada cuando se agregó el componente que procesa la plantilla de página de reproducción, se modifica para incluir head.jsp de la página de base y un body.jsp local.

### Tipo de recurso Super {#super-resource-type}

El primer paso es agregar una propiedad super type de recurso al `/apps/an-scf-sandbox/components/playpage` nodo para que herede las secuencias de comandos y propiedades del supertipo.

Uso de CRXDE Lite:

<!--Resolve steps below-->
    Nombre: `sling:resourceSuperType`
    Type: `String`
    Value: &quot;foundation/components/page&quot;

1. Haga clic en verde **[!UICONTROL [+]Agregar]**
1. Haga clic en **[!UICONTROL Guardar todo]**

![chlimage_1-231](assets/chlimage_1-231.png)

### Secuencias de comandos de cabeza y cuerpo {#head-and-body-scripts}

1. En el panel **CRXDE Lite** explorer, navegue hasta el archivo `/apps/an-scf-sandbox/components/playpage` y haga doble clic en él `playpage.jsp` para abrirlo en el panel de edición.

#### /apps/an-scf-sandbox/components/playpage/playpage.jsp {#apps-an-scf-sandbox-components-playpage-playpage-jsp}

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

1. Teniendo en cuenta las etiquetas de script abiertas/cerradas, reemplace &quot; // TODO ...&quot; con incluye secuencias de comandos para las partes del encabezado y del cuerpo de &lt;html>.

   Con un supertipo de `foundation/components/page`, cualquier secuencia de comandos no definida en la misma carpeta se resolverá en una secuencia de comandos de la `/apps/foundation/components/page` carpeta (si existe), o en una secuencia de comandos de la `/libs/foundation/components/page` carpeta.

#### /apps/an-scf-sandbox/components/playpage/playpage.jsp {#apps-an-scf-sandbox-components-playpage-playpage-jsp-1}

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

1. No `head.jsp` es necesario superponer la secuencia de comandos de base, pero la secuencia de comandos de base `body.jsp` está vacía.

   Para configurar la creación, superponga `body.jsp` con una secuencia de comandos local e incluya un sistema de párrafos (parsys) en el cuerpo:

   1. Ir a `/apps/an-scf-sandbox/components`
   1. Seleccione el `playpage`nodo
   1. Haga clic con el botón derecho y seleccione `Create > Create File...`

      * Nombre: **body.jsp**
   1. Haga clic en **[!UICONTROL Guardar todo]**
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

1. Haga clic en **[!UICONTROL Guardar todo]**

**Vea la página en un navegador en modo de edición:**

* IU estándar: [http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html](http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.md)

No solo debería ver el encabezado Reproducción **de la** comunidad, sino también la interfaz de usuario para editar el contenido de la página.

El panel lateral Recursos/Componente se ve cuando se abre de forma alternada el panel lateral y la ventana es lo suficientemente ancha como para que se muestren tanto el contenido lateral como el contenido de la página.

![chlimage_1-232](assets/chlimage_1-232.png)

* IU clásica: [http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html](http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html)

A continuación se muestra cómo aparece la página de reproducción en la IU clásica, incluso con Content Finder (cf):

![chlimage_1-233](assets/chlimage_1-233.png)

## Componentes de Communities {#communities-components}

Para habilitar los componentes de Comunidades para la creación, comience por seguir estas instrucciones:

* [Acceso a componentes de comunidades](basics.md#accessing-communities-components)

A los efectos de este simulador para pruebas, comience con estos componentes de **Comunidades** (active la casilla de verificación):

* Comentarios
* Foro
* Clasificación
* Críticas
* Resumen de críticas (visualización)
* Votación

Además, elija componentes **[!UICONTROL generales]** , como

* Imagen
* Tabla
* Texto
* Título (Foundation)

>[!NOTE]
>
>Los componentes activados para el par de página se almacenan en el repositorio como el valor de la `components` propiedad de la variable
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` nodo.

## Página de aterrizaje {#landing-page}

En un entorno de varios idiomas, la página raíz incluiría una secuencia de comandos que analizaría la solicitud del cliente para determinar el idioma preferido.

En este sencillo ejemplo, la página raíz se está configurando de forma estática para redireccionar a la página en inglés, que puede desarrollarse en el futuro para ser la página de aterrizaje principal con un vínculo a la página de reproducción.

Cambie la dirección URL del explorador a la página raíz: [http://localhost:4502/editor.html/content/an-scf-sandbox.html](https://locahost:4502/editor.html/content/an-scf-sandbox.html)

* Seleccione el icono Información de página
* Seleccionar propiedades **[!UICONTROL abiertas]**
* En la ficha AVANZADO

   * Para la entrada de redireccionamiento, vaya a **[!UICONTROL Sitios web > Sitio de Simulador para pruebas SCF > Simulador para pruebas SCF]**
   * Haga clic en **[!UICONTROL Aceptar]**

* Haga clic en **[!UICONTROL Aceptar]**

Una vez que se publique el sitio, la búsqueda en la página raíz de una instancia de publicación se redirigirá a la página en inglés.

El último paso antes de jugar con los componentes SCF de las comunidades es agregar una carpeta de biblioteca de clientes (clientlibs).... [Agregar clientes](add-clientlibs.md)