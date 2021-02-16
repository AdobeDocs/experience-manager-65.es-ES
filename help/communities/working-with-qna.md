---
title: Función de foro de preguntas y respuestas
seo-title: Función de foro de preguntas y respuestas
description: Añadir la función de foro QnA en una página
seo-description: Añadir la función de foro QnA en una página
uuid: e0d95009-0d04-4fa7-8d05-5948c4e37f08
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 6e6ffe09-c50b-4238-8b8c-597c133d0a9e
docset: aem65
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 9%

---


# Función de foro de preguntas y respuestas{#q-a-forum-feature}

## Introducción {#introduction}

La función de foro QnA (preguntas y respuestas) proporciona un área para que los miembros de la comunidad hagan y respondan preguntas. Permite a los miembros:

* Crear nuevas preguntas
* Añadir imágenes en línea (con compatibilidad para arrastrar y soltar)
* Vista y respuesta a preguntas
* Buscar una pregunta
* Ayudar a moderar el contenido de QnA
* Identifique las mejores respuestas
* Mover las preguntas de control de calidad de una página a otra

La documentación describe:

* Añadir la función de foro QnA en un sitio AEM.
* Configuración del componente `QnA`.

## Añadir un foro de preguntas y respuestas a una página {#adding-a-q-a-forum-to-a-page}

