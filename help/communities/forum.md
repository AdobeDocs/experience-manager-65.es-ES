---
title: Función de foro
seo-title: Forum Feature
description: Cómo añadir y configurar la función de foro
seo-description: How to add and configure the forum feature
uuid: e69be4e1-c9d5-4d51-8e7e-609e5460e378
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d936cef5-ad76-482d-97bf-c40137185812
docset: aem65
exl-id: 2b1a4917-9db6-436a-a5fd-c102fe41fb9d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 10%

---

# Función de foro{#forum-feature}

## Introducción {#introduction}

La función de foro proporciona un área para los visitantes del sitio que han iniciado sesión (miembros de la comunidad) en el entorno de publicación para:

* Crear nuevos temas
* Ver y responder temas
* Seguir un tema
* Buscar en un foro
* Ayudar a moderar el contenido del foro
* Mover temas de foro de una página a otra

Esta sección de la documentación describe:

* Adición de la función de foro a un sitio AEM.
* Ajustes de configuración para `Forum` componente.

### Adición de un foro a una página {#adding-a-forum-to-a-page}

Para agregar un `Forum` a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Forum`

y arrástrela a su lugar en una página en la que debería aparecer el foro.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de Communities](/help/communities/basics.md).

Cuando la variable [bibliotecas requeridas del lado del cliente](/help/communities/essentials-forum.md#essentials-for-client-side) se incluyen, así es como se muestra la variable `Forum` aparecerá el componente:

![forum-component](assets/forum-component.png)

### Configuración de un foro {#configuring-a-forum}

Seleccione la colocación `Forum` para acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configure-new](assets/configure-new.png)

![forum-config](assets/forum-config.png)

#### Ficha Configuración {#settings-tab}

En el **Configuración** especifique la configuración de los temas y las respuestas:

* **Permitir la miniatura del archivo adjunto**

   Si se selecciona, se crea una miniatura de la imagen adjunta.

* **Tamaño máximo de la miniatura del archivo adjunto**

   Tamaño máximo (en píxeles) de la imagen en miniatura del archivo adjunto. El valor predeterminado es 800 x 800.

* **Tamaño mínimo de la imagen para la miniatura**
* **Tamaño máximo de la miniatura**

   Tamaño máximo (en píxeles) de la imagen en miniatura para la imagen en línea. El valor predeterminado es 800 x 800.

* **Temas por página**

   Define el número de temas/entradas que se muestran por página. El valor predeterminado es 10.

* **Moderado**

   Si se selecciona, la publicación de temas y comentarios debe aprobarse antes de que aparezcan en un sitio de publicación. El valor predeterminado no está seleccionado.

* **Cerrado**

   Si se selecciona, el foro se cierra a nuevos temas y comentarios. El valor predeterminado no está seleccionado.

* **Editor de texto enriquecido**

   Si se selecciona, los temas y comentarios se pueden introducir con marcado. El valor predeterminado no está seleccionado.

* **Permitir etiquetado**

   Si está activada, permita que los miembros agreguen etiquetas a su publicación (consulte **Campo de etiqueta** ). El valor predeterminado no está seleccionado.

* **Permitir cargas de archivos**

   Si está activada, permita que los archivos adjuntos se agreguen al tema o comentario. El valor predeterminado no está seleccionado.

* **Permitir seguimiento**

   Si está marcada esta opción, incluya la siguiente función para las publicaciones en el foro, que permite que los miembros se [notificadas](/help/communities/notifications.md) de nuevos puestos. El valor predeterminado no está seleccionado.

* **Permitir fijación**

   Si se selecciona, los temas del foro pueden colocarse en la parte superior de la lista de temas. El valor predeterminado no está seleccionado.

* **Permitir contenido destacado**

   Si se selecciona, la idea puede identificarse como [contenido destacado](/help/communities/featured.md). El valor predeterminado no está seleccionado.

* **Permitir suscripciones por correo electrónico**

   Si está activada, permita que se notifique a los miembros de los anuncios nuevos por correo electrónico ([suscripción](/help/communities/subscriptions.md)). Requiere `Allow Following` que se comprobarán y [correo electrónico configurado](/help/communities/email.md). El valor predeterminado no está seleccionado.

* **Tamaño máximo de archivo**

   Solo relevante si `Allow File Uploads` está activada. Este campo limita el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 104857600 (10 Mb).

* **Tipos de archivo permitidos**

   Solo relevante si `Allow File Uploads` está activada. Lista de extensiones de archivo separados por coma con el separador &quot;punto&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permitirá cargar aquellos que no se especifiquen. El valor predeterminado no se especifica de forma que se permitan todos los tipos de archivo.

* **Adjuntar tamaño máximo de archivo de imagen**
Solo es relevante si está marcada la opción Permitir cargas de archivos . Número máximo de bytes que puede tener un archivo de imagen cargado. El valor predeterminado es 2097152 (2 Mb).

* **Permitir respuestas de debate**

   Si está marcada esta opción, permita que se respondan a los comentarios publicados en el tema. El valor predeterminado no está seleccionado.

* **Habilitar la votación**

   Si está marcada esta opción, incluya la función Votación con un tema. El valor predeterminado no está seleccionado.

* **Permitir que los usuarios eliminen comentarios y temas**

   Si está marcada esta opción, permita que los miembros eliminen los comentarios y temas que publicaron. El valor predeterminado no está seleccionado.

* **Mostrar rutas**

   Si está activada, muestre las rutas de navegación en las páginas de temas. El valor predeterminado está marcado.

* **Mostrar insignias**

   Si está activada, muestre ganado y asignado [distintivos](/help/communities/implementing-scoring.md) con la entrada de blog de un miembro. El valor predeterminado no está seleccionado.

* **Permitir miembros privilegiados**

   Si está marcada esta opción, solo los miembros privilegiados pueden crear contenido.

* **Miembros privilegiados permitidos**

   Añada los miembros privilegiados a los que se permite crear contenido.

* **Bloquee el contenido que haya creado el usuario en el modo de edición de autor**

   Si está habilitado, bloquea el contenido generado por el usuario mientras edita en modo Autor.

* **Habilitar la mención**

   Si está habilitado, permite a los usuarios registrados de la comunidad identificar a otros miembros registrados (con el nombre, apellidos y nombre de usuario) y etiquetarlos con la sintaxis común @user-name . Los usuarios etiquetados reciben notificaciones sobre sus menciones.

* **Menciones máximas**

   Restringir el número máximo de menciones permitidas en un anuncio. El valor predeterminado es 10.

* **Patrón de menciones en la interfaz de usuario**

   Especifique la cadena de patrón permitida para etiquetar (@mention) al usuario registrado en una publicación. Por ejemplo `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Puede ser necesario comprobar ambas `AllowThreaded Replies` y `Allow users to Delete Comments and Topics` para activar los comentarios sobre un tema.

