---
title: Experimente el sitio publicado
seo-title: Experimente el sitio publicado
description: Navegue hasta un sitio publicado para habilitarlo
seo-description: Navegue hasta un sitio publicado para habilitarlo
uuid: 1bfefa8a-fd9c-4ca8-b2ff-add79776c8ae
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 26715b94-e2ea-4da7-a0e2-3e5a367ac1cd
translation-type: tm+mt
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---



# Experimente el sitio publicado {#experience-the-published-site}


**[⇐ Crear y asignar recursos de habilitación](resource.md)**

## Ir a un nuevo sitio al publicar {#browse-to-new-site-on-publish}

Ahora que el sitio de la comunidad recién creado y sus recursos de habilitación y ruta de aprendizaje han sido publicados, es posible experimentar el sitio de Tutorial de Habilitación.

Comience navegando hasta la dirección URL que se muestra al crear el sitio, pero en el servidor de publicación, p. ej.

* URL del autor = [http://localhost:4502/content/sites/enable/en.html](http://localhost:4502/content/sites/enable/en.html)
* URL de publicación = [http://localhost:4503/content/sites/enable/en.html](http://localhost:4503/content/sites/enable/en.html)

Si la página principal [predeterminada estaba configurada](enablement-create-site.md#changethedefaulthomepage), entonces simplemente navegando a [http://localhost:4503/](http://localhost:4503/) debería iniciar el sitio.

Al llegar por primera vez al sitio publicado, el visitante del sitio no suele haber iniciado sesión y sería anónimo.

**http://localhost:4503/content/sites/enable/en.html**

![chlimage_1-433](assets/chlimage_1-433.png)

## Visitante anónimo del sitio {#anonymous-site-visitor}

Un visitante anónimo del sitio se presenta inmediatamente con la página de inicio de sesión de este sitio de comunidad de habilitación privada. Tenga en cuenta que no hay opción de registrarse por sí mismo ni de iniciar sesión en Facebook o Twitter.

Observe que esta página principal muestra cuatro elementos de menú: `Assignments, Ski Catalog, What's New` y `Discussions`, pero no se puede acceder a ninguno sin iniciar sesión.

>[!NOTE]
>
>Es posible otorgar acceso anónimo a un sitio de habilitación sin permitir que los visitantes se automatriculen.
>Si un recurso de habilitación está establecido en `show in catalog` y `allow anonymous access`, los visitantes anónimos del sitio podrán ver los recursos del catálogo.

### Impedir el acceso anónimo a JCR {#prevent-anonymous-access-on-jcr}

Una limitación conocida expone el contenido del sitio de la comunidad a visitantes anónimos a través del contenido jcr y json, aunque **[!UICONTROL permitir el acceso]** anónimo está deshabilitado para el contenido del sitio. Sin embargo, este comportamiento se puede controlar mediante restricciones de Sling como solución alternativa.

Para proteger el contenido del sitio de la comunidad del acceso de usuarios anónimos a través del contenido jcr y json, siga estos pasos:

1. En la instancia de AEM Author, vaya a https://&lt;host>:&lt;puerto>/editor.html/content/site/&lt;nombre del sitio>.html.

   >[!NOTE]
   >
   >No vaya al sitio localizado.

1. Vaya a Propiedades **[!UICONTROL de la página]**.

   ![page-properties-1](assets/page-properties-1.png)

1. Vaya a la ficha **[!UICONTROL Avanzado]** .
1. Enable **[!UICONTROL Authentication Requirement]**.

   ![site-authentication-1](assets/site-authentication-1.png)

1. Agregue la ruta de la página de inicio de sesión. Por ejemplo, `/content/......./GetStarted`.
1. Publique la página.

## Miembro matriculado {#enrolled-member}

Esta experiencia depende de los usuarios `Riley Taylor` y `Sidney Croft` se [crea](enablement-setup.md#publishcreateenablementmembers) y [asigna](resource.md#settings) a la ruta de aprendizaje de *Clases* de Esquí a través de su pertenencia al grupo Clase ** Comunitaria de Esquí.

Iniciar sesión con

* `Username: riley`
* `Password: password`

Si el perfil de usuario no se creó mediante el registro propio, la primera vez que un miembro inicia sesión, se muestra su página de perfil para que pueda verificarla y modificarla según sea necesario.

La próxima vez que el miembro inicie sesión, se mostrará la página principal, identificada por el primer elemento de menú.

![chlimage_1-434](assets/chlimage_1-434.png)

### Asignaciones {#assignments}

La página Asignaciones es donde se muestra al miembro todas las rutas de aprendizaje y todos los recursos de habilitación asignados específicamente a ellos.

Cada asignación proporciona información básica sobre

* El tipo de asignación
* Si es una nueva asignación
* El nombre
* Detalles pertinentes para el tipo de cesión
* Contacto de asignación, experto y autor (si se proporciona)

El tipo de asignación se indica con un icono en la esquina superior izquierda de la tarjeta. La imagen de una carretera es para un camino de aprendizaje con el número de recursos de habilitación incluidos.

![chlimage_1-435](assets/chlimage_1-435.png)

Al seleccionar *Clases* de esquí se mostrarán los dos recursos de habilitación a los que hace referencia la ruta de aprendizaje.

![chlimage_1-436](assets/chlimage_1-436.png)

Si selecciona *Clases de esquí 1* , se abrirá la página de detalles del recurso de habilitación.

Desde la página de detalles, el miembro puede aprender, [clasificar](rating.md) la lección y agregar [comentarios](comments.md). Cualquier actividad de miembro se verá reflejada en la sección Novedades del sitio.

Las interacciones con el recurso de habilitación se anotarán en la sección Informe accesible en el entorno de creación.

![chlimage_1-437](assets/chlimage_1-437.png)

### Catálogo de esquí {#ski-catalog}

La página Catálogo de esquí es el catálogo de recursos de habilitación etiquetados con etiquetas del `Tutorial` espacio de nombres. Los dos recursos de *lección* de esquí están etiquetados con la `Skiing` etiqueta , de modo que si se selecciona cualquier etiqueta que no sea `All` o `Tutorial: Sports / Skiing` , no se muestra nada.

Cuando a un miembro no se le han asignado recursos de habilitación, ya sea directamente o a través de una ruta de aprendizaje, es posible interactuar con los recursos de habilitación ubicados dentro de un catálogo y proporcionar comentarios a través de comentarios y clasificaciones.

![chlimage_1-438](assets/chlimage_1-438.png)

### Discusiones {#discussions}

Además de valorar y comentar los recursos de habilitación ([cuando se habilita](enablement-create-site.md#step33asettings)), la plantilla de sitio de comunidad desde la que `Enablement Tutorial` se creó incluye la función [de](functions.md#forum-function) foro (el título es `Discussions)`.

Seleccione el `Discussions`vínculo y anuncie un tema.

Cierre la sesión e inicie sesión como Sidney Croft (cliente/contraseña) y responda a la pregunta, así como siga el tema.

Observe que, además de moderación en línea, hay opciones para compartir el tema en medios sociales o para enviarlo por correo electrónico.

![chlimage_1-439](assets/chlimage_1-439.png)

### Novedades {#what-s-new}

El elemento `What's New` de menú es el título dado a la función [de flujo de](functions.md#activity-stream-function) actividad en la estructura de este sitio de comunidad.

Todavía ha iniciado sesión como Sidney, seleccione el `What's New` enlace para mostrar la actividad.

![chlimage_1-440](assets/chlimage_1-440.png)

## Miembro de la comunidad de confianza {#trusted-community-member}

Esta experiencia supone que ` [Quinn Harper](enablement-setup.md#publishcreateenablementmembers)` se le asignaron las funciones de [moderador](enablement-create-site.md#moderation) y contacto con [recursos](resource.md#settings).

Iniciar sesión con

* `Username: quinn`
* `Password: password`

Una vez que haya iniciado sesión, observe que hay un nuevo elemento de menú, que `Administration`aparece porque se le ha dado al miembro la función de moderador.

![chlimage_1-441](assets/chlimage_1-441.png)

La página principal se identifica mediante el primer elemento de menú, Asignaciones. Quinn es el contacto de recursos de moderador y habilitación y no se ha matriculado en ningún recurso de habilitación o ruta de aprendizaje, por lo que no hay nada que mostrar.

### Administración {#administration}

Lo que hay es la actividad de los dos alumnos `Riley Taylor` y `Sidney Croft`. Al seleccionar el `Administration` vínculo para acceder a la consola de moderación, Quinn puede utilizar la consola [de moderación](moderation.md) masiva para moderar sus publicaciones.

Al seleccionar el icono del panel lateral, se abren los filtros utilizados para buscar contenido de comunidad.

Al pasar el ratón por encima de una tarjeta de comentarios se muestran las acciones de moderación.

![chlimage_1-442](assets/chlimage_1-442.png)

## Informes sobre el autor {#reports-on-author}

Existen dos formas de acceder a los informes de los alumnos y a los recursos de habilitación.

En el autor, vaya a la consola **[Comunidades,](resources.md)**Recursos, donde se administran los recursos de habilitación y, después de seleccionar un sitio de comunidad, podrá generar informes para

* Todos los recursos de habilitación y rutas de aprendizaje
* Un recurso de habilitación específico o una ruta de aprendizaje

Vaya a la consola **[Comunidades,](reports.md)**Informes y genere informes según

* Asignaciones a recursos de habilitación y rutas de aprendizaje
* Anuncios en un sitio de comunidad durante un período específico
* Vistas (visitas al sitio) de un sitio de la comunidad durante un período específico

* Los anuncios y las vistas pueden estar en todo el contenido o en contenido específico:

   * Foro
   * Tema de foro
   * P y R
   * Pregunta de P y R
   * Blog
   * Artículo de blog
   * Calendario
   * Evento de calendario

### Consola de recursos {#resources-console}

Con un poco de actividad e interacción con los recursos al publicar, vale la pena ver los informes sobre el autor.

* En autor
* Iniciar sesión con privilegios administrativos
* Vaya del menú principal a **[!UICONTROL Comunidades > Recursos]**
* Seleccionar el `Enablement Tutorial` sitio
* Seleccione el icono `Report` para ver un resumen de todos los recursos
* Seleccione un recurso y, a continuación, el icono `Report` de un informe sobre ese recurso

Tenga en cuenta que es muy probable que se muestren datos de Adobe Analytics, que pueden tardar de 1 a 12 horas en aparecer. Sin embargo, los informes SCORM básicos ya están disponibles.

#### Informe de recursos de lecciones de esquí {#ski-lessons-resource-report}

![chlimage_1-443](assets/chlimage_1-443.png)

#### Informe de usuario de lecciones de esquí {#ski-lessons-user-report}

* Seleccionar **[!UICONTROL comunidades > Recursos]**

* Abrir tarjeta `Enablement Tutorial`
* Abrir tarjeta `Ski Lessons`
* Seleccione `Report > User Report`

![chlimage_1-444](assets/chlimage_1-444.png)

### Consola de informes {#reports-console}

La consola Informes permite generar informes en

* **Asignaciones** para cualquier sitio de la comunidad de habilitación
* **Vistas** de cualquier sitio de comunidad
* **Anuncios** para cualquier sitio de comunidad

Para informes sobre asignaciones:

* En autor
* Iniciar sesión con privilegios administrativos
* Vaya a **[!UICONTROL Comunidades > Informes > Informe Asignaciones]**
* Seleccione un **[!UICONTROL sitio]** en el menú desplegable (seleccione `Enablement Tutorial`)

* Seleccionar **[!UICONTROL grupo]** (seleccionar `Community Ski Class`)

* Seleccionar una **[!UICONTROL asignación]** (seleccionar `Ski Lessons`)

* Seleccionar **[!UICONTROL generación]**

![chlimage_1-445](assets/chlimage_1-445.png)

Para informes sobre vistas:

* En autor
* Iniciar sesión con privilegios administrativos
* Vaya a **[!UICONTROL Comunidades > Informes > Informe Vistas]**
* Seleccione un **sitio **en el menú desplegable (seleccione`Enablement Tutorial`)

* Seleccionar tipo **[!UICONTROL de contenido]** (seleccione `all`)

* Seleccionar un intervalo **[!UICONTROL de fechas]** (seleccionar `Last 7 days`)

* Seleccionar **[!UICONTROL generación]**

![chlimage_1-446](assets/chlimage_1-446.png)

**[⇐ Crear y asignar recursos de habilitación](resource.md)**
