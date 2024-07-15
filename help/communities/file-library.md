---
title: Función Biblioteca de archivos
description: La función Biblioteca de archivos permite que los visitantes del sitio que inicien sesión carguen, administren y descarguen archivos.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 05cfaab5-a12d-475f-9095-a9fb13571d0a
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 1%

---

# Función Biblioteca de archivos{#file-library-feature}

## Introducción {#introduction}

La función de biblioteca de archivos proporciona un lugar para que los visitantes del sitio que han iniciado sesión (miembros de la comunidad) carguen, administren y descarguen archivos dentro del sitio de la comunidad.

Esta sección de la documentación describe lo siguiente:

* AEM Agregar la función de biblioteca de archivos a un sitio de la.
* Ajustes de configuración para el componente `File Library`.

### Agregar una biblioteca de archivos a una página {#adding-a-file-library-to-a-page}

Para agregar un componente `File Library` a una página en modo de autor, busque el componente:

* `Communities / File Library`

Y arrástrela a su lugar en una página.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](/help/communities/basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](/help/communities/essentials-file-library.md#essentials-for-client-side), así es como aparece el componente `File Library`:

![biblioteca de archivos1](assets/file-library1.png)

### Configurar la biblioteca de archivos {#configuring-file-library}

Seleccione el componente `File Library` colocado para que pueda acceder y seleccionar el icono `Configure` que abre el cuadro de diálogo de edición.

![configurar-nuevo](assets/configure-new.png)

![biblioteca de archivos2](assets/file-library2.png)

#### Pestaña Comentarios {#comments-tab}

En la ficha **Comentarios**, especifique si los comentarios de los archivos cargados aparecen y cómo:

* **Permitir comentarios sobre los archivos**

  Si se selecciona esta opción, se permiten comentarios sobre los archivos cargados. El valor predeterminado está desmarcado.

* **Comentarios por página**

  Limita el número de comentarios que se muestran por página y el número de respuestas que se muestran. El valor predeterminado es **10**.

* **Tamaño máximo de archivo**

  Este valor limita el tamaño del archivo cargado. El límite predeterminado es 104857600 (10 MB).

* **Longitud máxima del mensaje**

  Número máximo de caracteres que pueden introducirse en el cuadro de texto. El valor predeterminado es de 4096 caracteres.

* **Tipos de archivo permitidos**

  Lista separada por comas de las extensiones de archivo con el separador de &quot;puntos&quot;. Por ejemplo, .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permitirán los tipos de archivo que no se especifiquen. No se ha especificado el valor predeterminado de modo que se permitan todos los tipos de archivo.

* **Editor de texto enriquecido**

  Si se selecciona, los comentarios se pueden introducir con marcado. El valor predeterminado está desmarcado.

* **Eliminar comentarios**

  Si se selecciona, los usuarios pueden eliminar sus propios comentarios. La opción predeterminada está activada.

* **Permitir etiquetado**

  Si se selecciona, se habilita la capacidad de agregar una etiqueta al archivo. El valor predeterminado está desmarcado.

* **Áreas de nombres permitidas**

  Si la opción Permitir etiquetado está activada, las etiquetas disponibles se limitan a las áreas de nombres seleccionadas. Si no se comprueban áreas de nombres, se permiten todas. El valor predeterminado es todas las áreas de nombres.

* **Límite de sugerencias**

  Si la opción Permitir etiquetado está activada, esta configuración limita el número de etiquetas sugeridas que se deben mostrar. Si se establece en -1, no hay límite. El valor predeterminado es -1.

* **Permitir Votación**

  Si se selecciona, se habilita la capacidad de votar por un archivo. El valor predeterminado está desmarcado.

* **Permitir seguimiento**

  Si se selecciona esta opción, se debe incluir la siguiente característica para artículos de blog, que permite [notificar](/help/communities/notifications.md) a los miembros las nuevas publicaciones. El valor predeterminado está desmarcado.

* **Habilitar la mención**

  Si está habilitada, permite a los usuarios de la comunidad registrada identificar a otros miembros registrados (mediante nombre, apellidos y nombre de usuario) y etiquetarlos con la sintaxis común de @user-name. Los usuarios etiquetados reciben notificaciones sobre sus menciones.

* **Menciones máximas**

  Restringir el número máximo de menciones permitidas en una publicación. El valor predeterminado es 10.

* **Patrón de mención de IU**

  Especifique la cadena de patrón permitida para etiquetar (@mention) al usuario registrado en una publicación. Por ejemplo, `~{{familyName}}{{givenName}}`.

* **Permitir respuestas de subprocesos**

  Si está activado, permitir respuestas a comentarios publicados. El valor predeterminado está desmarcado.

#### Pestaña Moderación de usuario {#user-moderation-tab}

En la ficha **Moderación de usuarios**, configure la moderación de los comentarios, si se permiten los comentarios:

* **Moderación previa**

  Si se selecciona, los comentarios deben aprobarse antes de aparecer en un sitio de publicación. El valor predeterminado está desmarcado.

* **Eliminar comentarios**

  Si se selecciona, el visitante que publicó el comentario puede eliminarlo, si lo desea. La opción predeterminada está activada.

* **Denegar comentarios**

  Si se selecciona esta opción, se permite que los moderadores de confianza denieguen comentarios. El valor predeterminado está desmarcado.

* **Cerrar/volver a abrir comentarios**

  Si se selecciona esta opción, permite que los moderadores de miembros de confianza cierren y abran de nuevo los comentarios. El valor predeterminado está desmarcado.

* **Marcar comentarios**

  Si se selecciona, permite que los visitantes marquen los comentarios como inadecuados. El valor predeterminado está desmarcado.

* **Lista de motivos de marca**

  Si se selecciona esta opción, se permite a los visitantes elegir, en una lista desplegable, el motivo por el que marcan un comentario como inapropiado. El valor predeterminado está desmarcado.

* **Motivo de indicación personalizado**

  Si se selecciona, permite que los visitantes especifiquen su propio motivo para marcar un comentario como inapropiado. El valor predeterminado está desmarcado.

* **Umbral de moderación**

  Introduzca el número de veces que los visitantes deben marcar un comentario antes de notificarlo a los moderadores. El valor predeterminado es una vez (**1**).

* **Límite de indicación**

  Introduzca el número de veces que se debe marcar un comentario antes de ocultarlo de la vista pública. Este número debe ser mayor o igual que el **umbral de moderación**. El valor predeterminado es 5.

### Pestaña Configuración de ordenación {#sort-settings-tab}

Ordenar por

Establecer como predeterminado

### Información adicional {#additional-information}

Encontrará más información en la página de [File Library Essentials](/help/communities/essentials-file-library.md) para desarrolladores.

Para moderar los temas publicados y los comentarios, vea [Moderar el contenido generado por el usuario](/help/communities/moderate-ugc.md).

Para etiquetar temas y comentarios publicados, consulte [Etiquetado de contenido generado por el usuario](/help/communities/tag-ugc.md).
