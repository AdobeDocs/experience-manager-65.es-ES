---
title: Agregar Clientlibs
seo-title: Agregar Clientlibs
description: Agregar una ClientLibraryFolder
seo-description: Agregar una ClientLibraryFolder
uuid: 2944923d-caca-4607-81a4-4122a2ce8e41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 46f81c3f-6512-43f1-8ec1-cc717ab6f6ff
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Agregar Clientlibs{#add-clientlibs}

## Agregar una ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Cree una ClientLibraryFolder con el nombre `clientlibs`que contendrá el JS y CSS utilizados para procesar las páginas del sitio.

El valor de `categories`propiedad proporcionado a esta biblioteca de cliente es el identificador utilizado para incluir directamente esta clientlib desde una página de contenido o para incrustarla en otros clientes.

1. con **CRXDE Lite**, expanda `/etc/designs`

1. haga clic con el botón derecho `an-scf-sandbox` y seleccione `Create Node`

   * Nombre : `clientlibs`
   * Tipo : `cq:ClientLibraryFolder`

1. click **OK**

![chlimage_1-47](assets/chlimage_1-47.png)

En la ficha **Propiedades** del nuevo `clientlibs` nodo, introduzca la propiedad **`categories`**:

* Nombre: **categorías**
* Tipo: **Cadena**
* Valor: **apps.an-scf-sandbox**
* click **Add**
* haga clic en **Guardar todo**

Nota: anteponer el valor de las categorías con &#39;aplicaciones&#39;. es una convención para identificar la &#39;aplicación propietaria&#39; como una carpeta /apps, no como /libs.  IMPORTANTE: Agregue los archivos `js.tx`t y**`css.tx`**t del marcador de posición. (No es oficialmente un cq:ClientLibraryFolder sin ellos).

1. clic derecho **`/etc/designs/an-scf-sandbox/clientlibs`**
1. seleccionar **Crear archivo...**
1. **escriba** Nombre: `css.txt`
1. seleccionar **Crear archivo...**
1. **escriba** Nombre: `js.txt`
1. haga clic en **Guardar todo**

![chlimage_1-48](assets/chlimage_1-48.png)

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

En la ficha **Propiedades** del `clientlibs` nodo, introduzca la propiedad String de varios valores **embed**. Esto incrusta las bibliotecas del lado del [cliente (clientlibs) necesarias para los componentes](/help/communities/client-customize.md#clientlibs-for-scf)SCF. Para este tutorial se añaden muchos de los clientlibs necesarios para los componentes Communities.

**Tenga en cuenta** que este puede ser o no el método deseado para usar en un sitio de producción, ya que existen consideraciones de conveniencia en comparación con el tamaño y la velocidad de los clientes descargados para cada página.

Si solo utiliza una función en una página, puede incluir la clientlib completa de esa característica directamente en la página, por ejemplo: &lt;% ui:includeClientLib categories=cq.social.hbs.forum&quot; %>

En este caso, incluidos todos ellos y así los clientes SCF más básicos que son los clientes autores son preferibles:

* Nombre : **`embed`**
* Tipo : **`String`**
* click **`Multi`**
* Valor: **`cq.social.scf`***&lt;enter> mostrará un cuadro de diálogo, haga clic **[+] **después de cada entrada para agregar las siguientes categorías de clientlib:*

   * **`cq.ckeditor`**
   * **`cq.social.author.hbs.comments`**
   * **`cq.social.author.hbs.forum`**
   * **`cq.social.author.hbs.rating`**
   * **`cq.social.author.hbs.reviews`**
   * **`cq.social.author.hbs.voting`**
   * click **OK**

* haga clic en **Guardar todo**

![chlimage_1-49](assets/chlimage_1-49.png)

Así es como `/etc/designs/an-scf-sandbox/clientlibs` debería aparecer ahora en el repositorio:

![chlimage_1-50](assets/chlimage_1-50.png)

### Incluir Clientlibs en la plantilla PlayPage {#include-clientlibs-in-playpage-template}

Sin incluir la categoría `apps.an-scf-sandbox` ClientLibraryFolder en la página, los componentes SCF no funcionarán ni se les aplicará estilo, ya que no estarán disponibles los JavaScript ni los estilos necesarios.

Por ejemplo, sin incluir clientlibs, el componente de comentarios de SCF no tiene estilo:

![chlimage_1-51](assets/chlimage_1-51.png)

Una vez que se incluye apps.an-scf-sandbox clientlibs, el componente de comentarios de SCF aparece con estilo:

![chlimage_1-52](assets/chlimage_1-52.png)

La instrucción include pertenece al <head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> de la sección <html> script. El valor predeterminado **`foundation head.jsp`** incluye una secuencia de comandos que se puede superponer: **`headlibs.jsp`**.

**Copie headlibs.jsp e incluya clientlibs:**

1. con **CRXDE Lite**, seleccione **`/libs/foundation/components/page/headlibs.jsp`**

1. haga clic con el botón derecho y seleccione **Copiar ** (o seleccione Copiar en la barra de herramientas)
1. select**`/apps/an-scf-sandbox/components/playpage`**
1. haga clic con el botón derecho y seleccione **Pegar ** (o seleccione Pegar en la barra de herramientas)
1. haga doble clic **`headlibs.jsp`** para abrirlo
1. anexe la línea siguiente al final del archivo
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. haga clic en **Guardar todo**

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

![chlimage_1-53](assets/chlimage_1-53.png)

### Guardar su trabajo hasta ahora {#saving-your-work-so-far}

En este punto, existe un simulador de pruebas minimalista y puede que valga la pena guardarlo como paquete para que, mientras se reproduce, si el repositorio se daña y desea volver a empezar, puede desactivar el servidor, cambiar el nombre o eliminar la carpeta crx-quickstart/, activar el servidor, cargar e instalar este paquete guardado y no tener que repetir estos pasos más básicos.

Este paquete existe en el tutorial [Crear una página](/help/communities/create-sample-page.md) de muestra para aquellos que no pueden esperar para simplemente saltar y empezar a reproducir...

Para crear un paquete:

* en CRXDE Lite, haga clic en el icono [Paquete](https://localhost:4502/crx/packmgr/)
* haga clic en **Crear paquete**

   * Nombre del paquete: an-scf-sandbox-Minimum-pkg
   * Versión: 0,1
   * Grupo: &lt;dejar como predeterminado>
   * click **OK**

* click **Edit**

   * seleccionar **Filtros **ficha

      * haga clic en **Agregar filtro**
      * Ruta raíz: &lt;examinar a** /apps/an-scf-sandbox**>
      * haga clic en **Finalizado**
      * haga clic en **Agregar filtro**
      * Ruta raíz: &lt;examinar **/etc/designs/an-scf-sandbox**>
      * haga clic en **Finalizado**
      * haga clic en **Agregar filtro**
      * Ruta raíz: &lt;examinar **/content/an-scf-sandbox**>
      * haga clic en **Finalizado**
   * click **Save**


* haga clic en **Generar**

Ahora puede seleccionar **Descargar** para guardarlo en el disco y **Cargar paquete** en otra parte, así como seleccionar **Más > Replicar** para insertar el simulador de pruebas en una instancia de publicación local host para expandir el dominio del simulador de pruebas.