Para agregar un componente `QnA` a una página en modo de autor, utilice el navegador de componentes para ubicar `Communities / QnA` y arrástrelo a su lugar en una página donde debería aparecer el foro QnA.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de comunidades](/help/communities/basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](/help/communities/qna-essentials.md#essentials-for-client-side), así es como aparece el componente `QnA`:

![qna-component](assets/qna-component.png)

### Configuración de QnA {#configuring-qna}

Seleccione el componente `QnA` colocado para acceder y seleccione el icono `Configure` que abre el cuadro de diálogo de edición.

![configurar](assets/configure-new.png)

![qna-config](assets/qna-config.png)

#### Ficha Configuración {#settings-tab}

En la ficha **Configuración**, especifique la configuración de los temas (preguntas) y las respuestas (respuestas):

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

   Si está activada, permita que los miembros agreguen etiquetas a su anuncio (consulte la ficha **Campo de etiqueta**). El valor predeterminado no está seleccionado.

* **Permitir cargas de archivos**

   Si está activada, permita que los archivos adjuntos se agreguen a la pregunta o comentario. El valor predeterminado no está seleccionado.

* **Permitir seguimiento**

   Si se selecciona, incluya la siguiente función para las publicaciones del foro, que permite que los miembros [reciban una notificación](/help/communities/notifications.md) de las nuevas publicaciones. El valor predeterminado no está seleccionado.

* **Permitir fijación**

   Si se selecciona, los temas del foro se pueden fijar en la parte superior de la lista de temas. El valor predeterminado no está seleccionado.

* **Permitir suscripciones por correo electrónico**

   Si se selecciona, permita que se notifique a los miembros de los nuevos anuncios por correo electrónico ([suscripción](/help/communities/subscriptions.md)). Requiere permitir que se marque la opción Siguiente y [se configure el mensaje de correo electrónico](/help/communities/email.md). El valor predeterminado no está seleccionado.

* **Tamaño máximo de archivo**

   Solo es pertinente si se comprueba `Allow File Uploads`. Este campo limita el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 104857600 (10 Mb).

* **Tipos de archivo permitidos**

   Solo es pertinente si se comprueba `Allow File Uploads`. Lista separada por comas de extensiones de archivo con el separador &quot;punto&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permite cargar los no especificados. El valor predeterminado no es ninguno, por lo que se permiten** **todos los tipos de archivo.

* **Tamaño máximo de archivo de imagen adjunto**

   Solo es relevante si está activada la opción Permitir cargas de archivos. Número máximo de bytes que puede tener un archivo de imagen cargado. El valor predeterminado es 2097152 (2 Mb).

* **Permitir respuestas**

   Si está activada, permita respuestas a los comentarios publicados en la pregunta. El valor predeterminado no está seleccionado.

* **Habilitar la votación**

   Si está activada, incluya la función de voto con una pregunta. El valor predeterminado no está seleccionado.

* **Permitir que los usuarios eliminen comentarios y temas**

   Si se selecciona, permita que los miembros eliminen los comentarios y las preguntas que han publicado. El valor predeterminado no está seleccionado.

* **Permitir miembros privilegiados**

   Si se selecciona, solo los miembros con privilegios pueden crear contenido.

* **Bloquee el contenido que haya creado el usuario en el modo de edición de autor**

   Si está activada, bloquea el contenido generado por el usuario mientras edita en modo de autor.

* **Mover la respuesta seleccionada a la parte superior**

   Si se selecciona, la primera respuesta que se muestra es una respuesta seleccionada. El valor predeterminado no está seleccionado.
* **Mostrar insignias**

   Si está marcado, muestre [distintivos](/help/communities/implementing-scoring.md) obtenidos y asignados con una entrada de blog de miembro. El valor predeterminado no está seleccionado.

* **Permitir contenido destacado**

   si se selecciona, la idea puede identificarse como [contenido destacado](/help/communities/featured.md). El valor predeterminado no está seleccionado.

* **Habilitar la mención**

   Si está habilitada, permite que los usuarios registrados de la comunidad identifiquen a otros miembros registrados (con el nombre, apellidos y nombre de usuario) y los etiqueten con la sintaxis común @user-name. Los usuarios etiquetados reciben notificaciones sobre sus menciones.

* **Menciones máximas**

   Restringir el número máximo de menciones permitidas en una publicación. El valor predeterminado es 10.

* **Patrón de menciones en la interfaz de usuario**

   Especifique la cadena de patrón permitida para etiquetar (@mención) al usuario registrado en una publicación. Por ejemplo, `~{{familyName}}{{givenName}}`.

#### Ficha Moderación del usuario {#user-moderation-tab}

En la ficha **Moderación del usuario**, especifique cómo se administran los temas publicados (preguntas) y las respuestas (contenido generado por el usuario). Para obtener más información, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

* **Denegar respuestas**

   Si se selecciona, los moderadores miembros de confianza pueden denegar las respuestas publicadas y evitar que la respuesta aparezca en el foro público de preguntas y respuestas. El valor predeterminado no está seleccionado.

* **Cerrar/abrir de nuevo los temas**

   Si se selecciona, los moderadores de miembros de confianza pueden cerrar una pregunta (tema) para ediciones y respuestas adicionales, y también volver a abrir una pregunta. El valor predeterminado no está seleccionado.

* **Mover**
temasSi está activada, permita que los moderadores del lado de publicación muevan las preguntas. El valor predeterminado no está seleccionado.

* **Marcar entradas**

   Si se selecciona, permita que los miembros marquen las preguntas o respuestas de otros como inapropiadas. El valor predeterminado no está seleccionado.

* **Lista de motivos de indicación**

   Si se selecciona, permita que los miembros elijan, desde una lista desplegable, el motivo por el que marcan una pregunta o respuesta como inadecuada. El valor predeterminado no está seleccionado.

* **Motivo de indicación personalizado**

   Si se selecciona, permita que los miembros especifiquen su propio motivo para marcar una pregunta o respuesta como inapropiada. El valor predeterminado no está seleccionado.

* **Umbral de moderación**

   Introduzca el número de veces que los miembros deben marcar una pregunta o respuesta antes de que se notifique a los moderadores. El valor predeterminado es 1 (una vez).

* **Límite de indicación**

   Escriba el número de veces que se debe marcar una pregunta o respuesta antes de que se oculte en la vista pública. Si se establece en -1, la pregunta o respuesta marcada nunca se oculta en la vista pública. De lo contrario, este número debe ser bueno o igual al umbral de moderación. El valor predeterminado es 5.

#### Ficha Campo de etiqueta {#tag-field-tab}

En la ficha **Campo de etiqueta**, las etiquetas que se pueden aplicar, si se permiten en la ficha **Configuración**, están limitadas según las Áreas de nombres elegidas.

* **Espacios de nombres permitidos**

   Relevante si `Allow Tagging` está marcado en la ficha **Configuración**. Las etiquetas que se pueden aplicar están limitadas a las que se encuentran dentro de las categorías de Área de nombres seleccionadas. La lista de Áreas de nombres incluye &quot;Etiquetas estándar&quot; (la Área de nombres predeterminada) e &quot;Incluir todas las etiquetas&quot;. El valor predeterminado no está marcado, lo que significa que se permiten todas las Áreas de nombres.

* **Límite de sugerencias**

   Escriba el número de etiquetas que se mostrarán como una sugerencia para el miembro que se publica en el foro. Un valor de **-**1 significa que no hay límites. El valor predeterminado es 0.

#### Ficha Ordenar configuración {#sort-settings-tab}

En la ficha **Ordenar configuración**, especifique cómo se ordenan los comentarios publicados cuando se muestran.

* **Ordenar por**

   Marque todas las selecciones de clasificación permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. El valor predeterminado es `Newest, Oldest, Last Updated`.

* **Establecer como predeterminado**

   Despliegue para seleccionar una de las opciones de ordenación seleccionadas para que aparezcan como predeterminadas. El valor predeterminado es `Newest`.

* **Seleccione las opciones de hora para la clasificación de Analytics**

   Desplegable para seleccionar uno de `All, Last 24 Hours, Last 7 Days, Last 30 Days`. El valor predeterminado es `All`.

## Experiencia de Visitante del sitio {#site-visitor-experience}

### Identificación de respuestas {#identifying-answers}

Una respuesta se puede marcar como una respuesta correcta o útil mediante el botón `Select Answer`. Una vez que una pregunta se marca como respondida, no se puede seleccionar otra respuesta hasta que se anule la selección de la primera mediante el botón `Unmark Chosen Answer`.

Una vez seleccionada como una respuesta viable, se puede anular la selección mediante el botón `Unmark Chosen Answer`.

Una vez seleccionada una respuesta como respuesta viable, se muestra una indicación de que la pregunta se ha `Answered` junto al tema de la pregunta en la página principal de control de calidad.

#### Moderadores y administradores {#moderators-and-administrators}

Cuando el usuario que ha iniciado sesión tiene privilegios de moderador o administrador, puede realizar las tareas de moderación permitidas por la configuración del componente, independientemente de quién haya creado la pregunta o la respuesta.

También pueden identificar respuestas.

#### Miembros {#members}

Cuando los visitantes del sitio inician sesión, según la configuración, pueden:

* Publicar una nueva pregunta.
* Edite o elimine las preguntas creadas por ellos.
* Marque las preguntas o respuestas de otros miembros.
* Identifique las respuestas a las preguntas que han creado.

#### Anónimo {#anonymous}

Los visitantes del sitio que no iniciaron sesión sólo pueden leer las preguntas y respuestas publicadas, traducirlas si son compatibles, pero no pueden agregar preguntas ni respuestas, ni marcar anuncios de otros.

## Información adicional {#additional-information}

Encontrará más información en la página [QnA Essentials](/help/communities/qna-essentials.md) para desarrolladores.

Para obtener información sobre la moderación de los temas y comentarios publicados, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para etiquetar temas y comentarios publicados, consulte [Etiquetado de contenido generado por el usuario](/help/communities/tag-ugc.md).
