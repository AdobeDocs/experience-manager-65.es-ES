---
title: Notas de la versión para  [!DNL Adobe Experience Manager]  6.5
description: Encuentre información de la versión, novedades, instrucciones de instalación y una lista de cambios detallada para  [!DNL Adobe Experience Manager]  6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 3e1f704d1d0e64deefe157338ab5081521a45c3c
workflow-type: tm+mt
source-wordcount: '9855'
ht-degree: 19%

---

# Notas de la versión del Service Pack de [!DNL Adobe Experience Manager] 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.24.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versión del Service Pack |
| Fecha | jueves, 26 de noviembre de 2025 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

<!-- OLD DOWNLOAD URL
(https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) -->

## Qué se incluye en [!DNL Experience Manager] 6.5.24.0 {#what-is-included-in-aem-6524}

[!DNL Experience Manager] 6.5.24.0 incluye nuevas funciones, mejoras clave solicitadas por el cliente y correcciones de errores. También incluye mejoras de rendimiento, estabilidad y seguridad publicadas desde la disponibilidad inicial de la versión 6.5 en abril de 2019. [Instalar este Service Pack](#install) en [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->


## Funciones y mejoras clave

### Formularios

* **Compatibilidad para pasar XCI personalizados:** Se agregó compatibilidad para pasar XCI personalizados en parámetros de la aplicación de cmdline xmlformcmd. Esto permite a los usuarios especificar archivos XCI personalizados para realizar pruebas, mejorar la flexibilidad y el control sobre el proceso de prueba. (LC-3923248)


## Problemas corregidos en el Service Pack 24 {#fixed-issues}

<!-- 6.5.24.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Assets] {#assets-sp24}

* Después de actualizar a la versión 6.5.23.0, la ordenación de carpetas por fecha de modificación en la vista de tarjetas causó problemas al localizar recursos modificados recientemente para implementaciones locales. (ASSETS-56946)
* Las entradas de registro de advertencia repetidas se generan durante las ejecuciones del programador. (ASSETS-52554)
* La ordenación de títulos no funciona en la vista de lista. (ASSETS-50716)
* La ventana Propiedades de la colección no se cierra incluso después de hacer clic en el botón Cancelar. (ASSETS-48504)

* Se produce un error de *URL no válida* al intentar realizar anotaciones en recursos en AEM 6.5.22. (NPR-42684)
* El formulario del editor de metadatos de Assets no se reinicializa después de realizar acciones de relación o desrelación. (ASSETS-52207)
* Cuando los recursos del DAM remoto se sincronizan con el sitio local de Sites, el estado publicado de los recursos se actualiza incorrectamente a `Not published`. (ASSETS-48958)
* Problemas al actualizar de SP23 a la versión 6.5 LTS. (ASSETS-50541)

### [!DNL Sites]{#sites-6524}

#### Accesibilidad {#sites-accessibility-6524}

* El cuadro de diálogo **Cambiar formato de visualización** ahora admite la operación completa del teclado. El enfoque ya no omite el botón **Ver configuración** y las claves estándar (`Tab`, `Enter`, `Space`) funcionan de manera consistente. (SITES-24306)
* Los usuarios del teclado pueden quitar las etiquetas de estado publicadas sin necesidad de utilizar el ratón. El enfoque aterriza en cada etiqueta y la activación funciona con `Enter`/`Space` y Retroceso/Eliminación. El control de etiquetas ahora se comporta como un botón, lo que mejora los comentarios de los lectores de pantalla y cumple con WCAG 2.1.1 Keyboard. (SITES-24491)
* El carril de filtros se desplaza responsivamente a las ventanillas móviles estrechas. Los controles de selección y los resultados permanecen dentro de la ventanilla con un zoom del 400 %, lo que elimina el desplazamiento horizontal y el corte de contenido. (SITES-24708)
* AEM restaura el acceso completo mediante el teclado a los botones Restablecer, Personalizar y Dispositivo de ContextHub. Las teclas de tabulación y flecha llegan a cada control, muestran un indicador de enfoque visible y activan acciones con `Enter` o `Space`. Los lectores de pantalla anuncian etiquetas claras. (SITES-24939)
* La entrada de fecha y el selector permanecen totalmente visibles a 320 px. El modal Deformación de tiempo utiliza un tamaño adaptable, por lo que el control ya no recorta ni desaparece en la ventanilla más pequeña. (SITES-24962)
* El carril de referencias ahora admite un zoom del explorador del 400 % sin perder el acceso a su contenido. El carril utiliza un tamaño adaptable en lugar de una anchura fija, por lo que los elementos permanecen visibles y se pueden seleccionar a 1280×1024. (SITES-24972)
* El carril de filtros ahora funciona con un zoom del 400 %. El carril cambia de tamaño con unidades relativas y ya no bloquea ni oculta los controles de filtro. Los usuarios pueden ver y seleccionar cada opción de filtro sin desplazamiento horizontal ni destinos de visita recortados. (SITES-24981)
* Los usuarios de teclado pueden utilizar menús de formato en el modal Teaser. Al presionar `Enter` o `Space` en **Lista** o **Formato de párrafo**, se abre la ventana emergente, las teclas de dirección navegan por las opciones y `Enter` aplica la selección. `Escape` cierra el menú y restaura el enfoque en el control activador, lo que produce un flujo de trabajo de barra de herramientas coherente. (SITES-25235)
* La ventana emergente del selector de color de la muestra ahora permanece dentro de la ventanilla móvil a 320 px. La ventana emergente muestra todas las filas de color y admite el desplazamiento, de modo que los autores pueden seleccionar cualquier muestra en pantallas pequeñas. (SITES-25274)
* Los menús desplegables de la barra de herramientas demográfica ahora funcionan completamente con el teclado. Al abrir un menú, el enfoque se mueve a la primera opción, las teclas de flecha navegan por la lista y Esc/Tab se cierran o avanzan sin dejar el enfoque en la barra de herramientas. Los elementos interactivos utilizan una semántica adecuada para que NVDA y otros lectores anuncien las opciones correctamente. (SITES-25310)
* Añadir componente en el árbol de contenido funciona según se ha diseñado en AEM 6.5 SP24. El error inicial se produjo por la falta de permisos de autor en una configuración local, no de AEM. Los autores con derechos de edición pueden activar el botón y agregar componentes mediante el teclado o el ratón. (SITES-25312)
* El acceso mediante teclado y lector de pantalla en la barra de herramientas Demográfica ahora funciona de forma fiable. Los autores que usan NVDA pueden atravesar **Commerce**, **Persona** y 88 con flechas, observar comentarios de enfoque claros y comprender qué pestaña está activa. (SITES-25326)

* El vínculo **Saltar al contenido** ahora mueve el foco del teclado al encabezado del contenido principal. El enfoque permanece visible en un destino identificado de forma exclusiva, por lo que los lectores de pantalla anuncian la sección correcta. El cambio cumple con WCAG 2.4.1 y 2.4.3. (SITES-24061)
* La navegación mediante el teclado en el árbol de páginas de inicio de Sites sigue una secuencia lógica después de usar **Seleccionar todo**. El enfoque se mueve de **Seleccionar todo** al siguiente control (Abrir carril izquierdo) en lugar de saltar al inicio de la página. (SITES-24307)
* Los títulos de secciones y los controles de edición del editor de Sites responden al enfoque del teclado y a la activación. Los usuarios del teclado muestran el mismo título y las mismas acciones que antes solo aparecían al pasar el ratón por encima. (SITES-24479)
* Los botones del editor de sitios exponen nombres descriptivos en lugar de etiquetas genéricas o que faltan. Las tecnologías de asistencia anuncian la acción correcta, lo que mejora la claridad y reduce los clics erróneos. (SITES-24480)
* Los lectores de pantalla reciben un mensaje hablado que dice &quot;Cargando&quot; mientras la vista de Sites se actualiza. La actualización añade una región activa de estado dedicada y escribe el mensaje en ella mediante programación, lo que confirma el progreso sin desplazar el enfoque. (SITES-24481)
* El carril lateral de Assets ahora incluye un control **Cerrar** y devuelve el enfoque al botón de alternancia. Los usuarios de teclado y lector de pantalla descartan el panel inmediatamente en lugar de desplazarse por cada control. El cambio reduce las pulsaciones de teclas y hace coincidir el comportamiento esperado del panel. (SITES-24489)
* La lista de la pestaña ARIA del Editor de páginas de sitios incluye un nombre descriptivo. Los lectores de pantalla ahora identifican el control como una lista de pestañas y leen la etiqueta correcta, lo que permite a los usuarios encontrar el conjunto correcto de pestañas y moverse entre ellas de forma fiable. (SITES-24492)
* La búsqueda en el carril lateral del Editor ahora anuncia los resultados a los lectores de pantalla. A medida que los usuarios escriben, un mensaje de estado activo informa de la cantidad de coincidencias y actualizaciones sin desplazar el foco. Los usuarios del teclado descubren los resultados inmediatamente. (SITES-24506)
* La selección de filas en la vista de lista mejora para los usuarios de tecnología de asistencia. La casilla de verificación muestra un nombre significativo que se deriva de la fila Título, por lo que los anuncios son breves y describen la acción correctamente. (SITES-24514)
* Nombres de accesibilidad de Vista de lista corregidos. La tabla quita `aria-label` de los elementos no interactivos y asigna la etiqueta al vínculo o botón procesable. Los usuarios del lector de pantalla ahora escuchan etiquetas precisas y no duplicadas en toda la columna. (SITES-24515)
* El encabezado adhesivo dejó de ocultar el cuadro de diálogo modal de teaser durante el uso de zoom alto. El contenido sigue siendo legible y utilizable con un zoom del 200% y el 400%, con flujo vertical y sin secciones recortadas. (SITES-24523)
* Escribir en el campo de búsqueda ya no déclencheur un anuncio prematuro del primer resultado o una activación accidental. La experiencia ahora anuncia un mensaje de estado conciso con el recuento de resultados, mientras que el enfoque permanece en el campo hasta que el usuario navega a la lista. (SITES-24658)
* El campo Texto alternativo del cuadro de diálogo de hipervínculos del editor de texto ahora expone una etiqueta programática. Los lectores de pantalla anuncian &quot;Texto alternativo&quot; para el campo y el enfoque aterriza en el control con el nombre correcto. Esta corrección mejora la navegación para los usuarios de teclado y voz. (SITES-24675)
* Se ha añadido un mensaje de estado activo al carril Referencias para que las tecnologías de asistencia anuncien cambios inmediatamente. Déclencheur Al seleccionar varios elementos, aparece un mensaje claro sobre la disponibilidad de la referencia, que evita los cambios de estado silencioso y reduce las acciones repetidas. (SITES-24678)
* El cuadro de diálogo Imagen ahora anuncia su estado de carga a través de una región activa ARIA. Los lectores de pantalla escuchan el mensaje &quot;Cargando, espere&quot; mientras aparece el control de número. Y, una actualización lista cuando termine el contenido, para que los usuarios sepan cuándo pueden interactuar. (SITES-24697)
* El cuadro de diálogo Selección de vínculo ahora muestra una región activa que anuncia los resultados de la búsqueda. Los lectores de pantalla oyen el estado &quot;resultados actualizados&quot; después de cada búsqueda sin desplazar el foco, por lo que los usuarios obtienen una confirmación clara de que la búsqueda se ha completado. (SITES-24700)
* El cuadro de diálogo Selección de vínculo ahora se refleja en 320 px. Todos los campos y acciones permanecen visibles y utilizables, y la barra de desplazamiento horizontal ya no aparece. (SITES-24709)
* El cuadro de diálogo Selección de vínculos ahora utiliza la misma etiqueta para el texto en pantalla y para el nombre accesible en cada elemento de árbol. Los lectores de pantalla anuncian cada elemento mientras se mueven con las teclas de flecha, incluido el último nivel, lo que elimina los nodos silenciosos y los nombres que no coinciden. (SITES-24710)
* Los filtros de cambio ahora informan de su estado como expandido o contraído. El botón conmuta `aria-expanded` de forma sincronizada con el panel de filtros y muestra un solo nombre no cifrado (&quot;Cambiar filtros&quot;), con lo que se elimina el confuso &quot;¿filtro?&quot; anuncio. Los usuarios del lector de pantalla pueden predecir el resultado de activar el control. (SITES-24713)
* Los encabezados modales ya no cubren el contenido con una anchura de 320 píxeles. El encabezado se libera de su estado adhesivo y el cuerpo del cuadro de diálogo se desplaza, de modo que todos los campos y botones de acción permanecen visibles y se pueden utilizar. Los usuarios del teclado pueden llegar a todos los controles sin perder el enfoque. (SITES-24718)
* Los vínculos de navegación de la aplicación ahora exponen la semántica de los vínculos adecuada. Los lectores de pantalla anuncian cada elemento como un vínculo en lugar de como un elemento de lista, lo que mejora la navegación mediante el teclado y el control por voz. El contenedor de lista mantiene la semántica de la lista, mientras que los vínculos siguen siendo los destinatarios enfocables. (SITES-24719)
* El estado de los resultados ahora anuncia a los lectores de pantalla cuando cambian los filtros. La NVDA lee tanto el recuento &quot;X de Y resultados&quot; como el mensaje &quot;sin resultados&quot;. El estado de paginación utiliza una región activa que se actualiza in situ, de modo que los usuarios escuchan la confirmación sin desplazar el foco. (SITES-24720)
* El botón de giro del cuadro de diálogo Carrusel anuncia ahora un nombre único y conciso para los lectores de pantalla. El control ya no repite la etiqueta de grupo ni la de entrada, lo que reduce el nivel de detalle y la confusión para los usuarios de NVDA. (SITES-24725)
* La lista de búsqueda del menú Ayuda expone la semántica adecuada. El contenedor presenta una lista y cada resultado permanece como un vínculo sin una función en conflicto. NVDA y JAWS anuncian los vínculos con precisión y la navegación sigue siendo coherente. (SITES-24729)
* Adobe ha corregido la ventana emergente de muestra de color en Preferencias del usuario, de modo que NVDA anuncia la muestra enfocada, no la seleccionada anteriormente. Los usuarios del teclado escuchan nombres de color precisos mientras se desplazan por la lista y pueden confirmar la selección correcta. (SITES-24739)
* NVDA ahora lee la descripción completa en el directorio de árbol. El panel de detalles expone el texto multilínea como un valor y lo vincula a la etiqueta del campo. Los usuarios del teclado escuchan el texto completo mientras tabulan por los campos de solo lectura. (SITES-24780)
* El directorio de árbol ahora anuncia la fecha de modificación. NVDA lee la fecha en la que el enfoque se mueve a la columna Modificado. La cuadrícula vincula cada fecha con el nombre del elemento para que los usuarios escuchen el archivo y su última actualización. (SITES-24782)
* El modo de vista previa ahora respeta las preferencias de espaciado de texto del usuario. El lienzo refleja los cambios de altura de letra, palabra y línea en todo el contenido previsualizado. El texto ya no permanece fijo ni se recorta mientras aumenta el espaciado. Los usuarios de teclado y visión reducida leen el contenido sin saltos de diseño. (SITES-24936)
* AEM corrige el orden de tabulación en las páginas del Editor de Assets. La tabulación ahora se desplaza de los controles del encabezado a los botones del concentrador de contactos y, finalmente, a las herramientas del lienzo en una secuencia clara. Los lectores de pantalla siguen el mismo orden, lo que elimina la confusión y acelera la navegación mediante el teclado. (SITES-24937)
* AEM agrega un nombre de programación a la barra de menús Acciones de tarjeta. Los lectores de pantalla anuncian el control correctamente y los usuarios de voz pueden dirigirlo por su nombre. La navegación y el enfoque del teclado permanecen inalterados. (SITES-24938)
* Los menús de Vista de tarjeta respetan el espaciado de texto aumentado. El elemento Más acciones aumenta y ya no trunca las etiquetas, incluida la Publicación rápida. Los usuarios que aumentan el espaciado entre letras, palabras o líneas mantienen las etiquetas completas y el acceso mediante el teclado. (SITES-24941)
* Se ha eliminado la función &quot;presentación&quot; que ocultaba la tabla de la página principal de Sites del árbol de accesibilidad. La tabla vuelve a leerse correctamente. NVDA y JAWS detectan la tabla, reconocen los encabezados y anuncian las relaciones de encabezado durante la navegación de filas y columnas. (SITES-24942)
* La ordenación de los comentarios en la vista de lista es explícita y coherente. Después de una ordenación, el encabezado expone el orden a través de `aria-sort`. Anuncia el cambio, mientras que los encabezados sin ordenar ya no reclaman un estado, lo que ayuda a los usuarios del lector de pantalla a rastrear qué columna controla el orden. (SITES-24943)
* El encabezado Editar diseño ya no expone un botón **Editar** que no funciona. El control ahora actúa como una etiqueta de estado estática y permanece fuera del orden de tabulación, por lo que los usuarios del teclado no malgastan una pulsación de tecla. Use **Seleccionar otro modo** para cambiar de modo, con comentarios claros del lector de pantalla. (SITES-24950)
* La barra de herramientas del emulador muestra los nombres completos de los dispositivos de forma predeterminada. La etiqueta ya no se trunca durante la carga, por lo que los usuarios pueden leer y seleccionar dispositivos sin tener dudas. El texto se adapta perfectamente a los niveles de zoom y a las anchuras estrechas. (SITES-24952)
* La barra de herramientas del emulador se adapta a ventanillas pequeñas. A 320 píxeles, la lista de dispositivos y controla la pantalla sin recortar, de modo que los usuarios pueden seleccionar Galaxy S7 y modelos más nuevos. El diseño se adapta y ajusta para evitar el desplazamiento horizontal incluso con un zoom del 400 %. (SITES-24953)
* Los lectores de pantalla anuncian el dispositivo seleccionado y sus medidas en el emulador. NVDA deja de leer el flujo de regla; el botón del dispositivo utiliza una descripción adjunta para el texto de información del objeto, que reduce el ruido y guía la navegación. (SITES-24955)
* La barra de filtro ahora trata cada etiqueta seleccionada como un botón de acción. Borrar nombres accesibles y controlar el enfoque mejoran los anuncios y el control del teclado. (SITES-24980)
* Las actualizaciones de estado en la vista del filtro de administración de sitios se anuncian a los lectores de pantalla. Cuando los usuarios cambian de Tarjeta/Lista mientras se cargan los elementos, NVDA ahora transmite el mensaje &quot;Por favor, espere&quot; a través de una región activa. Esta guía evita clics y confusiones adicionales. (SITES-24992)
* El foco del teclado ahora se mueve en un orden lógico cuando los usuarios expanden el carril izquierdo. El enfoque cambia directamente del botón del carril izquierdo al contenido expandido, lo que elimina la necesidad de volver atrás u omitir elementos. Este cambio mejora la accesibilidad para los usuarios del lector de pantalla y del teclado. (SITES-24998)
* Los comentarios del lector de pantalla del botón **Editar** ahora coinciden con el control. Al activar el botón se anuncia la acción Editar en lugar de un mensaje de vista previa, lo que mejora la claridad y reduce los errores de entrada para los usuarios que no son usuarios del ratón. (SITES-25208)
* La acción de confirmación en el cuadro de diálogo Teaser se anuncia correctamente a los lectores de pantalla. Los informes de control &quot;Confirmar&quot;, no la descripción del icono, lo que proporciona a los usuarios del teclado y del lector de pantalla una guía clara. (SITES-25223)
* El botón Ayuda ahora muestra un nombre de acceso no cifrado. Los lectores de pantalla anuncian &quot;Ayuda&quot; en lugar de una descripción detallada del icono. Los usuarios comprenden la acción y pueden encontrar asistencia más rápido. (SITES-25224)
* El modal Deformación de tiempo muestra un anillo de enfoque claro en los vínculos **`Set Date`** y **Deformación de tiempo de salida**. Los usuarios que pulsan ven exactamente dónde aterriza el enfoque y evitan acciones no deseadas. El anillo mantiene al menos un contraste de 3:1 contra el fondo. (SITES-25232)
* Los lectores de pantalla ahora anuncian los controles Anotar y Cerrar anotación con precisión en la barra de herramientas Anotación. La NVDA ya no dice &quot;Previsualizar botón presionado&quot;, lo que engañó a los autores y sugirió la acción incorrecta. El anuncio coincide con el botón presionado y mantiene el flujo de trabajo despejado. (SITES-25234)
* La navegación mediante el teclado en la barra de herramientas de anotaciones se comporta de forma coherente. El enfoque ya no salta a Exit al abrir el modo y, en su lugar, se mueve al control inicial para agregar anotaciones. Los usuarios navegan por los controles en secuencia sin tabulación inversa. (SITES-25241)
* La visualización en pantalla pequeña funciona según lo esperado en el modal Teaser. El cuadro de diálogo ya no crea una barra de desplazamiento horizontal de 320 píxeles y la barra de herramientas permanece accesible sin necesidad de desplazarse lateralmente. Esta actualización ayuda a los usuarios con poca visión que hacen zoom en la página. (SITES-25242)
* La visualización en pantalla pequeña funciona según lo esperado en el modal Image. El cuadro de diálogo ya no crea una barra de desplazamiento horizontal de 320 píxeles y las herramientas de imagen permanecen accesibles sin necesidad de desplazarse lateralmente. Esta actualización mejora la navegación de los usuarios con poca visión que hacen zoom en la página. (SITES-25244)
* El modal de búsqueda respeta la configuración de espaciado de texto del usuario. Elevar el alto de línea, el espaciado de párrafo, el espaciado entre letras o el espaciado entre palabras ya no corta el texto ni se superpone con el árbol. El contenido se desplaza a los valores de WCAG 1.4.12 y permanece totalmente legible. (SITES-25245)
* El modo de búsqueda ahora se adapta a pantallas pequeñas sin superponerse al directorio de árbol a 320 px. El contenido se desplaza dentro del cuadro de diálogo, sólo mantiene el desplazamiento vertical y mantiene los controles visibles. Esta corrección mejora la legibilidad y la navegación mediante el teclado y se alinea con WCAG Reflow. (SITES-25246)
* El desbordamiento modal de carrusel ya no fuerza el desplazamiento horizontal en anchos del tamaño del teléfono. El componente se adapta a 320 píxeles, conserva el flujo vertical y mantiene los controles a la vista. El cambio mejora la legibilidad y el acceso mediante el teclado durante la creación. (SITES-25254)
* Los flujos de trabajo de anotación ya no pierden el enfoque. El modal coloca el enfoque inicial en un encabezado significativo, evita que el enfoque salte fuera del cuadro de diálogo y restaura el enfoque en el déclencheur después de la desestimación. La salida del lector de pantalla sigue siendo concisa y relevante. (SITES-25257)
* El cuadro de diálogo **Eliminar anotación** ahora controla correctamente el foco del teclado. Al abrir el cuadro de diálogo, el foco se mueve a su encabezado para el contexto del lector de pantalla y, al cerrarlo, se vuelve a enfocar en el botón **Eliminar anotación** que lo inició. Los usuarios ya no aterrizan en controles no relacionados o detrás del modal. (SITES-25258)
* El Selector de fecha de deformación de tiempo ahora administra el enfoque correctamente. Al presionar `Esc`, se vuelve a enfocar el botón **Selector de fecha** y al elegir una fecha, se mueve el enfoque al campo de entrada vinculado. Los usuarios de teclado y lector de pantalla mantienen el contexto y no aterrizan detrás del modal. (SITES-25264)
* Los lectores de pantalla anuncian las acciones correctas para los botones **Anotar** y **Cerrar anotación**. NVDA ya no dice &quot;Previsualizar botón pulsado&quot;; anuncia el nombre del botón para que los usuarios sepan cuándo comienza o termina el modo de anotación. (SITES-25268)
* El modal Anotación ahora muestra una acción **Enviar** clara. Los autores pueden agregar un comentario y enviarlo con el botón del icono del lápiz o descartar el modal con `Esc`, sin adivinar el flujo. (SITES-25269)
* La entrada de anotación incluye botones de acción explícitos. El cuadro de diálogo muestra **Enviar** para guardar la nota y **Cancelar** para cerrarla, ambos accesibles mediante el teclado y anunciados por la tecnología de asistencia. Los autores ya no necesitan depender de hacer clic fuera del cuadro de diálogo o presionar solamente `Esc` para finalizar. (SITES-25281)
* El modo de anotación ahora mantiene el foco del teclado en la superposición y en su barra de herramientas. La página detrás de la superposición ya no recibe atención cuando los autores pulsan la tecla Tab, por lo que los usuarios se mantienen orientados y pueden navegar por las anotaciones sin saltar al contenido subyacente. (SITES-25282)
* El selector de dispositivos de Editar diseño funciona según lo diseñado. Cuando dos opciones de dispositivo tienen anchuras similares (por ejemplo, iPhone 8 Plus junto a Galaxy 7), el botón seleccionado muestra una información del objeto para mostrar la etiqueta completa mientras ambos botones permanecen visibles y accesibles. (SITES-25285)
* Con un zoom del 200 %, Editar diseño ya no supera la página. La barra de herramientas se representa completamente y expone el desplazamiento horizontal cuando es necesario, restaurando el acceso a los controles anteriormente ocultos para los usuarios con problemas de visión. (SITES-25288)
* El orden de tabulación en la vista previa del diseño ahora se mueve de la barra de herramientas principal directamente a la barra de herramientas Demográfica. Los usuarios de teclado y lector de pantalla pueden recorrer los controles en una secuencia predecible en lugar de saltar a la barra de herramientas secundaria. El cambio se ajusta al orden de enfoque de WCAG 2.4.3. (SITES-25305)
* Al ampliar la página al 200 %, ya no se oculta parte de la barra de herramientas Demográfica. La sección de la barra de herramientas administra el desbordamiento y proporciona desplazamiento en su propia región, manteniendo todos los controles visibles y operables a gran ampliación. (SITES-25309)
* Las entradas de texto en la barra de herramientas Demografía ahora exponen nombres accesibles adecuados. Cada campo incluye un ID único con una etiqueta programática, de modo que los lectores de pantalla anuncian el propósito del campo y los usuarios pueden navegar por ella. La etiqueta visible se encuentra cerca del control para mejorar la legibilidad de la visión reducida. (SITES-25316)
* El botón Editar ahora anuncia la acción correcta para filtrar los lectores en la barra de herramientas secundaria. Al activarlo se lee &quot;Editar&quot; en lugar del &quot;botón de previsualización&quot; no relacionado, que elimina la confusión durante la navegación mediante el teclado. (SITES-25320)
* El deslizador del carrito de la barra de herramientas Demografía ahora expone un nombre accesible adecuado. Los lectores de pantalla anuncian que &quot;Total del carro de compras&quot; y las herramientas de entrada de voz pueden dirigir el control por nombre, mejorando el cumplimiento con WCAG 4.1.2 (Nombre, Función, Valor). (SITES-25322)
* El control deslizante de la barra de herramientas Demografía ahora mantiene el enfoque cuando los autores cambian el valor con las teclas de dirección. El enfoque ya no salta al botón del carro de compras, por lo que los usuarios del teclado ajustan el valor continuamente y los lectores de pantalla anuncian cada cambio. (SITES-25324)
* Buscar en Assets ahora Refluir sin problemas a 320 px (aproximadamente 400% de zoom). El modal mantiene los encabezados, campos y acciones legibles y no superpuestos, de modo que los autores pueden buscar sin desplazamiento horizontal. (SITES-25330)
* El panel Assets del editor sigue una secuencia de enfoque lógica. Los usuarios del teclado pulsan las pestañas en cada miniatura y pueden acceder a los controles de salida del panel. El cambio elimina las omisiones y mejora el cumplimiento con WCAG 2.4.3. (SITES-25360)
* AEM actualiza los botones **Lists** y **Paragraphs** del editor de texto enriquecido del modal Teaser para exponer su estado expandido y contraído. Los botones ahora alternan `aria-expanded` y anuncian el cambio de estado a los lectores de pantalla. Los autores obtienen comentarios claros y evitan adivinar antes de abrir o cerrar los menús de formato. (SITES-25365)
* AEM anuncia el estado de carga en el modal Teaser. El modal ahora expone un mensaje de estado activo mientras se carga el contenido, por lo que NVDA y JAWS dicen &quot;Cargando, espere&quot;. Los autores deben recibir comentarios claros y evitar interactuar con el cuadro de diálogo antes de que esté listo. (SITES-25366)
* Mejora la mensajería de estado en la ficha Recurso del cuadro de diálogo Selección de vínculo. Cuando se produce un error, el componente inserta una actualización de estado legible y mantiene el enfoque del teclado estable, lo que permite que NVDA/JAWS informe a los usuarios de inmediato. (SITES-25368)
* Se ha corregido el comportamiento de la IU en el panel Nota para ventanillas muy estrechas. Con 320 píxeles, el título y el control Add entraban en conflicto anteriormente; la barra de herramientas ahora se desplaza y conserva una clara separación entre los elementos. Los autores pueden operar los controles sin pérdida de información o función. (SITES-25376)
* Se ha corregido un estado de error persistente en la ficha **Vínculos y acciones** del cuadro de diálogo **Teaser**. Después de que los autores habiliten **Call to action** y corrijan los campos en blanco o no válidos, la pestaña borrará el estilo y el icono de error y quitará `aria-invalid`. Los lectores de pantalla ya no anuncian un error una vez que se validan los campos. (SITES-25527)
* La administración de errores en los formularios de administración de sitios ahora cumple las expectativas de accesibilidad. Cuando la validación falla, la página muestra el error inmediatamente, cambia el enfoque a un destinatario de mensaje utilizable y expone el texto a lectores de pantalla como JAWS. (SITES-27138)
* Ahora, al crear una carpeta en Sites, se muestra un mensaje de confirmación claro. JAWS anuncia el mensaje a través de la región activa, de modo que los autores reciban comentarios inmediatos y accesibles después de la acción. (SITES-27141)
* Se ha corregido un hueco en la accesibilidad en el que las imágenes de los cuadros de diálogo de creación se representaban sin texto alternativo. El cuadro de diálogo ahora proporciona texto alternativo descriptivo donde sea necesario y texto alternativo vacío para elementos puramente visuales, lo que restaura el comportamiento compatible con JAWS y otros lectores de pantalla. (SITES-27153)
* Tratamiento de errores mejorado en los cuadros de diálogo de creación. Cuando se produce un error de configuración, la interfaz de usuario muestra texto explícito y almacena en déclencheur un anuncio del lector de pantalla mediante una región de alerta. Los autores reciben comentarios inmediatos y pueden corregir el problema sin perder contexto. (SITES-27155)
* Se ha corregido un defecto de accesibilidad Reflow en Administración de sitios. Con un zoom del explorador del 400 %, la barra de herramientas y la cuadrícula controlan las acciones de teclas superpuestas e insertadas fuera de la pantalla, lo que bloquea la navegación mediante el teclado y el uso del lector de pantalla. El diseño ahora se reajusta correctamente para que los botones de búsqueda, filtro y acción permanezcan visibles y operables con un zoom del 400 %. (SITES-27238)
* Contraste bajo corregido en el mensaje de estado de bloqueo que se muestra en la página Flujo de trabajo Bloquear/Desbloquear. El mensaje ahora cumple una proporción de 4,5:1, lo que mejora la legibilidad y el cumplimiento de la ley ADA para los autores. (SITES-27270)
* Se han agregado nombres accesibles a los iconos de marca de verificación en el cuadro de diálogo **Permisos efectivos**. JAWS ahora anuncia los iconos y su significado, mejorando la navegación mediante el teclado y el cumplimiento de las normas ADA. (SITES-27272)
* La navegación oculta en el encabezado aceptaba el enfoque y confundía a los usuarios con visión y al lector de pantalla. La actualización deshabilita el enfoque en los controles contraídos y expone sólo los elementos visibles. La navegación sigue siendo predecible y cumple con WCAG 2.4.3. (SITES-35224)

* Se han corregido los iconos de miniatura de carpeta en el Administrador de sitios para que se comporten como imágenes decorativas. La actualización elimina la función de imagen y aplica texto alternativo vacío, por lo que la tecnología de asistencia ignora los iconos y solo lee etiquetas significativas. (SITES-2852)
* Adobe ha aumentado el contraste de color para el texto Referencias de la página de inicio de Sites. El texto ahora cumple con WCAG 2.1 AA con una relación de al menos 4.5:1 y se lee claramente en temas claros y pantallas brillantes. (SITES-24755)
* El hito del carril Referencias ahora anuncia su nombre a los lectores de pantalla. La región expone un `aria-label` único (&quot;Carril de referencias&quot;), que mejora la navegación de hitos y la distingue de otras regiones. (SITES-24973)
* La descripción RTE bloqueó la navegación de pestañas hacia adelante y el flujo de diálogo se interrumpió. La corrección restaura el movimiento de teclado estándar. Los autores continúan más allá del campo con una sola pestaña y mantienen el orden de selección predecible. (SITES-35228)
* Los controles de creación carecían de nombres accesibles y de texto de icono sin procesar expuesto, lo que confundía a JAWS. La corrección agrega etiquetas ARIA explícitas y funciones estándar. Los anuncios suenan correctos y se alinean con las expectativas de accesibilidad. (SITES-35227)
* A la lista desplegable Categorías le faltaba una etiqueta específica, por lo que JAWS hablaba de un &quot;menú de botón de imágenes&quot; genérico. La actualización asigna al control el nombre &quot;Categorías&quot; y define su función. Los usuarios del lector de pantalla escuchan una etiqueta precisa y comprenden las opciones disponibles. (SITES-35226)
* El cuadro de diálogo Propiedades mostraba una cuadrícula de datos que los lectores de pantalla trataban como texto sin formato. JAWS y NVDA no se centraron y no anunciaron filas y columnas. La corrección agrega semántica de tabla real y funciones ARIA. Los lectores de pantalla ahora reconocen correctamente la tabla y rastrean el enfoque. (SITES-35225)
* El editor de texto Fragmento de contenido está cargado con una barra de acciones truncada. Los iconos se recortaron y el menú de desbordamiento se volvió inaccesible. La actualización corrige el diseño para que la barra de herramientas completa permanezca visible y accesible. (SITES-33005)
* Los campos de formulario de pestañas básicos no mostraban un texto de error útil. El formulario ahora muestra mensajes en línea claros y los vincula al campo para lectores de pantalla. Los usuarios de tecnologías de asistencia y teclado obtienen orientación inmediata para corregir la entrada. (SITES-32480)
* El multicampo utilizado en un componente personalizado expone botones de icono sin etiquetar y un orden de tabulación incoherente. JAWS / NVDA solo anunció &quot;botón&quot; o controles omitidos, lo que bloqueó la operación del teclado. La actualización proporciona nombres descriptivos para Agregar, Quitar y Mover, normaliza las tabulaciones y anuncia actualizaciones de la lista para satisfacer las expectativas de ADA. (SITES-30660)
* La publicación rápida ahora devuelve una notificación de éxito clara. El cuadro de diálogo se cierra, un mensaje confirma la acción y los lectores de pantalla anuncian el mensaje para que los autores no pierdan el resultado. (SITES-26912)
* No se requiere ningún cambio. Adobe ha revisado la afirmación de que el icono de búsqueda se superpone con el texto cercano. El encabezado incluía una etiqueta añadida por el cliente; AEM de vainilla solo procesa el icono. Una instancia limpia muestra el diseño correcto con un zoom del 100 %, por lo que el error se cerró por estar fuera de ámbito. (SITES-26910)
* Crear temas de página ya no oculta el estado de enfoque. Los estilos acuático y desierto representan un resaltado consistente en la ficha **Básico** y en las fichas adyacentes durante la navegación mediante el teclado. Este cambio restaura la retroalimentación de enfoque predecible y perceptible para los usuarios con baja visión. (SITES-26907)



#### Interfaz de usuario de administración{#sites-adminui-6524}

Los usuarios del lector de pantalla no recibieron ayuda de navegación en la cuadrícula **Modelo del sistema de catálogo**. JAWS solo anunció la posición de la celda y luego se quedó en silencio. La versión añade directrices y funciones accesibles, lo que permite a JAWS leer el contexto de la lista, el elemento seleccionado y los controles de flecha/espacio necesarios. (SITES-30661)

#### IU clásica{#sites-classicui-6524}

Las casillas de verificación de la IU clásica perdieron sus etiquetas y mostraron opciones en blanco. Los cuadros de diálogo también mostraban HTML codificados como `<br>`. La actualización restaura las etiquetas de las casillas de verificación y descodifica el marcado, de modo que los cuadros de diálogo se leen correctamente. (SITES-31822)

<!--
#### [!DNL Content Fragments]{#sites-contentfragments-6524}
-->

#### [!DNL Content Fragments]: administración{#sites-admin-6524}

Los paréntesis en el nombre de un fragmento de contenido provocaban que el panel Referencias informara de un uso incorrecto. Los autores vieron 0 incluso cuando otros fragmentos hacían referencia a él. La corrección corrige el análisis de rutas para &quot;(&quot; y &quot;)&quot; y muestra el recuento y las entradas adecuados que no sean cero. (SITES-35078)


#### [!DNL Content Fragments]: editor de fragmentos{#sites-fragments-editor-6524}

* Error de cancelación de publicación para fragmentos de contenido cuya ruta DAM contenía paréntesis. El asistente Administrar publicación reescribió &quot;(&quot; y &quot;)&quot; y rompió la ruta del recurso. La corrección conserva los caracteres y resuelve el elemento correcto, por lo que la acción de cancelar la publicación finaliza. (SITES-35077)
* Al editar un fragmento de contenido y volver a la lista de Assets, se ocultaba el fragmento o toda la carpeta. La lista no se pudo actualizar después de cerrar el editor. La corrección ahora actualiza la lista de forma fiable y mantiene visible el fragmento editado sin una recarga dura. (SITES-35374)

* El Editor de fragmentos de contenido no pudo abrir el Selector de recursos de Polaris porque se eliminaron los ámbitos de IMS necesarios. La corrección restaura los ámbitos mínimos y restablece la conexión de entrega. La exploración y selección de recursos funcionan de nuevo, sin errores HTTP 500. (SITES-35837)

#### [!DNL Content Fragments]: API de GraphQL {#sites-graphql-api-6524}

Después de cada implementación, las consultas de GraphQL válidas empezaron a devolver `GraphQL_QueryValidationError`. El extremo mantuvo un esquema obsoleto hasta que los equipos vaciaron las cachés o reiniciaron. La corrección actualiza el esquema de GraphQL y el registro de consultas persistentes durante la implementación y restaura inmediatamente las respuestas normales. (SITES-34301)

<!--
#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6524}


#### [!DNL Content Fragments] - REST API{#sites-restapi-6524}


#### Component Console{#sites-component-console-6524}


#### Core Backend{#sites-core-backend-6524}


#### Core Components{#sites-core-components-6524}


#### Campaign integration{#sites-campaign-integration-6524}
-->


#### ContentHub {#sites-contenthub-6524}

ContextHub ya no inserta una segunda copia de jQuery en las páginas de publicación. La biblioteca de cliente del motor de segmentos descarta la dependencia cq.shared que extraía jQuery 1.12.4, de modo que los sitios cargan un jQuery coherente y el código front-end funciona de forma fiable. (SITES-30404)

#### Fragmentos de experiencias{#sites-experiencefragments-6524}

* Los fragmentos de experiencias ahora localizan la advertencia que se muestra cuando no existe ninguna configuración de Adobe Target. El mensaje se muestra en la configuración regional del autor en lugar de en inglés, por lo que los pasos de exportación y activación se leen correctamente para los equipos globales. (SITES-11868)
* La publicación de una variación de Fragmento de experiencia ahora muestra un mensaje de error localizado cuando ningún servicio de nube se adjunta a la variación. El mensaje aparece en la interfaz de usuario en el idioma del usuario en lugar de en una cadena solo en inglés. (SITES-20293)
* La exportación de un fragmento de experiencia a Target se bloqueó con `Attempt to modify attribute at illegal index: -1`. La instrumentación de Web Vitals entró en conflicto con el exportador y la administración de atributos dañados. La corrección endurece el procesamiento de atributos y elimina ese conflicto. Las exportaciones se realizan correctamente y el fragmento se procesa en Target. (SITES-31891)

* Las propiedades del fragmento de experiencia ahora localizan la pestaña **Referencias**. Las etiquetas y los encabezados de columna como &quot;Página&quot;, &quot;Ruta de la página&quot; y &quot;Título de la variación&quot; se muestran en el idioma del autor. Este cambio elimina las cadenas solo en inglés y mantiene la coherencia de la vista de propiedades para los equipos globales. (SITES-11203)
* Ahora, **Variaciones** > **Crear flujo de trabajo** muestra texto de traducción completo. El cuadro de diálogo gestiona las cadenas de configuración regional largas ajustando y ajustando el tamaño del contenido correctamente, eliminando las etiquetas recortadas o cortadas. (SITES-19304)
* Las propiedades del fragmento de experiencia ahora localizan las etiquetas de estado de los medios sociales. Los autores ven valores de estado como Publicado y No publicado en el idioma seleccionado en todas las configuraciones regionales. Este cambio quita las cadenas de sólo inglés que causaron confusión durante la revisión. (SITES-20014)

<!--
#### Foundation Components (Legacy){#sites-foundation-components-legacy-6524}
-->

#### Lanzamientos{#sites-launches-6524}

* Al eliminar un Launch muy grande, se bloqueó el repositorio. El trabajo puso en cola demasiadas eliminaciones y dejó sin contenido otras solicitudes. La corrección ahora agrupa la eliminación y produce entre fragmentos, por lo que la limpieza se completa mientras el sistema sigue respondiendo. (SITES-32004)

* Configuración de Launch > Propiedades muestra los desplegables de Compañía y Propiedad en funcionamiento. **Guardar** y **Cerrar** respetan los campos completados y la validación del título ya no déclencheur errores en la compañía o la propiedad. (CQ-4359853)
* Las comprobaciones necesarias en la configuración de IMS se ejecutan al actualizar, no solo al crear. Los valores vacíos de campos como ID de cliente o Secreto de cliente muestran un error y detienen el guardado hasta que se introduzca un valor válido, lo que impide la reutilización del valor anterior. (CQ-4359938)
* La creación de Launch muestra la validación traducida y las cadenas de error. Ya no aparecen mensajes exclusivos en inglés para errores de creación y páginas de origen que faltan. Los autores ven comentarios claros y correctos respecto a la configuración regional durante la configuración de Launch. (SITES-13085)
* La promoción de lanzamiento actualiza las propiedades de página `jcr:title`, `jcr:description` y `cq:redirectTarget` en la página de origen. El cambio elimina las exclusiones de propiedades en la configuración de despliegue de MSM y la lógica de flujo de trabajo. Las campañas, las traducciones y la optimización de los motores de búsqueda mantienen títulos, descripciones y redirecciones coherentes. (SITES-34509)
* La acción de Launch ignoró el ámbito e incluyó páginas que compartían el mismo elemento principal que la sección de destino. La actualización fuerza los límites del subárbol y promociona solo la página elegida y sus descendientes. Las páginas no relacionadas conservan el contenido existente. (SITES-34344)
* Se ha corregido la promoción automática de Launch anidada que se detenía en Autor y omitía el nivel de publicación. La promoción automática de un lanzamiento secundario publica las páginas actualizadas en los editores configurados y completa el lanzamiento completo según lo programado. (SITES-30420)

<!--
#### Link Checker{#sites-link-checker-6524}
-->

#### MSM: Live Copies{#sites-msm-live-copies-6524}

* Un despliegue de nivel de carpeta no pudo crear Live Copies para los fragmentos de experiencias en esa carpeta. Los despliegues individuales funcionaron, lo que interrumpió los flujos de trabajo masivos. El cambio alinea el despliegue de carpetas con el comportamiento de la página y propaga las relaciones y referencias en el subárbol. (SITES-35161)
* Después de eliminar un componente en una Live Copy, **Habilitar herencia** se interrumpió con un error de JavaScript y el componente permaneció ausente hasta un segundo intento. La actualización corrige la recarga posterior a la eliminación para que lleve los parámetros correctos y reemplaza la llamada de alerta obsoleta. El cuadro de diálogo se abre sin problemas y la herencia se restaura en el primer intento. (SITES-31387)
* El Asistente para despliegue aceptó **Más tarde** sin fecha. Los autores avanzaron y crearon un despliegue sin una programación. La actualización exige la selección de fechas y muestra un mensaje claro. La acción **Continuar** permanece deshabilitada hasta que exista una fecha. (SITES-31374)


#### Editor de páginas{#sites-pageeditor-6524}

* Al abrir el árbol de contenido en una página con un contenedor de Personalization, se ha devuelto un panel vacío y un error de referencia nula en la consola. Los autores no pudieron elegir ni configurar componentes. La actualización elimina el error y vuelve a habilitar el árbol y las interacciones de componentes. (SITES-34336)
* Conmutación de modo interrumpido de AEM 6.5 SP23 en el editor de páginas. Al hacer clic en **Diseño**, **Desarrollador** o **Segmentación**, el editor se quedó atascado en el modo **Editar** y se lanzó una consola `TypeError`. La actualización restaura los cambios del modo de la barra de herramientas y borra el error. (SITES-34536)
* El editor de páginas saltó del punto de inserción cuando los autores agregaron componentes en contenedores largos. La actualización ajusta la temporización de la superposición y la gestión del desplazamiento. La vista ocupa su lugar y el nuevo componente permanece a la vista y listo para configurarse. (SITES-32621)
* Las etiquetas de etiquetas personalizadas fallaban en el Editor de páginas y la IU siempre mostraba &quot;Etiquetas&quot;. El predicado ahora evalúa `fieldLabel` primero y `labelText` segundo y, a continuación, aplica el valor predeterminado. Los autores ven la etiqueta que establecen. (SITES-32278)
* Al cancelar el filtro Ubicación en Sites, el icono OmniSearch se desalineó y se superpuso con el texto del marcador de posición. El icono se volvió impracticable. La corrección realinea el déclencheur y restaura el área de visitas, de modo que tanto el ratón como el teclado pueden buscar. (SITES-30946)
* Al elegir Desarrollador, la página quedó en mal estado y se bloqueó la creación en esa página. El panel desapareció y la interfaz de usuario dejó de responder. La actualización repara la lógica de alternancia de modo y la administración de caché, manteniendo la página editable y mostrando los datos del desarrollador inmediatamente. (SITES-30922)
* Al hacer clic en **Borrar** en **Insertar nuevo componente**, no se quitó la consulta de búsqueda y se dejó la lista filtrada a un solo elemento (Acordeón). La corrección restablece la consulta y actualiza la lista. Todos los componentes permitidos aparecen de nuevo. (SITES-30921)

<!--
#### Replication{#sites-replication-6524}
-->

#### Editor de texto enriquecido{#sites-rte-6524}

* En pantalla completa, el editor de texto enriquecido ocultaba el resultado de la revisión ortográfica detrás del cuadro de diálogo cuando no existían errores. La actualización trae el panel de resultados al frente y mantiene visibles los mensajes y las sugerencias. Los autores revisan y aceptan correcciones sin salir de pantalla completa. (SITES-32366)
* Las imágenes del editor de texto enriquecido ahora respetan la alineación seleccionada. Los autores establecen left, center o right en el cuadro de diálogo de imagen y el editor aplica esa opción de forma coherente en la salida. El cambio también estabiliza el cuadro de diálogo Texto alternativo para que el texto alternativo y la alineación se guarden y persistan durante las reediciones. (SITES-30634)

#### Editor universal {#sites-universal-editor-6524}

La configuración del controlador de autenticación de token de consulta confundió a los usuarios porque las etiquetas no coincidían con los campos. La interfaz de usuario extrajo texto de la ruta y mostró los nombres incorrectos. La corrección restaura etiquetas claras y precisas para la clasificación del servicio y las opciones de token de consulta. (SITES-31305)


### [!DNL Assets]{#assets-6524}


#### [!DNL Dynamic Media]{#assets-dm-6524}

* La opción **Seleccionar miniatura** para vídeos ahora se comporta correctamente en AEM Assets: Dynamic Media. El clic abre el cuadro de diálogo y permite seleccionar una miniatura de Assets, lo que elimina el comportamiento de clic muerto anterior y la limitación de solo extracción de fotogramas de vídeo. (ASSETS-58926)


### [!DNL Forms]{#forms-6524}

<!--
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, December 4, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

#### Forms Designer

* Los usuarios tuvieron problemas con los hipervínculos en los que no se podía hacer clic en casos de prueba específicos, lo que afectó a su capacidad para navegar y verificar los vínculos dentro de la aplicación. (LC-3923505)
* Los usuarios experimentaron problemas de accesibilidad con los archivos PDF generados mediante AEM Forms Designer 6.5.23 para idiomas no latinos. Las etiquetas de ruta no se colocaban dentro de un contenedor de artefactos, lo que provocaba errores en las comprobaciones de PAC y del lector de pantalla. (LC-3923295)
* Los usuarios experimentaron hipervínculos rotos en los cuadros de texto de Formato de documento portátil (PDF) después de aplicar parches de la versión 6.5.21 a la 6.5.23 mediante el Servicio de salida. (LC-3923290)
* Los usuarios experimentaron problemas de accesibilidad con los formularios de documento de registro (DoR). Cuando los campos de entrada están vacíos, los lectores de pantalla solo leen los subtítulos de los campos y no los valores, lo que dificulta a los usuarios con discapacidad la navegación eficaz por los formularios. (LC-3923234)
* Los usuarios se enfrentaban a problemas de accesibilidad en DoR PDF forms, donde NVDA leía incorrectamente &quot;no disponible&quot; para casillas de verificación, botones de opción y campos de texto, a menudo repitiendo el mensaje y creando confusión para los usuarios del lector de pantalla. (LC-3923201)
* Los usuarios experimentaban una discrepancia en el orden de tabulación en el XDP al añadir nuevos campos. El orden de tabulación existente cambió inesperadamente y afecta a la navegación del formulario. (LC-3923183, LC-3922630)
* Los usuarios han experimentado problemas con el procesamiento de HTML. Al utilizar el evento `docReady`, no se almacenó en déclencheur correctamente en HTML, lo que provocó que los scripts no se ejecutaran según lo esperado. (LC-3923118)
* Los usuarios han experimentado problemas con los scripts de procesamiento de PDF que no funcionaban en el entorno de producción de AEM Forms Cloud. (LC-3923082 )
* Los usuarios han experimentado problemas con campos flotantes en los formularios. Cuando se utilizan diferentes archivos de datos, los campos flotantes se representan correctamente con un archivo pero no con el otro, a pesar de diferencias menores no relacionadas con los campos. (LC-3923056)
* Los usuarios veían una página maestra en español en blanco cuando solo se seleccionaba contenido en inglés en un XDP (paquete de datos XML) con varias páginas maestras. (LC-3923009)
* Los usuarios observaron información obsoleta del año de copyright en el Designer de AEM. Esto ocurría en el cuadro emergente al inicio, en la sección &quot;Acerca de&quot; y en la sección &quot;Avisos legales&quot;, que muestra &quot;2003-2024&quot; en lugar de &quot;2003-2025&quot;. (LC-3923005)
* Los usuarios encontraban una página de PDF en blanco al utilizar la paginación en AEM Forms Designer. El problema se producía al seleccionar &quot;Parte superior de la siguiente página/Parte superior de la página&quot; para WireAdviceHeader, interrumpiendo el diseño de las iteraciones de datos. (LC-3922997, LC-3922830)
* Los usuarios experimentaron un problema en el que el valor filedigest de la Definición de esquema (XSD) del lenguaje de marcado extensible (XML) no persistió en la versión de 64 bits de AEM Forms Designer. (LC-3922924)
* Los usuarios experimentaban un formato de hipervínculo inestable en AEM Designer 6.5.19, donde los hipervínculos dentro de un cuadro de texto adoptaban incorrectamente estilos del texto adyacente, como el formato del primer carácter. (LC-3922376)
* Los usuarios han experimentado problemas al procesar formularios HTML mediante el procesamiento móvil en MAC con AEM Forms OSGI v6.5.22. (LC-3923058)
* Los usuarios experimentaban errores de &quot;objeto de ruta no etiquetado&quot; en los archivos de formato de documento portátil (PDF) al utilizar campos con borde o en segundo plano en plantillas XDP creadas con Designer 6.5.23 y analizadas con PAC 2024. (LC-3923013)
* Los usuarios experimentaron un error con el color de fondo del encabezado &quot;Dati Richiedente&quot; en el componente de aplicación portátil (PAC), al recibir el mensaje &quot;objeto de ruta no etiquetado&quot;. (LC-3922912)
* Los usuarios experimentaron un problema en el cual plantillas específicas sustituían la fuente deseada por una fuente condensada. (LC-3922330)

#### Formularios adaptables

* Los usuarios veían que faltaban opciones en el Editor de reglas. Cuando los autores escribían reglas sobre las entradas numéricas, las opciones de Consulta, UTM y Detalles del explorador no estaban disponibles. (FORMS-21660)
* Los usuarios experimentaban bloqueos de aplicaciones al interactuar con OdataResponse debido a una excepción de puntero nulo. (FORMS-20344)
* Los usuarios experimentaban problemas al crear reglas para mostrar un panel y establecer el enfoque en un elemento dentro de él. La regla setFocus se ejecutaba antes de la actualización de la visibilidad, lo que provocaba que la acción de enfoque fallara. (FORMS-19563)
* Los usuarios han experimentado problemas con la selección de componentes en AEM Forms Author. Al desplazarse entre pestañas en el modo de edición, algunos contenedores se volvían inseleccionables, lo que impedía una fácil identificación e interacción. (FORMS-18525)
* Los usuarios experimentaron un error de &quot;URL no válida&quot; al intentar realizar anotaciones en recursos en AEM 6.5.22. (NPR-42684)

### Foundation {#foundation-6524}


#### Apache Felix {#foundation-apachefelix-6524}

Se ha actualizado el paquete de la consola web Felix para incluir FELIX-6747. Este parche corrige la gestión de respuestas que anteriormente rompía el procesamiento y la autenticación de páginas en la consola web de OSGi. La consola se carga de forma coherente y ya no genera entradas IllegalStateException en los registros. (NPR-42730)

<!--
#### Campaign{#foundation-campaign-6524}

#### Cloud Services{#foundation-cloudservices-6524}

#### Communities {#foundation-communities-6524}

#### Content distribution{#foundation-content-distribution-6524}

#### CRX {#foundation-crx-6524}
-->

#### Granite{#foundation-granite-6524}

* Las cadenas sin procesar o de sólo inglés ya no aparecen en el cuadro de diálogo **Quitar control de acceso**. El cuadro de diálogo presenta contenido totalmente localizado en todos los idiomas compatibles para una accesibilidad coherente. (GRANITE-48479)
* El icono Ayuda ahora muestra una etiqueta concisa a las tecnologías de asistencia. JAWS lee &quot;Botón de ayuda&quot; y ya no agrega palabras &quot;menú&quot; superfluas. Esta actualización incorpora el control en la conformidad con WCAG 4.1.2 y simplifica el uso del teclado y del lector de pantalla. (GRANITE-55360)
* Restaure la fábrica del motor de scripts HTL después de eliminar un bucle de dependencia en los servicios OSGi. Los entornos se inician sin problemas, el procesamiento HTL funciona en todos los pods de creación y los administradores ya no encuentran errores de inicio ni servicios de scripts que falten. (GRANITE-58276)

* El cuadro de búsqueda de encabezado ya no superpone el icono de lupa en el texto del marcador de posición. El marcador de posición se muestra con el relleno adecuado y permanece totalmente legible en los exploradores. (GRANITE-54391)
* Los autores ven etiquetas legibles en los campos autocompletados en lugar de valores sin procesar en el cuadro de diálogo. La implementación mantiene el valor persistente en JCR y mejora la claridad para configuraciones de selección única y múltiple que generan opciones de forma dinámica. (GRANITE-57615)
* El modo de edición permanece funcional cuando htmlLibraryManager.debug se establece en true. El cambio restaura la resolución y carga adecuada de clientlib, lo que permite a los desarrolladores utilizar las herramientas de depuración del Administrador de bibliotecas de HTML durante la creación. (GRANITE-58002)
* La página de edición del agente de replicación ya no genera un error de JavaScript en la IU clásica. La página se abre, muestra todas las pestañas y guarda la configuración del agente sin errores de consola. (GRANITE-58302)
* Se ha corregido la agregación estado-estado en Información general del sistema. La vista ahora se actualiza después de que se ejecuten las comprobaciones individuales y muestra los recuentos correctos. Los operadores ven &quot;OK&quot; cuando se superan las comprobaciones de seguridad y mantenimiento, en lugar de un titular incorrecto de &quot;2 errores&quot;. (GRANITE-61482)
* Se detuvo la ejecución de `CodeUpgradeTasks` durante las actualizaciones de AEM 6.5 LTS (Long Term Support). La actualización ahora continúa sin cambios ni reconfiguraciones del repositorio activados por tareas. Esta corrección reduce el riesgo de actualización y evita un tiempo de inactividad evitable. (GRANITE-61486)
* En los cuadros de diálogo de creación, los campos obligatorios ahora muestran un único error de validación preciso. El mensaje utiliza la etiqueta propia del campo cuando está presente y vuelve a un indicador genérico cuando no existe ninguna etiqueta. Ya no aparecen los mensajes duplicados y no coincidentes entre los campos. (GRANITE-59531)
* El cuadro de diálogo del asistente para la creación de páginas ahora vuelve a validar los campos obligatorios en cada interacción, incluidos los cambios de pestaña y las ediciones de varios campos. El botón **Crear** permanece deshabilitado hasta que los autores completen todas las entradas necesarias y el asistente muestra errores en línea para los valores que faltan. (GRANITE-58826)

#### Integraciones{#foundation-integrations-6524}

La publicación de actividades de AEM Target ya no falla cuando los autores establecen las fechas de inicio y finalización. La integración envía marcas de tiempo compatibles con los estándares que incluyen la zona horaria, de modo que Target procesa la carga útil de la actividad y completa la sincronización según lo esperado. (CQ-4360733)

<!--
#### Jetty{#foundation-jetty-6524}
-->

#### Localización{#foundation-localization-6524}

* La localización en zh-CN elimina una frase ambigua del estado de recopilación de referencias que se muestra durante las operaciones de recursos como Mover. La interfaz de usuario ahora muestra `正在获取对 [[0]] 项的引用`, lo que proporciona un significado preciso y una terminología coherente. (CQ-4354648)
* La creación de una colección inteligente ya no traduce palabras clave de búsqueda guardada al actualizar. Los autores que introducen términos en inglés ven que se conservan esos mismos términos y la colección sigue arrojando resultados coherentes. (NPR-43158)
* Se ha corregido el texto de información de objeto truncado en el panel Imagen. La descripción &quot;Mostrar pie de ilustración como elemento emergente&quot; se representa completamente en todas las configuraciones regionales admitidas, lo que mejora la guía para los autores que no están en inglés. (SITES-10490)
* La vista de columna de administración de sitios truncó las etiquetas localizadas en francés y español. &quot;Hora de finalización&quot; y &quot;Hora de desactivación&quot; aparecieron truncadas y no mostraron información sobre herramientas. Adobe corrigió las traducciones y restauró la información del objeto al pasar el ratón por encima, por lo que las etiquetas se leyeron en su totalidad. (SITES-31318)
* El cuadro de diálogo **Mover** de Sites mostraba claves i18n sin procesar en lugar de etiquetas legibles. Elementos como &quot;Páginas de referencia&quot;, &quot;Creado en&quot;, &quot;Creado por&quot; y &quot;Ruta&quot; parecían confusos. La corrección enlaza el cuadro de diálogo con los diccionarios correctos y proporciona traducciones, con una reserva en inglés. (SITES-30881)

<!--
#### Oak {#foundation-oak-6524}
-->

#### Plataforma{#foundation-platform-6524}

* Los errores de validación ahora muestran un texto claro y descriptivo en lugar de solo un icono. Los lectores de pantalla anuncian el mensaje automáticamente cuando aparece, por lo que los usuarios no necesitan navegar a un icono para saber qué ha fallado. (CQ-4359152)


* Las etiquetas de desplazamiento en la barra de navegación ya no permanecen en la pantalla después de que el cursor se desplace fuera del control. La interfaz de usuario oculta inmediatamente estas informaciones de herramientas al desenfocar o al alejar el ratón, lo que evita el desorden visual y los clics erróneos. (CQ-4360030)
* En Sites, las acciones de la barra de herramientas dejan de crear una segunda ventana emergente cuando se repiten los clics. El segundo clic cierra la ventana emergente existente y deja solo una instancia visible, lo que elimina la superposición y la distracción. (CQ-4360038)
* El obsoleto texto de copyright de 2024 ya no aparece. La página Inicio de sesión y el programa emergente **Ayuda** > **Acerca de AEM** 2025 y AEM leen el año mediante programación para evitar ediciones manuales. (CQ-4360042)
* Al hacer clic en una información de objeto en la barra de encabezado de AEM, ya no se déclencheur la acción subyacente. Los elementos emergentes solo se abren cuando los usuarios hacen clic en el botón real, lo que evita cuadros de diálogo accidentales al interactuar con texto de información del objeto. (CQ-4360105)
* La renovación del año ya no deja texto de copyright obsoleto. La pantalla Inicio de sesión y el cuadro de diálogo **Ayuda** > **Acerca de AEM** derivan el año del reloj del sistema y representan el valor actualizado cada vez que se carga la interfaz de usuario. (CQ-4360173)
* Las ventanas emergentes de la barra de encabezado ahora se alternan correctamente. Al hacer clic en la misma acción (por ejemplo, **Buscar** o **Filtro**), se cerrará la ventana emergente de apertura en lugar de abrir otra superposición. El cambio evita las ventanas emergentes apiladas y devuelve el enfoque al control de encabezado. (NPR-42891)
* La vista de calendario Proyectos y Bandeja de entrada se representa correctamente. Al cambiar de vista, la página ya no queda vacía; el calendario se carga y muestra los elementos programados. (NPR-42968)

<!--
#### Security{#foundation-security-6524}
-->

#### Sling{#foundation-sling-6524}

* Se ha corregido un error inesperado de compilación de JSP con el paquete `org.apache.sling.scripting.jsp:2.6.0`. (SLING-12442)
* La plataforma actualiza el motor principal de Sling de 2.16.2 a 2.16.6. El nuevo motor endurece la validación de entrada y estabiliza el procesamiento de solicitudes bajo carga. (NPR-43105)

#### Editor SPA {#foundation-spa-editor-6524}

Al activar el servlet principal de Sling **Comprobar tipo de contenido**, se anularon las exportaciones de `.model.json` en AEM 6.5 SP21/22. Las solicitudes devolvían HTML o errores porque el exportador cambiaba el tipo de cadena media. La corrección emite un JSON con el tipo correcto desde el inicio, por lo que `.model.json` funciona en los entornos de creación y publicación. (SITES-32634)


#### Traducción{#foundation-translation-6524}

* Se ha añadido una operación de reindexación para el estado del proyecto de traducción. Los administradores pueden reconstruir el índice de respaldo cuando la vista de estado no esté sincronizada, restaurando los resultados y eliminando las advertencias de recorrido de Oak. La página se carga más rápido y muestra los estados de trabajo actuales. (NPR-42699)
* Se ha corregido una regresión en la que XLIFF importaba los archivos correctos, pero no cambiaba los archivos del diccionario JSON. Las importaciones ahora se dirigen a la ruta i18n correcta y conservan las traducciones, de modo que los viajes de ida y vuelta de localización se completan sin ediciones manuales. (NPR-42989)


* El XML de reglas de traducción ahora funciona según lo configurado. El marco de trabajo de traducción respeta las reglas de excepción y se aplica correctamente a los patrones `include` y `exclude` durante la creación del trabajo. Las solicitudes de traducción ya no envían contenido excluido. (NPR-42761)



#### Interfaz de usuario{#foundation-ui-6524}

* Se ha corregido una regresión de la interfaz de usuario que deshabilitaba las entradas en el cuadro de diálogo Licencia de Adobe Stock. El cuadro de diálogo ahora se comporta con normalidad, acepta texto en campos obligatorios y completa el flujo de licencias de recursos de Stock desde la vista Detalles del recurso. (NPR-42748)

* Se ha corregido la visibilidad de grupos en el entorno de creación. La consola de grupos ya no se detiene con unos 41 resultados y devuelve el conjunto completo de suscripciones para cada usuario. Esta corrección restaura el comportamiento coherente después de las correcciones acumulativas y mantiene la seguridad actual endurecida. (NPR-42749)


<!--
#### WCM{#foundation-wcm-6524}



#### Workflow{#foundation-workflow-6524}
-->




## Instalar [!DNL Experience Manager] 6.5.24.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.24.0 requiere [!DNL Experience Manager] 6.5. Consulte la [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas. <!-- UPDATE FOR EACH NEW RELEASE -->
* La descarga del Service Pack está disponible en [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip) de Adobe.
* En una implementación con MongoDB y varias instancias, instale [!DNL Experience Manager] 6.5.24.0 en una de las instancias de creación mediante el Administrador de paquetes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe no recomienda quitar ni desinstalar el paquete [!DNL Experience Manager] 6.5.24.0. Como tal, antes de instalar el paquete, debe crear una copia de seguridad de `crx-repository` en caso de que deba revertirla. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Instalar el Service Pack en [!DNL Experience Manager] 6.5{#install-service-pack}

1. Reinicie la instancia antes de la instalación si está en modo de actualización (cuando la instancia se haya actualizado desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de realizar la instalación, realice una instantánea o una copia de seguridad nueva de la instancia de [!DNL Experience Manager].

1. Descargue el Service Sack desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra el Administrador de paquetes y seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

1. Para actualizar el conector S3, detenga la instancia después de la instalación del Service Pack, sustituya el conector existente por un nuevo archivo binario, proporcionado en la carpeta de instalación, y reinicie la instancia. Consulte [Almacén de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo de la IU del administrador de paquetes a veces se cierra durante la instalación del Service Pack. Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete actualizador para asegurarse de que la instalación es correcta. Normalmente, este problema se produce en el explorador [!DNL Safari], pero puede ocurrir de forma intermitente en cualquier explorador.

**Instalación automática**

Existen dos métodos diferentes que puede utilizar para instalar [!DNL Experience Manager] 6.5.24.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en la carpeta `../crx-quickstart/install` cuando el servidor esté disponible en línea. El paquete se instala automáticamente.
* Use la API [HTTP del Administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que se instalen los paquetes anidados.

>[!NOTE]
>
>Experience Manager 6.5.24.0 no admite la instalación de Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar la instalación**

Para conocer las plataformas que están certificadas para funcionar con esta versión, consulte los [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.24.0)` en [!UICONTROL Productos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos los paquetes OSGi tienen el valor **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web: `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es de la versión 1.22.20 o posterior (utilice la consola web: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### Instalar Service Pack para [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Para obtener instrucciones para instalar el Service Pack en Experience Manager Forms, consulte [Instrucciones de instalación del Service Pack de Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La funcionalidad Formularios adaptables, disponible en [AEM 6.5 Inicio rápido](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), está diseñada únicamente para la exploración y la evaluación. Para su uso en producción, es esencial obtener una licencia válida para AEM Forms, ya que la funcionalidad Formularios adaptables requiere una licencia adecuada.

### Instalación del paquete de índice de GraphQL para fragmentos de contenido de Experience Manager{#install-aem-graphql-index-add-on-package}

Los clientes que usen GraphQL deben instalar el [fragmento de contenido de Experience Manager con el paquete de índice 1.1.1 de GraphQL](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Al hacerlo, puede añadir la definición de índice necesaria según las funciones que utilizan realmente.

Si no se instala este paquete, las consultas de GraphQL pueden ser lentas o dar error.

>[!NOTE]
>
>Instale este paquete solo una vez por instancia; no es necesario reinstalarlo con cada Service Pack.

### UberJar{#uber-jar}

UberJar para [!DNL Experience Manager] 6.5.24.0 está disponible en el [repositorio de Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.24/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para utilizar UberJar en un proyecto de Maven, consulte [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.24</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar y los demás artefactos relacionados están disponibles en el repositorio de Maven Central, en lugar del repositorio Maven público de Adobe (`repo.adobe.com`). Se ha cambiado el nombre del archivo principal de UberJar a `uber-jar-<version>.jar`. Por lo tanto, no hay `classifier`, con `apis` como valor, para la etiqueta `dependency`.



## Funciones en desuso y eliminadas{#removed-deprecated-features}

Consulte [Funciones obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md) para obtener una lista detallada de todas las funciones obsoletas o eliminadas de AEM 6.5.

### Compatibilidad con fragmentos de contenido en la API de REST de AEM Assets {#cf-support-assets-rest-api}

AEM 6.5 LTS SP2 proporciona OpenAPI modernas para la administración de modelos y fragmentos de contenido, por lo que los puntos finales de compatibilidad de fragmentos de contenido más antiguos en la API de REST de AEM Assets ya no se utilizan.

Adobe tiene la intención de mantener estos extremos más antiguos disponibles hasta que se produzca un anuncio de fin de vida útil. Adobe no planea más mejoras para los extremos obsoletos.

### Editor de SPA {#spa-editor}

[El editor de SPA](/help/sites-developing/spa-overview.md) ha quedado obsoleto para nuevos proyectos a partir de la versión 6.5.24 de AEM 6.5. El Editor SPA sigue siendo compatible con los proyectos existentes, pero no debe utilizarse para nuevos proyectos.

Los editores preferidos para administrar contenido sin encabezado en AEM ahora son:

* [El editor universal](/help/sites-developing/universal-editor/introduction.md) para la edición visual.
* [El editor de fragmentos de contenido](/help/sites-developing/universal-editor/introduction.md) para la edición de contenido sin encabezado basada en formularios.

## Problemas conocidos{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **Relacionado con Oak**
A partir del Service Pack 13, ha comenzado a aparecer el siguiente registro de errores que afecta a la caché de persistencia:

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  O bien

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  Para resolver esta excepción, haga lo siguiente:

   1. Eliminar las dos carpetas siguientes de `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. Instalar el Service Pack o reiniciar Experience Manager as a Cloud Service.
Las nuevas carpetas de `cache` y `diff-cache` se crean automáticamente y ya no experimentará una excepción relacionada con `mvstore` en `error.log`.

* Actualice las consultas de GraphQL que puedan haber usado un nombre de API personalizado para el modelo de contenido y utilizará el nombre predeterminado del modelo de contenido en su lugar.

* Una consulta de GraphQL puede emplear el índice `damAssetLucene`, en lugar del índice `fragments`. Esta acción podría provocar que las consultas de GraphQL fallen o tarden mucho en ejecutarse.

  Para corregir el problema, `damAssetLucene` debe estar configurado para incluir las dos propiedades siguientes en `/indexRules/dam:Asset/properties`:

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  Una vez modificada la definición del índice, se requiere una reindexación (`reindex` = `true`).

  Después de estos pasos, las consultas de GraphQL deberían funcionar más rápido.

* Al intentar mover, eliminar o publicar fragmentos de contenido, sitios o páginas, hay un problema cuando se recuperan las referencias de fragmentos de contenido. La consulta en segundo plano falla. Es decir, la funcionalidad no funciona.
Para garantizar el funcionamiento correcto, debe añadir las siguientes propiedades al nodo de definición de índice `/oak:index/damAssetLucene` (no se requiere la reindexación):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Si actualiza la instancia de [!DNL Experience Manager] de la versión 6.5.0-6.5.4 al Service Pack más reciente de Java™ 11, verá excepciones `RRD4JReporter` en el archivo `error.log`. Para detener las excepciones, reinicie la instancia de [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Los usuarios pueden cambiar el nombre de una carpeta en una jerarquía de [!DNL Assets] y publicar una carpeta anidada en [!DNL Brand Portal]. Sin embargo, el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Durante la instalación de [!DNL Experience Manager] 6.5.x.x se pueden mostrar los siguientes errores y mensajes de advertencia:
   * “Cuando la integración de Adobe Target se configura en [!DNL Experience Manager] mediante la API de Target Standard (autenticación IMS) y, a continuación, se exportan fragmentos de experiencias a Target, se crean tipos de ofertas incorrectos. En lugar de “Experience Fragment”/source “Adobe Experience Manager”, Target crea varias ofertas con el tipo “HTML”/source “Adobe Target Classic”.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en `granite/operations/maintenance`.
   * La validación del lado del servidor de formularios adaptables falla cuando se utilizan funciones de agregado como SUM, MAX y MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en `granite/operations/maintenance`.
   * La zona interactiva de una imagen interactiva de Dynamic Media no está visible al previsualizar el recurso a través del visor de banners a la venta.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]`: tiempo de espera agotado para completar el cambio de registro sin registrar.

* A partir de AEM 6.5.15, el motor Rhino JavaScript proporcionado por el paquete ```org.apache.servicemix.bundles.rhino``` presenta un nuevo comportamiento de hoisting. Los scripts que utilizan el modo estricto (```use strict;```) deben declarar sus variables correctas. De lo contrario, no se ejecutan y terminan generando un error de tiempo de ejecución.

* La instalación del contenido listo para usar relacionado con el etiquetado mediante un paquete de actualización oficial restablece la propiedad de idiomas del nodo `/content/cq:tags` a su valor predeterminado. Esta acción se aplica a los paquetes de servicio, los paquetes de servicio de seguridad, los paquetes de funciones ampliadas, los paquetes de funciones acumulativas, los parches, etc. Por lo tanto, es necesario añadirlo desde las propiedades antes de la instalación.

### Problema conocido de AEM Sites {#known-issues-aem-sites-6524}

Fragmentos de contenido: la previsualización falla debido a la protección DoS para un gran árbol de fragmentos. Consulte el [artículo de KB sobre las opciones de configuración predeterminadas del ejecutor de consultas de GraphQL](https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)

### Problemas conocidos de AEM Forms {#known-issues-aem-forms-6524}

* **FORMS-14521** Si un usuario intenta obtener una vista previa de un borrador de carta con datos XML guardados, se queda atascado en el estado `Loading` para algunas cartas específicas.
* **FORMS-16603** En la vista preliminar de la interfaz de usuario de Interactive Communications Agent, algunos valores calculados no se muestran correctamente.
* **FORMS-15681** Cuando la carta se ve en la Vista preliminar, el contenido cambia. Es decir, algunos espacios desaparecen y ciertas letras se reemplazan por `x`.
* **FORMS-15428**: Después de actualizar al paquete de servicio 20 de AEM Forms (6.5.20.0) con el complemento de Forms, las configuraciones que dependen del servicio de Adobe Analytics Cloud heredado mediante autenticación basada en credenciales dejan de funcionar. Este problema impedía que las reglas de análisis se ejecutaran de forma correcta.
* **FORMS-16557** En la vista preliminar de la interfaz de usuario de Interactive Communications Agent, el símbolo de moneda (como el signo de dólar $) se muestra de manera incoherente en todos los valores de campo. Aparece para valores de hasta 999, pero falta para valores de 1000 y superiores.
* **FORMS-16575** Las modificaciones realizadas en el XDP de los fragmentos de diseño anidados en una comunicación interactiva no se reflejarán en el editor de CI.
* **FORMS-21378**: cuando la validación del lado del servidor (SSV) está habilitada, es posible que se produzcan errores en los envíos de formularios. Si tiene este problema, póngase en contacto con el Soporte técnico de Adobe para obtener ayuda.

* **FORMS-23722** (faltan archivos adjuntos en Asignar tarea): cuando un formulario con un campo **Archivo adjunto** que utiliza bindref se envía a un flujo de trabajo de AEM que usa un paso **Asignar tarea**, los archivos adjuntos no aparecen cuando la tarea se abre desde la Bandeja de entrada. Los archivos se guardan correctamente en el repositorio, pero la interfaz de usuario del paso Asignar tarea no muestra los archivos adjuntos.

* **FORMS-23802** (las funciones personalizadas no se cargan cuando el formulario está en la página de Sites): las funciones personalizadas no funcionan en la vista previa ni en la publicación cuando el formulario adaptable está incrustado en una página de Sites y la versión de la biblioteca de componentes principales de aem-forms es inferior a 1.1.76. Puede ver un error como `InvalidFormContainerException: No form container found` en los registros. Para resolver este problema, [descargue e instale la revisión](/help/release-notes/aem-forms-hotfix.md) para AEM Forms SP24 (AddOn 6.0.1454).

#### Problemas conocidos con revisiones disponibles {#aem-forms-issues-with-hotfixes}

<!-- 
>[!NOTE]
>
>Avoid upgrading to Service Pack 6.5.24.0 for issues without an available hotfix. It may lead to unexpected errors. Upgrade to Service Pack 6.5.24.0 only after the required hotfixes are released. -->

Los siguientes problemas incluyen una revisión disponible para su descarga e instalación. Puede [descargar e instalar la revisión](/help/release-notes/aem-forms-hotfix.md) para resolver los siguientes problemas:

<!--* FORMS-23881 On AEM Forms JEE deployments set up using the 6.5.23.0 full installer, Output Service fails to process requests when a custom XCI file is supplied in the invocation. To resolve this issue, install the latest AEM 6.5.24.0 Forms Service Pack from the [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) portal.-->

* **FORMS-23789** (solo AEM Forms en JEE): Los usuarios experimentaron problemas con Log4j en AEM Forms en JEE SP24, lo que provocó interrupciones en el registro y la supervisión de los clientes empresariales. Para resolver este problema, [descargue e instale la revisión](/help/release-notes/aem-forms-hotfix.md) para AEM Forms en el paquete de servicio JEE 6.5.24.0.

* **FORMS-23802** Las funciones personalizadas no se cargan en la vista previa ni en la publicación cuando el formulario está en una página de Sites con una versión anterior de aem-forms-core-component (&lt;1.1.76). Para resolver este problema, instale la revisión [AEM Forms AddOn 6.0.1454](/help/release-notes/aem-forms-hotfix.md) para SP24.

* **FORMS-23789** (solo AEM Forms en JEE): Los usuarios experimentaron problemas con Log4j en AEM Forms en JEE SP24, lo que provocó interrupciones en el registro y la supervisión de los clientes empresariales. Para resolver este problema, [descargue e instale la revisión](/help/release-notes/aem-forms-hotfix.md) para AEM Forms en el paquete de servicio JEE 6.5.24.0.

* **FORMS-23802** Las funciones personalizadas no se cargan en la vista previa ni en la publicación cuando el formulario está en una página de Sites con una versión anterior de aem-forms-core-component (&lt;1.1.76). Para resolver este problema, instale la revisión [AEM Forms AddOn 6.0.1454](/help/release-notes/aem-forms-hotfix.md) para SP24.

* AEM Forms ahora incluye una actualización de la versión de Struts de la 2.5.33 a la 6.x para el componente de formularios. Esta actualización ofrece los cambios de Struts que se omitieron anteriormente y que no se incluyeron en SP24. La compatibilidad se añadió a través de una [revisión](/help/release-notes/aem-forms-hotfix.md) que puede descargar e instalar para añadir compatibilidad con la última versión de Struts.

* **FORMS-14926** Después de instalar AEM Forms JEE Service Pack 21 (6.5.21.0), si encuentra entradas duplicadas de Jars Geode `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` en la carpeta `<AEM_Forms_Installation>/lib/caching/lib`, realice los siguientes pasos para resolver el problema:

   1. Detenga los localizadores, si están en funcionamiento.
   2. Detenga el servidor de AEM.
   3. Ir a `<AEM_Forms_Installation>/lib/caching/lib`.
   4. Quite todos los archivos de parche de Geode, excepto `geode-*-1.15.1.2.jar`. Confirme que solo están presentes los Jars Geode con `version 1.15.1.2`.
   5. Abra el símbolo del sistema en modo de administrador.
   6. Instale el parche de Geode mediante el archivo `geode-*-1.15.1.2.jar`.

* **FORMS-15256** Cuando los usuarios actualizaron desde AEM 6.5 Forms Service Pack 18 o 19 a Service Pack 20 o 21, encontraron un error de compilación de JSP. Este error les impedía abrir o crear formularios adaptables. También causó problemas con otras interfaces de AEM. Estas interfaces incluían el Editor de páginas, la IU de AEM Forms, el Editor de flujos de trabajo y la IU de Información general del sistema.

  Si tiene un problema de este tipo, siga estos pasos para resolverlo:
   1. Vaya al directorio `/libs/fd/aemforms/install/` en CRXDE.
   2. Elimine el paquete con el nombre `com.adobe.granite.ui.commons-5.10.26.jar`.
   3. Reinicie el servidor de AEM.

* **FORMS-23703** Cuando la regla `contains` está configurada sin un valor predeterminado, se produce un error en la validación del lado del servidor para un formulario adaptable. Puede instalar la versión más reciente de [AEM Forms 6.5.24.0 Service Pack](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases) para solucionar el problema.

* Los conectores del modelo de datos de formulario **GRANITE-63681** pueden no autenticarse debido a que las palabras clave y el patrón regex requeridos no están permitidos de manera predeterminada. Para resolver el problema, descargue e instale la revisión desde el [vínculo](/help/release-notes/aem-forms-hotfix.md).

  <!--To resolve the issue, add the following via the Configuration Manager (`/system/console/configmgr`):

  * **Keywords:** `fdm-client-secret`, `oauth-client-secret`
  * **Regex:** `^\[/conf/[^/]+(/[^/]+)?/settings/dam/cfm/models/[^,\]]+(?:,/conf/[^/]+(/[^/]+)?/settings/dam/cfm/models/[^,\]]+)*\]$`

    >[!VIDEO](https://video.tv.adobe.com/v/3479697)-->

* La conversión de **FORMS-23979** HTML a PDF (PDFG) puede experimentar tiempos de espera intermitentes. Posteriormente se publicó una versión más reciente del complemento de Forms para SP24 que incluye la corrección. Si encuentra este problema, actualice su entorno al [último complemento de Forms publicado para 6.5.24.0](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases).

* **FORMS-23717** Después de actualizar a **AEM Forms6.5.24.0**, `server.log` y `error.log` se pueden inundar con mensajes WARN repetidos, como *Error al crear la fábrica del analizador seguro* o *No se admite el atributo Security*. Los registros pueden crecer en alrededor de **5-10 líneas por segundo** (cientos de MB por hora), lo que puede llenar el disco y bloquear el despliegue de producción.

Para reducir el volumen de registro, establezca el nivel de registro de `com.adobe.util.XMLSecurityUtil` en `ERROR` en la configuración del servidor de aplicaciones o a través del argumento de JVM `-Dlogging.level.com.adobe.util.XMLSecurityUtil=ERROR`. Esto solo oculta los mensajes y no corrige la causa subyacente.

* **FORMS-23875** En la búsqueda del modelo de datos de formulario, se muestra una etiqueta de HTML en la interfaz de usuario aunque no haya una entidad relevante. Para resolver el problema, descargue e instale la revisión desde [el vínculo](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bb-expressionmanager-pkg-10.0.48.zip).

## Paquetes de contenido y paquetes OSGi incluidos{#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en esta versión de [!DNL Experience Manager] 6.5 Service Pack:

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.24.0](/help/release-notes/assets/65240-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.24.0](/help/release-notes/assets/65240-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sitios web restringidos{#restricted-sites}

Estos sitios web solo están disponibles para los clientes. Si es cliente y necesita acceso, póngase en contacto con el administrador de cuentas de Adobe.

* [Descarga de producto en licensing.adobe.com](https://licensing.adobe.com/)
* [Contacte con el servicio de atención al cliente de Adobe](https://experienceleague.adobe.com/es/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página de productos](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html?lang=es)
>* Documentación de[[!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/es/docs/experience-manager-65)
>* [Suscripción a las actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html)

