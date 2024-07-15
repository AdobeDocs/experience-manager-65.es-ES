---
title: Guía de componentes de la comunidad
description: Una herramienta de desarrollo interactiva para empezar a usar el marco de componente social (SCF)
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 12c0eae5-fd76-4480-a012-25d3312f3570
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 0%

---

# Guía de componentes de la comunidad  {#community-components-guide}

La guía de componentes de la comunidad es una herramienta de desarrollo interactiva para el [marco de trabajo de componentes sociales (SCF)](scf.md). Proporciona una lista de los componentes de comunidades de Adobe Experience Manager AEM () disponibles o las funciones más complejas creadas de varios componentes.

Junto con la información básica de cada componente, la guía permite experimentar cómo funcionan los componentes o funciones de SCF y cómo se pueden configurar o personalizar.

Para obtener información acerca de los aspectos básicos de desarrollo relacionados con cada componente, vea [Aspectos básicos de las características y los componentes](essentials.md).

## Introducción {#getting-started}

La guía está diseñada para utilizarse en instalaciones de desarrollo de instancias de autor (localhost:4502) e instancias de publicación (localhost:4503).

Para acceder al sitio de componentes de la comunidad, vaya a

* [https://&lt;server>:&lt;port>/content/community-components/en.html](http://localhost:4502/content/community-components/en.html)

Las interacciones con los componentes de las comunidades varían en función de:

* El servidor (autor o publicación).
* Si el visitante del sitio ha iniciado sesión o no.
* Si ha iniciado sesión, los privilegios asignados al miembro.
* Indica si el SRP predeterminado [JSRP](jsrp.md) está en uso.

En Autor, para entrar al modo de edición, inserte `editor.html` o `cf#` como el primer segmento de ruta de acceso después del nombre del servidor:

* IU estándar:

  [https://&lt;server>:&lt;port>/editor.html/content/community-components/en.html](http://localhost:4502/editor.html/content/community-components/en.html)

* IU clásica:

  [https://&lt;server>:&lt;port>/cf#/content/community-components/en.html](http://localhost:4502/cf#/content/community-components/en.html)

>[!NOTE]
>
>En el modo Autor y en el modo Edición, los vínculos de una página no están activos.
>
>Para navegar a una página de componente, seleccione primero el modo Vista previa para activar los vínculos.
>
>Con la página del componente mostrada en el explorador, vuelva al modo Editar para abrir el cuadro de diálogo de edición del componente.
>
>Para obtener información general sobre la creación, consulte la [guía rápida para la creación de páginas](../../help/sites-authoring/qg-page-authoring.md).
>
>AEM Si no está familiarizado con el uso de la, consulte la documentación sobre [gestión básica](../../help/sites-authoring/basic-handling.md).

### Página principal {#home-page}

La guía proporciona una lista de los componentes de SCF disponibles para la vista previa y la creación de prototipos en la parte izquierda de la página.

Guía de componentes tal y como se ve en una instancia de autor en el modo de edición:

![community-component1](assets/community-component1.png)

## Páginas de componentes {#component-pages}

Seleccione un componente de la lista que aparece en la parte izquierda de la página.

![community-component-pages](assets/community-component2.png)

Se muestra el cuerpo principal de la guía:

1. Título: nombre del componente seleccionado
1. [Bibliotecas de cliente](#client-side-libraries): Una lista de una o más categorías requeridas
1. [Incluible](scf.md#add-or-include-a-communities-component): si el componente se puede incluir dinámicamente, el estado se puede alternar en el modo de edición de autor:

   * Si se añade, el texto que se muestra es: &quot;Este componente se incluye a través de su nodo de par&quot;.
   * Si se incluye, el texto que se muestra es: &quot;Este componente se incluye dinámicamente&quot;.
   * Si no se puede incluir, no se muestra ningún texto

1. Componente o función de muestra: una instancia activa del componente o función. Si es un componente, puede modificarse con los cambios realizados en las plantillas, CSS y datos proporcionados en la sección de la pestaña.

>[!NOTE]
>
>Después de realizar una selección desde el lado izquierdo, el componente aparecerá debajo, en lugar de junto, a la lista de componentes cuando la ventana del explorador sea demasiado estrecha.

### Interacciones de autor {#author-interactions}

Al utilizar la guía en una instancia de autor, es posible experimentar la configuración de un componente al abrir su cuadro de diálogo. La información para los desarrolladores se proporciona en la sección [Componentes y características esenciales](essentials.md) de la documentación, mientras que la configuración del cuadro de diálogo se describe en la sección [Componentes de comunidades](author-communities.md) para autores.

Para la guía Componentes de la comunidad, algunos ajustes del cuadro de diálogo de componentes se superponen al estado de alternancia [Incluible](scf.md#add-or-include-a-communities-component). Para alternar entre el uso del recurso existente o un recurso incluido dinámicamente, en el modo de edición, seleccione el componente y el texto que se puede incluir y haga doble clic para abrir el cuadro de diálogo de edición:

![community-component3](assets/community-component3.png)

En la ficha **Plantillas**:

![community-component4](assets/community-component4.png)

* **Incluir el componente secundario con sling:include**

  Si no se selecciona, la Guía de componentes utiliza el recurso existente en el repositorio (un nodo jcr que es secundario de un nodo par).

   * El texto mostrado es: &quot;Este componente se incluye a través de su nodo de par&quot;.

  Si se selecciona, la Guía de componentes utiliza sling para incluir dinámicamente un componente del resourceType del nodo secundario (recurso no existente).

   * El texto mostrado es: &quot;Este componente se incluye dinámicamente&quot;.

  El valor predeterminado está desmarcado.

### Interacciones de Publish {#publish-interactions}

Al utilizar la guía en una instancia de publicación, es posible experimentar los componentes y las funciones como un visitante del sitio (sin iniciar sesión) y como miembros con varios privilegios al iniciar sesión.

>[!NOTE]
>
>Tenga en cuenta que si el SRP se deja en [JSRP](jsrp.md) de forma predeterminada, entonces el UGC introducido en la instancia de publicación solo estará visible en la publicación, y *no* estará visible desde la consola [moderación](moderate-ugc.md) en la instancia de autor.

## Bibliotecas del cliente {#client-side-libraries}

Las bibliotecas del lado del cliente (clientlibs) enumeradas para cada componente son las *necesarias* a las que se hace referencia cuando el componente se coloca en una página. Los clientlibs proporcionan un medio para administrar y optimizar la descarga de JavaScript y CSS utilizados para procesar el componente en el explorador.

Para obtener más información, visite [Clientlibs for Communities Components](clientlibs.md).

## Suplantación {#impersonation}

En la instancia de autor, donde a menudo se inicia sesión como administrador o desarrollador, para experimentar cómo ha iniciado sesión el componente como otro usuario, utilice el cuadro de texto a la izquierda del botón **[!UICONTROL Suplantar]** para escribir el nombre de usuario o seleccionar en la lista desplegable y, a continuación, haga clic en el botón. Haga clic en Revertir para cerrar la sesión y finalizar la suplantación.

La instancia de publicación no necesita suplantar. Solo tiene que usar el enlace Iniciar/Cerrar sesión para suplantar a varios usuarios, como los [usuarios de demostración](tutorials.md#demo-users).

## Personalización {#customization}

Cuando se habilita, cada componente SCF está disponible para crear prototipos de posibles personalizaciones mediante la modificación temporal de la plantilla, CSS y datos del componente.

### Habilitar la personalización {#enabling-customization}

>[!NOTE]
>
>**Esta herramienta es de sólo lectura**. Ninguna de las ediciones realizadas en plantillas, CSS o datos se guarda en el repositorio.

Para experimentar rápidamente con las personalizaciones, se debe agregar la propiedad `scg:showIde` al nodo JCR de contenido de la página de componente y establecerla en true.

Con el componente Comentarios como ejemplo, en la instancia de autor o publicación, ha iniciado sesión con privilegios de administrador:

1. Buscar [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)

   Por ejemplo, [http://localhost:4503/crx/de](http://localhost:4503/crx/de)

1. Seleccione el nodo `jcr:content` del componente

   Por ejemplo, `/content/community-components/en/comments/jcr:content`

1. Añadir una propiedad

   * **Nombre** `scg:showIde`
   * **Tipo** `String`
   * **Valor** `true`

1. Seleccionar **[!UICONTROL Guardar todo]**
1. Vuelva a cargar la página Comentarios en la guía

   [http://localhost:4503/content/community-components/en/comments.html](http://localhost:4503/content/community-components/en/comments.html)

1. Tenga en cuenta que ahora hay tres pestañas para plantillas, CSS y datos.

![community-component5](assets/community-component5.png)

![community-component6](assets/community-component6.png)

### Pestaña Plantillas {#templates-tab}

Seleccione la pestaña plantillas para ver las plantillas asociadas al componente.

El Editor de plantillas permite compilar las ediciones locales y aplicarlas a la instancia del componente de muestra en la parte superior de la página sin afectar al componente en el repositorio.

La ejecución de compilaciones en ediciones locales resaltará los errores colocando un punto en el margen interno y marcando el texto en rojo.

### Pestaña CSS {#css-tab}

Seleccione la pestaña CSS para ver el CSS asociado al componente.

Si un componente está compuesto por varios componentes, parte del CSS puede aparecer enumerado en uno de los demás componentes.

El editor CSS permite modificar el CSS y aplicarlo a la instancia del componente de ejemplo en la parte superior de la página.

Se puede seleccionar una regla para resaltar las partes del DOM que utilizan esa regla haciendo clic en junto a la regla en el margen.

### Pestaña Datos {#data-tab}

Seleccione la pestaña Datos para mostrar los datos del extremo .social.json. Estos datos son editables y se aplican a la instancia de componente de ejemplo.

Los errores de sintaxis se pueden marcar en el margen interno y resaltar en el editor.
