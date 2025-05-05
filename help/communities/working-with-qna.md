---
title: Función de foro de preguntas y respuestas
description: Aprenda a añadir la función de foro de control de calidad a una página que permite a los miembros de la comunidad que iniciaron sesión hacer y responder preguntas.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 17081710-35e0-4f5b-9485-1f85c065fd70
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 0%

---

# Función de foro de preguntas y respuestas{#q-a-forum-feature}

## Introducción {#introduction}

La función de foro QnA (preguntas y respuestas) proporciona un área para que los miembros de la comunidad formulen y respondan preguntas. Permite a los miembros:

* Creación de preguntas
* Agregar imágenes en línea (con compatibilidad para arrastrar y soltar)
* Ver y responder preguntas
* Buscar una pregunta
* Ayuda a moderar el contenido de control de calidad
* Identificar las mejores respuestas
* Mover preguntas de control de calidad de una página a otra

La documentación describe:

* AEM Adición de la función de foro de control de calidad a un sitio de.
* Ajustes de configuración para el componente `QnA`.

## Añadir un foro de preguntas y respuestas a una página {#adding-a-q-a-forum-to-a-page}

Para agregar un componente `QnA` a una página en modo de autor, use el explorador de componentes para localizar `Communities / QnA` y arrástrelo a su lugar en una página en la que debería aparecer el foro de control de calidad.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](/help/communities/basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](/help/communities/qna-essentials.md#essentials-for-client-side), así es como aparece el componente `QnA`:

![componente qna](assets/qna-component.png)

### Configuración de QnA {#configuring-qna}

Seleccione el componente `QnA` colocado para que pueda acceder y seleccionar el icono `Configure` que abre el cuadro de diálogo de edición.

![configurar](assets/configure-new.png)

![qna-config](assets/qna-config.png)

#### Pestaña Configuración {#settings-tab}

En la ficha **Configuración**, especifique la configuración para los temas (preguntas) y las respuestas (respuestas):

* **Permitir miniatura de datos adjuntos**

  Si se selecciona, se crea una miniatura de la imagen adjunta.

* **Tamaño máximo de miniatura adjunta**

  Tamaño máximo (en píxeles) de la imagen en miniatura del archivo adjunto. El valor predeterminado es 800 x 800.

* **Tamaño mínimo de imagen para la miniatura**

  Tamaño mínimo (en bytes) de la imagen para generar miniaturas para imágenes alineadas. El valor predeterminado es 100000 bytes (100 kb).

* **Tamaño máximo de miniatura**

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

  Si se selecciona esta opción, se permite a los miembros agregar etiquetas de etiqueta a sus publicaciones (consulte **Campo de etiqueta** en la pestaña). La opción predeterminada no está seleccionada.

* **Permitir cargas de archivos**

  Si se selecciona esta opción, se permite añadir archivos adjuntos a la pregunta o al comentario. La opción predeterminada no está seleccionada.

* **Permitir seguimiento**

  Si se selecciona esta opción, se debe incluir la siguiente característica para las publicaciones del foro, que permite [notificar](/help/communities/notifications.md) a los miembros las nuevas publicaciones. La opción predeterminada no está seleccionada.

* **Permitir anclaje**

  Si se selecciona, los temas del foro se pueden anclar al principio de la lista de temas. La opción predeterminada no está seleccionada.

* **Permitir suscripciones por correo electrónico**

  Si se selecciona esta opción, se notificarán las nuevas publicaciones a los miembros por correo electrónico ([suscripción](/help/communities/subscriptions.md)). Requiere que se compruebe Permitir seguimiento y que se configure [correo electrónico](/help/communities/email.md). La opción predeterminada no está seleccionada.

* **Tamaño máximo de archivo**

  Relevante solo si `Allow File Uploads` está marcado. Este campo limita el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 104857600 (10 Mb).

* **Tipos de archivo permitidos**

  Relevante solo si `Allow File Uploads` está marcado. Lista separada por comas de las extensiones de archivo con el separador de &quot;puntos&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se podrán cargar los que no se hayan especificado. El valor predeterminado no se ha especificado, de modo que se permiten **todos los** tipos de archivo.

* **Tamaño máximo de archivo de imagen adjunto**

  Solo es relevante si está marcada la opción Permitir cargas de archivos. Número máximo de bytes que puede tener un archivo de imagen cargado. El valor predeterminado es 2097152 (2 Mb).

* **Permitir respuestas**

  Si se selecciona esta opción, se permiten las respuestas a los comentarios publicados en la pregunta. La opción predeterminada no está seleccionada.

* **Permitir Votación**

  Si se selecciona esta opción, se debe incluir la función de votación con una pregunta. La opción predeterminada no está seleccionada.

* **Permitir que los usuarios eliminen comentarios y temas**

  Si se selecciona esta opción, permite que los miembros eliminen los comentarios y las preguntas que hayan publicado. La opción predeterminada no está seleccionada.

* **Permitir miembros privilegiados**

  Si se selecciona, solo se permite a los miembros privilegiados crear contenido.

* **Bloquear contenido generado por el usuario en el modo de edición de autor**

  Si está habilitado, bloquea el contenido generado por el usuario mientras lo edita en el modo Autor.

* **Mover la respuesta seleccionada al principio**

  Si se selecciona, la primera respuesta que se muestra es una respuesta seleccionada. La opción predeterminada no está seleccionada.
* **Mostrar insignias**

  Si se selecciona esta opción, se muestran [insignias](/help/communities/implementing-scoring.md) ganadas y asignadas con la entrada de blog de un miembro. La opción predeterminada no está seleccionada.

* **Permitir contenido destacado**

  Si se selecciona, la idea se puede identificar como [contenido destacado](/help/communities/featured.md). La opción predeterminada no está seleccionada.

* **Habilitar la mención**

  Si está habilitada, permite a los usuarios de la comunidad registrada identificar a otros miembros registrados (mediante nombre, apellidos y nombre de usuario) y etiquetarlos con la sintaxis común de @user-name. Los usuarios etiquetados reciben notificaciones sobre sus menciones.

* **Menciones máximas**

  Restringir el número máximo de menciones permitidas en una publicación. El valor predeterminado es 10.

* **Patrón de mención de IU**

  Especifique la cadena de patrón permitida para etiquetar (@mention) al usuario registrado en una publicación. Por ejemplo, `~{{familyName}}{{givenName}}`.

#### Pestaña Moderación de usuario {#user-moderation-tab}

En la ficha **Moderación de usuarios** especifique cómo se administran los temas publicados (preguntas) y las respuestas (contenido generado por el usuario). Para obtener más información, consulte [Moderar contenido generado por el usuario](/help/communities/moderate-ugc.md).

* **Denegar respuestas**

  Si se selecciona, los moderadores de confianza pueden denegar las respuestas publicadas e impedir que aparezcan en el foro público de preguntas y respuestas. La opción predeterminada no está seleccionada.

* **Cerrar/volver a abrir temas**

  Si se selecciona, los moderadores de miembros de confianza pueden cerrar una pregunta (tema) para realizar más ediciones y obtener respuestas, así como volver a abrir una pregunta. La opción predeterminada no está seleccionada.

* **Mover temas**
Si se selecciona, permite que los moderadores de publicación muevan preguntas. La opción predeterminada no está seleccionada.

* **Marcar entradas**

  Si se selecciona esta opción, se permite a los miembros marcar las preguntas o respuestas de otros como inadecuadas. La opción predeterminada no está seleccionada.

* **Lista de motivos de marca**

  Si se selecciona esta opción, se permite a los miembros elegir, en una lista desplegable, el motivo por el que marcan una pregunta o respuesta como inadecuada. La opción predeterminada no está seleccionada.

* **Motivo de indicación personalizado**

  Si se selecciona esta opción, permite que los miembros especifiquen su propia razón para marcar una pregunta o respuesta como inapropiada. La opción predeterminada no está seleccionada.

* **Umbral de moderación**

  Introduzca el número de veces que los miembros deben marcar una pregunta o respuesta antes de notificarlo a los moderadores. El valor predeterminado es 1 (una vez).

* **Límite de indicación**

  Introduzca el número de veces que se debe marcar una pregunta o respuesta antes de ocultarla de la vista pública. Si se establece en -1, la pregunta o respuesta marcada nunca se oculta de la vista pública. De lo contrario, este número debe ser mayor o igual que el umbral de moderación. El valor predeterminado es 5.

#### Pestaña Campo de etiqueta {#tag-field-tab}

En la ficha **Campo de etiqueta**, las etiquetas que se pueden aplicar, si se permiten en la ficha **Configuración**, están limitadas según las áreas de nombres elegidas.

* **Áreas de nombres permitidas**

  Relevante si `Allow Tagging` está marcado en la ficha **Configuración**. Las etiquetas que se pueden aplicar están limitadas a las categorías de área de nombres marcadas. La lista de áreas de nombres incluye &quot;Etiquetas estándar&quot; (el área de nombres predeterminada) e &quot;Incluir todas las etiquetas&quot;. El valor predeterminado es ninguno marcado, lo que significa que se permiten todas las áreas de nombres.

* **Límite de sugerencias**

  Introduzca el número de etiquetas que desea mostrar como sugerencia al usuario que publica en el foro. Un valor de **-**&#x200B;1 significa que no hay límites. El valor predeterminado es 0.

#### Pestaña Configuración de ordenación {#sort-settings-tab}

En la ficha **Configuración de ordenación**, especifique cómo se ordenan los comentarios publicados cuando se muestran.

* **Ordenar por**

  Compruebe todas las selecciones de ordenación permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. El valor predeterminado es `Newest, Oldest, Last Updated`.

* **Establecer como predeterminado**

  Tire hacia abajo para seleccionar una de las opciones de ordenación seleccionadas y que aparezca como la predeterminada. El valor predeterminado es `Newest`.

* **Seleccionar opciones de hora para la ordenación de Analytics**

  Lista desplegable para seleccionar uno de `All, Last 24 Hours, Last 7 Days, Last 30 Days`. El valor predeterminado es `All`.

## Experiencia del visitante del sitio {#site-visitor-experience}

### Identificación de respuestas {#identifying-answers}

Una respuesta se puede marcar como correcta o útil usando el botón `Select Answer`. Una vez que una pregunta está marcada como Respondida, no se puede seleccionar otra respuesta hasta que se haya anulado la selección de la primera con el botón `Unmark Chosen Answer`.

Una vez seleccionada como respuesta viable, se puede anular su selección con el botón `Unmark Chosen Answer`.

Una vez que se selecciona una respuesta como respuesta viable, se muestra una indicación de que la pregunta ha sido `Answered` junto al tema de la pregunta en la página principal de control de calidad.

#### Moderadores y administradores {#moderators-and-administrators}

Cuando el usuario que ha iniciado sesión tiene privilegios de moderador o administrador, puede realizar las tareas de moderación permitidas por la configuración del componente, independientemente de quién haya creado la pregunta o respuesta.

También pueden identificar respuestas.

#### Miembros {#members}

Cuando los visitantes del sitio inician sesión, según la configuración, pueden:

* Post tiene una nueva pregunta.
* Edite o elimine las preguntas que han creado.
* Marcar preguntas o respuestas de otros miembros.
* Identifique las respuestas a las preguntas que han creado.

#### Anónimo {#anonymous}

Los visitantes del sitio que no hayan iniciado sesión solo podrán leer las preguntas y respuestas publicadas, traducirlas si es compatible, pero no podrán añadir una pregunta o respuesta, ni marcar publicaciones de otros.

## Información adicional {#additional-information}

Encontrará más información en la página de [QnA Essentials](/help/communities/qna-essentials.md) para desarrolladores.

Para moderar los temas publicados y los comentarios, vea [Moderar el contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para etiquetar temas y comentarios publicados, consulte [Etiquetado de contenido generado por el usuario](/help/communities/tag-ugc.md).
