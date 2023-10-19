---
title: Función de calendario
description: Descubra cómo la función Calendario proporciona información sobre eventos de la comunidad en formato de calendario.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: c9b34b00-525d-4ca3-bd18-11bb7ce66787
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 7%

---

# Función de calendario {#calendar-feature}

## Introducción {#introduction}

La función de calendario permite proporcionar información de eventos de la comunidad en formato de calendario a todos los visitantes del sitio o solo a los visitantes del sitio (miembros de la comunidad) que hayan iniciado sesión, mientras que solo los miembros autorizados pueden agregar eventos.

Esta sección de la documentación describe

* AEM Adición de la función de calendario a un sitio de
* Ajustes de configuración para `Calendar` componentes

## Agregar un calendario a una página {#adding-a-calendar-to-a-page}

Para agregar un `Calendar` a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Calendar`

Y arrástrela a su lugar en una página, como una posición relativa a la función que deben revisar los usuarios.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](/help/communities/basics.md).

Si la variable [bibliotecas requeridas del lado del cliente](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side) están incluidos, así es como se `Calendar` aparece el componente.

![componente de calendario](assets/calendar-component.png)

### Configurar el calendario {#configuring-calendar}

Seleccione el colocado `Calendar` para que pueda acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configurar](assets/configure-new.png)

![configure-calendar](assets/configure-calendar1.png)

#### Pestaña Configuración {#settings-tab}

En el **Configuración** , especifique si desea permitir que se apliquen etiquetas a las entradas del calendario.

* **Eventos por página**

  Define el número de eventos que se muestran por página. El valor predeterminado es 10.

* **Moderado**

  Si se selecciona, la publicación de eventos de calendario y comentarios debe aprobarse antes de que aparezcan en un sitio de publicación. El valor predeterminado está desmarcado.

* **Cerrado**

  Si se selecciona, el calendario se cierra a las nuevas entradas de evento y comentarios. El valor predeterminado está desmarcado.

* **Editor de texto enriquecido**

  Si se selecciona, los eventos de calendario y los comentarios se pueden introducir con marcado. La opción predeterminada está activada.

* **Permitir etiquetado**

  Si se selecciona esta opción, permite a los miembros agregar etiquetas de etiqueta a los eventos que publican (consulte **Campo de etiqueta** pestaña). La opción predeterminada está activada.

* **Permitir cargas de archivos**

  Si se selecciona esta opción, se permite agregar archivos adjuntos a un evento de calendario o comentario. La opción predeterminada está activada.

* **Permitir seguimiento**

  Si se selecciona esta opción, se permite a los miembros seguir los eventos publicados en el calendario. La opción predeterminada está activada.

* **Tamaño máximo de archivo**

  Relevante solo si `Allow File Uploads` está marcada. Este campo limita el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 104857600 (10 Mb).

* **Tipos de archivo permitidos**

  Relevante solo si `Allow File Uploads` está marcada. Lista separada por comas de las extensiones de archivo con el separador de &quot;puntos&quot;. Por ejemplo, .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se podrán cargar los que no se hayan especificado. El valor predeterminado no se ha especificado, de modo que se permiten todos los tipos de archivo.

* **Tamaño máximo de archivo de imagen adjunto**

  Solo es relevante si está marcada la opción Permitir cargas de archivos. Número máximo de bytes que puede tener un archivo de imagen cargado. El valor predeterminado es 2097152** **(2 Mb).

* **Tipos de imagen de portada permitidos**

  Lista separada por comas de las extensiones de archivo de imagen con el separador de &quot;puntos&quot;. El valor predeterminado es `.jpg,.jpeg,.png,.gif,.bmp`.

* **Permitir respuestas de debate**

  Si se selecciona esta opción, se permiten las respuestas a los comentarios publicados en el evento del calendario. La opción predeterminada está activada.

* **Permitir que los usuarios eliminen comentarios y eventos**

  Si se selecciona esta opción, permite que los miembros eliminen los comentarios y los eventos de calendario que hayan publicado. La opción predeterminada está activada.

* **Habilitar la votación**

  Si se selecciona, se debe incluir la función de votación con un evento de calendario. La opción predeterminada está activada.

* **Mostrar rutas**

  Mostrar rutas en la página de eventos. La opción predeterminada está activada.

* **Filtro de intervalo de fechas**

  Define el número de días agregados a la fecha actual para calcular el valor &quot;Hasta&quot; del filtro de página con lista de eventos de calendario. El número predeterminado es 30.

* **Permitir contenido destacado**

  Si se selecciona, la idea se puede identificar como [contenido destacado](/help/communities/featured.md). El valor predeterminado está desmarcado.

En el **Moderación de usuario** , especifique cómo se administran los temas expuestos y las respuestas (contenido generado por el usuario). Para obtener más información, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

#### Pestaña Moderación de usuario {#user-moderation-tab}

* **Denegar entradas**

  Si se selecciona, se permite a los moderadores miembros de confianza denegar publicaciones e impedir que aparezcan en el foro público. La opción predeterminada está activada.

* **Cerrar/abrir de nuevo los eventos**

  Si se selecciona, los moderadores de miembros de confianza pueden cerrar un evento para realizar más ediciones y comentarios, y también pueden volver a abrir un evento. La opción predeterminada está activada.

* **Marcar entradas**

  Si se selecciona esta opción, se permite a los miembros marcar los eventos o comentarios de otros como inadecuados. La opción predeterminada está activada.

* **Lista de motivos de indicación**

  Si se selecciona esta opción, se permite a los miembros elegir, en una lista desplegable, el motivo por el que marcan un evento o comentario como inapropiado. El valor predeterminado está desmarcado.

* **Motivo de indicación personalizado**

  Si se selecciona esta opción, permite que los miembros especifiquen su propio motivo para marcar un evento o comentario como inapropiado. El valor predeterminado está desmarcado.

* **Umbral de moderación**

  Introduzca el número de veces que los miembros deben marcar un evento o comentario antes de notificarlo a los moderadores. El valor predeterminado es 1 ( una vez).

* **Límite de indicación**

  Introduzca el número de veces que se debe marcar un evento o comentario antes de ocultarlo de la vista pública. Si se establece en -1, el tema o comentario marcado nunca se ocultará de la vista pública. De lo contrario, este número debe ser mayor o igual que el umbral de moderación. El valor predeterminado es 5.

#### Pestaña Campo de etiqueta {#tag-field-tab}

En el **Campo de etiqueta** pestaña, las etiquetas que se pueden aplicar, si se permiten en la **Configuración** están limitadas según las áreas de nombres seleccionadas.

* **Espacios de nombres permitidos**

  Relevante si `Allow Tagging` está marcada en la **Configuración** pestaña. Las etiquetas que se pueden aplicar se limitan a aquellas dentro de las categorías de área de nombres comprobadas. La lista de áreas de nombres incluye &quot;Etiquetas estándar&quot; (el área de nombres predeterminada) e &quot;Incluir todas las etiquetas&quot;. El valor predeterminado es ninguno marcado, lo que significa que se permiten todas las áreas de nombres.

* **Límite de sugerencias**

  Introduzca el número de etiquetas que desea mostrar como sugerencia al usuario que publica en el foro. El valor predeterminado es **-**1 (sin límites).

>[!NOTE]
>
>Visita [Administración de etiquetas](/help/sites-administering/tags.md) donde puede aprender a añadir un área de nombres de etiqueta (taxonomía).

#### Pestaña Traducción {#translation-tab}

En el **Traducción** , si la traducción está habilitada para el sitio de la comunidad, la traducción puede configurarse para traducir todo el hilo (evento y comentarios) en lugar de publicaciones específicas.

* **Traducir todos**

  Si se selecciona, el evento y los comentarios se traducen al idioma preferido del usuario. La opción predeterminada está activada.

## Experiencia del visitante del sitio {#site-visitor-experience}

En el entorno de publicación, la función de calendario muestra un campo de búsqueda con un intervalo de fechas predeterminado y cualquier evento de calendario que se encuentre dentro de ese intervalo.

Cuando se selecciona un evento de calendario, se muestran los detalles, la descripción y los comentarios del evento de calendario.

Otras capacidades dependen de si el visitante del sitio es un moderador, administrador, miembro de la comunidad, miembro privilegiado o anónimo.

### Moderadores y administradores {#moderators-and-administrators}

Cuando el usuario que ha iniciado sesión tiene privilegios de moderador o administrador, puede realizar lo siguiente [tareas de moderación](/help/communities/moderate-ugc.md) (según lo permitido por la configuración del componente) en todos los eventos de calendario y comentarios publicados en un evento.

![moderators-view](assets/moderators-view.png)

#### Miembros {#members}

Cuando el usuario que ha iniciado sesión es miembro de la comunidad o [miembro privilegiado](/help/communities/users.md#privileged-members-group) (según la configuración), pueden seleccionar `New Event` para crear y publicar un nuevo evento de calendario.

Concretamente, pueden:

* Creación de un evento de calendario
* Publicar un comentario en un evento de calendario
* Editar su propio evento o comentario del calendario
* Eliminar su propio evento o comentario del calendario
* Marcar los eventos o comentarios del calendario de otros usuarios

![create-event](assets/configure-calendar2.png)

![event-post](assets/configure-calendar3.png)

#### Anónimo {#anonymous}

Los visitantes del sitio que no hayan iniciado sesión solo pueden leer los eventos de calendario publicados, traducirlos si se admiten, pero no pueden agregar un evento o comentario ni marcar los eventos o comentarios de otros.

![anonymous-user-view](assets/anonymous-user-view1.png)

## Información adicional {#additional-information}

Puede encontrar más información en la [Calendar Essentials](/help/communities/calendar-basics-for-developers.md) para desarrolladores.

Para ver la moderación de los eventos de calendario y los comentarios, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para etiquetar eventos de calendario y comentarios, consulte [Etiquetado del contenido generado por el usuario](/help/communities/tag-ugc.md).

Para ver la traducción de los eventos de calendario y los comentarios, consulte [Traducción del contenido generado por el usuario](/help/communities/translate-ugc.md).
