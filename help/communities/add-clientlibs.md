---
title: Agregar Clientlibs
seo-title: Add Clientlibs
description: Agregar una carpeta ClientLibrary
seo-description: Add a ClientLibraryFolder
uuid: 2944923d-caca-4607-81a4-4122a2ce8e41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 46f81c3f-6512-43f1-8ec1-cc717ab6f6ff
docset: aem65
exl-id: 569f2052-b4fe-4f7f-aec9-657217cba091
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 6%

---

# Agregar Clientlibs {#add-clientlibs}

## Agregar una ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Crear una ClientLibraryFolder denominada `clientlibs` que contendrán los JS y CSS utilizados para procesar las páginas del sitio.

La variable `categories` el valor de propiedad dado a esta biblioteca de cliente es el identificador utilizado para incluir directamente esta clientlib desde una página de contenido o para incrustarla en otras clientlibs.

1. Uso **CRXDE Lite**, expandir `/etc/designs`

1. Clic con el botón derecho `an-scf-sandbox` y seleccione `Create Node`

   * Nombre : `clientlibs`
   * Tipo : `cq:ClientLibraryFolder`

1. Haga clic en **Aceptar**

![add-client-library](assets/add-client-library.png)

En el **Propiedades** para la nueva `clientlibs` , introduzca el **categories** propiedad:

* Nombre : **categories**
* Tipo : **Cadena**
* Valor : **apps.an-scf-sandbox**
* Haga clic en **Agregar**
* Haga clic en **Guardar todo**

Nota : anteponer el valor de categorías a &quot;apps&quot;. es una convención para identificar la &quot;aplicación propietaria&quot; como si estuviera en la carpeta /apps, no en /libs.  IMPORTANTE : Agregar marcador de posición `js.tx`t y **`css.txt`** archivos. (No es oficialmente un cq:ClientLibraryFolder sin ellos).

1. Clic con el botón derecho **`/etc/designs/an-scf-sandbox/clientlibs`**
1. Select **Crear archivo...**
1. Entrar **Nombre:** `css.txt`
1. Select **Crear archivo...**
1. Entrar **Nombre:** `js.txt`
1. Haga clic en **Guardar todo**

![clientlibs-css](assets/clientlibs-css.png)

La primera línea de css.txt y js.txt identifica la ubicación base desde la que se encuentran las siguientes listas de archivos.

Intente configurar el contenido de css.txt en

```
#base=.
 style.css
```

A continuación, cree un archivo en clientlibs llamado style.css y establezca el contenido en

`body {`

`background-color: #b0c4de;`

`}`

### Incrustar Clientlibs SCF {#embed-scf-clientlibs}

En el **Propiedades** para la variable `clientlibs` , introduzca la propiedad String de varios valores. **embed**. Esto incrusta lo necesario [bibliotecas del lado del cliente (clientlibs) para componentes SCF](/help/communities/client-customize.md#clientlibs-for-scf). Para este tutorial, se añaden muchos de los clientlibs necesarios para los componentes Communities.

**Nota** que este puede ser o no el método deseado para usar en un sitio de producción, ya que existen consideraciones de comodidad en comparación con el tamaño/velocidad de los clientlibs descargados para cada página.

Si solo utiliza una función en una página, puede incluir la clientlib completa de esa característica directamente en la página, por ejemplo,

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

En este caso, incluidos todos y así los clientlibs de SCF más básicos, que son los clientlibs de autor, son preferibles:

* Nombre : **`embed`**
* Tipo : **`String`**
* Haga clic **`Multi`**
* Valor: **`cq.social.scf`**

   * Aparecerá un cuadro de diálogo, haga clic en **`+`** después de cada entrada para añadir las siguientes categorías clientlib:

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * Haga clic en **Aceptar**

* Haga clic en **Guardar todo**

![scf-clientlibs](assets/scf-clientlibs.png)

Así es como `/etc/designs/an-scf-sandbox/clientlibs` debería aparecer en el repositorio :

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### Incluir Clientlibs en la plantilla de PlayPage {#include-clientlibs-in-playpage-template}

Sin incluir el `apps.an-scf-sandbox` categoría ClientLibraryFolder en la página; los componentes SCF no funcionarán ni se diseñarán, ya que los Javascript y los estilos necesarios no estarán disponibles.

Por ejemplo, sin incluir clientlibs, el componente de comentarios de SCF aparece sin estilo :

![clientlibs-comment](assets/clientlibs-comment.png)

Una vez que se incluye apps.an-scf-sandbox clientlibs , el componente de comentarios de SCF aparece con estilo:

![clientlibs-comment-style](assets/clientlibs-comment1.png)

La sentencia include pertenece al grupo `head` de la sección `html` secuencia de comandos. El valor predeterminado **`foundation head.jsp`** incluye una secuencia de comandos que se puede superponer: **`headlibs.jsp`**.

**Copie headlibs.jsp e incluya clientlibs:**

1. Uso **CRXDE Lite**, seleccione **`/libs/foundation/components/page/headlibs.jsp`**

1. Haga clic con el botón derecho y seleccione **Copiar** (o seleccione Copiar en la barra de herramientas)
1. Seleccione **`/apps/an-scf-sandbox/components/playpage`**
1. Haga clic con el botón derecho y seleccione **Pegar** (o seleccione Pegar en la barra de herramientas)
1. Hacer doble clic **`headlibs.jsp`** para abrirlo
1. Añada la línea siguiente al final del archivo
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. Haga clic en **Guardar todo**

```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

Cargue el sitio web en el explorador y compruebe si el fondo no está a la sombra de azul.

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![community-play](assets/community-play.png)

### Guardar su trabajo hasta ahora {#saving-your-work-so-far}

En este punto, existe un simulador de pruebas minimalista y puede que valga la pena guardarlo como paquete para que, mientras se reproduce, si el repositorio se daña y desea volver a empezar, puede desactivar el servidor, cambiar el nombre o eliminar la carpeta crx-quickstart/, activar el servidor, cargar e instalar este paquete guardado y no tener que repetir estos pasos más básicos.

Este paquete existe en la variable [Crear una página de muestra](/help/communities/create-sample-page.md) tutorial para aquellos que no pueden esperar para simplemente saltar y comenzar a jugar!...

Para crear un paquete:

* En el CRXDE Lite, haga clic en el [Icono de paquete](https://localhost:4502/crx/packmgr/)
* Haga clic en **Crear paquete**

   * Nombre del paquete: an-scf-sandbox-Minimum-pkg
   * Versión: 0,1
   * Grupo: `leave as default`
   * Haga clic en **Aceptar**

* Haga clic en **Editar**

   * Select **Filtros** ficha

      * Haga clic en **Añadir filtro**
      * Ruta raíz: buscar `/apps/an-scf-sandbox`
      * Haga clic en **Listo**
      * Haga clic en **Añadir filtro**
      * Ruta raíz: buscar `/etc/designs/an-scf-sandbox`
      * Haga clic en **Listo**
      * Haga clic en **Añadir filtro**
      * Ruta raíz: buscar `/content/an-scf-sandbox**`
      * Haga clic en **Listo**
   * Haga clic en **Guardar**


* Haga clic en **Generar**

Ahora puede seleccionar **Descargar** para guardarlo en disco y **Cargar paquete** en cualquier otra parte, así como seleccionar **Más > Replicar** para insertar el simulador de pruebas en una instancia de publicación de localhost para expandir el dominio del simulador de pruebas.
