---
title: '[!DNL Adobe Experience Manager] Notas de la versión de Service Pack 6.5'
description: Notas de la versión específicas de [!DNL Adobe Experience Manager] 6.5 Service Pack 7
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: c92efd64662e831c8771a8f35701f4e9ed788645
workflow-type: tm+mt
source-wordcount: '4201'
ht-degree: 5%

---


# [!DNL Adobe Experience Manager] Notas de la versión de Service Pack 6.5  {#aem-service-pack-release-notes}

## Información de la versión {#release-information}

| Productos | [!DNL Adobe Experience Manager] 6,5 |
| -------- | ---------------------------- |
| Versión | 6.5.7.0 |
| Tipo | Versión de Service Pack |
| Fecha | 26 de noviembre de 2020 |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip) |

<!-- TBD: Update the SD link when SP7 is available. -->

## Qué se incluye en [!DNL Adobe Experience Manager] 6.5.7.0 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.7.0 es una actualización importante que incluye nuevas funciones, mejoras clave solicitadas por los clientes y mejoras de rendimiento, estabilidad y seguridad, que se han publicado desde la versión 6.5 de abril de 2019. El Service Pack se instala en [!DNL Adobe Experience Manager] 6.5.

Las funciones y mejoras clave introducidas en [!DNL Adobe Experience Manager] 6.5.7.0 incluyen:

* Ordenar las páginas de Live Copy disponibles para la implementación con las propiedades [!UICONTROL Name], [!UICONTROL Last modified date,] y [!UICONTROL Last rollout date].

* Realizar los movimientos de página y los despliegues de MSM como operaciones asincrónicas para reducir su impacto en el rendimiento del tiempo de ejecución.

* Los usuarios pueden ordenar recursos digitales en vistas de tarjetas y columnas.

