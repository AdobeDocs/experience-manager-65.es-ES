---
title: Función de foro de preguntas y respuestas
seo-title: Q&A Forum Feature
description: Adición de la función de foro QnA a una página
seo-description: Adding the QnA forum feature to a page
uuid: e0d95009-0d04-4fa7-8d05-5948c4e37f08
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 6e6ffe09-c50b-4238-8b8c-597c133d0a9e
docset: aem65
exl-id: 17081710-35e0-4f5b-9485-1f85c065fd70
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1368'
ht-degree: 9%

---

# Función de foro de preguntas y respuestas{#q-a-forum-feature}

## Introducción {#introduction}

La función de foro QnA (preguntas y respuestas) proporciona un área para que los miembros de la comunidad hagan y respondan preguntas. Permite a los miembros:

* Crear nuevas preguntas
* Agregar imágenes en línea (con compatibilidad para arrastrar y soltar)
* Ver y responder preguntas
* Buscar una pregunta
* Ayudar a moderar el contenido de control de calidad
* Identificar las mejores respuestas
* Mover preguntas de control de calidad de una página a otra

La documentación describe:

* Añadir la función de foro QnA a un sitio AEM.
* Ajustes de configuración para `QnA`componente.

## Adición de un foro de preguntas y respuestas a una página {#adding-a-q-a-forum-to-a-page}

Para agregar un `QnA` a una página en modo de autor, utilice el navegador de componentes para localizar `Communities / QnA` y arrástrela a su lugar en una página donde debería aparecer el foro QnA.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de Communities](/help/communities/basics.md).

Cuando la variable [bibliotecas requeridas del lado del cliente](/help/communities/qna-essentials.md#essentials-for-client-side) se incluyen, así es como se muestra la variable `QnA` aparece el componente:

![qna-component](assets/qna-component.png)

### Configuración de QnA {#configuring-qna}

Seleccione la colocación `QnA` para acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configure](assets/configure-new.png)

![qna-config](assets/qna-config.png)

#### Ficha Configuración {#settings-tab}

En el **Configuración** , especifique la configuración para los temas (preguntas) y las respuestas (respuestas):

* **Permitir la miniatura del archivo adjunto**

   Si se selecciona, se crea una miniatura de la imagen adjunta.

* **Tamaño máximo de la miniatura del archivo adjunto**

   Tamaño máximo (en píxeles) de la imagen en miniatura del archivo adjunto. El valor predeterminado es 800 x 800.

* **Tamaño mínimo de la imagen de la miniatura**

   Tamaño mínimo (en bytes) de la imagen para generar miniaturas para imágenes en línea. El valor predeterminado es 100000 bytes (100 kb).

* **Tamaño máximo de la miniatura**

   Tamaño máximo (en píxeles) de la imagen en miniatura para imagen en línea. El valor predeterminado es 800 x 800.

* **Temas por página**

   Define el número de preguntas/anuncios que se muestran por página. El valor predeterminado es 10.

* **Moderado**

   Si se selecciona, la publicación de temas y comentarios debe aprobarse antes de que aparezcan en un sitio de publicación. El valor predeterminado no está seleccionado.

* **Cerrado**

   Si se selecciona, el foro se cierra a nuevas preguntas y comentarios. El valor predeterminado no está seleccionado.

* **Editor de texto enriquecido**

   Si se selecciona, los temas y comentarios se pueden introducir con marcado. El valor predeterminado no está seleccionado.

* **Permitir etiquetado**

   Si está activada, permita que los miembros agreguen etiquetas a su publicación (consulte **Campo de etiqueta** ). El valor predeterminado no está seleccionado.

* **Permitir cargas de archivos**

   Si está activada, permita que los archivos adjuntos se agreguen a la pregunta o comentario. El valor predeterminado no está seleccionado.

* **Permitir seguimiento**

   Si está marcada esta opción, incluya la siguiente función para las publicaciones en el foro, que permite que los miembros se [notificadas](/help/communities/notifications.md) de nuevos puestos. El valor predeterminado no está seleccionado.

* **Permitir fijación**

   Si se selecciona, los temas del foro se pueden fijar en la parte superior de la lista de temas. El valor predeterminado no está seleccionado.

