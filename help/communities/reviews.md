---
title: Uso del resumen de revisiones y revisiones (visualización)
seo-title: Uso del resumen de revisiones y revisiones (visualización)
description: Adición de los componentes Resumen de revisiones y revisiones a una página
seo-description: Adición de los componentes Resumen de revisiones y revisiones a una página
uuid: bd1ccee7-b26b-4a27-b1ea-89609f5080af
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: bf4e7809-8def-4647-aaa6-3ac36865511f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Uso del resumen de revisiones y revisiones (visualización) {#using-reviews-and-reviews-summary-display}

El `Reviews`componente es una composición de [ y `Comments`](comments.md)[ `Rating`](rating.md) componentes listos para su uso.

El `Reviews Summary (Display)` componente proporciona un resumen de una instancia activa o cerrada de un `Reviews` componente para que se muestre en cualquier parte del sitio.

>[!NOTE]
>
>No se admite la publicación anónima de una revisión. Los visitantes del sitio deben registrarse (convertirse en miembros) e iniciar sesión para participar. El visitante que ha iniciado sesión puede actualizar su revisión en cualquier momento.

## Adding a Review to a Page {#adding-a-review-to-a-page}

Para agregar un `Reviews` componente a una página en modo de autor, utilice el navegador de componentes para ubicarlo `Communities / Reviews` y arrastrarlo hasta su lugar en una página, como una posición relativa a la función que los usuarios pueden revisar.

Para obtener la información necesaria, visite [Communities Components Basics](basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se incluyen las bibliotecas [del lado del cliente](reviews-basics.md#essentials-for-client-side) necesarias, así es como aparecerá el `Reviews`componente.

![chlimage_1-340](assets/chlimage_1-340.png)

## Configuración de las revisiones {#configuring-reviews}

Seleccione el componente colocado al que desea acceder y seleccione el `Reviews` `Configure` icono que abre el cuadro de diálogo de edición.

![chlimage_1-341](assets/chlimage_1-341.png)

En la ficha Clasificaciones **** permitidas, especifique la lista completa de clasificaciones que se mostrarán a los miembros. La primera calificación debe ser general o general, ya que es la calificación la que proporciona la calificación media del `Review Summary (Display)` componente. Las dos clasificaciones siguientes de la configuración predeterminada deben tener un título diferente, que no sea &quot;Subrating 1&quot; o &quot;Subrating 2&quot;.

![chlimage_1-342](assets/chlimage_1-342.png)

* **[!UICONTROL Clasificaciones permitidas]**

   Una lista de clasificaciones de las que un miembro puede elegir.

   Utilice la flecha arriba, la flecha abajo y los botones de eliminación para modificar las selecciones visibles.

   Haga clic en **[!UICONTROL Agregar elemento]** para agregar otra opción de clasificación.

En la ficha Clasificaciones **** requeridas, vuelva a introducir los elementos de la lista de Clasificaciones **** permitidas que deben clasificarse. Si un elemento solo se especifica en la ficha Clasificaciones permitidas, puede dejarse sin marcar cuando lo envíe el miembro.

En el sitio web, las clasificaciones requeridas se marcan con un asterisco. Si se requiere un elemento y se deja sin marcar, se mostrará un mensaje al miembro y se denegará el envío hasta que se marquen todas las clasificaciones necesarias.

![chlimage_1-343](assets/chlimage_1-343.png)

* **[!UICONTROL Clasificaciones obligatorias]**

   Un subconjunto de clasificaciones permitidas, que indica qué clasificaciones son necesarias.

   Utilice la flecha arriba, la flecha abajo y los botones de eliminación para modificar las selecciones visibles.

   Haga clic en **[!UICONTROL Agregar elemento]** para agregar otra opción de respuesta.

>[!NOTE]
>
>Si se introduce un elemento en la ficha Clasificaciones **** requeridas que no se especifica en la ficha Clasificaciones **** permitidas, no se incluirá en los elementos a clasificar.

En la ficha **[!UICONTROL Revisiones]** , especifique cómo se administran las revisiones.

![chlimage_1-340](assets/chlimage_1-344.png)

* **[!UICONTROL Permitir respuestas]** Si está activada, permita respuestas a las revisiones. El valor predeterminado no está marcado.

* **[!UICONTROL Cerrada]** Si se selecciona, la revisión se cierra a nuevos exámenes y respuestas. El valor predeterminado no está marcado.

* **[!UICONTROL Permitir cargas]** de archivos Si está activada, permita que los archivos adjuntos se carguen para la revisión. El valor predeterminado no está marcado.

* **Tamaño **máximo del archivo relevante solo si está activada la opción**[!UICONTROL Permitir cargas ]**de archivos. Este campo limita el tamaño (en bytes) de un archivo cargado. El valor predeterminado es 10 MB.

* **[!UICONTROL Longitud]** máxima del mensaje Número máximo de caracteres que se pueden introducir en el cuadro de texto. El valor predeterminado es de 4096 caracteres.

* **[!UICONTROL Tipos]** de archivo permitidos solo si está activada la opción **[!UICONTROL Permitir cargas]** de archivos. Una lista separada por comas de extensiones de archivo con el separador &quot;punto&quot;. Por ejemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Si se especifica algún tipo de archivo, no se permitirán los no especificados. El valor predeterminado no se especifica de forma que se permitan todos los tipos de archivo.

* **[!UICONTROL Editor]** de texto enriquecido Si está marcado, los anuncios se pueden introducir con marcado. El valor predeterminado no está marcado.

* **[!UICONTROL Permitir voto]** Si está activada, incluya la función de voto de un tema. El valor predeterminado no está marcado.

En la ficha Moderación **[!UICONTROL del]** usuario, especifique cómo se administran las revisiones publicadas. Para obtener más información, consulte [Moderación del contenido](moderate-ugc.md)generado por el usuario.

![chlimage_1-345](assets/chlimage_1-345.png)

* **[!UICONTROL Premoderación]** Si está activada, las revisiones deben aprobarse antes de que aparezcan en un sitio de publicación. El valor predeterminado no está marcado.

* **[!UICONTROL Eliminar críticas]** Si se selecciona, el miembro que publicó la revisión puede eliminarla. El valor predeterminado no está marcado.

* **[!UICONTROL Denegar revisiones]** Si se selecciona, permita que los moderadores rechacen las revisiones. El valor predeterminado no está marcado.

* **[!UICONTROL Cerrar/volver a abrir revisiones]** Si está activada, permita que los moderadores cierren y vuelvan a abrir las revisiones. El valor predeterminado no está marcado.

* **[!UICONTROL Marcar revisiones]** Si está activada, permite a los miembros marcar las revisiones como inapropiadas. El valor predeterminado no está marcado.

* **[!UICONTROL Marcar lista]** de motivos Si está activada, permita que los miembros elijan, en una lista desplegable, el motivo por el que marcan una revisión como inapropiada. El valor predeterminado no está marcado.

* **[!UICONTROL Razón]** de marca personalizada Si está activada, permita que los miembros introduzcan su propio motivo para marcar una revisión como inapropiada. El valor predeterminado no está marcado.

* **[!UICONTROL Umbral]** de moderaciónIntroduzca el número de veces que los miembros deben marcar una revisión antes de que se notifique a los moderadores. El valor predeterminado es una vez (1).

* **[!UICONTROL Límite]** de marcado Especifique el número de veces que se debe marcar una revisión antes de que se oculte de la vista pública. Este número debe ser mayor o igual que el umbral **[!UICONTROL de moderación]**. El valor predeterminado es 5.

### Adición de un resumen de revisión (visualización) a una página {#adding-a-review-summary-display-to-a-page}

Para agregar un `Reviews Summary (Display)` componente a una página en modo de autor, ubique el componente

* `Communities / Reviews Summary (Display)`

y arrástrelo a su lugar en una página donde se va a mostrar un resumen de una revisión activa o cerrada.

Para obtener la información necesaria, visite [Communities Components Basics](basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se incluyen las bibliotecas [del lado del cliente](reviews-basics.md#essentials-for-client-side) necesarias, así es como aparecerá el `Reviews Summary (Display)`componente.

![chlimage_1-346](assets/chlimage_1-346.png)

>[!NOTE]
>
>El &quot;Promedio&quot; refleja los votos del primer elemento que aparece en las fichas Clasificaciones permitidas de la revisión que se está resumiendo.

### Configuración del resumen de las revisiones (visualización) {#configuring-reviews-summary-display}

Seleccione el componente colocado al que desea acceder y seleccione el `Reviews Summary (Display)` `Configure` icono que abre el cuadro de diálogo de edición.

![chlimage_1-347](assets/chlimage_1-347.png)

En la ficha **[!UICONTROL Revisar resumen]**

![chlimage_1-348](assets/chlimage_1-348.png)

* `Review Path`

   introduzca o busque la instancia colocada del `reviews`componente para resumir, por ejemplo, si se agrega a la página Web del sitio de participación de [Geometrixx,](getting-started.md) la ruta sería:

   /content/sites/engagement/es/page/jcr:content/content/Primary/views

* `Include histogram`

   Si se selecciona, incluya la visualización de un gráfico de barras que indique cuántas de cada clasificación de estrella hay en las revisiones que se resumen. El valor predeterminado no está marcado.

### Cambio a un tipo de revisión personalizada {#changing-to-a-custom-review-type}

El componente Reseñas utiliza el sistema de comentarios.

Al cambiar el tipo de recurso de comentarios, el sistema de comentarios ya no generará una instancia de un comentario usando el valor predeterminado, sino una instancia personalizada (ampliada) por los desarrolladores.

Una vez conocidos los tipos de recursos personalizados, introduzca el modo [de](../../help/sites-authoring/default-components-designmode.md) diseño y haga doble clic en el componente `Comments` colocado para abrir un cuadro de diálogo con una ficha adicional.

En la ficha Tipos **[!UICONTROL de]** recursos, especifique el resourceType personalizado para las nuevas instancias de los `Comments or Voting`componentes:

![chlimage_1-349](assets/chlimage_1-349.png)

* **[!UICONTROL Tipo de medio de comentario]**

   Vaya al resourceType de un `comment`componente extendido (un solo comentario) en /apps. Por ejemplo, `/apps/social/commons/components/hbs/comments/comment`

   Este recurso identifica el resourceType del UGC creado cuando un visitante publica un comentario.

* **[!UICONTROL Tipo de medio de votación]**

   Vaya al resourceType de un `voting`componente extendido en /apps. Por ejemplo, `/apps/social/components/hbs/voting`

   Este recurso identificará el tipo de recurso del UGC creado cuando un visitante publica una votación.

* **[!UICONTROL Tipo de recurso del sistema de comentarios]**

   Vaya al resourceType de un `comments`componente extendido (sistema de comentarios) en /apps. Deje en blanco a menos que la plantilla de página incluya [](scf.md#add-or-include-a-communities-component) dinámicamente el sistema de comentarios en la secuencia de comandos subyacente en lugar de agregarlo a la página como recurso (nodo de comentarios). Obtenga más información leyendo sobre el asistente [{{include}}](handlebars-helpers.md#include)

## Experiencia del visitante del sitio {#site-visitor-experience}

### Moderadores y administradores {#moderators-and-administrators}

Cuando el usuario que ha iniciado sesión tiene privilegios de moderador o administrador, puede realizar las tareas de moderación permitidas por la configuración del componente, independientemente de quién haya creado la revisión.

### Miembros {#members}

Cuando el visitante del sitio ha iniciado sesión, según la configuración, es posible que

* Publicar una nueva revisión
* Editar su propia revisión
* Eliminar su propia revisión
* Marcar los comentarios de revisión de otros

Solo se permite una clasificación por miembro. El miembro puede cambiar su calificación en cualquier momento.

### Anónimo {#anonymous}

Los visitantes del sitio que no hayan iniciado sesión sólo podrán leer las revisiones publicadas, traducirlas si son compatibles, pero no podrán agregar una clasificación o una revisión, ni marcar los comentarios de revisión de otros.

## Información adicional {#additional-information}

Puede encontrar más información en la página [Revisar elementos esenciales](reviews-basics.md) para desarrolladores.

Para moderar los comentarios publicados, consulte [Moderación del contenido](moderate-ugc.md)generado por el usuario.

Para ver la traducción de los comentarios publicados, consulte [Traducción de contenido](translate-ugc.md)generado por el usuario.
