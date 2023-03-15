---
title: Función de foro de preguntas y respuestas
seo-title: Q&A Forum Feature
description: Añadir la función de foro de control de calidad a una página
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

La función de foro QnA (preguntas y respuestas) proporciona un área para que los miembros de la comunidad formulen y respondan preguntas. Permite a los miembros:

* Creación de nuevas preguntas
* Agregar imágenes en línea (con compatibilidad para arrastrar y soltar)
* Ver y responder preguntas
* Buscar una pregunta
* Ayuda a moderar el contenido de control de calidad
* Identificar las mejores respuestas
* Mover preguntas de control de calidad de una página a otra

La documentación describe:

* AEM Adición de la función de foro de control de calidad a un sitio de.
* Ajustes de configuración para `QnA`componente.

## Añadir un foro de preguntas y respuestas a una página {#adding-a-q-a-forum-to-a-page}

Para agregar un `QnA` a una página en modo de autor, utilice el navegador de componentes para localizar `Communities / QnA` y arrástrelo hasta su lugar en una página en la que debería aparecer el foro de control de calidad.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](/help/communities/basics.md).

Si la variable [bibliotecas requeridas del lado del cliente](/help/communities/qna-essentials.md#essentials-for-client-side) están incluidos, así es como se `QnA` el componente aparece:

![qna-component](assets/qna-component.png)

### Configuración de QnA {#configuring-qna}

Seleccione el colocado `QnA` para acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configurar](assets/configure-new.png)

![qna-config](assets/qna-config.png)

#### Pestaña Configuración {#settings-tab}

En el **Configuración** pestaña, especifique la configuración de los temas (preguntas) y respuestas (respuestas):

* **Permitir la miniatura del archivo adjunto**

   Si se selecciona, se crea una miniatura de la imagen adjunta.

* **Tamaño máximo de la miniatura del archivo adjunto**

   Tamaño máximo (en píxeles) de la imagen en miniatura del archivo adjunto. El valor predeterminado es 800 x 800.

* **Tamaño mínimo de la imagen de la miniatura**

   Tamaño mínimo (en bytes) de la imagen para generar miniaturas para imágenes alineadas. El valor predeterminado es 100000 bytes (100 kb).

* **Tamaño máximo de la miniatura**

   Tamaño máximo (en píxeles) de la imagen en miniatura para la imagen alineada. El valor predeterminado es 800 x 800.

* **Temas por página**

   Define el número de preguntas/entradas que se muestran por página. El valor predeterminado es 10.

* **Moderado**

   Si se selecciona, la publicación de temas y comentarios debe aprobarse antes de que aparezcan en un sitio de publicación. La opción predeterminada no está seleccionada.

* **Cerrado**

   Si se selecciona, el foro está cerrado a nuevas preguntas y comentarios. La opción predeterminada no está seleccionada.

* **Editor de texto enriquecido**

   Si se selecciona, los temas y los comentarios se pueden introducir con marcado. La opción predeterminada no está seleccionada.

* **Permitir etiquetado**

   Si se selecciona esta opción, permite a los miembros añadir etiquetas de etiqueta a sus publicaciones (consulte **Campo de etiqueta** pestaña). La opción predeterminada no está seleccionada.

* **Permitir cargas de archivos**

   Si se selecciona esta opción, se permite añadir archivos adjuntos a la pregunta o al comentario. La opción predeterminada no está seleccionada.

* **Permitir seguimiento**

   Si se selecciona esta opción, se incluye la siguiente función para las publicaciones del foro, que permite a los miembros [notificado](/help/communities/notifications.md) de nuevos puestos. La opción predeterminada no está seleccionada.

* **Permitir fijación**

   Si se selecciona, los temas del foro se pueden anclar al principio de la lista de temas. La opción predeterminada no está seleccionada.

* **Permitir suscripciones por correo electrónico**

   Si se selecciona esta opción, se notificará a los miembros de las nuevas publicaciones por correo electrónico ([suscripción](/help/communities/subscriptions.md)). Requiere que se compruebe Permitir seguimiento y [correo electrónico configurado](/help/communities/email.md). La opción predeterminada no está seleccionada.

