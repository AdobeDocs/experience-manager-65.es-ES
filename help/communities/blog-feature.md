---
title: Función Blog
description: Descubra cómo la función de blog admite el suministro de información de la comunidad en formato de diario. Los usuarios autorizados realizan las entradas en el entorno de Publish.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 4650ac36-5506-4efc-be35-fac9e5a58f3d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 0%

---

# Función Blog {#blog-feature}

## Introducción {#introduction}

La función de blog para AEM Communities se ha transformado de una actividad de creación a una verdadera actividad de la comunidad que tiene lugar en el entorno de Publish.

La función de blog permite proporcionar información de la comunidad en formato de diario. Las entradas de blog las realizan en el entorno de Publish miembros autorizados (usuarios registrados y conectados).

La funcionalidad del blog proporciona :

* Creación, en Publish, de artículos y comentarios de blogs
* Edición de texto enriquecido
* Imágenes en línea (con compatibilidad para arrastrar y soltar)
* Contenido de redes sociales incrustado ([Compatibilidad con incrustación](/help/communities/blog-developer-basics.md#allowing-rich-media))
* Modo de borrador
* Publicación programada
* Componga en nombre de (un [miembro con privilegios](/help/communities/users.md#privileged-members-group) puede crear contenido en nombre de otro miembro de la comunidad)
* [Moderación en contexto y masiva](/help/communities/moderate-ugc.md) de artículos y comentarios de blogs

Esta sección de la documentación describe lo siguiente:

* AEM Adición de la función de blog a un sitio de
* Ajustes de configuración para componentes del blog

>[!NOTE]
>
>Los componentes `Journal` y `Journal Sidebar` se denominan `Blog` y `Blog Sidebar`.
>
>AEM La función de blog encontrada en la versión 6.0 y versiones anteriores de se ha eliminado. Se basaba en una plantilla y solo permitía a los autores crear contenido en el entorno de creación.

## Adición de componentes de blog a una página {#adding-blog-components-to-a-page}

Si desea agregar un blog a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Blog`
* `Communities / Blog Sidebar`

Y arrástrelos a su lugar en una página donde debería aparecer el blog.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](/help/communities/basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](/help/communities/blog-developer-basics.md#essentials-for-client-side), el componente `Blog` aparece de la siguiente manera:

![add-blog-component](assets/add-blog-component.png)

### Configurar el blog {#configuring-blog}

Seleccione el componente `Blog` colocado para que pueda acceder y seleccionar el icono `Configure` que abre el cuadro de diálogo de edición.

![configurar](assets/configure-new.png)

![Configuración de blog](assets/blog-configure.png)

#### Pestaña Configuración {#settings-tab}

En la ficha **Configuración**, especifique las características básicas del blog:

* **Permitir miniatura de datos adjuntos**

  Si se selecciona, se crea una miniatura de la imagen adjunta.

* **Tamaño máximo de miniatura adjunta**

  Tamaño máximo (en píxeles) de la imagen en miniatura del archivo adjunto. El valor predeterminado es 800 x 800.

* **Tamaño mínimo de imagen para la miniatura**

  Tamaño mínimo (en bytes) de la imagen para generar miniaturas para imágenes alineadas. El valor predeterminado es 100000 bytes (100 kb).

* **Tamaño máximo de miniatura**

  Tamaño máximo (en píxeles) de la imagen en miniatura para la imagen alineada. El valor predeterminado es 800 x 800.

* **Permitir miembros privilegiados**

  Si se selecciona, solo se permite a los miembros privilegiados crear contenido.

* **Miembros privilegiados permitidos**

  Añada los miembros privilegiados que tienen permiso para crear contenido.

* **Bloquear contenido generado por el usuario en el modo de edición de autor**

  Si está habilitado, bloquea el contenido generado por el usuario mientras lo edita en el modo Autor.

* **Título de diario**

  Título del blog que se mostrará en la página.

>[!NOTE]
>
>El Título del diario se utiliza para crear automáticamente la dirección URL del blog.
>
>Se utilizan un máximo de 50 caracteres (con 5 caracteres adicionales para garantizar la exclusividad) del título del diario que especifique aquí para crear la dirección URL del blog.

* **Descripción del diario**

  La descripción del blog.

* **Temas por página**

  Define el número de entradas de blog/comentarios que se muestran por página. El valor predeterminado es 10.

* **Moderado**

  Si se selecciona, la publicación de entradas de blog y comentarios debe aprobarse antes de que aparezcan en un sitio publicado. El valor predeterminado es sin marcar.

* **Cerrado**

  Si se selecciona, el blog se cierra a las nuevas entradas de blog y comentarios. El valor predeterminado está desmarcado.

* **Editor de texto enriquecido**

  Si se selecciona, las entradas de blog y los comentarios se pueden introducir con marcado. La opción predeterminada está activada.

* **Permitir etiquetado**

  Si se selecciona esta opción, se permite a los miembros agregar etiquetas de etiqueta a sus publicaciones (consulte **Campo de etiqueta** en la pestaña). El valor predeterminado está desmarcado.

* **Permitir cargas de archivos**

  Si se selecciona esta opción, permite que se agreguen archivos adjuntos a una entrada de blog o comentario. El valor predeterminado está desmarcado.

* **Tamaño máximo de archivo**

  Relevante solo si `Allow File Uploads` está marcado. Este campo limita el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 104857600 (10 Mb).

* **Tipos de archivo permitidos**

  Relevante solo si `Allow File Uploads` está marcado. Lista separada por comas de las extensiones de archivo con el separador de &quot;puntos&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se podrán cargar los tipos de archivo no especificados. El valor predeterminado no se ha especificado, de modo que se permiten todos los tipos de archivo.

* **Tamaño máximo de archivo de imagen adjunto**

  Solo es relevante si está marcada la opción Permitir cargas de archivos. Número máximo de bytes que puede tener un archivo de imagen cargado. El valor predeterminado es 2097152 (2 Mb).

* **Permitir respuestas**

  Si está activada, permitir respuestas a comentarios publicados en la entrada de blog. El valor predeterminado está desmarcado.

* **Permitir Votación**

  Si se selecciona, se debe incluir la función de votación con una entrada de blog. El valor predeterminado está desmarcado.

* **Permitir que los usuarios eliminen comentarios y temas**

  Si se selecciona esta opción, permite que los miembros eliminen los comentarios y las entradas de blog que hayan publicado. El valor predeterminado está desmarcado.

* **Permitir seguimiento**

  Si se selecciona esta opción, se debe incluir la siguiente característica para artículos de blog, que permite [notificar](/help/communities/notifications.md) a los miembros las nuevas publicaciones. El valor predeterminado está desmarcado.

* **Permitir suscripciones por correo electrónico**

  Si se selecciona esta opción, se notificarán las nuevas publicaciones a los miembros por correo electrónico ([suscripción](/help/communities/subscriptions.md)). Requiere que se compruebe `Allow Following` y que se configure [correo electrónico](/help/communities/email.md). El valor predeterminado está desmarcado.

* **Mostrar insignias**

  Si se selecciona esta opción, se muestran [insignias](/help/communities/implementing-scoring.md) ganadas y asignadas con la entrada de blog de un miembro. El valor predeterminado está desmarcado.

* **No obtener respuestas en la página del listado**

* **Permitir contenido destacado**

  Si se selecciona, la idea se identifica como [contenido destacado](/help/communities/featured.md). El valor predeterminado está desmarcado.

* **Habilitar la mención**

  Si está habilitada, permite a los usuarios de la comunidad registrada identificar a otros miembros registrados (mediante nombre, apellidos y nombre de usuario) y etiquetarlos con la sintaxis común de @user-name. Los usuarios etiquetados reciben notificaciones sobre sus propias menciones.

* **Menciones máximas**

  Restringir el número máximo de menciones permitidas en una publicación. El valor predeterminado es 10.

* **Patrón de mención de IU**

  Especifique la cadena de patrón permitida para etiquetar (@mention) al usuario registrado en una publicación. Por ejemplo, `~{{familyName}}{{givenName}}`.

#### Pestaña Moderación de usuario {#user-moderation-tab}

En la ficha **Moderación de usuario**, especifique la configuración de moderación:

* **Denegar publicaciones**

  Si se selecciona, los moderadores de confianza pueden denegar las publicaciones e impedir que aparezcan en el foro público. El valor predeterminado está desmarcado.

* **Cerrar/volver a abrir temas**

  Si se selecciona esta opción, los moderadores de miembros de confianza pueden cerrar un tema para editarlo y enviarlo a otros comentarios, y también pueden volver a abrir un tema. El valor predeterminado está desmarcado.

* **Marcar entradas**

  Si se selecciona esta opción, se permite a los miembros marcar los temas o comentarios de otros como inadecuados. El valor predeterminado está desmarcado.

* **Lista de motivos de marca**

  Si se selecciona esta opción, se permite a los miembros elegir, en una lista desplegable, el motivo por el que marcan un tema o comentario como inapropiado. El valor predeterminado está desmarcado.

* **Motivo de indicación personalizado**

  Si se selecciona esta opción, permite que los miembros especifiquen su propio motivo para marcar un tema o comentario como inapropiado. El valor predeterminado está desmarcado.

* **Umbral de moderación**

  Introduzca el número de veces que los miembros deben marcar un tema o comentario antes de notificarlo a los moderadores. El valor predeterminado es 1 ( una vez).

* **Límite de indicación**

  Introduzca el número de veces que se debe marcar un tema o comentario antes de ocultarlo de la vista pública. Si se establece en -1, el tema o comentario marcado nunca se ocultará de la vista pública. De lo contrario, este número debe ser mayor o igual que el umbral de moderación. El valor predeterminado es 5.

#### Pestaña Campo de etiqueta {#tag-field-tab}

En la ficha **Campo de etiqueta**, especifique qué etiquetas se pueden aplicar si **Permitir etiquetado** está marcado en la ficha **Configuración**:

* **Áreas de nombres permitidas**

  Relevante si `Allow Tagging` está marcado en la ficha **Configuración**. Las etiquetas que se pueden aplicar se limitan a aquellas etiquetas dentro de las categorías de área de nombres comprobadas. La lista de áreas de nombres incluye &quot;Etiquetas estándar&quot; (el área de nombres predeterminada) e &quot;Incluir todas las etiquetas&quot;. El valor predeterminado es ninguno marcado, lo que significa que se permiten todas las áreas de nombres.

* **Límite de sugerencias**

  Introduzca el número de etiquetas que desea mostrar como sugerencia al usuario que publica en el foro. Un valor de -1 significa que no hay límites. El valor predeterminado es 0.

### Configurar la barra lateral del blog {#configuring-blog-sidebar}

Al hacer doble clic en el componente `Blog Sidebar`, se abre un cuadro de diálogo de edición.

En la ficha **Configuración de la barra lateral del diario**, especifique el formato de fecha para los archivos y el tipo de entradas que se mostrarán en la barra lateral

![barra lateral-componentes-blog](assets/blog-component-sidebar.png)

* **Formato de fecha**

  Formato utilizado para mostrar los archivos de las entradas de blog. El formato utiliza marcadores de posición siguiendo la convención de Java™.

   * yyyy : año completo, como &#39;2015&#39;
   * aa : año corto, como &#39;15&#39;
   * MMMMM : mes completo, como junio
   * MMM : mes corto, como junio
   * MM : número de mes, como 06

  El valor predeterminado es &quot;yyyy MMMMM&quot;, que muestra, por ejemplo, &quot;2015 June&quot;

* **Tipo de vista**

  Título y tipo de entradas de blog que se mostrarán en la barra lateral. La elección es entre

   * Autores
   * Categorías
   * Archivos

* **Ruta del componente Blog**

  *(Opcional)* Ubicación del recurso de blog desde el que se enumerarán los artículos de blog. Si se deja en blanco, se utiliza el componente de resourceType `social/journal/components/hbs/journal` que aparece en la misma página.

   * Por ejemplo, `/content/sites/engage/en/blog/jcr:content/content/primary/blog`

* **Límite de sugerencias**

  El número de artículos de blog que se mostrarán. Un valor de -1 significa que no hay límite. El valor predeterminado es -1.

## Experiencia del visitante del sitio {#site-visitor-experience}

En el entorno de publicación, la función de blog muestra el artículo de blog más reciente seguido de los artículos de blog más antiguos en orden descendente de creación. Las barras laterales del blog permiten a los visitantes del sitio aplicar filtros para limitar la selección de artículos de blog mostrados.

El artículo del blog va seguido de un vínculo para publicar o ver comentarios.

Cuando se selecciona un artículo de blog, se muestran el artículo del blog y los comentarios (si está activado).

Otras capacidades dependen de si el visitante del sitio es un moderador, administrador, miembro de la comunidad, miembro privilegiado o anónimo.

### Trabajar con artículos {#working-with-articles}

Al crear un artículo de blog, existe la opción de hacer lo siguiente:

1. Publish inmediatamente
1. Publish a Draft
1. Publish en una fecha y hora programadas

Los artículos del blog aparecen en la ficha adecuada (Publicado, Borradores o Programado) para que los miembros puedan crear en el momento de la publicación.

#### Moderadores y administradores {#moderators-and-administrators}

Cuando el usuario que ha iniciado sesión tiene privilegios de moderador o administrador, puede realizar [tareas de moderación](/help/communities/moderate-ugc.md) (según lo permita la configuración del componente) en todos los artículos de blog y comentarios publicados en un blog.

![moderador-homepage](assets/moderator-homepage.png)

#### Miembros {#members}

Cuando el usuario que inició sesión es un miembro de la comunidad o [miembro privilegiado](/help/communities/users.md#privileged-members-group) (según la configuración), puede seleccionar `New Article` para crear y publicar un nuevo artículo de blog.

Concretamente, pueden:

* Creación de un artículo de blog
* Post publica un nuevo artículo de blog en nombre de otro miembro
* Post un comentario a un artículo de blog
* Editar su propio artículo o comentario del blog
* Eliminar su propio artículo o comentario del blog
* Marcar artículos o comentarios de blogs de otros usuarios

![página principal-miembro](assets/member-homepage.png)

![crear-blog](assets/create-blog.png)

#### Anónimo {#anonymous}

Los visitantes del sitio que no hayan iniciado sesión solo podrán leer los artículos y comentarios publicados en el blog, traducirlos si es compatible, pero no podrán añadir un artículo o comentario en el blog ni marcar los artículos o comentarios de otros.

![vista-de-usuario-anónimo](assets/anonymous-user-view.png)

## Información adicional {#additional-information}

Encontrará más información en la página de [Blog Essentials](/help/communities/blog-developer-basics.md) para desarrolladores.

Para moderar las entradas de blog y los comentarios, vea [Moderar el contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para etiquetar entradas de blog y comentarios, consulte [Etiquetado de contenido generado por el usuario](/help/communities/tag-ugc.md).

Para obtener la traducción de entradas de blog y comentarios, consulte [Traducción de contenido generado por el usuario](/help/communities/translate-ugc.md).