* [!DNL Assets] y  [!DNL Dynamic Media] proporcionar varias mejoras de accesibilidad. Las mejoras están relacionadas con la navegación mediante el teclado, el uso de lectores de pantalla y la posibilidad de que los usuarios utilicen una tecnología de asistencia similar (AT). Consulte [[!DNL Assets] mejoras](#assets-6570) y [[!DNL Dynamic Media] mejoras](#dynamic-media-6570).

* Configuración del cliente HTTP del modelo de datos de formulario para optimizar el rendimiento.

* Disponibilidad de la opción Restablecer para cada componente en el modo Diseño

* [!DNL Experience Manager] 6.5 Service Pack 7 Forms mejora el rendimiento de:

   * Validando los valores de campo en el servidor al enviar un formulario adaptable.

   * Conversión de un formulario PDF a un formulario adaptable mediante [!DNL Automated Forms Conversion service].

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.22.5.

Para obtener una lista completa de las funciones y mejoras introducidas en [!DNL Experience Manager] 6.5.7.0, consulte [Novedades de [!DNL Adobe Experience Manager] 6.5 Service Pack 7](new-features-latest-service-pack.md).

La siguiente es la lista de correcciones que se proporciona en la versión [!DNL Experience Manager] 6.5.7.0.

### [!DNL Sites] {#sites-6570}

* Cuando abre la opción [!UICONTROL Timewrap] para una página, mantenga abierta la opción de carril lateral de la línea de tiempo y navegue a la consola [!UICONTROL Sites], se produce el error `Failed to Load` (NPR-34951).

* La opción [!UICONTROL Timewrap] no muestra imágenes para el intervalo de fecha y hora seleccionado (NPR-34951).

* Cuando un filtro llama a `getHeader()` desde una página que contiene un fragmento de contenido, se produce el error `java.lang.AbstractMethodError` (NPR-34942).

* Cuando la ruta de una página contiene varias subcadenas de contenido, las previsualizaciones no se procesan y la función de comparación de versiones también falla (NPR-34740).

* Cuando se establece un valor numérico para la propiedad de etiqueta de tipo `String` de un componente, se puede eliminar el componente y deshacer la operación de eliminación. Sin embargo, después de deshacer la operación de eliminación, la propiedad label cambia de `String` a `Long` (NPR-34739).

* La siguiente excepción se produce al agregar un fragmento de experiencia basado en una plantilla con un diseño bloqueado a una página (NPR-34632):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* Al mover una carpeta, se producen problemas transversales y se produce el siguiente error (NPR-34554):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* Cuando se crean, publican y mueven nuevos recursos a una nueva ubicación, se crea el flujo de trabajo `Request to complete move operation` y se anula el estado. Al cargar un nuevo recurso y ejecutar una operación `move` se crea el flujo de trabajo `Request to complete move operation` en estado pendiente (NPR-34543).

* Al exportar un fragmento de experiencia de [!DNL Experience Manager] 6.5.2 entorno a [!DNL Target] Standard, la llamada de API falla porque la propiedad del área de trabajo no está disponible para [!DNL Target] Standard (NPR-34557).

* Los usuarios no pueden publicar páginas mediante la opción [!UICONTROL administrar publicación] porque la opción [!UICONTROL Publicar] desaparece (NPR-34542).

* Al agregar algunos estilos al texto, se agrega una etiqueta `<div>` al texto y el estilo ya no se puede aplicar al texto (NPR-34531).

* Cuando se selecciona un elemento en un menú emergente y se actualizan los archivos necesarios, no se permiten guardar valores de cuadro de diálogo, ya que el otro menú tiene un campo obligatorio vacío (NPR-34529).

* Al crear una página a partir de una plantilla personalizada y moverla dentro de la jerarquía del modelo, los componentes se eliminan antes de los inicios de página que aparecen en la página dentro de la jerarquía de Live Copy (NPR-34527).

* Una vez aplicado un estilo de artículo a un contenido, no se puede eliminar (NPR-34486).

* Todas las copias en vivo y las copias de un fragmento de experiencia apuntan al mismo [!DNL Adobe Target] ID de oferta (NPR-34469).

* Los elementos de lista con viñetas se muestran además de la lista numerada (NPR-34455).

* La opción de comparación con el origen no muestra la diferencia entre la página de origen y la versión editada de una página (NPR-34285).

* Al eliminar una página, los detalles de las versiones no se pueden configurar (NPR-34159).

* Cuando un usuario selecciona la opción de diálogo [!UICONTROL Selección abierta], el enfoque del teclado se desplaza al control oculto presente en la página (CQ-4307779, CQ-4293601).

* Al mover una carpeta publicada en el Autor, las rutas de acceso de la carpeta no se actualizan en consecuencia en la instancia de publicación (CQ-4305144).

* Cuando un usuario selecciona la tecla `Enter` en la opción [!UICONTROL Seleccionar todo], el enfoque del teclado no se mueve a la opción [!UICONTROL Crear control] (CQ-4293599).

* Al seleccionar la clave `Esc`, el enfoque no se restaura al control principal (CQ-4293593, CQ-4293590).

* Se mejoró la compatibilidad con WCAG para [!DNL Sites] UI y componentes principales (CQ-4293448).

* [!UICONTROL Las funciones ] de ampliación   de zoom y escala están desactivadas para la  [!DNL Sites Editor] página (CQ-4282353).

* Después de utilizar la opción Girar a la derecha, el lector de pantalla deja de narrar el estado de rotación o de volteo actual (CQ-4282128).

* Los botones de diálogo Listo y Cancelar configuración tienen más de un tabulador (CQ-4274601).

* No se permite mover páginas con un nombre similar en el mismo nivel (NPR-35041).

* Después de seleccionar la opción Borrar (x), el enfoque del teclado no se mueve al campo [!UICONTROL Filtro] (CQ-4293581).

* Al actualizar a [!DNL Experience Manager] 6.5.6.0, el comportamiento del sistema de párrafos heredado cambia y no funciona correctamente (NPR-35117).

* Los usuarios del teclado no pueden cambiar el enfoque de la ficha en un orden adecuado después de seleccionar la sección [!UICONTROL Acción] en una página [!DNL AEM Sites] (CQ-4307786).

* Después de seleccionar una opción en la lista de menú del destinatario de vínculos de la barra de herramientas RTE al editar un fragmento de contenido, el cuadro de diálogo del autor del fragmento de contenido inicio para parpadear (CQ-4305532).

* Los usuarios del teclado no pueden seleccionar las opciones de la lista desplegable [!UICONTROL Añadir componente] mediante la tecla de flecha abajo (CQ-4295097).

* El enfoque de tabulación no cambia en el orden adecuado al seleccionar una fecha en el menú Calendario de la ficha [!UICONTROL Recursos] de una página [!DNL Sites] (CQ-4293600).

* El enfoque de tabulación no cambia a las opciones siguientes o anteriores para los usuarios del teclado después de eliminar las opciones Vínculo o Texto disponibles al editar una página Sitios (CQ-4293597).

* Los usuarios del teclado no pueden volver a cambiar el enfoque de la ficha a Más opciones en la sección [!UICONTROL Acciones] después de ver las opciones disponibles y pulsar la tecla `Esc` (CQ-4293592).

* Cuando activa la opción [!UICONTROL Rotar] para una imagen en el modo [!UICONTROL Editar], el enfoque de tabulación, en lugar de permanecer en Rotar, cambia a la opción [!UICONTROL Rehacer] para los usuarios del teclado (CQ-4293587).

* En el cuadro de diálogo [!UICONTROL Abrir selección] disponible en la ficha [!UICONTROL Vínculo y acciones], el enfoque de la ficha cambia a elementos ocultos en la página después de la opción [!UICONTROL Cancelar] (CQ-4293579).

* Cuando los usuarios del teclado editan una imagen, navegan a la opción [!UICONTROL Finalizar] y presionan la tecla Intro, los lectores de pantalla no anuncian la finalización (CQ-4282351).

* Las opciones Subir y Bajar disponibles en el cuadro de diálogo [!UICONTROL Vínculo y Acciones] no están disponibles para el lector de pantalla y los usuarios del teclado (CQ-4281120).

* Los usuarios del teclado no pueden restaurar el enfoque de tabulación después de navegar a la opción Cerrar (X) en la página [!UICONTROL Propiedades] (CQ-4293581, NPR-34653).

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] 6.5.7.0  [!DNL Assets] corrige los siguientes problemas y proporciona las siguientes mejoras.

