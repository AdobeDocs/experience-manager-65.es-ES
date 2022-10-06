---
title: Guía de componentes de comunidad
seo-title: Community Components Guide
description: Una herramienta de desarrollo interactiva para empezar a utilizar el marco de componentes sociales (SCF)
seo-description: An interactive development tool to get started with the social component framework (SCF)
uuid: 120e56d1-b93c-4f92-bab4-6bb5e40e0ddf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a777a3f1-b39f-4d90-b9b6-02d3e321a86f
exl-id: 12c0eae5-fd76-4480-a012-25d3312f3570
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 2%

---

# Guía de componentes de comunidad  {#community-components-guide}

La guía de componentes de comunidad es una herramienta de desarrollo interactivo para [marco de componentes sociales (SCF)](scf.md). Proporciona una lista de los componentes de AEM Communities disponibles o de las funciones más complejas creadas a partir de varios componentes.

Junto con la información básica de cada componente, la guía permite experimentar con cómo funcionan los componentes y funciones de SCF y cómo se pueden configurar o personalizar.

Para obtener información sobre los aspectos básicos del desarrollo relacionados con cada componente, consulte [Elementos esenciales de funciones y componentes](essentials.md).

## Introducción {#getting-started}

La guía está diseñada para utilizarse en instalaciones de desarrollo de instancias de autor (localhost:4502) y publicación (localhost:4503).

Para acceder al sitio Componentes de la comunidad , vaya a

