---
title: Función Foro
description: Obtenga información sobre cómo agregar y configurar la función de foro que proporciona un área para que los miembros de la comunidad que iniciaron sesión creen, vean, sigan, busquen o respondan a temas.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b1a4917-9db6-436a-a5fd-c102fe41fb9d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 1%

---

# Función Foro{#forum-feature}

## Introducción {#introduction}

La función de foro proporciona un área para que los visitantes del sitio (miembros de la comunidad) conectados en el entorno de Publish puedan hacer lo siguiente:

* Crear temas
* Ver y responder a temas
* Seguir un tema
* Buscar en un foro
* Ayuda a moderar el contenido del foro
* Mover temas de foro de una página a otra

Esta sección de la documentación describe lo siguiente:

* AEM Adición de la función de foro a un sitio de.
* Ajustes de configuración para el componente `Forum`.

### Adición de un foro a una página {#adding-a-forum-to-a-page}

Para agregar un componente `Forum` a una página en modo de autor, use el explorador de componentes para localizar

* `Communities / Forum`

Y arrástrelo a su lugar en una página en la que debería aparecer el foro.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](/help/communities/basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](/help/communities/essentials-forum.md#essentials-for-client-side), así es como aparece el componente `Forum`:

![forum-component](assets/forum-component.png)

### Configuración de un foro {#configuring-a-forum}

Seleccione el componente `Forum` colocado para que pueda acceder y seleccionar el icono `Configure` que abre el cuadro de diálogo de edición.

![configurar-nuevo](assets/configure-new.png)

![forum-config](assets/forum-config.png)

#### Pestaña Configuración {#settings-tab}

En la ficha **Configuración**, especifique la configuración de los temas y las respuestas:

* **Permitir miniatura de datos adjuntos**

  Si se selecciona, se crea una miniatura de la imagen adjunta.

* **Tamaño máximo de miniatura adjunta**

  Tamaño máximo (en píxeles) de la imagen en miniatura del archivo adjunto. El valor predeterminado es 800 x 800.

* **Tamaño mínimo de la imagen de la miniatura**
* **Tamaño máximo de miniatura**

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

  Si se selecciona esta opción, se permite a los miembros agregar etiquetas de etiqueta a sus publicaciones (consulte **Campo de etiqueta** en la pestaña). El valor predeterminado está desmarcado.

* **Permitir cargas de archivos**

  Si se selecciona esta opción, permite que se agreguen archivos adjuntos al tema o comentario. El valor predeterminado está desmarcado.

* **Permitir seguimiento**

  Si se selecciona esta opción, se debe incluir la siguiente característica para las publicaciones del foro, que permite [notificar](/help/communities/notifications.md) a los miembros las nuevas publicaciones. El valor predeterminado está desmarcado.

* **Permitir anclaje**

  Si se selecciona, los temas del foro pueden estar anclados en la parte superior de la lista de temas. El valor predeterminado está desmarcado.

* **Permitir contenido destacado**

  Si se selecciona, la idea se puede identificar como [contenido destacado](/help/communities/featured.md). El valor predeterminado está desmarcado.

* **Permitir suscripciones por correo electrónico**

  Si se selecciona esta opción, se notificarán las nuevas publicaciones a los miembros por correo electrónico ([suscripción](/help/communities/subscriptions.md)). Requiere que se compruebe `Allow Following` y que se configure [correo electrónico](/help/communities/email.md). El valor predeterminado está desmarcado.

* **Tamaño máximo de archivo**

  Relevante solo si `Allow File Uploads` está marcado. Este campo limita el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 104857600 (10 Mb).

* **Tipos de archivo permitidos**

  Relevante solo si `Allow File Uploads` está marcado. Lista separada por comas de las extensiones de archivo con el separador de &quot;puntos&quot;. Por ejemplo, .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se podrán cargar los que no se hayan especificado. El valor predeterminado no se ha especificado, de modo que se permiten todos los tipos de archivo.

* **Tamaño máximo de archivo de imagen adjunto**
Solo es relevante si está marcada la opción Permitir cargas de archivos. Número máximo de bytes que puede tener un archivo de imagen cargado. El valor predeterminado es 2097152 (2 Mb).

* **Permitir respuestas de subprocesos**

  Si se selecciona esta opción, se permiten las respuestas a los comentarios publicados en el tema. El valor predeterminado está desmarcado.

* **Permitir Votación**

  Si se selecciona esta opción, se debe incluir la función de votación con un tema. El valor predeterminado está desmarcado.

* **Permitir que los usuarios eliminen comentarios y temas**

  Si se selecciona esta opción, permite que los miembros eliminen los comentarios y temas que hayan publicado. El valor predeterminado está desmarcado.

* **Mostrar rutas**

  Si se selecciona, se muestran las rutas de exploración de navegación en las páginas de temas. La opción predeterminada está activada.

* **Mostrar insignias**

  Si se selecciona esta opción, se muestran [insignias](/help/communities/implementing-scoring.md) ganadas y asignadas con la entrada de blog de un miembro. El valor predeterminado está desmarcado.

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

* **Patrón de mención de IU**

  Especifique la cadena de patrón permitida para etiquetar (@mention) al usuario registrado en una publicación. Por ejemplo, `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Es posible que sea necesario comprobar `AllowThreaded Replies` y `Allow users to Delete Comments and Topics` para habilitar los comentarios en un tema.

#### Pestaña Moderación de usuario {#user-moderation-tab}

En la ficha **Moderación de usuarios** especifique cómo se administran los temas publicados y las respuestas (contenido generado por el usuario). Para obtener más información, consulte [Moderar contenido generado por el usuario](/help/communities/moderate-ugc.md).

* **Denegar publicaciones**

  Si se selecciona, los moderadores de confianza pueden denegar las publicaciones e impedir que aparezcan en el foro público. El valor predeterminado está desmarcado.

* **Cerrar/volver a abrir temas**

  Si se selecciona esta opción, los moderadores de miembros de confianza pueden cerrar un tema para editarlo y enviarlo a otros comentarios, y también pueden volver a abrir un tema. El valor predeterminado está desmarcado.

* **Mover temas**

  Si se selecciona esta opción, los moderadores de publicación pueden mover los temas. La opción predeterminada está activada.

* **Marcar entradas**

  Si se selecciona esta opción, se permite a los miembros marcar los temas o comentarios de otros como inadecuados. El valor predeterminado está desmarcado.

* **Lista de motivos de marca**

  Si se selecciona esta opción, se permite a los miembros elegir, en una lista desplegable, el motivo por el que marcan un tema o comentario como inapropiado. El valor predeterminado está desmarcado.

* **Motivo de indicación personalizado**

  Si se selecciona esta opción, permite que los miembros especifiquen su propio motivo para marcar un tema o comentario como inapropiado. El valor predeterminado está desmarcado.

* **Umbral de moderación**

  Introduzca el número de veces que los miembros deben marcar un tema o comentario antes de notificarlo a los moderadores. El valor predeterminado es 1 (una vez).

* **Límite de indicación**

  Introduzca el número de veces que se debe marcar un tema o comentario antes de ocultarlo de la vista pública. Si se establece en -1, el tema o comentario marcado nunca se ocultará de la vista pública. De lo contrario, este número debe ser mayor o igual que el umbral de moderación. El valor predeterminado es 5.

#### Pestaña Campo de etiqueta {#tag-field-tab}

En la ficha **Campo de etiqueta**, las etiquetas que se pueden aplicar, si se permiten en la ficha **Configuración**, están limitadas según las áreas de nombres elegidas.

* **Áreas de nombres permitidas**

  Relevante si `Allow Tagging` está marcado en la ficha **Configuración**. Las etiquetas que se pueden aplicar se limitan a aquellas dentro de las categorías de área de nombres comprobadas. La lista de áreas de nombres incluye &quot;Etiquetas estándar&quot; (el área de nombres predeterminada) e &quot;Incluir todas las etiquetas&quot;. El valor predeterminado es ninguno marcado, lo que significa que se permiten todas las áreas de nombres.

* **Límite de sugerencias**

  Introduzca el número de etiquetas que desea mostrar como sugerencia al usuario que publica en el foro. El valor predeterminado es **-**&#x200B;1 (sin límites).

#### Pestaña Traducción {#translation-tab}

En la ficha **Traducción**, si la traducción está habilitada para el sitio de la comunidad, la traducción puede establecerse para traducir todo el tema o las publicaciones seleccionadas.

* **Traducir todo**

  Si se selecciona, el hilo del foro se traduce al idioma preferido del usuario. El valor predeterminado está desmarcado.

#### Pestaña Configuración de ordenación {#sort-settings-tab}

En la ficha **Configuración de ordenación**, especifique cómo se ordenan los comentarios publicados cuando se muestran.

* **Ordenar por**

  Comprobar todas las selecciones de ordenación permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. El valor predeterminado es `Newest, Oldest, Last Updated`.

* **Establecer como predeterminado**

  Tire hacia abajo para seleccionar una de las opciones de ordenación seleccionadas y que aparezca como la predeterminada. El valor predeterminado es `Newest`.

* **Seleccionar opciones de hora para la ordenación de Analytics**

  Tire hacia abajo para seleccionar una de las siguientes opciones: `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

  El valor predeterminado es `All`.

### Información adicional {#additional-information}

Encontrará más información en la página de [Forum Essentials](/help/communities/essentials-forum.md) para desarrolladores.

Para moderar los temas publicados y los comentarios, vea [Moderar el contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para etiquetar temas y comentarios publicados, consulte [Etiquetado de contenido generado por el usuario](/help/communities/tag-ugc.md).

Para obtener la traducción de los temas y comentarios publicados, consulte [Traducción del contenido generado por el usuario](/help/communities/translate-ugc.md).
