---
title: Uso de comentarios
description: La función Comentarios permite a los visitantes del sitio iniciar sesión compartir sus opiniones y conocimientos
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 30baebd9-13c5-4fde-a494-85601abc32a5
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 1%

---

# Uso de comentarios {#using-comments}

## Introducción {#introduction}

La función de comentarios se utiliza para permitir que los visitantes (miembros) del sitio que hayan iniciado sesión compartan sus opiniones y conocimientos sobre el contenido del sitio. Esta función suele estar presente en otras funciones, pero se puede agregar a cualquier sitio web.

El documento describe:

* Agregando `Comments` a una página.
* Ajustes de configuración para `Comments` componente.

>[!NOTE]
>
>No se admite la publicación anónima de un comentario. Los visitantes del sitio deben registrarse (convertirse en miembros) e iniciar sesión para participar.

### Agregar comentarios a una página {#adding-comments-to-a-page}

Para agregar un `Comments` a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Comments`

y arrástrela a su lugar en una página, como una posición relativa a la función en la que los usuarios pueden realizar comentarios, o simplemente en la parte inferior de la página.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](/help/communities/basics.md).

Si la variable [bibliotecas requeridas del lado del cliente](/help/communities/essentials-comments.md#essentials-for-client-side) están incluidos, así es como se `Comments` aparece el componente.

![comments-component](assets/comments-component.png)

>[!NOTE]
>
>Solo uno `Comments` puede existir un componente en una página. Tenga en cuenta que varias funciones de Communities ya incluyen comentarios, como un blog, un calendario, un foro, un control de calidad y revisiones.

### Configuración de comentarios {#configuring-comments}

Seleccione el colocado `Comments` para acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![icono de configuración](assets/configure.png)

![comentariosconfiguración](assets/commentssettings.png)

#### Pestaña Comentarios {#comments-tab}

En el **Comentarios** , especifique cómo los visitantes introducen los comentarios.

* **Permitir respuestas**

  Si se selecciona esta opción, los miembros podrán responder a los comentarios existentes. La opción predeterminada no está seleccionada.

* **Comentarios por página**

  Limita el número de comentarios que se muestran por página y el número de respuestas que se muestran. El valor predeterminado es 10.

* **Permitir cargas de archivos**

  Si se selecciona, la opción para cargar un archivo se presenta con la casilla de entrada de texto. La opción predeterminada no está seleccionada.

* **Tamaño máximo de archivo**

  Solo es relevante si está marcada la opción Permitir cargas de archivos. Este valor limita el tamaño del archivo cargado. El límite predeterminado es 10 MB.

* **Longitud máxima del mensaje**

  Número máximo de caracteres que pueden introducirse en el cuadro de texto. El valor predeterminado es de 4096 caracteres.

* **Tipos de archivo permitidos**

  Solo es relevante si está marcada la opción Permitir cargas de archivos. Lista separada por comas de las extensiones de nombre de archivo con el separador de &quot;puntos&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permiten los que no se hayan especificado. El valor predeterminado no se ha especificado, de modo que se permiten todos los tipos de archivo.

* **Editor de texto enriquecido**

  Si se selecciona, los comentarios se introducen con marcado. La opción predeterminada no está seleccionada.

* **Permitir votación**

  Si se selecciona, la opción para votar hacia arriba o hacia abajo se presenta con el cuadro de entrada de texto. La opción predeterminada no está seleccionada.

* **Permitir seguimiento**

  Si se selecciona esta opción, se permite que los miembros sigan los comentarios. La opción predeterminada no está seleccionada.

* **Mostrar distintivos**

  Si se selecciona esta opción, se muestran las insignias obtenidas y concedidas. La opción predeterminada no está seleccionada.

#### Pestaña Moderación de usuario {#user-moderation-tab}

En el **Moderación de usuario** , especifique cómo se administran los comentarios publicados. Para obtener más información, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

* **Premoderación**

  Si se selecciona, los comentarios deben aprobarse antes de aparecer en un sitio de publicación. La opción predeterminada no está seleccionada.

* **Eliminar comentarios**

  Si se selecciona, el miembro que publicó el comentario tiene la capacidad de eliminarlo. La opción predeterminada no está seleccionada.

* **Denegar comentarios**

  Si se selecciona, permite que los moderadores denieguen comentarios. La opción predeterminada no está seleccionada.

* **Cerrar / volver a abrir comentarios**

  Si se selecciona esta opción, los moderadores pueden cerrar y volver a abrir los comentarios. La opción predeterminada no está seleccionada.

* **Marcar comentarios**

  Si se selecciona esta opción, se permite a los miembros marcar comentarios como inadecuados. La opción predeterminada no está seleccionada.

* **Lista de motivos de marca**

  Si se selecciona esta opción, permite a los miembros elegir, en una lista desplegable, el motivo por el que marcan un comentario como inapropiado. La opción predeterminada no está seleccionada.

* **Motivo de indicación personalizado**

  Si se selecciona esta opción, permite que los miembros especifiquen su propio motivo para marcar un comentario como inapropiado. La opción predeterminada no está seleccionada.

* **Umbral de moderación**

  Introduzca el número de veces que los miembros deben marcar un comentario antes de notificarlo a los moderadores. El valor predeterminado es una vez (1).

* **Límite de indicación**

  Introduzca el número de veces que se debe marcar un comentario antes de ocultarlo de la vista pública. Este número debe ser mayor o igual que **Umbral de moderación**. El valor predeterminado es 5.

#### Pestaña Configuración de ordenación {#sort-settings-tab}

En el **Configuración de orden** , especifique cómo se ordenan los comentarios publicados cuando se muestran.

* **Campo de ordenación**

  Tire hacia abajo para seleccionar una de `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`, o `Most Liked`.

* **Orden de clasificación**

  Tire hacia abajo para seleccionar una de `Ascending` o `Descending`.

### Cambio a un tipo de comentario personalizado {#changing-to-a-custom-comment-type}

Al cambiar el Tipo de recurso de comentario, el sistema de comentarios ya no genera una instancia de un comentario con el valor predeterminado, sino una que han personalizado (ampliado) los desarrolladores.

Una vez conocidos los tipos de recursos personalizados, escriba [Modo de diseño](/help/sites-authoring/default-components-designmode.md) y haga doble clic en el elemento colocado `Comments` para abrir un cuadro de diálogo con una pestaña adicional.

En el **Tipos de recursos** pestaña, especifique el resourceType personalizado para las nuevas instancias de la `Comments or Voting` componentes:

![resource-type](assets/resource-type.png)

* **Tipo de medio de comentario**

  Navegue hasta el resourceType de un `comment` componente (comentario único) en /apps. Por ejemplo, `/apps/social/commons/components/hbs/comments/comment`

  Este recurso identifica el resourceType del UGC creado cuando un visitante publica un comentario.

* **Tipo de medio de votación**

  Navegue hasta el resourceType de un `voting` en /apps. Por ejemplo, `/apps/social/components/hbs/voting`

  Este recurso identifica el tipo de recurso de UGC creado cuando un visitante publica un voto.

* **Tipo de medio de sistema de comentario**

  Navegue hasta el resourceType de un `comments`(Sistema de comentarios) en /apps. Dejar en blanco a menos que la plantilla de página [incluye dinámicamente](/help/communities/scf.md#add-or-include-a-communities-component) Utilice el sistema de comentarios en la secuencia de comandos subyacente en lugar de añadirse a la página como recurso (nodo de comentarios). Para obtener más información, lea la [`{{include}}` ayudante](/help/communities/handlebars-helpers.md#include).

### Experiencia del visitante del sitio {#site-visitor-experience}

#### Moderadores y administradores {#moderators-and-administrators}

Cuando el usuario que ha iniciado sesión tiene privilegios de moderador o administrador, puede realizar las tareas de moderación permitidas por la configuración del componente, independientemente de quién haya creado el comentario.

#### Miembros {#members}

Cuando el visitante del sitio inicia sesión, según la configuración, puede ser

* Publicar un nuevo comentario
* Editar su propio comentario
* Eliminar su propio comentario
* Marcar comentarios de otros usuarios

#### Anónimo {#anonymous}

Los visitantes del sitio que no hayan iniciado sesión solo pueden leer los comentarios publicados, traducirlos si se admiten, pero no pueden agregar un comentario ni marcar los comentarios de otros.

### Información adicional {#additional-information}

Puede encontrar más información en la [Comments Essentials](/help/communities/essentials-comments.md) para desarrolladores.

Para ver la moderación de los comentarios publicados, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para ver la traducción de los comentarios publicados, consulte [Traducción del contenido generado por el usuario](/help/communities/translate-ugc.md).