* En esta versión se han realizado las siguientes mejoras para la accesibilidad en [!DNL Experience Manager Assets]. Para obtener más información, consulte [características de accesibilidad en [!DNL Assets]](/help/assets/accessibility.md).

   * Al navegar por la línea de tiempo con un teclado, la tecla `Esc` puede contraer la opción [!UICONTROL Mostrar todo] sin perder el enfoque (CQ-4293598).
   * Al navegar con la tecla de tabulación del teclado, después de quitar la última etiqueta de las etiquetas agregadas, el campo de etiqueta conserva el enfoque (NPR-35109).
   * [!DNL Experience Manager] los componentes ahora contienen la información adecuada sobre el nombre, la función y el valor que deben utilizar los lectores de pantalla (NPR-34255).
   * Después de eliminar el cuadro combinado Tipo/Tamaño, el cuadro combinado Vínculo, el cuadro combinado Idioma o el cuadro de edición de texto, el enfoque del teclado vuelve a los elementos de la interfaz de usuario siguiente o anterior o a un elemento de la interfaz de usuario más relevante (CQ-4293585).
   * Al pasar el puntero sobre las opciones, aparecen sugerencias como Seleccionar y Descargar. Es posible que los usuarios que utilizan un ampliador de pantalla no vean las miniaturas de los archivos debido a estas sugerencias. Ahora, es posible conservar el enfoque, después de eliminar la opción con la tecla `Escape`. (CQ-4293554).
   * Al seleccionar una celda de cuadrícula de la cuadrícula presente en la página, el enfoque se desplaza a la barra de acciones que aparece en la pantalla (CQ-4282127).
   * Los usuarios visuales pueden diferenciar entre texto normal y un vínculo, ya que se muestran pistas visuales (subrayado e icono de chevron) para los vínculos a todas las soluciones de la página de inicio [!DNL Experience Manager] (CQ-4282072).

* La siguiente mejora de la experiencia del usuario se realiza en [!DNL Assets]:

   * Permitir la clasificación de recursos en la vista de tarjetas y la vista de columnas (NPR-35097).

* Después de la actualización a 6.5, si se genera un archivo JSON mediante la API HTTP de Assets, hay problemas con la codificación utilizada en el archivo (NPR-35129).

* Los usuarios de un grupo al que no se ha otorgado permiso para crear colecciones (la opción Crear colección no está disponible) aún pueden crear colecciones si acceden directamente a la URL `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections` (NPR-35115).

* Cuando se ordenan por nombre, los recursos buscados se ordenan de forma que se distingue entre mayúsculas y minúsculas. Esto crea dos listas ordenadas independientes basadas en mayúsculas que aparecen de forma ordenada en los resultados de búsqueda (NPR-35068).

* Cuando se abre un fragmento de contenido en el editor, los mensajes de advertencia (`Invalid value specified for a metadata property`) se registran en los registros de errores (NPR-35012).

* Los usuarios sin privilegios de administrador pueden editar recursos caducados mediante la aplicación de escritorio [Experience Manager]. (NPR-34993).

* Cuando se arrastra el mismo recurso en la interfaz de usuario de Recursos y se crea una nueva versión, los cambios en los metadatos no son persistentes (NPR-34940).

* Al editar colecciones, un usuario puede eliminar el título de la colección y guardar correctamente los cambios (NPR-34889).

* Al cargar una imagen de duplicado, se presenta una opción de eliminación. Si selecciona Eliminar, las imágenes se pueden cargar. El flujo de trabajo de recursos de actualización DAM también se activa (NPR-34744).