* **Tamaño máximo de archivo**

   Relevante solo si `Allow File Uploads` está marcada. Este campo limita el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 104857600 (10 Mb).

* **Tipos de archivo permitidos**

   Relevante solo si `Allow File Uploads` está marcada. Lista separada por comas de las extensiones de archivo con el separador de &quot;puntos&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permite cargar los que no se hayan especificado. No se ha especificado ningún valor predeterminado de modo que ** permitan todos ** tipos de archivos.

* **Tamaño máximo de archivo de imagen adjunto**

   Solo es relevante si está marcada la opción Permitir cargas de archivos. Número máximo de bytes que puede tener un archivo de imagen cargado. El valor predeterminado es 2097152 (2 Mb).

* **Permitir respuestas**

   Si se selecciona esta opción, se permiten las respuestas a los comentarios publicados en la pregunta. La opción predeterminada no está seleccionada.

* **Habilitar la votación**

   Si se selecciona esta opción, se debe incluir la función de votación con una pregunta. La opción predeterminada no está seleccionada.

* **Permitir que los usuarios eliminen comentarios y temas**

   Si se selecciona esta opción, permite que los miembros eliminen los comentarios y las preguntas que hayan publicado. La opción predeterminada no está seleccionada.

* **Permitir miembros privilegiados**

   Si se selecciona, solo se permite a los miembros privilegiados crear contenido.

* **Bloquee el contenido que haya creado el usuario en el modo de edición de autor**

   Si está habilitado, bloquea el contenido generado por el usuario mientras lo edita en el modo Autor.

* **Mover la respuesta seleccionada a la parte superior**

   Si se selecciona, la primera respuesta que se muestra es una respuesta seleccionada. La opción predeterminada no está seleccionada.
* **Mostrar insignias**

   Si se selecciona esta opción, se muestran las ganancias y las asignaciones [distintivos](/help/communities/implementing-scoring.md) con la entrada de blog de un miembro. La opción predeterminada no está seleccionada.

* **Permitir contenido destacado**

   si se selecciona, la idea puede identificarse como [contenido destacado](/help/communities/featured.md). La opción predeterminada no está seleccionada.

* **Habilitar la mención**

   Si está habilitada, permite a los usuarios de la comunidad registrada identificar a otros miembros registrados (mediante nombre, apellidos y nombre de usuario) y etiquetarlos con la sintaxis común de @user-name. Los usuarios etiquetados reciben notificaciones sobre sus menciones.

* **Menciones máximas**

   Restringir el número máximo de menciones permitidas en una publicación. El valor predeterminado es 10.

* **Patrón de menciones en la interfaz de usuario**

   Especifique la cadena de patrón permitida para etiquetar (@mention) al usuario registrado en una publicación. Por ejemplo, `~{{familyName}}{{givenName}}`.

#### Pestaña Moderación de usuario {#user-moderation-tab}

En el **Moderación de usuario** , especifique cómo se administran los temas publicados (preguntas) y las respuestas (contenido generado por el usuario). Para obtener más información, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

* **Denegar respuestas**

   Si se selecciona, los moderadores de confianza pueden denegar las respuestas publicadas e impedir que aparezcan en el foro público de preguntas y respuestas. La opción predeterminada no está seleccionada.

* **Cerrar/abrir de nuevo los temas**

   Si se selecciona, los moderadores de miembros de confianza pueden cerrar una pregunta (tema) para realizar más ediciones y obtener respuestas, así como volver a abrir una pregunta. La opción predeterminada no está seleccionada.

* **Mover temas**
Si se selecciona, permite que los moderadores de publicación muevan preguntas. La opción predeterminada no está seleccionada.

* **Marcar entradas**

   Si se selecciona esta opción, se permite a los miembros marcar las preguntas o respuestas de otros como inadecuadas. La opción predeterminada no está seleccionada.

* **Lista de motivos de indicación**

   Si se selecciona esta opción, se permite a los miembros elegir, en una lista desplegable, el motivo por el que marcan una pregunta o respuesta como inadecuada. La opción predeterminada no está seleccionada.

* **Motivo de indicación personalizado**

   Si se selecciona esta opción, permite que los miembros especifiquen su propia razón para marcar una pregunta o respuesta como inapropiada. La opción predeterminada no está seleccionada.

