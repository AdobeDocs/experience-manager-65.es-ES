---
title: Función Foro
description: Obtenga información sobre cómo agregar y configurar la función de foro que proporciona un área para que los miembros de la comunidad que iniciaron sesión creen, vean, sigan, busquen o respondan a temas.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b1a4917-9db6-436a-a5fd-c102fe41fb9d
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 9%

---

# Función Foro{#forum-feature}

## Introducción {#introduction}

La función de foro proporciona un área para que los visitantes del sitio (miembros de la comunidad) que han iniciado sesión en el entorno de publicación puedan hacer lo siguiente:

* Crear temas
* Ver y responder a temas
* Seguir un tema
* Buscar en un foro
* Ayuda a moderar el contenido del foro
* Mover temas de foro de una página a otra

Esta sección de la documentación describe lo siguiente:

* AEM Adición de la función de foro a un sitio de.
* Ajustes de configuración para `Forum` componente.

### Adición de un foro a una página {#adding-a-forum-to-a-page}

Para agregar un `Forum` a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Forum`

Y arrástrelo a su lugar en una página en la que debería aparecer el foro.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](/help/communities/basics.md).

Si la variable [bibliotecas requeridas del lado del cliente](/help/communities/essentials-forum.md#essentials-for-client-side) están incluidos, así es como se `Forum` el componente aparece:

![forum-component](assets/forum-component.png)

### Configuración de un foro {#configuring-a-forum}

Seleccione el colocado `Forum` para que pueda acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configure-new](assets/configure-new.png)

![forum-config](assets/forum-config.png)

#### Pestaña Configuración {#settings-tab}

En el **Configuración** pestaña, especifique la configuración de los temas y las respuestas:

* **Permitir la miniatura del archivo adjunto**

  Si se selecciona, se crea una miniatura de la imagen adjunta.

* **Tamaño máximo de la miniatura del archivo adjunto**

  Tamaño máximo (en píxeles) de la imagen en miniatura del archivo adjunto. El valor predeterminado es 800 x 800.

* **Tamaño mínimo de la imagen de la miniatura**
* **Tamaño máximo de la miniatura**

  Tamaño máximo (en píxeles) de la imagen en miniatura para la imagen alineada. El valor predeterminado es 800 x 800.

* **Temas por página**

  Define el número de temas/entradas que se muestran por página. El valor predeterminado es 10.

* **Moderado**

  Si se selecciona, la publicación de temas y comentarios debe aprobarse antes de que puedan aparecer en un sitio de publicación. El valor predeterminado está desmarcado.

* **Cerrado**

  Si se selecciona, el foro cierra nuevos temas y comentarios. El valor predeterminado está desmarcado.

* **Editor de texto enriquecido**

  Si se selecciona, los temas y los comentarios se pueden introducir con marcado. El valor predeterminado está desmarcado.

* **Permitir etiquetado**

  Si se selecciona esta opción, permite que los miembros agreguen etiquetas de etiqueta a sus publicaciones (consulte **Campo de etiqueta** pestaña). El valor predeterminado está desmarcado.

* **Permitir cargas de archivos**

  Si se selecciona esta opción, permite que se agreguen archivos adjuntos al tema o comentario. El valor predeterminado está desmarcado.

* **Permitir seguimiento**

  Si se selecciona esta opción, se incluye la siguiente función para las publicaciones del foro, que permite a los miembros [notificado](/help/communities/notifications.md) de nuevos puestos. El valor predeterminado está desmarcado.

* **Permitir fijación**

  Si se selecciona, los temas del foro pueden estar anclados en la parte superior de la lista de temas. El valor predeterminado está desmarcado.

* **Permitir contenido destacado**

  Si se selecciona, la idea se puede identificar como [contenido destacado](/help/communities/featured.md). El valor predeterminado está desmarcado.

* **Permitir suscripciones por correo electrónico**

  Si se selecciona esta opción, se notificará a los miembros de las nuevas publicaciones por correo electrónico ([suscripción](/help/communities/subscriptions.md)). Requiere `Allow Following` que se van a comprobar y [correo electrónico configurado](/help/communities/email.md). El valor predeterminado está desmarcado.

* **Tamaño máximo de archivo**

  Relevante solo si `Allow File Uploads` está marcada. Este campo limita el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 104857600 (10 Mb).

* **Tipos de archivo permitidos**

  Relevante solo si `Allow File Uploads` está marcada. Lista separada por comas de las extensiones de archivo con el separador de &quot;puntos&quot;. Por ejemplo, .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se podrán cargar los que no se hayan especificado. El valor predeterminado no se ha especificado, de modo que se permiten todos los tipos de archivo.

* **Tamaño máximo de archivo de imagen adjunto**
Solo es relevante si está marcada la opción Permitir cargas de archivos. Número máximo de bytes que puede tener un archivo de imagen cargado. El valor predeterminado es 2097152 (2 Mb).

* **Permitir respuestas de debate**

  Si se selecciona esta opción, se permiten las respuestas a los comentarios publicados en el tema. El valor predeterminado está desmarcado.

* **Habilitar la votación**

  Si se selecciona esta opción, se debe incluir la función de votación con un tema. El valor predeterminado está desmarcado.

* **Permitir que los usuarios eliminen comentarios y temas**

  Si se selecciona esta opción, permite que los miembros eliminen los comentarios y temas que hayan publicado. El valor predeterminado está desmarcado.

* **Mostrar rutas**

  Si se selecciona, se muestran las rutas de exploración de navegación en las páginas de temas. La opción predeterminada está activada.

* **Mostrar insignias**

  Si se selecciona esta opción, se muestran las ganancias y las asignaciones [distintivos](/help/communities/implementing-scoring.md) con la entrada de blog de un miembro. El valor predeterminado está desmarcado.

* **Permitir miembros privilegiados**

  Si se selecciona, solo se permite a los miembros privilegiados crear contenido.

* **Miembros privilegiados permitidos**

  Añada los miembros privilegiados que tienen permiso para crear contenido.

* **Bloquear contenido generado por el usuario en el modo de edición de autor**

  Si está habilitado, bloquea el contenido generado por el usuario mientras lo edita en el modo Autor.

* **Habilitar la mención**

  Si está habilitada, permite a los usuarios de la comunidad registrada identificar a otros miembros registrados (mediante nombre, apellidos y nombre de usuario) y etiquetarlos con la sintaxis común de @user-name. Los usuarios etiquetados reciben notificaciones sobre sus menciones.

* **Menciones máximas**

  Restringir el número máximo de menciones permitidas en una publicación. El valor predeterminado es 10.

* **Patrón de menciones en la interfaz de usuario**

  Especifique la cadena de patrón permitida para etiquetar (@mention) al usuario registrado en una publicación. Por ejemplo, `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Puede ser necesario comprobar ambos `AllowThreaded Replies` y `Allow users to Delete Comments and Topics` para habilitar los comentarios sobre un tema.

