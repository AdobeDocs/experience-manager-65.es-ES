---
title: Uso de comentarios
seo-title: Uso de comentarios
description: La función Comentarios permite a los visitantes del sitio que inician sesión compartir sus opiniones y conocimientos
seo-description: La función Comentarios permite a los visitantes del sitio que inician sesión compartir sus opiniones y conocimientos
uuid: 40acd962-846c-483c-b789-aab3a7d2b31b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 216cfb3e-777e-4773-afba-749debdca000
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Uso de comentarios{#using-comments}

## Introducción {#introduction}

La función de comentarios se utiliza para permitir que los visitantes (miembros) del sitio que inician sesión compartan sus opiniones y conocimientos sobre el contenido del sitio. Esta función suele estar presente en otras funciones, pero puede agregarse a cualquier sitio web.

El documento describe:

* agregar `Comments`a una página.
* configuración del `Comments`componente.

>[!NOTE]
>
>No se admite la publicación anónima de un comentario. Los visitantes del sitio deben registrarse (convertirse en miembros) e iniciar sesión para participar.

### Adición de comentarios a una página {#adding-comments-to-a-page}

Para agregar un `Comments`componente a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Comments`

y arrástrelo a su lugar en una página, como una posición relativa a la función en la que los usuarios pueden comentar o simplemente en la parte inferior de la página.

Para obtener la información necesaria, visite [Communities Components Basics](/help/communities/basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se incluyen las bibliotecas [del lado del cliente](/help/communities/essentials-comments.md#essentials-for-client-side) necesarias, es así como aparece el `Comments`componente.

![chlimage_1-143](assets/chlimage_1-143.png)

>[!NOTE]
>
>Solo puede existir un `Comments`componente en una página. Tenga en cuenta que varias funciones de Comunidades ya incluyen comentarios, como un blog, calendario, foro, control de calidad y reseñas.

### Configuración de comentarios {#configuring-comments}

Seleccione el componente colocado al que desea acceder y seleccione el `Comments` `Configure` icono que abre el cuadro de diálogo de edición.

![configuración de](assets/configure.png) comentarios de icono ![](assets/commentssettings.png)

#### Ficha Comentarios {#comments-tab}

En la ficha **Comentarios** , especifique cómo los visitantes introducen los comentarios.

* **Permitir respuestas**

   Si se selecciona, permite que los miembros respondan a los comentarios existentes. El valor predeterminado no está seleccionado.

* **Comentarios por página**

   Limita el número de comentarios mostrados por página y el número de respuestas mostradas. El valor predeterminado es 10.

* **Permitir cargas de archivos**

   Si se selecciona, la opción para cargar un archivo se muestra con el cuadro de entrada de texto. El valor predeterminado no está seleccionado.

* **Tamaño máximo de archivo**

   Solo es relevante si está activada la opción Permitir cargas de archivos. Este valor limita el tamaño del archivo cargado. El límite predeterminado es 10 MB.

* **Longitud máxima del mensaje**

   Número máximo de caracteres que se pueden introducir en el cuadro de texto. El valor predeterminado es de 4096 caracteres.

* **Tipos de archivo permitidos**

   Solo es relevante si está activada la opción Permitir cargas de archivos. Una lista separada por comas de extensiones de nombre de archivo con el separador &quot;punto&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permiten los no especificados. El valor predeterminado no es ninguno, por lo que se permiten** **todos los tipos de archivo.

* **Editor de texto enriquecido**

   Si se selecciona, los comentarios se introducen con marcado. El valor predeterminado no está seleccionado.

* **Habilitar la votación**

   Si se selecciona, la opción para votar hacia arriba o hacia abajo se muestra con el cuadro de entrada de texto. El valor predeterminado no está seleccionado.

* **Permitir seguimiento**

   Si está activada, permita que los miembros sigan los comentarios. El valor predeterminado no está seleccionado.

* **Mostrar insignias**

   Si se selecciona, permita que se muestren las insignias ganadas y concedidas. El valor predeterminado no está seleccionado.

#### Ficha Moderación del usuario {#user-moderation-tab}

En la ficha **Moderación del usuario **, especifique cómo se administran los comentarios publicados. Para obtener más información, consulte [Moderación del contenido](/help/communities/moderate-ugc.md)generado por el usuario.

* **Premoderación** Si está activada, los comentarios deben aprobarse antes de que aparezcan en un sitio de publicación. El valor predeterminado no está seleccionado.

* **Eliminar comentarios**

   Si se selecciona, se proporciona al miembro que publicó el comentario la capacidad de eliminarlo. El valor predeterminado no está seleccionado.

* **Denegar comentarios**

   Si se selecciona, permita que los moderadores rechacen los comentarios. El valor predeterminado no está seleccionado.

* **Cerrar/abrir de nuevo los comentarios**

   Si se selecciona, permita que los moderadores cierren y vuelvan a abrir los comentarios. El valor predeterminado no está seleccionado.

* **Marcar comentarios**

   Si se selecciona, permita que los miembros marquen los comentarios como inapropiados. El valor predeterminado no está seleccionado.

* **Lista de motivos de indicación**

   Si se selecciona, permita que los miembros elijan, en una lista desplegable, el motivo por el que marcan un comentario como inapropiado. El valor predeterminado no está seleccionado.

* **Motivo de indicación personalizado**

   Si se selecciona, permita que los miembros especifiquen su propio motivo para marcar un comentario como inapropiado. El valor predeterminado no está seleccionado.

* **Umbral de moderación**

   Escriba el número de veces que los miembros deben marcar un comentario antes de que se notifique a los moderadores. El valor predeterminado es una vez (1).

* **Límite de indicación**

   Introduzca el número de veces que se debe marcar un comentario antes de ocultarlo en la vista pública. Este número debe ser mayor o igual que el umbral **de moderación**. El valor predeterminado es 5.

#### Ficha Ordenar configuración {#sort-settings-tab}

En la ficha **Ordenar configuración **, especifique cómo se ordenan los comentarios publicados cuando se muestran.

* **Campo de ordenación**

   Despliegue para seleccionar uno de `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`o `Most Liked`.

* **Orden**

   Despliegue para seleccionar uno de `Ascending` o `Descending`.

### Cambio a un tipo de comentario personalizado {#changing-to-a-custom-comment-type}

Al cambiar el tipo de recurso de comentario, el sistema de comentarios ya no genera una instancia de un comentario usando el valor predeterminado, sino una instancia personalizada (ampliada) por los desarrolladores.

Una vez conocidos los tipos de recursos personalizados, introduzca el modo [de](/help/sites-authoring/default-components-designmode.md) diseño y haga doble clic en el componente `Comments` colocado para abrir un cuadro de diálogo con una ficha adicional.

En la ficha **Tipos de recursos **, especifique el resourceType personalizado para las nuevas instancias de los `Comments or Voting`componentes:

![chlimage_1-144](assets/chlimage_1-144.png)

* **Tipo de medio de comentario**

   Vaya al resourceType de un `comment`componente extendido (un solo comentario) en /apps. Por ejemplo, `/apps/social/commons/components/hbs/comments/comment`

   Este recurso identifica el resourceType del UGC creado cuando un visitante publica un comentario.

* **Tipo de medio de votación**

   Vaya al resourceType de un `voting`componente extendido en /apps. Por ejemplo, `/apps/social/components/hbs/voting`

   Este recurso identifica el tipo de recurso del UGC creado cuando un visitante publica una votación.

* **Tipo de recurso del sistema de comentarios**

   Vaya al resourceType de un `comments`componente extendido (sistema de comentarios) en /apps. Deje en blanco a menos que la plantilla de página incluya [](/help/communities/scf.md#add-or-include-a-communities-component) dinámicamente el sistema de comentarios en la secuencia de comandos subyacente en lugar de agregarlo a la página como recurso (nodo de comentarios). Obtenga más información leyendo sobre el asistente [{{include}}](/help/communities/handlebars-helpers.md#include).

### Experiencia del visitante del sitio {#site-visitor-experience}

#### Moderadores y administradores {#moderators-and-administrators}

Cuando el usuario que ha iniciado sesión tiene privilegios de moderador o administrador, puede realizar las tareas de moderación permitidas por la configuración del componente, independientemente de quién haya creado el comentario.

#### Miembros {#members}

Cuando el visitante del sitio ha iniciado sesión, según la configuración, es posible que

* publicar un nuevo comentario
* editar sus propios comentarios
* eliminar su propio comentario
* marcar los comentarios de otros

#### Anónimo {#anonymous}

Los visitantes del sitio que no hayan iniciado sesión solo podrán leer los comentarios publicados, traducirlos si son compatibles, pero no podrán agregar comentarios ni marcar los comentarios de otros.

### Información adicional {#additional-information}

Puede encontrar más información en la página [Comentarios esenciales](/help/communities/essentials-comments.md) para desarrolladores.

Para moderar los comentarios publicados, consulte [Moderación del contenido](/help/communities/moderate-ugc.md)generado por el usuario.

Para ver la traducción de los comentarios publicados, consulte [Traducción de contenido](/help/communities/translate-ugc.md)generado por el usuario.