* **Umbral de moderación**

   Introduzca el número de veces que los miembros deben marcar una pregunta o respuesta antes de notificarlo a los moderadores. El valor predeterminado es 1 (una vez).

* **Límite de indicación**

   Introduzca el número de veces que se debe marcar una pregunta o respuesta antes de ocultarla de la vista pública. Si se establece en -1, la pregunta o respuesta marcada nunca se oculta de la vista pública. De lo contrario, este número debe ser bueno o igual al umbral de moderación. El valor predeterminado es 5.

#### Pestaña Campo de etiqueta {#tag-field-tab}

En el **Campo de etiqueta** pestaña, las etiquetas que se pueden aplicar, si se permiten en la **Configuración** están limitadas según las áreas de nombres seleccionadas.

* **Espacios de nombres permitidos**

   Relevante si `Allow Tagging` está marcada en la **Configuración** pestaña. Las etiquetas que se pueden aplicar están limitadas a las categorías de área de nombres marcadas. La lista de áreas de nombres incluye &quot;Etiquetas estándar&quot; (el área de nombres predeterminada) e &quot;Incluir todas las etiquetas&quot;. El valor predeterminado es ninguno marcado, lo que significa que se permiten todas las áreas de nombres.

* **Límite de sugerencias**

   Introduzca el número de etiquetas que desea mostrar como sugerencia al usuario que publica en el foro. Un valor de **-**1 significa que no hay límites. El valor predeterminado es 0.

#### Pestaña Configuración de ordenación {#sort-settings-tab}

En el **Configuración de orden** , especifique cómo se ordenan los comentarios publicados cuando se muestran.

* **Ordenar por**

   Compruebe todas las selecciones de ordenación permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. El valor predeterminado es `Newest, Oldest, Last Updated`.

* **Establecer como predeterminado**

   Tire hacia abajo para seleccionar una de las opciones de ordenación seleccionadas y que aparezca como la predeterminada. El valor predeterminado es `Newest`.

* **Seleccione las opciones de hora para la clasificación de Analytics**

   Desplegable para seleccionar una de `All, Last 24 Hours, Last 7 Days, Last 30 Days`. El valor predeterminado es `All`.

## Experiencia del visitante del sitio {#site-visitor-experience}

### Identificación de respuestas {#identifying-answers}

Una respuesta se puede marcar como correcta o útil usando la variable `Select Answer` botón. Una vez que una pregunta está marcada como Respondida, no se puede seleccionar otra respuesta hasta que se haya anulado la selección de la primera con el `Unmark Chosen Answer` botón.

Una vez seleccionada como respuesta viable, se puede anular su selección con la variable `Unmark Chosen Answer` botón.

Una vez seleccionada una respuesta como respuesta viable, una indicación de que la pregunta se ha `Answered` aparece junto al tema de la pregunta en la página principal de control de calidad.

#### Moderadores y administradores {#moderators-and-administrators}

Cuando el usuario que ha iniciado sesión tiene privilegios de moderador o administrador, puede realizar las tareas de moderación permitidas por la configuración del componente, independientemente de quién haya creado la pregunta o respuesta.

También pueden identificar respuestas.

#### Miembros {#members}

Cuando los visitantes del sitio inician sesión, según la configuración, pueden:

* Publicar una nueva pregunta.
* Edite o elimine las preguntas que han creado.
* Marcar preguntas o respuestas de otros miembros.
* Identifique las respuestas a las preguntas que han creado.

#### Anónimo {#anonymous}

Los visitantes del sitio que no hayan iniciado sesión solo podrán leer las preguntas y respuestas publicadas, traducirlas si es compatible, pero no podrán añadir una pregunta o respuesta, ni marcar publicaciones de otros.

## Información adicional {#additional-information}

Encontrará más información en la [Aspectos básicos de QnA](/help/communities/qna-essentials.md) para desarrolladores.

Para ver la moderación de los temas publicados y los comentarios, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para etiquetar temas y comentarios publicados, consulte [Etiquetado del contenido generado por el usuario](/help/communities/tag-ugc.md).
