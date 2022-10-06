---
title: Funciones e interfaces accesibles de [!DNL Experience Manager Assets]
description: Conozca las funciones de accesibilidad de [!DNL Adobe Experience Manager] 6,5 [!DNL Assets] ayudar a los usuarios con discapacidades.
contentOwner: AG
feature: Asset Management
role: User, Architect, Leader
exl-id: 15555941-99a2-4586-8d7b-b22f3ec17805
source-git-commit: 399ae241593b5cc14ef1c2efd090f0d1fae7c2df
workflow-type: tm+mt
source-wordcount: '1924'
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

[!DNL Adobe Experience Manager] permite a los creadores y editores de contenido ofrecer experiencias increíbles en la web. El Adobe se esfuerza por incluir a los creadores con discapacidades mejorando la accesibilidad de [!DNL Experience Manager]. El software se mejora continuamente para satisfacer las necesidades de todos los tipos de usuarios y cumplir con los estándares mundiales que incluyen personas con discapacidades visuales, auditivas, de movilidad o de otro tipo.

[!DNL Experience Manager] publica información de conformidad que describe los estándares a los que se adhiere, describe las características de accesibilidad del producto y describe el nivel de cumplimiento. Los informes de conformidad con la accesibilidad ayudan a [!DNL Experience Manager] los usuarios comprenden el nivel de cumplimiento de los distintos estándares. Las mejoras realizadas en [!DNL Assets] permita que todos los usuarios utilicen fácilmente las interfaces mediante el teclado, el lector de pantalla, los ampliadores y otras tecnologías de asistencia.

[!DNL Experience Manager] ofrece distintos niveles de compatibilidad con las siguientes normas:

