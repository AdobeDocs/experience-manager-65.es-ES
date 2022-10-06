---
title: Función de ideación
seo-title: Ideation Feature
description: Adición y configuración de la función Ideación
seo-description: Adding and configuring the Ideation feature
uuid: 38468290-6d00-4ee4-91d8-7c2e8ae32712
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a3f5a21d-2df6-4663-a1ea-3a067c46f860
docset: aem65
exl-id: e130bab4-524d-4413-ba8b-53d0ed9e8623
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 10%

---

# Función de ideación {#ideation-feature}

## Introducción {#introduction}

La función de ideación proporciona un área para los visitantes del sitio que han iniciado sesión (miembros de la comunidad) en el entorno de publicación para:

* Cree ideas para compartirlas con la comunidad.
* Ver y comentar ideas.
* Sigue una idea.
* Votar sobre una idea.

Esta sección de la documentación describe:

* Adición de la función de ideación a un sitio AEM.
* Ajustes de configuración del componente Ideación.

### Adición de una idea a una página {#adding-a-ideation-to-a-page}

Para agregar un `Ideation` a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Ideation`

y arrástrela a su lugar en una página en la que debería aparecer la idea.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de Communities](/help/communities/basics.md).

Cuando la variable [bibliotecas requeridas del lado del cliente](/help/communities/ideation.md#essentials-for-client-side) se incluyen, así es como se muestra la variable `Ideation` aparecerá el componente:

![ideación](assets/ideation.png)

### Configuración de una idea {#configuring-an-ideation}

Seleccione la colocación `Ideation` para acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configure-new](assets/configure-new.png)

![ideation-settings](assets/ideation-settings.png)

#### Ficha Configuración {#settings-tab}

En el **[!UICONTROL Configuración]** especifique la configuración de las ideas y los comentarios:

* **Permitir la miniatura del archivo adjunto**
* **Tamaño máximo de la miniatura del archivo adjunto**
* **Tamaño mínimo de la imagen de la miniatura**
* **Tamaño máximo de la miniatura**
* **Permitir miembros privilegiados**
* **Miembros privilegiados permitidos**
* **Bloquee el contenido que haya creado el usuario en el modo de edición de autor**
* **Título de ideación**

* Título para mostrar la idea. El valor predeterminado es `Ideation`.
* **Descripción de ideación**

   Descripción que se mostrará como un subtítulo para la idea. El valor predeterminado no es una descripción.

* **Temas por página**

   Define el número de ideas/anuncios que se muestran por página. El valor predeterminado es 10.

* **Moderado**

   Si se selecciona, la publicación de ideas y comentarios debe aprobarse antes de que aparezcan en un sitio de publicación. El valor predeterminado no está seleccionado.

* **Cerrado**

   Si se selecciona, el foro de ideación está cerrado a nuevas ideas y comentarios. El valor predeterminado no está seleccionado.

* **Editor de texto enriquecido**

   Si se selecciona, las ideas y los comentarios pueden introducirse con marcado. El valor predeterminado no está seleccionado.

* **Permitir etiquetado**

   Si está activada, permita que los miembros agreguen etiquetas a su publicación (consulte **[!UICONTROL Campo de etiqueta]** ). El valor predeterminado no está seleccionado.

* **Permitir cargas de archivos**

   Si está activada, permita que los archivos adjuntos se agreguen a la idea o comentario. El valor predeterminado no está seleccionado.

* **Tamaño máximo de archivo**

   Solo relevante si `Allow File Uploads` está activada. Este campo limita el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 104857600 (10 Mb).

* **Tipos de archivo permitidos**

   Solo relevante si `Allow File Uploads` está activada. Lista de extensiones de archivo separados por coma con el separador &quot;punto&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permitirá cargar aquellos que no se especifiquen. El valor predeterminado no se especifica de forma que se permitan todos los tipos de archivo.

* **Tamaño máximo de archivo de imagen adjunto**

   Solo es relevante si está marcada la opción Permitir cargas de archivos . Número máximo de bytes que puede tener un archivo de imagen cargado. El valor predeterminado es 2097152 (2 Mb).

* **Permitir respuestas**

   Si está marcada esta opción, permita que se respondan a los comentarios publicados en la idea. El valor predeterminado no está seleccionado.

* **Habilitar la votación**

   Si está comprobado, permita votar los comentarios de una idea. El valor predeterminado no está seleccionado.

* **Permitir que los usuarios eliminen comentarios y temas**

   Si se selecciona, permita que los miembros eliminen los comentarios e ideas que publicaron. El valor predeterminado no está seleccionado.

* **Permitir seguimiento**

   Si está marcada esta opción, incluya la siguiente función para anuncios de ideas, que permite que los miembros se [notificadas](/help/communities/notifications.md) de nuevos puestos. El valor predeterminado no está seleccionado.

* **Permitir suscripciones por correo electrónico**

   Si está activada, permita que se notifique a los miembros de los anuncios nuevos por correo electrónico ([suscripción](/help/communities/subscriptions.md)). Requiere `Allow Following` que se comprobarán y [correo electrónico configurado](/help/communities/email.md). El valor predeterminado no está seleccionado.

* **Habilitar la votación**

   Si está comprobado, permita votar los comentarios de una idea. El valor predeterminado no está seleccionado.

* **Mostrar insignias**

   Si está activada, muestre ganado y asignado [distintivos](/help/communities/implementing-scoring.md) con la idea de un miembro. El valor predeterminado no está seleccionado.

* **No obtener respuestas en la página de lista**

* **Permitir contenido destacado**

   Si se selecciona, la idea puede identificarse como [contenido destacado](/help/communities/featured.md). El valor predeterminado no está seleccionado.

* **Habilitar la mención**
* **Menciones máximas**
* **Patrón de menciones en la interfaz de usuario**

#### Pestaña Moderación del usuario {#user-moderation-tab}

En el **[!UICONTROL Moderación del usuario]** especifique cómo se administran las ideas y comentarios publicados (contenido generado por el usuario). Para obtener más información, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

* **Denegar entradas**

   Si se selecciona, se permitirá a los moderadores miembros de confianza denegar publicaciones e impedir que la publicación aparezca en el foro público. El valor predeterminado no está seleccionado.

* **Cerrar/abrir de nuevo los temas**

   Si se selecciona, los moderadores miembros de confianza pueden cerrar un tema para realizar más ediciones y comentarios, y también pueden volver a abrir un tema. El valor predeterminado no está seleccionado.

* **Marcar entradas**

   Si se selecciona, permita a los miembros marcar como inapropiados los temas o comentarios de otros. El valor predeterminado no está seleccionado.

* **Lista de motivos de indicación**

   Si está marcada esta opción, permita que los miembros elijan, desde una lista desplegable, el motivo por el que marcan un tema o comentario como inapropiado. El valor predeterminado no está seleccionado.

* **Motivo de indicación personalizado**

   Si está activada, permita que los miembros especifiquen su propio motivo para marcar un tema o comentario como inapropiado. El valor predeterminado no está seleccionado.

* **Umbral de moderación**

   Introduzca el número de veces que los miembros deben marcar un tema o comentario antes de que se notifique a los moderadores. El valor predeterminado es 1 ( una vez).

* **Límite de indicación**

   Introduzca el número de veces que se debe marcar un tema o comentario antes de ocultarlo de la vista pública. Si se establece en -1, el tema o comentario marcado nunca se oculta a la vista del público. De lo contrario, este número debe ser bueno o igual al umbral de moderación. El valor predeterminado es 5.

#### Ficha Campo de etiqueta {#tag-field-tab}

En el **[!UICONTROL Campo de etiqueta]** , las etiquetas que se pueden aplicar, si se permiten en la sección **[!UICONTROL Configuración]** , se limitan según los espacios de nombres seleccionados.

* **Espacios de nombres permitidos**

   Pertinente si `Allow Tagging` se marca en la sección **[!UICONTROL Configuración]** pestaña . Las etiquetas que se pueden aplicar se limitan a las que están dentro de las categorías de espacio de nombres seleccionadas. La lista de áreas de nombres incluye &quot;Etiquetas estándar&quot; (el espacio de nombres predeterminado) así como &quot;Incluir todas las etiquetas&quot;. El valor predeterminado es ninguno activado, lo que significa que se permiten todas las áreas de nombres.

* **Límite de sugerencias**

   Introduzca el número de etiquetas que se mostrarán como una sugerencia para el usuario que publica en el foro. Un valor de **-1** significa sin límite. El valor predeterminado es 0.

#### Ficha Ordenar configuración {#sort-settings-tab}

En el **[!UICONTROL Configuración de ordenación]** , especifique cómo se ordenan los comentarios publicados cuando se muestran.

* **Ordenar por**

   Compruebe todas las selecciones de ordenación permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. El valor predeterminado es `Newest, Oldest, Last Updated`.

* **Establecer como predeterminado**

   Despliegue para seleccionar una de las opciones de ordenación seleccionadas que aparecerán como predeterminadas. El valor predeterminado es `Newest`.

* **Seleccione las opciones de hora para la clasificación de Analytics**

   Desplegable para seleccionar uno de `All, Last 24 Hours, Last 7 Days, Last 30 Days`. El valor predeterminado es `All`.

## Experiencia del visitante del sitio {#site-visitor-experience}

### Creación de una idea {#creating-idea}

Al igual que con todas las características de Communities, si no se ha iniciado sesión, el visitante del sitio solo puede leer ideas y ver otras opiniones (a través de comentarios y votos/&quot;Me gusta&quot;).

Una vez que haya iniciado sesión, un miembro puede crear una nueva idea.

![create-new-idea](assets/create-new-idea.png)

Antes de presentar la idea, es posible que el miembro guarde un borrador.

Seleccione la `Save as Draft` , se guarda un borrador.

![save-idea](assets/save-idea.png)

Al ver borradores guardados en el `My Drafts` , seleccione `Read More` para volver a entrar en el modo de edición:

![edit-idea](assets/edit-idea.png)

#### Proporcionar comentarios {#providing-feedback}

Una vez publicada la idea, otros miembros pueden iniciar sesión, abrir la idea ( `Read More`) y me gusta la idea, añadiendo así al recuento de votos, y hacer comentarios.

![comentarios](assets/feedback-idea.png)

### Información adicional {#additional-information}

Puede encontrar más información en la [Aspectos básicos de la idea](/help/communities/ideation.md) para desarrolladores.

Para moderar los temas y comentarios publicados, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para etiquetar temas y comentarios publicados, consulte [Etiquetado del contenido generado por el usuario](/help/communities/tag-ugc.md).