#### Pestaña Moderación del usuario {#user-moderation-tab}

En el **Moderación del usuario** especifique cómo se administran los temas publicados y las respuestas (contenido generado por el usuario). Para obtener más información, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

* **Denegar entradas**

   Si se selecciona, se permitirá a los moderadores miembros de confianza denegar publicaciones e impedir que la publicación aparezca en el foro público. El valor predeterminado no está seleccionado.

* **Cerrar/abrir de nuevo los temas**

   Si se selecciona, los moderadores miembros de confianza pueden cerrar un tema para realizar más ediciones y comentarios, y también pueden volver a abrir un tema. El valor predeterminado no está seleccionado.

* **Mover temas**

   Si está marcada esta opción, permita que los moderadores del lado de publicación movieran los temas. El valor predeterminado está marcado.

* **Marcar entradas**

   Si se selecciona, permita a los miembros marcar como inapropiados los temas o comentarios de otros. El valor predeterminado no está seleccionado.

* **Lista de motivos de indicación**

   Si está marcada esta opción, permita que los miembros elijan, desde una lista desplegable, el motivo por el que marcan un tema o comentario como inapropiado. El valor predeterminado no está seleccionado.

* **Motivo de indicación personalizado**

   Si está activada, permita que los miembros especifiquen su propio motivo para marcar un tema o comentario como inapropiado. El valor predeterminado no está seleccionado.

* **Umbral de moderación**

   Introduzca el número de veces que los miembros deben marcar un tema o comentario antes de que se notifique a los moderadores. El valor predeterminado es 1 (una vez).

* **Límite de indicación**

   Introduzca el número de veces que se debe marcar un tema o comentario antes de ocultarlo de la vista pública. Si se establece en -1, el tema o comentario marcado nunca se oculta a la vista del público. De lo contrario, este número debe ser bueno o igual al umbral de moderación. El valor predeterminado es 5.

#### Ficha Campo de etiqueta {#tag-field-tab}

En el **Campo de etiqueta** , las etiquetas que se pueden aplicar, si se permiten en la sección **Configuración** , se limitan según los espacios de nombres seleccionados.

* **Espacios de nombres permitidos**

   Pertinente si `Allow Tagging` se marca en la sección **Configuración** pestaña . Las etiquetas que se pueden aplicar se limitan a las que están dentro de las categorías de espacio de nombres seleccionadas. La lista de áreas de nombres incluye &quot;Etiquetas estándar&quot; (el espacio de nombres predeterminado) así como &quot;Incluir todas las etiquetas&quot;. El valor predeterminado es ninguno activado, lo que significa que se permiten todas las áreas de nombres.

* **Límite de sugerencias**

   Introduzca el número de etiquetas que se mostrarán como una sugerencia para el usuario que publica en el foro. El valor predeterminado es **-**1 (sin límites).

#### Ficha Traducción {#translation-tab}

En el **Traducción** , si la traducción está habilitada para el sitio de la comunidad, la traducción se puede configurar para traducir el tema completo o los anuncios seleccionados.

* **Traducir todos**

   Si se selecciona, el hilo del foro se traduce al idioma preferido del usuario. El valor predeterminado no está seleccionado.

#### Ficha Ordenar configuración {#sort-settings-tab}

En el **Configuración de ordenación** , especifique cómo se ordenan los comentarios publicados cuando se muestran.

* **Ordenar por**

   Compruebe todas las selecciones de ordenación permitidas : `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. El valor predeterminado es `Newest, Oldest, Last Updated`.

* **Establecer como predeterminado**

   Despliegue para seleccionar una de las opciones de ordenación seleccionadas que aparecerán como predeterminadas. El valor predeterminado es `Newest`.

* **Seleccione las opciones de hora para la clasificación de Analytics**

   Despliegue para seleccionar una de las siguientes opciones: `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

   El valor predeterminado es `All`.

### Información adicional {#additional-information}

Puede encontrar más información en la [Forum Essentials](/help/communities/essentials-forum.md) para desarrolladores.

Para moderar los temas y comentarios publicados, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para etiquetar temas y comentarios publicados, consulte [Etiquetado del contenido generado por el usuario](/help/communities/tag-ugc.md).

Para ver la traducción de los temas y comentarios publicados, consulte [Traducción del contenido generado por el usuario](/help/communities/translate-ugc.md).