* **Permitir suscripciones por correo electrónico**

   Si está activada, permita que se notifique a los miembros de los anuncios nuevos por correo electrónico ([suscripción](/help/communities/subscriptions.md)). Requiere permitir que se verifique y [correo electrónico configurado](/help/communities/email.md). El valor predeterminado no está seleccionado.

* **Tamaño máximo de archivo**

   Solo relevante si `Allow File Uploads` está activada. Este campo limita el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 104857600 (10 Mb).

* **Tipos de archivo permitidos**

   Solo relevante si `Allow File Uploads` está activada. Lista de extensiones de archivo separados por coma con el separador &quot;punto&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permite cargar aquellos que no se hayan especificado. El valor predeterminado no se especifica de forma que se permitan** **todos los tipos de archivo.

* **Tamaño máximo de archivo de imagen adjunto**

   Solo es relevante si está marcada la opción Permitir cargas de archivos . Número máximo de bytes que puede tener un archivo de imagen cargado. El valor predeterminado es 2097152 (2 Mb).

* **Permitir respuestas**

   Si está activada, permita que se respondan a los comentarios publicados en la pregunta. El valor predeterminado no está seleccionado.

* **Habilitar la votación**

   Si está marcada esta opción, incluya la función Votación con una pregunta. El valor predeterminado no está seleccionado.

* **Permitir que los usuarios eliminen comentarios y temas**

   Si está activada, permita que los miembros eliminen los comentarios y preguntas que hayan publicado. El valor predeterminado no está seleccionado.

* **Permitir miembros privilegiados**

   Si está marcada esta opción, solo los miembros privilegiados pueden crear contenido.

* **Bloquee el contenido que haya creado el usuario en el modo de edición de autor**

   Si está habilitado, bloquea el contenido generado por el usuario mientras edita en modo Autor.

* **Mover la respuesta seleccionada a la parte superior**

   Si se selecciona, la primera respuesta que se muestra es una respuesta seleccionada. El valor predeterminado no está seleccionado.
* **Mostrar insignias**

   Si está activada, muestre ganado y asignado [distintivos](/help/communities/implementing-scoring.md) con la entrada de blog de un miembro. El valor predeterminado no está seleccionado.

* **Permitir contenido destacado**

   si se selecciona, la idea puede identificarse como [contenido destacado](/help/communities/featured.md). El valor predeterminado no está seleccionado.

* **Habilitar la mención**

   Si está habilitado, permite a los usuarios registrados de la comunidad identificar a otros miembros registrados (con el nombre, apellidos y nombre de usuario) y etiquetarlos con la sintaxis común @user-name . Los usuarios etiquetados reciben notificaciones sobre sus menciones.

* **Menciones máximas**

   Restringir el número máximo de menciones permitidas en un anuncio. El valor predeterminado es 10.

* **Patrón de menciones en la interfaz de usuario**

   Especifique la cadena de patrón permitida para etiquetar (@mention) al usuario registrado en una publicación. Por ejemplo, `~{{familyName}}{{givenName}}`.

#### Pestaña Moderación del usuario {#user-moderation-tab}

En el **Moderación del usuario** especifique cómo se administran los temas publicados (preguntas) y las respuestas (contenido generado por el usuario). Para obtener más información, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

* **Denegar respuestas**

   Si se selecciona, los moderadores miembros de confianza pueden denegar las respuestas publicadas y evitar que la respuesta aparezca en el foro público de preguntas y respuestas. El valor predeterminado no está seleccionado.

* **Cerrar/abrir de nuevo los temas**

   Si se selecciona, los moderadores miembros de confianza pueden cerrar una pregunta (tema) para ediciones y respuestas adicionales, y también volver a abrir una pregunta. El valor predeterminado no está seleccionado.

* **Mover temas**
Si está marcada esta opción, permita que los moderadores del lado de publicación movieran las preguntas. El valor predeterminado no está seleccionado.

* **Marcar entradas**

   Si se selecciona, permita a los miembros marcar las preguntas o respuestas de otros como inapropiadas. El valor predeterminado no está seleccionado.

* **Lista de motivos de indicación**

   Si está activada, permita que los miembros elijan, desde una lista desplegable, el motivo por el que marcan una pregunta o respuesta como inadecuada. El valor predeterminado no está seleccionado.

