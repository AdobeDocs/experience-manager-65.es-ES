---
title: Función de la biblioteca de archivos
seo-title: Función de la biblioteca de archivos
description: La función Biblioteca de archivos permite a los visitantes del sitio que inician sesión cargar, administrar y descargar archivos
seo-description: La función Biblioteca de archivos permite a los visitantes del sitio que inician sesión cargar, administrar y descargar archivos
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Función de la biblioteca de archivos{#file-library-feature}

## Introducción {#introduction}

La función de biblioteca de archivos proporciona un lugar para que los visitantes del sitio que han iniciado sesión (miembros de la comunidad) carguen, gestionen y descarguen archivos dentro del sitio de la comunidad.

Esta sección de la documentación describe

* adición de la función de biblioteca de archivos a un sitio de AEM
* configuración del `File Library` componente

### Adición de una biblioteca de archivos a una página {#adding-a-file-library-to-a-page}

Para agregar un `File Library` componente a una página en modo de autor, ubique el componente

* `Communities / File Library`

y arrástrelo a su lugar en una página.

Para obtener la información necesaria, visite [Communities Components Basics](/help/communities/basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se incluyen las bibliotecas [del lado del cliente](/help/communities/essentials-file-library.md#essentials-for-client-side) necesarias, así es como aparecerá el `File Library` componente:

![chlimage_1-145](assets/chlimage_1-145.png)

### Configuración de la biblioteca de archivos {#configuring-file-library}

Seleccione el componente colocado al que desea acceder y seleccione el `File Library` `Configure` icono que abre el cuadro de diálogo de edición.

![chlimage_1-146](assets/chlimage_1-146.png) ![forum-config-1](assets/forum-config-1.png)

#### Ficha Comentarios {#comments-tab}

En la ficha **Comments **tab, especifique si los comentarios de los archivos cargados aparecen y cómo aparecerán:

* **Permitir comentarios en archivos** Si está activada, permita comentarios en los archivos cargados. El valor predeterminado no está marcado.

* **Comentarios por página** Limita el número de comentarios que se muestran por página, así como el número de respuestas que se muestran. El valor predeterminado es **10**.

* **Tamaño** máximo del archivoEste valor limitará el tamaño del archivo cargado. El límite predeterminado es 104857600 (10 Mb).

* **Longitud** máxima del mensaje Número máximo de caracteres que se pueden introducir en el cuadro de texto. El valor predeterminado es de 4096 caracteres.

* **Tipos** de archivo permitidos Una lista de extensiones de archivo separadas por coma con el separador &quot;punto&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permitirán los no especificados. El valor predeterminado no es ninguno, por lo que se permiten** **todos los tipos de archivo.

* **Editor** de texto enriquecido Si está marcado, los comentarios se pueden introducir con marcado. El valor predeterminado no está marcado.

* **Eliminar comentarios** Si se selecciona, los usuarios pueden eliminar sus propios comentarios. El valor predeterminado está marcado.

* **Permitir etiquetado** Si se selecciona, se habilitará la capacidad de agregar una etiqueta al archivo. El valor predeterminado no está marcado.

* **Espacios** de nombres permitidos Si se selecciona Permitir etiquetado, las etiquetas disponibles se limitarán a los espacios de nombres marcados. Si no se marca ninguna, se permite todo. El valor predeterminado es todos los espacios de nombres.

* **Límite** de sugerencias Si se selecciona Permitir etiquetado, esta configuración limita el número de etiquetas sugeridas para mostrar. Si se establece en -1, no hay límite. El valor predeterminado es -1.

* **Permitir voto** Si se selecciona, se habilitará la capacidad de votar para un archivo. El valor predeterminado no está marcado.

* **Permitir lo siguiente** Si está activado, incluya la siguiente función para los artículos de blog, que permite que se [notifique](/help/communities/notifications.md) a los miembros de los nuevos anuncios. El valor predeterminado no está marcado.

* **Habilitar mención** Si está habilitada, permite que los usuarios registrados de la comunidad identifiquen a otros miembros registrados (con el nombre, apellidos y nombre de usuario) y los etiqueten con la sintaxis común @user-name. Los usuarios etiquetados reciben notificaciones sobre sus menciones.

* **Menciones** máximasRestringir el número máximo de menciones permitidas en una publicación. El valor predeterminado es 10.

* **Patrón** de mención de la interfaz de usuarioEspecifique la cadena de patrón permitida para etiquetar (@mención) al usuario registrado en una publicación. Por ejemplo, ~{{familyName}}{{givenName}}.

* **Permitir respuestas por subprocesos** Si está activada, permita respuestas a los comentarios publicados. El valor predeterminado no está marcado.

#### Ficha Moderación del usuario {#user-moderation-tab}

En la ficha Moderación **** del usuario, configure la moderación de los comentarios si se permiten los comentarios:

* **Premoderación** Si está activada, los comentarios deben aprobarse antes de que aparezcan en un sitio de publicación. El valor predeterminado no está marcado.

* **Eliminar comentarios** Si se selecciona, el visitante que publicó el comentario puede eliminarlo. El valor predeterminado está marcado.

* **Denegar comentarios** Si se selecciona, permita que los moderadores de miembros de confianza rechacen los comentarios. El valor predeterminado no está marcado.

* **Cerrar/volver a abrir Comentarios** Si está activado, permita que los moderadores de miembros de confianza cierren y vuelvan a abrir los comentarios. El valor predeterminado no está marcado.

* **Marcar comentarios** Si se selecciona, permita a los visitantes marcar los comentarios como inapropiados. El valor predeterminado no está marcado.

* **Indicar lista** de motivos Si está activada, permita que los visitantes elijan, en una lista desplegable, el motivo por el que marcan un comentario como inapropiado. El valor predeterminado no está marcado.

* **Razón** de marca personalizada Si se selecciona, permita que los visitantes introduzcan su propio motivo para marcar un comentario como inapropiado. El valor predeterminado no está marcado.

* **Umbral** de moderaciónEspecifique el número de veces que los visitantes deben marcar un comentario antes de que se notifique a los moderadores. El valor predeterminado es una vez (**1**).

* **Límite** de marcado Escriba el número de veces que se debe marcar un comentario antes de que se oculte de la vista pública. Este número debe ser mayor o igual que el umbral **de moderación**. El valor predeterminado es 5.

### Ficha Ordenar configuración {#sort-settings-tab}

Ordenar por

Establecer como predeterminado

### Información adicional {#additional-information}

Puede encontrar más información en la página [File Library Essentials](/help/communities/essentials-file-library.md) para desarrolladores.

Para obtener información sobre la moderación de los temas y comentarios publicados, consulte [Moderación del contenido](/help/communities/moderate-ugc.md)generado por el usuario.

Para etiquetar temas y comentarios publicados, consulte [Etiquetado de contenido](/help/communities/tag-ugc.md)generado por el usuario.
