---
title: Función de calendario
seo-title: Calendar Feature
description: Proporciona información de eventos de la comunidad en formato de calendario
seo-description: Provides community event information in a calendar format
uuid: 262f6afa-d8aa-4815-8440-a8ed5668c76d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 70fa0b9c-cb98-45c4-9c94-bef4a9f3741e
docset: aem65
exl-id: c9b34b00-525d-4ca3-bd18-11bb7ce66787
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 7%

---

# Función de calendario {#calendar-feature}

## Introducción {#introduction}

La función de calendario permite proporcionar información de eventos de la comunidad en formato de calendario a todos los visitantes del sitio o solo a los visitantes del sitio (miembros de la comunidad), mientras que solo los miembros autorizados pueden agregar eventos.

Esta sección de la documentación describe

* Adición de la función de calendario a un sitio AEM
* Ajustes de configuración para `Calendar` componentes

## Adición de un calendario a una página {#adding-a-calendar-to-a-page}

Para agregar un `Calendar` a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Calendar`

y arrástrela a su lugar en una página, por ejemplo, una posición relativa a la función para que los usuarios la revisen.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de Communities](/help/communities/basics.md).

Cuando la variable [bibliotecas requeridas del lado del cliente](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side) se incluyen, así es como se muestra la variable `Calendar` aparecerá el componente.

![componente de calendario](assets/calendar-component.png)

### Configuración del calendario {#configuring-calendar}

Seleccione la colocación `Calendar` para acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configure](assets/configure-new.png)

![configure-calendar](assets/configure-calendar1.png)

#### Ficha Configuración {#settings-tab}

En el **Configuración** , especifique si desea permitir o no que las etiquetas se apliquen a las entradas del calendario.

* **Eventos por página**

   Define el número de eventos que se muestran por página. El valor predeterminado es 10.

* **Moderado**

   Si se selecciona, la publicación de eventos de calendario y comentarios debe aprobarse antes de que aparezcan en un sitio de publicación. El valor predeterminado no está seleccionado.

* **Cerrado**

   Si se selecciona, el calendario se cierra a nuevas entradas de eventos y comentarios. El valor predeterminado no está seleccionado.

* **Editor de texto enriquecido**

   Si se selecciona, los eventos de calendario y los comentarios se pueden introducir con marcado. El valor predeterminado está marcado.

* **Permitir etiquetado**

   Si está activada, permita que los miembros agreguen etiquetas a los eventos que anuncien (consulte **Campo de etiqueta** ). El valor predeterminado está marcado.

* **Permitir cargas de archivos**

   Si está activada, permita que los archivos adjuntos se agreguen a un evento o comentario de calendario. El valor predeterminado está marcado.

* **Permitir seguimiento**

   Si está activada, permita que los miembros sigan los eventos anunciados en el calendario. El valor predeterminado está marcado.

* **Tamaño máximo de archivo**

   Solo relevante si `Allow File Uploads` está activada. Este campo limita el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 104857600 (10 Mb).

* **Tipos de archivo permitidos**

   Solo relevante si `Allow File Uploads` está activada. Lista de extensiones de archivo separados por coma con el separador &quot;punto&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permitirá cargar aquellos que no se especifiquen. El valor predeterminado no se especifica de forma que se permitan todos los tipos de archivo.

* **Tamaño máximo de archivo de imagen adjunto**

   Solo es relevante si está marcada la opción Permitir cargas de archivos . Número máximo de bytes que puede tener un archivo de imagen cargado. El valor predeterminado es 2097152** **(2 Mb).

* **Tipos de imagen de portada permitidos**

   Lista separada por comas de las extensiones de archivo de imagen con el separador &quot;punto&quot;. El valor predeterminado es `.jpg,.jpeg,.png,.gif,.bmp`.

* **Permitir respuestas de debate**

   Si está marcada esta opción, permita que se respondan a los comentarios anunciados en el evento de calendario. El valor predeterminado está marcado.

* **Permitir que los usuarios eliminen comentarios y eventos**

   Si está activada, permita que los miembros eliminen los comentarios y los eventos de calendario que hayan publicado. El valor predeterminado es** **marcado.

* **Habilitar la votación**

   Si está marcada esta opción, incluya la función Votación con un evento de calendario. El valor predeterminado está marcado.

* **Mostrar rutas**

   Mostrar rutas en la página de eventos. El valor predeterminado está marcado.

* **Filtro de intervalo de fechas**

   Define el número de días agregados a la fecha actual para calcular el valor &quot;Para&quot; del filtro de página de lista de eventos de calendario. El número predeterminado es 30.

* **Permitir contenido destacado**

   Si se selecciona, la idea puede identificarse como [contenido destacado](/help/communities/featured.md). El valor predeterminado no está seleccionado.

En el **Moderación del usuario** especifique cómo se administran los temas publicados y las respuestas (contenido generado por el usuario). Para obtener más información, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

#### Pestaña Moderación del usuario {#user-moderation-tab}

* **Denegar entradas**

   Si se selecciona, se permitirá a los moderadores miembros de confianza denegar publicaciones e impedir que la publicación aparezca en el foro público. El valor predeterminado está marcado.

* **Cerrar/abrir de nuevo los eventos**

   Si se selecciona, los moderadores miembros de confianza pueden cerrar un evento para realizar más ediciones y comentarios, y también pueden volver a abrir un evento. El valor predeterminado está marcado.

* **Marcar entradas**

   Si está activada, permita que los miembros marquen los eventos o comentarios de otros como inapropiados. El valor predeterminado está marcado.

* **Lista de motivos de indicación**

   Si está marcada esta opción, permita que los miembros elijan, desde una lista desplegable, el motivo por el que marcan un evento o comentario como inapropiado. El valor predeterminado no está seleccionado.

* **Motivo de indicación personalizado**

   Si está marcada esta opción, permita que los miembros especifiquen su propio motivo para marcar un evento o comentario como inapropiado. El valor predeterminado no está seleccionado.

* **Umbral de moderación**

   Introduzca el número de veces que los miembros deben marcar un evento o comentario antes de notificar a los moderadores. El valor predeterminado es 1 ( una vez).

* **Límite de indicación**

   Introduzca el número de veces que se debe marcar un evento o comentario antes de ocultarlo de la vista pública. Si se establece en -1, el tema o comentario marcado nunca se oculta a la vista del público. De lo contrario, este número debe ser bueno o igual al umbral de moderación. El valor predeterminado es 5.

#### Ficha Campo de etiqueta {#tag-field-tab}

En el **Campo de etiqueta** , las etiquetas que se pueden aplicar, si se permiten en la sección **Configuración** , se limitan según los espacios de nombres seleccionados.

* **Espacios de nombres permitidos**

   Pertinente si `Allow Tagging` se marca en la sección **Configuración** pestaña . Las etiquetas que se pueden aplicar se limitan a las que están dentro de las categorías de espacio de nombres seleccionadas. La lista de áreas de nombres incluye &quot;Etiquetas estándar&quot; (el espacio de nombres predeterminado) así como &quot;Incluir todas las etiquetas&quot;. El valor predeterminado es ninguno activado, lo que significa que se permiten todas las áreas de nombres.

* **Límite de sugerencias**

   Introduzca el número de etiquetas que se mostrarán como una sugerencia para el usuario que publica en el foro. El valor predeterminado es **-**1 (sin límites).

>[!NOTE]
>
>Visita [Administración de etiquetas](/help/sites-administering/tags.md) para aprender a añadir un nuevo espacio de nombres de etiqueta (taxonomía).

#### Ficha Traducción {#translation-tab}

En el **Traducción** , si la traducción está habilitada para el sitio de la comunidad, la traducción se puede configurar para que traduzca todo el subproceso (evento y comentarios) en lugar de anuncios específicos.

* **Traducir todos**

   Si se selecciona, el evento y los comentarios se traducen al idioma preferido del usuario. El valor predeterminado está marcado.

## Experiencia del visitante del sitio {#site-visitor-experience}

En el entorno de publicación, la función de calendario mostrará un campo de búsqueda con un intervalo de fechas predeterminado y cualquier evento de calendario que se encuentre dentro de ese intervalo.

Cuando se selecciona un evento de calendario, se muestran los detalles, la descripción y los comentarios del evento de calendario.

Otras capacidades dependen de si el visitante del sitio es moderador, administrador, miembro de la comunidad, miembro privilegiado o anónimo.

### Moderadores y administradores {#moderators-and-administrators}

Cuando el usuario que ha iniciado sesión tiene privilegios de moderador o administrador, puede realizar [tareas de moderación](/help/communities/moderate-ugc.md) (según lo permita la configuración del componente) en todos los eventos de calendario y comentarios anunciados en un evento.

![vista moderadores](assets/moderators-view.png)

#### Miembros {#members}

Cuando el usuario que ha iniciado sesión es un miembro de la comunidad o [miembro privilegiado](/help/communities/users.md#privileged-members-group) (según la configuración), pueden seleccionar `New Event` para crear y anunciar un nuevo evento de calendario.

Concretamente, podrán:

* Crear un nuevo evento de calendario
* Publicar un comentario en un evento de calendario
* Editar su propio evento de calendario o comentario
* Eliminar su propio evento de calendario o comentario
* Marcar eventos de calendario o comentarios de otros

![create-event](assets/configure-calendar2.png)

![event-post](assets/configure-calendar3.png)

#### Anónimo {#anonymous}

Los visitantes del sitio que no hayan iniciado sesión solo podrán leer los eventos de calendario anunciados, traducirlos si son compatibles, pero no pueden agregar un evento o comentario ni marcar los eventos o comentarios de otros.

![anonymous-user-view](assets/anonymous-user-view1.png)

## Información adicional {#additional-information}

Puede encontrar más información en la [Elementos básicos del calendario](/help/communities/calendar-basics-for-developers.md) para desarrolladores.

Para moderar eventos de calendario y comentarios, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para etiquetar eventos de calendario y comentarios, consulte [Etiquetado del contenido generado por el usuario](/help/communities/tag-ugc.md).

Para ver la traducción de los eventos y comentarios del calendario, consulte [Traducción del contenido generado por el usuario](/help/communities/translate-ugc.md).
