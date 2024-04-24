---
title: Añadir Clientlibs
description: Aprenda a agregar una ClientLibraryFolder (clientlibs) que se utilice para contener las hojas de estilo en cascada y JavaScript utilizadas para representar las páginas del sitio.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 569f2052-b4fe-4f7f-aec9-657217cba091
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# Añadir Clientlibs {#add-clientlibs}

## Añadir una ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Cree una ClientLibraryFolder con el nombre `clientlibs` que contiene las hojas de estilos en cascada (CSS) y JavaScript (JS) utilizadas para representar las páginas del sitio.

El `categories` el valor de propiedad dado a esta biblioteca de cliente es el identificador utilizado para incluir directamente esta clientlib de una página de contenido o para incrustarla en otras clientlibs.

1. Uso de **CRXDE Lite**, expanda `/etc/designs`

1. Clic con el botón derecho `an-scf-sandbox` y seleccione `Create Node`

   * Nombre : `clientlibs`
   * Tipo : `cq:ClientLibraryFolder`

1. Clic **OK**

![add-client-library](assets/add-client-library.png)

En el **Propiedades** para el nuevo `clientlibs` , introduzca el **categorías** propiedad:

* Nombre : **categorías**
* Tipo : **Cadena**
* Valor : **apps.an-scf-sandbox**
* Clic **Añadir**
* Clic **Guardar todo**

Nota: anteponga el valor de categorías con &quot;apps&quot;. es una convención para identificar la &quot;aplicación propietaria&quot; como en la carpeta /apps, no /libs. IMPORTANTE: Agregar marcador de posición `js.tx`t y **`css.txt`** archivos. (No es oficialmente una cq:ClientLibraryFolder sin ellas).

1. Clic con el botón derecho **`/etc/designs/an-scf-sandbox/clientlibs`**
1. Seleccionar **Crear archivo...**
1. Entrar **Nombre:** `css.txt`
1. Seleccionar **Crear archivo...**
1. Entrar **Nombre:** `js.txt`
1. Clic **Guardar todo**

![clientlibs-css](assets/clientlibs-css.png)

La primera línea de los archivos css.txt y js.txt identifica la ubicación base desde la que se encuentran las siguientes listas de archivos.

Intente establecer el contenido de css.txt en

```
#base=.
 style.css
```

A continuación, cree un archivo en clientlibs denominado style.css y establezca el contenido en

`body {`

`background-color: #b0c4de;`

`}`

### Incrustar Clientlibs SCF {#embed-scf-clientlibs}

En el **Propiedades** para la pestaña `clientlibs` , introduzca la propiedad de cadena de varios valores **incrustar**. Esto incrusta lo necesario [bibliotecas del lado del cliente (clientlibs) para componentes de SCF](/help/communities/client-customize.md#clientlibs-for-scf). Para este tutorial, se agregan muchos de los clientlibs necesarios para los componentes de Communities.

Este puede ser o no el enfoque deseado para utilizar en un sitio de producción, ya que hay consideraciones de comodidad en comparación con el tamaño y la velocidad de los clientlibs descargados para cada página.

Si solo utiliza una función en una página, puede incluir la clientlib completa de esa función directamente en la página, por ejemplo,

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

En este caso, incluyéndolos todos y por lo tanto se prefieren los clientlibs SCF más básicos que son los clientlibs de autor:

* Nombre : **`embed`**
* Tipo : **`String`**
* Clic **`Multi`**
* Valor: **`cq.social.scf`**

   * Aparecerá un cuadro de diálogo, haga clic en **`+`** después de cada entrada para agregar las siguientes categorías clientlib:

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * Clic **OK**

* Clic **Guardar todo**

![scf-clientlibs](assets/scf-clientlibs.png)

Así es como `/etc/designs/an-scf-sandbox/clientlibs` debería aparecer en el repositorio:

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### Incluir Clientlibs en la plantilla de PlayPage {#include-clientlibs-in-playpage-template}

Sin incluir el `apps.an-scf-sandbox` En la categoría ClientLibraryFolder de la página, los componentes SCF no funcionan ni tienen estilo, ya que los estilos JavaScript y CSS necesarios no están disponibles.

Por ejemplo, sin incluir los clientlibs, el componente Comentarios de SCF aparece sin estilo :

![clientlibs-comment](assets/clientlibs-comment.png)

Una vez que se incluye apps.an-scf-sandbox clientlibs, el componente Comentarios de SCF aparece con el siguiente estilo:

![clientlibs-comment-styled](assets/clientlibs-comment1.png)

La instrucción include pertenece al `head` de la sección `html` script. El valor predeterminado **`foundation head.jsp`** incluye una secuencia de comandos que se puede superponer: **`headlibs.jsp`**.

**Copie headlibs.jsp e incluya clientlibs:**

1. Uso de **CRXDE Lite**, seleccione **`/libs/foundation/components/page/headlibs.jsp`**

1. Haga clic con el botón derecho y seleccione **Copiar** (o seleccione Copiar en la barra de herramientas)
1. Seleccionar **`/apps/an-scf-sandbox/components/playpage`**
1. Haga clic con el botón derecho y seleccione **Pegar** (o seleccione Pegar en la barra de herramientas)
1. Doble clic **`headlibs.jsp`** para que pueda abrirlo
1. Anexe la línea siguiente al final del archivo
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. Clic **Guardar todo**

```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

Cargue el sitio web en el explorador y compruebe si el fondo no es azul.

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![juego comunitario](assets/community-play.png)

### Guardar El Trabajo Hasta El Momento {#saving-your-work-so-far}

En este punto, existe una zona protegida minimalista. Puede valer la pena guardarlo como un paquete para que, mientras se reproduce, si el repositorio se daña y desea volver a empezar, pueda desactivar el servidor. A continuación, cambie el nombre de la carpeta crx-quickstart/, encienda el servidor, cargue e instale este paquete guardado y no tenga que repetir estos pasos más básicos.

Este paquete existe en [Crear una página de muestra](/help/communities/create-sample-page.md) tutorial para aquellos que no pueden esperar para saltar y comenzar a jugar.

Para crear un paquete:

* En el CRXDE Lite, haga clic en [Icono de paquete](https://localhost:4502/crx/packmgr/)
* Clic **Crear paquete**

   * Nombre del paquete: an-scf-sandbox-minimal-pkg
   * Versión: 0.1
   * Grupo: `leave as default`
   * Clic **OK**

* Clic **Editar**

   * Seleccionar **Filtros** pestaña

      * Clic **Añadir filtro**
      * Ruta raíz: buscar `/apps/an-scf-sandbox`
      * Haga clic en **Listo**.
      * Clic **Añadir filtro**
      * Ruta raíz: buscar `/etc/designs/an-scf-sandbox`
      * Haga clic en **Listo**.
      * Clic **Añadir filtro**
      * Ruta raíz: buscar `/content/an-scf-sandbox**`
      * Haga clic en **Listo**.

   * Clic **Guardar**

* Clic **Generar**

Ahora puede seleccionar **Descargar** para guardarlo en el disco y **Cargar paquete** en otra parte y seleccione **Más > Replicar** para insertar la zona protegida en una instancia de publicación localhost para expandir el dominio de la zona protegida.
