---
title: Función de foro de preguntas y respuestas
seo-title: Función de foro de preguntas y respuestas
description: Adición de la función de foro QnA a una página
seo-description: Adición de la función de foro QnA a una página
uuid: e0d95009-0d04-4fa7-8d05-5948c4e37f08
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 6e6ffe09-c50b-4238-8b8c-597c133d0a9e
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Función de foro de preguntas y respuestas{#q-a-forum-feature}

## Introducción {#introduction}

La función de foro QnA (preguntas y respuestas) proporciona un área para que los miembros de la comunidad hagan y respondan preguntas. Permite a los miembros:

* Crear nuevas preguntas
* Agregar imágenes en línea (con compatibilidad con arrastrar y soltar)
* Ver y responder preguntas
* Buscar una pregunta
* Ayudar a moderar el contenido de QnA
* Identifique las mejores respuestas
* Mover las preguntas de control de calidad de una página a otra

La documentación describe:

* adición de la función de foro QnA a un sitio de AEM.
* configuración del `QnA`componente.

## Adición de un foro de preguntas y respuestas a una página {#adding-a-q-a-forum-to-a-page}

Para agregar un `QnA` componente a una página en modo de autor, utilice el navegador de componentes para ubicarlo `Communities / QnA`y arrastrarlo hasta su lugar en una página en la que debería aparecer el foro de control de calidad.

Para obtener la información necesaria, visite [Communities Components Basics](/help/communities/basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se incluyen las bibliotecas [del lado del cliente](/help/communities/qna-essentials.md#essentials-for-client-side) requeridas, así es como aparece el `QnA`componente:

![chlimage_1](assets/chlimage_1.png)

### Configuración de QnA {#configuring-qna}

Seleccione el componente colocado al que desea acceder y seleccione el `QnA` `Configure` icono que abre el cuadro de diálogo de edición.

![chlimage_1-1](assets/chlimage_1-1.png) ![qna-config](assets/qna-config.png)

#### Ficha Configuración {#settings-tab}

En la ficha **Configuración** , especifique la configuración de los temas (preguntas) y las respuestas (respuestas):

* **Permitir la miniatura del archivo adjunto**

   Si se selecciona, se crea una miniatura de la imagen adjunta.

* **Tamaño máximo de la miniatura del archivo adjunto**

   Tamaño máximo (en píxeles) de la imagen en miniatura del archivo adjunto. El valor predeterminado es 800 x 800.

* **Tamaño mínimo de la imagen de la miniatura**

   Tamaño mínimo (en bytes) de la imagen para generar una miniatura para las imágenes en línea. El valor predeterminado es 100000 bytes (100 kb).

* **Tamaño máximo de la miniatura**

   Tamaño máximo (en píxeles) de la imagen en miniatura para la imagen en línea. El valor predeterminado es 800 x 800.

* **Temas por página**

   Define el número de preguntas y publicaciones que se muestran por página. El valor predeterminado es 10.

* **Moderado**

   Si se selecciona, la publicación de temas y comentarios debe aprobarse antes de que aparezcan en un sitio de publicación. El valor predeterminado no está seleccionado.

* **Cerrado**

   Si se selecciona, el foro se cierra a nuevas preguntas y comentarios. El valor predeterminado no está seleccionado.

* **Editor de texto enriquecido**

   Si se selecciona, los temas y comentarios se pueden introducir con marcado. El valor predeterminado no está seleccionado.

* **Permitir etiquetado**

   Si está activada, permita que los miembros agreguen etiquetas a su anuncio (consulte la ficha Campo **** de etiqueta). El valor predeterminado no está seleccionado.

* **Permitir cargas de archivos**

   Si está activada, permita que los archivos adjuntos se agreguen a la pregunta o comentario. El valor predeterminado no está seleccionado.

* **Permitir seguimiento**

   Si está activada, incluya la siguiente función para las publicaciones del foro, que permite que se [notifique](/help/communities/notifications.md) a los miembros de las nuevas publicaciones. El valor predeterminado no está seleccionado.

* **Permitir fijación**

   Si se selecciona, los temas del foro se pueden fijar en la parte superior de la lista de temas. El valor predeterminado no está seleccionado.

* **Permitir suscripciones por correo electrónico**

   Si está activada, permita que se notifique a los miembros de los anuncios nuevos por correo electrónico ([suscripción](/help/communities/subscriptions.md)). Requiere permitir que se marque la opción Seguir y se configure [el](/help/communities/email.md)correo electrónico. El valor predeterminado no está seleccionado.

* **Tamaño máximo de archivo**

   Solo es pertinente si `Allow File Uploads` está marcado. Este campo limita el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 104857600 (10 Mb).

* **Tipos de archivo permitidos**

   Solo es pertinente si `Allow File Uploads` está marcado. Una lista separada por comas de extensiones de archivo con el separador &quot;punto&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permite cargar los no especificados. El valor predeterminado no es ninguno, por lo que se permiten** **todos los tipos de archivo.

* **Tamaño máximo de archivo de imagen adjunto**

   Solo es relevante si está activada la opción Permitir cargas de archivos. Número máximo de bytes que puede tener un archivo de imagen cargado. El valor predeterminado es 2097152*** **(2 Mb).

* **Permitir respuestas**

   Si está activada, permita respuestas a los comentarios publicados en la pregunta. El valor predeterminado no está seleccionado.
* **Habilitar la votación**

   Si está activada, incluya la función de voto con una pregunta. El valor predeterminado no está seleccionado.

* **Permitir que los usuarios eliminen comentarios y temas**

   Si se selecciona, permita que los miembros eliminen los comentarios y las preguntas que han publicado. El valor predeterminado es** **sin seleccionar.

* **Permitir miembros privilegiados**

   Si se selecciona, solo los miembros con privilegios pueden crear contenido.

* **Bloquee el contenido que haya creado el usuario en el modo de edición de autor**

   Si está activada, bloquea el contenido generado por el usuario mientras edita en modo de autor.

* **Mover la respuesta seleccionada a la parte superior**Si está activada, la primera respuesta que se muestra es una respuesta seleccionada. El valor predeterminado no está seleccionado.
* **Mostrar insignias**

   Si está activada, muestre [los distintivos](/help/communities/implementing-scoring.md) obtenidos y asignados con una entrada de blog de miembro. El valor predeterminado no está seleccionado.

* **Permitir contenido destacado**

   si se selecciona, la idea se puede identificar como contenido [](/help/communities/featured.md)destacado. El valor predeterminado no está seleccionado.

* **Habilitar la mención**

   Si está habilitada, permite que los usuarios registrados de la comunidad identifiquen a otros miembros registrados (con el nombre, apellidos y nombre de usuario) y los etiqueten con la sintaxis común @user-name. Los usuarios etiquetados reciben notificaciones sobre sus menciones.

* **Menciones máximas**

   Restringir el número máximo de menciones permitidas en una publicación. El valor predeterminado es 10.

* **Patrón de menciones en la interfaz de usuario**

   Especifique la cadena de patrón permitida para etiquetar (@mención) al usuario registrado en una publicación. Por ejemplo, ~{{familyName}}{{givenName}}.

#### Ficha Moderación del usuario {#user-moderation-tab}

En la ficha Moderación **del** usuario, especifique cómo se administran los temas publicados (preguntas) y las respuestas (contenido generado por el usuario). Para obtener más información, consulte [Moderación del contenido](/help/communities/moderate-ugc.md)generado por el usuario.

* **Denegar respuestas**

   Si se selecciona, los moderadores miembros de confianza pueden denegar las respuestas publicadas y evitar que la respuesta aparezca en el foro público de preguntas y respuestas. El valor predeterminado no está seleccionado.

* **Cerrar/abrir de nuevo los temas**

   Si se selecciona, los moderadores de miembros de confianza pueden cerrar una pregunta (tema) para ediciones y respuestas adicionales, y también volver a abrir una pregunta. El valor predeterminado no está seleccionado.

* **Mover temas** Si está activado, permita que los moderadores del lado de publicación muevan las preguntas. El valor predeterminado no está seleccionado.

* **Marcar entradas**

   Si se selecciona, permita que los miembros marquen las preguntas o respuestas de otros como inapropiadas. El valor predeterminado no está seleccionado.

* **Lista de motivos de indicación**

   Si se selecciona, permita que los miembros elijan, en una lista desplegable, el motivo por el que marcan una pregunta o una respuesta como inadecuada. El valor predeterminado no está seleccionado.

* **Motivo de indicación personalizado**

   Si se selecciona, permita que los miembros especifiquen su propio motivo para marcar una pregunta o respuesta como inapropiada. El valor predeterminado no está seleccionado.

* **Umbral de moderación**

   Escriba el número de veces que los miembros deben marcar una pregunta o respuesta antes de que se notifique a los moderadores. El valor predeterminado es 1 ( una vez).

* **Límite de indicación**

   Escriba el número de veces que se debe marcar una pregunta o respuesta antes de que se oculte de la vista pública. Si se establece en -1, la pregunta o respuesta marcada nunca se oculta en la vista pública. De lo contrario, este número debe ser mayor o igual que el umbral de moderación. El valor predeterminado es 5.

#### Ficha Campo de etiqueta {#tag-field-tab}

En la ficha Campo **** Etiqueta, las etiquetas que se pueden aplicar, si se permiten en la ficha **Configuración **ficha, están limitadas según los espacios de nombres elegidos.

* **Espacios de nombres** permitidos relevantes si `Allow Tagging` se marca en la ficha **Configuración **ficha. Las etiquetas que se pueden aplicar están limitadas a las que se encuentran dentro de las categorías de espacio de nombres seleccionadas. La lista de espacios de nombres incluye &quot;Etiquetas estándar&quot; (el espacio de nombres predeterminado) y &quot;Incluir todas las etiquetas&quot;. El valor predeterminado no está marcado, lo que significa que se permiten todos los espacios de nombres.

* **Límite** de sugerencias Introduzca el número de etiquetas que se mostrarán como una sugerencia para el miembro que se publica en el foro. Un valor de **-**1 significa que no hay límites. El valor predeterminado es 0.

#### Ficha Ordenar configuración {#sort-settings-tab}

En la ficha **Ordenar configuración** , especifique cómo se ordenan los comentarios publicados cuando se muestran.

* **Ordenar por**

   Marque todas las selecciones de clasificación permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. El valor predeterminado es `Newest, Oldest, Last Updated`.

* **Establecer como predeterminado**

   Despliegue para seleccionar una de las opciones de ordenación seleccionadas para que aparezcan como predeterminadas. El valor predeterminado es `Newest`.

* **Seleccione las opciones de hora para la clasificación de Analytics**

   Desplegable para seleccionar uno de `All, Last 24 Hours, Last 7 Days, Last 30 Days`. El valor predeterminado es `All`.

## Experiencia del visitante del sitio {#site-visitor-experience}

### Identificación de respuestas {#identifying-answers}

Una respuesta se puede marcar como una respuesta correcta o útil mediante el `Select Answer` botón. Una vez que una pregunta se marca como respondida, no se puede seleccionar otra respuesta hasta que se anule la selección de la primera mediante el `Unmark Chosen Answer`botón.

Una vez seleccionada como una respuesta viable, se puede anular la selección mediante el `Unmark Chosen Answer` botón.

Una vez seleccionada una respuesta como respuesta viable, `Answered`se muestra una indicación de que la pregunta se ha mostrado junto al tema de la pregunta en la página principal de control de calidad.

#### Moderadores y administradores {#moderators-and-administrators}

Cuando el usuario que ha iniciado sesión tiene privilegios de moderador o administrador, puede realizar las tareas de moderación permitidas por la configuración del componente, independientemente de quién haya creado la pregunta o la respuesta.

También pueden identificar respuestas.

#### Miembros {#members}

Cuando los visitantes del sitio inician sesión, según la configuración, pueden:

* publicar una nueva pregunta.
* edite o elimine las preguntas que hayan creado.
* marcar preguntas o respuestas de otros miembros.
* identifique las respuestas a las preguntas que han creado.

#### Anónimo {#anonymous}

Los visitantes del sitio que no iniciaron sesión sólo pueden leer las preguntas y respuestas publicadas, traducirlas si son compatibles, pero no pueden agregar preguntas ni respuestas, ni marcar anuncios de otros.

## Información adicional {#additional-information}

Puede encontrar más información en la página de [QnA Essentials](/help/communities/qna-essentials.md) para desarrolladores.

Para obtener información sobre la moderación de los temas y comentarios publicados, consulte [Moderación del contenido](/help/communities/moderate-ugc.md)generado por el usuario.

Para etiquetar temas y comentarios publicados, consulte [Etiquetado de contenido](/help/communities/tag-ugc.md)generado por el usuario.
