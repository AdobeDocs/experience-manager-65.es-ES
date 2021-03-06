---
title: Añadir Clientlibs
seo-title: Añadir Clientlibs
description: Añadir una ClientLibraryFolder
seo-description: Añadir una ClientLibraryFolder
uuid: 2944923d-caca-4607-81a4-4122a2ce8e41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 46f81c3f-6512-43f1-8ec1-cc717ab6f6ff
docset: aem65
translation-type: tm+mt
source-git-commit: fcdae5363e7a0070b5d6b76227e5c65efb71bc03
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 2%

---


# Añadir Clientlibs {#add-clientlibs}

## Añadir una ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Cree una ClientLibraryFolder con el nombre `clientlibs` que contendrá el JS y CSS utilizados para representar las páginas del sitio.

El valor de la propiedad `categories` que se da a esta biblioteca de cliente es el identificador utilizado para incluir directamente esta clientlib desde una página de contenido o para incrustarla en otros clientlibs.

1. Usando **CRXDE Lite**, expanda `/etc/designs`

1. Haga clic con el botón derecho `an-scf-sandbox` y seleccione `Create Node`

   * Nombre : `clientlibs`
   * Tipo : `cq:ClientLibraryFolder`

1. Haga clic en **Aceptar**

![add-client-library](assets/add-client-library.png)

En la ficha **Propiedades** del nuevo nodo `clientlibs`, introduzca la propiedad **categorías**:

* Nombre: **categorías**
* Tipo: **Cadena**
* Valor: **apps.an-scf-sandbox**
* Haga clic en **Agregar**
* Haga clic en **Guardar todo**

Nota: anteponer el valor de categorías con &#39;aplicaciones&#39;. es una convención para identificar la &#39;aplicación propietaria&#39; como una carpeta /apps, no como /libs.  IMPORTANTE: Añada los archivos de marcador de posición `js.tx`t y **`css.txt`**. (No es oficialmente un cq:ClientLibraryFolder sin ellos).

1. Haga clic con el botón derecho **`/etc/designs/an-scf-sandbox/clientlibs`**
1. Seleccione **Crear archivo...**
1. Escriba **Nombre:** `css.txt`
1. Seleccione **Crear archivo...**
1. Escriba **Nombre:** `js.txt`
1. Haga clic en **Guardar todo**

![clientlibs-css](assets/clientlibs-css.png)

La primera línea de css.txt y js.txt identifica la ubicación base desde la que se encuentran las siguientes listas de archivos.

Intente establecer el contenido de css.txt en

```
#base=.
 style.css
```

A continuación, cree un archivo en clientlibs llamado style.css y defina el contenido en

`body {`

`background-color: #b0c4de;`

`}`

### Incrustar clientes SCF {#embed-scf-clientlibs}

En la ficha **Propiedades** del nodo `clientlibs`, introduzca la propiedad de varios valores String **embed**. Esto incrusta las [bibliotecas del lado del cliente (clientlibs) necesarias para los componentes de SCF](/help/communities/client-customize.md#clientlibs-for-scf). Para este tutorial se añaden muchos de los clientlibs necesarios para los componentes Communities.

**** Tenga en cuenta que este método puede ser o no el deseado para un sitio de producción, ya que existen consideraciones de conveniencia en comparación con el tamaño y la velocidad de los clientes descargados para cada página.

Si solo utiliza una función en una página, puede incluir la clientlib completa de esa característica directamente en la página, por ejemplo:

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

En este caso, incluidos todos ellos y así los clientes SCF más básicos que son los clientes autores son preferibles:

* Nombre : **`embed`**
* Tipo : **`String`**
* Haga clic **`Multi`**
* Value: **`cq.social.scf`**

   * Aparecerá un cuadro de diálogo,
haga clic **`+`** después de cada entrada para agregar las siguientes categorías clientlib:

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * Haga clic en **Aceptar**

* Haga clic en **Guardar todo**

![scf-clientlibs](assets/scf-clientlibs.png)

Así es como `/etc/designs/an-scf-sandbox/clientlibs` debe aparecer ahora en el repositorio:

![scf-clientlibs-vista](assets/scf-clientlibs1.png)

### Incluir Clientlibs en la plantilla PlayPage {#include-clientlibs-in-playpage-template}

Sin incluir la categoría `apps.an-scf-sandbox` ClientLibraryFolder en la página, los componentes SCF no funcionarán ni se les aplicará estilo, ya que no estarán disponibles los JavaScript y los estilos necesarios.

Por ejemplo, sin incluir clientlibs, el componente de comentarios de SCF no tiene estilo:

![clientlibs-comment](assets/clientlibs-comment.png)

Una vez que se incluye apps.an-scf-sandbox clientlibs, el componente de comentarios de SCF aparece con estilo:

![clientlibs-comment-style](assets/clientlibs-comment1.png)

La sentencia include pertenece a la sección `head` de la secuencia de comandos `html`. El **`foundation head.jsp`** predeterminado incluye una secuencia de comandos que se puede superponer: **`headlibs.jsp`**.

**Copie headlibs.jsp e incluya clientlibs:**

1. Utilizando **CRXDE Lite**, seleccione **`/libs/foundation/components/page/headlibs.jsp`**

1. Haga clic con el botón derecho y seleccione **Copiar** (o seleccione Copiar en la barra de herramientas)
1. Seleccione **`/apps/an-scf-sandbox/components/playpage`**
1. Haga clic con el botón derecho y seleccione **Pegar** (o seleccione Pegar en la barra de herramientas)
1. Haga clic en doble **`headlibs.jsp`** para abrirlo
1. Anexe la línea siguiente al final del archivo
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

Cargue el sitio web en el navegador y vea si el fondo no es azul.

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![community-play](assets/community-play.png)

### Guardando su trabajo hasta ahora {#saving-your-work-so-far}

En este punto, existe un simulador para pruebas minimalista y puede que valga la pena guardarlo como paquete para que, mientras se reproduce, si el repositorio se daña y desea pasar el inicio, pueda desactivar el servidor, cambiar el nombre o eliminar la carpeta crx-quickstart/, activar el servidor, cargar e instalar este paquete guardado y no tener que repetir estos pasos más básicos.

Este paquete existe en el tutorial [Crear una página de muestra](/help/communities/create-sample-page.md) para aquellos que no pueden esperar para simplemente saltar y reproducir el inicio...

Para crear un paquete:

* En el CRXDE Lite, haga clic en el icono [Paquete](https://localhost:4502/crx/packmgr/)
* Haga clic en **Crear paquete**

   * Nombre del paquete: an-scf-sandbox-Minimum-pkg
   * Versión: 0,1
   * Agrupar: `leave as default`
   * Haga clic en **Aceptar**

* Haga clic en **Editar**

   * Seleccione la ficha **Filtros**

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

Ahora puede seleccionar **Descargar** para guardarlo en el disco y **Cargar paquete** en otra parte, así como seleccionar **Más > Replicar** para insertar el simulador de pruebas en una instancia de publicación localhost para expandir el dominio del simulador de pruebas.