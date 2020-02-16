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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Función de foro{#forum-feature}

## Introducción {#introduction}

La función de foro proporciona un área para los visitantes del sitio con sesión iniciada (miembros de la comunidad) en el entorno de publicación para:

* crear nuevos temas
* ver y responder a temas
* seguir un tema
* buscar en un foro
* ayudar a moderar el contenido del foro
* mover temas de foro de una página a otra

Esta sección de la documentación describe

* adición de la función de foro a un sitio de AEM
* configuración del `Forum`componente

### Adding a Forum to a Page {#adding-a-forum-to-a-page}

Para agregar un `Forum` componente a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Forum`

y arrástrelo a su lugar en una página donde debería aparecer el foro.

Para obtener la información necesaria, visite [Communities Components Basics](/help/communities/basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se incluyen las bibliotecas [del lado del cliente](/help/communities/essentials-forum.md#essentials-for-client-side) necesarias, así es como aparecerá el `Forum`componente:

![chlimage_1-104](assets/chlimage_1-104.png)

### Configuración de un foro {#configuring-a-forum}

Seleccione el componente colocado al que desea acceder y seleccione el `Forum` `Configure` icono que abre el cuadro de diálogo de edición.

![chlimage_1-105](assets/chlimage_1-105.png) ![forum-config](assets/forum-config.png)

#### Ficha Configuración {#settings-tab}

En la ficha **Configuración **, especifique la configuración de los temas y las respuestas:

* **Permitir miniatura de datos adjuntos**Si está activada, se crea una miniatura de la imagen adjunta.
* **Tamaño** máximo de la miniatura de adiciónTamaño máximo (en píxeles) de la imagen en miniatura del archivo adjunto. El valor predeterminado es 800 x 800.

* **Tamaño mínimo de imagen para miniatura**
* **Tamaño** máximo de miniatura Tamaño máximo (en píxeles) de la imagen en miniatura para la imagen en línea. El valor predeterminado es 800 x 800.

* **Temas por página**Define el número de temas/publicaciones que se muestran por página. El valor predeterminado es 10.
* **Moderado** Si se selecciona, la publicación de temas y comentarios debe aprobarse antes de que aparezcan en un sitio de publicación. El valor predeterminado no está marcado.

* **Cerrado** Si está marcado, el foro está cerrado a nuevos temas y comentarios. El valor predeterminado no está marcado.

* **Editor** de texto enriquecido Si está marcado, los temas y comentarios se pueden introducir con marcado. El valor predeterminado no está marcado.

* **Permitir etiquetado** Si está activado, permita que los miembros agreguen etiquetas a su anuncio (consulte la ficha Campo **** de etiqueta). El valor predeterminado no está marcado.

* **Permitir cargas** de archivos Si está activada, permita que los archivos adjuntos se agreguen al tema o comentario. El valor predeterminado no está marcado.

* **Permitir lo siguiente** Si está marcado, incluya la siguiente función para las publicaciones del foro, que permite que se [notifique](/help/communities/notifications.md) a los miembros de las nuevas publicaciones. El valor predeterminado no está marcado.

* **Permitir fijar** si se selecciona, los temas del foro pueden fijarse en la parte superior de la lista de temas. El valor predeterminado no está marcado.

* **Si se selecciona Permitir contenido** destacado, la idea se puede identificar como contenido [](/help/communities/featured.md)destacado. El valor predeterminado no está marcado.

* **Permitir suscripciones** por correo electrónico Si está activada, permita que se notifique a los miembros de las nuevas publicaciones por correo electrónico ([suscripción](/help/communities/subscriptions.md)). Requiere `Allow Following` que se marque y se configure [el](/help/communities/email.md)correo electrónico. El valor predeterminado no está marcado.

* **Tamaño** máximo del archivo relevante solo si `Allow File Uploads` está marcado. Este campo limitará el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 104857600 (10 Mb).

* **Tipos** de archivo permitidos solo si `Allow File Uploads` está marcado. Una lista separada por comas de extensiones de archivo con el separador &quot;punto&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permitirá cargar los no especificados. El valor predeterminado no es ninguno, por lo que se permiten** **todos los tipos de archivo.

* **El tamaño** máximo del archivo de imagen adjunto solo es relevante si se ha marcado Permitir cargas de archivos. Número máximo de bytes que puede tener un archivo de imagen cargado. El valor predeterminado es 2097152*** **(2 Mb).

* **Permitir respuestas** por hilos Si está activada, permita respuestas a comentarios publicados en el tema. El valor predeterminado no está marcado.

* **Permitir voto** Si está activada, incluya la función de voto con un tema. El valor predeterminado no está marcado.

* **Permitir que los usuarios eliminen comentarios y temas** Si se selecciona esta opción, permita que los miembros eliminen los comentarios y temas que han publicado. El valor predeterminado no está marcado.

* **Mostrar rutas de exploración** Si está activada, muestre las rutas de navegación en las páginas de temas. El valor predeterminado está marcado.

* **Mostrar distintivos** Si está activada, muestre [distintivos](/help/communities/implementing-scoring.md) obtenidos y asignados con una entrada de blog de miembro. El valor predeterminado no está marcado.

* **Permitir miembros** privilegiados Si está activada, solo los miembros privilegiados pueden crear contenido.

* **Permitidos miembros privilegiados**Añada los miembros privilegiados con permiso para crear contenido.
* **Bloquear contenido generado por el usuario en modo** de edición de autor Si está activado, bloquea el contenido generado por el usuario mientras se edita en modo de autor.

* **Habilitar mención** Si está habilitada, permite que los usuarios registrados de la comunidad identifiquen a otros miembros registrados (con el nombre, apellidos y nombre de usuario) y los etiqueten con la sintaxis común @user-name. Los usuarios etiquetados reciben notificaciones sobre sus menciones.

* **Menciones** máximasRestringir el número máximo de menciones permitidas en una publicación. El valor predeterminado es 10.

* **Patrón** de mención de la interfaz de usuarioEspecifique la cadena de patrón permitida para etiquetar (@mención) al usuario registrado en una publicación. Por ejemplo `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Puede que sea necesario comprobar `AllowThreaded Replies` y `Allow users to Delete Comments and Topics` activar los comentarios sobre un tema.

#### Ficha Moderación del usuario {#user-moderation-tab}

En la ficha **Moderación del usuario **, especifique cómo se administran los temas publicados y las respuestas (contenido generado por el usuario). Para obtener más información, consulte [Moderación del contenido](/help/communities/moderate-ugc.md)generado por el usuario.

* **Denegar publicaciones** Si se selecciona, los moderadores miembros de confianza podrán denegar las publicaciones e impedir que aparezcan en el foro público. El valor predeterminado no está marcado.

* **Cerrar o volver a abrir temas** Si se selecciona, los moderadores de miembros de confianza pueden cerrar un tema para realizar más ediciones y comentarios, y también pueden volver a abrir un tema. El valor predeterminado no está marcado.

* **Mover temas** Si está activado, permita que los moderadores del lado de publicación muevan los temas. El valor predeterminado está marcado.

* **Marcar anuncios** Si está activada, permite a los miembros marcar los temas o comentarios de otros como inapropiados. El valor predeterminado no está marcado.

* **Marcar lista** de motivos Si está activada, permita que los miembros elijan, en una lista desplegable, el motivo por el que marcan un tema o comentario como inapropiado. El valor predeterminado no está marcado.

* **Razón** de marca personalizada Si está activada, permita que los miembros introduzcan su propio motivo para marcar un tema o comentario como inapropiado. El valor predeterminado no está marcado.

* **Umbral** de moderaciónIntroduzca el número de veces que los miembros deben marcar un tema o comentario antes de que se notifique a los moderadores. El valor predeterminado es 1 ( una vez).

* **Límite** de marcado Escriba el número de veces que se debe marcar un tema o comentario antes de que se oculte en la vista pública. Si se establece en -1, el tema o comentario marcado nunca se oculta en la vista pública. De lo contrario, este número debe ser mayor o igual que el umbral de moderación. El valor predeterminado es 5.

#### Ficha Campo de etiqueta {#tag-field-tab}

En la ficha Campo **** Etiqueta, las etiquetas que se pueden aplicar, si se permiten en la ficha **Configuración **ficha, están limitadas según los espacios de nombres elegidos.

* **Espacios de nombres** permitidos relevantes si `Allow Tagging` se marca en la ficha **Configuración **ficha. Las etiquetas que se pueden aplicar están limitadas a las que se encuentran dentro de las categorías de espacio de nombres seleccionadas. La lista de espacios de nombres incluye &quot;Etiquetas estándar&quot; (el espacio de nombres predeterminado) y &quot;Incluir todas las etiquetas&quot;. El valor predeterminado no está marcado, lo que significa que se permiten todos los espacios de nombres.

* **Límite** de sugerencias Introduzca el número de etiquetas que se mostrarán como una sugerencia para el miembro que se publica en el foro. El valor predeterminado es **-**1 (sin límites).

#### Ficha Traducción {#translation-tab}

En la **Traducción **ficha, si la traducción está habilitada para el sitio de la comunidad, la traducción puede configurarse para traducir el tema completo o los anuncios seleccionados.

* **Traducir todo** si está marcado, el hilo del foro se traduce al idioma preferido del usuario. El valor predeterminado no está marcado.

#### Ficha Ordenar configuración {#sort-settings-tab}

En la ficha **Ordenar configuración **, especifique cómo se ordenan los comentarios publicados cuando se muestran.

* **Ordenar por** Marcar todas las selecciones de clasificación permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. El valor predeterminado es `Newest, Oldest, Last Updated`.

* **Configure la opción Desplegable predeterminada** para seleccionar una de las opciones de ordenación seleccionadas para que aparezca como opción predeterminada. El valor predeterminado es `Newest`.

* **Seleccione Opciones de tiempo para** Desplegar clasificación de Analytics para seleccionar una de `All, Last 24 Hours, Last 7 Days, Last 30 Days`. El valor predeterminado es `All`.

### Información adicional {#additional-information}

Puede encontrar más información en la página [Forum Essentials](/help/communities/essentials-forum.md) para desarrolladores.

Para obtener información sobre la moderación de los temas y comentarios publicados, consulte [Moderación del contenido](/help/communities/moderate-ugc.md)generado por el usuario.

Para etiquetar temas y comentarios publicados, consulte [Etiquetado de contenido](/help/communities/tag-ugc.md)generado por el usuario.

Para ver la traducción de los temas y comentarios publicados, consulte [Traducción de contenido](/help/communities/translate-ugc.md)generado por el usuario.
