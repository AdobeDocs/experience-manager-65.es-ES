---
title: '[!DNL Adobe Experience Manager] Notas de la versión anterior de Service Pack 6.5'
description: Notas de la versión de los Service Packs [!DNL Adobe Experience Manager] 6.5.
contentOwner: AK
translation-type: tm+mt
source-git-commit: 131e564e4ed50c4f08412ba39c62f15b9c362b8c
workflow-type: tm+mt
source-wordcount: '17898'
ht-degree: 17%

---


# Revisiones y paquetes de funciones incluidos en los Service Packs anteriores {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## [!DNL Adobe Experience Manager] 6.5.7.0  {#experience-manager-6570}

[!DNL Adobe Experience Manager] 6.5.7.0 es una actualización importante que incluye nuevas funciones, mejoras clave solicitadas por los clientes y mejoras de rendimiento, estabilidad y seguridad, publicadas tras la publicación de la versión 6.5 en abril de 2019. El Service Pack se instala en [!DNL Adobe Experience Manager] 6.5.

Las funciones y mejoras clave introducidas en [!DNL Adobe Experience Manager] 6.5.7.0 incluyen:

* Realizar los movimientos de página y los despliegues de MSM como operaciones asincrónicas para reducir su impacto en el rendimiento del tiempo de ejecución.

* Los usuarios pueden ordenar los recursos digitales en las vistas de tarjeta y columna.

