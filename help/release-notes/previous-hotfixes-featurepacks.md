---
title: Notas de la versión de Service Pack de AEM 6.5
description: Notas de versión específicas de Service Pack 3 de Adobe Experience Manager 6.5.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: 95d9ed8a0ccfa7651b83058d337511dd6b15665f

---


# Revisiones y paquetes de funciones incluidos en instancias de Service Pack anteriores {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## AEM 6.5.2.0

AEM 6.5.2.0 is an important release that includes performance, stability, security, and key customer fixes and enhancements released since the general availability of AEM 6.5 in **April 2019**. Se puede instalar en AEM 6.5.

Algunos aspectos destacados de esta versión del Service Pack son:

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.10.3.
* Se agregó una propiedad de configuración para permitir la exportación de fragmentos de experiencia directamente a espacios de trabajo que haya definido el usuario en Adobe Target.
* Los usuarios de recursos pueden buscar imágenes visualmente similares. AEM muestra las imágenes etiquetadas inteligentes del repositorio de DAM similares a una imagen que seleccionó el usuario. Consulte [Búsqueda visual](../assets/search-assets.md#visualsearch).

* Se mejoró la funcionalidad de los recursos conectados para añadir la compatibilidad con la recuperación de documentos desde implementaciones de DAM remotas. Los autores del sitio pueden buscar y filtrar los tipos de documentos admitidos en el Buscador de contenido. Los documentos remotos se pueden agregar al componente Descargar en páginas web. Consulte [Uso de activos conectados](../assets/use-assets-across-connected-assets-instances.md).

* Mejore los filtros de tipo de documento con más tipos MIME para admitir opciones de varios valores.
* Se ha introducido un flujo de trabajo de reprocesamiento externo para la compatibilidad con varios recursos
* Se ha optimizado el rendimiento de Dynamic Media mediante el uso de filtros de recursos predeterminados para la replicación.
* Se han restaurado las opciones de edición de los recursos de recorte o rotación para DMS7.
* Se ha implementado una opción para silenciar un vídeo durante la carga en VideoPlayer.
* Se ha introducido una corrección para garantizar que la vista de columnas de la IU de recursos muestre solo contenido específico del usuario.
* Se ha introducido una corrección para permitir que los cambios de acordeón de estilo se reflejen en los resultados de búsqueda.

### Recursos {#assets}

**Mejoras del producto**

* Se mejoró la funcionalidad de los recursos conectados para añadir la compatibilidad con la recuperación de documentos desde implementaciones de DAM remotas. Los autores del sitio pueden buscar y filtrar los tipos de documentos admitidos en el Buscador de contenido. Los documentos remotos se pueden agregar al componente Descargar en páginas web. Revisión para CQ-4270245. Consulte [Uso de activos conectados](/help/assets/use-assets-across-connected-assets-instances.md).

* Los usuarios de recursos pueden buscar imágenes visualmente similares. AEM muestra las imágenes etiquetadas inteligentes del repositorio de DAM similares a una imagen que seleccionó el usuario. Consulte [Búsqueda visual](../assets/search-assets.md#visualsearch).

**Correcciones**

* Las rutas de recursos de las direcciones URL y los metadatos de las carpetas que genera la API de ACP no son URL codificadas. GRANITE-26198: revisión para CQ-4271814
* Si se descomprime un archivo con una carpeta que tenga un signo de porcentaje (%) en su nombre no se podrá abrir con la interfaz de recursos. NPR-29989: revisión para CQ-4270467
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
* La función Compartir vínculo no funciona en la instancia de AEM con la configuración de DMS7. NPR-30080, NPR-30492: revisión para CQ-4273651
* Cuando se agrega el componente de Dynamic Media Scene7 a la página y esta se publica, la configuración de dmscene7 no siempre se activa. NPR-30641: revisión para CQ-4275962
* Se agregó un elemento IPSJobJournal en AEM para crear solo un trabajo de sistemas de prevención de intrusiones (IPS) por perfil de procesamiento. NPR-30490: revisión para CQ-4273614
* Medios dinámicos: Se han agregado filtros predeterminados para excluir recursos de la replicación en el nodo de publicación de AEM. NPR-30538: revisión para CQ-4274678
* Se ha introducido un flujo de trabajo de reprocesamiento externo para la compatibilidad con varios recursos a fin de permitir que la carpeta sea una carga útil. El flujo de trabajo consta de dos pasos: vuelve a procesar los recursos sin controladores mediante el mapa de metadatos al paso siguiente y vuelve a cargar todos los recursos sin el control de recursos en S7 en un solo trabajo de IPS. Para obtener más información, consulte la configuración de los servicios de Dynamic Media Cloud. NPR-30489: revisión para CQ-4272903
* Al cargar un archivo CSV incorrecto después de uno correcto, se elimina el archivo CSV correcto. Revisión para CQ-4277694, CQ-4277814
* Se va a eliminar el icono incorrecto específico de las carpetas de contribución. Revisión para CQ-4277580
* Al seleccionar un usuario en el selector de usuarios de la ficha Contribución de recursos, el nombre del usuario no aparece en la tabla y el cuadro de diálogo Eliminar usuario que está en la página Propiedades muestra un texto incorrecto. Revisión para CQ-4277875
* Los colaboradores no se pueden agregar a la carpeta de Contribución de recursos desde el selector de usuarios al seleccionar al usuario y hacer clic en Añadir. Revisión para CQ-4277824, CQ-4278087
* La búsqueda por nombre de usuario en minúsculas no funciona en el selector de usuarios. Revisión para CQ-4277958, CQ-4277930
* Los usuarios que no son administradores pueden publicar recursos en una nueva carpeta que esté en una carpeta de contribución de recursos. Revisión para CQ-4278200
* dam-user (no es administrador) no tiene la opción de añadir colaboradores a la carpeta de contribución de recursos. Revisión para CQ-4278192
* El botón &quot;Crear&quot; está visible en la carpeta de contribución de recursos. Revisión para CQ-4277560
* Al ordenar la consulta de búsqueda por relevancia, se devuelven documentos de InDesign junto con plantillas de InDesign. Revisión para CQ-4273864
* Si el usuario tiene un id. de correo electrónico en mayúsculas, los usuarios no pueden registrar los recursos que ya se han extraído. Revisión para CQ-4276575
* La operación Eliminar solo se aplica a los ajustes preestablecidos seleccionados y, si la pantalla actualiza automáticamente la lista después de la operación, se muestran otros ajustes preestablecidos que ya se han actualizado. Revisión para CQ-4261461
* La configuración de Dynamic Media Cloud Services en modo DMHybrid da como resultado varios grupos de informes vacíos creados en Analytics y sin ningún id. de grupo de informes almacenado en AEM, lo que provoca que los grupos de informes se dupliquen. Revisión para CQ-4249780
* No se puede sincronizar la operación de cambio de nombre en un recurso de AEM que tenga un nombre duplicado en Scene7. Revisión para CQ-4276763
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

### Sitios {#sites-6520}

* Si la herencia de LiveCopy está dañada, las páginas de Live Copy muestran vínculos de copia de idioma en lugar de vínculos de LiveCopy. (NPR-30980)
* Para un nuevo modelo, si el número de registros es superior a 40, solo se muestran los primeros 40 registros. El modelo muestra líneas en blanco para el resto de los registros. (NPR-31182)
* El complemento Editor de texto enriquecido (RTE) del componente de texto muestra caracteres distorsionados para texto en japonés y coreano. (NPR-31331)
* El editor de texto enriquecido (RTE) no permite insertar una tabla incrustada como elemento de lista. (NPR-30879)
* El Editor de texto enriquecido (RTE) de scaffolding de fuera del cuadro se aplica de forma inesperada al tamaño de fuente en línea a los elementos. (NPR-31284)
* Cuando un usuario se centra en los campos del carril izquierdo y utiliza combinaciones de teclas para pegar contenido, pega el contenido del portapapeles del editor de páginas en lugar del contenido copiado de los campos del carril izquierdo. (NPR-31172)
* Cuando un usuario agrega un campo Carga de archivo a un campo múltiple, la ruta de la imagen se almacena en el nodo del componente en lugar del nodo de varios campos. (NPR-30882)
* La API ResponsiveGridExporter no devuelve la interfaz com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter. El paquete com.day.cq.wcm.foundation.model.impl se declara como paquete privado. (NPR-31398)
* Cuando se abre una página que contiene algunos fragmentos de experiencia en modo que no es de editor (ya sea en Autor sin el `editor.html` prefijo y `wcmmode=disabled`o en Editor), la solicitud termina en el código de error de estado HTTP 500. (NPR-30743)

### WCM: editor de páginas {#wcm-page-editor-6520}

**Mejoras del producto**

* Mejore los filtros de tipo de documento con más tipos MIME para admitir opciones de varios valores. Revisión para CQ-4270694

### Administración de fragmentos de contenido {#content-fragment-management-6520}

* La consulta que isa la IU de los modelos de fragmento de contenido es muy lenta y, finalmente, acaba en error. Revisión para CQ-4270807

### IU: bases {#ui-foundation}

* Desencadenador de accesos directos que impide que el usuario utilice &quot;m,&quot; &quot;p,&quot; y &quot;e&quot; en las interfaces de usuario específicas. NPR-30355: revisión para GRANITE-26346
* Cerrar la interfaz de usuario de búsqueda de recursos no restablece el carril izquierdo a la selección de contenido, lo que impide que el usuario abra el carril del filtro por segunda vez posteriormente. NPR-30509: revisión para CQ-4274716
* Entorno de varios inquilinos: la navegación principal de la IU de recursos no está disponible y se produce un error de JavaScript. NPR-30104: revisión para GRANITE-26344

### Traducción {#translation-6520}

* Problema de traducción: solo unos pocos componentes se traducen mediante traducción automática. NPR-30079: revisión para CQ-4273764

### Plataforma {#platform-6520}

* El remitente de correo predeterminado de AEM no puede enviar correo a un servidor SMTP remoto a través de TLS v1.2. NPR-30476: revisión para GRANITE-26605

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
>Service Pack de AEM no incluye correcciones para AEM Forms. Estas se entregan mediante un paquete independiente de complementos de Forms. Asimismo, se ha publicado un instalador acumulativo que incluye correcciones para AEM Forms en JEE. Para obtener más información, consulte [Instalación del complemento de AEM Forms](#install-aem-forms-add-on-package) e [Instalación del instalador JEE de AEM Forms](#forms-jee-installer).

Los aspectos destacados de los formularios de AEM 6.5.2.0 son:

* Se agregó la configuración &quot;Automática&quot; en `RenderAtClient` en la API `PDFFormRenderOptions` para la instancia de OSGi de AEM Forms.

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
* La adición o edición de una conexión de servicio Web invocando servicios Web desde AEM Forms Workbench genera un error: ClassNotFoundException org.apache.axis.message.SOAPBodyElement. NPR-30105: revisión para CQ-4273217

### Paquetes de funciones incluidos {#feature-packs-included}

>[!NOTE]
>
>Para los clientes de AEM Forms, es esencial instalar el paquete de complementos de AEM Forms después de instalar cualquier paquete de servicio, paquete acumulativo o paquete de funciones de AEM.

#### Sitios {#sites-feature-packs-included}

* Se agregó una propiedad de configuración para permitir la exportación de fragmentos de experiencia directamente a espacios de trabajo que haya definido el usuario en Adobe Target. NPR-29189: revisión para CQ-4249782

#### Forms: servicios de documentos {#forms-document-services-1}

* Se agregó la configuración &quot;Automática&quot; en `RenderAtClient` en la API `PDFFormRenderOptions` para la instancia de OSGi de AEM Forms. NPR-30759: revisión para CQ-4278193

## AEM 6.5.1.0 {#release-6510}

AEM 6.5.1.0 is an important release that includes performance, stability, security, and key customer fixes and enhancements released since the general availability of AEM 6.5 in *April 2019.* Se puede instalar en AEM 6.5.

Algunos aspectos destacados de esta versión del Service Pack son:

* Se habilitó la inclusión de dynamic-UI-state en el seguimiento de eventos como atributos personalizados. 
* Se ha incluido la compatibilidad con la entrega de recursos de vídeo de 360 grados en Dynamic Media Scene 7.
* Enabled *Japanese Word Wrap* feature via the styles plugin of Rich Text Editor. For more information, see [Configure Japanese word wrap](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### Recursos

* Se ha actualizado la interfaz DAM DMGgateway para que sea compatible con varias partes de S3. NPR-29740: revisión para CQ-4226303
* La vista previa de las representaciones genera `Only empty tenantId is currently supported` un error después de actualizar a AEM 6.5\. NPR-29986: revisión para CQ-4272353
* El cuadro de diálogo Eliminar no está visible para permitir la eliminación de trabajos. NPR-29720: revisión para CQ-4271074
* Después de añadir el título del recurso en la página de propiedades, cuando un usuario intenta cerrar la página, AEM vuelve a abrir la página de propiedades. NPR-29627: revisión para CQ-4264929
* El elemento VersioningTimelineEventProvider debe proporcionar la versión raíz junto con el nodo de tipo nt: versión. Revisión para GRANITE-26063
* Se ha implementado la capacidad de cargar y reproducir vídeos de 360 grados en el modo DM-Scene7 de AEM. Revisión para CQ-4265131
* Live Copy recupera un estado incorrecto si se edita el origen. Revisión para CQ-4265451
* Se habilitó la compatibilidad con el administrador de varios sitios para los recursos. Revisión para CQ-4271453, CQ-4268621, CQ-4257491
* La interfaz de AEM debe mostrar una entrada adicional para la versión actual del recurso en el historial de línea de tiempo, mostrando así el último comentario de registro de Adobe Asset Link. Revisión para CQ-4262864
* La línea de tiempo del fragmento de contenido muestra un mensaje de error cuando faltan propiedades. Revisión para CQ-4272560
* Problema con el reproductor de vídeo de Scene7 cuando se expande a pantalla completa. Revisión para CQ-4266700
* ZoomVerticalViewer: los botones de desplazamiento no se deben mostrar si se utiliza un único recurso de imagen. Revisión para CQ-4264795
* La eliminación de un nodo secundario en Live Copy debe desasociar el elemento liveRelationship. Revisión para CQ-4270395
* El esquema de metadatos solo contiene elementos de la configuración global y no contiene los del inquilino activo. El valor de la dirección URL de formPath vuelve al valor predeterminado incluso cuando se cambia. NPR-29945: revisión para CQ-4262898
* La publicación de ajustes preestablecidos de imagen en Brand Portal devolvió un error con el código 500. NPR-29510: revisión para CQ-4268659

### Sitios

* Las propiedades vacías y varias propiedades no se propagan desde el modelo durante el lanzamiento. El restablecimiento de Live Copy con un plano técnico no funciona en los componentes. NPR-29253: revisión para CQ-4264928, CQ-4264926, CQ-4267722
* CoralUI, when used with `Multifield`, stores the `fileReferenceParameter` at the component level instead of multifield level. NPR-29537: revisión para CQ-4266129
* Mejora del componente de texto de AEM y del Editor de texto al japonés. NPR-29785: revisión para CQ-4265090
* La página restaurada con Deformación de tiempo debe hacer referencia a la imagen correcta en el momento de controlar las versiones. NPR-29431: revisión para CQ-4262638
* Problema con la herencia de los nodos del sistema de estilo de principal a secundario. NPR-29516: revisión para CQ-4270330
* Mensaje de error al configurar la publicación social para la autenticación de Facebook. NPR-29211: revisión para CQ-4266630
* La miniatura representada en el fragmento de contenido muestra una representación interna del calendario para los campos de fecha y hora. NPR-29531: revisión para CQ-4269362
* Al abrir la ficha Permisos en la implementación de Coral2 no se muestran los botones. Revisión para CQ-4269419

### Comercio

* ConstraintViolationException, cuando se ejecuta la migración de contenido diferido para el comercio electrónico. NPR-29247: revisión para CQ-4264383

### Administración de fragmentos de contenido

* Parsing error when opening a Content Fragment which has characters dollar `($)` and open brace `({)`. Revisión para CQ-4270266

### Fragmentos de experiencias

* Exportar fragmentos de experiencias de AEM a Adobe Target. Revisión para CQ-4265469
* La exportación de fragmentos de experiencia a destino falla con la imagen inteligente. Revisión para CQ-4269606

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

* La actualización a AEM 6.4.3 hace que el administrador de varios sitios tarde mucho en implementarse. Revisión para CQ-4271410

### Integración

* Error de conexión en las credenciales de BrightEdge. NPR-29168: revisión para CQ-4265872

* Aparece un mensaje de excepción al intentar editar y guardar la configuración de inicio de AEM. NPR-29176: revisión para CQ-4265782/CQ-4266153

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

* Se cierra la sesión durante el proceso de OAuth en cada replicación a Brand portal. NPR-30001: revisión para GRANITE-26196

### Proyectos

* La publicación de recursos de la carpeta de AEM Author /content/dam/mac en Brand Portal no funciona. NPR-29819: revisión para CQ-4271118

### Plataforma

* HtmlLibraryManager elimina todo el contenido de crx-quickstart cuando se invalida la caché. NPR-29863: revisión para GRANITE-26197

### Felix

* Los detalles de uso de memoria no se muestran en la consola del sistema al utilizar Java11\. NPR-29669

### Forms

Los aspectos destacados de los formularios de AEM 6.5.1.0 son:

* OSGi only: Added a new attribute `PAGECOUNT` in Output and Forms Service.

* Sólo OSGI: Se ha habilitado la compatibilidad para crear archivos PDF estáticos mediante Forms Service.
* Permisos activados en XMLForm.exe para usuarios raíz y administradores.
* Se habilitó la compatibilidad con ADFS v3.0 para la integración local de Dynamics.

#### Paquete de complemento de Forms

**Integración de back-end**

* Error al recuperar el lenguaje de definición del servicio web protegido (WSDL). NPR-29944: revisión para CQ-4270777
* Cuando AEM Forms se instala en IBM WebSphere, se produce un error al crear un modelo de datos de formulario basado en SOAP. Revisión para CQ-4251134
* Se habilitó la compatibilidad con los servicios de federación de Active Directory (ADFS) v3.0 para la integración local de Microsoft Dynamics. Revisión para CQ-4270586
* Cuando se cambia el título de un origen de datos, el modelo de datos de formulario no muestra el título actualizado. Revisión para CQ-4265599
* Si el nombre de una entidad o atributo contiene guiones o espacio, las expresiones no pueden evaluar dichas entidades y atributos. Revisión para CQ-4225129

* Se observa una salida incorrecta cuando hay dos puntos en la salida de cadena primitiva. Revisión para CQ-4260825

* Incluso cuando no se espera contenido del resultado de la API de REST, la operación de invocación del modelo de datos de formulario genera un error. Revisión para CQ-4268828

**Formularios adaptables**

* No se puede agregar una nueva instancia en el fragmento del formulario adaptable durante la carga diferida. NPR-29818: revisión para CQ-4269875
* El componente de verificación no registra ni muestra ningún error en las plantillas del documento de registro. Revisión para CQ-4272999
* Se agregó la compatibilidad para deshabilitar el editor de diseño para formularios adaptables. Revisión para CQ-4270810
* Se ha restaurado el paso de verificación de formularios adaptables en AEM 6.5\. Revisión para CQ-4269583

* El error de validación del campo Formulario adaptable interrumpe Adobe Sign. Revisión para CQ-4269463
* Cuando una instancia de AEM Forms tiene más de 20 fragmentos de formulario adaptables y el nombre de todos los fragmentos de formulario comienza con la misma cadena, la búsqueda no devuelve fragmentos o solo devuelve los 20 fragmentos creados recientemente. Revisión para CQ-4264414, CQ-4264914

* Problemas de rendimiento cuando la aplicación de formularios adaptables se utiliza con conjuntos de datos grandes. . Revisión para CQ-4235310

* Cuando se accede a través de una cuenta anónima en una instancia de publicación, la secuencia de comandos de GuideRuntime no se carga. Revisión para CQ-4268679

**Forms: comunicación interactiva**

* La plantilla de comunicación interactiva no enumera los componentes del encabezado y pie de página en la lista de componentes permitidos. Revisión para CQ-4237895
* Cuando se crea una plantilla de impresión de comunicación interactiva que contiene un campo de imagen, el título del gráfico se define en blanco. Revisión para CQ-4264772
* Color de línea de un gráfico que, al eliminarse, se establece como no definido. Revisión para CQ-4264762
* Los cambios realizados en la capa de diseño en el fragmento de documento desaparecen al realizar los cambios para mantener sincronizados. Revisión para CQ-4266054
* El elemento del modelo de datos de formulario de un fragmento de documento vinculado a un campo de texto no muestra el icono de herencia y permite el enlace. Revisión para CQ-4261089
* La API de procesamiento del canal de impresión no tiene la opción de pasar datos como parámetro en la API. Revisión para CQ-4263540
* La configuración del agente no está visible, ya que la casilla de verificación Editar por agente se desactiva cuando se cambia el tipo de enlace de fragmento de texto a Ninguno/Objeto del modelo de datos para campo o variable de cadena. Revisión para CQ-4261953
* Al enviar la interfaz de usuario del agente, el archivo json de datos web resultante almacena información para los campos no enlazados con cancelación de herencia. Revisión para CQ-4265621

**Forms: flujo de trabajo**

* Cuando se vuelve a enviar un formulario desde la bandeja de salida de la aplicación de formularios adaptables, se pierden datos. NPR-28345: revisión para CQ-4260929
* Los documentos no se cierran mientras se guardan en casos no variables. Revisión para CQ-4269784
* La aplicación de formularios adaptables ha dejado de ser compatible con Microsoft Windows 8.1\. Revisión para CQ-4265274
* Cuando se adjunta una imagen de más de 2 MB como datos adjuntos a un formulario en la versión de Android de la aplicación de AEM Forms, la aplicación se bloquea. Revisión para CQ-4265578

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

* La IU para crear correspondencia de AEM 6.5 Forms (IU de CCR) no puede abrir la correspondencia creada con AEM 6.3 Forms. Revisión para CQ-4266392
* La función Sumar en XDP no funciona si el tipo de datos de DDE es de tipo número. Revisión para CQ-4227403
* Se va a actualizar la lógica de invalidación de letras en memoria de la caché, porque cuando se publica un recurso no se actualiza la hora de la última modificación. Revisión para CQ-4250465
* No se puede publicar un fragmento de documento, DD y letras. Revisión para CQ-4272893

#### Instalador JEE de Forms

**Generador de PDF**

* La conversión de archivos CAD a PDF ha producido un error con JDK de 64 bits. NPR-29924, NPR-29925: revisión para CQ-4272113
* Se reemplazó el nombre de PhantomJS a WebToPDF para la conversión de HTMLtoPDF. NPR-29933: revisión para CQ-4234545
* Se genera un error al convertir el archivo zip a PDF. Revisión para CQ-4268628

**Forms: Designer**

* Cuando se realiza una comprobación de accesibilidad completa en el PDF estático creado con AEM Form Designer, la comprobación de idioma principal crea un error debido a la ausencia del atributo de idioma. Revisión para CQ-4272923, CQ-4271002

**Forms: seguridad de documentos**

* La firma digital con módulo de seguridad de hardware (HSM) no funciona en OSGi Linux en Java 11 y Java 8\. NPR-29838: revisión para CQ-4270441
* La firma digital con el módulo de seguridad de hardware (HSM) no funciona en JEE Linux ni en ninguno de los servidores de aplicaciones compatibles, como JBoss y Websphere. NPR-29839: revisión para CQ-4266721
* La comprobación de firmas en un PDF mediante firma electrónica avanzada en formato PDF (PAdES) genera la excepción InvalidOperationException. NPR-29842: revisión para CQ-4244837
* Se agregó la compatibilidad de Document Security Extension con Office 2019\. Revisión para CQ-4254369, CQ-4259764

**Forms: servicios de documentos**

* PDF no puede convertir a PDF/A-1b con campo Formulario no tiene sentencia de apariencia. NPR-29940: revisión para CQ-4269618

* OSGi: No se puede determinar el número de páginas generadas durante el procesamiento. NPR-28922: revisión para CQ-4270870
* Se ha habilitado la compatibilidad con archivos PDF estáticos mediante Forms Service en OSGi de AEM Forms. NPR-28572: revisión para CQ-4270869
* No se pueden cambiar los permisos en el archivo XMLForm.exe. NPR-29828, NPR-29237: revisión para el T-4267080
* El PDF estático que creó el módulo de salida del servidor de AEM Forms no rellena el atributo o etiqueta de idioma con el idioma del documento creado. NPR-27332: revisión para CQ-4271002

**Forms: base JEE**

* Pdfg_srt no está disponible en los artefactos finales y provoca errores en el instalador. NPR-29854: revisión para CQ-4270137
* LCBackupMode.sh no funciona. NPR-29840: revisión para CQ-4269424
* La referencia del puerto UDP debe eliminarse de la interfaz de usuario (IU) para WebSphere. Revisión para CQ-4264782

### Paquetes de funciones incluidos

#### Recursos - Incluido

* Se habilitó la compatibilidad con el administrador de varios sitios para los recursos. For more information, see [Reuse assets using MSM for Assets](https://helpx.adobe.com/experience-manager/6-5/help/assets/reuse-assets-using-msm.html). NPR-29199: revisión para CQ-4259922

#### Sitios: incluidos

* Exportar fragmentos de experiencias de AEM a Adobe Target. For more details, see [The Experience Fragment Link Rewriter Provider - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). Revisión para CQ-4265469

#### Forms: servicios de documentos - Incluido

* Solo OSGi: Se ha agregado un nuevo atributo PAGECOUNT en Output y Forms Service. NPR-28922: revisión para CQ-4270870
* Solo OSGi: Se ha habilitado la compatibilidad para crear archivos PDF estáticos mediante Forms Service. NPR-28572: revisión para CQ-4270869
* Permisos activados en XMLForm.exe para usuarios raíz y administradores. NPR-29237: revisión para CQ-4267080

### Paquetes de contenido y paquetes OSGi

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en AEM 6.5.1.0

Lista de paquetes OSGi incluidos en AEM 6.5.1.0

[Obtener archivo](assets/6_5-bundle-list.txt)

Lista de paquetes de contenido incluidos en AEM 6.5.1.0

[Obtener archivo](assets/6_5-content-package-list.txt)
