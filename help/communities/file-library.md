---
title: Función de la biblioteca de archivos
seo-title: Función de la biblioteca de archivos
description: La función Biblioteca de archivos permite que los visitantes del sitio iniciados en sesión carguen, gestionen y descarguen archivos
seo-description: La función Biblioteca de archivos permite que los visitantes del sitio iniciados en sesión carguen, gestionen y descarguen archivos
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
translation-type: tm+mt
source-git-commit: cdbe098ada0b6c50952284f92cc2063435034a38
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 9%

---


# Función de la biblioteca de archivos{#file-library-feature}

## Introducción {#introduction}

La función de biblioteca de archivos proporciona un lugar para que los visitantes del sitio que han iniciado sesión (miembros de la comunidad) carguen, gestionen y descarguen archivos dentro del sitio de la comunidad.

Esta sección de la documentación describe:

* Añadir la función de biblioteca de archivos en un sitio AEM.
* Configuración del componente `File Library`.

### Añadir una biblioteca de archivos en una página {#adding-a-file-library-to-a-page}

Para agregar un componente `File Library` a una página en modo de autor, busque el componente:

* `Communities / File Library`

y arrástrelo a su lugar en una página.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de comunidades](/help/communities/basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](/help/communities/essentials-file-library.md#essentials-for-client-side), así es como aparecerá el componente `File Library`:

![file-library1](assets/file-library1.png)

### Configuración de la biblioteca de archivos {#configuring-file-library}

Seleccione el componente `File Library` colocado para acceder y seleccione el icono `Configure` que abre el cuadro de diálogo de edición.

![configure-new](assets/configure-new.png)

![file-library2](assets/file-library2.png)

#### Ficha Comentarios {#comments-tab}

En la ficha **Comentarios**, especifique si aparecen los comentarios de los archivos cargados y cómo aparecen:

* **Permitir comentarios sobre los archivos**

   Si está activada, permita comentarios en los archivos cargados. El valor predeterminado no está marcado.

* **Comentarios por página**

   Limita el número de comentarios mostrados por página, así como el número de respuestas mostradas. El valor predeterminado es **10**.

* **Tamaño máximo de archivo**

   Este valor limitará el tamaño del archivo cargado. El límite predeterminado es 104857600 (10 Mb).

* **Longitud máxima del mensaje**

   Número máximo de caracteres que se pueden introducir en el cuadro de texto. El valor predeterminado es de 4096 caracteres.

* **Tipos de archivo permitidos**

   Lista separada por comas de extensiones de archivo con el separador &quot;punto&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permitirán los no especificados. El valor predeterminado no se especifica de forma que se permitan todos los tipos de archivo.

* **Editor de texto enriquecido**

   Si se selecciona, los comentarios se pueden introducir con marcado. El valor predeterminado no está marcado.

* **Eliminar comentarios**

   Si se selecciona, los usuarios pueden eliminar sus propios comentarios. El valor predeterminado está marcado.

* **Permitir etiquetado**

   Si se selecciona, se habilitará la capacidad de agregar una etiqueta al archivo. El valor predeterminado no está marcado.

* **Espacios de nombres permitidos**

   Si se selecciona Permitir etiquetado, las etiquetas disponibles se limitarán a las Áreas de nombres seleccionadas. Si no se marca ninguna, se permite todo. El valor predeterminado es todas las Áreas de nombres.

* **Límite de sugerencias**

   Si la opción Permitir etiquetado está activada, esta opción limita el número de etiquetas sugeridas para mostrar. Si se establece en -1, no hay límite. El valor predeterminado es -1.

* **Habilitar la votación**

   Si se selecciona, se habilitará la capacidad de votar por un archivo. El valor predeterminado no está marcado.

* **Permitir seguimiento**

   Si se selecciona, incluya la siguiente función para los artículos de blog, que permite que los miembros reciban [notificación](/help/communities/notifications.md) de los nuevos anuncios. El valor predeterminado no está marcado.

* **Habilitar la mención**

   Si está habilitada, permite que los usuarios registrados de la comunidad identifiquen a otros miembros registrados (con el nombre, apellidos y nombre de usuario) y los etiqueten con la sintaxis común @user-name. Los usuarios etiquetados reciben notificaciones sobre sus menciones.

* **Menciones máximas**

   Restringir el número máximo de menciones permitidas en una publicación. El valor predeterminado es 10.

* **Patrón de menciones en la interfaz de usuario**

   Especifique la cadena de patrón permitida para etiquetar (@mención) al usuario registrado en una publicación. Por ejemplo, ~{{familyName}}{{givenName}}.

* **Permitir respuestas de debate**

   Si está activada, permita respuestas a los comentarios publicados. El valor predeterminado no está marcado.

#### Ficha Moderación del usuario {#user-moderation-tab}

En la ficha **Moderación del usuario**, configure la moderación de los comentarios, si se permiten los comentarios:

* **Moderación previa**

   Si se selecciona, los comentarios deben aprobarse antes de que aparezcan en un sitio de publicación. El valor predeterminado no está marcado.

* **Eliminar comentarios**

   Si se selecciona, el visitante que publicó el comentario puede eliminarlo. El valor predeterminado está marcado.

* **Denegar comentarios**

   Si está activada, permita que los moderadores de miembros de confianza rechacen los comentarios. El valor predeterminado no está marcado.

* **Cerrar/abrir de nuevo los comentarios**

   Si está activada, permita que los moderadores de miembros de confianza cierren y vuelvan a abrir comentarios. El valor predeterminado no está marcado.

* **Marcar comentarios**

   Si se selecciona, permita que los visitantes marquen los comentarios como inapropiados. El valor predeterminado no está marcado.

* **Lista de motivos de indicación**

   Si se selecciona, permita que los visitantes elijan, desde una lista desplegable, el motivo por el que marcan un comentario como inapropiado. El valor predeterminado no está marcado.

* **Motivo de indicación personalizado**

   Si se selecciona, permita que los visitantes especifiquen su propio motivo para marcar un comentario como inapropiado. El valor predeterminado no está marcado.

* **Umbral de moderación**

   Escriba el número de veces que los visitantes deben marcar un comentario antes de que se notifique a los moderadores. El valor predeterminado es una vez (**1**).

* **Límite de indicación**

   Escriba el número de veces que se debe marcar un comentario antes de que se oculte de la vista pública. Este número debe ser bueno o igual al **Umbral de moderación**. El valor predeterminado es 5.

### Ficha Ordenar configuración {#sort-settings-tab}

Ordenar por

Establecer como predeterminado

### Información adicional {#additional-information}

Puede encontrar más información en la página [File Library Essentials](/help/communities/essentials-file-library.md) para desarrolladores.

Para obtener información sobre la moderación de los temas y comentarios publicados, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para etiquetar temas y comentarios publicados, consulte [Etiquetado de contenido generado por el usuario](/help/communities/tag-ugc.md).
