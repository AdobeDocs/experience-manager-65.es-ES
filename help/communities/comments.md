---
title: Uso de comentarios
seo-title: Using Comments
description: La función Comentarios permite que los visitantes del sitio que inician sesión compartan sus opiniones y conocimientos
seo-description: Comments feature lets signed-in site visitors share their opinions and knowledge
uuid: 40acd962-846c-483c-b789-aab3a7d2b31b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 216cfb3e-777e-4773-afba-749debdca000
docset: aem65
exl-id: 30baebd9-13c5-4fde-a494-85601abc32a5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 6%

---

# Uso de comentarios {#using-comments}

## Introducción {#introduction}

La función de comentarios se utiliza para permitir que los visitantes del sitio que inician sesión (los miembros) compartan sus opiniones y conocimientos sobre el contenido del sitio. Esta función suele estar presente en otras funciones, pero puede agregarse a cualquier sitio web.

El documento describe:

* Adición `Comments` a una página.
* Ajustes de configuración para `Comments` componente.

>[!NOTE]
>
>No se admite la publicación anónima de un comentario. Los visitantes del sitio deben registrarse (convertirse en miembros) e iniciar sesión para participar.

### Adición de comentarios a una página {#adding-comments-to-a-page}

Para agregar un `Comments` a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Comments`

y arrástrela a su lugar en una página, como una posición relativa a la función en la que los usuarios pueden hacer comentarios o simplemente en la parte inferior de la página.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de Communities](/help/communities/basics.md).

Cuando la variable [bibliotecas requeridas del lado del cliente](/help/communities/essentials-comments.md#essentials-for-client-side) se incluyen, así es como se muestra la variable `Comments` aparece.

![comments-component](assets/comments-component.png)

>[!NOTE]
>
>Solo una `Comments` puede existir en una página. Tenga en cuenta que varias funciones de Communities ya incluyen comentarios, como un blog, calendario, foro, control de calidad y reseñas.

### Configuración de comentarios {#configuring-comments}

Seleccione la colocación `Comments` para acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![icono de configuración](assets/configure.png)

![configuración de comentarios](assets/commentssettings.png)

#### Ficha Comentarios {#comments-tab}

En el **Comentarios** especifique cómo los visitantes introducen los comentarios.

* **Permitir respuestas**

   Si se selecciona, permite que los miembros respondan a los comentarios existentes. El valor predeterminado no está seleccionado.

* **Comentarios por página**

   Limita el número de comentarios mostrados por página y el número de respuestas mostradas. El valor predeterminado es 10.

* **Permitir cargas de archivos**

   Si se selecciona, la opción para cargar un archivo se muestra con el cuadro de entrada de texto. El valor predeterminado no está seleccionado.

* **Tamaño máximo de archivo**

   Solo es relevante si está marcada la opción Permitir cargas de archivos . Este valor limita el tamaño del archivo cargado. El límite predeterminado es 10 MB.

* **Longitud máxima del mensaje**

   Número máximo de caracteres que se pueden introducir en el cuadro de texto. El valor predeterminado es de 4096 caracteres.

* **Tipos de archivo permitidos**

   Solo es relevante si está marcada la opción Permitir cargas de archivos . Lista de extensiones de nombre de archivo separadas por coma con el separador &quot;punto&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permiten los no especificados. El valor predeterminado no se especifica de forma que se permitan todos los tipos de archivo.

* **Editor de texto enriquecido**

   Si se selecciona, los comentarios se introducen con marcado. El valor predeterminado no está seleccionado.

* **Habilitar la votación**

   Si se selecciona, la opción para votar hacia arriba o hacia abajo aparece con el cuadro de entrada de texto. El valor predeterminado no está seleccionado.

* **Permitir seguimiento**

   Si está activada, permita que los miembros sigan los comentarios. El valor predeterminado no está seleccionado.

* **Mostrar insignias**

   Si está marcada esta opción, permita que se muestren los distintivos obtenidos y concedidos. El valor predeterminado no está seleccionado.

#### Pestaña Moderación del usuario {#user-moderation-tab}

En el **Moderación del usuario** especifique cómo se administran los comentarios publicados. Para obtener más información, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

* **Moderación previa**

   Si está activada, los comentarios deben aprobarse antes de que aparezcan en un sitio de publicación. El valor predeterminado no está seleccionado.

* **Eliminar comentarios**

   Si se selecciona, el miembro que publicó el comentario tiene la capacidad de eliminarlo. El valor predeterminado no está seleccionado.

* **Denegar comentarios**

   Si está activada, permita que los moderadores rechacen los comentarios. El valor predeterminado no está seleccionado.

* **Cerrar/abrir de nuevo los comentarios**

   Si está marcada esta opción, permita que los moderadores cierren y vuelvan a abrir comentarios. El valor predeterminado no está seleccionado.

* **Marcar comentarios**

   Si se selecciona, permita a los miembros marcar los comentarios como inapropiados. El valor predeterminado no está seleccionado.

* **Lista de motivos de indicación**

   Si está marcada esta opción, permita que los miembros elijan, desde una lista desplegable, el motivo por el que marcan un comentario como inapropiado. El valor predeterminado no está seleccionado.

* **Motivo de indicación personalizado**

   Si está activada, permita que los miembros indiquen sus propios motivos para marcar un comentario como inapropiado. El valor predeterminado no está seleccionado.

* **Umbral de moderación**

   Introduzca el número de veces que los miembros deben marcar un comentario antes de que se notifique a los moderadores. El valor predeterminado es una sola vez (1).

* **Límite de indicación**

   Introduzca el número de veces que se debe marcar un comentario antes de ocultarlo de la vista pública. Este número debe ser bueno o igual que la variable **Umbral de moderación**. El valor predeterminado es 5.

#### Ficha Ordenar configuración {#sort-settings-tab}

En el **Configuración de ordenación** , especifique cómo se ordenan los comentarios publicados cuando se muestran.

* **Campo de ordenación**

   Desplegable para seleccionar uno de `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`o `Most Liked`.

* **Orden**

   Desplegable para seleccionar uno de `Ascending` o `Descending`.

### Cambio a un tipo de comentario personalizado {#changing-to-a-custom-comment-type}

Al cambiar el Tipo de recurso de comentario, el sistema de comentarios ya no genera una instancia de un comentario con el valor predeterminado, sino una que los desarrolladores han personalizado (ampliado).

Una vez conocidos los tipos de recursos personalizados, introduzca [Modo de diseño](/help/sites-authoring/default-components-designmode.md) y haga doble clic en la `Comments` para abrir un cuadro de diálogo con una pestaña adicional.

En el **Tipos de recurso** especifique el resourceType personalizado para nuevas instancias de la pestaña `Comments or Voting` componentes:

![resource-type](assets/resource-type.png)

* **Tipo de medio de comentario**

   Vaya al resourceType de una extensión `comment` en /apps. Por ejemplo, `/apps/social/commons/components/hbs/comments/comment`. 

   Este recurso identifica el resourceType del UGC creado cuando un visitante publica un comentario.

* **Tipo de medio de votación**

   Vaya al resourceType de una extensión `voting` en /apps. Por ejemplo, `/apps/social/components/hbs/voting`. 

   Este recurso identifica el tipo de recurso del UGC creado cuando un visitante publica una votación.

* **Tipo de recurso del sistema de comentarios**

   Vaya al resourceType de una extensión `comments`(sistema de comentarios) en /apps. Dejar en blanco a menos que la plantilla de página [incluye dinámicamente](/help/communities/scf.md#add-or-include-a-communities-component) el sistema de comentarios en la secuencia de comandos subyacente en lugar de agregarse a la página como recurso (nodo comentarios). Para obtener más información, consulte [{{include}} helper](/help/communities/handlebars-helpers.md#include).

### Experiencia del visitante del sitio {#site-visitor-experience}

#### Moderadores y administradores {#moderators-and-administrators}

Cuando el usuario que ha iniciado sesión tiene privilegios de moderador o administrador, puede realizar las tareas de moderación permitidas por la configuración del componente, independientemente de quién haya creado el comentario.

#### Miembros {#members}

Cuando el visitante del sitio ha iniciado sesión, según la configuración, es posible que

* Publicar un comentario nuevo
* Editar su propio comentario
* Eliminar su propio comentario
* Marcar comentarios de otros

#### Anónimo {#anonymous}

Los visitantes del sitio que no hayan iniciado sesión solo podrán leer los comentarios publicados, traducirlos si son compatibles, pero no pueden agregar un comentario ni marcar los comentarios de otros.

### Información adicional {#additional-information}

Puede encontrar más información en la [Comentarios esenciales](/help/communities/essentials-comments.md) para desarrolladores.

Para moderar los comentarios publicados, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para ver la traducción de los comentarios publicados, consulte [Traducción del contenido generado por el usuario](/help/communities/translate-ugc.md).
