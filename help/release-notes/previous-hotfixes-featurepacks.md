---
title: Notas de la versión anterior de AEM 6.5 Service Pack
description: Notas de la versión específicas de Adobe Experience Manager 6.5 Service Pack 3 y versiones anteriores.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: 0e95ac8850a693764b82a29960b472d156dac535

---


# Revisiones y paquetes de funciones incluidos en instancias de Service Pack anteriores {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## Adobe Experience Manager 6.5.3.0

[!DNL Adobe Experience Manager] 6.5.3.0 es una versión importante que incluye correcciones y mejoras clave para el cliente, de rendimiento, estabilidad y seguridad, publicadas desde la disponibilidad general de la versión 6.5 en **abril de 2019**. It can be installed on top of [!DNL Adobe Experience Manager] 6.5.

Algunos aspectos destacados de esta versión del Service Pack son:

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.10.6.

* [!DNL Experience Manager Assets] ahora admite archivos ZIP creados con el algoritmo Deflate64.

* Se ha agregado una nueva columna para la fecha de creación, que es ordenable, en la vista de lista DAM y en los resultados de búsqueda de recursos en la vista de listas.

* La clasificación de recursos basada en la columna Nombre se ha activado en la vista de Listas.

* [!DNL Dynamic Media] ahora admite recursos de vídeo de recorte inteligente. Smart Crop es una función de aprendizaje automático que vuelve a recortar un vídeo mientras mueve el fotograma para seguir el punto focal de la escena.

* [!DNL Dynamic Media] admite imágenes inteligentes.

* Posibilidad de [establecer las preferencias fuera de oficina](../forms/using/configure-out-of-office-settings.md) en [!DNL Experience Manager] flujos de trabajo.

* Posibilidad de [compartir elementos](../forms/using/configure-shared-queues-osgi.md) de Bandeja de entrada o Bandeja de entrada con otros usuarios en [!DNL Experience Manager] flujos de trabajo.

* Capacidad para [generar comunicaciones interactivas en modo](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)por lotes.

* Se ha actualizado la versión de jQuery incluida en ContextHub a 3.4.1.

### Assets {#assets-6530-enhancements}

**Mejoras del producto**

* [!DNL Experience Manager Assets] ahora admite archivos ZIP creados con el algoritmo Deflate64 (NPR-27573).

* Se ha agregado una nueva columna para la fecha de creación, que es ordenable, en la vista de lista DAM y en los resultados de búsqueda de recursos en la vista de listas (NPR-31312).

* Se ha permitido la ordenación de recursos basada en la columna Nombre en la vista de Listas (NPR-31299).

* Los archivos de recursos GLB, GLTF, OBJ y STL admiten la previsualización de recursos en la página Detalles de recursos de DAM (CQ-4282277).

* El evento ReplicationOnModifyListener se activa para nodos de fragmento durante la carga de fragmentos en [!DNL Dynamic Media] (CQ-4281279).

* [!DNL Dynamic Media] ahora admite recursos de vídeo de recorte inteligente. Smart Crop es una función de aprendizaje automático que vuelve a recortar un vídeo mientras mueve el fotograma para seguir el punto focal de la escena (CQ-4278995).

* [!DNL Dynamic Media] admite imágenes inteligentes (CQ-422249).

* La vista de búsqueda y exploración se ha establecido como vista predeterminada en el selector de base si se pasan parámetros de consulta en la solicitud (NPR-31601).

**Correcciones**

* Los metadatos de algunos documentos PDF no se actualizan ni guardan en el PDF al modificar su título (NPR-31629).

* El uso compartido de recursos no funciona para los recursos que tienen el carácter más &#39;+&#39; en sus nombres (NPR-31547).

* Las ediciones en el formulario de búsqueda predeterminado Administración de recursos * El carril de búsqueda no funciona de la forma esperada (NPR-31502).

* No se muestran sugerencias al utilizar la vista de recursos de Omniture para buscar recursos (NPR-31496).

* Las referencias de recursos dentro de las colecciones no se actualizan cuando los recursos a los que se hace referencia se mueven a otra ubicación, en casos en los que diferentes usuarios hacen referencia a los mismos recursos (NPR-31486).

* Las etiquetas IPTC de Duplicado se agregan a los metadatos de los recursos (NPR-31328).

* El recuento de resultados de búsqueda en la esquina superior derecha no se actualiza con precisión cuando la búsqueda se activa desde el carril de filtros (NPR-31316).

* Todas las casillas de verificación se desactivan al desactivar las casillas de verificación de segundo nivel en el filtro Tipo de archivo y el texto de la barra de búsqueda no está sincronizado con las propiedades seleccionadas o no seleccionadas (NPR-31287).

* No se pueden quitar todos los miembros (usuarios/grupos) de la sección Miembros de una carpeta; al intentar eliminar todos los usuarios, el usuario que ha iniciado sesión se agrega a la lista (NPR-31171).

* Los recursos con el símbolo más &#39;+&#39; en el nombre del archivo no se pueden eliminar (NPR-31162).

* El menú desplegable Crear, que está visible en el menú superior al seleccionar una carpeta, no muestra &#39;Carpeta&#39; como opción de creación (NPR-30877).

* Selección de carpetas Crear > Elemento de acción FileUpload falta cuando se aplica ACL para Deny jcr:removeChildNodes y jcr:removeNode en la ruta a un usuario (NPR-30840).

* Los flujos de trabajo DAM pasan a un estado antiguo cuando se cargan determinados recursos mp4, lo que provoca que todos los flujos de trabajo restantes pasen a un estado antiguo (NPR-30662).

* Error de memoria insuficiente cuando se carga un archivo PDF grande (de varios gigabytes) en DAM y se procesan sus subrecursos (NPR-30614).

* El movimiento masivo de recursos está fallando y mostrando un mensaje de advertencia (NPR-30610).

* Los nombres de los recursos se cambian a minúsculas al mover recursos de una carpeta a otra en [!DNL Experience Manager] ejecución en el modo de ejecución de [!DNL Dynamic Media] Scene7 (NPR-31630).

* Se observa un error al editar un conjunto de imágenes remoto para la imagen que reside en la carpeta con el mismo nombre de compañía de Scene7 (NPR-31340).

* [!DNL Dynamic Media] los recursos que contienen referencias no se publican (NPR-31180).

* Las cargas desde [!DNL Experience Manager Dynamic Media] Scene7 en modo de ejecución a Scene7 tardan demasiado en completarse (NPR-31048).

* La zona interactiva añadida a un recurso de imagen no es visible a través del visor de imágenes interactivo en la página de detalles de recursos (NPR-30979).

* Se crean enormes trabajos de sling y vuelve a aparecer la pancarta de procesamiento cuando las acciones realizadas en recursos en [!DNL Experience manager Assets] se pasan a la escena 7 (NPR-30947).

* El conflicto se produce al crear una copia de idioma de los recursos y no se carga en Scene7 (NPR-30932).

