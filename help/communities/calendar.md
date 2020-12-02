---
title: Función de calendario
seo-title: Función de calendario
description: Proporciona información de evento de la comunidad en formato de calendario
seo-description: Proporciona información de evento de la comunidad en formato de calendario
uuid: 262f6afa-d8aa-4815-8440-a8ed5668c76d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 70fa0b9c-cb98-45c4-9c94-bef4a9f3741e
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 7%

---


# Característica de calendario {#calendar-feature}

## Introducción {#introduction}

La función de calendario permite proporcionar información de evento de la comunidad en un formato de calendario a todos los visitantes del sitio o solo a los visitantes del sitio (miembros de la comunidad), mientras que solo los miembros autorizados pueden agregar eventos.

Esta sección de la documentación describe

* Añadir la función de calendario en un sitio AEM
* Configuración de los componentes `Calendar`

## Añadir un calendario en una página {#adding-a-calendar-to-a-page}

Para agregar un componente `Calendar` a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Calendar`

y arrástrelo a su lugar en una página, como una posición relativa a la función que los usuarios deben revisar.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de comunidades](/help/communities/basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side), así es como aparecerá el componente `Calendar`.

![calendar-component](assets/calendar-component.png)

### Configuración del calendario {#configuring-calendar}

Seleccione el componente `Calendar` colocado para acceder y seleccione el icono `Configure` que abre el cuadro de diálogo de edición.

![configurar](assets/configure-new.png)

![configure-calendar](assets/configure-calendar1.png)

#### Ficha Configuración {#settings-tab}

En la ficha **Configuración**, especifique si desea o no permitir que las etiquetas se apliquen a las entradas de calendario.

* **Eventos por página**

   Define el número de eventos que se muestran por página. El valor predeterminado es 10.

* **Moderado**

   Si se selecciona, la publicación de eventos y comentarios de calendario debe aprobarse antes de que aparezcan en un sitio de publicación. El valor predeterminado no está marcado.

* **Cerrado**

   Si se selecciona, el calendario se cierra a nuevas entradas y comentarios de evento. El valor predeterminado no está marcado.

* **Editor de texto enriquecido**

   Si se selecciona, los eventos y comentarios del calendario pueden introducirse con marcado. El valor predeterminado está marcado.

* **Permitir etiquetado**

   Si está activada, permita que los miembros agreguen etiquetas a los eventos que publiquen (consulte la ficha **Campo de etiqueta**). El valor predeterminado está marcado.

* **Permitir cargas de archivos**

   Si está activada, permita que los archivos adjuntos se agreguen a un evento o comentario de calendario. El valor predeterminado está marcado.

* **Permitir seguimiento**

   Si está activada, permita que los miembros sigan los eventos publicados en el calendario. El valor predeterminado está marcado.

* **Tamaño máximo de archivo**

   Solo es pertinente si se comprueba `Allow File Uploads`. Este campo limitará el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 104857600 (10 Mb).

* **Tipos de archivo permitidos**

   Solo es pertinente si se comprueba `Allow File Uploads`. Lista separada por comas de extensiones de archivo con el separador &quot;punto&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permitirá cargar los no especificados. El valor predeterminado no se especifica de forma que se permitan todos los tipos de archivo.

* **Tamaño máximo de archivo de imagen adjunto**

   Solo es relevante si está activada la opción Permitir cargas de archivos. Número máximo de bytes que puede tener un archivo de imagen cargado. El valor predeterminado es 2097152*** **(2 Mb).

* **Tipos de imagen de portada permitidos**

   Lista separada por comas de extensiones de archivo de imagen con el separador &quot;punto&quot;. El valor predeterminado es `.jpg,.jpeg,.png,.gif,.bmp`.

* **Permitir respuestas de debate**

   Si está activada, permita respuestas a los comentarios publicados en el evento del calendario. El valor predeterminado está marcado.

* **Permitir que los usuarios eliminen comentarios y eventos**

   Si está activada, permita que los miembros eliminen los comentarios y eventos de calendario que han publicado. El valor predeterminado es** **marcado.

* **Habilitar la votación**

   Si está activada, incluya la función de voto con un evento de calendario. El valor predeterminado está marcado.

* **Mostrar rutas**

   Mostrar rutas en la página de eventos. El valor predeterminado está marcado.

* **Filtro de intervalo de fechas**

   Define el número de días agregados a la fecha actual para calcular el valor &quot;A&quot; del filtro de página de lista de eventos de calendario. El número predeterminado es 30.

* **Permitir contenido destacado**

   Si se selecciona, la idea se puede identificar como [contenido destacado](/help/communities/featured.md). El valor predeterminado no está marcado.

En la ficha **Moderación del usuario**, especifique cómo se administran los temas publicados y las respuestas (contenido generado por el usuario). Para obtener más información, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

#### Ficha Moderación del usuario {#user-moderation-tab}

* **Denegar entradas**

   Si se selecciona, los moderadores miembros de confianza podrán denegar las publicaciones e impedir que aparezcan en el foro público. El valor predeterminado está marcado.

* **Cerrar/abrir de nuevo los eventos**

   Si se selecciona, los moderadores de miembros de confianza pueden cerrar un evento para realizar más ediciones y comentarios, y también pueden volver a abrir un evento. El valor predeterminado está marcado.

* **Marcar entradas**

   Si se selecciona, permita que los miembros marquen los eventos o comentarios de otros como inapropiados. El valor predeterminado está marcado.

* **Lista de motivos de indicación**

   Si se selecciona, permita que los miembros elijan, desde una lista desplegable, el motivo por el que marcan un evento o comentario como inapropiado. El valor predeterminado no está marcado.

* **Motivo de indicación personalizado**

   Si se selecciona, permita que los miembros especifiquen su propio motivo para marcar un evento o comentario como inapropiado. El valor predeterminado no está marcado.

* **Umbral de moderación**

   Escriba el número de veces que los miembros deben marcar un evento o comentario antes de que se notifique a los moderadores. El valor predeterminado es 1 ( una vez).

* **Límite de indicación**

   Escriba el número de veces que se debe marcar un evento o comentario antes de ocultarlo en la vista pública. Si se establece en -1, el tema o comentario marcado nunca se oculta en la vista pública. De lo contrario, este número debe ser bueno o igual al umbral de moderación. El valor predeterminado es 5.

#### Ficha Campo de etiqueta {#tag-field-tab}

En la ficha **Campo de etiqueta**, las etiquetas que se pueden aplicar, si se permiten en la ficha **Configuración**, están limitadas según las Áreas de nombres elegidas.

* **Espacios de nombres permitidos**

   Relevante si `Allow Tagging` se comprueba en la ficha **Configuración**. Las etiquetas que se pueden aplicar están limitadas a las que se encuentran dentro de las categorías de Área de nombres seleccionadas. La lista de Áreas de nombres incluye &quot;Etiquetas estándar&quot; (la Área de nombres predeterminada) y &quot;Incluir todas las etiquetas&quot;. El valor predeterminado no está marcado, lo que significa que se permiten todas las Áreas de nombres.

* **Límite de sugerencias**

   Escriba el número de etiquetas que se mostrarán como una sugerencia para el miembro que se publica en el foro. El valor predeterminado es **-**1 (sin límites).

>[!NOTE]
>
>Visite [Administración de etiquetas](/help/sites-administering/tags.md) para obtener información sobre cómo agregar una nueva Área de nombres de etiquetas (taxonomía).

#### Ficha Traducción {#translation-tab}

En la ficha **Traducción**, si la traducción está habilitada para el sitio de la comunidad, la traducción puede configurarse para traducir el subproceso completo (eventos y comentarios) en lugar de publicaciones específicas.

* **Traducir todos**

   Si se selecciona, el evento y los comentarios se traducen al idioma preferido del usuario. El valor predeterminado está marcado.

## Experiencia de Visitante del sitio {#site-visitor-experience}

En el entorno de publicación, la función de calendario mostrará un campo de búsqueda con un intervalo de fechas predeterminado y cualquier evento de calendario que se encuentre dentro de ese intervalo.

Cuando se selecciona un evento de calendario, se muestran los detalles, la descripción y los comentarios del evento de calendario.

Otras capacidades dependen de si el visitante del sitio es un moderador, administrador, miembro de la comunidad, miembro privilegiado o anónimo.

### Moderadores y administradores {#moderators-and-administrators}

Cuando el usuario que ha iniciado sesión tiene privilegios de moderador o administrador, puede realizar [tareas de moderación](/help/communities/moderate-ugc.md) (según lo permite la configuración del componente) en todos los eventos de calendario y comentarios publicados en un evento.

![moderadores: vista](assets/moderators-view.png)

#### Miembros {#members}

Cuando el usuario que ha iniciado sesión es un miembro de la comunidad o [miembro con privilegios](/help/communities/users.md#privileged-members-group) (según la configuración), puede seleccionar `New Event` para crear y anunciar un nuevo evento de calendario.

Concretamente, podrán:

* Crear un nuevo evento de calendario
* Anunciar un comentario en un evento de calendario
* Editar su propio evento o comentario de calendario
* Eliminar su propio evento de calendario o comentario
* Marcar los eventos o comentarios del calendario de otros

![create-evento](assets/configure-calendar2.png)

![evento-post](assets/configure-calendar3.png)

#### Anónimo {#anonymous}

Los visitantes del sitio que no hayan iniciado sesión sólo podrán leer los eventos del calendario publicados, traducirlos si son compatibles, pero no podrán agregar un evento o comentario ni marcar los eventos o comentarios de otros.

![anónima-user-vista](assets/anonymous-user-view1.png)

## Información adicional {#additional-information}

Puede encontrar más información en la página [Calendar Essentials](/help/communities/calendar-basics-for-developers.md) para desarrolladores.

Para obtener información sobre la moderación de eventos y comentarios de calendario, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para etiquetar eventos de calendario y comentarios, consulte [Etiquetado de contenido generado por el usuario](/help/communities/tag-ugc.md).

Para obtener la traducción de eventos y comentarios de calendario, consulte [Traducción de contenido generado por el usuario](/help/communities/translate-ugc.md).
