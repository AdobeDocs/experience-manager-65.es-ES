---
title: Función de blog
seo-title: Función de blog
description: Información de la comunidad en formato de diario
seo-description: Información de la comunidad en formato de diario
uuid: 7323063f-81e8-45c3-9035-bf7df6124830
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: cf8b3d72-30ba-40ca-ae48-b61abbb28802
docset: aem65
translation-type: tm+mt
source-git-commit: 272eedc1585dbdea315b49d010e4b1d78cedc360

---


# Función de blog {#blog-feature}

## Introducción {#introduction}

La función de blog de Comunidades AEM ha pasado de ser una actividad de creación a una auténtica actividad comunitaria que tiene lugar en el entorno de publicación.

La función de blog permite proporcionar información de la comunidad en formato de diario. Los miembros autorizados (usuarios registrados y con sesión iniciada) realizan entradas de blog en el entorno de publicación.

La función de blog provee :

* Creación de artículos y comentarios de blog en el lado de la publicación
* Edición de texto enriquecido
* Imágenes en línea (con compatibilidad para arrastrar y soltar)
* Contenido incrustado de redes sociales (compatibilidad con[oEmbed](/help/communities/blog-developer-basics.md#allowing-rich-media))
* Modo de borrador
* Publicación programada
* Redactar en nombre (un miembro [](/help/communities/users.md#privileged-members-group) privilegiado puede crear contenido en nombre de otro miembro de la comunidad)
* [Moderación](/help/communities/moderate-ugc.md) masiva y en contexto de artículos y comentarios de blog

Esta sección de la documentación describe:

* Adición de la función de blog a un sitio de AEM
* Configuración de los componentes del blog

>[!NOTE]
>
>Los componentes `Journal`y `Journal Sidebar` se titulan `Blog` y `Blog Sidebar`.
>
>La función de blog que se encuentra en AEM 6.0 y versiones anteriores ahora se ha eliminado. Se basaba en una plantilla y solo permitía a los autores crear contenido en el entorno de creación.

## Adición de componentes de blog a una página {#adding-blog-components-to-a-page}

Si desea agregar un blog a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Blog`
* `Communities / Blog Sidebar`

y arrástrelos a su lugar en una página donde debería aparecer el blog.

Para obtener la información necesaria, visite [Communities Components Basics](/help/communities/basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se incluyen las bibliotecas [del lado del cliente](/help/communities/blog-developer-basics.md#essentials-for-client-side) necesarias, así es como aparecerá el `Blog`componente:

![chlimage_1-229](assets/chlimage_1-229.png)

Y cómo aparecerá el `Blog Sidebar` :

![chlimage_1-230](assets/chlimage_1-230.png)

### Configuración del blog {#configuring-blog}

Seleccione el componente colocado al que desea acceder y seleccione el `Blog` `Configure` icono que abre el cuadro de diálogo de edición.

![chlimage_1-231](assets/chlimage_1-231.png) Configuración ![de blog](assets/blog-configure.png)

#### Ficha Configuración {#settings-tab}

En la ficha **Configuración** , especifique las características básicas del blog:

* **Permitir la miniatura del archivo adjunto**

   Si se selecciona, se crea una miniatura de la imagen adjunta.

* **Tamaño máximo de la miniatura del archivo adjunto**

   Tamaño máximo (en píxeles) de la imagen en miniatura del archivo adjunto. El valor predeterminado es 800 x 800.

* **Tamaño mínimo de la imagen de la miniatura**

   Tamaño mínimo (en bytes) de la imagen para generar una miniatura para las imágenes en línea. El valor predeterminado es 100000 bytes (100 kb).

* **Tamaño máximo de la miniatura**

   Tamaño máximo (en píxeles) de la imagen en miniatura para la imagen en línea. El valor predeterminado es 800 x 800.

* **Permitir miembros privilegiados**

   Si se selecciona, solo los miembros con privilegios pueden crear contenido.

* **Miembros privilegiados permitidos**

   Agregue los miembros privilegiados con permiso para crear contenido.

* **Bloquee el contenido que haya creado el usuario en el modo de edición de autor**

   Si está activada, bloquea el contenido generado por el usuario mientras edita en modo de autor.

* **Título del diario**

   Título del blog que se mostrará en la página.

>[!NOTE]
>
>El Título del diario se utiliza para crear automáticamente la URL para el blog.
>Se utilizan un máximo de 50 caracteres (con 5 caracteres adicionales para la exclusividad) desde el título del diario que especifique aquí para crear una URL para el blog.

* **Descripción del diario**

   La descripción del blog.

* **Temas por página**

   Define el número de entradas/comentarios de blog que se muestran por página. El valor predeterminado es 10.

* **Moderado**

   Si se selecciona, la publicación de entradas y comentarios de blog debe aprobarse antes de que aparezcan en un sitio publicado. El valor predeterminado está desactivado.

* **Cerrado**

   Si se selecciona, el blog se cierra a las nuevas entradas y comentarios del blog. El valor predeterminado no está marcado.

* **Editor de texto enriquecido**

   Si se selecciona, las entradas de blog y los comentarios se pueden introducir con marcado. El valor predeterminado está marcado.

* **Permitir etiquetado**

   Si está activada, permita que los miembros agreguen etiquetas a su anuncio (consulte la ficha Campo **** de etiqueta). El valor predeterminado no está marcado.

* **Permitir cargas de archivos**

   Si está activada, permita que los archivos adjuntos se agreguen a una entrada de blog o comentario. El valor predeterminado no está marcado.

* **Tamaño máximo de archivo**

   Solo es pertinente si `Allow File Uploads` está marcado. Este campo limitará el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 104857600 (10 Mb).

* **Tipos de archivo permitidos**

   Solo es pertinente si `Allow File Uploads` está marcado. Una lista separada por comas de extensiones de archivo con el separador &quot;punto&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permitirá cargar los no especificados. El valor predeterminado no se especifica de forma que se permitan todos los tipos de archivo.

* **Tamaño máximo de archivo de imagen adjunto**

   Solo es relevante si está activada la opción Permitir cargas de archivos. Número máximo de bytes que puede tener un archivo de imagen cargado. El valor predeterminado es 2097152 (2 Mb).

* **Permitir respuestas**

   Si está activada, permita respuestas a los comentarios publicados en la entrada de blog. El valor predeterminado no está marcado.

* **Habilitar la votación**

   Si está activada, incluya la función Votación con una entrada de blog. El valor predeterminado no está marcado.

* **Permitir que los usuarios eliminen comentarios y temas**

   Si está activada, permita que los miembros eliminen los comentarios y las entradas de blog que han publicado. El valor predeterminado es** **sin marcar.

* **Permitir seguimiento**

   Si está activada, incluya la siguiente función para los artículos de blog, que permite que se [notifique](/help/communities/notifications.md) a los miembros de los nuevos anuncios. El valor predeterminado no está marcado.

* **Permitir suscripciones por correo electrónico**

   Si está activada, permita que se notifique a los miembros de los anuncios nuevos por correo electrónico ([suscripción](/help/communities/subscriptions.md)). Requiere `Allow Following` que se marque y se configure [el](/help/communities/email.md)correo electrónico. El valor predeterminado no está marcado.

* **Mostrar insignias**

   Si está activada, muestre [los distintivos](/help/communities/implementing-scoring.md) obtenidos y asignados con una entrada de blog de miembro. El valor predeterminado no está marcado.

* **No obtener respuestas en la página del listado**

* **Permitir contenido destacado**

   Si se selecciona, la idea se puede identificar como contenido [](/help/communities/featured.md)destacado. El valor predeterminado no está marcado.

* **Habilitar la mención**

   Si está habilitada, permite que los usuarios registrados de la comunidad identifiquen a otros miembros registrados (con el nombre, apellidos y nombre de usuario) y los etiqueten con la sintaxis común @user-name. Los usuarios etiquetados reciben notificaciones sobre sus menciones.

* **Menciones máximas**

   Restringir el número máximo de menciones permitidas en una publicación. El valor predeterminado es 10.

* **Patrón de menciones en la interfaz de usuario**

   Especifique la cadena de patrón permitida para etiquetar (@mención) al usuario registrado en una publicación. Por ejemplo, ~{{familyName}}{{givenName}}.

#### Ficha Moderación del usuario {#user-moderation-tab}

En la ficha Moderación **** del usuario, especifique la configuración de moderación:

* **Denegar entradas**

   Si se selecciona, los moderadores miembros de confianza podrán denegar las publicaciones e impedir que aparezcan en el foro público. El valor predeterminado no está marcado.

* **Cerrar/abrir de nuevo los temas**

   Si se selecciona, los moderadores de miembros de confianza pueden cerrar un tema para realizar más ediciones y comentarios, y también pueden volver a abrir un tema. El valor predeterminado no está marcado.

* **Marcar entradas**

   Si se selecciona, permita que los miembros marquen los temas o comentarios de otros como inapropiados. El valor predeterminado no está marcado**.**

* **Lista de motivos de indicación**

   Si se selecciona, permita que los miembros elijan, en una lista desplegable, el motivo por el que marcan un tema o comentario como inapropiado. El valor predeterminado no está marcado.

* **Motivo de indicación personalizado**

   Si se selecciona, permita que los miembros especifiquen su propio motivo para marcar un tema o comentario como inapropiado. El valor predeterminado no está marcado**.**

* **Umbral de moderación**

   Escriba el número de veces que los miembros deben marcar un tema o comentario antes de que se notifique a los moderadores. El valor predeterminado es 1 ( una vez).

* **Límite de indicación**

   Introduzca el número de veces que se debe marcar un tema o comentario antes de ocultarlo en la vista pública. Si se establece en -1, el tema o comentario marcado nunca se oculta en la vista pública. De lo contrario, este número debe ser bueno o igual al umbral de moderación. El valor predeterminado es 5.

#### Ficha Campo de etiqueta {#tag-field-tab}

En la ficha Campo **** Etiqueta, especifique las etiquetas que se pueden aplicar si se activa la opción **Permitir etiquetado** en la ficha **Configuración** :

* **Espacios de nombres permitidos**

   Relevante si `Allow Tagging` se comprueba en la ficha **Configuración **ficha. Las etiquetas que se pueden aplicar están limitadas a las que se encuentran dentro de las categorías de espacio de nombres seleccionadas. La lista de espacios de nombres incluye &quot;Etiquetas estándar&quot; (el espacio de nombres predeterminado) y &quot;Incluir todas las etiquetas&quot;. El valor predeterminado no está marcado, lo que significa que se permiten todos los espacios de nombres.

* **Límite de sugerencias**

   Escriba el número de etiquetas que se mostrarán como una sugerencia para el miembro que se publica en el foro. Un valor de -1 significa que no hay límites. El valor predeterminado es 0.

### Configuración de la barra lateral del blog {#configuring-blog-sidebar}

Al hacer doble clic en el `Blog Sidebar` componente, se abre un cuadro de diálogo de edición.

En la ficha Configuración **de barra lateral de** diario, especifique el formato de fecha para los archivos y el tipo de entradas que se mostrarán en la barra lateral:

![blog-component-sidebar](assets/blog-component-sidebar.png)

* **Formato de fecha**

   Formato utilizado para mostrar archivos de entradas de blog. El formato utiliza marcadores de posición siguiendo la convención Java.

   * yyyy : año completo, como &#39;2015&#39;
   * yy : año corto, como &#39;15&#39;
   * MMMMM : mes completo, como junio
   * MMM: mes corto, como Jun
   * MM: número de mes, como 06
   El valor predeterminado es &quot;aaaa MMMMM&quot;, que se mostraría, por ejemplo, &quot;2015 junio&quot;

* **Tipo de vista**

   Título y tipo de entradas de blog que se mostrarán en la barra lateral. La elección es entre

   * Autores
   * Categorías
   * Archivos

* **Ruta del componente de Blopg**

   *(Opcional)* La ubicación del recurso de blog desde el que se enumerarán los artículos de blog. Si se deja en blanco, usará el componente de resourceType `social/journal/components/hbs/journal` que aparece en la misma página.

   * Por ejemplo, `/content/sites/engage/en/blog/jcr:content/content/primary/blog`

* **Límite de sugerencias**

   El número de artículos de blog que se van a mostrar. Un valor de -1 significa que no hay límite. El valor predeterminado es -1.

## Experiencia del visitante del sitio {#site-visitor-experience}

En el entorno de publicación, la función de blog mostrará el artículo de blog más reciente seguido de artículos de blog más antiguos en orden descendente de creación. Las barras laterales de blog permiten a los visitantes del sitio aplicar filtros para limitar la selección de los artículos de blog mostrados.

El artículo del blog va seguido de un vínculo para publicar o ver comentarios.

Cuando se selecciona un artículo de blog, se muestran el artículo de blog y los comentarios (si están activados).

Otras capacidades dependen de si el visitante del sitio es un moderador, administrador, miembro de la comunidad, miembro privilegiado o anónimo.

### Trabajo con artículos {#working-with-articles}

Al crear un nuevo artículo de blog, hay la opción de:

1. Publicar inmediatamente
1. Publicación de un borrador
1. Publicar en una fecha y hora programadas

Los artículos del blog aparecerán en la ficha correspondiente (Publicados, Borradores o Programados) a los miembros que pueden crear al publicar.

#### Moderadores y administradores {#moderators-and-administrators}

Cuando el usuario que ha iniciado sesión tiene privilegios de moderador o administrador, puede realizar tareas [de](/help/communities/moderate-ugc.md) moderación (como permite la configuración del componente) en todos los artículos de blog y comentarios publicados en un blog.

![chlimage_1-232](assets/chlimage_1-232.png)

#### Miembros {#members}

Cuando el usuario que ha iniciado sesión es miembro de la comunidad o miembro [](/help/communities/users.md#privileged-members-group) privilegiado (según la configuración), puede seleccionar `New Article` crear y publicar un nuevo artículo de blog.

Concretamente, podrán:

* Creación de un nuevo artículo de blog
* Publicar un nuevo artículo de blog en nombre de otro miembro
* Publicar un comentario en un artículo de blog
* Editar su propio artículo o comentario de blog
* Eliminar su propio artículo o comentario de blog
* Marcar los artículos o comentarios del blog de otros

![chlimage_1-233](assets/chlimage_1-233.png) ![chlimage_1-234](assets/chlimage_1-234.png)

#### Anónimo {#anonymous}

Los visitantes del sitio que no hayan iniciado sesión sólo podrán leer artículos y comentarios publicados del blog, traducirlos si son compatibles, pero no podrán agregar un artículo o comentario del blog ni marcar los artículos o comentarios de otros.

![chlimage_1-235](assets/chlimage_1-235.png)

## Información adicional {#additional-information}

Puede encontrar más información en la página [Blog Essentials](/help/communities/blog-developer-basics.md) para desarrolladores.

Para obtener información sobre la moderación de entradas y comentarios de blog, consulte [Moderación del contenido](/help/communities/moderate-ugc.md)generado por el usuario.

Para etiquetar entradas y comentarios de blog, consulte [Etiquetado de contenido](/help/communities/tag-ugc.md)generado por el usuario.

Para ver la traducción de entradas y comentarios de blog, consulte [Traducción de contenido](/help/communities/translate-ugc.md)generado por el usuario.
