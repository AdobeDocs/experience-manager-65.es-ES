---
title: '[!DNL Adobe Experience Manager] 6.5 Notas de la versión anterior de Service Pack.'
description: Notas de la versión de los Service Packs [!DNL Adobe Experience Manager] 6.5.
contentOwner: AK
translation-type: tm+mt
source-git-commit: 544d99921a3b487bf8ae64111a8568f8f02fcd03
workflow-type: tm+mt
source-wordcount: '14953'
ht-degree: 20%

---


# Revisiones y paquetes de funciones incluidos en instancias de Service Pack anteriores {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## [!DNL Adobe Experience Manager] 6.5.6.0  {#experience-manager-6560}

Adobe Experience Manager 6.5.6.0 es una actualización importante que incluye nuevas funciones, mejoras clave solicitadas por los clientes y mejoras en el rendimiento, la estabilidad y la seguridad, que se publican desde la disponibilidad general de la versión 6.5 en **abril de 2019**. Se puede instalar sobre Adobe Experience Manager 6.5.

Las principales funciones y mejoras introducidas en Adobe Experience Manager 6.5.6.0 incluyen:

* Publique o cancele la publicación de recursos de forma selectiva en [!DNL Experience Manager] o [!DNL Dynamic Media] mediante [!UICONTROL Asistente para publicación rápida] o [!UICONTROL Administrar publicación].

* Utilice la interfaz de usuario [!DNL Dynamic Media] para invalidar el contenido en caché de la red de Envío de contenido (CDN).

* La publicación de las carpetas de contribución de recursos desde Brand Portal a Recursos Experience Manager ahora también se admite a través del servidor proxy.

* Los grupos autogenerados de carpetas privadas ahora se limpian al eliminar la carpeta privada en [!DNL Experience Manager Assets].

* Las descripciones de los modificadores en el editor de ajustes preestablecidos [!UICONTROL Viewer] de vídeo se han actualizado en [!DNL Dynamic Media].

* Se proporciona una nueva configuración de compañía para reflejar el estado del conector [!DNL Dynamic Media].

* Las opciones predeterminadas para `test` y `aiprocess` se actualizan a `Thumbnail`, desde `Rasterize` anteriormente en Dynamic Media, para asegurarse de que los usuarios necesitan crear solo miniaturas y omitir la extracción de página y la extracción de palabras clave.