* Al utilizar [!DNL Adobe Asset Link] con [!DNL Adobe InDesign], los resultados de búsqueda no contienen carpetas y colecciones, sino que solo contienen recursos (NPR-34699, CQ-4303666).

* Al pasar el puntero sobre la vista de tarjetas, la pantalla se desplaza como resultado del enfoque (automático) en las acciones rápidas disponibles en la tarjeta (NPR-34514).

* Al editar las propiedades de varios recursos de forma masiva, al seleccionar la opción [!UICONTROL Guardar] se cierra la vista del editor masivo y se redirige a la página principal [!DNL Assets]. Este comportamiento es el mismo que el de la opción [!UICONTROL Guardar y cerrar] y no se espera (NPR-34546).

* La colección inteligente no presenta la configuración de interfaz de usuario correcta después de guardar. La consulta se guarda correctamente, pero la interfaz siempre muestra el último predicado de opciones agregado (NPR-34539).

* Al agregar recursos a [!DNL Experience Manager], los metadatos sin Área de nombres no se importan (NPR-34530).

* Al arrastrar un recurso a una carpeta para moverlo, la interfaz de usuario también muestra la opción [!UICONTROL Colocar en Lightbox] y [!UICONTROL Colocar en colección]. Incluso si se cancela la operación de movimiento, la interfaz de usuario sigue mostrando las dos últimas opciones (NPR-34526).

* El símbolo `%>` se muestra en la página de colecciones (NPR-34499).

* En la vista de columnas, [!DNL Assets] muestra los nombres de duplicados y recursos al desplazarse hacia arriba y hacia abajo antes de que se muestren todos los recursos (NPR-34464).

* Si crea una carpeta privada inmediatamente después de crear una carpeta pública, la carpeta pública utiliza la configuración de la carpeta privada (NPR-34415).

* En la vista de la tarjeta, las tarjetas no aparecen en orden alfabético y las tarjetas no se pueden ordenar alfabéticamente (NPR-34234).