* [!DNL Assets] y  [!DNL Dynamic Media] proporcionan varias mejoras de accesibilidad. Las mejoras están relacionadas con la navegación mediante el teclado, el uso de lectores de pantalla y la posibilidad de que los usuarios utilicen tecnologías de asistencia similares (AT). Consulte [[!DNL Assets] mejoras](#assets-6570) y [[!DNL Dynamic Media] mejoras](#dynamic-media-6570).

* [Modelo de datos de formulario ](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration) Configuración del cliente HTTP para optimizar el rendimiento.

* [Disponibilidad de la opción Restablecer para cada ](../../help/forms/using/resize-using-layout-mode.md#resize-components) componente en el modo Diseño

* [!DNL Experience Manager] 6.5 Service Pack 7 Forms mejora el rendimiento para:

   * Validación de los valores de campo en el servidor al enviar un formulario adaptable.

   * Conversión de un formulario PDF en un formulario adaptable mediante [!DNL Automated Forms Conversion service].

* Soporte para [!DNL Microsoft SQL Server] 2019 en [!DNL Experience Manager Forms].

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.22.5.

Para obtener una lista completa de las funciones y mejoras introducidas en [!DNL Experience Manager] 6.5.7.0, consulte [Novedades de [!DNL Adobe Experience Manager] 6.5 Service Pack 7](new-features-latest-service-pack.md).

La siguiente es la lista de correcciones que se proporcionan en la versión [!DNL Experience Manager] 6.5.7.0.

### [!DNL Sites] {#sites-6570}

* Cuando se abre la opción [!UICONTROL Timewrap] para una página, se mantiene abierta la opción del carril lateral de la línea de tiempo y se desplaza a la consola [!UICONTROL Sites], se produce el error `Failed to Load` (NPR-34951).

* La opción [!UICONTROL Timewrap] no muestra imágenes para la fecha y el intervalo de tiempo seleccionados (NPR-34951).

* Cuando un filtro llama a `getHeader()` desde una página que contiene un fragmento de contenido, se produce el error `java.lang.AbstractMethodError` (NPR-34942).

* Cuando la ruta de una página contiene varias subcadenas de contenido, las vistas previas no se pueden procesar y la función de comparación de versiones también falla (NPR-34740).

* Cuando se define un valor numérico para la propiedad de etiqueta de tipo `String` de un componente, se puede eliminar el componente y deshacer la operación de eliminación. Sin embargo, después de deshacer la eliminación, la propiedad de etiqueta cambia de `String` a `Long` (NPR-34739).

* La siguiente excepción se produce al añadir un fragmento de experiencia basado en una plantilla con un diseño bloqueado a una página (NPR-34632):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* Al mover una carpeta, se producen problemas transversales y se produce el siguiente error (NPR-34554):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* Cuando se crean, publican y mueven nuevos recursos a una nueva ubicación, el flujo de trabajo `Request to complete move operation` se crea y se anula. Al cargar un nuevo recurso y ejecutar una operación `move` , se crea el flujo de trabajo `Request to complete move operation` en estado pendiente (NPR-34543).

* Cuando se exporta un fragmento de experiencia de [!DNL Experience Manager] 6.5.2 environment a [!DNL Target] Standard, la llamada de API falla porque la propiedad del espacio de trabajo no está disponible para [!DNL Target] Standard (NPR-34557).

* Los usuarios no pueden publicar páginas mediante la opción [!UICONTROL administrar publicación] porque la opción [!UICONTROL Publicar] desaparece (NPR-34542).

* Cuando agrega algunos estilos al texto, se agrega una etiqueta `<div>` al texto y el estilo ya no se puede aplicar al texto (NPR-34531).

* Cuando selecciona un elemento en un menú emergente y actualiza los archivos necesarios, no permite guardar valores de cuadro de diálogo, ya que el otro menú tiene un campo obligatorio vacío (NPR-34529).

* Cuando crea una página a partir de una plantilla personalizada y la mueve dentro de la jerarquía del modelo, los componentes eliminados anteriormente desde la página empiezan a aparecer en la página dentro de la jerarquía de la copia activa (NPR-34527).

* Una vez que se aplica un estilo de artículo a un contenido, no se puede eliminar (NPR-34486).

* Todas las Live Copies y copias de un fragmento de experiencia apuntan al mismo ID de oferta [!DNL Adobe Target] (NPR-34469).

* Los elementos de la lista con viñetas se muestran además de la lista numerada (NPR-34455).

* La opción de comparación con la fuente no muestra la diferencia entre la página de origen y la versión editada de una página (NPR-34285).

* Al eliminar una página, los detalles de versiones no se pueden configurar (NPR-34159).

* Cuando un usuario selecciona la opción de diálogo [!UICONTROL Abrir selección], el foco del teclado se mueve al control oculto presente en la página (CQ-4307779, CQ-4293601).

* Al mover una carpeta publicada en el Autor, las rutas de carpeta no se actualizan en consecuencia en la instancia de publicación (CQ-4305144).

* Cuando un usuario selecciona la tecla `Enter` en la opción [!UICONTROL Seleccionar todo], el foco del teclado no se mueve a la opción [!UICONTROL Crear control] (CQ-4293599).

* Al seleccionar la clave `Esc`, el enfoque no se restaura al control principal (CQ-4293593, CQ-4293590).

* Se ha mejorado el cumplimiento de WCAG para la interfaz de usuario y los componentes principales de [!DNL Sites] (CQ-4293448).

*  Las   funciones de ampliación del zoom están deshabilitadas para la  [!DNL Sites Editor] página (CQ-4282353).

* Después de utilizar la opción Rotar a la derecha, el lector de pantalla deja de narrar el estado de giro o giro actual (CQ-4282128).

* Los botones de diálogo Listo y Cancelar configuración tienen más de un tabulador (CQ-4274601).

* No se permite mover páginas con un nombre similar en el mismo nivel (NPR-35041).

* Después de seleccionar la opción Borrar (x), el foco del teclado no se mueve al campo [!UICONTROL Filtro] (CQ-4293581).

* Al actualizar a [!DNL Experience Manager] 6.5.6.0, el comportamiento del sistema de párrafos heredado cambia y no funciona correctamente (NPR-35117).

* Los usuarios del teclado no pueden cambiar el enfoque de la pestaña en un orden adecuado después de seleccionar la sección [!UICONTROL Acción] en una página [!DNL AEM Sites] (CQ-4307786).

* Después de seleccionar una opción en la lista de menús de destino de vínculo de la barra de herramientas RTE al editar un fragmento de contenido, el cuadro de diálogo de creación de fragmentos de contenido comienza a parpadear (CQ-4305532).

* Los usuarios del teclado no pueden seleccionar las opciones de la lista desplegable [!UICONTROL Agregar componente] mediante la tecla de flecha abajo (CQ-4295097).

* El enfoque de la pestaña no cambia en el orden adecuado al seleccionar una fecha del menú Calendario en la pestaña [!UICONTROL Assets] de una página [!DNL Sites] (CQ-4293600).

* El enfoque de la pestaña no cambia a las opciones siguientes o anteriores para los usuarios del teclado después de eliminar las opciones Vínculo o Texto disponibles al editar una página Sitios (CQ-4293597).

* Los usuarios del teclado no pueden volver a cambiar el foco de la pestaña a Más opciones en la sección [!UICONTROL Acciones] después de ver las opciones disponibles y de pulsar la tecla `Esc` (CQ-4293592).

* Cuando se activa la opción [!UICONTROL Rotar] para una imagen en el modo [!UICONTROL Editar], el enfoque de la pestaña, en lugar de permanecer en Rotar, cambia a la opción [!UICONTROL Rehacer] para los usuarios del teclado (CQ-4293587).

* En el cuadro de diálogo [!UICONTROL Abrir selección] disponible en la pestaña [!UICONTROL Vínculo y acciones], el enfoque de la pestaña cambia a elementos ocultos en la página después de la opción [!UICONTROL Cancelar] (CQ-4293579).

* Cuando los usuarios del teclado editan una imagen, navegan a la opción [!UICONTROL Finish] y pulsan la tecla Intro, los lectores de pantalla no anuncian la finalización (CQ-4282351).

* Las opciones Subir y Bajar disponibles en el cuadro de diálogo [!UICONTROL Vínculo y Acciones] no están disponibles para el lector de pantalla y los usuarios del teclado (CQ-4281120).

* Los usuarios del teclado no pueden restaurar el enfoque de la pestaña después de navegar a la opción Cerrar (X) en la página [!UICONTROL Propiedades] (CQ-4293581, NPR-34653).

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] 6.5.7.0  [!DNL Assets] corrige los problemas siguientes y proporciona las siguientes mejoras.

* Las siguientes mejoras se han realizado para la accesibilidad en [!DNL Experience Manager Assets] en esta versión. Para obtener más información, consulte [funciones de accesibilidad en [!DNL Assets]](/help/assets/accessibility.md).

   * Al navegar por la línea de tiempo mediante un teclado, la tecla `Esc` puede contraer la opción [!UICONTROL Mostrar todo] sin perder el enfoque (CQ-4293598).
   * Al navegar mediante la tecla de tabulación del teclado, después de eliminar la última etiqueta de las etiquetas agregadas, el campo de etiqueta mantiene el enfoque (NPR-35109).
   * [!DNL Experience Manager] los componentes ahora contienen información apropiada sobre el nombre, la función y el valor que deben utilizar los lectores de pantalla (NPR-34255).
   * Después de eliminar el cuadro combinado Tipo/Tamaño, el cuadro combinado Vínculo, el cuadro combinado Idioma o el cuadro de edición de texto, el foco del teclado vuelve a los elementos de la interfaz de usuario siguientes o anteriores o a un elemento de la interfaz de usuario más relevante (CQ-4293585).
   * Al pasar el puntero sobre las opciones, aparecen sugerencias como Seleccionar y Descargar. Es posible que los usuarios que utilizan un ampliador de pantalla no vean las miniaturas del archivo debido a estas sugerencias. Ahora, es posible conservar el enfoque, después de eliminar la opción utilizando la clave `Escape`. (CQ-4293554).
   * Al seleccionar una celda de cuadrícula de la cuadrícula presente en la página, el foco se desplaza a la barra de acciones que aparece en la pantalla (CQ-4282127).
   * Los usuarios visuales pueden diferenciar entre texto normal y un vínculo, ya que las pistas visuales (subrayado e icono de cheurón) se muestran para los vínculos a todas las soluciones en la [!DNL Experience Manager] página principal (CQ-4282072).

* La siguiente mejora de la experiencia de usuario se realiza en [!DNL Assets]:

   * Habilite la ordenación de recursos en la vista de tarjeta y la vista de columna (NPR-35097).

* Después de la actualización a 6.5, si se genera un archivo JSON mediante la API HTTP de Assets, hay problemas con la codificación utilizada en el archivo (NPR-35129).

* Los usuarios de un grupo al que no se haya concedido el permiso para crear colecciones (la opción Crear colección no está disponible) siguen pudiendo crear colecciones accediendo directamente a la URL `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections` (NPR-35115).

* Cuando se ordenan por nombre, los recursos buscados se ordenan de manera que distingan entre mayúsculas y minúsculas. Esto crea dos listas separadas clasificadas basadas en mayúsculas que aparecen ordenadas en los resultados de búsqueda (NPR-35068).

* Cuando se abre un fragmento de contenido en el editor, los mensajes de advertencia (`Invalid value specified for a metadata property`) se registran en los registros de errores (NPR-35012).

* Los usuarios sin privilegios de administrador pueden editar recursos caducados mediante la aplicación de escritorio [Experience Manager]. (NPR-34993).

* Cuando se arrastra el mismo recurso en la interfaz de usuario de Assets y se crea una nueva versión, los cambios en los metadatos no son persistentes (NPR-34940).

* Al editar colecciones, un usuario puede eliminar el título de la colección y guardar correctamente los cambios (NPR-34889).

* Al cargar una imagen duplicada, se presenta una opción de eliminación. Al seleccionar eliminar , las imágenes se pueden cargar. El flujo de trabajo de recursos de actualización de DAM también se activa (NPR-34744).

* Al utilizar [!DNL Adobe Asset Link] con [!DNL Adobe InDesign], los resultados de búsqueda no contienen carpetas y colecciones, sino que solo contienen recursos (NPR-34699, CQ-4303666).

* Al pasar el puntero sobre la vista de tarjeta, la pantalla se desplaza como resultado del enfoque (automático) en las acciones rápidas disponibles en la tarjeta (NPR-34514).

* Al editar las propiedades de varios recursos de forma masiva, al seleccionar la opción [!UICONTROL Guardar] se cierra la vista del editor de forma masiva y se redirige a la página principal [!DNL Assets]. Este comportamiento es el mismo que el de la opción [!UICONTROL Guardar y cerrar] y no se espera (NPR-34546).

* La colección inteligente no presenta la configuración correcta de la interfaz de usuario después de guardar. La consulta se guarda correctamente, pero la interfaz siempre muestra el último predicado de opciones añadido (NPR-34539).

* Al agregar recursos a [!DNL Experience Manager], los metadatos sin área de nombres no se importan (NPR-34530).

* Al arrastrar un recurso a una carpeta para moverlo, la interfaz de usuario también muestra la opción [!UICONTROL Soltar en Lightbox] y [!UICONTROL Soltar en la colección]. Incluso si se cancela la operación de traslado, la interfaz de usuario sigue mostrando las dos últimas opciones (NPR-34526).

* El símbolo `%>` se muestra en la página de colecciones (NPR-34499).

* En la vista de columna, [!DNL Assets] muestra nombres de carpeta y recurso duplicados al desplazarse hacia arriba y hacia abajo antes de que se muestren todos los recursos (NPR-34464).

* Si crea una carpeta privada inmediatamente después de crear una carpeta pública, la carpeta pública utiliza la configuración de la carpeta privada (NPR-34415).

* En la vista de tarjeta, las tarjetas no aparecen en orden alfabético y no se pueden ordenar alfabéticamente (NPR-34234).

* Al volver a abrir reglas en cascada, las opciones no se mantienen en la interfaz de usuario (CQ-4301452).

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* Las siguientes mejoras se realizan para la accesibilidad en [!DNL Dynamic Media] (CQ-4290306). Para obtener más información, consulte [funciones de accesibilidad en [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

   * Los lectores de pantalla (JAWS, Narrador) narran el nombre, la función y el estado de los elementos de menú en la opción de menú Tamaño incrustado (CQ-4290927).
   * Los usuarios pueden navegar por el cuadro de diálogo Vínculo de correo electrónico utilizando la clave `Tab` (CQ-4290926).
   * El flujo de trabajo para crear perfiles de codificación de vídeo es más sencillo de usar, dada la mejora del lector de pantalla (CQ-4290623, CQ-4290622).
   * Al navegar con la clave `Tab`, el enfoque se desplaza a los elementos de interfaz de usuario adecuados en el flujo de trabajo para crear un vídeo interactivo (CQ-4290621, CQ-4290620, CQ-4290619).
   * La página Publicar , la página Editar recurso , la página Editar recortes inteligentes y la página Editor de conjuntos de imágenes se han mejorado para cumplir con los estándares web. Los usuarios de tecnología de asistencia (AT) ahora pueden navegar fácilmente por estas páginas y realizar acciones como recortar imágenes (CQ-4290617, CQ-4290616, CQ-4290613, CQ-4290612, CQ-429 0610, CQ-4290614).
   * Se han mejorado los visualizadores para permitir que los usuarios naveguen mediante un teclado (CQ-4290615).
   * Los usuarios del teclado y del lector de pantalla pueden utilizar la funcionalidad de recorte (CQ-4290609).
   * Los usuarios del teclado pueden administrar mejor las zonas interactivas (CQ-4290604, CQ-4290603).

* Los conjuntos de imágenes remotas no se pueden editar en [!DNL Experience Manager] si el nombre de la empresa y el de la carpeta son los mismos (NPR-31340).

* El orden z-index es incorrecto cuando intenta previsualizar la salida después de agregar una zona interactiva a una imagen [!DNL Dynamic Media] o después de editar un [!DNL Dynamic Media] vídeo o un [!DNL Experience Fragment] con una imagen (CQ-4307267).

* [!DNL Dynamic Media] la sincronización falla cuando se vuelven a procesar los conjuntos de medios mixtos (CQ-4307184).

* Si un recurso se mueve a una carpeta en la que se configura la sincronización automática para [!DNL Dynamic Media], el recurso no se sincroniza (CQ-4307122).

* [!DNL Dynamic Media] el vídeo no se reproduce en dispositivos iOS con los controles de vídeo HTML5 nativos (CQ-4306977, CQ-4306727).

* No se pueden descargar imágenes en las que se aplica SmartCrop (CQ-4304558).

* No se pueden publicar carpetas en Dynamic Media de forma selectiva (CQ-4304526).

* Al cancelar la publicación de un archivo de vídeo desde [!DNL Experience Manager] no se cancela la publicación del conjunto de vídeos adaptables desde una implementación configurada de Scene7 (CQ-4304405).

* Añadir un recurso de imagen panorámica en un componente multimedia panorámico y actualizar la página provoca el error `Uncaught ReferenceError: $ is not defined` (CQ-4302810).

* En el [!UICONTROL Editor de ajustes preestablecidos de visualizador], al editar el ajuste preestablecido [!UICONTROL PanoramicImage/PanoramicImage_VR], en el componente `PanoramicView`, la etiqueta del modificador `PANORAMICVIEW_AUTOROTATE` no está disponible (CQ-4302443).

* Los subtítulos de vídeo no se muestran si el vídeo no es el primero de un MixedMediaSet (CQ-4298161).

* El visor de catálogos electrónicos HTML5 en dispositivos móviles iPhone no puede girar las páginas ni voltear las páginas (CQ-4296611).

* Cuando se desplazan muestras en un dispositivo móvil, las muestras se desplazan hacia la derecha y hacia fuera del área visible durante unos segundos antes de volver a la vista (CQ-4296439).

* Cuando se crea un registro maestro de ajustes preestablecidos de visualizador, el CSS y la ilustración no se publican y solo se publica el ajuste preestablecido de visualizador (CQ-4262205).

* Al intentar vincular un fragmento de experiencia para una zona interactiva determinada en el componente [!UICONTROL Vídeo interactivo/Imágenes], no muestra la ruta de fragmento de experiencia seleccionada. En su lugar, devuelve un valor vacío del campo de ruta (NPR-35146, CQ-4298136).

* No se puede obtener una vista previa de un fragmento de experiencia en el Editor IVV (CQ-4308560).

* Al añadir una zona interactiva a una imagen y seleccionar un fragmento de experiencia, no es posible seleccionar las subcarpetas y las variantes del fragmento de experiencia (CQ-4307455).

* Los recursos que no son de imagen no se muestran como publicados después de su carga (CQ-4306415).

#### [!DNL Experience Manager] Recursos 3D  {#three-d-assets-6570}

* `DAM CQ MIME Type` el servicio aplica tipos MIME incorrectos a los recursos 3D, lo que provoca una representación incorrecta (NPR-34731).

### [!DNL Commerce] {#commerce-6570}

* La interfaz de usuario de Commerce product collection no enumera más de 15 productos dentro de una colección (NPR-34502).

### Plataforma {#platform-6570}

* Una sesión HTTP sobre HTTPS no se invalida (NPR-35083).
* Se devuelve un `NullPointerException` al iniciar tareas de mantenimiento diarias o semanales desde la interfaz de usuario (NPR-34953).
* El validador de W3C informa de advertencias para archivos JavaScript de la biblioteca de cliente compatibles (NPR-34898).
* La función `AudienceOmniSearchHandler` utiliza un índice obsoleto (NPR-34870).
* Cerrar sesión desde el Experience Manager no borra las cookies (NPR-34743).
* La función `findByTitle` de la API `TagManager` no funciona si el nombre de la etiqueta contiene un carácter especial (NPR-34357).
* El proceso de importación del paquete de sincronización de usuarios falla (NPR-34399).
* Se ha agregado compatibilidad con las propiedades `ariaLabel` y `ariaLabelledby` en el componente `Coral.Masonry` (GRANITE-29962).
* La caché de Dispatcher no se actualiza para páginas con fragmentos de contenido después de instalar los últimos paquetes de componentes principales (CQ-4306788).
* Los nombres de etiquetas localizados con comillas (`"`) no se muestran correctamente en la interfaz de usuario (CQ-4305439).

### Interfaz de usuario {#ui-6570}

* El campo [!UICONTROL Enlace a] de las propiedades del componente muestra sugerencias de autocompletado que no coinciden con la cadena especificada (NPR-34865).

* AEM muestra el siguiente mensaje de error cuando programa una ventana de mantenimiento diaria distribuida entre 2 días (NPR-35280):

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### Integraciones {#integrations-6570}

* La edición de una configuración [!DNL Adobe Launch] existente falla (NPR-35045).
* No se puede exportar [!DNL Experience Fragments] a [!DNL Adobe Target] si se utiliza la configuración IMS y el entorno [!DNL Adobe Target Standard] (NPR-34555).
* La opción [!UICONTROL Crear] aparece en la página [!UICONTROL Audiencias] al pasar de una carpeta a la página [!UICONTROL Audiencias] (NPR-35151).

### Sling {#sling-6570}

* La comprobación de estado de inicio de sesión predeterminada valida las credenciales de un usuario que no existe (NPR-34686).

### Proyectos de traducción {#translation-6570}

* Al cancelar un proyecto de traducción en [!DNL Experience Manager], la solicitud de cancelación no se envía al proveedor de traducción (NPR-34433).

### [!DNL Communities] {#communities-6570}

* Todos los casos de terminología no equitativa en el producto se sustituyen por equivalentes aceptados (NPR-34311).
* [!DNL Google+] se elimina de la lista de opciones de uso compartido en redes sociales (NPR-33877).

### [!DNL Brand Portal] {#brandportal-6570}

* La interfaz de usuario no responde al seleccionar los recursos en la [!UICONTROL Vista de lista] (NPR-34728).

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>[!DNL Experience Manager Forms] lanza los paquetes de complementos una semana después de la fecha de lanzamiento programada del paquete de servicio de [!DNL Experience Manager].

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack no incluye correcciones para  [!DNL Forms]. Se entregan mediante un paquete de complementos [!DNL Forms] independiente. Además, se ha lanzado un instalador acumulativo que incluye correcciones para [!DNL Experience Manager Forms] en JEE. Para obtener más información, consulte [Instalación del complemento de AEM Forms](#install-aem-forms-add-on-package) e [Instalación de AEM Forms en JEE](#install-aem-forms-jee-installer).

**Formularios adaptables**

* No se puede editar un formulario adaptable mediante la IU clásica después de aplicar [!DNL Experience Manager] Service Pack 6 (NPR-35126).

* Cuando se convierte un PDF en un formulario adaptable, no se puede establecer un valor para un panel anidado usando un modelo de datos de formulario en la presentación con fichas. Además, hay problemas al configurar un valor para los grupos de botones de opción de forma dinámica con una matriz estática mediante el editor de código (NPR-35062).

* Cuando se introducen caracteres japoneses en un componente de campo de texto en un formulario adaptable, se pueden especificar más caracteres que el límite máximo de 35 caracteres (NPR-35039).

* El formulario adaptable muestra parámetros no deseados, como `owner` y `status`, en la página **[!UICONTROL Gracias]** que se muestra después de enviar el formulario (NPR-34989).

* El cuadro de diálogo [!UICONTROL Selección de archivos] para el componente [!UICONTROL Attachment] muestra los tipos de archivo no admitidos, así como la selección que da como resultado un error durante el envío del formulario adaptable (NPR-34970).

* Cuando se inserta un formulario adaptable en una página [!DNL Experience Manager Sites] que incluye texto antes del formulario, el cursor se mueve directamente al formulario en lugar del texto antes del formulario (NPR-34947).

* [!UICONTROL La opción de vista previa con ] datos para rellenar previamente un formulario adaptable con un archivo XML de datos de  [!DNL Experience Manager] 6.2 no funciona correctamente (NPR-35087).

* Al actualizar el diccionario de datos de un formulario adaptable, el formulario no se traduce, ya que el formulario adaptable devuelve valores en caché (NPR-34845).

* Los fragmentos tardan más en cargarse de forma adaptable debido a la invalidación de la caché (NPR-34567).

* La navegación con pestañas no funciona correctamente para los lectores de pantalla de forma adaptativa (NPR-34544).

**Administración de correspondencia**

* No se pueden guardar valores para etiquetas XML con datos numéricos, que incluyen tipo flotante, como borrador (NPR-35050).

* Al migrar los recursos desde ES3, estos incluyen dos condiciones predeterminadas no editables (NPR-34972).

* Cuando edita un diccionario de datos en una carta, la sección [!UICONTROL Contenido de Cuarentena] muestra rectángulos giratorios en lugar de información útil (NPR-34853).

**Comunicación interactiva**

* El nombre de configuración de lanzamiento para la comunicación interactiva, disponible después de instalar el paquete de complementos [!DNL Forms], duplica el nombre de configuración de lanzamiento estándar (NPR-34976).

**Seguridad de los documentos**

* Cuando se guarda una nueva directiva de seguridad de documento, el Experience Manager Forms muestra el mensaje de error `Relative validity period is required` (NPR-34679).

* Document Security no es capaz de proteger el documento PDF 2.0 (CQ-4305851).

Para obtener información sobre las actualizaciones de seguridad, consulte la [página de boletines de seguridad del Experience Manager](https://helpx.adobe.com/security/products/experience-manager.html).

## [!DNL Adobe Experience Manager] 6.5.6.0  {#experience-manager-6560}

Adobe Experience Manager 6.5.6.0 es una actualización importante que incluye nuevas funciones, mejoras clave solicitadas por los clientes y mejoras de rendimiento, estabilidad y seguridad, publicadas tras la publicación general de la versión 6.5 en **abril de 2019**. Se puede instalar sobre Adobe Experience Manager 6.5.

Las funciones y mejoras clave introducidas en Adobe Experience Manager 6.5.6.0 incluyen:

* Publicar o cancelar la publicación de forma selectiva en [!DNL Experience Manager] o [!DNL Dynamic Media] mediante el asistente [!UICONTROL Publicación rápida] o [!UICONTROL Administrar publicación].

* Utilice la interfaz de usuario [!DNL Dynamic Media] para invalidar el contenido almacenado en caché de la red de entrega de contenido (CDN).

* La publicación de las carpetas de contribución de recursos desde Brand Portal en Recursos de Experience Manager ahora también se puede realizar a través del servidor proxy.

* Los grupos de carpetas privadas autogenerados ahora se limpian al eliminar la carpeta privada en [!DNL Experience Manager Assets].

* Las descripciones de los modificadores en el editor de ajustes preestablecidos de [!UICONTROL Viewer] se han actualizado en [!DNL Dynamic Media].

* Se proporciona una nueva configuración de empresa para reflejar el estado del conector [!DNL Dynamic Media].

* Las opciones predeterminadas para `test` y `aiprocess` se actualizan a `Thumbnail`, desde `Rasterize` anteriormente en Dynamic Media, para garantizar que los usuarios necesiten crear solo miniaturas y omitir la extracción de páginas y la extracción de palabras clave.

* [Rellene previamente un formulario adaptable en el cliente](../../help/forms/using/prepopulate-adaptive-form-fields.md#prefill-at-client).

* [Integración del modelo de datos de formulario con las API de RESTful en un servidor con implementación](../../help/forms/using/configure-data-sources.md) de SSL bidireccional.

* [Almacenamiento en caché mejorado para páginas](../../help/forms/using/configure-adaptive-forms-cache.md) de formularios adaptables traducidas.

* Compatibilidad con [Etiquetas de texto de Adobe Sign en el servicio de Automated forms conversion](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html).

* Compatibilidad con [convertir formularios de color en formularios adaptables](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html) mediante [!DNL Automated Forms Conversion service].

* Compatibilidad con los protocolos SMB 2 y SMB 3.

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.22.4.

Para obtener una lista completa de las funciones y mejoras introducidas en Experience Manager 6.5.6.0, consulte [Novedades de Adobe Experience Manager 6.5 Service Pack 6](new-features-latest-service-pack.md).

La siguiente es la lista de correcciones que se proporcionan en la versión [!DNL Experience Manager] 6.5.6.0.

### [!DNL Sites] {#sites-6560}

* En [!DNL Sites] o [!DNL Screens], seleccione un proyecto y haga clic en [!UICONTROL Publicaciones de administración]. Los usuarios no pueden avanzar en el asistente [!UICONTROL Administrar publicación] debido a errores en la interfaz de usuario. Específicamente, la opción [!UICONTROL Publicar] no funciona (NPR-34099).
* La posición de iParsys (Sistema de párrafos heredado) no se revierte a su posición predeterminada original después de anular la selección de las opciones [!UICONTROL Cancelar herencia] o [!UICONTROL Deshabilitar herencia] (NPR-34097).
* Si el `RolloutConfigManagerFactoryImpl` no puede cargar una configuración de lanzamiento, no intenta cargar las configuraciones que faltan. Devuelve las configuraciones en caché (NPR-34092).
* En el componente principal de texto, después de utilizar la opción de edición HTML de origen, se elimina la clase de la etiqueta `em` (NPR-34081).
* Después de actualizar de Experience Manager 6.3.3 a Experience Manager 6.5.3, el proceso de implementación tarda mucho más y el lanzamiento falla con un error de tiempo de espera (NPR-34049).
* El `htmlwriter` no codifica los valores de atributo. El marcado presente en el marcado XF se exporta con valores de atributo decodificados (concretamente `"` en lugar de `&#34`). Provoca problemas en el lado de Target con el Compositor de experiencias visuales que utiliza el XF exportado (NPR-34048).
* Al mover páginas en [!DNL Experience Manager Sites], mejore el registro para capturar el error de creación de versiones con el motivo (NPR-34014).
* En [!DNL Rich Text Editor] si se elimina todo el texto, también se elimina la etiqueta de párrafo (NPR-33976).
* Cuando se abre o actualiza la página `siteadmin` (en la IU clásica), las opciones del menú `New` se desactivan (NPR-33949).

   ![Captura de pantalla para ilustrar el problema de la falta de menú en la IU clásica](assets/33949_missing_menu.png)

* Un [!DNL Content Fragment] no se puede usar como `TemplatedResource` ya que falla en `ContentFragmentUsePojo` (NPR-33911).
* Las operaciones de movimiento sincrónico y asíncrono pueden provocar errores debido a transferencias simultáneas. Las operaciones de movimiento de página están restringidas únicamente al movimiento asincrónico. Evita el movimiento simultáneo de páginas (NPR-33875).
* [!UICONTROL La operación Administrar ] publicación para replicar contenido de la instancia Autor a Publicación falla y genera un error de JavaScript (NPR-33872).
* Cuando se seleccionan varias páginas o recursos para crear versiones, la nueva versión se crea solo para la última página o recurso seleccionado (NPR-33866).
* Mueva una página de modelo con Live Copies a otra carpeta. Al moverlo a la carpeta original, la operación de movimiento falla sin ningún error (NPR-33864).
* Cuando se utiliza la acción de mover para cambiar el nombre de una página web en la consola [!DNL Sites] , se muestran dos cuadros de diálogo superpuestos en el último paso del asistente (NPR-33831).

   ![Captura de pantalla para ilustrar el problema NPR-33831 de diálogo de movimiento superpuesto](assets/33831_rename_dialog.png)

* Las propiedades `cq:acLinks` y `cq:acUUID` de [!DNL Adobe Campaign] de la copia se eliminan durante la operación de copiar y pegar (NPR-33794).
* Al intentar un despliegue en una página secundaria de una Live Copy principal independiente, [!DNL Experience Manager] genera una excepción de puntero nulo (NPR-33676).
* Los componentes [!DNL RTE] de un contenedor de diseño no están visibles cuando el contenedor de diseño se copia y se vuelve a pegar en la página. Los componentes [!DNL RTE] no se pueden editar, pero se muestran al actualizar la página (NPR-33662).
* Al cambiar el tamaño de un componente de diseño para diferentes puntos de interrupción (medio y grande), el diseño no se comporta como se espera (NPR-33608).
* En el modo de edición en línea en [!DNL RTE], arrastrar una imagen no funciona para el componente Texto (NPR-33602).
* Es posible crear un componente en una página de modelo con el mismo nombre que el nombre de la página. Durante el despliegue, `_msm_moved` se añade un sufijo para cambiar el nombre del componente. El componente se mueve al final del [!UICONTROL Sistema de párrafos] (NPR-33535).
* Cuando offTime o onTime están configurados en muchas páginas o recursos, requieren muchos recursos y ralentizan el sistema durante el inicio y el cierre (NPR-33482).
* Un usuario con permisos CRUD en `/content/experience-fragment` no puede eliminar una carpeta (NPR-33436).
* Puede seleccionar [!UICONTROL HTML y JSON] como opción para [!UICONTROL Adobe Target export format] en una carpeta principal de la sección [!DNL Experience Fragments]. Las mismas propiedades se muestran en la IU táctil para las subcarpetas de esta carpeta principal. Sin embargo, en CRXDE, para `cq:adobeTargetExportFormat`, solo muestra HTML en lugar de mostrar `html,json` (NPR-33423).
* No se admite Publicar o Cancelar la publicación desde un alias de página. Elimine la opción que parece reclamar lo contrario (NPR-33415).
* Una etiqueta específica se puede mover de una ubicación a otra en [!DNL Experience Manager]. También se puede aplicar a diferentes páginas antes y después de moverse. Al editar las propiedades de las páginas, la etiqueta no se muestra para su edición aunque la etiqueta sea la misma (NPR-33353).
* Una plantilla de página no se representa correctamente cuando se elimina un contenedor de diseño de una plantilla que contiene varios contenedores de diseño (NPR-33347).
* En el editor de plantillas, intente eliminar una plantilla utilizada por más de 100 000 páginas en `/content/`. Se muestra un error sin ningún mensaje de error (NPR-33312).
* La redirección a la página [!DNL Experience Manager] con anclaje no funciona en la instancia de autor, ya que `PageRedirectServlets` coloca la cadena de consulta después de un fragmento de URL o un anclaje (NPR-34288).
* La creación de una marca en `/content/campaign` resulta en una estructura que no permite crear campañas. [!UICONTROL La opción Crear ] marca deja a la marca recién creada sin capacidad para crear  [!UICONTROL ofertas y ] actividades, ya que no hay   opción de creación (NPR-34113).
* Puede suspender el [!DNL Live Copy] de una página y la herencia se rompe como se ve en el modo Editor. En las propiedades de página, el icono que representa la herencia indica incorrectamente que la herencia existe y no se rompe (NPR-34017).
* Las páginas con muchas referencias no se pueden mover asincrónicamente y, a veces, la operación de movimiento falla (CQ-4297969).
* Una página web con el carácter `/` en la dirección URL deja de responder durante la creación. Cuando se añade un componente durante la creación, el uso de la CPU aumenta y el explorador deja de responder (CQ-4295749).
* En el modo Examinar, NVDA no narra un valor seleccionado en la opción de menú Tipo/Tamaño. El enfoque visual no está en el elemento seleccionado. Los usuarios que dependen de un lector de pantalla no pueden utilizar el modo Examinar (CQ-4294993).
* Al crear una página web, los usuarios pueden seleccionar la plantilla [!UICONTROL Página de contenido] . En la pestaña [!UICONTROL Social Media], los usuarios seleccionan una [!UICONTROL Variación de XF preferida]. Para seleccionar un fragmento de experiencia en el modo de exploración NVDA, los usuarios no pueden utilizar teclas de teclado (CQ-4292669).
* Se ha actualizado la biblioteca de controladores a la versión más segura 4.7.3 (NPR-34484).
* Varias instancias de scripts entre sitios en componentes [!DNL Experience Manager Sites] (NPR-33925).
* El campo de nombre de la carpeta al crear una nueva carpeta es vulnerable a las secuencias de comandos entre sitios almacenadas (GRANITE-30094).
* Los resultados de búsqueda de la página [!UICONTROL  bienvenida] y la plantilla de finalización de ruta son vulnerables a scripts entre sitios (NPR-33719, NPR-33718).
* La creación de una propiedad binaria en un nodo no estructurado da como resultado secuencias de comandos entre sitios en el cuadro de diálogo de propiedades binarias (NPR-33717).
* Ejecución de scripts en sitios múltiples al utilizar la opción [!UICONTROL Control de acceso Test] en la interfaz CRX DE (NPR-33716).
* Las entradas del usuario no se codifican correctamente para distintos componentes al enviar información al cliente (NPR-33695).
* Ejecución de scripts en sitios múltiples en la vista Calendario de la bandeja de entrada del Experience Manager (NPR-33545).
* Una dirección URL que termina con `childrenlist.html` muestra una página HTML en lugar de una respuesta 404. Estas direcciones URL son vulnerables a la ejecución de scripts en sitios múltiples (NPR-33441).


### [!DNL Assets] {#assets-6560}

**Mejoras de accesibilidad en Recursos Experience Manager**

* Con las teclas del teclado, los usuarios ahora pueden acceder a las opciones de la interfaz de usuario interactiva en la lista de recursos [!UICONTROL Referencias] (NPR-34115) y centrarse en ellas.

* El lector de pantalla ahora anuncia la acción prevista de los predicados en la página de búsqueda (NPR-34104).

* La página de búsqueda y la página de resultados de búsqueda ahora tienen títulos más informativos para comprender mejor a los usuarios de lectores de pantalla (NPR-34093).

* Los lectores de pantalla ahora anuncian las opciones para eliminar las etiquetas seleccionadas en la pestaña [!UICONTROL Básico] de la página [!UICONTROL Propiedades] del recurso (NPR-33972).

* Los elementos de cada fila de la vista de lista ahora se anuncian como los elementos de la misma fila por los lectores de pantalla (NPR-33932).

* El enfoque del usuario al navegar con la tecla `Tab` ahora se mueve a la opción de cierre en la vista previa de la versión (NPR-33863).

* El enfoque del usuario ahora pasa al icono de búsqueda después de cerrar Omnisearch (NPR-33705).

* Las opciones de interfaz de usuario procesables ahora tienen un enfoque visual más destacado con un contraste mejorado cuando se navega con teclas de teclado. Los usuarios del teclado pueden identificar las áreas enfocadas (NPR-33542).

* La funcionalidad de arrastrar con el teclado ahora funciona en [!UICONTROL Editor de esquemas de metadatos] en el modo de exploración del lector de pantalla (CQ-4296326).

* En el cuadro de diálogo de uso compartido de vínculos, al navegar en el modo Examinar, un lector de pantalla,

   * No narra la información de la tabla en cuanto se carga el cuadro de diálogo.

   * Puede navegar a todas las sugerencias automáticas de la lista.

   * Narra las sugerencias automáticas mostradas para [!UICONTROL Añadir dirección de correo electrónico/Buscar] (CQ-4294232).

* El uso de la tecla `Esc` para eliminar los iconos de acción rápida de la vista de tarjeta ya no elimina el enfoque del teclado del último elemento focalizado (CQ-4293554).

* Para las opciones interactivas en la interfaz de usuario, el lector de pantalla ahora anuncia su propósito en lugar de los nombres literales de los iconos (CQ-4272943).

* El foco del teclado ahora se mueve correctamente a [!UICONTROL Flotante], [!UICONTROL InlineZoom], [!UICONTROL Banner_comprador], [!UICONTROL Zoom_dark], [!UICONTROL Zoom_light], [!UICONTROL ZoomVertical_dark&lt;a11/ Opciones>, y [!UICONTROL ZoomVertical_light] al navegar mediante la tecla de tabulación del teclado en los detalles del recurso [!UICONTROL Visualizadores] en [!DNL Dynamic Media] (CQ-4290605).]

* [!UICONTROL Ahora se puede acceder a la opción Guardar y ] cerrar de la página   Propiedades del recurso mediante las teclas de teclado (NPR-34107).

* Los lectores de pantalla ahora anuncian los mensajes de error debido a combinaciones incorrectas de nombre de usuario y contraseña en la página de inicio de sesión cada vez que se produce el error (NPR-33722).

* En la sección del encabezado [!DNL Experience Manager], al navegar en el modo Examinar, el lector de pantalla ahora anuncia,

   * Sugerencias editadas automáticamente en [!UICONTROL Tipo para buscar] en Omnisearch.

   * El estado se expande o contrae para las opciones [!UICONTROL Solutions], [!UICONTROL Help], [!UICONTROL Inbox] y [!UICONTROL User].

   * El mensaje de estado [!UICONTROL Búsqueda de ayuda] que se muestra cuando el usuario introduce una cadena de búsqueda en el campo [!UICONTROL Buscar ayuda] en la opción [!UICONTROL Ayuda].

   ![Menú Ayuda del encabezado](assets/Help_aem_header.png)

   *Figura:  [!UICONTROL Busque ] Helpin   Helpmenu.*

   * El mensaje de error si se introduce un valor incorrecto en el campo [!UICONTROL Suplantar como] en la opción [!UICONTROL Usuario] y el enfoque se mueve correctamente al campo de texto (NPR-33804).

   ![Menú del usuario en el encabezado](assets/User_aem_header.png)

   *Figura:  [!UICONTROL Suplantar ] un campo en el menú   Usuario del encabezado.*

* El usuario ahora puede cambiar el enfoque mediante el teclado en:

   * [!UICONTROL Campo Buscar/agregar ] dirección de correo electrónico en el cuadro de  [!UICONTROL diálogo ] Compartir vínculos .

   * [!UICONTROL Agregue Usuario o ] Groupfield en  [!UICONTROL Grupo cerrado de usuarios ] la pestaña   Permiso de las  [!UICONTROL propiedades]  de la carpeta (NPR-34452).

**Problemas corregidos en Recursos de Experience Manager**

[!DNL Adobe Experience Manager] 6.5.6.0  [!DNL Assets] proporciona correcciones a los siguientes problemas:

* Las anotaciones no se resaltan al seleccionarlas en la cronología del recurso (CQ-4302422).

* La vista previa de los activos de garantía de marketing (como Folleto, Volante y Tarjeta de presentación) creados con la plantilla [!DNL Adobe InDesign] no muestra saltos de línea y saltos de párrafo (NPR-34268).

* La extracción de texto y, por lo tanto, la búsqueda de texto completo de los archivos PDF cargados no funciona (NPR-34164). Para solucionarlo, reinicie la implementación [!DNL sAdobe Experience Manager] después de instalar el Service Pack 6.

* La línea de tiempo de los recursos de varias páginas muestra anotaciones aplicadas a todos los subrecursos al examinar el recurso en la vista Línea de tiempo, en lugar de mostrar las anotaciones específicas de los subrecursos específicos (NPR-34100).

* Las carpetas de recursos no se publican mediante la opción [!UICONTROL Administrar publicación] si las carpetas contienen recursos en los formatos de archivo JavaScript, CSS o JSON (NPR-34090).

* Al anular la selección o eliminar las etiquetas o filtros aplicados en Omnisearch, se ejecuta la consulta de búsqueda varias veces, lo que aumenta el tiempo de búsqueda (NPR-34078).

* En la vista de tarjeta, cuando un flujo de trabajo (en un recurso de una carpeta) está en curso o pendiente, la página se vuelve a cargar hasta que el flujo de trabajo se completa o finaliza. Por lo tanto, los autores no pueden trabajar en esos recursos de la carpeta para la que tienen que desplazarse hacia abajo (NPR-33986).

* Si el usuario mueve un recurso publicado a una nueva ubicación, el recurso se vuelve a publicar aunque la opción [!UICONTROL Volver a publicar] no esté seleccionada. Esto lleva a que muchos recursos huérfanos yacen en la instancia de publicación. Sin embargo, el comportamiento predeterminado es que la operación de movimiento en un recurso publicado lo anula de forma automática; este recurso se vuelve a publicar si el autor selecciona la opción [!UICONTROL Volver a publicar] al mover el recurso (NPR-33934).

* La página [!UICONTROL Mover recursos] para los recursos de las colecciones no carga todo el contenido HTML, como la opción [!UICONTROL Ajustar/ volver a publicar]. Por lo tanto, los usuarios no pueden completar la operación de traslado (NPR-33860).

* Mover un recurso y añadir caracteres especiales en el nombre y el título de los recursos movidos crea una carpeta adicional (con el mismo nombre) en la nueva ubicación del recurso (NPR-33826).

*  El botón de descarga de un recurso se desactiva cuando se selecciona la opción   Correo electrónico en el   cuadro de diálogo Descargar (NPR-33730).

* El error &quot;URI de solicitud demasiado largo&quot; se observa al realizar operaciones masivas en recursos, como la edición masiva de metadatos (NPR-33723).

* Se observa un error de JavaScript y los usuarios no pueden seleccionar ni eliminar las opciones generadas en el campo [!UICONTROL Desplegable] mediante la funcionalidad [!UICONTROL Agregar a través de la ruta JSON] en el [!UICONTROL Editor del formulario de esquema de metadatos de la carpeta], si el archivo JSON cargado tiene espacio o caracteres especiales en su valor (NPR-33377112).

* Las representaciones estáticas de los recursos no se actualizan cuando el recurso se actualiza mediante la opción [!UICONTROL Open] en [!DNL desktop app] o [!DNL Adobe Asset Link] y se sincronizan de nuevo con [!DNL Adobe Experience Manager] (CQ-4296279).

* En la vista de columna, la operación de mover de un conjunto de recursos también mueve los recursos seleccionados antes de utilizar la opción [!UICONTROL Filter] para ellos. Tenga en cuenta que el uso de la opción [!UICONTROL Filter] anula la selección anterior (NPR-34018).

* Las barras invertidas se añaden antes que los caracteres especiales en las sugerencias de búsqueda de recursos, que tienen caracteres especiales en su nombre (NPR-33834).

* Al crear reglas para la lista desplegable en [!UICONTROL Formulario de esquema de metadatos de carpeta], el usuario no puede seleccionar valores de la columna [!UICONTROL Opciones de campo] (CQ-4297530).

* La copia en tiempo de ejecución del modelo de flujo de trabajo personalizado de los recursos (creado en `/var/workflow/models/dam`) se elimina al instalar [!DNL Experience Manager] 6.5 Service Pack 5 o una versión anterior en [!DNL Experience Manager] 6.5 (NPR-34532). Para recuperar la copia en tiempo de ejecución, sincronice la copia en tiempo de diseño del modelo de flujo de trabajo con la copia en tiempo de ejecución mediante la API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

**Problemas corregidos en Dynamic Media**

* Si el usuario define la configuración de codificación en ediciones después de crear el perfil de vídeo, la configuración de recorte inteligente se elimina de los perfiles de vídeo (CQ-4299177).

* Los recursos parpadean al cargar la página cuando el usuario cambia entre las opciones de raíl lateral (por ejemplo, [!UICONTROL Información general], [!UICONTROL Línea de tiempo], [!UICONTROL Visualizadores]) en la página de detalles del recurso (NPR-34235).

* Los siguientes problemas se observan con el trabajo de reprocesamiento:

   * Falta el ID de trabajo en el identificador de trabajo devuelto por el trabajo de reprocesamiento.

   * Reprocesar el trabajo para registros de vídeo solo nombre de archivo y no ruta completa.

   * El trabajo de reprocesamiento no tiene la opción de establecer el tipo de recurso como estático.

   * `ExcludeFromAVS` no se proporciona (CQ-4298401).

* La funcionalidad de recorte inteligente falla con un error cuando el perfil de imagen se agrega a una carpeta que tiene varias relaciones de aspecto (por ejemplo, 11) (NPR-34082).

* El flujo de trabajo de los recursos de actualización de DAM se activa cuando el usuario se desplaza hacia abajo en la página [!UICONTROL Archivo de flujo de trabajo] en la pestaña [!UICONTROL Flujo de trabajo] dentro de [!UICONTROL Herramientas] en [!DNL Adobe Experience Manager] configurada con Dynamic Media Scene7 (CQ-4299727).

* Los símbolos de la pestaña [!UICONTROL Behavior] del [!UICONTROL Editor de ajustes preestablecidos de visualizador] no están localizados (CQ-4299026).

* La vista principal muestra la imagen con un diseño incorrecto que no cabe en el visor si este se encuentra en modo interactivo (CQ-4298293).

* Los cambios en los ajustes preestablecidos de imagen en [!UICONTROL Adobe Experience Manager] no se sincronizan con Scene7 Publishing System (CQ-4299713).

### [!DNL Commerce] {#commerce-6560}

* Los vínculos a recursos de productos no se refactorizan cuando se mueven recursos (NPR-34098).

### Plataforma {#platform-6560}

* No se pueden descargar registros con la herramienta Diagnóstico en una instancia de Experience Manager actualizada (NPR-34336).
* La actualización falla con un error debido a las dependencias en una versión específica del paquete de base `cq-wcm-api` (CQ-4300520).
* No se especifican los valores predeterminados para las opciones **[!UICONTROL Connect Timeout]** y **[!UICONTROL Socket Timeout]** para la configuración del Agente predeterminado (publicación) (NPR-33707).
* Las actualizaciones en la configuración de asignación en `/etc/map.publish` no se reflejan en las páginas del sitio (NPR-34015).
* [La ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html) documentación de referencia de la API no incluye la documentación del  `com.day.cq.tagging` paquete (CQ-4295864).

### Interfaz de usuario {#ui-6560}

* La interfaz del explorador de descarga no muestra todos los temas del trabajo (NPR-34308).
* La interfaz [Configuration Browser](/help/sites-administering/configurations.md) no muestra todas las configuraciones (NPR-33644).
* Al pulsar la tecla `Esc` al buscar usuarios que suplanten, se cierra el cuadro de diálogo **[!UICONTROL Usuario]** en lugar de la lista de usuarios (NPR-34084).

### Integraciones {#integrations-6560}

* Las actividades con nombres largos no se sincronizan con [!DNL Adobe Target] (NPR-34254).

* Al seleccionar una propiedad al crear una nueva configuración de Launch de Adobe, aparece el siguiente mensaje de error (NPR-33947):

   ```javascript
   GET http://hostname:Port/libs/cq/dtm-reactor/content/configurations/createcloudconfigwizard/jcr:content/body/items/form/items/wizard/items/general/items/fixedcolumns/items/container/items/general/items/property/data.html?query=&start=0&end=25&imsConfigurationId=Adobe%20Launch&companyId=&_charset_=utf-8 400 (Bad Request)
   ```

### Proyectos de traducción {#translation-6560}

* No se crea un proyecto de traducción si el `authorizableID` del usuario incluye caracteres especiales (NPR-33828).

### Sling  {#sling-6560}

* La comprobación de estado y el detector de patrones tienen una funcionalidad superpuesta. Como resultado, la comprobación de estado se elimina del producto (NPR-33928).

### WCM {#wcm-6560}

* Componentes de base: cuando se añade un componente de imagen de base a una página y se hace referencia a una imagen, la operación `Undo` no funciona (NPR-34516).

* No se puede usar la operación de movimiento de página (CQ-4303028).

### [!DNL Communities] {#communities-6560}

* Compartir una publicación en medios sociales muestra una opción obsoleta de Google+ (NPR-33877).

* El miembro de la comunidad no puede modificar la plantilla de grupo u otra configuración de función de grupo (NPR-33530).

* Las etiquetas de hipervínculo de las imágenes no se generan correctamente en una publicación de foro (NPR-33464).

* Los errores de accesibilidad se identifican en la función Asignación de la comunidad (NPR-33442).

* Los usuarios existentes de un grupo de comunidad agregados a través de Admin Console se eliminan de la lista de usuarios en cualquier modificación en la consola de grupo de la comunidad (NPR-34315).

* El `TagFilterServlet` filtra datos potencialmente confidenciales (NPR-33868).

<!--
* Tag filters are vulnerable to sensitive information disclosure (NPR-33868).
-->

### [!DNL Forms] {#forms-6560}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack no incluye correcciones para  [!DNL Forms]. Se entregan mediante un paquete de complementos [!DNL Forms] independiente. Además, se ha lanzado un instalador acumulativo que incluye correcciones para [!DNL Experience Manager Forms] en JEE. Para obtener más información, consulte [Instalación del complemento de AEM Forms](#install-aem-forms-add-on-package) e [Instalación de AEM Forms en JEE](#install-aem-forms-jee-installer).

Después de instalar el paquete de complementos [!DNL Experience Manager Forms] 6.5.6.0:

* Detenga la instancia [!DNL Experience Manager Forms].

* Elimine los archivos `bcpkix-1.51`, `bcmail-1.51` y `bcprov-1.51` JAR del directorio `crx-repository\launchpad\ext`.

* Eliminar la propiedad` sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider` del archivo `sling.properties`.

* Reinicie la instancia [!DNL Experience Manager Forms].

**Formularios adaptables**

* Cuando falta un fragmento de formulario adaptable, el formulario adaptable no se puede procesar (NPR-34302).

* La descripción del contenido de ayuda de los campos de formulario adaptables muestra una etiqueta HTML de párrafo (NPR-34116).

* Cuando se selecciona la propiedad **[!UICONTROL Revalidate on Server]**, el formulario adaptable no se envía (NPR-33876).

* La acción de envío **[!UICONTROL Submit to REST endpoint]** no funciona para una forma adaptativa (CQ-4299044).

* Accesibilidad: Cuando se intenta enviar un formulario adaptable sin cargar un archivo adjunto para un campo obligatorio, el enfoque no se desplaza automáticamente al campo adjunto (CQ-4298065).

* Cuando se agregan filas a una tabla de un formulario adaptable, las opciones **[!UICONTROL Add to top]** y **[!UICONTROL Add to bottom]** no muestran los resultados adecuados (CQ-4297511).

* La secuencia de comandos [!UICONTROL Value Commit] se activa incorrectamente, lo que provoca la pérdida de datos de forma adaptativa (CQ-4296874).

* El selector de fechas no funciona correctamente en formularios adaptables localizados (NPR-34333).

* Cuando hay un guión bajo o un espacio en el nombre del archivo, no se puede adjuntar el archivo a un formulario adaptable (CQ-4301001).

* Cuando un panel repetible anidado tiene más ocurrencias que su principal, todas las ocurrencias de dicho panel repetible anidado no se pueden rellenar previamente (NPR-33666).

* Los formularios adaptables tienen algunos resueltores de recursos abiertos. Esto provoca errores de envío. El problema se produce de forma intermitente (CQ-4299407).

* Cuando se abre la configuración de campo por primera vez, no se muestra el icono de propiedades (CQ-4296284).

* Los usuarios pueden editar los metadatos del envío, como `afPath`, `afSubmissionTime` y `signers`, al enviar un formulario adaptable. Para resolver el problema, los valores de metadatos se eliminan de los datos de envío del formulario en el lado del cliente. Los usuarios pueden utilizar el objeto `FormSubmitInfo` para recuperar estos valores del servidor (NPR-33654).

* Las entradas del usuario no están correctamente codificadas para los componentes [!DNL Forms] al enviar información al cliente (NPR-33611).

**Flujo de trabajo**

* Cuando un aprobador de flujo de trabajo carga un archivo adjunto, este se cambia a `undefined` (NPR-33699).

* [!DNL Experience Manager] La operación de purga del flujo de trabajo falla y muestra el siguiente mensaje de error (NPR-33575):

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* [!DNL Experience Manager Forms] aplicación para  [!DNL Windows] deja de responder después de enviar un formulario (NPR-34409).

* Cuando instala AEM Service Pack, la lista de elementos **To Do** no se muestra como vínculos. El texto de los elementos **To Do** incluye etiquetas HTML (NPR-34317).

**Comunicación interactiva**

* Cuando se incluye un fragmento de documento de texto con componentes repetibles anidados, la comunicación interactiva no se guarda (NPR-34095).

**Administración de correspondencia**

* Cuando modifica un fragmento de documento de texto que incluye valores de diccionario de datos, la interfaz de usuario del agente deja de responder (NPR-33930).

* Copiar y pegar contenido de un documento [!DNL Microsoft Word] en un fragmento de documento de texto en una carta genera problemas de formato (NPR-33536).

**Servicios de documento**

* Cuando se genera un archivo PDF a partir de un archivo XDP mediante los servicios Output y Forms, el resultado es que falta texto y que se superpone (NPR-34237, CQ-4299331).

* Cuando se convierte un archivo HTML a PDF, el atributo `MaxReuseCount` no se puede configurar (NPR-33470).

* Cuando descarga un archivo PDF que incluye funciones interactivas de Extensiones de Reader, no puede agregar un archivo adjunto al archivo PDF mediante [!DNL Adobe Reader] (NPR-33729).

**Seguridad de los documentos**

* No se puede ejecutar la operación de firma con certificados basados en HSM en un archivo PDF después de instalar [!DNL Experience Manager] Service Pack (NPR-34310).

**Diseñador**

* No se pueden abrir XForms en Designer versión 6.5.x (CQ-4295322).

* Cuando se abre Designer, la pantalla de bienvenida muestra un año incorrecto (CQ-4295289).

* Cuando instala [!DNL Acrobat DC] en el servidor, la opción **[!UICONTROL Distribuir formulario]** está inactiva (CQ-4296304).

Para obtener información sobre las actualizaciones de seguridad, consulte la [página de boletines de seguridad del Experience Manager](https://helpx.adobe.com/security/products/experience-manager.html).

## [!DNL Adobe Experience Manager] 6.5.5.0  {#experience-manager-6550}

Adobe Experience Manager 6.5.5.0 es una actualización importante que incluye nuevas funciones, mejoras clave solicitadas por los clientes y mejoras de rendimiento, estabilidad y seguridad, publicadas tras la publicación general de la versión 6.5 en **abril de 2019**. Se puede instalar sobre Adobe Experience Manager 6.5.

Algunas de las funciones y mejoras clave introducidas en [!DNL Adobe Experience Manager] 6.5.5.0 incluyen:

* No se permite el acceso anónimo al CRXDE Lite. En su lugar, se dirige a los usuarios a la pantalla de inicio de sesión. Consulte [Desarrollo con el CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* Personalice los nombres de columna que se muestran en la bandeja de entrada [!DNL Adobe Experience Manager].

* Se ha mejorado la accesibilidad en varias áreas de la administración de contenido web de Experience Manager (WCM), como el Editor de páginas, los componentes principales, RTE y la interfaz de usuario de administración.

* Guarde un [!DNL Interactive Communication] como borrador.

* Compatibilidad con [!DNL Oracle WebLogic 12] para Forms Experience Manager en JEE.

* Se ha mejorado la gestión de excepciones en el flujo de interfaz de usuario [!DNL Adobe Experience Manager Assets].

* Para obtener la URL de publicación para Dynamic Media Scene7, se agrega un nuevo método `getRemoteAssetPublishURL` a la interfaz `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi`.

* [Las ](#assets-6550) mejoras de accesibilidad cumplen  [!DNL Adobe Experience Manager Assets] las directrices de accesibilidad del contenido web (WCAG).

* Se ha eliminado la integración de Uso compartido de paquetes de Adobe Experience Manager.

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.22.3.

Para obtener una lista completa de las funciones, los aspectos más destacados y las funciones clave introducidas en Experience Manager 6.5 Service Pack 5, consulte [Novedades del Service Pack 5](new-features-latest-service-pack.md) de Adobe Experience Manager 6.5 .

La siguiente es la lista de correcciones que se proporcionan en la versión [!DNL Experience Manager] 6.5.5.0.

### [!DNL Sites] {#sites-6550}

* Experience Manager Sites proporciona una opción para publicar o cancelar la publicación de una página desde su alias. La opción no funciona (NPR-33415).
* Cuando se elimina un contenedor de diseño de una plantilla que contiene varias plantillas, la plantilla no se representa correctamente (NPR-33347).
* Cuando una página Sitios Experience Manager forma parte de un conjunto de contenido grande con varias Live Copies, la vista previa del historial de versiones de la página no se carga (NPR-33311).
* Cuando utiliza el comando Mover para cambiar el nombre de una página Sitios Experience Manager, el título de la página no se actualiza (NPR-33264).
* Al mover páginas a través de la vista de columna, las columnas desaparecen (NPR-33216).
* Cuando el nombre de un componente local en una copia de idioma es idéntico al nombre de un componente en el modelo y el componente se despliega desde el modelo, el término `_msm_moved` no se agrega al nombre del componente local (NPR-33208).
* El servlet de redireccionamiento de página anexa .html a una URL de sitios Experience Manager donde ResourceType no es `cq:Page` (NPR-33176).
* Al pegar un subárbol, no hay opción de decidir si las subpáginas correspondientes se pegarán o no (NPR-33149).
* El número de resultados en el uso activo de un componente está limitado al número 49 (NPR-33058).
* Cuando se basa un fragmento de contenido en un esquema y contiene un área de texto obligatoria o un campo de ruta, el fragmento de contenido no se guarda (NPR-33007).
* Al crear un componente personalizado utilizando el componente de fragmento de experiencia predeterminado y utilizarlo en páginas de sitios de Experience Manager, el Experience Manager no muestra referencias (uso) para el componente personalizado (NPR-32852).
* Al cambiar el nombre de una carpeta con un gran número de referencias, muchas referencias a la carpeta no se actualizan (NPR-32765).
* Cuando activa la opción de edición de la fuente, esta está disponible para las opciones de pantalla completa en línea, pero sigue faltando para el cuadro de diálogo de edición y las opciones de pantalla completa del editor de texto enriquecido (NPR-32763).
* Si tiene un campo múltiple y contiene un campo obligatorio (como un campo desplegable o un campo de ruta) en las propiedades de página de un modelo, cuando se despliega una página que contiene un campo múltiple de este tipo, las propiedades de página de la copia activa no se guardan (NPR-32751).
* Los lectores de pantalla no pueden utilizar la estructura de encabezado para desplazarse por una página. Además, la ficha Componentes tiene la etiqueta incorrecta (NPR-32648).
* Cuando se inicia la paginación, el Selector de fragmentos de experiencia no carga todos los elementos (NPR-32605).
* Los permisos de autor para leer, modificar, crear y eliminar Live Copies se revocan. Cada autor tuvo que proporcionar explícitamente permisos de lectura y modificación para mover páginas dentro de un modelo (NPR-32550).
* Los autores de contenido no pueden crear Launch para una página que tenga una integración con Adobe Analytics (NPR-32548).
* Cuando un usuario reanuda la herencia con la sincronización, la Live Copy de la página principal no se sincroniza con el modelo y muestra un estado incorrecto (NPR-32500).
* La página del editor de sitios de Experience Manager tarda más de 15 segundos en cargarse (NPR-32413).
* Algunos campos no muestran la opción Cancelar herencia (NPR-32362).
* Al seleccionar una ruta para un componente Fragmento de experiencia y seleccionar la casilla de verificación Abrir cuadro de diálogo de selección , no se desplaza a la ruta seleccionada en el Explorador de rutas (NPR-32308).
* Al actualizar de Experience Manager 6.2 a Experience Manager 6.5, el componente Parsys de las plantillas estáticas no se muestra correctamente. La altura del componente Parsys se establece en 0 y los componentes que contiene no son visibles (NPR-33663).
* Cuando un usuario copia y pega un contenedor de diseño en la misma página, los componentes de un contenedor de diseño no se muestran (NPR-33648).
* La comprobación de estado de Dispatcher muestra `Invalid cookie header` un mensaje de advertencia en los archivos de registro (NPR-33629).
* XSS reflejado en PreferencesServlet (NPR-33438).
* Los usuarios anónimos pueden acceder a las funciones del CRXDE Lite (GRANITE-27790).

### [!DNL Assets] {#assets-6550}

>[!IMPORTANT]
>
>Se recomienda a los usuarios de Windows de [!DNL Experience Manager desktop app] que actualicen a la [aplicación de escritorio versión 2.0.3.2](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html#whats-new-added) para acceder al repositorio DAM en la instancia [!DNL Adobe Experience Manager 6.5.5.0]. Como pueden encontrar problemas al acceder al repositorio de DAM en la instancia [!DNL Adobe Experience Manager] 6.5.5.0 usando la aplicación de escritorio versión 2.0.2.

**Mejoras de accesibilidad en Recursos Experience Manager**

* Ahora es posible centrarse en el teclado en la lista [!UICONTROL Comentarios] y en la opción en la que se puede hacer clic para [!UICONTROL Crear] comentarios de la versión en [!UICONTROL Crear nueva versión] en el panel de activos [!UICONTROL Línea de tiempo] (NPR-33424).

* Ahora es posible alcanzar la opción [!UICONTROL Ver configuración] para los recursos y cambiar la configuración en el cuadro de diálogo [!UICONTROL Ver configuración] mediante teclas de teclado (NPR-33420).

* La ventana emergente del cuadro de lista del cuadro combinado (en varios campos de diferentes páginas) ahora muestra las entradas como una lista de opciones que pueden anunciar los lectores de pantalla (NPR-33516).

* Los lectores de pantalla ahora anuncian la funcionalidad de ordenación de los encabezados que se pueden ordenar (en la vista de lista, [!UICONTROL Línea de tiempo] y la página [!UICONTROL Administrar publicación]) y se puede acceder a los controles de clasificación de los encabezados de columna mediante el teclado (NPR-32979).

* Los elementos en los que se puede hacer clic, como tarjetas de comentarios, actualizaciones de versiones, cuadros combinados e iconos de cheurón de los menús, ahora se pueden centrar e interactuar con ellos mediante un teclado (NPR-33514).

* Los lectores de pantalla ahora anuncian correctamente la funcionalidad (o el propósito de la acción) de los iconos de perspectivas (para uso, impresiones y clics) en [!UICONTROL Vista de perspectivas] (NPR-33513).

* Los campos de formulario de solo lectura (por ejemplo, campos desactivados en [!UICONTROL pestaña Básico] del recurso [!UICONTROL Propiedades]) ahora se pueden enfocar mediante el teclado (NPR-33493, CQ-4273031).

* Las etiquetas de varios campos de entrada ahora son etiquetas permanentes (por lo tanto accesibles) y no solo etiquetas de marcador de posición, que desaparecieron cuando se introdujo texto (NPR-33475).

* Los distintos niveles de encabezado (como títulos de páginas y encabezados de sección) ahora se perciben como encabezados con diferentes niveles para los usuarios de lectores de pantalla (NPR-33471).

* Ahora se puede acceder a los elementos interactivos de la interfaz de usuario, como los vínculos y las opciones (en las opciones de encabezado y zoom de la página de recursos, la navegación por carpetas) mediante un teclado (NPR-33468, CQ-4271412).

* Los indicadores de progreso [!UICONTROL Options], [!UICONTROL Scope] y [!UICONTROL Workflows] de la página [!UICONTROL Administrar publicación] ahora los lectores de pantalla leen correctamente como indicadores de progreso, en lugar de pestañas (NPR-33416).

* El color de los iconos de clasificación por estrellas (como en la sección [!UICONTROL Clasificación] de la pestaña [!UICONTROL Avanzadas] del recurso [!UICONTROL Propiedades] o en la vista de tarjeta) cambia para que el contraste adecuado sea visible para los usuarios con visión limitada y sin percepción del color (NPR-33414).

* Ahora se puede acceder a la flecha hacia arriba situada junto al campo [!UICONTROL Comentario] de la página de detalles de recursos mediante las teclas de teclado (NPR-33397).

* Los lectores de pantalla ahora anuncian correctamente los estados expandidos y colapsados del cuadro de diálogo [!UICONTROL Etiquetas] del recurso [!UICONTROL Propiedades] y la navegación del carril izquierdo (en la interfaz de usuario de recursos) (NPR-33396).

* Los títulos de todas las páginas exploradas en [!DNL Adobe Experience Manager] Assets ahora son únicos (NPR-33343).

* Al navegar por la estructura de árbol, los lectores de pantalla ahora anuncian correctamente varios elementos del control de vista de árbol (NPR-33304).

* Ahora se puede acceder a las distintas versiones de recursos de la vista [!UICONTROL Línea de tiempo] en la página de detalles de recursos mediante las teclas de teclado (NPR-33283).

* Los nombres de las sugerencias de búsqueda que aparecen en el cuadro combinado Omnisearch ahora los anuncian los lectores de pantalla al utilizar la funcionalidad de búsqueda (NPR-33280).

* Los lectores de pantalla ahora anuncian los elementos en los que se puede hacer clic y [!UICONTROL Ir al enlace] en [!UICONTROL Barra de referencias] como elementos en los que se puede hacer clic (NPR-33278).

* Los lectores de pantalla ya no anuncian la información de estructura de la tabla (como la fila 1, celda 1, tabla) del cuadro de diálogo [!UICONTROL Compartir vínculo] cuando se abre el cuadro de diálogo (NPR-33268).

* Los lectores de pantalla ahora anuncian correctamente el propósito de varios elementos de cuadro combinado (como el campo Ruta y la opción para abrir el cuadro de diálogo Selección en la pestaña Básico de las Propiedades del recurso) (NPR-33235).

* La información de que las filas de la tabla de vista de lista están seleccionables ahora se comunica a los usuarios del lector de pantalla cuando el foco del teclado está en ellas. Cuando un puntero se sitúa sobre las filas, los lectores de pantalla anuncian la información (NPR-33234).

* Ahora los lectores de pantalla pueden acceder a las opciones (que tienen [!UICONTROL x]) para eliminar cada una de las etiquetas seleccionadas debajo del campo [!UICONTROL Etiquetas] de la pestaña [!UICONTROL Básico] de [!UICONTROL Propiedades] (NPR-33206).

* El selector de fechas del calendario ahora se puede enfocar y activar mediante el teclado por parte de los usuarios de lectores de pantalla y usuarios de teclado con visión (NPR-33200).

* El conmutador para cambiar entre la vista de lista y la vista de tarjeta ahora expone correctamente su funcionalidad (de ajustar vistas) al lector de pantalla (NPR-33069).

* Ahora se puede acceder al menú en el carril izquierdo. Los lectores de pantalla anuncian adecuadamente la funcionalidad y el propósito de expandir el menú (NPR-33068).

* Los usuarios de lectores de pantalla ahora pueden acceder al cuadro de lista y a muchos otros elementos de la interfaz de usuario sin visión y los lectores de pantalla anuncian la siguiente información al respecto (NPR-33040):

   * si se requiere la introducción de datos por parte del usuario en un elemento antes del envío del formulario.
   * si un elemento no es editable.
   * si un widget está seleccionado o no.

* Ahora se puede acceder a la opción para abrir la barra lateral de filtro mediante el teclado (NPR-32842, CQ-4273018).

* Ahora se puede acceder al control de casilla de verificación en el encabezado de columna de la vista de lista y los lectores de pantalla anuncian el propósito del uso del control (NPR-32722, NPR-33005).

* Las etiquetas de los campos horas (HH) y minutos (mm) del selector de fechas del calendario ahora son etiquetas permanentes en lugar de etiquetas de marcador de posición, y no desaparecen cuando el usuario introduce texto en estos campos (NPR-32720).

* El texto de los vínculos de las notificaciones (que aparecen después de hacer clic en el icono de la campana) ahora se anuncia a los usuarios de lectores de pantalla, que utilizan la pestaña para acceder a cada vínculo (NPR-32645).

* [!UICONTROL Seleccione],  [!UICONTROL Descargar],  [!UICONTROL Propiedades] y  [!UICONTROL Más ] acciones. Ahora se puede acceder mediante el teclado a las opciones de tarjetas de recursos en  [!UICONTROL Vista de ] perspectivas (NPR-32609).

* Los lectores de pantalla ya no anuncian el contenido oculto visualmente (como el contenido de la barra de menús del encabezado en los resultados de búsqueda) cuando se accede mediante el teclado (NPR-32606).

* El propósito de las etiquetas en los controles para pasar a los meses siguiente y anterior en el selector de fechas del calendario ahora lo anuncian los lectores de pantalla (NPR-32604).

* Los iconos de clasificación por estrellas ahora se pueden enfocar y activar con las teclas de teclado (NPR-32513).

* Ahora se puede acceder a la funcionalidad para controlar el volumen de vídeo a través de la pestaña (para centrarse en el control deslizante del volumen) y las teclas de flecha (para ajustar el volumen) del teclado (NPR-32065).

* El propósito de los campos de entrada de límite inferior ([!UICONTROL From]) y límite superior ([!UICONTROL To]) del filtro Tamaño de archivo ahora se anuncia para los usuarios de lectores de pantalla que no tengan visión (NPR-32064).

* El menú [!UICONTROL Idiomas] del formulario [!UICONTROL Crear y traducir] ahora es accesible para los lectores de pantalla en modo Examinar (CQ-4293906).

* Ahora se puede acceder al panel [!UICONTROL Referencias] con las siguientes mejoras (NPR-33261, CQ-4293798):

   * En el modo Examinar, el foco del lector de pantalla ya no se mueve a los campos de edición multilínea ocultos en las secciones [!UICONTROL Referencias del sitio], [!UICONTROL Referencias de recursos], [!UICONTROL Textos] y [!UICONTROL Referencias de formulario].

   * Los lectores de pantalla ahora anuncian la función de los elementos [!UICONTROL Referencias del sitio] y [!UICONTROL Textos en idiomas].

   * El enfoque de los lectores de pantalla en el modo Examinar cambia en una secuencia significativa a varios elementos.

* [!UICONTROL Ahora se puede acceder a la página ] Editor de esquemas de metadatos y a sus elementos mediante el teclado y es fácil leerlos en la pantalla (CQ-4290962, CQ-4272953).

* El propósito del símbolo `X` para eliminar las etiquetas seleccionadas lo anuncian ahora los lectores de pantalla junto con el número de etiquetas seleccionadas (CQ-4273017).

* Para evitar confusiones para usuarios sin visión que utilizan lectores de pantalla, los iconos decorativos y las imágenes ahora son ignorados por los lectores de pantalla (CQ-4272944).

**Problemas corregidos en Recursos de Experience Manager**

[!DNL Adobe Experience Manager] 6.5.5.0 Assets proporciona correcciones a los siguientes problemas:

*  La opción de inicio en el cuadro de diálogo  [!UICONTROL Crear ] flujo de trabajo para los recursos de una colección está desactivada, lo que impide que se active el flujo de trabajo (NPR-32471).

* Cuando se utiliza la ventana emergente en cascada en los esquemas de metadatos, al seleccionar y guardar una opción desplegable que contiene un apóstrofo (desde la lista desplegable secundaria), la opción de apóstrofo seleccionada desaparece después de volver a abrir el recurso [!UICONTROL Propiedades] (NPR-32649).

* [!UICONTROL Asset Insights Sincroniza ] Jobstops y falla si encuentra entradas no válidas (en el lado de Analytics) en lugar de pasar a la siguiente entrada (NPR-32674).

* Gyroscope no funciona porque los sensores de movimiento están desactivados de forma predeterminada en los navegadores móviles en el visor panorámico (CQ-4272937).

* [!UICONTROL El asistente de ] configuración de recursos conectados no funciona con el error 404 al instalar 6.5.3 en 6.5.1 (NPR-32730).

* Durante el proceso de escritura de XMP, todas las propiedades de metadatos de espacio de nombres personalizadas cambian el prefijo de espacio de nombres personalizado a ns2 en lugar del prefijo de espacio de nombres configurado (NPR-32748).

* La carga diferida no se activa y solo se muestran 100 activos al seleccionar para revisar las tareas de la bandeja de entrada de notificaciones (NPR-32750).

* `NullPointerException` se observa debido a la falta de preferencias de nodo en el perfil de usuario recién creado (SAML/SSO). Este error evita que los usuarios que inician sesión recientemente utilicen la integración [!DNL Adobe Experience Manager Stock] (NPR-32777).

* Las advertencias transversales se observan en los registros al abrir una colección inteligente que contiene más de 10 000 activos (NPR-32980).

* Los nombres de los recursos se cambian a minúsculas al mover recursos de una carpeta a otra en [!DNL Adobe Experience Manager] en modo de ejecución de Dynamic Media Scene7 (NPR-32995).

* Los recursos en los que se ha buscado no se pueden eliminar después de navegar a sus propiedades desde los resultados de búsqueda y volver a los resultados de búsqueda para eliminarlos (NPR-32998).

*  La siguiente opción permanece deshabilitada al seleccionar la carpeta de destino en la interfaz  [!UICONTROL Mover ] recursos (NPR-33356).

*  Nextoption no está habilitado al seleccionar el nodo principal (donde la carpeta secundaria única es visible) y luego seleccionar la carpeta secundaria (NPR-33275).

* Los permisos de desprotección y desprotección están deshabilitados en Adobe Asset Link (AAL) para usuarios con permiso de eliminación, aunque se hayan concedido otros permisos, como leer, crear o modificar (NPR-33272).

* Las representaciones de recorte inteligente no están disponibles en el cuadro de diálogo de descarga de recursos (NPR-33167).

* Se observa una excepción en los registros al abrir el carril de representaciones para un PDF en una carpeta con perfil de recorte inteligente (CQ-4294201).

* Los ajustes preestablecidos de imagen no se publican si [!UICONTROL Dynamic Media sync mode] está desactivado de forma predeterminada en el Experience Manager con Dynamic Media Scene7 runmode (CQ-4294200).

* El procesamiento de recursos mientras la carga masiva se atasca y la instancia de flujo de trabajo muestra instancias atascadas del recurso de actualización DAM (CQ-4293916).

* La creación de una configuración de Dynamic Media en Experience Manager funciona, pero en la interfaz de usuario no sucede nada al seleccionar Guardar (CQ-4292442).

* La vista previa de los recursos de vídeo F4V no funciona en la reproducción progresiva en Safari/Mac (CQ-4289844).

* La carpeta adicional se crea al recortar de forma inteligente un recurso que se encuentra dentro de una carpeta principal con el carácter de punto `.` en su nombre (CQ-4289337).

* La miniatura no funciona y el banner de procesamiento de vídeo no se muestra cuando se copia un vídeo (CQ-4284125).

* El visor dimensional muestra incorrectamente miniaturas vacías en Firefox para algunos modelos con vistas de cámara vacías (CQ-4283447).

* Los problemas de rendimiento corregidos en 6.5.5.0 son (CQ-4279206):

   * Se tarda demasiado en cargar binarios grandes en los servidores de procesamiento de imágenes de Dynamic Media.

   * El tiempo de generación de miniaturas en el Experience Manager aumenta debido a la arquitectura de Dynamic Media Scene7.

* Los problemas de migración de Dynamic Media Scene7 fallan para clientes con un gran número de activos (CQ-4279206).

* El diseño del visor de vídeo 360 se rompe si se utiliza `setVideo` y el vídeo se desplaza hacia abajo al utilizar `video= modifier` (CQ-4263201).

* Aparece un mensaje de error al instalar el paquete SDL Experience Manager (NPR-33175).

* Vulnerabilidad del SSRF en el Experience Manager (NPR-33435).

### Plataforma {#platform-6550}

* No se llama al filtro [!DNL Sling] si la entrada de mapa `sling:match` se crea en `/etc/maps` (NPR-33362).
* El Experience Manager se bloquea debido a un error de segmentación con [!DNL Apache Lucene] (NPR-32988).
* [!DNL Jackson] falta el paquete principal del archivo uberjar de Experience Manager (NPR-32848).
* El CRXDE Lite no carga contenido para usuarios sin permiso de lectura en la propiedad `jcr:primaryType` de un nodo (NPR-32611).
* [!DNL Granite] el programador de tareas de mantenimiento se reinicia con demasiada frecuencia durante las implementaciones de Experience Manager (CQ-4294627).
* Cuando una consulta SQL se ejecuta durante mucho tiempo, por ejemplo 7 horas, el Experience Manager deja de responder (NPR-33044).

### Interfaz de usuario {#ui-6550}

* La selección de botones de opción no persiste en un campo múltiple (NPR-33309).
* El límite de carga diferida no funciona para la vista de lista (NPR-33124).
* La página de resultados de Omnisearch no muestra un mensaje si no hay coincidencias (NPR-32974).
* El filtro Omnisearch devuelve todas las coincidencias en el nodo `/content` ignorando la ubicación seleccionada (NPR-32849).

### Integraciones {#integrations-6550}

* La caché interna se borra al publicar una página con un componente Adobe Target (NPR-33162).
* La integración con Adobe Target no funciona en [!DNL Windows Internet Explorer] 11 (NPR-33111).
* Al configurar Adobe Target, los campos [!UICONTROL Empresa] y [!UICONTROL Grupo de informes] no aparecen al seleccionar una fuente de informes (NPR-32502).
* Al exportar [!DNL Experience Fragments] mediante [!DNL Adobe I/O], los metadatos como el producto de origen no se exportan a Adobe Target (NPR-32159).
* Los usuarios de IMS autorizados en el grupo de administración de Experience Manager locales no pueden crear ni modificar las configuraciones de IMS (NPR-33045).
* La página de configuraciones de Adobe Launch no muestra todos los registros (NPR-33011).
* Los usuarios del grupo de autores de contenido no pueden editar las propiedades de un componente de Adobe Target debido a un error de JavaScript (NPR-32996).
* Ejecución de scripts en sitios múltiples para JSON (NPR-32744).

### Proyectos de traducción {#translation-6550}

* Las etiquetas traducidas no se importan en el Experience Manager desde servicios de traducción de terceros (NPR-33154).
* La página de configuración de traducción muestra un proveedor de traducción incorrecto al que se utilizó para la traducción (NPR-32971).
* Al agregar una carpeta de fragmentos de experiencia a un proyecto de traducción existente, se crea un nuevo proyecto (NPR-32843).
* Se ve un error `NullPointerException` en los registros de ejecución de un trabajo de traducción (NPR-32628).

### WCM {#wcm-6550}

* Editor de páginas: el [!DNL Sites] Editor de páginas no permite que los usuarios que utilizan solo el teclado omitan el contenido principal en lugar de cambiar el enfoque de la pestaña a través de todas las opciones disponibles en el encabezado (CQ-4293883).
* Editor de páginas: los paneles que utilizan el componente Bueno e incluyen datos guardados no se muestran debido a las actualizaciones en las versiones [!DNL Chrome] y [!DNL Firefox] (CQ-4292995).
* MSM: al eliminar un componente de la página, este no se elimina de la versión publicada de la página (CQ-4292360).

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* Si se elimina un esquema de metadatos publicado de [!DNL Brand Portal], se produce un error (CQ-4292063).
* Si un administrador configura [!DNL Experience Manager Assets] 6.5.4 con Brand Portal a través de la consola de desarrollador de Adobe, el usuario [!DNL Brand Portal] no puede publicar un recurso de la carpeta de contribución de [!DNL Brand Portal] a [!DNL Experience Manager] (NPR-33046).
* Duplique la replicación de las carpetas principales que causan conflictos (NPR-33001).

### [!DNL Communities] {#communities-6550}

* No se puede eliminar una tarjeta en la consola de moderación mediante la opción de menú de edición rápida (NPR-33117).
* Se produce un error al acceder a la página [!UICONTROL Flujo de actividad] (NPR-33146).
* Los grupos eliminados en la instancia de autor no se eliminan de todas las instancias de publicación (NPR-33199).
* Los autores, después de crear un nuevo grupo, no se redirigen a la sección [!UICONTROL Grupo de la comunidad] de [!DNL Internet Explorer] 11 (NPR-33205).
* El acceso a un mensaje en la bandeja de entrada del Experience Manager no cambia el estado del mensaje a Leído (NPR-32764).
* Editar un grupo [!DNL Communities] y cambiar la imagen en miniatura no actualiza la imagen en miniatura del grupo (NPR-32599).
* Un usuario no puede enviar un correo electrónico a otro usuario de una comunidad (NPR-32598).
* Un blog enviado no se muestra hasta que el usuario actualiza la página (NPR-32391).
* Al crear una versión de notificaciones y suscripciones de Contenido generado por el usuario (UGC), se almacena un ID incorrecto de la página de origen (CQ-4279355, CQ-4289703).
* Problema de scripts en sitios múltiples (NPR-33203).

### Flujo de trabajo {#workflow-6550}

* La opción [!UICONTROL Línea de tiempo] en el carril izquierdo tarda más tiempo en cargarse de lo esperado (NPR-32851).
* Después de reiniciar una instancia de Experience Manager, el correo electrónico para la tarea de revisión de una colección incluye un vínculo de carga útil incorrecto (NPR-32774).

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>Experience Manager Service Pack no incluye correcciones para [!DNL Forms]. Estas se entregan mediante un paquete independiente de complementos de Forms. Asimismo, se ha publicado un instalador acumulativo que incluye correcciones para AEM Forms en JEE. Para obtener más información, consulte [Instalación del complemento Forms del Experience Manager](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) y [Instalación de Forms del Experience Manager en JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

* Gestión de correspondencia: El orden de los recursos en una zona de destino se ajusta después de enviar una carta (NPR-33359, NPR-33153).
* Forms adaptable: Cuando un usuario edita un formulario adaptable, la opción [!UICONTROL Iniciar flujo de trabajo] disponible en el menú [!UICONTROL Información de página] no funciona (NPR-33004).
* Forms adaptable: El usuario no puede guardar un formulario adaptable con más de un archivo adjunto (NPR-32997).
* Forms adaptable: Cambiar el diseño del panel en un formulario adaptable provoca un error (CQ-4293880).
* Forms adaptable: Una nueva línea a una cadena en un diccionario de formularios adaptables añade `&#xa;` caracteres al diccionario (NPR-33266).
* Accesibilidad de Forms adaptable: Cuando un usuario obtiene una vista previa de un formulario adaptable como un formulario HTML, el campo [!UICONTROL Scribble Signature] no puede conservar el enfoque de la pestaña (NPR-33159).
* Accesibilidad de Forms adaptable: Los mensajes de error que se muestran al enviar un formulario adaptable no se vinculan a un atributo `aria-describedBy` (NPR-33071).
* Accesibilidad de Forms adaptable: Los campos marcados como obligatorios en un formulario adaptable no tienen el atributo obligatorio establecido en True en el esquema de accesibilidad de ARIA (NPR-33070).
* Servicio PDFG: Cuando un usuario convierte un archivo de texto a un PDF, los caracteres japoneses no se representan correctamente (NPR-33238).
* Servicio PDFG: La operación `CreatePDF` no puede convertir un archivo PDF al formato PDF OCR (NPR-32994).
* Servicio PDFG: La conversión a PDF falla en la 200ª instancia de un documento [!DNL OpenOffice] (NPR-32766).
* Integración de back-end: Las solicitudes del modelo de datos de formulario fallan porque el token de actualización caduca debido a un estado inactivo incorrecto (NPR-33169).
* Designer: Los lectores de pantalla ejecutan el orden de tabulación en función del orden geográfico predeterminado en lugar del orden de tabulación personalizado definido en el archivo XDP (NPR-32160).
* Designer: Si la opción de etiquetado está activada, el borde del subformulario desaparece en la salida PDF generada (NPR-32778).
* XSS almacenado con GuideSOMProviderServlet (NPR-32700).

## Adobe Experience Manager 6.5.4.0 {#experience-manager-6540}

Adobe Experience Manager 6.5.4.0 es una actualización importante que incluye nuevas funciones, mejoras clave solicitadas por los clientes y rendimiento, estabilidad y mejoras de seguridad, publicada desde la publicación general de la versión 6.5 en **Abril de 2019**. Se puede instalar sobre Adobe Experience Manager 6.5.

Algunas de las funciones y mejoras clave introducidas en Adobe Experience Manager 6.5.4.0 son:

* Adobe Experience Manager Assets ahora se configura con Brand Portal a través de la consola [!DNL Adobe I/O].

* Ya está disponible un nuevo paso [Generate printable Output](../forms/using/aem-forms-workflow-step-reference.md) para los flujos de trabajo de Adobe Experience Manager Forms.

* [Compatibilidad con varias columnas ](../forms/using/resize-using-layout-mode.md) para el modo de diseño de formularios adaptables y comunicaciones interactivas.

* Compatibilidad con [Texto enriquecido](../forms/using/designing-form-template.md) en formularios HTML5.

* [Mejoras de ](new-features-latest-service-pack.md#accessibility-enhancements) accesibilidad en Recursos Experience Manager.

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.10.8.

* Ahora puede sincronizar subárboles de contenido selectivo con *Dynamic Media - modo Scene7* en lugar de con todos los disponibles en `content/dam`.

* La integración del modelo de datos de formulario con el servicio web SOAP ahora admite grupos de opciones o atributos en elementos.

* Ahora, las estructuras de entrada o salida SOAP y de datos complejos admiten la sustitución dinámica de grupos.

Para obtener una lista completa de las funciones y los aspectos destacados introducidos en los Service Packs más recientes, consulte [Novedades de los Service Packs de Adobe Experience Manager 6.5](new-features-latest-service-pack.md).

### Sites {#sites-fixes}

* Cuando una dirección URL de una página de Adobe Experience Manager Sites contiene dos puntos (`:`) o un símbolo de porcentaje (`%`), el explorador deja de responder y los picos de uso de CPU (NPR-32369, NPR-31918).

* Cuando se abre una página Sitios Experience Manager para editarla y se copia un componente, la acción de pegado permanece no disponible para algunos marcadores de posición (NPR-32317).

* Cuando se abre el asistente Administrar publicación, un fragmento de experiencia vinculado a un componente principal no se muestra en las listas de referencias publicadas (NPR-32233).

* La descripción general de la Live Copy en la interfaz de usuario táctil tarda mucho más que la IU clásica en procesarse (NPR-32149).

* Cuando la hora del servidor y la hora del equipo se encuentran en diferentes zonas horarias, la hora de publicación programada muestra la hora del servidor en la interfaz de usuario táctil, mientras que en la IU clásica se muestra la hora del equipo (NPR-32077).

* Experience Manager Sites no puede abrir una página con un sufijo en la dirección URL (NPR-32072).

* Cuando un usuario edita un fragmento de contenido, se restaura una variación eliminada del fragmento de contenido (NPR-32062).

* Los usuarios pueden guardar un fragmento de contenido sin proporcionar información en los campos obligatorios (NPR-31988).

* kernel.js y ui.js no se cumplieron previamente ni se almacenaron en caché. Produce un tiempo adicional en el procesamiento de páginas (NPR-31891).

* Cuando PageEventAuditListener está habilitado, la longitud de la cola de confirmación aumenta. Afecta al rendimiento de muchas operaciones, como la publicación masiva, la navegación y el movimiento masivo de recursos (NPR-31890).

* Cuando se arrastran fragmentos de experiencias, se observa un tiempo de respuesta alto (NPR-31878).

* Cuando selecciona la opción Arrastrar componente aquí en el marcador de posición de una cuadrícula adaptable, se envía una solicitud de GET y la solicitud da como resultado un error HTTP 403 (NPR-31845).

* Al mover el contenido dentro de la misma carpeta, la opción de mover la página está desactivada (NPR-31840).

* En el modo de estructura de plantillas editables, la lista de componentes permitidos del contenedor de diseño muestra resultados incorrectos. En el contenedor de diseño solo se muestran los componentes con cuadro de diálogo de diseño (NPR-31816).

* Cuando una página tiene permisos de solo lectura para un usuario, la opción Abrir propiedades se puede ver en sites.html pero no en editor.html (NPR-31770).

* Cuando un usuario hace clic en el botón Crear , la opción de página no está disponible (NPR-31756).

* No se puede sincronizar la campaña en la campaña de Adobe que contenga el componente de importador de diseños OOTB (predeterminado) (NPR-31728).

* Cuando intenta cambiar una lista de viñetas a una lista numerada, solo se cambian los dos primeros elementos de la lista (NPR-31636).

* Cuando se anula la creación de una página y se selecciona el nodo secundario, el cuadro de diálogo de selección sigue mostrando el nodo inicial. Cuando la página se crea y el usuario hace clic en Examinar, la página se redirige al nodo raíz en lugar del nodo creado (NPR-31618).

* El cuadro de diálogo de configuración de vista no funciona correctamente para la función de flujo de trabajo de personalización de la bandeja de entrada (NPR-32503 y NPR-32492).

* Aparece un mensaje de error al ver la información del flujo de trabajo mediante la bandeja de entrada (CQ-4282168).

### Assets {#assets-6540-enhancements}

* El botón para el flujo de trabajo de déclencheur en la página de recopilación de recursos está desactivado (NPR-32471).

* Se crea una carpeta sin nombre en SPS (Scene7 Publishing System) mientras se mueve un recurso de una carpeta a otra en Experience Manager con la configuración de Dynamic Media Scene7 (NPR-32440).

* La acción para mover todos los recursos (mediante Seleccionar todo y, a continuación, mover) a una carpeta que contenga recursos publicados falla con error (NPR-32366).

* Error en la generación de representación de recursos con ${extension} (NPR-32294).

* Las direcciones URL del historial de versiones se muestran en el campo Referencias por de la página de propiedades de los recursos (NPR-31889).

* El archivo ZIP descargado de DAM no se puede abrir con WinZip (NPR-32293).

* Los permisos originales de una carpeta se actualizan cuando se abre la Configuración de carpeta para cambiar el título de la carpeta o la imagen en miniatura y después se guardan (NPR-32292).

* El icono de calendario para la activación programada no se muestra en la columna Estado (en la IU clásica de la lista de recursos DAM) para los recursos cuya activación está programada para una fecha y hora posteriores (NPR-32291).

* La creación de fragmentos de código mediante plantillas de fragmento genera un error al buscar colecciones durante el proceso de creación de fragmentos (NPR-32290).

* Se activan varias consultas de búsqueda cuando se seleccionan varias etiquetas del filtro de búsqueda (NPR-32143).

* La interfaz de usuario de Recursos de Experience Manager muestra nombres de archivo truncados cuando se cargan recursos con más de 50 caracteres en el nombre de archivo (NPR-32054).

* Todas las casillas de verificación del panel Filtro se desactivan cuando se desactivan la primera y la segunda casillas de verificación, cuando se seleccionaron las casillas de verificación del nivel dos del árbol de casillas de verificación de Adobe Stock (NPR-31919).

* La búsqueda de archivos y carpetas mediante las facetas Omnisearch proporciona una excepción (NPR-31872).

* El resaltado de campos para la selección de campos obligatoria en el editor de metadatos no se elimina incluso después de seleccionar el campo requerido, cuando las reglas de dependencia se establecen en el formulario de esquema de metadatos correspondiente (NPR-31834).

* Los nombres completos de las etiquetas de nivel de hoja (de la jerarquía de etiquetas) no se muestran en la página Propiedades del recurso (NPR-31820).

* El uso del comando posterior de la página Propiedades del recurso en el navegador Safari da error (NPR-31753).

* La página de resultados de la búsqueda en la interfaz de usuario táctil (realizada a través de Omnisearch) se desplaza automáticamente hacia arriba y pierde la posición de desplazamiento del usuario (NPR-31307).

* La página de detalles de recursos de PDF no muestra botones de acción, excepto los botones Recopilación y Añadir representación en el Experience Manager que se ejecuta en el modo de ejecución de Dynamic Media Scene7 (CQ-4286705).

* Los recursos tardan demasiado en procesarse a través del proceso de carga por lotes de Scene7 (CQ-4286445).

* El botón Guardar no importa el conjunto remoto cuando el usuario no ha realizado ningún cambio en el Editor de conjuntos en el cliente de Dynamic Media (CQ-4285690).

* La miniatura de un recurso 3D no es informativa, cuando se incorpora un modelo 3D compatible en un Experience Manager (CQ-4283701).

* El estado sin procesar del ajuste preestablecido del visualizador de vídeo de recorte inteligente aparece dos veces en el texto del banner junto con el nombre del ajuste preestablecido (CQ-4283517).

* La altura incorrecta del contenedor de un modelo 3D cargado con una vista previa en el visor 3D se observa en la página de detalles del recurso (CQ-4283309).

* El Editor de carrusel no se abre en IE 11 en modo híbrido Dynamic Media Experience Manager (CQ-4255590).

* El foco del teclado se atasca en la lista desplegable Correo electrónico del cuadro de diálogo Descargar, en los navegadores Chrome y Safari (NPR-32067).

* La casilla de verificación Sincronizar todo el contenido no está habilitada de forma predeterminada al intentar agregar la configuración de nube de DM en el Experience Manager (CQ-4288533).

### Interfaz de usuario de base {#foundation-ui-6540}

* El control del ratón cambia al campo de filtro anterior en lugar de permanecer en el campo de filtro existente al buscar recursos mediante el panel Filtro (NPR-32538).

* Etiquetado de plataforma: Para buscar etiquetas, escriba en los campos de etiqueta , se muestran las etiquetas que están fuera de los límites raíz y no respeta la propiedad `rootPath` de los campos de etiqueta (NPR-31895).

* Interfaz de usuario de plataforma: El explorador de rutas se rompe si se agrega una ruta no válida en el campo de texto (NPR-31884).

* La notificación se oculta detrás de un menú adhesivo en la selección de páginas (NPR-31628).

### Plataforma {#platform-sling-6540}

* (HTL) Los guiones bajos sustituyen los dos puntos en la sección de ruta de la URL (NPR-32231).

### Proyectos {#projects-6540}

* El botón Crear no es visible para el usuario aunque este tenga permiso para crear un proyecto en la subcarpeta (NPR-31832).

### Traducción de proyectos {#projects-translation-6540}

* La creación del proyecto de traducción interrumpe la interfaz de usuario cuando la opción Recortar espacios está activada en `Apache Sling JSP Script Handler` (NPR-32154).

* Se observa un error en la interfaz de usuario y una excepción de punto nulo en los registros de errores cuando cualquier etiqueta, que se deba traducir, se agrega a un proyecto de traducción (NPR-31896).

### Integraciones {#integrations-6540}

* La generación de URL de la biblioteca de Launch se basa únicamente en los valores `path` y `library_name` de la API de Launch y no en el valor `library_path` (NPR-31550).

* Aparece un mensaje de error al procesar elementos relacionados con LiveFile (FYR-12420).

* ReportSuitesServlet es vulnerable a SSRF (NPR-32156).

### Editor de plantillas WCM {#wcm-template-editor-6540}

* En el modo de estructura de plantillas editables, la lista de componentes permitidos en el contenedor de diseño no muestra el componente de botón de vínculo (CQ-4282099).

### Editor de páginas WCM {#wcm-page-editor-6540}

* Se observa un error al seleccionar una superposición y, a continuación, seleccionar una cuadrícula interactiva Arrastre los componentes aquí (CQ-4283342).

### Segmentación de campañas {#campaign-targeting-6540}

* La configuración de la nube de Target falla con el error obtener solicitud de mboxes fallida (CQ-4279880).

### Brand Portal {#assets-brand-portal-6540}

* Los usuarios de Brand Portal no pueden publicar recursos de carpetas de contribución en [!DNL Assets] al actualizar a [!DNL Adobe I/O] en el Experience Manager 6.5.4 (CQDOC-15655). Para una corrección inmediata en el Experience Manager 6.5.4, se recomienda [descargar la corrección](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) e instalarla en la instancia de autor.

* Los valores emergentes del esquema de metadatos no son visibles en las propiedades del recurso (CQ-4283287).

* El subesquema de metadatos no muestra pestañas basadas en mimetype en propiedades de recursos (CQ-4283288).

* El esquema de cancelación de publicación de metadatos rellena un mensaje de error aunque el esquema se elimine en el servidor.

* La imagen de vista previa no se muestra para un recurso publicado (CQ-4285886).

* El usuario no puede publicar ni cancelar la publicación de recursos que contengan comillas simples en el nombre (CQ-4272686).

* Los términos y condiciones no se muestran al descargar varios recursos (CQ-4281224).

* Se han corregido vulnerabilidades de seguridad menores.

### Communities {#communities-6540}

* El formulario Crear miembro se muestra como una página en blanco (NPR-31997).

* El usuario no puede ver el informe de Analytics sobre la instancia de autor (NPR-30913).

### Oak: Indexación y Consultas {#oak-indexing-6540}

* Los documentos de Microsoft Word y MS Excel, que contienen imagen JPEG, cuando se analizan con el analizador de Tika no se analizan y se observa un error de clase no encontrada (NPR-31952).

### Forms {#forms-6540}

>[!NOTE]
>
>Experience Manager Service Pack no incluye correcciones para Experience Manager Forms. Estas se entregan mediante un paquete independiente de complementos de Forms. Además, se ha publicado un instalador acumulativo que incluye correcciones para Adobe Experience Manager Forms en JEE. Para obtener más información, consulte [Instalación del complemento Forms del Experience Manager](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) y [Instalación de Forms del Experience Manager en JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

* Gestión de correspondencia: Las letras muestran caracteres adicionales después del envío a los flujos de trabajo del proceso posterior (NPR-32626).

* Gestión de correspondencia: Las letras muestran un marcador de posición desplegable como un componente de texto después del envío a los flujos de trabajo posteriores al proceso (NPR-32539).

* Gestión de correspondencia: Los valores predeterminados definidos en la plantilla de letras no se muestran en el modo de vista previa (NPR-32511).

* Forms móvil: El botón de envío se muestra con un tamaño expandido mientras se procesa un formulario XDP en una versión HTML (NPR-32514).

* Servicios de documentos: Problemas de acceso a URL para cartas y otras páginas después de aplicar el Service Pack 2 (NPR-32508, NPR-32509).

* Servicios de documentos: Si el número de transacciones en un servidor supera un límite específico, la conversión de HTML a PDF falla y la configuración del tipo de archivo se elimina del servidor [!DNL Forms] (NPR-32204).

* Forms adaptable: La herramienta de accesibilidad del explorador informa de errores en formularios adaptables según las directrices de nivel AA de WCAG2 (NPR-32312, NPR-32309, CQ-4285439).

* Forms adaptable: La herramienta de accesibilidad del explorador Chrome informa de un error de práctica recomendada (NPR-32310).

* Forms adaptable: Problemas de traducción al configurar un formulario adaptable incrustado en una página de Sites de Experience Manager (NPR-32168).

* Workbench: Aparece un mensaje de error al utilizar la operación Obtener propiedades de PDF para el servicio Utilidades de PDF (NPR-32150).

* Seguridad de documentos: Un archivo PDF protegido no se puede abrir sin conexión con la opción DisableGlobalOfflineSynchronizationData establecida en True (NPR-32078).

* Designer: Si la opción de etiquetado está activada, el borde del subformulario desaparece en la salida PDF generada (NPR-32547, NPR-31983, NPR-31950).

* Designer: Si hay celdas combinadas en una tabla, la prueba de accesibilidad falla para el archivo PDF de salida convertido desde un formulario XDP utilizando el servicio de salida (CQ-4285372).

* Base JEE: Si un servidor Forms de Experience Manager está desconectado de un clúster, los problemas de almacenamiento en caché le impiden volver a conectarse al servidor (NPR-32412).

## Adobe Experience Manager 6.5.3.0 {#experience-manager-6530}

[!DNL Adobe Experience Manager] 6.5.3.0 es una versión importante que incluye correcciones y mejoras clave para el cliente, de rendimiento, estabilidad y seguridad publicadas tras la publicación general de la versión 6.5 en  **abril de 2019**. Se puede instalar sobre [!DNL Adobe Experience Manager] 6.5.

Algunos aspectos destacados de esta versión de Service Pack son:

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.10.6.

* [!DNL Experience Manager Assets] ahora admite archivos ZIP creados con el algoritmo Deflate64.

* Se ha añadido una nueva columna para la fecha creada, que es ordenable, en la vista de lista DAM y en los resultados de búsqueda de recursos en la vista de lista.

* La ordenación de recursos basada en la columna Nombre se ha habilitado en la vista de lista.

* [!DNL Dynamic Media] ahora admite recursos de vídeo de recorte inteligente. Recorte inteligente es una función impulsada por el aprendizaje automático que recorta de nuevo un vídeo mientras mueve el marco para seguir al punto focal de la escena.

* [!DNL Dynamic Media] admite imágenes inteligentes.

* Capacidad para [establecer las preferencias de fuera de Office](../forms/using/configure-out-of-office-settings.md) en los flujos de trabajo [!DNL Experience Manager].

* Capacidad para [compartir elementos de la bandeja de entrada o la bandeja de entrada](../forms/using/configure-shared-queues-osgi.md) con otros usuarios en los flujos de trabajo [!DNL Experience Manager].

* Capacidad para [generar comunicaciones interactivas en modo por lotes](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

* Se ha actualizado la versión de jQuery incluida en ContextHub a 3.4.1.

### Recursos {#assets-6530-enhancements}

**Mejoras del producto**

* [!DNL Experience Manager Assets] ahora admite archivos ZIP creados con el algoritmo Deflate64 (NPR-27573).

* Se agrega una nueva columna para la fecha creada, que es ordenable, en la vista de lista de DAM y en los resultados de búsqueda de recursos en la vista de lista (NPR-31312).

* En la vista de lista, los usuarios pueden ordenar la lista de recursos utilizando la columna [!UICONTROL Name] (NPR-31299).

* Los archivos GLB, GLTF, OBJ y STL se pueden previsualizar en la página [!UICONTROL Detalles del recurso] de DAM (CQ-4282277).

* `ReplicationOnModifyListener` se activa para nodos de fragmento durante la carga del fragmento en  [!DNL Dynamic Media] (CQ-4281279).

* [!DNL Dynamic Media] ahora admite recursos de vídeo de recorte inteligente. Recorte inteligente es una función impulsada por el aprendizaje automático que vuelve a recortar un vídeo mientras mueve el marco para seguir al punto focal de la escena (CQ-4278995).

* [!DNL Dynamic Media] admite imágenes inteligentes (CQ-422249).

* La vista de búsqueda o exploración se establece como la vista predeterminada en el selector de base si se pasan parámetros de consulta en la solicitud (NPR-31601).

**Correcciones**

* Los metadatos de algunos documentos PDF no se actualizan ni se guardan en el PDF cuando se modifica su título (NPR-31629).

* El uso compartido de recursos no funciona para un recurso que tiene más caracteres (`+`) en el nombre del archivo (NPR-31547).

* Las ediciones en el formulario de búsqueda predeterminado Carril de búsqueda de administración de Assets no funcionan como se espera (NPR-31502).

* Las sugerencias no se muestran al utilizar la vista Omnisearch en recursos para buscar recursos (NPR-31496).

* Las referencias de los recursos dentro de las colecciones no se actualizan cuando los recursos a los que se hace referencia se mueven a otra ubicación, en casos en que una colección diferente hace referencia a los mismos recursos (NPR-31486).

* Las etiquetas IPTC duplicadas se añaden a los metadatos de recursos (NPR-31328).

* El recuento de resultados de búsqueda no se actualiza con precisión cuando se activa una búsqueda desde el carril de filtro (NPR-31316).

* Todas las casillas de verificación se desactivan al anular la selección de las casillas de verificación de segundo nivel en el filtro Tipo de archivo y el texto de la barra de búsqueda no está sincronizado con las propiedades seleccionadas o no seleccionadas (NPR-31287).

* No se pueden quitar todos los miembros (usuarios/grupos) de la sección Miembros de una carpeta; al intentar eliminar todos los usuarios, el usuario que ha iniciado sesión se añade a la lista (NPR-31171).

* Los recursos con el símbolo más (`+`) en el nombre del archivo no se pueden eliminar (NPR-31162).

* El menú desplegable Crear , que se puede ver en el menú superior al seleccionar una carpeta, no muestra &quot;Carpeta&quot; como opción de creación (NPR-30877).

* Selección de carpetas Crear > FileUpload el elemento de acción no está presente cuando se aplican ACL para Denegar `jcr:removeChildNodes` y `jcr:removeNode` en la ruta a un usuario (NPR-30840).

* Los flujos de trabajo de DAM pasan a un estado obsoleto cuando se cargan ciertos activos de mp4, lo que provoca que todos los flujos de trabajo restantes pasen a estar en estado obsoleto (NPR-30662).

* Error de falta de memoria se observa cuando se cargan en DAM archivos PDF grandes (de varios gigabytes) y se procesan sus subrecursos (NPR-30614).

* El movimiento masivo de recursos está fallando y mostrando un mensaje de advertencia (NPR-30610).

* Los nombres de los recursos se cambian a minúsculas al mover recursos de una carpeta a otra en [!DNL Experience Manager] que se ejecutan en el modo [!DNL Dynamic Media]-Scene7 (NPR-31630).

* Se observa un error al editar un conjunto de imágenes remoto, para la imagen que reside en la carpeta con el mismo nombre que el nombre de la empresa de Scene7 (NPR-31340).

* [!DNL Dynamic Media] los recursos que contienen referencias no se publican (NPR-31180).

* Las cargas del modo [!DNL Dynamic Media]7-Scene7 a [!DNL Dynamic Media Classic] tardan demasiado en completarse (NPR-31048).

* La zona interactiva añadida a un recurso de imagen no es visible a través del visualizador interactivo de imágenes en la página de detalles del recurso (NPR-30979).

* Se crean enormes trabajos de sling y vuelve a aparecer el banner de procesamiento cuando las acciones realizadas en los recursos en [!DNL Experience manager Assets] se pasan a Scene7 (NPR-30947).

* El conflicto ocurre al crear una copia de idioma de los recursos y no se cargan en Scene7 (NPR-30932).

* Las representaciones dinámicas descargadas de [!DNL Experience Manager] que se ejecutan en modo [!DNL Dynamic Media]-híbrido están dañadas (son de tipo texto con contenido que no puede encontrar la imagen en lugar del tipo de contenido de imagen) (NPR-30876).

* [!DNL Dynamic Media] El flujo de trabajo de codificación de vídeo no puede generar miniaturas para el vídeo que se migra del modo  [!DNL Dynamic Media Classic] a  [!DNL Dynamic Media]-Scene7 en Adobe Experience Manager (CQ-4282011).

* IpsApiException se observa al migrar recursos de una instancia a otra mediante distintos ID de empresa de Scene7 (CQ-4280548).

* La miniatura de un recurso 3D no es informativa, cuando se incorpora un modelo 3D compatible en [!DNL Experience Manager] (CQ-4283701).

* Los botones de desplazamiento se muestran en el visor si un recurso 3D tiene pocas vistas de cámara (CQ-4283322).

* Altura incorrecta del contenedor de un modelo 3D cargado con una vista previa en DimensionalViewer en la página Detalles del recurso (CQ-4283309).

* Los vídeos no se pueden reproducir con SmartCropVideoViewer en Internet Explorer 11 y Safari (CQ-4281422).

* El uso del botón mover para mover varios recursos, de una carpeta a otra, falla en [!DNL Experience Manager] al ejecutarse en [!DNL Dynamic Media]-Scene7 runmode (CQ-4280384).

* El vídeo distorsionado se ve en los detalles del recurso cuando el tipo MIME es distinto de MP4 (CQ-4279704).

* Los vídeos recién introducidos en carpetas con perfil de vídeo permanecen en estado de procesamiento incluso después de que el porcentaje de codificación se complete al 100% (CQ-4279389).

* Al mover recursos de una carpeta, se crea un gran número de trabajos de Sling (llamadas a la API de Scene7) que el que se necesita de forma ideal (CQ-4278664).

* Los nombres de los conjuntos de imágenes se cambian a minúsculas en Scene7, cuando se crea un conjunto de imágenes (o conjunto de medios) y se les asigna un nombre con la convención de nombres adecuada en DAM (CQ-4281112).

* Scene7 Migrator establece el estado de publicación incorrectamente (CQ-4263492).

* La página de resultados de búsqueda de la interfaz de usuario táctil (realizada a través de Omnisearch) se desplaza automáticamente hacia arriba y pierde la posición de desplazamiento del usuario en los fragmentos de contenido (CQ-4282898).

* Los archivos PDF no están indexados y el contenido dentro de no se puede buscar (CQ-4278916).

* Un error &quot;Grupo no enumerado por el selector de usuarios: se espera que false sea igual a true&quot; se observa al agregar Closed User Group con diferentes `principalName` y `authorizableId` (CQ-4278177).

* La vista de columna de la interfaz de usuario de Assets muestra todas las rutas, independientemente de la ruta raíz de DAM del inquilino específico (CQ-4278175).

* La búsqueda del selector de recursos no funciona según lo esperado (CQ-4275886).

* Los flujos de trabajo de representación fallan (CQ-4271928).

* Depuración de eventos DAM elimina los datos de evento más recientes (`maxSavedActivities`) y contiene los datos creados anteriormente (NPR-31336).

* La página de resultados de la búsqueda en la interfaz de usuario táctil (realizada a través de Omnisearch) se desplaza automáticamente hacia arriba y pierde la posición de desplazamiento del usuario (NPR-31307).

* La barra de acciones y el recuento de recursos no se actualizan al seleccionar todo y, a continuación, anular la selección de algunos elementos (carpetas o recursos individuales) en la interfaz de usuario táctil (NPR-31118).

* Se muestra una excepción en [!DNL Experience Manager] mientras se sondea por los detalles del trabajo de un recurso (CQ-4283569).

### Sites

* Si se rompe la herencia de LiveCopy, las páginas de Live Copy muestran vínculos de copia de idioma en lugar de vínculos de LiveCopy (NPR-30980).
* Para un nuevo modelo, si el número de registros es superior a 40, solo se muestran los 40 primeros registros. Modelo muestra líneas en blanco para el resto de los registros (NPR-31182).
* Cuando un usuario añade caracteres japoneses o coreanos en la propiedad description de un menú, el menú muestra caracteres distorsionados para texto en japonés y coreano (NPR-31331).
* El Editor de texto enriquecido (RTE) no permite insertar una tabla incrustada como elemento de lista (NPR-30879).
* De forma predeterminada, scaffolding Rich Text Editor (RTE). aplica el tamaño de fuente en línea a los elementos de forma inesperada (NPR-31284).
* Cuando un usuario se centra en los campos del carril izquierdo y utiliza un método abreviado de teclado para pegar contenido, pega el contenido del portapapeles del editor de páginas en lugar del contenido copiado de los campos del carril izquierdo (NPR-31172).
* Cuando un usuario agrega un campo Carga de archivo a un campo múltiple, la ruta de la imagen se almacena en el nodo de componente en lugar del nodo de campo múltiple (NPR-30882).
* La API `ResponsiveGridExporter` no devuelve la interfaz `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter`. El paquete `com.day.cq.wcm.foundation.model.impl` se declara como paquete privado (NPR-31398).

<!-- Review: NPR-31398 has fixVersion as 6530. However, it is mentioned twice in 6530 and 6520 as fixed. 
Remove one mention of this fix.
-->

* Cuando se abre una página que contiene algunos fragmentos de experiencia en modo que no es de editor (ya sea en Autor sin el prefijo `editor.html` y `wcmmode=disabled` o en Editor), la solicitud termina en código de error de estado HTTP `500` (NPR-30743).
* Los usuarios no pueden cambiar su contraseña y acceder a su página de perfil (NPR-31161).

### Interfaz de usuario y búsqueda {#ui-interface-and-search}

* Al cambiar de la vista de tarjeta a la vista de lista en una página de resultados de búsqueda, hay un retraso antes de que la página se pueda desplazar (NPR-31286).

* La casilla [!UICONTROL Seleccionar todo] está oculta en la vista de lista de la interfaz de usuario [!DNL Sites] (NPR-31614).

* El recuento [!UICONTROL Select All] de una página de resultados de búsqueda es incorrecto (NPR-31120).

* El editor de metadatos muestra las etiquetas que no existen (NPR-31119).

### Traducción {#translation}

* Aparecen dos ventanas emergentes de calendario al seleccionar la opción Fecha de vencimiento en un trabajo de traducción (NPR-31270).

### Plataforma

* La opción Mime type en la consola web no funciona (NPR-31108).

* El certificado de cliente no se acepta al configurar el inicio de sesión único (NPR-31165).

* Las actualizaciones en la configuración del tamaño del búfer para el servicio HTTP basado en Jetty no se guardan (NPR-30925).

* QueryBuilder ahora es compatible con el pedido `fn:name()` en consultas xpath (NPR-31322).

* Se crea un árbol de activación duplicado al actualizar desde [!DNL Experience Manager] 6.3 (NPR-31513).

* Las solicitudes reenviadas no conservan los encabezados de respuesta que se establecen durante la autenticación sling (NPR-30013).

* La búsqueda dentro de los componentes del selector no funciona (NPR-31692).

* Se muestra un error al adjuntar un archivo ZIP a una publicación [!DNL Experience Manager Communities] debido a diferentes versiones del paquete POI de Apache y el paquete Tika de Apache (NPR-31018).

* El paquete `org.apache.sling.distribution.api` está oculto en el administrador de configuración y, por lo tanto, no está disponible para paquetes personalizados (NPR-31720).

### Proyectos

* El cambio de vistas de calendario no funciona (NPR-31271).

### Brand Portal {#assets-brand-portal-6530}

**Mejoras del producto**

* El flujo de trabajo de importación de Asset Sourcing en [!DNL Experience Manager Assets] se modifica para recuperar solo los recursos recién creados de [!DNL Brand Portal] a [!DNL Experience Manager] y omitir los recursos que ya existen en la NUEVA carpeta para evitar la replicación (CQ-4278527).

**Correcciones**

* Aparece un icono incorrecto al crear una nueva carpeta de contribución en la función de abastecimiento de recursos (CQ-4282825).
* Al crear una nueva carpeta Contribución, una o ambas subcarpetas (NUEVA y COMPARTIDA) no aparecen dentro de la carpeta Contribución (CQ-4282424).
* El sistema genera una excepción si el usuario intenta volver a publicar la carpeta Contribution de [!DNL Experience Manager] a [!DNL Brand Portal] después de recibir nuevos activos en la carpeta Contribution desde [!DNL Brand Portal] el final (CQ-4279740).
* La creación de la carpeta Contribution dentro de una carpeta Contribution (carpeta anidada) está prohibida para evitar la complejidad (CQ-4278391).
* El sistema genera una excepción al cargar la lista de usuarios [!DNL Brand Portal] (archivo .csv) importada desde el Admin Console [!DNL Experience Manager]. Solo son obligatorios los campos Correo electrónico, Nombre y Apellido del archivo .csv (CQ-4278390).

### Comunidades {#communities-6530}

**Correcciones**

* Los vínculos rápidos para administrar grupos (Open/Edit/Publish/Delete Groups) no son visibles para los administradores de la comunidad (administrador del grupo/administrador del sitio) (NPR-31627).
* Un blog enviado no se muestra a menos que la página se actualice/recargue manualmente (NPR-31599).
* La consulta JCR utilizada por la función &quot;Menciones&quot; distingue entre mayúsculas y minúsculas y tarda demasiado en devolver resultados (NPR-31475).
* [!DNL Experience Manager] 6.5 El archivo UberJar lanza una excepción, el  `cq-social-translation` paquete no aparece en el archivo UberJar  [!DNL Experience Manager] 6.5 (NPR-31186).
* Las bibliotecas de Jackson Databind se actualizaron a la versión 2.9.9.3 para abordar nuevas vulnerabilidades (NPR-30967).
* Los títulos de las actividades y las notificaciones son incoherentes (NPR-30941).
* La paginación no funciona correctamente en los blogs [!DNL Communities] (NPR-30914).
* Los informes de Analytics no se rellenan en el [!DNL Experience Manager] entorno de creación; aparece una página en blanco (NPR-30913).

### Oak {#oak}

* Las actualizaciones del índice de Lucene hacen que el servidor de autor se ralentice (NPR-31548).

### Forms {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack no incluye correcciones para  [!DNL Experience Manager Forms]. Estas se entregan mediante un paquete independiente de complementos de Forms. Además, se ha lanzado un instalador acumulativo que incluye correcciones para [!DNL Experience Manager Forms] en JEE. Para obtener más información, consulte [Instalación del complemento Forms del Experience Manager](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) y [Instalación de Forms del Experience Manager en JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

#### Paquete de complemento de Forms {#forms-add-on-package-6530}

**Formularios adaptables**

* Las cadenas contienen la clave de diccionario al localizar formularios adaptables (NPR-31110).

**Comunicación interactiva**

* **MissingNode.toString()** devuelve resultados inexactos después de actualizar las bibliotecas de Jackson a 2.10.0 (NPR-31549).

* El editor de texto elimina aleatoriamente los caracteres de espacio del texto copiado de Microsoft Word (NPR-31113).

**Administración de correspondencia**

* Los rótulos y la información sobre herramientas no se muestran al migrar letras del LiveCycle ES4SP1 a [!DNL Experience Manager] 6.5 (NPR-31615).

* **El formato del flujo de texto ya no es** compatible con la visualización de un mensaje de error al guardar letras como borradores (NPR-30463).

**Flujo de trabajo**

* El flujo de trabajo de OSGi falla debido a la utilización del 100% de la CPU (NPR-31233).

**Formularios HTML5**

* Al generar la vista previa HTML5 de un formulario XDP, se muestra un parpadeo al agregar instancias de un subformulario (NPR-30909).

#### Instalador de Forms en JEE {#forms-jee-installer-6530}

**Forms: servicios de documentos**

* El servicio web SOAP que utiliza MTOM en un proyecto .NET muestra excepciones para los métodos AssemblerServiceClient invoke y HtmlToPDF2 (NPR-4281771).

* Vulnerabilidad de seguridad 2012-5784 y 2014-3596 encontradas con AXIS 1.4 jar y corregidas con [AXIS1.4.1 jar](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0014.html) (NPR-31015).

**Base JEE**

* La configuración de la acción no carga los nombres de proceso para la acción Invocar un envío de Forms Workflow (NPR-31478).

### Paquetes de funciones incluidos {#feature-packs-included-6530}

>[!NOTE]
>
>Para los clientes [!DNL Experience Manager Forms], es esencial instalar el paquete de complementos [!DNL Experience Manager Forms] después de instalar cualquier paquete de servicio, paquete de correcciones acumulativas o paquete de funciones [!DNL Experience Manager].

#### Forms: base JEE {#forms-foundation-jee-feature}

* [!DNL Experience Manager] Compatibilidad de Forms con el Oracle 18c (NPR-29155).

## Adobe Experience Manager 6.5.2.0 {#experience-manager-6520}

[!DNL Adobe Experience Manager] 6.5.2.0 es una versión importante que incluye correcciones y mejoras clave para el cliente, de rendimiento, estabilidad y seguridad publicadas desde la disponibilidad general de  [!DNL Adobe Experience Manager] 6.5 en  **abril de 2019**. Se puede instalar sobre [!DNL Experience Manager] 6.5.

Algunos aspectos destacados de esta versión de Service Pack son:

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.10.3.
* Se agregó una propiedad de configuración para permitir la exportación de fragmentos de experiencia directamente a espacios de trabajo que haya definido el usuario en [!DNL Adobe Target].
* Los usuarios de recursos pueden buscar imágenes visualmente similares. [!DNL Experience Manager] muestra las imágenes con etiquetas inteligentes del repositorio de DAM similares a una imagen seleccionada por el usuario. Consulte [Búsqueda visual](../assets/search-assets.md#visualsearch).

* Se mejoró la funcionalidad de los recursos conectados para añadir la compatibilidad con la recuperación de documentos desde implementaciones de DAM remotas. Los autores del sitio pueden buscar y filtrar los tipos de documentos admitidos en el Buscador de contenido. Los documentos remotos se pueden agregar al componente Descargar en páginas web. Consulte [Uso de activos conectados](../assets/use-assets-across-connected-assets-instances.md).

* Filtros de tipo EnhanceDocument con más tipos MIME para admitir opciones de varios valores.
* Se ha introducido un flujo de trabajo de reprocesamiento externo para la compatibilidad con varios recursos
* Rendimiento [!DNL Dynamic Media] optimizado mediante el uso de filtros de recursos predeterminados para la replicación.
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
* La descompresión de un archivo con una carpeta que tiene un signo de porcentaje (%) en su nombre no se puede abrir con la interfaz [!DNL Experience Manager Assets]. NPR-29989: revisión para CQ-4270467
* IU táctil: Durante el asistente de administración de publicación, las referencias se agregan después de la página en el cuerpo de la solicitud de publicación, lo que provoca que todos los recursos se publiquen después de la página y, cuando se procesa la página, se pierden algunos de los recursos de la instancia de publicación. NPR-29985: revisión para CQ-4270724
* La función de recursos no relacionados no funciona en recursos relacionados que tienen caracteres especiales (caracteres que se codifican con el URI) en el nombre. NPR-30387: revisión para CQ-4274446
* Al editar un fragmento de contenido, la versión se crea con el usuario incorrecto.
* Error durante la creación de colecciones en el sistema basado en inquilinos. NPR-30114: revisión para CQ-4272948
* La vista de columnas de la IU de recursos no respeta la ruta raíz de DAM del inquilino actual, pero accede a todas las rutas de DAM del inquilino. NPR-30636: revisión para CQ-4275481
* Posible ejecución de scripts en sitios múltiples a través de la ventana de alerta de archivos restringidos, ya que la imagen insertada se puede ver. NPR-30617: revisión para CQ-4270133
* Varios inquilinos: Los inquilinos que guardan las propiedades de la carpeta observan que la acción de descripción del mensaje de error y la solicitud de éxito no se ha realizado correctamente. &quot;No se pueden editar las propiedades. Permisos insuficientes&quot;. Esto, por lo tanto, puede causar confusión. NPR-30545: revisión para CQ-4275333
* El cuadro de diálogo del selector de recursos no permite la selección de recursos, por lo que no se puede actualizar el origen con la funcionalidad de reemplazo de origen relacionada. NPR-30502: revisión para CQ-4275029
* [!UICONTROL Flujo de ] trabajo de recursos de actualización de DAM : en estado obsoleto al cargar archivos mp4 de gran tamaño. NPR-30480: revisión para CQ-4271352
* La funcionalidad para crear la tarea de revisión no funciona debido a una carga útil nula que provoca que todas las acciones relacionadas con la tarea de revisión subsiguientes no funcionen. NPR-30468: revisión para CQ-4274263
* Problema de conectividad de etiquetas inteligentes de Adobe a través de Datapower. NPR-30026: revisión para CQ-4269457
* La vista de columnas de la IU de recursos genera un error al intentar abrir los filtros en el carril izquierdo. NPR-30501: revisión para CQ-4273862
* Al agregar grupos sincronizados desde LDAP en las propiedades del grupo de usuarios cerrado (CUG) de una carpeta de recursos, el grupo no se guarda ni se recupera. NPR-30615: revisión para CQ-4274689
* Los campos de orientación y estilo de búsqueda de filtro no aplican el valor completado automáticamente a la consulta de búsqueda. NPR-30620: revisión para CQ-4275724
* El vínculo de uso compartido de los recursos de una carpeta con espacio y carácter &quot;&amp;&quot; en el nombre, muestra elementos en gris vacíos en algunos recursos. NPR-30557: revisión para CQ-4270187
* El formulario del esquema de metadatos de carpeta no detecta automáticamente el tipo de datos y, por lo tanto, no crea el elemento TypeHint relacionado al enviar el formulario. NPR-30599: revisión para CQ-4275227
* Las opciones de edición de recorte y rotación de recursos están desactivadas en la IU de creación de DMS7. NPR-30118: revisión para CQ-4273221
* La función Compartir vínculo no funciona en la instancia [!DNL Experience Manager] con la configuración de DMS7. NPR-30080, NPR-30492: revisión para CQ-4273651
* Al agregar el componente [!DNL Dynamic Media]-Scene7 a la página y publicarla, la configuración de dmscene7 no se déclencheur cada vez. NPR-30641: revisión para CQ-4275962
* Se ha agregado un IPSJobJournal en [!DNL Experience Manager] para crear solo un trabajo de sistemas de prevención de intrusiones (IPS) por perfil de procesamiento. NPR-30490: revisión para CQ-4273614
* [!DNL Dynamic Media]: Se han agregado filtros predeterminados para excluir los recursos de la replicación en el nodo de  [!DNL Experience Manager] publicación. NPR-30538: revisión para CQ-4274678
* Se ha introducido un flujo de trabajo de reprocesamiento externo para la compatibilidad con varios recursos a fin de permitir que la carpeta sea una carga útil. El flujo de trabajo consta de dos pasos: vuelve a procesar los recursos sin controladores mediante el mapa de metadatos al paso siguiente y vuelve a cargar todos los recursos sin el control de recursos en S7 en un solo trabajo de IPS. Para obtener más información, consulte Configuración de Cloud Services [!DNL Dynamic Media] . NPR-30489: revisión para CQ-4272903
* Al cargar un archivo CSV incorrecto después de uno correcto, se elimina el archivo CSV correcto. Revisión para CQ-4277694, CQ-4277814
* Se va a eliminar el icono incorrecto específico de las carpetas de contribución. Revisión para CQ-4277580
* Al seleccionar un usuario en el selector de usuarios de la ficha Contribución de recursos, el nombre del usuario no aparece en la tabla y el cuadro de diálogo Eliminar usuario que está en la página Propiedades muestra un texto incorrecto. Revisión para CQ-4277875
* Los colaboradores no se pueden agregar a la carpeta de Contribución de recursos desde el selector de usuarios al seleccionar al usuario y hacer clic en Añadir. Revisión para CQ-4277824, CQ-4278087
* La búsqueda por nombre de usuario en minúsculas no funciona en el selector de usuarios. Revisión para CQ-4277958, CQ-4277930
* Los usuarios que no son administradores pueden publicar recursos en una nueva carpeta que esté en una carpeta de contribución de recursos. Revisión para CQ-4278200
* dam-user (no es administrador) no tiene la opción de añadir colaboradores a la carpeta de contribución de recursos. Revisión para CQ-4278192
* El botón &quot;Crear&quot; está visible en la carpeta de contribución de recursos. Revisión para CQ-4277560
* Al ordenar la consulta de búsqueda por relevancia, se devuelven [!DNL InDesign] documentos junto con [!DNL InDesign] plantillas. Revisión para CQ-4273864
* Si el usuario tiene un id. de correo electrónico en mayúsculas, los usuarios no pueden registrar los recursos que ya se han extraído. Revisión para CQ-4276575
* La operación Eliminar solo se aplica a los ajustes preestablecidos seleccionados y, si la pantalla actualiza automáticamente la lista después de la operación, se muestran otros ajustes preestablecidos que ya se han actualizado. Revisión para CQ-4261461
* La configuración de los Cloud Services [!DNL Dynamic Media] en modo [!DNL Dynamic Media]-híbrido da como resultado varios grupos de informes vacíos creados en [!DNL Analytics] y sin ningún id de grupo de informes almacenado en [!DNL Experience Manager], lo que resulta en una duplicación del grupo de informes. Revisión para CQ-4249780
* La operación Cambiar el nombre del recurso [!DNL Experience Manager] al nombre duplicado no se sincroniza con Scene7. Revisión para CQ-4276763
* El contenido que creó el usuario se muestra incorrectamente en el panel de filtros de búsqueda. Revisión para CQ-4273875
* La opción Buscar similares no está disponible en imágenes TIFF. Revisión para CQ-4278238
* Se ha implementado la opción de silenciar el vídeo durante la carga en VideoPlayer. Revisión para CQ-4266465
* Visualizadores: Visor de vídeos: poster=none funciona incorrectamente en el caso de que se utilice un vídeo externo. Revisión para CQ-4265536
* El icono de espera está visible durante la reproducción de vídeos en los navegadores IE11 y MS Edge. Revisión para CQ-4251539
* Los archivos README del SDK 3.8 y de los visores 5.13 no se actualizan y contienen información de versiones anteriores. Revisión para CQ-4273737
* El fragmento de contenido recibe versiones incluso antes de guardar los cambios. NPR-30616: revisión para CQ-4273088
* Se reemplaza el valor de Asset#getMetadata(String) con Asset#getMetadataValueFromJcr(String) en el proceso de creación de miniaturas. NPR-30491: revisión para CQ-4273067
* La carga de archivos JPG devuelve varias instancias del mensaje &quot;Replicación del elemento ReplicateOnModifyWorker ACTUALIZADA&quot; en cada recurso, lo que provoca una degradación del rendimiento.
* Si se descomprime el archivo zip mediante la función Extraer archivo se producen problemas con las carpetas cuyo nombre contiene el símbolo de porcentaje (%) en el título. NPR-29990: revisión para CQ-4270467

### Sitios {#sites-6520}

* Si se rompe la herencia de LiveCopy, las páginas de Live Copy muestran vínculos de copia de idioma en lugar de vínculos de LiveCopy (NPR-30980).
* Para un nuevo modelo, si el número de registros es superior a 40, solo se muestran los primeros 40 registros. Modelo muestra líneas en blanco para el resto de los registros (NPR-31182).
* El complemento Editor de texto enriquecido (RTE) del componente de texto muestra caracteres distorsionados para texto en japonés y coreano (NPR-31331).
* El Editor de texto enriquecido (RTE) no permite insertar una tabla incrustada como elemento de lista (NPR-30879).
* El scaffolding Rich Text Editor (RTE) de fuera de la caja se aplica en línea de tamaño de fuente a los elementos de forma inesperada (NPR-31284).
* Cuando un usuario se centra en los campos del carril izquierdo y utiliza combinaciones de teclas para pegar contenido, pega el contenido del portapapeles del editor de páginas en lugar del contenido copiado de los campos del carril izquierdo (NPR-31172).
* Cuando un usuario agrega un campo Carga de archivo a un campo múltiple, la ruta de la imagen se almacena en el nodo de componente en lugar del nodo de campo múltiple (NPR-30882).
* La API `ResponsiveGridExporter` no devuelve la interfaz `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter`. El paquete `com.day.cq.wcm.foundation.model.impl` se declara como paquete privado (NPR-31398).
* Cuando se abre una página que contiene algunos fragmentos de experiencia en modo que no es de editor (ya sea en Autor sin el prefijo `editor.html` y `wcmmode=disabled` o en Editor), la solicitud termina en código de error de estado HTTP 500 (NPR-30743).

### WCM: editor de páginas {#wcm-page-editor-6520}

**Mejoras del producto**

* Filtros de tipo EnhanceDocument con más tipos MIME para admitir opciones de varios valores. Revisión para CQ-4270694

### Administración de fragmentos de contenido {#content-fragment-management-6520}

* La consulta que isa la IU de los modelos de fragmento de contenido es muy lenta y, finalmente, acaba en error. Revisión para CQ-4270807

### IU: bases {#ui-foundation}

* Desencadenador de accesos directos que impide que el usuario utilice &quot;m,&quot; &quot;p,&quot; y &quot;e&quot; en las interfaces de usuario específicas. NPR-30355: revisión para GRANITE-26346
* Al cerrar la [!DNL Experience Manager Assets] interfaz de usuario de búsqueda no se restablece el carril izquierdo a la selección de contenido, lo que impide que el usuario abra el carril de filtro por segunda vez posteriormente. NPR-30509: revisión para CQ-4274716
* Entorno de varios inquilinos: [!DNL Experience Manager Assets] La navegación superior de la interfaz de usuario no está disponible y se produce un error de JavaScript. NPR-30104: revisión para GRANITE-26344

### Traducción {#translation-6520}

* Problema de traducción: solo unos pocos componentes se traducen mediante traducción automática. NPR-30079: revisión para CQ-4273764

### Plataforma {#platform-6520}

* [!DNL Experience Manager]El remitente de correo predeterminado de no puede enviar correo a un servidor SMTP remoto a través de TLS v1.2. NPR-30476: revisión para GRANITE-26605

### Proyectos {#projects-6520}

* Los valores de dam:folderThumbnailPaths no se actualizan y muestran miniaturas antiguas incluso después de eliminar los recursos de la carpeta. NPR-30424: revisión para CQ-4273667
* Al completar la opción Mover, el título y el nombre del activo no cambian. NPR-30647: revisión para CQ-4276265

### Comunidades {#communities-6520}

* El diagnóstico de sincronización de usuarios está completamente dañado y no funciona. NPR-30004, NPR-29943: revisión para CQ-4270287, CQ-4271348

### Sling  {#sling}

* La instancia actualizada de 6.3.3.2 a 6.5 devuelve configuraciones OSGi duplicadas. NPR-30130: revisión para CQ-4274016

### Integración

* El contenido personalizado no se muestra correctamente en la instancia de publicación hasta que no se reinicia la instancia. NPR-30377: revisión para CQ-4273706
* Al configurar el inicio en un sitio web, la dirección de la biblioteca tiene una barra diagonal (/) precargada, lo que provoca que el usuario tenga que intervenir de forma manual cada vez. NPR-30694: revisión para CQ-4275501

### Forms {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack no incluye correcciones para  [!DNL Experience Manager Forms]. Se entregan mediante un paquete de complementos [!DNL Forms] independiente. Además, se ha lanzado un instalador acumulativo que incluye correcciones para [!DNL Experience Manager Forms] en JEE. Para obtener más información, consulte [Instalación del complemento Forms del Experience Manager](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) y [Instalación de Forms del Experience Manager en JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

Los aspectos destacados de los formularios [!DNL Experience Manager] 6.5.2.0 son:

* Se ha agregado la configuración &quot;Automático&quot; a `RenderAtClient` en la API `PDFFormRenderOptions` para [!DNL Experience Manager] OSGi de Forms.

#### Paquete de complemento de Forms

**Integración del back-end**

* No se puede configurar el modelo de datos de formulario con una URL de carga equilibrada alojada en AWS. NPR-30123: revisión para CQ-4273359
* Al crear el modelo de datos de formulario (FDM) con el lenguaje de definición de servicio web (WSDL), se devuelve el mensaje de error `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type`: NPR-30477: Revisión para CQ-4272921

**Administración de correspondencia**

* &quot;La representación de la IU de creación de correspondencia (IU de CCR) falla de forma intermitente con el siguiente error en la consola:
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**Comunicación interactiva**

* Un campo marcado como obligatorio en el modelo de datos del formulario se muestra como necesario en la IU para crear correspondencia. NPR-30623: revisión para CQ-4274902

**Forms: flujo de trabajo**

* Las variables de salida no asignadas en las carpetas inspeccionadas hacen que la invocación genere un error. Revisión para CQ-4264451

**Formularios HTML5**

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
* Al agregar o editar una conexión de servicio Web invocando servicios Web desde [!DNL Experience Manager Forms] Workbench, se genera un error: ClassNotFoundException org.apache.axis.message.SOAPBodyElement. NPR-30105: revisión para CQ-4273217

### Paquetes de funciones incluidos

>[!NOTE]
>
>Para los clientes [!DNL Experience Manager Forms], es esencial instalar el paquete de complementos [!DNL Experience Manager Forms] después de instalar cualquier paquete de servicio, paquete de correcciones acumulativas o paquete de funciones [!DNL Experience Manager].

#### Sitios {#sites-feature-packs-included}

* Se agregó una propiedad de configuración para permitir la exportación de fragmentos de experiencia directamente a espacios de trabajo que haya definido el usuario en [!DNL Adobe Target]. NPR-29189: revisión para CQ-4249782

#### Forms: servicios de documentos {#forms-document-services-1}

* Se ha agregado la configuración &quot;Automático&quot; a `RenderAtClient` en la API `PDFFormRenderOptions` para [!DNL Experience Manager Forms] OSGi. NPR-30759: revisión para CQ-4278193

## Adobe Experience Manager 6.5.1.0 {#experience-manager-6510}

[!DNL Adobe Experience Manager] 6.5.1.0 es una versión importante que incluye correcciones y mejoras clave para el cliente, de rendimiento, estabilidad y seguridad publicadas tras la publicación general de la versión  [!DNL Adobe Experience Manager] 6.5 en  *abril de 2019.*[!DNL Experience Manager] Se puede instalar en 6.5.

Algunos aspectos destacados de esta versión de Service Pack son:

* Se habilitó la inclusión de dynamic-UI-state en el seguimiento de eventos como atributos personalizados. 
* Se ha incluido compatibilidad con el envío de recursos de vídeo de 360 grados en el modo [!DNL Dynamic Media]-Scene7.
* Se habilitó la función *Justificación de palabras japonesas* mediante el complemento de estilos del Editor de texto enriquecido. Para obtener más información, consulte [Configuración del ajuste de palabras en japonés](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### Recursos

* Se ha actualizado la interfaz DAM DMGateway para que sea compatible con varias partes de S3. NPR-29740: revisión para CQ-4226303
* La vista previa de representaciones genera el error `Only empty tenantId is currently supported` después de actualizar a [!DNL Experience Manager] 6.5. NPR-29986: Revisión para CQ-4272353
* El cuadro de diálogo Eliminar no está visible para permitir la eliminación de trabajos. NPR-29720: revisión para CQ-4271074
* Después de agregar el título del recurso en la página de propiedades, cuando un usuario intenta cerrar la página, [!DNL Experience Manager] vuelve a abrir la página de propiedades. NPR-29627: revisión para CQ-4264929
* El elemento VersioningTimelineEventProvider debe proporcionar la versión raíz junto con el nodo de tipo nt: versión. Revisión para GRANITE-26063
* Se ha implementado la capacidad de cargar y reproducir 360 vídeos esféricos en modo [!DNL Experience Manager] DM-Scene7. Revisión para CQ-4265131
* Live Copy recupera un estado incorrecto si se edita el origen. Revisión para CQ-4265451
* Se habilitó la compatibilidad con Multi-Site Manager para [!DNL Experience Manager Assets]. Revisión para CQ-4271453, CQ-4268621, CQ-4257491
* [!DNL Experience Manager] La interfaz de debe mostrar una entrada adicional para la versión actual del recurso en el historial de cronología, mostrando el último comentario de registro de  [!DNL Adobe Asset Link]. Revisión para CQ-4262864
* La línea de tiempo del fragmento de contenido muestra un mensaje de error cuando faltan propiedades. Revisión para CQ-4272560
* Problema con el reproductor de vídeo de Scene7 cuando se expande a pantalla completa. Revisión para CQ-4266700
* ZoomVerticalViewer: los botones de desplazamiento no se deben mostrar si se utiliza un único recurso de imagen. Revisión para CQ-4264795
* La eliminación de un nodo secundario en Live Copy debe desasociar el elemento liveRelationship. Revisión para CQ-4270395
* El esquema de metadatos solo contiene elementos de la configuración global y no contiene los del inquilino activo. El valor de la dirección URL de formPath vuelve al valor predeterminado incluso cuando se cambia. NPR-29945: revisión para CQ-4262898
* La publicación de ajustes preestablecidos de imagen en [!DNL Brand Portal] falla con un código de error 500. NPR-29510: revisión para CQ-4268659

### Sitios

* Las propiedades vacías y varias propiedades no se propagan desde el modelo durante el lanzamiento. El restablecimiento de Live Copy con un plano técnico no funciona en los componentes. NPR-29253: revisión para CQ-4264928, CQ-4264926, CQ-4267722
* Cuando se utiliza CoralUI con `Multifield`, almacena el `fileReferenceParameter` en el nivel de componente en lugar de en el nivel de campo múltiple. NPR-29537: revisión para CQ-4266129
* Mejora del componente de texto [!DNL Experience Manager] y del Editor de texto al japonés. NPR-29785: revisión para CQ-4265090
* La página restaurada con Deformación de tiempo debe hacer referencia a la imagen correcta en el momento de controlar las versiones. NPR-29431: revisión para CQ-4262638
* Problema con la herencia de los nodos del sistema de estilos de principal a secundario. NPR-29516: revisión para CQ-4270330
* Mensaje de error al configurar la publicación social en autenticación [!DNL Facebook]. NPR-29211: revisión para CQ-4266630
* La miniatura representada en el fragmento de contenido muestra una representación interna del calendario para los campos de fecha y hora. NPR-29531: revisión para CQ-4269362
* Al abrir la ficha Permisos en la implementación de Coral2 no se muestran los botones. Revisión para CQ-4269419

### Comercio

* ConstraintViolationException, cuando se ejecuta la migración de contenido diferido para el comercio electrónico. NPR-29247: revisión para CQ-4264383

### Administración de fragmentos de contenido

* Error de análisis al abrir un fragmento de contenido que tiene caracteres de dólar `($)` y llave `({)` abierta. Revisión para CQ-4270266

### Fragmentos de experiencias

* Exportar [!DNL Experience Manager] fragmentos de experiencias a [!DNL Adobe Target]. Revisión para CQ-4265469
* La exportación de fragmentos de experiencias al destino falla con la imagen inteligente. Revisión para CQ-4269606

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

* La actualización a [!DNL Experience Manager] 6.4.3 hace que el administrador de varios sitios tarde mucho en implementarse. Revisión para CQ-4271410

### Integración

* Error de conexión en las credenciales de BrightEdge. NPR-29168: revisión para CQ-4265872

* Se muestra un mensaje de excepción al intentar editar y guardar la configuración de inicio [!DNL Experience Manager]. NPR-29176: revisión para CQ-4265782/CQ-4266153

### Interfaz de usuario

* Se agregó la compatibilidad para rastrear estados de IU dinámicos como atributos personalizados, mientras se rastrean determinados eventos en la API de seguimiento de base. Revisión para GRANITE-26283
* No se puede establecer la función de seguimiento en el botón de envío. Revisión para GRANITE-26326
* El asistente no puede establecer la función de seguimiento en el botón de envío. NPR-29995, NPR-30025: revisión para CQ-4264289

### Communities

* No se pueden alinear los nuevos distintivos en la lista desplegable de la página de perfil del usuario. NPR-29381: revisión para CQ-4267987
* Los visitantes y los miembros que no tengan privilegios de moderador pueden ver las publicaciones pendientes o no aprobadas pegando la dirección URL. NPR-29724: revisión para CQ-4271124, CQ-4271441
* Se observa un tiempo de respuesta alto de hasta 40-50 segundos cuando el usuario inicia sesión en la comunidad. NPR-29677: revisión para CQ-4269444

### Replicación

* El componente del agente de replicación es susceptible a una vulnerabilidad que revela información confidencial a usuarios no autorizados. NPR-29611: revisión para GRANITE-25070

* Se cierra la sesión durante el proceso de OAuth en cada replicación a [!DNL Brand Portal]. NPR-30001: revisión para GRANITE-26196

### Proyectos

* Publicar [!DNL Experience Manager Assets] desde la [!DNL Experience Manager] carpeta Autor /content/dam/mac a [!DNL Brand Portal] no funciona. NPR-29819: revisión para CQ-4271118

### Plataforma

* HtmlLibraryManager elimina todo el contenido de crx-quickstart cuando se invalida la caché. NPR-29863: revisión para GRANITE-26197

### Felix

* Los detalles de uso de memoria no se muestran en la consola del sistema al utilizar Java11\. NPR-29669

### Forms

Los aspectos destacados de [!DNL Experience Manager Forms] 6.5.1.0 son:

* Solo OSGi: Se ha agregado un nuevo atributo `PAGECOUNT` en Output y Forms Service.

* Solo OSGI: Se ha habilitado la compatibilidad para crear archivos PDF estáticos mediante el servicio de Forms.
* Permisos activados en XMLForm.exe para usuarios raíz y administradores.
* Se habilitó la compatibilidad con ADFS v3.0 para la integración local de Dynamics.

#### Paquete de complemento de Forms

**Integración de back-end**

* Error al recuperar el lenguaje de definición del servicio web protegido (WSDL). NPR-29944: revisión para CQ-4270777
* Cuando [!DNL Experience Manager Forms] está instalado en IBM WebSphere, la creación de un modelo de datos de formulario basado en SOAP falla. Revisión para CQ-4251134
* Se habilitó la compatibilidad con los servicios de federación de Active Directory (ADFS) v3.0 para la integración local de Microsoft Dynamics. Revisión para CQ-4270586
* Cuando se cambia el título de un origen de datos, el modelo de datos de formulario no muestra el título actualizado. Revisión para CQ-4265599
* Si el nombre de una entidad o atributo contiene guiones o espacio, las expresiones no pueden evaluar dichas entidades y atributos. Revisión para CQ-4225129

* Se observa un resultado incorrecto cuando hay dos puntos en la salida de cadena primitiva. Revisión para CQ-4260825

* Incluso cuando no se espera contenido del resultado de la API de REST, la operación de invocación del modelo de datos de formulario genera un error. Revisión para CQ-4268828

**Formularios adaptables**

* No se puede agregar una nueva instancia en el fragmento del formulario adaptable durante la carga diferida. NPR-29818: revisión para CQ-4269875
* El componente de verificación no registra ni muestra ningún error en las plantillas del documento de registro. Revisión para CQ-4272999
* Se agregó la compatibilidad para deshabilitar el editor de diseño para formularios adaptables. Revisión para CQ-4270810
* Se ha restaurado el paso de verificación para Forms adaptable en [!DNL Experience Manager] 6.5. Revisión para CQ-4269583

* El error de validación del campo del formulario adaptable rompe [!DNL Adobe Sign]. Revisión para CQ-4269463
* Cuando una instancia [!DNL Experience Manager Forms] tiene más de 20 fragmentos de formulario adaptables y el nombre de todos los fragmentos de formulario comienza con la misma cadena, la búsqueda no devuelve fragmentos creados o solo devuelve 20 fragmentos creados recientemente. Revisión para CQ-4264414, CQ-4264914

* Problemas de rendimiento cuando la aplicación de formularios adaptables se utiliza con conjuntos de datos grandes. . Revisión para CQ-4235310

* Cuando se accede a través de una cuenta anónima en una instancia de publicación, la secuencia de comandos de GuideRuntime no se carga. Revisión para CQ-4268679

**Forms: comunicación interactiva**

* La plantilla de comunicación interactiva no enumera los componentes del encabezado y pie de página en la lista de componentes permitidos. Revisión para CQ-4237895
* Cuando se crea una plantilla de impresión de comunicación interactiva que contiene un campo de imagen, el título del gráfico se define en blanco. Revisión para CQ-4264772
* Color de línea de un gráfico que, al eliminarse, se establece como no definido. Revisión para CQ-4264762
* Los cambios realizados en la capa de diseño en el fragmento de documento desaparecen al realizar los cambios de mantenimiento sincronizados. Revisión para CQ-4266054
* El elemento del modelo de datos de formulario de un fragmento de documento vinculado a un campo de texto no muestra el icono de herencia y permite el enlace. Revisión para CQ-4261089
* La API de procesamiento del canal de impresión no tiene la opción de pasar datos como parámetro en la API. Revisión para CQ-4263540
* La configuración del agente no está visible, ya que la casilla de verificación Editar por agente se desmarca cuando el tipo de enlace se cambia de fragmento de texto a Ninguno/Objeto de modelo de datos para el campo/variable de cadena. Revisión para CQ-4261953
* Al enviar la interfaz de usuario del agente, el archivo json de datos web resultante almacena información para los campos independientes cancelados por herencia. Revisión para CQ-4265621

**Forms: flujo de trabajo**

* Cuando se vuelve a enviar un formulario desde la bandeja de salida de la aplicación de formularios adaptables, se pierden datos. NPR-28345: revisión para CQ-4260929
* Los documentos no se cierran mientras se guardan en casos no variables. Revisión para CQ-4269784
* La aplicación de formularios adaptables ha dejado de ser compatible con Microsoft Windows 8.1. Revisión para CQ-4265274
* Cuando se adjunta una imagen de más de 2 MB como archivo adjunto de nivel de campo a un formulario en la versión de Android de la aplicación [!DNL Experience Manager Forms], la aplicación se bloquea. Revisión para CQ-4265578

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

* [!DNL Experience Manager Forms] 6.5 La IU Crear correspondencia (IU de CCR) no abre la correspondencia creada con  [!DNL Experience Manager Forms] 6.3. Revisión para CQ-4266392
* La función Sumar en XDP no funciona si el tipo de datos de DDE es de tipo número. Revisión para CQ-4227403
* Se va a actualizar la lógica de invalidación de letras en memoria de la caché, porque cuando se publica un recurso no se actualiza la hora de la última modificación. Revisión para CQ-4250465
* No se puede publicar un fragmento de documento, DD y letras. Revisión para CQ-4272893

#### Instalador JEE de Forms

**Generador de PDF**

* La conversión de archivos CAD a PDF ha producido un error con JDK de 64 bits. NPR-29924, NPR-29925: revisión para CQ-4272113
* Se reemplazó el nombre de PhantomJS a WebToPDF para la conversión de HTMLtoPDF. NPR-29933: revisión para CQ-4234545
* Se genera un error al convertir el archivo zip a PDF. Revisión para CQ-4268628

**Forms: Designer**

* Cuando se realiza una comprobación de accesibilidad completa en el PDF estático creado mediante [!DNL Experience Manager Forms Designer], la comprobación del idioma principal falla debido a la ausencia del atributo del idioma. Revisión para CQ-4272923, CQ-4271002

**Forms: seguridad de documentos**

* La firma digital con módulo de seguridad de hardware (HSM) no funciona en OSGi Linux en Java 11 y Java 8\. NPR-29838: revisión para CQ-4270441
* La firma digital con el módulo de seguridad de hardware (HSM) no funciona en JEE Linux ni en ninguno de los servidores de aplicaciones compatibles, como JBoss y Websphere. NPR-29839: revisión para CQ-4266721
* La comprobación de firmas en un PDF mediante firma electrónica avanzada en formato PDF (PAdES) genera la excepción InvalidOperationException. NPR-29842: revisión para CQ-4244837
* Se agregó la compatibilidad de Document Security Extension con Office 2019\. Revisión para CQ-4254369, CQ-4259764

**Forms: servicios de documentos**

* El PDF no se puede convertir a PDF/A-1b; el campo Formulario no tiene diccionario de apariencia. NPR-29940: revisión para CQ-4269618

* OSGi: No se puede determinar el número de páginas generadas durante el procesamiento. NPR-28922: revisión para CQ-4270870
* Se habilitó la compatibilidad con archivos PDF estáticos mediante el servicio de Forms en [!DNL Experience Manager Forms OSGi]. NPR-28572: revisión para CQ-4270869
* No se pueden cambiar los permisos en el archivo XMLForm.exe. NPR-29828, NPR-29237: revisión para el T-4267080
* El PDF estático creado por el módulo de salida del servidor [!DNL Experience Manager Forms] no rellena el atributo/etiqueta de idioma con el idioma del documento creado. NPR-27332: revisión para CQ-4271002

**Forms: base JEE**

* Pdfg_srt no está disponible en los artefactos finales y provoca errores en el instalador. NPR-29854: revisión para CQ-4270137
* LCBackupMode.sh no funciona. NPR-29840: revisión para CQ-4269424
* La referencia del puerto UDP debe eliminarse de la interfaz de usuario (IU) para WebSphere. Revisión para CQ-4264782

### Paquetes de funciones incluidos

#### Recursos - Incluido

* Se habilitó la compatibilidad con Multi-Site Manager para [!DNL Experience Manager Assets]. Para obtener más información, consulte [Reutilización de recursos con MSM para recursos de Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-65/assets/using/reuse-assets-using-msm.html). NPR-29199: revisión para CQ-4259922

#### Sitios: incluidos

* Exportar [!DNL Experience Manager] fragmentos de experiencias a [!DNL Adobe Target]. Para obtener más información, consulte [El proveedor de reescritura de vínculos de fragmentos de experiencias - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). Revisión para CQ-4265469

#### Forms - Servicios de documentos - Incluidos

* Solo OSGi: Se ha agregado un nuevo atributo PAGECOUNT en Output y Forms Service. NPR-28922: revisión para CQ-4270870
* Solo OSGi: Se ha habilitado la compatibilidad para crear archivos PDF estáticos mediante el servicio de Forms. NPR-28572: revisión para CQ-4270869
* Permisos activados en XMLForm.exe para usuarios raíz y administradores. NPR-29237: revisión para CQ-4267080

### Paquetes de contenido y paquetes OSGi

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en [!DNL Experience Manager] 6.5.1.0

Lista de paquetes OSGi incluidos en [!DNL Experience Manager] 6.5.1.0

[Obtener archivo](assets/6_5-bundle-list.txt)

Lista de paquetes de contenido incluidos en [!DNL Experience Manager] 6.5.1.0

[Obtener archivo](assets/6_5-content-package-list.txt)