* [Rellene previamente un formulario adaptable en el cliente](../../help/forms/using/prepopulate-adaptive-form-fields.md#prefill-at-client).

* [Integración del modelo de datos de formulario con las API de RESTful en un servidor con implementación](../../help/forms/using/configure-data-sources.md) SSL bidireccional.

* [Se mejoró el almacenamiento en caché para páginas](../../help/forms/using/configure-adaptive-forms-cache.md) de formularios adaptables traducidas.

* Compatibilidad con [Etiquetas de texto de Adobe Sign en el servicio de Automated forms conversion](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html).

* Compatibilidad con [convertir formularios coloreados en formularios adaptables](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html) mediante [!DNL Automated Forms Conversion service].

* Compatibilidad con los protocolos SMB 2 y SMB 3.

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.22.4.

Para obtener una lista completa de las funciones y mejoras introducidas en Experience Manager 6.5.6.0, consulte [Novedades de Adobe Experience Manager 6.5 Service Pack 6](new-features-latest-service-pack.md).

La siguiente es la lista de correcciones que se proporciona en la versión [!DNL Experience Manager] 6.5.6.0.

### [!DNL Sites] {#sites-6560}

* En [!DNL Sites] o [!DNL Screens], seleccione un proyecto y haga clic en [!UICONTROL Publicaciones de administración]. Los usuarios no pueden avanzar en el asistente para [!UICONTROL Administrar publicación] debido a errores en la interfaz de usuario. Específicamente, la opción [!UICONTROL Publicar] no funciona (NPR-34099).
* La posición de iParsys (Sistema de párrafos heredado) no se vuelve a su posición predeterminada original después de anular la selección de las opciones [!UICONTROL Cancelar herencia] o [!UICONTROL Deshabilitar herencia] (NPR-34097).
* Si el `RolloutConfigManagerFactoryImpl` no puede cargar una configuración de implementación, no intenta cargar las configuraciones que faltan. Devuelve las configuraciones almacenadas en caché (NPR-34092).
* En el componente de núcleo de texto, después de utilizar la opción de edición HTML de origen, se elimina la clase de la etiqueta `em` (NPR-34081).
* Después de actualizar de Experience Manager 6.3.3 a Experience Manager 6.5.3, el proceso de implementación tarda mucho más y la implementación falla con un error de tiempo de espera (NPR-34049).
* El `htmlwriter` no codifica los valores de atributo. El marcado que está presente en el marcado XF se exporta con valores de atributos descodificados (concretamente `"` en lugar de `&#34`). Provoca problemas en el lado del Destinatario con el Compositor de experiencias visuales que utiliza el XF exportado (NPR-34048).
* Al mover páginas en [!DNL Experience Manager Sites], mejore el registro para capturar el error de creación de versiones con el motivo (NPR-34014).
* En [!DNL Rich Text Editor] si se elimina todo el texto, la etiqueta de párrafo también se elimina (NPR-33976).
* Cuando se abre o actualiza la página `siteadmin` (en la IU clásica), las opciones del menú `New` se desactivan (NPR-33949).

   ![Captura de pantalla que ilustra el problema de falta de menú en la IU clásica](assets/33949_missing_menu.png)

* Un [!DNL Content Fragment] no se puede usar como `TemplatedResource` porque falla en `ContentFragmentUsePojo` (NPR-33911).
* Las operaciones de movimiento sincrónico y asíncrono pueden provocar errores debido a transferencias simultáneas. Las operaciones de movimiento de página están restringidas sólo al movimiento asincrónico. Evita el movimiento simultáneo de páginas (NPR-33875).
* [!UICONTROL La operación Administrar ] publicación para replicar contenido de la instancia Autor a Publicación falla y genera un error de JavaScript (NPR-33872).
* Cuando se seleccionan varias páginas o recursos para crear versiones, la nueva versión se crea solo para la última página o recurso seleccionado (NPR-33866).
* Mueva una página de modelo con copias en vivo a otra carpeta. Al moverlo a la carpeta original, la operación de movimiento falla sin ningún error (NPR-33864).
* Cuando se utiliza la acción de mover para cambiar el nombre de una página Web en la consola [!DNL Sites], se muestran dos cuadros de diálogo superpuestos en el último paso del asistente (NPR-33831).

   ![Captura de pantalla que ilustra el problema del NPR-33831 con el diálogo de movimiento superpuesto](assets/33831_rename_dialog.png)

* Las propiedades `cq:acLinks` y `cq:acUUID` de [!DNL Adobe Campaign] de la copia se eliminan durante la operación de copiar y pegar (NPR-33794).
* Al intentar un despliegue en una página secundaria de una Live Copy principal independiente, [!DNL Experience Manager] genera una excepción de puntero nulo (NPR-33676).
* Los componentes [!DNL RTE] de un contenedor de diseño no están visibles cuando el contenedor de diseño se copia y se vuelve a pegar en la página. Los componentes [!DNL RTE] no son editables, pero se muestran al actualizar la página (NPR-33662).
* Al cambiar el tamaño de un componente de diseño para diferentes puntos de interrupción (medio y grande), el diseño no se comporta como se espera (NPR-33608).
* En el modo de edición en línea de [!DNL RTE], arrastrar una imagen no funciona para el componente Texto (NPR-33602).
* Es posible crear un componente en una página de modelo con el mismo nombre que el nombre de la página. Durante la implementación, `_msm_moved` se sustituye para cambiar el nombre del componente. El componente se mueve al final del [!UICONTROL Sistema de párrafos] (NPR-33535).
* Cuando offTime o onTime están configurados en muchas páginas o recursos, consumen muchos recursos y ralentizan el sistema durante el inicio y el cierre (NPR-33482).
* Un usuario con permisos CRUD en `/content/experience-fragment` no puede eliminar una carpeta (NPR-33436).
* Puede seleccionar [!UICONTROL HTML y JSON] como opción para [!UICONTROL formato de exportación de Adobe Target] en una carpeta principal de la sección [!DNL Experience Fragments]. Las mismas propiedades se muestran en la IU táctil para las subcarpetas de esta carpeta principal. Sin embargo, en CRXDE, para `cq:adobeTargetExportFormat`, solo muestra HTML en lugar de mostrar `html,json` (NPR-33423).
* No se admite Publicar o Cancelar la publicación desde un alias de página. Elimine la opción que parece indicar lo contrario (NPR-33415).
* Una etiqueta específica se puede mover de una ubicación a otra en [!DNL Experience Manager]. También se puede aplicar a diferentes páginas antes y después de moverse. Al editar las propiedades de las páginas, la etiqueta no se muestra para su edición aunque la etiqueta sea la misma (NPR-33353).
* Una plantilla de página no se representa correctamente cuando se elimina un contenedor de diseño de una plantilla que contiene varios contenedores de diseño (NPR-33347).
* En el editor de plantillas, intente eliminar una plantilla que se utilice en más de 100000 páginas en `/content/`. Se muestra un error sin ningún mensaje de error (NPR-33312).
* El redireccionamiento a la página [!DNL Experience Manager] con anclaje no funciona en la instancia de Autor, ya que `PageRedirectServlets` coloca la cadena de consulta después de un fragmento de URL o un anclaje (NPR-34288).
* La creación de una marca en `/content/campaign` resulta en una estructura que no permite crear campañas. [!UICONTROL La opción Crear ] marca deja a la marca recién creada sin capacidad para crear  [!UICONTROL Ofertas y ] actividades, ya que no hay   opción de creación (NPR-34113).
* Puede suspender el [!DNL Live Copy] de una página y la herencia se interrumpe como se ve en el modo Editor. En las propiedades de página, el icono que representa la herencia indica incorrectamente que la herencia existe y no está rota (NPR-34017).
* Las páginas con muchas referencias no se pueden mover asincrónicamente y, en ocasiones, la operación de movimiento falla (CQ-4297969).
* Una página web con el carácter `/` en la dirección URL deja de responder durante la creación. Cuando se agrega un componente durante la creación, aumenta el uso de la CPU y el explorador deja de responder (CQ-4295749).
* En el modo de exploración, NVDA no narra un valor seleccionado en la opción de menú Tipo/Tamaño. El enfoque visual no está en el elemento seleccionado. Los usuarios que dependen de un lector de pantalla no pueden utilizar el modo de exploración (CQ-4294993).
* Al crear una página web, los usuarios pueden seleccionar la plantilla [!UICONTROL Página de contenido]. En la ficha [!UICONTROL Medios sociales], los usuarios seleccionan una [!UICONTROL variación de XF preferida]. Para seleccionar un fragmento de experiencia en el modo de exploración NVDA, los usuarios no pueden utilizar las teclas del teclado (CQ-4292669).
* Se ha actualizado la biblioteca de controladores a la versión 4.7.3 más segura (NPR-34484).
* Varias instancias de secuencias de comandos entre sitios en [!DNL Experience Manager Sites] componentes (NPR-33925).
* El campo del nombre de la carpeta al crear una nueva carpeta es vulnerable a las secuencias de comandos almacenadas entre sitios (GRANITE-30094).
* Los resultados de búsqueda en la página[!UICONTROL  bienvenida] y la plantilla de finalización de ruta son vulnerables a los scripts entre sitios (NPR-33719, NPR-33718).
* La creación de una propiedad binaria en un nodo no estructurado da como resultado secuencias de comandos entre sitios en el cuadro de diálogo de propiedad binaria (NPR-33717).
* Secuencias de comandos entre sitios al utilizar la opción [!UICONTROL Prueba de Control de acceso] en la interfaz CRX DE (NPR-33716).
* Las entradas de usuario no se codifican correctamente para varios componentes al enviar información al cliente (NPR-33695).
* Secuencias de comandos entre sitios en la vista de calendario para la Bandeja de entrada del Experience Manager (NPR-33545).
* Una dirección URL que termina con `childrenlist.html` muestra una página HTML en lugar de una respuesta 404. Estas direcciones URL son vulnerables a los scripts entre sitios (NPR-33441).


### [!DNL Assets] {#assets-6560}

**Mejoras de accesibilidad en Recursos Experience Manager**

* Con las teclas del teclado, los usuarios ahora pueden acceder a las opciones interactivas de la interfaz de usuario y centrarse en ellas en la lista de recursos [!UICONTROL Referencias] (NPR-34115).

* El lector de pantalla ahora anuncia la acción prevista de los predicados en la página de búsqueda (NPR-34104).

* La página de búsqueda y la página de resultados de búsqueda ahora tienen títulos más informativos para comprender mejor a los usuarios de lectores de pantalla (NPR-34093).

* Los lectores de pantalla ahora anuncian las opciones para eliminar las etiquetas seleccionadas en la ficha [!UICONTROL Basic] de la página del recurso [!UICONTROL Properties] (NPR-33972).

* Los elementos de cada fila de la vista de lista ahora son anunciados como los elementos de la misma fila por los lectores de pantalla (NPR-33932).

* El enfoque del usuario al navegar con la tecla `Tab` ahora pasa a la opción de cierre en la previsualización de la versión (NPR-33863).

* El enfoque del usuario ahora se mueve al icono de búsqueda después de que Omniture esté cerrado (NPR-33705).

* Las opciones de interfaz de usuario procesables ahora tienen un enfoque visual más prominente y un mayor contraste al navegar con las teclas del teclado. Los usuarios del teclado pueden identificar las áreas enfocadas (NPR-33542).

* La funcionalidad de arrastrar mediante el teclado ahora funciona en [!UICONTROL Editor de Esquemas de metadatos] en el modo de exploración del lector de pantalla (CQ-4296326).

* En el cuadro de diálogo de uso compartido de vínculos, al navegar en el modo de exploración, un lector de pantalla,

   * No narra la información de la tabla en cuanto se carga el cuadro de diálogo.

   * Puede navegar a todas las sugerencias automáticas de la lista.

   * Narra las sugerencias automáticas mostradas para [!UICONTROL Añadir dirección de correo electrónico/Buscar] (CQ-4294232).

* El uso de la tecla `Esc` para eliminar los iconos de acción rápida de la vista de tarjeta ya no elimina el enfoque del teclado del último elemento seleccionado (CQ-4293554).

* Para las opciones interactivas en la interfaz de usuario, el lector de pantalla ahora anuncia su propósito en lugar de los nombres literales de los iconos (CQ-4272943).

* El enfoque del teclado ahora se mueve correctamente a [!UICONTROL Flotante], [!UICONTROL InlineZoom], [!UICONTROL Banner_comprador], [!UICONTROL Zoom_dark], [!UICONTROL Zoom_light], [!UICONTROL ZoomVertical_dark] y [!UICONTROL opciones de ZoomVertical_light] al navegar mediante la tecla de tabulación del teclado en los detalles de recursos [!UICONTROL Visores] en [!DNL Dynamic Media] (CQ-4290605).

* [!UICONTROL Ahora se puede acceder a la opción Guardar y ] cerrar en la página   Propiedades del recurso con las teclas del teclado (NPR-34107).

* Los mensajes de error debido a combinaciones incorrectas de nombre de usuario y contraseña en la página de inicio de sesión ahora los lectores de pantalla anuncian cada vez que se produce el error (NPR-33722).

* En la sección de encabezado [!DNL Experience Manager], al navegar en el modo Examinar, el lector de pantalla ahora anuncia:

   * Sugerencias editadas automáticamente en [!UICONTROL Escriba para buscar] en Omniture Search.

   * El estado se expande o contrae para las opciones [!UICONTROL Soluciones], [!UICONTROL Ayuda], [!UICONTROL Bandeja de entrada] y [!UICONTROL Usuario].

   * El mensaje de estado [!UICONTROL Búsqueda de ayuda] que se muestra cuando el usuario introduce una cadena de búsqueda en el campo [!UICONTROL Buscar ayuda] en la opción [!UICONTROL Ayuda].

   ![Menú Ayuda en el encabezado](assets/Help_aem_header.png)

   *Figura:  [!UICONTROL Busque ] Helpin   Helpmenu.*

   * El mensaje de error si se introduce un valor incorrecto en el campo [!UICONTROL Suplantar como] en la opción [!UICONTROL Usuario] y el enfoque se mueve correctamente al campo de texto (NPR-33804).

   ![Menú Usuario en el encabezado](assets/User_aem_header.png)

   *Figura:  [!UICONTROL Suplantar ] un campo en el   menú Usuario en el encabezado.*

* Ahora el usuario puede cambiar el enfoque mediante el teclado:

   * [!UICONTROL Buscar/Añadir ] dirección de correo electrónico en el cuadro de diálogo  [!UICONTROL Vincular ] uso compartido.

   * [!UICONTROL Añadir usuario o ] grupo en  [!UICONTROL Usuario ] cerrado Agrupar la   ficha de permisos de  [!UICONTROL Propiedades]  de carpeta (NPR-34452).

**Problemas solucionados en Experience Manager Assets**

[!DNL Adobe Experience Manager] 6.5.6.0  [!DNL Assets] proporciona correcciones a los siguientes problemas:

* Las anotaciones no se resaltan cuando se seleccionan en la línea de tiempo del recurso (CQ-4302422).

* La previsualización de activos de garantía de marketing (como Folleto, Volante y Tarjeta de presentación) creada con la plantilla [!DNL Adobe InDesign] no muestra saltos de línea ni saltos de párrafo (NPR-34268).

* La extracción de texto y, por lo tanto, la búsqueda de texto completo de los archivos PDF cargados no funciona (NPR-34164). Para solucionarlo, reinicie la implementación [!DNL sAdobe Experience Manager] después de instalar Service Pack 6.

* La línea de tiempo de los recursos de varias páginas muestra las anotaciones aplicadas a todos los subrecursos al explorar el recurso en la vista de la línea de tiempo, en lugar de mostrar las anotaciones específicas de los subrecursos específicos (NPR-34100).

* Las carpetas de recursos no se publican con la opción [!UICONTROL Administrar publicación] si las carpetas contienen recursos en los formatos de archivo JavaScript, CSS o JSON (NPR-34090).

* Al anular la selección o eliminar las etiquetas o filtros aplicados en Omniture, se ejecuta la consulta de búsqueda varias veces, lo que aumenta el tiempo de búsqueda (NPR-34078).

* En la vista de tarjetas cuando un flujo de trabajo (en un recurso de una carpeta) está en curso o pendiente, la página se vuelve a cargar hasta que se completa o finaliza el flujo de trabajo. Por lo tanto, los autores no pueden trabajar en los recursos de la carpeta para la que tienen que desplazarse hacia abajo (NPR-33986).

* Si el usuario mueve un recurso publicado a una nueva ubicación, el recurso se vuelve a publicar aunque la opción [!UICONTROL Volver a publicar] no esté seleccionada. Esto provoca que muchos recursos huérfanos se encuentren en la instancia de publicación. Sin embargo, el comportamiento predeterminado es que la operación de movimiento de un recurso publicado la anula de forma automática; este recurso se vuelve a publicar si el autor selecciona la opción [!UICONTROL Volver a publicar] al mover el recurso (NPR-33934).

* La página [!UICONTROL Mover recursos] para los recursos de las colecciones no carga todo el contenido HTML, como la opción [!UICONTROL Ajustar/volver a publicar]. Por lo tanto, los usuarios no pueden completar la operación de movimiento (NPR-33860).

* Al mover un recurso y añadir caracteres especiales en el nombre y el título de los recursos movidos, se crea una carpeta adicional (con el mismo nombre) en la nueva ubicación del recurso (NPR-33826).

* [!UICONTROL El ] botón de descarga de un recurso se desactiva cuando se selecciona   la opción de correo electrónico en el   cuadro de diálogo de descarga (NPR-33730).

* El error &quot;Solicitar URI demasiado largo&quot; se observa al realizar operaciones masivas en recursos, como la edición masiva de metadatos (NPR-33723).

* Se observa un error de JavaScript y los usuarios no pueden seleccionar ni eliminar las opciones generadas en el campo [!UICONTROL Desplegable] mediante la funcionalidad [!UICONTROL Añadir a través de la ruta JSON] en el [!UICONTROL Editor de formularios de Esquema de metadatos de la carpeta], si el archivo JSON cargado tiene un valor de espacio o caracteres especiales (NPR-3333777112).

* Las representaciones estáticas de recursos no se actualizan cuando el recurso se actualiza con la opción [!UICONTROL Abrir] en [!DNL desktop app] o [!DNL Adobe Asset Link] y se sincronizan de nuevo con [!DNL Adobe Experience Manager] (CQ-4296279).

* En la vista de columna, la operación de mover en un conjunto de recursos también mueve los recursos seleccionados antes de utilizar la opción [!UICONTROL Filtrar] para ellos. Tenga en cuenta que el uso de la opción [!UICONTROL Filtro] anula la selección anterior (NPR-34018).

* Las barras invertidas se agregan antes que los caracteres especiales en las sugerencias de búsqueda de recursos, que tienen caracteres especiales en su nombre (NPR-33834).

* Al crear reglas para el menú desplegable en [!UICONTROL Formulario de Esquema de metadatos de carpeta], el usuario no puede seleccionar valores en la columna [!UICONTROL Opciones de campo] (CQ-4297530).

* La copia en tiempo de ejecución del modelo de flujo de trabajo personalizado de recursos (creado en `/var/workflow/models/dam`) se elimina al instalar [!DNL Experience Manager] 6.5 Service Pack 5 o una versión anterior en [!DNL Experience Manager] 6.5 (NPR-34532). Para recuperar la copia en tiempo de ejecución, sincronice la copia en tiempo de diseño del modelo de flujo de trabajo con la copia en tiempo de ejecución mediante la API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

**Problemas solucionados en Dynamic Media**

* Si el usuario define la configuración de codificación en las ediciones después de crear el perfil de vídeo, la configuración de recorte inteligente se elimina de los perfiles de vídeo (CQ-4299177).

* Los recursos parpadean al cargarse la página cuando el usuario cambia entre las opciones de carril lateral (por ejemplo, [!UICONTROL Información general], [!UICONTROL Línea de tiempo], [!UICONTROL Visores]) en la página de detalles de recursos (NPR-34235).

* Se observan los siguientes problemas con el trabajo de reprocesamiento:

   * Falta el identificador de trabajo en el identificador de trabajo devuelto por el trabajo de reprocesamiento.

   * El trabajo de reprocesamiento para los registros de vídeo solo tiene que ver con el nombre del archivo y no con la ruta completa.

   * El trabajo de reprocesamiento no tiene la opción de establecer el tipo de recurso como estático.

   * `ExcludeFromAVS` no se proporciona (CQ-4298401).

* La funcionalidad de recorte inteligente falla cuando se agrega perfil de imagen a una carpeta con varias proporciones de aspecto (por ejemplo, 11) (NPR-34082).

* El flujo de trabajo de recursos de actualización DAM se activa cuando el usuario se desplaza hacia abajo en la página [!UICONTROL Archivo de flujo de trabajo] de la ficha [!UICONTROL Flujo de trabajo] de [!UICONTROL Herramientas] en [!DNL Adobe Experience Manager] configurada con Dynamic Media Scene7 (CQ-4299727).

* Los símbolos de la ficha [!UICONTROL Comportamiento] del [!UICONTROL Editor de ajustes preestablecidos de visor] no están localizados (CQ-4299026).

* La vista principal muestra la imagen con una presentación incorrecta que no cabe en el visor, si el visor está en modo interactivo (CQ-4298293).

* Los cambios en los ajustes preestablecidos de imagen en [!UICONTROL Adobe Experience Manager] no se sincronizan con Scene7 Publishing System (CQ-4299713).

### [!DNL Commerce] {#commerce-6560}

* Los vínculos a recursos de productos no se vuelven a factorizar cuando se mueven recursos (NPR-34098).

### Plataforma {#platform-6560}

* No se pueden descargar registros con la herramienta Diagnóstico en una instancia de Experience Manager actualizada (NPR-34336).
* La actualización falla con un error debido a las dependencias en una versión específica del paquete de base `cq-wcm-api` (CQ-4300520).
* No se especifican los valores predeterminados para las opciones **[!UICONTROL Tiempo de espera de conexión]** y **[!UICONTROL Tiempo de espera de socket]** para la configuración del agente predeterminado (publicación) (NPR-33707).
* Las actualizaciones de la configuración de asignación en `/etc/map.publish` no se reflejan en las páginas del sitio (NPR-34015).
* [La ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html) documentación de referencia de API no incluye la documentación del  `com.day.cq.tagging` paquete (CQ-4295864).

### Interfaz de usuario {#ui-6560}

* La interfaz del explorador de descarga no muestra todos los temas de trabajo (NPR-34308).
* La interfaz [Configuration Browser](/help/sites-administering/configurations.md) no muestra todas las configuraciones (NPR-33644).
* Al pulsar la tecla `Esc` al buscar usuarios que suplanten, se cierra el cuadro de diálogo **[!UICONTROL Usuario]** en lugar de la lista del usuario (NPR-34084).

### Integraciones {#integrations-6560}

* Las actividades con nombres largos no se sincronizan con [!DNL Adobe Target] (NPR-34254).

* Al seleccionar una propiedad al crear una nueva configuración de inicio de Adobe, aparece el siguiente mensaje de error (NPR-33947):

   ```javascript
   GET http://hostname:Port/libs/cq/dtm-reactor/content/configurations/createcloudconfigwizard/jcr:content/body/items/form/items/wizard/items/general/items/fixedcolumns/items/container/items/general/items/property/data.html?query=&start=0&end=25&imsConfigurationId=Adobe%20Launch&companyId=&_charset_=utf-8 400 (Bad Request)
   ```

### Proyectos de traducción {#translation-6560}

* No se crea un proyecto de traducción si el `authorizableID` del usuario incluye caracteres especiales (NPR-33828).

### Sling {#sling-6560}

* La comprobación de estado y el detector de patrones tienen una funcionalidad superpuesta. Como resultado, la comprobación de estado de salud se elimina del producto (NPR-33928).

### WCM {#wcm-6560}

* Componentes de base: cuando se agrega un componente de imagen de base a una página y se hace referencia a una imagen, la operación `Undo` no funciona (NPR-34516).

* No se puede utilizar la operación de desplazamiento de página (CQ-4303028).

### [!DNL Communities] {#communities-6560}

* Compartir una publicación en medios sociales muestra una opción obsoleta de Google+ (NPR-33877).

* El miembro de la comunidad no puede modificar la plantilla de grupo ni otros ajustes de la función de grupo (NPR-33530).

* Las etiquetas de hipervínculo de las imágenes no se generan correctamente en una publicación de foro (NPR-33464).

* Los errores de accesibilidad se identifican en la función Asignación de comunidad (NPR-33442).

* Los usuarios existentes de un grupo de comunidad agregados a través de la consola de administración se eliminan de la lista de usuario en cualquier modificación de la consola de grupo de comunidad (NPR-34315).

* El `TagFilterServlet` filtra datos potencialmente sensibles (NPR-33868).

<!--
* Tag filters are vulnerable to sensitive information disclosure (NPR-33868).
-->

### [!DNL Forms] {#forms-6560}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack no incluye correcciones para  [!DNL Forms]. Se entregan mediante un paquete de complemento [!DNL Forms] independiente. Además, se ha publicado un instalador acumulativo que incluye correcciones para [!DNL Experience Manager Forms] en JEE. Para obtener más información, consulte [Instalación de AEM Forms Add-on](#install-aem-forms-add-on-package) y [Instalación de AEM Forms en JEE](#install-aem-forms-jee-installer).

Después de instalar el paquete del complemento [!DNL Experience Manager Forms] 6.5.6.0:

* Detenga la instancia [!DNL Experience Manager Forms].

* Elimine los archivos `bcpkix-1.51`, `bcmail-1.51` y `bcprov-1.51` JAR del directorio `crx-repository\launchpad\ext`.

* Eliminar la propiedad` sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider` del archivo `sling.properties`.

* Reinicie la instancia [!DNL Experience Manager Forms].

**Formularios adaptables**

* Cuando falta un fragmento de formulario adaptable, el formulario adaptable no se procesa (NPR-34302).

* La descripción del contenido de la ayuda de los campos de formulario adaptables muestra una etiqueta HTML de párrafo (NPR-34116).

* Al seleccionar la propiedad **[!UICONTROL Revalidate en el servidor]**, el formulario adaptable no se puede enviar (NPR-33876).

* La acción de envío **[!UICONTROL Enviar a extremo REST]** no funciona para un formulario adaptable (CQ-4299044).

* Accesibilidad: Al intentar enviar un formulario adaptable sin cargar un archivo adjunto para un campo obligatorio, el enfoque no se desplaza automáticamente al campo adjunto (CQ-4298065).

* Cuando agrega filas a una tabla de un formulario adaptable, las opciones **[!UICONTROL Añadir a top]** y **[!UICONTROL Añadir a bottom]** no muestran los resultados adecuados (CQ-4297511).

* La secuencia de comandos [!UICONTROL Value Commit] se activa incorrectamente, lo que resulta en la pérdida de datos en un formulario adaptable (CQ-4296874).

* El selector de fechas no funciona correctamente en formularios adaptables localizados (NPR-34333).

* Cuando hay un subrayado o espacio en el nombre del archivo, no se puede adjuntar el archivo a un formulario adaptable (CQ-4301001).

* Cuando un panel repetible anidado tiene más apariciones que su principal, todas las ocurrencias de dicho panel repetible anidado no se pueden rellenar previamente (NPR-33666).

* Los formularios adaptables tienen algunos resueltores de recursos abiertos. Esto lleva a errores de envío. El problema se produce de forma intermitente (CQ-4299407).

* Al abrir la configuración de campo por primera vez, no se muestra el icono de propiedades (CQ-4296284).

* Los usuarios pueden editar metadatos de envío, como `afPath`, `afSubmissionTime` y `signers`, al enviar un formulario adaptable. Para resolver el problema, los valores de metadatos se eliminan de los datos de envío del formulario en el lado del cliente. Los usuarios pueden utilizar el objeto `FormSubmitInfo` para recuperar estos valores del servidor (NPR-33654).

* Las entradas de usuario no se codifican correctamente para los componentes [!DNL Forms] al enviar información al cliente (NPR-33611).

**Flujo de trabajo**

* Cuando un aprobador de flujo de trabajo carga un archivo adjunto, se cambia su nombre a `undefined` (NPR-33699).

* [!DNL Experience Manager] Error en la operación de depuración de flujo de trabajo y muestra el siguiente mensaje de error (NPR-33575):

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* [!DNL Experience Manager Forms] aplicación para  [!DNL Windows] dejar de responder después de enviar un formulario (NPR-34409).

* Al instalar AEM Service Pack, la lista **Tareas pendientes** de elementos no se muestra como vínculos. El texto de los elementos **Por hacer** incluye etiquetas HTML (NPR-34317).

**Comunicación interactiva**

* Cuando se incluye un fragmento de documento de texto con componentes repetibles anidados, la comunicación interactiva no se guarda (NPR-34095).

**Administración de correspondencia**

* Al modificar un fragmento de documento de texto que incluye valores de diccionario de datos, la interfaz de usuario del agente deja de responder (NPR-33930).

* Copiar y pegar contenido de un documento [!DNL Microsoft Word] en un fragmento de documento de texto en una carta genera problemas de formato (NPR-33536).

**Servicios de documento**

* Cuando se genera un archivo PDF a partir de un archivo XDP mediante los servicios Output y Forms, el resultado es que falta texto y se superpone (NPR-34237, CQ-4299331).

* Al convertir un archivo HTML a PDF, el atributo `MaxReuseCount` no se puede configurar (NPR-33470).

* Cuando se descarga un archivo PDF que incluye funciones interactivas de Extensiones de Reader, no se puede agregar un archivo adjunto al archivo PDF mediante [!DNL Adobe Reader] (NPR-33729).

**:Seguridad de los documentos**

* No se puede ejecutar la operación de firma con certificados basados en HSM en un archivo PDF después de instalar [!DNL Experience Manager] Service Pack (NPR-34310).

**Diseñador**

* No se pueden abrir XForms en Designer versión 6.5.x (CQ-4295322).

* Al abrir Designer, la pantalla de bienvenida muestra un año incorrecto (CQ-4295289).

* Al instalar [!DNL Acrobat DC] en el servidor, la opción **[!UICONTROL Distribuir formulario]** está inactiva (CQ-4296304).

Para obtener información sobre las actualizaciones de seguridad, consulte [página de boletines de seguridad de Experience Manager](https://helpx.adobe.com/security/products/experience-manager.html).

## [!DNL Adobe Experience Manager] 6.5.5.0  {#experience-manager-6550}

Adobe Experience Manager 6.5.5.0 es una actualización importante que incluye nuevas funciones, mejoras clave solicitadas por los clientes y mejoras en el rendimiento, la estabilidad y la seguridad, que se publican desde la disponibilidad general de la versión 6.5 en **abril de 2019**. Se puede instalar sobre Adobe Experience Manager 6.5.

Algunas funciones y mejoras clave introducidas en [!DNL Adobe Experience Manager] 6.5.5.0 incluyen:

* No se permite el acceso anónimo al CRXDE Lite. En su lugar, se dirige a los usuarios a la pantalla de inicio de sesión. Consulte [Desarrollo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* Personalice los nombres de columna que se muestran en la bandeja de entrada [!DNL Adobe Experience Manager].

* Se ha mejorado la accesibilidad en varias áreas de Experience Manager Web Gestor de contenido (WCM), como el Editor de páginas, los Componentes principales, RTE y la interfaz de usuario del administrador.

* Guarde un [!DNL Interactive Communication] como borrador.

* Compatibilidad con [!DNL Oracle WebLogic 12] para Forms Experience Manager en JEE.

* Se mejoró la gestión de excepciones en el flujo de la interfaz de usuario [!DNL Adobe Experience Manager Assets].

* Para obtener la URL de publicación para Dynamic Media Scene7, se agrega un nuevo método `getRemoteAssetPublishURL` a la interfaz `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi`.

* [Mejoras de ](#assets-6550) accesibilidad  [!DNL Adobe Experience Manager Assets] de conformidad con las directrices de accesibilidad del contenido web (WCAG).

* Se ha eliminado la integración de Package Share de Adobe Experience Manager.

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.22.3.

Para obtener una lista completa de las funciones, los aspectos destacados clave y las funciones clave que se incluyen en el Service Pack 5 de Experience Manager 6.5, consulte [Novedades de Adobe Experience Manager 6.5 Service Pack 5](new-features-latest-service-pack.md).

La siguiente es la lista de correcciones que se proporciona en la versión [!DNL Experience Manager] 6.5.5.0.

### [!DNL Sites] {#sites-6550}

* Sitios Experience Manager proporciona una opción para publicar o cancelar la publicación de una página desde su alias. La opción no funciona (NPR-33415).
* Cuando se elimina un contenedor de diseño de una plantilla que contiene varias plantillas, la plantilla no se representa correctamente (NPR-33347).
* Cuando una página Sitios Experience Manager forma parte de un conjunto de contenido grande con varias Live Copies, la previsualización del historial de versiones de la página no se carga (NPR-33311).
* Cuando se utiliza el comando Mover para cambiar el nombre de una página Sitios Experience Manager, el título de la página no se actualiza (NPR-33264).
* Al mover páginas a través de la vista de columna, las columnas desaparecen (NPR-33216).
* Cuando el nombre de un componente local en una copia de idioma es idéntico al nombre de un componente en el modelo y el componente se despliega desde el modelo, el término `_msm_moved` no se agrega al nombre del componente local (NPR-33208).
* El servlet Redireccionamiento de página anexa .html a una dirección URL de sitios de Experience Manager donde ResourceType no es `cq:Page` (NPR-33176).
* Al pegar un subárbol, no hay opción de decidir si las subpáginas correspondientes se van a pegar o no (NPR-33149).
* El número de resultados en el uso activo de un componente está limitado al número 49 (NPR-33058).
* Cuando se basa un fragmento de contenido en un esquema y contiene un área de texto obligatoria o un campo de ruta, el fragmento de contenido no se guarda (NPR-33007).
* Cuando se crea un componente personalizado con el componente Fragmento de experiencia predeterminado y se utiliza en páginas Sitios Experience Manager, el Experience Manager no muestra referencias (uso) para el componente personalizado (NPR-32852).
* Al cambiar el nombre de una carpeta con un gran número de referencias, muchas referencias a la carpeta no se actualizan (NPR-32765).
* Cuando se activa la opción de edición de origen, esta opción queda disponible para las opciones de pantalla completa en línea, pero sigue faltando para el cuadro de diálogo de edición y las opciones de pantalla completa del editor de texto enriquecido (NPR-32763).
* Si tiene un campo múltiple y contiene un campo requerido (como un menú desplegable o un campo de ruta) en las propiedades de página de un modelo, cuando se despliega una página que contiene un campo múltiple de este tipo, las propiedades de página de la Live Copy no se guardan (NPR-32751).
* Los lectores de pantalla no pueden utilizar la estructura de encabezados para navegar por una página. Además, la ficha Componentes tiene una etiqueta incorrecta (NPR-32648).
* Cuando se producen inicios de paginación, el selector de fragmentos de experiencia no carga todos los elementos (NPR-32605).
* Se revocan los permisos de autor para leer, modificar, crear y eliminar copias en directo. Cada autor tenía que proporcionar explícitamente permisos de lectura y modificación para mover páginas dentro de un modelo (NPR-32550).
* Los autores de contenido no pueden crear Launch para una página que se integra con Adobe Analytics (NPR-32548).
* Cuando un usuario reanuda la herencia con la sincronización, la Live Copy de la página principal no se sincroniza con el modelo y muestra un estado incorrecto (NPR-32500).
* La página del editor Sitios Experience Manager tarda más de 15 segundos en cargarse (NPR-32413).
* Algunos campos no muestran la opción Cancelar herencia (NPR-32362).
* Cuando se selecciona una ruta para un componente Fragmento de experiencia y se selecciona la casilla de verificación Abrir cuadro de diálogo de selección, no se navega a la ruta seleccionada en el Explorador de rutas (NPR-32308).
* Al actualizar de Experience Manager 6.2 a Experience Manager 6.5, el componente Parsys de las plantillas estáticas no se muestra correctamente. La altura del componente Parsys se establece en 0 y los componentes que contiene no son visibles (NPR-33663).
* Cuando un usuario copia y pega un Contenedor de diseño en la misma página, los componentes de un Contenedor de diseño no se muestran (NPR-33648).
* La comprobación de estado del despachante muestra `Invalid cookie header` un mensaje de advertencia en los archivos de registro (NPR-33629).
* Se refleja XSS en PreferencesServlet (NPR-33438).
* Los usuarios anónimos pueden acceder a las funciones de CRXDE Lite (GRANITE-27790).

### [!DNL Assets] {#assets-6550}

>[!IMPORTANT]
>
>Se recomienda a los usuarios de Windows de [!DNL Experience Manager desktop app] que actualicen a [versión 2.0.3.2](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html#whats-new-added) de la aplicación de escritorio para acceder al repositorio de DAM en la instancia [!DNL Adobe Experience Manager 6.5.5.0]. Como pueden encontrar problemas al acceder al repositorio de DAM en la instancia [!DNL Adobe Experience Manager] 6.5.5.0 mediante la versión 2.0.2 de la aplicación de escritorio.

**Mejoras de accesibilidad en Recursos Experience Manager**

* Ahora es posible enfocar el teclado en la lista [!UICONTROL Comentarios] y la opción en la que se puede hacer clic para [!UICONTROL Crear] comentarios de la versión en [!UICONTROL Crear nueva versión] en el panel [!UICONTROL Línea de tiempo] de recursos (NPR-33424).

* Ahora es posible acceder a la opción [!UICONTROL Configuración de Vista] para los recursos y cambiar la configuración en el cuadro de diálogo [!UICONTROL Configuración de Vista] mediante las teclas del teclado (NPR-33420).

* La ventana emergente del cuadro de lista del cuadro combinado (en varios campos de diferentes páginas) ahora muestra las entradas como una lista de opciones que pueden anunciar los lectores de pantalla (NPR-33516).

* La funcionalidad de ordenación de los encabezados que se pueden ordenar (en la vista de lista, [!UICONTROL vista de línea de tiempo] y [!UICONTROL Administrar publicación]) ahora la anuncian los lectores de pantalla y se puede acceder a los controles de clasificación de los encabezados de columna mediante el teclado (NPR-32979).

* Los elementos en los que se puede hacer clic, como tarjetas de comentarios, actualizaciones de versiones, cuadros combinados e iconos de chevron de los menús, ahora se pueden enfocar e interactuar con un teclado (NPR-33514).

* La funcionalidad (o propósito de acción) de los iconos de perspectivas (para uso, impresiones y clics) en [!UICONTROL Vista de perspectivas] ahora los lectores de pantalla anuncian correctamente (NPR-33513).

* Los campos de formulario de sólo lectura (por ejemplo, campos desactivados en [!UICONTROL ficha Básico] del recurso [!UICONTROL Propiedades]) ahora se pueden enfocar mediante el teclado (NPR-33493, CQ-4273031).

* Las etiquetas de varios campos de entrada ahora son etiquetas permanentes (por lo tanto accesibles) y no solo etiquetas de marcador de posición, que desaparecían cuando se introducía texto (NPR-33475).

* Los diferentes niveles de encabezados (como títulos de página y encabezados de sección) ahora se perciben como encabezados con diferentes niveles para los usuarios de lectores de pantalla (NPR-33471).

* Ahora se puede acceder a los elementos interactivos de la interfaz de usuario, como los vínculos y las opciones (en las opciones de encabezado y zoom de la página de recursos, navegación por carpetas) mediante un teclado (NPR-33468, CQ-4271412).

* Los indicadores de progreso de [!UICONTROL Opciones], [!UICONTROL Ámbito] y [!UICONTROL Flujos de trabajo] en la página [!UICONTROL Administrar publicación] ahora los lectores de pantalla leen correctamente como indicadores de progreso, en lugar de fichas (NPR-33416).

* El color de los iconos de clasificación por estrellas (como en la sección [!UICONTROL Clasificación] de la ficha [!UICONTROL Avanzadas] del recurso [!UICONTROL Propiedades] o en la vista de la tarjeta) se cambia para que el contraste adecuado sea visible para los usuarios con visión limitada y sin percepción de color (NPR-33414).

* Ahora se puede acceder a la flecha hacia arriba situada junto al campo [!UICONTROL Comentario] en la página de detalles de recursos mediante las teclas del teclado (NPR-33397).

* Los estados expandidos y contraídos del cuadro de diálogo [!UICONTROL Etiquetas] en el recurso [!UICONTROL Propiedades] y navegación por el carril izquierdo (en la interfaz de usuario de los recursos) ahora los anuncian correctamente los lectores de pantalla (NPR-33396).

* Los títulos de todas las páginas exploradas en [!DNL Adobe Experience Manager] recursos ahora son únicos (NPR-33343).

* Al navegar por la estructura de árbol, los lectores de pantalla anuncian ahora correctamente varios elementos del control de vista de árbol (NPR-33304).

* Ahora se puede acceder a diferentes versiones de los recursos en la página de detalles de [!UICONTROL Línea de tiempo] vista en los recursos mediante las teclas del teclado (NPR-33283).

* Los nombres de las sugerencias de búsqueda que aparecen en el cuadro combinado Omnisearch ahora los anuncian los lectores de pantalla al utilizar la funcionalidad de búsqueda (NPR-33280).

* Los elementos activos y [!UICONTROL Ir al vínculo] en [!UICONTROL carril de referencias] ahora los lectores de pantalla anuncian como elementos activos (NPR-33278).

* La información de estructura de tabla (como la fila 1, celda 1, tabla) del cuadro de diálogo [!UICONTROL Vínculo compartido] ya no la anuncian los lectores de pantalla cuando se abre el cuadro de diálogo (NPR-33268).

* El propósito de varios elementos de cuadro combinado (como el campo Ruta y la opción para abrir el cuadro de diálogo Selección en la ficha Básico de Propiedades del recurso) ahora lo anuncian correctamente los lectores de pantalla (NPR-33235).

* La información de que las filas de la tabla de vista de listas son seleccionables ahora se comunica a los usuarios del lector de pantalla cuando el teclado está en ellas. Cuando se sitúa un puntero sobre las filas, los lectores de pantalla anuncian la información (NPR-33234).

* Las opciones (que tienen [!UICONTROL x]) para eliminar cada una de las etiquetas seleccionadas debajo del campo [!UICONTROL Etiquetas] en la ficha [!UICONTROL Básico] de [!UICONTROL Propiedades] ahora son accesibles para los lectores de pantalla (NPR-33206).

* El selector de fechas del calendario ahora puede seleccionarse y procesarse mediante el teclado por usuarios de lectores de pantalla y usuarios de teclado con visión (NPR-33200).

* El cambio para cambiar entre la vista de lista y la vista de tarjetas ahora expone correctamente su funcionalidad (de ajustar vistas) al lector de pantalla (NPR-33069).

* Ahora se puede acceder al menú en el carril izquierdo. Los lectores de pantalla anuncian adecuadamente la funcionalidad y el propósito de ampliar el menú (NPR-33068).

* Los usuarios de lectores de pantalla ahora pueden acceder al cuadro de lista y a muchos otros elementos de la interfaz de usuario, y los lectores de pantalla anuncian la siguiente información (NPR-33040):

   * si se requiere la introducción de datos por parte del usuario en un elemento antes del envío del formulario.
   * si un elemento no es editable.
   * si un widget está seleccionado o no.

* Ahora se puede acceder a la opción de abrir la barra lateral del filtro mediante el teclado (NPR-32842, CQ-4273018).

* Ahora se puede acceder al control de casilla de verificación en el encabezado de columna de la vista de lista y los lectores de pantalla anuncian el propósito de utilizar el control (NPR-32722, NPR-33005).

* Las etiquetas de los campos de horas (HH) y minutos (mm) en el selector de fechas del calendario son ahora etiquetas permanentes en lugar de etiquetas de marcador de posición, y no desaparecen cuando el usuario introduce texto en estos campos (NPR-32720).

* El texto de los vínculos de las notificaciones (que aparecen después de hacer clic en el icono de la campana) ahora se anuncia a los usuarios del lector de pantalla, que utilizan la ficha para acceder a cada vínculo (NPR-32645).

* [!UICONTROL Seleccione],  [!UICONTROL Descargar],  [!UICONTROL Propiedades] y  [!UICONTROL Más ] accionesLas opciones de tarjetas de recursos en  [!UICONTROL la ] vista de perspectivas ahora están disponibles mediante el teclado (NPR-32609).

* El contenido oculto visualmente (como el contenido de la barra de menús del encabezado en los resultados de búsqueda) ya no lo anuncian los lectores de pantalla cuando se accede mediante el teclado (NPR-32606).

* El propósito de las etiquetas de los controles para pasar a los meses siguiente y anterior en el selector de fechas del calendario ahora lo anuncian los lectores de pantalla (NPR-32604).

* Los iconos de clasificación por estrellas ahora se pueden enfocar y activar con las teclas del teclado (NPR-32513).

* Ahora se puede acceder a la funcionalidad para controlar el volumen de vídeo mediante tabuladores (para centrarse en el control deslizante del volumen) y teclas de flecha (para ajustar el volumen) en el teclado (NPR-32065).

* El propósito de los campos de entrada de límite inferior ([!UICONTROL Desde]) y límite superior ([!UICONTROL A]) del filtro Tamaño de archivo ahora se anuncia a los usuarios de lectores de pantalla sin visión de futuro (NPR-32064).

* El menú [!UICONTROL Idiomas] del formulario [!UICONTROL Crear y traducir] ahora es accesible para los lectores de pantalla en modo de exploración (CQ-4293906).

* Ahora se puede acceder al panel [!UICONTROL Referencias] con las siguientes mejoras (NPR-33261, CQ-4293798):

   * En el modo de exploración, el enfoque del lector de pantalla ya no se mueve a los campos de edición de varias líneas ocultos en las secciones [!UICONTROL Referencias del sitio], [!UICONTROL Referencias de recursos], [!UICONTROL Copias] y [!UICONTROL Referencias de formulario].

   * Los lectores de pantalla ahora anuncian la función de los elementos [!UICONTROL Referencias del sitio] y [!UICONTROL Copias de idioma].

   * El enfoque de los lectores de pantalla en el modo de exploración cambia en una secuencia significativa a varios elementos.

* [!UICONTROL Ahora se puede acceder a la página de ] edición de Esquemas de metadatos y a sus elementos mediante el teclado y son fáciles de leer en pantalla (CQ-4290962, CQ-4272953).

* El propósito del símbolo `X` para eliminar las etiquetas seleccionadas lo anuncian los lectores de pantalla junto con el número de etiquetas seleccionadas (CQ-4273017).

* Para evitar confusiones entre los usuarios sin visión de futuro que utilizan lectores de pantalla, los iconos y las imágenes decorativos ahora son ignorados por los lectores de pantalla (CQ-4272944).

**Problemas solucionados en Experience Manager Assets**

[!DNL Adobe Experience Manager] 6.5.5.0 Assets ofrece correcciones a los siguientes problemas:

* [!UICONTROL La opción ] Inicio del cuadro de diálogo  [!UICONTROL Crear ] flujo de trabajo para los recursos de una colección está desactivada, lo que impide que se active el flujo de trabajo (NPR-32471).

* Cuando se utiliza la ventana emergente en cascada en esquemas de metadatos, al seleccionar y guardar una opción desplegable que contiene un apóstrofo (del menú desplegable secundario), la opción de apóstrofo seleccionada desaparece después de volver a abrir el recurso [!UICONTROL Propiedades] (NPR-32649).

* [!UICONTROL Asset Insights Sincroniza ] Jobstops y falla si encuentra entradas no válidas (en el lado de Analytics) en lugar de pasar a la siguiente entrada (NPR-32674).

* El ámbito de navegación no funciona, ya que los sensores de movimiento están desactivados de forma predeterminada en los navegadores móviles en el visor panorámico (CQ-4272937).

* [!UICONTROL El asistente ] de configuración de recursos conectados no funciona con el error 404 al instalar 6.5.3 en 6.5.1 (NPR-32730).

* Durante el proceso de reescritura XMP, todas las propiedades de metadatos de Área de nombres personalizadas cambian el prefijo de Área de nombres personalizado a ns2 en lugar del prefijo de Área de nombres configurado (NPR-32748).

* La carga diferida no se activa y solo se muestran 100 recursos al seleccionar para revisar las tareas de la bandeja de entrada de notificaciones (NPR-32750).

* `NullPointerException` se observa debido a la ausencia de preferencias de nodos en el perfil de usuario recién creado (SAML/SSO). Este error impide que los usuarios que inicien sesión recientemente utilicen la integración [!DNL Adobe Experience Manager Stock] (NPR-32777).

* Se observan advertencias transitorias en los registros al abrir una colección inteligente que contiene más de 10.000 recursos (NPR-32980).

* Los nombres de los recursos se cambian a minúsculas al mover recursos de una carpeta a otra en [!DNL Adobe Experience Manager] en el modo de ejecución de Dynamic Media Scene7 (NPR-32995).

* Un recurso buscado no se puede eliminar después de navegar a sus propiedades desde los resultados de búsqueda y luego volver a los resultados de búsqueda para eliminarlo (NPR-32998).

* [!UICONTROL La opción ] Siguiente permanece desactivada al seleccionar la carpeta de destino en la interfaz  [!UICONTROL Mover ] recursos (NPR-33356).

* [!UICONTROL La opción ] Siguiente no está habilitada al seleccionar el nodo principal (donde se ve una sola carpeta secundaria) y, a continuación, seleccionar la carpeta secundaria (NPR-33275).

* Los permisos de protección y desprotección están desactivados en el vínculo de recursos de Adobe (AAL) para los usuarios con permisos de eliminación, aunque se hayan concedido otros permisos como leer, crear o modificar (NPR-33272).

* Las representaciones de recorte inteligente no están disponibles en el cuadro de diálogo de descarga de recursos (NPR-33167).

* Se observa una excepción en los registros al abrir el carril de representaciones para un PDF en una carpeta con perfil de recorte inteligente (CQ-4294201).

* Los ajustes preestablecidos de imagen no se publican si el [!UICONTROL modo de sincronización de Dynamic Media] está deshabilitado de forma predeterminada en el Experience Manager con el modo de ejecución Scene7 de Dynamic Media (CQ-4294200).

* El procesamiento de recursos mientras la carga masiva se queda atascada y la instancia de flujo de trabajo muestra instancias atascadas del recurso de actualización DAM (CQ-4293916).

* La creación de una configuración de Dynamic Media en Experience Manager funciona, pero en la interfaz de usuario no sucede nada al seleccionar Guardar (CQ-4292442).

* La previsualización de recursos de vídeo F4V no funciona en la reproducción progresiva en Safari/Mac (CQ-4289844).

* La carpeta adicional se crea al recortar de forma inteligente un recurso que se encuentra dentro de una carpeta principal con un carácter de punto `.` en su nombre (CQ-4289337).

* La miniatura está dañada y la pancarta de procesamiento de vídeo no se muestra cuando se copia un vídeo (CQ-4284125).

* El visor de dimensiones muestra incorrectamente miniaturas vacías en Firefox para algunos modelos con vistas de cámara vacías (CQ-4283447).

* Los problemas de rendimiento corregidos en 6.5.5.0 son (CQ-4279206):

   * Se tarda demasiado en cargar archivos binarios grandes en los servidores de procesamiento de imágenes de Dynamic Media.

   * El tiempo de generación de miniaturas en el Experience Manager aumenta debido a la arquitectura Scene7 de Dynamic Media.

* Los problemas de migración de Dynamic Media Scene7 fallan para clientes con un gran número de recursos (CQ-4279206).

* El diseño del visor de vídeo 360 se interrumpe si se utiliza `setVideo` y el vídeo se desplaza al usar `video= modifier` (CQ-4263201).

* Aparece un mensaje de error al instalar el paquete SDL Experience Manager (NPR-33175).

* Vulnerabilidad del SSRF en Experience Manager (NPR-33435).

### Plataforma {#platform-6550}

* No se llama al filtro [!DNL Sling] si la entrada de mapa `sling:match` se crea en `/etc/maps` (NPR-33362).
* El Experience Manager se bloquea debido a un error de segmentación con [!DNL Apache Lucene] (NPR-32988).
* [!DNL Jackson] falta el paquete principal del archivo uberjar de Experience Manager (NPR-32848).
* CRXDE Lite no carga contenido para usuarios sin permiso de lectura en la propiedad `jcr:primaryType` de un nodo (NPR-32611).
* [!DNL Granite] el Planificador de tarea de mantenimiento se reinicializa con demasiada frecuencia durante las implementaciones de Experience Manager (CQ-4294627).
* Cuando una consulta SQL se ejecuta durante mucho tiempo, por ejemplo 7 horas, el Experience Manager deja de responder (NPR-33044).

### Interfaz de usuario {#ui-6550}

* La selección de botones de radio no persiste en un campo múltiple (NPR-33309).
* El límite de carga diferida no funciona para la vista de lista (NPR-33124).
* La página de resultados de Omniture no muestra un mensaje si no hay coincidencias (NPR-32974).
* El filtro Omnisearch devuelve todas las coincidencias en el nodo `/content`, ignorando la ubicación seleccionada (NPR-32849).

### Integraciones {#integrations-6550}

* La caché interna se borra cuando se publica una página con un componente de Adobe Target (NPR-33162).
* La integración con Adobe Target no funciona con [!DNL Windows Internet Explorer] 11 (NPR-33111).
* Al configurar Adobe Target, los campos [!UICONTROL Compañía] y [!UICONTROL Grupo de informes] no aparecen al seleccionar un origen de sistema de informes (NPR-32502).
* Al exportar [!DNL Experience Fragments] mediante Adobe I/O, los metadatos como Producto de origen no se exportan a Adobe Target (NPR-32159).
* Los usuarios de IMS autorizados en el grupo de administración de Experience Manager locales no pueden crear ni modificar configuraciones de IMS (NPR-33045).
* La página de configuraciones de Inicio de Adobe no muestra todos los registros (NPR-33011).
* Los usuarios del grupo de autores de contenido no pueden editar las propiedades de un componente de Adobe Target debido a un error de JavaScript (NPR-32996).
* Secuencias de comandos entre sitios para JSON (NPR-32744).

### Proyectos de traducción {#translation-6550}

* Las etiquetas traducidas no se importan en Experience Manager desde servicios de traducción de terceros (NPR-33154).
* La página de configuración de traducción muestra un proveedor de traducción incorrecto al que se utilizó para la traducción (NPR-32971).
* Añadir una carpeta de fragmentos de experiencia en un proyecto de traducción existente crea un nuevo proyecto (NPR-32843).
* Se muestra un error `NullPointerException` en los registros de ejecución de un trabajo de traducción (NPR-32628).

### WCM {#wcm-6550}

* Editor de páginas: el [!DNL Sites] Editor de páginas no permite que los usuarios que utilizan solo el teclado pasen al contenido principal en lugar de desplazar el enfoque de la ficha a través de todas las opciones disponibles en el encabezado (CQ-4293883).
* Editor de páginas: los paneles que utilizan el componente Well e incluyen datos guardados no se muestran debido a las actualizaciones en las versiones [!DNL Chrome] y [!DNL Firefox] (CQ-4292995).
* MSM: Al eliminar un componente de la página, no se elimina de la versión publicada de la página (CQ-4292360).

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* Si elimina un esquema de metadatos publicado de [!DNL Brand Portal], se producirá un error (CQ-4292063).
* Si un administrador configura [!DNL Experience Manager Assets] 6.5.4 con Brand Portal a través de Adobe Developer Console, el usuario [!DNL Brand Portal] no puede publicar un recurso de carpeta de contribución de [!DNL Brand Portal] a [!DNL Experience Manager] (NPR-33046).
* Replicación de duplicados de las carpetas principales que causan conflictos (NPR-33001).

### [!DNL Communities] {#communities-6550}

* No se puede eliminar una tarjeta en la consola de moderación mediante la opción de menú de edición rápida (NPR-33117).
* Se produce un error al acceder a la página [!UICONTROL Flujo de Actividad] (NPR-33146).
* Los grupos eliminados en la instancia de autor no se eliminan de todas las instancias de publicación (NPR-33199).
* Después de crear un nuevo grupo, los autores no se redirigen a la sección [!UICONTROL Grupo de la comunidad] de [!DNL Internet Explorer] 11 (NPR-33205).
* El acceso a un mensaje en la Bandeja de entrada del Experience Manager no cambia el estado del mensaje a Leído (NPR-32764).
* Editar un grupo [!DNL Communities] y cambiar la imagen en miniatura no actualiza la imagen en miniatura del grupo (NPR-32599).
* Un usuario no puede enviar un correo electrónico a otro usuario de una comunidad (NPR-32598).
* Un blog enviado no se muestra hasta que el usuario actualiza la página (NPR-32391).
* Al crear una versión de las notificaciones y suscripciones de contenido generado por el usuario (UGC), se almacena un ID incorrecto de la página de origen (CQ-4279355, CQ-4289703).
* Problema de secuencia de comandos entre sitios (NPR-33203).

### Flujo de trabajo {#workflow-6550}

* La opción [!UICONTROL Línea de tiempo] en el carril izquierdo tarda más tiempo en cargarse de lo esperado (NPR-32851).
* Después de reiniciar una instancia de Experience Manager, el correo electrónico de la tarea de revisión de una colección incluye un vínculo de carga útil incorrecto (NPR-32774).

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>Experience Manager Service Pack no incluye correcciones para [!DNL Forms]. Estas se entregan mediante un paquete independiente de complementos de Forms. Asimismo, se ha publicado un instalador acumulativo que incluye correcciones para AEM Forms en JEE. Para obtener más información, consulte [Instalación de Experience Manager Forms Add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) y [Instalación de Experience Manager Forms en JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

* Administración de correspondencia: El orden de los activos en una zona de destinatario se desplaza después de enviar una carta (NPR-33359, NPR-33153).
* Forms adaptable: Cuando un usuario edita un formulario adaptable, la opción [!UICONTROL Flujo de trabajo de Inicio] disponible en el menú [!UICONTROL Información de página] no funciona (NPR-33004).
* Forms adaptable: El usuario no puede guardar un formulario adaptable con más de un archivo adjunto (NPR-32997).
* Forms adaptable: Si se cambia la presentación del panel en un formulario adaptable, se producirá un error (CQ-4293880).
* Forms adaptable: Una nueva línea a una cadena en un diccionario de formularios adaptables agrega `&#xa;` caracteres al diccionario (NPR-33266).
* Accesibilidad adaptable a Forms: Cuando un usuario previsualización un formulario adaptable como un formulario HTML, el campo [!UICONTROL Firma de garabatos] no puede mantener el enfoque de tabulación (NPR-33159).
* Accesibilidad adaptable a Forms: Los mensajes de error que se muestran al enviar un formulario adaptable no se vinculan a un atributo `aria-describedBy` (NPR-33071).
* Accesibilidad adaptable a Forms: Los campos marcados como obligatorios en un formulario adaptable no tienen el atributo obligatorio establecido en True en el esquema de accesibilidad ARIA (NPR-33070).
* Servicio PDFG: Cuando un usuario convierte un archivo de texto a un PDF, los caracteres japoneses no se representan correctamente (NPR-33238).
* Servicio PDFG: La operación `CreatePDF` no puede convertir un archivo PDF a formato OCR PDF (NPR-32994).
* Servicio PDFG: La conversión a PDF falla en la 200ª instancia de un documento [!DNL OpenOffice] (NPR-32766).
* BackendIntegration: Las solicitudes del modelo de datos de formulario fallan al caducar el token de actualización debido a un estado inactivo incorrecto (NPR-33169).
* Designer: Los lectores de pantalla ejecutan el orden de tabulación en función del orden geográfico predeterminado en lugar del orden de tabulación personalizado definido en el archivo XDP (NPR-32160).
* Designer: Si la opción de etiquetado está activada, el borde del subformulario desaparece en la salida PDF generada (NPR-32778).
* XSS almacenado con GuideSOMProviderServlet (NPR-32700).

## Adobe Experience Manager 6.5.4.0 {#experience-manager-6540}

Adobe Experience Manager 6.5.4.0 es una actualización importante que incluye nuevas funciones, mejoras y rendimiento clave solicitados por el cliente, estabilidad y mejoras de seguridad, publicadas desde la disponibilidad general de la versión 6.5 en **abril de 2019**. Se puede instalar sobre Adobe Experience Manager 6.5.

Algunas de las funciones y mejoras clave introducidas en Adobe Experience Manager 6.5.4.0 incluyen:

* Adobe Experience Manager Assets ahora se configura con Brand Portal a través de la consola de Adobe I/O.

* Ahora hay disponible un nuevo paso [Generar salida imprimible](../forms/using/aem-forms-workflow-step-reference.md) para flujos de trabajo de Adobe Experience Manager Forms.

* [Compatibilidad con varias columnas ](../forms/using/resize-using-layout-mode.md) para el modo de presentación de formularios adaptables y comunicaciones interactivas.

* Compatibilidad con [texto enriquecido](../forms/using/designing-form-template.md) en formularios HTML5.

* [Mejoras de ](new-features-latest-service-pack.md#accessibility-enhancements) accesibilidad en Recursos Experience Manager.

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.10.8.

* Ahora puede sincronizar subárboles de contenido selectivo con *Dynamic Media - modo Scene7* en lugar de todo lo disponible en `content/dam`.

* La integración del modelo de datos de formulario con el servicio web SOAP ahora admite grupos de opciones o atributos en los elementos.

* La entrada o salida de SOAP y las estructuras de datos complejas ahora admiten la sustitución dinámica de grupos.

Para obtener una lista completa de las características y los aspectos destacados clave que se han incorporado en los Service Packs más recientes, consulte [Novedades de los Service Packs](new-features-latest-service-pack.md) de Adobe Experience Manager 6.5.

### Sites {#sites-fixes}

* Cuando una dirección URL de una página de Adobe Experience Manager Sites contiene dos puntos (`:`) o un símbolo de porcentaje (`%`), el explorador deja de responder y picos de uso de CPU (NPR-32369, NPR-31918).

* Cuando se abre una página Sitios Experience Manager para editarla y se copia un componente, la acción de pegado permanece no disponible para algunos marcadores de posición (NPR-32317).

* Cuando se abre el asistente Administrar publicación, no se muestra un fragmento de experiencia vinculado a un componente principal en las listas de referencias publicadas (NPR-32233).

* La descripción general de la Live Copy en la IU táctil tarda mucho más que la IU clásica en procesarse (NPR-32149).

* Cuando la hora del servidor y la hora del equipo están en diferentes zonas horarias, la hora de publicación programada muestra la hora del servidor en la IU táctil, mientras que en la IU clásica se muestra la hora del equipo (NPR-32077).

* Sitios Experience Manager no puede abrir una página con un sufijo en la dirección URL (NPR-32072).

* Cuando un usuario edita un fragmento de contenido, se restaura una variación eliminada del fragmento de contenido (NPR-32062).

* Los usuarios pueden guardar un fragmento de contenido sin proporcionar información en los campos requeridos (NPR-31988).

* kernel.js y ui.js no se cumplimentan ni se almacenan en caché. Esto lleva a tiempo adicional en el procesamiento de páginas (NPR-31891).

* Cuando PageEventAuditListener está habilitado, la longitud de la cola de confirmación aumenta. Afecta al rendimiento de muchas operaciones, como la publicación masiva, la navegación y el movimiento masivo de recursos (NPR-31890).

* Cuando se arrastran fragmentos de experiencia, se observa un tiempo de respuesta alto (NPR-31878).

* Cuando selecciona la opción Arrastrar componente aquí en el marcador de posición de una cuadrícula adaptable, se envía una solicitud de GET y la solicitud da como resultado un error HTTP 403 (NPR-31845).

* Al mover el contenido dentro de la misma carpeta, se desactiva la opción de mover la página (NPR-31840).

* En el modo de estructura de plantillas editables, la lista de componentes permitida en el contenedor de diseño muestra resultados incorrectos. En el contenedor de diseño (NPR-31816) solo se muestran los componentes con cuadro de diálogo de diseño.

* Cuando una página tiene permisos de solo lectura para un usuario, la opción Abrir propiedades está visible en sites.html pero no en editor.html (NPR-31770).

* Cuando un usuario hace clic en el botón Crear, la opción de página no está disponible (NPR-31756).

* No se puede sincronizar la campaña en la campaña de Adobe que contiene el componente importador de diseños OOTB (listo para usar) (NPR-31728).

* Cuando se intenta cambiar una lista de viñetas a una lista numerada, solo se cambian los dos primeros elementos de la lista (NPR-31636).

* Cuando se anula la creación de una página y se selecciona el nodo secundario, el cuadro de diálogo de selección aún muestra el nodo inicial. Cuando se crea la página y el usuario hace clic en Examinar, la página se redirige al nodo raíz en lugar del nodo creado (NPR-31618).

* El cuadro de diálogo de configuración de vista no funciona correctamente para la función de flujo de trabajo de personalización de la Bandeja de entrada (NPR-32503 y NPR-32492).

* Aparece un mensaje de error al ver la información del flujo de trabajo mediante la Bandeja de entrada (CQ-4282168).

### Assets {#assets-6540-enhancements}

* El botón para activar el flujo de trabajo en la página de recopilación de recursos está desactivado (NPR-32471).

* Se crea una carpeta sin nombre en SPS (Scene7 Publishing System) mientras se mueve un recurso de una carpeta a otra en Experience Manager con la configuración de Dynamic Media Scene7 (NPR-32440).

* La acción para mover todos los recursos (mediante Seleccionar todo y, a continuación, mover) a una carpeta que contenga recursos publicados falla con error (NPR-32366).

* Error en la generación de representaciones para recursos con ${extension} (NPR-32294).

* Las direcciones URL del historial de versiones se muestran en el campo Referenciado por de la página de propiedades de recursos (NPR-31889).

* El archivo ZIP descargado de DAM no se puede abrir con WinZip (NPR-32293).

* Los permisos originales de una carpeta se actualizan cuando se abre la configuración de la carpeta para cambiar el título de la carpeta o la imagen en miniatura y, a continuación, se guardan (NPR-32292).

* El icono de calendario para la activación programada no se muestra en la columna Estado (en la IU clásica de la lista de recursos DAM) para los recursos cuya activación está programada para una fecha y hora posteriores (NPR-32291).

* La creación de fragmentos de código mediante plantillas de fragmento produce un error al buscar colecciones durante el proceso de creación de fragmentos (NPR-32290).

* Se activan varias consultas de búsqueda cuando se seleccionan varias etiquetas en el filtro de búsqueda (NPR-32143).

* La interfaz de usuario de Recursos Experience Manager muestra nombres de archivo truncados cuando se cargan recursos con más de 50 caracteres en el nombre de archivo (NPR-32054).

* Todas las casillas de verificación del panel Filtro se desactivan cuando se desactivan la primera y la segunda casillas de verificación, cuando se seleccionan las casillas de verificación del nivel dos del árbol de casillas de verificación en Adobe Stock (NPR-31919).

* La búsqueda de archivos y carpetas mediante facetas de Omnisearch ofrece una excepción (NPR-31872).

* El resaltado de campos para la selección obligatoria de campos en el editor de metadatos no se elimina ni siquiera después de seleccionar el campo requerido, cuando las reglas de dependencia se establecen en el correspondiente formulario de esquema de metadatos (NPR-31834).

* Los nombres completos de las etiquetas de nivel de hoja (de la jerarquía de etiquetas) no se muestran en la página Propiedades del recurso (NPR-31820).

* El uso del comando posterior de la página Propiedades del recurso en el navegador Safari genera un error (NPR-31753).

* La página de resultados de la búsqueda por IU táctil (realizada a través de Omnisearch) se desplaza automáticamente hacia arriba y pierde la posición de desplazamiento del usuario (NPR-31307).

* La página de detalles de recursos de los recursos PDF no muestra botones de acción excepto los botones Para colección y Añadir representación en el Experience Manager que se ejecuta en el modo de ejecución de Dynamic Media Scene7 (CQ-4286705).

* Los recursos tardan demasiado en procesarse mediante el proceso de carga por lotes de Scene7 (CQ-4286445).

* El botón Guardar no importa Conjunto remoto cuando el usuario no ha realizado ningún cambio en el Editor de conjuntos en el cliente de Dynamic Media (CQ-4285690).

* La miniatura de un recurso 3D no es informativa cuando se ingesta un modelo 3D compatible en un Experience Manager (CQ-4283701).

* El estado sin procesar del ajuste preestablecido de visor de vídeo de recorte inteligente aparece dos veces en el texto de la pancarta junto con el nombre del ajuste preestablecido (CQ-4283517).

* En la página de detalles del recurso (CQ-4283309) se observa una altura de contenedor incorrecta de un modelo 3D cargado con vista previa en el visor 3D.

* El Editor de carrusel no se abre en IE 11 en modo Dynamic Media híbrido Experience Manager (CQ-4255590).

* El enfoque del teclado se queda atascado en la lista desplegable Correo electrónico del cuadro de diálogo Descargar, en los navegadores Chrome y Safari (NPR-32067).

* La casilla de verificación Sincronizar todo el contenido no está habilitada de forma predeterminada al intentar agregar la configuración de la nube DM en el Experience Manager (CQ-4288533).

### Interfaz de usuario de base {#foundation-ui-6540}

* El control del ratón cambia al campo de filtro anterior en lugar de permanecer en el campo de filtro existente al buscar recursos con el panel Filtro (NPR-32538).

* Etiquetado de plataforma: Para buscar etiquetas, escriba en los campos de etiqueta, se muestran las etiquetas situadas fuera de los límites raíz y no respeta la propiedad `rootPath` de los campos de etiqueta (NPR-31895).

* Interfaz de usuario de plataforma: El navegador de rutas se interrumpe si se agrega una ruta no válida en el campo de texto (NPR-31884).

* La notificación se oculta detrás de un menú adhesivo en la selección de página (NPR-31628).

### Plataforma {#platform-sling-6540}

* (HTL) Los caracteres de subrayado reemplazan los dos puntos en la sección de ruta de la dirección URL (NPR-32231).

### Proyectos {#projects-6540}

* El botón Crear no está visible para el usuario aunque éste tenga permiso para crear un proyecto en la subcarpeta (NPR-31832).

### Traducción de proyectos {#projects-translation-6540}

* La creación de proyectos de traducción interrumpe la interfaz de usuario cuando se activa la opción Recortar espacios en `Apache Sling JSP Script Handler` (NPR-32154).

* Se observa un error en la interfaz de usuario y una excepción de punto nulo en los registros de errores cuando se agrega cualquier etiqueta a un proyecto de traducción (NPR-31896).

### Integraciones {#integrations-6540}

* La generación de direcciones URL de la biblioteca de inicio se basa únicamente en los valores `path` y `library_name` de la API de inicio y no en el valor `library_path` (NPR-31550).

* Aparece un mensaje de error al procesar los elementos relacionados con LiveFile (FYR-12420).

* ReportSuitesServlet es vulnerable a SSRF (NPR-32156).

### Editor de plantillas WCM {#wcm-template-editor-6540}

* En el modo de estructura de plantillas editables, la lista de componentes permitida en el contenedor de diseño no muestra el componente de botón de vínculo (CQ-4282099).

### Editor de páginas WCM {#wcm-page-editor-6540}

* Se observa un error al seleccionar una superposición y, a continuación, seleccionar una cuadrícula adaptable Arrastre los componentes aquí (CQ-4283342).

### Objetivo de campaña {#campaign-targeting-6540}

* La configuración de la nube de destinatario falla con el error al obtener la solicitud de mboxes (CQ-4279880).

### Brand Portal {#assets-brand-portal-6540}

* Los usuarios de Brand Portal no pueden publicar recursos de carpetas de contribución en [!DNL Assets] al actualizar a Adobe I/O en Experience Manager 6.5.4 (CQDOC-15655). Para una corrección inmediata en Experience Manager 6.5.4, se recomienda [descargar la revisión](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) e instalarla en la instancia de creación.

* Los valores emergentes de esquema de metadatos no están visibles en las propiedades del recurso (CQ-4283287).

* El subesquema de metadatos no muestra fichas basadas en mimetype en propiedades de recursos (CQ-4283288).

* El esquema Cancelar la publicación de metadatos rellena un mensaje de error aunque el esquema se elimina al final.

* La imagen de previsualización no se muestra para un recurso publicado (CQ-4285886).

* El usuario no puede publicar ni cancelar la publicación de recursos que contengan una sola cotización en el nombre (CQ-4272686).

* Los términos y condiciones no se muestran al descargar varios recursos (CQ-4281224).

* Se han solucionado pequeñas vulnerabilidades de seguridad.

### Communities {#communities-6540}

* El formulario Crear miembro se muestra como una página en blanco (NPR-31997).

* El usuario no puede realizar la vista del informe de Analytics en la instancia de autor (NPR-30913).

### Oak- Indexación y Consultas {#oak-indexing-6540}

* Los documentos de Microsoft Word y MS Excel, que contienen imágenes JPEG, cuando se analizan con el analizador Tika no se analizan y se observa un error de clase no encontrada (NPR-31952).

### Forms {#forms-6540}

>[!NOTE]
>
>Experience Manager Service Pack no incluye correcciones para Experience Manager Forms. Estas se entregan mediante un paquete independiente de complementos de Forms. Además, se ha publicado un instalador acumulativo que incluye correcciones para Adobe Experience Manager Forms en JEE. Para obtener más información, consulte [Instalación de Experience Manager Forms Add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) y [Instalación de Experience Manager Forms en JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

* Administración de correspondencia: Las letras muestran caracteres adicionales después del envío a los flujos de trabajo del proceso de publicación (NPR-32626).

* Administración de correspondencia: Las letras muestran un marcador de posición desplegable como un componente de texto después de enviarlo a flujos de trabajo posteriores al proceso (NPR-32539).

* Administración de correspondencia: Los valores predeterminados definidos en la plantilla de letras no se muestran en el modo de Previsualización (NPR-32511).

* Forms móvil: El botón de envío se muestra con un tamaño ampliado mientras se procesa un formulario XDP en una versión HTML (NPR-32514).

* Servicios de documento: Problemas de acceso a URL para cartas y otras páginas después de aplicar Service Pack 2 (NPR-32508, NPR-32509).

* Servicios de documento: Si el número de transacciones en un servidor supera un límite específico, la conversión de HTML a PDF falla y la configuración del tipo de archivo se elimina del servidor [!DNL Forms] (NPR-32204).

* Forms adaptable: La herramienta de accesibilidad de navegadores informa de errores en formularios adaptables según las directrices WCAG2 de nivel AA (NPR-32312, NPR-32309, CQ-4285439).

* Forms adaptable: La herramienta de accesibilidad del navegador Chrome informa de un error de práctica recomendada (NPR-32310).

* Forms adaptable: Problemas de traducción al configurar un formulario adaptable incrustado en una página Sitios Experience Manager (NPR-32168).

* Área de trabajo: Aparece un mensaje de error al utilizar la operación Obtener propiedades de PDF para el servicio Utilidades de PDF (NPR-32150).

* Seguridad de documento: Un archivo PDF protegido no se puede abrir sin conexión con la opción DisableGlobalOfflineSynchronizationData establecida en True (NPR-32078).

* Designer: Si la opción de etiquetado está activada, el borde del subformulario desaparece en la salida PDF generada (NPR-32547, NPR-31983, NPR-31950).

* Designer: Si hay celdas combinadas en una tabla, la prueba de accesibilidad falla para el archivo PDF de salida convertido desde un formulario XDP mediante el servicio de salida (CQ-4285372).

* Foundation JEE: Si un servidor Forms Experience Manager está desconectado de un clúster, los problemas de almacenamiento en caché impiden que se vuelva a conectar al servidor (NPR-32412).

## Adobe Experience Manager 6.5.3.0 {#experience-manager-6530}

[!DNL Adobe Experience Manager] 6.5.3.0 es una versión importante que incluye correcciones y mejoras clave para el cliente, de rendimiento, estabilidad y seguridad, publicadas desde la disponibilidad general de la versión 6.5 en  **abril de 2019**. Se puede instalar sobre [!DNL Adobe Experience Manager] 6.5.

Algunos aspectos destacados de esta versión del Service Pack son:

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.10.6.

* [!DNL Experience Manager Assets] ahora admite archivos ZIP creados con el algoritmo Deflate64.

* Se ha agregado una nueva columna para la fecha de creación, que es ordenable, en la vista de lista DAM y en los resultados de búsqueda de recursos en la vista de listas.

* La clasificación de recursos basada en la columna Nombre se ha activado en la vista de Listas.

* [!DNL Dynamic Media] ahora admite recursos de vídeo de recorte inteligente. Smart Crop es una función de aprendizaje automático que vuelve a recortar un vídeo mientras mueve el fotograma para seguir el punto focal de la escena.

* [!DNL Dynamic Media] admite imágenes inteligentes.

* Capacidad para [establecer las preferencias de Fuera de Office](../forms/using/configure-out-of-office-settings.md) en flujos de trabajo [!DNL Experience Manager].

* Capacidad para [compartir elementos de la Bandeja de entrada o de la Bandeja de entrada](../forms/using/configure-shared-queues-osgi.md) con otros usuarios en flujos de trabajo [!DNL Experience Manager].

* Capacidad para [generar comunicaciones interactivas en modo por lotes](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

* Se ha actualizado la versión de jQuery incluida en ContextHub a 3.4.1.

### Recursos {#assets-6530-enhancements}

**Mejoras del producto**

* [!DNL Experience Manager Assets] ahora admite archivos ZIP creados con el algoritmo Deflate64 (NPR-27573).

* Se agrega una nueva columna para la fecha de creación, que es ordenable, en la vista de lista DAM y en los resultados de búsqueda de recursos en la vista de listas (NPR-31312).

* En la vista de lista, los usuarios pueden ordenar la lista de los recursos mediante la columna [!UICONTROL Name] (NPR-31299).

* Los archivos GLB, GLTF, OBJ y STL se pueden previsualizar en la página [!UICONTROL Detalles del recurso] de DAM (CQ-4282277).

* `ReplicationOnModifyListener` El evento se activa para nodos de fragmento durante la carga de fragmentos en  [!DNL Dynamic Media] (CQ-4281279).

* [!DNL Dynamic Media] ahora admite recursos de vídeo de recorte inteligente. Smart Crop es una función de aprendizaje automático que vuelve a recortar un vídeo mientras mueve el fotograma para seguir el punto focal de la escena (CQ-4278995).

* [!DNL Dynamic Media] admite imágenes inteligentes (CQ-422249).

* La vista de búsqueda o exploración se establece como la vista predeterminada en el selector de base si se pasan parámetros de consulta en la solicitud (NPR-31601).

**Correcciones**

* Los metadatos de algunos documentos PDF no se actualizan ni se guardan en el PDF cuando se modifica su título (NPR-31629).

* El uso compartido de recursos no funciona para un recurso que tiene más caracteres (`+`) en el nombre del archivo (NPR-31547).

* Las ediciones en el formulario de búsqueda predeterminado Recursos Administración Raíl de búsqueda no funcionan del modo esperado (NPR-31502).

* Las sugerencias no se muestran cuando se utiliza Omnisearch en la vista de recursos para buscar recursos (NPR-31496).

* Las referencias de recursos dentro de las colecciones no se actualizan cuando los recursos a los que se hace referencia se mueven a otra ubicación, en casos en los que diferentes usuarios hacen referencia a los mismos recursos (NPR-31486).

* Las etiquetas IPTC de duplicado se agregan a los metadatos de los recursos (NPR-31328).

* El recuento de resultados de búsqueda no se actualiza con precisión cuando se activa una búsqueda desde el carril del filtro (NPR-31316).

* Todas las casillas de verificación se desactivan al anular la selección de las casillas de verificación de segundo nivel en el filtro Tipo de archivo y el texto de la barra de búsqueda no está sincronizado con las propiedades seleccionadas o no seleccionadas (NPR-31287).

* No se pueden quitar todos los miembros (usuarios/grupos) de la sección Miembros de una carpeta; al intentar eliminar todos los usuarios, el usuario que ha iniciado sesión se agrega a la lista (NPR-31171).

* Los recursos con símbolo más (`+`) en el nombre del archivo no se pueden eliminar (NPR-31162).

* El menú desplegable Crear, que está visible en el menú superior al seleccionar una carpeta, no muestra &#39;Carpeta&#39; como opción de creación (NPR-30877).

* Selección de carpetas Crear > Elemento de acción FileUpload no aparece cuando se aplican las opciones ACL de Denegar `jcr:removeChildNodes` y `jcr:removeNode` en ruta a un usuario (NPR-30840).

* Los flujos de trabajo DAM pasan a un estado antiguo cuando se cargan determinados recursos mp4, lo que provoca que todos los flujos de trabajo restantes pasen a un estado antiguo (NPR-30662).

* Error de memoria insuficiente cuando se carga un archivo PDF grande (de varios gigabytes) en DAM y se procesan sus subrecursos (NPR-30614).

* El movimiento masivo de recursos está fallando y mostrando un mensaje de advertencia (NPR-30610).

* Los nombres de los recursos se cambian a minúsculas al mover recursos de una carpeta a otra en [!DNL Experience Manager] modo [!DNL Dynamic Media]-Scene7 (NPR-31630).

* Se observa un error al editar un conjunto de imágenes remoto para la imagen que reside en la carpeta con el mismo nombre que el nombre de compañía de Scene7 (NPR-31340).

* [!DNL Dynamic Media] los recursos que contienen referencias no se publican (NPR-31180).

* Las cargas del modo [!DNL Dynamic Media]7-Scene7 a [!DNL Dynamic Media Classic] tardan demasiado en completarse (NPR-31048).

* La zona interactiva añadida a un recurso de imagen no es visible a través del visor de imágenes interactivo en la página de detalles de recursos (NPR-30979).

* Se crean enormes trabajos de sling y vuelve a aparecer la pancarta de procesamiento cuando las acciones realizadas en recursos en [!DNL Experience manager Assets] se pasan a Scene7 (NPR-30947).

* El conflicto se produce al crear una copia de idioma de los recursos y no se carga en Scene7 (NPR-30932).

* Las representaciones dinámicas descargadas de [!DNL Experience Manager] que se ejecutan en el modo [!DNL Dynamic Media]-híbrido están dañadas (son de tipo texto con contenido que &#39;no puede encontrar la imagen&#39; en lugar de tipo de contenido de imagen) (NPR-30876).

* [!DNL Dynamic Media] El flujo de trabajo de codificación de vídeo no puede generar miniaturas para el vídeo que se ha migrado  [!DNL Dynamic Media Classic] al modo  [!DNL Dynamic Media]-Scene7 en Adobe Experience Manager (CQ-4282011).

* Se ha observado una excepción IpsApiException al migrar recursos de una instancia a otra con diferentes ID de compañía de Scene7 (CQ-4280548).

* La miniatura del recurso 3D no es informativa, cuando se ingesta un modelo 3D compatible en [!DNL Experience Manager] (CQ-4283701).

* Los botones de desplazamiento se muestran en el visor si un recurso 3D tiene pocas vistas de cámara (CQ-4283322).

* Altura incorrecta del contenedor de un modelo 3D cargado previsualizado en la página de detalles de recursos de Dimensional Viewer (CQ-4283309).

* Los vídeos no se pueden reproducir con SmartCropVideoViewer en Internet Explorer 11 y Safari (CQ-4281422).

* El uso del botón mover para mover varios recursos, de una carpeta a otra, falla en [!DNL Experience Manager] ejecución en el modo de ejecución [!DNL Dynamic Media]-Scene7 (CQ-4280384).

* El vídeo distorsionado se ve en los detalles del recurso cuando el tipo MIME no es MP4 (CQ-4279704).

* Los vídeos recientemente ingestados en carpetas con perfil de vídeo permanecen en estado de procesamiento incluso después de que el porcentaje de codificación se complete al 100 % (CQ-4279389).

* Al mover recursos desde una carpeta, se crea un gran número de trabajos de sling (llamadas a la API de Scene7) que lo que se necesita de forma ideal (CQ-4278664).

* Los nombres del conjunto de imágenes se cambian a minúsculas en Scene7 cuando se crea un conjunto de imágenes (o conjunto de medios) y se les asigna un nombre con la convención de nombres adecuada en DAM (CQ-4281112).

* Scene7 Migrator establece el estado de publicación incorrectamente (CQ-4263492).

* La página de resultados de la búsqueda por IU táctil (realizada a través de Omniture) se desplaza automáticamente hacia arriba y pierde la posición de desplazamiento del usuario en los fragmentos de contenido (CQ-4282898).

* Los archivos PDF no se indexan y el contenido dentro de no se puede buscar (CQ-4278916).

* Error &quot;Grupo no enumerado por selector de usuario: se espera que false sea igual a true&quot; al agregar Closed User Group con `principalName` y `authorizableId` (CQ-4278177) diferentes.

* La Vista de columna de la interfaz de usuario de recursos muestra todas las rutas, independientemente de la ruta raíz de la presa específica del inquilino (CQ-4278175).

* La búsqueda del selector de recursos no funciona correctamente (CQ-4275886).

* Los Flujos de trabajo de representación fallan (CQ-4271928).

* Depuración de Evento DAM elimina los datos de evento más recientes (`maxSavedActivities`) y contiene los datos creados anteriormente (NPR-31336).

* La página de resultados de la búsqueda por IU táctil (realizada a través de Omnisearch) se desplaza automáticamente hacia arriba y pierde la posición de desplazamiento del usuario (NPR-31307).

* La barra de acciones y el recuento de recursos no se actualizan al seleccionar todo y, a continuación, anular la selección de algunos elementos (carpetas/recursos individuales) en la IU táctil (NPR-31118).

* Se muestra una excepción en [!DNL Experience Manager] al sondear los detalles de un trabajo de un recurso (CQ-4283569).

### Sites

* Si la herencia de LiveCopy está dañada, las páginas de Live Copy muestran vínculos de copia de idioma en lugar de vínculos de LiveCopy (NPR-30980).
* Para un nuevo modelo, si el número de registros es superior a 40, solo se muestran los primeros 40 registros. El modelo muestra líneas en blanco para el resto de los registros (NPR-31182).
* Cuando un usuario agrega caracteres japoneses o coreanos en la propiedad description de un menú, el menú muestra caracteres distorsionados para texto en japonés y coreano (NPR-31331).
* El editor de texto enriquecido (RTE) no permite insertar una tabla incrustada como elemento de lista (NPR-30879).
* Fuera de la casilla, scaffolding Rich Text Editor (RTE). aplica tamaño de fuente en línea a los elementos de forma inesperada (NPR-31284).
* Cuando un usuario se centra en los campos del carril izquierdo y utiliza un método abreviado de teclado para pegar contenido, pega el contenido del portapapeles del editor de páginas en lugar del contenido copiado de los campos del carril izquierdo (NPR-31172).
* Cuando un usuario agrega un campo Carga de archivo a un campo múltiple, la ruta de la imagen se almacena en el nodo del componente en lugar del nodo de varios campos (NPR-30882).
* La API `ResponsiveGridExporter` no devuelve la interfaz `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter`. El paquete `com.day.cq.wcm.foundation.model.impl` se declara como un paquete privado (NPR-31398).

<!-- Review: NPR-31398 has fixVersion as 6530. However, it is mentioned twice in 6530 and 6520 as fixed. 
Remove one mention of this fix.
-->

* Cuando se abre una página que contiene algunos fragmentos de experiencia en modo que no es de editor (ya sea en Autor sin el prefijo `editor.html` y `wcmmode=disabled` o en Editor), la solicitud termina en código de error de estado HTTP `500` (NPR-30743).
* Los usuarios no pueden cambiar su contraseña ni acceder a su página de perfil (NPR-31161).

### Búsqueda e interfaz de usuario {#ui-interface-and-search}

* Al cambiar de la vista de tarjeta a la vista de lista en una página de resultados de búsqueda, hay un retraso antes de que la página se pueda desplazar (NPR-31286).

* La casilla [!UICONTROL Seleccionar todo] está oculta en la vista de lista de la interfaz de usuario [!DNL Sites] (NPR-31614).

* El recuento [!UICONTROL Seleccionar todo] en una página de resultados de búsqueda es incorrecto (NPR-31120).

* El editor de metadatos muestra etiquetas que no existen (NPR-31119).

### Traducción {#translation}

* Aparecen dos ventanas emergentes de calendario al seleccionar la opción Fecha de vencimiento en un trabajo de traducción (NPR-31270).

### Plataforma

* La opción Tipo de MIME en la consola web no funciona (NPR-31108).

* El certificado de cliente no se acepta al configurar el inicio de sesión único (NPR-31165).

* Las actualizaciones en la configuración del tamaño del búfer para el servicio HTTP basado en Jetty no se guardan (NPR-30925).

* QueryBuilder ahora admite pedidos por `fn:name()` en consultas xpath (NPR-31322).

* El árbol de activación de duplicado se crea al actualizar desde [!DNL Experience Manager] 6.3 (NPR-31513).

* Las solicitudes reenviadas no conservan los encabezados de respuesta establecidos durante la autenticación sling (NPR-30013).

* La búsqueda dentro de los componentes del selector no funciona (NPR-31692).

* Se muestra un error al adjuntar un archivo ZIP a una publicación [!DNL Experience Manager Communities] debido a diferentes versiones del paquete Apache POI y Apache Tika (NPR-31018).

* El paquete `org.apache.sling.distribution.api` está oculto en el administrador de configuración y, por lo tanto, no está disponible para paquetes personalizados (NPR-31720).

### Proyectos

* El cambio de vistas de calendario no funciona (NPR-31271).

### Brand Portal {#assets-brand-portal-6530}

**Mejoras del producto**

* El flujo de trabajo de importación de Asset Sourcing en [!DNL Experience Manager Assets] se modifica para recuperar solamente los recursos recién creados de [!DNL Brand Portal] a [!DNL Experience Manager] y omitir los recursos que ya existen en la NUEVA carpeta para evitar la replicación (CQ-4278527).

**Correcciones**

* Aparece un icono incorrecto al crear una nueva carpeta de contribución en la función de fuentes de recursos (CQ-4282825).
* Al crear una nueva carpeta Contribution, una o ambas subcarpetas (NUEVAS y COMPARTIDAS) no aparece dentro de la carpeta Contribution (CQ-4282424).
* El sistema emite una excepción si el usuario intenta volver a publicar la carpeta Contribution de [!DNL Experience Manager] a [!DNL Brand Portal] después de recibir nuevos recursos en la carpeta Contribution desde [!DNL Brand Portal] extremo (CQ-4279740).
* La creación de la carpeta Contribution dentro de una carpeta Contribution (carpeta anidada) está prohibida para evitar la complejidad (CQ-4278391).
* El sistema genera una excepción al cargar la lista de usuario [!DNL Brand Portal] (archivo .csv) importada desde el Admin Console [!DNL Experience Manager]. Solo son obligatorios los campos Correo electrónico, Nombre y Apellido del archivo .csv (CQ-4278390).

### Comunidades {#communities-6530}

**Correcciones**

* Los vínculos rápidos para administrar grupos (Abrir/Editar/Publicar/Eliminar grupos) no son visibles para los administradores de la comunidad (administrador del grupo/administrador del sitio) (NPR-31627).
* Un blog enviado no se muestra a menos que la página se actualice o recargue manualmente (NPR-31599).
* La consulta JCR utilizada por la función &quot;Menciones&quot; distingue entre mayúsculas y minúsculas y tarda demasiado en devolver resultados (NPR-31475).
* [!DNL Experience Manager] 6.5 El archivo UberJar emite una excepción; falta el  `cq-social-translation` paquete del archivo  [!DNL Experience Manager] 6.5 UberJar (NPR-31186).
* Las bibliotecas del enlace de datos Jackson se actualizaron a la versión 2.9.9.3 para abordar nuevas vulnerabilidades (NPR-30967).
* Los títulos de las actividades y las notificaciones son incoherentes (NPR-30941).
* La paginación no funciona correctamente en [!DNL Communities] blogs (NPR-30914).
* Los informes de Analytics no se rellenan en el entorno de creación [!DNL Experience Manager]; aparece una página en blanco (NPR-30913).

### Oak {#oak}

* Las actualizaciones del índice de Lucene hacen que el servidor de creación se ralentice (NPR-31548).

### Forms {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack no incluye correcciones para  [!DNL Experience Manager Forms]. Estas se entregan mediante un paquete independiente de complementos de Forms. Además, se ha publicado un instalador acumulativo que incluye correcciones para [!DNL Experience Manager Forms] en JEE. Para obtener más información, consulte [Instalación de Experience Manager Forms Add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) y [Instalación de Experience Manager Forms en JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

#### Paquete de complemento de Forms {#forms-add-on-package-6530}

**Formularios adaptables**

* Las cadenas contienen la clave del diccionario al localizar formularios adaptables (NPR-31110).

**Comunicación interactiva**

* **MissingNode.toString()** devuelve resultados inexactos después de actualizar las bibliotecas de Jackson a 2.10.0 (NPR-31549).

* El editor de texto elimina aleatoriamente los caracteres de espacio del texto copiado de Microsoft Word (NPR-31113).

**Administración de correspondencia**

* Los rótulos y la información sobre herramientas no se muestran al migrar letras de LiveCycle ES4SP1 a [!DNL Experience Manager] 6.5 (NPR-31615).

* **El formato de flujo de texto ya no es** compatible. Se muestra un mensaje de error mientras se guardan letras como borradores (NPR-30463).

**Flujo de trabajo**

* El flujo de trabajo de OSGi falla debido a la utilización del 100% de la CPU (NPR-31233).

**HTML5 Forms**

* Al generar la vista previa HTML5 de un formulario XDP, se muestra un parpadeo al agregar instancias de un subformulario (NPR-30909).

#### Instalador de Forms en JEE {#forms-jee-installer-6530}

**Forms: servicios de documentos**

* El servicio web SOAP que utiliza MTOM en un proyecto .NET muestra excepciones para los métodos AssemblerServiceClient invoke y HtmlToPDF2 (NPR-4281771).

* Vulnerabilidad de seguridad 2012-5784 y 2014-3596 encontrada con AXIS 1.4 jar, y corrección proporcionada con [AXIS1.4.1 jar](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0014.html) (NPR-31015).

**Base JEE**

* La configuración de la acción no carga los nombres de proceso para Invocar una acción de envío de Forms Workflow (NPR-31478).

### Paquetes de funciones incluidos {#feature-packs-included-6530}

>[!NOTE]
>
>Para los clientes [!DNL Experience Manager Forms], es esencial instalar el paquete de complementos [!DNL Experience Manager Forms] después de instalar cualquier Service Pack, paquete de correcciones acumulativas o paquete de funciones [!DNL Experience Manager].

#### Forms: base JEE {#forms-foundation-jee-feature}

* [!DNL Experience Manager] Compatibilidad de Forms con Oracle 18c (NPR-29155).

## Adobe Experience Manager 6.5.2.0 {#experience-manager-6520}

[!DNL Adobe Experience Manager] 6.5.2.0 es una versión importante que incluye correcciones y mejoras clave de rendimiento, estabilidad, seguridad y del cliente publicadas desde la disponibilidad general de  [!DNL Adobe Experience Manager] 6.5 en  **abril de 2019**. Se puede instalar sobre [!DNL Experience Manager] 6.5.

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

### Assets

**Mejoras del producto**

* Se mejoró la funcionalidad de los recursos conectados para añadir la compatibilidad con la recuperación de documentos desde implementaciones de DAM remotas. Los autores del sitio pueden buscar y filtrar los tipos de documentos admitidos en el Buscador de contenido. Los documentos remotos se pueden agregar al componente Descargar en páginas web. Revisión para CQ-4270245. Consulte [Uso de activos conectados](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Experience Manager Assets] los usuarios pueden buscar imágenes visualmente similares. [!DNL Experience Manager] muestra las imágenes con etiquetas inteligentes del repositorio de DAM similares a una imagen seleccionada por el usuario. Consulte [Búsqueda visual](../assets/search-assets.md#visualsearch).

**Correcciones**

* Las rutas de recursos de las direcciones URL y los metadatos de las carpetas que genera la API de ACP no son URL codificadas. GRANITE-26198: revisión para CQ-4271814
* La descompresión de un archivo con una carpeta con un signo de porcentaje (%) en su nombre no se puede abrir con la interfaz [!DNL Experience Manager Assets]. NPR-29989: revisión para CQ-4270467
* IU táctil: Durante el asistente para administrar la publicación, las referencias se agregan después de la página en el cuerpo de la solicitud de publicación, lo que provoca que todos los recursos se publiquen después de la página y, cuando se procesa la página, se pierden algunos de los recursos de la instancia de publicación. NPR-29985: revisión para CQ-4270724
* La función de recursos no relacionados no funciona en recursos relacionados que tienen caracteres especiales (caracteres que se codifican con el URI) en el nombre. NPR-30387: revisión para CQ-4274446
* Al editar un fragmento de contenido, la versión se crea con el usuario incorrecto.
* Error durante la creación de colecciones en el sistema basado en inquilinos. NPR-30114: revisión para CQ-4272948
* La vista de columnas de la IU de recursos no respeta la ruta raíz de DAM del inquilino actual, pero accede a todas las rutas de DAM del inquilino. NPR-30636: revisión para CQ-4275481
* Posible ejecución de scripts en sitios múltiples a través de la ventana de alerta de archivos restringidos, ya que la imagen insertada se puede ver. NPR-30617: revisión para CQ-4270133
* MultiTenant: Los inquilinos que guardan las propiedades de la carpeta observan que tanto el mensaje de éxito como el mensaje de error que describe la acción no se han realizado correctamente: &quot;No se pueden editar las propiedades. Permisos insuficientes&quot;. Esto, por lo tanto, puede causar confusión. NPR-30545: revisión para CQ-4275333
* El cuadro de diálogo del selector de recursos no permite la selección de recursos, por lo que no se puede actualizar el origen con la funcionalidad de reemplazo de origen relacionada. NPR-30502: revisión para CQ-4275029
* [!UICONTROL Flujo de ] trabajo de recursos de actualización de DAM: en el estado antiguo al cargar archivos mp4 de gran tamaño. NPR-30480: revisión para CQ-4271352
* La funcionalidad para crear la tarea de revisión no funciona debido a una carga útil nula que provoca que todas las acciones relacionadas con la tarea de revisión subsiguientes no funcionen. NPR-30468: revisión para CQ-4274263
* Problema de conectividad de etiquetas inteligentes de Adobe a través de Datapower. NPR-30026: revisión para CQ-4269457
* La vista de columnas de la IU de recursos genera un error al intentar abrir los filtros en el carril izquierdo. NPR-30501: revisión para CQ-4273862
* Al agregar grupos sincronizados desde LDAP en las propiedades del grupo de usuarios cerrado (CUG) de una carpeta de recursos, el grupo no se guarda ni se recupera. NPR-30615: revisión para CQ-4274689
* Los campos de orientación y estilo de búsqueda de filtro no aplican el valor completado automáticamente a la consulta de búsqueda. NPR-30620: revisión para CQ-4275724
* El vínculo de uso compartido de los recursos de una carpeta con espacio y carácter &quot;&amp;&quot; en el nombre, muestra elementos en gris vacíos en algunos recursos. NPR-30557: revisión para CQ-4270187
* El formulario del esquema de metadatos de carpeta no detecta automáticamente el tipo de datos y, por lo tanto, no crea el elemento TypeHint relacionado al enviar el formulario. NPR-30599: revisión para CQ-4275227
* Las opciones de edición de recorte y rotación de recursos están desactivadas en la IU de creación de DMS7. NPR-30118: revisión para CQ-4273221
* La función Compartir vínculo no funciona en la instancia [!DNL Experience Manager] con la configuración de DMS7. NPR-30080, NPR-30492: revisión para CQ-4273651
* Añadir el componente [!DNL Dynamic Media]-Scene7 a la página y luego publicar la página no activa la configuración de dmscene7 cada vez. NPR-30641: revisión para CQ-4275962
* Se añadió un IPSJobJournal en [!DNL Experience Manager] para crear solo un trabajo de sistemas de prevención de intrusiones (IPS) por perfil de procesamiento. NPR-30490: revisión para CQ-4273614
* [!DNL Dynamic Media]:: Se han añadido filtros predeterminados para excluir recursos de la replicación en el nodo de  [!DNL Experience Manager] publicación. NPR-30538: revisión para CQ-4274678
* Se ha introducido un flujo de trabajo de reprocesamiento externo para la compatibilidad con varios recursos a fin de permitir que la carpeta sea una carga útil. El flujo de trabajo consta de dos pasos: vuelve a procesar los recursos sin controladores mediante el mapa de metadatos al paso siguiente y vuelve a cargar todos los recursos sin el control de recursos en S7 en un solo trabajo de IPS. Para obtener más información, consulte Configuración de Cloud Services [!DNL Dynamic Media]. NPR-30489: revisión para CQ-4272903
* Al cargar un archivo CSV incorrecto después de uno correcto, se elimina el archivo CSV correcto. Revisión para CQ-4277694, CQ-4277814
* Se va a eliminar el icono incorrecto específico de las carpetas de contribución. Revisión para CQ-4277580
* Al seleccionar un usuario en el selector de usuarios de la ficha Contribución de recursos, el nombre del usuario no aparece en la tabla y el cuadro de diálogo Eliminar usuario que está en la página Propiedades muestra un texto incorrecto. Revisión para CQ-4277875
* Los colaboradores no se pueden agregar a la carpeta de Contribución de recursos desde el selector de usuarios al seleccionar al usuario y hacer clic en Añadir. Revisión para CQ-4277824, CQ-4278087
* La búsqueda por nombre de usuario en minúsculas no funciona en el selector de usuarios. Revisión para CQ-4277958, CQ-4277930
* Los usuarios que no son administradores pueden publicar recursos en una nueva carpeta que esté en una carpeta de contribución de recursos. Revisión para CQ-4278200
* dam-user (no es administrador) no tiene la opción de añadir colaboradores a la carpeta de contribución de recursos. Revisión para CQ-4278192
* El botón &quot;Crear&quot; está visible en la carpeta de contribución de recursos. Revisión para CQ-4277560
* La ordenación de la consulta de búsqueda por relevancia devuelve [!DNL InDesign] documentos junto con [!DNL InDesign] plantillas. Revisión para CQ-4273864
* Si el usuario tiene un id. de correo electrónico en mayúsculas, los usuarios no pueden registrar los recursos que ya se han extraído. Revisión para CQ-4276575
* La operación Eliminar solo se aplica a los ajustes preestablecidos seleccionados y, si la pantalla actualiza automáticamente la lista después de la operación, se muestran otros ajustes preestablecidos que ya se han actualizado. Revisión para CQ-4261461
* La configuración de Cloud Services [!DNL Dynamic Media] en el modo [!DNL Dynamic Media]-híbrido resulta en varios grupos de informes vacíos creados en [!DNL Analytics] y sin ID de grupo de informes almacenados en [!DNL Experience Manager], lo que resulta en una duplicación de grupos de informes. Revisión para CQ-4249780
* No se puede sincronizar la operación de cambio de nombre del recurso en [!DNL Experience Manager] con el nombre duplicado en Scene7. Revisión para CQ-4276763
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

* Si la herencia de LiveCopy está dañada, las páginas de Live Copy muestran vínculos de copia de idioma en lugar de vínculos de LiveCopy (NPR-30980).
* Para un nuevo modelo, si el número de registros es superior a 40, solo se muestran los primeros 40 registros. El modelo muestra líneas en blanco para el resto de los registros (NPR-31182).
* El complemento Editor de texto enriquecido (RTE) del componente de texto muestra caracteres distorsionados para texto en japonés y coreano (NPR-31331).
* El editor de texto enriquecido (RTE) no permite insertar una tabla incrustada como elemento de lista (NPR-30879).
* El Editor de texto enriquecido (RTE) de scaffolding de fuera del cuadro se aplica en línea de tamaño de fuente a los elementos de forma inesperada (NPR-31284).
* Cuando un usuario se centra en los campos del carril izquierdo y utiliza combinaciones de teclas para pegar contenido, pega el contenido del portapapeles del editor de páginas en lugar del contenido copiado de los campos del carril izquierdo (NPR-31172).
* Cuando un usuario agrega un campo Carga de archivo a un campo múltiple, la ruta de la imagen se almacena en el nodo del componente en lugar del nodo de varios campos (NPR-30882).
* La API `ResponsiveGridExporter` no devuelve la interfaz `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter`. El paquete `com.day.cq.wcm.foundation.model.impl` se declara como paquete privado (NPR-31398).
* Cuando se abre una página que contiene algunos fragmentos de experiencia en modo que no es de editor (ya sea en Autor sin el prefijo `editor.html` y `wcmmode=disabled` o en Editor), la solicitud termina en el código de error de estado HTTP 500 (NPR-30743).

### WCM: editor de páginas {#wcm-page-editor-6520}

**Mejoras del producto**

* Mejorarfiltros de tipo documento con más tipos MIME para admitir opciones de varios valores. Revisión para CQ-4270694

### Administración de fragmentos de contenido {#content-fragment-management-6520}

* La consulta que isa la IU de los modelos de fragmento de contenido es muy lenta y, finalmente, acaba en error. Revisión para CQ-4270807

### IU: bases {#ui-foundation}

* Desencadenador de accesos directos que impide que el usuario utilice &quot;m,&quot; &quot;p,&quot; y &quot;e&quot; en las interfaces de usuario específicas. NPR-30355: revisión para GRANITE-26346
* Al cerrar [!DNL Experience Manager Assets] la interfaz de usuario de búsqueda no se restablece el carril izquierdo a la selección de contenido, lo que impide que el usuario abra el carril del filtro por segunda vez posteriormente. NPR-30509: revisión para CQ-4274716
* Entorno de varios inquilinos: [!DNL Experience Manager Assets] La navegación superior de la interfaz de usuario no está disponible y se produce un error de JavaScript. NPR-30104: revisión para GRANITE-26344

### Traducción {#translation-6520}

* Problema de traducción: solo unos pocos componentes se traducen mediante traducción automática. NPR-30079: revisión para CQ-4273764

### Plataforma  {#platform-6520}

* [!DNL Experience Manager]El remitente de correo predeterminado de no puede enviar correo a un servidor SMTP remoto a través de TLS v1.2. NPR-30476: revisión para GRANITE-26605

### Proyectos {#projects-6520}

* Los valores de dam:folderThumbnailPaths no se actualizan y muestran miniaturas antiguas incluso después de eliminar los recursos de la carpeta. NPR-30424: revisión para CQ-4273667
* Al completar la opción Mover, el título y el nombre del activo no cambian. NPR-30647: revisión para CQ-4276265

### Comunidades  {#communities-6520}

* El diagnóstico de sincronización de usuarios está completamente dañado y no funciona. NPR-30004, NPR-29943: revisión para CQ-4270287, CQ-4271348

### Sling {#sling}

* La instancia actualizada de 6.3.3.2 a 6.5 devuelve configuraciones OSGi duplicadas. NPR-30130: revisión para CQ-4274016

### Integración

* El contenido personalizado no se muestra correctamente en la instancia de publicación hasta que no se reinicia la instancia. NPR-30377: revisión para CQ-4273706
* Al configurar el inicio en un sitio web, la dirección de la biblioteca tiene una barra diagonal (/) precargada, lo que provoca que el usuario tenga que intervenir de forma manual cada vez. NPR-30694: revisión para CQ-4275501

### Forms {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack no incluye correcciones para  [!DNL Experience Manager Forms]. Se entregan mediante un paquete de complemento [!DNL Forms] independiente. Además, se ha publicado un instalador acumulativo que incluye correcciones para [!DNL Experience Manager Forms] en JEE. Para obtener más información, consulte [Instalación de Experience Manager Forms Add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) y [Instalación de Experience Manager Forms en JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

Los aspectos destacados de los formularios [!DNL Experience Manager] 6.5.2.0 son:

* Se añadió la configuración &#39;Auto&#39; en `RenderAtClient` en la API `PDFFormRenderOptions` para [!DNL Experience Manager] OSGi de Forms.

#### Paquete de complemento de Forms

**Integración del back-end**

* No se puede configurar el modelo de datos de formulario con una URL de carga equilibrada alojada en AWS. NPR-30123: revisión para CQ-4273359
* Al crear el modelo de datos de formulario (FDM) con el lenguaje de definición de servicio Web (WSDL), se devuelve el mensaje de error `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type`: NPR-30477: Revisión para CQ-4272921

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

#### Instalador JEE de Forms

**Forms: seguridad de documentos**

* El proceso de aplicación de una firma con marca de hora devuelve el error: ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException: error de invocación. NPR-30820: revisión para CQ-4275852

**Forms: servicios de documentos**

* Si &quot;SubmitURL&quot; contiene un símbolo &amp;, se muestran errores de análisis en el registro cuando se realiza una solicitud POST para procesar el servlet de renderpdf. NPR-30865: revisión para CQ-4278232

**Forms: base JEE**

* El servicio HTMLtoPDF no muestra maxReuseCount en la consola JMX. NPR-30134, NPR-30304: revisión para CQ-4273763
* Añadir o editar una conexión de servicio Web invocando servicios Web desde [!DNL Experience Manager Forms] Workbench genera un error: ClassNotFoundException org.apache.axis.message.SOAPBodyElement. NPR-30105: revisión para CQ-4273217

### Paquetes de funciones incluidos

>[!NOTE]
>
>Para los clientes [!DNL Experience Manager Forms], es esencial instalar el paquete de complementos [!DNL Experience Manager Forms] después de instalar cualquier Service Pack, paquete de correcciones acumulativas o paquete de funciones [!DNL Experience Manager].

#### Sitios {#sites-feature-packs-included}

* Se agregó una propiedad de configuración para permitir la exportación de fragmentos de experiencia directamente a espacios de trabajo que haya definido el usuario en [!DNL Adobe Target]. NPR-29189: revisión para CQ-4249782

#### Forms: servicios de documentos {#forms-document-services-1}

* Se añadió la configuración &#39;Auto&#39; en `RenderAtClient` en la API `PDFFormRenderOptions` para OSGi [!DNL Experience Manager Forms]. NPR-30759: revisión para CQ-4278193

## Adobe Experience Manager 6.5.1.0 {#experience-manager-6510}

[!DNL Adobe Experience Manager] 6.5.1.0 es una versión importante que incluye correcciones y mejoras clave de rendimiento, estabilidad, seguridad y del cliente publicadas desde la disponibilidad general de  [!DNL Adobe Experience Manager] 6.5 en  *abril de 2019.*[!DNL Experience Manager] Se puede instalar en 6.5.

Algunos aspectos destacados de esta versión del Service Pack son:

* Se habilitó la inclusión de dynamic-UI-state en el seguimiento de eventos como atributos personalizados. 
* Se ha incluido compatibilidad con el envío de recursos de vídeo de 360 grados en el modo [!DNL Dynamic Media]-Scene7.
* Se habilitó la función *Ajuste de palabras en japonés* mediante el complemento de estilos del Editor de texto enriquecido. Para obtener más información, consulte [Configuración del ajuste de palabras en japonés](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### Recursos

* Se ha actualizado la interfaz DAM DMGgateway para que sea compatible con varias partes de S3. NPR-29740: revisión para CQ-4226303
* La previsualización de representaciones genera un error `Only empty tenantId is currently supported` después de actualizar a [!DNL Experience Manager] 6.5. NPR-29986: Revisión para CQ-4272353
* El cuadro de diálogo Eliminar no está visible para permitir la eliminación de trabajos. NPR-29720: revisión para CQ-4271074
* Después de agregar el título del recurso en la página de propiedades, cuando un usuario intenta cerrar la página, [!DNL Experience Manager] vuelve a abrir la página de propiedades. NPR-29627: revisión para CQ-4264929
* El elemento VersioningTimelineEventProvider debe proporcionar la versión raíz junto con el nodo de tipo nt: versión. Revisión para GRANITE-26063
* Se ha implementado la capacidad de cargar y reproducir vídeos esféricos de 360 en modo [!DNL Experience Manager] DM-Scene7. Revisión para CQ-4265131
* Live Copy recupera un estado incorrecto si se edita el origen. Revisión para CQ-4265451
* Se habilitó la compatibilidad con Multi-Site Manager para [!DNL Experience Manager Assets]. Revisión para CQ-4271453, CQ-4268621, CQ-4257491
* [!DNL Experience Manager] debe mostrar una entrada adicional para la versión actual del recurso en el historial de línea de tiempo, mostrando el último comentario de protección de  [!DNL Adobe Asset Link]. Revisión para CQ-4262864
* La línea de tiempo del fragmento de contenido muestra un mensaje de error cuando faltan propiedades. Revisión para CQ-4272560
* Problema con el reproductor de vídeo de Scene7 cuando se expande a pantalla completa. Revisión para CQ-4266700
* ZoomVerticalViewer: los botones de desplazamiento no se deben mostrar si se utiliza un único recurso de imagen. Revisión para CQ-4264795
* La eliminación de un nodo secundario en Live Copy debe desasociar el elemento liveRelationship. Revisión para CQ-4270395
* El esquema de metadatos solo contiene elementos de la configuración global y no contiene los del inquilino activo. El valor de la dirección URL de formPath vuelve al valor predeterminado incluso cuando se cambia. NPR-29945: revisión para CQ-4262898
* La publicación de ajustes preestablecidos de imagen en [!DNL Brand Portal] falla con el código de error 500. NPR-29510: revisión para CQ-4268659

### Sitios

* Las propiedades vacías y varias propiedades no se propagan desde el modelo durante el lanzamiento. El restablecimiento de Live Copy con un plano técnico no funciona en los componentes. NPR-29253: revisión para CQ-4264928, CQ-4264926, CQ-4267722
* CoralUI, cuando se utiliza con `Multifield`, almacena el `fileReferenceParameter` en el nivel del componente en lugar de en el nivel de varios campos. NPR-29537: revisión para CQ-4266129
* Mejora del componente de texto [!DNL Experience Manager] y del Editor de texto al japonés. NPR-29785: revisión para CQ-4265090
* La página restaurada con Deformación de tiempo debe hacer referencia a la imagen correcta en el momento de controlar las versiones. NPR-29431: revisión para CQ-4262638
* Problema con la herencia de los nodos del sistema de estilo de principal a secundario. NPR-29516: revisión para CQ-4270330
* Un mensaje de error al configurar la publicación social en [!DNL Facebook] autenticación. NPR-29211: revisión para CQ-4266630
* La miniatura representada en el fragmento de contenido muestra una representación interna del calendario para los campos de fecha y hora. NPR-29531: revisión para CQ-4269362
* Al abrir la ficha Permisos en la implementación de Coral2 no se muestran los botones. Revisión para CQ-4269419

### Comercio

* ConstraintViolationException, cuando se ejecuta la migración de contenido diferido para el comercio electrónico. NPR-29247: revisión para CQ-4264383

### Administración de fragmentos de contenido

* Error de análisis al abrir un fragmento de contenido que tiene caracteres dólar `($)` y llave abierta `({)`. Revisión para CQ-4270266

### Fragmentos de experiencias

* Exportar [!DNL Experience Manager] fragmentos de experiencias a [!DNL Adobe Target]. Revisión para CQ-4265469
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

* La actualización a [!DNL Experience Manager] 6.4.3 hace que Multi-Site Manager tarde mucho en implementarse. Revisión para CQ-4271410

### Integración

* Error de conexión en las credenciales de BrightEdge. NPR-29168: revisión para CQ-4265872

* Se muestra un mensaje de excepción al intentar editar y guardar la configuración de inicio [!DNL Experience Manager]. NPR-29176: revisión para CQ-4265782/CQ-4266153

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

* Publicar [!DNL Experience Manager Assets] desde la carpeta [!DNL Experience Manager] Autor /content/dam/mac a [!DNL Brand Portal] no funciona. NPR-29819: revisión para CQ-4271118

### Plataforma

* HtmlLibraryManager elimina todo el contenido de crx-quickstart cuando se invalida la caché. NPR-29863: revisión para GRANITE-26197

### Felix

* Los detalles de uso de memoria no se muestran en la consola del sistema al utilizar Java11\. NPR-29669

### Forms

Los aspectos destacados de [!DNL Experience Manager Forms] 6.5.1.0 son:

* Solo OSGi: Se añadió un nuevo atributo `PAGECOUNT` en Output y Forms Service.

* Sólo OSGI: Se ha habilitado la compatibilidad para crear archivos PDF estáticos mediante el servicio Forms.
* Permisos activados en XMLForm.exe para usuarios raíz y administradores.
* Se habilitó la compatibilidad con ADFS v3.0 para la integración local de Dynamics.

#### Paquete de complemento de Forms

**Integración de back-end**

* Error al recuperar el lenguaje de definición del servicio web protegido (WSDL). NPR-29944: revisión para CQ-4270777
* Cuando [!DNL Experience Manager Forms] se instala en IBM WebSphere, se produce un error al crear un modelo de datos de formulario basado en SOAP. Revisión para CQ-4251134
* Se habilitó la compatibilidad con los servicios de federación de Active Directory (ADFS) v3.0 para la integración local de Microsoft Dynamics. Revisión para CQ-4270586
* Cuando se cambia el título de un origen de datos, el modelo de datos de formulario no muestra el título actualizado. Revisión para CQ-4265599
* Si el nombre de una entidad o atributo contiene guiones o espacio, las expresiones no pueden evaluar dichas entidades y atributos. Revisión para CQ-4225129

* Se observa una salida incorrecta cuando hay dos puntos en la salida de cadena primitiva. Revisión para CQ-4260825

* Incluso cuando no se espera contenido del resultado de la API de REST, la operación de invocación del modelo de datos de formulario genera un error. Revisión para CQ-4268828

**Formularios adaptables**

* No se puede agregar una nueva instancia en el fragmento del formulario adaptable durante la carga diferida. NPR-29818: revisión para CQ-4269875
* El componente de verificación no registra ni muestra ningún error en las plantillas del documento de registro. Revisión para CQ-4272999
* Se agregó la compatibilidad para deshabilitar el editor de diseño para formularios adaptables. Revisión para CQ-4270810
* Se ha restaurado el paso de verificación para Forms adaptable en [!DNL Experience Manager] 6.5. Revisión para CQ-4269583

* Error de validación del campo de formulario adaptable [!DNL Adobe Sign]. Revisión para CQ-4269463
* Cuando una instancia [!DNL Experience Manager Forms] tiene más de 20 fragmentos de formulario adaptables y nombre de todos los inicios de fragmentos de formulario con la misma cadena, la búsqueda devuelve sólo 20 fragmentos creados recientemente o no. Revisión para CQ-4264414, CQ-4264914

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
* Cuando se adjunta una imagen de más de 2 MB como datos adjuntos de nivel de campo a un formulario en la versión de Android de la aplicación [!DNL Experience Manager Forms], la aplicación se bloquea. Revisión para CQ-4265578

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

* [!DNL Experience Manager Forms] 6.5 Crear interfaz de usuario de correspondencia (IU de CCR) no puede abrir la correspondencia creada con  [!DNL Experience Manager Forms] 6.3. Revisión para CQ-4266392
* La función Sumar en XDP no funciona si el tipo de datos de DDE es de tipo número. Revisión para CQ-4227403
* Se va a actualizar la lógica de invalidación de letras en memoria de la caché, porque cuando se publica un recurso no se actualiza la hora de la última modificación. Revisión para CQ-4250465
* No se puede publicar un fragmento de documento, DD y letras. Revisión para CQ-4272893

#### Instalador JEE de Forms

**Generador de PDF**

* La conversión de archivos CAD a PDF ha producido un error con JDK de 64 bits. NPR-29924, NPR-29925: revisión para CQ-4272113
* Se reemplazó el nombre de PhantomJS a WebToPDF para la conversión de HTMLtoPDF. NPR-29933: revisión para CQ-4234545
* Se genera un error al convertir el archivo zip a PDF. Revisión para CQ-4268628

**Forms: Designer**

* Cuando se realiza una comprobación de accesibilidad completa en el PDF estático creado con [!DNL Experience Manager Forms Designer], la comprobación del idioma principal falla debido a la falta del atributo de idioma. Revisión para CQ-4272923, CQ-4271002

**Forms: seguridad de documentos**

* La firma digital con módulo de seguridad de hardware (HSM) no funciona en OSGi Linux en Java 11 y Java 8\. NPR-29838: revisión para CQ-4270441
* La firma digital con el módulo de seguridad de hardware (HSM) no funciona en JEE Linux ni en ninguno de los servidores de aplicaciones compatibles, como JBoss y Websphere. NPR-29839: revisión para CQ-4266721
* La comprobación de firmas en un PDF mediante firma electrónica avanzada en formato PDF (PAdES) genera la excepción InvalidOperationException. NPR-29842: revisión para CQ-4244837
* Se agregó la compatibilidad de Document Security Extension con Office 2019\. Revisión para CQ-4254369, CQ-4259764

**Forms: servicios de documentos**

* PDF no puede convertir a PDF/A-1b con campo Formulario no tiene sentencia de apariencia. NPR-29940: revisión para CQ-4269618

* OSGi: No se puede determinar el número de páginas generadas durante el procesamiento. NPR-28922: revisión para CQ-4270870
* Se ha habilitado la compatibilidad con archivos PDF estáticos mediante el servicio de Forms en [!DNL Experience Manager Forms OSGi]. NPR-28572: revisión para CQ-4270869
* No se pueden cambiar los permisos en el archivo XMLForm.exe. NPR-29828, NPR-29237: revisión para el T-4267080
* El PDF estático creado por el módulo de salida del servidor [!DNL Experience Manager Forms] no rellena el atributo/etiqueta del idioma con el idioma del documento creado. NPR-27332: revisión para CQ-4271002

**Forms: base JEE**

* Pdfg_srt no está disponible en los artefactos finales y provoca errores en el instalador. NPR-29854: revisión para CQ-4270137
* LCBackupMode.sh no funciona. NPR-29840: revisión para CQ-4269424
* La referencia del puerto UDP debe eliminarse de la interfaz de usuario (IU) para WebSphere. Revisión para CQ-4264782

### Paquetes de funciones incluidos

#### Recursos: incluidos

* Se habilitó la compatibilidad con Multi-Site Manager para [!DNL Experience Manager Assets]. Para obtener más información, consulte [Reutilización de recursos con MSM para recursos Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-65/assets/using/reuse-assets-using-msm.html). NPR-29199: revisión para CQ-4259922

#### Sitios: incluidos

* Exportar [!DNL Experience Manager] fragmentos de experiencias a [!DNL Adobe Target]. Para obtener más información, consulte [Proveedor de reescritores de vínculos de fragmentos de experiencia - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). Revisión para CQ-4265469

#### Forms: servicios de documentos - Incluido

* Solo OSGi: Se añadió un nuevo atributo PAGECOUNT en Output y Forms Service. NPR-28922: revisión para CQ-4270870
* Solo OSGi: Se ha habilitado la compatibilidad para crear archivos PDF estáticos mediante el servicio Forms. NPR-28572: revisión para CQ-4270869
* Permisos activados en XMLForm.exe para usuarios raíz y administradores. NPR-29237: revisión para CQ-4267080

### Paquetes de contenido y paquetes OSGi

Los siguientes documentos de texto lista los paquetes OSGi y los paquetes de contenido incluidos en [!DNL Experience Manager] 6.5.1.0

Lista de los paquetes OSGi incluidos en [!DNL Experience Manager] 6.5.1.0

[Obtener archivo](assets/6_5-bundle-list.txt)

Lista de paquetes de contenido incluidos en [!DNL Experience Manager] 6.5.1.0

[Obtener archivo](assets/6_5-content-package-list.txt)
