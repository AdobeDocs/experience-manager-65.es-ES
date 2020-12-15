---
title: Función de foro
seo-title: Función de foro
description: Cómo agregar y configurar la función de foro
seo-description: Cómo agregar y configurar la función de foro
uuid: e69be4e1-c9d5-4d51-8e7e-609e5460e378
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d936cef5-ad76-482d-97bf-c40137185812
docset: aem65
translation-type: tm+mt
source-git-commit: 871c42ee000eb250c1c6159d9a0c752e8ed4d7b8
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 10%

---


# Función de foro{#forum-feature}

## Introducción {#introduction}

La función de foro proporciona un área para los visitantes del sitio con sesión iniciada (miembros de la comunidad) en el entorno de publicación para:

* Crear nuevos temas
* Vista y respuesta a los temas
* Seguir un tema
* Buscar en un foro
* Ayudar a moderar el contenido del foro
* Mover temas de foro de una página a otra

Esta sección de la documentación describe:

* Añadir la función de foro en un sitio AEM.
* Configuración del componente `Forum`.

### Añadir un foro a una página {#adding-a-forum-to-a-page}

Para agregar un componente `Forum` a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Forum`

y arrástrelo a su lugar en una página donde debería aparecer el foro.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de comunidades](/help/communities/basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](/help/communities/essentials-forum.md#essentials-for-client-side), así es como aparecerá el componente `Forum`:

![forum-component](assets/forum-component.png)

### Configuración de un foro {#configuring-a-forum}

Seleccione el componente `Forum` colocado para acceder y seleccione el icono `Configure` que abre el cuadro de diálogo de edición.

![configure-new](assets/configure-new.png)

![forum-config](assets/forum-config.png)

#### Ficha Configuración {#settings-tab}

En la ficha **Configuración**, especifique la configuración de los temas y las respuestas:

* **Permitir la miniatura del archivo adjunto**

   Si se selecciona, se crea una miniatura de la imagen adjunta.

* **Tamaño máximo de la miniatura del archivo adjunto**

   Tamaño máximo (en píxeles) de la imagen en miniatura del archivo adjunto. El valor predeterminado es 800 x 800.

* **Tamaño mínimo de imagen para miniatura**
* **Tamaño máximo de la miniatura**

   Tamaño máximo (en píxeles) de la imagen en miniatura para la imagen en línea. El valor predeterminado es 800 x 800.

* **Temas por página**

   Define el número de temas/entradas que se muestran por página. El valor predeterminado es 10.

* **Moderado**

   Si se selecciona, la publicación de temas y comentarios debe aprobarse antes de que aparezcan en un sitio de publicación. El valor predeterminado no está marcado.

* **Cerrado**

   Si se selecciona, el foro se cierra a nuevos temas y comentarios. El valor predeterminado no está marcado.

* **Editor de texto enriquecido**

   Si se selecciona, los temas y comentarios se pueden introducir con marcado. El valor predeterminado no está marcado.

* **Permitir etiquetado**

   Si está activada, permita que los miembros agreguen etiquetas a su anuncio (consulte la ficha **Campo de etiqueta**). El valor predeterminado no está marcado.

* **Permitir cargas de archivos**

   Si está activada, permita que los archivos adjuntos se agreguen al tema o comentario. El valor predeterminado no está marcado.

* **Permitir seguimiento**

   Si se selecciona, incluya la siguiente función para las publicaciones del foro, que permite que los miembros [reciban una notificación](/help/communities/notifications.md) de las nuevas publicaciones. El valor predeterminado no está marcado.

* **Permitir fijación**

   Si se selecciona, los temas del foro pueden fijarse en la parte superior de la lista de temas. El valor predeterminado no está marcado.

* **Permitir contenido destacado**

   Si se selecciona, la idea se puede identificar como [contenido destacado](/help/communities/featured.md). El valor predeterminado no está marcado.

* **Permitir suscripciones por correo electrónico**

   Si se selecciona, permita que se notifique a los miembros de los nuevos anuncios por correo electrónico ([suscripción](/help/communities/subscriptions.md)). Requiere que `Allow Following` se compruebe y [se configure el correo electrónico](/help/communities/email.md). El valor predeterminado no está marcado.

* **Tamaño máximo de archivo**

   Solo es pertinente si se comprueba `Allow File Uploads`. Este campo limitará el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 104857600 (10 Mb).

* **Tipos de archivo permitidos**

   Solo es pertinente si se comprueba `Allow File Uploads`. Lista separada por comas de extensiones de archivo con el separador &quot;punto&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permitirá cargar los no especificados. El valor predeterminado no se especifica de forma que se permitan todos los tipos de archivo.

* **Adjuntar máximo**
tamaño de archivo de imagenRelevante solo si se ha marcado Permitir cargas de archivos. Número máximo de bytes que puede tener un archivo de imagen cargado. El valor predeterminado es 2097152 (2 Mb).

* **Permitir respuestas de debate**

   Si está activada, permita respuestas a los comentarios publicados en el tema. El valor predeterminado no está marcado.

* **Habilitar la votación**

   Si está activada, incluya la función de voto con un tema. El valor predeterminado no está marcado.

* **Permitir que los usuarios eliminen comentarios y temas**

   Si está activada, permita que los miembros eliminen los comentarios y temas que han publicado. El valor predeterminado no está marcado.

* **Mostrar rutas**

   Si se selecciona, muestre las rutas de exploración en las páginas de temas. El valor predeterminado está marcado.

* **Mostrar insignias**

   Si está marcado, muestre [distintivos](/help/communities/implementing-scoring.md) obtenidos y asignados con una entrada de blog de miembro. El valor predeterminado no está marcado.

* **Permitir miembros privilegiados**

   Si se selecciona, solo los miembros con privilegios pueden crear contenido.

* **Miembros privilegiados permitidos**

   Añada los miembros privilegiados con permiso para crear contenido.

* **Bloquee el contenido que haya creado el usuario en el modo de edición de autor**

   Si está activada, bloquea el contenido generado por el usuario mientras edita en modo de autor.

* **Habilitar la mención**

   Si está habilitada, permite que los usuarios registrados de la comunidad identifiquen a otros miembros registrados (con el nombre, apellidos y nombre de usuario) y los etiqueten con la sintaxis común @user-name. Los usuarios etiquetados reciben notificaciones sobre sus menciones.

* **Menciones máximas**

   Restringir el número máximo de menciones permitidas en una publicación. El valor predeterminado es 10.

* **Patrón de menciones en la interfaz de usuario**

   Especifique la cadena de patrón permitida para etiquetar (@mención) al usuario registrado en una publicación. Por ejemplo `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Puede que sea necesario comprobar `AllowThreaded Replies` y `Allow users to Delete Comments and Topics` para habilitar los comentarios sobre un tema.

