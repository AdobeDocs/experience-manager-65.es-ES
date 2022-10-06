---
title: Función de la biblioteca de archivos
seo-title: File Library Feature
description: La función Biblioteca de archivos permite a los visitantes del sitio que inician sesión cargar, administrar y descargar archivos
seo-description: The File Library feature lets signed-in site visitors upload, manage, and download files
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
exl-id: 05cfaab5-a12d-475f-9095-a9fb13571d0a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 9%

---

# Función de la biblioteca de archivos{#file-library-feature}

## Introducción {#introduction}

La función de biblioteca de archivos proporciona un lugar donde los visitantes del sitio que han iniciado sesión (miembros de la comunidad) pueden cargar, administrar y descargar archivos dentro del sitio de la comunidad.

Esta sección de la documentación describe:

* Adición de la función de biblioteca de archivos a un sitio AEM.
* Ajustes de configuración para `File Library` componente.

### Adición de una biblioteca de archivos a una página {#adding-a-file-library-to-a-page}

Para agregar un `File Library` a una página en modo de autor, ubique el componente:

* `Communities / File Library`

y arrástrela a su lugar en una página.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de Communities](/help/communities/basics.md).

Cuando la variable [bibliotecas requeridas del lado del cliente](/help/communities/essentials-file-library.md#essentials-for-client-side) se incluyen, así es como se muestra la variable `File Library` aparecerá el componente:

![file-library1](assets/file-library1.png)

### Configuración de la biblioteca de archivos {#configuring-file-library}

Seleccione la colocación `File Library` para acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configure-new](assets/configure-new.png)

![file-library2](assets/file-library2.png)

#### Ficha Comentarios {#comments-tab}

En el **Comentarios** especifique si aparecen los comentarios de los archivos cargados y cómo aparecerán:

* **Permitir comentarios sobre los archivos**

   Si está activada, permita que se comenten los archivos cargados. El valor predeterminado no está seleccionado.

* **Comentarios por página**

   Limita el número de comentarios mostrados por página, así como el número de respuestas mostradas. El valor predeterminado es **10**.

* **Tamaño máximo de archivo**

   Este valor limitará el tamaño del archivo cargado. El límite predeterminado es 104857600 (10 Mb).

* **Longitud máxima del mensaje**

   Número máximo de caracteres que se pueden introducir en el cuadro de texto. El valor predeterminado es de 4096 caracteres.

* **Tipos de archivo permitidos**

   Lista de extensiones de archivo separados por coma con el separador &quot;punto&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permitirán los no especificados. El valor predeterminado no se especifica de modo que se permitan todos los tipos de archivo.

* **Editor de texto enriquecido**

   Si se selecciona, los comentarios pueden introducirse con marcado. El valor predeterminado no está seleccionado.

* **Eliminar comentarios**

   Si se selecciona, los usuarios pueden eliminar sus propios comentarios. El valor predeterminado está marcado.

* **Permitir etiquetado**

   Si se selecciona, se habilita la capacidad de agregar una etiqueta al archivo. El valor predeterminado no está seleccionado.

* **Espacios de nombres permitidos**

   Si se selecciona Permitir etiquetado , las etiquetas disponibles se limitarán a los espacios de nombres marcados. Si no se selecciona ninguno, se permiten todos. El valor predeterminado son todas las áreas de nombres.

* **Límite de sugerencias**

   Si la opción Permitir etiquetado está activada, esta opción limita el número de etiquetas sugeridas para mostrar. Si se establece en -1, no hay límite. El valor predeterminado es -1.

* **Habilitar la votación**

   Si se selecciona, se habilitará la capacidad de votar para un archivo. El valor predeterminado no está seleccionado.

* **Permitir seguimiento**

   Si está marcada esta opción, incluya la siguiente característica para artículos de blog, que permite que los miembros sean [notificadas](/help/communities/notifications.md) de nuevos puestos. El valor predeterminado no está seleccionado.

* **Habilitar la mención**

   Si está habilitado, permite a los usuarios registrados de la comunidad identificar a otros miembros registrados (con el nombre, apellidos y nombre de usuario) y etiquetarlos con la sintaxis común @user-name . Los usuarios etiquetados reciben notificaciones sobre sus menciones.

* **Menciones máximas**

   Restringir el número máximo de menciones permitidas en un anuncio. El valor predeterminado es 10.

* **Patrón de menciones en la interfaz de usuario**

   Especifique la cadena de patrón permitida para etiquetar (@mention) al usuario registrado en una publicación. Por ejemplo ~{{familyName}}{{givenName}}.

* **Permitir respuestas de debate**

   Si está activado, permita que las respuestas a los comentarios publicados. El valor predeterminado no está seleccionado.

#### Pestaña Moderación del usuario {#user-moderation-tab}

En el **Moderación del usuario** , configure la moderación de los comentarios si se permiten comentarios :

* **Moderación previa**

   Si se selecciona, los comentarios deben aprobarse antes de que aparezcan en un sitio de publicación. El valor predeterminado no está seleccionado.

* **Eliminar comentarios**

   Si se selecciona, el visitante que publicó el comentario tiene la capacidad de eliminarlo. El valor predeterminado está marcado.

* **Denegar comentarios**

   Si está activada, permita que los moderadores miembros de confianza rechacen los comentarios. El valor predeterminado no está seleccionado.

* **Cerrar/abrir de nuevo los comentarios**

   Si está marcada esta opción, permita que los moderadores miembros de confianza cierren y vuelvan a abrir los comentarios. El valor predeterminado no está seleccionado.

* **Marcar comentarios**

   Si está marcada esta opción, permita a los visitantes marcar comentarios como inapropiados. El valor predeterminado no está seleccionado.

* **Lista de motivos de indicación**

   Si está marcada esta opción, permita a los visitantes elegir, desde una lista desplegable, el motivo por el que marcan un comentario como inapropiado. El valor predeterminado no está seleccionado.

* **Motivo de indicación personalizado**

   Si está marcada esta opción, permita que los visitantes especifiquen su propio motivo para marcar un comentario como inapropiado. El valor predeterminado no está seleccionado.

* **Umbral de moderación**

   Especifique el número de veces que los visitantes deben marcar un comentario antes de que se notifique a los moderadores. El valor predeterminado es una vez (**1**).

* **Límite de indicación**

   Introduzca el número de veces que se debe marcar un comentario antes de ocultarlo de la vista pública. Este número debe ser bueno o igual que la variable **Umbral de moderación**. El valor predeterminado es 5.

### Ficha Ordenar configuración {#sort-settings-tab}

Ordenar por

Establecer como predeterminado

### Información adicional {#additional-information}

Puede encontrar más información en la [Elementos esenciales de la biblioteca de archivos](/help/communities/essentials-file-library.md) para desarrolladores.

Para moderar los temas y comentarios publicados, consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para etiquetar temas y comentarios publicados, consulte [Etiquetado del contenido generado por el usuario](/help/communities/tag-ugc.md).
