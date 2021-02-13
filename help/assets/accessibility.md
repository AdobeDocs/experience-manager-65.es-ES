---
title: Accesibilidad en [!DNL Experience Manager Assets]
description: Obtenga información sobre cómo las funciones de accesibilidad de [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] ayudan a los usuarios con discapacidades.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 863d1bd3f0f188153fcbbb7256d3ac2e3b247f59
workflow-type: tm+mt
source-wordcount: '1919'
ht-degree: 2%

---


<!--
Possible topics to cover in this article are below.

* Compile a list of enhancements done in the last ~1 year.
* Showcase a few prominent use cases (search?) in a screencast.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, etc.
* List all UIs that are keyboard navigable.
* Unified list of the product tasks supported, such as, search assets, download assets, add or editing metadata, use DM Viewers, etc.
* Do we need to add support matrix of user tasks with browser and screen reader combinations. Everything may not work in all browsers and/or using all screen readers.
* Any exceptions that users should be aware of. It may help to call out (it may be done in ACR) what tasks are NOT supported.
* CTAs – what's next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Link to a11y-specific online methods to report issues, seek support, or request enhancements, if any. Asked the a11y team on Slack.
-->

# Funciones de accesibilidad en [!DNL Adobe Experience Manager Assets] {#accessibility-in-aem-assets}

[!DNL Adobe Experience Manager] permite a los creadores y editores de contenido ofrecer experiencias increíbles en la web. El Adobe se esfuerza por incluir a los creadores con discapacidades mejorando la accesibilidad de [!DNL Experience Manager]. El software se mejora continuamente para satisfacer las necesidades de todos los tipos de usuarios y cumplir con los estándares mundiales que incluyen personas con discapacidades visuales, auditivas, de movilidad u otras discapacidades.

[!DNL Experience Manager] publica información de conformidad que describe los estándares a los que se adhiere, describe las características de accesibilidad del producto y describe el nivel de cumplimiento. Los informes de conformidad de accesibilidad ayudan a [!DNL Experience Manager] los usuarios a comprender el nivel de cumplimiento de los distintos estándares. Las mejoras realizadas en [!DNL Assets] permiten a todos los usuarios utilizar fácilmente las interfaces mediante el teclado, el lector de pantalla, los ampliadores y otras tecnologías de asistencia.

[!DNL Experience Manager] proporciona distintos niveles de soporte para los siguientes estándares:

