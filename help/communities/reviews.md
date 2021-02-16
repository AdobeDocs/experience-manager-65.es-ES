---
title: Uso del resumen de revisiones y revisiones (visualización)
seo-title: Uso del resumen de revisiones y revisiones (visualización)
description: Añadir los componentes Resumen de revisiones y revisiones en una página
seo-description: Añadir los componentes Resumen de revisiones y revisiones en una página
uuid: bd1ccee7-b26b-4a27-b1ea-89609f5080af
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: bf4e7809-8def-4647-aaa6-3ac36865511f
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 4%

---


# Uso del resumen de revisiones y revisiones (visualización) {#using-reviews-and-reviews-summary-display}

El componente `Reviews` es una composición de componentes [Comments](comments.md) y [Rating](rating.md) listos para su uso.

El componente `Reviews Summary (Display)` proporciona un resumen de una instancia activa o cerrada de un componente `Reviews` para mostrarla en cualquier parte del sitio.

>[!NOTE]
>
>No se admite la publicación anónima de una revisión. Los visitantes del sitio deben registrarse (convertirse en miembros) e iniciar sesión para participar. El visitante firmado podrá actualizar su revisión en cualquier momento.

## Añadir una revisión a una página {#adding-a-review-to-a-page}

Para agregar un componente `Reviews` a una página en modo de autor, utilice el navegador de componentes para ubicar `Communities / Reviews` y arrástrelo a su lugar en una página, como una posición relativa a la función que los usuarios deben revisar.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de comunidades](basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](reviews-basics.md#essentials-for-client-side), así es como aparecerá el componente `Reviews`.

![create-review](assets/create-review.png)

## Configuración de revisiones {#configuring-reviews}

Seleccione el componente `Reviews` colocado para acceder y seleccione el icono `Configure` que abre el cuadro de diálogo de edición.

![configure-new](assets/configure-new.png)

En la ficha **[!UICONTROL Clasificaciones permitidas]**, especifique la lista completa de las clasificaciones que se mostrarán a los miembros. La primera clasificación debe ser general o general, ya que es la clasificación la que proporciona la clasificación promedio para el componente `Review Summary (Display)`. Las dos clasificaciones siguientes de la configuración predeterminada deben tener un título diferente, que no sea &quot;Subrating 1&quot; o &quot;Subrating 2&quot;.

![permita-rating](assets/configure-review1.png)

* **[!UICONTROL Clasificaciones permitidas]**

   Lista de clasificaciones de la que un miembro puede elegir.

   Utilice la flecha arriba, la flecha abajo y los botones de eliminación para modificar las selecciones visibles.

   Haga clic en **[!UICONTROL Añadir elemento]** para agregar otra opción de clasificación.

En la ficha **[!UICONTROL Clasificaciones requeridas]**, vuelva a introducir los elementos de la lista de **[!UICONTROL Clasificaciones permitidas]** que deben clasificarse. Si un elemento solo se especifica en la ficha Clasificaciones permitidas, puede dejarse sin marcar cuando lo envíe el miembro.

En el sitio web, las clasificaciones requeridas se marcan con un asterisco. Si se requiere un elemento y se deja sin marcar, se mostrará un mensaje al miembro y se denegará el envío hasta que se marquen todas las clasificaciones necesarias.

![required-rating](assets/configure-review2.png)

* **[!UICONTROL Clasificaciones obligatorias]**

   Un subconjunto de clasificaciones permitidas, que indica qué clasificaciones son necesarias.

   Utilice la flecha arriba, la flecha abajo y los botones de eliminación para modificar las selecciones visibles.

   Haga clic en **[!UICONTROL Añadir elemento]** para agregar otra opción de respuesta.

>[!NOTE]
>
>Si se introduce un elemento en la ficha **[!UICONTROL Clasificaciones requeridas]** que no se especifica en la ficha **[!UICONTROL Clasificaciones permitidas]**, no se incluirá en los elementos a clasificar.

En la ficha **[!UICONTROL Revisiones]**, especifique cómo se administran las revisiones.

![críticas](assets/configure-review3.png)

* **[!UICONTROL Permitir respuestas]**

   Si está activada, permita respuestas a las revisiones. El valor predeterminado no está marcado.

* **[!UICONTROL Cerrado]**

   Si se selecciona, la revisión se cierra a nuevos exámenes y respuestas. El valor predeterminado no está marcado.

* **[!UICONTROL Permitir cargas de archivos]**

   Si está activada, permita que los archivos adjuntos se carguen para la revisión. El valor predeterminado no está marcado.

* **Tamaño máximo de archivo**

   Solo es relevante si **[!UICONTROL Permitir cargas de archivos]** está marcado. Este campo limita el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 10 MB.

* **[!UICONTROL Longitud máxima del mensaje]**

   Número máximo de caracteres que se pueden introducir en el cuadro de texto. El valor predeterminado es de 4096 caracteres.

* **[!UICONTROL Tipos de archivo permitidos]**

   Solo es relevante si **[!UICONTROL Permitir cargas de archivos]** está marcado. Lista separada por comas de extensiones de archivo con el separador &quot;punto&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permitirán los no especificados. El valor predeterminado no se especifica de forma que se permitan todos los tipos de archivo.

* **[!UICONTROL Editor de texto enriquecido]**

   Si se selecciona, las publicaciones se pueden introducir con marcado. El valor predeterminado no está marcado.

* **[!UICONTROL Habilitar la votación]**

   Si está activada, incluya la función de voto de un tema. El valor predeterminado no está marcado.

En la ficha **[!UICONTROL Moderación del usuario]**, especifique cómo se administran las revisiones publicadas. Para obtener más información, consulte [Moderación del contenido generado por el usuario](moderate-ugc.md).

![user-moderation](assets/configure-review4.png)

* **[!UICONTROL Moderación previa]**

   Si se selecciona, las revisiones deben aprobarse antes de que aparezcan en un sitio de publicación. El valor predeterminado no está marcado.

* **[!UICONTROL Eliminar críticas]**

   Si se selecciona, el miembro que publicó la revisión puede eliminarla. El valor predeterminado no está marcado.

* **[!UICONTROL Denegar críticas]**

   Si se selecciona, permita que los moderadores denieguen las revisiones. El valor predeterminado no está marcado.

* **[!UICONTROL Cerrar/abrir de nuevo las críticas]**

   Si se selecciona, permita que los moderadores cierren y vuelvan a abrir las revisiones. El valor predeterminado no está marcado.

* **[!UICONTROL Marcar críticas]**

   Si se selecciona, permita que los miembros marquen las revisiones como inapropiadas. El valor predeterminado no está marcado.

* **[!UICONTROL Lista de motivos de indicación]**

   Si se selecciona, permita que los miembros elijan, desde una lista desplegable, el motivo por el que marcan una revisión como inapropiada. El valor predeterminado no está marcado.

* **[!UICONTROL Motivo de indicación personalizado]**

   Si se selecciona, permita que los miembros especifiquen su propio motivo para marcar una revisión como inapropiada. El valor predeterminado no está marcado.

* **[!UICONTROL Umbral de moderación]**

   Especifique el número de veces que los miembros deben marcar una revisión antes de que se notifique a los moderadores. El valor predeterminado es una vez (1).

* **[!UICONTROL Límite de indicación]**

   Especifique el número de veces que se debe marcar una revisión antes de ocultarla de la vista pública. Este número debe ser bueno o igual al **[!UICONTROL Umbral de moderación]**. El valor predeterminado es 5.

### Añadir un resumen de revisión (visualización) en una página {#adding-a-review-summary-display-to-a-page}

Para agregar un componente `Reviews Summary (Display)` a una página en modo de autor, busque el componente

* `Communities / Reviews Summary (Display)`

y arrástrelo a su lugar en una página donde se va a mostrar un resumen de una revisión activa o cerrada.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de comunidades](basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](reviews-basics.md#essentials-for-client-side), así es como aparecerá el componente `Reviews Summary (Display)`.

![resumen de revisión](assets/configure-review5.png)

>[!NOTE]
>
>El &quot;Promedio&quot; refleja los votos del primer elemento que aparece en las fichas Clasificaciones permitidas de la revisión que se está resumiendo.

### Configuración del resumen de las revisiones (visualización) {#configuring-reviews-summary-display}

Seleccione el componente `Reviews Summary (Display)` colocado para acceder y seleccione el icono `Configure` que abre el cuadro de diálogo de edición.

![configurar](assets/configure-new.png)

En la ficha **[!UICONTROL Resumen de revisión]**

![resumen de revisión](assets/configure-review6.png)

* `Review Path`

   introduzca o busque la instancia ubicada del componente `reviews`para resumir, por ejemplo, si se agrega a la página Web del sitio [Participación en Geometrixx,](getting-started.md) la ruta sería:

   `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

   Si se selecciona, incluya la visualización de un gráfico de barras que indique cuántas de cada clasificación de estrella hay en las revisiones que se resumen. El valor predeterminado no está marcado.

### Cambiar a un tipo de revisión personalizada {#changing-to-a-custom-review-type}

El componente Reseñas utiliza el sistema de comentarios.

Al cambiar el tipo de recurso de comentarios, el sistema de comentarios ya no generará una instancia de un comentario usando el valor predeterminado, sino una instancia personalizada (ampliada) por los desarrolladores.

Una vez conocidos los tipos de recursos personalizados, introduzca [Modo de diseño](../../help/sites-authoring/default-components-designmode.md) y haga clic en el doble del componente `Comments` colocado para abrir un cuadro de diálogo con una ficha adicional.

En la ficha **[!UICONTROL Tipos de recursos]**, especifique el resourceType personalizado para nuevas instancias de los componentes `Comments or Voting`:

![comentarios-votación](assets/configure-review7.png)

* **[!UICONTROL Tipo de medio de comentario]**

   Vaya al resourceType de un componente `comment`extendido (comentario único) en /apps. Por ejemplo, `/apps/social/commons/components/hbs/comments/comment`.

   Este recurso identificará el resourceType del UGC creado cuando un visitante publica un comentario.

* **[!UICONTROL Tipo de medio de votación]**

   Vaya al resourceType de un componente `voting`extendido en /apps. Por ejemplo, `/apps/social/components/hbs/voting`.

   Este recurso identificará el tipo de recurso del UGC creado cuando un visitante publique una votación.

* **[!UICONTROL Tipo de recurso del sistema de comentarios]**

   Vaya al resourceType de un componente `comments`extendido (sistema de comentarios) en /apps. Deje en blanco a menos que la plantilla de página [incluya dinámicamente](scf.md#add-or-include-a-communities-component) el sistema de comentarios en la secuencia de comandos subyacente en lugar de agregarla a la página como un recurso (nodo de comentarios). Obtenga más información leyendo sobre el asistente [{{include}}](handlebars-helpers.md#include).

## Experiencia de Visitante del sitio {#site-visitor-experience}

### Moderadores y administradores {#moderators-and-administrators}

Cuando el usuario que ha iniciado sesión tiene privilegios de moderador o administrador, puede realizar las tareas de moderación permitidas por la configuración del componente, independientemente de quién haya creado la revisión.

### Miembros {#members}

Cuando se inicia sesión en el visitante del sitio, según la configuración, es posible que:

* Publicar una nueva revisión
* Editar su propia revisión
* Eliminar su propia revisión
* Marcar los comentarios de revisión de otros

Solo se permite una clasificación por miembro. El miembro puede cambiar su calificación en cualquier momento.

### Anónimo {#anonymous}

Los visitantes del sitio que no hayan iniciado sesión solo podrán leer las revisiones publicadas, traducirlas si son compatibles, pero no podrán agregar una clasificación o una revisión, ni marcar los comentarios de revisión de otros.

## Información adicional {#additional-information}

Puede encontrar más información en la página [Review Essentials](reviews-basics.md) para desarrolladores.

Para obtener información sobre la moderación de los comentarios publicados, consulte [Moderación del contenido generado por el usuario](moderate-ugc.md).

Para ver la traducción de los comentarios publicados, consulte [Traducción de contenido generado por el usuario](translate-ugc.md).
