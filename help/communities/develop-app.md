---
title: Desarrollar aplicación de zona protegida
seo-title: Develop Sandbox Application
description: Desarrollar aplicaciones mediante scripts de base
seo-description: Develop application using foundation scripts
uuid: 572f68cd-9ecb-4b43-a7f8-4aa8feb6c64e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 910229a3-38b1-44f1-9c09-55f8fd6cbb1d
exl-id: 7ac0056c-a742-49f4-8312-2cf90ab9f23a
source-git-commit: 10227bcfcfd5a9b0f126fee74dce6ec7842f5e95
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 7%

---

# Desarrollar aplicación de zona protegida  {#develop-sandbox-application}

En esta sección, ahora que la plantilla se ha configurado en la variable [aplicación inicial](initial-app.md) y las páginas iniciales establecidas en la sección [contenido inicial](initial-content.md) , la aplicación se puede desarrollar utilizando secuencias de comandos de base, incluida la capacidad de habilitar la creación con componentes de Communities. Al final de esta sección, el sitio web estará en funcionamiento.

## Uso de scripts de página base {#using-foundation-page-scripts}

El script predeterminado, creado cuando se añadió el componente que procesa la plantilla de página de reproducción, se modifica para incluir head.jsp de la página de base y body.jsp local.

### Tipo de superrecurso {#super-resource-type}

El primer paso es agregar una propiedad de supertipo de recurso a `/apps/an-scf-sandbox/components/playpage` para que herede los scripts y las propiedades del supertipo.

Uso del CRXDE Lite:

1. Seleccionar nodo `/apps/an-scf-sandbox/components/playpage`.
1. En la pestaña Propiedades, introduzca una nueva propiedad con los siguientes valores:

   Nombre: `sling:resourceSuperType`

   Tipo: `String`

   Valor: `foundation/components/page`

1. Haga clic en el icono verde **[!UICONTROL +Agregar]** botón.
1. Haga clic en **[!UICONTROL Guardar todo]**.

   ![page-script](assets/page-script.png)

### Scripts de encabezado y cuerpo {#head-and-body-scripts}

1. Entrada **CRXDE Lite** panel del explorador, navegue hasta `/apps/an-scf-sandbox/components/playpage` y haga doble clic en el archivo `playpage.jsp` para abrirlo en el panel de edición.

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

1. Consciente de las etiquetas de script de apertura/cierre, reemplace &quot; // TODO ...&quot; por inclusiones de scripts para las partes de la cabeza y el cuerpo de &lt;html>.

   Con un super tipo de `foundation/components/page`, cualquier script no definido en esta misma carpeta se resolverá en un script en `/apps/foundation/components/page` carpeta (si existe), de lo contrario a una secuencia de comandos en `/libs/foundation/components/page` carpeta.

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

1. El script de base `head.jsp` no necesita superponerse, pero el script de base `body.jsp` está vacío.

   Para configurar la creación, haga clic en Superponer `body.jsp` con una secuencia de comandos local e incluya un sistema de párrafos (parsys) en el cuerpo:

   1. Navegue hasta `/apps/an-scf-sandbox/components`.
   1. Seleccione el `playpage` nodo.
   1. Haga clic con el botón derecho y seleccione `Create > Create File...`

      * Nombre: **body.jsp**

   1. Haga clic en **[!UICONTROL Guardar todo]**.

   Abrir `/apps/an-scf-sandbox/components/playpage/body.jsp` y pegue el texto siguiente:

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

**Ver la página en un explorador en modo de edición:**

* IU estándar: `http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html`

No solo debería ver el encabezado **Community Play**, pero también la interfaz de usuario para editar contenido de página.

El panel lateral Recursos/Componente se ve cuando tanto el panel lateral se abre alternativamente y la ventana es lo suficientemente ancha como para que se muestre el contenido del lado y el contenido de la página.

![view-page](assets/view-page.png)

* IU clásica: `http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html`

A continuación, se muestra cómo aparece la página de reproducción en la IU clásica, incluido con el buscador de contenido (cf):

![play-page-view](assets/play-page-view.png)

## Componentes de Communities {#communities-components}

Para habilitar los componentes de Communities para la creación, comience por seguir estas instrucciones:

* [Acceder a componentes de Communities](basics.md#accessing-communities-components)

Para los fines de esta zona protegida, comience con lo siguiente **Communities** componentes (active la casilla):

* Comentarios
* Foro
* Clasificación
* Repasos
* Resumen de críticas (visualización)
* Votación

Además, elija **[!UICONTROL General]** componentes, como

* Imagen
* Tabla
* Texto
* Título (Foundation)

>[!NOTE]
>
>Los componentes habilitados para el par de página se almacenan en el repositorio como el valor del `components` propiedad del
>
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` node.

## Página de aterrizaje {#landing-page}

En un entorno de varios idiomas, la página raíz incluiría una secuencia de comandos que analizaría la solicitud del cliente para determinar el idioma preferido.

En este ejemplo sencillo, la página raíz se está configurando estáticamente para redirigir a la página en inglés, que puede desarrollarse en el futuro para que sea la página de aterrizaje principal con un vínculo a la página de reproducción.

Cambie la dirección URL del explorador a la página raíz: `http://localhost:4502/editor.html/content/an-scf-sandbox.html`

* Seleccione el icono Información de página
* Seleccionar **[!UICONTROL Abrir propiedades]**
* En la pestaña AVANZADAS

   * Para la entrada Redirigir, vaya a **[!UICONTROL Sitios web]** > **[!UICONTROL Sitio de zona protegida SCF]** > **[!UICONTROL Zona protegida SCF]**
   * Haga clic en **[!UICONTROL Aceptar]**

* Haga clic en **[!UICONTROL Aceptar]**

Una vez publicado el sitio, la navegación a la página raíz de una instancia de publicación redireccionará a la página en inglés.

El último paso antes de jugar con los componentes SCF de las comunidades es añadir una carpeta de biblioteca de cliente (clientlibs) .... [Añadir Clienlibs](add-clientlibs.md)