* [Directrices de accesibilidad del contenido web (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [Se revisó el artículo 508 de la Ley](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines) de rehabilitación.
* [Iniciativa de Accesibilidad - Aplicaciones de Internet enriquecidas y accesibles (WAI-ARIA) por W3C](https://www.w3.org/WAI/standards-guidelines/aria/).
* [ES 301 549](https://en.wikipedia.org/wiki/EN_301_549).

Para leer un informe con detalles del nivel de cumplimiento, consulte la página [Informe de conformidad de accesibilidad](https://www.adobe.com/accessibility/compliance.html) (ACR).

Para saber cómo [!DNL Dynamic Media] es accesible, consulte [accesibilidad en [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

## Tecnologías de asistencia {#at-support}

Los usuarios con discapacidades suelen depender del hardware y el software para acceder al contenido web y utilizar productos de software. Estas herramientas se conocen como tecnologías de asistencia. [!DNL Experience Manager Assets] Puede trabajar con los siguientes tipos de tecnologías de asistencia (AT) al utilizar las funciones principales del software:

* Lectores de pantalla y ampliador de pantalla.
* Software de reconocimiento de voz.
* Uso del teclado: navegación y accesos directos.
* Hardware de asistencia, incluidos los controles del conmutador, pantallas Braille actualizables y otros dispositivos de entrada de equipos.
* Herramientas de ampliación de la interfaz de usuario.

## [!DNL Experience Manager Assets] casos de uso accesibles  {#accessible-assets-use-cases}

En [!DNL Experience Manager], las características de accesibilidad abordan dos requisitos clave de [!DNL Experience Manager] usuarios y sus clientes.

* Para los diseñadores y creadores de contenido, existen funciones para crear y publicar contenido accesible que sus clientes y visitantes de sitios web utilizan a su vez. Las personas con discapacidad utilizan el contenido con la ayuda de tecnologías de asistencia. Para obtener más información, consulte [guías de accesibilidad web](/help/managing/web-accessibility.md).
* [!DNL Experience Manager] también permite a los usuarios y administradores con discapacidades acceder a la interfaz de usuario y a los controles para crear y administrar contenido. Las personas con discapacidades pueden utilizar tecnologías de asistencia para navegar, utilizar y administrar la capacidad [!DNL Assets].

Las funciones principales de [!DNL Assets] son más accesibles que antes y se actualizan regularmente para mejorar el cumplimiento de los estándares globales. Las operaciones de CRUD en [!DNL Assets] tienen cierto grado de accesibilidad incorporada en ellas. Se puede acceder a flujos de trabajo DAM como agregar, administrar, buscar y distribuir recursos con la ayuda de métodos abreviados de teclado, texto del lector de pantalla, contraste de color, etc.

## Compatibilidad con el uso del teclado {#keyboard-use}

Muchos elementos de la interfaz de usuario en los que se puede hacer clic o en los que se puede realizar una acción con un puntero también se pueden utilizar con el teclado. Con un teclado, los usuarios pueden centrarse en los elementos de la interfaz de usuario y realizar una acción adecuada. Los usuarios pueden utilizar directamente los métodos abreviados de teclado para déclencheur de un comando o una acción sin tener que centrarse en los elementos de la interfaz de usuario y realizar el déclencheur mediante el teclado. Por ejemplo, los usuarios pueden abrir la línea de tiempo de un recurso en la parte izquierda de la interfaz de usuario navegando hasta el control de la interfaz de usuario mediante un teclado, seleccionando `Return` y seleccionando `Alt + 2` método abreviado de teclado.

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### Métodos abreviados de teclado en [!DNL Assets] {#keyboard-shortcuts}

Las siguientes acciones de [!DNL Assets] funcionan con los métodos abreviados de teclado enumerados. La mayoría de los métodos abreviados de teclado que se aplican a [!DNL Experience Manager] consolas también se aplican a [!DNL Assets]. Consulte [combinaciones de teclas para consolas](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts). Consulte cómo [habilitar o deshabilitar los métodos abreviados de teclado](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts).

| Interfaz de usuario o escenario | Método abreviado de teclado | Acción |
|---|---|---|
| Vista de columna en la interfaz de usuario [!DNL Assets] | Teclas de flecha arriba y abajo | Navegue a archivos y carpetas dentro de la misma jerarquía. |
| Vista de columna en la interfaz de usuario [!DNL Assets] | Teclas de flecha izquierda y derecha | Vaya a los archivos y carpetas situados encima o debajo de la carpeta actual. |
| Exploración de carpetas en [!DNL Assets] | `/` | Invocar la búsqueda abriendo el cuadro Omnisearch. |
| [!DNL Assets] Consola | ` | Conmutar raíles laterales |
| [!DNL Assets] Consola | `Alt + 1` | Abra el árbol de contenido. |
| [!DNL Assets] Consola | `Alt + 2` | Abra el carril izquierdo [!UICONTROL Navegación]. |
| [!DNL Assets] Consola | `Alt + 3` | Mostrar [!UICONTROL cronología] de un recurso seleccionado. |
| [!DNL Assets] Consola | `Alt + 4` | Abra las referencias de Live Copy del recurso seleccionado. |
| [!DNL Assets] Consola | `Alt + 5` | Busque y busque en inicio dentro de la carpeta seleccionada. |
| El recurso o la carpeta están seleccionados | Retroceso | Elimine el recurso o la carpeta seleccionados. |
| El recurso o la carpeta están seleccionados | `p` | Abra la página Propiedades del recurso seleccionado. |
| El recurso o la carpeta están seleccionados | `e` | Edite el recurso seleccionado. |
| El recurso o la carpeta están seleccionados | `m` | Mueva el recurso seleccionado. |
| El recurso o la carpeta están seleccionados | `Ctrl + c` | Copie el recurso seleccionado. |
| El recurso o la carpeta están seleccionados | `Esc` | Anule la selección. |
| Se abre el cuadro de diálogo y está en el foco | `Esc` | Cerrar. |
| Dentro de una carpeta en DAM | `Ctrl + v` | Pegue el recurso copiado. |
| [!DNL Assets] Consola | `Ctrl + A` | Seleccione todos los recursos. |
| Páginas de propiedades de recursos | `Ctrl + S` | Guarde los cambios. |
| [!DNL Assets] Consola | `?` | Consulte una lista de métodos abreviados de teclado. |

## Inicie sesión y navegue por la [!DNL Assets] interfaz de usuario {#login}

Los usuarios pueden utilizar el teclado para desplazarse hasta el campo de inicio de sesión y rellenarlo para iniciar sesión. Los mensajes de error debido a combinaciones incorrectas de nombre de usuario y contraseña en la página de inicio de sesión son anunciados por los lectores de pantalla cada vez que se produce el error.

Después de iniciar sesión, los usuarios de DAM pueden navegar dentro de la interfaz de usuario [!DNL Assets] mediante el teclado. Los elementos de la interfaz de usuario, como el carril izquierdo, los menús, el perfil del usuario, la barra de búsqueda, los archivos y las carpetas, y la configuración y la administración se pueden navegar mediante el teclado. El orden de navegación del teclado es de izquierda a derecha y de arriba abajo. Cuando se navega con un teclado, una opción procesable cuando se selecciona se resalta con un mejor contraste de color y es narrada por un lector de pantalla. Cuando corresponde, un lector de pantalla anuncia el estado (por ejemplo, expandido, contraído y estado mixto) de las opciones centradas en el menú. Además, el lector de pantalla anuncia el propósito de la opción procesable, en lugar de indicar el aspecto o la ubicación de la interfaz.

Si un usuario expande la opción de ayuda o perfil del usuario desde el menú, el lector de pantalla anuncia la opción o el estado correspondientes. Si un usuario expande la opción de perfil de usuario, las opciones disponibles se pueden seleccionar con un teclado. Por ejemplo, un administrador puede hacerse pasar por otro usuario. Si un usuario busca una cadena en la opción [!UICONTROL Ayuda], un narrador anuncia &quot;Búsqueda de ayuda&quot; para indicar que se está realizando una búsqueda.

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## Examinar recursos y vista la información relacionada {#browse}

En la interfaz de usuario [!DNL Assets], los usuarios pueden utilizar el teclado para explorar la lista de recursos digitales existentes en el repositorio de DAM, realizar la previsualización o descarga de un recurso, ver las representaciones generadas, cambiar de vista, ver las representaciones generadas, ver la cronología y el historial de versiones, ver comentarios y referencias, y vista y administración de metadatos.

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

Al explorar el repositorio de recursos, la siguiente funcionalidad mejora la accesibilidad:

* El lector de pantalla anuncia alternativas de texto que ilustran el propósito o la funcionalidad de los iconos en lugar de sus nombres.
* Los usuarios pueden acceder a las opciones interactivas de la interfaz de usuario y centrarlas en la lista Referencias de los recursos con las teclas del teclado.
* Los elementos de cada fila de la vista de lista son anunciados como los elementos de la misma fila por los lectores de pantalla.
* Al navegar con la tecla `Tab`, el enfoque puede moverse a la opción de cierre en la previsualización de la versión.
* Cuando se utiliza el teclado para examinar, las opciones de interfaz de usuario activables resaltadas tienen un enfoque visual más prominente con un contraste mejorado. Hace que el área enfocada sea más identificable para el usuario.
* El uso de la tecla `Esc` para eliminar los iconos de acción rápida de la vista en miniatura no elimina el enfoque del teclado del último elemento seleccionado.
* Con un recurso seleccionado, al seleccionar `Alt + 4` método abreviado de teclado se abre la lista [!UICONTROL References] en el carril izquierdo. Con la tecla `Tab`, los usuarios pueden navegar por las entradas de referencia que no sean cero. Al navegar únicamente por las entradas de referencia que no son cero, también se ahorra esfuerzo y pulsaciones de teclas.
* Los comentarios de un recurso están disponibles en la línea de tiempo del recurso. Se puede acceder a ella si se accede al carril izquierdo mediante un teclado o un método abreviado de teclado.
* [!UICONTROL Se ] puede acceder a la configuración de vistas  [!DNL Experience Manager] mediante un teclado. Los usuarios pueden navegar por los tamaños de tarjeta disponibles mediante las teclas de flecha y seleccionar y desplazarse por las fichas para navegar y establecer otros elementos en la vista de configuración de Vista existente.

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## Administre recursos digitales {#manage-assets}

Muchas tareas de administración de recursos, como las operaciones de CRUD, la descarga de recursos y la adición de metadatos, son accesibles en varios grados. [!DNL Assets] permite realizar las tareas mediante diversas tecnologías de asistencia, como un lector de pantalla y un teclado.

Vea una demostración en vídeo de cómo utilizar un teclado para [explorar el repositorio y descargar un recurso](https://youtu.be/K3dgqMRQJys).

Para las operaciones de metadatos que normalmente realizan funciones como los especialistas en marketing y los administradores, las siguientes funciones mejoran la accesibilidad:

* [!UICONTROL Ahora se puede acceder a la opción Guardar y ] cerrar en la página   Propiedades del recurso mediante el teclado.
* Los lectores de pantalla anuncian las opciones para eliminar las etiquetas seleccionadas en la ficha [!UICONTROL Basic] del recurso [!UICONTROL Properties].
* Los usuarios pueden utilizar el cuadro de diálogo emergente Selector de datos con un teclado. El elemento de interfaz de usuario del Selector de datos se utiliza para establecer tiempos de activación y de desactivación y seleccionar fecha.
* La funcionalidad de arrastrar mediante el teclado funciona correctamente en [!UICONTROL Editor de Esquemas de metadatos] en el modo de exploración del lector de pantalla.
* Un usuario puede mover el enfoque mediante el teclado al campo Añadir usuario o grupo en [!UICONTROL Grupo de usuarios cerrado] en la ficha [!UICONTROL Permisos] de la carpeta [!UICONTROL Propiedades].

## Buscar recursos digitales {#search-assets}

Una experiencia de búsqueda de recursos rápida y fluida aumenta la velocidad de contenido. Los casos de uso de velocidad de contenido forman parte de la funcionalidad principal [!DNL Assets]. Para inicio de una búsqueda desde la barra de Omniture, los usuarios pueden utilizar el método abreviado de teclado `/` o `Tab` junto con los lectores de pantalla para localizar rápidamente la opción de búsqueda. El lector de pantalla narra el nombre de la opción como &quot;Botón de búsqueda&quot; cuando el enfoque está en la opción de búsqueda ![opción de búsqueda](assets/do-not-localize/search_icon.png). Los usuarios pueden seleccionar `Return` para abrir el cuadro Omnisearch. El lector de pantalla no sólo narra la palabra clave escrita en el cuadro de búsqueda, sino que también narra las sugerencias ofrecidas por [!DNL Experience Manager Assets]. Los usuarios pueden utilizar una combinación de teclas de flecha, `Return` y `Tab` para acceder a las distintas opciones de déclencheur de una búsqueda.

La funcionalidad de búsqueda se hace accesible mediante la siguiente funcionalidad:

* El título de la página, según esté disponible para un lector de pantalla, ayuda a identificar la página como página de búsqueda de recursos.
* Los usuarios buscan recursos desde el campo Omniture Search. Los usuarios pueden abrirlo mediante la navegación mediante el teclado o mediante el método abreviado de teclado `/`.
* Los usuarios pueden escribir en inicio la palabra clave de búsqueda y luego seleccionar las sugerencias automáticas utilizando las teclas de flecha. La sugerencia resaltada se puede seleccionar con la clave `Return` y se buscarán los recursos para la sugerencia seleccionada.
* Los lectores de pantalla pueden identificar y anunciar las casillas de verificación de estados mixtos (en las que, a menos que seleccione todos los predicados anidados, las casillas de verificación de primer nivel no se seleccionan y pasan por alto) en el panel Filtros al filtrar los resultados de búsqueda.
* El enfoque del usuario pasa a las opciones de búsqueda después de que se cierre el cuadro de búsqueda de Omniture.

Al filtrar los resultados de búsqueda:

* La página de resultados de la búsqueda tiene un título informativo para comprender mejor a los usuarios del lector de pantalla.
* Un lector de pantalla anuncia las opciones del filtro de búsqueda como acordeones ampliables.
* Los lectores de pantalla anuncian los predicados con opciones de estados mixtos.

## Compartir recursos {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

Al compartir recursos, las siguientes funciones mejoran la accesibilidad:

* Un usuario puede mover el enfoque mediante el teclado en el campo Buscar y Añadir dirección de correo electrónico del cuadro de diálogo de uso compartido de vínculos.

* En el cuadro de diálogo de uso compartido de vínculos, al navegar en el modo Examinar, los lectores de pantalla,

   * No narre la información de la tabla cuando se cargue el cuadro de diálogo.
   * Puede navegar a todas las sugerencias de la lista.
   * Narre las sugerencias que se muestran para Añadir la dirección de correo electrónico y los campos de búsqueda.

## Documentación accesible {#accessible-docs}

[!DNL Experience Manager] proporciona documentación accesible para personas con discapacidades. Lo siguiente ayuda a hacer accesible la oferta de contenido por ahora, mientras que Adobe sigue mejorando la plantilla y el contenido:

* Los lectores de pantalla pueden leer el texto.
* Las imágenes y las ilustraciones tienen texto alternativo disponible.
* Se puede navegar con el teclado.
* Las tasas de contraste ayudan a resaltar algunas partes del sitio web de documentación.

## Proporcionar comentarios {#a11y-feedback}

Para proporcionar comentarios, formular preguntas y solicitar mejoras del producto relacionadas con la accesibilidad, utilice los siguientes métodos:

* Rellene el formulario en [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html).
* Envíenos un correo electrónico a access@adobe.com.

>[!MORELIKETHIS]
>
>* [Funciones de accesibilidad en [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).
>* [Notas de la versión de las mejoras realizadas en cada versión](/help/release-notes/new-features-latest-service-pack.md) de Service Pack.
>* [[!DNL Adobe Experience Manager] guía](/help/managing/web-accessibility.md) de accesibilidad.
>* [Informes de conformidad (ACR) y listado de VPAT para soluciones](https://www.adobe.com/accessibility/compliance.html) de Adobe.

