---
title: Notas de la versión de Adobe Experience Manager 6.5 Service Pack
description: Notas de versión específicas de Service Pack 5 de Adobe Experience Manager 6.5.
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: cb48bba01b78a0724f3a07875f601367520b2a8e
workflow-type: tm+mt
source-wordcount: '4508'
ht-degree: 7%

---


# Notas de la versión de Adobe Experience Manager 6.5 Service Pack {#aem-service-pack-release-notes}

## Información de la versión {#release-information}

| Productos | Adobe Experience Manager 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.5.0 |
| Tipo | Versión de Service Pack |
| Fecha | 04 de junio de 2020 |
| Descargar URL | [Uso compartido](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.5.0)de paquetes, distribución [de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) |

## Novedades de Adobe Experience Manager 6.5.5.0 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.5.0 es una actualización importante que incluye nuevas funciones, mejoras clave solicitadas por los clientes y mejoras de rendimiento, estabilidad y seguridad, publicadas tras la disponibilidad general de la versión 6.5 en **abril de 2019**. Se puede instalar sobre Adobe Experience Manager 6.5.

Algunas funciones y mejoras clave introducidas en Adobe Experience Manager 6.5.5.0 incluyen:

* Personalice los nombres de columna que se muestran en la Bandeja de entrada de Adobe Experience Manager.

* Se ha mejorado la accesibilidad en varias áreas del Gestor de contenido web de Experience Manager (WCM), como el Editor de páginas, los componentes principales, RTE y la interfaz de usuario del administrador.

* Guardar un [!DNL Interactive Communication] borrador.

* Compatibilidad con formularios [!DNL Oracle WebLogic 12] de Experience Manager en JEE.

* Se ha mejorado la gestión de excepciones en el flujo de la interfaz [!DNL Adobe Experience Manager Assets] de usuario.

* Para obtener la URL de publicación para Dynamic Media Scene7, `getRemoteAssetPublishURL` se agrega un nuevo método a la `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` interfaz.