* [Directrices de accesibilidad del contenido web (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [Se ha revisado el artículo 508 de la Ley de rehabilitación](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines).
* [Iniciativa de accesibilidad - Aplicaciones de Internet enriquecidas accesibles (WAI-ARIA) por W3C](https://www.w3.org/WAI/standards-guidelines/aria/).
* [ES 301 549](https://en.wikipedia.org/wiki/EN_301_549).

Para leer un informe con detalles sobre el nivel de cumplimiento, consulte [Informe de conformidad de accesibilidad](https://www.adobe.com/accessibility/compliance.html) (ACR).

Para saber cómo [!DNL Dynamic Media] es accesible, consulte [accesibilidad en [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

## Tecnologías de asistencia {#at-support}

Los usuarios con discapacidades suelen depender del hardware y el software para acceder al contenido web y utilizar productos de software. Estas herramientas se conocen como tecnologías de asistencia. [!DNL Experience Manager Assets] puede trabajar con los siguientes tipos de tecnologías de asistencia (AT) al utilizar las funcionalidades principales del software:

* Lectores de pantalla y ampliador de pantalla.
* Software de reconocimiento de voz.
* Uso del teclado: navegación y métodos abreviados.
* Hardware de asistencia, incluidos controles de conmutador, pantallas Braille actualizables y otros dispositivos de entrada de equipo.
* Herramientas de ampliación de la interfaz de usuario.

## [!DNL Experience Manager Assets] casos de uso accesibles {#accessible-assets-use-cases}

En [!DNL Experience Manager], las funciones de accesibilidad cumplen dos requisitos clave de [!DNL Experience Manager] usuarios y sus clientes.

* Para los diseñadores y creadores de contenido, existen funciones para crear y publicar contenido accesible que sus clientes y visitantes del sitio web utilizan a su vez. Las personas con discapacidades utilizan el contenido con la ayuda de tecnologías de asistencia. Para obtener más información, consulte [directrices de accesibilidad web](/help/managing/web-accessibility.md).
* [!DNL Experience Manager] también permite que sus usuarios y administradores con discapacidades accedan a la interfaz de usuario y a los controles para crear y administrar el contenido. Las personas con discapacidades pueden utilizar tecnologías de asistencia para desplazarse, utilizar y administrar la variable [!DNL Assets] capacidad.

Las funciones principales de [!DNL Assets] son más accesibles que antes y se actualizan periódicamente para mejorar el cumplimiento de las normas globales. Las operaciones de CRUD en [!DNL Assets] tienen un cierto grado de accesibilidad integrado en ellas. Los flujos de trabajo de DAM, como agregar, administrar, buscar y distribuir recursos, son accesibles mediante métodos abreviados de teclado, texto del lector de pantalla, contraste de color, etc.

## Compatibilidad con el uso del teclado {#keyboard-use}

Muchos elementos de la interfaz de usuario en los que se puede hacer clic o en los que se puede actuar con un puntero también se pueden utilizar con el teclado. Con un teclado, los usuarios pueden centrarse en los elementos de la interfaz de usuario y realizar una acción adecuada. Los usuarios pueden utilizar directamente los métodos abreviados del teclado para almacenar en déclencheur un comando o una acción sin tener que centrarse en los elementos de la interfaz de usuario y colocarlos en déclencheur mediante el teclado. Por ejemplo, los usuarios pueden abrir la línea de tiempo de un recurso en la parte izquierda de la interfaz de usuario navegando hasta el control de interfaz de usuario mediante un teclado y seleccionando `Return`y seleccionando `Alt + 2` atajo de teclado.

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### Métodos abreviados del teclado en [!DNL Assets] {#keyboard-shortcuts}

Las siguientes acciones en [!DNL Assets] trabaje con los métodos abreviados del teclado enumerados. La mayoría de los métodos abreviados del teclado que se aplican a [!DNL Experience Manager] Las consolas también se aplican a [!DNL Assets]. Consulte [combinaciones de teclas para las consolas](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts). Consulte cómo [activar o desactivar los métodos abreviados del teclado](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts).

| Interfaz de usuario o situación | Métodos abreviados del teclado | Acción |
|---|---|---|
| Vista de columna en [!DNL Assets] interfaz de usuario | Teclas de flecha arriba y abajo | Vaya a archivos y carpetas dentro de la misma jerarquía. |
| Vista de columna en [!DNL Assets] interfaz de usuario | Teclas de flecha izquierda y derecha | Vaya a los archivos y carpetas situados encima o debajo de la carpeta actual. |
| Exploración de carpetas en [!DNL Assets] | `/` | Invocar la búsqueda abriendo el cuadro Omnisearch . |
| [!DNL Assets] Consola | &grave; | Conmutar raíles laterales |
| [!DNL Assets] Consola | `Alt + 1` | Abra el árbol de contenido. |
| [!DNL Assets] Consola | `Alt + 2` | Apertura [!UICONTROL Navegación] carril izquierdo. |
| [!DNL Assets] Consola | `Alt + 3` | Mostrar [!UICONTROL Cronología] de un recurso seleccionado. |
| [!DNL Assets] Consola | `Alt + 4` | Abra las referencias de Live Copy del recurso seleccionado. |
| [!DNL Assets] Consola | `Alt + 5` | Inicie la búsqueda y la búsqueda dentro de la carpeta seleccionada. |
| El recurso o la carpeta están seleccionados | Retroceso | Elimine el recurso o la carpeta seleccionados. |
| El recurso o la carpeta están seleccionados | `p` | Abra la página Propiedades del recurso seleccionado. |
| El recurso o la carpeta están seleccionados | `e` | Edite el recurso seleccionado. |
| El recurso o la carpeta están seleccionados | `m` | Mover el recurso seleccionado. |
| El recurso o la carpeta están seleccionados | `Ctrl + c` | Copie el recurso seleccionado. |
| El recurso o la carpeta están seleccionados | `Esc` | Cancelar la selección. |
| El cuadro de diálogo se abre y está en el foco | `Esc` | Cerrar. |
| Dentro de una carpeta en DAM | `Ctrl + v` | Pegue el recurso copiado. |
| [!DNL Assets] Consola | `Ctrl + A` | Seleccione todos los recursos. |
| Páginas de propiedad de recursos | `Ctrl + S` | Guarde los cambios. |
| [!DNL Assets] Consola | `?` | Consulte una lista de métodos abreviados del teclado. |

## Iniciar sesión y navegar [!DNL Assets] interfaz de usuario {#login}

Los usuarios pueden utilizar el teclado para desplazarse hasta el campo de inicio de sesión y rellenarlo para iniciar sesión. Los lectores de pantalla anuncian los mensajes de error debido a combinaciones incorrectas de nombre de usuario y contraseña en la página de inicio de sesión cada vez que se produce el error.

Después de iniciar sesión, los usuarios de DAM pueden navegar dentro de [!DNL Assets] interfaz de usuario mediante el teclado. Los elementos de la interfaz de usuario, como el carril izquierdo, los menús, el perfil de usuario, la barra de búsqueda, los archivos y carpetas, y los ajustes de administración y configuración se pueden navegar mediante el teclado. El orden de navegación del teclado es de izquierda a derecha y de arriba a abajo. Al navegar mediante un teclado, una opción procesable cuando está enfocada se resalta con mejor contraste de color y la narran los lectores de pantalla. Cuando corresponde, el estado (por ejemplo, expandido, contraído y de estado mixto) de las opciones centradas en el menú lo anuncia un lector de pantalla. Además, el lector de pantalla anuncia el propósito de la opción procesable, en lugar de indicar el aspecto o la ubicación de la interfaz.

Si un usuario amplía la opción de ayuda o perfil de usuario desde el menú, el lector de pantalla anuncia la opción o el estado correspondientes. Si un usuario amplía la opción de perfil de usuario, las opciones disponibles se pueden seleccionar mediante un teclado. Por ejemplo, un administrador puede suplantar a un usuario diferente. Si un usuario busca una cadena desde la [!UICONTROL Ayuda] , un narrador anuncia &quot;Búsqueda de ayuda&quot; para indicar que la búsqueda está en curso.

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## Examinar recursos y ver la información relacionada {#browse}

En el [!DNL Assets] interfaz de usuario de , los usuarios pueden utilizar el teclado para navegar por la lista de recursos digitales existentes en el repositorio de DAM, previsualizar o descargar un recurso, ver representaciones generadas, cambiar de vista, ver las representaciones generadas, ver la cronología y el historial de versiones, ver comentarios y referencias, y ver y administrar metadatos.

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

Al examinar el repositorio de recursos, la siguiente funcionalidad mejora la accesibilidad:

* El lector de pantalla anuncia alternativas textuales que ilustran el propósito o la funcionalidad de los iconos en lugar de sus nombres.
* Los usuarios pueden acceder y enfocar las opciones de la interfaz de usuario interactiva en la lista de referencias de los recursos mediante las teclas de teclado.
* Los lectores de pantalla anuncian los elementos de cada fila de la vista de lista como los elementos de la misma fila.
* Al navegar mediante `Tab` , el enfoque puede moverse a la opción de cierre en la vista previa de la versión.
* Al utilizar el teclado para examinar, las opciones de interfaz de usuario procesables resaltadas tienen un enfoque visual más destacado con un contraste mejorado. Hace que el área centrada sea más identificable para el usuario.
* Uso del `Esc` para eliminar los iconos de acción rápida de la vista de miniaturas, no se quita el foco del teclado del último elemento seleccionado.
* Con un recurso seleccionado, seleccionar `Alt + 4` la combinación de teclas abre [!UICONTROL Referencias] en el carril izquierdo. Uso `Tab` , los usuarios pueden navegar por las entradas de referencia diferentes de cero. Al navegar solo por las entradas de referencia diferentes de cero también se ahorran esfuerzos y pulsaciones de teclas.
* Los comentarios de un recurso están disponibles en la cronología de recursos. Se puede acceder a él si se accede al carril izquierdo mediante un teclado o un método abreviado de teclado.
* [!UICONTROL Configuración de vista] en [!DNL Experience Manager] son accesibles mediante un teclado. Los usuarios pueden navegar por los tamaños de tarjeta disponibles mediante las teclas de flecha y seleccionar y desplazarse por las fichas para navegar y establecer otros elementos en la vista Configuración de vista existente.

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## Administre recursos digitales {#manage-assets}

Muchas tareas de administración de recursos, como operaciones CRUD, descarga de recursos y adición de metadatos, son accesibles en varios grados. [!DNL Assets] permite realizar las tareas utilizando varias tecnologías de asistencia, como un lector de pantalla y un teclado.

Vea una demostración en vídeo de cómo utilizar un teclado para [examinar el repositorio y descargar un recurso](https://youtu.be/K3dgqMRQJys).

Para las operaciones de metadatos que suelen realizar funciones como especialistas en marketing y administradores, las siguientes funciones mejoran la accesibilidad:

* [!UICONTROL Guardar y cerrar] opción en el recurso [!UICONTROL Propiedades] ahora se puede acceder a la página mediante el teclado.
* Los lectores de pantalla anuncian las opciones para eliminar las etiquetas seleccionadas en [!UICONTROL Básico] pestaña de recurso [!UICONTROL Propiedades].
* Los usuarios pueden utilizar el cuadro de diálogo emergente Marcador de datos con un teclado. El elemento Interfaz de usuario del selector de datos se utiliza para establecer horas de trabajo y horas de inactividad y seleccionar fecha.
* La funcionalidad de arrastrar con el teclado funciona correctamente en [!UICONTROL Editor de esquemas de metadatos] en el modo Examinar del lector de pantalla.
* Un usuario puede mover el foco mediante el teclado al campo Agregar usuario o grupo de [!UICONTROL Grupo de usuarios cerrado] en el [!UICONTROL Permisos] pestaña de carpeta [!UICONTROL Propiedades].

## Buscar recursos digitales {#search-assets}

Una experiencia de búsqueda de recursos rápida y sin problemas aumenta la velocidad de contenido. Los casos de uso de velocidad de contenido son parte del núcleo [!DNL Assets] funcionalidad. Para iniciar una búsqueda desde la barra Omnisearch, los usuarios pueden utilizar la combinación de teclas `/` o use `Tab` junto con lectores de pantalla para localizar rápidamente la opción de búsqueda. El lector de pantalla narra el nombre de la opción como &quot;Botón de búsqueda&quot; cuando el foco está en la opción de búsqueda ![opción de búsqueda](assets/do-not-localize/search_icon.png). Los usuarios pueden seleccionar `Return` para abrir el cuadro Omnisearch. El lector de pantalla no solo narra la palabra clave escrita en el cuadro de búsqueda, sino que también narra las sugerencias que ofrece [!DNL Experience Manager Assets]. Los usuarios pueden utilizar una combinación de teclas de flecha, `Return`y `Tab` para acceder a las distintas opciones para almacenar en déclencheur una búsqueda.

La funcionalidad de búsqueda es accesible a través de la siguiente funcionalidad:

* El título de la página, según esté disponible para un lector de pantalla, ayuda a identificar la página como página de búsqueda de recursos.
* Los usuarios buscan recursos desde el campo Omnisearch . Los usuarios pueden abrirlo mediante la navegación mediante el teclado o el método abreviado de teclado `/`.
* Los usuarios pueden empezar a escribir la palabra clave de búsqueda y luego seleccionar las sugerencias automáticas mediante las teclas de flecha. La sugerencia resaltada se puede seleccionar utilizando la variable `Return` la sugerencia seleccionada se busca en clave y recursos.
* Los lectores de pantalla pueden identificar y anunciar las casillas de verificación de estado mixto (en las que, a menos que seleccione todos los predicados anidados, las casillas de verificación de primer nivel no se seleccionan y se rompen) en el panel Filtros al filtrar los resultados de la búsqueda.
* El enfoque del usuario pasa a las opciones de búsqueda después de cerrar el cuadro Omnisearch .

Al filtrar los resultados de búsqueda:

* La página de resultados de la búsqueda tiene un título informativo para comprender mejor a los usuarios del lector de pantalla.
* Un lector de pantalla anuncia las opciones del filtro de búsqueda como acordeones ampliables.
* Los lectores de pantalla anuncian los predicados que tienen opciones de estado mixto.

## Compartir recursos {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

Al compartir recursos, las siguientes funcionalidades mejoran la accesibilidad:

* Un usuario puede mover el enfoque mediante el teclado del campo Buscar y agregar dirección de correo electrónico del cuadro de diálogo de uso compartido de vínculos.

* En el cuadro de diálogo de uso compartido de vínculos, al navegar en el modo Examinar, los lectores de pantalla,

   * No narre la información de la tabla cuando se carga el cuadro de diálogo.
   * Puede navegar a todas las sugerencias de la lista.
   * Narre las sugerencias mostradas para los campos Añadir dirección de correo electrónico y Buscar .

## Documentación accesible {#accessible-docs}

[!DNL Experience Manager] proporciona documentación accesible para uso de las personas con discapacidades. Lo siguiente ayuda a que la oferta de contenido sea accesible por ahora, mientras que el Adobe sigue mejorando la plantilla y el contenido:

* Los lectores de pantalla pueden leer el texto.
* Las imágenes y las ilustraciones tienen texto alternativo disponible.
* La navegación con el teclado es posible.
* Los índices de contraste ayudan a resaltar algunas partes del sitio web de documentación.

## Proporcionar comentarios {#a11y-feedback}

Para proporcionar comentarios, hacer preguntas y solicitar mejoras del producto relacionadas con la accesibilidad, utilice los siguientes métodos:

* Rellene el formulario en [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html).
* Envíenos un correo electrónico a access@adobe.com.

>[!MORELIKETHIS]
>
>* [Funciones de accesibilidad en [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).
>* [Notas de la versión de las mejoras realizadas en cada versión de Service Pack](/help/release-notes/release-notes.md).
>* [[!DNL Adobe Experience Manager] guía de accesibilidad](/help/managing/web-accessibility.md).
>* [Informes de conformidad (ACR) y listado de VPAT para soluciones de Adobe](https://www.adobe.com/accessibility/compliance.html).