* [https://&lt;server>:&lt;port>/content/community-components/en.html](http://localhost:4502/content/community-components/en.html)

Las interacciones con los componentes de Communities variarán según:

* El servidor (autor o publicación).
* Indica si el visitante del sitio ha iniciado sesión o no.
* Si ha iniciado sesión, los privilegios asignados al miembro.
* Indica si el SRP predeterminado es o no, [JSRP](jsrp.md), está en uso.

Al crear, para entrar en el modo de edición, inserte una de las opciones siguientes: `editor.html` o `cf#` como el primer segmento de ruta después del nombre del servidor:

* IU estándar:

   [https://&lt;server>:&lt;port>/editor.html/content/community-components/en.html](http://localhost:4502/editor.html/content/community-components/en.html)

* IU clásica:

   [https://&lt;server>:&lt;port>/cf#/content/community-components/en.html](http://localhost:4502/cf#/content/community-components/en.html)

>[!NOTE]
>
>En el modo de edición de autor, los vínculos de una página no están activos.
>
>Para desplazarse a una página de componentes, seleccione primero el modo de vista previa para activar los vínculos.
>
>Con la página de componentes mostrada en el navegador, vuelva al modo de edición para abrir el cuadro de diálogo de edición del componente.
>
>Para obtener información general sobre la creación, consulte [guía rápida para la creación de páginas](../../help/sites-authoring/qg-page-authoring.md).
>
>Si no está familiarizado con AEM, consulte la documentación de [tratamiento básico](../../help/sites-authoring/basic-handling.md).

### Página principal {#home-page}

La guía proporciona una lista de los componentes de SCF disponibles para su previsualización y creación de prototipos en el lado izquierdo de la página.

Guía de componentes tal como se ve en una instancia de autor en el modo de edición:

![community-component1](assets/community-component1.png)

## Páginas de componentes {#component-pages}

Seleccione un componente de la lista a lo largo de la parte izquierda de la página.

![community-component-pages](assets/community-component2.png)

Se muestra el cuerpo principal de la guía:

1. Título: Nombre del componente seleccionado
1. [Bibliotecas del lado cliente](#client-side-libraries): Una lista de una o más categorías requeridas
1. [Incluible](scf.md#add-or-include-a-communities-component): Si el componente se puede incluir dinámicamente, se puede alternar el estado en el modo de edición de autor:

   * Si se agrega, el texto mostrado es: &quot;Este componente se incluye a través de su nodo par.&quot;
   * Si se incluye, el texto mostrado es: &quot;Este componente se incluye de forma dinámica.&quot;
   * Si no se puede incluir, no se muestra ningún texto

1. Componente o función de ejemplo: una instancia activa del componente o función. Si un componente es, puede modificarse con los cambios realizados en las plantillas, CSS y los datos proporcionados en la sección de la pestaña .

>[!NOTE]
>
>Después de realizar una selección desde el lado izquierdo, el componente aparecerá debajo, en lugar de al lado, la lista de componentes cuando la ventana del navegador sea demasiado estrecha.

### Interacciones de autor {#author-interactions}

Al utilizar la guía en una instancia de autor, es posible experimentar la configuración de un componente abriendo su cuadro de diálogo. La información para desarrolladores se proporciona en la sección [Componentes y funciones esenciales](essentials.md) de la documentación, mientras que la configuración del cuadro de diálogo se describe en [Componentes de Communities](author-communities.md) para autores.

Para la guía Componentes de comunidad , algunos ajustes del cuadro de diálogo de componentes se superponen con la variable [Incluible](scf.md#add-or-include-a-communities-component) alternar estado. Para alternar entre el uso del recurso existente o un recurso incluido dinámicamente, en el modo de edición seleccione el componente y el texto inclusible y haga doble clic para abrir el cuadro de diálogo de edición:

![community-component3](assets/community-component3.png)

En el **Plantillas** pestaña:

![community-component4](assets/community-component4.png)

* **Incluir el componente secundario con sling:include**

   Si no está marcada, la Guía de componentes utilizará el recurso existente en el repositorio (un nodo jcr que es un nodo secundario de un nodo par).

   * el texto mostrado es: &quot;Este componente se incluye a través de su nodo par.&quot;

   Si se selecciona, la Guía de componentes utilizará sling para incluir dinámicamente un componente del resourceType del nodo secundario (recurso no existente).

   * el texto mostrado es: &quot;Este componente se incluye de forma dinámica.&quot;

   El valor predeterminado no está seleccionado.

### Publicar interacciones {#publish-interactions}

Al utilizar la guía en una instancia de publicación, es posible experimentar los componentes y las funciones como visitante del sitio (sin sesión iniciada) y como miembros con varios privilegios cuando se inicia sesión.

>[!NOTE]
>
>Tenga en cuenta que si se deja el SRP, el valor predeterminado es [JSRP](jsrp.md), luego UGC introducido en la instancia de publicación solo será visible en la publicación, y *not* sea visible desde la variable [moderación](moderate-ugc.md) en la instancia de autor.

## Bibliotecas de cliente {#client-side-libraries}

Las bibliotecas del lado del cliente (clientlibs) enumeradas para cada componente son las siguientes *obligatorio* para hacer referencia a cuando el componente se coloca en una página. clientlibs proporciona un medio para administrar y optimizar la descarga de Javascript y CSS utilizados para renderizar el componente en el navegador.

Para obtener más información, visite [Clientlibs para componentes de Communities](clientlibs.md).

## Suplantación {#impersonation}

En la instancia de autor, donde uno de ellos suele haber iniciado sesión como administrador o desarrollador, para experimentar el componente que ha iniciado sesión como otro usuario, utilice el cuadro de texto situado a la izquierda del **[!UICONTROL Suplantar]** para escribir el nombre de usuario o seleccione en la lista desplegable y, a continuación, haga clic en el botón . Haga clic en Revertir para cerrar la sesión y finalizar la suplantación.

La instancia de publicación no necesita suplantar. Simplemente utilice el vínculo de inicio de sesión/cierre de sesión para suplantar a varios usuarios, como el [usuarios de demostración](tutorials.md#demo-users).

## Personalización {#customization}

Cuando está habilitado, cada componente SCF está disponible para crear prototipos de posibles personalizaciones mediante la modificación temporal de la plantilla, la CSS y los datos del componente.

### Activación de la personalización {#enabling-customization}

>[!NOTE]
>
>**Esta herramienta es de solo lectura**. Ninguna de las ediciones realizadas en plantillas, CSS o datos se guardan en el repositorio.

Para experimentar rápidamente con las personalizaciones, la variable `scg:showIde`La propiedad debe añadirse al nodo JCR de contenido de la página de componentes y establecerse en true.

Con el componente comentarios como ejemplo, en la instancia de autor o publicación, ha iniciado sesión con privilegios de administrador:

1. Vaya a [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)

   Por ejemplo, [http://localhost:4503/crx/de](http://localhost:4503/crx/de)

1. Seleccione el `jcr:content` node

   Por ejemplo, `/content/community-components/en/comments/jcr:content`. 

1. Agregar una propiedad

   * **Nombre** `scg:showIde`
   * **Tipo** `String`
   * **Valor** `true`

1. Select **[!UICONTROL Guardar todo]**
1. Vuelva a cargar la página Comentarios en la guía

   [http://localhost:4503/content/community-components/en/comments.html](http://localhost:4503/content/community-components/en/comments.html)

1. Tenga en cuenta que ahora hay 3 fichas para Plantillas, CSS y Datos.

![community-component5](assets/community-component5.png)

![community-component6](assets/community-component6.png)

### Ficha Plantillas {#templates-tab}

Seleccione la pestaña plantillas para ver las plantillas asociadas al componente.

El Editor de plantillas permite compilar ediciones locales y aplicarlas a la instancia de componente de muestra en la parte superior de la página sin afectar al componente en el repositorio.

Al ejecutar la compilación en ediciones locales, se resaltarán los errores colocando un punto en el guión y marcando el texto en rojo.

### Ficha CSS {#css-tab}

Seleccione la pestaña CSS para ver el CSS asociado al componente.

Si un componente es una composición de varios componentes, algunos CSS pueden aparecer en la lista de uno de los otros componentes.

El editor CSS permite modificar el CSS y aplicarlo a la instancia de componente de ejemplo en la parte superior de la página.

Se puede seleccionar una regla para resaltar las partes del DOM usando esa regla haciendo clic en al lado de la regla en el guión.

### Ficha Datos {#data-tab}

Seleccione la pestaña Data para mostrar los datos del extremo .social.json . Estos datos son editables y se aplican a la instancia de componente de ejemplo.

Los errores de sintaxis se pueden marcar en el guión y resaltarse en el editor.