#### Ficha Moderación del usuario {#user-moderation-tab}

En la ficha **Moderación del usuario**, especifique cómo se administran los temas publicados y las respuestas (contenido generado por el usuario). Para obtener más información, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

* **Denegar entradas**

   Si se selecciona, los moderadores miembros de confianza podrán denegar las publicaciones e impedir que aparezcan en el foro público. El valor predeterminado no está marcado.

* **Cerrar/abrir de nuevo los temas**

   Si se selecciona, los moderadores de miembros de confianza pueden cerrar un tema para realizar más ediciones y comentarios, y también pueden volver a abrir un tema. El valor predeterminado no está marcado.

* **Mover temas**

   Si está activada, permita que los moderadores del lado de publicación muevan los temas. El valor predeterminado está marcado.

* **Marcar entradas**

   Si se selecciona, permita que los miembros marquen los temas o comentarios de otros como inapropiados. El valor predeterminado no está marcado.

* **Lista de motivos de indicación**

   Si se selecciona, permita que los miembros elijan, desde una lista desplegable, el motivo por el que marcan un tema o comentario como inapropiado. El valor predeterminado no está marcado.

* **Motivo de indicación personalizado**

   Si se selecciona, permita que los miembros especifiquen su propio motivo para marcar un tema o comentario como inapropiado. El valor predeterminado no está marcado.

* **Umbral de moderación**

   Escriba el número de veces que los miembros deben marcar un tema o comentario antes de que se notifique a los moderadores. El valor predeterminado es 1 (una vez).

* **Límite de indicación**

   Introduzca el número de veces que se debe marcar un tema o comentario antes de ocultarlo en la vista pública. Si se establece en -1, el tema o comentario marcado nunca se oculta en la vista pública. De lo contrario, este número debe ser bueno o igual al umbral de moderación. El valor predeterminado es 5.

#### Ficha Campo de etiqueta {#tag-field-tab}

En la ficha **Campo de etiqueta**, las etiquetas que se pueden aplicar, si se permiten en la ficha **Configuración**, están limitadas según las Áreas de nombres elegidas.

* **Espacios de nombres permitidos**

   Relevante si `Allow Tagging` se comprueba en la ficha **Configuración**. Las etiquetas que se pueden aplicar están limitadas a las que se encuentran dentro de las categorías de Área de nombres seleccionadas. La lista de Áreas de nombres incluye &quot;Etiquetas estándar&quot; (la Área de nombres predeterminada) y &quot;Incluir todas las etiquetas&quot;. El valor predeterminado no está marcado, lo que significa que se permiten todas las Áreas de nombres.

* **Límite de sugerencias**

   Escriba el número de etiquetas que se mostrarán como una sugerencia para el miembro que se publica en el foro. El valor predeterminado es **-**1 (sin límites).

#### Ficha Traducción {#translation-tab}

En la ficha **Traducción**, si la traducción está habilitada para el sitio de la comunidad, la traducción puede configurarse para traducir el tema completo o los anuncios seleccionados.

* **Traducir todos**

   Si se selecciona, el hilo del foro se traduce al idioma preferido del usuario. El valor predeterminado no está marcado.

#### Ficha Ordenar configuración {#sort-settings-tab}

En la ficha **Ordenar configuración**, especifique cómo se ordenan los comentarios publicados cuando se muestran.

* **Ordenar por**

   Comprobar todas las selecciones de clasificación permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. El valor predeterminado es `Newest, Oldest, Last Updated`.

* **Establecer como predeterminado**

   Despliegue para seleccionar una de las opciones de ordenación seleccionadas para que aparezcan como predeterminadas. El valor predeterminado es `Newest`.

* **Seleccione las opciones de hora para la clasificación de Analytics**

   Despliegue para seleccionar una de las siguientes opciones: `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

   El valor predeterminado es `All`.

### Información adicional {#additional-information}

Puede encontrar más información en la página [Forum Essentials](/help/communities/essentials-forum.md) para desarrolladores.

Para obtener información sobre la moderación de los temas y comentarios publicados, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para etiquetar temas y comentarios publicados, consulte [Etiquetado de contenido generado por el usuario](/help/communities/tag-ugc.md).

Para obtener la traducción de los temas y comentarios publicados, consulte [Traducción de contenido generado por el usuario](/help/communities/translate-ugc.md).