#### Pestaña Moderación de usuario {#user-moderation-tab}

En el **Moderación de usuario** , especifique cómo se administran los temas expuestos y las respuestas (contenido generado por el usuario). Para obtener más información, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

* **Denegar entradas**

  Si se selecciona, los moderadores de confianza pueden denegar las publicaciones e impedir que aparezcan en el foro público. El valor predeterminado está desmarcado.

* **Cerrar/abrir de nuevo los temas**

  Si se selecciona esta opción, los moderadores de miembros de confianza pueden cerrar un tema para editarlo y enviarlo a otros comentarios, y también pueden volver a abrir un tema. El valor predeterminado está desmarcado.

* **Mover temas**

  Si se selecciona esta opción, los moderadores de publicación pueden mover los temas. La opción predeterminada está activada.

* **Marcar entradas**

  Si se selecciona esta opción, se permite a los miembros marcar los temas o comentarios de otros como inadecuados. El valor predeterminado está desmarcado.

* **Lista de motivos de indicación**

  Si se selecciona esta opción, se permite a los miembros elegir, en una lista desplegable, el motivo por el que marcan un tema o comentario como inapropiado. El valor predeterminado está desmarcado.

* **Motivo de indicación personalizado**

  Si se selecciona esta opción, permite que los miembros especifiquen su propio motivo para marcar un tema o comentario como inapropiado. El valor predeterminado está desmarcado.

* **Umbral de moderación**

  Introduzca el número de veces que los miembros deben marcar un tema o comentario antes de notificarlo a los moderadores. El valor predeterminado es 1 (una vez).

* **Límite de indicación**

  Introduzca el número de veces que se debe marcar un tema o comentario antes de ocultarlo de la vista pública. Si se establece en -1, el tema o comentario marcado nunca se ocultará de la vista pública. De lo contrario, este número debe ser mayor o igual que el umbral de moderación. El valor predeterminado es 5.

#### Pestaña Campo de etiqueta {#tag-field-tab}

En el **Campo de etiqueta** pestaña, las etiquetas que se pueden aplicar, si se permiten en la **Configuración** están limitadas según las áreas de nombres seleccionadas.

* **Espacios de nombres permitidos**

  Relevante si `Allow Tagging` está marcada en la **Configuración** pestaña. Las etiquetas que se pueden aplicar se limitan a aquellas dentro de las categorías de área de nombres comprobadas. La lista de áreas de nombres incluye &quot;Etiquetas estándar&quot; (el área de nombres predeterminada) e &quot;Incluir todas las etiquetas&quot;. El valor predeterminado es ninguno marcado, lo que significa que se permiten todas las áreas de nombres.

* **Límite de sugerencias**

  Introduzca el número de etiquetas que desea mostrar como sugerencia al usuario que publica en el foro. El valor predeterminado es **-**1 (sin límites).

#### Pestaña Traducción {#translation-tab}

En el **Traducción** pestaña, si la traducción está habilitada para el sitio de la comunidad, la traducción puede configurarse para traducir todo el tema o las publicaciones seleccionadas.

* **Traducir todos**

  Si se selecciona, el hilo del foro se traduce al idioma preferido del usuario. El valor predeterminado está desmarcado.

#### Pestaña Configuración de ordenación {#sort-settings-tab}

En el **Configuración de orden** , especifique cómo se ordenan los comentarios publicados cuando se muestran.

* **Ordenar por**

  Compruebe todas las selecciones de ordenación permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. El valor predeterminado es `Newest, Oldest, Last Updated`.

* **Establecer como predeterminado**

  Tire hacia abajo para seleccionar una de las opciones de ordenación seleccionadas y que aparezca como la predeterminada. El valor predeterminado es `Newest`.

* **Seleccione las opciones de hora para la clasificación de Analytics**

  Tire hacia abajo para seleccionar una de las siguientes opciones: `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

  El valor predeterminado es `All`.

### Información adicional {#additional-information}

Puede encontrar más información en la [Forum Essentials](/help/communities/essentials-forum.md) para desarrolladores.

Para ver la moderación de los temas publicados y los comentarios, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para etiquetar temas y comentarios publicados, consulte [Etiquetado del contenido generado por el usuario](/help/communities/tag-ugc.md).

Para ver la traducción de los temas publicados y los comentarios, consulte [Traducción del contenido generado por el usuario](/help/communities/translate-ugc.md).