* [Mejoras](#assets-6550) de accesibilidad en [!DNL Adobe Experience Manager Assets] conformidad con las directrices de accesibilidad de contenido web (WCAG).

* Se ha eliminado la integración de Uso compartido de paquetes de Adobe Experience Manager.

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.22.3.

Para obtener una lista completa de las funciones, los elementos destacados clave y las funciones clave incluidas en el Service Pack 5 de Experience Manager 6.5, consulte [Novedades de Adobe Experience Manager 6.5 Service Pack 5](new-features-latest-service-pack.md) .

A continuación se muestra la lista de correcciones que se proporcionan en la versión [!DNL Experience Manager] 6.5.5.0.

### [!DNL Sites] {#sites-6550}

* Sitios de Experience Manager proporciona una opción para publicar o cancelar la publicación de una página desde su alias. La opción no funciona (NPR-33415).
* Cuando se elimina un contenedor de diseño de una plantilla que contiene varias plantillas, la plantilla no se representa correctamente (NPR-33347).
* Cuando una página Sitios de Experience Manager forma parte de un conjunto de contenido grande con varias Live Copies, la previsualización del historial de versiones de la página no se carga (NPR-33311).
* Al utilizar el comando Mover para cambiar el nombre de una página Sitios de Experience Manager, el título de la página no se actualiza (NPR-33264).
* Al mover páginas a través de la vista de columna, las columnas desaparecen (NPR-33216).
* Cuando el nombre de un componente local en una copia de idioma es idéntico al nombre de un componente en el modelo y el componente se despliega desde el plano, no `_msm_moved` se agrega el término al nombre del componente local (NPR-33208).
* El servlet Redireccionamiento de página anexa .html a una URL de sitios de Experience Manager donde ResourceType no está `cq:Page` (NPR-33176).
* Al pegar un subárbol, no hay opción de decidir si las subpáginas correspondientes se van a pegar o no (NPR-33149).
* El número de resultados en el uso activo de un componente está limitado al número 49 (NPR-33058).
* Cuando se basa un fragmento de contenido en un esquema y contiene un área de texto obligatoria o un campo de ruta, el fragmento de contenido no se guarda (NPR-33007).
* Al crear un componente personalizado con el componente de fragmento de experiencia predeterminado y utilizarlo en páginas de sitios de Experience Manager, Experience Manager no muestra referencias (uso) para el componente personalizado (NPR-32852).
* Al cambiar el nombre de una carpeta con un gran número de referencias, muchas referencias a la carpeta no se actualizan (NPR-32765).
* Cuando se activa la opción de edición de origen, esta opción queda disponible para las opciones de pantalla completa en línea, pero sigue faltando para el cuadro de diálogo de edición y las opciones de pantalla completa del editor de texto enriquecido (NPR-32763).
* Si tiene un campo múltiple y contiene un campo requerido (como un menú desplegable o un campo de ruta) en las propiedades de página de un modelo, cuando se despliega una página que contiene un campo múltiple de este tipo, las propiedades de página de la Live Copy no se guardan (NPR-32751).
* Los lectores de pantalla no pueden utilizar la estructura de encabezados para navegar por una página. Además, la ficha Componentes tiene una etiqueta incorrecta (NPR-32648).
* Cuando se producen inicios de paginación, el selector de fragmentos de experiencia no carga todos los elementos (NPR-32605).
* Se revocan los permisos de autor para leer, modificar, crear y eliminar copias en directo. Cada autor tenía que proporcionar explícitamente permisos de lectura y modificación para mover páginas dentro de un modelo (NPR-32550).
* Los autores de contenido no pueden crear Launch para una página que tenga una integración con Adobe Analytics (NPR-32548).
* Cuando un usuario reanuda la herencia con la sincronización, la Live Copy de la página principal no se sincroniza con el modelo y muestra un estado incorrecto (NPR-32500).
* La página del editor Sitios de Experience Manager tarda más de 15 segundos en cargarse (NPR-32413).
* Algunos campos no muestran la opción Cancelar herencia (NPR-32362).
* Cuando se selecciona una ruta para un componente Fragmento de experiencia y se selecciona la casilla de verificación Abrir cuadro de diálogo de selección, no se navega a la ruta seleccionada en el Explorador de rutas (NPR-32308).
* Al actualizar desde Experience Manager 6.2 a Experience Manager 6.5, el componente Parsys de las plantillas estáticas no se muestra correctamente. La altura del componente Parsys se establece en 0 y los componentes que contiene no son visibles (NPR-33663).
* Cuando un usuario copia y pega un Contenedor de diseño en la misma página, los componentes de un Contenedor de diseño no se muestran (NPR-33648).
* La comprobación de estado del despachante muestra `Invalid cookie header` un mensaje de advertencia en los archivos de registro (NPR-33629).

### [!DNL Assets] {#assets-6550}

**Mejoras de accesibilidad en Recursos de Experience Manager**

* Ahora es posible enfocar el teclado en la lista de [!UICONTROL comentarios] y en la opción en la que se puede hacer clic para [!UICONTROL crear] comentarios de versión en [!UICONTROL Crear nueva versión] en el panel de recursos de la [!UICONTROL línea de tiempo] (NPR-33424).

* Ahora es posible acceder a la opción Configuración [!UICONTROL de] Vista de recursos y cambiar la configuración en el cuadro de diálogo Configuración [!UICONTROL de] Vista con las teclas del teclado (NPR-33420).

* La ventana emergente del cuadro de lista del cuadro combinado (en varios campos en diferentes páginas) ahora muestra las entradas como una lista de opciones que pueden anunciar los lectores de pantalla (NPR-33516).

* Los lectores de pantalla anuncian ahora la funcionalidad de ordenación de los encabezados que se pueden ordenar (en la vista de listas, en la vista de [!UICONTROL línea de tiempo] y en la página [!UICONTROL Administrar publicación] ) y los controles de clasificación de los encabezados de columna son accesibles mediante el teclado (NPR-32979).

* Los elementos en los que se puede hacer clic, como tarjetas de comentarios, actualizaciones de versiones, cuadros combinados e iconos de chevron de los menús, ahora se pueden enfocar e interactuar con un teclado (NPR-33514).

* La funcionalidad (o el propósito de acción) de los iconos de perspectivas (para uso, impresiones y clics) en la Vista [!UICONTROL de] perspectivas ahora son anunciados correctamente por los lectores de pantalla (NPR-33513).

* Los campos de formulario de sólo lectura (por ejemplo, campos desactivados en la ficha  Básico de [!UICONTROL Propiedades]del recurso) ahora se pueden enfocar mediante el teclado (NPR-33493, CQ-4273031).

* Las etiquetas de varios campos de entrada ahora son etiquetas permanentes (por lo tanto accesibles) y no solo etiquetas de marcador de posición, que desaparecían cuando se introducía texto (NPR-33475).

* Los diferentes niveles de encabezados (como títulos de página y encabezados de sección) ahora se perciben como encabezados con diferentes niveles para los usuarios de lectores de pantalla (NPR-33471).

* Ahora se puede acceder a los elementos interactivos de la interfaz de usuario, como los vínculos y las opciones (en las opciones de encabezado y zoom de la página de recursos, navegación por carpetas) mediante un teclado (NPR-33468, CQ-4271412).

* Los indicadores de progreso de [!UICONTROL Opciones], [!UICONTROL Alcance]y [!UICONTROL Flujos de trabajo] en la página [!UICONTROL Administrar publicación] ahora los lectores de pantalla los leen correctamente como indicadores de progreso, en lugar de fichas (NPR-33416).

* El color de los iconos de clasificación por estrellas (como en la sección [!UICONTROL Clasificación] de la ficha [!UICONTROL Avanzado] de [!UICONTROL Propiedades] del recurso o en la vista de la tarjeta) se cambia para que el contraste adecuado sea visible para los usuarios con visión limitada y sin percepción de color (NPR-33414).

* Ahora se puede acceder a la flecha hacia arriba situada junto al campo [!UICONTROL Comentario] en la página de detalles de recursos con las teclas del teclado (NPR-33397).

* Los lectores de pantalla anuncian ahora correctamente los estados expandidos y contraídos del cuadro de diálogo [!UICONTROL Etiquetas] en [!UICONTROL Propiedades] del recurso y navegación por el carril izquierdo (en la interfaz de usuario de los recursos) (NPR-33396).

* Los títulos de todas las páginas exploradas en [!DNL Adobe Experience Manager] Assets ahora son únicos (NPR-33343).

* Al navegar por la estructura de árbol, los lectores de pantalla anuncian ahora correctamente varios elementos del control de vista de árbol (NPR-33304).

* Ahora se puede acceder a diferentes versiones de los recursos de la página de detalles de la vista de la [!UICONTROL línea de tiempo] mediante las teclas del teclado (NPR-33283).

* Los nombres de las sugerencias de búsqueda que aparecen en el cuadro combinado Omnisearch ahora los anuncian los lectores de pantalla al utilizar la funcionalidad de búsqueda (NPR-33280).

* Los elementos activos e [!UICONTROL Ir al vínculo] en el carril  Referencias ahora son anunciados por los lectores de pantalla como elementos activos (NPR-33278).

* La información de estructura de tabla (como la fila 1, celda 1, tabla) del cuadro de diálogo [!UICONTROL Compartir vínculo] ya no la anuncian los lectores de pantalla cuando se abre el cuadro de diálogo (NPR-33268).

* El propósito de varios elementos de cuadro combinado (como el campo Ruta y la opción para abrir el cuadro de diálogo Selección en la ficha Básico de Propiedades del recurso) ahora lo anuncian correctamente los lectores de pantalla (NPR-33235).

* La información de que las filas de la tabla de vista de listas son seleccionables ahora se comunica a los usuarios del lector de pantalla cuando el teclado está en ellas. Esta información se anuncia cuando se sitúa el ratón sobre las filas (NPR-33234).

* Ahora los lectores de pantalla pueden acceder a las opciones (con [!UICONTROL x]) para eliminar cada una de las etiquetas seleccionadas debajo del campo [!UICONTROL Etiquetas] de la ficha [!UICONTROL Básico] de [!UICONTROL Propiedades] (NPR-33206).

* El selector de fechas del calendario ahora puede seleccionarse y procesarse mediante el teclado por usuarios de lectores de pantalla y usuarios de teclado con visión (NPR-33200).

* El cambio para cambiar entre la vista de lista y la vista de tarjetas ahora expone correctamente su funcionalidad (de ajustar vistas) al lector de pantalla (NPR-33069).

* Ahora se puede acceder al menú en el carril izquierdo. Los lectores de pantalla anuncian adecuadamente la funcionalidad y el propósito de ampliar el menú (NPR-33068).

* Los usuarios de lectores de pantalla ahora pueden acceder al cuadro de Lista y a muchos otros elementos de la interfaz de usuario, y los lectores de pantalla anuncian la siguiente información (NPR-33040):

   * si se requiere la introducción de datos por parte del usuario en un elemento antes del envío del formulario.
   * si un elemento no es editable.
   * si un widget está seleccionado o no.

* Ahora se puede acceder a la opción de abrir la barra lateral del filtro mediante el teclado (NPR-32842, CQ-4273018).

* Ahora se puede acceder al control de casilla de verificación en el encabezado de columna de la vista de lista y los lectores de pantalla anuncian el propósito de utilizar el control (NPR-32722, NPR-33005).

* Las etiquetas de los campos de horas (HH) y minutos (mm) en el selector de fechas del calendario son ahora etiquetas permanentes en lugar de etiquetas de marcador de posición, y no desaparecen cuando el usuario introduce texto en estos campos (NPR-32720).

* El texto de los vínculos de las notificaciones (que aparecen después de hacer clic en el icono de la campana) ahora se anuncia a los usuarios del lector de pantalla, que utilizan la ficha para acceder a cada vínculo (NPR-32645).

* [!UICONTROL Ahora se puede acceder mediante el teclado a las opciones Seleccionar], [!UICONTROL Descargar], [!UICONTROL Propiedades]y [!UICONTROL Más acciones] en tarjetas de recursos de la Vista  de perspectivas (NPR-32609).

* El contenido oculto visualmente (como el contenido de la barra de menús del encabezado en los resultados de búsqueda) ya no lo anuncian los lectores de pantalla cuando se accede mediante el teclado (NPR-32606).

* El propósito de las etiquetas de los controles para pasar a los meses siguiente y anterior en el selector de fechas del calendario ahora lo anuncian los lectores de pantalla (NPR-32604).

* Los iconos de clasificación por estrellas ahora se pueden enfocar y activar con las teclas del teclado (NPR-32513).

* Ahora se puede acceder a la funcionalidad para controlar el volumen de vídeo mediante tabuladores (para centrarse en el control deslizante del volumen) y teclas de flecha (para ajustar el volumen) en el teclado (NPR-32065).

* El propósito de los campos de entrada de límite inferior ([!UICONTROL Desde]) y límite superior ([!UICONTROL Hasta]) del filtro Tamaño de archivo ahora se anuncia para los usuarios de lectores de pantalla sin visión de futuro (NPR-32064).

* Ahora los lectores de pantalla pueden acceder al menú [!UICONTROL Idiomas] del formulario [!UICONTROL Crear y traducir] en modo de exploración (CQ-4293906).

* Ahora se puede acceder al panel [!UICONTROL Referencias] con las siguientes mejoras (NPR-33261, CQ-4293798):

   * En el modo de exploración, el enfoque del lector de pantalla ya no se desplaza a los campos de edición de varias líneas ocultos en las secciones Referencias del sitio, Referencias [!UICONTROL de]recursos, [!UICONTROL Copias]y Referencias [!UICONTROL de] formulario.

   * Los lectores de pantalla ahora anuncian la función de los elementos Referencias [!UICONTROL del] sitio y Copias de [!UICONTROL idioma] .

   * El enfoque de los lectores de pantalla en el modo de exploración cambia en una secuencia significativa a varios elementos.

* [!UICONTROL Ahora se puede acceder a la página Editor] de Esquemas de metadatos y a sus elementos mediante el teclado y son fáciles de leer en pantalla (CQ-4290962, CQ-4272953).

* El símbolo `X` para eliminar las etiquetas seleccionadas lo anuncian los lectores de pantalla junto con el número de etiquetas seleccionadas (CQ-4273017).

* Para evitar confusiones entre los usuarios sin visión de futuro que utilizan lectores de pantalla, los iconos y las imágenes decorativos ahora son ignorados por los lectores de pantalla (CQ-4272944).

**Problemas solucionados en Recursos de Experience Manager**

[!DNL Adobe Experience Manager] 6.5.5.0 Assets ofrece correcciones a los siguientes problemas:

* [!UICONTROL La opción Inicio] del cuadro de diálogo [!UICONTROL Crear flujo de trabajo] para los recursos de una colección está desactivada, lo que impide que se active el flujo de trabajo (NPR-32471).

* Cuando se utiliza la ventana emergente en cascada en esquemas de metadatos, al seleccionar y guardar una opción desplegable que contiene un apóstrofo (desde el menú desplegable secundario), la opción de apóstrofo seleccionada desaparece después de volver a abrir [!UICONTROL Propiedades] del recurso (NPR-32649).

* [!UICONTROL El trabajo] de sincronización de Asset Insights se detiene y falla si encuentra entradas no válidas (en el lado de Analytics) en lugar de moverse a la siguiente entrada (NPR-32674).

* El ámbito de navegación no funciona, ya que los sensores de movimiento están desactivados de forma predeterminada en los navegadores móviles en el visor panorámico (CQ-4272937).

* [!UICONTROL El asistente de configuración] de recursos conectados no funciona con el error 404 al instalar 6.5.3 en 6.5.1 (NPR-32730).

* Durante el proceso de reescritura XMP, todas las propiedades de metadatos de Área de nombres personalizadas cambian el prefijo de Área de nombres personalizado a ns2 en lugar del prefijo de Área de nombres configurado (NPR-32748).

* La carga diferida no se activa y solo se muestran 100 recursos al seleccionar para revisar las tareas de la bandeja de entrada de notificaciones (NPR-32750).

* `NullPointerException` se observa debido a la ausencia de preferencias de nodos en el perfil de usuario recién creado (SAML/SSO). Este error impide que los usuarios que inicien sesión recientemente utilicen [!DNL Adobe Experience Manager Stock] la integración (NPR-32777).

* Se observan advertencias transitorias en los registros al abrir una colección inteligente que contiene más de 10.000 recursos (NPR-32980).

* Los nombres de los recursos se cambian a minúsculas al mover recursos de una carpeta a otra al [!DNL Adobe Experience Manager] trabajar en el modo de ejecución de Dynamic Media Scene7 (NPR-32995).

* Un recurso buscado no se puede eliminar después de navegar a sus propiedades desde los resultados de búsqueda y luego volver a los resultados de búsqueda para eliminarlo (NPR-32998).

* [!UICONTROL La siguiente] opción permanece desactivada al seleccionar la carpeta de destino en la interfaz [!UICONTROL Mover recursos] (NPR-33356).

* [!UICONTROL La siguiente] opción no está activada al seleccionar el nodo principal (donde se puede ver una sola carpeta secundaria) y, a continuación, seleccionar la carpeta secundaria (NPR-33275).

* Los permisos de protección y desprotección están desactivados en Adobe Asset Link (AAL) para los usuarios con permisos de eliminación, aunque se hayan concedido otros permisos como leer, crear o modificar (NPR-33272).

* Las representaciones de recorte inteligente no están disponibles en el cuadro de diálogo de descarga de recursos (NPR-33167).

* Se observa una excepción en los registros al abrir el carril de representaciones para un PDF en una carpeta con perfil de recorte inteligente (CQ-4294201).

* Los ajustes preestablecidos de imagen no se publican si el modo [!UICONTROL de sincronización de medios] dinámicos está desactivado de forma predeterminada en Experience Manager con el modo de ejecución de Scene7 de Dynamic Media (CQ-4294200).

* El procesamiento de recursos mientras la carga masiva se queda atascada y la instancia de flujo de trabajo muestra instancias atascadas del recurso de actualización DAM (CQ-4293916).

* La creación de una configuración de Dynamic Media en Experience Manager funciona, pero en la interfaz de usuario no sucede nada al seleccionar Guardar (CQ-4292442).

* La Previsualización de recursos de vídeo F4V no funciona en la reproducción progresiva en Safari/Mac (CQ-4289844).

* La carpeta adicional se crea al recortar de forma inteligente un recurso que se encuentra dentro de una carpeta principal con caracteres de punto `.` en su nombre (CQ-4289337).

* La miniatura está dañada y la pancarta de procesamiento de vídeo no se muestra cuando se copia un vídeo (CQ-4284125).

* El visor de dimensiones muestra incorrectamente miniaturas vacías en Firefox para algunos modelos con vistas de cámara vacías (CQ-4283447).

* Los problemas de rendimiento corregidos en 6.5.5.0 son (CQ-4279206):

   * Se tarda demasiado en cargar archivos binarios grandes en los servidores de procesamiento de imágenes de Dynamic Media.

   * El tiempo de generación de miniaturas en Experience Manager aumenta debido a la arquitectura de Dynamic Media Scene7.

* Los problemas de migración a Dynamic Media Scene7 fallan en clientes con un gran número de recursos (CQ-4279206).

* El diseño del visor de vídeo 360 se interrumpe si `setVideo` se utiliza y el vídeo se desplaza hacia abajo en el uso `video= modifier` (CQ-4263201).

* Aparece un mensaje de error al instalar el paquete SDL de Experience Manager (NPR-33175).

### Plataforma {#platform-6550}

* No se llama al [!DNL Sling] filtro si la entrada del `sling:match` mapa se crea en `/etc/maps` (NPR-33362).
* Experience Manager se bloquea debido a un error de segmentación con [!DNL Apache Lucene] (NPR-32988).
* [!DNL Jackson] falta el paquete principal del archivo uberjar de Experience Manager (NPR-32848).
* CRXDE Lite no carga contenido para usuarios sin permiso de lectura en la `jcr:primaryType` propiedad de un nodo (NPR-32611).
* [!DNL Granite] el Planificador de tarea de mantenimiento se reinicia con demasiada frecuencia durante las implementaciones de Experience Manager (CQ-4294627).
* Cuando una consulta SQL se ejecuta durante mucho tiempo, por ejemplo, 7 horas, Experience Manager deja de responder (NPR-33044).

### Interfaz de usuario {#ui-6550}

* La selección de botones de radio no persiste en un campo múltiple (NPR-33309).
* El límite de carga diferida no funciona para la vista de lista (NPR-33124).
* La página de resultados de Omniture no muestra un mensaje si no hay coincidencias (NPR-32974).
* El filtro Omnisearch devuelve todas las coincidencias bajo `/content` el nodo que ignoran la ubicación seleccionada (NPR-32849).

### Integraciones {#integrations-6550}

* La caché interna se borra cuando se publica una página con un componente de Adobe Destinatario (NPR-33162).
* La integración con Adobe Destinatario no funciona en [!DNL Windows Internet Explorer] 11 (NPR-33111).
* Al configurar Adobe Destinatario, los campos [!UICONTROL Compañía] y Grupo [!UICONTROL de] informes no aparecen al seleccionar un origen de sistema de informes (NPR-32502).
* Al exportar [!DNL Experience Fragments] mediante Adobe I/O, los metadatos como el producto de origen no se exportan a Adobe Destinatario (NPR-32159).
* Los usuarios de IMS autorizados en el grupo de administración local de Experience Manager no pueden crear ni modificar configuraciones de IMS (NPR-33045).
* La página de configuraciones de Adobe Launch no muestra todos los registros (NPR-33011).
* Los usuarios del grupo de autores de contenido no pueden editar las propiedades de un componente de Adobe Destinatario debido a un error de JavaScript (NPR-32996).

### Proyectos de traducción {#translation-6550}

* Las etiquetas traducidas no se importan en Experience Manager desde servicios de traducción de terceros (NPR-33154).
* La página de configuración de traducción muestra un proveedor de traducción incorrecto al que se utilizó para la traducción (NPR-32971).
* Añadir una carpeta de fragmentos de experiencia en un proyecto de traducción existente crea un nuevo proyecto (NPR-32843).
* Se muestra un `NullPointerException` error en los registros de ejecución de un trabajo de traducción (NPR-32628).

### WCM {#wcm-6550}

* Editor de páginas: el Editor de [!DNL Sites] páginas no permite que los usuarios que utilizan solo el teclado pasen al contenido principal en lugar de desplazar el enfoque de la ficha a través de todas las opciones disponibles en el encabezado (CQ-4293883).
* Editor de páginas: los paneles que utilizan el componente Well e incluyen datos guardados no se muestran debido a las actualizaciones en [!DNL Chrome] y [!DNL Firefox] versiones (CQ-4292995).
* MSM: Al eliminar un componente de la página, no se elimina de la versión publicada de la página (CQ-4292360).

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* Si elimina un esquema de metadatos publicado de [!DNL Brand Portal] resulta en un error (CQ-4292063).
* Si un administrador configura [!DNL Experience Manager Assets] 6.5.4 con Brand Portal a través de Adobe Developer Console, el [!DNL Brand Portal] usuario no puede publicar el recurso de una carpeta de contribución de [!DNL Brand Portal] a [!DNL Experience Manager] (NPR-33046).
* Replicación de Duplicados de las carpetas principales que causan conflictos (NPR-33001).

### [!DNL Communities] {#communities-6550}

* No se puede eliminar una tarjeta en la consola de moderación mediante la opción de menú de edición rápida (NPR-33117).
* Se produce un error al acceder a la página Flujo [!UICONTROL de] Actividad (NPR-33146).
* Los grupos eliminados en la instancia de autor no se eliminan de todas las instancias de publicación (NPR-33199).
* Después de crear un nuevo grupo, los autores no se redirigen a la sección Grupo [!UICONTROL de] comunidad del [!DNL Internet Explorer] 11 (NPR-33205).
* El acceso a un mensaje en la Bandeja de entrada de Experience Manager no cambia el estado del mensaje a Leído (NPR-32764).
* Editar un [!DNL Communities] grupo y cambiar la imagen en miniatura no actualiza la imagen en miniatura del grupo (NPR-32599).
* Un usuario no puede enviar un correo electrónico a otro usuario de una comunidad (NPR-32598).
* Un blog enviado no se muestra hasta que el usuario actualiza la página (NPR-32391).
* Al crear una versión de las notificaciones y suscripciones de contenido generado por el usuario (UGC), se almacena un ID incorrecto de la página de origen (CQ-4279355, CQ-4289703).

### Flujo de trabajo {#workflow-6550}

* La opción [!UICONTROL Línea de tiempo] del carril izquierdo tarda más tiempo en cargarse de lo esperado (NPR-32851).
* Después de reiniciar una instancia de Experience Manager, el correo electrónico de la tarea de revisión de una colección incluye un vínculo de carga útil incorrecto (NPR-32774).

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>Experience Manager Service Pack no incluye correcciones para [!DNL Forms]. Estas se entregan mediante un paquete independiente de complementos de Forms. Asimismo, se ha publicado un instalador acumulativo que incluye correcciones para AEM Forms en JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

* Administración de correspondencia: El orden de los activos en una zona de destinatario se desplaza después de enviar una carta (NPR-33359, NPR-33153).
* Formularios adaptables: Cuando un usuario edita un formulario adaptable, la opción Flujo de trabajo [!UICONTROL de] Inicio disponible en el menú Información [!UICONTROL de] página no funciona (NPR-33004).
* Formularios adaptables: El usuario no puede guardar un formulario adaptable con más de un archivo adjunto (NPR-32997).
* Formularios adaptables: Si se cambia la presentación del panel en un formulario adaptable, se producirá un error (CQ-4293880).
* Formularios adaptables: Una nueva línea de una cadena en un diccionario de formularios adaptables agrega `&#xa;` caracteres al diccionario (NPR-33266).
* Accesibilidad de formularios adaptables: Cuando un usuario previsualización un formulario adaptable como formulario HTML, el campo Firma [!UICONTROL de] garabatos no puede mantener el enfoque de tabulación (NPR-33159).
* Accesibilidad de formularios adaptables: Los mensajes de error que se muestran al enviar un formulario adaptable no se vinculan a un `aria-describedBy` atributo (NPR-33071).
* Accesibilidad de formularios adaptables: Los campos marcados como obligatorios en un formulario adaptable no tienen el atributo obligatorio establecido en True en el esquema de accesibilidad ARIA (NPR-33070).
* Servicio PDFG: Cuando un usuario convierte un archivo de texto a un PDF, los caracteres japoneses no se representan correctamente (NPR-33238).
* Servicio PDFG: `CreatePDF` no se puede convertir un archivo PDF al formato OCR PDF (NPR-32994).
* Servicio PDFG: La conversión a PDF falla en la 200ª instancia de un [!DNL OpenOffice] documento (NPR-32766).
* BackendIntegration: Las solicitudes del modelo de datos de formulario fallan al caducar el token de actualización debido a un estado inactivo incorrecto (NPR-33169).
* Designer: Los lectores de pantalla ejecutan el orden de tabulación en función del orden geográfico predeterminado en lugar del orden de tabulación personalizado definido en el archivo XDP (NPR-32160).
* Designer: Si la opción de etiquetado está activada, el borde del subformulario desaparece en la salida PDF generada (NPR-32778).

## Install 6.5.5.0 {#install}

**Requisitos de configuración**

* AEM 6.5.5.0 requires AEM 6.5. See [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* La descarga del Service Pack está disponible en Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* En una implementación con MongoDB y varias instancias, instale AEM 6.5.5.0 en una de las instancias de creación mediante el Administrador de paquetes.
* Antes de realizar la instalación, realice una instantánea o una copia de seguridad nueva de la instancia de AEM.
* Reinicie la instancia antes de la instalación. Aunque esto solo es necesario cuando la instancia sigue en modo de actualización (y este es el caso cuando la instancia se actualizó desde una versión anterior), se recomienda si la instancia se ejecutó durante un período más largo.

>[!NOTE]
>
>Adobe no recomienda quitar o desinstalar el paquete de Adobe Experience Manager 6.5.5.0.

### Instalación de Service Pack {#install-service-pack}

Siga estos pasos para instalar Service Pack en una instancia existente de Adobe Experience Manager 6.5:

1. Descargue el Service Pack desde [Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.5.0) o [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip).

1. Abra el Administrador de paquetes y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener información sobre cómo utilizarla, consulte Administrador [de paquetes](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html).

1. Select the package and click **[!UICONTROL Install]**.

>[!NOTE]
>
>El cuadro de diálogo en la interfaz de usuario del administrador de paquetes a veces se cierra durante la instalación del Service Pack. Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete de actualización antes de asegurarse de que la instalación se realiza correctamente. Typically, this happens on [!DNL Safari] but can intermittently happen on any browser.

**Instalación automática**

Existen dos formas de instalar automáticamente Adobe Experience Manager 6.5.5.0 en una instancia de trabajo:

A. Coloque el paquete en la `../crx-quickstart/install` carpeta cuando el servidor esté disponible en línea. El paquete se instala automáticamente.

B. Utilice la API [HTTP del Administrador](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html)de paquetes. Utilícelo `cmd=install&recursive=true` para instalar los paquetes anidados.

>[!NOTE]
>
>Adobe Experience Manager 6.5.5.0 no admite la instalación de Bootstrap.

**Validar la instalación**

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.5.0)` en Productos instalados.

1. All OSGi bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: `/system/console/bundles`).

1. The OSGI bundle `org.apache.jackrabbit.oak-core` is version 1.10.6 or higher (Use Web Console: `/system/console/bundles`).

Para conocer las plataformas certificadas para trabajar con esta versión, consulte los requisitos [técnicos](/help/sites-deploying/technical-requirements.md).

### Instalación del paquete de complementos de formularios de Adobe Experience Manager {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Omita este paso si no utiliza AEM Forms. Las correcciones en los formularios de Adobe Experience Manager se entregan a través de un paquete de complemento independiente.

1. Asegúrese de que ha instalado Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Instalación de formularios de Adobe Experience Manager en JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Omita este paso si no utiliza AEM Forms en JEE. Las correcciones en los formularios de Adobe Experience Manager en JEE se entregan a través de un instalador independiente.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes for patch 0014](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0014.html).

### UberJar {#uber-jar}

UberJar para Experience Manager 6.5.5.0 está disponible en el repositorio [](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.5/)de Adobe Public Maven.

Para usar UberJar en un proyecto Maven, vea [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.5</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## Funciones en desuso {#removed-deprecated-features}

Esta sección lista las funciones y funciones que se han marcado como obsoletas en AEM 6.5.5.0. Las funciones que se planea eliminar en una versión futura se definen como obsoletas en primer lugar, con una opción alternativa para su uso.

Se aconseja a los clientes que revisen si utilizan la función o la capacidad en su implementación actual y que planifiquen cambiar su implementación para utilizar la opción alternativa.

| Área | Función | Reemplazo |
|---|---|---|
| Integraciones | La pantalla de inclusión **[!UICONTROL de servicios de nube de]** AEM ya no se utiliza. Con la integración de AEM y Destinatario actualizada en AEM 6.5 para admitir la API de Destinatario Standard, que utiliza la autenticación mediante Adobe IMS y E/S, y la función cada vez mayor de Adobe Launch para instrumentar las páginas de AEM para el análisis y la personalización, el asistente para la selección se ha vuelto funcionalmente irrelevante. | Configure las conexiones del sistema, la autenticación IMS de Adobe y las integraciones de Adobe I/O a través de los respectivos servicios de nube de AEM. |

## Problemas conocidos {#known-issues}

* Si va a instalar [!DNL Experience Manager] 6.5.5.0 con [!DNL Java] 11, reinicie el servidor después de instalar el Service Pack. No es necesario reiniciar el equipo si está instalando el Service Pack con [!DNL Java] 8.

* Si se cambia el nombre de una carpeta en la jerarquía [!DNL Experience Manager Assets] y se publica en la carpeta anidada que contiene un recurso, [!DNL Brand Portal]el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Durante la instalación de AEM 6.5.5.0, la actualización de [!DNL Chrome] la versión 83 provoca un problema al compilar los paquetes. Use otros exploradores disponibles, como [!DNL Internet Explorer] y [!DNL Firefox], u otras opciones de instalación de paquetes estándar de AEM para resolver el problema. El problema se resuelve tras instalar AEM 6.5.5.0.

* No se puede enviar un correo electrónico al servidor SMTP remoto mediante el remitente de correo predeterminado de AEM, ya que solo permite la comunicación mediante TLS v1.2. Quite el paquete `javax.mail:mail:1.5.0-b01` de `system/console` y actualice los paquetes para resolver el problema.

* Cuando un usuario selecciona configurar un campo por primera vez en un formulario adaptable, la opción para guardar una configuración no se muestra en el navegador de propiedades. Si selecciona configurar otro campo del formulario adaptable en el mismo editor, se resuelve el problema.

* Si [!UICONTROL el asistente para la configuración] de recursos conectados devuelve un mensaje de error 404 después de la instalación, vuelva a instalar manualmente los paquetes `cq-remotedam-client-ui-content` y `cq-remotedam-client-ui-components` mediante el Administrador de paquetes.

* Durante la instalación de AEM 6.5.x.x pueden aparecer los siguientes errores y mensajes de advertencia:
   * &quot;Cuando la integración de Target se configura en AEM mediante la API de Target Standard (autenticación IMS), la exportación de fragmentos de experiencia a Target provoca la creación de tipos de ofertas incorrectos. En lugar de tener que escribir &quot;Fragmento de experiencias&quot;/origen &quot;Adobe Experience Manager&quot;, Destino, se crean varias ofertas con el tipo &quot;HTML&quot;/origen &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La validación del lado del servidor de Formulario adaptable falla cuando se utilizan funciones acumuladas como SUM, MAX y MIN. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La zona interactiva de una imagen interactiva de Dynamic Media no está visible al obtener una vista previa del recurso a través del visor de pancarta de ventas.

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en AEM 6.5.5.0:

* [Lista de paquetes OSGi incluidos en AEM 6.5.5.0](assets/6550_bundles.txt)

* [Lista de paquetes de contenido incluidos en AEM 6.5.5.0](assets/6550_packages.txt)

## Restricted sites {#restricted-sites}

Estos sitios solo están disponibles para los clientes. Si es un cliente y necesita obtener acceso, póngase en contacto con su administrador de cuentas de Adobe.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/)
* [Póngase en contacto con el servicio de asistencia](https://docs.adobe.com/content/help/en/customer-one/using/home.html)al cliente Para obtener más información sobre el acceso al portal de asistencia técnica, consulte [Acceso al portal](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)de asistencia técnica.

>[!MORELIKETHIS]
>
>* [Notas de la versión de AEM 6.5](/help/release-notes/release-notes.md)
>* [Página de productos AEM](https://www.adobe.com/solutions/web-experience-management.html)
>* [Documentación de AEM 6.5](https://helpx.adobe.com/support/experience-manager/6-5.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

