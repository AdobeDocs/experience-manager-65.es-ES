---
title: Funciones e interfaces accesibles de [!DNL Experience Manager Assets]
description: Descubra cómo funciona la accesibilidad en [!DNL Adobe Experience Manager] 6,5 [!DNL Assets] ayudar a los usuarios con discapacidades.
contentOwner: AG
feature: Asset Management
role: User, Architect, Leader
exl-id: 15555941-99a2-4586-8d7b-b22f3ec17805
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 0%

---

<!--
Possible topics to cover in this article are below.

* Compile a list of enhancements done in the last ~1 year.
* Showcase a few prominent use cases (search?) in a screencast.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, and so on.
* List all UIs that are keyboard navigable.
* Unified list of the product tasks supported, such as, search assets, download assets, add or editing metadata, use DM Viewers, and so on.
* Do we need to add support matrix of user tasks with browser and screen reader combinations. Everything may not work in all browsers and/or using all screen readers.
* Any exceptions that users should be aware of. It may help to call out (it may be done in ACR) what tasks are NOT supported.
* CTAs – what's next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Link to a11y-specific online methods to report issues, seek support, or request enhancements, if any. Asked the a11y team on Slack.
-->

# Funciones de accesibilidad en [!DNL Adobe Experience Manager Assets] {#accessibility-in-aem-assets}

[!DNL Adobe Experience Manager] permite a los creadores y editores de contenido ofrecer experiencias increíbles en la web. Adobe se esfuerza por incluir a los creadores con discapacidad mejorando la accesibilidad de [!DNL Experience Manager]. El software se mejora continuamente para satisfacer las necesidades de todos los tipos de usuarios y se adhiere a los estándares mundiales que incluyen personas con deficiencias visuales, auditivas, de movilidad u otras.

[!DNL Experience Manager] publica información de conformidad que describe los estándares a los que se adhiere, describe las funciones de accesibilidad del producto y describe el nivel de conformidad. Ayuda de los informes de conformidad de accesibilidad [!DNL Experience Manager] Los usuarios de comprenden el nivel de cumplimiento de los distintos estándares. Mejoras realizadas en [!DNL Assets] permite que todos los usuarios utilicen las interfaces fácilmente mediante el teclado, el lector de pantalla, las lupas y otras tecnologías de asistencia.

[!DNL Experience Manager] ofrece distintos niveles de compatibilidad con los siguientes estándares:

* [Directrices de accesibilidad del contenido web (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [Revisión del artículo 508 de la Ley de rehabilitación](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines).
* [Iniciativa de accesibilidad - Aplicaciones de Internet enriquecidas accesibles (WAI-ARIA) de W3C](https://www.w3.org/WAI/standards-guidelines/aria/).
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549).

Para leer un informe con detalles del nivel de cumplimiento, consulte [Informe de conformidad de accesibilidad](https://www.adobe.com/accessibility/compliance.html) ACR (Página de la).

Para saber cómo [!DNL Dynamic Media] es accesible, consulte [accesibilidad en [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

## Tecnologías de asistencia {#at-support}

Los usuarios con discapacidades suelen depender del hardware y el software para acceder al contenido web y utilizar productos de software. Estas herramientas se conocen como tecnologías de asistencia. [!DNL Experience Manager Assets] puede trabajar con los siguientes tipos de tecnologías de asistencia (AT) al utilizar las funcionalidades principales del software:

* Lectores de pantalla y ampliador de pantalla.
* Software de reconocimiento de voz.
* Uso del teclado: navegación y métodos abreviados.
* Hardware de asistencia, incluidos controles de conmutador, pantallas de Braille actualizables y otros dispositivos de entrada de equipo.
* Herramientas de ampliación de IU.

## [!DNL Experience Manager Assets] Casos de uso de accesibles {#accessible-assets-use-cases}

Entrada [!DNL Experience Manager], las funciones de accesibilidad abordan dos requisitos clave de [!DNL Experience Manager] usuarios y sus clientes.

* Para los diseñadores y creadores de contenido, hay funciones para crear y publicar contenido accesible que utilizan a su vez sus clientes y visitantes del sitio web. Las personas con discapacidad utilizan el contenido con la ayuda de tecnologías de asistencia. Para obtener más información, consulte [directrices de accesibilidad web](/help/managing/web-accessibility.md).
* [!DNL Experience Manager] también permite a los usuarios y administradores con discapacidades acceder a la interfaz de usuario y a los controles para crear y administrar contenido. Las personas con discapacidades pueden utilizar tecnologías de asistencia para navegar, utilizar y administrar el [!DNL Assets] capacidad.

Las funciones principales de [!DNL Assets] son más accesibles que antes y se actualizan regularmente para mejorar el cumplimiento de las normas globales. Las operaciones de CRUD en [!DNL Assets] tienen algún grado de accesibilidad integrado en ellas. Los flujos de trabajo de DAM, como la adición, administración, búsqueda y distribución de recursos, son accesibles con la ayuda de métodos abreviados de teclado, texto del lector de pantalla, contraste de color, etc.

## Compatibilidad con el uso del teclado {#keyboard-use}

Muchos elementos de la interfaz de usuario en los que se puede hacer clic o que se pueden llevar a cabo acciones con un puntero también se pueden utilizar con el teclado. Con un teclado, los usuarios pueden centrarse en los elementos de la interfaz de usuario y realizar las acciones adecuadas. Los usuarios pueden utilizar directamente los métodos abreviados de teclado para almacenar en déclencheur un comando o una acción sin tener que centrarse en los elementos de la interfaz de usuario y almacenarlos en déclencheur mediante el teclado. Por ejemplo, los usuarios pueden abrir la cronología de un recurso en el lado izquierdo de la interfaz de usuario navegando hasta el control de interfaz de usuario con un teclado y seleccionando `Return`y seleccionando `Alt + 2` método abreviado de teclado.

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into 'basic handling' info aka article to 'understand and use the workspace'.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into 'basic handling' info aka article to 'understand and use the workspace'. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into 'basic handling' info aka article to 'understand and use the workspace'.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### Métodos abreviados de teclado en [!DNL Assets] {#keyboard-shortcuts}

Las siguientes acciones en [!DNL Assets] trabaje con los métodos abreviados de teclado enumerados. La mayoría de los métodos abreviados de teclado aplicables a [!DNL Experience Manager] Las consolas también se aplican a [!DNL Assets]. Consulte [métodos abreviados del teclado para consolas](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts). Consulte cómo [habilitar o deshabilitar los métodos abreviados de teclado](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts).

| Interfaz de usuario o escenario | Métodos abreviados del teclado | Acción |
|---|---|---|
| Vista de columna en [!DNL Assets] interfaz de usuario | Teclas de flecha arriba y abajo | Navegue hasta archivos y carpetas dentro de la misma jerarquía. |
| Vista de columna en [!DNL Assets] interfaz de usuario | Teclas de flecha izquierda y derecha | Vaya a los archivos y carpetas que se encuentran por encima o por debajo de la carpeta actual. |
| Exploración de carpetas en [!DNL Assets] | `/` | Invoque la búsqueda abriendo el cuadro Omnisearch. |
| [!DNL Assets] Consola | &grave; | Conmutar raíles laterales |
| [!DNL Assets] Consola | `Alt + 1` | Abra el árbol de contenido. |
| [!DNL Assets] Consola | `Alt + 2` | Abrir [!UICONTROL Navegación] carril izquierdo. |
| [!DNL Assets] Consola | `Alt + 3` | Mostrar [!UICONTROL Cronología] de un recurso seleccionado. |
| [!DNL Assets] Consola | `Alt + 4` | Abra las referencias de Live Copy del recurso seleccionado. |
| [!DNL Assets] Consola | `Alt + 5` | Inicie la búsqueda y busque dentro de la carpeta seleccionada. |
| Se ha seleccionado el recurso o la carpeta | Retroceso | Eliminar el recurso o la carpeta seleccionados. |
| Se ha seleccionado el recurso o la carpeta | `p` | Abra la página Propiedades del recurso seleccionado. |
| Se ha seleccionado el recurso o la carpeta | `e` | Editar el recurso seleccionado. |
| Se ha seleccionado el recurso o la carpeta | `m` | Mover el recurso seleccionado. |
| Se ha seleccionado el recurso o la carpeta | `Ctrl + c` | Copie el recurso seleccionado. |
| Se ha seleccionado el recurso o la carpeta | `Esc` | Cancelar la selección. |
| Se abre el cuadro de diálogo y está enfocado | `Esc` | Cerrar cuadro de diálogo. |
| Dentro de una carpeta en DAM | `Ctrl + v` | Pegue el recurso copiado. |
| [!DNL Assets] Consola | `Ctrl + A` | Seleccionar todos los recursos. |
| Páginas de propiedades de recursos | `Ctrl + S` | Guardar cambios. |
| [!DNL Assets] Consola | `?` | Consulte una lista de métodos abreviados de teclado. |

## Inicio de sesión y navegación [!DNL Assets] interfaz de usuario {#login}

Los usuarios pueden utilizar el teclado para desplazarse a y rellenar el campo de inicio de sesión para iniciar sesión. Los mensajes de error debido a combinaciones incorrectas de nombre de usuario y contraseña en la página de inicio de sesión los anuncian los lectores de pantalla cada vez que se produce el error.

Después de iniciar sesión, los usuarios de DAM pueden navegar dentro de [!DNL Assets] interfaz de usuario con teclado. Los elementos de la interfaz de usuario, como el carril izquierdo, los menús, el perfil de usuario, la barra de búsqueda, los archivos y carpetas y las opciones de administración y configuración, se pueden navegar mediante el teclado. El orden de navegación del teclado es de izquierda a derecha y de arriba a abajo. Al navegar con un teclado, una opción procesable cuando está enfocado se resalta con mejor contraste de color y se narra mediante un lector de pantalla. Cuando corresponde, un lector de pantalla anuncia el estado (por ejemplo, expandido, contraído y de estado mixto) de las opciones enfocadas del menú. Además, el lector de pantalla anuncia el propósito de la opción procesable, en lugar de, por ejemplo, la apariencia o la ubicación de la interfaz.

Si un usuario expande la ayuda o la opción de perfil de usuario desde el menú, el lector de pantalla anuncia la opción o el estado correspondientes. Si un usuario amplía la opción de perfil de usuario, las opciones disponibles se pueden seleccionar mediante un teclado. Por ejemplo, un administrador puede suplantar a un usuario diferente. Si un usuario busca una cadena desde el [!UICONTROL Ayuda] , un narrador anuncia &quot;Buscando en la Ayuda&quot; para indicar que se está realizando una búsqueda.

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## Examinar recursos y ver información relacionada {#browse}

En el [!DNL Assets] En la interfaz de usuario de, los usuarios pueden utilizar el teclado para examinar la lista de recursos digitales existentes en el repositorio de DAM, previsualizar o descargar un recurso, ver representaciones generadas, cambiar vistas, ver las representaciones generadas, ver la cronología y el historial de versiones, ver comentarios y referencias, y ver y administrar metadatos.

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog was not accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

Al examinar el repositorio de recursos, la siguiente funcionalidad mejora la accesibilidad:

* El lector de pantalla anuncia alternativas de texto que ilustran el propósito o la funcionalidad de los iconos en lugar de sus nombres.
* Los usuarios pueden acceder a las opciones interactivas de la interfaz de usuario y centrarlas en la lista de recursos Referencias mediante las teclas del teclado.
* Los lectores de pantalla anuncian los elementos de cada fila en la vista de lista como elementos de la misma fila.
* Al navegar mediante `Tab` , el enfoque puede moverse a la opción cerrar en la vista previa de la versión.
* Al utilizar el teclado para examinar, las opciones de interfaz de usuario procesables resaltadas tienen un enfoque visual más prominente con un contraste mejorado. Hace que el área enfocada sea más identificable para el usuario.
* Uso del `Esc` La tecla para quitar los iconos de acción rápida de la vista de miniaturas no quita el foco del teclado del último elemento centrado.
* Con un recurso seleccionado, seleccione `Alt + 4` atajo de teclado abre el [!UICONTROL Referencias] en el carril izquierdo. Uso de `Tab` , los usuarios pueden navegar por las entradas de referencia distintas de cero. Al examinar sólo las entradas de referencia distintas de cero, se ahorra esfuerzo y también las pulsaciones de teclas.
* Los comentarios de un recurso están disponibles en la cronología del recurso. Es accesible si se accede al carril izquierdo mediante un teclado o un método abreviado de teclado.
* [!UICONTROL Configuración de vista] in [!DNL Experience Manager] son accesibles mediante un teclado. Los usuarios pueden desplazarse por los tamaños de tarjeta disponibles mediante las teclas de dirección y seleccionar y tabular para desplazarse por otros elementos de la vista Configuración de vista existente y establecerlos.

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## Administrar recursos digitales {#manage-assets}

Muchas tareas de administración de recursos, como las operaciones de CRUD, la descarga de un recurso y la adición de metadatos, son accesibles en varios grados. [!DNL Assets] permite realizar las tareas utilizando varias tecnologías de asistencia, como un lector de pantalla y un teclado.

Vea un vídeo de demostración sobre cómo utilizar un teclado para [examine el repositorio y descargue un recurso](https://youtu.be/K3dgqMRQJys).

Para las operaciones de metadatos que suelen realizar funciones como especialistas en marketing y administradores, las siguientes funciones mejoran la accesibilidad:

* [!UICONTROL Guardar y cerrar] opción en el recurso [!UICONTROL Propiedades] ahora se puede acceder a la página mediante el teclado.
* Los lectores de pantalla anuncian las opciones para eliminar las etiquetas seleccionadas en [!UICONTROL Básico] pestaña de recurso [!UICONTROL Propiedades].
* Los usuarios pueden utilizar el cuadro de diálogo emergente Selector de fecha con un teclado. El elemento de interfaz de usuario Selector de fecha se utiliza para establecer las horas de activación y desactivación, y seleccionar la fecha.
* La funcionalidad de arrastrar mediante el teclado funciona correctamente en [!UICONTROL Editor de esquemas de metadatos] en el modo examinar del lector de pantalla.
* Un usuario puede mover el enfoque con el teclado al campo Añadir usuario o grupo en [!UICONTROL Grupo de usuarios cerrado] en el [!UICONTROL Permisos] pestaña de la carpeta [!UICONTROL Propiedades].

## Buscar recursos digitales {#search-assets}

Una experiencia de búsqueda de recursos rápida y perfecta aumenta la velocidad de contenido. Los casos de uso de velocidad de contenido son parte del núcleo [!DNL Assets] funcionalidad. Para iniciar una búsqueda desde la barra de Omnisearch, los usuarios pueden utilizar métodos abreviados de teclado `/` o use `Tab` junto con lectores de pantalla para localizar rápidamente la opción de búsqueda. El lector de pantalla narra el nombre de la opción como &quot;Botón de búsqueda&quot; cuando el enfoque está en la opción de búsqueda ![opción de búsqueda](assets/do-not-localize/search_icon.png). Los usuarios pueden seleccionar `Return` para abrir el cuadro Omnisearch. El lector de pantalla no solo narra la palabra clave escrita en el cuadro de búsqueda, sino que también narra las sugerencias ofrecidas por [!DNL Experience Manager Assets]. Los usuarios pueden utilizar una combinación de teclas de dirección, `Return`, y `Tab` para acceder a las distintas opciones de déclencheur de una búsqueda.

La funcionalidad de búsqueda se hace accesible mediante la siguiente funcionalidad:

* El título de página, disponible para un lector de pantalla, ayuda a identificar la página como página de búsqueda de recursos.
* Los usuarios buscan recursos desde el campo Omnisearch. Los usuarios pueden abrirlo con la navegación mediante el teclado o con el método abreviado de teclado `/`.
* Los usuarios pueden empezar a escribir la palabra clave de búsqueda y, a continuación, seleccionar las sugerencias automáticas utilizando las teclas de flecha. La sugerencia destacada se puede seleccionar mediante las opciones `Return` clave y recursos se buscan para la sugerencia seleccionada.
* Los lectores de pantalla pueden identificar y anunciar las casillas de verificación de estado mixto (en las que, a menos que seleccione todos los predicados anidados, las casillas de verificación de primer nivel no están seleccionadas y se atraviesan) en el panel Filtros al filtrar los resultados de búsqueda.
* El enfoque del usuario se desplaza a las opciones de búsqueda una vez cerrado el cuadro Omnisearch.

Al filtrar los resultados de búsqueda:

* La página de resultados de búsqueda tiene un título informativo para comprender mejor a los usuarios del lector de pantalla.
* Un lector de pantalla anuncia las opciones en el filtro de búsqueda como acordeones expandibles.
* Los lectores de pantalla anuncian los predicados con opciones de estado mixto.

## Compartir recursos {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

Al compartir recursos, las siguientes funcionalidades mejoran la accesibilidad:

* Un usuario puede mover el enfoque con el teclado dentro del campo Buscar y agregar dirección de correo electrónico en el cuadro de diálogo de uso compartido de vínculos.

* En el cuadro de diálogo de uso compartido de vínculos, al navegar en el modo de exploración, los lectores de pantalla,

   * No narre la información de la tabla cuando se carga el cuadro de diálogo.
   * Puede navegar a todas las sugerencias de la lista.
   * Narre las sugerencias mostradas para los campos Añadir dirección de correo electrónico y Buscar.

## Documentación accesible {#accessible-docs}

[!DNL Experience Manager] proporciona documentación accesible para su uso por personas con discapacidades. A continuación, se ayuda a que la oferta de contenido sea accesible por ahora, mientras que Adobe sigue mejorando la plantilla y el contenido:

* Los lectores de pantalla pueden leer el texto.
* Las imágenes e ilustraciones tienen texto alternativo disponible.
* Se puede navegar con el teclado.
* Las relaciones de contraste ayudan a resaltar algunas partes del sitio web de documentación.

## Proporcionar comentarios {#a11y-feedback}

Para proporcionar comentarios, formular preguntas y solicitar mejoras del producto, relacionadas con la accesibilidad, utilice los siguientes métodos:

* Rellene el formulario en [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html).
* Envíenos un correo electrónico a access@adobe.com.

>[!MORELIKETHIS]
>
>* [Funciones de accesibilidad en [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).
>* [Notas de la versión de las mejoras realizadas en cada versión del Service Pack](/help/release-notes/release-notes.md).
>* [[!DNL Adobe Experience Manager] guía de accesibilidad](/help/managing/web-accessibility.md).
>* [ACR Informes de conformidad () y listado de VPAT para soluciones de Adobe](https://www.adobe.com/accessibility/compliance.html).
