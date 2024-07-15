---
title: Función ideación
description: Aprenda a añadir y configurar la función Ideación que permite a los miembros de la comunidad crear, ver, seguir, votar y comentar ideas compartidas con la comunidad.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: e130bab4-524d-4413-ba8b-53d0ed9e8623
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 0%

---

# Función ideación {#ideation-feature}

## Introducción {#introduction}

La función de ideación proporciona un área para que los visitantes del sitio (miembros de la comunidad) conectados en el entorno de Publish puedan hacer lo siguiente:

* Cree ideas para compartir con la comunidad.
* Ver y comentar ideas.
* Sigue una idea.
* Vote una idea.

Esta sección de la documentación describe lo siguiente:

* AEM Adición de la función de ideación a un sitio de.
* Ajustes de configuración del componente Ideación.

### Adición de una idea a una página {#adding-a-ideation-to-a-page}

Para agregar un componente `Ideation` a una página en modo de autor, use el explorador de componentes para localizar

* `Communities / Ideation`

Y arrástrela a su lugar en una página donde debería aparecer la idea.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](/help/communities/basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](/help/communities/ideation.md#essentials-for-client-side), así es como aparece el componente `Ideation`:

![ideación](assets/ideation.png)

### Configuración de una idea {#configuring-an-ideation}

Seleccione el componente `Ideation` colocado para que pueda acceder y seleccionar el icono `Configure` que abre el cuadro de diálogo de edición.

![configurar-nuevo](assets/configure-new.png)

![configuración de ideación](assets/ideation-settings.png)

#### Pestaña Configuración {#settings-tab}

En la ficha **[!UICONTROL Configuración]**, especifique la configuración para las ideas y los comentarios:

* **Permitir miniatura de datos adjuntos**
* **Tamaño máximo de miniatura adjunta**
* **Tamaño mínimo de imagen para la miniatura**
* **Tamaño máximo de miniatura**
* **Permitir miembros privilegiados**
* **Miembros privilegiados permitidos**
* **Bloquear contenido generado por el usuario en el modo de edición de autor**
* **Título de ideación**

* El título para mostrar de la idea. El valor predeterminado es `Ideation`.
* **Descripción de ideación**

  Descripción que se mostrará como subtítulo de la idea. El valor predeterminado es sin descripción.

* **Temas por página**

  Define el número de ideas/entradas que se muestran por página. El valor predeterminado es 10.

* **Moderado**

  Si se selecciona, la publicación de ideas y comentarios debe aprobarse antes de que puedan aparecer en un sitio de publicación. El valor predeterminado está desmarcado.

* **Cerrado**

  Si se selecciona, el foro de ideas se cierra a nuevas ideas y comentarios. El valor predeterminado está desmarcado.

* **Editor de texto enriquecido**

  Si se selecciona, las ideas y los comentarios se pueden introducir con marcado. El valor predeterminado está desmarcado.

* **Permitir etiquetado**

  Si se selecciona esta opción, se permite a los miembros agregar etiquetas de etiqueta a sus publicaciones (consulte **[!UICONTROL Campo de etiqueta]** en la pestaña). El valor predeterminado está desmarcado.

* **Permitir cargas de archivos**

  Si se selecciona esta opción, se pueden añadir archivos adjuntos a la idea o al comentario. El valor predeterminado está desmarcado.

* **Tamaño máximo de archivo**

  Relevante solo si `Allow File Uploads` está marcado. Este campo limita el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 104857600 (10 Mb).

* **Tipos de archivo permitidos**

  Relevante solo si `Allow File Uploads` está marcado. Lista separada por comas de las extensiones de archivo con el separador de &quot;puntos&quot;. Por ejemplo, .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se podrán cargar los que no se hayan especificado. El valor predeterminado no se ha especificado, de modo que se permiten todos los tipos de archivo.

* **Tamaño máximo de archivo de imagen adjunto**

  Solo es relevante si está marcada la opción Permitir cargas de archivos. Número máximo de bytes que puede tener un archivo de imagen cargado. El valor predeterminado es 2097152 (2 Mb).

* **Permitir respuestas**

  Si se selecciona esta opción, se permiten las respuestas a los comentarios publicados en la idea. El valor predeterminado está desmarcado.

* **Permitir Votación**

  Si se selecciona esta opción, se permite la votación sobre los comentarios de una idea. El valor predeterminado está desmarcado.

* **Permitir que los usuarios eliminen comentarios y temas**

  Si se selecciona esta opción, se permite a los miembros eliminar los comentarios y las ideas que hayan publicado. El valor predeterminado está desmarcado.

* **Permitir seguimiento**

  Si se selecciona esta opción, se debe incluir la siguiente característica para las publicaciones de ideas, que permite [notificar](/help/communities/notifications.md) a los miembros las nuevas publicaciones. El valor predeterminado está desmarcado.

* **Permitir suscripciones por correo electrónico**

  Si se selecciona esta opción, se notificarán las nuevas publicaciones a los miembros por correo electrónico ([suscripción](/help/communities/subscriptions.md)). Requiere que se compruebe `Allow Following` y que se configure [correo electrónico](/help/communities/email.md). El valor predeterminado está desmarcado.

* **Permitir Votación**

  Si se selecciona esta opción, se permite la votación sobre los comentarios de una idea. El valor predeterminado está desmarcado.

* **Mostrar insignias**

  Si se selecciona esta opción, se muestran [insignias](/help/communities/implementing-scoring.md) ganadas y asignadas con la idea de un miembro. El valor predeterminado está desmarcado.

* **No obtener respuestas en la página del listado**

* **Permitir contenido destacado**

  Si se selecciona, la idea se puede identificar como [contenido destacado](/help/communities/featured.md). El valor predeterminado está desmarcado.

* **Habilitar la mención**
* **Menciones máximas**
* **Patrón de mención de IU**

#### Pestaña Moderación de usuario {#user-moderation-tab}

En la ficha **[!UICONTROL Moderación de usuarios]** especifique cómo se administran las ideas publicadas y los comentarios (contenido generado por el usuario). Para obtener más información, consulte [Moderar contenido generado por el usuario](/help/communities/moderate-ugc.md).

* **Denegar publicaciones**

  Si se selecciona, los moderadores de confianza pueden denegar las publicaciones e impedir que aparezcan en el foro público. El valor predeterminado está desmarcado.

* **Cerrar o volver a abrir temas**

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

En la ficha **[!UICONTROL Campo de etiqueta]**, las etiquetas que se pueden aplicar, si se permiten en la ficha **[!UICONTROL Configuración]**, están limitadas según las áreas de nombres elegidas.

* **Áreas de nombres permitidas**

  Relevante si `Allow Tagging` está marcado en la ficha **[!UICONTROL Configuración]**. Las etiquetas que se pueden aplicar se limitan a aquellas dentro de las categorías de área de nombres comprobadas. La lista de áreas de nombres incluye &quot;Etiquetas estándar&quot; (el área de nombres predeterminada) e &quot;Incluir todas las etiquetas&quot;. El valor predeterminado es ninguno marcado, lo que significa que se permiten todas las áreas de nombres.

* **Límite de sugerencias**

  Introduzca el número de etiquetas que desea mostrar como sugerencia al usuario que publica en el foro. Un valor de **-1** significa que no hay límite. El valor predeterminado es 0.

#### Pestaña Configuración de ordenación {#sort-settings-tab}

En la ficha **[!UICONTROL Configuración de ordenación]**, especifique cómo se ordenan los comentarios publicados cuando se muestran.

* **Ordenar por**

  Compruebe todas las selecciones de ordenación permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. El valor predeterminado es `Newest, Oldest, Last Updated`.

* **Establecer como predeterminado**

  Tire hacia abajo para seleccionar una de las opciones de ordenación seleccionadas y que aparezca como la predeterminada. El valor predeterminado es `Newest`.

* **Seleccionar opciones de hora para la ordenación de Analytics**

  Tire hacia abajo para seleccionar uno de `All, Last 24 Hours, Last 7 Days, Last 30 Days`. El valor predeterminado es `All`.

## Experiencia del visitante del sitio {#site-visitor-experience}

### Creación de una idea {#creating-idea}

Al igual que con todas las funciones de las Comunidades, si no ha iniciado sesión, el visitante de un sitio solo puede leer ideas y ver opiniones de otros (a través de comentarios y votaciones/me gusta).

Una vez que haya iniciado sesión, un miembro puede crear una idea.

![crear-nueva-idea](assets/create-new-idea.png)

Antes de presentar la idea, es posible que el miembro guarde un borrador.

Al seleccionar el botón `Save as Draft`, se guarda un borrador.

![save-idea](assets/save-idea.png)

Cuando vea los borradores guardados en la ficha `My Drafts`, seleccione `Read More` para volver a entrar en el modo de edición:

![edit-idea](assets/edit-idea.png)

#### Proporcionar comentarios {#providing-feedback}

Una vez publicada la idea, otros miembros pueden iniciar sesión, abrir la idea (`Read More`) y gustar la idea, agregando así al recuento de votos, y hacer comentarios.

![comentarios](assets/feedback-idea.png)

### Información adicional {#additional-information}

Encontrará más información en la página de [Ideation Essentials](/help/communities/ideation.md) para desarrolladores.

Para moderar los temas publicados y los comentarios, vea [Moderar el contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para etiquetar temas y comentarios publicados, consulte [Etiquetado de contenido generado por el usuario](/help/communities/tag-ugc.md).