* Al volver a abrir las reglas en cascada, las opciones no se mantienen en la interfaz de usuario (CQ-4301452).

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* Las siguientes mejoras se realizan para la accesibilidad en [!DNL Dynamic Media] (CQ-4290306). Para obtener más información, consulte [características de accesibilidad en [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

   * Los lectores de pantalla (JAWS, Narrador) narran el nombre, la función y el estado de los elementos de menú en la opción de menú Tamaño incrustado (CQ-4290927).
   * Los usuarios pueden navegar por el cuadro de diálogo Vínculo de correo electrónico mediante la tecla `Tab` (CQ-4290926).
   * El flujo de trabajo para crear perfiles de codificación de vídeo es más sencillo de utilizar, dada la mejora del lector de pantalla (CQ-4290623, CQ-4290622).
   * Al navegar con la clave `Tab`, el enfoque se desplaza a los elementos de interfaz de usuario adecuados en el flujo de trabajo para crear un vídeo interactivo (CQ-4290621, CQ-4290620, CQ-4290619).
   * La página Publicar, la página Editar recurso, la página Editar recortes inteligentes y la página Editor de conjuntos de imágenes se han mejorado para cumplir con los estándares web. Los usuarios de tecnología de asistencia (AT) ahora pueden navegar fácilmente por estas páginas y realizar acciones como recortar imágenes (CQ-4290617, CQ-4290616, CQ-4290613, CQ-4290612, CQ-429 0610, CQ-4290614).
   * Los visores se han mejorado para permitir a los usuarios navegar con un teclado (CQ-4290615).
   * Los usuarios del teclado y del lector de pantalla pueden utilizar la funcionalidad de recorte (CQ-4290609).
   * Los usuarios del teclado pueden administrar mejor las zonas interactivas (CQ-4290604, CQ-4290603).

* Los conjuntos de imágenes remotos no se pueden editar en [!DNL Experience Manager] si el nombre de la compañía y el nombre de la carpeta son los mismos (NPR-31340).

* El orden del índice z es incorrecto cuando se intenta previsualización de la salida después de agregar una zona interactiva a una imagen [!DNL Dynamic Media] o después de editar un [!DNL Dynamic Media] vídeo o un [!DNL Experience Fragment] con una imagen (CQ-4307267).

* [!DNL Dynamic Media] la sincronización falla cuando se vuelven a procesar conjuntos de medios mixtos (CQ-4307184).

* Si un recurso se mueve a una carpeta en la que se ha configurado la sincronización automática con [!DNL Dynamic Media], el recurso no se sincroniza (CQ-4307122).

* [!DNL Dynamic Media] el vídeo no se reproduce en dispositivos iOS con los controles de vídeo HTML5 nativos (CQ-4306977, CQ-4306727).

* No se pueden descargar imágenes en las que se aplica SmartCrop (CQ-4304558).

* No se pueden publicar carpetas en Dynamic Media de forma selectiva (CQ-4304526).

* Al cancelar la publicación de un archivo de vídeo de [!DNL Experience Manager] no se cancela la publicación del conjunto de vídeos adaptable a partir de una implementación de Scene7 configurada (CQ-4304405).

* Añadir un recurso de imagen panorámica en un componente de medios panorámico y actualizar la página resulta en `Uncaught ReferenceError: $ is not defined` error (CQ-4302810).

* En el [!UICONTROL Editor de ajustes preestablecidos de visor], al editar el ajuste preestablecido [!UICONTROL PanoramicImage/PanoramicImage_VR], en el componente `PanoramicView`, la etiqueta del modificador `PANORAMICVIEW_AUTOROTATE` no está disponible (CQ-4302443).

* Los subtítulos de vídeo no se muestran si el vídeo no es el primero de un conjunto de medios mixtos (CQ-4298161).

* El visor de catálogos electrónicos HTML5 en dispositivos móviles iPhone no puede pasar las páginas ni voltearlas (CQ-4296611).

* Cuando se desplazan muestras en un dispositivo móvil, las muestras se desplazan hacia la derecha y hacia fuera del área visible durante unos segundos antes de volver a desplazarse hacia la vista (CQ-4296439).

* Cuando se crea un registro maestro de ajustes preestablecidos de visor, el CSS y la ilustración no se publican y solo se publica el ajuste preestablecido de visor (CQ-4262205).

* Al intentar vincular un fragmento de experiencias para un punto interactivo determinado en el componente [!UICONTROL Vídeo/imágenes interactivos], no muestra la ruta de fragmento de experiencias seleccionada. En su lugar, devuelve un valor vacío desde el campo de ruta (NPR-35146, CQ-4298136).

* No se puede realizar la previsualización de un fragmento de experiencia en el Editor de IVV (CQ-4308560).

* Al agregar una zona interactiva a una imagen y seleccionar un fragmento de experiencias, no es posible seleccionar las subcarpetas y las variantes del fragmento de experiencias (CQ-4307455).

* Los recursos que no son de imagen no se muestran como publicados tras la carga (CQ-4306415).

#### [!DNL Experience Manager] Recursos 3D  {#three-d-assets-6570}

* `DAM CQ MIME Type` el servicio aplica tipos MIME incorrectos a los recursos 3D que producen una representación incorrecta (NPR-34731).

### [!DNL Commerce] {#commerce-6570}

* La interfaz de usuario de la colección de productos Commerce no lista más de 15 productos dentro de una colección (NPR-34502).

### Plataforma {#platform-6570}

* No se invalida una sesión HTTP sobre HTTPS (NPR-35083).
* Se devuelve un `NullPointerException` al iniciar tareas de mantenimiento diarias o semanales desde la interfaz de usuario (NPR-34953).
* El validador de W3C informa de advertencias para archivos JavaScript de la biblioteca cliente compatibles (NPR-34898).
* La función `AudienceOmniSearchHandler` utiliza un índice obsoleto (NPR-34870).
* Al cerrar sesión en el Experience Manager no se borran las cookies (NPR-34743).
* La función `findByTitle` de la API `TagManager` no funciona si el nombre de la etiqueta contiene un carácter especial (NPR-34357).
* Error en el proceso de importación del paquete de sincronización de usuarios (NPR-34399).
* Se añadió la compatibilidad con las propiedades `ariaLabel` y `ariaLabelledby` del componente `Coral.Masonry` (GRANITE-29962).
* La caché de Dispatcher no se actualiza para páginas con fragmentos de contenido después de instalar los últimos paquetes de componentes principales (CQ-4306788).
* Los nombres de etiquetas localizados con comillas (`"`) no se muestran correctamente en la interfaz de usuario (CQ-4305439).

### Interfaz de usuario {#ui-6570}

* El campo [!UICONTROL Vínculo a] de las propiedades del componente muestra sugerencias de autocompletado que no coinciden con la cadena especificada (NPR-34865).

* AEM muestra el siguiente mensaje de error cuando programa una ventana de mantenimiento diaria distribuida entre 2 días (NPR-35280):

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### Integraciones {#integrations-6570}

* Error al editar una configuración [!DNL Adobe Launch] existente (NPR-35045).
* No se puede exportar [!DNL Experience Fragments] a [!DNL Adobe Target] si se utiliza la configuración IMS y el entorno [!DNL Adobe Target Standard] (NPR-34555).
* La opción [!UICONTROL Crear] aparece en la página [!UICONTROL Audiencias] al navegar de una carpeta a la página [!UICONTROL Audiencias] (NPR-35151).

### Sling {#sling-6570}

* La comprobación de estado de inicio de sesión predeterminada valida las credenciales de un usuario que no existe (NPR-34686).

### Proyectos de traducción {#translation-6570}

* Al cancelar un proyecto de traducción en [!DNL Experience Manager], la solicitud de cancelación no se envía al proveedor de traducción (NPR-34433).

### [!DNL Communities] {#communities-6570}

* Todos los casos de terminología no equitativa en el producto se sustituyen por equivalentes aceptados (NPR-34311).
* [!DNL Google+] se elimina de la lista de opciones de uso compartido en redes sociales (NPR-33877).

### [!DNL Brand Portal] {#brandportal-6570}

* La interfaz de usuario no responde al seleccionar los recursos en la [!UICONTROL Vista de Lista] (NPR-34728).

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>[!DNL Experience Manager Forms] libera los paquetes de complementos una semana después de la fecha de lanzamiento programada de  [!DNL Experience Manager] Service Pack.

**Formularios adaptables**

* No se puede editar un formulario adaptable mediante la IU clásica después de aplicar [!DNL Experience Manager] Service Pack 6 (NPR-35126).

* Cuando se convierte un PDF a un formulario adaptable, no se puede definir un valor para un panel anidado con un modelo de datos de formulario en la presentación con fichas. Además, hay problemas al configurar un valor para los grupos de botones de radio dinámicamente con una matriz estática mediante el editor de código (NPR-35062).

* Al introducir caracteres japoneses en un componente de campo de texto en un formulario adaptable, puede especificar más caracteres que el límite máximo de 35 caracteres (NPR-35039).

* El formulario adaptable muestra parámetros no deseados, como `owner` y `status`, en la página **[!UICONTROL Gracias]** que se muestra después de enviar el formulario (NPR-34989).

* El cuadro de diálogo [!UICONTROL Selección de archivos] para el componente [!UICONTROL Datos adjuntos] muestra los tipos de archivo no admitidos, así como la selección, lo que da como resultado un error durante el envío del formulario adaptable (NPR-34970).

* Cuando se inserta un formulario adaptable en una página [!DNL Experience Manager Sites] que incluye texto antes del formulario, el enfoque del cursor se desplaza directamente al formulario en lugar del texto anterior al formulario (NPR-34947).

* [!UICONTROL La previsualización con ] Dataoption para rellenar previamente un formulario adaptable con un archivo XML de datos  [!DNL Experience Manager] 6.2 no funciona correctamente (NPR-35087).

* Al actualizar el diccionario de datos de un formulario adaptable, el formulario no se traduce, ya que el formulario adaptable devuelve valores en caché (NPR-34845).

* Los fragmentos tardan más tiempo en cargarse en un formulario adaptable debido a la invalidación de caché (NPR-34567).

* La navegación por tabuladores no funciona correctamente para lectores de pantalla en un formulario adaptable (NPR-34544).

**Administración de correspondencia**

* No se pueden guardar los valores de las etiquetas XML con datos numéricos, que incluyen el tipo flotante, como borrador (NPR-35050).

* Al migrar los recursos desde ES3, estos incluyen dos condiciones predeterminadas no editables (NPR-34972).

* Cuando se edita un diccionario de datos en una carta, la sección [!UICONTROL Contenido de la Cuaresma] muestra rectángulos giratorios en lugar de información útil (NPR-34853).

**Comunicación interactiva**

* El nombre de configuración de implementación para Interactive Communication, disponible tras instalar el paquete de complemento [!DNL Forms], duplicado el nombre de configuración de implementación estándar (NPR-34976).

**:Seguridad de los documentos**

* Cuando se guarda una nueva directiva de seguridad de documento, Forms Experience Manager muestra el mensaje de error `Relative validity period is required` (NPR-34679).

* Cuando se guarda una nueva directiva de seguridad de documento, Forms Experience Manager muestra el mensaje de error `Invalid filed value.Numeric value is required` (NPR-34678).

* Documento Security no puede proteger el documento PDF 2.0 (CQ-4305851).

Para obtener información sobre las actualizaciones de seguridad, consulte [página de boletines de seguridad de Experience Manager](https://helpx.adobe.com/security/products/experience-manager.html).

## Instalar 6.5.7.0 {#install}

**Requisitos de configuración y más información**

* AEM 6.5.7.0 requiere AEM 6.5. Consulte [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas.
* La descarga del Service Pack está disponible en Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* En una implementación con MongoDB y varias instancias, instale AEM 6.5.7.0 en una de las instancias de creación mediante el Administrador de paquetes.

>[!NOTE]
>
>Adobe no recomienda quitar o desinstalar el paquete [!DNL Adobe Experience Manager] 6.5.7.0.

### Instalar Service Pack {#install-service-pack}

Siga los pasos siguientes para instalar Service Pack en una instancia de Adobe Experience Manager 6.5 existente:

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (y este es el caso cuando la instancia se actualizó desde una versión anterior). Adobe también recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de realizar la instalación, realice una instantánea o una copia de seguridad nueva de la instancia [Experience Manager].

1. Descargue el Service Pack desde [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip).

1. Abra el Administrador de paquetes y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

1. Para actualizar el conector S3, detenga la instancia después de instalar el Service Pack, sustituya el conector existente por un nuevo archivo binario proporcionado en la carpeta de instalación y reinicie la instancia. Consulte [Almacén de datos Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo en la interfaz de usuario del administrador de paquetes a veces se cierra durante la instalación del Service Pack. Adobe recomienda que espere a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete de actualización antes de asegurarse de que la instalación se realiza correctamente. Generalmente, esto sucede en [!DNL Safari] pero puede suceder de manera intermitente en cualquier explorador.

**Instalación automática**

Existen dos formas de instalar automáticamente Adobe Experience Manager 6.5.7.0 en una instancia de trabajo:

A. Coloque el paquete en la carpeta `../crx-quickstart/install` cuando el servidor esté disponible en línea. El paquete se instala automáticamente.

B. Utilice la [API HTTP del Administrador de paquetes](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html). Utilice `cmd=install&recursive=true` para instalar los paquetes anidados.

>[!NOTE]
>
>Adobe Experience Manager 6.5.7.0 no admite la instalación de Bootstrap.

**Validar la instalación**

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.7.0)` en [!UICONTROL Productos instalados].

1. Todos los paquetes OSGi son **[!UICONTROL ACTIVE]** o **[!UICONTROL FRAGMENT]** en la consola OSGi (utilice la consola web: `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.3 o posterior (utilice la consola web: `/system/console/bundles`).

Para conocer las plataformas certificadas para trabajar con esta versión, consulte los [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

### Instalación del paquete de complementos de Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>[!DNL Experience Manager Forms] libera los paquetes de complementos una semana después de la fecha de lanzamiento programada de  [!DNL Experience Manager] Service Pack.

>[!NOTE]
>
>Omita este paso si no utiliza AEM Forms. Las correcciones en Adobe Experience Manager Forms se entregan a través de un paquete adicional independiente.

1. Asegúrese de que ha instalado Adobe Experience Manager Service Pack.
1. Descargue el paquete adicional de Forms correspondiente en [AEM Forms releases](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html) para su sistema operativo.
1. Instale el paquete de complementos de Forms como se describe en [Instalación de paquetes de complementos de AEM Forms](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Instalar Adobe Experience Manager Forms en JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Omita este paso si no utiliza AEM Forms en JEE. Las correcciones en Adobe Experience Manager Forms en JEE se entregan a través de un instalador independiente.

Para obtener información sobre la instalación acumulativa del instalador para Experience Manager Forms en JEE y la configuración posterior a la implementación, consulte las [notas de la versión](jee-patch-installer-65.md).

### UberJar {#uber-jar}

UberJar para Experience Manager 6.5.7.0 está disponible en el [repositorio de Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.7/).

Para usar UberJar en un proyecto de Maven, consulte [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM del proyecto:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.7</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar y los otros artefactos relacionados están disponibles en el repositorio de Maven Central en lugar del repositorio de Maven Público de Adobe (`repo.adobe.com`). Se cambia el nombre del archivo principal de UberJar a `uber-jar-<version>.jar`. Por lo tanto, no hay `classifier`, con `apis` como valor, para la etiqueta `dependency`.

## Funciones en desuso {#removed-deprecated-features}

A continuación se muestra una lista de funciones y funcionalidades que se marcan como obsoletas con [!DNL Experience Manager] 6.5.7.0. Las funciones se marcan como obsoletas inicialmente y posteriormente se eliminan en una versión futura. Normalmente se proporciona una opción alternativa.

Revise si utiliza una función o una capacidad en una implementación. Además, planee cambiar la implementación para utilizar una opción alternativa.

| Área | Función | Reemplazo |
|---|---|---|
| Integraciones | La pantalla **[!UICONTROL AEM Cloud Services Opt-In]** está en desuso. Con la integración de AEM y Destinatario actualizada en AEM 6.5 para admitir la API de Target Standard, que utiliza la autenticación mediante IMS y E/S de Adobe, y el creciente papel de Inicio de Adobe para instrumentar páginas AEM para análisis y personalización, el asistente para la inclusión se ha vuelto funcionalmente irrelevante. | Configure las conexiones del sistema, la autenticación IMS de Adobe y las integraciones de Adobe I/O mediante los respectivos servicios de nube de AEM. |
| Conectores | El conector JCR de Adobe para Microsoft SharePoint 2010 y Microsoft SharePoint 2013 está en desuso para AEM 6.5. | N/D |

## Problemas conocidos {#known-issues}

* Ignore los siguientes errores en el archivo `error.log` durante la instalación de Experience Manager 6.5.7.0:

   ```TXT
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy(1314)] : Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy(1316)] : Could not load implementation object class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy(1315)] : Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy)
   ```

* Si está actualizando la instancia [!DNL Experience Manager] de la versión 6.5 a la versión 6.5.7.0, puede vista de las excepciones `RRD4JReporter` en el archivo `error.log`. Reinicie la instancia para resolver el problema.

* Si instala [!DNL Experience Manager] 6.5 Service Pack 5 o un Service Pack anterior en [!DNL Experience Manager] 6.5, se elimina la copia en tiempo de ejecución del modelo de flujo de trabajo personalizado de recursos (creado en `/var/workflow/models/dam`).
Para recuperar la copia del tiempo de ejecución, Adobe recomienda sincronizar la copia en tiempo de diseño del modelo de flujo de trabajo personalizado con su copia en tiempo de ejecución mediante la API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Póngase en contacto con el Servicio de atención al cliente de Adobe si tiene problemas al editar y crear reglas en cascada en [!UICONTROL Esquema de metadatos de carpeta Editor de Forms] y [!UICONTROL Editor de Forms para Esquemas de metadatos] mediante el cuadro de diálogo [!UICONTROL Definir regla]. Las reglas que ya se han creado y guardado funcionan correctamente.

* Si se cambia el nombre de una carpeta en la jerarquía en [!DNL Experience Manager Assets] y la carpeta anidada que contiene un recurso se publica en [!DNL Brand Portal], el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Cuando un usuario selecciona configurar un campo por primera vez en un formulario adaptable, la opción para guardar una configuración no se muestra en el navegador de propiedades. Si selecciona configurar otro campo del formulario adaptable en el mismo editor, se resuelve el problema.

* Si el asistente [!UICONTROL Configuración de recursos conectados] devuelve un mensaje de error 404 después de la instalación, vuelva a instalar manualmente los paquetes `cq-remotedam-client-ui-content` y `cq-remotedam-client-ui-components` mediante el Administrador de paquetes.

* Durante la instalación de AEM 6.5.x.x pueden aparecer los siguientes errores y mensajes de advertencia:
   * &quot;Cuando la integración de Target se configura en AEM mediante la API de Target Standard (autenticación IMS), la exportación de fragmentos de experiencia a Target provoca la creación de tipos de ofertas incorrectos. En lugar de tener que escribir &quot;Fragmento de experiencias&quot;/origen &quot;Adobe Experience Manager&quot;, Destino, se crean varias ofertas con el tipo &quot;HTML&quot;/origen &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La validación del lado del servidor de Formulario adaptable falla cuando se utilizan funciones acumuladas como SUM, MAX y MIN. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La zona interactiva de una imagen interactiva de Dynamic Media no está visible al obtener una vista previa del recurso a través del visor de pancarta de ventas.

## Paquetes y paquetes de contenido OSGi incluidos {#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en AEM 6.5.7.0:

* [Lista de paquetes OSGi incluidos en AEM 6.5.7.0](assets/6570_bundles.txt)

* [Lista de paquetes de contenido incluidos en AEM 6.5.7.0](assets/6570_packages.txt)

## Sitios web restringidos {#restricted-sites}

Estos sitios web solo están disponibles para los clientes. Si es un cliente y necesita obtener acceso, póngase en contacto con su administrador de cuentas de Adobe.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/)
* Consulte [cómo comunicarse con el servicio de atención al cliente](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Notas de la versión 6.5](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] página del producto](https://www.adobe.com/es/marketing/experience-manager.html)
>* [[!DNL Experience Manager] 6.5 documentación](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* Suscríbase a [actualizaciones de productos con prioridad de Adobe](https://www.adobe.com/subscription/priority-product-update.html)

