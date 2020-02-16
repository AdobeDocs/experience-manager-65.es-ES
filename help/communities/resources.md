---
title: Consola de recursos de habilitación
seo-title: Consola de recursos de habilitación
description: La consola Recursos es donde los administradores de habilitación crean, administran y asignan recursos a los miembros de un sitio de comunidad de habilitación
seo-description: La consola Recursos es donde los administradores de habilitación crean, administran y asignan recursos a los miembros de un sitio de comunidad de habilitación
uuid: 52445b39-c339-4b39-8004-eb36de99bced
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1ef15e76-fe7c-4ced-a20d-c0a9385e3ee4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Consola de recursos de habilitación {#enablement-resources-console}

En AEM Communities, la consola Recursos es donde los administradores de [habilitación](users.md) crean, administran y asignan recursos a los miembros de un sitio de la comunidad de habilitación.

## Requisitos {#requirements}

Antes de agregar recursos de habilitación para un sitio de comunidad, las instancias de AEM deben configurarse correctamente, como:

* SCORM
* FFmpeg

Para obtener más información, consulte [Configuración de la habilitación](enablement.md).

>[!CAUTION]
>
>Si SCORM se instala después de la creación del sitio de la comunidad, se deben volver a crear los recursos de habilitación presentes antes de la instalación de SCORM.

>[!NOTE]
>
>Con el lanzamiento de [AEM 6.3](deploy-communities.md#latestfeaturepack) y los paquetes de funciones equivalentes de Communities, [AEM 6.2 FP3](deploy-communities.md#latestfeaturepack) y [AEM 6.1 FP7](https://docs.adobe.com/content/docs/en/aem/6-1/deploy/communities.html#Latest Feature Pack), la función de habilitación ya no requiere una base de datos [](mysql.md)MySQL.

## Terminología {#terminology}

### Medio {#resource}

Los recursos son esenciales para una comunidad [de](overview.md#enablement-community)habilitación. Son los materiales asignados a los miembros que les permiten mejorar sus habilidades.

Características de un recurso:

* Puede ser de tipo
   * Imagen (JPG, PNG, GIF, BMP)
   * Vídeo (MP4)
   * Flash (SWF)
   * Documento (PDF)
   * Prueba (SCORM)
* Se puede hacer referencia desde una o más rutas de aprendizaje

### Ruta de aprendizaje {#learning-path}

Una ruta de aprendizaje es un conjunto lógico de recursos de habilitación agrupados para facilitar la asignación a los miembros.

### Grupo de miembros {#members-group}

Cuando se crea un sitio de comunidad, el nombre asignado al sitio para la dirección URL se utiliza en la creación de grupos [de usuarios específicos del](users.md) sitio configurados con distintos permisos para diversas funciones. Todos estos grupos creados automáticamente llevan el prefijo `Community *<site-name>*`.

Uno de estos grupos de usuarios es `Community *<site-name>* Members` el grupo, que identifica a los usuarios registrados en el entorno de publicación como miembros de la comunidad. Consulte el tutorial [Introducción a Comunidades de AEM para habilitar](getting-started-enablement.md) , por ejemplo.

Para las comunidades [de](overview.md#egagementcommunity)participación, es razonable permitir que los visitantes del sitio se automatriculen o utilicen el inicio de sesión social, en cuyo momento se agregan automáticamente al grupo de miembros.

Para las comunidades [de](overview.md#enablement-community)activación, se recomienda convertir el sitio en privado, lo que requiere un administrador para agregar usuarios al grupo de miembros.

## Acceso a los recursos de habilitación de un sitio de la comunidad {#accessing-a-community-site-s-enablement-resources}

### Navegar a los recursos de comunidades {#navigate-to-communities-resources}

En el entorno de creación, para acceder a la consola Recursos

* Desde la navegación global: **[!UICONTROL Navegación > Comunidades > Recursos]**

![chlimage_1-163](assets/chlimage_1-163.png)

### Seleccionar un sitio de comunidad {#select-a-community-site}

La consola Recursos de comunidades mostrará todos los sitios de la comunidad.

Los recursos de habilitación se crean para un sitio de comunidad específico después de seleccionar el sitio desde la consola Recursos.

Una vez seleccionado un sitio de comunidad específico, se puede acceder a los recursos de habilitación y las rutas de aprendizaje existentes para la administración y modificación, y se pueden crear nuevos recursos de habilitación y rutas de aprendizaje.

![chlimage_1-164](assets/chlimage_1-164.png)

#### Búsqueda {#search-features}

![chlimage_1-165](assets/chlimage_1-165.png)

Seleccione el icono de alternancia del panel lateral para buscar un recurso de habilitación o una ruta de aprendizaje. Cuando se selecciona, se abre un panel de búsqueda en el lado izquierdo de la consola y proporciona un cuadro de texto en el que se pueden introducir términos de búsqueda.

![chlimage_1-166](assets/chlimage_1-166.png)

#### Modo de selección {#selection-mode}

Para seleccionar varios recursos de habilitación, seleccione el primero pasando el ratón por encima de la tarjeta y seleccionando el icono de marca de verificación. Una vez seleccionada, si selecciona cualquier otra tarjeta, se agregará al grupo de selección. Al seleccionar una segunda vez se anula la selección de la tarjeta.

![chlimage_1-167](assets/chlimage_1-167.png)

## Crear un recurso {#create-a-resource}

![chlimage_1-168](assets/chlimage_1-168.png)

Para agregar un nuevo recurso de habilitación al sitio de comunidad

* Seleccione el icono `Create`
* En el submenú que se muestra, seleccione `Resource`

Esto inicia un proceso paso a paso de

* Descripción del recurso (nombre, imagen de tarjeta y texto)
* Selección del contenido del recurso
* Selección de una imagen de portada para el recurso
* Identificación de contactos de recursos
* Asignación de recursos a miembros

Cuando el recurso forma parte de un curso, una ruta de aprendizaje, los miembros solo se deben asignar a la ruta de aprendizaje. Las asignaciones se pueden agregar después de crear el recurso de habilitación.

### 1 Basic Info {#basic-info}

![chlimage_1-169](assets/chlimage_1-169.png)

* **[!UICONTROL Agregar imagen]**

   (*opcional*) Imagen que se muestra en la tarjeta para el recurso de habilitación en la página de asignaciones del miembro, así como en la consola Recursos. La imagen se selecciona en el sistema de archivos local del servidor. Si no se proporciona una imagen, se generará una miniatura para el recurso cargado.

   ***Nota***: el tamaño de imagen recomendado no es simplemente 480 x 480 píxeles. Debido al diseño interactivo de las tarjetas con diversas dimensiones del navegador, el tamaño de visualización variará de 220 x 165 píxeles a 400 x 165 píxeles.

* **[!UICONTROL Nombre del sitio]**

   (solo *lectura*) El sitio de la comunidad al que se agrega el recurso.

* **[!UICONTROL Nombre&amp;amp de recurso;ast;]**

   (*obligatorio*) El nombre para mostrar del recurso. Se crea un nombre de nodo válido a partir del nombre para mostrar.

* **[!UICONTROL Etiquetas]**

   (*opcional*) Se pueden elegir una o varias etiquetas que asocien el recurso de habilitación con uno o varios catálogos. Consulte [Etiquetado de recursos](tag-resources.md)de habilitación.

* **[!UICONTROL Mostrar en el catálogo]**

   Cuando está desactivada, el recurso de habilitación no aparecerá en ningún catálogo. Si se selecciona, el recurso de habilitación aparecerá en todos los catálogos a menos que se filtre [previamente](catalog-developer-essentials.md#pre-filters) o que se filtre el miembro desde la interfaz de usuario. El valor predeterminado no está marcado.

* **[!UICONTROL Descripción]**

   (*opcional*) La descripción que se mostrará para el recurso de habilitación.

* **[!UICONTROL Recurso pequeño]**

   (*opcional*) Seleccionado en Recursos AEM. Imagen en miniatura para representar el recurso en el entorno de publicación, como en un catálogo.

* **[!UICONTROL Recurso grande]**

   (*opcional*) Seleccionado en Recursos AEM. Imagen grande que representa el recurso en el entorno de publicación, como en la página principal de un recurso.

* **[!UICONTROL Recurso de fragmento de contenido]**

   (*opcional*) Seleccionado en Recursos AEM. Un fragmento de contenido al que se puede hacer referencia en el entorno de publicación, pero que no está en uso de forma predeterminada.

* Seleccione **[!UICONTROL Siguiente]**

### 2 Add Content {#add-content}

![chlimage_1-170](assets/chlimage_1-170.png)

Aunque parece que se pueden seleccionar varios recursos de habilitación, solo se permite uno.

Seleccione el `'+' icon`, en la esquina superior derecha, para comenzar el proceso de selección del recurso identificando el origen.

![chlimage_1-171](assets/chlimage_1-171.png)

* **[!UICONTROL Cargar desde mis archivos]** locales La carga desde el sistema de archivos local utilizará el navegador de archivos nativo para seleccionar y cargar un archivo. Los tipos de archivo admitidos son SCORM.zip (HTML5 o SWF), vídeo MP4, SWF, PDF y tipos de imagen (JPG, PNG, GIF, BMP). El nombre de archivo se convierte en el nombre del recurso, que se agrega a la biblioteca de recursos.

* **[!UICONTROL Examinar biblioteca]** de recursosSeleccione una opción de la biblioteca de recursos. La selección está limitada a aquellos que son visibles dentro del sitio de la comunidad.

* **[!UICONTROL Añadir URL externa]**

   Introduzca un vínculo al contenido de aprendizaje.

   En el cuadro de diálogo que se abre, introduzca:

   * **[!UICONTROL Título]**

      Nombre del recurso para el recurso de habilitación.

   * **[!UICONTROL URL]**

      Dirección URL de un recurso.

* **[!UICONTROL Añadir una URL de Adobe Connect]**

   Introduzca un vínculo a una sesión de Adobe Connect.

   En el cuadro de diálogo que se abre, introduzca:

   * **[!UICONTROL Título]**

      Nombre del recurso para el recurso de habilitación.

   * **[!UICONTROL URL]**

      Dirección URL de una sesión de Adobe Connect.

* **[!UICONTROL Definir un medio externo]**

   Introduzca la ubicación en la que se presentará el material. Los valores del estado y la puntuación de éxito se introducen manualmente (consulte [Informes](reports.md)). Se puede utilizar una imagen de portada cargada para proporcionar información adicional.

   En el cuadro de diálogo que se abre, introduzca:

   * **[!UICONTROL Título]**

      Nombre del recurso para el recurso de habilitación.

   * **[!UICONTROL Ubicación]**

      Ubicación de un sitio físico, como una clase.

#### Ejemplo de un recurso de vídeo añadido {#example-of-an-added-video-resource}

![chlimage_1-172](assets/chlimage_1-172.png)

* **[!UICONTROL Imagen de portada del medio]**

   La imagen de portada es una imagen que se mostrará cuando se vea por primera vez el recurso de habilitación. Por ejemplo, la imagen de portada se muestra cuando todavía no se está reproduciendo un recurso de vídeo. Si no se carga una imagen personalizada, se muestra una imagen predeterminada. En el caso de los recursos de vídeo, es posible [generar una miniatura](enablement.md#ffmpeg), pero solo cuando se carga y no cuando se hace referencia al vídeo como URL. Para los recursos de ubicación, la imagen se puede utilizar para proporcionar información adicional.

   El tamaño recomendado para la imagen de portada es de 640 x 360 píxeles.

* Seleccione **[!UICONTROL Siguiente]**

### 3 Settings {#settings}

![chlimage_1-173](assets/chlimage_1-173.png)

>[!NOTE]
>
>Los alumnos no deben matricularse directamente en los recursos de habilitación a los que se hará referencia desde una ruta de aprendizaje. Los alumnos solo deben estar matriculados en la ruta de aprendizaje.
>
>Si un miembro está matriculado en un recurso y en una ruta de aprendizaje que hace referencia a ese recurso, sus asignaciones mostrarán tanto el recurso único como el recurso dentro de la ruta de aprendizaje.

* **[!UICONTROL Entornos sociales]**

   Esta configuración controla si los alumnos pueden o no proporcionar información sobre el recurso de habilitación. La configuración [de](sites-console.md#moderation) moderación es la del sitio de la comunidad principal.

   * **[!UICONTROL Permitir comentarios]**

      Si se selecciona, los miembros pueden comentar sobre el recurso. El valor predeterminado está marcado.

   * **[!UICONTROL Permitir clasificaciones]**

      Si se selecciona, los miembros pueden clasificar el recurso. El valor predeterminado está marcado.

   * **[!UICONTROL Permitir acceso anónimo]**

      Si se selecciona, los visitantes anónimos del sitio pueden ver el recurso en un catálogo cuando el sitio de la comunidad también permite el acceso anónimo. El valor predeterminado no está marcado.

* **[!UICONTROL Fecha de vencimiento]**
   *(Opcional)* Se puede seleccionar una fecha para completar la asignación.

* **[!UICONTROL Autor del medio]**
   *(Opcional)* El autor del recurso de habilitación. Utilice el menú desplegable para seleccionar entre los usuarios que son miembros del grupo [de](#members-group)miembros.

* **[!UICONTROL Resource Contact&amp;ast;]**
   *(Requerido)* Una persona con la que el miembro puede ponerse en contacto en relación con el recurso de habilitación. Utilice el menú desplegable para seleccionar entre los usuarios que son miembros del grupo [de](#members-group)miembros.

* **[!UICONTROL Experto de medios]**
   *(Opcional)* Una persona con la que el miembro puede ponerse en contacto y que tenga experiencia en el recurso de habilitación. Utilice el menú desplegable para seleccionar entre los usuarios que son miembros del grupo [de](#members-group)miembros.

### 4 Assignments {#assignments}

![chlimage_1-174](assets/chlimage_1-174.png)

* **[!UICONTROL Agregar asignadores]** Utilice el menú desplegable para seleccionar entre [los miembros](#members-group) (usuarios y grupos de usuarios en negrita) los que se matricularán como alumnos. Cuando los miembros inician sesión en el sitio de la comunidad, los recursos de habilitación (y las rutas de aprendizaje) en los que se inscriben aparecerán en la página [Asignaciones](functions.md#assignments-function) .

* select **[!UICONTROL Create]**

![chlimage_1-175](assets/chlimage_1-175.png)

La creación correcta del recurso de habilitación regresa a la consola Recursos con el recurso recién creado seleccionado. Desde esta consola, es posible [administrar el recurso](#managing-a-resource).

## Create a Learning Path {#create-a-learning-path}

![chlimage_1-176](assets/chlimage_1-176.png)

Para agregar una nueva ruta de aprendizaje al sitio de la comunidad

* Seleccione el icono `Create`
* En el submenú que se muestra, seleccione `Learning Path`

Esto inicia un proceso paso a paso de

* Identificación de la ruta de aprendizaje
* Proporcionar una imagen de tarjeta para representar la ruta de aprendizaje a los alumnos
* Referencia a los recursos de habilitación para incluir en la ruta de aprendizaje
* Ordenar los recursos de forma opcional
* Identificación opcional de rutas de aprendizaje previas
* Identificación de un contacto de ruta de aprendizaje
* Registro de miembros

En el caso de los recursos de habilitación incluidos en una ruta de aprendizaje, las asignaciones sólo deben realizarse para la ruta de aprendizaje y no para los recursos individuales.

### Información básica {#basic-info-1}

![chlimage_1-177](assets/chlimage_1-177.png)

* **[!UICONTROL Agregar imagen]**

   (*opcional*) Imagen que se muestra en la tarjeta para la ruta de aprendizaje en la página de asignaciones del miembro, así como en la consola Recursos. La imagen se selecciona en el sistema de archivos local del servidor. Si no se proporciona una imagen, se generará una miniatura para el recurso cargado.

   ***Nota***: el tamaño de imagen recomendado ya no es simplemente 480 x 480 píxeles. Debido al diseño interactivo de las tarjetas con diversas dimensiones del navegador, el tamaño de visualización variará de 220 x 165 píxeles a 400 x 165 píxeles.

* **[!UICONTROL Nombre del sitio]**

   (solo *lectura*) El sitio de la comunidad al que se agrega el recurso.

* **[!UICONTROL Nombre de la ruta de aprendizaje]**

   (*obligatorio*) El nombre para mostrar de la ruta de aprendizaje. Se crea un nombre de nodo válido a partir del nombre para mostrar.

* **[!UICONTROL Etiquetas]**

   (*opcional*) Se pueden elegir una o varias etiquetas que asocien la ruta de aprendizaje con uno o varios catálogos. Consulte [Etiquetado de recursos](tag-resources.md)de habilitación.

* **[!UICONTROL Mostrar en el catálogo]**

   Si no se selecciona, la ruta de aprendizaje no aparecerá en ningún catálogo. Si se selecciona, la ruta de aprendizaje aparecerá en todos los catálogos a menos que se filtre [previamente](catalog-developer-essentials.md#pre-filters) o que el miembro se filtre desde la interfaz de usuario. Mostrar la ruta de aprendizaje en un catálogo otorgará indirectamente a READ acceso a todos sus recursos contenidos. El valor predeterminado no está marcado.

* **[!UICONTROL Descripción]**

   (*opcional*) La descripción que se mostrará para el recurso de habilitación.

* **[!UICONTROL Recurso pequeño]**

   (*opcional*) Seleccionado en Recursos AEM. Imagen en miniatura para representar el recurso en el entorno de publicación, como en un catálogo.

* **[!UICONTROL Recurso grande]**

   (*opcional*) Seleccionado en Recursos AEM. Imagen grande que representa el recurso en el entorno de publicación, como en la página principal de un recurso.

* **[!UICONTROL Recurso de fragmento de contenido]**

   (*opcional*) Seleccionado en Recursos AEM. Un fragmento de contenido al que se puede hacer referencia en el entorno de publicación, pero que no está en uso de forma predeterminada.

* Seleccione **[!UICONTROL Siguiente]**

### Añadir requisitos previos {#add-prerequisites}

![chlimage_1-178](assets/chlimage_1-178.png)

* **[!UICONTROL Rutas]** de aprendizaje previas (*opcional*) Cuando se seleccionan otras rutas de aprendizaje publicadas, deben completarse antes de que un alumno pueda seleccionar esta ruta de aprendizaje.

* Seleccione **[!UICONTROL Siguiente]**

### Añadir medios {#add-resources}

![chlimage_1-179](assets/chlimage_1-179.png)

* **[!UICONTROL Aplicar el orden de la ruta de aprendizaje]**

   (*opcional*) si se establece en Activado, el orden en el que se agregan los recursos de habilitación es el orden en el que los alumnos deben continuar a través de la ruta de aprendizaje. El valor predeterminado está desactivado.

* **[!UICONTROL Medios]**

   Uno o más recursos elegidos entre los *recursos de habilitación *publicados creados para el sitio de comunidad actual.

>[!NOTE]
>
>Solo puede seleccionar los recursos disponibles en el mismo nivel que la ruta de aprendizaje. Por ejemplo, para una ruta de aprendizaje creada en un grupo, solo están disponibles los recursos de nivel de grupo; para una ruta de aprendizaje creada en un sitio de comunidad, los recursos de ese sitio están disponibles para añadirlos a la ruta de aprendizaje.

* Seleccione **[!UICONTROL Siguiente]**.

### Configuración {#settings-1}

![chlimage_1-180](assets/chlimage_1-180.png)

* **[!UICONTROL Añadir matriculaciones]**

   Utilice el menú desplegable para seleccionar entre los miembros y grupos de miembros (enumerados en negrita) que son miembros del grupo [de](#members-group)miembros del sitio de la comunidad. No es necesario agregar asignaciones al crear la ruta de aprendizaje por primera vez. Las propiedades de la ruta de aprendizaje se pueden modificar para añadir alumnos posteriormente.

* **[!UICONTROL Ruta de acceso de aprendizaje: Contact&amp;ast;]**

   *(Requerido)* Una persona con la que el miembro puede ponerse en contacto con respecto a la ruta de aprendizaje. Utilice el menú desplegable para seleccionar entre los usuarios que son miembros del grupo [de](#members-group)miembros del sitio de la comunidad.

* Seleccione **[!UICONTROL Crear]**

>[!NOTE]
>
>Los recursos de habilitación a los que se hace referencia desde la ruta de aprendizaje no deben incluir los mismos Asignados (alumnos), si los hay.
>
>Si un miembro está matriculado en un recurso de habilitación y en una ruta de aprendizaje que hace referencia a ese recurso, sus asignaciones mostrarán el recurso único y el recurso dentro de la ruta de aprendizaje.

## Administración de un recurso {#managing-a-resource}

Para administrar un único recurso de habilitación

* Desde la consola Recursos
* Seleccione el sitio de comunidad que contiene el recurso
* Seleccione el recurso

Para el recurso de habilitación seleccionado, es posible:

* Ver propiedades (predeterminado)
* Editar propiedades
* Eliminar
* Publicación
* Cancelar publicación

Para cargar una nueva versión del recurso de habilitación, se recomienda crear un nuevo recurso y, a continuación, anular la inscripción de los miembros de la versión anterior y matricularlos en la nueva versión.

### Editar recurso {#edit-resource}

![chlimage_1-181](assets/chlimage_1-181.png)

Al seleccionar el icono del lápiz, los pasos que se muestran para crear un recurso de habilitación están disponibles para que se pueda modificar cualquiera de la información proporcionada.

Si el único cambio es modificar asignaciones en el paso Configuración, al guardar los cambios se publicarán las modificaciones. Si se realizan otros cambios, el recurso debe publicarse explícitamente después de guardarlo.

### Eliminar medio {#delete-resource}

![chlimage_1-182](assets/chlimage_1-182.png)

Al seleccionar el icono de la papelera, el recurso de habilitación se `Delete`realizará después de la confirmación.

### Publicación {#publish}

![chlimage_1-183](assets/chlimage_1-183.png)

Antes de que los alumnos puedan ver un recurso de habilitación asignado, debe publicarse:

* Seleccione el icono del mundo para `Publish`
* En el cuadro de diálogo que aparece, seleccione de nuevo **[!UICONTROL Publicar]** .
* Seleccionar **[!UICONTROL cerrar]**

Aunque el cuadro de diálogo indica que la acción está en cola, a menudo se publica inmediatamente.

### Cancelar publicación {#unpublish}

![chlimage_1-184](assets/chlimage_1-184.png)

Para que los miembros del entorno de publicación no tengan acceso a los recursos de habilitación temporalmente sin eliminarlos, utilice el icono de mundo para `Unpublish`el recurso.

### Informe {#report}

![chlimage_1-185](assets/chlimage_1-185.png)

El icono Informe proporciona acceso a los informes generados cuando los alumnos interactúan con los recursos de habilitación asignados en el entorno de publicación. El informe varía según el tipo de recurso.

Para todas las rutas de aprendizaje, es posible ver un informe basado en recursos o alumnos ( `User Report`).

![chlimage_1-186](assets/chlimage_1-186.png)

Este informe es específico para el recurso de habilitación o la ruta de aprendizaje actuales. La profundidad de los informes proporcionados depende de si [Adobe Analytics](analytics.md) tiene o no licencia y está habilitado para el sitio de la comunidad. Los informes [Cronología](#timeline), Participación [del](#viewer-engagement)visor y [Participación por dispositivo](#engagement-by-device) se importan desde Adobe Analytics en función del intervalo [de](analytics.md#report-importer)sondeo.

Para todos los recursos de habilitación, independientemente de si Adobe Analytics está habilitado o no, hay informes sobre el estado [y las](#assignee-status) clasificaciones del [usuario asignado](#ratings) , así como una tabla de resumen [del](#report-summary) informe.

![chlimage_1-187](assets/chlimage_1-187.png)

#### Escala de tiempo {#timeline}

El informe Cronología de Analytics muestra cuándo se producen eventos a lo largo del tiempo para este recurso de habilitación:

* **Vistas**

   Una vista se produce cuando un alumno visita la página de detalles del recurso

* **Veces que se ha reproducido**

   Una reproducción se produce cuando alLearner interactúa con el recurso, como reproducir un vídeo o abrir un PDF

* **Clasificaciones**

   Una clasificación se produce cuando un alumno asigna una clasificación de estrella a un recurso

* **Comentarios**

   Un comentario es cuando alLearner agrega un comentario

El eje vertical es el número de eventos.

El eje horizontal es la hora del calendario.

[Se requiere](sites-console.md#analytics)Adobe Analytics.

#### Participación del visor {#viewer-engagement}

El informe Participación del visor de Analytics muestra, para los recursos de vídeo, el número de alumnos que han visto el recurso y, si no se han reproducido hasta el final, en qué momento los alumnos han dejado de reproducirlo.

El eje vertical es el número de alumnos que han visto este recurso.

El eje horizontal es la duración de este recurso.

[Se requiere el ID de organización de Marketing Cloud](sites-console.md#enablement).

#### Participación por dispositivo {#engagement-by-device}

El informe Participación de Analytics por dispositivo, para los recursos de vídeo, describe el porcentaje de vistas que se reprodujeron desde el escritorio y desde dispositivos móviles.

[Se requiere el ID de organización de Marketing Cloud](sites-console.md#enablement).

#### Estado del usuario asignado {#assignee-status}

El informe de estado del usuario asignado, basado en el número de alumnos, describe cuántos tienen

* **No iniciado**
* **En curso**
* **Completado**

#### Clasificaciones {#ratings}

El informe Clasificaciones se basa en el número de alumnos que han clasificado el recurso de habilitación, mostrando el número de cada clasificación por estrella seguida de un resumen del número total de clasificaciones y la clasificación promedio.

#### Resumen del informe {#report-summary}

Para un recurso de habilitación, el resumen del informe es una tabla que enumera

* Cada alumno que ha interactuado con el recurso
   * Su situación
   * Si se les asignó el recurso
      * En lugar de buscar el recurso en un catálogo
   * Número de comentarios publicados
   * La calificación otorgada, en su caso

Para un informe de recursos de ruta de aprendizaje, el resumen del informe es una lista de tabla

* Cada recurso incluido en la ruta de aprendizaje
   * Estado de publicación
   * Número de vistas
   * Número de reproducciones
   * Puntuación promedio
   * Formato
   * Tamaño
   * Nombre del sitio de la comunidad

Para un informe de usuario de ruta de aprendizaje, el resumen del informe es una lista de tabla

* Cada alumno asignado a la ruta de aprendizaje
   * Número de recursos completados
   * Su situación

Es posible ajustar la visualización de la tabla seleccionando columnas mediante el `Show / hide columns` selector.

#### Download Report as CSV {#download-report-as-csv}

La tabla Resumen de informes se puede descargar en formato CSV con un botón en la parte superior de la consola.

* para un recurso de habilitación: `Download Resource Report as CSV` botón
* para una ruta de aprendizaje: `Download Learning Path Report as CSV` botón

El resumen completo de los informes se descarga independientemente de las columnas que se hayan elegido para la visualización.