* Las representaciones dinámicas descargadas de [!DNL Experience Manager] la ejecución en modo [!DNL Dynamic Media] híbrido están dañadas (son de tipo de texto con contenido que &#39;no puede encontrar la imagen&#39; en lugar de tipo de contenido de imagen) (NPR-30876).

* [!DNL Dynamic Media] El flujo de trabajo de codificación de vídeo no puede generar miniaturas para el vídeo migrado de Scene7 al modo [!DNL Dynamic Media] de ejecución de Scene7 (CQ-4282011).

* Se ha observado una excepción IpsApiException al migrar recursos de una instancia a otra mediante distintos ID de compañía de Scene7 (CQ-4280548).

* La miniatura del recurso 3D no es informativa cuando se ingesta un modelo 3D compatible [!DNL Experience Manager] (CQ-4283701).

* Los botones de desplazamiento se muestran en el visor si un recurso 3D tiene pocas vistas de cámara (CQ-4283322).

* Altura incorrecta del contenedor de un modelo 3D cargado previsualizado en la página de detalles de recursos de Dimensional Viewer (CQ-4283309).

* Los vídeos no se pueden reproducir con SmartCropVideoViewer en Internet Explorer 11 y Safari (CQ-4281422).

* El uso del botón Mover para mover varios recursos, de una carpeta a otra, no se puede [!DNL Experience Manager] ejecutar en el modo de ejecución [!DNL Dynamic Media] - scene7 (CQ-4280384).

* El vídeo distorsionado se ve en los detalles del recurso cuando el tipo MIME no es MP4 (CQ-4279704).

* Los vídeos recientemente ingestados en carpetas con perfil de vídeo permanecen en estado de procesamiento incluso después de que el porcentaje de codificación se complete al 100 % (CQ-4279389).

* Al mover recursos desde una carpeta, se crea un gran número de trabajos de sling (llamadas a la API de Scene7) que lo que se necesita de forma ideal (CQ-4278664).

* Los nombres del conjunto de imágenes se cambian a minúsculas en la escena 7, cuando se crea un conjunto de imágenes (o conjunto de medios) y se les asigna un nombre con la convención de nombres adecuada en DAM (CQ-4281112).

* El migrador de Scene7 establece el estado de publicación de forma incorrecta (CQ-4263492).

* La página de resultados de la búsqueda por IU táctil (realizada a través de Omniture) se desplaza automáticamente hacia arriba y pierde la posición de desplazamiento del usuario en los fragmentos de contenido (CQ-4282898).

* Los archivos PDF no se indexan y el contenido dentro de no se puede buscar (CQ-4278916).

* Error &quot;Grupo no enumerado por selector de usuario: &quot;se espera que false sea igual a true&quot; se observa al agregar un grupo de usuarios cerrado con diferente `principalName` y `authorizableId` (CQ-4278177).

* La Vista de columna de la interfaz de usuario de recursos muestra todas las rutas, independientemente de la ruta raíz de la presa específica del inquilino (CQ-4278175).

* La búsqueda del selector de recursos no funciona correctamente (CQ-4275886).

* Los Flujos de trabajo de representación fallan (CQ-4271928).

* Depuración de Evento DAM elimina los datos de evento más recientes (maxSavedActivities) y contiene los datos creados anteriormente (NPR-31336).

* La página de resultados de la búsqueda por IU táctil (realizada a través de Omnisearch) se desplaza automáticamente hacia arriba y pierde la posición de desplazamiento del usuario (NPR-31307).

* La barra de acciones y el recuento de recursos no se actualizan al seleccionar todo y, a continuación, anular la selección de algunos elementos (carpetas/recursos individuales) en la IU táctil (NPR-31118).

* Se muestra una excepción en [!DNL Experience Manager] la encuesta para obtener detalles de un recurso (CQ-4283569).

### Sites {#sites}

* Si la herencia de LiveCopy está dañada, las páginas de Live Copy muestran vínculos de copia de idioma en lugar de vínculos de LiveCopy (NPR-30980).
* Para un nuevo modelo, si el número de registros es superior a 40, solo se muestran los primeros 40 registros. El modelo muestra líneas en blanco para el resto de los registros (NPR-31182).
* Cuando un usuario agrega caracteres japoneses o coreanos en la propiedad description de un menú, el menú muestra caracteres distorsionados para texto en japonés y coreano. (NPR-31331).
* El editor de texto enriquecido (RTE) no permite insertar una tabla incrustada como elemento de lista (NPR-30879).
* Fuera de la casilla, scaffolding Rich Text Editor (RTE). aplica tamaño de fuente en línea a los elementos de forma inesperada (NPR-31284).
* Cuando un usuario se centra en los campos del carril izquierdo y utiliza un método abreviado de teclado para pegar contenido, pega el contenido del portapapeles del editor de páginas en lugar del contenido copiado de los campos del carril izquierdo (NPR-31172).
* Cuando un usuario agrega un campo Carga de archivo a un campo múltiple, la ruta de la imagen se almacena en el nodo del componente en lugar del nodo de varios campos (NPR-30882).
* La API ResponsiveGridExporter no devuelve la interfaz com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter. El paquete com.day.cq.wcm.foundation.model.impl se declara como paquete privado (NPR-31398).
* Cuando se abre una página que contiene algunos fragmentos de experiencia en modo que no es de editor (ya sea en Autor sin el `editor.html` prefijo y `wcmmode=disabled`o en Editor), la solicitud termina en el código de error de estado HTTP 500 (NPR-30743).
* Los usuarios no pueden cambiar su contraseña ni acceder a su página de perfil (NPR-31161).

### Búsqueda e interfaz de usuario {#search-ui-interface}

* Al cambiar de la vista de tarjeta a la vista de Lista en una página de resultados de búsqueda, hay un retraso antes de que se pueda desplazar la página (NPR-31286).

* La casilla de verificación Seleccionar todo está oculta en la vista de Lista de la [!DNL Sites] interfaz de usuario (NPR-31614).

* El recuento Seleccionar todo en una página de resultados de búsqueda es incorrecto (NPR-31120).

* El editor de metadatos muestra etiquetas que no existen (NPR-31119).

### Traducción {#translation}

* Aparecen dos ventanas emergentes de calendario al seleccionar la opción Fecha de vencimiento en un trabajo de traducción (NPR-31270).

### Plataforma {#platform}

* La opción Tipo de MIME en la consola web no funciona (NPR-31108).

* El certificado de cliente no se acepta al configurar el inicio de sesión único (NPR-31165).

* Las actualizaciones en la configuración del tamaño del búfer para el servicio HTTP basado en Jetty no se guardan (NPR-30925).

* QueryBuilder ahora admite pedidos ``fn:name()`` en consultas xpath (NPR-31322).

* El árbol de activación de Duplicado se crea al actualizar desde [!DNL Experience Manager] 6.3 (NPR-31513).

* Las solicitudes reenviadas no conservan los encabezados de respuesta establecidos durante la autenticación sling (NPR-30013).

* La búsqueda dentro de los componentes del selector no funciona (NPR-31692).

* Se muestra un error al adjuntar un archivo ZIP a una [!DNL Experience Manager Communities] publicación debido a las diferentes versiones del paquete Apache POI y Apache Tika (NPR-31018).

* El ``org.apache.sling.distribution.api`` paquete está oculto en el administrador de configuración y, por lo tanto, no está disponible para paquetes personalizados (NPR-31720).

### Proyectos {#projects}

* El cambio de vistas de calendario no funciona (NPR-31271).

### Brand Portal {#assets-brand-portal}

**Mejoras del producto**

* El flujo de trabajo de importación de fuentes de recursos en [!DNL Experience Manager Assets] se modifica para recuperar solo los recursos recién creados de [!DNL Brand Portal] a [!DNL Experience Manager], y omitir los recursos que ya existen en la carpeta NEW para evitar la replicación (CQ-4278527).

**Correcciones**

* Aparece un icono incorrecto al crear una nueva carpeta de contribución en la función de fuentes de recursos (CQ-4282825).
* Al crear una nueva carpeta Contribution, una o ambas subcarpetas (NUEVAS y COMPARTIDAS) no aparece dentro de la carpeta Contribution (CQ-4282424).
* El sistema emite una excepción si el usuario intenta volver a publicar la carpeta Contribution de [!DNL Experience Manager] a [!DNL Brand Portal] después de recibir nuevos recursos en la carpeta Contribution desde el [!DNL Brand Portal] final (CQ-4279740).
* La creación de la carpeta Contribution dentro de una carpeta Contribution (carpeta anidada) está prohibida para evitar la complejidad (CQ-4278391).
* El sistema emite una excepción al cargar la lista del [!DNL Brand Portal] usuario (archivo .csv) importada desde la Consola [!DNL Experience Manager] de administración. Solo son obligatorios los campos Correo electrónico, Nombre y Apellido del archivo .csv (CQ-4278390).

### Communities {#communities}

**Correcciones**

* Los vínculos rápidos para administrar grupos (Abrir/Editar/Publicar/Eliminar grupos) no son visibles para los administradores de la comunidad (administrador del grupo/administrador del sitio) (NPR-31627).
* Un blog enviado no se muestra a menos que la página se actualice o recargue manualmente (NPR-31599).
* La consulta JCR utilizada por la función &quot;Menciones&quot; distingue entre mayúsculas y minúsculas y tarda demasiado en devolver resultados (NPR-31475).
* [!DNL Experience Manager] 6.5 El archivo UberJar emite una excepción; falta el paquete `cq-social-translation` del archivo [!DNL Experience Manager] 6.5 UberJar (NPR-31186).
* Las bibliotecas del enlace de datos Jackson se actualizaron a la versión 2.9.9.3 para abordar nuevas vulnerabilidades (NPR-30967).
* Los títulos de las actividades y las notificaciones son incoherentes (NPR-30941).
* Pagination is not working properly in [!DNL Communities] Blogs (NPR-30914).
* Analytics reports are not populated in [!DNL Experience Manager] author environment, blank page appears (NPR-30913).

### Oak {#oak}

* Las actualizaciones del índice de Lucene hacen que el servidor de creación se ralentice (NPR-31548).

### Formularios {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack no incluye correcciones para [!DNL Experience Manager Forms]. Estas se entregan mediante un paquete independiente de complementos de Forms. In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. Para obtener más información, consulte [Instalación del complemento](#install-aem-forms-add-on-package) de formularios de Experience Manager e [Instalación de formularios de Experience Manager en JEE](#install-aem-forms-jee-installer).

#### Paquete de complemento de Forms {#forms-add-on-package-6530}

**Formularios adaptables**

* Las cadenas contienen la clave del diccionario al localizar formularios adaptables (NPR-31110).

**Comunicación interactiva**

* **MissingNode.toString()** devuelve resultados inexactos después de actualizar las bibliotecas de Jackson a 2.10.0 (NPR-31549).

* El editor de texto elimina aleatoriamente los caracteres de espacio del texto copiado de Microsoft Word (NPR-31113).

**Administración de correspondencia**

* Los rótulos y la información sobre herramientas no se muestran al migrar letras de LiveCycle ES4SP1 a [!DNL Experience Manager] 6.5 (NPR-31615).

* **El formato de flujo de texto ya no se muestra** en los mensajes de error al guardar las letras como borradores (NPR-30463).

**Flujo de trabajo**

* El flujo de trabajo de OSGi falla debido a la utilización del 100% de la CPU (NPR-31233).

**HTML5 Forms**

* Al generar la vista previa HTML5 de un formulario XDP, se muestra un parpadeo al agregar instancias de un subformulario (NPR-30909).

#### Forms on JEE installer {#forms-jee-installer-6530}

**Forms: servicios de documentos**

* El servicio web SOAP que utiliza MTOM en un proyecto .NET muestra excepciones para los métodos AssemblerServiceClient invoke y HtmlToPDF2 (NPR-4281771).

**Base JEE**

* La configuración de la acción no carga los nombres de proceso para la acción de envío Invocar un flujo de trabajo de formularios (NPR-31478).

### Paquetes de funciones incluidos {#feature-packs-included-6530}

>[!NOTE]
>
>For [!DNL Experience Manager Forms] customers, it is essential to install [!DNL Experience Manager Forms] add-on package after installing any [!DNL Experience Manager] Service Pack, Cumulative Fix Pack, or Feature Pack.

#### Forms: base JEE {#forms-foundation-jee-feature}

* [!DNL Experience Manager] Compatibilidad con formularios para Oracle 18c (NPR-29155).

## Adobe Experience Manager 6.5.2.0

[!DNL Adobe Experience Manager] 6.5.2.0 es una versión importante que incluye correcciones y mejoras clave de rendimiento, estabilidad, seguridad y del cliente publicadas desde la disponibilidad general de [!DNL Adobe Experience Manager] 6.5 en **abril de 2019**. It can be installed on top of [!DNL Experience Manager] 6.5.

Algunos aspectos destacados de esta versión del Service Pack son:

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.10.3.
* Se agregó una propiedad de configuración para permitir la exportación de fragmentos de experiencia directamente a espacios de trabajo que haya definido el usuario en [!DNL Adobe Target].
* Los usuarios de recursos pueden buscar imágenes visualmente similares. [!DNL Experience Manager] muestra las imágenes con etiquetas inteligentes del repositorio de DAM similares a una imagen seleccionada por el usuario. Consulte [Búsqueda visual](../assets/search-assets.md#visualsearch).

* Se mejoró la funcionalidad de los recursos conectados para añadir la compatibilidad con la recuperación de documentos desde implementaciones de DAM remotas. Los autores del sitio pueden buscar y filtrar los tipos de documentos admitidos en el Buscador de contenido. Los documentos remotos se pueden agregar al componente Descargar en páginas web. Consulte [Uso de activos conectados](../assets/use-assets-across-connected-assets-instances.md).

* Mejorarfiltros de tipo de documento con más tipos MIME para admitir opciones de varios valores.
* Se ha introducido un flujo de trabajo de reprocesamiento externo para la compatibilidad con varios recursos
* Rendimiento optimizado [!DNL Dynamic Media] mediante el uso de filtros de recursos predeterminados para la replicación.
* Se han restaurado las opciones de edición de los recursos de recorte o rotación para DMS7.
* Se ha implementado una opción para silenciar un vídeo durante la carga en VideoPlayer.
* Se ha introducido una corrección para garantizar que la vista de columnas de la IU de recursos muestre solo contenido específico del usuario.
* Se ha introducido una corrección para permitir que los cambios de acordeón de estilo se reflejen en los resultados de búsqueda.

### Assets {#assets}

**Mejoras del producto**

* Se mejoró la funcionalidad de los recursos conectados para añadir la compatibilidad con la recuperación de documentos desde implementaciones de DAM remotas. Los autores del sitio pueden buscar y filtrar los tipos de documentos admitidos en el Buscador de contenido. Los documentos remotos se pueden agregar al componente Descargar en páginas web. Revisión para CQ-4270245. Consulte [Uso de activos conectados](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Experience Manager Assets] los usuarios pueden buscar imágenes visualmente similares. [!DNL Experience Manager] muestra las imágenes con etiquetas inteligentes del repositorio de DAM similares a una imagen seleccionada por el usuario. Consulte [Búsqueda visual](../assets/search-assets.md#visualsearch).

**Correcciones**

* Las rutas de recursos de las direcciones URL y los metadatos de las carpetas que genera la API de ACP no son URL codificadas. GRANITE-26198: revisión para CQ-4271814
* Unzipping an archive with a folder having a percent sign (%) in its name can not be opened using [!DNL Experience Manager Assets] interface. NPR-29989: revisión para CQ-4270467
* IU táctil: Durante el asistente para administrar la publicación, las referencias se agregan después de la página en el cuerpo de la solicitud de publicación, lo que provoca que todos los recursos se publiquen después de la página y, cuando se procesa la página, se pierden algunos de los recursos de la instancia de publicación. NPR-29985: revisión para CQ-4270724
* La función de recursos no relacionados no funciona en recursos relacionados que tienen caracteres especiales (caracteres que se codifican con el URI) en el nombre. NPR-30387: revisión para CQ-4274446
* Al editar un fragmento de contenido, la versión se crea con el usuario incorrecto.
* Error durante la creación de colecciones en el sistema basado en inquilinos. NPR-30114: revisión para CQ-4272948
* La vista de columnas de la IU de recursos no respeta la ruta raíz de DAM del inquilino actual, pero accede a todas las rutas de DAM del inquilino. NPR-30636: revisión para CQ-4275481
* Posible ejecución de scripts en sitios múltiples a través de la ventana de alerta de archivos restringidos, ya que la imagen insertada se puede ver. NPR-30617: revisión para CQ-4270133
* MultiTenant: Los inquilinos que guardan las propiedades de la carpeta observan que tanto el mensaje de éxito como el mensaje de error que describe la acción no se han realizado correctamente: &quot;No se pueden editar las propiedades. Permisos insuficientes&quot;. Esto, por lo tanto, puede causar confusión. NPR-30545: revisión para CQ-4275333
* El cuadro de diálogo del selector de recursos no permite la selección de recursos, por lo que no se puede actualizar el origen con la funcionalidad de reemplazo de origen relacionada. NPR-30502: revisión para CQ-4275029
* Flujo de trabajo de recursos de actualización de DAM: tiene un estado obsoleto al cargar archivos mp4 de gran tamaño. NPR-30480: revisión para CQ-4271352
* La funcionalidad para crear la tarea de revisión no funciona debido a una carga útil nula que provoca que todas las acciones relacionadas con la tarea de revisión subsiguientes no funcionen. NPR-30468: revisión para CQ-4274263
* Problema de conectividad de etiquetas inteligentes de Adobe a través de Datapower. NPR-30026: revisión para CQ-4269457
* La vista de columnas de la IU de recursos genera un error al intentar abrir los filtros en el carril izquierdo. NPR-30501: revisión para CQ-4273862
* Al agregar grupos sincronizados desde LDAP en las propiedades del grupo de usuarios cerrado (CUG) de una carpeta de recursos, el grupo no se guarda ni se recupera. NPR-30615: revisión para CQ-4274689
* Los campos de orientación y estilo de búsqueda de filtro no aplican el valor completado automáticamente a la consulta de búsqueda. NPR-30620: revisión para CQ-4275724
* El vínculo de uso compartido de los recursos de una carpeta con espacio y carácter &quot;&amp;&quot; en el nombre, muestra elementos en gris vacíos en algunos recursos. NPR-30557: revisión para CQ-4270187
* El formulario del esquema de metadatos de carpeta no detecta automáticamente el tipo de datos y, por lo tanto, no crea el elemento TypeHint relacionado al enviar el formulario. NPR-30599: revisión para CQ-4275227
* Las opciones de edición de recorte y rotación de recursos están desactivadas en la IU de creación de DMS7. NPR-30118: revisión para CQ-4273221
* Share Link feature is not working on [!DNL Experience Manager] instance with DMS7 configuration. NPR-30080, NPR-30492: revisión para CQ-4273651
* Adding the [!DNL Dynamic Media] Scene7 component to the page, and then publishing the page does not trigger the dmscene7 configuration every time. NPR-30641: revisión para CQ-4275962
* Added an IPSJobJournal in [!DNL Experience Manager] to create only one Intrusion Prevention Systems (IPS) job per processing profile. NPR-30490: revisión para CQ-4273614
* [!DNL Dynamic Media]:: Se han Añadido filtros predeterminados para excluir recursos de la replicación en el nodo de [!DNL Experience Manager] publicación. NPR-30538: revisión para CQ-4274678
* Se ha introducido un flujo de trabajo de reprocesamiento externo para la compatibilidad con varios recursos a fin de permitir que la carpeta sea una carga útil. El flujo de trabajo consta de dos pasos: vuelve a procesar los recursos sin controladores mediante el mapa de metadatos al paso siguiente y vuelve a cargar todos los recursos sin el control de recursos en S7 en un solo trabajo de IPS. For more details, see Configuring [!DNL Dynamic Media] Cloud Services. NPR-30489: revisión para CQ-4272903
* Al cargar un archivo CSV incorrecto después de uno correcto, se elimina el archivo CSV correcto. Revisión para CQ-4277694, CQ-4277814
* Se va a eliminar el icono incorrecto específico de las carpetas de contribución. Revisión para CQ-4277580
* Al seleccionar un usuario en el selector de usuarios de la ficha Contribución de recursos, el nombre del usuario no aparece en la tabla y el cuadro de diálogo Eliminar usuario que está en la página Propiedades muestra un texto incorrecto. Revisión para CQ-4277875
* Los colaboradores no se pueden agregar a la carpeta de Contribución de recursos desde el selector de usuarios al seleccionar al usuario y hacer clic en Añadir. Revisión para CQ-4277824, CQ-4278087
* La búsqueda por nombre de usuario en minúsculas no funciona en el selector de usuarios. Revisión para CQ-4277958, CQ-4277930
* Los usuarios que no son administradores pueden publicar recursos en una nueva carpeta que esté en una carpeta de contribución de recursos. Revisión para CQ-4278200
* dam-user (no es administrador) no tiene la opción de añadir colaboradores a la carpeta de contribución de recursos. Revisión para CQ-4278192
* El botón &quot;Crear&quot; está visible en la carpeta de contribución de recursos. Revisión para CQ-4277560
* Sorting search query by relevance returns [!DNL InDesign] documents along with [!DNL InDesign] templates. Revisión para CQ-4273864
* Si el usuario tiene un id. de correo electrónico en mayúsculas, los usuarios no pueden registrar los recursos que ya se han extraído. Revisión para CQ-4276575
* La operación Eliminar solo se aplica a los ajustes preestablecidos seleccionados y, si la pantalla actualiza automáticamente la lista después de la operación, se muestran otros ajustes preestablecidos que ya se han actualizado. Revisión para CQ-4261461
* Configuring [!DNL Dynamic Media] Cloud Services in DMHybrid mode results in multiple empty report suites created in [!DNL Analytics], and with no report suite id stored in [!DNL Experience Manager], resulting in report suite duplication. Revisión para CQ-4249780
* Rename operation in [!DNL Experience Manager] asset to duplicated name fails to synchronize to Scene7. Revisión para CQ-4276763
* El contenido que creó el usuario se muestra incorrectamente en el panel de filtros de búsqueda. Revisión para CQ-4273875
* La opción Buscar similares no está disponible en imágenes TIFF. Revisión para CQ-4278238
* Se ha implementado la opción de silenciar el vídeo durante la carga en VideoPlayer. Revisión para CQ-4266465
* Visores: Visor de vídeos: poster=none funciona incorrectamente en caso de que se utilice un vídeo externo. Revisión para CQ-4265536
* El icono de espera está visible durante la reproducción de vídeos en los navegadores IE11 y MS Edge. Revisión para CQ-4251539
* Los archivos README de los visores 3.8 y 5.13 no se actualizan y contienen información de versiones anteriores. Revisión para CQ-4273737
* El fragmento de contenido recibe versiones incluso antes de guardar los cambios. NPR-30616: revisión para CQ-4273088
* Se reemplaza el valor de Asset#getMetadata(String) con Asset#getMetadataValueFromJcr(String) en el proceso de creación de miniaturas. NPR-30491: revisión para CQ-4273067
* La carga de archivos JPG devuelve varias instancias del mensaje &quot;Replicación del elemento ReplicateOnModifyWorker ACTUALIZADA&quot; en cada recurso, lo que provoca una degradación del rendimiento.
* Si se descomprime el archivo zip mediante la función Extraer archivo se producen problemas con las carpetas cuyo nombre contiene el símbolo de porcentaje (%) en el título. NPR-29990: revisión para CQ-4270467

### Sites {#sites-6520}

* Si la herencia de LiveCopy está dañada, las páginas de Live Copy muestran vínculos de copia de idioma en lugar de vínculos de LiveCopy. (NPR-30980)
* Para un nuevo modelo, si el número de registros es superior a 40, solo se muestran los primeros 40 registros. El modelo muestra líneas en blanco para el resto de los registros. (NPR-31182)
* El complemento Editor de texto enriquecido (RTE) del componente de texto muestra caracteres distorsionados para texto en japonés y coreano. (NPR-31331)
* El Editor de texto enriquecido (RTE) no permite insertar una tabla incrustada como elemento de lista. (NPR-30879)
* El Editor de texto enriquecido (RTE) de scaffolding de fuera del cuadro se aplica de forma inesperada al tamaño de fuente en línea a los elementos. (NPR-31284)
* Cuando un usuario se centra en los campos del carril izquierdo y utiliza combinaciones de teclas para pegar contenido, pega el contenido del portapapeles del editor de páginas en lugar del contenido copiado de los campos del carril izquierdo. (NPR-31172)
* Cuando un usuario agrega un campo Carga de archivo a un campo múltiple, la ruta de la imagen se almacena en el nodo del componente en lugar del nodo de varios campos. (NPR-30882)
* La API ResponsiveGridExporter no devuelve la interfaz com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter. El paquete com.day.cq.wcm.foundation.model.impl se declara como paquete privado. (NPR-31398)
* Cuando se abre una página que contiene algunos fragmentos de experiencia en modo que no es de editor (ya sea en Autor sin el `editor.html` prefijo y `wcmmode=disabled`o en Editor), la solicitud termina en el código de error de estado HTTP 500. (NPR-30743)

### WCM: editor de páginas {#wcm-page-editor-6520}

**Mejoras del producto**

* Mejorarfiltros de tipo documento con más tipos MIME para admitir opciones de varios valores. Revisión para CQ-4270694

### Administración de fragmentos de contenido {#content-fragment-management-6520}

* La consulta que isa la IU de los modelos de fragmento de contenido es muy lenta y, finalmente, acaba en error. Revisión para CQ-4270807

### IU: bases {#ui-foundation}

* Desencadenador de accesos directos que impide que el usuario utilice &quot;m,&quot; &quot;p,&quot; y &quot;e&quot; en las interfaces de usuario específicas. NPR-30355: revisión para GRANITE-26346
* Closing [!DNL Experience Manager Assets] Search UI does not reset the left rail to Content selection preventing the user from opening the filter rail the second time subsequently. NPR-30509: revisión para CQ-4274716
* Multi-tenant environment: [!DNL Experience Manager Assets] UI top navigation is not available and throwing JavaScript error. NPR-30104: revisión para GRANITE-26344

### Traducción {#translation-6520}

* Problema de traducción: solo unos pocos componentes se traducen mediante traducción automática. NPR-30079: revisión para CQ-4273764

### Plataforma {#platform-6520}

* [!DNL Experience Manager]El remitente de correo predeterminado de no puede enviar correo a un servidor SMTP remoto a través de TLS v1.2. NPR-30476: revisión para GRANITE-26605

### Proyectos {#projects-6520}

* Los valores de dam:folderThumbnailPaths no se actualizan y muestran miniaturas antiguas incluso después de eliminar los recursos de la carpeta. NPR-30424: revisión para CQ-4273667
* Al completar la opción Mover, el título y el nombre del activo no cambian. NPR-30647: revisión para CQ-4276265

### Comunidades {#communities-6520}

* El diagnóstico de sincronización de usuarios está completamente dañado y no funciona. NPR-30004, NPR-29943: revisión para CQ-4270287, CQ-4271348

### Sling {#sling}

* La instancia actualizada de 6.3.3.2 a 6.5 devuelve configuraciones OSGi duplicadas. NPR-30130: revisión para CQ-4274016

### Integración {#integration}

* El contenido personalizado no se muestra correctamente en la instancia de publicación hasta que no se reinicia la instancia. NPR-30377: revisión para CQ-4273706
* Al configurar el inicio en un sitio web, la dirección de la biblioteca tiene una barra diagonal (/) precargada, lo que provoca que el usuario tenga que intervenir de forma manual cada vez. NPR-30694: revisión para CQ-4275501

### Forms {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack no incluye correcciones para [!DNL Experience Manager Forms]. They are delivered using a separate [!DNL Forms] add-on package. In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. For more information, see [Install Experience Manager Forms add-on](#install-aem-forms-add-on-package) and [Install Experience Manager Forms JEE installer](#forms-jee-installer).

The key highlights for [!DNL Experience Manager] 6.5.2.0 forms are:

* Added &#39;Auto&#39; setting to `RenderAtClient` in `PDFFormRenderOptions` API for [!DNL Experience Manager] Forms OSGi.

#### Paquete de complemento de Forms {#forms-add-on-package}

**Integración del back-end**

* No se puede configurar el modelo de datos de formulario con una URL de carga equilibrada alojada en AWS. NPR-30123: revisión para CQ-4273359
* Al crear el modelo de datos de formulario (FDM) con el lenguaje de definición de servicio Web (WSDL), se `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` devuelve el mensaje de error: NPR-30477: Revisión para CQ-4272921

**Administración de correspondencia**

* &quot;La representación de Crear interfaz de usuario de correspondencia (IU de CCR) falla de forma intermitente con el siguiente error en la consola:
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**Comunicación interactiva**

* Un campo marcado como obligatorio en el modelo de datos del formulario se muestra como necesario en la IU para crear correspondencia. NPR-30623: revisión para CQ-4274902

**Forms: flujo de trabajo**

* Las variables de salida no asignadas en las carpetas inspeccionadas hacen que la invocación genere un error. Revisión para CQ-4264451

**HTML5 Forms**

* Cuando se implementa el código o proyecto personalizado por segunda vez, la página no se procesa y se produce el siguiente error:

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539: revisión para CQ-4272509

* Cuando se utiliza la opción de acceso al escritorio no visual en el modo Examinar para leer un formulario de HTML5, el navegador Chrome lee el elemento &quot;gráfico&quot; antes que cada gráfico vectorial escalable (SVG) en el diseño de formulario. NPR-30449: revisión para CQ-4274732

#### Instalador JEE de Forms {#forms-jee-installer}

**Forms: seguridad de documentos**

* El proceso de aplicación de una firma con marca de hora devuelve el error: ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException: error de invocación. NPR-30820: revisión para CQ-4275852

**Forms: servicios de documentos**

* Si &quot;SubmitURL&quot; contiene un símbolo &amp;, se muestran errores de análisis en el registro cuando se realiza una solicitud POST para procesar el servlet de renderpdf. NPR-30865: revisión para CQ-4278232

**Forms: base JEE**

* El servicio HTMLtoPDF no muestra maxReuseCount en la consola JMX. NPR-30134, NPR-30304: revisión para CQ-4273763
* Adding or editing a Web Service connection by invoking web services from [!DNL Experience Manager Forms] Workbench throws an error: ClassNotFoundException org.apache.axis.message.SOAPBodyElement. NPR-30105: revisión para CQ-4273217

### Paquetes de funciones incluidos {#feature-packs-included}

>[!NOTE]
>
>For [!DNL Experience Manager Forms] customers, it is essential to install [!DNL Experience Manager Forms] add-on package after installing any [!DNL Experience Manager] Service Pack, Cumulative Fix Pack, or Feature Pack.

#### Sites {#sites-feature-packs-included}

* Se agregó una propiedad de configuración para permitir la exportación de fragmentos de experiencia directamente a espacios de trabajo que haya definido el usuario en [!DNL Adobe Target]. NPR-29189: revisión para CQ-4249782

#### Forms: servicios de documentos {#forms-document-services-1}

* Added &#39;Auto&#39; setting to `RenderAtClient` in `PDFFormRenderOptions` API for [!DNL Experience Manager Forms] OSGi. NPR-30759: revisión para CQ-4278193

## Adobe Experience Manager 6.5.1.0 {#release-6510}

[!DNL Adobe Experience Manager] 6.5.1.0 es una versión importante que incluye correcciones y mejoras clave para el cliente, de rendimiento, estabilidad y seguridad realizadas desde la disponibilidad general de [!DNL Adobe Experience Manager] 6.5 en *abril de 2019.*[!DNL Experience Manager] Se puede instalar en 6.5.

Algunos aspectos destacados de esta versión del Service Pack son:

* Se habilitó la inclusión de dynamic-UI-state en el seguimiento de eventos como atributos personalizados. 
* Included support for the delivery of 360-degree video assets in [!DNL Dynamic Media] Scene 7.
* Enabled *Japanese Word Wrap* feature via the styles plugin of Rich Text Editor. For more information, see [Configure Japanese word wrap](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### Recursos

* Se ha actualizado la interfaz DAM DMGgateway para que sea compatible con varias partes de S3. NPR-29740: revisión para CQ-4226303
* La previsualización de representaciones genera `Only empty tenantId is currently supported` un error después de actualizar a [!DNL Experience Manager] 6.5. NPR-29986: Revisión para CQ-4272353
* El cuadro de diálogo Eliminar no está visible para permitir la eliminación de trabajos. NPR-29720: revisión para CQ-4271074
* After adding asset title in the properties page, when a user attempts to close the page, [!DNL Experience Manager] opens the properties page again. NPR-29627: revisión para CQ-4264929
* El elemento VersioningTimelineEventProvider debe proporcionar la versión raíz junto con el nodo de tipo nt: versión. Revisión para GRANITE-26063
* Implemented the ability to upload and play 360 spherical videos in [!DNL Experience Manager] DM-Scene7 mode. Revisión para CQ-4265131
* Live Copy recupera un estado incorrecto si se edita el origen. Revisión para CQ-4265451
* Enabled Multi-Site Manager support for [!DNL Experience Manager Assets]. Revisión para CQ-4271453, CQ-4268621, CQ-4257491
* [!DNL Experience Manager] debe mostrar una entrada adicional para la versión actual del recurso en el historial de línea de tiempo, mostrando el último comentario de protección de [!DNL Adobe Asset Link]. Revisión para CQ-4262864
* La línea de tiempo del fragmento de contenido muestra un mensaje de error cuando faltan propiedades. Revisión para CQ-4272560
* Problema con el reproductor de vídeo de Scene7 cuando se expande a pantalla completa. Revisión para CQ-4266700
* ZoomVerticalViewer: los botones de desplazamiento no se deben mostrar si se utiliza un único recurso de imagen. Revisión para CQ-4264795
* La eliminación de un nodo secundario en Live Copy debe desasociar el elemento liveRelationship. Revisión para CQ-4270395
* El esquema de metadatos solo contiene elementos de la configuración global y no contiene los del inquilino activo. El valor de la dirección URL de formPath vuelve al valor predeterminado incluso cuando se cambia. NPR-29945: revisión para CQ-4262898
* Publish image presets to [!DNL Brand Portal] fails with 500 error code. NPR-29510: revisión para CQ-4268659

### Sitios

* Las propiedades vacías y varias propiedades no se propagan desde el modelo durante el lanzamiento. El restablecimiento de Live Copy con un plano técnico no funciona en los componentes. NPR-29253: revisión para CQ-4264928, CQ-4264926, CQ-4267722
* CoralUI, when used with `Multifield`, stores the `fileReferenceParameter` at the component level instead of multifield level. NPR-29537: revisión para CQ-4266129
* Enhancement of [!DNL Experience Manager] text component and Text Editor to Japanese. NPR-29785: revisión para CQ-4265090
* La página restaurada con Deformación de tiempo debe hacer referencia a la imagen correcta en el momento de controlar las versiones. NPR-29431: revisión para CQ-4262638
* Problema con la herencia de los nodos del sistema de estilo de principal a secundario. NPR-29516: revisión para CQ-4270330
* An error message while setting up the social posting to [!DNL Facebook] authentication. NPR-29211: revisión para CQ-4266630
* La miniatura representada en el fragmento de contenido muestra una representación interna del calendario para los campos de fecha y hora. NPR-29531: revisión para CQ-4269362
* Al abrir la ficha Permisos en la implementación de Coral2 no se muestran los botones. Revisión para CQ-4269419

### Comercio

* ConstraintViolationException, cuando se ejecuta la migración de contenido diferido para el comercio electrónico. NPR-29247: revisión para CQ-4264383

### Administración de fragmentos de contenido

* Parsing error when opening a Content Fragment which has characters dollar `($)` and open brace `({)`. Revisión para CQ-4270266

### Fragmentos de experiencias

* Exportar fragmentos [!DNL Experience Manager] de experiencias a [!DNL Adobe Target]. Revisión para CQ-4265469
* La exportación de fragmentos de experiencia a destinatario falla con la imagen inteligente. Revisión para CQ-4269606

* El usuario llega a un callejón sin salida cuando intenta mover los fragmentos de experiencia a través de la omnibúsqueda de la vista de tarjeta. Revisión para CQ-4263848

### WCM: editor de páginas

* Se ha reflejado el proceso de ejecución de scripts en sitios múltiples al utilizar un selector no válido. Revisión para CQ-4270397

### Replicación

* Los datos que proporcionó el usuario no se evitan en la salida del componente `cq/replication/components/agent`, lo que provoca una vulnerabilidad en la ejecución almacenada de scripts en sitios múltiples (XSS). Revisión para CQ-4266263

### Flujo de trabajo

* Campo del selector de calendario del participante en el cuadro de diálogo dañado. NPR-29727: revisión para CQ-4270423

### WCM: editor de aplicaciones de página única (SPA)

* Se habilitó la captura de contenido preprocesado desde un extremo remoto. Revisión para CQ-4270238
* Advertencias en los registros al abrir una página de plantilla de SPA representada del lado del servidor. Revisión para CQ-4270238

### WCM: administrador de varios sitios (MSM)

* Upgrade to [!DNL Experience Manager] 6.4.3 makes Multi-Site Manager take a long time to roll out. Revisión para CQ-4271410

### Integración

* Error de conexión en las credenciales de BrightEdge. NPR-29168: revisión para CQ-4265872

* An exception message is displayed when trying to edit and save the [!DNL Experience Manager] launch configuration. NPR-29176: revisión para CQ-4265782/CQ-4266153

### Interfaz de usuario

* Se agregó la compatibilidad para rastrear estados de IU dinámicos como atributos personalizados, mientras se rastrean determinados eventos en la API de seguimiento de base. Revisión para GRANITE-26283
* No se puede establecer la función de seguimiento en el botón de envío. Revisión para GRANITE-26326
* El asistente no puede establecer la función de seguimiento en el botón de envío. NPR-29995, NPR-30025: revisión para CQ-4264289

### Comunidades

* No se pueden alinear los nuevos distintivos en la lista desplegable de la página de perfil del usuario. NPR-29381: revisión para CQ-4267987
* Los visitantes y los miembros que no tengan privilegios de moderador pueden ver las publicaciones pendientes o no aprobadas pegando la dirección URL. NPR-29724: revisión para CQ-4271124, CQ-4271441
* Se observa un tiempo de respuesta alto de hasta 40-50 segundos cuando el usuario inicia sesión en la comunidad. NPR-29677: revisión para CQ-4269444

### Replicación

* El componente del agente de replicación es susceptible a una vulnerabilidad que revela información confidencial a usuarios no autorizados. NPR-29611: revisión para GRANITE-25070

* Se cierra la sesión durante el proceso de OAuth en cada replicación a [!DNL Brand Portal]. NPR-30001: revisión para GRANITE-26196

### Proyectos

* Publish [!DNL Experience Manager Assets] from [!DNL Experience Manager] Author /content/dam/mac folder to [!DNL Brand Portal] doesn&#39;t work. NPR-29819: revisión para CQ-4271118

### Plataforma

* HtmlLibraryManager elimina todo el contenido de crx-quickstart cuando se invalida la caché. NPR-29863: revisión para GRANITE-26197

### Felix

* Los detalles de uso de memoria no se muestran en la consola del sistema al utilizar Java11\. NPR-29669

### Forms

The key highlights for [!DNL Experience Manager Forms] 6.5.1.0 are:

* OSGi only: Added a new attribute `PAGECOUNT` in Output and Forms Service.

* Sólo OSGI: Se ha habilitado la compatibilidad para crear archivos PDF estáticos mediante Forms Service.
* Permisos activados en XMLForm.exe para usuarios raíz y administradores.
* Se habilitó la compatibilidad con ADFS v3.0 para la integración local de Dynamics.

#### Paquete de complemento de Forms

**Integración de back-end**

* Error al recuperar el lenguaje de definición del servicio web protegido (WSDL). NPR-29944: revisión para CQ-4270777
* When [!DNL Experience Manager Forms]  is installed on IBM WebSphere, creating a form data model based on SOAP fails. Revisión para CQ-4251134
* Se habilitó la compatibilidad con los servicios de federación de Active Directory (ADFS) v3.0 para la integración local de Microsoft Dynamics. Revisión para CQ-4270586
* Cuando se cambia el título de un origen de datos, el modelo de datos de formulario no muestra el título actualizado. Revisión para CQ-4265599
* Si el nombre de una entidad o atributo contiene guiones o espacio, las expresiones no pueden evaluar dichas entidades y atributos. Revisión para CQ-4225129

* Se observa una salida incorrecta cuando hay dos puntos en la salida de cadena primitiva. Revisión para CQ-4260825

* Incluso cuando no se espera contenido del resultado de la API de REST, la operación de invocación del modelo de datos de formulario genera un error. Revisión para CQ-4268828

**Formularios adaptables**

* No se puede agregar una nueva instancia en el fragmento del formulario adaptable durante la carga diferida. NPR-29818: revisión para CQ-4269875
* El componente de verificación no registra ni muestra ningún error en las plantillas del documento de registro. Revisión para CQ-4272999
* Se agregó la compatibilidad para deshabilitar el editor de diseño para formularios adaptables. Revisión para CQ-4270810
* Restored the verify step for Adaptive Forms in [!DNL Experience Manager] 6.5. Hotfix for CQ-4269583

* Adaptive Form field validation failure breaks [!DNL Adobe Sign]. Revisión para CQ-4269463
* When an [!DNL Experience Manager Forms] instance has more than 20 adaptive form fragments and name of all the form fragments starts with the same string, the search returns no or only recent 20 created fragments. Revisión para CQ-4264414, CQ-4264914

* Problemas de rendimiento cuando la aplicación de formularios adaptables se utiliza con conjuntos de datos grandes. . Revisión para CQ-4235310

* Cuando se accede a través de una cuenta anónima en una instancia de publicación, la secuencia de comandos de GuideRuntime no se carga. Revisión para CQ-4268679

**Forms: comunicación interactiva**

* La plantilla de comunicación interactiva no enumera los componentes del encabezado y pie de página en la lista de componentes permitidos. Revisión para CQ-4237895
* Cuando se crea una plantilla de impresión de comunicación interactiva que contiene un campo de imagen, el título del gráfico se define en blanco. Revisión para CQ-4264772
* Color de línea de un gráfico que, al eliminarse, se establece como no definido. Revisión para CQ-4264762
* Los cambios realizados en la capa de diseño en el fragmento de Documento desaparecen al realizar los cambios para mantener la sincronización. Revisión para CQ-4266054
* El elemento del modelo de datos de formulario de un fragmento de documento vinculado a un campo de texto no muestra el icono de herencia y permite el enlace. Revisión para CQ-4261089
* La API de procesamiento del canal de impresión no tiene la opción de pasar datos como parámetro en la API. Revisión para CQ-4263540
* La configuración del agente no está visible, ya que la casilla de verificación Editar por agente se desactiva cuando se cambia el tipo de enlace de fragmento de texto a Ninguno/Objeto del modelo de datos para campo o variable de cadena. Revisión para CQ-4261953
* Al enviar la interfaz de usuario del agente, el archivo json de datos web resultante almacena información para los campos no enlazados con cancelación de herencia. Revisión para CQ-4265621

**Forms: flujo de trabajo**

* Cuando se vuelve a enviar un formulario desde la bandeja de salida de la aplicación de formularios adaptables, se pierden datos. NPR-28345: revisión para CQ-4260929
* Los documentos no se cierran mientras se guardan en casos no variables. Revisión para CQ-4269784
* La aplicación de formularios adaptables ha dejado de ser compatible con Microsoft Windows 8.1. Revisión para CQ-4265274
* When an image of more than 2 MB is attached as a field level attachment to a form in the Android version of [!DNL Experience Manager Forms] app, the app crashes. Revisión para CQ-4265578

* Se habilitaron las opciones de rellenado previo del canal de impresión de comunicación interactiva en la tarea de asignación. Revisión para CQ-4265577
* Los usuarios no pueden ver una tarea compartida hasta que pasan a ser miembros del grupo al que se asigna esa tarea. Revisión para CQ-4248733
* La opción para guardar o enviar aplicaciones JEE en la aplicación de formulario adaptable está bloqueada en Windows. Revisión para CQ-4268704
* El modelo de datos de formulario asociado con la variable del modelo de datos de formulario no está visible. Revisión para CQ-4266554
* No se admite la variable de estado de la firma de documentos mediante la compatibilidad con variables. Revisión para CQ-4266312
* Los envíos desde el espacio de trabajo producen errores con caracteres que tengan diéresis. Revisión para CQ-4263172
* En una configuración actualizada, si el flujo de trabajo se abre para la edición, se muestra un error en lugar del nombre del flujo de trabajo en la interfaz de usuario de la carpeta de inspección (IU). Revisión para CQ-4238579

**Forms: administración**

* Cuando se carga una extensión que no sea xsd o schema.json, la carga no se produce y no se genera ningún mensaje de error. Revisión para CQ-4266716

**Forms: administración de correspondencia**

* [!DNL Experience Manager Forms] 6.5 Crear interfaz de usuario de correspondencia (IU de CCR) no puede abrir la correspondencia creada con [!DNL Experience Manager Forms] 6.3. Revisión para CQ-4266392
* La función Sumar en XDP no funciona si el tipo de datos de DDE es de tipo número. Revisión para CQ-4227403
* Se va a actualizar la lógica de invalidación de letras en memoria de la caché, porque cuando se publica un recurso no se actualiza la hora de la última modificación. Revisión para CQ-4250465
* No se puede publicar un fragmento de documento, DD y letras. Revisión para CQ-4272893

#### Instalador JEE de Forms

**Generador de PDF**

* La conversión de archivos CAD a PDF ha producido un error con JDK de 64 bits. NPR-29924, NPR-29925: revisión para CQ-4272113
* Se reemplazó el nombre de PhantomJS a WebToPDF para la conversión de HTMLtoPDF. NPR-29933: revisión para CQ-4234545
* Se genera un error al convertir el archivo zip a PDF. Revisión para CQ-4268628

**Forms: Designer**

* When a full accessibility check is performed on the static PDF created using [!DNL Experience Manager Forms Designer], the Primary Language check fails due to missing language attribute. Revisión para CQ-4272923, CQ-4271002

**Forms: seguridad de documentos**

* La firma digital con módulo de seguridad de hardware (HSM) no funciona en OSGi Linux en Java 11 y Java 8\. NPR-29838: revisión para CQ-4270441
* La firma digital con el módulo de seguridad de hardware (HSM) no funciona en JEE Linux ni en ninguno de los servidores de aplicaciones compatibles, como JBoss y Websphere. NPR-29839: revisión para CQ-4266721
* La comprobación de firmas en un PDF mediante firma electrónica avanzada en formato PDF (PAdES) genera la excepción InvalidOperationException. NPR-29842: revisión para CQ-4244837
* Se agregó la compatibilidad de Document Security Extension con Office 2019\. Revisión para CQ-4254369, CQ-4259764

**Forms: servicios de documentos**

* PDF no puede convertir a PDF/A-1b con campo Formulario no tiene sentencia de apariencia. NPR-29940: revisión para CQ-4269618

* OSGi: No se puede determinar el número de páginas generadas durante el procesamiento. NPR-28922: revisión para CQ-4270870
* Se ha habilitado la compatibilidad con archivos PDF estáticos mediante Forms Service en [!DNL Experience Manager Forms OSGi]. NPR-28572: revisión para CQ-4270869
* No se pueden cambiar los permisos en el archivo XMLForm.exe. NPR-29828, NPR-29237: revisión para el T-4267080
* The static PDF created by the [!DNL Experience Manager Forms] server’s output module does not populate the language attribute/tag with the language of the document created. NPR-27332: revisión para CQ-4271002

**Forms: base JEE**

* Pdfg_srt no está disponible en los artefactos finales y provoca errores en el instalador. NPR-29854: revisión para CQ-4270137
* LCBackupMode.sh no funciona. NPR-29840: revisión para CQ-4269424
* La referencia del puerto UDP debe eliminarse de la interfaz de usuario (IU) para WebSphere. Revisión para CQ-4264782

### Paquetes de funciones incluidos

#### Recursos: incluidos

* Enabled Multi-Site Manager support for [!DNL Experience Manager Assets]. For more information, see [Reuse assets using MSM for Experience Manager Assets](https://helpx.adobe.com/experience-manager/6-5/help/assets/reuse-assets-using-msm.html). NPR-29199: revisión para CQ-4259922

#### Sitios: incluidos

* Exportar fragmentos [!DNL Experience Manager] de experiencias a [!DNL Adobe Target]. For more details, see [The Experience Fragment Link Rewriter Provider - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). Revisión para CQ-4265469

#### Forms: servicios de documentos - Incluido

* Solo OSGi: Se Añadió un nuevo atributo PAGECOUNT en Output y Forms Service. NPR-28922: revisión para CQ-4270870
* Solo OSGi: Se ha habilitado la compatibilidad para crear archivos PDF estáticos mediante Forms Service. NPR-28572: revisión para CQ-4270869
* Permisos activados en XMLForm.exe para usuarios raíz y administradores. NPR-29237: revisión para CQ-4267080

### Paquetes de contenido y paquetes OSGi

The following text documents list the OSGi bundles and Content Packages included in [!DNL Experience Manager] 6.5.1.0

List of OSGi bundles included in [!DNL Experience Manager] 6.5.1.0

[Obtener archivo](assets/6_5-bundle-list.txt)

List of Content Packages included in [!DNL Experience Manager] 6.5.1.0

[Obtener archivo](assets/6_5-content-package-list.txt)