* **Motivo de indicación personalizado**

   Si se selecciona, permita a los miembros introducir sus propios motivos para marcar una pregunta o respuesta como inapropiada. El valor predeterminado no está seleccionado.

* **Umbral de moderación**

   Introduzca el número de veces que los miembros deben marcar una pregunta o respuesta antes de que se notifique a los moderadores. El valor predeterminado es 1 (una vez).

* **Límite de indicación**

   Introduzca el número de veces que se debe marcar una pregunta o respuesta antes de ocultarla de la vista pública. Si se establece en -1, la pregunta o respuesta marcada nunca se oculta a la vista del público. De lo contrario, este número debe ser bueno o igual al umbral de moderación. El valor predeterminado es 5.

#### Ficha Campo de etiqueta {#tag-field-tab}

En el **Campo de etiqueta** , las etiquetas que se pueden aplicar, si se permiten en la sección **Configuración** , se limitan según los espacios de nombres seleccionados.

* **Espacios de nombres permitidos**

   Pertinente si `Allow Tagging` se marca en la sección **Configuración** pestaña . Las etiquetas que se pueden aplicar se limitan a las que están dentro de las categorías de espacio de nombres seleccionadas. La lista de áreas de nombres incluye &quot;Etiquetas estándar&quot; (el espacio de nombres predeterminado) e &quot;Incluir todas las etiquetas&quot;. El valor predeterminado es ninguno activado, lo que significa que se permiten todas las áreas de nombres.

* **Límite de sugerencias**

   Introduzca el número de etiquetas que se mostrarán como una sugerencia para el usuario que publica en el foro. Un valor de **-**1 significa que no hay límites. El valor predeterminado es 0.

#### Ficha Ordenar configuración {#sort-settings-tab}

En el **Configuración de ordenación** , especifique cómo se ordenan los comentarios publicados cuando se muestran.

* **Ordenar por**

   Compruebe todas las selecciones de ordenación permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. El valor predeterminado es `Newest, Oldest, Last Updated`.

* **Establecer como predeterminado**

   Despliegue para seleccionar una de las opciones de ordenación seleccionadas que aparecerán como predeterminadas. El valor predeterminado es `Newest`.

* **Seleccione las opciones de hora para la clasificación de Analytics**

   Desplegable para seleccionar uno de `All, Last 24 Hours, Last 7 Days, Last 30 Days`. El valor predeterminado es `All`.

## Experiencia del visitante del sitio {#site-visitor-experience}

### Identificación de respuestas {#identifying-answers}

Una respuesta puede marcarse como una respuesta correcta o útil utilizando la variable `Select Answer` botón. Una vez que una pregunta está marcada como Respondida, no se puede seleccionar otra respuesta hasta que se anula la selección de la primera mediante la función `Unmark Chosen Answer` botón.

Una vez seleccionada como respuesta viable, se puede anular la selección utilizando la variable `Unmark Chosen Answer` botón.

Una vez seleccionada la respuesta como respuesta viable, una indicación de que la pregunta se ha `Answered` se muestra junto al tema de la pregunta en la página de control de calidad principal.

#### Moderadores y administradores {#moderators-and-administrators}

Cuando el usuario que ha iniciado sesión tiene privilegios de moderador o administrador, puede realizar las tareas de moderación permitidas por la configuración del componente, independientemente de quién haya creado la pregunta o la respuesta.

También pueden identificar respuestas.

#### Miembros {#members}

Cuando los visitantes del sitio inician sesión, según la configuración, pueden:

* Publicar una nueva pregunta.
* Edite o elimine las preguntas que hayan creado.
* Indicar preguntas o respuestas de otros miembros.
* Identifique respuestas para preguntas creadas por ellos.

#### Anónimo {#anonymous}

Los visitantes del sitio que no hayan iniciado sesión solo podrán leer las preguntas y respuestas publicadas, traducirlas si son compatibles, pero no podrán agregar preguntas ni respuestas, ni marcar publicaciones de otros.

## Información adicional {#additional-information}

Puede encontrar más información en la [Aspectos básicos de la garantía de calidad](/help/communities/qna-essentials.md) para desarrolladores.

Para moderar los temas y comentarios publicados, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para etiquetar temas y comentarios publicados, consulte [Etiquetado del contenido generado por el usuario](/help/communities/tag-ugc.md).
